---
title: "Azure Active Directory 混合式身分識別設計考量 - 判斷資料保護需求 | Microsoft Docs"
description: "在規劃混合式身分識別解決方案時，請識別您企業的資料保護需求，以及有哪些可用選項可充分因應這些需求。"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 40dc4baa-fe82-4ab6-a3e4-f36fa9dcd0df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 96bf9d4c26a22f718c29804c11681199e775f589
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="plan-for-enhancing-data-security-through-strong-identity-solution"></a>透過增強式身分識別解決方案規劃更高的資料安全性
保護資料的第一個步驟，是識別誰可以存取該資料，而在此程序中，您必須要有可與您的系統整合以提供驗證和授權功能的身分識別解決方案。 驗證和授權常被混淆，兩者角色也常被誤解。 這兩者其實是很不一樣的，如下圖所說明：

![](./media/hybrid-id-design-considerations/mobile-devicemgt-lifecycle.png)

**行動裝置管理生命週期階段**

在規劃混合式身分識別解決方案時，您必須了解企業的資料保護需求，以及哪些選項最能因應這些需求。

> [!NOTE]
> 完成資料安全性的規劃後，請檢閱 [判斷多因素驗證需求](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md) ，以確定您有關多因素驗證需求的選項不受您在這一節中所做決策的影響。
> 
> 

## <a name="determine-data-protection-requirements"></a>判斷資料保護需求
在行動裝置時代，大部分的公司都有共同的目標：讓使用者在行動裝置上提高生產力，無論是在內部部署，還是遠端的任何位置。 雖然可能有此共同目標，但有這類需求的公司也會顧慮必須要降低以保護公司資料安全和維護使用者隱私權的威脅數量。 每一家公司在這方面可能會有不同的需求；會隨著公司所屬產業而異的符合性規則，會產生不同的設計決策。 

但無論是何種產業，都有一些安全性層面是必須探索並驗證的，這將在下一節說明。

## <a name="data-protection-paths"></a>資料保護路徑
![](./media/hybrid-id-design-considerations/data-protection-paths.png)

**資料保護路徑**

在上圖中，身分識別元件將是在存取資料之前最先受到驗證的。 不過，這項資料在受到存取期間可能會處於不同的狀態。 此圖表上的每個數字，分別代表資料在某個時間點的所在的路徑。 這些數字的說明如下：

1. 裝置層級的資料保護。
2. 傳輸過程中的資料保護。
3. 在內部部署中待用時的資料保護。
4. 在雲端中待用時的資料保護。

雖然混合式身分識別解決方案並未直接提供可讓 IT 人員在每一個階段保護資料本身的技術性控制，但混合式身分識別解決方案仍必須能夠運用內部部署和雲端管理資源，在授與資料的存取權之前識別使用者。 規劃您的混合式身分識別解決方案時，請確定會根據貴組織的需求來回答下列問題：

## <a name="data-protection-at-rest"></a>保護待用資料
不論資料是在何處待用 (裝置、雲端或內部部署)，請務必執行評估，以了解組織在這方面的需求。 針對這個層面，請確實回答下列問題：

* 您的公司需要保護待用資料嗎？
  * 如果是，混合式身分識別解決方案是否能夠與您目前的內部部署基礎結構整合？
  * 如果是，混合式身分識別解決方案是否能夠與您在雲端中的工作負載整合？
* 雲端身分識別管理是否能夠保護使用者的認證，和其他儲存在雲端中的資料？

## <a name="data-protection-in-transit"></a>傳輸過程中的資料保護
在裝置與資料中心之間或裝置與雲端之間傳輸的資料，必須受到保護。 不過，所謂的傳輸中並不一定表示雲端服務外部元件的通訊程序；有時也可能在內部發生，像是兩個虛擬網路之間。 針對這個層面，請確實回答下列問題：

* 您的公司需要保護傳輸中的資料嗎？
  * 如果是，混合式身分識別解決方案是否能夠與 SSL/TLS 之類的安全控制項整合？
* 雲端身分識別管理是否可確保進入和存在於目錄的流量 (在資料中心之中和之間) 進行簽署？

## <a name="compliance"></a>法規遵循
規定、法律和法規遵循需求會隨著您的公司所屬的產業而有所不同。 受到嚴格規範的公司，必須處理與法規遵循有關的身分識別管理問題。 諸如沙賓法案 (SOX)、健康保險流通與責任法案 (HIPAA)、美國金融服務法案 (GLBA) 和支付卡產業資料安全標準 (PCI DSS) 等法規，在身分識別和存取方面都有非常嚴格的規定。 您的公司所將採用的混合式身分識別解決方案，必須具有核心功能可因應這些法規的一或多項需求。 針對這個層面，請確實回答下列問題：

* 混合式身分識別解決方案是否符合貴公司的法規需求？
* 混合式身分識別解決方案是否有內建功能可讓您的公司符合法規需求？ 

> [!NOTE]
> 請確定會記下每個答案，並了解答案背後的原理。 [定義資料保護策略](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) 將介紹可用選項，以及每個選項的優點/缺點。  回答這些問題之後，您就能選取最適合業務需求的選項。
> 
> 

## <a name="next-steps"></a>後續步驟
 [判斷內容管理需求](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)

## <a name="see-also"></a>另請參閱
[設計考量概觀](active-directory-hybrid-identity-design-considerations-overview.md)

