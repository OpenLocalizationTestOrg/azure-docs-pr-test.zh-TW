---
title: "Azure AD 的 aaaDevelop 應用程式 |Microsoft 文件 '"
description: "這篇文章針對 hello IT 專業人員所撰寫，與 Active Directory 整合 Azure 應用程式提供指導方針。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a>開發適用於 Azure Active Directory 的企業營運應用程式
本指南提供的開發特定業務 (LoB) 應用程式的 Azure Active Directory (AD).hello 概觀主要適用對象是 Active Directory/Office 365 全域管理員。

## <a name="overview"></a>概觀
建置整合 Azure AD 的應用程式，可讓您組織的使用者使用 Office 365 單一登入。 Azure AD 可讓您控制 hello hello 應用程式的驗證原則中都有 hello 應用程式。 深入了解條件式存取並 tooprotect 應用程式與多重要素驗證 (MFA) 如何查看 toolearn[設定存取規則](active-directory-conditional-access-azuread-connected-apps.md)。

註冊您的應用程式 toouse Azure Active Directory。 註冊 hello 應用程式時，表示您的開發人員可以使用 Azure AD tooauthenticate 使用者，並要求存取 toouser 資源，例如電子郵件、 行事曆及文件。

您目錄的任何成員 (不是來賓) 都可以註冊應用程式，亦稱為 *建立應用程式物件*。

登錄應用程式可讓任何使用者 toodo hello 下列：

* 取得 Azure AD 識別的應用程式的身分識別
* 取得一個或多個密碼/金鑰 hello 應用程式可以使用本身 tooauthenticate tooAD
* 在 hello Azure 入口網站的自訂名稱、 標誌等品牌 hello 應用程式。
* 適用於 Azure AD 授權功能 tootheir 應用程式，包括：

  * 角色型存取控制 (RBAC)
  * 為 oAuth 授權伺服器的 azure Active Directory （安全 hello 應用程式所公開的 API）
* 宣告所需的權限所需的 hello 應用程式 toofunction，如預期般，包括：

      - 應用程式權限 (僅限全域系統管理員)。 例如： 角色成員資格，在另一個 Azure AD 應用程式或角色成員資格相對 tooan Azure 資源，資源群組或訂用帳戶
      - 委派的權限 (任何使用者)。 例如：Azure AD、登入及讀取設定檔

> [!NOTE]
> 根據預設，任何成員都可以註冊應用程式。 如何 toorestrict 使用權限註冊應用程式 toospecific 成員，請參閱的 toolearn[應用程式如何加入 tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance)。
>
>

以下是您，hello 全域管理員，需要 toodo toohelp 開發人員透過他們的應用程式準備好實際執行：

* 設定存取規則 (存取原則/MFA)
* 設定 hello 應用程式 toorequire 使用者指派，並將使用者指派
* 隱藏 hello 預設使用者同意經驗

## <a name="configure-access-rules"></a>設定存取規則
設定每個應用程式的存取規則 tooyour SaaS 應用程式。 例如，您可以要求使用 MFA，或只允許存取 toousers 受信任的網路。 hello 文件中的 hello 詳細資料，這可用[設定存取規則](active-directory-conditional-access-azuread-connected-apps.md)。

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a>設定 hello 應用程式 toorequire 使用者指派，並將使用者指派
根據預設，使用者不須獲得指派，即可存取應用程式。 不過，如果 hello 應用程式公開的角色，或您想要將應用程式 tooappear hello 使用者的存取面板上，您應該要求使用者指派。

[要求使用者指派](active-directory-applications-guiding-developers-requiring-user-assignment.md)

如果您是 Azure AD Premium 或 Enterprise Mobility Suite (EMS) 的訂閱者，則強烈建議使用群組。 將群組指派 toohello 應用程式可讓您 toodelegate 持續存取管理 toohello 群組的擁有者 hello。 您可以建立 hello 群組，或要求使用群組管理設備組織 toocreate hello 群組中的 hello 負責合作對象。

[將使用者指派 tooan 應用程式](active-directory-applications-guiding-developers-assigning-users.md)  
[將群組指派 tooan 應用程式](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a>隱藏使用者同意
根據預設，每個使用者經歷了同意體驗 toosign 中。 hello 同意體驗，詢問使用者 toogrant 權限 tooan 應用程式，可以是令人不安的使用者不熟悉這類的決策。

對於您信任的應用程式，您可以簡化 hello 使用者體驗同意 toohello 應用程式代表您的組織。

如需有關使用者同意和 hello 同意體驗 Azure 中，請參閱[整合應用程式與 Azure Active Directory](active-directory-integrating-applications.md)。

## <a name="related-articles"></a>相關文章
* [啟用安全的遠端存取 tooon 內部部署應用程式與 Azure AD Application Proxy](active-directory-application-proxy-get-started.md)
* [SaaS 應用程式的 Azure 條件式存取預覽](active-directory-conditional-access-azuread-connected-apps.md)
* [管理與 Azure AD 存取 tooapps](active-directory-managing-access-to-apps.md)
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
