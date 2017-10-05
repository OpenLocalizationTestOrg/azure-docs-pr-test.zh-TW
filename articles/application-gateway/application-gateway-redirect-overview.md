---
title: "Azure 應用程式閘道的重新導向概觀 | Microsoft Docs"
description: "了解 Azure 應用程式閘道的重新導向功能"
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
ms.openlocfilehash: ea9ae8373ff67bf9557b06bbc8a4b0d82a03e2d0
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="application-gateway-redirect-overview"></a><span data-ttu-id="abce0-103">應用程式閘道重新導向概觀</span><span class="sxs-lookup"><span data-stu-id="abce0-103">Application Gateway redirect overview</span></span>

<span data-ttu-id="abce0-104">許多 Web 應用程式的常見案例是支援自動 HTTP 至 HTTPS 的重新導向，以確保應用程式與其使用者之間的通訊會透過加密的路徑進行。</span><span class="sxs-lookup"><span data-stu-id="abce0-104">A common scenario for many web applications is to support automatic HTTP to HTTPS redirection to ensure all communication between application and its users occurs over an encrypted path.</span></span> <span data-ttu-id="abce0-105">在過去，客戶會使用一些技巧 (例如建立專屬後端集區)，其唯一目的是要將其在 HTTP 上接收的要求重新導向至 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="abce0-105">In the past, customers have used techniques such as creating a dedicated backend pool whose sole purpose is to redirect requests it receives on HTTP to HTTPS.</span></span>  <span data-ttu-id="abce0-106">應用程式閘道現在支援應用程式閘道上重新導向流量的功能。</span><span class="sxs-lookup"><span data-stu-id="abce0-106">Application gateway now supports ability to redirect traffic on the Application Gateway.</span></span> <span data-ttu-id="abce0-107">這可簡化應用程式組態、將資源使用量最佳化，並支援新的重新導向案例，包括全域和路徑式重新導向。</span><span class="sxs-lookup"><span data-stu-id="abce0-107">This simplifies application configuration, optimizes the resource usage, and supports new redirection scenarios including global and path-based redirection.</span></span> <span data-ttu-id="abce0-108">應用程式閘道重新導向支援不只限於 HTTP -> HTTPS 重新導向。</span><span class="sxs-lookup"><span data-stu-id="abce0-108">Application Gateway redirection support is not limited to HTTP -> HTTPS redirection alone.</span></span> <span data-ttu-id="abce0-109">這是泛型重新導向機制，可將在一個接聽程式接收的流量重新導向至應用程式閘道上的另一個接聽程式。</span><span class="sxs-lookup"><span data-stu-id="abce0-109">This is a generic redirection mechanism, which allows for redirection of traffic received at one listener to another listener on Application Gateway.</span></span> <span data-ttu-id="abce0-110">它也支援重新導向至外部網站。</span><span class="sxs-lookup"><span data-stu-id="abce0-110">It also supports redirection to an external site as well.</span></span> <span data-ttu-id="abce0-111">應用程式閘道重新導向提供下列功能：</span><span class="sxs-lookup"><span data-stu-id="abce0-111">Application Gateway redirection support offers the following capabilities:</span></span>

1. <span data-ttu-id="abce0-112">從閘道上的一個接聽程式到另一個接聽程式的全域重新導向。</span><span class="sxs-lookup"><span data-stu-id="abce0-112">Global redirection from one listener to another listener on the Gateway.</span></span> <span data-ttu-id="abce0-113">這允許在網站上進行 HTTP 至 HTTPS 重新導向。</span><span class="sxs-lookup"><span data-stu-id="abce0-113">This enables HTTP to HTTPS redirection on a site.</span></span>
2. <span data-ttu-id="abce0-114">路徑式重新導向。</span><span class="sxs-lookup"><span data-stu-id="abce0-114">Path-based redirection.</span></span> <span data-ttu-id="abce0-115">這類型的重新導向只允許在特定網站區域上進行 HTTP 至 HTTPS 重新導向，例如以 /cart/* 表示的購物車區域。</span><span class="sxs-lookup"><span data-stu-id="abce0-115">This type of redirection enables HTTP to HTTPS redirection only on a specific site area, for example a shopping cart area denoted by /cart/*.</span></span>
3. <span data-ttu-id="abce0-116">重新導向至外部網站。</span><span class="sxs-lookup"><span data-stu-id="abce0-116">Redirect to external site.</span></span>

![重新導向](./media/application-gateway-redirect-overview/redirect.png)

<span data-ttu-id="abce0-118">有了這項變更，客戶必須建立新的重新導向組態物件，以指定重新導向所需的目標接聽程式或外部網站。</span><span class="sxs-lookup"><span data-stu-id="abce0-118">With this change, customers would need to create a new redirect configuration object, which specifies the target listener or external site to which redirection is desired.</span></span> <span data-ttu-id="abce0-119">此組態元素也支援能將 URI 路徑和查詢字串附加至重新導向之 URL 的選項。</span><span class="sxs-lookup"><span data-stu-id="abce0-119">The configuration element also supports options to enable appending the URI path and query string to the redirected URL.</span></span> <span data-ttu-id="abce0-120">客戶也可以選擇重新導向為暫時 (HTTP 狀態碼 302) 或永久重新導向 (HTTP 狀態碼 301)。</span><span class="sxs-lookup"><span data-stu-id="abce0-120">Customers could also choose whether redirection is a temporary (HTTP status code 302) or a permanent redirect (HTTP status code 301).</span></span> <span data-ttu-id="abce0-121">一旦建立，此重新導向組態會透過新規則附加至來源接聽程式。</span><span class="sxs-lookup"><span data-stu-id="abce0-121">Once created this redirect configuration is attached to the source listener via a new rule.</span></span> <span data-ttu-id="abce0-122">若使用時基本規則，重新導向組態會與來源接聽程式相關聯並為全域重新導向。</span><span class="sxs-lookup"><span data-stu-id="abce0-122">When using a basic rule, the redirect configuration is associated with a source listener and is a global redirect.</span></span> <span data-ttu-id="abce0-123">若使用路徑式規則，重新導向組態會定義於 URL 路徑圖上，因此僅適用於網站的特定路徑區域。</span><span class="sxs-lookup"><span data-stu-id="abce0-123">When a path-based rule is used, the redirect configuration is defined on the URL path map and hence only applies to the specific path area of a site.</span></span>

### <a name="next-steps"></a><span data-ttu-id="abce0-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="abce0-124">Next steps</span></span>

[<span data-ttu-id="abce0-125">在應用程式閘道上設定 URL 重新導向</span><span class="sxs-lookup"><span data-stu-id="abce0-125">Configure URL redirection on an application gateway</span></span>](application-gateway-configure-redirect-powershell.md)
