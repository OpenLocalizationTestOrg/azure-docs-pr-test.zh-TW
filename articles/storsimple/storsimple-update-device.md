---
title: "aaaUpdate StorSimple 裝置 |Microsoft 文件"
description: "說明如何 toouse hello StorSimple 更新功能 tooinstall 規則和維護模式更新和 hotfix。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="9a2f5-103">更新您的 StorSimple 8000 系列裝置</span><span class="sxs-lookup"><span data-stu-id="9a2f5-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="9a2f5-104">概觀</span><span class="sxs-lookup"><span data-stu-id="9a2f5-104">Overview</span></span>
<span data-ttu-id="9a2f5-105">hello StorSimple 更新功能可讓您 tooeasily 保持您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-105">hello StorSimple updates features allow you tooeasily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="9a2f5-106">根據 hello 更新類型，您可以套用更新 toohello 裝置透過 hello Azure 傳統入口網站或透過 hello Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-106">Depending on hello update type, you can apply updates toohello device via hello Azure classic portal or via hello Windows PowerShell interface.</span></span> <span data-ttu-id="9a2f5-107">這個教學課程描述 hello 更新類型及如何 tooinstall 每個。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-107">This tutorial describes hello update types and how tooinstall each of them.</span></span>

<span data-ttu-id="9a2f5-108">您可以套用兩種類型的裝置更新：</span><span class="sxs-lookup"><span data-stu-id="9a2f5-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="9a2f5-109">一般 (或標準模式) 更新</span><span class="sxs-lookup"><span data-stu-id="9a2f5-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="9a2f5-110">維護模式更新</span><span class="sxs-lookup"><span data-stu-id="9a2f5-110">Maintenance mode updates</span></span>

<span data-ttu-id="9a2f5-111">您可以安裝 hello Azure 傳統入口網站或 Windows PowerShell 中; 透過定期更新不過，您必須使用 Windows PowerShell tooinstall 維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-111">You can install regular updates via hello Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell tooinstall Maintenance mode updates.</span></span> 

<span data-ttu-id="9a2f5-112">以下將個別說明每個更新類型。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="9a2f5-113">一般更新</span><span class="sxs-lookup"><span data-stu-id="9a2f5-113">Regular updates</span></span>
<span data-ttu-id="9a2f5-114">定期更新將會非干擾性更新可以在 hello 裝置處於正常模式時安裝。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-114">Regular updates are non-disruptive updates that can be installed when hello device is in Normal mode.</span></span> <span data-ttu-id="9a2f5-115">這些更新會透過 hello Microsoft Update 網站 tooeach 裝置控制器套用。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-115">These updates are applied through hello Microsoft Update website tooeach device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9a2f5-116">控制器容錯移轉可能會發生 hello 更新程序期間。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-116">A controller failover may occur during hello update process.</span></span> <span data-ttu-id="9a2f5-117">不過，這不會影響系統的可用性或運作。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="9a2f5-118">如需 tooinstall regular 更新的方式透過 hello Azure 傳統入口網站的詳細資訊，請參閱[安裝定期更新 hello Azure 傳統入口網站透過](#install-regular-updates-via-the-azure-classic-portal)。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-118">For details on how tooinstall regular updates via hello Azure classic portal, see [Install regular updates via hello Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="9a2f5-119">您也可以透過 Windows PowerShell for StorSimple 安裝一般更新。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="9a2f5-120">如需詳細資訊，請參閱 [透過 Windows PowerShell for StorSimple 安裝一般更新](#install-regular-updates-via-windows-powershell-for-storsimple)。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="9a2f5-121">維護模式更新</span><span class="sxs-lookup"><span data-stu-id="9a2f5-121">Maintenance mode updates</span></span>
<span data-ttu-id="9a2f5-122">維護模式更新是干擾性更新，例如磁碟韌體升級。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="9a2f5-123">這些更新需要 hello 裝置 toobe 放入維護模式。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-123">These updates require hello device toobe put into Maintenance mode.</span></span> <span data-ttu-id="9a2f5-124">如需詳細資訊，請參閱 [步驟 2：進入維護模式](#step2)。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="9a2f5-125">您無法使用 hello Azure 傳統入口網站 tooinstall 維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-125">You cannot use hello Azure classic portal tooinstall Maintenance mode updates.</span></span> <span data-ttu-id="9a2f5-126">您必須改用 Windows PowerShell for StorSimple。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="9a2f5-127">如需 tooinstall 維護模式更新的方式的詳細資訊，請參閱[透過 Windows PowerShell for StorSimple 安裝維護模式更新](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple)。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-127">For details on how tooinstall Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a2f5-128">維護模式更新必須個別套用 tooeach 控制站。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-128">Maintenance mode updates must be applied separately tooeach controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a><span data-ttu-id="9a2f5-129">安裝定期更新，透過 hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="9a2f5-129">Install regular updates via hello Azure classic portal</span></span>
<span data-ttu-id="9a2f5-130">您可以使用 hello Azure 傳統入口網站 tooapply 更新 tooyour StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-130">You can use hello Azure classic portal tooapply updates tooyour StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="9a2f5-131">透過 Windows PowerShell for StorSimple 安裝一般更新</span><span class="sxs-lookup"><span data-stu-id="9a2f5-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="9a2f5-132">或者，您可以使用 Windows PowerShell for StorSimple tooapply 一般 （一般模式） 的更新。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-132">Alternatively, you can use Windows PowerShell for StorSimple tooapply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a2f5-133">雖然您可以安裝使用 Windows PowerShell for StorSimple 的定期更新，但是我們強烈建議您安裝定期更新，透過 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through hello Azure classic portal.</span></span> <span data-ttu-id="9a2f5-134">預先檢查更新 1 開始，將會執行先前 tooinstalling 更新從 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-134">Beginning with Update 1, pre-checks will be performed prior tooinstalling updates from hello portal.</span></span> <span data-ttu-id="9a2f5-135">這些前置檢查可防止失敗，並確保提供更順暢的體驗。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="9a2f5-136">透過 Windows PowerShell for StorSimple 安裝維護模式更新</span><span class="sxs-lookup"><span data-stu-id="9a2f5-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="9a2f5-137">您可以使用 Windows PowerShell for StorSimple tooapply 維護模式更新 tooyour StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-137">You use Windows PowerShell for StorSimple tooapply Maintenance mode updates tooyour StorSimple device.</span></span> <span data-ttu-id="9a2f5-138">在此模式中，所有的 I/O 要求都會暫停。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="9a2f5-139">也會停止服務，例如非揮發性隨機存取記憶體 (NVRAM) 或 hello 叢集服務。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-139">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="9a2f5-140">這兩個控制站會在您進入或結束此模式時重新啟動。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="9a2f5-141">當您結束此模式中時，所有 hello 服務將會繼續，而且應該是狀況良好。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-141">When you exit this mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="9a2f5-142">(這可能需要數分鐘的時間)。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="9a2f5-143">如果您需要 tooapply 維護模式更新，您會收到 hello Azure 傳統入口網站透過警示您有必須安裝的更新。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-143">If you need tooapply Maintenance mode updates, you will receive an alert through hello Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="9a2f5-144">此警示將會包含使用 Windows PowerShell for StorSimple tooinstall hello 更新的指示。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-144">This alert will include instructions for using Windows PowerShell for StorSimple tooinstall hello updates.</span></span> <span data-ttu-id="9a2f5-145">更新您的裝置之後，使用 hello 相同程序 toochange hello 裝置 tooRegular 模式。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-145">After you update your device, use hello same procedure toochange hello device tooRegular mode.</span></span> <span data-ttu-id="9a2f5-146">如需逐步指示，請參閱 [步驟 4：結束維護模式](#step4)。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="9a2f5-147">之前進入維護模式，請確認兩個裝置控制器會處於狀況良好，藉由檢查 hello**硬體狀態**上 hello**維護**hello Azure 傳統入口網站中的頁面。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking hello **Hardware Status** on hello **Maintenance** page in hello Azure classic portal.</span></span> <span data-ttu-id="9a2f5-148">如果 hello 控制器未正常運作，請連絡 Microsoft 支援 hello 接下來的步驟。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-148">If hello controller is not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="9a2f5-149">如需詳細資訊，請移 tooContact Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-149">For more information, go tooContact Microsoft Support.</span></span> 
> * <span data-ttu-id="9a2f5-150">當您處於維護模式時，您需要 tooapply hello 更新第一次一個控制站上，然後在 hello 另一個控制器。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-150">When you are in Maintenance mode, you need tooapply hello update first on one controller and then on hello other controller.</span></span>
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a><span data-ttu-id="9a2f5-151">步驟 1： 連接 toohello 序列主控台<a name="step1"></span><span class="sxs-lookup"><span data-stu-id="9a2f5-151">Step 1: Connect toohello serial console <a name="step1"></span></span>
<span data-ttu-id="9a2f5-152">首先，使用應用程式，例如 PuTTY tooaccess hello 序列主控台。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-152">First, use an application such as PuTTY tooaccess hello serial console.</span></span> <span data-ttu-id="9a2f5-153">hello 下列程序說明如何 toouse PuTTY tooconnect toohello 序列主控台。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-153">hello following procedure explains how toouse PuTTY tooconnect toohello serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="9a2f5-154">步驟 2：進入維護模式 <a name="step2"></span><span class="sxs-lookup"><span data-stu-id="9a2f5-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="9a2f5-155">連接 toohello 主控台之後，判斷是否有更新 tooinstall，然後輸入 維護模式 tooinstall 它們。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-155">After you connect toohello console, determine whether there are updates tooinstall, and enter Maintenance mode tooinstall them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="9a2f5-156">步驟 3：安裝更新 <a name="step3"></span><span class="sxs-lookup"><span data-stu-id="9a2f5-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="9a2f5-157">接下來，安裝您的更新。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="9a2f5-158">步驟 4：結束維護模式 <a name="step4"></span><span class="sxs-lookup"><span data-stu-id="9a2f5-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="9a2f5-159">最後，結束維護模式。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="9a2f5-160">透過 Windows PowerShell for StorSimple 安裝 Hotfix</span><span class="sxs-lookup"><span data-stu-id="9a2f5-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="9a2f5-161">不同於 Microsoft Azure StorSimple 的更新，Hotfix 是從共用資料夾進行安裝的。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="9a2f5-162">和更新一樣，有兩種類型的 Hotfix：</span><span class="sxs-lookup"><span data-stu-id="9a2f5-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="9a2f5-163">一般的 Hotfix</span><span class="sxs-lookup"><span data-stu-id="9a2f5-163">Regular hotfixes</span></span> 
* <span data-ttu-id="9a2f5-164">維護模式的 Hotfix</span><span class="sxs-lookup"><span data-stu-id="9a2f5-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="9a2f5-165">hello 下列程序說明如何 toouse Windows PowerShell for StorSimple tooinstall 規則和維護模式 hotfix。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-165">hello following procedures explain how toouse Windows PowerShell for StorSimple tooinstall regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a><span data-ttu-id="9a2f5-166">發生什麼事 tooupdates，如果您執行原廠重設的 hello 裝置？</span><span class="sxs-lookup"><span data-stu-id="9a2f5-166">What happens tooupdates if you perform a factory reset of hello device?</span></span>
<span data-ttu-id="9a2f5-167">如果裝置重設 toofactory 設定，然後所有 hello 更新都都將遺失。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-167">If a device is reset toofactory settings, then all hello updates are lost.</span></span> <span data-ttu-id="9a2f5-168">Hello 原廠重設裝置在註冊及設定之後，您必須將安裝更新 toomanually 透過 hello Azure 傳統入口網站及/或 Windows PowerShell for StorSimple。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-168">After hello factory-reset device is registered and configured, you will need toomanually install updates through hello Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="9a2f5-169">如需原廠重設的詳細資訊，請參閱[hello 裝置 toofactory 預設設定重設](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings)。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-169">For more information about factory reset, see [Reset hello device toofactory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a2f5-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9a2f5-170">Next steps</span></span>
* <span data-ttu-id="9a2f5-171">深入了解[使用 Windows PowerShell for StorSimple tooadminister StorSimple 裝置](storsimple-windows-powershell-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-171">Learn more about [using Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="9a2f5-172">深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="9a2f5-172">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

