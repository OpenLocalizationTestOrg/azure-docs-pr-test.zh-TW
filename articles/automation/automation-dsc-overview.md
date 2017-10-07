---
title: "aaaAzure 自動化 DSC 的概觀 |Microsoft 文件"
description: "Azure 自動化期望狀態組態 (DSC)、其條款和已知問題的概觀"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "powershell dsc, 需要的狀態組態, powershell dsc azure"
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a>Azure 自動化 DSC 概觀

Azure 自動化 DSC 是一項 Azure 服務，可讓您 toowrite、 管理及編譯 PowerShell 預期狀態設定 (DSC)[組態](https://msdn.microsoft.com/powershell/dsc/configurations)，匯入[DSC 資源](https://msdn.microsoft.com/powershell/dsc/resources)，並指派設定 tootarget 節點，所有 hello 雲端中。

## <a name="why-use-azure-automation-dsc"></a>為何使用 Azure Automation DSC

Azure Automation DSC 提供在 Azure 外部使用 DSC 的數個優點。

### <a name="built-in-pull-server"></a>內建提取伺服器

Azure 自動化提供[DSC 提取伺服器](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver)，目標節點會自動接收組態，符合 toohello 預期狀態，以及回報其相容性。
hello Azure 自動化中的內建的提取伺服器 hello 需要 tooset 排除設定和維護您自己的提取伺服器。
Azure 自動化可鎖定目標虛擬機器或實體 Windows 或 Linux 機器，hello 雲端或內部部署中。

### <a name="management-of-all-your-dsc-artifacts"></a>所有 DSC 構件的管理

Azure Automation DSC 讓太 hello 相同的管理層[PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) Azure 自動化提供 PowerShell 指令碼處理。

從 hello Azure 入口網站或 PowerShell，您可以管理所有您 DSC 設定、 資源和目標節點。

![Hello Azure 自動化刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a>將報告資料匯入至 Log Analytics

使用 Azure 自動化 DSC 傳送詳細報告狀態資料 toohello 內建的提取伺服器所管理的節點。
您可以設定 Azure 自動化 DSC toosend 此資料 tooyour Microsoft Operations Management Suite (OMS) 的記錄分析工作區。
如何 toosend DSC 狀態資料 tooyour 記錄分析工作區中，請參閱的 toolearn[向前復原 Azure 自動化 DSC 報告資料 tooOMS 記錄分析](automation-dsc-diagnostics.md)。

## <a name="introduction-video"></a>簡介影片

偏好觀看 tooreading 嗎？ 看看下列影片從 2015 年首次宣佈 Azure Automation DSC 的 hello。

>[!NOTE]
>雖然正確 hello 概念和生命週期，這段影片中所述，Azure Automation DSC 已在這段影片錄製，因為許多前進。
>現在已上市，hello Azure 入口網站中具備更廣泛的 UI，而且支援許多其他功能。

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a>後續步驟

* toolearn 如何 tooonboard 節點 toobe 所管理的 Azure 自動化 DSC，請參閱[供 Azure Automation DSC 來管理登入機器](automation-dsc-onboarding.md)
* 請參閱 < 開始使用 Azure 自動化 DSC tooget[開始使用 Azure 自動化 DSC](automation-dsc-getting-started.md)
* toolearn 需編譯 DSC 設定，以指派 tootarget 節點，請參閱[編譯在 Azure Automation DSC 設定](automation-dsc-compile.md)
* 如需 Azure Automation DSC 的 PowerShell Cmdlet 參考，請參閱 [Azure Automation DSC Cmdlet](/powershell/module/azurerm.automation/#automation)。
* 如需定價資訊，請參閱 [Azure Automation DSC 定價](https://azure.microsoft.com/pricing/details/automation/)。
* toosee 示範如何使用 Azure 自動化 DSC 在連續部署管線中，請參閱[連續部署 tooIaaS Vm 使用 Azure 自動化 DSC 和 Chocolatey](automation-dsc-cd-chocolatey.md)
