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
# <a name="call-hello-microsoft-graph-api-from-an-ios-app"></a>從 iOS 應用程式呼叫 hello Microsoft Graph API

本指南示範如何取得存取權杖和呼叫 hello Microsoft Graph API 或需要向 Azure Active Directory v2 端點的存取權杖的其他 Api 的原生 iOS 應用程式 (Swift)。

在 hello 本指南結尾，您的應用程式將會無法 toocall 受保護應用程式開發介面使用個人帳戶 （包括 outlook.com、 live.com 和其他項目），以及工作及學校帳戶，從任何的公司或組織有 Azure Active Directory。

> ### <a name="pre-requisites"></a>必要條件
> - 本指南需要 XCode 8.x。 您可以[從這裡](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode 下載 URL") 下載 XCode。
> - [Carthage](https://github.com/Carthage/Carthage) 以進行套件管理

### <a name="how-this-guide-works"></a>本指南使用方式

![本指南使用方式](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

本指南所建立的 hello 範例應用程式可讓 iOS 應用程式 tooquery hello Microsoft Graph API 或 Web API 可接受來自 Azure Active Directory v2 端點的語彙基元。 對於此案例中，權杖就會加入 tooHTTP 透過 hello 授權標頭的要求。 權杖取得和更新是由 hello Microsoft 驗證程式庫 (MSAL) 處理。


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>處理權杖取得以存取受保護的 Web API

Hello 使用者驗證之後，hello 範例應用程式會收到可使用的 tooquery hello Microsoft Graph API 或 Microsoft Azure Active Directory v2 所保護的 Web API 的語彙基元。

例如，Microsoft Graph 需要存取特定資源 – 例如，tooread 存取語彙基元 tooallow 使用者設定檔，Api 會存取使用者的行事曆，或傳送電子郵件。 您的應用程式可以使用 MSAL，以透過指定 API 範圍來要求存取權杖。 加入的 toohello hello 對所提出的每個呼叫的 HTTP 授權標頭的受保護資源，則此存取權杖。

MSAL 會為您管理快取和重新整理存取權杖，因此您的應用程式不需要執行這些作業。


### <a name="nuget-packages"></a>NuGet 套件

本指南會使用下列 NuGet 套件 hello:

|程式庫|說明|
|---|---|
|[MSAL.framework](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|適用於 iOS 的 Microsoft Authentication Library 預覽|

