---
title: "aaaGet 啟動 Azure AD 整合與應用程式 |Microsoft 文件"
description: "本文章是整合 Azure Active Directory (AD) 與在內部部署應用程式和雲端應用程式的入門指南。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: db6d210d-c970-49e9-bd20-36d984bcd1c3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 5a7a851e8418083fee72ab58477a9cab75d0d4bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-active-directory-with-applications-getting-started-guide"></a>整合 Azure Active Directory 與應用程式入門指南
## <a name="overview"></a>概觀
本主題是預定的 toogive 您與 Azure Active Directory (AD) 整合應用程式的藍圖。 每個 hello 的以下各節包含更詳細主題的簡短摘要，以便識別這個使用者入門指南的哪些部分是相關 tooyou。  按照每個主體 hello 連結以取得深入剖析。

## <a name="before-you-begin-take-inventory"></a>在開始之前，請取得清查
您跳 toointegrating 應用程式與 Azure AD 中之前，您和您想要 toogo 是重要的 tooknow。  hello 下列問題會預期的 toohelp 想像您 Azure AD 應用程式整合專案。

### <a name="application-inventory"></a>應用程式清查
* 您所有應用程式的所在位置？ 擁有者為？
* 您的應用程式需要何種驗證？
* 需要哪些人存取 toowhich 應用程式？
* 您想 toodeploy 新的應用程式嗎？
  * 您將在公司內部建立並將它部署在 Azure 計算執行個體？
  * 您可以使用其中所提供之 hello Azure 應用程式庫？

### <a name="user-and-group-inventory"></a>使用者和群組清查
* 您的使用者帳戶所在的位置？
  * 內部部署 Active Directory
  * Azure AD
  * 您擁有在個別的應用程式資料庫中
  * 在未經約束的應用程式中
  * 所有上述 hello
* 個別使用者目前有哪些權限和角色指派？ 您需要 tooreview 其存取權或您確定您的使用者存取和角色指派是適當現在嗎？
* 是否已經在您的內部部署 Active Directory 中建立群組？
  * 您的群組的組織方式？
  * Hello 群組成員是誰？
  * 哪些權限/角色指派 hello 群組目前有？
* 您將會整合之前需要 tooclean 使用者/群組的資料庫嗎？  (這是很重要的問題。 垃圾進，垃圾出 - 應當避免無用資料。)

### <a name="access-management-inventory"></a>存取管理清查
* 您如何目前管理使用者存取 tooapplications？ 所需要 toochange 嗎？  您是否有考慮其他方式 toomanage 存取，例如與[RBAC](role-based-access-control-configure.md)例如？
* 需要哪些人存取 toowhat？

或許您沒有 hello 的這些問題的答案 tooall 最前面位置，但是沒關係。  本指南可協助您回答其中一些問題，並做出一些明智的決策。

## <a name="prerequisites"></a>必要條件
* 一個 Azure 訂用帳戶，以及一個 Azure Active Directory 目錄。  如果您尚沒有 Azure 訂用帳戶，可以免費試用 Azure 30 天。 [立即試用！](https://azure.microsoft.com/trial/get-started-active-directory/)

## <a name="application-integration-with-azure-ad"></a>與 Azure AD 的應用程式整合
### <a name="finding-unsanctioned-cloud-applications-with-cloud-app-discovery"></a>使用 Cloud App Discovery 尋找未經約束的雲端應用程式
如上所述，可能有應用程式到目前為止仍未受到組織的管理。  Hello 清查程序的一部分，很可能 toofind 未經批准雲端應用程式。 請參閱 [使用 Cloud App Discovery 尋找未經約束的雲端應用程式](active-directory-cloudappdiscovery-whatis.md)。

### <a name="authentication-types"></a>驗證類型
每個應用程式可能有不同的驗證需求。 利用 Azure AD，可將簽署憑證用於使用 SAML 2.0、WS-同盟或 OpenID Connect 通訊協定，以及密碼單一登入的應用程式。 如需要與 Azure AD 搭配使用的應用程式驗證類型的詳細資訊，請參閱[在 Azure Active Directory 中管理同盟單一登入的憑證](active-directory-sso-certs.md)和[密碼式單一登入](active-directory-appssoaccess-whatis.md)。

### <a name="enabling-sso-with-azure-ad-app-proxy"></a>使用 Azure AD 應用程式 Proxy 啟用 SSO
與 Microsoft Azure AD 應用程式 Proxy，您可以提供存取 tooapplications 位於您私人網路安全地從任何地方和任何裝置上。 在您的環境中安裝應用程式 Proxy 連接器之後，可以輕鬆地使用 Azure AD 來加以設定。

### <a name="integrating-applications-with-azure-ad"></a>整合應用程式與 Azure AD
hello 下列文章中討論的 hello 不同方式的應用程式整合與 Azure AD，並提供一些指引。

* [判斷哪一個 Active Directory toouse](active-directory-administer.md)
* [在 hello Azure 應用程式庫中使用應用程式](active-directory-appssoaccess-whatis.md)
* [整合 SaaS 應用程式教學課程清單](active-directory-saas-tutorial-list.md)

## <a name="managing-access-tooapplications"></a>管理存取 tooapplications
hello 下列文章說明已整合 Azure AD 連接器，使用 Azure AD 與 Azure AD 之後，您可以管理存取 tooapplications 的方式。

* [使用 Azure AD 的管理存取 tooapps](active-directory-managing-access-to-apps.md)
* [使用 Azure AD 連接器自動化](active-directory-saas-app-provisioning.md)
* [將使用者指派 tooan 應用程式](active-directory-applications-guiding-developers-assigning-users.md)
* [將群組指派 tooan 應用程式](active-directory-applications-guiding-developers-assigning-groups.md)
* [共用帳戶](active-directory-sharing-accounts.md)

## <a name="integrating-custom-applications"></a>整合自訂應用程式
如果您要撰寫新的應用程式，而且想 tooassist 開發人員運用 hello 電源 Azure AD，請參閱[Guiding 開發人員](active-directory-applications-guiding-developers-for-lob-applications.md)。

如果您想 tooadd 您自訂的應用程式 toohello Azure 應用程式庫，請參閱[「 攜帶您自己的應用程式 」 使用自助 Azure AD SAML 組態](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)。

## <a name="see-also"></a>另請參閱
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)

