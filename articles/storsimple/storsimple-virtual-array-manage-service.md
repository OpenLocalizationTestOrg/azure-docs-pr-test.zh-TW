---
title: "部署 StorSimple 裝置管理員服務 | Microsoft Docs"
description: "說明如何在 Azure 入口網站中建立和刪除 StorSimple 裝置管理員服務，並說明如何管理服務註冊金鑰。"
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
ms.openlocfilehash: 1881a0625b107ae1a90e5b772f5296a4d728973d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-the-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="3c130-103">部署 StorSimple Virtual Array 的 StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="3c130-103">Deploy the StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="3c130-104">概觀</span><span class="sxs-lookup"><span data-stu-id="3c130-104">Overview</span></span>

<span data-ttu-id="3c130-105">StorSimple 裝置管理員服務在 Microsoft Azure 中執行，並連接至多個 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="3c130-105">The StorSimple Device Manager service runs in Microsoft Azure and connects to multiple StorSimple devices.</span></span> <span data-ttu-id="3c130-106">建立服務之後，您可以使用服務從在瀏覽器中執行的 Microsoft Azure 入口網站管理這些裝置。</span><span class="sxs-lookup"><span data-stu-id="3c130-106">After you create the service, you can use it to manage the devices from the Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="3c130-107">這可讓您從單一集中位置監視所有連接至 StorSimple 裝置管理員服務的裝置，因而將管理負擔降到最低。</span><span class="sxs-lookup"><span data-stu-id="3c130-107">This allows you to monitor all the devices that are connected to the StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="3c130-108">StorSimple 裝置管理員服務相關的一般工作包括︰</span><span class="sxs-lookup"><span data-stu-id="3c130-108">The common tasks related to a StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="3c130-109">建立服務</span><span class="sxs-lookup"><span data-stu-id="3c130-109">Create a service</span></span>
* <span data-ttu-id="3c130-110">刪除服務</span><span class="sxs-lookup"><span data-stu-id="3c130-110">Delete a service</span></span>
* <span data-ttu-id="3c130-111">取得服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="3c130-111">Get the service registration key</span></span>
* <span data-ttu-id="3c130-112">重新產生服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="3c130-112">Regenerate the service registration key</span></span>

<span data-ttu-id="3c130-113">本教學課程說明如何執行上述每一項工作。</span><span class="sxs-lookup"><span data-stu-id="3c130-113">This tutorial describes how to perform each of the preceding tasks.</span></span> <span data-ttu-id="3c130-114">本文所含資訊僅適用於 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="3c130-114">The information contained in this article is applicable only to StorSimple Virtual Arrays.</span></span> <span data-ttu-id="3c130-115">如需 StorSimple 8000 系列的詳細資訊，請移至 [部署 StorSimple Manager 服務](storsimple-manage-service.md)。</span><span class="sxs-lookup"><span data-stu-id="3c130-115">For more information on StorSimple 8000 series, go to [deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="3c130-116">建立服務</span><span class="sxs-lookup"><span data-stu-id="3c130-116">Create a service</span></span>

<span data-ttu-id="3c130-117">若要建立服務，您需要：</span><span class="sxs-lookup"><span data-stu-id="3c130-117">To create a service, you need to have:</span></span>

* <span data-ttu-id="3c130-118">具有企業合約的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3c130-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="3c130-119">使用中的 Microsoft Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="3c130-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="3c130-120">用於存取管理的計費資訊</span><span class="sxs-lookup"><span data-stu-id="3c130-120">The billing information that is used for access management</span></span>

<span data-ttu-id="3c130-121">您在建立服務時也可以選擇產生儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c130-121">You can also choose to generate a storage account when you create the service.</span></span>

<span data-ttu-id="3c130-122">單一服務可以管理多個裝置。</span><span class="sxs-lookup"><span data-stu-id="3c130-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="3c130-123">不過，裝置不能跨越多個服務。</span><span class="sxs-lookup"><span data-stu-id="3c130-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="3c130-124">大型企業可以擁有多個服務執行個體使用不同的訂用帳戶、組織或甚至是部署位置。</span><span class="sxs-lookup"><span data-stu-id="3c130-124">A large enterprise can have multiple service instances to work with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="3c130-125">您需要個別的 StorSimple 裝置管理員服務執行個體來管理 StorSimple 8000 系列裝置和 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="3c130-125">You need separate instances of StorSimple Device Manager service to manage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="3c130-126">執行下列步驟來建立服務。</span><span class="sxs-lookup"><span data-stu-id="3c130-126">Perform the following steps to create a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="3c130-127">刪除服務</span><span class="sxs-lookup"><span data-stu-id="3c130-127">Delete a service</span></span>

<span data-ttu-id="3c130-128">刪除服務之前，請確定沒有任何連接的裝置正在使用它。</span><span class="sxs-lookup"><span data-stu-id="3c130-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="3c130-129">如果服務正在使用中，請停用連接的裝置。</span><span class="sxs-lookup"><span data-stu-id="3c130-129">If the service is in use, deactivate the connected devices.</span></span> <span data-ttu-id="3c130-130">停用作業將會斷絕裝置與服務之間的連接，但是會保留雲端中的裝置資料。</span><span class="sxs-lookup"><span data-stu-id="3c130-130">The deactivate operation will sever the connection between the device and the service, but preserve the device data in the cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c130-131">刪除服務之後，就無法回復此作業。</span><span class="sxs-lookup"><span data-stu-id="3c130-131">After a service is deleted, the operation cannot be reversed.</span></span> <span data-ttu-id="3c130-132">使用服務的任何裝置在可以搭配另一個服務使用之前，都必須恢復出廠預設值。</span><span class="sxs-lookup"><span data-stu-id="3c130-132">Any device that was using the service will need to be factory reset before it can be used with another service.</span></span> <span data-ttu-id="3c130-133">在此案例中，裝置上的本機資料以及組態將會遺失。</span><span class="sxs-lookup"><span data-stu-id="3c130-133">In this scenario, the local data on the device, as well as the configuration, will be lost.</span></span>
 

<span data-ttu-id="3c130-134">執行下列步驟來刪除服務。</span><span class="sxs-lookup"><span data-stu-id="3c130-134">Perform the following steps to delete a service.</span></span>

#### <a name="to-delete-a-service"></a><span data-ttu-id="3c130-135">刪除服務</span><span class="sxs-lookup"><span data-stu-id="3c130-135">To delete a service</span></span>

1. <span data-ttu-id="3c130-136">移至 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="3c130-136">Go to **All resources**.</span></span> <span data-ttu-id="3c130-137">搜尋您的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="3c130-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="3c130-138">選取您想要刪除的服務。</span><span class="sxs-lookup"><span data-stu-id="3c130-138">Select the service that you wish to delete.</span></span>
   
    ![選取要刪除的服務](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="3c130-140">移至服務儀表板，確保沒有裝置連接至此服務。</span><span class="sxs-lookup"><span data-stu-id="3c130-140">Go to your service dashboard to ensure there are no devices connected to the service.</span></span> <span data-ttu-id="3c130-141">如果沒有裝置向此服務註冊，您也會看到相關的橫幅訊息。</span><span class="sxs-lookup"><span data-stu-id="3c130-141">If there are no devices registered with this service, you will also see a banner message to the effect.</span></span> <span data-ttu-id="3c130-142">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="3c130-142">Click **Delete**.</span></span>
   
    ![刪除服務](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="3c130-144">當系統提示您確認時，按一下確認通知中的 [是]。</span><span class="sxs-lookup"><span data-stu-id="3c130-144">When prompted for confirmation, click **Yes** in the confirmation notification.</span></span> 
   
    ![確認刪除服務](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="3c130-146">刪除服務可能需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="3c130-146">It may take a few minutes for the service to be deleted.</span></span> <span data-ttu-id="3c130-147">成功刪除服務之後會通知您。</span><span class="sxs-lookup"><span data-stu-id="3c130-147">After the service is successfully deleted, you will be notified.</span></span>
   
    ![成功刪除服務](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="3c130-149">將會重新整理服務清單。</span><span class="sxs-lookup"><span data-stu-id="3c130-149">The list of services will be refreshed.</span></span>

 ![更新的服務清單](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-the-service-registration-key"></a><span data-ttu-id="3c130-151">取得服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="3c130-151">Get the service registration key</span></span>
<span data-ttu-id="3c130-152">在您成功建立服務之後，您必須在 StorSimple 裝置註冊服務。</span><span class="sxs-lookup"><span data-stu-id="3c130-152">After you have successfully created a service, you will need to register your StorSimple device with the service.</span></span> <span data-ttu-id="3c130-153">若要註冊您的第一個 StorSimple 裝置，您必須使用服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="3c130-153">To register your first StorSimple device, you will need the service registration key.</span></span> <span data-ttu-id="3c130-154">若要使用現有的 StorSimple 服務註冊其他裝置，您需要註冊金鑰和服務資料加密金鑰 (在註冊期間於第一個裝置上產生)。</span><span class="sxs-lookup"><span data-stu-id="3c130-154">To register additional devices with an existing StorSimple service, you will need both the registration key and the service data encryption key (which is generated on the first device during registration).</span></span> <span data-ttu-id="3c130-155">如需服務資料加密金鑰的詳細資訊，請參閱 [StorSimple 安全性](storsimple-security.md)。</span><span class="sxs-lookup"><span data-stu-id="3c130-155">For more information about the service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="3c130-156">您可以存取服務的 [金鑰] 刀鋒視窗來取得註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="3c130-156">You can get the registration key by accessing the **Keys** blade for your service.</span></span>

<span data-ttu-id="3c130-157">執行下列步驟以取得服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="3c130-157">Perform the following steps to get the service registration key.</span></span>

#### <a name="to-get-the-service-registration-key"></a><span data-ttu-id="3c130-158">若要取得服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="3c130-158">To get the service registration key</span></span>
1. <span data-ttu-id="3c130-159">在 [StorSimple 裝置管理員]中，移至 [管理]**&gt;**[金鑰]。</span><span class="sxs-lookup"><span data-stu-id="3c130-159">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![[金鑰] 刀鋒視窗](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="3c130-161">[金鑰] 刀鋒視窗中會顯示服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="3c130-161">In the **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="3c130-162">使用複製圖示來複製註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="3c130-162">Copy the registration key using the copy icon.</span></span> 

<span data-ttu-id="3c130-163">將服務註冊金鑰保存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="3c130-163">Keep the service registration key in a safe location.</span></span> <span data-ttu-id="3c130-164">您需要這個金鑰，以及服務資料加密金鑰，才能對額外裝置註冊此服務。</span><span class="sxs-lookup"><span data-stu-id="3c130-164">You will need this key, as well as the service data encryption key, to register additional devices with this service.</span></span> <span data-ttu-id="3c130-165">取得服務註冊金鑰之後，您必須透過 Windows PowerShell for StorSimple 介面設定裝置。</span><span class="sxs-lookup"><span data-stu-id="3c130-165">After obtaining the service registration key, you will need to configure your device through the Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-the-service-registration-key"></a><span data-ttu-id="3c130-166">重新產生服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="3c130-166">Regenerate the service registration key</span></span>
<span data-ttu-id="3c130-167">如果您必須執行金鑰替換或服務系統管理員的清單已變更，則您必須重新產生服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="3c130-167">You will need to regenerate a service registration key if you are required to perform key rotation or if the list of service administrators has changed.</span></span> <span data-ttu-id="3c130-168">當您重新產生金鑰時，新的金鑰僅用於註冊後續裝置。</span><span class="sxs-lookup"><span data-stu-id="3c130-168">When you regenerate the key, the new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="3c130-169">已註冊的裝置不會受到此程序影響。</span><span class="sxs-lookup"><span data-stu-id="3c130-169">The devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="3c130-170">執行下列步驟以重新產生服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="3c130-170">Perform the following steps to regenerate a service registration key.</span></span>

#### <a name="to-regenerate-the-service-registration-key"></a><span data-ttu-id="3c130-171">重新產生服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="3c130-171">To regenerate the service registration key</span></span>
1. <span data-ttu-id="3c130-172">在 [StorSimple 裝置管理員]中，移至 [管理]**&gt;**[金鑰]。</span><span class="sxs-lookup"><span data-stu-id="3c130-172">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![[金鑰] 刀鋒視窗](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="3c130-174">在 [金鑰] 刀鋒視窗中，按一下 [重新產生]。</span><span class="sxs-lookup"><span data-stu-id="3c130-174">In the **Keys** blade, click **Regenerate**.</span></span>
   
   ![按一下重新產生](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="3c130-176">在 [重新產生服務註冊金鑰] 刀鋒視窗中，檢閱重新產生金鑰時所需的動作。</span><span class="sxs-lookup"><span data-stu-id="3c130-176">In the **Regenerate service registration key** blade, review the action required when the keys are regenerated.</span></span> <span data-ttu-id="3c130-177">向此服務註冊的所有後續裝置會使用新的註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="3c130-177">All the subsequent devices that are registered with this service will use the new registration key.</span></span> <span data-ttu-id="3c130-178">按一下 [重新產生] 以確認。</span><span class="sxs-lookup"><span data-stu-id="3c130-178">Click **Regenerate** to confirm.</span></span> <span data-ttu-id="3c130-179">註冊完成之後會通知您。</span><span class="sxs-lookup"><span data-stu-id="3c130-179">You will be notified after the registration is complete.</span></span>
   
   ![確認重新產生金鑰](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="3c130-181">新的服務註冊金鑰隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="3c130-181">A new service registration key will appear.</span></span>
   
    ![確認重新產生金鑰](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="3c130-183">複製這個金鑰並儲存，以對任何新的裝置註冊此服務。</span><span class="sxs-lookup"><span data-stu-id="3c130-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c130-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3c130-184">Next steps</span></span>
* <span data-ttu-id="3c130-185">深入了解[開始使用](storsimple-virtual-array-deploy1-portal-prep.md) StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="3c130-185">Learn how to [get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="3c130-186">深入了解 [管理 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="3c130-186">Learn how to [administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

