---
title: "Azure SQL Database 連線架構 | Microsoft Docs"
description: "本文件說明 Azure 內外部的 Azure SQLDB 連線架構。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 8a1dd89c9e82483184ceb5d767190a5a5044265d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="aa8c6-103">Azure SQL Database 連線架構</span><span class="sxs-lookup"><span data-stu-id="aa8c6-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="aa8c6-104">本文說明 Azure SQL Database 連線架構並說明不同的元件函數如何將流量導向至您的 Azure SQL Database 執行個體。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-104">This article explains the Azure SQL Database connectivity architecture and explains how the different components function to direct traffic to your instance of Azure SQL Database.</span></span> <span data-ttu-id="aa8c6-105">這些 Azure SQL Database 連線元件函數可使用從 Azure 內部連線的用戶端和從 Azure 外部連線的用戶端，將網路流量導向至 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-105">These Azure SQL Database connectivity components function to direct network traffic to the Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="aa8c6-106">本文也提供可變更連線方式的指令碼範例，以及和變更預設連線設定相關的考量。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-106">This article also provides script samples to change how connectivity occurs, and the considerations related to changing the default connectivity settings.</span></span> <span data-ttu-id="aa8c6-107">如果閱讀本文之後有任何問題，請透過 dmalik@microsoft.com 來連絡 Dhruv。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="aa8c6-108">連線架構</span><span class="sxs-lookup"><span data-stu-id="aa8c6-108">Connectivity architecture</span></span>

<span data-ttu-id="aa8c6-109">下圖提供 Azure SQL Database 連線架構的高階概觀。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-109">The following diagram provides a high-level overview of the Azure SQL Database connectivity architecture.</span></span> 

![架構概觀](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="aa8c6-111">下列步驟說明如何透過 Azure SQL Database 軟體負載平衡器 (SLB) 和 Azure SQL Database 閘道，和 Azure SQL Database 建立連線。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-111">The following steps describe how a connection is established to an Azure SQL database through the Azure SQL Database software load-balancer (SLB) and the Azure SQL Database gateway.</span></span>

- <span data-ttu-id="aa8c6-112">Azure 內部或 Azure 外部的用戶端會連線到其有公用 IP 位址且接聽連接埠 1433 的 SLB。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-112">Clients within Azure or outside of Azure connect to the SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="aa8c6-113">SLB 會將流量導向至 Azure SQL Database 閘道。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-113">The SLB directs traffic to the Azure SQL Database gateway.</span></span>
- <span data-ttu-id="aa8c6-114">閘道會將流量重新導向至正確的 Proxy 中介軟體。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-114">The gateway redirects the traffic to the correct proxy middleware.</span></span>
- <span data-ttu-id="aa8c6-115">Proxy 中介軟體會將流量重新導向到適當的 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-115">The proxy middleware redirects the traffic to the appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aa8c6-116">這些元件各個都在網路和應用程式層內建分散式阻斷服務 (DDoS) 保護。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-116">Each of these components has distributed denial of service (DDoS) protection built-in at the network and the app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="aa8c6-117">從 Azure 內部連線</span><span class="sxs-lookup"><span data-stu-id="aa8c6-117">Connectivity from within Azure</span></span>

<span data-ttu-id="aa8c6-118">如果您從 Azure 內部連線，該連線預設的連線原則為 [重新導向]。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="aa8c6-119">[重新導向] 原則代表連線在和 Azure SQL Database 建立 TCP 工作階段之後，會將其 Azure SQL Database 閘道的目的地虛擬 IP 變更為 Proxy 中介軟體的目的地虛擬 IP，將該用戶端工作階段重新導向至 Proxy 中介軟體。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-119">A policy of **Redirect** means that connections after the TCP session is established to the Azure SQL database, the client session is then redirected to the proxy middleware with a change to the destination virtual IP from that of the Azure SQL Database gateway to that of the proxy middleware.</span></span> <span data-ttu-id="aa8c6-120">此後，所有後續封包會略過 Azure SQL Database 閘道，直接流經 Proxy 中介軟體。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-120">Thereafter, all subsequent packets flow directly via the proxy middleware, bypassing the Azure SQL Database gateway.</span></span> <span data-ttu-id="aa8c6-121">下圖說明此流量。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-121">The following diagram illustrates this traffic flow.</span></span>

![架構概觀](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="aa8c6-123">從 Azure 外部連線</span><span class="sxs-lookup"><span data-stu-id="aa8c6-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="aa8c6-124">如果您從 Azure 外部連線，該連線預設的連線原則為 [Proxy]。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="aa8c6-125">[Proxy] 原則代表會透過 Azure SQL Database 閘道建立 TCP 工作階段，且所有後續封包都會流經閘道。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-125">A policy of **Proxy** means that the TCP session is established via the Azure SQL Database gateway and all subsequent packets flow via the gateway.</span></span> <span data-ttu-id="aa8c6-126">下圖說明此流量。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-126">The following diagram illustrates this traffic flow.</span></span>

![架構概觀](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="aa8c6-128">Azure SQL Database 閘道 IP 位址</span><span class="sxs-lookup"><span data-stu-id="aa8c6-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="aa8c6-129">若要從內部部署資源連線到 Azure SQL Database，您必須允許輸出網路流量流到 Azure 區域的 Azure SQL Database 閘道。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-129">To connect to an Azure SQL database from on-premises resources, you need to allow outbound network traffic to the Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="aa8c6-130">在從內部部署資源連線時的預設 Proxy 模式中連線時，您只能透過閘道連線。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-130">Your connections only go via the gateway when connecting in Proxy mode, which is the default when connecting from on-premises resources.</span></span>

<span data-ttu-id="aa8c6-131">下表列出所有資料區之 Azure SQL Database 閘道的主要和次要 IP。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-131">The following table lists the primary and secondary IPs of the Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="aa8c6-132">對於某些區域，會有兩個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="aa8c6-133">在這些區域中，主要 IP 位址是閘道目前的 IP 位址，而次要 IP 位址為容錯移轉 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-133">In these regions, the primary IP address is the current IP address of the gateway and the second IP address is a failover IP address.</span></span> <span data-ttu-id="aa8c6-134">容錯移轉位址是指可能會移動伺服器以讓服務保持高可用性的位址。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-134">The failover address is the address to which we might move your server to keep the service availability high.</span></span> <span data-ttu-id="aa8c6-135">對於這些區域，建議您針對這兩個 IP 位址允許輸出。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-135">For these regions, we recommend that you allow outbound to both the IP addresses.</span></span> <span data-ttu-id="aa8c6-136">次要 IP 位址為 Microsoft 所有，在由 Azure SQL Database 啟動以接受連線之前，並不會接聽任何服務。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-136">The second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database to accept connections.</span></span>

| <span data-ttu-id="aa8c6-137">區域名稱</span><span class="sxs-lookup"><span data-stu-id="aa8c6-137">Region Name</span></span> | <span data-ttu-id="aa8c6-138">主要 IP 位址</span><span class="sxs-lookup"><span data-stu-id="aa8c6-138">Primary IP address</span></span> | <span data-ttu-id="aa8c6-139">次要 IP 位址</span><span class="sxs-lookup"><span data-stu-id="aa8c6-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="aa8c6-140">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-140">Australia East</span></span> | <span data-ttu-id="aa8c6-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="aa8c6-141">191.238.66.109</span></span> | <span data-ttu-id="aa8c6-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="aa8c6-142">13.75.149.87</span></span> |
| <span data-ttu-id="aa8c6-143">澳大利亞東南部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-143">Australia South East</span></span> | <span data-ttu-id="aa8c6-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="aa8c6-144">191.239.192.109</span></span> | <span data-ttu-id="aa8c6-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="aa8c6-145">13.73.109.251</span></span> |
| <span data-ttu-id="aa8c6-146">巴西南部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-146">Brazil South</span></span> | <span data-ttu-id="aa8c6-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="aa8c6-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="aa8c6-148">加拿大中部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-148">Canada Central</span></span> | <span data-ttu-id="aa8c6-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="aa8c6-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="aa8c6-150">加拿大東部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-150">Canada East</span></span> | <span data-ttu-id="aa8c6-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="aa8c6-151">40.86.226.166</span></span> | |
| <span data-ttu-id="aa8c6-152">美國中部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-152">Central US</span></span> | <span data-ttu-id="aa8c6-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="aa8c6-153">23.99.160.139</span></span> | <span data-ttu-id="aa8c6-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="aa8c6-154">13.67.215.62</span></span> |
| <span data-ttu-id="aa8c6-155">東亞</span><span class="sxs-lookup"><span data-stu-id="aa8c6-155">East Asia</span></span> | <span data-ttu-id="aa8c6-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="aa8c6-156">191.234.2.139</span></span> | <span data-ttu-id="aa8c6-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="aa8c6-157">52.175.33.150</span></span> |
| <span data-ttu-id="aa8c6-158">美國東部 1</span><span class="sxs-lookup"><span data-stu-id="aa8c6-158">East US 1</span></span> | <span data-ttu-id="aa8c6-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="aa8c6-159">191.238.6.43</span></span> | <span data-ttu-id="aa8c6-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="aa8c6-160">40.121.158.30</span></span> |
| <span data-ttu-id="aa8c6-161">美國東部 2</span><span class="sxs-lookup"><span data-stu-id="aa8c6-161">East US 2</span></span> | <span data-ttu-id="aa8c6-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="aa8c6-162">191.239.224.107</span></span> | <span data-ttu-id="aa8c6-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="aa8c6-163">40.79.84.180</span></span> |
| <span data-ttu-id="aa8c6-164">印度中部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-164">India Central</span></span> | <span data-ttu-id="aa8c6-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="aa8c6-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="aa8c6-166">印度南部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-166">India South</span></span> | <span data-ttu-id="aa8c6-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="aa8c6-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="aa8c6-168">印度西部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-168">India West</span></span> | <span data-ttu-id="aa8c6-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="aa8c6-169">104.211.160.80</span></span> | |
| <span data-ttu-id="aa8c6-170">日本東部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-170">Japan East</span></span> | <span data-ttu-id="aa8c6-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="aa8c6-171">191.237.240.43</span></span> | <span data-ttu-id="aa8c6-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="aa8c6-172">13.78.61.196</span></span> |
| <span data-ttu-id="aa8c6-173">日本西部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-173">Japan West</span></span> | <span data-ttu-id="aa8c6-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="aa8c6-174">191.238.68.11</span></span> | <span data-ttu-id="aa8c6-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="aa8c6-175">104.214.148.156</span></span> |
| <span data-ttu-id="aa8c6-176">韓國中部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-176">Korea Central</span></span> | <span data-ttu-id="aa8c6-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="aa8c6-177">52.231.32.42</span></span> | |
| <span data-ttu-id="aa8c6-178">韓國南部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-178">Korea South</span></span> | <span data-ttu-id="aa8c6-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="aa8c6-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="aa8c6-180">美國中北部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-180">North Central US</span></span> | <span data-ttu-id="aa8c6-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="aa8c6-181">23.98.55.75</span></span> | <span data-ttu-id="aa8c6-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="aa8c6-182">23.96.178.199</span></span> |
| <span data-ttu-id="aa8c6-183">北歐</span><span class="sxs-lookup"><span data-stu-id="aa8c6-183">North Europe</span></span> | <span data-ttu-id="aa8c6-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="aa8c6-184">191.235.193.75</span></span> | <span data-ttu-id="aa8c6-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="aa8c6-185">40.113.93.91</span></span> |
| <span data-ttu-id="aa8c6-186">美國中南部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-186">South Central US</span></span> | <span data-ttu-id="aa8c6-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="aa8c6-187">23.98.162.75</span></span> | <span data-ttu-id="aa8c6-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="aa8c6-188">13.66.62.124</span></span> |
| <span data-ttu-id="aa8c6-189">東南亞</span><span class="sxs-lookup"><span data-stu-id="aa8c6-189">South East Asia</span></span> | <span data-ttu-id="aa8c6-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="aa8c6-190">23.100.117.95</span></span> | <span data-ttu-id="aa8c6-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="aa8c6-191">104.43.15.0</span></span> |
| <span data-ttu-id="aa8c6-192">英國北部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-192">UK North</span></span> | <span data-ttu-id="aa8c6-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="aa8c6-193">13.87.97.210</span></span> | |
| <span data-ttu-id="aa8c6-194">英國南部 1</span><span class="sxs-lookup"><span data-stu-id="aa8c6-194">UK South 1</span></span> | <span data-ttu-id="aa8c6-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="aa8c6-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="aa8c6-196">英國南部 2</span><span class="sxs-lookup"><span data-stu-id="aa8c6-196">UK South 2</span></span> | <span data-ttu-id="aa8c6-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="aa8c6-197">13.87.34.7</span></span> | |
| <span data-ttu-id="aa8c6-198">英國西部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-198">UK West</span></span> | <span data-ttu-id="aa8c6-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="aa8c6-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="aa8c6-200">美國中西部</span><span class="sxs-lookup"><span data-stu-id="aa8c6-200">West Central US</span></span> | <span data-ttu-id="aa8c6-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="aa8c6-201">13.78.145.25</span></span> | |
| <span data-ttu-id="aa8c6-202">西歐</span><span class="sxs-lookup"><span data-stu-id="aa8c6-202">West Europe</span></span> | <span data-ttu-id="aa8c6-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="aa8c6-203">191.237.232.75</span></span> | <span data-ttu-id="aa8c6-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="aa8c6-204">40.68.37.158</span></span> |
| <span data-ttu-id="aa8c6-205">美國西部 1</span><span class="sxs-lookup"><span data-stu-id="aa8c6-205">West US 1</span></span> | <span data-ttu-id="aa8c6-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="aa8c6-206">23.99.34.75</span></span> | <span data-ttu-id="aa8c6-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="aa8c6-207">104.42.238.205</span></span> |
| <span data-ttu-id="aa8c6-208">美國西部 2</span><span class="sxs-lookup"><span data-stu-id="aa8c6-208">West US 2</span></span> | <span data-ttu-id="aa8c6-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="aa8c6-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="aa8c6-210">變更 Azure SQL Database 連線原則</span><span class="sxs-lookup"><span data-stu-id="aa8c6-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="aa8c6-211">若要變更 Azure SQL Database 伺服器的 Azure SQL Database 連線原則，請使用 [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-211">To change the Azure SQL Database connection policy for an Azure SQL Database server, use the [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="aa8c6-212">如果您的連線原則設定為 [Proxy]，所有網路封包都會流經 Azure SQL Database 閘道。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-212">If your connection policy is set to **Proxy**, all network packets flow via the Azure SQL Database gateway.</span></span> <span data-ttu-id="aa8c6-213">對於此設定，您必須只允許輸出至 Azure SQL Database 閘道 IP。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-213">For this setting, you need to allow outbound to only the Azure SQL Database gateway IP.</span></span> <span data-ttu-id="aa8c6-214">和 [重新導向] 設定相比，使用 [Proxy] 設定會較為延遲。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="aa8c6-215">如果您的連線原則設定為 [重新導向]，所有網路封包都會直接流到中介軟體 Proxy。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-215">If your connection policy is setting **Redirect**, all network packets flow directly to the middleware proxy.</span></span> <span data-ttu-id="aa8c6-216">對於此設定，您需要允許輸出至多個 IP。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-216">For this setting, you need to allow outbound to multiple IPs.</span></span> 

## <a name="script-to-change-connection-settings"></a><span data-ttu-id="aa8c6-217">變更連線設定的指令碼</span><span class="sxs-lookup"><span data-stu-id="aa8c6-217">Script to change connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aa8c6-218">此指令碼需要 [Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-218">This script requires the [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="aa8c6-219">下列 PowerShell 指令碼會示範如何變更連線原則。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-219">The following PowerShell script shows how to change the connection policy.</span></span>

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting the current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting the property to ‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="aa8c6-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa8c6-220">Next steps</span></span>

- <span data-ttu-id="aa8c6-221">如需如何變更 Azure SQL Database 伺服器的 Azure SQL Database 連線原則，請參閱[使用 REST API 建立或更新伺服器連線原則](https://msdn.microsoft.com/library/azure/mt604439.aspx)。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-221">For information on how to change the Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using the REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="aa8c6-222">如需使用 ADO.NET 4.5 或更新版本用戶端之 Azure SQL Database 連接行為的詳細資訊，請參閱 [ADO.NET 4.5 超過 1433以外的連接埠](sql-database-develop-direct-route-ports-adonet-v12.md)。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="aa8c6-223">如需一般應用程式開發概觀的資訊，請參閱 [SQL Database 應用程式開發概觀](sql-database-develop-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="aa8c6-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>
