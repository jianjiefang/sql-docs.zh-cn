---
title: getProcedureTerm 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getProcedureTerm
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3336d4c1-d999-43cc-b36b-ff1532e899bc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f86809112c7eb156772c85f639944f8390f3e587
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925196"
---
# <a name="getprocedureterm-method-sqlserverdatabasemetadata"></a>getProcedureTerm 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索与此数据库中的“过程”对应的首选术语。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getProcedureTerm()  
```  
  
## <a name="return-value"></a>返回值  
 包含过程术语的 String  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getProcedureTerm 方法是由 java.sql.DatabaseMetaData 接口中的 getProcedureTerm 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
