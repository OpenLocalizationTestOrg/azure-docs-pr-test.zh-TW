---
title: "Azure StorSimple Manager 的虛擬陣列管理 aaaMicrosoft |Microsoft 文件"
description: "了解如何 toomanage StorSimple 內部部署虛擬陣列使用中的 hello StorSimple 裝置管理員服務 hello Azure 入口網站。"
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
ms.openlocfilehash: 1fabf9ca524b461266346a6cabf49aef772032ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooadminister-your-storsimple-virtual-array"></a><span data-ttu-id="44b39-103">使用您的 StorSimple Virtual Array hello StorSimple 裝置管理員服務 tooadminister</span><span class="sxs-lookup"><span data-stu-id="44b39-103">Use hello StorSimple Device Manager service tooadminister your StorSimple Virtual Array</span></span>
![安裝程序流程](./media/storsimple-virtual-array-manager-service-administration/manage4.png)

## <a name="overview"></a><span data-ttu-id="44b39-105">概觀</span><span class="sxs-lookup"><span data-stu-id="44b39-105">Overview</span></span>
<span data-ttu-id="44b39-106">本文說明 hello StorSimple 裝置管理員服務介面，包括如何透過此 UI 執行 tooconnect tooit 和 hello 各種選項，並提供連結 toohello 特定工作流程。</span><span class="sxs-lookup"><span data-stu-id="44b39-106">This article describes hello StorSimple Device Manager service interface, including how tooconnect tooit and hello various options available, and provides links toohello specific workflows that can be performed via this UI.</span></span>

<span data-ttu-id="44b39-107">閱讀本文之後，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="44b39-107">After reading this article, you will know how to:</span></span>

* <span data-ttu-id="44b39-108">連接 toohello StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="44b39-108">Connect toohello StorSimple Device Manager service</span></span>
* <span data-ttu-id="44b39-109">瀏覽 hello StorSimple 裝置管理員 UI</span><span class="sxs-lookup"><span data-stu-id="44b39-109">Navigate hello StorSimple Device Manager UI</span></span>
* <span data-ttu-id="44b39-110">管理您的 StorSimple Virtual Array 透過 hello StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="44b39-110">Administer your StorSimple Virtual Array via hello StorSimple Device Manager service</span></span>

> [!NOTE]
> <span data-ttu-id="44b39-111">tooview hello 管理選項可供 hello StorSimple 8000 系列裝置，跳過[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="44b39-111">tooview hello management options available for hello StorSimple 8000 series device, go too[Use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>
> 
> 

## <a name="connect-toohello-storsimple-device-manager-service"></a><span data-ttu-id="44b39-112">連接 toohello StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="44b39-112">Connect toohello StorSimple Device Manager service</span></span>
<span data-ttu-id="44b39-113">hello StorSimple 裝置管理員服務在 Microsoft Azure 中執行，並連接 toomultiple StorSimple 虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="44b39-113">hello StorSimple Device Manager service runs in Microsoft Azure and connects toomultiple StorSimple Virtual Arrays.</span></span> <span data-ttu-id="44b39-114">您使用管理中心的 Microsoft Azure 入口網站，在瀏覽器 toomanage 執行這些裝置。</span><span class="sxs-lookup"><span data-stu-id="44b39-114">You use a central Microsoft Azure portal running in a browser toomanage these devices.</span></span> <span data-ttu-id="44b39-115">tooconnect toohello StorSimple 裝置管理員服務，請勿 hello 遵循。</span><span class="sxs-lookup"><span data-stu-id="44b39-115">tooconnect toohello StorSimple Device Manager service, do hello following.</span></span>

#### <a name="tooconnect-toohello-service"></a><span data-ttu-id="44b39-116">tooconnect toohello 服務</span><span class="sxs-lookup"><span data-stu-id="44b39-116">tooconnect toohello service</span></span>
1. <span data-ttu-id="44b39-117">跳過[https://ms.portal.azure.com](https://ms.portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="44b39-117">Go too[https://ms.portal.azure.com](https://ms.portal.azure.com).</span></span>
2. <span data-ttu-id="44b39-118">使用您的 Microsoft 帳戶認證，登入 toohello Microsoft Azure 入口網站 （位於 hello 的右上方 hello 窗格）。</span><span class="sxs-lookup"><span data-stu-id="44b39-118">Using your Microsoft account credentials, log on toohello Microsoft Azure portal (located at hello top-right of hello pane).</span></span>
3. <span data-ttu-id="44b39-119">瀏覽 tooBrowse--> 'Filter' StorSimple 裝置管理員 tooview 上指定的訂用帳戶中的所有您裝置管理員。</span><span class="sxs-lookup"><span data-stu-id="44b39-119">Navigate tooBrowse --> 'Filter' on StorSimple Device Managers tooview all your device managers in a given subscription.</span></span>

## <a name="use-hello-storsimple-device-manager-service-tooperform-management-tasks"></a><span data-ttu-id="44b39-120">使用 hello StorSimple 裝置管理員服務 tooperform 管理工作</span><span class="sxs-lookup"><span data-stu-id="44b39-120">Use hello StorSimple Device Manager service tooperform management tasks</span></span>
<span data-ttu-id="44b39-121">hello 下表顯示之所有 hello 常見管理工作和複雜工作流程可以在 hello StorSimple 裝置管理員服務摘要 刀鋒視窗中執行的摘要。</span><span class="sxs-lookup"><span data-stu-id="44b39-121">hello following table shows a summary of all hello common management tasks and complex workflows that can be performed within hello StorSimple Device Manager service summary blade.</span></span> <span data-ttu-id="44b39-122">這些工作被組織根據 hello 刀鋒視窗啟動它們。</span><span class="sxs-lookup"><span data-stu-id="44b39-122">These tasks are organized based on hello blades on which they are initiated.</span></span>

<span data-ttu-id="44b39-123">如需有關每個工作流程的詳細資訊，請按一下 hello hello 資料表中的適當程序。</span><span class="sxs-lookup"><span data-stu-id="44b39-123">For more information about each workflow, click hello appropriate procedure in hello table.</span></span>

#### <a name="storsimple-device-manager-workflows"></a><span data-ttu-id="44b39-124">StorSimple 裝置管理員工作流程</span><span class="sxs-lookup"><span data-stu-id="44b39-124">StorSimple Device Manager workflows</span></span>
| <span data-ttu-id="44b39-125">如果您希望 toodo 如此...</span><span class="sxs-lookup"><span data-stu-id="44b39-125">If you want toodo this ...</span></span> | <span data-ttu-id="44b39-126">使用此程序</span><span class="sxs-lookup"><span data-stu-id="44b39-126">Use this procedure</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44b39-127">建立服務</span><span class="sxs-lookup"><span data-stu-id="44b39-127">Create a service</span></span></br><span data-ttu-id="44b39-128">刪除服務</span><span class="sxs-lookup"><span data-stu-id="44b39-128">Delete a service</span></span></br><span data-ttu-id="44b39-129">取得 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="44b39-129">Get hello service registration key</span></span></br><span data-ttu-id="44b39-130">重新產生 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="44b39-130">Regenerate hello service registration key</span></span> |[<span data-ttu-id="44b39-131">部署 hello StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="44b39-131">Deploy hello StorSimple Device Manager service</span></span>](storsimple-virtual-array-manage-service.md) |
| <span data-ttu-id="44b39-132">檢視 hello 活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="44b39-132">View hello activity logs</span></span> |[<span data-ttu-id="44b39-133">使用摘要的 hello StorSimple 服務</span><span class="sxs-lookup"><span data-stu-id="44b39-133">Use hello StorSimple service summary</span></span>](storsimple-virtual-array-service-summary.md) |
| <span data-ttu-id="44b39-134">停用 Virtual Array</span><span class="sxs-lookup"><span data-stu-id="44b39-134">Deactivate a Virtual Array</span></span></br><span data-ttu-id="44b39-135">刪除 Virtual Array</span><span class="sxs-lookup"><span data-stu-id="44b39-135">Delete a Virtual Array</span></span> |[<span data-ttu-id="44b39-136">停用或刪除虛擬陣列</span><span class="sxs-lookup"><span data-stu-id="44b39-136">Deactivate or delete a virtual array</span></span>](storsimple-virtual-array-deactivate-and-delete-device.md) |
| <span data-ttu-id="44b39-137">災害復原和裝置容錯移轉</span><span class="sxs-lookup"><span data-stu-id="44b39-137">Disaster recovery and device failover</span></span></br><span data-ttu-id="44b39-138">容錯移轉必要條件</span><span class="sxs-lookup"><span data-stu-id="44b39-138">Failover prerequisites</span></span></br><span data-ttu-id="44b39-139">業務持續性災害復原 (BCDR)</span><span class="sxs-lookup"><span data-stu-id="44b39-139">Business continuity disaster recovery (BCDR)</span></span></br><span data-ttu-id="44b39-140">災害復原時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="44b39-140">Errors during disaster recovery</span></span> |[<span data-ttu-id="44b39-141">StorSimple Virtual Array 的災害復原和裝置容錯移轉</span><span class="sxs-lookup"><span data-stu-id="44b39-141">Disaster recovery and device failover for your StorSimple Virtual Array</span></span>](storsimple-virtual-array-failover-dr.md) |
| <span data-ttu-id="44b39-142">備份共用和磁碟區</span><span class="sxs-lookup"><span data-stu-id="44b39-142">Back up shares and volumes</span></span></br><span data-ttu-id="44b39-143">進行手動備份</span><span class="sxs-lookup"><span data-stu-id="44b39-143">Take a manual backup</span></span></br><span data-ttu-id="44b39-144">變更 hello 備份排程</span><span class="sxs-lookup"><span data-stu-id="44b39-144">Change hello backup schedule</span></span></br><span data-ttu-id="44b39-145">檢視現有的備份</span><span class="sxs-lookup"><span data-stu-id="44b39-145">View existing backups</span></span> |[<span data-ttu-id="44b39-146">備份 StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="44b39-146">Back up your StorSimple Virtual Array</span></span>](storsimple-virtual-array-backup.md) |
| <span data-ttu-id="44b39-147">從備份組複製共用</span><span class="sxs-lookup"><span data-stu-id="44b39-147">Clone shares from a backup set</span></span></br><span data-ttu-id="44b39-148">從備份組複製磁碟區</span><span class="sxs-lookup"><span data-stu-id="44b39-148">Clone volumes from a backup set</span></span></br><span data-ttu-id="44b39-149">項目層級復原 (僅限檔案伺服器)</span><span class="sxs-lookup"><span data-stu-id="44b39-149">Item-level recovery (file server only)</span></span> |[<span data-ttu-id="44b39-150">從 StorSimple Virtual Array 的備份複製</span><span class="sxs-lookup"><span data-stu-id="44b39-150">Clone from a backup of your StorSimple Virtual Array</span></span>](storsimple-virtual-array-clone.md) |
| <span data-ttu-id="44b39-151">有關儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="44b39-151">About  storage accounts</span></span></br><span data-ttu-id="44b39-152">新增儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="44b39-152">Add a storage account</span></span></br><span data-ttu-id="44b39-153">編輯儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="44b39-153">Edit a storage account</span></span></br><span data-ttu-id="44b39-154">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="44b39-154">Delete a storage account</span></span> |[<span data-ttu-id="44b39-155">管理 StorSimple Virtual Array hello 的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="44b39-155">Manage storage accounts for hello StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-storage-accounts.md) |
| <span data-ttu-id="44b39-156">關於存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="44b39-156">About access control records</span></span></br><span data-ttu-id="44b39-157">加入或修改存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="44b39-157">Add or modify an access control record</span></span> </br><span data-ttu-id="44b39-158">刪除存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="44b39-158">Delete an access control record</span></span> |[<span data-ttu-id="44b39-159">管理 StorSimple Virtual Array hello 的存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="44b39-159">Manage access control records for hello StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-acrs.md) |
| <span data-ttu-id="44b39-160">檢視工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="44b39-160">View job details</span></span> |[<span data-ttu-id="44b39-161">管理 StorSimple Virtual Array 作業</span><span class="sxs-lookup"><span data-stu-id="44b39-161">Manage StorSimple Virtual Array jobs</span></span>](storsimple-virtual-array-manage-jobs.md) |
| <span data-ttu-id="44b39-162">設定警示設定</span><span class="sxs-lookup"><span data-stu-id="44b39-162">Configure alert settings</span></span></br><span data-ttu-id="44b39-163">接收警示通知</span><span class="sxs-lookup"><span data-stu-id="44b39-163">Receive alert notifications</span></span></br><span data-ttu-id="44b39-164">管理警示</span><span class="sxs-lookup"><span data-stu-id="44b39-164">Manage alerts</span></span></br><span data-ttu-id="44b39-165">檢閱警示</span><span class="sxs-lookup"><span data-stu-id="44b39-165">Review alerts</span></span> |[<span data-ttu-id="44b39-166">檢視及管理警示的 hello StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="44b39-166">View and manage alerts for hello StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-alerts.md) |
| <span data-ttu-id="44b39-167">修改 hello 裝置系統管理員密碼</span><span class="sxs-lookup"><span data-stu-id="44b39-167">Modify hello device administrator password</span></span> |[<span data-ttu-id="44b39-168">變更 hello StorSimple Virtual Array 裝置系統管理員密碼</span><span class="sxs-lookup"><span data-stu-id="44b39-168">Change hello StorSimple Virtual Array device administrator password</span></span>](storsimple-virtual-array-change-device-admin-password.md) |
| <span data-ttu-id="44b39-169">安裝軟體更新</span><span class="sxs-lookup"><span data-stu-id="44b39-169">Install software updates</span></span> |[<span data-ttu-id="44b39-170">更新您的 Virtual Array</span><span class="sxs-lookup"><span data-stu-id="44b39-170">Update your Virtual Array</span></span>](storsimple-virtual-array-install-update.md) |

> [!NOTE]
> <span data-ttu-id="44b39-171">您必須使用 hello[本機 web UI](storsimple-ova-web-ui-admin.md) hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="44b39-171">You must use hello [local web UI](storsimple-ova-web-ui-admin.md) for hello following tasks:</span></span>
> 
> * [<span data-ttu-id="44b39-172">擷取 hello 服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="44b39-172">Retrieve hello service data encryption key</span></span>](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key)
> * [<span data-ttu-id="44b39-173">建立支援封裝</span><span class="sxs-lookup"><span data-stu-id="44b39-173">Create a support package</span></span>](storsimple-ova-web-ui-admin.md#generate-a-log-package)
> * [<span data-ttu-id="44b39-174">停止和重新啟動 Virtual Array</span><span class="sxs-lookup"><span data-stu-id="44b39-174">Stop and restart a Virtual Array</span></span>](storsimple-ova-web-ui-admin.md#shut-down-and-restart-your-device)
> 
> 

## <a name="next-steps"></a><span data-ttu-id="44b39-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="44b39-175">Next steps</span></span>
<span data-ttu-id="44b39-176">如需 hello web UI 以及如何 toouse，跳過[使用 hello StorSimple web UI tooadminister 您 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="44b39-176">For information about hello web UI and how toouse it, go too[Use hello StorSimple web UI tooadminister your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

