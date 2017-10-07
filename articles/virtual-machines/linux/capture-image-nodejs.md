---
title: "為範本 Azure Linux VM toouse aaaCapture |Microsoft 文件"
description: "深入了解如何 toocapture 和 Linux 型 Azure 虛擬機器 (VM) 與 hello Azure Resource Manager 部署模型所建立的映像一般化。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a>擷取在 Azure 上執行的 Linux 虛擬機器
請遵循本文章 toogeneralize 中的 hello 步驟，並擷取 Azure Linux 虛擬機器 (VM) 中 hello Resource Manager 部署模型。 當一般化 hello VM 時，您會移除個人帳戶資訊，並準備 hello VM toobe 做為映像。 您接著擷取的 hello 的作業系統上，連接的資料磁碟的 Vhd 映像一般化虛擬硬碟 (VHD) 和[Resource Manager 範本](../../azure-resource-manager/resource-group-overview.md)針對新的 VM 部署。 這篇文章說明如何 toocapture VM 的映像以 hello Azure CLI 1.0 使用未受管理的磁碟的 VM。 您也可以[擷取 VM，使用 Azure 受管理磁碟的 hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 受管理的磁碟都由 hello Azure 平台，而且不需要任何準備或位置 toostore 它們。 如需詳細資訊，請參閱 [Azure 受控磁碟概觀](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 

toocreate Vm 使用 hello 映像，為每個新的 VM，並將它從 hello 擷取 VHD 映像使用 hello 範本 （JavaScript 物件標記法或 JSON，檔案） toodeploy 設定網路資源。 如此一來，您可以複寫其目前軟體的組態，toohello 類似您在 hello Azure Marketplace 中使用映像的 VM。

> [!TIP]
> 如果您想 toocreate 一份您現有的 Linux VM 以其特定狀態的備份] 或 [偵錯時，請參閱[建立在 Azure 上執行的 Linux 虛擬機器的複本](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 如果您想 tooupload Linux VHD 從內部部署 VM，請參閱和[上傳並從自訂的磁碟映像建立 Linux VM](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。  

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- [Azure CLI 1.0](#before-you-begin) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI

## <a name="before-you-begin"></a>開始之前
請確定您符合下列必要條件 hello:

* **Hello Resource Manager 部署模型中建立的 azure VM** -如果您尚未建立 Linux VM，您可以使用 hello[入口網站](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，hello [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，或[資源管理員範本](create-ssh-secured-vm-from-template.md)。 
  
    設定 VM，視 hello。 例如，[新增資料磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)、套用更新，並安裝應用程式。 
* **Azure CLI** -安裝 hello [Azure CLI](../../cli-install-nodejs.md)本機電腦上。

## <a name="step-1-remove-hello-azure-linux-agent"></a>步驟 1： 移除 hello Azure Linux 代理程式
首先，執行 hello **waagent**命令與 hello**解除佈建**hello Linux VM 上的參數。 此命令會刪除檔案和資料 toomake hello 準備好將一般化 VM。 如需詳細資訊，請參閱 hello [Azure Linux 代理程式使用者指南](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

1. 連接 tooyour 使用 SSH 用戶端的 Linux VM。
2. 在 hello SSH 視窗中，輸入下列命令的 hello:
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > 只有執行此命令在 VM 上的您想 toocapture 做為映像。 它並不保證清除所有的機密資訊的 hello 映像，或適用於轉散發。
 
3. 型別**y** toocontinue。 您可以新增 hello **-強制**參數 tooavoid 此確認步驟。
4. Hello 命令完成之後，請輸入**結束**。 此步驟會關閉 hello SSH 用戶端。

## <a name="step-2-capture-hello-vm"></a>步驟 2： 擷取 hello VM
使用 hello Azure CLI toogeneralize，並擷取 hello VM。 在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包含 **myResourceGroup**、**myVnet** 和 **myVM**。

1. 從本機電腦，開啟 hello Azure CLI 和[Azure 訂用帳戶的登入 tooyour](../../xplat-cli-connect.md)。 
2. 確定您處於 Resource Manager 模式。
   
    ```azurecli
    azure config mode arm
    ```
3. 關閉 VM，您已經解除佈建使用下列命令的 hello hello:
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. 一般化 hello VM 以 hello 下列命令：
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. 現在執行 hello **azure vm 擷取**命令中，哪些擷取 hello VM。 在下列範例的 hello，hello 以擷取 Vhd 的映像名稱開頭**MyVHDNamePrefix**，和 hello **-t**選項指定路徑 toohello 範本**MyTemplate.json**. 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > 根據預設，在使用 hello 原始 VM 的相同儲存體帳戶的 hello 建立 hello 映像的 VHD 檔案。 使用 hello*相同儲存體帳戶*toostore hello 任何新的 Vm，您建立從 hello 映像的 Vhd。 

6. 擷取的映像，在文字編輯器中開啟 hello JSON 範本 toofind hello 位置。 在 hello **storageProfile**，尋找 hello **uri**的 hello**映像**位於 hello**系統**容器。 例如，hello hello OS 磁碟映像的 URI 太類似`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>步驟 3： 從 hello 擷取映像建立 VM
現在使用 hello 映像與範本 toocreate Linux VM。 下列步驟顯示如何 toouse hello Azure CLI 和 hello 擷取 toocreate hello VM 在新的虛擬網路中的 JSON 檔案範本。

### <a name="create-network-resources"></a>建立網路資源
toouse hello 範本，您必須先設定虛擬網路和 NIC tooset 新的 vm。 我們建議您對這些資源的資源群組中建立 hello 儲存您的 VM 映像的位置。 執行命令之後，以取代您的資源和適當的 Azure 位置 (在這些命令中為"centralus") 的名稱類似 toohello:

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a>取得 hello hello NIC 的識別碼
toodeploy 從使用儲存在擷取期間的 JSON hello hello 映像的 VM，您需要 hello 識別碼 hello nic。 取得此執行 hello 下列命令：

```azurecli
azure network nic show myResourceGroup1 myNIC
```

hello**識別碼**在 hello 的輸出是類似太`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`

### <a name="create-a-vm"></a>建立 VM
現在執行的 hello 下列命令 toocreate hello 從 VM 會擷取 VM 映像。 使用 hello **-f**參數 toospecify hello 路徑 toohello 範本 JSON 檔案儲存。

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

在 hello 命令輸出中，您提示的 toosupply 新的 VM 名稱、 hello 系統管理員使用者名稱和密碼，而且 hello hello NIC 您先前建立的識別碼。

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

hello 下列範例會顯示您成功部署請參閱：

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-hello-deployment"></a>確認 hello 部署
現在 SSH toohello 建立虛擬機器您 tooverify hello 部署並開始使用 hello 新的 VM。 透過 SSH，tooconnect 尋找 hello 的 hello 您藉由執行下列命令的 hello 建立的 VM 的 IP 位址：

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

hello 公用 IP 位址會列在 hello 命令輸出。 依預設，您會連接 toohello Linux VM 的 SSH 連接埠 22。

## <a name="create-additional-vms"></a>建立額外的 VM
使用 hello 擷取映像和範本 toodeploy 使用 hello 步驟 hello 前面一節中的其他 Vm。 其他選項 toocreate Vm 從 hello 映像包括使用快速入門範本，或執行 hello **azure vm 建立**命令。

### <a name="use-hello-captured-template"></a>使用 hello 擷取的範本
toouse hello 擷取映像和範本，請遵循下列步驟 （hello 前面一節中詳細說明）：

* 請確認您的 VM 映像處於 hello 裝載 VM 的 VHD 的相同儲存體帳戶。
* 複製 hello 範本 JSON 檔案，並指定 hello hello 新 VM 的 VHD （或 Vhd） 的作業系統磁碟的唯一名稱。 例如，在 hello **storageProfile**下**vhd**，請在**uri**，指定唯一的名稱，如 hello **osDisk** VHD，類似太`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`
* 相同或不同的虛擬網路，請在任一個 hello 中建立的 NIC。
* 使用修改的 hello 範本 JSON 檔案，在您設定虛擬網路的 hello hello 資源群組中建立的部署。

### <a name="use-a-quickstart-template"></a>使用快速入門範本
如果您想 hello 網路設定當您從自動建立 VM hello 映像，您可以在範本中指定這些資源。 例如，請參閱 hello [101 vm 從-使用者-映像範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)從 GitHub。 此範本建立的 VM，您自訂映像和 hello 必要的虛擬網路、 公用 IP 位址，及 NIC 的資源。 在 hello Azure 入口網站中使用 hello 範本的逐步解說，請參閱[如何 toocreate 使用資源管理員範本的自訂映像中的虛擬機器](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/)。

### <a name="use-hello-azure-vm-create-command"></a>使用 hello azure vm 建立命令
通常它是最簡單的 toouse 資源管理員範本 toocreate 從 hello 映像的 VM。 不過，您可以在其中建立 hello VM*以命令方式*使用 hello **azure vm 建立**命令與 hello **-Q** (**-映像 urn**) 參數. 如果您使用此方法時，您也可以傳遞 hello **-d** (**-os-磁碟 vhd**) hello OS.vhd 檔案的參數 toospecify hello 位置 hello 新的 VM。 這個檔案必須在 hello hello hello 映像的 VHD 檔案所在的儲存體帳戶的 vhd 容器中。 hello 命令複製 VHD hello hello 新的 VM 會自動 toohello **vhd**容器。

執行前**azure vm 建立**hello 映像，以完成下列步驟的 hello:

1. 建立資源群組，或識別 hello 部署現有的資源群組。
2. 建立公用 IP 位址資源和 NIC 資源 hello 新的 VM。 如步驟 toocreate 的虛擬網路、 公用 IP 位址和 NIC 使用 hello CLI，請參閱稍早在本文中。 (**azure vm 建立**也可以建立 NIC，但您需要為虛擬網路和子網路的 toopass 其他參數。)

然後執行可將 Uri 傳遞 tooboth hello 新作業系統的 VHD 檔案，並 hello 現有映像的命令。 在此範例中，大小 Standard_A1 VM 建立 hello 美東地區。

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

如需其他命令選項，請執行 `azure help vm create`。

## <a name="next-steps"></a>後續步驟
toomanage Vm 以 hello CLI，請參閱中的 hello 工作[部署和管理虛擬機器使用的 Azure Resource Manager 範本和 hello Azure CLI](create-ssh-secured-vm-from-template.md)。

