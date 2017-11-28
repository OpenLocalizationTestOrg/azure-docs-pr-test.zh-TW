---
title: "SQL Database 連線架構 aaaAzure |Microsoft 文件"
description: "本文件說明 hello Azure SQLDB 連線架構從 Azure 內部或從 Azure 外部。"
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
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="e0cbc-103">Azure SQL Database 連線架構</span><span class="sxs-lookup"><span data-stu-id="e0cbc-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="e0cbc-104">本文說明 hello Azure SQL Database 連線架構，並說明 hello 不同元件的 toodirect 流量 tooyour Azure SQL Database 執行個體的運作方式。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-104">This article explains hello Azure SQL Database connectivity architecture and explains how hello different components function toodirect traffic tooyour instance of Azure SQL Database.</span></span> <span data-ttu-id="e0cbc-105">與在 Azure 中從連接的用戶端及連線從 Azure 外部的用戶端，這些 Azure SQL Database 連接元件函式 toodirect 網路流量 toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-105">These Azure SQL Database connectivity components function toodirect network traffic toohello Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="e0cbc-106">本文也提供指令碼範例 toochange 連線進行的方式，以及 hello 考量相關 toochanging hello 預設連線設定。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-106">This article also provides script samples toochange how connectivity occurs, and hello considerations related toochanging hello default connectivity settings.</span></span> <span data-ttu-id="e0cbc-107">如果閱讀本文之後有任何問題，請透過 dmalik@microsoft.com 來連絡 Dhruv。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="e0cbc-108">連線架構</span><span class="sxs-lookup"><span data-stu-id="e0cbc-108">Connectivity architecture</span></span>

<span data-ttu-id="e0cbc-109">下列圖表中的 hello 提供 hello Azure SQL Database 連線架構的高階概觀。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-109">hello following diagram provides a high-level overview of hello Azure SQL Database connectivity architecture.</span></span> 

![架構概觀](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="e0cbc-111">hello 下列步驟描述如何連接是透過 hello Azure SQL Database 軟體負載平衡器 (SLB) 和 hello Azure SQL Database 閘道建立的 tooan Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-111">hello following steps describe how a connection is established tooan Azure SQL database through hello Azure SQL Database software load-balancer (SLB) and hello Azure SQL Database gateway.</span></span>

- <span data-ttu-id="e0cbc-112">在 Azure 或 Azure 外部的用戶端連線 toohello SLB，其具有公用 IP 位址和通訊埠 1433年上接聽。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-112">Clients within Azure or outside of Azure connect toohello SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="e0cbc-113">hello SLB 指示流量 toohello Azure SQL Database 的閘道。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-113">hello SLB directs traffic toohello Azure SQL Database gateway.</span></span>
- <span data-ttu-id="e0cbc-114">hello 閘道重新導向 hello 流量 toohello 正確的 proxy 中介軟體。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-114">hello gateway redirects hello traffic toohello correct proxy middleware.</span></span>
- <span data-ttu-id="e0cbc-115">hello proxy 中介軟體重新導向 hello 流量 toohello 適當 Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-115">hello proxy middleware redirects hello traffic toohello appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0cbc-116">每個元件具有分散式阻斷服務 (DDoS) 內建在 hello 網路和 hello 應用程式層的保護。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-116">Each of these components has distributed denial of service (DDoS) protection built-in at hello network and hello app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="e0cbc-117">從 Azure 內部連線</span><span class="sxs-lookup"><span data-stu-id="e0cbc-117">Connectivity from within Azure</span></span>

<span data-ttu-id="e0cbc-118">如果您從 Azure 內部連線，該連線預設的連線原則為 [重新導向]。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="e0cbc-119">原則的**重新導向**表示 hello TCP 工作階段後建立的 toohello Azure SQL database 的連接，hello 用戶端工作階段則會重新導向的變更 toohello 目的地虛擬 ip 從 toohello proxy 中介軟體hello Azure SQL Database 閘道 toothat hello proxy 中介軟體。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-119">A policy of **Redirect** means that connections after hello TCP session is established toohello Azure SQL database, hello client session is then redirected toohello proxy middleware with a change toohello destination virtual IP from that of hello Azure SQL Database gateway toothat of hello proxy middleware.</span></span> <span data-ttu-id="e0cbc-120">此後，所有後續封包流程直接透過 hello proxy 中介軟體，並略過 hello Azure SQL Database 的閘道。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-120">Thereafter, all subsequent packets flow directly via hello proxy middleware, bypassing hello Azure SQL Database gateway.</span></span> <span data-ttu-id="e0cbc-121">hello 下列圖表說明此流量。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-121">hello following diagram illustrates this traffic flow.</span></span>

![架構概觀](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="e0cbc-123">從 Azure 外部連線</span><span class="sxs-lookup"><span data-stu-id="e0cbc-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="e0cbc-124">如果您從 Azure 外部連線，該連線預設的連線原則為 [Proxy]。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="e0cbc-125">原則的**Proxy**表示透過 hello Azure SQL Database 閘道建立 hello TCP 工作階段，所有後續封包流程透過 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-125">A policy of **Proxy** means that hello TCP session is established via hello Azure SQL Database gateway and all subsequent packets flow via hello gateway.</span></span> <span data-ttu-id="e0cbc-126">hello 下列圖表說明此流量。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-126">hello following diagram illustrates this traffic flow.</span></span>

![架構概觀](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="e0cbc-128">Azure SQL Database 閘道 IP 位址</span><span class="sxs-lookup"><span data-stu-id="e0cbc-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="e0cbc-129">tooconnect tooan Azure SQL database 與內部部署資源，您會需要 tooallow 輸出網路流量 toohello SQL Azure 閘道為您的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-129">tooconnect tooan Azure SQL database from on-premises resources, you need tooallow outbound network traffic toohello Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="e0cbc-130">在 Proxy 模式中，這是 hello 預設值，從內部部署資源連接時連接時，您的連接只能移到透過 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-130">Your connections only go via hello gateway when connecting in Proxy mode, which is hello default when connecting from on-premises resources.</span></span>

<span data-ttu-id="e0cbc-131">下表將列出 hello hello 主要和次要的所有資料區的 hello Azure SQL Database 閘道的 Ip。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-131">hello following table lists hello primary and secondary IPs of hello Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="e0cbc-132">對於某些區域，會有兩個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="e0cbc-133">在這些區域，hello 主要 IP 位址是 hello 目前閘道 IP 位址 hello 而且 hello 第二個 IP 位址的容錯移轉 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-133">In these regions, hello primary IP address is hello current IP address of hello gateway and hello second IP address is a failover IP address.</span></span> <span data-ttu-id="e0cbc-134">hello 容錯移轉的位址是 hello 位址 toowhich 我們可能會移動伺服器 tookeep hello 服務的可用性高。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-134">hello failover address is hello address toowhich we might move your server tookeep hello service availability high.</span></span> <span data-ttu-id="e0cbc-135">這些區域中，我們建議您允許輸出 tooboth hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-135">For these regions, we recommend that you allow outbound tooboth hello IP addresses.</span></span> <span data-ttu-id="e0cbc-136">hello 第二個 IP 位址由 Microsoft 所擁有並不會接聽任何服務之前啟動 Azure SQL Database tooaccept 連接。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-136">hello second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database tooaccept connections.</span></span>

| <span data-ttu-id="e0cbc-137">區域名稱</span><span class="sxs-lookup"><span data-stu-id="e0cbc-137">Region Name</span></span> | <span data-ttu-id="e0cbc-138">主要 IP 位址</span><span class="sxs-lookup"><span data-stu-id="e0cbc-138">Primary IP address</span></span> | <span data-ttu-id="e0cbc-139">次要 IP 位址</span><span class="sxs-lookup"><span data-stu-id="e0cbc-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="e0cbc-140">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-140">Australia East</span></span> | <span data-ttu-id="e0cbc-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="e0cbc-141">191.238.66.109</span></span> | <span data-ttu-id="e0cbc-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="e0cbc-142">13.75.149.87</span></span> |
| <span data-ttu-id="e0cbc-143">澳大利亞東南部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-143">Australia South East</span></span> | <span data-ttu-id="e0cbc-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="e0cbc-144">191.239.192.109</span></span> | <span data-ttu-id="e0cbc-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="e0cbc-145">13.73.109.251</span></span> |
| <span data-ttu-id="e0cbc-146">巴西南部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-146">Brazil South</span></span> | <span data-ttu-id="e0cbc-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="e0cbc-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="e0cbc-148">加拿大中部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-148">Canada Central</span></span> | <span data-ttu-id="e0cbc-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="e0cbc-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="e0cbc-150">加拿大東部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-150">Canada East</span></span> | <span data-ttu-id="e0cbc-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="e0cbc-151">40.86.226.166</span></span> | |
| <span data-ttu-id="e0cbc-152">美國中部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-152">Central US</span></span> | <span data-ttu-id="e0cbc-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="e0cbc-153">23.99.160.139</span></span> | <span data-ttu-id="e0cbc-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="e0cbc-154">13.67.215.62</span></span> |
| <span data-ttu-id="e0cbc-155">東亞</span><span class="sxs-lookup"><span data-stu-id="e0cbc-155">East Asia</span></span> | <span data-ttu-id="e0cbc-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="e0cbc-156">191.234.2.139</span></span> | <span data-ttu-id="e0cbc-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="e0cbc-157">52.175.33.150</span></span> |
| <span data-ttu-id="e0cbc-158">美國東部 1</span><span class="sxs-lookup"><span data-stu-id="e0cbc-158">East US 1</span></span> | <span data-ttu-id="e0cbc-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="e0cbc-159">191.238.6.43</span></span> | <span data-ttu-id="e0cbc-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="e0cbc-160">40.121.158.30</span></span> |
| <span data-ttu-id="e0cbc-161">美國東部 2</span><span class="sxs-lookup"><span data-stu-id="e0cbc-161">East US 2</span></span> | <span data-ttu-id="e0cbc-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="e0cbc-162">191.239.224.107</span></span> | <span data-ttu-id="e0cbc-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="e0cbc-163">40.79.84.180</span></span> |
| <span data-ttu-id="e0cbc-164">印度中部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-164">India Central</span></span> | <span data-ttu-id="e0cbc-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="e0cbc-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="e0cbc-166">印度南部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-166">India South</span></span> | <span data-ttu-id="e0cbc-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="e0cbc-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="e0cbc-168">印度西部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-168">India West</span></span> | <span data-ttu-id="e0cbc-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="e0cbc-169">104.211.160.80</span></span> | |
| <span data-ttu-id="e0cbc-170">日本東部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-170">Japan East</span></span> | <span data-ttu-id="e0cbc-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="e0cbc-171">191.237.240.43</span></span> | <span data-ttu-id="e0cbc-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="e0cbc-172">13.78.61.196</span></span> |
| <span data-ttu-id="e0cbc-173">日本西部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-173">Japan West</span></span> | <span data-ttu-id="e0cbc-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="e0cbc-174">191.238.68.11</span></span> | <span data-ttu-id="e0cbc-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="e0cbc-175">104.214.148.156</span></span> |
| <span data-ttu-id="e0cbc-176">韓國中部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-176">Korea Central</span></span> | <span data-ttu-id="e0cbc-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="e0cbc-177">52.231.32.42</span></span> | |
| <span data-ttu-id="e0cbc-178">韓國南部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-178">Korea South</span></span> | <span data-ttu-id="e0cbc-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="e0cbc-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="e0cbc-180">美國中北部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-180">North Central US</span></span> | <span data-ttu-id="e0cbc-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="e0cbc-181">23.98.55.75</span></span> | <span data-ttu-id="e0cbc-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="e0cbc-182">23.96.178.199</span></span> |
| <span data-ttu-id="e0cbc-183">北歐</span><span class="sxs-lookup"><span data-stu-id="e0cbc-183">North Europe</span></span> | <span data-ttu-id="e0cbc-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="e0cbc-184">191.235.193.75</span></span> | <span data-ttu-id="e0cbc-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="e0cbc-185">40.113.93.91</span></span> |
| <span data-ttu-id="e0cbc-186">美國中南部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-186">South Central US</span></span> | <span data-ttu-id="e0cbc-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="e0cbc-187">23.98.162.75</span></span> | <span data-ttu-id="e0cbc-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="e0cbc-188">13.66.62.124</span></span> |
| <span data-ttu-id="e0cbc-189">東南亞</span><span class="sxs-lookup"><span data-stu-id="e0cbc-189">South East Asia</span></span> | <span data-ttu-id="e0cbc-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="e0cbc-190">23.100.117.95</span></span> | <span data-ttu-id="e0cbc-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="e0cbc-191">104.43.15.0</span></span> |
| <span data-ttu-id="e0cbc-192">英國北部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-192">UK North</span></span> | <span data-ttu-id="e0cbc-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="e0cbc-193">13.87.97.210</span></span> | |
| <span data-ttu-id="e0cbc-194">英國南部 1</span><span class="sxs-lookup"><span data-stu-id="e0cbc-194">UK South 1</span></span> | <span data-ttu-id="e0cbc-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="e0cbc-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="e0cbc-196">英國南部 2</span><span class="sxs-lookup"><span data-stu-id="e0cbc-196">UK South 2</span></span> | <span data-ttu-id="e0cbc-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="e0cbc-197">13.87.34.7</span></span> | |
| <span data-ttu-id="e0cbc-198">英國西部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-198">UK West</span></span> | <span data-ttu-id="e0cbc-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="e0cbc-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="e0cbc-200">美國中西部</span><span class="sxs-lookup"><span data-stu-id="e0cbc-200">West Central US</span></span> | <span data-ttu-id="e0cbc-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="e0cbc-201">13.78.145.25</span></span> | |
| <span data-ttu-id="e0cbc-202">西歐</span><span class="sxs-lookup"><span data-stu-id="e0cbc-202">West Europe</span></span> | <span data-ttu-id="e0cbc-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="e0cbc-203">191.237.232.75</span></span> | <span data-ttu-id="e0cbc-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="e0cbc-204">40.68.37.158</span></span> |
| <span data-ttu-id="e0cbc-205">美國西部 1</span><span class="sxs-lookup"><span data-stu-id="e0cbc-205">West US 1</span></span> | <span data-ttu-id="e0cbc-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="e0cbc-206">23.99.34.75</span></span> | <span data-ttu-id="e0cbc-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="e0cbc-207">104.42.238.205</span></span> |
| <span data-ttu-id="e0cbc-208">美國西部 2</span><span class="sxs-lookup"><span data-stu-id="e0cbc-208">West US 2</span></span> | <span data-ttu-id="e0cbc-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="e0cbc-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="e0cbc-210">變更 Azure SQL Database 連線原則</span><span class="sxs-lookup"><span data-stu-id="e0cbc-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="e0cbc-211">toochange hello Azure SQL Database 伺服器，請使用 hello Azure SQL Database 連線原則[REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-211">toochange hello Azure SQL Database connection policy for an Azure SQL Database server, use hello [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="e0cbc-212">如果您連接的原則設定太**Proxy**，所有的網路封包流程透過 hello Azure SQL Database 的閘道。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-212">If your connection policy is set too**Proxy**, all network packets flow via hello Azure SQL Database gateway.</span></span> <span data-ttu-id="e0cbc-213">此設定，您需要 tooallow 輸出 tooonly hello Azure SQL Database 閘道 IP。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-213">For this setting, you need tooallow outbound tooonly hello Azure SQL Database gateway IP.</span></span> <span data-ttu-id="e0cbc-214">和 [重新導向] 設定相比，使用 [Proxy] 設定會較為延遲。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="e0cbc-215">如果您連接的原則設定**重新導向**，所有的網路封包直接傳送 toohello 中介軟體 proxy。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-215">If your connection policy is setting **Redirect**, all network packets flow directly toohello middleware proxy.</span></span> <span data-ttu-id="e0cbc-216">此設定，您需要 tooallow 輸出 toomultiple Ip。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-216">For this setting, you need tooallow outbound toomultiple IPs.</span></span> 

## <a name="script-toochange-connection-settings"></a><span data-ttu-id="e0cbc-217">指令碼 toochange 連線設定</span><span class="sxs-lookup"><span data-stu-id="e0cbc-217">Script toochange connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0cbc-218">此指令碼需要 hello [Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-218">This script requires hello [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="e0cbc-219">hello 下列 PowerShell 指令碼會示範如何 toochange hello 連線原則。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-219">hello following PowerShell script shows how toochange hello connection policy.</span></span>

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

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="e0cbc-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e0cbc-220">Next steps</span></span>

- <span data-ttu-id="e0cbc-221">如需如何 toochange hello Azure SQL Database 伺服器的 Azure SQL Database 連線原則資訊，請參閱[建立或更新伺服器的連線原則使用 hello REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-221">For information on how toochange hello Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using hello REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="e0cbc-222">如需使用 ADO.NET 4.5 或更新版本用戶端之 Azure SQL Database 連接行為的詳細資訊，請參閱 [ADO.NET 4.5 超過 1433以外的連接埠](sql-database-develop-direct-route-ports-adonet-v12.md)。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="e0cbc-223">如需一般應用程式開發概觀的資訊，請參閱 [SQL Database 應用程式開發概觀](sql-database-develop-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e0cbc-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>
