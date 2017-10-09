---
title: "aaaManage Azure 保留的 IP 位址 （傳統）-PowerShell |Microsoft 文件"
description: "了解保留的 IP 位址 （傳統） 以及 toomanage 它們使用 PowerShell。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a>保留的 IP 位址 (傳統)

> [!div class="op_single_selector"]
> * [Azure 入口網站](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI](virtual-network-deploy-static-pip-arm-cli.md)
> * [範本](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (傳統)](virtual-networks-reserved-public-ip.md)

Azure 中的 IP 位址分為兩個類別：動態和保留。 依預設由 Azure 管理的公用 IP 位址是動態的。 該 hello 用於給定的雲端服務 (VIP) 的 IP 位址的方式或 tooaccess 資源遭到關閉或停止 （取消配置） 時，VM 或角色執行個體直接 (ILPIP) 可以從時間 tootime 變更。

tooprevent 變更 IP 位址，您可以保留的 IP 位址。 保留的 Ip 僅做 VIP，確保 hello 雲端服務會維持為 hello 相同，因為即使資源都已關閉或停止 （取消配置） 該 hello IP 位址。 此外，您可以轉換現有的動態 Ip 做 VIP tooa 保留 IP 位址。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 本文說明如何使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 了解如何 tooreserve 靜態公用 IP 位址使用 hello [Resource Manager 部署模型](virtual-network-ip-addresses-overview-arm.md)。

在 Azure 中的 toolearn 進一步了解 IP 位址，請閱讀 hello [IP 位址](virtual-network-ip-addresses-overview-classic.md)發行項。

## <a name="when-do-i-need-a-reserved-ip"></a>何時需要保留的 IP？
* **您想要訂用帳戶中保留的 hello IP 的 tooensure**。 如果您想 tooreserve 的 IP 位址，才會釋放，從您的訂用帳戶，在任何情況下，您應該使用保留公用 IP。  
* **您想要您與雲端服務的 IP toostay 即使透過停止或取消配置狀態 (Vm)**。 如果您想使用的 IP 位址不會變更，來存取您服務 toobe，即使 hello 中的 Vm 雲端服務都已關閉或停止 （取消配置）。
* **您想要從 Azure 的輸出流量使用可預期的 IP 位址的 tooensure**。 您可能需要您在內部部署防火牆設定 tooallow 唯一流量來自特定 IP 位址。 您可以藉由保留 IP，知道 hello 來源 IP 位址，而不需要您的防火牆規則，因為 tooan IP 變更 tooupdate。

## <a name="faq"></a>常見問題集
1. 我是否可以針對所有 Azure 服務都使用保留的 IP？ <br>
    否。 保留的 IP 僅可用於 VM 和雲端服務透過 VIP 公開的執行個體角色。
2. 我可以有多少保留的 IP？ <br>
    如需詳細資訊，請參閱 hello [Azure 限制](../azure-subscription-service-limits.md#networking-limits)發行項。
3. 保留的 IP 是否會收取費用？ <br>
    有時是。 如需定價詳細資料，請參閱 hello[保留 IP 位址定價詳細資料](http://go.microsoft.com/fwlink/?LinkID=398482)頁面。
4. 我該如何保留 IP 位址？ <br>
    您可以使用 PowerShell，hello [Azure 管理 REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx)，或使用 hello [Azure 入口網站](https://portal.azure.com)tooreserve Azure 地區內的 IP 位址。 保留的 IP 位址是相關聯的 tooyour 訂用帳戶。
5. 我是否可以將保留的 IP 位址與同質群組型 VNet 搭配使用？ <br>
    否。 保留的 IP 僅在區域 VNet 才受支援。 與同質群組關聯的 VNet 不支援保留的 IP。 如需有關如何將 VNet 與區域或同質群組產生關聯的詳細資訊，請參閱 hello[關於區域 Vnet 和同質群組](virtual-networks-migrate-to-regional-vnet.md)發行項。

## <a name="manage-reserved-vips"></a>管理保留的 VIP

請確定您已安裝並設定 PowerShell hello hello 中的步驟，以[安裝和設定 PowerShell](/powershell/azure/overview)發行項。 

您可以使用保留的 Ip，您必須先新增它 tooyour 訂用帳戶。 toocreate hello 公用 IP 集區的保留 IP 位址用於 hello*美國中部*位置，執行下列命令的 hello:

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

但是請注意，您無法指定正在保留的 IP。 tooview 哪些 IP 位址會保留在您訂用帳戶，執行下列 PowerShell 命令的 hello，並注意 hello 值*ReservedIPName*和*位址*:

```powershell
Get-AzureReservedIP
```

預期的輸出：

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
>當您使用 PowerShell 建立保留的 IP 位址時，您無法指定在資源群組 toocreate hello 保留 IP。 Azure 會自動將它放在名為 *Default-Networking* 的資源群組中。 如果您建立使用 hello hello 保留 IP [Azure 入口網站](http://portal.azure.com)，您可以指定您選擇的任何資源群組。 如果您建立 hello 保留 IP 的資源群組中非*預設網路*不過，每當您參考 hello 保留 IP 與命令例如`Get-AzureReservedIP`和`Remove-AzureReservedIP`，您必須參考 hello 名稱*群組資源群組名稱保留 ip 名稱*。  例如，如果您建立名為保留的 IP *myreservedip 產生*資源群組中名為*myResourceGroup*，您必須參考 hello hello 保留 IP，當做名稱*群組 myResourceGroupmyreservedip 產生*。   

一旦 IP 已保留，直到刪除為止會維持相關聯的 tooyour 訂用帳戶。 toodelete 保留 IP，執行下列 PowerShell 命令的 hello:

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a>保留現有的雲端服務的 hello IP 位址
您可以保留現有的雲端服務的 hello IP 位址加入 hello`-ServiceName`參數。 雲端服務 tooreserve hello IP 位址*TestService*在 hello*美國中部*位置，執行下列 PowerShell 命令的 hello:

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a>關聯保留的 IP tooa 新的雲端服務
hello 下列指令碼會建立新的保留 IP，然後將其相關聯 tooa 新的雲端服務名稱為*TestService*。

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> 當您建立保留的 IP toouse 與雲端服務時，您仍然 toohello VM 使用參照*VIP:&lt;連接埠號碼 >*以輸入通訊。 保留 IP，並不表示您可以直接連接 toohello VM。 hello 保留的 IP 會被指派 toohello 雲端服務 VM 已部署至該 hello。 若要直接 tooconnect tooa VM 的 IP，您有 tooconfigure 執行個體層級公用 IP。 執行個體層級公用 IP 是一種公用 IP （稱為 ILPIP），會直接指派 tooyour VM。 此類型 IP 無法保留。 如需詳細資訊，請閱讀 hello[執行個體層級公用 IP (ILPIP)](virtual-networks-instance-level-public-ip.md)發行項。
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a>從執行中部署移除保留的 IP
保留 IP tooremove 加入 tooa 新雲端服務，請執行下列 PowerShell 命令的 hello:

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> 從執行中部署移除保留的 IP 並不會從您的訂用帳戶移除 hello 保留項目。 它會釋出 hello IP toobe 您訂用帳戶中的另一個資源所使用。
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a>執行部署的保留的 IP tooa 產生關聯
hello 下列命令會建立名為雲端服務*TestService2*與名為的新 VM *TestVM2*。 現有的 hello 保留的 IP 名為*myreservedip 產生*則相關聯的 toohello 雲端服務。

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a>使用服務組態檔相關聯的保留的 IP tooa 雲端服務
您也可以使用服務組態檔 (CSCFG) 關聯保留的 IP tooa 雲端服務。 hello 下列範例 xml 會說明如何 tooconfigure 保留 VIP 的雲端服務 toouse 命名*myreservedip 產生*:

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a>後續步驟
* 了解如何[IP 定址](virtual-network-ip-addresses-overview-classic.md)hello 傳統部署模型中的運作方式。
* 深入了解 [保留的私人 IP 位址](virtual-networks-reserved-private-ip.md)。
* 深入了解 [執行個體層級公用 IP (ILPIP) 位址](virtual-networks-instance-level-public-ip.md)。

