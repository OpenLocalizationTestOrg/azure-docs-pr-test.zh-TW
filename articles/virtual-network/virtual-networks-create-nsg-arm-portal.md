---
title: "管理網路安全性群組 - Azure 入口網站 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站管理網路安全性群組。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: faee5ac8-f4c4-4f97-ade5-197a37aad496
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ecb4fb4608628f5a1bd54fac6af19fecfa4508f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-the-azure-portal"></a>使用 Azure 入口網站管理網路安全性群組

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

本文涵蓋之內容包括資源管理員部署模型。 您也可以 [在傳統部署模型中建立 NSG](virtual-networks-create-nsg-classic-ps.md)。

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

以下的範例 PowerShell 命令會預期已根據上述案例建立簡單的環境。 如果您想要以本文件顯示的方式執行命令，請先依照下列方式建置測試環境：部署[此範本](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd)，按一下 [部署至 Azure]，視情況取代預設參數值，然後遵循入口網站中的指示。 下列步驟使用 **RG-NSG** 作為部署範本之資源群組的名稱。

## <a name="create-the-nsg-frontend-nsg"></a>建立 NSG-FrontEnd NSG
若要根據上述案例建立 **NSG-FrontEnd** NSG，請遵循下列步驟執行。

1. 透過瀏覽器瀏覽至 http://portal.azure.com，並視需要使用您的 Azure 帳戶登入。
2. 按一下 [瀏覽] >  > [網路安全性群組]。
   
    ![Azure 入口網站 - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. 在 [網路安全性群組] 刀鋒視窗中，按一下 [新增]。
   
    ![Azure 入口網站 - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. 在 [建立網路安全性群組] 刀鋒視窗的 *RG-NSG* 資源群組中建立名為 *NSG-FrontEnd* 的 NSG，然後按一下 [建立]。
   
    ![Azure 入口網站 - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a>建立現有 NSG 中的規則
若要從 Azure 入口網站建立現有 NSG 中的規則，請遵循下列步驟執行。

1. 按一下 [瀏覽] >  > [網路安全性群組]。
2. 在 NSG 清單中按一下 [NSG-FrontEnd] **NSG-FrontEnd** > 
   
    ![Azure 入口網站 - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. 在 [輸入安全性規則] 清單中，按一下 [新增]。
   
    ![Azure 入口網站 - 新增規則](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. 在 [新增輸入安全性規則] 刀鋒視窗中，建立一個名為 web-rule 的規則，優先順序設為 [200]，以允許從任何來源經由 [TCP] 與連接埠 [80] 存取任何 VM，然後按一下 [確定]。 請注意，這些設定大部分已是預設值。
   
    ![Azure 入口網站 - 規則設定](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. 數秒後，您會看到 NSG 中的新規則。
   
    ![Azure 入口網站 - 新增規則](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. 重複步驟 6，建立名為 rdp-rule 的輸入規則，設定優先順序為 [250]，並允許透過 [TCP] 連接埠 [3389] 從任何來源存取任何 VM。

## <a name="associate-the-nsg-to-the-frontend-subnet"></a>建立 NSG 與 FrontEnd 子網路的關聯
1. 按一下 [瀏覽 >]  >  [資源群組]  >  [RG NSG]。
2. 在 [RG-NSG] 刀鋒視窗中，按一下 [...]  >  [TestVNet]。
   
    ![Azure 入口網站 - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. 在 [設定] 刀鋒視窗中，按一下 [子網路] > [FrontEnd] > [網路安全性群組] > [NSG-FrontEnd]。
   
    ![Azure 入口網站 - 子網路設定](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. 在 [FrontEnd] 刀鋒視窗中，按一下 [儲存]。
   
    ![Azure 入口網站 - 子網路設定](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-the-nsg-backend-nsg"></a>建立 NSG-BackEnd NSG
若要建立 **NSG-BackEnd** NSG 並將它與 **BackEnd** 子網路建立關聯，請遵循下列步驟。

1. 重複 [建立 NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) 中的步驟，建立名為 *NSG-BackEnd*
2. 重複 [在現有的 NSG 中建立規則](#Create-rules-in-an-existing-NSG) 中的步驟，建立下表中的 **輸入** 規則。
   
   | 輸入規則 | 輸出規則 |
   | --- | --- |
   | ![Azure 入口網站 - 輸入規則](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Azure 入口網站 - 輸出規則](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. 重複[建立 NSG 與 FrontEnd 子網路的關聯](#Associate-the-NSG-to-the-FrontEnd-subnet)中的步驟，建立 **NSG-Backend** NSG 與 **BackEnd** 子網路的關聯。

## <a name="next-steps"></a>後續步驟
* 了解如何 [管理現有的 NSG](virtual-network-manage-nsg-arm-portal.md)
* [啟用 NSG 的記錄](virtual-network-nsg-manage-log.md) 。

