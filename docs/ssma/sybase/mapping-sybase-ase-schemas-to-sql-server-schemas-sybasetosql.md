---
title: 将 Sybase ASE 架构映射到 SQL Server 架构（SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Schema Mapping
ms.assetid: 2c927003-c49d-4fe1-8e3e-5b2899166268
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5c39e81f8faffed606e6ca94315c47d383174c91
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68028867"
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>将 Sybase ASE 架构映射到 SQL Server 架构 (SybaseToSQL)
在 Sybase 自适应服务器企业（ASE）中，每个数据库都有一个或多个架构。 默认情况下，SSMA 将数据库和架构中的所有对象迁移到或 SQL Azure 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的相同数据库和架构。 不过，你可以自定义 ASE 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 数据库与架构之间的映射。  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>ASE、SQL Server 或 SQL Azure 架构  
ASE 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 都通过使用两部分表示法作为*数据库*来指定数据库及其架构。 例如，在 ASE**演示**数据库中，可能有一个**dbo**架构。 该数据库和架构对指定为**demo. dbo**。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 具有相同的数据库和架构，则该对也指定为**demo. dbo**。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目标数据库和架构  
在 SSMA 中，可以将 ASE 架构映射到任何可用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 架构。  
  
**修改数据库和架构**  
  
1.  在 Sybase 元数据资源管理器中，选择 "**数据库**"。  
  
    选择单个数据库、"**架构**" 文件夹或单独的架构时，还可以使用 "**架构映射**" 选项卡。 为所选对象自定义 "**架构映射**" 选项卡中的列表。  
  
2.  在右侧窗格中，单击 "**架构映射**" 选项卡。  
  
    你将看到所有 ASE 数据库的列表及其架构，后跟目标值。 此目标以两部分表示法（*数据库*）表示，其中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 将迁移对象和数据的位置。  
  
3.  选择包含要更改的映射的行，然后单击 "**修改**"。  
  
4.  在 "**选择目标架构**" 对话框中，您可以浏览可用目标数据库和架构，或在两部分表示法（数据库架构）的文本框中键入数据库和架构名称，然后单击 **"确定"**。  
  
5.  "**架构映射**" 选项卡上的目标更改。  
  
**映射模式**  
  
-   映射到 SQL Server  
  
您可以将源数据库映射到任何目标数据库。 默认情况下，源数据库映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 SSMA 连接的目标数据库。 如果要映射的目标数据库在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不存在，则系统会提示你提供消息 **"目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据中不存在数据库和/或架构。它将在同步过程中创建。是否要继续？ "** 单击“是”。 同样，你可以将架构映射到目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库下将在同步过程中创建的非现有架构。  
  
-   映射到 SQL Azure  
  
您可以将源数据库映射到连接的目标 SQL Azure 数据库或连接的目标 SQL Azure 数据库中的任何架构。 如果将源架构映射到已连接目标数据库下的任何非现有架构，则系统会提示您输入消息 **"目标元数据中不存在架构"。它将在同步过程中创建。是否要继续？"** 单击" 是 "。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>恢复到默认数据库和架构  
如果自定义 ASE 架构与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 架构之间的映射，则可以将映射恢复为默认值。  
  
**恢复为默认数据库和架构**  
  
1.  在 "架构映射" 选项卡下，选择任意行，然后单击 "**重置为默认值**" 以还原为默认数据库和架构。  
  
## <a name="next-steps"></a>后续步骤  
如果要分析 Sybase ASE 对象到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 对象的转换，可以[创建转换报告](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md)。 否则，可以[将 ASE 数据库对象定义转换](converting-sybase-ase-database-objects-sybasetosql.md)为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 对象定义。  
  
## <a name="see-also"></a>另请参阅  
[将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
