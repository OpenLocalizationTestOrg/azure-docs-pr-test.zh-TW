---
title: "教學課程：Azure Active Directory 與 Evidence.com 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Evidence.com 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 655a12685641964c81dd6a94ae7e7a19a9a30001
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a>教學課程：Azure Active Directory 與 Evidence.com 整合

在本教學課程中，您將了解如何整合 Evidence.com 與 Azure Active Directory (Azure AD)。

Evidence.com 與 Azure AD 整合提供下列優點：

- 您可以在 Azure AD 中管控可存取 Evidence.com 的人員。
- 您可以讓使用者使用其 Azure AD 帳戶自動登入 Evidence.com (單一登入)。
- 您可以在 Azure 入口網站中集中管理您的帳戶。

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 Evidence.com 整合，您需要下列項目：

- Azure AD 訂用帳戶
- 已啟用 Evidence.com 單一登入功能的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二項主要的基本工作組成：

1. 從資源庫新增 Evidence.com
2. 設定並測試 Azure AD 單一登入

## <a name="adding-evidencecom-from-the-gallery"></a>從資源庫新增 Evidence.com
若要設定將 Evidence.com 整合到 Azure AD 中，您需要從資源庫將 Evidence.com 新增到受控 SaaS 應用程式清單。

**若要從資源庫新增 Evidence.com，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Azure Active Directory 按鈕][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![企業應用程式刀鋒視窗][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![新增應用程式按鈕][3]

4. 在搜尋方塊中，輸入 **Evidence.com**，從結果面板中選取 [Evidence.com]，然後按一下 [新增] 按鈕以新增應用程式。

    ![結果清單中的 Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Evidence.com 設定及測試 Azure AD 單一登入。

若要讓單一登入能夠運作，Azure AD 必須知道 Evidence.com 與 Azure AD 中互相對應的使用者。 換句話說，必須在 Azure AD 使用者和 Evidence.com 中的相關使用者之間建立連結關聯性。

在 Evidence.com 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。

若要設定並測試透過 Evidence.com 使用 Azure AD 單一登入，您需要完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 Evidence.com 測試使用者](#create-a-evidencecom-test-user)** - 使 Evidence.com 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。
4. **[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Evidence.com 應用程式中設定單一登入。

**若要設定透過 Evidence.com 使用 Azure AD 單一登入功能，請執行下列步驟：**

1. 在 Azure 入口網站的 [Evidence.com] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入連結][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. 在 [Evidence.com 網域與 URL] 區段上，執行下列步驟：

    ![Evidence.com 網域及 URL 單一登入資訊](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    a. 在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<yourtenant>.evidence.com`

    b. 在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<yourtenant>.evidence.com`

    > [!NOTE] 
    > 這些都不是真正的值。 使用實際的「登入 URL」及「識別碼」來更新這些值。 請連絡 [Evidence.com 用戶端支援小組](https://communities.taser.com/support/SupportContactUs?typ=LE)以取得這些值。 

4. 在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。

    ![憑證下載連結](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. 在 [Evidence.com 組態] 區段上，按一下 [設定 Evidence.com] 以開啟 [設定登入] 視窗。 從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。

    ![Evidence.com 設定](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. 在個別的網頁瀏覽器視窗中，以系統管理員身分登入您的 Evidence.com 租用戶，並瀏覽至 [Admin]  索引標籤

8. 按一下 [機構單一登入] 

9. 選取 [SAML 型單一登入] 

10. 將顯示在 Azure 入口網站中的 **SAML 實體 ID**、**SAML 單一登入服務 URL** 和**登出 URL** 值複製到 Evidence.com 中的對應欄位。

11. 在記事本中開啟您下載的憑證 (Base64) 檔案，將其內容複製到剪貼簿，然後貼到 [安全性憑證] 方塊中。 

12. 在 Evidence.com 中儲存組態。

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

   ![建立 Azure AD 測試使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。

    ![Azure Active Directory 按鈕](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. 若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。

    ![[新增] 按鈕](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. 在 [使用者] 對話方塊中，執行下列步驟：

    ![[使用者] 對話方塊](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    a. 在 [名稱] 方塊中，輸入 **BrittaSimon**。

    b. 在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。

    c. 選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。

    d. 按一下頁面底部的 [新增] 。
 
### <a name="create-a-evidencecom-test-user"></a>建立 Evidence.com 測試使用者

必須先針對 Evidence.com 應用程式內的存取佈建 Azure AD 使用者，才可以讓他們登入。 本節描述如何建立 Evidence.com 內的 Azure AD 使用者帳戶。

**若要在 Evidence.com 中佈建使用者帳戶：**

1. 在網頁瀏覽器視窗中，以系統管理員身分登入您的 Evidence.com 公司網站。

2. 瀏覽至 [Admin]  索引標籤。

3. 按一下 [新增使用者] 。

4. 按一下 [新增]  按鈕。

5. 所新增之使用者的 [電子郵件地址]  必須符合 Azure AD 中想要允許存取的使用者名稱。 如果使用者名稱和電子郵件地址不是您組織中的相同值，您可以使用 Azure 入口網站的 **[Evidence.com] > [屬性] > [單一登入]** 區段，將傳送至 Evidence.com 的 nameidenitifer 變更為電子郵件地址。

### <a name="assign-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 Evidence.com 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者角色][200] 

**若要將 Britta Simon 指派到 Evidence.com，請執行以下步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [Evidence.com]。

    ![應用程式清單中的 Evidence.com 連結](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. 在左側功能表中，按一下 [使用者和群組]。

    ![[使用者和群組] 連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![[新增指派] 窗格][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。

在「存取面板」中按一下 Evidence.com 圖格時，應該會自動登入 Evidence.com 應用程式。
如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

