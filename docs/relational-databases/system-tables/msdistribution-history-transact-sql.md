---
title: MSdistribution_history （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistribution_history
- MSdistribution_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_history system table
ms.assetid: 55665bd2-9e1d-4efc-8f60-c63a24f66b28
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 979175ee4495f885f77600d530c57800ff69e624
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82805477"
---
# <a name="msdistribution_history-transact-sql"></a>MSdistribution_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdistribution_history**表包含与本地分发服务器关联的分发代理的历史记录行。 此表存储在分发数据库中。  
  
## <a name="definition"></a>定义  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|分发代理的 ID。|  
|**runstatus**|**int**|运行状态：<br /><br /> **1** = 启动。<br /><br /> **2** = 成功。<br /><br /> **3** = 正在进行。<br /><br /> **4** = 空闲。<br /><br /> **5** = 重试。<br /><br /> **6** = 失败。|  
|**start_time**|**datetime**|开始执行作业的时间。|  
|**time**|**datetime**|记录消息的时间。|  
|**duration**|**int**|消息会话的持续时间（秒）。|  
|**注释**|**nvarchar(4000)**|消息文本。|  
|**xact_seqno**|**varbinary(16)**|上次处理的事务序列号。|  
|**current_delivery_rate**|**float**|自从最后一个历史记录条目后，平均每秒传送的命令数。|  
|**current_delivery_latency**|**int**|自从最后一个历史记录条目后，命令从进入分发数据库到应用于订阅服务器之间的滞后时间。 以毫秒为单位。|  
|**delivered_transactions**|**int**|会话中传递的事务总数。|  
|**delivered_commands**|**int**|会话中传递的命令总数。|  
|**average_commands**|**int**|会话中传递的平均命令数。|  
|**delivery_rate**|**float**|平均每秒传递的命令数。|  
|**delivery_latency**|**int**|命令从进入分发数据库到应用于订阅服务器之间的滞后时间。 以毫秒为单位。|  
|**total_delivered_commands**|**bigint**|创建订阅后所传递的命令总数。|  
|**error_id**|**int**|**MSrepl_error**系统表中的错误的 ID。|  
|**updateable_row**|**bit**|如果可以覆盖历史记录行，则设置为**1** 。|  
|**timestamp**|**timestamp**|该表的时间戳列。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
