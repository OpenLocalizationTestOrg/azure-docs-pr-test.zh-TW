---
title: "在 Azure Active Directory B2B 共同作業的 aaaConfigure SaaS 應用程式 |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業的程式碼與 PowerShell 範例"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a>為 B2B 共同作業設定 SaaS 應用程式

Azure Active Directory (Azure AD) B2B 共同作業可搭配與 Azure AD 整合的大部分應用程式使用。 在本節中，我們將逐步說明用於設定一些常見 SaaS 應用程式以搭配 Azure AD B2B 使用的指示。

在您查看應用程式特定指示之前，以下是一些主要規則：

* 適用於大部分的 hello 應用程式，使用者安裝程式會以手動方式需要 toohappen。 亦即，使用者必須手動建立 hello 應用程式中。

* 支援自動安裝，例如 Dropbox 的應用程式從 hello 應用程式建立個別的邀請。 使用者必須確定 tooaccept 每個邀請。

* Hello 使用者屬性，toomitigate 中來賓使用者損害的使用者設定檔磁碟 (UPD) 的所有問題都設定**使用者識別碼**太**user.mail**。


## <a name="dropbox-business"></a>Dropbox Business

tooenable 使用者 toosign 中使用其組織帳戶，您必須手動設定 Dropbox 商務 toouse Azure AD 做為安全性聲明標記語言 (SAML) 身分識別提供者。 如果尚未設定的 toodo Dropbox 商務。 因此，它無法提示或否則允許使用者 toosign 中使用 Azure AD。

1. tooadd hello Dropbox 商務應用程式到 Azure AD 中，選取**企業應用程式**在 hello 左的窗格，然後按一下**新增**。

  ![hello hello 企業應用程式 頁面上的 新增 按鈕](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. 在 hello**新增應用程式**視窗中，輸入**dropbox**在 hello 搜尋方塊，然後選取  **dropbox 企業版**hello 結果 清單中。

  ![搜尋"dropbox"hello 上新增的應用程式頁面](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. 在 hello**單一登入**頁面上，選取**單一登入**在 hello 左的窗格，然後輸入**user.mail**在 hello**使用者識別碼**方塊。 (其預設為 UPN。)

  ![設定單一登入 hello 應用程式](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. toodownload hello 憑證 toouse Dropbox 組態選取**設定 DropBox**，然後選取**SAML 單一登入服務 URL** hello 清單中。

  ![下載 hello Dropbox 設定憑證](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. 登入以 hello tooDropbox 登入 URL 從 hello**單一登入**頁面。

  ![hello Dropbox 登入頁面](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. 在 hello 功能表中，選取 **管理主控台**。

  ![hello hello Dropbox 功能表上的 「 系統管理員主控台 」 連結](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. 在 hello**驗證**對話方塊中，選取**詳細**，hello 憑證上傳，然後在 hello**登入 URL**方塊中，輸入 hello SAML 單一登入 URL。

  ![hello hello 摺疊 [驗證] 對話方塊中的"More"連結](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![hello 」 登入 URL"hello 中的擴充驗證 對話方塊](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. tooconfigure hello Azure 入口網站中的使用者自動安裝程式選取**佈建**hello 左窗格中，選取**自動**在 hello**佈建模式**方塊，並選取**授權**。

  ![設定自動使用者佈建在 hello Azure 入口網站](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

Hello Dropbox 應用程式中已設定客體或成員的使用者之後，他們會收到個別的邀請，從 Dropbox。 toouse Dropbox 單一登入，受邀者必須接受 hello 邀請中的連結即可。

## <a name="box"></a>Box
您可以使用 hello SAML 通訊協定為基礎的同盟，以啟用使用者 tooauthenticate 方塊 guest 使用者以 Azure AD 帳戶。 在此程序，您上傳中繼資料 tooBox.com。

1. 從 hello 企業應用程式中加入 hello Box 應用程式。

2. 在 hello 順序中，以設定單一登入：

  ![設定 Box 單一登入](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 a. 在 hello**登入 URL**方塊中，確定 hello 登入 URL 已設定適當的方塊 hello Azure 入口網站中。 此 URL 是 hello Box.com 租用戶 URL。 它應該遵循命名慣例的 hello *https://.box.com*。  
 hello**識別碼**不適 toothis 應用程式，但它仍會顯示為必要欄位。

 b. 在 hello**使用者識別碼**方塊中，輸入**user.mail** （適用於來賓帳戶的 SSO)。

 c. 在 [SAML 簽署憑證] 之下，按一下 [建立新憑證]。

 d. 設定您 Box.com 租用戶 toouse Azure AD 身分識別提供者的 toobegin 下載 hello 中繼資料檔案，並儲存它 tooyour 本機磁碟機。

 e. 轉送 hello 中繼資料檔案 toohello 方塊支援小組，以單一登入您的設定。

3. Azure AD 使用者自動安裝，hello 左窗格中，選取**佈建**，然後選取**授權**。

  ![授權 Azure AD tooconnect tooBox](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

Dropbox 受邀者，例如方塊受邀者必須兌換邀請他們 hello Box 應用程式。

## <a name="next-steps"></a>後續步驟

請參閱下列 Azure AD B2B 共同作業的發行項的 hello:

* [何謂 Azure AD B2B 共同作業？](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B 共同作業使用者屬性](active-directory-b2b-user-properties.md)
* [新增 B2B 共同作業使用者 tooa 角色](active-directory-b2b-add-guest-to-role.md)
* [委派 B2B 共同作業邀請](active-directory-b2b-delegate-invitations.md)
* [動態群組與 B2B 共同作業](active-directory-b2b-dynamic-groups.md)
* [B2B 共同作業程式碼與 PowerShell 範例](active-directory-b2b-code-samples.md)
* [B2B 共同作業使用者權杖](active-directory-b2b-user-token.md)
* [B2B 共同作業使用者宣告對應](active-directory-b2b-claims-mapping.md)
* [Office 365 外部共用](active-directory-b2b-o365-external-user.md)
* [B2B 共同作業目前的限制](active-directory-b2b-current-limitations.md)
