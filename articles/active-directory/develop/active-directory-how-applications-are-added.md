---
title: "aaaHow 應用程式會加入 tooAzure Active Directory。"
description: "本文說明如何將應用程式加入 Azure Active Directory tooan 執行個體。"
services: active-directory
documentationcenter: 
author: shoatman
manager: kbrint
editor: 
ms.assetid: 3321d130-f2a8-4e38-b35e-0959693f3576
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/09/2016
ms.author: shoatman
ms.custom: aaddev
ms.openlocfilehash: 3ca710c58a403b52e8b728202ad9010f4873bcea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-and-why-applications-are-added-tooazure-ad"></a>將應用程式如何及為何加入 tooAzure AD
其中一個 hello 最初令人感到困惑項目在您的 Azure Active Directory 執行個體中檢視應用程式的清單時了解 hello 應用程式的來源，以及為何發生。  這篇文章會提供應用程式都可以在 hello 目錄和您提供可協助您了解如何應用程式的來源目錄中的 toobe 內容的方式的高層級概觀。

## <a name="what-services-does-azure-ad-provide-tooapplications"></a>有哪些服務 Azure AD 提供 tooapplications？
應用程式會加入 tooAzure AD tooleverage 一或多個 hello 它所提供的服務。  這些服務包括：

* 應用程式驗證與授權
* 使用者驗證與授權
* 使用同盟或密碼的單一登入 (SSO)
* 使用者佈建與同步處理
* 以角色為基礎的存取控制。使用 hello 目錄 toodefine 應用程式角色 tooperform 角色為基礎的應用程式中的授權檢查。
* oAuth 授權服務 （使用 Office 365 和其他 Microsoft 應用程式 tooauthorize 存取 tooAPIs/資源）。
* 發佈應用程式與 proxy;發行應用程式從私人網路 toohello 網際網路

## <a name="how-are-applications-represented-in-hello-directory"></a>應用程式代表 hello 目錄中的？
代表 hello 2 的物件，使用 Azure AD 中應用程式： 應用程式物件與服務主體物件。  一個應用程式物件，註冊中 「 家用 」 / 「 擁有者 」 或 「 發行 」 目錄以及一個或多個服務主體物件，表示它會每個目錄中的 hello 應用程式。  

hello 應用程式物件描述 hello 應用程式 tooAzure AD （hello 多租用戶的服務），而且可能包括 hello 下列任何一項: (*注意*： 這不是獨占清單。)

* 名稱、標誌和發行者
* 密碼 （對稱和/或非對稱金鑰會用 tooauthenticate hello 應用程式）
* API 相依性 (oAuth)
* API/資源/發佈範圍 (oAuth)
* 應用程式角色 (RBAC)
* SSO 中繼資料和組態 (SSO)
* 使用者佈建中繼資料和組態
* Proxy 中繼資料和組態

hello 服務主要是每個 hello 應用程式會包括其主目錄的目錄中的 hello 應用程式的記錄。  hello 服務主體：

* 是指回 tooan 應用程式物件，透過 hello 應用程式 id 屬性
* 記錄本機使用者和群組應用程式角色指派
* 記錄本機使用者和系統管理員權限授與 toohello 應用程式
  * 例如： hello 應用程式 tooaccess 特定使用者的電子郵件的權限
* 記錄本機原則，包括條件式存取原則
* 記錄應用程式的本機替代本機設定
  * 宣告轉換規則
  * 屬性對應 (使用者佈建)
  * （如果 hello 應用程式支援的自訂角色），租用戶特定的應用程式角色
  * 名稱/標誌

### <a name="a-diagram-of-application-objects-and-service-principals-across-directories"></a>目錄間的應用程式物件和服務主體圖表
![說明應用程式物件和服務主體如何與現有 Azure AD 執行個體共存的圖表。][apps_service_principals_directory]

您可以從 hello 上圖中看到。  Microsoft 會維護兩個目錄內部 （左側 hello），它使用 toopublish 應用程式。

* 一個用於 Microsoft 應用程式 (Microsoft 服務目錄)
* 一個用於預先整合的協力廠商應用程式 (應用程式庫目錄)

應用程式的發行者/廠商與 Azure AD 整合所需的 toohave 發行目錄。  (某些 SAAS 目錄)。

自行新增的應用程式包括：

* 自行開發的應用程式 (與 AAD 整合)
* 為單一登入而進行連線的應用程式
* 使用發行的應用程式 hello Azure AD 應用程式 proxy。

### <a name="a-couple-of-notes-and-exceptions"></a>幾個附註和例外狀況
* 並非所有的服務主體點後 tooapplication 物件。  是嗎？ 最初是建立 Azure AD 時 hello 服務會提供更多限制 tooapplications 所以 hello 服務主體已足夠完成建立應用程式識別。  hello 原始服務主體已更接近圖形 toohello Windows Server Active Directory 服務帳戶。  基於這個理由，就仍然可以 toocreate 服務主體使用 hello Azure AD PowerShell，而不需要第一個建立的應用程式物件。  hello Graph API 要求的應用程式物件之前建立服務主體。
* 並非所有的 hello 上面所述的資訊目前是以程式設計方式公開。  只有 hello 下列 hello UI 中的項目：
  * 宣告轉換規則
  * 屬性對應 (使用者佈建)
* 如需詳細資訊的詳細資訊 hello 服務主體和應用程式物件，請參閱 toohello Azure AD Graph REST API 參考文件。  *提示*: hello Azure AD Graph API 文件是目前可用的 Azure AD 的 hello 最接近的動作 tooa 結構描述參考。  
  * [應用程式](https://msdn.microsoft.com/library/azure/dn151677.aspx)
  * [服務主體](https://msdn.microsoft.com/library/azure/dn194452.aspx)

## <a name="how-are-apps-added-toomy-azure-ad-instance"></a>應用程式如何加入 toomy Azure AD 執行個體？
有許多方法可加入應用程式 tooAzure AD:

* 新增應用程式從 hello [Azure Active Directory 應用程式庫](https://azure.microsoft.com/updates/azure-active-directory-over-1000-apps/)
* 註冊/登入與 Azure Active Directory 整合的協力廠商應用程式 (例如：[Smartsheet](https://app.smartsheet.com/b/home) 或 [DocuSign](https://www.docusign.net/member/MemberLogin.aspx))
  * 在向上/使用者在註冊時為問的 toogive 權限 toohello 應用程式 tooaccess 其設定檔和其他權限。  第一個人 toogive hello 同意原因代表 hello 應用程式 toobe 加入的 toohello 目錄服務主體。
* 註冊/登入 Microsoft 線上服務 (如 [Office 365](http://products.office.com/)
  * 當您訂閱 tooOffice 365 開始試用版的一個或多個服務主體的建立 hello 目錄代表 hello 使用的 toodeliver hello 功能的所有 Office 365 與相關聯的各種服務。
  * 某些的 Office 365 服務，例如 SharePoint 上持續 tooallow 之間的通訊安全包括工作流程的元件建立服務主體。
* Hello，請參閱 Azure 管理入口網站中新增您正在開發應用程式： https://msdn.microsoft.com/library/azure/dn132599.aspx
* 新增您使用 Visual Studio 開發的應用程式，請參閱：
  * [ASP.Net 驗證方法](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions)
  * [連接的服務](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)
* 新增應用程式 toouse toouse hello [Azure AD Application Proxy](https://msdn.microsoft.com/library/azure/dn768219.aspx)
* 連接應用程式進行使用 SAML 或密碼 SSO 的單一登入
* 許多其他項目，包括在 Azure 中的各種開發人員經驗和/在跨開發人員中心的 API 總管體驗

## <a name="who-has-permission-tooadd-applications-toomy-azure-ad-instance"></a>誰有權限 tooadd 應用程式 toomy Azure AD 執行個體？
只有全域系統管理員可以：

* 新增應用程式從 hello Azure AD app 資源庫 （預先整合第 3 個合作對象應用程式）
* 發行應用程式使用 Azure AD Application Proxy hello

您的目錄中的所有使用者都有權限 tooadd 應用程式所開發並自行決定哪些應用程式透過它們共用/授與存取 tootheir 組織資料。  *請記住向上/tooan 應用程式中的使用者登，並授與權限可能會導致服務主體所建立。*

這個可能一開始音效有關，但保留 hello 下列幾點：

* 應用程式已能夠 tooleverage Windows Server Active Directory 進行使用者驗證，而不需要在 hello 目錄中註冊/記錄 hello 應用程式 toobe 多年。  現在 hello 組織會改善可視性 tooexactly 多少應用程式使用了 hello 目錄和苦頭 for。
* 不需要系統管理導向的應用程式發佈/註冊程序。  Active Directory Federation Services 與可能的系統管理員必須 tooadd 應用程式做為信賴憑證者的合作對象代表開發人員。  現在開發人員可以自助。
* 簽章在/總 tooapps 基於商業用途使用其組織帳戶的使用者是個好方法。  如果後續離開 hello 組織，他們將會遺失存取 tootheir 帳戶 hello 應用程式正在使用中。
* 記錄哪些資料與哪些應用程式共用是件好事。  資料比以往更容易進行傳輸，且清楚記錄哪些人員與哪些應用程式共用哪些資料會很有用。
* 使用 Azure AD 的 oAuth 應用程式決定完全權限，使用者可以 toogrant tooapplications 而哪些權限需要以系統管理員 tooagree。  您應該很指出只有系統管理員可以同意 toolarger 範圍和更重要的權限。
* 加入並讓其資料是應用程式 tooaccess 稽核事件，讓您可以檢視內 hello Azure Managment 入口 toodetermine hello 稽核報告的使用者應用程式新增的方式 toohello 目錄。

**注意：** *Microsoft 本身已運作，現在有許多個月使用 hello 預設組態。*

與所有作業，稱為很可能 tooprevent 您目錄中使用者加入應用程式和執行自行決定對他們與應用程式中藉由修改 hello Azure 管理入口網站中的目錄設定共用哪些資訊。  hello 下列設定可存取您目錄中的 「 設定 」 索引標籤上的 hello Azure 管理入口網站中。

![Hello UI 來設定整合式應用程式設定的螢幕擷取畫面][app_settings]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>後續步驟
深入了解如何 tooadd 應用程式 tooAzure AD 與 tooconfigure 如何服務應用程式。

* 開發人員：[深入了解如何 toointegrate aad 應用程式](https://msdn.microsoft.com/library/azure/dn151122.aspx)
* 開發人員：[檢閱在 GitHub 上與 Azure Active Directory 整合的應用程式範例程式碼](https://github.com/AzureADSamples)
* 開發人員和 IT 專業人員：[檢閱 hello hello Azure Active Directory Graph API 的 REST API 文件集](https://msdn.microsoft.com/library/azure/hh974478.aspx)
* IT 專業人員：[深入了解如何 toouse Azure Active Directory 預先整合應用程式從 hello 應用程式庫](https://msdn.microsoft.com/library/azure/dn308590.aspx)
* IT 專業人員： [尋找設定特定預先整合應用程式的教學課程](https://msdn.microsoft.com/library/azure/dn893637.aspx)
* IT 專業人員：[深入了解如何使用應用程式的 toopublish hello Azure Active Directory 應用程式 Proxy](https://msdn.microsoft.com/library/azure/dn768219.aspx)

## <a name="see-also"></a>另請參閱
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](../active-directory-apps-index.md)

<!--Image references-->
[apps_service_principals_directory]:../media/active-directory-how-applications-are-added/HowAppsAreAddedToAAD.jpg
[app_settings]:../media/active-directory-how-applications-are-added/IntegratedAppSettings.jpg
