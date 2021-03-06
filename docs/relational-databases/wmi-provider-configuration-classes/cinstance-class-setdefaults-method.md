---
description: CInstance 类 - SetDefaults 方法
title: 'SetDefaults 方法 (CInstance) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (CInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: ed9e99c2-3e28-4ee8-bc20-61ca05984973
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 99771d12be4c10d8d4b823ceb788e9722d417fca
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91890977"
---
# <a name="cinstance-class---setdefaults-method"></a>CInstance 类 - SetDefaults 方法
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  设置客户端实例的所有默认值， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并提供覆盖现有数据的选项。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示 [客户端实例的](../../relational-databases/wmi-provider-configuration-classes/cinstance-class.md) CInstance 类 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
#### <a name="parameters"></a>参数  
  
|参数|说明|  
|---------------|-----------------|  
|*OverwriteAll*|指定是否覆盖客户端实例上的现有值的布尔值：如果为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **true 则** 覆盖现有数据，则为 **false** ; 如果不覆盖现有数据，则为 false。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端协议](../../database-engine/configure-windows/configure-client-protocols.md)  
  
