---
title: "在 Operations Management Suite 安全性和稽核解決方案基準基準評估 aaaWeb |Microsoft 文件"
description: "本文件說明如何 toouse web 基準評估 OMS 安全性和稽核解決方案 tooperform 基準評估相容性和安全性用途的所有受監視的 web 伺服器中。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: dafa9d3d93fae31748306b60ee40b285dd59c802
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Operations Management Suite 安全性和稽核解決方案中的 Web 基準評估
這份文件可協助您使用 OMS 安全性和稽核 web 基準評估功能 tooaccess hello 受監視資源的安全的狀態。

## <a name="what-is-web-baseline-assessment"></a>什麼是 Web 基準評估？
OMS 安全性目前會提供作業系統的安全性基準評估。 它會每 24 小時，會掃描您的伺服器 hello OS 設定，並提供讓您檢視可能有弱點的設定。 如需詳細資訊，請參閱 [Operations Management Suite 安全性和稽核解決方案中的基準評估](https://docs.microsoft.com/azure/operations-management-suite/oms-security-baseline)。

hello Web 基準評估 hello 目標是 toofind 可能有弱點的網頁伺服器設定。 hello web 基準設定為 hello 三個主要來源：.NET、 ASP.NET 和 IIS 組態。  就像 hello 作業系統基準評估，OMS 安全性即將 tooscan 您網頁伺服器每隔 24 小時制，並提供讓您檢視它們的安全性狀態。  在 網際網路資訊服務 (IIS) 中，設定是高度可自訂，可讓覆寫的不同網站和應用程式層級 toobe。 hello 掃描器檢查 hello 加法 toohello 預設根層級中每個應用程式/網站層級的設定。 這有助於您 tooidentify 可能有弱點的設定，並快速修正，以及我們的建議的設定。

>[!NOTE] 
>您可以下載 hello 常見的組態識別碼與在此使用 OMS 安全性的基準規則[頁面](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335?redir=0)。


## <a name="web-security-baseline-assessment"></a>Web 安全性基準評估

此預覽 hello 功能可以透過 hello OMS 搜尋選項和 hello OMS 安全性和稽核儀表板。 請遵循以下 tooperform hello appropriated 查詢 hello 步驟：

1. 在 hello **Microsoft Operations Management Suite**主要儀表板中，按一下**安全性和稽核**磚。
2. 在 hello**安全性和稽核**儀表板，您可以看到 hello Web 基準檢視方塊 下一步 toohello OS 基準檢視方塊。
   
    ![OMS 安全性和稽核 Web 安全幸基準評估](./media/oms-security-web-baseline/oms-security-web-baseline-fig5.png)

3. hello 左的窗格會顯示 hello 數目進行比較的網頁伺服器 toohello 基準，hello 平均百分比傳遞所有的 hello 評估伺服器的規則及 hello 所評估的伺服器清單。
4. 右窗格會列出 hello 唯一 hello 規則失敗*嚴重性*，和*RuleType*。 按一下任一 hello 右窗格的規則將會顯示 hello 詳細資料，該規則。 範例所示 hello 影像下方。 評估 hello 規則都會列在下*規則設定*。 hello *AzId*欄位，也就是 Microsoft 用於追蹤 hello 基準規則每個規則的唯一識別碼。 此外 toothat 使用者可以看到 hello*預期的結果*（Microsoft 的建議值），和其他詳細資料有關的 hello 規則 hello 安全性影響。
    
    ![查詢](./media/oms-security-web-baseline/oms-security-web-baseline-fig6.png)

5. 您可以建立您自己的查詢 tooreview hello 結果。 

hello 第一個查詢，您可以使用為 hello **Web 基準評估摘要**。 在 hello**這裡開始搜尋**欄位中，輸入此查詢：*類型 = SecurityBaselineSummary BaselineType = Web*。 hello 下面是輸出範例：

![查詢結果](./media/oms-security-web-baseline/oms-security-web-baseline-fig7.png)

>[!NOTE] 
>在此查詢中，每筆記錄都會指出在單一伺服器上的評估摘要。

當您在 hello**記錄搜尋**，您可以輸入不同的查詢 tooobtain hello web 基準評估的詳細資訊。 此外 toohello 上述查詢中，您也可以使用下列是在此預覽中的 hello:

**Web 基準規則評估**︰每筆記錄均代表單一伺服器上的單一 Web 基準規則評估。 它包含所有資料針對失敗的規則，hello *SitePath*上哪些 hello 規則評估，hello*預期的結果*，和 hello*實際結果*。

查詢：*Type=SecurityBaseline BaselineType=Web AnalyzeResult=Failed*

![查詢結果 2](./media/oms-security-web-baseline/oms-security-web-baseline-fig8.png)

**顯示特定伺服器的所有結果**： 此查詢會顯示如何 toosee 結果的特定伺服器： 查詢：*類型 = SecurityBaseline BaselineType = Web 電腦 = BaselineTestVM1*

![查詢結果 3](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

您可以使用這些記錄/查詢 toocreate 您自己的儀表板、 報表或警示。 以下是範例 UI 控制項，您可以加入 tooyour 儀表板。 您可以了解如何 toovisualize 資料，可使用 OMS 檢視表設計工具[這裡](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/)。 囉 」 畫面下方是 hello 的並排顯示的範例看起來像一旦完成這項自訂。

![儀表板](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

## <a name="see-also"></a>另請參閱
在本文件中，您已了解 OMS 安全性和稽核 Web 基準評估。 toolearn 進一步了解 OMS 安全性，請參閱下列文章 hello:

* [Operations Management Suite (OMS) 概觀](operations-management-suite-overview.md)
* [監視及回應 tooSecurity 警示在 Operations Management Suite 安全性和稽核解決方案](oms-security-responding-alerts.md)
* [在 Operations Management Suite 安全性和稽核解決方案內監視資源](oms-security-monitoring-resources.md)

