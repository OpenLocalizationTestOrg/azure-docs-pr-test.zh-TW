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
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a>從 Windows 桌面應用程式呼叫 hello Microsoft Graph API

本指南示範原生 Windows Desktop .NET (XAML) 應用程式如何取得存取權杖，以及如何呼叫 Microsoft 圖形 API 或需要來自 Azure Active Directory v2 端點之存取權杖的其他 API。

在 hello 本指南結尾，您的應用程式將會無法 toocall 受保護應用程式開發介面使用個人帳戶 （包括 outlook.com、 live.com 和其他項目），以及工作及學校帳戶，從任何的公司或組織有 Azure Active Directory。  

> 本指南需要 Visual Studio 2015 Update 3 或 Visual Studio 2017。  沒有嗎？ [免費下載 Visual Studio 2017](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a>本指南使用方式

![本指南使用方式](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

本指南所建立的 hello 範例應用程式可讓 Windows 桌面應用程式 tooquery Microsoft Graph API 或 Web API 可接受來自 Azure Active Directory v2 端點的語彙基元。 對於此案例中，權杖就會加入 tooHTTP 透過 hello 授權標頭的要求。 權杖取得和更新是由 hello Microsoft 驗證程式庫 (MSAL) 處理。


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>處理權杖取得以存取受保護的 Web API

Hello 使用者驗證之後，hello 範例應用程式會收到可使用的 tooquery Microsoft Graph API 或 Microsoft Azure Active Directory v2 所保護的 Web API 的語彙基元。

例如，Microsoft Graph 需要存取特定資源 – 例如，tooread 存取語彙基元 tooallow 使用者設定檔，Api 會存取使用者的行事曆，或傳送電子郵件。 您的應用程式可以要求存取權杖使用 MSAL tooaccess 這些資源指定應用程式開發介面的範圍。 加入的 toohello hello 對所提出的每個呼叫的 HTTP 授權標頭的受保護資源，則此存取權杖。 

MSAL 會為您管理快取和重新整理存取權杖，因此您的應用程式不需要執行這些作業。


### <a name="nuget-packages"></a>NuGet 套件

本指南會使用下列 NuGet 套件 hello:

|程式庫|描述|
|---|---|
|[Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client)|Microsoft Authentication Library (MSAL)|

