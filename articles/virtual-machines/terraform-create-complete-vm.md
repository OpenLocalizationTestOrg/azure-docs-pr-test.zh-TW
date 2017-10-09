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
ms.openlocfilehash: 916a838c118f28b3fbd373188e0acb2afc655081
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="24a76-103">在 Azure 中使用 Terraform 建立基本基礎結構</span><span class="sxs-lookup"><span data-stu-id="24a76-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="24a76-104">本文將告訴您需要 tootake tooprovision 虛擬機器，以及基礎結構，到 Azure 的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="24a76-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="24a76-105">您將學習如何 toowrite Terraform 指令碼和 toovisualize hello 如何才能變更可讓這些雲端基礎結構。</span><span class="sxs-lookup"><span data-stu-id="24a76-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="24a76-106">您也將學習如何在 Azure 中使用 Terraform 的 toocreate 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="24a76-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="24a76-107">tooget 啟動，建立一個稱為 \terraform_azure101.tf 文字編輯器 （Visual Studio 程式碼/適/Vim/等等） 所選擇的檔案。</span><span class="sxs-lookup"><span data-stu-id="24a76-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="24a76-108">hello 的 hello 檔案的確切名稱不重要，因為 Terraform 接受 hello 做為參數的資料夾名稱： hello 資料夾中的所有指令碼會執行。</span><span class="sxs-lookup"><span data-stu-id="24a76-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="24a76-109">貼上下列程式碼 hello 新檔案中的 hello:</span><span class="sxs-lookup"><span data-stu-id="24a76-109">Paste hello following code in hello new file:</span></span>

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
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
<span data-ttu-id="24a76-110">在 hello `provider` hello 部分指令碼，您可告知 Terraform toouse Azure 提供者 tooprovision 資源 hello 指令碼中。</span><span class="sxs-lookup"><span data-stu-id="24a76-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="24a76-111">tooget 值 subscription_id、 appId、 密碼和 tenant_id，請參閱 hello[安裝及設定 Terraform](terraform-install-configure.md)指南。</span><span class="sxs-lookup"><span data-stu-id="24a76-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="24a76-112">如果您已經建立 hello 值的環境變數，此區塊中，您不需要 tooinclude 它。</span><span class="sxs-lookup"><span data-stu-id="24a76-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="24a76-113">hello`azurerm_resource_group`資源會指示 Terraform toocreate 新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="24a76-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="24a76-114">您可以在本文稍後看到更多在 Terraform 中可用的資源類型。</span><span class="sxs-lookup"><span data-stu-id="24a76-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="24a76-115">執行 hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="24a76-115">Execute hello script</span></span>
<span data-ttu-id="24a76-116">儲存 hello 指令碼之後，結束 toohello 主控台命令列，然後輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="24a76-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
<span data-ttu-id="24a76-117">azure tooinitialize Terraform 提供者。</span><span class="sxs-lookup"><span data-stu-id="24a76-117">tooinitialize Terraform provider for Azure.</span></span> <span data-ttu-id="24a76-118">然後輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="24a76-118">Then type hello following:</span></span>
```
terraform plan terraformscripts
```
<span data-ttu-id="24a76-119">我們假設`terraformscripts`hello 資料夾儲存 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="24a76-119">We assume that `terraformscripts` is hello folder where hello script was saved.</span></span> <span data-ttu-id="24a76-120">我們使用 hello `plan` Terraform 命令，查看 hello hello 指令碼中定義的資源。</span><span class="sxs-lookup"><span data-stu-id="24a76-120">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="24a76-121">在比較 toohello Terraform 所儲存的狀態資訊，然後輸出 hello 計劃的執行_沒有_實際上在 Azure 中建立資源。</span><span class="sxs-lookup"><span data-stu-id="24a76-121">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="24a76-122">Hello 前一個命令執行之後，您應該會看到像下列螢幕 hello:</span><span class="sxs-lookup"><span data-stu-id="24a76-122">After you execute hello previous command, you should see something like hello following screen:</span></span>

![Terraform plan](linux/media/terraform/tf_plan2.png)

<span data-ttu-id="24a76-124">如果一切正確，佈建在 Azure 中的這個新資源群組，藉由執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="24a76-124">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply terraformscripts
```
<span data-ttu-id="24a76-125">在 hello Azure 入口網站，您應該會看到 hello 新空的資源群組稱為`terraformtest`。</span><span class="sxs-lookup"><span data-stu-id="24a76-125">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="24a76-126">在 hello 下列區段，您將虛擬機器，而且所有 hello 支援該虛擬機器 toohello 資源群組的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="24a76-126">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="24a76-127">使用 Terraform 佈建 Ubuntu VM</span><span class="sxs-lookup"><span data-stu-id="24a76-127">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="24a76-128">讓我們來擴充虛擬機器執行 Ubuntu hello Terraform 指令碼，我們建立了具有必要 tooprovision hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="24a76-128">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="24a76-129">您在下列各節的 hello 佈建的 hello 資源包括：</span><span class="sxs-lookup"><span data-stu-id="24a76-129">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="24a76-130">有單一子網路的網路</span><span class="sxs-lookup"><span data-stu-id="24a76-130">A network with a single subnet</span></span>
* <span data-ttu-id="24a76-131">網路介面卡</span><span class="sxs-lookup"><span data-stu-id="24a76-131">A network interface card</span></span> 
* <span data-ttu-id="24a76-132">有儲存體容器的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="24a76-132">A storage account with a storage container</span></span>
* <span data-ttu-id="24a76-133">公用 IP</span><span class="sxs-lookup"><span data-stu-id="24a76-133">A public IP</span></span>
* <span data-ttu-id="24a76-134">虛擬機器，它會利用所有的 hello 先前的資源</span><span class="sxs-lookup"><span data-stu-id="24a76-134">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="24a76-135">如需每個 hello Azure Terraform 資源的完整文件，請參閱 hello [Terraform 文件](https://www.terraform.io/docs/providers/azurerm/index.html)。</span><span class="sxs-lookup"><span data-stu-id="24a76-135">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="24a76-136">hello 完整版的 hello[佈建指令碼](#complete-terraform-script)也為了方便起見。</span><span class="sxs-lookup"><span data-stu-id="24a76-136">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="24a76-137">擴充 hello Terraform 指令碼</span><span class="sxs-lookup"><span data-stu-id="24a76-137">Extend hello Terraform script</span></span>
<span data-ttu-id="24a76-138">擴充 hello 下列資源以建立 hello 指令碼：</span><span class="sxs-lookup"><span data-stu-id="24a76-138">Extend hello script that was created with hello following resources:</span></span> 
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
<span data-ttu-id="24a76-139">hello 至上一個指令碼會建立虛擬網路與該虛擬網路中的子網路。</span><span class="sxs-lookup"><span data-stu-id="24a76-139">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="24a76-140">請注意您已經建立透過 hello 虛擬網路和 hello 子網路定義中的"${azurerm_resource_group.helloterraform.name}"hello 參考 toohello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="24a76-140">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

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
<span data-ttu-id="24a76-141">hello 先前的指令碼片段會建立公用 IP 與網路介面，可利用建立 hello 公用 IP。</span><span class="sxs-lookup"><span data-stu-id="24a76-141">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="24a76-142">請注意 hello 參考 toosubnet_id public_ip_address_id。</span><span class="sxs-lookup"><span data-stu-id="24a76-142">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="24a76-143">Terraform 具有內建智慧 toounderstand hello 該網路介面具有相依性 hello 資源建立 hello hello 網路介面建立之前，需要 toobe。</span><span class="sxs-lookup"><span data-stu-id="24a76-143">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

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
<span data-ttu-id="24a76-144">現在，您建立了儲存體帳戶，並且在該儲存體帳戶內定義了儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="24a76-144">Here, you created a storage account and defined a storage container within that storage account.</span></span> <span data-ttu-id="24a76-145">這個儲存體帳戶是您用來儲存虛擬硬碟 (Vhd) hello toobe 建立相關的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="24a76-145">This storage account is where you store virtual hard disks (VHDs) for hello virtual machine about toobe created.</span></span>

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
<span data-ttu-id="24a76-146">最後，hello 先前程式碼片段會建立虛擬機器，它會利用所有已佈建的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="24a76-146">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="24a76-147">它們是儲存體帳戶和容器的 VHD，網路介面與公用 IP 子網路指定，而且 hello 資源群組已建立。</span><span class="sxs-lookup"><span data-stu-id="24a76-147">They are a storage account and container for a VHD, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="24a76-148">請注意 hello vm_size 屬性，其中 hello 指令碼會指定 Azure A0 SKU。</span><span class="sxs-lookup"><span data-stu-id="24a76-148">Note hello vm_size property, where hello script specifies an Azure A0 SKU.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="24a76-149">執行 hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="24a76-149">Execute hello script</span></span>
<span data-ttu-id="24a76-150">Hello 儲存了完整的指令碼，結束 toohello 主控台/命令列與 hello 下列輸入：</span><span class="sxs-lookup"><span data-stu-id="24a76-150">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply terraformscripts
```
<span data-ttu-id="24a76-151">一段時間後 hello 資源，包括虛擬機器時，會出現在 hello `terraformtest` hello Azure 入口網站中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="24a76-151">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="24a76-152">完成 Terraform 指令碼</span><span class="sxs-lookup"><span data-stu-id="24a76-152">Complete Terraform script</span></span>

<span data-ttu-id="24a76-153">為了方便起見，以下是 hello 完整 Terraform 指令碼來佈建所有 hello 基礎結構的本文中所討論。</span><span class="sxs-lookup"><span data-stu-id="24a76-153">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

```
variable "resourcesname" {
  default = "helloterraform"
}

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

## <a name="next-steps"></a><span data-ttu-id="24a76-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="24a76-154">Next steps</span></span>
<span data-ttu-id="24a76-155">您已使用 Terraform 在 Azure 中建立基本基礎結構。</span><span class="sxs-lookup"><span data-stu-id="24a76-155">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="24a76-156">如需更多複雜案例 (包括使用負載平衡器、虛擬機器擴展集的範例)，請參閱許多[適用於 Azure 的 Terraform 範例](https://github.com/hashicorp/terraform/tree/master/examples)。</span><span class="sxs-lookup"><span data-stu-id="24a76-156">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="24a76-157">支援的 Azure 提供者的最新清單，請參閱 hello [Terraform 文件](https://www.terraform.io/docs/providers/azurerm/index.html)。</span><span class="sxs-lookup"><span data-stu-id="24a76-157">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
