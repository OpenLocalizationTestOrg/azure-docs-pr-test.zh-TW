---
title: "aaaCreate 具有多個 Nic-Azure CLI 1.0 的 VM （傳統） |Microsoft 文件"
description: "了解 toocreate 具有使用多個 Nic 的 VM （傳統） hello Azure 命令列介面 (CLI) 1.0 的方式。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b436e41e-866c-439f-a7c7-7b4b041725ef
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 181bfb28027caff33410ca94744e79206a2a0d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a>建立與使用 Azure CLI 1.0 hello 的多個 Nic VM （傳統）

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

您可以在 Azure 中建立虛擬機器 (Vm)，並附加多個網路介面 (Nic) tooeach 的 Vm。 有多個 NIC 時，可透過各個 NIC 分隔不同的流量類型。 例如，一個 NIC 通訊 hello 網際網路，而另一個不只與內部資源通訊連接 toohello 網際網路。 許多網路虛擬應用裝置，例如應用程式傳遞和 WAN 最佳化解決方案需要 hello 能力 tooseparate 跨多個 Nic 的網路流量。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。 本文說明如何使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 深入了解如何 tooperform 這些步驟使用 hello [Resource Manager 部署模型](virtual-network-deploy-multinic-arm-cli.md)。

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

hello 下列步驟使用的資源群組名稱為*IaaSStory* hello 網頁伺服器和資源群組名稱為*IaaSStory 後端*hello DB 伺服器。

## <a name="prerequisites"></a>必要條件
您可以建立 hello DB 伺服器之前，您需要 toocreate hello *IaaSStory*此案例中的 hello 必要資源與資源群組。 toocreate 這些資源，完成 hello 遵循的步驟。 建立虛擬網路中 hello 的 hello 步驟[建立虛擬網路](virtual-networks-create-vnet-classic-cli.md)發行項。

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a>部署 hello 後端 Vm
後端 Vm 相依於下列資源的 hello hello 建立 hello:

* **資料磁碟的儲存體帳戶**。 為提升效能，hello hello 資料庫伺服器上的資料磁碟會使用固態硬碟 (SSD) 技術，需要進階儲存體帳戶。 請確定 hello 部署 toosupport 高階儲存體的 Azure 位置。
* **NIC**。 每部 VM 都會有兩個 NIC，一個用於資料庫存取，另一個用於管理。
* **可用性設定組**。 所有資料庫伺服器將會都加入 tooa 一個可用性設定組，其中至少一個 hello Vm tooensure 已啟動並執行在維護期間。

### <a name="step-1---start-your-script"></a>步驟 1：啟動指令碼
您可以下載 hello 完整 bash 指令碼使用[這裡](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh)。 完成下列步驟 toochange hello 指令碼 toowork 您環境中的 hello:

1. 變更 hello hello 變數值以下根據您現有的資源群組，在上面部署[必要條件](#Prerequisites)。

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. 變更 hello 值 hello 變數的下列根據 hello 值要 toouse 後端部署。

    ```azurecli
    backendCSName="IaaSStory-Backend"
    prmStorageAccountName="iaasstoryprmstorage"
    image="0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskPrefix="db"
    dataDiskName="datadisk"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a>步驟 2：為 VM 建立必要的資源
1. 為所有後端 VM 建立新的雲端服務。 請注意 hello 使用 hello `$backendCSName` hello 資源群組名稱 中的變數和`$location`hello Azure 區域。

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. 建立 hello OS 的進階儲存體帳戶和您的 Vm 所使用的資料磁碟 toobe。

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a>步驟 3：建立具有多個 NIC 的 VM
1. 啟動多個 Vm，根據 hello 迴圈 toocreate`numberOfVMs`變數。

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. 針對每個 VM 中，指定 hello 名稱和每個 hello 兩個 Nic 的 IP 位址。

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. 建立 hello VM。 請注意 hello 使用量的 hello`--nic-config`參數，其中包含所有 Nic 具有名稱、 子網路和 IP 位址的清單。

    ```azurecli
    azure vm create $backendCSName $image $username $password \
        --connect $backendCSName \
        --vm-name $vmNamePrefix$suffixNumber \
        --vm-size $vmSize \
        --availability-set $avSetName \
        --blob-url $prmStorageAccountName.blob.core.windows.net/vhds/$osDiskName$suffixNumber.vhd \
        --virtual-network-name $vnetName \
        --subnet-names $backendSubnetName \
        --nic-config $nic1Name:$backendSubnetName:$ipAddress1::,$nic2Name:$backendSubnetName:$ipAddress2::
    ```

4. 針對每個 VM，請建立兩個資料磁碟。

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a>步驟 4-執行 hello 指令碼
既然您已下載並變更您的需求，執行 hello 指令碼 toocreate hello 備份為基礎的 hello 指令碼會結束資料庫具有多個 Nic 的 Vm。

1. 儲存您的指令碼並從 **Bash** 終端機執行。 您會看到 hello 初始輸出，如下所示。

        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name IaaSStory-Backend
        info:    service create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM

2. 請稍候幾分鐘 hello 執行將結束，您會看到 hello 其餘 hello 輸出如下所示。

        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM
        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
