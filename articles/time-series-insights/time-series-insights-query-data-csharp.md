---
title: "從使用 C# 的 Azure 時間數列 Insights 環境的 hello aaaQuery 資料 |Microsoft 文件"
description: "本教學課程涵蓋了如何從 tooquery 資料 hello 時間數列 Insights 環境中使用 C# 範例程式碼。"
keywords: 
services: tsi
documentationcenter: 
author: ankryach
manager: jhubbard
editor: 
ms.assetid: 
ms.service: tsi
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: ankryach
ms.openlocfilehash: 0ddec36b7f275f6de279948193e45f045d30b644
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="query-data-from-hello-azure-time-series-insights-environment-using-c"></a><span data-ttu-id="fab1c-103">查詢資料從使用 C# hello Azure 時間數列 Insights 環境</span><span class="sxs-lookup"><span data-stu-id="fab1c-103">Query data from hello Azure Time Series Insights environment using C#</span></span>

<span data-ttu-id="fab1c-104">此 C# 範例會示範如何從 tooquery 資料 hello Azure 時間數列 Insights 環境。</span><span class="sxs-lookup"><span data-stu-id="fab1c-104">This C# example demonstrates how tooquery data from hello Azure Time Series Insights environment.</span></span>
<span data-ttu-id="fab1c-105">hello 範例示範數個基本查詢 API 使用範例：</span><span class="sxs-lookup"><span data-stu-id="fab1c-105">hello sample shows several basic examples of Query API usage:</span></span>
1. <span data-ttu-id="fab1c-106">在準備步驟中，取得 hello 存取權杖透過 hello Azure Active Directory API。</span><span class="sxs-lookup"><span data-stu-id="fab1c-106">As a preparation step, acquire hello access token through hello Azure Active Directory API.</span></span> <span data-ttu-id="fab1c-107">將此變數傳遞權杖 hello`Authorization`每個查詢 API 要求的標頭。</span><span class="sxs-lookup"><span data-stu-id="fab1c-107">Pass this token in hello `Authorization` header of every Query API request.</span></span> <span data-ttu-id="fab1c-108">若要了解如何設定非互動式應用程式，請參閱[驗證與授權](time-series-insights-authentication-and-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="fab1c-108">For setting up non-interactive applications, see [Authentication and authorization](time-series-insights-authentication-and-authorization.md).</span></span> <span data-ttu-id="fab1c-109">此外，請在 hello 開頭 hello 範例定義的所有 hello 常數均已正確都設定。</span><span class="sxs-lookup"><span data-stu-id="fab1c-109">Also, ensure all hello constants defined at hello beginning of hello sample are correctly set.</span></span>
2. <span data-ttu-id="fab1c-110">hello 使用者的環境的 hello 清單有存取 toois 取得。</span><span class="sxs-lookup"><span data-stu-id="fab1c-110">hello list of environments that hello user has access toois obtained.</span></span> <span data-ttu-id="fab1c-111">Hello 環境的其中一個是做為重要，hello 環境，且此環境中進一步查詢資料。</span><span class="sxs-lookup"><span data-stu-id="fab1c-111">One of hello environments is picked up as hello environment of interest, and further data is queried for this environment.</span></span>
3. <span data-ttu-id="fab1c-112">例如的 HTTPS 要求，要求可用性資料時感興趣的 hello 環境。</span><span class="sxs-lookup"><span data-stu-id="fab1c-112">As an example of HTTPS request, availability data is requested for hello environment of interest.</span></span>
4. <span data-ttu-id="fab1c-113">Web 通訊端要求的範例，為感興趣的 hello 環境要求事件彙總資料。</span><span class="sxs-lookup"><span data-stu-id="fab1c-113">As an example of web socket request, event aggregates data is requested for hello environment of interest.</span></span> <span data-ttu-id="fab1c-114">資料要求的 hello 整個可用性時間範圍。</span><span class="sxs-lookup"><span data-stu-id="fab1c-114">Data is requested for hello whole availability time range.</span></span>

## <a name="c-example"></a><span data-ttu-id="fab1c-115">C# 範例</span><span class="sxs-lookup"><span data-stu-id="fab1c-115">C# example</span></span>

```csharp
using System;
using System.Diagnostics;
using System.IO;
using System.Net;
using System.Net.WebSockets;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

namespace TimeSeriesInsightsQuerySample
{
    class Program
    {
        // For automated execution under application identity,
        // use application created in Active Directory.
        // toocreate hello application in AAD, follow hello steps provided here:
        // https://docs.microsoft.com/en-us/azure/time-series-insights/time-series-insights-authentication-and-authorization

        // SET hello application ID of application registered in your Azure Active Directory
        private static string ApplicationClientId = "#DUMMY#";

        // SET hello application key of hello application registered in your Azure Active Directory
        private static string ApplicationClientSecret = "#DUMMY#";

        // SET hello Azure Active Directory tenant.
        private static string Tenant = "#DUMMY#.onmicrosoft.com";

        public static async Task SampleAsync()
        {
            // 1. Acquire an access token.
            string accessToken = await AcquireAccessTokenAsync();

            // 2. Obtain list of environments and get environment FQDN for hello environment of interest.
            string environmentFqdn;
            {
                Uri uri = new UriBuilder("https", "api.timeseries.azure.com")
                {
                    Path = "environments",
                    Query = "api-version=2016-12-12"
                }.Uri;
                HttpWebRequest request = WebRequest.CreateHttp(uri);
                request.Method = "GET";
                request.Headers.Add("x-ms-client-application-name", "TimeSeriesInsightsQuerySample");
                request.Headers.Add("Authorization", "Bearer " + accessToken);

                using (WebResponse webResponse = await request.GetResponseAsync())
                using (var sr = new StreamReader(webResponse.GetResponseStream()))
                {
                    string responseJson = await sr.ReadToEndAsync();

                    JObject result = JsonConvert.DeserializeObject<JObject>(responseJson);
                    JArray environmentsList = (JArray)result["environments"];
                    if (environmentsList.Count == 0)
                    {
                        // List of user environments is empty, fallback toosample environment.
                        environmentFqdn = "10000000-0000-0000-0000-100000000108.env.timeseries.azure.com";
                    }
                    else
                    {
                        // Assume hello first environment is hello environment of interest.
                        JObject firstEnvironment = (JObject)environmentsList[0];
                        environmentFqdn = firstEnvironment["environmentFqdn"].Value<string>();
                    }
                }
            }
            Console.WriteLine("Using environment FQDN '{0}'", environmentFqdn);

            // 3. Obtain availability data for hello environment and get availability range.
            DateTime fromAvailabilityTimestamp;
            DateTime toAvailabilityTimestamp;
            {
                Uri uri = new UriBuilder("https", environmentFqdn)
                {
                    Path = "availability",
                    Query = "api-version=2016-12-12"
                }.Uri;
                HttpWebRequest request = WebRequest.CreateHttp(uri);
                request.Method = "GET";
                request.Headers.Add("x-ms-client-application-name", "TimeSeriesInsightsQuerySample");
                request.Headers.Add("Authorization", "Bearer " + accessToken);

                using (WebResponse webResponse = await request.GetResponseAsync())
                using (var sr = new StreamReader(webResponse.GetResponseStream()))
                {
                    string responseJson = await sr.ReadToEndAsync();

                    JObject result = JsonConvert.DeserializeObject<JObject>(responseJson);
                    JObject range = (JObject)result["range"];
                    fromAvailabilityTimestamp = range["from"].Value<DateTime>();
                    toAvailabilityTimestamp = range["to"].Value<DateTime>();
                }
            }
            Console.WriteLine(
                "Obtained availability range [{0}, {1}]",
                fromAvailabilityTimestamp,
                toAvailabilityTimestamp);

            // 4. Get aggregates for hello environment:
            //    group by Event Source Name and calculate number of events in each group.
            {
                // Assume data for hello whole availablility range is requested.
                DateTime from = fromAvailabilityTimestamp;
                DateTime too= toAvailabilityTimestamp;

                JObject inputPayload = new JObject(
                    // Send HTTP headers as a part of hello message since .NET WebSocket does not support
                    // sending custom headers on HTTP GET upgrade request tooWebSocket protocol request.
                    new JProperty("headers", new JObject(
                        new JProperty("x-ms-client-application-name", "TimeSeriesInsightsQuerySample"),
                        new JProperty("Authorization", "Bearer " + accessToken))),
                    new JProperty("content", new JObject(
                        new JProperty("aggregates", new JArray(new JObject(
                            new JProperty("dimension", new JObject(
                                new JProperty("uniqueValues", new JObject(
                                    new JProperty("input", new JObject(
                                        new JProperty("builtInProperty", "$esn"))),
                                    new JProperty("take", 1000))))),
                            new JProperty("measures", new JArray(new JObject(
                                new JProperty("count", new JObject()))))))),
                        new JProperty("searchSpan", new JObject(
                            new JProperty("from", from),
                            new JProperty("to", to))))));

                var webSocket = new ClientWebSocket();

                // Establish web socket connection.
                Uri uri = new UriBuilder("wss", environmentFqdn)
                {
                    Path = "aggregates",
                    Query = "api-version=2016-12-12"
                }.Uri;
                await webSocket.ConnectAsync(uri, CancellationToken.None);

                // Send input payload.
                byte[] inputPayloadBytes = Encoding.UTF8.GetBytes(inputPayload.ToString());
                await webSocket.SendAsync(
                    new ArraySegment<byte>(inputPayloadBytes),
                    WebSocketMessageType.Text,
                    endOfMessage: true,
                    cancellationToken: CancellationToken.None);

                // Read response messages from web socket.
                JObject responseContent = null;
                using (webSocket)
                {
                    while (true)
                    {
                        string message;
                        using (var ms = new MemoryStream())
                        {
                            // Write from socket toomemory stream.
                            const int bufferSize = 16 * 1024;
                            var temporaryBuffer = new byte[bufferSize];
                            while (true)
                            {
                                WebSocketReceiveResult response = await webSocket.ReceiveAsync(
                                    new ArraySegment<byte>(temporaryBuffer),
                                    CancellationToken.None);

                                ms.Write(temporaryBuffer, 0, response.Count);
                                if (response.EndOfMessage)
                                {
                                    break;
                                }
                            }

                            // Reset position toohello beginning tooallow reads.
                            ms.Position = 0;

                            using (var sr = new StreamReader(ms))
                            {
                                message = sr.ReadToEnd();
                            }
                        }

                        JObject messageObj = JsonConvert.DeserializeObject<JObject>(message);

                        // Stop reading if error is emitted.
                        if (messageObj["error"] != null)
                        {
                            break;
                        }

                        // Number of items corresponds toonumber of aggregates in input payload
                        JArray currentContents = (JArray)messageObj["content"];

                        // In this sample list of aggregates in input payload contains
                        // only 1 item since request contains 1 aggregate.
                        responseContent = (JObject)currentContents[0];

                        // Stop reading if 100% of completeness is reached.
                        if (messageObj["percentCompleted"] != null &&
                            Math.Abs((double)messageObj["percentCompleted"] - 100d) < 0.01)
                        {
                            break;
                        }
                    }

                    // Close web socket connection.
                    if (webSocket.State == WebSocketState.Open)
                    {
                        await webSocket.CloseAsync(
                            WebSocketCloseStatus.NormalClosure,
                            "CompletedByClient",
                            CancellationToken.None);
                    }
                }

                Console.WriteLine("Dimension Value\t\tCount");
                JArray dimensionValues = (JArray)responseContent["dimension"];
                JArray measures = (JArray)responseContent["measures"];
                Debug.Assert(
                    dimensionValues.Count == measures.Count,
                    "Number of measures and dimensions should match.");
                for (int i = 0; i < dimensionValues.Count; i++)
                {
                    string currentDimensionValue = (string)dimensionValues[i];
                    JArray currentMeasureValues = (JArray)measures[i];
                    double currentCount = (double)currentMeasureValues[0];

                    Console.WriteLine("{0}\t\t{1}", currentDimensionValue, currentCount);
                }
            }
        }

        private static async Task<string> AcquireAccessTokenAsync()
        {
            if (ApplicationClientId == "#DUMMY#" || ApplicationClientSecret == "#DUMMY#" || Tenant.StartsWith("#DUMMY#"))
            {
                throw new Exception(
                    $"Use hello link {"https://docs.microsoft.com/en-us/azure/time-series-insights/time-series-insights-authentication-and-authorization"} tooupdate hello values of 'ApplicationClientId', 'ApplicationClientSecret' and 'Tenant'.");
            }

            var authenticationContext = new AuthenticationContext(
                $"https://login.windows.net/{Tenant}",
                TokenCache.DefaultShared);

            AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
                resource: "https://api.timeseries.azure.com/",
                clientCredential: new ClientCredential(
                    clientId: ApplicationClientId,
                    clientSecret: ApplicationClientSecret));

            // Show interactive logon dialog tooacquire token on behalf of hello user.
            // Suitable for native apps, and not on server-side of a web application.
            //AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
            //    resource: "https://api.timeseries.azure.com/",
            //    // Set well-known client ID for Azure PowerShell
            //    clientId: "1950a258-227b-4e31-a9cf-717495945fc2",
            //    // Set redirect URI for Azure PowerShell
            //    redirectUri: new Uri("urn:ietf:wg:oauth:2.0:oob"),
            //    parameters: new PlatformParameters(PromptBehavior.Auto));

            return token.AccessToken;
        }

        static void Main(string[] args)
        {
            Task.Run(async () => await SampleAsync()).Wait();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="fab1c-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fab1c-116">Next steps</span></span>

<span data-ttu-id="fab1c-117">如需完整查詢 API 參考 hello，請參閱 hello[查詢 API](/rest/api/time-series-insights/time-series-insights-reference-queryapi)文件。</span><span class="sxs-lookup"><span data-stu-id="fab1c-117">For hello full Query API reference, see hello [Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) document.</span></span>
