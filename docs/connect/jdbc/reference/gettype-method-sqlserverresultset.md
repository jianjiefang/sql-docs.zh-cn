---
title: getType 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ffbc4a02-e851-431c-bc1a-7ab381d982bb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e66f027245ce27bd89be03128bb6731cc8810af3
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80911123"
---
# <a name="gettype-method-sqlserverresultset"></a>getType 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的游标类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getType()  
```  
  
## <a name="return-value"></a>返回值  
 指示当前游标类型的 int  值，可取值如下：  
  
 ResultSet.TYPE_FORWARD_ONLY  
  
 ResultSet.TYPE_SCROLL_INSENSITIVE  
  
 ResultSet.TYPE_SCROLL_SENSITIVE  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getType 方法是由 java.sql.ResultSet 接口中的 getType 方法指定的。  
  
 此方法可以用于确定实际游标类型。 如果应用程序选择了 TYPE_FORWARD_ONLY 或使用了默认游标类型，将返回 TYPE_FORWARD_ONLY。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
