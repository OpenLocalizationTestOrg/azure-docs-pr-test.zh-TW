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
# <a name="introduction-tooqueues"></a><span data-ttu-id="fb58d-103">簡介 tooQueues</span><span class="sxs-lookup"><span data-stu-id="fb58d-103">Introduction tooQueues</span></span>

<span data-ttu-id="fb58d-104">Azure 佇列儲存體是用於儲存大量訊息，可透過使用 HTTP 或 HTTPS 驗證呼叫的 hello world 中從任何地方存取服務。</span><span class="sxs-lookup"><span data-stu-id="fb58d-104">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="fb58d-105">單一佇列訊息可以是總 too64 KB 的大小，並佇列可以包含數百萬個訊息，向上 toohello 總容量限制的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fb58d-105">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="common-uses"></a><span data-ttu-id="fb58d-106">常見用途</span><span class="sxs-lookup"><span data-stu-id="fb58d-106">Common uses</span></span>

<span data-ttu-id="fb58d-107">佇列儲存體的一般用途包括：</span><span class="sxs-lookup"><span data-stu-id="fb58d-107">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="fb58d-108">以非同步方式建立工作 tooprocess 待辦項的目</span><span class="sxs-lookup"><span data-stu-id="fb58d-108">Creating a backlog of work tooprocess asynchronously</span></span>
* <span data-ttu-id="fb58d-109">從 Azure web 角色 tooan Azure 背景工作角色傳遞訊息</span><span class="sxs-lookup"><span data-stu-id="fb58d-109">Passing messages from an Azure web role tooan Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="fb58d-110">佇列服務概念</span><span class="sxs-lookup"><span data-stu-id="fb58d-110">Queue service concepts</span></span>

<span data-ttu-id="fb58d-111">hello 佇列服務包含下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="fb58d-111">hello Queue service contains hello following components:</span></span>

![佇列概念](./media/storage-queues-introduction/queue1.png)

* <span data-ttu-id="fb58d-113">**URL 格式：**可以使用 hello 下列 URL 格式來定址佇列：</span><span class="sxs-lookup"><span data-stu-id="fb58d-113">**URL format:** Queues are addressable using hello following URL format:</span></span>   
    <span data-ttu-id="fb58d-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="fb58d-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="fb58d-115">下列 URL 的 hello 解決 hello 圖表中的佇列：</span><span class="sxs-lookup"><span data-stu-id="fb58d-115">hello following URL addresses a queue in hello diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="fb58d-116">**儲存體帳戶：**所有存取的 tooAzure 是儲存體透過儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fb58d-116">**Storage account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="fb58d-117">如需關於儲存體帳戶容量的詳細資訊，請參閱＜ [Azure 儲存體延展性和效能目標](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) ＞(英文)。</span><span class="sxs-lookup"><span data-stu-id="fb58d-117">See [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="fb58d-118">**佇列：** 佇列包含一組訊息。</span><span class="sxs-lookup"><span data-stu-id="fb58d-118">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="fb58d-119">所有訊息都必須放在佇列中。</span><span class="sxs-lookup"><span data-stu-id="fb58d-119">All messages must be in a queue.</span></span> <span data-ttu-id="fb58d-120">請注意該 hello 佇列名稱必須全部小寫。</span><span class="sxs-lookup"><span data-stu-id="fb58d-120">Note that hello queue name must be all lowercase.</span></span> <span data-ttu-id="fb58d-121">如需為佇列命名的詳細資訊，請參閱 [為佇列和中繼資料命名](https://msdn.microsoft.com/library/azure/dd179349.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fb58d-121">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

* <span data-ttu-id="fb58d-122">**訊息：**的訊息，任何格式的總 too64 KB。</span><span class="sxs-lookup"><span data-stu-id="fb58d-122">**Message:** A message, in any format, of up too64 KB.</span></span> <span data-ttu-id="fb58d-123">hello 訊息保留在 hello 佇列中的最大時間是七天。</span><span class="sxs-lookup"><span data-stu-id="fb58d-123">hello maximum time that a message can remain in hello queue is seven days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb58d-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fb58d-124">Next steps</span></span>

* [<span data-ttu-id="fb58d-125">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="fb58d-125">Create a storage account</span></span>](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="fb58d-126">透過 .NET 開始使用佇列</span><span class="sxs-lookup"><span data-stu-id="fb58d-126">Getting started with Queues using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
