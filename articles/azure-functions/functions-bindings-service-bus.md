---
title: "aaaAzure 函式服務匯流排觸發程序和繫結 |Microsoft 文件"
description: "了解觸發 toouse Azure 服務匯流排的方式，在 Azure 函式中的繫結。"
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, 動態運算, 無伺服器架構"
ms.assetid: daedacf0-6546-4355-a65c-50873e74f66b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/01/2017
ms.author: glenga
ms.openlocfilehash: dff9e89bd3840b8c11f91cae41e13502afc7aa60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="5caba-104">Azure Functions 服務匯流排繫結</span><span class="sxs-lookup"><span data-stu-id="5caba-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="5caba-105">這篇文章說明如何 tooconfigure 地使用 Azure 功能中的 Azure 服務匯流排繫結。</span><span class="sxs-lookup"><span data-stu-id="5caba-105">This article explains how tooconfigure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="5caba-106">Azure Functions 支援服務匯流排佇列和主題的觸發程序和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="5caba-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="5caba-107">服務匯流排觸發程序</span><span class="sxs-lookup"><span data-stu-id="5caba-107">Service Bus trigger</span></span>
<span data-ttu-id="5caba-108">使用 hello Service Bus 觸發程序 toorespond toomessages 從服務匯流排佇列或主題。</span><span class="sxs-lookup"><span data-stu-id="5caba-108">Use hello Service Bus trigger toorespond toomessages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="5caba-109">hello Service Bus 佇列和主題觸發程序會由下列 JSON 物件中 hello hello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="5caba-109">hello Service Bus queue and topic triggers are defined by hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="5caba-110">*佇列*觸發程序︰</span><span class="sxs-lookup"><span data-stu-id="5caba-110">*queue* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* <span data-ttu-id="5caba-111">*主題*觸發程序︰</span><span class="sxs-lookup"><span data-stu-id="5caba-111">*topic* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

<span data-ttu-id="5caba-112">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="5caba-112">Note hello following:</span></span>

* <span data-ttu-id="5caba-113">如`connection`，[函式應用程式中建立的應用程式設定](functions-how-to-use-azure-function-app-settings.md)包含 hello 連接字串 tooyour 服務匯流排命名空間，然後指定 hello hello 應用程式設定名稱在 hello`connection`觸發程序中的屬性。</span><span class="sxs-lookup"><span data-stu-id="5caba-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your trigger.</span></span> <span data-ttu-id="5caba-114">您取得 hello 連接字串顯示 hello 步驟[取得 hello 管理認證](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials)。</span><span class="sxs-lookup"><span data-stu-id="5caba-114">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="5caba-115">hello 連接字串必須是服務匯流排命名空間、 不限的 tooa 特定佇列或主題。</span><span class="sxs-lookup"><span data-stu-id="5caba-115">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="5caba-116">如果您離開`connection`空的 hello 觸發程序會假設預設服務匯流排連接字串會指定在應用程式中設定，稱為`AzureWebJobsServiceBus`。</span><span class="sxs-lookup"><span data-stu-id="5caba-116">If you leave `connection` empty, hello trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="5caba-117">針對 `accessRights`，可用值為 `manage` 和 `listen`。</span><span class="sxs-lookup"><span data-stu-id="5caba-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="5caba-118">hello 預設值是`manage`，表示該 hello`connection`具有 hello**管理**權限。</span><span class="sxs-lookup"><span data-stu-id="5caba-118">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="5caba-119">如果您使用的連接字串，但是沒有 hello**管理**權限，設定`accessRights`太`listen`。</span><span class="sxs-lookup"><span data-stu-id="5caba-119">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="5caba-120">否則，hello 函式執行階段可能會失敗，嘗試 toodo 作業需要管理權限。</span><span class="sxs-lookup"><span data-stu-id="5caba-120">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="5caba-121">觸發程序行為</span><span class="sxs-lookup"><span data-stu-id="5caba-121">Trigger behavior</span></span>
* <span data-ttu-id="5caba-122">**單一執行緒**-根據預設，多個訊息同時的 hello 函式執行階段處理序。</span><span class="sxs-lookup"><span data-stu-id="5caba-122">**Single-threading** - By default, hello Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="5caba-123">toodirect hello 執行階段 tooprocess 只有單一佇列或主題訊息一次設定`serviceBus.maxConcurrentCalls`中的 too1 *host.json*。</span><span class="sxs-lookup"><span data-stu-id="5caba-123">toodirect hello runtime tooprocess only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` too1 in *host.json*.</span></span> 
  <span data-ttu-id="5caba-124">如需有關 *host.json* 的資訊，請參閱[資料夾結構](functions-reference.md#folder-structure)和 [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="5caba-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="5caba-125">**有害訊息處理** - 服務匯流排會自行處理無法在 Azure Functions 組態或程式碼中控制或設定的有害訊息。</span><span class="sxs-lookup"><span data-stu-id="5caba-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="5caba-126">**PeekLock 行為**-hello 函式執行階段接收的訊息中[`PeekLock`模式](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode)和呼叫`Complete`hello 訊息，如果成功，完成 hello 函式或呼叫`Abandon`如果 hello函式會失敗。</span><span class="sxs-lookup"><span data-stu-id="5caba-126">**PeekLock behavior** - hello Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> 
  <span data-ttu-id="5caba-127">如果 hello 函式執行時間長於 hello `PeekLock` hello 鎖定逾時，會自動更新。</span><span class="sxs-lookup"><span data-stu-id="5caba-127">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="5caba-128">觸發程序使用方式</span><span class="sxs-lookup"><span data-stu-id="5caba-128">Trigger usage</span></span>
<span data-ttu-id="5caba-129">本節說明如何 toouse Service Bus 觸發函式程式碼中。</span><span class="sxs-lookup"><span data-stu-id="5caba-129">This section shows you how toouse your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="5caba-130">在 C# 和 F # hello Service Bus 觸發程序訊息可以是 hello 的下列輸入的類型的已還原序列化的 tooany:</span><span class="sxs-lookup"><span data-stu-id="5caba-130">In C# and F#, hello Service Bus trigger message can be deserialized tooany of hello following input types:</span></span>

* <span data-ttu-id="5caba-131">`string` - 適用於字串訊息</span><span class="sxs-lookup"><span data-stu-id="5caba-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="5caba-132">`byte[]` - 適用於二進位資料</span><span class="sxs-lookup"><span data-stu-id="5caba-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="5caba-133">任何[物件](https://msdn.microsoft.com/library/system.object.aspx) - 適用於 JSON 序列化的資料。</span><span class="sxs-lookup"><span data-stu-id="5caba-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="5caba-134">如果您宣告自訂的輸入的類型，例如`CustomType`，Azure 函式會嘗試 toodeserialize hello JSON 資料到您指定的型別。</span><span class="sxs-lookup"><span data-stu-id="5caba-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="5caba-135">`BrokeredMessage`-可讓您 hello 還原序列化訊息以 hello [BrokeredMessage.GetBody<T>（)](https://msdn.microsoft.com/library/hh144211.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="5caba-135">`BrokeredMessage` - gives you hello deserialized message with hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="5caba-136">在 Node.js hello Service Bus 觸發程序訊息傳遞到做為字串或 JSON 物件的 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="5caba-136">In Node.js, hello Service Bus trigger message is passed into hello function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="5caba-137">觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="5caba-137">Trigger sample</span></span>
<span data-ttu-id="5caba-138">假設您有下列 function.json hello:</span><span class="sxs-lookup"><span data-stu-id="5caba-138">Suppose you have hello following function.json:</span></span>

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

<span data-ttu-id="5caba-139">請參閱 hello 處理服務匯流排佇列訊息的特定語言的範例。</span><span class="sxs-lookup"><span data-stu-id="5caba-139">See hello language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="5caba-140">C#</span><span class="sxs-lookup"><span data-stu-id="5caba-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="5caba-141">F#</span><span class="sxs-lookup"><span data-stu-id="5caba-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="5caba-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="5caba-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="5caba-143">C# 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="5caba-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="5caba-144">F# 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="5caba-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="5caba-145">Node.js 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="5caba-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="5caba-146">服務匯流排輸出繫結</span><span class="sxs-lookup"><span data-stu-id="5caba-146">Service Bus output binding</span></span>
<span data-ttu-id="5caba-147">hello 函式的服務匯流排佇列和主題輸出使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="5caba-147">hello Service Bus queue and topic output for a function use hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="5caba-148">*佇列*輸出︰</span><span class="sxs-lookup"><span data-stu-id="5caba-148">*queue* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* <span data-ttu-id="5caba-149">*主題*輸出︰</span><span class="sxs-lookup"><span data-stu-id="5caba-149">*topic* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

<span data-ttu-id="5caba-150">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="5caba-150">Note hello following:</span></span>

* <span data-ttu-id="5caba-151">如`connection`，[函式應用程式中建立的應用程式設定](functions-how-to-use-azure-function-app-settings.md)包含 hello 連接字串 tooyour 服務匯流排命名空間，然後指定 hello hello 應用程式設定名稱在 hello`connection`在輸出中的屬性繫結。</span><span class="sxs-lookup"><span data-stu-id="5caba-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your output binding.</span></span> <span data-ttu-id="5caba-152">您取得 hello 連接字串顯示 hello 步驟[取得 hello 管理認證](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials)。</span><span class="sxs-lookup"><span data-stu-id="5caba-152">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="5caba-153">hello 連接字串必須是服務匯流排命名空間、 不限的 tooa 特定佇列或主題。</span><span class="sxs-lookup"><span data-stu-id="5caba-153">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="5caba-154">如果您離開`connection`空的 hello 輸出繫結假設預設服務匯流排連接字串會指定在應用程式中設定，稱為`AzureWebJobsServiceBus`。</span><span class="sxs-lookup"><span data-stu-id="5caba-154">If you leave `connection` empty, hello output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="5caba-155">針對 `accessRights`，可用值為 `manage` 和 `listen`。</span><span class="sxs-lookup"><span data-stu-id="5caba-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="5caba-156">hello 預設值是`manage`，表示該 hello`connection`具有 hello**管理**權限。</span><span class="sxs-lookup"><span data-stu-id="5caba-156">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="5caba-157">如果您使用的連接字串，但是沒有 hello**管理**權限，設定`accessRights`太`listen`。</span><span class="sxs-lookup"><span data-stu-id="5caba-157">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="5caba-158">否則，hello 函式執行階段可能會失敗，嘗試 toodo 作業需要管理權限。</span><span class="sxs-lookup"><span data-stu-id="5caba-158">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="5caba-159">輸出使用方式</span><span class="sxs-lookup"><span data-stu-id="5caba-159">Output usage</span></span>
<span data-ttu-id="5caba-160">在 C# 和 F #，Azure 函式可以從任何下列類型的 hello 建立服務匯流排佇列訊息：</span><span class="sxs-lookup"><span data-stu-id="5caba-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of hello following types:</span></span>

* <span data-ttu-id="5caba-161">任何[物件](https://msdn.microsoft.com/library/system.object.aspx) - 參數定義看起來像 `out T paramName` (C#)。</span><span class="sxs-lookup"><span data-stu-id="5caba-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="5caba-162">函式會將 hello 物件還原序列化成 JSON 訊息。</span><span class="sxs-lookup"><span data-stu-id="5caba-162">Functions deserializes hello object into a JSON message.</span></span> <span data-ttu-id="5caba-163">如果 hello 函式結束時，hello 輸出值是 null，函式會建立 hello 訊息與 null 的物件。</span><span class="sxs-lookup"><span data-stu-id="5caba-163">If hello output value is null when hello function exits, Functions creates hello message with a null object.</span></span>
* <span data-ttu-id="5caba-164">`string` - 參數定義看起來像 `out string paraName` (C#)。</span><span class="sxs-lookup"><span data-stu-id="5caba-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="5caba-165">Hello 參數值為非 null hello 函式結束時，如果函式會建立訊息。</span><span class="sxs-lookup"><span data-stu-id="5caba-165">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="5caba-166">`byte[]` - 參數定義看起來像 `out byte[] paraName` (C#)。</span><span class="sxs-lookup"><span data-stu-id="5caba-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="5caba-167">Hello 參數值為非 null hello 函式結束時，如果函式會建立訊息。</span><span class="sxs-lookup"><span data-stu-id="5caba-167">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="5caba-168">`BrokeredMessage` - 參數定義看起來像 `out BrokeredMessage paraName` (C#)。</span><span class="sxs-lookup"><span data-stu-id="5caba-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="5caba-169">Hello 參數值為非 null hello 函式結束時，如果函式會建立訊息。</span><span class="sxs-lookup"><span data-stu-id="5caba-169">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>

<span data-ttu-id="5caba-170">若要在 C# 函式中建立多個訊息，您可以使用 `ICollector<T>` 或 `IAsyncCollector<T>`。</span><span class="sxs-lookup"><span data-stu-id="5caba-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="5caba-171">當您呼叫 hello 時，會建立訊息`Add`方法。</span><span class="sxs-lookup"><span data-stu-id="5caba-171">A message is created when you call hello `Add` method.</span></span>

<span data-ttu-id="5caba-172">在 Node.js，您可以指定字串、 位元組陣列或 Javascript 物件 （還原序列化為 JSON） 太`context.binding.<paramName>`。</span><span class="sxs-lookup"><span data-stu-id="5caba-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) too`context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="5caba-173">輸出範例</span><span class="sxs-lookup"><span data-stu-id="5caba-173">Output sample</span></span>
<span data-ttu-id="5caba-174">假設您有下列 function.json 定義服務匯流排佇列輸出 hello:</span><span class="sxs-lookup"><span data-stu-id="5caba-174">Suppose you have hello following function.json, that defines a Service Bus queue output:</span></span>

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

<span data-ttu-id="5caba-175">請參閱 hello 傳送訊息 toohello 服務匯流排佇列的特定語言的範例。</span><span class="sxs-lookup"><span data-stu-id="5caba-175">See hello language-specific sample that sends a message toohello service bus queue.</span></span>

* [<span data-ttu-id="5caba-176">C#</span><span class="sxs-lookup"><span data-stu-id="5caba-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="5caba-177">F#</span><span class="sxs-lookup"><span data-stu-id="5caba-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="5caba-178">Node.js</span><span class="sxs-lookup"><span data-stu-id="5caba-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="5caba-179">C# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="5caba-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="5caba-180">或者，toocreate 多則訊息：</span><span class="sxs-lookup"><span data-stu-id="5caba-180">Or, toocreate multiple messages:</span></span>

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, ICollector<string> outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue.Add("1 " + message);
    outputSbQueue.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="5caba-181">F# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="5caba-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="5caba-182">Node.js 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="5caba-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="5caba-183">或者，toocreate 多則訊息：</span><span class="sxs-lookup"><span data-stu-id="5caba-183">Or, toocreate multiple messages:</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = [];
    context.bindings.outputSbQueueMsg.push("1 " + message);
    context.bindings.outputSbQueueMsg.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="5caba-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5caba-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

