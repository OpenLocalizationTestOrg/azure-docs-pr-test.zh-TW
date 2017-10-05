---
title: "使用 Azure .NET SDK 建立資料管線 |Microsoft Docs"
description: "了解如何使用 Data Factory .NET SDK，以程式設計方式建立、監視和管理 Azure Data Factory。"
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
ms.openlocfilehash: 9d9dac75321c5d4e079f49320d9b7c6f56e48754
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="6aab1-103">使用 Azure Data Factory .NET SDK 來建立、監視及管理 Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6aab1-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="6aab1-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6aab1-104">Overview</span></span>
<span data-ttu-id="6aab1-105">您可以使用 Data Factory .NET SDK，以程式設計方式建立、監視及管理 Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6aab1-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="6aab1-106">本文包含指導您建立範例 .NET 主控台應用程式的逐步解說，此應用程式將會建立並監視 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="6aab1-106">This article contains a walkthrough that you can follow to create a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="6aab1-107">這篇文章並未涵蓋所有的 Data Factory .NET API。</span><span class="sxs-lookup"><span data-stu-id="6aab1-107">This article does not cover all the Data Factory .NET API.</span></span> <span data-ttu-id="6aab1-108">如需適用於 Data Factory 之 .NET API 的完整文件，請參閱 [Data Factory .NET API 參考](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1)。</span><span class="sxs-lookup"><span data-stu-id="6aab1-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6aab1-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="6aab1-109">Prerequisites</span></span>
* <span data-ttu-id="6aab1-110">Visual Studio 2012、2013 或 2015</span><span class="sxs-lookup"><span data-stu-id="6aab1-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="6aab1-111">下載並安裝 [Azure .NET SDK](http://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="6aab1-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="6aab1-112">Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="6aab1-112">Azure PowerShell.</span></span> <span data-ttu-id="6aab1-113">按照 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 一文中的指示操作，在您的電腦上安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="6aab1-113">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install Azure PowerShell on your computer.</span></span> <span data-ttu-id="6aab1-114">您可以使用 Azure PowerShell 建立 Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6aab1-114">You use Azure PowerShell to create an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="6aab1-115">在 Azure Active Directory 中建立應用程式</span><span class="sxs-lookup"><span data-stu-id="6aab1-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="6aab1-116">建立 Azure Active Directory 應用程式、建立該應用程式的服務主體，然後將其指派給 **Data Factory 參與者** 角色。</span><span class="sxs-lookup"><span data-stu-id="6aab1-116">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="6aab1-117">啟動 **PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="6aab1-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="6aab1-118">執行下列命令並輸入您用來登入 Azure 入口網站的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="6aab1-118">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="6aab1-119">執行下列命令以檢視此帳戶的所有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6aab1-119">Run the following command to view all the subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="6aab1-120">執行下列命令以選取您要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6aab1-120">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="6aab1-121">以您的 Azure 訂用帳戶名稱取代 **&lt;NameOfAzureSubscription**&gt;。</span><span class="sxs-lookup"><span data-stu-id="6aab1-121">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="6aab1-122">請記下此命令輸出中的 **SubscriptionId** 和 **TenantId**。</span><span class="sxs-lookup"><span data-stu-id="6aab1-122">Note down **SubscriptionId** and **TenantId** from the output of this command.</span></span>

5. <span data-ttu-id="6aab1-123">在 PowerShell 中執行以下命令，建立名為 **ADFTutorialResourceGroup** 的 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="6aab1-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="6aab1-124">如果資源群組已存在，您可指定是否要更新 (Y) 或予以保留 (N)。</span><span class="sxs-lookup"><span data-stu-id="6aab1-124">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="6aab1-125">如果使用不同的資源群組，您必須以資源群組的名稱取代本教學課程中的 ADFTutorialResourceGroup。</span><span class="sxs-lookup"><span data-stu-id="6aab1-125">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="6aab1-126">建立 Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6aab1-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="6aab1-127">如果您收到下列錯誤，請指定不同的 URL 並再次執行此命令。</span><span class="sxs-lookup"><span data-stu-id="6aab1-127">If you get the following error, specify a different URL and run the command again.</span></span>
    
    ```PowerShell
    Another object with the same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="6aab1-128">建立 AD 服務主體。</span><span class="sxs-lookup"><span data-stu-id="6aab1-128">Create the AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="6aab1-129">對 **Data Factory 參與者** 角色新增服務主體。</span><span class="sxs-lookup"><span data-stu-id="6aab1-129">Add service principal to the **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="6aab1-130">取得應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="6aab1-130">Get the application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="6aab1-131">記下輸出的應用程式識別碼 (applicationID)。</span><span class="sxs-lookup"><span data-stu-id="6aab1-131">Note down the application ID (applicationID) from the output.</span></span>

<span data-ttu-id="6aab1-132">您應會從這些步驟取得下列四個值︰</span><span class="sxs-lookup"><span data-stu-id="6aab1-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="6aab1-133">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="6aab1-133">Tenant ID</span></span>
* <span data-ttu-id="6aab1-134">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="6aab1-134">Subscription ID</span></span>
* <span data-ttu-id="6aab1-135">應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="6aab1-135">Application ID</span></span>
* <span data-ttu-id="6aab1-136">密碼 (在第一個命令中指定)</span><span class="sxs-lookup"><span data-stu-id="6aab1-136">Password (specified in the first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="6aab1-137">逐步介紹</span><span class="sxs-lookup"><span data-stu-id="6aab1-137">Walkthrough</span></span>
<span data-ttu-id="6aab1-138">在逐步解說中，您可以建立具有管線的資料處理站，其中包含複製活動。</span><span class="sxs-lookup"><span data-stu-id="6aab1-138">In the walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="6aab1-139">複製活動會將資料從 Azure Blob 儲存體中的資料夾，複製到相同 Blob 儲存體中的另一個資料夾。</span><span class="sxs-lookup"><span data-stu-id="6aab1-139">The copy activity copies data from a folder in your Azure blob storage to another folder in the same blob storage.</span></span> 

<span data-ttu-id="6aab1-140">複製活動會在 Azure Data Factory 中執行資料移動。</span><span class="sxs-lookup"><span data-stu-id="6aab1-140">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="6aab1-141">此活動是由全域可用的服務所提供，可以使用安全、可靠及可調整的方式，在各種不同的資料存放區之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="6aab1-141">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="6aab1-142">如需複製活動的詳細資訊，請參閱 [資料移動活動](data-factory-data-movement-activities.md) 文章。</span><span class="sxs-lookup"><span data-stu-id="6aab1-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

1. <span data-ttu-id="6aab1-143">使用 Visual Studio 2012/2013/2015 建立 C# .NET 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6aab1-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="6aab1-144">啟動 **Visual Studio** 2012/2013/2015。</span><span class="sxs-lookup"><span data-stu-id="6aab1-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="6aab1-145">按一下 [檔案]，指向 [新增]，然後按一下 [專案]。</span><span class="sxs-lookup"><span data-stu-id="6aab1-145">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="6aab1-146">展開 [範本]，然後選取 [Visual C#]。</span><span class="sxs-lookup"><span data-stu-id="6aab1-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="6aab1-147">在此逐步解說中，您使用的是 C#，但您可以使用任何 .NET 語言。</span><span class="sxs-lookup"><span data-stu-id="6aab1-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="6aab1-148">從右邊的專案類型清單中選取 [主控台應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="6aab1-148">Select **Console Application** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="6aab1-149">在 [名稱] 中輸入 **DataFactoryAPITestApp** 。</span><span class="sxs-lookup"><span data-stu-id="6aab1-149">Enter **DataFactoryAPITestApp** for the Name.</span></span>
   6. <span data-ttu-id="6aab1-150">在 [位置] 中選取 **C:\ADFGetStarted**。</span><span class="sxs-lookup"><span data-stu-id="6aab1-150">Select **C:\ADFGetStarted** for the Location.</span></span>
   7. <span data-ttu-id="6aab1-151">按一下 [確定]  以建立專案。</span><span class="sxs-lookup"><span data-stu-id="6aab1-151">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="6aab1-152">按一下 [**工具**]，指向 [**NuGet 封裝管理員**]，然後按一下 [**封裝管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="6aab1-152">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="6aab1-153">在 [Package Manager Console] 中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="6aab1-153">In the **Package Manager Console**, do the following steps:</span></span>
   1. <span data-ttu-id="6aab1-154">執行以下命令安裝 Data Factory 套件：`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="6aab1-154">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="6aab1-155">執行下列命令安裝 Azure Active Directory 套件 (您在程式碼中使用 Active Directory API)︰`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="6aab1-155">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="6aab1-156">以下列內容取代專案中 **App.config** 檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="6aab1-156">Replace the contents of **App.config** file in the project with the following content:</span></span> 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating the AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. <span data-ttu-id="6aab1-157">在 App.Config 檔案中，以您自己的值更新**&lt;應用程式識別碼&gt;**、**&lt;密碼&gt;**、**&lt;訂用帳戶識別碼&gt;****&lt;租用戶識別碼&gt;**的值。</span><span class="sxs-lookup"><span data-stu-id="6aab1-157">In the App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="6aab1-158">將下列 **using** 陳述式新增至專案的 **Program.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="6aab1-158">Add the following **using** statements to the **Program.cs** file in the project.</span></span>

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
6. <span data-ttu-id="6aab1-159">將下列會建立 **DataPipelineManagementClient** 類別執行個體的程式碼新增至 **Main** 方法中。</span><span class="sxs-lookup"><span data-stu-id="6aab1-159">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span></span> <span data-ttu-id="6aab1-160">您會使用此物件來建立 Data Factory、連結的服務、輸入和輸出資料集，以及管線。</span><span class="sxs-lookup"><span data-stu-id="6aab1-160">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="6aab1-161">您也會使用此物件來監視執行階段的資料集配量。</span><span class="sxs-lookup"><span data-stu-id="6aab1-161">You also use this object to monitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify the name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: the name of the data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="6aab1-162">以您的 Azure 資源群組名稱取代 **resourceGroupName** 的值。</span><span class="sxs-lookup"><span data-stu-id="6aab1-162">Replace the value of **resourceGroupName** with the name of your Azure resource group.</span></span> <span data-ttu-id="6aab1-163">若要建立資源群組，請使用 [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6aab1-163">You can create a resource group using the [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="6aab1-164">將 Data Factory 的名稱 (dataFactoryName) 更新成唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="6aab1-164">Update name of the data factory (dataFactoryName) to be unique.</span></span> <span data-ttu-id="6aab1-165">Data Factory 的名稱必須是全域唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="6aab1-165">Name of the data factory must be globally unique.</span></span> <span data-ttu-id="6aab1-166">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="6aab1-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="6aab1-167">將下列會建立 **data Factory** 的程式碼新增至 **Main** 方法中。</span><span class="sxs-lookup"><span data-stu-id="6aab1-167">Add the following code that creates a **data factory** to the **Main** method.</span></span>

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
8. <span data-ttu-id="6aab1-168">將下列會建立 **Azure 儲存體**的程式碼新增至 **Main** 方法中。</span><span class="sxs-lookup"><span data-stu-id="6aab1-168">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="6aab1-169">以 Azure 儲存體帳戶的名稱和金鑰取代 **storageaccountname** 和 **accountkey**。</span><span class="sxs-lookup"><span data-stu-id="6aab1-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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
9. <span data-ttu-id="6aab1-170">將下列會建立**輸入和輸出資料集**的程式碼新增至 **Main** 方法中。</span><span class="sxs-lookup"><span data-stu-id="6aab1-170">Add the following code that creates **input and output datasets** to the **Main** method.</span></span>

    <span data-ttu-id="6aab1-171">輸入 Blob 的 **FolderPath** 是設定為 **adftutorial/**，其中的 **adftutorial** 是 Blob 儲存體中容器的名稱。</span><span class="sxs-lookup"><span data-stu-id="6aab1-171">The **FolderPath** for the input blob is set to **adftutorial/** where **adftutorial** is the name of the container in your blob storage.</span></span> <span data-ttu-id="6aab1-172">如果 Azure Blob 儲存體中沒有此容器，請以下列名稱建立容器： **adftutorial** ，並將文字檔上傳至容器。</span><span class="sxs-lookup"><span data-stu-id="6aab1-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file to the container.</span></span>

    <span data-ttu-id="6aab1-173">輸出 Blob 的 FolderPath 是設定為：**adftutorial/apifactoryoutput/{Slice}**，其中的 **Slice** 是根據 **SliceStart** (每個配量的開始日期時間) 的值自動計算而得。</span><span class="sxs-lookup"><span data-stu-id="6aab1-173">The FolderPath for the output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on the value of **SliceStart** (start date-time of each slice.)</span></span>

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
10. <span data-ttu-id="6aab1-174">將下列會**建立並啟用管線**的程式碼新增至 **Main** 方法中。</span><span class="sxs-lookup"><span data-stu-id="6aab1-174">Add the following code that **creates and activates a pipeline** to the **Main** method.</span></span> <span data-ttu-id="6aab1-175">此管線有一個 **CopyActivity**，它以 **BlobSource** 為來源，**BlobSink** 為接收器。</span><span class="sxs-lookup"><span data-stu-id="6aab1-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="6aab1-176">複製活動會在 Azure Data Factory 中執行資料移動。</span><span class="sxs-lookup"><span data-stu-id="6aab1-176">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="6aab1-177">此活動是由全域可用的服務所提供，可以使用安全、可靠及可調整的方式，在各種不同的資料存放區之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="6aab1-177">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="6aab1-178">如需複製活動的詳細資訊，請參閱 [資料移動活動](data-factory-data-movement-activities.md) 文章。</span><span class="sxs-lookup"><span data-stu-id="6aab1-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

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
    
                // Initial value for pipeline's active period. With this, you won't need to set slice status
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
12. <span data-ttu-id="6aab1-179">將下列程式碼加入 **Main** 方法中，以取得輸出資料集的資料配量狀態。</span><span class="sxs-lookup"><span data-stu-id="6aab1-179">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span></span> <span data-ttu-id="6aab1-180">預期此範例中只有一個配量。</span><span class="sxs-lookup"><span data-stu-id="6aab1-180">There is only one slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling the slice status");
        // wait before the next status check
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
13. <span data-ttu-id="6aab1-181">**(選用)** 將下列取得資料配量之執行詳細資料的程式碼新增到 **Main** 方法中。</span><span class="sxs-lookup"><span data-stu-id="6aab1-181">**(optional)** Add the following code to get run details for a data slice to the **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for the output slice to be ready
    Console.WriteLine("\nGive it a few minutes for the output slice to be ready and press any key.");
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
    
    Console.WriteLine("\nPress any key to exit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="6aab1-182">將 **Main** 方法所使用的下列 Helper 方法新增至 **Program** 類別中。</span><span class="sxs-lookup"><span data-stu-id="6aab1-182">Add the following helper method used by the **Main** method to the **Program** class.</span></span> <span data-ttu-id="6aab1-183">此方法會顯示一個對話方塊，讓您提供用來登入 Azure 入口網站的**使用者名稱**和**密碼**。</span><span class="sxs-lookup"><span data-stu-id="6aab1-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use to log in to Azure portal.</span></span>

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

        throw new InvalidOperationException("Failed to acquire token");
    }
    ```

15. <span data-ttu-id="6aab1-184">在 [方案總管] 中展開 **DataFactoryAPITestApp** 專案，以滑鼠右鍵按一下 [參考]，然後按一下 [加入參考]。</span><span class="sxs-lookup"><span data-stu-id="6aab1-184">In the Solution Explorer, expand the project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="6aab1-185">選取 `System.Configuration` 組件的核取方塊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6aab1-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="6aab1-186">建置主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6aab1-186">Build the console application.</span></span> <span data-ttu-id="6aab1-187">按一下功能表上的 [建置]，再按一下 [建置方案]。</span><span class="sxs-lookup"><span data-stu-id="6aab1-187">Click **Build** on the menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="6aab1-188">確認您 Azure Blob 儲存體之 adftutorial 容器中至少有一個檔案。</span><span class="sxs-lookup"><span data-stu-id="6aab1-188">Confirm that there is at least one file in the adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="6aab1-189">如果沒有，請在「記事本」中以下列內容建立 Emp.txt 檔案，然後將它上傳至 adftutorial 容器。</span><span class="sxs-lookup"><span data-stu-id="6aab1-189">If not, create Emp.txt file in Notepad with the following content and upload it to the adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="6aab1-190">按一下功能表上的 [偵錯] -> [開始偵錯]，執行範例。</span><span class="sxs-lookup"><span data-stu-id="6aab1-190">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span></span> <span data-ttu-id="6aab1-191">當您看到 [取得資料配量的執行詳細資料]，請等待數分鐘再按 **ENTER**。</span><span class="sxs-lookup"><span data-stu-id="6aab1-191">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="6aab1-192">使用 Azure 入口網站確認 Data Factory： **APITutorialFactory** 是使用下列成品所建立：</span><span class="sxs-lookup"><span data-stu-id="6aab1-192">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span></span>
    * <span data-ttu-id="6aab1-193">連結服務：**AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="6aab1-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="6aab1-194">資料集：**DatasetBlobSource** 和 **DatasetBlobDestination**。</span><span class="sxs-lookup"><span data-stu-id="6aab1-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="6aab1-195">管線： **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="6aab1-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="6aab1-196">確認輸出檔案已建立於 **adftutorial** 容器的 **apifactoryoutput** 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="6aab1-196">Verify that an output file is created in the **apifactoryoutput** folder in the **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="6aab1-197">取得失敗資料配量的清單</span><span class="sxs-lookup"><span data-stu-id="6aab1-197">Get a list of failed data slices</span></span> 

```csharp
// Parse the resource path
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

## <a name="next-steps"></a><span data-ttu-id="6aab1-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6aab1-198">Next steps</span></span>
<span data-ttu-id="6aab1-199">請參閱下列範例以建立管線，該管線使用 .NET SDK (從 Azure Blob 儲存體將資料複製到 Azure SQL Database)：</span><span class="sxs-lookup"><span data-stu-id="6aab1-199">See the following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage to an Azure SQL database:</span></span> 

- [<span data-ttu-id="6aab1-200">建立管線以將資料從 Blob 儲存體複製到 SQL Database</span><span class="sxs-lookup"><span data-stu-id="6aab1-200">Create a pipeline to copy data from Blob Storage to SQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
