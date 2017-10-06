---
title: "如何 tooconfigure ExpressRoute 電路的路由 （對等互連）： 資源管理員： Azure |Microsoft 文件"
description: "這篇文章會引導您完成建立及佈建 hello 私人、 公用及 Microsoft 對等互連的 ExpressRoute 電路的 hello 步驟。 本文也會顯示 toocheck hello 狀態、 更新或刪除您的電路的互連的方式。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a>建立和修改 ExpressRoute 線路的對等互連

這篇文章可協助您建立和管理 ExpressRoute 電路 hello Resource Manager 部署模型使用 hello Azure 入口網站中的路由組態。 您也可以檢查 hello 狀態、 更新或刪除，並取消佈建 ExpressRoute 循環的對等互連。 如果您想 toouse 不同方法 toowork 與您的循環，請從下列清單中的 hello 選取一個發行項：


## <a name="configuration-prerequisites"></a>組態必要條件

* 請確定您已經檢閱 hello[必要條件](expressroute-prerequisites.md)頁面 hello[路由需求](expressroute-routing.md)頁面和 hello[工作流程](expressroute-workflows.md)頁面開始設定之前。
* 您必須擁有作用中的 ExpressRoute 線路。 請依照下列指示 hello 太[建立 ExpressRoute 電路](expressroute-howto-circuit-portal-resource-manager.md)和有 hello 電路啟用您的連線提供者，才能繼續。 hello ExpressRoute 電路必須位於您 toobe 無法 toorun hello cmdlet hello 下一節中的佈建並啟用狀態。
* 如果您計劃 toouse 共用金鑰/MD5 雜湊，是確定 toouse 這兩端 hello 通道和 limit hello 數目的字元 tooa 最大值為 25。

這些說明僅適用於 toocircuits 建立與服務供應項目層級 2 連線服務的提供者。 如果您使用的服務提供者提供受管理的第 3 層服務 (通常是 IPVPN，如 MPLS)，連線提供者會為您設定和管理路由。 

> [!IMPORTANT]
> 我們目前不會進行通告透過 hello 服務管理入口網站的服務提供者所設定的對等互連。 我們正努力在近期推出這項功能。 設定 BGP 對等互連之前，請洽詢您的服務提供者。
> 
> 

您可以為 ExpressRoute 線路設定一個、兩個或全部三個對等 (Azure 私用、Azure 公用和 Microsoft)。 您可以依自己選擇的任何順序設定對等。 不過，您必須確定您完成每個對等互連一次一個的 hello 設定。

## <a name="azure-private-peering"></a>Azure 私用對等

本節可協助您建立、 取得、 更新和刪除 hello Azure ExpressRoute 循環的私用對等設定。

### <a name="toocreate-azure-private-peering"></a>toocreate Azure 私人互連

1. 設定 hello ExpressRoute 電路。 確保 hello 循環完全佈建的 hello 連線服務提供者才能繼續。

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. 設定 Azure 私用對等互連 hello 循環。 請確定您具備下列項目，再繼續進行下一個步驟的 hello hello:

  * / 30 子網路 hello 主要連結。 hello 子網路不能保留的虛擬網路的任何位址空間的一部分。
  * / 30 hello 次要連結的子網路。 hello 子網路不能保留的虛擬網路的任何位址空間的一部分。
  * 有效的 VLAN ID tooestablish 此對等。 請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。
  * 對等的 AS 編號。 您可以使用 2 位元組和 4 位元組 AS 編號。 您可以將私用 AS 編號用於此對等。 請確定您不是使用 65515。
  * **選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。
3. 選取 hello Azure 私用的對等資料列，hello 下列範例所示：

  ![私用](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. 設定私用對等。 hello 下列影像顯示組態範例：

  ![設定私用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. 一旦您已指定所有參數，請儲存 hello 組態。 已成功接受 hello 組態之後，您會看到類似下列範例的 toohello:

  ![儲存私用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a>tooview Azure 私用對等互連的詳細資料

您可以檢視選取對等互連 hello Azure 私人互連的 hello 的屬性。

![檢視私用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate Azure 私用對等組態

您可以選取 hello 資料列的對等互連，並修改 hello 對等屬性。

![更新私用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a>toodelete Azure 私人互連

Hello 下列影像所示，您可以藉由選取 hello 刪除圖示，移除您對等的設定：

![刪除私用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a>Azure 公用對等

本節可協助您建立、 取得、 更新和刪除 hello Azure ExpressRoute 循環的公用對等設定。

### <a name="toocreate-azure-public-peering"></a>toocreate Azure 公用對等互連

1. 設定 ExpressRoute 電路。 確保 hello 循環完全佈建的 hello 連線服務提供者再進一步繼續。

  ![列出公用對等互連](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. 設定 Azure 公用對等互連 hello 循環。 請確定您具備下列項目，再繼續進行下一個步驟的 hello hello:

  * / 30 子網路 hello 主要連結。 這必須是有效的公用 IPv4 首碼。
  * / 30 hello 次要連結的子網路。 這必須是有效的公用 IPv4 首碼。
  * 有效的 VLAN ID tooestablish 此對等。 請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。
  * 對等的 AS 編號。 您可以使用 2 位元組和 4 位元組 AS 編號。
  * **選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。
3. 請選取 hello Azure 公用對等資料列，hello 下列影像所示：

  ![選取公用對等互連列](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. 設定公用對等。 hello 下列影像顯示組態範例：

  ![設定公用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. 一旦您已指定所有參數，請儲存 hello 組態。 已成功接受 hello 組態之後，您會看到類似下列範例的 toohello:

  ![儲存公用對等互連設定](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a>tooview Azure 公用對等互連的詳細資料

您可以檢視選取對等互連 hello Azure 公用對等的 hello 的屬性。

![檢視公用對等互連屬性](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate Azure 公用對等組態

您可以選取 hello 資料列的對等互連，並修改 hello 對等屬性。

![選取公用對等互連列](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a>toodelete Azure 公用對等互連

Hello 下列範例所示，您可以藉由選取 hello 刪除圖示，移除您對等的設定：

![刪除公用對等互連](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a>Microsoft 對等互連

本節可協助您建立、 取得、 更新和刪除 ExpressRoute 循環的 hello Microsoft 對等設定。

> [!IMPORTANT]
> Microsoft 對等互連的 ExpressRoute 電路已設定先前 tooAugust 1，2017年必須透過 hello Microsoft 對等互連，公告的所有服務首碼，即使未定義路由篩選器。 Microsoft 對等互連的當天或之後 2017 年 8 月 1，已設定的 ExpressRoute 電路並不會有任何前置詞通告的路由篩選器連接直到 toohello 循環。 如需詳細資訊，請參閱[設定 Microsoft 對等互連的路由篩選](how-to-routefilter-powershell.md)。
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate Microsoft 對等互連

1. 設定 ExpressRoute 電路。 確保 hello 循環完全佈建的 hello 連線服務提供者再進一步繼續。

  ![列出 Microsoft 對等互連](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. 設定 Microsoft 對等互連 hello 循環。 請確定您擁有 hello 下列資訊才能繼續。

  * / 30 子網路 hello 主要連結。 這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。
  * / 30 hello 次要連結的子網路。 這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。
  * 有效的 VLAN ID tooestablish 此對等。 請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。
  * 對等的 AS 編號。 您可以使用 2 位元組和 4 位元組 AS 編號。
  * 通告前置詞： 您必須提供清單的所有前置詞您計劃 tooadvertise 透過 hello BGP 工作階段。 只接受公用 IP 位址首碼。 如果您計劃 toosend 一組前置詞，您可以傳送的逗號分隔清單。 這些前置詞必須是已註冊的 tooyou 在 RIR / IRR。
  * **選用-**客戶 ASN： 如果您不是數字的已註冊的 toohello 對等互連的廣告前置詞，您可以指定 hello 為其所註冊的數字 toowhich。
  * 路由登錄名稱： 您可以指定 hello RIR / IRR 哪些 hello 做為數字，但前置詞會註冊。
  * **選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。
3. 您可以選取 hello 對等互連想 tooconfigure，hello 下列所示範例。 選取 hello Microsoft 對等資料列。

  ![選取 Microsoft 對等互連列](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. 設定 Microsoft 對等。 hello 下列影像顯示組態範例：

  ![設定 Microsoft 對等互連](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. 一旦您已指定所有參數，請儲存 hello 組態。

  如果您的電路取得 tooa '所需的驗證' 狀態 （如 hello 映像中所示），您必須開啟支援票證 tooshow hello 前置詞 tooour 支援小組擁有權證明。

  ![儲存 Microsoft 對等互連設定](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  您可以直接從 hello 入口網站中，開啟支援票證，hello 下列範例所示：

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. 已成功接受 hello 組態之後，您會看到類似下列映像的 toohello:

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a>tooview Microsoft 對等詳細資料

您可以檢視選取對等互連 hello Azure 公用對等的 hello 的屬性。

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a>tooupdate Microsoft 對等組態

您可以選取 hello 資料列的對等互連，並修改 hello 對等屬性。

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a>toodelete Microsoft 對等互連

Hello 下列影像所示，您可以藉由選取 hello 刪除圖示，移除您對等的設定：

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a>後續步驟

下一步，[連結 VNet tooan ExpressRoute 電路](expressroute-howto-linkvnet-portal-resource-manager.md)
* 如需 ExpressRoute 工作流程的詳細資訊，請參閱 [ExpressRoute 工作流程](expressroute-workflows.md)。
* 如需線路對等的詳細資訊，請參閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)。
* 如需使用虛擬網路的詳細資訊，請參閱 [虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。
