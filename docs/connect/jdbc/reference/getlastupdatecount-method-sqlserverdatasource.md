---
description: getLastUpdateCount 方法 (SQLServerDataSource)
title: getLastUpdateCount 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c4fbb24-0b02-42da-928c-a903bb591cc7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 44b5b9c19b07479aaeae6eb400d3212accd3e5fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435769"
---
# <a name="getlastupdatecount-method-sqlserverdatasource"></a>getLastUpdateCount 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回一个指示是否启用 lastUpdateCount 属性的 Boolean**** 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean getLastUpdateCount()  
```  
  
## <a name="return-value"></a>返回值  
 如果启用了 lastUpdateCount，则为 true****。 否则为 **false**。  
  
## <a name="remarks"></a>备注  
 如果将 lastUpdateCount 属性设置为 true****，则 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 将只返回由 SQL 语句传递给服务器的最后更新计数。 如果将 lastUpdateCount 属性设置为 false****，则驱动程序将返回所有更新计数，包括任何可能已不再使用的触发器所返回的更新计数。 如果未设置 lastUpdateCount 属性，则 getLastUpdateCount 方法将返回默认值 true****。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
