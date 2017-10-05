---
title: "Azure 轉送 .NET Standard API 概觀 | Microsoft Docs"
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
ms.openlocfilehash: f3f4a2e721b1a75a5b92a5c17a9939c7013340d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="07f38-103">Azure 轉送混合式連線 .NET Standard API 概觀</span><span class="sxs-lookup"><span data-stu-id="07f38-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="07f38-104">本文將摘要列出一些主要 Azure 轉送混合式連線 .NET Standard [用戶端 API](/dotnet/api/microsoft.azure.relay)。</span><span class="sxs-lookup"><span data-stu-id="07f38-104">This article summarizes some of the key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="07f38-105">轉送連接字串產生器</span><span class="sxs-lookup"><span data-stu-id="07f38-105">Relay Connection String Builder</span></span>

<span data-ttu-id="07f38-106">[RelayConnectionStringBuilder][RelayConnectionStringBuilder] 類別會格式化專用於轉送混合式連線的連接字串。</span><span class="sxs-lookup"><span data-stu-id="07f38-106">The [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific to Relay Hybrid Connections.</span></span> <span data-ttu-id="07f38-107">您可以使用它來驗證連接字串的格式，或從頭開始建置連接字串。</span><span class="sxs-lookup"><span data-stu-id="07f38-107">You can use it to verify the format of a connection string, or to build a connection string from scratch.</span></span> <span data-ttu-id="07f38-108">如需範例，請參閱下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="07f38-108">See the following code for an example:</span></span>

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of the Hybrid Connection}";
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

<span data-ttu-id="07f38-109">您也可以直接將連接字串傳遞到 `RelayConnectionStringBuilder` 方法。</span><span class="sxs-lookup"><span data-stu-id="07f38-109">You can also pass a connection string directly to the `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="07f38-110">這項作業可讓您確認連接字串格式有效。</span><span class="sxs-lookup"><span data-stu-id="07f38-110">This operation enables you to verify that the connection string is in a valid format.</span></span> <span data-ttu-id="07f38-111">如果有任何參數無效，建構函式會產生 `ArgumentException`。</span><span class="sxs-lookup"><span data-stu-id="07f38-111">If any of the parameters are invalid, the constructor generates an `ArgumentException`.</span></span>

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare the connectionStringBuilder so that it can be used outside of the loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create the connectionStringBuilder using the supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a><span data-ttu-id="07f38-112">混合式連線串流</span><span class="sxs-lookup"><span data-stu-id="07f38-112">Hybrid Connection Stream</span></span>
<span data-ttu-id="07f38-113">無論您使用的是 [HybridConnectionClient][HCClient] 或 [HybridConnectionListener][HCListener]，[HybridConnectionStream][HCStream] 類別都是用來傳送和接收 Azure 轉送端點之資料的主要物件。</span><span class="sxs-lookup"><span data-stu-id="07f38-113">The [HybridConnectionStream][HCStream] class is the primary object used to send and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="07f38-114">取得混合式連線串流</span><span class="sxs-lookup"><span data-stu-id="07f38-114">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="07f38-115">接聽程式</span><span class="sxs-lookup"><span data-stu-id="07f38-115">Listener</span></span>
<span data-ttu-id="07f38-116">使用 [HybridConnectionListener][HCListener]，您可以取得如下的 `HybridConnectionStream` 物件︰</span><span class="sxs-lookup"><span data-stu-id="07f38-116">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection to the Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="07f38-117">用戶端</span><span class="sxs-lookup"><span data-stu-id="07f38-117">Client</span></span>
<span data-ttu-id="07f38-118">使用 [HybridConnectionClient][HCClient]，您可以取得如下的 `HybridConnectionStream` 物件︰</span><span class="sxs-lookup"><span data-stu-id="07f38-118">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection to the Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="07f38-119">接收資料</span><span class="sxs-lookup"><span data-stu-id="07f38-119">Receiving data</span></span>
<span data-ttu-id="07f38-120">[HybridConnectionStream][HCStream] 類別允許雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="07f38-120">The [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="07f38-121">在大部分的案例中，您會持續接收來自串流的資料。</span><span class="sxs-lookup"><span data-stu-id="07f38-121">In most cases, you continuously receive from the stream.</span></span> <span data-ttu-id="07f38-122">如果您從串流讀取文字，建議您使用 [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) 物件，這可讓您更容易剖析資料。</span><span class="sxs-lookup"><span data-stu-id="07f38-122">If you are reading text from the stream, you may also want to use a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of the data.</span></span> <span data-ttu-id="07f38-123">例如，您可以讀取文字 (而非`byte[]`) 格式的資料。</span><span class="sxs-lookup"><span data-stu-id="07f38-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="07f38-124">下列程式碼會從串流讀取個別的文字行，直到要求取消：</span><span class="sxs-lookup"><span data-stu-id="07f38-124">The following code reads individual lines of text from the stream until a cancellation is requested:</span></span>

```csharp
// Create a CancellationToken, so that we can cancel the while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from the 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of the processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a><span data-ttu-id="07f38-125">傳送資料</span><span class="sxs-lookup"><span data-stu-id="07f38-125">Sending data</span></span>
<span data-ttu-id="07f38-126">一旦建立連線，您可以傳送訊息到轉送端點。</span><span class="sxs-lookup"><span data-stu-id="07f38-126">Once you have a connection established, you can send a message to the Relay endpoint.</span></span> <span data-ttu-id="07f38-127">因為連線物件會繼承[串流](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx)，請傳送 `byte[]` 格式的資料。</span><span class="sxs-lookup"><span data-stu-id="07f38-127">Because the connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="07f38-128">下列範例示範如何執行：</span><span class="sxs-lookup"><span data-stu-id="07f38-128">The following example shows how to do this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="07f38-129">不過，如果您想要直接傳送文字，不需每次都將字串編碼，您可以使用 [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) 物件來包裝 `hybridConnectionStream` 物件。</span><span class="sxs-lookup"><span data-stu-id="07f38-129">However, if you want to send text directly, without needing to encode the string each time, you can wrap the `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// The StreamWriter object only needs to be created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="07f38-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="07f38-130">Next steps</span></span>
<span data-ttu-id="07f38-131">若要深入了解 Azure 轉送，請造訪下列連結：</span><span class="sxs-lookup"><span data-stu-id="07f38-131">To learn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="07f38-132">Microsoft.Azure.Relay reference</span><span class="sxs-lookup"><span data-stu-id="07f38-132">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="07f38-133">什麼是 Azure 轉送？</span><span class="sxs-lookup"><span data-stu-id="07f38-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="07f38-134">可用的轉送 API</span><span class="sxs-lookup"><span data-stu-id="07f38-134">Available Relay APIs</span></span>](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener