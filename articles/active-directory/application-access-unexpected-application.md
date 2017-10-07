---
title: "我的應用程式清單中的 aaaUnexpected 應用程式 |Microsoft 文件"
description: "如何 toosee 租用戶中的所有應用程式，並了解應用程式如何出現在所有應用程式清單中，在企業應用程式"
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
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a>我的應用程式清單中有未預期的應用程式

本文將協助您 toounderstand 應用程式出現在您**所有應用程式**清單下**企業應用程式**。 

## <a name="how-toosee-all-applications-in-your-tenant"></a>如何 toosee 租用戶中的所有應用程式

toosee 所有 hello 租用戶中的應用程式，您需要 toouse hello**篩選**控制 tooshow**所有應用程式**下 hello**所有應用程式**清單。 toodo，後續 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

6.  按一下 hello 使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**。

7.  在 hello**篩選**刀鋒視窗中，設定 hello**顯示**太選項**所有應用程式。**

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a>特定應用程式為何出現在我的所有應用程式清單中？

當篩選太**所有應用程式**，hello**所有應用程式****清單**顯示租用戶中的每個服務主體物件。 服務主體物件可能以各種方式出現在此清單中︰

1.  當您從 hello 應用程式庫，新增任何應用程式時，包括：

   1. **Azure AD 資源庫應用程式** – 與 Azure AD 預先整合以啟用單一登入的應用程式。

   2. **應用程式 Proxy 應用程式**– 您想 tooprovide 安全單一登入 tooexternally 在內部部署環境中執行的應用程式。

   3. **自訂開發的應用程式**– 的應用程式，您的組織希望 toodevelop 上 hello Azure AD 應用程式開發平台，但所可能尚不存在。

   4. **不在資源庫內的應用程式** – 引進您自己的應用程式！ 您想，任何網頁連結或呈現使用者名稱和密碼欄位中，任何應用程式支援 SAML 或 OpenID Connect 通訊協定，或支援您想進行單一登入 Azure AD 與 toointegrate SCIM。

2.  註冊或登入與 Azure Active Directory 整合的第三方<sup></sup>應用程式時。 例如，[Smartsheet](https://app.smartsheet.com/b/home) 或 [DocuSign](https://www.docusign.net/member/MemberLogin.aspx)。

3.  當註冊，或新增授權 tooa 使用者或群組 tooa 第一個合作對象應用程式，就像[Microsoft Office 365](http://products.office.com/)。

4.  當您新增新的應用程式註冊藉由建立自訂開發的應用程式使用 hello [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration)。

5.  當您新增新的應用程式註冊藉由建立自訂開發的應用程式使用 hello [V2.0 應用程式註冊入口網站](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal)。

6.  當您新增您使用 Visual Studio 的 [ASP.net 驗證方法](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions)或[已連線服務](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)所開發的應用程式時。

7.  當您建立服務主體物件，使用 hello [Azure AD PowerShell 模組](/powershell/azure/install-adv2?view=azureadps-2.0)。

8.  當您[tooan 應用程式的同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)為您的租用戶系統管理員 toouse 資料。

9.  當[tooan 應用程式取得使用者同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)toouse 租用戶中的資料。

10. 當您啟用的某些服務會在您的租用戶中儲存資料時。 重設密碼，這建立模型的一個範例是以服務主體的 toostore 密碼重設原則安全的方式。

tooget 更多詳細資料上的應用程式如何加入 tooyour 目錄讀取[如何及為何將應用程式加入 tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added)。

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a>我想 tooremove 在特定的使用者或群組的指派 tooan 應用程式

tooremove 的使用者或群組指派 tooan 應用程式，請遵循 hello 中所列的 hello 步驟[移除企業應用程式在 Azure Active Directory 中的使用者或群組指派](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal)發行項。

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a>我想 toodisable 針對每個使用者的所有存取 tooan 應用程式

toodisable 所有使用者登入 tooan 應用程式，所列出的 hello 後續 hello 步驟[停用使用者登入企業應用程式在 Azure Active Directory 的](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal)發行項。

## <a name="i-want-toodelete-an-application-entirely"></a>我想完全 toodelete 應用程式

太**刪除應用程式**，請遵循下列指示 hello:

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想要 toodelete hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 **刪除**hello 最上層應用程式的圖示**概觀**刀鋒視窗。

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a>我想 toodisable 所有未來的使用者同意作業 tooany 應用程式

針對整個目錄防止終端使用者同意 tooany 應用程式，請停用使用者同意。 系統管理員仍然可以代表使用者行使同意。 同意 toolearn 進一步了解應用程式，以及為什麼您可能會或可能不希望 toodo，讀取[了解使用者和系統管理員同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)。

太**停用整個目錄中的所有未來的使用者同意作業**，請遵循下列指示 hello:

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [使用者設定]。

6.  停用所有未來的使用者同意作業設定 hello**使用者可以允許其資料應用程式 tooaccess**太切換**否**按一下 hello**儲存** 按鈕。

## <a name="next-steps"></a>後續步驟
[使用 Azure Active Directory 管理應用程式](active-directory-enable-sso-scenario.md)
