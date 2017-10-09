---
title: "aaaDeploy StorSimple 裝置管理員服務 |Microsoft 文件"
description: "說明如何 toocreate 和 delete hello hello Azure 入口網站中的 StorSimple 裝置管理員服務以及 toomanage hello 服務登錄機碼的方式。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="157ee-103">部署 StorSimple Virtual Array 的 hello StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="157ee-103">Deploy hello StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="157ee-104">概觀</span><span class="sxs-lookup"><span data-stu-id="157ee-104">Overview</span></span>

<span data-ttu-id="157ee-105">hello StorSimple 裝置管理員服務在 Microsoft Azure 中執行，並連接 toomultiple StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="157ee-105">hello StorSimple Device Manager service runs in Microsoft Azure and connects toomultiple StorSimple devices.</span></span> <span data-ttu-id="157ee-106">建立 hello 服務之後，您可以使用它 toomanage hello 裝置 hello Microsoft Azure 入口網站瀏覽器中執行。</span><span class="sxs-lookup"><span data-stu-id="157ee-106">After you create hello service, you can use it toomanage hello devices from hello Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="157ee-107">這可讓您 toomonitor 所有 hello 的裝置連線的 toohello StorSimple 裝置管理員都服務從單一中央位置，藉此將管理負擔降至最低。</span><span class="sxs-lookup"><span data-stu-id="157ee-107">This allows you toomonitor all hello devices that are connected toohello StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="157ee-108">hello 常見工作相關的 tooa StorSimple 裝置管理員服務如下：</span><span class="sxs-lookup"><span data-stu-id="157ee-108">hello common tasks related tooa StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="157ee-109">建立服務</span><span class="sxs-lookup"><span data-stu-id="157ee-109">Create a service</span></span>
* <span data-ttu-id="157ee-110">刪除服務</span><span class="sxs-lookup"><span data-stu-id="157ee-110">Delete a service</span></span>
* <span data-ttu-id="157ee-111">取得 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="157ee-111">Get hello service registration key</span></span>
* <span data-ttu-id="157ee-112">重新產生 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="157ee-112">Regenerate hello service registration key</span></span>

<span data-ttu-id="157ee-113">本教學課程說明如何 tooperform 每個的 hello 前面的工作。</span><span class="sxs-lookup"><span data-stu-id="157ee-113">This tutorial describes how tooperform each of hello preceding tasks.</span></span> <span data-ttu-id="157ee-114">這篇文章中所包含的 hello 資訊是適用於只有 tooStorSimple 虛擬的陣列。</span><span class="sxs-lookup"><span data-stu-id="157ee-114">hello information contained in this article is applicable only tooStorSimple Virtual Arrays.</span></span> <span data-ttu-id="157ee-115">如需 StorSimple 8000 系列的詳細資訊，請移至太[部署 StorSimple Manager 服務](storsimple-manage-service.md)。</span><span class="sxs-lookup"><span data-stu-id="157ee-115">For more information on StorSimple 8000 series, go too[deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="157ee-116">建立服務</span><span class="sxs-lookup"><span data-stu-id="157ee-116">Create a service</span></span>

<span data-ttu-id="157ee-117">toocreate 服務，您需要 toohave:</span><span class="sxs-lookup"><span data-stu-id="157ee-117">toocreate a service, you need toohave:</span></span>

* <span data-ttu-id="157ee-118">具有企業合約的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="157ee-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="157ee-119">使用中的 Microsoft Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="157ee-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="157ee-120">hello 用於存取管理的計費資訊</span><span class="sxs-lookup"><span data-stu-id="157ee-120">hello billing information that is used for access management</span></span>

<span data-ttu-id="157ee-121">您也可以選擇 toogenerate 儲存體帳戶建立 hello 服務時。</span><span class="sxs-lookup"><span data-stu-id="157ee-121">You can also choose toogenerate a storage account when you create hello service.</span></span>

<span data-ttu-id="157ee-122">單一服務可以管理多個裝置。</span><span class="sxs-lookup"><span data-stu-id="157ee-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="157ee-123">不過，裝置不能跨越多個服務。</span><span class="sxs-lookup"><span data-stu-id="157ee-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="157ee-124">大型企業可以擁有多個服務執行個體 toowork 與不同的訂閱、 組織或甚至是部署位置。</span><span class="sxs-lookup"><span data-stu-id="157ee-124">A large enterprise can have multiple service instances toowork with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="157ee-125">您需要不同的 StorSimple 裝置管理員服務 toomanage StorSimple 8000 系列裝置和 StorSimple 虛擬陣列執行個體。</span><span class="sxs-lookup"><span data-stu-id="157ee-125">You need separate instances of StorSimple Device Manager service toomanage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="157ee-126">執行下列步驟 toocreate 服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="157ee-126">Perform hello following steps toocreate a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="157ee-127">刪除服務</span><span class="sxs-lookup"><span data-stu-id="157ee-127">Delete a service</span></span>

<span data-ttu-id="157ee-128">刪除服務之前，請確定沒有任何連接的裝置正在使用它。</span><span class="sxs-lookup"><span data-stu-id="157ee-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="157ee-129">如果 hello 服務正在使用中，停用 hello 連接裝置。</span><span class="sxs-lookup"><span data-stu-id="157ee-129">If hello service is in use, deactivate hello connected devices.</span></span> <span data-ttu-id="157ee-130">hello 停用作業將會斷絕 hello hello 裝置與 hello 服務之間的連接，但是會保留 hello 雲端中的 hello 裝置資料。</span><span class="sxs-lookup"><span data-stu-id="157ee-130">hello deactivate operation will sever hello connection between hello device and hello service, but preserve hello device data in hello cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="157ee-131">刪除服務之後，hello 作業無法反轉。</span><span class="sxs-lookup"><span data-stu-id="157ee-131">After a service is deleted, hello operation cannot be reversed.</span></span> <span data-ttu-id="157ee-132">已使用 hello 服務的任何裝置需要 toobe 原廠重設之前可以搭配另一個服務。</span><span class="sxs-lookup"><span data-stu-id="157ee-132">Any device that was using hello service will need toobe factory reset before it can be used with another service.</span></span> <span data-ttu-id="157ee-133">在此案例中，hello hello 裝置，以及 hello 組態上的本機資料將會遺失。</span><span class="sxs-lookup"><span data-stu-id="157ee-133">In this scenario, hello local data on hello device, as well as hello configuration, will be lost.</span></span>
 

<span data-ttu-id="157ee-134">執行下列步驟 toodelete 服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="157ee-134">Perform hello following steps toodelete a service.</span></span>

#### <a name="toodelete-a-service"></a><span data-ttu-id="157ee-135">toodelete 服務</span><span class="sxs-lookup"><span data-stu-id="157ee-135">toodelete a service</span></span>

1. <span data-ttu-id="157ee-136">跳過**所有資源**。</span><span class="sxs-lookup"><span data-stu-id="157ee-136">Go too**All resources**.</span></span> <span data-ttu-id="157ee-137">搜尋您的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="157ee-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="157ee-138">選取您想 toodelete hello 服務。</span><span class="sxs-lookup"><span data-stu-id="157ee-138">Select hello service that you wish toodelete.</span></span>
   
    ![選取服務 toodelete](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="157ee-140">移 tooyour 服務儀表板 tooensure 有無任何裝置已連線 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="157ee-140">Go tooyour service dashboard tooensure there are no devices connected toohello service.</span></span> <span data-ttu-id="157ee-141">如果沒有與此服務註冊的裝置，也會看到橫幅訊息 toohello 效果。</span><span class="sxs-lookup"><span data-stu-id="157ee-141">If there are no devices registered with this service, you will also see a banner message toohello effect.</span></span> <span data-ttu-id="157ee-142">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="157ee-142">Click **Delete**.</span></span>
   
    ![刪除服務](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="157ee-144">當提示確認，請按一下**是**hello 確認通知中。</span><span class="sxs-lookup"><span data-stu-id="157ee-144">When prompted for confirmation, click **Yes** in hello confirmation notification.</span></span> 
   
    ![確認刪除服務](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="157ee-146">可能需要幾分鐘，讓 hello 服務 toobe 刪除。</span><span class="sxs-lookup"><span data-stu-id="157ee-146">It may take a few minutes for hello service toobe deleted.</span></span> <span data-ttu-id="157ee-147">Hello 服務已成功刪除之後，系統會通知您。</span><span class="sxs-lookup"><span data-stu-id="157ee-147">After hello service is successfully deleted, you will be notified.</span></span>
   
    ![成功刪除服務](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="157ee-149">服務的 hello 清單會重新整理。</span><span class="sxs-lookup"><span data-stu-id="157ee-149">hello list of services will be refreshed.</span></span>

 ![更新的服務清單](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a><span data-ttu-id="157ee-151">取得 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="157ee-151">Get hello service registration key</span></span>
<span data-ttu-id="157ee-152">您已成功建立服務之後，您將需要 tooregister hello 服務您 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="157ee-152">After you have successfully created a service, you will need tooregister your StorSimple device with hello service.</span></span> <span data-ttu-id="157ee-153">tooregister 第一個 StorSimple 裝置，您將需要 hello 服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="157ee-153">tooregister your first StorSimple device, you will need hello service registration key.</span></span> <span data-ttu-id="157ee-154">tooregister 現有 StorSimple 服務的其他裝置，您將需要 hello 註冊金鑰和 hello 服務資料加密金鑰 （這在註冊期間產生 hello 第一個裝置上）。</span><span class="sxs-lookup"><span data-stu-id="157ee-154">tooregister additional devices with an existing StorSimple service, you will need both hello registration key and hello service data encryption key (which is generated on hello first device during registration).</span></span> <span data-ttu-id="157ee-155">如需 hello 服務資料加密金鑰的詳細資訊，請參閱[StorSimple 安全性](storsimple-security.md)。</span><span class="sxs-lookup"><span data-stu-id="157ee-155">For more information about hello service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="157ee-156">您可以藉由存取 hello 取得 hello 登錄機碼**金鑰**刀鋒視窗中為您的服務。</span><span class="sxs-lookup"><span data-stu-id="157ee-156">You can get hello registration key by accessing hello **Keys** blade for your service.</span></span>

<span data-ttu-id="157ee-157">執行下列步驟 tooget hello 服務登錄機碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="157ee-157">Perform hello following steps tooget hello service registration key.</span></span>

#### <a name="tooget-hello-service-registration-key"></a><span data-ttu-id="157ee-158">tooget hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="157ee-158">tooget hello service registration key</span></span>
1. <span data-ttu-id="157ee-159">在 hello **StorSimple 裝置管理員**刀鋒視窗中，跳過**管理&gt;**  **金鑰**。</span><span class="sxs-lookup"><span data-stu-id="157ee-159">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![[金鑰] 刀鋒視窗](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="157ee-161">在 hello**金鑰**刀鋒視窗中，會出現服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="157ee-161">In hello **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="157ee-162">複製使用 hello 複製圖示 hello 註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="157ee-162">Copy hello registration key using hello copy icon.</span></span> 

<span data-ttu-id="157ee-163">將 hello 服務註冊金鑰保存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="157ee-163">Keep hello service registration key in a safe location.</span></span> <span data-ttu-id="157ee-164">您將需要此金鑰，以及 hello 服務資料加密金鑰，tooregister 其他裝置向此服務。</span><span class="sxs-lookup"><span data-stu-id="157ee-164">You will need this key, as well as hello service data encryption key, tooregister additional devices with this service.</span></span> <span data-ttu-id="157ee-165">取得之後 hello 服務註冊金鑰，您需要 tooconfigure 您的裝置 hello Windows PowerShell 透過 StorSimple 介面。</span><span class="sxs-lookup"><span data-stu-id="157ee-165">After obtaining hello service registration key, you will need tooconfigure your device through hello Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-hello-service-registration-key"></a><span data-ttu-id="157ee-166">重新產生 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="157ee-166">Regenerate hello service registration key</span></span>
<span data-ttu-id="157ee-167">如果您被需要的 tooperform 金鑰輪動或服務管理員 hello 清單是否已變更，您將需要 tooregenerate 服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="157ee-167">You will need tooregenerate a service registration key if you are required tooperform key rotation or if hello list of service administrators has changed.</span></span> <span data-ttu-id="157ee-168">當您重新產生 hello 索引鍵時，hello 新的金鑰僅用於註冊後續的裝置。</span><span class="sxs-lookup"><span data-stu-id="157ee-168">When you regenerate hello key, hello new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="157ee-169">hello 已經註冊的裝置不會影響此處理程序。</span><span class="sxs-lookup"><span data-stu-id="157ee-169">hello devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="157ee-170">執行下列步驟 tooregenerate 服務註冊金鑰的 hello。</span><span class="sxs-lookup"><span data-stu-id="157ee-170">Perform hello following steps tooregenerate a service registration key.</span></span>

#### <a name="tooregenerate-hello-service-registration-key"></a><span data-ttu-id="157ee-171">tooregenerate hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="157ee-171">tooregenerate hello service registration key</span></span>
1. <span data-ttu-id="157ee-172">在 hello **StorSimple 裝置管理員**刀鋒視窗中，跳過**管理&gt;**  **金鑰**。</span><span class="sxs-lookup"><span data-stu-id="157ee-172">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![[金鑰] 刀鋒視窗](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="157ee-174">在 hello**金鑰**刀鋒視窗中，按一下 **重新產生**。</span><span class="sxs-lookup"><span data-stu-id="157ee-174">In hello **Keys** blade, click **Regenerate**.</span></span>
   
   ![按一下重新產生](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="157ee-176">在 hello**重新產生服務登錄機碼**刀鋒視窗中，檢閱 hello 動作時才需要 hello 重新產生金鑰。</span><span class="sxs-lookup"><span data-stu-id="157ee-176">In hello **Regenerate service registration key** blade, review hello action required when hello keys are regenerated.</span></span> <span data-ttu-id="157ee-177">所有 hello 後續裝置註冊的此服務會都使用 hello 新的註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="157ee-177">All hello subsequent devices that are registered with this service will use hello new registration key.</span></span> <span data-ttu-id="157ee-178">按一下**重新產生**tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="157ee-178">Click **Regenerate** tooconfirm.</span></span> <span data-ttu-id="157ee-179">Hello 註冊完成後，系統會通知您。</span><span class="sxs-lookup"><span data-stu-id="157ee-179">You will be notified after hello registration is complete.</span></span>
   
   ![確認重新產生金鑰](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="157ee-181">新的服務註冊金鑰隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="157ee-181">A new service registration key will appear.</span></span>
   
    ![確認重新產生金鑰](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="157ee-183">複製這個金鑰並儲存，以對任何新的裝置註冊此服務。</span><span class="sxs-lookup"><span data-stu-id="157ee-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="157ee-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="157ee-184">Next steps</span></span>
* <span data-ttu-id="157ee-185">了解如何太[開始](storsimple-virtual-array-deploy1-portal-prep.md)與 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="157ee-185">Learn how too[get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="157ee-186">了解如何太[管理您的 StorSimple 裝置](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="157ee-186">Learn how too[administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

