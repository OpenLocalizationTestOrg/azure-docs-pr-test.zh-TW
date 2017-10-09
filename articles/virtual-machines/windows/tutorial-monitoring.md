---
title: "aaaAzure 監視和 Windows 虛擬機器 |Microsoft 文件"
description: "教學課程 - 使用 Azure PowerShell 監視 Windows 虛擬機器"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a>使用 Azure PowerShell 監視 Windows 虛擬機器

Azure 監視會使用代理程式 toocollect 開機和 Azure Vm 的效能資料，將此資料儲存在 Azure 儲存體，讓它可以透過入口網站、 hello Azure PowerShell 模組，以及 hello Azure CLI 存取。 在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 啟用 VM 上的開機診斷
> * 檢視開機診斷
> * 檢視 VM 主機計量
> * 安裝 hello 診斷延伸模組
> * 檢視 VM 計量
> * 建立警示
> * 設定進階監視

本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。 執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。 如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。

在本教學課程 toocomplete hello 範例中的，您必須擁有現有的虛擬機器。 如有需要，這個[指令碼範例](../scripts/virtual-machines-windows-powershell-sample-create-vm.md)可以為您建立一部虛擬機器。 當使用 hello 教學課程時，取代 hello 資源群組、 VM 名稱和位置在需要時。

## <a name="view-boot-diagnostics"></a>檢視開機診斷

為 Windows 虛擬機器開機，hello 開機診斷代理程式會擷取可用於疑難排解用途的螢幕輸出。 此功能預設為啟用狀態。 hello 擷取的螢幕擷取畫面會儲存在 Azure 儲存體帳戶，也會建立預設。 

您可以取得 hello 開機診斷資料以 hello [Get AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata)命令。 在下列範例的 hello，開機診斷是下載的 toohello 根的 hello * c:\*磁碟機。 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a>檢視主機計量

在 Azure 中有 Windows VM 專用的主機 VM 與它互動。 度量自動和收集到的 hello 主機可以在 hello Azure 入口網站中檢視。

1. 在 hello Azure 入口網站，按一下 **資源群組**，選取**myResourceGroup**，然後選取**myVM** hello 資源清單中。
2. 按一下**度量**在 hello VM 刀鋒視窗中，，然後選取任何下 hello 主機計量**可用的度量**toosee hello 主機 VM 執行的方式。

    ![檢視主機計量](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a>安裝診斷擴充功能

hello 基本主機計量可供使用，但更細微的 toosee 和特定 VM 的度量，您 tooneed tooinstall hello Azure 診斷擴充功能在 hello VM 上。 hello Azure 診斷擴充功能可讓其他監視和診斷資料 toobe hello VM 從擷取。 您可以檢視這些效能度量，並依據 hello VM 執行的方式建立警示。 hello 診斷延伸模組會安裝透過 hello Azure 入口網站，如下所示：

1. 在 hello Azure 入口網站，按一下 **資源群組**，選取**myResourceGroup**，然後選取**myVM** hello 資源清單中。
2. 按一下 [診斷設定]。 hello 清單顯示*開機診斷*已經啟用 hello 前一節。 按一下核取方塊 hello*基本度量*。
3. 按一下 hello**啟用客體層級監視** 按鈕。

    ![檢視診斷計量](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a>檢視 VM 計量

您可以在 hello 檢視 hello VM 度量您檢視 hello 主機 VM 計量的相同方式：

1. 在 hello Azure 入口網站，按一下 **資源群組**，選取**myResourceGroup**，然後選取**myVM** hello 資源清單中。
2. toosee 如何 hello VM 正在執行中，按一下**度量**hello VM 刀鋒視窗中，且然後選取其中一個下 hello 診斷度量**可用的度量**。

    ![檢視 VM 計量](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a>建立警示

您可以根據特定效能計量來建立警示。 警示可能會使用的 toonotify 時的平均 CPU 使用率超過某個臨界值或可用的磁碟空間低於特定大小，例如。 警示會顯示在 hello Azure 入口網站，或可以透過電子郵件傳送。 您也可以在所產生的回應 tooalerts 觸發 Azure 自動化 runbook 或 Azure 邏輯應用程式。

hello 下列範例會建立警示的平均 CPU 使用量。

1. 在 hello Azure 入口網站，按一下 **資源群組**，選取**myResourceGroup**，然後選取**myVM** hello 資源清單中。
2. 按一下**警示規則**hello VM 刀鋒視窗，然後按一下**新增度量的警示**hello 的 hello 警示 刀鋒視窗的頂端。
4. 提供警示的 [名稱]，例如 myAlertRule。
5. tootrigger 警示時的 CPU 百分比超過五分鐘，1.0 會保留所有 hello 選取其他預設值。
6. （選擇性） 核取方塊 hello*電子郵件擁有者、 參與者與讀者*toosend 電子郵件通知。 hello 預設動作是 toopresent hello 入口網站中的通知。
7. 按一下 hello**確定** 按鈕。

## <a name="advanced-monitoring"></a>進階監視 

您可以使用 [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) (OMS) 對您的 VM 進行更進階的監視。 如果您尚未這麼做，可以註冊 Operations Management Suite 的[免費試用版](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial)。

當您擁有存取 toohello OMS 入口網站時，您可以在 hello 設定 刀鋒視窗上找到 hello 工作區的索引鍵和工作區識別碼。 使用 hello[組 AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand tootooadd hello OMS 擴充 toohello VM。 更新 hello 變數中的值如下範例 tooreflect hello 您 OMS 工作區金鑰和工作區識別碼。  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

您應該在幾分鐘之後, 會看到 hello hello OMS 工作區中的新 VM。 

![OMS 刀鋒視窗](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>後續步驟
在本教學課程中，您利用 Azure 資訊安全中心設定並檢閱 VM。 您已了解如何︰

> [!div class="checklist"]
> * 建立虛擬網路
> * 建立資源群組和 VM 
> * 啟用 hello VM 上的開機診斷功能
> * 檢視開機診斷
> * 檢視主機計量
> * 安裝 hello 診斷延伸模組
> * 檢視 VM 計量
> * 建立警示
> * 設定進階監視

前進 toohello 下一個教學課程的 toolearn 有關 Azure 資訊安全中心。

> [!div class="nextstepaction"]
> [管理 VM 安全性](./tutorial-azure-security.md)