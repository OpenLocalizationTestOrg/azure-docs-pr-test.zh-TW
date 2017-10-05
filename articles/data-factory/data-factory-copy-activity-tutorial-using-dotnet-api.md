---
title: "教學課程：使用 .NET API 建立具有複製活動的管線 | Microsoft Docs"
description: "在本教學課程中，您會使用 .NET API，建立具有複製活動的 Azure Data Factory 管線。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 30c7cd1ba455d7b1bc93d76e7ee79455bb52aae9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a><span data-ttu-id="abfb2-103">教學課程：使用 .NET API 建立具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="abfb2-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="abfb2-104">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="abfb2-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="abfb2-105">複製精靈</span><span class="sxs-lookup"><span data-stu-id="abfb2-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="abfb2-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="abfb2-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="abfb2-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="abfb2-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="abfb2-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="abfb2-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="abfb2-109">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="abfb2-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="abfb2-110">REST API</span><span class="sxs-lookup"><span data-stu-id="abfb2-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="abfb2-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="abfb2-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="abfb2-112">在本文中，您會了解如何使用 [.NET API](https://portal.azure.com) 建立資料處理站，其中有管線可將資料從 Azure Blob 儲存體複製到 Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="abfb2-112">In this article, you learn how to use [.NET API](https://portal.azure.com) to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="abfb2-113">如果您不熟悉 Azure Data Factory，請先詳閱 [Azure Data Factory 簡介](data-factory-introduction.md)一文，再進行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="abfb2-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="abfb2-114">在本教學課程中，您可以建立包含一個活動的管線：複製活動。</span><span class="sxs-lookup"><span data-stu-id="abfb2-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="abfb2-115">複製活動會將資料從支援的資料存放區複製到支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="abfb2-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="abfb2-116">如需作為來源和接收區支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="abfb2-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="abfb2-117">此活動是由全域可用的服務所提供，可以使用安全、可靠及可調整的方式，在各種不同的資料存放區之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="abfb2-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="abfb2-118">如需複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="abfb2-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="abfb2-119">一個管線中可以有多個活動。</span><span class="sxs-lookup"><span data-stu-id="abfb2-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="abfb2-120">您可以將一個活動的輸出資料集設為另一個活動的輸入資料集，藉此鏈結兩個活動 (讓一個活動接著另一個活動執行)。</span><span class="sxs-lookup"><span data-stu-id="abfb2-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="abfb2-121">如需詳細資訊，請參閱[管線中的多個活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="abfb2-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="abfb2-122">如需適用於 Data Factory 之 .NET API 的完整文件，請參閱 [Data Factory .NET API 參考](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1)。</span><span class="sxs-lookup"><span data-stu-id="abfb2-122">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>
> 
> <span data-ttu-id="abfb2-123">本教學課程中的資料管線會將資料從來源資料存放區，複製到目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="abfb2-123">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="abfb2-124">如需如何使用 Azure Data Factory 轉換資料的教學課程，請參閱[教學課程︰使用 Hadoop 叢集建置管線來轉換資料](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="abfb2-124">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abfb2-125">必要條件</span><span class="sxs-lookup"><span data-stu-id="abfb2-125">Prerequisites</span></span>
* <span data-ttu-id="abfb2-126">請檢閱 [教學課程概觀和必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) ，以取得本教學課程的概觀並完成 **必要** 步驟。</span><span class="sxs-lookup"><span data-stu-id="abfb2-126">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to get an overview of the tutorial and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="abfb2-127">Visual Studio 2012、2013 或 2015</span><span class="sxs-lookup"><span data-stu-id="abfb2-127">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="abfb2-128">下載並安裝 [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="abfb2-128">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>
* <span data-ttu-id="abfb2-129">Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="abfb2-129">Azure PowerShell.</span></span> <span data-ttu-id="abfb2-130">按照 [如何安裝和設定 Azure PowerShell](../powershell-install-configure.md) 一文中的指示操作，在您的電腦上安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="abfb2-130">Follow instructions in [How to install and configure Azure PowerShell](../powershell-install-configure.md) article to install Azure PowerShell on your computer.</span></span> <span data-ttu-id="abfb2-131">您可以使用 Azure PowerShell 建立 Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="abfb2-131">You use Azure PowerShell to create an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="abfb2-132">在 Azure Active Directory 中建立應用程式</span><span class="sxs-lookup"><span data-stu-id="abfb2-132">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="abfb2-133">建立 Azure Active Directory 應用程式、建立該應用程式的服務主體，然後將其指派給 **Data Factory 參與者** 角色。</span><span class="sxs-lookup"><span data-stu-id="abfb2-133">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="abfb2-134">啟動 **PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="abfb2-134">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="abfb2-135">執行下列命令並輸入您用來登入 Azure 入口網站的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="abfb2-135">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="abfb2-136">執行下列命令以檢視此帳戶的所有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="abfb2-136">Run the following command to view all the subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="abfb2-137">執行下列命令以選取您要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="abfb2-137">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="abfb2-138">以您的 Azure 訂用帳戶名稱取代 **&lt;NameOfAzureSubscription**&gt;。</span><span class="sxs-lookup"><span data-stu-id="abfb2-138">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="abfb2-139">請記下此命令輸出中的 **SubscriptionId** 和 **TenantId**。</span><span class="sxs-lookup"><span data-stu-id="abfb2-139">Note down **SubscriptionId** and **TenantId** from the output of this command.</span></span>

5. <span data-ttu-id="abfb2-140">在 PowerShell 中執行以下命令，建立名為 **ADFTutorialResourceGroup** 的 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="abfb2-140">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="abfb2-141">如果資源群組已存在，您可指定是否要更新 (Y) 或予以保留 (N)。</span><span class="sxs-lookup"><span data-stu-id="abfb2-141">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="abfb2-142">如果使用不同的資源群組，您必須以資源群組的名稱取代本教學課程中的 ADFTutorialResourceGroup。</span><span class="sxs-lookup"><span data-stu-id="abfb2-142">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="abfb2-143">建立 Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="abfb2-143">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="abfb2-144">如果您收到下列錯誤，請指定不同的 URL 並再次執行此命令。</span><span class="sxs-lookup"><span data-stu-id="abfb2-144">If you get the following error, specify a different URL and run the command again.</span></span>
    
    ```PowerShell
    Another object with the same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="abfb2-145">建立 AD 服務主體。</span><span class="sxs-lookup"><span data-stu-id="abfb2-145">Create the AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="abfb2-146">對 **Data Factory 參與者** 角色新增服務主體。</span><span class="sxs-lookup"><span data-stu-id="abfb2-146">Add service principal to the **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="abfb2-147">取得應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="abfb2-147">Get the application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="abfb2-148">記下輸出的應用程式識別碼 (applicationID)。</span><span class="sxs-lookup"><span data-stu-id="abfb2-148">Note down the application ID (applicationID) from the output.</span></span>

<span data-ttu-id="abfb2-149">您應會從這些步驟取得下列四個值︰</span><span class="sxs-lookup"><span data-stu-id="abfb2-149">You should have following four values from these steps:</span></span>

* <span data-ttu-id="abfb2-150">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="abfb2-150">Tenant ID</span></span>
* <span data-ttu-id="abfb2-151">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="abfb2-151">Subscription ID</span></span>
* <span data-ttu-id="abfb2-152">應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="abfb2-152">Application ID</span></span>
* <span data-ttu-id="abfb2-153">密碼 (在第一個命令中指定)</span><span class="sxs-lookup"><span data-stu-id="abfb2-153">Password (specified in the first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="abfb2-154">逐步介紹</span><span class="sxs-lookup"><span data-stu-id="abfb2-154">Walkthrough</span></span>
1. <span data-ttu-id="abfb2-155">使用 Visual Studio 2012/2013/2015 建立 C# .NET 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="abfb2-155">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="abfb2-156">啟動 **Visual Studio** 2012/2013/2015。</span><span class="sxs-lookup"><span data-stu-id="abfb2-156">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="abfb2-157">按一下 [檔案]，指向 [新增]，然後按一下 [專案]。</span><span class="sxs-lookup"><span data-stu-id="abfb2-157">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="abfb2-158">展開 [範本]，然後選取 [Visual C#]。</span><span class="sxs-lookup"><span data-stu-id="abfb2-158">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="abfb2-159">在此逐步解說中，您使用的是 C#，但您可以使用任何 .NET 語言。</span><span class="sxs-lookup"><span data-stu-id="abfb2-159">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="abfb2-160">從右邊的專案類型清單中選取 [主控台應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="abfb2-160">Select **Console Application** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="abfb2-161">在 [名稱] 中輸入 **DataFactoryAPITestApp** 。</span><span class="sxs-lookup"><span data-stu-id="abfb2-161">Enter **DataFactoryAPITestApp** for the Name.</span></span>
   6. <span data-ttu-id="abfb2-162">在 [位置] 中選取 **C:\ADFGetStarted**。</span><span class="sxs-lookup"><span data-stu-id="abfb2-162">Select **C:\ADFGetStarted** for the Location.</span></span>
   7. <span data-ttu-id="abfb2-163">按一下 [確定]  以建立專案。</span><span class="sxs-lookup"><span data-stu-id="abfb2-163">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="abfb2-164">按一下 [**工具**]，指向 [**NuGet 封裝管理員**]，然後按一下 [**封裝管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="abfb2-164">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="abfb2-165">在 [Package Manager Console] 中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="abfb2-165">In the **Package Manager Console**, do the following steps:</span></span>
   1. <span data-ttu-id="abfb2-166">執行以下命令安裝 Data Factory 套件：`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="abfb2-166">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="abfb2-167">執行下列命令安裝 Azure Active Directory 套件 (您在程式碼中使用 Active Directory API)︰`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="abfb2-167">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="abfb2-168">將下列 **appSetttings** 區段新增 **App.config** 檔案。</span><span class="sxs-lookup"><span data-stu-id="abfb2-168">Add the following **appSetttings** section to the **App.config** file.</span></span> <span data-ttu-id="abfb2-169">以下 Helper 方法會使用這些設定： **Microsoft.identitymodel.waad.preview.graph.graphinterface**。</span><span class="sxs-lookup"><span data-stu-id="abfb2-169">These settings are used by the helper method: **GetAuthorizationHeader**.</span></span>

    <span data-ttu-id="abfb2-170">以您自己的值取代**&lt;應用程式識別碼&gt;**、**&lt;密碼&gt;**、**&lt;訂用帳戶識別碼&gt;****&lt;租用戶識別碼&gt;**的值。</span><span class="sxs-lookup"><span data-stu-id="abfb2-170">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>

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

5. <span data-ttu-id="abfb2-171">將下列 **using** 陳述式加入專案的原始程式檔 (Program.cs) 中。</span><span class="sxs-lookup"><span data-stu-id="abfb2-171">Add the following **using** statements to the source file (Program.cs) in the project.</span></span>

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

6. <span data-ttu-id="abfb2-172">將下列會建立 **DataPipelineManagementClient** 類別執行個體的程式碼新增至 **Main** 方法中。</span><span class="sxs-lookup"><span data-stu-id="abfb2-172">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span></span> <span data-ttu-id="abfb2-173">您會使用此物件來建立 Data Factory、連結的服務、輸入和輸出資料集，以及管線。</span><span class="sxs-lookup"><span data-stu-id="abfb2-173">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="abfb2-174">您也會使用此物件來監視執行階段的資料集配量。</span><span class="sxs-lookup"><span data-stu-id="abfb2-174">You also use this object to monitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="abfb2-175">以您的 Azure 資源群組名稱取代 **resourceGroupName** 的值。</span><span class="sxs-lookup"><span data-stu-id="abfb2-175">Replace the value of **resourceGroupName** with the name of your Azure resource group.</span></span>
   >
   > <span data-ttu-id="abfb2-176">將 Data Factory 的名稱 (dataFactoryName) 更新成唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="abfb2-176">Update name of the data factory (dataFactoryName) to be unique.</span></span> <span data-ttu-id="abfb2-177">Data Factory 的名稱必須是全域唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="abfb2-177">Name of the data factory must be globally unique.</span></span> <span data-ttu-id="abfb2-178">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="abfb2-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>

7. <span data-ttu-id="abfb2-179">將下列會建立 **data Factory** 的程式碼新增至 **Main** 方法中。</span><span class="sxs-lookup"><span data-stu-id="abfb2-179">Add the following code that creates a **data factory** to the **Main** method.</span></span>

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

    <span data-ttu-id="abfb2-180">資料處理站可以有一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="abfb2-180">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="abfb2-181">其中的管線可以有一或多個活動。</span><span class="sxs-lookup"><span data-stu-id="abfb2-181">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="abfb2-182">例如，「複製活動」會從來源將資料複製到目的地資料存放區，HDInsight Hive 活動則是執行 Hive 指令碼來轉換輸入資料，以產生輸出資料。</span><span class="sxs-lookup"><span data-stu-id="abfb2-182">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="abfb2-183">讓我們在這個步驟中開始建立 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="abfb2-183">Let's start with creating the data factory in this step.</span></span>
8. <span data-ttu-id="abfb2-184">將下列會建立 **Azure 儲存體**的程式碼新增至 **Main** 方法中。</span><span class="sxs-lookup"><span data-stu-id="abfb2-184">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="abfb2-185">以 Azure 儲存體帳戶的名稱和金鑰取代 **storageaccountname** 和 **accountkey**。</span><span class="sxs-lookup"><span data-stu-id="abfb2-185">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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

    <span data-ttu-id="abfb2-186">您在資料處理站中建立的連結服務會將您的資料存放區和計算服務連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="abfb2-186">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="abfb2-187">在本教學課程中，您不會使用任何計算服務，例如 Azure HDInsight 或 Azure Data Lake Analytics。</span><span class="sxs-lookup"><span data-stu-id="abfb2-187">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="abfb2-188">您可以使用兩種類型的資料存放區：Azure 儲存體 (來源) 和 Azure SQL Database (目的地)。</span><span class="sxs-lookup"><span data-stu-id="abfb2-188">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

    <span data-ttu-id="abfb2-189">因此，您可以建立名為 AzureStorageLinkedService 和 AzureSqlLinkedService 的兩個連結服務︰類型為 AzureStorage 和 AzureSqlDatabase。</span><span class="sxs-lookup"><span data-stu-id="abfb2-189">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

    <span data-ttu-id="abfb2-190">AzureStorageLinkedService 會將 Azure 儲存體帳戶連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="abfb2-190">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="abfb2-191">此儲存體帳戶是您在其中建立容器並將資料上傳為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)一部分的帳戶。</span><span class="sxs-lookup"><span data-stu-id="abfb2-191">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
9. <span data-ttu-id="abfb2-192">將下列會建立 **Azure SQL 連結服務**的程式碼新增至 **Main** 方法中。</span><span class="sxs-lookup"><span data-stu-id="abfb2-192">Add the following code that creates an **Azure SQL linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="abfb2-193">以您的 Azure SQL 伺服器名稱、資料庫名稱、使用者和密碼取代 **servername**、**databasename**、**username** **password**。</span><span class="sxs-lookup"><span data-stu-id="abfb2-193">Replace **servername**, **databasename**, **username**, and **password** with names of your Azure SQL server, database, user, and password.</span></span>

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    <span data-ttu-id="abfb2-194">AzureSqlLinkedService 會將 Azure SQL Database 連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="abfb2-194">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="abfb2-195">從 Blob 儲存體複製的資料會儲存在此資料庫中。</span><span class="sxs-lookup"><span data-stu-id="abfb2-195">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="abfb2-196">您在此資料庫中建立了 emp 資料表，作為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="abfb2-196">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
10. <span data-ttu-id="abfb2-197">將下列會建立**輸入和輸出資料集**的程式碼新增至 **Main** 方法中。</span><span class="sxs-lookup"><span data-stu-id="abfb2-197">Add the following code that creates **input and output datasets** to the **Main** method.</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "InputDataset";
    string Dataset_Destination = "OutputDataset";

    Console.WriteLine("Creating input dataset of type: Azure Blob");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
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

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
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
    
    <span data-ttu-id="abfb2-198">在上一個步驟中，您已建立可將 Azure 儲存體帳戶和 Azure SQL Database 連結至資料處理站的連結服務。</span><span class="sxs-lookup"><span data-stu-id="abfb2-198">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="abfb2-199">在此步驟中，您會定義名為 InputDataset 和 OutputDataset 的兩個資料集，它們分別代表 AzureStorageLinkedService 和 AzureSqlLinkedService 所參照資料存放區中儲存的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="abfb2-199">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

    <span data-ttu-id="abfb2-200">Azure 儲存體連結服務會指定 Data Factory 服務在執行階段用來連線到 Azure 儲存體帳戶的連接字串。</span><span class="sxs-lookup"><span data-stu-id="abfb2-200">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="abfb2-201">而且，輸入 Blob 資料集 (InputDataset) 會指定包含輸入資料的容器和資料夾。</span><span class="sxs-lookup"><span data-stu-id="abfb2-201">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="abfb2-202">同樣第，Azure SQL Database 連結服務會指定 Data Factory 在執行階段用來連線到 Azure SQL Database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="abfb2-202">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="abfb2-203">而且，輸出 SQL 資料表資料集 (OututDataset) 會指定資料庫中作為 Blob 儲存體資料複製目的地的資料表。</span><span class="sxs-lookup"><span data-stu-id="abfb2-203">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span>

    <span data-ttu-id="abfb2-204">在此步驟中，您將在 AzureStorageLinkedService 連結服務所代表的 Azure 儲存體中，建立名為 InputDataset 的資料集，該資料集會指向 Blob 容器 (adftutorial) 根資料夾中的 Blob 檔案 (emp.txt)。</span><span class="sxs-lookup"><span data-stu-id="abfb2-204">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="abfb2-205">如果您未指定 (或跳過) fileName 的值，則輸入資料夾中所有 Blob 資料都會複製到目的地。</span><span class="sxs-lookup"><span data-stu-id="abfb2-205">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="abfb2-206">在本教學課程中，您可指定 fileName 的值。</span><span class="sxs-lookup"><span data-stu-id="abfb2-206">In this tutorial, you specify a value for the fileName.</span></span>    

    <span data-ttu-id="abfb2-207">在此步驟中，您會建立名為 **OutputDataset**的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="abfb2-207">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="abfb2-208">此資料集指向 Azure SQL Database 中 **AzureSqlLinkedService**所代表的 SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="abfb2-208">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService**.</span></span>
11. <span data-ttu-id="abfb2-209">將下列會**建立並啟用管線**的程式碼新增至 **Main** 方法中。</span><span class="sxs-lookup"><span data-stu-id="abfb2-209">Add the following code that **creates and activates a pipeline** to the **Main** method.</span></span> <span data-ttu-id="abfb2-210">在此步驟中您會建立管線，其中含有使用 **InputDataset** 作為輸入和使用 **OutputDataset** 作為輸出的**複製活動**。</span><span class="sxs-lookup"><span data-stu-id="abfb2-210">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

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
                            Name = "BlobToAzureSql",
                            Inputs = new List<ActivityInput>()
                            {
                                new ActivityInput() {
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
                    }
                }
            }
        });
    ```

    <span data-ttu-id="abfb2-211">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="abfb2-211">Note the following points:</span></span>
   
    - <span data-ttu-id="abfb2-212">在活動區段中，只會有一個 **type** 設為 **Copy** 的活動。</span><span class="sxs-lookup"><span data-stu-id="abfb2-212">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="abfb2-213">如需複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="abfb2-213">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="abfb2-214">在 Data Factory 解決方案中，您也可以使用[資料轉換活動](data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="abfb2-214">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="abfb2-215">活動的輸入設定為 **InputDataset**，活動的輸出則設定為 **OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="abfb2-215">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="abfb2-216">在 **typeProperties** 區段中，來源類型指定為 **BlobSource**，接收類型指定為 **SqlSink**。</span><span class="sxs-lookup"><span data-stu-id="abfb2-216">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="abfb2-217">如需複製活動作為來源和接收器支援的資料存放區完整清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="abfb2-217">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="abfb2-218">若要了解如何使用特定支援的資料存放區作為來源/接收器，請按一下資料表中的連結。</span><span class="sxs-lookup"><span data-stu-id="abfb2-218">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
   
    <span data-ttu-id="abfb2-219">目前，驅動排程的是輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="abfb2-219">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="abfb2-220">在本教學課程中，輸出資料集設定成一小時產生一次配量。</span><span class="sxs-lookup"><span data-stu-id="abfb2-220">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="abfb2-221">管線具有相隔一天 (也就是 24 小時) 的開始時間和結束時間。</span><span class="sxs-lookup"><span data-stu-id="abfb2-221">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="abfb2-222">因此，管線會產生輸出資料集的 24 個配量。</span><span class="sxs-lookup"><span data-stu-id="abfb2-222">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span>
12. <span data-ttu-id="abfb2-223">將下列程式碼加入 **Main** 方法中，以取得輸出資料集的資料配量狀態。</span><span class="sxs-lookup"><span data-stu-id="abfb2-223">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span></span> <span data-ttu-id="abfb2-224">在此範例中只預期有配量。</span><span class="sxs-lookup"><span data-stu-id="abfb2-224">There is only slice expected in this sample.</span></span>

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

13. <span data-ttu-id="abfb2-225">將下列會取得資料配量之執行詳細資料的程式碼加入 **Main** 方法中。</span><span class="sxs-lookup"><span data-stu-id="abfb2-225">Add the following code to get run details for a data slice to the **Main** method.</span></span>

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
            }
        );

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

14. <span data-ttu-id="abfb2-226">將 **Main** 方法所使用的下列 Helper 方法新增至 **Program** 類別中。</span><span class="sxs-lookup"><span data-stu-id="abfb2-226">Add the following helper method used by the **Main** method to the **Program** class.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="abfb2-227">當您複製並貼上下列程式碼時，請確定複製的程式碼位於與 Main 方法相同的層級。</span><span class="sxs-lookup"><span data-stu-id="abfb2-227">When you copy and paste the following code, make sure that the copied code is at the same level as the Main method.</span></span>

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

15. <span data-ttu-id="abfb2-228">在 [方案總管] 中展開專案 (DataFactoryAPITestApp)，以滑鼠右鍵按一下 [參考]，然後按一下 [新增參考]。</span><span class="sxs-lookup"><span data-stu-id="abfb2-228">In the Solution Explorer, expand the project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="abfb2-229">選取 **System.Configuration** 組件的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="abfb2-229">Select check box for **System.Configuration** assembly.</span></span> <span data-ttu-id="abfb2-230">然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="abfb2-230">and click **OK**.</span></span>
16. <span data-ttu-id="abfb2-231">建置主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="abfb2-231">Build the console application.</span></span> <span data-ttu-id="abfb2-232">按一下功能表上的 [建置]，再按一下 [建置方案]。</span><span class="sxs-lookup"><span data-stu-id="abfb2-232">Click **Build** on the menu and click **Build Solution**.</span></span>
17. <span data-ttu-id="abfb2-233">確認您 Azure Blob 儲存體之 **adftutorial** 容器中至少有一個檔案。</span><span class="sxs-lookup"><span data-stu-id="abfb2-233">Confirm that there is at least one file in the **adftutorial** container in your Azure blob storage.</span></span> <span data-ttu-id="abfb2-234">如果沒有，請在「記事本」中以下列內容建立 **Emp.txt** 檔案，然後將它上傳至 adftutorial 容器。</span><span class="sxs-lookup"><span data-stu-id="abfb2-234">If not, create **Emp.txt** file in Notepad with the following content and upload it to the adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
18. <span data-ttu-id="abfb2-235">按一下功能表上的 [偵錯] -> [開始偵錯]，執行範例。</span><span class="sxs-lookup"><span data-stu-id="abfb2-235">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span></span> <span data-ttu-id="abfb2-236">當您看到 [取得資料配量的執行詳細資料]，請等待數分鐘再按 **ENTER**。</span><span class="sxs-lookup"><span data-stu-id="abfb2-236">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
19. <span data-ttu-id="abfb2-237">使用 Azure 入口網站確認 Data Factory： **APITutorialFactory** 是使用下列成品所建立：</span><span class="sxs-lookup"><span data-stu-id="abfb2-237">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span></span>
   * <span data-ttu-id="abfb2-238">連結服務：**LinkedService_AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="abfb2-238">Linked service: **LinkedService_AzureStorage**</span></span>
   * <span data-ttu-id="abfb2-239">資料集︰**InputDataset** 和 **OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="abfb2-239">Dataset: **InputDataset** and **OutputDataset**.</span></span>
   * <span data-ttu-id="abfb2-240">管線： **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="abfb2-240">Pipeline: **PipelineBlobSample**</span></span>
20. <span data-ttu-id="abfb2-241">確認在指定 Azure SQL Database 的 **emp** 資料表中建立兩筆員工記錄。</span><span class="sxs-lookup"><span data-stu-id="abfb2-241">Verify that the two employee records are created in the **emp** table in the specified Azure SQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="abfb2-242">後續步驟</span><span class="sxs-lookup"><span data-stu-id="abfb2-242">Next steps</span></span>
<span data-ttu-id="abfb2-243">如需適用於 Data Factory 之 .NET API 的完整文件，請參閱 [Data Factory .NET API 參考](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1)。</span><span class="sxs-lookup"><span data-stu-id="abfb2-243">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>

<span data-ttu-id="abfb2-244">在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="abfb2-244">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="abfb2-245">下表提供複製活動所支援作為來源或目的地的資料存放區清單：</span><span class="sxs-lookup"><span data-stu-id="abfb2-245">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="abfb2-246">若要深入了解如何從資料存放區雙向複製資料，請按一下資料表中資料存放區的連結。</span><span class="sxs-lookup"><span data-stu-id="abfb2-246">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>

