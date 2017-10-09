
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a>C# 程式範例

hello 本文的下一個小節提供使用 ADO.NET toosend TRANSACT-SQL 陳述式 toohello SQL database 的 C# 程式。 hello C# 程式會執行下列動作的 hello:

1. [連接 tooour 使用 ADO.NET 的 SQL database](#cs_1_connect)。
2. [建立資料表](#cs_2_createtables)。
3. [填入 hello 資料表與資料，藉由發出 T-SQL INSERT 陳述式](#cs_3_insert)。
4. [使用聯結更新資料](#cs_4_updatejoin)。
5. [使用聯結刪除資料](#cs_5_deletejoin)。
6. [使用聯結選取資料列](#cs_6_selectrows)。
7. 關閉 hello 連接 （可從 tempdb 中卸除任何暫存資料表）。

hello C# 程式包含：

- C# 程式碼 tooconnect toohello 資料庫。
- 傳回 hello T-SQL 原始程式碼的方法。
- 送出 hello T-SQL toohello 資料庫的兩種方法。

#### <a name="toocompile-and-run"></a>toocompile 和 執行

這個 C# 程式邏輯上是一個 .cs 檔案。 但是這裡 hello 程式實際分成數個程式碼區塊，每個區塊更容易 toosee toomake，並了解。 toocompile 並執行此程式，請勿遵循 hello:

1. 在 Visual Studio 中建立 C# 專案。
    - hello 專案類型應該是*主控台*應用程式，從結果類似下列階層中的 hello:**範本** > **Visual C#** >**的傳統 Windows 桌面** > **主控台應用程式 (.NET Framework)**。
3. 在 hello 檔案**Program.cs**，清除 hello 小型的起始行程式碼。
3. 加入 Program.cs，複製和貼上每個區塊，下列中的 hello 的 hello 這裡顯示的相同順序。
4. 在 Program.cs 中，編輯 hello 下列值的 hello **Main**方法：

   - **cb.DataSource**
   - **cd.UserID**
   - **cb.Password**
   - **InitialCatalog**

5. 確認該組 hello **System.Data.dll**參考。 tooverify，依序展開 [hello**參考**節點 hello**方案總管] 中**窗格。
6. toobuild hello 程式，在 Visual Studio 中，按一下 hello**建置**功能表。
7. toorun hello 程式，從 Visual Studio 中，按一下 [hello**啟動**] 按鈕。 hello 報表輸出會顯示在 cmd.exe 視窗中。

> [!NOTE]
> 您可以編輯 hello T-SQL tooadd 前置 hello 選擇 **#**  toohello 資料表名稱，會為暫存資料表中的建立這些**tempdb**。 沒有測試資料庫可供使用時，這很適合用於示範。 Hello 連接關閉時，會自動刪除暫存資料表。 不會對暫存資料表強制執行外部索引鍵的任何 REFERENCES。
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a>C# 區塊 1：使用 ADO.NET 連線

- [下一頁](#cs_2_createtables)


```csharp
using System;
using System.Data.SqlClient;   // System.Data.dll 
//using System.Data;           // For:  SqlDbType , ParameterDirection

namespace csharp_db_test
{
   class Program
   {
      static void Main(string[] args)
      {
         try
         {
            var cb = new SqlConnectionStringBuilder();
            cb.DataSource = "your_server.database.windows.net";
            cb.UserID = "your_user";
            cb.Password = "your_password";
            cb.InitialCatalog = "your_database";

            using (var connection = new SqlConnection(cb.ConnectionString))
            {
               connection.Open();

               Submit_Tsql_NonQuery(connection, "2 - Create-Tables",
                  Build_2_Tsql_CreateTables());

               Submit_Tsql_NonQuery(connection, "3 - Inserts",
                  Build_3_Tsql_Inserts());

               Submit_Tsql_NonQuery(connection, "4 - Update-Join",
                  Build_4_Tsql_UpdateJoin(),
                  "@csharpParmDepartmentName", "Accounting");

               Submit_Tsql_NonQuery(connection, "5 - Delete-Join",
                  Build_5_Tsql_DeleteJoin(),
                  "@csharpParmDepartmentName", "Legal");

               Submit_6_Tsql_SelectEmployees(connection);
            }
         }
         catch (SqlException e)
         {
            Console.WriteLine(e.ToString());
         }
         Console.WriteLine("View hello report output here, then press any key tooend hello program...");
         Console.ReadKey();
      }
```


<a name="cs_2_createtables"/>
### <a name="c-block-2-t-sql-toocreate-tables"></a>C# 區塊 2: T-SQL toocreate 資料表

- [上一個](#cs_1_connect) &nbsp; / &nbsp; [下一個](#cs_3_insert)

```csharp
      static string Build_2_Tsql_CreateTables()
      {
         return @"
DROP TABLE IF EXISTS tabEmployee;
DROP TABLE IF EXISTS tabDepartment;  -- Drop parent table last.


CREATE TABLE tabDepartment
(
   DepartmentCode  nchar(4)          not null
      PRIMARY KEY,
   DepartmentName  nvarchar(128)     not null
);

CREATE TABLE tabEmployee
(
   EmployeeGuid    uniqueIdentifier  not null  default NewId()
      PRIMARY KEY,
   EmployeeName    nvarchar(128)     not null,
   EmployeeLevel   int               not null,
   DepartmentCode  nchar(4)              null
      REFERENCES tabDepartment (DepartmentCode)  -- (REFERENCES would be disallowed on temporary tables.)
);
";
      }
```

#### <a name="entity-relationship-diagram-erd"></a>實體關聯圖 (ERD)

hello 上述 CREATE TABLE 陳述式包含 hello**參考**關鍵字 toocreate*外部索引鍵*(FK) 兩個資料表之間的關聯性。  如果您使用 tempdb，標記為註解 hello`--REFERENCES`關鍵字使用的前置連字號組。

接下來是 ERD 顯示 hello hello 兩個資料表之間的關聯性。 hello 中 hello #tabEmployee.DepartmentCode 值*子*資料行是有限的 toohello 值出現在 hello #tabDepartment.Department*父*資料行。

![顯示外部索引鍵的 ERD](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-tooinsert-data"></a>C# 的區塊 3: T-SQL tooinsert 資料

- [上一個](#cs_2_createtables) &nbsp; / &nbsp; [下一個](#cs_4_updatejoin)


```csharp
      static string Build_3_Tsql_Inserts()
      {
         return @"
-- hello company has these departments.
INSERT INTO tabDepartment
   (DepartmentCode, DepartmentName)
      VALUES
   ('acct', 'Accounting'),
   ('hres', 'Human Resources'),
   ('legl', 'Legal');

-- hello company has these employees, each in one department.
INSERT INTO tabEmployee
   (EmployeeName, EmployeeLevel, DepartmentCode)
      VALUES
   ('Alison'  , 19, 'acct'),
   ('Barbara' , 17, 'hres'),
   ('Carol'   , 21, 'acct'),
   ('Deborah' , 24, 'legl'),
   ('Elle'    , 15, null);
";
      }
```


<a name="cs_4_updatejoin"/>
### <a name="c-block-4-t-sql-tooupdate-join"></a>C# 區塊 4: T-SQL tooupdate 聯結

- [上一個](#cs_3_insert) &nbsp; / &nbsp; [下一個](#cs_5_deletejoin)


```csharp
      static string Build_4_Tsql_UpdateJoin()
      {
         return @"
DECLARE @DName1  nvarchar(128) = @csharpParmDepartmentName;  --'Accounting';


-- Promote everyone in one department (see @parm...).
UPDATE empl
   SET
      empl.EmployeeLevel += 1
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName1;
";
      }
```


<a name="cs_5_deletejoin"/>
### <a name="c-block-5-t-sql-toodelete-join"></a>C# 區塊 5: T-SQL toodelete 聯結

- [上一個](#cs_4_updatejoin) &nbsp; / &nbsp; [下一個](#cs_6_selectrows)


```csharp
      static string Build_5_Tsql_DeleteJoin()
      {
         return @"
DECLARE @DName2  nvarchar(128);
SET @DName2 = @csharpParmDepartmentName;  --'Legal';


-- Right size hello Legal department.
DELETE empl
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName2

-- Disband hello Legal department.
DELETE tabDepartment
   WHERE DepartmentName = @DName2;
";
      }
```



<a name="cs_6_selectrows"/>
### <a name="c-block-6-t-sql-tooselect-rows"></a>C# 區塊 6: T-SQL tooselect 資料列

- [上一個](#cs_5_deletejoin) &nbsp; / &nbsp; [下一個](#cs_6b_datareader)


```csharp
      static string Build_6_Tsql_SelectEmployees()
      {
         return @"
-- Look at all hello final Employees.
SELECT
      empl.EmployeeGuid,
      empl.EmployeeName,
      empl.EmployeeLevel,
      empl.DepartmentCode,
      dept.DepartmentName
   FROM
      tabEmployee   as empl
      LEFT OUTER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   ORDER BY
      EmployeeName;
";
      }
```


<a name="cs_6b_datareader"/>
### <a name="c-block-6b-executereader"></a>C# 區塊 6b：ExecuteReader

- [上一個](#cs_6_selectrows) &nbsp; / &nbsp; [下一個](#cs_7_executenonquery)

這個方法是設計的 toorun hello T-SQL SELECT 陳述式建立的 hello **Build_6_Tsql_SelectEmployees**方法。


```csharp
      static void Submit_6_Tsql_SelectEmployees(SqlConnection connection)
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("Now, SelectEmployees (6)...");

         string tsql = Build_6_Tsql_SelectEmployees();

         using (var command = new SqlCommand(tsql, connection))
         {
            using (SqlDataReader reader = command.ExecuteReader())
            {
               while (reader.Read())
               {
                  Console.WriteLine("{0} , {1} , {2} , {3} , {4}",
                     reader.GetGuid(0),
                     reader.GetString(1),
                     reader.GetInt32(2),
                     (reader.IsDBNull(3)) ? "NULL" : reader.GetString(3),
                     (reader.IsDBNull(4)) ? "NULL" : reader.GetString(4));
               }
            }
         }
      }
```


<a name="cs_7_executenonquery"/>
### <a name="c-block-7-executenonquery"></a>C# 區塊 7：ExecuteNonQuery

- [上一個](#cs_6b_datareader) &nbsp; / &nbsp; [下一個](#cs_8_output)

呼叫這個方法是修改 hello 資料表的資料內容，而不需傳回任何資料列的作業。


```csharp
      static void Submit_Tsql_NonQuery(
         SqlConnection connection,
         string tsqlPurpose,
         string tsqlSourceCode,
         string parameterName = null,
         string parameterValue = null
         )
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("T-SQL too{0}...", tsqlPurpose);

         using (var command = new SqlCommand(tsqlSourceCode, connection))
         {
            if (parameterName != null)
            {
               command.Parameters.AddWithValue(  // Or, use SqlParameter class.
                  parameterName,
                  parameterValue);
            }
            int rowsAffected = command.ExecuteNonQuery();
            Console.WriteLine(rowsAffected + " = rows affected.");
         }
      }
   } // EndOfClass
}
```


<a name="cs_8_output"/>
### <a name="c-block-8-actual-test-output-toohello-console"></a>C# 區塊 8： 實際的測試輸出 toohello 主控台

- [上一個](#cs_7_executenonquery)

本節會擷取 hello hello 程式傳送 toohello 主控台的輸出。 測試回合之間的不只有 hello guid 值。


```text
[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>> csharp_db_test.exe

=================================
Now, CreateTables (10)...

=================================
Now, Inserts (20)...

=================================
Now, UpdateJoin (30)...
2 rows affected, by UpdateJoin.

=================================
Now, DeleteJoin (40)...

=================================
Now, SelectEmployees (50)...
0199be49-a2ed-4e35-94b7-e936acf1cd75 , Alison , 20 , acct , Accounting
f0d3d147-64cf-4420-b9f9-76e6e0a32567 , Barbara , 17 , hres , Human Resources
cf4caede-e237-42d2-b61d-72114c7e3afa , Carol , 22 , acct , Accounting
cdde7727-bcfd-4f72-a665-87199c415f8b , Elle , 15 , NULL , NULL

[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>>
```
