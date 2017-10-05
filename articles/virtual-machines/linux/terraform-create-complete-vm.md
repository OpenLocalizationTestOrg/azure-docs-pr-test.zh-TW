---
title: "在 Azure 中使用 Terraform 建立基本基礎結構 | Microsoft Docs"
description: "了解如何使用 Terraform 建立 Azure 資源"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: aa0926de32dd85f4460bbfa84b7a6007e2199d51
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a>在 Azure 中使用 Terraform 建立基本基礎結構
本文說明將虛擬機器和基礎結構佈建至 Azure 需進行的步驟。 您將了解如何撰寫 Terraform 指令碼，以及如何在雲端基礎結構中進行變更前將其視覺化。 您也將了解如何在 Azure 中使用 Terraform 建立基礎結構。

首先，在您所選的文字編輯器 (Visual Studio Code/Sublime/Vim/等等) 中，建立名為 \terraform_azure101.tf 的檔案。 檔案的確切名稱並不重要，因為 Terraform 接受以資料夾名稱作為參數：資料夾中的所有指令碼都會執行。 將下列程式碼貼到新檔案中：

~~~~
# Configure the Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have to include this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
在指令碼的 `provider` 區段中，您可以告訴 Terraform 使用 Azure 提供者在指令碼中佈建資源。 若要取得 subscription_id、appId、password、and tenant_id 的值，請參閱[安裝和設定 Terraform](terraform-install-configure.md) 指南。 如果您已為此區塊中的值建立環境變數，就不需要將其納入。 

`azurerm_resource_group` 資源指示 Terraform 建立新的資源群組。 您可以在本文稍後看到更多在 Terraform 中可用的資源類型。

## <a name="execute-the-script"></a>執行指令碼
儲存指令碼之後，結束並返回主控台/命令列，然後輸入下列命令：
```
terraform init
```
 為 Azure 初始化 Terraform 提供者。 然後將目錄變更為 **terraformscripts**，並發出下列命令：
```
terraform plan
```
我們使用 `plan` Terraform 命令，該命令會查看指令碼中定義的資源。 它會將這些資源與 Terraform 所儲存的狀態資訊進行比較，然後輸出計劃性執行，而「不需」在 Azure 中實際建立資源。 

執行上述命令之後，您應該會看到如下列畫面的內容：

![Terraform plan](./media/terraform/tf_plan2.png)

如果一切看起來正確無誤，請執行下列命令，在 Azure 中佈建這個新的資源群組： 
```
terraform apply
```
在 Azure 入口網站中，您應該會看到名為 `terraformtest` 的新空白資源群組。 在下一節中，您要將虛擬機器以及該虛擬機器支援的所有基礎結構新增至資源群組。

## <a name="provision-an-ubuntu-vm-with-terraform"></a>使用 Terraform 佈建 Ubuntu VM
我們來使用佈建執行 Ubuntu 之虛擬機器所需的詳細資料，擴充已經建立的 Terraform 指令碼。 您在下列各節中佈建的資源包括：

* 有單一子網路的網路
* 網路介面卡 
* 適用於虛擬機器診斷的儲存體帳戶
* 公用 IP
* 使用先前所有資源的虛擬機器 

如需每個 Azure Terraform 資源的完整文件，請參閱 [Terraform 文件](https://www.terraform.io/docs/providers/azurerm/index.html) \(英文\)。

為了方便起見，也提供完整版的[佈建指令碼](#complete-terraform-script)。

### <a name="extend-the-terraform-script"></a>擴充 Terraform 指令碼
使用下列資源擴充建立的指令碼： 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
上述指令碼會建立虛擬網路與該虛擬網路中的子網路。 請注意您已透過 "${azurerm_resource_group.helloterraform.name}" 在虛擬網路和子網路定義中建立之資源群組的參考。

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
上述指令碼的程式碼片段會建立公用 IP，以及建立使用該公用 IP 的網路介面。 請注意 subnet_id 和 public_ip_address_id 的參考。 Terraform 具有內建智慧，可了解網路介面相依於在網路介面建立之前所需建立的資源。

~~~~
# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
至此您已建立了儲存體帳戶。 虛擬機器會將其診斷詳細資料儲存在此儲存體帳戶。

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
最後，先前的程式碼片段會建立虛擬機器，使用已佈建的所有資源。 這些資源是適用於虛擬機器診斷的儲存體帳戶、指定公用 IP 與子網路的網路介面，以及您已建立的資源群組。 請注意 vm_size 屬性，可供指令碼指定 Azure 標準 DS1v2 SKU。

您需要提供 SSH 公開金鑰。 請將公開金鑰值放到區段 **...在此處插入 OPENSSH 公開金鑰...**上方。 您可以使用現有的 ssh 金鑰組，或者依照 [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) 或 [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) 說明文件來產生金鑰組。

### <a name="execute-the-script"></a>執行指令碼
儲存完整的指令碼後，結束並返回主控台/命令列，然後輸入下列命令：
```
terraform apply
```
稍後，資源 (包括虛擬機器) 就會出現在 Azure 入口網站的 `terraformtest` 資源群組中。

## <a name="complete-terraform-script"></a>完成 Terraform 指令碼

為了方便起見，以下是佈建本文中所有基礎結構的完整 Terraform 指令碼。

```
# Configure the Microsoft Azure Provider
provider "azurerm" {
  subscription_id = "XXX"
  client_id       = "XXX"
  client_secret   = "XXX"
  tenant_id       = "XXX"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}

# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}

# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }

    tags {
        environment = "Terraform Demo"
    }
}

# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
```

## <a name="next-steps"></a>後續步驟
您已使用 Terraform 在 Azure 中建立基本基礎結構。 如需更多複雜案例 (包括使用負載平衡器、虛擬機器擴展集的範例)，請參閱許多[適用於 Azure 的 Terraform 範例](https://github.com/hashicorp/terraform/tree/master/examples)。 如需支援的 Azure 提供者最新清單，請參閱 [Terraform 文件](https://www.terraform.io/docs/providers/azurerm/index.html) \(英文\)。
