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
# <a name="how-toouse-azure-redis-cache-with-python"></a>如何 toouse Azure Redis 快取使用 Python
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

本主題說明您如何 tooget 開始使用 Azure Redis 快取使用 Python。

## <a name="prerequisites"></a>必要條件
安裝 [redis-py](https://github.com/andymccurdy/redis-py)。

## <a name="create-a-redis-cache-on-azure"></a>在 Azure 上建立 Redis 快取
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>擷取 hello 主機名稱和存取金鑰
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-hello-non-ssl-endpoint"></a>啟用 hello 非 SSL 端點
有些 Redis 用戶端不支援 SSL，以及預設 hello[非 SSL 連接埠已停用新的 Azure Redis 快取執行個體](cache-configure.md#access-ports)。 Hello 撰寫本文時，在 hello [redis py](https://github.com/andymccurdy/redis-py)用戶端不支援 SSL。 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-toohello-cache-and-retrieve-it"></a>加入一些內容 toohello 快取並擷取它
    >>> import redis
    >>> r = redis.StrictRedis(host='<name>.redis.cache.windows.net',
          port=6380, db=0, password='<key>', ssl=True)
    >>> r.set('foo', 'bar')
    True
    >>> r.get('foo')
    b'bar'


將 `<name>` 取代為您的快取名稱，並將 `key` 取代為您的存取金鑰。

<!--Image references-->
[1]: ./media/cache-python-get-started/redis-cache-new-cache-menu.png
[2]: ./media/cache-python-get-started/redis-cache-cache-create.png
