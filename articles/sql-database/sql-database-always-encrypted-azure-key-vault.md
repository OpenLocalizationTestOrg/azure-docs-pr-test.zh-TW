---
title: "永遠加密：SQL Database - Azure Key Vault | Microsoft Docs"
description: "本文章將示範如何 toosecure 資料加密使用的 SQL 資料庫中的敏感性資料 hello 永遠加密精靈 在 SQL Server Management Studio。 它也包含指示，教您如何 toostore Azure 金鑰保存庫中的每個加密金鑰。"
keywords: "資料加密, 加密金鑰, 雲端加密"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: 6ca16644-5969-497b-a413-d28c3b835c9b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: sstein
ms.openlocfilehash: 8226bfef584e979643f5bb0747d4df16569f8204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a>一律加密：保護 SQL Database 中的機密資料，並將加密金鑰儲存在「Azure 金鑰保存庫」中

本文將告訴您如何 toosecure 敏感性資料，在 SQL 資料庫與資料加密使用 hello[永遠加密精靈](https://msdn.microsoft.com/library/mt459280.aspx)中[SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx)。 它也包含指示，教您如何 toostore Azure 金鑰保存庫中的每個加密金鑰。

永遠加密已在 Azure SQL Database 的新資料加密技術，可幫助的 SQL Server 進行用戶端與伺服器之間，以及使用 hello 資料時移動時保護靜止 hello 伺服器上的機密資料。 一律加密可確保敏感性資料，永遠不會顯示為 hello 資料庫系統內的純文字。 設定資料加密之後，只有用戶端應用程式或具有存取 toohello 金鑰的應用程式伺服器可以存取純文字資料。 如需詳細資訊，請參閱 [一律加密 (資料庫引擎)](https://msdn.microsoft.com/library/mt163865.aspx)。

設定永遠加密的 hello 資料庫 toouse 之後，您將建立用戶端應用程式中使用 C# 和 Visual Studio toowork hello 加密資料。

請遵循本文章中的 hello 步驟，並了解如何為 Azure SQL database 的 tooset 設定永遠加密。 在本文中，您將學習影響 tooperform hello 下列工作：

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
* [Azure PowerShell](/powershell/azure/overview) 1.0 或更新版本。 型別**(Get-module azure ListAvailable)。版本**toosee 執行的 PowerShell 版本。

## <a name="enable-your-client-application-tooaccess-hello-sql-database-service"></a>啟用用戶端應用程式 tooaccess hello SQL Database 服務
您必須啟用用戶端應用程式 tooaccess hello SQL Database 服務藉由設定 hello 必要的驗證和取得 hello *ClientId*和*密碼*，您將需要 tooauthenticate下列程式碼的 hello 中的應用程式。

1. 開啟 hello [Azure 傳統入口網站](http://manage.windowsazure.com)。
2. 選取**Active Directory** ，按一下 應用程式將使用的 hello Active Directory 執行個體。
3. 按一下 應用程式，然後按一下新增。
4. 輸入您的應用程式的名稱 (例如： *myClientApp*)，請選取**WEB 應用程式**，然後按一下 hello 箭號 toocontinue。
5. Hello**登入 URL**和**應用程式識別碼 URI**您可以輸入有效的 URL (例如， *http://myClientApp*)，並繼續。
6. 按一下 [設定] 。
7. 複製您的 [用戶端識別碼] 。 (您之後在程式碼中將需要此值)。
8. 在 hello**金鑰**區段中，選取**1 年**從 hello**選取持續時間**下拉式清單。 （您將可以複製 hello 金鑰之後，您將儲存在步驟 13）。
9. 向下捲動並按一下 [新增應用程式] 。
10. 保留**顯示**設定得**Microsoft 應用程式**選取**Microsoft Azure 服務管理 API**。 按一下 hello 核取記號 toocontinue。
11. 選取**存取 Azure 服務管理...**從 hello**委派的權限**下拉式清單。
12. 按一下 [儲存] 。
13. 儲存完成的 hello 之後, 將 hello 索引鍵值複製 hello**金鑰**> 一節。 (您之後在程式碼中將需要此值)。

## <a name="create-a-key-vault-toostore-your-keys"></a>您的金鑰建立金鑰保存庫 toostore
現在已設定您的用戶端應用程式，並可讓用戶端識別碼，它是時間 toocreate 金鑰保存庫，並設定其存取原則，讓您和您的應用程式可以存取保存庫 hello 機密資料 （hello 永遠加密金鑰）。 hello*建立*，*取得*，*清單*，*登*，*確認*， *wrapKey*，和*unwrapKey*不需要建立新的資料行主要金鑰和設定加密與 SQL Server Management Studio 的權限。

您可以執行下列指令碼的 hello，快速建立金鑰保存庫。 如需這些 Cmdlet 的詳細說明，以及有關建立及設定金鑰保存庫的詳細資訊，請參閱[開始使用 Azure 金鑰保存庫](../key-vault/key-vault-get-started.md)。

    $subscriptionName = '<your Azure subscription name>'
    $userPrincipalName = '<username@domain.com>'
    $clientId = '<client ID that you copied in step 7 above>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $vaultName = 'AeKeyVault'


    Login-AzureRmAccount
    $subscriptionId = (Get-AzureRmSubscription -SubscriptionName $subscriptionName).Id
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroupName -Location $location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
    Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list




## <a name="create-a-blank-sql-database"></a>建立空白 SQL Database
1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 跳過**新增** > **資料 + 儲存體** > **SQL Database**。
3. 在新的或現有伺服器上建立名稱為 **Clinic** (診所) 的**空白**資料庫。 如需有關如何 toocreate 資料庫在 hello Azure 入口網站，請參閱詳細指示[第一個 Azure SQL database](sql-database-get-started-portal.md)。
   
    ![建立空白資料庫](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

連接字串將會需要 hello 稍後 hello 教學課程中，因此建立 hello 資料庫之後，請瀏覽 toohello 新實習課程資料庫和複本 hello 的連接字串。 您可以在任何時間，取得 hello 連接字串，但它是簡單 toocopy hello Azure 入口網站中。

1. 跳過**SQL 資料庫** > **診所** > **顯示資料庫的連接字串**。
2. 複製連接字串 hello **ADO.NET**。
   
    ![複製 hello 連接字串](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a>使用 SSMS 連接 toohello 資料庫
開啟 SSMS 並連接 toohello 伺服器與 hello 診所資料庫。

1. 開啟 SSMS。 (跳過**連接** > **Database Engine** tooopen hello**連接 tooServer**如果它未開啟的視窗。)
2. 輸入您的伺服器名稱和認證。 hello SQL 資料庫刀鋒視窗上可以找到 hello 伺服器名稱和 hello 連接字串中您之前複製。 型別 hello 完整的伺服器名稱，包括*.database.windows.net*。
   
    ![複製 hello 連接字串](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

如果 hello**新防火牆規則**視窗隨即開啟，登入 tooAzure 並讓 SSMS 為您建立新的防火牆規則。

## <a name="create-a-table"></a>建立資料表
在本節中，您將建立資料表 toohold 病患資料。 它不是一開始加密-您將設定加密 hello 下一節。

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
SSMS 提供可協助您輕鬆地設定 hello 資料行主要金鑰、 資料行加密金鑰，加密的資料行的和您所設定 永遠加密的精靈。

1. 展開 [資料庫]  > **空白** > ，藉由資料庫加密來保護 SQL Database 中的機密資料。
2. 以滑鼠右鍵按一下 hello**病患**資料表，然後選取**加密資料行**tooopen hello 永遠加密精靈：
   
    ![加密資料行](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

hello 永遠加密精靈包含下列各節的 hello:**資料行選取**，**主要金鑰設定**，**驗證**，和**摘要**.

### <a name="column-selection"></a>資料行選取
按一下**下一步**上 hello**簡介**頁面 tooopen hello**資料行選取**頁面。 這個頁面上，您將選取的資料行要 tooencrypt， [hello 類型的加密，以及哪些資料行加密金鑰 (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse。

請加密每個病患的 **SSN** 和 **BirthDate** 資訊。 hello SSN 資料行都將使用決定性加密，它支援等號比較查閱、 聯結和分組方式。 hello BirthDate 資料行，將使用隨機化的加密，不支援作業。

設定 hello**加密類型**hello SSN 資料行太**決定性**太 hello BirthDate 資料行和**隨機化**。 按一下 [下一步] 。

![加密資料行](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a>主要金鑰組態
hello**主要金鑰設定**頁面是設定您的 CMK 和選取 hello 金鑰存放區提供者 hello CMK 的儲存位置。 目前，您可以在 hello Windows 憑證存放區、 Azure 金鑰保存庫或硬體安全性模組 (HSM) 中儲存 CMK。

本教學課程示範如何 toostore 您在 Azure 金鑰保存庫中的金鑰。

1. 選取 [Azure 金鑰保存庫] 。
2. 從 hello 下拉式清單中選取 hello 所需的金鑰保存庫。
3. 按一下 [下一步] 。

![主要金鑰組態](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a>驗證
您可以現在加密 hello 資料行，或稍後儲存 PowerShell 指令碼 toorun。 此教學課程中，選取**現在繼續 toofinish**按一下**下一步**。

### <a name="summary"></a>摘要
請確認 hello 設定都正確，然後按一下**完成**toocomplete hello 安裝程式的一律加密。

![摘要](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-hello-wizards-actions"></a>確認 hello 精靈的動作
Hello 精靈完成後，您的資料庫設定永遠加密。 hello 精靈執行 hello 下列動作：

* 建立資料行主要金鑰 (CMK) 並將它儲存在「Azure 金鑰保存庫」中。
* 建立資料行加密金鑰 (CMK) 並將它儲存在「Azure 金鑰保存庫」中。
* 設定的 hello 選取加密的資料行。 hello 病患資料表目前有任何資料，但 hello 選取資料行中的任何現有資料已加密。

您可以確認 hello 建立 hello 索引鍵，在 SSMS 中，展開**診所** > **安全性** > **永遠加密金鑰**。

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a>建立搭配 hello 加密資料的用戶端應用程式
現在，永遠加密已設定，您可以建立執行的應用程式*插入*和*選取*hello 上加密的資料行。  

> [!IMPORTANT]
> 您的應用程式必須使用[SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)物件時傳遞純文字資料 toohello server 使用永遠加密資料行。 在不使用 SqlParameter 物件的情況下傳遞常值會導致例外狀況。
> 
> 

1. 開啟 Visual Studio 並建立新的 C# **主控台應用程式**(Visual Studio 2015 和更早版本) 或**主控台應用程式 (.NET Framework)** (Visual Studio 2017 和更新版本)。 請確定您的專案已設定太**.NET Framework 4.6**或更新版本。
2. 名稱 hello 專案**AlwaysEncryptedConsoleAKVApp**按一下**確定**。
3. 安裝下列 NuGet 套件移過 hello**工具** > **NuGet 套件管理員** > **Package Manager Console**。

Hello Package Manager Console 中，執行下列兩行程式碼。

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-tooenable-always-encrypted"></a>修改您的連接字串 tooenable 永遠加密
本章節將說明如何在資料庫連接字串中的 tooenable 永遠加密。

tooenable 永遠加密，您需要 tooadd hello **Column Encryption Setting**關鍵字 tooyour 連接字串，並將它設定太**啟用**。

您可以直接在 hello 連接字串設定，或您可以使用來設定[SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx)。 hello hello 範例應用程式下一節顯示如何 toouse **SqlConnectionStringBuilder**。

### <a name="enable-always-encrypted-in-hello-connection-string"></a>Hello 連接字串中啟用 永遠加密
新增下列關鍵字 tooyour 連接字串 hello。

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a>使用 SqlConnectionStringBuilder 來啟用一律加密
hello 下列程式碼會示範如何藉由設定永遠加密的 tooenable [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx)太[啟用](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx)。

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-hello-azure-key-vault-provider"></a>註冊 hello Azure 金鑰保存庫提供者
hello 下列程式碼會示範如何 tooregister hello hello ADO.NET 驅動程式與 Azure 金鑰保存庫提供者。

    private static ClientCredential _clientCredential;

    static void InitializeAzureKeyVaultProvider()
    {
       _clientCredential = new ClientCredential(clientId, clientSecret);

       SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
          new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

       Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
          new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

       providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
       SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
    }



## <a name="always-encrypted-sample-console-application"></a>一律加密範例主控台應用程式
這個範例會示範如何：

* 修改您永遠加密的連接字串 tooenable。
* 登錄 Azure 金鑰保存庫，因為 hello 應用程式的金鑰存放區提供者。  
* 將資料插入加密的 hello 資料行。
* 在加密資料行中篩選特定值來選取記錄。

取代 hello 內容**Program.cs**以下列程式碼的 hello。 取代 hello hello 全域 connectionString 中的變數直接位於您從 hello Azure 入口網站的有效的連接字串 hello Main 方法的 hello 列的連接字串。 這是 hello 唯一的變更，您需要 toomake toothis 程式碼。

永遠加密的 hello 應用程式 toosee 在中執行動作。

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider;

    namespace AlwaysEncryptedConsoleAKVApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"<connection string from hello portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

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

            InsertPatient(new Patient()
            {
                SSN = "999-99-0001",
                FirstName = "Orlando",
                LastName = "Gee",
                BirthDate = DateTime.Parse("01/04/1964")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0002",
                FirstName = "Keith",
                LastName = "Harris",
                BirthDate = DateTime.Parse("06/20/1977")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0003",
                FirstName = "Donna",
                LastName = "Carreras",
                BirthDate = DateTime.Parse("02/09/1973")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0004",
                FirstName = "Janet",
                LastName = "Gates",
                BirthDate = DateTime.Parse("08/31/1985")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0005",
                FirstName = "Lucy",
                LastName = "Harrington",
                BirthDate = DateTime.Parse("05/06/1993")
            });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
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


        private static ClientCredential _clientCredential;

        static void InitializeAzureKeyVaultProvider()
        {

            _clientCredential = new ClientCredential(clientId, clientSecret);

            SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
              new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
              new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

            providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        }

        public async static Task<string> GetToken(string authority, string resource, string scope)
        {
            var authContext = new AuthenticationContext(authority);
            AuthenticationResult result = await authContext.AcquireTokenAsync(resource, _clientCredential);

            if (result == null)
                throw new InvalidOperationException("Failed tooobtain hello access token");
            return result.AccessToken;
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
您可以快速檢查 hello hello 伺服器上的實際資料由查詢使用 SSMS hello 病患資料加密 (使用目前的連接位置**Column Encryption Setting**尚未啟用)。

執行下列查詢 hello 診所資料庫上的 hello。

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

您可以看到 hello 加密資料行不包含任何純文字資料。

   ![新的主控台應用程式](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

toouse SSMS tooaccess hello 純文字資料，您可以加入 hello *Column Encryption Setting = 啟用*參數 toohello 連線。

1. 在 SSMS 中，於 [物件總管] 中您的伺服器上按一下滑鼠右鍵，然後選擇 [中斷連線]。
2. 按一下**連接** > **Database Engine** tooopen hello**連接 tooServer**視窗，然後按一下**選項**。
3. 按一下 [其他連接參數] 並輸入 **Column Encryption Setting=enabled**。
   
    ![新的主控台應用程式](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. 執行下列查詢 hello 診所資料庫上的 hello。
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     您現在可以看到 hello 加密資料行中的 hello 純文字資料。

    ![新的主控台應用程式](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a>後續步驟
建立使用永遠加密的資料庫之後，您可能想 toodo hello 下列：

* [輪替和清除金鑰](https://msdn.microsoft.com/library/mt607048.aspx)。
* [移轉已經透過一律加密來加密的資料](https://msdn.microsoft.com/library/mt621539.aspx)。

## <a name="related-information"></a>相關資訊
* [一律加密 (用戶端開發)](https://msdn.microsoft.com/library/mt147923.aspx)
* [透明資料加密](https://msdn.microsoft.com/library/bb934049.aspx)
* [SQL Server 加密](https://msdn.microsoft.com/library/bb510663.aspx)
* [一律加密精靈](https://msdn.microsoft.com/library/mt459280.aspx)
* [一律加密部落格](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

