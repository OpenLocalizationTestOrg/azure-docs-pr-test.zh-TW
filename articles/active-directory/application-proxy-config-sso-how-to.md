---
title: "aaaHow tooconfigure 單一登入 tooan 應用程式 Proxy 應用程式 |Microsoft 文件"
description: "如何快速地設定單一登入 tooyour 應用程式 proxy 應用程式"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: e1289203177c77b3a8bcc9058c5c0b8ae50f243e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-single-sign-on-tooan-application-proxy-application"></a>如何 tooconfigure 單一登入 tooan 應用程式 Proxy 應用程式

單一登入 (SSO) 允許使用者 tooaccess 應用程式而不需驗證多次。 它可讓 hello 單一驗證 toooccur 在 hello 雲端中，對 Azure Active Directory，並允許 hello 服務或連接器 tooimpersonate hello 使用者 toocomplete hello 應用程式從任何額外的驗證挑戰。

## <a name="how-tooconfigure-single-sign-on"></a>如何 tooconfigure 單一登入
tooconfigure SSO，首先請確定您的應用程式已設定為預先驗證透過 Azure Active Directory。 toodo，請移過**Azure Active Directory**  - &gt; **企業應用程式** - &gt; **所有應用程式**  - &gt;您的應用程式 **- &gt;應用程式 Proxy**。 在此頁面上，您會看見 hello [預先驗證] 欄位中，並確定太設定 「 Azure Active Directory。 

如需有關 hello 預先驗證方法的詳細資訊，請參閱 hello 的步驟 4[應用程式發行文件](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)。

   ![Azure 入口網站中的預先驗證方法](./media/application-proxy-config-sso-how-to/app-proxy.png)

## <a name="configuring-single-sign-on-modes-for-application-proxy-applications"></a>針對應用程式 Proxy 應用程式設定單一登入模式
接下來，我們設定 hello 特定類型的單一登入。 根據使用何種驗證 hello 後端應用程式分類 hello 登入方法。 應用程式 Proxy 應用程式支援三種登入類型：

-   **密碼型登入**： 密碼式登入可以用於任何使用使用者名稱和密碼欄位 toosign 上應用程式。 您可以在我們的[密碼 SSO 設定文件](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#bring-your-own-password-sso-applications)中找到設定步驟。

-   **整合式 Windows 驗證**：對於使用整合式 Windows 驗證 (IWA) 的應用程式，單一登入是透過 Kerberos 限制委派 (KCD) 來啟用。 這提供中 Active Directory tooimpersonate 使用者和 toosend 的應用程式 Proxy 連接器權限，並接收權杖，代表它們。 設定 KCD 的詳細資訊，請參閱 hello[單一登入 KCD 文件](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)。

-   **標頭形式的登入**：標頭形式的登入是透過合作關係啟用，並且需要一些額外設定。 如需 hello 合作關係與設定單一登入 tooan 應用程式使用標頭進行驗證的逐步指示的詳細資訊，請參閱 hello [Azure AD 文件的 PingAccess](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access)。

每個選項可以找到移 tooyour 應用程式 「 企業應用程式 」 及開啟 hello**單一登入**hello 左邊功能表上的頁面。 請注意，是否 hello 舊的入口網站中建立您的應用程式，您可能不會看到所有這些選項。

在此頁面上，您還會看到一個額外登入選項：連結的登入。 應用程式 Proxy 也支援此選項。 不過請注意此選項不會新增單一登入 toohello 應用程式。 話雖如此 hello 應用程式可能已經有單一登入使用另一個服務，例如 Active Directory 同盟服務實作。 

此選項可讓系統管理員 toocreate 連結 tooan 應用程式，使用者第一次進入存取 hello 應用程式時。 例如，如果沒有為應用程式設定使用 Active Directory Federation Services 2.0 tooauthenticate 使用者，系統管理員可以使用 hello 」 連結登入 選項 toocreate 連結 tooit hello 存取面板上。

## <a name="next-steps"></a>後續步驟
[提供單一登入 tooyour 應用程式與應用程式 Proxy](active-directory-application-proxy-sso-using-kcd.md)
