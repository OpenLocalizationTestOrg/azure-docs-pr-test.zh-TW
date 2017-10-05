---
title: "StorSimple 8000 系列 Update 5 版本資訊 | Microsoft Docs"
description: "說明 StorSimple 8000 系列 Update 5 的新功能、問題及因應措施。"
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
ms.openlocfilehash: e68dce72d648171faab930bbb4af9fd61816b19b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="storsimple-8000-series-update-5-release-notes"></a><span data-ttu-id="10c38-103">StorSimple 8000 系列 Update 5 版本資訊</span><span class="sxs-lookup"><span data-stu-id="10c38-103">StorSimple 8000 Series Update 5 release notes</span></span>

## <a name="overview"></a><span data-ttu-id="10c38-104">概觀</span><span class="sxs-lookup"><span data-stu-id="10c38-104">Overview</span></span>

<span data-ttu-id="10c38-105">下列版本資訊說明 StorSimple 8000 系列 Update 5 的新功能，並識別未決的重要問題。</span><span class="sxs-lookup"><span data-stu-id="10c38-105">The following release notes describe the new features and identify the critical open issues for StorSimple 8000 Series Update 5.</span></span> <span data-ttu-id="10c38-106">當中也包含此版本中隨附之 StorSimple 軟體更新的清單。</span><span class="sxs-lookup"><span data-stu-id="10c38-106">They also contain a list of the StorSimple software updates included in this release.</span></span>

<span data-ttu-id="10c38-107">Update 5 可以套用至任何執行 Update 0.1 到 Update 4 的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="10c38-107">Update 5 can be applied to any StorSimple device running Update 0.1 through Update 4.</span></span> <span data-ttu-id="10c38-108">與 Update 5 關聯的裝置版本為 6.3.9600.17845。</span><span class="sxs-lookup"><span data-stu-id="10c38-108">The device version associated with Update 5 is 6.3.9600.17845.</span></span>

<span data-ttu-id="10c38-109">在 StorSimple 方案中部署更新之前，請檢閱版本資訊中所包含的資訊。</span><span class="sxs-lookup"><span data-stu-id="10c38-109">Review the information contained in the release notes before you deploy the update in your StorSimple solution.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="10c38-110">Update 5 有裝置軟體、磁碟韌體、作業系統安全性和其他作業系統更新。</span><span class="sxs-lookup"><span data-stu-id="10c38-110">Update 5 has device software, disk firmware, OS security, and other OS updates.</span></span> <span data-ttu-id="10c38-111">安裝此更新，大約需要花費 4 小時。</span><span class="sxs-lookup"><span data-stu-id="10c38-111">It takes approximately 4 hours to install this update.</span></span> <span data-ttu-id="10c38-112">磁碟韌體更新是干擾性更新，會導致您的裝置停機。</span><span class="sxs-lookup"><span data-stu-id="10c38-112">Disk firmware update is a disruptive update and results in a downtime for your device.</span></span> <span data-ttu-id="10c38-113">建議您套用 Update 5，讓您的裝置維持在最新狀態。</span><span class="sxs-lookup"><span data-stu-id="10c38-113">We recommend that you apply Update 5 to keep your device up-to-date.</span></span>
> * <span data-ttu-id="10c38-114">如果是新版本，您可能不會立即看到更新，因為我們會分階段推出更新。</span><span class="sxs-lookup"><span data-stu-id="10c38-114">For new releases, you may not see updates immediately because we do a phased rollout of the updates.</span></span> <span data-ttu-id="10c38-115">請等候數天然後再次掃描更新，因為很快就會提供這些更新。</span><span class="sxs-lookup"><span data-stu-id="10c38-115">Wait a few days, and then scan for updates again as these updates will become available soon.</span></span>

## <a name="whats-new-in-update-5"></a><span data-ttu-id="10c38-116">Update 5 的新功能</span><span class="sxs-lookup"><span data-stu-id="10c38-116">What's new in Update 5</span></span>

<span data-ttu-id="10c38-117">Update 5 包含以下重要的改良功能和錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="10c38-117">The following key improvements and bug fixes have been made in Update 5.</span></span>

* <span data-ttu-id="10c38-118">**使用 Azure Active Directory (AAD) 來向 StorSimple 裝置管理員服務驗證** – 從 Update 5 起，系統會使用 Azure Active Directory 來向 StorSimple 裝置管理員服務驗證。</span><span class="sxs-lookup"><span data-stu-id="10c38-118">**Use of Azure Active Directory (AAD) to authenticate with StorSimple Device Manager service** – From Update 5 onwards, Azure Active Directory is used to authenticate with the StorSimple Device Manager service.</span></span> <span data-ttu-id="10c38-119">舊的驗證機制會在 2017 年 12 月後淘汰。</span><span class="sxs-lookup"><span data-stu-id="10c38-119">The old authentication mechanism will be deprecated by December 2017.</span></span> <span data-ttu-id="10c38-120">所有使用者都必須在其防火牆規則中包含新的驗證 URL。</span><span class="sxs-lookup"><span data-stu-id="10c38-120">All the users must include the new authentication URLs in their firewall rules.</span></span> <span data-ttu-id="10c38-121">如需詳細資訊，請移至 [StorSimple 裝置網路需求中所列出的驗證 URL](storsimple-8000-system-requirements.md#url-patterns-for-azure-portal)。</span><span class="sxs-lookup"><span data-stu-id="10c38-121">For more information, go to [authentication URLs listed in the networking requirements for your StorSimple device](storsimple-8000-system-requirements.md#url-patterns-for-azure-portal).</span></span>

    <span data-ttu-id="10c38-122">如果未將驗證 URL 包含在防火牆規則內，使用者會看到重大警示，其內容指出他們的 StorSimple 裝置無法向服務驗證。</span><span class="sxs-lookup"><span data-stu-id="10c38-122">If the authentication URL is not included in the firewall rules, the users will see a critical alert that their StorSimple device could not authenticate with the service.</span></span> <span data-ttu-id="10c38-123">如果使用者看到此警示，就必須包含新的驗證 URL。</span><span class="sxs-lookup"><span data-stu-id="10c38-123">If the users see this alert, they need to include the new authentication URL.</span></span> <span data-ttu-id="10c38-124">如需詳細資訊，請移至 [StorSimple 網路警示](storsimple-8000-manage-alerts.md#networking-alerts)。</span><span class="sxs-lookup"><span data-stu-id="10c38-124">For more information, go to [StorSimple networking alerts](storsimple-8000-manage-alerts.md#networking-alerts).</span></span>

* <span data-ttu-id="10c38-125">**新的 StorSimple Snapshot Manager 版本** - Update 5 發行了新的 StorSimple Snapshot Manager 版本。</span><span class="sxs-lookup"><span data-stu-id="10c38-125">**New version of StorSimple Snapshot Manager** - A new version of StorSimple Snapshot Manager is released with Update 5.</span></span> <span data-ttu-id="10c38-126">我們建議您更新成這個版本。</span><span class="sxs-lookup"><span data-stu-id="10c38-126">We recommend that you update to this version.</span></span> <span data-ttu-id="10c38-127">這個版本可與所有執行 Update 3 或更新版本的 StorSimple 裝置相容。</span><span class="sxs-lookup"><span data-stu-id="10c38-127">This version is compatible with all the StorSimple devices that are running Update 3 or later.</span></span> <span data-ttu-id="10c38-128">如需詳細資訊，請移至[部署 StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="10c38-128">For more information, go to [deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span></span>


## <a name="issues-fixed-in-update-5"></a><span data-ttu-id="10c38-129">Update 5 中修正的問題</span><span class="sxs-lookup"><span data-stu-id="10c38-129">Issues fixed in Update 5</span></span>

<span data-ttu-id="10c38-130">下表提供 Update 5 中已修正之問題的摘要。</span><span class="sxs-lookup"><span data-stu-id="10c38-130">The following table provides a summary of issues that were fixed in Update 5.</span></span>

| <span data-ttu-id="10c38-131">否</span><span class="sxs-lookup"><span data-stu-id="10c38-131">No</span></span> | <span data-ttu-id="10c38-132">功能</span><span class="sxs-lookup"><span data-stu-id="10c38-132">Feature</span></span> | <span data-ttu-id="10c38-133">問題</span><span class="sxs-lookup"><span data-stu-id="10c38-133">Issue</span></span> | <span data-ttu-id="10c38-134">適用於實體裝置</span><span class="sxs-lookup"><span data-stu-id="10c38-134">Applies to physical device</span></span> | <span data-ttu-id="10c38-135">適用於虛擬裝置</span><span class="sxs-lookup"><span data-stu-id="10c38-135">Applies to virtual device</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="10c38-136">1</span><span class="sxs-lookup"><span data-stu-id="10c38-136">1</span></span> |<span data-ttu-id="10c38-137">Windows PowerShell 遠端處理</span><span class="sxs-lookup"><span data-stu-id="10c38-137">Windows PowerShell remoting</span></span> |<span data-ttu-id="10c38-138">在舊版中，使用者會在嘗試透過 Windows PowerShell 對 StorSimple 雲端設備建立遠端連線時收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="10c38-138">In the previous release, a user would receive an error while trying to establish a remote connection to the StorSimple Cloud Appliance via Windows PowerShell.</span></span> <span data-ttu-id="10c38-139">此版本已找出此問題的根本原因並加以修正。</span><span class="sxs-lookup"><span data-stu-id="10c38-139">This issue was root-caused and fixed in this release.</span></span> |<span data-ttu-id="10c38-140">否</span><span class="sxs-lookup"><span data-stu-id="10c38-140">No</span></span> |<span data-ttu-id="10c38-141">是</span><span class="sxs-lookup"><span data-stu-id="10c38-141">Yes</span></span> |
| <span data-ttu-id="10c38-142">2</span><span class="sxs-lookup"><span data-stu-id="10c38-142">2</span></span> |<span data-ttu-id="10c38-143">頻寬範本</span><span class="sxs-lookup"><span data-stu-id="10c38-143">Bandwidth templates</span></span> |<span data-ttu-id="10c38-144">舊版中的頻寬範本有問題，從而導致頻寬比裝置所設定的值還低。</span><span class="sxs-lookup"><span data-stu-id="10c38-144">In earlier release, there was an issue with bandwidth templates that resulted in lower bandwidth than what the device was configured for.</span></span> <span data-ttu-id="10c38-145">本版已經修正這個問題。</span><span class="sxs-lookup"><span data-stu-id="10c38-145">This issue is resolved in this release.</span></span> |<span data-ttu-id="10c38-146">是</span><span class="sxs-lookup"><span data-stu-id="10c38-146">Yes</span></span> |<span data-ttu-id="10c38-147">是</span><span class="sxs-lookup"><span data-stu-id="10c38-147">Yes</span></span> |
| <span data-ttu-id="10c38-148">3</span><span class="sxs-lookup"><span data-stu-id="10c38-148">3</span></span> |<span data-ttu-id="10c38-149">容錯移轉</span><span class="sxs-lookup"><span data-stu-id="10c38-149">Failover</span></span> |<span data-ttu-id="10c38-150">在舊版中，當擁有大量磁碟區的裝置容錯移轉至另一個執行 Update 4 的裝置時，該程序會在嘗試套用存取控制記錄時失敗。</span><span class="sxs-lookup"><span data-stu-id="10c38-150">In previous release, when a device with a large number of volumes was failed over to another device running Update 4, the process would fail when trying to apply the access control records.</span></span> <span data-ttu-id="10c38-151">此版本已經修正這個問題。</span><span class="sxs-lookup"><span data-stu-id="10c38-151">This issue is fixed in this release.</span></span> |<span data-ttu-id="10c38-152">是</span><span class="sxs-lookup"><span data-stu-id="10c38-152">Yes</span></span> |<span data-ttu-id="10c38-153">是</span><span class="sxs-lookup"><span data-stu-id="10c38-153">Yes</span></span> |



## <a name="known-issues-in-update-5-from-previous-releases"></a><span data-ttu-id="10c38-154">Update 5 中舊版的已知問題</span><span class="sxs-lookup"><span data-stu-id="10c38-154">Known issues in Update 5 from previous releases</span></span>

<span data-ttu-id="10c38-155">Update 5 中沒有新的已知問題。</span><span class="sxs-lookup"><span data-stu-id="10c38-155">There are no new known issues in Update 5.</span></span> <span data-ttu-id="10c38-156">如需 Update 5 中舊版遺留的問題清單，請移至 [Update 3 版本資訊](storsimple-update3-release-notes.md#known-issues-in-update-3)。</span><span class="sxs-lookup"><span data-stu-id="10c38-156">For a list of issues carried over to Update 5 from previous releases, go to [Update 3 release notes](storsimple-update3-release-notes.md#known-issues-in-update-3).</span></span>

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-5"></a><span data-ttu-id="10c38-157">Update 5 中的序列連結 SCSI (SAS) 控制器和韌體更新</span><span class="sxs-lookup"><span data-stu-id="10c38-157">Serial-attached SCSI (SAS) controller and firmware updates in Update 5</span></span>

<span data-ttu-id="10c38-158">此版本包含 SAS 控制器和 LSI 驅動程式與韌體的更新。</span><span class="sxs-lookup"><span data-stu-id="10c38-158">This release has SAS controller and LSI driver and firmware updates.</span></span> <span data-ttu-id="10c38-159">如需有關如何安裝這些更新的詳細資訊，請參閱[在 StorSimple 裝置上安裝 Update 5](storsimple-8000-install-update-5.md) 。</span><span class="sxs-lookup"><span data-stu-id="10c38-159">For more information on how to install these updates, see [install Update 5](storsimple-8000-install-update-5.md) on your StorSimple device.</span></span>

## <a name="storsimple-cloud-appliance-updates-in-update-5"></a><span data-ttu-id="10c38-160">Update 5 中的 StorSimple 雲端設備更新 | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="10c38-160">StorSimple Cloud Appliance updates in Update 5</span></span>

<span data-ttu-id="10c38-161">這項更新無法套用至 StorSimple Cloud Appliance (也稱為虛擬裝置)。</span><span class="sxs-lookup"><span data-stu-id="10c38-161">This update cannot be applied to the StorSimple Cloud Appliance (also known as the virtual device).</span></span> <span data-ttu-id="10c38-162">必須使用 Update 5 映像建立新的雲端設備。</span><span class="sxs-lookup"><span data-stu-id="10c38-162">New cloud appliances need to be created using the Update 5 image.</span></span> <span data-ttu-id="10c38-163">如需如何建立 StorSimple 雲端設備的資訊，請移至[部署和管理 StorSimple 雲端設備](storsimple-8000-cloud-appliance-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="10c38-163">For information on how to create a StorSimple Cloud Appliance, go to [Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="10c38-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="10c38-164">Next step</span></span>

<span data-ttu-id="10c38-165">了解如何[在 StorSimple 裝置上安裝 Update 5](storsimple-8000-install-update-5.md)。</span><span class="sxs-lookup"><span data-stu-id="10c38-165">Learn how to [install Update 5](storsimple-8000-install-update-5.md) on your StorSimple device.</span></span>

