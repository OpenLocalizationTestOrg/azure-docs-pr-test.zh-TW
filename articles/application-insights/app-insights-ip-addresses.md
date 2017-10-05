---
title: "Application Insights 使用的 IP 位址 | Microsoft Docs"
description: "Application Insights 所需的伺服器防火牆例外狀況"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 44d989f8-bae9-40ff-bfd5-8343d3e59358
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 8/11/2017
ms.author: bwren
ms.openlocfilehash: 3bb076c63223fc1567c6b7b25c1a513bbc81ed58
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="ip-addresses-used-by-application-insights"></a><span data-ttu-id="6f985-103">Application Insights 使用的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="6f985-103">IP addresses used by Application Insights</span></span>
<span data-ttu-id="6f985-104">[Azure Application Insights](app-insights-overview.md) 服務會使用一些 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6f985-104">The [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span></span> <span data-ttu-id="6f985-105">如果您所監視的應用程式裝載於防火牆後面，您可能需要知道這些位址。</span><span class="sxs-lookup"><span data-stu-id="6f985-105">You might need to know these addresses if the app that you are monitoring is hosted behind a firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="6f985-106">雖然這些位址是靜態的，但可能隨時需要變更。</span><span class="sxs-lookup"><span data-stu-id="6f985-106">Although these addresses are static, it's possible that we will need to change them from time to time.</span></span>
> 
> 

## <a name="outgoing-ports"></a><span data-ttu-id="6f985-107">連出連接埠</span><span class="sxs-lookup"><span data-stu-id="6f985-107">Outgoing ports</span></span>
<span data-ttu-id="6f985-108">您需要在伺服器防火牆開啟某些連出連接埠，以允許 Application Insights SDK 和/或狀態監視器將資料傳送至入口網站：</span><span class="sxs-lookup"><span data-stu-id="6f985-108">You need to open some outgoing ports in your server's firewall to allow the Application Insights SDK and/or Status Monitor to send data to the portal:</span></span>

| <span data-ttu-id="6f985-109">目的</span><span class="sxs-lookup"><span data-stu-id="6f985-109">Purpose</span></span> | <span data-ttu-id="6f985-110">URL</span><span class="sxs-lookup"><span data-stu-id="6f985-110">URL</span></span> | <span data-ttu-id="6f985-111">IP</span><span class="sxs-lookup"><span data-stu-id="6f985-111">IP</span></span> | <span data-ttu-id="6f985-112">連接埠</span><span class="sxs-lookup"><span data-stu-id="6f985-112">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6f985-113">遙測</span><span class="sxs-lookup"><span data-stu-id="6f985-113">Telemetry</span></span> |<span data-ttu-id="6f985-114">dc.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6f985-114">dc.services.visualstudio.com</span></span><br/><span data-ttu-id="6f985-115">dc.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="6f985-115">dc.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="6f985-116">40.114.241.141</span><span class="sxs-lookup"><span data-stu-id="6f985-116">40.114.241.141</span></span><br/><span data-ttu-id="6f985-117">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="6f985-117">104.45.136.42</span></span><br/><span data-ttu-id="6f985-118">40.84.189.107</span><span class="sxs-lookup"><span data-stu-id="6f985-118">40.84.189.107</span></span><br/><span data-ttu-id="6f985-119">168.63.242.221</span><span class="sxs-lookup"><span data-stu-id="6f985-119">168.63.242.221</span></span><br/><span data-ttu-id="6f985-120">52.167.221.184</span><span class="sxs-lookup"><span data-stu-id="6f985-120">52.167.221.184</span></span><br/><span data-ttu-id="6f985-121">52.169.64.244</span><span class="sxs-lookup"><span data-stu-id="6f985-121">52.169.64.244</span></span> |<span data-ttu-id="6f985-122">443</span><span class="sxs-lookup"><span data-stu-id="6f985-122">443</span></span> |
| <span data-ttu-id="6f985-123">即時計量串流</span><span class="sxs-lookup"><span data-stu-id="6f985-123">Live Metrics Stream</span></span> |<span data-ttu-id="6f985-124">rt.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6f985-124">rt.services.visualstudio.com</span></span><br/><span data-ttu-id="6f985-125">rt.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="6f985-125">rt.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="6f985-126">23.96.28.38</span><span class="sxs-lookup"><span data-stu-id="6f985-126">23.96.28.38</span></span><br/><span data-ttu-id="6f985-127">13.92.40.198</span><span class="sxs-lookup"><span data-stu-id="6f985-127">13.92.40.198</span></span> |<span data-ttu-id="6f985-128">443</span><span class="sxs-lookup"><span data-stu-id="6f985-128">443</span></span> |
| <span data-ttu-id="6f985-129">內部遙測</span><span class="sxs-lookup"><span data-stu-id="6f985-129">Internal Telemetry</span></span> |<span data-ttu-id="6f985-130">breeze.aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6f985-130">breeze.aimon.applicationinsights.io</span></span> |<span data-ttu-id="6f985-131">52.161.11.71</span><span class="sxs-lookup"><span data-stu-id="6f985-131">52.161.11.71</span></span> |<span data-ttu-id="6f985-132">443</span><span class="sxs-lookup"><span data-stu-id="6f985-132">443</span></span> |

## <a name="status-monitor"></a><span data-ttu-id="6f985-133">狀態監視器</span><span class="sxs-lookup"><span data-stu-id="6f985-133">Status Monitor</span></span>
<span data-ttu-id="6f985-134">狀態監視器組態 - 只有在進行變更時才需要。</span><span class="sxs-lookup"><span data-stu-id="6f985-134">Status Monitor Configuration - needed only when making changes.</span></span>

| <span data-ttu-id="6f985-135">目的</span><span class="sxs-lookup"><span data-stu-id="6f985-135">Purpose</span></span> | <span data-ttu-id="6f985-136">URL</span><span class="sxs-lookup"><span data-stu-id="6f985-136">URL</span></span> | <span data-ttu-id="6f985-137">IP</span><span class="sxs-lookup"><span data-stu-id="6f985-137">IP</span></span> | <span data-ttu-id="6f985-138">連接埠</span><span class="sxs-lookup"><span data-stu-id="6f985-138">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6f985-139">組態</span><span class="sxs-lookup"><span data-stu-id="6f985-139">Configuration</span></span> |`management.core.windows.net` | |`443` |
| <span data-ttu-id="6f985-140">組態</span><span class="sxs-lookup"><span data-stu-id="6f985-140">Configuration</span></span> |`management.azure.com` | |`443` |
| <span data-ttu-id="6f985-141">組態</span><span class="sxs-lookup"><span data-stu-id="6f985-141">Configuration</span></span> |`login.windows.net` | |`443` |
| <span data-ttu-id="6f985-142">組態</span><span class="sxs-lookup"><span data-stu-id="6f985-142">Configuration</span></span> |`login.microsoftonline.com` | |`443` |
| <span data-ttu-id="6f985-143">組態</span><span class="sxs-lookup"><span data-stu-id="6f985-143">Configuration</span></span> |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| <span data-ttu-id="6f985-144">組態</span><span class="sxs-lookup"><span data-stu-id="6f985-144">Configuration</span></span> |`auth.gfx.ms` | |`443` |
| <span data-ttu-id="6f985-145">組態</span><span class="sxs-lookup"><span data-stu-id="6f985-145">Configuration</span></span> |`login.live.com` | |`443` |
| <span data-ttu-id="6f985-146">安裝</span><span class="sxs-lookup"><span data-stu-id="6f985-146">Installation</span></span> |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a><span data-ttu-id="6f985-147">HockeyApp</span><span class="sxs-lookup"><span data-stu-id="6f985-147">HockeyApp</span></span>
| <span data-ttu-id="6f985-148">目的</span><span class="sxs-lookup"><span data-stu-id="6f985-148">Purpose</span></span> | <span data-ttu-id="6f985-149">URL</span><span class="sxs-lookup"><span data-stu-id="6f985-149">URL</span></span> | <span data-ttu-id="6f985-150">IP</span><span class="sxs-lookup"><span data-stu-id="6f985-150">IP</span></span> | <span data-ttu-id="6f985-151">連接埠</span><span class="sxs-lookup"><span data-stu-id="6f985-151">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6f985-152">當機資料</span><span class="sxs-lookup"><span data-stu-id="6f985-152">Crash data</span></span> |<span data-ttu-id="6f985-153">gate.hockeyapp.net</span><span class="sxs-lookup"><span data-stu-id="6f985-153">gate.hockeyapp.net</span></span> |<span data-ttu-id="6f985-154">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="6f985-154">104.45.136.42</span></span> |<span data-ttu-id="6f985-155">80、443</span><span class="sxs-lookup"><span data-stu-id="6f985-155">80, 443</span></span> |

## <a name="availability-tests"></a><span data-ttu-id="6f985-156">可用性集合</span><span class="sxs-lookup"><span data-stu-id="6f985-156">Availability tests</span></span>
<span data-ttu-id="6f985-157">這是用來執行 [可用性 Web 測試](app-insights-monitor-web-app-availability.md) 的位址清單。</span><span class="sxs-lookup"><span data-stu-id="6f985-157">This is the list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span></span> <span data-ttu-id="6f985-158">如果您想要在您的應用程式上執行 Web 測試，但您的 Web 伺服器限於為特定用戶端提供服務，則您必須允許來自我們的可用性測試伺服器的連入流量。</span><span class="sxs-lookup"><span data-stu-id="6f985-158">If you want to run web tests on your app, but your web server is restricted to serving specific clients, then you will have to permit incoming traffic from our availability test servers.</span></span>

<span data-ttu-id="6f985-159">為來自這些位址 (IP 位址會依照位置分組) 的連入流量開啟連接埠 80 (http) 和 443 (https)︰</span><span class="sxs-lookup"><span data-stu-id="6f985-159">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):</span></span>

```
AU : Sydney
13.70.83.252
13.75.150.96
13.75.153.9
13.75.158.185
BR : Sao Paulo
191.232.32.122
191.232.172.45
191.232.176.218
191.232.191.225
CH : Zurich
94.245.66.43
94.245.66.44
94.245.66.45
94.245.66.48
FR : Paris
94.245.72.44
94.245.72.45
94.245.72.46
94.245.72.49
94.245.72.52
94.245.72.53
HK : Hong Kong
13.75.121.122
23.99.115.153
23.99.123.38
23.102.232.186
52.175.38.49
52.175.39.103
IE : Dublin
13.74.184.101
13.74.185.160
40.69.200.198
52.164.224.46
52.169.12.203
52.169.14.11
52.169.237.149
52.178.183.105
JP : Kawaguchi
52.243.33.33
52.243.33.141
52.243.35.253
52.243.41.117
NL : Amsterdam
52.174.166.113
52.174.178.96
52.174.31.140
52.174.35.14
52.178.104.23
52.178.109.190
52.178.111.139
52.233.166.221
RU : Moscow
94.245.82.32
94.245.82.33
94.245.82.37
94.245.82.38
SE : Stockholm
94.245.78.40
94.245.78.41
94.245.78.42
94.245.78.45
SG : Singapore
52.187.29.7
52.187.179.17
52.187.76.248
52.187.43.24
52.163.57.91
52.187.30.120
US : CA-San Jose
104.45.228.236
104.45.237.251
13.64.152.110
13.64.156.54
13.64.232.251
13.64.236.105
13.91.94.59
40.118.131.182
40.83.189.192
40.83.215.122
US : FL-Miami
65.54.78.49
65.54.78.50
65.54.78.51
65.54.78.54
65.54.78.57
65.54.78.58
65.54.78.59
65.54.78.60
US : IL-Chicago
23.96.247.139
23.96.249.113
52.162.124.242
52.162.126.139
52.162.241.147
52.162.246.222
52.162.247.136
52.237.153.231
52.237.154.216
52.237.156.14
52.237.157.218
52.237.157.37
US : TX-San Antonio
104.210.145.106
13.84.176.24
13.84.49.16
13.85.11.137
13.85.26.248
13.85.69.145
52.171.136.162
52.171.141.253
52.171.57.172
52.171.58.140
US : VA-Ashburn
13.82.218.95
13.90.96.71
13.90.98.52
13.92.137.70
40.85.187.235
40.87.61.61
52.168.8.247
52.170.38.79
52.170.80.61
52.179.9.26

```  

## <a name="data-access-api"></a><span data-ttu-id="6f985-160">資料存取 API</span><span class="sxs-lookup"><span data-stu-id="6f985-160">Data access API</span></span>
| <span data-ttu-id="6f985-161">目的</span><span class="sxs-lookup"><span data-stu-id="6f985-161">Purpose</span></span> | <span data-ttu-id="6f985-162">URI</span><span class="sxs-lookup"><span data-stu-id="6f985-162">URI</span></span> | <span data-ttu-id="6f985-163">IP</span><span class="sxs-lookup"><span data-stu-id="6f985-163">IP</span></span> | <span data-ttu-id="6f985-164">連接埠</span><span class="sxs-lookup"><span data-stu-id="6f985-164">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6f985-165">API</span><span class="sxs-lookup"><span data-stu-id="6f985-165">API</span></span> |<span data-ttu-id="6f985-166">api.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6f985-166">api.applicationinsights.io</span></span><br/><span data-ttu-id="6f985-167">api1.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6f985-167">api1.applicationinsights.io</span></span><br/><span data-ttu-id="6f985-168">api2.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6f985-168">api2.applicationinsights.io</span></span><br/><span data-ttu-id="6f985-169">api3.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6f985-169">api3.applicationinsights.io</span></span><br/><span data-ttu-id="6f985-170">api4.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6f985-170">api4.applicationinsights.io</span></span><br/><span data-ttu-id="6f985-171">api5.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6f985-171">api5.applicationinsights.io</span></span> |<span data-ttu-id="6f985-172">13.82.26.252</span><span class="sxs-lookup"><span data-stu-id="6f985-172">13.82.26.252</span></span><br/><span data-ttu-id="6f985-173">40.76.213.73</span><span class="sxs-lookup"><span data-stu-id="6f985-173">40.76.213.73</span></span> |<span data-ttu-id="6f985-174">80,443</span><span class="sxs-lookup"><span data-stu-id="6f985-174">80,443</span></span> |
| <span data-ttu-id="6f985-175">API 文件</span><span class="sxs-lookup"><span data-stu-id="6f985-175">API docs</span></span> |<span data-ttu-id="6f985-176">dev.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6f985-176">dev.applicationinsights.io</span></span><br/><span data-ttu-id="6f985-177">dev.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="6f985-177">dev.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="6f985-178">dev.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6f985-178">dev.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6f985-179">www.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6f985-179">www.applicationinsights.io</span></span><br/><span data-ttu-id="6f985-180">www.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="6f985-180">www.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="6f985-181">www.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6f985-181">www.aisvc.visualstudio.com</span></span> |<span data-ttu-id="6f985-182">13.82.24.149</span><span class="sxs-lookup"><span data-stu-id="6f985-182">13.82.24.149</span></span><br/><span data-ttu-id="6f985-183">40.114.82.10</span><span class="sxs-lookup"><span data-stu-id="6f985-183">40.114.82.10</span></span> |<span data-ttu-id="6f985-184">80,443</span><span class="sxs-lookup"><span data-stu-id="6f985-184">80,443</span></span> |
| <span data-ttu-id="6f985-185">內部 API</span><span class="sxs-lookup"><span data-stu-id="6f985-185">Internal API</span></span> |<span data-ttu-id="6f985-186">aigs.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6f985-186">aigs.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6f985-187">aigs1.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6f985-187">aigs1.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6f985-188">aigs2.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6f985-188">aigs2.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6f985-189">aigs3.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6f985-189">aigs3.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6f985-190">aigs4.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6f985-190">aigs4.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6f985-191">aigs5.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6f985-191">aigs5.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6f985-192">aigs6.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6f985-192">aigs6.aisvc.visualstudio.com</span></span> |<span data-ttu-id="6f985-193">動態</span><span class="sxs-lookup"><span data-stu-id="6f985-193">dynamic</span></span>|<span data-ttu-id="6f985-194">443</span><span class="sxs-lookup"><span data-stu-id="6f985-194">443</span></span> |

## <a name="application-insights-analytics"></a><span data-ttu-id="6f985-195">Application Insights 分析</span><span class="sxs-lookup"><span data-stu-id="6f985-195">Application Insights Analytics</span></span>

| <span data-ttu-id="6f985-196">目的</span><span class="sxs-lookup"><span data-stu-id="6f985-196">Purpose</span></span> | <span data-ttu-id="6f985-197">URI</span><span class="sxs-lookup"><span data-stu-id="6f985-197">URI</span></span> | <span data-ttu-id="6f985-198">IP</span><span class="sxs-lookup"><span data-stu-id="6f985-198">IP</span></span> | <span data-ttu-id="6f985-199">連接埠</span><span class="sxs-lookup"><span data-stu-id="6f985-199">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6f985-200">Analytics 入口網站</span><span class="sxs-lookup"><span data-stu-id="6f985-200">Analytics Portal</span></span> | <span data-ttu-id="6f985-201">analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6f985-201">analytics.applicationinsights.io</span></span> | <span data-ttu-id="6f985-202">動態</span><span class="sxs-lookup"><span data-stu-id="6f985-202">dynamic</span></span> | <span data-ttu-id="6f985-203">80,443</span><span class="sxs-lookup"><span data-stu-id="6f985-203">80,443</span></span> |
| <span data-ttu-id="6f985-204">CDN</span><span class="sxs-lookup"><span data-stu-id="6f985-204">CDN</span></span> | <span data-ttu-id="6f985-205">applicationanalytics.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="6f985-205">applicationanalytics.azureedge.net</span></span> | <span data-ttu-id="6f985-206">動態</span><span class="sxs-lookup"><span data-stu-id="6f985-206">dynamic</span></span> | <span data-ttu-id="6f985-207">80,443</span><span class="sxs-lookup"><span data-stu-id="6f985-207">80,443</span></span> |
| <span data-ttu-id="6f985-208">媒體 CDN</span><span class="sxs-lookup"><span data-stu-id="6f985-208">Media CDN</span></span> | <span data-ttu-id="6f985-209">applicationanalyticsmedia.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="6f985-209">applicationanalyticsmedia.azureedge.net</span></span> | <span data-ttu-id="6f985-210">動態</span><span class="sxs-lookup"><span data-stu-id="6f985-210">dynamic</span></span> | <span data-ttu-id="6f985-211">80,443</span><span class="sxs-lookup"><span data-stu-id="6f985-211">80,443</span></span> |

<span data-ttu-id="6f985-212">注意：*.applicationinsights.io 網域由 Application Insights 團隊所擁有。</span><span class="sxs-lookup"><span data-stu-id="6f985-212">Note: *.applicationinsights.io domain is owned by Application Insights team.</span></span>

## <a name="application-insights-azure-portal-extension"></a><span data-ttu-id="6f985-213">Application Insights Azure 入口網站擴充功能</span><span class="sxs-lookup"><span data-stu-id="6f985-213">Application Insights Azure Portal Extension</span></span>

| <span data-ttu-id="6f985-214">目的</span><span class="sxs-lookup"><span data-stu-id="6f985-214">Purpose</span></span> | <span data-ttu-id="6f985-215">URI</span><span class="sxs-lookup"><span data-stu-id="6f985-215">URI</span></span> | <span data-ttu-id="6f985-216">IP</span><span class="sxs-lookup"><span data-stu-id="6f985-216">IP</span></span> | <span data-ttu-id="6f985-217">連接埠</span><span class="sxs-lookup"><span data-stu-id="6f985-217">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6f985-218">Application Insights 擴充功能</span><span class="sxs-lookup"><span data-stu-id="6f985-218">Application Insights Extension</span></span> | <span data-ttu-id="6f985-219">stamp2.app.insightsportal.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6f985-219">stamp2.app.insightsportal.visualstudio.com</span></span> | <span data-ttu-id="6f985-220">動態</span><span class="sxs-lookup"><span data-stu-id="6f985-220">dynamic</span></span> | <span data-ttu-id="6f985-221">80,443</span><span class="sxs-lookup"><span data-stu-id="6f985-221">80,443</span></span> |
| <span data-ttu-id="6f985-222">Application Insights 擴充功能 CDN</span><span class="sxs-lookup"><span data-stu-id="6f985-222">Application Insights Extension CDN</span></span> | <span data-ttu-id="6f985-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6f985-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6f985-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6f985-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6f985-225">insightsportal-cdn-aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6f985-225">insightsportal-cdn-aimon.applicationinsights.io</span></span> | <span data-ttu-id="6f985-226">動態</span><span class="sxs-lookup"><span data-stu-id="6f985-226">dynamic</span></span> | <span data-ttu-id="6f985-227">80,443</span><span class="sxs-lookup"><span data-stu-id="6f985-227">80,443</span></span> |

## <a name="application-insights-sdks"></a><span data-ttu-id="6f985-228">Application Insights SDK</span><span class="sxs-lookup"><span data-stu-id="6f985-228">Application Insights SDKs</span></span>

| <span data-ttu-id="6f985-229">目的</span><span class="sxs-lookup"><span data-stu-id="6f985-229">Purpose</span></span> | <span data-ttu-id="6f985-230">URI</span><span class="sxs-lookup"><span data-stu-id="6f985-230">URI</span></span> | <span data-ttu-id="6f985-231">IP</span><span class="sxs-lookup"><span data-stu-id="6f985-231">IP</span></span> | <span data-ttu-id="6f985-232">連接埠</span><span class="sxs-lookup"><span data-stu-id="6f985-232">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6f985-233">Application Insights JS SDK CDN</span><span class="sxs-lookup"><span data-stu-id="6f985-233">Application Insights JS SDK CDN</span></span> | <span data-ttu-id="6f985-234">az416426.vo.msecnd.net</span><span class="sxs-lookup"><span data-stu-id="6f985-234">az416426.vo.msecnd.net</span></span> | <span data-ttu-id="6f985-235">動態</span><span class="sxs-lookup"><span data-stu-id="6f985-235">dynamic</span></span> | <span data-ttu-id="6f985-236">80,443</span><span class="sxs-lookup"><span data-stu-id="6f985-236">80,443</span></span> |
| <span data-ttu-id="6f985-237">Application Insights Java SDK</span><span class="sxs-lookup"><span data-stu-id="6f985-237">Application Insights Java SDK</span></span> | <span data-ttu-id="6f985-238">aijavasdk.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="6f985-238">aijavasdk.blob.core.windows.net</span></span> | <span data-ttu-id="6f985-239">動態</span><span class="sxs-lookup"><span data-stu-id="6f985-239">dynamic</span></span> | <span data-ttu-id="6f985-240">80,443</span><span class="sxs-lookup"><span data-stu-id="6f985-240">80,443</span></span> |

## <a name="profiler"></a><span data-ttu-id="6f985-241">分析工具</span><span class="sxs-lookup"><span data-stu-id="6f985-241">Profiler</span></span>

| <span data-ttu-id="6f985-242">目的</span><span class="sxs-lookup"><span data-stu-id="6f985-242">Purpose</span></span> | <span data-ttu-id="6f985-243">URI</span><span class="sxs-lookup"><span data-stu-id="6f985-243">URI</span></span> | <span data-ttu-id="6f985-244">IP</span><span class="sxs-lookup"><span data-stu-id="6f985-244">IP</span></span> | <span data-ttu-id="6f985-245">連接埠</span><span class="sxs-lookup"><span data-stu-id="6f985-245">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6f985-246">代理程式</span><span class="sxs-lookup"><span data-stu-id="6f985-246">Agent</span></span> | <span data-ttu-id="6f985-247">agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="6f985-247">agent.azureserviceprofiler.net</span></span><br/><span data-ttu-id="6f985-248">*.agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="6f985-248">*.agent.azureserviceprofiler.net</span></span> | <span data-ttu-id="6f985-249">動態</span><span class="sxs-lookup"><span data-stu-id="6f985-249">dynamic</span></span> | <span data-ttu-id="6f985-250">443</span><span class="sxs-lookup"><span data-stu-id="6f985-250">443</span></span>
| <span data-ttu-id="6f985-251">入口網站</span><span class="sxs-lookup"><span data-stu-id="6f985-251">Portal</span></span> | <span data-ttu-id="6f985-252">gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="6f985-252">gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="6f985-253">動態</span><span class="sxs-lookup"><span data-stu-id="6f985-253">dynamic</span></span> | <span data-ttu-id="6f985-254">443</span><span class="sxs-lookup"><span data-stu-id="6f985-254">443</span></span>
| <span data-ttu-id="6f985-255">儲存體</span><span class="sxs-lookup"><span data-stu-id="6f985-255">Storage</span></span> | <span data-ttu-id="6f985-256">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="6f985-256">*.core.windows.net</span></span> | <span data-ttu-id="6f985-257">動態</span><span class="sxs-lookup"><span data-stu-id="6f985-257">dynamic</span></span> | <span data-ttu-id="6f985-258">443</span><span class="sxs-lookup"><span data-stu-id="6f985-258">443</span></span>

## <a name="snapshot-debugger"></a><span data-ttu-id="6f985-259">快照集偵錯工具</span><span class="sxs-lookup"><span data-stu-id="6f985-259">Snapshot Debugger</span></span>

| <span data-ttu-id="6f985-260">目的</span><span class="sxs-lookup"><span data-stu-id="6f985-260">Purpose</span></span> | <span data-ttu-id="6f985-261">URI</span><span class="sxs-lookup"><span data-stu-id="6f985-261">URI</span></span> | <span data-ttu-id="6f985-262">IP</span><span class="sxs-lookup"><span data-stu-id="6f985-262">IP</span></span> | <span data-ttu-id="6f985-263">連接埠</span><span class="sxs-lookup"><span data-stu-id="6f985-263">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6f985-264">代理程式</span><span class="sxs-lookup"><span data-stu-id="6f985-264">Agent</span></span> | <span data-ttu-id="6f985-265">ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="6f985-265">ppe.azureserviceprofiler.net</span></span><br/><span data-ttu-id="6f985-266">*.ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="6f985-266">*.ppe.azureserviceprofiler.net</span></span> | <span data-ttu-id="6f985-267">動態</span><span class="sxs-lookup"><span data-stu-id="6f985-267">dynamic</span></span> | <span data-ttu-id="6f985-268">443</span><span class="sxs-lookup"><span data-stu-id="6f985-268">443</span></span>
| <span data-ttu-id="6f985-269">入口網站</span><span class="sxs-lookup"><span data-stu-id="6f985-269">Portal</span></span> | <span data-ttu-id="6f985-270">ppe.gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="6f985-270">ppe.gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="6f985-271">動態</span><span class="sxs-lookup"><span data-stu-id="6f985-271">dynamic</span></span> | <span data-ttu-id="6f985-272">443</span><span class="sxs-lookup"><span data-stu-id="6f985-272">443</span></span>
| <span data-ttu-id="6f985-273">儲存體</span><span class="sxs-lookup"><span data-stu-id="6f985-273">Storage</span></span> | <span data-ttu-id="6f985-274">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="6f985-274">*.core.windows.net</span></span> | <span data-ttu-id="6f985-275">動態</span><span class="sxs-lookup"><span data-stu-id="6f985-275">dynamic</span></span> | <span data-ttu-id="6f985-276">443</span><span class="sxs-lookup"><span data-stu-id="6f985-276">443</span></span>
