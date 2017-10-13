---
title: "設定連接至 StorSimple Virtual Array 之主機上的 MPIO | Microsoft Docs"
description: "說明如何針對與執行 Windows Server 2012 R2 的主機連接的 StorSimple Virtual Array 設定多重路徑 I/O (MPIO)。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5b7a7f99-ee5b-4b7d-ab32-483a5a1fa504
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/01/2017
ms.author: alkohli
ms.openlocfilehash: c75c6ed40754aee964e2b68f4f569dc1422507f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-multipath-io-on-windows-server-host-for-the-storsimple-virtual-array"></a>在 Windows Server 主機上設定 StorSimple Virtual Array 的多重路徑 I/O
## <a name="overview"></a>概觀
本文說明如何在 Windows Server 主機上安裝多重路徑 I/O 功能 (MPIO)，套用僅限 StorSimple 磁碟區的特定組態設定，然後確認 StorSimple 磁碟區的 MPIO。 此程序假設具有兩個網路介面的 StorSimple 1200 Virtual Array 連接至具有兩個網路介面的 Windows Server 主機。 本文中所包含的資訊僅適用於虛擬陣列。 如需 StorSimple 8000 系列裝置的資訊，請移至 [設定 StorSimple 主機的 MPIO](storsimple-configure-mpio-windows-server.md)。 

Windows Server 中的 MPIO 功能可協助建置高可用性、容錯的儲存體組態。 MPIO 使用備援實體路徑元件 — 配接器、纜線以及交換器 — 以在伺服器與存放裝置之間建立邏輯路徑。 如果元件故障而導致邏輯路徑失敗，多重路徑邏輯使用替代的 I/O 路徑，讓應用程式仍然可以存取其資料。 此外，依照您的設定，MPIO 也能藉由重新平衡所有路徑的負載來改善效能。 如需詳細資訊，請參閱 [MPIO 概觀](https://technet.microsoft.com/library/cc725907.aspx "MPIO 概觀 and features")。

為了讓 StorSimple 解決方案發揮高可用性，請在連接至 StorSimple Virtual Array (型號 1200) 的 Windows Server 主機上設定 MPIO。 主機伺服器隨即可容許連結、網路或介面失敗。 

您必須依照下列步驟設定 MPIO： 

* 組態必要條件
* 步驟 1：在 Windows Server 主機上安裝 MPIO
* 步驟 2：為 StorSimple 磁碟區設定 MPIO 
* 步驟 3：在主機上掛接 StorSimple 磁碟區

上述步驟會在下列各節討論。

## <a name="prerequisites"></a>必要條件
本節將詳細說明 Windows Server 主機和虛擬陣列的組態必要條件。

### <a name="on-windows-server-host"></a>在 Windows Server 主機上
* 確定 Windows Server 主機已啟用 2 個網路介面。

### <a name="on-storsimple-virtual-array"></a>在 StorSimple Virtual Array 上
* 虛擬陣列應該設定為 iSCSI 伺服器。 若要深入了解，請參閱[將虛擬陣列設定為 iSCSI 伺服器](storsimple-virtual-array-deploy3-iscsi-setup.md)。 應該在陣列上啟用一或多個網路介面。   
* 虛擬陣列上的網路介面應該可從 Windows Server 主機觸達。
* 應該在 StorSimple Virtual Array 上建立一或多個磁碟區。 若要深入了解，請參閱在 StorSimple Virtual Array 上[新增磁碟區](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume)。 在此程序中，我們在虛擬陣列上建立 3 個磁碟區 (1 個固定在本機的磁碟區，2 個階層式磁碟區，如下所示)。
  
    ![mpio0](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio0.png)

### <a name="hardware-configuration-for-storsimple-virtual-array"></a>StorSimple Virtual Array 的硬體設定
下圖顯示讓此程序中使用的 Windows Server 主機和 StorSimple Virtual Array 達到高可用性和平衡負載多重路徑的硬體設定。

![mpio 硬體組態](./media/storsimple-virtual-array-configure-mpio-windows-server/1200hardwareconfig.png)

如上圖所示：

* 在 Hyper-V 上佈建的 StorSimple Virtual Array 是設定為 iSCSI 伺服器的單一節點作用中裝置。
* 陣列上已啟用兩個虛擬網路介面。 在虛擬陣列的本機 Web UI 中，瀏覽至 [網路設定] 來確認已啟用兩個網路介面，如下所示︰
  
    ![在 1200 上啟用的網路介面](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio9.png)
  
    請記下啟用之網路介面 (乙太網路，預設為乙太網路 2) 的 IPv4 位址，並加以儲存供稍後在主機上使用。
* Windows Server 主機已啟用 2 個網路介面。 如果主機和陣列的連接介面位於相同的子網路上，將會有 4 個路徑可用。 在此程序中是這個情況。 不過，如果陣列和主機介面上的每個網路介面位於不同的 IP 子網路上 (且不可路由傳送)，則只有 2 個路徑可用。

## <a name="step-1-install-mpio-on-the-windows-server-host"></a>步驟 1：在 Windows Server 主機上安裝 MPIO
MPIO 是 Windows 伺服器預設不會安裝的選擇性功能。 您應該透過伺服器管理員將它安裝為功能。 若要在 Windows Server 主機上安裝這項功能，請完成下列程序。

[!INCLUDE [storsimple-install-mpio-windows-server-host](../../includes/storsimple-install-mpio-windows-server-host.md)]

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>步驟 2：為 StorSimple 磁碟區設定 MPIO 
您必須設定 MPIO 才能識別 StorSimple 磁碟區。 若要設定 MPIO 以辨識 StorSimple 磁碟區，請執行下列步驟。

[!INCLUDE [storsimple-configure-mpio-volumes](../../includes/storsimple-configure-mpio-volumes.md)]

## <a name="step-3-mount-storsimple-volumes-on-the-host"></a>步驟 3：在主機上掛接 StorSimple 磁碟區
在 Windows 伺服器上設定 MPIO 之後，就能掛接在 StorSimple 陣列上建立的磁碟區，並可以利用 MPIO 獲得備援。 若要掛接磁碟區，請執行下列步驟。

#### <a name="to-mount-volumes-on-the-host"></a>若要在主機上掛接磁碟區
1. 在 Windows Server 主機上，開啟 [iSCSI 啟動器內容]  視窗。 移至 [伺服器管理員] > [儀表板] > [工具] > [iSCSI 啟動器]。
2. 在 [iSCSI 啟動器 - 內容] 對話方塊中，按一下 [探索]，然後按一下 [搜尋目標入口]。
3. 在 [搜尋目標入口]  對話方塊中，執行下列動作：
   
    1. 輸入 StorSimple Virtual Array 上第一個啟用的網路介面的 IP 位址。 根據預設，這會是 **乙太網路**。 
    2. 按一下 [確定] 以返回 [iSCSI 啟動器內容] 對話方塊。
     
    > [!IMPORTANT]
    > 如果您使用私人網路進行 iSCSI 連線，請輸入連線到私人網路的 DATA 連接埠 IP 位址。
     
4. 在陣列上針對第二個網路介面 (例如，乙太網路 2) 重複步驟 2-3 。 
5. 在 [iSCSI 啟動器內容] 對話方塊中，選取 [目標] 索引標籤。 針對虛擬陣列，您應該將每個磁碟區表面視為**探索到的目標**之下的目標。 在此情況下，會發現三個目標 (對應到三個磁碟區)。
   
    ![mpio1](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio1.png)
6. 按一下 [連接]，與您的 StorSimple Virtual Array 建立 iSCSI 工作階段。 [連線到目標]  對話方塊隨即出現。 選取 [啟用多重路徑]  核取方塊。 按一下 [進階] 。
   
    ![mpio2](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio2.png)
7. 在 [進階設定]  對話方塊中，執行下列動作：                                        
   
    1. 在 [本機介面卡] 下拉式清單中，選取 [Microsoft iSCSI 啟動器]。
    2. 在 [啟動器 IP]  下拉式清單中，選取主機的 IP 位址。
    3. 在 [目標入口 IP]  下拉式清單中，選取陣列介面的 IP。
    4. 按一下 [確定] 以返回 [iSCSI 啟動器內容] 對話方塊。
     
        ![mpio3](./media/storsimple-ova-configure-mpio-windows-server/mpio3.png)

8. 按一下 [內容] 。 
   
    ![mpio4](./media/storsimple-ova-configure-mpio-windows-server/mpio4.png)

9. 在 [內容] 對話方塊中，按一下 [新增工作階段]。
   
   ![mpio5](./media/storsimple-ova-configure-mpio-windows-server/mpio5.png)
10. 在 [連線到目標] 對話方塊中，選取 [啟用多重路徑] 核取方塊。 按一下 [進階] 。
11. 在 [進階設定]  對話方塊中：                                        
    
    1. 在 [本機介面卡]  下拉式清單中，選取 [Microsoft iSCSI 啟動器]。

    2. 在 [啟動器 IP]  下拉式清單中，選取對應到主機的 IP 位址。 在此情況下，您會將陣列上的兩個網路介面連線到主機上的單一網路介面。 因此，這個介面會和第一個工作階段提供的相同。

    3. 在 [目標入口 IP]  下拉式清單中，為陣列上啟用的第二個資料介面選取 IP 位址。

    4. 按一下 [確定]  以返回 [iSCSI 啟動器內容] 對話方塊。 您完成將第二個工作階段新增到目標。
      
       ![mpio11](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio11.png)
    
    5. 在新增所需的工作階段 (路徑) 之後，請在 [iSCSI 啟動器內容] 對話方塊中，選取目標，然後按一下 [內容]。 在 [內容]  對話方塊的 [工作階段] 索引標籤中，針對可能的路徑排列組合記下其對應的四個工作階段識別碼。 若要取消工作階段，請選取工作階段識別碼旁邊的核取方塊，然後按一下 [中斷連線] 。

    6. 若要檢視工作階段內顯示的裝置，請選取 [裝置]  索引標籤。 若要為選取的裝置設定 MPIO 原則，請按一下 [MPIO] 。

    7. [詳細資料] 對話方塊隨即顯示。 在 [MPIO] 索引標籤上，您可以選取適當 [負載平衡原則] 設定。 您也可以檢視 [使用中] 或 [待命] 路徑類型。
12. 重複步驟 8-11，將其他工作階段 (路徑) 新增到目標。 主機上有兩個介面且虛擬陣列上也有兩個，您總共可以為每個目標新增四個工作階段。 
    
    ![mpio14](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio14.png)
13. 您必須為每個磁碟區重複這些步驟 (表面做為目標)。
    
    ![mpio15](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio15.png)
14. 藉由瀏覽至 [伺服器管理員] > [儀表板] > [電腦管理]，來開啟 [電腦管理]。 在左窗格中，按一下 [存放裝置] > [磁碟管理]。 在 StorSimple Virtual Array 上建立且可讓此主機看見的磁碟區，在 [磁碟管理] 下會顯示為新磁碟。
15. 初始化磁碟，並建立新的磁碟區。 在格式化程序期間，選取 64 KB 的配置單位大小 (AUS)。 對所有可用的磁碟區重複此程序。
    
    ![磁碟管理](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio20.png)
16. 在 [磁碟管理] 下，於 [磁碟] 按一下滑鼠右鍵，然後選取 [內容]。
17. 在 [多重路徑磁碟裝置內容] 對話方塊中，按一下 [MPIO] 索引標籤。
    
    ![磁碟屬性](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio21.png)
18. 在 [DSM 名稱] 區段中，按一下 [詳細資料] 並確認參數已設定為預設參數。 預設參數如下：
    
    * 路徑確認期間 = 30
    * 重試計數 = 3
    * PDO 移除期間 = 20
    * 重試間隔 = 1
    * 啟用路徑確認 = 未選取。
    
    > [!NOTE]
    > **請不要修改預設的參數。**
   
## <a name="next-steps"></a>後續步驟
深入了解[使用 StorSimple 裝置管理員服務管理 StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md)。

