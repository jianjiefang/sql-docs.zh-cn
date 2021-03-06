---
title: core. sp_add_collector_type （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_collector_type
- sp_add_collector_type_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- core.sp_add_collector_type stored procedure
- management data warehouse, data collector stored procedures
- sp_add_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 1d981037-2147-464e-a456-7d8e479bce89
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2e8d56f2959b78779f4ef8761053eab61cb7dd58
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829666"
---
# <a name="coresp_add_collector_type-transact-sql"></a>core.sp_add_collector_type (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  向管理数据仓库数据库中的 core.supported_collector_types 视图中添加一个新条目。 必须在管理数据仓库数据库的上下文中执行此过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
core.sp_add_collector_type [ @collector_type_uid = ] 'collector_type_uid'  
```  
  
## <a name="arguments"></a>参数  
 [ @collector_type_uid =] "*collector_type_uid*"  
 收集器类型的 GUID。 *collector_type_uid*是**uniqueidentifier**，没有默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="permissions"></a>权限  
 需要**mdw_admin** （具有 EXECUTE 权限）固定数据库角色的成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例向 core.supported_collector_types 视图中添加一般 T-SQL 查询收集器类型。 默认情况下，一般 T-SQL 查询收集器类型已经存在。 因此，如果在默认安装上运行这些代码，则您将会收到一条消息，指出该收集器类型已存在。  
  
 如果您已通过使用 core.sp_remove_collector_type 存储过程删除了一般 T-SQL 查询收集器类型，之后又希望将它重新添加为可以向管理数据仓库上载数据的已注册收集器类型，则这些代码可以成功运行。  
  
```  
USE <management_data_warehouse>;  
GO  
DECLARE @RC int;  
DECLARE @collector_type_uid uniqueidentifier;  
SELECT @collector_type_uid = (SELECT collector_type_uid FROM msdb.dbo.syscollector_collector_types WHERE name = N'Generic T-SQL Query Collector Type');  
EXECUTE @RC = core.sp_add_collector_type @collector_type_uid;  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;系统存储过程](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;的数据收集器存储过程](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [管理数据仓库](../../relational-databases/data-collection/management-data-warehouse.md)  
  
  
