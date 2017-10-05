---
title: "更換 StorSimple 8000 系列裝置控制器 | Microsoft Docs"
description: "說明如何取下並更換 StorSimple 8000 系列裝置上的一個或兩個控制器模組。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 849eccff114c2fd6d952e44d095d0cc89a238675
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-controller-module-on-your-storsimple-device"></a><span data-ttu-id="efcba-103">更換 StorSimple 裝置上的控制器模組</span><span class="sxs-lookup"><span data-stu-id="efcba-103">Replace a controller module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="efcba-104">概觀</span><span class="sxs-lookup"><span data-stu-id="efcba-104">Overview</span></span>
<span data-ttu-id="efcba-105">本教學課程說明如何取下並更換 StorSimple 裝置中的一個或兩個控制器模組。</span><span class="sxs-lookup"><span data-stu-id="efcba-105">This tutorial explains how to remove and replace one or both controller modules in a StorSimple device.</span></span> <span data-ttu-id="efcba-106">它也會討論單一和雙重控制器更換案例的基礎邏輯。</span><span class="sxs-lookup"><span data-stu-id="efcba-106">It also discusses the underlying logic for the single and dual controller replacement scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="efcba-107">在執行控制器更換之前，我們建議您一律將控制器韌體更新至最新版本。</span><span class="sxs-lookup"><span data-stu-id="efcba-107">Prior to performing a controller replacement, we recommend that you always update your controller firmware to the latest version.</span></span>
> 
> <span data-ttu-id="efcba-108">若要避免損害您的 StorSimple 裝置，請勿退出控制器，直到 LED 顯示成下列其中一個：</span><span class="sxs-lookup"><span data-stu-id="efcba-108">To prevent damage to your StorSimple device, do not eject the controller until the LEDs are showing as one of the following:</span></span>
> 
> * <span data-ttu-id="efcba-109">所有燈都已關閉。</span><span class="sxs-lookup"><span data-stu-id="efcba-109">All lights are OFF.</span></span>
> * <span data-ttu-id="efcba-110">LED 3、![綠色勾號圖示](./media/storsimple-controller-replacement/HCS_GreenCheckIcon.png)和![紅色叉號圖示](./media/storsimple-controller-replacement/HCS_RedCrossIcon.png)是閃爍，而 LED 0 和 LED 7 是**開啟**。</span><span class="sxs-lookup"><span data-stu-id="efcba-110">LED 3, ![Green check icon](./media/storsimple-controller-replacement/HCS_GreenCheckIcon.png), and ![Red cross icon](./media/storsimple-controller-replacement/HCS_RedCrossIcon.png) are flashing, and LED 0 and LED 7 are **ON**.</span></span>


<span data-ttu-id="efcba-111">下表顯示支援的控制器更換案例。</span><span class="sxs-lookup"><span data-stu-id="efcba-111">The following table shows the supported controller replacement scenarios.</span></span>

| <span data-ttu-id="efcba-112">案例</span><span class="sxs-lookup"><span data-stu-id="efcba-112">Case</span></span> | <span data-ttu-id="efcba-113">更換案例</span><span class="sxs-lookup"><span data-stu-id="efcba-113">Replacement scenario</span></span> | <span data-ttu-id="efcba-114">適用程序</span><span class="sxs-lookup"><span data-stu-id="efcba-114">Applicable procedure</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="efcba-115">1</span><span class="sxs-lookup"><span data-stu-id="efcba-115">1</span></span> |<span data-ttu-id="efcba-116">一個控制器處於故障狀態，而另一個控制器為狀況良好並作用中。</span><span class="sxs-lookup"><span data-stu-id="efcba-116">One controller is in a failed state, the other controller is healthy and active.</span></span> |<span data-ttu-id="efcba-117">[單一控制器更換](#replace-a-single-controller)，其中描述[單一控制器更換背後的邏輯](#single-controller-replacement-logic)，以及[更換步驟](#single-controller-replacement-steps)。</span><span class="sxs-lookup"><span data-stu-id="efcba-117">[Single controller replacement](#replace-a-single-controller), which describes the [logic behind a single controller replacement](#single-controller-replacement-logic), as well as the [replacement steps](#single-controller-replacement-steps).</span></span> |
| <span data-ttu-id="efcba-118">2</span><span class="sxs-lookup"><span data-stu-id="efcba-118">2</span></span> |<span data-ttu-id="efcba-119">兩個控制器都故障，而且需要更換。</span><span class="sxs-lookup"><span data-stu-id="efcba-119">Both the controllers have failed and require replacement.</span></span> <span data-ttu-id="efcba-120">底座、磁碟和磁碟機箱的狀況良好。</span><span class="sxs-lookup"><span data-stu-id="efcba-120">The chassis, disks, and disk enclosure are healthy.</span></span> |<span data-ttu-id="efcba-121">[雙重控制器更換](#replace-both-controllers)，其中描述[雙重控制器更換背後的邏輯](#dual-controller-replacement-logic)，以及[更換步驟](#dual-controller-replacement-steps)。</span><span class="sxs-lookup"><span data-stu-id="efcba-121">[Dual controller replacement](#replace-both-controllers), which describes the [logic behind a dual controller replacement](#dual-controller-replacement-logic), as well as the [replacement steps](#dual-controller-replacement-steps).</span></span> |
| <span data-ttu-id="efcba-122">3</span><span class="sxs-lookup"><span data-stu-id="efcba-122">3</span></span> |<span data-ttu-id="efcba-123">交換來自相同裝置或來自不同裝置的控制器。</span><span class="sxs-lookup"><span data-stu-id="efcba-123">Controllers from the same device or from different devices are swapped.</span></span> <span data-ttu-id="efcba-124">底座、磁碟和磁碟機箱的狀況良好。</span><span class="sxs-lookup"><span data-stu-id="efcba-124">The chassis, disks, and disk enclosures are healthy.</span></span> |<span data-ttu-id="efcba-125">插槽不符警示訊息將出現。</span><span class="sxs-lookup"><span data-stu-id="efcba-125">A slot mismatch alert message will appear.</span></span> |
| <span data-ttu-id="efcba-126">4</span><span class="sxs-lookup"><span data-stu-id="efcba-126">4</span></span> |<span data-ttu-id="efcba-127">遺漏一個控制器，而另一個控制器故障。</span><span class="sxs-lookup"><span data-stu-id="efcba-127">One controller is missing and the other controller fails.</span></span> |<span data-ttu-id="efcba-128">[雙重控制器更換](#replace-both-controllers)，其中描述[雙重控制器更換背後的邏輯](#dual-controller-replacement-logic)，以及[更換步驟](#dual-controller-replacement-steps)。</span><span class="sxs-lookup"><span data-stu-id="efcba-128">[Dual controller replacement](#replace-both-controllers), which describes the [logic behind a dual controller replacement](#dual-controller-replacement-logic), as well as the [replacement steps](#dual-controller-replacement-steps).</span></span> |
| <span data-ttu-id="efcba-129">5</span><span class="sxs-lookup"><span data-stu-id="efcba-129">5</span></span> |<span data-ttu-id="efcba-130">一個或兩個控制器故障。</span><span class="sxs-lookup"><span data-stu-id="efcba-130">One or both controllers have failed.</span></span> <span data-ttu-id="efcba-131">您無法透過序列主控台或 Windows PowerShell 遠端存取裝置。</span><span class="sxs-lookup"><span data-stu-id="efcba-131">You cannot access the device through the serial console or Windows PowerShell remoting.</span></span> |<span data-ttu-id="efcba-132">[連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md) 。</span><span class="sxs-lookup"><span data-stu-id="efcba-132">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) for a manual controller replacement procedure.</span></span> |
| <span data-ttu-id="efcba-133">6</span><span class="sxs-lookup"><span data-stu-id="efcba-133">6</span></span> |<span data-ttu-id="efcba-134">控制器有不同的組建版本，原因可能是︰</span><span class="sxs-lookup"><span data-stu-id="efcba-134">The controllers have a different build version, which may be due to:</span></span><ul><li><span data-ttu-id="efcba-135">控制器有不同的軟體版本。</span><span class="sxs-lookup"><span data-stu-id="efcba-135">Controllers have a different software version.</span></span></li><li><span data-ttu-id="efcba-136">控制器有不同的韌體版本。</span><span class="sxs-lookup"><span data-stu-id="efcba-136">Controllers have a different firmware version.</span></span></li></ul> |<span data-ttu-id="efcba-137">如果控制器軟體版本不同，更換邏輯會偵測到並更新更換控制器上的軟體版本。</span><span class="sxs-lookup"><span data-stu-id="efcba-137">If the controller software versions are different, the replacement logic detects that and updates the software version on the replacement controller.</span></span><br><br><span data-ttu-id="efcba-138">如果控制器軔體版本不同，而且舊的韌體版本**無法**自動升級，則 Azure 入口網站中會出現警示訊息。</span><span class="sxs-lookup"><span data-stu-id="efcba-138">If the controller firmware versions are different and the old firmware version is **not** automatically upgradeable, an alert message will appear in the Azure portal.</span></span> <span data-ttu-id="efcba-139">您應掃描更新並安裝韌體更新。</span><span class="sxs-lookup"><span data-stu-id="efcba-139">You should scan for updates and install the firmware updates.</span></span></br></br><span data-ttu-id="efcba-140">如果控制器軔體版本不同，而且舊的韌體版本可以自動升級，控制器更換邏輯會偵測到此情況，並且在控制器啟動之後，軔體將會自動更新。</span><span class="sxs-lookup"><span data-stu-id="efcba-140">If the controller firmware versions are different and the old firmware version is automatically upgradeable, the controller replacement logic will detect this, and after the controller starts, the firmware will be automatically updated.</span></span> |

<span data-ttu-id="efcba-141">您需要取下故障的控制器模組。</span><span class="sxs-lookup"><span data-stu-id="efcba-141">You need to remove a controller module if it has failed.</span></span> <span data-ttu-id="efcba-142">一或兩個控制器模組可能故障，這會導致單一控制器更換或雙重控制器更換。</span><span class="sxs-lookup"><span data-stu-id="efcba-142">One or both the controller modules can fail, which can result in a single controller replacement or dual controller replacement.</span></span> <span data-ttu-id="efcba-143">如需更換程序和其背後邏輯的資訊，請參閱以下各項：</span><span class="sxs-lookup"><span data-stu-id="efcba-143">For replacement procedures and the logic behind them, see the following:</span></span>

* [<span data-ttu-id="efcba-144">更換單一控制器</span><span class="sxs-lookup"><span data-stu-id="efcba-144">Replace a single controller</span></span>](#replace-a-single-controller)
* [<span data-ttu-id="efcba-145">更換兩個控制器</span><span class="sxs-lookup"><span data-stu-id="efcba-145">Replace both controllers</span></span>](#replace-both-controllers)
* [<span data-ttu-id="efcba-146">取下控制器</span><span class="sxs-lookup"><span data-stu-id="efcba-146">Remove a controller</span></span>](#remove-a-controller)
* [<span data-ttu-id="efcba-147">插入控制器</span><span class="sxs-lookup"><span data-stu-id="efcba-147">Insert a controller</span></span>](#insert-a-controller)
* [<span data-ttu-id="efcba-148">識別您裝置上的作用中控制器</span><span class="sxs-lookup"><span data-stu-id="efcba-148">Identify the active controller on your device</span></span>](#identify-the-active-controller-on-your-device)

> [!IMPORTANT]
> <span data-ttu-id="efcba-149">取下及更換控制器之前，請閱讀 [StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)中的安全資訊。</span><span class="sxs-lookup"><span data-stu-id="efcba-149">Before removing and replacing a controller, review the safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="replace-a-single-controller"></a><span data-ttu-id="efcba-150">更換單一控制器</span><span class="sxs-lookup"><span data-stu-id="efcba-150">Replace a single controller</span></span>
<span data-ttu-id="efcba-151">當 Microsoft Azure StorSimple 裝置上的兩個控制器之一故障、無法運作或遺漏時，您必須更換單一控制器。</span><span class="sxs-lookup"><span data-stu-id="efcba-151">When one of the two controllers on the Microsoft Azure StorSimple device has failed, is malfunctioning, or is missing, you need to replace a single controller.</span></span>

### <a name="single-controller-replacement-logic"></a><span data-ttu-id="efcba-152">單一控制器更換邏輯</span><span class="sxs-lookup"><span data-stu-id="efcba-152">Single controller replacement logic</span></span>
<span data-ttu-id="efcba-153">在單一控制器更換中，您應該先取下故障的控制器。</span><span class="sxs-lookup"><span data-stu-id="efcba-153">In a single controller replacement, you should first remove the failed controller.</span></span> <span data-ttu-id="efcba-154">(裝置中剩餘的控制器是作用中控制器)。當插入更換控制器時，會發生下列動作：</span><span class="sxs-lookup"><span data-stu-id="efcba-154">(The remaining controller in the device is the active controller.) When you insert the replacement controller, the following actions occur:</span></span>

1. <span data-ttu-id="efcba-155">更換控制器立即開始與 StorSimple 裝置進行通訊。</span><span class="sxs-lookup"><span data-stu-id="efcba-155">The replacement controller immediately starts communicating with the StorSimple device.</span></span>
2. <span data-ttu-id="efcba-156">作用中控制器的虛擬硬碟 (VHD) 快照會複製在更換控制器上。</span><span class="sxs-lookup"><span data-stu-id="efcba-156">A snapshot of the virtual hard disk (VHD) for the active controller is copied on the replacement controller.</span></span>
3. <span data-ttu-id="efcba-157">會修改快照，以便當更換控制器從這個 VHD 啟動時，系統會將它會辨識為待命控制器。</span><span class="sxs-lookup"><span data-stu-id="efcba-157">The snapshot is modified so that when the replacement controller starts from this VHD, it will be recognized as a standby controller.</span></span>
4. <span data-ttu-id="efcba-158">完成修改後，更換控制器將啟動為待命控制器。</span><span class="sxs-lookup"><span data-stu-id="efcba-158">When the modifications are complete, the replacement controller will start as the standby controller.</span></span>
5. <span data-ttu-id="efcba-159">兩個控制器同時執行時，叢集就會恢復上線。</span><span class="sxs-lookup"><span data-stu-id="efcba-159">When both the controllers are running, the cluster comes online.</span></span>

### <a name="single-controller-replacement-steps"></a><span data-ttu-id="efcba-160">單一控制器更換步驟</span><span class="sxs-lookup"><span data-stu-id="efcba-160">Single controller replacement steps</span></span>
<span data-ttu-id="efcba-161">如果 Microsoft Azure StorSimple 裝置的其中一個控制器故障，請完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="efcba-161">Complete the following steps if one of the controllers in your Microsoft Azure StorSimple device fails.</span></span> <span data-ttu-id="efcba-162">(另一個控制器必須作用中並執行中。</span><span class="sxs-lookup"><span data-stu-id="efcba-162">(The other controller must be active and running.</span></span> <span data-ttu-id="efcba-163">如果兩個控制器都故障或無法運作，請移至 [雙重控制器更換步驟](#dual-controller-replacement-steps))。</span><span class="sxs-lookup"><span data-stu-id="efcba-163">If both controllers fail or malfunction, go to [dual controller replacement steps](#dual-controller-replacement-steps).)</span></span>

> [!NOTE]
> <span data-ttu-id="efcba-164">可能需要 30 – 45 分鐘，控制器才會重新啟動，並從單一控制器更換程序完全復原。</span><span class="sxs-lookup"><span data-stu-id="efcba-164">It can take 30 – 45 minutes for the controller to restart and completely recover from the single controller replacement procedure.</span></span> <span data-ttu-id="efcba-165">整個程序的時間總計 (包括接上纜線) 大約 2 小時。</span><span class="sxs-lookup"><span data-stu-id="efcba-165">The total time for the entire procedure, including attaching the cables, is approximately 2 hours.</span></span>


#### <a name="to-remove-a-single-failed-controller-module"></a><span data-ttu-id="efcba-166">若要取下單一故障的控制器模組</span><span class="sxs-lookup"><span data-stu-id="efcba-166">To remove a single failed controller module</span></span>
1. <span data-ttu-id="efcba-167">在 Azure 入口網站中，移至 StorSimple 裝置管理員服務，按一下 [裝置]，然後按一下您想要監視的裝置名稱。</span><span class="sxs-lookup"><span data-stu-id="efcba-167">In the Azure portal, go to the StorSimple Device Manager service, click **Devices**, and then click the name of the device that you want to monitor.</span></span>
2. <span data-ttu-id="efcba-168">移至 [監視] > [硬體健康狀態]。</span><span class="sxs-lookup"><span data-stu-id="efcba-168">Go to **Monitor > Hardware health**.</span></span> <span data-ttu-id="efcba-169">控制器 0 或控制器 1 的狀態應該是紅色，表示故障。</span><span class="sxs-lookup"><span data-stu-id="efcba-169">The status of either Controller 0 or Controller 1 should be red, which indicates a failure.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="efcba-170">單一控制器更換中的故障控制器一律為待命控制器。</span><span class="sxs-lookup"><span data-stu-id="efcba-170">The failed controller in a single controller replacement is always a standby controller.</span></span>
   
3. <span data-ttu-id="efcba-171">使用圖 1 和下表來找出故障的控制器模組。</span><span class="sxs-lookup"><span data-stu-id="efcba-171">Use Figure 1 and the following table to locate the failed controller module.</span></span>
   
    ![裝置主要機箱模組的後擋板](./media/storsimple-controller-replacement/IC740994.png)
   
    <span data-ttu-id="efcba-173">**圖 1** StorSimple 裝置的背面</span><span class="sxs-lookup"><span data-stu-id="efcba-173">**Figure 1** Back of StorSimple device</span></span>
   
   | <span data-ttu-id="efcba-174">標籤</span><span class="sxs-lookup"><span data-stu-id="efcba-174">Label</span></span> | <span data-ttu-id="efcba-175">說明</span><span class="sxs-lookup"><span data-stu-id="efcba-175">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="efcba-176">1</span><span class="sxs-lookup"><span data-stu-id="efcba-176">1</span></span> |<span data-ttu-id="efcba-177">PCM 0</span><span class="sxs-lookup"><span data-stu-id="efcba-177">PCM 0</span></span> |
   | <span data-ttu-id="efcba-178">2</span><span class="sxs-lookup"><span data-stu-id="efcba-178">2</span></span> |<span data-ttu-id="efcba-179">PCM 1</span><span class="sxs-lookup"><span data-stu-id="efcba-179">PCM 1</span></span> |
   | <span data-ttu-id="efcba-180">3</span><span class="sxs-lookup"><span data-stu-id="efcba-180">3</span></span> |<span data-ttu-id="efcba-181">控制器 0</span><span class="sxs-lookup"><span data-stu-id="efcba-181">Controller 0</span></span> |
   | <span data-ttu-id="efcba-182">4</span><span class="sxs-lookup"><span data-stu-id="efcba-182">4</span></span> |<span data-ttu-id="efcba-183">控制器 1</span><span class="sxs-lookup"><span data-stu-id="efcba-183">Controller 1</span></span> |
4. <span data-ttu-id="efcba-184">在故障的控制器上，從資料連接埠取下所有已連接的網路纜線。</span><span class="sxs-lookup"><span data-stu-id="efcba-184">On the failed controller, remove all the connected network cables from the data ports.</span></span> <span data-ttu-id="efcba-185">如果您是使用 8600 機型，也請取下將控制器連接至 EBOD 控制器的SAS 纜線。</span><span class="sxs-lookup"><span data-stu-id="efcba-185">If you are using an 8600 model, also remove the SAS cables that connect the controller to the EBOD controller.</span></span>
5. <span data-ttu-id="efcba-186">依照[取下控制器](#remove-a-controller)中的步驟，取下故障的控制器。</span><span class="sxs-lookup"><span data-stu-id="efcba-186">Follow the steps in [remove a controller](#remove-a-controller) to remove the failed controller.</span></span>
6. <span data-ttu-id="efcba-187">在取下故障控制器的同一插槽中安裝原廠更換品。</span><span class="sxs-lookup"><span data-stu-id="efcba-187">Install the factory replacement in the same slot from which the failed controller was removed.</span></span> <span data-ttu-id="efcba-188">這樣會觸發單一控制器更換邏輯。</span><span class="sxs-lookup"><span data-stu-id="efcba-188">This triggers the single controller replacement logic.</span></span> <span data-ttu-id="efcba-189">如需詳細資訊，請參閱[單一控制器更換邏輯](#single-controller-replacement-logic)。</span><span class="sxs-lookup"><span data-stu-id="efcba-189">For more information, see [single controller replacement logic](#single-controller-replacement-logic).</span></span>
7. <span data-ttu-id="efcba-190">當單一控制器更換邏輯在背景中進行時，請重新連接纜線。</span><span class="sxs-lookup"><span data-stu-id="efcba-190">While the single controller replacement logic progresses in the background, reconnect the cables.</span></span> <span data-ttu-id="efcba-191">請完全依照更換之前連接纜線的相同方式，小心地連接所有纜線。</span><span class="sxs-lookup"><span data-stu-id="efcba-191">Take care to connect all the cables exactly the same way that they were connected before the replacement.</span></span>
8. <span data-ttu-id="efcba-192">在控制器重新啟動之後，請檢查 Azure 入口網站中的 [控制器狀態] 和 [叢集狀態]，以確認控制器回到良好的狀態且處於待命模式。</span><span class="sxs-lookup"><span data-stu-id="efcba-192">After the controller restarts, check the **Controller status** and the **Cluster status** in the Azure portal to verify that the controller is back to a healthy state and is in standby mode.</span></span>

> [!NOTE]
> <span data-ttu-id="efcba-193">如果您是透過序列主控台監視裝置，則可能會在控制器從更換程序中復原時看到多次重新啟動。</span><span class="sxs-lookup"><span data-stu-id="efcba-193">If you are monitoring the device through the serial console, you may see multiple restarts while the controller is recovering from the replacement procedure.</span></span> <span data-ttu-id="efcba-194">當序列主控台功能表呈現時，您便知道更換已完成。</span><span class="sxs-lookup"><span data-stu-id="efcba-194">When the serial console menu is presented, then you know that the replacement is complete.</span></span> <span data-ttu-id="efcba-195">如果功能表未在啟動控制器更換的兩個小時內出現，請[連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="efcba-195">If the menu does not appear within two hours of starting the controller replacement, please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
>
> <span data-ttu-id="efcba-196">從 Update 4 開始，您也可以在裝置的 Windows PowerShell 介面中使用 Cmdlet `Get-HCSControllerReplacementStatus` 來監視控制器更換程序的狀態。</span><span class="sxs-lookup"><span data-stu-id="efcba-196">Starting Update 4, you can also use the cmdlet `Get-HCSControllerReplacementStatus` in the Windows PowerShell interface of the device to monitor the status of the controller replacement process.</span></span>
> 

## <a name="replace-both-controllers"></a><span data-ttu-id="efcba-197">更換兩個控制器</span><span class="sxs-lookup"><span data-stu-id="efcba-197">Replace both controllers</span></span>
<span data-ttu-id="efcba-198">當 Microsoft Azure StorSimple 裝置上的兩個控制器故障、無法運作或遺漏時，您必須更換兩個控制器。</span><span class="sxs-lookup"><span data-stu-id="efcba-198">When both controllers on the Microsoft Azure StorSimple device have failed, are malfunctioning, or are missing, you need to replace both controllers.</span></span> 

### <a name="dual-controller-replacement-logic"></a><span data-ttu-id="efcba-199">雙重控制器更換</span><span class="sxs-lookup"><span data-stu-id="efcba-199">Dual controller replacement logic</span></span>
<span data-ttu-id="efcba-200">在雙重控制器更換中，先移除兩個故障的控制器，再插入更換控制器。</span><span class="sxs-lookup"><span data-stu-id="efcba-200">In a dual controller replacement, you first remove both failed controllers and then insert replacements.</span></span> <span data-ttu-id="efcba-201">當插入兩個更換控制器時，會發生下列動作：</span><span class="sxs-lookup"><span data-stu-id="efcba-201">When the two replacement controllers are inserted, the following actions occur:</span></span>

1. <span data-ttu-id="efcba-202">插槽 0 中的更換控制器會檢查下列情況：</span><span class="sxs-lookup"><span data-stu-id="efcba-202">The replacement controller in slot 0 checks the following:</span></span>
   
   1. <span data-ttu-id="efcba-203">它是否使用目前版本的韌體和軟體？</span><span class="sxs-lookup"><span data-stu-id="efcba-203">Is it using current versions of the firmware and software?</span></span>
   2. <span data-ttu-id="efcba-204">它是否為叢集的一部分？</span><span class="sxs-lookup"><span data-stu-id="efcba-204">Is it a part of the cluster?</span></span>
   3. <span data-ttu-id="efcba-205">對等控制器是否執行中並構成叢集？</span><span class="sxs-lookup"><span data-stu-id="efcba-205">Is the peer controller running and is it clustered?</span></span>
      
      <span data-ttu-id="efcba-206">如果上述狀況無一成立，則控制器會尋找最新的每日備份 (位於磁碟機 S 上的 **nonDOMstorage** )。</span><span class="sxs-lookup"><span data-stu-id="efcba-206">If none of these conditions are true, the controller looks for the latest daily backup (located in the **nonDOMstorage** on drive S).</span></span> <span data-ttu-id="efcba-207">控制器會從備份複製 VHD 的最新快照。</span><span class="sxs-lookup"><span data-stu-id="efcba-207">The controller copies the latest snapshot of the VHD from the backup.</span></span>
2. <span data-ttu-id="efcba-208">在位置 0 的控制站會使用快照集映像本身。</span><span class="sxs-lookup"><span data-stu-id="efcba-208">The controller in slot 0 uses the snapshot to image itself.</span></span>
3. <span data-ttu-id="efcba-209">同時，插槽 1 中的控制器會等到控制器 0 完成映像和啟動。</span><span class="sxs-lookup"><span data-stu-id="efcba-209">Meanwhile, the controller in slot 1 waits for controller 0 to complete the imaging and start.</span></span>
4. <span data-ttu-id="efcba-210">在控制器 0 啟動之後，控制器 1 會偵測到控制器 0 所建立的叢集，這會觸發單一控制器更換邏輯。</span><span class="sxs-lookup"><span data-stu-id="efcba-210">After controller 0 starts, controller 1 detects the cluster created by controller 0, which triggers the single controller replacement logic.</span></span> <span data-ttu-id="efcba-211">如需詳細資訊，請參閱 [單一控制器更換邏輯](#single-controller-replacement-logic)。</span><span class="sxs-lookup"><span data-stu-id="efcba-211">For more information, see [single controller replacement logic](#single-controller-replacement-logic).</span></span>
5. <span data-ttu-id="efcba-212">之後，兩個兩個控制器將執行中，而且叢集將恢復上線。</span><span class="sxs-lookup"><span data-stu-id="efcba-212">Afterwards, both controllers will be running and the cluster will come online.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efcba-213">在雙重控制器更換後，於設定 StorSimple 裝置之後，務必進行裝置的手動備份。</span><span class="sxs-lookup"><span data-stu-id="efcba-213">Following a dual controller replacement, after the StorSimple device is configured, it is essential that you take a manual backup of the device.</span></span> <span data-ttu-id="efcba-214">直到過了 24 小時之後，才會觸發每日裝置組態備份。</span><span class="sxs-lookup"><span data-stu-id="efcba-214">Daily device configuration backups are not triggered until after 24 hours have elapsed.</span></span> <span data-ttu-id="efcba-215">與 [Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md) 合作，進行裝置的手動備份。</span><span class="sxs-lookup"><span data-stu-id="efcba-215">Work with [Microsoft Support](storsimple-8000-contact-microsoft-support.md) to make a manual backup of your device.</span></span>


### <a name="dual-controller-replacement-steps"></a><span data-ttu-id="efcba-216">雙重控制器更換步驟</span><span class="sxs-lookup"><span data-stu-id="efcba-216">Dual controller replacement steps</span></span>
<span data-ttu-id="efcba-217">當 Microsoft Azure StorSimple 裝置中的兩個控制器都故障時，需要這個工作流程。</span><span class="sxs-lookup"><span data-stu-id="efcba-217">This workflow is required when both of the controllers in your Microsoft Azure StorSimple device have failed.</span></span> <span data-ttu-id="efcba-218">這可能會發生在冷卻系統停止運作的資料中心，因此兩個控制器會在短時間內故障。</span><span class="sxs-lookup"><span data-stu-id="efcba-218">This could happen in a datacenter in which the cooling system stops working, and as a result, both the controllers fail within a short period of time.</span></span> <span data-ttu-id="efcba-219">視 StorSimple 裝置是關閉還是開啟，以及您使用的是 8600 還是 8100 機型而定，會需要一組不同的步驟。</span><span class="sxs-lookup"><span data-stu-id="efcba-219">Depending on whether the StorSimple device is turned off or on, and whether you are using an 8600 or an 8100 model, a different set of steps is required.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efcba-220">可能需要 45 分鐘到 1 小時，控制器才會重新啟動，並從雙重控制器更換程序完全復原。</span><span class="sxs-lookup"><span data-stu-id="efcba-220">It can take 45 minutes to 1 hour for the controller to restart and completely recover from a dual controller replacement procedure.</span></span> <span data-ttu-id="efcba-221">整個程序的時間總計 (包括接上纜線) 大約 2.5 小時。</span><span class="sxs-lookup"><span data-stu-id="efcba-221">The total time for the entire procedure, including attaching the cables, is approximately 2.5 hours.</span></span>

#### <a name="to-replace-both-controller-modules"></a><span data-ttu-id="efcba-222">若要取下兩個控制器模組</span><span class="sxs-lookup"><span data-stu-id="efcba-222">To replace both controller modules</span></span>
1. <span data-ttu-id="efcba-223">如果裝置已關閉，請略過此步驟並繼續進行下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="efcba-223">If the device is turned off, skip this step and proceed to the next step.</span></span> <span data-ttu-id="efcba-224">如果裝置已開啟，請關閉裝置。</span><span class="sxs-lookup"><span data-stu-id="efcba-224">If the device is turned on, turn off the device.</span></span>
   
   1. <span data-ttu-id="efcba-225">如果您使用的是 8600 機型，請先關閉主要機箱，然後再關閉 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="efcba-225">If you are using an 8600 model, turn off the primary enclosure first, and then turn off the EBOD enclosure.</span></span>
   2. <span data-ttu-id="efcba-226">等到裝置完全關閉。</span><span class="sxs-lookup"><span data-stu-id="efcba-226">Wait until the device has shut down completely.</span></span> <span data-ttu-id="efcba-227">裝置背面的所有 LED 都將關閉。</span><span class="sxs-lookup"><span data-stu-id="efcba-227">All the LEDs in the back of the device will be off.</span></span>
2. <span data-ttu-id="efcba-228">取下所有已連接至資料連接埠的網路纜線。</span><span class="sxs-lookup"><span data-stu-id="efcba-228">Remove all the network cables that are connected to the data ports.</span></span> <span data-ttu-id="efcba-229">如果您使用的是 8600 機型，請一併取下將主要機箱連接至 EBOD 機箱的 SAS 纜線。</span><span class="sxs-lookup"><span data-stu-id="efcba-229">If you are using an 8600 model, also remove the SAS cables that connect the primary enclosure to the EBOD enclosure.</span></span>
3. <span data-ttu-id="efcba-230">從 StorSimple 裝置取下兩個控制器。</span><span class="sxs-lookup"><span data-stu-id="efcba-230">Remove both controllers from the StorSimple device.</span></span> <span data-ttu-id="efcba-231">如需詳細資訊，請參閱[取下控制器](#remove-a-controller)。</span><span class="sxs-lookup"><span data-stu-id="efcba-231">For more information, see [remove a controller](#remove-a-controller).</span></span>
4. <span data-ttu-id="efcba-232">首先插入控制器 0 的原廠更換品，再插入控制器 1。</span><span class="sxs-lookup"><span data-stu-id="efcba-232">Insert the factory replacement for Controller 0 first, and then insert Controller 1.</span></span> <span data-ttu-id="efcba-233">如需詳細資訊，請參閱[插入控制器](#insert-a-controller)。</span><span class="sxs-lookup"><span data-stu-id="efcba-233">For more information, see [insert a controller](#insert-a-controller).</span></span> <span data-ttu-id="efcba-234">這樣會觸發雙重控制器更換邏輯。</span><span class="sxs-lookup"><span data-stu-id="efcba-234">This triggers the dual controller replacement logic.</span></span> <span data-ttu-id="efcba-235">如需詳細資訊，請參閱[雙重控制器更換邏輯](#dual-controller-replacement-logic)。</span><span class="sxs-lookup"><span data-stu-id="efcba-235">For more information, see [dual controller replacement logic](#dual-controller-replacement-logic).</span></span>
5. <span data-ttu-id="efcba-236">當雙重控制器更換邏輯在背景中進行時，請重新連接纜線。</span><span class="sxs-lookup"><span data-stu-id="efcba-236">While the controller replacement logic progresses in the background, reconnect the cables.</span></span> <span data-ttu-id="efcba-237">請完全依照更換之前連接纜線的相同方式，小心地連接所有纜線。</span><span class="sxs-lookup"><span data-stu-id="efcba-237">Take care to connect all the cables exactly the same way that they were connected before the replacement.</span></span> <span data-ttu-id="efcba-238">請參閱[安裝 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md)或[安裝 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md)的＜佈線您的裝置＞一節中，您機型適用的詳細指示。</span><span class="sxs-lookup"><span data-stu-id="efcba-238">See the detailed instructions for your model in the Cable your device section of [install your StorSimple 8100 device](storsimple-8100-hardware-installation.md) or [install your StorSimple 8600 device](storsimple-8600-hardware-installation.md).</span></span>
6. <span data-ttu-id="efcba-239">開啟 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="efcba-239">Turn on the StorSimple device.</span></span> <span data-ttu-id="efcba-240">如果您使用的是 8600 機型：</span><span class="sxs-lookup"><span data-stu-id="efcba-240">If you are using an 8600 model:</span></span>
   
   1. <span data-ttu-id="efcba-241">確定首先開啟 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="efcba-241">Make sure that the EBOD enclosure is turned on first.</span></span>
   2. <span data-ttu-id="efcba-242">等到 EBOD 機箱執行。</span><span class="sxs-lookup"><span data-stu-id="efcba-242">Wait until the EBOD enclosure is running.</span></span>
   3. <span data-ttu-id="efcba-243">開啟主要機箱。</span><span class="sxs-lookup"><span data-stu-id="efcba-243">Turn on the primary enclosure.</span></span>
   4. <span data-ttu-id="efcba-244">在第一個控制器重新啟動並處於狀況良好的狀態之後，系統就會執行。</span><span class="sxs-lookup"><span data-stu-id="efcba-244">After the first controller restarts and is in a healthy state, the system will be running.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="efcba-245">如果您是透過序列主控台監視裝置，則可能會在控制器從更換程序中復原時看到多次重新啟動。</span><span class="sxs-lookup"><span data-stu-id="efcba-245">If you are monitoring the device through the serial console, you may see multiple restarts while the controller is recovering from the replacement procedure.</span></span> <span data-ttu-id="efcba-246">當序列主控台功能表出現時，您便知道更換已完成。</span><span class="sxs-lookup"><span data-stu-id="efcba-246">When the serial console menu appears, then you know that the replacement is complete.</span></span> <span data-ttu-id="efcba-247">如果功能表未在啟動控制器更換的 2.5 個小時內出現，請[連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="efcba-247">If the menu does not appear within 2.5 hours of starting the controller replacement, please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
     
## <a name="remove-a-controller"></a><span data-ttu-id="efcba-248">取下控制器</span><span class="sxs-lookup"><span data-stu-id="efcba-248">Remove a controller</span></span>
<span data-ttu-id="efcba-249">請使用下列程序，從 StorSimple 裝置中取下故障的控制器模組。</span><span class="sxs-lookup"><span data-stu-id="efcba-249">Use the following procedure to remove a faulty controller module from your StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="efcba-250">下圖適用於控制器 0。</span><span class="sxs-lookup"><span data-stu-id="efcba-250">The following illustrations are for controller 0.</span></span> <span data-ttu-id="efcba-251">若為控制器 1，這些將相反。</span><span class="sxs-lookup"><span data-stu-id="efcba-251">For controller 1, these would be reversed.</span></span>


#### <a name="to-remove-a-controller-module"></a><span data-ttu-id="efcba-252">若要取下控制器模組</span><span class="sxs-lookup"><span data-stu-id="efcba-252">To remove a controller module</span></span>
1. <span data-ttu-id="efcba-253">以姆指與食指抓住模組閂鎖。</span><span class="sxs-lookup"><span data-stu-id="efcba-253">Grasp the module latch between your thumb and forefinger.</span></span>
2. <span data-ttu-id="efcba-254">輕輕擠壓姆指與食指，以鬆開控制器閂鎖。</span><span class="sxs-lookup"><span data-stu-id="efcba-254">Gently squeeze your thumb and forefinger together to release the controller latch.</span></span>
   
    ![鬆開控制器閂鎖](./media/storsimple-controller-replacement/IC741047.png)
   
    <span data-ttu-id="efcba-256">**圖 2** 鬆開控制器閂鎖</span><span class="sxs-lookup"><span data-stu-id="efcba-256">**Figure 2** Releasing controller latch</span></span>
3. <span data-ttu-id="efcba-257">請使用閂鎖做為把手，將控制器滑出底座。</span><span class="sxs-lookup"><span data-stu-id="efcba-257">Use the latch as a handle to slide the controller out of the chassis.</span></span>
   
    ![將控制器滑出底座](./media/storsimple-controller-replacement/IC741048.png)
   
    <span data-ttu-id="efcba-259">**圖 3** 將控制器滑出底座</span><span class="sxs-lookup"><span data-stu-id="efcba-259">**Figure 3** Sliding the controller out of the chassis</span></span>

## <a name="insert-a-controller"></a><span data-ttu-id="efcba-260">插入控制器</span><span class="sxs-lookup"><span data-stu-id="efcba-260">Insert a controller</span></span>
<span data-ttu-id="efcba-261">在您從 StorSimple 裝置取下故障模組之後，請使用下列程序來安裝原廠提供的控制器模組。</span><span class="sxs-lookup"><span data-stu-id="efcba-261">Use the following procedure to install a factory-supplied controller module after you remove a faulty module from your StorSimple device.</span></span>

#### <a name="to-install-a-controller-module"></a><span data-ttu-id="efcba-262">若要安裝控制器模組</span><span class="sxs-lookup"><span data-stu-id="efcba-262">To install a controller module</span></span>
1. <span data-ttu-id="efcba-263">查看介面連接器是否有任何損毀。</span><span class="sxs-lookup"><span data-stu-id="efcba-263">Check to see if there is any damage to the interface connectors.</span></span> <span data-ttu-id="efcba-264">如果有任一連接器接腳壞掉或彎曲，請勿安裝該模組。</span><span class="sxs-lookup"><span data-stu-id="efcba-264">Do not install the module if any of the connector pins are damaged or bent.</span></span>
2. <span data-ttu-id="efcba-265">當閂鎖完全鬆開時，請將控制器模組滑入底座。</span><span class="sxs-lookup"><span data-stu-id="efcba-265">Slide the controller module into the chassis while the latch is fully released.</span></span>
   
    ![將控制器滑入底座](./media/storsimple-controller-replacement/IC741053.png)
   
    <span data-ttu-id="efcba-267">**圖 4** 將控制器滑入底座</span><span class="sxs-lookup"><span data-stu-id="efcba-267">**Figure 4** Sliding controller into the chassis</span></span>
3. <span data-ttu-id="efcba-268">一旦插入控制器模組，請馬上關閉閂鎖，同時繼續將控制器模組推入底座。</span><span class="sxs-lookup"><span data-stu-id="efcba-268">With the controller module inserted, begin closing the latch while continuing to push the controller module into the chassis.</span></span> <span data-ttu-id="efcba-269">閂鎖將扣上，以將控制器固定位。</span><span class="sxs-lookup"><span data-stu-id="efcba-269">The latch will engage to guide the controller into place.</span></span>
   
    ![關閉控制器閂鎖](./media/storsimple-controller-replacement/IC741054.png)
   
    <span data-ttu-id="efcba-271">**圖 5** 關閉控制器閂鎖</span><span class="sxs-lookup"><span data-stu-id="efcba-271">**Figure 5** Closing the controller latch</span></span>
4. <span data-ttu-id="efcba-272">當閂鎖卡入定位時，即表示完成。</span><span class="sxs-lookup"><span data-stu-id="efcba-272">You're done when the latch snaps into place.</span></span> <span data-ttu-id="efcba-273">**正常** LED 現在應該亮起。</span><span class="sxs-lookup"><span data-stu-id="efcba-273">The **OK** LED should now be on.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="efcba-274">最多可能需要 5 分鐘，控制器和 LED 即會啟動。</span><span class="sxs-lookup"><span data-stu-id="efcba-274">It can take up to 5 minutes for the controller and the LED to activate.</span></span>
  
5. <span data-ttu-id="efcba-275">若要確認更換成功，請在 Azure 入口網站中，瀏覽至 [監視] > [硬體健康狀態]，並確定控制器 0 及控制器 1 兩者都狀況良好 (狀態為綠色)。</span><span class="sxs-lookup"><span data-stu-id="efcba-275">To verify that the replacement is successful, in the Azure portal, go to your device and then navigate to **Monitor** > **Hardware health**, and make sure that both controller 0 and controller 1 are healthy (status is green).</span></span>

## <a name="identify-the-active-controller-on-your-device"></a><span data-ttu-id="efcba-276">識別您裝置上的作用中控制器</span><span class="sxs-lookup"><span data-stu-id="efcba-276">Identify the active controller on your device</span></span>
<span data-ttu-id="efcba-277">有許多情況，例如第一次裝置註冊或控制器更換，會要求您在 StorSimple 裝置上找出作用中控制器。</span><span class="sxs-lookup"><span data-stu-id="efcba-277">There are many situations, such as first-time device registration or controller replacement, that require you to locate the active controller on a StorSimple device.</span></span> <span data-ttu-id="efcba-278">作用中控制器會處理所有磁碟韌體和網路作業。</span><span class="sxs-lookup"><span data-stu-id="efcba-278">The active controller processes all the disk firmware and networking operations.</span></span> <span data-ttu-id="efcba-279">您可以使用下列任一方法來識別作用中控制器：</span><span class="sxs-lookup"><span data-stu-id="efcba-279">You can use any of the following methods to identify the active controller:</span></span>

* [<span data-ttu-id="efcba-280">使用 Azure 入口網站來識別作用中控制器</span><span class="sxs-lookup"><span data-stu-id="efcba-280">Use the Azure portal to identify the active controller</span></span>](#use-the-azure-portal-to-identify-the-active-controller)
* [<span data-ttu-id="efcba-281">使用 Windows PowerShell for StorSimple 來識別作用中控制器</span><span class="sxs-lookup"><span data-stu-id="efcba-281">Use Windows PowerShell for StorSimple to identify the active controller</span></span>](#use-windows-powershell-for-storsimple-to-identify-the-active-controller)
* [<span data-ttu-id="efcba-282">檢查實體裝置來識別作用中控制器</span><span class="sxs-lookup"><span data-stu-id="efcba-282">Check the physical device to identify the active controller</span></span>](#check-the-physical-device-to-identify-the-active-controller)

<span data-ttu-id="efcba-283">接著說明上述各程序。</span><span class="sxs-lookup"><span data-stu-id="efcba-283">Each of these procedures is described next.</span></span>

### <a name="use-the-azure-portal-to-identify-the-active-controller"></a><span data-ttu-id="efcba-284">使用 Azure 入口網站來識別作用中控制器</span><span class="sxs-lookup"><span data-stu-id="efcba-284">Use the Azure portal to identify the active controller</span></span>
<span data-ttu-id="efcba-285">在 Azure 入口網站中，瀏覽至您的裝置，並移至 [監視] > [硬體健康狀態]，捲動至 [控制器]區段。</span><span class="sxs-lookup"><span data-stu-id="efcba-285">In the Azure portal, navigate to your device and then to **Monitor** > **Hardware health**, and scroll to the **Controllers** section.</span></span> <span data-ttu-id="efcba-286">在這裡您可以確認哪一個控制站作用中。</span><span class="sxs-lookup"><span data-stu-id="efcba-286">Here you can verify which controller is active.</span></span>

![識別 Azure 入口網站中的作用中控制器](./media/storsimple-controller-replacement/IC752072.png)

<span data-ttu-id="efcba-288">**圖 6** 顯示作用中控制器的 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="efcba-288">**Figure 6** Azure portal showing the active controller</span></span>

### <a name="use-windows-powershell-for-storsimple-to-identify-the-active-controller"></a><span data-ttu-id="efcba-289">使用 Windows PowerShell for StorSimple 來識別作用中控制器</span><span class="sxs-lookup"><span data-stu-id="efcba-289">Use Windows PowerShell for StorSimple to identify the active controller</span></span>
<span data-ttu-id="efcba-290">透過序列主控台存取您的裝置時，會呈現橫幅訊息。</span><span class="sxs-lookup"><span data-stu-id="efcba-290">When you access your device through the serial console, a banner message is presented.</span></span> <span data-ttu-id="efcba-291">橫幅訊息包含基本裝置資訊，例如：型號、名稱、已安裝的軟體版本、您要存取的控制器的狀態等。</span><span class="sxs-lookup"><span data-stu-id="efcba-291">The banner message contains basic device information such as the model, name, installed software version, and status of the controller you are accessing.</span></span> <span data-ttu-id="efcba-292">下圖顯示橫幅訊息的範例：</span><span class="sxs-lookup"><span data-stu-id="efcba-292">The following image shows an example of a banner message:</span></span>

![序列橫幅訊息](./media/storsimple-controller-replacement/IC741098.png)

<span data-ttu-id="efcba-294">**圖 7** 橫幅訊息將控制器 0 顯示為作用中</span><span class="sxs-lookup"><span data-stu-id="efcba-294">**Figure 7** Banner message showing controller 0 as Active</span></span>

<span data-ttu-id="efcba-295">您可以使用橫幅訊息，來判定您所連接的控制器是主動還是被動。</span><span class="sxs-lookup"><span data-stu-id="efcba-295">You can use the banner message to determine whether the controller you are connected to is active or passive.</span></span>

### <a name="check-the-physical-device-to-identify-the-active-controller"></a><span data-ttu-id="efcba-296">檢查實體裝置來識別作用中控制器</span><span class="sxs-lookup"><span data-stu-id="efcba-296">Check the physical device to identify the active controller</span></span>
<span data-ttu-id="efcba-297">若要識別裝置上的作用中控制器，請在主要機箱背面找出 DATA 5 連接埠上的藍色 LED。</span><span class="sxs-lookup"><span data-stu-id="efcba-297">To identify the active controller on your device, locate the blue LED above the DATA 5 port on the back of the primary enclosure.</span></span>

<span data-ttu-id="efcba-298">如果此 LED 閃爍，控制器是作用中，而且另一個控制器處於待命模式。</span><span class="sxs-lookup"><span data-stu-id="efcba-298">If this LED is blinking, the controller is active and the other controller is in standby mode.</span></span> <span data-ttu-id="efcba-299">使用下圖和下表來提供協助。</span><span class="sxs-lookup"><span data-stu-id="efcba-299">Use the following diagram and table as an aid.</span></span>

![包含資料連接埠的裝置主要機箱後擋板](./media/storsimple-controller-replacement/IC741055.png)

<span data-ttu-id="efcba-301">**圖 8** 具有資料連接埠和監視 LED 的主要機箱背面</span><span class="sxs-lookup"><span data-stu-id="efcba-301">**Figure 8** Back of primary enclosure with data ports and monitoring LEDs</span></span>

| <span data-ttu-id="efcba-302">標籤</span><span class="sxs-lookup"><span data-stu-id="efcba-302">Label</span></span> | <span data-ttu-id="efcba-303">說明</span><span class="sxs-lookup"><span data-stu-id="efcba-303">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="efcba-304">1-6</span><span class="sxs-lookup"><span data-stu-id="efcba-304">1-6</span></span> |<span data-ttu-id="efcba-305">DATA 0 – 5 個網路連接埠</span><span class="sxs-lookup"><span data-stu-id="efcba-305">DATA 0 – 5 network ports</span></span> |
| <span data-ttu-id="efcba-306">7</span><span class="sxs-lookup"><span data-stu-id="efcba-306">7</span></span> |<span data-ttu-id="efcba-307">藍色 LED</span><span class="sxs-lookup"><span data-stu-id="efcba-307">Blue LED</span></span> |

## <a name="next-steps"></a><span data-ttu-id="efcba-308">後續步驟</span><span class="sxs-lookup"><span data-stu-id="efcba-308">Next steps</span></span>
<span data-ttu-id="efcba-309">深入了解 [StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="efcba-309">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

