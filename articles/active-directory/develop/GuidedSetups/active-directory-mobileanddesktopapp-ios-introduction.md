---
title: "aaaAzure AD v2 iOS 入門-簡介 |Microsoft 文件"
description: "iOS (Swift) 應用程式如何呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
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
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: f40aebbb75490912e533aecc7eedfb2b2dcd8c6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-ios-app"></a><span data-ttu-id="e1a47-103">從 iOS 應用程式呼叫 hello Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="e1a47-103">Call hello Microsoft Graph API from an iOS app</span></span>

<span data-ttu-id="e1a47-104">本指南示範如何取得存取權杖和呼叫 hello Microsoft Graph API 或需要向 Azure Active Directory v2 端點的存取權杖的其他 Api 的原生 iOS 應用程式 (Swift)。</span><span class="sxs-lookup"><span data-stu-id="e1a47-104">This guide demonstrates how a native iOS application (Swift) can get an access token and call hello Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="e1a47-105">在 hello 本指南結尾，您的應用程式將會無法 toocall 受保護應用程式開發介面使用個人帳戶 （包括 outlook.com、 live.com 和其他項目），以及工作及學校帳戶，從任何的公司或組織有 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="e1a47-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>

> ### <a name="pre-requisites"></a><span data-ttu-id="e1a47-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="e1a47-106">Pre-requisites</span></span>
> - <span data-ttu-id="e1a47-107">本指南需要 XCode 8.x。</span><span class="sxs-lookup"><span data-stu-id="e1a47-107">XCode 8.x is required for this guide.</span></span> <span data-ttu-id="e1a47-108">您可以[從這裡](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode 下載 URL") 下載 XCode。</span><span class="sxs-lookup"><span data-stu-id="e1a47-108">You can download XCode [from here](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode Download URL").</span></span>
> - <span data-ttu-id="e1a47-109">[Carthage](https://github.com/Carthage/Carthage) 以進行套件管理</span><span class="sxs-lookup"><span data-stu-id="e1a47-109">[Carthage](https://github.com/Carthage/Carthage) for package management</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="e1a47-110">本指南使用方式</span><span class="sxs-lookup"><span data-stu-id="e1a47-110">How this guide works</span></span>

![本指南使用方式](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

<span data-ttu-id="e1a47-112">本指南所建立的 hello 範例應用程式可讓 iOS 應用程式 tooquery hello Microsoft Graph API 或 Web API 可接受來自 Azure Active Directory v2 端點的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="e1a47-112">hello sample application created by this guide enables an iOS application tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="e1a47-113">對於此案例中，權杖就會加入 tooHTTP 透過 hello 授權標頭的要求。</span><span class="sxs-lookup"><span data-stu-id="e1a47-113">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="e1a47-114">權杖取得和更新是由 hello Microsoft 驗證程式庫 (MSAL) 處理。</span><span class="sxs-lookup"><span data-stu-id="e1a47-114">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="e1a47-115">處理權杖取得以存取受保護的 Web API</span><span class="sxs-lookup"><span data-stu-id="e1a47-115">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="e1a47-116">Hello 使用者驗證之後，hello 範例應用程式會收到可使用的 tooquery hello Microsoft Graph API 或 Microsoft Azure Active Directory v2 所保護的 Web API 的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="e1a47-116">After hello user authenticates, hello sample application receives a token that can be used tooquery hello Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="e1a47-117">例如，Microsoft Graph 需要存取特定資源 – 例如，tooread 存取語彙基元 tooallow 使用者設定檔，Api 會存取使用者的行事曆，或傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="e1a47-117">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="e1a47-118">您的應用程式可以使用 MSAL，以透過指定 API 範圍來要求存取權杖。</span><span class="sxs-lookup"><span data-stu-id="e1a47-118">Your application can request an access token using MSAL by specifying API scopes.</span></span> <span data-ttu-id="e1a47-119">加入的 toohello hello 對所提出的每個呼叫的 HTTP 授權標頭的受保護資源，則此存取權杖。</span><span class="sxs-lookup"><span data-stu-id="e1a47-119">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span>

<span data-ttu-id="e1a47-120">MSAL 會為您管理快取和重新整理存取權杖，因此您的應用程式不需要執行這些作業。</span><span class="sxs-lookup"><span data-stu-id="e1a47-120">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="e1a47-121">NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="e1a47-121">NuGet packages</span></span>

<span data-ttu-id="e1a47-122">本指南會使用下列 NuGet 套件 hello:</span><span class="sxs-lookup"><span data-stu-id="e1a47-122">This guide uses hello following NuGet packages:</span></span>

|<span data-ttu-id="e1a47-123">程式庫</span><span class="sxs-lookup"><span data-stu-id="e1a47-123">Library</span></span>|<span data-ttu-id="e1a47-124">說明</span><span class="sxs-lookup"><span data-stu-id="e1a47-124">Description</span></span>|
|---|---|
|[<span data-ttu-id="e1a47-125">MSAL.framework</span><span class="sxs-lookup"><span data-stu-id="e1a47-125">MSAL.framework</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|<span data-ttu-id="e1a47-126">適用於 iOS 的 Microsoft Authentication Library 預覽</span><span class="sxs-lookup"><span data-stu-id="e1a47-126">Microsoft Authentication Library Preview for iOS</span></span>|

