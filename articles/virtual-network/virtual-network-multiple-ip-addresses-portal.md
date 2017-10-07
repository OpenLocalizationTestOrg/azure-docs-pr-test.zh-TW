---
title: "Azure 虛擬機器-入口網站的 aaaMultiple IP 位址 |Microsoft 文件"
description: "了解如何 tooassign 多個 IP 位址 tooa 虛擬機器使用 hello Azure 入口網站 |資源管理員。"
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 3a8cae97-3bed-430d-91b3-274696d91e34
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/30/2016
ms.author: annahar
ms.openlocfilehash: 34075766ac68c8de38c258a4d70e35881f28bb0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-portal"></a>指派多個 IP 位址 toovirtual 使用，在電腦 hello Azure 入口網站

>[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]
>
本文說明如何透過 hello Azure Resource Manager 部署模型使用的虛擬機器 (VM) toocreate hello Azure 入口網站。 Tooresources 透過 hello 傳統部署模型所建立，無法指派多個 IP 位址。 深入了解 Azure 的部署模型，讀取 hello toolearn[了解部署模型](../resource-manager-deployment-model.md)發行項。

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>建立有多個 IP 位址的 VM

如果您想 toocreate 具有多個 IP 位址或靜態私人 IP 位址的 VM，您必須建立使用 PowerShell 或 hello Azure CLI。 如何按一下 hello PowerShell 或 CLI 選項在此發行項 toolearn hello 最上方。 您可以使用單一動態私人 IP 位址，以及 （選擇性） 單一公用 IP 位址使用 hello 入口網站中 hello 的 hello 步驟來建立 VM[建立 Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md)或[建立 Linux VM](../virtual-machines/linux/quick-create-portal.md)文件。 建立 hello VM 之後，您可以從動態 toostatic 變更 hello IP 位址類型，並加入其他 IP 位址使用 hello 中的下列步驟 hello 網站[新增 IP 位址 tooa VM](#add)本文一節。

## <a name="add"></a>新增 IP 位址 tooa VM

您可以藉由完成 hello 遵照的步驟，新增私人和公用 IP 位址 tooa NIC。 hello hello 下列各節中的範例假設您已經有含 hello 三 hello 中所述的 IP 組態的 VM[案例](#Scenario)在此文件，但它不需要您執行。

### <a name="coreadd"></a>核心步驟

1. 如有必要，請到其中，瀏 toohello 在 https://portal.azure.com 並登入 Azure 入口網站。
2. 在 hello 入口網站中，按一下 **更多服務**> 類型*虛擬機器*在 hello 篩選 方塊中，然後按一下**虛擬機器**。
3. 在 hello**虛擬機器**刀鋒視窗中，按一下的 hello VM 想 tooadd IP 位址。 按一下**網路介面**中出現，hello 虛擬機器刀鋒視窗，然後再選取 hello 網路介面想 tooadd hello IP 位址。 在 hello 範例所示 hello 遵循圖片，hello NIC 名為*myNIC* hello 名為 VM 從*myVM*選取：

    ![網路介面](./media/virtual-network-multiple-ip-addresses-portal/figure1.png)

4. 在 hello 刀鋒視窗中出現的 hello 您選取的 NIC，按一下  **IP 組態**。

完整的 hello hello 以下各節的其中一個步驟，您想 tooadd 根據 hello 類型的 IP 位址。

### <a name="add-a-private-ip-address"></a>**新增私人 IP 位址**

完成下列步驟 tooadd 新的私用 IP 位址的 hello:

1. 完整的 hello 步驟 hello[核心步驟](#coreadd)本文一節。
2. 按一下 [新增] 。 在 hello**新增 IP 組態**刀鋒視窗中，建立名為 IP 設定*IPConfig 4*與*10.0.0.7*為*靜態*私人 IP 位址，然後按一下 **確定**。

    > [!NOTE]
    > 時新增靜態 IP 位址，您必須上 hello 子網路 hello NIC 連線到指定的未使用且有效地址。 如果您選取的 hello 位址無法使用，hello 入口網站會顯示 X 代表 hello IP 位址，而您會需要 tooselect 另一部。

3. 一旦您按一下 [確定]，hello 刀鋒視窗會關閉，而您會看到 hello 列出新 IP 組態。 按一下**確定**tooclose hello**新增 IP 組態**刀鋒視窗。
4. 您可以按一下**新增**tooadd 額外的 IP 設定，或關閉所有開啟刀鋒視窗 toofinish 新增 IP 位址。
5. 新增 hello 私人 IP 位址 toohello VM 作業系統 hello hello 作業系統的步驟，以[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。

### <a name="add-a-public-ip-address"></a>新增公用 IP 位址

公用 IP 位址是由新的 IP 設定或現有的 IP 組態關聯公用 IP 位址資源 tooeither 加入。

> [!NOTE]
> 公用 IP 位址需要少許費用。 進一步瞭解 IP 位址定價，toolearn 讀取 hello [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses)頁面。 沒有可用的訂用帳戶中的公用 IP 位址限制 toohello 數目。 深入了解 hello 限制、 讀取 hello toolearn [Azure 限制](../azure-subscription-service-limits.md#networking-limits)發行項。
> 

### <a name="create-public-ip"></a>建立公用 IP 位址資源

公用 IP 位址是公用 IP 位址資源的其中一項設定 如果您有不是您想要的目前關聯的 tooan IP 設定公用 IP 位址資源 tooassociate tooan IP 設定，就會略過下列步驟的 hello，並視需要完成 hello 以下各節，其中的 hello 步驟。 如果您沒有可用的公用 IP 位址資源，請完成下列其中一個步驟 toocreate hello:

1. 如有必要，請到其中，瀏 toohello 在 https://portal.azure.com 並登入 Azure 入口網站。
3. 在 hello 入口網站中，按一下 **新增** > **網路** > **公用 IP 位址**。
4. 在 hello**建立公用 IP 位址**刀鋒視窗中，輸入**名稱**，選取**IP 位址指派**型別，**訂用帳戶**、**資源群組**，和**位置**，然後按一下 **建立**hello 下列圖片所示：

    ![建立公用 IP 位址資源](./media/virtual-network-multiple-ip-addresses-portal/figure5.png)

5. 完整的 hello 中 hello 以下各節 tooassociate hello 公用 IP 位址資源 tooan IP 組態的其中一個步驟。

#### <a name="associate-hello-public-ip-address-resource-tooa-new-ip-configuration"></a>關聯的 hello 公用 IP 位址資源 tooa 新的 IP 設定

1. 完整的 hello 步驟 hello[核心步驟](#coreadd)本文一節。
2. 按一下 [新增] 。 在 hello**新增 IP 組態**刀鋒視窗中，建立名為 IP 設定*IPConfig 4*。 啟用 hello**公用 IP 位址**選取現有的可用公用 IP 位址資源從 hello**選擇公用 IP 位址**刀鋒視窗中出現。

    一旦您已選取 hello 公用 IP 位址資源，請按一下**確定**hello 刀鋒視窗會關閉。 如果您沒有現有的公用 IP 位址，您可以建立一個 hello hello 中的步驟，以[建立公用 IP 位址資源](#create-public-ip)本文一節。 

3. 檢閱 hello 新的 IP 設定。 即使未明確指派私人 IP 位址，其中一個已自動指派 toohello IP 組態，因為所有的 IP 設定必須具有私人 IP 位址。
4. 您可以按一下**新增**tooadd 額外的 IP 設定，或關閉所有開啟刀鋒視窗 toofinish 新增 IP 位址。
5. 完成您的作業系統中 hello hello 步驟新增 hello 私用 IP 位址 toohello VM 作業系統[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。 請勿將 hello 公用 IP 位址 toohello 作業系統。

#### <a name="associate-hello-public-ip-address-resource-tooan-existing-ip-configuration"></a>關聯的 hello 公用 IP 位址資源 tooan 現有 IP 組態

1. 完整的 hello 步驟 hello[核心步驟](#coreadd)本文一節。
2. 按一下 您希望 tooadd hello 公用 IP 位址資源的 hello IP 組態。
3. 在 hello IPConfig 刀鋒視窗中顯示，按一下  **IP 位址**。
4. 在 hello**選擇公用 IP 位址**刀鋒視窗中，選取的公用 IP 位址。
5. 按一下**儲存**hello 刀鋒視窗會關閉。 如果您沒有現有的公用 IP 位址，您可以建立一個 hello hello 中的步驟，以[建立公用 IP 位址資源](#create-public-ip)本文一節。
3. 檢閱 hello 新的 IP 設定。
4. 您可以按一下**新增**tooadd 額外的 IP 設定，或關閉所有開啟刀鋒視窗 toofinish 新增 IP 位址。 請勿將 hello 公用 IP 位址 toohello 作業系統。


[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
