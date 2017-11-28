---
title: "Azure AD v2 ASP.NET Web 伺服器快速入門 - 簡介 | Microsoft Docs"
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
ms.openlocfilehash: 8062923b6270ec6253dc231a3db4333cf4666b42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-with-microsoft-to-an-aspnet-web-app"></a><span data-ttu-id="f8368-103">將「使用 Microsoft 登入」新增至 ASP.NET Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="f8368-103">Add sign-in with Microsoft to an ASP.NET web app</span></span>

<span data-ttu-id="f8368-104">本指南示範如何使用 ASP.NET MVC 方案實作「使用 Microsoft 登入」，解決方案中包含使用 OpenID Connect 的傳統網頁瀏覽器型應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8368-104">This guide demonstrates how to implement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="f8368-105">在本指南最後，您的應用程式將能夠接受使用個人帳戶 (包括 outlook.com、live.com 和其他帳戶)，以及來自已經整合 Azure Active Directory 之公司或組織的公司與學校帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="f8368-105">At the end of this guide, your application will be able to accept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="f8368-106">本指南需要 Visual Studio 2015 Update 3 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="f8368-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="f8368-107">沒有嗎？</span><span class="sxs-lookup"><span data-stu-id="f8368-107">Don’t have it?</span></span>  [<span data-ttu-id="f8368-108">免費下載 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f8368-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="f8368-109">本指南使用方式</span><span class="sxs-lookup"><span data-stu-id="f8368-109">How this guide works</span></span>

![本指南使用方式](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="f8368-111">本指南是以透過瀏覽器存取 ASP.NET 網站，並要求使用者透過登入按鈕進行驗證的案例為基礎。</span><span class="sxs-lookup"><span data-stu-id="f8368-111">This guide is based on the scenario where a browser accesses an ASP.NET web site, requesting a user to authenticate via a sign-in button.</span></span> <span data-ttu-id="f8368-112">在這個案例中，大部分轉譯網頁的工作會在伺服器端執行。</span><span class="sxs-lookup"><span data-stu-id="f8368-112">In this scenario, most of the work to render the web page occurs on the server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="f8368-113">程式庫</span><span class="sxs-lookup"><span data-stu-id="f8368-113">Libraries</span></span>

<span data-ttu-id="f8368-114">本指南使用下列程式庫：</span><span class="sxs-lookup"><span data-stu-id="f8368-114">This guide uses the following libraries:</span></span>

|<span data-ttu-id="f8368-115">程式庫</span><span class="sxs-lookup"><span data-stu-id="f8368-115">Library</span></span>|<span data-ttu-id="f8368-116">描述</span><span class="sxs-lookup"><span data-stu-id="f8368-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="f8368-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="f8368-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="f8368-118">可讓應用程式使用 OpenIdConnect 進行驗證的中介軟體</span><span class="sxs-lookup"><span data-stu-id="f8368-118">Middleware that enables an application to use OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="f8368-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="f8368-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="f8368-120">可讓應用程式使用 Cookie 維持使用者工作階段的中介軟體</span><span class="sxs-lookup"><span data-stu-id="f8368-120">Middleware that enables an application to maintain user session using cookies</span></span>|
|[<span data-ttu-id="f8368-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="f8368-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="f8368-122">可讓 OWIN 型應用程式使用 ASP.NET 要求管線在 IIS 上執行</span><span class="sxs-lookup"><span data-stu-id="f8368-122">Enables OWIN-based applications to run on IIS using the ASP.NET request pipeline</span></span>|

