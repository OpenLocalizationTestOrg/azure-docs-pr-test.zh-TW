---
title: "具有多個 IP 位址使用 hello Azure CLI 1.0 aaaVM |Microsoft 文件"
description: "了解如何 tooassign 多個 IP 位址 tooa 虛擬機器使用 hello Azure CLI 1.0 |資源管理員。"
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a><span data-ttu-id="54303-103">使用 Azure CLI 1.0 toovirtual 機器指派多個 IP 位址</span><span class="sxs-lookup"><span data-stu-id="54303-103">Assign multiple IP addresses toovirtual machines using Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="54303-104">本文說明如何透過 hello Azure Resource Manager 部署模型使用的虛擬機器 (VM) toocreate hello Azure CLI 1.0。</span><span class="sxs-lookup"><span data-stu-id="54303-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 1.0.</span></span> <span data-ttu-id="54303-105">Tooresources 透過 hello 傳統部署模型所建立，無法指派多個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="54303-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="54303-106">深入了解 Azure 的部署模型，讀取 hello toolearn[了解部署模型](../resource-manager-deployment-model.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="54303-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="54303-107"><a name = "create"></a>建立有多個 IP 位址的 VM</span><span class="sxs-lookup"><span data-stu-id="54303-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="54303-108">您可以完成這項工作中使用 Azure CLI 1.0 （即本文） hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="54303-108">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span></span> <span data-ttu-id="54303-109">hello 遵循的步驟說明如何 toocreate 範例 VM 具有多個 IP 位址，hello 案例中所述。</span><span class="sxs-lookup"><span data-stu-id="54303-109">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="54303-110">視您的實作而定，變更變數名稱和 IP 位址類型。</span><span class="sxs-lookup"><span data-stu-id="54303-110">Change variable names and IP address types as required for your implementation.</span></span>

1. <span data-ttu-id="54303-111">在安裝和設定步驟的下列 hello Azure CLI 1.0 hello hello[安裝及設定 hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)文件和登入您的 Azure 帳戶以 hello`azure-login`命令。</span><span class="sxs-lookup"><span data-stu-id="54303-111">Install and configure hello Azure CLI 1.0 by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with hello `azure-login` command.</span></span>

2. <span data-ttu-id="54303-112">建立資源群組：</span><span class="sxs-lookup"><span data-stu-id="54303-112">Create a resource group:</span></span>
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. <span data-ttu-id="54303-113">建立虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="54303-113">Create a virtual network:</span></span>

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. <span data-ttu-id="54303-114">建立 hello 虛擬網路子網路：</span><span class="sxs-lookup"><span data-stu-id="54303-114">Create a subnet in hello virtual network:</span></span>

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. <span data-ttu-id="54303-115">建立 hello VM 的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="54303-115">Create  a storage account for hello VM.</span></span> <span data-ttu-id="54303-116">下列命令，取代執行 hello 之前*mystorageaccount*具有唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="54303-116">Before running hello following command, replace *mystorageaccount* with a unique name.</span></span> <span data-ttu-id="54303-117">hello 名稱必須是唯一的 Azure:</span><span class="sxs-lookup"><span data-stu-id="54303-117">hello name must be unique across Azure:</span></span>

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. <span data-ttu-id="54303-118">建立 hello IP 組態，NIC，並指派 hello IP 組態 toohello nic。</span><span class="sxs-lookup"><span data-stu-id="54303-118">Create hello IP configurations, a NIC, and assign hello IP configurations toohello NIC.</span></span> <span data-ttu-id="54303-119">您可以新增、 移除或變更視 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="54303-119">You can add, remove, or change hello configurations as necessary.</span></span> <span data-ttu-id="54303-120">hello 案例描述 hello 的設定：</span><span class="sxs-lookup"><span data-stu-id="54303-120">hello following configurations are described in hello scenario:</span></span>

    <span data-ttu-id="54303-121">**IPConfig-1**</span><span class="sxs-lookup"><span data-stu-id="54303-121">**IPConfig-1**</span></span>

    <span data-ttu-id="54303-122">輸入遵循 toocreate hello 命令：</span><span class="sxs-lookup"><span data-stu-id="54303-122">Enter hello commands that follow toocreate:</span></span>

    - <span data-ttu-id="54303-123">使用靜態公用 IP 位址的公用 IP 位址資源</span><span class="sxs-lookup"><span data-stu-id="54303-123">A public IP address resource with a static public IP address</span></span>
    - <span data-ttu-id="54303-124">指派 hello 公用 IP 位址和靜態私人 IP 位址 tooit NIC。</span><span class="sxs-lookup"><span data-stu-id="54303-124">A NIC, assigning hello public IP address and a static private IP address tooit.</span></span>
    
    <span data-ttu-id="54303-125">取代*mypublicdns* hello Azure 位置內必須是唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="54303-125">Replace *mypublicdns* with a name that is unique within hello Azure location.</span></span>

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > <span data-ttu-id="54303-126">公用 IP 位址需要少許費用。</span><span class="sxs-lookup"><span data-stu-id="54303-126">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="54303-127">進一步瞭解 IP 位址定價，toolearn 讀取 hello [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses)頁面。</span><span class="sxs-lookup"><span data-stu-id="54303-127">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="54303-128">沒有可用的訂用帳戶中的公用 IP 位址限制 toohello 數目。</span><span class="sxs-lookup"><span data-stu-id="54303-128">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="54303-129">深入了解 hello 限制、 讀取 hello toolearn [Azure 限制](../azure-subscription-service-limits.md#networking-limits)發行項。</span><span class="sxs-lookup"><span data-stu-id="54303-129">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    <span data-ttu-id="54303-130">**IPConfig-2**</span><span class="sxs-lookup"><span data-stu-id="54303-130">**IPConfig-2**</span></span>

     <span data-ttu-id="54303-131">新的公用 IP 位址資源與新的 IP 組態的靜態公用 IP 位址和靜態私人 IP 位址，請輸入下列命令 toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="54303-131">Enter hello following commands toocreate a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span></span>
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    <span data-ttu-id="54303-132">**IPConfig-3**</span><span class="sxs-lookup"><span data-stu-id="54303-132">**IPConfig-3**</span></span>

    <span data-ttu-id="54303-133">輸入下列命令 toocreate 靜態私人 IP 位址與任何公用 IP 位址的 IP 組態的 hello:</span><span class="sxs-lookup"><span data-stu-id="54303-133">Enter hello following commands toocreate an IP configuration with a static private IP address and no public IP address:</span></span>

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    ><span data-ttu-id="54303-134">雖然這篇文章會指派所有 IP 組態 tooa 單一 NIC，您也可以指派多個 IP 組態 tooany NIC 的 VM 中。</span><span class="sxs-lookup"><span data-stu-id="54303-134">Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations tooany NIC in a VM.</span></span> <span data-ttu-id="54303-135">toolearn toocreate 具有多個 Nic，VM 讀取方式 hello 建立具有多個 Nic 的發行項的 VM。</span><span class="sxs-lookup"><span data-stu-id="54303-135">toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs article.</span></span>

7. <span data-ttu-id="54303-136">建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="54303-136">Create a Linux VM</span></span> 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    <span data-ttu-id="54303-137">toochange hello VM 大小 tooStandard DS2 v2，比方說，只要加入下列屬性的 hello `--vm-size Standard_DS3_v2` toohello`azure vm create`命令在步驟 6。</span><span class="sxs-lookup"><span data-stu-id="54303-137">toochange hello VM size tooStandard DS2 v2, for example, simply add hello following property `--vm-size Standard_DS3_v2` toohello `azure vm create` command in step 6.</span></span>

8. <span data-ttu-id="54303-138">輸入下列命令 tooview hello NIC hello 和 hello 相關聯的 IP 設定：</span><span class="sxs-lookup"><span data-stu-id="54303-138">Enter hello following command tooview hello NIC and hello associated IP configurations:</span></span>

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. <span data-ttu-id="54303-139">新增 hello 私人 IP 位址 toohello VM 作業系統 hello hello 作業系統的步驟，以[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。</span><span class="sxs-lookup"><span data-stu-id="54303-139">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="54303-140"><a name="add"></a>新增 IP 位址 tooa VM</span><span class="sxs-lookup"><span data-stu-id="54303-140"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="54303-141">您可以加入其他私人和公用 IP 位址 tooan 現有 NIC 的完成 hello 遵循的步驟。</span><span class="sxs-lookup"><span data-stu-id="54303-141">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="54303-142">hello 範例是根據 hello[案例](#Scenario)本文中所述。</span><span class="sxs-lookup"><span data-stu-id="54303-142">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="54303-143">開啟 Azure CLI，並完成剩餘步驟，本節中的單一的 CLI 工作階段內的 hello。</span><span class="sxs-lookup"><span data-stu-id="54303-143">Open Azure CLI and complete hello remaining steps in this section within a single CLI session.</span></span> <span data-ttu-id="54303-144">如果您還沒有安裝和設定 Azure CLI，完成 hello 步驟 hello[安裝及設定 hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)文件和登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="54303-144">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span></span>

2. <span data-ttu-id="54303-145">完成下列各節，您的需求為基礎的 hello 的其中一個 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="54303-145">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    - <span data-ttu-id="54303-146">**新增私人 IP 位址**</span><span class="sxs-lookup"><span data-stu-id="54303-146">**Add a private IP address**</span></span>
    
        <span data-ttu-id="54303-147">tooadd 私用 IP 位址 tooa NIC，您必須建立使用下方的 hello 命令的 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="54303-147">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command below.</span></span> <span data-ttu-id="54303-148">hello 靜態位址必須是未使用的 hello 子網路位址。</span><span class="sxs-lookup"><span data-stu-id="54303-148">hello static address must be an unused address for hello subnet.</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        <span data-ttu-id="54303-149">使用唯一組態名稱和私人 IP 位址 (適用於具有靜態 IP 位址的組態)，視需要建立最多的組態。</span><span class="sxs-lookup"><span data-stu-id="54303-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    - <span data-ttu-id="54303-150">**新增公用 IP 位址**</span><span class="sxs-lookup"><span data-stu-id="54303-150">**Add a public IP address**</span></span>
    
        <span data-ttu-id="54303-151">公用 IP 位址會藉由將它 tooeither 加入新的 IP 設定或現有的 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="54303-151">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="54303-152">視需要完成 hello hello 以下各節，其中的步驟。</span><span class="sxs-lookup"><span data-stu-id="54303-152">Complete hello steps in one of hello sections that follow, as you require.</span></span>

        > [!NOTE]
        > <span data-ttu-id="54303-153">公用 IP 位址需要少許費用。</span><span class="sxs-lookup"><span data-stu-id="54303-153">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="54303-154">進一步瞭解 IP 位址定價，toolearn 讀取 hello [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses)頁面。</span><span class="sxs-lookup"><span data-stu-id="54303-154">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="54303-155">沒有可用的訂用帳戶中的公用 IP 位址限制 toohello 數目。</span><span class="sxs-lookup"><span data-stu-id="54303-155">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="54303-156">深入了解 hello 限制、 讀取 hello toolearn [Azure 限制](../azure-subscription-service-limits.md#networking-limits)發行項。</span><span class="sxs-lookup"><span data-stu-id="54303-156">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
        >

        <span data-ttu-id="54303-157">**關聯的 hello 資源 tooa 新的 IP 設定**</span><span class="sxs-lookup"><span data-stu-id="54303-157">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="54303-158">每當您在新的 IP 組態中新增公用 IP 位址時，也必須新增私人 IP 位址，因為所有的 IP 組態都必須有一個私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="54303-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="54303-159">您可以新增現有的公用 IP 位址資源，或建立一個新的資源。</span><span class="sxs-lookup"><span data-stu-id="54303-159">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="54303-160">toocreate 一個新輸入 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="54303-160">toocreate a new one, enter hello following command:</span></span>

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        <span data-ttu-id="54303-161">新的 IP 設定，以靜態私人 IP 位址和相關聯的 hello toocreate *myPublicIP3*公用 IP 位址資源，請輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="54303-161">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        <span data-ttu-id="54303-162">**關聯的 hello 資源 tooan 現有 IP 組態**</span><span class="sxs-lookup"><span data-stu-id="54303-162">**Associate hello resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="54303-163">公用 IP 位址資源只能是關聯的 tooan 還沒有相關聯的 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="54303-163">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="54303-164">您可以判斷 IP 組態是否有相關聯的公用 IP 位址，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="54303-164">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        <span data-ttu-id="54303-165">尋找列類似 toohello 稍後 IPConfig 3 hello 傳回輸出的其中一個：</span><span class="sxs-lookup"><span data-stu-id="54303-165">Look for a line similar toohello one that follows for IPConfig-3 in hello returned output:</span></span>

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        <span data-ttu-id="54303-166">因為 hello**公用 IP**資料行*IpConfig 3*是空白的沒有公用 IP 位址資源是 tooit 目前相關聯。</span><span class="sxs-lookup"><span data-stu-id="54303-166">Since hello **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="54303-167">您可以新增現有公用 IP 位址資源 tooIpConfig-3，或輸入下列其中一個命令 toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="54303-167">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        <span data-ttu-id="54303-168">輸入下列命令 tooassociate hello 公用 IP 位址資源 toohello 現有 IP 設定名為 hello *IPConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="54303-168">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. <span data-ttu-id="54303-169">檢視 hello 私人 IP 位址和 hello 公用 IP 位址資源指派的 toohello NIC 輸入 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="54303-169">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      <span data-ttu-id="54303-170">hello 傳回輸出，則為類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="54303-170">hello returned output is similar toohello following:</span></span>
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. <span data-ttu-id="54303-171">新增 hello 的私人 IP 位址新增 toohello NIC toohello VM 作業系統的 hello 中的 hello 指示[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。</span><span class="sxs-lookup"><span data-stu-id="54303-171">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="54303-172">請勿將 hello 公用 IP 位址 toohello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="54303-172">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
