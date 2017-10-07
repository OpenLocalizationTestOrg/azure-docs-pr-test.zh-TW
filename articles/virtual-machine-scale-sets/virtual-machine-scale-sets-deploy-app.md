---
title: "aaaDeploy 上虛擬機器規模的應用程式設定"
description: "使用 Azure 虛擬機器擴展集延伸模組 toodepoy 應用程式。"
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a>在虛擬機器擴展集上部署您的應用程式

本文說明如何在 hello 時段 hello tooinstall 軟體設定不同的方式已佈建。

您可能會想 tooreview hello[小數位數設定的設計概觀](virtual-machine-scale-sets-design-overview.md)文件，其中描述一些 hello 虛擬機器擴展集所加諸的限制。

## <a name="capture-and-reuse-an-image"></a>擷取並重複使用映像

您可以使用您已為您的標尺的 Azure tooprepare 基底映像中設定虛擬機器。 此程序會在您可以在擴展集做為 hello 基底映像參考的儲存體帳戶中建立受管理的磁碟。 

下列步驟 hello:

1. 建立 Azure 虛擬機器
   * [Linux][linux-vm-create]
   * [Windows][windows-vm-create]

2. 遠端至 hello 虛擬機器，並自訂 hello 系統 tooyour 喜好。

   如果想要，您可以立即安裝應用程式。 不過，知道安裝您的應用程式現在，您可能會進行升級您的應用程式更複雜，因為您可能需要 tooremove 它第一次。 相反地，您可以使用此步驟 tooinstall 任何可能需要您的應用程式，例如特定執行階段或作業系統功能的必要條件。

3. 請遵循 hello 」 擷取機器 」 教學課程的[Linux] [ linux-vm-capture]或[Windows][windows-vm-capture]。

4. 建立[虛擬機器擴展集][ vmss-create] hello 與映像 hello 上一個步驟中所擷取的 URI。

如需磁碟的詳細資訊，請參閱[受控磁碟概觀](../virtual-machines/windows/managed-disks-overview.md)和[使用連結的資料磁碟](virtual-machine-scale-sets-attached-disks.md)。

## <a name="install-when-hello-scale-set-is-provisioned"></a>Hello 規模調整集合已佈建時，安裝

虛擬機器延伸模組就會套用 tooa 虛擬機器規模集。 透過虛擬機器擴充功能，您可以自訂 hello 虛擬機器擴展集做為整個群組內。 如需擴充功能的詳細資訊，請參閱[虛擬機器擴充功能](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

視您的作業系統為 Linux 或 Windows 而定，有三個主要延伸模組可供您使用。

### <a name="windows"></a>Windows

Windows 作業系統，請使用其中一個 hello**自訂指令碼 v1.8**擴充功能或 hello **PowerShell DSC**延伸模組。

#### <a name="custom-script"></a>Custom Script

hello 自訂指令碼延伸執行指令碼 hello 規模集中的每個虛擬機器執行個體。 組態檔或變數，指出哪些檔案會下載的 toohello 虛擬機器，然後再執行哪些命令。 如需範例可以使用這個 toorun 安裝程式、 指令碼、 批次檔，任何可執行檔。

PowerShell 會基於 hello 設定使用雜湊表。 這個範例會設定 hello 自訂指令碼延伸 toorun 安裝 IIS 的 PowerShell 指令碼。

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>使用 hello`-ProtectedSetting`切換可能包含機密資訊的任何設定。

---------


Azure CLI hello 設定使用的 json 檔案。 這個範例會設定 hello 自訂指令碼延伸 toorun 安裝 IIS 的 PowerShell 指令碼。 儲存下列 json 檔案儲存為 hello _settings.json_。

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

然後，執行下列 Azure CLI 命令。

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>使用 hello`--protected-settings`切換可能包含機密資訊的任何設定。

### <a name="powershell-dsc"></a>PowerShell DSC

您可以使用 PowerShell DSC toocustomize hello 小數位數組 vm 執行個體。 hello **DSC**延伸模組所發行**Microsoft.Powershell**部署，並在每個虛擬機器執行個體上執行提供的 hello DSC 設定。 組態檔或變數會告知 hello 延伸其中*.zip*是封裝，以及哪些_指令碼函式_組合 toorun。

PowerShell 會基於 hello 設定使用雜湊表。 下列範例會部署 DSC 封裝以安裝 IIS。

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>使用 hello`-ProtectedSetting`切換可能包含機密資訊的任何設定。

-----------

Azure CLI 會使用 json hello 設定。 下列範例會部署 DSC 封裝以安裝 IIS。 儲存下列 json 檔案儲存為 hello _settings.json_。

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

然後，執行下列 Azure CLI 命令。

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>使用 hello`--protected-settings`切換可能包含機密資訊的任何設定。

### <a name="linux"></a>Linux

Linux 可以使用任一 hello**自訂指令碼 v2.0**擴充功能或使用**雲端 init**期間建立。

自訂指令碼是一種簡單的延伸，下載檔案 toohello 虛擬機器執行個體，並在執行命令。

#### <a name="custom-script"></a>Custom Script

儲存下列 json 檔案儲存為 hello _settings.json_。

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

請使用現有的虛擬機器規模集的這個延伸模組 tooan hello Azure CLI tooadd。 Hello 標尺每個虛擬機器設定自動執行 hello 延伸模組。

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>使用 hello`--protected-settings`切換可能包含機密資訊的任何設定。

#### <a name="cloud-init"></a>Cloud-Init

建立 hello 規模集時，會使用雲端 Init。 首先，建立名為本機檔案_雲端 init.txt_和加入組態 tooit。 例如，請參閱[此 gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)

設定使用 hello Azure CLI toocreate 小數位數。 hello`--custom-data`欄位可接受 hello 雲端初始化指令碼檔案名稱。

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a>如何管理應用程式更新？

如果您部署您的應用程式，透過擴充功能時，改變 hello 在某些方面的延伸模組定義。 這項變更會導致 hello 延伸 toobe 重新部署 tooall 虛擬機器執行個體。 項目**必須**變更有關 hello 擴充功能，例如重新命名參考的檔案，否則 Azure hello 延伸模組不再顯示已變更的作用。

如果您的作業系統映像到法式 hello 應用程式，使用自動的部署管線的應用程式更新。 設計您的架構 toofacilitate 快速交換至生產環境中設定預備標尺。 這種方法的理想範例為 hello [Azure Spinnaker 驅動程式工作](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/)。

[Packer](https://www.packer.io/)和[Terraform](https://www.terraform.io/)支援 Azure 資源管理員，讓您可以定義您的映像 」 做為程式碼 」，並建置在 Azure 中，然後使用您規模集中的 hello VHD。 不過，這麼做對 Marketplace 映像會造成問題，其中延伸模組/自訂指令碼會變得更加重要，因為您不是直接從 Marketplace 操縱位元。

## <a name="what-happens-when-a-scale-set-scales-out"></a>當擴展集相應放大時，會發生什麼情況？
當您新增一或多個虛擬機器 tooa 規模集時，會自動安裝 hello 應用程式。 範例 hello 規模調整集合，如果有定義的擴充功能，它們執行新的虛擬機器上每次建立時。 如果 hello 規模調整集合為基礎的自訂映像，任何新的虛擬機器是一份 hello 來源的自訂映像。 如果 hello 小數位數組虛擬機器是容器主機，您可能在自訂指令碼延伸必須啟動程式碼 tooload hello 容器。 或者，延伸模組可以安裝會向叢集 Orchestrator (例如 Azure Container Service) 註冊的代理程式。


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a>如何在各個更新網域推出 OS 更新？
假設您想要 tooupdate 作業系統映像，同時保留 hello 虛擬機器擴展集執行。 PowerShell 和 hello Azure CLI 可以更新 hello 虛擬機器映像，一部虛擬機器一次。 hello[升級虛擬機器擴展集](./virtual-machine-scale-sets-upgrade-scale-set.md)發行項也會提供進一步資訊的選擇有哪些可用 tooperform 作業系統升級各虛擬機器規模集。

## <a name="next-steps"></a>後續步驟

* [使用 PowerShell toomanage 規模集。](virtual-machine-scale-sets-windows-manage.md)
* [建立擴展集範本。](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

