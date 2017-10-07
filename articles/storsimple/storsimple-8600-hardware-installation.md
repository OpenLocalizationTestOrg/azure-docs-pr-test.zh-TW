---
title: "aaaInstall Microsoft Azure StorSimple 8600 裝置 |Microsoft 文件"
description: "描述如何 toounpack，機架掛接，與您在部署及設定 hello 軟體之前，將 StorSimple 8600 裝置纜線連接。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3d82ba5f-3e34-40dc-9c33-50f952bc6be8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 10/24/2016
ms.author: alkohli
ms.openlocfilehash: 0fc0ddf076725fededdde33a260b950b72edc8db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="unpack-rack-mount-and-cable-your-storsimple-8600-device"></a>打開包裝、掛接機架和佈線 StorSimple 8600 裝置
## <a name="overview"></a>Overview
您的 Microsoft Azure StorSimple 8600 是雙重機箱裝置，包含主要及 EBOD 機箱。 本教學課程說明如何 toounpack、 利用機架掛接及纜線 hello StorSimple 8600 裝置的硬體設定 hello StorSimple 軟體。

## <a name="unpack-your-storsimple-8600-device"></a>打開您的 StorSimple 8600 裝置包裝
hello 下列步驟提供清楚、 詳細的指示 toounpack StorSimple 8600 儲存體裝置。 此裝置隨附於這兩個箱子，一個用於 hello 主要機箱，另一個用於 hello EBOD 機箱。 然後這兩個箱子會放在單一的箱子中。

### <a name="prepare-toounpack-your-device"></a>準備 toounpack 您的裝置
打開裝置包裝之前，請先檢閱下列資訊的 hello。

![警告圖示](./media/storsimple-safety/IC740879.png)![重量圖示](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **警告！**

1. 請確定您有兩個人員可用 toomanage hello hello 裝置的權數，如果您要以手動方式處理。 完全設定的機箱重量向上 too32 公斤 （70 磅）。
2. 放置在平坦的表面上的 hello 方塊。

接下來，完成下列步驟 toounpack hello 您的裝置。

#### <a name="toounpack-your-device"></a>toounpack 您的裝置
1. 檢查 hello 方塊和 hello 包裝發泡材料碎、 割傷、 漬或任何其他明顯損壞。 如果 hello 箱子或包裝嚴重損毀，請勿開啟 hello 方塊。 請[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)toohelp 您評估 hello 裝置是否正常運作。
2. 開啟 hello 外部方塊，然後取出 hello 對應 tooprimary 和 EBOD 機箱的兩個方塊。 您可以現在先解壓縮 hello 主要和 EBOD 機箱。 下列圖 hello 顯示 hello 機箱的其中一個 hello 解壓縮檢視。
   
    ![打開您的儲存體裝置包裝](./media/storsimple-8600-hardware-installation/HCSUnpackyour4Udevice.png)
   
    **儲存體裝置打開包裝的樣子**
   
   | 標籤 | 說明 |
   | --- | --- |
   |   1 |包裝箱 |
   |   2 |SAS 纜線 (在附件和纜線匣) |
   |   3 |底層發泡材料 |
   |   4 |裝置 |
   |   5 |頂層發泡材料 |
   |   6 |附件箱 |
3. 在打開 hello 兩個箱子之後, 請確定您有：
   
   * 1 個主要機箱 （hello 主要機箱和 EBOD 機箱是以兩個箱子中）
   * 1 個 EBOD 機箱
   * 4 條電源線，每個箱子各 2 條
   * 2 條 SAS 纜線 （tooconnect hello 主要機箱 tooEBOD 機箱）
   * 1 條轉接乙太網路纜線
   * 2 條序列主控台纜線
   * 1 個用於序列存取的序列-USB 轉換器
   * 4 個 QSFP-to-SFP+ 配接器以用於 10 GbE 網路介面
   * 2 個機架掛接套件 （4 的側軌個掛接硬體，hello 主要機箱和 EBOD 機箱各 2），每個方塊中的 1
   * 開始使用文件
     
     如果您未收到任何 hello 上面所列的項目[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。  

hello 下一個步驟為 toorack 掛接裝置。

## <a name="rack-mount-your-storsimple-8600-device"></a>機架掛接您的 StorSimple 8600 裝置
請遵循下一個步驟 tooinstall hello StorSimple 8600 存放裝置在有前後支柱的標準 19 吋機架中。 此裝置有兩個機箱：主要機箱和 EBOD 機箱。 這兩種需要 toobe 機架掛接。

hello 安裝包含多個步驟，其中每個 hello 下列程序中討論。

> [!IMPORTANT]
> StorSimple 裝置需要機架掛接才能正常運作。
> 
> 

### <a name="site-preparation"></a>場地準備
hello 機箱必須安裝在有前後支柱的標準 19 吋機架中。 使用下列程序 tooprepare 安裝機架 hello。

#### <a name="tooprepare-hello-site-for-rack-installation"></a>tooprepare hello 站台安裝機架
1. 請確定該 hello 主要和 EBOD 機箱都休止安全地置於平坦、 平穩和層級的工作介面 （或類似）。
2. 請確認該 hello 站台，您想設定 tooset 具有標準 AC 電源從到獨立來源或機架電源分配器 (PDU) 與不斷電供應系統 (UPS)。
3. 請確定該一個 4U (2 X 2U) 插槽 hello 想 toomount hello 機箱的機架上。

![警告圖示](./media/storsimple-safety/IC740879.png)![重量圖示](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **警告！**

 請確定您有兩個人員可用 toomanage hello 加權，當您以手動方式處理 hello 裝置設定。 完全設定的機箱重量向上 too32 公斤 （70 磅）。

### <a name="rack-prerequisites"></a>機架必要條件
hello 機箱的設計適合安裝在標準 19 吋機櫃中：

* 最小深度 27.84 吋機架張貼 toopost
* 最大重量 hello 裝置重 32 公斤
* 最大背部壓力為 5 Pascal (0.5 mm 水位表)

### <a name="rack-mounting-rail-kit"></a>機架掛接滑軌套件
會提供一組掛接滑軌 hello 19 吋機櫃搭配使用。 hello 滑軌已測試 toohandle hello 最大機箱重量。 這些滑軌也能夠安裝多個機箱而不會遺失 hello 機架內的空間。 第一次安裝 hello EBOD 機箱。

#### <a name="tooinstall-hello-ebod-enclosure-on-hello-rails"></a>tooinstall hello hello 搭配滑軌安裝在 EBOD 機箱
1. 只有在內部滑軌未安裝在您的裝置上時才執行此步驟。 一般而言，hello 內部滑軌安裝在 hello 工廠。 如果尚未安裝滑軌，安裝在 hello 左滑軌和右滑軌 toohello 兩側 hello 機箱的底座。 它們是在每一邊使用六個公制螺絲來連接。 方向，標示為投影片的 hello 滑軌 toohelp **LH – 前端**和**RH – 前端**，貼附朝向 hello hello 機箱背面的 hello 結束且錐形的結束。
   
    ![附加滑軌投影片 tooenclosure 底座](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoEnclosureChassis.png)
   
    **附加滑軌投影片 toohello hello 機箱的側邊**
   
   | 標籤 | 說明 |
   | --- | --- |
   |  1 |M 3x4 圓頭螺釘 |
   |  2 |底座滑軌 |
2. 附加 hello 左的滑軌和右滑軌組件 toohello 機櫃垂直桿。 標示 hello **LH**， **RH**，和**這一面朝**tooguide 您透過正確的方向。
3. 找出 hello 滑軌 pin 在 hello 正面和背面固定的 hello 滑軌組件。 擴充 hello 滑軌 toofit hello 機架支柱之間，並插入 hello post 前端和尾端機架支柱垂直成員漏洞 hello 的 pin。 請務必 hello 滑軌組件是層級。
4. 安全 hello 滑軌組件 toohello 機架 hello 顆公制螺絲的兩個使用垂直成員提供。 使用一個螺絲 hello 前面，而另一個在 hello 後方。
5. Hello 對其他滑軌組件重複上述步驟。
   
     ![附加滑軌投影片 toorack 封包](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoRackCabinet.png)
   
    **將滑軌組件 toohello 機架**
   
   | 標籤 | 說明 |
   | --- | --- |
   |   1 |固定螺絲 |
   |   2 |方孔前端機架柱螺絲 |
   |   3 |左邊前端滑軌位置插梢 |
   |   4 |固定螺絲 |
   |   5 |左邊後端滑軌位置插梢 |

### <a name="mounting-hello-ebod-enclosure-in-hello-rack"></a>Hello EBOD 機箱裝載於機架 hello
使用剛安裝的 hello 機架滑軌，執行下列步驟 toomount hello EBOD 機箱 hello 機架中的 hello。

#### <a name="toomount-hello-ebod-enclosure"></a>toomount hello EBOD 機箱
1. 小幫手，抬起 hello 機箱並將它與 hello 機架滑軌對齊。
2. 請仔細插入 hello 機箱 hello 滑軌中，然後再將其完全推入 hello 機架封包。
   
    ![將裝置插入機架 hello](./media/storsimple-8600-hardware-installation/HCSInsertingDeviceintheRack.png)
   
    **Hello 機箱裝載於機架 hello**
3. 移除 hello left 和左右前端螺帽提取 hello cap 可用。 hello 墊圈螺帽只需貼齊到 hello flanges。
4. 藉由安裝穿過每一個墊圈左邊和右邊的某個提供十字頭螺絲，到 hello 機架保護 hello 機箱。
5. 安裝 hello 墊圈螺帽它們進入位置，然後加以貼齊定位。
   
     ![安裝輪緣蓋](./media/storsimple-8600-hardware-installation/HCSInstallingFlangeCaps.png)
   
    **安裝 hello 墊圈螺帽**
   
   | 標籤 | 說明 |
   | --- | --- |
   |   1 |機箱鎖固螺絲 |

### <a name="mounting-hello-primary-enclosure-in-hello-rack"></a>Hello 主要機箱裝載於機架 hello
當您完成 hello EBOD 機箱裝載之後，您需要 toomount hello 主要機箱下列 hello 相同的步驟。

> [!NOTE]
> * 很可能 toohave hello 主要機箱與 hello EBOD 機箱之間的一些空的插槽中 hello 機架。
> * 使用提供的 hello 2 公尺 SAS 纜線 tooconnect hello 主要機箱 toohello EBOD 機箱。
> * 有 hello，音響 toohello EBOD 單位的 hello 相對位置沒有任何條件約束。 因此，hello 主要機箱可以放在 hello 上方插槽與下方的 hello EBOD 機箱，反之亦然。
> 
> 

hello 下一個步驟是 toocable 電源、 網路和序列存取您的裝置。

## <a name="cable-your-storsimple-8600-device"></a>佈線您的 StorSimple 8600 裝置
hello 下列程序說明如何 toocable StorSimple 8600 裝置的電源、 網路和序列連線。

### <a name="prerequisites"></a>必要條件
在開始 toocable 您的裝置之前，您必須：

* 您的主要機箱和 hello EBOD 機箱，完全解除封裝
* 4 條電源線 (2 個主要的 hello 與 hello EBOD 機箱) 隨附於您的裝置
* 2 條 SAS 纜線隨附 hello 裝置 tooconnect hello EBOD 機箱 toohello 主要機箱
* 存取 too2 電源分配單元 (Pdu) （建議選項）
* 網路纜線
* 提供的序列纜線
* 序列 USB 轉換器，並 hello 適當的驅動程式安裝在您的電腦上 （如有需要）
* 提供 4 個 QSFP-to-SFP+ 配接器以用於 10 GbE 網路介面
* [支援的硬體，在您的 StorSimple 裝置上的 hello 10 GbE 網路介面](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)

### <a name="sas-and-power-cabling"></a>SAS 及電源佈線
您的裝置同時有主要機箱和 EBOD 機箱。 這需要 hello 單位 toobe 接上一起取得序列連接 SCSI (SAS) 連線和電源。

設定此裝置 hello 第一次，請執行 hello 步驟 SAS 佈線第一次，然後完成 hello 電源佈線的步驟。

[!INCLUDE [storsimple-cable-8600-for-SAS](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

### <a name="network-cabling"></a>網路佈線
您的裝置已在使用中-待命組態： 在任何時候，一個控制器模組為主動，且處理所有磁碟和網路作業，而 hello 另一個控制器模組處於待命狀態。 如果控制器故障，就會發生，hello 待命控制器立即啟動，並繼續所有 hello 磁碟和網路作業。

toosupport 此備用控制器容錯移轉，您需要的 toocable 裝置網路 hello 步驟中所示。

#### <a name="toocable-for-network-connection"></a>toocable 網路連線
1. 您的裝置在每個控制器上有六個網路介面：四個 1 Gbps 和兩個 10 Gbps 乙太網路連接埠。 請參閱 toohello hello 裝置背板上遵循圖 tooidentify hello 資料連接埠。
   
     ![8600 裝置的後擋板](./media/storsimple-8600-hardware-installation/HCSBackplaneof2UDevicewithPortsLabeled.jpg)
   
    **顯示 hello 資料連接埠的裝置背面**
   
   | 標籤 | 說明 |
   | --- | --- |
   |   0,1,4,5 |1 GbE 網路介面 |
   |   2,3 |10 GbE 網路介面 |
   |   6 |序列連接埠 |
2. 請參閱下列的網路纜線圖表的 hello。 （藍色實線顯示 hello 最小網路組態。 對於高可用性和效能，需要的其他組態會以虛線顯示。)

![為您的 4U 裝置進行網路佈線](./media/storsimple-8600-hardware-installation/HCSCableYour4UDeviceforNetwork.png)

**您裝置的網路纜線**

| 標籤 | 說明 |
| --- | --- |
| A |具有網際網路存取的 LAN |
| B |控制器 0 |
| C |PCM 0 |
| D |控制器 1 |
| E |PCM 1 |
| F |EBOD 控制器 0 |
| G |EBOD 控制器 1 |
| H,I |主機 (例如，檔案伺服器) |
| 0-5 |網路介面 |
| 6 |主要機箱 |
| 7 |EBOD 機箱 |

當纜線連接 hello 裝置，需要 hello 最低設定：

* 各個控制器上至少已連接兩個網路介面，一個用於雲端存取，一個用於 iSCSI。 hello DATA 0 連接埠會自動啟用並設定透過 hello hello 裝置序列主控台。 除了 DATA 0，另一個資料連接埠也需要 toobe 透過 hello Azure 傳統入口網站設定。 在此情況下，連接的 DATA 0 連接埠 toohello 主要 LAN （可存取網際網路的網路）。 hello 連接埠可以是其他資料連接 tooSAN/iSCSI LAN (VLAN) 區段的 hello 網路，視預期的 hello 角色而定。
* 每個連接控制器 toohello 上的相同介面相同網路 tooensure 可用性，如果控制器容錯移轉發生。 比方說，如果您選擇 tooconnect DATA 0 和 DATA 3 的其中一個 hello 控制站，您需要對應上的 DATA 0 和 DATA 3 tooconnect hello hello 另一個控制器。

針對高可用性和效能，請記住：

* 可能的話，請在各個控制器上設定一組用於雲端存取 (1 GbE)，和另一組用於 iSCSI (建議 10 GbE) 的網路介面。
* 如果可能的話，連接的網路介面從開關故障針對每個控制器 tootwo 不同的交換器 tooensure 可用性。 hello 圖說明 hello 兩個 10 GbE 網路介面、 DATA 2 和 DATA 3，從每個連接控制器 tootwo 不同的交換器。 如需詳細資訊，請參閱 toohello**網路介面**下 hello [StorSimple 裝置的高可用性需求](storsimple-system-requirements.md#high-availability-requirements-for-storsimple)。

> [!NOTE]
> 如果您 10 GbE 網路介面使用 SFP + 收發器，使用 hello 提供 QSFP-SFP + 介面卡。 如需詳細資訊，請移至太[支援 hello 10 GbE 網路介面上您的 StorSimple 裝置的硬體](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)。
> 
> 

### <a name="serial-port-cabling"></a>序列連接埠佈線
執行下列步驟 toocable hello 序列連接埠。

#### <a name="toocable-for-serial-connection"></a>連接序列 toocable
1. 您的裝置在每個控制器上有以扳手圖示識別的序列連接埠。 toolocate hello 序列通訊埠，請參閱 toohello 圖，顯示您的裝置背面的 hello hello 資料連接埠。
2. 識別您的裝置背板上的 hello 主動控制站。 閃爍藍色 LED 表示該 hello 控制器為作用中。
3. 使用提供的 hello 序列纜線 （如有需要您的膝上型電腦的 hello USB 序列轉換器），並將主控台或電腦連接 （使用終端機模擬 toohello 裝置） toohello hello 作用中控制器的序列通訊埠。
4. 在電腦上安裝 hello 序列 USB 驅動程式 （隨附於 hello 裝置）。
5. 設定 hello 序列連線如下：
   
   * 115,200 傳輸速率
   * 8 資料位元
   * 1 停止位元
   * 無同位檢查
   * 流程控制設定得**無**
6. 確認 hello 連線藉由按下 Enter hello 主控台上的運作。 序列主控台功能表應該會出現。

> [!NOTE]
> **熄燈管理：** hello 裝置是安裝在遠端資料中心或限制存取的電腦機房，確保 hello 序列連線 tooboth 控制站都已連線的 tooa 序列主控台開關或類似設備。 如此可以在網路中斷或非預期失敗時允許頻外遠端控制和支援作業。
> 
> 

完成纜線連接裝置的電源、 網路存取權，而且在序列 connection.hello 下一個步驟是 tooconfigure hello 軟體在您的裝置上。

## <a name="next-steps"></a>後續步驟
現在您已經準備就緒太[部署和設定內部部署 StorSimple 裝置](storsimple-deployment-walkthrough-u2.md)。

