---
title: "aaaAzure 容器登錄 webhook |Microsoft 文件"
description: Azure Container Registry Webhook
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: "Docker、容器、ACR"
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a><span data-ttu-id="8f347-104">使用 Azure Container Registry Webhook - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8f347-104">Using Azure Container Registry webhooks - Azure portal</span></span>

<span data-ttu-id="8f347-105">Azure 容器登錄中儲存並管理私人 Docker 容器映像，Docker Hub 儲存公用 Docker 映像的類似 toohello 方式。</span><span class="sxs-lookup"><span data-stu-id="8f347-105">An Azure container registry stores and manages private Docker container images, similar toohello way Docker Hub stores public Docker images.</span></span> <span data-ttu-id="8f347-106">您使用 webhook tootrigger 事件時，會發生在您登錄儲存機制的其中一個特定動作。</span><span class="sxs-lookup"><span data-stu-id="8f347-106">You use webhooks tootrigger events when certain actions take place in one of your registry repositories.</span></span> <span data-ttu-id="8f347-107">Webhook 可以回應 hello 登錄層級 tooevents 或向下 tooa 特定儲存機制標記範圍內。</span><span class="sxs-lookup"><span data-stu-id="8f347-107">Webhooks can respond tooevents at hello registry level or they can be scoped down tooa specific repository tag.</span></span> 

<span data-ttu-id="8f347-108">如需背景和概念，請參閱 hello[概觀](./container-registry-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="8f347-108">For more background and concepts, see hello [overview](./container-registry-intro.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f347-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="8f347-109">Prerequisites</span></span> 

- <span data-ttu-id="8f347-110">Azure 容器管理的登錄 - 在 Azure 訂用帳戶中建立受管理的容器登錄。</span><span class="sxs-lookup"><span data-stu-id="8f347-110">Azure container managed registry - Create a managed container registry in your Azure subscription.</span></span> <span data-ttu-id="8f347-111">例如，使用 hello Azure 入口網站或 hello Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="8f347-111">For example, use hello Azure portal or hello Azure CLI 2.0.</span></span> 
- <span data-ttu-id="8f347-112">Docker CLI-tooset Docker 主機和存取 hello Docker CLI 命令，在本機電腦上安裝 Docker 引擎。</span><span class="sxs-lookup"><span data-stu-id="8f347-112">Docker CLI - tooset up your local computer as a Docker host and access hello Docker CLI commands, install Docker Engine.</span></span> 

## <a name="create-webhook-azure-portal"></a><span data-ttu-id="8f347-113">建立 Webhook Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8f347-113">Create webhook Azure portal</span></span>

1. <span data-ttu-id="8f347-114">登入 toohello Azure 入口網站，並瀏覽您想在其中 toocreate webhook toohello 登錄。</span><span class="sxs-lookup"><span data-stu-id="8f347-114">Log in toohello Azure portal and navigate toohello registry in which you want toocreate webhooks.</span></span> 

2. <span data-ttu-id="8f347-115">在 hello 容器刀鋒視窗中，選取 hello"Webhook 」 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8f347-115">In hello container blade, select hello "Webhooks" tab.</span></span> 

3. <span data-ttu-id="8f347-116">從 hello webhook 刀鋒視窗工具列中選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="8f347-116">Select "Add" from hello webhook blade toolbar.</span></span> 

4. <span data-ttu-id="8f347-117">完整的 hello*建立 Webhook*表單以 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="8f347-117">Complete hello *Create Webhook* form with hello following information:</span></span>

| <span data-ttu-id="8f347-118">值</span><span class="sxs-lookup"><span data-stu-id="8f347-118">Value</span></span> | <span data-ttu-id="8f347-119">描述</span><span class="sxs-lookup"><span data-stu-id="8f347-119">Description</span></span> |
|---|---|
| <span data-ttu-id="8f347-120">名稱</span><span class="sxs-lookup"><span data-stu-id="8f347-120">Name</span></span> | <span data-ttu-id="8f347-121">您想要 toogive toohello webhook hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="8f347-121">hello name you want toogive toohello webhook.</span></span> <span data-ttu-id="8f347-122">它只能包含小寫字母和數字，且必須為 5-50 個字元之間。</span><span class="sxs-lookup"><span data-stu-id="8f347-122">It can only contain lowercase letters and numbers and between 5-50 characters.</span></span> |
| <span data-ttu-id="8f347-123">服務 URI</span><span class="sxs-lookup"><span data-stu-id="8f347-123">Service URI</span></span> | <span data-ttu-id="8f347-124">hello hello webhook 傳送通知 POST 的位置的 URI。</span><span class="sxs-lookup"><span data-stu-id="8f347-124">hello URI where hello webhook should send POST notifications.</span></span> |
| <span data-ttu-id="8f347-125">自訂標頭</span><span class="sxs-lookup"><span data-stu-id="8f347-125">Custom headers</span></span> | <span data-ttu-id="8f347-126">您想要 toopass 以及 hello POST 要求標頭。</span><span class="sxs-lookup"><span data-stu-id="8f347-126">Headers you want toopass along with hello POST request.</span></span> <span data-ttu-id="8f347-127">它們應該為「金鑰：值」的格式。</span><span class="sxs-lookup"><span data-stu-id="8f347-127">They should be in "key: value" format.</span></span> |
| <span data-ttu-id="8f347-128">觸發程序動作</span><span class="sxs-lookup"><span data-stu-id="8f347-128">Trigger actions</span></span> | <span data-ttu-id="8f347-129">Hello webhook 觸發程序的動作。</span><span class="sxs-lookup"><span data-stu-id="8f347-129">Actions that trigger hello webhook.</span></span> <span data-ttu-id="8f347-130">目前 webhook 可藉由推入及/或刪除動作 tooan 映像。</span><span class="sxs-lookup"><span data-stu-id="8f347-130">Currently webhooks can be triggered by push and/or delete actions tooan image.</span></span> |
| <span data-ttu-id="8f347-131">狀態</span><span class="sxs-lookup"><span data-stu-id="8f347-131">Status</span></span> | <span data-ttu-id="8f347-132">hello hello webhook 建立之後的狀態。</span><span class="sxs-lookup"><span data-stu-id="8f347-132">hello status for hello webhook after it's created.</span></span> <span data-ttu-id="8f347-133">此選項預設為啟用狀態。</span><span class="sxs-lookup"><span data-stu-id="8f347-133">It's enabled by default.</span></span> |
| <span data-ttu-id="8f347-134">Scope</span><span class="sxs-lookup"><span data-stu-id="8f347-134">Scope</span></span> | <span data-ttu-id="8f347-135">於哪一個 hello webhook works hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="8f347-135">hello scope at which hello webhook works.</span></span> <span data-ttu-id="8f347-136">根據預設 hello 範圍是 hello 登錄中的所有事件。</span><span class="sxs-lookup"><span data-stu-id="8f347-136">By default hello scope is for all events in hello registry.</span></span> <span data-ttu-id="8f347-137">可以針對儲存機制或標記中指定使用 hello 格式"儲存機制： 標記 」。</span><span class="sxs-lookup"><span data-stu-id="8f347-137">It can be specified for a repository or a tag by using hello format "repository: tag".</span></span> |

<span data-ttu-id="8f347-138">範例 Webhook 表單：</span><span class="sxs-lookup"><span data-stu-id="8f347-138">Example webhook form:</span></span>

![DCOS UI](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a><span data-ttu-id="8f347-140">建立 Webhook Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8f347-140">Create webhook Azure CLI</span></span>

<span data-ttu-id="8f347-141">webhook 使用 toocreate hello Azure CLI，使用 hello [az acr webhook 建立](/cli/azure/acr/webhook#create)命令。</span><span class="sxs-lookup"><span data-stu-id="8f347-141">toocreate a webhook using hello Azure CLI, use hello [az acr webhook create](/cli/azure/acr/webhook#create) command.</span></span>

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a><span data-ttu-id="8f347-142">測試 Webhook</span><span class="sxs-lookup"><span data-stu-id="8f347-142">Test webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="8f347-143">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8f347-143">Azure portal</span></span>

<span data-ttu-id="8f347-144">在容器上的先前 toousing hello webhook 發送的映像，刪除動作，可以測試使用 hello **Ping**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8f347-144">Prior toousing hello webhook on container image push and delete actions, it can be tested using hello **Ping** button.</span></span> <span data-ttu-id="8f347-145">使用時，會傳送一般 post 要求 toohello 指定端點與記錄檔 hello 回應 hello Ping。</span><span class="sxs-lookup"><span data-stu-id="8f347-145">When used, hello Ping sends a generic post request toohello specified endpoint and logs hello response.</span></span> <span data-ttu-id="8f347-146">這是很有幫助 hello webhook 的 tooverify 是否已正確設定。</span><span class="sxs-lookup"><span data-stu-id="8f347-146">This is helpful tooverify that hello webhook has been set up correctly.</span></span>

1. <span data-ttu-id="8f347-147">選取您想要 tootest hello webhook。</span><span class="sxs-lookup"><span data-stu-id="8f347-147">Select hello webhook you want tootest.</span></span> 
2. <span data-ttu-id="8f347-148">在 hello 頂端的工具列上，選取 hello"Ping"動作。</span><span class="sxs-lookup"><span data-stu-id="8f347-148">In hello top toolbar, select hello "Ping" action.</span></span> 
3. <span data-ttu-id="8f347-149">請檢查 hello 要求和回應。</span><span class="sxs-lookup"><span data-stu-id="8f347-149">Check hello request and response.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="8f347-150">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8f347-150">Azure CLI</span></span>

<span data-ttu-id="8f347-151">tootest 以 hello Azure CLI ACR webhook 使用 hello [az acr webhook ping](/cli/azure/acr/webhook#ping)命令。</span><span class="sxs-lookup"><span data-stu-id="8f347-151">tootest an ACR webhook with hello Azure CLI, use hello [az acr webhook ping](/cli/azure/acr/webhook#ping) command.</span></span>

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

<span data-ttu-id="8f347-152">toosee hello 結果，請使用 hello [az acr webhook 清單事件](/cli/azure/acr/webhook#list-events)命令。</span><span class="sxs-lookup"><span data-stu-id="8f347-152">toosee hello results, use hello [az acr webhook list-events](/cli/azure/acr/webhook#list-events) command.</span></span> 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a><span data-ttu-id="8f347-153">刪除 Webhook</span><span class="sxs-lookup"><span data-stu-id="8f347-153">Delete webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="8f347-154">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8f347-154">Azure portal</span></span>

<span data-ttu-id="8f347-155">可以藉由選取 hello webhook hello hello Azure 入口網站上的刪除按鈕來刪除每個 webhook。</span><span class="sxs-lookup"><span data-stu-id="8f347-155">Each webhook can be deleted by selecting hello webhook and then hello delete button on hello Azure portal.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="8f347-156">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8f347-156">Azure CLI</span></span>

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```