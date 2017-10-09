---
title: "使用 Azure 入口網站 hello aaaManage Nsg |Microsoft 文件"
description: "深入了解如何 toomanage 現有 Nsg 使用 hello Azure 入口網站。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a>管理 Nsg 使用 hello 入口網站

> [!div class="op_single_selector"]
> * [入口網站](virtual-network-manage-nsg-arm-portal.md)
> * [PowerShell](virtual-network-manage-nsg-arm-ps.md)
> * [Azure CLI](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。 本文說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello 傳統部署模型。
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a>擷取資訊
您可以檢視您現有的 NSG、擷取現有 NSG 的規則，並找出與 NSG 相關聯的資源。

### <a name="view-existing-nsgs"></a>檢視現有的 NSG

tooview 所有現有 Nsg 中的訂閱，完成下列步驟的 hello:

1. 從瀏覽器，瀏覽 toohttp://portal.azure.com，並視需要登入您的 Azure 帳戶。

2. 按一下 [瀏覽] >  > [網路安全性群組]。

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. 請檢查在 hello Nsg hello 清單**網路安全性群組**刀鋒視窗。

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a>檢視資源群組中的 NSG

tooview hello Nsg 中的清單 hello **RG NSG**資源群組中，完成下列步驟的 hello:

1. 按一下 [資源群組] > **RG-NSG** > **...**。

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. 在 [hello] 清單中的資源，尋找項目顯示 hello NSG 圖示，hello 中所示**資源**刀鋒視窗的下方。

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a>列出 NSG 的所有規則

名為 NSG tooview hello 規則**NSG 前端**完整 hello 下列步驟：

1. 從 hello**網路安全性群組**刀鋒視窗中或使用 hello**資源**按一下刀鋒視窗中，如上所示**NSG 前端**。

2. 在 hello**設定**索引標籤上，按一下 **輸入安全性規則**。

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. hello**輸入安全性規則**刀鋒視窗會顯示如下所示。

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. 在 hello**設定**索引標籤上，按一下 **連出安全性規則**toosee hello 輸出規則。

    > [!NOTE]
    > tooview 預設規則，按一下 hello**預設規則**在 hello 顯示 hello 規則的 hello 刀鋒視窗最上方的圖示。
    >

### <a name="view-nsgs-associations"></a>檢視 NSG 關聯

tooview 哪些資源 hello **NSG 前端**NSG 是關聯、 完整 hello 下列步驟：

1. 從 hello**網路安全性群組**刀鋒視窗中或使用 hello**資源**按一下刀鋒視窗中，如上所示**NSG 前端**。

2. 在 hello**設定**索引標籤上，按一下 **子網路**tooview 哪個子網路相關聯 toohello NSG。

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. 在 hello**設定**索引標籤上，按一下 **網路介面**tooview 什麼 Nic 相關聯 toohello NSG。

## <a name="manage-rules"></a>管理規則
您可以加入現有的 NSG 規則 tooan、 編輯現有的規則和移除規則。

### <a name="add-a-rule"></a>新增規則
規則，允許 tooadd**輸入**流量 tooport **443**從任何機器 toohello **NSG 前端**NSG，完成下列步驟的 hello:

1. 從 hello**網路安全性群組**刀鋒視窗中或使用 hello**資源**按一下刀鋒視窗中，如上所示**NSG 前端**。
2. 在 hello**設定**索引標籤上，按一下 **輸入安全性規則**。
3. 在 hello**輸入安全性規則**刀鋒視窗中，按一下 **新增**。 然後，在 hello**新增連入的安全性規則**刀鋒視窗中，填入 hello 值，如下所示，然後按一下**確定**。

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    幾秒之後，請注意在 hello hello 新規則**輸入安全性規則**刀鋒視窗。

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a>變更規則
tooallow 上面所建立的 toochange hello 規則輸入流量從 hello**網際網路**唯一、 完整 hello 下列步驟：

1. 從 hello**網路安全性群組**刀鋒視窗中或使用 hello**資源**按一下刀鋒視窗中，如上所示**NSG 前端**。
2. 在 hello**設定**索引標籤上，按一下 hello 上面所建立的規則。
3. 在 hello**允許 https**刀鋒視窗中，變更 hello**來源**如下所示的屬性，然後按一下**儲存**。

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a>刪除規則

toodelete hello 規則建立上述的完整 hello 下列步驟：

1. 從 hello**網路安全性群組**刀鋒視窗中或使用 hello**資源**按一下刀鋒視窗中，如上所示**NSG 前端**。
2. 在 hello**設定**索引標籤上，按一下 hello 上面所建立的規則。
3. 在 hello**允許 https**刀鋒視窗中，按一下**刪除**，然後按一下**是**。

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a>管理關聯
您可以將關聯 NSG toosubnets 和 Nic。 您也可以中斷 NSG 與其相關聯的任何資源的關聯。

### <a name="associate-an-nsg-tooa-nic"></a>關聯 NSG tooa NIC
tooassociate hello **NSG 前端**NSG toohello **TestNICWeb1** NIC，完成下列步驟的 hello:

1. 從 hello**網路安全性群組**刀鋒視窗中或使用 hello**資源**按一下刀鋒視窗中，如上所示**NSG 前端**。
2. 在 hello**設定**索引標籤上，按一下 **網路介面** > **關聯** > **TestNICWeb1**。

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a>中斷 NSG 與 NIC 的關聯

toodissociate hello **NSG 前端**hello 從 NSG **TestNICWeb1** NIC，完成下列步驟的 hello:

1. 從 hello Azure 入口網站，按一下 **資源群組 >** > **RG NSG** > **...**  >  **TestNICWeb1**。

2. 在 hello **TestNICWeb1**刀鋒視窗中，按一下 **變更安全性...**  > **無**。

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> 您也可以使用現有的 NSG 此刀鋒視窗 tooassociate hello NIC tooany。
>

### <a name="dissociate-an-nsg-from-a-subnet"></a>中斷 NSG 與子網路的關聯

toodissociate hello **NSG 前端**hello 從 NSG**前端**子網路、 完整 hello 下列步驟：

1. 從 hello Azure 入口網站，按一下 **資源群組 >** > **RG NSG** > **...**  >  **TestVNet**。

2. 在 hello**設定**刀鋒視窗中，按一下 **子網路** > **前端** > **網路安全性群組** > **無**。

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. 在 hello**前端**刀鋒視窗中，按一下 **儲存**。

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a>NSG tooa 子網路建立關聯

tooassociate hello **NSG 前端**NSG toohello **FronEnd**一次的子網路，完成下列步驟的 hello:

1. 從 hello Azure 入口網站，按一下 **資源群組 >** > **RG NSG** > **...**  >  **TestVNet**。
2. 在 hello**設定**刀鋒視窗中，按一下 **子網路** > **前端** > **網路安全性群組** > **NSG 前端**。
3. 在 hello**前端**刀鋒視窗中，按一下 **儲存**。

> [!NOTE]
> 您也可以將關聯 NSG tooa thh NSG 的子網路**設定**刀鋒視窗。
>

## <a name="delete-an-nsg"></a>刪除 NSG
如果它不是相關聯 tooany 資源，您只能刪除 NSG。 toodelete NSG，完成下列步驟的 hello:。

1. 從 hello Azure 入口網站，按一下 **資源群組 >** > **RG NSG** > **...**  >  **NSG 前端**。
2. 在 hello**設定**刀鋒視窗中，按一下 **網路介面**。
3. 如果沒有列出任何 Nic，按一下 hello NIC，並遵循步驟 2 中的[中斷 NIC 的 NSG 關聯](#Dissociate-an-NSG-from-a-NIC)。
4. 針對每個 NIC 重複步驟 3。
5. 在 hello**設定**刀鋒視窗中，按一下 **子網路**。
6. 如果沒有列出任何子網路，請按一下 hello 子網路，請依照下列步驟 2 和 3 中的[中斷關聯子網路的 NSG](#Dissociate-an-NSG-from-a-subnet)。
7. 捲動左的 toohello **NSG 前端**刀鋒視窗中，然後按一下 **刪除** > **是**。

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a>後續步驟
* [啟用 NSG 的記錄](virtual-network-nsg-manage-log.md) 。
