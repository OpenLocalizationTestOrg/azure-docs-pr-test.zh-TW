---
title: "aaaInstall 和設定 Azure 虛擬機器搭配使用 Ansible |Microsoft 文件"
description: "深入了解如何 tooinstall 和設定來管理 Azure 資源上 Ubuntu、 CentOS 和 SLES Ansible"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/25/2017
ms.author: iainfou
ms.openlocfilehash: b33d1893909b6134a5474617c9af2d6e4f627c05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a>安裝並在 Azure 中設定 Ansible toomanage 虛擬機器
這篇文章說明如何 tooinstall Ansible 和必要的 Azure Python SDK 模組的某些 hello 最常見的 Linux 散發版本。 您可以安裝 Ansible 其他散發版本上藉由調整 hello 安裝封裝 toofit 您特定的平台。 toocreate Azure 資源安全的方式，您也學到如何 toocreate 並定義 Ansible toouse 的認證。 

如需安裝選項和其他平台的步驟，請參閱 hello [Ansible 安裝指南](https://docs.ansible.com/ansible/intro_installation.html)。


## <a name="install-ansible"></a>安裝 Ansible
首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroupAnsible*在 hello *eastus*位置：

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

現在建立 VM，並安裝其中一個 hello 遵循散發版本 Ansible:

- [Ubuntu 16.04 LTS](#ubuntu1604-lts)
- [CentOS 7.3](#centos-73)
- [SLES 12.2 SP2](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS
使用 [az vm create](/cli/azure/vm#create) 來建立 VM。 hello 下列範例會建立名為的 VM *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM 使用 hello`publicIpAddress`述 hello hello VM 的輸出建立作業：

```bash
ssh azureuser@<publicIpAddress>
```

您在 VM 上，安裝所需的 hello 套件 hello Azure Python SDK 模組與 Ansible 如下所示：

```bash
## Install pre-requisite packages
sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev python-pip

## Install Azure SDKs via pip
pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via apt
sudo apt-get install -y software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update && sudo apt-get install -y ansible
```

現在太移動[建立 Azure 認證](#create-azure-credentials)。


### <a name="centos-73"></a>CentOS 7.3
使用 [az vm create](/cli/azure/vm#create) 來建立 VM。 hello 下列範例會建立名為的 VM *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM 使用 hello`publicIpAddress`述 hello hello VM 的輸出建立作業：

```bash
ssh azureuser@<publicIpAddress>
```

您在 VM 上，安裝所需的 hello 套件 hello Azure Python SDK 模組與 Ansible 如下所示：

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

現在太移動[建立 Azure 認證](#create-azure-credentials)。


### <a name="sles-122-sp2"></a>SLES 12.2 SP2
使用 [az vm create](/cli/azure/vm#create) 來建立 VM。 hello 下列範例會建立名為的 VM *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM 使用 hello`publicIpAddress`述 hello hello VM 的輸出建立作業：

```bash
ssh azureuser@<publicIpAddress>
```

您在 VM 上，安裝所需的 hello 套件 hello Azure Python SDK 模組與 Ansible 如下所示：

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

現在太移動[建立 Azure 認證](#create-azure-credentials)。


## <a name="create-azure-credentials"></a>建立 Azure 認證
Ansible 會使用使用者名稱與密碼或服務主體與 Azure 進行通訊。 Azure 服務主體是安全性識別，可供您與應用程式、服務及諸如 Ansible 等自動化工具搭配使用。 您可以控制和定義 hello 權限，如 toowhat 作業 hello 服務主體可以在 Azure 中執行。 透過提供使用者名稱和密碼的 tooimprove 安全性，這個範例會建立基本的服務主體。

建立服務主體與[az ad 預存程序建立-如-rbac](/cli/azure/ad/sp#create-for-rbac)和 Ansible 需要輸出 hello 認證：

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

從上述命令 hello hello 輸出的範例如下所示：

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

tooauthenticate tooAzure，您也需要您的 Azure 訂用帳戶 ID 與 tooobtain [az 帳戶顯示](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

您可以使用這兩個命令 hello 輸出 hello 下一個步驟中。


## <a name="create-ansible-credentials-file"></a>建立 Ansible 認證檔案
tooprovide 認證 tooAnsible，定義環境變數，或建立本機認證檔案。 如需有關如何 toodefine Ansible 認證，請參閱[提供認證 tooAzure 模組](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules)。 

針對開發環境，在您的主機 VM 上建立 Ansible 的「認證」檔案，如下所示：

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

hello*認證*檔案本身結合 hello 訂用帳戶 ID 與建立服務主體的 hello 輸出。 從先前的 hello 輸出[az ad 預存程序建立-如-rbac](/cli/azure/ad/sp#create-for-rbac)命令是 hello 相同訂單所需的*client_id*，*密碼*，和*租用戶*. 下列範例 hello*認證*檔案會顯示比對 hello 上述輸出這些值。 輸入您自己的值，如下所示︰

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a>使用 Ansible 環境變數
如果您正在 Ansible 塔或 Jenkins toouse 工具，您可以定義環境變數，如下所示。 這些變數會結合 hello 輸出建立服務主體中的 hello 訂用帳戶 ID。 從先前的 hello 輸出[az ad 預存程序建立-如-rbac](/cli/azure/ad/sp#create-for-rbac)命令是 hello 相同訂單所需的*AZURE_CLIENT_ID*， *AZURE_SECRET*，和*AZURE_租用戶*。 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a>後續步驟
您現在可以 Ansible 和 hello 必要安裝，Azure Python SDK 模組和 Ansible toouse 為定義的認證。 了解如何太[Ansible 與建立 VM](ansible-create-vm.md)。 您也可以了解如何太[建立完整的 Azure VM 和支援資源 Ansible](ansible-create-complete-vm.md)。
