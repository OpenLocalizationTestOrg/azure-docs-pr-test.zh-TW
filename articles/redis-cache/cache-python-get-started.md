---
title: "aaaHow toouse Azure Redis 快取使用 Python |Microsoft 文件"
description: "開始搭配使用 Azure Redis 快取與 Python"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: f186202c-fdad-4398-af8c-aee91ec96ba3
ms.service: cache
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: 74c03eb4ce17ff3574595fd2bb37e399d71c6eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-python"></a><span data-ttu-id="d68b2-103">如何 toouse Azure Redis 快取使用 Python</span><span class="sxs-lookup"><span data-stu-id="d68b2-103">How toouse Azure Redis Cache with Python</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d68b2-104">.NET</span><span class="sxs-lookup"><span data-stu-id="d68b2-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="d68b2-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d68b2-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="d68b2-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="d68b2-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="d68b2-107">Java</span><span class="sxs-lookup"><span data-stu-id="d68b2-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="d68b2-108">Python</span><span class="sxs-lookup"><span data-stu-id="d68b2-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="d68b2-109">本主題說明您如何 tooget 開始使用 Azure Redis 快取使用 Python。</span><span class="sxs-lookup"><span data-stu-id="d68b2-109">This topic shows you how tooget started with Azure Redis Cache using Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d68b2-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d68b2-110">Prerequisites</span></span>
<span data-ttu-id="d68b2-111">安裝 [redis-py](https://github.com/andymccurdy/redis-py)。</span><span class="sxs-lookup"><span data-stu-id="d68b2-111">Install [redis-py](https://github.com/andymccurdy/redis-py).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="d68b2-112">在 Azure 上建立 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="d68b2-112">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="d68b2-113">擷取 hello 主機名稱和存取金鑰</span><span class="sxs-lookup"><span data-stu-id="d68b2-113">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-hello-non-ssl-endpoint"></a><span data-ttu-id="d68b2-114">啟用 hello 非 SSL 端點</span><span class="sxs-lookup"><span data-stu-id="d68b2-114">Enable hello non-SSL endpoint</span></span>
<span data-ttu-id="d68b2-115">有些 Redis 用戶端不支援 SSL，以及預設 hello[非 SSL 連接埠已停用新的 Azure Redis 快取執行個體](cache-configure.md#access-ports)。</span><span class="sxs-lookup"><span data-stu-id="d68b2-115">Some Redis clients don't support SSL, and by default hello [non-SSL port is disabled for new Azure Redis Cache instances](cache-configure.md#access-ports).</span></span> <span data-ttu-id="d68b2-116">Hello 撰寫本文時，在 hello [redis py](https://github.com/andymccurdy/redis-py)用戶端不支援 SSL。</span><span class="sxs-lookup"><span data-stu-id="d68b2-116">At hello time of this writing, hello [redis-py](https://github.com/andymccurdy/redis-py) client doesn't support SSL.</span></span> 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="d68b2-117">加入一些內容 toohello 快取並擷取它</span><span class="sxs-lookup"><span data-stu-id="d68b2-117">Add something toohello cache and retrieve it</span></span>
    >>> import redis
    >>> r = redis.StrictRedis(host='<name>.redis.cache.windows.net',
          port=6380, db=0, password='<key>', ssl=True)
    >>> r.set('foo', 'bar')
    True
    >>> r.get('foo')
    b'bar'


<span data-ttu-id="d68b2-118">將 `<name>` 取代為您的快取名稱，並將 `key` 取代為您的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="d68b2-118">Replace `<name>` with your cache name and `key` with your access key.</span></span>

<!--Image references-->
[1]: ./media/cache-python-get-started/redis-cache-new-cache-menu.png
[2]: ./media/cache-python-get-started/redis-cache-cache-create.png
