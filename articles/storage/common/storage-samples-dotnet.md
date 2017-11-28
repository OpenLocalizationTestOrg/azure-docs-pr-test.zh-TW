---
title: "aaaAzure 使用適用於.NET 的儲存體範例 |Microsoft 文件"
description: "檢視、下載及執行 Azure 儲存體的範例程式碼和應用程式。 探索使用者入門範例 blob、 佇列、 表格和檔案，使用 hello.NET 儲存體用戶端程式庫。"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: 6b02b596f77845fc5fa474fa235c2b5df6e94ad7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="ba809-104">使用 .NET 的 Azure 儲存體範例</span><span class="sxs-lookup"><span data-stu-id="ba809-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="ba809-105">.NET 範例索引</span><span class="sxs-lookup"><span data-stu-id="ba809-105">.NET sample index</span></span>

<span data-ttu-id="ba809-106">hello 表概略說明我們的範例儲存機制和 hello 案例涵蓋的每個範例。</span><span class="sxs-lookup"><span data-stu-id="ba809-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="ba809-107">按一下 hello 連結 tooview hello 對應範例程式碼在 GitHub 中。</span><span class="sxs-lookup"><span data-stu-id="ba809-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="ba809-108">端點</span><span class="sxs-lookup"><span data-stu-id="ba809-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="ba809-109">案例</span><span class="sxs-lookup"><span data-stu-id="ba809-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="ba809-110">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="ba809-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="ba809-111"><b>Blob</b></span><span class="sxs-lookup"><span data-stu-id="ba809-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="ba809-112">附加 Blob</span><span class="sxs-lookup"><span data-stu-id="ba809-112">Append Blob</span></span></td> 
<td><span data-ttu-id="ba809-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference 方法範例 (英文)</a></span><span class="sxs-lookup"><span data-stu-id="ba809-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-114">區塊 Blob</span><span class="sxs-lookup"><span data-stu-id="ba809-114">Block Blob</span></span></td>
<td><span data-ttu-id="ba809-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application (Azure Blob 儲存體影像中心 Web 應用程式)</a></span><span class="sxs-lookup"><span data-stu-id="ba809-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ba809-116">用戶端加密</span><span class="sxs-lookup"><span data-stu-id="ba809-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="ba809-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob 加密範例</a></span><span class="sxs-lookup"><span data-stu-id="ba809-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ba809-118">複製 Blob</span><span class="sxs-lookup"><span data-stu-id="ba809-118">Copy Blob</span></span></td>
<td><span data-ttu-id="ba809-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">開始使用 Blob</a></span><span class="sxs-lookup"><span data-stu-id="ba809-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ba809-120">建立容器</span><span class="sxs-lookup"><span data-stu-id="ba809-120">Create Container</span></span></td>
<td><span data-ttu-id="ba809-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application (Azure Blob 儲存體影像中心 Web 應用程式)</a></span><span class="sxs-lookup"><span data-stu-id="ba809-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ba809-122">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="ba809-122">Delete Blob</span></span></td>
<td><span data-ttu-id="ba809-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application (Azure Blob 儲存體影像中心 Web 應用程式)</a></span><span class="sxs-lookup"><span data-stu-id="ba809-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ba809-124">刪除容器</span><span class="sxs-lookup"><span data-stu-id="ba809-124">Delete Container</span></span></td>
<td><span data-ttu-id="ba809-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">開始使用 Blob</a></span><span class="sxs-lookup"><span data-stu-id="ba809-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ba809-126">Blob 中繼資料/屬性/統計資料</span><span class="sxs-lookup"><span data-stu-id="ba809-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="ba809-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">開始使用 Blob</a></span><span class="sxs-lookup"><span data-stu-id="ba809-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ba809-128">容器 ACL/中繼資料/屬性</span><span class="sxs-lookup"><span data-stu-id="ba809-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="ba809-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application (Azure Blob 儲存體影像中心 Web 應用程式)</a></span><span class="sxs-lookup"><span data-stu-id="ba809-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ba809-130">取得頁面範圍</span><span class="sxs-lookup"><span data-stu-id="ba809-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="ba809-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">開始使用 Blob</a></span><span class="sxs-lookup"><span data-stu-id="ba809-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ba809-132">租用 Blob/容器</span><span class="sxs-lookup"><span data-stu-id="ba809-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="ba809-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">開始使用 Blob</a></span><span class="sxs-lookup"><span data-stu-id="ba809-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ba809-134">列出 Blob/容器</span><span class="sxs-lookup"><span data-stu-id="ba809-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="ba809-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">開始使用 Blob</a></span><span class="sxs-lookup"><span data-stu-id="ba809-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="ba809-136">分頁 Blob</span><span class="sxs-lookup"><span data-stu-id="ba809-136">Page Blob</span></span></td>
<td><span data-ttu-id="ba809-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">開始使用 Blob</a></span><span class="sxs-lookup"><span data-stu-id="ba809-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="ba809-138">SAS</span><span class="sxs-lookup"><span data-stu-id="ba809-138">SAS</span></span></td>
<td><span data-ttu-id="ba809-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">開始使用 Blob</a></span><span class="sxs-lookup"><span data-stu-id="ba809-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="ba809-140">服務屬性</span><span class="sxs-lookup"><span data-stu-id="ba809-140">Service Properties</span></span></td>
<td><span data-ttu-id="ba809-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">開始使用 Blob</a></span><span class="sxs-lookup"><span data-stu-id="ba809-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="ba809-142">快照 Blob</span><span class="sxs-lookup"><span data-stu-id="ba809-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="ba809-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">使用增量快照備份 Azure 虛擬機器磁碟</a></span><span class="sxs-lookup"><span data-stu-id="ba809-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="ba809-144"><b>檔案</b></span><span class="sxs-lookup"><span data-stu-id="ba809-144"><b>File</b></span></span></td>
<td><span data-ttu-id="ba809-145">建立共用/目錄/檔案</span><span class="sxs-lookup"><span data-stu-id="ba809-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="ba809-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure 儲存體 .NET 檔案儲存體範例</a></span><span class="sxs-lookup"><span data-stu-id="ba809-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="ba809-147">刪除共用/目錄/檔案</span><span class="sxs-lookup"><span data-stu-id="ba809-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="ba809-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET (開始使用 .NET 中的 Azure 檔案服務)</a></span><span class="sxs-lookup"><span data-stu-id="ba809-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-149">目錄屬性/中繼資料</span><span class="sxs-lookup"><span data-stu-id="ba809-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="ba809-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure 儲存體 .NET 檔案儲存體範例</a></span><span class="sxs-lookup"><span data-stu-id="ba809-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-151">下載檔案</span><span class="sxs-lookup"><span data-stu-id="ba809-151">Download Files</span></span></td> 
<td><span data-ttu-id="ba809-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure 儲存體 .NET 檔案儲存體範例</a></span><span class="sxs-lookup"><span data-stu-id="ba809-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-153">檔案屬性/中繼資料/計量</span><span class="sxs-lookup"><span data-stu-id="ba809-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="ba809-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure 儲存體 .NET 檔案儲存體範例</a></span><span class="sxs-lookup"><span data-stu-id="ba809-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-155">檔案服務屬性</span><span class="sxs-lookup"><span data-stu-id="ba809-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="ba809-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure 儲存體 .NET 檔案儲存體範例</a></span><span class="sxs-lookup"><span data-stu-id="ba809-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-157">列出目錄和檔案</span><span class="sxs-lookup"><span data-stu-id="ba809-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="ba809-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure 儲存體 .NET 檔案儲存體範例</a></span><span class="sxs-lookup"><span data-stu-id="ba809-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="ba809-159">列出共用</span><span class="sxs-lookup"><span data-stu-id="ba809-159">List Shares</span></span></td> 
<td><span data-ttu-id="ba809-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure 儲存體 .NET 檔案儲存體範例</a></span><span class="sxs-lookup"><span data-stu-id="ba809-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="ba809-161">共用屬性/中繼資料/統計資料</span><span class="sxs-lookup"><span data-stu-id="ba809-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="ba809-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure 儲存體 .NET 檔案儲存體範例</a></span><span class="sxs-lookup"><span data-stu-id="ba809-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="ba809-163"><b>佇列</b></span><span class="sxs-lookup"><span data-stu-id="ba809-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="ba809-164">新增訊息</span><span class="sxs-lookup"><span data-stu-id="ba809-164">Add Message</span></span></td> 
<td><span data-ttu-id="ba809-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET (開始使用 .NET 中的 Azure 佇列服務)</a></span><span class="sxs-lookup"><span data-stu-id="ba809-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-166">用戶端加密</span><span class="sxs-lookup"><span data-stu-id="ba809-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="ba809-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure 儲存體 .NET 佇列用戶端加密</a></span><span class="sxs-lookup"><span data-stu-id="ba809-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-168">建立佇列</span><span class="sxs-lookup"><span data-stu-id="ba809-168">Create Queues</span></span></td> 
<td><span data-ttu-id="ba809-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET (開始使用 .NET 中的 Azure 佇列服務)</a></span><span class="sxs-lookup"><span data-stu-id="ba809-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-170">刪除訊息/佇列</span><span class="sxs-lookup"><span data-stu-id="ba809-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="ba809-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET (開始使用 .NET 中的 Azure 佇列服務)</a></span><span class="sxs-lookup"><span data-stu-id="ba809-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-172">查看訊息</span><span class="sxs-lookup"><span data-stu-id="ba809-172">Peek Message</span></span></td> 
<td><span data-ttu-id="ba809-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET (開始使用 .NET 中的 Azure 佇列服務)</a></span><span class="sxs-lookup"><span data-stu-id="ba809-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-174">佇列 ACL/中繼資料/統計資料</span><span class="sxs-lookup"><span data-stu-id="ba809-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="ba809-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET (開始使用 .NET 中的 Azure 佇列服務)</a></span><span class="sxs-lookup"><span data-stu-id="ba809-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-176">佇列服務屬性</span><span class="sxs-lookup"><span data-stu-id="ba809-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="ba809-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET (開始使用 .NET 中的 Azure 佇列服務)</a></span><span class="sxs-lookup"><span data-stu-id="ba809-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-178">更新訊息</span><span class="sxs-lookup"><span data-stu-id="ba809-178">Update Message</span></span></td> 
<td><span data-ttu-id="ba809-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET (開始使用 .NET 中的 Azure 佇列服務)</a></span><span class="sxs-lookup"><span data-stu-id="ba809-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="ba809-180"><b>資料表</b></span><span class="sxs-lookup"><span data-stu-id="ba809-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="ba809-181">建立資料表</span><span class="sxs-lookup"><span data-stu-id="ba809-181">Create Table</span></span></td> 
<td><span data-ttu-id="ba809-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">使用 Azure 儲存體管理並行存取 - 範例應用程式</a></span><span class="sxs-lookup"><span data-stu-id="ba809-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-183">刪除實體/資料表</span><span class="sxs-lookup"><span data-stu-id="ba809-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="ba809-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">在 .NET 中開始使用 Azure 表格儲存體</a></span><span class="sxs-lookup"><span data-stu-id="ba809-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-185">插入/合併/取代實體</span><span class="sxs-lookup"><span data-stu-id="ba809-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="ba809-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">使用 Azure 儲存體管理並行存取 - 範例應用程式</a></span><span class="sxs-lookup"><span data-stu-id="ba809-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-187">查詢實體</span><span class="sxs-lookup"><span data-stu-id="ba809-187">Query Entities</span></span></td> 
<td><span data-ttu-id="ba809-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">在 .NET 中開始使用 Azure 表格儲存體</a></span><span class="sxs-lookup"><span data-stu-id="ba809-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-189">查詢資料表</span><span class="sxs-lookup"><span data-stu-id="ba809-189">Query Tables</span></span></td> 
<td><span data-ttu-id="ba809-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">在 .NET 中開始使用 Azure 表格儲存體</a></span><span class="sxs-lookup"><span data-stu-id="ba809-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-191">資料表 ACL/屬性</span><span class="sxs-lookup"><span data-stu-id="ba809-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="ba809-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">在 .NET 中開始使用 Azure 表格儲存體</a></span><span class="sxs-lookup"><span data-stu-id="ba809-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="ba809-193">更新實體</span><span class="sxs-lookup"><span data-stu-id="ba809-193">Update Entity</span></span></td> 
<td><span data-ttu-id="ba809-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">使用 Azure 儲存體管理並行存取 - 範例應用程式</a></span><span class="sxs-lookup"><span data-stu-id="ba809-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="ba809-195">Azure 程式碼範例程式庫</span><span class="sxs-lookup"><span data-stu-id="ba809-195">Azure Code Samples library</span></span>

<span data-ttu-id="ba809-196">tooview hello 完整的範例程式庫，請移 toohello [Azure 程式碼範例](https://azure.microsoft.com/resources/samples/?service=storage)程式庫，包括 Azure 儲存體，您可以下載並在本機執行的範例。</span><span class="sxs-lookup"><span data-stu-id="ba809-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="ba809-197">hello 程式碼範例庫提供以.zip 格式的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="ba809-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="ba809-198">或者，您可以瀏覽，然後複製每個範例 hello GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="ba809-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="ba809-199">入門指南</span><span class="sxs-lookup"><span data-stu-id="ba809-199">Getting started guides</span></span>

<span data-ttu-id="ba809-200">請參閱下列指南，如果您要尋找的指示 hello tooinstall 並開始使用 hello Azure 儲存體用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="ba809-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="ba809-201">Getting Started with Azure Blob Service in .NET (開始使用 .NET 中的 Azure Blob 服務)</span><span class="sxs-lookup"><span data-stu-id="ba809-201">Getting Started with Azure Blob Service in .NET</span></span>](../blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="ba809-202">Getting Started with Azure Queue Service in .NET (開始使用 .NET 中的 Azure 佇列服務)</span><span class="sxs-lookup"><span data-stu-id="ba809-202">Getting Started with Azure Queue Service in .NET</span></span>](../storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="ba809-203">Getting Started with Azure Table Service in .NET (開始使用 .NET 中的 Azure 表格服務)</span><span class="sxs-lookup"><span data-stu-id="ba809-203">Getting Started with Azure Table Service in .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="ba809-204">Getting Started with Azure File Service in .NET (開始使用 .NET 中的 Azure 檔案服務)</span><span class="sxs-lookup"><span data-stu-id="ba809-204">Getting Started with Azure File Service in .NET</span></span>](../storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="ba809-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba809-205">Next steps</span></span>

<span data-ttu-id="ba809-206">如需其他語言的範例相關資訊︰</span><span class="sxs-lookup"><span data-stu-id="ba809-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="ba809-207">Java：[使用 Java 的 Azure 儲存體範例](storage-samples-java.md)</span><span class="sxs-lookup"><span data-stu-id="ba809-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="ba809-208">所有其他語言︰[Azure 儲存體範例](../storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="ba809-208">All other languages: [Azure Storage samples](../storage-samples.md)</span></span>
