---
title: "aaaAzure 容器執行個體的教學課程-準備您的應用程式 |Azure 文件"
description: "準備部署 tooAzure 容器執行個體的應用程式"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a>建立部署 tooAzure 容器執行個體的容器

Azure Container Instances 能夠將 Docker 容器部署至 Azure 基礎結構，而不需要佈建任何虛擬機器，或採用較高層級的任何服務。 在本教學課程中，您將以 Node.js 建置簡單的 Web 應用程式，然後封裝在可使用 Azure Container Instances 來執行的容器中。 我們將討論：

> [!div class="checklist"]
> * 從 GitHub 複製應用程式來源  
> * 從應用程式來源建立容器映像
> * 在本機的 Docker 環境中測試 hello 映像

在後續教學課程中，您將上傳您的映像 tooan Azure 容器登錄中，然後再部署它們 tooAzure 容器執行個體。

## <a name="before-you-begin"></a>開始之前

本教學課程假設使用者對核心 Docker 概念有基本認識，例如容器、容器映像和基本 Docker 命令。 如有需要，請參閱[開始使用 Docker]( https://docs.docker.com/get-started/)以取得容器基本概念入門。 

toocomplete 本教學課程中，您需要 Docker 開發環境。 Docker 提供可輕鬆在 [Mac](https://docs.docker.com/docker-for-mac/)、[Windows](https://docs.docker.com/docker-for-windows/) 或 [Linux](https://docs.docker.com/engine/installation/#supported-platforms) 系統上設定 Docker 的套件。

## <a name="get-application-code"></a>取得應用程式程式碼

在此教學課程中的 hello 範例包含簡單的 web 應用程式內建[Node.js](http://nodejs.org)。 hello 應用程式是靜態的 HTML 網頁，並看起來像這樣：

![在瀏覽器中顯示的教學課程應用程式][aci-tutorial-app]

使用 git toodownload hello 範例：

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a>建立 hello 容器映像

hello hello 範例儲存機制中提供的 Dockerfile 顯示 hello 容器的建立方式。 它會從開始[官方 Node.js 映像][ dockerhub-nodeimage]根據[Alpine Linux](https://alpinelinux.org/)，是很適合的 toouse 與容器的小型分佈。 接著將 hello 應用程式檔案複製到 hello 容器，會安裝相依性使用 hello Node 封裝管理員，而且最後會開始 hello 應用程式。

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

使用 hello`docker build`命令 toocreate hello 容器映像，標記成*aci 教學課程應用*:

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

使用 hello `docker images` toosee hello 建置映像：

```bash
docker images
```

輸出：

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a>在本機執行 hello 容器

您嘗試部署 hello 容器 tooAzure 容器執行個體之前，本機執行 tooconfirm 正常運作。 hello`-d`參數讓 hello 容器 hello 背景中執行時`-p`可讓您 toomap 您計算 tooport 80 hello 容器中的任意連接埠。

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

Hello 容器開啟 hello 瀏覽器 toohttp://localhost:8080 tooconfirm 正在執行。

![Hello 瀏覽器中的本機執行 hello 應用程式][aci-tutorial-app-local]

## <a name="next-steps"></a>後續步驟

在此教學課程中，您可以建立容器映像可以部署的 tooAzure 容器執行個體。 已完成下列步驟的 hello:

> [!div class="checklist"]
> * 從 GitHub 複製 hello 應用程式來源  
> * 從應用程式來源建立容器映像
> * 在本機測試 hello 容器

前進 toohello 下一個教學課程的 toolearn 有關在 Azure 容器登錄中儲存容器映像。

> [!div class="nextstepaction"]
> [推入映像 tooAzure 容器登錄中](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png