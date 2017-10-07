---
title: "aaaAzure Active Directory 混合式身分識別設計考量-判斷事件 rResponse 需求 |Microsoft 文件"
description: "決定監視和報告功能 hello 混合式身分識別解決方案，可以利用 IT tootake 動作 tooidentify 並減輕潛在威脅"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: a3d2a459-599b-4b67-8e51-7369ee25082d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 7084096f318ef461e8331fb6edde1b77d4108466
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="determine-incident-response-requirements-for-your-hybrid-identity-solution"></a>判斷混合式身分識別解決方案的事件回應需求
大型或中型組織最有可能會有[安全性事件回應](https://technet.microsoft.com/library/cc700825.aspx)位置 toohelp IT 在執行動作據以 toohello 層級的事件。 hello 身分識別管理系統是 hello 事件回應程序中的重要元件，因為它可以是使用的 toohelp 識別執行特定動作對 hello 的目標人員。 hello 混合式身分識別解決方案必須能夠 tooprovide 監視和報告功能，可以利用 IT tootake 動作 tooidentify 並降低潛在的威脅。 一般事件回應計劃中，您必須遵循階段 hello 計劃的 hello:

1. 初步評估。
2. 事件傳達的訊息。
3. 損毀控制與風險降低。
4. 識別是否遭到入侵及嚴重性。
5. 保留證據。
6. 通知 tooappropriate 合作對象。
7. 系統修復。
8. 文件。
9. 損毀和成本評估。
10. 修訂程序和計畫。

決定其 hello 識別期間洩露和嚴重性階段，它將會需要 tooidentify hello 系統已遭入侵，已存取，並判斷 hello 區分這些檔案的檔案。 混合式身分識別系統應該能夠 toofulfill 這些需求 tooassist 您識別 hello 使用者做這些變更。 

## <a name="monitoring-and-reporting"></a>監視和報告
也可協助多次 hello 識別系統中初始評估階段主要如果 hello 系統具有內建稽核與報告功能。 在初始評估 hello，IT 系統管理員必須能夠 tooidentify 可疑的活動，或 hello 系統應該能夠 tootrigger 自動根據預先設定的工作。 許多活動可能表示可能的攻擊，但是在其他情況下，設定不良的系統可能會導致 tooa 誤判數目入侵偵測系統中。 

應該協助 IT 系統管理員 」 tooidentify hello 身分識別管理系統，並報告這些可疑的活動。 通常可藉由監視所有系統並具備可強調顯示潛在威脅的報告功能，來滿足這些技術需求。 使用 hello 問題下方 toohelp 設計時考量事件回應需求您混合式身分識別解決方案：

* 貴公司擁有適當的安全性事件回應嗎？
  * 如果是，會 hello 目前身分識別管理系統使用 hello 程序的一部分嗎？
* 您的公司需要 tooidentify 可疑登入嘗試從使用者跨不同裝置嗎？
* 您的公司是否需要 toodetect 潛在盜用的使用者的認證？
* 您的公司是否需要 tooaudit 使用者的存取和動作？
* 當使用者重設其密碼時，貴公司需要 tooknow？

## <a name="policy-enforcement"></a>強制執行原則
在損毀控制項和風險降低階段，請務必 tooquickly 減少受到攻擊的 hello 實際和潛在影響。 此時所採取的動作可讓 hello 次要和主要的一個宣告之間的差異。 hello 確切的反應取決於您的組織和您所面對的 hello 攻擊的 hello 性質。 如果 hello 初始評估結束帳戶已遭到洩露，您將需要 tooenforce 原則 tooblock 此帳戶。 這是一個範例中，將內容運用 hello 身分識別管理系統。 使用以下 toohelp 納入考量原則的會實施 tooreact tooan 進行中的事件時，設計您的混合式身分識別解決方案的 hello 問題：

* 您的公司有原則位置 tooblock 使用者從網路存取 hello 中如有必要？
  * 如果是，不會 hello 目前方案整合 hello 混合式身分識別管理系統，必須進行 tooadopt 嗎？
* 您的公司需要 tooenforce 條件式存取位於隔離的使用者嗎？ 

> [!NOTE]
> 請確定每個答案 tootake 附註，並了解 hello 回應 hello 背後的基本原理。 [定義的資料保護策略](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)將介紹可用 hello 選項以及每個選項的優點/缺點。  回答這些問題之後，您就能選取最適合業務需求的選項。
> 
> 

## <a name="next-steps"></a>後續步驟
[定義資料保護策略](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)

## <a name="see-also"></a>另請參閱
[設計考量概觀](active-directory-hybrid-identity-design-considerations-overview.md)

