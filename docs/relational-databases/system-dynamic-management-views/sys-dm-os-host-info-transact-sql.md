---
title: sys. dm_os_host_info （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 02/10/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_os_host_info
- sys.dm_os_host_info_TSQL
- dm_os_host_info
- dm_os_host_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_host_info dynamic management view
ms.assetid: 9bb6ef86-957b-4ca1-ad20-ca2f8460a86d
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8275ed39d49c8fdb64c1d2f26cc1d218c525500c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830505"
---
# <a name="sysdm_os_host_info-transact-sql"></a>sys. dm_os_host_info （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

返回一个显示操作系统版本信息的行。  
  
|列名称 |数据类型 |说明 |  
|-----------------|---------------|-----------------|  
|**host_platform** |**nvarchar(256)** |操作系统的类型： Windows 或 Linux |
|**host_distribution** |**nvarchar(256)** |操作系统的说明。 |
|**host_release**|**nvarchar(256)**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 操作系统版本（版本号） 有关值和说明的列表，请参阅[操作系统版本（Windows）](/windows/desktop/SysInfo/operating-system-version)。 <br> 对于 Linux，返回一个空字符串。 |  
|**host_service_pack_level**|**nvarchar(256)**|Windows 操作系统的 Service Pack 级别。 <br> 对于 Linux，返回一个空字符串。 |  
|**host_sku**|**int**|Windows 单品 (SKU) ID。 有关 SKU Id 和说明的列表，请参阅[GetProductInfo 函数](https://msdn.microsoft.com/library/ms724358.aspx)。 可以为 Null。 <br> 对于 Linux，返回 NULL。 |  
|**os_language_version**|**int**|操作系统的 Windows 区域设置标识符 (LCID)。 有关 LCID 值和说明的列表，请参阅[Microsoft 分配的区域设置 id](https://go.microsoft.com/fwlink/?LinkId=208080)。 不可为 null。|  

## <a name="remarks"></a>备注  
此视图类似于[sys. dm_os_windows_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)，添加了用于区分 Windows 和 Linux 的列。
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
`SELECT` `sys.dm_os_host_info` `public` 默认情况下，对角色授予权限。 如果已吊销，则需要 `VIEW SERVER STATE` 对服务器的权限。   
 
> [!CAUTION]
>  从版本 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.3 开始， [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 版本17需要 `SELECT` 权限才能 `sys.dm_os_host_info` 连接到 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 。 如果 `SELECT` 撤消了权限 `public` ，则只有具有权限的登录名 `VIEW SERVER STATE` 可以连接到最新版本的 SSMS。 （其他工具（例如 `sqlcmd.exe` ）无需 `SELECT` 权限即可连接 `sys.dm_os_host_info` 。）

  
## <a name="examples"></a>示例  
 下面的示例返回**sys.databases dm_os_host_info**视图中的所有列。  
  
```  
SELECT host_platform, host_distribution, host_release, 
    host_service_pack_level, host_sku, os_language_version  
FROM sys.dm_os_host_info;  
```  

下面是有关 Windows 的示例结果集：
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Windows   |Windows Server 2012 R2 Standard    |6.3    |   |7  |2052 |  

下面是 Linux 上的示例结果集：
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Linux |Ubuntu |16.04  |   |Null   |2052 |  

  
## <a name="see-also"></a>另请参阅  
 [sys. dm_os_sys_info &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_windows_info (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)  
 

