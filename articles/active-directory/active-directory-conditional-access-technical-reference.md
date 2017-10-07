---
title: "Active Directory 條件式存取的技術參考 aaaAzure |Microsoft 文件"
description: "條件式存取控制與 Azure Active Directory 檢查 hello 您挑選驗證 hello 使用者時，才能允許存取 toohello 應用程式特定的條件。 一旦符合這些條件，hello 使用者已驗證，而且允許存取 toohello 應用程式。"
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a>Azure Active Directory 條件式存取的技術參考

## <a name="services-enabled-with-conditional-access"></a>已啟用條件式存取功能的服務

各種 Azure AD 應用程式類型都支援「條件式存取」規則。 此清單包括：


* 應用程式註冊以 hello Azure 應用程式 Proxy
* Azure 遠端應用程式
* 已開發並已向 Azure AD 註冊的企業營運及多租用戶應用程式
* Dynamics CRM
* 同盟的應用程式從 hello Azure AD 應用程式庫
* Microsoft Office 365 Yammer
* Microsoft Office 365 Exchange Online
* Microsoft Office 365 SharePoint Online (包括商務用 OneDrive)
* Microsoft Power BI 
* 密碼 SSO 應用程式從 hello Azure AD 應用程式庫
* Visual Studio Team Services
* Microsoft Teams









## <a name="enable-access-rules"></a>啟用存取規則
您可以依據個別應用程式來啟用或停用每個規則。 當規則是**ON**會啟用並強制執行存取 hello 應用程式的使用者。 何時**OFF**它們不會使用並會影響 hello 使用者登入體驗。

## <a name="applying-rules-toospecific-users"></a>套用規則 toospecific 使用者
規則可能會藉由設定為基礎的安全性群組的使用者集合套用的 toospecific**套用到**。 **套用到**可以設定得**所有使用者**或**群組**。 當設定太**所有使用者**hello 規則會套用與應用程式存取 toohello tooany 使用者。 hello**群組**選項可讓特定的安全性以及發佈群組 toobe 選取，將只針對這些群組強制執行規則。

在部署規則時，常會 toofirst 套用一組有限的使用者，試驗群組的成員。 一旦完成 hello 規則套用太**所有使用者**。 這會導致 hello 規則 toobe 強制執行 hello 組織中的所有使用者。

選取群組也可能會豁免原則使用 hello**除了**選項。 這些群組的任何成員即使出現在包含群組中，也不必套用原則。

## <a name="at-work-networks"></a>「工作時」網路
使用"At 工作 」 網路的條件式存取規則仰賴受信任的 IP 位址範圍已在 Azure AD 中設定或使用 「 內部公司網路 」 hello 來自 AD FS 宣告。 這些規則包含：

* 不在工作時需要多重要素驗證
* 不工作時封鎖存取

用於指定「工作時」網路的選項

1. 在 hello 中設定受信任的 IP 位址範圍[多因素驗證設定頁面](../multi-factor-authentication/multi-factor-authentication-whats-next.md)。 條件式存取原則會在每個驗證發行 tooevaluate 要求和語彙基元規則上使用 hello 設定範圍。 
2. 設定 hello corpnet 宣告內的使用方式，這個選項可以搭配使用 AD FS 同盟目錄。 toolearn 深入了解 hello 內部公司網路的宣告，請參閱[Tusted Ip](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)。


## <a name="rules-based-on-application-sensitivity"></a>根據應用程式敏感性的規則
規則是每個允許 hello 高價值的服務 toobe 而不會影響存取 tooother 服務保護的應用程式設定。 可以設定條件式存取規則，在 hello**設定**hello 應用程式 索引標籤。 

目前提供的規則︰

* **需要多重要素驗證**
  
  * 此原則會套用的 toowill 的所有使用者都是必要的 tooauthenticate 透過多重要素驗證至少一次。
* **不在工作時需要多重要素驗證**
  
  * 如果套用此原則，所有使用者都都需要的 toohave 執行多重要素驗證至少一次只要從非工作遠端位置存取 hello 服務。 如果它們從工作 tooremote 位置，就會需要的 tooperform 多重要素驗證時存取 hello 服務。
* **不工作時封鎖存取** 
  
  * 當使用者移動工作 tooa 遠端位置時，請他們即將遭到封鎖時 hello 「 封鎖存取不在工作時 」 原則套用的 toothem。  當他們回到工作位置時，就會再次允許他們存取。

## <a name="related-topics"></a>相關主題
* [保護存取 tooOffice 365 和其他應用程式連接 tooAzure Active Directory](active-directory-conditional-access.md)
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)

