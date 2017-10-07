---
title: "aaaIntroduction tooAzure Blob 儲存體 |Microsoft 文件"
description: "簡介 tooAzure Blob 儲存體"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: robinsh
ms.openlocfilehash: 3431f826ae51d42dbced084ee60f9ff70a8168d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooblob-storage"></a>簡介 tooBlob 儲存體

Azure Blob 儲存體是用於儲存大量非結構化的物件的資料，例如文字或二進位資料，可以在 hello world，透過 HTTP 或 HTTPS 從任何地方存取服務。 您可以使用 Blob 儲存體 tooexpose 資料公開 toohello 世界中或 toostore 應用程式資料未公開。

Blob 儲存體的一般用途包括：

* 服務映像，或直接文 tooa 瀏覽器
* 儲存檔案供分散式存取
* 串流傳輸視訊和音訊
* 儲存備份和還原、災害復原和封存資料
* 儲存資料供內部部署或 Azure 託管服務進行分析

## <a name="blob-service-concepts"></a>Blob 服務概念

hello Blob 服務包含下列元件的 hello:

![Blob 架構](./media/storage-blobs-introduction/blob1.png)

* **儲存體帳戶：**所有存取的 tooAzure 是儲存體透過儲存體帳戶。 此儲存體帳戶可以是**一般用途的儲存體帳戶**或專門用於儲存物件/Blob 的 **Blob 儲存體帳戶**。 如需詳細資訊，請參閱[關於 Azure 儲存體帳戶](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)。

* **容器：** 容器提供一組 Blob 的群組。 所有 Blob 都必須放在容器中。 一個帳戶可以包含的容器不限數量。 容器可以儲存無限制的 Blob。 請注意該 hello 容器名稱必須是小寫。

* **Blob：** 任何類型和大小的檔案。 Azure 儲存體提供三種類型的 Blob：區塊 Blob、分頁 Blob 及附加 Blob。
  
    *區塊 Blob* 很適合儲存文字或二進位檔案，例如文件和媒體檔案。 *附加 blob*會類似 tooblock blob 的區塊，由組成，但它們會針對最佳化在所附加作業，讓它們可用於記錄的案例。 單一區塊 blob 可包含總 too50，000 區塊 too100 MB，總稍微大於 4.75 TB (100 MB X 50000) 的總大小。 單一附加 blob 可包含總 too50，000 區塊 too4 MB，總稍微超過 195 GB (4 MB X 50000) 的總大小。
  
    *分頁 blob*最長 too1 TB 的大小，可能會和更頻繁的讀取/寫入作業時很有效率。 Azure 虛擬機器會使用分頁 Blob 作為作業系統和資料磁碟。
  
    如需有關命名容器和 Blob 的詳細資訊，請參閱 [命名和參考容器、Blob 及中繼資料](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata)。

## <a name="next-steps"></a>後續步驟

* [建立儲存體帳戶](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [透過 .NET 開始使用 Blob 儲存體](storage-dotnet-how-to-use-blobs.md)