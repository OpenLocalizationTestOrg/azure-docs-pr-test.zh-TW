---
title: "aaaAzure AD v2 JS SPA 引導式安裝-簡介 |Microsoft 文件"
description: "JavaScript SPA 應用程式如何呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
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
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a>呼叫 hello Microsoft Graph API 從 JavaScript 單一頁面應用程式 (SPA)

本指南示範如何 JavaScript 單一頁面應用程式 (SPA) 可以登入 [個人] 的工作及學校帳戶，取得存取權杖，並呼叫 hello Microsoft Graph API 或需要存取權杖，從其他應用程式開發介面 hello Azure Active Directory v2 端點。

### <a name="how-this-guide-works"></a>本指南使用方式

![本指南所產生的 hello 範例應用程式的運作方式](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a>相關資訊

本指南所建立的 hello 範例應用程式可讓 JavaScript SPA tooquery hello Microsoft Graph API 或 Web API 可接受來自 Azure Active Directory v2 端點的語彙基元。 此案例中，登入時的使用者存取權杖是透過 hello 授權標頭的要求和加入 tooHTTP 要求。 Hello Microsoft 驗證程式庫 (MSAL) 會處理權杖取得及更新。

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a>程式庫

本指南會使用下列程式庫的 hello:

|程式庫|說明|
|---|---|
|[msal.js](https://github.com/AzureAD/microsoft-authentication-library-for-js)|Microsoft Authentication Library for JavaScript 預覽|

> [!NOTE]
> *msal.js*目標 hello *Azure Active Directory v2 端點*-這可讓個人、 學校和工作帳戶 toosign 中的並取得語彙基元。 hello *Azure Active Directory v2 端點*具有[一些限制](..\active-directory-v2-limitations.md)。 如果您只有興趣學校和工作帳戶，請使用*adal.js*和 hello *V1 端點*。 toounderstand hello v1 和 v2 端點之間的差異讀取 hello [v1 v2 比較](..\active-directory-v2-compare.md)。

<!--end-collapse-->
