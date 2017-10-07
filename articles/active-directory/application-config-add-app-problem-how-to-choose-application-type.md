---
title: "哪一個應用程式加入應用程式時，請輸入 toouse aaaHow toochoose |Microsoft 文件"
description: "了解支援的 hello 類型，您可以使用 Azure AD 整合的應用程式及其相關的組態選項"
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
ms.openlocfilehash: 46e3672e7f5048b0fa54171f0fc169362c9d5ac6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-which-application-type-toouse-when-adding-an-application"></a>如何新增應用程式時，哪一個應用程式輸入 toouse toochoose

這篇文章可協助您 toounderstand hello 四種主要類型的應用程式，您可以使用 Azure AD 整合：

* 每一項支援的功能
* 您可能選擇哪個應用程式的理由
* 如何 tooconfigure 這些應用程式的核心屬性，例如使用者的方式**佈建**，到底**單一登入**技術 toouse。

## <a name="supported-application-types-in-azure-ad"></a>Azure AD 中支援的應用程式類型

Azure AD 支援四種主要的應用程式類型，您可以使用新增 hello**新增**功能下找到**企業應用程式**。 其中包含：

-   **Azure AD 資源庫應用程式** – 與 Azure AD 預先整合以啟用單一登入的應用程式。

-   **應用程式 Proxy 應用程式**– 您想 tooprovide 安全單一登入 tooexternally 在內部部署環境中執行的應用程式。

-   **自訂開發的應用程式**– 的應用程式，您的組織希望 toodevelop 上 hello Azure AD 應用程式開發平台，但所可能尚不存在。

-   **不在資源庫內的應用程式** – 引進您自己的應用程式！ 您想，任何網頁連結或呈現使用者名稱和密碼欄位中，任何應用程式支援 SAML 或 OpenID Connect 通訊協定，或支援您想進行單一登入 Azure AD 與 toointegrate SCIM。

## <a name="features-and-capabilities-supported-by-all-hello-above-application-types"></a>功能和所有 hello 上方的應用程式類型所支援的功能

hello 支援下列功能是由任何 hello 上方 4 應用程式類型在 Azure AD 中：

-   **快速啟動** – 依照[簡單部署步驟](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)快速開始使用應用程式

-   **一般屬性管理**– 取得[直接深層連結](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users)tooan 應用程式，[自訂商標 hello](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal)應用程式，或[停用 hello 應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal)所有使用者。

-   **使用者和群組管理**–[指派](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)或[移除](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal)使用者和群組的 tooan 應用程式，以及選擇性地指派 hello 特定應用程式角色，而這些使用者和群組具有存取權

-   **自助式應用程式存取**– 啟用使用者 toorequest[自助式應用程式存取](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)tooan 應用程式從其應用程式存取面板藉由直接新增應用程式或[聯結自助服務啟用的群組](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management)，選擇性地需要 business 核准沿著 hello 方法

-   **單一登入**– 請參閱[所有 hello 登入 tooan 應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins)，或您的應用程式

-   **稽核記錄檔**– 請參閱[詳細的稽核記錄檔的修改 tooan 應用程式的相關](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs)，tooall 或您的應用程式

-   **條件式和風險型存取**– 強大設定[條件式存取規則](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)當使用者嘗試 toosign tooa 特定應用程式中的時，會強制執行

-   **權限檢視**– 檢視任何 hello [OAuth2 權限](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)應用程式具有存取 tooin 目錄從單一位置

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>特定應用程式類型所支援的單一登入和佈建模式

hello 下表描述 hello 不同單一登入和佈建 hello 上方的應用程式類型的每個支援的模式。 您可以使用此資料表 toohelp 您 toounderstand 哪一個應用程式需要 tooadd toosupport 特定的目標。

  ![應用程式類型表格](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>如何 toochoose 單一登入模式

支援的 hello**單一登入**以下列出 Azure AD 應用程式模式。

-   **Azure AD 單一登入已停用**– 選擇 Azure AD 單一登入已停用**單一登入模式**您是否尚未準備 toointegrate 搭配單一登入 Azure AD，與此應用程式或只測試它

-   **登入連結**– 選擇 hello[連結登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)**單一登入模式**如果您使用現有單一登入的方案，已連線的應用程式，或者如果您只想toopublish 簡單連結為您的使用者在其[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)或[Office 365 應用程式啟動器](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **密碼型登入**– 選擇 hello[密碼式登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)**單一登入模式**如果您的應用程式呈現 HTML 使用者名稱和密碼欄位，而且您想 toostore，使用者名稱和密碼安全地 toobe 重新執行 toohello 應用程式更新版本

-   **SAML 型登入**– 選擇 hello [SAML 型登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)基礎的單一登入模式，如果您的應用程式支援 hello SAML 或 OpenID Connect 通訊協定，或您要讓 toobe 無法 toomap 使用者 toospecific 應用程式角色在 規則定義在您的 SAML 宣告 *

   >[!NOTE]
   >Hello 應用程式 proxy 已針對應用程式時，不使用此選項。
   >
   >

-   **標頭型登入**– 請選擇此選項[標頭型登入](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad)單一登入模式如果您使用支援 HTTP 標頭的 PingAccess 的應用程式以您想 tooperform 單一登入太的驗證

   >[!NOTE]
   >Hello 應用程式 proxy 與 PingAccess 設定應用程式時，才可用這個選項。
   >
   >

-   **整合式 Windows 驗證**– 選擇 hello[整合式 Windows 驗證](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)單一登入模式公開您希望 tooperform 單一登入太內部 WIA 應用程式時

   >[!NOTE]
   >Hello 應用程式 proxy 設定的應用程式時，才可用這個選項。
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a>自訂開發之應用程式的單一登入模式

您可以透過 hello 開發的自訂應用程式[自訂開發的應用程式](#_Custom-Developed_Applications)經驗也支援其他單一登入模式以上未列出。 其中包含：

-   以 [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) 為基礎的登入

-   以 [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) 為基礎的登入

-   以 [WS-同盟 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) 為基礎的登入

-   以 [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) 為基礎的登入

讀取 hello [Azure Active Directory 開發人員手冊 》](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn 深入了解如何支援這些 toocreate 自訂開發應用程式的單一登入模式。

## <a name="how-tooset-an-applications-single-sign-on-mode"></a>如何 tooset 應用程式的單一登入模式

tooset 應用程式的**單一登入**模式中，遵循下方的 hello 指示：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想 tooconfigure 單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 **單一登入**從 hello 應用程式的左導覽功能表。

## <a name="how-toochoose-a-provisioning-mode"></a>如何 toochoose 佈建模式

-   **手動佈建**– 選擇 hello[手動](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes)佈建模式，如果您有現有的帳戶，或想 toomanage 此應用程式之外的 Azure AD 的帳戶。

-   **自動佈建**– 選擇 hello[自動](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning)**佈建模式**如果您想 tooenable 自動 API 為基礎的佈建及/或取消佈建使用者帳戶 toothis應用程式 

   >[!NOTE]
   >這個選項是僅適用於應用程式內 hello**精選**分類的 hello [Azure AD 應用程式庫](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery)。
   >
   >

-   **SCIM 為基礎的自動佈建**– 使用[SCIM 為基礎的自動佈建](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning)您的應用程式是否支援偵測變更 toousers 和群組，變更會自動發出 hello SCIM 通訊協定tooany 應用程式與 Azure AD 整合 

   >[!NOTE]
   >此選項未列為特定的佈建模式，但對於所有與 Azure AD 整合的應用程式，依預設會啟用。
   >
   >

## <a name="how-tooset-an-applications-provisioning-mode"></a>如何 tooset 應用程式的佈建模式

tooset 應用程式的**佈建**模式中，遵循下方的 hello 指示：

tooset 應用程式的**單一登入**模式中，遵循下方的 hello 指示：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您要為其 tooconfigure 佈建的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 **佈建**從 hello 應用程式的左導覽功能表。

## <a name="next-steps"></a>後續步驟
[使用 Azure Active Directory 管理應用程式](active-directory-enable-sso-scenario.md)
