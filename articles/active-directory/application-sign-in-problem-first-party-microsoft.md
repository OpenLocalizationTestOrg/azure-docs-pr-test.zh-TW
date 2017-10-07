---
title: "登入 tooa Microsoft 應用程式的 aaaProblems |Microsoft 文件"
description: "疑難排解 toofirst 合作對象 Microsoft 應用程式使用 （例如 Office 365) 的 Azure AD 在登入時所面臨的常見問題"
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
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a>登入 tooa Microsoft 應用程式的問題

Microsoft 應用程式 (如 Office 365 Exchange、SharePoint、Yammer 等) 在指派與管理方面，比第三方 SaaS 應用程式或與 Azure AD 整合以單一登入的其他應用程式略為困難。

有三種主要方式，使用者也可以取得存取 tooa Microsoft 發行的應用程式。

-   Hello Office 365 或其他付費的套件中的應用程式，會授與使用者存取透過**授權指派**任一直接 tootheir 使用者帳戶，或透過使用我們的群組為基礎的授權指派功能的群組。

-   對於應用程式，Microsoft 或第三個合作對象發行自由每個人都能 toouse，使用者可能會被授與存取透過**使用者同意**。 This0 表示他們登入 toohello 應用程式與 Azure AD 工作或學校帳戶，並允許它 toohave 存取 toosome 有限的一組資料上他們的帳戶。

-   對於應用程式，Microsoft 或第 3 合作對象發行自由每個人都能 toouse，可能也會授與使用者存取透過**系統管理員的同意**。 這表示系統管理員所判斷可能每個人都可以在 hello 組織中，使用 hello 應用程式，讓他們登入具有全域管理員帳戶的 toohello 應用程式，並授與存取 tooeveryone hello 組織中。

tootroubleshoot 您的問題，以 hello 開頭[一般問題區域與應用程式存取 tooconsider](#general-problem-areas-with-application-access-to-consider) ，然後讀取 hello[逐步解說： 步驟 tootroubleshoot Microsoft 應用程式存取](#walkthrough-steps-to-troubleshoot-microsoft-application-access)tooget 到 hello 詳細資料。

## <a name="general-problem-areas-with-application-access-tooconsider"></a>應用程式存取 tooconsider 的一般問題區域

以下是一般的問題區域，如果您有其中 toostart，但我們建議您閱讀 hello 逐步解說 tooget 移快速了解可以切入 hello 的清單：[逐步解說： 步驟 tootroubleshoot Microsoft 應用程式存取](#walkthrough-steps-to-troubleshoot-microsoft-application-access).

-   [Hello 使用者帳戶的問題](#problems-with-the-users-account)

-   [群組的問題](#problems-with-groups)

-   [條件式存取原則的問題](#problems-with-conditional-access-policies)

-   [應用程式同意的問題](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a>步驟 tootroubleshoot Microsoft 應用程式存取

下面是一些常見的問題同仁時遇到使用者無法登入 tooa Microsoft 應用程式。

-   一般會先發出 toocheck

  * 請確定 hello 使用者登入 toohello**更正 URL**並不是本機應用程式的 URL。

  * 請確定 hello 使用者帳戶是**並未鎖定。**

  * 請確定 hello**使用者帳戶存在**Azure Active Directory 中。 [檢查 Azure Active Directory 中是否存在使用者帳戶](#problems-with-the-users-account)

  * 請確定 hello 使用者帳戶是**啟用**的登入。[檢查使用者帳戶的狀態](#problems-with-the-users-account)

  * 請確定 hello 使用者的**密碼未過期或遺失。** [重設使用者密碼](#reset-a-users-password)或[啟用自助式密碼重設](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)

   * 確定 **Multi-Factor Authentication** 未封鎖使用者存取。 [檢查使用者的多重要素驗證狀態](#check-a-users-multi-factor-authentication-status)或[檢查使用者的驗證連絡資訊](#check-a-users-authentication-contact-info)

   * 確定**條件式存取原則**或**身分識別保護**原則未封鎖使用者存取。 [檢查特定條件式存取原則](#problems-with-conditional-access-policies)、[檢查特定應用程式條件式存取原則](#check-a-specific-applications-conditional-access-policy)或[停用特定條件式存取原則](#disable-a-specific-conditional-access-policy)

   * 請確定使用者的**驗證連絡人資訊**已啟動 toodate tooallow Multi-factor Authentication 或條件式存取原則 toobe 強制執行。 [檢查使用者的多重要素驗證狀態](#check-a-users-multi-factor-authentication-status)或[檢查使用者的驗證連絡資訊](#check-a-users-authentication-contact-info)

-   如**Microsoft** **需要授權的應用程式**（例如 Office365)，以下是一些特定的問題 toocheck 並非 hello 上述的一般問題：

   * 請確認 hello 使用者或已**指派授權。** [檢查使用者獲指派的授權](#check-a-users-assigned-licenses)或[檢查群組獲指派的授權](#check-a-groups-assigned-licenses)

   * 如果 hello 授權為**指派 tooa** **靜態群組**，確保該 hello**使用者所屬的**該群組。 [檢查使用者的群組成員資格](#check-a-users-group-memberships)

   * 如果 hello 授權為**指派 tooa** **動態群組**，確保該 hello**動態群組規則已正確設定**。 [檢查動態群組成員資格準則](#check-a-dynamic-groups-membership-criteria)

   * 如果 hello 授權為**指派 tooa** **動態群組**，確定該 hello 動態群組擁有**完成處理**其成員資格，以及該 hello**使用者成員**（這可能需要一些時間）。 [檢查使用者的群組成員資格](#check-a-users-group-memberships)

   *  一旦您確定 hello 授權指派，請確定 hello 授權**過期**。

   *  請確定 hello 授權**hello 應用程式**他們存取的。

-   如**Microsoft** **應用程式不需要授權的**，以下是一些其他項目 toocheck:

   * 如果 hello 應用程式要求**使用者層級權限**（例如 「 存取這位使用者的信箱 」），請確定該 hello 使用者登入 toohello 應用程式，且已經執行**使用者層級同意作業** toolet hello 應用程式存取其資料。

   * 如果 hello 應用程式要求**系統管理員層級權限**（例如 「 存取所有使用者的信箱 」），請確定已執行 全域管理員**上的系統管理員層級同意作業代表所有使用者**hello 組織中。

## <a name="problems-with-hello-users-account"></a>Hello 使用者帳戶的問題

因為 tooa 問題指派 toohello 應用程式的使用者，可能會封鎖應用程式存取。 以下是針對使用者和其帳戶設定進行疑難排解的一些方法︰

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

  * **請注意**： 如果使用者存在於**強制**狀態時，您可能設定太**已停用**暫時 toolet 它們放回其帳戶。 當它們位於上一步時，您可以變更其狀態太**啟用**再次 toorequire 它們 toore 註冊他們的連絡資訊在其下一步 期間登入。 或者，您可以依照 hello 中的 hello 步驟[檢查使用者的驗證連絡人資訊](#check-a-users-authentication-contact-info)tooverify 或設定此資料。

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

## <a name="problems-with-groups"></a>群組的問題

應用程式存取權可以指派 toohello 應用程式群組 tooa 時發生問題。 因為被封鎖。 以下是為群組和群組成員資格問題疑難排解的一些方法︰

-   [檢查群組成員資格](#check-a-groups-membership)

-   [檢查動態群組成員資格準則](#check-a-dynamic-groups-membership-criteria)

-   [檢查群組獲指派的授權](#check-a-groups-assigned-licenses)

-   [重新處理群組的授權](#reprocess-a-groups-licenses)

-   [指派授權至群組](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a>檢查群組成員資格

toocheck 群組的成員資格，後續 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有群組]。

6.  **搜尋**hello 您感興趣的群組和**按一下 hello 列**tooselect。

7.  按一下**成員**tooreview hello 清單的使用者指派 toothis 群組。

### <a name="check-a-dynamic-groups-membership-criteria"></a>檢查動態群組成員資格準則 

toocheck 動態群組成員資格準則，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有群組]。

6.  **搜尋**hello 您感興趣的群組和**按一下 hello 列**tooselect。

7.  按一下 [動態成員資格規則]。

8.  檢閱 hello**簡單**或**進階**規則為此群組定義，並確定 hello 使用者想 toobe 此群組的成員符合這些準則。

### <a name="check-a-groups-assigned-licenses"></a>檢查群組獲指派的授權

toocheck 群組的指派授權，後續 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有群組]。

6.  **搜尋**hello 您感興趣的群組和**按一下 hello 列**tooselect。

7.  按一下**授權**toosee 授權 hello 群組目前已指派。

### <a name="reprocess-a-groups-licenses"></a>重新處理群組的授權

tooreprocess 群組的指派授權，後續 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有群組]。

6.  **搜尋**hello 您感興趣的群組和**按一下 hello 列**tooselect。

7.  按一下**授權**toosee 授權 hello 群組目前已指派。

8.  按一下 hello**重新處理**按鈕 tooensure hello 指派授權 toothis 群組的成員，都是最新。 這可能需要很長的時間，取決於 hello 大小和複雜度 hello 群組。

   >[!NOTE]
   >toodo 這速度更快，請考慮暫時直接指派授權 toohello 使用者。 [指派授權至使用者](#problems-with-application-consent)。
   >
   >

### <a name="assign-a-group-a-license"></a>指派授權至群組

tooassign 授權 tooa 群組，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有群組]。

6.  **搜尋**hello 您感興趣的群組和**按一下 hello 列**tooselect。

7.  按一下**授權**toosee 授權 hello 群組目前已指派。

8.  按一下 hello**指派** 按鈕。

9.  選取**一或多個產品**hello 清單中的可用產品。

10. **選擇性**按一下 hello**指派選項**項目 toogranularly 指派產品。 完成時按一下 [確定]。

11. 按一下 hello**指派**按鈕 tooassign 這些授權 toothis 群組。 這可能需要很長的時間，取決於 hello 大小和複雜度 hello 群組。

   >[!NOTE]
   >toodo 這速度更快，請考慮暫時直接指派授權 toohello 使用者。 [指派授權至使用者](#problems-with-application-consent)。
   > 
   >

## <a name="problems-with-conditional-access-policies"></a>條件式存取原則的問題

### <a name="check-a-specific-conditional-access-policy"></a>檢查特定的條件式存取原則

toocheck 或驗證的單一條件式存取原則：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**hello 瀏覽功能表中。

5.  按一下 hello**條件式存取**瀏覽項目。

6.  按一下您感興趣檢查 hello 原則。

7.  檢查有無特定的條件、指派，或其他可能會封鎖使用者存取的設定。

   >[!NOTE]
   >您可能希望 tootemporarily 停用此原則 tooensure，則會不影響符號集 toodo 如此，組 hello**啟用原則**太切換**否**按一下 hello**儲存**按鈕.
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a>檢查特定應用程式的條件式存取原則

toocheck 或驗證單一應用程式的目前設定的條件式存取原則：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**hello 瀏覽功能表中。

5.  按一下 [所有應用程式]。

6.  搜尋您感興趣，或 hello 使用者 「 hello 」 應用程式正在嘗試 toosign tooby 應用程式中的顯示名稱或應用程式的識別碼。

     >[!NOTE]
     >如果您沒有看到您所需的 hello 應用程式，按一下 hello**篩選**按鈕，然後依序展開 hello hello 清單範圍太**所有應用程式**。 如果您想 toosee 更多資料行，請按一下 hello**資料行**按鈕 tooadd 應用程式的其他詳細資料。
     >
     >

7.  按一下 hello**條件式存取**瀏覽項目。

8.  按一下您感興趣檢查 hello 原則。

9.  檢查有無特定的條件、指派，或其他可能會封鎖使用者存取的設定。

     >[!NOTE]
     >您可能希望 tootemporarily 停用此原則 tooensure，則會不影響符號集 toodo 如此，組 hello**啟用原則**太切換**否**按一下 hello**儲存**按鈕.
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a>停用特定的條件式存取原則

toocheck 或驗證的單一條件式存取原則：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**hello 瀏覽功能表中。

5.  按一下 hello**條件式存取**瀏覽項目。

6.  按一下您感興趣檢查 hello 原則。

7.  停用 hello 原則所設定的 hello**啟用原則**太切換**否**按一下 hello**儲存** 按鈕。

## <a name="problems-with-application-consent"></a>應用程式同意的問題

因為尚未發生 hello 適當的權限同意作業，可能會封鎖應用程式的存取。 以下提供一些方式，可讓您疑難排解並解決應用程式同意問題：

-   [執行使用者層級同意作業](#perform-a-user-level-consent-operation)

-   [為任何應用程式執行系統管理員層級同意作業](#perform-administrator-level-consent-operation-for-any-application)

-   [為單一租用戶應用程式執行系統管理員層級同意](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [為多租用戶應用程式執行系統管理員層級同意](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a>執行使用者層級同意作業

-   任何開啟連接的識別碼已啟用應用程式要求的權限，瀏覽 toohello 應用程式的登入畫面執行 hello 登入使用者的使用者同意層級 toohello 應用程式。

-   如果您想 toodo 此以程式設計的方式，請參閱[要求個別的使用者同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent)。

### <a name="perform-administrator-level-consent-operation-for-any-application"></a>為任何應用程式執行系統管理員層級同意作業

-   如**僅使用 hello V1 應用程式模型所開發的應用程式**，您可以藉由新增強制此系統管理員的同意層級 toooccur"**？ 提示 = admin\_同意**"toohello 結尾應用程式的登入 URL。

-   如**任何使用 hello V2 應用程式模型開發的應用程式**，您可以強制此系統管理員層級同意 toooccur hello 指示下 hello**要求 hello 權限的目錄系統管理員**區段[使用 hello 系統管理員同意端點](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)。

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a>為單一租用戶應用程式執行系統管理員層級同意

-   如**單一租用戶應用程式**，來要求權限 （類似您所開發，或在您的組織擁有），您可以執行**系統管理層級同意**代表所有作業使用者的全域管理員身分登入，然後按一下 hello**授與權限**按鈕上方的 hello hello**應用程式登錄-&gt;所有應用程式-&gt;選取應用程式&gt;必要的使用權限**刀鋒視窗。

-   如**任何使用 hello V1 或 V2 應用程式模型開發的應用程式**，您可以強制此系統管理員層級同意 toooccur hello 指示下 hello**要求從 hello 權限目錄管理員**區段[使用 hello 系統管理員同意端點](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)。

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a>為多租用戶應用程式執行系統管理員層級同意

-   適用於要求權限的**多租用戶應用程式** (例如第三方或 Microsoft 開發的應用程式)：您可以執行**系統管理員層級同意**作業。 全域管理員身分登入，並按一下 hello**授與權限**hello 下的按鈕**企業應用程式-&gt;所有應用程式-&gt;選取應用程式-&gt;權限**刀鋒視窗 (可立即)。

-   您也可以強制此系統管理員層級同意 toooccur hello 指示下 hello **hello 權限要求目錄管理員從**區段[使用 hello 系統管理員同意端點](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

## <a name="next-steps"></a>後續步驟
[使用 hello 系統管理員同意端點](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

