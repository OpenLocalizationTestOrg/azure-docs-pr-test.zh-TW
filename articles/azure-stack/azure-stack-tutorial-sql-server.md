---
title: "將 SQL 資料庫提供給您的 Azure Stack 使用者 | Microsoft Docs"
description: "此教學課程說明如何安裝 SQL Server 資源提供者，並建立供應項目以讓 Azure Stack 使用者建立 SQL 資料庫。"
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
ms.openlocfilehash: bba8257bc4477f985d1a9399e65a1338d237f134
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="make-sql-databases-available-to-your-azure-stack-users"></a><span data-ttu-id="a1b41-103">將 SQL 資料庫提供給您的 Azure Stack 使用者</span><span class="sxs-lookup"><span data-stu-id="a1b41-103">Make SQL databases available to your Azure Stack users</span></span>

<span data-ttu-id="a1b41-104">身為 Azure Stack 雲端系統管理員，您可以建立供應項目以讓您的使用者 (租用戶) 建立 SQL 資料庫，以搭配其雲端原生應用程式、網站與工作負載使用。</span><span class="sxs-lookup"><span data-stu-id="a1b41-104">As an Azure Stack cloud administrator, you can create offers that let your users (tenants) create SQL databases that they can use with their cloud-native apps, websites, and workloads.</span></span> <span data-ttu-id="a1b41-105">透過將對這些自訂隨選雲端式資料庫的存取權提供給您的使用者，您可以節省其時間與資源。</span><span class="sxs-lookup"><span data-stu-id="a1b41-105">By providing these custom, on-demand, cloud-based databases to your users, you can save them time and resources.</span></span> <span data-ttu-id="a1b41-106">若要設定，您將必須：</span><span class="sxs-lookup"><span data-stu-id="a1b41-106">To set this up, you will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a1b41-107">部署 SQL Server 資源提供者</span><span class="sxs-lookup"><span data-stu-id="a1b41-107">Deploy the SQL Server resource provider</span></span>
> * <span data-ttu-id="a1b41-108">建立優惠</span><span class="sxs-lookup"><span data-stu-id="a1b41-108">Create an offer</span></span>
> * <span data-ttu-id="a1b41-109">測試供應項目</span><span class="sxs-lookup"><span data-stu-id="a1b41-109">Test the offer</span></span>

## <a name="deploy-the-sql-server-resource-provider"></a><span data-ttu-id="a1b41-110">部署 SQL Server 資源提供者</span><span class="sxs-lookup"><span data-stu-id="a1b41-110">Deploy the SQL Server resource provider</span></span>

<span data-ttu-id="a1b41-111">部署程序於[在 Azure Stack 上使用 SQL 資料庫](azure-stack-sql-resource-provider-deploy.md)文章中詳細說明，而且由下列主要步驟組成：</span><span class="sxs-lookup"><span data-stu-id="a1b41-111">The deployment process is described in detail in the [Use SQL databases on Azure Stack article](azure-stack-sql-resource-provider-deploy.md), and is comprised of the following primary steps:</span></span>

1.  <span data-ttu-id="a1b41-112">[部署 SQL 資源提供者]( azure-stack-sql-resource-provider-deploy.md#deploy-the-resource-provider)。</span><span class="sxs-lookup"><span data-stu-id="a1b41-112">[Deploy the SQL resource provider]( azure-stack-sql-resource-provider-deploy.md#deploy-the-resource-provider).</span></span>
2.  <span data-ttu-id="a1b41-113">[驗證部署]( azure-stack-sql-resource-provider-deploy.md#verify-the-deployment-using-the-azure-stack-portal)。</span><span class="sxs-lookup"><span data-stu-id="a1b41-113">[Verify the deployment]( azure-stack-sql-resource-provider-deploy.md#verify-the-deployment-using-the-azure-stack-portal).</span></span>
3.  <span data-ttu-id="a1b41-114">[透過連線到主控 SQL 伺服器以提供容量]( azure-stack-sql-resource-provider-deploy.md#provide-capacity-by-connecting-to-a-hosting-sql-server)。</span><span class="sxs-lookup"><span data-stu-id="a1b41-114">[Provide capacity by connecting to a hosting SQL server]( azure-stack-sql-resource-provider-deploy.md#provide-capacity-by-connecting-to-a-hosting-sql-server).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="a1b41-115">建立優惠</span><span class="sxs-lookup"><span data-stu-id="a1b41-115">Create an offer</span></span>

1.  <span data-ttu-id="a1b41-116">[設定配額](azure-stack-setting-quotas.md)並將它命名為 *SQLServerQuota*。</span><span class="sxs-lookup"><span data-stu-id="a1b41-116">[Set a quota](azure-stack-setting-quotas.md) and name it *SQLServerQuota*.</span></span> <span data-ttu-id="a1b41-117">選取 [命名空間] 欄位的 [Microsoft.SQLAdapter]。</span><span class="sxs-lookup"><span data-stu-id="a1b41-117">Select **Microsoft.SQLAdapter** for the **Namespace** field.</span></span>
2.  <span data-ttu-id="a1b41-118">[建立方案](azure-stack-create-plan.md)。</span><span class="sxs-lookup"><span data-stu-id="a1b41-118">[Create a plan](azure-stack-create-plan.md).</span></span> <span data-ttu-id="a1b41-119">將它命名為 *TestSQLServerPlan*，選取 [Microsoft.SQLAdapter] 服務，並選取 [SQLServerQuota] 配額。</span><span class="sxs-lookup"><span data-stu-id="a1b41-119">Name it *TestSQLServerPlan*, select the **Microsoft.SQLAdapter** service, and **SQLServerQuota** quota.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a1b41-120">若要讓使用者建立其他應用程式，方案中可能需要有其他服務。</span><span class="sxs-lookup"><span data-stu-id="a1b41-120">To let users create other apps, other services might be required in the plan.</span></span> <span data-ttu-id="a1b41-121">例如，Azure Functions 要求方案必須包括 **Microsoft.Storage** 服務，而 Wordpress 則需要 **Microsoft.MySQLAdapter**。</span><span class="sxs-lookup"><span data-stu-id="a1b41-121">For example, Azure Functions requires that the plan include the **Microsoft.Storage** service, while Wordpress requires **Microsoft.MySQLAdapter**.</span></span>
    > 
    >

3.  <span data-ttu-id="a1b41-122">[建立供應項目](azure-stack-create-offer.md)，將它命名為 **TestSQLServerOffer**，然後選取 [TestSQLServerPlan] 方案。</span><span class="sxs-lookup"><span data-stu-id="a1b41-122">[Create an offer](azure-stack-create-offer.md), name it **TestSQLServerOffer** and select the **TestSQLServerPlan** plan.</span></span>

## <a name="test-the-offer"></a><span data-ttu-id="a1b41-123">測試供應項目</span><span class="sxs-lookup"><span data-stu-id="a1b41-123">Test the offer</span></span>

<span data-ttu-id="a1b41-124">既然您已部署 SQL Server 資源提供者並建立供應項目，您能以使用者身分登入並訂閱該供應項目，然後建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="a1b41-124">Now that you've deployed the SQL Server resource provider and created an offer, you can sign in as a user, subscribe to the offer, and create a database.</span></span>

### <a name="subscribe-to-the-offer"></a><span data-ttu-id="a1b41-125">訂閱該供應項目</span><span class="sxs-lookup"><span data-stu-id="a1b41-125">Subscribe to the offer</span></span>
1. <span data-ttu-id="a1b41-126">以租用戶身分登入 Azure Stack 入口網站 (https://portal.local.azurestack.external)。</span><span class="sxs-lookup"><span data-stu-id="a1b41-126">Sign in to the Azure Stack portal (https://portal.local.azurestack.external) as a tenant.</span></span>
2. <span data-ttu-id="a1b41-127">按一下 [取得訂用帳戶]，然後在 [顯示名稱] 下輸入 **TestSQLServerSubscription**。</span><span class="sxs-lookup"><span data-stu-id="a1b41-127">Click **Get a subscription** and then type **TestSQLServerSubscription** under **Display Name**.</span></span>
3. <span data-ttu-id="a1b41-128">按一下 [選取服務] > [TestSQLServerOffer] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="a1b41-128">Click **Select an offer** > **TestSQLServerOffer** > **Create**.</span></span>
4. <span data-ttu-id="a1b41-129">按一下 [更多服務] > [訂用帳戶] > [TestSQLServerSubscription] > [資源提供者]。</span><span class="sxs-lookup"><span data-stu-id="a1b41-129">Click **More services** > **Subscriptions** > **TestSQLServerSubscription** > **Resource providers**.</span></span>
5. <span data-ttu-id="a1b41-130">按一下 **Microsoft.SQLAdapter** 提供者旁的 [註冊]。</span><span class="sxs-lookup"><span data-stu-id="a1b41-130">Click **Register** next to the **Microsoft.SQLAdapter** provider.</span></span>

### <a name="create-a-sql-database"></a><span data-ttu-id="a1b41-131">建立 SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="a1b41-131">Create a SQL database</span></span>

1. <span data-ttu-id="a1b41-132">按一下 [+] > [資料 + 儲存體] > [SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="a1b41-132">Click **+** > **Data + Storage** > **SQL Database**.</span></span>
2. <span data-ttu-id="a1b41-133">將欄位維持為預設值，或您可以使用這些範例：</span><span class="sxs-lookup"><span data-stu-id="a1b41-133">Leave the defaults for the fields, or you can use these examples:</span></span>
    - <span data-ttu-id="a1b41-134">**資料庫名稱**：SQLdb</span><span class="sxs-lookup"><span data-stu-id="a1b41-134">**Database Name**: SQLdb</span></span>
    - <span data-ttu-id="a1b41-135">**大小上限 (MB)**：100</span><span class="sxs-lookup"><span data-stu-id="a1b41-135">**Max Size in MB**: 100</span></span>
    - <span data-ttu-id="a1b41-136">**訂用帳戶**：TestSQLOffer</span><span class="sxs-lookup"><span data-stu-id="a1b41-136">**Subscription**: TestSQLOffer</span></span>
    - <span data-ttu-id="a1b41-137">**資源群組**：SQL-RG</span><span class="sxs-lookup"><span data-stu-id="a1b41-137">**Resource Group**: SQL-RG</span></span>
3. <span data-ttu-id="a1b41-138">按一下 [登入設定]，輸入資料庫認證，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a1b41-138">Click **Login Settings**, enter credentials for the database, and then click **OK**.</span></span>
4. <span data-ttu-id="a1b41-139">按一下 [SKU] > 選取您為 SQL 主控伺服器 建立的 SQL SKU > [確定]。</span><span class="sxs-lookup"><span data-stu-id="a1b41-139">Click **SKU** > select the SQL SKU that you created for the SQL Hosting Server > **OK**.</span></span>
5. <span data-ttu-id="a1b41-140">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a1b41-140">Click **Create**.</span></span>

<span data-ttu-id="a1b41-141">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="a1b41-141">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a1b41-142">部署 SQL Server 資源提供者</span><span class="sxs-lookup"><span data-stu-id="a1b41-142">Deploy the SQL Server resource provider</span></span>
> * <span data-ttu-id="a1b41-143">建立優惠</span><span class="sxs-lookup"><span data-stu-id="a1b41-143">Create an offer</span></span>
> * <span data-ttu-id="a1b41-144">測試供應項目</span><span class="sxs-lookup"><span data-stu-id="a1b41-144">Test the offer</span></span>

<span data-ttu-id="a1b41-145">請前進到下一個教學課程，以了解如何：</span><span class="sxs-lookup"><span data-stu-id="a1b41-145">Advance to the next tutorial to learn how to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a1b41-146">將 Web、行動裝置與 API 應用程式提供給您的使用者</span><span class="sxs-lookup"><span data-stu-id="a1b41-146">Make web, mobile, and API apps available to your users</span></span>]( azure-stack-tutorial-app-service.md)

