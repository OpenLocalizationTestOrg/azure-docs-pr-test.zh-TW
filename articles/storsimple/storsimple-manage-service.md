---
title: "部署 StorSimple Manager 服務 | Microsoft Docs"
description: "說明如何在 Azure 傳統入口網站中建立和刪除 StorSimple Manager 服務，並說明如何管理服務註冊金鑰。"
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
ms.openlocfilehash: ba3637a3a8b15b45c16bf5a00c1f4225bcfc5af8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-the-storsimple-manager-service-in-the-azure-classic-portal"></a><span data-ttu-id="33fd6-103">在 Azure 傳統入口網站中部署 StorSimple Manager 服務</span><span class="sxs-lookup"><span data-stu-id="33fd6-103">Deploy the StorSimple Manager service in the Azure classic portal</span></span>

## <a name="overview"></a><span data-ttu-id="33fd6-104">概觀</span><span class="sxs-lookup"><span data-stu-id="33fd6-104">Overview</span></span>
<span data-ttu-id="33fd6-105">StorSimple Manager 服務可在 Microsoft Azure 中執行，並且連接至多個 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="33fd6-105">The StorSimple Manager service runs in Microsoft Azure and connects to multiple StorSimple devices.</span></span> <span data-ttu-id="33fd6-106">建立服務之後，您可以使用服務從在瀏覽器中執行的 Microsoft Azure 傳統入口網站管理這些裝置。</span><span class="sxs-lookup"><span data-stu-id="33fd6-106">After you create the service, you can use it to manage the devices from the Microsoft Azure classic portal running in a browser.</span></span> <span data-ttu-id="33fd6-107">這可讓您從單一集中位置監視連線至 StorSimple Manager 服務的所有裝置，所以可以盡可能降低管理負擔。</span><span class="sxs-lookup"><span data-stu-id="33fd6-107">This allows you to monitor all the devices that are connected to the StorSimple Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="33fd6-108">StorSimple Manager 登陸頁面會列出所有 StorSimple Manager 服務，您可用來管理您的 StorSimple 儲存體裝置。</span><span class="sxs-lookup"><span data-stu-id="33fd6-108">The StorSimple Manager landing page lists all the StorSimple Manager services that you can use to manage your StorSimple storage devices.</span></span> <span data-ttu-id="33fd6-109">針對每個 StorSimple Manager 服務，下列資訊會顯示在 StorSimple Manager 頁面上：</span><span class="sxs-lookup"><span data-stu-id="33fd6-109">For each StorSimple Manager service, the following information is presented on the StorSimple Manager page:</span></span>

* <span data-ttu-id="33fd6-110">**名稱** – 在建立時指派給您的 StorSimple Manager 服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="33fd6-110">**Name** – The name that was assigned to your StorSimple Manager service when it was created.</span></span> <span data-ttu-id="33fd6-111">**建立服務之後，就無法變更服務名稱。這也適用於其他實體，例如裝置、磁碟區、磁碟區容器和備份原則，在 Azure 傳統入口網站中無法重新命名。**</span><span class="sxs-lookup"><span data-stu-id="33fd6-111">**The service name cannot be changed after the service is created. This is also true for other entities such as devices, volumes, volume containers, and backup policies that cannot be renamed in the Azure classic portal.**</span></span>
* <span data-ttu-id="33fd6-112">**狀態** – 服務的狀態，可以是 [作用中]、[建立] 或是 [線上]。</span><span class="sxs-lookup"><span data-stu-id="33fd6-112">**Status** – The status of the service, which can be **Active**, **Creating**, or **Online**.</span></span>
* <span data-ttu-id="33fd6-113">**位置** – 部署 StorSimple 裝置所在的地理位置。</span><span class="sxs-lookup"><span data-stu-id="33fd6-113">**Location** – The geographical location in which the StorSimple device will be deployed.</span></span>
* <span data-ttu-id="33fd6-114">**訂用帳戶** – 與您的服務相關聯的計費訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="33fd6-114">**Subscription** – The billing subscription that is associated with your service.</span></span>

<span data-ttu-id="33fd6-115">可以透過 StorSimple Manager 頁面執行的一般工作包括：</span><span class="sxs-lookup"><span data-stu-id="33fd6-115">The common tasks that can be performed through the StorSimple Manager page are:</span></span>

* <span data-ttu-id="33fd6-116">建立服務</span><span class="sxs-lookup"><span data-stu-id="33fd6-116">Create a service</span></span>
* <span data-ttu-id="33fd6-117">刪除服務</span><span class="sxs-lookup"><span data-stu-id="33fd6-117">Delete a service</span></span>
* <span data-ttu-id="33fd6-118">取得服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="33fd6-118">Get the service registration key</span></span>
* <span data-ttu-id="33fd6-119">重新產生服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="33fd6-119">Regenerate the service registration key</span></span>

<span data-ttu-id="33fd6-120">本教學課程說明如何執行這些工作。</span><span class="sxs-lookup"><span data-stu-id="33fd6-120">This tutorial describes how to perform each of these tasks.</span></span>

## <a name="create-a-service"></a><span data-ttu-id="33fd6-121">建立服務</span><span class="sxs-lookup"><span data-stu-id="33fd6-121">Create a service</span></span>
<span data-ttu-id="33fd6-122">如果您想要部署您的 StorSimple 裝置，使用 [ **快速建立** ] 選項來建立 StorSimple Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="33fd6-122">Use the **Quick Create** option to create a StorSimple Manager service if you want to deploy your StorSimple device.</span></span> <span data-ttu-id="33fd6-123">若要建立服務，您需要：</span><span class="sxs-lookup"><span data-stu-id="33fd6-123">To create a service, you need to have:</span></span>

* <span data-ttu-id="33fd6-124">具有企業合約的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="33fd6-124">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="33fd6-125">使用中的 Microsoft Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="33fd6-125">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="33fd6-126">用於存取管理的計費資訊</span><span class="sxs-lookup"><span data-stu-id="33fd6-126">The billing information that is used for access management</span></span>

<span data-ttu-id="33fd6-127">您也可以選擇在建立服務時產生預設儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="33fd6-127">You can also choose to generate a default storage account when you create the service.</span></span>

<span data-ttu-id="33fd6-128">單一服務可以管理多個裝置。</span><span class="sxs-lookup"><span data-stu-id="33fd6-128">A single service can manage multiple devices.</span></span> <span data-ttu-id="33fd6-129">不過，裝置不能跨越多個服務。</span><span class="sxs-lookup"><span data-stu-id="33fd6-129">However, a device cannot span multiple services.</span></span> <span data-ttu-id="33fd6-130">大型企業可以擁有多個服務執行個體使用不同的訂用帳戶、組織或甚至是部署位置。</span><span class="sxs-lookup"><span data-stu-id="33fd6-130">A large enterprise can have multiple service instances to work with different subscriptions, organizations, or even deployment locations.</span></span> <span data-ttu-id="33fd6-131">請注意，您需要個別的 StorSimple Manager 服務來管理 StorSimple 8000 系列裝置和 StorSimple 虛擬陣列的執行個體。</span><span class="sxs-lookup"><span data-stu-id="33fd6-131">Please note that you need separate instances of StorSimple Manager service to manage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="33fd6-132">如果您在 2016 年 8 月前建立了未使用的服務 (在此資源上未執行任何裝置作業)，則無法透過 Azure 入口網站或 Azure 傳統入口網站進行管理。</span><span class="sxs-lookup"><span data-stu-id="33fd6-132">If you have an unused service created (no device operations were performed on this resource) prior to August 2016, it cannot be managed via Azure portal or Azure classic portal.</span></span> <span data-ttu-id="33fd6-133">我們建議您在 Azure 入口網站中建立新的服務。</span><span class="sxs-lookup"><span data-stu-id="33fd6-133">We recommend that you create a new service in the Azure portal.</span></span>

<span data-ttu-id="33fd6-134">執行下列步驟來建立服務。</span><span class="sxs-lookup"><span data-stu-id="33fd6-134">Perform the following steps to create a service.</span></span>

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="33fd6-135">刪除服務</span><span class="sxs-lookup"><span data-stu-id="33fd6-135">Delete a service</span></span>
<span data-ttu-id="33fd6-136">刪除服務之前，請確定沒有任何連接的裝置正在使用它。</span><span class="sxs-lookup"><span data-stu-id="33fd6-136">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="33fd6-137">如果服務正在使用中，請停用連接的裝置。</span><span class="sxs-lookup"><span data-stu-id="33fd6-137">If the service is in use, deactivate the connected devices.</span></span> <span data-ttu-id="33fd6-138">停用作業將會斷絕裝置與服務之間的連接，但是會保留雲端中的裝置資料。</span><span class="sxs-lookup"><span data-stu-id="33fd6-138">The deactivate operation will sever the connection between the device and the service, but preserve the device data in the cloud.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="33fd6-139">刪除服務之後，就無法回復此作業。</span><span class="sxs-lookup"><span data-stu-id="33fd6-139">After a service is deleted, the operation cannot be reversed.</span></span> <span data-ttu-id="33fd6-140">使用服務的任何裝置在可以搭配另一個服務使用之前，都必須恢復出廠預設值。</span><span class="sxs-lookup"><span data-stu-id="33fd6-140">Any device that was using the service will need to be factory reset before it can be used with another service.</span></span> <span data-ttu-id="33fd6-141">在此案例中，裝置上的本機資料以及組態將會遺失。</span><span class="sxs-lookup"><span data-stu-id="33fd6-141">In this scenario, the local data on the device, as well as the configuration, will be lost.</span></span>

<span data-ttu-id="33fd6-142">執行下列步驟來刪除服務。</span><span class="sxs-lookup"><span data-stu-id="33fd6-142">Perform the following steps to delete a service.</span></span>

### <a name="to-delete-a-service"></a><span data-ttu-id="33fd6-143">刪除服務</span><span class="sxs-lookup"><span data-stu-id="33fd6-143">To delete a service</span></span>
1. <span data-ttu-id="33fd6-144">在 [ **StorSimple Manager 服務** ] 頁面上，選取您要刪除的服務。</span><span class="sxs-lookup"><span data-stu-id="33fd6-144">On the **StorSimple Manager service** page, select the service that you wish to delete.</span></span>
2. <span data-ttu-id="33fd6-145">按一下頁面底部的 [ **刪除** ]。</span><span class="sxs-lookup"><span data-stu-id="33fd6-145">Click **Delete** at the bottom of the page.</span></span>
3. <span data-ttu-id="33fd6-146">在確認通知處按一下 [ **是** ]。</span><span class="sxs-lookup"><span data-stu-id="33fd6-146">Click **Yes** in the confirmation notification.</span></span> <span data-ttu-id="33fd6-147">刪除服務可能需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="33fd6-147">It may take a few minutes for the service to be deleted.</span></span>

## <a name="get-the-service-registration-key"></a><span data-ttu-id="33fd6-148">取得服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="33fd6-148">Get the service registration key</span></span>
<span data-ttu-id="33fd6-149">在您成功建立服務之後，您必須在 StorSimple 裝置註冊服務。</span><span class="sxs-lookup"><span data-stu-id="33fd6-149">After you have successfully created a service, you will need to register your StorSimple device with the service.</span></span> <span data-ttu-id="33fd6-150">若要註冊您的第一個 StorSimple 裝置，您必須使用服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="33fd6-150">To register your first StorSimple device, you will need the service registration key.</span></span> <span data-ttu-id="33fd6-151">若要使用現有的 StorSimple 服務註冊其他裝置，您需要註冊金鑰和服務資料加密金鑰 (在註冊期間於第一個裝置上產生)。</span><span class="sxs-lookup"><span data-stu-id="33fd6-151">To register additional devices with an existing StorSimple service, you will need both the registration key and the service data encryption key (which is generated on the first device during registration).</span></span> <span data-ttu-id="33fd6-152">如需服務資料加密金鑰的詳細資訊，請參閱 [StorSimple 安全性](storsimple-security.md)。</span><span class="sxs-lookup"><span data-stu-id="33fd6-152">For more information about the service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="33fd6-153">您可以藉由存取 [ **註冊金鑰** on the **註冊金鑰** ]，以取得註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="33fd6-153">You can get the registration key by accessing **Registration Key** on the **Services** page.</span></span>

<span data-ttu-id="33fd6-154">執行下列步驟以取得服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="33fd6-154">Perform the following steps to get the service registration key.</span></span>

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

<span data-ttu-id="33fd6-155">將服務註冊金鑰保存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="33fd6-155">Keep the service registration key in a safe location.</span></span> <span data-ttu-id="33fd6-156">您需要這個金鑰，以及服務資料加密金鑰，才能對額外裝置註冊此服務。</span><span class="sxs-lookup"><span data-stu-id="33fd6-156">You will need this key, as well as the service data encryption key, to register additional devices with this service.</span></span> <span data-ttu-id="33fd6-157">取得服務註冊金鑰之後，您必須透過 Windows PowerShell for StorSimple 介面設定裝置。</span><span class="sxs-lookup"><span data-stu-id="33fd6-157">After obtaining the service registration key, you will need to configure your device through the Windows PowerShell for StorSimple interface.</span></span>

<span data-ttu-id="33fd6-158">如需如何使用此註冊金鑰的詳細資訊，請參閱[步驟 3：透過 Windows PowerShell for StorSimple 設定和註冊裝置](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)。</span><span class="sxs-lookup"><span data-stu-id="33fd6-158">For details on how to use this registration key, see [Step 3: Configure and register the device through Windows PowerShell for StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

## <a name="regenerate-the-service-registration-key"></a><span data-ttu-id="33fd6-159">重新產生服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="33fd6-159">Regenerate the service registration key</span></span>
<span data-ttu-id="33fd6-160">如果您必須執行金鑰替換或服務系統管理員的清單已變更，則您必須重新產生服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="33fd6-160">You will need to regenerate a service registration key if you are required to perform key rotation or if the list of service administrators has changed.</span></span> <span data-ttu-id="33fd6-161">當您重新產生金鑰時，新的金鑰僅用於註冊後續裝置。</span><span class="sxs-lookup"><span data-stu-id="33fd6-161">When you regenerate the key, the new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="33fd6-162">已註冊的裝置不會受到此程序影響。</span><span class="sxs-lookup"><span data-stu-id="33fd6-162">The devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="33fd6-163">執行下列步驟以重新產生服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="33fd6-163">Perform the following steps to regenerate a service registration key.</span></span>

### <a name="to-regenerate-the-service-registration-key"></a><span data-ttu-id="33fd6-164">重新產生服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="33fd6-164">To regenerate the service registration key</span></span>
1. <span data-ttu-id="33fd6-165">在 [StorSimple Manager 服務] 頁面上，按一下 [註冊金鑰]。</span><span class="sxs-lookup"><span data-stu-id="33fd6-165">On the **StorSimple Manager service** page, click **Registration Key**.</span></span>
2. <span data-ttu-id="33fd6-166">在 [服務註冊金鑰] 對話方塊中，按一下 [重新產生]。</span><span class="sxs-lookup"><span data-stu-id="33fd6-166">In the **Service Registration Key** dialog box, click **Regenerate**.</span></span>
3. <span data-ttu-id="33fd6-167">您將會看見確認訊息。</span><span class="sxs-lookup"><span data-stu-id="33fd6-167">You will see a confirmation message.</span></span> <span data-ttu-id="33fd6-168">按一下 [ **確定** ] 繼續重新產生。</span><span class="sxs-lookup"><span data-stu-id="33fd6-168">Click **OK** to continue with the regeneration.</span></span>
4. <span data-ttu-id="33fd6-169">新的服務註冊金鑰隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="33fd6-169">A new service registration key will appear.</span></span>
5. <span data-ttu-id="33fd6-170">複製這個金鑰並儲存，以對任何新的裝置註冊此服務。</span><span class="sxs-lookup"><span data-stu-id="33fd6-170">Copy this key and save it for registering any new devices with this service.</span></span>
6. <span data-ttu-id="33fd6-171">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="33fd6-171">Click the check icon</span></span> ![核取圖示](./media/storsimple-manage-service/HCS_CheckIcon.png) <span data-ttu-id="33fd6-173">以關閉此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="33fd6-173">to close this dialog box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33fd6-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="33fd6-174">Next steps</span></span>
* <span data-ttu-id="33fd6-175">深入了解 [StorSimple 部署程序](storsimple-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="33fd6-175">Learn more about the [StorSimple deployment process](storsimple-deployment-walkthrough-u2.md).</span></span>
* <span data-ttu-id="33fd6-176">深入了解 [管理 StorSimple 儲存體帳戶](storsimple-manage-storage-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="33fd6-176">Learn more about [managing your StorSimple storage account](storsimple-manage-storage-accounts.md).</span></span>
* <span data-ttu-id="33fd6-177">深入了解如何 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="33fd6-177">Learn more about how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>
