---
title: "aaaCreate 您的第一個 Azure 容器執行個體容器 |Azure 文件"
description: "部署和開始使用 Azure Container Instances"
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b57c52714933bd3b28c44d33f9af7cd1f23fb951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a>在 Azure Container Instances 中建立您的第一個容器

Azure 容器執行個體便可輕鬆 toocreate 並管理 Azure 中的容器。 在這個快速入門中，您會在 Azure 中建立容器，並將它公開 toohello 網際網路的公用 IP 位址。 只需要一個命令就能完成這項作業。 只在幾秒內，您就能在瀏覽器中看到下列結果：

![在瀏覽器中檢視使用 Azure Container Instances 所部署的應用程式][aci-app-browser]

如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本快速入門會要求執行 hello Azure CLI 版本 2.0.12 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="create-a-resource-group"></a>建立資源群組

Azure Container Instances 是 Azure 資源，必須放在 Azure 資源群組中，這是可用來部署和管理 Azure 資源的邏輯集合。

建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。 

hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置。

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a>建立容器

您可以提供名稱、Docker 映像和 Azure 資源群組來建立容器。 您可以選擇公開 hello 容器 toohello 網際網路的公用 IP 位址。 在此案例中，我們使用的容器裝載一個非常簡單的 Web 應用程式 (以 [Node.js](http://nodejs.org) 撰寫)。

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

在幾秒內，您應該取得回應 tooyour 要求。 Hello 容器會處於一開始，**建立**狀態，但應該在幾秒鐘內啟動。 您可以查看使用 hello hello 狀態`show`命令：

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

在 hello hello 輸出底部，您會看到 hello 容器佈建狀態和其 IP 位址：

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

一旦 hello 容器移 toohello **Succeeded**狀態時，可以使用提供的 hello IP 位址的 hello 瀏覽器中連線。 

![在瀏覽器中檢視使用 Azure Container Instances 所部署的應用程式][aci-app-browser]

## <a name="pull-hello-container-logs"></a>提取 hello 容器的記錄檔

您可以拉 hello 記錄檔中的 hello 容器所建立的 hello`logs`命令：

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

輸出：

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a>刪除 hello 容器

當您完成 hello 容器之後時，您可以移除使用 hello`delete`命令：

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a>後續步驟

Hello 的所有程式碼使用此快速入門中的 hello 容器則[GitHub 上][app-github-repo]，以及其 Dockerfile。 如果您想要自行建置和部署 tooAzure 容器執行個體使用 hello Azure 容器登錄中的 tootry，繼續進行 toohello Azure 容器執行個體教學課程。

> [!div class="nextstepaction"]
> [Azure Container Instances 教學課程](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png