---
title: "在 StorSimple 裝置上安裝 Update 3 | Microsoft Docs"
description: "說明如何在您的 StorSimple 8000 系列裝置上安裝「StorSimple 8000 系列 Update 3」。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: c6c4634d-4f3a-4bc4-b307-a22bf18664e1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 72b004a6c2604e0fc20b71b4b69217622f8f9ea0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-3-on-your-storsimple-8000-series-device"></a><span data-ttu-id="5fdee-103">在 StorSimple 8000 系列裝置上安裝 Update 3</span><span class="sxs-lookup"><span data-stu-id="5fdee-103">Install Update 3 on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="5fdee-104">概觀</span><span class="sxs-lookup"><span data-stu-id="5fdee-104">Overview</span></span>

<span data-ttu-id="5fdee-105">本教學課程說明如何透過 Azure 傳統入口網站及使用 Hotfix 方法，在執行舊軟體版本的 StorSimple 裝置上安裝 Update 3。</span><span class="sxs-lookup"><span data-stu-id="5fdee-105">This tutorial explains how to install Update 3 on a StorSimple device running an earlier software version via the Azure classic portal and using the hotfix method.</span></span> <span data-ttu-id="5fdee-106">當閘道器是設定於 StorSimple 裝置之 DATA 0 以外的網路介面上，且您正嘗試從 Update 1 以前的軟體版本更新時，就會使用 Hotfix 方法。</span><span class="sxs-lookup"><span data-stu-id="5fdee-106">The hotfix method is used when a gateway is configured on a network interface other than DATA 0 of the StorSimple device and you are trying to update from a pre-Update 1 software version.</span></span>

<span data-ttu-id="5fdee-107">Update 3 包含裝置軟體、LSI 驅動程式和韌體以及 Storport 和 Spaceport 的更新。</span><span class="sxs-lookup"><span data-stu-id="5fdee-107">Update 3 includes device software, LSI driver and firmware, Storport and Spaceport updates.</span></span> <span data-ttu-id="5fdee-108">如果是從 Update 2 或更舊的版本進行更新，系統也會要求您套用 iSCSI、WMI 更新，以及在某些情況下必須套用磁碟韌體更新。</span><span class="sxs-lookup"><span data-stu-id="5fdee-108">If updating from Update 2 or an earlier version, you will also be required to apply iSCSI, WMI, and in certain cases, disk firmware updates.</span></span> <span data-ttu-id="5fdee-109">裝置軟體、WMI、iSCSI、LSI 驅動程式、Spaceport 及 Storport 修正程式為非干擾性更新，且可透過 Azure 傳統入口網站套用。</span><span class="sxs-lookup"><span data-stu-id="5fdee-109">The device software, WMI, iSCSI, LSI driver, Spaceport, and Storport fixes are non-disruptive updates and can be applied via the Azure classic portal.</span></span> <span data-ttu-id="5fdee-110">磁碟韌體更新為干擾性更新，且只能透過裝置的 Windows PowerShell 介面套用。</span><span class="sxs-lookup"><span data-stu-id="5fdee-110">The disk firmware updates are disruptive updates and can only be applied via the Windows PowerShell interface of the device.</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="5fdee-111">安裝前會執行一組手動和自動預先檢查，以根據硬體狀態和網路連線來判斷裝置健全狀況。</span><span class="sxs-lookup"><span data-stu-id="5fdee-111">A set of manual and automatic pre-checks are done prior to the install to determine the device health in terms of hardware state and network connectivity.</span></span> <span data-ttu-id="5fdee-112">這些預先檢查只會在您從 Azure 傳統入口網站套用更新時執行。</span><span class="sxs-lookup"><span data-stu-id="5fdee-112">These pre-checks are performed only if you apply the updates from the Azure classic portal.</span></span>
> * <span data-ttu-id="5fdee-113">建議您透過 Azure 傳統入口網站安裝軟體和驅動程式更新。</span><span class="sxs-lookup"><span data-stu-id="5fdee-113">We recommend that you install the software and driver updates via the Azure  classic portal.</span></span> <span data-ttu-id="5fdee-114">如果入口網站中的更新前閘道器檢查失敗，請移至裝置的 Windows PowerShell 介面安裝更新 (勿透過其他方式)。</span><span class="sxs-lookup"><span data-stu-id="5fdee-114">You should only go to the Windows PowerShell interface of the device (to install updates) if the pre-update gateway check fails in the portal.</span></span> <span data-ttu-id="5fdee-115">視您從哪一個版本更新而定，可能需要 1.5-2.5 小時來安裝更新。</span><span class="sxs-lookup"><span data-stu-id="5fdee-115">Depending upon the version you are updating from, the updates may take 1.5-2.5 hours to install.</span></span> <span data-ttu-id="5fdee-116">維護模式更新必須透過裝置的 Windows PowerShell 介面安裝。</span><span class="sxs-lookup"><span data-stu-id="5fdee-116">The maintenance mode updates must be installed via the Windows PowerShell interface of the device.</span></span> <span data-ttu-id="5fdee-117">由於維護模式更新是干擾性更新，它們將會導致裝置的停機時間。</span><span class="sxs-lookup"><span data-stu-id="5fdee-117">As maintenance mode updates are disruptive updates, these will result in a down time for your device.</span></span>
> * <span data-ttu-id="5fdee-118">如果執行選擇性的 StorSimple Snapshot Manager，更新裝置之前，請先將您的 Snapshot Manager 版本升級至 Update 2。</span><span class="sxs-lookup"><span data-stu-id="5fdee-118">If running the optional StorSimple Snapshot Manager, ensure that you have upgraded your Snapshot Manager version to Update 2 prior to updating the device.</span></span>
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-3-via-the-azure-classic-portal"></a><span data-ttu-id="5fdee-119">透過 Azure 傳統入口網站安裝 Update 3</span><span class="sxs-lookup"><span data-stu-id="5fdee-119">Install Update 3 via the Azure classic portal</span></span>
<span data-ttu-id="5fdee-120">請執行下列步驟來將您的裝置更新至 [Update 3](storsimple-update3-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="5fdee-120">Perform the following steps to update your device to [Update 3](storsimple-update3-release-notes.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5fdee-121">如果您是要套用 Update 2 或更新版本 (包括 Update 2.1)，Microsoft 將可以提取裝置的其他診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="5fdee-121">If you are applying Update 2 or later (including Update 2.1), Microsoft will be able to pull additional diagnostic information from the device.</span></span> <span data-ttu-id="5fdee-122">因此，當我們的作業小組識別有問題的裝置時，我們更有能力從裝置收集資訊並診斷問題。</span><span class="sxs-lookup"><span data-stu-id="5fdee-122">As a result, when our operations team identifies devices that are having problems, we are better equipped to collect information from the device and diagnose issues.</span></span> <span data-ttu-id="5fdee-123">接受 Update 2 或更新版本，表示您允許我們提供此主動支援。</span><span class="sxs-lookup"><span data-stu-id="5fdee-123">By accepting Update 2 or later, you allow us to provide this proactive support.</span></span>
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

<span data-ttu-id="5fdee-124">確認您裝置執行的是 **StorSimple 8000 系列 Update 3 (6.3.9600.17759)**。</span><span class="sxs-lookup"><span data-stu-id="5fdee-124">Verify that your device is running **StorSimple 8000 Series Update 3 (6.3.9600.17759)**.</span></span> <span data-ttu-id="5fdee-125">[ **上次更新日期** ] 應該也已修改。</span><span class="sxs-lookup"><span data-stu-id="5fdee-125">The **Last updated date** should also be modified.</span></span> 
   - <span data-ttu-id="5fdee-126">如果您是從 Update 2 之前的版本更新，您也會看到有可用的維護模式更新 (此訊息可能會在您安裝更新之後繼續顯示長達 24 小時)。</span><span class="sxs-lookup"><span data-stu-id="5fdee-126">If you are updating from a version prior to Update 2, you will also see that the Maintenance mode updates are available (this message might continue to be displayed for up to 24 hours after you install the updates).</span></span>
     <span data-ttu-id="5fdee-127">維護模式更新為干擾性更新，會導致裝置產生停機時間，且只能透過您裝置的 Windows PowerShell 介面加以套用。</span><span class="sxs-lookup"><span data-stu-id="5fdee-127">Maintenance mode updates are disruptive updates that result in device downtime and can only be applied via the Windows PowerShell interface of your device.</span></span> <span data-ttu-id="5fdee-128">在某些情況下，當您執行 Update 1.2 時，磁碟韌體可能已經是最新狀態，這種情況下，您不需要安裝任何維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="5fdee-128">In some cases when you are running Update 1.2, your disk firmware might already be up-to-date, in which case you don't need to install any maintenance mode updates.</span></span>
   - <span data-ttu-id="5fdee-129">如果您是從 Update 2 或更新版本進行更新，您的裝置現在應該已是最新狀態。</span><span class="sxs-lookup"><span data-stu-id="5fdee-129">If you are updating from Update 2 or later, your device should now be up-to-date.</span></span> <span data-ttu-id="5fdee-130">您可以略過下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="5fdee-130">You can skip the next step.</span></span>

<span data-ttu-id="5fdee-131">下載維護模式更新，方法是使用 [下載 Hotfix](#to-download-hotfixes) 中列出的步驟來搜尋和下載 KB3121899，它會安裝磁碟韌體更新 (此時應該已經安裝其他更新)。</span><span class="sxs-lookup"><span data-stu-id="5fdee-131">Download the maintenance mode updates by using the steps listed in [to download hotfixes](#to-download-hotfixes) to search for and download KB3121899, which installs disk firmware updates (the other updates should already be installed by now).</span></span> <span data-ttu-id="5fdee-132">請遵循 [安裝及驗證維護模式 Hotfix](#to-install-and-verify-maintenance-mode-hotfixes) 中列出的步驟安裝維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="5fdee-132">Follow the steps listed in [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes) to install the maintenance mode updates.</span></span> 

## <a name="install-update-3-as-a-hotfix"></a><span data-ttu-id="5fdee-133">以 Hotfix 方式安裝 Update 3</span><span class="sxs-lookup"><span data-stu-id="5fdee-133">Install Update 3 as a hotfix</span></span>
<span data-ttu-id="5fdee-134">請在嘗試透過 Azure 傳統入口網站安裝更新，而無法通過閘道器檢查時執行此程序。</span><span class="sxs-lookup"><span data-stu-id="5fdee-134">Use this procedure if you fail the gateway check when trying to install the updates through the Azure classic portal.</span></span> <span data-ttu-id="5fdee-135">當您指派閘道器給非 DATA 0 網路介面且您的裝置正在執行早於 Update 1 的軟體版本時，檢查才會失敗。</span><span class="sxs-lookup"><span data-stu-id="5fdee-135">The check fails as you have a gateway assigned to a non-DATA 0 network interface and your device is running a software version prior to Update 1.</span></span>

<span data-ttu-id="5fdee-136">可以使用 Hotfix 方法升級的軟體版本為：</span><span class="sxs-lookup"><span data-stu-id="5fdee-136">The software versions that can be upgraded using the hotfix method are:</span></span>

* <span data-ttu-id="5fdee-137">Update 0.1、0.2、0.3</span><span class="sxs-lookup"><span data-stu-id="5fdee-137">Update 0.1, 0.2, 0.3</span></span>
* <span data-ttu-id="5fdee-138">Update 1、1.1、1.2</span><span class="sxs-lookup"><span data-stu-id="5fdee-138">Update 1, 1.1, 1.2</span></span>
* <span data-ttu-id="5fdee-139">Update 2、2.1、2.2</span><span class="sxs-lookup"><span data-stu-id="5fdee-139">Update 2, 2.1, 2.2</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="5fdee-140">如果您的裝置正在執行 Release (GA) 版本，請連絡 [Microsoft 支援服務](storsimple-contact-microsoft-support.md) 以協助您進行更新。</span><span class="sxs-lookup"><span data-stu-id="5fdee-140">If your device is running Release (GA) version, please contact [Microsoft Support](storsimple-contact-microsoft-support.md) to assist you with the update.</span></span>
> 
> 

<span data-ttu-id="5fdee-141">Hotfix 方法涉及下列三個步驟：</span><span class="sxs-lookup"><span data-stu-id="5fdee-141">The hotfix method involves the following three steps:</span></span>

1. <span data-ttu-id="5fdee-142">從 Microsoft Update Catalog 下載 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="5fdee-142">Download the hotfixes from the Microsoft Update Catalog.</span></span>
2. <span data-ttu-id="5fdee-143">安裝及驗證定期模式 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="5fdee-143">Install and verify the regular mode hotfixes.</span></span>
3. <span data-ttu-id="5fdee-144">安裝並確認維護模式 Hotfix (僅限於從 Update 2 之前的軟體更新時)。</span><span class="sxs-lookup"><span data-stu-id="5fdee-144">Install and verify the maintenance mode hotfix (only when updating from pre-Update 2 software).</span></span>

#### <a name="download-updates-for-your-device"></a><span data-ttu-id="5fdee-145">下載適用於您裝置的更新</span><span class="sxs-lookup"><span data-stu-id="5fdee-145">Download updates for your device</span></span>
<span data-ttu-id="5fdee-146">**如果您裝置執行的是 Update 2.1 或 2.2**，您就必須依指定的順序下載並安裝下列 Hotfix：</span><span class="sxs-lookup"><span data-stu-id="5fdee-146">**If your device is running Update 2.1 or 2.2**, you must download and install the following hotfixes in the prescribed order:</span></span>

| <span data-ttu-id="5fdee-147">順序</span><span class="sxs-lookup"><span data-stu-id="5fdee-147">Order</span></span> | <span data-ttu-id="5fdee-148">KB</span><span class="sxs-lookup"><span data-stu-id="5fdee-148">KB</span></span> | <span data-ttu-id="5fdee-149">說明</span><span class="sxs-lookup"><span data-stu-id="5fdee-149">Description</span></span> | <span data-ttu-id="5fdee-150">更新類型</span><span class="sxs-lookup"><span data-stu-id="5fdee-150">Update type</span></span> | <span data-ttu-id="5fdee-151">安裝時間</span><span class="sxs-lookup"><span data-stu-id="5fdee-151">Install time</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5fdee-152">1.</span><span class="sxs-lookup"><span data-stu-id="5fdee-152">1.</span></span> |<span data-ttu-id="5fdee-153">KB3186843</span><span class="sxs-lookup"><span data-stu-id="5fdee-153">KB3186843</span></span> |<span data-ttu-id="5fdee-154">軟體更新 &#42;</span><span class="sxs-lookup"><span data-stu-id="5fdee-154">Software update &#42;</span></span> |<span data-ttu-id="5fdee-155">定期 </span><span class="sxs-lookup"><span data-stu-id="5fdee-155">Regular</span></span> <br></br><span data-ttu-id="5fdee-156">非干擾性</span><span class="sxs-lookup"><span data-stu-id="5fdee-156">Non-disruptive</span></span> |<span data-ttu-id="5fdee-157">~ 45 分鐘</span><span class="sxs-lookup"><span data-stu-id="5fdee-157">~ 45 mins</span></span> |
| <span data-ttu-id="5fdee-158">2.</span><span class="sxs-lookup"><span data-stu-id="5fdee-158">2.</span></span> |<span data-ttu-id="5fdee-159">KB3186859</span><span class="sxs-lookup"><span data-stu-id="5fdee-159">KB3186859</span></span> |<span data-ttu-id="5fdee-160">LSI 驅動程式與韌體</span><span class="sxs-lookup"><span data-stu-id="5fdee-160">LSI driver and firmware</span></span> |<span data-ttu-id="5fdee-161">定期 </span><span class="sxs-lookup"><span data-stu-id="5fdee-161">Regular</span></span> <br></br><span data-ttu-id="5fdee-162">非干擾性</span><span class="sxs-lookup"><span data-stu-id="5fdee-162">Non-disruptive</span></span> |<span data-ttu-id="5fdee-163">~ 20 分鐘</span><span class="sxs-lookup"><span data-stu-id="5fdee-163">~ 20 mins</span></span> |
| <span data-ttu-id="5fdee-164">3.</span><span class="sxs-lookup"><span data-stu-id="5fdee-164">3.</span></span> |<span data-ttu-id="5fdee-165">KB3121261</span><span class="sxs-lookup"><span data-stu-id="5fdee-165">KB3121261</span></span> |<span data-ttu-id="5fdee-166">Storport 和 Spaceport 修正程式 </span><span class="sxs-lookup"><span data-stu-id="5fdee-166">Storport and Spaceport fix</span></span> </br> <span data-ttu-id="5fdee-167">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="5fdee-167">Windows Server 2012 R2</span></span> |<span data-ttu-id="5fdee-168">定期 </span><span class="sxs-lookup"><span data-stu-id="5fdee-168">Regular</span></span> <br></br><span data-ttu-id="5fdee-169">非干擾性</span><span class="sxs-lookup"><span data-stu-id="5fdee-169">Non-disruptive</span></span> |<span data-ttu-id="5fdee-170">~ 20 分鐘</span><span class="sxs-lookup"><span data-stu-id="5fdee-170">~ 20 mins</span></span> |

<span data-ttu-id="5fdee-171">&#42;  *請注意，軟體更新是由兩個二進位檔組成︰開頭為 `all-hcsmdssoftwareupdate` 的裝置軟體更新，以及開頭為 `all-cismdsagentupdatebundle` 的 Cis 和 Mds 代理程式。必須先安裝裝置軟體更新，再安裝 Cis 和 Mds 代理程式。您還必須在套用 Cis 和 MDS 代理程式更新之後，先透過 `Restart-HcsController` Cmdlet 重新啟動作用中的控制器，然後才套用剩餘的更新。*</span><span class="sxs-lookup"><span data-stu-id="5fdee-171">&#42;  *Note that the software update consists of two binary files: device software update prefaced with `all-hcsmdssoftwareupdate` and the Cis and Mds agent prefaced with `all-cismdsagentupdatebundle`. The device software update must be installed before the Cis and Mds agent. You must also restart the active controller via the `Restart-HcsController` cmdlet after you apply the Cis and Mds agent update (and before applying the remaining updates).*</span></span> 

<span data-ttu-id="5fdee-172">**如果您裝置執行的是 Update 0.1、0.2、0.3、1.0、1.1、1.2 或 2.0**，則除了軟體、LSI 驅動程式及韌體更新 (如前一個表格所示) 之外，您還必須依指定的順序下載並安裝下列 Hotfix：</span><span class="sxs-lookup"><span data-stu-id="5fdee-172">**If your device is running Update 0.1, 0.2, 0.3, 1.0, 1.1, 1.2, or 2.0**, you must download and install the following hotfixes in addition to the software, LSI driver and firmware updates (shown in the preceding table), in the prescribed order:</span></span>

| <span data-ttu-id="5fdee-173">順序</span><span class="sxs-lookup"><span data-stu-id="5fdee-173">Order</span></span> | <span data-ttu-id="5fdee-174">KB</span><span class="sxs-lookup"><span data-stu-id="5fdee-174">KB</span></span> | <span data-ttu-id="5fdee-175">說明</span><span class="sxs-lookup"><span data-stu-id="5fdee-175">Description</span></span> | <span data-ttu-id="5fdee-176">更新類型</span><span class="sxs-lookup"><span data-stu-id="5fdee-176">Update type</span></span> | <span data-ttu-id="5fdee-177">安裝時間</span><span class="sxs-lookup"><span data-stu-id="5fdee-177">Install time</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5fdee-178">4.</span><span class="sxs-lookup"><span data-stu-id="5fdee-178">4.</span></span> |<span data-ttu-id="5fdee-179">KB3146621</span><span class="sxs-lookup"><span data-stu-id="5fdee-179">KB3146621</span></span> |<span data-ttu-id="5fdee-180">iSCSI 封裝</span><span class="sxs-lookup"><span data-stu-id="5fdee-180">iSCSI package</span></span> |<span data-ttu-id="5fdee-181">定期 </span><span class="sxs-lookup"><span data-stu-id="5fdee-181">Regular</span></span> <br></br><span data-ttu-id="5fdee-182">非干擾性</span><span class="sxs-lookup"><span data-stu-id="5fdee-182">Non-disruptive</span></span> |<span data-ttu-id="5fdee-183">~ 20 分鐘</span><span class="sxs-lookup"><span data-stu-id="5fdee-183">~ 20 mins</span></span> |
| <span data-ttu-id="5fdee-184">5.</span><span class="sxs-lookup"><span data-stu-id="5fdee-184">5.</span></span> |<span data-ttu-id="5fdee-185">KB3103616</span><span class="sxs-lookup"><span data-stu-id="5fdee-185">KB3103616</span></span> |<span data-ttu-id="5fdee-186">WMI 封裝</span><span class="sxs-lookup"><span data-stu-id="5fdee-186">WMI package</span></span> |<span data-ttu-id="5fdee-187">定期 </span><span class="sxs-lookup"><span data-stu-id="5fdee-187">Regular</span></span> <br></br><span data-ttu-id="5fdee-188">非干擾性</span><span class="sxs-lookup"><span data-stu-id="5fdee-188">Non-disruptive</span></span> |<span data-ttu-id="5fdee-189">~ 12 分鐘</span><span class="sxs-lookup"><span data-stu-id="5fdee-189">~ 12 mins</span></span> |

<br></br>

<span data-ttu-id="5fdee-190">**如果您裝置執行的版本是 0.2、0.3、1.0、1.1 及 1.2**，則除了前面表格所示的所有更新之外，您可能還需要安裝磁碟韌體更新。</span><span class="sxs-lookup"><span data-stu-id="5fdee-190">**If your device is running versions 0.2, 0.3, 1.0, 1.1, and 1.2**, you may also need to install disk firmware updates on top of all the updates shown in the preceding tables.</span></span> <span data-ttu-id="5fdee-191">您可以執行 `Get-HcsFirmwareVersion` Cmdlet 來確認是否需要進行磁碟韌體更新。</span><span class="sxs-lookup"><span data-stu-id="5fdee-191">You can verify whether you need the disk firmware updates by running the `Get-HcsFirmwareVersion` cmdlet.</span></span> <span data-ttu-id="5fdee-192">如果您執行的是這些韌體版本：`XMGG`、`XGEG`、`KZ50`、`F6C2`、`VR08`，您就不需要安裝這些更新。</span><span class="sxs-lookup"><span data-stu-id="5fdee-192">If you are running these firmware versions: `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, then you do not need to install these updates.</span></span>

| <span data-ttu-id="5fdee-193">順序</span><span class="sxs-lookup"><span data-stu-id="5fdee-193">Order</span></span> | <span data-ttu-id="5fdee-194">KB</span><span class="sxs-lookup"><span data-stu-id="5fdee-194">KB</span></span> | <span data-ttu-id="5fdee-195">說明</span><span class="sxs-lookup"><span data-stu-id="5fdee-195">Description</span></span> | <span data-ttu-id="5fdee-196">更新類型</span><span class="sxs-lookup"><span data-stu-id="5fdee-196">Update type</span></span> | <span data-ttu-id="5fdee-197">安裝時間</span><span class="sxs-lookup"><span data-stu-id="5fdee-197">Install time</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5fdee-198">6.</span><span class="sxs-lookup"><span data-stu-id="5fdee-198">6.</span></span> |<span data-ttu-id="5fdee-199">KB3121899</span><span class="sxs-lookup"><span data-stu-id="5fdee-199">KB3121899</span></span> |<span data-ttu-id="5fdee-200">磁碟韌體</span><span class="sxs-lookup"><span data-stu-id="5fdee-200">Disk firmware</span></span> |<span data-ttu-id="5fdee-201">維護 </span><span class="sxs-lookup"><span data-stu-id="5fdee-201">Maintenance</span></span> <br></br><span data-ttu-id="5fdee-202">干擾性</span><span class="sxs-lookup"><span data-stu-id="5fdee-202">Disruptive</span></span> |<span data-ttu-id="5fdee-203">~ 30 分鐘</span><span class="sxs-lookup"><span data-stu-id="5fdee-203">~ 30 mins</span></span> |

<br></br>

> [!IMPORTANT]
> * <span data-ttu-id="5fdee-204">此程序僅需要執行一次，即可套用 Update 3。</span><span class="sxs-lookup"><span data-stu-id="5fdee-204">This procedure needs to be performed only once to apply Update 3.</span></span> <span data-ttu-id="5fdee-205">您可以使用 Azure 傳統入口網站套用後續的更新。</span><span class="sxs-lookup"><span data-stu-id="5fdee-205">You can use the Azure classic portal to apply subsequent updates.</span></span>
> * <span data-ttu-id="5fdee-206">如果您是從 Update 2.2 進行更新，則總安裝時間會接近 1.1 小時。</span><span class="sxs-lookup"><span data-stu-id="5fdee-206">If updating from Update 2.2, the total install time is close to 1.1 hours.</span></span>
> * <span data-ttu-id="5fdee-207">使用此程序套用更新之前，請確定兩個裝置控制器都在線上，而且所有硬體元件的狀況良好。</span><span class="sxs-lookup"><span data-stu-id="5fdee-207">Before using this procedure to apply the update, make sure that both the device controllers are online and all the hardware components are healthy.</span></span>
> 
> 

<span data-ttu-id="5fdee-208">請執行以下步驟來下載及安裝 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="5fdee-208">Perform the following steps to download and install the hotfixes.</span></span>

[!INCLUDE [storsimple-install-update3-hotfix](../../includes/storsimple-install-update3-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a><span data-ttu-id="5fdee-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5fdee-209">Next steps</span></span>
<span data-ttu-id="5fdee-210">深入了解 [Update 3 版](storsimple-update3-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="5fdee-210">Learn more about the [Update 3 release](storsimple-update3-release-notes.md).</span></span>

