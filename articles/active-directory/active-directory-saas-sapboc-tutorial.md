---
title: "教學課程：Azure Active Directory 與 SAP Business Object Cloud 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 SAP 商務物件雲端之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a>教學課程：Azure Active Directory 與 SAP Business Object Cloud 整合

在此教學課程中，您學習如何 toointegrate SAP 商務物件雲端與 Azure Active Directory (Azure AD)。

您會收到 hello 與 Azure AD 整合 SAP 商務物件雲端時，下列優點：

- 在 Azure AD 中，您可以控制誰可以存取 tooSAP 商務物件的雲端。
- 您可以自動登入您的使用者 tooSAP 商務物件雲端使用單一登入和使用者的 Azure AD 帳戶。
- 您可以管理您的帳戶，在一個集中位置，hello Azure 入口網站。

toolearn 進一步了解軟體即服務 (SaaS) 應用程式與 Azure AD 整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory？](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooset 與 SAP 商務物件雲端的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已開啟單一登入的 SAP Business Object Cloud

> [!NOTE]
> 如果您在測試 hello 步驟在本教學課程，我們建議您不要在生產環境中測試它們。

測試本教學課程中的 hello 步驟建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，可以[取得一個月的免費試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 

本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 加入 SAP 商務物件雲端從 hello 組件庫。
2. 設定和測試 Azure AD 單一登入。

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a>新增 SAP 商務物件雲端從 hello 組件庫
SAP 商務物件雲端的 Azure ad 的 hello 圖庫中的 hello 整合 tooset SAP 商務物件雲端 tooyour 之新增受管理的 SaaS 應用程式。

tooadd hello 圖庫 SAP 商務物件雲端：

1. 在 [hello [Azure 入口網站](https://portal.azure.com)，在 [hello 左側的功能表中選取**Azure Active Directory**。 

    ![hello Azure Active Directory] 按鈕][1]

2. 選取 [企業應用程式]，然後選取 [所有應用程式]。

    ![hello 企業應用程式] 頁面][2]
    
3. tooadd 新的應用程式中，選取**新的應用程式**。

    ![hello 新應用程式按鈕][3]

4. 在 [hello] 搜尋方塊中，輸入**SAP 商務物件雲端**。

    ![hello 搜尋方塊](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. 在 [hello [結果] 窗格中，選取**SAP 商務物件雲端**，然後選取**新增**。

    ![Hello 結果清單中的 SAP 商務物件雲端](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您將以名為 Britta Simon 的測試使用者身分，設定及測試與 SAP Business Object Cloud 搭配運作的 Azure AD 單一登入。

Azure AD 單一登入 toowork，需要 tooknow hello Azure AD SAP 商務物件雲端中的對等項目的使用者。 必須先建立 Azure AD 使用者與 SAP 商務物件雲端中的 hello 相關的使用者之間的連結關聯性。

tooestablish hello 連結關聯性，在 SAP 商務物件雲端中，適用於**Username**，hello hello 值指派**使用者名**在 Azure AD 中。

tooconfigure 和測試 Azure AD 單一登入與 SAP 商務物件的雲端，完成下列工作的 hello:

1. [設定 Azure AD 單一登入](#set-up-azure-ad-single-sign-on)。 設定使用者 toouse 這項功能。
2. [建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)。 測試 Azure AD 單一登入與 hello 使用者許 Simon。
3. [建立 SAP Business Object Cloud 測試使用者](#create-an-sap-business-object-cloud-test-user)。 在 SAP 商務物件雲端連結的 toohello hello 使用者的 Azure AD 表示法建立許 Simon 對應項目。
4. [指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)。 設定 Azure AD 單一登入許 Simon toouse。
5. [測試單一登入](#test-single-sign-on)。 請確認該 hello 設定可正常運作。

### <a name="set-up-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您開啟 Azure AD 單一登入 hello Azure 入口網站中。 然後，您要在 SAP Business Object Cloud 應用程式中設定單一登入。

Azure AD 單一登入與 SAP 商務物件雲端 tooset:

1. 在 Azure 入口網站上 hello hello **SAP 商務物件雲端**應用程式整合頁面上，選取**單一登入**。

    ![選取 [單一登入]][4]

2. 在 hello**單一登入**] 頁面上，針對**模式**，選取**SAML 型登入**。
 
    ![選取 SAML 登入](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. 在下**SAP 商務物件雲端網域和 Url**完整 hello 下列步驟：

    1. 在 [hello**登入 URL**方塊中，輸入 URL，其中具有 hello 下列模式： 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. 在 [hello**識別碼**方塊中，輸入 URL，其中具有 hello 下列模式：
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![SAP Business Object Cloud 網域和 URL 頁面的 URL](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > 這些 Url 中的 hello 值為僅供示範之。 更新 hello 值與實際的 hello 登入 URL 和識別碼的 URL。 tooget hello 登入 URL，請連絡 hello [SAP 商務物件雲端的用戶端支援小組](https://www.sap.com/product/analytics/cloud-analytics.support.html)。 您可以藉由從 hello 系統管理員主控台下載 hello SAP 商務物件雲端中繼資料取得 hello 識別項 URL。 稍後在 hello 教學課程的說明。 

4. 在 [SAML 簽章憑證] 下，選取 [中繼資料 XML]。 然後，儲存您的電腦上的 hello 中繼資料檔案。

    ![選取 [中繼資料 XML]](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. 選取 [ **儲存**]。

    ![選取 [儲存]](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入 tooyour SAP 商務物件雲端公司網站。

7. 選取 [功能表] > [系統] > [管理]。
    
    ![依序選取 [功能表]、[系統] 和 [管理]](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. 在 [hello**安全性**索引標籤，選取 hello**編輯**（畫筆） 圖示。
    
    ![Hello 安全性索引標籤上，選取 [hello [編輯] 圖示](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. 選取 [SAML 單一登入 (SSO)] 作為 [驗證方法]。

    ![選取 [SAML 單一登入 hello 驗證方法](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. toodownload hello 服務提供者中繼資料 (步驟 1) 選取**下載**。 在 [hello 中繼資料檔，尋找並複製 hello **entityID**值。 在 hello Azure 入口網站中，在**SAP 商務物件雲端網域和 Url**，hello 值貼在 hello**識別碼**方塊。

    ![複製並貼上 hello entityID 值](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. tooupload hello 服務提供者中繼資料 (步驟 2) 在您從網站下載的 hello 檔案 hello Azure 入口網站底下**上傳的身分識別提供者中繼資料**，選取**上傳**。  

    ![在上傳識別提供者中繼資料下，選取 [上傳]](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. 在 [hello**使用者屬性**清單，您在實作想 toouse 選取 hello 使用者屬性 (步驟 3)。 此使用者屬性對應 toohello 身分識別提供者。 tooenter hello 使用者] 頁面上，使用 hello 的自訂屬性**自訂 SAML 對應**選項。 或者，您可以選取**電子郵件**或**使用者識別碼**做 hello 使用者屬性。 在本例中，我們選取 [**電子郵件**因為我們對應 hello 使用者識別項宣告以 hello **userprincipalname**中 hello 屬性**使用者屬性**hello > 一節Azure 入口網站。 這會提供唯一的使用者電子郵件，每個成功的 SAML 回應中傳送 toohello SAP 商務物件雲端應用程式。

    ![選取使用者屬性](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. hello 身分識別提供者 (步驟 4)，在 hello tooverify hello 帳戶**登入認證 （電子郵件）**方塊中，輸入 hello 使用者的電子郵件地址。 然後，選取 [驗證帳戶]。 hello 系統新增登入認證 toohello 使用者帳戶。

    ![輸入電子郵件，並選取 [驗證帳戶]](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. 選取 hello**儲存**圖示。

    ![[儲存] 圖示](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> 您可以讀取這些指示 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定您的應用程式 ！ 選取 [新增 hello 應用程式之後**Active Directory** > **企業應用程式**，選取 hello**單一登入**] 索引標籤。您可以存取 hello 內嵌文件以 hello**組態**區段中的，在 hello hello 頁面底部。 如需詳細資訊，請參閱 [Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)。

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
在本節中，您可以建立 hello Azure 入口網站中名為許 Simon 的測試使用者。

toocreate 在 Azure AD 中的測試使用者：

1. 在 [hello Azure 入口網站，在 hello 左功能表中，選取 [ **Azure Active Directory**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，選取**使用者和群組**，然後選取**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**對話方塊中，選取**新增**。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊中，完成下列步驟的 hello:
 
    1. 在 [hello**名稱**方塊中，輸入**BrittaSimon**。

    2. 在 [hello**使用者名**方塊中，輸入 hello 使用者許 Simon hello 電子郵件地址。

    3. 選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 [hello**密碼**方塊。

    4. 選取 [ **建立**]。

        ![hello [使用者] 對話方塊](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![建立 Azure AD 使用者][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a>建立 SAP Business Object Cloud 測試使用者

必須 SAP 商務物件雲端中佈建 azure AD 使用者，才可以登入 tooSAP 商務物件的雲端。 在 SAP Business Object Cloud 中，必須以手動方式進行佈建。

tooprovision 使用者帳戶：

1. Tooyour SAP 商務物件雲端公司網站管理員身分登入。

2. 選取 [功能表] > [安全性] > [使用者]。

    ![新增員工](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. 在 [hello**使用者**tooadd 新的使用者詳細資料頁面選取** + **。 

    ![新增使用者頁面](./media/active-directory-saas-sapboc-tutorial/user4.png)

    接著，完成下列步驟的 hello:

    1. 在 [hello**使用者識別碼**方塊中，輸入 hello hello 使用者，使用者識別碼，例如**許**。

    2. 在 [hello**名字**方塊中，例如輸入 hello 使用者 hello 名字**許**。

    3. 在 [hello**姓氏**方塊中，輸入 hello 最後一個 hello 使用者名稱，例如**Simon**。

    4. 在 [hello**顯示名稱**方塊中，輸入 hello 完整 hello 使用者名稱，例如**許 Simon**。

    5. 在 [hello**電子郵件**方塊中，輸入 hello hello 使用者電子郵件地址，例如** brittasimon@contoso.com **。

    6. 在 [hello**選取角色**頁面上，選取 hello hello 使用者適當的角色，然後選取**確定**。

      ![選取角色](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. 選取 hello**儲存**圖示。  


### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您允許 hello 使用者許 Simon toouse Azure AD 單一登入授與 hello 使用者帳戶存取 tooSAP 商務物件的雲端。

tooassign 許 Simon tooSAP 商務物件雲端：

1. 在 [hello Azure 入口網站，開啟 hello 應用程式檢視，並前往 toohello 目錄檢視。 選取 [企業應用程式]，然後選取 [所有應用程式]。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**SAP 商務物件雲端**。

    ![設定單一登入](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. 在 [hello 左窗格中，選取 [**使用者和群組**。

    ![選取 [使用者和群組]][202] 

4. 選取 [新增] 。 然後，在 hello**將作業加入**頁面上，選取**使用者和群組**。

    ![hello 新增指派] 頁面][203]

5. 在 [hello**使用者和群組**頁面 hello 清單中的使用者，選取**許 Simon**。

6. 在 [hello**使用者和群組**頁面上，選取**選取**。

7. 在 [hello**將作業加入**頁面上，選取**指派**。

![指派 hello 使用者角色][200] 
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您測試您 Azure AD 單一登入組態使用 hello 存取面板。

當您選取 hello SAP 商務物件雲端磚 hello 存取面板中時，您應該會自動登入 tooyour SAP 商務物件雲端應用程式。

如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

