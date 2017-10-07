---
title: "教學課程：Azure Active Directory 與 ArcGIS Online 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 ArcGIS Online 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a>教學課程：Azure Active Directory 與 ArcGIS Online 整合

在此教學課程中，您學會如何 toointegrate ArcGIS Online 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 ArcGIS 線上可以提供下列優點 hello:

- 您可以控制存取 tooArcGIS 線上 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooArcGIS 線上 （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>必要條件

tooconfigure 與線上 ArcGIS 的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 ArcGIS Online 單一登入功能的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 新增線上 ArcGIS 從 hello 組件庫
2. 設定並測試 Azure AD 單一登入

## <a name="adding-arcgis-online-from-hello-gallery"></a>新增線上 ArcGIS 從 hello 組件庫
tooconfigure hello 整合 ArcGIS 線上到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd ArcGIS 線上。

**tooadd ArcGIS 線上 hello 圖庫中，從執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新的應用程式**上 hello hello 對話方塊 tooadd 新應用程式頂端的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**ArcGIS 線上**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. 在 hello 結果 窗格中，選取  **ArcGIS 線上**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 ArcGIS Online 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 ArcGIS 線上中是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello ArcGIS 線上中相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** ArcGIS 線上中。

tooconfigure 和測試 Azure AD 單一登入與 ArcGIS Online，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立線上 ArcGIS 的測試使用者](#creating-an-arcgis-online-test-user)** -toohave 許 Simon ArcGIS Online 連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 ArcGIS 線上應用程式中。

**tooconfigure Azure AD 單一登入與 ArcGIS Online，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **ArcGIS 線上**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. 在 hello **ArcGIS 線上網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    在 hello**登入 URL**文字方塊中，使用下列模式的 hello 類型 hello 值：`https://<company>.maps.arcgis.com`

    > [!NOTE] 
    > 這個值不是真正的 hello。 更新此值以 hello 實際的登入 URL。 請連絡[ArcGIS 線上的用戶端支援小組](http://support.esri.com/)tooget 此值。 

4. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。

    ![設定單一登入](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 ArcGIS 公司網站。

7. 按一下 [編輯設定]。

    ![編輯設定](./media/active-directory-saas-arcgis-tutorial/ic784742.png "編輯設定")

8. 按一下 [安全性] 。

    ![安全性](./media/active-directory-saas-arcgis-tutorial/ic784743.png "安全性")

9. 在 [企業登入] 下方，按一下 [設定識別提供者]。

    ![企業登入](./media/active-directory-saas-arcgis-tutorial/ic784744.png "企業登入")

10. 在 hello**設定身分識別提供者**組態頁面上，執行下列步驟的 hello:
   
    ![設定識別提供者](./media/active-directory-saas-arcgis-tutorial/ic784745.png "設定識別提供者")
   
    a. 在 hello**名稱**文字方塊中，輸入您的組織名稱。

    b. 如**hello 企業身分識別提供者的中繼資料，才會提供使用**，選取**檔案**。

    c. tooupload 您下載的中繼資料檔案中，按一下 **選擇檔案**。

    d. 按一下 [設定識別提供者]。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. 跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. 在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**許 Simon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-an-arcgis-online-test-user"></a>建立 ArcGIS Online 測試使用者

在順序 tooenable Azure AD 使用者 toolog 入 ArcGIS Online，您必須是佈建到 ArcGIS 線上。  
在 ArcGIS 線上 hello 情況下，佈建須手動進行。

**tooprovision 使用者帳戶，執行下列步驟的 hello:**

1. 登入 tooyour **ArcGIS**租用戶。

2. 按一下 [邀請成員]。
   
    ![邀請成員](./media/active-directory-saas-arcgis-tutorial/ic784747.png "邀請成員")

3. 選取 [自動新增成員而不傳送電子郵件]，然後按 [下一步]。
   
    ![自動新增成員](./media/active-directory-saas-arcgis-tutorial/ic784748.png "自動新增成員")

4. 在 hello**成員**對話方塊頁面上，執行下列步驟的 hello:
   
     ![新增並檢閱](./media/active-directory-saas-arcgis-tutorial/ic784749.png "新增並檢閱")
    
     a. 輸入 hello**電子郵件**，**名字**，和**姓氏**想 tooprovision 之有效 AAD 帳戶。
  
     b. 按一下 [新增並檢閱]。
5. 檢閱您所輸入，然後按一下 hello 資料**新增成員**。
   
    ![新增成員](./media/active-directory-saas-arcgis-tutorial/ic784750.png "新增成員")
        
    > [!NOTE]
    > hello Azure Active Directory 帳戶持有者將收到一封電子郵件，並遵循連結 tooconfirm 他們的帳戶之前就會生效。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與存取 tooArcGIS 線上啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooArcGIS 上線，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**ArcGIS 線上**。

    ![設定單一登入](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello ArcGIS 線上磚 hello 存取面板中的時，您應該取得自動登入 tooyour ArcGIS 線上應用程式。
如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

