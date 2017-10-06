---
title: "aaaOperations Management Suite (OMS) 架構 |Microsoft 文件"
description: "Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。  這份文件識別包含在 OMS 中的 hello 不同服務，並提供連結 tootheir 詳細內容。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 40e41686-7e35-4d85-bbe8-edbcb295a534
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: fa3227aa9c19219009ebe363b7fd2d6565cec59c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="oms-architecture"></a>OMS 架構
[Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/services/operations-management-suite/) 是管理內部部署和雲端環境的雲端型服務集合。  本文說明 hello 不同內部部署和雲端元件 OMS，及其高階的雲端運算架構。  您可以針對每個服務，以取得詳細資料，請參閱 toohello 文件。

## <a name="log-analytics"></a>Log Analytics
所收集的所有資料[記錄分析](https://azure.microsoft.com/documentation/services/log-analytics/)儲存在裝載於 Azure hello OMS 儲存機制。  連線的來源產生資料收集到 hello OMS 儲存機制。  目前支援三種類型的已連接來源。

* 上安裝代理程式[Windows](../log-analytics/log-analytics-windows-agents.md)或[Linux](../log-analytics/log-analytics-linux-agents.md)電腦直接連線 tooOMS。
* System Center Operations Manager (SCOM) 管理群組[連接 tooLog 分析](../log-analytics/log-analytics-om-agents.md)。  SCOM 代理程式仍持續與管理伺服器轉送事件和效能資料 tooLog 分析 toocommunicate。
* [Azure 儲存體帳戶](../log-analytics/log-analytics-azure-storage.md)，收集 Azure 背景工作角色、Web 角色或虛擬機器中的 [Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) 資料。

資料來源定義 hello 記錄分析會從已連線的來源，包括事件記錄檔和效能計數器收集的資料。  加入功能 tooOMS 解決方案，並可輕鬆地加入 tooyour 工作區中的 hello [OMS 解決方案資源庫](../log-analytics/log-analytics-add-solutions.md)。  某些解決方案可能需要從 SCOM 代理程式直接連接 tooLog 分析，而有些則可能需要安裝其他代理程式 toobe。

記錄分析具有 web 入口網站，您可以使用 toomanage OMS 資源、 加入和設定 OMS 解決方案，並檢視及分析 hello OMS 儲存機制中的資料。

![Log Analytics 高階架構](media/operations-management-suite-architecture/log-analytics.png)

## <a name="azure-automation"></a>Azure 自動化
[Azure 自動化 runbook](http://azure.microsoft.com/documentation/services/automation) hello Azure 雲端中執行的而且可以存取位於 Azure 中其他雲端服務，或從可存取的資源 hello 公用網際網路。  您也可以使用[Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md) 指定本機資料中心的內部部署電腦，讓 Runbook 可以存取本機資源。

[DSC 設定](../automation/automation-dsc-overview.md)儲存在 Azure 自動化可直接套用的 tooAzure 虛擬機器。  其他實體和虛擬機器可以從 hello Azure Automation DSC 提取伺服器要求組態。

Azure 自動化有一項 OMS 解決方案，會顯示統計資料，並連結 toolaunch hello Azure 入口網站進行任何作業。

![Azure 自動化高階架構](media/operations-management-suite-architecture/automation.png)

## <a name="azure-backup"></a>Azure 備份
[Azure 備份](http://azure.microsoft.com/documentation/services/backup) 中的受保護資料儲存在位於特定地理區域的備份保存庫中。  hello 資料會複寫在 hello 相同的區域，並根據 hello 保存庫類型，也可能供進一步備援複寫的 tooanother 區域。

Azure 備份有三種基本案例。

* 具有 Azure 備份代理程式的 Windows 電腦。  這可讓您 toobackup 檔案和資料夾從任何 Windows server 或用戶端直接 tooyour Azure 備份保存庫。  
* System Center Data Protection Manager (DPM) 或 Microsoft Azure 備份伺服器。 這可讓您 tooleverage DPM 或 Microsoft Azure 備份伺服器 toobackup 檔案和資料夾此外 tooapplication 工作負載，例如 SQL 和 SharePoint toolocal 儲存體，然後複寫 tooyour Azure 備份保存庫。
* Azure 虛擬機器擴充功能。  這可讓您 toobackup Azure 虛擬機器 tooyour Azure 備份保存庫。

Azure 備份有一項 OMS 解決方案，會顯示統計資料，並連結 toolaunch hello Azure 入口網站進行任何作業。

![Azure 備份高階架構](media/operations-management-suite-architecture/backup.png)

## <a name="azure-site-recovery"></a>Azure Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) 可協調虛擬機器和實體伺服器的複寫、容錯移轉和容錯回復。 HYPER-V 主機、 VMware hypervisor 與主要和次要資料中心內的實體伺服器或 hello 資料中心與 Azure 儲存體之間交換複寫資料。  Site Recovery 會將元資料儲存到位於特定地理 Azure 區域的保存庫中。 不會儲存複寫的資料 hello Site Recovery 服務。

Azure Site Recovery 有三種基本複寫案例。

**Hyper-V 虛擬機器的複寫**

* 如果 VMM 雲端中管理 HYPER-V 虛擬機器，您就可以複寫 tooa 次要資料中心或 tooAzure 儲存體。  複寫 tooAzure 是透過安全的網際網路連線。  複寫 tooa 次要資料中心是透過 hello LAN。
* 若為 HYPER-V 虛擬機器不由 VMM 管理，您只能複寫 tooAzure 儲存體。  複寫 tooAzure 是透過安全的網際網路連線。

**VMWare 虛擬機器的複寫**

* 您可以將 VMware 虛擬機器 tooa 次要資料中心執行 VMware 或 tooAzure 儲存體的複寫。  透過站對站 VPN、 Azure ExpressRoute 或是安全的網際網路連線，就會發生複寫 tooAzure。 複寫 tooa 次要資料中心發生 hello InMage Scout 資料通道。

**實體 Windows 和 Linux 伺服器的複寫** 

* 您可以將實體伺服器 tooa 次要資料中心或 tooAzure 儲存體的複寫。 透過站對站 VPN、 Azure ExpressRoute 或是安全的網際網路連線，就會發生複寫 tooAzure。 複寫 tooa 次要資料中心發生 hello InMage Scout 資料通道。  Azure Site Recovery 有一項 OMS 解決方案會顯示統計資料，但是您必須使用 hello Azure 入口網站進行任何作業。

![Azure Site Recovery 高階架構](media/operations-management-suite-architecture/site-recovery.png)

## <a name="next-steps"></a>後續步驟
* 了解 [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics)。
* 了解 [Azure 自動化](https://azure.microsoft.com/documentation/services/automation)。
* 了解 [Azure 備份](http://azure.microsoft.com/documentation/services/backup)。
* 了解 [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery)。

