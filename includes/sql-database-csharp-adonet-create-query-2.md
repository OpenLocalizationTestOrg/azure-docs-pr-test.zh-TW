
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a><span data-ttu-id="f7d87-101">C# 程式範例</span><span class="sxs-lookup"><span data-stu-id="f7d87-101">C# program example</span></span>

<span data-ttu-id="f7d87-102">hello 本文的下一個小節提供使用 ADO.NET toosend TRANSACT-SQL 陳述式 toohello SQL database 的 C# 程式。</span><span class="sxs-lookup"><span data-stu-id="f7d87-102">hello next sections of this article present a C# program that uses ADO.NET toosend Transact-SQL statements toohello SQL database.</span></span> <span data-ttu-id="f7d87-103">hello C# 程式會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="f7d87-103">hello C# program performs hello following actions:</span></span>

1. <span data-ttu-id="f7d87-104">[連接 tooour 使用 ADO.NET 的 SQL database](#cs_1_connect)。</span><span class="sxs-lookup"><span data-stu-id="f7d87-104">[Connects tooour SQL database using ADO.NET](#cs_1_connect).</span></span>
2. <span data-ttu-id="f7d87-105">[建立資料表](#cs_2_createtables)。</span><span class="sxs-lookup"><span data-stu-id="f7d87-105">[Creates tables](#cs_2_createtables).</span></span>
3. <span data-ttu-id="f7d87-106">[填入 hello 資料表與資料，藉由發出 T-SQL INSERT 陳述式](#cs_3_insert)。</span><span class="sxs-lookup"><span data-stu-id="f7d87-106">[Populates hello tables with data, by issuing T-SQL INSERT statements](#cs_3_insert).</span></span>
4. <span data-ttu-id="f7d87-107">[使用聯結更新資料](#cs_4_updatejoin)。</span><span class="sxs-lookup"><span data-stu-id="f7d87-107">[Updates data by use of a join](#cs_4_updatejoin).</span></span>
5. <span data-ttu-id="f7d87-108">[使用聯結刪除資料](#cs_5_deletejoin)。</span><span class="sxs-lookup"><span data-stu-id="f7d87-108">[Deletes data by use of a join](#cs_5_deletejoin).</span></span>
6. <span data-ttu-id="f7d87-109">[使用聯結選取資料列](#cs_6_selectrows)。</span><span class="sxs-lookup"><span data-stu-id="f7d87-109">[Selects data rows by use of a join](#cs_6_selectrows).</span></span>
7. <span data-ttu-id="f7d87-110">關閉 hello 連接 （可從 tempdb 中卸除任何暫存資料表）。</span><span class="sxs-lookup"><span data-stu-id="f7d87-110">Closes hello connection (which drops any temporary tables from tempdb).</span></span>

<span data-ttu-id="f7d87-111">hello C# 程式包含：</span><span class="sxs-lookup"><span data-stu-id="f7d87-111">hello C# program contains:</span></span>

- <span data-ttu-id="f7d87-112">C# 程式碼 tooconnect toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="f7d87-112">C# code tooconnect toohello database.</span></span>
- <span data-ttu-id="f7d87-113">傳回 hello T-SQL 原始程式碼的方法。</span><span class="sxs-lookup"><span data-stu-id="f7d87-113">Methods that return hello T-SQL source code.</span></span>
- <span data-ttu-id="f7d87-114">送出 hello T-SQL toohello 資料庫的兩種方法。</span><span class="sxs-lookup"><span data-stu-id="f7d87-114">Two methods that submit hello T-SQL toohello database.</span></span>

#### <a name="toocompile-and-run"></a><span data-ttu-id="f7d87-115">toocompile 和 執行</span><span class="sxs-lookup"><span data-stu-id="f7d87-115">toocompile and run</span></span>

<span data-ttu-id="f7d87-116">這個 C# 程式邏輯上是一個 .cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="f7d87-116">This C# program is logically one .cs file.</span></span> <span data-ttu-id="f7d87-117">但是這裡 hello 程式實際分成數個程式碼區塊，每個區塊更容易 toosee toomake，並了解。</span><span class="sxs-lookup"><span data-stu-id="f7d87-117">But here hello program is physically divided into several code blocks, toomake each block easier toosee and understand.</span></span> <span data-ttu-id="f7d87-118">toocompile 並執行此程式，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="f7d87-118">toocompile and run this program, do hello following:</span></span>

1. <span data-ttu-id="f7d87-119">在 Visual Studio 中建立 C# 專案。</span><span class="sxs-lookup"><span data-stu-id="f7d87-119">Create a C# project in Visual Studio.</span></span>
    - <span data-ttu-id="f7d87-120">hello 專案類型應該是*主控台*應用程式，從結果類似下列階層中的 hello:**範本** > **Visual C#** >**的傳統 Windows 桌面** > **主控台應用程式 (.NET Framework)**。</span><span class="sxs-lookup"><span data-stu-id="f7d87-120">hello project type should be a *console* application, from something like hello following hierarchy: **Templates** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
3. <span data-ttu-id="f7d87-121">在 hello 檔案**Program.cs**，清除 hello 小型的起始行程式碼。</span><span class="sxs-lookup"><span data-stu-id="f7d87-121">In hello file **Program.cs**, erase hello small starter lines of code.</span></span>
3. <span data-ttu-id="f7d87-122">加入 Program.cs，複製和貼上每個區塊，下列中的 hello 的 hello 這裡顯示的相同順序。</span><span class="sxs-lookup"><span data-stu-id="f7d87-122">Into Program.cs, copy and paste each of hello following blocks, in hello same sequence they are presented here.</span></span>
4. <span data-ttu-id="f7d87-123">在 Program.cs 中，編輯 hello 下列值的 hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="f7d87-123">In Program.cs, edit hello following values in hello **Main** method:</span></span>

   - <span data-ttu-id="f7d87-124">**cb.DataSource**</span><span class="sxs-lookup"><span data-stu-id="f7d87-124">**cb.DataSource**</span></span>
   - <span data-ttu-id="f7d87-125">**cd.UserID**</span><span class="sxs-lookup"><span data-stu-id="f7d87-125">**cd.UserID**</span></span>
   - <span data-ttu-id="f7d87-126">**cb.Password**</span><span class="sxs-lookup"><span data-stu-id="f7d87-126">**cb.Password**</span></span>
   - <span data-ttu-id="f7d87-127">**InitialCatalog**</span><span class="sxs-lookup"><span data-stu-id="f7d87-127">**InitialCatalog**</span></span>

5. <span data-ttu-id="f7d87-128">確認該組 hello **System.Data.dll**參考。</span><span class="sxs-lookup"><span data-stu-id="f7d87-128">Verify that hello assembly **System.Data.dll** is referenced.</span></span> <span data-ttu-id="f7d87-129">tooverify，依序展開 [hello**參考**節點 hello**方案總管] 中**窗格。</span><span class="sxs-lookup"><span data-stu-id="f7d87-129">tooverify, expand hello **References** node in hello **Solution Explorer** pane.</span></span>
6. <span data-ttu-id="f7d87-130">toobuild hello 程式，在 Visual Studio 中，按一下 hello**建置**功能表。</span><span class="sxs-lookup"><span data-stu-id="f7d87-130">toobuild hello program in Visual Studio, click hello **Build** menu.</span></span>
7. <span data-ttu-id="f7d87-131">toorun hello 程式，從 Visual Studio 中，按一下 [hello**啟動**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f7d87-131">toorun hello program from Visual Studio, click hello **Start** button.</span></span> <span data-ttu-id="f7d87-132">hello 報表輸出會顯示在 cmd.exe 視窗中。</span><span class="sxs-lookup"><span data-stu-id="f7d87-132">hello report output is displayed in a cmd.exe window.</span></span>

> [!NOTE]
> <span data-ttu-id="f7d87-133">您可以編輯 hello T-SQL tooadd 前置 hello 選擇 **#**  toohello 資料表名稱，會為暫存資料表中的建立這些**tempdb**。</span><span class="sxs-lookup"><span data-stu-id="f7d87-133">You have hello option of editing hello T-SQL tooadd a leading **#** toohello table names, which creates them as temporary tables in **tempdb**.</span></span> <span data-ttu-id="f7d87-134">沒有測試資料庫可供使用時，這很適合用於示範。</span><span class="sxs-lookup"><span data-stu-id="f7d87-134">This can be useful for demonstration purposes, when no test database is available.</span></span> <span data-ttu-id="f7d87-135">Hello 連接關閉時，會自動刪除暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="f7d87-135">Temporary tables are deleted automatically when hello connection closes.</span></span> <span data-ttu-id="f7d87-136">不會對暫存資料表強制執行外部索引鍵的任何 REFERENCES。</span><span class="sxs-lookup"><span data-stu-id="f7d87-136">Any REFERENCES for foreign keys are not enforced for temporary tables.</span></span>
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a><span data-ttu-id="f7d87-137">C# 區塊 1：使用 ADO.NET 連線</span><span class="sxs-lookup"><span data-stu-id="f7d87-137">C# block 1: Connect by using ADO.NET</span></span>

- [<span data-ttu-id="f7d87-138">下一頁</span><span class="sxs-lookup"><span data-stu-id="f7d87-138">Next</span></span>](#cs_2_createtables)


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
### <a name="c-block-2-t-sql-toocreate-tables"></a><span data-ttu-id="f7d87-139">C# 區塊 2: T-SQL toocreate 資料表</span><span class="sxs-lookup"><span data-stu-id="f7d87-139">C# block 2: T-SQL toocreate tables</span></span>

- <span data-ttu-id="f7d87-140">[上一個](#cs_1_connect) &nbsp; / &nbsp; [下一個](#cs_3_insert)</span><span class="sxs-lookup"><span data-stu-id="f7d87-140">[Previous](#cs_1_connect) &nbsp; / &nbsp; [Next](#cs_3_insert)</span></span>

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

#### <a name="entity-relationship-diagram-erd"></a><span data-ttu-id="f7d87-141">實體關聯圖 (ERD)</span><span class="sxs-lookup"><span data-stu-id="f7d87-141">Entity Relationship Diagram (ERD)</span></span>

<span data-ttu-id="f7d87-142">hello 上述 CREATE TABLE 陳述式包含 hello**參考**關鍵字 toocreate*外部索引鍵*(FK) 兩個資料表之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="f7d87-142">hello preceding CREATE TABLE statements involve hello **REFERENCES** keyword toocreate a *foreign key* (FK) relationship between two tables.</span></span>  <span data-ttu-id="f7d87-143">如果您使用 tempdb，標記為註解 hello`--REFERENCES`關鍵字使用的前置連字號組。</span><span class="sxs-lookup"><span data-stu-id="f7d87-143">If you are using tempdb, comment out hello `--REFERENCES` keyword using a pair of leading dashes.</span></span>

<span data-ttu-id="f7d87-144">接下來是 ERD 顯示 hello hello 兩個資料表之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="f7d87-144">Next is an ERD that displays hello relationship between hello two tables.</span></span> <span data-ttu-id="f7d87-145">hello 中 hello #tabEmployee.DepartmentCode 值*子*資料行是有限的 toohello 值出現在 hello #tabDepartment.Department*父*資料行。</span><span class="sxs-lookup"><span data-stu-id="f7d87-145">hello values in hello #tabEmployee.DepartmentCode *child* column are limited toohello values present in hello #tabDepartment.Department *parent* column.</span></span>

![顯示外部索引鍵的 ERD](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-tooinsert-data"></a><span data-ttu-id="f7d87-147">C# 的區塊 3: T-SQL tooinsert 資料</span><span class="sxs-lookup"><span data-stu-id="f7d87-147">C# block 3: T-SQL tooinsert data</span></span>

- <span data-ttu-id="f7d87-148">[上一個](#cs_2_createtables) &nbsp; / &nbsp; [下一個](#cs_4_updatejoin)</span><span class="sxs-lookup"><span data-stu-id="f7d87-148">[Previous](#cs_2_createtables) &nbsp; / &nbsp; [Next](#cs_4_updatejoin)</span></span>


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
### <a name="c-block-4-t-sql-tooupdate-join"></a><span data-ttu-id="f7d87-149">C# 區塊 4: T-SQL tooupdate 聯結</span><span class="sxs-lookup"><span data-stu-id="f7d87-149">C# block 4: T-SQL tooupdate-join</span></span>

- <span data-ttu-id="f7d87-150">[上一個](#cs_3_insert) &nbsp; / &nbsp; [下一個](#cs_5_deletejoin)</span><span class="sxs-lookup"><span data-stu-id="f7d87-150">[Previous](#cs_3_insert) &nbsp; / &nbsp; [Next](#cs_5_deletejoin)</span></span>


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
### <a name="c-block-5-t-sql-toodelete-join"></a><span data-ttu-id="f7d87-151">C# 區塊 5: T-SQL toodelete 聯結</span><span class="sxs-lookup"><span data-stu-id="f7d87-151">C# block 5: T-SQL toodelete-join</span></span>

- <span data-ttu-id="f7d87-152">[上一個](#cs_4_updatejoin) &nbsp; / &nbsp; [下一個](#cs_6_selectrows)</span><span class="sxs-lookup"><span data-stu-id="f7d87-152">[Previous](#cs_4_updatejoin) &nbsp; / &nbsp; [Next](#cs_6_selectrows)</span></span>


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
### <a name="c-block-6-t-sql-tooselect-rows"></a><span data-ttu-id="f7d87-153">C# 區塊 6: T-SQL tooselect 資料列</span><span class="sxs-lookup"><span data-stu-id="f7d87-153">C# block 6: T-SQL tooselect rows</span></span>

- <span data-ttu-id="f7d87-154">[上一個](#cs_5_deletejoin) &nbsp; / &nbsp; [下一個](#cs_6b_datareader)</span><span class="sxs-lookup"><span data-stu-id="f7d87-154">[Previous](#cs_5_deletejoin) &nbsp; / &nbsp; [Next](#cs_6b_datareader)</span></span>


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
### <a name="c-block-6b-executereader"></a><span data-ttu-id="f7d87-155">C# 區塊 6b：ExecuteReader</span><span class="sxs-lookup"><span data-stu-id="f7d87-155">C# block 6b: ExecuteReader</span></span>

- <span data-ttu-id="f7d87-156">[上一個](#cs_6_selectrows) &nbsp; / &nbsp; [下一個](#cs_7_executenonquery)</span><span class="sxs-lookup"><span data-stu-id="f7d87-156">[Previous](#cs_6_selectrows) &nbsp; / &nbsp; [Next](#cs_7_executenonquery)</span></span>

<span data-ttu-id="f7d87-157">這個方法是設計的 toorun hello T-SQL SELECT 陳述式建立的 hello **Build_6_Tsql_SelectEmployees**方法。</span><span class="sxs-lookup"><span data-stu-id="f7d87-157">This method is designed toorun hello T-SQL SELECT statement that is built by hello **Build_6_Tsql_SelectEmployees** method.</span></span>


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
### <a name="c-block-7-executenonquery"></a><span data-ttu-id="f7d87-158">C# 區塊 7：ExecuteNonQuery</span><span class="sxs-lookup"><span data-stu-id="f7d87-158">C# block 7: ExecuteNonQuery</span></span>

- <span data-ttu-id="f7d87-159">[上一個](#cs_6b_datareader) &nbsp; / &nbsp; [下一個](#cs_8_output)</span><span class="sxs-lookup"><span data-stu-id="f7d87-159">[Previous](#cs_6b_datareader) &nbsp; / &nbsp; [Next](#cs_8_output)</span></span>

<span data-ttu-id="f7d87-160">呼叫這個方法是修改 hello 資料表的資料內容，而不需傳回任何資料列的作業。</span><span class="sxs-lookup"><span data-stu-id="f7d87-160">This method is called for operations that modify hello data content of tables without returning any data rows.</span></span>


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
### <a name="c-block-8-actual-test-output-toohello-console"></a><span data-ttu-id="f7d87-161">C# 區塊 8： 實際的測試輸出 toohello 主控台</span><span class="sxs-lookup"><span data-stu-id="f7d87-161">C# block 8: Actual test output toohello console</span></span>

- [<span data-ttu-id="f7d87-162">上一個</span><span class="sxs-lookup"><span data-stu-id="f7d87-162">Previous</span></span>](#cs_7_executenonquery)

<span data-ttu-id="f7d87-163">本節會擷取 hello hello 程式傳送 toohello 主控台的輸出。</span><span class="sxs-lookup"><span data-stu-id="f7d87-163">This section captures hello output that hello program sent toohello console.</span></span> <span data-ttu-id="f7d87-164">測試回合之間的不只有 hello guid 值。</span><span class="sxs-lookup"><span data-stu-id="f7d87-164">Only hello guid values vary between test runs.</span></span>


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
