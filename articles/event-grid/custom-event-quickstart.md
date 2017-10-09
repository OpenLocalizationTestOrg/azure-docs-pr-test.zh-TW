---
title: "Azure 事件方格 aaaCustom 事件 |Microsoft 文件"
description: "使用 Azure 事件方格 toopublish 主題和訂閱 toothat 事件。"
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 5055df1c970b043cadf06978a076f7f5c83501cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a>使用 Azure Event Grid 建立和路由傳送自訂事件

Azure 事件方格是 hello 雲端事件記錄服務。 在本文中，您可以使用 hello Azure CLI toocreate 自訂主題、 訂閱 toohello 主題，並觸發 hello 事件 tooview hello 結果。 一般而言，您可以傳送事件 tooan 端點回應 toohello 事件，如 webhook 或 Azure 函式。 不過，此發行項 toosimplify，只會收集 hello 訊息的 hello 事件 tooa URL 傳送。 使用名為 [RequestBin](https://requestb.in/) 的開放原始碼、第三方工具來建立此 URL。

>[!NOTE]
>**RequestBin** 是一個開放原始碼工具，不適用於高輸送量的使用方式。 這裡 hello 工具 hello 使用是單純的價格。 如果您一次推送多個事件，您可能不會看到所有您在 hello 工具中的事件。

當您完成時，您會看到 hello 事件資料，已傳送 tooan 端點。

![事件資料](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本文時需執行 hello 最新版 Azure CLI (2.0.14 或更新版本)。 toofind hello 版本，執行`az --version`。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)。

## <a name="create-a-resource-group"></a>建立資源群組

Event Grid 為 Azure 資源，必須放入 Azure 資源群組中。 hello 資源群組是邏輯集合至哪一個 Azure 部署及管理資源。

建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。 

hello 下列範例會建立名為的資源群組*gridResourceGroup*在 hello *westus2*位置。

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a>建立自訂主題

主題會提供您張貼事件之使用者定義的端點。 hello 下列範例會建立 hello 主題資源群組中。 以主題的唯一名稱取代 `<topic_name>`。 hello 主題名稱必須是唯一的因為它由 DNS 項目。 Hello 預覽版本，支援事件方格**westus2**和**westcentralus**位置。

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a>建立訊息端點

之前訂閱 toohello 主題，讓我們來建立 hello hello 事件訊息的端點。 要比撰寫程式碼 toorespond toohello 事件，讓我們來建立收集 hello 訊息，所以您可以檢視它們的端點。 開放原始碼、 協力廠商工具，可讓您 toocreate 端點，而檢視要求傳送 tooit RequestBin。 跳過[RequestBin](https://requestb.in/)，然後按一下**建立 RequestBin**。  複製 hello bin URL，因為您會需要它時訂閱 toohello 主題。

## <a name="subscribe-tooa-topic"></a>訂閱 tooa 主題

您的事件訂閱 tooa 主題 tootell 事件方格想 tootrack。 hello 下列範例會訂閱您所建立，而且會傳遞做為事件通知的 hello 端點 hello URL RequestBin toohello 主題。 取代`<event_subscription_name>`使用您的訂用帳戶，唯一的名稱和`<URL_from_RequestBin>`與 hello 值 hello 前面一節。 藉由訂閱時指定端點，事件方格會處理 hello 路由的事件 toothat 端點。 如`<topic_name>`，使用您稍早建立的 hello 值。 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a>傳送事件 tooyour 主題

現在，讓我們來觸發事件 toosee 事件方格將 hello 訊息 tooyour 端點的散佈。 首先，我們取得 hello URL 和金鑰 hello 主題。 再次，將您的主題名稱用於 `<topic_name>`。

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

toosimplify 本文中，我們已將設定範例的事件資料 toosend toohello 主題。 一般而言，應用程式或 Azure 服務就會傳送 hello 事件資料。 下列範例中的 hello 取得 hello 事件資料：

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

如果您`echo "$body"`您所見 hello 完整事件。 hello `data` hello JSON 的項目是 hello 裝載您的事件。 任何語式正確的 JSON 都可以進入這個欄位。 您也可以使用進階的路由和篩選的 hello [主旨] 欄位。

CURL 是可執行 HTTP 要求的公用程式。 在本文中，我們會使用 CURL toosend hello 事件 tooour 主題。 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

您也觸發了 hello 事件和事件方格傳送 hello 訊息 toohello 端點時，訂閱設定。 瀏覽 toohello RequestBin 您稍早建立的 URL。 或者，按一下已開啟 RequestBin 瀏覽器中的重新整理。 您會看到您剛傳送嗨事件。 

```json
[{
  "id": "1807",
  "eventType": "recordInserted",
  "subject": "myapp/vehicles/motorcycles",
  "eventTime": "2017-08-10T21:03:07+00:00",
  "data": {
    "make": "Ducati",
    "model": "Monster"
  },
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/topics/{topic}"
}]
```

## <a name="clean-up-resources"></a>清除資源
如果您打算使用此事件的 toocontinue，請勿清除建立本文章中的 hello 資源。 如果您不打算 toocontinue，使用下列命令 toodelete hello 資源在本文中所建立的 hello。

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a>後續步驟

您現在知道如何 toocreate 主題和事件訂閱，深入了解哪些事件方格可協助您執行：

- [關於 Event Grid](overview.md)
- [使用 Azure Event Grid 和 Logic Apps 監視虛擬機器變更](monitor-virtual-machine-changes-event-grid-logic-app.md)
