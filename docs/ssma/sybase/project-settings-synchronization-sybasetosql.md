---
title: 项目设置（同步）（SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2cd6bc01-b8e5-4312-83a4-eac66dc1d460
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 663a4b1e49d1f81ce040254a2c8f39a1a1f84b38
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68028684"
---
# <a name="project-settings-synchronization-sybasetosql"></a>项目设置（同步）(SybaseToSQL)
"**项目设置**" 对话框的 "同步" 页包含用于自定义 SSMA 将数据库对象（如表和存储过程）加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 的方式的设置。  
  
您可以访问两个包含相同设置的不同同步页：  
  
-   如果要为所有未来的 SSMA 项目指定设置，请在 "**工具**" 菜单上，选择 "**默认项目设置**"，从 "**迁移目标版本**" 下拉框中选择需要查看或更改其设置的迁移项目类型，然后选择左窗格底部的 "**同步**"。  
  
-   若要指定当前项目的设置，请在 "**工具**" 菜单上选择 "**项目设置**"，然后选择左窗格底部的 "**同步**"。  
  
## <a name="options"></a>选项  
**多次**  
指定在将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时 SSMA 应执行的尝试次数。 当前尝试中未加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的对象将重试，直到 SSMA 达到当前同步过程中的最大尝试次数。  
  
## <a name="synchronization-for-sql-server"></a>SQL Server 同步  
**刷新本地对象和远程对象更改**  
指定在本地对象和远程对象均更改时，SSMA 是否应将本地对象元数据替换为远程对象元数据。  
如果选择 "**从数据库刷新**"，则在满足条件时，SSMA 会将数据库定义加载到元数据中。  
如果选择了 "**写入数据库**"，则在满足条件时，SSMA 将根据 SSMA 元数据内容来更新数据库中的对象。  
如果选择 "**跳过**"，SSMA 不会执行任何刷新操作。   
默认选项集是**写入数据库。**  
  
**在本地对象更改时刷新本地对象**  
指定在远程对象发生更改时，SSMA 是否应将本地对象元数据替换为远程对象元数据。  
如果选择 "**从数据库刷新**"，则在满足条件时，SSMA 会将数据库定义加载到元数据中。  
如果选择 "**写入数据库**"，则在满足条件时，SSMA 会根据 SSMA 元数据内容更新数据库中的对象。  
如果选择 "**跳过**"，SSMA 不会执行任何刷新操作。   
默认选项集是**写入数据库**。  
  
**刷新远程对象的本地对象更改**  
指定在远程对象发生更改时，SSMA 是否应将本地对象元数据替换为远程对象元数据。  
如果选择 "**从数据库刷新**"，则在满足条件时，SSMA 会将数据库定义加载到元数据中。  
如果选择 "**写入数据库**"，则在满足条件时，SSMA 会根据 SSMA 元数据内容更新数据库中的对象。  
如果选择 "**跳过**"，SSMA 不会执行任何刷新操作。   
**从数据库刷新**默认选项集。  
  
**当缺少本地对象元数据时刷新**  
指定 SSMA 是否应在目标数据库上存在对象而不是本地对象时创建本地元数据。  
如果选择 "**从数据库刷新**"，则在满足条件时，SSMA 将选择 "从数据库刷新" 选项。  
如果选择 "**写入数据库**"，则在满足条件时，SSMA 将从数据库中删除该对象。  
如果选择 "**跳过**"，SSMA 不会执行任何刷新操作。   
**从数据库刷新**默认选项集。  
  
