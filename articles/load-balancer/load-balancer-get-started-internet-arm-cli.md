---
title: "aaaCreate 網際網路對向負載平衡器-Azure CLI |Microsoft 文件"
description: "了解如何使用資源管理員中的網際網路對向負載平衡器 toocreate hello Azure CLI"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a>建立使用 Azure CLI hello 網際網路負載平衡器

> [!div class="op_single_selector"]
> * [入口網站](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [範本](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

本文涵蓋 hello Resource Manager 部署模型。 您也可以[學習 toocreate 網際網路向負載平衡器使用傳統部署的方式](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>使用 Azure CLI hello hello 方案部署

下列步驟的 hello 顯示 toocreate 網際網路向負載平衡器使用 CLI 的 Azure 資源管理員的方式。 使用 Azure 資源管理員建立並個別設定每個資源，然後放在一起 toocreate 資源。

您必須建立並設定下列物件 toodeploy 負載平衡器的 hello:

* 前端 IP 組態 - 包含傳入網路流量的公用 IP 位址。
* 後端位址集區-包含 hello 虛擬機器 tooreceive 從 hello 負載平衡器的網路流量的網路介面 (Nic)。
* 負載平衡規則-包含對應 hello 負載平衡器 tooport hello 後端位址集區中的公用連接埠的規則。
* 輸入 NAT 規則-包含 hello 負載平衡器 tooa 通訊埠上的特定虛擬機器 hello 後端位址集區中的公用通訊埠對應規則。
* 探查-包含 hello 後端位址集區中的虛擬機器執行個體的健全狀況探查使用 toocheck 可用性。

如需詳細資訊，請參閱 [Azure Resource Manager 的負載平衡器支援](load-balancer-arm.md)。

## <a name="set-up-cli-toouse-resource-manager"></a>設定 CLI toouse 資源管理員

1. 如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。
2. 執行 hello **azure 組態模式**命令 tooswitch tooResource 管理員模式，如下所示。

    ```azurecli
        azure config mode arm
    ```

    預期的輸出：

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>建立虛擬網路和 hello 前端 IP 集區的公用 IP 位址

1. 建立名為虛擬網路 (VNet) *NRPVnet* hello 美國東部位置使用的資源群組中名為*NRPRG*。

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    建立名為 NRPVnetSubnet 的子網路，其中包含 NRPVnet 中 10.0.0.0/24 的 CIDR 區塊。

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. 建立名為的公用 IP 位址*NRPPublicIP*前端的 IP 集區與 DNS 名稱所使用的 toobe *loadbalancernrp.eastus.cloudapp.azure.com*。 下方的 hello 命令會使用 hello 靜態配置類型和4 分鐘閒置逾時。

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > hello 負載平衡器將會使用自己的 FQDN hello 公用 IP 的 hello 網域標籤。 這個傳統的部署，會使用 hello 雲端服務，如 hello 負載平衡器完全完整網域名稱 (FQDN) 的已變更。
   > 此範例中的 hello FQDN 是*loadbalancernrp.eastus.cloudapp.azure.com*。

## <a name="create-a-load-balancer"></a>建立負載平衡器

hello 下列命令會建立名為負載平衡器*NRPlb*在 hello *NRPRG* hello 中的資源群組*美國東部*Azure 位置。

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a>建立前端 IP 集區與後端位址集區
此範例示範如何 toocreate hello 前端 IP 集區接收上 hello hello 連入網路流量負載平衡器和 hello hello 前端集區讓傳送嗨負載平衡網路流量的後端 IP 集區。

1. 建立 hello hello 上一個步驟和 hello 負載平衡器中建立的公用 IP 建立關聯的前端 IP 集區。

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. 設定從 hello 前端 IP 集區的後端位址集區使用 tooreceive 連入流量。

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a>建立 LB 規則、NAT 規則及探查

這個範例會建立 hello 下列項目。

* NAT 規則 tootranslate 通訊埠 21 tooport 22 上的所有連入流量<sup>1</sup>
* NAT 規則 tootranslate 連接埠 23 tooport 22 上的所有傳入流量
* 負載平衡器規則 toobalance hello 連接埠 80 tooport 80 上的所有連入流量 hello 後端集區中的位址。
* 探查規則 toocheck hello 健全狀況狀態上名為的頁面*HealthProbe.aspx*。

<sup>1</sup> NAT 規則是相關聯的 tooa hello 負載平衡器後方的特定虛擬機器執行個體。 到達連接埠 21 hello 網路流量會傳送 tooa 特定虛擬機器上連接埠 22 此 NAT 規則相關聯。 您必須為 NAT 規則指定通訊協定 (UDP 或 TCP)。 這兩種通訊協定不能指定 toohello 相同連接埠。

1. 建立 hello NAT 規則。

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. 建立負載平衡器規則。

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. 建立健全狀況探查。

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. 檢查您的設定。

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    預期的輸出：

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a>建立 NIC

您需要 toocreate Nic （或修改現有的） 並將其關聯 tooNAT 規則、 負載平衡器規則和探查。

1. 建立名為的 NIC *lb nic1 是*，並將它與 hello 關聯*rdp1* NAT 規則以及 hello *NRPbackendpool*後端位址集區。

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    預期的輸出：

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. 建立名為的 NIC *lb nic2 是*，並將它與 hello 關聯*rdp2* NAT 規則以及 hello *NRPbackendpool*後端位址集區。

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. 建立名為的虛擬機器 (VM) *web1*，並將它與 hello NIC 名為關聯*lb nic1 是*。 儲存體帳戶呼叫*web1nrp*之前執行下列的 hello 命令所建立。

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > 中的負載平衡器需要 toobe 中 Vm hello 相同可用性設定組。 使用`azure availset create`toocreate 可用性設定組。

    hello 輸出應類似 toohello 下列：

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > hello 參考用訊息**這是不含設定的 publicIP NIC**卻因為 hello NIC 建立 hello 連接 tooInternet 使用 hello 負載平衡器公用 IP 位址的負載平衡器。

    因為 hello *lb nic1 是*NIC 都與 hello *rdp1* NAT 規則，您可以在太連接*web1*透過連接埠 3441 hello 負載平衡器上使用 RDP。

4. 建立名為的虛擬機器 (VM) *web2*，並將它與 hello NIC 名為關聯*lb nic2 是*。 儲存體帳戶呼叫*web1nrp*之前執行下列的 hello 命令所建立。

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a>更新現有負載平衡器
您可以新增參考現有負載平衡器的規則。 在 hello 下一個範例中，新的負載平衡器規則加入 tooan 現有負載平衡器**NRPlb**

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a>刪除負載平衡器
使用下列命令 tooremove 負載平衡器的 hello:

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a>後續步驟
[開始設定內部負載平衡器](load-balancer-get-started-ilb-arm-cli.md)

[設定負載平衡器分配模式](load-balancer-distribution-mode.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)
