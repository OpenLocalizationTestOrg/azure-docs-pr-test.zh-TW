---
title: "Azure AD Application Proxy 的 SSO aaaManage |Microsoft 文件"
description: "深入了解的單一登入應用程式 proxy 的 hello 基本概念"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: a278751a5cb1bf98c970a4e5d2eb3edc3b784096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a>Azure AD 應用程式 Proxy 如何提供單一登入？

單一登入是 Azure AD 應用程式 Proxy 的重要元素。  因為您的使用者只能有 toosign tooAzure hello 雲端中的 Active Directory 中，它會提供 hello 最佳使用者體驗。 一旦驗證 tooAzure Active Directory hello 應用程式 Proxy 連接器處理 hello 驗證 toohello 在內部部署應用程式。 hello 後端應用程式無法分辨 hello 遠端使用者透過應用程式 Proxy 與一般情況下使用已加入網域的裝置上登入之間的差異。 

toouse Azure Active Directory 的單一登入 tooyour 應用程式，您需要 tooselect **Azure Active Directory** hello 預先驗證方法。 如果您選取**通過**則您的使用者未完全驗證 tooAzure Active Directory，但是會導向直線 toohello 應用程式。 當您第一次發行的應用程式，或瀏覽 tooyour hello Azure 入口網站中的應用程式編輯 hello 應用程式 Proxy 設定，您可以設定這項設定。 

toosee 單一登入選項，請遵循下列步驟：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 瀏覽過**Azure Active Directory** > **企業應用程式** > **所有應用程式**。
3. 選取 hello 應用程式的單一登入選項想 toomanage。
4. 選取 [單一登入]。

   ![SSO 下拉式功能表](./media/application-proxy-sso-overview/single-sign-on-mode.png)

hello 下拉式清單中的功能表會顯示為單一登入 tooyour 應用程式的五個選項：

* 已啟用 Azure AD 單一登入
* 密碼型登入
* 連結型登入
* 整合式 Windows 驗證
* 標頭型登入

## <a name="azure-ad-single-sign-on-disabled"></a>已啟用 Azure AD 單一登入

如果您不想 toouse 單一登入 tooyour 應用程式的 Azure Active Directory 整合，請選擇**Azure AD 單一登入已停用**。 選取此選項後，使用者可能會進行兩次驗證。 首先，它們會驗證 tooAzure Active Directory，並再登入 toohello 應用程式本身。 

如果在內部部署應用程式不需要使用者 tooauthenticate，但是您想要 tooadd Azure Active Directory 安全性層級為遠端存取，此選項是不錯的選擇。 

## <a name="password-based-sign-on"></a>密碼型登入

如果您想要 toouse Azure Active Directory 與密碼保存庫在內部部署應用程式，選擇**密碼式登入**。 如果您的應用程式使用使用者名稱/密碼組合 (而不是存取權杖或標頭) 進行驗證，此選項是個不錯的選擇。 使用密碼型登入，您的使用者需要 toosign toohello 應用程式 hello 中的第一次存取它。 在這之後，Azure Active Directory 會代表 hello 使用者提供 hello 使用者名稱和密碼。 

如需設定密碼型登入的詳細資訊，請參閱[使用應用程式 Proxy 單一登入的密碼保存庫](application-proxy-sso-azure-portal.md)。

## <a name="linked-sign-on"></a>連結型登入

如果您已經有為您的內部部署身分識別設定的單一登入解決方案，請選擇 [連結型登入]。 此選項可讓 Azure Active Directory tooleverage 現有 SSO 解決方案，但是遠端存取 toohello 應用程式仍可讓您的使用者。 

如需連結登入 (先前稱為現有單一登入) 的詳細資訊，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)。

## <a name="integrated-windows-authentication"></a>整合式 Windows 驗證

如果您在內部部署應用程式使用整合式 Windows Authentication(IWA) 或您想 toouse Kerberos 限制委派 (KCD) 的單一登入，選擇 **整合式 Windows 驗證**。 使用此選項，您的使用者只需要 tooauthenticate tooAzure Active Directory，並接著 hello 應用程式 Proxy 連接器模擬 hello 使用者 tooget Kerberos 權杖並 toohello 應用程式中的登入。 

如需設定整合式 Windows 驗證的詳細資訊，請參閱 [使用應用程式 Proxy 單一登入的 Kerberos 限制委派](active-directory-application-proxy-sso-using-kcd.md)。

## <a name="header-based-sign-on"></a>標頭型登入 

如果應用程式使用標頭進行驗證，請選擇 [標頭型登入]。 使用此選項，您的使用者只需要 tooauthentication hello Azure Active Directory。 與協力廠商驗證服務的 Microsoft 合作夥伴呼叫 PingAccess，轉譯成 hello 應用程式標頭格式的 hello Azure Active Directory 存取權杖。 

如需設定標頭型驗證的相關資訊，請參閱[使用應用程式 Proxy 單一登入的標頭型驗證](application-proxy-ping-access.md)。

## <a name="next-steps"></a>後續步驟

- [使用應用程式 Proxy 進行單一登入的密碼保存庫](application-proxy-sso-azure-portal.md)
- [可供使用應用程式 Proxy 單一登入的 Kerberos 限制委派](active-directory-application-proxy-sso-using-kcd.md)
- [使用應用程式 Proxy 單一登入的標頭型驗證](application-proxy-ping-access.md) 
