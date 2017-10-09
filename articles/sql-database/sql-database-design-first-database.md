---
title: "aaaDesign 第一個 Azure SQL 資料庫 |Microsoft 文件"
description: "了解 toodesign 第一個 Azure SQL database。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/03/2017
ms.author: carlrab
ms.openlocfilehash: 65f0a1594cbdda7480abf32a847266a073e7560d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-sql-database"></a>設計您的第一個 Azure SQL Database

Azure SQL Database 是關聯式資料庫做為-的中的服務 (DBaaS) hello Microsoft 雲端 ("Azure")。 在此教學課程中，您學習如何 toouse hello Azure 入口網站和[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) 來： 

> [!div class="checklist"]
> * Hello Azure 入口網站中建立資料庫
> * 設定在 hello Azure 入口網站中的伺服器層級防火牆規則
> * 使用 SSMS 連接 toohello 資料庫
> * 使用 SSMS 建立資料表
> * 使用 BCP 大量載入資料
> * 使用 SSMS 查詢該資料
> * 還原先前的 hello 資料庫 tooa[還原時間點](sql-database-recovery-using-backups.md#point-in-time-restore)hello Azure 入口網站中

如果您沒有 Azure 訂用帳戶，請在開始之前先[建立免費帳戶](https://azure.microsoft.com/free/)。

## <a name="prerequisites"></a>必要條件

toocomplete 此教學課程，請確定您已安裝：
- hello 最新版本的[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)。
- hello 最新版本的[BCP 和 SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433)。

## <a name="log-in-toohello-azure-portal"></a>登入 toohello Azure 入口網站

登入 toohello [Azure 入口網站](https://portal.azure.com/)。

## <a name="create-a-blank-sql-database"></a>建立空白 SQL Database

Azure SQL Database 會使用一組定義的[計算和儲存體資源](sql-database-service-tiers.md)建立。 hello 資料庫內建立[Azure 資源群組](../azure-resource-manager/resource-group-overview.md)和[Azure SQL Database 邏輯伺服器](sql-database-features.md)。 

請遵循這些步驟 toocreate 空白的 SQL 資料庫。 

1. 按一下 hello**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕。

2. 選取**資料庫**從 hello**新增**頁面上，並選取**SQL Database**從 hello**資料庫**頁面。 

   ![建立空白資料庫](./media/sql-database-design-first-database/create-empty-database.png)

3. 填寫 hello SQL Database 表單以下列資訊，hello hello 前面影像所示：   

   | 設定       | 建議的值 | 說明 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **資料庫名稱** | mySampleDatabase | 如需有效的資料庫名稱，請參閱[資料庫識別碼](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)。 | 
   | **訂用帳戶** | 您的訂用帳戶  | 如需訂用帳戶的詳細資訊，請參閱[訂用帳戶](https://account.windowsazure.com/Subscriptions)。 |
   | **資源群組** | myResourceGroup | 如需有效的資源群組名稱，請參閱[命名規則和限制](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)。 |
   | **選取來源** | 空白資料庫 | 指定應建立空白資料庫。 |

4. 按一下**伺服器**toocreate 及設定新的伺服器，為您新的資料庫。 填寫 hello**表單的新伺服器**以 hello 下列資訊： 

   | 設定       | 建議的值 | 說明 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器名稱** | 任何全域唯一名稱 | 如需有效的伺服器名稱，請參閱[命名規則和限制](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)。 | 
   | **伺服器管理員登入** | 任何有效名稱 | 如需有效的登入名稱，請參閱[資料庫識別碼](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)。|
   | **密碼** | 任何有效密碼 | 您的密碼必須至少為 8 個字元，且必須包含下列類別目錄的 hello 的其中三種字元： 大寫字母、 小寫字元、 數字和非英數字元。 |
   | **位置** | 任何有效位置 | 如需區域的相關資訊，請參閱 [Azure 區域](https://azure.microsoft.com/regions/)。 |

   ![建立資料庫伺服器](./media//sql-database-design-first-database/create-database-server.png)

5. 按一下 [選取] 。

6. 按一下**定價層**toospecify hello 服務層和效能層級的新資料庫。 針對此快速入門，選取 [20 DTUs (20 個 DTU)] 和 [250] GB 儲存體。

   ![建立資料庫-s1](./media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. 按一下 [Apply (套用)] 。  

8. 選取**定序**hello （適用於此教學課程中，使用 hello 預設值） 的空白資料庫。 如需定序的詳細資訊，請參閱[定序](https://docs.microsoft.com/sql/t-sql/statements/collations)。

9. 按一下**建立**tooprovision hello 資料庫。 提供有關分鐘半 toocomplete 採用。 

10. 在 [hello] 工具列上按一下**通知**toomonitor hello 部署程序。

   ![通知](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a>建立伺服器層級防火牆規則

hello SQL Database 服務會建立防火牆 hello 伺服器層級，避免外部應用程式和工具連接 toohello 伺服器或 hello 伺服器上的任何資料庫，除非針對特定的 IP 位址的 tooopen hello 防火牆就會建立防火牆規則。 請遵循這些步驟 toocreate [SQL Database 伺服器層級防火牆規則](sql-database-firewall-configure.md)對您的用戶端 IP 位址，並透過您的 IP 位址只的 hello SQL Database 防火牆的外部連接。 

> [!NOTE]
> SQL Database 會透過連接埠 1433 通訊。 如果您嘗試 tooconnect 從公司網路內，由您的網路防火牆可能不允許透過通訊埠 1433年的輸出流量。 如果是這樣，您無法連接 tooyour Azure SQL Database 伺服器，除非您的 IT 部門會開啟通訊埠 1433年。
>

1. Hello 部署完成之後，請按一下**SQL 資料庫**從 hello 左側功能表，然後按一下**mySampleDatabase**上 hello **SQL 資料庫**頁面。 hello 概觀 頁面的資料庫會開啟，顯示您 hello 完全符合規定的伺服器名稱 (例如**mynewserver20170313.database.windows.net**)，並提供進一步組態的選項。 將這個完整伺服器名稱複製起來，以供稍後使用。

   > [!IMPORTANT]
   > 您需要此完整的伺服器名稱 tooconnect tooyour 伺服器和其後續的快速入門中的資料庫。
   > 

   ![伺服器名稱](./media/sql-database-connect-query-dotnet/server-name.png) 

2. 按一下**設定伺服器防火牆**hello 工具列 hello 如上圖所示。 hello**防火牆設定**hello SQL 資料庫伺服器 頁面隨即開啟。 

   ![伺服器防火牆規則](./media/sql-database-get-started-portal/server-firewall-rule.png) 


3. 按一下**新增用戶端 IP** hello 工具列 tooadd 上目前的 IP 位址 tooa 新防火牆規則。 防火牆規則可以針對單一 IP 位址或 IP 位址範圍開啟連接埠 1433。

4. 按一下 [儲存] 。 為開啟通訊埠 1433 hello 邏輯伺服器上的目前的 IP 位址建立伺服器層級防火牆規則。

   ![設定伺服器防火牆規則](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. 按一下**確定**，然後關閉 hello**防火牆設定**頁面。

您現在可以連接 toohello SQL Database 伺服器和資料庫使用 SQL Server Management Studio 或您選擇從這個 IP 位址，使用先前建立的 hello 伺服器系統管理員帳戶的其他工具。

> [!IMPORTANT]
> 根據預設，透過 hello SQL Database 防火牆會啟用所有 Azure 服務。 按一下**OFF**上所有的 Azure 服務的這個頁面 toodisable。

## <a name="sql-server-connection-information"></a>SQL Server 連線資訊

取得 hello Azure 入口網站中的 hello Azure SQL Database 伺服器的完整的伺服器名稱。 您使用 hello 完整的伺服器名稱 tooconnect tooyour 伺服器使用 SQL Server Management Studio。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。 
3. 在 [hello **Essentials** hello Azure 入口網站頁面，為您的資料庫中] 窗格找到並複製 hello**伺服器名稱**。

   ![連線資訊](./media/sql-database-connect-query-dotnet/server-name.png)

## <a name="connect-toohello-database-with-ssms"></a>使用 SSMS 連接 toohello 資料庫

使用[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) tooestablish 連接 tooyour Azure SQL Database 伺服器。

1. 開啟 SQL Server Management Studio。

2. 在 hello**連接 tooServer**對話方塊方塊中，輸入下列資訊的 hello:

   | 設定       | 建議的值 | 說明 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | 伺服器類型 | 資料庫引擎 | 這是必要值 |
   | 伺服器名稱 | hello 完整的伺服器名稱 | hello 名稱應該像下面這樣： **mynewserver20170313.database.windows.net**。 |
   | 驗證 | SQL Server 驗證 | SQL 驗證是我們已在此教學課程中的 hello 唯一的驗證類型。 |
   | 登入 | hello 伺服器系統管理員帳戶 | 這是您指定當您建立 hello 伺服器 hello 帳戶。 |
   | 密碼 | hello 伺服器系統管理員帳戶的密碼 | 這是您指定當您建立 hello 伺服器 hello 密碼。 |

   ![連接 tooserver](./media/sql-database-connect-query-ssms/connect.png)

3. 按一下**選項**在 hello**連接 tooserver**  對話方塊。 在 hello**連接 toodatabase**區段中，輸入**mySampleDatabase** tooconnect toothis 資料庫。

   ![連接的伺服器上的 toodb](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. 按一下 [ **連接**]。 在 SSMS 中，開啟 hello 物件總管 視窗。 

5. 在 物件總管 中，展開**資料庫**，然後展開  **mySampleDatabase** tooview hello 範例資料庫中的 hello 物件。

   ![資料庫物件](./media/sql-database-connect-query-ssms/connected.png)  

## <a name="create-tables-in-hello-database"></a>Hello 資料庫中建立資料表 

使用四個資料表建立資料庫結構描述，其會使用 [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference) 建立大學的學生管理系統模型：

- Person
- 課程
- 學生
- 建立大學專屬學生管理系統的信用額度

hello 下圖顯示這些資料表的其他相關的 tooeach 的方式。 在這當中有部分資料表會參考其他資料表的資料欄。 例如，hello 學生資料表參考 hello **PersonId** hello 的資料行**人員**資料表。 研究 hello 圖表 toounderstand hello 本教學課程中的資料表是相關的 tooone 另一個。 深入了解如何針對 toocreate 有效的資料庫資料表，請參閱[建立有效的資料庫資料表](https://msdn.microsoft.com/library/cc505842.aspx)。 如需選擇資料類型的相關資訊，請參閱[資料類型 (英文)](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql)。

> [!NOTE]
> 您也可以使用 hello[資料表設計工具中 SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) toocreate 和設計您的資料表。 

![資料表關聯性](./media/sql-database-design-first-database/tutorial-database-tables.png)

1. 在 物件總管 中，於 **mySampleDatabase** 上按一下滑鼠右鍵，然後按一下新增查詢。 空白查詢視窗，也就是開啟連接的 tooyour 資料庫。

2. 在 hello 查詢視窗中，執行下列查詢 toocreate 四份資料表在資料庫中的 hello: 

   ```sql 
   -- Create Person table

   CREATE TABLE Person
   (
   PersonId   INT IDENTITY PRIMARY KEY,
   FirstName   NVARCHAR(128) NOT NULL,
   MiddelInitial NVARCHAR(10),
   LastName   NVARCHAR(128) NOT NULL,
   DateOfBirth   DATE NOT NULL
   )
   
   -- Create Student table
 
   CREATE TABLE Student
   (
   StudentId INT IDENTITY PRIMARY KEY,
   PersonId  INT REFERENCES Person (PersonId),
   Email   NVARCHAR(256)
   )
   
   -- Create Course table
 
   CREATE TABLE Course
   (
   CourseId  INT IDENTITY PRIMARY KEY,
   Name   NVARCHAR(50) NOT NULL,
   Teacher   NVARCHAR(256) NOT NULL
   ) 

   -- Create Credit table
 
   CREATE TABLE Credit
   (
   StudentId   INT REFERENCES Student (StudentId),
   CourseId   INT REFERENCES Course (CourseId),
   Grade   DECIMAL(5,2) CHECK (Grade <= 100.00),
   Attempt   TINYINT,
   CONSTRAINT  [UQ_studentgrades] UNIQUE CLUSTERED
   (
   StudentId, CourseId, Grade, Attempt
   )
   )
   ```

   ![建立資料表](./media/sql-database-design-first-database/create-tables.png)

3. 展開 hello SQL Server Management Studio 物件總管 中 toosee hello 您建立的資料表中的 hello 「 資料表 」 節點。

   ![建立 ssms 資料表](./media/sql-database-design-first-database/ssms-tables-created.png)

## <a name="load-data-into-hello-tables"></a>資料載入至 hello 資料表

1. 建立資料夾，稱為**SampleTableData**您下載資料夾 toostore 的範例資料為您的資料庫中。 

2. 以滑鼠右鍵按一下 hello 下列連結，並將它們儲存成 hello **SampleTableData**資料夾。 

   - [SampleCourseData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCourseData)
   - [SamplePersonData](https://sqldbtutorial.blob.core.windows.net/tutorials/SamplePersonData)
   - [SampleStudentData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleStudentData)
   - [SampleCreditData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCreditData)

3. 開啟 [命令提示字元] 視窗，並瀏覽 toohello SampleTableData 資料夾。

4. 執行下列命令 tooinsert 範例資料插入 hello 資料表取代 hello 值的 hello **ServerName**， **DatabaseName**， **UserName**，和**密碼**與您的環境的 hello 值。
  
   ```bcp
   bcp Course in SampleCourseData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Person in SamplePersonData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Student in SampleStudentData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Credit in SampleCreditData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   ```

您現在已將您稍早建立的 hello 資料表載入資料範例。

## <a name="query-data"></a>查詢資料

執行 hello hello 資料庫資料表中的下列查詢 tooretrieve 資訊。 請參閱[撰寫 SQL 查詢](https://technet.microsoft.com/library/bb264565.aspx)toolearn 深入了解撰寫 SQL 查詢。 hello 第一個查詢會聯結所有四個資料表 toofind 所有 hello 學生都教導由 'Dominick 教宗' 他類別中具有高於 75%的等級。 hello 第二個查詢聯結所有的四個資料表，並尋找所在 'Noe 智傑' 曾經已註冊的所有課程。

1. 在 SQL Server Management Studio 查詢視窗中，執行下列查詢的 hello:

   ```sql 
   -- Find hello students taught by Dominick Pope who have a grade higher than 75%

   SELECT  person.FirstName,
   person.LastName,
   course.Name,
   credit.Grade
   FROM  Person AS person
   INNER JOIN Student AS student ON person.PersonId = student.PersonId
   INNER JOIN Credit AS credit ON student.StudentId = credit.StudentId
   INNER JOIN Course AS course ON credit.CourseId = course.courseId
   WHERE course.Teacher = 'Dominick Pope' 
   AND Grade > 75
   ```

2. 在 [SQL Server Management Studio] 查詢視窗中，執行下列查詢︰

   ```sql
   -- Find all hello courses in which Noe Coleman has ever enrolled

   SELECT  course.Name,
   course.Teacher,
   credit.Grade
   FROM  Course AS course
   INNER JOIN Credit AS credit ON credit.CourseId = course.CourseId
   INNER JOIN Student AS student ON student.StudentId = credit.StudentId
   INNER JOIN Person AS person ON person.PersonId = student.PersonId
   WHERE person.FirstName = 'Noe'
   AND person.LastName = 'Coleman'
   ```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>還原資料庫 tooa 前一個點的時間

假設您不小心刪除了資料表。 這是您無法輕易復原的情況。 Azure SQL Database 可讓您 toogo 後 tooany 點時間 hello 上次向上 too35 天並還原階段 tooa 新資料庫中的這一點。 您可以此資料庫 toorecover 刪除的資料。 hello 下列步驟之前，還原 hello 範例資料庫 tooa 點 hello 資料表加入。

1. 在 hello 您資料庫的 SQL Database 頁面上，按一下 **還原**hello 工具列上。 hello**還原**頁面隨即開啟。

   ![還原](./media/sql-database-design-first-database/restore.png)

2. 填寫 hello**還原**hello 所需資訊的表單：
    * 資料庫名稱︰提供資料庫名稱 
    * 時間點： 選取 hello**時間點**hello 還原表單上的索引標籤 
    * 還原點： 選取 hello 資料庫已變更之前發生的時間
    * 目標伺服器︰還原資料庫時，您無法變更此值 
    * 彈性資料庫集區：選取 [無]  
    * 定價層：選取 [20 DTU] 和 [250 GB] 的儲存體。

   ![還原點](./media/sql-database-design-first-database/restore-point.png)

3. 按一下**確定**toorestore hello 資料庫太[還原時間點 tooa](sql-database-recovery-using-backups.md#point-in-time-restore) hello 資料表加入之前。 還原資料庫 tooa 不同點時間 hello 中建立重複的資料庫與 as of 時間點 hello hello 原始資料庫相同的伺服器指定，只要 hello 的保留期限內您[服務層](sql-database-service-tiers.md)。

## <a name="next-steps"></a>後續步驟 
在本教學課程中，您已了解基本的資料庫工作，例如建立資料庫和資料表、 載入和查詢資料，以及還原 hello 資料庫 tooa 前一個點的時間。 您已了解如何︰
> [!div class="checklist"]
> * 建立資料庫
> * 設定防火牆規則
> * 連接與 toohello 資料庫[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)
> * 建立資料表
> * 大量載入資料
> * 查詢該資料
> * 使用 SQL Database 的時間還原 hello 資料庫 tooa 先前點[還原時間點](sql-database-recovery-using-backups.md#point-in-time-restore)功能

前進 toohello 下一個教學課程的 toolearn 關於設計資料庫，使用 Visual Studio 和 C#。

> [!div class="nextstepaction"]
>[設計 Azure SQL Database 並連接 C# 和 ADO.NET](sql-database-design-first-database-csharp.md)
