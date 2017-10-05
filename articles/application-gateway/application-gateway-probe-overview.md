---
title: "Azure 應用程式閘道的健全狀況監視概觀 | Microsoft Docs"
description: "了解 Azure 應用程式閘道的監視功能"
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
ms.openlocfilehash: 899115d213e626f17e58c2e5f01313f760f9e7f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="application-gateway-health-monitoring-overview"></a><span data-ttu-id="fb4d5-103">應用程式閘道健全狀況監視概觀</span><span class="sxs-lookup"><span data-stu-id="fb4d5-103">Application Gateway health monitoring overview</span></span>

<span data-ttu-id="fb4d5-104">Azure 應用程式閘道預設會監視其後端集區中所有資源的健康狀況，並自動從集區中移除任何被視為狀況不良的資源。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-104">Azure Application Gateway by default monitors the health of all resources in its back-end pool and automatically removes any resource considered unhealthy from the pool.</span></span> <span data-ttu-id="fb4d5-105">應用程式閘道會繼續監視狀況不良的執行個體，一旦其恢復可用狀態並回應健康狀況探查，就會將其新增回狀況良好後端集區中。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-105">Application Gateway continues to monitor the unhealthy instances and adds them back to the healthy back-end pool once they become available and respond to health probes.</span></span> <span data-ttu-id="fb4d5-106">應用程式閘道會以後端 HTTP 設定中定義的相同連接埠傳送健康狀態探查。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-106">Application gateway sends the health probes with the same port that is defined in the back-end HTTP settings.</span></span> <span data-ttu-id="fb4d5-107">此組態可確保探查所測試的連接埠會和客戶用來連接到後端的連接埠相同。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-107">This configuration ensures that the probe is testing the same port that customers would be using to connect to the backend.</span></span>

![應用程式閘道探查範例][1]

<span data-ttu-id="fb4d5-109">除了使用預設的健全狀況探查監視，您也可以自訂健全狀況探查，以符合應用程式的需求。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-109">In addition to using default health probe monitoring, you can also customize the health probe to suit your application's requirements.</span></span> <span data-ttu-id="fb4d5-110">本文會探討預設和自訂健全狀態探查。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-110">In this article, both default and custom health probes are covered.</span></span>

> [!NOTE]
> <span data-ttu-id="fb4d5-111">如果應用程式閘道子網路上有 NSG，則應在應用程式閘道子網路上開啟連接埠範圍 65503-65534，以供輸入流量使用。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-111">If there is an NSG on Application Gateway subnet, port ranges 65503-65534 should be opened on the Application Gateway subnet for Inbound traffic.</span></span> <span data-ttu-id="fb4d5-112">需要這些連接埠，後端健康狀態 API 才能運作。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-112">These ports are required for the backend health API to work.</span></span>

## <a name="default-health-probe"></a><span data-ttu-id="fb4d5-113">預設的健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="fb4d5-113">Default health probe</span></span>

<span data-ttu-id="fb4d5-114">如果您沒有設定任何自訂探查組態，應用程式閘道就會自動設定預設健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-114">An application gateway automatically configures a default health probe when you don't set up any custom probe configuration.</span></span> <span data-ttu-id="fb4d5-115">監視行為的運作方式是對後端集區所設定的 IP 位址提出 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-115">The monitoring behavior works by making an HTTP request to the IP addresses configured for the back-end pool.</span></span> <span data-ttu-id="fb4d5-116">針對預設探查，如果後端 http 設定設為使用 HTTPS，探查也會使用 HTTPS 測試後端的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-116">For default probes if the backend http settings are configured for HTTPS, the probe uses HTTPS as well to test health of the backends.</span></span>

<span data-ttu-id="fb4d5-117">例如：您將應用程式閘道設定為使用 A、B 和 C 後端伺服器來接收連接埠 80 上的 HTTP 網路流量。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-117">For example: You configure your application gateway to use back-end servers A, B, and C to receive HTTP network traffic on port 80.</span></span> <span data-ttu-id="fb4d5-118">預設健全狀況監視每 30 秒就會對三部伺服器進行一次測試，以取得狀況良好的 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-118">The default health monitoring tests the three servers every 30 seconds for a healthy HTTP response.</span></span> <span data-ttu-id="fb4d5-119">狀況良好的 HTTP 回應具有 200 到 399 之間的 [狀態碼](https://msdn.microsoft.com/library/aa287675.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-119">A healthy HTTP response has a [status code](https://msdn.microsoft.com/library/aa287675.aspx) between 200 and 399.</span></span>

<span data-ttu-id="fb4d5-120">如果伺服器 A 的預設探查檢查失敗，應用程式閘道就會將其從後端集區中移除，網路流量也不會再流向此伺服器。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-120">If the default probe check fails for server A, the application gateway removes it from its back-end pool, and network traffic stops flowing to this server.</span></span> <span data-ttu-id="fb4d5-121">預設探查仍會繼續每 30 秒檢查一次伺服器 A。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-121">The default probe still continues to check for server A every 30 seconds.</span></span> <span data-ttu-id="fb4d5-122">當伺服器 A 成功回應預設健全狀態探查所提出的要求時，就會變為狀況良好並重新回到後端集區中，而流量也會開始再次流向該伺服器。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-122">When server A responds successfully to one request from a default health probe, it is added back as healthy to the back-end pool, and traffic starts flowing to the server again.</span></span>

### <a name="default-health-probe-settings"></a><span data-ttu-id="fb4d5-123">預設的健全狀況探查設定</span><span class="sxs-lookup"><span data-stu-id="fb4d5-123">Default health probe settings</span></span>

| <span data-ttu-id="fb4d5-124">探查屬性</span><span class="sxs-lookup"><span data-stu-id="fb4d5-124">Probe property</span></span> | <span data-ttu-id="fb4d5-125">值</span><span class="sxs-lookup"><span data-stu-id="fb4d5-125">Value</span></span> | <span data-ttu-id="fb4d5-126">說明</span><span class="sxs-lookup"><span data-stu-id="fb4d5-126">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fb4d5-127">探查 URL</span><span class="sxs-lookup"><span data-stu-id="fb4d5-127">Probe URL</span></span> |<span data-ttu-id="fb4d5-128">http://127.0.0.1:\<連接埠\>/</span><span class="sxs-lookup"><span data-stu-id="fb4d5-128">http://127.0.0.1:\<port\>/</span></span> |<span data-ttu-id="fb4d5-129">URL 路徑</span><span class="sxs-lookup"><span data-stu-id="fb4d5-129">URL path</span></span> |
| <span data-ttu-id="fb4d5-130">間隔</span><span class="sxs-lookup"><span data-stu-id="fb4d5-130">Interval</span></span> |<span data-ttu-id="fb4d5-131">30</span><span class="sxs-lookup"><span data-stu-id="fb4d5-131">30</span></span> |<span data-ttu-id="fb4d5-132">探查間隔 (秒)</span><span class="sxs-lookup"><span data-stu-id="fb4d5-132">Probe interval in seconds</span></span> |
| <span data-ttu-id="fb4d5-133">逾時</span><span class="sxs-lookup"><span data-stu-id="fb4d5-133">Time-out</span></span> |<span data-ttu-id="fb4d5-134">30</span><span class="sxs-lookup"><span data-stu-id="fb4d5-134">30</span></span> |<span data-ttu-id="fb4d5-135">探查逾時 (秒)</span><span class="sxs-lookup"><span data-stu-id="fb4d5-135">Probe time-out in seconds</span></span> |
| <span data-ttu-id="fb4d5-136">狀況不良臨界值</span><span class="sxs-lookup"><span data-stu-id="fb4d5-136">Unhealthy threshold</span></span> |<span data-ttu-id="fb4d5-137">3</span><span class="sxs-lookup"><span data-stu-id="fb4d5-137">3</span></span> |<span data-ttu-id="fb4d5-138">探查重試計數。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-138">Probe retry count.</span></span> <span data-ttu-id="fb4d5-139">連續探查失敗計數到達狀況不良臨界值後，就會將後端伺服器標示為故障。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-139">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

> [!NOTE]
> <span data-ttu-id="fb4d5-140">連接埠會是和後端 HTTP 設定相同的連接埠。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-140">The port is the same port as the back-end HTTP settings.</span></span>

<span data-ttu-id="fb4d5-141">預設探查只會查看 http://127.0.0.1:\<連接埠\> 來判斷健康狀態。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-141">The default probe looks only at http://127.0.0.1:\<port\> to determine health status.</span></span> <span data-ttu-id="fb4d5-142">如果您需要設定健全狀態探查，使其移至自訂 URL 或修改任何其他設定，則必須使用如下列步驟所述的自訂探查：</span><span class="sxs-lookup"><span data-stu-id="fb4d5-142">If you need to configure the health probe to go to a custom URL or modify any other settings, you must use custom probes as described in the following steps:</span></span>

## <a name="custom-health-probe"></a><span data-ttu-id="fb4d5-143">自訂的健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="fb4d5-143">Custom health probe</span></span>

<span data-ttu-id="fb4d5-144">自訂探查可讓您更細微地控制健全狀況監視。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-144">Custom probes allow you to have a more granular control over the health monitoring.</span></span> <span data-ttu-id="fb4d5-145">使用自訂探查時，您可以設定探查間隔、要測試的 URL 和路徑，以及在將後端集區執行個體標示為狀況不良前，可接受的失敗回應次數。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-145">When using custom probes, you can configure the probe interval, the URL and path to test, and how many failed responses to accept before marking the back-end pool instance as unhealthy.</span></span>

### <a name="custom-health-probe-settings"></a><span data-ttu-id="fb4d5-146">自訂的健全狀況探查設定</span><span class="sxs-lookup"><span data-stu-id="fb4d5-146">Custom health probe settings</span></span>

<span data-ttu-id="fb4d5-147">下表提供自訂健全狀況探查的屬性定義。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-147">The following table provides definitions for the properties of a custom health probe.</span></span>

| <span data-ttu-id="fb4d5-148">探查屬性</span><span class="sxs-lookup"><span data-stu-id="fb4d5-148">Probe property</span></span> | <span data-ttu-id="fb4d5-149">說明</span><span class="sxs-lookup"><span data-stu-id="fb4d5-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fb4d5-150">Name</span><span class="sxs-lookup"><span data-stu-id="fb4d5-150">Name</span></span> |<span data-ttu-id="fb4d5-151">探查的名稱。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-151">Name of the probe.</span></span> <span data-ttu-id="fb4d5-152">此名稱用來在後端 HTTP 設定中指出探查。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-152">This name is used to refer to the probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="fb4d5-153">通訊協定</span><span class="sxs-lookup"><span data-stu-id="fb4d5-153">Protocol</span></span> |<span data-ttu-id="fb4d5-154">用來傳送探查的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-154">Protocol used to send the probe.</span></span> <span data-ttu-id="fb4d5-155">探查會使用後端 HTTP 設定中定義的通訊協定</span><span class="sxs-lookup"><span data-stu-id="fb4d5-155">The probe uses the protocol defined in the back-end HTTP settings</span></span> |
| <span data-ttu-id="fb4d5-156">Host</span><span class="sxs-lookup"><span data-stu-id="fb4d5-156">Host</span></span> |<span data-ttu-id="fb4d5-157">用來傳送探查的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-157">Host name to send the probe.</span></span> <span data-ttu-id="fb4d5-158">只有當應用程式閘道上設定多站台時適用，否則請使用 '127.0.0.1'。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-158">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="fb4d5-159">此值與 VM 主機名稱不同。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-159">This value is different from VM host name.</span></span> |
| <span data-ttu-id="fb4d5-160">Path</span><span class="sxs-lookup"><span data-stu-id="fb4d5-160">Path</span></span> |<span data-ttu-id="fb4d5-161">探查的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-161">Relative path of the probe.</span></span> <span data-ttu-id="fb4d5-162">有效路徑的開頭為 '/'。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-162">The valid path starts from '/'.</span></span> |
| <span data-ttu-id="fb4d5-163">間隔</span><span class="sxs-lookup"><span data-stu-id="fb4d5-163">Interval</span></span> |<span data-ttu-id="fb4d5-164">探查間隔 (秒)。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-164">Probe interval in seconds.</span></span> <span data-ttu-id="fb4d5-165">這個值是兩個連續探查之間的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-165">This value is the time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="fb4d5-166">逾時</span><span class="sxs-lookup"><span data-stu-id="fb4d5-166">Time-out</span></span> |<span data-ttu-id="fb4d5-167">探查逾時 (秒)。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-167">Probe time-out in seconds.</span></span> <span data-ttu-id="fb4d5-168">如果在這個逾時期間內未收到有效的回應，則會將探查標示為失敗。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-168">If a valid response is not received within this time-out period, the probe is marked as failed.</span></span>  |
| <span data-ttu-id="fb4d5-169">狀況不良臨界值</span><span class="sxs-lookup"><span data-stu-id="fb4d5-169">Unhealthy threshold</span></span> |<span data-ttu-id="fb4d5-170">探查重試計數。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-170">Probe retry count.</span></span> <span data-ttu-id="fb4d5-171">連續探查失敗計數到達狀況不良臨界值後，就會將後端伺服器標示為故障。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-171">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="fb4d5-172">如果已將應用程式閘道設定為單一站台，根據預設，除非已在自訂探查中加以設定，否則應將主機名稱指定為 '127.0.0.1'。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-172">If Application Gateway is configured for a single site, by default the Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
> <span data-ttu-id="fb4d5-173">僅供參考，自訂探查會傳送到 \<通訊協定\>://\<主機\>:\<連接埠\>\<路徑\>。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-173">For reference a custom probe is sent to \<protocol\>://\<host\>:\<port\>\<path\>.</span></span> <span data-ttu-id="fb4d5-174">所使用的連接埠會是和後端 HTTP 設定中所定義者相同的連接埠。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-174">The port used will be the same port as defined in the back-end HTTP settings.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb4d5-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fb4d5-175">Next steps</span></span>
<span data-ttu-id="fb4d5-176">在了解應用程式閘道的健全狀態監視之後，您可以在 Azure 入口網站中[自訂健全狀態探查](application-gateway-create-probe-portal.md)，或使用 PowerShell 和 Azure Resource Manager 部署模型設定[自訂健全狀態探查](application-gateway-create-probe-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="fb4d5-176">After learning about Application Gateway health monitoring, you can configure a [custom health probe](application-gateway-create-probe-portal.md) in the Azure portal or a [custom health probe](application-gateway-create-probe-ps.md) using PowerShell and the Azure Resource Manager deployment model.</span></span>

[1]: ./media/application-gateway-probe-overview/appgatewayprobe.png
