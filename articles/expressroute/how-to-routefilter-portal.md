---
title: "設定 Azure ExpressRoute Microsoft 對等互連的路由篩選：入口網站 | Microsoft Docs"
description: "本文說明如何使用 Microsoft 對等互連 tooconfigure 路由篩選 hello Azure 入口網站"
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
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
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
  - [建立 ExpressRoute 電路](expressroute-howto-circuit-portal-resource-manager.md)和有 hello 電路啟用您的連線提供者，才能繼續。 hello ExpressRoute 電路必須在佈建並啟用狀態。
  - [建立 Microsoft 對等互連](expressroute-howto-routing-portal-resource-manager.md)如果您管理直接 hello BGP 工作階段。 或者，讓您的連線提供者為您的線路佈建 Microsoft 對等互連。

-  您必須建立及設定路由篩選。
    - 找出 hello 服務 tooconsume 透過 Microsoft 對等互連
    - 識別 hello 與 hello 服務相關聯的 BGP 社群值的清單
    - 建立規則 tooallow hello 前置詞清單相符 hello BGP 社群值

-  您必須將附加 hello 路由篩選 toohello ExpressRoute 電路。

## <a name="before-you-begin"></a>開始之前

開始設定之前，請確定您符合下列準則的 hello:

 - 檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。

 - 您必須擁有作用中的 ExpressRoute 線路。 請依照下列指示 hello 太[建立 ExpressRoute 電路](expressroute-howto-circuit-portal-resource-manager.md)和有 hello 電路啟用您的連線提供者，才能繼續。 hello ExpressRoute 電路必須在佈建並啟用狀態。

 - 您必須擁有使用中 Microsoft 對等互連。 請遵循[建立和修改對等互連設定](expressroute-howto-routing-portal-resource-manager.md)的指示


## <a name="prefixes"></a>步驟 1. 取得前置詞和 BGP 社群值的清單

### <a name="1-get-a-list-of-bgp-community-values"></a>1.取得 BGP 社群值的清單

服務可透過 Microsoft 對等互連存取相關聯的 BGP 社群值位於 hello [ExpressRoute 路由需求](expressroute-routing.md)頁面。

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a>2.進行您想 toouse hello 值的清單

建立一份您想要的 BGP 社群值 toouse hello 路由篩選器中。 例如，hello Dynamics 365 服務的 BGP 社群值會是 12076:5040。

## <a name="filter"></a>步驟 2. 建立路由篩選和篩選規則

路由篩選條件可以有只有一個規則，並 hello 規則必須是 'Allow'，型別。 此規則可以具有與其相關聯的 BGP 社群值清單。

### <a name="1-create-a-route-filter"></a>1.建立路由篩選
您可以藉由選取 hello 選項 toocreate 建立路由篩選器，新的資源。 按一下**新增** > **網路** > **RouteFilter**hello 下列影像所示：

![建立路由篩選](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

您必須在資源群組中放置 hello 路由篩選器。 

![建立路由篩選](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a>2.建立篩選規則

您可以新增和更新規則，藉由選取 hello 管理您的路由篩選條件的規則索引標籤。

![建立路由篩選](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


您可以選取的 hello 服務想 tooconnect toofrom hello 下拉式清單並儲存完成的 hello 規則。

![建立路由篩選](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <a name="attach"></a>步驟 3. 附加 hello 路由篩選 tooan ExpressRoute 電路

您可以選取"hello 新增循環 按鈕，從 hello 下拉式清單選取 hello ExpressRoute 電路附加 hello 路由篩選 tooa 循環。

![建立路由篩選](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <a name="getproperties"></a>tooget hello 屬性的路由篩選器

當您開啟 hello 入口網站中的 hello 資源時，您可以檢視路由篩選器的屬性。

![建立路由篩選](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <a name="updateproperties"></a>tooupdate hello 屬性的路由篩選器

您可以藉由選取 hello 「 管理規則 」 按鈕更新 BGP 社群值附加的 tooa 循環的 hello 清單。


![建立路由篩選](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![建立路由篩選](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <a name="detach"></a>toodetach ExpressRoute 電路的路由篩選條件

toodetach hello 路由篩選器，從電路 hello 電路上按一下滑鼠右鍵，並按一下 「 取消 」 的關聯。

![建立路由篩選](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <a name="delete"></a>toodelete 路由篩選器

您可以選取 hello [刪除] 按鈕來刪除路由篩選器。 

![建立路由篩選](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a>後續步驟

如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。
