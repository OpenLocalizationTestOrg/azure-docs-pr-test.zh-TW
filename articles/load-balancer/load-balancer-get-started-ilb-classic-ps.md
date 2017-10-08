---
title: "aaaCreate Azure 內部負載平衡器-PowerShell 傳統 |Microsoft 文件"
description: "了解 toocreate 內部負載平衡器在 hello 傳統部署模型中使用 PowerShell 的方式"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a>開始使用 PowerShell 建立內部負載平衡器 (傳統)

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [雲端服務](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。  本文說明如何使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 了解如何太[使用 hello 資源管理員的模型執行這些步驟](load-balancer-get-started-ilb-arm-ps.md)。

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a>建立虛擬機器的內部負載平衡器集

內部負載平衡器設定和 hello 伺服器，則會傳送其流量 tooit toocreate，您有 toodo hello 下列：

1. 建立執行個體的內部負載平衡一組負載平衡的 hello 伺服器之間取得平衡的連入流量 toobe 負載 hello 端點。
2. 新增對應 toohello 將接收 hello 連入流量的虛擬機器端點。
3. 設定將用來傳送嗨流量 toobe 負載平衡 toosend 其流量 toohello 虛擬 IP (VIP) 位址 hello 內部負載平衡的執行個體的 hello 伺服器。

### <a name="step-1-create-an-internal-load-balancing-instance"></a>步驟 1︰建立內部負載平衡執行個體

對於現有的雲端服務或部署在區域虛擬網路的雲端服務，您可以建立內部負載平衡的執行個體，以下列 Windows PowerShell 命令的 hello:

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

請注意，這種使用 hello [Add-azureendpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet 會使用 hello DefaultProbe 參數集。 如需其他參數集的詳細資訊，請參閱 [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx)。

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a>步驟 2： 新增端點 toohello 內部負載平衡執行個體

下列是一個範例：

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a>步驟 3： 設定伺服器 toosend 其流量 toohello 新內部負載平衡的端點

您有太設定 hello 伺服器的流量是進行 toobe 負載平衡 toouse hello 新 IP 位址 (hello VIP) hello 內部負載平衡的執行個體。 這是內部負載平衡的 hello 執行個體所接聽的 hello 位址。 在大部分情況下，您需要 toojust 加入或修改 hello 內部負載平衡的執行個體的 hello VIP 的 DNS 記錄。

如果您指定 hello IP 位址 hello hello 內部負載平衡的執行個體建立期間，您已經有 hello VIP。 否則，您可以看到 hello VIP 從 hello 下列命令：

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

toouse 這些命令中，填寫 hello 值，然後移除 hello < 和 >。 下列是一個範例：

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

從 hello 顯示 hello Get-azureinternalloadbalancer 命令，記下 hello IP 位址以 hello 必要的變更 tooyour 伺服器或資料流取得傳送 toohello VIP 的 DNS 記錄 tooensure。

> [!NOTE]
> hello Microsoft Azure 平台會使用各種不同的系統管理情況靜態、 可公開路由傳送的 IPv4 位址。 hello IP 位址是 168.63.129.16。 此 IP 位址不應該遭到任何防火牆封鎖，因為可能會造成非預期的行為。
> 內部負載平衡尊重 tooAzure，此 IP 位址會使用藉由監視 hello 負載平衡器 toodetermine hello 健全狀況狀態的虛擬機器負載平衡集的探查。 如果網路安全性小組使用的 toorestrict 內部負載平衡集內的流量 tooAzure 虛擬機器或套用的 tooa 虛擬網路子網路，請確定網路安全性規則從 168.63.129.16 加入 tooallow 流量。

## <a name="example-of-internal-load-balancing"></a>內部負載平衡的範例

您完成 hello 結束 tooend 程序建立一組負載平衡的兩個範例設定，請參閱 toostep hello 下列各節。

### <a name="an-internet-facing-multi-tier-application"></a>網際網路面向的多層式應用程式

您想 tooprovide 一組網際網路對向 web 伺服器的負載平衡資料庫服務。 這兩組伺服器都會裝載於單一 Azure 雲端服務。 網頁伺服器流量 tooTCP 連接埠 1433年必須分散 hello 資料庫層中的兩部虛擬機器。 圖 1 顯示 hello 設定。

![Hello 資料庫層的內部負載平衡集](./media/load-balancer-internal-getstarted/IC736321.png)

hello 設定包含下列 hello:

* hello 現有的雲端服務裝載 hello 虛擬機器名為 mytestcloud。
* hello 兩個現有資料庫伺服器則命名為 DB1 中，DB2。
* Hello web 層中的 web 伺服器連接 toohello hello 資料庫層中的資料庫伺服器使用 hello 私人 IP 位址。 另一個選項是 toouse hello 虛擬網路的 DNS，並以手動方式註冊 hello 內部負載平衡器集 A 記錄。

hello comandos siguientes configuran 新內部負載平衡的執行個體名為**ILBset**加入對應 toohello 兩個資料庫伺服器的端點 toohello 虛擬機器：

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a>移除內部負載平衡組態

tooremove 為內部負載平衡器執行個體，下列命令使用 hello 從端點的虛擬機器：

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

toouse 這些命令中，填寫 hello 值，並移除 hello < 和 >。

下列是一個範例：

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

tooremove 內部負載平衡器執行個體從雲端服務，下列命令使用 hello:

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

這些命令，toouse 填入 hello 值，並移除 hello < 和 >。

下列是一個範例：

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a>內部負載平衡器 Cmdlet 的其他資訊

tooobtain 內部負載平衡 cmdlet，執行下列命令在 Windows PowerShell 提示字元中的 hello 相關的其他資訊：

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a>後續步驟

[使用來源 IP 同質性設定負載平衡器分配模式](load-balancer-distribution-mode.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)

