---
title: "Microsoft Azure StorSimple Manager Virtual Array 管理 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站中的 StorSimple 裝置管理員服務管理 StorSimple 內部部署 Virtual Array。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 958244a5-f9f5-455e-b7ef-71a65558872e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: a74a160eae88a2d03460a1346479c333d8f9d524
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-administer-your-storsimple-virtual-array"></a><span data-ttu-id="994ec-103">使用 StorSimple 裝置管理員服務管理 StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="994ec-103">Use the StorSimple Device Manager service to administer your StorSimple Virtual Array</span></span>
![安裝程序流程](./media/storsimple-virtual-array-manager-service-administration/manage4.png)

## <a name="overview"></a><span data-ttu-id="994ec-105">概觀</span><span class="sxs-lookup"><span data-stu-id="994ec-105">Overview</span></span>
<span data-ttu-id="994ec-106">本文描述 StorSimple 裝置管理員服務介面，包括如何連接它和各種可用的選項，並提供可以透過此 UI 執行的特定工作流程的連結。</span><span class="sxs-lookup"><span data-stu-id="994ec-106">This article describes the StorSimple Device Manager service interface, including how to connect to it and the various options available, and provides links to the specific workflows that can be performed via this UI.</span></span>

<span data-ttu-id="994ec-107">閱讀本文之後，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="994ec-107">After reading this article, you will know how to:</span></span>

* <span data-ttu-id="994ec-108">連接至 StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="994ec-108">Connect to the StorSimple Device Manager service</span></span>
* <span data-ttu-id="994ec-109">瀏覽 StorSimple 裝置管理員 UI</span><span class="sxs-lookup"><span data-stu-id="994ec-109">Navigate the StorSimple Device Manager UI</span></span>
* <span data-ttu-id="994ec-110">透過 StorSimple 裝置管理員服務管理 StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="994ec-110">Administer your StorSimple Virtual Array via the StorSimple Device Manager service</span></span>

> [!NOTE]
> <span data-ttu-id="994ec-111">若要檢視 StorSimple 8000 系列裝置可用的管理選項，請移至 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="994ec-111">To view the management options available for the StorSimple 8000 series device, go to [Use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>
> 
> 

## <a name="connect-to-the-storsimple-device-manager-service"></a><span data-ttu-id="994ec-112">連接至 StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="994ec-112">Connect to the StorSimple Device Manager service</span></span>
<span data-ttu-id="994ec-113">StorSimple Manager 裝置管理員服務在 Microsoft Azure 中執行，並連接至多個 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="994ec-113">The StorSimple Device Manager service runs in Microsoft Azure and connects to multiple StorSimple Virtual Arrays.</span></span> <span data-ttu-id="994ec-114">您可以使用在瀏覽器中執行的中央 Microsoft Azure 入口網站來管理這些裝置。</span><span class="sxs-lookup"><span data-stu-id="994ec-114">You use a central Microsoft Azure portal running in a browser to manage these devices.</span></span> <span data-ttu-id="994ec-115">若要連接至 StorSimple 裝置管理員服務，請執行下列動作。</span><span class="sxs-lookup"><span data-stu-id="994ec-115">To connect to the StorSimple Device Manager service, do the following.</span></span>

#### <a name="to-connect-to-the-service"></a><span data-ttu-id="994ec-116">連接至此服務</span><span class="sxs-lookup"><span data-stu-id="994ec-116">To connect to the service</span></span>
1. <span data-ttu-id="994ec-117">移至 [https://ms.portal.azure.com](https://ms.portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="994ec-117">Go to [https://ms.portal.azure.com](https://ms.portal.azure.com).</span></span>
2. <span data-ttu-id="994ec-118">使用您的 Microsoft 帳戶認證，登入 Microsoft Azure 入口網站 (位於窗格右上角)。</span><span class="sxs-lookup"><span data-stu-id="994ec-118">Using your Microsoft account credentials, log on to the Microsoft Azure portal (located at the top-right of the pane).</span></span>
3. <span data-ttu-id="994ec-119">在 StorSimple 裝置管理員上瀏覽至 [瀏覽] --> [篩選]，以檢視指定訂用帳戶中所有的裝置管理員。</span><span class="sxs-lookup"><span data-stu-id="994ec-119">Navigate to Browse --> 'Filter' on StorSimple Device Managers to view all your device managers in a given subscription.</span></span>

## <a name="use-the-storsimple-device-manager-service-to-perform-management-tasks"></a><span data-ttu-id="994ec-120">使用 StorSimple 裝置管理員服務來執行管理工作</span><span class="sxs-lookup"><span data-stu-id="994ec-120">Use the StorSimple Device Manager service to perform management tasks</span></span>
<span data-ttu-id="994ec-121">下表顯示所有一般管理工作和複雜工作流程 (可在 StorSimple 裝置管理員服務摘要刀鋒視窗內執行) 的摘要。</span><span class="sxs-lookup"><span data-stu-id="994ec-121">The following table shows a summary of all the common management tasks and complex workflows that can be performed within the StorSimple Device Manager service summary blade.</span></span> <span data-ttu-id="994ec-122">這些工作會根據在其中啟動它們的刀鋒視窗加以組織。</span><span class="sxs-lookup"><span data-stu-id="994ec-122">These tasks are organized based on the blades on which they are initiated.</span></span>

<span data-ttu-id="994ec-123">如需每個工作流程的詳細資訊，請按一下資料表中的適當程序。</span><span class="sxs-lookup"><span data-stu-id="994ec-123">For more information about each workflow, click the appropriate procedure in the table.</span></span>

#### <a name="storsimple-device-manager-workflows"></a><span data-ttu-id="994ec-124">StorSimple 裝置管理員工作流程</span><span class="sxs-lookup"><span data-stu-id="994ec-124">StorSimple Device Manager workflows</span></span>
| <span data-ttu-id="994ec-125">如果您想要執行此動作...</span><span class="sxs-lookup"><span data-stu-id="994ec-125">If you want to do this ...</span></span> | <span data-ttu-id="994ec-126">使用此程序</span><span class="sxs-lookup"><span data-stu-id="994ec-126">Use this procedure</span></span> |
| --- | --- | --- |
| <span data-ttu-id="994ec-127">建立服務</span><span class="sxs-lookup"><span data-stu-id="994ec-127">Create a service</span></span></br><span data-ttu-id="994ec-128">刪除服務</span><span class="sxs-lookup"><span data-stu-id="994ec-128">Delete a service</span></span></br><span data-ttu-id="994ec-129">取得服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="994ec-129">Get the service registration key</span></span></br><span data-ttu-id="994ec-130">重新產生服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="994ec-130">Regenerate the service registration key</span></span> |[<span data-ttu-id="994ec-131">部署 StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="994ec-131">Deploy the StorSimple Device Manager service</span></span>](storsimple-virtual-array-manage-service.md) |
| <span data-ttu-id="994ec-132">檢視活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="994ec-132">View the activity logs</span></span> |[<span data-ttu-id="994ec-133">使用 StorSimple 服務摘要</span><span class="sxs-lookup"><span data-stu-id="994ec-133">Use the StorSimple service summary</span></span>](storsimple-virtual-array-service-summary.md) |
| <span data-ttu-id="994ec-134">停用 Virtual Array</span><span class="sxs-lookup"><span data-stu-id="994ec-134">Deactivate a Virtual Array</span></span></br><span data-ttu-id="994ec-135">刪除 Virtual Array</span><span class="sxs-lookup"><span data-stu-id="994ec-135">Delete a Virtual Array</span></span> |[<span data-ttu-id="994ec-136">停用或刪除虛擬陣列</span><span class="sxs-lookup"><span data-stu-id="994ec-136">Deactivate or delete a virtual array</span></span>](storsimple-virtual-array-deactivate-and-delete-device.md) |
| <span data-ttu-id="994ec-137">災害復原和裝置容錯移轉</span><span class="sxs-lookup"><span data-stu-id="994ec-137">Disaster recovery and device failover</span></span></br><span data-ttu-id="994ec-138">容錯移轉必要條件</span><span class="sxs-lookup"><span data-stu-id="994ec-138">Failover prerequisites</span></span></br><span data-ttu-id="994ec-139">業務持續性災害復原 (BCDR)</span><span class="sxs-lookup"><span data-stu-id="994ec-139">Business continuity disaster recovery (BCDR)</span></span></br><span data-ttu-id="994ec-140">災害復原時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="994ec-140">Errors during disaster recovery</span></span> |[<span data-ttu-id="994ec-141">StorSimple Virtual Array 的災害復原和裝置容錯移轉</span><span class="sxs-lookup"><span data-stu-id="994ec-141">Disaster recovery and device failover for your StorSimple Virtual Array</span></span>](storsimple-virtual-array-failover-dr.md) |
| <span data-ttu-id="994ec-142">備份共用和磁碟區</span><span class="sxs-lookup"><span data-stu-id="994ec-142">Back up shares and volumes</span></span></br><span data-ttu-id="994ec-143">進行手動備份</span><span class="sxs-lookup"><span data-stu-id="994ec-143">Take a manual backup</span></span></br><span data-ttu-id="994ec-144">變更備份排程</span><span class="sxs-lookup"><span data-stu-id="994ec-144">Change the backup schedule</span></span></br><span data-ttu-id="994ec-145">檢視現有的備份</span><span class="sxs-lookup"><span data-stu-id="994ec-145">View existing backups</span></span> |[<span data-ttu-id="994ec-146">備份 StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="994ec-146">Back up your StorSimple Virtual Array</span></span>](storsimple-virtual-array-backup.md) |
| <span data-ttu-id="994ec-147">從備份組複製共用</span><span class="sxs-lookup"><span data-stu-id="994ec-147">Clone shares from a backup set</span></span></br><span data-ttu-id="994ec-148">從備份組複製磁碟區</span><span class="sxs-lookup"><span data-stu-id="994ec-148">Clone volumes from a backup set</span></span></br><span data-ttu-id="994ec-149">項目層級復原 (僅限檔案伺服器)</span><span class="sxs-lookup"><span data-stu-id="994ec-149">Item-level recovery (file server only)</span></span> |[<span data-ttu-id="994ec-150">從 StorSimple Virtual Array 的備份複製</span><span class="sxs-lookup"><span data-stu-id="994ec-150">Clone from a backup of your StorSimple Virtual Array</span></span>](storsimple-virtual-array-clone.md) |
| <span data-ttu-id="994ec-151">有關儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="994ec-151">About  storage accounts</span></span></br><span data-ttu-id="994ec-152">新增儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="994ec-152">Add a storage account</span></span></br><span data-ttu-id="994ec-153">編輯儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="994ec-153">Edit a storage account</span></span></br><span data-ttu-id="994ec-154">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="994ec-154">Delete a storage account</span></span> |[<span data-ttu-id="994ec-155">管理 StorSimple Virtual Array 的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="994ec-155">Manage storage accounts for the StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-storage-accounts.md) |
| <span data-ttu-id="994ec-156">關於存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="994ec-156">About access control records</span></span></br><span data-ttu-id="994ec-157">加入或修改存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="994ec-157">Add or modify an access control record</span></span> </br><span data-ttu-id="994ec-158">刪除存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="994ec-158">Delete an access control record</span></span> |[<span data-ttu-id="994ec-159">管理 StorSimple Virtual Array 的存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="994ec-159">Manage access control records for the StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-acrs.md) |
| <span data-ttu-id="994ec-160">檢視工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="994ec-160">View job details</span></span> |[<span data-ttu-id="994ec-161">管理 StorSimple Virtual Array 作業</span><span class="sxs-lookup"><span data-stu-id="994ec-161">Manage StorSimple Virtual Array jobs</span></span>](storsimple-virtual-array-manage-jobs.md) |
| <span data-ttu-id="994ec-162">設定警示設定</span><span class="sxs-lookup"><span data-stu-id="994ec-162">Configure alert settings</span></span></br><span data-ttu-id="994ec-163">接收警示通知</span><span class="sxs-lookup"><span data-stu-id="994ec-163">Receive alert notifications</span></span></br><span data-ttu-id="994ec-164">管理警示</span><span class="sxs-lookup"><span data-stu-id="994ec-164">Manage alerts</span></span></br><span data-ttu-id="994ec-165">檢閱警示</span><span class="sxs-lookup"><span data-stu-id="994ec-165">Review alerts</span></span> |[<span data-ttu-id="994ec-166">檢視和管理 StorSimple Virtual Array 的警示</span><span class="sxs-lookup"><span data-stu-id="994ec-166">View and manage alerts for the StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-alerts.md) |
| <span data-ttu-id="994ec-167">修改裝置系統管理員密碼</span><span class="sxs-lookup"><span data-stu-id="994ec-167">Modify the device administrator password</span></span> |[<span data-ttu-id="994ec-168">變更 StorSimple Virtual Array 裝置系統管理員密碼</span><span class="sxs-lookup"><span data-stu-id="994ec-168">Change the StorSimple Virtual Array device administrator password</span></span>](storsimple-virtual-array-change-device-admin-password.md) |
| <span data-ttu-id="994ec-169">安裝軟體更新</span><span class="sxs-lookup"><span data-stu-id="994ec-169">Install software updates</span></span> |[<span data-ttu-id="994ec-170">更新您的 Virtual Array</span><span class="sxs-lookup"><span data-stu-id="994ec-170">Update your Virtual Array</span></span>](storsimple-virtual-array-install-update.md) |

> [!NOTE]
> <span data-ttu-id="994ec-171">您必須使用 [本機 Web UI](storsimple-ova-web-ui-admin.md) 以執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="994ec-171">You must use the [local web UI](storsimple-ova-web-ui-admin.md) for the following tasks:</span></span>
> 
> * [<span data-ttu-id="994ec-172">擷取服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="994ec-172">Retrieve the service data encryption key</span></span>](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key)
> * [<span data-ttu-id="994ec-173">建立支援封裝</span><span class="sxs-lookup"><span data-stu-id="994ec-173">Create a support package</span></span>](storsimple-ova-web-ui-admin.md#generate-a-log-package)
> * [<span data-ttu-id="994ec-174">停止和重新啟動 Virtual Array</span><span class="sxs-lookup"><span data-stu-id="994ec-174">Stop and restart a Virtual Array</span></span>](storsimple-ova-web-ui-admin.md#shut-down-and-restart-your-device)
> 
> 

## <a name="next-steps"></a><span data-ttu-id="994ec-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="994ec-175">Next steps</span></span>
<span data-ttu-id="994ec-176">如需 Web UI 及如何使用的詳細資訊，請移至 [使用 StorSimple Web UI 管理 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="994ec-176">For information about the web UI and how to use it, go to [Use the StorSimple web UI to administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

