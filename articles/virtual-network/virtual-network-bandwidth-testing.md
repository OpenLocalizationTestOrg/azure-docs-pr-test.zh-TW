---
title: "測試 Azure VM 網路輸送量 | Microsoft Docs"
description: "了解如何測試 Azure 虛擬機器網路輸送量。"
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/21/2017
ms.author: steveesp
ms.openlocfilehash: ccebc722386a19014674d7a59757a3685bd50793
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a><span data-ttu-id="66b18-103">頻寬/輸送量測試 (NTTTCP)</span><span class="sxs-lookup"><span data-stu-id="66b18-103">Bandwidth/Throughput testing (NTTTCP)</span></span>

<span data-ttu-id="66b18-104">在 Azure 中測試網路輸送量效能時，最好是使用工具來針對網路進行測試，而儘量不使用其他可能影響效能的資源。</span><span class="sxs-lookup"><span data-stu-id="66b18-104">When testing network throughput performance in Azure, it's best to use a tool that targets the network for testing and minimizes the use of other resources that could impact performance.</span></span> <span data-ttu-id="66b18-105">建議使用 NTTTCP。</span><span class="sxs-lookup"><span data-stu-id="66b18-105">NTTTCP is recommended.</span></span>

<span data-ttu-id="66b18-106">請將工具複製到兩個大小相同的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="66b18-106">Copy the tool to two Azure VMs of the same size.</span></span> <span data-ttu-id="66b18-107">一個 VM 作為「傳送端」，另一個作為「接收端」。</span><span class="sxs-lookup"><span data-stu-id="66b18-107">One VM functions as SENDER and the other as RECEIVER.</span></span>

#### <a name="deploying-vms-for-testing"></a><span data-ttu-id="66b18-108">部署用於測試的 VM</span><span class="sxs-lookup"><span data-stu-id="66b18-108">Deploying VMs for testing</span></span>
<span data-ttu-id="66b18-109">基於這項測試的目的，兩個 VM 應該位於相同的「雲端服務」或相同的「可用性設定組」中，以便我們使用其內部 IP 並將「負載平衡器」從測試中排除。</span><span class="sxs-lookup"><span data-stu-id="66b18-109">For the purposes of this test, the two VMs should be in either the same Cloud Service or the same Availability Set so that we can use their internal IPs and exclude the Load Balancers from the test.</span></span> <span data-ttu-id="66b18-110">您可以使用 VIP 進行測試，但這類型的測試不在本文件的涵蓋範圍內。</span><span class="sxs-lookup"><span data-stu-id="66b18-110">It is possible to test with the VIP but this kind of testing is outside the scope of this document.</span></span>
 
<span data-ttu-id="66b18-111">記下「傳送端」的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="66b18-111">Make a note of the RECEIVER's IP address.</span></span> <span data-ttu-id="66b18-112">讓我將該 IP 稱為 "a.b.c.r"</span><span class="sxs-lookup"><span data-stu-id="66b18-112">Let's call that IP "a.b.c.r"</span></span>

<span data-ttu-id="66b18-113">記下該 VM 上的核心數目。</span><span class="sxs-lookup"><span data-stu-id="66b18-113">Make a note of the number of cores on the VM.</span></span> <span data-ttu-id="66b18-114">讓我們將此稱為 "\#num\_cores"</span><span class="sxs-lookup"><span data-stu-id="66b18-114">Let's call this "\#num\_cores"</span></span>
 
<span data-ttu-id="66b18-115">在傳送端 VM 和接收端 VM 上執行長達 300 秒 (或 5 分鐘) 的 NTTTCP 測試。</span><span class="sxs-lookup"><span data-stu-id="66b18-115">Run the NTTTCP test for 300 seconds (or 5 minutes) on the sender VM and receiver VM.</span></span>

<span data-ttu-id="66b18-116">提示：第一次設定此測試時，您可以嘗試較短的測試期間以更快獲得回饋。</span><span class="sxs-lookup"><span data-stu-id="66b18-116">Tip: When setting up this test for the first time, you might try a shorter test period to get feedback sooner.</span></span> <span data-ttu-id="66b18-117">在工具如預期般運作之後，請將測試期間延長到 300 秒以獲得最精確的結果。</span><span class="sxs-lookup"><span data-stu-id="66b18-117">Once the tool is working as expected, extend the test period to 300 seconds for the most accurate results.</span></span>

> [!NOTE]
> <span data-ttu-id="66b18-118">傳送端**和**接收端必須指定**相同的**測試持續時間參數 (-t)。</span><span class="sxs-lookup"><span data-stu-id="66b18-118">The sender **and** receiver must specify **the same** test duration parameter (-t).</span></span>

<span data-ttu-id="66b18-119">測試單一 TCP 串流 10 秒：</span><span class="sxs-lookup"><span data-stu-id="66b18-119">To test a single TCP stream for 10 seconds:</span></span>

<span data-ttu-id="66b18-120">接收端參數：ntttcp -r -t 10 -P 1</span><span class="sxs-lookup"><span data-stu-id="66b18-120">Receiver parameters: ntttcp -r -t 10 -P 1</span></span>

<span data-ttu-id="66b18-121">傳送端參數：ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span><span class="sxs-lookup"><span data-stu-id="66b18-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span></span>

> [!NOTE]
> <span data-ttu-id="66b18-122">上述範例應該僅用來確認您的組態。</span><span class="sxs-lookup"><span data-stu-id="66b18-122">The preceding sample should only be used to confirm your configuration.</span></span> <span data-ttu-id="66b18-123">本文稍後會提供有效的測試範例。</span><span class="sxs-lookup"><span data-stu-id="66b18-123">Valid examples of testing are covered later in this document.</span></span>

## <a name="testing-vms-running-windows"></a><span data-ttu-id="66b18-124">測試執行 Windows 的 VM：</span><span class="sxs-lookup"><span data-stu-id="66b18-124">Testing VMs running WINDOWS:</span></span>

#### <a name="get-ntttcp-onto-the-vms"></a><span data-ttu-id="66b18-125">請將 NTTTCP 放到 VM 上。</span><span class="sxs-lookup"><span data-stu-id="66b18-125">Get NTTTCP onto the VMs.</span></span>

<span data-ttu-id="66b18-126">下載最新版本：<https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span><span class="sxs-lookup"><span data-stu-id="66b18-126">Download the latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span></span>

<span data-ttu-id="66b18-127">或搜尋它 (如果已移動)：<https://www.bing.com/search?q=ntttcp+download>\< -- 應該是第一個點選項目</span><span class="sxs-lookup"><span data-stu-id="66b18-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span></span>

<span data-ttu-id="66b18-128">請考慮將 NTTTCP 放在個別的資料夾，例如 c:\\tools</span><span class="sxs-lookup"><span data-stu-id="66b18-128">Consider putting NTTTCP in separate folder, like c:\\tools</span></span>

#### <a name="allow-ntttcp-through-the-windows-firewall"></a><span data-ttu-id="66b18-129">允許 NTTTCP 通過 Windows 防火牆</span><span class="sxs-lookup"><span data-stu-id="66b18-129">Allow NTTTCP through the Windows firewall</span></span>
<span data-ttu-id="66b18-130">在「接收端」的 Windows 防火牆上建立一個「允許」規則，以允許 NTTTCP 流量到達。</span><span class="sxs-lookup"><span data-stu-id="66b18-130">On the RECEIVER, create an Allow rule on the Windows Firewall to allow the NTTTCP traffic to arrive.</span></span> <span data-ttu-id="66b18-131">最簡單的方式是依名稱允許整個 NTTTCP 程式，而不是允許特定的輸入 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="66b18-131">It's easiest to allow the entire NTTTCP program by name rather than to allow specific TCP ports inbound.</span></span>

<span data-ttu-id="66b18-132">請依照下列方式允許 NTTTCP 通過 Windows 防火牆：</span><span class="sxs-lookup"><span data-stu-id="66b18-132">Allow ntttcp through the Windows Firewall like this:</span></span>

<span data-ttu-id="66b18-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="66b18-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

<span data-ttu-id="66b18-134">例如，如果您將 ntttcp.exe 複製到 "c:\\tools" 資料夾，則命令會是這樣：</span><span class="sxs-lookup"><span data-stu-id="66b18-134">For example, if you copied ntttcp.exe to the "c:\\tools" folder, this would be the command:</span></span> 

<span data-ttu-id="66b18-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="66b18-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

#### <a name="running-ntttcp-tests"></a><span data-ttu-id="66b18-136">執行 NTTTCP 測試</span><span class="sxs-lookup"><span data-stu-id="66b18-136">Running NTTTCP tests</span></span>

<span data-ttu-id="66b18-137">啟動「接收端」上的 NTTTCP (**從 CMD 執行**，不是從 PowerShell)：</span><span class="sxs-lookup"><span data-stu-id="66b18-137">Start NTTTCP on the RECEIVER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="66b18-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span><span class="sxs-lookup"><span data-stu-id="66b18-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span></span>

<span data-ttu-id="66b18-139">如果 VM 有四個核心且 IP 位址為 10.0.0.4，就會看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="66b18-139">If the VM has four cores and an IP address of 10.0.0.4, it would look like this:</span></span>

<span data-ttu-id="66b18-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="66b18-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span></span>


<span data-ttu-id="66b18-141">啟動「傳送端」上的 NTTTCP (**從 CMD 執行**，不是從 PowerShell)：</span><span class="sxs-lookup"><span data-stu-id="66b18-141">Start NTTTCP on the SENDER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="66b18-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="66b18-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span></span> 

<span data-ttu-id="66b18-143">等候結果。</span><span class="sxs-lookup"><span data-stu-id="66b18-143">Wait for the results.</span></span>


## <a name="testing-vms-running-linux"></a><span data-ttu-id="66b18-144">測試執行 Linux 的 VM：</span><span class="sxs-lookup"><span data-stu-id="66b18-144">Testing VMs running LINUX:</span></span>

<span data-ttu-id="66b18-145">請使用 nttcp-for-linux。</span><span class="sxs-lookup"><span data-stu-id="66b18-145">Use nttcp-for-linux.</span></span> <span data-ttu-id="66b18-146">可從 <https://github.com/Microsoft/ntttcp-for-linux> 取得</span><span class="sxs-lookup"><span data-stu-id="66b18-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span></span>

<span data-ttu-id="66b18-147">在 Linux VM (「傳送端」和「接收端」兩者) 上，執行下列命令以在 VM 上準備 ntttcp-for-linux：</span><span class="sxs-lookup"><span data-stu-id="66b18-147">On the Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span></span>

<span data-ttu-id="66b18-148">CentOS - 安裝 Git：</span><span class="sxs-lookup"><span data-stu-id="66b18-148">CentOS - Install Git:</span></span>
``` bash
  yum install gcc -y  
  yum install git -y
```
<span data-ttu-id="66b18-149">Ubuntu - 安裝 Git：</span><span class="sxs-lookup"><span data-stu-id="66b18-149">Ubuntu - Install Git:</span></span>
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
<span data-ttu-id="66b18-150">在兩部機器上都建立並安裝：</span><span class="sxs-lookup"><span data-stu-id="66b18-150">Make and Install on both:</span></span>
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

<span data-ttu-id="66b18-151">與 Windows 範例中相同，我們假設 Linux「接收端」的 IP 為 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="66b18-151">As in the Windows example, we assume the Linux RECEIVER's IP is 10.0.0.4</span></span>

<span data-ttu-id="66b18-152">啟動「接收端」上的 NTTTCP-for-Linux：</span><span class="sxs-lookup"><span data-stu-id="66b18-152">Start NTTTCP-for-Linux on the RECEIVER:</span></span>

``` bash
ntttcp -r -t 300
```

<span data-ttu-id="66b18-153">然後在「傳送端」上執行：</span><span class="sxs-lookup"><span data-stu-id="66b18-153">And on the SENDER, run:</span></span>

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
<span data-ttu-id="66b18-154">如果未提供時間參數，則測試時間長度預設為 60 秒</span><span class="sxs-lookup"><span data-stu-id="66b18-154">Test length defaults to 60 seconds if no time parameter is given</span></span>

## <a name="testing-between-vms-running-windows-and-linux"></a><span data-ttu-id="66b18-155">在執行 Windows 和 LINUX 的 VM 之間進行測試：</span><span class="sxs-lookup"><span data-stu-id="66b18-155">Testing between VMs running Windows and LINUX:</span></span>

<span data-ttu-id="66b18-156">在此案例中，我們應該啟用非同步模式，才能執行測試。</span><span class="sxs-lookup"><span data-stu-id="66b18-156">On this scenarios we should enable the no-sync mode so the test can run.</span></span> <span data-ttu-id="66b18-157">若要執行上述動作，請針對 Linux 使用 **-N 旗標**；針對 Windows 使用 **-ns 旗標**。</span><span class="sxs-lookup"><span data-stu-id="66b18-157">This is done by using the **-N flag** for Linux, and **-ns flag** for Windows.</span></span>

#### <a name="from-linux-to-windows"></a><span data-ttu-id="66b18-158">從 Linux 到 Windows：</span><span class="sxs-lookup"><span data-stu-id="66b18-158">From Linux to Windows:</span></span>

<span data-ttu-id="66b18-159">接收者 <Windows>：</span><span class="sxs-lookup"><span data-stu-id="66b18-159">Receiver <Windows>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

<span data-ttu-id="66b18-160">傳送者 <Linux>：</span><span class="sxs-lookup"><span data-stu-id="66b18-160">Sender <Linux> :</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-to-linux"></a><span data-ttu-id="66b18-161">從 Windows 到 Linux：</span><span class="sxs-lookup"><span data-stu-id="66b18-161">From Windows to Linux:</span></span>

<span data-ttu-id="66b18-162">接收者 <Linux>：</span><span class="sxs-lookup"><span data-stu-id="66b18-162">Receiver <Linux>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

<span data-ttu-id="66b18-163">傳送者 <Windows>：</span><span class="sxs-lookup"><span data-stu-id="66b18-163">Sender <Windows>:</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a><span data-ttu-id="66b18-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="66b18-164">Next steps</span></span>
* <span data-ttu-id="66b18-165">視結果而定，可能有將您案例的[網路輸送量機器最佳化](virtual-network-optimize-network-bandwidth.md)的空間。</span><span class="sxs-lookup"><span data-stu-id="66b18-165">Depending on results, there may be room to [Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span></span>
* <span data-ttu-id="66b18-166">深入了解 [Azure 虛擬網路的常見問題 (FAQ)](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="66b18-166">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
