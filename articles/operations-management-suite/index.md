---
title: "aaaAzure Operations Management Suite (OMS) 文件-教學課程 |Microsoft 文件"
description: "Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。 這份文件識別包含在 OMS 中的 hello 不同服務，並提供連結 tootheir 詳細內容。"
services: operations-management-suite
author: carolz
manager: carolz
layout: LandingPage
ms.assetid: 
ms.service: operations-management-suite
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: landing-page
ms.date: 01/23/2017
ms.author: carolz
ms.openlocfilehash: 11a8f5ecb3d84aed90554510fc1bb43320fdebb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>Operations Management Suite (OMS) 是什麼？
Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。  因為 OMS 實作為雲端型服務，所以您對基礎結構服務進行最小的投資就可以快速啟動並執行它。  會自動提供新功能，以節省持續性維護和升級成本。

此外 tooproviding 重要服務在其本身，OMS 可以整合 System Center 元件，例如 System Center Operations Manager tooextend 現有的管理投資 hello 雲端。  System Center 和 OMS 可一起運作的 tooprovide 完整的混合式管理體驗。

hello 下列各節會提供可實作這些 OMS 與 hello 服務的 hello 不同的值區域，高層級描述。  檢閱 hello 詳述每個文件之前，您可以參考 tooOMS 架構 hello 不同 OMS 元件的概觀。

## <a name="insight-and-analyticsmediaoperations-management-suite-overviewicon-insight-analyticspng-insight-and-analytics"></a>![深入解析與分析](media/operations-management-suite-overview/icon-insight-analytics.png) 深入解析與分析
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) 可協助您收集、相互關聯、搜尋和處理作業系統和應用程式所產生的記錄檔和效能資料。 它可讓您即時的 operational insights 使用整合的搜尋和自訂儀表板 tooreadily 地分析數百萬筆記錄的所有工作負載和伺服器，無論其實體位置為何。

您可以輕鬆加入解決方案 tooLog 分析會定義收集的資料 toobe 以及 hello 分析邏輯。  解決方案可能包含會自動傳遞 tooagents，幾乎不需要或不設定的其他功能。  此外 toousing 分析工具個別解決方案所提供，您可以執行自訂搜尋 hello 系統和應用程式之間的順序 toocorrelate 資料中的整個資料集。  

## <a name="automation--controlmediaoperations-management-suite-overviewicon-automation-controlpng-automation--control"></a>![自動化與控制](media/operations-management-suite-overview/icon-automation-control.png) 自動化與控制
Azure 自動化可自動化管理程序與[runbook](../automation/automation-runbook-types.md) ，它們 PowerShell 為基礎，並且在 hello Azure 雲端中執行。  Runbook 可以存取可使用 PowerShell 管理的任何產品或服務，包括其他雲端 (例如 Amazon Web Services (AWS)) 中的資源。  也可以在您本機資料中心 toomanage 本機資源的伺服器上，執行 Runbook。

Azure 自動化使用 [PowerShell DSC](../automation/automation-dsc-overview.md) 來提供組態管理。  您可以建立及管理裝載於 Azure 的 DSC 資源並將其套用 toocloud 和內部系統 toodefine 和自動強制執行其設定。

## <a name="protection-and-recoverymediaoperations-management-suite-overviewicon-protection-recoverypng-protection-and-disaster-recovery"></a>![保護和復原](media/operations-management-suite-overview/icon-protection-recovery.png) 保護和災害復原
[Azure 備份](http://azure.microsoft.com/documentation/services/backup) 會保護您的應用程式資料並保留數年，而您完全不必投入資本投資，並且只需要最少的營運成本。  它可以備份資料從 SQL Server 和 SharePoint 等加法 tooapplication 工作負載中的實體和虛擬 Windows 伺服器。  它也可用於由 System Center Data Protection Manager (DPM) 保護 tooreplicate 資料 tooAzure 備援及長期儲存。

[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery)佔 tooyour 業務續航力和災害復原 (BCDR) 策略可藉由協調複寫、 容錯移轉和復原的內部部署 HYPER-V 虛擬機器、 VMware 虛擬機器和實體 Windows /Linux 伺服器。 您可以複製機器 tooa 次要資料中心，或將它們複製 tooAzure 擴充您的資料中心。 Site Recovery 也提供工作負載的簡單容錯移轉和復原。 它會與災害復原機制 (例如 SQL Server AlwaysOn) 整合，並提供復原計劃輕鬆容錯移轉跨多部電腦分層的工作負載。

## <a name="oms-security-and-compliancemediaoperations-management-suite-overviewicon-security-compliancepng-security-and-compliance"></a>![OMS 安全性與法規遵循](media/operations-management-suite-overview/icon-security-compliance.png) 安全性與法規遵循
安全性與相容性，可協助您識別、 評估及降低安全性風險 tooyour 基礎結構。  透過分析記錄資料和來自代理程式的系統 tooassist 設定的記錄分析中的多個方案實作這些 OMS 功能您確保環境的 hello 持續安全性。

* hello[安全性和稽核 」 解決方案](oms-security-getting-started.md)會收集並分析受管理的系統 tooidentify 可疑的活動上的安全性事件。
* hello[反惡意程式碼解決方案](../log-analytics/log-analytics-malware.md)hello 受管理系統上的反惡意程式碼保護狀態報告。  
* hello 系統更新解決方案會分析 hello 安全性更新和其他更新受管理系統，讓您輕鬆地識別系統需要修補。

## <a name="next-steps"></a>後續步驟
* 了解 [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics)。
* 了解 [Azure 自動化](../automation/automation-intro.md)。
* 了解 [Azure 備份](http://azure.microsoft.com/documentation/services/backup)。
* 了解 [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery)。

