---
title: MSmerge_conflict_publication_article （T-sql）
description: 介绍 MSmerge_conflict_publication_article 存储过程，该存储过程包含有关发生冲突的行的信息，或者为实现数据收敛而撤消的行更改。
ms.custom: seo-lt-2019
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_conflict_publication_article_TSQL
- MSmerge_conflict_publication_article
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflict_publication_article system table
ms.assetid: dc4490b4-02d8-4dfc-98f5-0cf8de8e11be
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 070b8cfe44190f89db8e7adf142debbc29e64d15
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829236"
---
# <a name="msmerge_conflict_publication_article-transact-sql"></a>MSmerge_conflict_publication_article （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_conflict_publication_article**表包含有关发生冲突的行的信息，或者为实现数据收敛而撤消的行更改的信息。 对于发布中的每个复制表都存在一个冲突表，而冲突表的名称附加有发布和项目的名称。 这些项目特定的冲突表存储在用于进行冲突日志记录的数据库中，通常是发布数据库，但如果冲突日志记录分散，也可以是订阅数据库。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**_文章 \_ 列 \_ 名称_**|**各种**|表示复制表中的一列。 在该系统表中，表项目中的每列对应一列。|  
|**rowguid**|**uniqueidentifier**|冲突行的行标识符。|  
|**ModifiedDate**|**datetime**|发生冲突的时间。|  
|**源 \_ 数据源 \_ id**|**uniqueidentifier**|为其撤销行更改或失去冲突的订阅。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
