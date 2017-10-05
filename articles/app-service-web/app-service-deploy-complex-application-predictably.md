---
title: "透過可預測方式在 Azure 中佈建和部署微服務"
description: "學習如何在 Azure App Service 中將包含微服務的應用程式佈建和部署為單一單位，並且使用 JSON 資源群組範本和 PowerShell 指令碼為可預測的方式。"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: bb51e565-e462-4c60-929a-2ff90121f41d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2016
ms.author: cephalin
ms.openlocfilehash: 844f42e61ba443a4b74a52f622113e87a7781913
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="provision-and-deploy-microservices-predictably-in-azure"></a><span data-ttu-id="3fa45-103">透過可預測方式在 Azure 中佈建和部署微服務</span><span class="sxs-lookup"><span data-stu-id="3fa45-103">Provision and deploy microservices predictably in Azure</span></span>
<span data-ttu-id="3fa45-104">本教學課程示範如何在 [Azure App Service](/services/app-service/) 中將包含[微服務](https://en.wikipedia.org/wiki/Microservices)的應用程式佈建和部署為單一單位，並且使用 JSON 資源群組範本和 PowerShell 指令碼的可預測方式。</span><span class="sxs-lookup"><span data-stu-id="3fa45-104">This tutorial shows how to provision and deploy an application composed of [microservices](https://en.wikipedia.org/wiki/Microservices) in [Azure App Service](/services/app-service/) as a single unit and in a predictable manner using JSON resource group templates and PowerShell scripting.</span></span> 

<span data-ttu-id="3fa45-105">佈建和部署包含高低耦合微服務的高級別應用程式時，重複性和可預測性是成功的重要關鍵。</span><span class="sxs-lookup"><span data-stu-id="3fa45-105">When provisioning and deploying high-scale applications that are composed of highly decoupled microservices, repeatability and predictability are crucial to success.</span></span> <span data-ttu-id="3fa45-106">[Azure App Service](/services/app-service/) 可讓您建立微服務，其中包括 Web 應用程式、行動應用程式、API 應用程式和邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fa45-106">[Azure App Service](/services/app-service/) enables you to create microservices that include web apps, mobile apps, API apps, and logic apps.</span></span> <span data-ttu-id="3fa45-107">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 可讓您將所有微服務當成一個單位來進行管理，以及管理資源相依性 (例如資料庫和原始檔控制設定)。</span><span class="sxs-lookup"><span data-stu-id="3fa45-107">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you to manage all the microservices as a unit, together with resource dependencies such as database and source control settings.</span></span> <span data-ttu-id="3fa45-108">現在，您也可以使用 JSON 範本和簡單 PowerShell 指令碼來部署這類應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fa45-108">Now, you can also deploy such an application using JSON templates and simple PowerShell scripting.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="3fa45-109">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="3fa45-109">What you will do</span></span>
<span data-ttu-id="3fa45-110">在教學課程中，您將部署的應用程式包括：</span><span class="sxs-lookup"><span data-stu-id="3fa45-110">In the tutorial, you will deploy an application that includes:</span></span>

* <span data-ttu-id="3fa45-111">兩個 Web 應用程式 (即兩個微服務)</span><span class="sxs-lookup"><span data-stu-id="3fa45-111">Two web apps (i.e. two microservices)</span></span>
* <span data-ttu-id="3fa45-112">後端 SQL Database</span><span class="sxs-lookup"><span data-stu-id="3fa45-112">A backend SQL Database</span></span>
* <span data-ttu-id="3fa45-113">應用程式設定、連接字串和原始檔控制</span><span class="sxs-lookup"><span data-stu-id="3fa45-113">App settings, connection strings, and source control</span></span>
* <span data-ttu-id="3fa45-114">Application insights、警示、自動調整設定</span><span class="sxs-lookup"><span data-stu-id="3fa45-114">Application insights, alerts, autoscaling settings</span></span>

## <a name="tools-you-will-use"></a><span data-ttu-id="3fa45-115">將使用的工具</span><span class="sxs-lookup"><span data-stu-id="3fa45-115">Tools you will use</span></span>
<span data-ttu-id="3fa45-116">在本教學課程中，您將使用下列工具。</span><span class="sxs-lookup"><span data-stu-id="3fa45-116">In this tutorial, you will use the following tools.</span></span> <span data-ttu-id="3fa45-117">這不是工具的完整討論，因此將著重在端對端案例，並且只對每個工具進行簡短介紹，以及您可以在哪裡找到更多資訊。</span><span class="sxs-lookup"><span data-stu-id="3fa45-117">Since it’s not comprehensive discussion on tools, I’m going to stick to the end-to-end scenario and just give you a brief intro to each, and where you can find more information on it.</span></span> 

### <a name="azure-resource-manager-templates-json"></a><span data-ttu-id="3fa45-118">Azure 資源管理員範本 (JSON)</span><span class="sxs-lookup"><span data-stu-id="3fa45-118">Azure Resource Manager templates (JSON)</span></span>
<span data-ttu-id="3fa45-119">例如，每次在 Azure App Service 中建立 Web 應用程式時，Azure 資源管理員都會使用 JSON 範本來建立具有元件資源的整個資源群組。</span><span class="sxs-lookup"><span data-stu-id="3fa45-119">Every time you create a web app in Azure App Service, for example, Azure Resource Manager uses a JSON template to create the entire resource group with the component resources.</span></span> <span data-ttu-id="3fa45-120">來自 [Azure Marketplace](/marketplace) 的複雜範本 (例如 [Scalable WordPress](/marketplace/partners/wordpress/scalablewordpress/) 應用程式) 可以包括 MySQL 資料庫、儲存體帳戶、App Service 方案、Web 應用程式本身、警示規則、應用程式設定、自動調整設定等，而且您可以透過 PowerShell 使用所有這些範本。</span><span class="sxs-lookup"><span data-stu-id="3fa45-120">A complex template from the [Azure Marketplace](/marketplace) like the [Scalable WordPress](/marketplace/partners/wordpress/scalablewordpress/) app can include the MySQL database, storage accounts, the App Service plan, the web app itself, alert rules, app settings, autoscale settings, and more, and all these templates are available to you through PowerShell.</span></span> <span data-ttu-id="3fa45-121">如需如何下載和使用這些範本的詳細資訊，請參閱 [搭配使用 Azure PowerShell 與 Azure 資源管理員](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="3fa45-121">For information on how to download and use these templates, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="3fa45-122">如需 Azure 資源管理員範本的詳細資訊，請參閱 [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="3fa45-122">For more information on the Azure Resource Manager templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

### <a name="azure-sdk-26-for-visual-studio"></a><span data-ttu-id="3fa45-123">Azure SDK 2.6 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3fa45-123">Azure SDK 2.6 for Visual Studio</span></span>
<span data-ttu-id="3fa45-124">最新 SDK 已增強 JSON 編輯器中的資源管理員範本支援。</span><span class="sxs-lookup"><span data-stu-id="3fa45-124">The newest SDK contains improvements to the Resource Manager template support in the JSON editor.</span></span> <span data-ttu-id="3fa45-125">您可以使用此項快速從頭開始建立資源群組範本，或開啟現有 JSON 範本 (例如已下載的資源庫範本) 進行修改、填入參數檔案，甚至直接從 Azure 資源群組方案部署資源群組。</span><span class="sxs-lookup"><span data-stu-id="3fa45-125">You can use this to quickly create a resource group template from scratch or open an existing JSON template (such as a downloaded gallery template) for modification, populate the parameters file, and even deploy the resource group directly from an Azure Resource Group solution.</span></span>

<span data-ttu-id="3fa45-126">如需詳細資訊，請參閱 [Azure SDK 2.6 for Visual Studio](https://azure.microsoft.com/blog/2015/04/29/announcing-the-azure-sdk-2-6-for-net/)。</span><span class="sxs-lookup"><span data-stu-id="3fa45-126">For more information, see [Azure SDK 2.6 for Visual Studio](https://azure.microsoft.com/blog/2015/04/29/announcing-the-azure-sdk-2-6-for-net/).</span></span>

### <a name="azure-powershell-080-or-later"></a><span data-ttu-id="3fa45-127">Azure PowerShell 0.8.0 或更新版本</span><span class="sxs-lookup"><span data-stu-id="3fa45-127">Azure PowerShell 0.8.0 or later</span></span>
<span data-ttu-id="3fa45-128">自 0.8.0 版開始，Azure PowerShell 安裝除了 Azure 模組之外還包括 Azure 資源管理員模組。</span><span class="sxs-lookup"><span data-stu-id="3fa45-128">Beginning in version 0.8.0, the Azure PowerShell installation includes the Azure Resource Manager module in addition to the Azure module.</span></span> <span data-ttu-id="3fa45-129">這個新模組可讓您編寫資源群組部署的指令碼。</span><span class="sxs-lookup"><span data-stu-id="3fa45-129">This new module enables you to script the deployment of resource groups.</span></span>

<span data-ttu-id="3fa45-130">如需詳細資訊，請參閱 [搭配使用 Azure PowerShell 與 Azure 資源管理員](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="3fa45-130">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>

### <a name="azure-resource-explorer"></a><span data-ttu-id="3fa45-131">Azure 資源總管</span><span class="sxs-lookup"><span data-stu-id="3fa45-131">Azure Resource Explorer</span></span>
<span data-ttu-id="3fa45-132">此[預覽工具](https://resources.azure.com)可讓您瀏覽您的訂用帳戶與個別資源中的所有資源群組的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="3fa45-132">This [preview tool](https://resources.azure.com) enables you to explore the JSON definitions of all the resource groups in your subscription and the individual resources.</span></span> <span data-ttu-id="3fa45-133">在此工具中，您可以編輯資源的 JSON 定義、刪除整個階層的資源，以及建立新的資源。</span><span class="sxs-lookup"><span data-stu-id="3fa45-133">In the tool, you can edit the JSON definitions of a resource, delete an entire hierarchy of resources, and create new resources.</span></span>  <span data-ttu-id="3fa45-134">此工具中立即可用的資訊對於範本撰寫十分有用，因為它會顯示您需要針對特定類型的資源所設定的屬性、正確值等。您甚至可以在 [Azure 入口網站](https://portal.azure.com/)中建立資源群組，然後在總管工具中檢查其 JSON 定義，協助您建立資源群組的樣本。</span><span class="sxs-lookup"><span data-stu-id="3fa45-134">The information readily available in this tool is very helpful for template authoring because it shows you what properties you need to set for a particular type of resource, the correct values, etc. You can even create your resource group in the [Azure Portal](https://portal.azure.com/), then inspect its JSON definitions in the explorer tool to help you templatize the resource group.</span></span>

### <a name="deploy-to-azure-button"></a><span data-ttu-id="3fa45-135">部署至 Azure 按鈕</span><span class="sxs-lookup"><span data-stu-id="3fa45-135">Deploy to Azure button</span></span>
<span data-ttu-id="3fa45-136">如果您使用 GitHub 進行原始檔控制，則可以將 [部署至 Azure 按鈕](https://azure.microsoft.com/blog/2014/11/13/deploy-to-azure-button-for-azure-websites-2/) 放入 README.MD，而此檔案會啟用 Azure 的轉換金鑰部署 UI。</span><span class="sxs-lookup"><span data-stu-id="3fa45-136">If you use GitHub for source control, you can put a [Deploy to Azure button](https://azure.microsoft.com/blog/2014/11/13/deploy-to-azure-button-for-azure-websites-2/) into your README.MD, which enables a turn-key deployment UI to Azure.</span></span> <span data-ttu-id="3fa45-137">雖然您可以針對任何簡單 Web 應用程式執行這項作業，但是您可以將 azuredeploy.json 檔案放在儲存機制根目錄中，以擴充此項來啟用部署整個資源群組。</span><span class="sxs-lookup"><span data-stu-id="3fa45-137">While you can do this for any simple web app, you can extend this to enable deploying an entire resource group by putting an azuredeploy.json file in the repository root.</span></span> <span data-ttu-id="3fa45-138">此 JSON 檔案包含資源群組範本，將供 [部署至 Azure] 按鈕用來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="3fa45-138">This JSON file, which contains the resource group template, will be used by the Deploy to Azure button to create the resource group.</span></span> <span data-ttu-id="3fa45-139">如需範例，請參閱將在本教學課程中使用的 [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 範例。</span><span class="sxs-lookup"><span data-stu-id="3fa45-139">For an example, see the [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) sample, which you will use in this tutorial.</span></span>

## <a name="get-the-sample-resource-group-template"></a><span data-ttu-id="3fa45-140">取得範例資源群組範本</span><span class="sxs-lookup"><span data-stu-id="3fa45-140">Get the sample resource group template</span></span>
<span data-ttu-id="3fa45-141">因此，現在讓我們著手進行。</span><span class="sxs-lookup"><span data-stu-id="3fa45-141">So now let’s get right to it.</span></span>

1. <span data-ttu-id="3fa45-142">巡覽至 [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) App Service 範例。</span><span class="sxs-lookup"><span data-stu-id="3fa45-142">Navigate to the [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) App Service sample.</span></span>
2. <span data-ttu-id="3fa45-143">在 readme.md 中，按一下 [ **部署至 Azure**]。</span><span class="sxs-lookup"><span data-stu-id="3fa45-143">In readme.md, click **Deploy to Azure**.</span></span>
3. <span data-ttu-id="3fa45-144">您會進入 [deploy-to-azure](https://deploy.azure.com) 網站，並要求您輸入部署參數。</span><span class="sxs-lookup"><span data-stu-id="3fa45-144">You’re taken to the [deploy-to-azure](https://deploy.azure.com) site and asked to input deployment parameters.</span></span> <span data-ttu-id="3fa45-145">請注意，大部分的欄位都會填入儲存機制名稱以及一些隨機字串。</span><span class="sxs-lookup"><span data-stu-id="3fa45-145">Notice that most of the fields are populated with the repository name and some random strings for you.</span></span> <span data-ttu-id="3fa45-146">您可以視需要變更所有欄位，但唯一必須輸入的項目是 SQL Server 管理登入和密碼，然後按 [ **下一步**]。</span><span class="sxs-lookup"><span data-stu-id="3fa45-146">You can change all the fields if you want, but the only things you have to enter are the SQL Server administrative login and the password, then click **Next**.</span></span>
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-1-deploybuttonui.png)
4. <span data-ttu-id="3fa45-147">接著，按一下 [ **部署** ] 啟動部署程序。</span><span class="sxs-lookup"><span data-stu-id="3fa45-147">Next, click **Deploy** to start the deployment process.</span></span> <span data-ttu-id="3fa45-148">程序執行並完成之後，請按一下 http://todoapp*XXXX*.azurewebsites.net 連結來瀏覽已部署的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fa45-148">Once the process runs to completion, click the http://todoapp*XXXX*.azurewebsites.net link to browse the deployed application.</span></span> 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-2-deployprogress.png)
   
   <span data-ttu-id="3fa45-149">在您第一次瀏覽至 UI 時，UI 會比較慢，因為應用程式剛剛啟動，但確信它是功能完整的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fa45-149">The UI would be a little slow when you first browse to it because the apps are just starting up, but convince yourself that it’s a fully-functional application.</span></span>
5. <span data-ttu-id="3fa45-150">回到 [部署] 頁面，並按一下 [管理]  連結，以在 Azure 入口網站中查看新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fa45-150">Back in the Deploy page, click the **Manage** link to see the new application in the Azure Portal.</span></span>
6. <span data-ttu-id="3fa45-151">在 [ **Essentials** ] 下拉式清單中，按一下 [資源群組] 連結。</span><span class="sxs-lookup"><span data-stu-id="3fa45-151">In the **Essentials** dropdown, click the resource group link.</span></span> <span data-ttu-id="3fa45-152">也請注意 Web 應用程式已連線至 [ **外部專案**] 下的 GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="3fa45-152">Note also that the web app is already connected to the GitHub repository under **External Project**.</span></span> 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-3-portalresourcegroup.png)
7. <span data-ttu-id="3fa45-153">在資源群組刀鋒視窗中，請注意，資源群組中已經有兩個 Web 應用程式和一個 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="3fa45-153">In the resource group blade, note that there are already two web apps and one SQL Database in the resource group.</span></span>
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-4-portalresourcegroupclicked.png)

<span data-ttu-id="3fa45-154">剛剛您在短短幾分鐘內看到的所有項目都是完整部署的雙微服務應用程式，以及所有元件、相依性、設定、資料庫和連續發行 (由 Azure 資源管理員中的自動化協調流程所設定)。</span><span class="sxs-lookup"><span data-stu-id="3fa45-154">Everything that you just saw in a few short minutes is a fully deployed two-microservice application, with all the components, dependencies, settings, database, and continuous publishing, set up by an automated orchestration in Azure Resource Manager.</span></span> <span data-ttu-id="3fa45-155">這項作業是透過兩件事完成：</span><span class="sxs-lookup"><span data-stu-id="3fa45-155">All this was done by two things:</span></span>

* <span data-ttu-id="3fa45-156">[部署至 Azure] 按鈕</span><span class="sxs-lookup"><span data-stu-id="3fa45-156">The Deploy to Azure button</span></span>
* <span data-ttu-id="3fa45-157">儲存機制根目錄中的 azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="3fa45-157">azuredeploy.json in the repo root</span></span>

<span data-ttu-id="3fa45-158">您可以部署這個相同的應用程式數十次、數百次或數千次，而且每次的組態都完全相同。</span><span class="sxs-lookup"><span data-stu-id="3fa45-158">You can deploy this same application tens, hundreds, or thousands of times and have the exact same configuration every time.</span></span> <span data-ttu-id="3fa45-159">這種方法的重複性和可預測性可讓您輕鬆並自信地部署高延展性應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fa45-159">The repeatability and the predictability of this approach enables you to deploy high-scale applications with ease and confidence.</span></span>

## <a name="examine-or-edit-azuredeployjson"></a><span data-ttu-id="3fa45-160">檢查 (或編輯) AZUREDEPLOY.JSON</span><span class="sxs-lookup"><span data-stu-id="3fa45-160">Examine (or edit) AZUREDEPLOY.JSON</span></span>
<span data-ttu-id="3fa45-161">現在，讓我們看看已如何設定 GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="3fa45-161">Now let’s look at how the GitHub repository was set up.</span></span> <span data-ttu-id="3fa45-162">您將使用 Azure .NET SDK 中的 JSON 編輯器，因此，如果尚未安裝 [Azure .NET SDK 2.6](/downloads/)，請立即安裝。</span><span class="sxs-lookup"><span data-stu-id="3fa45-162">You will be using the JSON editor in the Azure .NET SDK, so if you haven’t already installed [Azure .NET SDK 2.6](/downloads/), do it now.</span></span>

1. <span data-ttu-id="3fa45-163">使用慣用的 git 工具複製 [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="3fa45-163">Clone the [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository using your favorite git tool.</span></span> <span data-ttu-id="3fa45-164">在下面的螢幕擷取畫面中，我將在 Visual Studio 2013 的 Team Explorer 中中進行這項作業。</span><span class="sxs-lookup"><span data-stu-id="3fa45-164">In the screenshot below, I’m doing this in the Team Explorer in Visual Studio 2013.</span></span>
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-1-vsclone.png)
2. <span data-ttu-id="3fa45-165">在 Visual Studio 中，從儲存機制根目錄中開啟 azuredeploy.json。</span><span class="sxs-lookup"><span data-stu-id="3fa45-165">From the repository root, open azuredeploy.json in Visual Studio.</span></span> <span data-ttu-id="3fa45-166">如果您看不到 [JSON 大綱] 窗格，則需要安裝 Azure .NET SDK。</span><span class="sxs-lookup"><span data-stu-id="3fa45-166">If you don’t see the JSON Outline pane, you need to install Azure .NET SDK.</span></span>
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-2-vsjsoneditor.png)

<span data-ttu-id="3fa45-167">我不打算詳述 JSON 格式，但是 [其他資源](#resources) 小節具有了解資源群組範本語言的連結。</span><span class="sxs-lookup"><span data-stu-id="3fa45-167">I’m not going to describe every detail of the JSON format, but the [More Resources](#resources) section has links for learning the resource group template language.</span></span> <span data-ttu-id="3fa45-168">在這裡，我只會說明可協助您開始建立專屬自訂範本以進行應用程式部署的有趣功能。</span><span class="sxs-lookup"><span data-stu-id="3fa45-168">Here, I’m just going to show you the interesting features that can help you get started in making your own custom template for app deployment.</span></span>

### <a name="parameters"></a><span data-ttu-id="3fa45-169">參數</span><span class="sxs-lookup"><span data-stu-id="3fa45-169">Parameters</span></span>
<span data-ttu-id="3fa45-170">查看 parameters 區段，了解大部分這些參數都是 [ **部署至 Azure** ] 按鈕提示您輸入的參數。</span><span class="sxs-lookup"><span data-stu-id="3fa45-170">Take a look at the parameters section to see that most of these parameters are what the **Deploy to Azure** button prompts you to input.</span></span> <span data-ttu-id="3fa45-171">[ **部署至 Azure** ] 按鈕後面的網站會使用 azuredeploy.json 中所定義的參數來填入輸入 UI。</span><span class="sxs-lookup"><span data-stu-id="3fa45-171">The site behind the **Deploy to Azure** button populates the input UI using the parameters defined in azuredeploy.json.</span></span> <span data-ttu-id="3fa45-172">這些參數用於整個資源定義 (例如資源名稱、屬性值等)。</span><span class="sxs-lookup"><span data-stu-id="3fa45-172">These parameters are used throughout the resource definitions, such as resource names, property values, etc.</span></span>

### <a name="resources"></a><span data-ttu-id="3fa45-173">資源</span><span class="sxs-lookup"><span data-stu-id="3fa45-173">Resources</span></span>
<span data-ttu-id="3fa45-174">在 resources 節點中，您可以看到已定義 4 個最上層資源，包括 SQL Server 執行個體、App Service 方案和兩個 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fa45-174">In the resources node, you can see that 4 top-level resources are defined, including a SQL Server instance, an App Service plan, and two web apps.</span></span> 

#### <a name="app-service-plan"></a><span data-ttu-id="3fa45-175">App Service 方案</span><span class="sxs-lookup"><span data-stu-id="3fa45-175">App Service plan</span></span>
<span data-ttu-id="3fa45-176">讓我們從 JSON 中的簡單根層級資源開始。</span><span class="sxs-lookup"><span data-stu-id="3fa45-176">Let’s start with a simple root-level resource in the JSON.</span></span> <span data-ttu-id="3fa45-177">在 [JSON 大綱] 中，按一下名為 **[hostingPlanName]** 的 App Service 方案反白顯示對應的 JSON 程式碼。</span><span class="sxs-lookup"><span data-stu-id="3fa45-177">In the JSON Outline, click the App Service plan named **[hostingPlanName]** to highlight the corresponding JSON code.</span></span> 

![](./media/app-service-deploy-complex-application-predictably/examinejson-3-appserviceplan.png)

<span data-ttu-id="3fa45-178">請注意， `type` 項目指定 App Service 方案 (很久以前稱為伺服器陣列) 的字串，並會使用 JSON 檔案中所定義的參數來填寫其他項目和屬性，而且此資源沒有任何巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="3fa45-178">Note that the `type` element specifies the string for an App Service plan (it was called a server farm a long, long time ago), and other elements and properties are filled in using the parameters defined in the JSON file, and this resource doesn’t have any nested resources.</span></span>

> [!NOTE]
> <span data-ttu-id="3fa45-179">也請注意，`apiVersion` 的值告訴 Azure 搭配使用哪一個版本的 REST API 與 JSON 資源定義，而且可能會影響資源在 `{}` 內的格式。</span><span class="sxs-lookup"><span data-stu-id="3fa45-179">Note also that the value of `apiVersion` tells Azure which version of the REST API to use the JSON resource definition with, and it can affect how the resource should be formatted inside the `{}`.</span></span> 
> 
> 

#### <a name="sql-server"></a><span data-ttu-id="3fa45-180">SQL Server</span><span class="sxs-lookup"><span data-stu-id="3fa45-180">SQL Server</span></span>
<span data-ttu-id="3fa45-181">接下來，按一下 [JSON 大綱] 中名為 **SQLServer** 的 SQL Server 資源。</span><span class="sxs-lookup"><span data-stu-id="3fa45-181">Next, click on the SQL Server resource named **SQLServer** in the JSON Outline.</span></span>

![](./media/app-service-deploy-complex-application-predictably/examinejson-4-sqlserver.png)

<span data-ttu-id="3fa45-182">請注意反白顯示 JSON 程式碼的下列資訊：</span><span class="sxs-lookup"><span data-stu-id="3fa45-182">Note the following about the highlighted JSON code:</span></span>

* <span data-ttu-id="3fa45-183">參數的使用確保透過讓所建立的資源彼此一致的方式來命名和設定所建立的資源。</span><span class="sxs-lookup"><span data-stu-id="3fa45-183">The use of parameters ensures that the created resources are named and configured in a way that makes them consistent with one another.</span></span>
* <span data-ttu-id="3fa45-184">SQLServer 資源有兩個巢狀資源，其各有不同的 `type` 值。</span><span class="sxs-lookup"><span data-stu-id="3fa45-184">The SQLServer resource has two nested resources, each has a different value for `type`.</span></span>
* <span data-ttu-id="3fa45-185">`“resources”: […]` 內巢狀資源 (其中已定義資料庫和防火牆規則) 的 `dependsOn` 項目指定根層級 SQLServer 資源的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="3fa45-185">The nested resources inside `“resources”: […]`, where the database and the firewall rules are defined, have a `dependsOn` element that specifies the resource ID of the root-level SQLServer resource.</span></span> <span data-ttu-id="3fa45-186">這會告訴 Azure 資源管理員：「建立此資源之前，那個其他資源必須已經存在；如果那個其他資源定義在範本中，則請先建立它」。</span><span class="sxs-lookup"><span data-stu-id="3fa45-186">This tells Azure Resource Manager, “before you create this resource, that other resource must already exist; and if that other resource is defined in the template, then create that one first”.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="3fa45-187">如需如何使用 `resourceId()` 函式的詳細資訊，請參閱 [Azure Resource Manager 範本函式](../azure-resource-manager/resource-group-template-functions-resource.md#resourceid)。</span><span class="sxs-lookup"><span data-stu-id="3fa45-187">For detailed information on how to use the `resourceId()` function, see [Azure Resource Manager Template Functions](../azure-resource-manager/resource-group-template-functions-resource.md#resourceid).</span></span>
  > 
  > 
* <span data-ttu-id="3fa45-188">`dependsOn` 項目的作用是 Azure 資源管理員可以知道可平行建立哪些資源，以及必須依序建立哪些資源。</span><span class="sxs-lookup"><span data-stu-id="3fa45-188">The effect of the `dependsOn` element is that Azure Resource Manager can know which resources can be created in parallel and which resources must be created sequentially.</span></span> 

#### <a name="web-app"></a><span data-ttu-id="3fa45-189">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="3fa45-189">Web app</span></span>
<span data-ttu-id="3fa45-190">現在，讓我們繼續討論更為複雜的實際 Web 應用程式本身。</span><span class="sxs-lookup"><span data-stu-id="3fa45-190">Now, let’s move on to the actual web apps themselves, which are more complicated.</span></span> <span data-ttu-id="3fa45-191">按一下 [ JSON 大綱] 中的 [variables(‘apiSiteName’)] Web 應用程式，以反白顯示其 JSON 程式碼。</span><span class="sxs-lookup"><span data-stu-id="3fa45-191">Click the [variables(‘apiSiteName’)] web app in the JSON Outline to highlight its JSON code.</span></span> <span data-ttu-id="3fa45-192">您會發現事情變得越來越有趣。</span><span class="sxs-lookup"><span data-stu-id="3fa45-192">You’ll notice that things are getting much more interesting.</span></span> <span data-ttu-id="3fa45-193">因此，我將逐一討論所有功能：</span><span class="sxs-lookup"><span data-stu-id="3fa45-193">For this purpose, I’ll talk about the features one by one:</span></span>

##### <a name="root-resource"></a><span data-ttu-id="3fa45-194">根資源</span><span class="sxs-lookup"><span data-stu-id="3fa45-194">Root resource</span></span>
<span data-ttu-id="3fa45-195">Web 應用程式與兩個不同的資源相依。</span><span class="sxs-lookup"><span data-stu-id="3fa45-195">The web app depends on two different resources.</span></span> <span data-ttu-id="3fa45-196">這表示只有在建立 App Service 方案和 SQL Server 執行個體之後，Azure 資源管理員才會建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fa45-196">This means that Azure Resource Manager will create the web app only after both the App Service plan and the SQL Server instance are created.</span></span>

![](./media/app-service-deploy-complex-application-predictably/examinejson-5-webapproot.png)

##### <a name="app-settings"></a><span data-ttu-id="3fa45-197">應用程式設定</span><span class="sxs-lookup"><span data-stu-id="3fa45-197">App settings</span></span>
<span data-ttu-id="3fa45-198">應用程式設定也會定義為巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="3fa45-198">The app settings are also defined as a nested resource.</span></span>

![](./media/app-service-deploy-complex-application-predictably/examinejson-6-webappsettings.png)

<span data-ttu-id="3fa45-199">在 `config/appsettings` 的 `properties` 項目中，您會有兩個格式為 `“<name>” : “<value>”` 的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="3fa45-199">In the `properties` element for `config/appsettings`, you have two app settings in the format `“<name>” : “<value>”`.</span></span>

* <span data-ttu-id="3fa45-200">`PROJECT` 是 [KUDU 設定](https://github.com/projectkudu/kudu/wiki/Customizing-deployments) ，告訴 Azure 部署在多專案 Visual Studio 方案中使用哪個專案。</span><span class="sxs-lookup"><span data-stu-id="3fa45-200">`PROJECT` is a [KUDU setting](https://github.com/projectkudu/kudu/wiki/Customizing-deployments) that tells Azure deployment which project to use in a multi-project Visual Studio solution.</span></span> <span data-ttu-id="3fa45-201">稍後會示範如何設定原始檔控制，但是，因為 ToDoApp 程式碼是在多專案 Visual Studio 方案中，所以我們需要這項設定。</span><span class="sxs-lookup"><span data-stu-id="3fa45-201">I will show you later how source control is configured, but since the ToDoApp code is in a multi-project Visual Studio solution, we need this setting.</span></span>
* <span data-ttu-id="3fa45-202">`clientUrl` 只是應用程式程式碼所使用的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="3fa45-202">`clientUrl` is simply an app setting that the application code uses.</span></span>

##### <a name="connection-strings"></a><span data-ttu-id="3fa45-203">連接字串</span><span class="sxs-lookup"><span data-stu-id="3fa45-203">Connection strings</span></span>
<span data-ttu-id="3fa45-204">連接字串也會定義為巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="3fa45-204">The connection strings are also defined as a nested resource.</span></span>

![](./media/app-service-deploy-complex-application-predictably/examinejson-7-webappconnstr.png)

<span data-ttu-id="3fa45-205">在 `config/connectionstrings` 的 `properties` 項目中，每個連接字串也會定義為「名稱:值」配對，並且具有特定格式：`“<name>” : {“value”: “…”, “type”: “…”}`。</span><span class="sxs-lookup"><span data-stu-id="3fa45-205">In the `properties` element for `config/connectionstrings`, each connection string is also defined as a name:value pair, with the specific format of `“<name>” : {“value”: “…”, “type”: “…”}`.</span></span> <span data-ttu-id="3fa45-206">針對 `type` 項目，可能的值為 `MySql`、`SQLServer`、`SQLAzure` 和 `Custom`。</span><span class="sxs-lookup"><span data-stu-id="3fa45-206">For the `type` element, possible values are `MySql`, `SQLServer`, `SQLAzure`, and `Custom`.</span></span>

> [!TIP]
> <span data-ttu-id="3fa45-207">如需連接字串型別的限定清單，請在 Azure PowerShell 中執行下列命令：\[Enum]::GetNames("Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.DatabaseType")</span><span class="sxs-lookup"><span data-stu-id="3fa45-207">For a definitive list of the connection string types, run the following command in Azure PowerShell: \[Enum]::GetNames("Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.DatabaseType")</span></span>
> 
> 

##### <a name="source-control"></a><span data-ttu-id="3fa45-208">原始檔控制</span><span class="sxs-lookup"><span data-stu-id="3fa45-208">Source control</span></span>
<span data-ttu-id="3fa45-209">原始檔控制也會定義為巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="3fa45-209">The source control settings are also defined as a nested resource.</span></span> <span data-ttu-id="3fa45-210">Azure 資源管理員使用這項資源來設定持續發佈 (請參閱後面 `IsManualIntegration` 上的警告)，並且在處理 JSON 檔案期間開始自動部署應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="3fa45-210">Azure Resource Manager uses this resource to configure continuous publishing (see caveat on `IsManualIntegration` later) and also to kick off the deployment of application code automatically during the processing of the JSON file.</span></span>

![](./media/app-service-deploy-complex-application-predictably/examinejson-8-webappsourcecontrol.png)

<span data-ttu-id="3fa45-211">`RepoUrl` 和 `branch` 應該相當具直覺式，而且應該指向 Git 儲存機制以及從發佈之分支的名稱。</span><span class="sxs-lookup"><span data-stu-id="3fa45-211">`RepoUrl` and `branch` should be pretty intuitive and should point to the Git repository and the name of the branch to publish from.</span></span> <span data-ttu-id="3fa45-212">同樣地，這些是透過輸入參數所定義。</span><span class="sxs-lookup"><span data-stu-id="3fa45-212">Again, these are defined by input parameters.</span></span> 

<span data-ttu-id="3fa45-213">請注意，在 `dependsOn` 項目，除了 Web 應用程式資源本身之外，`sourcecontrols/web` 也與 `config/appsettings` 和 `config/connectionstrings` 相依。</span><span class="sxs-lookup"><span data-stu-id="3fa45-213">Note in the `dependsOn` element that, in addition to the web app resource itself, `sourcecontrols/web` also depends on `config/appsettings` and `config/connectionstrings`.</span></span> <span data-ttu-id="3fa45-214">原因是設定 `sourcecontrols/web` 之後，Azure 部署程序會自動嘗試部署、建置和啟動應用程式碼。</span><span class="sxs-lookup"><span data-stu-id="3fa45-214">This is because once `sourcecontrols/web` is configured, the Azure deployment process will automatically attempt to deploy, build, and start the application code.</span></span> <span data-ttu-id="3fa45-215">因此，插入此相依性有助於確定在執行應用程式碼之前，應用程式可以存取所需的應用程式設定和連接字串。</span><span class="sxs-lookup"><span data-stu-id="3fa45-215">Therefore, inserting this dependency helps you make sure that the application has access to the required app settings and connection strings before the application code is run.</span></span> 

> [!NOTE]
> <span data-ttu-id="3fa45-216">也請注意，`IsManualIntegration` 設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="3fa45-216">Note also that `IsManualIntegration` is set to `true`.</span></span> <span data-ttu-id="3fa45-217">這個屬性是本教學課程中的必要屬性，因為您實際上未擁有 GitHub 儲存機制，因此無法實際授權 Azure 從 [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 設定持續發佈 (亦即，</span><span class="sxs-lookup"><span data-stu-id="3fa45-217">This property is necessary in this tutorial because you do not actually own the GitHub repository, and thus cannot actually grant permission to Azure to configure continuous publishing from [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) (i.e.</span></span> <span data-ttu-id="3fa45-218">自動推送儲存機制更新至 Azure)。</span><span class="sxs-lookup"><span data-stu-id="3fa45-218">push automatic repository updates to Azure).</span></span> <span data-ttu-id="3fa45-219">只有在之前已在 [Azure 入口網站](https://portal.azure.com/)中設定過擁有者的 GitHub 認證時，才能使用所指定儲存機制的預設值 `false`。</span><span class="sxs-lookup"><span data-stu-id="3fa45-219">You can use the default value `false` for the specified repository only if you have configured the owner’s GitHub credentials in the [Azure portal](https://portal.azure.com/) before.</span></span> <span data-ttu-id="3fa45-220">換句話說，如果您之前已使用使用者認證來設定 [Azure 入口網站](https://portal.azure.com/)中任何應用程式的 GitHub 或 BitBucket 原始檔控制，則 Azure 會記住認證，並在未來從 GitHub 或 BitBucket 部署任何應用程式時使用它們。</span><span class="sxs-lookup"><span data-stu-id="3fa45-220">In other words, if you have set up source control to GitHub or BitBucket for any app in the [Azure Portal](https://portal.azure.com/) previously, using your user credentials, then Azure will remember the credentials and use them whenever you deploy any app from GitHub or BitBucket in the future.</span></span> <span data-ttu-id="3fa45-221">不過，如果您還沒有這麼做，則 Azure 資源管理員嘗試設定 Web 應用程式的原始檔控制設定時，JSON 範本的部署會失敗。因為它無法使用儲存機制擁有者的認證登入 GitHub 或 BitBucket。</span><span class="sxs-lookup"><span data-stu-id="3fa45-221">However, if you haven’t done this already, deployment of the JSON template will fail when Azure Resource Manager tries to configure the web app’s source control settings because it cannot log into GitHub or BitBucket with the repository owner’s credentials.</span></span>
> 
> 

## <a name="compare-the-json-template-with-deployed-resource-group"></a><span data-ttu-id="3fa45-222">比較具有已部署資源群組的 JSON 範本</span><span class="sxs-lookup"><span data-stu-id="3fa45-222">Compare the JSON template with deployed resource group</span></span>
<span data-ttu-id="3fa45-223">您可以在這裡瀏覽 [Azure 入口網站](https://portal.azure.com/)中的所有 Web 應用程式刀鋒視窗，但還有另一個工具十分有用。</span><span class="sxs-lookup"><span data-stu-id="3fa45-223">Here, you can go through all the web app’s blades in the [Azure Portal](https://portal.azure.com/), but there’s another tool that’s just as useful, if not more.</span></span> <span data-ttu-id="3fa45-224">移至 [Azure 資源總管](https://resources.azure.com) 預覽工具，其可提供訂用帳戶中所有資源群組的 JSON 呈現，因為它們實際存在於 Azure 後端。</span><span class="sxs-lookup"><span data-stu-id="3fa45-224">Go to the [Azure Resource Explorer](https://resources.azure.com) preview tool, which gives you a JSON representation of all the resource groups in your subscriptions, as they actually exist in the Azure backend.</span></span> <span data-ttu-id="3fa45-225">您也可以看到 Azure 中資源群組的 JSON 階層如何與用來建立它的範本檔案中的階層對應。</span><span class="sxs-lookup"><span data-stu-id="3fa45-225">You can also see how the resource group’s JSON hierarchy in Azure corresponds with the hierarchy in the template file that’s used to create it.</span></span>

<span data-ttu-id="3fa45-226">例如，移至 [Azure 資源總管](https://resources.azure.com) 工具並展開總管中的節點時，可以看到資源群組以及收集在其個別資源型別下方的根層級資源。</span><span class="sxs-lookup"><span data-stu-id="3fa45-226">For example, when I go to the [Azure Resource Explorer](https://resources.azure.com) tool and expand the nodes in the explorer, I can see the resource group and the root-level resources that are collected under their respective resource types.</span></span>

![](./media/app-service-deploy-complex-application-predictably/ARM-1-treeview.png)

<span data-ttu-id="3fa45-227">如果您向下鑽研至 Web 應用程式，則應該可以看到與下面螢幕擷取畫面類似的 Web 應用程式組態詳細資料：</span><span class="sxs-lookup"><span data-stu-id="3fa45-227">If you drill down to a web app, you should be able to see web app configuration details similar to the below screenshot:</span></span>

![](./media/app-service-deploy-complex-application-predictably/ARM-2-jsonview.png)

<span data-ttu-id="3fa45-228">同樣地，巢狀資源的階層應該與 JSON 範本檔案中的階層極為類似，而且您應該會看到 JSON 窗格中正確反映的應用程式設定、連接字串等。</span><span class="sxs-lookup"><span data-stu-id="3fa45-228">Again, the nested resources should have a hierarchy very similar to those in your JSON template file, and you should see the app settings, connection strings, etc., properly reflected in the JSON pane.</span></span> <span data-ttu-id="3fa45-229">沒有這裡的設定可能表示 JSON 檔案發生問題，並可協助您疑難排解 JSON 範本檔案。</span><span class="sxs-lookup"><span data-stu-id="3fa45-229">The absence of settings here may indicate an issue with your JSON file and can help you troubleshoot your JSON template file.</span></span>

## <a name="deploy-the-resource-group-template-yourself"></a><span data-ttu-id="3fa45-230">自行部署資源群組範本</span><span class="sxs-lookup"><span data-stu-id="3fa45-230">Deploy the resource group template yourself</span></span>
<span data-ttu-id="3fa45-231">[ **部署至 Azure** ] 按鈕不錯，但是，只有在已將 azuredeploy.json 推送至 GitHub 時，它才可讓您在 azuredeploy.json 中部署資源群組範本。</span><span class="sxs-lookup"><span data-stu-id="3fa45-231">The **Deploy to Azure** button is great, but it allows you to deploy the resource group template in azuredeploy.json only if you have already pushed azuredeploy.json to GitHub.</span></span> <span data-ttu-id="3fa45-232">Azure .NET SDK 也提供工具，讓您直接從本機電腦部署任何 JSON 範本檔案。</span><span class="sxs-lookup"><span data-stu-id="3fa45-232">The Azure .NET SDK also provides the tools for you to deploy any JSON template file directly from your local machine.</span></span> <span data-ttu-id="3fa45-233">若要這樣做，請遵循下面的步驟：</span><span class="sxs-lookup"><span data-stu-id="3fa45-233">To do this, follow the steps below:</span></span>

1. <span data-ttu-id="3fa45-234">在 Visual Studio 中，按一下 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="3fa45-234">In Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="3fa45-235">按一下 [Visual C#] > [雲端] > [Azure 資源群組]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="3fa45-235">Click **Visual C#** > **Cloud** > **Azure Resource Group**, then click **OK**.</span></span>
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-1-vsproject.png)
3. <span data-ttu-id="3fa45-236">在 [選取 Azure 範本] 中，選取 [空白範本]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="3fa45-236">In **Select Azure Template**, select **Blank Template** and click **OK**.</span></span>
4. <span data-ttu-id="3fa45-237">將 azuredeploy.json 拖曳至新專案的 [ **樣本** ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="3fa45-237">Drag azuredeploy.json into the **Template** folder of your new project.</span></span>
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-2-copyjson.png)
5. <span data-ttu-id="3fa45-238">從 [方案總管]，開啟複製的 azuredeploy.json。</span><span class="sxs-lookup"><span data-stu-id="3fa45-238">From Solution Explorer, open the copied azuredeploy.json.</span></span>
6. <span data-ttu-id="3fa45-239">按一下 [ **加入資源**]，將一些標準 Application Insight 資源加入 JSON 檔案，但此作業僅供示範之用。</span><span class="sxs-lookup"><span data-stu-id="3fa45-239">Just for the sake of the demonstration, let’s add some standard Application Insight resources to our JSON file, by clicking **Add Resource**.</span></span> <span data-ttu-id="3fa45-240">如果您只想部署 JSON 檔案，請跳至部署步驟。</span><span class="sxs-lookup"><span data-stu-id="3fa45-240">If you’re just interested in deploying the JSON file, skip to the deploy steps.</span></span>
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-3-newresource.png)
7. <span data-ttu-id="3fa45-241">選取 [Web Apps 的 Application Insights]，並確定已選取現有 App Service 方案和 Web 應用程式，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="3fa45-241">Select **Application Insights for Web Apps**, then make sure an existing App Service plan and web app is selected, and then click **Add**.</span></span>
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-4-newappinsight.png)
   
   <span data-ttu-id="3fa45-242">您現在可以看到數個新資源 (根據資源和其作用而定) 與 App Service 方案或 Web 應用程式相依。</span><span class="sxs-lookup"><span data-stu-id="3fa45-242">You’ll now be able to see several new resources that, depending on the resource and what it does, have dependencies on either the App Service plan or the web app.</span></span> <span data-ttu-id="3fa45-243">這些資源不是透過其現有定義所啟用，而您將變更這項行為。</span><span class="sxs-lookup"><span data-stu-id="3fa45-243">These resources are not enabled by their existing definition and you’re going to change that.</span></span>
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-5-appinsightresources.png)
8. <span data-ttu-id="3fa45-244">在 [JSON 大綱] 中，按一下 **appInsights AutoScale** 反白顯示其 JSON 程式碼。</span><span class="sxs-lookup"><span data-stu-id="3fa45-244">In the JSON Outline, click **appInsights AutoScale** to highlight its JSON code.</span></span> <span data-ttu-id="3fa45-245">這是您 App Service 方案的調整設定。</span><span class="sxs-lookup"><span data-stu-id="3fa45-245">This is the scaling setting for your App Service plan.</span></span>
9. <span data-ttu-id="3fa45-246">在反白顯示的 JSON 程式碼中，找到 `location` 和 `enabled` 屬性，並如下所示設定它們。</span><span class="sxs-lookup"><span data-stu-id="3fa45-246">In the highlighted JSON code, locate the `location` and `enabled` properties and set them as shown below.</span></span>
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-6-autoscalesettings.png)
10. <span data-ttu-id="3fa45-247">在 [JSON 大綱] 中，按一下 **CPUHigh appInsights** 反白顯示其 JSON 程式碼。</span><span class="sxs-lookup"><span data-stu-id="3fa45-247">In the JSON Outline, click **CPUHigh appInsights** to highlight its JSON code.</span></span> <span data-ttu-id="3fa45-248">這是警示。</span><span class="sxs-lookup"><span data-stu-id="3fa45-248">This is an alert.</span></span>
11. <span data-ttu-id="3fa45-249">找到 `location` 和 `isEnabled` 屬性，並如下所示設定它們。</span><span class="sxs-lookup"><span data-stu-id="3fa45-249">Locate the `location` and `isEnabled` properties and set them as shown below.</span></span> <span data-ttu-id="3fa45-250">請對其他三個警示 (紫色燈泡) 執行相同的動作。</span><span class="sxs-lookup"><span data-stu-id="3fa45-250">Do the same for the other three alerts (purple bulbs).</span></span>
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-7-alerts.png)
12. <span data-ttu-id="3fa45-251">您現在可以開始進行部署。</span><span class="sxs-lookup"><span data-stu-id="3fa45-251">You’re now ready to deploy.</span></span> <span data-ttu-id="3fa45-252">以滑鼠右鍵按一下專案，然後選取  **部署** > **New 部署ment**。</span><span class="sxs-lookup"><span data-stu-id="3fa45-252">Right-click the project and select **Deploy** > **New Deployment**.</span></span>
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-8-newdeployment.png)
13. <span data-ttu-id="3fa45-253">登入 Azure 帳戶 (如果您尚未這樣做)。</span><span class="sxs-lookup"><span data-stu-id="3fa45-253">Log into your Azure account if you haven’t already done so.</span></span>
14. <span data-ttu-id="3fa45-254">在您的訂用帳戶中選取現有的資源群組，或選取 **azuredeploy.json**，然後按一下 [編輯參數] 建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3fa45-254">Select an existing resource group in your subscription or create a new one, select **azuredeploy.json**, and then click **Edit Parameters**.</span></span>
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-9-deployconfig.png)
    
    <span data-ttu-id="3fa45-255">您現在可以透過好用的資料表編輯範本檔案中定義的所有參數。</span><span class="sxs-lookup"><span data-stu-id="3fa45-255">You’ll now be able to edit all the parameters defined in the template file in a nice table.</span></span> <span data-ttu-id="3fa45-256">定義預設值的參數已經有其預設值，而定義允許值清單的參數則會顯示為下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="3fa45-256">Parameters that define defaults will already have their default values, and parameters that define a list of allowed values will be shown as dropdowns.</span></span>
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-10-parametereditor.png)
15. <span data-ttu-id="3fa45-257">填入所有空的參數，並在 [repoUrl](https://github.com/azure-appservice-samples/ToDoApp.git) 中使用 **GitHub repo address for ToDoApp**。</span><span class="sxs-lookup"><span data-stu-id="3fa45-257">Fill in all the empty parameters, and use the [GitHub repo address for ToDoApp](https://github.com/azure-appservice-samples/ToDoApp.git) in **repoUrl**.</span></span> <span data-ttu-id="3fa45-258">然後按一下 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="3fa45-258">Then, click **Save**.</span></span>
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-11-parametereditorfilled.png)
    
    > [!NOTE]
    > <span data-ttu-id="3fa45-259">自動調整是**標準**層級或更高層級所提供的功能，而計劃層級警示是**基本**層級或更高層級所提供的功能，您需要將 **sku** 參數設為**標準**或**進階**，才能看到所有新的 App Insights 資源都已啟動。</span><span class="sxs-lookup"><span data-stu-id="3fa45-259">Autoscaling is a feature offered in **Standard** tier or higher, and plan-level alerts are features offered in **Basic** tier or higher, you’ll need to set the **sku** parameter to **Standard** or **Premium** in order to see all your new App Insights resources light up.</span></span>
    > 
    > 
16. <span data-ttu-id="3fa45-260">按一下 [ **部署**]。</span><span class="sxs-lookup"><span data-stu-id="3fa45-260">Click **Deploy**.</span></span> <span data-ttu-id="3fa45-261">如果您選取 [儲存密碼]，則會將密碼**以純文字形式**儲存至參數檔。</span><span class="sxs-lookup"><span data-stu-id="3fa45-261">If you selected **Save passwords**, the password will be saved in the parameter file **in plain text**.</span></span> <span data-ttu-id="3fa45-262">否則，系統會在部署過程要求您輸入資料庫密碼。</span><span class="sxs-lookup"><span data-stu-id="3fa45-262">Otherwise, you’ll be asked to input the database password during the deployment process.</span></span>

<span data-ttu-id="3fa45-263">這樣就大功告成了！</span><span class="sxs-lookup"><span data-stu-id="3fa45-263">That’s it!</span></span> <span data-ttu-id="3fa45-264">現在，您只需要移至 [Azure 入口網站](https://portal.azure.com/)和 [Azure 資源總管工具](https://resources.azure.com)，即可查看已新增 JSON 已部署應用程式中的新警示和自動調整設定。</span><span class="sxs-lookup"><span data-stu-id="3fa45-264">Now you just need to go to the [Azure Portal](https://portal.azure.com/) and the [Azure Resource Explorer](https://resources.azure.com) tool to see the new alerts and autoscale settings added to your JSON deployed application.</span></span>

<span data-ttu-id="3fa45-265">您在本節中的步驟主要是完成下列作業：</span><span class="sxs-lookup"><span data-stu-id="3fa45-265">Your steps in this section mainly accomplished the following:</span></span>

1. <span data-ttu-id="3fa45-266">準備範本檔案</span><span class="sxs-lookup"><span data-stu-id="3fa45-266">Prepared the template file</span></span>
2. <span data-ttu-id="3fa45-267">建立要與範本檔案一起使用的參數檔案</span><span class="sxs-lookup"><span data-stu-id="3fa45-267">Created a parameter file to go with the template file</span></span>
3. <span data-ttu-id="3fa45-268">部署具有參數檔案的範本檔案</span><span class="sxs-lookup"><span data-stu-id="3fa45-268">Deployed the template file with the parameter file</span></span>

<span data-ttu-id="3fa45-269">最後一個步驟是透過 PowerShell Cmdlet 輕鬆完成。</span><span class="sxs-lookup"><span data-stu-id="3fa45-269">The last step is easily done by a PowerShell cmdlet.</span></span> <span data-ttu-id="3fa45-270">若要查看 Visual Studio 在部署您的應用程式時所執行的作業，請開啟 Scripts\Deploy-AzureResourceGroup.ps1。</span><span class="sxs-lookup"><span data-stu-id="3fa45-270">To see what Visual Studio did when it deployed your application, open Scripts\Deploy-AzureResourceGroup.ps1.</span></span> <span data-ttu-id="3fa45-271">在該處有很多程式碼，但我只想要討論部署具有參數檔案之範本檔案所需的所有相關程式碼。</span><span class="sxs-lookup"><span data-stu-id="3fa45-271">There’s a lot of code there, but I’m just going to highlight all the pertinent code you need to deploy the template file with the parameter file.</span></span>

![](./media/app-service-deploy-complex-application-predictably/deploy-12-powershellsnippet.png)

<span data-ttu-id="3fa45-272">最後一個 Cmdlet ( `New-AzureResourceGroup`) 是實際執行動作的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3fa45-272">The last cmdlet, `New-AzureResourceGroup`, is the one that actually performs the action.</span></span> <span data-ttu-id="3fa45-273">所有這些動作都是在告訴您，在工具的協助下，透過可預測方式部署您的雲端應用程式相當簡單。</span><span class="sxs-lookup"><span data-stu-id="3fa45-273">All this should demonstrate to you that, with the help of tooling, it is relatively straightforward to deploy your cloud application predictably.</span></span> <span data-ttu-id="3fa45-274">每次對具有相同參數檔案的相同範本執行 Cmdlet 時，結果都會相同。</span><span class="sxs-lookup"><span data-stu-id="3fa45-274">Every time you run the cmdlet on the same template with the same parameter file, you’re going to get the same result.</span></span>

## <a name="summary"></a><span data-ttu-id="3fa45-275">摘要</span><span class="sxs-lookup"><span data-stu-id="3fa45-275">Summary</span></span>
<span data-ttu-id="3fa45-276">在 DevOps 中，重複性和可預測性是任何成功部署包含微服務之高級別應用程式的關鍵。</span><span class="sxs-lookup"><span data-stu-id="3fa45-276">In DevOps, repeatability and predictability are keys to any successful deployment of a high-scale application composed of microservices.</span></span> <span data-ttu-id="3fa45-277">在本教學課程中，您已使用 Azure 資源管理員範本將雙微服務應用程式部署至 Azure 以做為單一資源群組。</span><span class="sxs-lookup"><span data-stu-id="3fa45-277">In this tutorial, you have deployed a two-microservice application to Azure as a single resource group using the Azure Resource Manager template.</span></span> <span data-ttu-id="3fa45-278">希望這可讓您了解如何開始將 Azure 中的應用程式轉換成範本，而且可以透過可預測方式進行佈建和部署。</span><span class="sxs-lookup"><span data-stu-id="3fa45-278">Hopefully, it has given you the knowledge you need in order to start converting your application in Azure into a template and can provision and deploy it predictably.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3fa45-279">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3fa45-279">Next Steps</span></span>
<span data-ttu-id="3fa45-280">了解如何[套用敏捷方法](app-service-agile-software-development.md)，並利用進階部署技術 [(例如0正式發佈前小眾測試部署) 持續輕鬆地發佈您的微服務應用程式](app-service-web-test-in-production-controlled-test-flight.md)。</span><span class="sxs-lookup"><span data-stu-id="3fa45-280">Find out how to [apply agile methodologies and continuously publish your microservices application with ease](app-service-agile-software-development.md) and advanced deployment techniques like [flighting deployment](app-service-web-test-in-production-controlled-test-flight.md) easily.</span></span>

<a name="resources"></a>

## <a name="more-resources"></a><span data-ttu-id="3fa45-281">其他資源</span><span class="sxs-lookup"><span data-stu-id="3fa45-281">More resources</span></span>
* [<span data-ttu-id="3fa45-282">Azure 資源管理員範本語言</span><span class="sxs-lookup"><span data-stu-id="3fa45-282">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="3fa45-283">編寫 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="3fa45-283">Authoring Azure Resource Manager Templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="3fa45-284">Azure 資源管理員範本函式</span><span class="sxs-lookup"><span data-stu-id="3fa45-284">Azure Resource Manager Template Functions</span></span>](../azure-resource-manager/resource-group-template-functions.md)
* [<span data-ttu-id="3fa45-285">使用 Azure 資源管理員範本部署應用程式</span><span class="sxs-lookup"><span data-stu-id="3fa45-285">Deploy an application with Azure Resource Manager template</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="3fa45-286">搭配使用 Azure PowerShell 與 Azure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="3fa45-286">Using Azure PowerShell with Azure Resource Manager</span></span>](../azure-resource-manager/powershell-azure-resource-manager.md)
* [<span data-ttu-id="3fa45-287">Azure 中的資源群組部署疑難排解</span><span class="sxs-lookup"><span data-stu-id="3fa45-287">Troubleshooting Resource Group Deployments in Azure</span></span>](../azure-resource-manager/resource-manager-common-deployment-errors.md)

