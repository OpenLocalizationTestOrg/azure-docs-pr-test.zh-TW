---
title: "aaaAzure Active Directory 混合式身分識別設計考量-決定存取控制需求 |Microsoft 文件"
description: "涵蓋 hello 識別及資源的混合式環境中的使用者識別的存取需求的功能。"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e3b3b984-0d15-4654-93be-a396324b9f5e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: f0c22629f732a4c13ee7a24456651bec7637c387
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a>判斷混合式身分識別解決方案的存取控制需求
他們也可以使用這個機會 tooreview 其混合式身分識別解決方案設計的組織時存取這些計劃 toomake hello 資源的需求適用於使用者它。 hello 資料存取跨所有的四大身分識別，也就是：

* 系統管理
* 驗證
* Authorization
* 稽核

遵循的 hello 各節將說明如何驗證和授權的詳細資訊，管理和稽核 hello 混合式身分識別生命週期的一部分。 如需這些功能的詳細資訊，請參閱 [判斷混合式身分識別管理工作](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) 。

> [!NOTE]
> 讀取[hello 四個核心的身分識別-hello 的混合式 IT 中的身分識別管理](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx)如需每個這些功能的詳細資訊。
> 
> 

## <a name="authentication-and-authorization"></a>驗證和授權
有不同的案例進行驗證和授權，這些案例會有必須滿足於 hello 公司是進行 tooadopt hello 混合式身分識別解決方案的特定需求。 案例涉及商務 tooBusiness (B2B) 通訊可以加入其他的挑戰 IT 系統管理員因為他們仍須先 tooensure hello 組織所使用的 hello 驗證和授權方法能夠與其商務合作夥伴進行通訊。 在 hello 設計驗證和授權需求的程序，請確定會回答下列問題的 hello:

* 您的組織只會驗證和授權位於其身分識別管理系統中的使用者嗎？
  * 是否有任何適用於 B2B 案例的方案？
  * 如果是，您已經知道哪些通訊協定 （SAML、 OAuth、 Kerberos、 語彙基元或憑證） 將會使用的 tooconnect 這兩個企業嗎？
* 您即將 tooadopt hello 混合式身分識別解決方案是否支援這些通訊協定？

另一個重要的點 tooconsider 是即將放置 hello 驗證儲存機制，供使用者和合作夥伴和 hello 系統管理模型 toobe 使用。 請考慮下列兩個核心選項 hello:

* 集中式： 在此模型 hello 中使用者的認證、 原則和管理可集中於內部或 hello 雲端中。
* 混合式： 在此模型 hello 使用者的認證、 原則和管理會集中於內部，而且複寫 hello 雲端中。

您的組織將採用哪一個模型而異相應 tootheir 商務需求，要遵循問題 tooidentify hello 身分識別管理系統將會位於而 hello 系統管理模式 toouse tooanswer hello:

* 您的組織目前具有內部部署的身分識別管理嗎？
  * 如果是，是否在計劃 tookeep 它？
  * 是否有任何法規或規範需求，您的組織必須遵循該指定應放 hello 身分識別管理系統？
* 沒有您的組織使用單一登入應用程式位於內部部署或 hello 雲端中嗎？
  * 如果是，並使用混合式身分識別模型的 hello 採用會影響此程序？

## <a name="access-control"></a>存取控制
雖然驗證和授權的核心項目 tooenable 存取 toocorporate 資料透過使用者的驗證，也很重要的 toocontrol hello 的這些使用者將擁有而且 hello 層級的存取 」 系統管理員必須透過 hello 存取層級他們所管理的資源。 您的混合式身分識別解決方案必須能夠 tooprovide 細微的存取權 tooresources，委派和以角色為基礎的存取控制。 請確定該 hello 下列問題會回答關於存取控制：

* 您的公司有多個使用者提高權限 toomanage 與身分識別系統嗎？
  * 如果每位使用者是，需要 hello 相同存取層級嗎？
* 將您的公司需要 toodelegate 存取 toousers toomanage 特定的資源嗎？
  * 如果是，這種情況發生的頻率為何？
* 您的公司需要 toointegrate 存取控制功能，在內部部署和雲端之間的資源嗎？
* 您的公司需要 toolimit 存取 tooresources 根據 toosome 條件嗎？
* 您的公司會有任何應用程式需要自訂控制項存取 toosome 資源嗎？
  * 如果是，這些應用程式位置 (在內部部署或雲端 hello)？
  * 如果是，其中是那些目標資源位於 (在內部部署或雲端 hello)？

> [!NOTE]
> 請確定每個答案 tootake 附註，並了解 hello 回應 hello 背後的基本原理。 [定義的資料保護策略](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)將介紹可用 hello 選項以及每個選項的優點/缺點。  回答這些問題，您就能選取最適合您業務需求的選項。
> 
> 

## <a name="next-steps"></a>後續步驟
[判斷事件因應需求](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a>另請參閱
[設計考量概觀](active-directory-hybrid-identity-design-considerations-overview.md)

