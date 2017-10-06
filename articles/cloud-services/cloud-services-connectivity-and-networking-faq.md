---
title: "aaaConnectivity 和網路功能的問題，Microsoft Azure 雲端服務的常見問題集 |Microsoft 文件"
description: "本文列出 hello 連線和 Microsoft Azure 雲端服務的網路功能的相關常見問題集。"
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
ms.openlocfilehash: e725dbbf585a76807362c59299d0a31f511afd3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connectivity-and-networking-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a><span data-ttu-id="90e9f-103">Azure 雲端服務之連線能力和網路服務問題：常見問題集 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="90e9f-103">Connectivity and networking issues for Azure Cloud Services: Frequently asked questions (FAQs)</span></span>

<span data-ttu-id="90e9f-104">本文包含 [Microsoft Azure 雲端服務](https://azure.microsoft.com/services/cloud-services)之連線能力和網路服務問題的相關常見問題集。</span><span class="sxs-lookup"><span data-stu-id="90e9f-104">This article includes frequently asked questions about connectivity and networking issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span></span> <span data-ttu-id="90e9f-105">此外，您也可以參考 hello[雲端服務 VM 大小頁面](cloud-services-sizes-specs.md)大小資訊。</span><span class="sxs-lookup"><span data-stu-id="90e9f-105">You can also consult hello [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="90e9f-106">無法在多 VIP 的雲端服務中保留 IP</span><span class="sxs-lookup"><span data-stu-id="90e9f-106">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="90e9f-107">首先，請確定您正嘗試 tooreserve hello IP 用於該 hello 虛擬機器執行個體已開啟。</span><span class="sxs-lookup"><span data-stu-id="90e9f-107">First, make sure that hello virtual machine instance that you're trying tooreserve hello IP for is turned on.</span></span> <span data-ttu-id="90e9f-108">第二，請確定您正在使用保留 Ip 的同時 hello 預備和生產環境部署。</span><span class="sxs-lookup"><span data-stu-id="90e9f-108">Second, make sure that you're using Reserved IPs for both hello staging and production deployments.</span></span> <span data-ttu-id="90e9f-109">**不這麼做**hello 部署正在升級時，變更 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="90e9f-109">**Do not** change hello settings while hello deployment is upgrading.</span></span>

## <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="90e9f-110">當我有 NSG 時，應如何設定遠端桌面？</span><span class="sxs-lookup"><span data-stu-id="90e9f-110">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="90e9f-111">新增規則 toohello 允許連接埠上的流量的 NSG **3389**和**20000**。</span><span class="sxs-lookup"><span data-stu-id="90e9f-111">Add rules toohello NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="90e9f-112">遠端桌面使用者連接埠 **3389**。</span><span class="sxs-lookup"><span data-stu-id="90e9f-112">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="90e9f-113">雲端服務執行個體是負載平衡，因此您無法直接控制至哪一個執行個體 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="90e9f-113">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="90e9f-114">hello *RemoteForwarder*和*RemoteAccess*代理程式管理 RDP 流量，並允許 hello 用戶端 toosend RDP cookie，並指定要個別執行個體 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="90e9f-114">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="90e9f-115">hello *RemoteForwarder*和*RemoteAccess*代理程式需要該連接埠**20000**開啟，如果您有 NSG 可能會封鎖連接。</span><span class="sxs-lookup"><span data-stu-id="90e9f-115">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="can-i-ping-a-cloud-service"></a><span data-ttu-id="90e9f-116">是否可偵測雲端服務？</span><span class="sxs-lookup"><span data-stu-id="90e9f-116">Can I ping a cloud service?</span></span>

<span data-ttu-id="90e9f-117">否，不是使用 hello normal"ping"/ ICMP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="90e9f-117">No, not by using hello normal "ping"/ICMP protocol.</span></span> <span data-ttu-id="90e9f-118">hello ICMP 通訊協定不允許透過 hello Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="90e9f-118">hello ICMP protocol is not permitted through hello Azure load balancer.</span></span>

<span data-ttu-id="90e9f-119">建議您不要連接埠 ping tootest 連線。</span><span class="sxs-lookup"><span data-stu-id="90e9f-119">tootest connectivity, we recommend that you do a port ping.</span></span> <span data-ttu-id="90e9f-120">當 Ping.exe 使用 ICMP 時，其他工具，例如 PSPing、 Nmap 及 telnet 可讓您 tootest 連線 tooa 特定 TCP 通訊埠。</span><span class="sxs-lookup"><span data-stu-id="90e9f-120">While Ping.exe uses ICMP, other tools, such as PSPing, Nmap, and telnet allow you tootest connectivity tooa specific TCP port.</span></span>

<span data-ttu-id="90e9f-121">如需詳細資訊，請參閱[改用 ICMP tootest Azure VM 連接的連接埠 ping](https://blogs.msdn.microsoft.com/mast/2014/06/22/use-port-pings-instead-of-icmp-to-test-azure-vm-connectivity/)。</span><span class="sxs-lookup"><span data-stu-id="90e9f-121">For more information, see [Use port pings instead of ICMP tootest Azure VM connectivity](https://blogs.msdn.microsoft.com/mast/2014/06/22/use-port-pings-instead-of-icmp-to-test-azure-vm-connectivity/).</span></span>

## <a name="how-do-i-prevent-receiving-thousands-of-hits-from-unknown-ip-addresses-that-indicate-some-sort-of-malicious-attack-toohello-cloud-service"></a><span data-ttu-id="90e9f-122">如何停止接收數千個叫用來自未知的 IP 位址，以指出特定類型的惡意攻擊 toohello 雲端服務？</span><span class="sxs-lookup"><span data-stu-id="90e9f-122">How do I prevent receiving thousands of hits from unknown IP addresses that indicate some sort of malicious attack toohello cloud service?</span></span>
<span data-ttu-id="90e9f-123">Azure 實作多層的網路安全性 tooprotect 分散式阻斷服務 (DDoS) 攻擊針對其平台服務。</span><span class="sxs-lookup"><span data-stu-id="90e9f-123">Azure implements a multilayer network security tooprotect its platform services against distributed denial-of-service (DDoS) attacks.</span></span> <span data-ttu-id="90e9f-124">hello Azure DDoS 防禦系統是 Azure 的連續監視處理序，以便透過滲透測試會持續改良的一部分。</span><span class="sxs-lookup"><span data-stu-id="90e9f-124">hello Azure DDoS defense system is part of Azure’s continuous monitoring process, which is continually improved through penetration-testing.</span></span> <span data-ttu-id="90e9f-125">此 DDoS 防禦系統設計 toowithstand 不僅攻擊從外部 hello 但來自其他 Azure 租用戶。</span><span class="sxs-lookup"><span data-stu-id="90e9f-125">This DDoS defense system is designed toowithstand not only attacks from hello outside but also from other Azure tenants.</span></span> <span data-ttu-id="90e9f-126">如需詳細資料，請參閱 [Microsoft Azure 網路安全性](http://download.microsoft.com/download/C/A/3/CA3FC5C0-ECE0-4F87-BF4B-D74064A00846/AzureNetworkSecurity_v3_Feb2015.pdf)。</span><span class="sxs-lookup"><span data-stu-id="90e9f-126">For more detail, see [Microsoft Azure Network Security](http://download.microsoft.com/download/C/A/3/CA3FC5C0-ECE0-4F87-BF4B-D74064A00846/AzureNetworkSecurity_v3_Feb2015.pdf).</span></span>

<span data-ttu-id="90e9f-127">您也可以建立啟動工作 tooselectively 區塊一些特定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="90e9f-127">You can also create a startup task tooselectively block some specific IP addresses.</span></span> <span data-ttu-id="90e9f-128">如需詳細資訊，請參閱[封鎖特定 IP 位址](cloud-services-startup-tasks-common.md#block-a-specific-ip-address)。</span><span class="sxs-lookup"><span data-stu-id="90e9f-128">For more information, see [Block a specific IP address](cloud-services-startup-tasks-common.md#block-a-specific-ip-address).</span></span>

## <a name="when-i-try-toordp-toomy-cloud-service-instance-i-get-hello-message-hello-user-account-has-expired"></a><span data-ttu-id="90e9f-129">當我嘗試 tooRDP toomy 雲端服務執行個體時，我會收到 hello 訊息，「 hello 使用者帳戶已過期 」。</span><span class="sxs-lookup"><span data-stu-id="90e9f-129">When I try tooRDP toomy cloud service instance, I get hello message, "hello user account has expired."</span></span>
<span data-ttu-id="90e9f-130">您略過您的 RDP 設定中的 hello 到期日時，可能會收到 hello 錯誤訊息 「 此使用者帳戶已過期 」。</span><span class="sxs-lookup"><span data-stu-id="90e9f-130">You may get hello error message "This user account has expired" when you bypass hello expiration date that is configured in your RDP settings.</span></span> <span data-ttu-id="90e9f-131">您可以從 hello 入口網站中變更 hello 到期日，依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="90e9f-131">You can change hello expiration date from hello portal by following these steps:</span></span>
1. <span data-ttu-id="90e9f-132">登入 toohello Azure 管理主控台 (https://manage.windowsazure.com)，瀏覽 tooyour 雲端服務，然後選取 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="90e9f-132">Log in toohello Azure Management Console (https://manage.windowsazure.com), navigate tooyour cloud service, and select hello **Configure** tab.</span></span>
2. <span data-ttu-id="90e9f-133">選取 [遠端]。</span><span class="sxs-lookup"><span data-stu-id="90e9f-133">Select **Remote**.</span></span>
3. <span data-ttu-id="90e9f-134">變更 hello"過期於 」 日期，並儲存 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="90e9f-134">Change hello "Expires On" date, and then save hello configuration.</span></span>

<span data-ttu-id="90e9f-135">您現在應該能夠 tooRDP tooyour 機器。</span><span class="sxs-lookup"><span data-stu-id="90e9f-135">You now should be able tooRDP tooyour machine.</span></span>

## <a name="why-is-loadbalancer-not-balancing-traffic-equally"></a><span data-ttu-id="90e9f-136">為什麼負載平衡器並未平均平衡流量？</span><span class="sxs-lookup"><span data-stu-id="90e9f-136">Why is LoadBalancer not balancing traffic equally?</span></span>
<span data-ttu-id="90e9f-137">如需如何內部負載平衡器運作方式的相關資訊，請參閱 [Azure Load Balancer 的新分散模式](https://azure.microsoft.com/blog/azure-load-balancer-new-distribution-mode/)。</span><span class="sxs-lookup"><span data-stu-id="90e9f-137">For information about how internal load balancer works, see [Azure Load Balancer new distribution mode](https://azure.microsoft.com/blog/azure-load-balancer-new-distribution-mode/).</span></span>

<span data-ttu-id="90e9f-138">使用的 hello 分配演算法是 5 個 tuple (來源 IP、 來源連接埠，目的地 IP、 目的地連接埠通訊協定類型) 雜湊 toomap 流量 tooavailable 伺服器。</span><span class="sxs-lookup"><span data-stu-id="90e9f-138">hello distribution algorithm used is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash toomap traffic tooavailable servers.</span></span> <span data-ttu-id="90e9f-139">它只在傳輸工作階段內提供綁定。</span><span class="sxs-lookup"><span data-stu-id="90e9f-139">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="90e9f-140">在相同的 TCP 或 UDP 工作階段將為的 hello 封包導向的 toohello hello 負載平衡端點之後執行個體的相同資料中心 IP (DIP)。</span><span class="sxs-lookup"><span data-stu-id="90e9f-140">Packets in hello same TCP or UDP session will be directed toohello same datacenter IP (DIP) instance behind hello load balanced endpoint.</span></span> <span data-ttu-id="90e9f-141">Hello 用戶端關閉並重新開啟 hello 連接或從 hello 開始新的工作階段時相同來源 IP，hello 來源連接埠變更，並造成 hello 流量 toogo tooa 不同 DIP 的端點。</span><span class="sxs-lookup"><span data-stu-id="90e9f-141">When hello client closes and re-opens hello connection or starts a new session from hello same source IP, hello source port changes and causes hello traffic toogo tooa different DIP endpoint.</span></span>
