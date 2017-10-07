---
title: "適用於 Vm （傳統）-Azure CLI 1.0 aaaConfigure 私人 IP 位址 |Microsoft 文件"
description: "了解 tooconfigure 私人 IP 位址的虛擬機器 （傳統） 使用 hello Azure 命令列介面 (CLI) 1.0 的方式。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a>設定私人 IP 位址使用 hello Azure CLI 1.0 為虛擬機器 （傳統）

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

本文涵蓋 hello 傳統部署模型。 您也可以[管理 hello Resource Manager 部署模型中的靜態私人 IP 位址](virtual-networks-static-private-ip-arm-cli.md)。

下列的 hello 範例 Azure CLI 命令預期簡單的環境中已經建立。 如果您想 toorun hello 命令，因為它們會顯示在此文件，第一次建立 hello 測試環境中所述[建立 vnet](virtual-networks-create-vnet-classic-cli.md)。

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>如何 toospecify 靜態私人 IP 位址建立 VM 時
名為的新 VM toocreate *DNS01*新的雲端服務中名為*TestService*根據上面的 hello 案例，請遵循下列步驟：

1. 如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。
2. 執行 hello **azure 服務建立**命令 toocreate hello 雲端服務。
   
        azure service create TestService --location uscentral
   
    預期的輸出：
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. 執行 hello **azure 建立的 vm**命令 toocreate hello VM。 請注意 hello 靜態私人 IP 位址的值。 之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    預期的輸出：
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * **-l (或 --location)**。 將會建立 hello VM 的 azure 區域。 在本文案例中為 *centralus*。
   * **-n (或 --vm-name)**。 建立 hello VM toobe 的名稱。
   * **-w (或 --virtual-network-name)**。 Hello hello VM 將會建立的 VNet 的名稱。 
   * **-S (或 --static-ip)**。 私用的靜態 IP 位址 hello VM。
   * **TestService**。 Hello VM 將會建立 hello 雲端服務名稱。
   * **bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**。 使用 toocreate hello VM 映像。
   * **adminuser**。 Hello Windows VM 的本機系統管理員。
   * **AdminP@ssw0rd**。 Hello Windows VM 的本機系統管理員密碼。

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>如何 tooretrieve 靜態私人 IP 位址適用於 VM 的資訊
tooview hello 靜態私人 IP 位址建立 VM 與 hello 指令碼，請執行下列 Azure CLI 命令的 hello hello 資訊，並觀察 hello 值*網路 StaticIP*:

    azure vm static-ip show DNS01

預期的輸出：

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>如何 tooremove 靜態私人 IP 位址從 VM
tooremove hello 靜態私人 IP 位址執行下列 Azure CLI 命令的 hello 上方的 hello 指令碼中加入 toohello VM:

    azure vm static-ip remove DNS01

預期的輸出：

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a>如何 tooadd 靜態的私用 IP tooan 現有的 VM
tooadd 靜態私人 IP 位址 toohello 下命令使用上述 runt hello 指令碼建立 VM:

    azure vm static-ip set DNS01 192.168.1.101

預期的輸出：

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a>後續步驟
* 深入了解 [保留的公用 IP](virtual-networks-reserved-public-ip.md) 位址。
* 深入了解 [執行個體層級公用 IP (ILPIP)](virtual-networks-instance-level-public-ip.md) 位址。
* 請參閱 hello[保留 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)。

