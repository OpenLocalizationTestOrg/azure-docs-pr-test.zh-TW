---
title: "aaaModify hello StorSimple 8000 系列裝置設定 |Microsoft 文件"
description: "描述如何 toouse 會 hello StorSimple 裝置管理員服務 tooreconfigure 已經部署 StorSimple 裝置。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 79711b45eafe732c1eed1e562b05e3837fbc9d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomodify-your-storsimple-device-configuration"></a>使用 hello StorSimple 裝置管理員服務 toomodify StorSimple 裝置的組態

## <a name="overview"></a>概觀

hello Azure 入口網站**裝置設定**> 一節中 hello**設定**刀鋒視窗包含您可以重新設定 StorSimple 裝置管理員管理 StorSimple 裝置的所有 hello 裝置參數服務。 本教學課程說明如何使用 hello**設定**刀鋒視窗 tooperform hello 下列裝置層級工作：

* 修改裝置的易記名稱
* 修改裝置的時間設定
* 指派次要 DNS
* 修改網路介面
* 交換或重新指派 IP

## <a name="modify-device-friendly-name"></a>修改裝置的易記名稱

您可以使用 hello Azure 入口網站 toochange hello 裝置名稱，並將它指派您所選擇的唯一易記名稱。 使用 hello**一般設定**刀鋒視窗上您裝置 toomodify hello 裝置的易記名稱。 hello 易記名稱可以包含任何字元，最多可有 64 個字元。

> [!NOTE] 
> Hello 裝置安裝程式完成之前，您只能修改 hello hello Azure 入口網站中的裝置名稱。 Hello 最低裝置設定完成之後，您無法變更 hello 裝置名稱。

![[一般設定] 中的裝置名稱](./media/storsimple-8000-modify-device-config/modify-general-settings3.png)

連接的 toohello StorSimple 裝置管理員服務的 StorSimple 裝置會指派預設名稱。 hello 預設名稱通常會反映 hello 裝置 hello 序號。 例如，預設的裝置名稱是 15 個字元，例如 8600-SHX0991003G44HT 表示 hello 下列：

* **8600** – 指出 hello 裝置模型。
* **SHX** – 指出 hello 製造站台。
* **0991003** – 表示特定產品。
* **G44HT**-hello 最後 5 位數會遞增的 toocreate 唯一序號。 這可能不是連續的組合。

## <a name="modify-device-description"></a>修改裝置描述

使用 hello**一般設定**裝置 toomodify hello 裝置描述上的刀鋒視窗。

![[一般設定] 中的裝置描述](./media/storsimple-8000-modify-device-config/modify-general-settings4.png)

裝置描述通常有助於識別 hello 擁有者和 hello 裝置 hello 實體位置。 hello 描述欄位必須包含少於 256 個字元。

## <a name="modify-time-settings"></a>修改時間設定

您的裝置必須同步時間順序 tooauthenticate 與雲端儲存體服務提供者。 使用 hello**一般設定**上您的裝置 toomodify hello 裝置時間設定 刀鋒視窗。

![[一般設定] 中的裝置描述](./media/storsimple-8000-modify-device-config/modify-general-settings2.png)

 從 hello 下拉式清單中選取您的時區。 您可以指定 tootwo 網路時間通訊協定 (NTP) 伺服器：

 - **主要 NTP 伺服器**-hello 組態需要，指定當您使用 Windows PowerShell for StorSimple tooconfigure 您的裝置。 您可以指定 hello 預設的 Windows Server **time.windows.com**為 NTP 伺服器。 您可以檢視 hello 主要 NTP 伺服器組態透過 hello Azure 入口網站，但您必須使用 hello Windows PowerShell 介面 toochange 它。 使用 hello `Set-HcsNTPClientServerAddress` cmdlet toomodify hello 主要 NTP 伺服器的裝置。 如需詳細資訊，請移 toosynxtax [Set-hcsntpclientserveraddress] (https://technet.microsoft.com/library/dn688138.aspx) cmdlet。

- **次要 NTP 伺服器**-hello 組態是選擇性的。 您可以使用 hello 入口 tooconfigure 次要 NTP 伺服器。

設定 hello NTP 伺服器時，請確定您的網路，允許從您的資料中心 toohello 網際網路 hello NTP 流量 toopass。 指定公用 NTP 伺服器時，您必須確定網路防火牆和其他安全性裝置會設定的 tooallow NTP 流量從網路外部的 hello 的 tootravel tooand。 若不允許雙向 NTP 流量，您必須使用內部 NTP 伺服器 (Windows 網域控制器會提供這個函式)。 如果您的裝置無法同步處理時間，它可能無法使用您的雲端存放裝置提供者無法 toocommunicate。

toosee 公用 NTP 伺服器清單，移 toohello [NTP 伺服器的 Web](http://support.ntp.org/bin/view/Servers/WebHome)。

### <a name="what-happens-if-hello-device-is-deployed-in-a-different-time-zone"></a>如果 hello 裝置部署在不同的時區會怎樣？

如果 hello 裝置部署在不同的時區，將會變更裝置時區 hello。 假設所有 hello 備份原則都使用 hello 裝置時區，hello 備份原則會自動調整根據新時區 hello。 不需使用者介入。

## <a name="modify-dns-settings"></a>修改 DNS 設定

您的裝置嘗試 toocommunicate 與雲端儲存體服務提供者時，會使用 DNS 伺服器。 使用 hello**網路設定**上裝置 tooview 刀鋒視窗，以及修改 hello 設定 DNS 設定。 

![[網路設定] 中的 DNS 設定](./media/storsimple-8000-modify-device-config/modify-network-settings1.png)

高可用性，您需要的 tooconfigure 這兩個主要的 hello 而且 hello 初始裝置部署期間 hello 次要 DNS 伺服器。

**主要 DNS 伺服器**-您使用 hello Windows PowerShell for StorSimple toofirst hello 初始設定期間指定 hello 主要 DNS 伺服器。 您可以重新設定 hello 主要 DNS 伺服器僅透過 hello Windows PowerShell 介面。 使用 hello `Set-HcsDNSClientServerAddress` cmdlet toomodify hello 主要 DNS 伺服器的裝置。 如需詳細資訊，請移 toosynxtax [Set-hcsdnsclientserveraddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet。

**次要 DNS 伺服器**-toomodify hello 次要 DNS 伺服器，使用 hello `Set-HcsDNSClientServerAddress` hello 裝置 hello Windows PowerShell 介面中的 cmdlet 或**網路設定**刀鋒視窗中的 hello Azure 在 StorSimple 裝置入口網站。

toomodify hello 次要 DNS 伺服器在 Azure 入口網站執行下列步驟的 hello。

1. 移 tooyour StorSimple 裝置管理員服務。 從 hello 的裝置清單，選取，然後按一下您的裝置。

2. 在 hello**設定**刀鋒視窗中，跳過**裝置設定 > 網路**。 這會開啟 hello**網路設定**刀鋒視窗。 按一下 [DNS 設定] 圖格。 修改 hello 次要 DNS 伺服器 IP 位址。

    ![修改次要 DNS 伺服器 IP 位址](./media/storsimple-8000-modify-device-config/modify-secondary-dns1.png)

4. 在 hello 命令列中，按一下**儲存**時提示您進行確認，請按一下 **確定**。

    ![儲存並確認變更](./media/storsimple-8000-modify-device-config/modify-secondary-dns-2.png)



## <a name="modify-network-interfaces"></a>修改網路介面

您的裝置具有六個裝置網路介面，其中四個是 1 GbE，而其中兩個是 10 Gbe。 這些介面都會標示為 DATA 0 至 DATA 5。 DATA 0、DATA 1、DATA 4 和 DATA 5 是 1 GbE，而 DATA 2 和 DATA 3 是 10 GbE 網路介面。

使用 hello**網路設定**刀鋒視窗 tooconfigure 每個的 hello 介面 toobe 使用。

![透過 [網路設定] 設定網路介面](./media/storsimple-8000-modify-device-config/modify-network-settings3.png)

tooensure 高可用性，建議您的裝置上有兩個以上的 iSCSI 介面和兩個具備雲端功能的介面。 我們建議停用未使用的介面，但並非必要。

每個網路介面，會顯示 hello 下列參數：

* **速度** – 並非使用者可設定的參數。 DATA 0、DATA 1、DATA 4 和 DATA 5 永遠是 1 GbE，而 DATA 2 和 DATA 3 是 10 GbE 介面。
  
  > [!NOTE]
  > 速度和雙工會一律自動交涉。 不支援 Jumbo 框架。
  
* **介面狀態** – 介面可以啟用或停用。 如果啟用，hello 裝置會嘗試 toouse hello 介面。 我們建議您啟用連接的 toohello 網路和使用這些介面。 停用任何您沒有使用的介面。
* **介面型別**– 此參數可讓您 tooisolate iSCSI 流量與雲端儲存體流量。 這個參數可以是 hello 下列其中一種：
  
  * **啟用雲端**– hello 裝置啟用時，將使用此介面 toocommunicate 與 hello 雲端。
  * **具備 iSCSI 功能**– hello 裝置啟用時，將使用此介面 toocommunicate 與 hello iSCSI 主機。
    
    我們建議您隔離 iSCSI 流量與雲端儲存空間流量。 也請注意是否主機是 hello 內相同的子網路與裝置，您不需要 tooassign 閘道;不過，如果您的主機位於不同的子網路與您的裝置，您將需要 tooassign 閘道。
* **IP 位址**– 當您設定任何的 hello 網路介面卡，您必須設定虛擬 IP (VIP)。 這可以是 IPv4 或 IPv6 或同時使用。 Hello 裝置網路介面支援 hello IPv4 和 IPv6 位址系列。 當您使用 IPv4 時，請以小數點十進位表示法指定 32 位元的 IP 位址 (*xxx.xxx.xxx.xxx*)。 當您使用 IPv6 時，僅需提供 4 位數前置詞，而裝置網路介面的 128 位元位址將會根據該前置詞自動產生。
* **子網路**– 這是指 toohello 子網路遮罩，並已透過 hello Windows PowerShell 介面設定。
* **閘道**– 這是它會試著 toocommunicate hello 內的節點時應使用此介面的 hello 預設閘道相同的 IP 位址空間 （子網路）。 hello 預設閘道必須是在 hello 相同位址空間 （子網路） 作為 hello 介面 IP 位址，由 hello 子網路遮罩。
* **固定 IP 位址**-這個欄位可供使用，只有當您設定 hello DATA 0 時，介面。 更新或疑難排解 hello 裝置等作業，您可能需要 tooconnect 直接 toohello 裝置控制站。 hello 固定 IP 位址可以是使用的 tooaccess 作用中的 hello 和您的裝置上的 hello 被動控制器。

> [!NOTE]
> * tooensure 正常運作，請確認 hello 介面速度和雙工 hello 參數，每個裝置介面連線到。 交換器介面應該針對乙太網路 (1000 Mbps) 進行交涉或設定，且為全雙工。 介面以較低速度運作或為半雙工時將導致效能問題。
> * toominimize 中斷與停機時間，我們建議您啟用 portfast hello 交換器連接埠的 hello iSCSI 網路介面，您的裝置會連接到的每個。 這可確保網路連線可以快速建立的容錯移轉的 hello 事件中。

### <a name="configure-data-0"></a>設定 DATA 0

DATA 0 依預設已啟用雲端功能。 在設定 DATA 0 時，您也是必要的 tooconfigure 兩個固定的 IP 位址，一個用於每個控制站。 這些固定 IP 位址可以是使用的 tooaccess hello 裝置控制站直接與您 hello 裝置，或當您存取 hello 用途疑難排解的 hello 控制站上安裝更新時很有用。

您可以重新設定 hello 固定 IP 透過 hello 資料 0 設定 刀鋒視窗的控制站。

![設定網路介面 - DATA 0](./media/storsimple-8000-modify-device-config/modify-network-settings2.png)

> [!NOTE]
> hello 固定 hello 控制站的 IP 位址可用來服務 hello 更新 toohello 裝置。 因此，hello 固定 Ip 必須可路由傳送，而且要能 tooconnect toohello 網際網路。

### <a name="configure-data-1---data-5"></a>設定 DATA 1 - DATA 5

資料 1-DATA 5 網路介面，您可以設定所有 hello 網路 hello 下列螢幕擷取畫面所示：

![設定網路介面 DATA 1 - DATA 5](./media/storsimple-8000-modify-device-config/modify-network-settings4.png)


## <a name="swap-or-reassign-ips"></a>交換或重新指派 IP

目前，若有任何網路介面上 hello 控制器會指派 VIP 給使用中 (由 hello 同一部裝置或 hello 網路中的另一個裝置)，然後 hello 控制器將會容錯移轉。 如果您交換或重新指派裝置網路介面的 VIP 時，必須遵循適當的程序，否則可能會建立重複的 IP。

執行下列步驟 tooswap hello 或重新指派任何 hello 網路介面的 hello Vip:

#### <a name="tooreassign-ips"></a>tooreassign Ip

1. 清除 hello 這兩個介面的 IP 位址。
2. 清除 hello IP 位址之後，指派 toohello 個別介面 hello 新的 IP 位址。

## <a name="next-steps"></a>後續步驟

* 了解如何太[為您的 StorSimple 裝置設定 MPIO](storsimple-8000-configure-mpio-windows-server.md)。
* 了解如何太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。

