---
title: "aaaAzure AD v2 Windows 桌面快速入門-簡介 |Microsoft 文件"
description: "Windows Desktop .NET (XAML) 應用程式如何呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
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
ms.openlocfilehash: 89d98fc46190ba9e47b7c3095f91e32eca455fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a><span data-ttu-id="858ac-103">從 Windows 桌面應用程式呼叫 hello Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="858ac-103">Call hello Microsoft Graph API from a Windows Desktop app</span></span>

<span data-ttu-id="858ac-104">本指南示範原生 Windows Desktop .NET (XAML) 應用程式如何取得存取權杖，以及如何呼叫 Microsoft 圖形 API 或需要來自 Azure Active Directory v2 端點之存取權杖的其他 API。</span><span class="sxs-lookup"><span data-stu-id="858ac-104">This guide demonstrates how a native Windows Desktop .NET (XAML) application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="858ac-105">在 hello 本指南結尾，您的應用程式將會無法 toocall 受保護應用程式開發介面使用個人帳戶 （包括 outlook.com、 live.com 和其他項目），以及工作及學校帳戶，從任何的公司或組織有 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="858ac-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

> <span data-ttu-id="858ac-106">本指南需要 Visual Studio 2015 Update 3 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="858ac-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="858ac-107">沒有嗎？</span><span class="sxs-lookup"><span data-stu-id="858ac-107">Don’t have it?</span></span> [<span data-ttu-id="858ac-108">免費下載 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="858ac-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a><span data-ttu-id="858ac-109">本指南使用方式</span><span class="sxs-lookup"><span data-stu-id="858ac-109">How this guide works</span></span>

![本指南使用方式](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

<span data-ttu-id="858ac-111">本指南所建立的 hello 範例應用程式可讓 Windows 桌面應用程式 tooquery Microsoft Graph API 或 Web API 可接受來自 Azure Active Directory v2 端點的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="858ac-111">hello sample application created by this guide enables a Windows Desktop Application tooquery Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="858ac-112">對於此案例中，權杖就會加入 tooHTTP 透過 hello 授權標頭的要求。</span><span class="sxs-lookup"><span data-stu-id="858ac-112">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="858ac-113">權杖取得和更新是由 hello Microsoft 驗證程式庫 (MSAL) 處理。</span><span class="sxs-lookup"><span data-stu-id="858ac-113">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="858ac-114">處理權杖取得以存取受保護的 Web API</span><span class="sxs-lookup"><span data-stu-id="858ac-114">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="858ac-115">Hello 使用者驗證之後，hello 範例應用程式會收到可使用的 tooquery Microsoft Graph API 或 Microsoft Azure Active Directory v2 所保護的 Web API 的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="858ac-115">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="858ac-116">例如，Microsoft Graph 需要存取特定資源 – 例如，tooread 存取語彙基元 tooallow 使用者設定檔，Api 會存取使用者的行事曆，或傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="858ac-116">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="858ac-117">您的應用程式可以要求存取權杖使用 MSAL tooaccess 這些資源指定應用程式開發介面的範圍。</span><span class="sxs-lookup"><span data-stu-id="858ac-117">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="858ac-118">加入的 toohello hello 對所提出的每個呼叫的 HTTP 授權標頭的受保護資源，則此存取權杖。</span><span class="sxs-lookup"><span data-stu-id="858ac-118">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="858ac-119">MSAL 會為您管理快取和重新整理存取權杖，因此您的應用程式不需要執行這些作業。</span><span class="sxs-lookup"><span data-stu-id="858ac-119">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="858ac-120">NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="858ac-120">NuGet Packages</span></span>

<span data-ttu-id="858ac-121">本指南會使用下列 NuGet 套件 hello:</span><span class="sxs-lookup"><span data-stu-id="858ac-121">This guide uses hello following NuGet packages:</span></span>

|<span data-ttu-id="858ac-122">程式庫</span><span class="sxs-lookup"><span data-stu-id="858ac-122">Library</span></span>|<span data-ttu-id="858ac-123">描述</span><span class="sxs-lookup"><span data-stu-id="858ac-123">Description</span></span>|
|---|---|
|[<span data-ttu-id="858ac-124">Microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="858ac-124">Microsoft.Identity.Client</span></span>](https://www.nuget.org/packages/Microsoft.Identity.Client)|<span data-ttu-id="858ac-125">Microsoft Authentication Library (MSAL)</span><span class="sxs-lookup"><span data-stu-id="858ac-125">Microsoft Authentication Library (MSAL)</span></span>|

