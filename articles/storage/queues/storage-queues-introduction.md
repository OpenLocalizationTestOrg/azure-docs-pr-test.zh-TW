---
title: "aaaIntroduction tooAzure 佇列儲存體 |Microsoft 文件"
description: "簡介 tooAzure 佇列儲存體"
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
ms.date: 08/07/2017
ms.author: robinsh
ms.openlocfilehash: 669effedff7beedde8a119c350a2a70edafedcf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooqueues"></a>簡介 tooQueues

Azure 佇列儲存體是用於儲存大量訊息，可透過使用 HTTP 或 HTTPS 驗證呼叫的 hello world 中從任何地方存取服務。 單一佇列訊息可以是總 too64 KB 的大小，並佇列可以包含數百萬個訊息，向上 toohello 總容量限制的儲存體帳戶。

## <a name="common-uses"></a>常見用途

佇列儲存體的一般用途包括：

* 以非同步方式建立工作 tooprocess 待辦項的目
* 從 Azure web 角色 tooan Azure 背景工作角色傳遞訊息

## <a name="queue-service-concepts"></a>佇列服務概念

hello 佇列服務包含下列元件的 hello:

![佇列概念](./media/storage-queues-introduction/queue1.png)

* **URL 格式：**可以使用 hello 下列 URL 格式來定址佇列：   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    下列 URL 的 hello 解決 hello 圖表中的佇列：  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **儲存體帳戶：**所有存取的 tooAzure 是儲存體透過儲存體帳戶。 如需關於儲存體帳戶容量的詳細資訊，請參閱＜ [Azure 儲存體延展性和效能目標](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) ＞(英文)。

* **佇列：** 佇列包含一組訊息。 所有訊息都必須放在佇列中。 請注意該 hello 佇列名稱必須全部小寫。 如需為佇列命名的詳細資訊，請參閱 [為佇列和中繼資料命名](https://msdn.microsoft.com/library/azure/dd179349.aspx)。

* **訊息：**的訊息，任何格式的總 too64 KB。 hello 訊息保留在 hello 佇列中的最大時間是七天。

## <a name="next-steps"></a>後續步驟

* [建立儲存體帳戶](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [透過 .NET 開始使用佇列](storage-dotnet-how-to-use-queues.md)
