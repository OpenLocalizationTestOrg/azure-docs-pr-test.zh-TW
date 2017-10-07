---
title: "教學課程：Azure Active Directory 與 Cisco Spark 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Cisco Spark 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 386c4fd816095e1c61de01dd1dee1bbd00311a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a>教學課程：Azure Active Directory 與 Cisco Spark 整合

在此教學課程中，您學會如何 toointegrate Cisco 二手與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Cisco Spark 可以提供下列優點 hello:

- 您可以控制存取 tooCisco Spark Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooCisco Spark （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 與 Cisco Spark 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Cisco Spark 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Cisco Spark
2. 設定並測試 Azure AD 單一登入

## <a name="adding-cisco-spark-from-hello-gallery"></a>從 hello 圖庫加入 Cisco Spark
tooconfigure hello 整合 Cisco Spark 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Cisco Spark。

**tooadd Cisco Spark 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Cisco Spark**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. 在 hello 結果 窗格中，選取  **Cisco Spark**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Cisco Spark 設定和測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow Cisco Spark 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 Cisco Spark 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

Cisco Spark 中指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及測試 Azure AD 單一登入與 Cisco Spark，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Cisco Spark](#creating-a-cisco-spark-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Cisco Spark 中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Cisco Spark 應用程式中。

**tooconfigure Azure AD 單一登入使用 Cisco Spark 執行 hello 下列步驟：**

1. 在 Azure 入口網站上 hello hello **Cisco Spark**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. 在 hello **Cisco Spark 網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    a. 在 hello**登入 URL**文字方塊中，輸入與 URL:`https://web.ciscospark.com/#/signin`

    b. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://idbroker.webex.com/<companyname>`

    > [!NOTE] 
    > 這不是真實的值。 更新此值以 hello 實際的識別項。 請連絡[Cisco Spark 用戶端支援小組](https://support.ciscospark.com/)tooget 此值。 
 
4. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. Cisco Spark 應用程式預期 hello SAML 判斷提示 toocontain 特定屬性。 設定下列屬性，此應用程式的 hello。 您可以從 hello 管理這些屬性的 hello 值**使用者屬性**應用程式整合頁面上的一節。 hello 下列螢幕擷取畫面會顯示這個範例。
    
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. 在 hello**使用者屬性**區段 hello**單一登入** 對話方塊中，上述 hello 映像中所示設定 SAML 權杖屬性和執行下列步驟的 hello:
    
    | 屬性名稱  | 屬性值 |
    | --------------- | -------------------- |    
    |   UID    | user.userprincipalname |   

    a. 按一下**加入屬性**tooopen hello**加入屬性**對話方塊。

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    b. 在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。
    
    c. 從 hello**值**清單，顯示該資料列的型別 hello 屬性值。
    
    d. 按一下 [確定] 。

7. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. 登入太[Cisco 雲端共同作業管理](https://admin.ciscospark.com/)以完整系統管理員認證。

9. 選取**設定**在 hello**驗證**區段中，按一下**修改**。
   
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. 選取 整合協力廠商識別提供者 **（進階）**和移 toohello 下一個畫面。

11. 在 hello**匯入 Idp 中繼資料**頁面上，可以拖曳和卸除 hello Azure AD 中繼資料檔案放入 hello 頁面或使用 hello 檔案瀏覽器選項 toolocate 並上傳 hello Azure AD 中繼資料檔案。 然後，選取 [需要中繼資料中憑證授權單位所簽署的憑證 (較安全)]，然後按 [下一步]。 
    
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. 選取 [測試 SSO 連接]，並在新的瀏覽器索引標籤開啟時，透過登入向 Azure AD 進行驗證。

13. 傳回 toohello **Cisco 雲端共同作業管理**瀏覽器索引標籤。如果 hello 測試成功，請選取**這項測試成功。**啟用單一登入 選項，然後按 下一步。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-cisco-spark-test-user"></a>建立 Cisco Spark 測試使用者

在本節中，您要在 Cisco Spark 中建立名為 Britta Simon 的使用者。 在本節中，您要在 Cisco Spark 中建立名為 Britta Simon 的使用者。

1. 移 toohello [Cisco 雲端共同作業管理](https://admin.ciscospark.com/)以完整系統管理員認證。

2. 按一下 [使用者]，然後按一下 [管理使用者]。
   
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. 在 [hello**管理使用者**視窗中，選取**手動新增或修改使用者**按一下**下一步]**。

4. 選取 [名稱和電子郵件地址]。 然後，填滿出 hello 文字方塊中，如下所示：
   
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    a. 在 hello**名字**文字方塊中，輸入**許**。 
    
    b. 在 hello**姓氏**文字方塊中，輸入**Simon**。
    
    c. 在 hello**電子郵件地址**文字方塊中，輸入 **britta.simon@contoso.com** 。

5. 按一下 hello 加上簽章 tooadd 許 Simon。 然後按 [下一步] 。

6. 在 hello**新增使用者的服務**視窗中，按一下 **儲存**然後**完成**。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與存取 tooCisco Spark 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooCisco Spark，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Cisco Spark**。

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。

當您按一下 hello Cisco Spark 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Cisco Spark 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

