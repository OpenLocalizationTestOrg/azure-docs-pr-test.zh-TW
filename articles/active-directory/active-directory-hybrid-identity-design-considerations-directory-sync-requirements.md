---
title: "aaaAzure Active Directory 混合式身分識別設計考量-判斷目錄同步處理需求 |Microsoft 文件"
description: "識別哪些需求所需的同步處理之間的所有 hello 使用者在 = 內部部署與雲端 hello 企業版。"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 593eaa71-17eb-4c16-8c98-43cc62987e65
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6646e3792c65f37c3d62eecdb6c6f3bd257f04f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="determine-directory-synchronization-requirements"></a>判斷目錄同步處理需求
同步處理就是要為使用者提供其內部部署識別基礎 hello 雲端中的身分識別。 它們會使用同步的帳戶進行驗證或同盟的驗證，hello 使用者仍需要 toohave hello 雲端中的身分識別。  這個識別會需要 toobe 維護而定期更新。  hello 更新可以有許多形式，標題變更 toopassword 的變更。  

請先評估 hello 組織在內部部署身分識別方案及使用者需求。 這項評估是重要 toodefine hello 技術的需求會如何建立和維護 hello 雲端中使用者身分識別。  對於大多數的組織，Active Directory 內部部署且將會透過將使用者的 hello 在內部部署目錄同步處理從，不過在某些情況下就會無法 hello 案例。  

請確定 tooanswer hello 下列問題：

* 您擁有一或多個 AD 樹系，或者完全沒有嗎？
  
  * 您要進行同步處理的 Azure AD 目錄有多少個？
    
    1. 您會使用篩選嗎？
    2. 您是否規劃了多部 Azure AD Connect 伺服器？
* 您目前沒有內部部署的同步處理工具嗎？
  
  * 如果是，您的使用者是否具有虛擬目錄/身分識別整合？
* 您是否有任何其他目錄內部的 toosynchronize （例如 LDAP 目錄，HR 資料庫等等）？
  * 您會執行任何 GALSync toobe 嗎？
  * Hello 目前狀態的 upn，請在您的組織為何？ 
  * 您擁有使用者要對其進行驗證的其他目錄嗎？
  * 貴公司是否使用 Microsoft Exchange？
    * 他們是否規劃擁有混合式交換部署？

既然您已了解關於同步處理要求時，您需要哪一種工具是 hello 正確一個 toomeet toodetermine 這些需求。  Microsoft 提供數個工具 tooaccomplish 目錄整合及同步處理。  請參閱 hello[混合式身分識別目錄整合工具比較資料表](active-directory-hybrid-identity-design-considerations-tools-comparison.md)如需詳細資訊。 

您已經有您的同步處理需求及 hello 工具，將會完成這項作業為您的公司，您需要使用這些目錄服務的 tooevaluate hello 應用程式。 這項評估是重要 toodefine hello 技術需求 toointegrate 這些應用程式 toohello 雲端。 請確定 tooanswer hello 下列問題：

* 這些應用程式將會移動的 toohello 雲端，然後使用 hello 目錄嗎？
* 是否有特殊的屬性，這些應用程式可以成功地使用需要同步處理的 toobe toohello 雲端？
* 將這些應用程式需要 toobe 重寫 tootake 利用雲端驗證？
* 將這些應用程式繼續 toolive 在內部部署使用者進行存取時使用 hello 雲端識別身分嗎？

您也需要 toodetermine hello 安全性需求和限制目錄同步作業。 這項評估是重要 tooget hello 需求，將會需要順序 toocreate 和維護 hello 雲端中的使用者身分識別的清單。 請確定 tooanswer hello 下列問題：

* 會 hello 同步伺服器是所在？
* 它將會加入網域嗎？
* 將在防火牆後面，例如 DMZ 在受限網路上找到 hello 伺服器嗎？
  * 您將無法 tooopen hello 需要防火牆連接埠 toosupport 同步處理？
* 您有 hello 同步處理伺服器的災害復原計劃嗎？
* 您有適用於所有樹系，您想要使用 toosynch hello 正確的權限的帳戶嗎？
  * 如果您的公司不知道 hello 解答這個問題，請檢閱 hello 文章中的 hello 節 < 密碼同步化的權限 >[安裝 hello Azure Active Directory 同步處理服務](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService)並判斷是否已經有與這些權限的帳戶，或如果您需要一個 toocreate。
* 如果您有多重樹系同步處理是 hello 同步伺服器可以 tooget tooeach 樹系？

> [!NOTE]
> 請確定每個答案 tootake 附註，並了解 hello 回應 hello 背後的基本原理。 [判斷事件回應需求](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)將介紹可用 hello 選項。 回答這些問題之後，您就能選取最適合業務需求的選項。
> 
> 

## <a name="next-steps"></a>後續步驟
[判斷多重要素驗證需求](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a>另請參閱
[設計考量概觀](active-directory-hybrid-identity-design-considerations-overview.md)

