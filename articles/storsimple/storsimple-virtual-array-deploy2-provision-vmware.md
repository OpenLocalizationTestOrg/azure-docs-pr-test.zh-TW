---
title: "在 VMware 中的 StorSimple Virtual Array aaaProvision |Microsoft 文件"
description: "部署 StorSimple Virtual Array 的第二個教學課程，內容為如何在 VMware 中佈建虛擬裝置。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 0425b2a9-d36f-433d-8131-ee0cacef95f8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0912c1c315a04ea46b6373a8fcd5554ecae14e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-vmware"></a>部署 StorSimple Virtual Array：在 VMware 中佈建
![](./media/storsimple-virtual-array-deploy2-provision-vmware/vmware4.png)

## <a name="overview"></a>概觀
這個教學課程描述如何 tooprovision 並連接 tooa StorSimple Virtual Array 和更新版本上執行 VMware ESXi 5.5 主機系統。 本文適用於 StorSimple 虛擬陣列在 Azure 入口網站和 Microsoft Azure 政府雲端 hello toohello 部署。

您需要系統管理員權限 tooprovision，並連線 tooa 虛擬裝置。 hello 佈建和初始設定可能需要約為 10 分鐘 toocomplete。

## <a name="provisioning-prerequisites"></a>佈建的必要條件
hello 必要條件 tooprovision 執行 VMware ESXi 5.5 主機系統上的虛擬裝置，而且上面，如下所示。

### <a name="for-hello-storsimple-device-manager-service"></a>Hello StorSimple 裝置管理員服務
在您開始前，請確定：

* 您已完成所有 hello 步驟[準備 hello 入口網站，供 StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md)。
* 您已下載適用於 VMware 的 hello 虛擬裝置映像從 hello Azure 入口網站。 如需詳細資訊，請參閱**步驟 3： 下載 hello 虛擬裝置映像**的[準備 hello 入口網站的 StorSimple Virtual Array 指南](storsimple-virtual-array-deploy1-portal-prep.md)。

### <a name="for-hello-storsimple-virtual-device"></a>Hello StorSimple 虛擬裝置
在您部署虛擬裝置之前，請確定：

* 您必須執行 HYPER-V 的存取 tooa 主機系統 (2008 R2 或更新版本)，可以是使用的 tooa 佈建裝置。
* hello 主機系統是無法 toodedicate hello 下列資源 tooprovision 虛擬裝置：

  * 至少 4 顆核心。
  * 至少 8 GB 的 RAM。 如果您計劃 tooconfigure hello 虛擬與檔案伺服器陣列，8 GB 支援小於 2 百萬個檔案。 您需要 16 GB RAM toosupport 2-4 百萬個檔案。
  * 一個網路介面。
  * 供系統資料使用的 500 GB 虛擬磁碟。

### <a name="for-hello-network-in-datacenter"></a>資料中心中的 hello 網路
在您開始前，請確定：

* 您已檢閱網路需求 toodeploy hello StorSimple 虛擬裝置並設定的 hello hello 需求依據的資料中心網路。 

## <a name="step-by-step-provisioning"></a>佈建的逐步指示
tooprovision 和 tooa 虛擬裝置連線，您需要下列步驟 tooperform hello:

1. 請確認 hello 主機系統有足夠的資源 toomeet hello 最低虛擬裝置需求。
2. 在 Hypervisor 中佈建虛擬裝置。
3. 啟動 hello 虛擬裝置及取得 hello IP 位址。

## <a name="step-1-ensure-host-system-meets-minimum-virtual-device-requirements"></a>步驟 1：確認主機系統符合最低的虛擬裝置需求
toocreate 虛擬裝置，您將需要：

* 存取 tooa 主機系統執行 VMware ESXi Server 5.5 及更新版本。
* 系統 toomanage hello ESXi 主機上的 VMware vSphere client。

  * 至少 4 顆核心。
  * 至少 8 GB 的 RAM。 如果您計劃 tooconfigure hello 虛擬與檔案伺服器陣列，8 GB 支援小於 2 百萬個檔案。 您需要 16 GB RAM toosupport 2-4 百萬個檔案。
  * 一個網路介面連接能夠路由流量 tooInternet toohello 網路。 hello 最小的網際網路頻寬應為 5 Mbps tooallow hello 裝置的最佳處理。
  * 供資料使用的 500 GB 虛擬磁碟。

## <a name="step-2-provision-a-virtual-device-in-hypervisor"></a>步驟 2：在 Hypervisor 中佈建虛擬裝置
執行下列步驟 tooprovision 中您的 hypervisor 的虛擬裝置 hello。

1. 複製您的系統上的 hello 虛擬裝置映像。 您下載 hello Azure 入口網站透過這個虛擬映像。

   1. 請確定您已下載 hello 最新的映像檔。 如果您先前下載 hello 映像，請再次下載 tooensure 您擁有 hello 最新的映像。 hello 最新的映像有兩個檔案 （而非一個）。
   2. 記下您稍後在 hello 程序中使用此映像時，會複製 hello 映像的 hello 位置。

2. 登入 toohello ESXi 伺服器使用 hello vSphere 用戶端。 您需要 toohave 系統管理員權限 toocreate 虛擬機器。

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image1.png)
3. 在 hello vSphere 中用戶端 hello 清查區段 hello 左窗格中，選取 hello ESXi 伺服器。

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image2.png)
4. 上傳 hello VMDK toohello ESXi 伺服器。 瀏覽 toohello**組態**hello 右窗格中的索引標籤。 選取 [硬體] 下方的 [儲存體]。

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image3.png)
5. 在 hello 右窗格中，在**Datastores**，選取 hello tooupload hello VMDK 所在的資料存放區。 hello 資料存放區必須有足夠的可用空間的 hello OS 和資料磁碟。

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image4.png)
6. 按一下滑鼠右鍵並選取 [瀏覽資料存放區]。

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image5.png)
7. 畫面會出現 [資料存放區瀏覽器]  視窗。

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image6.png)
8. 在 [hello] 工具列上，按一下 [![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png)圖示 toocreate 新的資料夾。 指定 hello 資料夾名稱，然後記下它。 您稍後在建立虛擬機器時，將會使用該資料夾名稱 (建議的最佳做法)。 按一下 [確定] 。

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image8.png)
9. hello 新資料夾會出現在 [hello] 的左窗格 hello**資料存放區的瀏覽器**。

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image9.png)
10. 按一下 hello 上載圖示![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png)選取**上傳檔案**。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image11.png)
11. 您所下載的瀏覽和點 toohello VMDK 檔案。 有兩個檔案。 選取檔案 tooupload。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image12m.png)
12. 按一下 [開啟] 。 hello VMDK 檔案 toohello hello 上的傳指定的資料存放區開始。 可能需要幾分鐘的時間 hello 檔案 tooupload。
13. Hello 上傳完成之後，您會看到您所建立的 hello 資料夾中的 hello 資料存放區中的 hello 檔案。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image14.png)

    現在上傳 hello 第二個 VMDK 檔案 toohello 相同的資料存放區。
14. 傳回 toohello vSphere 用戶端視窗。 在選取 ESXi 伺服器之後按一下滑鼠右鍵，然後選取 [新增虛擬機器] 。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image15.png)
15. 畫面會出限 [建立新虛擬機器]  視窗。 在 hello**組態**頁面上，選取 hello**自訂**選項。 按一下 [下一步] 。
    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image16.png)
16. 在 hello**名稱和位置**頁面上，指定 hello 您的虛擬機器名稱。 這個名稱應該符合您稍早在步驟 8 中指定 hello 資料夾名稱 （建議的最佳作法）。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image17.png)
17. 在 hello**儲存體**頁面上，選取您想要 toouse tooprovision VM 的資料存放區。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image18.png)
18. 在 hello**虛擬機器版本**頁面上，選取**虛擬機器版本： 8**。 所有支援的版本 8 too11。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image19.png)
19. 在 hello**客體作業系統**頁面上，選取 hello**客體作業系統**為**Windows**。 如**版本**，從 hello 下拉式清單中，選取**Microsoft Windows Server 2012 （64 位元）**。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image20.png)
20. 在 hello **Cpu**頁面上，調整 hello**虛擬通訊端數目**和**的每個虛擬通訊端的核心數目**讓的 hello**核心總數**是 4 個 （或以上）。 按一下 [下一步] 。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image21.png)
21. 在 hello**記憶體**頁面上，指定 8 GB （或以上） 的 RAM。 按一下 [下一步] 。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image22.png)
22. 在 hello**網路**頁面上，指定 hello hello 網路介面的數目。 hello 最低需求是一個網路介面。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image23.png)
23. 在 hello **SCSI 控制器**頁面上，接受預設 hello **LSI 邏輯 SAS 控制器**。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image24.png)
24. 在 hello**選取磁碟**頁面上，選擇**使用現有的虛擬磁碟**。 按一下 [下一步] 。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image25.png)
25. 在 hello**選取現有的磁碟**頁面的 **磁碟檔案路徑**，按一下 **瀏覽**。 這會開啟 [瀏覽資料存放區]  對話方塊。 瀏覽您上傳 hello VMDK toohello 位置。 為合併的 hello 一開始上傳的兩個檔案，現在可以看到 hello 資料存放區中的只能有一個檔案。 選取 hello 檔案，然後按一下**確定**。 按一下 [下一步] 。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image26.png)
26. 在 hello**進階選項**頁面上，接受預設值 hello，按一下 **下一步**。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image27.png)
27. 在 hello**準備 tooComplete**頁面上，檢閱與 hello 新的虛擬機器相關聯的所有 hello 設定。 請檢查**編輯 hello 虛擬機器設定完成前的**。 按一下 [繼續]。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image28.png)
28. 在 hello**虛擬機器屬性** 頁面的 hello**硬體**索引標籤上，找出 hello 裝置硬體。 選取 [新增硬碟] 。 按一下 [新增]。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image29.png)
29. 您會看到 [新增硬體] 視窗。 Hello 上**裝置類型**頁面的 **選擇 hello 類型的裝置想 tooadd**，選取**硬碟**，按一下**下一步**。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image30.png)
30. 在 hello**選取磁碟**頁面上，選擇**建立新的虛擬磁碟**。 按一下 [下一步] 。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image31.png)
31. 在 hello**建立磁碟**頁面上，變更 hello**磁碟大小**too500 GB （或以上）。 Hello 最低需求 500 GB 時，一律可以佈建較大的磁碟。 請注意，您無法擴充或縮減 hello 磁碟一次佈建。 如需 hello 大小磁碟 tooprovision 的詳細資訊，檢閱 hello hello 調整大小 > 一節[最佳做法文件](storsimple-ova-best-practices.md)。 在 [磁碟佈建] 下方，選取 [精簡佈建]。 按一下 [下一步] 。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image32.png)
32. 在 hello**進階選項**頁面上，接受預設 hello。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image33.png)
33. 在 hello**準備 tooComplete**頁面上，檢閱 hello 磁碟的選項。 按一下 [完成] 。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image34.png)
34. 傳回 toohello 虛擬機器內容頁面。 新的硬碟加入 tooyour 虛擬機器。 按一下 [完成] 。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image35.png)
35. Hello 右窗格中選取您的虛擬機器，以瀏覽 toohello**摘要** 索引標籤。檢閱您的虛擬機器的 hello 設定。

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image36.png)

您的虛擬機器已成功佈建。 hello 下一個步驟是 toopower 這部電腦上的，取得 hello 的 IP 位址。

## <a name="step-3-start-hello-virtual-device-and-get-hello-ip"></a>步驟 3： 啟動 hello 虛擬裝置及取得 hello IP
執行下列步驟 toostart hello 虛擬裝置，並連接 tooit。

#### <a name="toostart-hello-virtual-device"></a>toostart hello 虛擬裝置
1. 啟動 hello 虛擬裝置。 在 hello vSphere Configuration Manager hello 左窗格中，選取您的裝置，toobring hello 內容功能表上按一下滑鼠右鍵。 選取 [電源]，然後選取 [開啟電源]。 此時您的虛擬機器應該會開機。 您可以在 hello 右下檢視 hello 狀態**最近工作**hello vSphere 用戶端的窗格。

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image37.png)
2. hello 安裝工作需要幾分鐘的時間 toocomplete。 Hello 裝置開始執行之後，瀏覽 toohello**主控台** 索引標籤。傳送 Ctrl + Alt + Delete toolog toohello 裝置中。 或者，您可以指向 hello hello 主控台視窗上的資料指標，然後按下 Ctrl + Alt + Insert。 hello 預設使用者為*StorSimpleAdmin* hello 預設密碼為*Password1*。

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image38.png)
3. 基於安全性理由，hello 裝置系統管理員密碼到期 hello 第一次登入時。 您已提示的 toochange hello 密碼。

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image39.png)
4. 請輸入至少包含 8 個字元的密碼。 hello 密碼必須包含 3 超出 4 個需求： 大寫字母、 小寫、 數字及特殊字元。 重新輸入 hello 密碼 tooconfirm 它。 系統會通知您該 hello 密碼已變更。

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image40.png)
5. 已成功變更 hello 密碼之後，可能要重新啟動 hello 虛擬裝置。 等候 hello 重新開機 toocomplete。 hello Windows PowerShell 主控台中的 hello 裝置可能會顯示進度列以及。

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image41.png)
6. 步驟 6 至 8 僅適用於在非 DHCP 環境中開機的情況。 如果您是在 DHCP 環境，然後略過這些步驟，並移 toostep 9。 如果您已啟動您的裝置，在非 DHCP 環境中，您會看到下列畫面 hello。

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image42m.png)

   接著，設定 hello 網路。
7. 使用 hello`Get-HcsIpAddress`命令 toolist hello 網路介面啟用虛擬裝置上。 如果您的裝置具有單一網路介面啟用，hello 預設指派名稱 toothis 介面是`Ethernet`。

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image43m.png)
8. 使用 hello `Set-HcsIpAddress` cmdlet tooconfigure hello 網路。 範例如下所示：

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image44.png)
9. Hello 初始設定完成後，已開機 hello 裝置之後，您會看到 hello 裝置橫幅文字。 請記下 hello IP 位址，然後顯示 hello 橫幅文字 toomanage hello 裝置中的 hello URL。 您將使用此 IP 位址 tooconnect toohello web UI 您虛擬裝置並完成 hello 本機安裝及註冊。

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image45.png)
10. （選擇性）只有當您要部署您的裝置 hello 政府雲端中執行此步驟。 您現在將在您的裝置上啟用 hello 美國聯邦資訊處理標準 (FIPS) 模式。 hello FIPS 140 標準會定義核准 hello 保護機密資料的美國聯邦政府電腦系統所使用的密碼編譯演算法。

    1. tooenable hello FIPS 模式中，執行下列 cmdlet 的 hello:

        `Enable-HcsFIPSMode`
    2. 重新啟動您的裝置之後您已經啟用 hello FIPS 模式，以便 hello 密碼編譯的驗證才會生效。

       > [!NOTE]
       > 您可以在您的裝置上啟用或停用 FIPS 模式。 不支援 FIPS 和非 FIPS 模式之間交替 hello 裝置。
       >
       >

如果您的裝置不符合 hello 最低設定需求，您會看到 hello 橫幅文字 （如下所示） 中的錯誤。 您必須 toomodify hello 裝置設定，使其具有足夠的資源 toomeet hello 最低需求。 然後，您可以重新啟動，並連接 toohello 裝置。 在 toohello 最低設定需求，請參閱[步驟 1： 確定 hello 主機系統符合最低虛擬裝置需求](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements)。

![](./media/storsimple-virtual-array-deploy2-provision-vmware/image46.png)

如果您使用 hello 本機 web UI 的 hello 初始設定期間所面對任何其他錯誤，請參閱 toohello 下列工作流程：

* 也會執行診斷測試[疑難排解 web UI 安裝](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors)。
* [產生記錄檔封裝及檢視記錄檔](storsimple-ova-web-ui-admin.md#generate-a-log-package)。

## <a name="next-steps"></a>後續步驟
* [Set up your StorSimple Virtual Array as a file server (將 StorSimple 虛擬陣列設定為檔案伺服器)](storsimple-virtual-array-deploy3-fs-setup.md)
* [Set up your StorSimple Virtual Array as an iSCSI server (將 StorSimple 虛擬陣列設定為 iSCSI 伺服器)](storsimple-virtual-array-deploy3-iscsi-setup.md)
