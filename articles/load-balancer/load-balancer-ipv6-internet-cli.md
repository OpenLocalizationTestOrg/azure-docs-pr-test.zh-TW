---
title: "IPv6-Azure CLI aaaCreate 網際網路對向負載平衡器 |Microsoft 文件"
description: "了解如何 toocreate 網際網路對向負載平衡器 IPv6 的 Azure 資源管理員使用中的 hello Azure CLI"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "ipv6, azure load balancer, 雙重堆疊, 公用 ip, 原生 ipv6, 行動, iot"
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a>建立網際網路對向 IPv6 Azure 資源管理員中使用 Azure CLI hello 的負載平衡器

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Azure CLI](load-balancer-ipv6-internet-cli.md)
> * [範本](load-balancer-ipv6-internet-template.md)

Azure 負載平衡器是第 4 層 (TCP、UDP) 負載平衡器。 hello 負載平衡器連入流量的各項雲端服務中的狀況良好的服務執行個體或虛擬機器中負載平衡器集可提供高可用性。 Azure Load Balancer 也會在多個連接埠、多個 IP 位址或兩者上顯示這些服務。

## <a name="example-deployment-scenario"></a>範例部署案例

hello 下列圖表說明 hello 負載平衡解決方案使用本文中所述的 hello 範例範本部署。

![負載平衡器案例](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

在此案例中，您將建立下列 Azure 資源的 hello:

* 兩部虛擬機器 (VM)
* 虛擬網路介面，用於每個已指派 IPv4 和 IPv6 位址的 VM
* 配置有 IPv4 和 IPv6 公用 IP 位址的網際網路面向負載平衡器
* 可用性設定組的 toothat 包含 hello 兩個 Vm
* 兩個負載平衡規則 toomap hello 公用 Vip toohello 私用端點

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>使用 Azure CLI hello hello 方案部署

下列步驟的 hello 顯示 toocreate 網際網路向負載平衡器使用 CLI 的 Azure 資源管理員的方式。 使用 Azure 資源管理員中，每個資源建立個別的設定，然後放在一起 toocreate 資源。

toodeploy 負載平衡器，建立並設定 hello 下列物件：

* 前端 IP 組態 - 包含傳入網路流量的公用 IP 位址。
* 後端位址集區-包含 hello 虛擬機器 tooreceive 從 hello 負載平衡器的網路流量的網路介面 (Nic)。
* 負載平衡規則-包含對應 hello 負載平衡器 tooport hello 後端位址集區中的公用連接埠的規則。
* 輸入 NAT 規則-包含 hello 負載平衡器 tooa 通訊埠上的特定虛擬機器 hello 後端位址集區中的公用通訊埠對應規則。
* 探查-包含 hello 後端位址集區中的虛擬機器執行個體的健全狀況探查使用 toocheck 可用性。

如需詳細資料，請參閱 [Azure Resource Manager 的負載平衡器支援](load-balancer-arm.md)。

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a>設定您的 CLI 環境 toouse Azure 資源管理員

針對此範例中，目前我們正在執行 PowerShell 命令視窗中的 hello CLI 工具。 我們不使用 hello Azure PowerShell cmdlet，但我們會使用 PowerShell 的指令碼功能 tooimprove 可讀性並重複使用。

1. 如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。
2. 執行 hello **azure 組態模式**命令 tooswitch tooResource 管理員模式。

    ```azurecli
    azure config mode arm
    ```

    預期的輸出：

        info:    New mode is arm

3. 登入 tooAzure，並取得訂閱的清單。

    ```azurecli
    azure login
    ```

    出現提示時，請輸入您的 Azure 認證。

    ```azurecli
    azure account list
    ```

    Toouse 挑選您想要的 hello 訂用帳戶。 請記下一個步驟的 hello hello 訂用帳戶 Id。

4. 設定用於 hello CLI 命令的 PowerShell 變數。

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a>建立資源群組、負載平衡器、虛擬網路和子網路

1. 建立資源群組

    ```azurecli
    azure group create $rgName $location
    ```

2. 建立負載平衡器

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. 建立虛擬網路 (VNet)。

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    在此 VNet 中建立兩個子網路。

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a>建立 hello 前端集區的公用 IP 位址

1. Hello PowerShell 變數設定

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. 建立公用 IP 位址 hello 前端 IP 集區。

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > hello 負載平衡器會使用 hello 公用 IP 的 hello 網域標籤做為其 FQDN。 此的傳統部署，會使用 hello 雲端服務名稱，如 hello 負載平衡器 FQDN 已變更。
    > 此範例中的 hello FQDN 是*contoso09152016.southcentralus.cloudapp.azure.com*。

## <a name="create-front-end-and-back-end-pools"></a>建立前端和後端集區

這個範例會建立 hello 前端的 IP 集區收到 hello 負載平衡器上的 hello 連入網路流量和 hello 前端集區讓傳送嗨負載平衡網路流量的 hello 後端 IP 集區。

1. Hello PowerShell 變數設定

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. 建立 hello hello 上一個步驟和 hello 負載平衡器中建立的公用 IP 建立關聯的前端 IP 集區。

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a>建立 hello 探查、 NAT 規則和 LB 規則

這個範例會建立下列項目 hello:

* 探查規則 toocheck 連線 tooTCP 連接埠 80
* NAT 規則 tootranslate 所有連入流量連接埠 3389 tooport 3389 rdp<sup>1</sup>
* NAT 規則 tootranslate 所有連入流量連接埠 3391 tooport 3389 rdp<sup>1</sup>
* 負載平衡器規則 toobalance hello 連接埠 80 tooport 80 上的所有連入流量 hello 後端集區中的位址。

<sup>1</sup> NAT 規則是相關聯的 tooa hello 負載平衡器後方的特定虛擬機器執行個體。 toohello 特定虛擬機器和與 hello NAT 規則相關聯的連接埠，則傳送嗨網路流量到達連接埠 3389。 您必須為 NAT 規則指定通訊協定 (UDP 或 TCP)。 這兩種通訊協定不能指定 toohello 相同連接埠。

1. Hello PowerShell 變數設定

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. 建立 hello 探查

    hello 下列範例會建立一個 TCP 探查，檢查連線 tooback 端 TCP 通訊埠 80 每 15 秒。 它會將標記 hello 後端資源無法使用在兩個連續的失敗之後。

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. 建立允許 RDP 連線 toohello 後端資源的輸入的 NAT 規則

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. 建立負載平衡器的前端收到 hello 要求根據 toodifferent 後端連接埠傳送流量的規則

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. 檢查您的設定

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    預期的輸出：

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a>建立 NIC

建立 Nic，並將其關聯 tooNAT 規則、 負載平衡器規則和探查。

1. Hello PowerShell 變數設定

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. 建立的每個後端 NIC，並新增 IPv6 設定。

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a>建立 hello 後端 VM 資源，並附加每個 NIC

toocreate Vm，您必須儲存體帳戶。 對於負載平衡，hello Vm 需要 toobe 成員的可用性設定組。 如需建立 VM 的詳細資訊，請參閱 [使用 PowerShell 建立 Azure VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)

1. Hello PowerShell 變數設定

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > 此範例會使用 hello 使用者名稱和密碼以純文字的 hello vm。 清除使用認證 hello 時，務必謹慎。 處理認證在 PowerShell 中的更安全的方法，請參閱 hello [Get-credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet。

2. 建立 hello 儲存體帳戶和可用性設定組

    當您建立 hello Vm 時，您可能會使用現有的儲存體帳戶。 hello，下列命令會建立新的儲存體帳戶。

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    接下來，建立 hello 可用性設定組。

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. 建立具有相關聯的 hello Nic hello 虛擬機器

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a>後續步驟

[開始設定內部負載平衡器](load-balancer-get-started-ilb-arm-cli.md)

[設定負載平衡器分配模式](load-balancer-distribution-mode.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)
