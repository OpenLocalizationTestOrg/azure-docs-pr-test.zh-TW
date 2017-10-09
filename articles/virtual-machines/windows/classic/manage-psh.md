---
title: "aaaManage 您的虛擬機器使用 Azure PowerShell |Microsoft 文件"
description: "了解您可以使用中管理虛擬機器的 tooautomate 工作的命令。"
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a>使用 Azure PowerShell 管理您的虛擬機器
> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 使用 hello 資源管理員模型的一般 PowerShell 命令，請參閱[這裡](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

可以使用 Azure PowerShell cmdlet 來自動化執行每日 toomanage Vm 的許多工作。 這篇文章提供您命令範例更簡單的工作和連結 tooarticles 顯示 hello 指令更複雜的工作。

> [!NOTE]
> 如果您並未安裝及設定 Azure PowerShell，您可以在 hello 文件中取得指示[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。
> 
> 

## <a name="how-toouse-hello-example-commands"></a>如何 toouse hello 範例命令
您將需要的 tooreplace hello 中的 hello 文字的某些命令搭配適用於您環境的文字。 hello < 和 > 符號表示您需要 tooreplace 的文字。 當您取代 hello 文字時，移除 hello 符號，但讓 hello 引號留在原處。

## <a name="get-a-vm"></a>取得 VM
這是您會經常使用的基本工作。 使用 VM 的 tooget 資訊、 在 VM 上執行工作或取得輸出 toostore 在變數中。

tooget 資訊 hello VM，執行下列命令，取代 hello 加上引號，包括 hello < 和 > 字元的所有項目：

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

toostore hello 輸出在 $vm 變數中，執行：

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a>登入 tooa Windows 架構的 VM
執行以下命令：

> [!NOTE]
> 您可以從 hello 顯示 hello 取得 hello 虛擬機器和雲端服務名稱**Get-azurevm**命令。
> 
> $svcName ="<cloud service name>"$vmName ="<virtual machine name>"$localPath ="< 磁碟機和資料夾位置 toostore hello 下載 RDP 檔案，範例： c:\temp >"$localFile = $localPath +"\" + $vmname +".rdp 」 Get-azureremotedesktopfile-ServiceName $svcName-命名 $vmName LocalPath $localFile-啟動
> 
> 

## <a name="stop-a-vm"></a>停止 VM
請執行這個命令：

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> 使用虛擬 IP (VIP) 的 hello 雲端服務，以便在此參數 tookeep hello hello 該雲端服務中的最後一個 VM。 <br><br> 如果您使用 hello StayProvisioned 參數時，您將仍然要支付 hello VM。
> 
> 

## <a name="start-a-vm"></a>啟動 VM
請執行這個命令：

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a>連接資料磁碟
這項工作需要幾個步驟。 首先，您可以使用 hello * * * 新增-AzureDataDisk * * * cmdlet tooadd hello 磁碟 toohello $vm 物件。 然後，您使用**Update-azurevm** hello VM cmdlet tooupdate hello 設定。

您還需要 toodecide 是否 tooattach 新磁碟或其中所包含的資料。 為新的磁碟，hello 命令會建立 hello.vhd 檔案，並將它附加。

tooattach 新磁碟時，執行下列命令：

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

tooattach 現有的資料磁碟，執行下列命令：

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

從現有的.vhd 檔案在 blob 儲存體，tooattach 資料磁碟會執行下列命令：

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a>建立以 Windows 為基礎的 VM
新視窗為基礎的虛擬機器在 Azure 中，使用中的 hello 指示 toocreate[使用 Azure PowerShell toocreate 並預先設定 Windows 型虛擬機器](create-powershell.md)。 此主題會逐步引導您透過 hello 建立的 Azure PowerShell 命令設定，會建立可以預先設定的 windows VM:

* 具有 Active Directory 網域成員資格。
* 具有額外的磁碟。
* 成為現有負載平衡集的成員。
* 具有靜態 IP 位址。

