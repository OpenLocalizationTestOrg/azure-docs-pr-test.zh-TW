---
title: "Azure StorSimple Virtual Array iSCSI 伺服器安裝程式 aaaMicrosoft |Microsoft 文件"
description: "描述如何 tooperform 初始設定，註冊您的 StorSimple iSCSI 伺服器，並完成裝置設定。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4db116d1-978b-48e8-b572-a719a8425dbc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: b4ff6391cb2af69d4e83dcdac5e027f8498005b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array--set-up-as-an-iscsi-server-via-azure-portal"></a>部署 StorSimple Virtual Array - 透過 Azure 入口網站設定為 iSCSI 伺服器

![iSCSI 安裝程序流程](./media/storsimple-virtual-array-deploy3-iscsi-setup/iscsi4.png)

## <a name="overview"></a>概觀

此部署教學課程適用於 Microsoft Azure StorSimple Virtual Array toohello。 本教學課程說明如何 tooperform hello 初始設定，註冊您的 StorSimple iSCSI 伺服器，完成 hello 裝置設定，然後建立、 掛接、 初始化，並格式化磁碟區上設定 iSCSI 伺服器為您 StorSimple Virtual Array。 

這裡所述的 hello 程序會採取大約 30 分鐘 too1 小時 toocomplete。 這篇文章中發行的 hello 資訊適用於僅 tooStorSimple 虛擬陣列。

## <a name="setup-prerequisites"></a>安裝的必要條件

在您設定及安裝 StorSimple Virtual Array 之前，請先確定：

* 您已佈建的虛擬陣列，並連接中所述的 tooit[部署 StorSimple Virtual Array-佈建為 HYPER-V 中的虛擬陣列](storsimple-ova-deploy2-provision-hyperv.md)或[部署 StorSimple Virtual Array-佈建在 VMware 中的虛擬陣列](storsimple-virtual-array-deploy2-provision-vmware.md).
* 您必須從您建立 toomanage 您 StorSimple 虛擬陣列的 StorSimple 裝置管理員服務 hello hello 服務註冊金鑰。 如需詳細資訊，請參閱**步驟 2： 取得 hello 服務註冊金鑰**中[部署 StorSimple Virtual Array-準備 hello 入口網站](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key)。
* 如果這是 hello 第二或後續虛擬陣列，您會註冊現有的 StorSimple 裝置管理員服務時，您應該 hello 服務資料加密金鑰。 此服務已成功註冊 hello 第一個裝置時，所產生此金鑰。 如果您遺失了金鑰，請參閱**Get hello 服務資料加密金鑰**中[使用 hello Web UI tooadminister 您 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key)。

## <a name="step-by-step-setup"></a>安裝的逐步指示

使用遵循逐步指示 tooset hello，並設定 StorSimple 虛擬陣列：

* [步驟 1： 完成 hello 本機 web UI 安裝並註冊您的裝置](#step-1-complete-the-local-web-ui-setup-and-register-your-device)
* [步驟 2： 完成 hello 所需的裝置設定](#step-2-complete-the-required-device-setup)
* [步驟 3：新增磁碟區](#step-3-add-a-volume)
* [步驟 4：掛接、初始化及格式化磁碟區](#step-4-mount-initialize-and-format-a-volume)

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>步驟 1： 完成 hello 本機 web UI 安裝並註冊您的裝置

#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete hello 安裝和註冊的裝置 hello

1. 開啟瀏覽器視窗。 tooconnect toohello web UI 型別：
   
    `https://<ip-address of network interface>`
   
    使用 hello 上一個步驟中所述的 hello 連接 URL。 您會看到錯誤訊息，通知您沒有 hello 網站的安全性憑證有問題。 按一下**繼續 toothis 網頁**。
   
    ![安全性憑證錯誤](./media/storsimple-virtual-array-deploy3-iscsi-setup/image3.png)
2. 登入 toohello web UI 虛擬裝置做為**StorSimpleAdmin**。 輸入 hello 裝置系統管理員變更密碼。 您在步驟 3： 在開始 hello 虛擬裝置[部署 StorSimple Virtual Array-在 HYPER-V 中的虛擬裝置佈建](storsimple-virtual-array-deploy2-provision-hyperv.md)或[部署 StorSimple Virtual Array-在 VMware 中的虛擬裝置佈建](storsimple-virtual-array-deploy2-provision-vmware.md)。
   
    ![登入頁面](./media/storsimple-virtual-array-deploy3-iscsi-setup/image4.png)
3. 您將會進入 toohello**首頁**頁面。 此頁面描述 hello tooconfigure 和註冊 hello 與 hello StorSimple 裝置管理員服務的虛擬裝置所需的各種設定。 請注意該 hello**網路設定**， **Web proxy 設定**，和**時間設定**是選擇性的。 hello 只需要設定**裝置設定**和**雲端設定**。
   
    ![首頁](./media/storsimple-virtual-array-deploy3-iscsi-setup/image5.png)
4. 在 hello**網路設定**頁面**網路介面**，DATA 0 將會為您自動設定。 每個網路介面會由預設 tooget IP 位址自動設定 (DHCP)。 因此，系統會自動指派 IP 位址、子網路和閘道 (IPv4 和 IPv6 皆適用)。
   
    當您規劃 toodeploy 您的裝置為 iSCSI 伺服器 （tooprovision 區塊存放裝置），我們建議您停用 hello**自動取得 IP 位址**選項，並設定靜態 IP 位址。
   
    ![網路設定頁面](./media/storsimple-virtual-array-deploy3-iscsi-setup/image6.png)
   
    如果您加入多個網路介面 hello 佈建的 hello 裝置期間，您可以在此設定。 請注意，您可以將您的網路介面設定為僅 IPv4 或 IPv4 和 IPv6。 不支援僅 IPv6 組態。
5. 因為它們由您的裝置嘗試與您的雲端儲存體服務提供者或 tooresolve toocommunicate 您的裝置時名稱如果設定為檔案伺服器，都需要 DNS 伺服器。 在 hello**網路設定**頁面下 hello **DNS 伺服器**:
   
   1. 系統會自動設定主要及次要 DNS 伺服器。 如果您選擇 tooconfigure 靜態 IP 位址，您可以指定 DNS 伺服器。 為了達到高可用性，我們建議您設定主要及次要 DNS 伺服器。
   2. 按一下 [Apply (套用)] 。 這將會套用並驗證 hello 網路設定。
6. 在 hello**裝置設定**頁面：
   
   1. 指派一個唯一**名稱**tooyour 裝置。 這個名稱可以有 1 至 15 個字元，且可以包含字母、數字和連字號。
   2. 按一下 hello **iSCSI 伺服器**圖示![iSCSI 伺服器圖示](./media/storsimple-virtual-array-deploy3-iscsi-setup/image7.png)hello**類型**裝置所建立。 ISCSI 伺服器可讓您 tooprovision 區塊存放裝置。
   3. 指定是否要讓此裝置 toobe 已加入網域。 如果您的裝置是 iSCSI 伺服器，然後加入 hello 網域是選擇性的。 如果您決定 toonot 聯結 iSCSI 伺服器 tooa 網域，請按一下**套用**等候 hello 設定 toobe 套用，則可略過 toohello 下一個步驟。
      
       如果您想 toojoin hello 裝置 tooa 網域。 輸入 網域名稱，然後按一下套用。
      
      > [!NOTE]
      > 如果您的虛擬陣列是 Microsoft Azure Active Directory 和群組原則物件 (GPO) 自己組織單位 (OU) 中加入您的 iSCSI 伺服器 tooa 網域，確保會套用的 tooit。
      > 
      > 
   4. 此時畫面會出現對話方塊。 Hello 指定的格式輸入您的網域認證。 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-virtual-array-deploy3-iscsi-setup/image15.png). 將驗證 hello 網域認證。 如果 hello 認證不正確，您會看到一則錯誤訊息。
      
       ![認證](./media/storsimple-virtual-array-deploy3-iscsi-setup/image8.png)
   5. 按一下 [Apply (套用)] 。 這將會套用並驗證 hello 裝置設定。
7. (可省略) 設定 Web Proxy 伺服器。 雖然 Web Proxy 設定是選用的，但請注意，如果您使用 Web Proxy，就只能在此處設定它。
   
    ![設定 Web Proxy](./media/storsimple-virtual-array-deploy3-iscsi-setup/image9.png)
   
    在 hello **Web proxy**頁面：
   
   1. 供應 hello **Web proxy URL**格式如下： *http://host-IP 位址*或*FDQN:Port 數目*。 請注意，此處不支援 HTTPS URL。
   2. 將 [驗證] 指定為 [基本] 或 [無]。
   3. 如果您使用的驗證，您也必須 tooprovide **Username**和**密碼**。
   4. 按一下 [Apply (套用)] 。 這將會驗證並套用 hello 設定 web proxy 設定。
8. （選擇性） 設定您的裝置，例如時區的 hello 時間設定與 hello 主要和次要 NTP 伺服器。 NTP 伺服器是必要的，因為您的裝置必須讓時間同步，才能與您的雲端服務提供者進行驗證。
   
    ![時間設定](./media/storsimple-virtual-array-deploy3-iscsi-setup/image10.png)
   
    在 hello**時間設定**頁面：
   
   1. 從 hello 下拉式清單中，選取 hello**時區**根據裝置正在部署中的 hello hello 地理位置。 hello 裝置的預設時區是太平洋標準時間。 裝置將針對所有排程的操作使用這個時區。
   2. 指定**主要 NTP 伺服器**為您的裝置，或接受 time.windows.com hello 預設值。請確定您的網路允許 NTP 流量 toopass 從您的資料中心 toohello 網際網路。
   3. (選擇性) 指定裝置的 [次要 NTP 伺服器]  。
   4. 按一下 [Apply (套用)] 。 這將會驗證並套用設定的 hello 時間設定。
9. 設定您的裝置 hello 雲端設定。 在此步驟中，您將完成 hello 本機裝置設定，並再將 hello 裝置註冊 StorSimple 裝置管理員服務。
   
   1. 輸入 hello**服務註冊金鑰**您取得**步驟 2： 取得 hello 服務註冊金鑰**中[部署 StorSimple Virtual Array-準備 hello 入口網站](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key)。
   2. 如果這不是您要向此服務的 hello 第一個裝置，您將需要 tooprovide hello**服務資料加密金鑰**。 與 hello 服務註冊金鑰 tooregister 其他裝置以 hello StorSimple 裝置管理員服務需要此金鑰。 如需詳細資訊，請參閱太[Get hello 服務資料加密金鑰](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key)您的本機 web UI。
   3. 按一下 [註冊] 。 這會重新啟動裝置 hello。 您可能需要 toowait 2-3 分鐘，hello 裝置註冊成功。 Hello 裝置重新啟動之後，您將會進入 toohello 登在頁面中。
      
      ![註冊裝置](./media/storsimple-virtual-array-deploy3-iscsi-setup/image11.png)
10. 傳回 toohello Azure 入口網站。
11. 瀏覽 toohello**裝置**刀鋒視窗，您的服務。 如果您有大量資源，請依序按一下 [所有資源]、您的服務名稱 (如有必要，請搜尋) 及 [裝置]。
12. 在 hello**裝置**刀鋒視窗中，確認該 hello 裝置已成功透過查閱 hello 狀態連線 toohello 服務。 hello 裝置狀態應為**已 tooset 準備註冊**。
    
    ![註冊裝置](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png)

## <a name="step-2-configure-hello-device-as-iscsi-server"></a>步驟 2： 設定 iSCSI 伺服器 hello 裝置

執行 hello hello Azure 入口網站 toocomplete hello 所需裝置設定中所述步驟。

#### <a name="tooconfigure-hello-device-as-iscsi-server"></a>為 iSCSI 伺服器 tooconfigure hello 裝置

1. 移 tooyour StorSimple 裝置管理員服務，然後檢閱 太**管理 > 裝置**。 在 hello**裝置**刀鋒視窗中，選取 hello 您剛才建立的裝置。 此裝置會顯示為**已 tooset 準備註冊**。
   
    ![將裝置設定為 iSCSI 伺服器](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png) 
2. 按一下 hello 裝置，您會看到指出該 hello 裝置準備好 toosetup 橫幅訊息。
   
    ![將裝置設定為 iSCSI 伺服器](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis2m.png)  
3. 按一下**設定**hello 裝置命令列上。 這會開啟 hello**設定**刀鋒視窗。 在 hello**設定**刀鋒視窗中，執行下列 hello:
   
   * 自動填入 hello iSCSI 伺服器名稱。
   * 請確定 hello 雲端儲存體加密設定得**啟用**。 這可確保傳送 hello 裝置 toohello 雲端中的 hello 資料已加密。
   * 指定 32 個字元的加密金鑰，並將它記錄在金鑰管理應用程式中，供日後參考。
   * 選取儲存體帳戶 toobe 搭配您的裝置。 在此訂用帳戶，您可以選取現有的儲存體帳戶，或者您可以按一下**新增**toochoose 從不同的訂用帳戶的帳戶。
     
     ![將裝置設定為 iSCSI 伺服器](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis4m.png)
4. 按一下**設定**toocomplete hello iSCSI 伺服器設定。
   
    ![將裝置設定為 iSCSI 伺服器](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis5m.png) 
5. 將會通知您建立 hello iSCSI 伺服器正在進行中。 已成功建立 hello iSCSI 伺服器之後，hello**裝置**刀鋒視窗會更新，而且 hello 對應的裝置狀態**線上**。
   
    ![將裝置設定為 iSCSI 伺服器](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis9m.png)

## <a name="step-3-add-a-volume"></a>步驟 3：新增磁碟區

1. 在 hello**裝置**刀鋒視窗中，選取 hello 裝置您剛才設定 iSCSI 伺服器。 按一下**...** （或者以滑鼠右鍵按一下此資料列中），然後從 hello 內容功能表中，選取**新增磁碟區**。 您也可以按一下**新增磁碟區 +** hello 命令列。 這會開啟 hello**新增磁碟區**刀鋒視窗。
   
    ![新增磁碟區](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis10m.png)
2. 在 hello**新增磁碟區**刀鋒視窗中，請勿遵循 hello:
   
   * 在 hello**磁碟區名稱**欄位中，輸入您的磁碟區的唯一名稱。 hello 名稱必須是包含 3 too127 個字元的字串。
   * 在 hello**類型**下拉式清單中，指定是否 toocreate**分層**或**固定在本機**磁碟區。 對於需要本機保證、低延遲及更高效能的工作負載，請選取 [固定在本機的磁碟區]。 針對所有其他資料，請選取 [階層式磁碟區]**磁碟區**。
   * 在 hello**容量**欄位中，指定 hello hello 磁碟區的大小。 階層式磁碟區必須介於 500 GB 和 5 TB 之間，而固定在本機的磁碟區必須介於 50 GB 和 500 GB 之間。
     
     本機固定磁碟區以佈建，並確保 hello hello 磁碟區中的主要資料將會存留在 hello 裝置並不 spill toohello 雲端。
     
     為分層磁碟區上 hello 另一方面在精簡佈建。 當您建立階層式磁碟區時，大約 10%的 hello 空間 hello 本機層上佈建和 90%的 hello 空間 hello 雲端中佈建。 例如，如果您佈建 1 TB 磁碟區、 100 GB，也可以位於 hello 本機空間和 900GB 會用在 hello 雲端時 hello 資料層。 這又表示的是，如果您用完所有 hello 的本機空間 hello 在裝置上，您無法佈建階層式的共用 （因為 hello 10%將無法使用）。
     
     ![新增磁碟區](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis12.png)
   * 按一下**連線主機**，選取 存取控制記錄 (ACR) 對應 toohello iSCSI 啟動器您想 tooconnect toothis 磁碟區，然後再按一下**選取**。 <br><br> 
3. tooadd 新連線的主機，按一下**新增**，輸入的名稱 hello 主機和其 iSCSI 合格名稱 (IQN)，然後按一下**新增**。 如果您沒有 hello IQN，請移至太[附錄 a： 取得 hello Windows Server 主機的 IQN](#appendix-a-get-the-iqn-of-a-windows-server-host)。
   
      ![新增磁碟區](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis15m.png)
4. 磁碟區設定完成之後，按一下 [確定]。 將指定的 hello 與建立磁碟區設定，您會看到通知。 根據預設，監視和備份將被啟用 hello 磁碟區。
   
     ![新增磁碟區](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis18m.png)
5. hello 磁碟區的 tooconfirm 已成功建立，請移 toohello**磁碟區**刀鋒視窗。 您應該會看到列出的 hello 磁碟區。
   
   ![新增磁碟區](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis20m.png)

## <a name="step-4-mount-initialize-and-format-a-volume"></a>步驟 4：掛接、初始化及格式化磁碟區

執行 hello 下列步驟 toomount 初始化及格式化您的 StorSimple 磁碟區，Windows Server 主機上。

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount、 初始化及格式化磁碟區

1. 開啟 hello **iSCSI 啟動器**hello 適當伺服器上的應用程式。
2. 在 hello **iSCSI 啟動器屬性**視窗的 hello**探索**索引標籤上，按一下 **探索入口網站**。
   
    ![探索入口網站](./media/storsimple-virtual-array-deploy3-iscsi-setup/image22.png)
3. 在 hello**探索目標入口網站**對話方塊中，提供啟用 iSCSI 的網路介面，hello IP 位址，然後按一下**確定**。
   
    ![IP 位址](./media/storsimple-virtual-array-deploy3-iscsi-setup/image23.png)
4. 在 hello **iSCSI 啟動器屬性**視窗的 hello**目標**索引標籤上，找出 hello**探索目標**。 （每個磁碟區將是已探索到的目標）。hello 裝置狀態應顯示為**Inactive**。
   
    ![探索到的目標](./media/storsimple-virtual-array-deploy3-iscsi-setup/image24.png)
5. 選取目標裝置，然後按一下連接。 Hello 裝置連線之後，應該也變更 hello 狀態**Connected**。 (如需有關使用 hello Microsoft iSCSI 啟動器的詳細資訊，請參閱[安裝和設定 Microsoft iSCSI 啟動器][1]。
   
    ![選取目標裝置](./media/storsimple-virtual-array-deploy3-iscsi-setup/image25.png)
6. 在 Windows 主機上，按 hello Windows 爦羆坫 + X、，然後按一下**執行**。
7. 在 [hello**執行**] 對話方塊中，輸入**Diskmgmt.msc**。 按一下**確定**，和 hello**磁碟管理**對話方塊隨即出現。 hello 右窗格會顯示 hello 磁碟區在主機上。
8. 在 hello**磁碟管理**，hello 掛接的磁碟區將會出現視窗 hello 下列圖例所示。 以滑鼠右鍵按一下探索到的 hello 磁碟區 （按一下 hello 磁碟名稱），然後按一下**線上**。
   
    ![磁碟管理](./media/storsimple-virtual-array-deploy3-iscsi-setup/image26.png)
9. 按一下滑鼠右鍵，然後選取 [初始化磁碟] 。
   
    ![初始化磁碟 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image27.png)
10. 在 [hello] 對話方塊中，選取 hello 磁碟 tooinitialize，然後**確定**。
    
    ![初始化磁碟 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image28.png)
11. hello 新增簡單磁碟區精靈 隨即啟動。 請選取磁碟大小，然後按 [下一步] 。
    
    ![新增磁碟區精靈 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image29.png)
12. 指派磁碟機代號 toohello 磁碟區，然後按一下**下一步**。
    
    ![新增磁碟區精靈 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image30.png)
13. 輸入 hello 參數 tooformat hello 磁碟區。 **Windows Server 只支援 NTFS。** 設定 hello 配置單位大小 too64K。 並提供您磁碟區的標籤。 它是建議的最佳作法，您在您的 StorSimple Virtual Array 提供此名稱 toobe 相同 toohello 磁碟區名稱。 按一下 [下一步] 。
    
    ![新增磁碟區精靈 3](./media/storsimple-virtual-array-deploy3-iscsi-setup/image31.png)
14. 請檢查您的磁碟區的 hello 值，然後按一下**完成**。
    
    ![新增磁碟區精靈 4](./media/storsimple-virtual-array-deploy3-iscsi-setup/image32.png)
    
    hello 磁碟區將會顯示為**線上**上 hello**磁碟管理**頁面。
    
    ![磁碟區線上](./media/storsimple-virtual-array-deploy3-iscsi-setup/image33.png)

## <a name="next-steps"></a>後續步驟

了解如何 toouse hello 本機 web UI 太[管理您的 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。

## <a name="appendix-a-get-hello-iqn-of-a-windows-server-host"></a>附錄 a: Get hello Windows Server 主機的 IQN

執行下列步驟 tooget hello iSCSI hello 限定名稱 (IQN) 正在執行 Windows Server 2012 的 Windows 主機。

#### <a name="tooget-hello-iqn-of-a-windows-host"></a>tooget hello Windows 主機的 IQN

1. 在 Windows 主機上啟動 hello Microsoft iSCSI 啟動器。
2. 在 hello **iSCSI 啟動器屬性**視窗的 hello**組態**索引標籤上，選取並複製 hello 字串 hello 從**啟動器名稱**欄位。
   
    ![iSCSI 啟動器屬性](./media/storsimple-virtual-array-deploy3-iscsi-setup/image34.png)
3. 儲存這個字串。

<!--Reference link-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx



