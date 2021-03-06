---
title: 获取驱动程序版本 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e241d72-16da-4ada-ac67-e6308394108f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1a1c5c6d4dcc3a5bd5acaac37ffdcdadc184e497
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924659"
---
# <a name="getting-the-driver-version"></a>获取驱动程序版本
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  可以通过以下方法找到已安装 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 的版本：  
  
-   调用 [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 方法 [getDriverMajorVersion](../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md)、[getDriverMinorVersion](../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md) 或 [getDriverVersion](../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md)。  
  
-   版本将显示在产品分发内容的 readme.txt 文件中。  
  
 此外，可以通过在 SQLServerDatabaseMetaData 类上调用 [getDriverName](../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md) 方法来返回 JDBC 驱动程序名称。 例如，将返回“Microsoft JDBC Driver 6.4 for SQL Server”。  
  
 以下是调用 SQLServerDatabaseMetaData 类的各个方法所输出的内容示例：  
  
 `getDriverName = Microsoft JDBC Driver 6.4 for SQL Server`  
  
 `getDriverMajorVersion = 6`  
  
 `getDriverMinorVersion = 4`  
  
 `getDriverVersion = 6.4.` *xxx.x*  
  
 其中，“xxx.x”是最终版本号。  
  
## <a name="see-also"></a>另请参阅  
 [诊断 JDBC 驱动程序问题](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
