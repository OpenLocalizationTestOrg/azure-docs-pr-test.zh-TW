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
ms.openlocfilehash: 52f72da54cdd80691e09d7453bf6730454c4089e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a><span data-ttu-id="5a3a1-103">教學課程：使用 .NET API 建立具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="5a3a1-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5a3a1-104">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="5a3a1-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="5a3a1-105">複製精靈</span><span class="sxs-lookup"><span data-stu-id="5a3a1-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="5a3a1-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5a3a1-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="5a3a1-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a3a1-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="5a3a1-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a3a1-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="5a3a1-109">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="5a3a1-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="5a3a1-110">REST API</span><span class="sxs-lookup"><span data-stu-id="5a3a1-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="5a3a1-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="5a3a1-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="5a3a1-112">在本文中，您將學習如何 toouse [.NET API](https://portal.azure.com) toocreate data factory 管線，將資料從 Azure blob 儲存體 tooan Azure SQL database 複製。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-112">In this article, you learn how toouse [.NET API](https://portal.azure.com) toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="5a3a1-113">如果您是新 tooAzure Data Factory，閱讀 hello[簡介 tooAzure Data Factory](data-factory-introduction.md)發行項，然後再執行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="5a3a1-114">在本教學課程中，您可以建立包含一個活動的管線：複製活動。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="5a3a1-115">hello 複製活動會將資料從支援的資料存放區 tooa 支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="5a3a1-116">如需作為來源和接收區支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="5a3a1-117">hello 活動被提供安全、 可靠且可擴充的方式的各種資料存放區之間的資料可以複製的全域可用服務。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="5a3a1-118">如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="5a3a1-119">一個管線中可以有多個活動。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="5a3a1-120">此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="5a3a1-121">如需詳細資訊，請參閱[管線中的多個活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="5a3a1-122">如需適用於 Data Factory 之 .NET API 的完整文件，請參閱 [Data Factory .NET API 參考](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1)。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-122">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>
> 
> <span data-ttu-id="5a3a1-123">在此教學課程中的 hello 資料管線會將資料從來源資料存放區 tooa 目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-123">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="5a3a1-124">如需如何使用 Azure Data Factory，tootransform 資料，請參閱[教學課程： 建立使用 Hadoop 叢集管線 tootransform 資料](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-124">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a3a1-125">必要條件</span><span class="sxs-lookup"><span data-stu-id="5a3a1-125">Prerequisites</span></span>
* <span data-ttu-id="5a3a1-126">透過移[教學課程的概觀和必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)tooget hello 教學課程和完整 hello 概觀**必要條件**步驟。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-126">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget an overview of hello tutorial and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="5a3a1-127">Visual Studio 2012、2013 或 2015</span><span class="sxs-lookup"><span data-stu-id="5a3a1-127">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="5a3a1-128">下載並安裝 [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="5a3a1-128">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>
* <span data-ttu-id="5a3a1-129">Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-129">Azure PowerShell.</span></span> <span data-ttu-id="5a3a1-130">遵循指示[如何 tooinstall 和設定 Azure PowerShell](../powershell-install-configure.md)文章 tooinstall Azure PowerShell，在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-130">Follow instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="5a3a1-131">您使用 Azure PowerShell toocreate Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-131">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="5a3a1-132">在 Azure Active Directory 中建立應用程式</span><span class="sxs-lookup"><span data-stu-id="5a3a1-132">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="5a3a1-133">建立 Azure Active Directory 應用程式、 建立服務主體針對 hello 應用程式，並將它指派 toohello**資料 Factory 參與者**角色。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-133">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="5a3a1-134">啟動 **PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-134">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="5a3a1-135">執行下列命令的 hello 並輸入 hello 使用者名稱和密碼，您會使用 toosign toohello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="5a3a1-136">執行下列命令 tooview hello 這個帳戶的所有 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-136">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="5a3a1-137">執行下列命令 tooselect hello 訂用帳戶，您想要使用 toowork hello。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="5a3a1-138">取代 **&lt;NameOfAzureSubscription** &gt; hello 的 Azure 訂用帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-138">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="5a3a1-139">記下**SubscriptionId**和**TenantId**從 hello 這個命令的輸出。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-139">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="5a3a1-140">建立 Azure 資源群組名稱為**ADFTutorialResourceGroup**藉由執行下列命令在 hello PowerShell 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-140">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="5a3a1-141">如果已經存在 hello 資源群組，指定是否 tooupdate 它 (Y) 或保留為 (N)。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-141">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="5a3a1-142">如果您使用不同的資源群組，您會在本教學課程需要資源群組來取代 ADFTutorialResourceGroup toouse hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-142">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="5a3a1-143">建立 Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-143">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="5a3a1-144">如果您收到下列錯誤 hello，請指定不同的 URL，然後再次執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-144">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="5a3a1-145">建立 hello AD 服務主體。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-145">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="5a3a1-146">新增服務主體 toohello**資料 Factory 參與者**角色。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-146">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="5a3a1-147">取得 hello 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-147">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="5a3a1-148">記下 hello 輸出中的 hello 應用程式識別碼 (applicationID)。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-148">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="5a3a1-149">您應會從這些步驟取得下列四個值︰</span><span class="sxs-lookup"><span data-stu-id="5a3a1-149">You should have following four values from these steps:</span></span>

* <span data-ttu-id="5a3a1-150">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="5a3a1-150">Tenant ID</span></span>
* <span data-ttu-id="5a3a1-151">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="5a3a1-151">Subscription ID</span></span>
* <span data-ttu-id="5a3a1-152">應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="5a3a1-152">Application ID</span></span>
* <span data-ttu-id="5a3a1-153">（在 hello 第一個命令中指定） 的密碼</span><span class="sxs-lookup"><span data-stu-id="5a3a1-153">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="5a3a1-154">逐步介紹</span><span class="sxs-lookup"><span data-stu-id="5a3a1-154">Walkthrough</span></span>
1. <span data-ttu-id="5a3a1-155">使用 Visual Studio 2012/2013/2015 建立 C# .NET 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-155">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="5a3a1-156">啟動 **Visual Studio** 2012/2013/2015。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-156">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="5a3a1-157">按一下**檔案**，點太**新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-157">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="5a3a1-158">展開 [範本]，然後選取 [Visual C#]。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-158">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="5a3a1-159">在此逐步解說中，您使用的是 C#，但您可以使用任何 .NET 語言。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-159">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="5a3a1-160">選取**主控台應用程式**從 hello hello 右上的專案類型清單。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-160">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="5a3a1-161">輸入**DataFactoryAPITestApp** hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-161">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="5a3a1-162">選取**C:\ADFGetStarted** hello 位置。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-162">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="5a3a1-163">按一下**確定**toocreate hello 專案。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-163">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="5a3a1-164">按一下**工具**，點太**NuGet 套件管理員**，然後按一下**Package Manager Console**。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-164">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="5a3a1-165">在 hello **Package Manager Console**，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="5a3a1-165">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="5a3a1-166">執行下列命令 tooinstall Data Factory 套件 hello:`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="5a3a1-166">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="5a3a1-167">執行下列命令 tooinstall Azure Active Directory 封裝 （使用 Active Directory API hello 程式碼中） 的 hello:`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="5a3a1-167">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="5a3a1-168">新增下列 hello **appSetttings**區段 toohello **App.config**檔案。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-168">Add hello following **appSetttings** section toohello **App.config** file.</span></span> <span data-ttu-id="5a3a1-169">Hello helper 方法會使用這些設定： **GetAuthorizationHeader**。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-169">These settings are used by hello helper method: **GetAuthorizationHeader**.</span></span>

    <span data-ttu-id="5a3a1-170">以您自己的值取代**&lt;應用程式識別碼&gt;**、**&lt;密碼&gt;**、**&lt;訂用帳戶識別碼&gt;****&lt;租用戶識別碼&gt;**的值。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-170">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>

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

5. <span data-ttu-id="5a3a1-171">新增下列 hello**使用**陳述式 toohello 原始程式檔 (Program.cs) hello 專案中的。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-171">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

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

6. <span data-ttu-id="5a3a1-172">新增下列程式碼會建立的執行個體的 hello **DataPipelineManagementClient**類別 toohello **Main**方法。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-172">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="5a3a1-173">您可以使用這個物件 toocreate data factory、 連結的服務、 輸入和輸出資料集和管線。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-173">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="5a3a1-174">您也可以使用這個物件 toomonitor 配量的資料集在執行階段。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-174">You also use this object toomonitor slices of a dataset at runtime.</span></span>

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
   > <span data-ttu-id="5a3a1-175">取代 hello 值**resourceGroupName** hello Azure 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-175">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span>
   >
   > <span data-ttu-id="5a3a1-176">更新的 hello 資料 factory () toobe 唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-176">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="5a3a1-177">Hello data factory 名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-177">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="5a3a1-178">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>

7. <span data-ttu-id="5a3a1-179">新增下列程式碼會建立 hello**資料 factory** toohello **Main**方法。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-179">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

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

    <span data-ttu-id="5a3a1-180">資料處理站可以有一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-180">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="5a3a1-181">其中的管線可以有一或多個活動。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-181">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="5a3a1-182">例如，複製活動 toocopy 資料從來源 tooa 目的地資料存放區和 HDInsight Hive 活動 toorun Hive 指令碼 tootransform 輸入資料 tooproduct 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-182">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="5a3a1-183">讓我們開始在此步驟中建立 hello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-183">Let's start with creating hello data factory in this step.</span></span>
8. <span data-ttu-id="5a3a1-184">新增下列程式碼會建立 hello **Azure 儲存體連結服務**toohello **Main**方法。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-184">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="5a3a1-185">以 Azure 儲存體帳戶的名稱和金鑰取代 **storageaccountname** 和 **accountkey**。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-185">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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

    <span data-ttu-id="5a3a1-186">您可以建立連結的服務中的資料處理站 toolink 資料儲存和運算服務 toohello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-186">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="5a3a1-187">在本教學課程中，您不會使用任何計算服務，例如 Azure HDInsight 或 Azure Data Lake Analytics。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-187">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="5a3a1-188">您可以使用兩種類型的資料存放區：Azure 儲存體 (來源) 和 Azure SQL Database (目的地)。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-188">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

    <span data-ttu-id="5a3a1-189">因此，您可以建立名為 AzureStorageLinkedService 和 AzureSqlLinkedService 的兩個連結服務︰類型為 AzureStorage 和 AzureSqlDatabase。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-189">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

    <span data-ttu-id="5a3a1-190">hello AzureStorageLinkedService 連結您的 Azure 儲存體帳戶 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-190">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="5a3a1-191">這個儲存體帳戶為其中一個 hello 在其中建立容器及 hello 資料上傳的過程[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-191">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
9. <span data-ttu-id="5a3a1-192">新增下列程式碼會建立 hello **Azure SQL 連結服務**toohello **Main**方法。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-192">Add hello following code that creates an **Azure SQL linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="5a3a1-193">以您的 Azure SQL 伺服器名稱、資料庫名稱、使用者和密碼取代 **servername**、**databasename**、**username** **password**。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-193">Replace **servername**, **databasename**, **username**, and **password** with names of your Azure SQL server, database, user, and password.</span></span>

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

    <span data-ttu-id="5a3a1-194">AzureSqlLinkedService 連結您的 Azure SQL database toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-194">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="5a3a1-195">複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-195">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="5a3a1-196">在此資料庫中建立 hello emp 資料表的一部分[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-196">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
10. <span data-ttu-id="5a3a1-197">新增下列程式碼會建立 hello**輸入和輸出資料集**toohello **Main**方法。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-197">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

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
    
    <span data-ttu-id="5a3a1-198">在 hello 先前步驟中，您會建立連結的服務 toolink，您的 Azure 儲存體帳戶和 Azure SQL database tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-198">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="5a3a1-199">在此步驟中，您可以定義名為 InputDataset OutputDataset 代表輸入和輸出資料儲存在 hello 分別 AzureStorageLinkedService 和 AzureSqlLinkedService 所參考的資料存放區中的兩個資料集。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-199">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

    <span data-ttu-id="5a3a1-200">hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-200">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="5a3a1-201">此外，hello 輸入的 blob 資料集 (InputDataset) 指定 hello 容器和包含 hello 輸入的資料的 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-201">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="5a3a1-202">同樣地，hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-202">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="5a3a1-203">此外，hello 輸出 SQL 資料表資料集 (OututDataset) 會指定 hello 資料表中 hello 資料庫 toowhich hello hello blob 儲存體的資料複製。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-203">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

    <span data-ttu-id="5a3a1-204">在此步驟中，您建立資料集名為指向 tooa blob 檔案 (emp.txt) InputDataset hello 的 blob 容器 (adftutorial) 的根資料夾中 hello hello AzureStorageLinkedService 連結服務所代表的 Azure 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-204">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="5a3a1-205">如果您不指定 hello 檔名的值 （或略過它），從 hello 輸入資料夾中的所有 blob 資料，則複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-205">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="5a3a1-206">在本教學課程中，您可以指定 hello 檔案名稱的值。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-206">In this tutorial, you specify a value for hello fileName.</span></span>    

    <span data-ttu-id="5a3a1-207">在此步驟中，您會建立名為 **OutputDataset**的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-207">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="5a3a1-208">此資料集所代表的 hello Azure SQL database 中的點 tooa SQL 資料表**AzureSqlLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-208">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span>
11. <span data-ttu-id="5a3a1-209">新增 hello 下列程式碼的**會建立並啟動管線**toohello **Main**方法。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-209">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="5a3a1-210">在此步驟中您會建立管線，其中含有使用 **InputDataset** 作為輸入和使用 **OutputDataset** 作為輸出的**複製活動**。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-210">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

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

                    // Initial value for pipeline's active period. With this, you won't need tooset slice status
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

    <span data-ttu-id="5a3a1-211">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="5a3a1-211">Note hello following points:</span></span>
   
    - <span data-ttu-id="5a3a1-212">在 [hello 活動] 區段中，沒有一個活動其**類型**設定得**複製**。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-212">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="5a3a1-213">如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-213">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="5a3a1-214">在 Data Factory 解決方案中，您也可以使用[資料轉換活動](data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-214">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="5a3a1-215">輸入 hello 活動設定太**InputDataset**和輸出 hello 活動設定太**OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-215">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="5a3a1-216">在 [hello **typeProperties** ] 區段中， **BlobSource**指定 hello 來源類型為和**SqlSink**指定為 hello 接收器類型。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-216">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="5a3a1-217">支援的 hello 複製活動做為來源與接收的資料存放區的完整清單，請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-217">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="5a3a1-218">toolearn toouse 特定支援的資料如何儲存為來源/接收器，按一下 hello 資料表中的 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-218">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
   
    <span data-ttu-id="5a3a1-219">目前，輸出資料集是哪些磁碟機 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-219">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="5a3a1-220">在本教學課程中，輸出資料集是設定的 tooproduce 配量小時一次。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-220">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="5a3a1-221">hello 管線有開始時間和結束時間的一天分散，也就是 24 小時。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-221">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="5a3a1-222">因此，hello 管線所產生的輸出資料集的 24 配量。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-222">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span>
12. <span data-ttu-id="5a3a1-223">新增下列程式碼 toohello hello **Main**方法 tooget hello 狀態 hello 的資料配量的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-223">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="5a3a1-224">在此範例中只預期有配量。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-224">There is only slice expected in this sample.</span></span>

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

13. <span data-ttu-id="5a3a1-225">新增下列程式碼執行 tooget 詳細資料的資料配量 toohello hello **Main**方法。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-225">Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

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

    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```

14. <span data-ttu-id="5a3a1-226">新增下列 hello 所使用的 helper 方法的 hello **Main**方法 toohello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-226">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5a3a1-227">當您複製並貼上下列程式碼的 hello 時，請確定該 hello 複製程式碼位於相同層級為 hello Main 方法的 hello。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-227">When you copy and paste hello following code, make sure that hello copied code is at hello same level as hello Main method.</span></span>

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

15. <span data-ttu-id="5a3a1-228">在 hello 方案總管 中，展開 hello 專案 (DataFactoryAPITestApp)，以滑鼠右鍵按一下**參考**，然後按一下**加入參考**。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-228">In hello Solution Explorer, expand hello project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="5a3a1-229">選取 **System.Configuration** 組件的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-229">Select check box for **System.Configuration** assembly.</span></span> <span data-ttu-id="5a3a1-230">然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-230">and click **OK**.</span></span>
16. <span data-ttu-id="5a3a1-231">建置 hello 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-231">Build hello console application.</span></span> <span data-ttu-id="5a3a1-232">按一下**建置**hello 功能表，然後按一下上**建置方案**。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-232">Click **Build** on hello menu and click **Build Solution**.</span></span>
17. <span data-ttu-id="5a3a1-233">確認是否有至少一個檔案中 hello **adftutorial**您的 Azure blob 儲存體容器中。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-233">Confirm that there is at least one file in hello **adftutorial** container in your Azure blob storage.</span></span> <span data-ttu-id="5a3a1-234">如果沒有，請建立**Emp.txt**檔案 [記事本] 中以 hello 內容之後，並將它上傳 toohello adftutorial 容器。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-234">If not, create **Emp.txt** file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
18. <span data-ttu-id="5a3a1-235">按一下以執行 hello 範例**偵錯** -> **開始偵錯**hello 功能表上。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-235">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="5a3a1-236">當您看到 hello**正在執行的資料配量的詳細資料**，等待幾分鐘，然後按**ENTER**。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-236">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
19. <span data-ttu-id="5a3a1-237">使用 Azure 入口網站 tooverify hello 該 hello 資料 factory **APITutorialFactory**建立以 hello 下列成品：</span><span class="sxs-lookup"><span data-stu-id="5a3a1-237">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
   * <span data-ttu-id="5a3a1-238">連結服務：**LinkedService_AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="5a3a1-238">Linked service: **LinkedService_AzureStorage**</span></span>
   * <span data-ttu-id="5a3a1-239">資料集︰**InputDataset** 和 **OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-239">Dataset: **InputDataset** and **OutputDataset**.</span></span>
   * <span data-ttu-id="5a3a1-240">管線： **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="5a3a1-240">Pipeline: **PipelineBlobSample**</span></span>
20. <span data-ttu-id="5a3a1-241">確認 hello 兩個員工記錄建立於 hello **emp** hello 中的資料表指定 Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-241">Verify that hello two employee records are created in hello **emp** table in hello specified Azure SQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a3a1-242">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a3a1-242">Next steps</span></span>
<span data-ttu-id="5a3a1-243">如需適用於 Data Factory 之 .NET API 的完整文件，請參閱 [Data Factory .NET API 參考](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1)。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-243">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>

<span data-ttu-id="5a3a1-244">在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-244">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="5a3a1-245">hello 下表提供 hello 複製活動支援做為來源和目的地資料存放區的清單：</span><span class="sxs-lookup"><span data-stu-id="5a3a1-245">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="5a3a1-246">關於如何 toocopy 資料，從資料存放區，toolearn 按一下 hello 連結 hello hello 資料表中的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="5a3a1-246">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>

