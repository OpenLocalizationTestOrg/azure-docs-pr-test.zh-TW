---
title: "aaaSupported 在 Azure 資料目錄中的資料來源 |Microsoft 文件"
description: "本文列出 hello 目前支援的資料來源的規格。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: jstevens
editor: 
tags: 
ms.assetid: fd4345ca-2ed8-4c5e-9c4b-f954be2fc9f9
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 4bfcabf31bf9fd781c939a5026abc42a5407df32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="supported-data-sources-in-azure-data-catalog"></a><span data-ttu-id="9f98a-103">Azure 資料目錄中支援的資料來源</span><span class="sxs-lookup"><span data-stu-id="9f98a-103">Supported data sources in Azure Data Catalog</span></span>

<span data-ttu-id="9f98a-104">您可以使用公用 API 或按一下 發佈中繼資料-一次註冊工具，或直接 toohello Azure 資料目錄入口網站手動輸入資訊。</span><span class="sxs-lookup"><span data-stu-id="9f98a-104">You can publish metadata by using a public API or a click-once registration tool, or by manually entering information directly toohello Azure Data Catalog web portal.</span></span> <span data-ttu-id="9f98a-105">hello 下表摘要說明會受到 hello 目錄今天，而且每個 hello 的發行功能的所有資料來源。</span><span class="sxs-lookup"><span data-stu-id="9f98a-105">hello following table summarizes all data sources that are supported by hello catalog today, and hello publishing capabilities for each.</span></span> <span data-ttu-id="9f98a-106">也列出 hello 外部資料工具時，每個資料來源可啟動從我們 「 開啟位置 」 的入口網站的經驗。</span><span class="sxs-lookup"><span data-stu-id="9f98a-106">Also listed are hello external data tools that each data source can launch from our portal "open-in" experience.</span></span> <span data-ttu-id="9f98a-107">hello 第二個資料表包含每個資料來源連接屬性的詳細技術規格。</span><span class="sxs-lookup"><span data-stu-id="9f98a-107">hello second table contains a more technical specification of each data-source connection property.</span></span>


## <a name="list-of-supported-data-sources"></a><span data-ttu-id="9f98a-108">支援的資料來源的清單</span><span class="sxs-lookup"><span data-stu-id="9f98a-108">List of supported data sources</span></span>

<table>
    <tr>
       <td><span data-ttu-id="9f98a-109"><b>資料來源物件</b></span><span class="sxs-lookup"><span data-stu-id="9f98a-109"><b>Data source object</b></span></span></td>
       <td><span data-ttu-id="9f98a-110"><b>API</b></span><span class="sxs-lookup"><span data-stu-id="9f98a-110"><b>API</b></span></span></td>
       <td><span data-ttu-id="9f98a-111"><b>手動輸入</b></span><span class="sxs-lookup"><span data-stu-id="9f98a-111"><b>Manual entry</b></span></span></td>
       <td><span data-ttu-id="9f98a-112"><b>註冊工具</b></span><span class="sxs-lookup"><span data-stu-id="9f98a-112"><b>Registration tool</b></span></span></td>
       <td><span data-ttu-id="9f98a-113"><b>開啟工具</b></span><span class="sxs-lookup"><span data-stu-id="9f98a-113"><b>Open-in tools</b></span></span></td>
       <td><span data-ttu-id="9f98a-114"><b>注意事項</b></span><span class="sxs-lookup"><span data-stu-id="9f98a-114"><b>Notes</b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-115">Azure Data Lake Store 目錄</span><span class="sxs-lookup"><span data-stu-id="9f98a-115">Azure Data Lake Store directory</span></span></td>
      <td><span data-ttu-id="9f98a-116">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-116">✓</span></span></td>
      <td><span data-ttu-id="9f98a-117">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-117">✓</span></span></td>
      <td><span data-ttu-id="9f98a-118">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-118">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-119">Azure Data Lake Store 檔案</span><span class="sxs-lookup"><span data-stu-id="9f98a-119">Azure Data Lake Store file</span></span></td>
      <td><span data-ttu-id="9f98a-120">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-120">✓</span></span></td>
      <td><span data-ttu-id="9f98a-121">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-121">✓</span></span></td>
      <td><span data-ttu-id="9f98a-122">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-122">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-123">Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="9f98a-123">Azure Blob storage</span></span></td>
      <td><span data-ttu-id="9f98a-124">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-124">✓</span></span></td>
      <td><span data-ttu-id="9f98a-125">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-125">✓</span></span></td>
      <td><span data-ttu-id="9f98a-126">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-126">✓</span></span></td>
      <td><span data-ttu-id="9f98a-127"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-127"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-128">Azure 儲存體目錄</span><span class="sxs-lookup"><span data-stu-id="9f98a-128">Azure Storage directory</span></span></td>
      <td><span data-ttu-id="9f98a-129">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-129">✓</span></span></td>
      <td><span data-ttu-id="9f98a-130">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-130">✓</span></span></td>
      <td><span data-ttu-id="9f98a-131">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-131">✓</span></span></td>
      <td><span data-ttu-id="9f98a-132"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-132"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-133">Azure 儲存體資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-133">Azure Storage table</span></span></td>
      <td><span data-ttu-id="9f98a-134">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-134">✓</span></span></td>
      <td><span data-ttu-id="9f98a-135">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-135">✓</span></span></td>
      <td><span data-ttu-id="9f98a-136">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-136">✓</span></span></td>
      <td>
        <font size="2"></font>
      </td>
      <td>
        <font size="2"></font>
      </td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-137">HDFS 目錄</span><span class="sxs-lookup"><span data-stu-id="9f98a-137">HDFS directory</span></span></td>
      <td><span data-ttu-id="9f98a-138">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-138">✓</span></span></td>
      <td><span data-ttu-id="9f98a-139">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-139">✓</span></span></td>
      <td><span data-ttu-id="9f98a-140">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-140">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-141">HDFS 檔案</span><span class="sxs-lookup"><span data-stu-id="9f98a-141">HDFS file</span></span></td>
      <td><span data-ttu-id="9f98a-142">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-142">✓</span></span></td>
      <td><span data-ttu-id="9f98a-143">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-143">✓</span></span></td>
      <td><span data-ttu-id="9f98a-144">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-144">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-145">Hive 資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-145">Hive table</span></span></td>
      <td><span data-ttu-id="9f98a-146">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-146">✓</span></span></td>
      <td><span data-ttu-id="9f98a-147">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-147">✓</span></span></td>
      <td><span data-ttu-id="9f98a-148">✓</span><span class="sxs-lookup"><span data-stu-id="9f98a-148">✓</span></span></td>
      <td><span data-ttu-id="9f98a-149"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-149"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-150">Hive 檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-150">Hive view</span></span></td>
      <td><span data-ttu-id="9f98a-151">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-151">✓</span></span></td>
      <td><span data-ttu-id="9f98a-152">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-152">✓</span></span></td>
      <td><span data-ttu-id="9f98a-153">✓</span><span class="sxs-lookup"><span data-stu-id="9f98a-153">✓</span></span></td>
      <td><span data-ttu-id="9f98a-154"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-154"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-155">MySQL 資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-155">MySQL table</span></span></td>
      <td><span data-ttu-id="9f98a-156">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-156">✓</span></span></td>
      <td><span data-ttu-id="9f98a-157">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-157">✓</span></span></td>
      <td><span data-ttu-id="9f98a-158">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-158">✓</span></span></td>
      <td><span data-ttu-id="9f98a-159"><font size=2>Excel、Power BI</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-159"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-160">MySQL 檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-160">MySQL view</span></span></td>
      <td><span data-ttu-id="9f98a-161">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-161">✓</span></span></td>
      <td><span data-ttu-id="9f98a-162">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-162">✓</span></span></td>
      <td><span data-ttu-id="9f98a-163">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-163">✓</span></span></td>
      <td><span data-ttu-id="9f98a-164"><font size=2>Excel、Power BI</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-164"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-165">Oracle 資料庫資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-165">Oracle Database table</span></span></td>
      <td><span data-ttu-id="9f98a-166">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-166">✓</span></span></td>
      <td><span data-ttu-id="9f98a-167">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-167">✓</span></span></td>
      <td><span data-ttu-id="9f98a-168">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-168">✓</span></span></td>
      <td><span data-ttu-id="9f98a-169"><font size=2>Excel、Power BI</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-169"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-170">Oracle 資料庫檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-170">Oracle Database view</span></span></td>
      <td><span data-ttu-id="9f98a-171">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-171">✓</span></span></td>
      <td><span data-ttu-id="9f98a-172">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-172">✓</span></span></td>
      <td><span data-ttu-id="9f98a-173">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-173">✓</span></span></td>
      <td><span data-ttu-id="9f98a-174"><font size=2>Excel、Power BI</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-174"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-175">其他 (一般資產)</span><span class="sxs-lookup"><span data-stu-id="9f98a-175">Other (generic asset)</span></span></td>
      <td><span data-ttu-id="9f98a-176">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-176">✓</span></span></td>
      <td><span data-ttu-id="9f98a-177">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-177">✓</span></span></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-178">Azure SQL 資料倉儲資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-178">Azure SQL Data Warehouse table</span></span></td>
      <td><span data-ttu-id="9f98a-179">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-179">✓</span></span></td>
      <td><span data-ttu-id="9f98a-180">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-180">✓</span></span></td>
      <td><span data-ttu-id="9f98a-181">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-181">✓</span></span></td>
      <td><span data-ttu-id="9f98a-182"><font size=2>Excel、Power BI、SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-182"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-183">SQL 資料倉儲檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-183">SQL Data Warehouse view</span></span></td>
      <td><span data-ttu-id="9f98a-184">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-184">✓</span></span></td>
      <td><span data-ttu-id="9f98a-185">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-185">✓</span></span></td>
      <td><span data-ttu-id="9f98a-186">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-186">✓</span></span></td>
      <td><span data-ttu-id="9f98a-187"><font size=2>Excel、Power BI、SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-187"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-188">SQL Server Analysis Services 維度</span><span class="sxs-lookup"><span data-stu-id="9f98a-188">SQL Server Analysis Services dimension</span></span></td>
      <td><span data-ttu-id="9f98a-189">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-189">✓</span></span></td>
      <td><span data-ttu-id="9f98a-190">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-190">✓</span></span></td>
      <td><span data-ttu-id="9f98a-191">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-191">✓</span></span></td>
      <td><span data-ttu-id="9f98a-192"><font size=2>Excel、Power BI</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-192"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-193">SQL Server Analysis Services KPI</span><span class="sxs-lookup"><span data-stu-id="9f98a-193">SQL Server Analysis Services KPI</span></span></td>
      <td><span data-ttu-id="9f98a-194">✓</span><span class="sxs-lookup"><span data-stu-id="9f98a-194">✓</span></span></td>
      <td><span data-ttu-id="9f98a-195">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-195">✓</span></span></td>
      <td><span data-ttu-id="9f98a-196">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-196">✓</span></span></td>
      <td><span data-ttu-id="9f98a-197"><font size=2>Excel、Power BI</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-197"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-198">SQL Server Analysis Services 量值</span><span class="sxs-lookup"><span data-stu-id="9f98a-198">SQL Server Analysis Services measure</span></span></td>
      <td><span data-ttu-id="9f98a-199">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-199">✓</span></span></td>
      <td><span data-ttu-id="9f98a-200">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-200">✓</span></span></td>
      <td><span data-ttu-id="9f98a-201">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-201">✓</span></span></td>
      <td><span data-ttu-id="9f98a-202"><font size=2>Excel、Power BI</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-202"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-203">SQL Server Analysis Services 資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-203">SQL Server Analysis Services table</span></span></td>
      <td><span data-ttu-id="9f98a-204">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-204">✓</span></span></td>
      <td><span data-ttu-id="9f98a-205">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-205">✓</span></span></td>
      <td><span data-ttu-id="9f98a-206">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-206">✓</span></span></td>
      <td><span data-ttu-id="9f98a-207"><font size=2>Excel、Power BI</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-207"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-208">SQL Server Reporting Services 報表</span><span class="sxs-lookup"><span data-stu-id="9f98a-208">SQL Server Reporting Services report</span></span></td>
      <td><span data-ttu-id="9f98a-209">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-209">✓</span></span></td>
      <td><span data-ttu-id="9f98a-210">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-210">✓</span></span></td>
      <td><span data-ttu-id="9f98a-211">✓</span><span class="sxs-lookup"><span data-stu-id="9f98a-211">✓</span></span></td>
      <td><span data-ttu-id="9f98a-212"><font size=2>[瀏覽器]</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-212"><font size=2>Browser</font></span></span></td>
      <td><span data-ttu-id="9f98a-213"><font size=2>僅限原生模式伺服器。不支援 SharePoint 模式。</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-213"><font size=2>Native mode servers only. SharePoint mode is not supported.</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-214">SQL Server 資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-214">SQL Server table</span></span></td>
      <td><span data-ttu-id="9f98a-215">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-215">✓</span></span></td>
      <td><span data-ttu-id="9f98a-216">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-216">✓</span></span></td>
      <td><span data-ttu-id="9f98a-217">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-217">✓</span></span></td>
      <td><span data-ttu-id="9f98a-218"><font size=2>Excel、Power BI、SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-218"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-219">SQL Server 檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-219">SQL Server view</span></span></td>
      <td><span data-ttu-id="9f98a-220">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-220">✓</span></span></td>
      <td><span data-ttu-id="9f98a-221">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-221">✓</span></span></td>
      <td><span data-ttu-id="9f98a-222">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-222">✓</span></span></td>
      <td><span data-ttu-id="9f98a-223"><font size=2>Excel、Power BI、SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-223"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-224">Teradata 資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-224">Teradata table</span></span></td>
      <td><span data-ttu-id="9f98a-225">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-225">✓</span></span></td>
      <td><span data-ttu-id="9f98a-226">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-226">✓</span></span></td>
      <td><span data-ttu-id="9f98a-227">✓</span><span class="sxs-lookup"><span data-stu-id="9f98a-227">✓</span></span></td>
      <td><span data-ttu-id="9f98a-228"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-228"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-229">Teradata 檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-229">Teradata view</span></span></td>
      <td><span data-ttu-id="9f98a-230">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-230">✓</span></span></td>
      <td><span data-ttu-id="9f98a-231">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-231">✓</span></span></td>
      <td><span data-ttu-id="9f98a-232">✓</span><span class="sxs-lookup"><span data-stu-id="9f98a-232">✓</span></span></td>
      <td><span data-ttu-id="9f98a-233"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-233"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-234">SAP HANA 檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-234">SAP HANA view</span></span></td>
      <td><span data-ttu-id="9f98a-235">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-235">✓</span></span></td>
      <td><span data-ttu-id="9f98a-236">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-236">✓</span></span></td>
      <td><span data-ttu-id="9f98a-237">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-237">✓</span></span></td>
      <td><span data-ttu-id="9f98a-238"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-238"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-239">DB2 資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-239">DB2 table</span></span></td>
      <td><span data-ttu-id="9f98a-240">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-240">✓</span></span></td>
      <td><span data-ttu-id="9f98a-241">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-241">✓</span></span></td>
      <td><span data-ttu-id="9f98a-242">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-242">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-243">DB2 檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-243">DB2 view</span></span></td>
      <td><span data-ttu-id="9f98a-244">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-244">✓</span></span></td>
      <td><span data-ttu-id="9f98a-245">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-245">✓</span></span></td>
      <td><span data-ttu-id="9f98a-246">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-246">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-247">檔案系統檔案</span><span class="sxs-lookup"><span data-stu-id="9f98a-247">File system file</span></span></td>
      <td><span data-ttu-id="9f98a-248">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-248">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-249">FTP 目錄</span><span class="sxs-lookup"><span data-stu-id="9f98a-249">FTP directory</span></span></td>
      <td><span data-ttu-id="9f98a-250">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-250">✓</span></span></td>
      <td><span data-ttu-id="9f98a-251">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-251">✓</span></span></td>
      <td><span data-ttu-id="9f98a-252">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-252">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-253">FTP 檔案</span><span class="sxs-lookup"><span data-stu-id="9f98a-253">FTP file</span></span></td>
      <td><span data-ttu-id="9f98a-254">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-254">✓</span></span></td>
      <td><span data-ttu-id="9f98a-255">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-255">✓</span></span></td>
      <td><span data-ttu-id="9f98a-256">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-256">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-257">HTTP 報告</span><span class="sxs-lookup"><span data-stu-id="9f98a-257">HTTP report</span></span></td>
      <td><span data-ttu-id="9f98a-258">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-258">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-259">HTTP 端點</span><span class="sxs-lookup"><span data-stu-id="9f98a-259">HTTP endpoint</span></span></td>
      <td><span data-ttu-id="9f98a-260">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-260">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-261">HTTP 檔案</span><span class="sxs-lookup"><span data-stu-id="9f98a-261">HTTP file</span></span></td>
      <td><span data-ttu-id="9f98a-262">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-262">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-263">OData 實體集</span><span class="sxs-lookup"><span data-stu-id="9f98a-263">OData entity set</span></span></td>
      <td><span data-ttu-id="9f98a-264">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-264">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-265">OData 函式</span><span class="sxs-lookup"><span data-stu-id="9f98a-265">OData function</span></span></td>
      <td><span data-ttu-id="9f98a-266">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-266">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-267">PostgreSQL 資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-267">PostgreSQL table</span></span></td>
      <td><span data-ttu-id="9f98a-268">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-268">✓</span></span></td>
      <td><span data-ttu-id="9f98a-269">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-269">✓</span></span></td>
      <td><span data-ttu-id="9f98a-270">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-270">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-271">PostgreSQL 檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-271">PostgreSQL view</span></span></td>
      <td><span data-ttu-id="9f98a-272">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-272">✓</span></span></td>
      <td><span data-ttu-id="9f98a-273">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-273">✓</span></span></td>
      <td><span data-ttu-id="9f98a-274">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-274">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-275">SAP HANA 檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-275">SAP HANA view</span></span></td>
      <td><span data-ttu-id="9f98a-276">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-276">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td> <span data-ttu-id="9f98a-277">Salesforce 物件</span><span class="sxs-lookup"><span data-stu-id="9f98a-277">Salesforce object</span></span></td>
      <td><span data-ttu-id="9f98a-278">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-278">✓</span></span></td>
      <td><span data-ttu-id="9f98a-279">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-279">✓</span></span></td>
      <td><span data-ttu-id="9f98a-280">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-280">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-281">SharePoint 清單</span><span class="sxs-lookup"><span data-stu-id="9f98a-281">SharePoint list</span></span> </td>
      <td><span data-ttu-id="9f98a-282">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-282">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-283">Azure Cosmos DB 集合</span><span class="sxs-lookup"><span data-stu-id="9f98a-283">Azure Cosmos DB collection</span></span></td>
      <td><span data-ttu-id="9f98a-284">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-284">✓</span></span></td>
      <td><span data-ttu-id="9f98a-285">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-285">✓</span></span></td>
      <td><span data-ttu-id="9f98a-286">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-286">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-287">一般 ODBC 資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-287">Generic ODBC table</span></span></td>
      <td><span data-ttu-id="9f98a-288">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-288">✓</span></span></td>
      <td><span data-ttu-id="9f98a-289">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-289">✓</span></span></td>
      <td><span data-ttu-id="9f98a-290">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-290">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-291">一般 ODBC 檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-291">Generic ODBC view</span></span></td>
      <td><span data-ttu-id="9f98a-292">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-292">✓</span></span></td>
      <td><span data-ttu-id="9f98a-293">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-293">✓</span></span></td>
      <td><span data-ttu-id="9f98a-294">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-294">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-295">Cassandra 資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-295">Cassandra table</span></span></td>
      <td><span data-ttu-id="9f98a-296">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-296">✓</span></span></td>
      <td><span data-ttu-id="9f98a-297">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-297">✓</span></span></td>
      <td><span data-ttu-id="9f98a-298">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-298">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="9f98a-299"><font size=2>以一般 ODBC 資產形式發佈</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-299"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-300">Cassandra 檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-300">Cassandra view</span></span></td>
      <td><span data-ttu-id="9f98a-301">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-301">✓</span></span></td>
      <td><span data-ttu-id="9f98a-302">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-302">✓</span></span></td>
      <td><span data-ttu-id="9f98a-303">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-303">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="9f98a-304"><font size=2>以一般 ODBC 資產形式發佈</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-304"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-305">Sybase 資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-305">Sybase table</span></span></td>
      <td><span data-ttu-id="9f98a-306">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-306">✓</span></span></td>
      <td><span data-ttu-id="9f98a-307">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-307">✓</span></span></td>
      <td><span data-ttu-id="9f98a-308">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-308">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-309">Sybase 檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-309">Sybase view</span></span></td>
      <td><span data-ttu-id="9f98a-310">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-310">✓</span></span></td>
      <td><span data-ttu-id="9f98a-311">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-311">✓</span></span></td>
      <td><span data-ttu-id="9f98a-312">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-312">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-313">MongoDB 資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-313">MongoDB table</span></span></td>
      <td><span data-ttu-id="9f98a-314">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-314">✓</span></span></td>
      <td><span data-ttu-id="9f98a-315">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-315">✓</span></span></td>
      <td><span data-ttu-id="9f98a-316">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-316">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="9f98a-317"><font size=2>以一般 ODBC 資產形式發佈</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-317"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-318">MongoDB 檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-318">MongoDB view</span></span></td>
      <td><span data-ttu-id="9f98a-319">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-319">✓</span></span></td>
      <td><span data-ttu-id="9f98a-320">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-320">✓</span></span></td>
      <td><span data-ttu-id="9f98a-321">✓ </span><span class="sxs-lookup"><span data-stu-id="9f98a-321">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="9f98a-322"><font size=2>以一般 ODBC 資產形式發佈</font></span><span class="sxs-lookup"><span data-stu-id="9f98a-322"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
</table>

<span data-ttu-id="9f98a-323">如果您需要支援的其他來源，提出功能要求 toohello [Azure 資料目錄論壇](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="9f98a-323">If you need support for additional sources, submit a feature request toohello [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span></span>


## <a name="data-source-reference-specification"></a><span data-ttu-id="9f98a-324">資料來源參考規格</span><span class="sxs-lookup"><span data-stu-id="9f98a-324">Data-source reference specification</span></span>
> [!NOTE]
> <span data-ttu-id="9f98a-325">hello **DSL 結構**hello 下表中的資料行列出只有 hello 連接屬性 「 位址 」 屬性包所使用的 Azure 資料目錄。</span><span class="sxs-lookup"><span data-stu-id="9f98a-325">hello **DSL structure** column in hello following table lists only hello connection properties for "address" property bag that are used by Azure Data Catalog.</span></span> <span data-ttu-id="9f98a-326">也就是 「 位址 」 屬性包可包含 hello 資料來源的 Azure 資料目錄持續發生，但是不會使用其他連接屬性。</span><span class="sxs-lookup"><span data-stu-id="9f98a-326">That is, "address" property bag can contain other connection properties of hello data source which Azure Data Catalog persists, but does not use.</span></span>

<table>
    <tr>
       <td><span data-ttu-id="9f98a-327"><b>來源類型</b></span><span class="sxs-lookup"><span data-stu-id="9f98a-327"><b>Source type</b></span></span></td>
       <td><span data-ttu-id="9f98a-328"><b>資產類型</b></span><span class="sxs-lookup"><span data-stu-id="9f98a-328"><b>Asset type</b></span></span></td>
       <td><span data-ttu-id="9f98a-329"><b>物件類型</b></span><span class="sxs-lookup"><span data-stu-id="9f98a-329"><b>Object types</b></span></span></td>
       <td><span data-ttu-id="9f98a-330"><b>DSL 結構<b></span><span class="sxs-lookup"><span data-stu-id="9f98a-330"><b>DSL structure<b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-331">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="9f98a-331">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="9f98a-332">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-332">Container</span></span></td>
      <td><span data-ttu-id="9f98a-333">資料湖</span><span class="sxs-lookup"><span data-stu-id="9f98a-333">Data Lake</span></span></td>
      <td><span data-ttu-id="9f98a-334">
        <font size=2> 通訊協定：webhdfs</span><span class="sxs-lookup"><span data-stu-id="9f98a-334">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="9f98a-335">驗證：{基本、oauth}</span><span class="sxs-lookup"><span data-stu-id="9f98a-335">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="9f98a-336">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-336">Address:</span></span> <br><span data-ttu-id="9f98a-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-338">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="9f98a-338">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="9f98a-339">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-339">Table</span></span></td>
      <td><span data-ttu-id="9f98a-340">目錄、檔案</span><span class="sxs-lookup"><span data-stu-id="9f98a-340">Directory, file</span></span></td>
      <td><span data-ttu-id="9f98a-341">
        <font size=2> 通訊協定：webhdfs</span><span class="sxs-lookup"><span data-stu-id="9f98a-341">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="9f98a-342">驗證：{基本、oauth}</span><span class="sxs-lookup"><span data-stu-id="9f98a-342">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="9f98a-343">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-343">Address:</span></span> <br><span data-ttu-id="9f98a-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-345">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="9f98a-345">Azure Storage</span></span></td>
      <td><span data-ttu-id="9f98a-346">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-346">Container</span></span></td>
      <td><span data-ttu-id="9f98a-347">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-347">Container</span></span></td>
      <td><span data-ttu-id="9f98a-348">
        <font size=2> 通訊協定︰azure-blobs</span><span class="sxs-lookup"><span data-stu-id="9f98a-348">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="9f98a-349">驗證：{azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="9f98a-349">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="9f98a-350">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-350">Address:</span></span> <br><span data-ttu-id="9f98a-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="9f98a-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="9f98a-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 帳戶</span><span class="sxs-lookup"><span data-stu-id="9f98a-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="9f98a-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 容器 </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-354">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="9f98a-354">Azure Storage</span></span></td>
      <td><span data-ttu-id="9f98a-355">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-355">Table</span></span></td>
      <td><span data-ttu-id="9f98a-356">Blob、目錄</span><span class="sxs-lookup"><span data-stu-id="9f98a-356">Blob, directory</span></span></td>
      <td><span data-ttu-id="9f98a-357">
        <font size=2> 通訊協定︰azure-blobs</span><span class="sxs-lookup"><span data-stu-id="9f98a-357">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="9f98a-358">驗證：{azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="9f98a-358">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="9f98a-359">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-359">Address:</span></span> <br><span data-ttu-id="9f98a-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="9f98a-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="9f98a-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 帳戶</span><span class="sxs-lookup"><span data-stu-id="9f98a-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="9f98a-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span></span> <br><span data-ttu-id="9f98a-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-364">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="9f98a-364">Azure Storage</span></span></td>
      <td><span data-ttu-id="9f98a-365">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-365">Container</span></span></td>
      <td><span data-ttu-id="9f98a-366">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-366">Container</span></span></td>
      <td><span data-ttu-id="9f98a-367">
        <font size=2> 通訊協定：azure-tables</span><span class="sxs-lookup"><span data-stu-id="9f98a-367">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="9f98a-368">驗證：{azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="9f98a-368">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="9f98a-369">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-369">Address:</span></span> <br><span data-ttu-id="9f98a-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="9f98a-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="9f98a-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 帳戶 </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-372">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="9f98a-372">Azure Storage</span></span></td>
      <td><span data-ttu-id="9f98a-373">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-373">Table</span></span></td>
      <td><span data-ttu-id="9f98a-374">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-374">Table</span></span></td>
      <td><span data-ttu-id="9f98a-375">
        <font size=2> 通訊協定：azure-tables</span><span class="sxs-lookup"><span data-stu-id="9f98a-375">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="9f98a-376">驗證：{azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="9f98a-376">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="9f98a-377">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-377">Address:</span></span> <br><span data-ttu-id="9f98a-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="9f98a-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="9f98a-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 帳戶</span><span class="sxs-lookup"><span data-stu-id="9f98a-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="9f98a-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-381">Cosmos</span><span class="sxs-lookup"><span data-stu-id="9f98a-381">Cosmos</span></span></td>
      <td><span data-ttu-id="9f98a-382">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-382">Container</span></span></td>
      <td><span data-ttu-id="9f98a-383">虛擬叢集</span><span class="sxs-lookup"><span data-stu-id="9f98a-383">Virtual cluster</span></span></td>
      <td><span data-ttu-id="9f98a-384">
        <font size=2> 通訊協定：cosmos</span><span class="sxs-lookup"><span data-stu-id="9f98a-384">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="9f98a-385">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-385">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="9f98a-386">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-386">Address:</span></span> <br><span data-ttu-id="9f98a-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-388">Cosmos</span><span class="sxs-lookup"><span data-stu-id="9f98a-388">Cosmos</span></span></td>
      <td><span data-ttu-id="9f98a-389">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-389">Table</span></span></td>
      <td><span data-ttu-id="9f98a-390">資料流、資料流集、檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-390">Stream, stream set, view</span></span></td>
      <td><span data-ttu-id="9f98a-391">
        <font size=2> 通訊協定：cosmos</span><span class="sxs-lookup"><span data-stu-id="9f98a-391">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="9f98a-392">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-392">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="9f98a-393">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-393">Address:</span></span> <br><span data-ttu-id="9f98a-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-395">Datazen</span><span class="sxs-lookup"><span data-stu-id="9f98a-395">Datazen</span></span></td>
      <td><span data-ttu-id="9f98a-396">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-396">Container</span></span></td>
      <td><span data-ttu-id="9f98a-397">網站</span><span class="sxs-lookup"><span data-stu-id="9f98a-397">Site</span></span></td>
      <td><span data-ttu-id="9f98a-398">
        <font size=2> 通訊協定：http</span><span class="sxs-lookup"><span data-stu-id="9f98a-398">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="9f98a-399">驗證：{無、基本、windows、oauth}</span><span class="sxs-lookup"><span data-stu-id="9f98a-399">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="9f98a-400">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-400">Address:</span></span> <br><span data-ttu-id="9f98a-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-402">Datazen</span><span class="sxs-lookup"><span data-stu-id="9f98a-402">Datazen</span></span></td>
      <td><span data-ttu-id="9f98a-403">報告</span><span class="sxs-lookup"><span data-stu-id="9f98a-403">Report</span></span></td>
      <td><span data-ttu-id="9f98a-404">報告、儀表板</span><span class="sxs-lookup"><span data-stu-id="9f98a-404">Report, dashboard</span></span></td>
      <td><span data-ttu-id="9f98a-405">
        <font size=2> 通訊協定：http</span><span class="sxs-lookup"><span data-stu-id="9f98a-405">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="9f98a-406">驗證：{無、基本、windows、oauth}</span><span class="sxs-lookup"><span data-stu-id="9f98a-406">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="9f98a-407">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-407">Address:</span></span> <br><span data-ttu-id="9f98a-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-409">DB2</span><span class="sxs-lookup"><span data-stu-id="9f98a-409">DB2</span></span></td>
      <td><span data-ttu-id="9f98a-410">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-410">Container</span></span></td>
      <td><span data-ttu-id="9f98a-411">資料庫</span><span class="sxs-lookup"><span data-stu-id="9f98a-411">Database</span></span></td>
      <td><span data-ttu-id="9f98a-412">
        <font size=2> 通訊協定：db2</span><span class="sxs-lookup"><span data-stu-id="9f98a-412">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="9f98a-413">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-413">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="9f98a-414">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-414">Address:</span></span> <br><span data-ttu-id="9f98a-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-417">DB2</span><span class="sxs-lookup"><span data-stu-id="9f98a-417">DB2</span></span></td>
      <td><span data-ttu-id="9f98a-418">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-418">Table</span></span></td>
      <td><span data-ttu-id="9f98a-419">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-419">Table, view</span></span></td>
      <td><span data-ttu-id="9f98a-420">
        <font size=2> 通訊協定：db2</span><span class="sxs-lookup"><span data-stu-id="9f98a-420">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="9f98a-421">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-421">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="9f98a-422">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-422">Address:</span></span> <br><span data-ttu-id="9f98a-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="9f98a-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="9f98a-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-427">檔案系統</span><span class="sxs-lookup"><span data-stu-id="9f98a-427">File system</span></span></td>
      <td><span data-ttu-id="9f98a-428">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-428">Table</span></span></td>
      <td><span data-ttu-id="9f98a-429">檔案</span><span class="sxs-lookup"><span data-stu-id="9f98a-429">File</span></span></td>
      <td><span data-ttu-id="9f98a-430">
        <font size=2> 通訊協定：file</span><span class="sxs-lookup"><span data-stu-id="9f98a-430">
        <font size=2> Protocol: file</span></span> <br><span data-ttu-id="9f98a-431">驗證：{無、基本、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-431">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="9f98a-432">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-432">Address:</span></span> <br><span data-ttu-id="9f98a-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-434">FTP</span><span class="sxs-lookup"><span data-stu-id="9f98a-434">FTP</span></span></td>
      <td><span data-ttu-id="9f98a-435">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-435">Table</span></span></td>
      <td><span data-ttu-id="9f98a-436">目錄、檔案</span><span class="sxs-lookup"><span data-stu-id="9f98a-436">Directory, file</span></span></td>
      <td><span data-ttu-id="9f98a-437">
        <font size=2> 通訊協定：ftp</span><span class="sxs-lookup"><span data-stu-id="9f98a-437">
        <font size=2> Protocol: ftp</span></span> <br><span data-ttu-id="9f98a-438">驗證：{無、基本、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-438">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="9f98a-439">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-439">Address:</span></span> <br><span data-ttu-id="9f98a-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-441">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="9f98a-441">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="9f98a-442">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-442">Container</span></span></td>
      <td><span data-ttu-id="9f98a-443">叢集</span><span class="sxs-lookup"><span data-stu-id="9f98a-443">Cluster</span></span></td>
      <td><span data-ttu-id="9f98a-444">
        <font size=2> 通訊協定：webhdfs</span><span class="sxs-lookup"><span data-stu-id="9f98a-444">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="9f98a-445">驗證：{基本、oauth}</span><span class="sxs-lookup"><span data-stu-id="9f98a-445">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="9f98a-446">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-446">Address:</span></span> <br><span data-ttu-id="9f98a-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-448">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="9f98a-448">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="9f98a-449">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-449">Table</span></span></td>
      <td><span data-ttu-id="9f98a-450">目錄、檔案</span><span class="sxs-lookup"><span data-stu-id="9f98a-450">Directory, file</span></span></td>
      <td><span data-ttu-id="9f98a-451">
        <font size=2> 通訊協定：webhdfs</span><span class="sxs-lookup"><span data-stu-id="9f98a-451">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="9f98a-452">驗證：{基本、oauth}</span><span class="sxs-lookup"><span data-stu-id="9f98a-452">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="9f98a-453">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-453">Address:</span></span> <br><span data-ttu-id="9f98a-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-455">Hive</span><span class="sxs-lookup"><span data-stu-id="9f98a-455">Hive</span></span></td>
      <td><span data-ttu-id="9f98a-456">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-456">Container</span></span></td>
      <td><span data-ttu-id="9f98a-457">資料庫</span><span class="sxs-lookup"><span data-stu-id="9f98a-457">Database</span></span></td>
      <td><span data-ttu-id="9f98a-458">
        <font size=2> 通訊協定︰hive</span><span class="sxs-lookup"><span data-stu-id="9f98a-458">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="9f98a-459">驗證：{HDInsight、基本、使用者名稱、無}</span><span class="sxs-lookup"><span data-stu-id="9f98a-459">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="9f98a-460">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-460">Address:</span></span> <br><span data-ttu-id="9f98a-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-463">connectionProperties︰</span><span class="sxs-lookup"><span data-stu-id="9f98a-463">connectionProperties:</span></span> <br><span data-ttu-id="9f98a-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-465">Hive</span><span class="sxs-lookup"><span data-stu-id="9f98a-465">Hive</span></span></td>
      <td><span data-ttu-id="9f98a-466">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-466">Table</span></span></td>
      <td><span data-ttu-id="9f98a-467">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-467">Table, view</span></span></td>
      <td><span data-ttu-id="9f98a-468">
        <font size=2> 通訊協定︰hive</span><span class="sxs-lookup"><span data-stu-id="9f98a-468">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="9f98a-469">驗證：{HDInsight、基本、使用者名稱、無}</span><span class="sxs-lookup"><span data-stu-id="9f98a-469">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="9f98a-470">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-470">Address:</span></span> <br><span data-ttu-id="9f98a-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="9f98a-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="9f98a-474">connectionProperties︰</span><span class="sxs-lookup"><span data-stu-id="9f98a-474">connectionProperties:</span></span> <br><span data-ttu-id="9f98a-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-476">HTTP</span><span class="sxs-lookup"><span data-stu-id="9f98a-476">HTTP</span></span></td>
      <td><span data-ttu-id="9f98a-477">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-477">Container</span></span></td>
      <td><span data-ttu-id="9f98a-478">網站</span><span class="sxs-lookup"><span data-stu-id="9f98a-478">Site</span></span></td>
      <td><span data-ttu-id="9f98a-479">
        <font size=2> 通訊協定：http</span><span class="sxs-lookup"><span data-stu-id="9f98a-479">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="9f98a-480">驗證：{無、基本、windows、oauth}</span><span class="sxs-lookup"><span data-stu-id="9f98a-480">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="9f98a-481">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-481">Address:</span></span> <br><span data-ttu-id="9f98a-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-483">HTTP</span><span class="sxs-lookup"><span data-stu-id="9f98a-483">HTTP</span></span></td>
      <td><span data-ttu-id="9f98a-484">報告</span><span class="sxs-lookup"><span data-stu-id="9f98a-484">Report</span></span></td>
      <td><span data-ttu-id="9f98a-485">報告、儀表板</span><span class="sxs-lookup"><span data-stu-id="9f98a-485">Report, dashboard</span></span></td>
      <td><span data-ttu-id="9f98a-486">
        <font size=2> 通訊協定：http</span><span class="sxs-lookup"><span data-stu-id="9f98a-486">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="9f98a-487">驗證：{無、基本、windows、oauth}</span><span class="sxs-lookup"><span data-stu-id="9f98a-487">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="9f98a-488">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-488">Address:</span></span> <br><span data-ttu-id="9f98a-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-490">HTTP</span><span class="sxs-lookup"><span data-stu-id="9f98a-490">HTTP</span></span></td>
      <td><span data-ttu-id="9f98a-491">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-491">Table</span></span></td>
      <td><span data-ttu-id="9f98a-492">端點、檔案</span><span class="sxs-lookup"><span data-stu-id="9f98a-492">Endpoint, file</span></span></td>
      <td><span data-ttu-id="9f98a-493">
        <font size=2> 通訊協定：http</span><span class="sxs-lookup"><span data-stu-id="9f98a-493">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="9f98a-494">驗證：{無、基本、windows、oauth}</span><span class="sxs-lookup"><span data-stu-id="9f98a-494">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="9f98a-495">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-495">Address:</span></span> <br><span data-ttu-id="9f98a-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-497">MySQL</span><span class="sxs-lookup"><span data-stu-id="9f98a-497">MySQL</span></span></td>
      <td><span data-ttu-id="9f98a-498">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-498">Container</span></span></td>
      <td><span data-ttu-id="9f98a-499">資料庫</span><span class="sxs-lookup"><span data-stu-id="9f98a-499">Database</span></span></td>
      <td><span data-ttu-id="9f98a-500">
        <font size=2> 通訊協定：mysql</span><span class="sxs-lookup"><span data-stu-id="9f98a-500">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="9f98a-501">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-501">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="9f98a-502">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-502">Address:</span></span> <br><span data-ttu-id="9f98a-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-505">MySQL</span><span class="sxs-lookup"><span data-stu-id="9f98a-505">MySQL</span></span></td>
      <td><span data-ttu-id="9f98a-506">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-506">Table</span></span></td>
      <td><span data-ttu-id="9f98a-507">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-507">Table, view</span></span></td>
      <td><span data-ttu-id="9f98a-508">
        <font size=2> 通訊協定：mysql</span><span class="sxs-lookup"><span data-stu-id="9f98a-508">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="9f98a-509">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-509">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="9f98a-510">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-510">Address:</span></span> <br><span data-ttu-id="9f98a-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-514">OData</span><span class="sxs-lookup"><span data-stu-id="9f98a-514">OData</span></span></td>
      <td><span data-ttu-id="9f98a-515">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-515">Container</span></span></td>
      <td><span data-ttu-id="9f98a-516">實體容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-516">Entity container</span></span></td>
      <td><span data-ttu-id="9f98a-517">
        <font size=2> 通訊協定：odata</span><span class="sxs-lookup"><span data-stu-id="9f98a-517">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="9f98a-518">驗證：{無、基本、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-518">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="9f98a-519">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-519">Address:</span></span> <br><span data-ttu-id="9f98a-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-521">OData</span><span class="sxs-lookup"><span data-stu-id="9f98a-521">OData</span></span></td>
      <td><span data-ttu-id="9f98a-522">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-522">Table</span></span></td>
      <td><span data-ttu-id="9f98a-523">實體集、函式</span><span class="sxs-lookup"><span data-stu-id="9f98a-523">Entity set, function</span></span></td>
      <td><span data-ttu-id="9f98a-524">
        <font size=2> 通訊協定：odata</span><span class="sxs-lookup"><span data-stu-id="9f98a-524">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="9f98a-525">驗證：{無、基本、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-525">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="9f98a-526">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-526">Address:</span></span> <br><span data-ttu-id="9f98a-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="9f98a-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="9f98a-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-529">Oracle 資料庫</span><span class="sxs-lookup"><span data-stu-id="9f98a-529">Oracle Database</span></span></td>
      <td><span data-ttu-id="9f98a-530">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-530">Container</span></span></td>
      <td><span data-ttu-id="9f98a-531">資料庫</span><span class="sxs-lookup"><span data-stu-id="9f98a-531">Database</span></span></td>
      <td><span data-ttu-id="9f98a-532">
        <font size=2> 通訊協定：oracle</span><span class="sxs-lookup"><span data-stu-id="9f98a-532">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="9f98a-533">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-533">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="9f98a-534">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-534">Address:</span></span> <br><span data-ttu-id="9f98a-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-537">Oracle 資料庫</span><span class="sxs-lookup"><span data-stu-id="9f98a-537">Oracle Database</span></span></td>
      <td><span data-ttu-id="9f98a-538">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-538">Table</span></span></td>
      <td><span data-ttu-id="9f98a-539">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-539">Table, view</span></span></td>
      <td><span data-ttu-id="9f98a-540">
        <font size=2> 通訊協定：oracle</span><span class="sxs-lookup"><span data-stu-id="9f98a-540">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="9f98a-541">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-541">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="9f98a-542">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-542">Address:</span></span> <br><span data-ttu-id="9f98a-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="9f98a-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="9f98a-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-547">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="9f98a-547">PostgreSQL</span></span></td>
      <td><span data-ttu-id="9f98a-548">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-548">Container</span></span></td>
      <td><span data-ttu-id="9f98a-549">資料庫</span><span class="sxs-lookup"><span data-stu-id="9f98a-549">Database</span></span></td>
      <td><span data-ttu-id="9f98a-550">
        <font size=2> 通訊協定：postgresql</span><span class="sxs-lookup"><span data-stu-id="9f98a-550">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="9f98a-551">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-551">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="9f98a-552">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-552">Address:</span></span> <br><span data-ttu-id="9f98a-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-555">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="9f98a-555">PostgreSQL</span></span></td>
      <td><span data-ttu-id="9f98a-556">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-556">Table</span></span></td>
      <td><span data-ttu-id="9f98a-557">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-557">Table, view</span></span></td>
      <td><span data-ttu-id="9f98a-558">
        <font size=2> 通訊協定：postgresql</span><span class="sxs-lookup"><span data-stu-id="9f98a-558">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="9f98a-559">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-559">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="9f98a-560">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-560">Address:</span></span> <br><span data-ttu-id="9f98a-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="9f98a-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="9f98a-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-565">Power BI</span><span class="sxs-lookup"><span data-stu-id="9f98a-565">Power BI</span></span></td>
      <td><span data-ttu-id="9f98a-566">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-566">Container</span></span></td>
      <td><span data-ttu-id="9f98a-567">網站</span><span class="sxs-lookup"><span data-stu-id="9f98a-567">Site</span></span></td>
      <td><span data-ttu-id="9f98a-568">
        <font size=2> 通訊協定：http</span><span class="sxs-lookup"><span data-stu-id="9f98a-568">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="9f98a-569">驗證：{無、基本、windows、oauth}</span><span class="sxs-lookup"><span data-stu-id="9f98a-569">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="9f98a-570">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-570">Address:</span></span> <br><span data-ttu-id="9f98a-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-572">Power BI</span><span class="sxs-lookup"><span data-stu-id="9f98a-572">Power BI</span></span></td>
      <td><span data-ttu-id="9f98a-573">報告</span><span class="sxs-lookup"><span data-stu-id="9f98a-573">Report</span></span></td>
      <td><span data-ttu-id="9f98a-574">報告、儀表板</span><span class="sxs-lookup"><span data-stu-id="9f98a-574">Report, dashboard</span></span></td>
      <td><span data-ttu-id="9f98a-575">
        <font size=2> 通訊協定：http</span><span class="sxs-lookup"><span data-stu-id="9f98a-575">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="9f98a-576">驗證：{無、基本、windows、oauth}</span><span class="sxs-lookup"><span data-stu-id="9f98a-576">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="9f98a-577">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-577">Address:</span></span> <br><span data-ttu-id="9f98a-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-579">Power Query</span><span class="sxs-lookup"><span data-stu-id="9f98a-579">Power Query</span></span></td>
      <td><span data-ttu-id="9f98a-580">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-580">Table</span></span></td>
      <td><span data-ttu-id="9f98a-581">交互式資料</span><span class="sxs-lookup"><span data-stu-id="9f98a-581">Data mashup</span></span></td>
      <td><span data-ttu-id="9f98a-582">
        <font size=2> 通訊協定：power-query</span><span class="sxs-lookup"><span data-stu-id="9f98a-582">
        <font size=2> Protocol: power-query</span></span> <br><span data-ttu-id="9f98a-583">驗證：{oauth}</span><span class="sxs-lookup"><span data-stu-id="9f98a-583">Authentication: {oauth}</span></span> <br><span data-ttu-id="9f98a-584">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-584">Address:</span></span> <br><span data-ttu-id="9f98a-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-586">Salesforce</span><span class="sxs-lookup"><span data-stu-id="9f98a-586">Salesforce</span></span></td>
      <td><span data-ttu-id="9f98a-587">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-587">Table</span></span></td>
      <td><span data-ttu-id="9f98a-588">Object</span><span class="sxs-lookup"><span data-stu-id="9f98a-588">Object</span></span></td>
      <td><span data-ttu-id="9f98a-589">
        <font size=2> 通訊協定：salesforce-com</span><span class="sxs-lookup"><span data-stu-id="9f98a-589">
        <font size=2> Protocol: salesforce-com</span></span> <br><span data-ttu-id="9f98a-590">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-590">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="9f98a-591">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-591">Address:</span></span> <br><span data-ttu-id="9f98a-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span><span class="sxs-lookup"><span data-stu-id="9f98a-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span></span> <br><span data-ttu-id="9f98a-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span><span class="sxs-lookup"><span data-stu-id="9f98a-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span></span> <br><span data-ttu-id="9f98a-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-595">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="9f98a-595">SAP HANA</span></span></td>
      <td><span data-ttu-id="9f98a-596">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-596">Container</span></span></td>
      <td><span data-ttu-id="9f98a-597">伺服器</span><span class="sxs-lookup"><span data-stu-id="9f98a-597">Server</span></span></td>
      <td><span data-ttu-id="9f98a-598">
        <font size=2> 通訊協定：sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="9f98a-598">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="9f98a-599">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-599">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="9f98a-600">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-600">Address:</span></span> <br><span data-ttu-id="9f98a-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-602">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="9f98a-602">SAP HANA</span></span></td>
      <td><span data-ttu-id="9f98a-603">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-603">Table</span></span></td>
      <td><span data-ttu-id="9f98a-604">檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-604">View</span></span></td>
      <td><span data-ttu-id="9f98a-605">
        <font size=2> 通訊協定：sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="9f98a-605">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="9f98a-606">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-606">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="9f98a-607">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-607">Address:</span></span> <br><span data-ttu-id="9f98a-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="9f98a-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="9f98a-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-611">SharePoint</span><span class="sxs-lookup"><span data-stu-id="9f98a-611">SharePoint</span></span></td>
      <td><span data-ttu-id="9f98a-612">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-612">Table</span></span></td>
      <td><span data-ttu-id="9f98a-613">列出</span><span class="sxs-lookup"><span data-stu-id="9f98a-613">List</span></span></td>
      <td><span data-ttu-id="9f98a-614">
        <font size=2> 通訊協定：sharepoint-list</span><span class="sxs-lookup"><span data-stu-id="9f98a-614">
        <font size=2> Protocol: sharepoint-list</span></span> <br><span data-ttu-id="9f98a-615">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-615">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="9f98a-616">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-616">Address:</span></span> <br><span data-ttu-id="9f98a-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-618">SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="9f98a-618">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="9f98a-619">命令</span><span class="sxs-lookup"><span data-stu-id="9f98a-619">Command</span></span></td>
      <td><span data-ttu-id="9f98a-620">預存程序</span><span class="sxs-lookup"><span data-stu-id="9f98a-620">Stored procedure</span></span></td>
      <td><span data-ttu-id="9f98a-621">
        <font size=2> 通訊協定：tds</span><span class="sxs-lookup"><span data-stu-id="9f98a-621">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="9f98a-622">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-622">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="9f98a-623">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-623">Address:</span></span> <br><span data-ttu-id="9f98a-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="9f98a-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="9f98a-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-628">SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="9f98a-628">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="9f98a-629">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="9f98a-629">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="9f98a-630">資料表值函式</span><span class="sxs-lookup"><span data-stu-id="9f98a-630">Table-valued function</span></span></td>
      <td><span data-ttu-id="9f98a-631">
        <font size=2> 通訊協定：tds</span><span class="sxs-lookup"><span data-stu-id="9f98a-631">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="9f98a-632">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-632">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="9f98a-633">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-633">Address:</span></span> <br><span data-ttu-id="9f98a-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="9f98a-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="9f98a-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-638">SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="9f98a-638">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="9f98a-639">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-639">Container</span></span></td>
      <td><span data-ttu-id="9f98a-640">資料庫</span><span class="sxs-lookup"><span data-stu-id="9f98a-640">Database</span></span></td>
      <td><span data-ttu-id="9f98a-641">
        <font size=2> 通訊協定：tds</span><span class="sxs-lookup"><span data-stu-id="9f98a-641">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="9f98a-642">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-642">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="9f98a-643">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-643">Address:</span></span> <br><span data-ttu-id="9f98a-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-646">SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="9f98a-646">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="9f98a-647">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-647">Table</span></span></td>
      <td><span data-ttu-id="9f98a-648">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-648">Table, view</span></span></td>
      <td><span data-ttu-id="9f98a-649">
        <font size=2> 通訊協定：tds</span><span class="sxs-lookup"><span data-stu-id="9f98a-649">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="9f98a-650">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-650">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="9f98a-651">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-651">Address:</span></span> <br><span data-ttu-id="9f98a-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="9f98a-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="9f98a-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-656">SQL Server</span><span class="sxs-lookup"><span data-stu-id="9f98a-656">SQL Server</span></span></td>
      <td><span data-ttu-id="9f98a-657">命令</span><span class="sxs-lookup"><span data-stu-id="9f98a-657">Command</span></span></td>
      <td><span data-ttu-id="9f98a-658">預存程序</span><span class="sxs-lookup"><span data-stu-id="9f98a-658">Stored procedure</span></span></td>
      <td><span data-ttu-id="9f98a-659">
        <font size=2> 通訊協定：tds</span><span class="sxs-lookup"><span data-stu-id="9f98a-659">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="9f98a-660">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-660">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="9f98a-661">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-661">Address:</span></span> <br><span data-ttu-id="9f98a-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="9f98a-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="9f98a-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-666">SQL Server</span><span class="sxs-lookup"><span data-stu-id="9f98a-666">SQL Server</span></span></td>
      <td><span data-ttu-id="9f98a-667">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="9f98a-667">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="9f98a-668">資料表值函式</span><span class="sxs-lookup"><span data-stu-id="9f98a-668">Table-valued function</span></span></td>
      <td><span data-ttu-id="9f98a-669">
        <font size=2> 通訊協定：tds</span><span class="sxs-lookup"><span data-stu-id="9f98a-669">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="9f98a-670">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-670">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="9f98a-671">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-671">Address:</span></span> <br><span data-ttu-id="9f98a-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="9f98a-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="9f98a-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-676">SQL Server</span><span class="sxs-lookup"><span data-stu-id="9f98a-676">SQL Server</span></span></td>
      <td><span data-ttu-id="9f98a-677">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-677">Container</span></span></td>
      <td><span data-ttu-id="9f98a-678">資料庫</span><span class="sxs-lookup"><span data-stu-id="9f98a-678">Database</span></span></td>
      <td><span data-ttu-id="9f98a-679">
        <font size=2> 通訊協定：tds</span><span class="sxs-lookup"><span data-stu-id="9f98a-679">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="9f98a-680">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-680">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="9f98a-681">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-681">Address:</span></span> <br><span data-ttu-id="9f98a-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-684">SQL Server</span><span class="sxs-lookup"><span data-stu-id="9f98a-684">SQL Server</span></span></td>
      <td><span data-ttu-id="9f98a-685">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-685">Table</span></span></td>
      <td><span data-ttu-id="9f98a-686">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-686">Table, view</span></span></td>
      <td><span data-ttu-id="9f98a-687">
        <font size=2> 通訊協定：tds</span><span class="sxs-lookup"><span data-stu-id="9f98a-687">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="9f98a-688">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-688">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="9f98a-689">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-689">Address:</span></span> <br><span data-ttu-id="9f98a-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="9f98a-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="9f98a-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-694">SQL Server Analysis Services 多維度</span><span class="sxs-lookup"><span data-stu-id="9f98a-694">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="9f98a-695">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-695">Container</span></span></td>
      <td><span data-ttu-id="9f98a-696">模型</span><span class="sxs-lookup"><span data-stu-id="9f98a-696">Model</span></span></td>
      <td><span data-ttu-id="9f98a-697">
        <font size=2> 通訊協定：analysis-services</span><span class="sxs-lookup"><span data-stu-id="9f98a-697">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="9f98a-698">驗證：{windows、基本、匿名、無}</span><span class="sxs-lookup"><span data-stu-id="9f98a-698">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="9f98a-699">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-699">Address:</span></span> <br><span data-ttu-id="9f98a-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-703">SQL Server Analysis Services 多維度</span><span class="sxs-lookup"><span data-stu-id="9f98a-703">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="9f98a-704">KPI</span><span class="sxs-lookup"><span data-stu-id="9f98a-704">KPI</span></span></td>
      <td><span data-ttu-id="9f98a-705">KPI</span><span class="sxs-lookup"><span data-stu-id="9f98a-705">KPI</span></span></td>
      <td><span data-ttu-id="9f98a-706">
        <font size=2> 通訊協定：analysis-services</span><span class="sxs-lookup"><span data-stu-id="9f98a-706">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="9f98a-707">驗證：{windows、基本、匿名、無}</span><span class="sxs-lookup"><span data-stu-id="9f98a-707">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="9f98a-708">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-708">Address:</span></span> <br><span data-ttu-id="9f98a-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="9f98a-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="9f98a-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="9f98a-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="9f98a-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-714">SQL Server Analysis Services 多維度</span><span class="sxs-lookup"><span data-stu-id="9f98a-714">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="9f98a-715">Measure</span><span class="sxs-lookup"><span data-stu-id="9f98a-715">Measure</span></span></td>
      <td><span data-ttu-id="9f98a-716">Measure</span><span class="sxs-lookup"><span data-stu-id="9f98a-716">Measure</span></span></td>
      <td><span data-ttu-id="9f98a-717">
        <font size=2> 通訊協定：analysis-services</span><span class="sxs-lookup"><span data-stu-id="9f98a-717">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="9f98a-718">驗證：{windows、基本、匿名、無}</span><span class="sxs-lookup"><span data-stu-id="9f98a-718">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="9f98a-719">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-719">Address:</span></span> <br><span data-ttu-id="9f98a-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="9f98a-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="9f98a-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="9f98a-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="9f98a-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-725">SQL Server Analysis Services 多維度</span><span class="sxs-lookup"><span data-stu-id="9f98a-725">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="9f98a-726">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-726">Table</span></span></td>
      <td><span data-ttu-id="9f98a-727">維度</span><span class="sxs-lookup"><span data-stu-id="9f98a-727">Dimension</span></span></td>
      <td><span data-ttu-id="9f98a-728">
        <font size=2> 通訊協定：analysis-services</span><span class="sxs-lookup"><span data-stu-id="9f98a-728">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="9f98a-729">驗證：{windows、基本、匿名、無}</span><span class="sxs-lookup"><span data-stu-id="9f98a-729">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="9f98a-730">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-730">Address:</span></span> <br><span data-ttu-id="9f98a-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="9f98a-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="9f98a-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="9f98a-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="9f98a-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-736">SQL Server Analysis Services 表格式</span><span class="sxs-lookup"><span data-stu-id="9f98a-736">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="9f98a-737">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-737">Container</span></span></td>
      <td><span data-ttu-id="9f98a-738">模型</span><span class="sxs-lookup"><span data-stu-id="9f98a-738">Model</span></span></td>
      <td><span data-ttu-id="9f98a-739">
        <font size=2> 通訊協定：analysis-services</span><span class="sxs-lookup"><span data-stu-id="9f98a-739">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="9f98a-740">驗證：{windows、基本、匿名、無}</span><span class="sxs-lookup"><span data-stu-id="9f98a-740">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="9f98a-741">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-741">Address:</span></span> <br><span data-ttu-id="9f98a-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-745">SQL Server Analysis Services 表格式</span><span class="sxs-lookup"><span data-stu-id="9f98a-745">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="9f98a-746">KPI</span><span class="sxs-lookup"><span data-stu-id="9f98a-746">KPI</span></span></td>
      <td><span data-ttu-id="9f98a-747">KPI</span><span class="sxs-lookup"><span data-stu-id="9f98a-747">KPI</span></span></td>
      <td><span data-ttu-id="9f98a-748">
        <font size=2> 通訊協定：analysis-services</span><span class="sxs-lookup"><span data-stu-id="9f98a-748">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="9f98a-749">驗證：{windows、基本、匿名、無}</span><span class="sxs-lookup"><span data-stu-id="9f98a-749">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="9f98a-750">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-750">Address:</span></span> <br><span data-ttu-id="9f98a-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="9f98a-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="9f98a-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="9f98a-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="9f98a-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-756">SQL Server Analysis Services 表格式</span><span class="sxs-lookup"><span data-stu-id="9f98a-756">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="9f98a-757">Measure</span><span class="sxs-lookup"><span data-stu-id="9f98a-757">Measure</span></span></td>
      <td><span data-ttu-id="9f98a-758">Measure</span><span class="sxs-lookup"><span data-stu-id="9f98a-758">Measure</span></span></td>
      <td><span data-ttu-id="9f98a-759">
        <font size=2> 通訊協定：analysis-services</span><span class="sxs-lookup"><span data-stu-id="9f98a-759">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="9f98a-760">驗證：{windows、基本、匿名、無}</span><span class="sxs-lookup"><span data-stu-id="9f98a-760">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="9f98a-761">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-761">Address:</span></span> <br><span data-ttu-id="9f98a-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="9f98a-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="9f98a-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="9f98a-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="9f98a-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-767">SQL Server Analysis Services 表格式</span><span class="sxs-lookup"><span data-stu-id="9f98a-767">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="9f98a-768">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-768">Table</span></span></td>
      <td><span data-ttu-id="9f98a-769">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-769">Table</span></span></td>
      <td><span data-ttu-id="9f98a-770">
        <font size=2> 通訊協定：analysis-services</span><span class="sxs-lookup"><span data-stu-id="9f98a-770">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="9f98a-771">驗證：{windows、基本、匿名、無}</span><span class="sxs-lookup"><span data-stu-id="9f98a-771">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="9f98a-772">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-772">Address:</span></span> <br><span data-ttu-id="9f98a-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="9f98a-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="9f98a-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="9f98a-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="9f98a-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-778">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="9f98a-778">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="9f98a-779">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-779">Container</span></span></td>
      <td><span data-ttu-id="9f98a-780">伺服器</span><span class="sxs-lookup"><span data-stu-id="9f98a-780">Server</span></span></td>
      <td><span data-ttu-id="9f98a-781">
        <font size=2> 通訊協定：reporting-services</span><span class="sxs-lookup"><span data-stu-id="9f98a-781">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="9f98a-782">驗證：{windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-782">Authentication: {windows}</span></span> <br><span data-ttu-id="9f98a-783">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-783">Address:</span></span> <br><span data-ttu-id="9f98a-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-786">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="9f98a-786">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="9f98a-787">報告</span><span class="sxs-lookup"><span data-stu-id="9f98a-787">Report</span></span></td>
      <td><span data-ttu-id="9f98a-788">報告</span><span class="sxs-lookup"><span data-stu-id="9f98a-788">Report</span></span></td>
      <td><span data-ttu-id="9f98a-789">
        <font size=2> 通訊協定：reporting-services</span><span class="sxs-lookup"><span data-stu-id="9f98a-789">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="9f98a-790">驗證：{windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-790">Authentication: {windows}</span></span> <br><span data-ttu-id="9f98a-791">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-791">Address:</span></span> <br><span data-ttu-id="9f98a-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span><span class="sxs-lookup"><span data-stu-id="9f98a-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span></span> <br><span data-ttu-id="9f98a-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-795">Teradata</span><span class="sxs-lookup"><span data-stu-id="9f98a-795">Teradata</span></span></td>
      <td><span data-ttu-id="9f98a-796">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-796">Container</span></span></td>
      <td><span data-ttu-id="9f98a-797">資料庫</span><span class="sxs-lookup"><span data-stu-id="9f98a-797">Database</span></span></td>
      <td><span data-ttu-id="9f98a-798">
        <font size=2> 通訊協定：teradata</span><span class="sxs-lookup"><span data-stu-id="9f98a-798">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="9f98a-799">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-799">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="9f98a-800">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-800">Address:</span></span> <br><span data-ttu-id="9f98a-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-803">Teradata</span><span class="sxs-lookup"><span data-stu-id="9f98a-803">Teradata</span></span></td>
      <td><span data-ttu-id="9f98a-804">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-804">Table</span></span></td>
      <td><span data-ttu-id="9f98a-805">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-805">Table, view</span></span></td>
      <td><span data-ttu-id="9f98a-806">
        <font size=2> 通訊協定：teradata</span><span class="sxs-lookup"><span data-stu-id="9f98a-806">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="9f98a-807">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-807">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="9f98a-808">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-808">Address:</span></span> <br><span data-ttu-id="9f98a-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-812">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="9f98a-812">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="9f98a-813">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-813">Container</span></span></td>
      <td><span data-ttu-id="9f98a-814">模型</span><span class="sxs-lookup"><span data-stu-id="9f98a-814">Model</span></span></td>
      <td><span data-ttu-id="9f98a-815">
        <font size="2"> 通訊協定︰mssql-mds</span><span class="sxs-lookup"><span data-stu-id="9f98a-815">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="9f98a-816">驗證：{windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-816">Authentication: {windows}</span></span> <br><span data-ttu-id="9f98a-817">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-817">Address:</span></span> <br><span data-ttu-id="9f98a-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="9f98a-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="9f98a-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="9f98a-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="9f98a-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-821">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="9f98a-821">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="9f98a-822">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-822">Table</span></span></td>
      <td><span data-ttu-id="9f98a-823">實體</span><span class="sxs-lookup"><span data-stu-id="9f98a-823">Entity</span></span></td>
      <td><span data-ttu-id="9f98a-824">
        <font size="2"> 通訊協定︰mssql-mds</span><span class="sxs-lookup"><span data-stu-id="9f98a-824">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="9f98a-825">驗證：{windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-825">Authentication: {windows}</span></span> <br><span data-ttu-id="9f98a-826">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-826">Address:</span></span> <br><span data-ttu-id="9f98a-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="9f98a-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="9f98a-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="9f98a-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="9f98a-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span><span class="sxs-lookup"><span data-stu-id="9f98a-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span></span> <br><span data-ttu-id="9f98a-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-831">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9f98a-831">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="9f98a-832">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-832">Container</span></span></td>
      <td><span data-ttu-id="9f98a-833">資料庫</span><span class="sxs-lookup"><span data-stu-id="9f98a-833">Database</span></span></td>
      <td><span data-ttu-id="9f98a-834">
        <font size=2> 通訊協定︰document-db</span><span class="sxs-lookup"><span data-stu-id="9f98a-834">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="9f98a-835">驗證：{azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="9f98a-835">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="9f98a-836">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-836">Address:</span></span> <br><span data-ttu-id="9f98a-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="9f98a-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="9f98a-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-839">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9f98a-839">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="9f98a-840">集合</span><span class="sxs-lookup"><span data-stu-id="9f98a-840">Collection</span></span></td>
      <td><span data-ttu-id="9f98a-841">集合</span><span class="sxs-lookup"><span data-stu-id="9f98a-841">Collection</span></span></td>
      <td><span data-ttu-id="9f98a-842">
        <font size=2> 通訊協定︰document-db</span><span class="sxs-lookup"><span data-stu-id="9f98a-842">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="9f98a-843">驗證：{azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="9f98a-843">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="9f98a-844">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-844">Address:</span></span> <br><span data-ttu-id="9f98a-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="9f98a-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="9f98a-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 集合 </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-848">一般 ODBC</span><span class="sxs-lookup"><span data-stu-id="9f98a-848">Generic ODBC</span></span></td>
      <td><span data-ttu-id="9f98a-849">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-849">Container</span></span></td>
      <td><span data-ttu-id="9f98a-850">資料庫</span><span class="sxs-lookup"><span data-stu-id="9f98a-850">Database</span></span></td>
      <td><span data-ttu-id="9f98a-851">
        <font size=2> 通訊協定：odbc</span><span class="sxs-lookup"><span data-stu-id="9f98a-851">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="9f98a-852">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-852">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="9f98a-853">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-853">Address:</span></span> <br><span data-ttu-id="9f98a-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 選項</span><span class="sxs-lookup"><span data-stu-id="9f98a-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="9f98a-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-856">一般 ODBC</span><span class="sxs-lookup"><span data-stu-id="9f98a-856">Generic ODBC</span></span></td>
      <td><span data-ttu-id="9f98a-857">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-857">Table</span></span></td>
      <td><span data-ttu-id="9f98a-858">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-858">Table, View</span></span></td>
      <td><span data-ttu-id="9f98a-859">
        <font size=2> 通訊協定：odbc</span><span class="sxs-lookup"><span data-stu-id="9f98a-859">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="9f98a-860">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-860">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="9f98a-861">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-861">Address:</span></span> <br><span data-ttu-id="9f98a-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 選項</span><span class="sxs-lookup"><span data-stu-id="9f98a-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="9f98a-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="9f98a-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="9f98a-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-866">Sybase</span><span class="sxs-lookup"><span data-stu-id="9f98a-866">Sybase</span></span></td>
      <td><span data-ttu-id="9f98a-867">容器</span><span class="sxs-lookup"><span data-stu-id="9f98a-867">Container</span></span></td>
      <td><span data-ttu-id="9f98a-868">資料庫</span><span class="sxs-lookup"><span data-stu-id="9f98a-868">Database</span></span></td>
      <td><span data-ttu-id="9f98a-869">
        <font size=2> 通訊協定：sybase</span><span class="sxs-lookup"><span data-stu-id="9f98a-869">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="9f98a-870">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-870">authentication: {basic, windows}</span></span> <br><span data-ttu-id="9f98a-871">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-871">address:</span></span> <br><span data-ttu-id="9f98a-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-874">Sybase</span><span class="sxs-lookup"><span data-stu-id="9f98a-874">Sybase</span></span></td>
      <td><span data-ttu-id="9f98a-875">資料表</span><span class="sxs-lookup"><span data-stu-id="9f98a-875">Table</span></span></td>
      <td><span data-ttu-id="9f98a-876">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="9f98a-876">Table, View</span></span></td>
      <td><span data-ttu-id="9f98a-877">
        <font size=2> 通訊協定：sybase</span><span class="sxs-lookup"><span data-stu-id="9f98a-877">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="9f98a-878">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="9f98a-878">authentication: {basic, windows}</span></span> <br><span data-ttu-id="9f98a-879">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-879">address:</span></span> <br><span data-ttu-id="9f98a-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="9f98a-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="9f98a-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="9f98a-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="9f98a-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="9f98a-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="9f98a-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="9f98a-884">其他 （無 hello 以上）</span><span class="sxs-lookup"><span data-stu-id="9f98a-884">Other (none of hello above)</span></span></td>
      <td>\*</td>
      <td>\*</td>
      <td><span data-ttu-id="9f98a-885">
        <font size=2> 通訊協定：generic-asset</span><span class="sxs-lookup"><span data-stu-id="9f98a-885">
        <font size=2> Protocol: generic-asset</span></span> <br><span data-ttu-id="9f98a-886">位址：</span><span class="sxs-lookup"><span data-stu-id="9f98a-886">Address:</span></span> <br><span data-ttu-id="9f98a-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span><span class="sxs-lookup"><span data-stu-id="9f98a-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span></span></td>
    </tr>
</table>
