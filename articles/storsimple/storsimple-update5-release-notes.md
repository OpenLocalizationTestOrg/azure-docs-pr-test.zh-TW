---
title: "aaaStorSimple 8000 系列 Update 5 版本資訊 |Microsoft 文件"
description: "StorSimple 8000 系列 Update 5 描述 hello 新功能、 問題和因應措施。"
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
ms.date: 08/23/2017
ms.author: alkohli
ms.openlocfilehash: 9eb8ffb97b41ce3d4f1ffdf2975f904d0a2958e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-5-release-notes"></a><span data-ttu-id="23104-103">StorSimple 8000 系列 Update 5 版本資訊</span><span class="sxs-lookup"><span data-stu-id="23104-103">StorSimple 8000 Series Update 5 release notes</span></span>

## <a name="overview"></a><span data-ttu-id="23104-104">概觀</span><span class="sxs-lookup"><span data-stu-id="23104-104">Overview</span></span>

<span data-ttu-id="23104-105">hello 下列版本資訊說明 hello 新功能和識別 hello 重大議題 StorSimple 8000 系列 Update 5。</span><span class="sxs-lookup"><span data-stu-id="23104-105">hello following release notes describe hello new features and identify hello critical open issues for StorSimple 8000 Series Update 5.</span></span> <span data-ttu-id="23104-106">也會包含在此版本中所包含的 hello StorSimple 軟體更新清單。</span><span class="sxs-lookup"><span data-stu-id="23104-106">They also contain a list of hello StorSimple software updates included in this release.</span></span>

<span data-ttu-id="23104-107">Update 5 可以透過更新 4 中執行 Update 0.1 套用的 tooany StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="23104-107">Update 5 can be applied tooany StorSimple device running Update 0.1 through Update 4.</span></span> <span data-ttu-id="23104-108">更新 5 與相關聯的 hello 裝置版本是 6.3.9600.17845。</span><span class="sxs-lookup"><span data-stu-id="23104-108">hello device version associated with Update 5 is 6.3.9600.17845.</span></span>

<span data-ttu-id="23104-109">檢閱附註，然後再部署 hello 更新您的 StorSimple 解決方案中的 hello 版本中所包含的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="23104-109">Review hello information contained in hello release notes before you deploy hello update in your StorSimple solution.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="23104-110">Update 5 有裝置軟體、磁碟韌體、作業系統安全性和其他作業系統更新。</span><span class="sxs-lookup"><span data-stu-id="23104-110">Update 5 has device software, disk firmware, OS security, and other OS updates.</span></span> <span data-ttu-id="23104-111">它會採用大約 4 小時 tooinstall 這項更新。</span><span class="sxs-lookup"><span data-stu-id="23104-111">It takes approximately 4 hours tooinstall this update.</span></span> <span data-ttu-id="23104-112">磁碟韌體更新是干擾性更新，會導致您的裝置停機。</span><span class="sxs-lookup"><span data-stu-id="23104-112">Disk firmware update is a disruptive update and results in a downtime for your device.</span></span> <span data-ttu-id="23104-113">我們建議您套用更新 5 tookeep 您最新的裝置。</span><span class="sxs-lookup"><span data-stu-id="23104-113">We recommend that you apply Update 5 tookeep your device up-to-date.</span></span>
> * <span data-ttu-id="23104-114">新的版本，您可能不會看到更新立即，因為我們會執行 hello 更新分階段導入。</span><span class="sxs-lookup"><span data-stu-id="23104-114">For new releases, you may not see updates immediately because we do a phased rollout of hello updates.</span></span> <span data-ttu-id="23104-115">請等候數天然後再次掃描更新，因為很快就會提供這些更新。</span><span class="sxs-lookup"><span data-stu-id="23104-115">Wait a few days, and then scan for updates again as these updates will become available soon.</span></span>

## <a name="whats-new-in-update-5"></a><span data-ttu-id="23104-116">Update 5 的新功能</span><span class="sxs-lookup"><span data-stu-id="23104-116">What's new in Update 5</span></span>

<span data-ttu-id="23104-117">hello 下列索引鍵的改進和 bug 修正已進行更新 5 中。</span><span class="sxs-lookup"><span data-stu-id="23104-117">hello following key improvements and bug fixes have been made in Update 5.</span></span>

* <span data-ttu-id="23104-118">**使用具有 StorSimple 裝置管理員服務的 Azure Active Directory (AAD) tooauthenticate** – 從更新 5 及更新版本，Azure Active Directory 是一種使用的 tooauthenticate 與 hello StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="23104-118">**Use of Azure Active Directory (AAD) tooauthenticate with StorSimple Device Manager service** – From Update 5 onwards, Azure Active Directory is used tooauthenticate with hello StorSimple Device Manager service.</span></span> <span data-ttu-id="23104-119">將取代 2017 年 12 月 hello 舊的驗證機制。</span><span class="sxs-lookup"><span data-stu-id="23104-119">hello old authentication mechanism will be deprecated by December 2017.</span></span> <span data-ttu-id="23104-120">Hello 的所有使用者都必須都包含在其防火牆規則的 hello 新驗證 Url。</span><span class="sxs-lookup"><span data-stu-id="23104-120">All hello users must include hello new authentication URLs in their firewall rules.</span></span> <span data-ttu-id="23104-121">如需詳細資訊，請移至太[驗證 Url 列在 StorSimple 裝置的網路需求的 hello](storsimple-8000-system-requirements.md#url-patterns-for-azure-portal)。</span><span class="sxs-lookup"><span data-stu-id="23104-121">For more information, go too[authentication URLs listed in hello networking requirements for your StorSimple device](storsimple-8000-system-requirements.md#url-patterns-for-azure-portal).</span></span>

    <span data-ttu-id="23104-122">如果 hello 驗證 URL 未包含在 hello 的防火牆規則，hello 使用者會看到他們的 StorSimple 裝置無法與 hello 服務驗證重大警示。</span><span class="sxs-lookup"><span data-stu-id="23104-122">If hello authentication URL is not included in hello firewall rules, hello users will see a critical alert that their StorSimple device could not authenticate with hello service.</span></span> <span data-ttu-id="23104-123">如果 hello 使用者看到此警示，它們需要 tooinclude hello 新驗證 URL。</span><span class="sxs-lookup"><span data-stu-id="23104-123">If hello users see this alert, they need tooinclude hello new authentication URL.</span></span> <span data-ttu-id="23104-124">如需詳細資訊，請移至太[StorSimple 網路警示](storsimple-8000-manage-alerts.md#networking-alerts)。</span><span class="sxs-lookup"><span data-stu-id="23104-124">For more information, go too[StorSimple networking alerts](storsimple-8000-manage-alerts.md#networking-alerts).</span></span>

* <span data-ttu-id="23104-125">**新的 StorSimple Snapshot Manager 版本** - Update 5 發行了新的 StorSimple Snapshot Manager 版本。</span><span class="sxs-lookup"><span data-stu-id="23104-125">**New version of StorSimple Snapshot Manager** - A new version of StorSimple Snapshot Manager is released with Update 5.</span></span> <span data-ttu-id="23104-126">我們建議您更新 toothis 版本。</span><span class="sxs-lookup"><span data-stu-id="23104-126">We recommend that you update toothis version.</span></span> <span data-ttu-id="23104-127">這個版本是相容的所有 hello StorSimple 裝置，會執行 Update 3 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="23104-127">This version is compatible with all hello StorSimple devices that are running Update 3 or later.</span></span> <span data-ttu-id="23104-128">如需詳細資訊，請移至太[部署 StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="23104-128">For more information, go too[deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span></span>


## <a name="issues-fixed-in-update-5"></a><span data-ttu-id="23104-129">Update 5 中修正的問題</span><span class="sxs-lookup"><span data-stu-id="23104-129">Issues fixed in Update 5</span></span>

<span data-ttu-id="23104-130">hello 下表提供更新 5 中已修正的問題的摘要。</span><span class="sxs-lookup"><span data-stu-id="23104-130">hello following table provides a summary of issues that were fixed in Update 5.</span></span>

| <span data-ttu-id="23104-131">否</span><span class="sxs-lookup"><span data-stu-id="23104-131">No</span></span> | <span data-ttu-id="23104-132">功能</span><span class="sxs-lookup"><span data-stu-id="23104-132">Feature</span></span> | <span data-ttu-id="23104-133">問題</span><span class="sxs-lookup"><span data-stu-id="23104-133">Issue</span></span> | <span data-ttu-id="23104-134">適用於 toophysical 裝置</span><span class="sxs-lookup"><span data-stu-id="23104-134">Applies toophysical device</span></span> | <span data-ttu-id="23104-135">適用於 toovirtual 裝置</span><span class="sxs-lookup"><span data-stu-id="23104-135">Applies toovirtual device</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="23104-136">1</span><span class="sxs-lookup"><span data-stu-id="23104-136">1</span></span> |<span data-ttu-id="23104-137">Windows PowerShell 遠端處理</span><span class="sxs-lookup"><span data-stu-id="23104-137">Windows PowerShell remoting</span></span> |<span data-ttu-id="23104-138">在 hello 先前版本中，使用者會收到錯誤，在嘗試 tooestablish 遠端連線 toohello StorSimple 雲端應用裝置，透過 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="23104-138">In hello previous release, a user would receive an error while trying tooestablish a remote connection toohello StorSimple Cloud Appliance via Windows PowerShell.</span></span> <span data-ttu-id="23104-139">此版本已找出此問題的根本原因並加以修正。</span><span class="sxs-lookup"><span data-stu-id="23104-139">This issue was root-caused and fixed in this release.</span></span> |<span data-ttu-id="23104-140">否</span><span class="sxs-lookup"><span data-stu-id="23104-140">No</span></span> |<span data-ttu-id="23104-141">是</span><span class="sxs-lookup"><span data-stu-id="23104-141">Yes</span></span> |
| <span data-ttu-id="23104-142">2</span><span class="sxs-lookup"><span data-stu-id="23104-142">2</span></span> |<span data-ttu-id="23104-143">頻寬範本</span><span class="sxs-lookup"><span data-stu-id="23104-143">Bandwidth templates</span></span> |<span data-ttu-id="23104-144">在較早版本中，發生問題導致比哪些 hello 裝置已設定為低頻寬的頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="23104-144">In earlier release, there was an issue with bandwidth templates that resulted in lower bandwidth than what hello device was configured for.</span></span> <span data-ttu-id="23104-145">本版已經修正這個問題。</span><span class="sxs-lookup"><span data-stu-id="23104-145">This issue is resolved in this release.</span></span> |<span data-ttu-id="23104-146">是</span><span class="sxs-lookup"><span data-stu-id="23104-146">Yes</span></span> |<span data-ttu-id="23104-147">是</span><span class="sxs-lookup"><span data-stu-id="23104-147">Yes</span></span> |
| <span data-ttu-id="23104-148">3</span><span class="sxs-lookup"><span data-stu-id="23104-148">3</span></span> |<span data-ttu-id="23104-149">容錯移轉</span><span class="sxs-lookup"><span data-stu-id="23104-149">Failover</span></span> |<span data-ttu-id="23104-150">在先前版本中，具有大量的磁碟區的裝置已容錯移轉執行 Update 4 tooanother 裝置時 hello 程序都會失敗時嘗試 tooapply hello 存取控制記錄。</span><span class="sxs-lookup"><span data-stu-id="23104-150">In previous release, when a device with a large number of volumes was failed over tooanother device running Update 4, hello process would fail when trying tooapply hello access control records.</span></span> <span data-ttu-id="23104-151">此版本已經修正這個問題。</span><span class="sxs-lookup"><span data-stu-id="23104-151">This issue is fixed in this release.</span></span> |<span data-ttu-id="23104-152">是</span><span class="sxs-lookup"><span data-stu-id="23104-152">Yes</span></span> |<span data-ttu-id="23104-153">是</span><span class="sxs-lookup"><span data-stu-id="23104-153">Yes</span></span> |



## <a name="known-issues-in-update-5-from-previous-releases"></a><span data-ttu-id="23104-154">Update 5 中舊版的已知問題</span><span class="sxs-lookup"><span data-stu-id="23104-154">Known issues in Update 5 from previous releases</span></span>

<span data-ttu-id="23104-155">Update 5 中沒有新的已知問題。</span><span class="sxs-lookup"><span data-stu-id="23104-155">There are no new known issues in Update 5.</span></span> <span data-ttu-id="23104-156">如轉 tooUpdate 5 舊版問題的清單，請移至太[Update 3 版本資訊](storsimple-update3-release-notes.md#known-issues-in-update-3)。</span><span class="sxs-lookup"><span data-stu-id="23104-156">For a list of issues carried over tooUpdate 5 from previous releases, go too[Update 3 release notes](storsimple-update3-release-notes.md#known-issues-in-update-3).</span></span>

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-5"></a><span data-ttu-id="23104-157">Update 5 中的序列連結 SCSI (SAS) 控制器和韌體更新</span><span class="sxs-lookup"><span data-stu-id="23104-157">Serial-attached SCSI (SAS) controller and firmware updates in Update 5</span></span>

<span data-ttu-id="23104-158">此版本包含 SAS 控制器和 LSI 驅動程式與韌體的更新。</span><span class="sxs-lookup"><span data-stu-id="23104-158">This release has SAS controller and LSI driver and firmware updates.</span></span> <span data-ttu-id="23104-159">如需有關如何 tooinstall 這些更新，請參閱[安裝更新 5](storsimple-8000-install-update-5.md) StorSimple 裝置上。</span><span class="sxs-lookup"><span data-stu-id="23104-159">For more information on how tooinstall these updates, see [install Update 5](storsimple-8000-install-update-5.md) on your StorSimple device.</span></span>

## <a name="storsimple-cloud-appliance-updates-in-update-5"></a><span data-ttu-id="23104-160">Update 5 中的 StorSimple 雲端設備更新 | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="23104-160">StorSimple Cloud Appliance updates in Update 5</span></span>

<span data-ttu-id="23104-161">此更新不能套用的 toohello StorSimple 雲端應用裝置 （也稱為 hello 虛擬裝置）。</span><span class="sxs-lookup"><span data-stu-id="23104-161">This update cannot be applied toohello StorSimple Cloud Appliance (also known as hello virtual device).</span></span> <span data-ttu-id="23104-162">新的雲端應用裝置需要 toobe 使用 hello 更新 5 映像建立。</span><span class="sxs-lookup"><span data-stu-id="23104-162">New cloud appliances need toobe created using hello Update 5 image.</span></span> <span data-ttu-id="23104-163">如需詳細資訊 toocreate StorSimple 雲端應用裝置中，跳過[部署和管理 StorSimple 雲端應用裝置](storsimple-8000-cloud-appliance-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="23104-163">For information on how toocreate a StorSimple Cloud Appliance, go too[Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="23104-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="23104-164">Next step</span></span>

<span data-ttu-id="23104-165">了解如何太[安裝更新 5](storsimple-8000-install-update-5.md) StorSimple 裝置上。</span><span class="sxs-lookup"><span data-stu-id="23104-165">Learn how too[install Update 5](storsimple-8000-install-update-5.md) on your StorSimple device.</span></span>

