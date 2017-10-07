---
title: "在 Azure AD 中的 aaaManage 同盟憑證 |Microsoft 文件"
description: "了解如何 toocustomize hello 到期日您同盟的憑證，和如何 toorenew 憑證即將到期。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f516f7f0-b25a-4901-8247-f5964666ce23
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/09/2017
ms.author: jeedes
ms.openlocfilehash: e17622d25c9babfa295cc0bb68c24e21b8c574d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-certificates-for-federated-single-sign-on-in-azure-active-directory"></a>在 Azure Active Directory 中管理同盟單一登入的憑證
本文章涵蓋常見問題的解答，以及 Azure Active Directory (Azure AD) 建立 tooestablish toohello 憑證同盟單一登入 (SSO) tooyour SaaS 應用程式相關的資訊。 從 hello Azure AD app 資源庫，或使用非組件庫的應用程式範本，請新增應用程式。 使用 hello 同盟 SSO 選項設定 hello 應用程式。

本文是所設定的 SAML 同盟透過 toouse Azure AD 的 SSO 相關只有 tooapps hello 下列範例所示：

![Azure AD 單一登入](./media/active-directory-sso-certs/saml_sso.PNG)

## <a name="auto-generated-certificate-for-gallery-and-non-gallery-applications"></a>為資源庫和非資源庫應用程式自動產生的憑證
當您從 hello 圖庫新增新的應用程式，並設定 SAML 型登入時，Azure AD 會產生的憑證有效期為三年的 hello 應用程式。 您可以將此憑證從 hello **SAML 簽章憑證**> 一節。 組件庫的應用程式，選項 toodownload hello 憑證或中繼資料，根據 hello hello 應用程式的需求而定，可能會顯示這一節。

![Azure AD 單一登入](./media/active-directory-sso-certs/saml_certificate_download.png)

## <a name="customize-hello-expiration-date-for-your-federation-certificate-and-roll-it-over-tooa-new-certificate"></a>自訂 hello 同盟憑證的到期日和變換 tooa 新憑證
根據預設，憑證會設定 tooexpire 後三年。 您可以藉由完成下列步驟的 hello 選擇不同的到期日期，您的憑證。
hello 螢幕擷取畫面的 hello 不錯的範例中，使用 Salesforce，但是這些步驟可以套用 tooany 同盟 SaaS 應用程式。

1. 在 [hello [Azure 入口網站](https://aad.portal.azure.com)，按一下**企業應用程式**在 hello 左的窗格，然後按一下 [**新的應用程式**上 hello**概觀**頁面上：

   ![開啟 hello SSO 組態精靈](./media/active-directory-sso-certs/enterprise_application_new_application.png)

2. 搜尋 hello 組件庫的應用程式，然後選取您想 tooadd hello 應用程式。 如果找不到所需的 hello 應用程式，新增 hello 應用程式使用 hello**非組件庫的應用程式**選項。 只有在 hello （P1 和 P2） 的 Azure AD Premium SKU 中使用這項功能。

    ![Azure AD 單一登入](./media/active-directory-sso-certs/add_gallery_application.png)

3. 按一下 hello**單一登入**中 hello 左窗格和 [變更連結**單一登入模式**太**SAML 型登入**。 這個步驟會為您的應用程式產生三年的憑證。

4. toocreate 新的憑證，按一下 hello**建立新憑證**hello 中的連結**SAML 簽章憑證**> 一節。

    ![產生新的憑證](./media/active-directory-sso-certs/create_new_certficate.png)

5. hello**建立新的憑證**連結會開啟 hello 行事曆控制項。 您可以設定任何日期和時間設定 toothree 年 hello 從目前的日期。 hello 選取日期和時間是您的新憑證的 hello 新的到期日期和時間。 按一下 [儲存] 。

    ![下載，然後上傳 hello 憑證](./media/active-directory-sso-certs/certifcate_date_selection.PNG)

6. 現在可用 toodownload hello 新憑證。 按一下 hello**憑證**連結 toodownload 它。 此時，您的憑證不在作用中。 當您想 tooroll toothis 憑證上時，選取 hello**啟用新的憑證**核取方塊，然後按一下**儲存**。 從該點，Azure AD 會開始使用簽署 hello 回應 hello 新憑證。

7.  toolearn 如何 tooupload hello 憑證 tooyour 特定 SaaS 應用程式，請按一下 hello**檢視應用程式設定教學課程**連結。

## <a name="renew-a-certificate-that-will-soon-expire"></a>更新即將到期的憑證
hello 下列更新步驟應該導致為您的使用者沒有顯著的停機時間。 此區段功能 Salesforce 做為範例，但下列步驟中的 hello 螢幕擷取畫面可以套用 tooany 同盟 SaaS 應用程式。

1. 在 [hello **Azure Active Directory**應用程式**單一登入**頁面上，產生您的應用程式的 hello 新憑證。 您可以按一下 hello**建立新憑證**hello 中的連結**SAML 簽章憑證**> 一節。

    ![產生新的憑證](./media/active-directory-sso-certs/create_new_certficate.png)

2. 選取 hello 預期到期日期和時間，新的憑證然後按一下**儲存**。

3. 下載 hello 憑證在 hello **SAML 簽章憑證**選項。 上傳 hello 新憑證 toohello SaaS 應用程式的單一登入組態畫面。 toolearn 如何 toodo 特定 SaaS 應用程式，請按一下 hello**檢視應用程式設定教學課程**連結。
   
4. 在 Azure AD 中，選取 hello tooactivate hello 新憑證**啟用新的憑證**核取方塊，然後按一下 hello**儲存**hello hello 頁頂端的按鈕。 這在 Azure AD 戶端 hello 彙總 hello 新憑證。 hello hello 憑證狀態變更從**新增**太**Active**。 從該點，Azure AD 會開始使用簽署 hello 回應 hello 新憑證。 
   
    ![產生新的憑證](./media/active-directory-sso-certs/new_certificate_download.png)

## <a name="related-articles"></a>相關文章
* [如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Azure Active Directory 中應用程式管理的文件索引](active-directory-apps-index.md)
* [搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)
* [針對 SAML 型單一登入進行疑難排解](active-directory-saml-debugging.md)
