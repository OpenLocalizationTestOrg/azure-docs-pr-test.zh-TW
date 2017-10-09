---
title: "aaaHow toocreate Linux Azure VM 映像與 Packer |Microsoft 文件"
description: "深入了解如何在 Azure 中 Linux 虛擬機器的 toouse Packer toocreate 映像"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 5990598859e73efac477884bc8de5fd5138bf6e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a>Toouse Packer toocreate Linux 虛擬機器在 Azure 中的映像
在 Azure 中的每個虛擬機器 (VM) 是從定義 hello Linux 發行版本和作業系統版本的映像建立。 映像中可包含預先安裝的應用程式與組態。 hello Azure Marketplace 提供許多的第一個和第三方映像的最常見的分佈和應用程式環境，或您可以建立您自己的自訂映像，量身訂做 tooyour 需求。 這篇文章說明如何 toouse hello 開啟原始碼工具[Packer](https://www.packer.io/) toodefine 和建置在 Azure 中的自訂影像。


## <a name="create-azure-resource-group"></a>建立 Azure 資源群組
在 hello 建置過程中，Packer 會建立暫存的 Azure 資源，當它建立 hello 來源 VM。 來源 VM 用作映像的 toocapture，您必須定義的資源群組。 hello hello Packer 建置程序的輸出會儲存在此資源群組。

使用 [az group create](/cli/azure/group#create) 來建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a>建立 Azure 認證
Packer 會使用服務主體來向 Azure 驗證。 Azure 服務主體是安全性識別，可供您與應用程式、服務及諸如 Packer 等自動化工具搭配使用。 您可以控制和定義 hello 權限，如 toowhat 作業 hello 服務主體可以在 Azure 中執行。

建立服務主體與[az ad 預存程序建立-如-rbac](/cli/azure/ad/sp#create-for-rbac)和 Packer 需要輸出 hello 認證：

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

從上述命令 hello hello 輸出的範例如下所示：

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

tooauthenticate tooAzure，您也需要您的 Azure 訂用帳戶 ID 與 tooobtain [az 帳戶顯示](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

您可以使用這兩個命令 hello 輸出 hello 下一個步驟中。


## <a name="define-packer-template"></a>定義 Packer 範本
toobuild 映像，您會建立範本成為 JSON 檔案。 Hello 範本中定義產生器和 provisioners hello 實際執行的建置程序。 具有 packer [provisioner azure](https://www.packer.io/docs/builders/azure.html) ，可讓您 toodefine Azure 資源，例如 hello 服務主體認證 hello 前面步驟中建立。

建立名為*ubuntu.json*和 hello 貼上下列內容。 輸入您自己的值為 hello 下列：

| 參數                           | 其中 tooobtain |
|-------------------------------------|----------------------------------------------------|
| client_id                         | `az ad sp` 建立命令所產生之輸出的第一行 - appId |
| client_secret                     | `az ad sp` 建立命令所產生之輸出的第二行 - password |
| tenant_id                         | `az ad sp` 建立命令所產生之輸出的第三行 - tenant |
| subscription_id                   | `az account show` 命令所產生的輸出 |
| managed_image_resource_group_name | 您在 hello 第一個步驟中建立的資源群組名稱 |
| managed_image_name                | 建立 hello 受管理的磁碟映像的名稱 |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

此範本建置 Ubuntu 16.04 LTS 映像，請安裝 NGINX，然後 deprovisions hello VM。

> [!NOTE]
> 如果您展開此範本 tooprovision 使用者認證時，調整 hello provisioner 命令 deprovisions hello Azure 代理程式 tooread`-deprovision`而不是`deprovision+user`。
> hello`+user`旗標移除 hello 來源 VM 中的所有使用者帳戶。


## <a name="build-packer-image"></a>建置 Packer 映像
如果您還沒有安裝在本機電腦上的 Packer[依照 hello Packer 安裝指示](https://www.packer.io/docs/install/index.html)。

建立 hello 映像藉由指定您 Packer 範本檔案，如下所示：

```bash
./packer build ubuntu.json
```

從上述命令 hello hello 輸出的範例如下所示：

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH toobecome available...
==> azure-arm: Connected tooSSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! hello waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able toologin as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a>從 Azure 映像建立 VM
您現在可以使用 [az vm create](/cli/azure/vm#create) 從您的映像建立 VM。 指定您建立以 hello 映像 hello`--image`參數。 hello 下列範例會建立名為的 VM *myVM*從*myPackerImage*並產生 SSH 金鑰，如果它們尚不存在：

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

花幾分鐘的時間 toocreate hello VM。 一旦建立 hello VM 之後，記下 hello`publicIpAddress`顯示 hello Azure CLI。 這個位址是透過 web 瀏覽器使用的 tooaccess hello NGINX 站台。

tooallow web 流量 tooreach VM，開啟的通訊埠 80 hello 網際網路從[az vm 開啟通訊埠](/cli/azure/vm#open-port):

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a>測試 VM 和 NGINX
現在您可以開啟網頁瀏覽器並輸入`http://publicIpAddress`hello 網址列中。 提供自己的公用 IP 位址從 hello VM 建立處理程序。 hello 預設 NGINX 網頁會顯示如 hello 下列範例所示：

![預設 NGINX 網站](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a>後續步驟
在此範例中，您搭配 Packer toocreate VM 映像 NGINX 已經安裝。 您可以使用現有的部署工作流程，例如從 hello Ansible、 Chef 或 Puppet 的映像建立的應用程式 tooVMs toodeploy 連同此 VM 映像。

如需其他 Linux 散發套件的其他 Packer 範本範例，請參閱[這個 GitHub 存放庫](https://github.com/hashicorp/packer/tree/master/examples/azure)。