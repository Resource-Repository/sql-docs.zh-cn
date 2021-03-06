---
description: PropertyValType 属性（ServerNetworkProtocolProperty 类）
title: 'PropertyValType 属性 (ServerNetworkProtocolProperty) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- PropertyValType Property (ServerNetworkProtocolProperty
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PropertyValType property
ms.assetid: fbd42e8e-0642-4a19-b3c8-6ce88345145f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 812801e3a966ec1c2eb5d89c2ca54bb00f47e1c2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89517287"
---
# <a name="propertyvaltype-property-servernetworkprotocolproperty-class"></a>PropertyValType 属性（ServerNetworkProtocolProperty 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取存储在所引用属性中的值的数据类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.PropertyValType [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示实例上的网络协议属性的 [ServerNetworkProtocolProperty 类](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolproperty-class/servernetworkprotocolproperty-class.md) 对象 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 指定属性值的数据类型的 **uint32** 值。 如果是字符串值类型，则返回 0；如果是数值类型，则返回 1。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
