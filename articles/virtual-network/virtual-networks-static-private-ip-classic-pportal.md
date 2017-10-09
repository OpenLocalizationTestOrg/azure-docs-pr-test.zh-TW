---
title: "aaaConfigure 私人 IP 位址的 Vm （傳統）-Azure 入口網站 |Microsoft 文件"
description: "了解如何 tooconfigure 私人 IP 位址的虛擬機器 （傳統） 使用 hello Azure 入口網站。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a>設定私人 IP 位址使用 hello Azure 入口網站為虛擬機器 （傳統）

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

本文涵蓋 hello 傳統部署模型。 您也可以[管理 hello Resource Manager 部署模型中的靜態私人 IP 位址](virtual-networks-static-private-ip-arm-pportal.md)。

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

下列的 hello 範例步驟預期簡單的環境中已經建立。 如果您想 toorun hello 步驟，因為它們會顯示在此文件，第一次建立 hello 測試環境中所述[建立 vnet](virtual-networks-create-vnet-classic-pportal.md)。

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>如何 toospecify 靜態私人 IP 位址建立 VM 時
名為的 VM toocreate *DNS01*在 hello*前端*名為 VNet 的子網路*TestVNet*以靜態私人 ip 位址的*192.168.1.101*，請遵循下列步驟執行 hello:

1. 從瀏覽器，瀏覽 toohttp://portal.azure.com，並視需要登入您的 Azure 帳戶。
2. 按一下**新增** > **計算** > **Windows Server 2012 R2 Datacenter**，請注意該 hello**選取部署模型**清單已經顯示**傳統**，然後按一下**建立**。
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. 在 hello**建立 VM**刀鋒視窗中，輸入建立 hello VM toobe hello 名稱 (*DNS01*在我們的案例)，hello 本機系統管理員帳戶和密碼。
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. 按一下 選擇性組態  >  網路  >  虛擬網路，然後按一下TestVNet。 如果**TestVNet**就無法使用，請確定您使用 hello*美國中部*位置，建立 hello hello 本文開頭所述的測試環境。
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. 在 hello**網路**刀鋒視窗中，目前未選取請確定 hello 子網路是*前端*，然後按一下  **IP 位址**下**IP 位址指派**按一下**靜態**，然後輸入*192.168.1.101*如**IP 位址**如下所示。
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. 按一下**確定**在 hello **IP 位址**刀鋒視窗中，然後按一下 **確定**在 hello**網路**刀鋒視窗中，然後按一下**確定**在 hello**選用設定**刀鋒視窗。
7. 在 hello**建立 VM**刀鋒視窗中，按一下 **建立**。 請注意 hello 磚下方顯示在儀表板。
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>如何 tooretrieve 靜態私人 IP 位址適用於 VM 的資訊
tooview hello 靜態私人 IP 位址資訊 hello 與 hello 上述步驟，在建立 VM 執行下列步驟 hello。

1. 從 hello Azure Azure 入口網站中，按一下 **瀏覽所有** > **虛擬機器 （傳統）** > **DNS01**  >  **所有設定** > **IP 位址**，並注意 hello IP 位址指派和 IP 位址，如下所示。
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>如何 tooremove 靜態私人 IP 位址從 VM
tooremove hello 靜態私人 IP 位址從 hello 以上版本，在建立 VM，請遵循下列 hello 步驟。

1. 從 hello **IP 位址**按一下刀鋒視窗中，如上所示**動態**toohello 右邊**IP 位址指派**，然後按一下**儲存**，然後按一下**是**。
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Tooadd 靜態私人 IP 定址 tooan 現有 VM 的方式
tooadd 靜態私人 IP 位址 toohello VM 建立使用 hello 上述步驟，請遵循下列 hello 步驟：

1. 從 hello **IP 位址**按一下刀鋒視窗中，如上所示**靜態**右邊 toohello **IP 位址指派**。
2. IP 位址 輸入 192.168.1.101，然後按一下儲存，再按一下 是。

## <a name="next-steps"></a>後續步驟
* 深入了解 [保留的公用 IP](virtual-networks-reserved-public-ip.md) 位址。
* 深入了解 [執行個體層級公用 IP (ILPIP)](virtual-networks-instance-level-public-ip.md) 位址。
* 請參閱 hello[保留 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)。

