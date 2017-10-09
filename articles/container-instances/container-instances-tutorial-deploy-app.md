---
title: "aaaAzure 容器執行個體的教學課程-應用程式部署 |Microsoft 文件"
description: "Azure 容器執行個體教學課程 - 部署應用程式"
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
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a>部署容器 tooAzure 容器執行個體

這是 hello 三段式教學課程的最後一個。 上一節，[建立容器映像來源](container-instances-tutorial-prepare-app.md)和[推入 tooan Azure 容器登錄中](container-instances-tutorial-prepare-acr.md)。 本節藉由部署 hello 容器 tooAzure 容器執行個體完成 hello 教學課程。 完成的步驟包括：

> [!div class="checklist"]
> * 使用 Azure Resource Manager 範本來定義容器群組
> * 部署使用 Azure CLI hello hello 容器群組
> * 檢視容器記錄

## <a name="deploy-hello-container-using-hello-azure-cli"></a>部署使用 Azure CLI hello hello 容器

hello Azure CLI 能夠部署在單一命令中的容器 tooAzure 容器執行個體。 因為 hello 容器映像裝載在 hello 私人 Azure 容器登錄中，您必須包含 hello 認證需要的 tooaccess 它。 如有必要，您可以查詢這些認證，如下所示。

容器登錄的登入伺服器 (以登錄名稱來更新)：

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

容器登錄密碼：

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

toodeploy 1 CPU 核心和 1 GB 的記憶體，執行下列命令的 hello 要求您從 hello 容器登錄中與資源的容器映像：

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

在幾秒內，您就會從 Azure Resource Manager 收到首次的回應。 hello 部署中，使用 tooview hello 狀態：

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

我們可以繼續執行此命令，直到 hello 狀態變更從*暫止*太*執行*。 然後我們可以繼續進行。

## <a name="view-hello-application-and-container-logs"></a>檢視 hello 應用程式和容器的記錄檔

Hello 部署成功後，開啟瀏覽器 toohello IP 位址的下列命令的 hello hello 輸出所示：

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Hello 瀏覽器中的 hello world 應用程式][aci-app-browser]

您也可以檢視 hello 的 hello 容器的記錄檔輸出：

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

輸出：

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您完成部署您的容器 tooAzure 容器執行個體的 hello 程序。 已完成下列步驟的 hello:

> [!div class="checklist"]
> * 部署的 hello Azure 容器登錄中使用的 hello 容器 hello Azure CLI
> * 在 hello 瀏覽器中檢視 hello 應用程式
> * 檢視 hello 容器的記錄檔

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
