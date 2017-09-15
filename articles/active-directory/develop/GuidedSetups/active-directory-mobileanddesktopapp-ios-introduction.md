---
title: "Azure AD v2 iOS 快速入門 - 簡介 | Microsoft Docs"
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
ms.openlocfilehash: 948693c8501ecc46a1508e5ea085846d0910783e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="call-the-microsoft-graph-api-from-an-ios-app"></a><span data-ttu-id="7b9b2-103">從 iOS 應用程式呼叫 Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="7b9b2-103">Call the Microsoft Graph API from an iOS app</span></span>

<span data-ttu-id="7b9b2-104">本指南示範原生 iOS 應用程式 (Swift) 如何取得存取權杖，以及如何呼叫 Microsoft Graph API 或需要來自 Azure Active Directory v2 端點之存取權杖的其他 API。</span><span class="sxs-lookup"><span data-stu-id="7b9b2-104">This guide demonstrates how a native iOS application (Swift) can get an access token and call the Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="7b9b2-105">在本指南最後，您的應用程式將能夠使用個人帳戶 (包括 outlook.com、live.com 和其他帳戶)，以及使用來自使用 Azure Active Directory 之任何公司或組織的公司與學校帳戶呼叫受保護的 API。</span><span class="sxs-lookup"><span data-stu-id="7b9b2-105">At the end of this guide, your application will be able to call a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>

> ### <a name="pre-requisites"></a><span data-ttu-id="7b9b2-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="7b9b2-106">Pre-requisites</span></span>
> - <span data-ttu-id="7b9b2-107">本指南需要 XCode 8.x。</span><span class="sxs-lookup"><span data-stu-id="7b9b2-107">XCode 8.x is required for this guide.</span></span> <span data-ttu-id="7b9b2-108">您可以[從這裡](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode 下載 URL") 下載 XCode。</span><span class="sxs-lookup"><span data-stu-id="7b9b2-108">You can download XCode [from here](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode Download URL").</span></span>
> - <span data-ttu-id="7b9b2-109">[Carthage](https://github.com/Carthage/Carthage) 以進行套件管理</span><span class="sxs-lookup"><span data-stu-id="7b9b2-109">[Carthage](https://github.com/Carthage/Carthage) for package management</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="7b9b2-110">本指南使用方式</span><span class="sxs-lookup"><span data-stu-id="7b9b2-110">How this guide works</span></span>

![本指南使用方式](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

<span data-ttu-id="7b9b2-112">本指南建立的範例應用程式可讓 iOS 應用程式查詢 Microsoft Graph API，或查詢可接受來自 Azure Active Directory v2 端點之權杖的 Web API。</span><span class="sxs-lookup"><span data-stu-id="7b9b2-112">The sample application created by this guide enables an iOS application to query the Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="7b9b2-113">針對這個案例，系統會透過授權標頭將一個權杖新增到 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="7b9b2-113">For this scenario, a token is added to HTTP requests via the Authorization header.</span></span> <span data-ttu-id="7b9b2-114">權杖取得和更新作業是由 Microsoft Authentication Library (MSAL) 處理。</span><span class="sxs-lookup"><span data-stu-id="7b9b2-114">Token acquisition and renewal is handled by the Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="7b9b2-115">處理權杖取得以存取受保護的 Web API</span><span class="sxs-lookup"><span data-stu-id="7b9b2-115">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="7b9b2-116">使用者完成驗證之後，範例應用程式就會收到一個權杖，可用來查詢 Microsoft Graph API 或由 Microsoft Azure Active Directory v2 保護的 Web API。</span><span class="sxs-lookup"><span data-stu-id="7b9b2-116">After the user authenticates, the sample application receives a token that can be used to query the Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="7b9b2-117">像 Microsoft 圖形這樣的 API 需要存取權杖，才能允許存取特定資源，例如讀取使用者的設定檔、存取使用者的行事曆，或傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="7b9b2-117">APIs such as Microsoft Graph require an access token to allow accessing specific resources – for example, to read a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="7b9b2-118">您的應用程式可以使用 MSAL，以透過指定 API 範圍來要求存取權杖。</span><span class="sxs-lookup"><span data-stu-id="7b9b2-118">Your application can request an access token using MSAL by specifying API scopes.</span></span> <span data-ttu-id="7b9b2-119">此存取權杖接著會新增到 HTTP 授權標頭，這些是針對受保護資源發出之每個呼叫的授權標頭。</span><span class="sxs-lookup"><span data-stu-id="7b9b2-119">This access token is then added to the HTTP Authorization header for every call made against the protected resource.</span></span>

<span data-ttu-id="7b9b2-120">MSAL 會為您管理快取和重新整理存取權杖，因此您的應用程式不需要執行這些作業。</span><span class="sxs-lookup"><span data-stu-id="7b9b2-120">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="7b9b2-121">NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="7b9b2-121">NuGet packages</span></span>

<span data-ttu-id="7b9b2-122">本指南會使用以下 NuGet 套件：</span><span class="sxs-lookup"><span data-stu-id="7b9b2-122">This guide uses the following NuGet packages:</span></span>

|<span data-ttu-id="7b9b2-123">程式庫</span><span class="sxs-lookup"><span data-stu-id="7b9b2-123">Library</span></span>|<span data-ttu-id="7b9b2-124">說明</span><span class="sxs-lookup"><span data-stu-id="7b9b2-124">Description</span></span>|
|---|---|
|[<span data-ttu-id="7b9b2-125">MSAL.framework</span><span class="sxs-lookup"><span data-stu-id="7b9b2-125">MSAL.framework</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|<span data-ttu-id="7b9b2-126">適用於 iOS 的 Microsoft Authentication Library 預覽</span><span class="sxs-lookup"><span data-stu-id="7b9b2-126">Microsoft Authentication Library Preview for iOS</span></span>|

