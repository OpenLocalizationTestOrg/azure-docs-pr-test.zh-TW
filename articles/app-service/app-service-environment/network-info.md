---
title: "Azure App Service Environment 的網路考量"
description: "說明 ASE 網路流量與如何使用 ASE 設定 NSG 和 UDR"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 955a4d84-94ca-418d-aa79-b57a5eb8cb85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ccompy
ms.openlocfilehash: 3be0d7a202ff53f5532fd7169a50a04cfaf88832
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="networking-considerations-for-an-app-service-environment"></a><span data-ttu-id="0d926-103">App Service Environment 的網路考量</span><span class="sxs-lookup"><span data-stu-id="0d926-103">Networking considerations for an App Service environment</span></span> #

## <a name="overview"></a><span data-ttu-id="0d926-104">概觀</span><span class="sxs-lookup"><span data-stu-id="0d926-104">Overview</span></span> ##

 <span data-ttu-id="0d926-105">Azure [App Service Environment][Intro] 是將 Azure App Service 部署到您 Azure 虛擬網路 (VNet) 中子網路的一種部署。</span><span class="sxs-lookup"><span data-stu-id="0d926-105">Azure [App Service Environment][Intro] is a deployment of Azure App Service into a subnet in your Azure virtual network (VNet).</span></span> <span data-ttu-id="0d926-106">App Service Environment (ASE) 有二種部署類型：</span><span class="sxs-lookup"><span data-stu-id="0d926-106">There are two deployment types for an App Service environment (ASE):</span></span>

- <span data-ttu-id="0d926-107">**外部 ASE**：會在可存取網際網路的 IP 位址上公開 ASE 裝載的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d926-107">**External ASE**: Exposes the ASE-hosted apps on an internet-accessible IP address.</span></span> <span data-ttu-id="0d926-108">如需詳細資訊，請參閱[建立外部 ASE][MakeExternalASE]。</span><span class="sxs-lookup"><span data-stu-id="0d926-108">For more information, see [Create an External ASE][MakeExternalASE].</span></span>
- <span data-ttu-id="0d926-109">**ILB ASE**：會在您 VNet 內部的 IP 位址上公開 ASE 裝載的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d926-109">**ILB ASE**: Exposes the ASE-hosted apps on an IP address inside your VNet.</span></span> <span data-ttu-id="0d926-110">內部端點是一個內部負載平衡器 (ILB)，這就是它稱為 ILB ASE 的原因。</span><span class="sxs-lookup"><span data-stu-id="0d926-110">The internal endpoint is an internal load balancer (ILB), which is why it's called an ILB ASE.</span></span> <span data-ttu-id="0d926-111">如需詳細資訊，請參閱[建立和使用 ILB ASE][MakeILBASE]。</span><span class="sxs-lookup"><span data-stu-id="0d926-111">For more information, see [Create and use an ILB ASE][MakeILBASE].</span></span>

<span data-ttu-id="0d926-112">App Service Environment 現在有兩個版本：ASEv1 和 ASEv2。</span><span class="sxs-lookup"><span data-stu-id="0d926-112">There are now two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="0d926-113">如需 ASEv1 的資訊，請參閱 [App Service Environment v1 簡介][ASEv1Intro]。</span><span class="sxs-lookup"><span data-stu-id="0d926-113">For information on ASEv1, see [Introduction to App Service Environment v1][ASEv1Intro].</span></span> <span data-ttu-id="0d926-114">ASEv1 可以部署至傳統或 Resource Manager VNet 中。</span><span class="sxs-lookup"><span data-stu-id="0d926-114">ASEv1 can be deployed in a classic or Resource Manager VNet.</span></span> <span data-ttu-id="0d926-115">ASEv2 只能部署至 Resource Manager VNet 中。</span><span class="sxs-lookup"><span data-stu-id="0d926-115">ASEv2 can only be deployed into a Resource Manager VNet.</span></span>

<span data-ttu-id="0d926-116">來自 ASE 並傳送至網際網路的所有呼叫，都會透過為 ASE 指派的 VIP 離開 VNet。</span><span class="sxs-lookup"><span data-stu-id="0d926-116">All calls from an ASE that go to the internet leave the VNet through a VIP assigned for the ASE.</span></span> <span data-ttu-id="0d926-117">然後，此 VIP 的公用 IP 就會成為來自 ASE 並傳送至網際網路之所有呼叫的來源 IP。</span><span class="sxs-lookup"><span data-stu-id="0d926-117">The public IP of this VIP is then the source IP for all calls from the ASE that go to the internet.</span></span> <span data-ttu-id="0d926-118">如果 ASE 中的應用程式會呼叫位於 VNet 中或跨 VPN 的資源，則來源 IP 就會是 ASE 所用子網路中的其中一個 IP。</span><span class="sxs-lookup"><span data-stu-id="0d926-118">If the apps in your ASE make calls to resources in your VNet or across a VPN, the source IP is one of the IPs in the subnet used by your ASE.</span></span> <span data-ttu-id="0d926-119">因為 ASE 是位於 VNet 之內，所以它也可以存取 VNet 內的資源，而不需要任何額外設定。</span><span class="sxs-lookup"><span data-stu-id="0d926-119">Because the ASE is within the VNet, it can also access resources within the VNet without any additional configuration.</span></span> <span data-ttu-id="0d926-120">如果 VNet 是連線至您的內部部署網路，您 ASE 中的應用程式也會擁有該處資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="0d926-120">If the VNet is connected to your on-premises network, apps in your ASE also have access to resources there.</span></span> <span data-ttu-id="0d926-121">您不再需要設定 ASE 或您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d926-121">You don't need to configure the ASE or your app any further.</span></span>

![外部 ASE][1] 

<span data-ttu-id="0d926-123">如果您有外部 ASE，公用 VIP 也會是您 ASE 應用程式針對以下項目進行解析的端點：</span><span class="sxs-lookup"><span data-stu-id="0d926-123">If you have an External ASE, the public VIP is also the endpoint that your ASE apps resolve to for:</span></span>

* <span data-ttu-id="0d926-124">HTTP/S。</span><span class="sxs-lookup"><span data-stu-id="0d926-124">HTTP/S.</span></span> 
* <span data-ttu-id="0d926-125">FTP/S。</span><span class="sxs-lookup"><span data-stu-id="0d926-125">FTP/S.</span></span> 
* <span data-ttu-id="0d926-126">Web 部署。</span><span class="sxs-lookup"><span data-stu-id="0d926-126">Web deployment.</span></span>
* <span data-ttu-id="0d926-127">遠端偵錯。</span><span class="sxs-lookup"><span data-stu-id="0d926-127">Remote debugging.</span></span>

![ILB ASE][2]

<span data-ttu-id="0d926-129">如果您有 ILB ASE，則 ILB 的 IP 位址就會是 HTTP/S、FTP/S、Web 部署和遠端偵錯的端點。</span><span class="sxs-lookup"><span data-stu-id="0d926-129">If you have an ILB ASE, the IP address of the ILB is the endpoint for HTTP/S, FTP/S, web deployment, and remote debugging.</span></span>

<span data-ttu-id="0d926-130">一般的應用程式存取連接埠為：</span><span class="sxs-lookup"><span data-stu-id="0d926-130">The normal app access ports are:</span></span>

| <span data-ttu-id="0d926-131">使用</span><span class="sxs-lookup"><span data-stu-id="0d926-131">Use</span></span> | <span data-ttu-id="0d926-132">從</span><span class="sxs-lookup"><span data-stu-id="0d926-132">From</span></span> | <span data-ttu-id="0d926-133">收件人</span><span class="sxs-lookup"><span data-stu-id="0d926-133">To</span></span> |
|----------|---------|-------------|
|  <span data-ttu-id="0d926-134">HTTP/HTTPS</span><span class="sxs-lookup"><span data-stu-id="0d926-134">HTTP/HTTPS</span></span>  | <span data-ttu-id="0d926-135">可由使用者設定</span><span class="sxs-lookup"><span data-stu-id="0d926-135">User configurable</span></span> |  <span data-ttu-id="0d926-136">80、443</span><span class="sxs-lookup"><span data-stu-id="0d926-136">80, 443</span></span> |
|  <span data-ttu-id="0d926-137">FTP/FTPS</span><span class="sxs-lookup"><span data-stu-id="0d926-137">FTP/FTPS</span></span>    | <span data-ttu-id="0d926-138">可由使用者設定</span><span class="sxs-lookup"><span data-stu-id="0d926-138">User configurable</span></span> |  <span data-ttu-id="0d926-139">21、990、10001-10020</span><span class="sxs-lookup"><span data-stu-id="0d926-139">21, 990, 10001-10020</span></span> |
|  <span data-ttu-id="0d926-140">Visual Studio 遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="0d926-140">Visual Studio remote debugging</span></span>  |  <span data-ttu-id="0d926-141">可由使用者設定</span><span class="sxs-lookup"><span data-stu-id="0d926-141">User configurable</span></span> |  <span data-ttu-id="0d926-142">4016、4018、4020、4022</span><span class="sxs-lookup"><span data-stu-id="0d926-142">4016, 4018, 4020, 4022</span></span> |

<span data-ttu-id="0d926-143">這適用於您位於外部 ASE 或 ILB ASE 上的情況。</span><span class="sxs-lookup"><span data-stu-id="0d926-143">This is true if you're on an External ASE or on an ILB ASE.</span></span> <span data-ttu-id="0d926-144">如果您是在外部 ASE 中，就會叫用公用 VIP 上的那些連接埠。</span><span class="sxs-lookup"><span data-stu-id="0d926-144">If you're on an External ASE, you hit those ports on the public VIP.</span></span> <span data-ttu-id="0d926-145">如果您是在 ILB ASE 中，就會叫用 ILB 上的那些連接埠。</span><span class="sxs-lookup"><span data-stu-id="0d926-145">If you're on an ILB ASE, you hit those ports on the ILB.</span></span> <span data-ttu-id="0d926-146">如果您鎖定連接埠 443，可能會影響在入口網站中公開的某些功能。</span><span class="sxs-lookup"><span data-stu-id="0d926-146">If you lock down port 443, there can be an effect on some features exposed in the portal.</span></span> <span data-ttu-id="0d926-147">如需詳細資訊，請參閱[入口網站相依性](#portaldep)。</span><span class="sxs-lookup"><span data-stu-id="0d926-147">For more information, see [Portal dependencies](#portaldep).</span></span>

## <a name="ase-dependencies"></a><span data-ttu-id="0d926-148">ASE 相依性</span><span class="sxs-lookup"><span data-stu-id="0d926-148">ASE dependencies</span></span> ##

<span data-ttu-id="0d926-149">ASE 輸入存取相依性為：</span><span class="sxs-lookup"><span data-stu-id="0d926-149">An ASE inbound access dependency is:</span></span>

| <span data-ttu-id="0d926-150">使用</span><span class="sxs-lookup"><span data-stu-id="0d926-150">Use</span></span> | <span data-ttu-id="0d926-151">從</span><span class="sxs-lookup"><span data-stu-id="0d926-151">From</span></span> | <span data-ttu-id="0d926-152">收件人</span><span class="sxs-lookup"><span data-stu-id="0d926-152">To</span></span> |
|-----|------|----|
| <span data-ttu-id="0d926-153">管理</span><span class="sxs-lookup"><span data-stu-id="0d926-153">Management</span></span> | <span data-ttu-id="0d926-154">App Service 管理位址</span><span class="sxs-lookup"><span data-stu-id="0d926-154">App Service management addresses</span></span> | <span data-ttu-id="0d926-155">ASE 子網路：454、455</span><span class="sxs-lookup"><span data-stu-id="0d926-155">ASE subnet: 454, 455</span></span> |
|  <span data-ttu-id="0d926-156">ASE 內部通訊</span><span class="sxs-lookup"><span data-stu-id="0d926-156">ASE internal communication</span></span> | <span data-ttu-id="0d926-157">ASE 子網路：所有連接埠</span><span class="sxs-lookup"><span data-stu-id="0d926-157">ASE subnet: All ports</span></span> | <span data-ttu-id="0d926-158">ASE 子網路：所有連接埠</span><span class="sxs-lookup"><span data-stu-id="0d926-158">ASE subnet: All ports</span></span>
|  <span data-ttu-id="0d926-159">允許 Azure Load Balancer 輸入</span><span class="sxs-lookup"><span data-stu-id="0d926-159">Allow Azure load balancer inbound</span></span> | <span data-ttu-id="0d926-160">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="0d926-160">Azure load balancer</span></span> | <span data-ttu-id="0d926-161">ASE 子網路：所有連接埠</span><span class="sxs-lookup"><span data-stu-id="0d926-161">ASE subnet: All ports</span></span>
|  <span data-ttu-id="0d926-162">應用程式指派的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="0d926-162">App assigned IP addresses</span></span> | <span data-ttu-id="0d926-163">應用程式指派的位址</span><span class="sxs-lookup"><span data-stu-id="0d926-163">App assigned addresses</span></span> | <span data-ttu-id="0d926-164">ASE 子網路：所有連接埠</span><span class="sxs-lookup"><span data-stu-id="0d926-164">ASE subnet: All ports</span></span>

<span data-ttu-id="0d926-165">除了系統監控以外，輸入流量也提供了 ASE 的命令與控制。</span><span class="sxs-lookup"><span data-stu-id="0d926-165">The inbound traffic provides command and control of the ASE in addition to system monitoring.</span></span> <span data-ttu-id="0d926-166">此流量的來源 IP 列於 [ASE 管理位址][ASEManagement]文件中。</span><span class="sxs-lookup"><span data-stu-id="0d926-166">The source IPs for this traffic are listed in the [ASE Management addresses][ASEManagement] document.</span></span> <span data-ttu-id="0d926-167">網路安全性設定需在連接埠 454 和 455 上允許來自所有 IP 的存取。</span><span class="sxs-lookup"><span data-stu-id="0d926-167">The network security configuration needs to allow access from all IPs on ports 454 and 455.</span></span>

<span data-ttu-id="0d926-168">ASE 子網路中有許多用於內部元件通訊的連接埠，您可以變更這些連接埠。</span><span class="sxs-lookup"><span data-stu-id="0d926-168">Within the ASE subnet there are many ports used for internal component communication and they can change.</span></span>  <span data-ttu-id="0d926-169">ASE 子網路的所有連接埠都必須能夠從 ASE 子網路存取。</span><span class="sxs-lookup"><span data-stu-id="0d926-169">This requires all of the ports in the ASE subnet to be accessible from the ASE subnet.</span></span> 

<span data-ttu-id="0d926-170">您必須開啟最小連接埠 454、455 和 16001，才能在 Azure Load Balancer 與 ASE 子網路之間進行通訊。</span><span class="sxs-lookup"><span data-stu-id="0d926-170">For the communication between the Azure load balancer and the ASE subnet the minimum ports that need to be open are 454, 455 and 16001.</span></span> <span data-ttu-id="0d926-171">16001 連接埠可用來保持負載平衡器與 ASE 之間的流量運作。</span><span class="sxs-lookup"><span data-stu-id="0d926-171">The 16001 port is used for keep alive traffic between the load balancer and the ASE.</span></span> <span data-ttu-id="0d926-172">如果您使用 ILB ASE，則可以將流量僅鎖定於 454、455、16001 連接埠。</span><span class="sxs-lookup"><span data-stu-id="0d926-172">If you are using an ILB ASE then you can lock traffic down to just the 454, 455, 16001 ports.</span></span>  <span data-ttu-id="0d926-173">如果您使用外部 ASE，則需要考慮一般應用程式存取連接埠。</span><span class="sxs-lookup"><span data-stu-id="0d926-173">If you are using an External ASE then you need to take into account the normal app access ports.</span></span>  <span data-ttu-id="0d926-174">如果您使用應用程式指派的位址，則需要在所有連接埠將它開啟。</span><span class="sxs-lookup"><span data-stu-id="0d926-174">If you are using app assigned addresses you need to open it to all ports.</span></span>  <span data-ttu-id="0d926-175">將位址指派給特定應用程式時，負載平衡器會使用事先不知道的連接埠將 HTTP 和 HTTPS 流量傳送至 ASE。</span><span class="sxs-lookup"><span data-stu-id="0d926-175">When an address is assigned to a specific app, then the load balancer will use ports that are not known of in advance to send HTTP and HTTPS traffic to the ASE.</span></span>

<span data-ttu-id="0d926-176">如果您使用應用程式指派的 IP 位址，則需要允許將來自應用程式指派之 IP 的流量傳送至 ASE 子網路。</span><span class="sxs-lookup"><span data-stu-id="0d926-176">If you are using app assigned IP addresses you need to allow traffic from the IPs assigned to your apps to the ASE subnet.</span></span>

<span data-ttu-id="0d926-177">對於輸出存取，ASE 取決於多個外部系統。</span><span class="sxs-lookup"><span data-stu-id="0d926-177">For outbound access, an ASE depends on multiple external systems.</span></span> <span data-ttu-id="0d926-178">那些系統相依性會以 DNS 名稱定義，且不會對應至一組固定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0d926-178">Those system dependencies are defined with DNS names and don't map to a fixed set of IP addresses.</span></span> <span data-ttu-id="0d926-179">因此，ASE 需要透過不同的連接埠進行從 ASE 子網路至所有外部 IP 的輸出存取。</span><span class="sxs-lookup"><span data-stu-id="0d926-179">Thus, the ASE requires outbound access from the ASE subnet to all external IPs across a variety of ports.</span></span> <span data-ttu-id="0d926-180">ASE 具有下列輸出相依性：</span><span class="sxs-lookup"><span data-stu-id="0d926-180">An ASE has the following outbound dependencies:</span></span>

| <span data-ttu-id="0d926-181">使用</span><span class="sxs-lookup"><span data-stu-id="0d926-181">Use</span></span> | <span data-ttu-id="0d926-182">從</span><span class="sxs-lookup"><span data-stu-id="0d926-182">From</span></span> | <span data-ttu-id="0d926-183">收件人</span><span class="sxs-lookup"><span data-stu-id="0d926-183">To</span></span> |
|-----|------|----|
| <span data-ttu-id="0d926-184">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="0d926-184">Azure Storage</span></span> | <span data-ttu-id="0d926-185">ASE 子網路</span><span class="sxs-lookup"><span data-stu-id="0d926-185">ASE subnet</span></span> | <span data-ttu-id="0d926-186">table.core.windows.net、blob.core.windows.net、queue.core.windows.net、file.core.windows.net：80、443、445 (只有 ASEv1 才需要 445)</span><span class="sxs-lookup"><span data-stu-id="0d926-186">table.core.windows.net, blob.core.windows.net, queue.core.windows.net, file.core.windows.net: 80, 443, 445 (445 is only needed for ASEv1.)</span></span> |
| <span data-ttu-id="0d926-187">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0d926-187">Azure SQL Database</span></span> | <span data-ttu-id="0d926-188">ASE 子網路</span><span class="sxs-lookup"><span data-stu-id="0d926-188">ASE subnet</span></span> | <span data-ttu-id="0d926-189">database.windows.net：1433、11000-11999、14000-14999 (如需詳細資訊，請參閱 [SQL Database V12 連接埠用法](../../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md))</span><span class="sxs-lookup"><span data-stu-id="0d926-189">database.windows.net: 1433, 11000-11999, 14000-14999 (For more information, see [SQL Database V12 port usage](../../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md).)</span></span>|
| <span data-ttu-id="0d926-190">Azure 管理</span><span class="sxs-lookup"><span data-stu-id="0d926-190">Azure management</span></span> | <span data-ttu-id="0d926-191">ASE 子網路</span><span class="sxs-lookup"><span data-stu-id="0d926-191">ASE subnet</span></span> | <span data-ttu-id="0d926-192">management.core.windows.net、management.azure.com：443</span><span class="sxs-lookup"><span data-stu-id="0d926-192">management.core.windows.net, management.azure.com: 443</span></span> 
| <span data-ttu-id="0d926-193">SSL 憑證驗證</span><span class="sxs-lookup"><span data-stu-id="0d926-193">SSL certificate verification</span></span> |  <span data-ttu-id="0d926-194">ASE 子網路</span><span class="sxs-lookup"><span data-stu-id="0d926-194">ASE subnet</span></span>            |  <span data-ttu-id="0d926-195">ocsp.msocsp.com、mscrl.microsoft.com、crl.microsoft.com：443</span><span class="sxs-lookup"><span data-stu-id="0d926-195">ocsp.msocsp.com, mscrl.microsoft.com, crl.microsoft.com: 443</span></span>
| <span data-ttu-id="0d926-196">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d926-196">Azure Active Directory</span></span>        | <span data-ttu-id="0d926-197">ASE 子網路</span><span class="sxs-lookup"><span data-stu-id="0d926-197">ASE subnet</span></span>            |  <span data-ttu-id="0d926-198">網際網路：443</span><span class="sxs-lookup"><span data-stu-id="0d926-198">Internet: 443</span></span>
| <span data-ttu-id="0d926-199">App Service 管理</span><span class="sxs-lookup"><span data-stu-id="0d926-199">App Service management</span></span>        | <span data-ttu-id="0d926-200">ASE 子網路</span><span class="sxs-lookup"><span data-stu-id="0d926-200">ASE subnet</span></span>            |  <span data-ttu-id="0d926-201">網際網路：443</span><span class="sxs-lookup"><span data-stu-id="0d926-201">Internet: 443</span></span>
| <span data-ttu-id="0d926-202">Azure DNS</span><span class="sxs-lookup"><span data-stu-id="0d926-202">Azure DNS</span></span>                     | <span data-ttu-id="0d926-203">ASE 子網路</span><span class="sxs-lookup"><span data-stu-id="0d926-203">ASE subnet</span></span>            |  <span data-ttu-id="0d926-204">網際網路：53</span><span class="sxs-lookup"><span data-stu-id="0d926-204">Internet: 53</span></span>
| <span data-ttu-id="0d926-205">ASE 內部通訊</span><span class="sxs-lookup"><span data-stu-id="0d926-205">ASE internal communication</span></span>    | <span data-ttu-id="0d926-206">ASE 子網路：所有連接埠</span><span class="sxs-lookup"><span data-stu-id="0d926-206">ASE subnet: All ports</span></span> |  <span data-ttu-id="0d926-207">ASE 子網路：所有連接埠</span><span class="sxs-lookup"><span data-stu-id="0d926-207">ASE subnet: All ports</span></span>

<span data-ttu-id="0d926-208">如果 ASE 失去對這些相依性的存取，它會停止運作。</span><span class="sxs-lookup"><span data-stu-id="0d926-208">If the ASE loses access to these dependencies, it stops working.</span></span> <span data-ttu-id="0d926-209">當停止運作時間達到一定的長度之後，ASE 就會暫停。</span><span class="sxs-lookup"><span data-stu-id="0d926-209">When that happens long enough, the ASE is suspended.</span></span>

### <a name="customer-dns"></a><span data-ttu-id="0d926-210">客戶 DNS</span><span class="sxs-lookup"><span data-stu-id="0d926-210">Customer DNS</span></span> ###

<span data-ttu-id="0d926-211">如果已經使用客戶定義的 DNS 伺服器設定 VNet，租用戶工作負載就會使用該伺服器。</span><span class="sxs-lookup"><span data-stu-id="0d926-211">If the VNet is configured with a customer-defined DNS server, the tenant workloads use it.</span></span> <span data-ttu-id="0d926-212">基於管理目的，ASE 仍需要和 Azure DNS 通訊。</span><span class="sxs-lookup"><span data-stu-id="0d926-212">The ASE still needs to communicate with Azure DNS for management purposes.</span></span> 

<span data-ttu-id="0d926-213">如果 VNet 在 VPN 的另一端使用客戶 DNS 進行設定，DNS 伺服器必須能夠從包含 ASE 的子網路中進行連線。</span><span class="sxs-lookup"><span data-stu-id="0d926-213">If the VNet is configured with a customer DNS on the other side of a VPN, the DNS server must be reachable from the subnet that contains the ASE.</span></span>

<a name="portaldep"></a>

## <a name="portal-dependencies"></a><span data-ttu-id="0d926-214">入口網站相依性</span><span class="sxs-lookup"><span data-stu-id="0d926-214">Portal dependencies</span></span> ##

<span data-ttu-id="0d926-215">除了 ASE 功能性相依性之外，還有幾個額外項目和入口網站體驗有關。</span><span class="sxs-lookup"><span data-stu-id="0d926-215">In addition to the ASE functional dependencies, there are a few extra items related to the portal experience.</span></span> <span data-ttu-id="0d926-216">Azure 入口網站的部分功能需要能夠直接存取「SCM 網站」。</span><span class="sxs-lookup"><span data-stu-id="0d926-216">Some of the capabilities in the Azure portal depend on direct access to _SCM site_.</span></span> <span data-ttu-id="0d926-217">Azure App Service 中的每個應用程式都有兩個 URL。</span><span class="sxs-lookup"><span data-stu-id="0d926-217">For every app in Azure App Service, there are two URLs.</span></span> <span data-ttu-id="0d926-218">第一個 URL 是用來存取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d926-218">The first URL is to access your app.</span></span> <span data-ttu-id="0d926-219">第二個 URL 則是用來存取 SCM 網站，也稱為「Kudu 主控台」。</span><span class="sxs-lookup"><span data-stu-id="0d926-219">The second URL is to access the SCM site, which is also called the _Kudu console_.</span></span> <span data-ttu-id="0d926-220">使用 SCM 網站的功能包括：</span><span class="sxs-lookup"><span data-stu-id="0d926-220">Features that use the SCM site include:</span></span>

-   <span data-ttu-id="0d926-221">Web Job</span><span class="sxs-lookup"><span data-stu-id="0d926-221">Web jobs</span></span>
-   <span data-ttu-id="0d926-222">Functions</span><span class="sxs-lookup"><span data-stu-id="0d926-222">Functions</span></span>
-   <span data-ttu-id="0d926-223">記錄串流</span><span class="sxs-lookup"><span data-stu-id="0d926-223">Log streaming</span></span>
-   <span data-ttu-id="0d926-224">Kudu</span><span class="sxs-lookup"><span data-stu-id="0d926-224">Kudu</span></span>
-   <span data-ttu-id="0d926-225">擴充功能</span><span class="sxs-lookup"><span data-stu-id="0d926-225">Extensions</span></span>
-   <span data-ttu-id="0d926-226">處理序總管</span><span class="sxs-lookup"><span data-stu-id="0d926-226">Process Explorer</span></span>
-   <span data-ttu-id="0d926-227">主控台</span><span class="sxs-lookup"><span data-stu-id="0d926-227">Console</span></span>

<span data-ttu-id="0d926-228">當您使用 ILB ASE 時，無法從 VNet 外部透過網際網路存取 SCM 網站。</span><span class="sxs-lookup"><span data-stu-id="0d926-228">When you use an ILB ASE, the SCM site isn't internet accessible from outside the VNet.</span></span> <span data-ttu-id="0d926-229">當您的應用程式裝載於 ILB ASE 時，將無法從入口網站使用某些功能。</span><span class="sxs-lookup"><span data-stu-id="0d926-229">When your app is hosted on an ILB ASE, some capabilities will not work from the portal.</span></span>  

<span data-ttu-id="0d926-230">那些需要依賴 SCM 網站的功能中，有許多功能也會在 Kudo 主控台中直接提供。</span><span class="sxs-lookup"><span data-stu-id="0d926-230">Many of those capabilities that depend upon the SCM site are also available directly in the Kudu console.</span></span> <span data-ttu-id="0d926-231">您可以直接與它連線，不需要使用入口網站。</span><span class="sxs-lookup"><span data-stu-id="0d926-231">You can connect to it directly rather than by using the portal.</span></span> <span data-ttu-id="0d926-232">如果應用程式是裝載在 ILB ASE 中，請使用發行認證登入。</span><span class="sxs-lookup"><span data-stu-id="0d926-232">If your app is hosted in an ILB ASE, use your publishing credentials to sign in.</span></span> <span data-ttu-id="0d926-233">存取 ILB ASE 所裝載應用程式之 SCM 網站的 URL 具有以下格式：</span><span class="sxs-lookup"><span data-stu-id="0d926-233">The URL to access the SCM site of an app hosted in an ILB ASE has the following format:</span></span> 

```
<appname>.scm.<domain name the ILB ASE was created with> 
```

<span data-ttu-id="0d926-234">如果 ILB ASE 的網域名稱為 *contoso.net* 中，且應用程式名稱為 *testapp*，則應用程式已連線至 *testapp.contoso.net*。</span><span class="sxs-lookup"><span data-stu-id="0d926-234">If your ILB ASE is the domain name *contoso.net* and your app name is *testapp*, the app is reached at *testapp.contoso.net*.</span></span> <span data-ttu-id="0d926-235">與它搭配的 SCM 網站已經連線至 *testapp.scm.contoso.net*。</span><span class="sxs-lookup"><span data-stu-id="0d926-235">The SCM site that goes with it is reached at *testapp.scm.contoso.net*.</span></span>

### <a name="functions-and-web-jobs"></a><span data-ttu-id="0d926-236">函式和 Web 工作</span><span class="sxs-lookup"><span data-stu-id="0d926-236">Functions and Web jobs</span></span> ###

<span data-ttu-id="0d926-237">函式和 Web 工作都相依於 SCM 網站，但受到支援可用於入口網站，即使您的應用程式在 ILB ASE 中，只要您的瀏覽器可以到達 SCM 網站就沒問題。</span><span class="sxs-lookup"><span data-stu-id="0d926-237">Both Functions and Web jobs depend on the SCM site but are supported for use in the portal, even if your apps are in an ILB ASE, so long as your browser can reach the SCM site.</span></span>  <span data-ttu-id="0d926-238">如果您搭配 ILB ASE 使用自我簽署憑證，您必須啟用瀏覽器以信任該憑證。</span><span class="sxs-lookup"><span data-stu-id="0d926-238">If you are using a self-signed certificate with your ILB ASE, you will need to enable your browser to trust that certificate.</span></span>  <span data-ttu-id="0d926-239">若是 IE 和 Edge，這表示憑證必須在電腦信任存放區中。</span><span class="sxs-lookup"><span data-stu-id="0d926-239">For IE and Edge that means the certificate has to be in the computer trust store.</span></span>  <span data-ttu-id="0d926-240">如果您使用 Chrome，則表示您假設瀏覽器會直接到達 SCM 網站，而過早接受瀏覽器中的憑證。</span><span class="sxs-lookup"><span data-stu-id="0d926-240">If you are using Chrome then that means you accepted the certificate in the browser earlier by presumably hitting the scm site directly.</span></span>  <span data-ttu-id="0d926-241">最佳解決方法是使用瀏覽器信任鏈結中的商業憑證。</span><span class="sxs-lookup"><span data-stu-id="0d926-241">The best solution is to use a commercial certificate that is in the browser chain of trust.</span></span>  

## <a name="ase-ip-addresses"></a><span data-ttu-id="0d926-242">ASE IP 位址</span><span class="sxs-lookup"><span data-stu-id="0d926-242">ASE IP addresses</span></span> ##

<span data-ttu-id="0d926-243">ASE 有一些 IP 位址需要注意。</span><span class="sxs-lookup"><span data-stu-id="0d926-243">An ASE has a few IP addresses to be aware of.</span></span> <span data-ttu-id="0d926-244">如下：</span><span class="sxs-lookup"><span data-stu-id="0d926-244">They are:</span></span>

- <span data-ttu-id="0d926-245">**公用輸入 IP 位址**：用於外部 ASE 中的應用程式流量，以及外部 ASE 和 ILB ASE 中的管理流量。</span><span class="sxs-lookup"><span data-stu-id="0d926-245">**Public inbound IP address**: Used for app traffic in an External ASE, and management traffic in both an External ASE and an ILB ASE.</span></span>
- <span data-ttu-id="0d926-246">**輸出公用 IP**：用來作為 ASE 輸出連線離開 VNet 時的「來源」IP (不會透過 VPN 進行路由)。</span><span class="sxs-lookup"><span data-stu-id="0d926-246">**Outbound public IP**: Used as the "from" IP for outbound connections from the ASE that leave the VNet, which aren't routed down a VPN.</span></span>
- <span data-ttu-id="0d926-247">**ILB IP 位址**：如果您是使用 ILB ASE。</span><span class="sxs-lookup"><span data-stu-id="0d926-247">**ILB IP address**: If you use an ILB ASE.</span></span>
- <span data-ttu-id="0d926-248">**應用程式指派之以 IP 為主的 SSL 位址**：只有在使用外部 ASE 並已設定以 IP 為主的 SSL 時才能使用。</span><span class="sxs-lookup"><span data-stu-id="0d926-248">**App-assigned IP-based SSL addresses**: Only possible with an External ASE and when IP-based SSL is configured.</span></span>

<span data-ttu-id="0d926-249">在 Azure 入口網站中，所有這些 IP 位址都可以很容易地在 ASEv2 的 ASE UI 中看出來。</span><span class="sxs-lookup"><span data-stu-id="0d926-249">All these IP addresses are easily visible in an ASEv2 in the Azure portal from the ASE UI.</span></span> <span data-ttu-id="0d926-250">如果您有 ILB ASE，系統便會列出 ILB 的 IP。</span><span class="sxs-lookup"><span data-stu-id="0d926-250">If you have an ILB ASE, the IP for the ILB is listed.</span></span>

![IP 位址][3]

### <a name="app-assigned-ip-addresses"></a><span data-ttu-id="0d926-252">應用程式指派的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="0d926-252">App-assigned IP addresses</span></span> ###

<span data-ttu-id="0d926-253">在外部 ASE 的情況下，您可以將 IP 位址指派給個別的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d926-253">With an External ASE, you can assign IP addresses to individual apps.</span></span> <span data-ttu-id="0d926-254">您無法在 ILB ASE 的情況下那樣做。</span><span class="sxs-lookup"><span data-stu-id="0d926-254">You can't do that with an ILB ASE.</span></span> <span data-ttu-id="0d926-255">如需如何讓應用程式有自己 IP 位址的設定方式詳細資訊，請參閱[將現有的自訂 SSL 憑證繫結至 Azure Web Apps](../../app-service-web/app-service-web-tutorial-custom-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="0d926-255">For more information on how to configure your app to have its own IP address, see [Bind an existing custom SSL certificate to Azure web apps](../../app-service-web/app-service-web-tutorial-custom-ssl.md).</span></span>

<span data-ttu-id="0d926-256">當應用程式有自己以 IP 為主的 SSL 位址時，ASE 會保留兩個連接埠以對應至該 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0d926-256">When an app has its own IP-based SSL address, the ASE reserves two ports to map to that IP address.</span></span> <span data-ttu-id="0d926-257">一個連接埠供 HTTP 流量使用，另一個連接埠則供 HTTPS 使用。</span><span class="sxs-lookup"><span data-stu-id="0d926-257">One port is for HTTP traffic, and the other port is for HTTPS.</span></span> <span data-ttu-id="0d926-258">那些連接埠會列在 ASE UI 的 IP 位址區段中。</span><span class="sxs-lookup"><span data-stu-id="0d926-258">Those ports are listed in the ASE UI in the IP addresses section.</span></span> <span data-ttu-id="0d926-259">流量必須能夠從 VIP 觸達那些連接埠，否則會無法存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d926-259">Traffic must be able to reach those ports from the VIP or the apps are inaccessible.</span></span> <span data-ttu-id="0d926-260">在您設定網路安全性群組 (NSG) 時，請務必記住這項重要需求。</span><span class="sxs-lookup"><span data-stu-id="0d926-260">This requirement is important to remember when you configure Network Security Groups (NSGs).</span></span>

## <a name="network-security-groups"></a><span data-ttu-id="0d926-261">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="0d926-261">Network Security Groups</span></span> ##

<span data-ttu-id="0d926-262">[網路安全性群組][NSGs]提供控制 VNet 內網路存取的能力。</span><span class="sxs-lookup"><span data-stu-id="0d926-262">[Network Security Groups][NSGs] provide the ability to control network access within a VNet.</span></span> <span data-ttu-id="0d926-263">使用入口網站時，會有一個會拒絕一切內容的最低優先順序隱含拒絕規則。</span><span class="sxs-lookup"><span data-stu-id="0d926-263">When you use the portal, there's an implicit deny rule at the lowest priority to deny everything.</span></span> <span data-ttu-id="0d926-264">您所建立的是您的允許規則。</span><span class="sxs-lookup"><span data-stu-id="0d926-264">What you build are your allow rules.</span></span>

<span data-ttu-id="0d926-265">在 ASE 中，您不會有存取用來裝載 ASE 本身之 VM 的存取權。</span><span class="sxs-lookup"><span data-stu-id="0d926-265">In an ASE, you don't have access to the VMs used to host the ASE itself.</span></span> <span data-ttu-id="0d926-266">它們處於由 Microsoft 管理的訂用帳戶之中。</span><span class="sxs-lookup"><span data-stu-id="0d926-266">They're in a Microsoft-managed subscription.</span></span> <span data-ttu-id="0d926-267">如果想要針對 ASE 上的應用程式限制存取，請在 ASE 子網路上設定 NSG。</span><span class="sxs-lookup"><span data-stu-id="0d926-267">If you want to restrict access to the apps on the ASE, set NSGs on the ASE subnet.</span></span> <span data-ttu-id="0d926-268">這樣做時，請特別注意 ASE 相依性。</span><span class="sxs-lookup"><span data-stu-id="0d926-268">In doing so, pay careful attention to the ASE dependencies.</span></span> <span data-ttu-id="0d926-269">如果您封鎖任何相依性，ASE 會停止運作。</span><span class="sxs-lookup"><span data-stu-id="0d926-269">If you block any dependencies, the ASE stops working.</span></span>

<span data-ttu-id="0d926-270">NSG 可以透過 Azure 入口網站或 PowerShell 來設定。</span><span class="sxs-lookup"><span data-stu-id="0d926-270">NSGs can be configured through the Azure portal or via PowerShell.</span></span> <span data-ttu-id="0d926-271">這裡的資訊僅針對 Azure 入口網站說明。</span><span class="sxs-lookup"><span data-stu-id="0d926-271">The information here shows the Azure portal.</span></span> <span data-ttu-id="0d926-272">您會在入口網站中的 [網路] 底下，以最上層資源的形式建立及管理 NSG。</span><span class="sxs-lookup"><span data-stu-id="0d926-272">You create and manage NSGs in the portal as a top-level resource under **Networking**.</span></span>

<span data-ttu-id="0d926-273">將輸入和輸出需求納入考量時，NSG 看起來應類似此範例中顯示的 NSG。</span><span class="sxs-lookup"><span data-stu-id="0d926-273">When the inbound and outbound requirements are taken into account, the NSGs should look similar to the NSGs shown in this example.</span></span> <span data-ttu-id="0d926-274">VNet 位址範圍為 _192.168.250.0/16_，且 ASE 所在的子網路為 _192.168.251.128/25_。</span><span class="sxs-lookup"><span data-stu-id="0d926-274">The VNet address range is _192.168.250.0/16_, and the subnet that the ASE is in is _192.168.251.128/25_.</span></span>

<span data-ttu-id="0d926-275">讓 ASE 能夠運作的前兩個輸入需求顯示在此範例中清單的最上方。</span><span class="sxs-lookup"><span data-stu-id="0d926-275">The first two inbound requirements for the ASE to function are shown at the top of the list in this example.</span></span> <span data-ttu-id="0d926-276">它們能啟用 ASE 管理，並允許 ASE 和自己通訊。</span><span class="sxs-lookup"><span data-stu-id="0d926-276">They enable ASE management and allow the ASE to communicate with itself.</span></span> <span data-ttu-id="0d926-277">其他項目都是租用戶設定項目，而且可以管理對 ASE 裝載應用程式的網路存取。</span><span class="sxs-lookup"><span data-stu-id="0d926-277">The other entries are all tenant configurable and can govern network access to the ASE-hosted applications.</span></span> 

![輸入安全性規則][4]

<span data-ttu-id="0d926-279">預設規則可讓 VNet 中的 IP 與 ASE 子網路通訊。</span><span class="sxs-lookup"><span data-stu-id="0d926-279">A default rule enables the IPs in the VNet to talk to the ASE subnet.</span></span> <span data-ttu-id="0d926-280">另一個預設規則可讓負載平衡器 (也稱為公用 VIP) 和 ASE 通訊。</span><span class="sxs-lookup"><span data-stu-id="0d926-280">Another default rule enables the load balancer, also known as the public VIP, to communicate with the ASE.</span></span> <span data-ttu-id="0d926-281">您可以選取 [新增] 圖示旁邊的 [預設規則] 來查看預設規則。</span><span class="sxs-lookup"><span data-stu-id="0d926-281">To see the default rules, select **Default rules** next to the **Add** icon.</span></span> <span data-ttu-id="0d926-282">如果您在顯示的 NSG 規則後面加入拒絕其他任何內容的規則，便可以防止 VIP 和 ASE 之間產生流量。</span><span class="sxs-lookup"><span data-stu-id="0d926-282">If you put a deny everything else rule after the NSG rules shown, you prevent traffic between the VIP and the ASE.</span></span> <span data-ttu-id="0d926-283">若要防止來自 VNet 內部的流量，請新增您自己的規則來允許輸入。</span><span class="sxs-lookup"><span data-stu-id="0d926-283">To prevent traffic coming from inside the VNet, add your own rule to allow inbound.</span></span> <span data-ttu-id="0d926-284">使用來源等於 AzureLoadBalancer，目的地為 **Any**，以及 **\*** 的連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="0d926-284">Use a source equal to AzureLoadBalancer with a destination of **Any** and a port range of **\***.</span></span> <span data-ttu-id="0d926-285">由於 NSG 規則是套用至 ASE 子網路，因此不需要特別指定目的地。</span><span class="sxs-lookup"><span data-stu-id="0d926-285">Because the NSG rule is applied to the ASE subnet, you don't need to be specific in the destination.</span></span>

<span data-ttu-id="0d926-286">如果指派 IP 位址給應用程式，請確定維持開啟連接埠。</span><span class="sxs-lookup"><span data-stu-id="0d926-286">If you assigned an IP address to your app, make sure you keep the ports open.</span></span> <span data-ttu-id="0d926-287">若要查看連接埠，請選取 [App Service Environment] > [IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="0d926-287">To see the ports, select **App Service Environment** > **IP addresses**.</span></span>  

<span data-ttu-id="0d926-288">下列輸出規則中顯示的所有項目都是需要的項目，但不包含最後一個項目。</span><span class="sxs-lookup"><span data-stu-id="0d926-288">All the items shown in the following outbound rules are needed, except for the last item.</span></span> <span data-ttu-id="0d926-289">它們可啟用針對本文章之前所提到之 ASE 相依性的網路存取。</span><span class="sxs-lookup"><span data-stu-id="0d926-289">They enable network access to the ASE dependencies that were noted earlier in this article.</span></span> <span data-ttu-id="0d926-290">如果封鎖它們任何一項，ASE 會停止運作。</span><span class="sxs-lookup"><span data-stu-id="0d926-290">If you block any of them, your ASE stops working.</span></span> <span data-ttu-id="0d926-291">清單中的最後一個項目可讓 ASE 和 VNet 中的其他資源通訊。</span><span class="sxs-lookup"><span data-stu-id="0d926-291">The last item in the list enables your ASE to communicate with other resources in your VNet.</span></span>

![輸出安全性規則][5]

<span data-ttu-id="0d926-293">定義 NSG 之後，請將它們指派給 ASE 所在的子網路。</span><span class="sxs-lookup"><span data-stu-id="0d926-293">After your NSGs are defined, assign them to the subnet that your ASE is on.</span></span> <span data-ttu-id="0d926-294">如果您不記得 ASE VNet 或子網路，可以從 ASE 管理入口網站查看。</span><span class="sxs-lookup"><span data-stu-id="0d926-294">If you don’t remember the ASE VNet or subnet, you can see it from the ASE management portal.</span></span> <span data-ttu-id="0d926-295">若要將 NSG 指派給子網路，請移至子網路 UI 並選取 NSG。</span><span class="sxs-lookup"><span data-stu-id="0d926-295">To assign the NSG to your subnet, go to the subnet UI and select the NSG.</span></span>

## <a name="routes"></a><span data-ttu-id="0d926-296">路由</span><span class="sxs-lookup"><span data-stu-id="0d926-296">Routes</span></span> ##

<span data-ttu-id="0d926-297">路由最常在您使用 Azure ExpressRoute 設定 VNet 時造成問題。</span><span class="sxs-lookup"><span data-stu-id="0d926-297">Routes become problematic most commonly when you configure your VNet with Azure ExpressRoute.</span></span> <span data-ttu-id="0d926-298">VNet 中有三種類型的路由：</span><span class="sxs-lookup"><span data-stu-id="0d926-298">There are three types of routes in a VNet:</span></span>

-   <span data-ttu-id="0d926-299">系統路由</span><span class="sxs-lookup"><span data-stu-id="0d926-299">System routes</span></span>
-   <span data-ttu-id="0d926-300">BGP 路由</span><span class="sxs-lookup"><span data-stu-id="0d926-300">BGP routes</span></span>
-   <span data-ttu-id="0d926-301">使用者定義的路由 (UDR)</span><span class="sxs-lookup"><span data-stu-id="0d926-301">User-defined routes (UDRs)</span></span>

<span data-ttu-id="0d926-302">BGP 路由會覆寫系統路由。</span><span class="sxs-lookup"><span data-stu-id="0d926-302">BGP routes override system routes.</span></span> <span data-ttu-id="0d926-303">UDR 會覆寫 BGP 路由。</span><span class="sxs-lookup"><span data-stu-id="0d926-303">UDRs override BGP routes.</span></span> <span data-ttu-id="0d926-304">如需 Azure 虛擬網路中關於路由的詳細資訊，請參閱[使用者定義路由概觀][UDRs]。</span><span class="sxs-lookup"><span data-stu-id="0d926-304">For more information about routes in Azure virtual networks, see [User-defined routes overview][UDRs].</span></span>

<span data-ttu-id="0d926-305">ASE 用來管理系統的 Azure SQL 資料庫具備防火牆。</span><span class="sxs-lookup"><span data-stu-id="0d926-305">The Azure SQL database that the ASE uses to manage the system has a firewall.</span></span> <span data-ttu-id="0d926-306">它需要透過通訊由 ASE 公用 VIP 產生。</span><span class="sxs-lookup"><span data-stu-id="0d926-306">It requires communication to originate from the ASE public VIP.</span></span> <span data-ttu-id="0d926-307">從 ASE 連線到 SQL 資料庫的連線如果是透過 ExpressRoute 連線傳送及送出到其他 IP 位址，該連線將會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="0d926-307">Connections to the SQL database from the ASE will be denied if they are sent down the ExpressRoute connection and out another IP address.</span></span>

<span data-ttu-id="0d926-308">如果針對內送管理要求的回覆是透過 ExpressRoute 傳送，回覆位址將會和原始目的地不同。</span><span class="sxs-lookup"><span data-stu-id="0d926-308">If replies to incoming management requests are sent down the ExpressRoute, the reply address is different than the original destination.</span></span> <span data-ttu-id="0d926-309">這會中斷 TCP 通訊。</span><span class="sxs-lookup"><span data-stu-id="0d926-309">This mismatch breaks the TCP communication.</span></span>

<span data-ttu-id="0d926-310">若要在搭配 ExpressRoute 設定 VNet 時讓 ASE 能夠運作，最簡單的方式為：</span><span class="sxs-lookup"><span data-stu-id="0d926-310">For your ASE to work while your VNet is configured with an ExpressRoute, the easiest thing to do is:</span></span>

-   <span data-ttu-id="0d926-311">設定 ExpressRoute 來通告 _0.0.0.0/0_。</span><span class="sxs-lookup"><span data-stu-id="0d926-311">Configure ExpressRoute to advertise _0.0.0.0/0_.</span></span> <span data-ttu-id="0d926-312">根據預設，它會使用強制通道將所有輸出流量傳送至內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="0d926-312">By default, it force tunnels all outbound traffic on-premises.</span></span>
-   <span data-ttu-id="0d926-313">建立 UDR。</span><span class="sxs-lookup"><span data-stu-id="0d926-313">Create a UDR.</span></span> <span data-ttu-id="0d926-314">並以「0.0.0.0/0」的位址首碼及「網際網路」的下一個躍點類型，將它套用至包含 ASE 的子網路。</span><span class="sxs-lookup"><span data-stu-id="0d926-314">Apply it to the subnet that contains the ASE with an address prefix of _0.0.0.0/0_ and a next hop type of _Internet_.</span></span>

<span data-ttu-id="0d926-315">如果您做了這兩項變更，則 (來自 ASE 子網路) 將出發到網際網路的流量，將不會被強制經由 ExpressRoute 傳輸，並使 ASE 能夠運作。</span><span class="sxs-lookup"><span data-stu-id="0d926-315">If you make these two changes, internet-destined traffic that originates from the ASE subnet isn't forced down the ExpressRoute and the ASE works.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0d926-316">UDR 中定義的路由必須足夠明確，以優先於 ExpressRoute 組態所通告的任何路由。</span><span class="sxs-lookup"><span data-stu-id="0d926-316">The routes defined in a UDR must be specific enough to take precedence over any routes advertised by the ExpressRoute configuration.</span></span> <span data-ttu-id="0d926-317">前面的範例使用廣泛的 0.0.0.0/0 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="0d926-317">The preceding example uses the broad 0.0.0.0/0 address range.</span></span> <span data-ttu-id="0d926-318">因此有可能會不小心由使用更明確位址範圍的路由通告所覆寫。</span><span class="sxs-lookup"><span data-stu-id="0d926-318">It can potentially be accidentally overridden by route advertisements that use more specific address ranges.</span></span>
>
> <span data-ttu-id="0d926-319">針對從公用對等互連路徑至私人對等互連路徑的路由進行交叉通告的 ExpressRoute 設定，不支援 ASE。</span><span class="sxs-lookup"><span data-stu-id="0d926-319">ASEs aren't supported with ExpressRoute configurations that cross-advertise routes from the public-peering path to the private-peering path.</span></span> <span data-ttu-id="0d926-320">已設定公用對等互連的 ExpressRoute 設定，會收到來自 Microsoft 的路由通告。</span><span class="sxs-lookup"><span data-stu-id="0d926-320">ExpressRoute configurations with public peering configured receive route advertisements from Microsoft.</span></span> <span data-ttu-id="0d926-321">通告中會包含一大組 Microsoft Azure IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="0d926-321">The advertisements contain a large set of Microsoft Azure IP address ranges.</span></span> <span data-ttu-id="0d926-322">如果位址範圍在私人對等互連路徑上交叉通告，來自 ASE 子網路的所有輸出網路封包都會使用強制通道傳送至客戶的內部部署網路基礎結構。</span><span class="sxs-lookup"><span data-stu-id="0d926-322">If the address ranges are cross-advertised on the private-peering path, all outbound network packets from the ASE's subnet are force tunneled to a customer's on-premises network infrastructure.</span></span> <span data-ttu-id="0d926-323">ASE 目前不支援這個網路流量。</span><span class="sxs-lookup"><span data-stu-id="0d926-323">This network flow is currently not supported with ASEs.</span></span> <span data-ttu-id="0d926-324">此問題的一個解決方案是停止從公用對等互連路徑至私人對等互連路徑的交叉通告路由。</span><span class="sxs-lookup"><span data-stu-id="0d926-324">One solution to this problem is to stop cross-advertising routes from the public-peering path to the private-peering path.</span></span>

<span data-ttu-id="0d926-325">若要建立 UDR，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0d926-325">To create a UDR, follow these steps:</span></span>

1. <span data-ttu-id="0d926-326">移至 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0d926-326">Go to the Azure portal.</span></span> <span data-ttu-id="0d926-327">選取 [網路] > [路由表]。</span><span class="sxs-lookup"><span data-stu-id="0d926-327">Select **Networking** > **Route Tables**.</span></span>

2. <span data-ttu-id="0d926-328">在和您 VNet 相同的區域內建立一個新的路由表。</span><span class="sxs-lookup"><span data-stu-id="0d926-328">Create a new route table in the same region as your VNet.</span></span>

3. <span data-ttu-id="0d926-329">從您的路由表 UI 內，選取 [路由] > [新增]。</span><span class="sxs-lookup"><span data-stu-id="0d926-329">From within your route table UI, select **Routes** > **Add**.</span></span>

4. <span data-ttu-id="0d926-330">將 [下一個躍點類型] 設為 [網際網路]，將 [位址首碼] 設為 **0.0.0.0/0**。</span><span class="sxs-lookup"><span data-stu-id="0d926-330">Set the **Next hop type** to **Internet** and the **Address prefix** to **0.0.0.0/0**.</span></span> <span data-ttu-id="0d926-331">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="0d926-331">Select **Save**.</span></span>

    <span data-ttu-id="0d926-332">您就會看到類似以下的畫面：</span><span class="sxs-lookup"><span data-stu-id="0d926-332">You then see something like the following:</span></span>

    ![功能性路由][6]

5. <span data-ttu-id="0d926-334">建立新的路由表之後，請移至包含您 ASE 的子網路。</span><span class="sxs-lookup"><span data-stu-id="0d926-334">After you create the new route table, go to the subnet that contains your ASE.</span></span> <span data-ttu-id="0d926-335">從在入口網站取得的清單中選取您的路由表。</span><span class="sxs-lookup"><span data-stu-id="0d926-335">Select your route table from the list in the portal.</span></span> <span data-ttu-id="0d926-336">儲存變更之後，應該就會看見 NSG 和路由已註明了您的子網路。</span><span class="sxs-lookup"><span data-stu-id="0d926-336">After you save the change, you should then see the NSGs and routes noted with your subnet.</span></span>

    ![NSG 和路由][7]

### <a name="deploy-into-existing-azure-virtual-networks-that-are-integrated-with-expressroute"></a><span data-ttu-id="0d926-338">部署到與 ExpressRoute 整合的現有 Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="0d926-338">Deploy into existing Azure virtual networks that are integrated with ExpressRoute</span></span> ###

<span data-ttu-id="0d926-339">若要將 ASE 部署到與 ExpressRoute 整合的 VNet，請預先設定您想要部署 ASE 的子網路。</span><span class="sxs-lookup"><span data-stu-id="0d926-339">To deploy your ASE into a VNet that's integrated with ExpressRoute, preconfigure the subnet where you want the ASE deployed.</span></span> <span data-ttu-id="0d926-340">然後使用 Resource Manager 範本來部署。</span><span class="sxs-lookup"><span data-stu-id="0d926-340">Then use a Resource Manager template to deploy it.</span></span> <span data-ttu-id="0d926-341">在已設定 ExpressRoute 的 VNet 中建立 ASE：</span><span class="sxs-lookup"><span data-stu-id="0d926-341">To create an ASE in a VNet that already has ExpressRoute configured:</span></span>

- <span data-ttu-id="0d926-342">建立子網路以裝載 ASE。</span><span class="sxs-lookup"><span data-stu-id="0d926-342">Create a subnet to host the ASE.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0d926-343">除了 ASE 以外，子網路中可能沒有其他項目。</span><span class="sxs-lookup"><span data-stu-id="0d926-343">Nothing else can be in the subnet but the ASE.</span></span> <span data-ttu-id="0d926-344">請務必選擇預留未來成長空間的位址空間。</span><span class="sxs-lookup"><span data-stu-id="0d926-344">Be sure to choose an address space that allows for future growth.</span></span> <span data-ttu-id="0d926-345">您之後無法變更此設定。</span><span class="sxs-lookup"><span data-stu-id="0d926-345">You can't change this setting later.</span></span> <span data-ttu-id="0d926-346">我們建議使用包含 128 個位址的 `/25` 大小。</span><span class="sxs-lookup"><span data-stu-id="0d926-346">We recommend a size of `/25` with 128 addresses.</span></span>

- <span data-ttu-id="0d926-347">依照之前的描述建立 UDR (例如，路由表)，並在子網路上加以設定。</span><span class="sxs-lookup"><span data-stu-id="0d926-347">Create UDRs (for example, route tables) as described earlier, and set that on the subnet.</span></span>
- <span data-ttu-id="0d926-348">依照[使用 Resource Manager 範本建立 ASE][MakeASEfromTemplate] 中的描述，使用 Resource Manager 範本建立 ASE。</span><span class="sxs-lookup"><span data-stu-id="0d926-348">Create the ASE by using a Resource Manager template as described in [Create an ASE by using a Resource Manager template][MakeASEfromTemplate].</span></span>

<!--Image references-->
[1]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow.png
[2]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow2.png
[3]: ./media/network_considerations_with_an_app_service_environment/networkase-ipaddresses.png
[4]: ./media/network_considerations_with_an_app_service_environment/networkase-inboundnsg.png
[5]: ./media/network_considerations_with_an_app_service_environment/networkase-outboundnsg.png
[6]: ./media/network_considerations_with_an_app_service_environment/networkase-udr.png
[7]: ./media/network_considerations_with_an_app_service_environment/networkase-subnet.png

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ASEManagement]: ./management-addresses.md
