---
title: "Azure 資料目錄中支援的資料來源 | Microsoft Docs"
description: "本文列出目前支援之資料來源的規格。"
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
ms.openlocfilehash: d6867c73bc6ea3c238cceef8a68466d451f3365c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="supported-data-sources-in-azure-data-catalog"></a><span data-ttu-id="76bd1-103">Azure 資料目錄中支援的資料來源</span><span class="sxs-lookup"><span data-stu-id="76bd1-103">Supported data sources in Azure Data Catalog</span></span>

<span data-ttu-id="76bd1-104">您可以使用公用 API 或 Click Once 註冊工具，或是直接在「Azure 資料目錄」Web 入口網站中手動輸入資訊，來發佈中繼資料。</span><span class="sxs-lookup"><span data-stu-id="76bd1-104">You can publish metadata by using a public API or a click-once registration tool, or by manually entering information directly to the Azure Data Catalog web portal.</span></span> <span data-ttu-id="76bd1-105">下表摘要說明現今目錄支援的所有資料來源，以及每個資料來源適用的發佈功能。</span><span class="sxs-lookup"><span data-stu-id="76bd1-105">The following table summarizes all data sources that are supported by the catalog today, and the publishing capabilities for each.</span></span> <span data-ttu-id="76bd1-106">此外，也列出每個資料來源可以從我們的入口網站「開啟」體驗啟動的外部資料工具。</span><span class="sxs-lookup"><span data-stu-id="76bd1-106">Also listed are the external data tools that each data source can launch from our portal "open-in" experience.</span></span> <span data-ttu-id="76bd1-107">第二個表格包含每個資料來源連線屬性的較技術性規格。</span><span class="sxs-lookup"><span data-stu-id="76bd1-107">The second table contains a more technical specification of each data-source connection property.</span></span>


## <a name="list-of-supported-data-sources"></a><span data-ttu-id="76bd1-108">支援的資料來源的清單</span><span class="sxs-lookup"><span data-stu-id="76bd1-108">List of supported data sources</span></span>

<table>
    <tr>
       <td><span data-ttu-id="76bd1-109"><b>資料來源物件</b></span><span class="sxs-lookup"><span data-stu-id="76bd1-109"><b>Data source object</b></span></span></td>
       <td><span data-ttu-id="76bd1-110"><b>API</b></span><span class="sxs-lookup"><span data-stu-id="76bd1-110"><b>API</b></span></span></td>
       <td><span data-ttu-id="76bd1-111"><b>手動輸入</b></span><span class="sxs-lookup"><span data-stu-id="76bd1-111"><b>Manual entry</b></span></span></td>
       <td><span data-ttu-id="76bd1-112"><b>註冊工具</b></span><span class="sxs-lookup"><span data-stu-id="76bd1-112"><b>Registration tool</b></span></span></td>
       <td><span data-ttu-id="76bd1-113"><b>開啟工具</b></span><span class="sxs-lookup"><span data-stu-id="76bd1-113"><b>Open-in tools</b></span></span></td>
       <td><span data-ttu-id="76bd1-114"><b>注意事項</b></span><span class="sxs-lookup"><span data-stu-id="76bd1-114"><b>Notes</b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-115">Azure Data Lake Store 目錄</span><span class="sxs-lookup"><span data-stu-id="76bd1-115">Azure Data Lake Store directory</span></span></td>
      <td><span data-ttu-id="76bd1-116">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-116">✓</span></span></td>
      <td><span data-ttu-id="76bd1-117">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-117">✓</span></span></td>
      <td><span data-ttu-id="76bd1-118">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-118">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-119">Azure Data Lake Store 檔案</span><span class="sxs-lookup"><span data-stu-id="76bd1-119">Azure Data Lake Store file</span></span></td>
      <td><span data-ttu-id="76bd1-120">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-120">✓</span></span></td>
      <td><span data-ttu-id="76bd1-121">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-121">✓</span></span></td>
      <td><span data-ttu-id="76bd1-122">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-122">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-123">Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="76bd1-123">Azure Blob storage</span></span></td>
      <td><span data-ttu-id="76bd1-124">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-124">✓</span></span></td>
      <td><span data-ttu-id="76bd1-125">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-125">✓</span></span></td>
      <td><span data-ttu-id="76bd1-126">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-126">✓</span></span></td>
      <td><span data-ttu-id="76bd1-127"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-127"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-128">Azure 儲存體目錄</span><span class="sxs-lookup"><span data-stu-id="76bd1-128">Azure Storage directory</span></span></td>
      <td><span data-ttu-id="76bd1-129">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-129">✓</span></span></td>
      <td><span data-ttu-id="76bd1-130">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-130">✓</span></span></td>
      <td><span data-ttu-id="76bd1-131">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-131">✓</span></span></td>
      <td><span data-ttu-id="76bd1-132"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-132"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-133">Azure 儲存體資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-133">Azure Storage table</span></span></td>
      <td><span data-ttu-id="76bd1-134">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-134">✓</span></span></td>
      <td><span data-ttu-id="76bd1-135">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-135">✓</span></span></td>
      <td><span data-ttu-id="76bd1-136">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-136">✓</span></span></td>
      <td>
        <font size="2"></font>
      </td>
      <td>
        <font size="2"></font>
      </td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-137">HDFS 目錄</span><span class="sxs-lookup"><span data-stu-id="76bd1-137">HDFS directory</span></span></td>
      <td><span data-ttu-id="76bd1-138">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-138">✓</span></span></td>
      <td><span data-ttu-id="76bd1-139">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-139">✓</span></span></td>
      <td><span data-ttu-id="76bd1-140">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-140">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-141">HDFS 檔案</span><span class="sxs-lookup"><span data-stu-id="76bd1-141">HDFS file</span></span></td>
      <td><span data-ttu-id="76bd1-142">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-142">✓</span></span></td>
      <td><span data-ttu-id="76bd1-143">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-143">✓</span></span></td>
      <td><span data-ttu-id="76bd1-144">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-144">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-145">Hive 資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-145">Hive table</span></span></td>
      <td><span data-ttu-id="76bd1-146">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-146">✓</span></span></td>
      <td><span data-ttu-id="76bd1-147">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-147">✓</span></span></td>
      <td><span data-ttu-id="76bd1-148">✓</span><span class="sxs-lookup"><span data-stu-id="76bd1-148">✓</span></span></td>
      <td><span data-ttu-id="76bd1-149"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-149"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-150">Hive 檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-150">Hive view</span></span></td>
      <td><span data-ttu-id="76bd1-151">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-151">✓</span></span></td>
      <td><span data-ttu-id="76bd1-152">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-152">✓</span></span></td>
      <td><span data-ttu-id="76bd1-153">✓</span><span class="sxs-lookup"><span data-stu-id="76bd1-153">✓</span></span></td>
      <td><span data-ttu-id="76bd1-154"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-154"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-155">MySQL 資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-155">MySQL table</span></span></td>
      <td><span data-ttu-id="76bd1-156">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-156">✓</span></span></td>
      <td><span data-ttu-id="76bd1-157">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-157">✓</span></span></td>
      <td><span data-ttu-id="76bd1-158">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-158">✓</span></span></td>
      <td><span data-ttu-id="76bd1-159"><font size=2>Excel、Power BI</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-159"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-160">MySQL 檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-160">MySQL view</span></span></td>
      <td><span data-ttu-id="76bd1-161">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-161">✓</span></span></td>
      <td><span data-ttu-id="76bd1-162">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-162">✓</span></span></td>
      <td><span data-ttu-id="76bd1-163">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-163">✓</span></span></td>
      <td><span data-ttu-id="76bd1-164"><font size=2>Excel、Power BI</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-164"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-165">Oracle 資料庫資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-165">Oracle Database table</span></span></td>
      <td><span data-ttu-id="76bd1-166">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-166">✓</span></span></td>
      <td><span data-ttu-id="76bd1-167">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-167">✓</span></span></td>
      <td><span data-ttu-id="76bd1-168">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-168">✓</span></span></td>
      <td><span data-ttu-id="76bd1-169"><font size=2>Excel、Power BI</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-169"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-170">Oracle 資料庫檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-170">Oracle Database view</span></span></td>
      <td><span data-ttu-id="76bd1-171">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-171">✓</span></span></td>
      <td><span data-ttu-id="76bd1-172">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-172">✓</span></span></td>
      <td><span data-ttu-id="76bd1-173">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-173">✓</span></span></td>
      <td><span data-ttu-id="76bd1-174"><font size=2>Excel、Power BI</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-174"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-175">其他 (一般資產)</span><span class="sxs-lookup"><span data-stu-id="76bd1-175">Other (generic asset)</span></span></td>
      <td><span data-ttu-id="76bd1-176">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-176">✓</span></span></td>
      <td><span data-ttu-id="76bd1-177">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-177">✓</span></span></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-178">Azure SQL 資料倉儲資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-178">Azure SQL Data Warehouse table</span></span></td>
      <td><span data-ttu-id="76bd1-179">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-179">✓</span></span></td>
      <td><span data-ttu-id="76bd1-180">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-180">✓</span></span></td>
      <td><span data-ttu-id="76bd1-181">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-181">✓</span></span></td>
      <td><span data-ttu-id="76bd1-182"><font size=2>Excel、Power BI、SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-182"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-183">SQL 資料倉儲檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-183">SQL Data Warehouse view</span></span></td>
      <td><span data-ttu-id="76bd1-184">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-184">✓</span></span></td>
      <td><span data-ttu-id="76bd1-185">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-185">✓</span></span></td>
      <td><span data-ttu-id="76bd1-186">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-186">✓</span></span></td>
      <td><span data-ttu-id="76bd1-187"><font size=2>Excel、Power BI、SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-187"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-188">SQL Server Analysis Services 維度</span><span class="sxs-lookup"><span data-stu-id="76bd1-188">SQL Server Analysis Services dimension</span></span></td>
      <td><span data-ttu-id="76bd1-189">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-189">✓</span></span></td>
      <td><span data-ttu-id="76bd1-190">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-190">✓</span></span></td>
      <td><span data-ttu-id="76bd1-191">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-191">✓</span></span></td>
      <td><span data-ttu-id="76bd1-192"><font size=2>Excel、Power BI</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-192"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-193">SQL Server Analysis Services KPI</span><span class="sxs-lookup"><span data-stu-id="76bd1-193">SQL Server Analysis Services KPI</span></span></td>
      <td><span data-ttu-id="76bd1-194">✓</span><span class="sxs-lookup"><span data-stu-id="76bd1-194">✓</span></span></td>
      <td><span data-ttu-id="76bd1-195">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-195">✓</span></span></td>
      <td><span data-ttu-id="76bd1-196">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-196">✓</span></span></td>
      <td><span data-ttu-id="76bd1-197"><font size=2>Excel、Power BI</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-197"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-198">SQL Server Analysis Services 量值</span><span class="sxs-lookup"><span data-stu-id="76bd1-198">SQL Server Analysis Services measure</span></span></td>
      <td><span data-ttu-id="76bd1-199">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-199">✓</span></span></td>
      <td><span data-ttu-id="76bd1-200">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-200">✓</span></span></td>
      <td><span data-ttu-id="76bd1-201">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-201">✓</span></span></td>
      <td><span data-ttu-id="76bd1-202"><font size=2>Excel、Power BI</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-202"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-203">SQL Server Analysis Services 資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-203">SQL Server Analysis Services table</span></span></td>
      <td><span data-ttu-id="76bd1-204">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-204">✓</span></span></td>
      <td><span data-ttu-id="76bd1-205">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-205">✓</span></span></td>
      <td><span data-ttu-id="76bd1-206">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-206">✓</span></span></td>
      <td><span data-ttu-id="76bd1-207"><font size=2>Excel、Power BI</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-207"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-208">SQL Server Reporting Services 報表</span><span class="sxs-lookup"><span data-stu-id="76bd1-208">SQL Server Reporting Services report</span></span></td>
      <td><span data-ttu-id="76bd1-209">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-209">✓</span></span></td>
      <td><span data-ttu-id="76bd1-210">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-210">✓</span></span></td>
      <td><span data-ttu-id="76bd1-211">✓</span><span class="sxs-lookup"><span data-stu-id="76bd1-211">✓</span></span></td>
      <td><span data-ttu-id="76bd1-212"><font size=2>[瀏覽器]</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-212"><font size=2>Browser</font></span></span></td>
      <td><span data-ttu-id="76bd1-213"><font size=2>僅限原生模式伺服器。不支援 SharePoint 模式。</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-213"><font size=2>Native mode servers only. SharePoint mode is not supported.</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-214">SQL Server 資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-214">SQL Server table</span></span></td>
      <td><span data-ttu-id="76bd1-215">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-215">✓</span></span></td>
      <td><span data-ttu-id="76bd1-216">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-216">✓</span></span></td>
      <td><span data-ttu-id="76bd1-217">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-217">✓</span></span></td>
      <td><span data-ttu-id="76bd1-218"><font size=2>Excel、Power BI、SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-218"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-219">SQL Server 檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-219">SQL Server view</span></span></td>
      <td><span data-ttu-id="76bd1-220">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-220">✓</span></span></td>
      <td><span data-ttu-id="76bd1-221">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-221">✓</span></span></td>
      <td><span data-ttu-id="76bd1-222">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-222">✓</span></span></td>
      <td><span data-ttu-id="76bd1-223"><font size=2>Excel、Power BI、SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-223"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-224">Teradata 資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-224">Teradata table</span></span></td>
      <td><span data-ttu-id="76bd1-225">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-225">✓</span></span></td>
      <td><span data-ttu-id="76bd1-226">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-226">✓</span></span></td>
      <td><span data-ttu-id="76bd1-227">✓</span><span class="sxs-lookup"><span data-stu-id="76bd1-227">✓</span></span></td>
      <td><span data-ttu-id="76bd1-228"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-228"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-229">Teradata 檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-229">Teradata view</span></span></td>
      <td><span data-ttu-id="76bd1-230">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-230">✓</span></span></td>
      <td><span data-ttu-id="76bd1-231">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-231">✓</span></span></td>
      <td><span data-ttu-id="76bd1-232">✓</span><span class="sxs-lookup"><span data-stu-id="76bd1-232">✓</span></span></td>
      <td><span data-ttu-id="76bd1-233"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-233"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-234">SAP HANA 檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-234">SAP HANA view</span></span></td>
      <td><span data-ttu-id="76bd1-235">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-235">✓</span></span></td>
      <td><span data-ttu-id="76bd1-236">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-236">✓</span></span></td>
      <td><span data-ttu-id="76bd1-237">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-237">✓</span></span></td>
      <td><span data-ttu-id="76bd1-238"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-238"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-239">DB2 資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-239">DB2 table</span></span></td>
      <td><span data-ttu-id="76bd1-240">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-240">✓</span></span></td>
      <td><span data-ttu-id="76bd1-241">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-241">✓</span></span></td>
      <td><span data-ttu-id="76bd1-242">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-242">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-243">DB2 檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-243">DB2 view</span></span></td>
      <td><span data-ttu-id="76bd1-244">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-244">✓</span></span></td>
      <td><span data-ttu-id="76bd1-245">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-245">✓</span></span></td>
      <td><span data-ttu-id="76bd1-246">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-246">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-247">檔案系統檔案</span><span class="sxs-lookup"><span data-stu-id="76bd1-247">File system file</span></span></td>
      <td><span data-ttu-id="76bd1-248">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-248">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-249">FTP 目錄</span><span class="sxs-lookup"><span data-stu-id="76bd1-249">FTP directory</span></span></td>
      <td><span data-ttu-id="76bd1-250">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-250">✓</span></span></td>
      <td><span data-ttu-id="76bd1-251">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-251">✓</span></span></td>
      <td><span data-ttu-id="76bd1-252">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-252">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-253">FTP 檔案</span><span class="sxs-lookup"><span data-stu-id="76bd1-253">FTP file</span></span></td>
      <td><span data-ttu-id="76bd1-254">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-254">✓</span></span></td>
      <td><span data-ttu-id="76bd1-255">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-255">✓</span></span></td>
      <td><span data-ttu-id="76bd1-256">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-256">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-257">HTTP 報告</span><span class="sxs-lookup"><span data-stu-id="76bd1-257">HTTP report</span></span></td>
      <td><span data-ttu-id="76bd1-258">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-258">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-259">HTTP 端點</span><span class="sxs-lookup"><span data-stu-id="76bd1-259">HTTP endpoint</span></span></td>
      <td><span data-ttu-id="76bd1-260">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-260">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-261">HTTP 檔案</span><span class="sxs-lookup"><span data-stu-id="76bd1-261">HTTP file</span></span></td>
      <td><span data-ttu-id="76bd1-262">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-262">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-263">OData 實體集</span><span class="sxs-lookup"><span data-stu-id="76bd1-263">OData entity set</span></span></td>
      <td><span data-ttu-id="76bd1-264">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-264">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-265">OData 函式</span><span class="sxs-lookup"><span data-stu-id="76bd1-265">OData function</span></span></td>
      <td><span data-ttu-id="76bd1-266">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-266">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-267">PostgreSQL 資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-267">PostgreSQL table</span></span></td>
      <td><span data-ttu-id="76bd1-268">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-268">✓</span></span></td>
      <td><span data-ttu-id="76bd1-269">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-269">✓</span></span></td>
      <td><span data-ttu-id="76bd1-270">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-270">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-271">PostgreSQL 檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-271">PostgreSQL view</span></span></td>
      <td><span data-ttu-id="76bd1-272">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-272">✓</span></span></td>
      <td><span data-ttu-id="76bd1-273">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-273">✓</span></span></td>
      <td><span data-ttu-id="76bd1-274">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-274">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-275">SAP HANA 檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-275">SAP HANA view</span></span></td>
      <td><span data-ttu-id="76bd1-276">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-276">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td> <span data-ttu-id="76bd1-277">Salesforce 物件</span><span class="sxs-lookup"><span data-stu-id="76bd1-277">Salesforce object</span></span></td>
      <td><span data-ttu-id="76bd1-278">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-278">✓</span></span></td>
      <td><span data-ttu-id="76bd1-279">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-279">✓</span></span></td>
      <td><span data-ttu-id="76bd1-280">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-280">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-281">SharePoint 清單</span><span class="sxs-lookup"><span data-stu-id="76bd1-281">SharePoint list</span></span> </td>
      <td><span data-ttu-id="76bd1-282">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-282">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-283">Azure Cosmos DB 集合</span><span class="sxs-lookup"><span data-stu-id="76bd1-283">Azure Cosmos DB collection</span></span></td>
      <td><span data-ttu-id="76bd1-284">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-284">✓</span></span></td>
      <td><span data-ttu-id="76bd1-285">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-285">✓</span></span></td>
      <td><span data-ttu-id="76bd1-286">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-286">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-287">一般 ODBC 資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-287">Generic ODBC table</span></span></td>
      <td><span data-ttu-id="76bd1-288">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-288">✓</span></span></td>
      <td><span data-ttu-id="76bd1-289">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-289">✓</span></span></td>
      <td><span data-ttu-id="76bd1-290">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-290">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-291">一般 ODBC 檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-291">Generic ODBC view</span></span></td>
      <td><span data-ttu-id="76bd1-292">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-292">✓</span></span></td>
      <td><span data-ttu-id="76bd1-293">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-293">✓</span></span></td>
      <td><span data-ttu-id="76bd1-294">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-294">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-295">Cassandra 資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-295">Cassandra table</span></span></td>
      <td><span data-ttu-id="76bd1-296">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-296">✓</span></span></td>
      <td><span data-ttu-id="76bd1-297">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-297">✓</span></span></td>
      <td><span data-ttu-id="76bd1-298">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-298">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="76bd1-299"><font size=2>以一般 ODBC 資產形式發佈</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-299"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-300">Cassandra 檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-300">Cassandra view</span></span></td>
      <td><span data-ttu-id="76bd1-301">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-301">✓</span></span></td>
      <td><span data-ttu-id="76bd1-302">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-302">✓</span></span></td>
      <td><span data-ttu-id="76bd1-303">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-303">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="76bd1-304"><font size=2>以一般 ODBC 資產形式發佈</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-304"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-305">Sybase 資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-305">Sybase table</span></span></td>
      <td><span data-ttu-id="76bd1-306">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-306">✓</span></span></td>
      <td><span data-ttu-id="76bd1-307">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-307">✓</span></span></td>
      <td><span data-ttu-id="76bd1-308">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-308">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-309">Sybase 檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-309">Sybase view</span></span></td>
      <td><span data-ttu-id="76bd1-310">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-310">✓</span></span></td>
      <td><span data-ttu-id="76bd1-311">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-311">✓</span></span></td>
      <td><span data-ttu-id="76bd1-312">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-312">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-313">MongoDB 資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-313">MongoDB table</span></span></td>
      <td><span data-ttu-id="76bd1-314">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-314">✓</span></span></td>
      <td><span data-ttu-id="76bd1-315">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-315">✓</span></span></td>
      <td><span data-ttu-id="76bd1-316">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-316">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="76bd1-317"><font size=2>以一般 ODBC 資產形式發佈</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-317"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-318">MongoDB 檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-318">MongoDB view</span></span></td>
      <td><span data-ttu-id="76bd1-319">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-319">✓</span></span></td>
      <td><span data-ttu-id="76bd1-320">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-320">✓</span></span></td>
      <td><span data-ttu-id="76bd1-321">✓ </span><span class="sxs-lookup"><span data-stu-id="76bd1-321">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="76bd1-322"><font size=2>以一般 ODBC 資產形式發佈</font></span><span class="sxs-lookup"><span data-stu-id="76bd1-322"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
</table>

<span data-ttu-id="76bd1-323">如果您需要對其他來源的支援，請向 [Azure 資料目錄論壇](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409)提交功能要求。</span><span class="sxs-lookup"><span data-stu-id="76bd1-323">If you need support for additional sources, submit a feature request to the [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span></span>


## <a name="data-source-reference-specification"></a><span data-ttu-id="76bd1-324">資料來源參考規格</span><span class="sxs-lookup"><span data-stu-id="76bd1-324">Data-source reference specification</span></span>
> [!NOTE]
> <span data-ttu-id="76bd1-325">下表中的「DSL 結構」資料行僅列出「Azure 資料目錄」所使用「位址」屬性包的連線屬性。</span><span class="sxs-lookup"><span data-stu-id="76bd1-325">The **DSL structure** column in the following table lists only the connection properties for "address" property bag that are used by Azure Data Catalog.</span></span> <span data-ttu-id="76bd1-326">也就是說，「位址」屬性包可以針對 Azure 資料目錄保存但並未使用的資料來源，包含其他連接屬性。</span><span class="sxs-lookup"><span data-stu-id="76bd1-326">That is, "address" property bag can contain other connection properties of the data source which Azure Data Catalog persists, but does not use.</span></span>

<table>
    <tr>
       <td><span data-ttu-id="76bd1-327"><b>來源類型</b></span><span class="sxs-lookup"><span data-stu-id="76bd1-327"><b>Source type</b></span></span></td>
       <td><span data-ttu-id="76bd1-328"><b>資產類型</b></span><span class="sxs-lookup"><span data-stu-id="76bd1-328"><b>Asset type</b></span></span></td>
       <td><span data-ttu-id="76bd1-329"><b>物件類型</b></span><span class="sxs-lookup"><span data-stu-id="76bd1-329"><b>Object types</b></span></span></td>
       <td><span data-ttu-id="76bd1-330"><b>DSL 結構<b></span><span class="sxs-lookup"><span data-stu-id="76bd1-330"><b>DSL structure<b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-331">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="76bd1-331">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="76bd1-332">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-332">Container</span></span></td>
      <td><span data-ttu-id="76bd1-333">資料湖</span><span class="sxs-lookup"><span data-stu-id="76bd1-333">Data Lake</span></span></td>
      <td><span data-ttu-id="76bd1-334">
        <font size=2> 通訊協定：webhdfs</span><span class="sxs-lookup"><span data-stu-id="76bd1-334">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="76bd1-335">驗證：{基本、oauth}</span><span class="sxs-lookup"><span data-stu-id="76bd1-335">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="76bd1-336">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-336">Address:</span></span> <br><span data-ttu-id="76bd1-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-338">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="76bd1-338">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="76bd1-339">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-339">Table</span></span></td>
      <td><span data-ttu-id="76bd1-340">目錄、檔案</span><span class="sxs-lookup"><span data-stu-id="76bd1-340">Directory, file</span></span></td>
      <td><span data-ttu-id="76bd1-341">
        <font size=2> 通訊協定：webhdfs</span><span class="sxs-lookup"><span data-stu-id="76bd1-341">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="76bd1-342">驗證：{基本、oauth}</span><span class="sxs-lookup"><span data-stu-id="76bd1-342">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="76bd1-343">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-343">Address:</span></span> <br><span data-ttu-id="76bd1-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-345">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="76bd1-345">Azure Storage</span></span></td>
      <td><span data-ttu-id="76bd1-346">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-346">Container</span></span></td>
      <td><span data-ttu-id="76bd1-347">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-347">Container</span></span></td>
      <td><span data-ttu-id="76bd1-348">
        <font size=2> 通訊協定︰azure-blobs</span><span class="sxs-lookup"><span data-stu-id="76bd1-348">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="76bd1-349">驗證：{azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="76bd1-349">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="76bd1-350">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-350">Address:</span></span> <br><span data-ttu-id="76bd1-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="76bd1-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="76bd1-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 帳戶</span><span class="sxs-lookup"><span data-stu-id="76bd1-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="76bd1-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 容器 </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-354">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="76bd1-354">Azure Storage</span></span></td>
      <td><span data-ttu-id="76bd1-355">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-355">Table</span></span></td>
      <td><span data-ttu-id="76bd1-356">Blob、目錄</span><span class="sxs-lookup"><span data-stu-id="76bd1-356">Blob, directory</span></span></td>
      <td><span data-ttu-id="76bd1-357">
        <font size=2> 通訊協定︰azure-blobs</span><span class="sxs-lookup"><span data-stu-id="76bd1-357">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="76bd1-358">驗證：{azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="76bd1-358">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="76bd1-359">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-359">Address:</span></span> <br><span data-ttu-id="76bd1-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="76bd1-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="76bd1-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 帳戶</span><span class="sxs-lookup"><span data-stu-id="76bd1-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="76bd1-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span></span> <br><span data-ttu-id="76bd1-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-364">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="76bd1-364">Azure Storage</span></span></td>
      <td><span data-ttu-id="76bd1-365">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-365">Container</span></span></td>
      <td><span data-ttu-id="76bd1-366">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-366">Container</span></span></td>
      <td><span data-ttu-id="76bd1-367">
        <font size=2> 通訊協定：azure-tables</span><span class="sxs-lookup"><span data-stu-id="76bd1-367">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="76bd1-368">驗證：{azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="76bd1-368">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="76bd1-369">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-369">Address:</span></span> <br><span data-ttu-id="76bd1-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="76bd1-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="76bd1-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 帳戶 </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-372">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="76bd1-372">Azure Storage</span></span></td>
      <td><span data-ttu-id="76bd1-373">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-373">Table</span></span></td>
      <td><span data-ttu-id="76bd1-374">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-374">Table</span></span></td>
      <td><span data-ttu-id="76bd1-375">
        <font size=2> 通訊協定：azure-tables</span><span class="sxs-lookup"><span data-stu-id="76bd1-375">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="76bd1-376">驗證：{azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="76bd1-376">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="76bd1-377">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-377">Address:</span></span> <br><span data-ttu-id="76bd1-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="76bd1-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="76bd1-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 帳戶</span><span class="sxs-lookup"><span data-stu-id="76bd1-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="76bd1-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-381">Cosmos</span><span class="sxs-lookup"><span data-stu-id="76bd1-381">Cosmos</span></span></td>
      <td><span data-ttu-id="76bd1-382">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-382">Container</span></span></td>
      <td><span data-ttu-id="76bd1-383">虛擬叢集</span><span class="sxs-lookup"><span data-stu-id="76bd1-383">Virtual cluster</span></span></td>
      <td><span data-ttu-id="76bd1-384">
        <font size=2> 通訊協定：cosmos</span><span class="sxs-lookup"><span data-stu-id="76bd1-384">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="76bd1-385">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-385">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="76bd1-386">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-386">Address:</span></span> <br><span data-ttu-id="76bd1-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-388">Cosmos</span><span class="sxs-lookup"><span data-stu-id="76bd1-388">Cosmos</span></span></td>
      <td><span data-ttu-id="76bd1-389">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-389">Table</span></span></td>
      <td><span data-ttu-id="76bd1-390">資料流、資料流集、檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-390">Stream, stream set, view</span></span></td>
      <td><span data-ttu-id="76bd1-391">
        <font size=2> 通訊協定：cosmos</span><span class="sxs-lookup"><span data-stu-id="76bd1-391">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="76bd1-392">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-392">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="76bd1-393">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-393">Address:</span></span> <br><span data-ttu-id="76bd1-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-395">Datazen</span><span class="sxs-lookup"><span data-stu-id="76bd1-395">Datazen</span></span></td>
      <td><span data-ttu-id="76bd1-396">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-396">Container</span></span></td>
      <td><span data-ttu-id="76bd1-397">網站</span><span class="sxs-lookup"><span data-stu-id="76bd1-397">Site</span></span></td>
      <td><span data-ttu-id="76bd1-398">
        <font size=2> 通訊協定：http</span><span class="sxs-lookup"><span data-stu-id="76bd1-398">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="76bd1-399">驗證：{無、基本、windows、oauth}</span><span class="sxs-lookup"><span data-stu-id="76bd1-399">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="76bd1-400">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-400">Address:</span></span> <br><span data-ttu-id="76bd1-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-402">Datazen</span><span class="sxs-lookup"><span data-stu-id="76bd1-402">Datazen</span></span></td>
      <td><span data-ttu-id="76bd1-403">報告</span><span class="sxs-lookup"><span data-stu-id="76bd1-403">Report</span></span></td>
      <td><span data-ttu-id="76bd1-404">報告、儀表板</span><span class="sxs-lookup"><span data-stu-id="76bd1-404">Report, dashboard</span></span></td>
      <td><span data-ttu-id="76bd1-405">
        <font size=2> 通訊協定：http</span><span class="sxs-lookup"><span data-stu-id="76bd1-405">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="76bd1-406">驗證：{無、基本、windows、oauth}</span><span class="sxs-lookup"><span data-stu-id="76bd1-406">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="76bd1-407">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-407">Address:</span></span> <br><span data-ttu-id="76bd1-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-409">DB2</span><span class="sxs-lookup"><span data-stu-id="76bd1-409">DB2</span></span></td>
      <td><span data-ttu-id="76bd1-410">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-410">Container</span></span></td>
      <td><span data-ttu-id="76bd1-411">資料庫</span><span class="sxs-lookup"><span data-stu-id="76bd1-411">Database</span></span></td>
      <td><span data-ttu-id="76bd1-412">
        <font size=2> 通訊協定：db2</span><span class="sxs-lookup"><span data-stu-id="76bd1-412">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="76bd1-413">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-413">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="76bd1-414">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-414">Address:</span></span> <br><span data-ttu-id="76bd1-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-417">DB2</span><span class="sxs-lookup"><span data-stu-id="76bd1-417">DB2</span></span></td>
      <td><span data-ttu-id="76bd1-418">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-418">Table</span></span></td>
      <td><span data-ttu-id="76bd1-419">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-419">Table, view</span></span></td>
      <td><span data-ttu-id="76bd1-420">
        <font size=2> 通訊協定：db2</span><span class="sxs-lookup"><span data-stu-id="76bd1-420">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="76bd1-421">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-421">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="76bd1-422">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-422">Address:</span></span> <br><span data-ttu-id="76bd1-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="76bd1-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="76bd1-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-427">檔案系統</span><span class="sxs-lookup"><span data-stu-id="76bd1-427">File system</span></span></td>
      <td><span data-ttu-id="76bd1-428">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-428">Table</span></span></td>
      <td><span data-ttu-id="76bd1-429">檔案</span><span class="sxs-lookup"><span data-stu-id="76bd1-429">File</span></span></td>
      <td><span data-ttu-id="76bd1-430">
        <font size=2> 通訊協定：file</span><span class="sxs-lookup"><span data-stu-id="76bd1-430">
        <font size=2> Protocol: file</span></span> <br><span data-ttu-id="76bd1-431">驗證：{無、基本、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-431">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="76bd1-432">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-432">Address:</span></span> <br><span data-ttu-id="76bd1-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-434">FTP</span><span class="sxs-lookup"><span data-stu-id="76bd1-434">FTP</span></span></td>
      <td><span data-ttu-id="76bd1-435">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-435">Table</span></span></td>
      <td><span data-ttu-id="76bd1-436">目錄、檔案</span><span class="sxs-lookup"><span data-stu-id="76bd1-436">Directory, file</span></span></td>
      <td><span data-ttu-id="76bd1-437">
        <font size=2> 通訊協定：ftp</span><span class="sxs-lookup"><span data-stu-id="76bd1-437">
        <font size=2> Protocol: ftp</span></span> <br><span data-ttu-id="76bd1-438">驗證：{無、基本、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-438">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="76bd1-439">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-439">Address:</span></span> <br><span data-ttu-id="76bd1-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-441">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="76bd1-441">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="76bd1-442">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-442">Container</span></span></td>
      <td><span data-ttu-id="76bd1-443">叢集</span><span class="sxs-lookup"><span data-stu-id="76bd1-443">Cluster</span></span></td>
      <td><span data-ttu-id="76bd1-444">
        <font size=2> 通訊協定：webhdfs</span><span class="sxs-lookup"><span data-stu-id="76bd1-444">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="76bd1-445">驗證：{基本、oauth}</span><span class="sxs-lookup"><span data-stu-id="76bd1-445">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="76bd1-446">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-446">Address:</span></span> <br><span data-ttu-id="76bd1-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-448">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="76bd1-448">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="76bd1-449">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-449">Table</span></span></td>
      <td><span data-ttu-id="76bd1-450">目錄、檔案</span><span class="sxs-lookup"><span data-stu-id="76bd1-450">Directory, file</span></span></td>
      <td><span data-ttu-id="76bd1-451">
        <font size=2> 通訊協定：webhdfs</span><span class="sxs-lookup"><span data-stu-id="76bd1-451">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="76bd1-452">驗證：{基本、oauth}</span><span class="sxs-lookup"><span data-stu-id="76bd1-452">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="76bd1-453">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-453">Address:</span></span> <br><span data-ttu-id="76bd1-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-455">Hive</span><span class="sxs-lookup"><span data-stu-id="76bd1-455">Hive</span></span></td>
      <td><span data-ttu-id="76bd1-456">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-456">Container</span></span></td>
      <td><span data-ttu-id="76bd1-457">資料庫</span><span class="sxs-lookup"><span data-stu-id="76bd1-457">Database</span></span></td>
      <td><span data-ttu-id="76bd1-458">
        <font size=2> 通訊協定︰hive</span><span class="sxs-lookup"><span data-stu-id="76bd1-458">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="76bd1-459">驗證：{HDInsight、基本、使用者名稱、無}</span><span class="sxs-lookup"><span data-stu-id="76bd1-459">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="76bd1-460">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-460">Address:</span></span> <br><span data-ttu-id="76bd1-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-463">connectionProperties︰</span><span class="sxs-lookup"><span data-stu-id="76bd1-463">connectionProperties:</span></span> <br><span data-ttu-id="76bd1-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-465">Hive</span><span class="sxs-lookup"><span data-stu-id="76bd1-465">Hive</span></span></td>
      <td><span data-ttu-id="76bd1-466">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-466">Table</span></span></td>
      <td><span data-ttu-id="76bd1-467">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-467">Table, view</span></span></td>
      <td><span data-ttu-id="76bd1-468">
        <font size=2> 通訊協定︰hive</span><span class="sxs-lookup"><span data-stu-id="76bd1-468">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="76bd1-469">驗證：{HDInsight、基本、使用者名稱、無}</span><span class="sxs-lookup"><span data-stu-id="76bd1-469">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="76bd1-470">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-470">Address:</span></span> <br><span data-ttu-id="76bd1-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="76bd1-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="76bd1-474">connectionProperties︰</span><span class="sxs-lookup"><span data-stu-id="76bd1-474">connectionProperties:</span></span> <br><span data-ttu-id="76bd1-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-476">HTTP</span><span class="sxs-lookup"><span data-stu-id="76bd1-476">HTTP</span></span></td>
      <td><span data-ttu-id="76bd1-477">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-477">Container</span></span></td>
      <td><span data-ttu-id="76bd1-478">網站</span><span class="sxs-lookup"><span data-stu-id="76bd1-478">Site</span></span></td>
      <td><span data-ttu-id="76bd1-479">
        <font size=2> 通訊協定：http</span><span class="sxs-lookup"><span data-stu-id="76bd1-479">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="76bd1-480">驗證：{無、基本、windows、oauth}</span><span class="sxs-lookup"><span data-stu-id="76bd1-480">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="76bd1-481">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-481">Address:</span></span> <br><span data-ttu-id="76bd1-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-483">HTTP</span><span class="sxs-lookup"><span data-stu-id="76bd1-483">HTTP</span></span></td>
      <td><span data-ttu-id="76bd1-484">報告</span><span class="sxs-lookup"><span data-stu-id="76bd1-484">Report</span></span></td>
      <td><span data-ttu-id="76bd1-485">報告、儀表板</span><span class="sxs-lookup"><span data-stu-id="76bd1-485">Report, dashboard</span></span></td>
      <td><span data-ttu-id="76bd1-486">
        <font size=2> 通訊協定：http</span><span class="sxs-lookup"><span data-stu-id="76bd1-486">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="76bd1-487">驗證：{無、基本、windows、oauth}</span><span class="sxs-lookup"><span data-stu-id="76bd1-487">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="76bd1-488">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-488">Address:</span></span> <br><span data-ttu-id="76bd1-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-490">HTTP</span><span class="sxs-lookup"><span data-stu-id="76bd1-490">HTTP</span></span></td>
      <td><span data-ttu-id="76bd1-491">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-491">Table</span></span></td>
      <td><span data-ttu-id="76bd1-492">端點、檔案</span><span class="sxs-lookup"><span data-stu-id="76bd1-492">Endpoint, file</span></span></td>
      <td><span data-ttu-id="76bd1-493">
        <font size=2> 通訊協定：http</span><span class="sxs-lookup"><span data-stu-id="76bd1-493">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="76bd1-494">驗證：{無、基本、windows、oauth}</span><span class="sxs-lookup"><span data-stu-id="76bd1-494">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="76bd1-495">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-495">Address:</span></span> <br><span data-ttu-id="76bd1-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-497">MySQL</span><span class="sxs-lookup"><span data-stu-id="76bd1-497">MySQL</span></span></td>
      <td><span data-ttu-id="76bd1-498">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-498">Container</span></span></td>
      <td><span data-ttu-id="76bd1-499">資料庫</span><span class="sxs-lookup"><span data-stu-id="76bd1-499">Database</span></span></td>
      <td><span data-ttu-id="76bd1-500">
        <font size=2> 通訊協定：mysql</span><span class="sxs-lookup"><span data-stu-id="76bd1-500">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="76bd1-501">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-501">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="76bd1-502">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-502">Address:</span></span> <br><span data-ttu-id="76bd1-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-505">MySQL</span><span class="sxs-lookup"><span data-stu-id="76bd1-505">MySQL</span></span></td>
      <td><span data-ttu-id="76bd1-506">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-506">Table</span></span></td>
      <td><span data-ttu-id="76bd1-507">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-507">Table, view</span></span></td>
      <td><span data-ttu-id="76bd1-508">
        <font size=2> 通訊協定：mysql</span><span class="sxs-lookup"><span data-stu-id="76bd1-508">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="76bd1-509">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-509">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="76bd1-510">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-510">Address:</span></span> <br><span data-ttu-id="76bd1-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-514">OData</span><span class="sxs-lookup"><span data-stu-id="76bd1-514">OData</span></span></td>
      <td><span data-ttu-id="76bd1-515">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-515">Container</span></span></td>
      <td><span data-ttu-id="76bd1-516">實體容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-516">Entity container</span></span></td>
      <td><span data-ttu-id="76bd1-517">
        <font size=2> 通訊協定：odata</span><span class="sxs-lookup"><span data-stu-id="76bd1-517">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="76bd1-518">驗證：{無、基本、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-518">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="76bd1-519">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-519">Address:</span></span> <br><span data-ttu-id="76bd1-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-521">OData</span><span class="sxs-lookup"><span data-stu-id="76bd1-521">OData</span></span></td>
      <td><span data-ttu-id="76bd1-522">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-522">Table</span></span></td>
      <td><span data-ttu-id="76bd1-523">實體集、函式</span><span class="sxs-lookup"><span data-stu-id="76bd1-523">Entity set, function</span></span></td>
      <td><span data-ttu-id="76bd1-524">
        <font size=2> 通訊協定：odata</span><span class="sxs-lookup"><span data-stu-id="76bd1-524">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="76bd1-525">驗證：{無、基本、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-525">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="76bd1-526">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-526">Address:</span></span> <br><span data-ttu-id="76bd1-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="76bd1-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="76bd1-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-529">Oracle 資料庫</span><span class="sxs-lookup"><span data-stu-id="76bd1-529">Oracle Database</span></span></td>
      <td><span data-ttu-id="76bd1-530">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-530">Container</span></span></td>
      <td><span data-ttu-id="76bd1-531">資料庫</span><span class="sxs-lookup"><span data-stu-id="76bd1-531">Database</span></span></td>
      <td><span data-ttu-id="76bd1-532">
        <font size=2> 通訊協定：oracle</span><span class="sxs-lookup"><span data-stu-id="76bd1-532">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="76bd1-533">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-533">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="76bd1-534">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-534">Address:</span></span> <br><span data-ttu-id="76bd1-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-537">Oracle 資料庫</span><span class="sxs-lookup"><span data-stu-id="76bd1-537">Oracle Database</span></span></td>
      <td><span data-ttu-id="76bd1-538">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-538">Table</span></span></td>
      <td><span data-ttu-id="76bd1-539">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-539">Table, view</span></span></td>
      <td><span data-ttu-id="76bd1-540">
        <font size=2> 通訊協定：oracle</span><span class="sxs-lookup"><span data-stu-id="76bd1-540">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="76bd1-541">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-541">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="76bd1-542">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-542">Address:</span></span> <br><span data-ttu-id="76bd1-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="76bd1-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="76bd1-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-547">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="76bd1-547">PostgreSQL</span></span></td>
      <td><span data-ttu-id="76bd1-548">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-548">Container</span></span></td>
      <td><span data-ttu-id="76bd1-549">資料庫</span><span class="sxs-lookup"><span data-stu-id="76bd1-549">Database</span></span></td>
      <td><span data-ttu-id="76bd1-550">
        <font size=2> 通訊協定：postgresql</span><span class="sxs-lookup"><span data-stu-id="76bd1-550">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="76bd1-551">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-551">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="76bd1-552">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-552">Address:</span></span> <br><span data-ttu-id="76bd1-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-555">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="76bd1-555">PostgreSQL</span></span></td>
      <td><span data-ttu-id="76bd1-556">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-556">Table</span></span></td>
      <td><span data-ttu-id="76bd1-557">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-557">Table, view</span></span></td>
      <td><span data-ttu-id="76bd1-558">
        <font size=2> 通訊協定：postgresql</span><span class="sxs-lookup"><span data-stu-id="76bd1-558">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="76bd1-559">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-559">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="76bd1-560">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-560">Address:</span></span> <br><span data-ttu-id="76bd1-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="76bd1-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="76bd1-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-565">Power BI</span><span class="sxs-lookup"><span data-stu-id="76bd1-565">Power BI</span></span></td>
      <td><span data-ttu-id="76bd1-566">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-566">Container</span></span></td>
      <td><span data-ttu-id="76bd1-567">網站</span><span class="sxs-lookup"><span data-stu-id="76bd1-567">Site</span></span></td>
      <td><span data-ttu-id="76bd1-568">
        <font size=2> 通訊協定：http</span><span class="sxs-lookup"><span data-stu-id="76bd1-568">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="76bd1-569">驗證：{無、基本、windows、oauth}</span><span class="sxs-lookup"><span data-stu-id="76bd1-569">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="76bd1-570">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-570">Address:</span></span> <br><span data-ttu-id="76bd1-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-572">Power BI</span><span class="sxs-lookup"><span data-stu-id="76bd1-572">Power BI</span></span></td>
      <td><span data-ttu-id="76bd1-573">報告</span><span class="sxs-lookup"><span data-stu-id="76bd1-573">Report</span></span></td>
      <td><span data-ttu-id="76bd1-574">報告、儀表板</span><span class="sxs-lookup"><span data-stu-id="76bd1-574">Report, dashboard</span></span></td>
      <td><span data-ttu-id="76bd1-575">
        <font size=2> 通訊協定：http</span><span class="sxs-lookup"><span data-stu-id="76bd1-575">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="76bd1-576">驗證：{無、基本、windows、oauth}</span><span class="sxs-lookup"><span data-stu-id="76bd1-576">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="76bd1-577">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-577">Address:</span></span> <br><span data-ttu-id="76bd1-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-579">Power Query</span><span class="sxs-lookup"><span data-stu-id="76bd1-579">Power Query</span></span></td>
      <td><span data-ttu-id="76bd1-580">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-580">Table</span></span></td>
      <td><span data-ttu-id="76bd1-581">交互式資料</span><span class="sxs-lookup"><span data-stu-id="76bd1-581">Data mashup</span></span></td>
      <td><span data-ttu-id="76bd1-582">
        <font size=2> 通訊協定：power-query</span><span class="sxs-lookup"><span data-stu-id="76bd1-582">
        <font size=2> Protocol: power-query</span></span> <br><span data-ttu-id="76bd1-583">驗證：{oauth}</span><span class="sxs-lookup"><span data-stu-id="76bd1-583">Authentication: {oauth}</span></span> <br><span data-ttu-id="76bd1-584">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-584">Address:</span></span> <br><span data-ttu-id="76bd1-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-586">Salesforce</span><span class="sxs-lookup"><span data-stu-id="76bd1-586">Salesforce</span></span></td>
      <td><span data-ttu-id="76bd1-587">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-587">Table</span></span></td>
      <td><span data-ttu-id="76bd1-588">Object</span><span class="sxs-lookup"><span data-stu-id="76bd1-588">Object</span></span></td>
      <td><span data-ttu-id="76bd1-589">
        <font size=2> 通訊協定：salesforce-com</span><span class="sxs-lookup"><span data-stu-id="76bd1-589">
        <font size=2> Protocol: salesforce-com</span></span> <br><span data-ttu-id="76bd1-590">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-590">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="76bd1-591">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-591">Address:</span></span> <br><span data-ttu-id="76bd1-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span><span class="sxs-lookup"><span data-stu-id="76bd1-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span></span> <br><span data-ttu-id="76bd1-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span><span class="sxs-lookup"><span data-stu-id="76bd1-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span></span> <br><span data-ttu-id="76bd1-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-595">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="76bd1-595">SAP HANA</span></span></td>
      <td><span data-ttu-id="76bd1-596">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-596">Container</span></span></td>
      <td><span data-ttu-id="76bd1-597">伺服器</span><span class="sxs-lookup"><span data-stu-id="76bd1-597">Server</span></span></td>
      <td><span data-ttu-id="76bd1-598">
        <font size=2> 通訊協定：sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="76bd1-598">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="76bd1-599">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-599">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="76bd1-600">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-600">Address:</span></span> <br><span data-ttu-id="76bd1-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-602">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="76bd1-602">SAP HANA</span></span></td>
      <td><span data-ttu-id="76bd1-603">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-603">Table</span></span></td>
      <td><span data-ttu-id="76bd1-604">檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-604">View</span></span></td>
      <td><span data-ttu-id="76bd1-605">
        <font size=2> 通訊協定：sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="76bd1-605">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="76bd1-606">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-606">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="76bd1-607">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-607">Address:</span></span> <br><span data-ttu-id="76bd1-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="76bd1-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="76bd1-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-611">SharePoint</span><span class="sxs-lookup"><span data-stu-id="76bd1-611">SharePoint</span></span></td>
      <td><span data-ttu-id="76bd1-612">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-612">Table</span></span></td>
      <td><span data-ttu-id="76bd1-613">列出</span><span class="sxs-lookup"><span data-stu-id="76bd1-613">List</span></span></td>
      <td><span data-ttu-id="76bd1-614">
        <font size=2> 通訊協定：sharepoint-list</span><span class="sxs-lookup"><span data-stu-id="76bd1-614">
        <font size=2> Protocol: sharepoint-list</span></span> <br><span data-ttu-id="76bd1-615">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-615">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="76bd1-616">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-616">Address:</span></span> <br><span data-ttu-id="76bd1-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-618">SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="76bd1-618">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="76bd1-619">命令</span><span class="sxs-lookup"><span data-stu-id="76bd1-619">Command</span></span></td>
      <td><span data-ttu-id="76bd1-620">預存程序</span><span class="sxs-lookup"><span data-stu-id="76bd1-620">Stored procedure</span></span></td>
      <td><span data-ttu-id="76bd1-621">
        <font size=2> 通訊協定：tds</span><span class="sxs-lookup"><span data-stu-id="76bd1-621">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="76bd1-622">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-622">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="76bd1-623">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-623">Address:</span></span> <br><span data-ttu-id="76bd1-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="76bd1-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="76bd1-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-628">SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="76bd1-628">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="76bd1-629">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="76bd1-629">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="76bd1-630">資料表值函式</span><span class="sxs-lookup"><span data-stu-id="76bd1-630">Table-valued function</span></span></td>
      <td><span data-ttu-id="76bd1-631">
        <font size=2> 通訊協定：tds</span><span class="sxs-lookup"><span data-stu-id="76bd1-631">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="76bd1-632">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-632">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="76bd1-633">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-633">Address:</span></span> <br><span data-ttu-id="76bd1-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="76bd1-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="76bd1-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-638">SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="76bd1-638">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="76bd1-639">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-639">Container</span></span></td>
      <td><span data-ttu-id="76bd1-640">資料庫</span><span class="sxs-lookup"><span data-stu-id="76bd1-640">Database</span></span></td>
      <td><span data-ttu-id="76bd1-641">
        <font size=2> 通訊協定：tds</span><span class="sxs-lookup"><span data-stu-id="76bd1-641">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="76bd1-642">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-642">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="76bd1-643">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-643">Address:</span></span> <br><span data-ttu-id="76bd1-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-646">SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="76bd1-646">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="76bd1-647">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-647">Table</span></span></td>
      <td><span data-ttu-id="76bd1-648">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-648">Table, view</span></span></td>
      <td><span data-ttu-id="76bd1-649">
        <font size=2> 通訊協定：tds</span><span class="sxs-lookup"><span data-stu-id="76bd1-649">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="76bd1-650">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-650">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="76bd1-651">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-651">Address:</span></span> <br><span data-ttu-id="76bd1-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="76bd1-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="76bd1-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-656">SQL Server</span><span class="sxs-lookup"><span data-stu-id="76bd1-656">SQL Server</span></span></td>
      <td><span data-ttu-id="76bd1-657">命令</span><span class="sxs-lookup"><span data-stu-id="76bd1-657">Command</span></span></td>
      <td><span data-ttu-id="76bd1-658">預存程序</span><span class="sxs-lookup"><span data-stu-id="76bd1-658">Stored procedure</span></span></td>
      <td><span data-ttu-id="76bd1-659">
        <font size=2> 通訊協定：tds</span><span class="sxs-lookup"><span data-stu-id="76bd1-659">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="76bd1-660">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-660">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="76bd1-661">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-661">Address:</span></span> <br><span data-ttu-id="76bd1-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="76bd1-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="76bd1-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-666">SQL Server</span><span class="sxs-lookup"><span data-stu-id="76bd1-666">SQL Server</span></span></td>
      <td><span data-ttu-id="76bd1-667">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="76bd1-667">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="76bd1-668">資料表值函式</span><span class="sxs-lookup"><span data-stu-id="76bd1-668">Table-valued function</span></span></td>
      <td><span data-ttu-id="76bd1-669">
        <font size=2> 通訊協定：tds</span><span class="sxs-lookup"><span data-stu-id="76bd1-669">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="76bd1-670">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-670">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="76bd1-671">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-671">Address:</span></span> <br><span data-ttu-id="76bd1-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="76bd1-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="76bd1-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-676">SQL Server</span><span class="sxs-lookup"><span data-stu-id="76bd1-676">SQL Server</span></span></td>
      <td><span data-ttu-id="76bd1-677">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-677">Container</span></span></td>
      <td><span data-ttu-id="76bd1-678">資料庫</span><span class="sxs-lookup"><span data-stu-id="76bd1-678">Database</span></span></td>
      <td><span data-ttu-id="76bd1-679">
        <font size=2> 通訊協定：tds</span><span class="sxs-lookup"><span data-stu-id="76bd1-679">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="76bd1-680">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-680">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="76bd1-681">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-681">Address:</span></span> <br><span data-ttu-id="76bd1-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-684">SQL Server</span><span class="sxs-lookup"><span data-stu-id="76bd1-684">SQL Server</span></span></td>
      <td><span data-ttu-id="76bd1-685">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-685">Table</span></span></td>
      <td><span data-ttu-id="76bd1-686">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-686">Table, view</span></span></td>
      <td><span data-ttu-id="76bd1-687">
        <font size=2> 通訊協定：tds</span><span class="sxs-lookup"><span data-stu-id="76bd1-687">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="76bd1-688">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-688">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="76bd1-689">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-689">Address:</span></span> <br><span data-ttu-id="76bd1-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="76bd1-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="76bd1-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-694">SQL Server Analysis Services 多維度</span><span class="sxs-lookup"><span data-stu-id="76bd1-694">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="76bd1-695">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-695">Container</span></span></td>
      <td><span data-ttu-id="76bd1-696">模型</span><span class="sxs-lookup"><span data-stu-id="76bd1-696">Model</span></span></td>
      <td><span data-ttu-id="76bd1-697">
        <font size=2> 通訊協定：analysis-services</span><span class="sxs-lookup"><span data-stu-id="76bd1-697">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="76bd1-698">驗證：{windows、基本、匿名、無}</span><span class="sxs-lookup"><span data-stu-id="76bd1-698">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="76bd1-699">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-699">Address:</span></span> <br><span data-ttu-id="76bd1-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-703">SQL Server Analysis Services 多維度</span><span class="sxs-lookup"><span data-stu-id="76bd1-703">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="76bd1-704">KPI</span><span class="sxs-lookup"><span data-stu-id="76bd1-704">KPI</span></span></td>
      <td><span data-ttu-id="76bd1-705">KPI</span><span class="sxs-lookup"><span data-stu-id="76bd1-705">KPI</span></span></td>
      <td><span data-ttu-id="76bd1-706">
        <font size=2> 通訊協定：analysis-services</span><span class="sxs-lookup"><span data-stu-id="76bd1-706">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="76bd1-707">驗證：{windows、基本、匿名、無}</span><span class="sxs-lookup"><span data-stu-id="76bd1-707">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="76bd1-708">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-708">Address:</span></span> <br><span data-ttu-id="76bd1-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="76bd1-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="76bd1-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="76bd1-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="76bd1-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-714">SQL Server Analysis Services 多維度</span><span class="sxs-lookup"><span data-stu-id="76bd1-714">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="76bd1-715">Measure</span><span class="sxs-lookup"><span data-stu-id="76bd1-715">Measure</span></span></td>
      <td><span data-ttu-id="76bd1-716">Measure</span><span class="sxs-lookup"><span data-stu-id="76bd1-716">Measure</span></span></td>
      <td><span data-ttu-id="76bd1-717">
        <font size=2> 通訊協定：analysis-services</span><span class="sxs-lookup"><span data-stu-id="76bd1-717">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="76bd1-718">驗證：{windows、基本、匿名、無}</span><span class="sxs-lookup"><span data-stu-id="76bd1-718">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="76bd1-719">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-719">Address:</span></span> <br><span data-ttu-id="76bd1-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="76bd1-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="76bd1-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="76bd1-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="76bd1-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-725">SQL Server Analysis Services 多維度</span><span class="sxs-lookup"><span data-stu-id="76bd1-725">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="76bd1-726">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-726">Table</span></span></td>
      <td><span data-ttu-id="76bd1-727">維度</span><span class="sxs-lookup"><span data-stu-id="76bd1-727">Dimension</span></span></td>
      <td><span data-ttu-id="76bd1-728">
        <font size=2> 通訊協定：analysis-services</span><span class="sxs-lookup"><span data-stu-id="76bd1-728">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="76bd1-729">驗證：{windows、基本、匿名、無}</span><span class="sxs-lookup"><span data-stu-id="76bd1-729">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="76bd1-730">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-730">Address:</span></span> <br><span data-ttu-id="76bd1-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="76bd1-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="76bd1-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="76bd1-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="76bd1-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-736">SQL Server Analysis Services 表格式</span><span class="sxs-lookup"><span data-stu-id="76bd1-736">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="76bd1-737">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-737">Container</span></span></td>
      <td><span data-ttu-id="76bd1-738">模型</span><span class="sxs-lookup"><span data-stu-id="76bd1-738">Model</span></span></td>
      <td><span data-ttu-id="76bd1-739">
        <font size=2> 通訊協定：analysis-services</span><span class="sxs-lookup"><span data-stu-id="76bd1-739">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="76bd1-740">驗證：{windows、基本、匿名、無}</span><span class="sxs-lookup"><span data-stu-id="76bd1-740">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="76bd1-741">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-741">Address:</span></span> <br><span data-ttu-id="76bd1-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-745">SQL Server Analysis Services 表格式</span><span class="sxs-lookup"><span data-stu-id="76bd1-745">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="76bd1-746">KPI</span><span class="sxs-lookup"><span data-stu-id="76bd1-746">KPI</span></span></td>
      <td><span data-ttu-id="76bd1-747">KPI</span><span class="sxs-lookup"><span data-stu-id="76bd1-747">KPI</span></span></td>
      <td><span data-ttu-id="76bd1-748">
        <font size=2> 通訊協定：analysis-services</span><span class="sxs-lookup"><span data-stu-id="76bd1-748">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="76bd1-749">驗證：{windows、基本、匿名、無}</span><span class="sxs-lookup"><span data-stu-id="76bd1-749">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="76bd1-750">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-750">Address:</span></span> <br><span data-ttu-id="76bd1-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="76bd1-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="76bd1-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="76bd1-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="76bd1-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-756">SQL Server Analysis Services 表格式</span><span class="sxs-lookup"><span data-stu-id="76bd1-756">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="76bd1-757">Measure</span><span class="sxs-lookup"><span data-stu-id="76bd1-757">Measure</span></span></td>
      <td><span data-ttu-id="76bd1-758">Measure</span><span class="sxs-lookup"><span data-stu-id="76bd1-758">Measure</span></span></td>
      <td><span data-ttu-id="76bd1-759">
        <font size=2> 通訊協定：analysis-services</span><span class="sxs-lookup"><span data-stu-id="76bd1-759">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="76bd1-760">驗證：{windows、基本、匿名、無}</span><span class="sxs-lookup"><span data-stu-id="76bd1-760">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="76bd1-761">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-761">Address:</span></span> <br><span data-ttu-id="76bd1-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="76bd1-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="76bd1-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="76bd1-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="76bd1-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-767">SQL Server Analysis Services 表格式</span><span class="sxs-lookup"><span data-stu-id="76bd1-767">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="76bd1-768">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-768">Table</span></span></td>
      <td><span data-ttu-id="76bd1-769">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-769">Table</span></span></td>
      <td><span data-ttu-id="76bd1-770">
        <font size=2> 通訊協定：analysis-services</span><span class="sxs-lookup"><span data-stu-id="76bd1-770">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="76bd1-771">驗證：{windows、基本、匿名、無}</span><span class="sxs-lookup"><span data-stu-id="76bd1-771">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="76bd1-772">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-772">Address:</span></span> <br><span data-ttu-id="76bd1-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="76bd1-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="76bd1-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="76bd1-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="76bd1-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-778">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="76bd1-778">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="76bd1-779">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-779">Container</span></span></td>
      <td><span data-ttu-id="76bd1-780">伺服器</span><span class="sxs-lookup"><span data-stu-id="76bd1-780">Server</span></span></td>
      <td><span data-ttu-id="76bd1-781">
        <font size=2> 通訊協定：reporting-services</span><span class="sxs-lookup"><span data-stu-id="76bd1-781">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="76bd1-782">驗證：{windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-782">Authentication: {windows}</span></span> <br><span data-ttu-id="76bd1-783">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-783">Address:</span></span> <br><span data-ttu-id="76bd1-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-786">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="76bd1-786">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="76bd1-787">報告</span><span class="sxs-lookup"><span data-stu-id="76bd1-787">Report</span></span></td>
      <td><span data-ttu-id="76bd1-788">報告</span><span class="sxs-lookup"><span data-stu-id="76bd1-788">Report</span></span></td>
      <td><span data-ttu-id="76bd1-789">
        <font size=2> 通訊協定：reporting-services</span><span class="sxs-lookup"><span data-stu-id="76bd1-789">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="76bd1-790">驗證：{windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-790">Authentication: {windows}</span></span> <br><span data-ttu-id="76bd1-791">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-791">Address:</span></span> <br><span data-ttu-id="76bd1-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span><span class="sxs-lookup"><span data-stu-id="76bd1-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span></span> <br><span data-ttu-id="76bd1-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-795">Teradata</span><span class="sxs-lookup"><span data-stu-id="76bd1-795">Teradata</span></span></td>
      <td><span data-ttu-id="76bd1-796">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-796">Container</span></span></td>
      <td><span data-ttu-id="76bd1-797">資料庫</span><span class="sxs-lookup"><span data-stu-id="76bd1-797">Database</span></span></td>
      <td><span data-ttu-id="76bd1-798">
        <font size=2> 通訊協定：teradata</span><span class="sxs-lookup"><span data-stu-id="76bd1-798">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="76bd1-799">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-799">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="76bd1-800">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-800">Address:</span></span> <br><span data-ttu-id="76bd1-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-803">Teradata</span><span class="sxs-lookup"><span data-stu-id="76bd1-803">Teradata</span></span></td>
      <td><span data-ttu-id="76bd1-804">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-804">Table</span></span></td>
      <td><span data-ttu-id="76bd1-805">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-805">Table, view</span></span></td>
      <td><span data-ttu-id="76bd1-806">
        <font size=2> 通訊協定：teradata</span><span class="sxs-lookup"><span data-stu-id="76bd1-806">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="76bd1-807">驗證：{通訊協定、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-807">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="76bd1-808">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-808">Address:</span></span> <br><span data-ttu-id="76bd1-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-812">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="76bd1-812">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="76bd1-813">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-813">Container</span></span></td>
      <td><span data-ttu-id="76bd1-814">模型</span><span class="sxs-lookup"><span data-stu-id="76bd1-814">Model</span></span></td>
      <td><span data-ttu-id="76bd1-815">
        <font size="2"> 通訊協定︰mssql-mds</span><span class="sxs-lookup"><span data-stu-id="76bd1-815">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="76bd1-816">驗證：{windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-816">Authentication: {windows}</span></span> <br><span data-ttu-id="76bd1-817">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-817">Address:</span></span> <br><span data-ttu-id="76bd1-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="76bd1-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="76bd1-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="76bd1-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="76bd1-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-821">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="76bd1-821">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="76bd1-822">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-822">Table</span></span></td>
      <td><span data-ttu-id="76bd1-823">實體</span><span class="sxs-lookup"><span data-stu-id="76bd1-823">Entity</span></span></td>
      <td><span data-ttu-id="76bd1-824">
        <font size="2"> 通訊協定︰mssql-mds</span><span class="sxs-lookup"><span data-stu-id="76bd1-824">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="76bd1-825">驗證：{windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-825">Authentication: {windows}</span></span> <br><span data-ttu-id="76bd1-826">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-826">Address:</span></span> <br><span data-ttu-id="76bd1-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="76bd1-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="76bd1-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="76bd1-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="76bd1-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span><span class="sxs-lookup"><span data-stu-id="76bd1-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span></span> <br><span data-ttu-id="76bd1-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-831">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="76bd1-831">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="76bd1-832">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-832">Container</span></span></td>
      <td><span data-ttu-id="76bd1-833">資料庫</span><span class="sxs-lookup"><span data-stu-id="76bd1-833">Database</span></span></td>
      <td><span data-ttu-id="76bd1-834">
        <font size=2> 通訊協定︰document-db</span><span class="sxs-lookup"><span data-stu-id="76bd1-834">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="76bd1-835">驗證：{azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="76bd1-835">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="76bd1-836">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-836">Address:</span></span> <br><span data-ttu-id="76bd1-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="76bd1-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="76bd1-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-839">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="76bd1-839">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="76bd1-840">集合</span><span class="sxs-lookup"><span data-stu-id="76bd1-840">Collection</span></span></td>
      <td><span data-ttu-id="76bd1-841">集合</span><span class="sxs-lookup"><span data-stu-id="76bd1-841">Collection</span></span></td>
      <td><span data-ttu-id="76bd1-842">
        <font size=2> 通訊協定︰document-db</span><span class="sxs-lookup"><span data-stu-id="76bd1-842">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="76bd1-843">驗證：{azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="76bd1-843">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="76bd1-844">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-844">Address:</span></span> <br><span data-ttu-id="76bd1-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="76bd1-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="76bd1-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 集合 </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-848">一般 ODBC</span><span class="sxs-lookup"><span data-stu-id="76bd1-848">Generic ODBC</span></span></td>
      <td><span data-ttu-id="76bd1-849">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-849">Container</span></span></td>
      <td><span data-ttu-id="76bd1-850">資料庫</span><span class="sxs-lookup"><span data-stu-id="76bd1-850">Database</span></span></td>
      <td><span data-ttu-id="76bd1-851">
        <font size=2> 通訊協定：odbc</span><span class="sxs-lookup"><span data-stu-id="76bd1-851">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="76bd1-852">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-852">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="76bd1-853">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-853">Address:</span></span> <br><span data-ttu-id="76bd1-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 選項</span><span class="sxs-lookup"><span data-stu-id="76bd1-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="76bd1-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-856">一般 ODBC</span><span class="sxs-lookup"><span data-stu-id="76bd1-856">Generic ODBC</span></span></td>
      <td><span data-ttu-id="76bd1-857">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-857">Table</span></span></td>
      <td><span data-ttu-id="76bd1-858">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-858">Table, View</span></span></td>
      <td><span data-ttu-id="76bd1-859">
        <font size=2> 通訊協定：odbc</span><span class="sxs-lookup"><span data-stu-id="76bd1-859">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="76bd1-860">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-860">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="76bd1-861">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-861">Address:</span></span> <br><span data-ttu-id="76bd1-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 選項</span><span class="sxs-lookup"><span data-stu-id="76bd1-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="76bd1-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="76bd1-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="76bd1-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-866">Sybase</span><span class="sxs-lookup"><span data-stu-id="76bd1-866">Sybase</span></span></td>
      <td><span data-ttu-id="76bd1-867">容器</span><span class="sxs-lookup"><span data-stu-id="76bd1-867">Container</span></span></td>
      <td><span data-ttu-id="76bd1-868">資料庫</span><span class="sxs-lookup"><span data-stu-id="76bd1-868">Database</span></span></td>
      <td><span data-ttu-id="76bd1-869">
        <font size=2> 通訊協定：sybase</span><span class="sxs-lookup"><span data-stu-id="76bd1-869">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="76bd1-870">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-870">authentication: {basic, windows}</span></span> <br><span data-ttu-id="76bd1-871">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-871">address:</span></span> <br><span data-ttu-id="76bd1-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-874">Sybase</span><span class="sxs-lookup"><span data-stu-id="76bd1-874">Sybase</span></span></td>
      <td><span data-ttu-id="76bd1-875">資料表</span><span class="sxs-lookup"><span data-stu-id="76bd1-875">Table</span></span></td>
      <td><span data-ttu-id="76bd1-876">資料表、檢視</span><span class="sxs-lookup"><span data-stu-id="76bd1-876">Table, View</span></span></td>
      <td><span data-ttu-id="76bd1-877">
        <font size=2> 通訊協定：sybase</span><span class="sxs-lookup"><span data-stu-id="76bd1-877">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="76bd1-878">驗證：{基本、windows}</span><span class="sxs-lookup"><span data-stu-id="76bd1-878">authentication: {basic, windows}</span></span> <br><span data-ttu-id="76bd1-879">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-879">address:</span></span> <br><span data-ttu-id="76bd1-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="76bd1-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="76bd1-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="76bd1-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="76bd1-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="76bd1-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="76bd1-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="76bd1-884">其他 (以上皆非)</span><span class="sxs-lookup"><span data-stu-id="76bd1-884">Other (none of the above)</span></span></td>
      <td>\*</td>
      <td>\*</td>
      <td><span data-ttu-id="76bd1-885">
        <font size=2> 通訊協定：generic-asset</span><span class="sxs-lookup"><span data-stu-id="76bd1-885">
        <font size=2> Protocol: generic-asset</span></span> <br><span data-ttu-id="76bd1-886">位址：</span><span class="sxs-lookup"><span data-stu-id="76bd1-886">Address:</span></span> <br><span data-ttu-id="76bd1-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span><span class="sxs-lookup"><span data-stu-id="76bd1-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span></span></td>
    </tr>
</table>
