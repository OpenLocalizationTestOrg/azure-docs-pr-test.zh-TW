---
title: "aaaMake SQL 資料庫可用 tooyour Azure 堆疊使用者 |Microsoft 文件"
description: "教學課程 tooinstall hello SQL Server 資源提供者，並建立提供項目，讓 Azure 堆疊使用者可以建立 SQL 資料庫。"
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
ms.openlocfilehash: 778513ba982981895afe2d57b3b5dda71ead8886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="make-sql-databases-available-tooyour-azure-stack-users"></a><span data-ttu-id="584e1-103">將 SQL 資料庫可用 tooyour Azure 堆疊使用者</span><span class="sxs-lookup"><span data-stu-id="584e1-103">Make SQL databases available tooyour Azure Stack users</span></span>

<span data-ttu-id="584e1-104">身為 Azure Stack 雲端系統管理員，您可以建立供應項目以讓您的使用者 (租用戶) 建立 SQL 資料庫，以搭配其雲端原生應用程式、網站與工作負載使用。</span><span class="sxs-lookup"><span data-stu-id="584e1-104">As an Azure Stack cloud administrator, you can create offers that let your users (tenants) create SQL databases that they can use with their cloud-native apps, websites, and workloads.</span></span> <span data-ttu-id="584e1-105">藉由提供這些自訂、 隨、 以雲端為基礎的資料庫 tooyour 使用者，您可以將它們儲存時間和資源。</span><span class="sxs-lookup"><span data-stu-id="584e1-105">By providing these custom, on-demand, cloud-based databases tooyour users, you can save them time and resources.</span></span> <span data-ttu-id="584e1-106">tooset 最，您將會：</span><span class="sxs-lookup"><span data-stu-id="584e1-106">tooset this up, you will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="584e1-107">部署 hello SQL Server 資源提供者</span><span class="sxs-lookup"><span data-stu-id="584e1-107">Deploy hello SQL Server resource provider</span></span>
> * <span data-ttu-id="584e1-108">建立優惠</span><span class="sxs-lookup"><span data-stu-id="584e1-108">Create an offer</span></span>
> * <span data-ttu-id="584e1-109">測試 hello 優惠</span><span class="sxs-lookup"><span data-stu-id="584e1-109">Test hello offer</span></span>

## <a name="deploy-hello-sql-server-resource-provider"></a><span data-ttu-id="584e1-110">部署 hello SQL Server 資源提供者</span><span class="sxs-lookup"><span data-stu-id="584e1-110">Deploy hello SQL Server resource provider</span></span>

<span data-ttu-id="584e1-111">hello 部署程序中有詳細說明在 hello [Azure 堆疊發行項上的使用 SQL 資料庫](azure-stack-sql-resource-provider-deploy.md)，包含下列主要步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="584e1-111">hello deployment process is described in detail in hello [Use SQL databases on Azure Stack article](azure-stack-sql-resource-provider-deploy.md), and is comprised of hello following primary steps:</span></span>

1.  <span data-ttu-id="584e1-112">[部署 hello SQL 資源提供者]( azure-stack-sql-resource-provider-deploy.md#deploy-the-resource-provider)。</span><span class="sxs-lookup"><span data-stu-id="584e1-112">[Deploy hello SQL resource provider]( azure-stack-sql-resource-provider-deploy.md#deploy-the-resource-provider).</span></span>
2.  <span data-ttu-id="584e1-113">[確認 hello 部署]( azure-stack-sql-resource-provider-deploy.md#verify-the-deployment-using-the-azure-stack-portal)。</span><span class="sxs-lookup"><span data-stu-id="584e1-113">[Verify hello deployment]( azure-stack-sql-resource-provider-deploy.md#verify-the-deployment-using-the-azure-stack-portal).</span></span>
3.  <span data-ttu-id="584e1-114">[藉由連接 tooa 主控 SQL server 提供的容量]( azure-stack-sql-resource-provider-deploy.md#provide-capacity-by-connecting-to-a-hosting-sql-server)。</span><span class="sxs-lookup"><span data-stu-id="584e1-114">[Provide capacity by connecting tooa hosting SQL server]( azure-stack-sql-resource-provider-deploy.md#provide-capacity-by-connecting-to-a-hosting-sql-server).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="584e1-115">建立優惠</span><span class="sxs-lookup"><span data-stu-id="584e1-115">Create an offer</span></span>

1.  <span data-ttu-id="584e1-116">[設定配額](azure-stack-setting-quotas.md)並將它命名為 *SQLServerQuota*。</span><span class="sxs-lookup"><span data-stu-id="584e1-116">[Set a quota](azure-stack-setting-quotas.md) and name it *SQLServerQuota*.</span></span> <span data-ttu-id="584e1-117">選取**Microsoft.SQLAdapter** hello**命名空間**欄位。</span><span class="sxs-lookup"><span data-stu-id="584e1-117">Select **Microsoft.SQLAdapter** for hello **Namespace** field.</span></span>
2.  <span data-ttu-id="584e1-118">[建立方案](azure-stack-create-plan.md)。</span><span class="sxs-lookup"><span data-stu-id="584e1-118">[Create a plan](azure-stack-create-plan.md).</span></span> <span data-ttu-id="584e1-119">命名*TestSQLServerPlan*，選取 hello **Microsoft.SQLAdapter**服務，以及**SQLServerQuota**配額。</span><span class="sxs-lookup"><span data-stu-id="584e1-119">Name it *TestSQLServerPlan*, select hello **Microsoft.SQLAdapter** service, and **SQLServerQuota** quota.</span></span>

    > [!NOTE]
    > <span data-ttu-id="584e1-120">toolet 使用者建立其他應用程式，可能需要其他服務 hello 計劃中。</span><span class="sxs-lookup"><span data-stu-id="584e1-120">toolet users create other apps, other services might be required in hello plan.</span></span> <span data-ttu-id="584e1-121">例如，Azure 函式需要該 hello 計劃包含 hello **Microsoft.Storage**服務，而 Wordpress **Microsoft.MySQLAdapter**。</span><span class="sxs-lookup"><span data-stu-id="584e1-121">For example, Azure Functions requires that hello plan include hello **Microsoft.Storage** service, while Wordpress requires **Microsoft.MySQLAdapter**.</span></span>
    > 
    >

3.  <span data-ttu-id="584e1-122">[建立優惠](azure-stack-create-offer.md)，其命名**TestSQLServerOffer**和選取 hello **TestSQLServerPlan**計劃。</span><span class="sxs-lookup"><span data-stu-id="584e1-122">[Create an offer](azure-stack-create-offer.md), name it **TestSQLServerOffer** and select hello **TestSQLServerPlan** plan.</span></span>

## <a name="test-hello-offer"></a><span data-ttu-id="584e1-123">測試 hello 優惠</span><span class="sxs-lookup"><span data-stu-id="584e1-123">Test hello offer</span></span>

<span data-ttu-id="584e1-124">既然您已部署的 hello SQL Server 資源提供者，以及建立提供項目時，您可以登入的使用者身分，訂閱 toohello 供應項目，並建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="584e1-124">Now that you've deployed hello SQL Server resource provider and created an offer, you can sign in as a user, subscribe toohello offer, and create a database.</span></span>

### <a name="subscribe-toohello-offer"></a><span data-ttu-id="584e1-125">訂閱 toohello 供應項目</span><span class="sxs-lookup"><span data-stu-id="584e1-125">Subscribe toohello offer</span></span>
1. <span data-ttu-id="584e1-126">登入 toohello 堆疊 Azure 入口網站 (https://portal.local.azurestack.external) 做為租用戶。</span><span class="sxs-lookup"><span data-stu-id="584e1-126">Sign in toohello Azure Stack portal (https://portal.local.azurestack.external) as a tenant.</span></span>
2. <span data-ttu-id="584e1-127">按一下 [取得訂用帳戶]，然後在 [顯示名稱] 下輸入 **TestSQLServerSubscription**。</span><span class="sxs-lookup"><span data-stu-id="584e1-127">Click **Get a subscription** and then type **TestSQLServerSubscription** under **Display Name**.</span></span>
3. <span data-ttu-id="584e1-128">按一下 [選取服務] > [TestSQLServerOffer] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="584e1-128">Click **Select an offer** > **TestSQLServerOffer** > **Create**.</span></span>
4. <span data-ttu-id="584e1-129">按一下 [更多服務] > [訂用帳戶] > [TestSQLServerSubscription] > [資源提供者]。</span><span class="sxs-lookup"><span data-stu-id="584e1-129">Click **More services** > **Subscriptions** > **TestSQLServerSubscription** > **Resource providers**.</span></span>
5. <span data-ttu-id="584e1-130">按一下**註冊**下一步 toohello **Microsoft.SQLAdapter**提供者。</span><span class="sxs-lookup"><span data-stu-id="584e1-130">Click **Register** next toohello **Microsoft.SQLAdapter** provider.</span></span>

### <a name="create-a-sql-database"></a><span data-ttu-id="584e1-131">建立 SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="584e1-131">Create a SQL database</span></span>

1. <span data-ttu-id="584e1-132">按一下 [+] > [資料 + 儲存體] > [SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="584e1-132">Click **+** > **Data + Storage** > **SQL Database**.</span></span>
2. <span data-ttu-id="584e1-133">保持 hello 或預設值 hello 欄位，您可以使用這些範例：</span><span class="sxs-lookup"><span data-stu-id="584e1-133">Leave hello defaults for hello fields, or you can use these examples:</span></span>
    - <span data-ttu-id="584e1-134">**資料庫名稱**：SQLdb</span><span class="sxs-lookup"><span data-stu-id="584e1-134">**Database Name**: SQLdb</span></span>
    - <span data-ttu-id="584e1-135">**大小上限 (MB)**：100</span><span class="sxs-lookup"><span data-stu-id="584e1-135">**Max Size in MB**: 100</span></span>
    - <span data-ttu-id="584e1-136">**訂用帳戶**：TestSQLOffer</span><span class="sxs-lookup"><span data-stu-id="584e1-136">**Subscription**: TestSQLOffer</span></span>
    - <span data-ttu-id="584e1-137">**資源群組**：SQL-RG</span><span class="sxs-lookup"><span data-stu-id="584e1-137">**Resource Group**: SQL-RG</span></span>
3. <span data-ttu-id="584e1-138">按一下**登入設定**hello 資料庫中，輸入認證，然後按**確定**。</span><span class="sxs-lookup"><span data-stu-id="584e1-138">Click **Login Settings**, enter credentials for hello database, and then click **OK**.</span></span>
4. <span data-ttu-id="584e1-139">按一下**SKU** > 選取 hello 建立 hello SQL 主控伺服器的 SQL SKU >**確定**。</span><span class="sxs-lookup"><span data-stu-id="584e1-139">Click **SKU** > select hello SQL SKU that you created for hello SQL Hosting Server > **OK**.</span></span>
5. <span data-ttu-id="584e1-140">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="584e1-140">Click **Create**.</span></span>

<span data-ttu-id="584e1-141">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="584e1-141">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="584e1-142">部署 hello SQL Server 資源提供者</span><span class="sxs-lookup"><span data-stu-id="584e1-142">Deploy hello SQL Server resource provider</span></span>
> * <span data-ttu-id="584e1-143">建立優惠</span><span class="sxs-lookup"><span data-stu-id="584e1-143">Create an offer</span></span>
> * <span data-ttu-id="584e1-144">測試 hello 優惠</span><span class="sxs-lookup"><span data-stu-id="584e1-144">Test hello offer</span></span>

<span data-ttu-id="584e1-145">如何前進 toohello 下一個教學課程 toolearn 至：</span><span class="sxs-lookup"><span data-stu-id="584e1-145">Advance toohello next tutorial toolearn how to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="584e1-146">讓 web、 行動裝置、 應用程式開發介面應用程式可用 tooyour 使用者</span><span class="sxs-lookup"><span data-stu-id="584e1-146">Make web, mobile, and API apps available tooyour users</span></span>]( azure-stack-tutorial-app-service.md)

