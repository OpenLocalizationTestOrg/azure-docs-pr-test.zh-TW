---
title: "Azure SQL Database 的資料表稽核、TDS 重新導向及 IP 端點 | Microsoft Docs"
description: "了解在 Azure SQL Database 中實作資料表稽核時的稽核、TDS 重新導向及 IP 端點變更。"
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: 
ms.assetid: 4ef19ed1-e798-43a2-ad99-0e563f93ab53
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: giladm
ms.openlocfilehash: d4a7e6658ec65a70bd7e07859e2a69acee58b7b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sql-database----downlevel-clients-support-and-ip-endpoint-changes-for-table-auditing"></a><span data-ttu-id="7e8c6-103">SQL Database - 資料表稽核的舊版用戶端支援與 IP 端點變更</span><span class="sxs-lookup"><span data-stu-id="7e8c6-103">SQL Database -  Downlevel clients support and IP endpoint changes for Table Auditing</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e8c6-104">本文件僅適用於資料表稽核，也就是**現已淘汰**。</span><span class="sxs-lookup"><span data-stu-id="7e8c6-104">This document applies only to Table Auditing, which is **now deprecated**.</span></span><br>
> <span data-ttu-id="7e8c6-105">請使用新的 [Blob 稽核](sql-database-auditing.md)方法，**不**需要修改舊版用戶端連接字串。</span><span class="sxs-lookup"><span data-stu-id="7e8c6-105">Please use the new [Blob Auditing](sql-database-auditing.md) method, which **does not** require downlevel client connection string modifications.</span></span> <span data-ttu-id="7e8c6-106">Blob 稽核的其他資訊位在[開始使用 SQL Database 稽核](sql-database-auditing.md)。</span><span class="sxs-lookup"><span data-stu-id="7e8c6-106">Additional info on Blob Auditing can be found in [Get started with SQL database auditing](sql-database-auditing.md).</span></span>

<span data-ttu-id="7e8c6-107">[資料庫稽核](sql-database-auditing.md)可自動與支援 TDS 重新導向的 SQL 用戶端搭配運作。</span><span class="sxs-lookup"><span data-stu-id="7e8c6-107">[Database Auditing](sql-database-auditing.md) works automatically with SQL clients that support TDS redirection.</span></span> <span data-ttu-id="7e8c6-108">請注意，使用「Blob 稽核」方法時，不適用重新導向。</span><span class="sxs-lookup"><span data-stu-id="7e8c6-108">Note that redirection does not apply when using the Blob Auditing method.</span></span>

## <span data-ttu-id="7e8c6-109"><a id="subheading-1"></a>舊版用戶端支援</span><span class="sxs-lookup"><span data-stu-id="7e8c6-109"><a id="subheading-1"></a>Downlevel clients support</span></span>
<span data-ttu-id="7e8c6-110">實作 TDS 7.4 的任何用戶端應該也支援重新導向。</span><span class="sxs-lookup"><span data-stu-id="7e8c6-110">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="7e8c6-111">例外包括其中未完全支援重新導向功能的 JDBC 4.0，和其中未實作重新導向的 Tedious for Node.JS。</span><span class="sxs-lookup"><span data-stu-id="7e8c6-111">Exceptions to this include JDBC 4.0 in which the redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="7e8c6-112">對於「舊版用戶端」，也就是支援 TDS 7.3 版和以下版本 - 應該修改連接字串中的伺服器 FQDN：</span><span class="sxs-lookup"><span data-stu-id="7e8c6-112">For "Downlevel clients", i.e. which support TDS version 7.3 and below - the server FQDN in the connection string should be modified:</span></span>

<span data-ttu-id="7e8c6-113">連接字串中的原始伺服器 FQDN：<*伺服器名稱*>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="7e8c6-113">Original server FQDN in the connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="7e8c6-114">連接字串中已修改的伺服器 FQDN：<*伺服器名稱*>.database.**secure**.windows.net</span><span class="sxs-lookup"><span data-stu-id="7e8c6-114">Modified server FQDN in the connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="7e8c6-115">「舊版用戶端」的部分清單包括：</span><span class="sxs-lookup"><span data-stu-id="7e8c6-115">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="7e8c6-116">.NET 4.0 和以下版本，</span><span class="sxs-lookup"><span data-stu-id="7e8c6-116">.NET 4.0 and below,</span></span>
* <span data-ttu-id="7e8c6-117">ODBC 10.0 和以下版本。</span><span class="sxs-lookup"><span data-stu-id="7e8c6-117">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="7e8c6-118">JDBC (雖然 JDBC 支援 TDS 7.4，但並未完整支援 TDS 重新導向功能)</span><span class="sxs-lookup"><span data-stu-id="7e8c6-118">JDBC (while JDBC does support TDS 7.4, the TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="7e8c6-119">Tedious (適用於 Node.JS)</span><span class="sxs-lookup"><span data-stu-id="7e8c6-119">Tedious (for Node.JS)</span></span>

<span data-ttu-id="7e8c6-120">**備註：** 上述伺服器 FDQN 修改可能會對於套用 SQL Server 層級稽核原則有所助益，不需要每個資料庫中的組態步驟 (暫存緩和)。</span><span class="sxs-lookup"><span data-stu-id="7e8c6-120">**Remark:** The above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>

## <span data-ttu-id="7e8c6-121"><a id="subheading-2"></a>啟用稽核的 IP 端點變更</span><span class="sxs-lookup"><span data-stu-id="7e8c6-121"><a id="subheading-2"></a>IP endpoint changes when enabling Auditing</span></span>
<span data-ttu-id="7e8c6-122">請注意，當您啟用「資料表稽核」時，您資料庫的 IP 端點將會變更。</span><span class="sxs-lookup"><span data-stu-id="7e8c6-122">Please note that when you enable Table Auditing, the IP endpoint of your database will change.</span></span> <span data-ttu-id="7e8c6-123">如果您有嚴格的防火牆設定，請適當更新這些防火牆設定。</span><span class="sxs-lookup"><span data-stu-id="7e8c6-123">If you have strict firewall settings, please update those firewall settings accordingly.</span></span>

<span data-ttu-id="7e8c6-124">新的資料庫 IP 端點將取決於資料庫區域：</span><span class="sxs-lookup"><span data-stu-id="7e8c6-124">The new database IP endpoint will depend on the database region:</span></span>

| <span data-ttu-id="7e8c6-125">資料庫區域</span><span class="sxs-lookup"><span data-stu-id="7e8c6-125">Database Region</span></span> | <span data-ttu-id="7e8c6-126">可能的 IP 端點</span><span class="sxs-lookup"><span data-stu-id="7e8c6-126">Possible IP endpoints</span></span> |
| --- | --- |
| <span data-ttu-id="7e8c6-127">中國北部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-127">China North</span></span> |<span data-ttu-id="7e8c6-128">139.217.29.176, 139.217.28.254</span><span class="sxs-lookup"><span data-stu-id="7e8c6-128">139.217.29.176, 139.217.28.254</span></span> |
| <span data-ttu-id="7e8c6-129">中國東部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-129">China East</span></span> |<span data-ttu-id="7e8c6-130">42.159.245.65, 42.159.246.245</span><span class="sxs-lookup"><span data-stu-id="7e8c6-130">42.159.245.65, 42.159.246.245</span></span> |
| <span data-ttu-id="7e8c6-131">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-131">Australia East</span></span> |<span data-ttu-id="7e8c6-132">104.210.91.32, 40.126.244.159, 191.239.64.60, 40.126.255.94</span><span class="sxs-lookup"><span data-stu-id="7e8c6-132">104.210.91.32, 40.126.244.159, 191.239.64.60, 40.126.255.94</span></span> |
| <span data-ttu-id="7e8c6-133">澳洲東南部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-133">Australia Southeast</span></span> |<span data-ttu-id="7e8c6-134">191.239.184.223, 40.127.85.81, 191.239.161.83, 40.127.81.130</span><span class="sxs-lookup"><span data-stu-id="7e8c6-134">191.239.184.223, 40.127.85.81, 191.239.161.83, 40.127.81.130</span></span> |
| <span data-ttu-id="7e8c6-135">巴西南部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-135">Brazil South</span></span> |<span data-ttu-id="7e8c6-136">104.41.44.161, 104.41.62.230, 23.97.99.54, 104.41.59.191</span><span class="sxs-lookup"><span data-stu-id="7e8c6-136">104.41.44.161, 104.41.62.230, 23.97.99.54, 104.41.59.191</span></span> |
| <span data-ttu-id="7e8c6-137">美國中部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-137">Central US</span></span> |<span data-ttu-id="7e8c6-138">104.43.255.70, 40.83.14.7, 23.99.128.244, 40.83.15.176</span><span class="sxs-lookup"><span data-stu-id="7e8c6-138">104.43.255.70, 40.83.14.7, 23.99.128.244, 40.83.15.176</span></span> |
| <span data-ttu-id="7e8c6-139">美國中部 EUAP</span><span class="sxs-lookup"><span data-stu-id="7e8c6-139">Central US EUAP</span></span> |<span data-ttu-id="7e8c6-140">52.180.178.16, 52.180.176.190</span><span class="sxs-lookup"><span data-stu-id="7e8c6-140">52.180.178.16, 52.180.176.190</span></span> |
| <span data-ttu-id="7e8c6-141">東亞</span><span class="sxs-lookup"><span data-stu-id="7e8c6-141">East Asia</span></span> |<span data-ttu-id="7e8c6-142">23.99.125.133, 13.75.40.42, 23.97.71.138, 13.94.43.245</span><span class="sxs-lookup"><span data-stu-id="7e8c6-142">23.99.125.133, 13.75.40.42, 23.97.71.138, 13.94.43.245</span></span> |
| <span data-ttu-id="7e8c6-143">美國東部 2</span><span class="sxs-lookup"><span data-stu-id="7e8c6-143">East US 2</span></span> |<span data-ttu-id="7e8c6-144">104.209.141.31, 104.208.238.177, 191.237.131.51, 104.208.235.50</span><span class="sxs-lookup"><span data-stu-id="7e8c6-144">104.209.141.31, 104.208.238.177, 191.237.131.51, 104.208.235.50</span></span> |
| <span data-ttu-id="7e8c6-145">美國東部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-145">East US</span></span> |<span data-ttu-id="7e8c6-146">23.96.107.223, 104.41.150.122, 23.96.38.170, 104.41.146.44</span><span class="sxs-lookup"><span data-stu-id="7e8c6-146">23.96.107.223, 104.41.150.122, 23.96.38.170, 104.41.146.44</span></span> |
| <span data-ttu-id="7e8c6-147">美國東部 EUAP</span><span class="sxs-lookup"><span data-stu-id="7e8c6-147">East US EUAP</span></span> |<span data-ttu-id="7e8c6-148">52.225.190.86, 52.225.191.187</span><span class="sxs-lookup"><span data-stu-id="7e8c6-148">52.225.190.86, 52.225.191.187</span></span> |
| <span data-ttu-id="7e8c6-149">印度中部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-149">Central India</span></span> |<span data-ttu-id="7e8c6-150">104.211.98.219, 104.211.103.71</span><span class="sxs-lookup"><span data-stu-id="7e8c6-150">104.211.98.219, 104.211.103.71</span></span> |
| <span data-ttu-id="7e8c6-151">印度南部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-151">South India</span></span> |<span data-ttu-id="7e8c6-152">104.211.227.102, 104.211.225.157</span><span class="sxs-lookup"><span data-stu-id="7e8c6-152">104.211.227.102, 104.211.225.157</span></span> |
| <span data-ttu-id="7e8c6-153">印度西部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-153">West India</span></span> |<span data-ttu-id="7e8c6-154">104.211.161.152, 104.211.162.21</span><span class="sxs-lookup"><span data-stu-id="7e8c6-154">104.211.161.152, 104.211.162.21</span></span> |
| <span data-ttu-id="7e8c6-155">日本東部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-155">Japan East</span></span> |<span data-ttu-id="7e8c6-156">104.41.179.1, 40.115.253.81, 23.102.64.207, 40.115.250.196</span><span class="sxs-lookup"><span data-stu-id="7e8c6-156">104.41.179.1, 40.115.253.81, 23.102.64.207, 40.115.250.196</span></span> |
| <span data-ttu-id="7e8c6-157">日本西部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-157">Japan West</span></span> |<span data-ttu-id="7e8c6-158">104.214.140.140, 104.214.146.31, 191.233.32.34, 104.214.146.198</span><span class="sxs-lookup"><span data-stu-id="7e8c6-158">104.214.140.140, 104.214.146.31, 191.233.32.34, 104.214.146.198</span></span> |
| <span data-ttu-id="7e8c6-159">美國中北部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-159">North Central US</span></span> |<span data-ttu-id="7e8c6-160">191.236.155.178, 23.96.192.130, 23.96.177.169, 23.96.193.231</span><span class="sxs-lookup"><span data-stu-id="7e8c6-160">191.236.155.178, 23.96.192.130, 23.96.177.169, 23.96.193.231</span></span> |
| <span data-ttu-id="7e8c6-161">北歐</span><span class="sxs-lookup"><span data-stu-id="7e8c6-161">North Europe</span></span> |<span data-ttu-id="7e8c6-162">104.41.209.221, 40.85.139.245, 137.116.251.66, 40.85.142.176</span><span class="sxs-lookup"><span data-stu-id="7e8c6-162">104.41.209.221, 40.85.139.245, 137.116.251.66, 40.85.142.176</span></span> |
| <span data-ttu-id="7e8c6-163">美國中南部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-163">South Central US</span></span> |<span data-ttu-id="7e8c6-164">191.238.184.128, 40.84.190.84, 23.102.160.153, 40.84.186.66</span><span class="sxs-lookup"><span data-stu-id="7e8c6-164">191.238.184.128, 40.84.190.84, 23.102.160.153, 40.84.186.66</span></span> |
| <span data-ttu-id="7e8c6-165">東南亞</span><span class="sxs-lookup"><span data-stu-id="7e8c6-165">Southeast Asia</span></span> |<span data-ttu-id="7e8c6-166">104.215.198.156, 13.76.252.200, 23.97.51.109, 13.76.252.113</span><span class="sxs-lookup"><span data-stu-id="7e8c6-166">104.215.198.156, 13.76.252.200, 23.97.51.109, 13.76.252.113</span></span> |
| <span data-ttu-id="7e8c6-167">西歐</span><span class="sxs-lookup"><span data-stu-id="7e8c6-167">West Europe</span></span> |<span data-ttu-id="7e8c6-168">104.40.230.120, 13.80.23.64, 137.117.171.161, 13.80.8.37, 104.47.167.215, 40.118.56.193, 104.40.176.73, 40.118.56.20</span><span class="sxs-lookup"><span data-stu-id="7e8c6-168">104.40.230.120, 13.80.23.64, 137.117.171.161, 13.80.8.37, 104.47.167.215, 40.118.56.193, 104.40.176.73, 40.118.56.20</span></span> |
| <span data-ttu-id="7e8c6-169">美國西部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-169">West US</span></span> |<span data-ttu-id="7e8c6-170">191.236.123.146, 138.91.163.240, 168.62.194.148, 23.99.6.91</span><span class="sxs-lookup"><span data-stu-id="7e8c6-170">191.236.123.146, 138.91.163.240, 168.62.194.148, 23.99.6.91</span></span> |
| <span data-ttu-id="7e8c6-171">美國西部 2</span><span class="sxs-lookup"><span data-stu-id="7e8c6-171">West US 2</span></span> |<span data-ttu-id="7e8c6-172">13.66.224.156, 13.66.227.8</span><span class="sxs-lookup"><span data-stu-id="7e8c6-172">13.66.224.156, 13.66.227.8</span></span> |
| <span data-ttu-id="7e8c6-173">美國中西部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-173">West Central US</span></span> |<span data-ttu-id="7e8c6-174">52.161.29.186, 52.161.27.213</span><span class="sxs-lookup"><span data-stu-id="7e8c6-174">52.161.29.186, 52.161.27.213</span></span> |
| <span data-ttu-id="7e8c6-175">加拿大中部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-175">Canada Central</span></span> |<span data-ttu-id="7e8c6-176">13.88.248.106, 13.88.248.110</span><span class="sxs-lookup"><span data-stu-id="7e8c6-176">13.88.248.106, 13.88.248.110</span></span> |
| <span data-ttu-id="7e8c6-177">加拿大東部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-177">Canada East</span></span> |<span data-ttu-id="7e8c6-178">40.86.227.82, 40.86.225.194</span><span class="sxs-lookup"><span data-stu-id="7e8c6-178">40.86.227.82, 40.86.225.194</span></span> |
| <span data-ttu-id="7e8c6-179">英國北部</span><span class="sxs-lookup"><span data-stu-id="7e8c6-179">UK North</span></span> |<span data-ttu-id="7e8c6-180">13.87.101.18, 13.87.100.232</span><span class="sxs-lookup"><span data-stu-id="7e8c6-180">13.87.101.18, 13.87.100.232</span></span> |
| <span data-ttu-id="7e8c6-181">英國南部 2</span><span class="sxs-lookup"><span data-stu-id="7e8c6-181">UK South 2</span></span> |<span data-ttu-id="7e8c6-182">13.87.32.202, 13.87.32.226</span><span class="sxs-lookup"><span data-stu-id="7e8c6-182">13.87.32.202, 13.87.32.226</span></span> |
