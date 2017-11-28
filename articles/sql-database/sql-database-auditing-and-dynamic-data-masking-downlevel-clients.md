---
title: "aaaTable 稽核，TDS 重新導向，和 Azure SQL Database 的 IP 端點 |Microsoft 文件"
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
ms.openlocfilehash: 966c23f92fab6fa459a515ad841bb2d5f75436aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database----downlevel-clients-support-and-ip-endpoint-changes-for-table-auditing"></a><span data-ttu-id="ee150-103">SQL Database - 資料表稽核的舊版用戶端支援與 IP 端點變更</span><span class="sxs-lookup"><span data-stu-id="ee150-103">SQL Database -  Downlevel clients support and IP endpoint changes for Table Auditing</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee150-104">這份文件適用於僅 tooTable 稽核，也就是**現在已被取代**。</span><span class="sxs-lookup"><span data-stu-id="ee150-104">This document applies only tooTable Auditing, which is **now deprecated**.</span></span><br>
> <span data-ttu-id="ee150-105">請使用新 hello [Blob 稽核](sql-database-auditing.md)方法，其中**不**需要舊版用戶端連接字串修改。</span><span class="sxs-lookup"><span data-stu-id="ee150-105">Please use hello new [Blob Auditing](sql-database-auditing.md) method, which **does not** require downlevel client connection string modifications.</span></span> <span data-ttu-id="ee150-106">Blob 稽核的其他資訊位在[開始使用 SQL Database 稽核](sql-database-auditing.md)。</span><span class="sxs-lookup"><span data-stu-id="ee150-106">Additional info on Blob Auditing can be found in [Get started with SQL database auditing](sql-database-auditing.md).</span></span>

<span data-ttu-id="ee150-107">[資料庫稽核](sql-database-auditing.md)可自動與支援 TDS 重新導向的 SQL 用戶端搭配運作。</span><span class="sxs-lookup"><span data-stu-id="ee150-107">[Database Auditing](sql-database-auditing.md) works automatically with SQL clients that support TDS redirection.</span></span> <span data-ttu-id="ee150-108">請注意使用 hello Blob 稽核方法時，將不會套用該重新導向。</span><span class="sxs-lookup"><span data-stu-id="ee150-108">Note that redirection does not apply when using hello Blob Auditing method.</span></span>

## <span data-ttu-id="ee150-109"><a id="subheading-1"></a>舊版用戶端支援</span><span class="sxs-lookup"><span data-stu-id="ee150-109"><a id="subheading-1"></a>Downlevel clients support</span></span>
<span data-ttu-id="ee150-110">實作 TDS 7.4 的任何用戶端應該也支援重新導向。</span><span class="sxs-lookup"><span data-stu-id="ee150-110">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="ee150-111">例外狀況 toothis 納入 JDBC 4.0 的 hello 重新導向功能不完全支援和 Tedious for Node.JS 不會實作重新導向時。</span><span class="sxs-lookup"><span data-stu-id="ee150-111">Exceptions toothis include JDBC 4.0 in which hello redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="ee150-112">「 下層用戶端 」，也就是它支援 TDS 版本 7.3，且以下-hello hello 連接字串中的伺服器 FQDN 應修改：</span><span class="sxs-lookup"><span data-stu-id="ee150-112">For "Downlevel clients", i.e. which support TDS version 7.3 and below - hello server FQDN in hello connection string should be modified:</span></span>

<span data-ttu-id="ee150-113">原始伺服器 FQDN hello 連接字串中： <*伺服器名稱*>。.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="ee150-113">Original server FQDN in hello connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="ee150-114">已修改的伺服器 FQDN hello 連接字串中： <*伺服器名稱*>.database。**安全**。 windows.net</span><span class="sxs-lookup"><span data-stu-id="ee150-114">Modified server FQDN in hello connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="ee150-115">「舊版用戶端」的部分清單包括：</span><span class="sxs-lookup"><span data-stu-id="ee150-115">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="ee150-116">.NET 4.0 和以下版本，</span><span class="sxs-lookup"><span data-stu-id="ee150-116">.NET 4.0 and below,</span></span>
* <span data-ttu-id="ee150-117">ODBC 10.0 和以下版本。</span><span class="sxs-lookup"><span data-stu-id="ee150-117">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="ee150-118">JDBC （雖然 JDBC 可支援 TDS 7.4，hello TDS 重新導向功能不完全支援）</span><span class="sxs-lookup"><span data-stu-id="ee150-118">JDBC (while JDBC does support TDS 7.4, hello TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="ee150-119">Tedious (適用於 Node.JS)</span><span class="sxs-lookup"><span data-stu-id="ee150-119">Tedious (for Node.JS)</span></span>

<span data-ttu-id="ee150-120">**備註：** hello 上述伺服器 FDQN 修改可能會有所助益也沒有需要的設定步驟 （暫存緩和） 每個資料庫中套用 SQL Server 層級稽核原則。</span><span class="sxs-lookup"><span data-stu-id="ee150-120">**Remark:** hello above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>

## <span data-ttu-id="ee150-121"><a id="subheading-2"></a>啟用稽核的 IP 端點變更</span><span class="sxs-lookup"><span data-stu-id="ee150-121"><a id="subheading-2"></a>IP endpoint changes when enabling Auditing</span></span>
<span data-ttu-id="ee150-122">請注意，當您啟用稽核資料表，會變更資料庫的 hello IP 端點。</span><span class="sxs-lookup"><span data-stu-id="ee150-122">Please note that when you enable Table Auditing, hello IP endpoint of your database will change.</span></span> <span data-ttu-id="ee150-123">如果您有嚴格的防火牆設定，請適當更新這些防火牆設定。</span><span class="sxs-lookup"><span data-stu-id="ee150-123">If you have strict firewall settings, please update those firewall settings accordingly.</span></span>

<span data-ttu-id="ee150-124">hello 新資料庫 IP 端點將取決於 hello 資料庫區域：</span><span class="sxs-lookup"><span data-stu-id="ee150-124">hello new database IP endpoint will depend on hello database region:</span></span>

| <span data-ttu-id="ee150-125">資料庫區域</span><span class="sxs-lookup"><span data-stu-id="ee150-125">Database Region</span></span> | <span data-ttu-id="ee150-126">可能的 IP 端點</span><span class="sxs-lookup"><span data-stu-id="ee150-126">Possible IP endpoints</span></span> |
| --- | --- |
| <span data-ttu-id="ee150-127">中國北部</span><span class="sxs-lookup"><span data-stu-id="ee150-127">China North</span></span> |<span data-ttu-id="ee150-128">139.217.29.176, 139.217.28.254</span><span class="sxs-lookup"><span data-stu-id="ee150-128">139.217.29.176, 139.217.28.254</span></span> |
| <span data-ttu-id="ee150-129">中國東部</span><span class="sxs-lookup"><span data-stu-id="ee150-129">China East</span></span> |<span data-ttu-id="ee150-130">42.159.245.65, 42.159.246.245</span><span class="sxs-lookup"><span data-stu-id="ee150-130">42.159.245.65, 42.159.246.245</span></span> |
| <span data-ttu-id="ee150-131">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="ee150-131">Australia East</span></span> |<span data-ttu-id="ee150-132">104.210.91.32, 40.126.244.159, 191.239.64.60, 40.126.255.94</span><span class="sxs-lookup"><span data-stu-id="ee150-132">104.210.91.32, 40.126.244.159, 191.239.64.60, 40.126.255.94</span></span> |
| <span data-ttu-id="ee150-133">澳洲東南部</span><span class="sxs-lookup"><span data-stu-id="ee150-133">Australia Southeast</span></span> |<span data-ttu-id="ee150-134">191.239.184.223, 40.127.85.81, 191.239.161.83, 40.127.81.130</span><span class="sxs-lookup"><span data-stu-id="ee150-134">191.239.184.223, 40.127.85.81, 191.239.161.83, 40.127.81.130</span></span> |
| <span data-ttu-id="ee150-135">巴西南部</span><span class="sxs-lookup"><span data-stu-id="ee150-135">Brazil South</span></span> |<span data-ttu-id="ee150-136">104.41.44.161, 104.41.62.230, 23.97.99.54, 104.41.59.191</span><span class="sxs-lookup"><span data-stu-id="ee150-136">104.41.44.161, 104.41.62.230, 23.97.99.54, 104.41.59.191</span></span> |
| <span data-ttu-id="ee150-137">美國中部</span><span class="sxs-lookup"><span data-stu-id="ee150-137">Central US</span></span> |<span data-ttu-id="ee150-138">104.43.255.70, 40.83.14.7, 23.99.128.244, 40.83.15.176</span><span class="sxs-lookup"><span data-stu-id="ee150-138">104.43.255.70, 40.83.14.7, 23.99.128.244, 40.83.15.176</span></span> |
| <span data-ttu-id="ee150-139">美國中部 EUAP</span><span class="sxs-lookup"><span data-stu-id="ee150-139">Central US EUAP</span></span> |<span data-ttu-id="ee150-140">52.180.178.16, 52.180.176.190</span><span class="sxs-lookup"><span data-stu-id="ee150-140">52.180.178.16, 52.180.176.190</span></span> |
| <span data-ttu-id="ee150-141">東亞</span><span class="sxs-lookup"><span data-stu-id="ee150-141">East Asia</span></span> |<span data-ttu-id="ee150-142">23.99.125.133, 13.75.40.42, 23.97.71.138, 13.94.43.245</span><span class="sxs-lookup"><span data-stu-id="ee150-142">23.99.125.133, 13.75.40.42, 23.97.71.138, 13.94.43.245</span></span> |
| <span data-ttu-id="ee150-143">美國東部 2</span><span class="sxs-lookup"><span data-stu-id="ee150-143">East US 2</span></span> |<span data-ttu-id="ee150-144">104.209.141.31, 104.208.238.177, 191.237.131.51, 104.208.235.50</span><span class="sxs-lookup"><span data-stu-id="ee150-144">104.209.141.31, 104.208.238.177, 191.237.131.51, 104.208.235.50</span></span> |
| <span data-ttu-id="ee150-145">美國東部</span><span class="sxs-lookup"><span data-stu-id="ee150-145">East US</span></span> |<span data-ttu-id="ee150-146">23.96.107.223, 104.41.150.122, 23.96.38.170, 104.41.146.44</span><span class="sxs-lookup"><span data-stu-id="ee150-146">23.96.107.223, 104.41.150.122, 23.96.38.170, 104.41.146.44</span></span> |
| <span data-ttu-id="ee150-147">美國東部 EUAP</span><span class="sxs-lookup"><span data-stu-id="ee150-147">East US EUAP</span></span> |<span data-ttu-id="ee150-148">52.225.190.86, 52.225.191.187</span><span class="sxs-lookup"><span data-stu-id="ee150-148">52.225.190.86, 52.225.191.187</span></span> |
| <span data-ttu-id="ee150-149">印度中部</span><span class="sxs-lookup"><span data-stu-id="ee150-149">Central India</span></span> |<span data-ttu-id="ee150-150">104.211.98.219, 104.211.103.71</span><span class="sxs-lookup"><span data-stu-id="ee150-150">104.211.98.219, 104.211.103.71</span></span> |
| <span data-ttu-id="ee150-151">印度南部</span><span class="sxs-lookup"><span data-stu-id="ee150-151">South India</span></span> |<span data-ttu-id="ee150-152">104.211.227.102, 104.211.225.157</span><span class="sxs-lookup"><span data-stu-id="ee150-152">104.211.227.102, 104.211.225.157</span></span> |
| <span data-ttu-id="ee150-153">印度西部</span><span class="sxs-lookup"><span data-stu-id="ee150-153">West India</span></span> |<span data-ttu-id="ee150-154">104.211.161.152, 104.211.162.21</span><span class="sxs-lookup"><span data-stu-id="ee150-154">104.211.161.152, 104.211.162.21</span></span> |
| <span data-ttu-id="ee150-155">日本東部</span><span class="sxs-lookup"><span data-stu-id="ee150-155">Japan East</span></span> |<span data-ttu-id="ee150-156">104.41.179.1, 40.115.253.81, 23.102.64.207, 40.115.250.196</span><span class="sxs-lookup"><span data-stu-id="ee150-156">104.41.179.1, 40.115.253.81, 23.102.64.207, 40.115.250.196</span></span> |
| <span data-ttu-id="ee150-157">日本西部</span><span class="sxs-lookup"><span data-stu-id="ee150-157">Japan West</span></span> |<span data-ttu-id="ee150-158">104.214.140.140, 104.214.146.31, 191.233.32.34, 104.214.146.198</span><span class="sxs-lookup"><span data-stu-id="ee150-158">104.214.140.140, 104.214.146.31, 191.233.32.34, 104.214.146.198</span></span> |
| <span data-ttu-id="ee150-159">美國中北部</span><span class="sxs-lookup"><span data-stu-id="ee150-159">North Central US</span></span> |<span data-ttu-id="ee150-160">191.236.155.178, 23.96.192.130, 23.96.177.169, 23.96.193.231</span><span class="sxs-lookup"><span data-stu-id="ee150-160">191.236.155.178, 23.96.192.130, 23.96.177.169, 23.96.193.231</span></span> |
| <span data-ttu-id="ee150-161">北歐</span><span class="sxs-lookup"><span data-stu-id="ee150-161">North Europe</span></span> |<span data-ttu-id="ee150-162">104.41.209.221, 40.85.139.245, 137.116.251.66, 40.85.142.176</span><span class="sxs-lookup"><span data-stu-id="ee150-162">104.41.209.221, 40.85.139.245, 137.116.251.66, 40.85.142.176</span></span> |
| <span data-ttu-id="ee150-163">美國中南部</span><span class="sxs-lookup"><span data-stu-id="ee150-163">South Central US</span></span> |<span data-ttu-id="ee150-164">191.238.184.128, 40.84.190.84, 23.102.160.153, 40.84.186.66</span><span class="sxs-lookup"><span data-stu-id="ee150-164">191.238.184.128, 40.84.190.84, 23.102.160.153, 40.84.186.66</span></span> |
| <span data-ttu-id="ee150-165">東南亞</span><span class="sxs-lookup"><span data-stu-id="ee150-165">Southeast Asia</span></span> |<span data-ttu-id="ee150-166">104.215.198.156, 13.76.252.200, 23.97.51.109, 13.76.252.113</span><span class="sxs-lookup"><span data-stu-id="ee150-166">104.215.198.156, 13.76.252.200, 23.97.51.109, 13.76.252.113</span></span> |
| <span data-ttu-id="ee150-167">西歐</span><span class="sxs-lookup"><span data-stu-id="ee150-167">West Europe</span></span> |<span data-ttu-id="ee150-168">104.40.230.120, 13.80.23.64, 137.117.171.161, 13.80.8.37, 104.47.167.215, 40.118.56.193, 104.40.176.73, 40.118.56.20</span><span class="sxs-lookup"><span data-stu-id="ee150-168">104.40.230.120, 13.80.23.64, 137.117.171.161, 13.80.8.37, 104.47.167.215, 40.118.56.193, 104.40.176.73, 40.118.56.20</span></span> |
| <span data-ttu-id="ee150-169">美國西部</span><span class="sxs-lookup"><span data-stu-id="ee150-169">West US</span></span> |<span data-ttu-id="ee150-170">191.236.123.146, 138.91.163.240, 168.62.194.148, 23.99.6.91</span><span class="sxs-lookup"><span data-stu-id="ee150-170">191.236.123.146, 138.91.163.240, 168.62.194.148, 23.99.6.91</span></span> |
| <span data-ttu-id="ee150-171">美國西部 2</span><span class="sxs-lookup"><span data-stu-id="ee150-171">West US 2</span></span> |<span data-ttu-id="ee150-172">13.66.224.156, 13.66.227.8</span><span class="sxs-lookup"><span data-stu-id="ee150-172">13.66.224.156, 13.66.227.8</span></span> |
| <span data-ttu-id="ee150-173">美國中西部</span><span class="sxs-lookup"><span data-stu-id="ee150-173">West Central US</span></span> |<span data-ttu-id="ee150-174">52.161.29.186, 52.161.27.213</span><span class="sxs-lookup"><span data-stu-id="ee150-174">52.161.29.186, 52.161.27.213</span></span> |
| <span data-ttu-id="ee150-175">加拿大中部</span><span class="sxs-lookup"><span data-stu-id="ee150-175">Canada Central</span></span> |<span data-ttu-id="ee150-176">13.88.248.106, 13.88.248.110</span><span class="sxs-lookup"><span data-stu-id="ee150-176">13.88.248.106, 13.88.248.110</span></span> |
| <span data-ttu-id="ee150-177">加拿大東部</span><span class="sxs-lookup"><span data-stu-id="ee150-177">Canada East</span></span> |<span data-ttu-id="ee150-178">40.86.227.82, 40.86.225.194</span><span class="sxs-lookup"><span data-stu-id="ee150-178">40.86.227.82, 40.86.225.194</span></span> |
| <span data-ttu-id="ee150-179">英國北部</span><span class="sxs-lookup"><span data-stu-id="ee150-179">UK North</span></span> |<span data-ttu-id="ee150-180">13.87.101.18, 13.87.100.232</span><span class="sxs-lookup"><span data-stu-id="ee150-180">13.87.101.18, 13.87.100.232</span></span> |
| <span data-ttu-id="ee150-181">英國南部 2</span><span class="sxs-lookup"><span data-stu-id="ee150-181">UK South 2</span></span> |<span data-ttu-id="ee150-182">13.87.32.202, 13.87.32.226</span><span class="sxs-lookup"><span data-stu-id="ee150-182">13.87.32.202, 13.87.32.226</span></span> |
