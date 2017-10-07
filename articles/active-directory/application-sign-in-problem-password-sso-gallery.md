---
title: "單一登入的登入 tooan 已設定為同盟的 Azure AD 庫應用程式的 aaaProblems |Microsoft 文件"
description: "Tootroubleshoot，如何與 Azure AD 的組件庫設定為 密碼單一登入的應用程式問題"
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
ms.openlocfilehash: 7ba28765e1d1f13025d740790a2f87654ae0daed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-federated-single-sign-on"></a>登入 tooan 設定同盟單一登入 Azure AD 庫應用程式的問題

hello 存取面板是網頁型入口網站讓使用者具有工作或學校帳戶在 Azure Active Directory (Azure AD) tooview 並啟動雲端型應用程式中的 hello Azure AD 系統管理員已被授與存取權。 自助式群組並透過 hello 存取面板應用程式管理功能，也可以使用具有 Azure AD 版本的使用者。 hello 存取面板是分開 hello Azure 入口網站，而且不需要使用者 toohave Azure 訂用帳戶。

toouse 密碼型單一登入 (SSO) 在 hello 存取面板，hello 存取面板延伸模組必須安裝在 hello 使用者的瀏覽器。 當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>會議 hello 存取面板 的瀏覽器需求

存取面板 hello 需要支援 JavaScript 的瀏覽器，並啟用 CSS。 toouse 密碼型單一登入 (SSO) 在 hello 存取面板，hello 存取面板延伸模組必須安裝在 hello 使用者的瀏覽器。 當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。

針對密碼型 SSO，hello 終端使用者的瀏覽器可以是：

-   Internet Explorer 8、9、10、11 - 在 Windows 7 或更新版本上

-   Chrome - 在 Windows 7 或更新版本，和在 MacOS X 或更新版本上

-   Firefox 26.0 或更新版本 - 在 Windows XP SP2 或更新版本，和在 Mac OS X 10.6 或更新版本上

>[!NOTE]
>hello 密碼型 SSO 延伸模組時，可以使用 Windows 10 中的 edge 瀏覽器延伸模組會變成支援 edge。
>
>

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

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>設定適用於 Internet Explorer 的群組原則

您可以設定群組原則可讓您 tooremotely 安裝 hello 存取面板延伸模組的 Internet Explorer 上使用者的機器。

hello 的先決條件包括：

-   您已設定[Active Directory 網域服務](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)，及您已加入您的使用者機器 tooyour 網域。

-   您必須擁有 hello [編輯設定] 的權限 tooedit hello 群組原則物件 (GPO)。 根據預設，hello 下列安全性群組的成員擁有此權限： 網域系統管理員、 企業系統管理員和 Group Policy Creator Owners。 [深入了解](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)。

請遵循 hello 教學課程[如何 tooDeploy hello 存取面板延伸模組使用群組原則設定 Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy)如需有關如何 tooconfigure hello 群組原則，並將其部署 toousers 的逐步指示。

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>疑難排解 hello Internet Explorer 中的 存取面板

請遵循 hello[疑難排解 hello Internet explorer 的 存取面板延伸模組](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot)引導存取診斷工具和逐步指示在 ie 設定 hello 延伸模組。

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>如何 tooconfigure 密碼單一登入 Azure AD 圖庫應用程式

您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：

-   [從 hello Azure AD 資源庫新增應用程式](#_Add_an_application)

-   [設定密碼單一登入的 hello 應用程式](#configure-the-application-for-password-single-sign-on)

-   [將使用者指派 toohello 應用程式](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>從 hello Azure AD 資源庫新增應用程式

tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：

1.  開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**

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

6.  選取您想 tooconfigure 單一登入的 hello 應用程式

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  選取 hello 模式**密碼式登入。**

9.  [將使用者指派 toohello 應用程式](#_How_to_assign)。

10. 此外，您也可以提供代表 hello 使用者認證選取 hello 的 hello 使用者的資料列，並按一下**更新認證**並代表 hello 使用者輸入 hello 使用者名稱和密碼。 否則，使用者在提示的 tooenter hello 認證本身在啟動。

### <a name="assign-users-toohello-application"></a>將使用者指派 toohello 應用程式

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

## <a name="if-these-troubleshoot-steps-dont-resolve-hello-issue"></a>如果這些疑難排解步驟沒有解決 hello 問題 
開啟支援票證以 hello 如果有的話，下列資訊：

-   相互關聯錯誤 ID

-   UPN (使用者電子郵件地址)

-   TenantID

-   瀏覽器類型

-   錯誤發生期間的時區和時間/時間範圍

-   Fiddler 追蹤

## <a name="next-steps"></a>後續步驟
[提供單一登入 tooyour 應用程式與應用程式 Proxy](active-directory-application-proxy-sso-using-kcd.md)
