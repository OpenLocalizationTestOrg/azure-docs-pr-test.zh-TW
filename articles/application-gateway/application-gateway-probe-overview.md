---
title: "監視 Azure 應用程式閘道概觀 aaaHealth |Microsoft 文件"
description: "深入了解 hello 監視在 Azure 應用程式閘道的功能"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7eeba328-bb2d-4d3e-bdac-7552e7900b7f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 5091d80394a354ff849ce7ccee8cc9d2fd0456db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-health-monitoring-overview"></a><span data-ttu-id="f4546-103">應用程式閘道健全狀況監視概觀</span><span class="sxs-lookup"><span data-stu-id="f4546-103">Application Gateway health monitoring overview</span></span>

<span data-ttu-id="f4546-104">預設的 azure 應用程式閘道監視它的後端集區中的所有資源 hello 健全狀況，並自動移除任何從 hello 集區被視為狀況不良的資源。</span><span class="sxs-lookup"><span data-stu-id="f4546-104">Azure Application Gateway by default monitors hello health of all resources in its back-end pool and automatically removes any resource considered unhealthy from hello pool.</span></span> <span data-ttu-id="f4546-105">應用程式閘道會繼續 toomonitor hello 狀況不良的執行個體，並將其加入回 toohello 狀況良好的後端集區，當它們變成可用，而且回應 toohealth 探查。</span><span class="sxs-lookup"><span data-stu-id="f4546-105">Application Gateway continues toomonitor hello unhealthy instances and adds them back toohello healthy back-end pool once they become available and respond toohealth probes.</span></span> <span data-ttu-id="f4546-106">應用程式閘道會傳送 hello 健全狀況探查 hello 與 hello 後端 HTTP 設定中定義的相同連接埠。</span><span class="sxs-lookup"><span data-stu-id="f4546-106">Application gateway sends hello health probes with hello same port that is defined in hello back-end HTTP settings.</span></span> <span data-ttu-id="f4546-107">此組態可確保該 hello 探查測試的 hello 相同連接埠，客戶就會使用 tooconnect toohello 後端。</span><span class="sxs-lookup"><span data-stu-id="f4546-107">This configuration ensures that hello probe is testing hello same port that customers would be using tooconnect toohello backend.</span></span>

![應用程式閘道探查範例][1]

<span data-ttu-id="f4546-109">在加法 toousing 預設健全狀況探查的監視，您也可以自訂 hello 健全狀況探查 toosuit 應用程式的需求。</span><span class="sxs-lookup"><span data-stu-id="f4546-109">In addition toousing default health probe monitoring, you can also customize hello health probe toosuit your application's requirements.</span></span> <span data-ttu-id="f4546-110">本文會探討預設和自訂健全狀態探查。</span><span class="sxs-lookup"><span data-stu-id="f4546-110">In this article, both default and custom health probes are covered.</span></span>

> [!NOTE]
> <span data-ttu-id="f4546-111">如果應用程式閘道子網路上沒有 NSG，應輸入流量的 hello 應用程式閘道子網路上開啟連接埠範圍 65503 65534。</span><span class="sxs-lookup"><span data-stu-id="f4546-111">If there is an NSG on Application Gateway subnet, port ranges 65503-65534 should be opened on hello Application Gateway subnet for Inbound traffic.</span></span> <span data-ttu-id="f4546-112">這些連接埠不需要 hello 後端健全狀況 API toowork。</span><span class="sxs-lookup"><span data-stu-id="f4546-112">These ports are required for hello backend health API toowork.</span></span>

## <a name="default-health-probe"></a><span data-ttu-id="f4546-113">預設的健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="f4546-113">Default health probe</span></span>

<span data-ttu-id="f4546-114">如果您沒有設定任何自訂探查組態，應用程式閘道就會自動設定預設健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="f4546-114">An application gateway automatically configures a default health probe when you don't set up any custom probe configuration.</span></span> <span data-ttu-id="f4546-115">hello 監視行為的運作方式是進行 HTTP 要求 toohello IP 位址 hello 後端集區設定。</span><span class="sxs-lookup"><span data-stu-id="f4546-115">hello monitoring behavior works by making an HTTP request toohello IP addresses configured for hello back-end pool.</span></span> <span data-ttu-id="f4546-116">預設探查 hello 後端 http 設定設定為使用 HTTPS，如果 hello 探查使用 HTTPS 做為 hello 範例以及 tootest 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="f4546-116">For default probes if hello backend http settings are configured for HTTPS, hello probe uses HTTPS as well tootest health of hello backends.</span></span>

<span data-ttu-id="f4546-117">例如： 您設定連接埠 80 上的應用程式閘道 toouse 後端伺服器 A、 B 和 C tooreceive HTTP 網路流量。</span><span class="sxs-lookup"><span data-stu-id="f4546-117">For example: You configure your application gateway toouse back-end servers A, B, and C tooreceive HTTP network traffic on port 80.</span></span> <span data-ttu-id="f4546-118">hello 預設健全狀況監視測試 hello 三部伺服器處於狀況良好的 HTTP 回應每隔 30 秒。</span><span class="sxs-lookup"><span data-stu-id="f4546-118">hello default health monitoring tests hello three servers every 30 seconds for a healthy HTTP response.</span></span> <span data-ttu-id="f4546-119">狀況良好的 HTTP 回應具有 200 到 399 之間的 [狀態碼](https://msdn.microsoft.com/library/aa287675.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="f4546-119">A healthy HTTP response has a [status code](https://msdn.microsoft.com/library/aa287675.aspx) between 200 and 399.</span></span>

<span data-ttu-id="f4546-120">如果伺服器 A hello 預設探查檢查失敗，hello 應用程式閘道會從其後端集區中，移除它，網路流量停止傳送 toothis 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f4546-120">If hello default probe check fails for server A, hello application gateway removes it from its back-end pool, and network traffic stops flowing toothis server.</span></span> <span data-ttu-id="f4546-121">hello 預設探查仍會繼續 toocheck 伺服器每隔 30 秒。</span><span class="sxs-lookup"><span data-stu-id="f4546-121">hello default probe still continues toocheck for server A every 30 seconds.</span></span> <span data-ttu-id="f4546-122">當伺服器的回應從預設健全狀況探查成功 tooone 要求時，它就會重新加入做為狀況良好的 toohello 後端集區和流量開始再次流動 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f4546-122">When server A responds successfully tooone request from a default health probe, it is added back as healthy toohello back-end pool, and traffic starts flowing toohello server again.</span></span>

### <a name="default-health-probe-settings"></a><span data-ttu-id="f4546-123">預設的健全狀況探查設定</span><span class="sxs-lookup"><span data-stu-id="f4546-123">Default health probe settings</span></span>

| <span data-ttu-id="f4546-124">探查屬性</span><span class="sxs-lookup"><span data-stu-id="f4546-124">Probe property</span></span> | <span data-ttu-id="f4546-125">值</span><span class="sxs-lookup"><span data-stu-id="f4546-125">Value</span></span> | <span data-ttu-id="f4546-126">說明</span><span class="sxs-lookup"><span data-stu-id="f4546-126">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4546-127">探查 URL</span><span class="sxs-lookup"><span data-stu-id="f4546-127">Probe URL</span></span> |<span data-ttu-id="f4546-128">http://127.0.0.1:\<連接埠\>/</span><span class="sxs-lookup"><span data-stu-id="f4546-128">http://127.0.0.1:\<port\>/</span></span> |<span data-ttu-id="f4546-129">URL 路徑</span><span class="sxs-lookup"><span data-stu-id="f4546-129">URL path</span></span> |
| <span data-ttu-id="f4546-130">間隔</span><span class="sxs-lookup"><span data-stu-id="f4546-130">Interval</span></span> |<span data-ttu-id="f4546-131">30</span><span class="sxs-lookup"><span data-stu-id="f4546-131">30</span></span> |<span data-ttu-id="f4546-132">探查間隔 (秒)</span><span class="sxs-lookup"><span data-stu-id="f4546-132">Probe interval in seconds</span></span> |
| <span data-ttu-id="f4546-133">逾時</span><span class="sxs-lookup"><span data-stu-id="f4546-133">Time-out</span></span> |<span data-ttu-id="f4546-134">30</span><span class="sxs-lookup"><span data-stu-id="f4546-134">30</span></span> |<span data-ttu-id="f4546-135">探查逾時 (秒)</span><span class="sxs-lookup"><span data-stu-id="f4546-135">Probe time-out in seconds</span></span> |
| <span data-ttu-id="f4546-136">狀況不良臨界值</span><span class="sxs-lookup"><span data-stu-id="f4546-136">Unhealthy threshold</span></span> |<span data-ttu-id="f4546-137">3</span><span class="sxs-lookup"><span data-stu-id="f4546-137">3</span></span> |<span data-ttu-id="f4546-138">探查重試計數。</span><span class="sxs-lookup"><span data-stu-id="f4546-138">Probe retry count.</span></span> <span data-ttu-id="f4546-139">hello 連續探查失敗計數達到 hello 狀況不良閾值後，hello 後端伺服器標記為。</span><span class="sxs-lookup"><span data-stu-id="f4546-139">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

> [!NOTE]
> <span data-ttu-id="f4546-140">hello 連接埠是 hello 相同為 hello 後端 HTTP 設定連接埠。</span><span class="sxs-lookup"><span data-stu-id="f4546-140">hello port is hello same port as hello back-end HTTP settings.</span></span>

<span data-ttu-id="f4546-141">hello 預設探查只會查看 http://127.0.0.1:\<連接埠\>toodetermine 健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="f4546-141">hello default probe looks only at http://127.0.0.1:\<port\> toodetermine health status.</span></span> <span data-ttu-id="f4546-142">如果您需要 tooconfigure hello 健全狀況探查 toogo tooa 自訂 URL，或修改其他任何設定，您必須使用自訂探查 hello 步驟中所述：</span><span class="sxs-lookup"><span data-stu-id="f4546-142">If you need tooconfigure hello health probe toogo tooa custom URL or modify any other settings, you must use custom probes as described in hello following steps:</span></span>

## <a name="custom-health-probe"></a><span data-ttu-id="f4546-143">自訂的健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="f4546-143">Custom health probe</span></span>

<span data-ttu-id="f4546-144">自訂探查可讓您 toohave 更細微的控制，透過 hello 健全狀況監視。</span><span class="sxs-lookup"><span data-stu-id="f4546-144">Custom probes allow you toohave a more granular control over hello health monitoring.</span></span> <span data-ttu-id="f4546-145">當使用自訂探查，則您可以設定 hello 探查間隔、 hello URL 和路徑 tootest，以及多少失敗的回應 tooaccept，再將標示為狀況不良的 hello 後端集區執行個體。</span><span class="sxs-lookup"><span data-stu-id="f4546-145">When using custom probes, you can configure hello probe interval, hello URL and path tootest, and how many failed responses tooaccept before marking hello back-end pool instance as unhealthy.</span></span>

### <a name="custom-health-probe-settings"></a><span data-ttu-id="f4546-146">自訂的健全狀況探查設定</span><span class="sxs-lookup"><span data-stu-id="f4546-146">Custom health probe settings</span></span>

<span data-ttu-id="f4546-147">hello 下表提供自訂的健全狀況探查的 hello 屬性定義。</span><span class="sxs-lookup"><span data-stu-id="f4546-147">hello following table provides definitions for hello properties of a custom health probe.</span></span>

| <span data-ttu-id="f4546-148">探查屬性</span><span class="sxs-lookup"><span data-stu-id="f4546-148">Probe property</span></span> | <span data-ttu-id="f4546-149">說明</span><span class="sxs-lookup"><span data-stu-id="f4546-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f4546-150">名稱</span><span class="sxs-lookup"><span data-stu-id="f4546-150">Name</span></span> |<span data-ttu-id="f4546-151">Hello 探查的名稱。</span><span class="sxs-lookup"><span data-stu-id="f4546-151">Name of hello probe.</span></span> <span data-ttu-id="f4546-152">這個名稱是使用的 toorefer toohello 探查後端 HTTP 設定中。</span><span class="sxs-lookup"><span data-stu-id="f4546-152">This name is used toorefer toohello probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="f4546-153">通訊協定</span><span class="sxs-lookup"><span data-stu-id="f4546-153">Protocol</span></span> |<span data-ttu-id="f4546-154">使用 toosend hello 探查通訊協定。</span><span class="sxs-lookup"><span data-stu-id="f4546-154">Protocol used toosend hello probe.</span></span> <span data-ttu-id="f4546-155">hello 探查使用 hello hello 後端 HTTP 設定中所定義的通訊協定</span><span class="sxs-lookup"><span data-stu-id="f4546-155">hello probe uses hello protocol defined in hello back-end HTTP settings</span></span> |
| <span data-ttu-id="f4546-156">Host</span><span class="sxs-lookup"><span data-stu-id="f4546-156">Host</span></span> |<span data-ttu-id="f4546-157">主機名稱 toosend hello 探查。</span><span class="sxs-lookup"><span data-stu-id="f4546-157">Host name toosend hello probe.</span></span> <span data-ttu-id="f4546-158">只有當應用程式閘道上設定多站台時適用，否則請使用 '127.0.0.1'。</span><span class="sxs-lookup"><span data-stu-id="f4546-158">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="f4546-159">此值與 VM 主機名稱不同。</span><span class="sxs-lookup"><span data-stu-id="f4546-159">This value is different from VM host name.</span></span> |
| <span data-ttu-id="f4546-160">Path</span><span class="sxs-lookup"><span data-stu-id="f4546-160">Path</span></span> |<span data-ttu-id="f4546-161">Hello 探查相對路徑。</span><span class="sxs-lookup"><span data-stu-id="f4546-161">Relative path of hello probe.</span></span> <span data-ttu-id="f4546-162">hello 有效路徑的開頭 '/'。</span><span class="sxs-lookup"><span data-stu-id="f4546-162">hello valid path starts from '/'.</span></span> |
| <span data-ttu-id="f4546-163">間隔</span><span class="sxs-lookup"><span data-stu-id="f4546-163">Interval</span></span> |<span data-ttu-id="f4546-164">探查間隔 (秒)。</span><span class="sxs-lookup"><span data-stu-id="f4546-164">Probe interval in seconds.</span></span> <span data-ttu-id="f4546-165">這個值是兩個連續探查 hello 時間間隔。</span><span class="sxs-lookup"><span data-stu-id="f4546-165">This value is hello time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="f4546-166">逾時</span><span class="sxs-lookup"><span data-stu-id="f4546-166">Time-out</span></span> |<span data-ttu-id="f4546-167">探查逾時 (秒)。</span><span class="sxs-lookup"><span data-stu-id="f4546-167">Probe time-out in seconds.</span></span> <span data-ttu-id="f4546-168">如果這個逾時期限內未收到有效的回應，hello 探查被標示為失敗。</span><span class="sxs-lookup"><span data-stu-id="f4546-168">If a valid response is not received within this time-out period, hello probe is marked as failed.</span></span>  |
| <span data-ttu-id="f4546-169">狀況不良臨界值</span><span class="sxs-lookup"><span data-stu-id="f4546-169">Unhealthy threshold</span></span> |<span data-ttu-id="f4546-170">探查重試計數。</span><span class="sxs-lookup"><span data-stu-id="f4546-170">Probe retry count.</span></span> <span data-ttu-id="f4546-171">hello 連續探查失敗計數達到 hello 狀況不良閾值後，hello 後端伺服器標記為。</span><span class="sxs-lookup"><span data-stu-id="f4546-171">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="f4546-172">如果應用程式閘道設定為單一站台，依預設 hello 主機名稱應指定為 '127.0.0.1'，除非否則在自訂探查設定。</span><span class="sxs-lookup"><span data-stu-id="f4546-172">If Application Gateway is configured for a single site, by default hello Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
> <span data-ttu-id="f4546-173">參考自訂探查送出太\<通訊協定\>://\<主機\>:\<連接埠\>\<路徑\>。</span><span class="sxs-lookup"><span data-stu-id="f4546-173">For reference a custom probe is sent too\<protocol\>://\<host\>:\<port\>\<path\>.</span></span> <span data-ttu-id="f4546-174">hello 使用通訊埠會 hello hello 後端 HTTP 設定中所定義的相同連接埠。</span><span class="sxs-lookup"><span data-stu-id="f4546-174">hello port used will be hello same port as defined in hello back-end HTTP settings.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4546-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f4546-175">Next steps</span></span>
<span data-ttu-id="f4546-176">了解應用程式閘道健康狀態監控之後, 您可以設定[自訂健全狀況探查](application-gateway-create-probe-portal.md)hello Azure 入口網站中或[自訂健全狀況探查](application-gateway-create-probe-ps.md)使用 PowerShell 和 hello Azure 資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="f4546-176">After learning about Application Gateway health monitoring, you can configure a [custom health probe](application-gateway-create-probe-portal.md) in hello Azure portal or a [custom health probe](application-gateway-create-probe-ps.md) using PowerShell and hello Azure Resource Manager deployment model.</span></span>

[1]: ./media/application-gateway-probe-overview/appgatewayprobe.png
