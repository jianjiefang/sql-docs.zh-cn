---
title: 连接到数据源（用于 Oracle 的 ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connecting to data sources
ms.assetid: f724a9c5-342a-4f4e-a030-ec34f7378eaf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6ef567c9e3c7b63e7f5044de699750de856f3e52
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81281297"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>连接到数据源（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 ODBC 应用程序可以通过多种方式传递连接信息。 例如，应用程序可能会让驱动程序始终提示用户输入连接信息。 或者，应用程序可能需要一个指定数据源连接的连接字符串。 连接到数据源的方式取决于 ODBC 应用程序所使用的连接方法。  
  
 连接到数据源的一种常用方法是通过 "数据源" 对话框。 如果 ODBC 应用程序设置为使用对话框，则会显示该对话框，并提示您输入适当的数据源连接信息。  
  
 你还可以使用[连接字符串](../../odbc/microsoft/connection-string-format-and-attributes.md)连接到数据源。  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>使用对话框连接到数据源  
  
1.  出现 "数据源" 对话框时，选择 Oracle 数据源，然后单击 "确定"。 此时将显示“连接”对话框。  
  
2.  填写 "连接" 对话框的相应信息，然后单击 "确定"。  
  
 验证连接信息后，应用程序可以使用 Oracle 的 ODBC 驱动程序访问数据源所包含的信息。
