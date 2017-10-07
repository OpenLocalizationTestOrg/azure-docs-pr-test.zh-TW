---
title: "快速入門-aaaAzure 建立 Windows VM CLI |Microsoft 文件"
description: "快速了解 toocreate 以 hello Azure CLI Windows 虛擬機器。"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 029bdecec219b12b80b958ceeedda214f1b13149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-cli"></a>建立 Windows 虛擬機器以 hello Azure CLI

hello Azure CLI 會使用的 toocreate 和管理 Azure 資源，從 hello 命令列或指令碼中。 執行 Windows Server 2016 的虛擬機器使用 hello Azure CLI toodeploy 本指南詳述。 當部署完成之後，我們 toohello 伺服器連接，並安裝 IIS。

如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本快速入門會要求執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 


## <a name="create-a-resource-group"></a>建立資源群組

使用 [az group create](/cli/azure/group#create) 來建立資源群組。 Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。 

hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置。

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Create virtual machine

使用 [az vm create](/cli/azure/vm#create) 來建立 VM。 

hello 下列範例會建立名為的 VM *myVM*。 這個範例會使用*azureuser*系統管理使用者名稱和*myPassword12* hello 密碼。 更新這些值 toosomething 適當 tooyour 環境。 與 hello 虛擬機器建立的連接時，會需要這些值。

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

建立 hello VM 後，hello Azure CLI 顯示資訊的類似 toohello 下列範例。 記下 hello `publicIpAaddress`。 此位址為使用的 tooaccess hello VM。

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>針對 Web 流量開啟連接埠 80 

預設只有 RDP 連線允許 tooWindows 虛擬機器部署在 Azure 中。 如果此 VM 將會 toobe web 伺服器，您需要從網際網路 hello tooopen 連接埠 80。 使用 hello [az vm 開啟通訊埠](/cli/azure/vm#open-port)命令 tooopen hello 所需的連接埠。  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-toovirtual-machine"></a>Toovirtual 機器連線

使用 hello 下列命令 toocreate 與 hello 虛擬機器的遠端桌面工作階段。 取代 hello 公用 IP 位址的虛擬機器中的 hello IP 位址。 出現提示時，輸入 hello 建立 hello 虛擬機器時使用的認證。

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a>使用 PowerShell 安裝 IIS

既然您已登入 toohello Azure VM，您可以使用單行 PowerShell tooinstall IIS，並啟用 hello 本機防火牆規則 tooallow web 流量。 開啟 PowerShell 命令提示字元並執行下列命令的 hello:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>檢視 hello IIS [歡迎使用] 頁面

安裝 IIS 和現在 hello 網際網路從 VM 上開啟連接埠 80，您可以使用網頁瀏覽器，您的選擇 tooview hello 預設 IIS 歡迎使用頁面。 為確定 toouse hello 公用 IP 位址您 toovisit hello 預設頁面上面所記載。 

![IIS 預設網站](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>清除資源

當不再需要您可以使用 hello [az 群組刪除](/cli/azure/group#delete)命令 tooremove hello 資源群組、 VM 和所有相關的資源。

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>後續步驟

在此快速入門中，您已部署簡單的虛擬機器、網路安全性群組規則，並已安裝 Web 伺服器。 進一步了解 Azure 虛擬機器，toolearn 繼續 toohello 教學課程適用於 Windows Vm。

> [!div class="nextstepaction"]
> [Azure Windows 虛擬機器教學課程](./tutorial-manage-vm.md)
