---
title: "一律加密：Azure SQL Database - Windows 憑證存放區 | Microsoft Docs"
description: "本文章將示範如何使用資料庫加密的 SQL 資料庫中的 toosecure 敏感性資料 hello 永遠加密精靈 在 SQL Server Management Studio (SSMS)。 它也會顯示如何 toostore 加密金鑰在 hello Windows 憑證存放區。"
keywords: "加密資料, SQL 加密, 資料庫加密, 機密資料, 一律加密"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: 483f9a2120cc42b732142fc07807d3d8830a0c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a>永遠加密： SQL 資料庫中的機密資料保護和 hello Windows 憑證存放區中儲存加密金鑰

本文將告訴您如何 toosecure 敏感性資料，在 SQL 資料庫，資料庫加密使用 hello[永遠加密精靈](https://msdn.microsoft.com/library/mt459280.aspx)中[SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx)。 它也會顯示如何 toostore 加密金鑰在 hello Windows 憑證存放區。

永遠加密已在 Azure SQL Database 的新資料加密技術和 SQL Server，可協助保護敏感資料待用 hello 在伺服器上，在用戶端與伺服器之間移動期間以及 hello 資料使用中時，永遠不會確保機密資料會顯示為hello 資料庫系統內的純文字。 加密的資料之後，只有用戶端應用程式或具有存取 toohello 金鑰的應用程式伺服器可以存取純文字資料。 如需詳細資訊，請參閱 [一律加密 (資料庫引擎)](https://msdn.microsoft.com/library/mt163865.aspx)。

設定永遠加密的 hello 資料庫 toouse 之後, 您將建立用戶端應用程式中使用 C# 和 Visual Studio toowork hello 加密資料。

如何遵循本文章 toolearn hello 步驟 tooset 設定永遠加密的 Azure SQL database。 本文中，您將學習如何 tooperform hello 下列工作：

* 使用 SSMS toocreate 的 hello 永遠加密精靈[永遠加密金鑰](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3)。
  * 建立 [資料行主要金鑰 (CMK)](https://msdn.microsoft.com/library/mt146393.aspx)。
  * 建立 [資料行加密金鑰 (CEK)](https://msdn.microsoft.com/library/mt146372.aspx)。
* 建立資料庫資料表並將資料行加密。
* 建立的應用程式，將插入、 選取，並顯示 hello 加密資料行的資料。

## <a name="prerequisites"></a>必要條件
針對本教學課程，您將需要：

* Azure 帳戶和訂用帳戶。 如果您沒有帳戶，請註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 13.0.700.242 版或更新版本。
* [.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx)或更新版本 （在 hello 用戶端電腦）。
* [Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)。

## <a name="create-a-blank-sql-database"></a>建立空白 SQL Database
1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 按一下 [新增]  >  [資料 + 儲存體]  >  [SQL Database]。
3. 在新的或現有伺服器上建立名稱為 **Clinic** (診所) 的**空白**資料庫。 如需在 hello Azure 入口網站中建立資料庫的詳細指示，請參閱[第一個 Azure SQL database](sql-database-get-started-portal.md)。
   
    ![建立空白資料庫](./media/sql-database-always-encrypted/create-database.png)

您必須在 hello 教學課程後面 hello 連接字串。 建立 hello 資料庫之後，請移 toohello 新實習課程資料庫和複本 hello 的連接字串。 您可以在任何時間，取得 hello 連接字串，但它是簡單 toocopy 它在 hello Azure 入口網站中。

1. 按一下 [SQL Database]  >  [Clinic]  >  [顯示資料庫連接字串]。
2. 複製連接字串 hello **ADO.NET**。
   
    ![複製 hello 連接字串](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a>使用 SSMS 連接 toohello 資料庫
開啟 SSMS 並連接 toohello 伺服器與 hello 診所資料庫。

1. 開啟 SSMS。 (按一下**連接** > **Database Engine** tooopen hello**連接 tooServer**如果不是開啟的視窗)。
2. 輸入您的伺服器名稱和認證。 hello SQL 資料庫刀鋒視窗上可以找到 hello 伺服器名稱和 hello 連接字串中您之前複製。 型別 hello 完整的伺服器名稱包括*.database.windows.net*。
   
    ![複製 hello 連接字串](./media/sql-database-always-encrypted/ssms-connect.png)

如果 hello**新防火牆規則**視窗隨即開啟，登入 tooAzure 並讓 SSMS 為您建立新的防火牆規則。

## <a name="create-a-table"></a>建立資料表
在本節中，您將建立資料表 toohold 病患資料。 這是一般資料表一開始-您將設定加密 hello 下一節。

1. 展開 [資料庫] 。
2. 以滑鼠右鍵按一下 hello**診所**資料庫中，按一下 **新查詢**。
3. 貼上下列 TRANSACT-SQL (T-SQL) 至新增查詢視窗 hello 的 hello 和**Execute**它。

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a>將資料行加密 (設定「一律加密」)
SSMS 提供的精靈 tooeasily 藉由設定 hello CMK、 CEK 和加密的資料行讓您設定 永遠加密。

1. 展開 [資料庫]  > **空白** > ，藉由資料庫加密來保護 SQL Database 中的機密資料。
2. 以滑鼠右鍵按一下 hello**病患**資料表，然後選取**加密資料行**tooopen hello 永遠加密精靈：
   
    ![加密資料行](./media/sql-database-always-encrypted/encrypt-columns.png)

hello 永遠加密精靈包含下列各節的 hello:**資料行選取**，**主要金鑰設定**(CMK)，**驗證**，和**摘要**。

### <a name="column-selection"></a>資料行選取
按一下**下一步**上 hello**簡介**頁面 tooopen hello**資料行選取**頁面。 這個頁面上，您將選取的資料行要 tooencrypt， [hello 類型的加密，以及哪些資料行加密金鑰 (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse。

請加密每個病患的 **SSN** 和 **BirthDate** 資訊。 hello **SSN**欄將會使用具決定性加密，可支援等號比較查閱、 聯結和分組方式。 hello **BirthDate**欄將會使用隨機的加密，不支援作業。

設定 hello**加密類型**hello **SSN**資料行太**決定性**和 hello **BirthDate**資料行太**隨機**。 按一下 [下一步] 。

![加密資料行](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a>主要金鑰組態
hello**主要金鑰設定**頁面是設定您的 CMK 和選取 hello 金鑰存放區提供者 hello CMK 的儲存位置。 目前，您可以在 hello Windows 憑證存放區、 Azure 金鑰保存庫或硬體安全性模組 (HSM) 中儲存 CMK。 本教學課程會示範如何 toostore hello Windows 憑證中的金鑰存放區。

確認已選取 [Windows 憑證存放區]，然後按 [下一步]。

![主要金鑰組態](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a>驗證
您可以現在加密 hello 資料行，或稍後儲存 PowerShell 指令碼 toorun。 此教學課程中，選取**現在繼續 toofinish**按一下**下一步**。

### <a name="summary"></a>摘要
請確認 hello 設定都正確，然後按一下**完成**toocomplete hello 安裝程式的一律加密。

![摘要](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a>確認 hello 精靈的動作
Hello 精靈完成後，您的資料庫設定永遠加密。 hello 精靈執行 hello 下列動作：

* 建立 CMK。
* 建立 CEK。
* 設定的 hello 選取加密的資料行。 您**病患**資料表目前有任何資料，但 hello 選取資料行中的任何現有資料已加密。

您可以確認 hello 建立 hello 索引鍵，在 SSMS 中藉由選取太**診所** > **安全性** > **永遠加密金鑰**。 您現在可以看到 hello hello 精靈為您產生的新金鑰。

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a>建立搭配 hello 加密資料的用戶端應用程式
現在，永遠加密已設定，您可以建立執行的應用程式*插入*和*選取*hello 上加密的資料行。 toosuccessfully 執行 hello 範例應用程式，您必須執行上 hello hello 永遠加密精靈的執行所在的同一部電腦。 toorun hello 應用程式，另一部電腦上的，您必須部署永遠加密憑證 toohello 電腦執行 hello 用戶端應用程式。  

> [!IMPORTANT]
> 您的應用程式必須使用[SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)物件時傳遞純文字資料 toohello server 使用永遠加密資料行。 在不使用 SqlParameter 物件的情況下傳遞常值會導致例外狀況。
> 
> 

1. 開啟 Visual Studio，建立新的 C# 主控台應用程式。 請確定您的專案已設定太**.NET Framework 4.6**或更新版本。
2. 名稱 hello 專案**AlwaysEncryptedConsoleApp**按一下**確定**。

![新的主控台應用程式](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a>修改您的連接字串 tooenable 永遠加密
本章節將說明如何在資料庫連接字串中的 tooenable 永遠加密。 您將修改 hello 主控台應用程式，您剛建立 hello 下一節，「 永遠加密的範例主控台應用程式。 」

tooenable 永遠加密，您需要 tooadd hello **Column Encryption Setting**關鍵字 tooyour 連接字串，並將它設定太**啟用**。

您可以直接在 hello 連接字串設定，或您可以使用來設定[SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx)。 hello hello 範例應用程式下一節顯示如何 toouse **SqlConnectionStringBuilder**。

> [!NOTE]
> 這是 hello 唯一需要在用戶端應用程式特定 tooAlways 加密的變更。 如果您有現有的應用程式儲存其連接字串外部 (也就是在組態檔中)，您可能會無法 tooenable 永遠加密，而不需要變更任何程式碼。
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a>Hello 連接字串中啟用 永遠加密
新增下列關鍵字 tooyour 連接字串的 hello:

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a>使用 SqlConnectionStringBuilder 啟用一律加密
hello 下列程式碼會示範如何藉由設定永遠加密的 tooenable hello [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx)太[啟用](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx)。

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a>一律加密範例主控台應用程式
這個範例會示範如何：

* 修改您永遠加密的連接字串 tooenable。
* 將資料插入加密的 hello 資料行。
* 在加密資料行中篩選特定值來選取記錄。

取代 hello 內容**Program.cs**以下列程式碼的 hello。 Hello 以取代連接字串 hello 列上方 hello Main 方法中的 hello 全域 connectionString 變數有效的連接字串從 hello Azure 入口網站。 這是 hello 唯一的變更，您需要 toomake toothis 程式碼。

永遠加密的 hello 應用程式 toosee 在中執行動作。

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter tooexit...");
            Console.ReadLine();
        }


        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
         VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in hello Patients table tooreset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }


## <a name="verify-that-hello-data-is-encrypted"></a>驗證已加密 hello 資料
您可以快速檢查 hello hello 伺服器上的實際資料由查詢 hello 加密**病患**使用 SSMS 的資料。 （使用目前的連接位置 hello 資料行加密設定尚未啟用）。

執行下列查詢 hello 診所資料庫上的 hello。

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

您可以看到 hello 加密資料行不包含任何純文字資料。

   ![新的主控台應用程式](./media/sql-database-always-encrypted/ssms-encrypted.png)

toouse SSMS tooaccess hello 純文字資料，您可以加入 hello **Column Encryption Setting = 啟用**參數 toohello 連線。

1. 在 SSMS 中，於 物件總管 中您的伺服器上按一下滑鼠右鍵，然後按一下中斷連線。
2. 按一下**連接** > **Database Engine** tooopen hello**連接 tooServer**視窗中，然後再按一下**選項**。
3. 按一下 [其他連接參數] 並輸入 **Column Encryption Setting=enabled**。
   
    ![新的主控台應用程式](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. 執行 hello 下列查詢在 hello**診所**資料庫。
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     您現在可以看到 hello 加密資料行中的 hello 純文字資料。

    ![新的主控台應用程式](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> 如果您使用 SSMS （或任何用戶端） 從另一部電腦連接時，它不會存取 toohello 加密金鑰，並不會無法 toodecrypt hello 資料。
> 
> 

## <a name="next-steps"></a>後續步驟
建立使用永遠加密的資料庫之後，您可能想 toodo hello 下列：

* 從不同的電腦執行此範例。 它將不能存取 toohello 加密金鑰，因此不會存取 toohello 純文字資料，並將無法順利執行。
* [輪替和清除金鑰](https://msdn.microsoft.com/library/mt607048.aspx)。
* [移轉已經透過一律加密來加密的資料](https://msdn.microsoft.com/library/mt621539.aspx)。
* [部署 永遠加密憑證 tooother 用戶端機器](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1)（請參閱 hello 「 使憑證可用 tooApplications 」 和 「 使用者 」 一節）。

## <a name="related-information"></a>相關資訊
* [一律加密 (用戶端開發)](https://msdn.microsoft.com/library/mt147923.aspx)
* [透明資料加密](https://msdn.microsoft.com/library/bb934049.aspx)
* [SQL Server 加密](https://msdn.microsoft.com/library/bb510663.aspx)
* [Always Encrypted Wizard (一律加密精靈)](https://msdn.microsoft.com/library/mt459280.aspx)
* [Always Encrypted Blog (一律加密部落格)](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

