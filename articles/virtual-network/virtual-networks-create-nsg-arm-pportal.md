---
title: "aaaCreate 網路安全性群組-Azure 入口網站 |Microsoft 文件"
description: "深入了解如何 toocreate 及部署使用 hello Azure 入口網站的網路安全性群組。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5bc8fc2e-1e81-40e2-8231-0484cd5605cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74ecc7db06bb69f2041aa64d7b38b63eb379a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-portal"></a>建立網路安全性群組使用 hello Azure 入口網站

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

本文涵蓋 hello Resource Manager 部署模型。 您也可以[hello 傳統部署模型中建立 Nsg](virtual-networks-create-nsg-classic-ps.md)。

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

hello 範例 PowerShell 預期簡單的環境中已經建立下列命令會根據上面的 hello 案例。 如果您想 toorun hello 命令，因為它們會顯示在此文件，第一次建立 hello 測試環境部署[此範本](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd)，按一下 **部署 tooAzure**，取代 hello 預設參數值如果有必要，並遵循中的 hello 指示 hello 入口網站。 使用以下步驟 hello **RG NSG** hello hello 資源群組 hello 範本名稱已部署至。

## <a name="create-hello-nsg-frontend-nsg"></a>建立 hello NSG 前端 NSG
toocreate hello **NSG 前端**NSG 示 hello 案例以上版本，請遵循下列 hello 步驟。

1. 從瀏覽器，瀏覽 toohttp://portal.azure.com，並視需要登入您的 Azure 帳戶。
2. 按一下 [瀏覽] >  > [網路安全性群組]。
   
    ![Azure 入口網站 - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. 在 hello**網路安全性群組**刀鋒視窗中，按一下 **新增**。
   
    ![Azure 入口網站 - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. 在 hello**建立網路安全性群組**刀鋒視窗中，建立名為 NSG *NSG 前端*hello 中*RG NSG*資源群組，然後再按一下**建立**.
   
    ![Azure 入口網站 - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a>建立現有 NSG 中的規則
toocreate hello Azure 入口網站，從現有 NSG 中的規則，請遵循下列 hello 步驟。

1. 按一下 [瀏覽] >  > [網路安全性群組]。
2. 在 hello Nsg 清單中按一下**NSG 前端** > **輸入安全性規則**
   
    ![Azure 入口網站 - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. 中的 hello 清單**輸入安全性規則**，按一下 **新增**。
   
    ![Azure 入口網站 - 新增規則](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. 在 hello**新增連入的安全性規則**刀鋒視窗中，建立名為的規則*網頁規則*優先順序為*200*允許存取透過*TCP* tooport*80* tooany VM 從任何來源，然後按一下**確定**。 請注意，這些設定大部分已是預設值。
   
    ![Azure 入口網站 - 規則設定](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. 幾秒之後，您會看見 hello hello NSG 中的新規則。
   
    ![Azure 入口網站 - 新增規則](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. 重複步驟 too6 toocreate 名為的輸入的規則*rdp 規則*優先順序為*250*允許存取透過*TCP* tooport *3389*tooany 從任何來源的 VM。

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a>Hello NSG toohello 前端子網路建立關聯
1. 按一下 [瀏覽 >]  >  [資源群組]  >  [RG NSG]。
2. 在 hello **RG NSG**刀鋒視窗中，按一下  **...**  >  **TestVNet**。
   
    ![Azure 入口網站 - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. 在 hello**設定**刀鋒視窗中，按一下 **子網路** > **前端** > **網路安全性群組** > **NSG 前端**。
   
    ![Azure 入口網站 - 子網路設定](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. 在 hello**前端**刀鋒視窗中，按一下 **儲存**。
   
    ![Azure 入口網站 - 子網路設定](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a>建立 hello NSG 後端 NSG
toocreate hello **NSG 後端**NSG，並將它關聯 toohello**後端**子網路，後續 hello 步驟。

1. 中的步驟重複 hello[建立 hello NSG 前端 NSG](#Create-the-NSG-FrontEnd-NSG) toocreate NSG 名為*NSG 後端*
2. 中的步驟重複 hello[建立現有 NSG 中的規則](#Create-rules-in-an-existing-NSG)toocreate hello**輸入**hello 表中的規則。
   
   | 輸入規則 | 輸出規則 |
   | --- | --- |
   | ![Azure 入口網站 - 輸入規則](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Azure 入口網站 - 輸出規則](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. 中的步驟重複 hello [hello NSG toohello 前端子網路建立關聯](#Associate-the-NSG-to-the-FrontEnd-subnet)tooassociate hello **NSG 後端**NSG toohello**後端**子網路。

## <a name="next-steps"></a>後續步驟
* 了解如何太[管理現有的 Nsg](virtual-network-manage-nsg-arm-portal.md)
* [啟用 NSG 的記錄](virtual-network-nsg-manage-log.md) 。

