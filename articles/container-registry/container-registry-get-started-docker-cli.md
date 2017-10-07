---
title: "aaaPush Docker 映像 tooprivate Azure 登錄 |Microsoft 文件"
description: "發送和提取 Docker 映像 tooa 私用容器登錄在 Azure 中使用 hello Docker CLI"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a><span data-ttu-id="6c3ad-103">推入第一個影像 tooa 私用 Docker 容器登錄使用 hello Docker CLI</span><span class="sxs-lookup"><span data-stu-id="6c3ad-103">Push your first image tooa private Docker container registry using hello Docker CLI</span></span>
<span data-ttu-id="6c3ad-104">Azure 容器登錄中儲存和管理私人[Docker](http://hub.docker.com)容器映像、 類似 toohello 方式[Docker Hub](https://hub.docker.com/)存放公用 Docker 映像檔。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar toohello way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="6c3ad-105">使用 hello [Docker 命令列介面](https://docs.docker.com/engine/reference/commandline/cli/)(Docker CLI) 的[登入](https://docs.docker.com/engine/reference/commandline/login/)，[發送](https://docs.docker.com/engine/reference/commandline/push/)，[提取](https://docs.docker.com/engine/reference/commandline/pull/)，和您的容器上的其他操作登錄中。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-105">You use hello [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="6c3ad-106">如需背景和概念，請參閱[hello 概觀](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="6c3ad-106">For more background and concepts, see [hello overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="6c3ad-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="6c3ad-107">Prerequisites</span></span>
* <span data-ttu-id="6c3ad-108">**Azure 容器登錄庫** - 在 Azure 訂用帳戶中建立容器登錄庫。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="6c3ad-109">例如，使用 hello [Azure 入口網站](container-registry-get-started-portal.md)或 hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="6c3ad-110">**Docker CLI** -tooset Docker 主機和存取 hello Docker CLI 命令，在本機電腦上的安裝[Docker 引擎](https://docs.docker.com/engine/installation/)。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-tooa-registry"></a><span data-ttu-id="6c3ad-111">登入 tooa 登錄</span><span class="sxs-lookup"><span data-stu-id="6c3ad-111">Log in tooa registry</span></span>
<span data-ttu-id="6c3ad-112">執行`docker login`toolog tooyour 容器登錄中以在您[登錄認證](container-registry-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-112">Run `docker login` toolog in tooyour container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="6c3ad-113">hello 下列範例會傳遞 hello ID 和 Azure Active Directory 密碼[服務主體](../active-directory/active-directory-application-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-113">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="6c3ad-114">例如，您可能已指派服務主體 tooyour 登錄所需自動化案例。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-114">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="6c3ad-115">請確定 toospecify hello 完整的登錄名稱 （全部小寫）。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-115">Make sure toospecify hello fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="6c3ad-116">在此範例中為 `myregistry.azurecr.io`。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-toopull-and-push-an-image"></a><span data-ttu-id="6c3ad-117">步驟 toopull 並推送映像</span><span class="sxs-lookup"><span data-stu-id="6c3ad-117">Steps toopull and push an image</span></span>
<span data-ttu-id="6c3ad-118">hello，請遵循下載 hello Nginx 映像從公用 Docker Hub 登錄 hello，標記為私用 Azure 容器登錄中，將其發送 tooyour 登錄中，則會將其再次的範例。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-118">hello follow example downloads hello Nginx image from hello public Docker Hub registry, tags it for your private Azure container registry, pushes it tooyour registry, then pulls it again.</span></span>

<span data-ttu-id="6c3ad-119">**1.如 Nginx 提取 hello Docker 官方映像**</span><span class="sxs-lookup"><span data-stu-id="6c3ad-119">**1. Pull hello Docker official image for Nginx**</span></span>

<span data-ttu-id="6c3ad-120">第一次提取 hello 公用 Nginx 映像 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-120">First pull hello public Nginx image tooyour local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="6c3ad-121">**2.啟動 hello Nginx 容器**</span><span class="sxs-lookup"><span data-stu-id="6c3ad-121">**2. Start hello Nginx container**</span></span>

<span data-ttu-id="6c3ad-122">hello 下列命令會啟動本機 Nginx 容器 hello 以互動方式在連接埠 8080，可讓您從 Nginx toosee 輸出。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-122">hello following command starts hello local Nginx container interactively on port 8080, allowing you toosee output from Nginx.</span></span> <span data-ttu-id="6c3ad-123">它會移除 hello 執行一次停止容器。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-123">It removes hello running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="6c3ad-124">瀏覽過[http://localhost:8080/<](http://localhost:8080) tooview hello 執行容器。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-124">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span> <span data-ttu-id="6c3ad-125">您會看到下列其中一個螢幕類似 toohello。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-125">You see a screen similar toohello following one.</span></span>

![本機電腦上的 Nginx](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="6c3ad-127">toostop hello 執行的容器，請按 [CTRL] + [C]。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-127">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="6c3ad-128">**3.在登錄中建立 hello 映像的別名**</span><span class="sxs-lookup"><span data-stu-id="6c3ad-128">**3. Create an alias of hello image in your registry**</span></span>

<span data-ttu-id="6c3ad-129">hello 下列命令會建立別名 hello 影像的完整的路徑 tooyour 登錄。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-129">hello following command creates an alias of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="6c3ad-130">這個範例會指定 hello `samples` hello hello 登錄根目錄中的命名空間 tooavoid 雜亂。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-130">This example specifies hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="6c3ad-131">**4.推入 hello 映像 tooyour 登錄**</span><span class="sxs-lookup"><span data-stu-id="6c3ad-131">**4. Push hello image tooyour registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="6c3ad-132">**5.從登錄中提取 hello 映像**</span><span class="sxs-lookup"><span data-stu-id="6c3ad-132">**5. Pull hello image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="6c3ad-133">**6.從登錄啟動 hello Nginx 容器**</span><span class="sxs-lookup"><span data-stu-id="6c3ad-133">**6. Start hello Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="6c3ad-134">瀏覽過[http://localhost:8080/<](http://localhost:8080) tooview hello 執行容器。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-134">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span>

<span data-ttu-id="6c3ad-135">toostop hello 執行的容器，請按 [CTRL] + [C]。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-135">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="6c3ad-136">**7.（選擇性）移除 hello 映像**</span><span class="sxs-lookup"><span data-stu-id="6c3ad-136">**7. (Optional) Remove hello image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="6c3ad-137">並行限制</span><span class="sxs-lookup"><span data-stu-id="6c3ad-137">Concurrent Limits</span></span>
<span data-ttu-id="6c3ad-138">在某些情況下，同時執行呼叫可能會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="6c3ad-139">下表中的 hello 包含 hello 限制的並行呼叫上 Azure 容器登錄中的 「 發送 」 和 「 提取 」 作業：</span><span class="sxs-lookup"><span data-stu-id="6c3ad-139">hello following table contains hello limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="6c3ad-140">作業</span><span class="sxs-lookup"><span data-stu-id="6c3ad-140">Operation</span></span>  | <span data-ttu-id="6c3ad-141">限制</span><span class="sxs-lookup"><span data-stu-id="6c3ad-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="6c3ad-142">PULL</span><span class="sxs-lookup"><span data-stu-id="6c3ad-142">PULL</span></span>       | <span data-ttu-id="6c3ad-143">向上 too10 並行提取每個登錄</span><span class="sxs-lookup"><span data-stu-id="6c3ad-143">Up too10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="6c3ad-144">PUSH</span><span class="sxs-lookup"><span data-stu-id="6c3ad-144">PUSH</span></span>       | <span data-ttu-id="6c3ad-145">並行 too5 向上推播通知登錄每</span><span class="sxs-lookup"><span data-stu-id="6c3ad-145">Up too5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6c3ad-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c3ad-146">Next steps</span></span>
<span data-ttu-id="6c3ad-147">知道 hello 基本概念之後，您已經準備好使用您的登錄的 toostart ！</span><span class="sxs-lookup"><span data-stu-id="6c3ad-147">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="6c3ad-148">例如，啟動 部署容器映像 tooan [Azure 容器服務](https://azure.microsoft.com/documentation/services/container-service/)叢集。</span><span class="sxs-lookup"><span data-stu-id="6c3ad-148">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
