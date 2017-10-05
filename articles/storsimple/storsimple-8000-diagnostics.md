---
title: "針對 StorSimple 8000 裝置進行疑難排解的診斷工具 | Microsoft Docs"
description: "描述 StorSimple 裝置模式並說明如何使用 Windows PowerShell for StorSimple 來變更裝置的模式。"
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
ms.openlocfilehash: 8fae7bb357f8e5e8eff249edfe3a2aaafe04283c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-storsimple-diagnostics-tool-to-troubleshoot-8000-series-device-issues"></a><span data-ttu-id="b5c83-103">使用 StorSimple 診斷工具針對 8000 系列裝置問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="b5c83-103">Use the StorSimple Diagnostics Tool to troubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="b5c83-104">概觀</span><span class="sxs-lookup"><span data-stu-id="b5c83-104">Overview</span></span>

<span data-ttu-id="b5c83-105">StorSimple 診斷工具可診斷 StorSimple 裝置的系統、效能、網路和硬體元件健全狀況的相關問題。</span><span class="sxs-lookup"><span data-stu-id="b5c83-105">The StorSimple Diagnostics tool diagnoses issues related to system, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="b5c83-106">診斷工具可用在各種情況。</span><span class="sxs-lookup"><span data-stu-id="b5c83-106">The diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="b5c83-107">這些情況包括工作負載規劃、部署 StorSimple 裝置、評估網路環境，以及判斷作業裝置的效能。</span><span class="sxs-lookup"><span data-stu-id="b5c83-107">These scenarios include workload planning, deploying a StorSimple device, assessing the network environment, and determining the performance of an operational device.</span></span> <span data-ttu-id="b5c83-108">本文提供診斷工具的概觀，並說明如何使用此工具來診斷 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="b5c83-108">This article provides an overview of the diagnostics tool and describes how the tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="b5c83-109">診斷工具主要用於 StorSimple 8000 系列內部部署裝置 (8100 和 8600)。</span><span class="sxs-lookup"><span data-stu-id="b5c83-109">The diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="b5c83-110">執行診斷工具</span><span class="sxs-lookup"><span data-stu-id="b5c83-110">Run diagnostics tool</span></span>

<span data-ttu-id="b5c83-111">您可以透過 StorSimple 裝置的 Windows PowerShell 介面執行此工具。</span><span class="sxs-lookup"><span data-stu-id="b5c83-111">This tool can be run via the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="b5c83-112">有兩種方式可存取裝置的本機介面︰</span><span class="sxs-lookup"><span data-stu-id="b5c83-112">There are two ways to access the local interface of your device:</span></span>

* <span data-ttu-id="b5c83-113">[使用 PuTTY 連線至裝置序列主控台](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)</span><span class="sxs-lookup"><span data-stu-id="b5c83-113">[Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="b5c83-114">[透過適用於 StorSimple 的 Windows PowerShell 從遠端存取工具](storsimple-remote-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="b5c83-114">[Remotely access the tool via the Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="b5c83-115">在本文中，我們假設您已透過 PuTTY 連線至裝置序列主控台。</span><span class="sxs-lookup"><span data-stu-id="b5c83-115">In this article, we assume that you have connected to the device serial console via PuTTY.</span></span>

#### <a name="to-run-the-diagnostics-tool"></a><span data-ttu-id="b5c83-116">執行診斷工具</span><span class="sxs-lookup"><span data-stu-id="b5c83-116">To run the diagnostics tool</span></span>

<span data-ttu-id="b5c83-117">連線至裝置的 Windows PowerShell 介面之後，執行下列步驟來執行 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b5c83-117">Once you have connected to the Windows PowerShell interface of the device, perform the following steps to run the cmdlet.</span></span>
1. <span data-ttu-id="b5c83-118">遵循 [使用 PuTTY 來連接到裝置序列主控台](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)中的步驟，登入裝置序列主控台。</span><span class="sxs-lookup"><span data-stu-id="b5c83-118">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="b5c83-119">輸入以下命令：</span><span class="sxs-lookup"><span data-stu-id="b5c83-119">Type the following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="b5c83-120">如果未指定 scope 參數，Cmdlet 會執行所有診斷測試。</span><span class="sxs-lookup"><span data-stu-id="b5c83-120">If the scope parameter is not specified, the cmdlet executes all the diagnostic tests.</span></span> <span data-ttu-id="b5c83-121">這些測試包括系統、硬體元件健全狀況、網路和效能。</span><span class="sxs-lookup"><span data-stu-id="b5c83-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="b5c83-122">若只要執行特定測試，請指定 scope 參數。</span><span class="sxs-lookup"><span data-stu-id="b5c83-122">To run only a specific test, specify the scope parameter.</span></span> <span data-ttu-id="b5c83-123">例如，若只要執行網路測試，請輸入</span><span class="sxs-lookup"><span data-stu-id="b5c83-123">For instance, to run only the network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="b5c83-124">選取 PuTTY 視窗中的輸出，並複製到文字檔以進一步分析。</span><span class="sxs-lookup"><span data-stu-id="b5c83-124">Select and copy the output from the PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-to-use-the-diagnostics-tool"></a><span data-ttu-id="b5c83-125">使用診斷工具的情況</span><span class="sxs-lookup"><span data-stu-id="b5c83-125">Scenarios to use the diagnostics tool</span></span>

<span data-ttu-id="b5c83-126">使用診斷工具針對網路、效能、系統和系統的硬體健全狀況進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="b5c83-126">Use the diagnostics tool to troubleshoot the network, performance, system, and hardware health of the system.</span></span> <span data-ttu-id="b5c83-127">以下是可能的情況：</span><span class="sxs-lookup"><span data-stu-id="b5c83-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="b5c83-128">**裝置離線** - StorSimple 8000 系列裝置已離線。</span><span class="sxs-lookup"><span data-stu-id="b5c83-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="b5c83-129">但從 Windows PowerShell 介面中查看，兩個控制器似乎都正常運作。</span><span class="sxs-lookup"><span data-stu-id="b5c83-129">However, from the Windows PowerShell interface, it seems that both the controllers are up and running.</span></span>
    * <span data-ttu-id="b5c83-130">您可以使用此工具判斷網路狀態。</span><span class="sxs-lookup"><span data-stu-id="b5c83-130">You can use this tool to then determine the network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="b5c83-131">在註冊 (或透過安裝精靈進行設定) 裝置之前，請勿使用此工具來評估裝置的效能和網路設定。</span><span class="sxs-lookup"><span data-stu-id="b5c83-131">Do not use this tool to assess performance and network settings on a device before the registration (or configuring via setup wizard).</span></span> <span data-ttu-id="b5c83-132">在安裝精靈和註冊期間會指派有效的 IP 給裝置。</span><span class="sxs-lookup"><span data-stu-id="b5c83-132">A valid IP is assigned to the device during setup wizard and registration.</span></span> <span data-ttu-id="b5c83-133">在未註冊的裝置上，您可以執行此 Cmdlet 診斷硬體健全狀況和系統。</span><span class="sxs-lookup"><span data-stu-id="b5c83-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="b5c83-134">使用 scope 參數，例如︰</span><span class="sxs-lookup"><span data-stu-id="b5c83-134">Use the scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="b5c83-135">**持續的裝置問題** - 發生的裝置問題似乎持續不斷。</span><span class="sxs-lookup"><span data-stu-id="b5c83-135">**Persistent device issues** - You are experiencing device issues that seem to persist.</span></span> <span data-ttu-id="b5c83-136">比方說，註冊失敗。</span><span class="sxs-lookup"><span data-stu-id="b5c83-136">For instance, registration is failing.</span></span> <span data-ttu-id="b5c83-137">在裝置成功註冊並運作一段時間之後，也可能會發生裝置問題。</span><span class="sxs-lookup"><span data-stu-id="b5c83-137">You could also be experiencing device issues after the device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="b5c83-138">在此情況下，請使用此工具進行初步疑難排解，再向 Microsoft 支援服務登記服務要求。</span><span class="sxs-lookup"><span data-stu-id="b5c83-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="b5c83-139">我們建議您執行這項工具，並擷取這項工具的輸出。</span><span class="sxs-lookup"><span data-stu-id="b5c83-139">We recommend that you run this tool and capture the output of this tool.</span></span> <span data-ttu-id="b5c83-140">然後，您可以提供此輸出給支援服務，以加速疑難排解。</span><span class="sxs-lookup"><span data-stu-id="b5c83-140">You can then provide this output to Support to expedite troubleshooting.</span></span>
    * <span data-ttu-id="b5c83-141">如果發生任何硬體元件或叢集失敗，您應該登記支援要求。</span><span class="sxs-lookup"><span data-stu-id="b5c83-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="b5c83-142">**裝置效能低落** - StorSimple 裝置變慢。</span><span class="sxs-lookup"><span data-stu-id="b5c83-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="b5c83-143">在此情況下，請執行此 Cmdlet，並將 scope 參數設為 performance。</span><span class="sxs-lookup"><span data-stu-id="b5c83-143">In this case, run this cmdlet with scope parameter set to performance.</span></span> <span data-ttu-id="b5c83-144">分析輸出。</span><span class="sxs-lookup"><span data-stu-id="b5c83-144">Analyze the output.</span></span> <span data-ttu-id="b5c83-145">您會知道雲端讀寫延遲。</span><span class="sxs-lookup"><span data-stu-id="b5c83-145">You get the cloud read-write latencies.</span></span> <span data-ttu-id="b5c83-146">請使用報告的延遲當做為可達成的最高目標，考量內部資料處理時的一些額外負荷，然後在系統上部署工作負載。</span><span class="sxs-lookup"><span data-stu-id="b5c83-146">Use the reported latencies as maximum achievable target, factor in some overhead for the internal data processing, and then deploy the workloads on the system.</span></span> <span data-ttu-id="b5c83-147">如需詳細資訊，請參閱[使用網路測試針對裝置效能進行疑難排解](#network-test)。</span><span class="sxs-lookup"><span data-stu-id="b5c83-147">For more information, go to [Use the network test to troubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="b5c83-148">診斷測試和輸出範例</span><span class="sxs-lookup"><span data-stu-id="b5c83-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="b5c83-149">硬體測試</span><span class="sxs-lookup"><span data-stu-id="b5c83-149">Hardware test</span></span>

<span data-ttu-id="b5c83-150">這項測試會判斷系統上執行的硬體元件、USM 韌體和磁碟韌體的狀態。</span><span class="sxs-lookup"><span data-stu-id="b5c83-150">This test determines the status of the hardware components, the USM firmware, and the disk firmware running on your system.</span></span>

* <span data-ttu-id="b5c83-151">報告的硬體元件是未通過測試或不存在系統中的元件。</span><span class="sxs-lookup"><span data-stu-id="b5c83-151">The hardware components reported are those components that failed the test or are not present in the system.</span></span>
* <span data-ttu-id="b5c83-152">報告的 USM 韌體和磁碟韌體版本是指系統中的控制器 0、控制器 1 和共用元件。</span><span class="sxs-lookup"><span data-stu-id="b5c83-152">The USM firmware and disk firmware versions are reported for the Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="b5c83-153">如需硬體元件的完整清單，請移至︰</span><span class="sxs-lookup"><span data-stu-id="b5c83-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="b5c83-154">主要機箱中的元件</span><span class="sxs-lookup"><span data-stu-id="b5c83-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="b5c83-155">EBOD 機箱中的元件</span><span class="sxs-lookup"><span data-stu-id="b5c83-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="b5c83-156">如果硬體測試報告失敗的元件，請[向 Microsoft 支援服務登記服務要求](storsimple-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="b5c83-156">If the hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="b5c83-157">在 8100 裝置上執行硬體測試的輸出範例</span><span class="sxs-lookup"><span data-stu-id="b5c83-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="b5c83-158">以下是 StorSimple 8100 裝置的輸出範例。</span><span class="sxs-lookup"><span data-stu-id="b5c83-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="b5c83-159">8100 機型裝置中沒有 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="b5c83-159">In the 8100 model device, the EBOD enclosure is not present.</span></span> <span data-ttu-id="b5c83-160">因此，不會報告 EBOD 控制器元件。</span><span class="sxs-lookup"><span data-stu-id="b5c83-160">Hence, the EBOD controller components are not reported.</span></span>

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

### <a name="system-test"></a><span data-ttu-id="b5c83-161">系統測試</span><span class="sxs-lookup"><span data-stu-id="b5c83-161">System test</span></span>

<span data-ttu-id="b5c83-162">這項測試會報告系統資訊、可用的更新、叢集資訊，以及裝置的服務資訊。</span><span class="sxs-lookup"><span data-stu-id="b5c83-162">This test reports the system information, the updates available, the cluster information, and the service information for your device.</span></span>

* <span data-ttu-id="b5c83-163">系統資訊包括機型、裝置序號、時區、控制器狀態，以及系統上執行的詳細軟體版本。</span><span class="sxs-lookup"><span data-stu-id="b5c83-163">The system information includes the model, device serial number, time zone, controller status, and the detailed software version running on the system.</span></span> <span data-ttu-id="b5c83-164">若要了解輸出所報告的各種系統參數，請參閱[解譯系統資訊](#appendix-interpreting-system-information)。</span><span class="sxs-lookup"><span data-stu-id="b5c83-164">To understand the various system parameters reported as the output, go to [Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="b5c83-165">更新可用性報告定期和維護模式是否可用及其相關聯的套件名稱。</span><span class="sxs-lookup"><span data-stu-id="b5c83-165">The update availability reports whether the regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="b5c83-166">如果 `RegularUpdates` 和 `MaintenanceModeUpdates` 是 `false`，這表示沒有可用的更新。</span><span class="sxs-lookup"><span data-stu-id="b5c83-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that the updates are not available.</span></span> <span data-ttu-id="b5c83-167">您的裝置已是最新狀態。</span><span class="sxs-lookup"><span data-stu-id="b5c83-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="b5c83-168">叢集資訊包含所有 HCS 叢集群組的各種邏輯元件及其個別狀態的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b5c83-168">The cluster information contains the information on various logical components of all the HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="b5c83-169">如果您在此報告區段看到離線叢集群組，請[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="b5c83-169">If you see an offline cluster group in this section of the report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="b5c83-170">服務資訊包含在您的裝置上執行的所有 HCS 和 CiS 服務的名稱和狀態。</span><span class="sxs-lookup"><span data-stu-id="b5c83-170">The service information includes the names and statuses of all the HCS and CiS services running on your device.</span></span> <span data-ttu-id="b5c83-171">這項資訊可協助 Microsoft 支援服務針對裝置問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="b5c83-171">This information is helpful for the Microsoft Support in troubleshooting the device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="b5c83-172">在 8100 裝置上執行系統測試的輸出範例</span><span class="sxs-lookup"><span data-stu-id="b5c83-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="b5c83-173">以下是在 8100 裝置上執行系統測試的輸出範例。</span><span class="sxs-lookup"><span data-stu-id="b5c83-173">Here is a sample output of the system test run on an 8100 device.</span></span>

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

### <a name="network-test"></a><span data-ttu-id="b5c83-174">網路測試</span><span class="sxs-lookup"><span data-stu-id="b5c83-174">Network test</span></span>

<span data-ttu-id="b5c83-175">這項測試會驗證網路介面、連接埠、DNS 和 NTP 伺服器連線的狀態、SSL 憑證、儲存體帳戶認證、更新伺服器的連線能力，以及 StorSimple 裝置上的 Web Proxy 連線能力。</span><span class="sxs-lookup"><span data-stu-id="b5c83-175">This test validates the status of the network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity to the Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="b5c83-176">僅啟用 DATA0 時的網路測試輸出範例</span><span class="sxs-lookup"><span data-stu-id="b5c83-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="b5c83-177">以下是 8100 裝置的輸出範例。</span><span class="sxs-lookup"><span data-stu-id="b5c83-177">Here is a sample output of the 8100 device.</span></span> <span data-ttu-id="b5c83-178">您可以在輸出中看到︰</span><span class="sxs-lookup"><span data-stu-id="b5c83-178">You can see in the output that:</span></span>
* <span data-ttu-id="b5c83-179">只有啟用和設定 DATA 0 和 DATA 1 網路介面。</span><span class="sxs-lookup"><span data-stu-id="b5c83-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="b5c83-180">入口網站中未啟用 DATA 2 - 5。</span><span class="sxs-lookup"><span data-stu-id="b5c83-180">DATA 2 - 5 are not enabled in the portal.</span></span>
* <span data-ttu-id="b5c83-181">DNS 伺服器組態無效，裝置可以透過 DNS 伺服器來連線。</span><span class="sxs-lookup"><span data-stu-id="b5c83-181">The DNS server configuration is valid and the device can connect via the DNS server.</span></span>
* <span data-ttu-id="b5c83-182">NTP 伺服器連線能力也正常。</span><span class="sxs-lookup"><span data-stu-id="b5c83-182">The NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="b5c83-183">連接埠 80 和 443 已開啟。</span><span class="sxs-lookup"><span data-stu-id="b5c83-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="b5c83-184">但已封鎖連接埠 9354。</span><span class="sxs-lookup"><span data-stu-id="b5c83-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="b5c83-185">根據[系統網路需求](storsimple-system-requirements.md)，您必須開啟此連接埠，服務匯流排通訊才能進行。</span><span class="sxs-lookup"><span data-stu-id="b5c83-185">Based on the [system network requirements](storsimple-system-requirements.md), you need to open this port for the service bus communication.</span></span>
* <span data-ttu-id="b5c83-186">SSL 憑證有效。</span><span class="sxs-lookup"><span data-stu-id="b5c83-186">The SSL certification is valid.</span></span>
* <span data-ttu-id="b5c83-187">裝置可以連線至儲存體帳戶︰_myss8000storageacct_。</span><span class="sxs-lookup"><span data-stu-id="b5c83-187">The device can connect to the storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="b5c83-188">更新伺服器的連線能力有效。</span><span class="sxs-lookup"><span data-stu-id="b5c83-188">The connectivity to Update servers is valid.</span></span>
* <span data-ttu-id="b5c83-189">此裝置上未設定 Web Proxy。</span><span class="sxs-lookup"><span data-stu-id="b5c83-189">The web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="b5c83-190">啟用 DATA0 和 DATA1 時的網路測試輸出範例</span><span class="sxs-lookup"><span data-stu-id="b5c83-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

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

### <a name="performance-test"></a><span data-ttu-id="b5c83-191">效能測試</span><span class="sxs-lookup"><span data-stu-id="b5c83-191">Performance test</span></span>

<span data-ttu-id="b5c83-192">這項測試會透過裝置的雲端讀寫延遲來報告雲端效能。</span><span class="sxs-lookup"><span data-stu-id="b5c83-192">This test reports the cloud performance via the cloud read-write latencies for your device.</span></span> <span data-ttu-id="b5c83-193">這項工具可以用來建立 StorSimple 可達到的雲端效能基準線。</span><span class="sxs-lookup"><span data-stu-id="b5c83-193">This tool can be used to establish a baseline of the cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="b5c83-194">此工具會報告連線可達成的最大效能 (讀寫延遲的最佳案例)。</span><span class="sxs-lookup"><span data-stu-id="b5c83-194">The tool reports the maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="b5c83-195">由於此工具會報告可達成的最大效能，我們可以在部署工作負載時，將所報告的讀寫延遲當做目標。</span><span class="sxs-lookup"><span data-stu-id="b5c83-195">As the tool reports the maximum achievable performance, we can use the reported read-write latencies as targets when deploying the workloads.</span></span>

<span data-ttu-id="b5c83-196">測試會模擬裝置上不同磁碟區類型相關聯的 blob 大小。</span><span class="sxs-lookup"><span data-stu-id="b5c83-196">The test simulates the blob sizes associated with the different volume types on the device.</span></span> <span data-ttu-id="b5c83-197">固定在本機之磁碟區的一般分層和備份使用 64 KB blob 大小。</span><span class="sxs-lookup"><span data-stu-id="b5c83-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="b5c83-198">勾選封存選項的分層磁碟區使用 512 KB blob 資料大小。</span><span class="sxs-lookup"><span data-stu-id="b5c83-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="b5c83-199">如果您的裝置已設定分層和固定在本機的磁碟區，則只會執行對應至 64 KB blob 資料大小的測試。</span><span class="sxs-lookup"><span data-stu-id="b5c83-199">If your device has tiered and locally pinned volumes configured, only the test corresponding to 64 KB blob data size is run.</span></span>

<span data-ttu-id="b5c83-200">若要使用此工具，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b5c83-200">To use this tool, perform the following steps:</span></span>

1.  <span data-ttu-id="b5c83-201">首先，混合建立分層磁碟區和勾選封存選項的分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b5c83-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="b5c83-202">此動作可確保工具會同時對 64 KB 和 512 KB blob 大小執行測試。</span><span class="sxs-lookup"><span data-stu-id="b5c83-202">This action ensures that the tool runs the tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="b5c83-203">建立並設定磁碟區之後，執行此 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b5c83-203">Run the cmdlet after you have created and configured the volumes.</span></span> <span data-ttu-id="b5c83-204">輸入：</span><span class="sxs-lookup"><span data-stu-id="b5c83-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="b5c83-205">記下工具所報告的讀寫延遲。</span><span class="sxs-lookup"><span data-stu-id="b5c83-205">Make a note of the read-write latencies reported by the tool.</span></span> <span data-ttu-id="b5c83-206">這項測試可能需要執行幾分鐘之後才會報告結果。</span><span class="sxs-lookup"><span data-stu-id="b5c83-206">This test can take several minutes to run before it reports the results.</span></span>

4. <span data-ttu-id="b5c83-207">如果連線延遲全部在預期的範圍內，則工具所報告的延遲，可當做部署工作負載時可達成的最高目標。</span><span class="sxs-lookup"><span data-stu-id="b5c83-207">If the connection latencies are all under the expected range, then the latencies reported by the tool can be used as maximum achievable target when deploying the workloads.</span></span> <span data-ttu-id="b5c83-208">考量內部資料處理時的一些額外負荷。</span><span class="sxs-lookup"><span data-stu-id="b5c83-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="b5c83-209">如果診斷工具所報告的讀寫延遲很高︰</span><span class="sxs-lookup"><span data-stu-id="b5c83-209">If the read-write latencies reported by the diagnostics tool are high:</span></span>

    1. <span data-ttu-id="b5c83-210">設定 blob 服務的儲存體分析，然後分析輸出，以了解 Azure 儲存體帳戶的延遲。</span><span class="sxs-lookup"><span data-stu-id="b5c83-210">Configure Storage Analytics for blob services and analyze the output to understand the latencies for the Azure storage account.</span></span> <span data-ttu-id="b5c83-211">如需詳細指示，請參閱[啟用和設定儲存體分析](../storage/common/storage-enable-and-view-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="b5c83-211">For detailed instructions, go to [enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="b5c83-212">如果這些延遲也很高，而且與您從 StorSimple 診斷工具收到的數字齊鼓相當，則您需要向 Azure 儲存體登記服務要求。</span><span class="sxs-lookup"><span data-stu-id="b5c83-212">If those latencies are also high and comparable to the numbers you received from the StorSimple Diagnostics tool, then you need to log a service request with Azure storage.</span></span>

    2. <span data-ttu-id="b5c83-213">如果儲存體帳戶延遲較低，請連絡網路系統管理員來調查網路中的延遲問題。</span><span class="sxs-lookup"><span data-stu-id="b5c83-213">If the storage account latencies are low, contact your network administrator to investigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="b5c83-214">在 8100 裝置上執行效能測試的輸出範例</span><span class="sxs-lookup"><span data-stu-id="b5c83-214">Sample output of performance test run on an 8100 device</span></span>

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

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="b5c83-215">附錄︰解譯系統資訊</span><span class="sxs-lookup"><span data-stu-id="b5c83-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="b5c83-216">下表描述系統資訊中各種 Windows PowerShell 參數對應的意義。</span><span class="sxs-lookup"><span data-stu-id="b5c83-216">Here is a table describing what the various Windows PowerShell parameters in the system information map to.</span></span> 

| <span data-ttu-id="b5c83-217">PowerShell 參數</span><span class="sxs-lookup"><span data-stu-id="b5c83-217">PowerShell Parameter</span></span>    | <span data-ttu-id="b5c83-218">說明</span><span class="sxs-lookup"><span data-stu-id="b5c83-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="b5c83-219">執行個體識別碼</span><span class="sxs-lookup"><span data-stu-id="b5c83-219">Instance ID</span></span>             | <span data-ttu-id="b5c83-220">每個控制器都有相關聯的唯一識別碼或 GUID。</span><span class="sxs-lookup"><span data-stu-id="b5c83-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="b5c83-221">名稱</span><span class="sxs-lookup"><span data-stu-id="b5c83-221">Name</span></span>                    | <span data-ttu-id="b5c83-222">在裝置部署期間，透過 Azure 入口網站設定的裝置易記名稱。</span><span class="sxs-lookup"><span data-stu-id="b5c83-222">The friendly name of the device as configured through the Azure portal during device deployment.</span></span> <span data-ttu-id="b5c83-223">預設的易記名稱是裝置序號。</span><span class="sxs-lookup"><span data-stu-id="b5c83-223">The default friendly name is the device serial number.</span></span> |
| <span data-ttu-id="b5c83-224">模型</span><span class="sxs-lookup"><span data-stu-id="b5c83-224">Model</span></span>                   | <span data-ttu-id="b5c83-225">StorSimple 8000 系列裝置的機型。</span><span class="sxs-lookup"><span data-stu-id="b5c83-225">The model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="b5c83-226">機型可以是 8100 或 8600。</span><span class="sxs-lookup"><span data-stu-id="b5c83-226">The model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="b5c83-227">SerialNumber</span><span class="sxs-lookup"><span data-stu-id="b5c83-227">SerialNumber</span></span>            | <span data-ttu-id="b5c83-228">裝置序號是在工廠裡指派，長度為 15 個字元。</span><span class="sxs-lookup"><span data-stu-id="b5c83-228">The device serial number is assigned at the factory and is 15 characters long.</span></span> <span data-ttu-id="b5c83-229">例如，8600-SHX0991003G44HT 表示：</span><span class="sxs-lookup"><span data-stu-id="b5c83-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="b5c83-230">8600 – 裝置機型。</span><span class="sxs-lookup"><span data-stu-id="b5c83-230">8600 – Is the device model.</span></span><br><span data-ttu-id="b5c83-231">SHX – 製造場所。</span><span class="sxs-lookup"><span data-stu-id="b5c83-231">SHX – Is the manufacturing site.</span></span><br> <span data-ttu-id="b5c83-232">0991003 – 特定產品。</span><span class="sxs-lookup"><span data-stu-id="b5c83-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="b5c83-233">G44HT– 最後 5 位數會遞增以產生唯一序號。</span><span class="sxs-lookup"><span data-stu-id="b5c83-233">G44HT- the last 5 digits are incremented to create unique serial numbers.</span></span> <span data-ttu-id="b5c83-234">這可能不是連續的組合。</span><span class="sxs-lookup"><span data-stu-id="b5c83-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="b5c83-235">TimeZone</span><span class="sxs-lookup"><span data-stu-id="b5c83-235">TimeZone</span></span>                | <span data-ttu-id="b5c83-236">裝置時區是在裝置部署期間於 Azure 入口網站中設定。</span><span class="sxs-lookup"><span data-stu-id="b5c83-236">The device time zone as configured in the Azure portal during device deployment.</span></span>|
| <span data-ttu-id="b5c83-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="b5c83-237">CurrentController</span></span>       | <span data-ttu-id="b5c83-238">您透過 StorSimple 裝置的 Windows PowerShell 介面連接的控制器。</span><span class="sxs-lookup"><span data-stu-id="b5c83-238">The controller that you are connected to through the Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="b5c83-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="b5c83-239">ActiveController</span></span>        | <span data-ttu-id="b5c83-240">在裝置上運作的控制器，控制所有網路和磁碟作業。</span><span class="sxs-lookup"><span data-stu-id="b5c83-240">The controller that is active on your device and is controlling all the network and disk operations.</span></span> <span data-ttu-id="b5c83-241">這可以是控制器 0 或控制器 1。</span><span class="sxs-lookup"><span data-stu-id="b5c83-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="b5c83-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="b5c83-242">Controller0Status</span></span>       | <span data-ttu-id="b5c83-243">裝置上控制器 0 的狀態。</span><span class="sxs-lookup"><span data-stu-id="b5c83-243">The status of Controller 0 on your device.</span></span> <span data-ttu-id="b5c83-244">控制器狀態可以是正常、復原模式或無法存取。</span><span class="sxs-lookup"><span data-stu-id="b5c83-244">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="b5c83-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="b5c83-245">Controller1Status</span></span>       | <span data-ttu-id="b5c83-246">裝置上控制器 1 的狀態。</span><span class="sxs-lookup"><span data-stu-id="b5c83-246">The status of Controller 1 on your device.</span></span>  <span data-ttu-id="b5c83-247">控制器狀態可以是正常、復原模式或無法存取。</span><span class="sxs-lookup"><span data-stu-id="b5c83-247">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="b5c83-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="b5c83-248">SystemMode</span></span>              | <span data-ttu-id="b5c83-249">StorSimple 裝置的整體狀態。</span><span class="sxs-lookup"><span data-stu-id="b5c83-249">The overall status of your StorSimple device.</span></span> <span data-ttu-id="b5c83-250">裝置狀態可以是正常、維護或已解除 (對應至 Azure 入口網站中的已停用）。</span><span class="sxs-lookup"><span data-stu-id="b5c83-250">The device status can be normal, maintenance, or decommissioned (corresponds to deactivated in the Azure portal).</span></span>|
| <span data-ttu-id="b5c83-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="b5c83-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="b5c83-252">對應至裝置軟體版本的易記字串。</span><span class="sxs-lookup"><span data-stu-id="b5c83-252">The friendly string that corresponds to the device software version.</span></span> <span data-ttu-id="b5c83-253">如果是執行 Update 4 的系統，好易軟體版本會是 StorSimple 8000 Series Update 4.0。</span><span class="sxs-lookup"><span data-stu-id="b5c83-253">For a system running Update 4, the friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="b5c83-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="b5c83-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="b5c83-255">裝置上執行的 HCS 軟體版本。</span><span class="sxs-lookup"><span data-stu-id="b5c83-255">The HCS software version running on your device.</span></span> <span data-ttu-id="b5c83-256">例如，對應至 StorSimple 8000 Series Update 4.0 的 HCS 軟體版本是 6.3.9600.17820。</span><span class="sxs-lookup"><span data-stu-id="b5c83-256">For instance, the HCS software version corresponding to StorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="b5c83-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="b5c83-257">ApiVersion</span></span>              | <span data-ttu-id="b5c83-258">HCS 裝置的 Windows PowerShell API 軟體版本。</span><span class="sxs-lookup"><span data-stu-id="b5c83-258">The software version of the Windows PowerShell API of the HCS device.</span></span>|
| <span data-ttu-id="b5c83-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="b5c83-259">VhdVersion</span></span>              | <span data-ttu-id="b5c83-260">裝置所隨附之原廠映像的軟體版本。</span><span class="sxs-lookup"><span data-stu-id="b5c83-260">The software version of the factory image that the device was shipped with.</span></span> <span data-ttu-id="b5c83-261">如果您將裝置重設為原廠預設值，它會執行此軟體版本。</span><span class="sxs-lookup"><span data-stu-id="b5c83-261">If you reset your device to factory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="b5c83-262">OSVersion</span><span class="sxs-lookup"><span data-stu-id="b5c83-262">OSVersion</span></span>               | <span data-ttu-id="b5c83-263">裝置上執行之 Windows Server 作業系統的軟體版本。</span><span class="sxs-lookup"><span data-stu-id="b5c83-263">The software version of the Windows Server operating system running on the device.</span></span> <span data-ttu-id="b5c83-264">StorSimple 裝置是根據對應至 6.3.9600 的 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="b5c83-264">The StorSimple device is based off the Windows Server 2012 R2 that corresponds to 6.3.9600.</span></span>|
| <span data-ttu-id="b5c83-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="b5c83-265">CisAgentVersion</span></span>         | <span data-ttu-id="b5c83-266">StorSimple 裝置上執行的 Ci 代理程式版本。</span><span class="sxs-lookup"><span data-stu-id="b5c83-266">The version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="b5c83-267">此代理程式可協助與 Azure 中執行的 StorSimple Manager 服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="b5c83-267">This agent helps communicate with the StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="b5c83-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="b5c83-268">MdsAgentVersion</span></span>         | <span data-ttu-id="b5c83-269">與 StorSimple 裝置上執行的 Mds 代理程式相對應的版本。</span><span class="sxs-lookup"><span data-stu-id="b5c83-269">The version corresponding to the Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="b5c83-270">此代理程式會將資料移至的監視與診斷服務 (MDS)。</span><span class="sxs-lookup"><span data-stu-id="b5c83-270">This agent moves data to the Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="b5c83-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="b5c83-271">Lsisas2Version</span></span>          | <span data-ttu-id="b5c83-272">與 StorSimple 裝置上的 LSI 驅動程式相對應的版本。</span><span class="sxs-lookup"><span data-stu-id="b5c83-272">The version corresponding to the LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="b5c83-273">容量</span><span class="sxs-lookup"><span data-stu-id="b5c83-273">Capacity</span></span>                | <span data-ttu-id="b5c83-274">裝置的總容量 (以位元組為單位)。</span><span class="sxs-lookup"><span data-stu-id="b5c83-274">The total capacity of the device in bytes.</span></span>|
| <span data-ttu-id="b5c83-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="b5c83-275">RemoteManagementMode</span></span>    | <span data-ttu-id="b5c83-276">指出是否可以透過 Windows PowerShell 介面從遠端管理裝置。</span><span class="sxs-lookup"><span data-stu-id="b5c83-276">Indicates whether the device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="b5c83-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="b5c83-277">FipsMode</span></span>                | <span data-ttu-id="b5c83-278">指出您的裝置上是否啟用美國聯邦資訊處理標準 (FIPS) 模式。</span><span class="sxs-lookup"><span data-stu-id="b5c83-278">Indicates whether the United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="b5c83-279">FIPS 140 標準定義核准美國聯邦政府電腦系統所使用的密碼編譯演算法來保護機密資料。</span><span class="sxs-lookup"><span data-stu-id="b5c83-279">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span> <span data-ttu-id="b5c83-280">如果是執行 Update 4 或更新版本的裝置，預設會啟用 FIPS 模式。</span><span class="sxs-lookup"><span data-stu-id="b5c83-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b5c83-281">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b5c83-281">Next steps</span></span>

* <span data-ttu-id="b5c83-282">了解 [Invoke-HcsDiagnostics Cmdlet 的語法](https://technet.microsoft.com/library/mt795371.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b5c83-282">Learn the [syntax of the Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="b5c83-283">深入了解如何在 StorSimple 裝置上[針對部署問題進行疑難排解](storsimple-troubleshoot-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="b5c83-283">Learn more about how to [troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>
