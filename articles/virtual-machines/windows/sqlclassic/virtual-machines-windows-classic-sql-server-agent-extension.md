---
title: "aaaAutomate SQL Vm （傳統） 上的管理工作 |Microsoft 文件"
description: "本主題描述如何 toomanage hello SQL Server 代理程式延伸特定的 SQL Server 系統管理工作自動化。 其中包括自動備份、自動修補和 Azure 金鑰保存庫整合。 本主題使用 hello 傳統部署模式。"
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a>自動化管理工作在 Azure 虛擬機器以 hello SQL Server 代理程式延伸模組 （傳統）
> [!div class="op_single_selector"]
> * [資源管理員](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [傳統](../classic/sql-server-agent-extension.md)
> 
>
 
hello SQL Server IaaS 代理程式延伸模組 (SQLIaaSAgent) 會執行於 Azure 虛擬機器 tooautomate 系統管理工作。 本主題提供支援 hello 延伸模組，以及安裝、 狀態及移除指示 hello 服務的概觀。

> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 請參閱這篇文章，tooview hello 資源管理員版本[SQL Server Agent 擴充功能的 SQL Server Vm 資源管理員](../sql/virtual-machines-windows-sql-server-agent-extension.md)。

## <a name="supported-services"></a>支援的服務
hello SQL Server IaaS 代理程式延伸模組支援下列管理工作的 hello:

| 系統管理功能 | 說明 |
| --- | --- |
| **SQL 自動備份** |會自動將 hello 預設執行個體的 SQL Server hello VM 中的所有資料庫的備份排程 hello。 如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 自動備份 (傳統)](../classic/sql-automated-backup.md)。 |
| **SQL 自動修補** |設定維護間隔期間哪些更新將放置的 tooyour VM 可以採取，如此您就不必在您的工作負載尖峰期間更新。 如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 自動修補 (傳統)](../classic/sql-automated-patching.md)。 |
| **Azure 金鑰保存庫整合** |可讓您 tooautomatically 上安裝及設定 Azure 金鑰保存庫 SQL Server VM。 如需詳細資訊，請參閱 [在 Azure VM 上設定 SQL Server 的 Azure 金鑰保存庫整合 (傳統)](../classic/ps-sql-keyvault.md)。 |

## <a name="prerequisites"></a>必要條件
SQL Server IaaS 代理程式延伸模組在您的 VM 上需求 toouse hello:

### <a name="operating-system"></a>作業系統：
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

### <a name="sql-server-versions"></a>SQL Server 版本：
* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

### <a name="azure-powershell"></a>Azure PowerShell：
[下載並設定最新 Azure PowerShell 命令 hello](/powershell/azure/overview)。

啟動 Windows PowerShell，並將它連接 tooyour Azure 訂用帳戶以 hello **Add-azureaccount**命令。

    Add-AzureAccount

如果您有多個訂閱，使用**Select-azuresubscription** tooselect hello 訂用帳戶包含您的目標傳統 VM。

    Select-AzureSubscription -SubscriptionName <subscriptionname>

此時，您可以取得一份 hello 傳統虛擬機器和其相關聯的服務名稱與 hello **Get-azurevm**命令。

    Get-AzureVM

## <a name="installation"></a>安裝
對於傳統的 Vm，您必須使用 PowerShell tooinstall hello SQL Server IaaS 代理程式延伸模組，並設定相關聯的服務。 使用 hello**組 AzureVMSqlServerExtension** PowerShell cmdlet tooinstall hello 延伸模組。 例如，hello 下列命令會安裝在 Windows Server VM （傳統） 上的 hello 延伸模組並將它"SQLIaaSExtension"。

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

如果您更新 toohello hello SQL IaaS 代理程式延伸模組最新版本，您必須更新 hello 擴充功能之後，重新虛擬機器。

> [!NOTE]
> 傳統的虛擬機器沒有選項 tooinstall，並設定 hello SQL IaaS 代理程式延伸模組，透過 hello 入口網站。
> 
> 

## <a name="status"></a>狀態
其中一種方式 tooverify hello 延伸模組已安裝的是 tooview hello 代理程式狀態在 hello Azure 入口網站中。 選取列在 hello 虛擬機器刀鋒視窗中，虛擬機器，然後按一下上**延伸**。 您應該會看見 hello **SQLIaaSAgent**列出的副檔名。

![Azure 入口網站中的 SQL Server IaaS 代理程式擴充功能](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

您也可以使用 hello **Get AzureVMSqlServerExtension** Azure Powershell cmdlet。

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a>移除
在 hello Azure 入口網站，您可以解除安裝 hello 延伸 hello hello 上的省略符號，即可**延伸**刀鋒視窗中的虛擬機器內容。 然後按一下 [解除安裝]。

![解除安裝 SQL Server IaaS 代理程式延伸模組在 Azure 入口網站中的 hello](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

您也可以使用 hello**移除 AzureVMSqlServerExtension** Powershell cmdlet。

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a>後續步驟
開始使用其中一種 hello hello 延伸模組支援的服務。 如需詳細資訊，請參閱 hello 中參考的 hello 主題[支援服務](#supported-services)本文一節。

如需在 Azure 虛擬機器上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。

