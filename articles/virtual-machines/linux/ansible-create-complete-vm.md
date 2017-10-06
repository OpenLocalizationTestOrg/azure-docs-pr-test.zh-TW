---
title: "在 Azure 中完成的 Linux VM 的 aaaUse Ansible toocreate |Microsoft 文件"
description: "深入了解如何 toouse Ansible toocreate 和管理 Azure 中完整的 Linux 虛擬機器環境"
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
ms.openlocfilehash: 970b0427f39fc23240f9faab868196ca4f444e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a>使用 Ansible 在 Azure 中建立完整的 Linux 虛擬機器環境
Ansible 可讓您 tooautomate hello 部署和設定資源在您的環境中。 您可以在 Azure 中虛擬機器 (Vm) 使用 Ansible toomanage、 hello 相同，如同任何其他資源。 本文章將示範如何 toocreate 完整 Linux 環境和支援 Ansible 資源。 您也可以了解如何太[Ansible 建立基本 VM](ansible-create-vm.md)。


## <a name="prerequisites"></a>必要條件
toomanage Azure Ansible 資源，您需要遵循的 hello:

- Ansible 和 hello Azure Python SDK 模組安裝在主機系統上。
    - 在 [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts)、[CentOS 7.3](ansible-install-configure.md#centos-73) 和 [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2) 上安裝 Ansible
- Azure 認證和設定 Ansible toouse 它們。
    - [建立 Azure 認證和設定 Ansible](ansible-install-configure.md#create-azure-credentials)
- Azure CLI 2.0.4 版或更新版本。 執行`az --version`toofind hello 版本。 
    - 如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 您也可以在瀏覽器中使用 [Cloud Shell](/azure/cloud-shell/quickstart)。


## <a name="create-virtual-network"></a>建立虛擬網路
hello Ansible 腳本中的下一節建立虛擬網路，名為*myVnet*在 hello *10.0.0.0/16*位址空間：

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

tooadd 子網路，hello 下列區段會建立名為的子網路*mySubnet*在 hello *myVnet*虛擬網路：

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a>建立公用 IP 位址
跨網際網路，hello tooaccess 資源建立，並指派公用 IP 位址 tooyour VM。 hello Ansible 腳本中的下列區段會建立名為的公用 IP 位址*myPublicIP*:

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a>建立網路安全性群組
網路安全性群組 hello 流程控制的網路流量，進出您的 VM。 hello Ansible 腳本中的下列區段會建立名為的網路安全性群組*myNetworkSecurityGroup*並定義規則 tooallow SSH 流量的 TCP 連接埠 22:

```yaml
- name: Create Network Security Group that allows SSH
  azure_rm_securitygroup:
    resource_group: myResourceGroup
    name: myNetworkSecurityGroup
    rules:
      - name: SSH
        protocol: TCP
        destination_port_range: 22
        access: Allow
        priority: 1001
        direction: Inbound
```


## <a name="create-virtual-network-interface-card"></a>建立虛擬網路介面卡
虛擬網路介面卡 (NIC) 會連接您的 VM tooa 指定虛擬網路、 公用 IP 位址和網路安全性群組。 hello Ansible 腳本中的下列區段會建立名為以虛擬 NIC *myNIC*連接 toohello 虛擬網路功能資源已經建立：

```yaml
- name: Create virtual network inteface card
  azure_rm_networkinterface:
    resource_group: myResourceGroup
    name: myNIC
    virtual_network: myVnet
    subnet: mySubnet
    public_ip_name: myPublicIP
    security_group: myNetworkSecurityGroup
```


## <a name="create-virtual-machine"></a>Create virtual machine
hello 最後一個步驟是 toocreate VM，並使用所有建立的 hello 資源。 hello Ansible 腳本中的下列區段會建立名為的 VM *myVM*和附加 hello 虛擬 NIC，名為*myNIC*。 輸入您自己的公開金鑰資料在 hello *key_data*配對，如下所示：

```yaml
- name: Create VM
  azure_rm_virtualmachine:
    resource_group: myResourceGroup
    name: myVM
    vm_size: Standard_DS1_v2
    admin_username: azureuser
    ssh_password_enabled: false
    ssh_public_keys: 
      - path: /home/azureuser/.ssh/authorized_keys
        key_data: "ssh-rsa AAAAB3Nz{snip}hwhqT9h"
    network_interfaces: myNIC
    image:
      offer: CentOS
      publisher: OpenLogic
      sku: '7.3'
      version: latest
```

## <a name="complete-ansible-playbook"></a>完整 Ansible 腳本
toobring 所有這些章節，建立名為 Ansible 腳本*azure_create_complete_vm.yml*和 hello 貼上下列內容：

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create virtual network
    azure_rm_virtualnetwork:
      resource_group: myResourceGroup
      name: myVnet
      address_prefixes: "10.0.0.0/16"
  - name: Add subnet
    azure_rm_subnet:
      resource_group: myResourceGroup
      name: mySubnet
      address_prefix: "10.0.1.0/24"
      virtual_network: myVnet
  - name: Create public IP address
    azure_rm_publicipaddress:
      resource_group: myResourceGroup
      allocation_method: Static
      name: myPublicIP
  - name: Create Network Security Group that allows SSH
    azure_rm_securitygroup:
      resource_group: myResourceGroup
      name: myNetworkSecurityGroup
      rules:
        - name: SSH
          protocol: Tcp
          destination_port_range: 22
          access: Allow
          priority: 1001
          direction: Inbound
  - name: Create virtual network inteface card
    azure_rm_networkinterface:
      resource_group: myResourceGroup
      name: myNIC
      virtual_network: myVnet
      subnet: mySubnet
      public_ip_name: myPublicIP
      security_group: myNetworkSecurityGroup
  - name: Create VM
    azure_rm_virtualmachine:
      resource_group: myResourceGroup
      name: myVM
      vm_size: Standard_DS1_v2
      admin_username: azureuser
      ssh_password_enabled: false
      ssh_public_keys: 
        - path: /home/azureuser/.ssh/authorized_keys
          key_data: "ssh-rsa AAAAB3Nz{snip}hwhqT9h"
      network_interfaces: myNIC
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

Ansible 需要資源群組 toodeploy 到的所有資源。 使用 [az group create](/cli/azure/vm#create) 來建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：

```azurecli
az group create --name myResourceGroup --location eastus
```

toocreate hello 完成 VM 環境使用 Ansible，執行 hello 腳本，如下所示：

```bash
ansible-playbook azure_create_complete_vm.yml
```

hello 輸出看起來類似下列範例會顯示 hello 已成功建立 VM 的 toohello:

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create virtual network] *********************************************
changed: [localhost]

TASK [Add subnet] *********************************************************
changed: [localhost]

TASK [Create public IP address] *******************************************
changed: [localhost]

TASK [Create Network Security Group that allows SSH] **********************
changed: [localhost]

TASK [Create virtual network inteface card] *******************************
changed: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=7    changed=6    unreachable=0    failed=0
```

## <a name="next-steps"></a>後續步驟
這個範例會建立完整的 VM 環境，包括所需的 hello 虛擬網路功能資源。 更直接範例 toocreate 到現有的網路資源預設選項的 VM，請參閱[建立 VM](ansible-create-vm.md)。
