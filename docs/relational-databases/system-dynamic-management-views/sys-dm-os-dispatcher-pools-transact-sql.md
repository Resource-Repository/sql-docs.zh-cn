---
description: sys.dm_os_dispatcher_pools (Transact-SQL)
title: sys.dm_os_dispatcher_pools (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_dispatcher_pools_TSQL
- dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], views
- sys.dm_os_dispatcher_pools DMV
ms.assetid: b9edbc83-c6bc-4753-9bb5-a454cfe7d6bf
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 352fe048404c452cc7f6012a166e395f4731f38a
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97321885"
---
# <a name="sysdm_os_dispatcher_pools-transact-sql"></a>sys.dm_os_dispatcher_pools (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  返回有关会话调度程序池的信息。 调度程序池是由系统组件用来执行后台处理的线程池。  
  
> [!NOTE]  
>  若要从或调用此 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ，请使用名称 **sys.dm_pdw_nodes_os_dispatcher_pools**。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|dispatcher_pool_address|**varbinary(8)**|调度程序池的地址。 dispatcher_pool_address 是唯一的。 不可为 null。|  
|类型|**nvarchar(256)**|调度程序池的类型。 不可为 null。 有两种类型的调度程序池：<br /><br /> DISP_POOL_XE_ENGINE<br /><br /> DISP_POOL_XE_SESSION<br /><br /> 查询 DMV 以获取完整列表|  
|name|**nvarchar(256)**|调度程序池的名称。 不可为 null。|  
|dispatcher_count|**int**|处于活动状态的调度程序线程数。 不可为 null。|  
|dispatcher_ideal_count|**int**|调度程序池通过增大可使用的调度程序线程数。 不可为 null。|  
|dispatcher_timeout_ms|**int**|调度程序将在退出之前等待新工作的时间（以毫秒为单位）。 不可为 null。|  
|dispatcher_waiting_count|**int**|空闲的调度程序线程数。 不可为 null。|  
|queue_length|**int**|等待由调度程序池处理的工作项数。 不可为 null。|  
|pdw_node_id|**int**|**适用** 于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分发所在的节点的标识符。|  
  
## <a name="permissions"></a>权限

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 权限。   
在 SQL 数据库的基本、S0 和 S1 服务目标以及弹性池中的数据库上， `Server admin` `Azure Active Directory admin` 需要或帐户。 对于所有其他 SQL 数据库服务目标， `VIEW DATABASE STATE` 数据库中需要该权限。   

## <a name="see-also"></a>另请参阅  
  
  


