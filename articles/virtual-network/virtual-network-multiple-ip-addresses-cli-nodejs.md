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
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a>使用 Azure CLI 1.0 toovirtual 機器指派多個 IP 位址

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

本文說明如何透過 hello Azure Resource Manager 部署模型使用的虛擬機器 (VM) toocreate hello Azure CLI 1.0。 Tooresources 透過 hello 傳統部署模型所建立，無法指派多個 IP 位址。 深入了解 Azure 的部署模型，讀取 hello toolearn[了解部署模型](../resource-manager-deployment-model.md)發行項。

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>建立有多個 IP 位址的 VM

您可以完成這項工作中使用 Azure CLI 1.0 （即本文） hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md)。 hello 遵循的步驟說明如何 toocreate 範例 VM 具有多個 IP 位址，hello 案例中所述。 視您的實作而定，變更變數名稱和 IP 位址類型。

1. 在安裝和設定步驟的下列 hello Azure CLI 1.0 hello hello[安裝及設定 hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)文件和登入您的 Azure 帳戶以 hello`azure-login`命令。

2. 建立資源群組：
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. 建立虛擬網路：

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. 建立 hello 虛擬網路子網路：

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. 建立 hello VM 的儲存體帳戶。 下列命令，取代執行 hello 之前*mystorageaccount*具有唯一的名稱。 hello 名稱必須是唯一的 Azure:

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. 建立 hello IP 組態，NIC，並指派 hello IP 組態 toohello nic。 您可以新增、 移除或變更視 hello 組態。 hello 案例描述 hello 的設定：

    **IPConfig-1**

    輸入遵循 toocreate hello 命令：

    - 使用靜態公用 IP 位址的公用 IP 位址資源
    - 指派 hello 公用 IP 位址和靜態私人 IP 位址 tooit NIC。
    
    取代*mypublicdns* hello Azure 位置內必須是唯一的名稱。

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > 公用 IP 位址需要少許費用。 進一步瞭解 IP 位址定價，toolearn 讀取 hello [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses)頁面。 沒有可用的訂用帳戶中的公用 IP 位址限制 toohello 數目。 深入了解 hello 限制、 讀取 hello toolearn [Azure 限制](../azure-subscription-service-limits.md#networking-limits)發行項。

    **IPConfig-2**

     新的公用 IP 位址資源與新的 IP 組態的靜態公用 IP 位址和靜態私人 IP 位址，請輸入下列命令 toocreate hello:
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    **IPConfig-3**

    輸入下列命令 toocreate 靜態私人 IP 位址與任何公用 IP 位址的 IP 組態的 hello:

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    >雖然這篇文章會指派所有 IP 組態 tooa 單一 NIC，您也可以指派多個 IP 組態 tooany NIC 的 VM 中。 toolearn toocreate 具有多個 Nic，VM 讀取方式 hello 建立具有多個 Nic 的發行項的 VM。

7. 建立 Linux VM 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    toochange hello VM 大小 tooStandard DS2 v2，比方說，只要加入下列屬性的 hello `--vm-size Standard_DS3_v2` toohello`azure vm create`命令在步驟 6。

8. 輸入下列命令 tooview hello NIC hello 和 hello 相關聯的 IP 設定：

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. 新增 hello 私人 IP 位址 toohello VM 作業系統 hello hello 作業系統的步驟，以[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。

## <a name="add"></a>新增 IP 位址 tooa VM

您可以加入其他私人和公用 IP 位址 tooan 現有 NIC 的完成 hello 遵循的步驟。 hello 範例是根據 hello[案例](#Scenario)本文中所述。

1. 開啟 Azure CLI，並完成剩餘步驟，本節中的單一的 CLI 工作階段內的 hello。 如果您還沒有安裝和設定 Azure CLI，完成 hello 步驟 hello[安裝及設定 hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)文件和登入您的 Azure 帳戶。

2. 完成下列各節，您的需求為基礎的 hello 的其中一個 hello 步驟：

    - **新增私人 IP 位址**
    
        tooadd 私用 IP 位址 tooa NIC，您必須建立使用下方的 hello 命令的 IP 組態。 hello 靜態位址必須是未使用的 hello 子網路位址。

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        使用唯一組態名稱和私人 IP 位址 (適用於具有靜態 IP 位址的組態)，視需要建立最多的組態。

    - **新增公用 IP 位址**
    
        公用 IP 位址會藉由將它 tooeither 加入新的 IP 設定或現有的 IP 組態。 視需要完成 hello hello 以下各節，其中的步驟。

        > [!NOTE]
        > 公用 IP 位址需要少許費用。 進一步瞭解 IP 位址定價，toolearn 讀取 hello [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses)頁面。 沒有可用的訂用帳戶中的公用 IP 位址限制 toohello 數目。 深入了解 hello 限制、 讀取 hello toolearn [Azure 限制](../azure-subscription-service-limits.md#networking-limits)發行項。
        >

        **關聯的 hello 資源 tooa 新的 IP 設定**
    
        每當您在新的 IP 組態中新增公用 IP 位址時，也必須新增私人 IP 位址，因為所有的 IP 組態都必須有一個私人 IP 位址。 您可以新增現有的公用 IP 位址資源，或建立一個新的資源。 toocreate 一個新輸入 hello 下列命令：

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        新的 IP 設定，以靜態私人 IP 位址和相關聯的 hello toocreate *myPublicIP3*公用 IP 位址資源，請輸入下列命令的 hello:

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        **關聯的 hello 資源 tooan 現有 IP 組態**

        公用 IP 位址資源只能是關聯的 tooan 還沒有相關聯的 IP 組態。 您可以判斷 IP 組態是否有相關聯的公用 IP 位址，輸入下列命令的 hello:

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        尋找列類似 toohello 稍後 IPConfig 3 hello 傳回輸出的其中一個：

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        因為 hello**公用 IP**資料行*IpConfig 3*是空白的沒有公用 IP 位址資源是 tooit 目前相關聯。 您可以新增現有公用 IP 位址資源 tooIpConfig-3，或輸入下列其中一個命令 toocreate hello:

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        輸入下列命令 tooassociate hello 公用 IP 位址資源 toohello 現有 IP 設定名為 hello *IPConfig 3*:
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. 檢視 hello 私人 IP 位址和 hello 公用 IP 位址資源指派的 toohello NIC 輸入 hello 下列命令：

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      hello 傳回輸出，則為類似 toohello 下列：
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. 新增 hello 的私人 IP 位址新增 toohello NIC toohello VM 作業系統的 hello 中的 hello 指示[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。 請勿將 hello 公用 IP 位址 toohello 作業系統。

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
