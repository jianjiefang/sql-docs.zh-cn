---
title: sys. server_sql_modules （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.server_sql_modules
- sys.server_sql_modules_TSQL
- server_sql_modules_TSQL
- server_sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_sql_modules catalog view
ms.assetid: 9ef9a8b9-c470-4a61-b0c4-ee24ad871d63
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bd4eba56c6550f4a3ae8b033dbd81b71ac7b5418
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82821389"
---
# <a name="sysserver_sql_modules-transact-sql"></a>sys.server_sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含类型为 TR 的服务器级别触发器的 SQL 模块设置。 可将此关系与 sys.server_triggers 联接。 元组 (object_id) 是关系键。  
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|这是返回给定义该模块的服务器级别触发器的 FOREIGN KEY 引用。|  
|**definition**|**nvarchar(max)**|定义此模块的 SQL 文本。<br /><br /> NULL = 已加密。|  
|**uses_ansi_nulls**|**bit**|模块是通过将 ANSI NULLS 设置选项设置为 ON 而创建的。|  
|**uses_quoted_identifier**|**bit**|模块是通过将 QUOTED IDENTIFIER 设置选项设置为 ON 而创建的。|  
|**execute_as_principal_id**|**int**|EXECUTE AS 服务器主体的 ID。<br /><br /> 默认情况下或在 EXECUTE AS CALLER 情况下，值为 NULL。<br /><br /> 指定主体的 ID （如果 EXECUTE AS principal execute as principal-2 = 作为所有者执行）。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
