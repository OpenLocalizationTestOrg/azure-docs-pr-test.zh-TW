---
title: "Azure Event Grid 的自訂事件 | Microsoft Docs"
description: "使用 Azure Event Grid 來發佈主題，以及訂閱該事件。"
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 0290836bebadb20085a3ce84dddc088c3af385da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a><span data-ttu-id="dd5e8-103">使用 Azure Event Grid 建立和路由傳送自訂事件</span><span class="sxs-lookup"><span data-stu-id="dd5e8-103">Create and route custom events with Azure Event Grid</span></span>

<span data-ttu-id="dd5e8-104">Azure Event Grid 是一項雲端事件服務。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-104">Azure Event Grid is an eventing service for the cloud.</span></span> <span data-ttu-id="dd5e8-105">在本文中，您可使用 Azure CLI 建立自訂主題、訂閱主題，以及觸發事件來檢視結果。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-105">In this article, you use the Azure CLI to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span></span> <span data-ttu-id="dd5e8-106">一般而言，您可將事件傳送至可回應事件的端點，例如 Webhook 或 Azure Function。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-106">Typically, you send events to an endpoint that responds to the event, such as, a webhook or Azure Function.</span></span> <span data-ttu-id="dd5e8-107">不過，若要簡化這篇文章，您可將事件傳送至只會收集訊息的 URL。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-107">However, to simplify this article, you send the events to a URL that merely collects the messages.</span></span> <span data-ttu-id="dd5e8-108">使用名為 [RequestBin](https://requestb.in/) 的開放原始碼、第三方工具來建立此 URL。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-108">You create this URL by using an open source, third-party tool called [RequestBin](https://requestb.in/).</span></span>

>[!NOTE]
><span data-ttu-id="dd5e8-109">**RequestBin** 是一個開放原始碼工具，不適用於高輸送量的使用方式。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-109">**RequestBin** is an open source tool that is not intended for high throughput usage.</span></span> <span data-ttu-id="dd5e8-110">在此使用工具單純用於示範。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-110">The use of the tool here is purely demonstrative.</span></span> <span data-ttu-id="dd5e8-111">如果您一次推送多個事件，則可能看不到工具中的所有事件。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-111">If you push more than one event at a time, you might not see all of your events in the tool.</span></span>

<span data-ttu-id="dd5e8-112">當您完成時，您會看到事件資料已傳送至端點。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-112">When you are finished, you see that the event data has been sent to an endpoint.</span></span>

![事件資料](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="dd5e8-114">如果您選擇在本機安裝和使用 CLI，本文會要求您執行最新版的 Azure CLI (2.0.14 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-114">If you choose to install and use the CLI locally, this article requires that you are running the latest version of Azure CLI (2.0.14 or later).</span></span> <span data-ttu-id="dd5e8-115">若要尋找版本，請執行 `az --version`。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-115">To find the version, run `az --version`.</span></span> <span data-ttu-id="dd5e8-116">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-116">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="dd5e8-117">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="dd5e8-117">Create a resource group</span></span>

<span data-ttu-id="dd5e8-118">Event Grid 為 Azure 資源，必須放入 Azure 資源群組中。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-118">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="dd5e8-119">資源群組是在其中部署與管理 Azure 資源的邏輯集合。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-119">The resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="dd5e8-120">使用 [az group create](/cli/azure/group#create) 命令來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-120">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="dd5e8-121">下列範例會在 westus2 位置建立名為 gridResourceGroup 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-121">The following example creates a resource group named *gridResourceGroup* in the *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="dd5e8-122">建立自訂主題</span><span class="sxs-lookup"><span data-stu-id="dd5e8-122">Create a custom topic</span></span>

<span data-ttu-id="dd5e8-123">主題會提供您張貼事件之使用者定義的端點。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-123">A topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="dd5e8-124">下列範例可在您的資源群組中建立主題。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-124">The following example creates the topic in your resource group.</span></span> <span data-ttu-id="dd5e8-125">以主題的唯一名稱取代 `<topic_name>`。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="dd5e8-126">主題名稱必須是唯一的，因為它由 DNS 項目表示。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-126">The topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="dd5e8-127">在預覽版本中，Event Grid 支援 **westus2** 和 **westcentralus** 位置。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-127">For the preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span>

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="dd5e8-128">建立訊息端點</span><span class="sxs-lookup"><span data-stu-id="dd5e8-128">Create a message endpoint</span></span>

<span data-ttu-id="dd5e8-129">訂閱主題之前，讓我們建立事件訊息的端點。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-129">Before subscribing to the topic, let's create the endpoint for the event message.</span></span> <span data-ttu-id="dd5e8-130">讓我們建立可收集訊息的端點，以便檢視訊息，而不需撰寫程式碼來回應事件。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-130">Rather than write code to respond to the event, let's create an endpoint that collects the messages so you can view them.</span></span> <span data-ttu-id="dd5e8-131">RequestBin 是一個開放原始碼的第三方工具，可讓您建立端點，以及檢視傳送給它的要求。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-131">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="dd5e8-132">移至 [RequestBin](https://requestb.in/)，然後按一下 [建立 RequestBin]。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-132">Go to [RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span>  <span data-ttu-id="dd5e8-133">複製 bin URL，因為您在訂閱主題時需要用到它。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-133">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

## <a name="subscribe-to-a-topic"></a><span data-ttu-id="dd5e8-134">訂閱主題</span><span class="sxs-lookup"><span data-stu-id="dd5e8-134">Subscribe to a topic</span></span>

<span data-ttu-id="dd5e8-135">您可訂閱主題，告知 Event Grid 您想要追蹤的事件。下列範例可訂閱您所建立的主題，從 RequestBin 傳遞 URL 作為事件通知的端點。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-135">You subscribe to a topic to tell Event Grid which events you want to track. The following example subscribes to the topic you created, and passes the URL from RequestBin as the endpoint for event notification.</span></span> <span data-ttu-id="dd5e8-136">以您訂用帳戶的唯一名稱取代 `<event_subscription_name>`，並以上一節中的值取代 `<URL_from_RequestBin>`。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-136">Replace `<event_subscription_name>` with a unique name for your subscription, and `<URL_from_RequestBin>` with the value from the preceding section.</span></span> <span data-ttu-id="dd5e8-137">藉由在訂閱時指定端點，以便 Event Grid 將事件路由傳送至該端點。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-137">By specifying an endpoint when subscribing, Event Grid handles the routing of events to that endpoint.</span></span> <span data-ttu-id="dd5e8-138">對於 `<topic_name>`，使用您稍早建立的值。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-138">For `<topic_name>`, use the value you created earlier.</span></span> 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-to-your-topic"></a><span data-ttu-id="dd5e8-139">將事件傳送至主題</span><span class="sxs-lookup"><span data-stu-id="dd5e8-139">Send an event to your topic</span></span>

<span data-ttu-id="dd5e8-140">現在，讓我們觸發事件以了解 Event Grid 如何將訊息散發至您的端點。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-140">Now, let's trigger an event to see how Event Grid distributes the message to your endpoint.</span></span> <span data-ttu-id="dd5e8-141">首先，讓我們取得主題的 URL 和金鑰。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-141">First, let's get the URL and key for the topic.</span></span> <span data-ttu-id="dd5e8-142">再次，將您的主題名稱用於 `<topic_name>`。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-142">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="dd5e8-143">為了簡化這篇文章，我們已設定要傳送至主題的範例事件資料。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-143">To simplify this article, we have set up sample event data to send to the topic.</span></span> <span data-ttu-id="dd5e8-144">一般而言，應用程式或 Azure 服務就會傳送事件資料。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-144">Typically, an application or Azure service would send the event data.</span></span> <span data-ttu-id="dd5e8-145">下列範例可取得事件資料：</span><span class="sxs-lookup"><span data-stu-id="dd5e8-145">The following example gets the event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="dd5e8-146">如果您 `echo "$body"`，您可以看到完整事件。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-146">If you `echo "$body"` you can see the full event.</span></span> <span data-ttu-id="dd5e8-147">JSON 的 `data` 元素是您的事件承載。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-147">The `data` element of the JSON is the payload of your event.</span></span> <span data-ttu-id="dd5e8-148">任何語式正確的 JSON 都可以進入這個欄位。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-148">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="dd5e8-149">您也可以使用主體欄位進行進階路由傳送或篩選。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-149">You can also use the subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="dd5e8-150">CURL 是可執行 HTTP 要求的公用程式。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-150">CURL is a utility that performs HTTP requests.</span></span> <span data-ttu-id="dd5e8-151">在本文中，我們會使用 CURL 將事件傳送到我們的主題。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-151">In this article, we use CURL to send the event to our topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="dd5e8-152">您已觸發此事件，而 Event Grid 會將訊息傳送至您在訂閱時設定的端點。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-152">You have triggered the event, and Event Grid sent the message to the endpoint you configured when subscribing.</span></span> <span data-ttu-id="dd5e8-153">瀏覽至您稍早建立的 RequestBin URL。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-153">Browse to the RequestBin URL that you created earlier.</span></span> <span data-ttu-id="dd5e8-154">或者，按一下已開啟 RequestBin 瀏覽器中的重新整理。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-154">Or, click refresh in your open RequestBin browser.</span></span> <span data-ttu-id="dd5e8-155">您會看到剛傳送的事件。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-155">You see the event you just sent.</span></span> 

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

## <a name="clean-up-resources"></a><span data-ttu-id="dd5e8-156">清除資源</span><span class="sxs-lookup"><span data-stu-id="dd5e8-156">Clean up resources</span></span>
<span data-ttu-id="dd5e8-157">如果您打算繼續使用此事件，請勿清除在此本文中建立的資源。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-157">If you plan to continue working with this event, do not clean up the resources created in this article.</span></span> <span data-ttu-id="dd5e8-158">如果您不打算繼續，請使用下列命令來刪除您在本文建立的資源。</span><span class="sxs-lookup"><span data-stu-id="dd5e8-158">If you do not plan to continue, use the following command to delete the resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="dd5e8-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dd5e8-159">Next steps</span></span>

<span data-ttu-id="dd5e8-160">您現在知道如何建立主題和事件訂閱，深入了解 Event Grid 可協助您：</span><span class="sxs-lookup"><span data-stu-id="dd5e8-160">Now that you know how to create topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="dd5e8-161">關於 Event Grid</span><span class="sxs-lookup"><span data-stu-id="dd5e8-161">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="dd5e8-162">使用 Azure Event Grid 和 Logic Apps 監視虛擬機器變更</span><span class="sxs-lookup"><span data-stu-id="dd5e8-162">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
