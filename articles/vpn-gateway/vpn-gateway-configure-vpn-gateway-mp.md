---
title: "設定 VPN 閘道：傳統入口網站：Azure | Microsoft Docs"
description: "本文將逐步引導您設定虛擬網路 VPN 閘道，以及變更閘道 VPN 路由類型。 這些步驟適用於 toohello 傳統部署模型和 hello 傳統入口網站。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fbe59ba8-b11f-4d21-9bb1-225ec6c6d351
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/04/2017
ms.author: cherylmc
ms.openlocfilehash: 00d2fa18bab6eb24b33ddb18113f2a557db638d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vpn-gateway-in-hello-classic-portal"></a>在 hello 傳統入口網站中設定的 VPN 閘道 
如果您想 toocreate Azure 與內部部署位置之間的安全的跨單位連線，您會需要 toocreate 虛擬網路閘道。 VPN 閘道是一種特定類型的虛擬網路閘道。 在 hello 傳統部署模型中，VPN 閘道可以是下列其中一種 VPN 路由： 靜態或動態。 hello 您所選擇的 VPN 類型取決於您的網路設計計劃和您想要 toouse hello 在內部部署 VPN 裝置。 如需有關 VPN 裝置的詳細資訊，請參閱[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)。

**關於 Azure 部署模型**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-overview"></a>組態概觀
hello 下列步驟引導您完成設定您的 VPN 閘道 hello 傳統入口網站中。 這些步驟適用於 toogateways 使用 hello 傳統部署模型所建立的虛擬網路。 並非所有的 hello 閘道的組態設定是目前可用的 hello Azure 入口網站中。 如果是，我們將建立一組新的適用 toohello Azure 入口網站的指示。

### <a name="before-you-begin"></a>開始之前
設定閘道之前，您必須先 toocreate 虛擬網路。 步驟 toocreate 跨單位連線的虛擬網路，請參閱[使用站對站 VPN 連線設定虛擬網路](vpn-gateway-site-to-site-create.md)，或[使用點對站 VPN 連線設定虛擬網路](vpn-gateway-point-to-site-create.md). 接著，使用下列步驟 tooconfigure hello VPN 閘道的 hello 與收集 VPN 裝置需要 tooconfigure hello 資訊。 

如果您已經有 VPN 閘道，而您想 toochange hello VPN 路由類型，請參閱[toochange 如何 hello VPN 閘道的路由類型](#how-to-change-the-vpn-routing-type-for-your-gateway)。

## <a name="create-a-vpn-gateway"></a>建立 VPN 閘道
1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，hello 上**網路**頁面上，確認該 hello 狀態資料行，您的虛擬網路是**Created**。
2. 在 hello**名稱**資料行中，按一下 虛擬網路的 hello 名稱。
3. 在 hello**儀表板**頁面上，注意此 VNet 沒有閘道尚未設定。 當您瀏覽 hello 步驟 tooconfigure 您的閘道，您會看到此狀態。

![閘道未建立](./media/vpn-gateway-configure-vpn-gateway-mp/IC717025.png)

接下來，在 hello hello 頁面底部，按一下**建立閘道**。 您可以選取 [靜態路由] 或 [動態路由]。 hello 您所選取的 VPN 路由類型取決於幾項因素。 比方說，您的 VPN 裝置的支援，以及您是否需要 toosupport 點對站連線。 請檢查[關於 VPN 裝置的虛擬網路連線](vpn-gateway-about-vpn-devices.md)tooverify hello 您需要的 VPN 路由類型。 一旦建立 hello 閘道之後，您無法變更閘道刪除，並重新建立 hello 閘道 VPN 路由類型。 當 hello 系統提示您 tooconfirm hello 建立閘道，請按一下您想**是**。

![閘道 VPN 路由類型](./media/vpn-gateway-configure-vpn-gateway-mp/IC717026.png)

當建立閘道時，請注意 hello 閘道圖形在 hello 頁面上變更 tooyellow 顯示*建立閘道*。 它可能會佔用 too45 hello 閘道 toocreate 分鐘的時間。 等待 hello 閘道完成之前，您可以繼續進行其他組態設定。

![閘道正在建立](./media/vpn-gateway-configure-vpn-gateway-mp/IC717027.png)

當 hello 閘道的變更太*連接*，您可以收集所需的 VPN 裝置 hello 資訊。

![閘道正在連接](./media/vpn-gateway-configure-vpn-gateway-mp/IC717028.png)

## <a name="site-to-site-connections"></a>站對站連接

### <a name="step-1-gather-information-for-your-vpn-device-configuration"></a>步驟 1. 收集 VPN 裝置組態的資訊
如果您要建立站對站連線，建立 hello 閘道之後，收集 VPN 裝置組態的資訊。 這項資訊位於 hello**儀表板**頁面為您的虛擬網路：

1. **閘道 IP 位址-** hello IP 位址位於 hello**儀表板**頁面。 您必須能夠 toosee 它在您的閘道器之前已完成建立。
2. **共用索引鍵-**按一下**管理金鑰**在 hello 囉 」 畫面底部。 按一下 hello 圖示下一步 toohello 金鑰 toocopy 它 tooyour 剪貼簿，然後貼上並儲存 hello 金鑰。 此按鈕僅在有單一 S2S VPN 通道時才能正常運作。 如果您有多個 S2S VPN 通道，請使用 hello*取得虛擬網路閘道共用金鑰*API 或 PowerShell cmdlet。

![管理金鑰](./media/vpn-gateway-configure-vpn-gateway-mp/IC717029.png)

### <a name="step-2--configure-your-vpn-device"></a>步驟 2.  設定 VPN 裝置
站台對站連線 tooan 在內部部署網路需要 VPN 裝置。 雖然我們不提供的設定步驟適用於所有的 VPN 裝置，您可能會找到下列連結查看很有幫助的 hello hello 資訊：

- 如需有關相容的 VPN 裝置資訊，請參閱[ VPN 裝置](vpn-gateway-about-vpn-devices.md)。 
- 連結 toodevice 組態設定，請參閱[驗證 VPN 裝置](vpn-gateway-about-vpn-devices.md#devicetable)。 這些連結會以最佳方式來提供。 永遠是最佳 toocheck 與您的裝置製造商 hello 最新的組態資訊。
- 如需編輯裝置組態範例的相關資訊，請參閱[編輯範例](vpn-gateway-about-vpn-devices.md#editing)。
- 如需 IPsec/IKE 參數，請參閱[參數](vpn-gateway-about-vpn-devices.md#ipsec)。
- 然後再設定您的 VPN 裝置，請檢查任何[已知裝置相容性問題](vpn-gateway-about-vpn-devices.md#known)想 toouse hello VPN 裝置。

設定 VPN 裝置，當您需要下列項目 hello:

- hello 的虛擬網路閘道的公用 IP 位址。 您可以找到此移 toohello**概觀**刀鋒視窗中的虛擬網路。
- 共用金鑰。 這是共用相同 hello 建立您的站對站 VPN 連線時所指定的索引鍵。 在我們的範例中，我們會使用非常基本的共用金鑰。 您應該產生更複雜金鑰 toouse。

Hello VPN 裝置設定之後，您可以檢視更新的連接資訊在 hello 儀表板 頁面上您的 VNet。

### <a name="step-3-verify-your-local-network-ranges-and-vpn-gateway-ip-address"></a>步驟 3. 驗證您的區域網路範圍和 VPN 閘道 IP 位址
#### <a name="verify-your-vpn-gateway-ip-address"></a>驗證您的 VPN 閘道 IP 位址
為閘道 tooconnect 正常運作，hello VPN 裝置 IP 位址必須正確設定 hello 您為跨單位組態所指定的區域網路。 一般而言，這會設定 hello 站對站設定程序期間。 不過，如果您先前使用此區域網路搭配不同的裝置，或 hello IP 位址已變更為此區域網路，編輯 hello 設定 toospecify hello 正確的閘道 IP 位址。

1. tooverify 您閘道的 IP 位址，按一下 **網路**在 hello 入口網站左側的窗格，然後選取 **區域網路**hello 頁面頂端的 hello。 您會看到為您建立每個本機網路 hello VPN 閘道位址。 tooedit hello IP 位址，選取 hello VNet，然後按一下 **編輯**hello hello 頁底端。
2. 在 hello**指定本機網路詳細資料**頁面上，編輯 hello IP 位址，然後按一下hello 在 hello hello 頁面底部的下一步箭頭。
3. 在 hello**指定 hello 位址空間**頁面上，按一下您的設定上 hello 較低的右 toosave hello 核取記號。

#### <a name="verify-hello-address-ranges-for-your-local-networks"></a>請確認您的區域網路的 hello 位址範圍
Hello 正確流量 tooflow 透過 hello 閘道 tooyour 在內部部署位置，您必須確認已指定每個 IP 位址範圍的 tooverify。 每個範圍都必須列在您的 Azure「區域網路」  組態中。 根據您在內部部署位置的 hello 網路組態，這可以是一項大工程工作。 透過 hello 虛擬網路 VPN 閘道，就會傳送 hello 列出範圍內所包含的 IP 位址繫結的流量。 hello 範圍，您清單沒有 toobe 私人範圍，不過您會想在內部部署組態可接收 tooverify hello 輸入的流量。

tooadd 或編輯 hello 範圍的區域網路，使用下列步驟的 hello:

1. tooedit hello IP 位址範圍的區域網路中，按一下**網路**在 hello 入口網站左側的窗格，然後選取 **區域網路**hello 頁面頂端的 hello。 在 hello 入口網站，hello 最簡單方式 tooview hello 範圍所列位於 hello**編輯**頁面。 您的範圍，選取 hello VNet，然後按一下的 toosee**編輯**hello hello 頁底端。
2. 在 hello**指定本機網路詳細資料**頁面上，不進行任何變更。 按一下 hello 在 hello hello 頁面底部的 下一步箭號。
3. 在 hello**指定 hello 位址空間**頁面上，進行您的網路位址空間變更。 然後按一下 hello 核取記號 toosave 您的設定。

## <a name="how-tooview-gateway-traffic"></a>如何 tooview 閘道流量
您可以從虛擬網路 [ **儀表板** ] 頁面檢視您的閘道和閘道流量。

在 hello**儀表板**頁，您可以檢視下列 hello:

* hello 流經閘道，包括資料輸入和輸出資料的資料量。
* hello hello DNS 伺服器的名稱所指定的虛擬網路。
* hello 閘道與 VPN 裝置之間的連線。
* hello 的共用金鑰所使用的 tooconfigure 閘道連線 tooyour VPN 裝置。

## <a name="how-toochange-hello-vpn-routing-type-for-your-gateway"></a>如何 toochange hello VPN 閘道的路由類型
因為某些連線組態只適用於某些閘道路由類型，您可能會發現您需要 toochange hello 閘道 VPN 路由類型現有的 VPN 閘道。 例如，您可能想 tooadd 點對站連線能力 tooan 現有站台對站台具有連接是靜態閘道。 點對站連線需要動態閘道。 這表示 tooconfigure P2S 連線，您必須 toochange 從靜態 toodynamic 您閘道的 VPN 路由類型。

如果您需要 toochange 閘道的 VPN 路由類型，您將會刪除現有閘道 hello，並再建立新的閘道與 hello 新的路由類型。 您不需要 toodelete hello 整個虛擬網路 toochange hello 閘道路由類型。

在變更之前您閘道的 VPN 路由類型，是確定 tooverify VPN 裝置都支援您想 toouse hello 路由類型。 toodownload 新路由組態範例及檢查 VPN 裝置需求，請參閱[關於 VPN 裝置的虛擬網路連線](vpn-gateway-about-vpn-devices.md)。

> [!IMPORTANT]
> 當您刪除虛擬網路 VPN 閘道時，會釋放 hello 分派 toohello 閘道的 VIP。 當您重新建立 hello 閘道時，新的 VIP 會指派 tooit。
> 
> 

1. **刪除 hello 現有的 VPN 閘道。**
   
    在 hello**儀表板**虛擬網路的頁面上，瀏覽 toohello hello 頁面的底部，按一下 **刪除閘道**。 Hello 閘道的 hello 通知等候已被刪除。 一旦您收到您的閘道已刪除的 hello 通知囉 」 畫面上，您可以建立新的閘道。
2. **建立新的 VPN 閘道。**
   
    使用上方的 hello 頁面 toocreate 新的閘道 hello hello 程序：[建立 VPN 閘道](#create-a-vpn-gateway)。

## <a name="next-steps"></a>後續步驟
您可以將虛擬機器 tooyour 虛擬網路。 請參閱[如何自訂虛擬機器 toocreate](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

如果您想 tooconfigure 點對站 VPN 連線，請參閱[設定點對站 VPN 連線](vpn-gateway-point-to-site-create.md)。

