---
title: "aaaMake web、 mobile 及 API 應用程式可用 tooyour Azure 堆疊使用者 |Microsoft 文件"
description: "教學課程 tooinstall hello 應用程式服務資源提供者，並建立提供項目，讓您的 Azure 堆疊使用者 hello 能力 toocreate web、 行動裝置版和 API 應用程式。"
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
ms.openlocfilehash: 62b86cf6288b8f629bc92dade003c712fe523187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="make-web-mobile-and-api-apps-available-tooyour-azure-stack-users"></a><span data-ttu-id="57177-103">讓 web、 行動裝置、 應用程式開發介面應用程式可用 tooyour Azure 堆疊使用者</span><span class="sxs-lookup"><span data-stu-id="57177-103">Make web, mobile, and API apps available tooyour Azure Stack users</span></span>

<span data-ttu-id="57177-104">身為 Azure Stack 雲端系統管理員，您可以建立供應項目，以讓您的使用者 (租用戶) 建立 Azure Functions 與 Web、行動裝置與 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="57177-104">As an Azure Stack cloud administrator, you can create offers that let your users (tenants) create Azure Functions and web, mobile, and API applications.</span></span> <span data-ttu-id="57177-105">藉由提供存取 toothese tooyour 隨、 以雲端為基礎的應用程式的使用者，您可以將它們儲存時間和資源。</span><span class="sxs-lookup"><span data-stu-id="57177-105">By providing access toothese on-demand, cloud-based apps tooyour users, you can save them time and resources.</span></span> <span data-ttu-id="57177-106">tooset 最，您將會：</span><span class="sxs-lookup"><span data-stu-id="57177-106">tooset this up, you will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="57177-107">部署 hello 應用程式服務資源提供者</span><span class="sxs-lookup"><span data-stu-id="57177-107">Deploy hello App Service resource provider</span></span>
> * <span data-ttu-id="57177-108">建立優惠</span><span class="sxs-lookup"><span data-stu-id="57177-108">Create an offer</span></span>
> * <span data-ttu-id="57177-109">測試 hello 優惠</span><span class="sxs-lookup"><span data-stu-id="57177-109">Test hello offer</span></span>

## <a name="deploy-hello-app-service-resource-provider"></a><span data-ttu-id="57177-110">部署 hello 應用程式服務資源提供者</span><span class="sxs-lookup"><span data-stu-id="57177-110">Deploy hello App Service resource provider</span></span>

1. <span data-ttu-id="57177-111">[準備 hello Azure 堆疊開發套件主機](azure-stack-app-service-before-you-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="57177-111">[Prepare hello Azure Stack Development Kit host](azure-stack-app-service-before-you-get-started.md).</span></span> <span data-ttu-id="57177-112">這包括部署 hello SQL Server 資源提供者，才能建立某些應用程式。</span><span class="sxs-lookup"><span data-stu-id="57177-112">This includes deploying hello SQL Server resource provider, which is required for creating some apps.</span></span>
2. <span data-ttu-id="57177-113">[下載 hello installer 和協助程式指令碼](azure-stack-app-service-deploy.md#download-the-required-components)。</span><span class="sxs-lookup"><span data-stu-id="57177-113">[Download hello installer and helper scripts](azure-stack-app-service-deploy.md#download-the-required-components).</span></span>
3. <span data-ttu-id="57177-114">[執行 hello helper 指令碼所需的 toocreate 憑證](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack)。</span><span class="sxs-lookup"><span data-stu-id="57177-114">[Run hello helper script toocreate required certificates](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack).</span></span>
4. <span data-ttu-id="57177-115">[安裝應用程式服務資源提供者 hello](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack) (花費幾小時 tooinstall，在所有 hello 背景工作角色 tooappear)。</span><span class="sxs-lookup"><span data-stu-id="57177-115">[Install hello App Service resource provider](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack) (it will take a couple hours tooinstall and for all hello worker roles tooappear).</span></span>
5. <span data-ttu-id="57177-116">[驗證 hello 安裝](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation)。</span><span class="sxs-lookup"><span data-stu-id="57177-116">[Validate hello installation](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="57177-117">建立優惠</span><span class="sxs-lookup"><span data-stu-id="57177-117">Create an offer</span></span>

<span data-ttu-id="57177-118">例如，您可以建立供應項目，以讓使用者 建立 DNN Web 內容管理系統。</span><span class="sxs-lookup"><span data-stu-id="57177-118">As an example, you can create an offer that lets users create DNN web content management systems.</span></span> <span data-ttu-id="57177-119">它需要 hello SQL Server 服務已經啟用安裝 hello SQL Server 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="57177-119">It requires hello SQL Server service which you already enabled by installing hello SQL Server resource provider.</span></span>

1.  <span data-ttu-id="57177-120">[設定配額](azure-stack-setting-quotas.md)並將它命名為 *AppServiceQuota*。</span><span class="sxs-lookup"><span data-stu-id="57177-120">[Set a quota](azure-stack-setting-quotas.md) and name it *AppServiceQuota*.</span></span> <span data-ttu-id="57177-121">選取**Microsoft.Web** hello**命名空間**欄位。</span><span class="sxs-lookup"><span data-stu-id="57177-121">Select **Microsoft.Web** for hello **Namespace** field.</span></span>
2.  <span data-ttu-id="57177-122">[建立方案](azure-stack-create-plan.md)。</span><span class="sxs-lookup"><span data-stu-id="57177-122">[Create a plan](azure-stack-create-plan.md).</span></span> <span data-ttu-id="57177-123">命名*TestAppServicePlan*，選取 hello hello **Microsoft.SQL**服務，以及**AppService 配額**配額。</span><span class="sxs-lookup"><span data-stu-id="57177-123">Name it *TestAppServicePlan*, select hello hello **Microsoft.SQL** service, and **AppService Quota** quota.</span></span>

    > [!NOTE]
    > <span data-ttu-id="57177-124">toolet 使用者建立其他應用程式，可能需要其他服務 hello 計劃中。</span><span class="sxs-lookup"><span data-stu-id="57177-124">toolet users create other apps, other services might be required in hello plan.</span></span> <span data-ttu-id="57177-125">例如，Azure 函式需要該 hello 計劃包含 hello **Microsoft.Storage**服務，而 Wordpress **Microsoft.MySQL**。</span><span class="sxs-lookup"><span data-stu-id="57177-125">For example, Azure Functions requires that hello plan     include hello **Microsoft.Storage** service, while Wordpress requires **Microsoft.MySQL**.</span></span>
    > 
    >

3.  <span data-ttu-id="57177-126">[建立優惠](azure-stack-create-offer.md)，其命名**TestAppServiceOffer**和選取 hello **TestAppServicePlan**計劃。</span><span class="sxs-lookup"><span data-stu-id="57177-126">[Create an offer](azure-stack-create-offer.md), name it **TestAppServiceOffer** and select hello **TestAppServicePlan** plan.</span></span>

## <a name="test-hello-offer"></a><span data-ttu-id="57177-127">測試 hello 優惠</span><span class="sxs-lookup"><span data-stu-id="57177-127">Test hello offer</span></span>

<span data-ttu-id="57177-128">現在您已部署的 hello 應用程式服務資源提供者，以及建立提供項目時，您可以登入的使用者身分，訂閱 toohello 供應項目，並建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="57177-128">Now that you've deployed hello App Service resource provider and created an offer, you can sign in as a user, subscribe toohello offer, and create an app.</span></span> <span data-ttu-id="57177-129">針對此範例，我們將建立 DNN 平台內容管理系統。</span><span class="sxs-lookup"><span data-stu-id="57177-129">For this example, we'll create a DNN Platform content management system.</span></span> <span data-ttu-id="57177-130">您必須先建立 SQL 資料庫，然後 hello DNN web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="57177-130">You must first create a SQL database and then hello DNN web app.</span></span>

### <a name="subscribe-toohello-offer"></a><span data-ttu-id="57177-131">訂閱 toohello 供應項目</span><span class="sxs-lookup"><span data-stu-id="57177-131">Subscribe toohello offer</span></span>
1. <span data-ttu-id="57177-132">登入 toohello 堆疊 Azure 入口網站 (https://portal.local.azurestack.external) 做為租用戶。</span><span class="sxs-lookup"><span data-stu-id="57177-132">Sign in toohello Azure Stack portal (https://portal.local.azurestack.external) as a tenant.</span></span>
2. <span data-ttu-id="57177-133">按一下 [取得訂用帳戶] > 在 [顯示名稱] 下輸入 **TestAppServiceSubscription** > [選取服務] > [TestAppServiceOffer] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="57177-133">Click **Get a subscription** > type **TestAppServiceSubscription** under **Display Name** > **Select an offer** > **TestAppServiceOffer** > **Create**.</span></span>

### <a name="create-a-sql-database"></a><span data-ttu-id="57177-134">建立 SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="57177-134">Create a SQL database</span></span>

1. <span data-ttu-id="57177-135">按一下 [+] > [資料 + 儲存體] > [SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="57177-135">Click **+** > **Data + Storage** > **SQL Database**.</span></span>
2. <span data-ttu-id="57177-136">保留 hello hello 欄位的預設值以外，如下所示：</span><span class="sxs-lookup"><span data-stu-id="57177-136">Leave hello defaults for hello fields, except as follows:</span></span>
    - <span data-ttu-id="57177-137">**資料庫名稱**：DNNdb</span><span class="sxs-lookup"><span data-stu-id="57177-137">**Database Name**: DNNdb</span></span>
    - <span data-ttu-id="57177-138">**大小上限 (MB)**：100</span><span class="sxs-lookup"><span data-stu-id="57177-138">**Max Size in MB**: 100</span></span>
    - <span data-ttu-id="57177-139">**訂用帳戶**：TestAppServiceOffer</span><span class="sxs-lookup"><span data-stu-id="57177-139">**Subscription**: TestAppServiceOffer</span></span>
    - <span data-ttu-id="57177-140">**資源群組**：DNN-RG</span><span class="sxs-lookup"><span data-stu-id="57177-140">**Resource Group**: DNN-RG</span></span>
3. <span data-ttu-id="57177-141">按一下**登入設定**hello 資料庫中，輸入認證，然後按**確定**。</span><span class="sxs-lookup"><span data-stu-id="57177-141">Click **Login Settings**, enter credentials for hello database, and then click **OK**.</span></span> <span data-ttu-id="57177-142">稍後您將在這些步驟中用到這些認證。</span><span class="sxs-lookup"><span data-stu-id="57177-142">You'll use these credentials later in these steps.</span></span>
4. <span data-ttu-id="57177-143">按一下**SKU** > 選取 hello 建立 hello SQL 主控伺服器的 SQL SKU >**確定**。</span><span class="sxs-lookup"><span data-stu-id="57177-143">Click **SKU** > select hello SQL SKU that you created for hello SQL Hosting Server > **OK**.</span></span>
5. <span data-ttu-id="57177-144">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="57177-144">Click **Create**.</span></span>

### <a name="create-a-dnn-app"></a><span data-ttu-id="57177-145">建立 DNN 應用程式</span><span class="sxs-lookup"><span data-stu-id="57177-145">Create a DNN app</span></span>    

1. <span data-ttu-id="57177-146">按一下 [+] > [查看全部] > [DNN 平台預覽] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="57177-146">Click **+** > **See all** > **DNN Platform preview** > **Create**.</span></span>
2. <span data-ttu-id="57177-147">在 [應用程式名稱] 下輸入 *DNNapp*，然後在 [訂用帳戶] 下選取 [TestAppServiceOffer]。</span><span class="sxs-lookup"><span data-stu-id="57177-147">Type *DNNapp* under **App name** and select **TestAppServiceOffer** under **Subscription**.</span></span>
3. <span data-ttu-id="57177-148">按一下 [設定必要設定] > [新建] > 輸入 [App Service 方案] 名稱。</span><span class="sxs-lookup"><span data-stu-id="57177-148">Click **Configure required settings** > **Create New** > type an **App Service plan** name.</span></span>
4. <span data-ttu-id="57177-149">按一下 [定價層] > [F1 免費] > [選取] > [確定]。</span><span class="sxs-lookup"><span data-stu-id="57177-149">Click **Pricing tier** > **F1 Free** > **Select** > **OK**.</span></span>
5. <span data-ttu-id="57177-150">按一下**資料庫**並輸入您稍早建立的 hello 資訊 hello SQL database。</span><span class="sxs-lookup"><span data-stu-id="57177-150">Click **Database** and enter hello information for hello SQL database you created earlier.</span></span>
6. <span data-ttu-id="57177-151">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="57177-151">Click **Create**.</span></span>

<span data-ttu-id="57177-152">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="57177-152">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="57177-153">部署 hello 應用程式服務資源提供者</span><span class="sxs-lookup"><span data-stu-id="57177-153">Deploy hello App Service resource provider</span></span>
> * <span data-ttu-id="57177-154">建立優惠</span><span class="sxs-lookup"><span data-stu-id="57177-154">Create an offer</span></span>
> * <span data-ttu-id="57177-155">測試 hello 優惠</span><span class="sxs-lookup"><span data-stu-id="57177-155">Test hello offer</span></span>

<span data-ttu-id="57177-156">如何前進 toohello 下一個教學課程 toolearn 至：</span><span class="sxs-lookup"><span data-stu-id="57177-156">Advance toohello next tutorial toolearn how to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="57177-157">部署應用程式 tooAzure 和 Azure 堆疊</span><span class="sxs-lookup"><span data-stu-id="57177-157">Deploy apps tooAzure and Azure Stack</span></span>](azure-stack-solution-pipeline.md)
