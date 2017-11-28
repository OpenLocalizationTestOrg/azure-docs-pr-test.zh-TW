---
title: "hello Azure 轉送.NET 標準 Api 的 aaaOverview |Microsoft 文件"
description: "轉送 .NET Standard API 概觀"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b1da9ac1-811b-4df7-a22c-ccd013405c40
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: c90e00e809bd44eb0fbbff5eb03dfc8afa486523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="89ec6-103">Azure 轉送混合式連線 .NET Standard API 概觀</span><span class="sxs-lookup"><span data-stu-id="89ec6-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="89ec6-104">本文摘要說明一些 Azure 轉送混合式連線.NET 標準 hello 金鑰[用戶端應用程式開發介面](/dotnet/api/microsoft.azure.relay)。</span><span class="sxs-lookup"><span data-stu-id="89ec6-104">This article summarizes some of hello key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="89ec6-105">轉送連接字串產生器</span><span class="sxs-lookup"><span data-stu-id="89ec6-105">Relay Connection String Builder</span></span>

<span data-ttu-id="89ec6-106">hello [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder]類別格式都是特定 tooRelay 混合式連接的連接字串。</span><span class="sxs-lookup"><span data-stu-id="89ec6-106">hello [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific tooRelay Hybrid Connections.</span></span> <span data-ttu-id="89ec6-107">您可以使用連接字串或從可用的連接字串 toobuild tooverify hello 的格式。</span><span class="sxs-lookup"><span data-stu-id="89ec6-107">You can use it tooverify hello format of a connection string, or toobuild a connection string from scratch.</span></span> <span data-ttu-id="89ec6-108">請參閱下列範例程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="89ec6-108">See hello following code for an example:</span></span>

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of hello Hybrid Connection}";
var sharedAccessKeyName = "{SAS key name}";
var sharedAccessKey = "{SAS key value}";

var connectionStringBuilder = new RelayConnectionStringBuilder()
{
    Endpoint = endpoint,
    EntityPath = entityPath,
    SharedAccessKeyName = sasKeyName,
    SharedAccessKey = sasKeyValue
};
```

<span data-ttu-id="89ec6-109">您也可以傳遞連接字串直接 toohello`RelayConnectionStringBuilder`方法。</span><span class="sxs-lookup"><span data-stu-id="89ec6-109">You can also pass a connection string directly toohello `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="89ec6-110">這項作業可讓您 tooverify hello 連接字串為有效的格式。</span><span class="sxs-lookup"><span data-stu-id="89ec6-110">This operation enables you tooverify that hello connection string is in a valid format.</span></span> <span data-ttu-id="89ec6-111">如果任何 hello 參數無效，hello 建構函式會產生`ArgumentException`。</span><span class="sxs-lookup"><span data-stu-id="89ec6-111">If any of hello parameters are invalid, hello constructor generates an `ArgumentException`.</span></span>

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare hello connectionStringBuilder so that it can be used outside of hello loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create hello connectionStringBuilder using hello supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a><span data-ttu-id="89ec6-112">混合式連線串流</span><span class="sxs-lookup"><span data-stu-id="89ec6-112">Hybrid Connection Stream</span></span>
<span data-ttu-id="89ec6-113">hello [HybridConnectionStream] [ HCStream]類別是 hello 用的主要物件 toosend，而且從 Azure 轉送端點，接收資料，是否正在使用[HybridConnectionClient][ HCClient]，或[HybridConnectionListener][HCListener]。</span><span class="sxs-lookup"><span data-stu-id="89ec6-113">hello [HybridConnectionStream][HCStream] class is hello primary object used toosend and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="89ec6-114">取得混合式連線串流</span><span class="sxs-lookup"><span data-stu-id="89ec6-114">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="89ec6-115">接聽程式</span><span class="sxs-lookup"><span data-stu-id="89ec6-115">Listener</span></span>
<span data-ttu-id="89ec6-116">使用 [HybridConnectionListener][HCListener]，您可以取得如下的 `HybridConnectionStream` 物件︰</span><span class="sxs-lookup"><span data-stu-id="89ec6-116">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="89ec6-117">用戶端</span><span class="sxs-lookup"><span data-stu-id="89ec6-117">Client</span></span>
<span data-ttu-id="89ec6-118">使用 [HybridConnectionClient][HCClient]，您可以取得如下的 `HybridConnectionStream` 物件︰</span><span class="sxs-lookup"><span data-stu-id="89ec6-118">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="89ec6-119">接收資料</span><span class="sxs-lookup"><span data-stu-id="89ec6-119">Receiving data</span></span>
<span data-ttu-id="89ec6-120">hello [HybridConnectionStream] [ HCStream]類別可讓雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="89ec6-120">hello [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="89ec6-121">在大部分情況下，您持續收到 hello 資料流。</span><span class="sxs-lookup"><span data-stu-id="89ec6-121">In most cases, you continuously receive from hello stream.</span></span> <span data-ttu-id="89ec6-122">如果您從 hello 資料流讀取的文字，您也可以 toouse [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx)物件，可讓您更容易剖析 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="89ec6-122">If you are reading text from hello stream, you may also want toouse a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of hello data.</span></span> <span data-ttu-id="89ec6-123">例如，您可以讀取文字 (而非`byte[]`) 格式的資料。</span><span class="sxs-lookup"><span data-stu-id="89ec6-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="89ec6-124">hello 下列程式碼會讀取個別的文字行 hello 資料流之前已要求取消：</span><span class="sxs-lookup"><span data-stu-id="89ec6-124">hello following code reads individual lines of text from hello stream until a cancellation is requested:</span></span>

```csharp
// Create a CancellationToken, so that we can cancel hello while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from hello 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of hello processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a><span data-ttu-id="89ec6-125">傳送資料</span><span class="sxs-lookup"><span data-stu-id="89ec6-125">Sending data</span></span>
<span data-ttu-id="89ec6-126">建立連接之後，您可以傳送訊息 toohello 轉送端點。</span><span class="sxs-lookup"><span data-stu-id="89ec6-126">Once you have a connection established, you can send a message toohello Relay endpoint.</span></span> <span data-ttu-id="89ec6-127">因為 hello 連線物件會繼承[資料流](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx)，傳送資料做為`byte[]`。</span><span class="sxs-lookup"><span data-stu-id="89ec6-127">Because hello connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="89ec6-128">下列範例會示範如何 hello toodo 這樣：</span><span class="sxs-lookup"><span data-stu-id="89ec6-128">hello following example shows how toodo this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="89ec6-129">不過，如果您想要 toosend 文字直接管理，而不需要 tooencode hello 字串每個階段中，則可以包裝 hello`hybridConnectionStream`物件[StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx)物件。</span><span class="sxs-lookup"><span data-stu-id="89ec6-129">However, if you want toosend text directly, without needing tooencode hello string each time, you can wrap hello `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="89ec6-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="89ec6-130">Next steps</span></span>
<span data-ttu-id="89ec6-131">toolearn 深入了解 Azure 轉送，請前往下列連結：</span><span class="sxs-lookup"><span data-stu-id="89ec6-131">toolearn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="89ec6-132">Microsoft.Azure.Relay reference</span><span class="sxs-lookup"><span data-stu-id="89ec6-132">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="89ec6-133">什麼是 Azure 轉送？</span><span class="sxs-lookup"><span data-stu-id="89ec6-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="89ec6-134">可用的轉送 API</span><span class="sxs-lookup"><span data-stu-id="89ec6-134">Available Relay APIs</span></span>](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener