---
title: "aaaDeploy hello Azure StorSimple 裝置管理員服務 |Microsoft 文件"
description: "說明如何 toocreate 和 delete hello hello Azure 入口網站中的 StorSimple 裝置管理員服務以及 toomanage hello 服務登錄機碼的方式。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: alkohli
ms.openlocfilehash: b84a907d6b735c8fee7bdc51f9c0074857297d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-8000-series-devices"></a><span data-ttu-id="6e643-103">部署適用於 StorSimple 8000 系列裝置 hello StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="6e643-103">Deploy hello StorSimple Device Manager service for StorSimple 8000 series devices</span></span>

## <a name="overview"></a><span data-ttu-id="6e643-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6e643-104">Overview</span></span>

<span data-ttu-id="6e643-105">hello StorSimple 裝置管理員服務在 Microsoft Azure 中執行，並連接 toomultiple StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="6e643-105">hello StorSimple Device Manager service runs in Microsoft Azure and connects toomultiple StorSimple devices.</span></span> <span data-ttu-id="6e643-106">建立 hello 服務之後，您可以使用它 toomanage 所有 hello 的裝置連線的 toohello StorSimple 裝置管理員都服務從單一中央位置，藉此將管理負擔降至最低。</span><span class="sxs-lookup"><span data-stu-id="6e643-106">After you create hello service, you can use it toomanage all hello devices that are connected toohello StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="6e643-107">本教學課程描述 hello hello 建立、 刪除、 hello 服務移轉與 hello hello 服務登錄機碼管理所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="6e643-107">This tutorial describes hello steps required for hello creation, deletion, migration of hello service and hello management of hello service registration key.</span></span> <span data-ttu-id="6e643-108">這篇文章中所包含的 hello 資訊是適用於只有 tooStorSimple 8000 系列的裝置。</span><span class="sxs-lookup"><span data-stu-id="6e643-108">hello information contained in this article is applicable only tooStorSimple 8000 series devices.</span></span> <span data-ttu-id="6e643-109">如需 StorSimple 虛擬陣列的詳細資訊，請移至太[部署 StorSimple 裝置管理員服務為您的 StorSimple Virtual Array](storsimple-virtual-array-manage-service.md)。</span><span class="sxs-lookup"><span data-stu-id="6e643-109">For more information on StorSimple Virtual Arrays, go too[deploy a StorSimple Device Manager service for your StorSimple Virtual Array](storsimple-virtual-array-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="6e643-110">建立服務</span><span class="sxs-lookup"><span data-stu-id="6e643-110">Create a service</span></span>
<span data-ttu-id="6e643-111">toocreate StorSimple 裝置管理員服務，您需要 toohave:</span><span class="sxs-lookup"><span data-stu-id="6e643-111">toocreate a StorSimple Device Manager service, you need toohave:</span></span>

* <span data-ttu-id="6e643-112">具有企業合約的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6e643-112">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="6e643-113">使用中的 Microsoft Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="6e643-113">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="6e643-114">hello 用於存取管理的計費資訊</span><span class="sxs-lookup"><span data-stu-id="6e643-114">hello billing information that is used for access management</span></span>

<span data-ttu-id="6e643-115">允許只 hello 與 Enterprise 合約的訂閱。</span><span class="sxs-lookup"><span data-stu-id="6e643-115">Only hello subscriptions with an Enterprise Agreement are allowed.</span></span> <span data-ttu-id="6e643-116">Hello Azure 入口網站中不支援 Microsoft 發起者訂閱 hello Azure 傳統入口網站中所允許的。</span><span class="sxs-lookup"><span data-stu-id="6e643-116">Microsoft Sponsorship subscriptions that were allowed in hello Azure classic portal are not supported in hello Azure portal.</span></span> <span data-ttu-id="6e643-117">您會看到下列訊息時使用不支援的訂閱 hello:</span><span class="sxs-lookup"><span data-stu-id="6e643-117">You will see hello following message when using an unsupported subscription:</span></span>

![訂用帳戶無效](./media/storsimple-8000-manage-service/subscription-not-valid.jpg)

<span data-ttu-id="6e643-119">您也可以選擇 toogenerate 預設儲存體帳戶建立 hello 服務時。</span><span class="sxs-lookup"><span data-stu-id="6e643-119">You can also choose toogenerate a default storage account when you create hello service.</span></span>

<span data-ttu-id="6e643-120">單一服務可以管理多個裝置。</span><span class="sxs-lookup"><span data-stu-id="6e643-120">A single service can manage multiple devices.</span></span> <span data-ttu-id="6e643-121">不過，裝置不能跨越多個服務。</span><span class="sxs-lookup"><span data-stu-id="6e643-121">However, a device cannot span multiple services.</span></span> <span data-ttu-id="6e643-122">大型企業可以擁有多個服務執行個體 toowork 與不同的訂閱、 組織或甚至是部署位置。</span><span class="sxs-lookup"><span data-stu-id="6e643-122">A large enterprise can have multiple service instances toowork with different subscriptions, organizations, or even deployment locations.</span></span> 

> [!NOTE]
> <span data-ttu-id="6e643-123">您需要不同的 StorSimple 裝置管理員服務 toomanage StorSimple 8000 系列裝置和 StorSimple 虛擬陣列執行個體。</span><span class="sxs-lookup"><span data-stu-id="6e643-123">You need separate instances of StorSimple Device Manager service toomanage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>

<span data-ttu-id="6e643-124">執行下列步驟 toocreate 服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="6e643-124">Perform hello following steps toocreate a service.</span></span>

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]


<span data-ttu-id="6e643-125">每個 StorSimple 裝置管理員服務，下列屬性的 hello 存在：</span><span class="sxs-lookup"><span data-stu-id="6e643-125">For each StorSimple Device Manager service, hello following attributes exist:</span></span>

* <span data-ttu-id="6e643-126">**名稱**– 建立時指派 tooyour StorSimple 裝置管理員服務的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="6e643-126">**Name** – hello name that was assigned tooyour StorSimple Device Manager service when it was created.</span></span> <span data-ttu-id="6e643-127">**建立 hello 服務之後，就無法變更 hello 服務名稱。這也適用於其他實體，例如裝置、 磁碟區、 磁碟區容器和備份原則不能在 hello Azure 入口網站中重新命名。**</span><span class="sxs-lookup"><span data-stu-id="6e643-127">**hello service name cannot be changed after hello service is created. This is also true for other entities such as devices, volumes, volume containers, and backup policies that cannot be renamed in hello Azure portal.**</span></span>
* <span data-ttu-id="6e643-128">**狀態**– hello hello 服務狀態，它可以是**Active**，**建立**，或**線上**。</span><span class="sxs-lookup"><span data-stu-id="6e643-128">**Status** – hello status of hello service, which can be **Active**, **Creating**, or **Online**.</span></span>
* <span data-ttu-id="6e643-129">**位置**– hello 地理位置中的 hello StorSimple 裝置將會部署。</span><span class="sxs-lookup"><span data-stu-id="6e643-129">**Location** – hello geographical location in which hello StorSimple device will be deployed.</span></span>
* <span data-ttu-id="6e643-130">**訂用帳戶**– hello 帳單與服務相關聯的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6e643-130">**Subscription** – hello billing subscription that is associated with your service.</span></span>

## <a name="move-a-service-tooazure-portal"></a><span data-ttu-id="6e643-131">將服務 tooAzure 入口網站移</span><span class="sxs-lookup"><span data-stu-id="6e643-131">Move a service tooAzure portal</span></span>
<span data-ttu-id="6e643-132">StorSimple 8000 系列可以立即管理 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="6e643-132">StorSimple 8000 series can be now managed in hello Azure portal.</span></span> <span data-ttu-id="6e643-133">如果您有現有服務 toomanage hello StorSimple 裝置時，我們建議您移動您服務 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6e643-133">If you have an existing service toomanage hello StorSimple devices, we recommend that you move your service toohello Azure portal.</span></span> <span data-ttu-id="6e643-134">2017 年 9 月 30 後, 就無法使用 hello hello StorSimple Manager 服務的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="6e643-134">hello Azure classic portal for hello StorSimple Manager service is not available after September 30, 2017.</span></span>

<span data-ttu-id="6e643-135">使用分階段 hello 選項 toomigrate toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6e643-135">hello option toomigrate toohello Azure portal is available in phases.</span></span> <span data-ttu-id="6e643-136">如果您沒有看到選項 toomigrate tooAzure 入口網站，但是您想 toomove 並檢閱移轉的 hello 影響述 hello[考量轉換](#considerations-for-transition)，您可以[提交要求](https://aka.ms/ss8000-cx-signup)。</span><span class="sxs-lookup"><span data-stu-id="6e643-136">If you do not see an option toomigrate tooAzure portal but you want toomove and have reviewed hello impact of migration as documented in hello [Considerations for transition](#considerations-for-transition), you can [submit a request](https://aka.ms/ss8000-cx-signup).</span></span>

### <a name="considerations-for-transition"></a><span data-ttu-id="6e643-137">轉換之前</span><span class="sxs-lookup"><span data-stu-id="6e643-137">Considerations for transition</span></span>

<span data-ttu-id="6e643-138">在您移動 hello 服務之前，請檢閱 hello 影響移轉 toohello 新版的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6e643-138">Review hello impact of migrating toohello new Azure portal before you move hello service.</span></span>

#### <a name="before-you-transition"></a><span data-ttu-id="6e643-139">轉換前的注意事項</span><span class="sxs-lookup"><span data-stu-id="6e643-139">Before you transition</span></span>

* <span data-ttu-id="6e643-140">裝置需執行 Update 3.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6e643-140">Your device is running Update 3.0 or later.</span></span> <span data-ttu-id="6e643-141">如果您的裝置正在執行較舊的版本，安裝 hello 最新的更新。</span><span class="sxs-lookup"><span data-stu-id="6e643-141">If your device is running an older version, install hello latest updates.</span></span> <span data-ttu-id="6e643-142">如需詳細資訊，請移至太[安裝 Update 4](storsimple-8000-install-update-4.md)。</span><span class="sxs-lookup"><span data-stu-id="6e643-142">For more information, go too[Install Update 4](storsimple-8000-install-update-4.md).</span></span> <span data-ttu-id="6e643-143">如果使用 StorSimple 雲端設備 (8010/8020)，請以 Update 4.0 建立新的雲端設備。</span><span class="sxs-lookup"><span data-stu-id="6e643-143">If using a StorSimple Cloud Appliance (8010/8020), create a new cloud appliance with Update 4.0.</span></span> 

* <span data-ttu-id="6e643-144">一旦轉換的 toohello 新版 Azure 入口網站，您無法使用 Azure 傳統入口網站 toomanage hello StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="6e643-144">Once you are transitioned toohello new Azure portal, you cannot use hello Azure classic portal toomanage your StorSimple device.</span></span>

* <span data-ttu-id="6e643-145">hello 轉換非干擾性，而且沒有 hello 裝置不再停機時間。</span><span class="sxs-lookup"><span data-stu-id="6e643-145">hello transition is non-disruptive and there is no downtime for hello device.</span></span>

* <span data-ttu-id="6e643-146">所有在 hello hello StorSimple 裝置管理員指定的訂用帳戶會轉換。</span><span class="sxs-lookup"><span data-stu-id="6e643-146">All hello StorSimple Device Managers under hello specified subscription are transitioned.</span></span>

#### <a name="during-hello-transition"></a><span data-ttu-id="6e643-147">Hello 轉換期間</span><span class="sxs-lookup"><span data-stu-id="6e643-147">During hello transition</span></span>

* <span data-ttu-id="6e643-148">您無法從 hello 入口網站來管理您的裝置。</span><span class="sxs-lookup"><span data-stu-id="6e643-148">You cannot manage your device from hello portal.</span></span>
* <span data-ttu-id="6e643-149">例如階層處理和已排程備份的作業繼續進行 toooccur。</span><span class="sxs-lookup"><span data-stu-id="6e643-149">Operations such as tiering and scheduled backups continue toooccur.</span></span>
* <span data-ttu-id="6e643-150">請勿刪除 hello 轉換正在進行時 hello 舊的 StorSimple 裝置管理員。</span><span class="sxs-lookup"><span data-stu-id="6e643-150">Do not delete hello old StorSimple Device Managers while hello transition is in progress.</span></span>

#### <a name="after-hello-transition"></a><span data-ttu-id="6e643-151">Hello 轉換之後</span><span class="sxs-lookup"><span data-stu-id="6e643-151">After hello transition</span></span>

* <span data-ttu-id="6e643-152">您無法再從 hello 傳統入口網站管理您的裝置。</span><span class="sxs-lookup"><span data-stu-id="6e643-152">You can no longer manage your devices from hello classic portal.</span></span>

* <span data-ttu-id="6e643-153">不支援 hello 現有的 Azure 服務管理 (ASM) PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6e643-153">hello existing Azure Service Management (ASM) PowerShell cmdlets are not supported.</span></span> <span data-ttu-id="6e643-154">更新 hello 指令碼 toomanage hello Azure 資源管理員透過您的裝置。</span><span class="sxs-lookup"><span data-stu-id="6e643-154">Update hello scripts toomanage your devices through hello Azure Resource Manager.</span></span>

* <span data-ttu-id="6e643-155">您的服務和裝置設定會予以保留。</span><span class="sxs-lookup"><span data-stu-id="6e643-155">Your service and device configuration are retained.</span></span> <span data-ttu-id="6e643-156">所有磁碟區和備份也是轉換的 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6e643-156">All your volumes and backups are also transitioned toohello Azure portal.</span></span>

### <a name="begin-transition"></a><span data-ttu-id="6e643-157">開始轉換</span><span class="sxs-lookup"><span data-stu-id="6e643-157">Begin transition</span></span>

<span data-ttu-id="6e643-158">執行下列步驟 tootransition hello 您服務 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6e643-158">Perform hello following steps tootransition your service toohello Azure portal.</span></span>

1. <span data-ttu-id="6e643-159">移 hello 傳統入口網站中的 tooyour 現有 StorSimple Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="6e643-159">Go tooyour existing StorSimple Manager service in hello classic portal.</span></span>

2. <span data-ttu-id="6e643-160">您看到通知，通知您 hello StorSimple 裝置管理員服務現已推出 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6e643-160">You see a notification that informs you that hello StorSimple Device Manager service is now available in hello Azure portal.</span></span> <span data-ttu-id="6e643-161">請注意在 hello Azure 入口網站，hello 服務會參照的 tooas StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="6e643-161">Note that in hello Azure portal, hello service is referred tooas StorSimple Device Manager service.</span></span>

    ![移轉通知](./media/storsimple-8000-manage-service/service-transition1.jpg)

    1. <span data-ttu-id="6e643-163">請確定您已檢閱 hello 移轉的完整影響。</span><span class="sxs-lookup"><span data-stu-id="6e643-163">Ensure that you have reviewed hello full impact of migration.</span></span>
    2. <span data-ttu-id="6e643-164">檢閱 hello 清單將從 hello 傳統入口網站移的 StorSimple 裝置管理員。</span><span class="sxs-lookup"><span data-stu-id="6e643-164">Review hello list of StorSimple Device Managers that will be moved from hello classic portal.</span></span>

3. <span data-ttu-id="6e643-165">按一下 [移轉]。</span><span class="sxs-lookup"><span data-stu-id="6e643-165">Click **Migrate**.</span></span> <span data-ttu-id="6e643-166">hello 轉換開始，並採用幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="6e643-166">hello transition begins and takes a few minutes toocomplete.</span></span>

<span data-ttu-id="6e643-167">Hello 轉換完成之後，您可以管理您的裝置透過 hello hello Azure 入口網站中的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="6e643-167">Once hello transition is complete, you can manage your devices via hello StorSimple Device Manager service in hello Azure portal.</span></span>

<span data-ttu-id="6e643-168">在 hello Azure 入口網站，只 hello 執行 Update 3.0 的 StorSimple 裝置，支援更高版本。</span><span class="sxs-lookup"><span data-stu-id="6e643-168">In hello Azure portal, only hello StorSimple devices running Update 3.0 and higher are supported.</span></span> <span data-ttu-id="6e643-169">執行較舊版本的 hello 裝置的支援有限。</span><span class="sxs-lookup"><span data-stu-id="6e643-169">hello devices that are running older versions have limited support.</span></span> <span data-ttu-id="6e643-170">hello 下列資料表 summrizes hello 裝置執行 versios 先前 tooUpdate 3.0 中，一旦移轉自 hello 傳統 toohello Azure 入口網站支援的作業。</span><span class="sxs-lookup"><span data-stu-id="6e643-170">hello following table summrizes which operations are supported on hello device running versios prior tooUpdate 3.0, once you have migrated from hello classic toohello Azure portal.</span></span>

| <span data-ttu-id="6e643-171">作業</span><span class="sxs-lookup"><span data-stu-id="6e643-171">Operation</span></span>                                                                                                                       | <span data-ttu-id="6e643-172">支援</span><span class="sxs-lookup"><span data-stu-id="6e643-172">Supported</span></span>      |
|---------------------------------------------------------------------------------------------------------------------------------|----------------|
| <span data-ttu-id="6e643-173">註冊裝置</span><span class="sxs-lookup"><span data-stu-id="6e643-173">Register a device</span></span>                                                                                                               | <span data-ttu-id="6e643-174">是</span><span class="sxs-lookup"><span data-stu-id="6e643-174">Yes</span></span>            |
| <span data-ttu-id="6e643-175">設定裝置設定，例如一般設定、網路設定和安全性設定</span><span class="sxs-lookup"><span data-stu-id="6e643-175">Configure device settings such as general, network, and security</span></span>                                                                | <span data-ttu-id="6e643-176">是</span><span class="sxs-lookup"><span data-stu-id="6e643-176">Yes</span></span>            |
| <span data-ttu-id="6e643-177">掃描、下載，及安裝更新</span><span class="sxs-lookup"><span data-stu-id="6e643-177">Scan, download, and install updates</span></span>                                                                                             | <span data-ttu-id="6e643-178">是</span><span class="sxs-lookup"><span data-stu-id="6e643-178">Yes</span></span>            |
| <span data-ttu-id="6e643-179">停用裝置</span><span class="sxs-lookup"><span data-stu-id="6e643-179">Deactivate device</span></span>                                                                                                               | <span data-ttu-id="6e643-180">是</span><span class="sxs-lookup"><span data-stu-id="6e643-180">Yes</span></span>            |
| <span data-ttu-id="6e643-181">刪除裝置</span><span class="sxs-lookup"><span data-stu-id="6e643-181">Delete device</span></span>                                                                                                                   | <span data-ttu-id="6e643-182">是</span><span class="sxs-lookup"><span data-stu-id="6e643-182">Yes</span></span>            |
| <span data-ttu-id="6e643-183">建立、修改及刪除磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="6e643-183">Create, modify, and delete a volume container</span></span>                                                                                   | <span data-ttu-id="6e643-184">否</span><span class="sxs-lookup"><span data-stu-id="6e643-184">No</span></span>             |
| <span data-ttu-id="6e643-185">建立、修改及刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="6e643-185">Create, modify, and delete a volume</span></span>                                                                                             | <span data-ttu-id="6e643-186">否</span><span class="sxs-lookup"><span data-stu-id="6e643-186">No</span></span>             |
| <span data-ttu-id="6e643-187">建立、修改及刪除備份原則</span><span class="sxs-lookup"><span data-stu-id="6e643-187">Create, modify, and delete a backup policy</span></span>                                                                                      | <span data-ttu-id="6e643-188">否</span><span class="sxs-lookup"><span data-stu-id="6e643-188">No</span></span>             |
| <span data-ttu-id="6e643-189">進行手動備份</span><span class="sxs-lookup"><span data-stu-id="6e643-189">Take a manual backup</span></span>                                                                                                            | <span data-ttu-id="6e643-190">否</span><span class="sxs-lookup"><span data-stu-id="6e643-190">No</span></span>             |
| <span data-ttu-id="6e643-191">進行排程備份</span><span class="sxs-lookup"><span data-stu-id="6e643-191">Take a scheduled backup</span></span>                                                                                                         | <span data-ttu-id="6e643-192">不適用</span><span class="sxs-lookup"><span data-stu-id="6e643-192">Not applicable</span></span> |
| <span data-ttu-id="6e643-193">從備份組還原</span><span class="sxs-lookup"><span data-stu-id="6e643-193">Restore from a backupset</span></span>                                                                                                        | <span data-ttu-id="6e643-194">否</span><span class="sxs-lookup"><span data-stu-id="6e643-194">No</span></span>             |
| <span data-ttu-id="6e643-195">3.0 和更新版本執行更新的複製品 tooa 裝置</span><span class="sxs-lookup"><span data-stu-id="6e643-195">Clone tooa device running Update 3.0 and later</span></span> <br> <span data-ttu-id="6e643-196">hello 來源裝置正在執行版本先前 tooUpdate 3.0。</span><span class="sxs-lookup"><span data-stu-id="6e643-196">hello source device is running version prior tooUpdate 3.0.</span></span>                                | <span data-ttu-id="6e643-197">是</span><span class="sxs-lookup"><span data-stu-id="6e643-197">Yes</span></span>            |
| <span data-ttu-id="6e643-198">執行版本先前 tooUpdate 3.0 複製 tooa 裝置</span><span class="sxs-lookup"><span data-stu-id="6e643-198">Clone tooa device running versions prior tooUpdate 3.0</span></span>                                                                          | <span data-ttu-id="6e643-199">否</span><span class="sxs-lookup"><span data-stu-id="6e643-199">No</span></span>             |
| <span data-ttu-id="6e643-200">作為容錯移轉的來源裝置</span><span class="sxs-lookup"><span data-stu-id="6e643-200">Failover as source device</span></span> <br> <span data-ttu-id="6e643-201">（從執行 3.0 和更新版本，執行更新的版本先前 tooUpdate 3.0 tooa 裝置的裝置）</span><span class="sxs-lookup"><span data-stu-id="6e643-201">(from a device running version prior tooUpdate 3.0 tooa device running Update 3.0 and later)</span></span>                                                               | <span data-ttu-id="6e643-202">是</span><span class="sxs-lookup"><span data-stu-id="6e643-202">Yes</span></span>            |
| <span data-ttu-id="6e643-203">作為容錯移轉的目標裝置</span><span class="sxs-lookup"><span data-stu-id="6e643-203">Failover as target device</span></span> <br> <span data-ttu-id="6e643-204">（tooa 裝置執行軟體版本先前 tooUpdate 3.0）</span><span class="sxs-lookup"><span data-stu-id="6e643-204">(tooa device running software version prior tooUpdate 3.0)</span></span>                                                                                   | <span data-ttu-id="6e643-205">否</span><span class="sxs-lookup"><span data-stu-id="6e643-205">No</span></span>             |
| <span data-ttu-id="6e643-206">清除警示</span><span class="sxs-lookup"><span data-stu-id="6e643-206">Clear an alert</span></span>                                                                                                                  | <span data-ttu-id="6e643-207">是</span><span class="sxs-lookup"><span data-stu-id="6e643-207">Yes</span></span>            |
| <span data-ttu-id="6e643-208">檢視備份原則、備份類別目錄、磁碟區、磁碟區容器、監視圖表、作業，以及傳統入口網站中建立的警示</span><span class="sxs-lookup"><span data-stu-id="6e643-208">View backup policies, backup catalog, volumes, volume containers, monitoring charts, jobs, and alerts created in classic portal</span></span> | <span data-ttu-id="6e643-209">是</span><span class="sxs-lookup"><span data-stu-id="6e643-209">Yes</span></span>            |
| <span data-ttu-id="6e643-210">開啟和關閉裝置控制器</span><span class="sxs-lookup"><span data-stu-id="6e643-210">Turn on and off device controllers</span></span>                                                                                              | <span data-ttu-id="6e643-211">是</span><span class="sxs-lookup"><span data-stu-id="6e643-211">Yes</span></span>            |


## <a name="delete-a-service"></a><span data-ttu-id="6e643-212">刪除服務</span><span class="sxs-lookup"><span data-stu-id="6e643-212">Delete a service</span></span>

<span data-ttu-id="6e643-213">刪除服務之前，請確定沒有任何連接的裝置正在使用它。</span><span class="sxs-lookup"><span data-stu-id="6e643-213">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="6e643-214">如果 hello 服務正在使用中，停用 hello 連接裝置。</span><span class="sxs-lookup"><span data-stu-id="6e643-214">If hello service is in use, deactivate hello connected devices.</span></span> <span data-ttu-id="6e643-215">hello 停用作業將會斷絕 hello hello 裝置與 hello 服務之間的連接，但是會保留 hello 雲端中的 hello 裝置資料。</span><span class="sxs-lookup"><span data-stu-id="6e643-215">hello deactivate operation will sever hello connection between hello device and hello service, but preserve hello device data in hello cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6e643-216">刪除服務之後，hello 作業無法反轉。</span><span class="sxs-lookup"><span data-stu-id="6e643-216">After a service is deleted, hello operation cannot be reversed.</span></span> <span data-ttu-id="6e643-217">已使用 hello 服務的任何裝置需要 toobe 重設 toofactory 預設值，然後搭配另一個服務。</span><span class="sxs-lookup"><span data-stu-id="6e643-217">Any device that was using hello service needs toobe reset toofactory defaults before it can be used with another service.</span></span> <span data-ttu-id="6e643-218">在此案例中，hello hello 裝置，以及 hello 組態上的本機資料將會遺失。</span><span class="sxs-lookup"><span data-stu-id="6e643-218">In this scenario, hello local data on hello device, as well as hello configuration, is lost.</span></span>

<span data-ttu-id="6e643-219">執行下列步驟 toodelete 服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="6e643-219">Perform hello following steps toodelete a service.</span></span>

### <a name="toodelete-a-service"></a><span data-ttu-id="6e643-220">toodelete 服務</span><span class="sxs-lookup"><span data-stu-id="6e643-220">toodelete a service</span></span>

1. <span data-ttu-id="6e643-221">搜尋您想 toodelete hello 服務。</span><span class="sxs-lookup"><span data-stu-id="6e643-221">Search for hello service you want toodelete.</span></span> <span data-ttu-id="6e643-222">按一下**資源**圖示，然後輸入 hello 適當條款 toosearch。</span><span class="sxs-lookup"><span data-stu-id="6e643-222">Click **Resources** icon and then input hello appropriate terms toosearch.</span></span> <span data-ttu-id="6e643-223">在 hello 搜尋結果中，按一下您想要 toodelete hello 服務。</span><span class="sxs-lookup"><span data-stu-id="6e643-223">In hello search results, click hello service you want toodelete.</span></span>

    ![搜尋服務 toodelete](./media/storsimple-8000-manage-service/deletessdevman1.png)

2. <span data-ttu-id="6e643-225">這會帶您 toohello StorSimple 裝置管理員服務刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6e643-225">This takes you toohello StorSimple Device Manager service blade.</span></span> <span data-ttu-id="6e643-226">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="6e643-226">Click **Delete**.</span></span>

    ![刪除服務](./media/storsimple-8000-manage-service/deletessdevman2.png)

3. <span data-ttu-id="6e643-228">按一下**是**hello 確認通知中。</span><span class="sxs-lookup"><span data-stu-id="6e643-228">Click **Yes** in hello confirmation notification.</span></span> <span data-ttu-id="6e643-229">可能需要幾分鐘，讓 hello 服務 toobe 刪除。</span><span class="sxs-lookup"><span data-stu-id="6e643-229">It may take a few minutes for hello service toobe deleted.</span></span>

    ![確認刪除](./media/storsimple-8000-manage-service/deletessdevman3.png)

## <a name="get-hello-service-registration-key"></a><span data-ttu-id="6e643-231">取得 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="6e643-231">Get hello service registration key</span></span>

<span data-ttu-id="6e643-232">您已成功建立服務之後，您將需要 tooregister hello 服務您 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="6e643-232">After you have successfully created a service, you will need tooregister your StorSimple device with hello service.</span></span> <span data-ttu-id="6e643-233">tooregister 第一個 StorSimple 裝置，您將需要 hello 服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="6e643-233">tooregister your first StorSimple device, you will need hello service registration key.</span></span> <span data-ttu-id="6e643-234">tooregister 現有 StorSimple 服務的其他裝置，您需要 hello 註冊金鑰和 hello 服務資料加密金鑰 （這在註冊期間產生 hello 第一個裝置上）。</span><span class="sxs-lookup"><span data-stu-id="6e643-234">tooregister additional devices with an existing StorSimple service, you need both hello registration key and hello service data encryption key (which is generated on hello first device during registration).</span></span> <span data-ttu-id="6e643-235">如需 hello 服務資料加密金鑰的詳細資訊，請參閱[StorSimple 安全性](storsimple-8000-security.md)。</span><span class="sxs-lookup"><span data-stu-id="6e643-235">For more information about hello service data encryption key, see [StorSimple security](storsimple-8000-security.md).</span></span> <span data-ttu-id="6e643-236">您可以存取，以取得 hello 登錄機碼**金鑰**您 StorSimple 裝置管理員 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6e643-236">You can get hello registration key by accessing **Keys** on your StorSimple Device Manager blade.</span></span>

<span data-ttu-id="6e643-237">執行下列步驟 tooget hello 服務登錄機碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="6e643-237">Perform hello following steps tooget hello service registration key.</span></span>

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

<span data-ttu-id="6e643-238">將 hello 服務註冊金鑰保存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="6e643-238">Keep hello service registration key in a safe location.</span></span> <span data-ttu-id="6e643-239">您將需要此金鑰，以及 hello 服務資料加密金鑰，tooregister 其他裝置向此服務。</span><span class="sxs-lookup"><span data-stu-id="6e643-239">You will need this key, as well as hello service data encryption key, tooregister additional devices with this service.</span></span> <span data-ttu-id="6e643-240">取得之後 hello 服務註冊金鑰，您必須設定您的裝置 hello Windows PowerShell 透過 StorSimple 介面。</span><span class="sxs-lookup"><span data-stu-id="6e643-240">After obtaining hello service registration key, you must configure your device through hello Windows PowerShell for StorSimple interface.</span></span>

<span data-ttu-id="6e643-241">如需詳細資訊，如何 toouse 這個註冊金鑰，請參閱[步驟 3： 設定和註冊 hello 裝置透過 Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)。</span><span class="sxs-lookup"><span data-stu-id="6e643-241">For details on how toouse this registration key, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

## <a name="regenerate-hello-service-registration-key"></a><span data-ttu-id="6e643-242">重新產生 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="6e643-242">Regenerate hello service registration key</span></span>
<span data-ttu-id="6e643-243">如果您被需要的 tooperform 金鑰輪動或服務管理員 hello 清單是否已變更，您會需要 tooregenerate 服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="6e643-243">You need tooregenerate a service registration key if you are required tooperform key rotation or if hello list of service administrators has changed.</span></span> <span data-ttu-id="6e643-244">當您重新產生 hello 索引鍵時，hello 新的金鑰僅用於註冊後續的裝置。</span><span class="sxs-lookup"><span data-stu-id="6e643-244">When you regenerate hello key, hello new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="6e643-245">hello 已經註冊的裝置不會影響此處理程序。</span><span class="sxs-lookup"><span data-stu-id="6e643-245">hello devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="6e643-246">執行下列步驟 tooregenerate 服務註冊金鑰的 hello。</span><span class="sxs-lookup"><span data-stu-id="6e643-246">Perform hello following steps tooregenerate a service registration key.</span></span>

### <a name="tooregenerate-hello-service-registration-key"></a><span data-ttu-id="6e643-247">tooregenerate hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="6e643-247">tooregenerate hello service registration key</span></span>
1. <span data-ttu-id="6e643-248">在 hello **StorSimple 裝置管理員**刀鋒視窗中，跳過**管理&gt;**  **金鑰**。</span><span class="sxs-lookup"><span data-stu-id="6e643-248">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
    
    ![[金鑰] 刀鋒視窗](./media/storsimple-8000-manage-service/regenregkey2.png)

2. <span data-ttu-id="6e643-250">在 hello**金鑰**刀鋒視窗中，按一下 **重新產生**。</span><span class="sxs-lookup"><span data-stu-id="6e643-250">In hello **Keys** blade, click **Regenerate**.</span></span>

    ![按一下重新產生](./media/storsimple-8000-manage-service/regenregkey3.png)
3. <span data-ttu-id="6e643-252">在 hello**重新產生服務登錄機碼**刀鋒視窗中，檢閱 hello 動作時才需要 hello 重新產生金鑰。</span><span class="sxs-lookup"><span data-stu-id="6e643-252">In hello **Regenerate service registration key** blade, review hello action required when hello keys are regenerated.</span></span> <span data-ttu-id="6e643-253">所有 hello 後續裝置註冊的此服務會都使用 hello 新的註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="6e643-253">All hello subsequent devices that are registered with this service use hello new registration key.</span></span> <span data-ttu-id="6e643-254">按一下**重新產生**tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="6e643-254">Click **Regenerate** tooconfirm.</span></span> <span data-ttu-id="6e643-255">Hello 重新產生作業完成之後，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="6e643-255">You are notified after hello regeneration is complete.</span></span>

    ![確認重新產生](./media/storsimple-8000-manage-service/regenregkey4.png)

4. <span data-ttu-id="6e643-257">新的服務註冊金鑰隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="6e643-257">A new service registration key will appear.</span></span>

5. <span data-ttu-id="6e643-258">複製這個金鑰並儲存，以對任何新的裝置註冊此服務。</span><span class="sxs-lookup"><span data-stu-id="6e643-258">Copy this key and save it for registering any new devices with this service.</span></span>



## <a name="change-hello-service-data-encryption-key"></a><span data-ttu-id="6e643-259">變更 hello 服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="6e643-259">Change hello service data encryption key</span></span>
<span data-ttu-id="6e643-260">服務資料加密金鑰是使用的 tooencrypt 客戶機密資料，例如從 StorSimple Manager 服務 toohello StorSimple 裝置傳送的儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="6e643-260">Service data encryption keys are used tooencrypt confidential customer data, such as storage account credentials, that are sent from your StorSimple Manager service toohello StorSimple device.</span></span> <span data-ttu-id="6e643-261">您將需要 toochange 這些機碼定期如果您的 IT 組織具有 hello 存放裝置金鑰輪動原則。</span><span class="sxs-lookup"><span data-stu-id="6e643-261">You will need toochange these keys periodically if your IT organization has a key rotation policy on hello storage devices.</span></span> <span data-ttu-id="6e643-262">hello 金鑰變更程序可能會稍有不同，視沒有單一裝置或多個 hello StorSimple Manager 服務所管理的裝置。</span><span class="sxs-lookup"><span data-stu-id="6e643-262">hello key change process can be slightly different depending on whether there is a single device or multiple devices managed by hello StorSimple Manager service.</span></span> <span data-ttu-id="6e643-263">如需詳細資訊，請移至太[StorSimple 安全性和資料保護](storsimple-8000-security.md)。</span><span class="sxs-lookup"><span data-stu-id="6e643-263">For more information, go too[StorSimple security and data protection](storsimple-8000-security.md).</span></span>

<span data-ttu-id="6e643-264">變更 hello 服務資料加密金鑰是 3 個步驟程序：</span><span class="sxs-lookup"><span data-stu-id="6e643-264">Changing hello service data encryption key is a 3-step process:</span></span>

1. <span data-ttu-id="6e643-265">使用 Windows PowerShell 指令碼的 Azure 資源管理員，授權裝置 toochange hello 服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="6e643-265">Using Windows PowerShell scripts for Azure Resource Manager, authorize a device toochange hello service data encryption key.</span></span>
2. <span data-ttu-id="6e643-266">使用 Windows PowerShell for StorSimple，起始 hello 服務資料加密金鑰變更。</span><span class="sxs-lookup"><span data-stu-id="6e643-266">Using Windows PowerShell for StorSimple, initiate hello service data encryption key change.</span></span>
3. <span data-ttu-id="6e643-267">如果您有多個 StorSimple 裝置，更新其他裝置上 hello hello 服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="6e643-267">If you have more than one StorSimple device, update hello service data encryption key on hello other devices.</span></span>

### <a name="step-1-use-windows-powershell-script-tooauthorize-a-device-toochange-hello-service-data-encryption-key"></a><span data-ttu-id="6e643-268">步驟 1： 使用 Windows PowerShell 指令碼 tooAuthorize 裝置 toochange hello 服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="6e643-268">Step 1: Use Windows PowerShell script tooAuthorize a device toochange hello service data encryption key</span></span>
<span data-ttu-id="6e643-269">一般而言，hello 裝置系統管理員會要求該 hello 服務系統管理員授權裝置 toochange 服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="6e643-269">Typically, hello device administrator will request that hello service administrator authorize a device toochange service data encryption keys.</span></span> <span data-ttu-id="6e643-270">然後 hello 服務系統管理員將授權 hello 裝置 toochange hello 機碼。</span><span class="sxs-lookup"><span data-stu-id="6e643-270">hello service administrator will then authorize hello device toochange hello key.</span></span>

<span data-ttu-id="6e643-271">使用 hello 基礎的 Azure 資源管理員指令碼來執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="6e643-271">This step is performed using hello Azure Resource Manager based script.</span></span> <span data-ttu-id="6e643-272">hello 服務系統管理員可以選取適合 toobe 獲授權的裝置。</span><span class="sxs-lookup"><span data-stu-id="6e643-272">hello service administrator can select a device that is eligible toobe authorized.</span></span> <span data-ttu-id="6e643-273">hello 裝置處於已授權的 toostart hello 服務資料加密金鑰變更程序。</span><span class="sxs-lookup"><span data-stu-id="6e643-273">hello device is then authorized toostart hello service data encryption key change process.</span></span> 

<span data-ttu-id="6e643-274">如需有關使用 hello 指令碼的詳細資訊，請移至太[授權 ServiceEncryptionRollover.ps1](https://github.com/anoobbacker/storsimpledevicemgmttools/blob/master/Authorize-ServiceEncryptionRollover.ps1)</span><span class="sxs-lookup"><span data-stu-id="6e643-274">For more information about using hello script, go too[Authorize-ServiceEncryptionRollover.ps1](https://github.com/anoobbacker/storsimpledevicemgmttools/blob/master/Authorize-ServiceEncryptionRollover.ps1)</span></span>

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a><span data-ttu-id="6e643-275">哪些裝置可以被授權 toochange 服務資料加密金鑰？</span><span class="sxs-lookup"><span data-stu-id="6e643-275">Which devices can be authorized toochange service data encryption keys?</span></span>
<span data-ttu-id="6e643-276">裝置必須符合下列準則，它可以是授權的 tooinitiate 服務資料加密金鑰變更之前的 hello:</span><span class="sxs-lookup"><span data-stu-id="6e643-276">A device must meet hello following criteria before it can be authorized tooinitiate service data encryption key changes:</span></span>

* <span data-ttu-id="6e643-277">hello 裝置必須是線上 toobe 適合服務資料加密金鑰變更授權。</span><span class="sxs-lookup"><span data-stu-id="6e643-277">hello device must be online toobe eligible for service data encryption key change authorization.</span></span>
* <span data-ttu-id="6e643-278">您可以授權的 hello 相同裝置一次在 30 分鐘後如果 hello 金鑰變更未起始。</span><span class="sxs-lookup"><span data-stu-id="6e643-278">You can authorize hello same device again after 30 minutes if hello key change has not been initiated.</span></span>
* <span data-ttu-id="6e643-279">您可以授權另一個裝置，前提 hello 金鑰變更未起始 hello 先前授權的裝置。</span><span class="sxs-lookup"><span data-stu-id="6e643-279">You can authorize a different device, provided that hello key change has not been initiated by hello previously authorized device.</span></span> <span data-ttu-id="6e643-280">已獲授權 hello 新裝置之後，hello 舊裝置無法起始 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="6e643-280">After hello new device has been authorized, hello old device cannot initiate hello change.</span></span>
* <span data-ttu-id="6e643-281">Hello hello 服務資料加密金鑰變換正在進行時，您無法授權裝置。</span><span class="sxs-lookup"><span data-stu-id="6e643-281">You cannot authorize a device while hello rollover of hello service data encryption key is in progress.</span></span>
* <span data-ttu-id="6e643-282">某些 hello hello 服務中註冊的裝置已變換 hello 加密而其他裝置尚未時，您可以授權裝置。</span><span class="sxs-lookup"><span data-stu-id="6e643-282">You can authorize a device when some of hello devices registered with hello service have rolled over hello encryption while others have not.</span></span> 

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a><span data-ttu-id="6e643-283">步驟 2： 使用 Windows PowerShell for StorSimple tooinitiate hello 服務資料加密金鑰變更</span><span class="sxs-lookup"><span data-stu-id="6e643-283">Step 2: Use Windows PowerShell for StorSimple tooinitiate hello service data encryption key change</span></span>
<span data-ttu-id="6e643-284">StorSimple 介面上 hello 授權 StorSimple 裝置的 hello Windows PowerShell 會執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="6e643-284">This step is performed in hello Windows PowerShell for StorSimple interface on hello authorized StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="6e643-285">Hello 金鑰變換完成之前，可以在 hello 的 StorSimple Manager 服務的 Azure 入口網站中不執行任何作業。</span><span class="sxs-lookup"><span data-stu-id="6e643-285">No operations can be performed in hello Azure portal of your StorSimple Manager service until hello key rollover is completed.</span></span>
> 
> 

<span data-ttu-id="6e643-286">如果您使用 hello 裝置序列主控台 tooconnect toohello Windows PowerShell 介面，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="6e643-286">If you are using hello device serial console tooconnect toohello Windows PowerShell interface, perform hello following steps.</span></span>

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a><span data-ttu-id="6e643-287">tooinitiate hello 服務資料加密金鑰變更</span><span class="sxs-lookup"><span data-stu-id="6e643-287">tooinitiate hello service data encryption key change</span></span>
1. <span data-ttu-id="6e643-288">選取選項 1 toolog 上，具有完整存取權。</span><span class="sxs-lookup"><span data-stu-id="6e643-288">Select option 1 toolog on with full access.</span></span>
2. <span data-ttu-id="6e643-289">在 hello 命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="6e643-289">At hello command prompt, type:</span></span>
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. <span data-ttu-id="6e643-290">Hello cmdlet 順利完成之後，您會得到新的服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="6e643-290">After hello cmdlet has successfully completed, you will get a new service data encryption key.</span></span> <span data-ttu-id="6e643-291">複製並儲存此金鑰，以供此程序的步驟 3 使用。</span><span class="sxs-lookup"><span data-stu-id="6e643-291">Copy and save this key for use in step 3 of this process.</span></span> <span data-ttu-id="6e643-292">此金鑰將會使用所有剩餘 hello StorSimple Manager 服務註冊裝置的 hello tooupdate。</span><span class="sxs-lookup"><span data-stu-id="6e643-292">This key will be used tooupdate all hello remaining devices registered with hello StorSimple Manager service.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6e643-293">此程序必須在授權 StorSimple 裝置後的四個小時內起始。</span><span class="sxs-lookup"><span data-stu-id="6e643-293">This process must be initiated within four hours of authorizing a StorSimple device.</span></span>
   > 
   > 
   
   <span data-ttu-id="6e643-294">這個新的金鑰，然後會傳送 toohello 服務推入 toobe tooall hello 登錄的裝置與 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="6e643-294">This new key is then sent toohello service toobe pushed tooall hello devices that are registered with hello service.</span></span> <span data-ttu-id="6e643-295">Hello 服務儀表板上，即會出現警示。</span><span class="sxs-lookup"><span data-stu-id="6e643-295">An alert will then appear on hello service dashboard.</span></span> <span data-ttu-id="6e643-296">hello 服務將會停用所有 hello hello 註冊裝置上的作業，hello 裝置系統管理員將必須 tooupdate hello 服務資料加密金鑰 hello 上的其他裝置。</span><span class="sxs-lookup"><span data-stu-id="6e643-296">hello service will disable all hello operations on hello registered devices, and hello device administrator will then need tooupdate hello service data encryption key on hello other devices.</span></span> <span data-ttu-id="6e643-297">不過，hello I/o （傳送資料 toohello 雲端的主機） 不會被中斷。</span><span class="sxs-lookup"><span data-stu-id="6e643-297">However, hello I/Os (hosts sending data toohello cloud) will not be disrupted.</span></span>
   
   <span data-ttu-id="6e643-298">如果您有單一裝置註冊 tooyour 服務 hello 變換程序現在已完成，可以略過 hello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="6e643-298">If you have a single device registered tooyour service, hello rollover process is now complete and you can skip hello next step.</span></span> <span data-ttu-id="6e643-299">如果您有多個裝置已註冊的 tooyour 服務時，繼續 toostep 3。</span><span class="sxs-lookup"><span data-stu-id="6e643-299">If you have multiple devices registered tooyour service, proceed toostep 3.</span></span>

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a><span data-ttu-id="6e643-300">步驟 3： 更新其他 StorSimple 裝置上的 hello 服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="6e643-300">Step 3: Update hello service data encryption key on other StorSimple devices</span></span>
<span data-ttu-id="6e643-301">如果您有多個裝置已註冊的 tooyour StorSimple Manager 服務，必須在您的 StorSimple 裝置 hello Windows PowerShell 介面中執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="6e643-301">These steps must be performed in hello Windows PowerShell interface of your StorSimple device if you have multiple devices registered tooyour StorSimple Manager service.</span></span> <span data-ttu-id="6e643-302">您在步驟 2 中取得的 hello 金鑰必須使用的 tooupdate 所有 hello 剩餘 StorSimple 裝置向 StorSimple Manager 服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="6e643-302">hello key that you obtained in Step 2 must be used tooupdate all hello remaining StorSimple device registered with hello StorSimple Manager service.</span></span>

<span data-ttu-id="6e643-303">執行下列步驟 tooupdate hello 服務資料加密在裝置上的 hello。</span><span class="sxs-lookup"><span data-stu-id="6e643-303">Perform hello following steps tooupdate hello service data encryption on your device.</span></span>

#### <a name="tooupdate-hello-service-data-encryption-key"></a><span data-ttu-id="6e643-304">tooupdate hello 服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="6e643-304">tooupdate hello service data encryption key</span></span>
1. <span data-ttu-id="6e643-305">使用 Windows PowerShell for StorSimple tooconnect toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="6e643-305">Use Windows PowerShell for StorSimple tooconnect toohello console.</span></span> <span data-ttu-id="6e643-306">選取選項 1 toolog 上，具有完整存取權。</span><span class="sxs-lookup"><span data-stu-id="6e643-306">Select option 1 toolog on with full access.</span></span>
2. <span data-ttu-id="6e643-307">在 hello 命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="6e643-307">At hello command prompt, type:</span></span>
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. <span data-ttu-id="6e643-308">提供 hello 服務資料加密金鑰，您在取得[步驟 2： 使用 Windows PowerShell for StorSimple tooinitiate hello 服務資料加密金鑰變更](#to-initiate-the-service-data-encryption-key-change)。</span><span class="sxs-lookup"><span data-stu-id="6e643-308">Provide hello service data encryption key that you obtained in [Step 2: Use Windows PowerShell for StorSimple tooinitiate hello service data encryption key change](#to-initiate-the-service-data-encryption-key-change).</span></span>


## <a name="next-steps"></a><span data-ttu-id="6e643-309">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6e643-309">Next steps</span></span>
* <span data-ttu-id="6e643-310">深入了解 hello [StorSimple 部署程序](storsimple-8000-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="6e643-310">Learn more about hello [StorSimple deployment process](storsimple-8000-deployment-walkthrough-u2.md).</span></span>
* <span data-ttu-id="6e643-311">深入了解 [管理 StorSimple 儲存體帳戶](storsimple-8000-manage-storage-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="6e643-311">Learn more about [managing your StorSimple storage account](storsimple-8000-manage-storage-accounts.md).</span></span>
* <span data-ttu-id="6e643-312">深入了解如何太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="6e643-312">Learn more about how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>
