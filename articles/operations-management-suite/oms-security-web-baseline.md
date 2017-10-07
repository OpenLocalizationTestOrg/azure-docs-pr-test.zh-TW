---
title: "管理套件的安全性和稽核解決方案 Web 基準 aaaOperations |Microsoft 文件"
description: "本文件說明如何 toouse OMS 安全性和稽核解決方案 tooperform web 基準評估相容性和安全性用途的所有受監視的 web 伺服器。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Operations Management Suite 安全性和稽核解決方案中的 Web 基準評估
這份文件可協助您 toouse [Operations Management Suite (OMS) 的安全性和稽核解決方案](operations-management-suite-overview.md)web 基準評估功能 tooaccess hello 受監視資源的安全的狀態。

## <a name="what-is-web-baseline-assessment"></a>什麼是 Web 基準評估？
OMS 安全性目前會提供作業系統的安全性基準評估。 它會掃描每隔 24 小時的 hello 作業系統設定的伺服器，然後可讓您檢視可能有弱點的設定。 如需詳細資訊，請參閱 [Operations Management Suite 安全性和稽核解決方案中的基準評估](oms-security-baseline.md)。

hello web 基準評估 hello 目標是 toofind 可能有弱點的網頁伺服器設定。 hello web 基準設定為 hello 三個主要來源：.NET、 ASP.NET 和 IIS 組態。  就像 hello 作業系統基準評估，OMS 安全性即將 tooscan 您網頁伺服器每隔 24 小時制，並提供讓您檢視它們的安全性狀態。  在 網際網路資訊服務 (IIS) 中，設定是高度可自訂，可讓覆寫的不同網站和應用程式層級 toobe。 hello 掃描器檢查 hello 加法 toohello 預設根層級中每個應用程式/網站層級的設定。 這有助於您 tooidentify 潛在的弱點可能會設定位置，並快速修正。


## <a name="web-security-baseline-assessment"></a>Web 安全性基準評估
此預覽這項功能即將 toobe 使用 hello OMS 搜尋選項來存取。 請遵循以下 tooperform hello appropriated 查詢 hello 步驟：

1. 在 hello **Microsoft Operations Management Suite**主要儀表板按一下**安全性和稽核**磚。
2. 在 hello**安全性和稽核**儀表板，按一下 **記錄搜尋** 按鈕。
3. hello 第一個查詢，您可以使用為 hello **Web 基準評估摘要**。 在 hello**這裡開始搜尋**欄位中，輸入此查詢： 型別*= SecurityBaselineSummary BaselineType = web*。 下列畫面 hello 具有輸出範例：

![Web 基準評估摘要](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> 在此查詢中，每筆記錄都會指出在單一伺服器上的評估摘要。

當您在 hello**記錄搜尋**，您可以輸入不同的查詢 tooobtain hello web 基準評估的詳細資訊。 此外 toohello 上述查詢中，您也可以使用下列是在此預覽中的 hello。

**Web 基準規則評估**︰每筆記錄均代表單一伺服器上的單一 Web 基準規則評估。 它包含 hello 規則、 位置、 hello 預期的結果，以及 hello 實際結果的所有資料。

**查詢**：Type=SecurityBaseline BaselineType=web

![Web 基準規則評估](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

**顯示特定伺服器的所有結果**： 此查詢會顯示如何 toosee 結果的特定伺服器。

**查詢**：Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1

![所有結果](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

您也可以使用這些記錄/查詢 toocreate 您自己的儀表板、 報表或警示。 囉 」 畫面下方有範例 UI 控制項，您可以加入 tooyour 儀表板。 您可以了解如何 toovisualize 資料，可使用 OMS 檢視表設計工具[這裡](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/)。 囉 」 畫面下方是 hello 的並排顯示的範例看起來像一旦完成這項自訂。

![範例 UI](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> 如果您想要檢查 hello 基準評估 tooknow hello 設定，您可以下載[這個 Excel 試算表](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690)，其中包含這些設定。

## <a name="see-also"></a>另請參閱
在本文件中，您已了解 OMS 安全性和稽核 Web 基準評估。 toolearn 進一步了解 OMS 安全性，請參閱下列文章 hello:

* [Operations Management Suite (OMS) 概觀](operations-management-suite-overview.md)
* [監視及回應 tooSecurity 警示在 Operations Management Suite 安全性和稽核解決方案](oms-security-responding-alerts.md)
* [在 Operations Management Suite 安全性和稽核解決方案內監視資源](oms-security-monitoring-resources.md)

