---
title: "aaaTesting Azure VM 網路輸送量 |Microsoft 文件"
description: "了解如何 tootest Azure 虛擬機器的網路輸送量。"
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
ms.openlocfilehash: 2da85c27bc8d16a443b215891f4cd0460f41926f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a><span data-ttu-id="4822c-103">頻寬/輸送量測試 (NTTTCP)</span><span class="sxs-lookup"><span data-stu-id="4822c-103">Bandwidth/Throughput testing (NTTTCP)</span></span>

<span data-ttu-id="4822c-104">測試網路輸送量效能，請在 Azure 中時，最佳 toouse 目標 hello 網路進行測試，可能會影響效能的其他資源的 hello 使用降至最低的工具。</span><span class="sxs-lookup"><span data-stu-id="4822c-104">When testing network throughput performance in Azure, it's best toouse a tool that targets hello network for testing and minimizes hello use of other resources that could impact performance.</span></span> <span data-ttu-id="4822c-105">建議使用 NTTTCP。</span><span class="sxs-lookup"><span data-stu-id="4822c-105">NTTTCP is recommended.</span></span>

<span data-ttu-id="4822c-106">複製 hello 工具 tootwo hello 的 Azure Vm 大小相同。</span><span class="sxs-lookup"><span data-stu-id="4822c-106">Copy hello tool tootwo Azure VMs of hello same size.</span></span> <span data-ttu-id="4822c-107">一個 VM 做為傳送者和接收者為其他 hello。</span><span class="sxs-lookup"><span data-stu-id="4822c-107">One VM functions as SENDER and hello other as RECEIVER.</span></span>

#### <a name="deploying-vms-for-testing"></a><span data-ttu-id="4822c-108">部署用於測試的 VM</span><span class="sxs-lookup"><span data-stu-id="4822c-108">Deploying VMs for testing</span></span>
<span data-ttu-id="4822c-109">基於 hello 這項測試，兩個 Vm 應該位於 hello hello 相同雲端服務或 hello 相同可用性設定組，讓我們能夠使用其內部 Ip 並排除 hello 測試 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="4822c-109">For hello purposes of this test, hello two VMs should be in either hello same Cloud Service or hello same Availability Set so that we can use their internal IPs and exclude hello Load Balancers from hello test.</span></span> <span data-ttu-id="4822c-110">它是以 hello VIP 可能 tootest，但這種測試是在這份文件 hello 範圍之外。</span><span class="sxs-lookup"><span data-stu-id="4822c-110">It is possible tootest with hello VIP but this kind of testing is outside hello scope of this document.</span></span>
 
<span data-ttu-id="4822c-111">記下 hello 接收者的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4822c-111">Make a note of hello RECEIVER's IP address.</span></span> <span data-ttu-id="4822c-112">讓我將該 IP 稱為 "a.b.c.r"</span><span class="sxs-lookup"><span data-stu-id="4822c-112">Let's call that IP "a.b.c.r"</span></span>

<span data-ttu-id="4822c-113">記下的核心數目 hello hello VM 上。</span><span class="sxs-lookup"><span data-stu-id="4822c-113">Make a note of hello number of cores on hello VM.</span></span> <span data-ttu-id="4822c-114">讓我們將此稱為 "\#num\_cores"</span><span class="sxs-lookup"><span data-stu-id="4822c-114">Let's call this "\#num\_cores"</span></span>
 
<span data-ttu-id="4822c-115">VM hello 寄件者和接收者 VM 上執行的 hello NTTTCP 測試 300 秒 （或 5 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="4822c-115">Run hello NTTTCP test for 300 seconds (or 5 minutes) on hello sender VM and receiver VM.</span></span>

<span data-ttu-id="4822c-116">提示： 當第一次設定這項測試的 hello，您可以嘗試較短的測試週期 tooget 意見反應更快。</span><span class="sxs-lookup"><span data-stu-id="4822c-116">Tip: When setting up this test for hello first time, you might try a shorter test period tooget feedback sooner.</span></span> <span data-ttu-id="4822c-117">一旦 hello 工具如預期般，擴充 hello 測試期間 too300 秒 hello 最精確的結果。</span><span class="sxs-lookup"><span data-stu-id="4822c-117">Once hello tool is working as expected, extend hello test period too300 seconds for hello most accurate results.</span></span>

> [!NOTE]
> <span data-ttu-id="4822c-118">hello 寄件者**和**接收者必須指定**hello 相同**測試持續時間參數 (-t)。</span><span class="sxs-lookup"><span data-stu-id="4822c-118">hello sender **and** receiver must specify **hello same** test duration parameter (-t).</span></span>

<span data-ttu-id="4822c-119">tootest 10 秒的單一 TCP 資料流：</span><span class="sxs-lookup"><span data-stu-id="4822c-119">tootest a single TCP stream for 10 seconds:</span></span>

<span data-ttu-id="4822c-120">接收端參數：ntttcp -r -t 10 -P 1</span><span class="sxs-lookup"><span data-stu-id="4822c-120">Receiver parameters: ntttcp -r -t 10 -P 1</span></span>

<span data-ttu-id="4822c-121">傳送端參數：ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span><span class="sxs-lookup"><span data-stu-id="4822c-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span></span>

> [!NOTE]
> <span data-ttu-id="4822c-122">上述範例中的 hello 應該只能使用的 tooconfirm 您的設定。</span><span class="sxs-lookup"><span data-stu-id="4822c-122">hello preceding sample should only be used tooconfirm your configuration.</span></span> <span data-ttu-id="4822c-123">本文稍後會提供有效的測試範例。</span><span class="sxs-lookup"><span data-stu-id="4822c-123">Valid examples of testing are covered later in this document.</span></span>

## <a name="testing-vms-running-windows"></a><span data-ttu-id="4822c-124">測試執行 Windows 的 VM：</span><span class="sxs-lookup"><span data-stu-id="4822c-124">Testing VMs running WINDOWS:</span></span>

#### <a name="get-ntttcp-onto-hello-vms"></a><span data-ttu-id="4822c-125">NTTTCP 進入 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="4822c-125">Get NTTTCP onto hello VMs.</span></span>

<span data-ttu-id="4822c-126">下載最新版本的 hello: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span><span class="sxs-lookup"><span data-stu-id="4822c-126">Download hello latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span></span>

<span data-ttu-id="4822c-127">或搜尋它 (如果已移動)：<https://www.bing.com/search?q=ntttcp+download>\< -- 應該是第一個點選項目</span><span class="sxs-lookup"><span data-stu-id="4822c-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span></span>

<span data-ttu-id="4822c-128">請考慮將 NTTTCP 放在個別的資料夾，例如 c:\\tools</span><span class="sxs-lookup"><span data-stu-id="4822c-128">Consider putting NTTTCP in separate folder, like c:\\tools</span></span>

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a><span data-ttu-id="4822c-129">透過 hello 的 Windows 防火牆允許 NTTTCP</span><span class="sxs-lookup"><span data-stu-id="4822c-129">Allow NTTTCP through hello Windows firewall</span></span>
<span data-ttu-id="4822c-130">在 hello 接收者，建立允許規則 hello Windows 防火牆 tooallow 上的 NTTTCP 流量 tooarrive。</span><span class="sxs-lookup"><span data-stu-id="4822c-130">On hello RECEIVER, create an Allow rule on hello Windows Firewall tooallow the NTTTCP traffic tooarrive.</span></span> <span data-ttu-id="4822c-131">它是最簡單 tooallow hello 整個 NTTTCP 程式名稱而不是輸入 tooallow 特定 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="4822c-131">It's easiest tooallow hello entire NTTTCP program by name rather than tooallow specific TCP ports inbound.</span></span>

<span data-ttu-id="4822c-132">允許 ntttcp 透過 hello Windows 防火牆，就像這樣：</span><span class="sxs-lookup"><span data-stu-id="4822c-132">Allow ntttcp through hello Windows Firewall like this:</span></span>

<span data-ttu-id="4822c-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="4822c-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

<span data-ttu-id="4822c-134">例如，如果您複製 ntttcp.exe toohello"c:\\工具 」 資料夾中，這會是 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="4822c-134">For example, if you copied ntttcp.exe toohello "c:\\tools" folder, this would be hello command:</span></span> 

<span data-ttu-id="4822c-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="4822c-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

#### <a name="running-ntttcp-tests"></a><span data-ttu-id="4822c-136">執行 NTTTCP 測試</span><span class="sxs-lookup"><span data-stu-id="4822c-136">Running NTTTCP tests</span></span>

<span data-ttu-id="4822c-137">Hello 接收者上啟動 NTTTCP (**從 CMD 執行**，而不是從 PowerShell):</span><span class="sxs-lookup"><span data-stu-id="4822c-137">Start NTTTCP on hello RECEIVER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="4822c-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span><span class="sxs-lookup"><span data-stu-id="4822c-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span></span>

<span data-ttu-id="4822c-139">如果 hello VM 有四個核心和 IP 位址為 10.0.0.4，它看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="4822c-139">If hello VM has four cores and an IP address of 10.0.0.4, it would look like this:</span></span>

<span data-ttu-id="4822c-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="4822c-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span></span>


<span data-ttu-id="4822c-141">Hello 寄件者上啟動 NTTTCP (**從 CMD 執行**，而不是從 PowerShell):</span><span class="sxs-lookup"><span data-stu-id="4822c-141">Start NTTTCP on hello SENDER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="4822c-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="4822c-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span></span> 

<span data-ttu-id="4822c-143">等候 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="4822c-143">Wait for hello results.</span></span>


## <a name="testing-vms-running-linux"></a><span data-ttu-id="4822c-144">測試執行 Linux 的 VM：</span><span class="sxs-lookup"><span data-stu-id="4822c-144">Testing VMs running LINUX:</span></span>

<span data-ttu-id="4822c-145">請使用 nttcp-for-linux。</span><span class="sxs-lookup"><span data-stu-id="4822c-145">Use nttcp-for-linux.</span></span> <span data-ttu-id="4822c-146">可從 <https://github.com/Microsoft/ntttcp-for-linux> 取得</span><span class="sxs-lookup"><span data-stu-id="4822c-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span></span>

<span data-ttu-id="4822c-147">在 hello Linux Vm （傳送者和接收者），執行這些命令來準備 ntttcp-為-linux Vm 上：</span><span class="sxs-lookup"><span data-stu-id="4822c-147">On hello Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span></span>

<span data-ttu-id="4822c-148">CentOS - 安裝 Git：</span><span class="sxs-lookup"><span data-stu-id="4822c-148">CentOS - Install Git:</span></span>
``` bash
  yum install gcc -y  
  yum install git -y
```
<span data-ttu-id="4822c-149">Ubuntu - 安裝 Git：</span><span class="sxs-lookup"><span data-stu-id="4822c-149">Ubuntu - Install Git:</span></span>
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
<span data-ttu-id="4822c-150">在兩部機器上都建立並安裝：</span><span class="sxs-lookup"><span data-stu-id="4822c-150">Make and Install on both:</span></span>
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

<span data-ttu-id="4822c-151">如同 hello Windows 範例中，我們假設是 10.0.0.4 hello Linux 接收者的 IP。</span><span class="sxs-lookup"><span data-stu-id="4822c-151">As in hello Windows example, we assume hello Linux RECEIVER's IP is 10.0.0.4</span></span>

<span data-ttu-id="4822c-152">啟動 NTTTCP 為 Linux hello 接收者上：</span><span class="sxs-lookup"><span data-stu-id="4822c-152">Start NTTTCP-for-Linux on hello RECEIVER:</span></span>

``` bash
ntttcp -r -t 300
```

<span data-ttu-id="4822c-153">然後在 hello 寄件者，執行：</span><span class="sxs-lookup"><span data-stu-id="4822c-153">And on hello SENDER, run:</span></span>

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
<span data-ttu-id="4822c-154">指定測試長度預設值 too60 秒如果沒有時間參數</span><span class="sxs-lookup"><span data-stu-id="4822c-154">Test length defaults too60 seconds if no time parameter is given</span></span>

## <a name="testing-between-vms-running-windows-and-linux"></a><span data-ttu-id="4822c-155">在執行 Windows 和 LINUX 的 VM 之間進行測試：</span><span class="sxs-lookup"><span data-stu-id="4822c-155">Testing between VMs running Windows and LINUX:</span></span>

<span data-ttu-id="4822c-156">此案例中，我們應該啟用 hello 沒有同步處理模式讓 hello 測試執行。</span><span class="sxs-lookup"><span data-stu-id="4822c-156">On this scenarios we should enable hello no-sync mode so hello test can run.</span></span> <span data-ttu-id="4822c-157">這是使用 hello **-N 旗標**for Linux，和**奈旗標**for Windows。</span><span class="sxs-lookup"><span data-stu-id="4822c-157">This is done by using hello **-N flag** for Linux, and **-ns flag** for Windows.</span></span>

#### <a name="from-linux-toowindows"></a><span data-ttu-id="4822c-158">從 Linux tooWindows:</span><span class="sxs-lookup"><span data-stu-id="4822c-158">From Linux tooWindows:</span></span>

<span data-ttu-id="4822c-159">接收者 <Windows>：</span><span class="sxs-lookup"><span data-stu-id="4822c-159">Receiver <Windows>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

<span data-ttu-id="4822c-160">傳送者 <Linux>：</span><span class="sxs-lookup"><span data-stu-id="4822c-160">Sender <Linux> :</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a><span data-ttu-id="4822c-161">從 Windows tooLinux:</span><span class="sxs-lookup"><span data-stu-id="4822c-161">From Windows tooLinux:</span></span>

<span data-ttu-id="4822c-162">接收者 <Linux>：</span><span class="sxs-lookup"><span data-stu-id="4822c-162">Receiver <Linux>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

<span data-ttu-id="4822c-163">傳送者 <Windows>：</span><span class="sxs-lookup"><span data-stu-id="4822c-163">Sender <Windows>:</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a><span data-ttu-id="4822c-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4822c-164">Next steps</span></span>
* <span data-ttu-id="4822c-165">根據不同的結果，可能有空間太[最佳化網路輸送量機器](virtual-network-optimize-network-bandwidth.md)您的案例。</span><span class="sxs-lookup"><span data-stu-id="4822c-165">Depending on results, there may be room too[Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span></span>
* <span data-ttu-id="4822c-166">深入了解 [Azure 虛擬網路的常見問題 (FAQ)](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="4822c-166">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
