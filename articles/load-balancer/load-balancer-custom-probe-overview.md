---
title: "aaaLoad 平衡器自訂探查和監視的健全狀況狀態 |Microsoft 文件"
description: "了解如何自訂 toouse 探查 Azure 負載平衡器負載平衡器後方的 toomonitor 執行個體"
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
ms.openlocfilehash: 3dfcfcd2d5cffa58b160cb38d63acffbd997d452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-load-balancer-probes"></a><span data-ttu-id="51bd2-103">了解負載平衡器探查</span><span class="sxs-lookup"><span data-stu-id="51bd2-103">Understand load balancer probes</span></span>

<span data-ttu-id="51bd2-104">Azure 負載平衡器使用探查提供 hello 功能 toomonitor hello 健全狀況的伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="51bd2-104">Azure Load Balancer offers hello capability toomonitor hello health of server instances by using probes.</span></span> <span data-ttu-id="51bd2-105">當探查失敗 toorespond 時，負載平衡器會停止傳送新連線 toohello 狀況不良的執行個體。</span><span class="sxs-lookup"><span data-stu-id="51bd2-105">When a probe fails toorespond, Load Balancer stops sending new connections toohello unhealthy instance.</span></span> <span data-ttu-id="51bd2-106">hello 現有的連接不受影響，還新的連線傳送 toohealthy 執行個體。</span><span class="sxs-lookup"><span data-stu-id="51bd2-106">hello existing connections are not affected, and new connections are sent toohealthy instances.</span></span>

<span data-ttu-id="51bd2-107">雲端服務角色 (背景工作角色和 Web 角色) 會使用客體代理程式進行探查監視。</span><span class="sxs-lookup"><span data-stu-id="51bd2-107">Cloud service roles (worker roles and web roles) use a guest agent for probe monitoring.</span></span> <span data-ttu-id="51bd2-108">當您在負載平衡器後方使用虛擬機器時，必須設定 TCP 或 HTTP 自訂探查。</span><span class="sxs-lookup"><span data-stu-id="51bd2-108">TCP or HTTP custom probes must be configured when you use virtual machines behind Load Balancer.</span></span>

## <a name="understand-probe-count-and-timeout"></a><span data-ttu-id="51bd2-109">了解探查計數及逾時</span><span class="sxs-lookup"><span data-stu-id="51bd2-109">Understand probe count and timeout</span></span>

<span data-ttu-id="51bd2-110">探查行為取決於︰</span><span class="sxs-lookup"><span data-stu-id="51bd2-110">Probe behavior depends on:</span></span>

* <span data-ttu-id="51bd2-111">hello 成功允許標示為執行個體 toobe 的探查數目。</span><span class="sxs-lookup"><span data-stu-id="51bd2-111">hello number of successful probes that allow an instance toobe labeled as up.</span></span>
* <span data-ttu-id="51bd2-112">hello 會標示為停機的執行個體 toobe 造成的失敗探查數目。</span><span class="sxs-lookup"><span data-stu-id="51bd2-112">hello number of failed probes that cause an instance toobe labeled as down.</span></span>

<span data-ttu-id="51bd2-113">hello 逾時和頻率的設定值 SuccessFailCount 判斷執行個體是否已確認的 toobe 執行或未執行。</span><span class="sxs-lookup"><span data-stu-id="51bd2-113">hello timeout and frequency value set in  SuccessFailCount determine whether an instance is confirmed toobe running or not running.</span></span> <span data-ttu-id="51bd2-114">在 hello Azure 入口網站，設定 tootwo hello 值倍 hello 頻率的 hello 逾時。</span><span class="sxs-lookup"><span data-stu-id="51bd2-114">In hello Azure portal, hello timeout is set tootwo times hello value of hello frequency.</span></span>

<span data-ttu-id="51bd2-115">hello 探查設定所有負載平衡的執行個體的端點 （也就是負載平衡集） 必須是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="51bd2-115">hello probe configuration of all load-balanced instances for an endpoint (that is, a load-balanced set) must be hello same.</span></span> <span data-ttu-id="51bd2-116">這表示您不能有不同的探查設定每個角色執行個體或虛擬機器在 hello 相同託管之特定端點組合的服務。</span><span class="sxs-lookup"><span data-stu-id="51bd2-116">This means you cannot have a different probe configuration for each role instance or virtual machine in hello same hosted service for a particular endpoint combination.</span></span> <span data-ttu-id="51bd2-117">例如，每個執行個體必須具有相同的本機連接埠和逾時。</span><span class="sxs-lookup"><span data-stu-id="51bd2-117">For example, each instance must have identical local ports and timeouts.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51bd2-118">負載平衡器探查使用 hello IP 位址 168.63.129.16。</span><span class="sxs-lookup"><span data-stu-id="51bd2-118">A Load Balancer probe uses hello IP address 168.63.129.16.</span></span> <span data-ttu-id="51bd2-119">這個公用 IP 位址可加快 hello 帶您-擁有-IP Azure 虛擬網路案例的通訊 toointernal 平台資源。</span><span class="sxs-lookup"><span data-stu-id="51bd2-119">This public IP address facilitates communication toointernal platform resources for hello bring-your-own-IP Azure Virtual Network scenario.</span></span> <span data-ttu-id="51bd2-120">hello 虛擬公用 IP 位址 168.63.129.16 用於所有區域中，不會變更。</span><span class="sxs-lookup"><span data-stu-id="51bd2-120">hello virtual public IP address 168.63.129.16 is used in all regions and will not change.</span></span> <span data-ttu-id="51bd2-121">建議您在任何本機防火牆原則中允許此 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="51bd2-121">We recommend that you allow this IP address in any local firewall policies.</span></span> <span data-ttu-id="51bd2-122">它不應視為安全性風險因為只有 hello 內部 Azure 平台可以來源來自該位址的訊息。</span><span class="sxs-lookup"><span data-stu-id="51bd2-122">It should not be considered a security risk because only hello internal Azure platform can source a message from that address.</span></span> <span data-ttu-id="51bd2-123">如果不這麼做，會有未預期的行為中的各種案例，例如設定 hello 168.63.129.16 和具有重複的 IP 位址相同的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="51bd2-123">If you do not do this, there will be unexpected behavior in a variety of scenarios like configuring hello same IP address range of 168.63.129.16 and having duplicated IP addresses.</span></span>

## <a name="learn-about-hello-types-of-probes"></a><span data-ttu-id="51bd2-124">深入了解探查的 hello 類型</span><span class="sxs-lookup"><span data-stu-id="51bd2-124">Learn about hello types of probes</span></span>

### <a name="guest-agent-probe"></a><span data-ttu-id="51bd2-125">客體代理程式探查</span><span class="sxs-lookup"><span data-stu-id="51bd2-125">Guest agent probe</span></span>

<span data-ttu-id="51bd2-126">此探查僅供 Azure 雲端服務使用。</span><span class="sxs-lookup"><span data-stu-id="51bd2-126">This probe is available for Azure Cloud Services only.</span></span> <span data-ttu-id="51bd2-127">負載平衡器會利用 hello hello 虛擬機器，內部的客體代理程式然後會接聽並回應 HTTP 200 OK 回應時，才 hello hello 就緒狀態中目前的執行個體 （也就是在另一個狀態例如忙碌、 回收、 或停止）。</span><span class="sxs-lookup"><span data-stu-id="51bd2-127">Load Balancer utilizes hello guest agent inside hello virtual machine, and then listens and responds with an HTTP 200 OK response only when hello instance is in hello Ready state (that is, not in another state such as Busy, Recycling, or Stopping).</span></span>

<span data-ttu-id="51bd2-128">如需詳細資訊，請參閱[設定 hello 服務定義檔 (csdef) 健全狀況探查](https://msdn.microsoft.com/library/azure/ee758710.aspx)或[開始建立雲端服務的網際網路對向負載平衡器](load-balancer-get-started-internet-classic-cloud.md#check-load-balancer-health-status-for-cloud-services)。</span><span class="sxs-lookup"><span data-stu-id="51bd2-128">For more information, see [Configuring hello service definition file (csdef) for health probes](https://msdn.microsoft.com/library/azure/ee758710.aspx) or [Get started creating an Internet-facing load balancer for cloud services](load-balancer-get-started-internet-classic-cloud.md#check-load-balancer-health-status-for-cloud-services).</span></span>

### <a name="what-makes-a-guest-agent-probe-mark-an-instance-as-unhealthy"></a><span data-ttu-id="51bd2-129">什麼原因會讓客體代理程式探查將執行個體標示為狀況不良？</span><span class="sxs-lookup"><span data-stu-id="51bd2-129">What makes a guest agent probe mark an instance as unhealthy?</span></span>

<span data-ttu-id="51bd2-130">如果 hello 客體代理程式無法與 HTTP 200 「 確定 toorespond，hello 負載平衡器標記 hello 為沒有回應的執行個體和停止傳送流量 toothat 執行個體。</span><span class="sxs-lookup"><span data-stu-id="51bd2-130">If hello guest agent fails toorespond with HTTP 200 OK, hello load balancer marks hello instance as unresponsive and stops sending traffic toothat instance.</span></span> <span data-ttu-id="51bd2-131">hello 負載平衡器會繼續 tooping hello 執行個體。</span><span class="sxs-lookup"><span data-stu-id="51bd2-131">hello load balancer continues tooping hello instance.</span></span> <span data-ttu-id="51bd2-132">如果 hello 客體代理程式回應 HTTP 200，hello 負載平衡器會再次傳送流量 toothat 執行個體。</span><span class="sxs-lookup"><span data-stu-id="51bd2-132">If hello guest agent responds with an HTTP 200, hello load balancer sends traffic toothat instance again.</span></span>

<span data-ttu-id="51bd2-133">當您使用 web 角色時，不會監視 hello Azure 網狀架構或客體代理程式的 w3wp.exe 中通常執行 hello 網站程式碼。</span><span class="sxs-lookup"><span data-stu-id="51bd2-133">When you use a web role, hello website code typically runs in w3wp.exe, which is not monitored by hello Azure fabric or guest agent.</span></span> <span data-ttu-id="51bd2-134">這表示 （例如，HTTP 500 回應） 的 w3wp.exe 中失敗將不會報告的 toohello 客體代理程式，，和 hello 負載平衡器會等到該執行個體退出循環。</span><span class="sxs-lookup"><span data-stu-id="51bd2-134">This means that failures in w3wp.exe (for example, HTTP 500 responses) will not be reported toohello guest agent, and hello load balancer will not take that instance out of rotation.</span></span>

### <a name="http-custom-probe"></a><span data-ttu-id="51bd2-135">HTTP 自訂探查</span><span class="sxs-lookup"><span data-stu-id="51bd2-135">HTTP custom probe</span></span>

<span data-ttu-id="51bd2-136">hello 自訂 HTTP 負載平衡器探查會覆寫 hello 預設客體代理程式探查，這表示您可以建立您自己的自訂邏輯 toodetermine hello 健全狀況的 hello 角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="51bd2-136">hello custom HTTP Load Balancer probe overrides hello default guest agent probe, which means that you can create your own custom logic toodetermine hello health of hello role instance.</span></span> <span data-ttu-id="51bd2-137">hello 負載平衡器探查您的端點每 15 秒，根據預設。</span><span class="sxs-lookup"><span data-stu-id="51bd2-137">hello load balancer probes your endpoint every 15 seconds, by default.</span></span> <span data-ttu-id="51bd2-138">hello 例項會被視為 toobe hello 負載平衡器輪替循環中的，如果它的回應 HTTP 200 hello 逾時期限 （預設 31 秒） 內。</span><span class="sxs-lookup"><span data-stu-id="51bd2-138">hello instance is considered toobe in hello load balancer rotation if it responds with an HTTP 200 within hello timeout period (31 seconds by default).</span></span>

<span data-ttu-id="51bd2-139">這可以是如果您想 tooimplement 您自己的邏輯 tooremove 執行個體從負載平衡器輪替。</span><span class="sxs-lookup"><span data-stu-id="51bd2-139">This can be useful if you want tooimplement your own logic tooremove instances from load balancer rotation.</span></span> <span data-ttu-id="51bd2-140">比方說，您可以決定 tooremove 執行個體，如果它超過 90%的 CPU，並傳回-200 狀態。</span><span class="sxs-lookup"><span data-stu-id="51bd2-140">For example, you could decide tooremove an instance if it is above 90% CPU and returns a non-200 status.</span></span> <span data-ttu-id="51bd2-141">如果您有使用 w3wp.exe 的 web 角色，這也表示您會自動監視您的網站，因為在網站上的程式碼中的失敗會傳回非 200 狀態 toohello 負載平衡器探查。</span><span class="sxs-lookup"><span data-stu-id="51bd2-141">If you have web roles that use w3wp.exe, this also means you get automatic monitoring of your website, because failures in your website code will return a non-200 status toohello load balancer probe.</span></span>

> [!NOTE]
> <span data-ttu-id="51bd2-142">hello HTTP 自訂探查支援 HTTP 通訊協定只能和相對路徑。</span><span class="sxs-lookup"><span data-stu-id="51bd2-142">hello HTTP custom probe supports relative paths and HTTP protocol only.</span></span> <span data-ttu-id="51bd2-143">不支援 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="51bd2-143">HTTPS is not supported.</span></span>

### <a name="what-makes-an-http-custom-probe-mark-an-instance-as-unhealthy"></a><span data-ttu-id="51bd2-144">什麼原因會讓 HTTP 自訂探查將執行個體標示為狀況不良？</span><span class="sxs-lookup"><span data-stu-id="51bd2-144">What makes an HTTP custom probe mark an instance as unhealthy?</span></span>

* <span data-ttu-id="51bd2-145">hello HTTP 應用程式會傳回 200 （例如，403、 404、 或 500） 以外的 HTTP 回應碼。</span><span class="sxs-lookup"><span data-stu-id="51bd2-145">hello HTTP application returns an HTTP response code other than 200 (for example, 403, 404, or 500).</span></span> <span data-ttu-id="51bd2-146">這是正值通知 hello 應用程式的執行個體應該超出服務以立即開始。</span><span class="sxs-lookup"><span data-stu-id="51bd2-146">This is a positive acknowledgment that hello application instance should be taken out of service right away.</span></span>
* <span data-ttu-id="51bd2-147">hello HTTP 伺服器未完全回應 hello 逾時期限之後。</span><span class="sxs-lookup"><span data-stu-id="51bd2-147">hello HTTP server does not respond at all after hello timeout period.</span></span> <span data-ttu-id="51bd2-148">根據 hello 逾時設定的值，這可能表示該多個探查要求移至未接聽之前 hello 探查取得標示為不執行 （也就是前 SuccessFailCount 探查傳送）。</span><span class="sxs-lookup"><span data-stu-id="51bd2-148">Depending on hello timeout value that is set, this might mean that multiple probe requests go unanswered before hello probe gets marked as not running (that is, before SuccessFailCount probes are sent).</span></span>
* <span data-ttu-id="51bd2-149">hello 伺服器關閉 hello 連接，透過 TCP 重設。</span><span class="sxs-lookup"><span data-stu-id="51bd2-149">hello server closes hello connection via a TCP reset.</span></span>

### <a name="tcp-custom-probe"></a><span data-ttu-id="51bd2-150">TCP 自訂探查</span><span class="sxs-lookup"><span data-stu-id="51bd2-150">TCP custom probe</span></span>

<span data-ttu-id="51bd2-151">TCP 探查起始的連線，藉由執行三種方式與信號交換 hello 定義連接埠。</span><span class="sxs-lookup"><span data-stu-id="51bd2-151">TCP probes initiate a connection by performing a three-way handshake with hello defined port.</span></span>

### <a name="what-makes-a-tcp-custom-probe-mark-an-instance-as-unhealthy"></a><span data-ttu-id="51bd2-152">什麼原因會讓 TCP 自訂探查將執行個體標示為狀況不良？</span><span class="sxs-lookup"><span data-stu-id="51bd2-152">What makes a TCP custom probe mark an instance as unhealthy?</span></span>

* <span data-ttu-id="51bd2-153">hello TCP 伺服器未完全回應 hello 逾時期限之後。</span><span class="sxs-lookup"><span data-stu-id="51bd2-153">hello TCP server does not respond at all after hello timeout period.</span></span> <span data-ttu-id="51bd2-154">當 hello 探查標示為不執行 hello 失敗探查數目而定，要求是設定的 toogo 再將標示為不執行 hello 探查未接聽。</span><span class="sxs-lookup"><span data-stu-id="51bd2-154">When hello probe is marked as not running depends on hello number of failed probe requests that were configured toogo unanswered before marking hello probe as not running.</span></span>
* <span data-ttu-id="51bd2-155">hello 探查收到 hello 角色執行個體上重設的 TCP。</span><span class="sxs-lookup"><span data-stu-id="51bd2-155">hello probe receives a TCP reset from hello role instance.</span></span>

<span data-ttu-id="51bd2-156">如需有關設定 HTTP 健全狀況探查或 TCP 探查的詳細資訊，請參閱 [開始使用 PowerShell 在資源管理員中建立網際網路對向負載平衡器](load-balancer-get-started-internet-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="51bd2-156">For more information about configuring an HTTP health probe or a TCP probe, see [Get started creating an Internet-facing load balancer in Resource Manager using PowerShell](load-balancer-get-started-internet-arm-ps.md).</span></span>

## <a name="add-healthy-instances-back-into-load-balancer-rotation"></a><span data-ttu-id="51bd2-157">將狀況良好的執行個體重新加入負載平衡器循環</span><span class="sxs-lookup"><span data-stu-id="51bd2-157">Add healthy instances back into load balancer rotation</span></span>

<span data-ttu-id="51bd2-158">TCP 和 HTTP 探查被視為狀況良好，並將標示為狀況良好時 hello 角色執行個體：</span><span class="sxs-lookup"><span data-stu-id="51bd2-158">TCP and HTTP probes are considered healthy and mark hello role instance as healthy when:</span></span>

* <span data-ttu-id="51bd2-159">hello 負載平衡器取得第一個時間 hello VM 會開機正數探查 hello。</span><span class="sxs-lookup"><span data-stu-id="51bd2-159">hello load balancer gets a positive probe hello first time hello VM boots.</span></span>
* <span data-ttu-id="51bd2-160">hello 編號 SuccessFailCount （前述） 會定義 hello 成功的探查需要的 toomark hello 角色執行個體為狀況良好的值。</span><span class="sxs-lookup"><span data-stu-id="51bd2-160">hello number SuccessFailCount (described earlier) defines hello value of successful probes that are required toomark hello role instance as healthy.</span></span> <span data-ttu-id="51bd2-161">已移除的角色執行個體，如果成功，請連續探查的 hello 數目必須等於或超過 hello SuccessFailCount toomark hello 角色執行個體為 執行中的值。</span><span class="sxs-lookup"><span data-stu-id="51bd2-161">If a role instance was removed, hello number of successful, successive probes must equal or exceed hello value of SuccessFailCount toomark hello role instance as running.</span></span>

> [!NOTE]
> <span data-ttu-id="51bd2-162">如果角色執行個體的 hello 健全狀況有變動，hello 負載平衡器的等候時間之前將 hello 角色執行個體放入 hello 狀況良好狀態。</span><span class="sxs-lookup"><span data-stu-id="51bd2-162">If hello health of a role instance is fluctuating, hello load balancer waits longer before putting hello role instance back in hello healthy state.</span></span> <span data-ttu-id="51bd2-163">這是透過原則 tooprotect hello 使用者和 hello 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="51bd2-163">This is done via policy tooprotect hello user and hello infrastructure.</span></span>

## <a name="use-log-analytics-for-load-balancer"></a><span data-ttu-id="51bd2-164">使用負載平衡器的記錄分析</span><span class="sxs-lookup"><span data-stu-id="51bd2-164">Use log analytics for Load Balancer</span></span>

<span data-ttu-id="51bd2-165">您可以使用[記錄分析的負載平衡器](load-balancer-monitor-log.md)toocheck hello 探查健全狀況狀態和探查計數。</span><span class="sxs-lookup"><span data-stu-id="51bd2-165">You can use [log analytics for Load Balancer](load-balancer-monitor-log.md) toocheck on hello probe health status and probe count.</span></span> <span data-ttu-id="51bd2-166">記錄可以搭配負載平衡器健全狀況狀態相關的 Power BI 或 Azure Operational Insights tooprovide 統計資料。</span><span class="sxs-lookup"><span data-stu-id="51bd2-166">Logging can be used with Power BI or Azure Operational Insights tooprovide statistics about Load Balancer health status.</span></span>
