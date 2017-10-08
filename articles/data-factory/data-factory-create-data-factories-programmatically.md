---
title: "使用 Azure.NET SDK aaaCreate 資料管線 |Microsoft 文件"
description: "了解 tooprogrammatically 如何建立、 監視和管理 Azure data factory 使用 Data Factory SDK。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="68615-103">使用 Azure Data Factory .NET SDK 來建立、監視及管理 Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="68615-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="68615-104">概觀</span><span class="sxs-lookup"><span data-stu-id="68615-104">Overview</span></span>
<span data-ttu-id="68615-105">您可以使用 Data Factory .NET SDK，以程式設計方式建立、監視及管理 Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="68615-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="68615-106">本文將逐步解說中，您可以遵循 toocreate 範例.NET 主控台應用程式建立及監視 data factory。</span><span class="sxs-lookup"><span data-stu-id="68615-106">This article contains a walkthrough that you can follow toocreate a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="68615-107">本文並未涵蓋所有 hello Data Factory.NET API。</span><span class="sxs-lookup"><span data-stu-id="68615-107">This article does not cover all hello Data Factory .NET API.</span></span> <span data-ttu-id="68615-108">如需適用於 Data Factory 之 .NET API 的完整文件，請參閱 [Data Factory .NET API 參考](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1)。</span><span class="sxs-lookup"><span data-stu-id="68615-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="68615-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="68615-109">Prerequisites</span></span>
* <span data-ttu-id="68615-110">Visual Studio 2012、2013 或 2015</span><span class="sxs-lookup"><span data-stu-id="68615-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="68615-111">下載並安裝 [Azure .NET SDK](http://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="68615-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="68615-112">Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="68615-112">Azure PowerShell.</span></span> <span data-ttu-id="68615-113">遵循指示[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)文章 tooinstall Azure PowerShell，在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="68615-113">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="68615-114">您使用 Azure PowerShell toocreate Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="68615-114">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="68615-115">在 Azure Active Directory 中建立應用程式</span><span class="sxs-lookup"><span data-stu-id="68615-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="68615-116">建立 Azure Active Directory 應用程式、 建立服務主體針對 hello 應用程式，並將它指派 toohello**資料 Factory 參與者**角色。</span><span class="sxs-lookup"><span data-stu-id="68615-116">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="68615-117">啟動 **PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="68615-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="68615-118">執行下列命令的 hello 並輸入 hello 使用者名稱和密碼，您會使用 toosign toohello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="68615-118">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="68615-119">執行下列命令 tooview hello 這個帳戶的所有 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="68615-119">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="68615-120">執行下列命令 tooselect hello 訂用帳戶，您想要使用 toowork hello。</span><span class="sxs-lookup"><span data-stu-id="68615-120">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="68615-121">取代 **&lt;NameOfAzureSubscription** &gt; hello 的 Azure 訂用帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="68615-121">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="68615-122">記下**SubscriptionId**和**TenantId**從 hello 這個命令的輸出。</span><span class="sxs-lookup"><span data-stu-id="68615-122">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="68615-123">建立 Azure 資源群組名稱為**ADFTutorialResourceGroup**藉由執行下列命令在 hello PowerShell 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="68615-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="68615-124">如果已經存在 hello 資源群組，指定是否 tooupdate 它 (Y) 或保留為 (N)。</span><span class="sxs-lookup"><span data-stu-id="68615-124">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="68615-125">如果您使用不同的資源群組，您會在本教學課程需要資源群組來取代 ADFTutorialResourceGroup toouse hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="68615-125">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="68615-126">建立 Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="68615-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="68615-127">如果您收到下列錯誤 hello，請指定不同的 URL，然後再次執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="68615-127">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="68615-128">建立 hello AD 服務主體。</span><span class="sxs-lookup"><span data-stu-id="68615-128">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="68615-129">新增服務主體 toohello**資料 Factory 參與者**角色。</span><span class="sxs-lookup"><span data-stu-id="68615-129">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="68615-130">取得 hello 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="68615-130">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="68615-131">記下 hello 輸出中的 hello 應用程式識別碼 (applicationID)。</span><span class="sxs-lookup"><span data-stu-id="68615-131">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="68615-132">您應會從這些步驟取得下列四個值︰</span><span class="sxs-lookup"><span data-stu-id="68615-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="68615-133">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="68615-133">Tenant ID</span></span>
* <span data-ttu-id="68615-134">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="68615-134">Subscription ID</span></span>
* <span data-ttu-id="68615-135">應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="68615-135">Application ID</span></span>
* <span data-ttu-id="68615-136">（在 hello 第一個命令中指定） 的密碼</span><span class="sxs-lookup"><span data-stu-id="68615-136">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="68615-137">逐步介紹</span><span class="sxs-lookup"><span data-stu-id="68615-137">Walkthrough</span></span>
<span data-ttu-id="68615-138">Hello 逐步解說中，您可以建立 data factory 管線，包含複製活動。</span><span class="sxs-lookup"><span data-stu-id="68615-138">In hello walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="68615-139">hello 複製活動會將資料複製相同的 hello 您 Azure blob 儲存體 tooanother 資料夾中的資料夾從 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="68615-139">hello copy activity copies data from a folder in your Azure blob storage tooanother folder in hello same blob storage.</span></span> 

<span data-ttu-id="68615-140">hello 複製活動會在 Azure Data Factory 中執行 hello 資料移動。</span><span class="sxs-lookup"><span data-stu-id="68615-140">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="68615-141">hello 活動被提供安全、 可靠且可擴充的方式的各種資料存放區之間的資料可以複製的全域可用服務。</span><span class="sxs-lookup"><span data-stu-id="68615-141">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="68615-142">請參閱[資料移動活動](data-factory-data-movement-activities.md)hello 複製活動的詳細資料的發行項。</span><span class="sxs-lookup"><span data-stu-id="68615-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

1. <span data-ttu-id="68615-143">使用 Visual Studio 2012/2013/2015 建立 C# .NET 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="68615-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="68615-144">啟動 **Visual Studio** 2012/2013/2015。</span><span class="sxs-lookup"><span data-stu-id="68615-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="68615-145">按一下**檔案**，點太**新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="68615-145">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="68615-146">展開 [範本]，然後選取 [Visual C#]。</span><span class="sxs-lookup"><span data-stu-id="68615-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="68615-147">在此逐步解說中，您使用的是 C#，但您可以使用任何 .NET 語言。</span><span class="sxs-lookup"><span data-stu-id="68615-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="68615-148">選取**主控台應用程式**從 hello hello 右上的專案類型清單。</span><span class="sxs-lookup"><span data-stu-id="68615-148">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="68615-149">輸入**DataFactoryAPITestApp** hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="68615-149">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="68615-150">選取**C:\ADFGetStarted** hello 位置。</span><span class="sxs-lookup"><span data-stu-id="68615-150">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="68615-151">按一下**確定**toocreate hello 專案。</span><span class="sxs-lookup"><span data-stu-id="68615-151">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="68615-152">按一下**工具**，點太**NuGet 套件管理員**，然後按一下**Package Manager Console**。</span><span class="sxs-lookup"><span data-stu-id="68615-152">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="68615-153">在 hello **Package Manager Console**，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="68615-153">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="68615-154">執行下列命令 tooinstall Data Factory 套件 hello:`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="68615-154">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="68615-155">執行下列命令 tooinstall Azure Active Directory 封裝 （使用 Active Directory API hello 程式碼中） 的 hello:`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="68615-155">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="68615-156">取代 hello 內容**App.config** hello 以 hello 內容之後的專案中的檔案：</span><span class="sxs-lookup"><span data-stu-id="68615-156">Replace hello contents of **App.config** file in hello project with hello following content:</span></span> 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. <span data-ttu-id="68615-157">在 hello App.Config 檔案中，更新值**&lt;應用程式識別碼&gt;**， **&lt;密碼&gt;**，  **&lt;訂用帳戶 ID&gt;**，和**&lt;租用戶識別碼&gt;**以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="68615-157">In hello App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="68615-158">新增下列 hello**使用**陳述式 toohello **Program.cs** hello 專案中的檔案。</span><span class="sxs-lookup"><span data-stu-id="68615-158">Add hello following **using** statements toohello **Program.cs** file in hello project.</span></span>

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```
6. <span data-ttu-id="68615-159">新增下列程式碼會建立的執行個體的 hello **DataPipelineManagementClient**類別 toohello **Main**方法。</span><span class="sxs-lookup"><span data-stu-id="68615-159">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="68615-160">您可以使用這個物件 toocreate data factory、 連結的服務、 輸入和輸出資料集和管線。</span><span class="sxs-lookup"><span data-stu-id="68615-160">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="68615-161">您也可以使用這個物件 toomonitor 配量的資料集在執行階段。</span><span class="sxs-lookup"><span data-stu-id="68615-161">You also use this object toomonitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="68615-162">取代 hello 值**resourceGroupName** hello Azure 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="68615-162">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span> <span data-ttu-id="68615-163">您可以建立資源群組使用 hello[新增 AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="68615-163">You can create a resource group using hello [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="68615-164">更新的 hello 資料 factory () toobe 唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="68615-164">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="68615-165">Hello data factory 名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="68615-165">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="68615-166">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="68615-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="68615-167">新增下列程式碼會建立 hello**資料 factory** toohello **Main**方法。</span><span class="sxs-lookup"><span data-stu-id="68615-167">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```
8. <span data-ttu-id="68615-168">新增下列程式碼會建立 hello **Azure 儲存體連結服務**toohello **Main**方法。</span><span class="sxs-lookup"><span data-stu-id="68615-168">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="68615-169">以 Azure 儲存體帳戶的名稱和金鑰取代 **storageaccountname** 和 **accountkey**。</span><span class="sxs-lookup"><span data-stu-id="68615-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```
9. <span data-ttu-id="68615-170">新增下列程式碼會建立 hello**輸入和輸出資料集**toohello **Main**方法。</span><span class="sxs-lookup"><span data-stu-id="68615-170">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

    <span data-ttu-id="68615-171">hello **FolderPath** hello 輸入的 blob 設定太**adftutorial /**其中**adftutorial** hello 您的 blob 儲存體中的 hello 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="68615-171">hello **FolderPath** for hello input blob is set too**adftutorial/** where **adftutorial** is hello name of hello container in your blob storage.</span></span> <span data-ttu-id="68615-172">如果此容器不存在於您的 Azure blob 儲存體中，建立容器具有此名稱： **adftutorial**並上傳的文字檔案 toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="68615-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file toohello container.</span></span>

    <span data-ttu-id="68615-173">hello FolderPath hello 輸出 blob 設： **adftutorial/apifactoryoutput / {Slice}**其中**配量**是動態計算出根據的 hello 值**SliceStart**（開始日期時間的每個配量）。</span><span class="sxs-lookup"><span data-stu-id="68615-173">hello FolderPath for hello output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on hello value of **SliceStart** (start date-time of each slice.)</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
    
                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
                },
    
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
            }
        }
    });
    ```
10. <span data-ttu-id="68615-174">新增 hello 下列程式碼的**會建立並啟動管線**toohello **Main**方法。</span><span class="sxs-lookup"><span data-stu-id="68615-174">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="68615-175">此管線有一個 **CopyActivity**，它以 **BlobSource** 為來源，**BlobSink** 為接收器。</span><span class="sxs-lookup"><span data-stu-id="68615-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="68615-176">hello 複製活動會在 Azure Data Factory 中執行 hello 資料移動。</span><span class="sxs-lookup"><span data-stu-id="68615-176">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="68615-177">hello 活動被提供安全、 可靠且可擴充的方式的各種資料存放區之間的資料可以複製的全域可用服務。</span><span class="sxs-lookup"><span data-stu-id="68615-177">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="68615-178">請參閱[資料移動活動](data-factory-data-movement-activities.md)hello 複製活動的詳細資料的發行項。</span><span class="sxs-lookup"><span data-stu-id="68615-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need tooset slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
                                Name = Dataset_Source
                            }
                        },
                        Outputs = new List<ActivityOutput>()
                        {
                            new ActivityOutput()
                            {
                                Name = Dataset_Destination
                            }
                        },
                        TypeProperties = new CopyActivity()
                        {
                            Source = new BlobSource(),
                            Sink = new BlobSink()
                            {
                                WriteBatchSize = 10000,
                                WriteBatchTimeout = TimeSpan.FromMinutes(10)
                            }
                        }
                    }
    
                },
            }
        }
    });
    ```
12. <span data-ttu-id="68615-179">新增下列程式碼 toohello hello **Main**方法 tooget hello 狀態 hello 的資料配量的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="68615-179">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="68615-180">預期此範例中只有一個配量。</span><span class="sxs-lookup"><span data-stu-id="68615-180">There is only one slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");
        // wait before hello next status check
        Thread.Sleep(1000 * 12);
    
        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });
    
        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```
13. <span data-ttu-id="68615-181">**（選擇性）**新增 hello 下列程式碼執行 tooget 詳細資料的資料配量 toohello **Main**方法。</span><span class="sxs-lookup"><span data-stu-id="68615-181">**(optional)** Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }
    
    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="68615-182">新增下列 hello 所使用的 helper 方法的 hello **Main**方法 toohello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="68615-182">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span> <span data-ttu-id="68615-183">這個方法會出現，可讓您提供的對話方塊**使用者名**和**密碼**toolog 用於 tooAzure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="68615-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use toolog in tooAzure portal.</span></span>

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. <span data-ttu-id="68615-184">在 [hello 方案總管] 中，展開 hello 專案： **DataFactoryAPITestApp**，以滑鼠右鍵按一下**參考**，然後按一下**加入參考**。</span><span class="sxs-lookup"><span data-stu-id="68615-184">In hello Solution Explorer, expand hello project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="68615-185">選取 `System.Configuration` 組件的核取方塊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="68615-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="68615-186">建置 hello 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="68615-186">Build hello console application.</span></span> <span data-ttu-id="68615-187">按一下**建置**hello 功能表，然後按一下上**建置方案**。</span><span class="sxs-lookup"><span data-stu-id="68615-187">Click **Build** on hello menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="68615-188">確認至少一個檔案中沒有 hello adftutorial 容器在您的 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="68615-188">Confirm that there is at least one file in hello adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="68615-189">如果不是，建立 Emp.txt 檔案 [記事本] 中以 hello 下列內容並將它上傳 toohello adftutorial 容器。</span><span class="sxs-lookup"><span data-stu-id="68615-189">If not, create Emp.txt file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="68615-190">按一下以執行 hello 範例**偵錯** -> **開始偵錯**hello 功能表上。</span><span class="sxs-lookup"><span data-stu-id="68615-190">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="68615-191">當您看到 hello**正在執行的資料配量的詳細資料**，等待幾分鐘，然後按**ENTER**。</span><span class="sxs-lookup"><span data-stu-id="68615-191">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="68615-192">使用 Azure 入口網站 tooverify hello 該 hello 資料 factory **APITutorialFactory**建立以 hello 下列成品：</span><span class="sxs-lookup"><span data-stu-id="68615-192">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
    * <span data-ttu-id="68615-193">連結服務：**AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="68615-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="68615-194">資料集：**DatasetBlobSource** 和 **DatasetBlobDestination**。</span><span class="sxs-lookup"><span data-stu-id="68615-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="68615-195">管線： **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="68615-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="68615-196">確認已建立的輸出檔中 hello **apifactoryoutput**資料夾中 hello **adftutorial**容器。</span><span class="sxs-lookup"><span data-stu-id="68615-196">Verify that an output file is created in hello **apifactoryoutput** folder in hello **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="68615-197">取得失敗資料配量的清單</span><span class="sxs-lookup"><span data-stu-id="68615-197">Get a list of failed data slices</span></span> 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a><span data-ttu-id="68615-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="68615-198">Next steps</span></span>
<span data-ttu-id="68615-199">請參閱下列範例建立管線中使用.NET SDK 將資料從 Azure blob 儲存體 tooan Azure SQL database 複製 hello:</span><span class="sxs-lookup"><span data-stu-id="68615-199">See hello following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage tooan Azure SQL database:</span></span> 

- [<span data-ttu-id="68615-200">從 Blob 儲存體 tooSQL 資料庫中建立管線 toocopy 資料</span><span class="sxs-lookup"><span data-stu-id="68615-200">Create a pipeline toocopy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
