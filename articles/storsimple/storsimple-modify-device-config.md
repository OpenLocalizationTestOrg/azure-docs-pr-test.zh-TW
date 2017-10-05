---
title: "修改 StorSimple 裝置組態 | Microsoft Docs"
description: "描述如何使用 StorSimple Manager 服務來重新設定已部署的 StorSimple 裝置。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: bb679264-8d46-429c-9ef7-630dc3b4a423
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: v-sharos
ms.openlocfilehash: 5bfbeb038dbedae2bf77016abbc19458c3dc22c9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-manager-service-to-modify-your-storsimple-device-configuration"></a>使用 StorSimple Manager 服務來修改 StorSimple 裝置組態。
## <a name="overview"></a>概觀
Azure 傳統入口網站 [設定]  頁面包含所有裝置參數，可讓您重新設定 StorSimple Manager 服務所管理的 StorSimple 裝置。 本教學課程說明如何使用 [設定] 頁面來執行下列的裝置層級工作：

* 修改裝置設定 
* 修改時間設定 
* 修改 DNS 設定 
* 修改網路介面
* 交換或重新指派 IP

## <a name="modify-device-settings"></a>修改裝置設定
裝置設定包括裝置和裝置描述的易記名稱。

> [!NOTE] 
> 您無法修改 Azure 傳統入口網站中的裝置名稱。 不支援重新命名裝置。

系統會為連線到 StorSimple Manager 服務的 StorSimple 裝置指派預設名稱。 預設名稱通常會反映裝置的序號。 例如，長度為 15 個字元的預設裝置名稱，如 8600-SHX0991003G44HT，將表示以下項目：

* **8600** – 表示裝置型號。
* **SHX** – 表示製造場所。
* **0991003** – 表示特定產品。
* **G44HT**– 最後 5 位數會以遞增方式來建立唯一的序號。 這可能不是連續的組合。

您可以指定裝置描述。 裝置描述通常有助於識別擁有者和裝置的實體位置。 [描述] 欄位不得超過 256 個字元。

## <a name="modify-time-settings"></a>修改時間設定
您的裝置必須同步時間才能驗證雲端儲存空間服務提供者。 從下拉式清單選取您的時區，並指定最多兩個網路時間通訊協定 (NTP) 伺服器。 當您使用 Windows PowerShell for StorSimple 來設定您的裝置時，需要指定主要 NTP 伺服器。 您可以指定預設 Windows Server **time.windows.com** 作為 NTP 伺服器。 您可以透過 Azure 傳統入口網站來檢視主要 NTP 伺服器組態，但是您必須使用 Windows PowerShell 介面來進行變更。

次要 NTP 伺服器組態為選擇性。 您可以使用傳統入口網站來設定次要 NTP 伺服器。 

設定 NTP 伺服器時，請確定您的網路允許 NTP 流量從您的資料中心通過網際網路。 指定公用 NTP 伺服器時，您必須確定網路防火牆和其他安全性裝置皆設定為允許 NTP 流量傳入及傳出外部網路。 若不允許雙向 NTP 流量，您必須使用內部 NTP 伺服器 (Windows 網域控制器會提供這個函式)。 如果您的裝置無法同步時間，它可能無法與您的雲端儲存空間提供者進行通訊。

若要查看公用 NTP 伺服器清單，請移至 [NTP 伺服器網頁](http://support.ntp.org/bin/view/Servers/WebHome)。 

### <a name="what-happens-if-the-device-is-deployed-in-a-different-time-zone"></a>如果裝置部署在不同的時區會發生什麼狀況？
如果裝置部署在不同的時區，系統將會變更裝置的時區。 假設所有備份原則皆使用裝置時區，則備份原則會根據新的時區自動調整。 不需使用者介入。

## <a name="modify-dns-settings"></a>修改 DNS 設定
當您的裝置嘗試與雲端儲存空間服務提供者通訊時，系統會使用 DNS 伺服器。 如需高可用性，您必須在初始裝置部署期間設定主要和次要 DNS 伺服器。 若要重新設定主要 DNS 伺服器，您必須在 StorSimple 裝置上使用 Windows PowerShell 介面。

若要修改次要 DNS 伺服器，您可以使用 Azure 傳統入口網站。

## <a name="modify-network-interfaces"></a>修改網路介面
您的裝置具有六個裝置網路介面，其中四個是 1 GbE，而其中兩個是 10 Gbe。 這些介面都會標示為 DATA 0 至 DATA 5。 DATA 0、DATA 1、DATA 4 和 DATA 5 是 1 GbE，而 DATA 2 和 DATA 3 是 10 GbE 網路介面。

針對每個要使用的介面設定 [ **網路介面設定** ]。 若要確保高可用性，建議您的裝置上至少具有兩個 iSCSI 介面以及兩個已啟用雲端功能的介面。 我們建議停用未使用的介面，但並非必要。

當您設定任何網路介面時，您必須設定虛擬 IP (VIP)。

DATA 0 依預設已啟用雲端功能。 設定 DATA 0 時，您也需要設定兩個固定 IP 位址，每個控制器使用一個。 這些固定的 IP 位址可以用來直接存取裝置控制器，且當您在裝置上安裝更新或存取控制器以進行疑難排解時很有用。

在 StorSimple 8000 Series Update 1 中，DATA 0 的路由計量會設定為最低；因此，如果您的裝置正在執行 StorSimple 8000 Series Update 1，則所有雲端流量將透過 DATA 0 進行路由傳送。 如果您有多個已啟用雲端功能的網路介面位於 StorSimple 裝置上，請記下這一點。

> [!NOTE]
> 控制器的固定 IP 位址用來為裝置更新提供服務。 因此，固定 IP 必須可路由傳送且能夠連線到網際網路。
> 
> 

對於每個網路介面，系統會顯示下列參數：

* **速度** – 並非使用者可設定的參數。 DATA 0、DATA 1、DATA 4 和 DATA 5 永遠是 1 GbE，而 DATA 2 和 DATA 3 是 10 GbE 介面。
  
  > [!NOTE]
  > 速度和雙工會一律自動交涉。 不支援 Jumbo 框架。
  > 
  > 
* **介面狀態** – 介面可以啟用或停用。 如果已啟用，則裝置會嘗試使用介面。 我們建議您僅啟用那些連線到網路的使用中介面。 停用任何您沒有使用的介面。
* **介面類型** – 此參數可讓您隔離 iSCSI 流量和雲端儲存空間流量。 此參數可以是下列其中一項：
  
  * **啟用雲端** – 啟用時，裝置將使用此介面與雲端通訊。
  * **啟用 iSCSI** – 啟用時，裝置將使用此介面與 iSCSI 主機通訊。
    
    我們建議您隔離 iSCSI 流量與雲端儲存空間流量。 也請注意如果您的主機位於裝置所在的相同子網路內，您不需要指派閘道器；不過，如果您的主機位於與裝置不同的子網路，您將必須指派一個閘道器。
* **IP 位址** – 這可以是 IPv4 或 IPv6 或同時使用。 IPv4 和 IPv6 位址系列皆支援裝置網路介面。 當您使用 IPv4 時，請以小數點十進位表示法指定 32 位元的 IP 位址 (*xxx.xxx.xxx.xxx*)。 當您使用 IPv6 時，僅需提供 4 位數前置詞，而裝置網路介面的 128 位元位址將會根據該前置詞自動產生。
* **子網路** – 這是指子網路遮罩，且透過 Windows PowerShell 介面設定。
* **閘道器** – 這是在嘗試與位於不同 IP 位址空間 (子網路) 內的節點通訊時此介面應該使用的預設閘道器。 預設閘道器必須位於相同的位址空間 (子網路)，如同介面 IP 位址，且取決於子網路遮罩。
* **固定 IP 位址** – 僅當您設定 DATA 0 介面時才能使用此欄位。 對於更新或疑難排解裝置等作業，您可能需要直接連線到裝置控制器。 固定 IP 位址可用來存取裝置上的主動和被動控制器。

您可以透過 Azure 傳統入口網站重新設定控制器 0 及控制器 1。

> [!NOTE]
> * 若要確保適當的操作，請確認每個裝置介面所連線到交換器上的介面速度和雙工。 交換器介面應該針對乙太網路 (1000 Mbps) 進行交涉或設定，且為全雙工。 介面以較低速度運作或為半雙工時將導致效能問題。
> * 若要將中斷與停機時間降到最低，建議您針對裝置的 iSCSI 網路介面將會連接到的每個交換器連接埠上啟用 portfast。 如此可確保網路連線可以在發生容錯移轉時快速建立。
> 
> 

## <a name="swap-or-reassign-ips"></a>交換或重新指派 IP
目前，如果控制器上的任何網路介面已指派使用中的 VIP (由相同裝置或網路中的另一個裝置)，則控制器會進行容錯移轉。 因此，如果您針對裝置網路介面交換 VIP，則必須遵循適當的程序，因為您將建立重複的 IP 情況。

執行下列步驟來交換或重新指派任何網路介面的 VIP：

#### <a name="to-reassign-ips"></a>重新指派 IP
1. 清除兩個介面的 IP 位址。
2. 清除 IP 位址之後，指派新的 IP 位址給個別的介面。

## <a name="next-steps"></a>後續步驟
* 了解如何 [為 StorSimple 裝置設定 MPIO](storsimple-configure-mpio-windows-server.md)。
* 了解如何 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。

