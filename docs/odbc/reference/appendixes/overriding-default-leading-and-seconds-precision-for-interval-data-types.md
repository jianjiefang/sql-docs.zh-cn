---
title: 对于间隔数据类型重写前导和秒精度 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: 3d65493f-dce7-4d29-9f59-c63a4e47918c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e60d5d8fc696ad8e2bd4cfb0c082ff214e066d0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303598"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>重写间隔数据类型的默认前导和秒精度
当 ARD 的 SQL_DESC_TYPE 字段设置为 datetime 或 interval C 类型时，通过调用**SQLBindCol**或**SQLSetDescField**，SQL_DESC_PRECISION 字段（其中包含间隔秒精度）设置为以下默认值：  
  
-   6表示时间戳，使用另一个组件的所有时间间隔数据类型。  
  
-   对于所有其他数据类型为0。  
  
 对于所有间隔数据类型，包含时间间隔前导字段精度的 SQL_DESC_DATETIME_INTERVAL_PRECISION 描述符字段均设置为默认值2。  
  
 当 APD 中的 SQL_DESC_TYPE 字段设置为 datetime 或 interval C 类型时，通过调用**SQLBindParameter**或**SQLSetDescField**，APD 中的 "SQL_DESC_PRECISION" 和 "SQL_DESC_DATETIME_INTERVAL_PRECISION" 字段将设置为先前给定的默认值。 这适用于输入参数，但不适用于输入/输出参数或输出参数。  
  
 对**SQLSetDescRec**的调用会将间隔的精度设置为默认值，但会将间隔秒精度（在 SQL_DESC_PRECISION 字段中）设置为其*精度*参数的值。  
  
 如果某个应用程序不接受以前给定的任何一个默认值，则该应用程序应通过调用**SQLSetDescField**来设置 SQL_DESC_PRECISION 或 SQL_DESC_DATETIME_INTERVAL_PRECISION 字段。  
  
 如果应用程序调用**SQLGetData**将数据返回到 datetime 或 interval C 类型，则将使用默认的间隔的精度和间隔秒精度。 如果任何一个默认值都不是可接受的，则应用程序必须调用**SQLSetDescField**来设置描述符字段，或将**SQLSetDescRec**设置为 SQL_DESC_PRECISION。 对**SQLGetData**的调用应有一个 SQL_ARD_TYPE *TargetType*来使用 "描述符" 字段中的值。  
  
 调用**SQLPutData**时，将从与执行时数据参数或列相对应的说明符记录字段中读取时间间隔的精度和间隔秒精度，这些字段是对**SQLExecute**或**SQLExecDirect**调用的 APD 字段，或者是对**ARD**或**SQLBulkOperations**的调用的 SQLSetPos 字段。
