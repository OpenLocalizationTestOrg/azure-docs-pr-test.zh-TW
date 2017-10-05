---
title: "在 StorSimple 裝置上安裝 Update 1.2 | Microsoft Docs"
description: "說明如何在您的 StorSimple 8000 系列裝置上安裝 StorSimple 8000 系列更新 1.2。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 7a513923-eb77-4078-b0ab-f8e90183796a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 80ff35cc47dfc38089f4c392ef4c90baf9ccc03e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-12-on-your-storsimple-8000-series-device"></a><span data-ttu-id="68396-103">在 StorSimple 8000 系列裝置上安裝 Update 1.2</span><span class="sxs-lookup"><span data-stu-id="68396-103">Install Update 1.2 on your StorSimple 8000 series device</span></span>
## <a name="overview"></a><span data-ttu-id="68396-104">概觀</span><span class="sxs-lookup"><span data-stu-id="68396-104">Overview</span></span>
<span data-ttu-id="68396-105">本教學課程說明如何在執行 Update 1 之前軟體版本的 StorSimple 裝置上安裝 Update 1.2。</span><span class="sxs-lookup"><span data-stu-id="68396-105">This tutorial explains how to install Update 1.2 on a StorSimple device that is running a software version prior to Update 1.</span></span> <span data-ttu-id="68396-106">本教學課程也涵蓋了在 StorSimple 裝置之 DATA 0 以外的網路介面上設定閘道器時，進行更新所需的額外步驟。</span><span class="sxs-lookup"><span data-stu-id="68396-106">The tutorial also covers the additional steps required for the update when a gateway is configured on a network interface other than DATA 0 of the StorSimple device.</span></span>

<span data-ttu-id="68396-107">Update 1.2 包括裝置軟體更新、LSI 驅動程式更新和磁碟韌體更新。</span><span class="sxs-lookup"><span data-stu-id="68396-107">Update 1.2 includes device software updates, LSI driver updates and disk firmware updates.</span></span> <span data-ttu-id="68396-108">此軟體和 LSI 驅動程式更新為非干擾性更新，且可透過 Azure 傳統入口網站套用。</span><span class="sxs-lookup"><span data-stu-id="68396-108">The software and LSI driver updates are non-disruptive updates and can be applied via the Azure classic portal.</span></span> <span data-ttu-id="68396-109">磁碟韌體更新為干擾性更新，且只能透過裝置的 Windows PowerShell 介面套用。</span><span class="sxs-lookup"><span data-stu-id="68396-109">The disk firmware updates are disruptive updates and can only be applied via the Windows PowerShell interface of the device.</span></span>

<span data-ttu-id="68396-110">根據正在執行的裝置版本，您可以判斷是否套用 Update 1.2。</span><span class="sxs-lookup"><span data-stu-id="68396-110">Depending upon which version your device is running, you can determine if Update 1.2 will be applied.</span></span> <span data-ttu-id="68396-111">您可以藉由瀏覽至裝置**儀表板**的**快速瀏覽**區段，檢查裝置的軟體版本。</span><span class="sxs-lookup"><span data-stu-id="68396-111">You can check the software version of your device by navigating to the **quick glance** section of your device **Dashboard**.</span></span>

</br>

| <span data-ttu-id="68396-112">如果執行的軟體版本...</span><span class="sxs-lookup"><span data-stu-id="68396-112">If running software version …</span></span> | <span data-ttu-id="68396-113">在入口網站會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="68396-113">What happens in the portal?</span></span> |
| --- | --- |
| <span data-ttu-id="68396-114">Release - GA</span><span class="sxs-lookup"><span data-stu-id="68396-114">Release - GA</span></span> |<span data-ttu-id="68396-115">如果您正在執行 Release 版本 (GA)，請勿套用此更新。</span><span class="sxs-lookup"><span data-stu-id="68396-115">If you are running Release version (GA), do not apply this update.</span></span> <span data-ttu-id="68396-116">請 [連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md) 來更新您的裝置。</span><span class="sxs-lookup"><span data-stu-id="68396-116">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) to update your device.</span></span> |
| <span data-ttu-id="68396-117">Update 0.1</span><span class="sxs-lookup"><span data-stu-id="68396-117">Update 0.1</span></span> |<span data-ttu-id="68396-118">入口網站套用 Update 1.2。</span><span class="sxs-lookup"><span data-stu-id="68396-118">Portal applies Update 1.2.</span></span> |
| <span data-ttu-id="68396-119">Update 0.2</span><span class="sxs-lookup"><span data-stu-id="68396-119">Update 0.2</span></span> |<span data-ttu-id="68396-120">入口網站套用 Update 1.2。</span><span class="sxs-lookup"><span data-stu-id="68396-120">Portal applies Update 1.2.</span></span> |
| <span data-ttu-id="68396-121">Update 0.3</span><span class="sxs-lookup"><span data-stu-id="68396-121">Update 0.3</span></span> |<span data-ttu-id="68396-122">入口網站套用 Update 1.2。</span><span class="sxs-lookup"><span data-stu-id="68396-122">Portal applies Update 1.2.</span></span> |
| <span data-ttu-id="68396-123">Update 1</span><span class="sxs-lookup"><span data-stu-id="68396-123">Update 1</span></span> |<span data-ttu-id="68396-124">此更新將無法使用。</span><span class="sxs-lookup"><span data-stu-id="68396-124">This update will not be available.</span></span> |
| <span data-ttu-id="68396-125">Update 1.1</span><span class="sxs-lookup"><span data-stu-id="68396-125">Update 1.1</span></span> |<span data-ttu-id="68396-126">此更新將無法使用。</span><span class="sxs-lookup"><span data-stu-id="68396-126">This update will not be available.</span></span> |

</br>

> [!IMPORTANT]
> * <span data-ttu-id="68396-127">您可能不會立即看到 Update 1.2，因為我們會分階段推出更新。</span><span class="sxs-lookup"><span data-stu-id="68396-127">You may not see Update 1.2 immediately because we do a phased rollout of the updates.</span></span> <span data-ttu-id="68396-128">請在數天內再次掃描更新，因為很快就會提供 Update。</span><span class="sxs-lookup"><span data-stu-id="68396-128">Scan for updates in a few days again as this Update will become available soon.</span></span>
> * <span data-ttu-id="68396-129">此更新包括一組手動和自動預先檢查，以根據硬體狀態和網路連線來判斷裝置健全狀況。</span><span class="sxs-lookup"><span data-stu-id="68396-129">This update includes a set of manual and automatic pre-checks to determine the device health in terms of hardware state and network connectivity.</span></span> <span data-ttu-id="68396-130">這些預先檢查只會在您從 Azure 傳統入口網站套用更新時執行。</span><span class="sxs-lookup"><span data-stu-id="68396-130">These pre-checks are performed only if you apply the updates from the Azure classic portal.</span></span>
> * <span data-ttu-id="68396-131">建議您透過 Azure 傳統入口網站安裝軟體和驅動程式更新。</span><span class="sxs-lookup"><span data-stu-id="68396-131">We recommend that you install the software and driver updates via the Azure classic portal.</span></span> <span data-ttu-id="68396-132">如果入口網站中的更新前閘道器檢查失敗，請移至裝置的 Windows PowerShell 介面安裝更新 (勿透過其他方式)。</span><span class="sxs-lookup"><span data-stu-id="68396-132">You should only go to the Windows PowerShell interface of the device (to install updates) if the pre-update gateway check fails in the portal.</span></span> <span data-ttu-id="68396-133">更新可能需要 5-10 小時才能安裝 (包括 Windows Updates)。</span><span class="sxs-lookup"><span data-stu-id="68396-133">The updates may take 5-10 hours to install (including the Windows Updates).</span></span> <span data-ttu-id="68396-134">維護模式更新必須透過裝置的 Windows PowerShell 介面安裝。</span><span class="sxs-lookup"><span data-stu-id="68396-134">The maintenance mode updates must be installed via the Windows PowerShell interface of the device.</span></span> <span data-ttu-id="68396-135">由於維護模式更新是干擾性更新，它們將會導致裝置的停機時間。</span><span class="sxs-lookup"><span data-stu-id="68396-135">As maintenance mode updates are disruptive updates, these will result in a down time for your device.</span></span>
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-12-via-the-azure-classic-portal"></a><span data-ttu-id="68396-136">透過 Azure 傳統入口網站安裝 Update 1.2</span><span class="sxs-lookup"><span data-stu-id="68396-136">Install Update 1.2 via the Azure classic portal</span></span>
<span data-ttu-id="68396-137">請執行下列步驟，以將您的裝置更新至 [Update 1.2](storsimple-update1-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="68396-137">Perform the following steps to update your device to [Update 1.2](storsimple-update1-release-notes.md).</span></span> <span data-ttu-id="68396-138">只有當您在裝置上的 DATA 0 網路介面上設定閘道器時才使用此程序。</span><span class="sxs-lookup"><span data-stu-id="68396-138">Use this procedure only if you have a gateway configured on DATA 0 network interface on your device.</span></span>

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. <span data-ttu-id="68396-139">確認您的裝置是否正在執行 **StorSimple 8000 Series Update 1.2 (6.3.9600.17584)**。</span><span class="sxs-lookup"><span data-stu-id="68396-139">Verify that your device is running **StorSimple 8000 Series Update 1.2 (6.3.9600.17584)**.</span></span> <span data-ttu-id="68396-140">[ **上次更新日期** ] 應該也已修改。</span><span class="sxs-lookup"><span data-stu-id="68396-140">The **Last updated date** should also be modified.</span></span> <span data-ttu-id="68396-141">您也會看到有可用的維護模式更新 (此訊息可能會在您安裝更新之後繼續顯示長達 24 小時)。</span><span class="sxs-lookup"><span data-stu-id="68396-141">You'll also see that Maintenance mode updates are available (this message might continue to be displayed for up to 24 hours after you install the updates).</span></span>
   
   <span data-ttu-id="68396-142">維護模式更新為干擾性更新，會導致裝置產生停機時間，且只能透過您裝置的 Windows PowerShell 介面加以套用。</span><span class="sxs-lookup"><span data-stu-id="68396-142">Maintenance mode updates are disruptive updates that result in device downtime and can only be applied via the Windows PowerShell interface of your device.</span></span>
   
   <span data-ttu-id="68396-143">![維護頁面](./media/storsimple-install-update-1/InstallUpdate12_10M.png "維護頁面")</span><span class="sxs-lookup"><span data-stu-id="68396-143">![Maintenance page](./media/storsimple-install-update-1/InstallUpdate12_10M.png "Maintenance page")</span></span>
2. <span data-ttu-id="68396-144">使用 [下載 Hotfix](#to-download-hotfixes) 中列出的步驟，下載維護模式更新，以搜尋和下載 KB3063416，它會安裝磁碟韌體更新 (現在其他更新應該已安裝)。</span><span class="sxs-lookup"><span data-stu-id="68396-144">Download the maintenance mode updates by using the steps listed in [To download hotfixes](#to-download-hotfixes) to search for and download KB3063416, which installs disk firmware updates (the other updates should already be installed by now).</span></span>
3. <span data-ttu-id="68396-145">請遵循 [安裝及驗證維護模式 Hotfix](#to-install-and-verify-maintenance-mode-hotfixes) 中列出的步驟安裝這些維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="68396-145">Follow the steps listed in [Install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes) to install the maintenance mode updates.</span></span>
4. <span data-ttu-id="68396-146">在 Azure 傳統入口網站，瀏覽至 [維護] 頁面，然後在頁面底部，按一下 [掃描更新] 來檢查是否有任何 Windows 更新，然後按一下 [安裝更新]。</span><span class="sxs-lookup"><span data-stu-id="68396-146">In the Azure classic portal, navigate to the **Maintenance** page and at the bottom of the page, click **Scan Updates** to check for any Windows Updates and then click **Install Updates**.</span></span> <span data-ttu-id="68396-147">成功安裝所有更新之後就完成了。</span><span class="sxs-lookup"><span data-stu-id="68396-147">You're finished after all of the updates are successfully installed.</span></span>

## <a name="install-update-12-on-a-device-that-has-a-gateway-configured-for-a-non-data-0-network-interface"></a><span data-ttu-id="68396-148">在含有為非 DATA 0 網路介面設定之閘道器的裝置上安裝 Update 1.2</span><span class="sxs-lookup"><span data-stu-id="68396-148">Install Update 1.2 on a device that has a gateway configured for a non-DATA 0 network interface</span></span>
<span data-ttu-id="68396-149">請只在嘗試透過 Azure 傳統入口網站安裝更新，而無法通過閘道器檢查時再執行此程序。</span><span class="sxs-lookup"><span data-stu-id="68396-149">You should use this procedure only if you fail the gateway check when trying to install the updates through the Azure classic portal.</span></span> <span data-ttu-id="68396-150">當您指派閘道器給非 DATA 0 網路介面且您的裝置正在執行早於 Update 1 的軟體版本時，檢查才會失敗。</span><span class="sxs-lookup"><span data-stu-id="68396-150">The check fails as you have a gateway assigned to a non-DATA 0 network interface and your device is running a software version prior to Update 1.</span></span> <span data-ttu-id="68396-151">如果您的裝置在非 DATA 0 網路介面上沒有閘道器，您可以直接在 Azure 傳統入口網站中更新您的裝置。</span><span class="sxs-lookup"><span data-stu-id="68396-151">If your device does not have a gateway on a non-DATA 0 network interface, you can update your device directly from the Azure classic portal.</span></span> <span data-ttu-id="68396-152">請參閱 [透過 Azure 傳統入口網站安裝 Update 1.2](#install-update-1.2-via-the-azure-classic-portal)。</span><span class="sxs-lookup"><span data-stu-id="68396-152">See [Install update 1.2 via the Azure classic portal](#install-update-1.2-via-the-azure-classic-portal).</span></span>

<span data-ttu-id="68396-153">可以使用這個方法升級的軟體版本為 Update 0.1、Update 0.2、和 Update 0.3。</span><span class="sxs-lookup"><span data-stu-id="68396-153">The software versions that can be upgraded using this method are Update 0.1, Update 0.2, and Update 0.3.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="68396-154">如果您的裝置正在執行 Release (GA) 版本，請連絡 [Microsoft 支援服務](storsimple-contact-microsoft-support.md) 以協助您進行更新。</span><span class="sxs-lookup"><span data-stu-id="68396-154">If your device is running Release (GA) version, please contact [Microsoft Support](storsimple-contact-microsoft-support.md) to assist you with the update.</span></span>
> * <span data-ttu-id="68396-155">此程序僅需要執行一次，即可套用 Update 1.2。</span><span class="sxs-lookup"><span data-stu-id="68396-155">This procedure needs to be performed only once to apply Update 1.2.</span></span> <span data-ttu-id="68396-156">您可以使用 Azure 傳統入口網站套用後續的更新。</span><span class="sxs-lookup"><span data-stu-id="68396-156">You can use the Azure classic portal to apply subsequent updates.</span></span>
> 
> 

<span data-ttu-id="68396-157">如果您的裝置執行的是 Update 1.0 之前版本的軟體，而且有設定 DATA 0 以外的網路介面的閘道器，您可以下列兩種方式套用 Update 1.2：</span><span class="sxs-lookup"><span data-stu-id="68396-157">If your device is running pre-Update 1 software and it has a gateway set for a network interface other than DATA 0, you can apply Update 1.2 in the following two ways:</span></span>

* <span data-ttu-id="68396-158">**選項 1**：下載更新，並從裝置的 Windows PowerShell 介面使用 `Start-HcsHotfix` Cmdlet 套用更新。</span><span class="sxs-lookup"><span data-stu-id="68396-158">**Option 1**: Download the update and apply it by using the `Start-HcsHotfix` cmdlet from the Windows PowerShell interface of the device.</span></span> <span data-ttu-id="68396-159">這是建議的方法。</span><span class="sxs-lookup"><span data-stu-id="68396-159">This is the recommended method.</span></span> <span data-ttu-id="68396-160">**如果您的裝置正在執行 Update 1.0 或 Update 1.1，請勿使用這個方法來套用 Update 1.2。**</span><span class="sxs-lookup"><span data-stu-id="68396-160">**Do not use this method to apply Update 1.2 if your device is running Update 1.0 or Update 1.1.**</span></span>
* <span data-ttu-id="68396-161">**選項 2**：直接從 Azure 傳統入口網站移除閘道器組態並安裝更新。</span><span class="sxs-lookup"><span data-stu-id="68396-161">**Option 2**: Remove the gateway configuration and install the update directly from the Azure classic portal.</span></span>

<span data-ttu-id="68396-162">下列各節提供每個選項的詳細指示。</span><span class="sxs-lookup"><span data-stu-id="68396-162">Detailed instructions for each of these are provided in the following sections.</span></span>

## <a name="option-1-use-windows-powershell-for-storsimple-to-apply-update-12-as-a-hotfix"></a><span data-ttu-id="68396-163">選項 1：使用 Windows PowerShell for StorSimple 套用 Update 1.2 做為 hotfix</span><span class="sxs-lookup"><span data-stu-id="68396-163">Option 1: Use Windows PowerShell for StorSimple to apply Update 1.2 as a hotfix</span></span>
<span data-ttu-id="68396-164">請只在您執行的是 Update 0.1、0.2、0.3，且嘗試透過 Azure 傳統入口網站安裝更新，而無法通過閘道器檢查時再執行此程序。</span><span class="sxs-lookup"><span data-stu-id="68396-164">You should use this procedure only if you are running Update 0.1, 0.2, 0.3 and if your gateway check has failed when trying to install updates from the Azure classic portal.</span></span> <span data-ttu-id="68396-165">如果您正在執行 Release (GA) 軟體，請連絡 [Microsoft 支援服務](storsimple-contact-microsoft-support.md) 以更新您的裝置。</span><span class="sxs-lookup"><span data-stu-id="68396-165">If you are running Release (GA) software, please [Microsoft Support](storsimple-contact-microsoft-support.md) to update your device.</span></span>

<span data-ttu-id="68396-166">若要將 Update 1.2 安裝為 Hotfix，您必須下載並安裝下列 Hotfix：</span><span class="sxs-lookup"><span data-stu-id="68396-166">To install Update 1.2 as a hotfix, you must download and install the following hotfixes:</span></span>

| <span data-ttu-id="68396-167">順序</span><span class="sxs-lookup"><span data-stu-id="68396-167">Order</span></span> | <span data-ttu-id="68396-168">KB</span><span class="sxs-lookup"><span data-stu-id="68396-168">KB</span></span> | <span data-ttu-id="68396-169">說明</span><span class="sxs-lookup"><span data-stu-id="68396-169">Description</span></span> | <span data-ttu-id="68396-170">更新類型</span><span class="sxs-lookup"><span data-stu-id="68396-170">Update type</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="68396-171">1</span><span class="sxs-lookup"><span data-stu-id="68396-171">1</span></span> |<span data-ttu-id="68396-172">KB3063418</span><span class="sxs-lookup"><span data-stu-id="68396-172">KB3063418</span></span> |<span data-ttu-id="68396-173">軟體更新</span><span class="sxs-lookup"><span data-stu-id="68396-173">Software update</span></span> |<span data-ttu-id="68396-174">定期</span><span class="sxs-lookup"><span data-stu-id="68396-174">Regular</span></span> |
| <span data-ttu-id="68396-175">2</span><span class="sxs-lookup"><span data-stu-id="68396-175">2</span></span> |<span data-ttu-id="68396-176">KB3043005</span><span class="sxs-lookup"><span data-stu-id="68396-176">KB3043005</span></span> |<span data-ttu-id="68396-177">LSI SAS 控制器更新</span><span class="sxs-lookup"><span data-stu-id="68396-177">LSI SAS controller update</span></span> |<span data-ttu-id="68396-178">定期</span><span class="sxs-lookup"><span data-stu-id="68396-178">Regular</span></span> |
| <span data-ttu-id="68396-179">3</span><span class="sxs-lookup"><span data-stu-id="68396-179">3</span></span> |<span data-ttu-id="68396-180">KB3063416</span><span class="sxs-lookup"><span data-stu-id="68396-180">KB3063416</span></span> |<span data-ttu-id="68396-181">磁碟韌體</span><span class="sxs-lookup"><span data-stu-id="68396-181">Disk firmware</span></span> |<span data-ttu-id="68396-182">維護</span><span class="sxs-lookup"><span data-stu-id="68396-182">Maintenance</span></span> |

<span data-ttu-id="68396-183">使用此程序套用更新之前，請確認：</span><span class="sxs-lookup"><span data-stu-id="68396-183">Before using this procedure to apply the update, make sure that:</span></span>

* <span data-ttu-id="68396-184">這兩個裝置控制器都在線上。</span><span class="sxs-lookup"><span data-stu-id="68396-184">Both device controllers are online.</span></span>

<span data-ttu-id="68396-185">請執行下列步驟，以套用 Update 1.2。</span><span class="sxs-lookup"><span data-stu-id="68396-185">Perform the following steps to apply Update 1.2.</span></span> <span data-ttu-id="68396-186">**更新可能需要大約 2 小時才能完成 (軟體需要約 30 分鐘、驅動程式需要約 30 分鐘、磁碟韌體需要約 45 分鐘)。**</span><span class="sxs-lookup"><span data-stu-id="68396-186">**The updates could take around 2 hours to complete (approximately 30 minutes for software, 30 minutes for driver, 45 minutes for disk firmware).**</span></span>

[!INCLUDE [storsimple-install-update-option1](../../includes/storsimple-install-update-option1.md)]

## <a name="option-2-use-the-azure-classic-portal-to-apply-update-12-after-removing-the-gateway-configuration"></a><span data-ttu-id="68396-187">選項 2：在移除閘道器組態之後使用 Azure 傳統入口網站套用 Update 1.2</span><span class="sxs-lookup"><span data-stu-id="68396-187">Option 2: Use the Azure classic portal to apply Update 1.2 after removing the gateway configuration</span></span>
<span data-ttu-id="68396-188">此程序僅適用於執行 Update 1 之前軟體版本，並在 DATA 0 以外的網路介面上設定閘道器的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="68396-188">This procedure applies only to StorSimple devices that are running a software version prior to Update 1 and have a gateway set on a network interface other than DATA 0.</span></span> <span data-ttu-id="68396-189">您必須在套用更新之前清除閘道器設定。</span><span class="sxs-lookup"><span data-stu-id="68396-189">You will need to clear the gateway setting prior to applying the update.</span></span>

<span data-ttu-id="68396-190">更新可能需要花幾個小時才能完成。</span><span class="sxs-lookup"><span data-stu-id="68396-190">The update may take a few hours to complete.</span></span> <span data-ttu-id="68396-191">如果您的主機位於不同的子網路，移除 iSCSI 介面上的閘道器設定可能會導致停機。</span><span class="sxs-lookup"><span data-stu-id="68396-191">If your hosts are in different subnets, removing the gateway configuration on the iSCSI interfaces could result in downtime.</span></span> <span data-ttu-id="68396-192">建議您為 iSCSI 流量設定 DATA 0，以減少停機。</span><span class="sxs-lookup"><span data-stu-id="68396-192">We recommend that you configure DATA 0 for iSCSI traffic to reduce the downtime.</span></span>

<span data-ttu-id="68396-193">執行下列步驟來透過閘道器停用網路介面，然後再套用更新。</span><span class="sxs-lookup"><span data-stu-id="68396-193">Perform the following steps to disable the network interface with the gateway and then apply the update.</span></span>

[!INCLUDE [storsimple-install-update-option2](../../includes/storsimple-install-update-option2.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a><span data-ttu-id="68396-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="68396-194">Next steps</span></span>
<span data-ttu-id="68396-195">深入了解 [Update 1.2 版](storsimple-update1-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="68396-195">Learn more about the [Update 1.2 release](storsimple-update1-release-notes.md).</span></span>

