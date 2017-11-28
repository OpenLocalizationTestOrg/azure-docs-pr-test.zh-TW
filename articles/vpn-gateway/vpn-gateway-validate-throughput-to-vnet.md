---
title: "驗證 Microsoft Azure 虛擬網路的 VPN 輸送量 tooa |Microsoft 文件"
description: "hello 本文件的目的是 toohelp 使用者驗證 hello 從其內部部署資源 tooan Azure 虛擬機器的網路輸送量。"
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
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a><span data-ttu-id="9d087-103">如何 toovalidate VPN 輸送量 tooa 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="9d087-103">How toovalidate VPN throughput tooa virtual network</span></span>

<span data-ttu-id="9d087-104">VPN 閘道連線可讓您在 Azure 虛擬網路與您內部部署之間 tooestablish 安全跨單位連線 IT 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="9d087-104">A VPN gateway connection enables you tooestablish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="9d087-105">本文示範如何將網路輸送量 toovalidate hello 從內部部署資源 tooan Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9d087-105">This article shows how toovalidate network throughput from hello on-premises resources tooan Azure virtual machine.</span></span> <span data-ttu-id="9d087-106">本文章也提供疑難排解指引。</span><span class="sxs-lookup"><span data-stu-id="9d087-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="9d087-107">本文旨在 toohelp 診斷和修正常見的問題。</span><span class="sxs-lookup"><span data-stu-id="9d087-107">This article is intended toohelp diagnose and fix common issues.</span></span> <span data-ttu-id="9d087-108">如果您使用下列資訊，hello 無法 toosolve hello 問題[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。</span><span class="sxs-lookup"><span data-stu-id="9d087-108">If you're unable toosolve hello issue by using hello following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="9d087-109">概觀</span><span class="sxs-lookup"><span data-stu-id="9d087-109">Overview</span></span>

<span data-ttu-id="9d087-110">hello VPN 閘道連線包含下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="9d087-110">hello VPN gateway connection involves hello following components:</span></span>

- <span data-ttu-id="9d087-111">內部部署 VPN 裝置 (檢視[已經驗證的 VPN 裝置列表)](vpn-gateway-about-vpn-devices.md#devicetable)。</span><span class="sxs-lookup"><span data-stu-id="9d087-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="9d087-112">公用網際網路</span><span class="sxs-lookup"><span data-stu-id="9d087-112">Public Internet</span></span>
- <span data-ttu-id="9d087-113">Azure VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="9d087-113">Azure VPN gateway</span></span>
- <span data-ttu-id="9d087-114">Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="9d087-114">Azure virtual machine</span></span>

<span data-ttu-id="9d087-115">hello 下列圖表顯示 hello 邏輯在內部部署網路 tooan Azure 的虛擬網路透過 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="9d087-115">hello following diagram shows hello logical connectivity of an on-premises network tooan Azure virtual network through VPN.</span></span>

![邏輯客戶網路連線 tooMSFT 網路使用 VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a><span data-ttu-id="9d087-117">計算 hello 最大預期的輸入/輸出</span><span class="sxs-lookup"><span data-stu-id="9d087-117">Calculate hello maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="9d087-118">判斷您應用程式的基準輸送量需求。</span><span class="sxs-lookup"><span data-stu-id="9d087-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="9d087-119">判斷您的 Azure VPN 閘道輸送量限制。</span><span class="sxs-lookup"><span data-stu-id="9d087-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="9d087-120">如需說明，請參閱 hello 「 彙總輸送量 SKU 和 VPN 類型 」 一節[規劃和設計 VPN 閘道](vpn-gateway-plan-design.md)。</span><span class="sxs-lookup"><span data-stu-id="9d087-120">For help, see hello "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="9d087-121">判斷 hello [Azure VM 輸送量指引](../virtual-machines/virtual-machines-windows-sizes.md)VM 大小。</span><span class="sxs-lookup"><span data-stu-id="9d087-121">Determine hello [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="9d087-122">決定您網際網路服務提供者 (ISP) 的頻寬。</span><span class="sxs-lookup"><span data-stu-id="9d087-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="9d087-123">計算您預期的輸送量 - 最小頻寬的 (VM、閘道、ISP) * 0.8。</span><span class="sxs-lookup"><span data-stu-id="9d087-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) * 0.8.</span></span>

<span data-ttu-id="9d087-124">如果您導出的輸送量不符合您的應用程式基本輸送量需求，您需要識別為 hello 瓶頸的 hello 資源 tooincrease hello 頻寬。</span><span class="sxs-lookup"><span data-stu-id="9d087-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need tooincrease hello bandwidth of hello resource that you identified as hello bottleneck.</span></span> <span data-ttu-id="9d087-125">tooresize Azure VPN 閘道，請參閱[變更閘道 SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku)。</span><span class="sxs-lookup"><span data-stu-id="9d087-125">tooresize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="9d087-126">tooresize 虛擬機器，請參閱[VM 調整](../virtual-machines/virtual-machines-windows-resize-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="9d087-126">tooresize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="9d087-127">如果您遇到未預期的網際網路頻寬，您可能也想 toocontact ISP。</span><span class="sxs-lookup"><span data-stu-id="9d087-127">If you are not experiencing expected Internet bandwidth, you may also want toocontact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="9d087-128">使用效能工具驗證網路輸送量</span><span class="sxs-lookup"><span data-stu-id="9d087-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="9d087-129">由於測試時的 VPN 通道輸送量飽和情況無法呈現準確的結果，因此應在非尖峰時段執行此驗證。</span><span class="sxs-lookup"><span data-stu-id="9d087-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="9d087-130">我們會使用這項測試的 hello 工具是 iPerf，這適用於 Windows 和 Linux 上且擁有用戶端和伺服器模式。</span><span class="sxs-lookup"><span data-stu-id="9d087-130">hello tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="9d087-131">它是針對 Windows Vm 有限的 too3 Gbps。</span><span class="sxs-lookup"><span data-stu-id="9d087-131">It is limited too3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="9d087-132">此工具不會執行任何的讀取/寫入作業 toodisk。</span><span class="sxs-lookup"><span data-stu-id="9d087-132">This tool does not perform any read/write operations toodisk.</span></span> <span data-ttu-id="9d087-133">它只會產生自我產生一個結束 toohello 其他 TCP 流量。</span><span class="sxs-lookup"><span data-stu-id="9d087-133">It solely produces self-generated TCP traffic from one end toohello other.</span></span> <span data-ttu-id="9d087-134">它會產生基礎測量用戶端和伺服器節點之間的可用的 hello 頻寬的試驗的統計資料。</span><span class="sxs-lookup"><span data-stu-id="9d087-134">It generated statistics based on experimentation that measures hello bandwidth available between client and server nodes.</span></span> <span data-ttu-id="9d087-135">當測試兩個節點之間，其中一個作為 hello 伺服器以及其他做為用戶端 hello。</span><span class="sxs-lookup"><span data-stu-id="9d087-135">When testing between two nodes, one acts as hello server and hello other as a client.</span></span> <span data-ttu-id="9d087-136">完成這項測試之後，我們建議您反轉 hello 角色 tootest 同時上傳和下載兩個節點上的輸送量。</span><span class="sxs-lookup"><span data-stu-id="9d087-136">Once this test is completed, we recommend that you reverse hello roles tootest both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="9d087-137">下載 iPerf</span><span class="sxs-lookup"><span data-stu-id="9d087-137">Download iPerf</span></span>
<span data-ttu-id="9d087-138">下載 [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip)。</span><span class="sxs-lookup"><span data-stu-id="9d087-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="9d087-139">如需詳細資訊，請參閱 [iPerf 文件](https://iperf.fr/iperf-doc.php)。</span><span class="sxs-lookup"><span data-stu-id="9d087-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="9d087-140">Microsoft 的獨立公司所製造這篇文章討論的 hello 協力廠商產品。</span><span class="sxs-lookup"><span data-stu-id="9d087-140">hello third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="9d087-141">Microsoft 對於不提供任何瑕疵擔保默示或其他關於這些產品的 hello 效能或可靠性。</span><span class="sxs-lookup"><span data-stu-id="9d087-141">Microsoft makes no warranty, implied or otherwise, about hello performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="9d087-142">執行 iPerf (iperf3.exe)</span><span class="sxs-lookup"><span data-stu-id="9d087-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="9d087-143">啟用 NSG/ACL 規則，允許 hello 流量 （適用於測試 Azure VM 上的公用 IP 位址）。</span><span class="sxs-lookup"><span data-stu-id="9d087-143">Enable an NSG/ACL rule allowing hello traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="9d087-144">在這兩個節點上，啟用連接埠 5001 的防火牆例外狀況。</span><span class="sxs-lookup"><span data-stu-id="9d087-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="9d087-145">**Windows:**執行 hello 下列命令以系統管理員：</span><span class="sxs-lookup"><span data-stu-id="9d087-145">**Windows:** Run hello following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="9d087-146">tooremove hello 規則測試時已完成，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="9d087-146">tooremove hello rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="9d087-147">**Azure Linux：**Azure Linux 映像有寬鬆的防火牆。</span><span class="sxs-lookup"><span data-stu-id="9d087-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="9d087-148">如果沒有接聽的通訊埠的應用程式，hello 允許流量。</span><span class="sxs-lookup"><span data-stu-id="9d087-148">If there is an application listening on a port, hello traffic is allowed through.</span></span> <span data-ttu-id="9d087-149">受保護的自訂映像可能需要明確開啟連接埠。</span><span class="sxs-lookup"><span data-stu-id="9d087-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="9d087-150">常見的 Linux OS 層防火牆包括 `iptables`、`ufw` 或 `firewalld`。</span><span class="sxs-lookup"><span data-stu-id="9d087-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="9d087-151">Hello 伺服器節點上，變更 toohello 目錄 iperf3.exe 解壓縮的位置。</span><span class="sxs-lookup"><span data-stu-id="9d087-151">On hello server node, change toohello directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="9d087-152">然後在伺服器模式下執行 iPerf 然後將它設定 toolisten 連接埠 5001 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="9d087-152">Then run iPerf in server mode and set it toolisten on port 5001 as hello following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="9d087-153">Hello 用戶端在節點上，變更 toohello 目錄 iperf 工具會擷取並接著執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="9d087-153">On hello client node, change toohello directory where iperf tool is extracted and then run hello following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="9d087-154">hello 用戶端 30 秒查 5001 toohello 伺服器連接埠上的流量。</span><span class="sxs-lookup"><span data-stu-id="9d087-154">hello client is inducing traffic on port 5001 toohello server for 30 seconds.</span></span> <span data-ttu-id="9d087-155">hello 旗標 '-P '，表示我們使用 32 的同時連線 toohello 伺服器節點。</span><span class="sxs-lookup"><span data-stu-id="9d087-155">hello flag '-P ' that indicates we are using 32 simultaneous connections toohello server node.</span></span>

    <span data-ttu-id="9d087-156">hello 下列畫面顯示 hello 這個範例輸出：</span><span class="sxs-lookup"><span data-stu-id="9d087-156">hello following screen shows hello output from this example:</span></span>

    ![輸出](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="9d087-158">（選擇性） toopreserve hello 測試結果，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="9d087-158">(OPTIONAL) toopreserve hello testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="9d087-159">完成 hello 上一個步驟之後，執行相同的步驟與 hello 角色反轉，hello，因此 hello 伺服器節點現在會 hello 用戶端，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="9d087-159">After completing hello previous steps, execute hello same steps with hello roles reversed, so that hello server node will now be hello client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="9d087-160">處理檔案複製變慢的問題</span><span class="sxs-lookup"><span data-stu-id="9d087-160">Address slow file copy issues</span></span>
<span data-ttu-id="9d087-161">使用 Windows 檔案總管或透過 RDP 工作階段拖放時，您可能會遇到檔案複製變慢的問題。</span><span class="sxs-lookup"><span data-stu-id="9d087-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="9d087-162">此問題通常是因為 tooone 或兩個 hello 下列因素：</span><span class="sxs-lookup"><span data-stu-id="9d087-162">This problem is normally due tooone or both of hello following factors:</span></span>

- <span data-ttu-id="9d087-163">如 Windows 檔案總管與 RDP 的檔案應用程式，並未在複製檔案時使用多執行緒。</span><span class="sxs-lookup"><span data-stu-id="9d087-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="9d087-164">以提升效能、 使用多執行緒的檔案複製應用程式如[Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy 檔案使用 16 或 32 的執行緒。</span><span class="sxs-lookup"><span data-stu-id="9d087-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy files by using 16 or 32 threads.</span></span> <span data-ttu-id="9d087-165">按一下 檔案中的複本 Richcopy，toochange hello 執行緒編號**動作** > **複製選項** > **檔案複製**。</span><span class="sxs-lookup"><span data-stu-id="9d087-165">toochange hello thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br><span data-ttu-id="9d087-166">
![檔案複製變慢的問題](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span><span class="sxs-lookup"><span data-stu-id="9d087-166">
![Slow file copy issues](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span></span><br>
- <span data-ttu-id="9d087-167">VM 磁碟讀取/寫入速度不足。</span><span class="sxs-lookup"><span data-stu-id="9d087-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="9d087-168">如需詳細資訊，請參閱 [Azure 儲存體疑難排解](../storage/common/storage-e2e-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="9d087-168">For more information, see [Azure Storage Troubleshooting](../storage/common/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="9d087-169">內部部署裝置的外部對應介面</span><span class="sxs-lookup"><span data-stu-id="9d087-169">On-premises device external facing interface</span></span>
<span data-ttu-id="9d087-170">如果 hello 內部部署 VPN 裝置的面向網際網路 IP 位址會包含在 hello[區域網路](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway)在 Azure 中的定義，您可能會遇到無法 toobring hello VPN，偶爾中斷連線或效能問題。</span><span class="sxs-lookup"><span data-stu-id="9d087-170">If hello on-premises VPN device Internet-facing IP address is included in hello [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability toobring up hello VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="9d087-171">檢查延遲</span><span class="sxs-lookup"><span data-stu-id="9d087-171">Checking latency</span></span>
<span data-ttu-id="9d087-172">如果有任何延遲超過 100 毫秒之間的躍點，請使用 tracert tootrace tooMicrosoft Azure 邊緣裝置 toodetermine。</span><span class="sxs-lookup"><span data-stu-id="9d087-172">Use tracert tootrace tooMicrosoft Azure Edge device toodetermine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="9d087-173">Hello 與內部網路，從執行*tracert* toohello VIP hello Azure 閘道的 VM。</span><span class="sxs-lookup"><span data-stu-id="9d087-173">From hello on-premises network, run *tracert* toohello VIP of hello Azure Gateway or VM.</span></span> <span data-ttu-id="9d087-174">一旦您只會看到 * 傳回，您知道您已達到 hello Azure 邊緣。</span><span class="sxs-lookup"><span data-stu-id="9d087-174">Once you see only * returned, you know you have reached hello Azure edge.</span></span> <span data-ttu-id="9d087-175">當您看到包含 「 MSN"傳回的 DNS 名稱時，您知道您已達到 hello Microsoft 骨幹。</span><span class="sxs-lookup"><span data-stu-id="9d087-175">When you see DNS names that include "MSN" returned, you know you have reached hello Microsoft backbone.</span></span><br><br><span data-ttu-id="9d087-176">
![檢查延遲](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="9d087-176">
![Checking Latency](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d087-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9d087-177">Next steps</span></span>
<span data-ttu-id="9d087-178">詳細的資訊或說明，請參閱下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="9d087-178">For more information or help, check out hello following links:</span></span>

- [<span data-ttu-id="9d087-179">最佳化 Azure 虛擬機器的網路輸送量</span><span class="sxs-lookup"><span data-stu-id="9d087-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="9d087-180">Microsoft 支援服務</span><span class="sxs-lookup"><span data-stu-id="9d087-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
