---
title: "Azure Container Registry 教學課程 - 準備異地複寫的 Azure Container Registry"
description: "建立 Azure Container Registry、設定異地複寫、準備 Docker 映像並將其部署至登錄。 三段式教學課程的第一段。"
services: container-registry
author: mmacy
manager: timlt
ms.service: container-registry
ms.topic: tutorial
ms.date: 10/26/2017
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: 7ae0fbf5f7566bd3f1f6591501b8b004a1e5cb0f
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="prepare-a-geo-replicated-azure-container-registry"></a>準備異地複寫的 Azure Container Registry

Azure Container Registry 是一種部署在 Azure 中的私人 Docker 登錄，可讓您將網路保持在靠近部署的位置。 在這三篇教學課程系列文章中，您可以了解如何使用異地複寫，將執行於 Linux 容器中的 ASP.NET Core Web 應用程式部署至兩個[用於容器的 Web 應用程式](../app-service/containers/index.yml)執行個體。 您會了解 Azure 如何從最近的異地複寫存放庫，將映像自動部署到每個 Web 應用程式執行個體。

本教學課程是下列三段式課程的第一段：

> [!div class="checklist"]
> * 建立異地複寫的 Azure Container Registry
> * 從 GitHub 複製應用程式原始程式碼
> * 從應用程式來源建置 Docker 容器映像
> * 將容器映像推送至登錄

在後續教學課程中，您會將容器從私人登錄部署至執行於兩個 Azure 區域的 Web 應用程式。 接著，您會更新應用程式中的程式碼，並使用單一 `docker push` 來更新登錄中的這兩個 Web 應用程式執行個體。

## <a name="before-you-begin"></a>開始之前

本教學課程需要您執行 Azure CLI 2.0.20 版或更新版本。 執行 `az --version` 以尋找版本。 如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。

本教學課程假設使用者對核心 Docker 概念有基本認識，例如容器、容器映像和基本 Docker 命令。 如有需要，請參閱[開始使用 Docker]( https://docs.docker.com/get-started/)以取得容器基本概念入門。

若要完成本教學課程，您需要 Docker 開發環境。 Docker 提供可輕鬆在 [Mac](https://docs.docker.com/docker-for-mac/)、[Windows](https://docs.docker.com/docker-for-windows/) 或 [Linux](https://docs.docker.com/engine/installation/#supported-platforms) 系統上設定 Docker 的套件。

Azure Cloud Shell 不包括完成本教學課程每個步驟所需的 Docker 元件。 因此，我們建議您本機安裝 Azure CLI 和 Docker 開發環境。

> [!IMPORTANT]
> Azure 容器登錄的異地複寫功能目前處於**預覽**。 若您同意[補充的使用規定](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)即可取得預覽。 在公開上市 (GA) 之前，此功能的某些領域可能會變更。
>

## <a name="create-a-container-registry"></a>建立容器登錄庫

登入 [Azure 入口網站](http://portal.azure.com)。

選取 [新增] > [容器] > [Azure Container Registry]。

![在 Azure 入口網站中建立容器登錄][tut-portal-01]

為新的登錄進行以下設定：

* **登錄名稱**：建立登錄名稱，其必須在 Azure 中全域唯一且包含 5-50 個英數字元
* **資源群組**：**建立新的** > `myResourceGroup`
* **位置**：`West US`
* **管理員使用者**：`Enable` (必要項目；可讓用於容器的 Web 應用程式提取映像)
* **SKU**：`Premium` (異地複寫的必要項目)

選取 [建立] 以部署 ACR 執行個體。

![在 Azure 入口網站中建立容器登錄][tut-portal-02]

在本教學課程的其餘部分，我們使用 `<acrName>` 作為您所選容器**登錄名稱**的預留位置。

> [!TIP]
> 由於 Azure Container Registry 通常是存留較久且跨多部容器主機使用的資源，因此建議您在專屬的資源群組中建立您的登錄。 當您設定異地複寫登錄和 Webhook 時，這些額外的資源會放置在相同的資源群組中。
>

## <a name="configure-geo-replication"></a>設定異地複寫

現在，您已經具備進階登錄，即可設定異地複寫。 這樣一來，您的 Web 應用程式即可從最近的登錄來提取其容器映像 (在下一個教學課程中，您會將 Web 應用程式設為在兩個區域中執行)。

在 Azure 入口網站中，巡覽至您的新容器登錄，並選取 [服務] 下方的 [複寫]：

![在 Azure 入口網站的容器登錄 UI 中進行複寫][tut-portal-03]

系統會顯示地圖，並以綠色六邊形代表適用於異地複寫的 Azure 區域：

 ![Azure 入口網站的區域圖][tut-map-01]

選取美國東部地區的綠色六邊形，然後選取 [建立複寫] 下方的 [建立]，將登錄複寫到美國東部地區：

 ![在 Azure 入口網站中建立複寫 UI][tut-portal-04]

完成複寫時，入口網站會將這兩個區域顯示為 [就緒]。 使用 [重新整理] 按鈕，以重新整理複寫的狀態；建立並同步處理複本可能需要一分鐘左右的時間。

![Azure 入口網站中的複寫狀態 UI][tut-portal-05]

## <a name="container-registry-login"></a>Container Registry 登入

現在，您已設定異地複寫、建置容器映像，並將它推送到您的登錄。 您必須先登入 ACR 執行個體，再將映像推送至該處。 使用[基本 SKU、標準 SKU 和進階 SKU](container-registry-skus.md)時，您可以使用 Azure 身分識別進行驗證。

使用 [az acr login](https://docs.microsoft.com/cli/azure/acr#az_acr_login) 命令，驗證並快取登錄的認證。 將 `<acrName>` 取代為您在上述步驟中建立的登錄名稱。

```azurecli
az acr login --name <acrName>
```

完成時，此命令會傳回 `Login Succeeded`。

## <a name="get-application-code"></a>取得應用程式程式碼

本教學課程的範例包含一個由 [ASP.NET Core](http://dot.net) 建置的小型 Web 應用程式。 該應用程式有一個 HTML 網頁，可顯示 Azure Container Registry 部署映像的來源區域。

![在瀏覽器中顯示的教學課程應用程式][tut-app-01]

使用 git 將此範例下載到本機目錄中，並將 `cd` 下載到目錄中：

```bash
git clone https://github.com/Azure-Samples/acr-helloworld.git
cd acr-helloworld
```

## <a name="update-dockerfile"></a>更新 Dockerfile

範例隨附的 Dockerfile 會示範如何建置容器。 此作業會先從官方 [aspnetcore](https://store.docker.com/community/images/microsoft/aspnetcore) 映像開始，將應用程式檔案複製到容器內、安裝相依性，再使用官方 [aspnetcore-build](https://store.docker.com/community/images/microsoft/aspnetcore-build) 映像編譯輸出，最後建置最佳化的 aspnetcore 映像。

Dockerfile 是位於複製來源中的 `./AcrHelloworld/Dockerfile`。

```dockerfile
FROM microsoft/aspnetcore:2.0 AS base
# Update <acrName> with the name of your registry
# Example: uniqueregistryname.azurecr.io
ENV DOCKER_REGISTRY <acrName>.azurecr.io
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY *.sln ./
COPY AcrHelloworld/AcrHelloworld.csproj AcrHelloworld/
RUN dotnet restore
COPY . .
WORKDIR /src/AcrHelloworld
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS production
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AcrHelloworld.dll"]
```

*acr-helloworld* 映像中的應用程式會查詢 DNS 以取得登錄的登入伺服器相關資訊，並嘗試判斷其容器的部署來源區域。 您必須在 Dockerfile 的 `DOCKER_REGISTRY` 環境變數中，指定登錄的登入伺服器 URL。

首先，使用 `az acr show` 命令取得登錄的登入伺服器 URL。 將 `<acrName>` 取代為您在上述步驟中建立的登錄名稱。

```azurecli
az acr show --name <acrName> --query "{acrLoginServer:loginServer}" --output table
```

輸出：

```bash
AcrLoginServer
-----------------------------
uniqueregistryname.azurecr.io
```

接下來，使用登錄的登入伺服器 URL 更新 `DOCKER_REGISTRY` 這一行。 在此範例中，我們會將這一行更新為顯示範例登錄名稱 *uniqueregistryname*：

```dockerfile
ENV DOCKER_REGISTRY uniqueregistryname.azurecr.io
```

## <a name="build-container-image"></a>建置容器映像

現在，您已使用登錄 URL 更新 Dockerfile，即可使用 `docker build` 建立容器映像。 執行下列命令以建置映像，然後使用私人登錄 URL 加以標記，同樣將 `<acrName>` 取代為您的登錄名稱：

```bash
docker build . -f ./AcrHelloworld/Dockerfile -t <acrName>.azurecr.io/acr-helloworld:v1
```

建置好 Docker 映像時，會顯示幾行輸出 (以下顯示截斷的輸出)：

```bash
Sending build context to Docker daemon  523.8kB
Step 1/18 : FROM microsoft/aspnetcore:2.0 AS base
2.0: Pulling from microsoft/aspnetcore
3e17c6eae66c: Pulling fs layer
...
Step 18/18 : ENTRYPOINT dotnet AcrHelloworld.dll
 ---> Running in 6906d98c47a1
 ---> c9ca1763cfb1
Removing intermediate container 6906d98c47a1
Successfully built c9ca1763cfb1
Successfully tagged uniqueregistryname.azurecr.io/acr-helloworld:v1
```

使用 `docker images` 命令查看已建置的映像：

```bash
docker images
```

輸出：

```bash
REPOSITORY                                      TAG    IMAGE ID        CREATED               SIZE
uniqueregistryname.azurecr.io/acr-helloworld    v1     01ac48d5c8cf    About a minute ago    284MB
...
```

## <a name="push-image-to-azure-container-registry"></a>將映像推送至 Azure Container Registry

最後，使用 `docker push` 命令，將 *acr-helloworld* 映像推送至您的登錄。 將 `<acrName>` 取代為您的登錄名稱。

```bash
docker push <acrName>.azurecr.io/acr-helloworld:v1
```

由於您已將登錄設定為要進行異地複寫，因此系統會使用單一 `docker push` 命令，將您的映像自動複寫至「美國西部」和「美國東部」地區。

輸出：

```bash
The push refers to a repository [uniqueregistryname.azurecr.io/acr-helloworld]
cd54739c444b: Pushed
d6803756744a: Pushed
b7b1f3a15779: Pushed
a89567dff12d: Pushed
59c7b561ff56: Pushed
9a2f9413d9e4: Pushed
a75caa09eb1f: Pushed
v1: digest: sha256:0799014f91384bda5b87591170b1242bcd719f07a03d1f9a1ddbae72b3543970 size: 1792
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已建立私人的異地複寫容器登錄、建置容器映像，並將該映像推送至您的登錄。 在遵循本教學課程的步驟時，您即已完成下列作業：

> [!div class="checklist"]
> * 建立異地複寫的 Azure Container Registry
> * 從 GitHub 複製應用程式原始程式碼
> * 從應用程式來源建置 Docker 容器映像
> * 將容器映像推送至登錄

若要了解如何使用異地複寫來提供本地的映像，以將容器部署至多個「用於容器的 Web 應用程式」執行個體，請前往下一個教學課程。

> [!div class="nextstepaction"]
> [從 Azure Container Registry 部署 Web 應用程式](container-registry-tutorial-deploy-app.md)

<!-- IMAGES -->
[tut-portal-01]: ./media/container-registry-tutorial-prepare-registry/tut-portal-01.png
[tut-portal-02]: ./media/container-registry-tutorial-prepare-registry/tut-portal-02.png
[tut-portal-03]: ./media/container-registry-tutorial-prepare-registry/tut-portal-03.png
[tut-portal-04]: ./media/container-registry-tutorial-prepare-registry/tut-portal-04.png
[tut-portal-05]: ./media/container-registry-tutorial-prepare-registry/tut-portal-05.png
[tut-app-01]: ./media/container-registry-tutorial-prepare-registry/tut-app-01.png
[tut-map-01]: ./media/container-registry-tutorial-prepare-registry/tut-map-01.png
