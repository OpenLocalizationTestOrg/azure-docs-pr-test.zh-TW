---
title: "aaaCreate 基本基礎結構在 Azure 中的使用 Terraform |Microsoft 文件"
description: "深入了解如何 toocreate Azure 使用 Terraform 資源"
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
ms.openlocfilehash: 52591009ee7cb906402b8bca2ce63794ac7afcc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a>在 Azure 中使用 Terraform 建立基本基礎結構
本文將告訴您需要 tootake tooprovision 虛擬機器，以及基礎結構，到 Azure 的 hello 步驟。 您將學習如何 toowrite Terraform 指令碼和 toovisualize hello 如何才能變更可讓這些雲端基礎結構。 您也將學習如何在 Azure 中使用 Terraform 的 toocreate 基礎結構。

tooget 啟動，建立一個稱為 \terraform_azure101.tf 文字編輯器 （Visual Studio 程式碼/適/Vim/等等） 所選擇的檔案。 hello 的 hello 檔案的確切名稱不重要，因為 Terraform 接受 hello 做為參數的資料夾名稱： hello 資料夾中的所有指令碼會執行。 貼上下列程式碼 hello 新檔案中的 hello:

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
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
在 hello `provider` hello 部分指令碼，您可告知 Terraform toouse Azure 提供者 tooprovision 資源 hello 指令碼中。 tooget 值 subscription_id、 appId、 密碼和 tenant_id，請參閱 hello[安裝及設定 Terraform](terraform-install-configure.md)指南。 如果您已經建立 hello 值的環境變數，此區塊中，您不需要 tooinclude 它。 

hello`azurerm_resource_group`資源會指示 Terraform toocreate 新的資源群組。 您可以在本文稍後看到更多在 Terraform 中可用的資源類型。

## <a name="execute-hello-script"></a>執行 hello 指令碼
儲存 hello 指令碼之後，結束 toohello 主控台命令列，然後輸入 hello 下列：
```
terraform init
```
 tooinitialize azure 的 hello Terraform 提供者。 然後將 hello 目錄變更太**terraformscripts**，和問題 hello 下列命令：
```
terraform plan
```
我們使用 hello `plan` Terraform 命令，查看 hello hello 指令碼中定義的資源。 在比較 toohello Terraform 所儲存的狀態資訊，然後輸出 hello 計劃的執行_沒有_實際上在 Azure 中建立資源。 

Hello 前一個命令執行之後，您應該會看到像下列螢幕 hello:

![Terraform plan](./media/terraform/tf_plan2.png)

如果一切正確，佈建在 Azure 中的這個新資源群組，藉由執行下列 hello: 
```
terraform apply
```
在 hello Azure 入口網站，您應該會看到 hello 新空的資源群組稱為`terraformtest`。 在 hello 下列區段，您將虛擬機器，而且所有 hello 支援該虛擬機器 toohello 資源群組的基礎結構。

## <a name="provision-an-ubuntu-vm-with-terraform"></a>使用 Terraform 佈建 Ubuntu VM
讓我們來擴充虛擬機器執行 Ubuntu hello Terraform 指令碼，我們建立了具有必要 tooprovision hello 詳細資料。 您在下列各節的 hello 佈建的 hello 資源包括：

* 有單一子網路的網路
* 網路介面卡 
* Hello 虛擬機器診斷儲存體帳戶
* 公用 IP
* 虛擬機器，它會利用所有的 hello 先前的資源 

如需每個 hello Azure Terraform 資源的完整文件，請參閱 hello [Terraform 文件](https://www.terraform.io/docs/providers/azurerm/index.html)。

hello 完整版的 hello[佈建指令碼](#complete-terraform-script)也為了方便起見。

### <a name="extend-hello-terraform-script"></a>擴充 hello Terraform 指令碼
擴充 hello 下列資源以建立 hello 指令碼： 
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
hello 至上一個指令碼會建立虛擬網路與該虛擬網路中的子網路。 請注意您已經建立透過 hello 虛擬網路和 hello 子網路定義中的"${azurerm_resource_group.helloterraform.name}"hello 參考 toohello 資源群組。

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
hello 先前的指令碼片段會建立公用 IP 與網路介面，可利用建立 hello 公用 IP。 請注意 hello 參考 toosubnet_id public_ip_address_id。 Terraform 具有內建智慧 toounderstand hello 該網路介面具有相依性 hello 資源建立 hello hello 網路介面建立之前，需要 toobe。

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
至此您已建立了儲存體帳戶。 這個儲存體帳戶是 hello 虛擬機器將在其中儲存其診斷詳細資料。

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
最後，hello 先前程式碼片段會建立虛擬機器，它會利用所有已佈建的 hello 資源。 它們是 hello 虛擬機器診斷、 公用 IP 與指定的子網路的網路介面的儲存體帳戶並 hello 資源群組已建立。 請注意 hello vm_size 屬性，其中 hello 指令碼會指定 Azure 標準 DS1v2 SKU。

您會需要的 toosupply SSH 公開金鑰。 將 hello 公開金鑰值放入 hello 區段**...在此處插入 OPENSSH 公開金鑰...**上方。 您可以使用現有的 ssh 金鑰組，或遵循 hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows)或[Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys)文件 toogenerate hello 金鑰組。

### <a name="execute-hello-script"></a>執行 hello 指令碼
Hello 儲存了完整的指令碼，結束 toohello 主控台/命令列與 hello 下列輸入：
```
terraform apply
```
一段時間後 hello 資源，包括虛擬機器時，會出現在 hello `terraformtest` hello Azure 入口網站中的資源群組。

## <a name="complete-terraform-script"></a>完成 Terraform 指令碼

為了方便起見，以下是 hello 完整 Terraform 指令碼來佈建所有 hello 基礎結構的本文中所討論。

```
# Configure hello Microsoft Azure Provider
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
您已使用 Terraform 在 Azure 中建立基本基礎結構。 如需更多複雜案例 (包括使用負載平衡器、虛擬機器擴展集的範例)，請參閱許多[適用於 Azure 的 Terraform 範例](https://github.com/hashicorp/terraform/tree/master/examples)。 支援的 Azure 提供者的最新清單，請參閱 hello [Terraform 文件](https://www.terraform.io/docs/providers/azurerm/index.html)。
