---
title: "Microsoft Azure StorSimple 和雲端解決方案提供者方案概觀 | Microsoft Docs"
description: "StorSimple 和適用於 StorSimple 合作夥伴的 CSP 概觀。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/08/2017
ms.author: alkohli
ms.openlocfilehash: c8cb51093142146fc7d43b51a62d949f6cc38988
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="acaec-103">部署適用於雲端解決方案提供者方案的 StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="acaec-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="acaec-104">概觀</span><span class="sxs-lookup"><span data-stu-id="acaec-104">Overview</span></span>

<span data-ttu-id="acaec-105">雲端解決方案提供者 (CSP) 合作夥伴可以為客戶部署 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="acaec-105">StorSimple Virtual Array can be deployed by the Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="acaec-106">CSP 合作夥伴可以建立 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="acaec-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="acaec-107">然後，此服務可用來部署及管理 StorSimple Virtual Array，以及相關聯的共用、磁碟區和備份。</span><span class="sxs-lookup"><span data-stu-id="acaec-107">This service can then be used to deploy and manage StorSimple Virtual Array and the associated shares, volumes, and backups.</span></span>

<span data-ttu-id="acaec-108">本文說明 CSP 合作夥伴如何新增客戶，或將新的訂用帳戶新增至現有的客戶，然後建立服務在 CSP 中部署 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="acaec-108">This article describes how a CSP partner can add a customer or a new subscription to an existing customer and then create a service to deploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acaec-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="acaec-109">Prerequisites</span></span>

<span data-ttu-id="acaec-110">開始之前，請確定︰</span><span class="sxs-lookup"><span data-stu-id="acaec-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="acaec-111">您已註冊 CSP 方案。</span><span class="sxs-lookup"><span data-stu-id="acaec-111">You are enrolled under the CSP program.</span></span>
- <span data-ttu-id="acaec-112">您具備有效的[合作夥伴中心](http://partnercenter.microsoft.com/)登入認證。</span><span class="sxs-lookup"><span data-stu-id="acaec-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="acaec-113">認證可讓您登入合作夥伴入口網站，然後從夥伴儀表板新增客戶、搜尋客戶，或瀏覽至客戶帳戶。</span><span class="sxs-lookup"><span data-stu-id="acaec-113">The credentials enable you to sign in to the Partner portal to add new customers, search for customers, or navigate to a customer account from the Partner dashboard.</span></span> <span data-ttu-id="acaec-114">在 Azure 入口網站中，CSP 可以代表客戶擔任 StorSimple 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="acaec-114">The CSP can function as a StorSimple administrator on behalf of the customer in the Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="acaec-115">新增客戶</span><span class="sxs-lookup"><span data-stu-id="acaec-115">Add a customer</span></span>

<span data-ttu-id="acaec-116">新增客戶時會自動建立訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="acaec-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="acaec-117">若要新增客戶 (並自動建立訂用帳戶)，請在合作夥伴入口網站中執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="acaec-117">To add a customer (and automatically create a subscription), perform the following steps in the Partner portal.</span></span>

1. <span data-ttu-id="acaec-118">移至[合作夥伴中心](http://partnercenter.microsoft.com/)，使用 CSP 認證登入。</span><span class="sxs-lookup"><span data-stu-id="acaec-118">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="acaec-119">按一下 [儀表板] 。</span><span class="sxs-lookup"><span data-stu-id="acaec-119">Click **Dashboard**.</span></span>

     ![合作夥伴中心的儀表板](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="acaec-121">在左窗格中，按一下 [客戶]。</span><span class="sxs-lookup"><span data-stu-id="acaec-121">In the left-pane, click **Customers**.</span></span> <span data-ttu-id="acaec-122">在右窗格中，按一下 [新增客戶]。</span><span class="sxs-lookup"><span data-stu-id="acaec-122">In the right-pane, click **Add customers**.</span></span> <span data-ttu-id="acaec-123">輸入客戶的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="acaec-123">Enter the details of the customer.</span></span> <span data-ttu-id="acaec-124">按 [下一步︰訂用帳戶] 建立客戶訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="acaec-124">Click **Next: Subscriptions** to create a customer subscription.</span></span>

    ![新增客戶](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="acaec-126">選取 [Microsoft Azure] 優惠。</span><span class="sxs-lookup"><span data-stu-id="acaec-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="acaec-127">捲動到頁面底部，按一下 [檢閱]。</span><span class="sxs-lookup"><span data-stu-id="acaec-127">Scroll to the bottom of the page and click **Review**.</span></span>

    ![檢視訂用帳戶資訊](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="acaec-129">檢閱資訊，然後按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="acaec-129">Review the information and click **Submit**.</span></span>

    ![提交訂用帳戶](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="acaec-131">儲存確認資訊供日後參考。</span><span class="sxs-lookup"><span data-stu-id="acaec-131">Save the confirmation information for future reference.</span></span>

    ![儲存確認](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="acaec-133">尋找或瀏覽至您剛才新增的客戶。</span><span class="sxs-lookup"><span data-stu-id="acaec-133">Find or navigate to the customer you just added.</span></span> <span data-ttu-id="acaec-134">按一下 [公司名稱] 向下鑽研詳細資料。</span><span class="sxs-lookup"><span data-stu-id="acaec-134">Click the **Company name** to drill down into the details.</span></span>

    ![搜尋客戶](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="acaec-136">在左窗格中，選取 [服務管理]。</span><span class="sxs-lookup"><span data-stu-id="acaec-136">In the left-pane, select **Service management**.</span></span> <span data-ttu-id="acaec-137">在右窗格中的 [管理服務] 下，按一下 [Microsoft Azure 管理入口網站]，以 Azure 系統管理員身分代表客戶登入。</span><span class="sxs-lookup"><span data-stu-id="acaec-137">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span></span>

    ![登入 Azure 入口網站](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="acaec-139">若要建立 StorSimple 裝置管理員，請按一下 [+ 新增]，然後搜尋或瀏覽至 **StorSimple 虛擬裝置系列**。</span><span class="sxs-lookup"><span data-stu-id="acaec-139">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="acaec-140">如需詳細資訊，請移至[部署 StorSimple 裝置管理員服務](storsimple-virtual-array-manage-service.md)。</span><span class="sxs-lookup"><span data-stu-id="acaec-140">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![建立 StorSimple 裝置管理員服務](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="acaec-142">新增訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="acaec-142">Add a subscription</span></span>

<span data-ttu-id="acaec-143">在某些情況下，您可能已有現有的客戶，您需要新增訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="acaec-143">In some instances, you may have an existing customer, and you need to add a subscription.</span></span> <span data-ttu-id="acaec-144">若要將訂用帳戶新增至現有的客戶，請在合作夥伴入口網站中執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="acaec-144">To add a subscription to an existing customer, perform the following steps in the Partner portal.</span></span>

1. <span data-ttu-id="acaec-145">移至[合作夥伴中心](http://partnercenter.microsoft.com/)，使用 CSP 認證登入。</span><span class="sxs-lookup"><span data-stu-id="acaec-145">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="acaec-146">按一下 [儀表板] 。</span><span class="sxs-lookup"><span data-stu-id="acaec-146">Click **Dashboard**.</span></span>

     ![合作夥伴中心的儀表板](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="acaec-148">在左窗格中，按一下 [客戶]。</span><span class="sxs-lookup"><span data-stu-id="acaec-148">In the left-pane, click **Customers**.</span></span> <span data-ttu-id="acaec-149">尋找或瀏覽至客戶您想要新增訂用帳戶的客戶。</span><span class="sxs-lookup"><span data-stu-id="acaec-149">Find or navigate to the customer you want to add a subscription to.</span></span> <span data-ttu-id="acaec-150">按一下 ![展開核取圖示](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) 圖示，展開客戶公司名稱的資料列。</span><span class="sxs-lookup"><span data-stu-id="acaec-150">Click the ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon to expand the row for the company name for your customer.</span></span> <span data-ttu-id="acaec-151">在詳細資料中，按一下 [新增訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="acaec-151">In the details, click **Add subscriptions**.</span></span>

    ![客戶](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="acaec-153">在訂用帳戶中，檢查 **Microsoft Azure** 提供的**熱門優惠**，然後按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="acaec-153">Check **Microsoft Azure** for the **Top offers** in the subscription and click **Submit**.</span></span> <span data-ttu-id="acaec-154">這樣會建立新的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="acaec-154">This creates a new subscription.</span></span>

    ![新增訂用帳戶](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="acaec-156">建立新的訂用帳戶之後，在左窗格中按一下 [<-- 客戶]，以返回 [客戶] 頁面。</span><span class="sxs-lookup"><span data-stu-id="acaec-156">After a new subscription is created, click **<-- Customers** in the left-pane to return to the **Customers** page.</span></span> <span data-ttu-id="acaec-157">搜尋您剛建立訂用帳戶的客戶。</span><span class="sxs-lookup"><span data-stu-id="acaec-157">Search for the customer for whom you just created a subscription.</span></span> <span data-ttu-id="acaec-158">按一下 [公司名稱] 向下鑽研詳細資料。</span><span class="sxs-lookup"><span data-stu-id="acaec-158">Click the **Company name** to drill down into the details.</span></span>

    ![搜尋客戶](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="acaec-160">在左窗格中，選取 [服務管理]。</span><span class="sxs-lookup"><span data-stu-id="acaec-160">In the left-pane, select **Service management**.</span></span> <span data-ttu-id="acaec-161">在右窗格中的 [管理服務] 下，按一下 [Microsoft Azure 管理入口網站]，以 Azure 系統管理員身分代表客戶登入。</span><span class="sxs-lookup"><span data-stu-id="acaec-161">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span></span>

    ![登入 Azure 入口網站](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="acaec-163">若要建立 StorSimple 裝置管理員，請按一下 [+ 新增]，然後搜尋或瀏覽至 **StorSimple 虛擬裝置系列**。</span><span class="sxs-lookup"><span data-stu-id="acaec-163">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="acaec-164">如需詳細資訊，請移至[部署 StorSimple 裝置管理員服務](storsimple-virtual-array-manage-service.md)。</span><span class="sxs-lookup"><span data-stu-id="acaec-164">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![建立 StorSimple 裝置管理員服務](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="acaec-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="acaec-166">Next steps</span></span>

- <span data-ttu-id="acaec-167">關於 StorSimple in CSP，如果您還有其他問題，請移至 [StorSimple in CSP︰常見問題集](storsimple-partner-csp-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="acaec-167">If you have more questions regarding the StorSimple in CSP, go to [StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="acaec-168">如果您已準備好部署 StorSimple，請移至[部署 StorSimple in CSP](storsimple-partner-csp-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="acaec-168">If you are ready to deploy your StorSimple, go to [Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
