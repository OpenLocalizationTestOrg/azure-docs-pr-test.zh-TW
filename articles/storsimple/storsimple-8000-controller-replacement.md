---
title: "aaaReplace StorSimple 8000 系列裝置控制器 |Microsoft 文件"
description: "說明如何 tooremove 並取代您的 StorSimple 8000 系列裝置上的一個或兩個控制器模組。"
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
ms.openlocfilehash: 76d42529da42dff2a214fb840a52392a7f1a97ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-controller-module-on-your-storsimple-device"></a><span data-ttu-id="26552-103">更換 StorSimple 裝置上的控制器模組</span><span class="sxs-lookup"><span data-stu-id="26552-103">Replace a controller module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="26552-104">概觀</span><span class="sxs-lookup"><span data-stu-id="26552-104">Overview</span></span>
<span data-ttu-id="26552-105">本教學課程說明如何 tooremove 並取代在 StorSimple 裝置中的一個或兩個控制器模組。</span><span class="sxs-lookup"><span data-stu-id="26552-105">This tutorial explains how tooremove and replace one or both controller modules in a StorSimple device.</span></span> <span data-ttu-id="26552-106">它也會討論 hello 基礎邏輯 hello 單一和雙重控制器更換案例。</span><span class="sxs-lookup"><span data-stu-id="26552-106">It also discusses hello underlying logic for hello single and dual controller replacement scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="26552-107">Tooperforming 控制器更換之前，我們建議您一律更新您控制器韌體 toohello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="26552-107">Prior tooperforming a controller replacement, we recommend that you always update your controller firmware toohello latest version.</span></span>
> 
> <span data-ttu-id="26552-108">tooprevent 損壞 tooyour StorSimple 裝置，請勿退出 hello 控制站，直到 hello Led 顯示為 hello 下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="26552-108">tooprevent damage tooyour StorSimple device, do not eject hello controller until hello LEDs are showing as one of hello following:</span></span>
> 
> * <span data-ttu-id="26552-109">所有燈都已關閉。</span><span class="sxs-lookup"><span data-stu-id="26552-109">All lights are OFF.</span></span>
> * <span data-ttu-id="26552-110">LED 3、![綠色勾號圖示](./media/storsimple-controller-replacement/HCS_GreenCheckIcon.png)和![紅色叉號圖示](./media/storsimple-controller-replacement/HCS_RedCrossIcon.png)是閃爍，而 LED 0 和 LED 7 是**開啟**。</span><span class="sxs-lookup"><span data-stu-id="26552-110">LED 3, ![Green check icon](./media/storsimple-controller-replacement/HCS_GreenCheckIcon.png), and ![Red cross icon](./media/storsimple-controller-replacement/HCS_RedCrossIcon.png) are flashing, and LED 0 and LED 7 are **ON**.</span></span>


<span data-ttu-id="26552-111">hello 下表顯示支援的 hello 控制器更換案例。</span><span class="sxs-lookup"><span data-stu-id="26552-111">hello following table shows hello supported controller replacement scenarios.</span></span>

| <span data-ttu-id="26552-112">案例</span><span class="sxs-lookup"><span data-stu-id="26552-112">Case</span></span> | <span data-ttu-id="26552-113">更換案例</span><span class="sxs-lookup"><span data-stu-id="26552-113">Replacement scenario</span></span> | <span data-ttu-id="26552-114">適用程序</span><span class="sxs-lookup"><span data-stu-id="26552-114">Applicable procedure</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="26552-115">1</span><span class="sxs-lookup"><span data-stu-id="26552-115">1</span></span> |<span data-ttu-id="26552-116">一個控制器處於失敗狀態，hello 另一個控制器狀況良好，作用中。</span><span class="sxs-lookup"><span data-stu-id="26552-116">One controller is in a failed state, hello other controller is healthy and active.</span></span> |<span data-ttu-id="26552-117">[單一控制器更換](#replace-a-single-controller)，用來描述 hello[背後單一控制器更換邏輯](#single-controller-replacement-logic)，以及 hello[更換步驟](#single-controller-replacement-steps)。</span><span class="sxs-lookup"><span data-stu-id="26552-117">[Single controller replacement](#replace-a-single-controller), which describes hello [logic behind a single controller replacement](#single-controller-replacement-logic), as well as hello [replacement steps](#single-controller-replacement-steps).</span></span> |
| <span data-ttu-id="26552-118">2</span><span class="sxs-lookup"><span data-stu-id="26552-118">2</span></span> |<span data-ttu-id="26552-119">兩個 hello 控制器已失敗且需要更換。</span><span class="sxs-lookup"><span data-stu-id="26552-119">Both hello controllers have failed and require replacement.</span></span> <span data-ttu-id="26552-120">hello 底座、 磁碟和磁碟機箱均狀況良好。</span><span class="sxs-lookup"><span data-stu-id="26552-120">hello chassis, disks, and disk enclosure are healthy.</span></span> |<span data-ttu-id="26552-121">[更換雙重控制器時](#replace-both-controllers)，用來描述 hello[背後雙重控制器更換邏輯](#dual-controller-replacement-logic)，以及 hello[更換步驟](#dual-controller-replacement-steps)。</span><span class="sxs-lookup"><span data-stu-id="26552-121">[Dual controller replacement](#replace-both-controllers), which describes hello [logic behind a dual controller replacement](#dual-controller-replacement-logic), as well as hello [replacement steps](#dual-controller-replacement-steps).</span></span> |
| <span data-ttu-id="26552-122">3</span><span class="sxs-lookup"><span data-stu-id="26552-122">3</span></span> |<span data-ttu-id="26552-123">從控制器 hello 相同的裝置，或從不同裝置互換。</span><span class="sxs-lookup"><span data-stu-id="26552-123">Controllers from hello same device or from different devices are swapped.</span></span> <span data-ttu-id="26552-124">hello 底座、 磁碟和磁碟機箱均狀況良好。</span><span class="sxs-lookup"><span data-stu-id="26552-124">hello chassis, disks, and disk enclosures are healthy.</span></span> |<span data-ttu-id="26552-125">插槽不符警示訊息將出現。</span><span class="sxs-lookup"><span data-stu-id="26552-125">A slot mismatch alert message will appear.</span></span> |
| <span data-ttu-id="26552-126">4</span><span class="sxs-lookup"><span data-stu-id="26552-126">4</span></span> |<span data-ttu-id="26552-127">一個控制器遺漏，hello 其他控制器失敗。</span><span class="sxs-lookup"><span data-stu-id="26552-127">One controller is missing and hello other controller fails.</span></span> |<span data-ttu-id="26552-128">[更換雙重控制器時](#replace-both-controllers)，用來描述 hello[背後雙重控制器更換邏輯](#dual-controller-replacement-logic)，以及 hello[更換步驟](#dual-controller-replacement-steps)。</span><span class="sxs-lookup"><span data-stu-id="26552-128">[Dual controller replacement](#replace-both-controllers), which describes hello [logic behind a dual controller replacement](#dual-controller-replacement-logic), as well as hello [replacement steps](#dual-controller-replacement-steps).</span></span> |
| <span data-ttu-id="26552-129">5</span><span class="sxs-lookup"><span data-stu-id="26552-129">5</span></span> |<span data-ttu-id="26552-130">一個或兩個控制器故障。</span><span class="sxs-lookup"><span data-stu-id="26552-130">One or both controllers have failed.</span></span> <span data-ttu-id="26552-131">您無法存取 hello 裝置透過 hello 序列主控台或 Windows PowerShell 遠端功能。</span><span class="sxs-lookup"><span data-stu-id="26552-131">You cannot access hello device through hello serial console or Windows PowerShell remoting.</span></span> |<span data-ttu-id="26552-132">[連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md) 。</span><span class="sxs-lookup"><span data-stu-id="26552-132">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) for a manual controller replacement procedure.</span></span> |
| <span data-ttu-id="26552-133">6</span><span class="sxs-lookup"><span data-stu-id="26552-133">6</span></span> |<span data-ttu-id="26552-134">hello 控制器有不同的組建版本，這可能是因為：</span><span class="sxs-lookup"><span data-stu-id="26552-134">hello controllers have a different build version, which may be due to:</span></span><ul><li><span data-ttu-id="26552-135">控制器有不同的軟體版本。</span><span class="sxs-lookup"><span data-stu-id="26552-135">Controllers have a different software version.</span></span></li><li><span data-ttu-id="26552-136">控制器有不同的韌體版本。</span><span class="sxs-lookup"><span data-stu-id="26552-136">Controllers have a different firmware version.</span></span></li></ul> |<span data-ttu-id="26552-137">如果 hello 控制器軟體版本不同，hello 更換邏輯會偵測，並更新 hello hello 替換控制器上的軟體版本。</span><span class="sxs-lookup"><span data-stu-id="26552-137">If hello controller software versions are different, hello replacement logic detects that and updates hello software version on hello replacement controller.</span></span><br><br><span data-ttu-id="26552-138">如果 hello 控制器韌體版本不同，hello 舊的韌體版本是**不**自動升級，警示訊息會出現在 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="26552-138">If hello controller firmware versions are different and hello old firmware version is **not** automatically upgradeable, an alert message will appear in hello Azure portal.</span></span> <span data-ttu-id="26552-139">您應該掃描更新，並安裝 hello 韌體更新。</span><span class="sxs-lookup"><span data-stu-id="26552-139">You should scan for updates and install hello firmware updates.</span></span></br></br><span data-ttu-id="26552-140">如果 hello 控制器韌體版本不同，hello 舊的韌體版本可以自動升級，hello 控制器更換邏輯會偵測，並 hello 韌體 hello 控制器啟動之後，將會自動更新。</span><span class="sxs-lookup"><span data-stu-id="26552-140">If hello controller firmware versions are different and hello old firmware version is automatically upgradeable, hello controller replacement logic will detect this, and after hello controller starts, hello firmware will be automatically updated.</span></span> |

<span data-ttu-id="26552-141">如果失敗，您會需要 tooremove 控制器模組。</span><span class="sxs-lookup"><span data-stu-id="26552-141">You need tooremove a controller module if it has failed.</span></span> <span data-ttu-id="26552-142">一或兩個 hello 控制器模組可能會失敗，從而會導致更換單一控制器或更換雙重控制器時。</span><span class="sxs-lookup"><span data-stu-id="26552-142">One or both hello controller modules can fail, which can result in a single controller replacement or dual controller replacement.</span></span> <span data-ttu-id="26552-143">替代程序及 hello 背後的邏輯，請參閱下列 hello:</span><span class="sxs-lookup"><span data-stu-id="26552-143">For replacement procedures and hello logic behind them, see hello following:</span></span>

* [<span data-ttu-id="26552-144">更換單一控制器</span><span class="sxs-lookup"><span data-stu-id="26552-144">Replace a single controller</span></span>](#replace-a-single-controller)
* [<span data-ttu-id="26552-145">更換兩個控制器</span><span class="sxs-lookup"><span data-stu-id="26552-145">Replace both controllers</span></span>](#replace-both-controllers)
* [<span data-ttu-id="26552-146">取下控制器</span><span class="sxs-lookup"><span data-stu-id="26552-146">Remove a controller</span></span>](#remove-a-controller)
* [<span data-ttu-id="26552-147">插入控制器</span><span class="sxs-lookup"><span data-stu-id="26552-147">Insert a controller</span></span>](#insert-a-controller)
* [<span data-ttu-id="26552-148">識別您的裝置上的 hello 主動控制站</span><span class="sxs-lookup"><span data-stu-id="26552-148">Identify hello active controller on your device</span></span>](#identify-the-active-controller-on-your-device)

> [!IMPORTANT]
> <span data-ttu-id="26552-149">移除或取代控制站，請檢閱中的 hello 安全性資訊之前[StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="26552-149">Before removing and replacing a controller, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="replace-a-single-controller"></a><span data-ttu-id="26552-150">更換單一控制器</span><span class="sxs-lookup"><span data-stu-id="26552-150">Replace a single controller</span></span>
<span data-ttu-id="26552-151">當 hello Microsoft Azure StorSimple 裝置上的 hello 兩個控制器之一發生故障無法正常運作，或遺失時，您會需要 tooreplace 單一控制器。</span><span class="sxs-lookup"><span data-stu-id="26552-151">When one of hello two controllers on hello Microsoft Azure StorSimple device has failed, is malfunctioning, or is missing, you need tooreplace a single controller.</span></span>

### <a name="single-controller-replacement-logic"></a><span data-ttu-id="26552-152">單一控制器更換邏輯</span><span class="sxs-lookup"><span data-stu-id="26552-152">Single controller replacement logic</span></span>
<span data-ttu-id="26552-153">單一控制器更換時，您應該先移除 hello 故障的控制器。</span><span class="sxs-lookup"><span data-stu-id="26552-153">In a single controller replacement, you should first remove hello failed controller.</span></span> <span data-ttu-id="26552-154">（hello hello 裝置中其餘的控制器是作用中控制器的 hello）。當您插入 hello 替換控制器時，hello 執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="26552-154">(hello remaining controller in hello device is hello active controller.) When you insert hello replacement controller, hello following actions occur:</span></span>

1. <span data-ttu-id="26552-155">hello 替換控制器會立即開始與 hello StorSimple 裝置通訊。</span><span class="sxs-lookup"><span data-stu-id="26552-155">hello replacement controller immediately starts communicating with hello StorSimple device.</span></span>
2. <span data-ttu-id="26552-156">Hello 虛擬硬碟 (VHD) 的 hello 作用中控制器的快照集複製 hello 替換控制器上。</span><span class="sxs-lookup"><span data-stu-id="26552-156">A snapshot of hello virtual hard disk (VHD) for hello active controller is copied on hello replacement controller.</span></span>
3. <span data-ttu-id="26552-157">hello 快照經過修改，以便從此 VHD 啟動 hello 替換控制器，當它將其視為待命控制器。</span><span class="sxs-lookup"><span data-stu-id="26552-157">hello snapshot is modified so that when hello replacement controller starts from this VHD, it will be recognized as a standby controller.</span></span>
4. <span data-ttu-id="26552-158">完成 hello 修改後，hello 替換控制器將會開始為 hello 待命控制器。</span><span class="sxs-lookup"><span data-stu-id="26552-158">When hello modifications are complete, hello replacement controller will start as hello standby controller.</span></span>
5. <span data-ttu-id="26552-159">當兩個 hello 控制器正在執行時，hello 叢集就會上線。</span><span class="sxs-lookup"><span data-stu-id="26552-159">When both hello controllers are running, hello cluster comes online.</span></span>

### <a name="single-controller-replacement-steps"></a><span data-ttu-id="26552-160">單一控制器更換步驟</span><span class="sxs-lookup"><span data-stu-id="26552-160">Single controller replacement steps</span></span>
<span data-ttu-id="26552-161">完成下列步驟，如果其中一個 Microsoft Azure StorSimple 裝置中的 hello 控制站失敗 hello。</span><span class="sxs-lookup"><span data-stu-id="26552-161">Complete hello following steps if one of hello controllers in your Microsoft Azure StorSimple device fails.</span></span> <span data-ttu-id="26552-162">（hello 另一個控制器必須是有效且在執行。</span><span class="sxs-lookup"><span data-stu-id="26552-162">(hello other controller must be active and running.</span></span> <span data-ttu-id="26552-163">如果兩個控制器故障或運作失常，請移至太[雙重控制器更換步驟](#dual-controller-replacement-steps)。)</span><span class="sxs-lookup"><span data-stu-id="26552-163">If both controllers fail or malfunction, go too[dual controller replacement steps](#dual-controller-replacement-steps).)</span></span>

> [!NOTE]
> <span data-ttu-id="26552-164">它可以使用 hello 控制器 toorestart 30-45 分鐘，並從 hello 單一控制器更換程序中完全復原。</span><span class="sxs-lookup"><span data-stu-id="26552-164">It can take 30 – 45 minutes for hello controller toorestart and completely recover from hello single controller replacement procedure.</span></span> <span data-ttu-id="26552-165">hello 整個程序，包括接上纜線 hello hello 總時間是大約 2 小時。</span><span class="sxs-lookup"><span data-stu-id="26552-165">hello total time for hello entire procedure, including attaching hello cables, is approximately 2 hours.</span></span>


#### <a name="tooremove-a-single-failed-controller-module"></a><span data-ttu-id="26552-166">tooremove 單一故障的控制器模組</span><span class="sxs-lookup"><span data-stu-id="26552-166">tooremove a single failed controller module</span></span>
1. <span data-ttu-id="26552-167">在 hello Azure 入口網站，請移 toohello StorSimple 裝置管理員服務，按一下 **裝置**，然後按一下您想 toomonitor hello 裝置 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="26552-167">In hello Azure portal, go toohello StorSimple Device Manager service, click **Devices**, and then click hello name of hello device that you want toomonitor.</span></span>
2. <span data-ttu-id="26552-168">跳過**監視 > 硬體健全狀況**。</span><span class="sxs-lookup"><span data-stu-id="26552-168">Go too**Monitor > Hardware health**.</span></span> <span data-ttu-id="26552-169">控制器 0 或控制器 1 的 hello 狀態應為紅色，表示故障。</span><span class="sxs-lookup"><span data-stu-id="26552-169">hello status of either Controller 0 or Controller 1 should be red, which indicates a failure.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="26552-170">hello 單一控制器更換中故障的控制器一律是待命控制器。</span><span class="sxs-lookup"><span data-stu-id="26552-170">hello failed controller in a single controller replacement is always a standby controller.</span></span>
   
3. <span data-ttu-id="26552-171">使用圖 1 和 hello 下列資料表 toolocate hello 故障的控制器模組。</span><span class="sxs-lookup"><span data-stu-id="26552-171">Use Figure 1 and hello following table toolocate hello failed controller module.</span></span>
   
    ![裝置主要機箱模組的後擋板](./media/storsimple-controller-replacement/IC740994.png)
   
    <span data-ttu-id="26552-173">**圖 1** StorSimple 裝置的背面</span><span class="sxs-lookup"><span data-stu-id="26552-173">**Figure 1** Back of StorSimple device</span></span>
   
   | <span data-ttu-id="26552-174">標籤</span><span class="sxs-lookup"><span data-stu-id="26552-174">Label</span></span> | <span data-ttu-id="26552-175">說明</span><span class="sxs-lookup"><span data-stu-id="26552-175">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="26552-176">1</span><span class="sxs-lookup"><span data-stu-id="26552-176">1</span></span> |<span data-ttu-id="26552-177">PCM 0</span><span class="sxs-lookup"><span data-stu-id="26552-177">PCM 0</span></span> |
   | <span data-ttu-id="26552-178">2</span><span class="sxs-lookup"><span data-stu-id="26552-178">2</span></span> |<span data-ttu-id="26552-179">PCM 1</span><span class="sxs-lookup"><span data-stu-id="26552-179">PCM 1</span></span> |
   | <span data-ttu-id="26552-180">3</span><span class="sxs-lookup"><span data-stu-id="26552-180">3</span></span> |<span data-ttu-id="26552-181">控制器 0</span><span class="sxs-lookup"><span data-stu-id="26552-181">Controller 0</span></span> |
   | <span data-ttu-id="26552-182">4</span><span class="sxs-lookup"><span data-stu-id="26552-182">4</span></span> |<span data-ttu-id="26552-183">控制器 1</span><span class="sxs-lookup"><span data-stu-id="26552-183">Controller 1</span></span> |
4. <span data-ttu-id="26552-184">在 hello 故障的控制器，移除所有 hello 連接網路纜線從 hello 資料連接埠。</span><span class="sxs-lookup"><span data-stu-id="26552-184">On hello failed controller, remove all hello connected network cables from hello data ports.</span></span> <span data-ttu-id="26552-185">如果您使用 8600 的模型，也會移除的 hello SAS 纜線連接 hello 控制器 toohello EBOD 控制器。</span><span class="sxs-lookup"><span data-stu-id="26552-185">If you are using an 8600 model, also remove hello SAS cables that connect hello controller toohello EBOD controller.</span></span>
5. <span data-ttu-id="26552-186">中的 hello 步驟[移除控制器](#remove-a-controller)tooremove hello 無法控制站。</span><span class="sxs-lookup"><span data-stu-id="26552-186">Follow hello steps in [remove a controller](#remove-a-controller) tooremove hello failed controller.</span></span>
6. <span data-ttu-id="26552-187">安裝在相同位置中的 hello 故障的控制器的 hello hello 原廠更換品已移除。</span><span class="sxs-lookup"><span data-stu-id="26552-187">Install hello factory replacement in hello same slot from which hello failed controller was removed.</span></span> <span data-ttu-id="26552-188">這會觸發 hello 單一控制器更換邏輯。</span><span class="sxs-lookup"><span data-stu-id="26552-188">This triggers hello single controller replacement logic.</span></span> <span data-ttu-id="26552-189">如需詳細資訊，請參閱 [單一控制器更換邏輯](#single-controller-replacement-logic)。</span><span class="sxs-lookup"><span data-stu-id="26552-189">For more information, see [single controller replacement logic](#single-controller-replacement-logic).</span></span>
7. <span data-ttu-id="26552-190">當 hello 單一控制器更換邏輯進行 hello 背景時時，請重新連接 hello 纜線。</span><span class="sxs-lookup"><span data-stu-id="26552-190">While hello single controller replacement logic progresses in hello background, reconnect hello cables.</span></span> <span data-ttu-id="26552-191">需要小心 tooconnect hello 的纜線完全 hello hello 更換前連接它們的方式相同。</span><span class="sxs-lookup"><span data-stu-id="26552-191">Take care tooconnect all hello cables exactly hello same way that they were connected before hello replacement.</span></span>
8. <span data-ttu-id="26552-192">Hello 控制器重新啟動之後，請檢查 hello**控制器狀態**和 hello**叢集狀態**在 hello Azure hello 控制站的入口網站 tooverify 是回復 tooa 狀況良好狀態，而處於待命模式。</span><span class="sxs-lookup"><span data-stu-id="26552-192">After hello controller restarts, check hello **Controller status** and hello **Cluster status** in hello Azure portal tooverify that hello controller is back tooa healthy state and is in standby mode.</span></span>

> [!NOTE]
> <span data-ttu-id="26552-193">如果您要監視 hello 裝置透過 hello 序列主控台，您可能會在 hello 控制器從 hello 更換程序中復原時看到多次重新啟動。</span><span class="sxs-lookup"><span data-stu-id="26552-193">If you are monitoring hello device through hello serial console, you may see multiple restarts while hello controller is recovering from hello replacement procedure.</span></span> <span data-ttu-id="26552-194">當 hello 序列主控台功能表呈現時，您便知道 hello 取代已完成。</span><span class="sxs-lookup"><span data-stu-id="26552-194">When hello serial console menu is presented, then you know that hello replacement is complete.</span></span> <span data-ttu-id="26552-195">如果 hello 功能表啟動 hello 控制器更換的 2 小時內未出現，請[連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="26552-195">If hello menu does not appear within two hours of starting hello controller replacement, please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
>
> <span data-ttu-id="26552-196">從更新 4 的開始，您也可以使用 hello cmdlet `Get-HCSControllerReplacementStatus` hello hello 裝置 toomonitor hello 狀態 hello 控制器更換程序的 Windows PowerShell 介面中。</span><span class="sxs-lookup"><span data-stu-id="26552-196">Starting Update 4, you can also use hello cmdlet `Get-HCSControllerReplacementStatus` in hello Windows PowerShell interface of hello device toomonitor hello status of hello controller replacement process.</span></span>
> 

## <a name="replace-both-controllers"></a><span data-ttu-id="26552-197">更換兩個控制器</span><span class="sxs-lookup"><span data-stu-id="26552-197">Replace both controllers</span></span>
<span data-ttu-id="26552-198">當兩個控制器 hello Microsoft Azure StorSimple 裝置上的失敗、 運作失常，或遺漏時，您需要 tooreplace 兩個控制器。</span><span class="sxs-lookup"><span data-stu-id="26552-198">When both controllers on hello Microsoft Azure StorSimple device have failed, are malfunctioning, or are missing, you need tooreplace both controllers.</span></span> 

### <a name="dual-controller-replacement-logic"></a><span data-ttu-id="26552-199">雙重控制器更換</span><span class="sxs-lookup"><span data-stu-id="26552-199">Dual controller replacement logic</span></span>
<span data-ttu-id="26552-200">在雙重控制器更換中，先移除兩個故障的控制器，再插入更換控制器。</span><span class="sxs-lookup"><span data-stu-id="26552-200">In a dual controller replacement, you first remove both failed controllers and then insert replacements.</span></span> <span data-ttu-id="26552-201">當插入 hello 兩個替換控制器時，hello 執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="26552-201">When hello two replacement controllers are inserted, hello following actions occur:</span></span>

1. <span data-ttu-id="26552-202">插槽 0 中的 hello 替換控制器會檢查 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="26552-202">hello replacement controller in slot 0 checks hello following:</span></span>
   
   1. <span data-ttu-id="26552-203">是否使用目前版本的 hello 韌體及軟體？</span><span class="sxs-lookup"><span data-stu-id="26552-203">Is it using current versions of hello firmware and software?</span></span>
   2. <span data-ttu-id="26552-204">它是 hello 叢集的一部分嗎？</span><span class="sxs-lookup"><span data-stu-id="26552-204">Is it a part of hello cluster?</span></span>
   3. <span data-ttu-id="26552-205">是 hello 同儕節點控制器執行並已叢集處理？</span><span class="sxs-lookup"><span data-stu-id="26552-205">Is hello peer controller running and is it clustered?</span></span>
      
      <span data-ttu-id="26552-206">如果以上條件都成立，hello 控制器會尋找 hello 最新每日備份 (位於 hello **nonDOMstorage**磁碟機 S 上)。</span><span class="sxs-lookup"><span data-stu-id="26552-206">If none of these conditions are true, hello controller looks for hello latest daily backup (located in hello **nonDOMstorage** on drive S).</span></span> <span data-ttu-id="26552-207">hello 控制站複製 hello 備份 hello hello VHD 的最新快照集。</span><span class="sxs-lookup"><span data-stu-id="26552-207">hello controller copies hello latest snapshot of hello VHD from hello backup.</span></span>
2. <span data-ttu-id="26552-208">插槽 0 中的 hello 控制器會使用 hello 快照 tooimage 本身。</span><span class="sxs-lookup"><span data-stu-id="26552-208">hello controller in slot 0 uses hello snapshot tooimage itself.</span></span>
3. <span data-ttu-id="26552-209">同時，插槽 1 中的 hello 控制器等待控制器 0 toocomplete hello 製作映像開始。</span><span class="sxs-lookup"><span data-stu-id="26552-209">Meanwhile, hello controller in slot 1 waits for controller 0 toocomplete hello imaging and start.</span></span>
4. <span data-ttu-id="26552-210">控制器 0 啟動之後，控制器 1 會偵測控制器 0 時，所建立的觸發程序 hello 單一控制器更換邏輯 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="26552-210">After controller 0 starts, controller 1 detects hello cluster created by controller 0, which triggers hello single controller replacement logic.</span></span> <span data-ttu-id="26552-211">如需詳細資訊，請參閱 [單一控制器更換邏輯](#single-controller-replacement-logic)。</span><span class="sxs-lookup"><span data-stu-id="26552-211">For more information, see [single controller replacement logic](#single-controller-replacement-logic).</span></span>
5. <span data-ttu-id="26552-212">之後，將會執行兩個控制器，而且 hello 叢集會上線。</span><span class="sxs-lookup"><span data-stu-id="26552-212">Afterwards, both controllers will be running and hello cluster will come online.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26552-213">更換雙重控制器時，下列 hello StorSimple 裝置設定之後，很重要，您會製作手動備份 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="26552-213">Following a dual controller replacement, after hello StorSimple device is configured, it is essential that you take a manual backup of hello device.</span></span> <span data-ttu-id="26552-214">直到過了 24 小時之後，才會觸發每日裝置組態備份。</span><span class="sxs-lookup"><span data-stu-id="26552-214">Daily device configuration backups are not triggered until after 24 hours have elapsed.</span></span> <span data-ttu-id="26552-215">使用[Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)toomake 手動備份您的裝置。</span><span class="sxs-lookup"><span data-stu-id="26552-215">Work with [Microsoft Support](storsimple-8000-contact-microsoft-support.md) toomake a manual backup of your device.</span></span>


### <a name="dual-controller-replacement-steps"></a><span data-ttu-id="26552-216">雙重控制器更換步驟</span><span class="sxs-lookup"><span data-stu-id="26552-216">Dual controller replacement steps</span></span>
<span data-ttu-id="26552-217">這兩個 Microsoft Azure StorSimple 裝置中的 hello 控制站失敗時，需要這個工作流程。</span><span class="sxs-lookup"><span data-stu-id="26552-217">This workflow is required when both of hello controllers in your Microsoft Azure StorSimple device have failed.</span></span> <span data-ttu-id="26552-218">這種情形的資料中心所在 hello 冷卻系統停止運作，如此一來，兩個 hello 控制器失敗的時間在短時間內。</span><span class="sxs-lookup"><span data-stu-id="26552-218">This could happen in a datacenter in which hello cooling system stops working, and as a result, both hello controllers fail within a short period of time.</span></span> <span data-ttu-id="26552-219">取決於是否 hello StorSimple 裝置已關閉或開啟後，無論您使用 8600，或 8100 機型，一組不同的步驟。</span><span class="sxs-lookup"><span data-stu-id="26552-219">Depending on whether hello StorSimple device is turned off or on, and whether you are using an 8600 or an 8100 model, a different set of steps is required.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26552-220">它可以 hello 控制器 toorestart 45 分鐘內 too1 小時，並從雙重控制器更換程序中完全復原。</span><span class="sxs-lookup"><span data-stu-id="26552-220">It can take 45 minutes too1 hour for hello controller toorestart and completely recover from a dual controller replacement procedure.</span></span> <span data-ttu-id="26552-221">hello 整個程序，包括接上纜線 hello hello 總時間是大約 2.5 小時。</span><span class="sxs-lookup"><span data-stu-id="26552-221">hello total time for hello entire procedure, including attaching hello cables, is approximately 2.5 hours.</span></span>

#### <a name="tooreplace-both-controller-modules"></a><span data-ttu-id="26552-222">tooreplace 兩個控制器模組</span><span class="sxs-lookup"><span data-stu-id="26552-222">tooreplace both controller modules</span></span>
1. <span data-ttu-id="26552-223">如果 hello 裝置已關閉，請略過此步驟，然後繼續 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="26552-223">If hello device is turned off, skip this step and proceed toohello next step.</span></span> <span data-ttu-id="26552-224">如果開啟 hello 裝置時，關閉 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="26552-224">If hello device is turned on, turn off hello device.</span></span>
   
   1. <span data-ttu-id="26552-225">如果您使用 8600 的模型，請先關閉主要機箱 hello，，，然後將關閉 hello EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="26552-225">If you are using an 8600 model, turn off hello primary enclosure first, and then turn off hello EBOD enclosure.</span></span>
   2. <span data-ttu-id="26552-226">請等到 hello 裝置完全關閉。</span><span class="sxs-lookup"><span data-stu-id="26552-226">Wait until hello device has shut down completely.</span></span> <span data-ttu-id="26552-227">在 hello hello 裝置背面的所有 hello Led 都將關閉。</span><span class="sxs-lookup"><span data-stu-id="26552-227">All hello LEDs in hello back of hello device will be off.</span></span>
2. <span data-ttu-id="26552-228">移除所有 hello 網路纜線連接的 toohello 資料的連接埠。</span><span class="sxs-lookup"><span data-stu-id="26552-228">Remove all hello network cables that are connected toohello data ports.</span></span> <span data-ttu-id="26552-229">如果您使用 8600 的模型，也會移除的 hello SAS 纜線連接 hello 主要機箱 toohello EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="26552-229">If you are using an 8600 model, also remove hello SAS cables that connect hello primary enclosure toohello EBOD enclosure.</span></span>
3. <span data-ttu-id="26552-230">Hello StorSimple 裝置中移除兩個控制器。</span><span class="sxs-lookup"><span data-stu-id="26552-230">Remove both controllers from hello StorSimple device.</span></span> <span data-ttu-id="26552-231">如需詳細資訊，請參閱[取下控制器](#remove-a-controller)。</span><span class="sxs-lookup"><span data-stu-id="26552-231">For more information, see [remove a controller](#remove-a-controller).</span></span>
4. <span data-ttu-id="26552-232">首先，插入控制器 0 的 hello 原廠更換品，然後再插入控制器 1。</span><span class="sxs-lookup"><span data-stu-id="26552-232">Insert hello factory replacement for Controller 0 first, and then insert Controller 1.</span></span> <span data-ttu-id="26552-233">如需詳細資訊，請參閱[插入控制器](#insert-a-controller)。</span><span class="sxs-lookup"><span data-stu-id="26552-233">For more information, see [insert a controller](#insert-a-controller).</span></span> <span data-ttu-id="26552-234">這會觸發 hello 雙重控制器更換邏輯。</span><span class="sxs-lookup"><span data-stu-id="26552-234">This triggers hello dual controller replacement logic.</span></span> <span data-ttu-id="26552-235">如需詳細資訊，請參閱[雙重控制器更換邏輯](#dual-controller-replacement-logic)。</span><span class="sxs-lookup"><span data-stu-id="26552-235">For more information, see [dual controller replacement logic](#dual-controller-replacement-logic).</span></span>
5. <span data-ttu-id="26552-236">當 hello 控制器更換邏輯進行 hello 背景時時，請重新連接 hello 纜線。</span><span class="sxs-lookup"><span data-stu-id="26552-236">While hello controller replacement logic progresses in hello background, reconnect hello cables.</span></span> <span data-ttu-id="26552-237">需要小心 tooconnect hello 的纜線完全 hello hello 更換前連接它們的方式相同。</span><span class="sxs-lookup"><span data-stu-id="26552-237">Take care tooconnect all hello cables exactly hello same way that they were connected before hello replacement.</span></span> <span data-ttu-id="26552-238">請參閱 hello 詳細 hello 纜線的模型指示您裝置區段[安裝 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md)或[安裝 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="26552-238">See hello detailed instructions for your model in hello Cable your device section of [install your StorSimple 8100 device](storsimple-8100-hardware-installation.md) or [install your StorSimple 8600 device](storsimple-8600-hardware-installation.md).</span></span>
6. <span data-ttu-id="26552-239">開啟 hello StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="26552-239">Turn on hello StorSimple device.</span></span> <span data-ttu-id="26552-240">如果您使用的是 8600 機型：</span><span class="sxs-lookup"><span data-stu-id="26552-240">If you are using an 8600 model:</span></span>
   
   1. <span data-ttu-id="26552-241">確定首先開啟 EBOD 機箱的 hello。</span><span class="sxs-lookup"><span data-stu-id="26552-241">Make sure that hello EBOD enclosure is turned on first.</span></span>
   2. <span data-ttu-id="26552-242">請等到執行 hello EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="26552-242">Wait until hello EBOD enclosure is running.</span></span>
   3. <span data-ttu-id="26552-243">開啟 hello 主要機箱。</span><span class="sxs-lookup"><span data-stu-id="26552-243">Turn on hello primary enclosure.</span></span>
   4. <span data-ttu-id="26552-244">Hello 第一個控制器重新啟動，並處於狀況良好狀態之後，將會執行 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="26552-244">After hello first controller restarts and is in a healthy state, hello system will be running.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="26552-245">如果您要監視 hello 裝置透過 hello 序列主控台，您可能會在 hello 控制器從 hello 更換程序中復原時看到多次重新啟動。</span><span class="sxs-lookup"><span data-stu-id="26552-245">If you are monitoring hello device through hello serial console, you may see multiple restarts while hello controller is recovering from hello replacement procedure.</span></span> <span data-ttu-id="26552-246">Hello 序列主控台功能表中出現時，您便知道 hello 取代已完成。</span><span class="sxs-lookup"><span data-stu-id="26552-246">When hello serial console menu appears, then you know that hello replacement is complete.</span></span> <span data-ttu-id="26552-247">如果 hello 功能表啟動 hello 控制器更換的 2.5 小時內沒有出現，請[連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="26552-247">If hello menu does not appear within 2.5 hours of starting hello controller replacement, please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
     
## <a name="remove-a-controller"></a><span data-ttu-id="26552-248">取下控制器</span><span class="sxs-lookup"><span data-stu-id="26552-248">Remove a controller</span></span>
<span data-ttu-id="26552-249">使用您的 StorSimple 裝置中的下列程序 tooremove 發生故障的控制器模組的 hello。</span><span class="sxs-lookup"><span data-stu-id="26552-249">Use hello following procedure tooremove a faulty controller module from your StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="26552-250">下列圖例 hello 適用於控制器 0。</span><span class="sxs-lookup"><span data-stu-id="26552-250">hello following illustrations are for controller 0.</span></span> <span data-ttu-id="26552-251">若為控制器 1，這些將相反。</span><span class="sxs-lookup"><span data-stu-id="26552-251">For controller 1, these would be reversed.</span></span>


#### <a name="tooremove-a-controller-module"></a><span data-ttu-id="26552-252">tooremove 控制器模組</span><span class="sxs-lookup"><span data-stu-id="26552-252">tooremove a controller module</span></span>
1. <span data-ttu-id="26552-253">掌握用姆指與食指 hello 模組閂鎖。</span><span class="sxs-lookup"><span data-stu-id="26552-253">Grasp hello module latch between your thumb and forefinger.</span></span>
2. <span data-ttu-id="26552-254">輕輕擠壓您姆指與食指同時 toorelease hello 控制器閂鎖。</span><span class="sxs-lookup"><span data-stu-id="26552-254">Gently squeeze your thumb and forefinger together toorelease hello controller latch.</span></span>
   
    ![鬆開控制器閂鎖](./media/storsimple-controller-replacement/IC741047.png)
   
    <span data-ttu-id="26552-256">**圖 2** 鬆開控制器閂鎖</span><span class="sxs-lookup"><span data-stu-id="26552-256">**Figure 2** Releasing controller latch</span></span>
3. <span data-ttu-id="26552-257">Hello 閂鎖作為超出 hello 底座的控制代碼 tooslide hello 控制站。</span><span class="sxs-lookup"><span data-stu-id="26552-257">Use hello latch as a handle tooslide hello controller out of hello chassis.</span></span>
   
    ![將控制器滑出底座](./media/storsimple-controller-replacement/IC741048.png)
   
    <span data-ttu-id="26552-259">**圖 3** hello 控制器滑出底座 hello</span><span class="sxs-lookup"><span data-stu-id="26552-259">**Figure 3** Sliding hello controller out of hello chassis</span></span>

## <a name="insert-a-controller"></a><span data-ttu-id="26552-260">插入控制器</span><span class="sxs-lookup"><span data-stu-id="26552-260">Insert a controller</span></span>
<span data-ttu-id="26552-261">使用下列程序 tooinstall 廠的控制器模組故障的模組移除您的 StorSimple 裝置之後 hello。</span><span class="sxs-lookup"><span data-stu-id="26552-261">Use hello following procedure tooinstall a factory-supplied controller module after you remove a faulty module from your StorSimple device.</span></span>

#### <a name="tooinstall-a-controller-module"></a><span data-ttu-id="26552-262">tooinstall 控制器模組</span><span class="sxs-lookup"><span data-stu-id="26552-262">tooinstall a controller module</span></span>
1. <span data-ttu-id="26552-263">如果有任何損毀 toohello 介面連接器，請檢查 toosee。</span><span class="sxs-lookup"><span data-stu-id="26552-263">Check toosee if there is any damage toohello interface connectors.</span></span> <span data-ttu-id="26552-264">如果任何 hello 連接器針腳插腳損壞或彎曲，請勿安裝 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="26552-264">Do not install hello module if any of hello connector pins are damaged or bent.</span></span>
2. <span data-ttu-id="26552-265">Hello 控制器模組滑入底座 hello 中 hello 閂鎖完全鬆開時。</span><span class="sxs-lookup"><span data-stu-id="26552-265">Slide hello controller module into hello chassis while hello latch is fully released.</span></span>
   
    ![將控制器滑入底座](./media/storsimple-controller-replacement/IC741053.png)
   
    <span data-ttu-id="26552-267">**圖 4**將控制器滑入底座 hello</span><span class="sxs-lookup"><span data-stu-id="26552-267">**Figure 4** Sliding controller into hello chassis</span></span>
3. <span data-ttu-id="26552-268">Hello 插入控制器模組後，開始關閉至 hello 底座 hello 閂鎖，同時繼續 toopush hello 控制器模組。</span><span class="sxs-lookup"><span data-stu-id="26552-268">With hello controller module inserted, begin closing hello latch while continuing toopush hello controller module into hello chassis.</span></span> <span data-ttu-id="26552-269">hello 閂鎖會連絡 tooguide hello 控制器位置。</span><span class="sxs-lookup"><span data-stu-id="26552-269">hello latch will engage tooguide hello controller into place.</span></span>
   
    ![關閉控制器閂鎖](./media/storsimple-controller-replacement/IC741054.png)
   
    <span data-ttu-id="26552-271">**圖 5**關閉 hello 控制器閂鎖</span><span class="sxs-lookup"><span data-stu-id="26552-271">**Figure 5** Closing hello controller latch</span></span>
4. <span data-ttu-id="26552-272">您已大功告成 hello 閂鎖卡入定位時。</span><span class="sxs-lookup"><span data-stu-id="26552-272">You're done when hello latch snaps into place.</span></span> <span data-ttu-id="26552-273">hello**確定**LED 現在應該亮起。</span><span class="sxs-lookup"><span data-stu-id="26552-273">hello **OK** LED should now be on.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="26552-274">就可以在 hello 控制器和 LED tooactivate hello too5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="26552-274">It can take up too5 minutes for hello controller and hello LED tooactivate.</span></span>
  
5. <span data-ttu-id="26552-275">tooverify hello 取代為成功，請在 hello Azure 入口網站移 tooyour 裝置，然後瀏覽過**監視器** > **硬體健全狀況**，並請確定這兩個控制器 0 和控制器 1 的狀況良好 （狀態為綠色）。</span><span class="sxs-lookup"><span data-stu-id="26552-275">tooverify that hello replacement is successful, in hello Azure portal, go tooyour device and then navigate too**Monitor** > **Hardware health**, and make sure that both controller 0 and controller 1 are healthy (status is green).</span></span>

## <a name="identify-hello-active-controller-on-your-device"></a><span data-ttu-id="26552-276">識別您的裝置上的 hello 主動控制站</span><span class="sxs-lookup"><span data-stu-id="26552-276">Identify hello active controller on your device</span></span>
<span data-ttu-id="26552-277">有許多情況下，第一次裝置註冊或控制站取代，例如，必須在 StorSimple 裝置 toolocate hello 作用中的控制器。</span><span class="sxs-lookup"><span data-stu-id="26552-277">There are many situations, such as first-time device registration or controller replacement, that require you toolocate hello active controller on a StorSimple device.</span></span> <span data-ttu-id="26552-278">hello 作用中控制器會處理所有 hello 磁碟韌體和網路作業。</span><span class="sxs-lookup"><span data-stu-id="26552-278">hello active controller processes all hello disk firmware and networking operations.</span></span> <span data-ttu-id="26552-279">您可以使用任何下列方法 tooidentify hello 作用中控制器的 hello:</span><span class="sxs-lookup"><span data-stu-id="26552-279">You can use any of hello following methods tooidentify hello active controller:</span></span>

* [<span data-ttu-id="26552-280">使用 hello Azure 入口網站 tooidentify hello 作用中控制器</span><span class="sxs-lookup"><span data-stu-id="26552-280">Use hello Azure portal tooidentify hello active controller</span></span>](#use-the-azure-portal-to-identify-the-active-controller)
* [<span data-ttu-id="26552-281">使用 Windows PowerShell for StorSimple tooidentify hello 作用中控制器</span><span class="sxs-lookup"><span data-stu-id="26552-281">Use Windows PowerShell for StorSimple tooidentify hello active controller</span></span>](#use-windows-powershell-for-storsimple-to-identify-the-active-controller)
* [<span data-ttu-id="26552-282">檢查 hello 實體裝置 tooidentify hello 作用中控制器</span><span class="sxs-lookup"><span data-stu-id="26552-282">Check hello physical device tooidentify hello active controller</span></span>](#check-the-physical-device-to-identify-the-active-controller)

<span data-ttu-id="26552-283">接著說明上述各程序。</span><span class="sxs-lookup"><span data-stu-id="26552-283">Each of these procedures is described next.</span></span>

### <a name="use-hello-azure-portal-tooidentify-hello-active-controller"></a><span data-ttu-id="26552-284">使用 hello Azure 入口網站 tooidentify hello 作用中控制器</span><span class="sxs-lookup"><span data-stu-id="26552-284">Use hello Azure portal tooidentify hello active controller</span></span>
<span data-ttu-id="26552-285">在 hello Azure 入口網站中瀏覽 tooyour 裝置，然後太**監視器** > **硬體健全狀況**，並捲動 toohello**控制站**> 一節。</span><span class="sxs-lookup"><span data-stu-id="26552-285">In hello Azure portal, navigate tooyour device and then too**Monitor** > **Hardware health**, and scroll toohello **Controllers** section.</span></span> <span data-ttu-id="26552-286">在這裡您可以確認哪一個控制站作用中。</span><span class="sxs-lookup"><span data-stu-id="26552-286">Here you can verify which controller is active.</span></span>

![識別 Azure 入口網站中的作用中控制器](./media/storsimple-controller-replacement/IC752072.png)

<span data-ttu-id="26552-288">**圖 6** Azure 入口網站顯示 hello 作用中控制器</span><span class="sxs-lookup"><span data-stu-id="26552-288">**Figure 6** Azure portal showing hello active controller</span></span>

### <a name="use-windows-powershell-for-storsimple-tooidentify-hello-active-controller"></a><span data-ttu-id="26552-289">使用 Windows PowerShell for StorSimple tooidentify hello 作用中控制器</span><span class="sxs-lookup"><span data-stu-id="26552-289">Use Windows PowerShell for StorSimple tooidentify hello active controller</span></span>
<span data-ttu-id="26552-290">當您透過 hello 序列主控台存取您的裝置時，會顯示橫幅訊息。</span><span class="sxs-lookup"><span data-stu-id="26552-290">When you access your device through hello serial console, a banner message is presented.</span></span> <span data-ttu-id="26552-291">hello 橫幅訊息包含基本裝置資訊，例如 hello 模型、 名稱、 已安裝的軟體版本，以及您要存取的 hello 控制站的狀態。</span><span class="sxs-lookup"><span data-stu-id="26552-291">hello banner message contains basic device information such as hello model, name, installed software version, and status of hello controller you are accessing.</span></span> <span data-ttu-id="26552-292">hello 下列影像顯示橫幅訊息範例：</span><span class="sxs-lookup"><span data-stu-id="26552-292">hello following image shows an example of a banner message:</span></span>

![序列橫幅訊息](./media/storsimple-controller-replacement/IC741098.png)

<span data-ttu-id="26552-294">**圖 7** 橫幅訊息將控制器 0 顯示為作用中</span><span class="sxs-lookup"><span data-stu-id="26552-294">**Figure 7** Banner message showing controller 0 as Active</span></span>

<span data-ttu-id="26552-295">無論您是 hello 控制站，您可以使用 hello 橫幅訊息 toodetermine 連接 toois 主動或被動。</span><span class="sxs-lookup"><span data-stu-id="26552-295">You can use hello banner message toodetermine whether hello controller you are connected toois active or passive.</span></span>

### <a name="check-hello-physical-device-tooidentify-hello-active-controller"></a><span data-ttu-id="26552-296">檢查 hello 實體裝置 tooidentify hello 作用中控制器</span><span class="sxs-lookup"><span data-stu-id="26552-296">Check hello physical device tooidentify hello active controller</span></span>
<span data-ttu-id="26552-297">tooidentify hello 作用中控制器上您的裝置，找出 hello 藍色 LED hello DATA 5 連接埠上 hello 主要機箱背面的 hello 上方。</span><span class="sxs-lookup"><span data-stu-id="26552-297">tooidentify hello active controller on your device, locate hello blue LED above hello DATA 5 port on hello back of hello primary enclosure.</span></span>

<span data-ttu-id="26552-298">如果此 LED 閃爍不停，hello 控制器為作用中且 hello 另一個控制器處於待命模式。</span><span class="sxs-lookup"><span data-stu-id="26552-298">If this LED is blinking, hello controller is active and hello other controller is in standby mode.</span></span> <span data-ttu-id="26552-299">使用下列圖表中的 hello 和表格作為輔助工具。</span><span class="sxs-lookup"><span data-stu-id="26552-299">Use hello following diagram and table as an aid.</span></span>

![包含資料連接埠的裝置主要機箱後擋板](./media/storsimple-controller-replacement/IC741055.png)

<span data-ttu-id="26552-301">**圖 8** 具有資料連接埠和監視 LED 的主要機箱背面</span><span class="sxs-lookup"><span data-stu-id="26552-301">**Figure 8** Back of primary enclosure with data ports and monitoring LEDs</span></span>

| <span data-ttu-id="26552-302">標籤</span><span class="sxs-lookup"><span data-stu-id="26552-302">Label</span></span> | <span data-ttu-id="26552-303">說明</span><span class="sxs-lookup"><span data-stu-id="26552-303">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="26552-304">1-6</span><span class="sxs-lookup"><span data-stu-id="26552-304">1-6</span></span> |<span data-ttu-id="26552-305">DATA 0 – 5 個網路連接埠</span><span class="sxs-lookup"><span data-stu-id="26552-305">DATA 0 – 5 network ports</span></span> |
| <span data-ttu-id="26552-306">7</span><span class="sxs-lookup"><span data-stu-id="26552-306">7</span></span> |<span data-ttu-id="26552-307">藍色 LED</span><span class="sxs-lookup"><span data-stu-id="26552-307">Blue LED</span></span> |

## <a name="next-steps"></a><span data-ttu-id="26552-308">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26552-308">Next steps</span></span>
<span data-ttu-id="26552-309">深入了解 [StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="26552-309">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

