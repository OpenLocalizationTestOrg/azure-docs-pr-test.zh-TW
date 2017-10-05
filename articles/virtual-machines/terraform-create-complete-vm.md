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
ms.openlocfilehash: 9660a95b440c2e4311829979e270d9f10099f624
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="2fd9f-103">在 Azure 中使用 Terraform 建立基本基礎結構</span><span class="sxs-lookup"><span data-stu-id="2fd9f-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="2fd9f-104">本文說明將虛擬機器和基礎結構佈建至 Azure 需進行的步驟。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-104">This article describes the steps you need to take to provision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="2fd9f-105">您將了解如何撰寫 Terraform 指令碼，以及如何在雲端基礎結構中進行變更前將其視覺化。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-105">You will learn how to write Terraform scripts and how to visualize the changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="2fd9f-106">您也將了解如何在 Azure 中使用 Terraform 建立基礎結構。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-106">You also will learn how to create infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="2fd9f-107">首先，在您所選的文字編輯器 (Visual Studio Code/Sublime/Vim/等等) 中，建立名為 \terraform_azure101.tf 的檔案。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-107">To get started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="2fd9f-108">檔案的確切名稱並不重要，因為 Terraform 接受以資料夾名稱作為參數：資料夾中的所有指令碼都會執行。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-108">The exact name of the file isn't important because Terraform accepts the folder name as a parameter: all scripts in the folder get executed.</span></span> <span data-ttu-id="2fd9f-109">將下列程式碼貼到新檔案中：</span><span class="sxs-lookup"><span data-stu-id="2fd9f-109">Paste the following code in the new file:</span></span>

~~~~
# Configure the Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have to include this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group 
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
<span data-ttu-id="2fd9f-110">在指令碼的 `provider` 區段中，您可以告訴 Terraform 使用 Azure 提供者在指令碼中佈建資源。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-110">In the `provider` section of the script, you tell Terraform to use an Azure provider to provision resources in the script.</span></span> <span data-ttu-id="2fd9f-111">若要取得 subscription_id、appId、password、and tenant_id 的值，請參閱[安裝和設定 Terraform](terraform-install-configure.md) 指南。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-111">To get values for subscription_id, appId, password, and tenant_id, see the [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="2fd9f-112">如果您已為此區塊中的值建立環境變數，就不需要將其納入。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-112">If you have created environment variables for the values in this block, you don't need to include it.</span></span> 

<span data-ttu-id="2fd9f-113">`azurerm_resource_group` 資源指示 Terraform 建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-113">The `azurerm_resource_group` resource instructs Terraform to create a new resource group.</span></span> <span data-ttu-id="2fd9f-114">您可以在本文稍後看到更多在 Terraform 中可用的資源類型。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-the-script"></a><span data-ttu-id="2fd9f-115">執行指令碼</span><span class="sxs-lookup"><span data-stu-id="2fd9f-115">Execute the script</span></span>
<span data-ttu-id="2fd9f-116">儲存指令碼之後，結束並返回主控台/命令列，然後輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="2fd9f-116">After you save the script, exit to the console/command line, and type the following:</span></span>
```
terraform init
```
<span data-ttu-id="2fd9f-117">為 Azure 初始化 Terraform 提供者。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-117">to initialize Terraform provider for Azure.</span></span> <span data-ttu-id="2fd9f-118">接著輸入下列內容：</span><span class="sxs-lookup"><span data-stu-id="2fd9f-118">Then type the following:</span></span>
```
terraform plan terraformscripts
```
<span data-ttu-id="2fd9f-119">我們假設 `terraformscripts` 是儲存指令碼的資料夾。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-119">We assume that `terraformscripts` is the folder where the script was saved.</span></span> <span data-ttu-id="2fd9f-120">我們使用 `plan` Terraform 命令，該命令會查看指令碼中定義的資源。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-120">We used the `plan` Terraform command, which looks at the resources defined in the scripts.</span></span> <span data-ttu-id="2fd9f-121">它會將這些資源與 Terraform 所儲存的狀態資訊進行比較，然後輸出計劃性執行，而「不需」在 Azure 中實際建立資源。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-121">It compares them to the state information saved by Terraform and then outputs the planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="2fd9f-122">執行上述命令之後，您應該會看到如下列畫面的內容：</span><span class="sxs-lookup"><span data-stu-id="2fd9f-122">After you execute the previous command, you should see something like the following screen:</span></span>

![Terraform plan](linux/media/terraform/tf_plan2.png)

<span data-ttu-id="2fd9f-124">如果一切看起來正確無誤，請執行下列命令，在 Azure 中佈建這個新的資源群組：</span><span class="sxs-lookup"><span data-stu-id="2fd9f-124">If everything looks correct, provision this new resource group in Azure by executing the following:</span></span> 
```
terraform apply terraformscripts
```
<span data-ttu-id="2fd9f-125">在 Azure 入口網站中，您應該會看到名為 `terraformtest` 的新空白資源群組。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-125">In the Azure portal, you should see the new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="2fd9f-126">在下一節中，您要將虛擬機器以及該虛擬機器支援的所有基礎結構新增至資源群組。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-126">In the following section, you add a virtual machine and all the supporting infrastructure for that virtual machine to the resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="2fd9f-127">使用 Terraform 佈建 Ubuntu VM</span><span class="sxs-lookup"><span data-stu-id="2fd9f-127">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="2fd9f-128">我們來使用佈建執行 Ubuntu 之虛擬機器所需的詳細資料，擴充已經建立的 Terraform 指令碼。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-128">Let's extend the Terraform script we've created with the details that are necessary to provision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="2fd9f-129">您在下列各節中佈建的資源包括：</span><span class="sxs-lookup"><span data-stu-id="2fd9f-129">The resources that you provision in the following sections are:</span></span>

* <span data-ttu-id="2fd9f-130">有單一子網路的網路</span><span class="sxs-lookup"><span data-stu-id="2fd9f-130">A network with a single subnet</span></span>
* <span data-ttu-id="2fd9f-131">網路介面卡</span><span class="sxs-lookup"><span data-stu-id="2fd9f-131">A network interface card</span></span> 
* <span data-ttu-id="2fd9f-132">有儲存體容器的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="2fd9f-132">A storage account with a storage container</span></span>
* <span data-ttu-id="2fd9f-133">公用 IP</span><span class="sxs-lookup"><span data-stu-id="2fd9f-133">A public IP</span></span>
* <span data-ttu-id="2fd9f-134">使用先前所有資源的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2fd9f-134">A virtual machine that utilizes all the previous resources</span></span> 

<span data-ttu-id="2fd9f-135">如需每個 Azure Terraform 資源的完整文件，請參閱 [Terraform 文件](https://www.terraform.io/docs/providers/azurerm/index.html) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-135">For thorough documentation for each of the Azure Terraform resources, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="2fd9f-136">為了方便起見，也提供完整版的[佈建指令碼](#complete-terraform-script)。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-136">The full version of the [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-the-terraform-script"></a><span data-ttu-id="2fd9f-137">擴充 Terraform 指令碼</span><span class="sxs-lookup"><span data-stu-id="2fd9f-137">Extend the Terraform script</span></span>
<span data-ttu-id="2fd9f-138">使用下列資源擴充建立的指令碼：</span><span class="sxs-lookup"><span data-stu-id="2fd9f-138">Extend the script that was created with the following resources:</span></span> 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
<span data-ttu-id="2fd9f-139">上述指令碼會建立虛擬網路與該虛擬網路中的子網路。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-139">The previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="2fd9f-140">請注意您已透過 "${azurerm_resource_group.helloterraform.name}" 在虛擬網路和子網路定義中建立之資源群組的參考。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-140">Note the reference to the resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both the virtual network and the subnet definition.</span></span>

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
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
}
~~~~
<span data-ttu-id="2fd9f-141">上述指令碼的程式碼片段會建立公用 IP，以及建立使用該公用 IP 的網路介面。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-141">The previous script snippets create a public IP and a network interface that makes use of the public IP created.</span></span> <span data-ttu-id="2fd9f-142">請注意 subnet_id 和 public_ip_address_id 的參考。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-142">Note the references to subnet_id and public_ip_address_id.</span></span> <span data-ttu-id="2fd9f-143">Terraform 具有內建智慧，可了解網路介面相依於在網路介面建立之前所需建立的資源。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-143">Terraform has built-in intelligence to understand that the network interface has a dependency on the resources that need to be created before the creation of the network interface.</span></span>

~~~~
# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}
~~~~
<span data-ttu-id="2fd9f-144">現在，您建立了儲存體帳戶，並且在該儲存體帳戶內定義了儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-144">Here, you created a storage account and defined a storage container within that storage account.</span></span> <span data-ttu-id="2fd9f-145">此儲存體帳戶是您為要建立的虛擬機器存放虛擬硬碟 (VHD) 的位置。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-145">This storage account is where you store virtual hard disks (VHDs) for the virtual machine about to be created.</span></span>

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
~~~~
<span data-ttu-id="2fd9f-146">最後，先前的程式碼片段會建立虛擬機器，使用已佈建的所有資源。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-146">Finally, the previous snippet creates a virtual machine that utilizes all the resources provisioned already.</span></span> <span data-ttu-id="2fd9f-147">這些資源是儲存體帳戶和 VHD 的容器、指定公用 IP 與子網路的網路介面，以及您已建立的資源群組。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-147">They are a storage account and container for a VHD, a network interface with public IP and subnet specified, and the resource group you already created.</span></span> <span data-ttu-id="2fd9f-148">請注意 vm_size 屬性，可供指令碼指定 Azure A0 SKU。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-148">Note the vm_size property, where the script specifies an Azure A0 SKU.</span></span>

### <a name="execute-the-script"></a><span data-ttu-id="2fd9f-149">執行指令碼</span><span class="sxs-lookup"><span data-stu-id="2fd9f-149">Execute the script</span></span>
<span data-ttu-id="2fd9f-150">儲存完整的指令碼後，結束並返回主控台/命令列，然後輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="2fd9f-150">With the full script saved, exit to the console/command line and type the following:</span></span>
```
terraform apply terraformscripts
```
<span data-ttu-id="2fd9f-151">稍後，資源 (包括虛擬機器) 就會出現在 Azure 入口網站的 `terraformtest` 資源群組中。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-151">After some time, the resources, including a virtual machine, appear in the `terraformtest` resource group in the Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="2fd9f-152">完成 Terraform 指令碼</span><span class="sxs-lookup"><span data-stu-id="2fd9f-152">Complete Terraform script</span></span>

<span data-ttu-id="2fd9f-153">為了方便起見，以下是佈建本文中所有基礎結構的完整 Terraform 指令碼。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-153">For your convenience, below is the complete Terraform script that provisions all of the infrastructure discussed in this article.</span></span>

```
variable "resourcesname" {
  default = "helloterraform"
}

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

# create virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "tfvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "tfsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}


# create public IPs
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
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
}

# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="2fd9f-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2fd9f-154">Next steps</span></span>
<span data-ttu-id="2fd9f-155">您已使用 Terraform 在 Azure 中建立基本基礎結構。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-155">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="2fd9f-156">如需更多複雜案例 (包括使用負載平衡器、虛擬機器擴展集的範例)，請參閱許多[適用於 Azure 的 Terraform 範例](https://github.com/hashicorp/terraform/tree/master/examples)。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-156">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="2fd9f-157">如需支援的 Azure 提供者最新清單，請參閱 [Terraform 文件](https://www.terraform.io/docs/providers/azurerm/index.html) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="2fd9f-157">For an up-to-date list of supported Azure providers, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
