---
description: Type 属性 (ADO)
title: ) ADO (类型属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Type
- Field20::Type
helpviewer_keywords:
- Type property [ADO]
ms.assetid: 8a4c079f-9f4f-4545-801d-85983b8db71e
author: rothja
ms.author: jroth
ms.openlocfilehash: 9f4dcfd3c22363ab4950e03844647f990a34f4d5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988308"
---
# <a name="type-property-ado"></a>Type 属性 (ADO)
指示 [参数](./parameter-object.md)、 [字段](./field-object.md)或 [属性](./property-object-ado.md) 对象的操作类型或数据类型。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个 [DataTypeEnum](./datatypeenum.md) 值。  
  
## <a name="remarks"></a>注解  
 对于 **参数** 对象， **类型** 属性是可读/写的。 对于附加到[记录](./record-object-ado.md)的[字段](./fields-collection-ado.md)集合的新**字段**对象，在指定了**字段**的[值](./value-property-ado.md)属性并且数据提供程序已通过调用**Fields**集合的[Update](./update-method.md)方法成功添加了新**字段**之后，**类型**为 read/write。  
  
 对于所有其他对象， **Type** 属性为只读。  
  
## <a name="applies-to"></a>适用于  

:::row:::
    :::column:::
        [字段对象](./field-object.md)  
    :::column-end:::
    :::column:::
        [Parameter 对象](./parameter-object.md)  
    :::column-end:::
    :::column:::
        [属性对象 (ADO)](./property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅  
 [ () VB)  (字段的 Type 属性示例 ](./type-property-example-field-vb.md)   
 [ (VC + +) 的类型属性示例 () ](./type-property-example-property-vc.md)   
 [RecordType 属性 (ADO) ](./recordtype-property-ado.md)   
 [Type 属性（ADO 流）](./type-property-ado-stream.md)