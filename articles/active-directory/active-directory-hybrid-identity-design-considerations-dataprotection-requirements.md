---
title: "aaaAzure Active Directory 混合式身分識別設計考量-決定資料保護需求 |Microsoft 文件"
description: "當您規劃混合式身分識別解決方案，識別 hello 資料保護需求的業務及哪些選項可以使用 toobest 達到這些需求。"
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
ms.openlocfilehash: 189abf9affbc2894c322f362d84222d4e33d472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-enhancing-data-security-through-strong-identity-solution"></a>透過增強式身分識別解決方案規劃更高的資料安全性
hello 第一個步驟 tooprotect hello 資料會識別哪些人可以存取該資料，而且這個程序的一部分，您需要的 toohave 系統 tooprovide 驗證和授權功能與整合，可以識別解決方案。 驗證和授權常被混淆，兩者角色也常被誤解。 在現實它們是完全不同，hello 圖所示：

![](./media/hybrid-id-design-considerations/mobile-devicemgt-lifecycle.png)

**行動裝置管理生命週期階段**

規劃您的混合式身分識別解決方案時必須了解您的業務和哪些選項可以使用 toobest hello 資料保護需求達到這些需求。

> [!NOTE]
> 完成之後提供資料安全性規劃，檢閱[判斷多因素驗證需求](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)tooensure 有關多因素驗證需求選擇了不受 hello 決策您進行這一節。
> 
> 

## <a name="determine-data-protection-requirements"></a>判斷資料保護需求
在行動性 hello 時代，大部分的公司有共同的目標： 啟用其使用者 toobe 提高生產力在內部部署時，或從遠端在行動裝置上從任何地方順序 tooincrease 產能。 雖然這可能是共同的目標，公司已經有這類需求也會考量有關 hello 數量必須降低順序 tookeep 公司資料安全，並維護使用者的隱私權威脅。 每一家公司可能會在這方面，有不同的需求不同的符合性規則，將使變化相應 toowhich 業界 hello 公司做將會導致 toodifferent 設計決策。 

不過，有一些安全性層面應該瀏覽及驗證，不論 hello 業界 hello 下一節中所說明。

## <a name="data-protection-paths"></a>資料保護路徑
![](./media/hybrid-id-design-considerations/data-protection-paths.png)

**資料保護路徑**

在上方圖表 hello，hello 識別元件，會驗證才能存取資料的第一個 toobe hello。 不過，此資料可以在不同狀態期間 hello 存取它。 此圖表上的每個數字，分別代表資料在某個時間點的所在的路徑。 這些數字的說明如下：

1. Hello 裝置層級的資料保護。
2. 傳輸過程中的資料保護。
3. 在內部部署中待用時的資料保護。
4. 在 hello 雲端待用時的資料保護。

雖然 hello 技術控制項，將允許這些階段的每個 IT tooprotect hello 資料本身不會直接提供 hello 混合式身分識別解決方案，則需要 hello 混合式身分識別解決方案能夠利用這兩個內部部署部署和雲端身分識別管理資源 tooidentify hello 使用者授與存取 toohello 資料之前。 當您規劃混合式身分識別解決方案確定遵循該 hello 問題根據 tooyour 組織的需求：

## <a name="data-protection-at-rest"></a>保護待用資料
不論其中 hello 資料是在靜止 （裝置、 雲端或內部部署），請務必 tooperform 評估 toounderstand hello 組織必須在這方面。 這個區域中，請確定系統會要求該 hello 下列問題：

* 您的公司是否需要 tooprotect 待用的資料？
  * 如果是，請與您目前的內部部署基礎結構是否 hello 混合式身分識別解決方案可以 toointegrate？
  * 如果是，請與您在 hello 雲端中的工作負載是否 hello 混合式身分識別解決方案可以 toointegrate？
* 是 hello 雲端身分識別管理可以 tooprotect hello 使用者的認證和其他資料儲存在 hello 雲端？

## <a name="data-protection-in-transit"></a>傳輸過程中的資料保護
裝置 hello 與 hello 資料中心之間或 hello 裝置與 hello 雲端之間的傳輸中的資料必須加以保護。 不過，所謂的傳輸中並不一定表示雲端服務外部元件的通訊程序；有時也可能在內部發生，像是兩個虛擬網路之間。 這個區域中，請確定系統會要求該 hello 下列問題：

* 您的公司是否需要在傳輸過程中的 tooprotect 資料？
  * 如果是，是否 hello 混合式身分識別解決方案可以 toointegrate 與安全的控制項，例如 SSL/TLS？
* 沒有 hello 雲端身分識別管理可以保留 hello 流量 tooand hello 目錄存放區中 （在且資料中心之間） 簽署嗎？

## <a name="compliance"></a>法規遵循
規範、 法律及法規遵循需求而異公司所屬的相應 toohello 產業。 高管制產業中的公司必須先處理身分識別管理考量相關的 toocompliance 問題。 例如沙氏法案 (SOX)、 hello 健康保險流通與責任法案 (HIPAA) 規定 hello Gramm-Leach-Bliley Act (GLBA) 和 hello 付款卡產業資料安全標準 (PCI DSS) 非常嚴格有關身分識別和存取。 您的公司將採用的 hello 混合式身分識別解決方案必須都滿足 hello 需求的一或多個這些規定的 hello 核心功能。 這個區域中，請確定系統會要求該 hello 下列問題：

* 是 hello 混合式身分識別解決方案符合您公司的 hello 法規要求？
* 沒有 hello 混合式身分識別解決方案具有內建功能可讓您公司 toobe 符合法規需求？ 

> [!NOTE]
> 請確定每個答案 tootake 附註，並了解 hello 回應 hello 背後的基本原理。 [定義的資料保護策略](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)將介紹可用 hello 選項以及每個選項的優點/缺點。  回答這些問題之後，您就能選取最適合業務需求的選項。
> 
> 

## <a name="next-steps"></a>後續步驟
 [判斷內容管理需求](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)

## <a name="see-also"></a>另請參閱
[設計考量概觀](active-directory-hybrid-identity-design-considerations-overview.md)

