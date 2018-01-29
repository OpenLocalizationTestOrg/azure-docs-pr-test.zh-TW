---
title: "登入存取面板網站時遇到問題 | Microsoft Docs"
description: "針對您嘗試登入使用存取面板時可能遇到的問題進行疑難排解的指引"
services: active-directory
documentationcenter: 
author: ajamess
manager: mtillman
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviwer: japere
ms.openlocfilehash: 0f50a705d4453970d039c2219aef8e1a411fd533
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="problem-signing-in-to-the-access-panel-website"></a>登入存取面板網站時遇到問題

存取面板是網頁型入口網站，可讓在 Azure Active Directory (Azure AD) 中具有公司或學校帳戶的使用者，檢視和啟動 Azure AD 系統管理員已授權他們存取的雲端式應用程式。 具有 Azure AD 版本的使用者也可以透過存取面板使用自助群組和應用程式管理功能。 存取面板與 Azure 入口網站分開，使用者不需要具備 Azure 訂用帳戶也能使用。

如果使用者在 Azure AD 中有公司或學校帳戶，他們就可以登入存取面板。

-   使用者可以直接由 Azure AD 驗證。

-   使用者可以透過 Active Directory Federation Services (AD FS) 進行驗證。

-   使用者可以由 Windows Server Active Directory 驗證。

如果使用者具備 Azure 或 Office 365 的訂用帳戶，而且已經在使用 Azure 入口網站或 Office 365 應用程式，他們就可以直接使用存取面板，而不需要再次登入。 對於未經過驗證的使用者，系統會提示他們輸入 Azure AD 中的帳戶使用者名稱和密碼來登入。 如果組織已設定同盟，則輸入使用者名稱已經足夠。

## <a name="general-issues-to-check-first"></a>首先檢查的一般問題 

-   確定使用者登入**正確 URL**：<https://myapps.microsoft.com>

-   確定使用者的瀏覽器已將此 URL 新增至**信任的網站**

-   確定使用者的帳戶**已啟用**登入。

-   確定使用者的帳戶**未鎖定**。

-   確定使用者的**密碼未過期或忘記**。

-   確定 **Multi-Factor Authentication** 未封鎖使用者存取。

-   確定**條件式存取原則**或**身分識別保護**原則未封鎖使用者存取。

-   確定使用者的**驗證連絡資訊**為最新版本，而可強制執行 Multi-Factor Authentication 或條件式存取原則。

-   也要確定嘗試清除瀏覽器的 Cookie，然後嘗試再次登入。

## <a name="meeting-browser-requirements-for-the-access-panel"></a>符合存取面板的瀏覽器需求

存取面板需要支援 JavaScript 且已啟用 CSS 的瀏覽器。 若要在存取面板中使用密碼單一登入 (SSO)，必須在使用者的瀏覽器中安裝存取面板延伸模組。 當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。

若是密碼 SSO，則使用者的瀏覽器可以是：

-   Internet Explorer 8、9、10、11 -- 在 Windows 7 或更新版本上

-   Windows 10 Anniversary Edition 或更新版本上的 Edge 

-   Chrome - 在 Windows 7 或更新版本，和在 MacOS X 或更新版本上

-   Firefox 26.0 或更新版本 - 在 Windows XP SP2 或更新版本，和在 Mac OS X 10.6 或更新版本上


## <a name="problems-with-the-users-account"></a>使用者帳戶的問題

使用者帳戶發生問題時可能會封鎖對存取面板的存取。 以下是針對使用者和其帳戶設定進行疑難排解的一些方法︰

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

若要檢查使用者的帳戶是否存在，請依照下列步驟執行：

1.  開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**身分登入。

2.  按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。

3.  在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。

4.  按一下瀏覽功能表中的 [使用者和群組]。

5.  按一下 [所有使用者]。

6.  **搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。

7.  檢查使用者物件的屬性，確定符合您的預期，沒有遺失資料。

### <a name="check-a-users-account-status"></a>檢查使用者帳戶的狀態

若要檢查使用者帳戶的狀態，請依照下列步驟執行：

1.  開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。

2.  按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。

3.  在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。

4.  按一下瀏覽功能表中的 [使用者和群組]。

5.  按一下 [所有使用者]。

6.  **搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。

7.  按一下 [設定檔]。

8.  在 [設定] 下，確定 [封鎖登入] 設為 [否]。

### <a name="reset-a-users-password"></a>重設使用者的密碼

若要重設使用者的密碼，請依照下列步驟執行：

1.  開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**身分登入。

2.  按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。

3.  在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。

4.  按一下瀏覽功能表中的 [使用者和群組]。

5.  按一下 [所有使用者]。

6.  **搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。

7.  按一下使用者刀鋒視窗頂端的 [重設密碼]按鈕。

8.  在出現的 [重設密碼] 刀鋒視窗上，按一下 [重設密碼] 按鈕。

9.  為使用者複製**暫時密碼**或**輸入新密碼**。

10. 將這個新的密碼告知使用者，他們下次登入 Azure Active Directory 時必須變更此密碼。

### <a name="enable-self-service-password-reset"></a>啟用自助式密碼重設

若要啟用自助式密碼重設，請遵循下列部署步驟︰

-   [讓使用者重設其 Azure Active Directory 密碼](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [讓使用者重設或變更其 Active Directory 內部部署密碼](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a>檢查使用者的多重要素驗證狀態

若要檢查使用者的多重要素驗證狀態，請依照下列步驟執行：

1.  開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**身分登入。

2.  按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。

3.  在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。

4.  按一下瀏覽功能表中的 [使用者和群組]。

5.  按一下 [所有使用者]。

6.  按一下刀鋒視窗頂端的 [Multi-Factor Authentication] 按鈕。

7.  當 **Multi-Factor Authentication 管理網站**載入後，請確定您位於 [使用者] 索引標籤上。

8.  在使用者清單中搜尋、篩選或排序來尋找使用者。

9.  從使用者清單中選取使用者，然後視需要 [啟用]、[停用] 或 [強制執行] 多重要素驗證。

   >[!NOTE]
   >如果使用者處於 [已強制] 狀態，您可以暫時將他們設為 [已停用]，讓他們回到各自的帳戶。 退回之後，您可以再次將其狀態變更為 [已啟用]，以要求他們在下次登入時重新註冊連絡資訊。 或者，您可以依照[檢查使用者的驗證連絡資訊](#check-a-users-authentication-contact-info)中的步驟，為他們確認或設定此資料。
   >
   >

### <a name="check-a-users-authentication-contact-info"></a>檢查使用者的驗證連絡資訊

若要檢查用於多重要素驗證、條件式存取、身分識別保護和密碼重設的使用者驗證連絡資訊，請依照下列步驟執行︰

1.  開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**身分登入。

2.  按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。

3.  在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。

4.  按一下瀏覽功能表中的 [使用者和群組]。

5.  按一下 [所有使用者]。

6.  **搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。

7.  按一下 [設定檔]。

8.  向下捲動至 [驗證連絡資訊]。

9.  **檢閱**使用者註冊的資料，並視需要予以更新。

### <a name="check-a-users-group-memberships"></a>檢查使用者的群組成員資格

若要檢查使用者的群組成員資格，請依照下列步驟執行：

1.  開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**身分登入。

2.  按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。

3.  在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。

4.  按一下瀏覽功能表中的 [使用者和群組]。

5.  按一下 [所有使用者]。

6.  **搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。

7.  按一下 [群組]，查看使用者是哪些群組的成員。

### <a name="check-a-users-assigned-licenses"></a>檢查使用者獲指派的授權

若要檢查使用者獲指派的授權，請依照下列步驟執行：

1.  開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**身分登入。

2.  按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。

3.  在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。

4.  按一下瀏覽功能表中的 [使用者和群組]。

5.  按一下 [所有使用者]。

6.  **搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。

7.  按一下 [授權]，查看使用者目前已指派的授權。

### <a name="assign-a-user-a-license"></a>指派授權至使用者 

若要指派授權至使用者，請依照下列步驟執行︰

1.  開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**身分登入。

2.  按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。

3.  在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。

4.  按一下瀏覽功能表中的 [使用者和群組]。

5.  按一下 [所有使用者]。

6.  **搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。

7.  按一下 [授權]，查看使用者目前已指派的授權。

8.  按一下 [指派] 按鈕。

9.  從可用產品清單中選取**一或多個產品**。

10. (**選擇性**) 按一下 [指派選項] 項目，更細微地指派產品。 完成時按一下 [確定]。

11. 按一下 [指派] 按鈕，將這些授權指派給這位使用者。

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a>如果這些疑難排解步驟無法解決問題

使用下列資訊 (若有的話) 開啟支援票證︰

-   相互關聯錯誤 ID

-   UPN (使用者電子郵件地址)

-   租用戶識別碼

-   瀏覽器類型

-   錯誤發生期間的時區和時間/時間範圍

-   Fiddler 追蹤

## <a name="next-steps"></a>後續步驟
[使用應用程式 Proxy 提供單一登入應用程式](active-directory-application-proxy-sso-using-kcd.md)
