---
title: "web 應用程式使用範本-Azure Cosmos DB aaaDeploy |Microsoft 文件"
description: "了解如何 toodeploy Azure Cosmos DB 帳戶、 Azure App Service Web 應用程式和範例 web 應用程式使用 Azure Resource Manager 範本。"
services: cosmos-db, app-service\web
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 087d8786-1155-42c7-924b-0eaba5a8b3e0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: b2bdde9279aad570606d7bf06dfc710f564b4d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-cosmos-db-and-azure-app-service-web-apps-using-an-azure-resource-manager-template"></a><span data-ttu-id="32593-103">使用 Azure Resource Manager 範本部署 Azure Cosmos DB 和 Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="32593-103">Deploy Azure Cosmos DB and Azure App Service Web Apps using an Azure Resource Manager Template</span></span>
<span data-ttu-id="32593-104">本教學課程示範如何 toouse Azure Resource Manager 範本 toodeploy 和整合[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)、 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web 應用程式和範例 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="32593-104">This tutorial shows you how toouse an Azure Resource Manager template toodeploy and integrate [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/), an [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app, and a sample web application.</span></span>

<span data-ttu-id="32593-105">使用 Azure 資源管理員範本，您可以輕鬆地自動化 hello 部署和設定您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="32593-105">Using Azure Resource Manager templates, you can easily automate hello deployment and configuration of your Azure resources.</span></span>  <span data-ttu-id="32593-106">本教學課程示範如何 toodeploy web 應用程式並自動設定 Azure Cosmos DB 帳戶連線資訊。</span><span class="sxs-lookup"><span data-stu-id="32593-106">This tutorial shows how toodeploy a web application and automatically configure Azure Cosmos DB account connection information.</span></span>

<span data-ttu-id="32593-107">完成本教學課程之後, 您將無法 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="32593-107">After completing this tutorial, you will be able tooanswer hello following questions:</span></span>  

* <span data-ttu-id="32593-108">如何使用 Azure Resource Manager 範本 toodeploy 和整合 Azure Cosmos DB 帳戶和 Azure App Service 中的 web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="32593-108">How can I use an Azure Resource Manager template toodeploy and integrate an Azure Cosmos DB account and a web app in Azure App Service?</span></span>
* <span data-ttu-id="32593-109">如何使用 Azure Resource Manager 範本 toodeploy 和整合 Azure Cosmos DB 帳戶、 App Service Web 應用程式中的 web app 和 Webdeploy 應用程式？</span><span class="sxs-lookup"><span data-stu-id="32593-109">How can I use an Azure Resource Manager template toodeploy and integrate an Azure Cosmos DB account, a web app in App Service Web Apps, and a Webdeploy application?</span></span>

<a id="Prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="32593-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="32593-110">Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="32593-111">雖然本教學課程不會假設使用 Azure Resource Manager 範本或 JSON 的使用經驗，如果您想 toomodify hello 參考範本或部署選項，然後將需要的每個區域的知識。</span><span class="sxs-lookup"><span data-stu-id="32593-111">While this tutorial does not assume prior experience with Azure Resource Manager templates or JSON, should you wish toomodify hello referenced templates or deployment options, then knowledge of each of these areas will be required.</span></span>
> 
> 

<span data-ttu-id="32593-112">之前遵循 hello 指示在本教學課程，請確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="32593-112">Before following hello instructions in this tutorial, ensure that you have hello following:</span></span>

* <span data-ttu-id="32593-113">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="32593-113">An Azure subscription.</span></span> <span data-ttu-id="32593-114">Azure 是訂閱型平台。</span><span class="sxs-lookup"><span data-stu-id="32593-114">Azure is a subscription-based platform.</span></span>  <span data-ttu-id="32593-115">如需取得訂用帳戶的詳細資訊，請參閱[購買選項](https://azure.microsoft.com/pricing/purchase-options/)、[成員優惠](https://azure.microsoft.com/pricing/member-offers/)或[免費使用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="32593-115">For more information about obtaining a subscription, see [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), [Member Offers](https://azure.microsoft.com/pricing/member-offers/), or [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="32593-116"><a id="CreateDB"></a>步驟 1： 下載 hello 範本檔案</span><span class="sxs-lookup"><span data-stu-id="32593-116"><a id="CreateDB"></a>Step 1: Download hello template files</span></span>
<span data-ttu-id="32593-117">讓我們開始下載 hello 範本檔案，我們將在本教學課程中使用。</span><span class="sxs-lookup"><span data-stu-id="32593-117">Let's start by downloading hello template files we will use in this tutorial.</span></span>

1. <span data-ttu-id="32593-118">下載 hello[建立 Azure Cosmos DB 帳戶，Web 應用程式，並部署示範應用程式範例](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json)範本 tooa 本機資料夾 (例如 C:\Azure Cosmos DBTemplates)。</span><span class="sxs-lookup"><span data-stu-id="32593-118">Download hello [Create an Azure Cosmos DB account, Web Apps, and deploy a demo application sample](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json) template tooa local folder (e.g. C:\Azure Cosmos DBTemplates).</span></span> <span data-ttu-id="32593-119">這個範本將會部署 Azure Cosmos DB 帳戶、App Service Web 應用程式和 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="32593-119">This template will deploy an Azure Cosmos DB account, an App Service web app, and a web application.</span></span>  <span data-ttu-id="32593-120">它也會自動將設定 hello web 應用程式 tooconnect toohello Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="32593-120">It will also automatically configure hello web application tooconnect toohello Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="32593-121">下載 hello[建立 Azure Cosmos DB 帳戶和 Web 應用程式範例](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json)範本 tooa 本機資料夾 (例如 C:\Azure Cosmos DBTemplates)。</span><span class="sxs-lookup"><span data-stu-id="32593-121">Download hello [Create an Azure Cosmos DB account and Web Apps sample](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json) template tooa local folder (e.g. C:\Azure Cosmos DBTemplates).</span></span> <span data-ttu-id="32593-122">此範本將部署 Azure Cosmos DB 帳戶，App Service web 應用程式，並將修改 hello 站台的應用程式設定 tooeasily 介面 Azure Cosmos DB 連接資訊，但不包含 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="32593-122">This template will deploy an Azure Cosmos DB account, an App Service web app, and will modify hello site's application settings tooeasily surface Azure Cosmos DB connection information, but does not include a web application.</span></span>  

<a id="Build"></a>

## <a name="step-2-deploy-hello-azure-cosmos-db-account-app-service-web-app-and-demo-application-sample"></a><span data-ttu-id="32593-123">步驟 2： 部署的 hello Azure Cosmos DB 帳戶，App Service web 應用程式和示範應用程式範例</span><span class="sxs-lookup"><span data-stu-id="32593-123">Step 2: Deploy hello Azure Cosmos DB account, App Service web app and demo application sample</span></span>
<span data-ttu-id="32593-124">現在讓我們來部署第一個範本。</span><span class="sxs-lookup"><span data-stu-id="32593-124">Now let's deploy our first template.</span></span>

> [!TIP]
> <span data-ttu-id="32593-125">hello 範本不會驗證 hello web 應用程式名稱並輸入下方的 Azure Cosmos DB 帳戶名稱是） 有效且 b） 可用。</span><span class="sxs-lookup"><span data-stu-id="32593-125">hello template does not validate that hello web app name and Azure Cosmos DB account name entered below are a) valid and b) available.</span></span>  <span data-ttu-id="32593-126">強烈建議您確認的 hello hello 可用性命名您計劃 toosupply 先前 toosubmitting hello 部署。</span><span class="sxs-lookup"><span data-stu-id="32593-126">It is highly recommended that you verify hello availability of hello names you plan toosupply prior toosubmitting hello deployment.</span></span>
> 
> 

1. <span data-ttu-id="32593-127">登入 toohello [Azure 入口網站](https://portal.azure.com)、 按一下 [新增]，並搜尋 「 範本部署 」。</span><span class="sxs-lookup"><span data-stu-id="32593-127">Login toohello [Azure Portal](https://portal.azure.com), click New and search for "Template deployment".</span></span>
    <span data-ttu-id="32593-128">![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment1.png)</span><span class="sxs-lookup"><span data-stu-id="32593-128">![Screenshot of hello template deployment UI](./media/create-website/TemplateDeployment1.png)</span></span>
2. <span data-ttu-id="32593-129">選取 hello 範本部署項目，然後按一下**建立** ![hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment2.png)</span><span class="sxs-lookup"><span data-stu-id="32593-129">Select hello Template deployment item and click **Create** ![Screenshot of hello template deployment UI](./media/create-website/TemplateDeployment2.png)</span></span>
3. <span data-ttu-id="32593-130">按一下**編輯範本**，貼上 hello 內容 hello DocDBWebsiteTodo.json 範本檔案，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="32593-130">Click **Edit template**, paste hello contents of hello DocDBWebsiteTodo.json template file, and click **Save**.</span></span>
   <span data-ttu-id="32593-131">![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment3.png)</span><span class="sxs-lookup"><span data-stu-id="32593-131">![Screenshot of hello template deployment UI](./media/create-website/TemplateDeployment3.png)</span></span>
4. <span data-ttu-id="32593-132">按一下**編輯參數**，提供值的每一個 hello 強制參數，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="32593-132">Click **Edit parameters**, provide values for each of hello mandatory parameters, and click **OK**.</span></span>  <span data-ttu-id="32593-133">hello 參數如下所示：</span><span class="sxs-lookup"><span data-stu-id="32593-133">hello parameters are as follows:</span></span>
   
   1. <span data-ttu-id="32593-134">網站名稱： 指定 hello App Service web 應用程式名稱，而且您將使用 tooaccess hello web 應用程式使用的 tooconstruct hello URL (例如： 如果您指定"mydemodocdbwebapp"，則 hello URL 將會存取 hello web 應用程式mydemodocdbwebapp.azurewebsites.net)。</span><span class="sxs-lookup"><span data-stu-id="32593-134">SITENAME: Specifies hello App Service web app name and is used tooconstruct hello URL that you will use tooaccess hello web app (e.g. if you specify "mydemodocdbwebapp", then hello URL by which you will access hello web app will be mydemodocdbwebapp.azurewebsites.net).</span></span>
   2. <span data-ttu-id="32593-135">HOSTINGPLANNAME： 指定應用程式服務裝載計劃 toocreate hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="32593-135">HOSTINGPLANNAME: Specifies hello name of App Service hosting plan toocreate.</span></span>
   3. <span data-ttu-id="32593-136">位置： 指定 hello toocreate hello Azure Cosmos DB 和 web 應用程式資源中的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="32593-136">LOCATION: Specifies hello Azure location in which toocreate hello Azure Cosmos DB and web app resources.</span></span>
   4. <span data-ttu-id="32593-137">DATABASEACCOUNTNAME： 指定 hello Azure Cosmos DB 帳戶 toocreate hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="32593-137">DATABASEACCOUNTNAME: Specifies hello name of hello Azure Cosmos DB account toocreate.</span></span>   
      
      ![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment4.png)
5. <span data-ttu-id="32593-139">選擇現有的資源群組或提供名稱 toomake 新的資源群組，並選擇 hello 資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="32593-139">Choose an existing Resource group or provide a name toomake a new resource group, and choose a location for hello resource group.</span></span>

    ![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment5.png)
6. <span data-ttu-id="32593-141">按一下**檢查 法律條款**，**購買**，然後按一下**建立**toobegin hello 部署。</span><span class="sxs-lookup"><span data-stu-id="32593-141">Click **Review legal terms**, **Purchase**, and then click **Create** toobegin hello deployment.</span></span>  <span data-ttu-id="32593-142">選取**Pin toodashboard**因此 hello 產生部署是輕鬆地看到您的 Azure 入口網站首頁上。</span><span class="sxs-lookup"><span data-stu-id="32593-142">Select **Pin toodashboard** so hello resulting deployment is easily visible on your Azure portal home page.</span></span>
   <span data-ttu-id="32593-143">![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment6.png)</span><span class="sxs-lookup"><span data-stu-id="32593-143">![Screenshot of hello template deployment UI](./media/create-website/TemplateDeployment6.png)</span></span>
7. <span data-ttu-id="32593-144">Hello 部署完成時，就會開啟 hello 資源群組 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="32593-144">When hello deployment finishes, hello Resource group blade will open.</span></span>
   <span data-ttu-id="32593-145">![Hello 資源群組 刀鋒視窗的螢幕擷取畫面](./media/create-website/TemplateDeployment7.png)</span><span class="sxs-lookup"><span data-stu-id="32593-145">![Screenshot of hello resource group blade](./media/create-website/TemplateDeployment7.png)</span></span>  
8. <span data-ttu-id="32593-146">toouse hello 應用程式，直接瀏覽 toohello web 應用程式 URL （hello 上述範例中，在 hello URL 會是 http://mydemodocdbwebapp.azurewebsites.net）。</span><span class="sxs-lookup"><span data-stu-id="32593-146">toouse hello application, simply navigate toohello web app URL (in hello example above, hello URL would be http://mydemodocdbwebapp.azurewebsites.net).</span></span>  <span data-ttu-id="32593-147">您會看到下列 web 應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="32593-147">You'll see hello following web application:</span></span>
   
   ![範例待辦事項應用程式](./media/create-website/image2.png)
9. <span data-ttu-id="32593-149">請繼續並 hello web 應用程式中建立數個工作，然後傳回 toohello 資源群組 刀鋒視窗中 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="32593-149">Go ahead and create a couple of tasks in hello web app and then return toohello Resource group blade in hello Azure portal.</span></span> <span data-ttu-id="32593-150">按一下 hello 資源 清單中的 hello Azure Cosmos DB 帳戶資源，然後按一下**查詢總管**。</span><span class="sxs-lookup"><span data-stu-id="32593-150">Click hello Azure Cosmos DB account resource in hello Resources list and then click **Query Explorer**.</span></span>
    <span data-ttu-id="32593-151">![螢幕擷取畫面的 hello 透鏡與 hello 反白顯示的 web 應用程式的摘要](./media/create-website/TemplateDeployment8.png)</span><span class="sxs-lookup"><span data-stu-id="32593-151">![Screenshot of hello Summary lens with hello web app highlighted](./media/create-website/TemplateDeployment8.png)</span></span>  
10. <span data-ttu-id="32593-152">執行 hello 預設查詢，「 選取 * 從 c"，並檢查 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="32593-152">Run hello default query, "SELECT * FROM c" and inspect hello results.</span></span>  <span data-ttu-id="32593-153">請注意該 hello 查詢已擷取您在步驟 7 上述建立 hello todo 項目的 hello JSON 表示法。</span><span class="sxs-lookup"><span data-stu-id="32593-153">Notice that hello query has retrieved hello JSON representation of hello todo items you created in step 7 above.</span></span>  <span data-ttu-id="32593-154">感覺可用 tooexperiment 查詢;例如，請嘗試重新執行 SELECT * FROM c WHERE c.isComplete = true tooreturn 已標示為完成的所有 todo 項目。</span><span class="sxs-lookup"><span data-stu-id="32593-154">Feel free tooexperiment with queries; for example, try running SELECT * FROM c WHERE c.isComplete = true tooreturn all todo items which have been marked as complete.</span></span>
    
    ![Hello 查詢總管和結果的刀鋒視窗顯示 hello 查詢結果的螢幕擷取畫面](./media/create-website/image5.png)
11. <span data-ttu-id="32593-156">感覺可用 tooexplore hello Azure Cosmos DB 入口網站體驗，或修改 hello 範例待辦事項應用程式。</span><span class="sxs-lookup"><span data-stu-id="32593-156">Feel free tooexplore hello Azure Cosmos DB portal experience or modify hello sample Todo application.</span></span>  <span data-ttu-id="32593-157">當您準備好時，讓我們來部署另一個範本。</span><span class="sxs-lookup"><span data-stu-id="32593-157">When you're ready, let's deploy another template.</span></span>

<a id="Build"></a> 

## <a name="step-3-deploy-hello-document-account-and-web-app-sample"></a><span data-ttu-id="32593-158">步驟 3： 部署 hello 文件的帳戶和 web 應用程式範例</span><span class="sxs-lookup"><span data-stu-id="32593-158">Step 3: Deploy hello Document account and web app sample</span></span>
<span data-ttu-id="32593-159">現在讓我們來部署第二個範本。</span><span class="sxs-lookup"><span data-stu-id="32593-159">Now let's deploy our second template.</span></span>  <span data-ttu-id="32593-160">此範本是很有用的 tooshow 如何您可以將 Azure Cosmos DB 連接資訊，例如帳戶端點和服務主要金鑰插入 web 應用程式做為應用程式設定或自訂連接字串。</span><span class="sxs-lookup"><span data-stu-id="32593-160">This template is useful tooshow how you can inject Azure Cosmos DB connection information such as account endpoint and master key into a web app as application settings or as a custom connection string.</span></span> <span data-ttu-id="32593-161">例如，您可能有您的 web 應用程式，您會想 toodeploy Azure Cosmos DB 帳戶，且有 hello 連接資訊在部署期間自動填入。</span><span class="sxs-lookup"><span data-stu-id="32593-161">For example, perhaps you have your own web application that you would like toodeploy with an Azure Cosmos DB account and have hello connection information automatically populated during deployment.</span></span>

> [!TIP]
> <span data-ttu-id="32593-162">hello 範本不會驗證 hello web 應用程式名稱並輸入下方的 Azure Cosmos DB 帳戶名稱是） 有效且 b） 可用。</span><span class="sxs-lookup"><span data-stu-id="32593-162">hello template does not validate that hello web app name and Azure Cosmos DB account name entered below are a) valid and b) available.</span></span>  <span data-ttu-id="32593-163">強烈建議您確認的 hello hello 可用性命名您計劃 toosupply 先前 toosubmitting hello 部署。</span><span class="sxs-lookup"><span data-stu-id="32593-163">It is highly recommended that you verify hello availability of hello names you plan toosupply prior toosubmitting hello deployment.</span></span>
> 
> 

1. <span data-ttu-id="32593-164">在 hello [Azure 入口網站](https://portal.azure.com)、 按一下 [新增]，並搜尋 「 範本部署 」。</span><span class="sxs-lookup"><span data-stu-id="32593-164">In hello [Azure Portal](https://portal.azure.com), click New and search for "Template deployment".</span></span>
    <span data-ttu-id="32593-165">![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment1.png)</span><span class="sxs-lookup"><span data-stu-id="32593-165">![Screenshot of hello template deployment UI](./media/create-website/TemplateDeployment1.png)</span></span>
2. <span data-ttu-id="32593-166">選取 hello 範本部署項目，然後按一下**建立** ![hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment2.png)</span><span class="sxs-lookup"><span data-stu-id="32593-166">Select hello Template deployment item and click **Create** ![Screenshot of hello template deployment UI](./media/create-website/TemplateDeployment2.png)</span></span>
3. <span data-ttu-id="32593-167">按一下**編輯範本**，貼上 hello 內容 hello DocDBWebSite.json 範本檔案，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="32593-167">Click **Edit template**, paste hello contents of hello DocDBWebSite.json template file, and click **Save**.</span></span>
   <span data-ttu-id="32593-168">![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment3.png)</span><span class="sxs-lookup"><span data-stu-id="32593-168">![Screenshot of hello template deployment UI](./media/create-website/TemplateDeployment3.png)</span></span>
4. <span data-ttu-id="32593-169">按一下**編輯參數**，提供值的每一個 hello 強制參數，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="32593-169">Click **Edit parameters**, provide values for each of hello mandatory parameters, and click **OK**.</span></span>  <span data-ttu-id="32593-170">hello 參數如下所示：</span><span class="sxs-lookup"><span data-stu-id="32593-170">hello parameters are as follows:</span></span>
   
   1. <span data-ttu-id="32593-171">網站名稱： 指定 hello App Service web 應用程式名稱，而且您將使用 tooaccess hello web 應用程式使用的 tooconstruct hello URL (例如： 如果您指定"mydemodocdbwebapp"，則 hello URL 將會存取 hello web 應用程式mydemodocdbwebapp.azurewebsites.net)。</span><span class="sxs-lookup"><span data-stu-id="32593-171">SITENAME: Specifies hello App Service web app name and is used tooconstruct hello URL that you will use tooaccess hello web app (e.g. if you specify "mydemodocdbwebapp", then hello URL by which you will access hello web app will be mydemodocdbwebapp.azurewebsites.net).</span></span>
   2. <span data-ttu-id="32593-172">HOSTINGPLANNAME： 指定應用程式服務裝載計劃 toocreate hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="32593-172">HOSTINGPLANNAME: Specifies hello name of App Service hosting plan toocreate.</span></span>
   3. <span data-ttu-id="32593-173">位置： 指定 hello toocreate hello Azure Cosmos DB 和 web 應用程式資源中的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="32593-173">LOCATION: Specifies hello Azure location in which toocreate hello Azure Cosmos DB and web app resources.</span></span>
   4. <span data-ttu-id="32593-174">DATABASEACCOUNTNAME： 指定 hello Azure Cosmos DB 帳戶 toocreate hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="32593-174">DATABASEACCOUNTNAME: Specifies hello name of hello Azure Cosmos DB account toocreate.</span></span>   
      
      ![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment4.png)
5. <span data-ttu-id="32593-176">選擇現有的資源群組或提供名稱 toomake 新的資源群組，並選擇 hello 資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="32593-176">Choose an existing Resource group or provide a name toomake a new resource group, and choose a location for hello resource group.</span></span>

    ![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment5.png)
6. <span data-ttu-id="32593-178">按一下**檢查 法律條款**，**購買**，然後按一下**建立**toobegin hello 部署。</span><span class="sxs-lookup"><span data-stu-id="32593-178">Click **Review legal terms**, **Purchase**, and then click **Create** toobegin hello deployment.</span></span>  <span data-ttu-id="32593-179">選取**Pin toodashboard**因此 hello 產生部署是輕鬆地看到您的 Azure 入口網站首頁上。</span><span class="sxs-lookup"><span data-stu-id="32593-179">Select **Pin toodashboard** so hello resulting deployment is easily visible on your Azure portal home page.</span></span>
   <span data-ttu-id="32593-180">![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment6.png)</span><span class="sxs-lookup"><span data-stu-id="32593-180">![Screenshot of hello template deployment UI](./media/create-website/TemplateDeployment6.png)</span></span>
7. <span data-ttu-id="32593-181">Hello 部署完成時，就會開啟 hello 資源群組 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="32593-181">When hello deployment finishes, hello Resource group blade will open.</span></span>
   <span data-ttu-id="32593-182">![Hello 資源群組 刀鋒視窗的螢幕擷取畫面](./media/create-website/TemplateDeployment7.png)</span><span class="sxs-lookup"><span data-stu-id="32593-182">![Screenshot of hello resource group blade](./media/create-website/TemplateDeployment7.png)</span></span>  
8. <span data-ttu-id="32593-183">按一下 hello hello 資源 清單中的 Web 應用程式資源，然後按一下**應用程式設定** ![hello 資源群組的螢幕擷取畫面](./media/create-website/TemplateDeployment9.png)</span><span class="sxs-lookup"><span data-stu-id="32593-183">Click hello Web App resource in hello Resources list and then click **Application settings** ![Screenshot of hello resource group](./media/create-website/TemplateDeployment9.png)</span></span>  
9. <span data-ttu-id="32593-184">請注意如何在 hello Azure Cosmos DB 端點和每個 hello Azure Cosmos 資料庫主要金鑰的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="32593-184">Note how there are application settings present for hello Azure Cosmos DB endpoint and each of hello Azure Cosmos DB master keys.</span></span>

    ![應用程式設定的螢幕擷取畫面](./media/create-website/TemplateDeployment10.png)  
10. <span data-ttu-id="32593-186">感覺可用 toocontinue 瀏覽 hello Azure 入口網站，或遵循其中一種我們 Azure Cosmos DB[範例](http://go.microsoft.com/fwlink/?LinkID=402386)toocreate Azure Cosmos DB 應用程式。</span><span class="sxs-lookup"><span data-stu-id="32593-186">Feel free toocontinue exploring hello Azure Portal, or follow one of our Azure Cosmos DB [samples](http://go.microsoft.com/fwlink/?LinkID=402386) toocreate your own Azure Cosmos DB application.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="32593-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32593-187">Next steps</span></span>
<span data-ttu-id="32593-188">恭喜！</span><span class="sxs-lookup"><span data-stu-id="32593-188">Congratulations!</span></span> <span data-ttu-id="32593-189">您已使用 Azure Resource Manager 範本部署了 Azure Cosmos DB、App Service Web 應用程式及範例 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="32593-189">You've deployed Azure Cosmos DB, App Service web app and a sample web application using Azure Resource Manager templates.</span></span>

* <span data-ttu-id="32593-190">按一下 深入了解 Azure Cosmos DB toolearn[這裡](http://azure.com/docdb)。</span><span class="sxs-lookup"><span data-stu-id="32593-190">toolearn more about Azure Cosmos DB, click [here](http://azure.com/docdb).</span></span>
* <span data-ttu-id="32593-191">進一步了解 Azure App Service Web 應用程式，toolearn 按一下[這裡](http://go.microsoft.com/fwlink/?LinkId=325362)。</span><span class="sxs-lookup"><span data-stu-id="32593-191">toolearn more about Azure App Service Web apps, click [here](http://go.microsoft.com/fwlink/?LinkId=325362).</span></span>
* <span data-ttu-id="32593-192">按一下 進一步了解 Azure 資源管理員範本 toolearn[這裡](https://msdn.microsoft.com/library/azure/dn790549.aspx)。</span><span class="sxs-lookup"><span data-stu-id="32593-192">toolearn more about Azure Resource Manager templates, click [here](https://msdn.microsoft.com/library/azure/dn790549.aspx).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="32593-193">變更的項目</span><span class="sxs-lookup"><span data-stu-id="32593-193">What's changed</span></span>
* <span data-ttu-id="32593-194">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="32593-194">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
* <span data-ttu-id="32593-195">Hello 舊入口網站 toohello 新入口網站的變更如指南 toohello:[巡覽參考 hello Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)</span><span class="sxs-lookup"><span data-stu-id="32593-195">For a guide toohello change of hello old portal toohello new portal see: [Reference for navigating hello Azure Classic Portal](http://go.microsoft.com/fwlink/?LinkId=529715)</span></span>

> [!NOTE]
> <span data-ttu-id="32593-196">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](http://go.microsoft.com/fwlink/?LinkId=523751)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="32593-196">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](http://go.microsoft.com/fwlink/?LinkId=523751), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="32593-197">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="32593-197">No credit cards required; no commitments.</span></span>
> 
> 

