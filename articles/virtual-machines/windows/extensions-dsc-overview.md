---
title: "aaaDesired 狀態設定為 Azure 概觀 |Microsoft 文件"
description: "PowerShell 預期狀態設定為使用 hello Microsoft Azure 延伸模組處理常式的概觀。 包括必要條件、架構、Cmdlet..."
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: b0337a2f1124f35e5e40c1478bd7530427e59d44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a>簡介 toohello Azure Desired State Configuration 延伸模組處理常式
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

hello Azure VM 代理程式和相關聯的延伸模組是 hello Microsoft Azure 基礎結構服務的一部分。 VM 擴充功能是擴充 hello VM 功能及簡化各種 VM 管理操作的軟體元件。 例如，hello VMAccess 擴充功能可以使用的 tooreset 系統管理員密碼或 hello 自訂指令碼延伸可以是使用的 tooexecute hello VM 上的指令碼。

本文介紹 hello PowerShell 預期狀態設定 (DSC) 的延伸模組的 Azure Vm 中當做 hello Azure PowerShell SDK 的一部分。 您可以使用新的 cmdlet tooupload，並以 hello PowerShell DSC 擴充功能已啟用 Azure VM 上套用的 PowerShell DSC 設定。 PowerShell DSC tooenact hello hello PowerShell DSC 擴充功能呼叫收到 hello VM 上的 DSC 設定。 這項功能也會透過 hello Azure 入口網站提供的。

## <a name="prerequisites"></a>必要條件
**本機電腦**toointeract 與 hello Azure VM 延伸模組，您需要 toouse 任一 hello Azure 入口網站或 hello Azure PowerShell SDK。 

**客體代理程式**hello hello DSC 組態所設定的 Azure VM 需要 toobe Windows Management Framework (WMF) 4.0 或是 5.0 支援的作業系統。 hello 支援的 OS 版本的完整清單位於 hello [DSC 延伸模組版本歷程記錄](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/)。

## <a name="terms-and-concepts"></a>詞彙和概念
本指南會假設您熟悉下列概念的 hello:

組態 - DSC 組態文件。 

節點 - DSC 組態的目標。 在本文件中，「 節點 」 一律指的是 tooan Azure VM。

組態資料 - 包含組態之環境資料的 .psd1 檔案

## <a name="architectural-overview"></a>架構概觀
hello Azure DSC 延伸模組會使用 hello Azure VM 代理程式架構 toodeliver、 制定，及報告 Azure Vm 上執行的 DSC 設定。 hello DSC 延伸模組需要包含至少一個組態文件.zip 檔案，並提供一組參數透過 hello Azure PowerShell SDK 或 hello Azure 入口網站。

當第一次呼叫 hello 延伸 hello 時，它會執行安裝程序。 這個程序會使用下列邏輯 hello hello Windows Management Framework (WMF) 的版本：

1. 如果 hello Azure VM 的作業系統是 Windows Server 2016，會不採取任何動作。 Windows Server 2016 已安裝的 PowerShell hello 最新版本。
2. 如果 hello`wmfVersion`屬性已指定，該版的 hello WMF 已安裝，除非它是與 hello VM 之 OS 不相容。
3. 如果沒有`wmfVersion`屬性已指定，hello 最適用 hello WMF 已安裝的版本。

Hello WMF 安裝需要重新開機。 重新開機後，hello 擴充功能下載 hello.zip 檔案中 hello 指定`modulesUrl`屬性。 如果這個位置是在 Azure blob 儲存體，SAS 權杖可以指定在 hello`sasToken`屬性 tooaccess hello 檔案。 Hello.zip 會下載並解壓縮之後，hello 組態中定義的函式`configurationFunction`執行 toogenerate hello MOF 檔案。 然後執行 hello 延伸模組`Start-DscConfiguration -Force`在 hello 產生 MOF 檔案。 hello 擴充功能會擷取輸出，並將它寫出 toohello Azure 狀態的通道。 從這個點上 hello DSC LCM 處理監視及修正像平常一樣。 

## <a name="powershell-cmdlets"></a>PowerShell Cmdlet
PowerShell 指令程式可使用 Azure 資源管理員或 hello 傳統部署模型 toopackage、 發行和監視 DSC 延伸模組部署。 hello 列出下列 cmdlet hello 傳統部署模組，但是"Azure"取代"AzureRm"toouse hello Azure Resource Manager 模型。 例如，`Publish-AzureVMDscConfiguration`使用 hello 傳統部署模型，其中`Publish-AzureRmVMDscConfiguration`使用 Azure 資源管理員。 

`Publish-AzureVMDscConfiguration`接受在組態檔中、 掃描相依的 DSC 資源，然後建立包含 hello 組態和 DSC 資源所需的 tooenact hello 組態的.zip 檔案。 它也可以建立 hello 封裝使用本機 hello`-ConfigurationArchivePath`參數。 否則，它會發行 hello.zip 檔案 tooAzure blob 儲存體，並保護其的安全與 SAS 權杖。

此 cmdlet 建立 hello.zip 檔案根目錄 hello hello 保存資料夾有 hello.ps1 組態指令碼。 資源擁有 hello 模組資料夾放在 hello 保存資料夾中。 

`Set-AzureVMDscExtension`插入 hello 設定 hello PowerShell DSC 擴充功能所需的 VM 組態物件。 在 hello 傳統部署模型，hello VM 變更必須套用的 tooan Azure VM 與`Update-AzureVM`。 

`Get-AzureVMDscExtension`擷取特定 VM hello DSC 延伸模組狀態。 

`Get-AzureVMDscExtensionStatus`擷取 hello hello DSC 延伸模組處理常式所制定的 hello DSC 設定狀態。 此動作可在單一 VM 或一組 VM 上執行。

`Remove-AzureVMDscExtension`移除指定的虛擬機器中的 hello 延伸模組處理常式。 此 cmdlet 會**不**移除 hello 設定、 解除安裝 WMF，hello 或變更 hello 虛擬機器上的 hello 套用設定。 它只會移除 hello 延伸模組處理常式。 

**ASM 和 Azure Resource Manager Cmdlet 的主要差異**

* Azure Resource Manager Cmdlet 是同步的。 ASM Cmdlet 具備非同步性。
* ResourceGroupName、VMName、ArchiveStorageAccountName、Version 及 Location 皆為 Azure Resource Manager 中的必要參數。
* ArchiveResourceGroupName 是 Azure Resource Manager 的新選擇性參數。 當您儲存體帳戶所屬 tooa 不同的資源群組的其中一個 hello 建立 hello 虛擬機器的位置時，您可以指定這個參數。
* ConfigurationArchive 在 Azure Resource Manager 中稱為 ArchiveBlobName
* ContainerName 在 Azure Resource Manager 中稱為 ArchiveContainerName
* StorageEndpointSuffix 在 Azure Resource Manager 中稱為 ArchiveStorageEndpointSuffix
* 已加入 tooAzure 自動更新 hello 延伸模組處理常式 toohello 最新版本與版本，並可供使用的資源管理員 tooenable hello AutoUpdate 交換器。 請注意，這個參數會有 hello 潛在 toocause 重新開機的 hello hello WMF 發行新版本的 VM。 

## <a name="azure-portal-functionality"></a>Azure 入口網站功能
瀏覽 tooa VM。 在 [設定] -> [一般] 底下，按一下 [擴充功能]。 系統會建立新窗格。 按一下 [加入]，然後選取 [PowerShell DSC]。

hello 入口網站需要輸入。
**組態模組或指令碼**︰這是必要欄位。 需要.ps1 檔案包含設定指令碼或 hello.zip 內的模組資料夾中的所有依存資源與 hello 根目錄.ps1 設定指令碼的.zip 檔案。 它可以建立以 hello `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` hello Azure PowerShell SDK 中包含的 cmdlet。 hello.zip 檔案上傳到您使用者的 blob 儲存體受到 SAS 權杖。 

**組態資料 PSD1 檔案**︰這是選擇性欄位。 如果您的組態需要.psd1 的組態資料檔，請使用此欄位 tooselect 它並將它上傳 tooyour 使用者 blob 儲存體，所以保護由 SAS 權杖。 

**組態的模組完整名稱**：.ps1 檔案可以有多個組態函數。 輸入 hello hello 設定.ps1 指令碼後面接著名稱 '\'和 hello hello 設定函式名稱。 例如，如果.ps1 指令碼有 hello 名稱"configuration.ps1"hello 組態是"IisInstall 」，您會輸入：`configuration.ps1\IisInstall`

**組態引數**: hello 的設定函式會採用引數，如果在這裡 hello 格式輸入它們`argumentName1=value1,argumentName2=value2`。 請注意，此格式與透過 PowerShell Cmdlet 或 Resource Manager 範本接受組態引數的方式所採用的格式不同。 

## <a name="getting-started"></a>開始使用
hello Azure DSC 延伸模組會在 DSC 設定文件，並制定這些 Azure Vm 上。 以下是簡單的組態範例。 以 "IisInstall.ps1" 的名稱將它儲存在本機：

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

hello hello 遵循步驟進行 hello IisInstall.ps1 指令碼指定的 VM、 執行 hello 組態，並回報狀態。
###<a name="classic-model"></a>傳統模型
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish hello configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set hello VM toorun hello DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update hello configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a>Azure Resource Manager 模型

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish hello configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set hello VM toorun hello DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a>記錄
記錄檔位於︰

C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[版本號碼]

## <a name="next-steps"></a>後續步驟
如需有關 PowerShell DSC[造訪 hello PowerShell 文件中心](https://msdn.microsoft.com/powershell/dsc/overview)。 

檢查 hello [hello DSC 延伸模組的 Azure Resource Manager 範本](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 

toofind 額外的功能，您可以使用 PowerShell DSC[瀏覽 hello PowerShell 資源庫](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0)的多個 DSC 資源。

如需將敏感性參數傳遞至設定的詳細資訊，請參閱[管理認證安全地與 hello DSC 延伸模組處理常式](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
