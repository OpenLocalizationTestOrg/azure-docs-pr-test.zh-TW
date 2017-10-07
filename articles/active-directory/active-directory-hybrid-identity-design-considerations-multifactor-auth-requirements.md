---
title: "aaaAzure Active Directory 混合式身分識別設計考量-判斷多因素驗證需求"
description: "條件式存取控制與 Azure Active Directory 檢查 hello 您挑選驗證 hello 使用者時，才能允許存取 toohello 應用程式特定的條件。 一旦符合這些條件，hello 使用者已驗證，而且允許存取 toohello 應用程式。"
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a>判斷混合式身分識別解決方案的多重要素驗證需求
在行動力，與使用者存取資料和應用程式 hello 定域機組中以及從任何裝置，此世界中保護這項資訊變得重要。  每天都會出現關於安全性漏洞的新標題。  多因素驗證，並針對這類缺口，這不保證，但提供額外一層的安全性 toohelp 防止這些漏洞。
請先評估 hello 組織需求的多因素驗證。 也就是為何 hello 組織嘗試 toosecure。  這項評估是重要的 toodefine hello 技術的需求設定和啟用多因素驗證的 hello 組織使用者。

> [!NOTE]
> 如果您不熟悉 MFA 和其用途，強烈建議您閱讀 hello 文章[什麼是 Azure Multi-factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md)先前 toocontinue 閱讀本節。
> 
> 

請確定 tooanswer hello 下列：

* 您的公司正在 toosecure Microsoft 應用程式嗎？ 
* 這些 app 是如何發佈的？
* 您的公司提供遠端存取 tooallow 員工 tooaccess 在內部部署應用程式嗎？

如果是，何種遠端存取？您也需要的 tooevaluate 即將放置 hello 使用者要存取這些應用程式。 這項評估是另一個重要步驟 toodefine hello 適當的多因素驗證策略。 請確定 tooanswer hello 下列問題：

* Toobe hello 使用者位於何處？
* 他們將無所不在嗎？
* 您的公司是否需要根據 toohello 使用者位置 tooestablish 限制？

一旦您了解這些需求，請務必 tooalso 評估 hello 使用者的需求，進行多因素驗證。 這項評估很重要的因為它會定義 hello 需求推出多因素驗證。 請確定 tooanswer hello 下列問題：

* 熟悉 hello 使用者使用多重要素驗證？
* 將一些用法會需要的 tooprovide 額外的驗證？  
  * 如果是，所有 hello 時來自外部網路或存取特定的應用程式，或在其他情況下時間？
* Hello 使用者需要要求如何訓練 toosetup 和實作多重要素驗證？
* Hello 貴公司想 tooenable 多因素驗證使用者的主要案例是什麼？

之後回應 hello 上述問題，您都無法 toounderstand 是否有已實作多因素驗證內部部署。 這項評估是重要的 toodefine hello 技術的需求設定和啟用多因素驗證的 hello 組織使用者。 請確定 tooanswer hello 下列問題：

* 您的公司是否需要使用 MFA tooprotect 特殊權限帳戶？
* 貴公司是否需要 tooenable MFA 特定應用程式的相容性因素？
* 您的公司需要 tooenable MFA 所有符合資格的使用者，這些應用程式或只有系統管理員嗎？
* 您需要有 MFA 永遠啟用，或只何時 hello 使用者記錄公司網路外？

## <a name="next-steps"></a>後續步驟
[定義混合式身分識別採用策略](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a>另請參閱
[設計考量概觀](active-directory-hybrid-identity-design-considerations-overview.md)

