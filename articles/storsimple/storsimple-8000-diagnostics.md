---
title: "aaaDiagnostics 工具 tootroubleshoot StorSimple 8000 裝置 |Microsoft 文件"
description: "描述 hello StorSimple 裝置模式，並說明如何 toouse Windows PowerShell for StorSimple toochange hello 裝置模式。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a><span data-ttu-id="f3035-103">使用 hello StorSimple 診斷工具 tootroubleshoot 8000 系列裝置的問題</span><span class="sxs-lookup"><span data-stu-id="f3035-103">Use hello StorSimple Diagnostics Tool tootroubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="f3035-104">概觀</span><span class="sxs-lookup"><span data-stu-id="f3035-104">Overview</span></span>

<span data-ttu-id="f3035-105">hello StorSimple 診斷工具診斷問題的相關的 toosystem、 效能、 網路和 StorSimple 裝置的硬體元件健全狀況。</span><span class="sxs-lookup"><span data-stu-id="f3035-105">hello StorSimple Diagnostics tool diagnoses issues related toosystem, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="f3035-106">hello 診斷工具可在各種情況中。</span><span class="sxs-lookup"><span data-stu-id="f3035-106">hello diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="f3035-107">這些案例包括工作負載規劃、 部署 StorSimple 裝置、 評估 hello 網路環境中，以及決定 hello 效能的操作的裝置。</span><span class="sxs-lookup"><span data-stu-id="f3035-107">These scenarios include workload planning, deploying a StorSimple device, assessing hello network environment, and determining hello performance of an operational device.</span></span> <span data-ttu-id="f3035-108">本文章提供 hello 診斷工具的概觀，並說明如何使用 hello 工具，StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="f3035-108">This article provides an overview of hello diagnostics tool and describes how hello tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="f3035-109">hello 診斷工具的目的主要是用於 StorSimple 8000 系列在內部部署的裝置 （8100 和 8600）。</span><span class="sxs-lookup"><span data-stu-id="f3035-109">hello diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="f3035-110">執行診斷工具</span><span class="sxs-lookup"><span data-stu-id="f3035-110">Run diagnostics tool</span></span>

<span data-ttu-id="f3035-111">此工具可以透過您的 StorSimple 裝置 hello Windows PowerShell 介面執行。</span><span class="sxs-lookup"><span data-stu-id="f3035-111">This tool can be run via hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="f3035-112">有兩種 tooaccess hello 裝置的本機介面：</span><span class="sxs-lookup"><span data-stu-id="f3035-112">There are two ways tooaccess hello local interface of your device:</span></span>

* <span data-ttu-id="f3035-113">[使用 PuTTY tooconnect toohello 裝置序列主控台](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="f3035-113">[Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="f3035-114">[從遠端存取 hello 工具透過 hello Windows PowerShell for StorSimple](storsimple-remote-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="f3035-114">[Remotely access hello tool via hello Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="f3035-115">在本文中，我們假設您已經連接透過 putty 連線 toohello 裝置序列主控台。</span><span class="sxs-lookup"><span data-stu-id="f3035-115">In this article, we assume that you have connected toohello device serial console via PuTTY.</span></span>

#### <a name="toorun-hello-diagnostics-tool"></a><span data-ttu-id="f3035-116">toorun hello 診斷工具</span><span class="sxs-lookup"><span data-stu-id="f3035-116">toorun hello diagnostics tool</span></span>

<span data-ttu-id="f3035-117">一旦您已經連接的裝置 hello toohello Windows PowerShell 介面，執行下列步驟 toorun hello cmdlet hello。</span><span class="sxs-lookup"><span data-stu-id="f3035-117">Once you have connected toohello Windows PowerShell interface of hello device, perform hello following steps toorun hello cmdlet.</span></span>
1. <span data-ttu-id="f3035-118">登入 toohello 裝置序列主控台中的 hello 步驟[使用 PuTTY tooconnect toohello 裝置序列主控台](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="f3035-118">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="f3035-119">輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="f3035-119">Type hello following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="f3035-120">如果未指定 hello 範圍參數，hello 指令程式會執行所有的 hello 診斷測試。</span><span class="sxs-lookup"><span data-stu-id="f3035-120">If hello scope parameter is not specified, hello cmdlet executes all hello diagnostic tests.</span></span> <span data-ttu-id="f3035-121">這些測試包括系統、硬體元件健全狀況、網路和效能。</span><span class="sxs-lookup"><span data-stu-id="f3035-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="f3035-122">toorun 只為特定的測試，請指定 hello 範圍參數。</span><span class="sxs-lookup"><span data-stu-id="f3035-122">toorun only a specific test, specify hello scope parameter.</span></span> <span data-ttu-id="f3035-123">比方說，toorun 只有 hello 網路測試類型</span><span class="sxs-lookup"><span data-stu-id="f3035-123">For instance, toorun only hello network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="f3035-124">選取並複製從 hello PuTTY hello 輸出至文字檔案，供進一步分析 視窗。</span><span class="sxs-lookup"><span data-stu-id="f3035-124">Select and copy hello output from hello PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-toouse-hello-diagnostics-tool"></a><span data-ttu-id="f3035-125">案例 toouse hello 診斷工具</span><span class="sxs-lookup"><span data-stu-id="f3035-125">Scenarios toouse hello diagnostics tool</span></span>

<span data-ttu-id="f3035-126">使用 hello 診斷工具 tootroubleshoot hello 網路、 效能、 系統與硬體系統的健康情況 hello。</span><span class="sxs-lookup"><span data-stu-id="f3035-126">Use hello diagnostics tool tootroubleshoot hello network, performance, system, and hardware health of hello system.</span></span> <span data-ttu-id="f3035-127">以下是可能的情況：</span><span class="sxs-lookup"><span data-stu-id="f3035-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="f3035-128">**裝置離線** - StorSimple 8000 系列裝置已離線。</span><span class="sxs-lookup"><span data-stu-id="f3035-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="f3035-129">不過，從 hello Windows PowerShell 介面，看來，這兩個 hello 控制站正在執行。</span><span class="sxs-lookup"><span data-stu-id="f3035-129">However, from hello Windows PowerShell interface, it seems that both hello controllers are up and running.</span></span>
    * <span data-ttu-id="f3035-130">您可以使用此工具 toothen 判斷 hello 網路狀態。</span><span class="sxs-lookup"><span data-stu-id="f3035-130">You can use this tool toothen determine hello network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="f3035-131">請勿 hello 註冊 （或透過安裝精靈進行設定） 之前，先在裝置上使用此工具 tooassess 效能和網路設定。</span><span class="sxs-lookup"><span data-stu-id="f3035-131">Do not use this tool tooassess performance and network settings on a device before hello registration (or configuring via setup wizard).</span></span> <span data-ttu-id="f3035-132">有效的 IP 在安裝精靈並註冊期間指派 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="f3035-132">A valid IP is assigned toohello device during setup wizard and registration.</span></span> <span data-ttu-id="f3035-133">在未註冊的裝置上，您可以執行此 Cmdlet 診斷硬體健全狀況和系統。</span><span class="sxs-lookup"><span data-stu-id="f3035-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="f3035-134">使用 hello 範圍參數，例如：</span><span class="sxs-lookup"><span data-stu-id="f3035-134">Use hello scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="f3035-135">**持續性的裝置問題**-您遇到看上去 toopersist 裝置問題。</span><span class="sxs-lookup"><span data-stu-id="f3035-135">**Persistent device issues** - You are experiencing device issues that seem toopersist.</span></span> <span data-ttu-id="f3035-136">比方說，註冊失敗。</span><span class="sxs-lookup"><span data-stu-id="f3035-136">For instance, registration is failing.</span></span> <span data-ttu-id="f3035-137">您可能也會發生問題的裝置 hello 裝置已成功註冊而且可運作一段時間之後。</span><span class="sxs-lookup"><span data-stu-id="f3035-137">You could also be experiencing device issues after hello device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="f3035-138">在此情況下，請使用此工具進行初步疑難排解，再向 Microsoft 支援服務登記服務要求。</span><span class="sxs-lookup"><span data-stu-id="f3035-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="f3035-139">我們建議您執行這項工具的工具，並擷取 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="f3035-139">We recommend that you run this tool and capture hello output of this tool.</span></span> <span data-ttu-id="f3035-140">然後，您可以提供此輸出 tooSupport tooexpedite 疑難排解。</span><span class="sxs-lookup"><span data-stu-id="f3035-140">You can then provide this output tooSupport tooexpedite troubleshooting.</span></span>
    * <span data-ttu-id="f3035-141">如果發生任何硬體元件或叢集失敗，您應該登記支援要求。</span><span class="sxs-lookup"><span data-stu-id="f3035-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="f3035-142">**裝置效能低落** - StorSimple 裝置變慢。</span><span class="sxs-lookup"><span data-stu-id="f3035-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="f3035-143">在此情況下，與範圍參數集 tooperformance 執行這個指令程式。</span><span class="sxs-lookup"><span data-stu-id="f3035-143">In this case, run this cmdlet with scope parameter set tooperformance.</span></span> <span data-ttu-id="f3035-144">分析 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="f3035-144">Analyze hello output.</span></span> <span data-ttu-id="f3035-145">收到 hello 雲端讀取寫入延遲。</span><span class="sxs-lookup"><span data-stu-id="f3035-145">You get hello cloud read-write latencies.</span></span> <span data-ttu-id="f3035-146">使用 hello 報告延遲為最大可達成的目標，在內部資料處理 hello、 一些額外負荷的因素，然後再部署 hello hello 系統上的工作負載。</span><span class="sxs-lookup"><span data-stu-id="f3035-146">Use hello reported latencies as maximum achievable target, factor in some overhead for hello internal data processing, and then deploy hello workloads on hello system.</span></span> <span data-ttu-id="f3035-147">如需詳細資訊，請移至太[使用 hello 網路測試 tootroubleshoot 裝置效能](#network-test)。</span><span class="sxs-lookup"><span data-stu-id="f3035-147">For more information, go too[Use hello network test tootroubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="f3035-148">診斷測試和輸出範例</span><span class="sxs-lookup"><span data-stu-id="f3035-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="f3035-149">硬體測試</span><span class="sxs-lookup"><span data-stu-id="f3035-149">Hardware test</span></span>

<span data-ttu-id="f3035-150">這項測試會判斷 hello 狀態 hello 硬體元件、 hello USM 韌體，以及在您的系統上執行的 hello 磁碟韌體。</span><span class="sxs-lookup"><span data-stu-id="f3035-150">This test determines hello status of hello hardware components, hello USM firmware, and hello disk firmware running on your system.</span></span>

* <span data-ttu-id="f3035-151">hello 硬體元件報告這些元件失敗的 hello 測試或不存在於 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="f3035-151">hello hardware components reported are those components that failed hello test or are not present in hello system.</span></span>
* <span data-ttu-id="f3035-152">hello USM 韌體和磁碟的韌體版本 hello 控制器 0，控制器 1 會報告與您的系統中的共用元件。</span><span class="sxs-lookup"><span data-stu-id="f3035-152">hello USM firmware and disk firmware versions are reported for hello Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="f3035-153">如需硬體元件的完整清單，請移至︰</span><span class="sxs-lookup"><span data-stu-id="f3035-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="f3035-154">主要機箱中的元件</span><span class="sxs-lookup"><span data-stu-id="f3035-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="f3035-155">EBOD 機箱中的元件</span><span class="sxs-lookup"><span data-stu-id="f3035-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="f3035-156">如果 hello 硬體測試報告失敗的元件，[登入 Microsoft 支援服務的服務要求](storsimple-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="f3035-156">If hello hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="f3035-157">在 8100 裝置上執行硬體測試的輸出範例</span><span class="sxs-lookup"><span data-stu-id="f3035-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="f3035-158">以下是 StorSimple 8100 裝置的輸出範例。</span><span class="sxs-lookup"><span data-stu-id="f3035-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="f3035-159">在 hello 8100 機型的裝置，hello EBOD 機箱不存在。</span><span class="sxs-lookup"><span data-stu-id="f3035-159">In hello 8100 model device, hello EBOD enclosure is not present.</span></span> <span data-ttu-id="f3035-160">因此，不會報告 hello EBOD 控制器元件。</span><span class="sxs-lookup"><span data-stu-id="f3035-160">Hence, hello EBOD controller components are not reported.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a><span data-ttu-id="f3035-161">系統測試</span><span class="sxs-lookup"><span data-stu-id="f3035-161">System test</span></span>

<span data-ttu-id="f3035-162">這項測試會報告 hello 系統資訊、 hello 可用的更新、 hello 叢集資訊，以及您的裝置 hello 服務資訊。</span><span class="sxs-lookup"><span data-stu-id="f3035-162">This test reports hello system information, hello updates available, hello cluster information, and hello service information for your device.</span></span>

* <span data-ttu-id="f3035-163">hello 系統資訊包括 hello 模型、 裝置序號、 時區、 控制站狀態，以及 hello 系統上執行的 hello 詳細的軟體版本。</span><span class="sxs-lookup"><span data-stu-id="f3035-163">hello system information includes hello model, device serial number, time zone, controller status, and hello detailed software version running on hello system.</span></span> <span data-ttu-id="f3035-164">各種系統參數回報為 hello 輸出太移 toounderstand hello[解譯系統資訊](#appendix-interpreting-system-information)。</span><span class="sxs-lookup"><span data-stu-id="f3035-164">toounderstand hello various system parameters reported as hello output, go too[Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="f3035-165">hello 更新可用性將會報告是否有可用的 hello 一般和維護模式及其相關聯的套件名稱。</span><span class="sxs-lookup"><span data-stu-id="f3035-165">hello update availability reports whether hello regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="f3035-166">如果`RegularUpdates`和`MaintenanceModeUpdates`是`false`，這表示無法使用 hello 更新時。</span><span class="sxs-lookup"><span data-stu-id="f3035-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that hello updates are not available.</span></span> <span data-ttu-id="f3035-167">您的裝置已是最新狀態。</span><span class="sxs-lookup"><span data-stu-id="f3035-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="f3035-168">hello 叢集資訊包含 hello 有關各種邏輯元件的所有 hello HCS 叢集群組和其各自的狀態。</span><span class="sxs-lookup"><span data-stu-id="f3035-168">hello cluster information contains hello information on various logical components of all hello HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="f3035-169">如果您看到 hello 報表，本節中的離線叢集群組[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="f3035-169">If you see an offline cluster group in this section of hello report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="f3035-170">hello 服務資訊包括 hello 名稱和所有 hello HCS 的狀態，並且在您的裝置上執行的 Ci 服務。</span><span class="sxs-lookup"><span data-stu-id="f3035-170">hello service information includes hello names and statuses of all hello HCS and CiS services running on your device.</span></span> <span data-ttu-id="f3035-171">這項資訊是很有幫助 hello Microsoft 支援服務疑難排解 hello 裝置問題。</span><span class="sxs-lookup"><span data-stu-id="f3035-171">This information is helpful for hello Microsoft Support in troubleshooting hello device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="f3035-172">在 8100 裝置上執行系統測試的輸出範例</span><span class="sxs-lookup"><span data-stu-id="f3035-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="f3035-173">以下是範例的輸出 hello 8100 裝置上執行的系統測試。</span><span class="sxs-lookup"><span data-stu-id="f3035-173">Here is a sample output of hello system test run on an 8100 device.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a><span data-ttu-id="f3035-174">網路測試</span><span class="sxs-lookup"><span data-stu-id="f3035-174">Network test</span></span>

<span data-ttu-id="f3035-175">這項測試會驗證 hello hello 網路介面、 連接埠、 DNS 和 NTP 伺服器連線、 SSL 憑證、 儲存體帳戶認證、 連線 toohello 更新伺服器，及您的 StorSimple 裝置上的 web proxy 連線的狀態。</span><span class="sxs-lookup"><span data-stu-id="f3035-175">This test validates hello status of hello network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity toohello Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="f3035-176">僅啟用 DATA0 時的網路測試輸出範例</span><span class="sxs-lookup"><span data-stu-id="f3035-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="f3035-177">以下是 hello 8100 裝置之範例的輸出。</span><span class="sxs-lookup"><span data-stu-id="f3035-177">Here is a sample output of hello 8100 device.</span></span> <span data-ttu-id="f3035-178">您可以在 hello 輸出中看到的：</span><span class="sxs-lookup"><span data-stu-id="f3035-178">You can see in hello output that:</span></span>
* <span data-ttu-id="f3035-179">只有啟用和設定 DATA 0 和 DATA 1 網路介面。</span><span class="sxs-lookup"><span data-stu-id="f3035-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="f3035-180">2-5 的資料不會啟用 hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="f3035-180">DATA 2 - 5 are not enabled in hello portal.</span></span>
* <span data-ttu-id="f3035-181">hello DNS 伺服器組態無效，而且 hello 裝置可以透過 hello DNS 伺服器連線。</span><span class="sxs-lookup"><span data-stu-id="f3035-181">hello DNS server configuration is valid and hello device can connect via hello DNS server.</span></span>
* <span data-ttu-id="f3035-182">hello NTP 伺服器連線也是正常的。</span><span class="sxs-lookup"><span data-stu-id="f3035-182">hello NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="f3035-183">連接埠 80 和 443 已開啟。</span><span class="sxs-lookup"><span data-stu-id="f3035-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="f3035-184">但已封鎖連接埠 9354。</span><span class="sxs-lookup"><span data-stu-id="f3035-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="f3035-185">根據 hello[系統的網路需求](storsimple-system-requirements.md)，您針對 hello 服務匯流排通訊需要 tooopen 此連接埠。</span><span class="sxs-lookup"><span data-stu-id="f3035-185">Based on hello [system network requirements](storsimple-system-requirements.md), you need tooopen this port for hello service bus communication.</span></span>
* <span data-ttu-id="f3035-186">hello SSL 憑證無效。</span><span class="sxs-lookup"><span data-stu-id="f3035-186">hello SSL certification is valid.</span></span>
* <span data-ttu-id="f3035-187">hello 裝置可以連線 toohello 儲存體帳戶： _myss8000storageacct_。</span><span class="sxs-lookup"><span data-stu-id="f3035-187">hello device can connect toohello storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="f3035-188">hello 連線 tooUpdate 伺服器無效。</span><span class="sxs-lookup"><span data-stu-id="f3035-188">hello connectivity tooUpdate servers is valid.</span></span>
* <span data-ttu-id="f3035-189">hello web proxy 未設定此裝置上。</span><span class="sxs-lookup"><span data-stu-id="f3035-189">hello web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="f3035-190">啟用 DATA0 和 DATA1 時的網路測試輸出範例</span><span class="sxs-lookup"><span data-stu-id="f3035-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a><span data-ttu-id="f3035-191">效能測試</span><span class="sxs-lookup"><span data-stu-id="f3035-191">Performance test</span></span>

<span data-ttu-id="f3035-192">這項測試會報告透過 hello 雲端讀寫延遲為您的裝置 hello 雲端效能。</span><span class="sxs-lookup"><span data-stu-id="f3035-192">This test reports hello cloud performance via hello cloud read-write latencies for your device.</span></span> <span data-ttu-id="f3035-193">此工具可以使用的 tooestablish 的可讓您與 StorSimple 的 hello 雲端效能基準線。</span><span class="sxs-lookup"><span data-stu-id="f3035-193">This tool can be used tooestablish a baseline of hello cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="f3035-194">hello 工具報告 hello 最大的效能 （如 讀寫延遲的最佳情況下），您可以取得您的連線。</span><span class="sxs-lookup"><span data-stu-id="f3035-194">hello tool reports hello maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="f3035-195">當 hello 工具報告 hello 最大可達成的效能，我們可以使用部署時的目標 hello 工作負載時 hello 報告的讀寫延遲。</span><span class="sxs-lookup"><span data-stu-id="f3035-195">As hello tool reports hello maximum achievable performance, we can use hello reported read-write latencies as targets when deploying hello workloads.</span></span>

<span data-ttu-id="f3035-196">hello 測試會模擬 hello 與 hello hello 裝置上的不同的磁碟區類型相關聯的 blob 大小。</span><span class="sxs-lookup"><span data-stu-id="f3035-196">hello test simulates hello blob sizes associated with hello different volume types on hello device.</span></span> <span data-ttu-id="f3035-197">固定在本機之磁碟區的一般分層和備份使用 64 KB blob 大小。</span><span class="sxs-lookup"><span data-stu-id="f3035-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="f3035-198">勾選封存選項的分層磁碟區使用 512 KB blob 資料大小。</span><span class="sxs-lookup"><span data-stu-id="f3035-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="f3035-199">如果您的裝置有階層式和本機固定磁碟區設定，只有 hello 測試對應 too64 KB 的 blob 執行資料大小。</span><span class="sxs-lookup"><span data-stu-id="f3035-199">If your device has tiered and locally pinned volumes configured, only hello test corresponding too64 KB blob data size is run.</span></span>

<span data-ttu-id="f3035-200">此工具 toouse，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="f3035-200">toouse this tool, perform hello following steps:</span></span>

1.  <span data-ttu-id="f3035-201">首先，混合建立分層磁碟區和勾選封存選項的分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f3035-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="f3035-202">此動作可確保該 hello 工具會執行 hello 測試 64 KB 到 512 KB 的 blob 大小。</span><span class="sxs-lookup"><span data-stu-id="f3035-202">This action ensures that hello tool runs hello tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="f3035-203">您已建立並設定 hello 磁碟區之後，請執行 hello 指令程式。</span><span class="sxs-lookup"><span data-stu-id="f3035-203">Run hello cmdlet after you have created and configured hello volumes.</span></span> <span data-ttu-id="f3035-204">輸入：</span><span class="sxs-lookup"><span data-stu-id="f3035-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="f3035-205">記下 hello 工具回報的 hello 讀取寫入延遲。</span><span class="sxs-lookup"><span data-stu-id="f3035-205">Make a note of hello read-write latencies reported by hello tool.</span></span> <span data-ttu-id="f3035-206">這項測試可能需要幾分鐘的時間 toorun 回報 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="f3035-206">This test can take several minutes toorun before it reports hello results.</span></span>

4. <span data-ttu-id="f3035-207">如果 hello 連線延遲時間全部 hello 預期的範圍，則 hello hello 工具回報的延遲可用來當做最大可達成的目標部署的 hello 工作負載時。</span><span class="sxs-lookup"><span data-stu-id="f3035-207">If hello connection latencies are all under hello expected range, then hello latencies reported by hello tool can be used as maximum achievable target when deploying hello workloads.</span></span> <span data-ttu-id="f3035-208">考量內部資料處理時的一些額外負荷。</span><span class="sxs-lookup"><span data-stu-id="f3035-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="f3035-209">如果報告 hello 讀寫延遲 hello 診斷工具是高：</span><span class="sxs-lookup"><span data-stu-id="f3035-209">If hello read-write latencies reported by hello diagnostics tool are high:</span></span>

    1. <span data-ttu-id="f3035-210">設定 blob 服務儲存體分析，並分析 hello 輸出 toounderstand hello 延遲 hello Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3035-210">Configure Storage Analytics for blob services and analyze hello output toounderstand hello latencies for hello Azure storage account.</span></span> <span data-ttu-id="f3035-211">如需詳細指示，請移太[啟用及設定儲存體分析](../storage/common/storage-enable-and-view-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="f3035-211">For detailed instructions, go too[enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="f3035-212">如果這些延遲也是您收到 hello StorSimple 診斷工具的 高 和 比較 toohello 數字，則您需要 toolog 搭配 Azure 儲存體服務要求。</span><span class="sxs-lookup"><span data-stu-id="f3035-212">If those latencies are also high and comparable toohello numbers you received from hello StorSimple Diagnostics tool, then you need toolog a service request with Azure storage.</span></span>

    2. <span data-ttu-id="f3035-213">如果 hello 儲存體帳戶延遲低，請連絡您的網路中的任何延遲問題您網路系統管理員 tooinvestigate。</span><span class="sxs-lookup"><span data-stu-id="f3035-213">If hello storage account latencies are low, contact your network administrator tooinvestigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="f3035-214">在 8100 裝置上執行效能測試的輸出範例</span><span class="sxs-lookup"><span data-stu-id="f3035-214">Sample output of performance test run on an 8100 device</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="f3035-215">附錄︰解譯系統資訊</span><span class="sxs-lookup"><span data-stu-id="f3035-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="f3035-216">以下是描述哪些 hello hello 系統資訊的各種 Windows PowerShell 參數對應至資料表。</span><span class="sxs-lookup"><span data-stu-id="f3035-216">Here is a table describing what hello various Windows PowerShell parameters in hello system information map to.</span></span> 

| <span data-ttu-id="f3035-217">PowerShell 參數</span><span class="sxs-lookup"><span data-stu-id="f3035-217">PowerShell Parameter</span></span>    | <span data-ttu-id="f3035-218">說明</span><span class="sxs-lookup"><span data-stu-id="f3035-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="f3035-219">執行個體識別碼</span><span class="sxs-lookup"><span data-stu-id="f3035-219">Instance ID</span></span>             | <span data-ttu-id="f3035-220">每個控制器都有相關聯的唯一識別碼或 GUID。</span><span class="sxs-lookup"><span data-stu-id="f3035-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="f3035-221">名稱</span><span class="sxs-lookup"><span data-stu-id="f3035-221">Name</span></span>                    | <span data-ttu-id="f3035-222">hello 的 hello 裝置 hello Azure 入口網站的裝置部署期間設定的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="f3035-222">hello friendly name of hello device as configured through hello Azure portal during device deployment.</span></span> <span data-ttu-id="f3035-223">hello 預設易記名稱為 hello 裝置序號。</span><span class="sxs-lookup"><span data-stu-id="f3035-223">hello default friendly name is hello device serial number.</span></span> |
| <span data-ttu-id="f3035-224">模型</span><span class="sxs-lookup"><span data-stu-id="f3035-224">Model</span></span>                   | <span data-ttu-id="f3035-225">您的 StorSimple 8000 系列裝置 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="f3035-225">hello model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="f3035-226">hello 模型可以是 8100 或 8600。</span><span class="sxs-lookup"><span data-stu-id="f3035-226">hello model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="f3035-227">SerialNumber</span><span class="sxs-lookup"><span data-stu-id="f3035-227">SerialNumber</span></span>            | <span data-ttu-id="f3035-228">指派在 hello 工廠 hello 裝置序號，並為 15 個字元。</span><span class="sxs-lookup"><span data-stu-id="f3035-228">hello device serial number is assigned at hello factory and is 15 characters long.</span></span> <span data-ttu-id="f3035-229">例如，8600-SHX0991003G44HT 表示：</span><span class="sxs-lookup"><span data-stu-id="f3035-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="f3035-230">8600 – 是 hello 裝置模型。</span><span class="sxs-lookup"><span data-stu-id="f3035-230">8600 – Is hello device model.</span></span><br><span data-ttu-id="f3035-231">SHX – hello 製造站台。</span><span class="sxs-lookup"><span data-stu-id="f3035-231">SHX – Is hello manufacturing site.</span></span><br> <span data-ttu-id="f3035-232">0991003 – 特定產品。</span><span class="sxs-lookup"><span data-stu-id="f3035-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="f3035-233">G44HT hello 最後 5 位數會遞增 toocreate 唯一序號。</span><span class="sxs-lookup"><span data-stu-id="f3035-233">G44HT- hello last 5 digits are incremented toocreate unique serial numbers.</span></span> <span data-ttu-id="f3035-234">這可能不是連續的組合。</span><span class="sxs-lookup"><span data-stu-id="f3035-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="f3035-235">TimeZone</span><span class="sxs-lookup"><span data-stu-id="f3035-235">TimeZone</span></span>                | <span data-ttu-id="f3035-236">hello 裝置時區中的設定 hello Azure 入口網站裝置部署期間。</span><span class="sxs-lookup"><span data-stu-id="f3035-236">hello device time zone as configured in hello Azure portal during device deployment.</span></span>|
| <span data-ttu-id="f3035-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="f3035-237">CurrentController</span></span>       | <span data-ttu-id="f3035-238">您所連接的 toothrough hello Windows PowerShell 介面，您的 StorSimple 裝置 hello 控制器。</span><span class="sxs-lookup"><span data-stu-id="f3035-238">hello controller that you are connected toothrough hello Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="f3035-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="f3035-239">ActiveController</span></span>        | <span data-ttu-id="f3035-240">hello 控制器為作用中裝置上，且它會控制所有 hello 網路和磁碟作業。</span><span class="sxs-lookup"><span data-stu-id="f3035-240">hello controller that is active on your device and is controlling all hello network and disk operations.</span></span> <span data-ttu-id="f3035-241">這可以是控制器 0 或控制器 1。</span><span class="sxs-lookup"><span data-stu-id="f3035-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="f3035-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="f3035-242">Controller0Status</span></span>       | <span data-ttu-id="f3035-243">在您的裝置上的控制器 0 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="f3035-243">hello status of Controller 0 on your device.</span></span> <span data-ttu-id="f3035-244">hello 控制器狀態可以是一般處於修復模式，或無法連線。</span><span class="sxs-lookup"><span data-stu-id="f3035-244">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="f3035-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="f3035-245">Controller1Status</span></span>       | <span data-ttu-id="f3035-246">您的裝置上的 hello 控制器 1 的狀態。</span><span class="sxs-lookup"><span data-stu-id="f3035-246">hello status of Controller 1 on your device.</span></span>  <span data-ttu-id="f3035-247">hello 控制器狀態可以是一般處於修復模式，或無法連線。</span><span class="sxs-lookup"><span data-stu-id="f3035-247">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="f3035-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="f3035-248">SystemMode</span></span>              | <span data-ttu-id="f3035-249">hello StorSimple 裝置的整體狀態。</span><span class="sxs-lookup"><span data-stu-id="f3035-249">hello overall status of your StorSimple device.</span></span> <span data-ttu-id="f3035-250">hello 裝置狀態可以是正常現象，維護，或已解除任務 （對應 toodeactivated hello Azure 入口網站中的）。</span><span class="sxs-lookup"><span data-stu-id="f3035-250">hello device status can be normal, maintenance, or decommissioned (corresponds toodeactivated in hello Azure portal).</span></span>|
| <span data-ttu-id="f3035-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="f3035-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="f3035-252">hello 易記字串對應 toohello 裝置軟體版本。</span><span class="sxs-lookup"><span data-stu-id="f3035-252">hello friendly string that corresponds toohello device software version.</span></span> <span data-ttu-id="f3035-253">執行 Update 4 的系統，hello 易記的軟體版本將會是 StorSimple 8000 系列 Update 4.0。</span><span class="sxs-lookup"><span data-stu-id="f3035-253">For a system running Update 4, hello friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="f3035-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="f3035-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="f3035-255">在您的裝置上執行 hello HCS 軟體版本。</span><span class="sxs-lookup"><span data-stu-id="f3035-255">hello HCS software version running on your device.</span></span> <span data-ttu-id="f3035-256">比方說，hello HCS 軟體版本對應 tooStorSimple 8000 系列 Update 4.0 是 6.3.9600.17820。</span><span class="sxs-lookup"><span data-stu-id="f3035-256">For instance, hello HCS software version corresponding tooStorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="f3035-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="f3035-257">ApiVersion</span></span>              | <span data-ttu-id="f3035-258">hello hello HCS 裝置的 Windows PowerShell API hello 軟體版本。</span><span class="sxs-lookup"><span data-stu-id="f3035-258">hello software version of hello Windows PowerShell API of hello HCS device.</span></span>|
| <span data-ttu-id="f3035-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="f3035-259">VhdVersion</span></span>              | <span data-ttu-id="f3035-260">hello 的 hello 裝置 hello 原廠映像的軟體版本所隨附。</span><span class="sxs-lookup"><span data-stu-id="f3035-260">hello software version of hello factory image that hello device was shipped with.</span></span> <span data-ttu-id="f3035-261">如果您重設您的裝置 toofactory 預設值，然後它會執行此軟體版本。</span><span class="sxs-lookup"><span data-stu-id="f3035-261">If you reset your device toofactory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="f3035-262">OSVersion</span><span class="sxs-lookup"><span data-stu-id="f3035-262">OSVersion</span></span>               | <span data-ttu-id="f3035-263">hello hello Windows 伺服器作業系統 hello 裝置上執行的軟體版本。</span><span class="sxs-lookup"><span data-stu-id="f3035-263">hello software version of hello Windows Server operating system running on hello device.</span></span> <span data-ttu-id="f3035-264">hello StorSimple 裝置根據 hello 對應 too6.3.9600 的 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="f3035-264">hello StorSimple device is based off hello Windows Server 2012 R2 that corresponds too6.3.9600.</span></span>|
| <span data-ttu-id="f3035-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="f3035-265">CisAgentVersion</span></span>         | <span data-ttu-id="f3035-266">hello StorSimple 裝置上執行的 Ci 代理程式的版本。</span><span class="sxs-lookup"><span data-stu-id="f3035-266">hello version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="f3035-267">此代理程式可協助您與 Azure 中執行的 hello StorSimple Manager 服務通訊。</span><span class="sxs-lookup"><span data-stu-id="f3035-267">This agent helps communicate with hello StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="f3035-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="f3035-268">MdsAgentVersion</span></span>         | <span data-ttu-id="f3035-269">hello 版本對應 toohello Mds 的代理程式在您的 StorSimple 裝置上執行。</span><span class="sxs-lookup"><span data-stu-id="f3035-269">hello version corresponding toohello Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="f3035-270">此代理程式將資料 toohello 監視和診斷服務 (MDS)。</span><span class="sxs-lookup"><span data-stu-id="f3035-270">This agent moves data toohello Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="f3035-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="f3035-271">Lsisas2Version</span></span>          | <span data-ttu-id="f3035-272">hello 版本對應 toohello LSI 的驅動程式在您的 StorSimple 裝置上。</span><span class="sxs-lookup"><span data-stu-id="f3035-272">hello version corresponding toohello LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="f3035-273">容量</span><span class="sxs-lookup"><span data-stu-id="f3035-273">Capacity</span></span>                | <span data-ttu-id="f3035-274">以位元組為單位的 hello 裝置 hello 總容量。</span><span class="sxs-lookup"><span data-stu-id="f3035-274">hello total capacity of hello device in bytes.</span></span>|
| <span data-ttu-id="f3035-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="f3035-275">RemoteManagementMode</span></span>    | <span data-ttu-id="f3035-276">指出是否可以透過其 Windows PowerShell 介面從遠端管理的裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="f3035-276">Indicates whether hello device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="f3035-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="f3035-277">FipsMode</span></span>                | <span data-ttu-id="f3035-278">指出是否要在裝置上啟用 hello 美國聯邦資訊處理標準 (FIPS) 模式。</span><span class="sxs-lookup"><span data-stu-id="f3035-278">Indicates whether hello United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="f3035-279">hello FIPS 140 標準會定義核准 hello 保護機密資料的美國聯邦政府電腦系統所使用的密碼編譯演算法。</span><span class="sxs-lookup"><span data-stu-id="f3035-279">hello FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for hello protection of sensitive data.</span></span> <span data-ttu-id="f3035-280">如果是執行 Update 4 或更新版本的裝置，預設會啟用 FIPS 模式。</span><span class="sxs-lookup"><span data-stu-id="f3035-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f3035-281">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f3035-281">Next steps</span></span>

* <span data-ttu-id="f3035-282">了解 hello [hello Invoke HcsDiagnostics cmdlet 的語法](https://technet.microsoft.com/library/mt795371.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f3035-282">Learn hello [syntax of hello Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="f3035-283">深入了解如何太[部署問題進行疑難排解](storsimple-troubleshoot-deployment.md)StorSimple 裝置上。</span><span class="sxs-lookup"><span data-stu-id="f3035-283">Learn more about how too[troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>
