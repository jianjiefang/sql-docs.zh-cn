---
title: sp_set_firewall_rule （Azure SQL Database） |Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_set_firewall_rule
- sp_set_firewall_rule_TSQL
- sys.sp_set_firewall_rule
- sys.sp_set_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_firewall_rule
- firewall_rules, setting server rules
ms.assetid: a974a561-5382-4039-8499-3a56767bcefe
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 9bc37626879b743eb3a5d0864490dc3543a8d8a9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "70152066"
---
# <a name="sp_set_firewall_rule-azure-sql-database"></a>sp_set_firewall_rule (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  创建或更新您的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器的服务器级防火墙设置。 此存储过程仅在 master 数据库中可用于服务器级主体登录名或分配 Azure Active Directory 主体。  
  
  
## <a name="syntax"></a>语法  
  
```
sp_set_firewall_rule [@name =] 'name', 
    [@start_ip_address =] 'start_ip_address', 
    [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 下表说明了中[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]支持的参数和选项。  
  
|名称|数据类型|说明|  
|----------|--------------|-----------------|  
|[@name =]路径名|**NVARCHAR （128）**|用来描述和区分服务器级防火墙设置的名称。|  
|[@start_ip_address =]"start_ip_address"|**VARCHAR （50）**|服务器级防火墙设置范围内的最低 IP 地址。 等于或大于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器。 可能的最低 IP 地址为 `0.0.0.0`。|  
|[@end_ip_address =]"end_ip_address"|**VARCHAR （50）**|服务器级防火墙设置范围内的最高 IP 地址。 等于或小于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器。 可能的最高 IP 地址为 `255.255.255.255`。<br /><br /> 注意：如果此字段和*start_ip_address*字段都等于`0.0.0.0`，则允许 Azure 连接尝试。|  
  
## <a name="remarks"></a>备注  
 服务器级防火墙设置的名称必须是唯一的。 如果为存储过程提供的设置的名称在防火墙设置表中已经存在，则将更新开始和结束 IP 地址。 否则，将创建新的服务器级防火墙设置。  
  
 若添加的服务器级防火墙设置的起始和结束 IP 地址均为 `0.0.0.0`，此时支持从 Azure 访问你的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器。 为*name*参数提供一个值，该值有助于记住服务器级防火墙设置的用途。  
  
 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中，对连接和服务器级别的防火墙规则进行身份验证时所需的登录数据会暂时缓存在每个数据库中。 此缓存定期刷新。 若要强制刷新身份验证缓存并确保数据库具有最新版本的登录名表，请执行 [DBCC FLUSHAUTHCACHE (Transact-SQL)](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)。  
  
## <a name="permissions"></a>权限  
 只有由设置过程创建的服务器级别主体登录名或分配为管理员的 Azure Active Directory 主体才能创建或修改服务器级防火墙规则。 用户必须连接到 master 数据库才能执行 sp_set_firewall_rule。  
  
## <a name="examples"></a>示例  
 以下代码创建了支持从 Azure 进行访问的名为 `Allow Azure` 的服务器级防火墙设置。 在虚拟 master 数据库中执行以下。  
  
```  
-- Enable Azure connections.  
exec sp_set_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 以下代码仅为 IP 地址 `Example setting 1` 创建一个称为 `0.0.0.2` 的服务器级防火墙设置。 然后，再次`sp_set_firewall_rule`调用此存储过程，将该防火墙设置中的结束`0.0.0.4`IP 地址更新为。 这会创建一个范围，该范围`0.0.0.2`允许`0.0.0.3`IP 地址`0.0.0.4` 、和访问服务器。  
  
```  
-- Create server-level firewall setting for only IP 0.0.0.2  
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.2';  
  
-- Update server-level firewall setting to create a range of allowed IP addresses
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.4';  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [Azure SQL Database 防火墙](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [如何：配置防火墙设置（Azure SQL Database）](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [firewall_rules &#40;Azure SQL 数据库&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)
