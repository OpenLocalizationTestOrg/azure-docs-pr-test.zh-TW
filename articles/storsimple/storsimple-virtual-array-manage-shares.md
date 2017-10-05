---
title: "管理 StorSimple Virtual Array 共用 | Microsoft Docs"
description: "描述 StorSimple 裝置管理員，並說明如何使用它來管理 StorSimple Virtual Array 上的共用。"
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: e5c62689de36baa175001f5f4f70d87568876ef0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-shares-on-the-storsimple-virtual-array"></a><span data-ttu-id="e4492-103">使用 StorSimple 裝置管理員服務管理 StorSimple Virtual Array 上的共用</span><span class="sxs-lookup"><span data-stu-id="e4492-103">Use the StorSimple Device Manager service to manage shares on the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="e4492-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e4492-104">Overview</span></span>

<span data-ttu-id="e4492-105">本教學課程說明如何使用 StorSimple 裝置管理員服務，在 StorSimple Virtual Array 上建立和管理共用。</span><span class="sxs-lookup"><span data-stu-id="e4492-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="e4492-106">StorSimple 裝置管理員服務是 Azure 入口網站中的一項擴充，可讓您從單一 Web 介面來管理 StorSimple 解決方案。</span><span class="sxs-lookup"><span data-stu-id="e4492-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="e4492-107">除了管理共用和磁碟區，您還可以使用 StorSimple 裝置管理員服務來檢視和管理裝置、檢視警示、管理備份原則，以及管理備份目錄。</span><span class="sxs-lookup"><span data-stu-id="e4492-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, manage backup policies, and manage the backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="e4492-108">共用類型</span><span class="sxs-lookup"><span data-stu-id="e4492-108">Share Types</span></span>

<span data-ttu-id="e4492-109">StorSimple 共用可以是︰</span><span class="sxs-lookup"><span data-stu-id="e4492-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="e4492-110">**固定在本機**︰這些共用中的資料永遠停留在陣列上，不會流向雲端。</span><span class="sxs-lookup"><span data-stu-id="e4492-110">**Locally pinned**: Data in these shares stays on the array at all times and does not spill to the cloud.</span></span>
* <span data-ttu-id="e4492-111">**階層式**：這些磁碟區中的資料可能流向雲端。</span><span class="sxs-lookup"><span data-stu-id="e4492-111">**Tiered**: Data in these shares can spill to the cloud.</span></span> <span data-ttu-id="e4492-112">當您建立階層式共用時，大約 10% 的空間會佈建在本機層，而 90% 的空間會佈建在雲端。</span><span class="sxs-lookup"><span data-stu-id="e4492-112">When you create a tiered share, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span></span> <span data-ttu-id="e4492-113">舉例來說，如果您佈建 1 TB 的共用，當資料分層時，有 100 GB 會位於本機空間，900 GB 會用於雲端。</span><span class="sxs-lookup"><span data-stu-id="e4492-113">For example, if you provisioned a 1 TB share, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="e4492-114">這也意味著，如果裝置的可用空間用盡，您就無法佈建階層式共用 (因為本機層上需要的 10% 無法使用)。</span><span class="sxs-lookup"><span data-stu-id="e4492-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered share (because the 10 % required on the local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="e4492-115">佈建的容量</span><span class="sxs-lookup"><span data-stu-id="e4492-115">Provisioned capacity</span></span>

<span data-ttu-id="e4492-116">請參閱下表以了解每個共用類型的最大佈建容量。</span><span class="sxs-lookup"><span data-stu-id="e4492-116">Refer to the following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="e4492-117">**限制識別碼**</span><span class="sxs-lookup"><span data-stu-id="e4492-117">**Limit identifier**</span></span> | <span data-ttu-id="e4492-118">**限制**</span><span class="sxs-lookup"><span data-stu-id="e4492-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="e4492-119">分層共用的大小下限</span><span class="sxs-lookup"><span data-stu-id="e4492-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="e4492-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="e4492-120">500 GB</span></span> |
| <span data-ttu-id="e4492-121">分層共用的大小上限</span><span class="sxs-lookup"><span data-stu-id="e4492-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="e4492-122">20 TB</span><span class="sxs-lookup"><span data-stu-id="e4492-122">20 TB</span></span> |
| <span data-ttu-id="e4492-123">固定在本機的共用的大小下限</span><span class="sxs-lookup"><span data-stu-id="e4492-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="e4492-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="e4492-124">50 GB</span></span> |
| <span data-ttu-id="e4492-125">固定在本機的共用的大小上限</span><span class="sxs-lookup"><span data-stu-id="e4492-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="e4492-126">2 TB</span><span class="sxs-lookup"><span data-stu-id="e4492-126">2 TB</span></span> |

## <a name="the-shares-blade"></a><span data-ttu-id="e4492-127">[共用] 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="e4492-127">The Shares blade</span></span>

<span data-ttu-id="e4492-128">StorSimple 服務摘要刀鋒視窗的 [共用] 功能表會顯示給定 StorSimple 陣列上的儲存體共用清單，還可讓您管理它們。</span><span class="sxs-lookup"><span data-stu-id="e4492-128">The **Shares** menu on your StorSimple service summary blade displays the list of storage shares on a given StorSimple array and allows you to manage them.</span></span>

![[共用] 刀鋒視窗](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="e4492-130">共用包含一系列屬性：</span><span class="sxs-lookup"><span data-stu-id="e4492-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="e4492-131">**共用名稱** – 必須是唯一且有助於識別共用的描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="e4492-131">**Share Name** – A descriptive name that must be unique and helps identify the share.</span></span>
* <span data-ttu-id="e4492-132">**狀態** – 可為連線或離線。</span><span class="sxs-lookup"><span data-stu-id="e4492-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="e4492-133">如果共用已離線，共用的使用者將無法存取它。</span><span class="sxs-lookup"><span data-stu-id="e4492-133">If a share is offline, users of the share will not be able to access it.</span></span>
* <span data-ttu-id="e4492-134">**類型** – 指出共用為**階層式** (預設值) 或**固定在本機**。</span><span class="sxs-lookup"><span data-stu-id="e4492-134">**Type** – Indicates whether the share is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="e4492-135">**容量** – 相較於共用上可儲存的資料總量，指定已用的資料量。</span><span class="sxs-lookup"><span data-stu-id="e4492-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored on the share.</span></span>
* <span data-ttu-id="e4492-136">**描述** – 有助於描述共用的選擇性設定。</span><span class="sxs-lookup"><span data-stu-id="e4492-136">**Description** – An optional setting that helps describe the share.</span></span>
* <span data-ttu-id="e4492-137">**權限** -可透過 Windows 檔案總管來管理的共用 NTFS 權限。</span><span class="sxs-lookup"><span data-stu-id="e4492-137">**Permissions** - The NTFS permissions to the share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="e4492-138">**備份** – 如果是 StorSimple Virtual Array，所有共用會自動啟用備份。</span><span class="sxs-lookup"><span data-stu-id="e4492-138">**Backup** – In case of the StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![共用的詳細資料](./media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="e4492-140">使用本教學課程中的指示以執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="e4492-140">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="e4492-141">新增共用</span><span class="sxs-lookup"><span data-stu-id="e4492-141">Add a share</span></span>
* <span data-ttu-id="e4492-142">修改共用</span><span class="sxs-lookup"><span data-stu-id="e4492-142">Modify a share</span></span>
* <span data-ttu-id="e4492-143">讓共用離線</span><span class="sxs-lookup"><span data-stu-id="e4492-143">Take a share offline</span></span>
* <span data-ttu-id="e4492-144">刪除共用</span><span class="sxs-lookup"><span data-stu-id="e4492-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="e4492-145">新增共用</span><span class="sxs-lookup"><span data-stu-id="e4492-145">Add a share</span></span>

1. <span data-ttu-id="e4492-146">從 StorSimple 服務摘要刀鋒視窗中，從命令列按一下 [+ 新增共用]。</span><span class="sxs-lookup"><span data-stu-id="e4492-146">From the StorSimple service summary blade, click **+ Add share** from the command bar.</span></span> <span data-ttu-id="e4492-147">這會開啟 [新增共用] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e4492-147">This opens up the **Add share** blade.</span></span>

    ![新增共用](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="e4492-149">在 [新增共用] 刀鋒視窗中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="e4492-149">In the **Add share** blade, do the following:</span></span>
   
    1. <span data-ttu-id="e4492-150">在 [共用名稱] 欄位中，輸入共用的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="e4492-150">In the **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="e4492-151">該名稱必須為包含 3 至 127 個字元的字串。</span><span class="sxs-lookup"><span data-stu-id="e4492-151">The name must be a string that contains 3 to 127 characters.</span></span>

    2. <span data-ttu-id="e4492-152">共用的選擇性 [說明]。</span><span class="sxs-lookup"><span data-stu-id="e4492-152">An optional **Description** for the share.</span></span> <span data-ttu-id="e4492-153">說明將可協助識別共用的擁有者。</span><span class="sxs-lookup"><span data-stu-id="e4492-153">The description will help identify the share owners.</span></span>

    3. <span data-ttu-id="e4492-154">在 [類型] 下拉式清單中，指定要建立 [階層式] 還是 [固定在本機] 共用。</span><span class="sxs-lookup"><span data-stu-id="e4492-154">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="e4492-155">對於需要本機保證、低延遲，以及高效能的工作負載，請選取 [固定在本機的共用] 。</span><span class="sxs-lookup"><span data-stu-id="e4492-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="e4492-156">對於所有其他資料，請選取 [階層式] 共用。</span><span class="sxs-lookup"><span data-stu-id="e4492-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="e4492-157">在 [容量] 欄位中，指定共用大小。</span><span class="sxs-lookup"><span data-stu-id="e4492-157">In the **Capacity** field, specify the size of the share.</span></span> <span data-ttu-id="e4492-158">階層式共用必須介於 500 GB 和 20 TB 之間，而固定在本機的共用必須介於 50 GB 和 2 TB 之間。</span><span class="sxs-lookup"><span data-stu-id="e4492-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="e4492-159">在 [將預設完整權限設為] 欄位中，指派權限給存取此共用的使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="e4492-159">In the **Set default full permissions to** field, assign the permissions to the user, or the group that is accessing this share.</span></span> <span data-ttu-id="e4492-160">請以下列格式指定使用者或使用者群組的名稱：_john@contoso.com_。</span><span class="sxs-lookup"><span data-stu-id="e4492-160">Specify the name of the user or the user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="e4492-161">我們建議您利用使用者群組 (而非單一使用者)，來授予可存取這些共用的系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="e4492-161">We recommend that you use a user group (instead of a single user) to allow admin privileges to access these shares.</span></span> <span data-ttu-id="e4492-162">當您在此指派權限之後，就可以使用 [檔案總管] 來修改這些權限。</span><span class="sxs-lookup"><span data-stu-id="e4492-162">After you have assigned the permissions here, you can then use File Explorer to modify these permissions.</span></span>
3. <span data-ttu-id="e4492-163">共用設定完成之後，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="e4492-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="e4492-164">將會使用指定的設定來建立共用，您會看到通知。</span><span class="sxs-lookup"><span data-stu-id="e4492-164">A share will be created with the specified settings and you will see a notification.</span></span> <span data-ttu-id="e4492-165">根據預設，共用會啟用備份。</span><span class="sxs-lookup"><span data-stu-id="e4492-165">By default, backup will be enabled for the share.</span></span>
4. <span data-ttu-id="e4492-166">若要確認已成功建立共用，請移至 [共用] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e4492-166">To confirm that the share was successfully created, go to the **Shares** blade.</span></span> <span data-ttu-id="e4492-167">您應該會看列出共用。</span><span class="sxs-lookup"><span data-stu-id="e4492-167">You should see the share listed.</span></span>
   
    ![共用建立成功](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="e4492-169">修改共用</span><span class="sxs-lookup"><span data-stu-id="e4492-169">Modify a share</span></span>

<span data-ttu-id="e4492-170">當您需要變更共用的描述時，請修改共用。</span><span class="sxs-lookup"><span data-stu-id="e4492-170">Modify a share when you need to change the description of the share.</span></span> <span data-ttu-id="e4492-171">建立共用之後，就無法修改其他共用屬性。</span><span class="sxs-lookup"><span data-stu-id="e4492-171">No other share properties can be modified once the share is created.</span></span>

#### <a name="to-modify-a-share"></a><span data-ttu-id="e4492-172">若要修改共用</span><span class="sxs-lookup"><span data-stu-id="e4492-172">To modify a share</span></span>

1. <span data-ttu-id="e4492-173">從 StorSimple 服務摘要刀鋒視窗的 [共用] 設定中，選取您想要修改的共用所在的虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="e4492-173">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to modify resides.</span></span>
2. <span data-ttu-id="e4492-174">**選取**共用以檢視目前的描述並修改。</span><span class="sxs-lookup"><span data-stu-id="e4492-174">**Select** the share to view the current description and modify it.</span></span>
3. <span data-ttu-id="e4492-175">按一下 [儲存] 命令列以儲存變更。</span><span class="sxs-lookup"><span data-stu-id="e4492-175">Save your changes by clicking the **Save** command bar.</span></span> <span data-ttu-id="e4492-176">將會套用您指定的設定，您會看到通知。</span><span class="sxs-lookup"><span data-stu-id="e4492-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="e4492-177">編輯共用</span><span class="sxs-lookup"><span data-stu-id="e4492-177">Edit share</span></span>](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="e4492-178">讓共用離線</span><span class="sxs-lookup"><span data-stu-id="e4492-178">Take a share offline</span></span>

<span data-ttu-id="e4492-179">當您打算修改或刪除共用時，可能需要先讓共用離線。</span><span class="sxs-lookup"><span data-stu-id="e4492-179">You may need to take a share offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="e4492-180">當共用已離線時，即無法進行讀寫存取。</span><span class="sxs-lookup"><span data-stu-id="e4492-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="e4492-181">您必須讓主機和裝置上的共用都離線。</span><span class="sxs-lookup"><span data-stu-id="e4492-181">You will need to take the share offline on the host as well as on the device.</span></span>

#### <a name="to-take-a-share-offline"></a><span data-ttu-id="e4492-182">若要讓共用離線</span><span class="sxs-lookup"><span data-stu-id="e4492-182">To take a share offline</span></span>

1. <span data-ttu-id="e4492-183">請確定此共用不在使用中，再讓它離線。</span><span class="sxs-lookup"><span data-stu-id="e4492-183">Make sure that the share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="e4492-184">執行下列步驟，讓陣列上的共用離線︰</span><span class="sxs-lookup"><span data-stu-id="e4492-184">Take the share on the array offline by performing the following steps:</span></span>
   
    1. <span data-ttu-id="e4492-185">從 StorSimple 服務摘要刀鋒視窗的 [共用] 設定中，選取您想要設為離線的共用所在的虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="e4492-185">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to take offline resides.</span></span>

    2. <span data-ttu-id="e4492-186">**選取** 共用，從操作功能表中按一下 [...] (或以滑鼠右鍵按一下此資料列)，然後選取 [離線]。</span><span class="sxs-lookup"><span data-stu-id="e4492-186">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span></span>
     
        ![離線共用](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="e4492-188">檢閱 [離線] 刀鋒視窗中的資訊，並確認您接受此作業。</span><span class="sxs-lookup"><span data-stu-id="e4492-188">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span></span> <span data-ttu-id="e4492-189">按一下 [離線] 讓共用離線。</span><span class="sxs-lookup"><span data-stu-id="e4492-189">Click **Take offline** to take the share offline.</span></span> <span data-ttu-id="e4492-190">您會看到作業進行中的通知。</span><span class="sxs-lookup"><span data-stu-id="e4492-190">You will see a notification of the operation in progress.</span></span>

    4. <span data-ttu-id="e4492-191">若要確認共用已成功離線，請移至 [共用] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e4492-191">To confirm that the share was successfully taken offline, go to the **Shares** blade.</span></span> <span data-ttu-id="e4492-192">您應該會看到共用的狀態為離線。</span><span class="sxs-lookup"><span data-stu-id="e4492-192">You should see the status of the share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="e4492-193">刪除共用</span><span class="sxs-lookup"><span data-stu-id="e4492-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4492-194">只有已離線的共用才能刪除。</span><span class="sxs-lookup"><span data-stu-id="e4492-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="e4492-195">請完成下列步驟來刪除共用。</span><span class="sxs-lookup"><span data-stu-id="e4492-195">Complete the following steps to delete a share.</span></span>

#### <a name="to-delete-a-share"></a><span data-ttu-id="e4492-196">若要刪除共用</span><span class="sxs-lookup"><span data-stu-id="e4492-196">To delete a share</span></span>

1. <span data-ttu-id="e4492-197">從 StorSimple 服務摘要刀鋒視窗的 [共用] 設定中，選取您想要刪除的共用所在的虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="e4492-197">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish to delete resides.</span></span>
2. <span data-ttu-id="e4492-198">**選取** 共用，從操作功能表中按一下 [...] (或以滑鼠右鍵按一下此資料列)，然後選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="e4492-198">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span></span>
   
    ![刪除共用](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="e4492-200">檢查您想要刪除之共用的狀態。</span><span class="sxs-lookup"><span data-stu-id="e4492-200">Check the status of the share you want to delete.</span></span> <span data-ttu-id="e4492-201">如果您想要刪除的共用未離線，請先讓它離線。</span><span class="sxs-lookup"><span data-stu-id="e4492-201">If the share you want to delete is not offline, take it offline first.</span></span> <span data-ttu-id="e4492-202">請遵循[讓共用離線](#take-a-share-offline)中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="e4492-202">Follow the steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="e4492-203">當 [刪除]**刪除** 刀鋒視窗中提示您確認時，請接受確認並按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="e4492-203">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span></span> <span data-ttu-id="e4492-204">現在將刪除共用，[共用] 刀鋒視窗會顯示虛擬陣列內更新的共用清單。</span><span class="sxs-lookup"><span data-stu-id="e4492-204">The share will now be deleted and the **Shares** blade shows the updated list of shares within the virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4492-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e4492-205">Next steps</span></span>
<span data-ttu-id="e4492-206">了解如何[複製 StorSimple 共用](storsimple-virtual-array-clone.md)。</span><span class="sxs-lookup"><span data-stu-id="e4492-206">Learn how to [clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>

