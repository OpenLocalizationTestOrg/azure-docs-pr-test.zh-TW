---
title: "驗證傳輸到 Microsoft Azure 虛擬網路的 VPN 輸送量 | Microsoft Docs"
description: "本文件的目的是在協助使用者驗證從其內部部署資源到 Azure 虛擬機器的網路輸送量。"
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 2e0347854b5d30c955a50a01d6f7ba08e24f94b6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-validate-vpn-throughput-to-a-virtual-network"></a><span data-ttu-id="d19e6-103">如何驗證傳輸到虛擬網路的 VPN 輸送量</span><span class="sxs-lookup"><span data-stu-id="d19e6-103">How to validate VPN throughput to a virtual network</span></span>

<span data-ttu-id="d19e6-104">VPN 閘道連線可讓您在 Azure 內的虛擬網路和內部部署 IT 基礎結構之間建立安全的跨單位連線。</span><span class="sxs-lookup"><span data-stu-id="d19e6-104">A VPN gateway connection enables you to establish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="d19e6-105">本文章說明如何驗證從內部部署資源到 Azure 虛擬機器的網路輸送量。</span><span class="sxs-lookup"><span data-stu-id="d19e6-105">This article shows how to validate network throughput from the on-premises resources to an Azure virtual machine.</span></span> <span data-ttu-id="d19e6-106">本文章也提供疑難排解指引。</span><span class="sxs-lookup"><span data-stu-id="d19e6-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="d19e6-107">本文章旨在協助診斷和修正常見的問題。</span><span class="sxs-lookup"><span data-stu-id="d19e6-107">This article is intended to help diagnose and fix common issues.</span></span> <span data-ttu-id="d19e6-108">如果您在使用下列資訊後仍無法解決問題，[請連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。</span><span class="sxs-lookup"><span data-stu-id="d19e6-108">If you're unable to solve the issue by using the following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="d19e6-109">概觀</span><span class="sxs-lookup"><span data-stu-id="d19e6-109">Overview</span></span>

<span data-ttu-id="d19e6-110">VPN 閘道連線涉及下列元件：</span><span class="sxs-lookup"><span data-stu-id="d19e6-110">The VPN gateway connection involves the following components:</span></span>

- <span data-ttu-id="d19e6-111">內部部署 VPN 裝置 (檢視[已經驗證的 VPN 裝置列表)](vpn-gateway-about-vpn-devices.md#devicetable)。</span><span class="sxs-lookup"><span data-stu-id="d19e6-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="d19e6-112">公用網際網路</span><span class="sxs-lookup"><span data-stu-id="d19e6-112">Public Internet</span></span>
- <span data-ttu-id="d19e6-113">Azure VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="d19e6-113">Azure VPN gateway</span></span>
- <span data-ttu-id="d19e6-114">Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d19e6-114">Azure virtual machine</span></span>

<span data-ttu-id="d19e6-115">下圖顯示內部部署網路透過 VPN 到 Azure 虛擬網路的邏輯連線能力。</span><span class="sxs-lookup"><span data-stu-id="d19e6-115">The following diagram shows the logical connectivity of an on-premises network to an Azure virtual network through VPN.</span></span>

![客戶網路使用 VPN 到 MSFT 網路的邏輯連線能力](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-the-maximum-expected-ingressegress"></a><span data-ttu-id="d19e6-117">計算最大預期輸入/輸出</span><span class="sxs-lookup"><span data-stu-id="d19e6-117">Calculate the maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="d19e6-118">判斷您應用程式的基準輸送量需求。</span><span class="sxs-lookup"><span data-stu-id="d19e6-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="d19e6-119">判斷您的 Azure VPN 閘道輸送量限制。</span><span class="sxs-lookup"><span data-stu-id="d19e6-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="d19e6-120">如需說明，請參閱 [規劃與設計 VPN 閘道](vpn-gateway-plan-design.md) 的「依 SKU 和 VPN 類型彙總輸送量」區段。</span><span class="sxs-lookup"><span data-stu-id="d19e6-120">For help, see the "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="d19e6-121">判斷 VM 大小的 [Azure VM 輸送量指引](../virtual-machines/virtual-machines-windows-sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="d19e6-121">Determine the [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="d19e6-122">決定您網際網路服務提供者 (ISP) 的頻寬。</span><span class="sxs-lookup"><span data-stu-id="d19e6-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="d19e6-123">計算您預期的輸送量 - 最小頻寬的 (VM、閘道、ISP) * 0.8。</span><span class="sxs-lookup"><span data-stu-id="d19e6-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) * 0.8.</span></span>

<span data-ttu-id="d19e6-124">如果您算出的輸送量不符合您應用程式的基準輸送量需求，您需要增加您發現已成為瓶頸的資源頻寬。</span><span class="sxs-lookup"><span data-stu-id="d19e6-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need to increase the bandwidth of the resource that you identified as the bottleneck.</span></span> <span data-ttu-id="d19e6-125">如果要調整 Azure VPN 閘道的大小，請參閱 [變更閘道 SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku)。</span><span class="sxs-lookup"><span data-stu-id="d19e6-125">To resize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="d19e6-126">如果調整虛擬機器的大小，請參閱 [調整 VM 的大小](../virtual-machines/virtual-machines-windows-resize-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="d19e6-126">To resize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="d19e6-127">如果您未能享有預期的網際網路頻寬，您可能也需要連絡您的 ISP。</span><span class="sxs-lookup"><span data-stu-id="d19e6-127">If you are not experiencing expected Internet bandwidth, you may also want to contact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="d19e6-128">使用效能工具驗證網路輸送量</span><span class="sxs-lookup"><span data-stu-id="d19e6-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="d19e6-129">由於測試時的 VPN 通道輸送量飽和情況無法呈現準確的結果，因此應在非尖峰時段執行此驗證。</span><span class="sxs-lookup"><span data-stu-id="d19e6-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="d19e6-130">iPerf 是我們用於此測試的工作，分別在 Windows 與 Linux 上工作，並具有用戶端與伺服器模式。</span><span class="sxs-lookup"><span data-stu-id="d19e6-130">The tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="d19e6-131">Windows VM 限制在 3 Gbps。</span><span class="sxs-lookup"><span data-stu-id="d19e6-131">It is limited to 3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="d19e6-132">此工具不會對磁碟執行任何讀取/寫入作業。</span><span class="sxs-lookup"><span data-stu-id="d19e6-132">This tool does not perform any read/write operations to disk.</span></span> <span data-ttu-id="d19e6-133">此工具只會產生從一端到另一端自我產生的 TCP 流量。</span><span class="sxs-lookup"><span data-stu-id="d19e6-133">It solely produces self-generated TCP traffic from one end to the other.</span></span> <span data-ttu-id="d19e6-134">此工具然後根據測量用戶端與伺服器節點之間的可用頻寬實驗，產生統計資料。</span><span class="sxs-lookup"><span data-stu-id="d19e6-134">It generated statistics based on experimentation that measures the bandwidth available between client and server nodes.</span></span> <span data-ttu-id="d19e6-135">在兩個節點之間測試時，一個節點作為伺服器，另一個節點作為用戶端。</span><span class="sxs-lookup"><span data-stu-id="d19e6-135">When testing between two nodes, one acts as the server and the other as a client.</span></span> <span data-ttu-id="d19e6-136">一旦完成此項測試後，我們建議您對調角色，以測試雙方節點的上傳和下載輸送量。</span><span class="sxs-lookup"><span data-stu-id="d19e6-136">Once this test is completed, we recommend that you reverse the roles to test both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="d19e6-137">下載 iPerf</span><span class="sxs-lookup"><span data-stu-id="d19e6-137">Download iPerf</span></span>
<span data-ttu-id="d19e6-138">下載 [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip)。</span><span class="sxs-lookup"><span data-stu-id="d19e6-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="d19e6-139">如需詳細資訊，請參閱 [iPerf 文件](https://iperf.fr/iperf-doc.php)。</span><span class="sxs-lookup"><span data-stu-id="d19e6-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="d19e6-140">本文章討論的協力廠商產品是由獨立於 Microsoft 的公司製造。</span><span class="sxs-lookup"><span data-stu-id="d19e6-140">The third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="d19e6-141">Microsoft 對於這些產品的效能或可靠性不提供任何默示或其他保證。</span><span class="sxs-lookup"><span data-stu-id="d19e6-141">Microsoft makes no warranty, implied or otherwise, about the performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="d19e6-142">執行 iPerf (iperf3.exe)</span><span class="sxs-lookup"><span data-stu-id="d19e6-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="d19e6-143">啟用允許流量的 NSG/ACL 規則 (適用於 Azure VM 上的公用 IP 位址測試)。</span><span class="sxs-lookup"><span data-stu-id="d19e6-143">Enable an NSG/ACL rule allowing the traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="d19e6-144">在這兩個節點上，啟用連接埠 5001 的防火牆例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d19e6-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="d19e6-145">**Windows：**以系統管理員身分執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="d19e6-145">**Windows:** Run the following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="d19e6-146">如果要在測試完成時移除規則，請執行此命令：</span><span class="sxs-lookup"><span data-stu-id="d19e6-146">To remove the rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="d19e6-147">**Azure Linux：**Azure Linux 映像有寬鬆的防火牆。</span><span class="sxs-lookup"><span data-stu-id="d19e6-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="d19e6-148">如果有應用程式接聽連接埠，則允許通過流量。</span><span class="sxs-lookup"><span data-stu-id="d19e6-148">If there is an application listening on a port, the traffic is allowed through.</span></span> <span data-ttu-id="d19e6-149">受保護的自訂映像可能需要明確開啟連接埠。</span><span class="sxs-lookup"><span data-stu-id="d19e6-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="d19e6-150">常見的 Linux OS 層防火牆包括 `iptables`、`ufw` 或 `firewalld`。</span><span class="sxs-lookup"><span data-stu-id="d19e6-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="d19e6-151">在伺服器節點上，請變更至將 iperf3.exe 解壓縮的目錄。</span><span class="sxs-lookup"><span data-stu-id="d19e6-151">On the server node, change to the directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="d19e6-152">然後在伺服器模式中執行 iPerf，並以下列命令設為接聽連接埠 5001︰</span><span class="sxs-lookup"><span data-stu-id="d19e6-152">Then run iPerf in server mode and set it to listen on port 5001 as the following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="d19e6-153">在用戶端節點上，變更至將 iperf 工具解壓縮的目錄，然後執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="d19e6-153">On the client node, change to the directory where iperf tool is extracted and then run the following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of the iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="d19e6-154">用戶端引起從連接埠 5001 到伺服器的流量 30 秒。</span><span class="sxs-lookup"><span data-stu-id="d19e6-154">The client is inducing traffic on port 5001 to the server for 30 seconds.</span></span> <span data-ttu-id="d19e6-155">旗標「-P」指出我們正使用伺服器節點的 32 條同時連線。</span><span class="sxs-lookup"><span data-stu-id="d19e6-155">The flag '-P ' that indicates we are using 32 simultaneous connections to the server node.</span></span>

    <span data-ttu-id="d19e6-156">下列畫面顯示此範例的輸出：</span><span class="sxs-lookup"><span data-stu-id="d19e6-156">The following screen shows the output from this example:</span></span>

    ![輸出](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="d19e6-158">(選用) 如果要保留測試結果，請執行此命令：</span><span class="sxs-lookup"><span data-stu-id="d19e6-158">(OPTIONAL) To preserve the testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="d19e6-159">完成之前的步驟後，請在對調角色後執行相同的步驟，因此伺服器節點現在將是用戶端，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="d19e6-159">After completing the previous steps, execute the same steps with the roles reversed, so that the server node will now be the client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="d19e6-160">處理檔案複製變慢的問題</span><span class="sxs-lookup"><span data-stu-id="d19e6-160">Address slow file copy issues</span></span>
<span data-ttu-id="d19e6-161">使用 Windows 檔案總管或透過 RDP 工作階段拖放時，您可能會遇到檔案複製變慢的問題。</span><span class="sxs-lookup"><span data-stu-id="d19e6-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="d19e6-162">此問題一般是因為下列一個或多個因素造成︰</span><span class="sxs-lookup"><span data-stu-id="d19e6-162">This problem is normally due to one or both of the following factors:</span></span>

- <span data-ttu-id="d19e6-163">如 Windows 檔案總管與 RDP 的檔案應用程式，並未在複製檔案時使用多執行緒。</span><span class="sxs-lookup"><span data-stu-id="d19e6-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="d19e6-164">為了提升效能，請使用如 [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) 等多執行緒的檔案複製應用程式，以 16 或 32 條執行緒複製檔案。</span><span class="sxs-lookup"><span data-stu-id="d19e6-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) to copy files by using 16 or 32 threads.</span></span> <span data-ttu-id="d19e6-165">如果要在 Richcopy 內變更用於檔案複製的執行緒數量，請按一下 [動作]  >  [複製選項]  >  [檔案複製] 。</span><span class="sxs-lookup"><span data-stu-id="d19e6-165">To change the thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br><span data-ttu-id="d19e6-166">
![檔案複製變慢的問題](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span><span class="sxs-lookup"><span data-stu-id="d19e6-166">
![Slow file copy issues](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span></span><br>
- <span data-ttu-id="d19e6-167">VM 磁碟讀取/寫入速度不足。</span><span class="sxs-lookup"><span data-stu-id="d19e6-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="d19e6-168">如需詳細資訊，請參閱 [Azure 儲存體疑難排解](../storage/common/storage-e2e-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="d19e6-168">For more information, see [Azure Storage Troubleshooting](../storage/common/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="d19e6-169">內部部署裝置的外部對應介面</span><span class="sxs-lookup"><span data-stu-id="d19e6-169">On-premises device external facing interface</span></span>
<span data-ttu-id="d19e6-170">如果內部部署 VPN 裝置連結網際網路的 IP 位址包含在 Azure 中的 [區域網路](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) 定義內，您可能會遇到無法呼叫 VPN、零星中斷連線或效能問題。</span><span class="sxs-lookup"><span data-stu-id="d19e6-170">If the on-premises VPN device Internet-facing IP address is included in the [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability to bring up the VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="d19e6-171">檢查延遲</span><span class="sxs-lookup"><span data-stu-id="d19e6-171">Checking latency</span></span>
<span data-ttu-id="d19e6-172">使用 tracert 追蹤至 Microsoft Azure Edge 裝置，以判斷躍點之間是否有任何超過 100 ms 的延遲。</span><span class="sxs-lookup"><span data-stu-id="d19e6-172">Use tracert to trace to Microsoft Azure Edge device to determine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="d19e6-173">從內部部署網路，執行 *tracert* 以追蹤至 Azure Gateway 或 VM 的 VIP。</span><span class="sxs-lookup"><span data-stu-id="d19e6-173">From the on-premises network, run *tracert* to the VIP of the Azure Gateway or VM.</span></span> <span data-ttu-id="d19e6-174">您只看到 * 傳回後，即表示您已觸達 Azure 邊緣。</span><span class="sxs-lookup"><span data-stu-id="d19e6-174">Once you see only * returned, you know you have reached the Azure edge.</span></span> <span data-ttu-id="d19e6-175">您看到包括「MSN」的 DNS 名稱傳回時，即表示您已觸達 Microsoft 骨幹。</span><span class="sxs-lookup"><span data-stu-id="d19e6-175">When you see DNS names that include "MSN" returned, you know you have reached the Microsoft backbone.</span></span><br><br><span data-ttu-id="d19e6-176">
![檢查延遲](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="d19e6-176">
![Checking Latency](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d19e6-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d19e6-177">Next steps</span></span>
<span data-ttu-id="d19e6-178">如需詳細資訊或協助，請看看下列連結：</span><span class="sxs-lookup"><span data-stu-id="d19e6-178">For more information or help, check out the following links:</span></span>

- [<span data-ttu-id="d19e6-179">最佳化 Azure 虛擬機器的網路輸送量</span><span class="sxs-lookup"><span data-stu-id="d19e6-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="d19e6-180">Microsoft 支援服務</span><span class="sxs-lookup"><span data-stu-id="d19e6-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
