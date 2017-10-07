---
title: "aaaCreate 內部負載平衡器-Azure CLI |Microsoft 文件"
description: "了解如何使用內部負載平衡器 toocreate hello Azure CLI 資源管理員 中"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a>使用 Azure CLI hello 建立內部負載平衡器

> [!div class="op_single_selector"]
> * [Azure 入口網站](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [範本](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。  本文將說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello[傳統部署模型](load-balancer-get-started-ilb-classic-cli.md)。

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a>使用 Azure CLI hello 部署 hello 方案

hello 下列步驟顯示如何 toocreate 網際網路對向的負載平衡器使用 CLI 的 Azure 資源管理員。 使用 Azure 資源管理員中，每個資源建立個別的設定，然後放在一起 toocreate 資源。

您需要 toocreate 並設定下列物件 toodeploy 負載平衡器的 hello:

* **前端 IP 組態**- 包含傳入網路流量的公用 IP 位址
* **後端位址集區**： 包含啟用 hello 虛擬機器 tooreceive 從 hello 負載平衡器的網路流量的網路介面 (Nic)
* **負載平衡規則**： 包含規則，可將 hello 負載平衡器 tooport hello 後端位址集區中的公用連接埠
* **輸入 NAT 規則**： 包含 hello 負載平衡器 tooa 通訊埠上的特定虛擬機器 hello 後端位址集區中的公用連接埠對應規則
* **探查**： 包含會使用的 toocheck hello 可用性 hello 後端位址集區中的虛擬機器執行個體的健全狀態探查

如需詳細資料，請參閱 [Azure Resource Manager 的負載平衡器支援](load-balancer-arm.md)。

## <a name="set-up-cli-toouse-resource-manager"></a>設定 CLI toouse 資源管理員

1. 如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)。 請遵循 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示。
2. 執行 hello **azure 組態模式**命令 tooswitch tooResource 管理員模式下，如下所示：

    ```azurecli
    azure config mode arm
    ```

    預期的輸出：

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a>逐步建立內部負載平衡器

1. 登入 tooAzure。

    ```azurecli
    azure login
    ```

    出現提示時，輸入您的 Azure 認證。

2. 變更 hello 命令工具 tooAzure Resource Manager 模式。

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a>建立資源群組

Azure Resource Manager 中的所有資源都會與資源群組關聯。 若尚未建立資源群組，請先建立資源群組。

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a>建立內部負載平衡器集

1. 建立內部負載平衡器

    在下列案例中的 hello，美東地區建立名為 nrprg 的資源群組。

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > 內部負載平衡器，例如虛擬網路和虛擬網路子網路的所有資源都必須在 hello 相同的資源群組，並在 hello 相同區域。

2. 建立 hello 內部負載平衡器前端的 IP 位址。

    您使用的 hello IP 位址必須是虛擬網路的 hello 子網路範圍內。

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. 建立 hello 後端位址集區。

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    定義前端 IP 位址和後端位址集區之後，您可以建立負載平衡器規則、輸入 NAT 規則，以及自訂的健全狀況探查。

4. 建立 hello 內部負載平衡器負載平衡器規則。

    當您遵循 hello 先前的步驟時，hello 命令會建立接聽 tooport 1433 的負載平衡器規則 hello 前端，而傳送負載平衡網路流量 toohello 後端位址集區，也使用通訊埠 1433年。

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. 建立輸入 NAT 規則。

    輸入的 NAT 規則會移 tooa 特定虛擬機器執行個體的使用的 toocreate 端點在負載平衡器。 hello 先前的步驟建立兩個遠端桌面的 NAT 規則。

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. 建立 hello 負載平衡器的健全狀況探查。

    健全狀況探查會檢查所有虛擬機器執行個體 toomake 確定他們可以傳送網路流量。 hello 失敗的探查檢查虛擬機器執行個體移除 hello 負載平衡器，直到它變成上線並探查核取判斷為狀況良好。

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > hello Microsoft Azure 平台會使用各種不同的系統管理情況靜態、 可公開路由傳送的 IPv4 位址。 hello IP 位址是 168.63.129.16。 此 IP 位址不應該遭到任何防火牆封鎖，因為可能會造成非預期的行為。
    > 尊重 tooAzure 內部負載平衡，此 IP 位址可供監視探查 hello 負載平衡器 toodetermine hello 健全狀況狀態從一組負載平衡中虛擬機器。 如果網路安全性小組使用的 toorestrict 內部負載平衡集內的流量 tooAzure 虛擬機器或套用的 tooa 虛擬網路子網路，請確定網路安全性規則從 168.63.129.16 加入 tooallow 流量。

## <a name="create-nics"></a>建立 NIC

您需要 toocreate Nic （或修改現有的） 並將其關聯 tooNAT 規則、 負載平衡器規則和探查。

1. 建立名為 NIC *lb nic1 是*，然後將它產生關聯以 hello *rdp1* NAT 規則，並於 hello *beilb*後端位址集區。

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
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

2. 建立名為 NIC *lb nic2 是*，然後將它產生關聯以 hello *rdp2* NAT 規則，並於 hello *beilb*後端位址集區。

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. 建立虛擬機器名為*DB1*，然後將它產生關聯以 hello NIC 名為*lb nic1 是*。 儲存體帳戶呼叫*web1nrp*建立 hello 下列命令執行之前：

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > 中的負載平衡器需要 toobe 中 Vm hello 相同可用性設定組。 使用`azure availset create`toocreate 可用性設定組。

4. 建立名為的虛擬機器 (VM) *DB2*，然後將它產生關聯以 hello NIC 名為*lb nic2 是*。 儲存體帳戶呼叫*web1nrp*之前執行下列命令的 hello 建立。

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a>刪除負載平衡器

tooremove 負載平衡器，使用下列命令的 hello:

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a>後續步驟

[使用來源 IP 同質性設定負載平衡器分配模式](load-balancer-distribution-mode.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)

