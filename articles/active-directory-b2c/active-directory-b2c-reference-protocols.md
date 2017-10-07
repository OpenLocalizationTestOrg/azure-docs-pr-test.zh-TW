---
title: "Azure Active Directory B2C：驗證通訊協定 | Microsoft Docs"
description: "如何 toobuild 應用程式是直接使用 hello 通訊協定所支援的 Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5e407d0a-73a2-4d74-ac81-3aa6c31ddcee
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 8fa4cbebe711841d410b3ae43b78f893c06d9b63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# Azure AD B2C：驗證通訊協定
Azure Active Directory B2C (Azure AD B2C) 支援 OpenID Connect 與 OAuth 2.0 兩種業界標準通訊協定，為您的 app 提供身分識別即服務。 hello 服務符合標準，但是這些通訊協定的任何兩個實作都可以有只有些微的差異。 

本指南中的 hello 資訊非常有用，如果您撰寫程式碼，透過直接傳送和處理 HTTP 要求，而不是使用開放原始碼程式庫。 我們建議您閱讀這個頁面之前您深入了解的每個特定的通訊協定的 hello 詳細資料。 但如果您已熟悉 Azure AD B2C，您可以直接太[hello 通訊協定參考指南](#protocols)。

<!-- TODO: Need link toolibraries above -->

## hello 基本概念
使用 Azure AD B2C 每個應用程式需要 toobe hello B2C 目錄中註冊[Azure 入口網站](https://portal.azure.com)。 hello 應用程式登錄程序會收集，並將幾個值 tooyour 應用程式：

* 可唯一識別應用程式的 **應用程式識別碼** 。
* A**重新導向 URI**或**封裝識別碼**可以使用的 toodirect 回應後 tooyour 應用程式。
* 其他幾個狀況特定的值。 如需詳細資訊，了解[如何 tooregister 您的應用程式](active-directory-b2c-app-registration.md)。

註冊您的應用程式後，通訊與 Azure Active Directory (Azure AD) 傳送要求 toohello 端點：

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

幾乎所有 OAuth 和 OpenID Connect 的流量，四個合作對象都是參與 hello exchange:

![OAuth 2.0 角色](./media/active-directory-b2c-reference-protocols/protocols_roles.png)

* hello**授權伺服器**hello Azure AD 端點。 它會安全地處理的任何項目相關的 toouser 資訊和存取。 它也會處理 hello 資料流程中的 hello 合作對象之間的信任關係。 它負責驗證 hello 使用者的身分識別、 授與及撤銷存取 tooresources 以及簽發權杖。 它也稱為是 hello 身分識別提供者。

* hello**資源擁有者**通常是 hello 終端使用者。 Hello 合作對象擁有 hello 資料，以及它具有 hello 電源 tooallow 第三方 tooaccess 資料或資源。

* hello **OAuth 用戶端**是您的應用程式。 它是透過其應用程式識別碼來識別。 它通常是與使用者互動的 hello 合作對象。 它也會要求來自 hello 授權伺服器的權杖。 hello 資源擁有者必須授與 hello 用戶端權限 tooaccess hello 資源。

* hello**資源伺服器**是 hello 資源或資料所在的位置。 信任 hello 授權伺服器 toosecurely 驗證和授權 hello OAuth 用戶端。 它也會使用可以授與存取 tooa 資源的語彙基元 tooensure 的持有人存取權。

## 原則
在論證上，Azure AD B2C 原則是 hello hello 服務最重要功能。 Azure AD B2C 藉由引進原則延伸 hello 標準 OAuth 2.0 和 OpenID Connect 通訊協定。 這些選項可讓 Azure AD B2C tooperform 更多簡單驗證及授權。 

原則可完整描述取用者身分識別體驗，包括註冊、登入及設定檔編輯。 原則可定義於系統管理 UI 中。 您可以在 HTTP 驗證要求中使用特定的查詢參數來執行原則。 

原則不是標準功能的 OAuth 2.0 和 OpenID Connect，所以您應該採取 hello 時間 toounderstand 它們。 如需詳細資訊，請參閱 hello [Azure AD B2C 原則參考指南](active-directory-b2c-reference-policies.md)。

## 權杖
hello Azure AD B2C OAuth 2.0 和 OpenID Connect 實作會大量地使用 bearer 權杖，包括會以 JSON web 權杖 (Jwt) 表示的持有者權杖。 承載權杖是輕巧型的安全性權杖會授與 hello"bearer"存取 tooa 受保護資源。

hello 持有者是指可出示 hello 語彙基元任何一方。 Azure AD 必須先驗證合作對象，才能接收持有人權杖。 但是，它在 hello 必要步驟不會採用 toosecure 傳輸和儲存體中的 hello 語彙基元可以攔截和使用的非預期的合作對象。

某些安全性權杖有內建的機制，可防止未授權的合作對象使用它們，但持有人權杖沒有這項機制。 它們必須在安全的通道 (例如傳輸層安全性 (HTTPS)) 中傳輸。 

持有人權杖傳輸到外部安全通道，如果惡意人士可以使用攔截攻擊 tooacquire hello 語彙基元，並使用它 toogain 未經授權存取 tooa 受保護的資源。 當您儲存或快取供稍後使用持有者權杖時，適用相同的安全性原則的 hello。 務必確定您的應用程式以安全的方式傳輸和儲存持有人權杖。

如需持有人權杖的其他安全性考量，請參閱 [RFC 6750 第 5 節](http://tools.ietf.org/html/rfc6750)。

Azure AD B2C 中所使用的語彙基元的 hello 不同類型的相關資訊可用於[hello Azure AD 的權杖參照](active-directory-b2c-reference-tokens.md)。

## 通訊協定
當您準備好 tooreview 某些範例要求時，就可以開始一個 hello 遵循教學課程。 每一個都對應 tooa 特定的驗證案例。 如果您需要判斷哪一個流程最適合您的協助，請參閱[hello 類型的應用程式，您可以使用 Azure AD B2C 建置](active-directory-b2c-apps.md)。

* [使用 OAuth 2.0 建置行動與原生應用程式](active-directory-b2c-reference-oauth-code.md)
* [使用 OpenID Connect 建置 Web 應用程式](active-directory-b2c-reference-oidc.md)
* [建置使用 hello OAuth 2.0 隱含流程的單一頁面應用程式](active-directory-b2c-reference-spa.md)

