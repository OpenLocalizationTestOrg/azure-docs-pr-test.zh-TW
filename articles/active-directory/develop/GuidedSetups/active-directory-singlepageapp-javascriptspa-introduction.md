---
title: "aaaAzure AD v2 JS SPA 引導式安裝-簡介 |Microsoft 文件"
description: "JavaScript SPA 應用程式如何呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a><span data-ttu-id="7220b-103">呼叫 hello Microsoft Graph API 從 JavaScript 單一頁面應用程式 (SPA)</span><span class="sxs-lookup"><span data-stu-id="7220b-103">Call hello Microsoft Graph API from a JavaScript Single Page Application (SPA)</span></span>

<span data-ttu-id="7220b-104">本指南示範如何 JavaScript 單一頁面應用程式 (SPA) 可以登入 [個人] 的工作及學校帳戶，取得存取權杖，並呼叫 hello Microsoft Graph API 或需要存取權杖，從其他應用程式開發介面 hello Azure Active Directory v2 端點。</span><span class="sxs-lookup"><span data-stu-id="7220b-104">This guide demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call hello Microsoft Graph API or other APIs that require access tokens from hello Azure Active Directory v2 endpoint.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="7220b-105">本指南使用方式</span><span class="sxs-lookup"><span data-stu-id="7220b-105">How this guide works</span></span>

![本指南所產生的 hello 範例應用程式的運作方式](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="7220b-107">相關資訊</span><span class="sxs-lookup"><span data-stu-id="7220b-107">More Information</span></span>

<span data-ttu-id="7220b-108">本指南所建立的 hello 範例應用程式可讓 JavaScript SPA tooquery hello Microsoft Graph API 或 Web API 可接受來自 Azure Active Directory v2 端點的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="7220b-108">hello sample application created by this guide enables a JavaScript SPA tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="7220b-109">此案例中，登入時的使用者存取權杖是透過 hello 授權標頭的要求和加入 tooHTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="7220b-109">For this scenario, after a user signs-in, an access token is requested and added tooHTTP requests via hello authorization header.</span></span> <span data-ttu-id="7220b-110">Hello Microsoft 驗證程式庫 (MSAL) 會處理權杖取得及更新。</span><span class="sxs-lookup"><span data-stu-id="7220b-110">Token acquisition and renewal are handled by hello Microsoft Authentication Library (MSAL).</span></span>

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a><span data-ttu-id="7220b-111">程式庫</span><span class="sxs-lookup"><span data-stu-id="7220b-111">Libraries</span></span>

<span data-ttu-id="7220b-112">本指南會使用下列程式庫的 hello:</span><span class="sxs-lookup"><span data-stu-id="7220b-112">This guide uses hello following library:</span></span>

|<span data-ttu-id="7220b-113">程式庫</span><span class="sxs-lookup"><span data-stu-id="7220b-113">Library</span></span>|<span data-ttu-id="7220b-114">說明</span><span class="sxs-lookup"><span data-stu-id="7220b-114">Description</span></span>|
|---|---|
|[<span data-ttu-id="7220b-115">msal.js</span><span class="sxs-lookup"><span data-stu-id="7220b-115">msal.js</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js)|<span data-ttu-id="7220b-116">Microsoft Authentication Library for JavaScript 預覽</span><span class="sxs-lookup"><span data-stu-id="7220b-116">Microsoft Authentication Library for JavaScript Preview</span></span>|

> [!NOTE]
> <span data-ttu-id="7220b-117">*msal.js*目標 hello *Azure Active Directory v2 端點*-這可讓個人、 學校和工作帳戶 toosign 中的並取得語彙基元。</span><span class="sxs-lookup"><span data-stu-id="7220b-117">*msal.js* targets hello *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts toosign in and acquire tokens.</span></span> <span data-ttu-id="7220b-118">hello *Azure Active Directory v2 端點*具有[一些限制](..\active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="7220b-118">hello *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md).</span></span> <span data-ttu-id="7220b-119">如果您只有興趣學校和工作帳戶，請使用*adal.js*和 hello *V1 端點*。</span><span class="sxs-lookup"><span data-stu-id="7220b-119">If you are interested only in school and work accounts, use *adal.js* and hello *V1 endpoint*.</span></span> <span data-ttu-id="7220b-120">toounderstand hello v1 和 v2 端點之間的差異讀取 hello [v1 v2 比較](..\active-directory-v2-compare.md)。</span><span class="sxs-lookup"><span data-stu-id="7220b-120">toounderstand differences between hello v1 and v2 endpoints read hello [v1-v2 comparison](..\active-directory-v2-compare.md).</span></span>

<!--end-collapse-->
