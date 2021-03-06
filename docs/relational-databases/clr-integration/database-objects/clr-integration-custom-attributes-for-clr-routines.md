---
title: CLR 例程的自定义属性 |Microsoft Docs
description: 自定义特性可应用于 CLR 例程、用户定义类型和在 Microsoft SQL Server 中注册的用户定义聚合。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- SqlFacet attribute
- SqlTrigger attribute
- SqlProcedure attribute
- custom attributes [CLR integration]
- SqlUserDefinedAggregate attribute
- attributes [CLR integration]
- SqlMethod attribute
- SqlFunction attribute
- common language runtime [SQL Server], attributes
- SqlUserDefinedTypeAttribute attribute
ms.assetid: 95069d22-b05d-4670-b053-15ee2a664e33
author: rothja
ms.author: jroth
ms.openlocfilehash: bad209c4ddb516167b8048ae73680bc9ea59cc05
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810801"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>CLR 例程的 CLR 集成自定义属性
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  列出的属性可应用于公共语言运行时 (CLR) 例程、用户定义类型和在中注册的用户定义聚合 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 如果未应用此属性，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将采用默认值。 列出的属性在 **Microsoft sql** 命名空间中定义。  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>SqlUserDefinedAggregate 特性  
 **SqlUserDefinedAggregate**特性指示应将方法注册为用户定义的聚合。 必须使用此属性注释每个用户定义聚合。  
  
 有关详细信息，请参阅 [SqlUserDefinedAggregateAttribute](/dotnet/api/microsoft.sqlserver.server.sqluserdefinedaggregateattribute)。  
  
## <a name="the-sqlfunction-attribute"></a>SqlFunction 属性  
 **SqlFunction**特性指示应将方法注册为一个函数，并设置相应的函数属性。  
  
 有关详细信息，请参阅 [SqlFunctionAttribute](/dotnet/api/microsoft.sqlserver.server.sqlfunctionattribute)。  
  
## <a name="the-sqlfacet-attribute"></a>SqlFacet 特性  
 **SqlFacet**属性用于返回有关 (UDT) 表达式的用户定义类型的返回类型的信息。  
  
 有关详细信息，请参阅 [SqlFacetAttribute](/dotnet/api/microsoft.sqlserver.server.sqlfacetattribute)。  
  
## <a name="the-sqlprocedure-attribute"></a>SqlProcedure 属性  
 **SqlProcedure**特性指示应将方法注册为存储过程。 此属性仅由 Visual Studio 用于将指定的方法自动注册为存储过程；[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不使用此属性。  
  
 有关详细信息，请参阅 [SqlProcedureAttribute](/dotnet/api/microsoft.sqlserver.server.sqlprocedureattribute)。  
  
## <a name="the-sqltrigger-attribute"></a>SqlTrigger 特性  
 **SqlTrigger**特性指示应将方法注册为触发器。  
  
 有关详细信息，请参阅 [SqlTriggerContext](/dotnet/api/microsoft.sqlserver.server.sqltriggercontext) 和 [SqlTriggerAttribute](/dotnet/api/microsoft.sqlserver.server.sqltriggerattribute)。  
  
## <a name="the-sqluserdefinedtypeattribute"></a>SqlUserDefinedTypeAttribute  
 可将 SqlUserDefinedTypeAttribute 应用于程序集中的类定义。 此属性会使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 创建绑定到具有此自定义属性的类定义的用户定义类型。  
  
 有关详细信息，请参阅 [SqlUserDefinedTypeAttribute](/dotnet/api/microsoft.sqlserver.server.sqluserdefinedtypeattribute)。  
  
## <a name="the-sqlmethod-attribute"></a>SqlMethod 属性  
 **SqlMethod**特性用于指示 UDT 的方法或属性的确定性和数据访问属性。  
  
 有关详细信息，请参阅 [SqlMethodAttribute](/dotnet/api/microsoft.sqlserver.server.sqlmethodattribute)。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 用户定义聚合](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [CLR 用户定义函数](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [CLR 用户定义类型](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [CLR 存储过程](/dotnet/framework/data/adonet/sql/clr-stored-procedures)   
 [CLR 触发器](/dotnet/framework/data/adonet/sql/clr-triggers)  
  
