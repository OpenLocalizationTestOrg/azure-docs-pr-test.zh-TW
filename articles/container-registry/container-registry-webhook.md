---
title: "aaaAzure 容器登錄 webhook |Microsoft 文件"
description: Azure Container Registry Webhook
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: "Docker、容器、ACR"
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a>使用 Azure Container Registry Webhook - Azure 入口網站

Azure 容器登錄中儲存並管理私人 Docker 容器映像，Docker Hub 儲存公用 Docker 映像的類似 toohello 方式。 您使用 webhook tootrigger 事件時，會發生在您登錄儲存機制的其中一個特定動作。 Webhook 可以回應 hello 登錄層級 tooevents 或向下 tooa 特定儲存機制標記範圍內。 

如需背景和概念，請參閱 hello[概觀](./container-registry-intro.md)。

## <a name="prerequisites"></a>必要條件 

- Azure 容器管理的登錄 - 在 Azure 訂用帳戶中建立受管理的容器登錄。 例如，使用 hello Azure 入口網站或 hello Azure CLI 2.0。 
- Docker CLI-tooset Docker 主機和存取 hello Docker CLI 命令，在本機電腦上安裝 Docker 引擎。 

## <a name="create-webhook-azure-portal"></a>建立 Webhook Azure 入口網站

1. 登入 toohello Azure 入口網站，並瀏覽您想在其中 toocreate webhook toohello 登錄。 

2. 在 hello 容器刀鋒視窗中，選取 hello"Webhook 」 索引標籤。 

3. 從 hello webhook 刀鋒視窗工具列中選取 [新增]。 

4. 完整的 hello*建立 Webhook*表單以 hello 下列資訊：

| 值 | 描述 |
|---|---|
| 名稱 | 您想要 toogive toohello webhook hello 名稱。 它只能包含小寫字母和數字，且必須為 5-50 個字元之間。 |
| 服務 URI | hello hello webhook 傳送通知 POST 的位置的 URI。 |
| 自訂標頭 | 您想要 toopass 以及 hello POST 要求標頭。 它們應該為「金鑰：值」的格式。 |
| 觸發程序動作 | Hello webhook 觸發程序的動作。 目前 webhook 可藉由推入及/或刪除動作 tooan 映像。 |
| 狀態 | hello hello webhook 建立之後的狀態。 此選項預設為啟用狀態。 |
| Scope | 於哪一個 hello webhook works hello 範圍。 根據預設 hello 範圍是 hello 登錄中的所有事件。 可以針對儲存機制或標記中指定使用 hello 格式"儲存機制： 標記 」。 |

範例 Webhook 表單：

![DCOS UI](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a>建立 Webhook Azure CLI

webhook 使用 toocreate hello Azure CLI，使用 hello [az acr webhook 建立](/cli/azure/acr/webhook#create)命令。

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a>測試 Webhook

### <a name="azure-portal"></a>Azure 入口網站

在容器上的先前 toousing hello webhook 發送的映像，刪除動作，可以測試使用 hello **Ping**  按鈕。 使用時，會傳送一般 post 要求 toohello 指定端點與記錄檔 hello 回應 hello Ping。 這是很有幫助 hello webhook 的 tooverify 是否已正確設定。

1. 選取您想要 tootest hello webhook。 
2. 在 hello 頂端的工具列上，選取 hello"Ping"動作。 
3. 請檢查 hello 要求和回應。

### <a name="azure-cli"></a>Azure CLI

tootest 以 hello Azure CLI ACR webhook 使用 hello [az acr webhook ping](/cli/azure/acr/webhook#ping)命令。

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

toosee hello 結果，請使用 hello [az acr webhook 清單事件](/cli/azure/acr/webhook#list-events)命令。 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a>刪除 Webhook

### <a name="azure-portal"></a>Azure 入口網站

可以藉由選取 hello webhook hello hello Azure 入口網站上的刪除按鈕來刪除每個 webhook。

### <a name="azure-cli"></a>Azure CLI

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```