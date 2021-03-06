---
title: sys. dm_hadr_auto_page_repair （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 02/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_hadr_auto_page_repair_TSQL
- sys.dm_hadr_auto_page_repair
- sys.dm_hadr_auto_page_repair_TSQL
- dm_hadr_auto_page_repair
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- automatic page repair
- sys.dm_hadr_auto_page_repair dynamic management view
ms.assetid: d7840adf-4a1b-41ac-bc94-102c07ad1c79
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4cd78dd4ef6e5d5b718a98c73a75b55dd548ac85
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830568"
---
# <a name="sysdm_hadr_auto_page_repair-transact-sql"></a>sys.dm_hadr_auto_page_repair (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  为针对任何可用性数据库（位于服务器实例为任何可用性组承载的可用性副本上）的每一个自动页修复尝试都返回一行。 该视图包含对应于给定主/辅助数据库上最新自动页修复尝试的行，每个数据库最多可对应 100 行。 只要一个数据库对应的行达到最大值，则它的下个自动页修复尝试对应的行将替换现有的一个项。
  
  下表定义了各列的含义：  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|此行对应的数据库的 ID。|  
|**file_id**|**int**|页所在文件的 ID。|  
|**page_id**|**bigint**|文件中页的 ID。|  
|**error_type**|**int**|错误类型。 值可以是：<br /><br /> **-** 1 = 所有硬件823错误<br /><br /> 1 = 错误的校验和或页撕裂以外的 824 错误（例如，错误的页 ID）<br /><br /> 2 = 错误的校验和<br /><br /> 3 = 页撕裂|  
|**page_status**|**int**|页修复尝试的状态：<br /><br /> 2 = 排队等候来自伙伴的请求。<br /><br /> 3 = 请求已发送到伙伴。<br /><br /> 4 = 已成功修复页面。<br /><br /> 5 = 上一次尝试时无法修复页面/自动页修复将再次尝试修复页面。|  
|**modification_time**|**datetime**|页状态最后发生更改的时间。|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [自动页面修复 &#40;可用性组：数据库镜像&#41;](../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [suspect_pages &#40;Transact-sql&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
 [管理 suspect_pages 表 (SQL Server)](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  

