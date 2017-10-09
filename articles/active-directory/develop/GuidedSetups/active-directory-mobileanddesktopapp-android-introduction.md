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
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a>從 Android 應用程式呼叫 hello Microsoft Graph API

本指南示範原生 Android 應用程式如何取得存取權杖，以及如何呼叫 Microsoft 圖形 API 或需要來自 Azure Active Directory v2 端點之存取權杖的其他 API。

在 hello 本指南結尾，您的應用程式將會無法 toocall 受保護應用程式開發介面使用個人帳戶 （包括 outlook.com、 live.com 和其他項目），以及工作及學校帳戶，從任何的公司或組織有 Azure Active Directory。  

### <a name="how-this-sample-works"></a>這個範例的運作方式
![這個範例的運作方式](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

本指南所建立的 hello 範例根據的案例，其中的 Android 應用程式是使用的 tooquery Web API 可接受來自 Azure Active Directory v2 端點 – 在此情況下，Microsoft Graph API 的語彙基元。 對於此案例中，權杖就會加入 tooHTTP 透過 hello 授權標頭的要求。 權杖取得和更新是由 hello Microsoft 驗證程式庫 (MSAL) 處理。

### <a name="pre-requisites"></a>必要條件
* 本引導式設定著重在 Android Studio，但也可以接受任何其他 Android 應用程式開發環境。 
* 需要 Android SDK 21 或更新版本 (建議使用 SDK 25)。
* 這個 Android 版的 Microsoft Authentication Library (MSAL) 版本需要 Google Chrome 或使用「自訂索引標籤」的網頁瀏覽器。

> 注意：Visual Studio 的 Android 模擬器中未包括 Google Chrome。 我們建議您 tootest 的模擬器，應用程式開發介面 25 或映像 API 21 或更新版本已使用 Google Chrome 安裝此程式碼。


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a>如何 toohandle 語彙基元擷取 tooaccess 受保護的 Web API

Hello 使用者驗證之後，hello 範例應用程式會收到可使用的 tooquery Microsoft Graph API 或 Microsoft Azure Active Directory v2 所保護的 Web API 的語彙基元。

例如，Microsoft Graph 需要存取特定資源 – 例如，tooread 存取語彙基元 tooallow 使用者設定檔，Api 會存取使用者的行事曆，或傳送電子郵件。 您的應用程式可以要求存取權杖使用 MSAL tooaccess 這些資源指定應用程式開發介面的範圍。 加入的 toohello hello 對所提出的每個呼叫的 HTTP 授權標頭的受保護資源，則此存取權杖。 

MSAL 會為您管理快取和重新整理存取權杖，因此您的應用程式不需要執行這些作業。

### <a name="libraries"></a>程式庫

本指南會使用下列程式庫的 hello:

|程式庫|描述|
|---|---|
|[com.microsoft.identity.client (英文)](http://javadoc.io/doc/com.microsoft.identity.client/msal)|Microsoft Authentication Library (MSAL)|
