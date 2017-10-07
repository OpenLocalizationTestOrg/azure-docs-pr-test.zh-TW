---
title: "aaaCreate 叢集中的 Azure 負載平衡器規則"
description: "設定 Azure Service Fabric 叢集的 Azure 負載平衡器 tooopen 連接埠。"
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a>開啟 Service Fabric 叢集的連接埠

hello 負載平衡器部署與 Azure Service Fabric 叢集指示流量 tooyour 應用程式的節點上執行。 如果您變更您的應用程式 toouse 不同的通訊埠，您必須公開該通訊埠 （或路由傳送不同的連接埠） 在 hello Azure 負載平衡器。

當您部署您的 service fabric 叢集 tooAzure 時，為您自動建立負載平衡器。 如果您沒有負載平衡器，請參閱[設定網際網路面向的負載平衡器](..\load-balancer\load-balancer-get-started-internet-portal.md)。

## <a name="configure-service-fabric"></a>設定 Service Fabric

Service Fabric 應用程式**ServiceManifest.xml**組態檔定義您的應用程式必須要有 toouse hello 端點。 Hello 負載平衡器 hello 設定檔已更新的 toodefine 端點之後，必須更新的 tooexpose 該 （或不同） 連接埠。 如需有關如何 toocreate hello 服務網狀架構端點的詳細資訊，請參閱[安裝端點](service-fabric-service-manifest-resources.md)。

## <a name="create-a-load-balancer-rule"></a>建立負載平衡器規則

負載平衡器規則面對網際網路的連接埠會開啟，並將轉寄流量 toohello 內部節點的應用程式所使用的連接埠。 如果您沒有負載平衡器，請參閱[設定網際網路面向的負載平衡器](..\load-balancer\load-balancer-get-started-internet-portal.md)。

負載平衡器規則，您需要下列資訊 toocollect hello toocreate:

- 負載平衡器名稱。
- 資源群組的 hello 負載平衡器和 service fabric 叢集。
- 外部連接埠。
- 內部連接埠。

## <a name="azure-cli"></a>Azure CLI
>[!NOTE]
>如果您需要 toodetermine hello hello 負載平衡器名稱，請使用此命令 tooquickly get 所有負載平衡器和相關聯的 hello 資源群組的清單。
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

只需要單一命令 toocreate hello 與負載平衡器規則**Azure CLI**。 您只需要 tooknow hello 負載平衡器與資源群組 toocreate 新規則的兩個 hello 名稱。

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

hello Azure CLI 命令具有一些 hello 下表所述的參數：

| 參數 | 說明 |
| --------- | ----------- |
| `--backend-port`  | hello 連接埠 hello service fabric 應用程式正在接聽。 |
| `--frontend-port` | hello 連接埠 hello 負載平衡器會公開的外部連接。 |
| `-lb-name` | hello hello 名稱負載平衡器 toochange。 |
| `-g`       | hello 具有 hello 負載平衡器和 service fabric 叢集資源群組。 |
| `-n`       | hello 選擇 hello 規則的名稱。 |


>[!NOTE]
>如需有關如何 toocreate 負載平衡器以 hello Azure CLI，請參閱[建立負載平衡器以 hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md)。

## <a name="powershell"></a>PowerShell

>[!NOTE]
>如果您需要 toodetermine hello hello 負載平衡器名稱，請使用此命令 tooquickly get 所有負載平衡器和相關聯的資源群組的清單。
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

PowerShell 是比 hello Azure CLI 更為複雜。 在概念上，執行下列步驟 toocreate hello 規則。

1. 從 Azure 取得 hello 負載平衡器。
2. 建立規則。
3. 新增 hello 規則 toohello 負載平衡器。
4. 更新 hello 負載平衡器。

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

關於 hello`New-AzureRmLoadBalancerRuleConfig`命令時，hello`-FrontendPort`代表 hello 連接埠 hello 負載平衡器會公開外部連接，和 hello`-BackendPort`代表 hello 連接埠 hello service fabric 應用程式正在接聽。

>[!NOTE]
>如需有關如何 toocreate 負載平衡器使用 PowerShell，請參閱[使用 PowerShell 建立負載平衡器](..\load-balancer\load-balancer-get-started-internet-arm-ps.md)。

