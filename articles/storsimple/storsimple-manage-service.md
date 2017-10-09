---
title: "aaaDeploy hello StorSimple Manager 服務 |Microsoft 文件"
description: "說明 toocreate 和 delete hello StorSimple Manager 服務在 hello Azure 傳統入口網站，以及如何 toomanage hello 服務註冊金鑰。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: bc1d5650-275c-42ed-bc77-cdb596f85943
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f49b647d91b03bb89ebd0e5cce196e50e3c00296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-manager-service-in-hello-azure-classic-portal"></a><span data-ttu-id="4da68-103">部署在 hello Azure 傳統入口網站中的 hello StorSimple Manager 服務</span><span class="sxs-lookup"><span data-stu-id="4da68-103">Deploy hello StorSimple Manager service in hello Azure classic portal</span></span>

## <a name="overview"></a><span data-ttu-id="4da68-104">概觀</span><span class="sxs-lookup"><span data-stu-id="4da68-104">Overview</span></span>
<span data-ttu-id="4da68-105">hello StorSimple Manager 服務在 Microsoft Azure 中執行，並連接 toomultiple StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="4da68-105">hello StorSimple Manager service runs in Microsoft Azure and connects toomultiple StorSimple devices.</span></span> <span data-ttu-id="4da68-106">建立 hello 服務之後，您可以使用它 toomanage hello 裝置 hello Microsoft Azure 傳統入口網站瀏覽器中執行。</span><span class="sxs-lookup"><span data-stu-id="4da68-106">After you create hello service, you can use it toomanage hello devices from hello Microsoft Azure classic portal running in a browser.</span></span> <span data-ttu-id="4da68-107">這可讓您 toomonitor 所有 hello 的裝置連線的 toohello StorSimple Manager 都服務從單一中央位置，藉此將管理負擔降至最低。</span><span class="sxs-lookup"><span data-stu-id="4da68-107">This allows you toomonitor all hello devices that are connected toohello StorSimple Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="4da68-108">hello StorSimple Manager 登陸頁面列出所有 hello StorSimple Manager 服務，您可以使用 toomanage StorSimple 儲存體裝置。</span><span class="sxs-lookup"><span data-stu-id="4da68-108">hello StorSimple Manager landing page lists all hello StorSimple Manager services that you can use toomanage your StorSimple storage devices.</span></span> <span data-ttu-id="4da68-109">每個 StorSimple Manager 服務，hello 下列資訊是針對顯示 hello StorSimple 管理員 頁面上：</span><span class="sxs-lookup"><span data-stu-id="4da68-109">For each StorSimple Manager service, hello following information is presented on hello StorSimple Manager page:</span></span>

* <span data-ttu-id="4da68-110">**名稱**– 建立時指派 tooyour StorSimple Manager 服務的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="4da68-110">**Name** – hello name that was assigned tooyour StorSimple Manager service when it was created.</span></span> <span data-ttu-id="4da68-111">**建立 hello 服務之後，就無法變更 hello 服務名稱。這也適用於其他實體，例如裝置、 磁碟區、 磁碟區容器和備份原則不能在 hello Azure 傳統入口網站中重新命名。**</span><span class="sxs-lookup"><span data-stu-id="4da68-111">**hello service name cannot be changed after hello service is created. This is also true for other entities such as devices, volumes, volume containers, and backup policies that cannot be renamed in hello Azure classic portal.**</span></span>
* <span data-ttu-id="4da68-112">**狀態**– hello hello 服務狀態，它可以是**Active**，**建立**，或**線上**。</span><span class="sxs-lookup"><span data-stu-id="4da68-112">**Status** – hello status of hello service, which can be **Active**, **Creating**, or **Online**.</span></span>
* <span data-ttu-id="4da68-113">**位置**– hello 地理位置中的 hello StorSimple 裝置將會部署。</span><span class="sxs-lookup"><span data-stu-id="4da68-113">**Location** – hello geographical location in which hello StorSimple device will be deployed.</span></span>
* <span data-ttu-id="4da68-114">**訂用帳戶**– hello 帳單與服務相關聯的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4da68-114">**Subscription** – hello billing subscription that is associated with your service.</span></span>

<span data-ttu-id="4da68-115">hello 可透過 hello StorSimple Manager 頁面執行的一般工作包括：</span><span class="sxs-lookup"><span data-stu-id="4da68-115">hello common tasks that can be performed through hello StorSimple Manager page are:</span></span>

* <span data-ttu-id="4da68-116">建立服務</span><span class="sxs-lookup"><span data-stu-id="4da68-116">Create a service</span></span>
* <span data-ttu-id="4da68-117">刪除服務</span><span class="sxs-lookup"><span data-stu-id="4da68-117">Delete a service</span></span>
* <span data-ttu-id="4da68-118">取得 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="4da68-118">Get hello service registration key</span></span>
* <span data-ttu-id="4da68-119">重新產生 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="4da68-119">Regenerate hello service registration key</span></span>

<span data-ttu-id="4da68-120">這個教學課程描述如何 tooperform 每個這些工作。</span><span class="sxs-lookup"><span data-stu-id="4da68-120">This tutorial describes how tooperform each of these tasks.</span></span>

## <a name="create-a-service"></a><span data-ttu-id="4da68-121">建立服務</span><span class="sxs-lookup"><span data-stu-id="4da68-121">Create a service</span></span>
<span data-ttu-id="4da68-122">使用 hello**快速建立**選項 toocreate StorSimple Manager 服務，如果您想 toodeploy StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="4da68-122">Use hello **Quick Create** option toocreate a StorSimple Manager service if you want toodeploy your StorSimple device.</span></span> <span data-ttu-id="4da68-123">toocreate 服務，您需要 toohave:</span><span class="sxs-lookup"><span data-stu-id="4da68-123">toocreate a service, you need toohave:</span></span>

* <span data-ttu-id="4da68-124">具有企業合約的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4da68-124">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="4da68-125">使用中的 Microsoft Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="4da68-125">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="4da68-126">hello 用於存取管理的計費資訊</span><span class="sxs-lookup"><span data-stu-id="4da68-126">hello billing information that is used for access management</span></span>

<span data-ttu-id="4da68-127">您也可以選擇 toogenerate 預設儲存體帳戶建立 hello 服務時。</span><span class="sxs-lookup"><span data-stu-id="4da68-127">You can also choose toogenerate a default storage account when you create hello service.</span></span>

<span data-ttu-id="4da68-128">單一服務可以管理多個裝置。</span><span class="sxs-lookup"><span data-stu-id="4da68-128">A single service can manage multiple devices.</span></span> <span data-ttu-id="4da68-129">不過，裝置不能跨越多個服務。</span><span class="sxs-lookup"><span data-stu-id="4da68-129">However, a device cannot span multiple services.</span></span> <span data-ttu-id="4da68-130">大型企業可以擁有多個服務執行個體 toowork 與不同的訂閱、 組織或甚至是部署位置。</span><span class="sxs-lookup"><span data-stu-id="4da68-130">A large enterprise can have multiple service instances toowork with different subscriptions, organizations, or even deployment locations.</span></span> <span data-ttu-id="4da68-131">請注意，您需要不同的 StorSimple Manager 服務 toomanage StorSimple 8000 系列裝置和 StorSimple 虛擬陣列的執行個體。</span><span class="sxs-lookup"><span data-stu-id="4da68-131">Please note that you need separate instances of StorSimple Manager service toomanage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="4da68-132">如果您有建立未使用的服務 （沒有這項資源執行作業的裝置） 先前 tooAugust 2016，它無法透過 Azure 入口網站或 Azure 傳統入口網站進行管理。</span><span class="sxs-lookup"><span data-stu-id="4da68-132">If you have an unused service created (no device operations were performed on this resource) prior tooAugust 2016, it cannot be managed via Azure portal or Azure classic portal.</span></span> <span data-ttu-id="4da68-133">我們建議您在 hello Azure 入口網站中建立新的服務。</span><span class="sxs-lookup"><span data-stu-id="4da68-133">We recommend that you create a new service in hello Azure portal.</span></span>

<span data-ttu-id="4da68-134">執行下列步驟 toocreate 服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="4da68-134">Perform hello following steps toocreate a service.</span></span>

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="4da68-135">刪除服務</span><span class="sxs-lookup"><span data-stu-id="4da68-135">Delete a service</span></span>
<span data-ttu-id="4da68-136">刪除服務之前，請確定沒有任何連接的裝置正在使用它。</span><span class="sxs-lookup"><span data-stu-id="4da68-136">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="4da68-137">如果 hello 服務正在使用中，停用 hello 連接裝置。</span><span class="sxs-lookup"><span data-stu-id="4da68-137">If hello service is in use, deactivate hello connected devices.</span></span> <span data-ttu-id="4da68-138">hello 停用作業將會斷絕 hello hello 裝置與 hello 服務之間的連接，但是會保留 hello 雲端中的 hello 裝置資料。</span><span class="sxs-lookup"><span data-stu-id="4da68-138">hello deactivate operation will sever hello connection between hello device and hello service, but preserve hello device data in hello cloud.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="4da68-139">刪除服務之後，hello 作業無法反轉。</span><span class="sxs-lookup"><span data-stu-id="4da68-139">After a service is deleted, hello operation cannot be reversed.</span></span> <span data-ttu-id="4da68-140">已使用 hello 服務的任何裝置需要 toobe 原廠重設之前可以搭配另一個服務。</span><span class="sxs-lookup"><span data-stu-id="4da68-140">Any device that was using hello service will need toobe factory reset before it can be used with another service.</span></span> <span data-ttu-id="4da68-141">在此案例中，hello hello 裝置，以及 hello 組態上的本機資料將會遺失。</span><span class="sxs-lookup"><span data-stu-id="4da68-141">In this scenario, hello local data on hello device, as well as hello configuration, will be lost.</span></span>

<span data-ttu-id="4da68-142">執行下列步驟 toodelete 服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="4da68-142">Perform hello following steps toodelete a service.</span></span>

### <a name="toodelete-a-service"></a><span data-ttu-id="4da68-143">toodelete 服務</span><span class="sxs-lookup"><span data-stu-id="4da68-143">toodelete a service</span></span>
1. <span data-ttu-id="4da68-144">在 hello **StorSimple Manager 服務**頁面上，且想 toodelete 選取 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="4da68-144">On hello **StorSimple Manager service** page, select hello service that you wish toodelete.</span></span>
2. <span data-ttu-id="4da68-145">按一下**刪除**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="4da68-145">Click **Delete** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="4da68-146">按一下**是**hello 確認通知中。</span><span class="sxs-lookup"><span data-stu-id="4da68-146">Click **Yes** in hello confirmation notification.</span></span> <span data-ttu-id="4da68-147">可能需要幾分鐘，讓 hello 服務 toobe 刪除。</span><span class="sxs-lookup"><span data-stu-id="4da68-147">It may take a few minutes for hello service toobe deleted.</span></span>

## <a name="get-hello-service-registration-key"></a><span data-ttu-id="4da68-148">取得 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="4da68-148">Get hello service registration key</span></span>
<span data-ttu-id="4da68-149">您已成功建立服務之後，您將需要 tooregister hello 服務您 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="4da68-149">After you have successfully created a service, you will need tooregister your StorSimple device with hello service.</span></span> <span data-ttu-id="4da68-150">tooregister 第一個 StorSimple 裝置，您將需要 hello 服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="4da68-150">tooregister your first StorSimple device, you will need hello service registration key.</span></span> <span data-ttu-id="4da68-151">tooregister 現有 StorSimple 服務的其他裝置，您將需要 hello 註冊金鑰和 hello 服務資料加密金鑰 （這在註冊期間產生 hello 第一個裝置上）。</span><span class="sxs-lookup"><span data-stu-id="4da68-151">tooregister additional devices with an existing StorSimple service, you will need both hello registration key and hello service data encryption key (which is generated on hello first device during registration).</span></span> <span data-ttu-id="4da68-152">如需 hello 服務資料加密金鑰的詳細資訊，請參閱[StorSimple 安全性](storsimple-security.md)。</span><span class="sxs-lookup"><span data-stu-id="4da68-152">For more information about hello service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="4da68-153">您可以存取，以取得 hello 登錄機碼**登錄機碼**上 hello**服務**頁面。</span><span class="sxs-lookup"><span data-stu-id="4da68-153">You can get hello registration key by accessing **Registration Key** on hello **Services** page.</span></span>

<span data-ttu-id="4da68-154">執行下列步驟 tooget hello 服務登錄機碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="4da68-154">Perform hello following steps tooget hello service registration key.</span></span>

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

<span data-ttu-id="4da68-155">將 hello 服務註冊金鑰保存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="4da68-155">Keep hello service registration key in a safe location.</span></span> <span data-ttu-id="4da68-156">您將需要此金鑰，以及 hello 服務資料加密金鑰，tooregister 其他裝置向此服務。</span><span class="sxs-lookup"><span data-stu-id="4da68-156">You will need this key, as well as hello service data encryption key, tooregister additional devices with this service.</span></span> <span data-ttu-id="4da68-157">取得之後 hello 服務註冊金鑰，您需要 tooconfigure 您的裝置 hello Windows PowerShell 透過 StorSimple 介面。</span><span class="sxs-lookup"><span data-stu-id="4da68-157">After obtaining hello service registration key, you will need tooconfigure your device through hello Windows PowerShell for StorSimple interface.</span></span>

<span data-ttu-id="4da68-158">如需詳細資訊，如何 toouse 這個註冊金鑰，請參閱[步驟 3： 設定和註冊 hello 裝置透過 Windows PowerShell for StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)。</span><span class="sxs-lookup"><span data-stu-id="4da68-158">For details on how toouse this registration key, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

## <a name="regenerate-hello-service-registration-key"></a><span data-ttu-id="4da68-159">重新產生 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="4da68-159">Regenerate hello service registration key</span></span>
<span data-ttu-id="4da68-160">如果您被需要的 tooperform 金鑰輪動或服務管理員 hello 清單是否已變更，您將需要 tooregenerate 服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="4da68-160">You will need tooregenerate a service registration key if you are required tooperform key rotation or if hello list of service administrators has changed.</span></span> <span data-ttu-id="4da68-161">當您重新產生 hello 索引鍵時，hello 新的金鑰僅用於註冊後續的裝置。</span><span class="sxs-lookup"><span data-stu-id="4da68-161">When you regenerate hello key, hello new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="4da68-162">hello 已經註冊的裝置不會影響此處理程序。</span><span class="sxs-lookup"><span data-stu-id="4da68-162">hello devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="4da68-163">執行下列步驟 tooregenerate 服務註冊金鑰的 hello。</span><span class="sxs-lookup"><span data-stu-id="4da68-163">Perform hello following steps tooregenerate a service registration key.</span></span>

### <a name="tooregenerate-hello-service-registration-key"></a><span data-ttu-id="4da68-164">tooregenerate hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="4da68-164">tooregenerate hello service registration key</span></span>
1. <span data-ttu-id="4da68-165">在 hello **StorSimple Manager 服務**頁面上，按一下**登錄機碼**。</span><span class="sxs-lookup"><span data-stu-id="4da68-165">On hello **StorSimple Manager service** page, click **Registration Key**.</span></span>
2. <span data-ttu-id="4da68-166">在 hello**服務註冊金鑰**對話方塊中，按一下 **重新產生**。</span><span class="sxs-lookup"><span data-stu-id="4da68-166">In hello **Service Registration Key** dialog box, click **Regenerate**.</span></span>
3. <span data-ttu-id="4da68-167">您將會看見確認訊息。</span><span class="sxs-lookup"><span data-stu-id="4da68-167">You will see a confirmation message.</span></span> <span data-ttu-id="4da68-168">按一下**確定**toocontinue 與 hello 重新產生。</span><span class="sxs-lookup"><span data-stu-id="4da68-168">Click **OK** toocontinue with hello regeneration.</span></span>
4. <span data-ttu-id="4da68-169">新的服務註冊金鑰隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="4da68-169">A new service registration key will appear.</span></span>
5. <span data-ttu-id="4da68-170">複製這個金鑰並儲存，以對任何新的裝置註冊此服務。</span><span class="sxs-lookup"><span data-stu-id="4da68-170">Copy this key and save it for registering any new devices with this service.</span></span>
6. <span data-ttu-id="4da68-171">按一下 [hello] 核取圖示</span><span class="sxs-lookup"><span data-stu-id="4da68-171">Click hello check icon</span></span> ![核取圖示](./media/storsimple-manage-service/HCS_CheckIcon.png) <span data-ttu-id="4da68-173">tooclose 此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4da68-173">tooclose this dialog box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4da68-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4da68-174">Next steps</span></span>
* <span data-ttu-id="4da68-175">深入了解 hello [StorSimple 部署程序](storsimple-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="4da68-175">Learn more about hello [StorSimple deployment process](storsimple-deployment-walkthrough-u2.md).</span></span>
* <span data-ttu-id="4da68-176">深入了解 [管理 StorSimple 儲存體帳戶](storsimple-manage-storage-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="4da68-176">Learn more about [managing your StorSimple storage account](storsimple-manage-storage-accounts.md).</span></span>
* <span data-ttu-id="4da68-177">深入了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="4da68-177">Learn more about how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>
