---
title: "aaaSelf 服務應用程式存取和使用 Azure Active Directory 委派的管理 |Microsoft 文件"
description: "本文說明 tooenable 自助應用程式如何存取和使用 Azure Active Directory 委派的管理。"
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
ms.openlocfilehash: 90bec3bd71796f22a782929b028db0d18c3aa1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-application-access-and-delegated-management-with-azure-active-directory"></a>Azure Active Directory 的自助式應用程式存取和委派管理
為使用者啟用自助式功能是常見的企業 IT 案例。 許多應用程式和 hello 人員 best-informed toomake 存取大量的使用者授與的決策可能不是 hello 目錄管理員。 小組負責人或其他委派的系統管理員通常 hello 最佳人員 toodecide 可以存取應用程式。 不過，它是 hello 使用者使用 hello 應用程式，以及 hello 使用者知道他們需要 toobe 無法 toodo 他們的工作。

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。 

自助式應用程式存取是 [Azure Active Directory Premium](https://azure.microsoft.com/trial/get-started-active-directory/) P1 和 P2 授權的一項功能，可讓目錄管理員：

* 讓使用者 toorequest 存取 tooapplications 使用 [取得更多應用程式] 磚中 hello [Azure AD 存取面板](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)
* 設定使用者可以要求存取哪些應用程式
* 設定可為使用者 toobe 無法 tooself 指派存取 tooan 應用程式需要核准
* 應該核准 hello 要求及管理每個應用程式的存取設定

這項功能現在支援所有預先整合和自訂應用程式，以支援同盟或密碼單一登入 hello [Azure Active Directory 應用程式庫](https://azure.microsoft.com/marketplace/active-directory/all/)，包括 Salesforce、 Dropbox 等應用程式Google Apps 等等。
這篇文章說明如何：

* 設定一般使用者的自助式應用程式存取權，包括設定選擇性核准工作流程 
* 委派存取管理的特定應用程式 toohello 最適合組織中的人員，並讓它們 toouse hello Azure AD 存取面板 tooapprove 存取要求、 直接指派存取 tooselected 使用者，或者 （選擇性） 設定設定密碼單一登入的應用程式存取的認證

## <a name="configuring-self-service-application-access"></a>設定自助式應用程式存取權
tooenable 自助式應用程式存取和設定的應用程式可以加入或要求您的使用者，請遵循這些指示。

1. 登入 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)。

2.   在 [hello **Active Directory**區段中，選取您的目錄，然後選取 hello**應用程式**] 索引標籤。 

3. 選取 hello**新增**按鈕，並使用 hello 圖庫選項 tooselect 新增應用程式。

4. 加入您的應用程式之後，您會收到 hello 應用程式的 [快速入門] 頁面。 按一下**設定單一登入**、 選取 hello 需單一登入模式，並儲存 hello 設定。 

5. 接下來，選取 [hello**設定**] 索引標籤 tooenable 使用者 toorequest access toothis 應用程式從 hello Azure AD 存取面板中，設定**允許自助應用程式存取**太**是**.
  
  ![][1]

6. toooptionally 設定的存取要求的核准工作流程設定**授與存取權之前需要核准**太**是**。 然後可以選取一個或多個核准者，使用 hello**核准者** 按鈕。

  核准者可以是 Azure AD 帳戶，hello 組織中的任何使用者，而且可能會負責帳戶佈建、 授權，或任何其他商務程序需要授與存取 tooan 應用程式之前的組織。 hello 群組擁有者的一或多個共用帳戶群組，以便將指派的共用帳戶透過這些使用者存取這些群組 toogive hello 使用者 tooone，甚至可能是 hello 核准者。 

  如果沒有核准，然後使用者立即取得 hello 應用程式加入的 tootheir Azure AD 存取面板。 如果已設定 hello 應用程式註冊[自動使用者佈建](active-directory-saas-app-provisioning.md)，或已設定[[使用者管理] 的密碼 SSO 模式](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)，hello 使用者應該已經有使用者帳戶，並知道 hello 密碼。

7. 如果 hello 應用程式已設定的 toouse 密碼型單一登入，然後允許 hello 核准者代表每個使用者 tooset hello 登入認證的選項也會提供。 如需詳細資訊，請參閱 hello 一節[委派存取管理](#delegated-application-access-management)。

8. 最後，hello **Self-Assigned 使用者群組**顯示 hello hello 群組是使用的 toostore hello 使用者被授與或指派存取 toohello 應用程式的名稱。 hello 存取核准者會成為此群組的 hello 擁有者。 如果顯示 hello 群組名稱不存在，它會自動建立。 選擇性地 hello 群組名稱也可以設定 toohello 現有的群組名稱。

9. toosave hello 組態中，按一下 **儲存**在 hello 囉 」 畫面底部。 現在使用者可以從 hello 存取面板 toorequest access toothis 應用程式。

10. tootry hello 終端使用者體驗，登入貴組織的 Azure AD 存取面板 https://myapps.microsoft.com，最好使用不同的帳戶不是應用程式核准者。 

11. 在 hello**應用程式**索引標籤上，按一下 hello**取得更多應用程式**磚。 這個磚會顯示所有已啟用自助式應用程式存取與 hello 能力 toosearch hello 左側的應用程式類別目錄篩選條件的 hello 目錄中的 hello 應用程式庫。 

12. 按一下 應用程式就會啟動 hello 要求程序。 如果沒有核准程序是必要項目，則 hello 應用程式會立即加入之下 hello**應用程式**簡短確認結束之後的索引標籤。 如果需要核准，然後您會看到對話方塊，指出此項目，並傳送 toohello 核准者的電子郵件。 您必須登入 hello 存取面板為非核准者 toosee 此要求程序。

13. hello 電子郵件將 hello 核准者 toosign 導向到 hello Azure AD 存取面板中，並核准 hello 要求。 一旦 hello 要求獲得核准後 （且已執行任何特殊的處理序，您定義的 hello 核准者），hello 使用者會看見 hello 應用程式會出現在其**應用程式**，他們可以登入，到其中的索引標籤。

## <a name="delegated-application-access-management"></a>委派的應用程式存取管理
應用程式存取核准者可以是最適當人員 tooapprove hello 組織中的任何使用者或拒絕存取 toohello 應用程式有問題。 這位使用者可能會負責將帳戶佈建、 授權，或任何其他商務程序授與存取 tooan 應用程式之前需要您的組織。

當設定上面所述的自助式應用程式存取，任何指派給核准者看到的應用程式額外**管理應用程式**hello Azure AD 存取面板，其顯示它們的應用程式中的磚hello 存取系統管理員。 按一下某個應用程式會顯示包含數個選項的畫面。

![][2]

### <a name="approve-requests"></a>核准要求
hello**核准要求**磚允許核准者 toosee 任何暫止核准特定 toothat 應用程式和重新導向 toohello 核准即 hello 要求的 索引標籤可以確認或拒絕。 每次要求建立時，指示哪些 toodo hello 核准者也會收到自動化電子郵件。

### <a name="add-users"></a>新增使用者
hello**新增使用者**磚允許核准者 toodirectly 選取授與使用者存取 toohello 應用程式。 按一下此磚後, hello 核准者會看到對話方塊可讓它們 tooview 並搜尋使用者在他們的目錄。 這些使用者的 Azure AD 存取面板或 Office 365 中的 hello 應用程式中加入使用者結果。 是否需要任何手動佈建程序的使用者在 hello hello 使用者之前的應用程式中，可以 toosign 然後 hello 核准者應該指派存取權之前執行此程序。  

### <a name="manage-users"></a>管理使用者
hello**管理使用者**磚允許核准者 toodirectly 更新或移除哪些使用者可以存取 toohello 應用程式。 

### <a name="configure-password-sso-credentials-if-applicable"></a>設定密碼 SSO 認證 (如果適用)
hello**設定**磚僅會顯示是否由 IT 系統管理員 toouse 密碼型單一登入，hello hello 應用程式設定和 hello 系統管理員授與 hello 核准者 hello 能力 tooset 密碼 SSO 認證如先前所述。 選取時，hello 核准者會看見數個選項 hello 認證的傳播的 tooassigned 使用者的方式：

![][3]

* **使用者以自己的密碼登入**– 在此模式中，hello 分派使用者了解使用者名稱及密碼 hello 應用程式，則與會提示的 tooenter 它們在其第一個登入 toohello 應用程式時。 hello 案例對應 toohello 密碼 SSO 案例在 hello[使用者管理認證](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)。
* **使用者會自動登入使用我管理的個別帳戶**– 在此模式中，指派的 hello 不必要的 tooenter 或使用者知道他們的應用程式特定的認證登入 hello 應用程式時。 相反地，hello 核准者設定為每個使用者指派使用 hello 存取之後 hello 認證**新增使用者**磚。 Hello 使用者按一下時其存取面板或 Office 365 中的 hello 應用程式，它們會使用自動登入 hello hello 核准者設定的認證。 hello 案例對應 toohello 密碼 SSO 案例在 hello[系統管理員管理認證](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)。
* **使用者會自動登入使用我管理的單一帳戶**-特殊案例中，這種情況時，才能適當 toouse 所有指派的使用者需要 toobe 授與使用單一的共用的帳戶的存取權。 這項功能 hello 最常見使用案例是使用社交媒體應用程式，其中組織具有單一 「 公司 」 帳戶，而且多個使用者需要 toomake 更新 toothat 帳戶。 hello 案例也對應 toohello 密碼 SSO 案例在 hello[系統管理員管理認證](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)。 不過，選取此選項之後，hello 核准者將會提示的 tooenter hello 使用者名稱和 hello 單一的共用帳戶的密碼。 完成後，所有指派的使用者會登入其 Azure AD 存取面板或 Office 365 中的 hello 應用程式上按一下時，請使用此帳戶。

## <a name="additional-resources"></a>其他資源
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)

<!--Image references-->
[1]: ./media/active-directory-self-service-application-access/ssaa_admin.PNG
[2]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app.PNG
[3]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app_config.PNG
