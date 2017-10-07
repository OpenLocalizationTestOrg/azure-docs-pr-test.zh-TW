---
title: "aaaTrace 呼叫 API inspector-Azure API 管理 |Microsoft 文件"
description: "了解如何使用 tootrace 呼叫 hello API 在 Azure API 管理中的偵測器。"
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
ms.openlocfilehash: b0c401caa8da1b789f6cfe5edf97a5f118d78f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a><span data-ttu-id="f3189-103">Toouse hello API Inspector tootrace 如何呼叫在 Azure API 管理</span><span class="sxs-lookup"><span data-stu-id="f3189-103">How toouse hello API Inspector tootrace calls in Azure API Management</span></span>
<span data-ttu-id="f3189-104">API 管理能夠讓應用程式開發介面 Inspector 工具 toohelp 您偵錯和疑難排解您的應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="f3189-104">API Management provides an API Inspector tool toohelp you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="f3189-105">hello API 偵測器可以用於以程式設計的方式，也可以直接從 hello 開發人員入口網站使用。</span><span class="sxs-lookup"><span data-stu-id="f3189-105">hello API Inspector can be used programmatically and can also be used directly from hello developer portal.</span></span> 

<span data-ttu-id="f3189-106">此外 tootracing 作業 API 偵測器也會追蹤[原則運算式](https://msdn.microsoft.com/library/azure/dn910913.aspx)評估。</span><span class="sxs-lookup"><span data-stu-id="f3189-106">In addition tootracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="f3189-107">如需示範，請參閱[雲端涵蓋的時段 177： 更 API 管理功能](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)和 too21:00 向前快轉。</span><span class="sxs-lookup"><span data-stu-id="f3189-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too21:00.</span></span>

<span data-ttu-id="f3189-108">本指南提供使用 API 偵測器的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="f3189-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="f3189-109">只產生並提供給要求包含屬於 toohello 訂閱索引鍵使用應用程式開發介面的偵測器追蹤[管理員](api-management-howto-create-groups.md)帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3189-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong toohello [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="f3189-110"><a name="trace-call"></a>使用 API Inspector tootrace 呼叫</span><span class="sxs-lookup"><span data-stu-id="f3189-110"><a name="trace-call"> </a> Use API Inspector tootrace a call</span></span>
<span data-ttu-id="f3189-111">toouse API Inspector 新增**ocp apim 追蹤： true**要求標頭 tooyour 作業呼叫，然後下載並檢查使用 hello URL 以 hello hello 追蹤**ocp apim-追蹤位置**回應標頭。</span><span class="sxs-lookup"><span data-stu-id="f3189-111">toouse API Inspector, add an **ocp-apim-trace: true** request header tooyour operation call, and then download and inspect hello trace using hello URL indicated by hello **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="f3189-112">這可以程式設計方式，完成，而且還可以直接從 hello 開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="f3189-112">This can be done programatically, and can also be done directly from hello developer portal.</span></span>

<span data-ttu-id="f3189-113">本教學課程示範如何使用 toouse hello API Inspector tootrace 作業 hello hello 中設定的基本計算機 API[管理您的第一個應用程式開發介面](api-management-get-started.md)快速入門教學課程。</span><span class="sxs-lookup"><span data-stu-id="f3189-113">This tutorial shows how toouse hello API Inspector tootrace operations using hello Basic Calculator API that is configured in hello [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="f3189-114">如果您尚未完成該教學課程只需要幾分鐘的時間 tooimport hello 基本計算機應用程式開發介面，或您可以使用您選擇例如 hello 回應應用程式開發介面的另一個應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="f3189-114">If you haven't completed that tutorial it only takes a few moments tooimport hello Basic Calculator API, or you can use another API of your choosing such as hello Echo API.</span></span> <span data-ttu-id="f3189-115">每個 API 管理服務執行個體隨附預先設定的一種回應的 API，可以與使用的 tooexperiment 和了解 API 管理。</span><span class="sxs-lookup"><span data-stu-id="f3189-115">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="f3189-116">hello 回應 API 傳回 tooit 傳送任何輸入。</span><span class="sxs-lookup"><span data-stu-id="f3189-116">hello Echo API returns back whatever input is sent tooit.</span></span> <span data-ttu-id="f3189-117">toouse，您可以叫用任何 HTTP 指令動詞，與 hello 傳回值將只會為您的傳送。</span><span class="sxs-lookup"><span data-stu-id="f3189-117">toouse it, you can invoke any HTTP verb, and hello return value will simply be what you sent.</span></span> 

<span data-ttu-id="f3189-118">tooget 啟動，按一下**開發人員入口網站**API 管理服務的 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="f3189-118">tooget started, click **Developer portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="f3189-119">作業可以直接從 hello 開發人員入口網站，其提供方便的方式 tooview 呼叫，並測試應用程式開發介面的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="f3189-119">Operations can be called directly from hello developer portal which provides a convenient way tooview and test hello operations of an API.</span></span>

> <span data-ttu-id="f3189-120">如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。</span><span class="sxs-lookup"><span data-stu-id="f3189-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![API Management developer portal][api-management-developer-portal-menu]

<span data-ttu-id="f3189-122">按一下**Api**從 hello 最上層功能表，然後再按一下**基本計算機**。</span><span class="sxs-lookup"><span data-stu-id="f3189-122">Click **APIs** from hello top menu, and then click **Basic Calculator**.</span></span>

![Echo API][api-management-api]

<span data-ttu-id="f3189-124">按一下**試試**tootry hello**加入兩個整數**作業。</span><span class="sxs-lookup"><span data-stu-id="f3189-124">Click **Try it** tootry hello **Add two integers** operation.</span></span>

![試試看][api-management-open-console]

<span data-ttu-id="f3189-126">防止 hello 預設參數值，且您想要的 hello 產品選取 hello 訂用帳戶金鑰 toouse hello**訂閱金鑰**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="f3189-126">Keep hello default parameter values, and select hello subscription key for hello product you want toouse from hello **subscription-key** drop-down.</span></span>

<span data-ttu-id="f3189-127">根據預設，在 hello 開發人員入口網站 hello **Ocp Apim 追蹤**標頭已設定太**true**。</span><span class="sxs-lookup"><span data-stu-id="f3189-127">By default in hello developer portal hello **Ocp-Apim-Trace** header is already set too**true**.</span></span> <span data-ttu-id="f3189-128">此標頭會設定是否產生追蹤。</span><span class="sxs-lookup"><span data-stu-id="f3189-128">This header configures whether or not a trace is generated.</span></span>

![傳送][api-management-http-get]

<span data-ttu-id="f3189-130">按一下**傳送**tooinvoke hello 作業。</span><span class="sxs-lookup"><span data-stu-id="f3189-130">Click **Send** tooinvoke hello operation.</span></span>

![傳送][api-management-send-results]

<span data-ttu-id="f3189-132">在 hello 回應標頭會**ocp apim-追蹤位置**值類似 toohello，下列範例使用。</span><span class="sxs-lookup"><span data-stu-id="f3189-132">In hello response headers will be an **ocp-apim-trace-location** with a value similar toohello following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="f3189-133">您可以從下載 hello 追蹤 hello 指定的位置，以及檢閱 hello 下一個步驟中所示。</span><span class="sxs-lookup"><span data-stu-id="f3189-133">hello trace can be downloaded from hello specified location and reviewed as demonstrated in hello next step.</span></span> <span data-ttu-id="f3189-134">請注意，只有 hello 最後 100 的記錄檔項目會儲存在輪替中重複使用記錄檔的位置。</span><span class="sxs-lookup"><span data-stu-id="f3189-134">Note that only hello last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="f3189-135">因此，如果您進行 100 個以上的呼叫啟用追蹤的最後一開始覆寫 hello 位置中的第一個追蹤。</span><span class="sxs-lookup"><span data-stu-id="f3189-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting hello first traces in place.</span></span>

## <span data-ttu-id="f3189-136"><a name="inspect-trace"></a>檢查 hello 追蹤</span><span class="sxs-lookup"><span data-stu-id="f3189-136"><a name="inspect-trace"> </a>Inspect hello trace</span></span>
<span data-ttu-id="f3189-137">tooreview hello 追蹤中的 hello 值從 hello 下載 hello 追蹤檔案**ocp apim-追蹤位置**URL。</span><span class="sxs-lookup"><span data-stu-id="f3189-137">tooreview hello values in hello trace, download hello trace file from hello **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="f3189-138">它是以 JSON 格式的文字檔，並包含下列範例項目類似 toohello。</span><span class="sxs-lookup"><span data-stu-id="f3189-138">It is a text file in JSON format, and contains entries similar toohello following example.</span></span>

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
                    "message": "Request is being forwarded toohello backend service.",
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
                    "message": "Response headers have been sent toohello caller. Starting toostream hello response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming toohello caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="f3189-139"><a name="next-steps"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="f3189-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="f3189-140">請觀看 [雲端報導第 177 集：更多 API 管理功能](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)中追蹤原則運算式的示範。</span><span class="sxs-lookup"><span data-stu-id="f3189-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="f3189-141">向前快轉 too21:00 toosee hello 示範。</span><span class="sxs-lookup"><span data-stu-id="f3189-141">Fast-forward too21:00 toosee hello demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector tootrace a call]: #trace-call
[Inspect hello trace]: #inspect-trace
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




