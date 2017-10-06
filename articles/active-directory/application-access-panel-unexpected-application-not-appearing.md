---
title: "aaaAn 指派應用程式不會顯示在 hello 存取面板 |Microsoft 文件"
description: "應用程式並未出現在 hello 存取面板進行疑難排解"
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
ms.openlocfilehash: 089883f406267df4552c7fc991883f335ad49fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="an-assigned-application-is-not-appearing-on-hello-access-panel"></a>指派的應用程式不會顯示 hello 存取面板上

hello 存取面板是網頁型的入口網站，可讓使用者使用工作或學校帳戶，Azure Active Directory (Azure AD) tooview 並啟動雲端架構應用程式中的 hello Azure AD 系統管理員已授與它們存取權。 這些應用程式會代表 hello Azure AD 入口網站中的 hello 使用者設定。 hello 應用程式必須正確設定並指派的 toohello 使用者或群組 hello 使用者是 toosee hello 存取面板中的 hello 應用程式的成員。

應用程式的使用者會看見 hello 類型落在 hello 下列類別：

-   Office 365 應用程式

-   已設定同盟 SSO 的 Microsoft 及第三方應用程式

-   密碼型 SSO 應用程式

-   含現有 SSO 解決方案的應用程式

## <a name="general-issues-toocheck-first"></a>一般會先發出 toocheck

-   如果應用程式剛加入 tooa 使用者，toosign 入和登出再試一次到 hello 使用者的存取面板後幾分鐘的時間 toosee 如果 hello 應用程式會加入。

-   授權就已從使用者或群組 hello 使用者隸屬這可能需要很長的時間，取決於 hello 大小和複雜度所做的變更 toobe hello 群組。 允許額外的時間才能登入存取面板 hello。

## <a name="problems-related-tooapplication-configuration"></a>問題相關的 tooapplication 組態

應用程式未出現在使用者的存取面板上可能是因為並未正確設定。 下面是的一些您可以疑難排解問題相關的 tooapplication 組態：

-   [如何 tooconfigure 同盟單一登入 Azure AD 圖庫應用程式](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [如何 tooconfigure 同盟單一登入非組件庫的應用程式](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [如何 tooconfigure 密碼單一登入應用程式的 Azure AD 圖庫應用程式](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [如何 tooconfigure 密碼單一登入應用程式的非組件庫的應用程式](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>如何 tooconfigure 同盟單一登入 Azure AD 圖庫應用程式

啟用具備企業單一登入功能的 hello Azure AD 資源庫中的所有應用程式有可用的逐步教學課程。 您可以存取 hello[如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/)如需詳細資料的逐步指引。

您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：

-   [從 hello Azure AD 資源庫新增應用程式](#add-an-application-from-the-azure-ad-gallery)

-   [設定 Azure AD （登入 URL，識別項，回覆 URL） 中的 hello 應用程式的中繼資料值](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [擷取 Azure AD 中繼資料與憑證](#download-the-azure-ad-metadata-or-certificate)

-   [在 hello 應用程式 （登入 URL、 簽發者、 登出 URL 和憑證） 中設定 Azure AD 中繼資料值](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a>從 hello Azure AD 資源庫新增應用程式

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

#### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>設定單一登入應用程式從 hello Azure AD 資源庫

tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想 tooconfigure 單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  選取**SAML 型登入**從 hello**模式**下拉式清單。

9.  輸入中的所需的 hello 值**網域和 Url。** 您應該從 hello 應用程式廠商，以取得這些值。

   1. tooconfigure hello 應用程式做為 SP 起始的 SSO hello 登入 URL 是必要的值。 有些應用程式識別碼 hello 也是必要的值。

   2. tooconfigure hello 應用程式做為 IdP 初始化的 SSO，hello 回覆 URL 是必要的值。 有些應用程式識別碼 hello 也是必要的值。

10. **選擇性：**按一下**顯示進階的 URL 設定**您希望 toosee hello 非必要的值。

11. 在 hello**使用者屬性**，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。

12. **選擇性：**按一下**檢視和編輯所有其他使用者屬性**tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。

   tooadd 屬性：

   1. 按一下 [新增屬性]。 輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。

   2. 按一下 [儲存]。 您會看到 hello hello 資料表中的新屬性。

13. 按一下**設定&lt;應用程式名稱&gt;** tooaccess 文件中的有關 tooconfigure 單一登入 hello 應用程式中。 此外，您有 hello 中繼資料 Url 和與 hello 應用程式所需的憑證 toosetup SSO。

14. 按一下**儲存**toosave hello 組態。

15. 將使用者指派 toohello 應用程式。

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式

tooselect hello 使用者識別碼或新增使用者屬性，請遵循下列的 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想 tooshow 這裡的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您已設定單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  在 hello**使用者屬性**區段中，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。 hello 選取的選項必須在 hello 應用程式 tooauthenticate hello 使用者 toomatch hello 預期的值。

   >[!NOTE] 
   >Hello NameID 屬性 （使用者識別碼） 的 azure AD 選取 hello 格式會根據選取的 hello 值或 hello hello hello SAML AuthRequest 中的應用程式所要求的格式。 如需詳細資訊，請造訪 hello 文章[單一登入的 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)hello 下一節 NameIDPolicy。
   >
   >

9.  tooadd 使用者屬性，按一下**檢視和編輯所有其他使用者屬性**tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。

   tooadd 屬性：

   1. 按一下 [新增屬性]。 輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。

   2. 按一下 [儲存]。 您會看見 hello hello 資料表中的新屬性。

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a>下載 hello Azure AD 中繼資料或憑證

toodownload hello 應用程式中繼資料或憑證從 Azure AD，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您已設定單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  跳過**SAML 簽章憑證**區段，然後按一下 **下載**資料行值。 根據哪些 hello 應用程式需要設定單一登入，您會看到其中一個 hello 選項 toodownload hello 中繼資料 XML 或 hello 憑證。

    Azure AD 不會提供 URL tooget hello 中繼資料。 hello 中繼資料，才能擷取為 XML 檔案。

### <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a>如何 tooconfigure 同盟單一登入非組件庫的應用程式

tooconfigure 非組件庫的應用程式，您必須具備 toohave Azure AD premium 與 hello 應用程式支援 SAML 2.0。 如需有關 Azure AD 版本的詳細資訊，請參閱 [Azure AD 定價](https://azure.microsoft.com/pricing/details/active-directory/)。

-   [設定 Azure AD （登入 URL，識別項，回覆 URL） 中的 hello 應用程式的中繼資料值](#configuring-single-sign-on)

-   [選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [擷取 Azure AD 中繼資料與憑證](#download-the-azure-ad-metadata-or-certificate)

-   [在 hello 應用程式 （登入 URL、 簽發者、 登出 URL 和憑證） 中設定 Azure AD 中繼資料值](#configuring-single-sign-on)

#### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a>設定 Azure AD （登入 URL，識別項，回覆 URL） 中的 hello 應用程式的中繼資料值

tooconfigure 單一登入的應用程式不在 hello Azure AD 資源庫，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗。

6.  按一下**非組件庫的應用程式**在 hello**新增您自己的應用程式**> 一節。

7.  輸入 hello hello 應用程式名稱在 hello**名稱**文字方塊。

8.  按一下**新增**按鈕，tooadd hello 應用程式。

9.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

10. 選取**SAML 型登入**在 hello**模式**下拉式清單。

11. 輸入中的所需的 hello 值**網域和 Url。** 您應該從 hello 應用程式廠商，以取得這些值。

   1. tooconfigure hello IdP 初始化的 SSO 應用程式輸入 hello 回覆 URL 和識別碼 hello。

   2.  **選擇性：** tooconfigure hello 應用程式做為 SP 起始的 SSO hello 登入 URL 是必要的值。

12. 在 hello**使用者屬性**，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。

13. **選擇性：**按一下**檢視和編輯所有其他使用者屬性**tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。

   tooadd 屬性：

   1. 按一下 [新增屬性]。 輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。

   2. 按一下 [儲存]。 您會看到 hello hello 資料表中的新屬性。

14. 按一下**設定&lt;應用程式名稱&gt;** tooaccess 文件中的有關 tooconfigure 單一登入 hello 應用程式中。 此外，您有 Azure AD Url 和 hello 應用程式所需的憑證。

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式

tooselect hello 使用者識別碼或新增使用者屬性，請遵循下列的 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

   * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您已設定單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  在 hello**使用者屬性**區段中，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。 hello 選取的選項必須在 hello 應用程式 tooauthenticate hello 使用者 toomatch hello 預期的值。

   >[!NOTE] 
   >Hello NameID 屬性 （使用者識別碼） 的 azure AD 選取 hello 格式會根據選取的 hello 值或 hello hello hello SAML AuthRequest 中的應用程式所要求的格式。 如需詳細資訊，請造訪 hello 文章[單一登入的 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)hello 下一節 NameIDPolicy。
   >
   >

9.  tooadd 使用者屬性，按一下**檢視和編輯所有其他使用者屬性**tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。

   tooadd 屬性：

   1. 按一下 [新增屬性]。 輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。

   2. 按一下 [儲存]。 您會看到 hello hello 資料表中的新屬性。

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a>下載 hello Azure AD 中繼資料或憑證

toodownload hello 應用程式中繼資料或憑證從 Azure AD，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

   * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您已設定單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  跳過**SAML 簽章憑證**區段，然後按一下 **下載**資料行值。 根據哪些 hello 應用程式需要設定單一登入，您會看到其中一個 hello 選項 toodownload hello 中繼資料 XML 或 hello 憑證。

Azure AD 不會提供 URL tooget hello 中繼資料。 hello 中繼資料，才能擷取為 XML 檔案。

### <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>如何 tooconfigure 密碼單一登入 Azure AD 圖庫應用程式

您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：

-   [從 hello Azure AD 資源庫新增應用程式](#add-an-application-from-the-azure-ad-gallery)

-   [設定密碼單一登入的 hello 應用程式](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a>從 hello Azure AD 資源庫新增應用程式

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

#### <a name="configure-hello-application-for-password-single-sign-on"></a>設定密碼單一登入的 hello 應用程式

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

### <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>如何 tooconfigure 密碼單一登入非組件庫的應用程式

您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：

-   [新增不在資源庫內的應用程式](#add-a-non-gallery-application)

-   [設定密碼單一登入的 hello 應用程式](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a>新增不在資源庫內的應用程式

tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：

1.  開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**。

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗。

6.  按一下 [不在資源庫內的應用程式]。

7.  輸入 hello 應用程式的名稱在 hello**名稱**文字方塊。 選取 [新增]。

短時間，就能 toosee hello 應用程式的組態刀鋒視窗。

#### <a name="configure-hello-application-for-password-single-sign-on"></a>設定密碼單一登入的 hello 應用程式

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

10. [將使用者指派 toohello 應用程式](#how-to-assign-a-user-to-an-application-directly)。

11. 此外，您也可以提供代表 hello 使用者認證選取 hello 的 hello 使用者的資料列，並按一下**更新認證**並代表 hello 使用者輸入 hello 使用者名稱和密碼。 否則，使用者在提示的 tooenter hello 認證本身在啟動。

## <a name="problems-related-tooassigning-applications-toousers"></a>問題相關的 tooassigning 應用程式 toousers

使用者可能不只可看見應用程式存取面板上因為它們不會指派 toohello 應用程式。 以下是一些方式 toocheck:

-   [檢查 toohello 應用程式時，是否要指派使用者](#check-if-a-user-is-assigned-to-the-application)

-   [如何 tooassign 使用者 tooan 應用程式直接](#how-to-assign-a-user-to-an-application-directly)

-   [如果 tooa 授權指派給使用者的核取相關 toohello 應用程式](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [如何 tooassign 授權 tooa 使用者](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-toohello-application"></a>檢查 toohello 應用程式時，是否要指派使用者

toocheck 如果使用者被指派 toohello 應用程式，請遵循 hello 執行下列步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

6.  **搜尋**hello hello 有問題的應用程式名稱。

7.  按一下 [使用者和群組]。

8.  如果您的使用者被指派 toohello 應用程式，請檢查 toosee。

   * 如果沒有依照中的 hello 步驟 「 如何 tooassign 使用者 tooan 應用程式直接"toodo 讓。

### <a name="how-tooassign-a-user-tooan-application-directly"></a>如何 tooassign 使用者 tooan 應用程式直接

tooassign 一或多個使用者 tooan 應用程式直接管理，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**。

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

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a>檢查是否授權使用者相關 toohello 應用程式

toocheck 使用者的指派授權，後續 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有使用者]。

6.  **搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。

7.  按一下**授權**toosee 授權 hello 使用者目前已指派。

  * 如果這啟用第一個合作對象 Office 應用程式 tooappear tooan Office 授權指派給 hello 使用者 hello 使用者的存取面板。

### <a name="how-tooassign-a-user-a-license"></a>如何 tooassign 使用者授權 

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

## <a name="problems-related-tooassigning-applications-toogroups"></a>問題相關的 tooassigning 應用程式 toogroups

使用者會看見應用程式存取面板上因為它們已被指派 hello 應用程式群組的一部分。 以下是一些方式 toocheck:

-   [檢查使用者的群組成員資格](#check-a-users-group-memberships)

-   [如何 tooassign 應用程式 tooa 群組直接](#how-to-assign-an-application-to-a-group-directly)

-   [檢查使用者是否屬於 tooa 授權指派給群組](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [如何 tooassign 授權 tooa 群組](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a>檢查使用者的群組成員資格

toocheck 群組的成員資格，後續 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有使用者]。

6.  **搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。

7.  按一下 [群組]。

8.  如果您的使用者屬於群組的核取 toosee 指派 toohello 應用程式。

  * 如果您想從 hello 群組 tooremove hello 使用者**按一下 hello 列**hello 群組和選取的刪除。

### <a name="how-tooassign-an-application-tooa-group-directly"></a>如何 tooassign 應用程式 tooa 群組直接

tooassign 一或多個群組 tooan 的應用程式直接管理，後續 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**。

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。

8.  按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。

9.  按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。

10. 型別在 hello**完整的群組名稱**您感興趣指派到 hello hello 群組的**依名稱或電子郵件地址搜尋**搜尋 方塊。

11. 將滑鼠停留在 hello**群組**在 hello 清單 tooreveal**核取方塊**。 按一下 [hello] 核取方塊下一步 toohello 群組的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。

12. **選擇性：**如果您希望太**新增多個群組**，在另一個類型**完整的群組名稱**到 hello**依名稱或電子郵件地址搜尋**搜尋方塊中，按一下此群組 toohello hello 核取方塊 tooadd**選取**清單。

13. 當您完成選取群組，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。

14. **選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 群組您已選取。

15. 按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的群組。

在短時間，您已選取的 hello 使用者會無法 toolaunch 中的這些應用程式之後 hello 存取面板。

### <a name="check-if-a-user-is-part-of-group-assigned-tooa-license"></a>檢查使用者是否屬於 tooa 授權指派給群組

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有使用者]。

6.  **搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。

7.  按一下 [群組]。

8.  按一下 特定群組的 hello 資料列。

9.  按一下**授權**toosee 授權 hello 群組已指派 tooit。

   * 如果這可能會讓特定的第一個合作對象 Office 應用程式 tooappear tooan Office 授權指派給 hello 群組 hello 使用者的存取面板。

### <a name="how-tooassign-a-license-tooa-group"></a>如何 tooassign 授權 tooa 群組

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
>toodo 這速度更快，請考慮暫時直接指派授權 toohello 使用者。 
>
>

## <a name="next-steps"></a>後續步驟
[加入新使用者 tooAzure Active Directory](active-directory-users-create-azure-portal.md)

