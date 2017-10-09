---
title: "主機上的 aaaConfigure MPIO 連接 tooStorSimple 虛擬陣列 |Microsoft 文件"
description: "描述如何 tooconfigure 多重路徑 I/O (MPIO) 為您的 StorSimple Virtual Array 連接 tooa 主機執行 Windows Server 2012 R2。"
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
ms.openlocfilehash: 0e6df23bba29395329685cbf2c968675abb04cfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-on-windows-server-host-for-hello-storsimple-virtual-array"></a>Hello StorSimple Virtual Array 的 Windows Server 主機上設定多重路徑 I/O
## <a name="overview"></a>概觀
本文說明如何在您的 Windows Server 主機上的 tooinstall 多重路徑 I/O 功能 (MPIO) 套用特定的組態設定，僅限 StorSimple 磁碟區，然後確認 MPIO StorSimple 磁碟區。 hello 程序假設您的 StorSimple 1200 虛擬陣列，具有兩個網路介面是兩個網路介面連接的 tooa Windows Server 主機。 本文中所包含的 hello 資訊適用於 toohello 虛擬陣列。 如需 StorSimple 8000 系列裝置的資訊，請移太[設定 MPIO StorSimple 主機](storsimple-configure-mpio-windows-server.md)。 

在 Windows Server 可協助建置高可用性、 容錯儲存體設定中的 hello MPIO 功能。 MPIO 使用備援實體路徑元件，配接器、 纜線和交換器 — toocreate hello 伺服器與 hello 存放裝置之間的邏輯路徑。 如果沒有元件故障，造成邏輯路徑 toofail，則多重路徑邏輯會使用替代路徑 i/o，讓應用程式仍然可以存取其資料。 此外根據您的設定 MPIO 也可以改善效能的重新平衡所有這些路徑中的 hello 負載。 如需詳細資訊，請參閱 [MPIO 概觀](https://technet.microsoft.com/library/cc725907.aspx "MPIO 概觀 and features")。

Hello 高可用性的 StorSimple 解決方案，請在 hello Windows Server 主機已連線 tooyour StorSimple Virtual Array （模型 1200年） 上設定 MPIO。 hello 主機伺服器時，然後可容許連結、 網路或介面失效。 

您將需要這些步驟 tooconfigure MPIO toofollow: 

* 組態必要條件
* 步驟 1： 安裝 MPIO hello Windows Server 主機上
* 步驟 2：為 StorSimple 磁碟區設定 MPIO 
* 步驟 3: Hello 主機上的掛接 StorSimple 磁碟區

Hello 下列各節討論 hello 上述步驟。

## <a name="prerequisites"></a>必要條件
本節詳述 hello hello Windows Server 主機和虛擬陣列的組態先決條件。

### <a name="on-windows-server-host"></a>在 Windows Server 主機上
* 確定 Windows Server 主機已啟用 2 個網路介面。

### <a name="on-storsimple-virtual-array"></a>在 StorSimple Virtual Array 上
* hello 虛擬陣列應該設定為 iSCSI 伺服器。 詳細資訊，請參閱 toolearn[設定 iSCSI 伺服器的虛擬陣列](storsimple-virtual-array-deploy3-iscsi-setup.md)。 Hello 陣列上應該啟用一或多個網路介面。   
* hello 虛擬陣列上的網路介面應該從 hello Windows Server 主機。
* 應該在 StorSimple Virtual Array 上建立一或多個磁碟區。 詳細資訊，請參閱 toolearn[加入磁碟區](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume)StorSimple 虛擬陣列上。 在此程序中，我們會 hello 虛擬陣列上建立 3 磁碟區 （1 在本機固定，2 分層磁碟區所示下方）。
  
    ![mpio0](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio0.png)

### <a name="hardware-configuration-for-storsimple-virtual-array"></a>StorSimple Virtual Array 的硬體設定
hello 圖顯示 hello 硬體組態的高可用性和負載平衡您的 Windows Server 主機和 StorSimple Virtual Array 這個程序中的多重路徑。

![mpio 硬體組態](./media/storsimple-virtual-array-configure-mpio-windows-server/1200hardwareconfig.png)

Hello 前圖所示：

* 在 Hyper-V 上佈建的 StorSimple Virtual Array 是設定為 iSCSI 伺服器的單一節點作用中裝置。
* 陣列上已啟用兩個虛擬網路介面。 在本機 web UI 虛擬陣列 hello，確認 啟用瀏覽過的兩個網路介面**網路設定**如下所示：
  
    ![在 1200 上啟用的網路介面](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio9.png)
  
    請注意 hello IPv4 位址的 hello 啟用網路介面 （乙太網路，預設的乙太網路 2），並儲存供稍後使用 hello 主機上。
* Windows Server 主機已啟用 2 個網路介面。 Hello 主機和陣列的連接的介面是否位於 hello 相同子網路，則會有 4 個路徑可用。 這是此程序中的 hello 案例。 不過，如果 hello 陣列和主機介面上的每個網路介面是不同的 IP 子網路上 （且無法路由傳送），則只有 2 路徑會提供。

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>步驟 1： 安裝 MPIO hello Windows Server 主機上
MPIO 是 Windows 伺服器預設不會安裝的選擇性功能。 您應該透過伺服器管理員將它安裝為功能。 tooinstall 這項功能在 Windows Server 主機上，完成下列程序 hello。

[!INCLUDE [storsimple-install-mpio-windows-server-host](../../includes/storsimple-install-mpio-windows-server-host.md)]

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>步驟 2：為 StorSimple 磁碟區設定 MPIO 
MPIO 必須設定 toobe tooidentify StorSimple 磁碟區。 tooconfigure MPIO toorecognize StorSimple 磁碟區，執行下列步驟的 hello。

[!INCLUDE [storsimple-configure-mpio-volumes](../../includes/storsimple-configure-mpio-volumes.md)]

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>步驟 3: Hello 主機上的掛接 StorSimple 磁碟區
Windows Server 上設定 MPIO 後，建立 hello StorSimple 陣列上的磁碟區即可掛接，然後可利用 MPIO 的備援。 toomount 磁碟區，執行下列步驟的 hello。

#### <a name="toomount-volumes-on-hello-host"></a>toomount hello 主機上的磁碟區
1. 開啟 hello **iSCSI 啟動器屬性**hello Windows Server 主機上的視窗。 跳過**伺服器管理員 > 儀表板 > 工具 > iSCSI 啟動器**。
2. 在 hello **iSCSI 啟動器屬性**對話方塊中，按一下 **探索**，然後按一下**探索目標入口網站**。
3. 在 hello**探索目標入口網站**對話方塊方塊中，執行下列 hello:
   
    1. 在您的 StorSimple Virtual Array 輸入 hello 的 hello 第一個啟用的網路介面的 IP 位址。 根據預設，這會是 **乙太網路**。 
    2. 按一下**確定**tooreturn toohello **iSCSI 啟動器屬性** 對話方塊。
     
    > [!IMPORTANT]
    > 如果您使用私人網路進行 iSCSI 連線，請輸入 hello hello DATA 連接埠是連接的 toohello 私人網路的 IP 位址。
     
4. 在陣列上針對第二個網路介面 (例如，乙太網路 2) 重複步驟 2-3 。 
5. 選取 hello**目標** 索引標籤中 hello **iSCSI 啟動器屬性** 對話方塊。 針對虛擬陣列，您應該將每個磁碟區表面視為**探索到的目標**之下的目標。 在此情況下，會發現三個目標 （對應 toothree 磁碟區）。
   
    ![mpio1](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio1.png)
6. 按一下**連接**tooestablish 與 StorSimple 虛擬陣列的 iSCSI 工作階段。 A**連接 tooTarget**對話方塊隨即出現。 選取 hello**啟用多重路徑**核取方塊。 按一下 [進階] 。
   
    ![mpio2](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio2.png)
7. 在 hello**進階設定**對話方塊方塊中，執行下列 hello:                                        
   
    1. 在 hello**本機介面卡**下拉式清單中，選取**Microsoft iSCSI 啟動器**。
    2. 在 hello**啟動器 IP**下拉式清單中，選取 hello hello 主機 IP 位址。
    3. 在 hello**目標入口網站**IP 下拉式清單中，選取 hello IP 的陣列介面。
    4. 按一下**確定**tooreturn toohello **iSCSI 啟動器屬性** 對話方塊。
     
        ![mpio3](./media/storsimple-ova-configure-mpio-windows-server/mpio3.png)

8. 按一下 [內容] 。 
   
    ![mpio4](./media/storsimple-ova-configure-mpio-windows-server/mpio4.png)

9. 在 hello**屬性**對話方塊中，按一下 **新增工作階段**。
   
   ![mpio5](./media/storsimple-ova-configure-mpio-windows-server/mpio5.png)
10. 在 hello**連接 tooTarget**對話方塊中，選取 hello**啟用多重路徑**核取方塊。 按一下 [進階] 。
11. 在 hello**進階設定**對話方塊：                                        
    
    1. 在 hello**本機介面卡**下拉式清單中，選取 Microsoft iSCSI 啟動器。

    2. 在 hello**啟動器 IP**下拉式清單中，選取 hello IP 位址對應 toohello 主機。 在此情況下，您所連接 hello 陣列 tooa hello 主機上的單一網路介面上的兩個網路介面。 因此，這個介面是 hello 相同的 hello 提供第一個工作階段。

    3. 在 hello**目標入口網站 IP**下拉式清單中，選取 hello hello hello 陣列上啟用第二個資料介面的 IP 位址。

    4. 按一下**確定**tooreturn toohello iSCSI 啟動器屬性 對話方塊。 您已加入第二個工作階段 toohello 目標。
      
       ![mpio11](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio11.png)
    
    5. Hello 中加入想要的 hello 工作階段 （路徑） 之後, **iSCSI 啟動器屬性**對話方塊中，選取 hello 目標，然後按 **屬性**。 Hello hello 工作階段 索引標籤上**屬性**對話方塊中，注意 hello 四個工作階段識別碼對應 toohello 可能的路徑排列組合。 工作階段，toocancel 選取 hello 核取方塊，下一步 tooa 工作階段識別碼，然後按一下**中斷連線**。

    6. 顯示在工作階段中，選取 hello tooview 裝置**裝置** 索引標籤 tooconfigure hello MPIO 原則，是選取的裝置，請按一下**MPIO**。

    7. hello**詳細資料**對話方塊隨即出現。 在 hello **MPIO**索引標籤上，您可以選取適當的 hello**負載平衡原則**設定。 您也可以檢視 hello **Active**或**待命**路徑類型。
12. 重複步驟 8-11 tooadd 額外的工作階段 （路徑） toohello 目標。 Hello 主機上的兩個介面和 hello 虛擬陣列上的兩個，您就可以新增每個目標的四個工作階段總數。 
    
    ![mpio14](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio14.png)
13. 您將需要 toorepeat 步驟執行，每個磁碟區 （做為目標的介面）。
    
    ![mpio15](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio15.png)
14. 開啟**電腦管理**瀏覽過**伺服器管理員 > 儀表板 > 電腦管理**。 在 hello 左窗格中，按一下 **存放裝置 > 磁碟管理**。 hello hello StorSimple Virtual Array 上建立磁碟區會顯示 toothis 主機會出現在**磁碟管理**為新磁碟。
15. 初始化 hello 磁碟，並建立新的磁碟區。 在 hello 格式過程中，選取 64 KB 的配置單位大小 (AUS)。 所有與 hello 可用的磁碟區重複 hello 程序。
    
    ![磁碟管理](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio20.png)
16. 在下**磁碟管理**，以滑鼠右鍵按一下 hello**磁碟**選取**屬性**。
17. 在 [hello**多重路徑磁碟裝置屬性**對話方塊方塊中，按一下 hello **MPIO** ] 索引標籤。
    
    ![磁碟屬性](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio21.png)
18. 在 hello **DSM 名稱**區段中，按一下**詳細資料**並確認已設定 hello 參數 toohello 預設參數。 hello 預設參數為：
    
    * 路徑確認期間 = 30
    * 重試計數 = 3
    * PDO 移除期間 = 20
    * 重試間隔 = 1
    * 啟用路徑確認 = 未選取。
    
    > [!NOTE]
    > **請勿修改 hello 預設參數。**
   
## <a name="next-steps"></a>後續步驟
深入了解[使用您的 StorSimple Virtual Array hello StorSimple 裝置管理員服務 tooadminister](storsimple-virtual-array-manager-service-administration.md)。

