---
title: "使用 Azure CLI 2.0 Linux 上的 Web 應用程式 aaaManage |Microsoft 文件"
description: "在 Linux 上使用 Azure CLI 管理 Web 應用程式。"
keywords: "azure app service, web 應用程式, cli, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a>在 Linux 上使用 Azure CLI 管理 Web 應用程式

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

您使用本文章中的 hello 命令都能 toocreate 和管理使用 Azure CLI 2.0 Linux 上的 Web 應用程式。
您可以開始使用 hello 新 hello CLI 有兩種版本：

* 在您的電腦上[安裝 Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)。
* 使用 [Azure Cloud Shell (預覽)](../cloud-shell/overview.md)


## <a name="create-a-linux-app-service-plan"></a>建立 Linux App Service 方案

toocreate Linux 應用程式服務方案，您可以使用下列命令的 hello:

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a>建立自訂 Docker 容器 Web 應用程式

toocreate web 應用程式並將它設定為 toorun 自訂的 Docker 容器，您可以使用下列命令的 hello:

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a>啟動 hello Docker 容器的記錄

tooactivate hello Docker 容器的記錄，您可以使用下列命令的 hello:

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a>Linux 應用程式上的現有 Web 應用程式變更 hello 自訂的 Docker 容器

toochange 先前建立的應用程式，從 hello 目前 Docker 映像 tooa 新映像，您可以使用下列命令的 hello:

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a>使用私人登錄中的 Docker 映像

您可以設定您的應用程式 toouse 映像從私用的登錄。 您需要 tooprovide hello url 登錄、 使用者名稱和密碼。 這可以使用下列命令的 hello 來達成：

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a>啟用自訂 Docker 映像的連續部署

以下列的命令，您可以啟用 hello hello CD 功能，並取得 hello webhook url。 這個 url 可以是使用的 tooconfigure 您 DockerHub 或 Azure 容器登錄中儲存機制。

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a>在 Linux 上使用其中一個內建執行階段架構來建立 Web 應用程式

toocreate PHP 5.6 Web 應用程式，您可以使用下列命令的 hello Linux 應用程式上。

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a>在 Linux 應用程式上變更現有 Web 應用程式的架構版本

toochange 先前建立的應用程式，從目前架構版本 tooNode.js hello 6.11，您可以使用下列命令的 hello:

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a>為您的 Web 應用程式設定 Git 部署

tooset 向上 Git 部署應用程式，您可以使用下列命令的 hello:

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a>後續步驟
* [什麼是 Linux 上的 Azure Web 應用程式？](app-service-linux-intro.md)
* [安裝 Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [Azure Cloud Shell (預覽)](../cloud-shell/overview.md)
* [在 Azure App Service 中設定預備環境](./web-sites-staged-publishing.md)
* [在 Linux 上使用 Azure Web 應用程式持續部署](./app-service-linux-ci-cd.md)
