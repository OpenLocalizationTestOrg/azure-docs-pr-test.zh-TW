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
# <a name="azure-storage-samples-using-java"></a>使用 Java 的 Azure 儲存體範例

## <a name="java-sample-index"></a>Java 範例索引

下表提供我們的範例儲存機制和每個範例所涵蓋案例的概觀。 按一下連結即可檢視 GitHub 中對應的範例程式碼。

<table style="font-size:90%"><thead><tr><th style="font-size:110%">端點</th><th style="font-size:110%">案例</th><th style="font-size:110%">範例程式碼</th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><b>Blob</b></td>
<td>附加 Blob</td> 
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></td> 
</tr> 
<tr> 
<td>區塊 Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></td>
</tr> 
<tr> 
<td>用戶端加密</td>
<td><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">開始使用 Java 中的 Azure 用戶端加密</a></td>
</tr> 
<tr> 
<td>複製 Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></td>
</tr> 
<tr> 
<td>建立容器</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></td>
</tr> 
<tr> 
<td>刪除 Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></td>
</tr> 
<tr> 
<td>刪除容器</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></td>
</tr> 
<tr> 
<td>Blob 中繼資料/屬性/統計資料</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">開始使用 Java 中的 Azure Blob 服務</a></td>
</tr> 
<tr> 
<td>容器 ACL/中繼資料/屬性</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">開始使用 Java 中的 Azure Blob 服務</a></td>
</tr> 
<tr> 
<td>取得頁面範圍</td>
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">分頁 Blob 測試範例</a></td>
</tr> 
<tr> 
<td>租用 Blob/容器</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></td>
</tr> 
<tr> 
<td>列出 Blob/容器</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></td>
</tr> 
<tr> 
<td>分頁 Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></td>
</tr>
<tr> 
<td>SAS</td>
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS 測試範例</a></td>
</tr>   
<tr> 
<td>服務屬性</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">開始使用 Java 中的 Azure Blob 服務</a></td>
</tr>           
<tr> 
<td>快照 Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">開始使用 Java 中的 Azure Blob 服務</a></td>
</tr> 
<tr> 
<td rowspan="9"><b>檔案</b></td>
<td>建立共用/目錄/檔案</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">開始使用 Java 中的 Azure 檔案服務</a></td> 
</tr>
<tr> 
<td>刪除共用/目錄/檔案</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">開始使用 Java 中的 Azure 檔案服務</a></td> 
</tr> 
<tr> 
<td>目錄屬性/中繼資料</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">開始使用 Java 中的 Azure 檔案服務</a></td> 
</tr> 
<tr> 
<td>下載檔案</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">開始使用 Java 中的 Azure 檔案服務</a></td> 
</tr> 
<tr> 
<td>檔案屬性/中繼資料/計量</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">開始使用 Java 中的 Azure 檔案服務</a></td> 
</tr> 
<tr> 
<td>檔案服務屬性</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">開始使用 Java 中的 Azure 檔案服務</a></td> 
</tr> 
<tr> 
<td>列出目錄和檔案</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">開始使用 Java 中的 Azure 檔案服務</a></td> 
</tr>
<tr> 
<td>列出共用</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">開始使用 Java 中的 Azure 檔案服務</a></td> 
</tr>
<tr> 
<td>共用屬性/中繼資料/統計資料</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">開始使用 Java 中的 Azure 檔案服務</a></td> 
</tr>
<tr> 
<td rowspan="8"><b>佇列</b></td>
<td>新增訊息</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">儲存體 Java 用戶端程式庫範例</a></td> 
</tr> 
<tr> 
<td>用戶端加密</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">儲存體 Java 用戶端程式庫範例</a></td> 
</tr> 
<tr> 
<td>建立佇列</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">開始使用 Java 中的 Azure 佇列服務</a></td> 
</tr> 
<tr> 
<td>刪除訊息/佇列</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">開始使用 Java 中的 Azure 佇列服務</a></td> 
</tr> 
<tr> 
<td>查看訊息</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">開始使用 Java 中的 Azure 佇列服務</a></td> 
</tr> 
<tr> 
<td>佇列 ACL/中繼資料/統計資料</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">開始使用 Java 中的 Azure 佇列服務</a></td> 
</tr> 
<tr> 
<td>佇列服務屬性</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">開始使用 Java 中的 Azure 佇列服務</a></td> 
</tr> 
<tr> 
<td>更新訊息</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">開始使用 Java 中的 Azure 佇列服務</a></td> 
</tr> 
<tr> 
<td rowspan="7"><b>資料表</b></td>
<td>建立資料表</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">開始使用 Java 中的 Azure 表格服務</a></td> 
</tr> 
<tr> 
<td>刪除實體/資料表</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">開始使用 Java 中的 Azure 表格服務</a></td> 
</tr> 
<tr> 
<td>插入/合併/取代實體</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">儲存體 Java 用戶端程式庫範例</a></td> 
</tr> 
<tr> 
<td>查詢實體</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">開始使用 Java 中的 Azure 表格服務</a></td> 
</tr> 
<tr> 
<td>查詢資料表</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">開始使用 Java 中的 Azure 表格服務</a></td> 
</tr> 
<tr> 
<td>資料表 ACL/屬性</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">開始使用 Java 中的 Azure 表格服務</a></td> 
</tr> 
<tr> 
<td>更新實體</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">儲存體 Java 用戶端程式庫範例</a></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a>Azure 程式碼範例程式庫

若要檢視完整的範例程式庫，請移至 [Azure 程式碼範例](https://azure.microsoft.com/resources/samples/?service=storage)程式庫，其中包含您可以下載並在本機執行的「Azure 儲存體」範例。 程式碼範例程式庫會提供 .zip 格式的範例程式碼。 或者，您可以瀏覽並複製每個範例的 GitHub 儲存機制。

[!INCLUDE [storage-java-samples-include](../../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a>入門指南

如果您要尋找有關如何安裝和開始使用 Azure 儲存體用戶端程式庫的指示，請查看下列指南。

* [開始使用 Java 中的 Azure Blob 服務](../blobs/storage-java-how-to-use-blob-storage.md)
* [開始使用 Java 中的 Azure 佇列服務](../storage-java-how-to-use-queue-storage.md)
* [開始使用 Java 中的 Azure 表格服務](../../cosmos-db/table-storage-how-to-use-java.md)
* [開始使用 Java 中的 Azure 檔案服務](../storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a>後續步驟

如需其他語言的範例相關資訊︰

* .NET：[使用 .NET 的 Azure 儲存體範例](../storage-samples-dotnet.md)
* 所有其他語言︰[Azure 儲存體範例](../storage-samples.md)
