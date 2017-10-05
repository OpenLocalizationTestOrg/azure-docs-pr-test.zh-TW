---
title: "Microsoft Azure 雲端服務之連線能力和網路服務問題的常見問題集 | Microsoft Docs"
description: "本文列出 Microsoft Azure 雲端服務之連線能力和網路服務的相關常見問題集。"
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 55d5b692930e273af29c3de9d2b96b6d012b3415
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="connectivity-and-networking-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a><span data-ttu-id="16ea7-103">Azure 雲端服務之連線能力和網路服務問題：常見問題集 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="16ea7-103">Connectivity and networking issues for Azure Cloud Services: Frequently asked questions (FAQs)</span></span>

<span data-ttu-id="16ea7-104">本文包含 [Microsoft Azure 雲端服務](https://azure.microsoft.com/services/cloud-services)之連線能力和網路服務問題的相關常見問題集。</span><span class="sxs-lookup"><span data-stu-id="16ea7-104">This article includes frequently asked questions about connectivity and networking issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span></span> <span data-ttu-id="16ea7-105">您也可以參閱 [雲端服務 VM 大小頁面](cloud-services-sizes-specs.md) 以取得大小資訊。</span><span class="sxs-lookup"><span data-stu-id="16ea7-105">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="16ea7-106">無法在多 VIP 的雲端服務中保留 IP</span><span class="sxs-lookup"><span data-stu-id="16ea7-106">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="16ea7-107">首先，請確定您想要保留其 IP 的虛擬機器執行個體已開啟。</span><span class="sxs-lookup"><span data-stu-id="16ea7-107">First, make sure that the virtual machine instance that you're trying to reserve the IP for is turned on.</span></span> <span data-ttu-id="16ea7-108">其次，請確定您會將保留的 IP 同時用於預備與生產部署。</span><span class="sxs-lookup"><span data-stu-id="16ea7-108">Second, make sure that you're using Reserved IPs for both the staging and production deployments.</span></span> <span data-ttu-id="16ea7-109">**勿** 於部署正在升級時變更設定。</span><span class="sxs-lookup"><span data-stu-id="16ea7-109">**Do not** change the settings while the deployment is upgrading.</span></span>

## <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="16ea7-110">當我有 NSG 時，應如何設定遠端桌面？</span><span class="sxs-lookup"><span data-stu-id="16ea7-110">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="16ea7-111">將規則加入到 NSG，以允許連接埠 **3389** 和 **20000** 上的流量。</span><span class="sxs-lookup"><span data-stu-id="16ea7-111">Add rules to the NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="16ea7-112">遠端桌面使用者連接埠 **3389**。</span><span class="sxs-lookup"><span data-stu-id="16ea7-112">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="16ea7-113">系統已為雲端服務執行個體進行負載平衡，因此您無法直接控制要連線的執行個體。</span><span class="sxs-lookup"><span data-stu-id="16ea7-113">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="16ea7-114">*RemoteForwarder* 與 *RemoteAccess* 代理程式會管理 RDP 流量，並允許用戶端傳送 RDP Cookie 並指定要連線的個別執行個體。</span><span class="sxs-lookup"><span data-stu-id="16ea7-114">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="16ea7-115">RemoteForwarder 與 RemoteAccess 代理程式要求您必須開啟連接埠 20000，這在您使用 NSG 的情況下可能是封鎖的。</span><span class="sxs-lookup"><span data-stu-id="16ea7-115">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="can-i-ping-a-cloud-service"></a><span data-ttu-id="16ea7-116">是否可偵測雲端服務？</span><span class="sxs-lookup"><span data-stu-id="16ea7-116">Can I ping a cloud service?</span></span>

<span data-ttu-id="16ea7-117">否，不能使用一般的 "ping"/ICMP 通訊協定來進行。</span><span class="sxs-lookup"><span data-stu-id="16ea7-117">No, not by using the normal "ping"/ICMP protocol.</span></span> <span data-ttu-id="16ea7-118">不允許透過 Azure Load Balancer 進行 ICMP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="16ea7-118">The ICMP protocol is not permitted through the Azure load balancer.</span></span>

<span data-ttu-id="16ea7-119">若要測試連線能力，建議您進行連接埠偵測。</span><span class="sxs-lookup"><span data-stu-id="16ea7-119">To test connectivity, we recommend that you do a port ping.</span></span> <span data-ttu-id="16ea7-120">當 Ping.exe 使用 ICMP 時，諸如 PSPing、Nmap 及 telnet 等其他工具可讓您測試對特定 TCP 通訊埠的連線。</span><span class="sxs-lookup"><span data-stu-id="16ea7-120">While Ping.exe uses ICMP, other tools, such as PSPing, Nmap, and telnet allow you to test connectivity to a specific TCP port.</span></span>

<span data-ttu-id="16ea7-121">如需詳細資訊，請參閱[使用連接埠偵測而非 ICMP 來測試 Azure VM 連線能力](https://blogs.msdn.microsoft.com/mast/2014/06/22/use-port-pings-instead-of-icmp-to-test-azure-vm-connectivity/)。</span><span class="sxs-lookup"><span data-stu-id="16ea7-121">For more information, see [Use port pings instead of ICMP to test Azure VM connectivity](https://blogs.msdn.microsoft.com/mast/2014/06/22/use-port-pings-instead-of-icmp-to-test-azure-vm-connectivity/).</span></span>

## <a name="how-do-i-prevent-receiving-thousands-of-hits-from-unknown-ip-addresses-that-indicate-some-sort-of-malicious-attack-to-the-cloud-service"></a><span data-ttu-id="16ea7-122">如何避免接收來自未知 IP 位址的成千上萬個叫用，表示對雲端服務的某一種惡意攻擊？</span><span class="sxs-lookup"><span data-stu-id="16ea7-122">How do I prevent receiving thousands of hits from unknown IP addresses that indicate some sort of malicious attack to the cloud service?</span></span>
<span data-ttu-id="16ea7-123">Azure 會實作多層的網路安全性，可保護其平台服務免於遭受分散式阻斷服務 (DDoS) 攻擊。</span><span class="sxs-lookup"><span data-stu-id="16ea7-123">Azure implements a multilayer network security to protect its platform services against distributed denial-of-service (DDoS) attacks.</span></span> <span data-ttu-id="16ea7-124">Azure DDoS 防禦系統是屬於 Azure 的連續監視流程，會透過滲透測試持續進行改良。</span><span class="sxs-lookup"><span data-stu-id="16ea7-124">The Azure DDoS defense system is part of Azure’s continuous monitoring process, which is continually improved through penetration-testing.</span></span> <span data-ttu-id="16ea7-125">此 DDoS 防禦系統的設計，不僅可承受來自外部的攻擊，還能承受來自其他 Azure 租用戶的攻擊。</span><span class="sxs-lookup"><span data-stu-id="16ea7-125">This DDoS defense system is designed to withstand not only attacks from the outside but also from other Azure tenants.</span></span> <span data-ttu-id="16ea7-126">如需詳細資料，請參閱 [Microsoft Azure 網路安全性](http://download.microsoft.com/download/C/A/3/CA3FC5C0-ECE0-4F87-BF4B-D74064A00846/AzureNetworkSecurity_v3_Feb2015.pdf)。</span><span class="sxs-lookup"><span data-stu-id="16ea7-126">For more detail, see [Microsoft Azure Network Security](http://download.microsoft.com/download/C/A/3/CA3FC5C0-ECE0-4F87-BF4B-D74064A00846/AzureNetworkSecurity_v3_Feb2015.pdf).</span></span>

<span data-ttu-id="16ea7-127">您也可以建立啟動工作，選擇性地封鎖一些特定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="16ea7-127">You can also create a startup task to selectively block some specific IP addresses.</span></span> <span data-ttu-id="16ea7-128">如需詳細資訊，請參閱[封鎖特定 IP 位址](cloud-services-startup-tasks-common.md#block-a-specific-ip-address)。</span><span class="sxs-lookup"><span data-stu-id="16ea7-128">For more information, see [Block a specific IP address](cloud-services-startup-tasks-common.md#block-a-specific-ip-address).</span></span>

## <a name="when-i-try-to-rdp-to-my-cloud-service-instance-i-get-the-message-the-user-account-has-expired"></a><span data-ttu-id="16ea7-129">當我嘗試 RDP 到我的雲端服務執行個體時，會收到這個訊息：「使用者帳戶已過期」。</span><span class="sxs-lookup"><span data-stu-id="16ea7-129">When I try to RDP to my cloud service instance, I get the message, "The user account has expired."</span></span>
<span data-ttu-id="16ea7-130">當您略過 RDP 設定中所設定的到期日時，可能會收到「此使用者帳戶已過期」的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="16ea7-130">You may get the error message "This user account has expired" when you bypass the expiration date that is configured in your RDP settings.</span></span> <span data-ttu-id="16ea7-131">您可以從入口網站中變更到期日，方法是遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="16ea7-131">You can change the expiration date from the portal by following these steps:</span></span>
1. <span data-ttu-id="16ea7-132">登入 Azure 管理主控台 ( https://manage.windowsazure.com )，瀏覽至您的雲端服務，然後選取 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="16ea7-132">Log in to the Azure Management Console (https://manage.windowsazure.com), navigate to your cloud service, and select the **Configure** tab.</span></span>
2. <span data-ttu-id="16ea7-133">選取 [遠端]。</span><span class="sxs-lookup"><span data-stu-id="16ea7-133">Select **Remote**.</span></span>
3. <span data-ttu-id="16ea7-134">變更「到期日」的日期，然後儲存設定。</span><span class="sxs-lookup"><span data-stu-id="16ea7-134">Change the "Expires On" date, and then save the configuration.</span></span>

<span data-ttu-id="16ea7-135">您現在應該能夠 RDP 到您的電腦。</span><span class="sxs-lookup"><span data-stu-id="16ea7-135">You now should be able to RDP to your machine.</span></span>

## <a name="why-is-loadbalancer-not-balancing-traffic-equally"></a><span data-ttu-id="16ea7-136">為什麼負載平衡器並未平均平衡流量？</span><span class="sxs-lookup"><span data-stu-id="16ea7-136">Why is LoadBalancer not balancing traffic equally?</span></span>
<span data-ttu-id="16ea7-137">如需如何內部負載平衡器運作方式的相關資訊，請參閱 [Azure Load Balancer 的新分散模式](https://azure.microsoft.com/blog/azure-load-balancer-new-distribution-mode/)。</span><span class="sxs-lookup"><span data-stu-id="16ea7-137">For information about how internal load balancer works, see [Azure Load Balancer new distribution mode](https://azure.microsoft.com/blog/azure-load-balancer-new-distribution-mode/).</span></span>

<span data-ttu-id="16ea7-138">所用的分配演算法是 5 個 Tuple (來源 IP、來源連接埠、目的地 IP、目的地連接埠、通訊協定類型) 的雜湊，將流量對應至可用的伺服器。</span><span class="sxs-lookup"><span data-stu-id="16ea7-138">The distribution algorithm used is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash to map traffic to available servers.</span></span> <span data-ttu-id="16ea7-139">它只在傳輸工作階段內提供綁定。</span><span class="sxs-lookup"><span data-stu-id="16ea7-139">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="16ea7-140">相同 TCP 或 UDP 工作階段中的封包會被導向至負載平衡端點後面的相同資料中心 IP (DIP) 執行個體。</span><span class="sxs-lookup"><span data-stu-id="16ea7-140">Packets in the same TCP or UDP session will be directed to the same datacenter IP (DIP) instance behind the load balanced endpoint.</span></span> <span data-ttu-id="16ea7-141">當用戶端關閉並重新開啟連線或從相同的來源 IP 啟動新的工作階段時，來源連接埠便會變更，進而導致流量進入不同的 DIP 端點。</span><span class="sxs-lookup"><span data-stu-id="16ea7-141">When the client closes and re-opens the connection or starts a new session from the same source IP, the source port changes and causes the traffic to go to a different DIP endpoint.</span></span>
