---
title: xp_sscanf （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_sscanf_TSQL
- xp_sscanf
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sscanf
ms.assetid: 619a9df1-7008-407e-a75a-bc6f851454a8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e46fe3243f39f8783743bf11e08b6368d67116eb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68091903"
---
# <a name="xp_sscanf-transact-sql"></a>xp_sscanf (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将数据从字符串读入每个格式参数所指定的参数位置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
xp_sscanf { string OUTPUT , format } [ ,argument [ ,...n ] ]   
```  
  
## <a name="arguments"></a>参数  
 **string**  
 要从中读取参数值的字符串。  
  
 OUTPUT  
 指定时，将*参数*值放入 output 参数中。  
  
 *format*  
 格式的字符串，类似于 C 语言**sscanf**函数支持的字符串。 目前仅支持 %s 格式参数。  
  
 argument   
 一个**varchar**变量，它设置为相应*格式*参数的值。  
  
 *n*  
 是一个占位符，指示最多可指定 50 个参数。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 **xp_sscanf**返回以下消息：  
  
 `Command(s) completed successfully.`  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 以下示例使用 `xp_sscanf` 从源字符串提取两个值（根据它们在源字符串格式中的位置）。  
  
```  
DECLARE @filename varchar (20), @message varchar (20);  
EXEC xp_sscanf 'sync -b -fproducts10.tmp -rrandom', 'sync -b -f%s -r%s',   
  @filename OUTPUT, @message OUTPUT;  
SELECT @filename, @message;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------- --------------------   
products10.tmp        random  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;系统存储过程](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;的常规扩展存储过程](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_sprintf &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-sprintf-transact-sql.md)  
  
  
