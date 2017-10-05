---
title: "如何搭配使用 Azure Redis 快取與 Python | Microsoft Docs"
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
ms.openlocfilehash: cdbee52574d0ffbe82ef3dc98f2848f4d00ba2ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-python"></a><span data-ttu-id="1c4f5-103">如何搭配使用 Azure Redis 快取與 Python</span><span class="sxs-lookup"><span data-stu-id="1c4f5-103">How to use Azure Redis Cache with Python</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c4f5-104">.NET</span><span class="sxs-lookup"><span data-stu-id="1c4f5-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="1c4f5-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1c4f5-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="1c4f5-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="1c4f5-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="1c4f5-107">Java</span><span class="sxs-lookup"><span data-stu-id="1c4f5-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="1c4f5-108">Python</span><span class="sxs-lookup"><span data-stu-id="1c4f5-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="1c4f5-109">本主題說明如何搭配使用 Azure Redis 快取與 Python。</span><span class="sxs-lookup"><span data-stu-id="1c4f5-109">This topic shows you how to get started with Azure Redis Cache using Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c4f5-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1c4f5-110">Prerequisites</span></span>
<span data-ttu-id="1c4f5-111">安裝 [redis-py](https://github.com/andymccurdy/redis-py)。</span><span class="sxs-lookup"><span data-stu-id="1c4f5-111">Install [redis-py](https://github.com/andymccurdy/redis-py).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="1c4f5-112">在 Azure 上建立 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="1c4f5-112">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="1c4f5-113">擷取主機名稱和存取金鑰</span><span class="sxs-lookup"><span data-stu-id="1c4f5-113">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-the-non-ssl-endpoint"></a><span data-ttu-id="1c4f5-114">啟用非 SSL 端點</span><span class="sxs-lookup"><span data-stu-id="1c4f5-114">Enable the non-SSL endpoint</span></span>
<span data-ttu-id="1c4f5-115">有些 Redis 用戶端不支援 SSL，且預設會 [停用新的 Azure Redis 快取執行個體的非 SSL 連接埠](cache-configure.md#access-ports)。</span><span class="sxs-lookup"><span data-stu-id="1c4f5-115">Some Redis clients don't support SSL, and by default the [non-SSL port is disabled for new Azure Redis Cache instances](cache-configure.md#access-ports).</span></span> <span data-ttu-id="1c4f5-116">在本文撰寫當下， [redis-py](https://github.com/andymccurdy/redis-py) 用戶端不支援 SSL。</span><span class="sxs-lookup"><span data-stu-id="1c4f5-116">At the time of this writing, the [redis-py](https://github.com/andymccurdy/redis-py) client doesn't support SSL.</span></span> 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="1c4f5-117">在快取中加入項目並擷取該項目</span><span class="sxs-lookup"><span data-stu-id="1c4f5-117">Add something to the cache and retrieve it</span></span>
    >>> import redis
    >>> r = redis.StrictRedis(host='<name>.redis.cache.windows.net',
          port=6380, db=0, password='<key>', ssl=True)
    >>> r.set('foo', 'bar')
    True
    >>> r.get('foo')
    b'bar'


<span data-ttu-id="1c4f5-118">將 `<name>` 取代為您的快取名稱，並將 `key` 取代為您的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="1c4f5-118">Replace `<name>` with your cache name and `key` with your access key.</span></span>

<!--Image references-->
[1]: ./media/cache-python-get-started/redis-cache-new-cache-menu.png
[2]: ./media/cache-python-get-started/redis-cache-cache-create.png
