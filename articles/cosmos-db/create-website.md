---
title: "使用範本部署 Web 應用程式 - Azure Cosmos DB | Microsoft Docs"
description: "了解如何使用 Azure Resource Manager 範本，來部署 Azure Cosmos DB 帳戶、Azure App Service Web Apps，以及範例 Web 應用程式。"
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
ms.openlocfilehash: 633b88761de4d2c99cfd196cfac8e664fc83c546
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-azure-cosmos-db-and-azure-app-service-web-apps-using-an-azure-resource-manager-template"></a><span data-ttu-id="55346-103">使用 Azure Resource Manager 範本部署 Azure Cosmos DB 和 Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="55346-103">Deploy Azure Cosmos DB and Azure App Service Web Apps using an Azure Resource Manager Template</span></span>
<span data-ttu-id="55346-104">本教學課程示範如何使用 Azure Resource Manager 範本，來部署和整合 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)、[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web 應用程式及範例 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="55346-104">This tutorial shows you how to use an Azure Resource Manager template to deploy and integrate [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/), an [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app, and a sample web application.</span></span>

<span data-ttu-id="55346-105">使用 Azure Resource Manager 範本，您可以輕鬆自動化 Azure 資源的部署和設定。</span><span class="sxs-lookup"><span data-stu-id="55346-105">Using Azure Resource Manager templates, you can easily automate the deployment and configuration of your Azure resources.</span></span>  <span data-ttu-id="55346-106">本教學課程示範如何部署 Web 應用程式，以及自動設定 Azure Cosmos DB 帳戶連接資訊。</span><span class="sxs-lookup"><span data-stu-id="55346-106">This tutorial shows how to deploy a web application and automatically configure Azure Cosmos DB account connection information.</span></span>

<span data-ttu-id="55346-107">完成本教學課程後，您就能夠回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="55346-107">After completing this tutorial, you will be able to answer the following questions:</span></span>  

* <span data-ttu-id="55346-108">如何使用 Azure Resource Manager 範本，來部署和整合 Azure Cosmos DB 帳戶與 Azure App Service 中的 Web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="55346-108">How can I use an Azure Resource Manager template to deploy and integrate an Azure Cosmos DB account and a web app in Azure App Service?</span></span>
* <span data-ttu-id="55346-109">如何使用 Azure Resource Manager 範本，來部署和整合 Azure Cosmos DB 帳戶、App Service Web Apps 中的 Web 應用程式，以及 Webdeploy 應用程式？</span><span class="sxs-lookup"><span data-stu-id="55346-109">How can I use an Azure Resource Manager template to deploy and integrate an Azure Cosmos DB account, a web app in App Service Web Apps, and a Webdeploy application?</span></span>

<a id="Prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="55346-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="55346-110">Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="55346-111">雖然本教學課程不會假設先前有使用 Azure Resource Manager 範本或 JSON 的經驗，但是，如果您想要修改參考的範本或部署選項，則需要每個領域的知識。</span><span class="sxs-lookup"><span data-stu-id="55346-111">While this tutorial does not assume prior experience with Azure Resource Manager templates or JSON, should you wish to modify the referenced templates or deployment options, then knowledge of each of these areas will be required.</span></span>
> 
> 

<span data-ttu-id="55346-112">在依照本教學課程中的指示進行之前，請先確定您已備妥下列項目：</span><span class="sxs-lookup"><span data-stu-id="55346-112">Before following the instructions in this tutorial, ensure that you have the following:</span></span>

* <span data-ttu-id="55346-113">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="55346-113">An Azure subscription.</span></span> <span data-ttu-id="55346-114">Azure 是訂閱型平台。</span><span class="sxs-lookup"><span data-stu-id="55346-114">Azure is a subscription-based platform.</span></span>  <span data-ttu-id="55346-115">如需取得訂用帳戶的詳細資訊，請參閱[購買選項](https://azure.microsoft.com/pricing/purchase-options/)、[成員優惠](https://azure.microsoft.com/pricing/member-offers/)或[免費使用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="55346-115">For more information about obtaining a subscription, see [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), [Member Offers](https://azure.microsoft.com/pricing/member-offers/), or [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="55346-116"><a id="CreateDB"></a>步驟 1︰下載範本檔案</span><span class="sxs-lookup"><span data-stu-id="55346-116"><a id="CreateDB"></a>Step 1: Download the template files</span></span>
<span data-ttu-id="55346-117">讓我們從下載本教學課程要使用的範本檔案開始。</span><span class="sxs-lookup"><span data-stu-id="55346-117">Let's start by downloading the template files we will use in this tutorial.</span></span>

1. <span data-ttu-id="55346-118">將[建立 Azure Cosmos DB 帳戶、Web Apps 和部署示範應用程式範例](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json)範本下載至本機資料夾 (例如 C:\Azure Cosmos DBTemplates)。</span><span class="sxs-lookup"><span data-stu-id="55346-118">Download the [Create an Azure Cosmos DB account, Web Apps, and deploy a demo application sample](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json) template to a local folder (e.g. C:\Azure Cosmos DBTemplates).</span></span> <span data-ttu-id="55346-119">這個範本將會部署 Azure Cosmos DB 帳戶、App Service Web 應用程式和 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="55346-119">This template will deploy an Azure Cosmos DB account, an App Service web app, and a web application.</span></span>  <span data-ttu-id="55346-120">它還會自動設定 Web 應用程式以連接到 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="55346-120">It will also automatically configure the web application to connect to the Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="55346-121">將[建立 Azure Cosmos DB 帳戶和 Web Apps 範例](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json)範本下載至本機資料夾 (例如 C:\Azure Cosmos DBTemplates)。</span><span class="sxs-lookup"><span data-stu-id="55346-121">Download the [Create an Azure Cosmos DB account and Web Apps sample](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json) template to a local folder (e.g. C:\Azure Cosmos DBTemplates).</span></span> <span data-ttu-id="55346-122">這個範本將會部署 Azure Cosmos DB 帳戶、App Service Web 應用程式，並將修改網站的應用程式設定來輕鬆呈現 Azure Cosmos DB 連接資訊，但不包含 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="55346-122">This template will deploy an Azure Cosmos DB account, an App Service web app, and will modify the site's application settings to easily surface Azure Cosmos DB connection information, but does not include a web application.</span></span>  

<a id="Build"></a>

## <a name="step-2-deploy-the-azure-cosmos-db-account-app-service-web-app-and-demo-application-sample"></a><span data-ttu-id="55346-123">步驟 2：部署 Azure Cosmos DB 帳戶、App Service Web 應用程式與示範應用程式範例</span><span class="sxs-lookup"><span data-stu-id="55346-123">Step 2: Deploy the Azure Cosmos DB account, App Service web app and demo application sample</span></span>
<span data-ttu-id="55346-124">現在讓我們來部署第一個範本。</span><span class="sxs-lookup"><span data-stu-id="55346-124">Now let's deploy our first template.</span></span>

> [!TIP]
> <span data-ttu-id="55346-125">這個範本不會驗證下面輸入的 Web 應用程式名稱和 Azure Cosmos DB 帳戶名稱 a) 是否有效且 b) 可用。</span><span class="sxs-lookup"><span data-stu-id="55346-125">The template does not validate that the web app name and Azure Cosmos DB account name entered below are a) valid and b) available.</span></span>  <span data-ttu-id="55346-126">強烈建議您先確認打算提供之名稱的可用性，再提交部署。</span><span class="sxs-lookup"><span data-stu-id="55346-126">It is highly recommended that you verify the availability of the names you plan to supply prior to submitting the deployment.</span></span>
> 
> 

1. <span data-ttu-id="55346-127">登入 [Azure 入口網站](https://portal.azure.com)，按一下 [新增]，並搜尋「範本部署」。</span><span class="sxs-lookup"><span data-stu-id="55346-127">Login to the [Azure Portal](https://portal.azure.com), click New and search for "Template deployment".</span></span>
    <span data-ttu-id="55346-128">![範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment1.png)</span><span class="sxs-lookup"><span data-stu-id="55346-128">![Screenshot of the template deployment UI](./media/create-website/TemplateDeployment1.png)</span></span>
2. <span data-ttu-id="55346-129">選取範本部署項目，然後按一下 [建立] ![範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment2.png)</span><span class="sxs-lookup"><span data-stu-id="55346-129">Select the Template deployment item and click **Create** ![Screenshot of the template deployment UI](./media/create-website/TemplateDeployment2.png)</span></span>
3. <span data-ttu-id="55346-130">按一下 [編輯範本]，貼上 DocDBWebsiteTodo.json 範本檔案的內容，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="55346-130">Click **Edit template**, paste the contents of the DocDBWebsiteTodo.json template file, and click **Save**.</span></span>
   <span data-ttu-id="55346-131">![範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment3.png)</span><span class="sxs-lookup"><span data-stu-id="55346-131">![Screenshot of the template deployment UI](./media/create-website/TemplateDeployment3.png)</span></span>
4. <span data-ttu-id="55346-132">按一下 [編輯參數]，提供每個必要參數的值，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="55346-132">Click **Edit parameters**, provide values for each of the mandatory parameters, and click **OK**.</span></span>  <span data-ttu-id="55346-133">參數如下所示：</span><span class="sxs-lookup"><span data-stu-id="55346-133">The parameters are as follows:</span></span>
   
   1. <span data-ttu-id="55346-134">SITENAME：指定 App Service Web 應用程式名稱，並用來建構您將用來存取 Web 應用程式的 URL (例如：如果您指定 "mydemodocdbwebsite"，則將存取網站的 URL 會是 mydemodocdbwebsite.azurewebsites.net)。</span><span class="sxs-lookup"><span data-stu-id="55346-134">SITENAME: Specifies the App Service web app name and is used to construct the URL that you will use to access the web app (e.g. if you specify "mydemodocdbwebapp", then the URL by which you will access the web app will be mydemodocdbwebapp.azurewebsites.net).</span></span>
   2. <span data-ttu-id="55346-135">HOSTINGPLANNAME︰指定要建立的主控方案 App Service 名稱。</span><span class="sxs-lookup"><span data-stu-id="55346-135">HOSTINGPLANNAME: Specifies the name of App Service hosting plan to create.</span></span>
   3. <span data-ttu-id="55346-136">LOCATION：指定要在其中建立 Azure Cosmos DB 和 Web 應用程式資源的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="55346-136">LOCATION: Specifies the Azure location in which to create the Azure Cosmos DB and web app resources.</span></span>
   4. <span data-ttu-id="55346-137">DATABASEACCOUNTNAME：指定要建立的 Azure Cosmos DB 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="55346-137">DATABASEACCOUNTNAME: Specifies the name of the Azure Cosmos DB account to create.</span></span>   
      
      ![範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment4.png)
5. <span data-ttu-id="55346-139">選擇現有的資源群組，或提供名稱建立新的資源群組，然後選擇資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="55346-139">Choose an existing Resource group or provide a name to make a new resource group, and choose a location for the resource group.</span></span>

    ![範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment5.png)
6. <span data-ttu-id="55346-141">依序按一下 [檢閱法律條款]、[購買] 和 [建立] 以開始部署。</span><span class="sxs-lookup"><span data-stu-id="55346-141">Click **Review legal terms**, **Purchase**, and then click **Create** to begin the deployment.</span></span>  <span data-ttu-id="55346-142">選取 [釘選到儀表板]  讓產生的部署輕鬆簡單顯示在 Azure 入口網站的首頁上。</span><span class="sxs-lookup"><span data-stu-id="55346-142">Select **Pin to dashboard** so the resulting deployment is easily visible on your Azure portal home page.</span></span>
   <span data-ttu-id="55346-143">![範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment6.png)</span><span class="sxs-lookup"><span data-stu-id="55346-143">![Screenshot of the template deployment UI](./media/create-website/TemplateDeployment6.png)</span></span>
7. <span data-ttu-id="55346-144">部署完成時，就會開啟資源群組的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="55346-144">When the deployment finishes, the Resource group blade will open.</span></span>
   <span data-ttu-id="55346-145">![資源群組刀鋒視窗的螢幕擷取畫面](./media/create-website/TemplateDeployment7.png)</span><span class="sxs-lookup"><span data-stu-id="55346-145">![Screenshot of the resource group blade](./media/create-website/TemplateDeployment7.png)</span></span>  
8. <span data-ttu-id="55346-146">若要使用應用程式，只要瀏覽至 Web 應用程式 URL (上述範例中的 URL 會是 http://mydemodocdbwebapp.azurewebsites.net ) 。</span><span class="sxs-lookup"><span data-stu-id="55346-146">To use the application, simply navigate to the web app URL (in the example above, the URL would be http://mydemodocdbwebapp.azurewebsites.net).</span></span>  <span data-ttu-id="55346-147">您會看到下列的 Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="55346-147">You'll see the following web application:</span></span>
   
   ![範例待辦事項應用程式](./media/create-website/image2.png)
9. <span data-ttu-id="55346-149">請繼續在 Web 應用程式中建立幾個工作，然後回到 Azure 入口網站的資源群組刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="55346-149">Go ahead and create a couple of tasks in the web app and then return to the Resource group blade in the Azure portal.</span></span> <span data-ttu-id="55346-150">按一下 [資源] 清單中的 Azure Cosmos DB 帳戶資源，然後按一下 [查詢總管]。</span><span class="sxs-lookup"><span data-stu-id="55346-150">Click the Azure Cosmos DB account resource in the Resources list and then click **Query Explorer**.</span></span>
    <span data-ttu-id="55346-151">![包含反白顯示 Web 應用程式的 [摘要] 功能濾鏡的螢幕擷取畫面](./media/create-website/TemplateDeployment8.png)</span><span class="sxs-lookup"><span data-stu-id="55346-151">![Screenshot of the Summary lens with the web app highlighted](./media/create-website/TemplateDeployment8.png)</span></span>  
10. <span data-ttu-id="55346-152">執行預設查詢 "SELECT * FROM c"，然後檢查結果。</span><span class="sxs-lookup"><span data-stu-id="55346-152">Run the default query, "SELECT * FROM c" and inspect the results.</span></span>  <span data-ttu-id="55346-153">請注意查詢已擷取您在步驟 7 所建立待辦事項的 JSON 表示法。</span><span class="sxs-lookup"><span data-stu-id="55346-153">Notice that the query has retrieved the JSON representation of the todo items you created in step 7 above.</span></span>  <span data-ttu-id="55346-154">任意嘗試查詢；例如，嘗試執行 SELECT * FROM c WHERE c.isComplete = true，以傳回所有已標示為完成的待辦事項。</span><span class="sxs-lookup"><span data-stu-id="55346-154">Feel free to experiment with queries; for example, try running SELECT * FROM c WHERE c.isComplete = true to return all todo items which have been marked as complete.</span></span>
    
    ![顯示查詢結果的 [查詢總管] 和 [結果] 刀鋒視窗的螢幕擷取畫面](./media/create-website/image5.png)
11. <span data-ttu-id="55346-156">任意瀏覽 Azure Cosmos DB 入口網站體驗，或修改範例 Todo 應用程式。</span><span class="sxs-lookup"><span data-stu-id="55346-156">Feel free to explore the Azure Cosmos DB portal experience or modify the sample Todo application.</span></span>  <span data-ttu-id="55346-157">當您準備好時，讓我們來部署另一個範本。</span><span class="sxs-lookup"><span data-stu-id="55346-157">When you're ready, let's deploy another template.</span></span>

<a id="Build"></a> 

## <a name="step-3-deploy-the-document-account-and-web-app-sample"></a><span data-ttu-id="55346-158">步驟 3：部署文件帳戶和 Web 應用程式範例</span><span class="sxs-lookup"><span data-stu-id="55346-158">Step 3: Deploy the Document account and web app sample</span></span>
<span data-ttu-id="55346-159">現在讓我們來部署第二個範本。</span><span class="sxs-lookup"><span data-stu-id="55346-159">Now let's deploy our second template.</span></span>  <span data-ttu-id="55346-160">這個範本非常有用，它示範如何將帳戶端點和主要金鑰等 Azure Cosmos DB 連接資訊插入 Web 應用程式，以當做應用程式設定或自訂的連接字串。</span><span class="sxs-lookup"><span data-stu-id="55346-160">This template is useful to show how you can inject Azure Cosmos DB connection information such as account endpoint and master key into a web app as application settings or as a custom connection string.</span></span> <span data-ttu-id="55346-161">例如，您或許擁有想要使用 Azure Cosmos DB 帳戶部署的 Web 應用程式，以及在部署期間自動填入的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="55346-161">For example, perhaps you have your own web application that you would like to deploy with an Azure Cosmos DB account and have the connection information automatically populated during deployment.</span></span>

> [!TIP]
> <span data-ttu-id="55346-162">這個範本不會驗證下面輸入的 Web 應用程式名稱和 Azure Cosmos DB 帳戶名稱 a) 是否有效且 b) 可用。</span><span class="sxs-lookup"><span data-stu-id="55346-162">The template does not validate that the web app name and Azure Cosmos DB account name entered below are a) valid and b) available.</span></span>  <span data-ttu-id="55346-163">強烈建議您先確認打算提供之名稱的可用性，再提交部署。</span><span class="sxs-lookup"><span data-stu-id="55346-163">It is highly recommended that you verify the availability of the names you plan to supply prior to submitting the deployment.</span></span>
> 
> 

1. <span data-ttu-id="55346-164">在 [Azure 入口網站](https://portal.azure.com)中，按一下 [新增]，並搜尋「範本部署」。</span><span class="sxs-lookup"><span data-stu-id="55346-164">In the [Azure Portal](https://portal.azure.com), click New and search for "Template deployment".</span></span>
    <span data-ttu-id="55346-165">![範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment1.png)</span><span class="sxs-lookup"><span data-stu-id="55346-165">![Screenshot of the template deployment UI](./media/create-website/TemplateDeployment1.png)</span></span>
2. <span data-ttu-id="55346-166">選取範本部署項目，然後按一下 [建立] ![範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment2.png)</span><span class="sxs-lookup"><span data-stu-id="55346-166">Select the Template deployment item and click **Create** ![Screenshot of the template deployment UI](./media/create-website/TemplateDeployment2.png)</span></span>
3. <span data-ttu-id="55346-167">按一下 [編輯範本]，貼上 DocDBWebSite.json 範本檔案的內容，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="55346-167">Click **Edit template**, paste the contents of the DocDBWebSite.json template file, and click **Save**.</span></span>
   <span data-ttu-id="55346-168">![範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment3.png)</span><span class="sxs-lookup"><span data-stu-id="55346-168">![Screenshot of the template deployment UI](./media/create-website/TemplateDeployment3.png)</span></span>
4. <span data-ttu-id="55346-169">按一下 [編輯參數]，提供每個必要參數的值，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="55346-169">Click **Edit parameters**, provide values for each of the mandatory parameters, and click **OK**.</span></span>  <span data-ttu-id="55346-170">參數如下所示：</span><span class="sxs-lookup"><span data-stu-id="55346-170">The parameters are as follows:</span></span>
   
   1. <span data-ttu-id="55346-171">SITENAME：指定 App Service Web 應用程式名稱，並用來建構您將用來存取 Web 應用程式的 URL (例如：如果您指定 "mydemodocdbwebsite"，則將存取網站的 URL 會是 mydemodocdbwebsite.azurewebsites.net)。</span><span class="sxs-lookup"><span data-stu-id="55346-171">SITENAME: Specifies the App Service web app name and is used to construct the URL that you will use to access the web app (e.g. if you specify "mydemodocdbwebapp", then the URL by which you will access the web app will be mydemodocdbwebapp.azurewebsites.net).</span></span>
   2. <span data-ttu-id="55346-172">HOSTINGPLANNAME︰指定要建立的主控方案 App Service 名稱。</span><span class="sxs-lookup"><span data-stu-id="55346-172">HOSTINGPLANNAME: Specifies the name of App Service hosting plan to create.</span></span>
   3. <span data-ttu-id="55346-173">LOCATION：指定要在其中建立 Azure Cosmos DB 和 Web 應用程式資源的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="55346-173">LOCATION: Specifies the Azure location in which to create the Azure Cosmos DB and web app resources.</span></span>
   4. <span data-ttu-id="55346-174">DATABASEACCOUNTNAME：指定要建立的 Azure Cosmos DB 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="55346-174">DATABASEACCOUNTNAME: Specifies the name of the Azure Cosmos DB account to create.</span></span>   
      
      ![範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment4.png)
5. <span data-ttu-id="55346-176">選擇現有的資源群組，或提供名稱建立新的資源群組，然後選擇資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="55346-176">Choose an existing Resource group or provide a name to make a new resource group, and choose a location for the resource group.</span></span>

    ![範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment5.png)
6. <span data-ttu-id="55346-178">依序按一下 [檢閱法律條款]、[購買] 和 [建立] 以開始部署。</span><span class="sxs-lookup"><span data-stu-id="55346-178">Click **Review legal terms**, **Purchase**, and then click **Create** to begin the deployment.</span></span>  <span data-ttu-id="55346-179">選取 [釘選到儀表板]  讓產生的部署輕鬆簡單顯示在 Azure 入口網站的首頁上。</span><span class="sxs-lookup"><span data-stu-id="55346-179">Select **Pin to dashboard** so the resulting deployment is easily visible on your Azure portal home page.</span></span>
   <span data-ttu-id="55346-180">![範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment6.png)</span><span class="sxs-lookup"><span data-stu-id="55346-180">![Screenshot of the template deployment UI](./media/create-website/TemplateDeployment6.png)</span></span>
7. <span data-ttu-id="55346-181">部署完成時，就會開啟資源群組的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="55346-181">When the deployment finishes, the Resource group blade will open.</span></span>
   <span data-ttu-id="55346-182">![資源群組刀鋒視窗的螢幕擷取畫面](./media/create-website/TemplateDeployment7.png)</span><span class="sxs-lookup"><span data-stu-id="55346-182">![Screenshot of the resource group blade](./media/create-website/TemplateDeployment7.png)</span></span>  
8. <span data-ttu-id="55346-183">按一下 [資源] 清單中的 Web 應用程式資源，然後按一下 [應用程式設定] ![資源群組的螢幕擷取畫面](./media/create-website/TemplateDeployment9.png)</span><span class="sxs-lookup"><span data-stu-id="55346-183">Click the Web App resource in the Resources list and then click **Application settings** ![Screenshot of the resource group](./media/create-website/TemplateDeployment9.png)</span></span>  
9. <span data-ttu-id="55346-184">請注意出現的 Azure Cosmos DB 端點以及每個 Azure Cosmos DB 主要金鑰的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="55346-184">Note how there are application settings present for the Azure Cosmos DB endpoint and each of the Azure Cosmos DB master keys.</span></span>

    ![應用程式設定的螢幕擷取畫面](./media/create-website/TemplateDeployment10.png)  
10. <span data-ttu-id="55346-186">任意繼續瀏覽探索 Azure 入口網站，或遵循其中一個 Azure Cosmos DB [範例](http://go.microsoft.com/fwlink/?LinkID=402386)，來建立您自己的 Azure Cosmos DB 應用程式。</span><span class="sxs-lookup"><span data-stu-id="55346-186">Feel free to continue exploring the Azure Portal, or follow one of our Azure Cosmos DB [samples](http://go.microsoft.com/fwlink/?LinkID=402386) to create your own Azure Cosmos DB application.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="55346-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="55346-187">Next steps</span></span>
<span data-ttu-id="55346-188">恭喜！</span><span class="sxs-lookup"><span data-stu-id="55346-188">Congratulations!</span></span> <span data-ttu-id="55346-189">您已使用 Azure Resource Manager 範本部署了 Azure Cosmos DB、App Service Web 應用程式及範例 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="55346-189">You've deployed Azure Cosmos DB, App Service web app and a sample web application using Azure Resource Manager templates.</span></span>

* <span data-ttu-id="55346-190">若要深入了解 Azure Cosmos DB，請按一下[這裡](http://azure.com/docdb)。</span><span class="sxs-lookup"><span data-stu-id="55346-190">To learn more about Azure Cosmos DB, click [here](http://azure.com/docdb).</span></span>
* <span data-ttu-id="55346-191">若要深入了解 Azure App Service Web Apps，請按一下 [這裡](http://go.microsoft.com/fwlink/?LinkId=325362)。</span><span class="sxs-lookup"><span data-stu-id="55346-191">To learn more about Azure App Service Web apps, click [here](http://go.microsoft.com/fwlink/?LinkId=325362).</span></span>
* <span data-ttu-id="55346-192">若要深入了解 Azure 資源管理員範本，請按一下 [這裡](https://msdn.microsoft.com/library/azure/dn790549.aspx)。</span><span class="sxs-lookup"><span data-stu-id="55346-192">To learn more about Azure Resource Manager templates, click [here](https://msdn.microsoft.com/library/azure/dn790549.aspx).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="55346-193">變更的項目</span><span class="sxs-lookup"><span data-stu-id="55346-193">What's changed</span></span>
* <span data-ttu-id="55346-194">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="55346-194">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
* <span data-ttu-id="55346-195">如需從舊的入口網站變更為新入口網站的指南，請參閱： [瀏覽 Azure 傳統入口網站的參考](http://go.microsoft.com/fwlink/?LinkId=529715)</span><span class="sxs-lookup"><span data-stu-id="55346-195">For a guide to the change of the old portal to the new portal see: [Reference for navigating the Azure Classic Portal](http://go.microsoft.com/fwlink/?LinkId=529715)</span></span>

> [!NOTE]
> <span data-ttu-id="55346-196">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](http://go.microsoft.com/fwlink/?LinkId=523751)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="55346-196">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](http://go.microsoft.com/fwlink/?LinkId=523751), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="55346-197">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="55346-197">No credit cards required; no commitments.</span></span>
> 
> 

