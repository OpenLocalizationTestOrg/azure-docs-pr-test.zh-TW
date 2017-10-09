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
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a><span data-ttu-id="7f9e2-103">使用 .NET SDK 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7f9e2-103">Get started with Azure Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f9e2-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="7f9e2-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="7f9e2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f9e2-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="7f9e2-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="7f9e2-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="7f9e2-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="7f9e2-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="7f9e2-108">REST API</span><span class="sxs-lookup"><span data-stu-id="7f9e2-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="7f9e2-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7f9e2-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="7f9e2-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="7f9e2-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="7f9e2-111">Python</span><span class="sxs-lookup"><span data-stu-id="7f9e2-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="7f9e2-112">深入了解如何 toouse hello [Azure 資料湖存放區.NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform 基本作業，例如建立資料夾、 上傳和下載資料檔案，依此類推。如需有關 Data Lake 的詳細資訊，請參閱 [Azure Data Lake Store](data-lake-store-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-112">Learn how toouse hello [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f9e2-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="7f9e2-113">Prerequisites</span></span>
* <span data-ttu-id="7f9e2-114">**Visual Studio 2013、2015 或 2017**。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-114">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="7f9e2-115">下列的 hello 指示使用 Visual Studio 2015 Update 2。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-115">hello instructions below use Visual Studio 2015 Update 2.</span></span>

* <span data-ttu-id="7f9e2-116">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-116">**An Azure subscription**.</span></span> <span data-ttu-id="7f9e2-117">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="7f9e2-118">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-118">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="7f9e2-119">如需有關指示 toocreate 的帳戶，請參閱[開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7f9e2-119">For instructions on how toocreate an account, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

* <span data-ttu-id="7f9e2-120">**建立 Azure Active Directory 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-120">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="7f9e2-121">您可以使用 hello Azure AD 應用程式 tooauthenticate hello Data Lake Store 應用程式與 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-121">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="7f9e2-122">有不同的方法 tooauthenticate 與 Azure AD，這是**使用者驗證**或**服務對服務驗證**。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-122">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="7f9e2-123">如需指示和詳細資訊 tooauthenticate，請參閱[使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)或[服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="7f9e2-124">建立 .NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="7f9e2-124">Create a .NET application</span></span>
1. <span data-ttu-id="7f9e2-125">開啟 Visual Studio，建立主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-125">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="7f9e2-126">從 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-126">From hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="7f9e2-127">從**新專案**，輸入或選取下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="7f9e2-127">From **New Project**, type or select hello following values:</span></span>

   | <span data-ttu-id="7f9e2-128">屬性</span><span class="sxs-lookup"><span data-stu-id="7f9e2-128">Property</span></span> | <span data-ttu-id="7f9e2-129">值</span><span class="sxs-lookup"><span data-stu-id="7f9e2-129">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="7f9e2-130">類別</span><span class="sxs-lookup"><span data-stu-id="7f9e2-130">Category</span></span> |<span data-ttu-id="7f9e2-131">範本/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="7f9e2-131">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="7f9e2-132">範本</span><span class="sxs-lookup"><span data-stu-id="7f9e2-132">Template</span></span> |<span data-ttu-id="7f9e2-133">主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="7f9e2-133">Console Application</span></span> |
   | <span data-ttu-id="7f9e2-134">名稱</span><span class="sxs-lookup"><span data-stu-id="7f9e2-134">Name</span></span> |<span data-ttu-id="7f9e2-135">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="7f9e2-135">CreateADLApplication</span></span> |
4. <span data-ttu-id="7f9e2-136">按一下**確定**toocreate hello 專案。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-136">Click **OK** toocreate hello project.</span></span>
5. <span data-ttu-id="7f9e2-137">加入 hello Nuget 封裝 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-137">Add hello Nuget packages tooyour project.</span></span>

   1. <span data-ttu-id="7f9e2-138">Hello hello 方案總管 中的專案名稱上按一下滑鼠右鍵，然後按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-138">Right-click hello project name in hello Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="7f9e2-139">在 hello **Nuget 套件管理員**索引標籤上，請確定**套件來源**設定得**nuget.org**而且**包含發行前版本**核取方塊已選取。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-139">In hello **Nuget Package Manager** tab, make sure that **Package source** is set too**nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="7f9e2-140">搜尋並安裝下列 NuGet 套件 hello:</span><span class="sxs-lookup"><span data-stu-id="7f9e2-140">Search for and install hello following NuGet packages:</span></span>

      * <span data-ttu-id="7f9e2-141">`Microsoft.Azure.Management.DataLake.Store` - 本教學課程使用 v2.1.3-preview。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-141">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span></span>
      * <span data-ttu-id="7f9e2-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - 本教學課程使用 v2.2.12。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span></span>

        <span data-ttu-id="7f9e2-143">![新增 Nuget 來源](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "建立新的 Azure Data Lake 帳戶")</span><span class="sxs-lookup"><span data-stu-id="7f9e2-143">![Add a Nuget source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="7f9e2-144">關閉 hello **Nuget 套件管理員**。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-144">Close hello **Nuget Package Manager**.</span></span>
6. <span data-ttu-id="7f9e2-145">開啟**Program.cs**刪除 hello 現有程式碼，然後加入下列陳述式 tooadd 參考 toonamespaces hello。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-145">Open **Program.cs**, delete hello existing code, and then include hello following statements tooadd references toonamespaces.</span></span>

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. <span data-ttu-id="7f9e2-146">宣告 hello 變數，如下所示，並提供 hello 值的資料湖存放區名稱和 hello 資源群組名稱已存在。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-146">Declare hello variables as shown below, and provide hello values for Data Lake Store name and hello resource group name that already exist.</span></span> <span data-ttu-id="7f9e2-147">此外，請確定 hello 本機路徑和檔案名稱您在此處提供必須存在於 hello 電腦。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-147">Also, make sure hello local path and file name you provide here must exist on hello computer.</span></span> <span data-ttu-id="7f9e2-148">新增下列程式碼片段在 hello 命名空間宣告之後的 hello。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-148">Add hello following code snippet after hello namespace declarations.</span></span>

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

<span data-ttu-id="7f9e2-149">在 hello 剩餘 hello 發行項的區段，您可以看到 toouse hello 可用.NET 方法 tooperform 作業，例如驗證、 檔案上傳等等的方式。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-149">In hello remaining sections of hello article, you can see how toouse hello available .NET methods tooperform operations such as authentication, file upload, etc.</span></span>

## <a name="authentication"></a><span data-ttu-id="7f9e2-150">驗證</span><span class="sxs-lookup"><span data-stu-id="7f9e2-150">Authentication</span></span>

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a><span data-ttu-id="7f9e2-151">如果您要使用使用者驗證 (本教學課程建議的驗證方式)</span><span class="sxs-lookup"><span data-stu-id="7f9e2-151">If you are using end-user authentication (recommended for this tutorial)</span></span>

<span data-ttu-id="7f9e2-152">搭配使用現有的 Azure AD 原生應用程式 tooauthenticate 您的應用程式**以互動方式**，這表示您會收到提示 tooenter 您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-152">Use this with an existing Azure AD native application tooauthenticate your application **interactively**, which means you will be prompted tooenter your Azure credentials.</span></span>

<span data-ttu-id="7f9e2-153">為了方便使用，hello 以下程式碼片段會使用預設值，用戶端識別碼和重新導向 URI，將會使用任何 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-153">For ease of use, hello snippet below uses default values for client ID and redirect URI that will work with any Azure subscription.</span></span> <span data-ttu-id="7f9e2-154">toohelp 更快完成本教學課程中，我們建議使用此方法。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-154">toohelp you complete this tutorial faster, we recommend you use this approach.</span></span> <span data-ttu-id="7f9e2-155">在 hello 以下程式碼片段，只要提供 hello 值您的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-155">In hello snippet below, just provide hello value for your tenant ID.</span></span> <span data-ttu-id="7f9e2-156">您可以擷取使用所提供的 hello 指示[建立 Active Directory 應用程式](data-lake-store-end-user-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-156">You can retrieve it using hello instructions provided at [Create an Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

<span data-ttu-id="7f9e2-157">幾個事項 tooknow 有關上述這個程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="7f9e2-157">A couple of things tooknow about this snippet above:</span></span>

* <span data-ttu-id="7f9e2-158">toohelp 更快完成 hello 教學課程中，此程式碼片段使用的 Azure AD 網域和用戶端根據預設，所有的 Azure 訂用帳戶的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-158">toohelp you complete hello tutorial faster, this snippet uses an an Azure AD domain and client ID that is available by default for all Azure subscriptions.</span></span> <span data-ttu-id="7f9e2-159">因此，您可以**在應用程式中原封不動地使用此程式碼片段**。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-159">So, you can **use this snippet as-is in your application**.</span></span>
* <span data-ttu-id="7f9e2-160">不過，如果您想 toouse 您自己的 Azure AD 網域與應用程式用戶端識別碼，您必須建立 Azure AD 的原生應用程式，然後使用 hello Azure AD 租用戶識別碼、 用戶端識別碼和重新導向 URI hello 應用程式建立。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-160">However, if you do want toouse your own Azure AD domain and application client ID, you must create an Azure AD native application and then use hello Azure AD tenant ID, client ID, and redirect URI for hello application you created.</span></span> <span data-ttu-id="7f9e2-161">如需相關指示，請參閱[建立 Active Directory 應用程式以使用 Data Lake Store 進行使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-161">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span></span>

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a><span data-ttu-id="7f9e2-162">如果您要使用服務對服務驗證與用戶端密碼</span><span class="sxs-lookup"><span data-stu-id="7f9e2-162">If you are using service-to-service authentication with client secret</span></span>
<span data-ttu-id="7f9e2-163">下列程式碼片段 hello 可以是您的應用程式使用的 tooauthenticate**非互動方式**、 使用 hello 用戶端密碼 / 金鑰的應用程式 / 服務主體。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-163">hello following snippet can be used tooauthenticate your application **non-interactively**, using hello client secret / key for an application / service principal.</span></span> <span data-ttu-id="7f9e2-164">請將此方法用於現有的 Azure AD「Web 應用程式」應用程式。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-164">Use this with an existing Azure AD "Web App" Application.</span></span> <span data-ttu-id="7f9e2-165">如需有關如何 toocreate hello Azure AD web 應用程式，以及如何 tooretrieve hello 用戶端識別碼和用戶端密碼需要在 hello 以下程式碼片段，請參閱指示[使用資料建立服務對服務驗證 Active Directory 應用程式Lake Store](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-165">For instructions on how toocreate hello Azure AD web application and how tooretrieve hello client ID and client secret required in hello snippet below, see [Create an Active Directory Application for service-to-service authentication with Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span></span>

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a><span data-ttu-id="7f9e2-166">如果您要使用服務對服務驗證與憑證</span><span class="sxs-lookup"><span data-stu-id="7f9e2-166">If you are using service-to-service authentication with certificate</span></span>

<span data-ttu-id="7f9e2-167">第三個選項，hello 如下列程式碼片段可以是使用的 tooauthenticate 您的應用程式**非互動方式**、 hello 憑證使用 Azure Active Directory 應用程式 / 服務主體。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-167">As a third option, hello following snippet can be used tooauthenticate your application **non-interactively**, using hello certificate for an Azure Active Directory application / service principal.</span></span> <span data-ttu-id="7f9e2-168">請將此方法用於現有的 [Azure AD 與憑證](../azure-resource-manager/resource-group-authenticate-service-principal.md)。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-168">Use this with an existing [Azure AD Application with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a><span data-ttu-id="7f9e2-169">建立用戶端物件</span><span class="sxs-lookup"><span data-stu-id="7f9e2-169">Create client objects</span></span>
<span data-ttu-id="7f9e2-170">hello 下列程式碼片段會建立 hello Data Lake Store 帳戶和檔案系統所使用的用戶端物件 tooissue toohello 服務要求。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-170">hello following snippet creates hello Data Lake Store account and filesystem client objects, which are used tooissue requests toohello service.</span></span>

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a><span data-ttu-id="7f9e2-171">列出訂用帳戶內的所有 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="7f9e2-171">List all Data Lake Store accounts within a subscription</span></span>
<span data-ttu-id="7f9e2-172">hello 下列程式碼片段列出給定 Azure 訂用帳戶內的所有 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-172">hello following snippet lists all Data Lake Store accounts within a given Azure subscription.</span></span>

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

## <a name="create-a-directory"></a><span data-ttu-id="7f9e2-173">建立目錄</span><span class="sxs-lookup"><span data-stu-id="7f9e2-173">Create a directory</span></span>
<span data-ttu-id="7f9e2-174">下列程式碼片段說明 hello`CreateDirectory`方法，您可以使用 toocreate Data Lake Store 帳戶內的目錄。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-174">hello following snippet shows a `CreateDirectory` method that you can use toocreate a directory within a Data Lake Store account.</span></span>

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a><span data-ttu-id="7f9e2-175">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="7f9e2-175">Upload a file</span></span>
<span data-ttu-id="7f9e2-176">下列程式碼片段說明 hello`UploadFile`方法，您可以使用 tooupload 檔案 tooa Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-176">hello following snippet shows an `UploadFile` method that you can use tooupload files tooa Data Lake Store account.</span></span>

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

<span data-ttu-id="7f9e2-177">hello SDK 支援遞迴上傳和下載之間的本機檔案路徑和 Data Lake Store 檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-177">hello SDK supports recursive upload and download between a local file path and a Data Lake Store file path.</span></span>    

## <a name="get-file-or-directory-info"></a><span data-ttu-id="7f9e2-178">取得檔案或目錄資訊</span><span class="sxs-lookup"><span data-stu-id="7f9e2-178">Get file or directory info</span></span>
<span data-ttu-id="7f9e2-179">下列程式碼片段說明 hello`GetItemInfo`方法可讓您 tooretrieve 資訊的檔案或目錄的可用資料湖存放區中。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-179">hello following snippet shows a `GetItemInfo` method that you can use tooretrieve information about a file or directory available in Data Lake Store.</span></span>

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a><span data-ttu-id="7f9e2-180">列出檔案或目錄</span><span class="sxs-lookup"><span data-stu-id="7f9e2-180">List file or directories</span></span>
<span data-ttu-id="7f9e2-181">下列程式碼片段說明 hello `ListItem` toolist hello 檔案和目錄中可用的 Data Lake Store 帳戶的方法。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-181">hello following snippet shows a `ListItem` method that can use toolist hello file and directories in a Data Lake Store account.</span></span>

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a><span data-ttu-id="7f9e2-182">串連檔案</span><span class="sxs-lookup"><span data-stu-id="7f9e2-182">Concatenate files</span></span>
<span data-ttu-id="7f9e2-183">下列程式碼片段說明 hello`ConcatenateFiles`您使用 tooconcatenate 檔案的方法。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-183">hello following snippet shows a `ConcatenateFiles` method that you use tooconcatenate files.</span></span>

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a><span data-ttu-id="7f9e2-184">附加 tooa 檔</span><span class="sxs-lookup"><span data-stu-id="7f9e2-184">Append tooa file</span></span>
<span data-ttu-id="7f9e2-185">下列程式碼片段說明 hello`AppendToFile`附加資料 tooa 檔已儲存在 Data Lake Store 帳戶，您使用的方法。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-185">hello following snippet shows a `AppendToFile` method that you use append data tooa file already stored in a Data Lake Store account.</span></span>

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a><span data-ttu-id="7f9e2-186">下載檔案</span><span class="sxs-lookup"><span data-stu-id="7f9e2-186">Download a file</span></span>
<span data-ttu-id="7f9e2-187">下列程式碼片段說明 hello`DownloadFile`方法，您會使用 toodownload 來自 Data Lake Store 帳戶的檔案。</span><span class="sxs-lookup"><span data-stu-id="7f9e2-187">hello following snippet shows a `DownloadFile` method that you use toodownload a file from a Data Lake Store account.</span></span>

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a><span data-ttu-id="7f9e2-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7f9e2-188">Next steps</span></span>
* [<span data-ttu-id="7f9e2-189">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="7f9e2-189">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="7f9e2-190">搭配 Data Lake Store 使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="7f9e2-190">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="7f9e2-191">搭配 Data Lake Store 使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f9e2-191">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="7f9e2-192">Data Lake Store .NET SDK 參考</span><span class="sxs-lookup"><span data-stu-id="7f9e2-192">Data Lake Store .NET SDK Reference</span></span>](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [<span data-ttu-id="7f9e2-193">Data Lake Store REST 參考</span><span class="sxs-lookup"><span data-stu-id="7f9e2-193">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
