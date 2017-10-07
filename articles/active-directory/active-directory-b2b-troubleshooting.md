---
title: "Azure Active Directory B2B 共同作業 aaaTroubleshooting |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業常見問題的補救方式"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a>針對 Azure Active Directory B2B 共同作業問題進行疑難排解

以下是 Azure Active Directory (Azure AD) B2B 共同作業常見問題的補救方式。


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a>我已新增外部使用者，但沒有看到這些全域通訊錄或 hello 人員選擇器中

在其中外部使用者不會填入 hello 清單中的情況下，hello 物件可能需要幾分鐘的時間 tooreplicate。

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a>B2B 來賓使用者不會顯示在 SharePoint Online/OneDrive 人員選擇器中 
 
hello 能力 toosearch hello SharePoint Online (SPO) 的人員選擇器中的現有 guest 使用者的預設 toomatch 舊版行為，是 OFF。

您可以使用在 hello 租用戶和網站集合層級設定 'ShowPeoplePickerSuggestionsForGuestUsers' hello 啟用這項功能。 您可以設定使用 hello 組 SPOTenant 和集 SPOSite cmdlet，讓成員 hello 功能 toosearch hello 目錄中的所有現有來賓使用者。 Hello 租用戶範圍中的變更不會影響已佈建的 SPO 站台。

## <a name="invitations-have-been-disabled-for-directory"></a>已針對目錄停用邀請

如果您沒有 tooinvite 使用者權限，您會收到通知，請確認您的使用者帳戶是在使用者設定的授權的 tooinvite 外部使用者：

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

如果您最近有修改這些設定，或指派的 hello 來賓邀請者角色 tooa 使用者，可能有 15-60 分鐘的延遲之後 hello 變更才能生效。

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a>我受邀的 hello 使用者兌換期間收到錯誤訊息

常見錯誤包括：

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a>受邀者的管理員不允許在其租用戶中建立 EmailVerified 使用者

當邀請的使用者的組織使用 Azure Active Directory，但其中 hello 特定的使用者帳戶不存在 （例如，hello 使用者不存在於 Azure AD contoso.com）。 contoso.com 的 hello 系統管理員可能已有原則防止使用者建立。 hello 使用者必須檢查其管理員 toodetermine 與中，如果允許外部使用者。 hello 外部使用者的系統管理員可能需要其網域中的 tooallow 電子郵件驗證使用者 (請參閱此[文章](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)上允許電子郵件驗證的使用者)。

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a>外部使用者不存在於同盟網域中

如果您使用同盟驗證 hello 使用者還沒有 Azure Active Directory 中，不得受邀 hello 使用者。

這個問題，請 hello tooresolve 外部使用者的系統管理員必須進行 hello 使用者帳戶 tooAzure Active Directory 同步處理。

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a>‘\#’ (通常是無效的字元) 如何與 Azure AD 同步？

「\#」 是 Azure AD B2B 共同作業或外部的使用者 Upn 中的保留的字元，因為 hello 受邀帳戶user@contoso.com變成 user_contoso.com#EXT@fabrikam.onmicrosoft.com。因此，\#中來自內部部署 Upn 中不允許有 toosign toohello Azure 入口網站。 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a>新增外部使用者 tooa 同步處理群組時，我會收到的錯誤

外部使用者可以加入只太 「 指派 」 或者 「 安全性 」 群組和不屬於 toogroups 主控內部部署。

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a>我的外部使用者未收到電子郵件 tooredeem

hello 受邀者應洽詢其 ISP 或 hello 下列位址的垃圾郵件篩選器 tooensure 允許：Invites@microsoft.com

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a>我發現該 hello 自訂訊息並不會隨附於邀請訊息有時

使用的隱私權法律 toocomply，我們的 Api，未包含的自訂訊息中的 hello 電子郵件邀請時：

- hello 邀請者不在 hello 邀請租用戶的電子郵件地址
- 當應用程式服務主體傳送嗨邀請

如果重要 tooyou 這種情況下，您可以隱藏 API 邀請電子郵件，並透過您所選擇的 hello 電子郵件機制傳送。 請參閱您的組織法律顧問 toomake 確定任何電子郵件傳送這種方式也符合隱私權法律。

## <a name="next-steps"></a>後續步驟

請瀏覽有關 Azure AD B2B 共同作業的其他文章：

* [何謂 Azure AD B2B 共同作業？](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？](active-directory-b2b-admin-add-users.md)
* [資訊工作者如何新增 B2B 共同作業使用者？](active-directory-b2b-iw-add-users.md)
* [hello hello B2B 共同作業邀請電子郵件項目](active-directory-b2b-invitation-email.md)
* [B2B 共同作業邀請兌換](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B 共同作業授權](active-directory-b2b-licensing.md)
* [Azure Active Directory B2B 共同作業常見問題 (FAQ)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B 共同作業 API 和自訂](active-directory-b2b-api.md)
* [適用於 B2B 共同作業使用者的多重要素驗證](active-directory-b2b-mfa-instructions.md)
* [在沒有邀請的情況下新增 B2B 共同作業使用者](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory 中應用程式管理的文章索引](active-directory-apps-index.md)
