---
title: "為 StorSimple 裝置的 MPIO aaaConfigure |Microsoft 文件"
description: "說明如何為您的 StorSimple 裝置的多重路徑 I/O (MPIO) tooconfigure 連接 tooa 主機執行 Windows Server 2012 R2。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 879fd0f9-c763-4fa0-a5ba-f589a825b2df
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/03/2017
ms.author: alkohli
ms.openlocfilehash: 08cd53039b3868217c7d28e97d7c3c695c06e399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-for-your-storsimple-device"></a>為 StorSimple 裝置設定多重路徑 I/O
建置在 Windows Server toohelp hello 多重路徑 I/O (MPIO) 功能的支援的 Microsoft 建置高可用性、 容錯的 SAN 組態。 MPIO 使用備援實體路徑元件，配接器、 纜線和交換器 — toocreate hello 伺服器與 hello 存放裝置之間的邏輯路徑。 如果沒有元件故障，造成邏輯路徑 toofail，則多重路徑邏輯會使用替代路徑 i/o，讓應用程式仍然可以存取其資料。 此外根據您的設定 MPIO 也可以改善效能的重新平衡所有這些路徑中的 hello 負載。 如需詳細資訊，請參閱 [MPIO 概觀](https://technet.microsoft.com/library/cc725907.aspx "MPIO 概觀 and features")。  

Hello 高可用性的 StorSimple 解決方案，應該在您的 StorSimple 裝置上設定 MPIO。 當您執行 Windows Server 2012 R2 的主機伺服器上安裝 MPIO 時，hello 伺服器然後可容許連結、 網路或介面失效。 

MPIO 是 Windows 伺服器預設不會安裝的選擇性功能。 您應該透過伺服器管理員將它安裝為功能。 本主題描述 hello 步驟，您應該遵循 tooinstall，並執行 Windows Server 2012 R2 和連線的 tooa StorSimple 實體裝置的主機上使用 hello MPIO 功能。

> [!NOTE]
> **此程序僅適用於 StorSimple 8000 系列。StorSimple 虛擬裝置目前不支援 MPIO。**
> 
> 

您需要 toofollow 這些步驟 tooconfigure MPIO StorSimple 裝置上：

* 步驟 1： 安裝 MPIO hello Windows Server 主機上
* 步驟 2：為 StorSimple 磁碟區設定 MPIO 
* 步驟 3: Hello 主機上的掛接 StorSimple 磁碟區
* 步驟 4：設定 MPIO 以獲得高可用性與負載平衡

Hello 下列各節討論 hello 上述步驟。

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>步驟 1： 安裝 MPIO hello Windows Server 主機上
tooinstall 這項功能在 Windows Server 主機上，完成下列程序 hello。

#### <a name="tooinstall-mpio-on-hello-host"></a>tooinstall MPIO hello 主機上
1. 在 Windows Server 主機上開啟 [伺服器管理員]。 根據預設，伺服器管理員啟動的 hello Administrators 群組成員登入時 tooa 電腦執行 Windows Server 2012 R2 或 Windows Server 2012。 如果 hello 伺服器管理員 尚未開啟，請按一下**開始 > 伺服器管理員**。
   ![伺服器管理員](./media/storsimple-configure-mpio-windows-server/IC740997.png)
2. 按一下 [伺服器管理員] > [儀表板] > [新增角色及功能]。 這會啟動 hello**新增角色及功能**精靈。
   ![新增角色及功能精靈 1](./media/storsimple-configure-mpio-windows-server/IC740998.png)
3. 在 hello**新增角色及功能**精靈 中，執行下列 hello:
   
   * 在 hello**開始之前**頁面上，按一下**下一步**。
   * 在 hello**選取安裝類型**頁面上，接受預設設定 hello**角色型或功能型**安裝。 按一下 [伺服器管理員] &gt; [儀表板] &gt; [新增角色及功能] 。![新增角色及功能精靈 2](./media/storsimple-configure-mpio-windows-server/IC740999.png)
   * 在 hello**選取目的地伺服器**頁面上，選擇**從 hello 伺服器集區選取伺服器**。 應該會自動探索主機伺服器。 按一下 [下一步] 。
   * 在 hello**選取伺服器角色**頁面上，按一下**下一步**。
   * 在 hello**選取功能**頁面上，選取**多重路徑 I/O**，然後按一下**下一步**。![新增角色及功能精靈 5](./media/storsimple-configure-mpio-windows-server/IC741000.png)
   * 在 hello**確認安裝選項**頁面上，確認 hello 選取項目，然後選取**必要時自動重新啟動 hello 目的地伺服器**，如下所示。 按一下 [安裝]。![新增角色及功能精靈 8](./media/storsimple-configure-mpio-windows-server/IC741001.png)
   * Hello 安裝已完成時，將會通知您。 按一下**關閉**tooclose hello 精靈。![新增角色及功能精靈 9](./media/storsimple-configure-mpio-windows-server/IC741002.png)

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>步驟 2：為 StorSimple 磁碟區設定 MPIO 
MPIO 必須設定 toobe tooidentify StorSimple 磁碟區。 tooconfigure MPIO toorecognize StorSimple 磁碟區，執行下列步驟的 hello。

#### <a name="tooconfigure-mpio-for-storsimple-volumes"></a>為 StorSimple 磁碟區 tooconfigure MPIO
1. 開啟 hello **MPIO 設定**。 按一下 [伺服器管理員] > [儀表板] > [工具] > [MPIO]。
2. 在 [hello **MPIO 內容**對話方塊中，選取 hello**探索多重路徑**] 索引標籤。
3. 選取 新增 iSCSI 裝置支援，然後按一下新增。  
   ![MPIO 內容探索多重路徑](./media/storsimple-configure-mpio-windows-server/IC741003.png)
4. Hello 伺服器出現提示時重新開機。
5. 在 [hello **MPIO 內容**對話方塊方塊中，按一下 hello **MPIO 裝置**] 索引標籤。按一下**新增**。
    </br>![MPIO 內容 MPIO 裝置](./media/storsimple-configure-mpio-windows-server/IC741004.png)
6. 在 hello**新增 MPIO 支援**對話方塊的 **裝置硬體識別碼**，輸入您裝置的序號。您可以取得 hello 裝置序號存取您的 StorSimple Manager 服務和瀏覽過**裝置 > 儀表板**。 hello 裝置序號會顯示在右 hello**快速概覽**hello 裝置儀表板的窗格。
    </br>![新增 MPIO 支援](./media/storsimple-configure-mpio-windows-server/IC741005.png)
7. Hello 伺服器出現提示時重新開機。

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>步驟 3: Hello 主機上的掛接 StorSimple 磁碟區
Windows Server 上設定 MPIO 後，建立 hello StorSimple 裝置上的磁碟區即可掛接，然後可利用 MPIO 的備援。 toomount 磁碟區，執行下列步驟的 hello。

#### <a name="toomount-volumes-on-hello-host"></a>toomount hello 主機上的磁碟區
1. 開啟 hello **iSCSI 啟動器屬性**hello Windows Server 主機上的視窗。 按一下 [伺服器管理員] > [儀表板] > [工具] > [iSCSI 啟動器]。
2. 在 [hello **iSCSI 啟動器屬性**對話方塊中，按一下 hello 探索] 索引標籤，然後按一下**探索目標入口網站**。
3. 在 hello**探索目標入口網站**對話方塊方塊中，執行下列 hello:
   
   * 輸入您的 StorSimple 裝置的資料連接埠 hello hello IP 位址 （例如，輸入 DATA 0）。
   * 按一下**確定**tooreturn toohello **iSCSI 啟動器屬性** 對話方塊。
     
     > [!IMPORTANT]
     > **如果您使用私人網路進行 iSCSI 連線，請輸入 hello hello DATA 連接埠是連接的 toohello 私人網路的 IP 位址。**
     > 
     > 
4. 在裝置上針對第二個網路介面 (例如，DATA 1) 重複步驟 2-3 。 請記住，您應該為 iSCSI 啟用這些介面。 程式的詳細資訊，請參閱 toolearn[修改網路介面](storsimple-modify-device-config.md#modify-network-interfaces)。
5. 選取 hello**目標** 索引標籤中 hello **iSCSI 啟動器屬性** 對話方塊。 您應該會看到 hello StorSimple 裝置目標 IQN 下的**探索到的目標**。

   ![iSCSI 啟動器內容目標索引標籤](./media/storsimple-configure-mpio-windows-server/IC741007.png)
   
6. 按一下**連接**tooestablish 與您的 StorSimple 裝置的 iSCSI 工作階段。 A**連接 tooTarget**對話方塊隨即出現。
7. 在 hello**連接 tooTarget**對話方塊中，選取 hello**啟用多重路徑**核取方塊。 按一下 [進階] 。
8. 在 hello**進階設定**對話方塊方塊中，執行下列 hello:                                        
   
   * 在 hello**本機介面卡**下拉式清單中，選取**Microsoft iSCSI 啟動器**。
   * 在 hello**啟動器 IP**下拉式清單中，選取 hello hello 主機 IP 位址。
   * 在 hello**目標入口網站**IP 下拉式清單中，選取 hello 的裝置介面的 IP。
   * 按一下**確定**tooreturn toohello **iSCSI 啟動器屬性** 對話方塊。
9. 按一下 [內容] 。 在 hello**屬性**對話方塊中，按一下 **新增工作階段**。
10. 在 hello**連接 tooTarget**對話方塊中，選取 hello**啟用多重路徑**核取方塊。 按一下 [進階] 。
11. 在 hello**進階設定**對話方塊：                                        
    
    * 在 hello**本機介面卡**下拉式清單中，選取 Microsoft iSCSI 啟動器。
    * 在 hello**啟動器 IP**下拉式清單中，選取 hello IP 位址對應 toohello 主機。 在此情況下，您所連接 hello 裝置 tooa hello 主機上的單一網路介面上的兩個網路介面。 因此，這個介面是 hello 相同的 hello 提供第一個工作階段。
    * 在 hello**目標入口網站 IP**下拉式清單中，選取 hello hello hello 裝置上啟用 第二個資料介面的 IP 位址。
    * 按一下**確定**tooreturn toohello iSCSI 啟動器屬性 對話方塊。 您已加入第二個工作階段 toohello 目標。
12. 開啟**電腦管理**瀏覽過**伺服器管理員 > 儀表板 > 電腦管理**。 在 hello 左窗格中，按一下 **存放裝置 > 磁碟管理**。 hello hello StorSimple 裝置上建立磁碟區會顯示 toothis 主機會出現在**磁碟管理**為新磁碟。
13. 初始化 hello 磁碟，並建立新的磁碟區。 在 hello 格式過程中，選取 64 KB 的區塊大小。
    ![磁碟管理](./media/storsimple-configure-mpio-windows-server/IC741008.png)
14. 在下**磁碟管理**，以滑鼠右鍵按一下 hello**磁碟**選取**屬性**。
15. 在 [hello StorSimple 型號 # # #**多重路徑磁碟裝置屬性**對話方塊方塊中，按一下 hello **MPIO** ] 索引標籤。![StorSimple 8100 多重路徑磁碟 DeviceProp。](./media/storsimple-configure-mpio-windows-server/IC741009.png)
16. 在 hello **DSM 名稱**區段中，按一下**詳細資料**並確認已設定 hello 參數 toohello 預設參數。 hello 預設參數為：
    
    * 路徑確認期間 = 30
    * 重試計數 = 3
    * PDO 移除期間 = 20
    * 重試間隔 = 1
    * 啟用路徑確認 = 未選取。

> [!NOTE]
> **請勿修改 hello 預設參數。**


## <a name="step-4-configure-mpio-for-high-availability-and-load-balancing"></a>步驟 4：設定 MPIO 以獲得高可用性與負載平衡
以多重路徑為基礎的高可用性和負載平衡，多個工作階段必須手動新增 toodeclare hello 不同的可用路徑。 比方說，如果 hello 主機有兩個連線的介面 tooSAN 和 hello 裝置有兩個介面連接的 tooSAN，則您需要四個以 （只有兩個工作階段將需要每個 DATA 介面和主機介面如果的正確路徑排列設定的工作階段不同的 IP 子網路上且無法路由傳送)。

**我們建議您至少 8 中的平行工作階段間 hello 裝置和應用程式主機。** 這可藉由在 Windows Server 系統上啟用 4 個網路介面來達成。 使用 Windows Server 主機上 hello 硬體或作業系統層級上的實體網路介面或虛擬介面透過網路虛擬化技術。 Hello 兩個網路介面 hello 裝置上，使用此設定會產生 8 作用中工作階段。 這種組態有助於 hello 裝置和雲端的輸送量最佳化。

> [!IMPORTANT]
> **建議您不要混合使用 1 GbE 與 10 GbE 網路介面。如果您使用兩個網路介面，這兩個介面應屬於 hello 相同類型。**

hello 下列程序描述如何使用兩個網路介面主機兩個網路介面的 StorSimple 裝置時連接的 tooa 的 tooadd 工作階段。 這只會為您提供 2 個作用中的工作階段。 使用這個相同的程序與 StorSimple 裝置與兩個網路介面連接的 tooa 主機具有四個網路介面。 您將需要 tooconfigure 8，而不是 hello 4 此處所述的工作階段。

### <a name="tooconfigure-mpio-for-high-availability-and-load-balancing"></a>高可用性和負載平衡 tooconfigure MPIO
1. 執行探索的 hello 目標： 在 hello **iSCSI 啟動器屬性**] 對話方塊上 hello**探索**索引標籤上，按一下 [**探索入口網站**。
2. 在 hello**連接 tooTarget**對話方塊方塊中，輸入 hello 的其中一個 hello 裝置網路介面的 IP 位址。
3. 按一下**確定**tooreturn toohello **iSCSI 啟動器屬性** 對話方塊。
4. 在 hello **iSCSI 啟動器屬性**對話方塊中，選取 hello**目標**索引標籤上，反白顯示探索到的 hello 目標，然後按一下**連接**。 hello**連接 tooTarget**  對話方塊隨即出現。
5. 在 hello**連接 tooTarget**對話方塊：
   
   * 保持 hello 預設選取的目標設定**將此連線新增**toohello 我的最愛目標清單。 這會使得每次重新啟動此電腦會自動嘗試 toorestart hello 連接 hello 裝置。
   * 選取 hello**啟用多重路徑**核取方塊。
   * 按一下 [進階] 。
6. 在 hello**進階設定**對話方塊：
   
   * 在 hello**本機介面卡**下拉式清單中，選取**Microsoft iSCSI 啟動器**。
   * 在 hello**啟動器 IP**下拉式清單中，選取 hello hello 主機 IP 位址。
   * 在 hello**目標入口網站 IP**下拉式清單中，選取 hello hello 的裝置上啟用的 hello 資料介面 IP 位址。
   * 按一下**確定**tooreturn toohello iSCSI 啟動器屬性 對話方塊。
7. 按一下**屬性**，並在 hello**屬性**對話方塊中，按一下 **新增工作階段**。
8. 在 hello**連接 tooTarget**對話方塊中，選取 hello**啟用多重路徑**核取方塊，然後**進階**。
9. 在 hello**進階設定**對話方塊：
   
   1. 在 hello**本機介面卡**下拉式清單中，選取**Microsoft iSCSI 啟動器**。
   2. 在 hello**啟動器 IP**下拉式清單中，選取 hello IP 位址對應 toohello 第二個介面 hello 主機上的。
   3. 在 hello**目標入口網站 IP**下拉式清單中，選取 hello hello hello 裝置上啟用 第二個資料介面的 IP 位址。
   4. 按一下**確定**tooreturn toohello **iSCSI 啟動器屬性** 對話方塊。 您現在已新增第二個工作階段 toohello 目標。
10. 重複步驟 8-10 tooadd 額外的工作階段 （路徑） toohello 目標。 Hello 主機上的兩個介面和兩個 hello 裝置上，您就可以新增四個工作階段總數。
11. Hello 中加入想要的 hello 工作階段 （路徑） 之後, **iSCSI 啟動器屬性**對話方塊中，選取 hello 目標，然後按 **屬性**。 Hello hello 工作階段 索引標籤上**屬性**對話方塊中，注意 hello 四個工作階段識別碼對應 toohello 可能的路徑排列組合。 工作階段，toocancel 選取 hello 核取方塊，下一步 tooa 工作階段識別碼，然後按一下**中斷連線**。
12. 顯示在工作階段中，選取 hello tooview 裝置**裝置** 索引標籤 tooconfigure hello MPIO 原則，是選取的裝置，請按一下**MPIO**。 hello**裝置詳細資料**對話方塊隨即出現。 在 hello **MPIO**索引標籤上，您可以選取適當的 hello**負載平衡原則**設定。 您也可以檢視 hello **Active**或**待命**路徑類型。

## <a name="next-steps"></a>後續步驟
深入了解[使用您的 StorSimple 裝置組態 hello StorSimple Manager 服務 toomodify](storsimple-modify-device-config.md)。

