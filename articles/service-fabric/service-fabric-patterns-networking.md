---
title: "適用於 Azure Service Fabric aaaNetworking 模式 |Microsoft 文件"
description: "描述常見的網路模式適用於 Service Fabric 以及 toocreate 叢集中使用 Azure 網路的功能。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a>Service Fabric 網路功能模式
您可以將 Azure Service Fabric 叢集與其他的 Azure 網路功能整合起來。 在本文中，我們會示範如何 toocreate 叢集該使用 hello，下列功能：

- [現有虛擬網路或子網路](#existingvnet)
- [靜態公用 IP 位址](#staticpublicip)
- [僅內部負載平衡器](#internallb)
- [內部與外部負載平衡器](#internalexternallb)

Service Fabric 會在標準的虛擬機器擴展集內執行。 能在虛擬機器擴展集內使用的功能，就能在 Service Fabric 叢集內使用。 hello 網路區段的虛擬機器擴展集和服務網狀架構的 hello Azure Resource Manager 範本完全相同。 部署 tooan 現有的虛擬網路之後，它是簡單 tooincorporate 其他網路功能，例如 Azure ExpressRoute、 Azure VPN 閘道、 網路安全性群組，和虛擬網路對等互連。

Service Fabric 有一個方面是其他網路功能所沒有的。 hello [Azure 入口網站](https://portal.azure.com)在內部使用 hello Service Fabric 資源提供者 toocall tooa 叢集 tooget 資訊節點和應用程式。 hello Service Fabric 資源提供者需要可公開存取的輸入的存取 toohello HTTP 閘道連接埠 （連接埠 19080，預設值） 上 hello 管理端點。 [Service Fabric 總管](service-fabric-visualizing-your-cluster.md)使用 hello 管理端點 toomanage 您的叢集。 hello Service Fabric 資源提供者也會使用您的叢集 toodisplay hello Azure 入口網站中有關此連接埠 tooquery 資訊。 

若連接埠 19080 不能從 hello Service Fabric 資源提供者存取，訊息中，例如*找不到節點*會出現在 hello 入口網站，而且節點和應用程式的清單會出現空白。 如果您想 toosee 您 hello Azure 入口網站中的叢集，您的負載平衡器必須公開公用 IP 位址，而且您的網路安全性群組必須允許 19080 的連接埠的連入流量。 如果您的設定不符合這些需求，hello Azure 入口網站不會顯示叢集的 hello 狀態。

## <a name="templates"></a>範本

所有 Service Fabric 範本都位於[一個下載檔案](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip)中。 您應該要能夠 toodeploy hello 範本做為使用下列 PowerShell 命令的 hello。 如果您要部署的 hello 現有 Azure 虛擬網路的範本或 hello 靜態公用 IP 範本，先閱讀 hello[初始安裝](#initialsetup)本文一節。

<a id="initialsetup"></a>
## <a name="initial-setup"></a>初始設定

### <a name="existing-virtual-network"></a>現有的虛擬網路

在下列範例的 hello，我們開頭現有的虛擬網路中 hello 命名 ExistingRG vnet **ExistingRG**資源群組。 hello 子網路是名為 default。 當您使用 hello Azure 入口網站 toocreate 標準的虛擬機器 (VM) 時，會建立這些預設的資源。 您可以建立 hello 虛擬網路和子網路，而不需要建立 hello VM，但 hello 新增叢集 tooan 現有虛擬網路的主要目標是 tooprovide 網路連線 tooother Vm。 建立 hello VM 提供現有的虛擬網路通常是很好範例。 如果您的 Service Fabric 叢集使用只使用內部負載平衡器，沒有公用 IP 位址，您可以使用 VM，其為安全的公用 IP hello*跳方塊*。

### <a name="static-public-ip-address"></a>靜態公用 IP 位址

靜態公用 IP 位址通常是從指派給 vm 的 hello 分開管理的專用的資源。 它是在專用的網路資源群組中提供 （做為相對於的 tooin hello Service Fabric 叢集資源群組本身）。 建立名為 staticIP1 hello 中的靜態公用 IP 位址相同 ExistingRG 資源群組中的，在 hello Azure 入口網站或 PowerShell，透過：

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a>Service Fabric 範本

在本文中的 hello 範例，我們會使用 hello Service Fabric template.json。 建立叢集之前，您可以使用 hello 標準入口網站精靈 toodownload hello 範本從 hello 入口網站。 您也可以使用其中一個 hello 範本中 hello[範本庫](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric)，像是 hello[五個節點 Service Fabric 叢集](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/)。

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a>現有虛擬網路或子網路

1. 變更 hello 子網路參數 toohello hello 現有子網路名稱，並將兩個新參數 tooreference hello 現有的虛擬網路：

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. 變更 hello`vnetID`變數 toopoint toohello 現有的虛擬網路：

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. 從資源中移除 `Microsoft.Network/virtualNetworks`，讓 Azure 不會建立新的虛擬網路︰

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. 註解 hello 虛擬網路從 hello`dependsOn`屬性`Microsoft.Compute/virtualMachineScaleSets`，因此您不相依於建立新的虛擬網路：

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. 部署 hello 範本：

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    部署之後，應該包含您的虛擬網路 hello 新擴展集 Vm。 hello 虛擬機器規模集節點型別應該會顯示 hello 現有的虛擬網路和子網路。 您也可以使用遠端桌面通訊協定 (RDP) tooaccess hello 中已存在於 hello 虛擬網路的 VM 和 tooping hello 新擴展集 Vm:

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

如需其他範例，請參閱[而非特定 tooService 網狀架構](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet)。


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a>靜態公用 IP 位址

1. 加入現有的靜態 IP 資源群組、 名稱和完整的網域名稱 (FQDN) 的 hello hello 名稱的參數：

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. 移除 hello`dnsName`參數。 （hello 靜態 IP 位址已經有一個）。

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. 加入變數 tooreference hello 現有靜態 IP 位址：

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. 從資源中移除 `Microsoft.Network/publicIPAddresses`，讓 Azure 不會建立新的 IP 位址︰

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. 註解 hello IP 位址從 hello`dependsOn`屬性`Microsoft.Network/loadBalancers`，因此您不相依於建立新的 IP 位址：

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. 在 hello`Microsoft.Network/loadBalancers`資源、 變更 hello`publicIPAddress`的項目`frontendIPConfigurations`tooreference hello 現有靜態 IP 位址，而不是新建立的其中一個：

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. 在 hello`Microsoft.ServiceFabric/clusters`資源，變更`managementEndpoint`toohello hello 靜態 IP 位址的 DNS FQDN。 如果您使用安全的叢集，請確定您變更*http://*太*https://*。 （請注意，這個步驟適用於 tooService 網狀架構叢集。 如果您使用虛擬機器擴展集，請略過此步驟)。

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. 部署 hello 範本：

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

部署之後，您可以看到您的負載平衡器已繫結的 toohello 公用靜態 IP 位址從 hello 其他資源群組。 hello Service Fabric 用戶端連線的端點和[Service Fabric 總管](service-fabric-visualizing-your-cluster.md)端點點 toohello hello 靜態 IP 位址的 DNS FQDN。

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a>僅內部負載平衡器

這種情況下，使用僅供內部使用的負載平衡器取代 hello 預設 Service Fabric 範本中的 hello 外部負載平衡器。 Hello Azure 入口網站和 hello Service Fabric 資源提供者的顧慮，請參閱前面一節的 hello。

1. 移除 hello`dnsName`參數。 (不需要此參數)。

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. (選擇性) 如果您使用靜態配置方法，則可以新增靜態 IP 位址參數。 如果您使用動態配置方法，您不需要 toodo 此步驟。

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. 從資源中移除 `Microsoft.Network/publicIPAddresses`，讓 Azure 不會建立新的 IP 位址︰

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. 移除 hello IP 位址`dependsOn`屬性`Microsoft.Network/loadBalancers`，因此您不相依於建立新的 IP 位址。 新增虛擬網路的 hello`dependsOn`屬性，因為 hello 負載平衡器現在取決於 hello hello 虛擬網路子網路：

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. 變更 hello 負載平衡器的`frontendIPConfigurations`設定使用`publicIPAddress`，toousing 子網路和`privateIPAddress`。 `privateIPAddress` 使用預先定義的靜態內部 IP 位址。 toouse 動態 IP 位址，移除 hello`privateIPAddress`項目，然後再變更`privateIPAllocationMethod`太**動態**。

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. 在 hello`Microsoft.ServiceFabric/clusters`資源，變更`managementEndpoint`toopoint toohello 內部負載平衡器位址。 如果您使用安全的叢集，請確定您變更*http://*太*https://*。 （請注意，這個步驟適用於 tooService 網狀架構叢集。 如果您使用虛擬機器擴展集，請略過此步驟)。

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. 部署 hello 範本：

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

部署之後，您的負載平衡器會使用私用靜態 10.0.0.250 hello IP 位址。 如果您在相同的虛擬網路的另一部電腦，您可以移 toohello 內部[Service Fabric 總管](service-fabric-visualizing-your-cluster.md)端點。 請注意連接 tooone 的 hello hello 負載平衡器後方的節點。

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a>內部與外部負載平衡器

在此案例中，開始與 hello 現有單一節點類型外部負載平衡器並新增 hello 內部負載平衡器相同的節點類型。 連接後端連接埠 tooa 後端位址集區可以指派只有 tooa 單一負載平衡器。 選擇要讓哪個負載平衡器擁有您的應用程式連接埠，哪個負載平衡器擁有管理端點 (連接埠 19000 和 19080)。 如果您將 hello 管理端點 hello 內部負載平衡器上，將保留在心 hello Service Fabric 資源 hello 文章中稍早討論的提供者限制。 在 hello 範例中我們使用，hello 管理端點會保留在 hello 外部負載平衡器上。 您也會新增連接埠 80 的應用程式連接埠，並將它放 hello 內部負載平衡器上。

在兩個節點型別叢集中，一種節點類型是 hello 外部負載平衡器上。 hello 其他節點型別是 hello 內部負載平衡器上。 toouse hello 入口網站建立兩個節點類型的範本 （隨附於兩個負載平衡器） 中的兩個節點型別叢集，切換 hello 第二個負載平衡器 tooan 內部負載平衡器。 如需詳細資訊，請參閱 hello[僅供內部使用的負載平衡器](#internallb)> 一節。

1. 加入 hello 靜態內部負載平衡器 IP 位址參數。 （如相關 toousing 動態 IP 位址資訊，請參閱本文的稍早章節）。

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. 新增應用程式連接埠 80 參數。

3. tooadd hello 現有的內部版本網路變數，複製和貼上，並新增 「-Int"toohello 名稱：

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. 如果您啟動與 hello 入口網站所產生的範本會使用應用程式連接埠 80，hello 預設入口網站範本會加入 AppPort1 （連接埠 80） hello 外部負載平衡器上。 在此情況下，從 hello 外部負載平衡器移除 AppPort1`loadBalancingRules`和探查，因此您可以將其加入 toohello 內部負載平衡器：

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. 新增第二個 `Microsoft.Network/loadBalancers` 資源。 它看起來類似 hello 中建立的 toohello 內部負載平衡器[僅供內部使用的負載平衡器](#internallb) 區段中，但它會使用 hello"的 Int 」 負載平衡器變數，以及實作只有 hello 應用程式連接埠 80。 這也會移除`inboundNatPools`，tookeep hello 公用負載平衡器上的 RDP 端點。 如果您想 RDP hello 內部負載平衡器上，移動`inboundNatPools`從 hello 外部負載平衡器 toothis 內部負載平衡器：

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public tooPrivate IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add hello probe for hello app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. 在`networkProfile`hello`Microsoft.Compute/virtualMachineScaleSets`資源，新增 hello 內部的後端位址集區：

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. 部署 hello 範本：

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

部署之後，您可以看到 hello 資源群組中的兩個負載平衡器。 如果您瀏覽 hello 負載平衡器，您可以看到 hello 公用 IP 位址和管理端點 （連接埠 19000 和 19080） 指派 toohello 公用 IP 位址。 您也可以看到 hello 靜態內部 IP 位址與應用程式端點 （連接埠 80） 指派 toohello 內部負載平衡器。 同時指定負載平衡器使用 hello 相同虛擬機器規模集後端集區。

## <a name="next-steps"></a>後續步驟
[建立叢集](service-fabric-cluster-creation-via-arm.md)
