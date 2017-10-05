---
title: "使用 API 偵測器追蹤呼叫 - Azure API Management | Microsoft Docs"
description: "了解如何在 Azure API 管理中使用 API 偵測器來追蹤呼叫。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 4b222327-c8a4-4f33-9a06-adff2a9834d9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a9d4d3be7f046af975f6dc25670070204848588c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-api-inspector-to-trace-calls-in-azure-api-management"></a><span data-ttu-id="5e5eb-103">如何在 Azure API 管理中使用 API 偵測器來追蹤呼叫</span><span class="sxs-lookup"><span data-stu-id="5e5eb-103">How to use the API Inspector to trace calls in Azure API Management</span></span>
<span data-ttu-id="5e5eb-104">API 管理提供 API 偵測器工具協助您進行 API 的偵錯和疑難排解。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-104">API Management provides an API Inspector tool to help you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="5e5eb-105">API 偵測器可以程式設計的方式使用，也可以直接從開發人員入口網站使用。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-105">The API Inspector can be used programmatically and can also be used directly from the developer portal.</span></span> 

<span data-ttu-id="5e5eb-106">除了追蹤作業，API 偵測器也會追蹤 [原則運算式](https://msdn.microsoft.com/library/azure/dn910913.aspx) 評估。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-106">In addition to tracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="5e5eb-107">如需示範，請參閱 [雲端報導第 177 集：更多 API 管理功能](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ，並向前快轉到 21:00。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 21:00.</span></span>

<span data-ttu-id="5e5eb-108">本指南提供使用 API 偵測器的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="5e5eb-109">只有當要求包含屬於 [系統管理員](api-management-howto-create-groups.md) 的訂用帳戶金鑰，才會產生其 API 偵測器追蹤並提供使用。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong to the [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="5e5eb-110"><a name="trace-call"> </a> 使用 API 偵測器來追蹤呼叫</span><span class="sxs-lookup"><span data-stu-id="5e5eb-110"><a name="trace-call"> </a> Use API Inspector to trace a call</span></span>
<span data-ttu-id="5e5eb-111">若要使用 API 偵測器，請將 **ocp-apim-trace: true** 要求標頭新增至作業呼叫，然後使用 **ocp-apim-trace-location** 回應標頭所指出的 URL 來下載並檢查追蹤。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-111">To use API Inspector, add an **ocp-apim-trace: true** request header to your operation call, and then download and inspect the trace using the URL indicated by the **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="5e5eb-112">這可以透過程式設計來進行，也可以直接從開發人員入口網站來執行。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-112">This can be done programatically, and can also be done directly from the developer portal.</span></span>

<span data-ttu-id="5e5eb-113">本教學課程示範如何使用 API 偵測器來追蹤作業，方法是使用 [管理您的第一個 API](api-management-get-started.md) 入門教學課程中設定的基本計算機 API。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-113">This tutorial shows how to use the API Inspector to trace operations using the Basic Calculator API that is configured in the [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="5e5eb-114">如果您尚未完成該教學課程，匯入基本計算機 API 只需要幾分鐘的時間，或可以使用您選擇的另一個 API (例如 Echo API)。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-114">If you haven't completed that tutorial it only takes a few moments to import the Basic Calculator API, or you can use another API of your choosing such as the Echo API.</span></span> <span data-ttu-id="5e5eb-115">每個 API 管理服務執行個體隨附預先設定的範例 Echo API，可供您試驗與了解 API 管理。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-115">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="5e5eb-116">Echo API 會將任何傳送給它的輸入傳回。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-116">The Echo API returns back whatever input is sent to it.</span></span> <span data-ttu-id="5e5eb-117">若要使用該 API，您可以叫用任何 HTTP 指令動詞，而傳回值就是您傳送的值。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-117">To use it, you can invoke any HTTP verb, and the return value will simply be what you sent.</span></span> 

<span data-ttu-id="5e5eb-118">若要開始進行，請在您「API 管理」服務的「Azure 入口網站」中按一下 [開發人員入口網站]。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-118">To get started, click **Developer portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="5e5eb-119">您可以從開發人員入口網站直接呼叫作業，以便檢視和測試 API 的操作。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-119">Operations can be called directly from the developer portal which provides a convenient way to view and test the operations of an API.</span></span>

> <span data-ttu-id="5e5eb-120">如果您尚未建立 API 管理服務執行個體，請參閱[開始使用 Azure API 管理][Get started with Azure API Management]教學課程中的[建立 API 管理服務執行個體][Create an API Management service instance]。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![API Management developer portal][api-management-developer-portal-menu]

<span data-ttu-id="5e5eb-122">從上方功能表中按一下 [API]，然後按一下 [基本計算機]。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-122">Click **APIs** from the top menu, and then click **Basic Calculator**.</span></span>

![Echo API][api-management-api]

<span data-ttu-id="5e5eb-124">按一下 [試試看] 來嘗試 [新增兩個整數] 作業。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-124">Click **Try it** to try the **Add two integers** operation.</span></span>

![試試看][api-management-open-console]

<span data-ttu-id="5e5eb-126">保留預設的參數值，然後從 **subscription-key** 下拉式清單選取您想要使用的產品的訂閱金鑰。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-126">Keep the default parameter values, and select the subscription key for the product you want to use from the **subscription-key** drop-down.</span></span>

<span data-ttu-id="5e5eb-127">根據預設，開發人員入口網站中已將 **Ocp-Apim-Trace** 標頭設為 **true**。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-127">By default in the developer portal the **Ocp-Apim-Trace** header is already set to **true**.</span></span> <span data-ttu-id="5e5eb-128">此標頭會設定是否產生追蹤。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-128">This header configures whether or not a trace is generated.</span></span>

![傳送][api-management-http-get]

<span data-ttu-id="5e5eb-130">按一下 [ **傳送** ] 來叫用作業。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-130">Click **Send** to invoke the operation.</span></span>

![傳送][api-management-send-results]

<span data-ttu-id="5e5eb-132">在回應標頭中，將會有一個 **ocp-apim-trace-location** ，且值類似下列範例。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-132">In the response headers will be an **ocp-apim-trace-location** with a value similar to the following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="5e5eb-133">可從指定的位置下載追蹤來檢閱，如下一個步驟所示。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-133">The trace can be downloaded from the specified location and reviewed as demonstrated in the next step.</span></span> <span data-ttu-id="5e5eb-134">請注意，系統只會儲存最後 100 個記錄項目，並且會循環重複使用記錄位置。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-134">Note that only the last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="5e5eb-135">因此，如果您在啟用追蹤功能的情況下進行超過 100 次呼叫，最後就會開始就地覆寫前幾個追蹤。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting the first traces in place.</span></span>

## <span data-ttu-id="5e5eb-136"><a name="inspect-trace"> </a>檢查追蹤</span><span class="sxs-lookup"><span data-stu-id="5e5eb-136"><a name="inspect-trace"> </a>Inspect the trace</span></span>
<span data-ttu-id="5e5eb-137">若要檢閱追蹤裡的值，請從 **ocp-apim-trace-location** URL 下載追蹤檔案。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-137">To review the values in the trace, download the trace file from the **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="5e5eb-138">它是一個 JSON 格式的文字檔，且包含類似下列範例的項目。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-138">It is a text file in JSON format, and contains entries similar to the following example.</span></span>

```json
{
    "traceId": "abcd8ea63d134c1fabe6371566c7cbea",
    "traceEntries": {
        "inbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0725926",
                "data": {
                    "request": {
                        "method": "GET",
                        "url": "https://contoso5.azure-api.net/calc/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "Connection",
                                "value": "Keep-Alive"
                            },
                            {
                                "name": "Host",
                                "value": "contoso5.azure-api.net"
                            }
                        ]
                    }
                }
            },
            {
                "source": "mapper",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0726213",
                "data": {
                    "configuration": {
                        "api": {
                            "from": "/calc",
                            "to": {
                                "scheme": "http",
                                "host": "calcapi.cloudapp.net",
                                "port": 80,
                                "path": "/api",
                                "queryString": "",
                                "query": {},
                                "isDefaultPort": true
                            }
                        },
                        "operation": {
                            "method": "GET",
                            "uriTemplate": "/add?a={a}&b={b}"
                        },
                        "user": {
                            "id": 1,
                            "groups": [
                                "Administrators",
                                "Developers"
                            ]
                        },
                        "product": {
                            "id": 1
                        }
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0727522",
                "data": {
                    "message": "Request is being forwarded to the backend service.",
                    "request": {
                        "method": "GET",
                        "url": "http://calcapi.cloudapp.net/api/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "X-Forwarded-For",
                                "value": "33.52.215.35"
                            }
                        ]
                    }
                }
            }
        ],
        "outbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1960601",
                "data": {
                    "response": {
                        "status": {
                            "code": 200,
                            "reason": "OK"
                        },
                        "headers": [
                            {
                                "name": "Pragma",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Length",
                                "value": "124"
                            },
                            {
                                "name": "Cache-Control",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Type",
                                "value": "application/xml; charset=utf-8"
                            },
                            {
                                "name": "Date",
                                "value": "Tue, 23 Jun 2015 19:51:35 GMT"
                            },
                            {
                                "name": "Expires",
                                "value": "-1"
                            },
                            {
                                "name": "Server",
                                "value": "Microsoft-IIS/8.5"
                            },
                            {
                                "name": "X-AspNet-Version",
                                "value": "4.0.30319"
                            },
                            {
                                "name": "X-Powered-By",
                                "value": "ASP.NET"
                            }
                        ]
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1961112",
                "data": {
                    "message": "Response headers have been sent to the caller. Starting to stream the response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming to the caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="5e5eb-139"><a name="next-steps"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e5eb-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="5e5eb-140">請觀看 [雲端報導第 177 集：更多 API 管理功能](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)中追蹤原則運算式的示範。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="5e5eb-141">向前快轉到 21:00 來查看示範。</span><span class="sxs-lookup"><span data-stu-id="5e5eb-141">Fast-forward to 21:00 to see the demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector to trace a call]: #trace-call
[Inspect the trace]: #inspect-trace
[Next steps]: #next-steps

[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Azure Classic Portal]: https://manage.windowsazure.com/


[api-management-developer-portal-menu]: ./media/api-management-howto-api-inspector/api-management-developer-portal-menu.png
[api-management-api]: ./media/api-management-howto-api-inspector/api-management-api.png
[api-management-echo-api-get]: ./media/api-management-howto-api-inspector/api-management-echo-api-get.png
[api-management-developer-key]: ./media/api-management-howto-api-inspector/api-management-developer-key.png
[api-management-open-console]: ./media/api-management-howto-api-inspector/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-api-inspector/api-management-http-get.png
[api-management-send-results]: ./media/api-management-howto-api-inspector/api-management-send-results.png




