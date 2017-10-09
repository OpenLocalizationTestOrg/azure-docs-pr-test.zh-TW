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
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a>使用 Azure Container Instances 進行部署問題的疑難排解

本文將說明如何 tootroubleshoot 發出部署容器 tooAzure 容器執行個體時。 此外也說明某些 hello 您可能會碰到的常見問題。

## <a name="getting-diagnostic-events"></a>取得診斷事件

從您的應用程式程式碼的容器內的 tooview 記錄檔，您可以使用 hello [az 容器記錄](/cli/azure/container#logs)命令。 但如果您的容器未成功部署，您需要 hello Azure 容器執行個體的資源提供者所提供的 tooreview hello 診斷資訊。 您的容器，執行下列命令的 hello tooview hello 事件：

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

hello 輸出包含您的容器，以及部署事件 hello 核心屬性：

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

## <a name="common-deployment-issues"></a>常見部署問題

部署時所發生的大部分錯誤都可歸咎於幾個常見問題。

### <a name="unable-toopull-image"></a>無法 toopull 映像

如果 Azure 容器執行個體無法 toopull 映像一開始，重試最後失敗前段。 如果無法提取 hello 映像，則會顯示 hello 下列這類事件：

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

tooresolve，刪除 hello 容器，然後重試您的部署，您輸入 hello 映像名稱是正確的付費特別注意。

### <a name="container-continually-exits-and-restarts"></a>容器不斷結束又重新啟動

Azure Container Instances 目前僅支援長時間執行的服務。 如果您的容器執行 toocompletion，結束時，自動重新啟動並執行一次。 如果發生這種情況，系統會顯示如下所示的事件。 請注意該 hello 容器已成功啟動，然後再快速地重新啟動。 hello 容器執行個體 API 包含`retryCount`顯示多少次特定容器的屬性已重新啟動。

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
> 大部分的容器映像的 Linux 發行的設定殼層，（例如 bash），做為 hello 預設命令。 因為殼層本身不是長時間執行的服務，因此這些容器會立即結束並落入重新啟動迴圈。

### <a name="container-takes-a-long-time-toostart"></a>容器會很長的時間 toostart

如果您的容器會很長的時間 toostart，但最後順利完成，則會先來看看 hello 容器映像的大小。 因為 Azure 容器執行個體視提取您的容器映像，您會遇到的 hello 啟動時間是直接相關的 tooits 大小。

您可以檢視您的容器映像使用 Docker CLI hello hello 大小：

```bash
docker images
```

輸出：

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

hello 小的索引鍵 tookeeping 映像大小確保您的最終映像不包含任何項目就不需要在執行階段。 這是使用其中一種方式 toodo[多階段組建](https://docs.docker.com/engine/userguide/eng-image/multistage-build/)。 多階段組建讓您輕鬆 tooensure hello 最終映像包含您需要應用程式的唯一 hello 成品，以及此內容不是任何額外的 hello 時必要的建置時間。

hello 其他方式 tooreduce hello 的影響 hello 映像提取您的容器啟動時間是 toohost hello 容器映像使用 hello Azure 容器登錄中 hello 相同，但您想 toouse Azure 容器執行個體的區域。 這會縮短 hello hello 容器映像需求 tootravel 大幅縮短 hello 下載時間的網路路徑。
