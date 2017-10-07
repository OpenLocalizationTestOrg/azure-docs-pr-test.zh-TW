---
title: "aaaCompare B2B 共同作業和在 Azure Active Directory B2C |Microsoft 文件"
description: "Hello Azure Active Directory B2B 共同作業和 Azure AD B2C 之間的差異為何？"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 34d88b9a7d023e077568e8df3d5e1610ae05b361
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="compare-b2b-collaboration-and-b2c-in-azure-active-directory"></a>比較 Azure Active Directory 的 B2B 共同作業和 B2C

Azure Active Directory (Azure AD) B2B 共同作業和 Azure AD B2C 可讓您與外部使用者 toowork 在 Azure AD 中。 但它們究竟差在哪兒？


B2B 共同作業 |     Azure AD B2C 獨立供應項目
-------- | --------
適用於： 想要從夥伴組織，不論身分識別提供者的 toobe 無法 tooauthenticate 使用者的組織。 | 適用於︰邀請您的行動和 Web 應用程式的客戶 (無論是個人、機構或組織客戶) 加入您的 Azure AD。
支援的身分識別︰本機有工作或學校帳戶的員工、本機有工作或學校帳戶的合作夥伴、或任何電子郵件地址。 推出 toosupport 直接聯盟。  | 支援的身分識別︰具有本機應用程式帳戶的取用者使用者 (任何電子郵件地址或使用者名稱) 或任何以直接聯盟支援的社交身分識別。
中有哪些目錄 hello 合作夥伴使用者： hello 外部組織的使用者中受管理的夥伴特別 hello 與員工，但註解式相同的目錄。 它們可以受到管理 hello 相同方式成為員工，可以是相同的群組加入的 toohello 等等  | 中有哪些目錄 hello 客戶使用者實體： hello 應用程式目錄中。 分開管理 hello 組織的員工和合作夥伴目錄 （如果有的話。
單一登入 (SSO) tooall Azure AD 連接應用程式的支援。 例如，您可以提供存取 tooOffice 365 或內部部署應用程式，而且 tooother SaaS 應用程式，例如 Salesforce 或工作日。  |  SSO toocustomer 擁有 hello Azure AD B2C 租用戶內的應用程式都支援。 SSO tooOffice 365 或 tooother Microsoft 和非 Microsoft SaaS 應用程式不支援。
夥伴生命週期： hello 主機/邀請組織所管理。  | 客戶生命週期： 自助式或由 hello 應用程式管理。
安全性原則與相容性： hello 主機/邀請組織所管理。  | 安全性原則與相容性： hello 應用程式管理。
商標︰使用主控/邀請組織的品牌。  |    商標︰由應用程式管理。 通常會 toobe 產品品牌，與 hello 組織淡出到 hello 背景。
其他資訊：[部落格文章](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/)、[文件](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)  | 其他資訊：[產品頁面](https://azure.microsoft.com/en-us/services/active-directory-b2c/)、[文件](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)


### <a name="next-steps"></a>後續步驟

請瀏覽有關 Azure AD B2B 共同作業的其他文章：

* [何謂 Azure AD B2B 共同作業？](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B 共同作業使用者屬性](active-directory-b2b-user-properties.md)
* [新增 B2B 共同作業使用者 tooa 角色](active-directory-b2b-add-guest-to-role.md)
* [委派 B2B 共同作業邀請](active-directory-b2b-delegate-invitations.md)
* [動態群組和 B2B 共同作業](active-directory-b2b-dynamic-groups.md)
* [設定適用於 B2B 共同作業的 SaaS 應用程式](active-directory-b2b-configure-saas-apps.md)
* [B2B 共同作業使用者權杖](active-directory-b2b-user-token.md)
* [B2B 共同作業使用者宣告對應](active-directory-b2b-claims-mapping.md)
* [Office 365 外部共用](active-directory-b2b-o365-external-user.md)
* [B2B 共同作業目前的限制](active-directory-b2b-current-limitations.md)
* [取得 B2B 共同作業的支援](active-directory-b2b-support.md)
