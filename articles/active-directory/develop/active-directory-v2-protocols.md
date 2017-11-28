---
title: "關於 hello 授權通訊協定支援的 Azure AD v2.0 aaaLearn |Microsoft 文件"
description: "指南 tooprotocols，hello Azure AD v2.0 端點所支援。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5fb4fa1b-8fc4-438e-b3b0-258d8c145f22
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: f90511b1880ff223f725c1f79df9f79bddccc7bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# v2.0 通訊協定 - OAuth 2.0 與 OpenID Connect
hello v2.0 端點可以使用 Azure AD 身分識別做為服務使用業界標準通訊協定，OpenID Connect 和 OAuth 2.0。  Hello 服務符合標準時，可以是任何兩個實作這些通訊協定之間的些微差異。  如果您直接傳送給選擇 toowrite 您的程式碼 （& s） 處理 HTTP 要求或使用第 3 合作對象開啟原始碼程式庫，而不是使用我們的開放原始碼程式庫的一個 hello 資訊將非常有用。
<!-- TODO: Need link toolibraries above -->

> [!NOTE]
> 並非所有的 Azure Active Directory 案例和功能都受到 hello v2.0 端點。  toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
>
>

## hello 基本概念
在幾乎所有的 OAuth 和 OpenID Connect 流程中有四個合作對象以 hello exchange:

![OAuth 2.0 角色](../../media/active-directory-v2-flows/protocols_roles.png)

* hello**授權伺服器**hello v2.0 端點。  它負責確保 hello 使用者的身分識別、 授與及撤銷存取 tooresources 以及簽發權杖。  它也稱為 hello 身分識別提供者-它安全地處理的任何項目 toodo hello 使用者資訊、 與它們存取權，hello 流程中的合作對象之間的信任關係。
* hello**資源擁有者**通常是 hello 使用者。  它是擁有 hello 資料，且具有 hello 電源 tooallow hello 合作對象第三方 tooaccess，該資料或資源。
* hello **OAuth 用戶端**是您的應用程式中，然後再由其應用程式識別碼。它通常是 hello 合作對象 hello 使用者互動，，和來自 hello 授權伺服器要求語彙基元。  hello 用戶端必須授與權限 tooaccess hello 資源 hello 資源擁有者。
* hello**資源伺服器**是 hello 資源或資料所在的位置。  它會信任 hello toosecurely 驗證和授權 hello OAuth 用戶端，授權伺服器，並使用可授與存取 tooa 資源的 access_tokens tooensure 承載。

## App 註冊
每個使用 hello v2.0 端點的應用程式需要在註冊 toobe [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)之前它可以使用 OAuth 或 OpenID Connect 對其進行互動。  hello 應用程式登錄程序將會收集與指派少數值 tooyour 應用程式：

* 可唯一識別應用程式的 **應用程式 ID**
* A**重新導向 URI**或**封裝識別碼**可以使用的 toodirect 回應後 tooyour 應用程式
* 其他幾個狀況特定的值。

如需詳細資訊，了解如何太[註冊應用程式](active-directory-v2-app-registration.md)。

## 端點
一旦註冊，hello 應用程式將會傳送要求 toohello v2.0 端點通訊與 Azure AD:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

其中 hello`{tenant}`可以採用四個不同值的其中一個：

| 值 | 說明 |
| --- | --- |
| `common` |可讓使用者使用個人 Microsoft 帳戶和工作/學校帳戶，從 Azure Active Directory toosign hello 應用程式。 |
| `organizations` |僅允許使用者與工作/學校帳戶，從 Azure Active Directory toosign hello 應用程式。 |
| `consumers` |僅允許使用者使用個人 Microsoft 帳戶 (MSA) toosign hello 應用程式。 |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` 或 `contoso.onmicrosoft.com` |僅允許使用者與工作/學校帳戶，從特定的 Azure Active Directory 租用戶 toosign hello 應用程式。  Hello 好記的網域名稱的 hello Azure AD 租用戶，或是可以用 hello 租用戶的 guid 識別碼。 |

如需有關如何與這些端點，toointeract 選擇下方的特定應用程式類型。

## 權杖
hello v2.0 實作 OAuth 2.0 和 OpenID Connect 會大量使用 bearer 權杖，包括以 Jwt 表示的持有者權杖。 承載權杖是輕巧型的安全性權杖會授與 hello"bearer"存取 tooa 受保護資源。 就這個意義而言，hello"bearer"是指可出示 hello 語彙基元任何一方。 合作對象必須先通過驗證 Azure AD tooreceive hello 持有者權杖，必要時 hello toosecure 傳輸和儲存體中的 hello 語彙基元不採取步驟，但它可以攔截和使用非預期的合作對象。 雖然某些安全性權杖都有內建的機制，可防止未經授權的人士使用權杖，但持有者權杖沒有這項機制，而必須以安全通道來傳輸，例如傳輸層安全性 (HTTPS)。 持有人權杖傳送 hello 清除中時，如果攔截 hello 攻擊可由惡意的合作對象 tooacquire hello 語彙基元，並使用未經授權的存取 tooa 受保護資源的。 hello 儲存或快取持有者權杖供以後使用時，適用相同的安全性原則。 務必確定您的應用程式以安全的方式傳輸和儲存持有人權杖。 關於持有者權杖的其他安全性考量，請參閱 [RFC 6750 第 5 節](http://tools.ietf.org/html/rfc6750)。

不同類型的語彙基元 hello v2.0 端點中使用的進一步詳細資料位於[hello v2.0 端點權杖參照](active-directory-v2-tokens.md)。

## 通訊協定
如果您已準備好 toosee 某些範例要求，開始使用其中一個 hello 下列教學課程。  每一個對應 tooa 特定的驗證案例。  如果您需要決定哪一個 hello 右流程為您的協助，請參閱[hello 類型的應用程式可以使用 hello v2.0 建置](active-directory-v2-flows.md)。

* [使用 OAuth 2.0 建置行動與原生應用程式](active-directory-v2-protocols-oauth-code.md)
* [使用 OpenID Connect 建置 Web 應用程式](active-directory-v2-protocols-oidc.md)
* [使用 OAuth 2.0 隱含流程 hello 建置單一頁面應用程式](active-directory-v2-protocols-implicit.md)
* [使用 OAuth 2.0 用戶端認證流程 hello 建置精靈或伺服器端處理程序](active-directory-v2-protocols-oauth-client-creds.md)
* [取得語彙基元中 Web API 以 hello OAuth 2.0 On 代表的流程](active-directory-v2-protocols-oauth-on-behalf-of.md)
