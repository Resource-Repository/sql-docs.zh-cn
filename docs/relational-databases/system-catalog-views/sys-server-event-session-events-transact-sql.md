---
description: sys.server_event_session_events (Transact-SQL)
title: sys. server_event_session_events (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_event_session_events
- server_event_session_events_TSQL
- sys.server_event_session_events
- sys.server_event_session_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_session_events catalog view
- xe
ms.assetid: 75986e91-1fc7-4f14-98ac-4e90154a74db
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d7f58a80a3d3d85fd7411d629d9d018a40002641
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551399"
---
# <a name="sysserver_event_session_events-transact-sql"></a>sys.server_event_session_events (Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  返回事件会话中每个事件所对应的行。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|事件会话的 ID。 不可为 null。|  
|event_id|**int**|事件的 ID。 此 ID 在事件会话对象中是唯一的。 不可为 null。|  
|name|**sysname**|事件的名称。 不可为 null。|  
|包|**sysname**|包含事件的事件包的名称。 不可为 null。|  
|name|**sysname**|包含事件的模块的名称。 不可为 null。|  
|predicate|**nvarchar (3000) **|应用于事件的谓词表达式。 可以为 Null。|  
|predicate_xml|**nvarchar (3000) **|应用于事件的 XML 谓词表达式。 可以为 Null。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="remarks"></a>备注  
 此视图具有下列关系基数。  
  
| From | 到 | 关系 |
| ---- | -- | ------------ |
|sys.server_event_session_events.event_session_id|sys. server_event_sessions event_session_id|多对一|  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [&#40;Transact-sql&#41;的扩展事件目录视图 ](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [扩展事件](../../relational-databases/extended-events/extended-events.md)  
  
  
