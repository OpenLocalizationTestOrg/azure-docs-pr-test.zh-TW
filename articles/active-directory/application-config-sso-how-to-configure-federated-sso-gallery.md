---
title: "aaaHow tooconfigure 同盟單一登入 Azure AD 庫應用程式 |Microsoft 文件"
description: "如何 tooconfigure 同盟單一登入的現有 Azure AD 庫應用程式並使用教學課程 tooget 快速地移"
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
ms.openlocfilehash: a93de021fddd253e4fe663c221b822d12625fd54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>如何 tooconfigure 同盟單一登入 Azure AD 庫應用程式

Hello Azure AD 啟用具備企業單一登入功能的組件庫中的所有應用程式有可用的逐步教學課程。 您可以存取 hello[如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/)如需詳細的逐步指引。

## <a name="overview-of-steps-required"></a>所需步驟的概觀
您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：

-   [從 hello Azure AD 資源庫新增應用程式](#add-an-application-from-the-azure-ad-gallery)

-   [設定 Azure AD （登入 URL，識別項，回覆 URL） 中的 hello 應用程式的中繼資料值](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [擷取 Azure AD 中繼資料與憑證](#download-the-azure-ad-metadata-or-certificate)

-   [在 hello 應用程式 （登入 URL、 簽發者、 登出 URL 和憑證） 中設定 Azure AD 中繼資料值](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [將使用者指派 toohello 應用程式](#assign-users-to-the-application)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a>從 hello Azure AD 資源庫新增應用程式

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

在短時間之後, 就無法 toosee hello 應用程式的組態刀鋒視窗。

## <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>設定單一登入應用程式從 hello Azure AD 資源庫

tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員**。

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

   1. 按一下 [儲存]。 您會看到 hello hello 資料表中的新屬性。

13. 按一下**設定&lt;應用程式名稱&gt;** tooaccess 文件中的有關 tooconfigure 單一登入 hello 應用程式中。 此外，您有 hello 中繼資料 Url 和與 hello 應用程式所需的憑證 toosetup SSO。

14. 按一下**儲存**toosave hello 組態。

15. 將使用者指派 toohello 應用程式。

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式

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

   2. 按一下 [儲存] 。 您會看到 hello hello 資料表中的新屬性。

## <a name="download-hello-azure-ad-metadata-or-certificate"></a>下載 hello Azure AD 中繼資料或憑證

toodownload hello 應用程式中繼資料或憑證從 Azure AD，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  *  如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式**。

6.  選取您已設定單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  跳過**SAML 簽章憑證**區段，然後按一下 **下載**資料行值。 根據哪些 hello 應用程式需要設定單一登入，您會看到其中一個 hello 選項 toodownload hello 中繼資料 XML 或 hello 憑證。

Azure AD 不會提供 URL tooget hello 中繼資料。 hello 中繼資料，才能擷取為 XML 檔案。

## <a name="assign-users-toohello-application"></a>將使用者指派 toohello 應用程式

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

一段短時間，您已選取的 hello 使用者是使用這些應用程式 hello hello 方案描述 部分中所述的方法可以 toolaunch。

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a>自訂 hello SAML 宣告傳送 tooan 應用程式

toolearn 如何 toocustomize hello SAML 屬性宣告傳送 tooyour 應用程式，請參閱[宣告 Azure Active Directory 中的對應](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping)如需詳細資訊。

## <a name="next-steps"></a>後續步驟
[提供單一登入 tooyour 應用程式與應用程式 Proxy](active-directory-application-proxy-sso-using-kcd.md)



