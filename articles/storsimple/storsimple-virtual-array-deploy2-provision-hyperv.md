---
title: "在 HYPER-V 中的 StorSimple Virtual Array aaaProvision |Microsoft 文件"
description: "這是 StorSimple Virtual Array 部署中的第二個教學課程，說明在 Hyper-V 中佈建虛擬陣列。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 4354963c-e09d-41ac-9c8b-f21abeae9913
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f47d642f740827ae1440b819e07067c6a183527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a>部署 StorSimple Virtual Array：在 Hyper-V 中佈建
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a>概觀
本教學課程說明如何 tooprovision StorSimple 虛擬陣列在 Windows Server 2012 R2、 Windows Server 2012 或 Windows Server 2008 R2 上執行 HYPER-V 的主機系統上。 本文適用於 StorSimple 虛擬陣列在 Azure 入口網站和 Microsoft Azure 政府雲端中的 toohello 部署。

您需要系統管理員權限 tooprovision，及設定的虛擬陣列。 hello 佈建和初始設定可能需要約為 10 分鐘 toocomplete。

## <a name="provisioning-prerequisites"></a>佈建的必要條件
這裡您將找到 hello 必要條件 tooprovision 虛擬陣列在 Windows Server 2012 R2、 Windows Server 2012 或 Windows Server 2008 R2 上執行 HYPER-V 的主機系統上。

### <a name="for-hello-storsimple-device-manager-service"></a>Hello StorSimple 裝置管理員服務
在您開始前，請確定：

* 您已完成所有 hello 步驟[準備 hello 入口網站，供 StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md)。
* 您已下載之 HYPER-V 的 hello 虛擬陣列映像從 hello Azure 入口網站。 如需詳細資訊，請參閱**步驟 3： 下載 hello 虛擬陣列影像**的[準備 hello 入口網站的 StorSimple Virtual Array 指南](storsimple-virtual-array-deploy1-portal-prep.md)。

  > [!IMPORTANT]
  > hello StorSimple Virtual Array 上所執行的 hello 軟體只能搭配 hello StorSimple 裝置管理員服務。
  >
  >

### <a name="for-hello-storsimple-virtual-array"></a>Hello StorSimple Virtual Array
在您部署虛擬陣列之前，請確定：

* 您必須執行 HYPER-V 的 Windows Server 2008 R2 或更新版本，可以是使用的 tooa 佈建的裝置存取 tooa 主機系統。
* hello 主機系統是無法 toodedicate hello 下列資源 tooprovision 虛擬陣列：

  * 至少 4 顆核心。
  * 至少 8 GB 的 RAM。 如果您計劃 tooconfigure hello 虛擬與檔案伺服器陣列，8 GB 支援小於 2 百萬個檔案。 您需要 16 GB RAM toosupport 2-4 百萬個檔案。
  * 一個網路介面。
  * 供資料使用的 500 GB 虛擬磁碟。

### <a name="for-hello-network-in-hello-datacenter"></a>Hello 資料中心中的 hello 網路
在開始之前，請檢閱網路需求 toodeploy StorSimple Virtual Array hello，並適當地設定 hello 資料中心網路。 如需詳細資訊，請參閱 [StorSimple Virtual Array 網路需求](storsimple-ova-system-requirements.md#networking-requirements)。

## <a name="step-by-step-provisioning"></a>佈建的逐步指示
tooprovision 和 tooa 虛擬陣列連接，您需要下列步驟 tooperform hello:

1. 請確認 hello 主機系統有足夠的資源 toomeet hello 的最小的虛擬陣列需求。
2. 在 Hypervisor 中佈建虛擬陣列。
3. 啟動 hello 虛擬陣列，並取得 hello IP 位址。

Hello 下列各節將說明每個步驟。

## <a name="step-1-ensure-that-hello-host-system-meets-minimum-virtual-array-requirements"></a>步驟 1： 確定 hello 主機系統符合最低虛擬陣列需求
toocreate 虛擬陣列，您需要：

* Windows Server 2012 R2、 Windows Server 2012 或 Windows Server 2008 R2 SP1 上安裝的 hello HYPER-V 角色。
* Microsoft Windows 用戶端上的 Microsoft HYPER-V 管理員連接 toohello 主機。

請確定該 hello 基礎的硬體 （主機系統） 建立 hello 虛擬陣列可以 toodedicate hello 下列資源 tooyour 虛擬陣列：

* 至少 4 顆核心。
* 至少 8 GB 的 RAM。 如果您計劃 tooconfigure hello 虛擬與檔案伺服器陣列，8 GB 支援小於 2 百萬個檔案。 您需要 16 GB RAM toosupport 2-4 百萬個檔案。
* 一個網路介面。
* 供系統資料使用的 500 GB 虛擬磁碟。

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a>步驟 2：在 Hypervisor 中佈建虛擬陣列
執行下列步驟 tooprovision 您的 hypervisor 中的裝置 hello。

#### <a name="tooprovision-a-virtual-array"></a>tooprovision 虛擬陣列
1. 在 Windows Server 主機上，複製 hello 虛擬陣列映像 tooa 本機磁碟機。 您透過 hello Azure 入口網站下載此映像 （VHD 或 VHDX）。 記下您稍後在 hello 程序中使用此映像時，會複製 hello 映像的 hello 位置。
2. 開啟 [伺服器管理員] 。 在 hello 頂端的右上角，按一下 **工具**選取**HYPER-V 管理員**。

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   如果您執行 Windows Server 2008 R2，開啟 HYPER-V 管理員 hello。 在 [伺服器管理員] 中，按一下 [角色] > [Hyper-V] > [Hyper-V 管理員]。
3. 在**HYPER-V 管理員**hello 範圍窗格中，在您系統節點 tooopen hello 內容功能表中，以滑鼠右鍵按一下，然後按**新增** > **虛擬機器**。

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. 在 hello**開始之前**hello 新的虛擬機器精靈 頁面按一下**下一步**。
5. 在 hello**指定名稱和位置**頁面上，提供**名稱**的虛擬陣列。 按一下 [下一步] 。

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. 在 hello**指定世代**頁面上，選擇 hello 映像的裝置類型，然後按一下**下一步**。 如果您使用的是 Windows Server 2008 R2，則不會出現此頁面。

   * 如果您已下載適用於 Windows Server 2012 或更新版本的 .vhdx 映像，請選擇 [第 2 代]  。
   * 如果您已下載適用於 Windows Server 2008 R2 或更新版本的 .vhd 映像，請選擇 [第 1 代]  。

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. 在 hello**指派記憶體**頁面上，指定**啟動記憶體**的至少**8192 MB**，不要啟用動態記憶體 」，然後按一下**下一步**。

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. 在 hello**設定網路功能**頁面上，指定連接的 toohello 網際網路 hello 虛擬交換器，然後按一下**下一步**。

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. 在 hello**連接虛擬硬碟**頁面上，選擇**使用現有的虛擬硬碟**指定 hello hello 虛擬陣列映像 （.vhdx 或.vhd） 的位置，然後按**下一步**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. 檢閱 hello**摘要**，然後按一下**完成**toocreate hello 虛擬機器。

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. toomeet hello 最低需求，您需要 4 個核心。 tooadd 4 個虛擬處理器，選取在主機系統中 hello **HYPER-V 管理員**視窗。 在 hello 右窗格中的 hello 清單下**虛擬機器**，找出您剛才建立的 hello 虛擬機器。 選取並以滑鼠右鍵按一下 hello 機器名稱，然後選取**設定**。

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. 在 hello**設定**頁面上，在 hello 左窗格中，按一下**處理器**。 在 hello 右窗格中，設定**的虛擬處理器數量**too4 （或以上）。 按一下 [Apply (套用)] 。

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. toomeet hello 最低需求，您也需要 tooadd 500 GB 虛擬資料磁碟。 在 hello**設定**頁面：

    1. Hello 左窗格中，選取**SCSI 控制器**。
    2. Hello 右窗格中，選取**硬碟機**按一下**新增**。

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. 在 hello**硬碟**頁面上，選取 hello**虛擬硬碟**選項，然後按一下**新增**。 hello**新的虛擬硬碟精靈**啟動。

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. 在 hello**開始之前**的 hello 新增虛擬硬碟精靈 頁面上按一下**下一步**。
16. 在 [hello**選擇磁碟格式] 頁面上**，接受預設選項 hello **VHDX**格式。 按一下 [下一步] 。 如果您執行的是 Windows Server 2008 R2，則不會出現此畫面。

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. 在 [hello**選擇磁碟類型] 頁面上**，設定與虛擬硬碟類型**動態擴充**（建議選項）。 **固定大小**磁碟運作，但您可能需要 toowait 很長的時間。 我們建議您不要使用 hello **Differencing**選項。 按一下 [下一步] 。 在 Windows Server 2012 R2 和 Windows Server 2012，**動態擴充**是 hello 預設選項，而在 Windows Server 2008 R2，hello 預設為**固定大小**。

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. 在 hello**指定名稱和位置**頁面上，提供**名稱**以及**位置**（您可以瀏覽 tooone） hello 資料磁碟。 按一下 [下一步] 。

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. 在 hello**設定磁碟**頁面上，選取 hello 選項**建立新的空白虛擬硬碟磁碟**，並指定做為 hello 大小**500 GB** （或以上）。 Hello 最低需求 500 GB 時，一律可以佈建較大的磁碟。 請注意，您無法擴充或縮減 hello 磁碟一次佈建。 如需 hello 大小磁碟 tooprovision 的詳細資訊，檢閱 hello hello 調整大小 > 一節[最佳做法文件](storsimple-ova-best-practices.md)。 按一下 [下一步] 。

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. 在 hello**摘要**頁面上，檢閱您的虛擬資料磁碟的 hello 詳細資料，按一下 如果符合，**完成**toocreate hello 磁碟。 hello 精靈關閉，而加入 tooyour 機器的虛擬硬碟。

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. 傳回 toohello**設定**頁面。 按一下**確定**tooclose hello**設定**頁面上，並傳回 tooHyper HYPER-V 管理員 視窗。

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-hello-virtual-array-and-get-hello-ip"></a>步驟 3： 啟動 hello 虛擬陣列，並取得 hello IP
執行下列步驟 toostart hello 虛擬陣列，並連接 tooit。

#### <a name="toostart-hello-virtual-array"></a>toostart hello 虛擬陣列
1. 啟動 hello 虛擬陣列。

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. Hello 裝置正在執行之後，請選取裝置 hello、 以滑鼠右鍵按一下，然後選取**連接**。

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. 您可能必須 toowait 5-10 分鐘讓裝置 hello toobe，準備好。 狀態訊息會顯示 hello 主控台 tooindicate hello 進度。 Hello 裝置已經備妥之後，請繼續太**動作**。 按`Ctrl + Alt + Delete`toolog toohello 虛擬陣列中的。 hello 預設使用者為*StorSimpleAdmin* hello 預設密碼為*Password1*。

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. 基於安全性理由，hello 裝置系統管理員密碼到期 hello 第一次登入時。 您已提示的 toochange hello 密碼。

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   請輸入至少包含 8 個字元的密碼。 hello 密碼必須符合至少下列 4 個需求的 hello 超出 3： 大寫字母、 小寫、 數字及特殊字元。 重新輸入 hello 密碼 tooconfirm 它。 會通知您該 hello 密碼已變更。

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. 已成功變更 hello 密碼之後，可能會重新啟動 hello 虛擬陣列。 等候 hello 裝置 toostart。

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    hello 的 hello 裝置的 Windows PowerShell 主控台會顯示進度列並。

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. 步驟 6 至 8 僅適用於在非 DHCP 環境中開機的情況。 如果您是在 DHCP 環境，然後略過這些步驟，並移 toostep 9。 如果您已啟動您的裝置，在非 DHCP 環境中，您會看到下列畫面 hello。

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    接著，設定 hello 網路。
7. 使用 hello`Get-HcsIpAddress`命令在您的虛擬陣列上啟用 toolist hello 網路介面。 如果您的裝置具有單一網路介面啟用，hello 預設指派名稱 toothis 介面是`Ethernet`。

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. 使用 hello `Set-HcsIpAddress` cmdlet tooconfigure hello 網路。 請參閱下列範例中的 hello:

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. Hello 初始設定完成後，已開機 hello 裝置之後，您會看到 hello 裝置橫幅文字。 請記下 hello IP 位址，然後顯示 hello 橫幅文字 toomanage hello 裝置中的 hello URL。 使用此 IP 位址 tooconnect toohello web UI，您的虛擬陣列和 hello 完成本機安裝及註冊。

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. （選擇性）只有當您要部署您的裝置 hello 政府雲端中執行此步驟。 您現在將在您的裝置上啟用 hello 美國聯邦資訊處理標準 (FIPS) 模式。 hello FIPS 140 標準會定義核准 hello 保護機密資料的美國聯邦政府電腦系統所使用的密碼編譯演算法。

    1. tooenable hello FIPS 模式中，執行下列 cmdlet 的 hello:

        `Enable-HcsFIPSMode`
    2. 重新啟動您的裝置之後您已經啟用 hello FIPS 模式，以便 hello 密碼編譯的驗證才會生效。

       > [!NOTE]
       > 您可以在您的裝置上啟用或停用 FIPS 模式。 不支援 FIPS 和非 FIPS 模式之間交替 hello 裝置。
       >
       >

如果您的裝置不符合 hello 最低設定需求，您會看到下列錯誤 hello 橫幅文字 （如下所示） 中的 hello。 修改 hello 裝置設定，使 hello 機器有足夠的資源 toomeet hello 最低需求。 然後，您可以重新啟動，並連接 toohello 裝置。 在 toohello 最低設定需求，請參閱[步驟 1： 確定 hello 主機系統符合最低虛擬陣列需求](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements)。

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

如果您使用 hello 本機 web UI 的 hello 初始設定期間所面對任何其他錯誤，請參閱 toohello 下列工作流程：

* 也會執行診斷測試[疑難排解 web UI 安裝](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors)。
* [產生記錄檔封裝及檢視記錄檔](storsimple-ova-web-ui-admin.md#generate-a-log-package)。

## <a name="next-steps"></a>後續步驟
* [Set up your StorSimple Virtual Array as a file server (將 StorSimple 虛擬陣列設定為檔案伺服器)](storsimple-virtual-array-deploy3-fs-setup.md)
* [Set up your StorSimple Virtual Array as an iSCSI server (將 StorSimple 虛擬陣列設定為 iSCSI 伺服器)](storsimple-virtual-array-deploy3-iscsi-setup.md)
