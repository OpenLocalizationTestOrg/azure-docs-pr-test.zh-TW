---
title: "傳統模式中使用 aaaHow toocreate Nsg hello Azure CLI |Microsoft 文件"
description: "深入了解如何 toocreate 及使用 Azure CLI hello 的傳統模式中部署 Nsg"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a>如何 toocreate Nsg 中的 （傳統） hello Azure CLI
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

本文涵蓋 hello 傳統部署模型。 您也可以[hello Resource Manager 部署模型中建立 Nsg](virtual-networks-create-nsg-arm-cli.md)。

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

下列的 hello 範例 Azure CLI 命令預期已經根據上述的 hello 案例建立簡單的環境。 如果您想 toorun hello 命令，因為它們會顯示在此文件，第一次建置 hello 測試環境[建立 VNet](virtual-networks-create-vnet-classic-cli.md)。

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a>如何 toocreate hello NSG hello 前端子網路
名為 NSG 名為的 toocreate **NSG 前端**根據上面的 hello 案例，請遵循下列 hello 步驟。

1. 如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。
2. 執行 hello  **`azure config mode`** 命令 tooswitch tooclassic 模式，如下所示。
   
        azure config mode asm
   
    預期的輸出：
   
        info:    New mode is asm
3. 執行 hello  **`azure network nsg create`** 命令 toocreate NSG。
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    預期的輸出：
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    參數：
   
   * **-l (或 --location)**。 Hello 新的 NSG 建立所在的 azure 區域。 在本文案例中為 *westus*。
   * **-n (or --name)**。 名稱 hello 新的 NSG。 在本文案例中為 *NSG-FrontEnd*。
4. 執行 hello  **`azure network nsg rule create`** 命令 toocreate 允許從 hello 網際網路存取 tooport 3389 (RDP) 的規則。
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    預期的輸出：
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    參數：
   
   * **-a (或 --nsg-name)**。 Hello NSG 中的 hello 會建立規則的名稱。 在本文案例中為 *NSG-FrontEnd*。
   * **-n (or --name)**。 Hello 新規則的名稱。 在本文案例中為 *rdp-rule*。
   * **-c (或 --action)**。 Hello 規則 （拒絕或允許） 的存取層級。
   * **-p (或 --protocol)**。 通訊協定 (Tcp、 Udp 或 *) hello 規則。
   * **-r (或 --type)**。 連線 (輸入或輸出) 的方向。
   * **-y (或 --priority)**。 Hello 規則的優先順序。
   * **-f (或 --source-address-prefix)**。 CIDR 中的來源位址首碼或使用預設標記。
   * **-o (或 --source-port-range)**。 來源連接埠，或連接埠範圍。
   * **-e (或 --destination-address-prefix)**。 CIDR 中的目的地位址首碼或使用預設標記。
   * **-u (或 --destination-port-range)**。 目的地連接埠，或連接埠範圍。
5. 執行 hello  **`azure network nsg rule create`** 命令 toocreate 允許從 hello 網際網路存取 tooport 80 (HTTP) 的規則。
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    預期的輸出：
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. 執行 hello  **`azure network nsg subnet add`** 命令 toolink hello NSG toohello 前端子網路。
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    預期的輸出：
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a>Hello 回 toocreate hello NSG 如何結束子網路
名為 NSG 名為的 toocreate *NSG 後端*根據上面的 hello 案例，請遵循下列 hello 步驟。

1. 執行 hello  **`azure network nsg create`** 命令 toocreate NSG。
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    預期的輸出：
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    參數：
   
   * **-l (或 --location)**。 Hello 新的 NSG 建立所在的 azure 區域。 在本文案例中為 *westus*。
   * **-n (or --name)**。 名稱 hello 新的 NSG。 在本文案例中為 *NSG-FrontEnd*。
2. 執行 hello  **`azure network nsg rule create`** 命令 toocreate 允許從 hello 前端子網路的存取 tooport 1433 (SQL) 的規則。
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    預期的輸出：
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. 執行 hello  **`azure network nsg rule create`** 命令 toocreate 拒絕存取 toohello 網際網路的規則。
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    預期的輸出：
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. 執行 hello  **`azure network nsg subnet add`**  toolink hello NSG toohello 回結束子網路的命令。
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    預期的輸出：
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

