---
title: "在 Azure Data Lake Store 中使用 .NET SDK 開發應用程式 | Microsoft Docs"
description: "使用 Azure Data Lake Store .NET SDK 建立 Data Lake Store 帳戶，並在 Data Lake Store 中執行基本作業"
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
ms.openlocfilehash: 70f94a07b0102e3135eaf85e5877e3502762d7e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a><span data-ttu-id="6fb27-103">使用 .NET SDK 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="6fb27-103">Get started with Azure Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6fb27-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="6fb27-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="6fb27-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6fb27-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="6fb27-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="6fb27-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="6fb27-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="6fb27-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="6fb27-108">REST API</span><span class="sxs-lookup"><span data-stu-id="6fb27-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="6fb27-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6fb27-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="6fb27-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="6fb27-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="6fb27-111">Python</span><span class="sxs-lookup"><span data-stu-id="6fb27-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="6fb27-112">了解如何使用 [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) 來執行基本作業，例如建立資料夾、上傳和下載資料檔案等等。如需有關 Data Lake 的詳細資訊，請參閱 [Azure Data Lake Store](data-lake-store-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6fb27-112">Learn how to use the [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fb27-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="6fb27-113">Prerequisites</span></span>
* <span data-ttu-id="6fb27-114">**Visual Studio 2013、2015 或 2017**。</span><span class="sxs-lookup"><span data-stu-id="6fb27-114">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="6fb27-115">以下指示使用 Visual Studio 2015 Update 2。</span><span class="sxs-lookup"><span data-stu-id="6fb27-115">The instructions below use Visual Studio 2015 Update 2.</span></span>

* <span data-ttu-id="6fb27-116">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="6fb27-116">**An Azure subscription**.</span></span> <span data-ttu-id="6fb27-117">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="6fb27-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="6fb27-118">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="6fb27-118">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="6fb27-119">如需有關如何建立帳戶的指示，請參閱 [開始使用 Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6fb27-119">For instructions on how to create an account, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

* <span data-ttu-id="6fb27-120">**建立 Azure Active Directory 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6fb27-120">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="6fb27-121">您必須使用 Azure AD 應用程式來向 Azure AD 驗證 Data Lake Store 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6fb27-121">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="6fb27-122">有不同的方法可向 Azure AD 進行驗證：**使用者驗證**或**服務對服務驗證**。</span><span class="sxs-lookup"><span data-stu-id="6fb27-122">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="6fb27-123">如需有關如何驗證的指示和詳細資訊，請參閱[使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)或[服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="6fb27-123">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="6fb27-124">建立 .NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="6fb27-124">Create a .NET application</span></span>
1. <span data-ttu-id="6fb27-125">開啟 Visual Studio，建立主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6fb27-125">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="6fb27-126">從 [檔案] 功能表中，按一下 [新增]，再按 [專案]。</span><span class="sxs-lookup"><span data-stu-id="6fb27-126">From the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="6fb27-127">在 [ **新增專案**] 中，輸入或選取下列值：</span><span class="sxs-lookup"><span data-stu-id="6fb27-127">From **New Project**, type or select the following values:</span></span>

   | <span data-ttu-id="6fb27-128">屬性</span><span class="sxs-lookup"><span data-stu-id="6fb27-128">Property</span></span> | <span data-ttu-id="6fb27-129">值</span><span class="sxs-lookup"><span data-stu-id="6fb27-129">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="6fb27-130">類別</span><span class="sxs-lookup"><span data-stu-id="6fb27-130">Category</span></span> |<span data-ttu-id="6fb27-131">範本/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="6fb27-131">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="6fb27-132">範本</span><span class="sxs-lookup"><span data-stu-id="6fb27-132">Template</span></span> |<span data-ttu-id="6fb27-133">主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="6fb27-133">Console Application</span></span> |
   | <span data-ttu-id="6fb27-134">名稱</span><span class="sxs-lookup"><span data-stu-id="6fb27-134">Name</span></span> |<span data-ttu-id="6fb27-135">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="6fb27-135">CreateADLApplication</span></span> |
4. <span data-ttu-id="6fb27-136">按一下 [確定]  以建立專案。</span><span class="sxs-lookup"><span data-stu-id="6fb27-136">Click **OK** to create the project.</span></span>
5. <span data-ttu-id="6fb27-137">將 Nuget 封裝新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="6fb27-137">Add the Nuget packages to your project.</span></span>

   1. <span data-ttu-id="6fb27-138">在方案總管中以滑鼠右鍵按一下專案名稱，然後按一下 [ **管理 NuGet 封裝**]。</span><span class="sxs-lookup"><span data-stu-id="6fb27-138">Right-click the project name in the Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="6fb27-139">在 [Nuget 封裝管理員] 索引標籤中，確定 [封裝來源] 設為 [nuget.org]，且已選取 [包含發行前版本] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="6fb27-139">In the **Nuget Package Manager** tab, make sure that **Package source** is set to **nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="6fb27-140">搜尋並安裝下列 NuGet 封裝：</span><span class="sxs-lookup"><span data-stu-id="6fb27-140">Search for and install the following NuGet packages:</span></span>

      * <span data-ttu-id="6fb27-141">`Microsoft.Azure.Management.DataLake.Store` - 本教學課程使用 v2.1.3-preview。</span><span class="sxs-lookup"><span data-stu-id="6fb27-141">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span></span>
      * <span data-ttu-id="6fb27-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - 本教學課程使用 v2.2.12。</span><span class="sxs-lookup"><span data-stu-id="6fb27-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span></span>

        <span data-ttu-id="6fb27-143">![新增 Nuget 來源](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "建立新的 Azure Data Lake 帳戶")</span><span class="sxs-lookup"><span data-stu-id="6fb27-143">![Add a Nuget source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="6fb27-144">關閉 [ **Nuget 封裝管理員**]。</span><span class="sxs-lookup"><span data-stu-id="6fb27-144">Close the **Nuget Package Manager**.</span></span>
6. <span data-ttu-id="6fb27-145">開啟 **Program.cs**，刪除現有的程式碼，然後納入下列陳述式以新增命名空間的參考。</span><span class="sxs-lookup"><span data-stu-id="6fb27-145">Open **Program.cs**, delete the existing code, and then include the following statements to add references to namespaces.</span></span>

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. <span data-ttu-id="6fb27-146">宣告如下所示的變數，並提供已存在的 Data Lake Store 名稱和資源群組名稱的值。</span><span class="sxs-lookup"><span data-stu-id="6fb27-146">Declare the variables as shown below, and provide the values for Data Lake Store name and the resource group name that already exist.</span></span> <span data-ttu-id="6fb27-147">此外，請確定您在此處提供的本機路徑和檔案名稱必須存在於電腦。</span><span class="sxs-lookup"><span data-stu-id="6fb27-147">Also, make sure the local path and file name you provide here must exist on the computer.</span></span> <span data-ttu-id="6fb27-148">將下列程式碼片段加在命名空間宣告之後。</span><span class="sxs-lookup"><span data-stu-id="6fb27-148">Add the following code snippet after the namespace declarations.</span></span>

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
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with the name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with the name of the resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

<span data-ttu-id="6fb27-149">在本文的其餘章節中，您可以了解如何使用可用的 .NET 方法來執行一些作業，例如驗證、檔案上載等。</span><span class="sxs-lookup"><span data-stu-id="6fb27-149">In the remaining sections of the article, you can see how to use the available .NET methods to perform operations such as authentication, file upload, etc.</span></span>

## <a name="authentication"></a><span data-ttu-id="6fb27-150">驗證</span><span class="sxs-lookup"><span data-stu-id="6fb27-150">Authentication</span></span>

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a><span data-ttu-id="6fb27-151">如果您要使用使用者驗證 (本教學課程建議的驗證方式)</span><span class="sxs-lookup"><span data-stu-id="6fb27-151">If you are using end-user authentication (recommended for this tutorial)</span></span>

<span data-ttu-id="6fb27-152">使用這個項目與現有的 Azure AD 原生應用程式，**以互動方式**驗證您的應用程式，這表示系統會提示您輸入您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="6fb27-152">Use this with an existing Azure AD native application to authenticate your application **interactively**, which means you will be prompted to enter your Azure credentials.</span></span>

<span data-ttu-id="6fb27-153">為了方便使用，下列程式碼片段會針對用戶端識別碼和重新導向 URI 使用預設值，這些項目會與任何 Azure 訂用帳戶搭配使用。</span><span class="sxs-lookup"><span data-stu-id="6fb27-153">For ease of use, the snippet below uses default values for client ID and redirect URI that will work with any Azure subscription.</span></span> <span data-ttu-id="6fb27-154">為了協助您更快完成本教學課程，建議您使用此方法。</span><span class="sxs-lookup"><span data-stu-id="6fb27-154">To help you complete this tutorial faster, we recommend you use this approach.</span></span> <span data-ttu-id="6fb27-155">在下列程式碼片段中，只須提供您的租用戶識別碼值。</span><span class="sxs-lookup"><span data-stu-id="6fb27-155">In the snippet below, just provide the value for your tenant ID.</span></span> <span data-ttu-id="6fb27-156">您可以使用[建立 Active Directory 應用程式](data-lake-store-end-user-authenticate-using-active-directory.md)提供的指示來擷取它。</span><span class="sxs-lookup"><span data-stu-id="6fb27-156">You can retrieve it using the instructions provided at [Create an Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

    // User login via interactive popup
    // Use the client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with the user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

<span data-ttu-id="6fb27-157">上面這個程式碼片段有幾項須知：</span><span class="sxs-lookup"><span data-stu-id="6fb27-157">A couple of things to know about this snippet above:</span></span>

* <span data-ttu-id="6fb27-158">為了協助您更快完成本教學課程，此程式碼片段使用所有 Azure 訂用帳戶預設可用的 Azure AD 網域和用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="6fb27-158">To help you complete the tutorial faster, this snippet uses an an Azure AD domain and client ID that is available by default for all Azure subscriptions.</span></span> <span data-ttu-id="6fb27-159">因此，您可以**在應用程式中原封不動地使用此程式碼片段**。</span><span class="sxs-lookup"><span data-stu-id="6fb27-159">So, you can **use this snippet as-is in your application**.</span></span>
* <span data-ttu-id="6fb27-160">但是，如果您想要使用自己的 Azure AD 網域和應用程式用戶端識別碼，您必須建立 Azure AD 原生應用程式，然後使用您所建立之應用程式的 Azure AD 租用戶識別碼、用戶端識別碼和重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="6fb27-160">However, if you do want to use your own Azure AD domain and application client ID, you must create an Azure AD native application and then use the Azure AD tenant ID, client ID, and redirect URI for the application you created.</span></span> <span data-ttu-id="6fb27-161">如需相關指示，請參閱[建立 Active Directory 應用程式以使用 Data Lake Store 進行使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="6fb27-161">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span></span>

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a><span data-ttu-id="6fb27-162">如果您要使用服務對服務驗證與用戶端密碼</span><span class="sxs-lookup"><span data-stu-id="6fb27-162">If you are using service-to-service authentication with client secret</span></span>
<span data-ttu-id="6fb27-163">下列程式碼片段可供使用應用程式/服務主體的用戶端密碼/金鑰，**以非互動方式**驗證您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6fb27-163">The following snippet can be used to authenticate your application **non-interactively**, using the client secret / key for an application / service principal.</span></span> <span data-ttu-id="6fb27-164">請將此方法用於現有的 Azure AD「Web 應用程式」應用程式。</span><span class="sxs-lookup"><span data-stu-id="6fb27-164">Use this with an existing Azure AD "Web App" Application.</span></span> <span data-ttu-id="6fb27-165">如需有關如何建立 Azure AD Web 應用程式以及如何擷取以下程式碼片段必要用戶端識別碼和用戶端密碼的指示，請參閱[使用 Data Lake Store 建立 Active Directory 應用程式以進行服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="6fb27-165">For instructions on how to create the Azure AD web application and how to retrieve the client ID and client secret required in the snippet below, see [Create an Active Directory Application for service-to-service authentication with Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span></span>

    // Service principal / appplication authentication with client secret / key
    // Use the client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a><span data-ttu-id="6fb27-166">如果您要使用服務對服務驗證與憑證</span><span class="sxs-lookup"><span data-stu-id="6fb27-166">If you are using service-to-service authentication with certificate</span></span>

<span data-ttu-id="6fb27-167">第三個選項，下列程式碼片段可供使用 Azure Active Directory 應用程式/服務主體的憑證，**以非互動方式**驗證您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6fb27-167">As a third option, the following snippet can be used to authenticate your application **non-interactively**, using the certificate for an Azure Active Directory application / service principal.</span></span> <span data-ttu-id="6fb27-168">請將此方法用於現有的 [Azure AD 與憑證](../azure-resource-manager/resource-group-authenticate-service-principal.md)。</span><span class="sxs-lookup"><span data-stu-id="6fb27-168">Use this with an existing [Azure AD Application with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    // Service principal / application authentication with certificate
    // Use the client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a><span data-ttu-id="6fb27-169">建立用戶端物件</span><span class="sxs-lookup"><span data-stu-id="6fb27-169">Create client objects</span></span>
<span data-ttu-id="6fb27-170">下列程式碼片段會建立 Data Lake Store 帳戶和檔案系統用戶端物件，以便對服務發出要求。</span><span class="sxs-lookup"><span data-stu-id="6fb27-170">The following snippet creates the Data Lake Store account and filesystem client objects, which are used to issue requests to the service.</span></span>

    // Create client objects and set the subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a><span data-ttu-id="6fb27-171">列出訂用帳戶內的所有 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="6fb27-171">List all Data Lake Store accounts within a subscription</span></span>
<span data-ttu-id="6fb27-172">下列程式碼片段列出指定的 Azure 訂用帳戶中的所有 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6fb27-172">The following snippet lists all Data Lake Store accounts within a given Azure subscription.</span></span>

    // List all ADLS accounts within the subscription
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

## <a name="create-a-directory"></a><span data-ttu-id="6fb27-173">建立目錄</span><span class="sxs-lookup"><span data-stu-id="6fb27-173">Create a directory</span></span>
<span data-ttu-id="6fb27-174">下列程式碼片段顯示的 `CreateDirectory` 方法可用於在 Data Lake Store 帳戶中建立目錄。</span><span class="sxs-lookup"><span data-stu-id="6fb27-174">The following snippet shows a `CreateDirectory` method that you can use to create a directory within a Data Lake Store account.</span></span>

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a><span data-ttu-id="6fb27-175">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="6fb27-175">Upload a file</span></span>
<span data-ttu-id="6fb27-176">下列程式碼片段顯示的 `UploadFile` 方法可用於將檔案上傳到 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6fb27-176">The following snippet shows an `UploadFile` method that you can use to upload files to a Data Lake Store account.</span></span>

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

<span data-ttu-id="6fb27-177">SDK 支援在本機檔案路徑與 Data Lake Store 檔案路徑之間進行遞迴上傳和下載。</span><span class="sxs-lookup"><span data-stu-id="6fb27-177">The SDK supports recursive upload and download between a local file path and a Data Lake Store file path.</span></span>    

## <a name="get-file-or-directory-info"></a><span data-ttu-id="6fb27-178">取得檔案或目錄資訊</span><span class="sxs-lookup"><span data-stu-id="6fb27-178">Get file or directory info</span></span>
<span data-ttu-id="6fb27-179">下列程式碼片段顯示的 `GetItemInfo` 方法可用於擷取 Data Lake Store 中可用檔案或目錄的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6fb27-179">The following snippet shows a `GetItemInfo` method that you can use to retrieve information about a file or directory available in Data Lake Store.</span></span>

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a><span data-ttu-id="6fb27-180">列出檔案或目錄</span><span class="sxs-lookup"><span data-stu-id="6fb27-180">List file or directories</span></span>
<span data-ttu-id="6fb27-181">下列程式碼片段顯示的 `ListItem` 方法可用於列出 Data Lake Store 帳戶中的檔案和目錄。</span><span class="sxs-lookup"><span data-stu-id="6fb27-181">The following snippet shows a `ListItem` method that can use to list the file and directories in a Data Lake Store account.</span></span>

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a><span data-ttu-id="6fb27-182">串連檔案</span><span class="sxs-lookup"><span data-stu-id="6fb27-182">Concatenate files</span></span>
<span data-ttu-id="6fb27-183">下列程式碼片段顯示的 `ConcatenateFiles` 方法可用於串連檔案。</span><span class="sxs-lookup"><span data-stu-id="6fb27-183">The following snippet shows a `ConcatenateFiles` method that you use to concatenate files.</span></span>

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-to-a-file"></a><span data-ttu-id="6fb27-184">附加到檔案</span><span class="sxs-lookup"><span data-stu-id="6fb27-184">Append to a file</span></span>
<span data-ttu-id="6fb27-185">下列程式碼片段顯示的 `AppendToFile` 方法可用於將資料附加到 Data Lake Store 帳戶中已儲存的檔案。</span><span class="sxs-lookup"><span data-stu-id="6fb27-185">The following snippet shows a `AppendToFile` method that you use append data to a file already stored in a Data Lake Store account.</span></span>

    // Append to file
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a><span data-ttu-id="6fb27-186">下載檔案</span><span class="sxs-lookup"><span data-stu-id="6fb27-186">Download a file</span></span>
<span data-ttu-id="6fb27-187">下列程式碼片段顯示的 `DownloadFile` 方法可用於從 Data Lake Store 帳戶下載檔案。</span><span class="sxs-lookup"><span data-stu-id="6fb27-187">The following snippet shows a `DownloadFile` method that you use to download a file from a Data Lake Store account.</span></span>

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a><span data-ttu-id="6fb27-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6fb27-188">Next steps</span></span>
* [<span data-ttu-id="6fb27-189">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="6fb27-189">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="6fb27-190">搭配 Data Lake Store 使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6fb27-190">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="6fb27-191">搭配 Data Lake Store 使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6fb27-191">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="6fb27-192">Data Lake Store .NET SDK 參考</span><span class="sxs-lookup"><span data-stu-id="6fb27-192">Data Lake Store .NET SDK Reference</span></span>](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [<span data-ttu-id="6fb27-193">Data Lake Store REST 參考</span><span class="sxs-lookup"><span data-stu-id="6fb27-193">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
