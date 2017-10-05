---
title: "PowerShell for StorSimple 裝置管理 | Microsoft Docs"
description: "了解如何使用 Windows PowerShell for StorSimple 管理 StorSimple 裝置。"
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
ms.date: 04/03/2017
ms.author: alkohli@microsoft.com
ms.openlocfilehash: 89e1054117f19e787da5330932021351fb016209
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-windows-powershell-for-storsimple-to-administer-your-device"></a><span data-ttu-id="7880c-103">使用 Windows PowerShell for StorSimple 管理您的裝置</span><span class="sxs-lookup"><span data-stu-id="7880c-103">Use Windows PowerShell for StorSimple to administer your device</span></span>

## <a name="overview"></a><span data-ttu-id="7880c-104">概觀</span><span class="sxs-lookup"><span data-stu-id="7880c-104">Overview</span></span>

<span data-ttu-id="7880c-105">Windows PowerShell for StorSimple 提供命令列介面，可讓您用來管理 Microsoft Azure StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="7880c-105">Windows PowerShell for StorSimple provides a command-line interface that you can use to manage your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="7880c-106">一如其名，它是 Windows PowerShell 型的命令列介面，建置在有限制的 Runspace 之中。</span><span class="sxs-lookup"><span data-stu-id="7880c-106">As the name suggests, it is a Windows PowerShell-based, command-line interface that is built in a constrained runspace.</span></span> <span data-ttu-id="7880c-107">從命令列使用者的觀點來看，有限制的 Runspace 就像是 Windows PowerShell 的受限版本。</span><span class="sxs-lookup"><span data-stu-id="7880c-107">From the perspective of the user at the command line, a constrained runspace appears as a restricted version of Windows PowerShell.</span></span> <span data-ttu-id="7880c-108">這個介面具備 Windows PowerShell 的一些基本功能，同時又具有額外的專用 Cmdlet，相互搭配來管理 Microsoft Azure StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="7880c-108">While maintaining some of the basic capabilities of Windows PowerShell, this interface has additional dedicated cmdlets that are geared towards managing your Microsoft Azure StorSimple device.</span></span>

<span data-ttu-id="7880c-109">本文描述 Windows PowerShell for StorSimple 的功能，包括如何與此介面連線，以及使用此介面可執行之工作流程逐步程序的連結。</span><span class="sxs-lookup"><span data-stu-id="7880c-109">This article describes the Windows PowerShell for StorSimple features, including how you can connect to this interface, and contains links to step-by-step procedures or workflows that you can perform using this interface.</span></span> <span data-ttu-id="7880c-110">工作流程包含如何註冊您的裝置、在裝置上設定網路介面、安裝需要裝置處於維護模式的更新、變更裝置狀態、疑難排解您可能會遇到的任何問題。</span><span class="sxs-lookup"><span data-stu-id="7880c-110">The workflows include how to register your device, configure the network interface on your device, install updates that require the device to be in maintenance mode, change the device state, and troubleshoot any issues that you may experience.</span></span>

<span data-ttu-id="7880c-111">閱讀本文之後，您將能夠：</span><span class="sxs-lookup"><span data-stu-id="7880c-111">After reading this article, you will be able to:</span></span>

* <span data-ttu-id="7880c-112">使用 Windows PowerShell for StorSimple 連線至 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="7880c-112">Connect to your StorSimple device using Windows PowerShell for StorSimple.</span></span>
* <span data-ttu-id="7880c-113">使用 Windows PowerShell for StorSimple 管理 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="7880c-113">Administer your StorSimple device using Windows PowerShell for StorSimple.</span></span>
* <span data-ttu-id="7880c-114">在 Windows PowerShell for StorSimple 中取得說明。</span><span class="sxs-lookup"><span data-stu-id="7880c-114">Get help in Windows PowerShell for StorSimple.</span></span>

> [!NOTE]
> * <span data-ttu-id="7880c-115">Windows PowerShell for StorSimple 的 Cmdlet 可讓您從序列主控台管理 StorSimple 裝置或透過「Windows PowerShell 遠端」進行管理。</span><span class="sxs-lookup"><span data-stu-id="7880c-115">Windows PowerShell for StorSimple cmdlets allow you to manage your StorSimple device from a serial console or remotely via Windows PowerShell remoting.</span></span> <span data-ttu-id="7880c-116">如需此介面可使用的各個 Cmdlet 的詳細資訊，請移至 [Windows PowerShell for StorSimple 的 Cmdlet 參考資料](https://technet.microsoft.com/library/dn688168.aspx).</span><span class="sxs-lookup"><span data-stu-id="7880c-116">For more information about each of the individual cmdlets that can be used in this interface, go to [cmdlet reference for Windows PowerShell for StorSimple](https://technet.microsoft.com/library/dn688168.aspx).</span></span>
> * <span data-ttu-id="7880c-117">Azure PowerShell StorSimple 的 Cmdlet 是另一組不同的指令程式，可讓您從命令列將 StorSimple 服務層級和移轉工作自動化。</span><span class="sxs-lookup"><span data-stu-id="7880c-117">The Azure PowerShell StorSimple cmdlets are a different collection of cmdlets that allow you to automate StorSimple service-level and migration tasks from the command line.</span></span> <span data-ttu-id="7880c-118">如需 Azure PowerShell Cmdlet for StorSimple 的詳細資訊，請移至 [Azure StorSimple Cmdlet 參考資料](https://docs.microsoft.com/powershell/servicemanagement/azure.storsimple/v3.1.0/azure.storsimple)。</span><span class="sxs-lookup"><span data-stu-id="7880c-118">For more information about the Azure PowerShell cmdlets for StorSimple, go to the [Azure StorSimple cmdlet reference](https://docs.microsoft.com/powershell/servicemanagement/azure.storsimple/v3.1.0/azure.storsimple).</span></span>


<span data-ttu-id="7880c-119">您可以使用下列方法之一存取 Windows PowerShell for StorSimple：</span><span class="sxs-lookup"><span data-stu-id="7880c-119">You can access the Windows PowerShell for StorSimple using one of the following methods:</span></span>

* [<span data-ttu-id="7880c-120">連線至 StorSimple 裝置序列主控台</span><span class="sxs-lookup"><span data-stu-id="7880c-120">Connect to StorSimple device serial console</span></span>](#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)
* [<span data-ttu-id="7880c-121">使用 Windows PowerShell 遠端連線至 StorSimple</span><span class="sxs-lookup"><span data-stu-id="7880c-121">Connect remotely to StorSimple using Windows PowerShell</span></span>](#connect-remotely-to-storsimple-using-windows-powershell-for-storsimple)

## <a name="connect-to-windows-powershell-for-storsimple-via-the-device-serial-console"></a><span data-ttu-id="7880c-122">透過裝置序列主控台連線至 Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="7880c-122">Connect to Windows PowerShell for StorSimple via the device serial console</span></span>

<span data-ttu-id="7880c-123">您可以 [下載 PuTTY](http://www.putty.org/) 或類似的終端機模擬軟體，以連線至 Windows PowerShell for StorSimple。</span><span class="sxs-lookup"><span data-stu-id="7880c-123">You can [download PuTTY](http://www.putty.org/) or similar terminal emulation software to connect to Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="7880c-124">您需要將 PuTTY 設定為專門存取 Microsoft Azure StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="7880c-124">You need to configure PuTTY specifically to access the Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="7880c-125">下列主題包含有關如何設定 PuTTy 並連接至裝置的詳細步驟。</span><span class="sxs-lookup"><span data-stu-id="7880c-125">The following topics contain detailed steps about how to configure PuTTy and connect to the device.</span></span> <span data-ttu-id="7880c-126">並且說明序列主控台中的各種功能表選項。</span><span class="sxs-lookup"><span data-stu-id="7880c-126">Various menu options in the serial console are also explained.</span></span>

### <a name="putty-settings"></a><span data-ttu-id="7880c-127">PuTTY 設定</span><span class="sxs-lookup"><span data-stu-id="7880c-127">PuTTY settings</span></span>

<span data-ttu-id="7880c-128">請確定您使用下列的 PuTTY 設定從序列主控台連線到 Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="7880c-128">Make sure that you use the following PuTTY settings to connect to the Windows PowerShell interface from the serial console.</span></span>

#### <a name="to-configure-putty"></a><span data-ttu-id="7880c-129">設定 PuTTY</span><span class="sxs-lookup"><span data-stu-id="7880c-129">To configure PuTTY</span></span>

1. <span data-ttu-id="7880c-130">在 PuTTY [重新設定] 對話方塊的 [類別] 窗格中，選取 [鍵盤]。</span><span class="sxs-lookup"><span data-stu-id="7880c-130">In the PuTTY **Reconfiguration** dialog box, in the **Category** pane, select **Keyboard**.</span></span>
2. <span data-ttu-id="7880c-131">請確定已選取下列選項 (當您啟動新的工作階段時，這些是預設設定)。</span><span class="sxs-lookup"><span data-stu-id="7880c-131">Make sure that the following options are selected (these are the default settings when you start a new session).</span></span>
   
   | <span data-ttu-id="7880c-132">鍵盤項目</span><span class="sxs-lookup"><span data-stu-id="7880c-132">Keyboard item</span></span> | <span data-ttu-id="7880c-133">選取</span><span class="sxs-lookup"><span data-stu-id="7880c-133">Select</span></span> |
   | --- | --- |
   | <span data-ttu-id="7880c-134">退格鍵</span><span class="sxs-lookup"><span data-stu-id="7880c-134">Backspace key</span></span> |<span data-ttu-id="7880c-135">Control-?</span><span class="sxs-lookup"><span data-stu-id="7880c-135">Control-?</span></span> <span data-ttu-id="7880c-136">(127)</span><span class="sxs-lookup"><span data-stu-id="7880c-136">(127)</span></span> |
   | <span data-ttu-id="7880c-137">Home 和 End 按鍵</span><span class="sxs-lookup"><span data-stu-id="7880c-137">Home and End keys</span></span> |<span data-ttu-id="7880c-138">標準</span><span class="sxs-lookup"><span data-stu-id="7880c-138">Standard</span></span> |
   | <span data-ttu-id="7880c-139">功能鍵和數字鍵台</span><span class="sxs-lookup"><span data-stu-id="7880c-139">Function keys and keypad</span></span> |<span data-ttu-id="7880c-140">ESC[n~</span><span class="sxs-lookup"><span data-stu-id="7880c-140">ESC[n~</span></span> |
   | <span data-ttu-id="7880c-141">方向鍵的初始狀態</span><span class="sxs-lookup"><span data-stu-id="7880c-141">Initial state of cursor keys</span></span> |<span data-ttu-id="7880c-142">正常</span><span class="sxs-lookup"><span data-stu-id="7880c-142">Normal</span></span> |
   | <span data-ttu-id="7880c-143">數字鍵台的初始狀態</span><span class="sxs-lookup"><span data-stu-id="7880c-143">Initial state of numeric keypad</span></span> |<span data-ttu-id="7880c-144">正常</span><span class="sxs-lookup"><span data-stu-id="7880c-144">Normal</span></span> |
   | <span data-ttu-id="7880c-145">啟用額外的鍵盤功能</span><span class="sxs-lookup"><span data-stu-id="7880c-145">Enable extra keyboard features</span></span> |<span data-ttu-id="7880c-146">Control-Alt 和 AltGr 不同</span><span class="sxs-lookup"><span data-stu-id="7880c-146">Control-Alt is different from AltGr</span></span> |
   
    ![支援的 PuTTY 設定](./media/storsimple-windows-powershell-administration/IC740877.png)
3. <span data-ttu-id="7880c-148">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="7880c-148">Click **Apply**.</span></span>
4. <span data-ttu-id="7880c-149">在 [類別] 窗格中，選取 [轉譯]。</span><span class="sxs-lookup"><span data-stu-id="7880c-149">In the **Category** pane, select **Translation**.</span></span>
5. <span data-ttu-id="7880c-150">在 [遠端字元集] 清單方塊中，選取 [UTF-8]。</span><span class="sxs-lookup"><span data-stu-id="7880c-150">In the **Remote character set** list box, select **UTF-8**.</span></span>
6. <span data-ttu-id="7880c-151">在 [線條繪圖字元的處理] 下，選取 [使用 Unicode 線條繪圖字碼指標]。</span><span class="sxs-lookup"><span data-stu-id="7880c-151">Under **Handling of line drawing characters**, select **Use Unicode line drawing code points**.</span></span> <span data-ttu-id="7880c-152">下列螢幕擷取畫面顯示正確的 PuTTY 選取。</span><span class="sxs-lookup"><span data-stu-id="7880c-152">The following screenshot shows the correct PuTTY selections.</span></span>
   
    ![UTF PuTTY 設定](./media/storsimple-windows-powershell-administration/IC740878.png)
7. <span data-ttu-id="7880c-154">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="7880c-154">Click **Apply**.</span></span>

<span data-ttu-id="7880c-155">現在，您可以執行下列步驟，來使用 PuTTY 連線至裝置序列主控台。</span><span class="sxs-lookup"><span data-stu-id="7880c-155">You can now use PuTTY to connect to the device serial console by doing the following steps.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="about-the-serial-console"></a><span data-ttu-id="7880c-156">關於序列主控台</span><span class="sxs-lookup"><span data-stu-id="7880c-156">About the serial console</span></span>

<span data-ttu-id="7880c-157">當您透過序列主控台存取 StorSimple 裝置的 Windows PowerShell 介面時，會顯示一則橫幅訊息，後面接著功能表選項。</span><span class="sxs-lookup"><span data-stu-id="7880c-157">When you access the Windows PowerShell interface of your StorSimple device through the serial console, a banner message is presented, followed by menu options.</span></span>

<span data-ttu-id="7880c-158">橫幅訊息包含基本的 StorSimple 裝置資訊，例如：型號、名稱、已安裝的軟體版本、您要存取的控制器的狀態等。</span><span class="sxs-lookup"><span data-stu-id="7880c-158">The banner message contains basic StorSimple device information such as the model, name, installed software version, and status of the controller you are accessing.</span></span> <span data-ttu-id="7880c-159">下圖為橫幅訊息的範例。</span><span class="sxs-lookup"><span data-stu-id="7880c-159">The following image shows an example of a banner message.</span></span>

![序列橫幅訊息](./media/storsimple-windows-powershell-administration/IC741098.png)

> [!IMPORTANT]
> <span data-ttu-id="7880c-161">您可以從橫幅訊息辨別出連線的控制器是「主動」或「被動」。</span><span class="sxs-lookup"><span data-stu-id="7880c-161">You can use the banner message to identify whether the controller you are connected to is _Active_ or _Passive_.</span></span>

<span data-ttu-id="7880c-162">下圖顯示序列主控台功能表中可用的各種 Runspace 選項。</span><span class="sxs-lookup"><span data-stu-id="7880c-162">The following image shows the various runspace options that are available in the serial console menu.</span></span>

![註冊裝置 2](./media/storsimple-windows-powershell-administration/IC740906.png)

<span data-ttu-id="7880c-164">您可選擇下列設定：</span><span class="sxs-lookup"><span data-stu-id="7880c-164">You can choose from the following settings:</span></span>

1. <span data-ttu-id="7880c-165">**登入並具備完整存取權** 此選項可讓您連線 (使用適當的認證) 至本機控制器上的 **SSAdminConsole** Runspace。</span><span class="sxs-lookup"><span data-stu-id="7880c-165">**Log in with full access** This option allows you to connect (with the proper credentials) to the **SSAdminConsole** runspace on the local controller.</span></span> <span data-ttu-id="7880c-166">(本機控制器是您目前正透過 StorSimple 裝置序列主控台存取的控制器)。也可使用此選項讓「Microsoft 支援」存取不受限制的 Runspace (支援工作階段)，以對任何可能的裝置問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="7880c-166">(The local controller is the controller that you are currently accessing through the serial console of your StorSimple device.) This option can also be used to allow Microsoft Support to access unrestricted runspace (a support session) to troubleshoot any possible device issues.</span></span> <span data-ttu-id="7880c-167">使用選項 1 登入之後，您可以允許 Microsoft 支援工程師執行特定 Cmdlet 去存取不受限制的 Runspace。</span><span class="sxs-lookup"><span data-stu-id="7880c-167">After you use option 1 to log on, you can allow the Microsoft Support engineer to access unrestricted runspace by running a specific cmdlet.</span></span> <span data-ttu-id="7880c-168">如需詳細資訊，請參閱 [啟動支援工作階段](storsimple-8000-contact-microsoft-support.md#start-a-support-session-in-windows-powershell-for-storsimple)。</span><span class="sxs-lookup"><span data-stu-id="7880c-168">For details, refer to [Start a support session](storsimple-8000-contact-microsoft-support.md#start-a-support-session-in-windows-powershell-for-storsimple).</span></span>
   
2. <span data-ttu-id="7880c-169">**登入對等控制器並具備完整存取權** 此選項和選項 1 相同，不過是讓您連線 (使用適當的認證) 至對等控制器上的 **SSAdminConsole** Runspace。</span><span class="sxs-lookup"><span data-stu-id="7880c-169">**Log in to peer controller with full access** This option is the same as option 1, except that you can connect (with the proper credentials) to the **SSAdminConsole** runspace on the peer controller.</span></span> <span data-ttu-id="7880c-170">因為 StorSimple 裝置是高可用性的裝置，具有兩個主動-被動組態的控制器；對等指的是您透過序列主控台存取的裝置中的其他控制器。</span><span class="sxs-lookup"><span data-stu-id="7880c-170">Because the StorSimple device is a high availability device with two controllers in an active-passive configuration, peer refers to the other controller in the device that you are accessing through the serial console).</span></span>
   <span data-ttu-id="7880c-171">和選項 1 類似，此選項也可用於讓「Microsoft 支援」存取對等控制器上不受限制的 Runspace。</span><span class="sxs-lookup"><span data-stu-id="7880c-171">Similar to option 1, this option can also be used to allow Microsoft Support to access unrestricted runspace on a peer controller.</span></span>

3. <span data-ttu-id="7880c-172">**連線並具備有限存取權** 此選項用於在有限制的模式下存取 Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="7880c-172">**Connect with limited access** This option is used to access Windows PowerShell interface in limited mode.</span></span> <span data-ttu-id="7880c-173">系統不會提示您輸入存取認證。</span><span class="sxs-lookup"><span data-stu-id="7880c-173">You are not prompted for access credentials.</span></span> <span data-ttu-id="7880c-174">相較於選項 1 和 2，此選項會連線至更多限制的 Runspace。</span><span class="sxs-lookup"><span data-stu-id="7880c-174">This option connects to a more restricted runspace compared to options 1 and 2.</span></span>  <span data-ttu-id="7880c-175">可透過選項 1 執行但在此 Runspace 中「無法」 執行的一些工作包括：</span><span class="sxs-lookup"><span data-stu-id="7880c-175">Some of the tasks that are available through option 1 that **cannot* be performed in this runspace are:</span></span>
   
   * <span data-ttu-id="7880c-176">重設為原廠設定</span><span class="sxs-lookup"><span data-stu-id="7880c-176">Reset to the factory settings</span></span>
   * <span data-ttu-id="7880c-177">變更密碼</span><span class="sxs-lookup"><span data-stu-id="7880c-177">Change the password</span></span>
   * <span data-ttu-id="7880c-178">啟用或停用支援存取</span><span class="sxs-lookup"><span data-stu-id="7880c-178">Enable or disable support access</span></span>
   * <span data-ttu-id="7880c-179">套用更新</span><span class="sxs-lookup"><span data-stu-id="7880c-179">Apply updates</span></span>
   * <span data-ttu-id="7880c-180">安裝 Hotfix</span><span class="sxs-lookup"><span data-stu-id="7880c-180">Install hotfixes</span></span>

    > [!NOTE]
    > <span data-ttu-id="7880c-181">如果您忘記裝置管理員密碼並透過選項 1 或 2無法連線，這是慣用的選項。</span><span class="sxs-lookup"><span data-stu-id="7880c-181">This is the preferred option if you have forgotten the device administrator password and cannot connect through option 1 or 2.</span></span>

4. <span data-ttu-id="7880c-182">**變更語言** 此選項可讓您變更 Windows PowerShell 介面上的顯示語言。</span><span class="sxs-lookup"><span data-stu-id="7880c-182">**Change language** This option allows you to change the display language on the Windows PowerShell interface.</span></span> <span data-ttu-id="7880c-183">支援的語言有英文、日文、俄文、法文、南韓文、西班牙文、義大利文、德文、中文和巴西葡萄牙文。</span><span class="sxs-lookup"><span data-stu-id="7880c-183">The languages supported are English, Japanese, Russian, French, South Korean, Spanish, Italian, German, Chinese, and Brazilian Portuguese.</span></span>

## <a name="connect-remotely-to-storsimple-using-windows-powershell-for-storsimple"></a><span data-ttu-id="7880c-184">使用 Windows PowerShell 遠端連線至 StorSimple</span><span class="sxs-lookup"><span data-stu-id="7880c-184">Connect remotely to StorSimple using Windows PowerShell for StorSimple</span></span>

<span data-ttu-id="7880c-185">使用 Windows PowerShell 遠端連線到 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="7880c-185">You can use Windows PowerShell remoting to connect to your StorSimple device.</span></span> <span data-ttu-id="7880c-186">當您以這種方式連線時，將不會看到功能表。</span><span class="sxs-lookup"><span data-stu-id="7880c-186">When you connect this way, you will not see a menu.</span></span> <span data-ttu-id="7880c-187">(只有在您使用裝置上的序列主控台來連線時，才會看到功能表。</span><span class="sxs-lookup"><span data-stu-id="7880c-187">(You see a menu only if you use the serial console on the device to connect.</span></span> <span data-ttu-id="7880c-188">遠端連線會直接帶您前往與序列主控台上「選項 1：完整存取」對等的地方。)使用 Windows PowerShell 遠端連線到特定的 Runspace。</span><span class="sxs-lookup"><span data-stu-id="7880c-188">Connecting remotely takes you directly to the equivalent of "option 1 – full access” on the serial console.) With Windows PowerShell remoting, you connect to a specific runspace.</span></span> <span data-ttu-id="7880c-189">您也可以指定顯示語言。</span><span class="sxs-lookup"><span data-stu-id="7880c-189">You can also specify the display language.</span></span>

<span data-ttu-id="7880c-190">您使用序列主控台功能表中的 [變更語言]  選項設定的語言，和顯示語言無關。</span><span class="sxs-lookup"><span data-stu-id="7880c-190">The display language is independent of the language that you set by using the **Change Language** option in the serial console menu.</span></span> <span data-ttu-id="7880c-191">若未指定您的連線裝置的地區設定，遠端 PowerShell 將會自動為其挑選。</span><span class="sxs-lookup"><span data-stu-id="7880c-191">Remote PowerShell will automatically pick up the locale of the device you are connecting from if none is specified.</span></span>

> [!NOTE]
> <span data-ttu-id="7880c-192">如果您使用 Microsoft Azure 虛擬主機和 StorSimple 雲端設備，可以使用 Windows PowerShell 遠端和虛擬主機來連線至雲端設備。</span><span class="sxs-lookup"><span data-stu-id="7880c-192">If you are working with Microsoft Azure virtual hosts and StorSimple Cloud Appliances, you can use Windows PowerShell remoting and the virtual host to connect to the cloud appliance.</span></span> <span data-ttu-id="7880c-193">如果您已經在主機上設定共用位置，來儲存 Windows PowerShell 工作階段的資訊，請注意「所有人」主體只能包含已經過驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="7880c-193">If you have set up a share location on the host on which to save information from the Windows PowerShell session, you should be aware that the _Everyone_ principal includes only authenticated users.</span></span> <span data-ttu-id="7880c-194">因此，如果您將共用設定為允許「所有人」存取，且連線時未指定認證，則系統將會使用未經驗證的「匿名」主體，而您會看到錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="7880c-194">Therefore, if you have set up the share to allow access by _Everyone_ and you connect without specifying credentials, the unauthenticated Anonymous principal will be used and you will see an error.</span></span> <span data-ttu-id="7880c-195">若要修正此問題，在共用主機上您必須啟用「來賓」帳戶，然後給來賓帳戶完整存取權以進行共用，或您必須指定有效的認證以及 Windows PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="7880c-195">To fix this issue, on the share host you must enable the Guest account and then give the Guest account full access to the share or you must specify valid credentials along with the Windows PowerShell cmdlet.</span></span>


<span data-ttu-id="7880c-196">您可以透過 Windows PowerShell 遠端使用 HTTP 或 HTTPS 進行連線。</span><span class="sxs-lookup"><span data-stu-id="7880c-196">You can use HTTP or HTTPS to connect via Windows PowerShell remoting.</span></span> <span data-ttu-id="7880c-197">使用下列教學課程中的指示：</span><span class="sxs-lookup"><span data-stu-id="7880c-197">Use the instructions in the following tutorials:</span></span>

* [<span data-ttu-id="7880c-198">使用 HTTP 遠端連線</span><span class="sxs-lookup"><span data-stu-id="7880c-198">Connect remotely using HTTP</span></span>](storsimple-remote-connect.md#connect-through-http)
* [<span data-ttu-id="7880c-199">使用 HTTPS 遠端連線</span><span class="sxs-lookup"><span data-stu-id="7880c-199">Connect remotely using HTTPS</span></span>](storsimple-remote-connect.md#connect-through-https)

## <a name="connection-security-considerations"></a><span data-ttu-id="7880c-200">連線安全性考量</span><span class="sxs-lookup"><span data-stu-id="7880c-200">Connection security considerations</span></span>

<span data-ttu-id="7880c-201">當您決定如何連線到 Windows PowerShell for StorSimple 時，請考慮下列事項：</span><span class="sxs-lookup"><span data-stu-id="7880c-201">When you are deciding how to connect to Windows PowerShell for StorSimple, consider the following:</span></span>

* <span data-ttu-id="7880c-202">直接連線至裝置序列主控台是安全的，但透過網路交換器連線至序列主控台則否。</span><span class="sxs-lookup"><span data-stu-id="7880c-202">Connecting directly to the device serial console is secure, but connecting to the serial console over network switches is not.</span></span> <span data-ttu-id="7880c-203">透過網路交換器連線至裝置序列主控台時，請務必注意安全性風險。</span><span class="sxs-lookup"><span data-stu-id="7880c-203">Be cautious of the security risk when connecting to device serial over network switches.</span></span>
* <span data-ttu-id="7880c-204">透過 HTTP 工作階段連線的安全性，比在網路上透過序列主控台連線更高。</span><span class="sxs-lookup"><span data-stu-id="7880c-204">Connecting through an HTTP session might offer more security than connecting through the serial console over network.</span></span> <span data-ttu-id="7880c-205">雖然這不是最安全的方法，但在受信任的網路上是可接受的做法。</span><span class="sxs-lookup"><span data-stu-id="7880c-205">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>
* <span data-ttu-id="7880c-206">透過 HTTP 工作階段連線是我們建議，且最安全的選項。</span><span class="sxs-lookup"><span data-stu-id="7880c-206">Connecting through an HTTPS session is the most secure and the recommended option.</span></span>

## <a name="administer-your-storsimple-device-using-windows-powershell-for-storsimple"></a><span data-ttu-id="7880c-207">使用 Windows PowerShell for StorSimple 管理 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="7880c-207">Administer your StorSimple device using Windows PowerShell for StorSimple</span></span>

<span data-ttu-id="7880c-208">下表顯示所有一般管理工作及複雜工作流程 (可在您 StorSimple 裝置的 Windows PowerShell 介面執行) 的摘要。</span><span class="sxs-lookup"><span data-stu-id="7880c-208">The following table shows a summary of all the common management tasks and complex workflows that can be performed within the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="7880c-209">如需每個工作流程的詳細資訊，請按一下資料表中適當的項目。</span><span class="sxs-lookup"><span data-stu-id="7880c-209">For more information about each workflow, click the appropriate entry in the table.</span></span>

#### <a name="windows-powershell-for-storsimple-workflows"></a><span data-ttu-id="7880c-210">Windows PowerShell for StorSimple 的工作流程</span><span class="sxs-lookup"><span data-stu-id="7880c-210">Windows PowerShell for StorSimple workflows</span></span>

| <span data-ttu-id="7880c-211">如果您想要執行此動作...</span><span class="sxs-lookup"><span data-stu-id="7880c-211">If you want to do this ...</span></span> | <span data-ttu-id="7880c-212">使用此程序。</span><span class="sxs-lookup"><span data-stu-id="7880c-212">Use this procedure.</span></span> |
| --- | --- |
| <span data-ttu-id="7880c-213">登記裝置</span><span class="sxs-lookup"><span data-stu-id="7880c-213">Register your device</span></span> |[<span data-ttu-id="7880c-214">使用 Windows PowerShell for StorSimple 設定和註冊裝置</span><span class="sxs-lookup"><span data-stu-id="7880c-214">Configure and register the device using Windows PowerShell for StorSimple</span></span>](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |
| <span data-ttu-id="7880c-215">設定 Web Proxy</span><span class="sxs-lookup"><span data-stu-id="7880c-215">Configure web proxy</span></span></br><span data-ttu-id="7880c-216">檢視 Web Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="7880c-216">View web proxy settings</span></span> |[<span data-ttu-id="7880c-217">為 StorSimple 裝置設定 Web Proxy</span><span class="sxs-lookup"><span data-stu-id="7880c-217">Configure web proxy for your StorSimple device</span></span>](storsimple-8000-configure-web-proxy.md) |
| <span data-ttu-id="7880c-218">修改裝置上的 DATA 0 網路介面設定</span><span class="sxs-lookup"><span data-stu-id="7880c-218">Modify DATA 0 network interface settings on your device</span></span> |[<span data-ttu-id="7880c-219">修改 StorSimple 裝置上的 DATA 0 網路介面</span><span class="sxs-lookup"><span data-stu-id="7880c-219">Modify DATA 0 network interface for your StorSimple device</span></span>](storsimple-8000-modify-data-0.md) |
| <span data-ttu-id="7880c-220">停止控制器 </span><span class="sxs-lookup"><span data-stu-id="7880c-220">Stop a controller</span></span> </br> <span data-ttu-id="7880c-221">重新啟動或關閉控制器</span><span class="sxs-lookup"><span data-stu-id="7880c-221">Restart or shut down a controller</span></span> </br> <span data-ttu-id="7880c-222">關閉裝置</span><span class="sxs-lookup"><span data-stu-id="7880c-222">Shut down a device</span></span></br><span data-ttu-id="7880c-223">將裝置重設為出廠預設設定。</span><span class="sxs-lookup"><span data-stu-id="7880c-223">Reset the device to factory default settings</span></span> |[<span data-ttu-id="7880c-224">管理裝置控制器</span><span class="sxs-lookup"><span data-stu-id="7880c-224">Manage device controllers</span></span>](storsimple-8000-manage-device-controller.md) |
| <span data-ttu-id="7880c-225">安裝維護模式更新和 Hotfixe</span><span class="sxs-lookup"><span data-stu-id="7880c-225">Install maintenance mode updates and hotfixes</span></span> |[<span data-ttu-id="7880c-226">更新您的裝置</span><span class="sxs-lookup"><span data-stu-id="7880c-226">Update your device</span></span>](storsimple-update-device.md) |
| <span data-ttu-id="7880c-227">進入維護模式 </span><span class="sxs-lookup"><span data-stu-id="7880c-227">Enter maintenance mode</span></span> </br><span data-ttu-id="7880c-228">結束維護模式</span><span class="sxs-lookup"><span data-stu-id="7880c-228">Exit maintenance mode</span></span> |[<span data-ttu-id="7880c-229">StorSimple 裝置模式</span><span class="sxs-lookup"><span data-stu-id="7880c-229">StorSimple device modes</span></span>](storsimple-8000-device-modes.md) |
| <span data-ttu-id="7880c-230">建立支援封裝 </span><span class="sxs-lookup"><span data-stu-id="7880c-230">Create a Support package</span></span></br><span data-ttu-id="7880c-231">解密並編輯支援封裝</span><span class="sxs-lookup"><span data-stu-id="7880c-231">Decrypt and edit a support package</span></span> |[<span data-ttu-id="7880c-232">建立及管理支援封裝</span><span class="sxs-lookup"><span data-stu-id="7880c-232">Create and manage a Support package</span></span>](storsimple-8000-create-manage-support-package.md) |
| <span data-ttu-id="7880c-233">啟動支援工作階段</span><span class="sxs-lookup"><span data-stu-id="7880c-233">Start a Support session</span></span></br> |[<span data-ttu-id="7880c-234">在 Windows PowerShell for StorSimple 中啟動支援工作階段</span><span class="sxs-lookup"><span data-stu-id="7880c-234">Start a support session in Windows PowerShell for StorSimple</span></span>](storsimple-8000-create-manage-support-package.md#create-a-support-package) |

## <a name="get-help-in-windows-powershell-for-storsimple"></a><span data-ttu-id="7880c-235">在 Windows PowerShell for StorSimple 中取得說明</span><span class="sxs-lookup"><span data-stu-id="7880c-235">Get Help in Windows PowerShell for StorSimple</span></span>

<span data-ttu-id="7880c-236">在 Windows PowerShell for StorSimple 中也有 Cmdlet 的說明。</span><span class="sxs-lookup"><span data-stu-id="7880c-236">In Windows PowerShell for StorSimple, cmdlet Help is available.</span></span> <span data-ttu-id="7880c-237">此說明的最新版本也會線上提供，供您更新您系統上的說明。</span><span class="sxs-lookup"><span data-stu-id="7880c-237">An online, up-to-date version of this Help is also available, which you can use to update the Help on your system.</span></span>

<span data-ttu-id="7880c-238">在此介面中取得說明和在 Windows PowerShell 中類似，而且大部分與說明相關的 Cmdlet 都能用。</span><span class="sxs-lookup"><span data-stu-id="7880c-238">Getting Help in this interface is similar to that in Windows PowerShell, and most of the Help-related cmdlets will work.</span></span> <span data-ttu-id="7880c-239">您可以在 TechNet Library 中找到 Windows PowerShell 的線上說明： [Windows PowerShell 的指令碼撰寫](http://go.microsoft.com/fwlink/?LinkID=108518)。</span><span class="sxs-lookup"><span data-stu-id="7880c-239">You can find Help for Windows PowerShell online in the TechNet Library: [Scripting with Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=108518).</span></span>

<span data-ttu-id="7880c-240">以下是此 Windows PowerShell 介面中各種說明類型的簡短描述，包括如何更新說明。</span><span class="sxs-lookup"><span data-stu-id="7880c-240">The following is a brief description of the types of Help for this Windows PowerShell interface, including how to update the Help.</span></span>

### <a name="to-get-help-for-a-cmdlet"></a><span data-ttu-id="7880c-241">取得 Cmdlet 的說明</span><span class="sxs-lookup"><span data-stu-id="7880c-241">To get help for a cmdlet</span></span>

* <span data-ttu-id="7880c-242">使用下列命令可取得特定 Cmdlet 或功能的說明：`Get-Help <cmdlet-name>`</span><span class="sxs-lookup"><span data-stu-id="7880c-242">To get Help for any cmdlet or function, use the following command: `Get-Help <cmdlet-name>`</span></span>
* <span data-ttu-id="7880c-243">若要取得任何 Cmdlet 的線上說明，請使用前述 Cmdlet 搭配 `-Online` 參數：`Get-Help <cmdlet-name> -Online`</span><span class="sxs-lookup"><span data-stu-id="7880c-243">To get online Help for any cmdlet, use the previous cmdlet with the `-Online` parameter: `Get-Help <cmdlet-name> -Online`</span></span>
* <span data-ttu-id="7880c-244">如需完整說明，可以使用 `–Full` 參數，如需範例，則可使用 `–Examples` 參數。</span><span class="sxs-lookup"><span data-stu-id="7880c-244">For full Help, you can use the `–Full` parameter, and for examples, use the `–Examples` parameter.</span></span>

### <a name="to-update-help"></a><span data-ttu-id="7880c-245">更新說明</span><span class="sxs-lookup"><span data-stu-id="7880c-245">To update Help</span></span>

<span data-ttu-id="7880c-246">您可以輕鬆地更新 Windows PowerShell 介面中的說明。</span><span class="sxs-lookup"><span data-stu-id="7880c-246">You can easily update the Help in the Windows PowerShell interface.</span></span> <span data-ttu-id="7880c-247">請執行下列步驟更新您系統上的說明。</span><span class="sxs-lookup"><span data-stu-id="7880c-247">Perform the following steps to update the Help on your system.</span></span>

#### <a name="to-update-cmdlet-help"></a><span data-ttu-id="7880c-248">更新 Cmdlet 說明</span><span class="sxs-lookup"><span data-stu-id="7880c-248">To update cmdlet Help</span></span>
1. <span data-ttu-id="7880c-249">請使用 [ **以系統管理員身分執行** ] 選項啟動 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="7880c-249">Start Windows PowerShell with the **Run as administrator** option.</span></span>
2. <span data-ttu-id="7880c-250">在命令提示字元中，輸入：`Update-Help`</span><span class="sxs-lookup"><span data-stu-id="7880c-250">At the command prompt, type:  `Update-Help`</span></span>
3. <span data-ttu-id="7880c-251">將會安裝更新的說明檔。</span><span class="sxs-lookup"><span data-stu-id="7880c-251">The updated Help files will be installed.</span></span>
4. <span data-ttu-id="7880c-252">在說明檔案安裝之後，輸入： `Get-Help Get-Command`。</span><span class="sxs-lookup"><span data-stu-id="7880c-252">After the Help files are installed, type: `Get-Help Get-Command`.</span></span> <span data-ttu-id="7880c-253">將會顯示可用說明的 Cmdlet 清單。</span><span class="sxs-lookup"><span data-stu-id="7880c-253">This will display a list of cmdlets for which Help is available.</span></span>

> [!NOTE]
> <span data-ttu-id="7880c-254">若要取得 Runspace 中所有可用 Cmdlet 的清單，請登入對應的功能表選項並執行 `Get-Command` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="7880c-254">To get a list of all the available cmdlets in a runspace, log in to the corresponding menu option and run the `Get-Command` cmdlet.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7880c-255">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7880c-255">Next steps</span></span>

<span data-ttu-id="7880c-256">如果您在執行上述任何工作流程時遇到任何 StorSimple 裝置的問題，請參閱 [適用於疑難排解 StorSimple 部署的工具](storsimple-troubleshoot-deployment.md#tools-for-troubleshooting-storsimple-deployments)。</span><span class="sxs-lookup"><span data-stu-id="7880c-256">If you experience any issues with your StorSimple device when performing one of the above workflows, refer to [Tools for troubleshooting StorSimple deployments](storsimple-troubleshoot-deployment.md#tools-for-troubleshooting-storsimple-deployments).</span></span>

