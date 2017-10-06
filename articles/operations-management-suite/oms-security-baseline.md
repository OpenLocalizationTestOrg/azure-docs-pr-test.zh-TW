---
title: "管理組件安全性和稽核解決方案基準 aaaOperations |Microsoft 文件"
description: "本文件說明如何 toouse OMS 安全性和稽核解決方案 tooperform 相容性和安全性用途的所有受監視電腦的基準評估。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: ea52408cb9d2598728fe3826a946067e1c99318f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Operations Management Suite 安全性和稽核解決方案中的基準評估
這份文件可協助您 toouse [Operations Management Suite (OMS) 的安全性和稽核解決方案](operations-management-suite-overview.md)基準評估功能 tooaccess hello 受監視資源的安全的狀態。

## <a name="what-is-baseline-assessment"></a>什麼是基準評估？
Microsoft 與全球產業和政府組織共同定義可代表高度安全伺服器部署的 Windows 組態。 此組態是一組登錄機碼、稽核原則設定和安全性原則設定，以及 Microsoft 對於這些設定的建議值。 這組規則也稱為安全性基準。 OMS 安全性和稽核基準評估功能可以順暢地掃描所有電腦的相容性。 

規則類型有三種：

* **登錄規則**︰檢查登錄機碼是否正確設定。
* **稽核原則規則**︰稽核原則相關規則。
* **安全性原則規則**： 規則 hello 電腦上有關 hello 使用者的權限。

> [!NOTE]
> 讀取[使用 OMS 安全性 tooassess hello 安全性組態基準](https://blogs.technet.microsoft.com/msoms/2016/08/12/use-oms-security-to-assess-the-security-configuration-baseline/)這項功能的簡要概觀。
> 
> 

## <a name="security-baseline-assessment"></a>安全性基準評估
您可以檢閱目前的安全性基準評估受 OMS 安全性和稽核使用 hello 儀表板的所有電腦。  執行下列步驟 tooaccess hello 安全性基準評估的儀表板的 hello:

1. 在 hello **Microsoft Operations Management Suite**主要儀表板中，按一下**安全性和稽核**磚。
2. 在 hello**安全性和稽核**儀表板，按一下 **基準評估**下**安全性網域**。 hello**安全性基準評估**儀表板會顯示 hello 下列影像所示：
   
    ![OMS 安全性和稽核基準評估](./media/oms-security-baseline/oms-security-baseline-fig1.png)

此儀表板分成三個主要區域︰

* **電腦比較 toobaseline**： 這個區段讓 hello 可供存取且 hello 的傳遞 hello 評估的電腦百分比的電腦數目的摘要。 它也會提供 hello 前 10 台電腦及 hello 百分比結果 hello 評估。
* **所需規則的狀態**： 此區段已依嚴重性的 hello 意圖 toobring 感知的 hello 失敗規則，且失敗規則的類型。 尋找您可以快速識別大部分 hello 失敗規則 toohello 第一個圖形都非常重要，或不。 同時也提供一份 hello 前 10 個失敗的規則的嚴重性。 hello 第二個圖表會顯示 hello hello 評估期間失敗的規則類型。 
* **遺失基準評估電腦**： 本節列出 hello 電腦已無法存取到期 toooperating 系統不相容的問題或失敗。 

### <a name="accessing-computers-compared-toobaseline"></a>存取電腦比較 toobaseline
在理想情況下的所有電腦都必須符合的 hello 安全性基準評估。 不過，在某些情況下，應該不會發生這種情形。 Hello 安全性管理程序的一部分，它是重要 tooinclude 檢閱 hello 無法 toopass 安全性評估通過所有測試的電腦。 藉由選取 hello 選項是快速 toovisualize**存取電腦**位於 hello**電腦比較 toobaseline** > 一節。 您應該會看到 hello 記錄搜尋結果顯示 hello 的電腦清單中 hello 遵循畫面所示：

![存取的電腦結果](./media/oms-security-baseline/oms-security-baseline-fig2.png)

hello 搜尋結果會顯示以資料表格式，其中 hello 第一個資料行具有 hello 電腦名稱，而 hello 第二個色彩有 hello 失敗的規則數目。 tooretrieve hello 有關 hello 的規則類型失敗，按一下 hello hello 電腦名稱除了失敗的規則數目。 您應該會看到結果類似 toohello hello 下列影像所示：

![存取的電腦結果詳細資料](./media/oms-security-baseline/oms-security-baseline-fig3.png)

在搜尋結果中，您有存取規則的 hello 總數、 hello 嚴重失敗的規則數目 hello 警告規則和 hello 資訊失敗規則。

### <a name="accessing-required-rules-status"></a>存取需要的規則狀態
取得相關的電腦傳送嗨評估 hello 百分比數字的 hello 資訊之後，您可能想的 tooobtain 失敗相應 toohello 重要性的規則的詳細資訊。 此視覺效果可協助您 tooprioritize 哪些電腦應該處理第一個 tooensure 將無法相容 hello 下一個評估中。 將滑鼠停留在 hello 很重要的一部分位於 hello hello 圖形**失敗規則依嚴重性**磚，在**所需規則的狀態**，然後按一下它。 您應該會看到下列畫面結果類似 toohello:

![依嚴重性的失敗規則詳細資料](./media/oms-security-baseline/oms-security-baseline-fig4.png) 

這個記錄檔結果中，您會看到 hello 基準規則失敗，這個規則，與此安全性規則的 hello 通用組態列舉 (CCE) 識別碼 hello 描述的類型。 這些屬性應該是足夠 tooperform 矯正措施 toofix hello 目標電腦中的這個問題。

> [!NOTE]
> 如需有關 CCE 的詳細資訊，請存取 hello[國家 （地區） 的弱點可能會資料庫](https://nvd.nist.gov/cce/index.cfm)。
> 
> 

### <a name="accessing-computers-missing-baseline-assessment"></a>存取遺失基準評估的電腦
OMS hello 網域成員和網域控制站基準設定檔在 Windows Server 2008 R2 上最多可支援 tooWindows Server 2012 R2。 Windows Server 2016 基準尚未定案，將在發佈後盡快新增。 透過 OMS 安全性和稽核基準評估掃描的所有其他作業系統之下 hello**遺失基準評估電腦**> 一節。

## <a name="see-also"></a>另請參閱
在本文件中，您已了解 OMS 安全性和稽核基準評估。 toolearn 進一步了解 OMS 安全性，請參閱下列文章 hello:

* [Operations Management Suite (OMS) 概觀](operations-management-suite-overview.md)
* [監視及回應 tooSecurity 警示在 Operations Management Suite 安全性和稽核解決方案](oms-security-responding-alerts.md)
* [在 Operations Management Suite 安全性和稽核解決方案內監視資源](oms-security-monitoring-resources.md)

