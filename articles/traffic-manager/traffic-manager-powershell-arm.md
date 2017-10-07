---
title: "aaaUsing PowerShell toomanage Traffic Manager Azure |Microsoft 文件"
description: "使用 PowerShell 透過 Azure Resource Manager 執行流量管理員"
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a>使用 PowerShell toomanage Traffic Manager

Azure 資源管理員是在 Azure 中服務的 hello 慣用的管理介面。 您可以使用以 Azure Resource Manager 為基礎的 API 和工具來管理 Azure 流量管理員設定檔。

## <a name="resource-model"></a>資源模型

Azure 流量管理員使用名為「流量管理員設定檔」的設定集合進行設定。 此設定檔包含 DNS 設定、 流量路由設定、 端點監視設定，以及一份服務端點 toowhich 流量路由傳送。

每個流量管理員設定檔都以 'TrafficManagerProfiles' 類型的資源表示。 在 hello REST API 層級，每個設定檔的 hello URI 如下所示：

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a>設定 Azure PowerShell

這些指示使用 Microsoft Azure PowerShell。 hello 下列文章說明如何 tooinstall 和設定 Azure PowerShell。

* [如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)

本文中的 hello 範例假設您有現有的資源群組。 您可以建立資源群組，使用下列命令的 hello:

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> Azure Resource Manager 規定所有資源群組都要有位置。 Hello 預設會使用這個位置建立該資源群組中的資源。 不過，由於 Traffic Manager 設定檔的資源都是全域，不是地區，hello 所選擇的資源群組位置沒有任何影響有關 Azure Traffic Manager。

## <a name="create-a-traffic-manager-profile"></a>建立流量管理員設定檔

toocreate Traffic Manager 設定檔，使用 hello `New-AzureRmTrafficManagerProfile` cmdlet:

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

hello 下表描述 hello 參數：

| 參數 | 說明 |
| --- | --- |
| 名稱 |hello hello Traffic Manager 設定檔資源的資源名稱。 中的設定檔 hello 相同資源群組必須具有唯一的名稱。 這個名稱是分開 hello 所使用的 DNS 查詢的 DNS 名稱。 |
| resourceGroupName |hello hello 資源群組包含 hello 設定檔資源名稱。 |
| TrafficRoutingMethod |指定 hello 流量路由方法使用的 toodetermine 哪一個端點回應中傳回的 DNS 查詢。 可能的值為 'Performance'、'Weighted' 或 'Priority'。 |
| RelativeDnsName |指定此 Traffic Manager 設定檔所提供的 hello DNS 名稱 hello 主機名稱部分。 這個值會結合 hello Azure Traffic Manager tooform hello 完整的網域名稱 (FQDN) 的 hello 設定檔所使用的 DNS 網域名稱。 例如，設定 'contoso' hello 值會變成 'contoso.trafficmanager.net。' |
| TTL |指定 hello DNS--存留時間 (TTL)，以秒為單位。 Hello 本機 DNS 解析程式和 DNS 用戶端，此 TTL 會通知此流量管理員設定檔的時間長度 toocache DNS 回應。 |
| MonitorProtocol |指定 hello 通訊協定 toouse toomonitor 端點健全狀況。 可能的值為 'HTTP' 和 'HTTPS'。 |
| MonitorPort |指定 hello TCP 連接埠使用 toomonitor 端點健全狀況。 |
| MonitorPath |指定 hello 路徑相對 toohello 端點網域名稱使用 tooprobe 端點健全狀態。 |

hello cmdlet 在 Azure 中建立的 Traffic Manager 設定檔，並傳回對應的設定檔物件 tooPowerShell。 此時，hello 設定檔不包含任何端點。 如需新增端點 tooa Traffic Manager 設定檔的詳細資訊，請參閱[新增 Traffic Manager 端點](#adding-traffic-manager-endpoints)。

## <a name="get-a-traffic-manager-profile"></a>取得流量管理員設定檔

tooretrieve 現有的 Traffic Manager 設定檔物件，使用 hello `Get-AzureRmTrafficManagerProfle` cmdlet:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

此 Cmdlet 會傳回流量管理員設定檔物件。

## <a name="update-a-traffic-manager-profile"></a>更新流量管理員設定檔

修改流量管理員設定檔需要 3 個步驟︰

1. 擷取 hello 設定檔使用`Get-AzureRmTrafficManagerProfile`或使用 hello 設定檔所傳回`New-AzureRmTrafficManagerProfile`。
2. 修改 hello 設定檔。 您可以新增和移除端點，也可以變更端點或設定檔參數。 這些變更是離線作業。 您只變更代表 hello 設定檔的記憶體中的 hello 本機物件。
3. 認可您的變更使用 hello `Set-AzureRmTrafficManagerProfile` cmdlet。

除非 RelativeDnsName hello 設定檔可以變更所有設定檔屬性。 toochange hello RelativeDnsName，您必須刪除設定檔和新的設定檔，以新名稱。

hello 下列範例將示範如何 toochange hello 設定檔的 TTL:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

流量管理員端點有三種類型：

1. **Azure 端點**是 Azure 中託管的服務。
2. **外部端點**是 Azure 外部託管的服務。
3. **巢狀端點**Traffic Manager 設定檔使用的 tooconstruct 巢狀階層。 巢狀端點可讓複雜的應用程式使用進階的流量路由設定。

不論是這三種端點中的哪一種，您都可以透過兩種方式來新增端點：

1. 使用先前所述的 3 步驟程序。 這個方法的 hello 優點是可以在單一更新進行數個端點變更。
2. 使用 hello 新增 AzureRmTrafficManagerEndpoint cmdlet。 這個 cmdlet 會在單一作業中加入端點 tooan 現有流量管理員設定檔。

## <a name="adding-azure-endpoints"></a>新增 Azure 端點

Azure 端點會參考 Azure 中託管的服務。 支援兩種 Azure 端點：

1. Azure Web Apps 
2. Azure PublicIpAddress 資源 （這可以是附加的 tooa 負載平衡器或虛擬機器 NIC）。 hello PublicIpAddress 必須指派 toobe 使用 Traffic Manager 中的 DNS 名稱。

不論是上述哪一種，都必須注意以下事項：

* hello 服務使用 hello 'targetResourceId' 參數所指定`Add-AzureRmTrafficManagerEndpointConfig`或`New-AzureRmTrafficManagerEndpoint`。
* hello 'Target' 和 'EndpointLocation' 由隱含 hello TargetResourceId。
* 指定 hello 'Weight' 是選擇性的。 加權時，才會使用 hello 設定檔是否設定的 toouse hello '加權' 流量路由方法。 否則會予以忽略。 如果指定，hello 值必須介於 1 到 1000年之間的數字。 hello 預設值為 '1'。
* 指定 hello 'Priority' 是選擇性的。 Hello 設定檔是否設定的 toouse hello 'Priority' 流量路由方法時，才會使用優先順序。 否則會予以忽略。 有效值從 1 too1000 具有較低的值表示較高的優先順序。 如果對某個端點指定值，則所有端點也都必須進行指定。 如果省略，開始從 '1' 的預設值會套用 hello hello 端點所列的順序。

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a>範例 1︰使用 `Add-AzureRmTrafficManagerEndpointConfig` 新增 Web 應用程式端點

在此範例中，我們建立 Traffic Manager 設定檔，並加入兩個 Web 應用程式端點使用 hello `Add-AzureRmTrafficManagerEndpointConfig` cmdlet。

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a>範例 2︰使用 `New-AzureRmTrafficManagerEndpoint` 新增 publicIpAddress 端點

在此範例中，公用 IP 位址資源加入 toohello Traffic Manager 設定檔。 hello 公用 IP 位址都必須有 DNS 名稱設定，而且可以繫結任一 toohello NIC 的 VM 或 tooa 負載平衡器。

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a>新增外部端點

流量管理員會使用外部端點 toodirect 流量 tooservices Azure 外部所裝載。 如同 Azure 端點一樣，使用 `Add-AzureRmTrafficManagerEndpointConfig` 再接著使用 `Set-AzureRmTrafficManagerProfile`，或使用 `New-AzureRMTrafficManagerEndpoint`，都可以新增外部端點。

指定外部端點時：

* 必須使用 hello 'Target' 參數指定 hello 端點網域名稱
* 如果使用 「 效能 」 流量路由方法 hello，hello 'EndpointLocation' 需要。 否則為選擇性。 hello 值必須是[有效的 Azure 區域名稱](https://azure.microsoft.com/regions/)。
* hello '加權'，'Priority' 是選擇性的。

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>範例 1︰使用 `Add-AzureRmTrafficManagerEndpointConfig` 和 `Set-AzureRmTrafficManagerProfile` 新增外部端點

在此範例中，我們可以建立 Traffic Manager 設定檔、 新增兩個外部端點，以及認可 hello 變更。

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a>範例 2︰使用 `New-AzureRmTrafficManagerEndpoint` 新增外部端點

在此範例中，我們加入外部端點 tooan 現有的設定檔。 hello 設定檔來指定 hello 設定檔和資源群組名稱。

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a>新增「巢狀」端點

每個「流量管理員」設定檔皆指定一個流量路由方法。 不過，有一些需要更複雜的流量路由比 hello 路由單一 Traffic Manager 設定檔所提供的案例。 您可以巢狀多個流量路由方法的 Traffic Manager 設定檔 toocombine hello 優點。 巢狀設定檔可讓您 toooverride hello 預設 Traffic Manager 行為 toosupport 較大和更複雜的應用程式部署。 如需詳細範例，請參閱[巢狀流量管理員設定檔](traffic-manager-nested-profiles.md)。

巢狀的端點是在 hello 父系設定檔，使用特定端點的型別、 'NestedEndpoints' 設定。 指定巢狀端點時︰

* 必須使用 hello 'targetResourceId' 參數指定 hello 端點
* 如果使用 「 效能 」 流量路由方法 hello，hello 'EndpointLocation' 需要。 否則為選擇性。 hello 值必須是[有效的 Azure 區域名稱](http://azure.microsoft.com/regions/)。
* hello '加權'，'Priority' 是選擇性的與 Azure 的端點。
* hello 'MinChildEndpoints' 參數是選擇性的。 hello 預設值為 '1'。 Hello 可用的端點數目低於此臨界值時，如果 hello 父系設定檔會考慮 hello 子系的設定檔 '降低'，且 diverts 流量 toohello hello 父系設定檔中的其他端點。

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>範例 1︰使用 `Add-AzureRmTrafficManagerEndpointConfig` 和 `Set-AzureRmTrafficManagerProfile` 新增巢狀端點

在此範例中，我們可以建立新的 Traffic Manager 子系和父系設定檔、 新增 hello 子系為巢狀的端點 toohello 父代，以及認可 hello 變更。

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

為求簡潔，在此範例中，我們沒有新增任何其他端點 toohello 子系或父系設定檔。

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a>範例 2︰使用 `New-AzureRmTrafficManagerEndpoint` 新增巢狀端點

在此範例中，我們會加入現有的子系設定檔為巢狀的端點 tooan 現有父系設定檔。 hello 設定檔來指定 hello 設定檔和資源群組名稱。

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a>更新流量管理員端點

有兩種方式 tooupdate 現有流量管理員端點：

1. 取得 hello Traffic Manager 設定檔使用`Get-AzureRmTrafficManagerProfile`、 更新 hello 設定檔中的 hello 端點內容，以及認可 hello 變更使用`Set-AzureRmTrafficManagerProfile`。 這個方法沒有 hello 優點是能夠 tooupdate 在單一作業中的多個端點。
2. 取得 hello Traffic Manager 端點使用`Get-AzureRmTrafficManagerEndpoint`、 更新 hello 端點內容，以及認可使用的 hello 變更`Set-AzureRmTrafficManagerEndpoint`。 這個方法是比較簡單，，因為它不需要對 hello 設定檔中的 hello 端點陣列進行索引。

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a>範例 1︰使用 `Get-AzureRmTrafficManagerProfile` 和 `Set-AzureRmTrafficManagerProfile` 更新端點

在此範例中，我們會修改現有的設定檔中的兩個端點上的 hello 優先順序。

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a>範例 2︰使用 `Get-AzureRmTrafficManagerEndpoint` 和 `Set-AzureRmTrafficManagerEndpoint` 更新端點

在此範例中，我們會修改 hello 加權中現有的設定檔的單一端點。

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a>啟用和停用端點和設定檔

Traffic Manager 可讓個別端點 toobe 啟用和停用，以及允許啟用及停用整個設定檔。
取得/更新/設定 hello 端點或設定檔的資源，就可以進行這些變更。 toostreamline 這些常見的作業，它們也支援透過專用 cmdlet。

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a>範例 1：啟用和停用流量管理員設定檔

tooenable Traffic Manager 設定檔，使用`Enable-AzureRmTrafficManagerProfile`。 可以使用設定檔物件，指定 hello 設定檔。 hello 設定檔物件可以傳遞透過 hello 管線或使用 hello '-TrafficManagerProfile' 參數。 在此範例中，我們會藉由 hello 設定檔和資源群組名稱指定 hello 設定檔。

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

toodisable Traffic Manager 設定檔：

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

hello 停用 AzureRmTrafficManagerProfile cmdlet 會提示確認。 此提示可使用，以歸併 hello '-Force' 參數。

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a>範例 2：啟用和停用流量管理員端點

tooenable Traffic Manager 端點使用`Enable-AzureRmTrafficManagerEndpoint`。 有兩種方式 toospecify hello 端點

1. 使用透過 hello 管線傳遞 TrafficManagerEndpoint 物件，或使用 hello '-TrafficManagerEndpoint' 參數
2. 使用 hello 端點名稱、 端點類型、 設定檔名稱和資源群組名稱：

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

同樣地，toodisable 流量管理員端點：

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

如同`Disable-AzureRmTrafficManagerProfile`，hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet 會提示確認。 此提示可使用，以歸併 hello '-Force' 參數。

## <a name="delete-a-traffic-manager-endpoint"></a>停用流量管理員端點

tooremove 個別的端點，請使用 hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

這個 Cmdlet 會提示您確認。 此提示可使用，以歸併 hello '-Force' 參數。

## <a name="delete-a-traffic-manager-profile"></a>刪除流量管理員設定檔

toodelete Traffic Manager 設定檔，使用 hello`Remove-AzureRmTrafficManagerProfile`指令程式，指定 hello 設定檔和資源群組名稱：

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

這個 Cmdlet 會提示您確認。 此提示可使用，以歸併 hello '-Force' 參數。

刪除 hello 設定檔 toobe 也可以使用設定檔物件來指定：

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

也可輸送以下順序：

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a>後續步驟

[流量管理員監視](traffic-manager-monitoring.md)

[流量管理員的效能考量](traffic-manager-performance-considerations.md)
