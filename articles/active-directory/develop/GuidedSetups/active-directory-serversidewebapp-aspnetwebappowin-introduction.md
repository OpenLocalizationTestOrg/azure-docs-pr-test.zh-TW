---
title: "aaaAzure AD v2 ASP.NET Web 伺服器快速入門-簡介 |Microsoft 文件"
description: "使用 OpenID Connect 標準，搭配傳統網頁瀏覽器型應用程式，在 ASP.NET 方案上實作 Microsoft 登入"
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
ms.openlocfilehash: d6449926af2bdad24cbc8e91f74885a08f909103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a><span data-ttu-id="b9b6d-103">新增 Microsoft tooan ASP.NET web 應用程式使用登入</span><span class="sxs-lookup"><span data-stu-id="b9b6d-103">Add sign-in with Microsoft tooan ASP.NET web app</span></span>

<span data-ttu-id="b9b6d-104">本指南示範如何 tooimplement 使用登入 Microsoft 與傳統 web 瀏覽器型應用程式使用 OpenID Connect 使用 ASP.NET MVC 方案。</span><span class="sxs-lookup"><span data-stu-id="b9b6d-104">This guide demonstrates how tooimplement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="b9b6d-105">在本指南的 hello 結尾，您的應用程式會無法 tooaccept 符號集個人的帳戶 （包括 outlook.com、 live.com 和其他項目），以及運作並學校帳戶，從任何的公司或組織與 Azure Active Directory 整合。</span><span class="sxs-lookup"><span data-stu-id="b9b6d-105">At hello end of this guide, your application will be able tooaccept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="b9b6d-106">本指南需要 Visual Studio 2015 Update 3 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="b9b6d-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="b9b6d-107">沒有嗎？</span><span class="sxs-lookup"><span data-stu-id="b9b6d-107">Don’t have it?</span></span>  [<span data-ttu-id="b9b6d-108">免費下載 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="b9b6d-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="b9b6d-109">本指南使用方式</span><span class="sxs-lookup"><span data-stu-id="b9b6d-109">How this guide works</span></span>

![本指南使用方式](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="b9b6d-111">本指南根據 hello 案例中，瀏覽器存取的 ASP.NET 網站上，要求使用者 tooauthenticate 透過登入 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b9b6d-111">This guide is based on hello scenario where a browser accesses an ASP.NET web site, requesting a user tooauthenticate via a sign-in button.</span></span> <span data-ttu-id="b9b6d-112">在此案例中，大部分的 hello 工作 toorender hello 網頁上發生 hello 伺服器端。</span><span class="sxs-lookup"><span data-stu-id="b9b6d-112">In this scenario, most of hello work toorender hello web page occurs on hello server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="b9b6d-113">程式庫</span><span class="sxs-lookup"><span data-stu-id="b9b6d-113">Libraries</span></span>

<span data-ttu-id="b9b6d-114">本指南會使用下列程式庫的 hello:</span><span class="sxs-lookup"><span data-stu-id="b9b6d-114">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="b9b6d-115">程式庫</span><span class="sxs-lookup"><span data-stu-id="b9b6d-115">Library</span></span>|<span data-ttu-id="b9b6d-116">描述</span><span class="sxs-lookup"><span data-stu-id="b9b6d-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="b9b6d-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="b9b6d-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="b9b6d-118">可讓應用程式 toouse OpenIdConnect 驗證中介軟體</span><span class="sxs-lookup"><span data-stu-id="b9b6d-118">Middleware that enables an application toouse OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="b9b6d-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="b9b6d-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="b9b6d-120">中介軟體，可讓使用 cookie 的應用程式 toomaintain 使用者工作階段</span><span class="sxs-lookup"><span data-stu-id="b9b6d-120">Middleware that enables an application toomaintain user session using cookies</span></span>|
|[<span data-ttu-id="b9b6d-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="b9b6d-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="b9b6d-122">啟用 OWIN 應用程式 toorun 於 IIS 使用 hello ASP.NET 要求管線</span><span class="sxs-lookup"><span data-stu-id="b9b6d-122">Enables OWIN-based applications toorun on IIS using hello ASP.NET request pipeline</span></span>|

