---
title: "aaaListing hello Azure Active Directory 應用程式庫中的應用程式"
description: "Toolist 支援單一登入的應用程式如何 hello Azure Active Directory 庫 |Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a>列出在 hello Azure Active Directory 應用程式庫中的應用程式
toolist hello 中支援單一登入與 Azure Active Directory 的應用程式[Azure AD 資源庫](https://azure.microsoft.com/marketplace/active-directory/all/)，hello 應用程式第一次需要 hello 下列整合模式的其中一個 tooimplement:

* **OpenID Connect** -直接整合與 Azure AD 使用 OpenID Connect 來進行驗證並 hello 組態的 Azure AD 同意應用程式開發介面。 如果您剛開始整合您的應用程式不支援 SAML，這是 hello 建議模式。
* **SAML** – 您的應用程式已擁有 hello 能力 tooconfigure 協力廠商身分識別提供者使用 hello SAML 通訊協定。

每個模式的列出需求如下。

## <a name="openid-connect-integration"></a>OpenID Connect 整合
toointegrate 應用程式與 Azure AD，下列 hello[開發人員指示](active-directory-authentication-scenarios.md)。 然後完成 hello 回答以下問題和傳送toowaadpartners@microsoft.com。

* 提供可供 hello Azure AD team tootest hello 整合的應用程式中的測試租用戶或帳戶的認證。  
* 提供有關如何 hello Azure AD 的小組可以登入和連接的 Azure AD 使用 hello 的 tooyour 應用程式執行個體的指示[Azure AD 的同意架構](active-directory-integrating-applications.md#overview-of-the-consent-framework)。 
* 提供所需的 hello Azure AD 的任何進一步指示小組 tootest 單一登入您的應用程式。 
* 提供下列 hello 資訊：

> 公司名稱：
> 
> 公司網站：
> 
> 應用程式名稱：
> 
> 應用程式描述 (200 個字元的限制)：
> 
> 應用程式網站 (資訊)：
> 
> 應用程式技術支援網站或連絡資訊：
> 
> 應用程式識別碼 hello 應用程式，在 https://portal.azure.com hello 應用程式詳細資料中所示：
> 
> 客戶尋求 toosign 註冊應用程式註冊 URL 和/或購買 hello 應用程式：
> 
> 選擇您的應用程式 toobe （如可用的類別目錄，請參閱 Azure Active Directory Marketplace hello） 底下所列的 toothree 類別：
> 
> 附加應用程式小型圖示 (PNG 檔案、45px x 45px、背景純色)：
> 
> 附加應用程式大型圖示 (PNG 檔案、215px x 215px、背景純色)：
> 
> 附加應用程式標誌 (PNG 檔案、150px x 122px、透明背景色彩)：
> 
> 

## <a name="saml-integration"></a>SAML 整合
支援 SAML 2.0 的任何應用程式可直接與使用 Azure AD 租用戶整合[這些指示 tooadd 自訂應用程式](../active-directory-saas-custom-apps.md)。 一旦您已經測試過您的應用程式整合搭配 Azure AD，傳送下列資訊太 hello<mailto:waadpartners@microsoft.com>。

* 提供可供 hello Azure AD team tootest hello 整合的應用程式中的測試租用戶或帳戶的認證。  
* 提供 hello SAML 登入 URL，簽發者 URL (實體 ID) 和應用程式的回覆 URL （判斷提示取用者服務） 值，如所述[這裡](../active-directory-saas-custom-apps.md)。 如果您通常會提供這些值做為一個 SAML 中繼資料檔的一部分，也請一併傳送該檔案。
* 提供如何的簡短描述 tooconfigure Azure AD 作為身分識別提供者使用 SAML 2.0 的應用程式中。 如果您的應用程式支援設定的 Azure AD 作為身分識別提供者透過自助系統管理網站，然後請確定 hello 以上所提供的認證包含 hello 能力 tooset 其設定。
* 提供下列 hello 資訊：

> 公司名稱：
> 
> 公司網站：
> 
> 應用程式名稱：
> 
> 應用程式描述 (200 個字元的限制)：
> 
> 應用程式網站 (資訊)：
> 
> 應用程式技術支援網站或連絡資訊：
> 
> 客戶尋求 toosign 註冊應用程式註冊 URL 和/或購買 hello 應用程式：
> 
> 選擇您的應用程式 toobe 底下所列的 toothree 類別 (如可用的類別目錄，請參閱 hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):
> 
> 附加應用程式小型圖示 (PNG 檔案、45px x 45px、背景純色)：
> 
> 附加應用程式大型圖示 (PNG 檔案、215px x 215px、背景純色)：
> 
> 附加應用程式標誌 (PNG 檔案、150px x 122px、透明背景色彩)：
> 
> 

