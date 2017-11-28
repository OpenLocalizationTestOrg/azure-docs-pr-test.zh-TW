---
title: "Azure AD v2 JS SPA 指引設定 - 簡介 | Microsoft Docs"
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
ms.openlocfilehash: 3d195d0d67f8f82c9450ffd93767917698addee3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="call-the-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a><span data-ttu-id="5c71c-103">從 JavaScript 單一頁面應用程式 (SPA) 呼叫 Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="5c71c-103">Call the Microsoft Graph API from a JavaScript Single Page Application (SPA)</span></span>

<span data-ttu-id="5c71c-104">本指南示範 JavaScript 單一頁面應用程式 (SPA)如何登入個人公司及學校帳戶，取得存取權杖，以及呼叫 Microsoft Graph API 或需要來自 Azure Active Directory v2 端點之存取權杖的其他 API。</span><span class="sxs-lookup"><span data-stu-id="5c71c-104">This guide demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call the Microsoft Graph API or other APIs that require access tokens from the Azure Active Directory v2 endpoint.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="5c71c-105">本指南使用方式</span><span class="sxs-lookup"><span data-stu-id="5c71c-105">How this guide works</span></span>

![本指南產生之範例應用程式的運作方式](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="5c71c-107">相關資訊</span><span class="sxs-lookup"><span data-stu-id="5c71c-107">More Information</span></span>

<span data-ttu-id="5c71c-108">本指南建立的範例應用程式可讓 JavaScript SPA 查詢 Microsoft Graph API，或查詢可接受來自 Azure Active Directory v2 端點之權杖的 Web API。</span><span class="sxs-lookup"><span data-stu-id="5c71c-108">The sample application created by this guide enables a JavaScript SPA to query the Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="5c71c-109">針對這個案例，在使用者登入之後，系統會透過授權標頭要求一個存取權杖，並將其新增到 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="5c71c-109">For this scenario, after a user signs-in, an access token is requested and added to HTTP requests via the authorization header.</span></span> <span data-ttu-id="5c71c-110">權杖取得和更新作業是由 Microsoft Authentication Library (MSAL) 處理。</span><span class="sxs-lookup"><span data-stu-id="5c71c-110">Token acquisition and renewal are handled by the Microsoft Authentication Library (MSAL).</span></span>

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a><span data-ttu-id="5c71c-111">程式庫</span><span class="sxs-lookup"><span data-stu-id="5c71c-111">Libraries</span></span>

<span data-ttu-id="5c71c-112">本指南使用下列程式庫：</span><span class="sxs-lookup"><span data-stu-id="5c71c-112">This guide uses the following library:</span></span>

|<span data-ttu-id="5c71c-113">程式庫</span><span class="sxs-lookup"><span data-stu-id="5c71c-113">Library</span></span>|<span data-ttu-id="5c71c-114">說明</span><span class="sxs-lookup"><span data-stu-id="5c71c-114">Description</span></span>|
|---|---|
|[<span data-ttu-id="5c71c-115">msal.js</span><span class="sxs-lookup"><span data-stu-id="5c71c-115">msal.js</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js)|<span data-ttu-id="5c71c-116">Microsoft Authentication Library for JavaScript 預覽</span><span class="sxs-lookup"><span data-stu-id="5c71c-116">Microsoft Authentication Library for JavaScript Preview</span></span>|

> [!NOTE]
> <span data-ttu-id="5c71c-117">msal.js 的目標是 Azure Active Directory v2 端點 - 它會啟用個人、學校及公司帳戶以登入和取得權杖。</span><span class="sxs-lookup"><span data-stu-id="5c71c-117">*msal.js* targets the *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts to sign in and acquire tokens.</span></span> <span data-ttu-id="5c71c-118">Azure Active Directory v2 端點具有[一些限制](..\active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="5c71c-118">The *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md).</span></span> <span data-ttu-id="5c71c-119">如果您只對於學校和公司帳戶感到興趣，請使用 adal.js 和 V1 端點。</span><span class="sxs-lookup"><span data-stu-id="5c71c-119">If you are interested only in school and work accounts, use *adal.js* and the *V1 endpoint*.</span></span> <span data-ttu-id="5c71c-120">若要了解 v1 和 v2 端點之間的差異，請參閱 [v1-v2 比較](..\active-directory-v2-compare.md)。</span><span class="sxs-lookup"><span data-stu-id="5c71c-120">To understand differences between the v1 and v2 endpoints read the [v1-v2 comparison](..\active-directory-v2-compare.md).</span></span>

<!--end-collapse-->
