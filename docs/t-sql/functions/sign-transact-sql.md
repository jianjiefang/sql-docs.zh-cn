---
title: SIGN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SIGN_TSQL
- SIGN
dev_langs:
- TSQL
helpviewer_keywords:
- '- (negative)'
- + (positive sign)
- zero (0)
- SIGN function
- positive values [SQL Server]
- 0 (zero)
- negative values
ms.assetid: c3a98b52-6fbe-4127-a5c9-8a4922e83e28
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ec2e33afb82d3b3a733f98670c20de36681eabfa
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828583"
---
# <a name="sign-transact-sql"></a>SIGN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回指定表达式的正号 (+1)、零 (0) 或负号 (-1)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
SIGN ( numeric_expression )  
```  
  

## <a name="arguments"></a>参数  
 *numeric_expression*  
 是精确或近似数值数据类型类别（bit 数据类型除外）的[表达式](../../t-sql/language-elements/expressions-transact-sql.md)  。  
  
## <a name="return-types"></a>返回类型  
  
|指定的表达式|返回类型|  
|--------------------------|-----------------|  
|**bigint**|**bigint**|  
|**int/smallint/tinyint**|**int**|  
|**money/smallmoney**|**money**|  
|**numeric/decimal**|**numeric/decimal**|  
|**其他类型**|**float**|  
  
## <a name="examples"></a>示例  
 以下示例返回从 -1 到 1 的 SIGN 数值。  
  
```  
DECLARE @value real  
SET @value = -1  
WHILE @value < 2  
   BEGIN  
      SELECT SIGN(@value)  
      SET NOCOUNT ON  
      SELECT @value = @value + 1  
      SET NOCOUNT OFF  
   END  
SET NOCOUNT OFF  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
(1 row(s) affected)  
  
------------------------   
-1.0                       
  
(1 row(s) affected)  
  
------------------------   
0.0                        
  
(1 row(s) affected)  
  
------------------------   
1.0                        
  
(1 row(s) affected)  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 以下示例返回三个数字的 SIGN 值。  
  
```  
SELECT SIGN(-125), SIGN(0), SIGN(564);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
-----  -----  -----  
-1     0      1
```  
  
## <a name="see-also"></a>另请参阅  
 [数学函数 (Transact-SQL)](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  

