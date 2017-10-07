---
title: "aaaAutomated 修補 SQL Server Vm （傳統） |Microsoft 文件"
description: "說明 hello 自動修補功能的 SQL Server 虛擬機器在 Azure 使用 hello 傳統部署模式中執行。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a>Azure 虛擬機器中的 SQL Server 自動修補 (傳統)
> [!div class="op_single_selector"]
> * [資源管理員](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [傳統](../classic/sql-automated-patching.md)
> 
> 

自動修補會針對執行 SQL Server 的 Azure 虛擬機器建立維護時間範圍。 自動更新只能在此維護時間範圍內安裝。 針對 SQL Server，這可確保系統更新和任何相關聯的重新啟動發生在 hello 最佳時機進行 hello 資料庫。 自動的修補取決於 hello [SQL Server IaaS 代理程式延伸模組](../classic/sql-server-agent-extension.md)。

> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 請參閱這篇文章，tooview hello 資源管理員版本[自動修補 SQL server 在 Azure 虛擬機器資源管理員](../sql/virtual-machines-windows-sql-automated-patching.md)。

## <a name="prerequisites"></a>必要條件
toouse 自動修補，請考慮下列必要條件 hello:

**作業系統**：

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**SQL Server 版本**：

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Azure PowerShell**：

* [安裝最新 Azure PowerShell 命令 hello](/powershell/azure/overview)。

**SQL Server IaaS 擴充功能**：

* [安裝 SQL Server IaaS 延伸模組 hello](../classic/sql-server-agent-extension.md)。

## <a name="settings"></a>設定
hello 下表描述可以設定自動修補 」 的 hello 選項。 對於傳統的 Vm，您必須使用 PowerShell tooconfigure 這些設定。

| 設定 | 可能的值 | 說明 |
| --- | --- | --- |
| **自動修補** |啟用/停用 (已停用) |啟用或停用 Azure 虛擬機器的自動修補。 |
| **維護排程** |每天、星期一、星期二、星期三、星期四、星期五、星期六、星期日 |下載並安裝虛擬機器的 Windows、 SQL Server 和 Microsoft 更新的 hello 排程。 |
| **維護開始時間** |0-24 |hello 本機的開始時間 tooupdate hello 虛擬機器。 |
| **維護時間範圍** |30-180 |hello 的分鐘數允許 toocomplete hello 下載和安裝更新。 |
| **PATCH 類別** |重要事項 |hello 類別目錄更新 toodownload 及安裝。 |

## <a name="configuration-with-powershell"></a>使用 PowerShell 進行設定
在下列範例的 hello，PowerShell 會使用的 tooconfigure 自動修補現有的 SQL Server VM 上。 hello **New-azurevmsqlserverautopatchingconfig**命令會設定為 「 自動更新的新維護視窗。

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

根據此範例中，hello 下表描述 hello hello 目標 Azure VM 上的實際效果：

| 參數 | 效果 |
| --- | --- |
| **DayOfWeek** |在每個星期四安裝修補程式。 |
| **MaintenanceWindowStartingHour** |在上午 11:00 開始更新。 |
| **MaintenanceWindowsDuration** |必須在 120 分鐘內安裝修補程式。 根據 hello 開始時間，他們必須完成 1:00 pm。 |
| **PatchCategory** |hello 這個參數只可以設定為 「 重要 」。 |

它可能需要幾分鐘的時間 tooinstall，並設定 hello SQL Server IaaS 代理程式。

toodisable 自動修補相同指令碼而不執行 hello hello-Enable 參數 toohello New-azurevmsqlserverautopatchingconfig。 為進行安裝，可能需要幾分鐘的時間 toodisable 自動修補。

## <a name="next-steps"></a>後續步驟
如需有關其他可用之自動化工作的資訊，請參閱 [SQL Server IaaS 代理程式擴充功能](../classic/sql-server-agent-extension.md)。

如需有關在 Azure VM 上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。

