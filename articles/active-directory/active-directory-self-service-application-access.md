---
title: "Azure Active Directory 的自助式應用程式存取和委派管理 | Microsoft Docs"
description: "本文說明如何啟用 Azure Active Directory 的自助式應用程式存取和委派管理"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 448a7fe8-a162-475e-9ba2-2e3ab59302bc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: asmalser
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 7872d5229cdc053bfb9dc8ddba01785b0f8e5a9a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="self-service-application-access-and-delegated-management-with-azure-active-directory"></a>Azure Active Directory 的自助式應用程式存取和委派管理
為使用者啟用自助式功能是常見的企業 IT 案例。 許多使用者、許多應用程式，以及最有把握做出存取權授與決策的人員可能都不是目錄管理員。 通常決定誰可以存取應用程式的最佳人選是小組負責人或其他委派的系統管理員。 但是，這就是使用應用程式的使用者，而使用者知道他們需要什麼才能進行其作業。

> [!IMPORTANT]
> Microsoft 建議您使用 Azure 入口網站中的 [Azure AD 系統管理中心](https://aad.portal.azure.com)來管理 Azure AD，而不要使用本文所提及的 Azure 傳統入口網站。 

自助式應用程式存取是 [Azure Active Directory Premium](https://azure.microsoft.com/trial/get-started-active-directory/) P1 和 P2 授權的一項功能，可讓目錄管理員：

* 允許使用者使用 [Azure AD 存取面板](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)中的 [取得更多應用程式] 圖格來要求應用程式的存取權
* 設定使用者可以要求存取哪些應用程式
* 設定使用者是否需要竟過核准，才能夠自我分派應用程式的存取權
* 設定誰應該核准要求及管理每個應用程式的存取權

目前在 [Azure Active Directory 應用程式庫](https://azure.microsoft.com/marketplace/active-directory/all/)中支援同盟或密碼型單一登入的所有預先整合和自訂應用程式都支援這項功能，包括 Salesforce、Dropbox、Google Apps 等等。
這篇文章說明如何：

* 設定一般使用者的自助式應用程式存取權，包括設定選擇性核准工作流程 
* 將特定應用程式的存取管理委派給您組織中最適當的人員，讓他們能使用 Azure AD 存取面板來核准存取要求，直接將存取權指派給選取的使用者，或者 (選擇性) 在設定密碼型單一登入時設定應用程式存取的認證

## <a name="configuring-self-service-application-access"></a>設定自助式應用程式存取權
若要啟用自助式應用程式存取權，以及設定一般使用者可以新增或要求哪些應用程式，請遵循這些指示。

1. 登入 [Azure 傳統入口網站](https://manage.windowsazure.com/)。

2.   在 [Active Directory] 區段下選取您的目錄，然後選取 [應用程式] 索引標籤。 

3. 選取 [新增] 按鈕，並使用資源庫選項來選取和新增應用程式。

4. 新增應用程式之後，您將取得 [快速啟動] 頁面。 按一下 [設定單一登入] 、選取所需的單一登入模式，然後儲存設定。 

5. 接下來，選取 [設定] 索引標籤。 若要讓使用者要求從 Azure AD 存取面板存取此應用程式，請將 [允許自助式應用程式存取] 設定為 [是]。
  
  ![][1]

6. 若要選擇性設定存取要求的核准工作流程，請將 [授與存取權前需要核准] 設定為 [是]。 然後可以使用 [核准者]  按鈕來選取一或多個核准者。

  核准者可以是組織中具有 Azure AD 帳戶的任何使用者，而且可能負責帳戶佈建、授權或您的組織在授與應用程式存取權前所需的任何其他商務程序。 核准者甚至可以是一個或多個共用帳戶群組的群組擁有者，而且可以將使用者指派給其中一個群組，讓它們能透過共用帳戶進行存取。 

  如果不需要核准，則使用者會立即將應用程式新增至其 Azure AD 存取面板。 如果應用程式已設定[自動使用者佈建](active-directory-saas-app-provisioning.md)，或已設定[「使用者管理的」密碼 SSO 模式](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)，使用者應該已有使用者帳戶並知道密碼。

7. 如果應用程式已設定為使用密碼型單一登入，則也會提供允許核准者代表每個使用者設定 SSO 認證的選項。 如需詳細資訊，請參閱[委派存取管理](#delegated-application-access-management)一節。

8. 最後，[自我指派的使用者群組] 顯示的群組名稱將用來儲存被授與或指派應用程式存取權的使用者。 存取核准者會成為此群組的擁有者。 如果顯示的群組名稱不存在，系統就會自動建立。 可選擇性將此群組名稱設定為現有群組的名稱。

9. 若要儲存設定，請按一下畫面底部的 [儲存]。 現在使用者就能夠從存取面板要求存取此應用程式。

10. 若要嘗試使用者體驗，請在 https://myapps.microsoft.com 登入您組織的 Azure AD 存取面板，最好使用其他不是應用程式核准者的帳戶。 

11. 在 [應用程式] 索引標籤之下，按一下 [取得更多應用程式] 圖格。 此圖格會顯示目錄中所有已啟用自助式應用程式存取的應用程式庫，並可依左邊的應用程式類別進行搜尋和篩選。 

12. 按一下應用程式可啟動要求程序。 如果需要核准程序，則應用程式會在簡短確認之後，立即新增在 [應用程式]  索引標籤之下。 如果需要核准，則您會看到一個對話方塊如此表示，而且會傳送電子郵件給核准者。 您必須以非核准者身分登入存取面板，才能查看此要求程序。

13. 電子郵件會指示核准者登入 Azure AD 存取面板並核准要求。 一旦核准要求 (並由核准者執行您定義的任何特殊程序)，使用者會看到應用程式出現在其可登入的 [應用程式] 索引標籤之下。

## <a name="delegated-application-access-management"></a>委派的應用程式存取管理
應用程式存取核准者可以是您組織中最適合核准或拒絕存取有問題的應用程式的任何使用者。 此核准者可能負責帳戶佈建、授權或您的組織在授與應用程式存取權前所需的任何其他商務程序。

設定上述的自助式應用程式存取時，所有被指派的應用程式核准者都會在 Azure AD 存取面板中看見額外的 [管理應用程式] 圖格，其中顯示他們身為存取管理員的應用程式。 按一下某個應用程式會顯示包含數個選項的畫面。

![][2]

### <a name="approve-requests"></a>核准要求
[核准要求]  磚可讓核准者看到該應用程式特有的擱置核准，並重新導向至可確認或拒絕要求的 [核准] 索引標籤。 核准者也會在建立要求時收到自動化電子郵件，指示他們該怎麼做。

### <a name="add-users"></a>新增使用者
[新增使用者]  磚可讓核准者直接將應用程式的存取權授予選取的使用者。 按一下此磚時，核准者會看到一個對話方塊，可供檢視與搜尋其目錄中的使用者。 新增使用者會導致應用程式顯示在這些使用者的 Azure AD 存取面板或 Office 365 中。 如果在使用者能夠登入之前，需要在應用程式進行任何手動使用者佈建程序，則核准者應在指派存取權之前執行此程序。  

### <a name="manage-users"></a>管理使用者
[管理使用者]  磚可讓核准者直接更新或移除哪些使用者可存取應用程式。 

### <a name="configure-password-sso-credentials-if-applicable"></a>設定密碼 SSO 認證 (如果適用)
只有在 IT 系統管理員將應用程式設定為使用密碼型單一登入，且系統管理員授與核准者設定密碼 SSO 認證的功能 (如先前所述) 後，才會顯示 [設定] 圖格。 選取後，核准者會看見幾個選項，可供選取如何將認證散佈給指派的使用者：

![][3]

* **使用者使用自己的密碼登入** – 在此模式中，指派的使用者知道其用於應用程式的使用者名稱和密碼，而且系統會提示他們在第一次登入應用程式時輸入這些資訊。 此案例對應於[使用者管理認證](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)的密碼 SSO 案例。
* **使用者使用我管理的各個帳戶自動登入** – 在此模式中，指派的使用者在登入應用程式時，不需要輸入或知道其應用程式特定的認證。 相反地，核准者會在使用 [新增使用者]  磚指派存取權之後，為每個使用者設定認證。 當使用者按一下其存取面板或 Office 365 中的應用程式時，系統會使用核准者所設定的認證將他們自動登入。 此案例對應於[系統管理員管理認證](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)的密碼 SSO 案例。
* **使用者使用我管理的單一帳戶自動登入** - 這是特殊案例，適用於當所有指派的使用者必須獲得使用單一共用帳戶的權限時。 此功能的最常見使用案例就是社交媒體應用程式，案例中的組織有單一「公司」帳戶，而多個使用者必須對該帳戶進行更新。 此案例也對應於[系統管理員管理認證](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)的密碼 SSO 案例。 不過，選取此選項之後，系統會提示核准者輸入單一共用帳戶的使用者名稱和密碼。 完成後，所有指派的使用者會在按一下 Azure AD 存取面板或 Office 365 中的應用程式時，使用此帳戶登入。

## <a name="additional-resources"></a>其他資源
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)

<!--Image references-->
[1]: ./media/active-directory-self-service-application-access/ssaa_admin.PNG
[2]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app.PNG
[3]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app_config.PNG
