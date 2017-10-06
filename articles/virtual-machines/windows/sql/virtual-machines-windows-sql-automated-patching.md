---
title: "aaaAutomated 修補 SQL Server Vm （資源管理員） |Microsoft 文件"
description: "說明 hello 自動修補功能的 SQL Server 虛擬機器使用資源管理員在 Azure 中執行。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a>Azure 虛擬機器的 SQL Server 自動修補 (Resource Manager)
> [!div class="op_single_selector"]
> * [資源管理員](virtual-machines-windows-sql-automated-patching.md)
> * [傳統](../classic/sql-automated-patching.md)
> 
> 

自動修補會針對執行 SQL Server 的 Azure 虛擬機器建立維護時間範圍。 自動更新只能在此維護時間範圍內安裝。 SQL Server 的這個 rescriction 可確保系統更新和任何相關聯的重新啟動發生在 hello 最佳時機進行 hello 資料庫。 自動的修補取決於 hello [SQL Server IaaS 代理程式延伸模組](virtual-machines-windows-sql-server-agent-extension.md)。

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

tooview hello 精簡版本的本文中，請參閱[傳統 Azure 虛擬機器中的 SQL Server 自動修補](../classic/sql-automated-patching.md)。

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

* [安裝最新 Azure PowerShell 命令 hello](/powershell/azure/overview)如果您計劃 tooconfigure 使用 PowerShell 自動修補。

> [!NOTE]
> 自動的修補 」 依賴 hello SQL Server IaaS 代理程式延伸模組。 目前的 SQL 虛擬機器資源庫映像預設會新增這項擴充。 如需詳細資訊，請參閱 [SQL Server IaaS 代理程式擴充](virtual-machines-windows-sql-server-agent-extension.md)。
> 
> 

## <a name="settings"></a>設定
hello 下表描述可以設定自動修補 」 的 hello 選項。 hello 實際的組態步驟，視您使用 hello Azure 入口網站或 Azure Windows PowerShell 命令而有所不同。

| 設定 | 可能的值 | 說明 |
| --- | --- | --- |
| **自動修補** |啟用/停用 (已停用) |啟用或停用 Azure 虛擬機器的自動修補。 |
| **維護排程** |每天、星期一、星期二、星期三、星期四、星期五、星期六、星期日 |下載並安裝虛擬機器的 Windows、 SQL Server 和 Microsoft 更新的 hello 排程。 |
| **維護開始時間** |0-24 |hello 本機的開始時間 tooupdate hello 虛擬機器。 |
| **維護時間範圍** |30-180 |hello 的分鐘數允許 toocomplete hello 下載和安裝更新。 |
| **PATCH 類別** |重要事項 |hello 類別目錄更新 toodownload 及安裝。 |

## <a name="configuration-in-hello-portal"></a>Hello 入口網站中的組態
您可以使用 Azure 入口網站 tooconfigure hello 佈建期間，或現有 Vm 的自動修補。

### <a name="new-vms"></a>新的 VM
使用 hello Azure 入口網站 tooconfigure hello Resource Manager 部署模型中建立新的 SQL Server 虛擬機器時自動修補。

在 hello **SQL Server 設定**刀鋒視窗中，選取**自動修補**。 hello 下列 Azure 入口網站螢幕擷取畫面顯示 hello **SQL 自動修補**刀鋒視窗。

![Azure 入口網站中的 SQL 自動修補](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

針對內容，請參閱 hello 完整主題[佈建 Azure 中的 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。

### <a name="existing-vms"></a>現有的 VM
如果是現有的 SQL Server 虛擬機器，請選取您的 SQL Server 虛擬機器。 然後選取 hello **SQL Server 組態**區段 hello**設定**刀鋒視窗。

![現有 VM 的 SQL 自動修補](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

在 [hello **SQL Server 組態**刀鋒視窗中，按一下 hello**編輯**hello] 按鈕自動修補 > 一節。

![設定現有 VM 的 SQL 自動修補](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

完成後，請按一下 hello **[確定]**上 hello hello 底部的按鈕**SQL Server 組態**刀鋒視窗 toosave 您的變更。

如果您要啟用自動修補 hello 第一次，Azure 會在 hello 背景設定 hello SQL Server IaaS 代理程式。 在此期間，hello Azure 入口網站可能不會顯示已設定自動修補。 等待幾分鐘的時間安裝，hello 代理程式 toobe 設定。 之後的 hello Azure 入口網站會反映 hello 新設定。

> [!NOTE]
> 您也可以使用範本來設定「自動修補」。 如需詳細資訊，請參閱 [適用於自動修補的 Azure 快速入門範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update)。
> 
> 

## <a name="configuration-with-powershell"></a>使用 PowerShell 進行設定
佈建您的 SQL VM 之後, 使用 PowerShell tooconfigure 自動修補。

在下列範例的 hello，PowerShell 會使用的 tooconfigure 自動修補現有的 SQL Server VM 上。 hello **AzureRM.Compute\New New-azurevmsqlserverautopatchingconfig**命令會設定為 「 自動更新的新維護視窗。

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

根據此範例中，hello 下表描述 hello hello 目標 Azure VM 上的實際效果：

| 參數 | 效果 |
| --- | --- |
| **DayOfWeek** |在每個星期四安裝修補程式。 |
| **MaintenanceWindowStartingHour** |在上午 11:00 開始更新。 |
| **MaintenanceWindowsDuration** |必須在 120 分鐘內安裝修補程式。 根據 hello 開始時間，他們必須完成 1:00 pm。 |
| **PatchCategory** |hello 唯一可能的設定此參數為**重要**。 |

它可能需要幾分鐘的時間 tooinstall，並設定 hello SQL Server IaaS 代理程式。

toodisable 自動修補執行 hello 相同指令碼沒有 hello **-啟用**參數 toohello **AzureRM.Compute\New New-azurevmsqlserverautopatchingconfig**。 hello 缺乏 hello **-啟用**參數訊號 hello 命令 toodisable hello 功能。

## <a name="next-steps"></a>後續步驟
如需有關其他可用之自動化工作的資訊，請參閱 [SQL Server IaaS 代理程式擴充功能](virtual-machines-windows-sql-server-agent-extension.md)。

如需有關在 Azure VM 上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)。

