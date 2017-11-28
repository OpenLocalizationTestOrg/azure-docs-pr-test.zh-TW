---
title: "Azure 應用程式閘道 aaaRedirect 概觀 |Microsoft 文件"
description: "深入了解 Azure 應用程式閘道中的 hello 重新導向功能"
services: application-gateway
documentationcenter: na
author: amsriva
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/18/2017
ms.author: amsriva
ms.openlocfilehash: 7149e3bd000d336c51995fb0e90f971b4d9ba2be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-redirect-overview"></a><span data-ttu-id="5175d-103">應用程式閘道重新導向概觀</span><span class="sxs-lookup"><span data-stu-id="5175d-103">Application Gateway redirect overview</span></span>

<span data-ttu-id="5175d-104">許多 web 應用程式的常見案例是 toosupport 自動 HTTP tooHTTPS 重新導向 tooensure 應用程式和其使用者之間的通訊會透過加密的路徑。</span><span class="sxs-lookup"><span data-stu-id="5175d-104">A common scenario for many web applications is toosupport automatic HTTP tooHTTPS redirection tooensure all communication between application and its users occurs over an encrypted path.</span></span> <span data-ttu-id="5175d-105">在 hello 過去，客戶使用的技術，例如建立專用的後端集區，其唯一目的是 tooredirect HTTP tooHTTPS 收到的要求。</span><span class="sxs-lookup"><span data-stu-id="5175d-105">In hello past, customers have used techniques such as creating a dedicated backend pool whose sole purpose is tooredirect requests it receives on HTTP tooHTTPS.</span></span>  <span data-ttu-id="5175d-106">應用程式閘道現在支援能力 tooredirect 流量上 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="5175d-106">Application gateway now supports ability tooredirect traffic on hello Application Gateway.</span></span> <span data-ttu-id="5175d-107">這可簡化應用程式組態、 最佳化 hello 資源使用狀況，並支援新的重新導向案例，包括全域和路徑為基礎的重新導向。</span><span class="sxs-lookup"><span data-stu-id="5175d-107">This simplifies application configuration, optimizes hello resource usage, and supports new redirection scenarios including global and path-based redirection.</span></span> <span data-ttu-id="5175d-108">應用程式閘道重新導向支援不限於 tooHTTP]-> [HTTPS 單獨的重新導向。</span><span class="sxs-lookup"><span data-stu-id="5175d-108">Application Gateway redirection support is not limited tooHTTP -> HTTPS redirection alone.</span></span> <span data-ttu-id="5175d-109">這是流量的泛型的重新導向的機制，可在應用程式閘道上的一個接聽程式 tooanother 接聽程式接收重新導向。</span><span class="sxs-lookup"><span data-stu-id="5175d-109">This is a generic redirection mechanism, which allows for redirection of traffic received at one listener tooanother listener on Application Gateway.</span></span> <span data-ttu-id="5175d-110">它也支援重新導向 tooan 外部站台。</span><span class="sxs-lookup"><span data-stu-id="5175d-110">It also supports redirection tooan external site as well.</span></span> <span data-ttu-id="5175d-111">應用程式閘道重新導向的支援會提供下列功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="5175d-111">Application Gateway redirection support offers hello following capabilities:</span></span>

1. <span data-ttu-id="5175d-112">從一個接聽程式 tooanother 接聽 hello 閘道的全域重新導向。</span><span class="sxs-lookup"><span data-stu-id="5175d-112">Global redirection from one listener tooanother listener on hello Gateway.</span></span> <span data-ttu-id="5175d-113">這可讓站台上的 HTTP tooHTTPS 重新導向。</span><span class="sxs-lookup"><span data-stu-id="5175d-113">This enables HTTP tooHTTPS redirection on a site.</span></span>
2. <span data-ttu-id="5175d-114">路徑式重新導向。</span><span class="sxs-lookup"><span data-stu-id="5175d-114">Path-based redirection.</span></span> <span data-ttu-id="5175d-115">重新導向的這個類型可讓 HTTP tooHTTPS 重新導向只有在特定站台的區域中，例如購物車區域表示/車 / *。</span><span class="sxs-lookup"><span data-stu-id="5175d-115">This type of redirection enables HTTP tooHTTPS redirection only on a specific site area, for example a shopping cart area denoted by /cart/*.</span></span>
3. <span data-ttu-id="5175d-116">重新導向 tooexternal 站台。</span><span class="sxs-lookup"><span data-stu-id="5175d-116">Redirect tooexternal site.</span></span>

![重新導向](./media/application-gateway-redirect-overview/redirect.png)

<span data-ttu-id="5175d-118">透過這項變更，客戶需要 toocreate 新重新導向設定物件，指定 hello 目標接聽程式，或想要使用外部網站 toowhich 重新導向。</span><span class="sxs-lookup"><span data-stu-id="5175d-118">With this change, customers would need toocreate a new redirect configuration object, which specifies hello target listener or external site toowhich redirection is desired.</span></span> <span data-ttu-id="5175d-119">hello 組態項目也支援選項 tooenable 附加 hello URI 的路徑和查詢字串 toohello 重新導向 URL。</span><span class="sxs-lookup"><span data-stu-id="5175d-119">hello configuration element also supports options tooenable appending hello URI path and query string toohello redirected URL.</span></span> <span data-ttu-id="5175d-120">客戶也可以選擇重新導向為暫時 (HTTP 狀態碼 302) 或永久重新導向 (HTTP 狀態碼 301)。</span><span class="sxs-lookup"><span data-stu-id="5175d-120">Customers could also choose whether redirection is a temporary (HTTP status code 302) or a permanent redirect (HTTP status code 301).</span></span> <span data-ttu-id="5175d-121">一旦建立此重新導向設定是透過新的規則附加的 toohello 來源接聽程式。</span><span class="sxs-lookup"><span data-stu-id="5175d-121">Once created this redirect configuration is attached toohello source listener via a new rule.</span></span> <span data-ttu-id="5175d-122">使用時的基本規則，hello 重新導向組態與來源的接聽程式相關聯，是通用的重新導向。</span><span class="sxs-lookup"><span data-stu-id="5175d-122">When using a basic rule, hello redirect configuration is associated with a source listener and is a global redirect.</span></span> <span data-ttu-id="5175d-123">使用路徑規則時，定義上 hello URL 路徑對應 hello 重新導向設定，以及因此僅適用於 toohello 特定路徑區域中的站台。</span><span class="sxs-lookup"><span data-stu-id="5175d-123">When a path-based rule is used, hello redirect configuration is defined on hello URL path map and hence only applies toohello specific path area of a site.</span></span>

### <a name="next-steps"></a><span data-ttu-id="5175d-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5175d-124">Next steps</span></span>

[<span data-ttu-id="5175d-125">在應用程式閘道上設定 URL 重新導向</span><span class="sxs-lookup"><span data-stu-id="5175d-125">Configure URL redirection on an application gateway</span></span>](application-gateway-configure-redirect-powershell.md)
