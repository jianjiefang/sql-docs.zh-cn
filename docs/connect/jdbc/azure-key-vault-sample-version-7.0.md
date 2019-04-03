---
title: Azure 密钥保管库示例 |Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8fa94368a4242e7a02781a5283d5cbf15f25b2a2
ms.sourcegitcommit: a9a03f9a7ec4dad507d2dfd5ca33571580114826
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2019
ms.locfileid: "58567536"
---
# <a name="azure-key-vault-sample"></a>Azure 密钥保管库示例

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="sample-application-using-azure-key-vault-feature"></a>使用 Azure 密钥保管库功能的示例应用程序

此应用程序是可运行使用 JDBC 驱动程序 7.0 及更高版本和 Azure key Vault （版本 1.0.0），Adal4j （版本 1.6.0），以及其依赖项。  可通过将这些库添加到项目的 pom 文件中，如所述解决基本依赖关系[此处](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md):

```java
import java.net.URISyntaxException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.HashMap;
import java.util.Map;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionAzureKeyVaultProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerConnection;
import com.microsoft.sqlserver.jdbc.SQLServerException;
import com.microsoft.sqlserver.jdbc.SQLServerKeyVaultAuthenticationCallback;

public class AKV {

    static String connectionUrl = "jdbc:sqlserver://localhost;integratedSecurity=true;database=test;columnEncryptionSetting=enabled";
    static String applicationClientID = "Your Client ID";
    static String applicationKey = "Your Application Key";
    static String keyID = "Your Key ID";
    static String cmkName = "AKV_CMK_JDBC";
    static String cekName = "AKV_CEK_JDBC";
    static String akvTable = "akvTable";

    static String createTableSQL = "create table " + akvTable + " ("
            + "PlainNvarcharMax nvarchar(max) null,"
            + "RandomizedNvarcharMax nvarchar(max) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256', COLUMN_ENCRYPTION_KEY = "
            + cekName + ") NULL,"
            + "DeterministicNvarcharMax nvarchar(max) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256', COLUMN_ENCRYPTION_KEY = "
            + cekName + ") NULL" + ");";

    public static void main(String[] args)
            throws ClassNotFoundException, Exception {
        Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
        try (Connection connection = DriverManager.getConnection(connectionUrl);
                Statement statement = connection.createStatement()) {
            statement.execute("DBCC FREEPROCCACHE");

            System.out.println("Create SQLServerColumnEncryptionAzureKeyVaultProvider with 'authenticationCallback' and 'executorService(null)'");
            /* Constructor added in 6.0.0 driver version and removed in 6.2.2 driver, now added back in 7.0.0 driver
             * [Supports SQLServerKeyVaultAuthenticationCallback in 7.0 for backwards compatibility]
             * This constructor is marked @deprecated since it no longer uses 'ExecutorService' parameter passed. */
            @SuppressWarnings("deprecation")
            SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider1 = new SQLServerColumnEncryptionAzureKeyVaultProvider(
                    tryAuthenticationCallback(), null);
            setupKeyStoreProviders(akvProvider1.getName(), akvProvider1);
            testAKV(akvProvider1.getName(), akvProvider1, connection, statement);

            statement.execute("DBCC FREEPROCCACHE");
            System.out.println("Create SQLServerColumnEncryptionAzureKeyVaultProvider with 'authenticationCallback'");
            /* Constructor added in 7.0.0 driver version [Supports SQLServerKeyVaultAuthenticationCallback in 7.0 for backwards compatibility]
             * This constructor is recommended to replace the above deprecated constructor */
            SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider2 = new SQLServerColumnEncryptionAzureKeyVaultProvider(
                    tryAuthenticationCallback());
            testAKV(akvProvider2.getName(), akvProvider2, connection, statement);

            statement.execute("DBCC FREEPROCCACHE");
            System.out.println("Create SQLServerColumnEncryptionAzureKeyVaultProvider with 'clientId' and 'clientKey'");
            /* Constructor added in 6.2.2 driver version [Continued Support] */
            SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider3 = new SQLServerColumnEncryptionAzureKeyVaultProvider(
                    applicationClientID, applicationKey);
            testAKV(akvProvider3.getName(), akvProvider3, connection, statement);
            System.exit(0);
        }
    }

    private static SQLServerKeyVaultAuthenticationCallback tryAuthenticationCallback()
            throws URISyntaxException, SQLServerException {
        SQLServerKeyVaultAuthenticationCallback authenticationCallback = new SQLServerKeyVaultAuthenticationCallback() {

            @Override
            public String getAccessToken(String authority, String resource,
                    String scope) {
                AuthenticationResult result = null;
                try {
                    ExecutorService service = Executors.newFixedThreadPool(1);
                    AuthenticationContext context = new AuthenticationContext(
                            authority, false, service);
                    ClientCredential cred = new ClientCredential(
                            applicationClientID, applicationKey);
                    Future<AuthenticationResult> future = context
                            .acquireToken(resource, cred, null);
                    result = future.get();
                    service.shutdown();
                } catch (Exception e) {
                    e.printStackTrace();
                }
                return result.getAccessToken();
            }
        };

        return authenticationCallback;

    }

    private static void testAKV(String CUSTOM_AKV_PROVIDER_NAME,
            SQLServerColumnEncryptionKeyStoreProvider akvProvider,
            Connection connection, Statement statement)
            throws SQLException, InterruptedException {

        dropTable(statement);
        dropKeys(statement);

        System.out.println("createCMK");
        createCMK(CUSTOM_AKV_PROVIDER_NAME, statement);

        System.out.println("createCEK");
        createCEK(akvProvider, statement);

        System.out.println("create Table");
        statement.execute(createTableSQL);

        System.out.println("populate");
        populateCharNormalCase(connection);

        System.out.println("run the test");
        testChar(statement);
    }

    private static void setupKeyStoreProviders(String CUSTOM_AKV_PROVIDER_NAME,
            SQLServerColumnEncryptionKeyStoreProvider akvProvider)
            throws SQLServerException {
        Map<String, SQLServerColumnEncryptionKeyStoreProvider> map1 = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
        map1.put(CUSTOM_AKV_PROVIDER_NAME, akvProvider);
        SQLServerConnection.registerColumnEncryptionKeyStoreProviders(map1);
    }

    private static void dropTable(Statement statement) throws SQLException {
        statement.executeUpdate("if object_id('" + akvTable
                + "','U') is not null" + " drop table " + akvTable);
    }

    private static void dropKeys(Statement statement) throws SQLException {
        statement.executeUpdate(
                "if exists (SELECT name from sys.column_encryption_keys where name='"
                        + cekName + "')" + " begin"
                        + " drop column encryption key " + cekName + " end");
        statement.executeUpdate(
                "if exists (SELECT name from sys.column_master_keys where name='"
                        + cmkName + "')" + " begin" + " drop column master key "
                        + cmkName + " end");
    }

    private static void createCMK(String CUSTOM_AKV_PROVIDER_NAME,
            Statement statement) throws SQLException {
        String _createColumnMasterKeyTemplate = String.format(
                "CREATE COLUMN MASTER KEY [%s] WITH ( KEY_STORE_PROVIDER_NAME = '%s', KEY_PATH = '%s');",
                cmkName, CUSTOM_AKV_PROVIDER_NAME, keyID);
        statement.execute(_createColumnMasterKeyTemplate);
    }

    private static void createCEK(
            SQLServerColumnEncryptionKeyStoreProvider storeProvider,
            Statement statement) throws SQLServerException, SQLException {
        String letters = "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa";
        byte[] valuesDefault = letters.getBytes();
        byte[] key = storeProvider.encryptColumnEncryptionKey(keyID, "RSA_OAEP",
                valuesDefault);
        String cekSql = "CREATE COLUMN ENCRYPTION KEY " + cekName
                + " WITH VALUES " + "(COLUMN_MASTER_KEY = " + cmkName
                + ", ALGORITHM = 'RSA_OAEP', ENCRYPTED_VALUE = 0x"
                + bytesToHexString(key, key.length) + ")" + ";";
        statement.execute(cekSql);
    }

    final static char[] hexChars = {'0', '1', '2', '3', '4', '5', '6', '7', '8',
            '9', 'A', 'B', 'C', 'D', 'E', 'F'};

    private static String bytesToHexString(byte[] b, int length) {
        StringBuilder sb = new StringBuilder(length * 2);
        for (int i = 0; i < length; i++) {
            int hexVal = b[i] & 0xFF;
            sb.append(hexChars[(hexVal & 0xF0) >> 4]);
            sb.append(hexChars[(hexVal & 0x0F)]);
        }
        return sb.toString();
    }

    private static void populateCharNormalCase(Connection connection)
            throws SQLException {
        String sql = "insert into " + akvTable + " values(?,?,?)";
        try (PreparedStatement pstmt = connection.prepareStatement(sql)) {
            for (int i = 1; i <= 5; i++) { //Insert 5 rows
                for (int j = 1; j <= 3; j++) {
                    pstmt.setNString(j, "Row " + i + " Column " + j);
                }
                pstmt.execute();
            }
        }
    }

    /**
     * Rerieves the table
     *
     * @throws SQLException
     */
    private static void testChar(Statement statement) throws SQLException {
        try (ResultSet rs = statement
                .executeQuery("select * from " + akvTable);) {
            int numberOfColumns = rs.getMetaData().getColumnCount();
            while (rs.next()) {
                for (int i = 1; i <= numberOfColumns; i++) {
                    System.out.println(rs.getString(i));
                }
            }
        }
    }
}
```

## <a name="see-also"></a>另请参阅

[Azure Key Vault 示例版本 6.2.2](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md)  
[Azure Key Vault 示例版本 6.0.0](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md)  