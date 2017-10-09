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
# <a name="create-and-route-custom-events-with-azure-event-grid"></a><span data-ttu-id="61c1f-103">使用 Azure Event Grid 建立和路由傳送自訂事件</span><span class="sxs-lookup"><span data-stu-id="61c1f-103">Create and route custom events with Azure Event Grid</span></span>

<span data-ttu-id="61c1f-104">Azure 事件方格是 hello 雲端事件記錄服務。</span><span class="sxs-lookup"><span data-stu-id="61c1f-104">Azure Event Grid is an eventing service for hello cloud.</span></span> <span data-ttu-id="61c1f-105">在本文中，您可以使用 hello Azure CLI toocreate 自訂主題、 訂閱 toohello 主題，並觸發 hello 事件 tooview hello 結果。</span><span class="sxs-lookup"><span data-stu-id="61c1f-105">In this article, you use hello Azure CLI toocreate a custom topic, subscribe toohello topic, and trigger hello event tooview hello result.</span></span> <span data-ttu-id="61c1f-106">一般而言，您可以傳送事件 tooan 端點回應 toohello 事件，如 webhook 或 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="61c1f-106">Typically, you send events tooan endpoint that responds toohello event, such as, a webhook or Azure Function.</span></span> <span data-ttu-id="61c1f-107">不過，此發行項 toosimplify，只會收集 hello 訊息的 hello 事件 tooa URL 傳送。</span><span class="sxs-lookup"><span data-stu-id="61c1f-107">However, toosimplify this article, you send hello events tooa URL that merely collects hello messages.</span></span> <span data-ttu-id="61c1f-108">使用名為 [RequestBin](https://requestb.in/) 的開放原始碼、第三方工具來建立此 URL。</span><span class="sxs-lookup"><span data-stu-id="61c1f-108">You create this URL by using an open source, third-party tool called [RequestBin](https://requestb.in/).</span></span>

>[!NOTE]
><span data-ttu-id="61c1f-109">**RequestBin** 是一個開放原始碼工具，不適用於高輸送量的使用方式。</span><span class="sxs-lookup"><span data-stu-id="61c1f-109">**RequestBin** is an open source tool that is not intended for high throughput usage.</span></span> <span data-ttu-id="61c1f-110">這裡 hello 工具 hello 使用是單純的價格。</span><span class="sxs-lookup"><span data-stu-id="61c1f-110">hello use of hello tool here is purely demonstrative.</span></span> <span data-ttu-id="61c1f-111">如果您一次推送多個事件，您可能不會看到所有您在 hello 工具中的事件。</span><span class="sxs-lookup"><span data-stu-id="61c1f-111">If you push more than one event at a time, you might not see all of your events in hello tool.</span></span>

<span data-ttu-id="61c1f-112">當您完成時，您會看到 hello 事件資料，已傳送 tooan 端點。</span><span class="sxs-lookup"><span data-stu-id="61c1f-112">When you are finished, you see that hello event data has been sent tooan endpoint.</span></span>

![事件資料](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="61c1f-114">如果您選擇 tooinstall，並在本機上使用 hello CLI，本文時需執行 hello 最新版 Azure CLI (2.0.14 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="61c1f-114">If you choose tooinstall and use hello CLI locally, this article requires that you are running hello latest version of Azure CLI (2.0.14 or later).</span></span> <span data-ttu-id="61c1f-115">toofind hello 版本，執行`az --version`。</span><span class="sxs-lookup"><span data-stu-id="61c1f-115">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="61c1f-116">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="61c1f-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="61c1f-117">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="61c1f-117">Create a resource group</span></span>

<span data-ttu-id="61c1f-118">Event Grid 為 Azure 資源，必須放入 Azure 資源群組中。</span><span class="sxs-lookup"><span data-stu-id="61c1f-118">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="61c1f-119">hello 資源群組是邏輯集合至哪一個 Azure 部署及管理資源。</span><span class="sxs-lookup"><span data-stu-id="61c1f-119">hello resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="61c1f-120">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="61c1f-120">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="61c1f-121">hello 下列範例會建立名為的資源群組*gridResourceGroup*在 hello *westus2*位置。</span><span class="sxs-lookup"><span data-stu-id="61c1f-121">hello following example creates a resource group named *gridResourceGroup* in hello *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="61c1f-122">建立自訂主題</span><span class="sxs-lookup"><span data-stu-id="61c1f-122">Create a custom topic</span></span>

<span data-ttu-id="61c1f-123">主題會提供您張貼事件之使用者定義的端點。</span><span class="sxs-lookup"><span data-stu-id="61c1f-123">A topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="61c1f-124">hello 下列範例會建立 hello 主題資源群組中。</span><span class="sxs-lookup"><span data-stu-id="61c1f-124">hello following example creates hello topic in your resource group.</span></span> <span data-ttu-id="61c1f-125">以主題的唯一名稱取代 `<topic_name>`。</span><span class="sxs-lookup"><span data-stu-id="61c1f-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="61c1f-126">hello 主題名稱必須是唯一的因為它由 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="61c1f-126">hello topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="61c1f-127">Hello 預覽版本，支援事件方格**westus2**和**westcentralus**位置。</span><span class="sxs-lookup"><span data-stu-id="61c1f-127">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span>

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="61c1f-128">建立訊息端點</span><span class="sxs-lookup"><span data-stu-id="61c1f-128">Create a message endpoint</span></span>

<span data-ttu-id="61c1f-129">之前訂閱 toohello 主題，讓我們來建立 hello hello 事件訊息的端點。</span><span class="sxs-lookup"><span data-stu-id="61c1f-129">Before subscribing toohello topic, let's create hello endpoint for hello event message.</span></span> <span data-ttu-id="61c1f-130">要比撰寫程式碼 toorespond toohello 事件，讓我們來建立收集 hello 訊息，所以您可以檢視它們的端點。</span><span class="sxs-lookup"><span data-stu-id="61c1f-130">Rather than write code toorespond toohello event, let's create an endpoint that collects hello messages so you can view them.</span></span> <span data-ttu-id="61c1f-131">開放原始碼、 協力廠商工具，可讓您 toocreate 端點，而檢視要求傳送 tooit RequestBin。</span><span class="sxs-lookup"><span data-stu-id="61c1f-131">RequestBin is an open source, third-party tool that enables you toocreate an endpoint, and view requests that are sent tooit.</span></span> <span data-ttu-id="61c1f-132">跳過[RequestBin](https://requestb.in/)，然後按一下**建立 RequestBin**。</span><span class="sxs-lookup"><span data-stu-id="61c1f-132">Go too[RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span>  <span data-ttu-id="61c1f-133">複製 hello bin URL，因為您會需要它時訂閱 toohello 主題。</span><span class="sxs-lookup"><span data-stu-id="61c1f-133">Copy hello bin URL, because you need it when subscribing toohello topic.</span></span>

## <a name="subscribe-tooa-topic"></a><span data-ttu-id="61c1f-134">訂閱 tooa 主題</span><span class="sxs-lookup"><span data-stu-id="61c1f-134">Subscribe tooa topic</span></span>

<span data-ttu-id="61c1f-135">您的事件訂閱 tooa 主題 tootell 事件方格想 tootrack。</span><span class="sxs-lookup"><span data-stu-id="61c1f-135">You subscribe tooa topic tootell Event Grid which events you want tootrack.</span></span> <span data-ttu-id="61c1f-136">hello 下列範例會訂閱您所建立，而且會傳遞做為事件通知的 hello 端點 hello URL RequestBin toohello 主題。</span><span class="sxs-lookup"><span data-stu-id="61c1f-136">hello following example subscribes toohello topic you created, and passes hello URL from RequestBin as hello endpoint for event notification.</span></span> <span data-ttu-id="61c1f-137">取代`<event_subscription_name>`使用您的訂用帳戶，唯一的名稱和`<URL_from_RequestBin>`與 hello 值 hello 前面一節。</span><span class="sxs-lookup"><span data-stu-id="61c1f-137">Replace `<event_subscription_name>` with a unique name for your subscription, and `<URL_from_RequestBin>` with hello value from hello preceding section.</span></span> <span data-ttu-id="61c1f-138">藉由訂閱時指定端點，事件方格會處理 hello 路由的事件 toothat 端點。</span><span class="sxs-lookup"><span data-stu-id="61c1f-138">By specifying an endpoint when subscribing, Event Grid handles hello routing of events toothat endpoint.</span></span> <span data-ttu-id="61c1f-139">如`<topic_name>`，使用您稍早建立的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="61c1f-139">For `<topic_name>`, use hello value you created earlier.</span></span> 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a><span data-ttu-id="61c1f-140">傳送事件 tooyour 主題</span><span class="sxs-lookup"><span data-stu-id="61c1f-140">Send an event tooyour topic</span></span>

<span data-ttu-id="61c1f-141">現在，讓我們來觸發事件 toosee 事件方格將 hello 訊息 tooyour 端點的散佈。</span><span class="sxs-lookup"><span data-stu-id="61c1f-141">Now, let's trigger an event toosee how Event Grid distributes hello message tooyour endpoint.</span></span> <span data-ttu-id="61c1f-142">首先，我們取得 hello URL 和金鑰 hello 主題。</span><span class="sxs-lookup"><span data-stu-id="61c1f-142">First, let's get hello URL and key for hello topic.</span></span> <span data-ttu-id="61c1f-143">再次，將您的主題名稱用於 `<topic_name>`。</span><span class="sxs-lookup"><span data-stu-id="61c1f-143">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="61c1f-144">toosimplify 本文中，我們已將設定範例的事件資料 toosend toohello 主題。</span><span class="sxs-lookup"><span data-stu-id="61c1f-144">toosimplify this article, we have set up sample event data toosend toohello topic.</span></span> <span data-ttu-id="61c1f-145">一般而言，應用程式或 Azure 服務就會傳送 hello 事件資料。</span><span class="sxs-lookup"><span data-stu-id="61c1f-145">Typically, an application or Azure service would send hello event data.</span></span> <span data-ttu-id="61c1f-146">下列範例中的 hello 取得 hello 事件資料：</span><span class="sxs-lookup"><span data-stu-id="61c1f-146">hello following example gets hello event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="61c1f-147">如果您`echo "$body"`您所見 hello 完整事件。</span><span class="sxs-lookup"><span data-stu-id="61c1f-147">If you `echo "$body"` you can see hello full event.</span></span> <span data-ttu-id="61c1f-148">hello `data` hello JSON 的項目是 hello 裝載您的事件。</span><span class="sxs-lookup"><span data-stu-id="61c1f-148">hello `data` element of hello JSON is hello payload of your event.</span></span> <span data-ttu-id="61c1f-149">任何語式正確的 JSON 都可以進入這個欄位。</span><span class="sxs-lookup"><span data-stu-id="61c1f-149">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="61c1f-150">您也可以使用進階的路由和篩選的 hello [主旨] 欄位。</span><span class="sxs-lookup"><span data-stu-id="61c1f-150">You can also use hello subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="61c1f-151">CURL 是可執行 HTTP 要求的公用程式。</span><span class="sxs-lookup"><span data-stu-id="61c1f-151">CURL is a utility that performs HTTP requests.</span></span> <span data-ttu-id="61c1f-152">在本文中，我們會使用 CURL toosend hello 事件 tooour 主題。</span><span class="sxs-lookup"><span data-stu-id="61c1f-152">In this article, we use CURL toosend hello event tooour topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="61c1f-153">您也觸發了 hello 事件和事件方格傳送 hello 訊息 toohello 端點時，訂閱設定。</span><span class="sxs-lookup"><span data-stu-id="61c1f-153">You have triggered hello event, and Event Grid sent hello message toohello endpoint you configured when subscribing.</span></span> <span data-ttu-id="61c1f-154">瀏覽 toohello RequestBin 您稍早建立的 URL。</span><span class="sxs-lookup"><span data-stu-id="61c1f-154">Browse toohello RequestBin URL that you created earlier.</span></span> <span data-ttu-id="61c1f-155">或者，按一下已開啟 RequestBin 瀏覽器中的重新整理。</span><span class="sxs-lookup"><span data-stu-id="61c1f-155">Or, click refresh in your open RequestBin browser.</span></span> <span data-ttu-id="61c1f-156">您會看到您剛傳送嗨事件。</span><span class="sxs-lookup"><span data-stu-id="61c1f-156">You see hello event you just sent.</span></span> 

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

## <a name="clean-up-resources"></a><span data-ttu-id="61c1f-157">清除資源</span><span class="sxs-lookup"><span data-stu-id="61c1f-157">Clean up resources</span></span>
<span data-ttu-id="61c1f-158">如果您打算使用此事件的 toocontinue，請勿清除建立本文章中的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="61c1f-158">If you plan toocontinue working with this event, do not clean up hello resources created in this article.</span></span> <span data-ttu-id="61c1f-159">如果您不打算 toocontinue，使用下列命令 toodelete hello 資源在本文中所建立的 hello。</span><span class="sxs-lookup"><span data-stu-id="61c1f-159">If you do not plan toocontinue, use hello following command toodelete hello resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="61c1f-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="61c1f-160">Next steps</span></span>

<span data-ttu-id="61c1f-161">您現在知道如何 toocreate 主題和事件訂閱，深入了解哪些事件方格可協助您執行：</span><span class="sxs-lookup"><span data-stu-id="61c1f-161">Now that you know how toocreate topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="61c1f-162">關於 Event Grid</span><span class="sxs-lookup"><span data-stu-id="61c1f-162">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="61c1f-163">使用 Azure Event Grid 和 Logic Apps 監視虛擬機器變更</span><span class="sxs-lookup"><span data-stu-id="61c1f-163">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
