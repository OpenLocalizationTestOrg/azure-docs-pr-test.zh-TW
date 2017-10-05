---
title: "使用 Java 的 Azure 儲存體範例 | Microsoft Docs"
description: "檢視、下載及執行 Azure 儲存體的範例程式碼和應用程式。 探索使用 Java 儲存體用戶端程式庫之 Blob、佇列、資料表和檔案的入門範例。"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: fd27e1ac9a773e7b0f5245aa74acdb0521cd098c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="53bf6-104">使用 Java 的 Azure 儲存體範例</span><span class="sxs-lookup"><span data-stu-id="53bf6-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="53bf6-105">Java 範例索引</span><span class="sxs-lookup"><span data-stu-id="53bf6-105">Java sample index</span></span>

<span data-ttu-id="53bf6-106">下表提供我們的範例儲存機制和每個範例所涵蓋案例的概觀。</span><span class="sxs-lookup"><span data-stu-id="53bf6-106">The following table provides an overview of our samples repository and the scenarios covered in each sample.</span></span> <span data-ttu-id="53bf6-107">按一下連結即可檢視 GitHub 中對應的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="53bf6-107">Click on the links to view the corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="53bf6-108">端點</span><span class="sxs-lookup"><span data-stu-id="53bf6-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="53bf6-109">案例</span><span class="sxs-lookup"><span data-stu-id="53bf6-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="53bf6-110">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="53bf6-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="53bf6-111"><b>Blob</b></span><span class="sxs-lookup"><span data-stu-id="53bf6-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="53bf6-112">附加 Blob</span><span class="sxs-lookup"><span data-stu-id="53bf6-112">Append Blob</span></span></td> 
<td><span data-ttu-id="53bf6-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-114">區塊 Blob</span><span class="sxs-lookup"><span data-stu-id="53bf6-114">Block Blob</span></span></td>
<td><span data-ttu-id="53bf6-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-116">用戶端加密</span><span class="sxs-lookup"><span data-stu-id="53bf6-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="53bf6-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">開始使用 Java 中的 Azure 用戶端加密</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-118">複製 Blob</span><span class="sxs-lookup"><span data-stu-id="53bf6-118">Copy Blob</span></span></td>
<td><span data-ttu-id="53bf6-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-120">建立容器</span><span class="sxs-lookup"><span data-stu-id="53bf6-120">Create Container</span></span></td>
<td><span data-ttu-id="53bf6-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-122">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="53bf6-122">Delete Blob</span></span></td>
<td><span data-ttu-id="53bf6-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-124">刪除容器</span><span class="sxs-lookup"><span data-stu-id="53bf6-124">Delete Container</span></span></td>
<td><span data-ttu-id="53bf6-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-126">Blob 中繼資料/屬性/統計資料</span><span class="sxs-lookup"><span data-stu-id="53bf6-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="53bf6-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">開始使用 Java 中的 Azure Blob 服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-128">容器 ACL/中繼資料/屬性</span><span class="sxs-lookup"><span data-stu-id="53bf6-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="53bf6-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">開始使用 Java 中的 Azure Blob 服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-130">取得頁面範圍</span><span class="sxs-lookup"><span data-stu-id="53bf6-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="53bf6-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">分頁 Blob 測試範例</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-132">租用 Blob/容器</span><span class="sxs-lookup"><span data-stu-id="53bf6-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="53bf6-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-134">列出 Blob/容器</span><span class="sxs-lookup"><span data-stu-id="53bf6-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="53bf6-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-136">分頁 Blob</span><span class="sxs-lookup"><span data-stu-id="53bf6-136">Page Blob</span></span></td>
<td><span data-ttu-id="53bf6-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="53bf6-138">SAS</span><span class="sxs-lookup"><span data-stu-id="53bf6-138">SAS</span></span></td>
<td><span data-ttu-id="53bf6-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS 測試範例</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="53bf6-140">服務屬性</span><span class="sxs-lookup"><span data-stu-id="53bf6-140">Service Properties</span></span></td>
<td><span data-ttu-id="53bf6-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">開始使用 Java 中的 Azure Blob 服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="53bf6-142">快照 Blob</span><span class="sxs-lookup"><span data-stu-id="53bf6-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="53bf6-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="53bf6-144"><b>檔案</b></span><span class="sxs-lookup"><span data-stu-id="53bf6-144"><b>File</b></span></span></td>
<td><span data-ttu-id="53bf6-145">建立共用/目錄/檔案</span><span class="sxs-lookup"><span data-stu-id="53bf6-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="53bf6-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">開始使用 Java 中的 Azure 檔案服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="53bf6-147">刪除共用/目錄/檔案</span><span class="sxs-lookup"><span data-stu-id="53bf6-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="53bf6-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">開始使用 Java 中的 Azure 檔案服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-149">目錄屬性/中繼資料</span><span class="sxs-lookup"><span data-stu-id="53bf6-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="53bf6-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">開始使用 Java 中的 Azure 檔案服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-151">下載檔案</span><span class="sxs-lookup"><span data-stu-id="53bf6-151">Download Files</span></span></td> 
<td><span data-ttu-id="53bf6-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">開始使用 Java 中的 Azure 檔案服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-153">檔案屬性/中繼資料/計量</span><span class="sxs-lookup"><span data-stu-id="53bf6-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="53bf6-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">開始使用 Java 中的 Azure 檔案服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-155">檔案服務屬性</span><span class="sxs-lookup"><span data-stu-id="53bf6-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="53bf6-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">開始使用 Java 中的 Azure 檔案服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-157">列出目錄和檔案</span><span class="sxs-lookup"><span data-stu-id="53bf6-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="53bf6-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">開始使用 Java 中的 Azure 檔案服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="53bf6-159">列出共用</span><span class="sxs-lookup"><span data-stu-id="53bf6-159">List Shares</span></span></td> 
<td><span data-ttu-id="53bf6-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">開始使用 Java 中的 Azure 檔案服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="53bf6-161">共用屬性/中繼資料/統計資料</span><span class="sxs-lookup"><span data-stu-id="53bf6-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="53bf6-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">開始使用 Java 中的 Azure 檔案服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="53bf6-163"><b>佇列</b></span><span class="sxs-lookup"><span data-stu-id="53bf6-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="53bf6-164">新增訊息</span><span class="sxs-lookup"><span data-stu-id="53bf6-164">Add Message</span></span></td> 
<td><span data-ttu-id="53bf6-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">儲存體 Java 用戶端程式庫範例</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-166">用戶端加密</span><span class="sxs-lookup"><span data-stu-id="53bf6-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="53bf6-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">儲存體 Java 用戶端程式庫範例</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-168">建立佇列</span><span class="sxs-lookup"><span data-stu-id="53bf6-168">Create Queues</span></span></td> 
<td><span data-ttu-id="53bf6-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">開始使用 Java 中的 Azure 佇列服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-170">刪除訊息/佇列</span><span class="sxs-lookup"><span data-stu-id="53bf6-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="53bf6-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">開始使用 Java 中的 Azure 佇列服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-172">查看訊息</span><span class="sxs-lookup"><span data-stu-id="53bf6-172">Peek Message</span></span></td> 
<td><span data-ttu-id="53bf6-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">開始使用 Java 中的 Azure 佇列服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-174">佇列 ACL/中繼資料/統計資料</span><span class="sxs-lookup"><span data-stu-id="53bf6-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="53bf6-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">開始使用 Java 中的 Azure 佇列服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-176">佇列服務屬性</span><span class="sxs-lookup"><span data-stu-id="53bf6-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="53bf6-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">開始使用 Java 中的 Azure 佇列服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-178">更新訊息</span><span class="sxs-lookup"><span data-stu-id="53bf6-178">Update Message</span></span></td> 
<td><span data-ttu-id="53bf6-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">開始使用 Java 中的 Azure 佇列服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="53bf6-180"><b>資料表</b></span><span class="sxs-lookup"><span data-stu-id="53bf6-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="53bf6-181">建立資料表</span><span class="sxs-lookup"><span data-stu-id="53bf6-181">Create Table</span></span></td> 
<td><span data-ttu-id="53bf6-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">開始使用 Java 中的 Azure 表格服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-183">刪除實體/資料表</span><span class="sxs-lookup"><span data-stu-id="53bf6-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="53bf6-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">開始使用 Java 中的 Azure 表格服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-185">插入/合併/取代實體</span><span class="sxs-lookup"><span data-stu-id="53bf6-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="53bf6-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">儲存體 Java 用戶端程式庫範例</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-187">查詢實體</span><span class="sxs-lookup"><span data-stu-id="53bf6-187">Query Entities</span></span></td> 
<td><span data-ttu-id="53bf6-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">開始使用 Java 中的 Azure 表格服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-189">查詢資料表</span><span class="sxs-lookup"><span data-stu-id="53bf6-189">Query Tables</span></span></td> 
<td><span data-ttu-id="53bf6-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">開始使用 Java 中的 Azure 表格服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-191">資料表 ACL/屬性</span><span class="sxs-lookup"><span data-stu-id="53bf6-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="53bf6-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">開始使用 Java 中的 Azure 表格服務</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="53bf6-193">更新實體</span><span class="sxs-lookup"><span data-stu-id="53bf6-193">Update Entity</span></span></td> 
<td><span data-ttu-id="53bf6-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">儲存體 Java 用戶端程式庫範例</a></span><span class="sxs-lookup"><span data-stu-id="53bf6-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="53bf6-195">Azure 程式碼範例程式庫</span><span class="sxs-lookup"><span data-stu-id="53bf6-195">Azure Code Samples library</span></span>

<span data-ttu-id="53bf6-196">若要檢視完整的範例程式庫，請移至 [Azure 程式碼範例](https://azure.microsoft.com/resources/samples/?service=storage)程式庫，其中包含您可以下載並在本機執行的「Azure 儲存體」範例。</span><span class="sxs-lookup"><span data-stu-id="53bf6-196">To view the complete sample library, go to the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="53bf6-197">程式碼範例程式庫會提供 .zip 格式的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="53bf6-197">The Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="53bf6-198">或者，您可以瀏覽並複製每個範例的 GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="53bf6-198">Alternatively, you can browse and clone the GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="53bf6-199">入門指南</span><span class="sxs-lookup"><span data-stu-id="53bf6-199">Getting started guides</span></span>

<span data-ttu-id="53bf6-200">如果您要尋找有關如何安裝和開始使用 Azure 儲存體用戶端程式庫的指示，請查看下列指南。</span><span class="sxs-lookup"><span data-stu-id="53bf6-200">Check out the following guides if you are looking for instructions on how to install and get started with the Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="53bf6-201">開始使用 Java 中的 Azure Blob 服務</span><span class="sxs-lookup"><span data-stu-id="53bf6-201">Getting Started with Azure Blob Service in Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="53bf6-202">開始使用 Java 中的 Azure 佇列服務</span><span class="sxs-lookup"><span data-stu-id="53bf6-202">Getting Started with Azure Queue Service in Java</span></span>](../storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="53bf6-203">開始使用 Java 中的 Azure 表格服務</span><span class="sxs-lookup"><span data-stu-id="53bf6-203">Getting Started with Azure Table Service in Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="53bf6-204">開始使用 Java 中的 Azure 檔案服務</span><span class="sxs-lookup"><span data-stu-id="53bf6-204">Getting Started with Azure File Service in Java</span></span>](../storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a><span data-ttu-id="53bf6-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="53bf6-205">Next steps</span></span>

<span data-ttu-id="53bf6-206">如需其他語言的範例相關資訊︰</span><span class="sxs-lookup"><span data-stu-id="53bf6-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="53bf6-207">.NET：[使用 .NET 的 Azure 儲存體範例](../storage-samples-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="53bf6-207">.NET: [Azure Storage samples using .NET](../storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="53bf6-208">所有其他語言︰[Azure 儲存體範例](../storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="53bf6-208">All other languages: [Azure Storage samples](../storage-samples.md)</span></span>
