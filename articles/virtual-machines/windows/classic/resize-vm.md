---
title: "aaaResize hello 傳統部署模型 Azure 中的 Windows VM |Microsoft 文件"
description: "調整 hello 傳統部署模型，使用 Azure Powershell 中建立 Windows 虛擬機器的大小。"
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a>調整 hello 傳統部署模型中建立 Windows VM 的大小
本文章將示範如何 tooresize Windows VM，在建立使用 Azure Powershell hello 傳統部署模型。

當考量 hello 能力 tooresize VM 時，可控制 hello 範圍大小可用 tooresize hello 虛擬機器的兩個概念。 hello 第一個概念是以您的 VM 部署的 hello 區域。 在區域中可用的 VM 大小 hello 清單是 hello hello Azure 區域 web 頁面的 [服務] 索引標籤下。 hello 第二個概念是 hello 目前裝載的 VM 的實體硬體。 hello 實體伺服器裝載的 Vm 中群組在一起的一般實體硬體的叢集。 變更 VM 大小的 hello 方法不同取決於 hello 想要新的 VM 大小支援 hello 硬體叢集目前裝載的 hello VM。

> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 您也可以[hello Resource Manager 部署模型中建立 VM 調整](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="add-your-account"></a>新增帳戶
您必須設定 Azure PowerShell toowork 使用傳統的 Azure 資源。 請遵循以下 tooconfigure Azure PowerShell toomanage 傳統資源的 hello 步驟。

1. 在 hello PowerShell 提示字元中輸入`Add-AzureAccount`按一下**Enter**。 
2. 輸入您 Azure 訂用帳戶相關聯的 hello 電子郵件地址，然後按一下**繼續**。 
3. 輸入 hello 您帳戶的密碼。 
4. 按一下 [ **登入**]。 

## <a name="resize-in-hello-same-hardware-cluster"></a>調整在 hello 相同硬體叢集
tooresize VM tooa 大小可用在 hello 硬體叢集中裝載 hello VM，執行下列步驟的 hello。

1. 執行下列 PowerShell 命令裝載 hello 雲端服務可包含的 hello 硬體叢集中可用的 toolist hello VM 大小 hello VM hello。
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. 執行下列命令 tooresize hello VM hello。
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a>在新的硬體叢集上調整大小
tooresize VM tooa 大小不適用於裝載的 hello 硬體叢集 hello VM，hello 雲端服務和 hello 雲端服務中的所有 Vm 都必須重新建立。 每個雲端服務被裝載在單一硬體叢集上，因此 hello 雲端服務中的所有 Vm 都必須支援硬體叢集的大小。 hello 下列步驟將說明如何刪除，然後重新建立 VM tooresize hello 雲端服務。

1. 執行下列 PowerShell 命令 toolist hello VM 大小可用 hello 區域中的 hello。 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. 記下包含調整大小的 hello VM toobe hello 雲端服務中每個 VM 的所有組態設定。 
3. 刪除 hello hello 選項 tooretain hello 磁碟選取每個 VM 的雲端服務中的所有 Vm。
4. 重新建立 hello VM toobe 調整使用 hello 所需的 VM 大小。
5. 重新建立所有已使用 hello 硬體叢集現在裝載 hello 雲端服務中可用的 VM 大小的 hello 雲端服務中的其他 Vm。

您可以在[這裡](https://github.com/Azure/azure-vm-scripts)找到刪除雲端服務並使用新 VM 大小重新建立雲端服務的範例指令碼。 

## <a name="next-steps"></a>後續步驟
* [調整大小 hello Resource Manager 部署模型中建立的 VM](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

