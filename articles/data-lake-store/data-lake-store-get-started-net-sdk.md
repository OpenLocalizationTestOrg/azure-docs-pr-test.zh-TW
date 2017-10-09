---
title: "aaaUse hello.NET SDK toodevelop 應用程式在 Azure Data Lake Store |Microsoft 文件"
description: "使用 Azure 資料湖存放區.NET SDK toocreate Data Lake Store 帳戶，並在 hello 資料湖存放區中執行基本作業"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ea57d5a9-2929-4473-9d30-08227912aba7
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: nitinme
ms.openlocfilehash: cb3a1dfb2f6379f728069d66b0ee77ce0f838fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a>使用 .NET SDK 開始使用 Azure Data Lake Store
> [!div class="op_single_selector"]
> * [入口網站](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

深入了解如何 toouse hello [Azure 資料湖存放區.NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform 基本作業，例如建立資料夾、 上傳和下載資料檔案，依此類推。如需有關 Data Lake 的詳細資訊，請參閱 [Azure Data Lake Store](data-lake-store-overview.md)。

## <a name="prerequisites"></a>必要條件
* **Visual Studio 2013、2015 或 2017**。 下列的 hello 指示使用 Visual Studio 2015 Update 2。

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。

* **Azure Data Lake Store 帳戶**。 如需有關指示 toocreate 的帳戶，請參閱[開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)

* **建立 Azure Active Directory 應用程式**。 您可以使用 hello Azure AD 應用程式 tooauthenticate hello Data Lake Store 應用程式與 Azure AD。 有不同的方法 tooauthenticate 與 Azure AD，這是**使用者驗證**或**服務對服務驗證**。 如需指示和詳細資訊 tooauthenticate，請參閱[使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)或[服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。

## <a name="create-a-net-application"></a>建立 .NET 應用程式
1. 開啟 Visual Studio，建立主控台應用程式。
2. 從 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。
3. 從**新專案**，輸入或選取下列值的 hello:

   | 屬性 | 值 |
   | --- | --- |
   | 類別 |範本/Visual C#/Windows |
   | 範本 |主控台應用程式 |
   | 名稱 |CreateADLApplication |
4. 按一下**確定**toocreate hello 專案。
5. 加入 hello Nuget 封裝 tooyour 專案。

   1. Hello hello 方案總管 中的專案名稱上按一下滑鼠右鍵，然後按一下**管理 NuGet 封裝**。
   2. 在 hello **Nuget 套件管理員**索引標籤上，請確定**套件來源**設定得**nuget.org**而且**包含發行前版本**核取方塊已選取。
   3. 搜尋並安裝下列 NuGet 套件 hello:

      * `Microsoft.Azure.Management.DataLake.Store` - 本教學課程使用 v2.1.3-preview。
      * `Microsoft.Rest.ClientRuntime.Azure.Authentication` - 本教學課程使用 v2.2.12。

        ![新增 Nuget 來源](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "建立新的 Azure Data Lake 帳戶")
   4. 關閉 hello **Nuget 套件管理員**。
6. 開啟**Program.cs**刪除 hello 現有程式碼，然後加入下列陳述式 tooadd 參考 toonamespaces hello。

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. 宣告 hello 變數，如下所示，並提供 hello 值的資料湖存放區名稱和 hello 資源群組名稱已存在。 此外，請確定 hello 本機路徑和檔案名稱您在此處提供必須存在於 hello 電腦。 新增下列程式碼片段在 hello 命名空間宣告之後的 hello。

        namespace SdkSample
        {
            class Program
            {
                private static DataLakeStoreAccountManagementClient _adlsClient;
                private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;

                private static string _adlsAccountName;
                private static string _resourceGroupName;
                private static string _location;
                private static string _subId;

                private static void Main(string[] args)
                {
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with hello name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with hello name of hello resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

在 hello 剩餘 hello 發行項的區段，您可以看到 toouse hello 可用.NET 方法 tooperform 作業，例如驗證、 檔案上傳等等的方式。

## <a name="authentication"></a>驗證

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a>如果您要使用使用者驗證 (本教學課程建議的驗證方式)

搭配使用現有的 Azure AD 原生應用程式 tooauthenticate 您的應用程式**以互動方式**，這表示您會收到提示 tooenter 您的 Azure 認證。

為了方便使用，hello 以下程式碼片段會使用預設值，用戶端識別碼和重新導向 URI，將會使用任何 Azure 訂用帳戶。 toohelp 更快完成本教學課程中，我們建議使用此方法。 在 hello 以下程式碼片段，只要提供 hello 值您的租用戶識別碼。 您可以擷取使用所提供的 hello 指示[建立 Active Directory 應用程式](data-lake-store-end-user-authenticate-using-active-directory.md)。

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

幾個事項 tooknow 有關上述這個程式碼片段：

* toohelp 更快完成 hello 教學課程中，此程式碼片段使用的 Azure AD 網域和用戶端根據預設，所有的 Azure 訂用帳戶的識別碼。 因此，您可以**在應用程式中原封不動地使用此程式碼片段**。
* 不過，如果您想 toouse 您自己的 Azure AD 網域與應用程式用戶端識別碼，您必須建立 Azure AD 的原生應用程式，然後使用 hello Azure AD 租用戶識別碼、 用戶端識別碼和重新導向 URI hello 應用程式建立。 如需相關指示，請參閱[建立 Active Directory 應用程式以使用 Data Lake Store 進行使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)。

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a>如果您要使用服務對服務驗證與用戶端密碼
下列程式碼片段 hello 可以是您的應用程式使用的 tooauthenticate**非互動方式**、 使用 hello 用戶端密碼 / 金鑰的應用程式 / 服務主體。 請將此方法用於現有的 Azure AD「Web 應用程式」應用程式。 如需有關如何 toocreate hello Azure AD web 應用程式，以及如何 tooretrieve hello 用戶端識別碼和用戶端密碼需要在 hello 以下程式碼片段，請參閱指示[使用資料建立服務對服務驗證 Active Directory 應用程式Lake Store](data-lake-store-authenticate-using-active-directory.md)。

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a>如果您要使用服務對服務驗證與憑證

第三個選項，hello 如下列程式碼片段可以是使用的 tooauthenticate 您的應用程式**非互動方式**、 hello 憑證使用 Azure Active Directory 應用程式 / 服務主體。 請將此方法用於現有的 [Azure AD 與憑證](../azure-resource-manager/resource-group-authenticate-service-principal.md)。

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a>建立用戶端物件
hello 下列程式碼片段會建立 hello Data Lake Store 帳戶和檔案系統所使用的用戶端物件 tooissue toohello 服務要求。

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a>列出訂用帳戶內的所有 Data Lake Store 帳戶
hello 下列程式碼片段列出給定 Azure 訂用帳戶內的所有 Data Lake Store 帳戶。

    // List all ADLS accounts within hello subscription
    public static async Task<List<DataLakeStoreAccount>> ListAdlStoreAccounts()
    {
        var response = await _adlsClient.Account.ListAsync();
        var accounts = new List<DataLakeStoreAccount>(response);

        while (response.NextPageLink != null)
        {
            response = _adlsClient.Account.ListNext(response.NextPageLink);
            accounts.AddRange(response);
        }

        return accounts;
    }

## <a name="create-a-directory"></a>建立目錄
下列程式碼片段說明 hello`CreateDirectory`方法，您可以使用 toocreate Data Lake Store 帳戶內的目錄。

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a>上傳檔案
下列程式碼片段說明 hello`UploadFile`方法，您可以使用 tooupload 檔案 tooa Data Lake Store 帳戶。

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

hello SDK 支援遞迴上傳和下載之間的本機檔案路徑和 Data Lake Store 檔案路徑。    

## <a name="get-file-or-directory-info"></a>取得檔案或目錄資訊
下列程式碼片段說明 hello`GetItemInfo`方法可讓您 tooretrieve 資訊的檔案或目錄的可用資料湖存放區中。

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a>列出檔案或目錄
下列程式碼片段說明 hello `ListItem` toolist hello 檔案和目錄中可用的 Data Lake Store 帳戶的方法。

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a>串連檔案
下列程式碼片段說明 hello`ConcatenateFiles`您使用 tooconcatenate 檔案的方法。

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a>附加 tooa 檔
下列程式碼片段說明 hello`AppendToFile`附加資料 tooa 檔已儲存在 Data Lake Store 帳戶，您使用的方法。

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a>下載檔案
下列程式碼片段說明 hello`DownloadFile`方法，您會使用 toodownload 來自 Data Lake Store 帳戶的檔案。

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a>後續步驟
* [保護 Data Lake Store 中的資料](data-lake-store-secure-data.md)
* [搭配 Data Lake Store 使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [搭配 Data Lake Store 使用 Azure HDInsight](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Data Lake Store .NET SDK 參考](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [Data Lake Store REST 參考](https://msdn.microsoft.com/library/mt693424.aspx)
