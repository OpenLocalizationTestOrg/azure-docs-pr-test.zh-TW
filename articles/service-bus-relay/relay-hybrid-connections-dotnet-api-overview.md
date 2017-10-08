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
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a>Azure 轉送混合式連線 .NET Standard API 概觀

本文摘要說明一些 Azure 轉送混合式連線.NET 標準 hello 金鑰[用戶端應用程式開發介面](/dotnet/api/microsoft.azure.relay)。
  
## <a name="relay-connection-string-builder"></a>轉送連接字串產生器

hello [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder]類別格式都是特定 tooRelay 混合式連接的連接字串。 您可以使用連接字串或從可用的連接字串 toobuild tooverify hello 的格式。 請參閱下列範例程式碼的 hello:

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

您也可以傳遞連接字串直接 toohello`RelayConnectionStringBuilder`方法。 這項作業可讓您 tooverify hello 連接字串為有效的格式。 如果任何 hello 參數無效，hello 建構函式會產生`ArgumentException`。

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

## <a name="hybrid-connection-stream"></a>混合式連線串流
hello [HybridConnectionStream] [ HCStream]類別是 hello 用的主要物件 toosend，而且從 Azure 轉送端點，接收資料，是否正在使用[HybridConnectionClient][ HCClient]，或[HybridConnectionListener][HCListener]。

### <a name="getting-a-hybrid-connection-stream"></a>取得混合式連線串流

#### <a name="listener"></a>接聽程式
使用 [HybridConnectionListener][HCListener]，您可以取得如下的 `HybridConnectionStream` 物件︰

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a>用戶端
使用 [HybridConnectionClient][HCClient]，您可以取得如下的 `HybridConnectionStream` 物件︰

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a>接收資料
hello [HybridConnectionStream] [ HCStream]類別可讓雙向通訊。 在大部分情況下，您持續收到 hello 資料流。 如果您從 hello 資料流讀取的文字，您也可以 toouse [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx)物件，可讓您更容易剖析 hello 資料。 例如，您可以讀取文字 (而非`byte[]`) 格式的資料。

hello 下列程式碼會讀取個別的文字行 hello 資料流之前已要求取消：

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

### <a name="sending-data"></a>傳送資料
建立連接之後，您可以傳送訊息 toohello 轉送端點。 因為 hello 連線物件會繼承[資料流](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx)，傳送資料做為`byte[]`。 下列範例會示範如何 hello toodo 這樣：

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

不過，如果您想要 toosend 文字直接管理，而不需要 tooencode hello 字串每個階段中，則可以包裝 hello`hybridConnectionStream`物件[StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx)物件。

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a>後續步驟
toolearn 深入了解 Azure 轉送，請前往下列連結：

* [Microsoft.Azure.Relay reference](/dotnet/api/microsoft.azure.relay)
* [什麼是 Azure 轉送？](relay-what-is-it.md)
* [可用的轉送 API](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener