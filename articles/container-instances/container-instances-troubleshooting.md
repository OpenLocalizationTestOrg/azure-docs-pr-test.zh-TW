---
title: "aaaTroubleshooting Azure 容器執行個體"
description: "了解如何 tootroubleshoot 問題 Azure 容器執行個體"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/03/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: dfec636a0a174c74a6f2e9d9c4da6e871f8d2fda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a><span data-ttu-id="97375-103">使用 Azure Container Instances 進行部署問題的疑難排解</span><span class="sxs-lookup"><span data-stu-id="97375-103">Troubleshoot deployment issues with Azure Container Instances</span></span>

<span data-ttu-id="97375-104">本文將說明如何 tootroubleshoot 發出部署容器 tooAzure 容器執行個體時。</span><span class="sxs-lookup"><span data-stu-id="97375-104">This article shows how tootroubleshoot issues when deploying containers tooAzure Container Instances.</span></span> <span data-ttu-id="97375-105">此外也說明某些 hello 您可能會碰到的常見問題。</span><span class="sxs-lookup"><span data-stu-id="97375-105">It also describes some of hello common issues you may run into.</span></span>

## <a name="getting-diagnostic-events"></a><span data-ttu-id="97375-106">取得診斷事件</span><span class="sxs-lookup"><span data-stu-id="97375-106">Getting diagnostic events</span></span>

<span data-ttu-id="97375-107">從您的應用程式程式碼的容器內的 tooview 記錄檔，您可以使用 hello [az 容器記錄](/cli/azure/container#logs)命令。</span><span class="sxs-lookup"><span data-stu-id="97375-107">tooview logs from your application code within a container, you can use hello [az container logs](/cli/azure/container#logs) command.</span></span> <span data-ttu-id="97375-108">但如果您的容器未成功部署，您需要 hello Azure 容器執行個體的資源提供者所提供的 tooreview hello 診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="97375-108">But if your container does not deploy successfully, you need tooreview hello diagnostic information provided by hello Azure Container Instances resource provider.</span></span> <span data-ttu-id="97375-109">您的容器，執行下列命令的 hello tooview hello 事件：</span><span class="sxs-lookup"><span data-stu-id="97375-109">tooview hello events for your container, run hello following command:</span></span>

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

<span data-ttu-id="97375-110">hello 輸出包含您的容器，以及部署事件 hello 核心屬性：</span><span class="sxs-lookup"><span data-stu-id="97375-110">hello output includes hello core properties of your container, along with deployment events:</span></span>

```bash
{
  "containers": [
    {
      "command": null,
      "environmentVariables": [],
      "image": "microsoft/aci-helloworld",
      ...

      "events": [
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:52+00:00",
        "lastTimestamp": "2017-08-03T22:12:52+00:00",
        "message": "Pulling: pulling image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Pulled: Successfully pulled image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Created: Created container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Started: Started container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      }
    ],
    "name": "helloworld",
      "ports": [
        {
          "port": 80
        }
      ],
    ...
  ]
}
```

## <a name="common-deployment-issues"></a><span data-ttu-id="97375-111">常見部署問題</span><span class="sxs-lookup"><span data-stu-id="97375-111">Common deployment issues</span></span>

<span data-ttu-id="97375-112">部署時所發生的大部分錯誤都可歸咎於幾個常見問題。</span><span class="sxs-lookup"><span data-stu-id="97375-112">There are a few common issues that account for most errors in deployment.</span></span>

### <a name="unable-toopull-image"></a><span data-ttu-id="97375-113">無法 toopull 映像</span><span class="sxs-lookup"><span data-stu-id="97375-113">Unable toopull image</span></span>

<span data-ttu-id="97375-114">如果 Azure 容器執行個體無法 toopull 映像一開始，重試最後失敗前段。</span><span class="sxs-lookup"><span data-stu-id="97375-114">If Azure Container Instances is unable toopull your image initially, it retries for some period before eventually failing.</span></span> <span data-ttu-id="97375-115">如果無法提取 hello 映像，則會顯示 hello 下列這類事件：</span><span class="sxs-lookup"><span data-stu-id="97375-115">If hello image cannot be pulled, events like hello following are shown:</span></span>

```bash
"events": [
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:31+00:00",
    "lastTimestamp": "2017-08-03T22:19:31+00:00",
    "message": "Pulling: pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:32+00:00",
    "lastTimestamp": "2017-08-03T22:19:32+00:00",
    "message": "Failed: Failed toopull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:33+00:00",
    "lastTimestamp": "2017-08-03T22:19:33+00:00",
    "message": "BackOff: Back-off pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  }
]
```

<span data-ttu-id="97375-116">tooresolve，刪除 hello 容器，然後重試您的部署，您輸入 hello 映像名稱是正確的付費特別注意。</span><span class="sxs-lookup"><span data-stu-id="97375-116">tooresolve, delete hello container and retry your deployment, paying close attention that you have typed hello image name correctly.</span></span>

### <a name="container-continually-exits-and-restarts"></a><span data-ttu-id="97375-117">容器不斷結束又重新啟動</span><span class="sxs-lookup"><span data-stu-id="97375-117">Container continually exits and restarts</span></span>

<span data-ttu-id="97375-118">Azure Container Instances 目前僅支援長時間執行的服務。</span><span class="sxs-lookup"><span data-stu-id="97375-118">Currently, Azure Container Instances only supports long-running services.</span></span> <span data-ttu-id="97375-119">如果您的容器執行 toocompletion，結束時，自動重新啟動並執行一次。</span><span class="sxs-lookup"><span data-stu-id="97375-119">If your container runs toocompletion and exits, it automatically restarts and runs again.</span></span> <span data-ttu-id="97375-120">如果發生這種情況，系統會顯示如下所示的事件。</span><span class="sxs-lookup"><span data-stu-id="97375-120">If this happens, events like those following are shown.</span></span> <span data-ttu-id="97375-121">請注意該 hello 容器已成功啟動，然後再快速地重新啟動。</span><span class="sxs-lookup"><span data-stu-id="97375-121">Note that hello container successfully starts, then quickly restarts.</span></span> <span data-ttu-id="97375-122">hello 容器執行個體 API 包含`retryCount`顯示多少次特定容器的屬性已重新啟動。</span><span class="sxs-lookup"><span data-stu-id="97375-122">hello Container Instances API includes a `retryCount` property that shows how many times a particular container has restarted.</span></span>

```bash
"events": [
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:55+00:00",
    "lastTimestamp": "2017-08-03T22:23:22+00:00",
    "message": "Pulling: pulling image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:23:23+00:00",
    "message": "Pulled: Successfully pulled image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Created: Created container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Started: Started container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Created: Created container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Started: Started container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 13,
    "firstTimestamp": "2017-08-03T22:21:59+00:00",
    "lastTimestamp": "2017-08-03T22:24:36+00:00",
    "message": "BackOff: Back-off restarting failed container",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:22:13+00:00",
    "lastTimestamp": "2017-08-03T22:22:13+00:00",
    "message": "Created: Created container with id 72e347e891290e238135e4a6b3078748ca25a1275dbbff30d8d214f026d89220",
    "type": "Normal"
  },
  ...
```

> [!NOTE]
> <span data-ttu-id="97375-123">大部分的容器映像的 Linux 發行的設定殼層，（例如 bash），做為 hello 預設命令。</span><span class="sxs-lookup"><span data-stu-id="97375-123">Most container images for Linux distributions set a shell, such as bash, as hello default command.</span></span> <span data-ttu-id="97375-124">因為殼層本身不是長時間執行的服務，因此這些容器會立即結束並落入重新啟動迴圈。</span><span class="sxs-lookup"><span data-stu-id="97375-124">Since a shell on its own is not a long-running service, these containers immediately exit and fall into a restart loop.</span></span>

### <a name="container-takes-a-long-time-toostart"></a><span data-ttu-id="97375-125">容器會很長的時間 toostart</span><span class="sxs-lookup"><span data-stu-id="97375-125">Container takes a long time toostart</span></span>

<span data-ttu-id="97375-126">如果您的容器會很長的時間 toostart，但最後順利完成，則會先來看看 hello 容器映像的大小。</span><span class="sxs-lookup"><span data-stu-id="97375-126">If your container takes a long time toostart, but eventually succeeds, start by looking at hello size of your container image.</span></span> <span data-ttu-id="97375-127">因為 Azure 容器執行個體視提取您的容器映像，您會遇到的 hello 啟動時間是直接相關的 tooits 大小。</span><span class="sxs-lookup"><span data-stu-id="97375-127">Because Azure Container Instances pulls your container image on demand, hello startup time you experience is directly related tooits size.</span></span>

<span data-ttu-id="97375-128">您可以檢視您的容器映像使用 Docker CLI hello hello 大小：</span><span class="sxs-lookup"><span data-stu-id="97375-128">You can view hello size of your container image using hello Docker CLI:</span></span>

```bash
docker images
```

<span data-ttu-id="97375-129">輸出：</span><span class="sxs-lookup"><span data-stu-id="97375-129">Output:</span></span>

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

<span data-ttu-id="97375-130">hello 小的索引鍵 tookeeping 映像大小確保您的最終映像不包含任何項目就不需要在執行階段。</span><span class="sxs-lookup"><span data-stu-id="97375-130">hello key tookeeping image sizes small is ensuring that your final image does not contain anything that is not required at runtime.</span></span> <span data-ttu-id="97375-131">這是使用其中一種方式 toodo[多階段組建](https://docs.docker.com/engine/userguide/eng-image/multistage-build/)。</span><span class="sxs-lookup"><span data-stu-id="97375-131">One way toodo this is with [multi-stage builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span></span> <span data-ttu-id="97375-132">多階段組建讓您輕鬆 tooensure hello 最終映像包含您需要應用程式的唯一 hello 成品，以及此內容不是任何額外的 hello 時必要的建置時間。</span><span class="sxs-lookup"><span data-stu-id="97375-132">Multi-stage builds make it easy tooensure that hello final image contains only hello artifacts you need for your application, and not any of hello extra content that was required at build time.</span></span>

<span data-ttu-id="97375-133">hello 其他方式 tooreduce hello 的影響 hello 映像提取您的容器啟動時間是 toohost hello 容器映像使用 hello Azure 容器登錄中 hello 相同，但您想 toouse Azure 容器執行個體的區域。</span><span class="sxs-lookup"><span data-stu-id="97375-133">hello other way tooreduce hello impact of hello image pull on your container's startup time is toohost hello container image using hello Azure Container Registry in hello same region where you intend toouse Azure Container Instances.</span></span> <span data-ttu-id="97375-134">這會縮短 hello hello 容器映像需求 tootravel 大幅縮短 hello 下載時間的網路路徑。</span><span class="sxs-lookup"><span data-stu-id="97375-134">This shortens hello network path that hello container image needs tootravel, significantly shortening hello download time.</span></span>
