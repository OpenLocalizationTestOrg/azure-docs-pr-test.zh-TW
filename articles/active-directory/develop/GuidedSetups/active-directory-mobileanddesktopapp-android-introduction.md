---
title: "aaaAzure AD v2 Android 快速入門-簡介 |Microsoft 文件"
description: "Android 應用程式如何取得存取權杖，以及如何呼叫 Microsoft 圖形 API，或呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 7c76ab8bbf1a6c934ab672cccf85ae82f03f601a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a><span data-ttu-id="62afd-103">從 Android 應用程式呼叫 hello Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="62afd-103">Call hello Microsoft Graph API from an Android app</span></span>

<span data-ttu-id="62afd-104">本指南示範原生 Android 應用程式如何取得存取權杖，以及如何呼叫 Microsoft 圖形 API 或需要來自 Azure Active Directory v2 端點之存取權杖的其他 API。</span><span class="sxs-lookup"><span data-stu-id="62afd-104">This guide demonstrates how a native Android application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="62afd-105">在 hello 本指南結尾，您的應用程式將會無法 toocall 受保護應用程式開發介面使用個人帳戶 （包括 outlook.com、 live.com 和其他項目），以及工作及學校帳戶，從任何的公司或組織有 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="62afd-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

### <a name="how-this-sample-works"></a><span data-ttu-id="62afd-106">這個範例的運作方式</span><span class="sxs-lookup"><span data-stu-id="62afd-106">How this sample works</span></span>
![這個範例的運作方式](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

<span data-ttu-id="62afd-108">本指南所建立的 hello 範例根據的案例，其中的 Android 應用程式是使用的 tooquery Web API 可接受來自 Azure Active Directory v2 端點 – 在此情況下，Microsoft Graph API 的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="62afd-108">hello sample created by this guide is based on a scenario where an Android application is used tooquery a Web API that accepts tokens from Azure Active Directory v2 endpoint – in this case, Microsoft Graph API.</span></span> <span data-ttu-id="62afd-109">對於此案例中，權杖就會加入 tooHTTP 透過 hello 授權標頭的要求。</span><span class="sxs-lookup"><span data-stu-id="62afd-109">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="62afd-110">權杖取得和更新是由 hello Microsoft 驗證程式庫 (MSAL) 處理。</span><span class="sxs-lookup"><span data-stu-id="62afd-110">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="62afd-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="62afd-111">Pre-requisites</span></span>
* <span data-ttu-id="62afd-112">本引導式設定著重在 Android Studio，但也可以接受任何其他 Android 應用程式開發環境。</span><span class="sxs-lookup"><span data-stu-id="62afd-112">This guided setup is focused on Android Studio, but any other Android application development environment is also acceptable.</span></span> 
* <span data-ttu-id="62afd-113">需要 Android SDK 21 或更新版本 (建議使用 SDK 25)。</span><span class="sxs-lookup"><span data-stu-id="62afd-113">Android SDK 21 or newer is required (SDK 25 is recommended).</span></span>
* <span data-ttu-id="62afd-114">這個 Android 版的 Microsoft Authentication Library (MSAL) 版本需要 Google Chrome 或使用「自訂索引標籤」的網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="62afd-114">Google Chrome or a web browser using Custom Tabs is required for this release of Microsoft Authentication Library (MSAL) for Android.</span></span>

> <span data-ttu-id="62afd-115">注意：Visual Studio 的 Android 模擬器中未包括 Google Chrome。</span><span class="sxs-lookup"><span data-stu-id="62afd-115">Note: Google Chrome is not included on Visual Studio Emulator for Android.</span></span> <span data-ttu-id="62afd-116">我們建議您 tootest 的模擬器，應用程式開發介面 25 或映像 API 21 或更新版本已使用 Google Chrome 安裝此程式碼。</span><span class="sxs-lookup"><span data-stu-id="62afd-116">We recommend you tootest this code on an Emulator with API 25 or an image with API 21 or newer that has with Google Chrome installed.</span></span>


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a><span data-ttu-id="62afd-117">如何 toohandle 語彙基元擷取 tooaccess 受保護的 Web API</span><span class="sxs-lookup"><span data-stu-id="62afd-117">How toohandle token acquisition tooaccess a protected Web API</span></span>

<span data-ttu-id="62afd-118">Hello 使用者驗證之後，hello 範例應用程式會收到可使用的 tooquery Microsoft Graph API 或 Microsoft Azure Active Directory v2 所保護的 Web API 的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="62afd-118">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="62afd-119">例如，Microsoft Graph 需要存取特定資源 – 例如，tooread 存取語彙基元 tooallow 使用者設定檔，Api 會存取使用者的行事曆，或傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="62afd-119">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="62afd-120">您的應用程式可以要求存取權杖使用 MSAL tooaccess 這些資源指定應用程式開發介面的範圍。</span><span class="sxs-lookup"><span data-stu-id="62afd-120">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="62afd-121">加入的 toohello hello 對所提出的每個呼叫的 HTTP 授權標頭的受保護資源，則此存取權杖。</span><span class="sxs-lookup"><span data-stu-id="62afd-121">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="62afd-122">MSAL 會為您管理快取和重新整理存取權杖，因此您的應用程式不需要執行這些作業。</span><span class="sxs-lookup"><span data-stu-id="62afd-122">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>

### <a name="libraries"></a><span data-ttu-id="62afd-123">程式庫</span><span class="sxs-lookup"><span data-stu-id="62afd-123">Libraries</span></span>

<span data-ttu-id="62afd-124">本指南會使用下列程式庫的 hello:</span><span class="sxs-lookup"><span data-stu-id="62afd-124">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="62afd-125">程式庫</span><span class="sxs-lookup"><span data-stu-id="62afd-125">Library</span></span>|<span data-ttu-id="62afd-126">描述</span><span class="sxs-lookup"><span data-stu-id="62afd-126">Description</span></span>|
|---|---|
|[<span data-ttu-id="62afd-127">com.microsoft.identity.client (英文)</span><span class="sxs-lookup"><span data-stu-id="62afd-127">com.microsoft.identity.client</span></span>](http://javadoc.io/doc/com.microsoft.identity.client/msal)|<span data-ttu-id="62afd-128">Microsoft Authentication Library (MSAL)</span><span class="sxs-lookup"><span data-stu-id="62afd-128">Microsoft Authentication Library (MSAL)</span></span>|
