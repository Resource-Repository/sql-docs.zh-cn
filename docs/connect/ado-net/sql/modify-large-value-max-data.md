---
title: 修改 ADO.NET 中的大值（最大值）数据
description: 说明如何使用大值数据类型。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 8aca5f00-d80e-4320-81b3-016d0466f7ee
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: f55cb14a95844558e4a759a4acce71509d62d4ba
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725618"
---
# <a name="modifying-large-value-max-data-in-adonet"></a>修改 ADO.NET 中的大值（最大值）数据

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

大型对象 (LOB) 数据类型是指那些超过 8 KB 最大行大小的数据类型。 SQL Server 为 `max`、`varchar` 和 `nvarchar` 数据类型引入了 `varbinary` 说明符，以允许存储最长可达 2^32 个字节的值。 表列和 Transact-SQL 变量可以指定 `varchar(max)`、`nvarchar(max)` 或 `varbinary(max)` 数据类型。 在 .NET 中，可通过 `max` 获取 `DataReader` 数据类型，并将其指定为输入和输出参数值而不必进行任何特殊处理。 对于大型 `varchar` 数据类型，可以增量地检索和更新数据。  
  
`max` 数据类型可用于进行比较（作为 Transact-SQL 变量）和串联。 它们还可以用于 SELECT 语句的 DISTINCT、ORDER BY、GROUP BY 子句，以及聚合、连接和子查询。

有关大值数据类型的详细信息，请参阅 SQL Server 联机丛书中的[使用大值数据类型](/previous-versions/sql/sql-server-2008/ms178158(v=sql.100))。
  
## <a name="large-value-type-restrictions"></a>大值类型限制  
以下限制适用于对于较小数据类型不存在的 `max` 数据类型：  
  
- `sql_variant` 不能包含大型 `varchar` 数据类型。  
  
- 不能将大型 `varchar` 列指定为索引中的键列。 允许在非聚集索引的包含列中使用它们。  
  
- 大型 `varchar` 列不能用作分区键列。  
  
## <a name="working-with-large-value-types-in-transact-sql"></a>在 Transact-SQL 中使用大值类型  
Transact-SQL `OPENROWSET` 函数是连接和访问远程数据的一次性方法。 可在查询的 FROM 子句中像引用表名那样引用 `OPENROWSET`。 它也可作为 INSERT、UPDATE 或 DELETE 语句的目标表进行引用。  
  
`OPENROWSET` 函数包含 `BULK` 行集提供程序，它允许你直接从文件读取数据而不必将数据加载到目标表。 这样你可以在简单的 INSERT SELECT 语句中使用 `OPENROWSET`。  
  
`OPENROWSET BULK` 选项参数可以有效地控制在何处开始和结束读取数据、如何处理错误以及如何解释数据。 例如，可以指定以类型为 `varbinary`、`varchar` 或 `nvarchar` 的单行单列行集的形式读取数据文件。 有关完整的语法和选项，请参阅 SQL Server 联机丛书。  
  
以下示例向 AdventureWorks 示例数据库的 ProductPhoto 表中插入照片。 在使用 `BULK OPENROWSET` 提供程序时，即使不将值插入每个列中，也必须提供列的命名列表。 在此示例中，主键定义为标识列，可以从列列表中省略。 请注意，还必须在 `OPENROWSET` 语句的末尾提供相关名称，在本例中为 ThumbnailPhoto。 这与将文件加载到 `ProductPhoto` 表中的列相关联。  
  
```sql
INSERT Production.ProductPhoto (  
    ThumbnailPhoto,   
    ThumbnailPhotoFilePath,   
    LargePhoto,   
    LargePhotoFilePath)  
SELECT ThumbnailPhoto.*, null, null, N'tricycle_pink.gif'  
FROM OPENROWSET   
    (BULK 'c:\images\tricycle.jpg', SINGLE_BLOB) ThumbnailPhoto  
```  
  
## <a name="updating-data-using-update-write"></a>使用 UPDATE .WRITE 更新数据  
Transact-SQL UPDATE 语句具有新的 WRITE 语法，用于修改 `varchar(max)`、`nvarchar(max)` 或 `varbinary(max)` 列的内容。 这允许你对数据进行部分更新。 UPDATE .WRITE 语法在此以缩写形式显示：  
  
UPDATE  
  
{ *\<object>* }  
  
SET  
  
{ *column_name* = { .WRITE ( *expression* , @Offset , @Length ) }  
  
WRITE 方法指定将修改 column_name 值的某个部分  。 表达式是将复制到 column_name 的值， *是将写入表达式的开始点，* 自变量是列中该部分的长度`@Offset``@Length`。  
  
|如果|则|  
|--------|----------|  
|表达式设置为 NULL|忽略 `@Length`，并在指定的  *处截断 column_name 中的值*`@Offset`。|  
|`@Offset` 为 NULL|更新操作将表达式追加到现有 column_name 值的末尾并忽略  `@Length`。|  
|`@Offset` 大于 column_name 值的长度|SQL Server 将返回错误。|  
|`@Length` 为 NULL|更新操作将删除从 `@Offset` 到 `column_name` 值的结尾的所有数据。|  
  
> [!NOTE]
>  `@Offset` 和 `@Length` 都不能为负数。  
  
## <a name="example"></a>示例  
此 Transact-SQL 示例更新 DocumentSummary 中的一个部分值，这是 AdventureWorks 数据库中 Document 表的 `nvarchar(max)` 列。 通过指定替换单词、现有数据中要替换的单词的开始位置（偏移量）以及要替换的字符数（长度），将单词“components”替换为单词“features”。 该示例在 UPDATE 语句之前和之后都包含 SELECT 语句来比较结果。  
  
```sql
USE AdventureWorks;  
GO  
--View the existing value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety components of your bicycle.  
  
--Modify a single word in the DocumentSummary column  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N'features',28,10)  
WHERE DocumentID = 3 ;  
GO   
--View the modified value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety features of your bicycle.  
```  
  
## <a name="working-with-large-value-types-in-adonet"></a>在 ADO.NET 中使用大值类型  
通过将大值类型指定为 <xref:Microsoft.Data.SqlClient.SqlParameter> 中的 <xref:Microsoft.Data.SqlClient.SqlDataReader> 对象以返回结果集，或者通过 <xref:Microsoft.Data.SqlClient.SqlDataAdapter> 来填充 `DataSet`/`DataTable`，即可在 ADO.NET 中使用大值类型。 处理大值类型与其相关的较小值数据类型的方式没有区别。  
  
### <a name="using-getsqlbytes-to-retrieve-data"></a>使用 GetSqlBytes 检索数据  
`GetSqlBytes` 的 <xref:Microsoft.Data.SqlClient.SqlDataReader> 方法可用于检索 `varbinary(max)` 列的内容。 下面的代码段假定一个名为 <xref:Microsoft.Data.SqlClient.SqlCommand> 的 `cmd` 对象，该对象从表中选择 `varbinary(max)` 数据，并假定一个名为 <xref:Microsoft.Data.SqlClient.SqlDataReader> 的 `reader` 对象以 <xref:System.Data.SqlTypes.SqlBytes> 的形式检索数据。  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBytes bytes = reader.GetSqlBytes(0);  
    }  
```  
  
### <a name="using-getsqlchars-to-retrieve-data"></a>使用 GetSqlChars 检索数据  
`GetSqlChars` 的 <xref:Microsoft.Data.SqlClient.SqlDataReader> 方法可用于检索 `varchar(max)` 或 `nvarchar(max)` 列的内容。 下面的代码段假定一个名为 <xref:Microsoft.Data.SqlClient.SqlCommand> 的 `cmd` 对象，该对象从表中选择 `nvarchar(max)` 数据，并假定一个名为 <xref:Microsoft.Data.SqlClient.SqlDataReader> 的 `reader` 对象来检索数据。   
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
{  
    SqlChars buffer = reader.GetSqlChars(0);  
}  
```  
  
### <a name="using-getsqlbinary-to-retrieve-data"></a>使用 GetSqlBinary 检索数据  
`GetSqlBinary` 的 <xref:Microsoft.Data.SqlClient.SqlDataReader> 方法可用于检索 `varbinary(max)` 列的内容。 下面的代码段假定一个名为 <xref:Microsoft.Data.SqlClient.SqlCommand> 的 `cmd` 对象，该对象从表中选择 `varbinary(max)` 数据，并假定一个名为 <xref:Microsoft.Data.SqlClient.SqlDataReader> 的 `reader` 对象以 <xref:System.Data.SqlTypes.SqlBinary> 流的形式检索数据。  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBinary binaryStream = reader.GetSqlBinary(0);  
    }  
```  
  
### <a name="using-getbytes-to-retrieve-data"></a>使用 GetBytes 检索数据  
`GetBytes` 的 <xref:Microsoft.Data.SqlClient.SqlDataReader> 方法从指定的列偏移量将字节流从指定数组偏移量开始读入字节数组。 下面的代码段假定一个名为 <xref:Microsoft.Data.SqlClient.SqlDataReader> 的 `reader` 对象，该对象将字节检索到字节数组中。 请注意，与 `GetSqlBytes` 不同，`GetBytes` 需要数组缓冲区的大小。  
  
```csharp  
while (reader.Read())  
{  
    byte[] buffer = new byte[4000];  
    long byteCount = reader.GetBytes(1, 0, buffer, 0, 4000);  
}  
```  
  
### <a name="using-getvalue-to-retrieve-data"></a>使用 GetValue 检索数据  
`GetValue` 的 <xref:Microsoft.Data.SqlClient.SqlDataReader> 方法将值从指定的列偏移量读入数组。 下面的代码段假定一个名为 <xref:Microsoft.Data.SqlClient.SqlDataReader> 的 `reader` 对象，该对象从第一个列偏移量检索二进制数据，然后从第二列偏移量检索字符串数据。  
  
```csharp  
while (reader.Read())  
{  
    // Read the data from varbinary(max) column  
    byte[] binaryData = (byte[])reader.GetValue(0);  
  
    // Read the data from varchar(max) or nvarchar(max) column  
    String stringData = (String)reader.GetValue(1);  
}  
```  
  
## <a name="converting-from-large-value-types-to-clr-types"></a>从大值类型转换为 CLR 类型  
可以使用任何字符串转换方法（如 `varchar(max)`）来转换 `nvarchar(max)` 或 `ToString` 列的内容。 下面的代码段假定一个名为 <xref:Microsoft.Data.SqlClient.SqlDataReader> 的 `reader` 对象，该对象检索数据。  
  
```csharp  
while (reader.Read())  
{  
     string str = reader[0].ToString();  
     Console.WriteLine(str);  
}  
```  
  
### <a name="example"></a>示例  
下面的代码从 `LargePhoto` 数据库的 `ProductPhoto` 表中检索名称和 `AdventureWorks` 对象，并将其保存到文件中。 需要使用对 <xref:System.Drawing> 命名空间的引用来编译该程序集。  <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlBytes%2A> 的 <xref:Microsoft.Data.SqlClient.SqlDataReader> 方法返回公开 <xref:System.Data.SqlTypes.SqlBytes> 属性的 `Stream` 对象。 代码使用此对象创建新的 `Bitmap` 对象，然后以 Gif `ImageFormat` 格式保存该对象。  
  
[!code-csharp[DataWorks SqlBytes_Stream#1](~/../sqlclient/doc/samples/SqlBytes_Stream.cs#1)]
  
## <a name="using-large-value-type-parameters"></a>使用大值类型参数  
在 <xref:Microsoft.Data.SqlClient.SqlParameter> 对象中使用的大值类型的方式与在 <xref:Microsoft.Data.SqlClient.SqlParameter> 对象中使用较小值类型的方式相同。 可以将大值类型作为 <xref:Microsoft.Data.SqlClient.SqlParameter> 值进行检索，如下面的示例所示。 此代码假定 AdventureWorks 示例数据库中存在以下 GetDocumentSummary 存储过程。 该存储过程采用名为 @DocumentID 的输入参数，并在 @DocumentSummary 输出参数中返回 DocumentSummary 列的内容。  
  
```sql
CREATE PROCEDURE GetDocumentSummary   
(  
    @DocumentID int,  
    @DocumentSummary nvarchar(MAX) OUTPUT  
)  
AS  
SET NOCOUNT ON  
SELECT  @DocumentSummary=Convert(nvarchar(MAX), DocumentSummary)  
FROM    Production.Document  
WHERE   DocumentID=@DocumentID  
```  
  
### <a name="example"></a>示例  
ADO.NET 代码将创建 <xref:Microsoft.Data.SqlClient.SqlConnection> 和 <xref:Microsoft.Data.SqlClient.SqlCommand> 对象以执行 GetDocumentSummary 存储过程，并检索文档摘要，该摘要存储为大值类型。 代码为 @DocumentID 输入参数传递一个值，并在控制台窗口显示 @DocumentSummary 输出参数中传回的结果。  
  
[!code-csharp[DataWorks SqlParameter_Value#1](~/../sqlclient/doc/samples/SqlParameter_Value.cs#1)]
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 二进制和大值数据](sql-server-binary-large-value-data.md)
- [ADO.NET 中的 SQL Server 数据操作](sql-server-data-operations.md)