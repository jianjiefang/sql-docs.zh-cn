---
title: sys. dm_exec_query_plan_stats （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_plan_stats
- sys.dm_exec_query_plan_stats_TSQL
- dm_exec_query_plan_stats_TSQL
- dm_exec_query_plan_stats
helpviewer_keywords:
- sys.dm_exec_query_plan_stats management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfacb
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 279f1a8fbe3ec78dc0cae30d9879615b169075bf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "75656989"
---
# <a name="sysdm_exec_query_plan_stats-transact-sql"></a>sys. dm_exec_query_plan_stats （Transact-sql）
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

返回以前缓存的查询计划的上一个已知实际执行计划的等效值。

## <a name="syntax"></a>语法

```
sys.dm_exec_query_plan_stats(plan_handle)  
``` 

## <a name="arguments"></a>参数 
*plan_handle*  
是一个标记，用于唯一标识已执行并且其计划驻留在计划缓存中或当前正在执行的批处理的查询执行计划。 *plan_handle*为**varbinary （64）**。   

可以从以下动态管理对象中获取*plan_handle* ：  
  
-   [sys.dm_exec_cached_plans (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [sys. dm_exec_procedure_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [sys. dm_exec_trigger_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  

## <a name="table-returned"></a>返回的表

|列名|数据类型|说明|  
|-----------------|---------------|-----------------|
|**dbid**|**smallint**|在编译对应于此计划的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句时有效的上下文数据库的 ID。 对于临时和预定义 SQL 语句，指编译这些语句时所在的数据库的 ID。<br /><br /> 此列可为空值。|  
|**objectid**|**int**|此查询计划的对象（如存储过程或用户定义函数）的 ID。 对于即席批处理和已准备好的批处理，此列为 **null**。<br /><br /> 此列可为空值。|  
|**数字**|**smallint**|为存储过程编号的整数。 例如，用于 **orders** 应用程序的一组过程可命名为 **orderproc;1**、**orderproc;2** 等等。 对于即席批处理和已准备好的批处理，此列为 **null**。<br /><br /> 此列可为空值。|  
|**过**|**bit**|指示对应的存储过程是否已加密。<br /><br /> 0 = 未加密<br /><br /> 1 = 已加密<br /><br /> 此列不可为空值。|  
|**query_plan**|**xml**|包含与*plan_handle*一起指定的实际查询执行计划的上一个已知运行时显示计划表示形式。 显示计划的格式为 XML。 为包含即席 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句、存储过程调用以及用户定义函数调用等内容的每个批查询生成一个计划。<br /><br /> 此列可为空值。| 

## <a name="remarks"></a>备注
从[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.4 开始，此系统函数可用。

这是一个选择加入功能，并且需要启用[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451。 自 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.5 起，若要在数据库级别完成此操作，请参阅 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 中的 LAST_QUERY_PLAN_STATS 选项。

此系统函数在**轻型**查询执行统计信息分析基础结构下工作。 有关详细信息，请参阅[查询分析基础结构](../../relational-databases/performance/query-profiling-infrastructure.md)。  

Sys. dm_exec_query_plan_stats 的显示计划输出包含以下信息：
-  在缓存计划中找到的所有编译时信息
-  运行时信息，例如每个运算符的实际行数、查询总 CPU 时间和执行时间，溢出警告，实际 DOP，最大已用内存和授予的内存

在以下条件下，与**实际执行计划等效**的显示计划输出将在返回的表的**query_plan**列中返回**dm_exec_query_plan_stats**：  

-   可在[sys. dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)中找到该计划。     
    **AND**    
-   正在执行的查询是复杂的或消耗资源的查询。

在以下情况下，将在返回的表的**query_plan**列中返回**sys.databases 为 dm_exec_query_plan_stats**的**简化<sup>1</sup> **显示计划输出：  

-   可在[sys. dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)中找到该计划。     
    **AND**    
-   查询非常简单，通常归类为 OLTP 工作负载的一部分。

<sup>1</sup>从[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.5 开始，这是指仅包含根节点运算符（SELECT）的显示计划。 对于[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.4，这是指通过`sys.dm_exec_cached_plans`获取的缓存计划。

在以下条件下，**不从 sys.databases 返回任何输出** **dm_exec_query_plan_stats**：

-   使用*plan_handle*指定的查询计划已从计划缓存中逐出。     
    **或**    
-   最初无法缓存查询计划。 有关详细信息，请参阅[执行计划缓存和重复使用](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)。
  
> [!NOTE] 
> 由于**xml**数据类型中允许的嵌套级别数有限制，因此**dm_exec_query_plan**无法返回满足或超过128嵌套元素级别的查询计划。 在的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]早期版本中，此条件阻止查询计划返回，并生成[错误 6335](../../relational-databases/errors-events/database-engine-events-and-errors.md#errors-6000-to-6999)。 在[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 及更高版本中， **QUERY_PLAN**列返回 NULL。  

## <a name="permissions"></a>权限  
 要求具有对服务器的 `VIEW SERVER STATE` 权限。  

## <a name="examples"></a>示例  
  
### <a name="a-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan"></a>A. 查看特定缓存计划的上一个已知实际查询执行计划  
 下面的示例查询**dm_exec_cached_plans sys.databases**以查找有趣的计划，并从输出`plan_handle`复制其。  
  
```sql  
SELECT * FROM sys.dm_exec_cached_plans;  
GO  
```  
  
然后，若要获取最后一个已知的实际查询执行计划，请`plan_handle`使用复制的与系统函数**sys.databases dm_exec_query_plan_stats**。  
  
```sql  
SELECT * FROM sys.dm_exec_query_plan_stats(< copied plan_handle >);  
GO  
```   

### <a name="b-looking-at-last-known-actual-query-execution-plan-for-all-cached-plans"></a>B. 查看所有缓存计划的最后已知实际查询执行计划
  
```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps;  
GO  
```   

### <a name="c-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan-and-query-text"></a>C. 查看特定缓存计划和查询文本的上一个已知实际查询执行计划

```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps
WHERE st.text LIKE 'SELECT * FROM Person.Person%';  
GO  
```   

### <a name="d-look-at-cached-events-for-trigger"></a>D. 查看触发器的缓存事件

```sql
SELECT *
FROM sys.dm_exec_cached_plans
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle)
WHERE objtype ='Trigger';
GO
```

## <a name="see-also"></a>另请参阅
  [跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [动态管理视图和函数 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与执行相关的动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  

