---
title: "aaaProblems 登入 tooan 應用程式使用深層連結 |Microsoft 文件"
description: "如何從使用 Azure AD 的深層連結 URL 存取的應用程式的 tootroubleshoot 問題"
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
ms.openlocfilehash: dc82410001ac05895cc0244c3a89ace71bcf01a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-using-a-deeplink"></a>登入使用深層連結 tooan 應用程式的問題

hello 存取面板是網頁型的入口網站，可讓使用者使用工作或學校帳戶，Azure Active Directory (Azure AD) tooview 並啟動雲端架構應用程式中的 hello Azure AD 系統管理員已授與它們存取權。 

這些應用程式會代表 hello Azure AD 入口網站中的 hello 使用者設定。 hello 應用程式必須正確設定並指派的 toohello 使用者或群組 hello 使用者是 toosee hello 存取面板中的 hello 應用程式的成員。

深層連結或使用者的存取 Url 將是您的使用者可能會使用其密碼 SSO 應用程式直接從他們的瀏覽器的 URL 列的 tooaccess 的連結。 瀏覽 toothis 連結，使用者會自動登入 hello 應用程式，而不需要 toogo toohello 存取面板的第一次。 這是 hello 使用者使用 tooaccess hello Office 365 應用程式啟動程式從這些應用程式的相同連結。

## <a name="general-issues-toocheck-first"></a>一般會先發出 toocheck

-   請確定您使用**瀏覽器**符合 hello hello 存取面板的最低需求。

-   請確定 hello 使用者的瀏覽器已新增的 hello 應用程式 tooits hello URL**信任的網站**。

-   請確定 toocheck hello 應用程式是**設定**正確。

-   請確定 hello 使用者帳戶是**啟用**的登入。

-   請確定 hello 使用者帳戶是**並未鎖定。**

-   請確定 hello 使用者的**密碼未過期或遺失。**

-   確定 **Multi-Factor Authentication** 未封鎖使用者存取。

-   確定**條件式存取原則**或**身分識別保護**原則未封鎖使用者存取。

-   請確定使用者的**驗證連絡人資訊**已啟動 toodate tooallow Multi-factor Authentication 或條件式存取原則 toobe 強制執行。

-   請確定 tooalso 請嘗試清除瀏覽器的 cookie，然後再試一次 toosign 中的。

## <a name="checking-hello-deeplink"></a>檢查 hello 深層連結

toocheck，如果您擁有 hello 正確深層連結，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

7.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

8.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

9.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

10. 按一下**所有應用程式**tooview 所有應用程式的清單。

   * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

11. 選取您想要的 hello 核取 hello 深層連結的 hello 應用程式。

12. 找出 hello 標籤**使用者存取 URL**。 您的深層連結應符合此 URL。

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

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>如何 tooconfigure 密碼單一登入 Azure AD 圖庫應用程式

您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：

-   [從 hello Azure AD 資源庫新增應用程式](#add-an-application-from-the-Azure-AD-gallery)

-   [設定密碼單一登入的 hello 應用程式](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>從 hello Azure AD 資源庫新增應用程式

tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：

1.  開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**。

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗。

6.  在 hello**輸入的名稱**文字方塊中，從 hello**從 hello 圖庫新增**> 一節中，輸入 hello 名稱 hello 應用程式。

7.  選取要用於單一登入 tooconfigure hello 應用程式。

8.  然後再加入 hello 應用程式，您可以變更其名稱從 hello**名稱**文字方塊。

9.  按一下**新增**按鈕，tooadd hello 應用程式。

短時間，就能 toosee hello 應用程式的組態刀鋒視窗。

### <a name="configure-hello-application-for-password-single-sign-on"></a>設定密碼單一登入的 hello 應用程式

tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想 tooconfigure 單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  選取 hello 模式**密碼式登入。**

9.  [將使用者指派 toohello 應用程式](#how-to-assign-a-user-to-an-application-directly)。

10. 此外，您也可以提供代表 hello 使用者認證選取 hello 的 hello 使用者的資料列，並按一下**更新認證**並代表 hello 使用者輸入 hello 使用者名稱和密碼。 否則，使用者在提示的 tooenter hello 認證本身在啟動。

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>如何 tooconfigure 密碼單一登入非組件庫的應用程式

您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：

-   [新增不在資源庫內的應用程式](#add-a-non-gallery-application)

-   [設定密碼單一登入的 hello 應用程式](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a>新增不在資源庫內的應用程式

tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：

1.  開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**。

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗。

6.  按一下 [不在資源庫內的應用程式]。

7.  輸入 hello 應用程式的名稱在 hello**名稱**文字方塊。 選取 [新增]。

短時間，就能 toosee hello 應用程式的組態刀鋒視窗。

### <a name="configure-hello-application-for-password-single-sign-on"></a>設定密碼單一登入的 hello 應用程式

tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

    1.  如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想 tooconfigure 單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  選取 hello 模式**密碼式登入。**

9.  輸入 hello**登入 URL**。 這是讓使用者輸入其使用者名稱和密碼 toosign 中的以 hello URL。 請確定 hello 登入欄位會顯示在 hello URL。

10. 將使用者指派 toohello 應用程式。

11. 此外，您也可以提供代表 hello 使用者認證選取 hello 的 hello 使用者的資料列，並按一下**更新認證**並代表 hello 使用者輸入 hello 使用者名稱和密碼。 否則，使用者在提示的 tooenter hello 認證本身在啟動。

## <a name="how-tooassign-a-user-tooan-application-directly"></a>如何 tooassign 使用者 tooan 應用程式直接

tooassign 一或多個使用者 tooan 應用程式直接管理，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。

8.  按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。

9.  按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。

10. Hello 中的型別**全名**或**電子郵件地址**hello 使用者您感興趣指派到 hello 的**依名稱或電子郵件地址搜尋**搜尋 方塊。

11. 將滑鼠停留在 hello**使用者**在 hello 清單 tooreveal**核取方塊**。 按一下 [hello] 核取方塊下一步 toohello 使用者的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。

12. **選擇性：**如果您希望太**新增多個使用者**，在另一個類型**全名**或**電子郵件地址**到 hello**依名稱搜尋電子郵件地址或**搜尋 方塊中，然後按一下 hello 核取方塊 tooadd 這個使用者 toohello**選取**清單。

13. 當您完成選取的使用者，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。

14. **選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 使用者已選取。

15. 按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的使用者。

在短時間，您已選取的 hello 使用者會無法 toolaunch 中的這些應用程式之後 hello 存取面板。

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>如果不執行 hello 這些疑難排解步驟解決 hello 問題。 

開啟支援票證以 hello 如果有的話，下列資訊：

-   相互關聯錯誤 ID

-   UPN (使用者電子郵件地址)

-   TenantID

-   瀏覽器類型

-   錯誤發生期間的時區和時間/時間範圍

-   Fiddler 追蹤

## <a name="next-steps"></a>後續步驟
[提供單一登入 tooyour 應用程式與應用程式 Proxy](active-directory-application-proxy-sso-using-kcd.md)
