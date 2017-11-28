---
title: "aaaMicrosoft Azure StorSimple 和雲端方案提供者程式概觀 |Microsoft 文件"
description: "需 hello StorSimple 和 CSP StorSimple 協力廠商的概觀。"
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
ms.openlocfilehash: b5d999f2fbb9a27e7404ff454957b29dbef56af6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="4eac3-103">部署適用於雲端解決方案提供者方案的 StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="4eac3-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="4eac3-104">概觀</span><span class="sxs-lookup"><span data-stu-id="4eac3-104">Overview</span></span>

<span data-ttu-id="4eac3-105">StorSimple Virtual Array 可以部署的 hello 雲端方案提供者 (CSP) 夥伴以其客戶。</span><span class="sxs-lookup"><span data-stu-id="4eac3-105">StorSimple Virtual Array can be deployed by hello Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="4eac3-106">CSP 合作夥伴可以建立 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="4eac3-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="4eac3-107">這項服務可以接著使用的 toodeploy 和管理 StorSimple Virtual Array 與 hello 共用、 磁碟區以及備份。</span><span class="sxs-lookup"><span data-stu-id="4eac3-107">This service can then be used toodeploy and manage StorSimple Virtual Array and hello associated shares, volumes, and backups.</span></span>

<span data-ttu-id="4eac3-108">本文說明如何 CSP 夥伴可以新增客戶或新的訂用帳戶 tooan 現有客戶，，然後建立 StorSimple Virtual Array 服務 toodeploy CSP 中。</span><span class="sxs-lookup"><span data-stu-id="4eac3-108">This article describes how a CSP partner can add a customer or a new subscription tooan existing customer and then create a service toodeploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4eac3-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="4eac3-109">Prerequisites</span></span>

<span data-ttu-id="4eac3-110">開始之前，請確定︰</span><span class="sxs-lookup"><span data-stu-id="4eac3-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="4eac3-111">您已註冊裝置 hello CSP 計畫。</span><span class="sxs-lookup"><span data-stu-id="4eac3-111">You are enrolled under hello CSP program.</span></span>
- <span data-ttu-id="4eac3-112">您具備有效的[合作夥伴中心](http://partnercenter.microsoft.com/)登入認證。</span><span class="sxs-lookup"><span data-stu-id="4eac3-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="4eac3-113">hello 認證 toosign toohello 合作夥伴入口網站 tooadd 新客戶可讓您，搜尋客戶，或瀏覽 tooa 客戶帳戶從 hello 夥伴儀表板。</span><span class="sxs-lookup"><span data-stu-id="4eac3-113">hello credentials enable you toosign in toohello Partner portal tooadd new customers, search for customers, or navigate tooa customer account from hello Partner dashboard.</span></span> <span data-ttu-id="4eac3-114">代表 hello Azure 入口網站中的 hello 客戶，hello CSP 可以做為 StorSimple 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="4eac3-114">hello CSP can function as a StorSimple administrator on behalf of hello customer in hello Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="4eac3-115">新增客戶</span><span class="sxs-lookup"><span data-stu-id="4eac3-115">Add a customer</span></span>

<span data-ttu-id="4eac3-116">新增客戶時會自動建立訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4eac3-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="4eac3-117">tooadd 客戶 （及自動建立訂用帳戶），執行下列步驟在 hello 合作夥伴入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="4eac3-117">tooadd a customer (and automatically create a subscription), perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="4eac3-118">移 toohello[合作夥伴中心](http://partnercenter.microsoft.com/)然後使用 CSP 認證登入。</span><span class="sxs-lookup"><span data-stu-id="4eac3-118">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="4eac3-119">按一下 [儀表板] 。</span><span class="sxs-lookup"><span data-stu-id="4eac3-119">Click **Dashboard**.</span></span>

     ![合作夥伴中心的儀表板](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="4eac3-121">在 hello 左窗格中，按一下 **客戶**。</span><span class="sxs-lookup"><span data-stu-id="4eac3-121">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="4eac3-122">在 hello 右窗格中，按一下 **新增客戶**。</span><span class="sxs-lookup"><span data-stu-id="4eac3-122">In hello right-pane, click **Add customers**.</span></span> <span data-ttu-id="4eac3-123">輸入 hello hello 客戶詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4eac3-123">Enter hello details of hello customer.</span></span> <span data-ttu-id="4eac3-124">按一下**下一步： 訂用帳戶**toocreate 客戶訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4eac3-124">Click **Next: Subscriptions** toocreate a customer subscription.</span></span>

    ![新增客戶](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="4eac3-126">選取 [Microsoft Azure] 優惠。</span><span class="sxs-lookup"><span data-stu-id="4eac3-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="4eac3-127">捲軸 toohello 底部 hello 頁面，然後按一下**檢閱**。</span><span class="sxs-lookup"><span data-stu-id="4eac3-127">Scroll toohello bottom of hello page and click **Review**.</span></span>

    ![檢視訂用帳戶資訊](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="4eac3-129">檢閱 hello 資訊，然後按一下**送出**。</span><span class="sxs-lookup"><span data-stu-id="4eac3-129">Review hello information and click **Submit**.</span></span>

    ![提交訂用帳戶](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="4eac3-131">儲存 hello 確認資訊供日後參考。</span><span class="sxs-lookup"><span data-stu-id="4eac3-131">Save hello confirmation information for future reference.</span></span>

    ![儲存確認](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="4eac3-133">尋找或瀏覽 toohello 您剛才加入的客戶。</span><span class="sxs-lookup"><span data-stu-id="4eac3-133">Find or navigate toohello customer you just added.</span></span> <span data-ttu-id="4eac3-134">按一下 hello**公司名稱**toodrill 向下的到 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4eac3-134">Click hello **Company name** toodrill down into hello details.</span></span>

    ![搜尋 hello 客戶](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="4eac3-136">在 hello 左窗格中選取**服務管理**。</span><span class="sxs-lookup"><span data-stu-id="4eac3-136">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="4eac3-137">在 hello 右窗格中，在**管理服務**，按一下  **Microsoft Azure 管理入口網站**toosign 中客戶的 Azure 系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="4eac3-137">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![登入 tooAzure 入口網站](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="4eac3-139">toocreate StorSimple 裝置管理員 中，按一下**+ 新增**，搜尋或瀏覽過**StorSimple 虛擬裝置系列**。</span><span class="sxs-lookup"><span data-stu-id="4eac3-139">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="4eac3-140">如需詳細資訊，請移至太[部署 StorSimple 裝置管理員服務](storsimple-virtual-array-manage-service.md)。</span><span class="sxs-lookup"><span data-stu-id="4eac3-140">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![建立 StorSimple 裝置管理員服務](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="4eac3-142">新增訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4eac3-142">Add a subscription</span></span>

<span data-ttu-id="4eac3-143">在某些情況下，您可能有現有的客戶，而且您需要 tooadd 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4eac3-143">In some instances, you may have an existing customer, and you need tooadd a subscription.</span></span> <span data-ttu-id="4eac3-144">tooadd 訂用帳戶 tooan 現有客戶，執行下列步驟在 hello 合作夥伴入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="4eac3-144">tooadd a subscription tooan existing customer, perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="4eac3-145">移 toohello[合作夥伴中心](http://partnercenter.microsoft.com/)然後使用 CSP 認證登入。</span><span class="sxs-lookup"><span data-stu-id="4eac3-145">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="4eac3-146">按一下 [儀表板] 。</span><span class="sxs-lookup"><span data-stu-id="4eac3-146">Click **Dashboard**.</span></span>

     ![合作夥伴中心的儀表板](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="4eac3-148">在 hello 左窗格中，按一下 **客戶**。</span><span class="sxs-lookup"><span data-stu-id="4eac3-148">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="4eac3-149">尋找或瀏覽 toohello 客戶 tooadd 您想要訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4eac3-149">Find or navigate toohello customer you want tooadd a subscription to.</span></span> <span data-ttu-id="4eac3-150">按一下 hello![展開核取圖示](./media/storsimple-partner-csp-deploy/expand_pane_icon.png)hello 您客戶的公司名稱的圖示 tooexpand hello 資料列。</span><span class="sxs-lookup"><span data-stu-id="4eac3-150">Click hello ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon tooexpand hello row for hello company name for your customer.</span></span> <span data-ttu-id="4eac3-151">Hello 詳細資料中，按一下 **加入訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="4eac3-151">In hello details, click **Add subscriptions**.</span></span>

    ![客戶](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="4eac3-153">請檢查**Microsoft Azure** hello**排名最前面的優惠**hello 訂用帳戶，然後按一下**送出**。</span><span class="sxs-lookup"><span data-stu-id="4eac3-153">Check **Microsoft Azure** for hello **Top offers** in hello subscription and click **Submit**.</span></span> <span data-ttu-id="4eac3-154">這樣會建立新的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4eac3-154">This creates a new subscription.</span></span>

    ![新增訂用帳戶](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="4eac3-156">建立新的訂用帳戶之後，按一下**<-客戶**在 hello 左窗格 tooreturn toohello**客戶**頁面。</span><span class="sxs-lookup"><span data-stu-id="4eac3-156">After a new subscription is created, click **<-- Customers** in hello left-pane tooreturn toohello **Customers** page.</span></span> <span data-ttu-id="4eac3-157">搜尋 hello 客戶對您剛建立訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4eac3-157">Search for hello customer for whom you just created a subscription.</span></span> <span data-ttu-id="4eac3-158">按一下 hello**公司名稱**toodrill 向下的到 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4eac3-158">Click hello **Company name** toodrill down into hello details.</span></span>

    ![搜尋 hello 客戶](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="4eac3-160">在 hello 左窗格中選取**服務管理**。</span><span class="sxs-lookup"><span data-stu-id="4eac3-160">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="4eac3-161">在 hello 右窗格中，在**管理服務**，按一下  **Microsoft Azure 管理入口網站**toosign 中客戶的 Azure 系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="4eac3-161">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![登入 tooAzure 入口網站](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="4eac3-163">toocreate StorSimple 裝置管理員 中，按一下**+ 新增**，搜尋或瀏覽過**StorSimple 虛擬裝置系列**。</span><span class="sxs-lookup"><span data-stu-id="4eac3-163">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="4eac3-164">如需詳細資訊，請移至太[部署 StorSimple 裝置管理員服務](storsimple-virtual-array-manage-service.md)。</span><span class="sxs-lookup"><span data-stu-id="4eac3-164">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![建立 StorSimple 裝置管理員服務](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="4eac3-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4eac3-166">Next steps</span></span>

- <span data-ttu-id="4eac3-167">如果您在 CSP 中有更多有關 hello StorSimple 的問題，請移至太[CSP 中的 StorSimple： 常見問題集](storsimple-partner-csp-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="4eac3-167">If you have more questions regarding hello StorSimple in CSP, go too[StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="4eac3-168">如果您已準備 toodeploy 您的 StorSimple go 太[部署您的 StorSimple，在 CSP](storsimple-partner-csp-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="4eac3-168">If you are ready toodeploy your StorSimple, go too[Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
