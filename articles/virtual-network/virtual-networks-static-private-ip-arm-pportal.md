---
title: "對於 Azure 入口網站的 Vm-aaaConfigure 私人 IP 位址 |Microsoft 文件"
description: "了解如何 tooconfigure 私人 IP 位址的虛擬機器使用 hello Azure 入口網站。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a>設定使用 hello Azure 入口網站為虛擬機器的私人 IP 位址

> [!div class="op_single_selector"]
> * [Azure 入口網站](virtual-networks-static-private-ip-arm-pportal.md)
> * [PowerShell](virtual-networks-static-private-ip-arm-ps.md)
> * [Azure CLI](virtual-networks-static-private-ip-arm-cli.md)
> * [Azure 入口網站 (傳統)](virtual-networks-static-private-ip-classic-pportal.md)
> * [PowerShell (傳統)](virtual-networks-static-private-ip-classic-ps.md)
> * [Azure CLI (傳統)](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

本文涵蓋 hello Resource Manager 部署模型。 您也可以[管理 hello 傳統部署模型中的靜態私人 IP 位址](virtual-networks-static-private-ip-classic-pportal.md)。

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

下列的 hello 範例步驟預期簡單的環境中已經建立。 如果您想 toorun hello 步驟，因為它們會顯示在此文件，第一次建立 hello 測試環境中所述[建立 vnet](virtual-networks-create-vnet-arm-pportal.md)。

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a>如何 toocreate VM 進行測試靜態私人 IP 位址
您無法使用 hello Azure 入口網站，hello hello Resource Manager 部署模式中的 VM 建立期間設定靜態私人 IP 位址。 您必須先建立 hello VM，轉設定其私人 IP toobe 靜態。

名為的 VM toocreate *DNS01*在 hello*前端*名為 VNet 的子網路*TestVNet*，依照下列步驟執行 hello。

1. 從瀏覽器，瀏覽 toohttp://portal.azure.com，並視需要登入您的 Azure 帳戶。
2. 按一下**新增** > **計算** > **Windows Server 2012 R2 Datacenter**，請注意該 hello**選取部署模型**清單已經顯示**資源管理員**，然後按一下**建立**、 hello 圖所示。
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. 在 hello**基本概念**刀鋒視窗中，輸入 hello VM toobe 建立 hello 名稱 (*DNS01*在我們的案例)，hello 本機系統管理員帳戶和密碼，如 hello 圖所示。
   
    ![基本概念刀鋒視窗](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. 請確定 hello**位置**選取*美國中部*，然後按一下**選取現有**下**資源群組**，然後按一下 **資源群組**一次，然後按一下 *TestRG*，然後按一下**確定**。
   
    ![基本概念刀鋒視窗](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. 在 hello**大小選擇 「**刀鋒視窗中，選取**標準 A1**，然後按一下**選取**。
   
    ![選擇尺寸刀鋒視窗](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. 在**設定**刀鋒視窗中，請確定 hello 下列屬性會設定下面的 hello 值設定，然後按一下**確定**。
   
    -**儲存體帳戶**：vnetstorage
   
   * **網路**：TestVNet
   * **子網路**：FrontEnd
     
     ![選擇尺寸刀鋒視窗](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. 在 hello**摘要**刀鋒視窗中，按一下 **確定**。 請注意 hello 磚下方顯示在儀表板。
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>如何 tooretrieve 靜態私人 IP 位址適用於 VM 的資訊
tooview hello 靜態私人 IP 位址資訊 hello 與 hello 上述步驟，在建立 VM 執行下列步驟 hello。

1. 從 hello Azure Azure 入口網站中，按一下 **瀏覽所有** > **虛擬機器** > **DNS01** > **所有設定** > **網路介面**，然後按一下hello 列出只有網路介面上。
   
    ![部署 VM 磚](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. 在 hello**網路介面**刀鋒視窗中，按一下**所有設定** > **IP 位址**和注意事項 hello**指派**和**IP 位址**值。
   
    ![部署 VM 磚](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Tooadd 靜態私人 IP 定址 tooan 現有 VM 的方式
tooadd 靜態私人 IP 位址 toohello VM 建立使用 hello 上述步驟，請遵循下列 hello 步驟：

1. 從 hello **IP 位址**按一下刀鋒視窗中，如上所示**靜態**下**指派**。
2. IP 位址 輸入 192.168.1.101，然後按一下儲存。
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> 如果按一下後的**儲存**您注意到 hello 分派仍然可以設定太**動態**，這表示您輸入的 hello IP 位址已在使用。 請嘗試不同的 IP 位址。
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>如何 tooremove 靜態私人 IP 位址從 VM
tooremove hello 靜態私人 IP 位址從 VM 建立上述的 hello 完成下列步驟的 hello:

從 hello **IP 位址**按一下刀鋒視窗中，如上所示**動態**下**指派**，然後按一下**儲存**。

## <a name="next-steps"></a>後續步驟
* 深入了解 [保留的公用 IP](virtual-networks-reserved-public-ip.md) 位址。
* 深入了解 [執行個體層級公用 IP (ILPIP)](virtual-networks-instance-level-public-ip.md) 位址。
* 請參閱 hello[保留 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)。

