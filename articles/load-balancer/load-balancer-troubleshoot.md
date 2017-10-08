---
title: "aaaTroubleshoot Azure 負載平衡器 |Microsoft 文件"
description: "針對 Azure Load Balancer 的已知問題進行疑難排解"
services: load-balancer
documentationcenter: na
author: RamanDhillon
manager: timlt
editor: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/10/2017
ms.author: kumud
ms.openlocfilehash: 56b73fcbf0bbf18cedfd113a280cfafa2a3dc9f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-load-balancer"></a><span data-ttu-id="82261-103">針對 Azure Load Balancer 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="82261-103">Troubleshoot Azure Load Balancer</span></span>

<span data-ttu-id="82261-104">此頁面提供 Azure Load Balancer 常見問題的疑難排解資訊。</span><span class="sxs-lookup"><span data-stu-id="82261-104">This page provides troubleshooting information for common Azure Load Balancer questions.</span></span> <span data-ttu-id="82261-105">Hello 負載平衡器連線無法使用時，hello 最常見的徵兆如下：</span><span class="sxs-lookup"><span data-stu-id="82261-105">When hello Load Balancer connectivity is unavailable, hello most common symptoms are as follows:</span></span> 
- <span data-ttu-id="82261-106">Hello 負載平衡器後方的 Vm 都沒有回應 toohealth 探查</span><span class="sxs-lookup"><span data-stu-id="82261-106">VMs behind hello Load Balancer are not responding toohealth probes</span></span> 
- <span data-ttu-id="82261-107">Hello 負載平衡器後方的 Vm 都沒有回應 hello 設定連接埠上的 toohello 流量</span><span class="sxs-lookup"><span data-stu-id="82261-107">VMs behind hello Load Balancer are not responding toohello traffic on hello configured port</span></span>

## <a name="symptom-vms-behind-hello-load-balancer-are-not-responding-toohealth-probes"></a><span data-ttu-id="82261-108">徵兆： Hello 負載平衡器後方的 Vm 都沒有回應 toohealth 探查</span><span class="sxs-lookup"><span data-stu-id="82261-108">Symptom: VMs behind hello Load Balancer are not responding toohealth probes</span></span>
<span data-ttu-id="82261-109">集中 hello 負載平衡器後端伺服器 tooparticipate hello，它們必須通過 hello 探查核取。</span><span class="sxs-lookup"><span data-stu-id="82261-109">For hello backend servers tooparticipate in hello load balancer set, they must pass hello probe check.</span></span> <span data-ttu-id="82261-110">如需健康狀態探查的詳細資訊，請參閱[了解負載平衡器探查](load-balancer-custom-probe-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="82261-110">For more information about health probes, see [Understanding Load Balancer Probes](load-balancer-custom-probe-overview.md).</span></span> 

<span data-ttu-id="82261-111">hello 負載平衡器後端集區的 Vm 可能沒有回應探查 toohello 到期 tooany 的 hello 下列原因：</span><span class="sxs-lookup"><span data-stu-id="82261-111">hello Load Balancer backend pool VMs may not be responding toohello probes due tooany of hello following reasons:</span></span> 
- <span data-ttu-id="82261-112">負載平衡器後端集區 VM 的健康狀態不良</span><span class="sxs-lookup"><span data-stu-id="82261-112">Load Balancer backend pool VM is unhealthy</span></span> 
- <span data-ttu-id="82261-113">負載平衡器後端集區 VM 未接聽 hello 探查連接埠</span><span class="sxs-lookup"><span data-stu-id="82261-113">Load Balancer backend pool VM is not listening on hello probe port</span></span> 
- <span data-ttu-id="82261-114">防火牆或網路安全性小組已封鎖 hello hello 負載平衡器後端集區的 Vm 上的連接埠</span><span class="sxs-lookup"><span data-stu-id="82261-114">Firewall, or a network security group is blocking hello port on hello Load Balancer backend pool VMs</span></span> 
- <span data-ttu-id="82261-115">負載平衡器中的其他設定錯誤</span><span class="sxs-lookup"><span data-stu-id="82261-115">Other misconfigurations in Load Balancer</span></span>

### <a name="cause-1-load-balancer-backend-pool-vm-is-unhealthy"></a><span data-ttu-id="82261-116">原因 1︰負載平衡器後端集區 VM 的健康狀態不良</span><span class="sxs-lookup"><span data-stu-id="82261-116">Cause 1: Load Balancer backend pool VM is unhealthy</span></span> 

<span data-ttu-id="82261-117">**驗證和解決方式**</span><span class="sxs-lookup"><span data-stu-id="82261-117">**Validation and resolution**</span></span>

<span data-ttu-id="82261-118">tooresolve 這個問題，請登入參與的 Vm，toohello，並檢查是否 hello VM 狀態為狀況良好，並可在回應太**PsPing**或**TCPing**從 hello 集區中的另一個 VM。</span><span class="sxs-lookup"><span data-stu-id="82261-118">tooresolve this issue, log in toohello participating VMs, and check if hello VM state is healthy, and can respond too**PsPing** or **TCPing** from another VM in hello pool.</span></span> <span data-ttu-id="82261-119">如果 hello VM 會處於狀況不良，或無法 toorespond toohello 探查，您必須更正 hello 問題並取得的 hello VM 可以參與負載平衡之前，備份 tooa 狀況良好狀態。</span><span class="sxs-lookup"><span data-stu-id="82261-119">If hello VM is unhealthy, or is unable toorespond toohello probe, you must rectify hello issue and get hello VM back tooa healthy state before it can participate in load balancing.</span></span>

### <a name="cause-2-load-balancer-backend-pool-vm-is-not-listening-on-hello-probe-port"></a><span data-ttu-id="82261-120">原因 2： 負載平衡器後端集區 VM 未接聽 hello 探查連接埠</span><span class="sxs-lookup"><span data-stu-id="82261-120">Cause 2: Load Balancer backend pool VM is not listening on hello probe port</span></span>
<span data-ttu-id="82261-121">如果 hello VM 的狀況良好，但沒有回應 toohello 探查，然後一個可能的原因可能 hello 探查連接埠上未開啟 hello 參與 VM，或者 hello VM 未接聽該通訊埠。</span><span class="sxs-lookup"><span data-stu-id="82261-121">If hello VM is healthy, but is not responding toohello probe, then one possible reason could be that hello probe port is not open on hello participating VM, or hello VM is not listening on that port.</span></span>

<span data-ttu-id="82261-122">**驗證和解決方式**</span><span class="sxs-lookup"><span data-stu-id="82261-122">**Validation and resolution**</span></span>

1. <span data-ttu-id="82261-123">登入 toohello 後端 VM。</span><span class="sxs-lookup"><span data-stu-id="82261-123">Log in toohello backend VM.</span></span> 
2. <span data-ttu-id="82261-124">開啟命令提示字元並執行下列命令 toovalidate 沒有接聽 hello 探查連接埠之應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="82261-124">Open a command prompt and run hello following command toovalidate there is an application listening on hello probe port:</span></span>   
            <span data-ttu-id="82261-125">netstat -an</span><span class="sxs-lookup"><span data-stu-id="82261-125">netstat -an</span></span>
3. <span data-ttu-id="82261-126">如果 hello 連接埠狀態未列為**聆聽**，設定 hello 適當的連接埠。</span><span class="sxs-lookup"><span data-stu-id="82261-126">If hello port state is not listed as **LISTENING**, configure hello proper port.</span></span> 
4. <span data-ttu-id="82261-127">或者，選取其他已列為 **LISTENING** 的連接埠，並據此更新負載平衡器組態。</span><span class="sxs-lookup"><span data-stu-id="82261-127">Alternatively, select another port, that is listed as **LISTENING**, and update load balancer configuration accordingly.</span></span>              

###<a name="cause-3-firewall-or-a-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vms"></a><span data-ttu-id="82261-128">原因 3： 防火牆或網路安全性小組已封鎖 hello hello 負載平衡器後端集區的 Vm 上的連接埠</span><span class="sxs-lookup"><span data-stu-id="82261-128">Cause 3: Firewall, or a network security group is blocking hello port on hello load balancer backend pool VMs</span></span>  
<span data-ttu-id="82261-129">Hello hello hello 探查連接埠或一或多個網路安全性群組 hello VM，或 hello 子網路上設定封鎖 VM 上的防火牆不允許 hello 探查 tooreach hello 連接埠，hello VM 無法 toorespond toohello 健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="82261-129">If hello firewall on hello VM is blocking hello probe port, or one or more network security groups configured on hello subnet or on hello VM, is not allowing hello probe tooreach hello port, hello VM is unable toorespond toohello health probe.</span></span>          

<span data-ttu-id="82261-130">**驗證和解決方式**</span><span class="sxs-lookup"><span data-stu-id="82261-130">**Validation and resolution**</span></span>

* <span data-ttu-id="82261-131">如果啟用 hello 防火牆，請檢查它是否已設定 tooallow hello 探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="82261-131">If hello firewall is enabled, check if it is configured tooallow hello probe port.</span></span> <span data-ttu-id="82261-132">如果不是，設定 hello 防火牆 tooallow 流量 hello 探查連接埠，然後重新測試。</span><span class="sxs-lookup"><span data-stu-id="82261-132">If not, configure hello firewall tooallow traffic on hello probe port, and test again.</span></span> 
* <span data-ttu-id="82261-133">從網路安全性群組的 hello 清單中，檢查 hello hello 探查連接埠上的傳入或傳出流量是否干擾。</span><span class="sxs-lookup"><span data-stu-id="82261-133">From hello list of network security groups, check if hello incoming or outgoing traffic on hello probe port has interference.</span></span> 
* <span data-ttu-id="82261-134">另請檢查 如果**Deny All**網路安全性群組規則 hello 的 hello VM NIC 上或 hello 的優先順序高於 hello 預設規則，允許 LB 探查 （& s） 流量的子網路 （網路安全性群組必須允許的負載平衡器 IP168.63.129.16)。</span><span class="sxs-lookup"><span data-stu-id="82261-134">Also, check if a **Deny All** network security groups rule on hello NIC of hello VM or hello subnet that has a higher priority than hello default rule that allows LB probes & traffic (network security groups must allow Load Balancer IP of 168.63.129.16).</span></span> 
* <span data-ttu-id="82261-135">如果任何這些規則會封鎖 hello 探查流量，移除並重新設定 hello 規則 tooallow hello 探查流量。</span><span class="sxs-lookup"><span data-stu-id="82261-135">If any of these rules are blocking hello probe traffic, remove and reconfigure hello rules tooallow hello probe traffic.</span></span>  
* <span data-ttu-id="82261-136">測試如果 hello VM 已經開始回應 toohello 健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="82261-136">Test if hello VM has now started responding toohello health probes.</span></span> 

### <a name="cause-4-other-misconfigurations-in-load-balancer"></a><span data-ttu-id="82261-137">原因 4：負載平衡器中的其他設定錯誤</span><span class="sxs-lookup"><span data-stu-id="82261-137">Cause 4: Other misconfigurations in Load Balancer</span></span>
<span data-ttu-id="82261-138">如果所有 hello 上述原因看起來 toobe 進行驗證，並正確地解析 hello 後端 VM 仍不會回應 toohello 健全狀況探查，然後以手動方式連線，測試和收集一些追蹤 toounderstand hello 連線。</span><span class="sxs-lookup"><span data-stu-id="82261-138">If all hello preceding causes seem toobe validated and resolved correctly, and hello backend VM still does not respond toohello health probe, then manually test for connectivity, and collect some traces toounderstand hello connectivity.</span></span>

<span data-ttu-id="82261-139">**驗證和解決方式**</span><span class="sxs-lookup"><span data-stu-id="82261-139">**Validation and resolution**</span></span>

* <span data-ttu-id="82261-140">使用**Psping**從其中一個 hello 內其他 Vm hello VNet tootest hello 探查連接埠回應 (範例：.\psping.exe-t 10.0.0.4:3389) 並記錄結果。</span><span class="sxs-lookup"><span data-stu-id="82261-140">Use **Psping** from one of hello other VMs within hello VNet tootest hello probe port response (example: .\psping.exe -t 10.0.0.4:3389) and record results.</span></span> 
* <span data-ttu-id="82261-141">使用**TCPing**從其中一個 hello 內其他 Vm hello VNet tootest hello 探查連接埠回應 (範例：.\tcping.exe 10.0.0.4 3389) 並記錄結果。</span><span class="sxs-lookup"><span data-stu-id="82261-141">Use **TCPing** from one of hello other VMs within hello VNet tootest hello probe port response (example: .\tcping.exe 10.0.0.4 3389) and record results.</span></span> 
* <span data-ttu-id="82261-142">如果這些 ping 測試都沒有收到任何回應，則</span><span class="sxs-lookup"><span data-stu-id="82261-142">If no response is received in these ping tests, then</span></span>
    - <span data-ttu-id="82261-143">同時執行 Netsh 追蹤 hello 目標後端集區 VM 和 hello 從另一項測試 VM 上相同的 VNet。</span><span class="sxs-lookup"><span data-stu-id="82261-143">Run a simultaneous Netsh trace on hello target backend pool VM and another test VM from hello same VNet.</span></span> <span data-ttu-id="82261-144">現在，執行一些時間的 PsPing 測試、 收集某些網路追蹤，然後再停止 hello 測試。</span><span class="sxs-lookup"><span data-stu-id="82261-144">Now, run a PsPing test for some time, collect some network traces, and then stop hello test.</span></span> 
    - <span data-ttu-id="82261-145">分析 hello 網路擷取，並查看是否有這兩個內送和外寄的封包相關的 toohello ping 查詢。</span><span class="sxs-lookup"><span data-stu-id="82261-145">Analyze hello network capture and see if there are both incoming and outgoing packets related toohello ping query.</span></span> 
        - <span data-ttu-id="82261-146">如果觀察不到任何連入封包 hello 後端集區 VM 上，沒有可能的網路安全性群組或 UDR 組態錯誤封鎖 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="82261-146">If no incoming packets are observed on hello backend pool VM, there is potentially a network security groups or UDR mis-configuration blocking hello traffic.</span></span> 
        - <span data-ttu-id="82261-147">如果沒有傳出的封包 hello 後端集區 VM 上觀察到，hello VM 需要 toobe 檢查任何相關的問題 （eample，應用程式封鎖 hello 探查連接埠)。</span><span class="sxs-lookup"><span data-stu-id="82261-147">If no outgoing packets are observed on hello backend pool VM, hello VM needs toobe checked for any unrelated issues (for eample, Application blocking hello probe port).</span></span> 
    - <span data-ttu-id="82261-148">請確認 hello 探查封包在到達 hello 負載平衡器之前已強制的 tooanother 目的地 （可能是透過 UDR 設定）。</span><span class="sxs-lookup"><span data-stu-id="82261-148">Verify if hello probe packets are being forced tooanother destination (possibly via UDR settings) before reaching hello load balancer.</span></span> <span data-ttu-id="82261-149">這可能會造成 hello 流量 toonever 觸達 hello 後端 VM。</span><span class="sxs-lookup"><span data-stu-id="82261-149">This can cause hello traffic toonever reach hello backend VM.</span></span> 
* <span data-ttu-id="82261-150">變更 hello 探查類型 (例如，HTTP tooTCP) 及設定網路安全性群組 Acl 中的 hello 對應連接埠和防火牆 toovalidate hello 問題是否與探查回應 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="82261-150">Change hello probe type (for example, HTTP tooTCP), and configure hello corresponding port in network security groups ACLs and firewall toovalidate if hello issue is with hello configuration of probe response.</span></span> <span data-ttu-id="82261-151">如需健康狀態探查組態的詳細資訊，請參閱[端點負載平衡健康狀態探查組態 (英文)](https://blogs.msdn.microsoft.com/mast/2016/01/26/endpoint-load-balancing-heath-probe-configuration-details/)。</span><span class="sxs-lookup"><span data-stu-id="82261-151">For more information about health probe configuration, see [Endpoint Load Balancing health probe configuration](https://blogs.msdn.microsoft.com/mast/2016/01/26/endpoint-load-balancing-heath-probe-configuration-details/).</span></span>

## <a name="symptom-vms-behind-load-balancer-are-not-responding-tootraffic-on-hello-configured-data-port"></a><span data-ttu-id="82261-152">徵兆： 負載平衡器後方的 Vm 都沒有回應 hello 設定資料連接埠上 tootraffic</span><span class="sxs-lookup"><span data-stu-id="82261-152">Symptom: VMs behind Load Balancer are not responding tootraffic on hello configured data port</span></span>

<span data-ttu-id="82261-153">如果後端集區的 VM 會列示為狀況良好並回應 toohello 健全狀況探查，但仍未參與 hello 負載平衡，或沒有回應 toohello 資料流量，它可能是因為下列原因 hello 的 tooany:</span><span class="sxs-lookup"><span data-stu-id="82261-153">If a backend pool VM is listed as healthy and responds toohello health probes, but is still not participating in hello Load Balancing, or is not responding toohello data traffic, it may be due tooany of hello following reasons:</span></span> 
* <span data-ttu-id="82261-154">負載平衡器後端集區的 VM 未 hello 資料連接埠接聽</span><span class="sxs-lookup"><span data-stu-id="82261-154">Load Balancer Backend pool VM is not listening on hello data port</span></span> 
* <span data-ttu-id="82261-155">網路安全性群組封鎖 hello hello 負載平衡器後端集區 VM 上的連接埠</span><span class="sxs-lookup"><span data-stu-id="82261-155">Network security group is blocking hello port on hello Load Balancer backend pool VM</span></span>  
* <span data-ttu-id="82261-156">存取 hello 從負載平衡器 hello 相同的 VM 與 NIC</span><span class="sxs-lookup"><span data-stu-id="82261-156">Accessing hello Load Balancer from hello same VM and NIC</span></span> 
* <span data-ttu-id="82261-157">從 hello 參與負載平衡器後端集區 VM 存取 hello 網際網路負載平衡器 VIP</span><span class="sxs-lookup"><span data-stu-id="82261-157">Accessing hello Internet Load Balancer VIP from hello participating Load Balancer backend pool VM</span></span> 

### <a name="cause-1-load-balancer-backend-pool-vm-is-not-listening-on-hello-data-port"></a><span data-ttu-id="82261-158">原因 1： 負載平衡器後端集區 VM 並未 hello 資料連接埠上接聽</span><span class="sxs-lookup"><span data-stu-id="82261-158">Cause 1: Load Balancer backend pool VM is not listening on hello data port</span></span> 
<span data-ttu-id="82261-159">如果 VM 不會回應 toohello 資料流量，則可能是因為是 hello 目標連接埠上未開啟 hello 參與 VM，或 hello VM 未接聽該通訊埠。</span><span class="sxs-lookup"><span data-stu-id="82261-159">If a VM does not respond toohello data traffic, it may be because either hello target port is not open on hello participating VM, or, hello VM is not listening on that port.</span></span> 

<span data-ttu-id="82261-160">**驗證和解決方式**</span><span class="sxs-lookup"><span data-stu-id="82261-160">**Validation and resolution**</span></span>

1. <span data-ttu-id="82261-161">登入 toohello 後端 VM。</span><span class="sxs-lookup"><span data-stu-id="82261-161">Log in toohello backend VM.</span></span> 
2. <span data-ttu-id="82261-162">開啟命令提示字元並執行下列命令 toovalidate hello 資料連接埠上接聽應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="82261-162">Open a command prompt and run hello following command toovalidate there is an application listening on hello data port:</span></span>  
            <span data-ttu-id="82261-163">netstat -an</span><span class="sxs-lookup"><span data-stu-id="82261-163">netstat -an</span></span> 
3. <span data-ttu-id="82261-164">如果未列出 hello 連接埠與狀態 「 接聽 」 設定 hello 適當的接聽程式連接埠</span><span class="sxs-lookup"><span data-stu-id="82261-164">If hello port is not listed with State “LISTENING”, configure hello proper listener port</span></span> 
4. <span data-ttu-id="82261-165">如果 hello 連接埠標示為接聽，請檢查 hello 目標應用程式，該通訊埠上的任何可能的問題。</span><span class="sxs-lookup"><span data-stu-id="82261-165">If hello port is marked as Listening, then check hello target application on that port for any possible issues.</span></span> 

### <a name="cause-2-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vm"></a><span data-ttu-id="82261-166">原因 2： 網路安全性群組封鎖 hello hello 負載平衡器後端集區 VM 上的連接埠</span><span class="sxs-lookup"><span data-stu-id="82261-166">Cause 2: Network security group is blocking hello port on hello Load Balancer backend pool VM</span></span>  

<span data-ttu-id="82261-167">如果一或多個網路或 hello VM hello 子網路上設定的安全性群組，封鎖 hello 來源 IP 或連接埠，則 hello VM 無法 toorespond。</span><span class="sxs-lookup"><span data-stu-id="82261-167">If one or more network security groups configured on hello subnet or on hello VM, is blocking hello source IP or port, then hello VM is unable toorespond.</span></span>

* <span data-ttu-id="82261-168">列出 hello 網路安全性群組 hello 後端 VM 上設定。</span><span class="sxs-lookup"><span data-stu-id="82261-168">List hello network security groups configured on hello backend VM.</span></span> <span data-ttu-id="82261-169">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="82261-169">For more information, see:</span></span>
    -  [<span data-ttu-id="82261-170">管理使用 hello 入口網站的網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="82261-170">Manage network security groups using hello Portal</span></span>](../virtual-network/virtual-network-manage-nsg-arm-portal.md)
    -  [<span data-ttu-id="82261-171">使用 PowerShell 管理網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="82261-171">Manage network security groups using PowerShell</span></span>](../virtual-network/virtual-network-manage-nsg-arm-ps.md)
* <span data-ttu-id="82261-172">從網路安全性群組的 hello 清單中，檢查是否：</span><span class="sxs-lookup"><span data-stu-id="82261-172">From hello list of network security groups, check if:</span></span>
    - <span data-ttu-id="82261-173">hello hello 資料連接埠上的傳入或傳出流量具有干擾。</span><span class="sxs-lookup"><span data-stu-id="82261-173">hello incoming or outgoing traffic on hello data port has interference.</span></span> 
    - <span data-ttu-id="82261-174">**Deny All**網路安全性群組規則上 hello hello VM 或 hello 子網路具有較高的優先順序，讓流量負載平衡器探查，以及該 hello 預設規則的 NIC （網路安全性群組必須允許的負載平衡器 IP168.63.129.16 是探查連接埠)</span><span class="sxs-lookup"><span data-stu-id="82261-174">a **Deny All** network security group rule on hello NIC of hello VM or hello subnet that has a higher priority that hello default rule that allows Load Balancer probes and traffic (network security groups must allow Load Balancer IP of 168.63.129.16, that is probe port)</span></span> 
* <span data-ttu-id="82261-175">如果任何 hello 規則會封鎖 hello 流量，移除並重新設定這些規則 tooallow hello 資料流量。</span><span class="sxs-lookup"><span data-stu-id="82261-175">If any of hello rules are blocking hello traffic, remove and reconfigure those rules tooallow hello data traffic.</span></span>  
* <span data-ttu-id="82261-176">測試如果 hello VM 後立即啟動 toorespond toohello 健全狀態探查。</span><span class="sxs-lookup"><span data-stu-id="82261-176">Test if hello VM has now started toorespond toohello health probes.</span></span>

### <a name="cause-3-accessing-hello-load-balancer-from-hello-same-vm-and-network-interface"></a><span data-ttu-id="82261-177">原因 3： 存取從 hello hello 負載平衡器相同的 VM 及網路介面</span><span class="sxs-lookup"><span data-stu-id="82261-177">Cause 3: Accessing hello Load Balancer from hello same VM and Network interface</span></span> 

<span data-ttu-id="82261-178">如果您在 hello 後端的負載平衡器的 VM 中裝載的應用程式正嘗試 tooaccess 裝載於另一個應用程式 hello 相同的後端 VM hello 透過相同的網路介面，是不支援的案例，並將會失敗。</span><span class="sxs-lookup"><span data-stu-id="82261-178">If your application hosted in hello backend VM of a Load Balancer is trying tooaccess another application hosted in hello same backend VM over hello same Network Interface, it is an unsupported scenario and will fail.</span></span> 

<span data-ttu-id="82261-179">**解析**即可解決此問題，透過 hello 下列方法之一：</span><span class="sxs-lookup"><span data-stu-id="82261-179">**Resolution** You can resolve this issue via one of hello following methods:</span></span>
* <span data-ttu-id="82261-180">每個應用程式都設定個別的後端集區 VM。</span><span class="sxs-lookup"><span data-stu-id="82261-180">Configure separate backend pool VMs per application.</span></span> 
* <span data-ttu-id="82261-181">設定雙重 NIC Vm 中的 hello 應用程式，讓每個應用程式使用它自己的網路介面和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="82261-181">Configure hello application in dual NIC VMs so each application was using its own Network interface and IP address.</span></span> 

### <a name="cause-4-accessing-hello-internal-load-balancer-vip-from-hello-participating-load-balancer-backend-pool-vm"></a><span data-ttu-id="82261-182">原因 4： 從 hello 參與負載平衡器後端集區 VM 存取 hello 內部負載平衡器 VIP</span><span class="sxs-lookup"><span data-stu-id="82261-182">Cause 4: Accessing hello Internal Load Balancer VIP from hello participating Load Balancer backend pool VM</span></span>

<span data-ttu-id="82261-183">如果 ILB VIP 設定內部 VNet，而且其中一個 hello 參與者後端 Vm 正嘗試 tooaccess hello 內部負載平衡器 VIP，導致失敗。</span><span class="sxs-lookup"><span data-stu-id="82261-183">If an ILB VIP is configured inside a VNet, and one of hello participant backend VMs is trying tooaccess hello Internal Load Balancer VIP, that results in failure.</span></span> <span data-ttu-id="82261-184">這是不支援的案例。</span><span class="sxs-lookup"><span data-stu-id="82261-184">This is an unsupported scenario.</span></span>
<span data-ttu-id="82261-185">**解析**評估應用程式閘道或其他 proxy （例如，nginx 或 haproxy 等） toosupport 這一類的案例。</span><span class="sxs-lookup"><span data-stu-id="82261-185">**Resolution** Evaluate Application Gateway or other proxies (for example, nginx or haproxy) toosupport that kind of scenario.</span></span> <span data-ttu-id="82261-186">如需應用程式閘道的詳細資訊，請參閱[應用程式閘道的概觀](../application-gateway/application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="82261-186">For more information about Application Gateway, see [Overview of Application Gateway](../application-gateway/application-gateway-introduction.md)</span></span>

## <a name="additional-network-captures"></a><span data-ttu-id="82261-187">其他網路擷取</span><span class="sxs-lookup"><span data-stu-id="82261-187">Additional network captures</span></span>
<span data-ttu-id="82261-188">如果您決定 tooopen 支援案例，收集下列資訊以便快速解決 hello。</span><span class="sxs-lookup"><span data-stu-id="82261-188">If you decide tooopen a support case, collect hello following information for a quicker resolution.</span></span> <span data-ttu-id="82261-189">選擇下列測試單一的後端 VM tooperform hello:</span><span class="sxs-lookup"><span data-stu-id="82261-189">Choose a single backend VM tooperform hello following tests:</span></span>
- <span data-ttu-id="82261-190">使用 Psping 其中一個內 hello VNet tootest hello 探查連接埠回應 hello 後端 Vm (範例： psping 10.0.0.4:3389) 並記錄結果。</span><span class="sxs-lookup"><span data-stu-id="82261-190">Use Psping from one of hello backend VMs within hello VNet tootest hello probe port response (example: psping 10.0.0.4:3389) and record results.</span></span> 
- <span data-ttu-id="82261-191">使用其中一個內 hello VNet tootest hello 探查連接埠回應 hello 後端 Vm TCPing (範例： psping 10.0.0.4:3389) 並記錄結果。</span><span class="sxs-lookup"><span data-stu-id="82261-191">Use TCPing from one of hello backend VMs within hello VNet tootest hello probe port response (example: psping 10.0.0.4:3389) and record results.</span></span>
- <span data-ttu-id="82261-192">如果不收到任何回應時，在這些 ping 測試，hello 後端 VM 上執行的同時 Netsh trace，當您執行 PsPing，然後再停止 hello Netsh trace hello VNet 測試 VM。</span><span class="sxs-lookup"><span data-stu-id="82261-192">If no response is received in these ping tests, run a simultaneous Netsh trace on hello backend VM and hello VNet test VM while you run PsPing then stop hello Netsh trace.</span></span> 
  
## <a name="next-steps"></a><span data-ttu-id="82261-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82261-193">Next steps</span></span>

<span data-ttu-id="82261-194">如果 hello 上述步驟無法解決 hello 問題，請開啟[支援票證](https://azure.microsoft.com/support/options/)。</span><span class="sxs-lookup"><span data-stu-id="82261-194">If hello preceding steps do not resolve hello issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

