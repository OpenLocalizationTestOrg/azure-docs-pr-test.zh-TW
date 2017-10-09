---
title: "aaaTroubleshooting Azure Vm 之間的連線問題 |Microsoft 文件"
description: "了解如何 tooTroubleshoot hello Azure Vm 之間的連線問題。"
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a><span data-ttu-id="5f735-103">為 Azure VM 之間的連線問題疑難排解</span><span class="sxs-lookup"><span data-stu-id="5f735-103">Troubleshooting connectivity problems between Azure VMs</span></span>

<span data-ttu-id="5f735-104">您可能會遇到 Azure Vm 之間的連線問題。</span><span class="sxs-lookup"><span data-stu-id="5f735-104">You might experience connectivity problems between Azure VMs.</span></span> <span data-ttu-id="5f735-105">本文章提供疑難排解步驟 toohelp 解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="5f735-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="5f735-106">徵狀</span><span class="sxs-lookup"><span data-stu-id="5f735-106">Symptom</span></span>

<span data-ttu-id="5f735-107">Azure VM 無法連線 tooanother Azure VM。</span><span class="sxs-lookup"><span data-stu-id="5f735-107">An Azure VM cannot connect tooanother Azure VM.</span></span>

## <a name="troubleshooting-guidance"></a><span data-ttu-id="5f735-108">疑難排解指引</span><span class="sxs-lookup"><span data-stu-id="5f735-108">Troubleshooting guidance</span></span> 

1. [<span data-ttu-id="5f735-109">檢查是否 NIC 設定不正確</span><span class="sxs-lookup"><span data-stu-id="5f735-109">Check if NIC is misconfigured</span></span>](#step-1-check-if-nic-is-misconfigured)
2. [<span data-ttu-id="5f735-110">檢查是否封鎖的 NSG 或 UDR 網路流量</span><span class="sxs-lookup"><span data-stu-id="5f735-110">Check if network traffic is blocked by NSG or UDR</span></span>](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [<span data-ttu-id="5f735-111">檢查是否 VM 防火牆封鎖網路流量</span><span class="sxs-lookup"><span data-stu-id="5f735-111">Check if network traffic is blocked by VM firewall</span></span>](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [<span data-ttu-id="5f735-112">請檢查 VM 應用程式或服務是否正在接聽 hello 連接埠</span><span class="sxs-lookup"><span data-stu-id="5f735-112">Check whether VM app or service is listening on hello port</span></span>](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [<span data-ttu-id="5f735-113">檢查 hello 問題是否因 SNAT</span><span class="sxs-lookup"><span data-stu-id="5f735-113">Check whether hello problem is caused by SNAT</span></span>](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [<span data-ttu-id="5f735-114">檢查是否封鎖流量的 Acl hello 傳統 VM</span><span class="sxs-lookup"><span data-stu-id="5f735-114">Check whether traffic is blocked by ACLs for hello classic VM</span></span>](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [<span data-ttu-id="5f735-115">檢查是否對建立 hello 端點 hello 傳統 VM</span><span class="sxs-lookup"><span data-stu-id="5f735-115">Check whether hello endpoint is created for hello classic VM</span></span>](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [<span data-ttu-id="5f735-116">無法 tooconnect tooa VM 網路共用</span><span class="sxs-lookup"><span data-stu-id="5f735-116">Unable tooconnect tooa VM network share</span></span>](#step-8-unable-to-connect-to-a-vm-network-share)
9. [<span data-ttu-id="5f735-117">內部 Vnet 連線</span><span class="sxs-lookup"><span data-stu-id="5f735-117">Inter-Vnet connectivity</span></span>](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a><span data-ttu-id="5f735-118">疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="5f735-118">Troubleshooting steps</span></span>

<span data-ttu-id="5f735-119">請遵循這些步驟 tootroubleshoot hello 問題。</span><span class="sxs-lookup"><span data-stu-id="5f735-119">Follow these steps tootroubleshoot hello problem.</span></span> <span data-ttu-id="5f735-120">檢查 hello 問題是否解決每個步驟之後。</span><span class="sxs-lookup"><span data-stu-id="5f735-120">Check whether hello problem is resolved after each step.</span></span> 

### <a name="step-1-check-if-nic-is-misconfigured"></a><span data-ttu-id="5f735-121">步驟 1： 檢查 NIC 設定不正確</span><span class="sxs-lookup"><span data-stu-id="5f735-121">Step 1: Check if NIC is misconfigured</span></span>

<span data-ttu-id="5f735-122">請遵循[如何 tooreset Azure Windows VM 的網路介面](../virtual-machines/windows/reset-network-interface.md)。</span><span class="sxs-lookup"><span data-stu-id="5f735-122">Follow [How tooreset network interface for Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span></span> 

<span data-ttu-id="5f735-123">如果您修改 hello 網路介面 (NIC) 之後，就會發生 hello 問題，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5f735-123">If hello problem occurs after you modify hello network interface (NIC), follow these steps:</span></span>

<span data-ttu-id="5f735-124">**運算 NIC Vm**</span><span class="sxs-lookup"><span data-stu-id="5f735-124">**Mulit-NIC VMs**</span></span>

1. <span data-ttu-id="5f735-125">新增 NIC。</span><span class="sxs-lookup"><span data-stu-id="5f735-125">Add a NIC.</span></span>
2. <span data-ttu-id="5f735-126">修正 hello 錯誤 NIC] 或 [移除錯誤 NIC 的 hello 問題</span><span class="sxs-lookup"><span data-stu-id="5f735-126">Fix hello problems in hello bad NIC or remove bad NIC.</span></span>  <span data-ttu-id="5f735-127">然後出 hello nic。</span><span class="sxs-lookup"><span data-stu-id="5f735-127">Then readd hello NIC.</span></span>

<span data-ttu-id="5f735-128">如需詳細資訊，請參閱[新增網路介面 tooor 移除虛擬機器](virtual-network-network-interface-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="5f735-128">For more information, see [Add network interfaces tooor remove from virtual machines](virtual-network-network-interface-vm.md).</span></span>

<span data-ttu-id="5f735-129">**單一 NIC VM**</span><span class="sxs-lookup"><span data-stu-id="5f735-129">**Single-NIC VM**</span></span> 

- [<span data-ttu-id="5f735-130">重新部署 Windows VM</span><span class="sxs-lookup"><span data-stu-id="5f735-130">Redeploy Windows VM</span></span>](../virtual-machines/windows/redeploy-to-new-node.md)
- [<span data-ttu-id="5f735-131">重新部署 Linux VM</span><span class="sxs-lookup"><span data-stu-id="5f735-131">Redeploy Linux VM</span></span>](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a><span data-ttu-id="5f735-132">步驟 2： 檢查是否封鎖的 NSG 或 UDR 網路流量</span><span class="sxs-lookup"><span data-stu-id="5f735-132">Step 2: Check if network traffic is blocked by NSG or UDR</span></span>

<span data-ttu-id="5f735-133">利用[網路監看員 IP 流量確認](../network-watcher/network-watcher-ip-flow-verify-overview.md)和[NSG 流程記錄](../network-watcher/network-watcher-nsg-flow-logging-overview.md)tooidentify 如果沒有網路安全性群組或使用者定義路由之影響的流量。</span><span class="sxs-lookup"><span data-stu-id="5f735-133">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span>

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a><span data-ttu-id="5f735-134">步驟 3： 檢查是否 VM 防火牆封鎖網路流量</span><span class="sxs-lookup"><span data-stu-id="5f735-134">Step 3: Check if network traffic is blocked by VM firewall</span></span>

<span data-ttu-id="5f735-135">停用 hello 防火牆，然後再測試 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="5f735-135">Disable hello firewall, and then test hello result.</span></span> <span data-ttu-id="5f735-136">如果 hello 問題已解決，驗證 hello 防火牆中的 hello 設定，然後重新啟用。</span><span class="sxs-lookup"><span data-stu-id="5f735-136">If hello problem is resolved, validate hello settings in hello firewall and re-enable.</span></span>

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a><span data-ttu-id="5f735-137">步驟 4： 檢查 VM 應用程式或服務是否正在接聽 hello 連接埠</span><span class="sxs-lookup"><span data-stu-id="5f735-137">Step 4: Check whether VM app or service is listening on hello port</span></span>

<span data-ttu-id="5f735-138">您可以使用其中一個 VM 應用程式或服務正在接聽 hello 連接埠是否遵循方法 toocheck hello</span><span class="sxs-lookup"><span data-stu-id="5f735-138">You can use one of hello following methods toocheck whether VM Application or Service is listening on hello port</span></span>

- <span data-ttu-id="5f735-139">執行下列命令 toocheck 是否 hello 伺服器正在接聽該通訊埠的 hello。</span><span class="sxs-lookup"><span data-stu-id="5f735-139">Run hello following commands toocheck whether hello server is listening on that port.</span></span>

<span data-ttu-id="5f735-140">**Windows VM**</span><span class="sxs-lookup"><span data-stu-id="5f735-140">**Windows VM**</span></span>

    netstat –ano

<span data-ttu-id="5f735-141">**Linux VM**</span><span class="sxs-lookup"><span data-stu-id="5f735-141">**Linux VM**</span></span>

    netstat -l

- <span data-ttu-id="5f735-142">執行 hello **Telnet** hello VM tooitself tootest hello 連接埠上的命令。</span><span class="sxs-lookup"><span data-stu-id="5f735-142">Run hello **Telnet** command on hello VM tooitself tootest hello port.</span></span> <span data-ttu-id="5f735-143">如果 hello 測試失敗，應用程式或服務不是設定的 toolisten hello 連接埠上。</span><span class="sxs-lookup"><span data-stu-id="5f735-143">If hello test fails, application or service is not configured toolisten on hello port.</span></span>

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a><span data-ttu-id="5f735-144">步驟 5： 檢查 hello 問題是否因 SNAT</span><span class="sxs-lookup"><span data-stu-id="5f735-144">Step 5: Check whether hello problem is caused by SNAT</span></span>

<span data-ttu-id="5f735-145">在某些情況下，hello VM 放置後方會相依於 Azure 外部的資源的負載平衡解決方案。</span><span class="sxs-lookup"><span data-stu-id="5f735-145">In some scenarios, hello VM is placed behind a Load balance solution that has a dependency on resources outside of Azure.</span></span> <span data-ttu-id="5f735-146">在這些情況下，如果您遇到間歇性連線問題 hello 問題可能因[SNAT 連接埠耗盡](../load-balancer/load-balancer-outbound-connections.md)。</span><span class="sxs-lookup"><span data-stu-id="5f735-146">In these scenarios, if you experience intermittent connection problems, hello problem may be caused by [SNAT port exhaustion](../load-balancer/load-balancer-outbound-connections.md).</span></span> <span data-ttu-id="5f735-147">tooresolve hello 問題，建立 hello 負載平衡器後方的 VIP （或傳統的 ILPIP） 是針對每個 vm，並且與 NSG 或 ACL。</span><span class="sxs-lookup"><span data-stu-id="5f735-147">tooresolve hello issue, create a VIP (or ILPIP for classic) for each VM that is behind hello Load balancer and secure with NSG or ACL.</span></span> 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a><span data-ttu-id="5f735-148">步驟 6： 檢查是否封鎖流量的 Acl hello 傳統 VM</span><span class="sxs-lookup"><span data-stu-id="5f735-148">Step 6: Check whether traffic is blocked by ACLs for hello classic VM</span></span>

<span data-ttu-id="5f735-149">ACL 提供 hello 能力 tooselectively 允許或拒絕虛擬機器端點的流量。</span><span class="sxs-lookup"><span data-stu-id="5f735-149">An ACL provides hello ability tooselectively permit or deny traffic for a virtual machine endpoint.</span></span> <span data-ttu-id="5f735-150">如需詳細資訊，請參閱[端點上的管理 hello ACL](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint)。</span><span class="sxs-lookup"><span data-stu-id="5f735-150">For more information, see [Manage hello ACL on an endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a><span data-ttu-id="5f735-151">步驟 7： 檢查是否對建立 hello 端點 hello 傳統 VM</span><span class="sxs-lookup"><span data-stu-id="5f735-151">Step 7: Check whether hello endpoint is created for hello classic VM</span></span>

<span data-ttu-id="5f735-152">您在 Azure 中使用 hello 傳統部署模型中建立的所有 Vm 可以自動透過都通訊與 hello 中其他虛擬機器的私人網路通道相同雲端服務或虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5f735-152">All VMs that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="5f735-153">不過，其他虛擬網路上的電腦需要端點 toodirect hello 輸入的網路流量 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5f735-153">However, computers on other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="5f735-154">如需詳細資訊，請參閱[如何設定端點 tooset](../virtual-machines/windows/classic/setup-endpoints.md)。</span><span class="sxs-lookup"><span data-stu-id="5f735-154">For more information, see [How tooset up endpoints](../virtual-machines/windows/classic/setup-endpoints.md).</span></span>

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a><span data-ttu-id="5f735-155">步驟 8： 無法 tooconnect tooa VM 網路共用</span><span class="sxs-lookup"><span data-stu-id="5f735-155">Step 8: Unable tooconnect tooa VM network share</span></span>

<span data-ttu-id="5f735-156">如果您無法 tooconnect tooa VM 網路共用，hello 問題可能被因 hello VM 中無法使用 Nic。</span><span class="sxs-lookup"><span data-stu-id="5f735-156">If you are unable tooconnect tooa VM network share, hello problem can be caused by unavailable NICs in hello VM.</span></span> <span data-ttu-id="5f735-157">toodelete hello Nic 無法使用，請參閱[toodelete hello 無法使用 Nic 的方式](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span><span class="sxs-lookup"><span data-stu-id="5f735-157">toodelete hello unavailable NICs, see [How toodelete hello unavailable NICs](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span></span>

### <a name="step-9-inter-vnet-connectivity"></a><span data-ttu-id="5f735-158">步驟 9： 間 Vnet 連線</span><span class="sxs-lookup"><span data-stu-id="5f735-158">Step 9: Inter-Vnet connectivity</span></span>

<span data-ttu-id="5f735-159">利用[網路監看員 IP 流量確認](../network-watcher/network-watcher-ip-flow-verify-overview.md)和[NSG 流程記錄](../network-watcher/network-watcher-nsg-flow-logging-overview.md)tooidentify 如果沒有網路安全性群組或使用者定義路由之影響的流量。</span><span class="sxs-lookup"><span data-stu-id="5f735-159">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span> <span data-ttu-id="5f735-160">您也可以驗證您的內部 Vnet 組態[這裡](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections)。</span><span class="sxs-lookup"><span data-stu-id="5f735-160">You can also validate your Inter-Vnet configuration [here](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span></span>

### <a name="need-help-contact-support"></a><span data-ttu-id="5f735-161">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="5f735-161">Need help?</span></span> <span data-ttu-id="5f735-162">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="5f735-162">Contact support.</span></span>
<span data-ttu-id="5f735-163">如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="5f735-163">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
