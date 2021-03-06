---
description: ODBC 驱动程序管理器生成的事件
title: ODBC 驱动程序管理器生成的事件 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], events generated by
- Visual Studio Analyzer [ODBC], driver manager events
ms.assetid: 8c6efbbd-2c7d-4342-aa7b-201f94b3e3e3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2259867b2291299b5bed35536637a7968118e87b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482920"
---
# <a name="events-generated-by-the-odbc-driver-manager"></a>ODBC 驱动程序管理器生成的事件
> [!IMPORTANT]  
>  从 Windows 8 (中开始，从 Windows 8 Visual Studio Analyzer 中删除了对 Visual Studio Analyzer 的支持，只包含在较早版本的 Visual Studio 中 ) 。 有关备用故障排除机制，请使用投标跟踪。  
  
 当单击 "开始 Visual Studio Analyzer" 按钮时，将注册 ODBC 驱动程序管理器生成的事件。 该工具本身提供系统定义的事件以及创建自定义事件的能力。 有关事件的详细信息，请参阅 Visual Studio 文档中的 *Visual Studio Analyzer 参考指南* 。  
  
|Visual Studio Analyzer 事件|描述|  
|----------------------------------|-----------------|  
|**调用**|针对每个 ODBC API 条目生成。|  
|**ReturnException**|如果返回代码为 SQL_ERROR，则在每个 ODBC API 返回时生成。|  
|**ReturnNormal**|如果未 SQL_ERROR 返回代码，则在每个 ODBC API 返回时生成。|  
|**连接开始**|指示连接已启动;ODBC 驱动程序管理器调用驱动程序的连接 Api 时生成。|  
|**连接完成**|指示连接已完成;驱动程序的连接 Api 返回到 ODBC 驱动程序管理器时生成。|  
|**断开连接开始**|ODBC 驱动程序管理器调用驱动程序的 **SQLDisconnect** 函数时生成。|  
|**断开连接完成**|驱动程序的 **SQLDisconnect** 函数返回到 ODBC 驱动程序管理器时生成。|  
|**QuerySend**|ODBC 驱动程序管理器调用驱动程序的 **SQLPrepare**、 **SQLExecute**、 **SQLExecDirect** 函数以及目录函数（如 **SQLTables** 和 **SQLColumns**）时生成。|  
|**QueryResult**|当驱动程序将结果集返回到 ODBC 驱动程序管理器中涉及查询的函数时生成。|  
|**TransactionStart**|当应用程序将 SQL_ATTR_AUTOCOMMIT 的值设置为 SQL_AUTOCOMMIT_OFF 时，或在应用程序成功调用 **SQLEndTran**后生成。|  
|**TransactionCommit**|当应用程序调用 **SQLEndTran** 来提交本地事务时生成。|  
|**TransactionRollback**|当应用程序调用 **SQLEndTran** 回滚本地事务时生成。|  
|**JoinDTC**|当应用程序将分布式事务处理协调器加入 (DTC) 时生成。|  
|**LeaveDTC**|当应用程序离开分布式事务处理协调器 (DTC) 时生成。|
