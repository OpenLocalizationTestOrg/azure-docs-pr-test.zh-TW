---
title: "aaaAzure 容器服務教學課程-準備應用程式 |Microsoft 文件"
description: "Azure Container Service 教學課程 - 準備應用程式"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 容器, 微服務, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b537ecc9ff50358fb65b128bfe6eb894dd088cc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-images-toobe-used-with-azure-container-service"></a>建立容器映像 toobe 搭配 Azure 容器服務

在本教學課程 (七個章節的第一部分) 中，多容器應用程式已準備好用於 Kubernetes。 完成的步驟包括：  

> [!div class="checklist"]
> * 從 GitHub 複製應用程式來源  
> * 從 hello 應用程式來源中建立的容器映像
> * 在本機的 Docker 環境中測試 hello 應用程式

一旦完成，hello 下列應用程式是在本機開發環境中存取。

![Azure 上 Kubernetes 叢集的影像](media/container-service-kubernetes-tutorials/azure-vote.png)

在後續的教學課程，hello 容器映像已上傳的 tooan Azure 容器登錄中，而然後在 Azure 中的執行裝載 Kubernetes 叢集。

## <a name="before-you-begin"></a>開始之前

本教學課程假設使用者對核心 Docker 概念有基本認識，例如容器、容器映像和基本 Docker 命令。 如有需要，請參閱[開始使用 Docker]( https://docs.docker.com/get-started/)以取得容器基本概念入門。 

toocomplete 本教學課程中，您需要 Docker 開發環境。 Docker 提供可輕鬆在 [Mac](https://docs.docker.com/docker-for-mac/)、[Windows](https://docs.docker.com/docker-for-windows/) 或 [Linux](https://docs.docker.com/engine/installation/#supported-platforms) 系統上設定 Docker 的套件。

## <a name="get-application-code"></a>取得應用程式程式碼

在本教學課程中使用的 hello 範例應用程式是基本的投票應用程式。 hello 應用程式是由 web 前端元件及後端 Redis 執行個體所組成。 hello web 元件封裝成自訂容器映像。 hello Redis 執行個體使用的未修改的映像從 Docker Hub。  

使用 git toodownload hello 應用程式 tooyour 開發環境的複本。

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

內部 hello 複製的目錄 hello 應用程式的原始程式碼，預先建立的 Docker compose 檔和 Kubernetes 資訊清單檔案。 這些檔案是使用的 toocreate 資產到 hello 教學課程集。 

## <a name="create-container-images"></a>建立容器映像

[Docker 撰寫](https://docs.docker.com/compose/)可以是使用 tooautomate hello 建置現成可用的容器映像和 hello 多容器應用程式部署。

執行 hello docker compose.yml 檔案 toocreate hello 容器映像，下載 hello Redis 映像，並啟動 hello 應用程式。

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

完成時，使用 hello [docker 映像](https://docs.docker.com/engine/reference/commandline/images/)命令 toosee hello 建立映像。

```bash
docker images
```

請注意，已下載或建立三個映像。 hello *azure 投票前*映像包含 hello 應用程式。 它衍生自 hello *nginx 酒瓶*映像。 從 Docker Hub 下載 hello Redis 映像。

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

執行 hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/)命令 toosee hello 執行中的容器。

```bash
docker ps
```

輸出：

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a>在本機測試應用程式

瀏覽 toohttp://localhost:8080 toosee hello 執行應用程式。

![Azure 上 Kubernetes 叢集的影像](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a>清除資源

既然已經驗證應用程式的功能，就可以停止並移除 hello 執行中的容器。 請勿刪除 hello 容器映像。 hello *azure 投票前*映像處於 hello 下一個教學課程的上傳的 tooan Azure 容器登錄中的執行個體。

執行下列 toostop hello 執行容器的 hello。

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

使用下列命令的 hello 來刪除 hello 停止容器。

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

在完成時，您必須包含 hello Azure 投票應用程式的容器映像。

## <a name="next-steps"></a>後續步驟

在本教學課程中，應用程式已通過測試，且容器映像建立 hello 應用程式。 已完成下列步驟的 hello:

> [!div class="checklist"]
> * 從 GitHub 複製 hello 應用程式來源  
> * 已從應用程式來源建立容器映像
> * 在本機的 Docker 環境中測試的 hello 應用程式

前進 toohello 下一個教學課程的 toolearn 有關在 Azure 容器登錄中儲存容器映像。

> [!div class="nextstepaction"]
> [推入映像 tooAzure 容器登錄中](./container-service-tutorial-kubernetes-prepare-acr.md)
