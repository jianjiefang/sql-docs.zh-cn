---
title: catalog.environment_variables（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 45f5aacd-505a-443b-8fc2-c7929e78cff8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fdb7a7c325a6189feaea690fe2cc22d685ba86e6
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296660"
---
# <a name="catalogenvironment_variables-ssisdb-database"></a>catalog.environment_variables（SSISDB 数据库）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中所有环境的环境变量详细信息。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|variable_id|**bigint**|环境变量的唯一标识符 (ID)。|  
|environment_id|**bigint**|与环境变量关联的环境的唯一 ID。|  
|name|**sysname**|环境变量的名称。|  
|description|**nvarchar(1024)**|环境变量的说明。|  
|type|**nvarchar(128)**|环境变量的数据类型。|  
|sensitive|**bit**|当值为 `1` 时，变量是敏感的并在存储时加密。 当值为 `0` 时，变量是不敏感的并以纯文本形式存储值。|  
|值|**sql_variant**|环境变量的值。 当 sensitive 为 `0` 时，显示纯文本值。 当 sensitive 为 `1` 时，显示 **NULL** 值。|  
  
## <a name="remarks"></a>备注  
 此视图对于目录中的每个环境变量显示一行。  
  
## <a name="permissions"></a>权限  
 此视图需要下列权限之一：  
  
-   针对相应环境的 READ 权限  
  
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  
  
> [!NOTE]  
>  当您具有在服务器上执行操作的权限时，您还具有查看有关此操作的信息的权限。 将实施行级安全性；只显示您有权查看的行。  
  
  
