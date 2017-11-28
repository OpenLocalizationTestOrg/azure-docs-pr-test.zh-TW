---
title: "針對 Azure Container Instances 進行疑難排解"
description: "了解如何使用 Azure Container Instances 進行問題的疑難排解"
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
ms.openlocfilehash: 86fa4b7dca7c362f95c0243a33f03d1f2dd3ab42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a><span data-ttu-id="b8fe5-103">使用 Azure Container Instances 進行部署問題的疑難排解</span><span class="sxs-lookup"><span data-stu-id="b8fe5-103">Troubleshoot deployment issues with Azure Container Instances</span></span>

<span data-ttu-id="b8fe5-104">本文說明如何在將容器部署至 Azure Container Instances 時進行問題的疑難排解。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-104">This article shows how to troubleshoot issues when deploying containers to Azure Container Instances.</span></span> <span data-ttu-id="b8fe5-105">此外，也會說明一些您可能會碰到的常見問題。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-105">It also describes some of the common issues you may run into.</span></span>

## <a name="getting-diagnostic-events"></a><span data-ttu-id="b8fe5-106">取得診斷事件</span><span class="sxs-lookup"><span data-stu-id="b8fe5-106">Getting diagnostic events</span></span>

<span data-ttu-id="b8fe5-107">若要在容器內檢視應用程式程式碼中的記錄，您可以使用 [az container logs](/cli/azure/container#logs) 命令。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-107">To view logs from your application code within a container, you can use the [az container logs](/cli/azure/container#logs) command.</span></span> <span data-ttu-id="b8fe5-108">但如果容器的部署並未成功，您就需要檢閱由 Azure Container Instances 資源提供者所提供的診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-108">But if your container does not deploy successfully, you need to review the diagnostic information provided by the Azure Container Instances resource provider.</span></span> <span data-ttu-id="b8fe5-109">若要檢視容器的事件，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="b8fe5-109">To view the events for your container, run the following command:</span></span>

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

<span data-ttu-id="b8fe5-110">輸出中會包含容器的核心屬性以及部署事件：</span><span class="sxs-lookup"><span data-stu-id="b8fe5-110">The output includes the core properties of your container, along with deployment events:</span></span>

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

## <a name="common-deployment-issues"></a><span data-ttu-id="b8fe5-111">常見部署問題</span><span class="sxs-lookup"><span data-stu-id="b8fe5-111">Common deployment issues</span></span>

<span data-ttu-id="b8fe5-112">部署時所發生的大部分錯誤都可歸咎於幾個常見問題。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-112">There are a few common issues that account for most errors in deployment.</span></span>

### <a name="unable-to-pull-image"></a><span data-ttu-id="b8fe5-113">無法提取映像</span><span class="sxs-lookup"><span data-stu-id="b8fe5-113">Unable to pull image</span></span>

<span data-ttu-id="b8fe5-114">如果 Azure Container Instances 一開始無法提取您的映像，它會先重試一段時間，最後才會失敗。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-114">If Azure Container Instances is unable to pull your image initially, it retries for some period before eventually failing.</span></span> <span data-ttu-id="b8fe5-115">如果它無法提取映像，系統便會顯示如下所示的事件：</span><span class="sxs-lookup"><span data-stu-id="b8fe5-115">If the image cannot be pulled, events like the following are shown:</span></span>

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
    "message": "Failed: Failed to pull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
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

<span data-ttu-id="b8fe5-116">若要解決，請刪除容器並重試部署，特別注意您所輸入的映像名稱是否正確。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-116">To resolve, delete the container and retry your deployment, paying close attention that you have typed the image name correctly.</span></span>

### <a name="container-continually-exits-and-restarts"></a><span data-ttu-id="b8fe5-117">容器不斷結束又重新啟動</span><span class="sxs-lookup"><span data-stu-id="b8fe5-117">Container continually exits and restarts</span></span>

<span data-ttu-id="b8fe5-118">Azure Container Instances 目前僅支援長時間執行的服務。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-118">Currently, Azure Container Instances only supports long-running services.</span></span> <span data-ttu-id="b8fe5-119">如果您的容器執行完畢並結束，該容器會自動重新啟動並再次執行。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-119">If your container runs to completion and exits, it automatically restarts and runs again.</span></span> <span data-ttu-id="b8fe5-120">如果發生這種情況，系統會顯示如下所示的事件。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-120">If this happens, events like those following are shown.</span></span> <span data-ttu-id="b8fe5-121">請注意，容器會在成功啟動後又迅速重新啟動。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-121">Note that the container successfully starts, then quickly restarts.</span></span> <span data-ttu-id="b8fe5-122">Container Instances API 會包含 `retryCount` 屬性，以顯示特定容器的重新啟動次數。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-122">The Container Instances API includes a `retryCount` property that shows how many times a particular container has restarted.</span></span>

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
> <span data-ttu-id="b8fe5-123">Linux 散發套件的大部分容器映像都會設定殼層 (例如 bash) 來作為預設命令。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-123">Most container images for Linux distributions set a shell, such as bash, as the default command.</span></span> <span data-ttu-id="b8fe5-124">因為殼層本身不是長時間執行的服務，因此這些容器會立即結束並落入重新啟動迴圈。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-124">Since a shell on its own is not a long-running service, these containers immediately exit and fall into a restart loop.</span></span>

### <a name="container-takes-a-long-time-to-start"></a><span data-ttu-id="b8fe5-125">容器要等很久才會啟動</span><span class="sxs-lookup"><span data-stu-id="b8fe5-125">Container takes a long time to start</span></span>

<span data-ttu-id="b8fe5-126">如果您的容器要等很久才會啟動，但最終還是會啟動成功，請先看看您的容器映像大小。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-126">If your container takes a long time to start, but eventually succeeds, start by looking at the size of your container image.</span></span> <span data-ttu-id="b8fe5-127">因為 Azure Container Instances 會視需要來提取您的容器映像，因此啟動時間的長短會與其大小直接相關。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-127">Because Azure Container Instances pulls your container image on demand, the startup time you experience is directly related to its size.</span></span>

<span data-ttu-id="b8fe5-128">您可以使用 Docker CLI 來檢視容器映像大小：</span><span class="sxs-lookup"><span data-stu-id="b8fe5-128">You can view the size of your container image using the Docker CLI:</span></span>

```bash
docker images
```

<span data-ttu-id="b8fe5-129">輸出：</span><span class="sxs-lookup"><span data-stu-id="b8fe5-129">Output:</span></span>

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

<span data-ttu-id="b8fe5-130">讓映像不會變得太大的關鍵在於，確保最終的映像不會包含執行階段所不需要的任何項目。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-130">The key to keeping image sizes small is ensuring that your final image does not contain anything that is not required at runtime.</span></span> <span data-ttu-id="b8fe5-131">若要做到這一點，有一種方式是使用[多階段建置](https://docs.docker.com/engine/userguide/eng-image/multistage-build/)。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-131">One way to do this is with [multi-stage builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span></span> <span data-ttu-id="b8fe5-132">多階段建置可讓您輕鬆地確保最終映像只包含應用程式所需的構件，而不會包含建置階段所需的任何額外內容。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-132">Multi-stage builds make it easy to ensure that the final image contains only the artifacts you need for your application, and not any of the extra content that was required at build time.</span></span>

<span data-ttu-id="b8fe5-133">另一種可在容器啟動階段降低對於映像提取作業影響的方式，是在您想要使用 Azure Container Instances 的相同區域中，使用 Azure Container Registry 來裝載容器映像。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-133">The other way to reduce the impact of the image pull on your container's startup time is to host the container image using the Azure Container Registry in the same region where you intend to use Azure Container Instances.</span></span> <span data-ttu-id="b8fe5-134">這種方式會縮短容器映像需要經過的網路路徑，從而大幅縮短下載時間。</span><span class="sxs-lookup"><span data-stu-id="b8fe5-134">This shortens the network path that the container image needs to travel, significantly shortening the download time.</span></span>