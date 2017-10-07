---
title: "設定 Azure ExpressRoute Microsoft 對等互連的路由篩選：PowerShell | Microsoft Docs"
description: "本文說明如何 tooconfigure 路由篩選使用 PowerShell 的 Microsoft 對等互連"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a>針對 Microsoft 對等互連設定路由篩選

路由篩選條件是方式 tooconsume 支援的服務，透過 Microsoft 對等的子集。 此文章說明您設定和管理 ExpressRoute 電路的路由篩選器中的步驟 hello。

Dynamics 365 服務和 Office 365 服務例如 Exchange Online、 SharePoint Online 及 Skype for Business，都可存取透過 hello Microsoft 對等互連。 當 Microsoft 對等互連設定 ExpressRoute 循環中時，所有的前置詞相關的 toothese 服務會通告透過 hello BGP 工作階段所建立的。 BGP 社群值為附加的 tooevery 前置詞 tooidentify hello 服務提供透過 hello 前置詞。 如需 hello BGP 社群值和它們對應到 hello 服務的清單，請參閱[BGP 社群](expressroute-routing.md#bgp)。

如果您需要連線 tooall 服務時，大量的前置詞會透過 BGP 公告。 這會大幅增加 hello 的 hello 維護您網路中路由器的路由表的大小。 如果您計劃的 tooconsume 透過 Microsoft 對等提供服務的子集，您可以減少 hello 資料表大小的路由有兩種。 您可以：

- 在 BGP 社群上套用路由篩選，以篩選不想要的前置詞。 這是標準網路做法，在許多網路經常使用。

- 定義路由篩選器，並將其套用 tooyour ExpressRoute 電路。 路由篩選條件是新的資源，可讓您選取的 hello 清單服務您計劃 tooconsume 透過 Microsoft 對等互連。 ExpressRoute 路由器只會傳送 hello 隸屬 toohello 服務 hello 路由篩選器中所識別的前置詞清單。

### <a name="about"></a>關於路由篩選

當 Microsoft 對等互連設定 ExpressRoute 電路上時，hello Microsoft 邊緣路由器會建立一組 BGP 工作階段與 hello 邊緣路由器 （您或您的連線提供者）。 不為通告的 tooyour 網路的任何路由。 tooenable 路由通告 tooyour 網路，您必須建立關聯路由篩選器。

路由篩選器可讓您識別您想要透過 ExpressRoute 循環的 Microsoft 對等互連 tooconsume 的服務。 它基本上是空白清單的所有 hello BGP 社群值。 當路由篩選資源定義，並附加 tooan ExpressRoute 循環時，所有 toohello BGP 社群值對應的前置詞都是以通告的 tooyour 網路。

toobe 無法 tooattach 和 Office 365 服務在其上的路由篩選，您必須透過 ExpressRoute 授權 tooconsume Office 365 服務。 如果您不是授權的 tooconsume Office 365 服務透過 ExpressRoute，hello 作業 tooattach 路由篩選器將會失敗。 如需 hello 授權程序的詳細資訊，請參閱[for Office 365 的 Azure ExpressRoute](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)。 連線 tooDynamics 365 服務不需要任何先前的授權。

> [!IMPORTANT]
> Microsoft 對等互連的 ExpressRoute 電路已設定先前 tooAugust 1，2017年必須透過 Microsoft 對等互連，公告的所有服務首碼，即使未定義路由篩選器。 Microsoft 對等互連的當天或之後 2017 年 8 月 1，已設定的 ExpressRoute 電路並不會有任何前置詞通告的路由篩選器連接直到 toohello 循環。
> 
> 

### <a name="workflow"></a>工作流程

toobe 無法 toosuccessfully 連接 tooservices 透過 Microsoft 對等互連，您必須完成下列組態步驟的 hello:

- 您必須具有已佈建 Microsoft 對等互連的使用中 ExpressRoute 線路。 您可以使用下列指示 tooaccomplish hello 這些工作：
  - [建立 ExpressRoute 電路](expressroute-howto-circuit-arm.md)和有 hello 電路啟用您的連線提供者，才能繼續。 hello ExpressRoute 電路必須在佈建並啟用狀態。
  - [建立 Microsoft 對等互連](expressroute-circuit-peerings.md)如果您管理直接 hello BGP 工作階段。 或者，讓您的連線提供者為您的線路佈建 Microsoft 對等互連。

-  您必須建立及設定路由篩選。
    - 找出 hello 服務 tooconsume 透過 Microsoft 對等互連
    - 識別 hello 與 hello 服務相關聯的 BGP 社群值的清單
    - 建立規則 tooallow hello 前置詞清單相符 hello BGP 社群值

-  您必須將附加 hello 路由篩選 toohello ExpressRoute 電路。

## <a name="before-you-begin"></a>開始之前

開始設定之前，請確定您符合下列準則的 hello:

 - 安裝 hello hello Azure 資源管理員的 PowerShell 指令程式最新版本。 如需詳細資訊，請參閱[安裝和設定 Azure PowerShell](/powershell/azure/install-azurerm-ps)。

  > [!NOTE]
  > 從 hello PowerShell 資源庫，而不是使用 hello 安裝程式下載 hello 最新版本。 hello 安裝程式目前不支援所需的 hello cmdlet。
  > 

 - 檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。

 - 您必須擁有作用中的 ExpressRoute 線路。 請依照下列指示 hello 太[建立 ExpressRoute 電路](expressroute-howto-circuit-arm.md)和有 hello 電路啟用您的連線提供者，才能繼續。 hello ExpressRoute 電路必須在佈建並啟用狀態。

 - 您必須擁有使用中 Microsoft 對等互連。 請遵循[建立和修改對等互連設定](expressroute-circuit-peerings.md)的指示

### <a name="log-in-tooyour-azure-account"></a>登入 tooyour Azure 帳戶

開始之前這項設定，您必須登入 tooyour Azure 帳戶。 hello cmdlet 會提示您輸入您的 Azure 帳戶的 hello 登入認證。 登入之後，它會下載您的帳戶設定，這樣就可以使用 tooAzure PowerShell。

以較高的權限開啟 PowerShell 主控台並連接 tooyour 帳戶。 使用下列範例 toohelp 您連接的 hello:

```powershell
Login-AzureRmAccount
```

如果您有多個 Azure 訂用帳戶，請檢查 hello hello 帳戶的訂用帳戶。

```powershell
Get-AzureRmSubscription
```

指定您想 toouse hello 訂用帳戶。

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <a name="prefixes"></a>步驟 1. 取得前置詞和 BGP 社群值的清單

### <a name="1-get-a-list-of-bgp-community-values"></a>1.取得 BGP 社群值的清單

使用下列 cmdlet tooget hello 清單 BGP 社群相關聯的值與可透過 Microsoft 對等互連，存取服務的 hello 和 hello 與其相關聯的前置詞的清單：

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a>2.進行您想 toouse hello 值的清單

建立一份您想要的 BGP 社群值 toouse hello 路由篩選器中。 例如，hello Dynamics 365 服務的 BGP 社群值會是 12076:5040。

## <a name="filter"></a>步驟 2. 建立路由篩選和篩選規則

路由篩選條件可以有只有一個規則，並 hello 規則必須是 'Allow'，型別。 此規則可以具有與其相關聯的 BGP 社群值清單。

### <a name="1-create-a-route-filter"></a>1.建立路由篩選

首先，建立 hello 路由篩選器。 hello 命令 ' 新增 AzureRmRouteFilter' 只建立路由篩選條件的資源。 建立 hello 資源之後，您必須建立規則，然後將它附加 toohello 路由篩選物件。 執行下列命令 toocreate hello 路由篩選資源：

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a>2.建立篩選規則

Hello 範例所示，您可以指定一組 BGP 社群為以逗號分隔清單。 執行下列命令 toocreate hello 新的規則：
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a>3.新增 hello 規則 toohello 路由篩選器

執行下列命令 tooadd hello 篩選器規則 toohello 路由篩選器的 hello:
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <a name="attach"></a>步驟 3. 附加 hello 路由篩選 tooan ExpressRoute 電路

執行下列命令 tooattach hello 路由篩選 toohello ExpressRoute 循環，假設您有唯一的 Microsoft 對等的 hello:

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="getproperties"></a>tooget hello 屬性的路由篩選器

路由篩選器，使用下列步驟的 hello tooget hello 屬性：

1. 執行下列命令 tooget hello 路由篩選資源 hello:

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. 藉由執行下列命令的 hello hello 路由篩選器資源取得 hello 路由篩選規則：

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <a name="updateproperties"></a>tooupdate hello 屬性的路由篩選器

如果已附加 hello 路由篩選器 tooa 循環，更新 toohello BGP 社群清單會自動傳播 hello 建立 BGP 工作階段的廣告變更適當的前置詞。 您可以更新您的路由篩選器，使用下列命令的 hello hello BGP 社群清單：

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <a name="detach"></a>toodetach ExpressRoute 電路的路由篩選條件

一旦從 hello ExpressRoute 電路卸離路由篩選器時，沒有前置詞會通告透過 hello BGP 工作階段。 您可以卸離使用下列命令的 hello ExpressRoute 電路的路由篩選條件：
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="delete"></a>toodelete 路由篩選器

您只能刪除路由篩選器如果不是附加 tooany 循環。 請確定該 hello 路由篩選條件不會附加 tooany 循環，然後再嘗試 toodelete 它。 您可以刪除路由篩選條件使用 hello 下列命令：

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a>後續步驟

如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。
