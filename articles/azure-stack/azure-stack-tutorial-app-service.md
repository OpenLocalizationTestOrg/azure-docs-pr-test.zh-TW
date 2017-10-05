---
title: "將 Web、行動裝置與 API 應用程式提供給您的 Azure Stack 使用者 | Microsoft Docs"
description: "此教學課程說明如何安裝 App Service 資源提供者，並建立供應項目以為您的 Azure Stack 使用者提供建立 Web、行動裝置與 API 應用程式的能力。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/03/2017
ms.author: erikje
ms.custom: mvc
ms.openlocfilehash: 11ecaa8ec017a9eb1285928e3d3d367ddfc43022
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="make-web-mobile-and-api-apps-available-to-your-azure-stack-users"></a><span data-ttu-id="6cc47-103">將 Web、行動裝置與 API 應用程式提供給您的 Azure Stack 使用者</span><span class="sxs-lookup"><span data-stu-id="6cc47-103">Make web, mobile, and API apps available to your Azure Stack users</span></span>

<span data-ttu-id="6cc47-104">身為 Azure Stack 雲端系統管理員，您可以建立供應項目，以讓您的使用者 (租用戶) 建立 Azure Functions 與 Web、行動裝置與 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6cc47-104">As an Azure Stack cloud administrator, you can create offers that let your users (tenants) create Azure Functions and web, mobile, and API applications.</span></span> <span data-ttu-id="6cc47-105">透過將對這些隨選雲端式應用程式的存取權提供給您的使用者，您可以節省其時間與資源。</span><span class="sxs-lookup"><span data-stu-id="6cc47-105">By providing access to these on-demand, cloud-based apps to your users, you can save them time and resources.</span></span> <span data-ttu-id="6cc47-106">若要設定，您將必須：</span><span class="sxs-lookup"><span data-stu-id="6cc47-106">To set this up, you will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6cc47-107">部署 App Service 資源提供者</span><span class="sxs-lookup"><span data-stu-id="6cc47-107">Deploy the App Service resource provider</span></span>
> * <span data-ttu-id="6cc47-108">建立優惠</span><span class="sxs-lookup"><span data-stu-id="6cc47-108">Create an offer</span></span>
> * <span data-ttu-id="6cc47-109">測試供應項目</span><span class="sxs-lookup"><span data-stu-id="6cc47-109">Test the offer</span></span>

## <a name="deploy-the-app-service-resource-provider"></a><span data-ttu-id="6cc47-110">部署 App Service 資源提供者</span><span class="sxs-lookup"><span data-stu-id="6cc47-110">Deploy the App Service resource provider</span></span>

1. <span data-ttu-id="6cc47-111">[準備 Azure Stack 開發套件主機](azure-stack-app-service-before-you-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="6cc47-111">[Prepare the Azure Stack Development Kit host](azure-stack-app-service-before-you-get-started.md).</span></span> <span data-ttu-id="6cc47-112">這包括部署 SQL Server 資源提供者，而這是建立某些應用程式的必要條件。</span><span class="sxs-lookup"><span data-stu-id="6cc47-112">This includes deploying the SQL Server resource provider, which is required for creating some apps.</span></span>
2. <span data-ttu-id="6cc47-113">[下載安裝程式與協助程式指令碼](azure-stack-app-service-deploy.md#download-the-required-components)。</span><span class="sxs-lookup"><span data-stu-id="6cc47-113">[Download the installer and helper scripts](azure-stack-app-service-deploy.md#download-the-required-components).</span></span>
3. <span data-ttu-id="6cc47-114">[執行協助程式指令碼以建立必要憑證](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack)。</span><span class="sxs-lookup"><span data-stu-id="6cc47-114">[Run the helper script to create required certificates](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack).</span></span>
4. <span data-ttu-id="6cc47-115">[安裝 App Service 資源提供者](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack) (安裝資源提供者並讓所有背景工作角色出現將需要數小時)。</span><span class="sxs-lookup"><span data-stu-id="6cc47-115">[Install the App Service resource provider](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack) (it will take a couple hours to install and for all the worker roles to appear).</span></span>
5. <span data-ttu-id="6cc47-116">[驗證安裝](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation)。</span><span class="sxs-lookup"><span data-stu-id="6cc47-116">[Validate the installation](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="6cc47-117">建立優惠</span><span class="sxs-lookup"><span data-stu-id="6cc47-117">Create an offer</span></span>

<span data-ttu-id="6cc47-118">例如，您可以建立供應項目，以讓使用者 建立 DNN Web 內容管理系統。</span><span class="sxs-lookup"><span data-stu-id="6cc47-118">As an example, you can create an offer that lets users create DNN web content management systems.</span></span> <span data-ttu-id="6cc47-119">它需要 SQL Server 服務 (您已透過安裝 SQL Server 資源提供者而啟用)。</span><span class="sxs-lookup"><span data-stu-id="6cc47-119">It requires the SQL Server service which you already enabled by installing the SQL Server resource provider.</span></span>

1.  <span data-ttu-id="6cc47-120">[設定配額](azure-stack-setting-quotas.md)並將它命名為 *AppServiceQuota*。</span><span class="sxs-lookup"><span data-stu-id="6cc47-120">[Set a quota](azure-stack-setting-quotas.md) and name it *AppServiceQuota*.</span></span> <span data-ttu-id="6cc47-121">選取 [命名空間] 欄位的 [Microsoft.Web]。</span><span class="sxs-lookup"><span data-stu-id="6cc47-121">Select **Microsoft.Web** for the **Namespace** field.</span></span>
2.  <span data-ttu-id="6cc47-122">[建立方案](azure-stack-create-plan.md)。</span><span class="sxs-lookup"><span data-stu-id="6cc47-122">[Create a plan](azure-stack-create-plan.md).</span></span> <span data-ttu-id="6cc47-123">將它命名為 *TestAppServicePlan*，選取 [Microsoft.SQL] 服務，並選取 [AppService 配額] 配額。</span><span class="sxs-lookup"><span data-stu-id="6cc47-123">Name it *TestAppServicePlan*, select the the **Microsoft.SQL** service, and **AppService Quota** quota.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6cc47-124">若要讓使用者建立其他應用程式，方案中可能需要有其他服務。</span><span class="sxs-lookup"><span data-stu-id="6cc47-124">To let users create other apps, other services might be required in the plan.</span></span> <span data-ttu-id="6cc47-125">例如，Azure Functions 要求方案必須包括 **Microsoft.Storage** 服務，而 Wordpress 則需要 **Microsoft.MySQL**。</span><span class="sxs-lookup"><span data-stu-id="6cc47-125">For example, Azure Functions requires that the plan     include the **Microsoft.Storage** service, while Wordpress requires **Microsoft.MySQL**.</span></span>
    > 
    >

3.  <span data-ttu-id="6cc47-126">[建立供應項目](azure-stack-create-offer.md)，將它命名為 **TestAppServiceOffer**，然後選取 [TestAppServicePlan] 方案。</span><span class="sxs-lookup"><span data-stu-id="6cc47-126">[Create an offer](azure-stack-create-offer.md), name it **TestAppServiceOffer** and select the **TestAppServicePlan** plan.</span></span>

## <a name="test-the-offer"></a><span data-ttu-id="6cc47-127">測試供應項目</span><span class="sxs-lookup"><span data-stu-id="6cc47-127">Test the offer</span></span>

<span data-ttu-id="6cc47-128">既然您已部署 App Service 資源提供者並建立供應項目，您能以使用者身分登入並訂閱該供應項目，然後建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="6cc47-128">Now that you've deployed the App Service resource provider and created an offer, you can sign in as a user, subscribe to the offer, and create an app.</span></span> <span data-ttu-id="6cc47-129">針對此範例，我們將建立 DNN 平台內容管理系統。</span><span class="sxs-lookup"><span data-stu-id="6cc47-129">For this example, we'll create a DNN Platform content management system.</span></span> <span data-ttu-id="6cc47-130">您必須先建立 SQL 資料庫，然後再建立 DNN Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6cc47-130">You must first create a SQL database and then the DNN web app.</span></span>

### <a name="subscribe-to-the-offer"></a><span data-ttu-id="6cc47-131">訂閱該供應項目</span><span class="sxs-lookup"><span data-stu-id="6cc47-131">Subscribe to the offer</span></span>
1. <span data-ttu-id="6cc47-132">以租用戶身分登入 Azure Stack 入口網站 (https://portal.local.azurestack.external)。</span><span class="sxs-lookup"><span data-stu-id="6cc47-132">Sign in to the Azure Stack portal (https://portal.local.azurestack.external) as a tenant.</span></span>
2. <span data-ttu-id="6cc47-133">按一下 [取得訂用帳戶] > 在 [顯示名稱] 下輸入 **TestAppServiceSubscription** > [選取服務] > [TestAppServiceOffer] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="6cc47-133">Click **Get a subscription** > type **TestAppServiceSubscription** under **Display Name** > **Select an offer** > **TestAppServiceOffer** > **Create**.</span></span>

### <a name="create-a-sql-database"></a><span data-ttu-id="6cc47-134">建立 SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="6cc47-134">Create a SQL database</span></span>

1. <span data-ttu-id="6cc47-135">按一下 [+] > [資料 + 儲存體] > [SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="6cc47-135">Click **+** > **Data + Storage** > **SQL Database**.</span></span>
2. <span data-ttu-id="6cc47-136">將欄位維持為預設值，下列欄位除外：</span><span class="sxs-lookup"><span data-stu-id="6cc47-136">Leave the defaults for the fields, except as follows:</span></span>
    - <span data-ttu-id="6cc47-137">**資料庫名稱**：DNNdb</span><span class="sxs-lookup"><span data-stu-id="6cc47-137">**Database Name**: DNNdb</span></span>
    - <span data-ttu-id="6cc47-138">**大小上限 (MB)**：100</span><span class="sxs-lookup"><span data-stu-id="6cc47-138">**Max Size in MB**: 100</span></span>
    - <span data-ttu-id="6cc47-139">**訂用帳戶**：TestAppServiceOffer</span><span class="sxs-lookup"><span data-stu-id="6cc47-139">**Subscription**: TestAppServiceOffer</span></span>
    - <span data-ttu-id="6cc47-140">**資源群組**：DNN-RG</span><span class="sxs-lookup"><span data-stu-id="6cc47-140">**Resource Group**: DNN-RG</span></span>
3. <span data-ttu-id="6cc47-141">按一下 [登入設定]輸入資料庫認證，然後按一下 [確定]**OK**。</span><span class="sxs-lookup"><span data-stu-id="6cc47-141">Click **Login Settings**, enter credentials for the database, and then click **OK**.</span></span> <span data-ttu-id="6cc47-142">稍後您將在這些步驟中用到這些認證。</span><span class="sxs-lookup"><span data-stu-id="6cc47-142">You'll use these credentials later in these steps.</span></span>
4. <span data-ttu-id="6cc47-143">按一下 [SKU] > 選取您為 SQL 主控伺服器 建立的 SQL SKU > [確定]。</span><span class="sxs-lookup"><span data-stu-id="6cc47-143">Click **SKU** > select the SQL SKU that you created for the SQL Hosting Server > **OK**.</span></span>
5. <span data-ttu-id="6cc47-144">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6cc47-144">Click **Create**.</span></span>

### <a name="create-a-dnn-app"></a><span data-ttu-id="6cc47-145">建立 DNN 應用程式</span><span class="sxs-lookup"><span data-stu-id="6cc47-145">Create a DNN app</span></span>    

1. <span data-ttu-id="6cc47-146">按一下 [+] > [查看全部] > [DNN 平台預覽] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="6cc47-146">Click **+** > **See all** > **DNN Platform preview** > **Create**.</span></span>
2. <span data-ttu-id="6cc47-147">在 [應用程式名稱] 下輸入 *DNNapp*，然後在 [訂用帳戶] 下選取 [TestAppServiceOffer]。</span><span class="sxs-lookup"><span data-stu-id="6cc47-147">Type *DNNapp* under **App name** and select **TestAppServiceOffer** under **Subscription**.</span></span>
3. <span data-ttu-id="6cc47-148">按一下 [設定必要設定] > [新建] > 輸入 [App Service 方案] 名稱。</span><span class="sxs-lookup"><span data-stu-id="6cc47-148">Click **Configure required settings** > **Create New** > type an **App Service plan** name.</span></span>
4. <span data-ttu-id="6cc47-149">按一下 [定價層] > [F1 免費] > [選取] > [確定]。</span><span class="sxs-lookup"><span data-stu-id="6cc47-149">Click **Pricing tier** > **F1 Free** > **Select** > **OK**.</span></span>
5. <span data-ttu-id="6cc47-150">按一下 [資料庫] 並輸入您稍早建立之 SQL 資料庫的資訊。</span><span class="sxs-lookup"><span data-stu-id="6cc47-150">Click **Database** and enter the information for the SQL database you created earlier.</span></span>
6. <span data-ttu-id="6cc47-151">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6cc47-151">Click **Create**.</span></span>

<span data-ttu-id="6cc47-152">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="6cc47-152">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6cc47-153">部署 App Service 資源提供者</span><span class="sxs-lookup"><span data-stu-id="6cc47-153">Deploy the App Service resource provider</span></span>
> * <span data-ttu-id="6cc47-154">建立優惠</span><span class="sxs-lookup"><span data-stu-id="6cc47-154">Create an offer</span></span>
> * <span data-ttu-id="6cc47-155">測試供應項目</span><span class="sxs-lookup"><span data-stu-id="6cc47-155">Test the offer</span></span>

<span data-ttu-id="6cc47-156">請前進到下一個教學課程，以了解如何：</span><span class="sxs-lookup"><span data-stu-id="6cc47-156">Advance to the next tutorial to learn how to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6cc47-157">將應用程式部署到 Azure 和 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="6cc47-157">Deploy apps to Azure and Azure Stack</span></span>](azure-stack-solution-pipeline.md)
