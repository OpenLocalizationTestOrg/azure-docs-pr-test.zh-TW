---
title: "設定密碼單一登入 Azure AD 庫應用程式的 aaaProblem |Microsoft 文件"
description: "當您設定密碼單一登入的應用程式，已列出 hello Azure AD 應用程式庫中，了解 hello 一般問題的人臉"
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
ms.openlocfilehash: 78c37c52453c375bf7ccbca6df5c9008be4ce642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-an-azure-ad-gallery-application"></a>為 Azure AD 資源庫應用程式設定密碼單一登入時遇到的問題

本文協助您 toounderstand hello 一般問題的人臉設定時**密碼單一登入**與 Azure AD 庫應用程式。

## <a name="credentials-are-filled-in-but-hello-extension-does-not-submit-them"></a>認證會填入，但 hello 延伸模組未送出

這通常發生 hello 應用程式廠商已變更其登入頁面上最近 tooadd 欄位、 變更基礎的識別項，我們使用 toodetect hello 使用者名稱和密碼欄位，或修改 hello 登入體驗運作他們的應用程式的方式。 幸運的是，在許多情況下，Microsoft 可與應用程式廠商 toorapidly 解決這些問題。

Microsoft 有技術 tooautomatically 這些整合中斷，但有時候我們不能 toofind 時偵測到這些問題右離開，或者它們需要一些時間 toofix。 萬一 hello 當其中一個這些整合功能無法正常運作，我們非常感謝如果您開啟支援案例，以便我們可以盡快修正。

在加法 toothis**是否中斷此應用程式的廠商與連線****傳送我們**以便讓我們可以搭配它們 toonatively 會將其應用程式整合與 Azure Active Directory。 您可以傳送嗨廠商 toohello[列出 hello Azure Active Directory 應用程式庫中的應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)tooget 加以啟動。

## <a name="credentials-are-filled-in-and-submitted-but-hello-page-indicates-hello-credentials-are-incorrect"></a>認證會填入與提交，但 hello 頁面會指出 hello 認證不正確

這個問題，第一個核取 hello 下列 tooresolve:

-   擁有 hello 使用者首次試用過**直接登入 toohello 應用程式網站**hello 認證儲存它們。

  * 如果此作業有效，則有 hello 使用者按一下 hello**更新認證**hello 按鈕**應用程式磚**在 hello**應用程式**區段 hello[應用程式存取面板](https://myapps.microsoft.com/)tooupdate 它們 toohello 最新已知使用使用者名稱和密碼。

   * 如果您或其他系統管理員指派 hello 認證對這個使用者而言尋找 hello 使用者或群組的應用程式指派瀏覽 toohello**使用者和群組**hello 應用程式中，選取 hello 分派 索引標籤和按一下 hello**更新認證** 按鈕。

-   如果 hello 使用者指派自己的認證，擁有 hello 使用者**檢查確定他們的密碼尚未過期 hello 應用程式中的 toobe**而且如果是，**更新過期的密碼**登入 toohello應用程式直接。

   * 已更新 hello 應用程式中的 hello 密碼之後，要求 hello 使用者 tooclick hello**更新認證**按鈕 hello**應用程式磚**在 hello**應用程式**區段的 hello[應用程式存取面板](https://myapps.microsoft.com/)tooupdate 它們 toohello 最新已知使用使用者名稱和密碼。

   * 如果您或其他系統管理員指派 hello 認證對這個使用者而言尋找 hello 使用者或群組的應用程式指派瀏覽 toohello**使用者和群組**hello 應用程式中，選取 hello 分派 索引標籤和按一下 hello**更新認證** 按鈕。

-   Hello 使用者更新 hello 存取面板瀏覽器延伸模組已依照 hello 執行下列步驟在 hello [tooinstall hello 存取面板瀏覽器延伸模組的方式](#how-to-install-the-access-panel-browser-extension)> 一節。

-   請確認正在執行且已啟用使用者的瀏覽器 hello 存取面板瀏覽器延伸模組。

-   請確定您的使用者沒有 toosign toohello hello 存取面板時在應用程式**incognito、 inPrivate，或私用模式**。 hello 存取面板延伸模組不支援這些模式中。

如果這無法運作，它可能已經變更。 已暫時中斷與 Azure AD 的 hello 應用程式整合 hello 應用程式端的 hello 案例。 例如，發生這個問題 hello 應用程式廠商導入了其具有不同行為手動 vs 頁面上的指令碼自動化的輸入，這會導致自動化整合，我們自己，toobreak 類似。 幸運的是，在許多情況下，Microsoft 可與應用程式廠商 toorapidly 解決這些問題。

Microsoft 有技術 tooautomatically 這些整合中斷，但有時候我們不能 toofind 時偵測到這些問題右離開，或者它們需要一些時間 toofix。 萬一 hello 當其中一個這些整合功能無法正常運作，我們非常感謝如果您開啟支援案例，以便我們可以盡快修正。

在加法 toothis**是否中斷此應用程式的廠商與連線****傳送我們**以便讓我們可以搭配它們 toonatively 會將其應用程式整合與 Azure Active Directory。 您可以傳送嗨廠商 toohello[列出 hello Azure Active Directory 應用程式庫中的應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)tooget 加以啟動。

## <a name="hello-extension-works-in-chrome-and-firefox-but-not-in-internet-explorer"></a>在 Chrome 和 Firefox，但不是在 Internet Explorer hello 擴充功能的運作方式

有兩個主要原因 toothis 問題：

-   根據 hello 如果 hello 網站不是，在 Internet Explorer 中啟用的安全性設定的一部分**信任區域**，有時候我們的指令碼遭到封鎖而無法執行 hello 應用程式。

  *  tooresolve，太指示 hello 使用者**新增 hello 應用程式的網站**toohello**信任的網站**清單中其**Internet Explorer 安全性設定**。 您可以傳送使用者 toohello[如何 tooadd 網站 toomy 受信任的網站清單](https://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/how-do-i-add-a-site-to-my-trusted-sites-list/98cc77c8-b364-e011-8dfc-68b599b31bf5)文件以取得詳細指示。

-   在極少數的情況下，Internet Explorer 的安全性驗證可能有時會造成 hello 頁面 tooload 比 hello 指令碼執行更慢。

   * 不幸的是，這種情況可能會改變 hello 瀏覽器版本、 電腦的速度或瀏覽的站台而定。 在此情況下，我們建議您連絡支援部門，以便我們可以修正 hello 這個特定的應用程式整合。

在加法 toothis**是否中斷此應用程式的廠商與連線****傳送我們**以便讓我們可以搭配它們 toonatively 會將其應用程式整合與 Azure Active Directory。 您可以傳送嗨廠商 toohello[列出 hello Azure Active Directory 應用程式庫中的應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)tooget 加以啟動。

## <a name="check-if-hello-applications-login-page-has-changed-recently-or-requires-an-additional-field"></a>請檢查是否 hello 應用程式的登入頁面最近已變更或需要額外的欄位

如果已大幅變更 hello 應用程式的登入頁面，有時候這會導致我們整合 toobreak。 舉例來說，這是應用程式廠商在欄位中，captcha，加入正負號，或多重要素驗證 tootheir 發生。 幸運的是，在許多情況下，Microsoft 可與應用程式廠商 toorapidly 解決這些問題。

Microsoft 有技術 tooautomatically 偵測這些整合中斷，但有時候我們不能 toofind 時立即問題。 否則，這些會需要一些時間 toofix。 萬一 hello 當其中一個這些整合功能無法正常運作，我們非常感謝開啟支援案例，以便我們可以盡快修正。

在加法 toothis**是否中斷此應用程式的廠商與連線****傳送我們**以便讓我們可以搭配它們 toonatively 會將其應用程式整合與 Azure Active Directory。 您可以傳送嗨廠商 toohello[列出 hello Azure Active Directory 應用程式庫中的應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)tooget 加以啟動。

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>如何 tooinstall hello 存取面板瀏覽器延伸模組

tooinstall hello 存取面板瀏覽器延伸模組，請遵循下列 hello 步驟：

1.  開啟 hello[存取面板](https://myapps.microsoft.com)其中一種支援的 hello 瀏覽器和登入為**使用者**Azure AD 中。

2.  按一下**password SSO 應用程式**hello 存取面板中。

3.  在 hello 提示詢問 tooinstall hello 軟體，選取 **立即安裝**。

4.  根據您的瀏覽器就導向的 toohello 下載連結。 **新增**hello 延伸 tooyour 瀏覽器。

5.  如果您的瀏覽器要求，請選取 tooeither**啟用**或**允許**hello 延伸模組。

6.  安裝之後，**重新啟動**瀏覽器工作階段。

7.  到 hello 存取面板登入，請參閱 < 是否您可以**啟動**password SSO 應用程式

您可能也 hello 從下載擴充功能的 Chrome 和 Firefox hello 以下的直接連結：

-   [Chrome 存取面板延伸模組](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Firefox 存取面板延伸模組](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="next-steps"></a>後續步驟
[提供單一登入 tooyour 應用程式與應用程式 Proxy](active-directory-application-proxy-sso-using-kcd.md)

