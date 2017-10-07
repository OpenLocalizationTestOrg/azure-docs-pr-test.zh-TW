---
title: "aaaContinuous on Linux 的 Azure Web 應用程式部署 |Microsoft 文件"
description: "如何在 Linux 上的 Azure Web 應用程式中的 toosetup 連續部署。"
keywords: azure app service, linux, oss
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a>在 Linux 上使用 Azure Web 應用程式連續部署

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

在本教學課程中，您可以從受控的 [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) 存放庫或 [Docker 中樞](https://hub.docker.com)設定自訂容器映像的連續部署。

## <a name="step-1---sign-in-tooazure"></a>步驟 1-登入 tooAzure

登入 toohello http://portal.azure.com 在 Azure 入口網站

## <a name="step-2---enable-container-continuous-deployment-feature"></a>步驟 2 - 啟用容器連續部署功能

您可以使用的 hello 持續部署功能啟用[Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)並執行下列命令的 hello

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

在 hello  **[Azure 入口網站](https://portal.azure.com/)**，按一下 hello **App Service** hello 左側的 hello 頁面的選項。

按一下您想要的 tooconfigure Docker Hub 連續部署的應用程式的 hello 名稱。

在 hello**應用程式設定**，新增應用程式稱為`DOCKER_ENABLE_CI`hello 值`true`。

![將應用程式設定的影像插入](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a>步驟 3 - 準備 Webhook URL

您可以取得 hello Webhook URL 使用[Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)並執行下列命令的 hello

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

Hello Webhook URL，您需要下列端點 toohave hello: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`。

您可以取得您`publishingusername`和`publishingpwd`下載 hello web 應用程式發行設定檔使用 hello Azure 入口網站。

![將新增 webhook 2 的映像插入](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a>步驟 4：新增 Web Hook

### <a name="azure-container-registry"></a>Azure Container Registry

在您的登錄入口網站刀鋒視窗中，按一下 [Webhook]，按一下 [新增] 以建立新的 webhook。 在 hello**建立 webhook**刀鋒視窗中，提供您的 webhook 名稱。 Hello Webhook URI，您需要從取得的 tooprovide hello URL**步驟 3**

請確定您定義 hello 範圍，如 hello 包含您的容器映像儲存機制。

![插入 webhook 的映像](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

取得更新 hello 映像，hello web 應用程式會自動更新會自動 hello 新映像。

### <a name="docker-hub"></a>Docker 中樞

在您的 [Docker 中樞] 頁面上，依序按一下 [Webhook]、[建立 WEBHOOK]。

![將新增 webhook 1 的映像插入](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

Hello Webhook URL，您需要從取得的 tooprovide hello URL**步驟 3**

![將新增 webhook 2 的映像插入](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

取得更新 hello 映像，hello web 應用程式會自動更新會自動 hello 新映像。

## <a name="next-steps"></a>後續步驟
* [什麼是 Linux 上的 Azure Web 應用程式？](./app-service-linux-intro.md)
* [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/)
* [在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態](app-service-linux-using-nodejs-pm2.md)
* [在 Linux 上的 Azure Web 應用程式中使用 .NET Core](app-service-linux-using-dotnetcore.md)
* [在 Linux 上的 Azure Web 應用程式中使用 Ruby](app-service-linux-ruby-get-started.md)
* [Toouse 自訂的 Docker 的 Linux 上的 Azure Web 應用程式的映像](./app-service-linux-using-custom-docker-image.md)
* [Linux 上的 Azure App Service Web 應用程式常見問題集](./app-service-linux-faq.md) 
* [在 Linux 上使用 Azure CLI 2.0 管理 Web 應用程式](./app-service-linux-cli.md)



