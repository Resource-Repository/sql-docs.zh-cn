---
description: SET DATEFORMAT (Transact-SQL)
title: SET DATEFORMAT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATEFORMAT
- SET DATEFORMAT
- SET_DATEFORMAT_TSQL
- DATEFORMAT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], formats
- dates [SQL Server], ordering date parts
- SET DATEFORMAT option [SQL Server]
- DATEFORMAT option [SQL Server]
- date and time [SQL Server], SET DATEFORMAT
- options [SQL Server], date
- date and time [SQL Server], DATEFORMAT
- dateparts [SQL Server], dateformat
ms.assetid: da217878-7ec4-477e-aa13-604073c948f8
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d04845384da2c609cb473de149d4702d48fe012c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465838"
---
# <a name="set-dateformat-transact-sql"></a>SET DATEFORMAT (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  设置用于解释日期字符串的月、日和年日期部分的顺序。 这些字符串属于类型“date”、“smalldatetime”、“datetime”、“datetime2”或“datetimeoffset”。  
  
 有关所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 日期和时间数据类型及函数的概述，请参阅[日期和时间数据类型及函数 (Transact-SQL)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```syntaxsql
SET DATEFORMAT { format | @format_var }   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>参数
 *format* |  **@** _format_var_  
 日期部分的顺序。 有效参数为 **mdy**、**dmy**、**ymd**、**ydm**、**myd** 和 **dym**。 可以是 Unicode，也可以是转换为 Unicode 的双字节字符集 (DBCS)。 美国英语默认值为 **mdy**。 有关所有支持语言的默认 DATEFORMAT，请参阅 [sp_helplanguage (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)。  
  
## <a name="remarks"></a>注解  
 “date”、“datetime2”和“datetimeoffset”数据类型不支持 DATEFORMAT“ydm”。  
  
 DATEFORMAT 设置可能会对日期数据类型的字符串进行不同的解释，具体取决于字符串格式。 例如，“datetime”和“smalldatetime”的解释可能与“date”、“datetime2”或“datetimeoffset”不一致。 在字符串转换为数据库的日期值时，DATEFORMAT 会影响字符串的解释。 它不会影响日期数据类型值的显示，也不会影响数据库中的存储格式。  
  
 某些字符串格式（例如 ISO 8601）的解释与 DATEFORMAT 设置无关。  
  
 SET DATEFORMAT 的设置是在执行或运行时设置，而不是在分析时设置。  
  
 SET DATEFORMAT 将覆盖 [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) 的隐式日期格式设置。  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 下例使用不同的日期字符串作为具有相同 `DATEFORMAT` 设置的会话中的输入。  
  
```sql
-- Set date format to day/month/year.  
SET DATEFORMAT dmy;  
GO  
DECLARE @datevar DATETIME2 = '31/12/2008 09:01:01.1234567';  
SELECT @datevar;  
GO  
-- Result: 2008-12-31 09:01:01.123  
SET DATEFORMAT dmy;  
GO  
DECLARE @datevar DATETIME2 = '12/31/2008 09:01:01.1234567';  
SELECT @datevar;  
GO  
-- Result: Msg 241: Conversion failed when converting date and/or time -- from character string.  
  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)  

