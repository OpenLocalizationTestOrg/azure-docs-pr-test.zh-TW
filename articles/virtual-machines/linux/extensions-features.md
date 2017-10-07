---
title: "aaaVirtual 適用於 Linux 機器擴充功能和功能 |Microsoft 文件"
description: "了解哪些擴充功能適用於 Azure 虛擬機器，並依它們提供或改善的內容來分組。"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a>適用於 Linux 的虛擬機器擴充功能和功能

「Azure 虛擬機器」擴充功能是小型的應用程式，可在「Azure 虛擬機器」上提供部署後設定及自動化工作。 例如，如果虛擬機器需要的軟體安裝、 防毒保護或 Docker 組態，VM 延伸模組可以是使用的 toocomplete 這些工作。 Azure VM 延伸模組可以使用 hello Azure CLI、 PowerShell、 Azure 資源管理員範本，來執行，與 hello Azure 入口網站。 擴充功能可以與新的虛擬機器部署搭配，或是在任何現有的系統上執行。

本文件概述的 VM 擴充功能，使用 Azure VM 擴充功能和指引 toodetect，如何管理和移除 VM 擴充功能上的必要條件。 本文件提供通用的資訊，因為有許多可用的 VM 擴充功能，每個都有唯一可能的組態。 在每個文件特定 toohello 個別擴充功能，可以找到延伸模組的特定詳細資料。

## <a name="use-cases-and-samples"></a>使用案例和範例

有數個不同的 Azure VM 擴充功能可供使用，各有特定使用案例。 部分範例如下：

- 適用於使用 hello DSC 延伸模組，適用於 Linux 的 PowerShell 預期狀態設定 tooa 虛擬機器。 如需詳細資訊，請參閱 [Azure 期望狀態組態擴充功能簡介](https://github.com/Azure/azure-linux-extensions/tree/master/DSC)。
- 設定虛擬機器以 hello Microsoft 監視代理程式 VM 擴充功能的監視。 如需詳細資訊，請參閱[如何 toomonitor Linux VM](tutorial-monitoring.md)。
- 設定監視 Azure 基礎結構以 hello Datadog 延伸模組。 如需詳細資訊，請參閱 hello [Datadog 部落格](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/)。
- 使用 hello Docker VM 擴充功能的 Azure 虛擬機器上設定 Docker 主機。 如需詳細資訊，請參閱 [Docker VM 擴充功能](dockerextension.md)。

此外 tooprocess 特定延伸項目，自訂指令碼延伸模組是適用於 Windows 和 Linux 虛擬機器。 hello 適用於 Linux 的自訂指令碼擴充功能可讓虛擬機器上執行任何 Bash 指令碼 toobe。 自訂指令碼對於設計需要超過原生 Azure 工具可提供之設定的 Azure 部署很有用。 如需詳細資訊，請參閱 [Linux VM 自訂指令碼延伸模組](extensions-customscript.md)。


## <a name="prerequisites"></a>必要條件

每個虛擬機器擴充功能可能有它自己的必要條件組。 比方說，hello Docker VM 擴充功能包含受支援的 Linux 散發套件的必要的元件。 Hello 延伸模組特定文件會詳細說明個別的擴充功能的需求。

### <a name="azure-vm-agent"></a>Azure VM 代理程式

hello Azure VM 代理程式管理的 Azure 虛擬機器與 hello Azure 網狀架構控制器之間的互動。 hello VM 代理程式會負責部署及管理 Azure 虛擬機器，包括執行 VM 擴充功能的許多功能層面。 hello Azure VM 代理程式會預先安裝在 Azure Marketplace 映像，並手動安裝支援的作業系統上。

如需有關支援的作業系統和安裝指示，請參閱 [Azure 虛擬機器代理程式](../windows/classic/agents-and-extensions.md)。

## <a name="discover-vm-extensions"></a>探索 VM 擴充功能

有許多不同的 VM 擴充功能可供與「Azure 虛擬機器」搭配使用。 完整的清單中，執行下列命令以 hello Azure CLI、 hello 範例位置取代為您選擇的 hello 位置 hello toosee。

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a>執行 VM 延伸模組

Azure 虛擬機器擴充功能可以執行在現有的虛擬機器，您需要 toomake 組態變更或修復已部署的 VM 上的連線時很有用。 VM 擴充功能也可以搭配 Azure Resource Manager 範本部署。 使用具有 Resource Manager 範本中的擴充功能，可以部署及設定 Azure 虛擬機器而不需要部署後介入。

hello 下列方法可以是使用的 toorun 針對現有的虛擬機器擴充功能。

### <a name="azure-cli"></a>Azure CLI

Azure 虛擬機器擴充功能可以針對現有的虛擬機器執行使用 hello`az vm extension set`命令。 這個範例會針對虛擬機器執行 hello 自訂指令碼延伸。

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

hello 指令碼會產生輸出類似 toohello 下列文字：

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a>Azure 入口網站

VM 擴充功能可以透過 Azure 入口網站 hello 套用的 tooan 現有虛擬機器。 toodo，選取 hello 虛擬機器，選擇**延伸**，然後按一下**新增**。 選取您想要從 hello 可用延伸清單，並遵循 hello 精靈中的 hello 指示 「 hello 」 延伸模組。

hello 下列影像顯示 hello hello Linux 自訂指令碼擴充功能，從 hello Azure 入口網站安裝。

![安裝自訂指令碼延伸模組](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a>Azure 資源管理員範本

VM 擴充功能與 hello hello 範本部署執行，而且可以加入的 tooan Azure Resource Manager 範本。 當您使用範本部署擴充功能時，可以建立完全設定的 Azure 部署。 例如，下列 JSON hello 取自 Resource Manager 範本。 hello 範本將一組負載平衡虛擬機器和 Azure SQL database，部署，並在每個 VM 上安裝.NET Core 應用程式。 hello VM 延伸模組會負責 hello 軟體安裝。

如需詳細資訊，請參閱完整的 hello [Resource Manager 範本](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)。

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

如需詳細資訊，請參閱[編寫 Azure Resource Manager 範本](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions)。

## <a name="secure-vm-extension-data"></a>安全的 VM 擴充功能資料

如果您執行的 VM 延伸模組，可能需要 tooinclude 機密資訊，例如認證、 儲存體帳戶名稱，以及儲存體帳戶存取金鑰。 許多 VM 擴充功能包含受保護的組態加密資料，並只將它解密 hello 目標虛擬機器內。 每個擴充功能有特定受保護的組態結構描述，並每個都會在擴充功能特定文件中詳細說明。

hello 下列範例會顯示適用於 Linux 的 hello 自訂指令碼延伸執行個體。 請注意該 hello 命令 tooexecute 包含一組認證。 在此範例中，將不會加密 hello 命令 tooexecute。


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

移動 hello**命令 tooexecute**屬性 toohello**保護**組態保護 hello 執行字串。

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a>針對 VM 擴充功能進行疑難排解

每個 VM 擴充功能可能會有疑難排解步驟特定 toohello 延伸模組。 例如，當您使用 hello 自訂指令碼擴充功能，指令碼執行詳細資料可以找到本機 hello hello 延伸模組執行所在的虛擬機器上。 所有擴充功能特定的疑難排解步驟都會在擴充功能特定文件中詳述。

下列疑難排解步驟的 hello 套用 tooall 虛擬機器擴充功能。

### <a name="view-extension-status"></a>檢視擴充功能狀態

已執行的虛擬機器的虛擬機器擴充功能之後，請使用下列 Azure CLI 命令 tooreturn 延伸模組狀態的 hello。 請以您自己的值取代範例參數名稱。

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

hello 輸出看起來類似下列文字的 hello:

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

也可以在 hello Azure 入口網站中找到延伸模組的執行狀態。 tooview hello 狀態的延伸，選取 hello 虛擬機器，選擇**延伸**，並選取 hello 所需的擴充功能。

### <a name="rerun-a-vm-extension"></a>重新執行 VM 擴充功能

可能是虛擬機器擴充功能必須 toobe 的情況下重新執行。 您可以藉由移除它，然後重新執行您選擇的執行方法 hello 延伸模組執行擴充功能。 擴充功能，執行下列命令以 hello Azure CLI hello tooremove。 請以您自己的值取代範例參數名稱。

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

您可以使用 hello hello Azure 入口網站中的步驟，以移除擴充功能：

1. 選取虛擬機器。
2. 選擇**擴充功能**。
3. 選取所需的 hello 擴充功能。
4. 選擇**解除安裝**。

## <a name="common-vm-extension-reference"></a>常見的 VM 擴充功能參考
| 擴充功能名稱 | 說明 | 詳細資訊 |
| --- | --- | --- |
| Linux 的自訂指令碼擴充功能 |對「Azure 虛擬機器」執行指令碼 |[Linux 的自訂指令碼擴充功能](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| Docker 擴充功能 |安裝 hello Docker daemon toosupport 遠端 Docker 命令。 |[Docker VM 擴充功能](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| VM 存取擴充功能 |重新取得存取 tooan Azure 虛擬機器 |[VM 存取擴充功能](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| Azure 診斷擴充功能 |管理「Azure 診斷」 |[Azure 診斷擴充功能](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Azure VM 存取擴充功能 |管理使用者和認證 |[適用於 Linux 的 VM 存取擴充功能](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
