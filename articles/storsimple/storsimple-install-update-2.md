---
title: "在 StorSimple 裝置上安裝 Update 2 | Microsoft Docs"
description: "說明如何在您的 StorSimple 8000 系列裝置上安裝 StorSimple 8000 系列 Update 2。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8c8981df-75d9-4d19-b137-d6c6ba39dcfb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: e788439608b7122f2bca6b99b832baa5258e472d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-2-on-your-storsimple-device"></a><span data-ttu-id="1451f-103">在 StorSimple 裝置上安裝 Update 2</span><span class="sxs-lookup"><span data-stu-id="1451f-103">Install Update 2 on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="1451f-104">Overview</span><span class="sxs-lookup"><span data-stu-id="1451f-104">Overview</span></span>
<span data-ttu-id="1451f-105">本教學課程說明如何透過 Azure 傳統入口網站，在執行舊版軟體的 StorSimple 裝置上安裝 Update 2。</span><span class="sxs-lookup"><span data-stu-id="1451f-105">This tutorial explains how to install Update 2 on a StorSimple device running an earlier software version via the Azure classic portal.</span></span> <span data-ttu-id="1451f-106">本教學課程也涵蓋了當閘道器設定於 StorSimple 裝置之 DATA 0 以外的網路介面上，而您嘗試從 Update 1 以前的軟體版本更新時所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="1451f-106">The tutorial also covers the steps required for the update when a gateway is configured on a network interface other than DATA 0 of the StorSimple device and you are trying to update from a pre-Update 1 software version.</span></span>

<span data-ttu-id="1451f-107">Update 2 包括裝置軟體更新、LSI 驅動程式更新和磁碟韌體更新。</span><span class="sxs-lookup"><span data-stu-id="1451f-107">Update 2 includes device software updates, LSI driver updates, and disk firmware updates.</span></span> <span data-ttu-id="1451f-108">此裝置軟體和 LSI 更新為非干擾性更新，且可透過 Azure 傳統入口網站套用。</span><span class="sxs-lookup"><span data-stu-id="1451f-108">The device software and LSI updates are non-disruptive updates and can be applied via the Azure classic portal.</span></span> <span data-ttu-id="1451f-109">磁碟韌體更新為干擾性更新，且只能透過裝置的 Windows PowerShell 介面套用。</span><span class="sxs-lookup"><span data-stu-id="1451f-109">The disk firmware updates are disruptive updates and can only be applied via the Windows PowerShell interface of the device.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="1451f-110">您可能不會立即看到 Update 2，因為我們會分階段推出更新。</span><span class="sxs-lookup"><span data-stu-id="1451f-110">You may not see Update 2 immediately because we do a phased rollout of the updates.</span></span> <span data-ttu-id="1451f-111">請在數天內再次掃描更新，因為很快就會提供 Update。</span><span class="sxs-lookup"><span data-stu-id="1451f-111">Scan for updates in a few days again as this Update will become available soon.</span></span>
> * <span data-ttu-id="1451f-112">安裝前會執行一組手動和自動預先檢查，以根據硬體狀態和網路連線來判斷裝置健全狀況。</span><span class="sxs-lookup"><span data-stu-id="1451f-112">A set of manual and automatic pre-checks are done prior to the install to determine the device health in terms of hardware state and network connectivity.</span></span> <span data-ttu-id="1451f-113">這些預先檢查只會在您從 Azure 傳統入口網站套用更新時執行。</span><span class="sxs-lookup"><span data-stu-id="1451f-113">These pre-checks are performed only if you apply the updates from the Azure classic portal.</span></span>
> * <span data-ttu-id="1451f-114">建議您透過 Azure 傳統入口網站安裝軟體和驅動程式更新。</span><span class="sxs-lookup"><span data-stu-id="1451f-114">We recommend that you install the software and driver updates via the Azure  classic portal.</span></span> <span data-ttu-id="1451f-115">如果入口網站中的更新前閘道器檢查失敗，請移至裝置的 Windows PowerShell 介面安裝更新 (勿透過其他方式)。</span><span class="sxs-lookup"><span data-stu-id="1451f-115">You should only go to the Windows PowerShell interface of the device (to install updates) if the pre-update gateway check fails in the portal.</span></span> <span data-ttu-id="1451f-116">更新可能需要 4-7 小時才能安裝 (包括 Windows Updates)。</span><span class="sxs-lookup"><span data-stu-id="1451f-116">The updates may take 4-7 hours to install (including the Windows Updates).</span></span> <span data-ttu-id="1451f-117">維護模式更新必須透過裝置的 Windows PowerShell 介面安裝。</span><span class="sxs-lookup"><span data-stu-id="1451f-117">The maintenance mode updates must be installed via the Windows PowerShell interface of the device.</span></span> <span data-ttu-id="1451f-118">由於維護模式更新是干擾性更新，它們將會導致裝置的停機時間。</span><span class="sxs-lookup"><span data-stu-id="1451f-118">As maintenance mode updates are disruptive updates, these will result in a down time for your device.</span></span>
> * <span data-ttu-id="1451f-119">如果執行選擇性的 StorSimple Snapshot Manager，更新裝置之前，請先將您的 Snapshot Manager 版本升級至 Update 2。</span><span class="sxs-lookup"><span data-stu-id="1451f-119">If running the optional StorSimple Snapshot Manager, ensure that you have upgraded your Snapshot Manager version to Update 2 prior to updating the device.</span></span>
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-2-via-the-azure-classic-portal"></a><span data-ttu-id="1451f-120">透過 Azure 傳統入口網站安裝 Update 2</span><span class="sxs-lookup"><span data-stu-id="1451f-120">Install Update 2 via the Azure classic portal</span></span>
<span data-ttu-id="1451f-121">請執行下列步驟，以將您的裝置更新至 [Update 2](storsimple-update2-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="1451f-121">Perform the following steps to update your device to [Update 2](storsimple-update2-release-notes.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1451f-122">Update 2 讓 Microsoft 從裝置提取其他診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="1451f-122">Update 2 enables Microsoft to pull additional diagnostic information from the device.</span></span> <span data-ttu-id="1451f-123">因此，當我們的作業小組識別有問題的裝置時，我們更有能力從裝置收集資訊並診斷問題。</span><span class="sxs-lookup"><span data-stu-id="1451f-123">As a result, when our operations team identifies devices that are having problems, we are better equipped to collect information from the device and diagnose issues.</span></span> <span data-ttu-id="1451f-124">接受 Update 2，表示您允許我們提供此主動支援。</span><span class="sxs-lookup"><span data-stu-id="1451f-124">By accepting Update 2, you allow us to provide this proactive support.</span></span>
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. <span data-ttu-id="1451f-125">驗證您的裝置正在執行 **StorSimple 8000 系列 Update 2 (6.3.9600.17673)**。</span><span class="sxs-lookup"><span data-stu-id="1451f-125">Verify that your device is running **StorSimple 8000 Series Update 2 (6.3.9600.17673)**.</span></span> <span data-ttu-id="1451f-126">[ **上次更新日期** ] 應該也已修改。</span><span class="sxs-lookup"><span data-stu-id="1451f-126">The **Last updated date** should also be modified.</span></span> <span data-ttu-id="1451f-127">您也會看到有可用的維護模式更新 (此訊息可能會在您安裝更新之後繼續顯示長達 24 小時)。</span><span class="sxs-lookup"><span data-stu-id="1451f-127">You'll also see that Maintenance mode updates are available (this message might continue to be displayed for up to 24 hours after you install the updates).</span></span>
   
   <span data-ttu-id="1451f-128">維護模式更新為干擾性更新，會導致裝置產生停機時間，且只能透過您裝置的 Windows PowerShell 介面加以套用。</span><span class="sxs-lookup"><span data-stu-id="1451f-128">Maintenance mode updates are disruptive updates that result in device downtime and can only be applied via the Windows PowerShell interface of your device.</span></span> <span data-ttu-id="1451f-129">在某些情況下，當您執行 Update 1.2 時，磁碟韌體可能已經是最新狀態，這種情況下，您不需要安裝任何維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="1451f-129">In some cases when you are running Update 1.2, your disk firmware might already be up-to-date, in which case you don't need to install any maintenance mode updates.</span></span>
2. <span data-ttu-id="1451f-130">使用 [下載 Hotfix](#to-download-hotfixes) 中列出的步驟，下載維護模式更新，以搜尋和下載 KB3121899，它會安裝磁碟韌體更新 (現在其他更新應該已安裝)。</span><span class="sxs-lookup"><span data-stu-id="1451f-130">Download the maintenance mode updates by using the steps listed in [To download hotfixes](#to-download-hotfixes) to search for and download KB3121899, which installs disk firmware updates (the other updates should already be installed by now).</span></span>
3. <span data-ttu-id="1451f-131">請遵循 [安裝及驗證維護模式 Hotfix](#to-install-and-verify-maintenance-mode-hotfixes) 中列出的步驟安裝維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="1451f-131">Follow the steps listed in [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes) to install the maintenance mode updates.</span></span>

## <a name="install-update-2-as-a-hotfix"></a><span data-ttu-id="1451f-132">以 Hotfix 的方式安裝 Update 2</span><span class="sxs-lookup"><span data-stu-id="1451f-132">Install Update 2 as a hotfix</span></span>
<span data-ttu-id="1451f-133">請在嘗試透過 Azure 傳統入口網站安裝更新，而無法通過閘道器檢查時執行此程序。</span><span class="sxs-lookup"><span data-stu-id="1451f-133">Use this procedure if you fail the gateway check when trying to install the updates through the Azure classic portal.</span></span> <span data-ttu-id="1451f-134">當您指派閘道器給非 DATA 0 網路介面且您的裝置正在執行早於 Update 1 的軟體版本時，檢查才會失敗。</span><span class="sxs-lookup"><span data-stu-id="1451f-134">The check fails as you have a gateway assigned to a non-DATA 0 network interface and your device is running a software version prior to Update 1.</span></span>

<span data-ttu-id="1451f-135">可以使用 Hotfix 方法升級的軟體版本為 Update 0.1、Update 0.2、Update 0.3、Update 1、Update 1.1 及 Update 1.2。</span><span class="sxs-lookup"><span data-stu-id="1451f-135">The software versions that can be upgraded using the hotfix method are Update 0.1, Update 0.2, and Update 0.3, Update 1, Update 1.1, and Update 1.2.</span></span> <span data-ttu-id="1451f-136">Hotfix 方法涉及下列三個步驟：</span><span class="sxs-lookup"><span data-stu-id="1451f-136">The hotfix method involves the following three steps:</span></span>

* <span data-ttu-id="1451f-137">從 Microsoft Update Catalog 下載 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="1451f-137">Download the hotfixes from the Microsoft Update Catalog.</span></span>
* <span data-ttu-id="1451f-138">安裝及驗證定期模式 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="1451f-138">Install and verify the regular mode hotfixes.</span></span>
* <span data-ttu-id="1451f-139">安裝及驗證維護模式 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="1451f-139">Install and verify the maintenance mode hotfix.</span></span>

<span data-ttu-id="1451f-140">若要將 Update 2 安裝為 Hotfix，您必須下載並安裝下列 Hotfix：</span><span class="sxs-lookup"><span data-stu-id="1451f-140">To install Update 2 as a hotfix, you must download and install the following hotfixes:</span></span>

| <span data-ttu-id="1451f-141">順序</span><span class="sxs-lookup"><span data-stu-id="1451f-141">Order</span></span> | <span data-ttu-id="1451f-142">KB</span><span class="sxs-lookup"><span data-stu-id="1451f-142">KB</span></span> | <span data-ttu-id="1451f-143">說明</span><span class="sxs-lookup"><span data-stu-id="1451f-143">Description</span></span> | <span data-ttu-id="1451f-144">更新類型</span><span class="sxs-lookup"><span data-stu-id="1451f-144">Update type</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1451f-145">1</span><span class="sxs-lookup"><span data-stu-id="1451f-145">1</span></span> |<span data-ttu-id="1451f-146">KB3121901</span><span class="sxs-lookup"><span data-stu-id="1451f-146">KB3121901</span></span> |<span data-ttu-id="1451f-147">軟體更新</span><span class="sxs-lookup"><span data-stu-id="1451f-147">Software update</span></span> |<span data-ttu-id="1451f-148">定期</span><span class="sxs-lookup"><span data-stu-id="1451f-148">Regular</span></span> |
| <span data-ttu-id="1451f-149">2</span><span class="sxs-lookup"><span data-stu-id="1451f-149">2</span></span> |<span data-ttu-id="1451f-150">KB3121900</span><span class="sxs-lookup"><span data-stu-id="1451f-150">KB3121900</span></span> |<span data-ttu-id="1451f-151">LSI 驅動程式</span><span class="sxs-lookup"><span data-stu-id="1451f-151">LSI driver</span></span> |<span data-ttu-id="1451f-152">定期</span><span class="sxs-lookup"><span data-stu-id="1451f-152">Regular</span></span> |
| <span data-ttu-id="1451f-153">3</span><span class="sxs-lookup"><span data-stu-id="1451f-153">3</span></span> |<span data-ttu-id="1451f-154">KB3080728</span><span class="sxs-lookup"><span data-stu-id="1451f-154">KB3080728</span></span> |<span data-ttu-id="1451f-155">Storport 修正程式 </span><span class="sxs-lookup"><span data-stu-id="1451f-155">Storport fix</span></span> </br> <span data-ttu-id="1451f-156">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="1451f-156">Windows Server 2012 R2</span></span> |<span data-ttu-id="1451f-157">定期</span><span class="sxs-lookup"><span data-stu-id="1451f-157">Regular</span></span> |
| <span data-ttu-id="1451f-158">4</span><span class="sxs-lookup"><span data-stu-id="1451f-158">4</span></span> |<span data-ttu-id="1451f-159">KB3090322</span><span class="sxs-lookup"><span data-stu-id="1451f-159">KB3090322</span></span> |<span data-ttu-id="1451f-160">Spaceport 修正程式 </span><span class="sxs-lookup"><span data-stu-id="1451f-160">Spaceport fix</span></span> </br> <span data-ttu-id="1451f-161">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="1451f-161">Windows Server 2012 R2</span></span> |<span data-ttu-id="1451f-162">定期</span><span class="sxs-lookup"><span data-stu-id="1451f-162">Regular</span></span> |
| <span data-ttu-id="1451f-163">5</span><span class="sxs-lookup"><span data-stu-id="1451f-163">5</span></span> |<span data-ttu-id="1451f-164">KB3121899</span><span class="sxs-lookup"><span data-stu-id="1451f-164">KB3121899</span></span> |<span data-ttu-id="1451f-165">磁碟韌體</span><span class="sxs-lookup"><span data-stu-id="1451f-165">Disk firmware</span></span> |<span data-ttu-id="1451f-166">維護</span><span class="sxs-lookup"><span data-stu-id="1451f-166">Maintenance</span></span> |

> [!IMPORTANT]
> * <span data-ttu-id="1451f-167">如果您的裝置正在執行 Release (GA) 版本，請連絡 [Microsoft 支援服務](storsimple-contact-microsoft-support.md) 以協助您進行更新。</span><span class="sxs-lookup"><span data-stu-id="1451f-167">If your device is running Release (GA) version, please contact [Microsoft Support](storsimple-contact-microsoft-support.md) to assist you with the update.</span></span>
> * <span data-ttu-id="1451f-168">此程序僅需要執行一次，即可套用 Update 2。</span><span class="sxs-lookup"><span data-stu-id="1451f-168">This procedure needs to be performed only once to apply Update 2.</span></span> <span data-ttu-id="1451f-169">您可以使用 Azure 傳統入口網站套用後續的更新。</span><span class="sxs-lookup"><span data-stu-id="1451f-169">You can use the Azure classic portal to apply subsequent updates.</span></span>
> * <span data-ttu-id="1451f-170">每個 Hotfix 安裝可能需要約 20 分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="1451f-170">Each hotfix installation can take about 20 minutes to complete.</span></span> <span data-ttu-id="1451f-171">總計的安裝時間接近 2 小時。</span><span class="sxs-lookup"><span data-stu-id="1451f-171">Total install time is close to 2 hours.</span></span>
> * <span data-ttu-id="1451f-172">使用此程序套用更新之前，請確定兩個裝置控制器都在線上，而且所有硬體元件的狀況良好。</span><span class="sxs-lookup"><span data-stu-id="1451f-172">Before using this procedure to apply the update, make sure that both device controllers are online and all the hardware components are healthy.</span></span>
> 
> 

<span data-ttu-id="1451f-173">執行下列步驟，以 Hotfix 方式套用此更新。</span><span class="sxs-lookup"><span data-stu-id="1451f-173">Perform the following steps to apply this update as a hotfix.</span></span>

[!INCLUDE [storsimple-install-update2-hotfix](../../includes/storsimple-install-update2-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a><span data-ttu-id="1451f-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1451f-174">Next steps</span></span>
<span data-ttu-id="1451f-175">深入了解 [Update 2 版](storsimple-update2-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="1451f-175">Learn more about the [Update 2 release](storsimple-update2-release-notes.md).</span></span>

