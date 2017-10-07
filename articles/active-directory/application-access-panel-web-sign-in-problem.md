---
title: "登入存取面板 」 toohello 網站 aaaProblem |Microsoft 文件"
description: "您可能會發生在嘗試 toosign toouse 中的指引 tootroubleshoot 問題 hello 存取面板"
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
ms.reviwer: japere
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a>登入存取面板 toohello 」 網站的問題

hello 存取面板是網頁型入口網站讓使用者具有工作或學校帳戶在 Azure Active Directory (Azure AD) tooview 並啟動雲端型應用程式中的 hello Azure AD 系統管理員已被授與存取權。 自助式群組並透過 hello 存取面板應用程式管理功能，也可以使用具有 Azure AD 版本的使用者。 hello 存取面板是分開 hello Azure 入口網站，而且不需要使用者 toohave Azure 訂用帳戶。

使用者可以登入 toohello 存取面板中，如果他們擁有在 Azure AD 中的工作或學校帳戶。

-   使用者可以直接由 Azure AD 驗證。

-   使用者可以透過 Active Directory Federation Services (AD FS) 進行驗證。

-   使用者可以由 Windows Server Active Directory 驗證。

如果使用者擁有 Azure 或 Office 365 訂閱，且 hello Azure 入口網站或 Office 365 應用程式已使用，他們必須能夠 toouse 順暢地 hello 存取面板，而不需要在 toosign 一次。 未驗證的使用者會在提示的 toosign hello 使用者名稱和密碼，使用 Azure AD 中為其帳戶。 如果 hello 組織已設定同盟，輸入 hello 使用者名稱便已足夠。

## <a name="general-issues-toocheck-first"></a>一般會先發出 toocheck 

-   請確定 hello 使用者登入 toohello**更正 URL**: <https://myapps.microsoft.com>

-   請確定 hello 使用者的瀏覽器已新增 hello URL tooits**信任的網站**

-   請確定 hello 使用者帳戶是**啟用**的登入。

-   請確定 hello 使用者帳戶是**並未鎖定。**

-   請確定 hello 使用者的**密碼未過期或遺失。**

-   確定 **Multi-Factor Authentication** 未封鎖使用者存取。

-   確定**條件式存取原則**或**身分識別保護**原則未封鎖使用者存取。

-   請確定使用者的**驗證連絡人資訊**已啟動 toodate tooallow Multi-factor Authentication 或條件式存取原則 toobe 強制執行。

-   請確定 tooalso 請嘗試清除瀏覽器的 cookie，然後再試一次 toosign 中的。

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>會議 hello 存取面板 的瀏覽器需求

存取面板 hello 需要支援 JavaScript 的瀏覽器，並啟用 CSS。 toouse 密碼型單一登入 (SSO) 在 hello 存取面板，hello 存取面板延伸模組必須安裝在 hello 使用者的瀏覽器。 當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。

針對密碼型 SSO，hello 終端使用者的瀏覽器可以是：

-   Internet Explorer 8、9、10、11 -- 在 Windows 7 或更新版本上

-   Windows 10 Anniversary Edition 或更新版本上的 Edge 

-   Chrome - 在 Windows 7 或更新版本，和在 MacOS X 或更新版本上

-   Firefox 26.0 或更新版本 - 在 Windows XP SP2 或更新版本，和在 Mac OS X 10.6 或更新版本上


## <a name="problems-with-hello-users-account"></a>Hello 使用者帳戶的問題

存取 toohello 存取面板可以被封鎖，因為 tooa 問題與 hello 使用者帳戶。 以下是針對使用者和其帳戶設定進行疑難排解的一些方法︰

-   [檢查 Azure Active Directory 中是否存在使用者帳戶](#check-if-a-user-account-exists-in-azure-active-directory)

-   [檢查使用者帳戶的狀態](#check-a-users-account-status)

-   [重設使用者的密碼](#reset-a-users-password)

-   [啟用自助密碼重設](#enable-self-service-password-reset)

-   [檢查使用者的多重要素驗證狀態](#check-a-users-multi-factor-authentication-status)

-   [檢查使用者的驗證連絡資訊](#check-a-users-authentication-contact-info)

-   [檢查使用者的群組成員資格](#check-a-users-group-memberships)

-   [檢查使用者獲指派的授權](#check-a-users-assigned-licenses)

-   [指派授權至使用者](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a>檢查 Azure Active Directory 中是否存在使用者帳戶

toocheck 使用者帳戶是否存在，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有使用者]。

6.  **搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。

7.  檢查確定它們看起來如您預期且不會遺失任何資料的 hello 使用者物件 toobe hello 屬性。

### <a name="check-a-users-account-status"></a>檢查使用者帳戶的狀態

toocheck 使用者的帳戶狀態，請遵循下列步驟 hello:

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有使用者]。

6.  **搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。

7.  按一下 [設定檔]。

8.  在下**設定**確定**區塊登入**設定得**否**。

### <a name="reset-a-users-password"></a>重設使用者的密碼

tooreset 使用者的密碼，後續 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有使用者]。

6.  **搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。

7.  按一下 hello**重設密碼**在 hello hello 使用者 刀鋒視窗頂端的按鈕。

8.  按一下 hello**重設密碼**按鈕 hello**重設密碼**刀鋒視窗中出現。

9.  複製 hello**暫時密碼**或**輸入新密碼**hello 使用者。

10. 這個新的密碼 toohello 使用者進行通訊，它們是必要的 toochange 他們下一步 在此密碼登入 tooAzure Active Directory。

### <a name="enable-self-service-password-reset"></a>啟用自助式密碼重設

tooenable 自助式密碼重設，請遵循下列的 hello 部署步驟：

-   [啟用使用者 tooreset 其 Azure Active Directory 密碼](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [啟用使用者 tooreset 或變更其 Active Directory 內部部署密碼](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a>檢查使用者的多重要素驗證狀態

toocheck 使用者的多重要素驗證狀態，後續 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有使用者]。

6.  按一下 hello **Multi-factor Authentication**在 hello hello 刀鋒視窗頂端的按鈕。

7.  一次 hello**多因素驗證管理網站**載入，請確定您是在 hello**使用者** 索引標籤。

8.  Hello 的使用者清單中尋找 hello 使用者搜尋、 篩選或排序。

9.  選取 hello 使用者的使用者清單，hello 和**啟用**，**停用**，或**強制**所需的多因素驗證。

   >[!NOTE]
   >如果使用者存在於**強制**狀態時，您可能設定太**已停用**暫時 toolet 它們放回其帳戶。 當它們位於上一步時，您可以變更其狀態太**啟用**再次 toorequire 它們 toore 註冊他們的連絡資訊在其下一步 期間登入。 或者，您可以依照 hello 中的 hello 步驟[檢查使用者的驗證連絡人資訊](#check-a-users-authentication-contact-info)tooverify 或設定此資料。
   >
   >

### <a name="check-a-users-authentication-contact-info"></a>檢查使用者的驗證連絡資訊

toocheck 位使用者的驗證連絡資訊用於多重要素驗證、 條件式存取、 識別身分保護和重設密碼，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有使用者]。

6.  **搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。

7.  按一下 [設定檔]。

8.  向下捲動太**驗證連絡人資訊**。

9.  **檢閱**視 hello 資料註冊 hello 使用者和更新。

### <a name="check-a-users-group-memberships"></a>檢查使用者的群組成員資格

toocheck 使用者的群組成員資格，請遵循下列步驟 hello:

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有使用者]。

6.  **搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。

7.  按一下**群組**toosee 以分組 hello 使用者隸屬。

### <a name="check-a-users-assigned-licenses"></a>檢查使用者獲指派的授權

toocheck 使用者的指派授權，後續 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有使用者]。

6.  **搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。

7.  按一下**授權**toosee 授權 hello 使用者目前已指派。

### <a name="assign-a-user-a-license"></a>指派授權至使用者 

tooassign 授權 tooa 使用者，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有使用者]。

6.  **搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。

7.  按一下**授權**toosee 授權 hello 使用者目前已指派。

8.  按一下 hello**指派** 按鈕。

9.  選取**一或多個產品**hello 清單中的可用產品。

10. **選擇性**按一下 hello**指派選項**項目 toogranularly 指派產品。 完成時按一下 [確定]。

11. 按一下 hello**指派**按鈕 tooassign 這些授權 toothis 使用者。

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>如果這些疑難排解步驟無法解決 hello 問題

開啟支援票證以 hello 如果有的話，下列資訊：

-   相互關聯錯誤 ID

-   UPN (使用者電子郵件地址)

-   租用戶識別碼

-   瀏覽器類型

-   錯誤發生期間的時區和時間/時間範圍

-   Fiddler 追蹤

## <a name="next-steps"></a>後續步驟
[提供單一登入 tooyour 應用程式與應用程式 Proxy](active-directory-application-proxy-sso-using-kcd.md)
