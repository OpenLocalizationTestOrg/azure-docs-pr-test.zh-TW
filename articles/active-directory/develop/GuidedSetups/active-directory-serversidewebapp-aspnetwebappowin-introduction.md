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
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a>新增 Microsoft tooan ASP.NET web 應用程式使用登入

本指南示範如何 tooimplement 使用登入 Microsoft 與傳統 web 瀏覽器型應用程式使用 OpenID Connect 使用 ASP.NET MVC 方案。 

在本指南的 hello 結尾，您的應用程式會無法 tooaccept 符號集個人的帳戶 （包括 outlook.com、 live.com 和其他項目），以及運作並學校帳戶，從任何的公司或組織與 Azure Active Directory 整合。 

> 本指南需要 Visual Studio 2015 Update 3 或 Visual Studio 2017。  沒有嗎？  [免費下載 Visual Studio 2017](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a>本指南使用方式

![本指南使用方式](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

本指南根據 hello 案例中，瀏覽器存取的 ASP.NET 網站上，要求使用者 tooauthenticate 透過登入 按鈕。 在此案例中，大部分的 hello 工作 toorender hello 網頁上發生 hello 伺服器端。

## <a name="libraries"></a>程式庫

本指南會使用下列程式庫的 hello:

|程式庫|描述|
|---|---|
|[Microsoft.Owin.Security.OpenIdConnect](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|可讓應用程式 toouse OpenIdConnect 驗證中介軟體|
|[Microsoft.Owin.Security.Cookies](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|中介軟體，可讓使用 cookie 的應用程式 toomaintain 使用者工作階段|
|[Microsoft.Owin.Host.SystemWeb](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|啟用 OWIN 應用程式 toorun 於 IIS 使用 hello ASP.NET 要求管線|

