---
title: "aaaAutomate 管理工作上的 SQL Vm （資源管理員） |Microsoft 文件"
description: "本主題描述如何 toomanage hello SQL Server 代理程式延伸特定的 SQL Server 系統管理工作自動化。 其中包括自動備份、自動修補和 Azure 金鑰保存庫整合。 本主題使用 hello Resource Manager 部署模式。"
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a>自動化管理工作在 Azure 虛擬機器以 hello SQL Server 代理程式延伸模組 （資源管理員）
> [!div class="op_single_selector"]
> * [資源管理員](virtual-machines-windows-sql-server-agent-extension.md)
> * [傳統](../classic/sql-server-agent-extension.md)
> 
> 

hello SQL Server IaaS 代理程式延伸模組 (SQLIaaSExtension) 會執行於 Azure 虛擬機器 tooautomate 系統管理工作。 本主題提供支援 hello 延伸模組，以及安裝、 狀態及移除指示 hello 服務的概觀。

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

tooview hello 精簡版本的本文中，請參閱[SQL Server 代理程式延伸模組，如 SQL Server 傳統 Vm](../classic/sql-server-agent-extension.md)。

## <a name="supported-services"></a>支援的服務
hello SQL Server IaaS 代理程式延伸模組支援下列管理工作的 hello:

| 系統管理功能 | 說明 |
| --- | --- |
| **SQL 自動備份** |會自動將 hello 預設執行個體的 SQL Server hello VM 中的所有資料庫的備份排程 hello。 如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 自動備份 (Resource Manager)](virtual-machines-windows-sql-automated-backup.md)。 |
| **SQL 自動修補** |設定維護間隔期間哪些更新將放置的 tooyour VM 可以採取，如此您就不必在您的工作負載尖峰期間更新。 如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 自動修補 (Resource Manager)](virtual-machines-windows-sql-automated-patching.md)。 |
| **Azure 金鑰保存庫整合** |可讓您 tooautomatically 上安裝及設定 Azure 金鑰保存庫 SQL Server VM。 如需詳細資訊，請參閱 [在 Azure VM (Resource Manager) 上設定 SQL Server 的 Azure 金鑰保存庫整合](virtual-machines-windows-ps-sql-keyvault.md)。 |

一旦安裝並執行，hello SQL Server IaaS 代理程式延伸模組提供這些管理功能 hello hello 虛擬機器在 hello Azure 入口網站，並透過 Azure PowerShell for SQL Server marketplace 映像，以及透過 SQL Server 面板上適用於 hello 延伸模組的手動安裝的 azure PowerShell。 

## <a name="prerequisites"></a>必要條件
SQL Server IaaS 代理程式延伸模組在您的 VM 上需求 toouse hello:

**作業系統**：

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**SQL Server 版本**：

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Azure PowerShell**：

* [下載及設定 hello 最新的 Azure PowerShell 命令](/powershell/azure/overview)

## <a name="installation"></a>安裝
在佈建一個 hello SQL Server 虛擬機器圖庫映像時，會自動安裝 hello SQL Server IaaS 代理程式延伸模組。 如果您需要以手動方式是在其中一個這些 SQL Server Vm 上的 tooreinstall hello 延伸模組，請使用下列 PowerShell 命令的 hello:

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

它也是可能 tooinstall hello SQL Server IaaS 代理程式延伸模組僅作業系統的 Windows Server 虛擬機器上。 只有當您也已在該機器上手動安裝 SQL Server 時，才支援此做法。 然後透過手動安裝 hello 延伸 hello 相同**組 AzureVMSqlServerExtension** PowerShell cmdlet。

> [!NOTE]
> 如果您手動安裝 SQL Server IaaS 代理程式延伸模組 hello 作業系統專用的 Windows Server VM 上，您不可以管理透過 hello Azure 入口網站的 hello SQL Server 組態設定。 在此情況下，您必須使用 PowerShell 來進行所有變更。

## <a name="status"></a>狀態
其中一種方式 tooverify hello 延伸模組已安裝的是 tooview hello 代理程式狀態在 hello Azure 入口網站中。 選取**所有設定**在 hello 虛擬機器刀鋒視窗中，並按一下**延伸**。 您應該會看見 hello **SQLIaaSExtension**列出的副檔名。

![Azure 入口網站中的 SQL Server IaaS 代理程式擴充功能](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

您也可以使用 hello **Get AzureVMSqlServerExtension** Azure Powershell cmdlet。

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

hello 前一個命令會確認 hello 代理程式已安裝，並提供一般狀態資訊。 您也可以使用下列命令的 hello 取得特定的狀態資訊自動備份和修補。

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a>移除
在 hello Azure 入口網站，您可以解除安裝 hello 延伸 hello hello 上的省略符號，即可**延伸**刀鋒視窗中的虛擬機器內容。 然後按一下 [刪除] 。

![解除安裝 SQL Server IaaS 代理程式延伸模組在 Azure 入口網站中的 hello](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

您也可以使用 hello**移除 AzureRmVMSqlServerExtension** Powershell cmdlet。

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a>後續步驟
開始使用其中一種 hello hello 延伸模組支援的服務。 如需詳細資訊，請參閱 hello 中參考的 hello 主題[支援服務](#supported-services)本文一節。

如需在 Azure 虛擬機器上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)。

