---
title: "教學課程：Azure Active Directory 與 MOVEit Transfer - Azure AD integration 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 MOVEit Transfer - Azure AD integration 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5d9955655119a51656d6b17ba1cecf624c416874
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a>教學課程：Azure Active Directory 與 MOVEit Transfer - Azure AD integration 整合

在本教學課程中，您將了解如何整合 MOVEit Transfer - Azure AD integration 與 Azure Active Directory (Azure AD)。

將 MOVEit Transfer - Azure AD integration 與 Azure AD 整合可提供下列優點：

- 您可以在 Azure AD 中控制可存取 MOVEit Transfer - Azure AD integration 的人員。
- 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 MOVEit Transfer - Azure AD integration (單一登入)。
- 您可以在 Azure 入口網站中集中管理您的帳戶。

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 MOVEit Transfer - Azure AD integration 整合，您需要下列項目：

- Azure AD 訂用帳戶
- 已啟用 MOVEit Transfer - Azure AD integration 單一登入功能的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二項主要的基本工作組成：

1. 從資源庫新增 MOVEit Transfer - Azure AD integration
2. 設定並測試 Azure AD 單一登入

## <a name="adding-moveit-transfer---azure-ad-integration-from-the-gallery"></a>從資源庫新增 MOVEit Transfer - Azure AD integration
若要設定 MOVEit Transfer - Azure AD integration 與 Azure AD 整合，您需要從資源庫將 MOVEit Transfer - Azure AD integration 新增到受控 SaaS 應用程式清單中。

**若要從資源庫新增 MOVEit Transfer - Azure AD integration，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Azure Active Directory 按鈕][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![企業應用程式刀鋒視窗][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![新增應用程式按鈕][3]

4. 在搜尋方塊中，輸入 **MOVEit Transfer - Azure AD integration**，從結果面板中選取 [MOVEit Transfer - Azure AD integration]，然後按一下 [新增] 按鈕以新增應用程式。

    ![結果清單中的 MOVEit Transfer - Azure AD integration](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 MOVEit Transfer - Azure AD integration 搭配運作的 Azure AD 單一登入。

若要讓單一登入運作，Azure AD 必須知道 MOVEit Transfer - Azure AD integration 與 Azure AD 中互相對應的使用者。 換句話說，必須建立 Azure AD 使用者和 MOVEit Transfer - Azure AD integration 中相關使用者之間的連結關聯性。

在 MOVEit Transfer - Azure AD integration 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。

若要設定及測試對 MOVEit Transfer - Azure AD integration 的 Azure AD 單一登入，您需要完成下列建構元素：

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 MOVEit Transfer - Azure AD integration 測試使用者](#create-a-moveit-transfer---azure-ad-integration-test-user)** - 使 MOVEit Transfer - Azure AD integration 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。
4. **[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會於 Azure 入口網站啟用 Azure AD 單一登入，並在您的 MOVEit Transfer - Azure AD integration 應用程式中設定單一登入。

**若要使用 MOVEit Transfer - Azure AD integration 設定 Azure AD 單一登入功能，請執行下列步驟：**

1. 在 Azure 入口網站的 [MOVEit Transfer - Azure AD integration] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入連結][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. 在 [MOVEit Transfer - Azure AD integration 網域與 URL] 區段中，執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    a. 在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://contoso.com`

    b. 在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://contoso.com/<tenatid>`

    c. 在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`    
     
    > [!NOTE] 
    > 這些都不是真正的值。 使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。 您可以稍後在 [服務提供者中繼資料 URL] 區段中參照這些值，或連絡 [MOVEit Transfer - Azure AD integration 用戶端支援小組](https://community.ipswitch.com/s/support)以取得這些值。

4. 在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。

    ![憑證下載連結](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. 以系統管理員身分登入 MOVEit Transfer 租用戶。

7. 在左側的導覽窗格上，按一下 [設定] 。

    ![應用程式端上的設定區段](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. 按一下 [單一登入] 連結，其位於 [安全性原則] -> [使用者驗證] 下。

    ![應用程式端上的安全性原則](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. 按一下 [中繼資料 URL] 連結以下載中繼資料文件。

    ![服務提供者中繼資料 URL](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * 確認 **entityID** 符合 [MOVEit Transfer - Azure AD integration 網域與 URL] 區段中的 [識別碼]。
    * 確認 **AssertionConsumerService** 位置 URL 符合 [MOVEit Transfer - Azure AD integration 網域與 URL] 區段中的 [回覆 URL]。
    
    ![在應用程式端設定單一登入](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. 按一下 [新增識別提供者]  按鈕來加入新的同盟識別提供者。

    ![新增識別提供者](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. 按一下 [瀏覽...] 以選取您從 Azure 入口網站下載的中繼資料檔案，然後按一下 [新增識別提供者] 以上傳所下載的檔案。

    ![SAML 識別提供者](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. 選取 [是] 做為 [編輯同盟識別提供者設定...] 頁面中的 [啟用]，然後按一下 [儲存]。

    ![同盟識別提供者設定](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. 在 [編輯同盟識別提供者使用者設定] 頁面中，執行下列動作：
    
    ![編輯同盟識別提供者設定](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    a. 選取 [SAML NameID] 做為 [登入名稱]。
    
    b. 在 [其他] 中選取 [全名]，並在 [屬性名稱] 文字方塊中，輸入值：`http://schemas.microsoft.com/identity/claims/displayname`。
    
    c. 在 [其他] 中選取 [電子郵件]，並在 [屬性名稱] 文字方塊中，輸入值：`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`。
    
    d. 選取 [是] 做為 [在登入時自動建立帳戶]。
    
    e. 按一下 [儲存]  按鈕。

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

   ![建立 Azure AD 測試使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。

    ![Azure Active Directory 按鈕](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. 若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。

    ![[新增] 按鈕](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. 在 [使用者] 對話方塊中，執行下列步驟：

    ![[使用者] 對話方塊](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    a. 在 [名稱] 方塊中，輸入 **BrittaSimon**。

    b. 在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。

    c. 選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。

    d. 按一下頁面底部的 [新增] 。
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a>建立 MOVEit Transfer - Azure AD integration 測試使用者

本節的目標是要在 MOVEit Transfer - Azure AD integration 中建立一個名為 Britta Simon 的使用者。 MOVEit Transfer - Azure AD integration 支援您已啟用的 Just-In-Time 佈建。 在這一節沒有您需要進行的動作項目。 嘗試存取 MOVEit Transfer - Azure AD integration 時若尚無使用者，則會建立新使用者。

>[!NOTE]
>如果您需要手動建立使用者，則必須連絡 [MOVEit Transfer - Azure AD integration 用戶端支援小組](https://community.ipswitch.com/s/support)。

### <a name="assign-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 MOVEit Transfer - Azure AD integration 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者角色][200] 

**如要將 Britta Simon 指派給 MOVEit Transfer - Azure AD integration，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [MOVEit Transfer - Azure AD integration]。

    ![應用程式清單中的 MOVEit Transfer - Azure AD integration 連結](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. 在左側功能表中，按一下 [使用者和群組]。

    ![[使用者和群組] 連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![[新增指派] 窗格][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。

當您在「存取面板」中按一下 [MOVEit Transfer - Azure AD integration] 圖格時，應該會自動登入您的 MOVEit Transfer - Azure AD integration 應用程式。 

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

