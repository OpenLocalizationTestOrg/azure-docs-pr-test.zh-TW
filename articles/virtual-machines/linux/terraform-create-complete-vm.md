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
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="404b1-103">在 Azure 中使用 Terraform 建立基本基礎結構</span><span class="sxs-lookup"><span data-stu-id="404b1-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="404b1-104">本文說明將虛擬機器和基礎結構佈建至 Azure 需進行的步驟。</span><span class="sxs-lookup"><span data-stu-id="404b1-104">This article describes the steps you need to take to provision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="404b1-105">您將了解如何撰寫 Terraform 指令碼，以及如何在雲端基礎結構中進行變更前將其視覺化。</span><span class="sxs-lookup"><span data-stu-id="404b1-105">You will learn how to write Terraform scripts and how to visualize the changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="404b1-106">您也將了解如何在 Azure 中使用 Terraform 建立基礎結構。</span><span class="sxs-lookup"><span data-stu-id="404b1-106">You also will learn how to create infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="404b1-107">首先，在您所選的文字編輯器 (Visual Studio Code/Sublime/Vim/等等) 中，建立名為 \terraform_azure101.tf 的檔案。</span><span class="sxs-lookup"><span data-stu-id="404b1-107">To get started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="404b1-108">檔案的確切名稱並不重要，因為 Terraform 接受以資料夾名稱作為參數：資料夾中的所有指令碼都會執行。</span><span class="sxs-lookup"><span data-stu-id="404b1-108">The exact name of the file isn't important because Terraform accepts the folder name as a parameter: all scripts in the folder get executed.</span></span> <span data-ttu-id="404b1-109">將下列程式碼貼到新檔案中：</span><span class="sxs-lookup"><span data-stu-id="404b1-109">Paste the following code in the new file:</span></span>

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
<span data-ttu-id="404b1-110">在指令碼的 `provider` 區段中，您可以告訴 Terraform 使用 Azure 提供者在指令碼中佈建資源。</span><span class="sxs-lookup"><span data-stu-id="404b1-110">In the `provider` section of the script, you tell Terraform to use an Azure provider to provision resources in the script.</span></span> <span data-ttu-id="404b1-111">若要取得 subscription_id、appId、password、and tenant_id 的值，請參閱[安裝和設定 Terraform](terraform-install-configure.md) 指南。</span><span class="sxs-lookup"><span data-stu-id="404b1-111">To get values for subscription_id, appId, password, and tenant_id, see the [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="404b1-112">如果您已為此區塊中的值建立環境變數，就不需要將其納入。</span><span class="sxs-lookup"><span data-stu-id="404b1-112">If you have created environment variables for the values in this block, you don't need to include it.</span></span> 

<span data-ttu-id="404b1-113">`azurerm_resource_group` 資源指示 Terraform 建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="404b1-113">The `azurerm_resource_group` resource instructs Terraform to create a new resource group.</span></span> <span data-ttu-id="404b1-114">您可以在本文稍後看到更多在 Terraform 中可用的資源類型。</span><span class="sxs-lookup"><span data-stu-id="404b1-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-the-script"></a><span data-ttu-id="404b1-115">執行指令碼</span><span class="sxs-lookup"><span data-stu-id="404b1-115">Execute the script</span></span>
<span data-ttu-id="404b1-116">儲存指令碼之後，結束並返回主控台/命令列，然後輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="404b1-116">After you save the script, exit to the console/command line, and type the following:</span></span>
```
terraform init
```
 <span data-ttu-id="404b1-117">為 Azure 初始化 Terraform 提供者。</span><span class="sxs-lookup"><span data-stu-id="404b1-117">to initialize the Terraform provider for Azure.</span></span> <span data-ttu-id="404b1-118">然後將目錄變更為 **terraformscripts**，並發出下列命令：</span><span class="sxs-lookup"><span data-stu-id="404b1-118">Then change the directory to **terraformscripts**, and issue the following command:</span></span>
```
terraform plan
```
<span data-ttu-id="404b1-119">我們使用 `plan` Terraform 命令，該命令會查看指令碼中定義的資源。</span><span class="sxs-lookup"><span data-stu-id="404b1-119">We used the `plan` Terraform command, which looks at the resources defined in the scripts.</span></span> <span data-ttu-id="404b1-120">它會將這些資源與 Terraform 所儲存的狀態資訊進行比較，然後輸出計劃性執行，而「不需」在 Azure 中實際建立資源。</span><span class="sxs-lookup"><span data-stu-id="404b1-120">It compares them to the state information saved by Terraform and then outputs the planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="404b1-121">執行上述命令之後，您應該會看到如下列畫面的內容：</span><span class="sxs-lookup"><span data-stu-id="404b1-121">After you execute the previous command, you should see something like the following screen:</span></span>

![Terraform plan](./media/terraform/tf_plan2.png)

<span data-ttu-id="404b1-123">如果一切看起來正確無誤，請執行下列命令，在 Azure 中佈建這個新的資源群組：</span><span class="sxs-lookup"><span data-stu-id="404b1-123">If everything looks correct, provision this new resource group in Azure by executing the following:</span></span> 
```
terraform apply
```
<span data-ttu-id="404b1-124">在 Azure 入口網站中，您應該會看到名為 `terraformtest` 的新空白資源群組。</span><span class="sxs-lookup"><span data-stu-id="404b1-124">In the Azure portal, you should see the new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="404b1-125">在下一節中，您要將虛擬機器以及該虛擬機器支援的所有基礎結構新增至資源群組。</span><span class="sxs-lookup"><span data-stu-id="404b1-125">In the following section, you add a virtual machine and all the supporting infrastructure for that virtual machine to the resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="404b1-126">使用 Terraform 佈建 Ubuntu VM</span><span class="sxs-lookup"><span data-stu-id="404b1-126">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="404b1-127">我們來使用佈建執行 Ubuntu 之虛擬機器所需的詳細資料，擴充已經建立的 Terraform 指令碼。</span><span class="sxs-lookup"><span data-stu-id="404b1-127">Let's extend the Terraform script we've created with the details that are necessary to provision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="404b1-128">您在下列各節中佈建的資源包括：</span><span class="sxs-lookup"><span data-stu-id="404b1-128">The resources that you provision in the following sections are:</span></span>

* <span data-ttu-id="404b1-129">有單一子網路的網路</span><span class="sxs-lookup"><span data-stu-id="404b1-129">A network with a single subnet</span></span>
* <span data-ttu-id="404b1-130">網路介面卡</span><span class="sxs-lookup"><span data-stu-id="404b1-130">A network interface card</span></span> 
* <span data-ttu-id="404b1-131">適用於虛擬機器診斷的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="404b1-131">A storage account for the virtual machine diagnostics</span></span>
* <span data-ttu-id="404b1-132">公用 IP</span><span class="sxs-lookup"><span data-stu-id="404b1-132">A public IP</span></span>
* <span data-ttu-id="404b1-133">使用先前所有資源的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="404b1-133">A virtual machine that utilizes all the previous resources</span></span> 

<span data-ttu-id="404b1-134">如需每個 Azure Terraform 資源的完整文件，請參閱 [Terraform 文件](https://www.terraform.io/docs/providers/azurerm/index.html) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="404b1-134">For thorough documentation for each of the Azure Terraform resources, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="404b1-135">為了方便起見，也提供完整版的[佈建指令碼](#complete-terraform-script)。</span><span class="sxs-lookup"><span data-stu-id="404b1-135">The full version of the [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-the-terraform-script"></a><span data-ttu-id="404b1-136">擴充 Terraform 指令碼</span><span class="sxs-lookup"><span data-stu-id="404b1-136">Extend the Terraform script</span></span>
<span data-ttu-id="404b1-137">使用下列資源擴充建立的指令碼：</span><span class="sxs-lookup"><span data-stu-id="404b1-137">Extend the script that was created with the following resources:</span></span> 
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
<span data-ttu-id="404b1-138">上述指令碼會建立虛擬網路與該虛擬網路中的子網路。</span><span class="sxs-lookup"><span data-stu-id="404b1-138">The previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="404b1-139">請注意您已透過 "${azurerm_resource_group.helloterraform.name}" 在虛擬網路和子網路定義中建立之資源群組的參考。</span><span class="sxs-lookup"><span data-stu-id="404b1-139">Note the reference to the resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both the virtual network and the subnet definition.</span></span>

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
<span data-ttu-id="404b1-140">上述指令碼的程式碼片段會建立公用 IP，以及建立使用該公用 IP 的網路介面。</span><span class="sxs-lookup"><span data-stu-id="404b1-140">The previous script snippets create a public IP and a network interface that makes use of the public IP created.</span></span> <span data-ttu-id="404b1-141">請注意 subnet_id 和 public_ip_address_id 的參考。</span><span class="sxs-lookup"><span data-stu-id="404b1-141">Note the references to subnet_id and public_ip_address_id.</span></span> <span data-ttu-id="404b1-142">Terraform 具有內建智慧，可了解網路介面相依於在網路介面建立之前所需建立的資源。</span><span class="sxs-lookup"><span data-stu-id="404b1-142">Terraform has built-in intelligence to understand that the network interface has a dependency on the resources that need to be created before the creation of the network interface.</span></span>

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
<span data-ttu-id="404b1-143">至此您已建立了儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="404b1-143">Here, you created a storage account.</span></span> <span data-ttu-id="404b1-144">虛擬機器會將其診斷詳細資料儲存在此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="404b1-144">This storage account is where the virtual machine will store its diagnostics details.</span></span>

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
<span data-ttu-id="404b1-145">最後，先前的程式碼片段會建立虛擬機器，使用已佈建的所有資源。</span><span class="sxs-lookup"><span data-stu-id="404b1-145">Finally, the previous snippet creates a virtual machine that utilizes all the resources provisioned already.</span></span> <span data-ttu-id="404b1-146">這些資源是適用於虛擬機器診斷的儲存體帳戶、指定公用 IP 與子網路的網路介面，以及您已建立的資源群組。</span><span class="sxs-lookup"><span data-stu-id="404b1-146">They are a storage account for the virtual machine diagnostics, a network interface with public IP and subnet specified, and the resource group you already created.</span></span> <span data-ttu-id="404b1-147">請注意 vm_size 屬性，可供指令碼指定 Azure 標準 DS1v2 SKU。</span><span class="sxs-lookup"><span data-stu-id="404b1-147">Note the vm_size property, where the script specifies an Azure Standard DS1v2 SKU.</span></span>

<span data-ttu-id="404b1-148">您需要提供 SSH 公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="404b1-148">You are required to supply an SSH public key.</span></span> <span data-ttu-id="404b1-149">請將公開金鑰值放到區段 **...在此處插入 OPENSSH 公開金鑰...**上方。</span><span class="sxs-lookup"><span data-stu-id="404b1-149">Place the public key value into the section **... INSERT OPENSSH PUBLIC KEY HERE ...** above.</span></span> <span data-ttu-id="404b1-150">您可以使用現有的 ssh 金鑰組，或者依照 [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) 或 [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) 說明文件來產生金鑰組。</span><span class="sxs-lookup"><span data-stu-id="404b1-150">You can use an existing ssh key pair or follow the [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) or [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) documentation to generate the key pair.</span></span>

### <a name="execute-the-script"></a><span data-ttu-id="404b1-151">執行指令碼</span><span class="sxs-lookup"><span data-stu-id="404b1-151">Execute the script</span></span>
<span data-ttu-id="404b1-152">儲存完整的指令碼後，結束並返回主控台/命令列，然後輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="404b1-152">With the full script saved, exit to the console/command line and type the following:</span></span>
```
terraform apply
```
<span data-ttu-id="404b1-153">稍後，資源 (包括虛擬機器) 就會出現在 Azure 入口網站的 `terraformtest` 資源群組中。</span><span class="sxs-lookup"><span data-stu-id="404b1-153">After some time, the resources, including a virtual machine, appear in the `terraformtest` resource group in the Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="404b1-154">完成 Terraform 指令碼</span><span class="sxs-lookup"><span data-stu-id="404b1-154">Complete Terraform script</span></span>

<span data-ttu-id="404b1-155">為了方便起見，以下是佈建本文中所有基礎結構的完整 Terraform 指令碼。</span><span class="sxs-lookup"><span data-stu-id="404b1-155">For your convenience, below is the complete Terraform script that provisions all of the infrastructure discussed in this article.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="404b1-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="404b1-156">Next steps</span></span>
<span data-ttu-id="404b1-157">您已使用 Terraform 在 Azure 中建立基本基礎結構。</span><span class="sxs-lookup"><span data-stu-id="404b1-157">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="404b1-158">如需更多複雜案例 (包括使用負載平衡器、虛擬機器擴展集的範例)，請參閱許多[適用於 Azure 的 Terraform 範例](https://github.com/hashicorp/terraform/tree/master/examples)。</span><span class="sxs-lookup"><span data-stu-id="404b1-158">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="404b1-159">如需支援的 Azure 提供者最新清單，請參閱 [Terraform 文件](https://www.terraform.io/docs/providers/azurerm/index.html) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="404b1-159">For an up-to-date list of supported Azure providers, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
