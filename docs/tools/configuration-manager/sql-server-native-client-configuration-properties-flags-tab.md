---
title: SQL Server Native Client 配置属性（“标志”选项卡）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 59af121d-c8b9-4faa-91a1-b664f2c9b441
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 4d8fd24d496c9a9fd42422aa9e46d26ddb27f062
ms.sourcegitcommit: c37777216fb8b464e33cd6e2ffbedb6860971b0d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82087440"
---
# <a name="sql-server-native-client-configuration-properties-flags-tab"></a>SQL Server Native Client 配置属性（“标志”选项卡）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 库文件中提供的协议与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务器进行通信。 使用本页可将客户端计算机配置为使用传输层安全性 (TLS)（以前称为“安全套接字层 (SSL)”）请求加密的连接。 如果无法建立加密的连接，则连接将失败。  
  
 登录过程始终是加密的。 以下选项仅适用于加密数据。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如何对通信进行加密的详细信息，以及有关如何将客户端配置为信任服务器证书的根证书颁发机构的说明，请参阅“[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的加密连接”以及“如何：启用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的加密连接（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器）”（在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中）。  
  
## <a name="options"></a>选项  
 **强制协议加密**  
 使用 TLS 请求连接。  
  
 **信任服务器证书**  
 当设置为  “否”时，客户端进程将尝试验证服务器证书。 客户端和服务器均必须拥有公共证书颁发机构颁发的证书。 如果客户端计算机上没有证书，或如果验证证书失败，则连接将终止。  
  
 当设置为  “是”时，客户端不会验证服务器证书，而是使用自签名证书。  
  
 仅在“强制协议加密”  设置为“是”  时，才可使用“信任服务器证书”  。  
  
  
