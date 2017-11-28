---
title: "aaaDeactivate 及刪除 Microsoft Azure StorSimple Virtual Array |Microsoft 文件"
description: "描述如何從服務，方法是先停用後再將其刪除 tooremove StorSimple 裝置。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a><span data-ttu-id="1d146-103">停用及刪除 StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="1d146-103">Deactivate and delete a StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="1d146-104">概觀</span><span class="sxs-lookup"><span data-stu-id="1d146-104">Overview</span></span>

<span data-ttu-id="1d146-105">當您停用 StorSimple Virtual Array 時，您可以中斷 hello hello 裝置與之間連線 hello 相對應的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="1d146-105">When you deactivate a StorSimple Virtual Array, you break hello connection between hello device and hello corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="1d146-106">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="1d146-106">This tutorial explains how to:</span></span>

* <span data-ttu-id="1d146-107">停用裝置</span><span class="sxs-lookup"><span data-stu-id="1d146-107">Deactivate a device</span></span> 
* <span data-ttu-id="1d146-108">刪除或停用裝置</span><span class="sxs-lookup"><span data-stu-id="1d146-108">Delete a deactivated device</span></span>

<span data-ttu-id="1d146-109">本文章中的 hello 資訊適用於僅 tooStorSimple 虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="1d146-109">hello information in this article applies tooStorSimple Virtual Arrays only.</span></span> <span data-ttu-id="1d146-110">如需 8000 系列的資訊，請 toohow 太[停用或刪除裝置](storsimple-deactivate-and-delete-device.md)。</span><span class="sxs-lookup"><span data-stu-id="1d146-110">For information on 8000 series, go toohow too[deactivate or delete a device](storsimple-deactivate-and-delete-device.md).</span></span>

## <a name="when-toodeactivate"></a><span data-ttu-id="1d146-111">當 toodeactivate 嗎？</span><span class="sxs-lookup"><span data-stu-id="1d146-111">When toodeactivate?</span></span>

<span data-ttu-id="1d146-112">停用是永久性的作業，而且無法復原。</span><span class="sxs-lookup"><span data-stu-id="1d146-112">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="1d146-113">您無法以 hello StorSimple 裝置管理員服務重新登錄已停用的裝置。</span><span class="sxs-lookup"><span data-stu-id="1d146-113">You cannot register a deactivated device with hello StorSimple Device Manager service again.</span></span> <span data-ttu-id="1d146-114">您可能需要 toodeactivate 並刪除 StorSimple Virtual Array hello 下列案例中：</span><span class="sxs-lookup"><span data-stu-id="1d146-114">You may need toodeactivate and delete a StorSimple Virtual Array in hello following scenarios:</span></span>

* <span data-ttu-id="1d146-115">**規劃的容錯移轉**： 您的裝置已上線並想 toofail 透過您的裝置。</span><span class="sxs-lookup"><span data-stu-id="1d146-115">**Planned failover** : Your device is online and you plan toofail over your device.</span></span> <span data-ttu-id="1d146-116">如果您計劃 tooupgrade tooa 較大的裝置時，您可能需要 toofail 透過您的裝置。</span><span class="sxs-lookup"><span data-stu-id="1d146-116">If you are planning tooupgrade tooa larger device, you may need toofail over your device.</span></span> <span data-ttu-id="1d146-117">Hello 資料擁有權轉移和 hello 容錯移轉已完成之後，會自動刪除 hello 來源裝置。</span><span class="sxs-lookup"><span data-stu-id="1d146-117">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="1d146-118">**未規劃的容錯移轉**： 您的裝置已離線，而且您需要 toofail 透過 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="1d146-118">**Unplanned failover** : Your device is offline and you need toofail over hello device.</span></span> <span data-ttu-id="1d146-119">Hello 資料中心中斷，而且您的主要裝置已關閉時，可能會在災害期間發生此情況。</span><span class="sxs-lookup"><span data-stu-id="1d146-119">This scenario may occur during a disaster when there is an outage in hello datacenter and your primary device is down.</span></span> <span data-ttu-id="1d146-120">您可以規劃 toofail hello tooa 次要裝置上。</span><span class="sxs-lookup"><span data-stu-id="1d146-120">You plan toofail over hello device tooa secondary device.</span></span> <span data-ttu-id="1d146-121">Hello 資料擁有權轉移和 hello 容錯移轉已完成之後，會自動刪除 hello 來源裝置。</span><span class="sxs-lookup"><span data-stu-id="1d146-121">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="1d146-122">**解除委任**： 想 toodecommission hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="1d146-122">**Decommission** : You want toodecommission hello device.</span></span> <span data-ttu-id="1d146-123">這需要 toofirst 停用 hello 裝置，然後再刪除它。</span><span class="sxs-lookup"><span data-stu-id="1d146-123">This requires you toofirst deactivate hello device and then delete it.</span></span> <span data-ttu-id="1d146-124">當您停用裝置時，您將無法再存取儲存在本機的任何資料。</span><span class="sxs-lookup"><span data-stu-id="1d146-124">When you deactivate a device, you can no longer access any data that is stored locally.</span></span> <span data-ttu-id="1d146-125">您可以儲存在 hello 雲端之唯一存取和復原的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="1d146-125">You can only access and recover hello data stored in hello cloud.</span></span> <span data-ttu-id="1d146-126">如果您打算 tookeep hello 裝置資料停用之後，您應該採取所有資料的雲端快照的集之前停用的裝置。</span><span class="sxs-lookup"><span data-stu-id="1d146-126">If you plan tookeep hello device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="1d146-127">此雲端快照可讓您 toorecover 所有 hello 資料在後續階段。</span><span class="sxs-lookup"><span data-stu-id="1d146-127">This cloud snapshot allows you toorecover all hello data at a later stage.</span></span>

## <a name="deactivate-a-device"></a><span data-ttu-id="1d146-128">停用裝置</span><span class="sxs-lookup"><span data-stu-id="1d146-128">Deactivate a device</span></span>

<span data-ttu-id="1d146-129">toodeactivate 您的裝置，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="1d146-129">toodeactivate your device, perform hello following steps.</span></span>

#### <a name="toodeactivate-hello-device"></a><span data-ttu-id="1d146-130">toodeactivate hello 裝置</span><span class="sxs-lookup"><span data-stu-id="1d146-130">toodeactivate hello device</span></span>

1. <span data-ttu-id="1d146-131">在您的服務，請移過**管理 > 裝置**。</span><span class="sxs-lookup"><span data-stu-id="1d146-131">In your service, go too**Management > Devices**.</span></span> <span data-ttu-id="1d146-132">在 hello**裝置**刀鋒視窗，按一下，然後選取 hello 裝置，您會希望 toodeactivate。</span><span class="sxs-lookup"><span data-stu-id="1d146-132">In hello **Devices** blade, click and select hello device that you wish toodeactivate.</span></span>
   
    ![選取裝置 toodeactivate](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. <span data-ttu-id="1d146-134">在您**裝置儀表板**刀鋒視窗中，按一下 [ **...多個**hello] 清單中，從選取**停用**。</span><span class="sxs-lookup"><span data-stu-id="1d146-134">In your **Device dashboard** blade, click **… More** and from hello list, select **Deactivate**.</span></span>
   
    ![按一下停用](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. <span data-ttu-id="1d146-136">在 hello**停用**刀鋒視窗中，型別 hello 裝置名稱，然後按一下**停用**。</span><span class="sxs-lookup"><span data-stu-id="1d146-136">In hello **Deactivate** blade, type hello device name and then click **Deactivate**.</span></span> 
   
    ![確認停用](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    <span data-ttu-id="1d146-138">hello 停用程序會啟動並在幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="1d146-138">hello deactivate process starts and takes a few minutes toocomplete.</span></span>
   
    ![停用進行中](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. <span data-ttu-id="1d146-140">停用之後，重新整理裝置 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="1d146-140">After deactivation, hello list of devices refreshes.</span></span>
   
    ![停用完成](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    <span data-ttu-id="1d146-142">您現在可以刪除此裝置。</span><span class="sxs-lookup"><span data-stu-id="1d146-142">You can now delete this device.</span></span>

## <a name="delete-hello-device"></a><span data-ttu-id="1d146-143">刪除裝置 hello</span><span class="sxs-lookup"><span data-stu-id="1d146-143">Delete hello device</span></span>

<span data-ttu-id="1d146-144">裝置有 toobe 第一個已停用的 toodelete 它。</span><span class="sxs-lookup"><span data-stu-id="1d146-144">A device has toobe first deactivated toodelete it.</span></span> <span data-ttu-id="1d146-145">刪除裝置，即會從裝置連接的 toohello 服務的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="1d146-145">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="1d146-146">hello 服務可以再管理 hello 刪除裝置。</span><span class="sxs-lookup"><span data-stu-id="1d146-146">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="1d146-147">不過與 hello 裝置相關聯的 hello 資料會維持 hello 雲端。</span><span class="sxs-lookup"><span data-stu-id="1d146-147">hello data associated with hello device however remains in hello cloud.</span></span> <span data-ttu-id="1d146-148">所以這項資料會累算費用。</span><span class="sxs-lookup"><span data-stu-id="1d146-148">This data then accrues charges.</span></span>

<span data-ttu-id="1d146-149">toodelete hello 裝置，請執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="1d146-149">toodelete hello device, perform hello following steps.</span></span>

#### <a name="toodelete-hello-device"></a><span data-ttu-id="1d146-150">toodelete hello 裝置</span><span class="sxs-lookup"><span data-stu-id="1d146-150">toodelete hello device</span></span>

1. <span data-ttu-id="1d146-151">在您 StorSimple 裝置管理員 」 中，跳過**管理 > 裝置**。</span><span class="sxs-lookup"><span data-stu-id="1d146-151">In your StorSimple Device Manager, go too**Management > Devices**.</span></span> <span data-ttu-id="1d146-152">在 hello**裝置**刀鋒視窗中，選取您想 toodelete 停用的裝置。</span><span class="sxs-lookup"><span data-stu-id="1d146-152">In hello **Devices** blade, select a deactivated device that you wish toodelete.</span></span>
2. <span data-ttu-id="1d146-153">在 hello**裝置儀表板**刀鋒視窗中，按一下  **...多個**，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="1d146-153">In hello **Device dashboard** blade, click **… More** and then click **Delete**.</span></span>
   
   ![選取裝置 toodelete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. <span data-ttu-id="1d146-155">在 hello**刪除**刀鋒視窗中，輸入 hello 名稱，您的裝置 tooconfirm hello 刪除然後再按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="1d146-155">In hello **Delete** blade, type hello name of your device tooconfirm hello deletion and then click **Delete**.</span></span> <span data-ttu-id="1d146-156">正在刪除 hello 裝置不會刪除 hello 與 hello 裝置相關聯的雲端資料。</span><span class="sxs-lookup"><span data-stu-id="1d146-156">Deleting hello device does not delete hello cloud data associated with hello device.</span></span> 
   
   ![Confirm delete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. <span data-ttu-id="1d146-158">hello 刪除啟動，並採用幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="1d146-158">hello deletion starts and takes a few minutes toocomplete.</span></span>
   
   ![刪除進行中](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    <span data-ttu-id="1d146-160">刪除 hello 裝置之後，您可以檢視裝置 hello 更新清單。</span><span class="sxs-lookup"><span data-stu-id="1d146-160">After hello device is deleted, you can view hello updated list of devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d146-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d146-161">Next steps</span></span>

* <span data-ttu-id="1d146-162">如需詳細資訊，透過 toofail 移過[容錯移轉和災害復原您的 StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md)。</span><span class="sxs-lookup"><span data-stu-id="1d146-162">For information on how toofail over, go too[Failover and disaster recovery of your StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md).</span></span>

* <span data-ttu-id="1d146-163">toolearn 深入了解如何 toouse hello StorSimple 裝置管理員服務移過[使用 hello StorSimple 裝置管理員服務 tooadminister 您 StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="1d146-163">toolearn more about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span> 

