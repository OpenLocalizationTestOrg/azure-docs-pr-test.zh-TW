---
title: "負載平衡器自訂探查和監視健全狀況狀態 | Microsoft Docs"
description: "了解如何使用 Azure 負載平衡器的自訂探查，來監視負載平衡器後方的執行個體"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 46b152c5-6a27-4bfc-bea3-05de9ce06a57
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: cab028fed58d544a56f2f6b12b72364c7baf4d86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="understand-load-balancer-probes"></a><span data-ttu-id="a19c9-103">了解負載平衡器探查</span><span class="sxs-lookup"><span data-stu-id="a19c9-103">Understand load balancer probes</span></span>

<span data-ttu-id="a19c9-104">Azure 負載平衡器提供了使用探查來監視伺服器執行個體健全狀況的功能。</span><span class="sxs-lookup"><span data-stu-id="a19c9-104">Azure Load Balancer offers the capability to monitor the health of server instances by using probes.</span></span> <span data-ttu-id="a19c9-105">當探查無法回應時，負載平衡器會停止傳送新的連線至狀況不良的執行個體。</span><span class="sxs-lookup"><span data-stu-id="a19c9-105">When a probe fails to respond, Load Balancer stops sending new connections to the unhealthy instance.</span></span> <span data-ttu-id="a19c9-106">現有的連線不會受到影響，而新的連線會傳送到狀況良好的執行個體。</span><span class="sxs-lookup"><span data-stu-id="a19c9-106">The existing connections are not affected, and new connections are sent to healthy instances.</span></span>

<span data-ttu-id="a19c9-107">雲端服務角色 (背景工作角色和 Web 角色) 會使用客體代理程式進行探查監視。</span><span class="sxs-lookup"><span data-stu-id="a19c9-107">Cloud service roles (worker roles and web roles) use a guest agent for probe monitoring.</span></span> <span data-ttu-id="a19c9-108">當您在負載平衡器後方使用虛擬機器時，必須設定 TCP 或 HTTP 自訂探查。</span><span class="sxs-lookup"><span data-stu-id="a19c9-108">TCP or HTTP custom probes must be configured when you use virtual machines behind Load Balancer.</span></span>

## <a name="understand-probe-count-and-timeout"></a><span data-ttu-id="a19c9-109">了解探查計數及逾時</span><span class="sxs-lookup"><span data-stu-id="a19c9-109">Understand probe count and timeout</span></span>

<span data-ttu-id="a19c9-110">探查行為取決於︰</span><span class="sxs-lookup"><span data-stu-id="a19c9-110">Probe behavior depends on:</span></span>

* <span data-ttu-id="a19c9-111">允許執行個體標示為已啟動的成功探查數目。</span><span class="sxs-lookup"><span data-stu-id="a19c9-111">The number of successful probes that allow an instance to be labeled as up.</span></span>
* <span data-ttu-id="a19c9-112">導致執行個體標示為已關閉的失敗探查數目。</span><span class="sxs-lookup"><span data-stu-id="a19c9-112">The number of failed probes that cause an instance to be labeled as down.</span></span>

<span data-ttu-id="a19c9-113">在 SuccessFailCount 中設定的逾時和頻率值會決定執行個體是否確定為執行中或非執行中。</span><span class="sxs-lookup"><span data-stu-id="a19c9-113">The timeout and frequency value set in  SuccessFailCount determine whether an instance is confirmed to be running or not running.</span></span> <span data-ttu-id="a19c9-114">在 Azure 入口網站中，逾時設定為頻率值的兩倍。</span><span class="sxs-lookup"><span data-stu-id="a19c9-114">In the Azure portal, the timeout is set to two times the value of the frequency.</span></span>

<span data-ttu-id="a19c9-115">端點 (也就是負載平衡集) 的所有負載平衡執行個體的探查設定必須相同。</span><span class="sxs-lookup"><span data-stu-id="a19c9-115">The probe configuration of all load-balanced instances for an endpoint (that is, a load-balanced set) must be the same.</span></span> <span data-ttu-id="a19c9-116">這表示針對位在相同託管服務特定端點組合的各個角色執行個體或虛擬機器，您不能有不同的探查設定。</span><span class="sxs-lookup"><span data-stu-id="a19c9-116">This means you cannot have a different probe configuration for each role instance or virtual machine in the same hosted service for a particular endpoint combination.</span></span> <span data-ttu-id="a19c9-117">例如，每個執行個體必須具有相同的本機連接埠和逾時。</span><span class="sxs-lookup"><span data-stu-id="a19c9-117">For example, each instance must have identical local ports and timeouts.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a19c9-118">負載平衡器探查會使用 IP 位址 168.63.129.16。</span><span class="sxs-lookup"><span data-stu-id="a19c9-118">A Load Balancer probe uses the IP address 168.63.129.16.</span></span> <span data-ttu-id="a19c9-119">這個公用 IP 位址可促進自備 IP Azure 虛擬網路案例中內部平台資源的通訊。</span><span class="sxs-lookup"><span data-stu-id="a19c9-119">This public IP address facilitates communication to internal platform resources for the bring-your-own-IP Azure Virtual Network scenario.</span></span> <span data-ttu-id="a19c9-120">虛擬公用 IP 位址 168.63.129.16 會使用於所有區域中，且不會變更。</span><span class="sxs-lookup"><span data-stu-id="a19c9-120">The virtual public IP address 168.63.129.16 is used in all regions and will not change.</span></span> <span data-ttu-id="a19c9-121">建議您在任何本機防火牆原則中允許此 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a19c9-121">We recommend that you allow this IP address in any local firewall policies.</span></span> <span data-ttu-id="a19c9-122">它不應被視為安全性風險，因為只有內部 Azure 平台可以從該位址取得訊息來源。</span><span class="sxs-lookup"><span data-stu-id="a19c9-122">It should not be considered a security risk because only the internal Azure platform can source a message from that address.</span></span> <span data-ttu-id="a19c9-123">如果您不這麼做，各種不同的案例中將會有非預期的行為，例如設定相同的 IP 位址範圍 168.63.129.16 和具有重複的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a19c9-123">If you do not do this, there will be unexpected behavior in a variety of scenarios like configuring the same IP address range of 168.63.129.16 and having duplicated IP addresses.</span></span>

## <a name="learn-about-the-types-of-probes"></a><span data-ttu-id="a19c9-124">深入了解探查類型</span><span class="sxs-lookup"><span data-stu-id="a19c9-124">Learn about the types of probes</span></span>

### <a name="guest-agent-probe"></a><span data-ttu-id="a19c9-125">客體代理程式探查</span><span class="sxs-lookup"><span data-stu-id="a19c9-125">Guest agent probe</span></span>

<span data-ttu-id="a19c9-126">此探查僅供 Azure 雲端服務使用。</span><span class="sxs-lookup"><span data-stu-id="a19c9-126">This probe is available for Azure Cloud Services only.</span></span> <span data-ttu-id="a19c9-127">只有在執行個體處於 [就緒] 狀態 (也就是不在其他狀態中，例如 [忙碌]、[回收中] 或 [停止中]) 時，負載平衡器才會利用虛擬機器內的客體代理程式、然後接聽並以「HTTP 200 確定」做為回應。</span><span class="sxs-lookup"><span data-stu-id="a19c9-127">Load Balancer utilizes the guest agent inside the virtual machine, and then listens and responds with an HTTP 200 OK response only when the instance is in the Ready state (that is, not in another state such as Busy, Recycling, or Stopping).</span></span>

<span data-ttu-id="a19c9-128">如需詳細資訊，請查看[設定適用於健全狀況探查的服務定義檔案 (csdef)](https://msdn.microsoft.com/library/azure/ee758710.aspx) 或[開始為雲端服務建立網際網路面向的負載平衡器](load-balancer-get-started-internet-classic-cloud.md#check-load-balancer-health-status-for-cloud-services)。</span><span class="sxs-lookup"><span data-stu-id="a19c9-128">For more information, see [Configuring the service definition file (csdef) for health probes](https://msdn.microsoft.com/library/azure/ee758710.aspx) or [Get started creating an Internet-facing load balancer for cloud services](load-balancer-get-started-internet-classic-cloud.md#check-load-balancer-health-status-for-cloud-services).</span></span>

### <a name="what-makes-a-guest-agent-probe-mark-an-instance-as-unhealthy"></a><span data-ttu-id="a19c9-129">什麼原因會讓客體代理程式探查將執行個體標示為狀況不良？</span><span class="sxs-lookup"><span data-stu-id="a19c9-129">What makes a guest agent probe mark an instance as unhealthy?</span></span>

<span data-ttu-id="a19c9-130">如果客體代理程式無法以「HTTP 200 確定」回應，則負載平衡器會將執行個體標示為沒有回應，並停止傳送流量到該執行個體。</span><span class="sxs-lookup"><span data-stu-id="a19c9-130">If the guest agent fails to respond with HTTP 200 OK, the load balancer marks the instance as unresponsive and stops sending traffic to that instance.</span></span> <span data-ttu-id="a19c9-131">負載平衡器會繼續 ping 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a19c9-131">The load balancer continues to ping the instance.</span></span> <span data-ttu-id="a19c9-132">如果客體代理程式以 HTTP 200 回應，則負載平衡器會再次傳送流量到該執行個體。</span><span class="sxs-lookup"><span data-stu-id="a19c9-132">If the guest agent responds with an HTTP 200, the load balancer sends traffic to that instance again.</span></span>

<span data-ttu-id="a19c9-133">使用 Web 角色時，網站程式碼通常會在不受 Azure 網狀架構或客體代理程式監視的 w3wp.exe 中執行。</span><span class="sxs-lookup"><span data-stu-id="a19c9-133">When you use a web role, the website code typically runs in w3wp.exe, which is not monitored by the Azure fabric or guest agent.</span></span> <span data-ttu-id="a19c9-134">這表示 w3wp.exe 中的失敗 (例如，HTTP 500 回應) 不會向客體代理程式回報，而且負載平衡器不會將該執行個體退出循環。</span><span class="sxs-lookup"><span data-stu-id="a19c9-134">This means that failures in w3wp.exe (for example, HTTP 500 responses) will not be reported to the guest agent, and the load balancer will not take that instance out of rotation.</span></span>

### <a name="http-custom-probe"></a><span data-ttu-id="a19c9-135">HTTP 自訂探查</span><span class="sxs-lookup"><span data-stu-id="a19c9-135">HTTP custom probe</span></span>

<span data-ttu-id="a19c9-136">自訂 HTTP 負載平衡器探查會覆寫預設客體代理程式探查，這代表您可以建立自己的自訂邏輯來判斷角色執行個體的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="a19c9-136">The custom HTTP Load Balancer probe overrides the default guest agent probe, which means that you can create your own custom logic to determine the health of the role instance.</span></span> <span data-ttu-id="a19c9-137">根據預設，負載平衡器會每隔 15 秒探查您的端點。</span><span class="sxs-lookup"><span data-stu-id="a19c9-137">The load balancer probes your endpoint every 15 seconds, by default.</span></span> <span data-ttu-id="a19c9-138">如果執行個體在逾時期限 (預設為 31 秒) 內以 HTTP 200 回應，它就會被視為處於負載平衡器循環中。</span><span class="sxs-lookup"><span data-stu-id="a19c9-138">The instance is considered to be in the load balancer rotation if it responds with an HTTP 200 within the timeout period (31 seconds by default).</span></span>

<span data-ttu-id="a19c9-139">這很適合在您想要實作自己的邏輯，以從負載平衡器循環中移除執行個體時使用。</span><span class="sxs-lookup"><span data-stu-id="a19c9-139">This can be useful if you want to implement your own logic to remove instances from load balancer rotation.</span></span> <span data-ttu-id="a19c9-140">例如，如果執行個體超過 90% CPU，並傳回非 200 狀態，您可以決定移除執行個體。</span><span class="sxs-lookup"><span data-stu-id="a19c9-140">For example, you could decide to remove an instance if it is above 90% CPU and returns a non-200 status.</span></span> <span data-ttu-id="a19c9-141">如果您有使用 w3wp.exe 的 Web 角色，這也表示您能夠自動監視您的網站，因為網站程式碼中的錯誤會將非 200 狀態傳回給負載平衡器探查。</span><span class="sxs-lookup"><span data-stu-id="a19c9-141">If you have web roles that use w3wp.exe, this also means you get automatic monitoring of your website, because failures in your website code will return a non-200 status to the load balancer probe.</span></span>

> [!NOTE]
> <span data-ttu-id="a19c9-142">HTTP 自訂探查僅支援相對路徑和 HTTP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="a19c9-142">The HTTP custom probe supports relative paths and HTTP protocol only.</span></span> <span data-ttu-id="a19c9-143">不支援 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="a19c9-143">HTTPS is not supported.</span></span>

### <a name="what-makes-an-http-custom-probe-mark-an-instance-as-unhealthy"></a><span data-ttu-id="a19c9-144">什麼原因會讓 HTTP 自訂探查將執行個體標示為狀況不良？</span><span class="sxs-lookup"><span data-stu-id="a19c9-144">What makes an HTTP custom probe mark an instance as unhealthy?</span></span>

* <span data-ttu-id="a19c9-145">HTTP 應用程式傳回 200 以外的 HTTP 回應碼 (例如，403、404 或 500)。</span><span class="sxs-lookup"><span data-stu-id="a19c9-145">The HTTP application returns an HTTP response code other than 200 (for example, 403, 404, or 500).</span></span> <span data-ttu-id="a19c9-146">這是應用程式執行個體應該立即被帶離服務的正面回答。</span><span class="sxs-lookup"><span data-stu-id="a19c9-146">This is a positive acknowledgment that the application instance should be taken out of service right away.</span></span>
* <span data-ttu-id="a19c9-147">HTTP 伺服器在逾時期限之後完全沒有回應。</span><span class="sxs-lookup"><span data-stu-id="a19c9-147">The HTTP server does not respond at all after the timeout period.</span></span> <span data-ttu-id="a19c9-148">根據設定的逾時值，這可能表示在探查標示為非執行中之前 (也就是說，在傳送 SuccessFailCount 探查之前)，多個探查要求並未獲得回應。</span><span class="sxs-lookup"><span data-stu-id="a19c9-148">Depending on the timeout value that is set, this might mean that multiple probe requests go unanswered before the probe gets marked as not running (that is, before SuccessFailCount probes are sent).</span></span>
* <span data-ttu-id="a19c9-149">伺服器會透過 TCP 重設關閉連線。</span><span class="sxs-lookup"><span data-stu-id="a19c9-149">The server closes the connection via a TCP reset.</span></span>

### <a name="tcp-custom-probe"></a><span data-ttu-id="a19c9-150">TCP 自訂探查</span><span class="sxs-lookup"><span data-stu-id="a19c9-150">TCP custom probe</span></span>

<span data-ttu-id="a19c9-151">TCP 探查透過利用定義的連接埠執行三向信號交換來初始化連線。</span><span class="sxs-lookup"><span data-stu-id="a19c9-151">TCP probes initiate a connection by performing a three-way handshake with the defined port.</span></span>

### <a name="what-makes-a-tcp-custom-probe-mark-an-instance-as-unhealthy"></a><span data-ttu-id="a19c9-152">什麼原因會讓 TCP 自訂探查將執行個體標示為狀況不良？</span><span class="sxs-lookup"><span data-stu-id="a19c9-152">What makes a TCP custom probe mark an instance as unhealthy?</span></span>

* <span data-ttu-id="a19c9-153">TCP 伺服器在逾時期限之後完全沒有回應。</span><span class="sxs-lookup"><span data-stu-id="a19c9-153">The TCP server does not respond at all after the timeout period.</span></span> <span data-ttu-id="a19c9-154">當探查標示為非執行中時，取決於失敗探查的數目，在探查標示為非執行中之前，這些要求設定為未獲得回應。</span><span class="sxs-lookup"><span data-stu-id="a19c9-154">When the probe is marked as not running depends on the number of failed probe requests that were configured to go unanswered before marking the probe as not running.</span></span>
* <span data-ttu-id="a19c9-155">探查會從角色執行個體接收 TCP 重設。</span><span class="sxs-lookup"><span data-stu-id="a19c9-155">The probe receives a TCP reset from the role instance.</span></span>

<span data-ttu-id="a19c9-156">如需有關設定 HTTP 健全狀況探查或 TCP 探查的詳細資訊，請參閱 [開始使用 PowerShell 在資源管理員中建立網際網路對向負載平衡器](load-balancer-get-started-internet-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="a19c9-156">For more information about configuring an HTTP health probe or a TCP probe, see [Get started creating an Internet-facing load balancer in Resource Manager using PowerShell](load-balancer-get-started-internet-arm-ps.md).</span></span>

## <a name="add-healthy-instances-back-into-load-balancer-rotation"></a><span data-ttu-id="a19c9-157">將狀況良好的執行個體重新加入負載平衡器循環</span><span class="sxs-lookup"><span data-stu-id="a19c9-157">Add healthy instances back into load balancer rotation</span></span>

<span data-ttu-id="a19c9-158">TCP 和 HTTP 探查於下列狀況時會視為狀況良好，並將角色執行個體標示為狀況良好：</span><span class="sxs-lookup"><span data-stu-id="a19c9-158">TCP and HTTP probes are considered healthy and mark the role instance as healthy when:</span></span>

* <span data-ttu-id="a19c9-159">負載平衡器在 VM 第一次開機時會取得正面探查。</span><span class="sxs-lookup"><span data-stu-id="a19c9-159">The load balancer gets a positive probe the first time the VM boots.</span></span>
* <span data-ttu-id="a19c9-160">SuccessFailCount 的數目 (如上所述) 可定義將角色執行個體標示為狀況良好所需的成功探查值。</span><span class="sxs-lookup"><span data-stu-id="a19c9-160">The number SuccessFailCount (described earlier) defines the value of successful probes that are required to mark the role instance as healthy.</span></span> <span data-ttu-id="a19c9-161">如果已移除角色執行個體，成功且連續的探查數目必須大於或等於 SuccessFailCount 的值才能將角色執行個體標示為執行中。</span><span class="sxs-lookup"><span data-stu-id="a19c9-161">If a role instance was removed, the number of successful, successive probes must equal or exceed the value of SuccessFailCount to mark the role instance as running.</span></span>

> [!NOTE]
> <span data-ttu-id="a19c9-162">如果角色執行個體的健全狀況出現變動，負載平衡器會先等候較長的時間，才將角色執行個體重新放回狀況良好的狀態。</span><span class="sxs-lookup"><span data-stu-id="a19c9-162">If the health of a role instance is fluctuating, the load balancer waits longer before putting the role instance back in the healthy state.</span></span> <span data-ttu-id="a19c9-163">這是透過原則保護使用者和基礎結構來完成。</span><span class="sxs-lookup"><span data-stu-id="a19c9-163">This is done via policy to protect the user and the infrastructure.</span></span>

## <a name="use-log-analytics-for-load-balancer"></a><span data-ttu-id="a19c9-164">使用負載平衡器的記錄分析</span><span class="sxs-lookup"><span data-stu-id="a19c9-164">Use log analytics for Load Balancer</span></span>

<span data-ttu-id="a19c9-165">您可以使用 [負載平衡器的記錄分析](load-balancer-monitor-log.md) 來檢查探查健全狀況狀態和探查計數。</span><span class="sxs-lookup"><span data-stu-id="a19c9-165">You can use [log analytics for Load Balancer](load-balancer-monitor-log.md) to check on the probe health status and probe count.</span></span> <span data-ttu-id="a19c9-166">記錄可以與 Power BI 或 Azure Operation Insights 搭配使用，以提供負載平衡器健康狀態。</span><span class="sxs-lookup"><span data-stu-id="a19c9-166">Logging can be used with Power BI or Azure Operational Insights to provide statistics about Load Balancer health status.</span></span>
