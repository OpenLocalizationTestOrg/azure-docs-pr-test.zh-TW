---
title: "aaaAutomate StorSimple fileshare DR 與 Azure Site Recovery |Microsoft 文件"
description: "描述 hello 步驟和最佳作法，建立裝載於 Microsoft Azure StorSimple 儲存體檔案共用的災害復原方案。"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 23049a2c-055e-4d0e-b8f5-af2a87ecf53f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/09/2017
ms.author: vidarmsft
ms.openlocfilehash: fa3e8d4e77ca0f6a7b5f9bbb956a4de12547642e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automated-disaster-recovery-solution-using-azure-site-recovery-for-file-shares-hosted-on-storsimple"></a>針對 StorSimple 上裝載的檔案共用使用 Azure Site Recovery 的自動化災害復原解決方案
## <a name="overview"></a>概觀
Microsoft Azure StorSimple 是混合式雲端儲存體解決方案位址 hello 通常與檔案共用相關聯的非結構化資料的複雜性。 StorSimple 會使用雲端儲存體，當做 hello 的延伸模組在內部部署解決方案和自動層跨內部部署儲存體和雲端儲存體的資料。 整合資料保護與本機和雲端快照集，可以降低對 hello 正在擴張的儲存體基礎結構需求。

[Azure Site Recovery](../site-recovery/site-recovery-overview.md) 是以 Azure 為基礎的服務，藉由協調虛擬機器的複寫、容錯移轉及復原，提供災害復原 (DR) 功能。 Azure Site Recovery 支援許多複寫技術 tooconsistently 複寫、 保護及流暢地容錯移轉虛擬機器和應用程式 tooprivate/公用或託管雲端。

您可以使用 Azure Site Recovery 中，虛擬機器複寫和 StorSimple 雲端快照集功能，來保護 hello 完整的檔案伺服器環境。 在 hello 事件中的中斷，您可以使用您的檔案共用線上 Azure 在短短幾分鐘內按一下 toobring。

本文件詳細說明如何為您 StorSimple 儲存體上裝載的檔案共用建立災害復原解決方案，以及使用單鍵復原計劃執行已計劃、未計劃及測試容錯移轉。 基本上，它會顯示如何修改復原計劃的 hello 在您的 Azure Site Recovery 保存庫 tooenable StorSimple 容錯移轉期間災害案例。 此外，它也會說明支援的組態與先決條件。 本文件假設您熟悉 hello 的 Azure Site Recovery 和 StorSimple 架構的基本概念。

## <a name="supported-azure-site-recovery-deployment-options"></a>支援的 Azure Site Recovery 部署選項
客戶可以將檔案伺服器部署為在 Hyper-V 或 VMware 上執行的實體服務或虛擬機器 (VM)，然後從由 StorSimple 儲存體劃分出來的磁碟區建立檔案共用。 Azure Site Recovery 保護這兩個實體和虛擬部署 tooeither 次要站台或 tooAzure。 本文件涵蓋 Azure 以做為檔案伺服器裝載在 HYPER-V 上的 VM hello 復原站台與 StorSimple 儲存體上的檔案共用的 DR 解決方案的詳細資料。 其他案例中的 hello 檔案伺服器 VM 位在 VMware VM 或實體機器實作類似。

## <a name="prerequisites"></a>必要條件
實作一種單鍵災害復原解決方案，用於裝載於 StorSimple 儲存體檔案共用中的 Azure Site Recovery 有 hello 下列必要條件：

* Hyper-V 或 VMware 或實體電腦上裝載的內部部署 Windows Server 2012 R2 檔案伺服器 VM
* 在 Azure StorSimple Manager 註冊之 StorSimple 儲存體裝置內部部署
* StorSimple hello Azure StorSimple manager （這可以保持關閉狀態） 中建立的雲端應用裝置
* 裝載在 hello hello StorSimple 儲存裝置上設定的磁碟區上的檔案共用
* [Azure Site Recovery 服務保存庫](../site-recovery/site-recovery-vmm-to-vmm.md) 

此外，如果 Azure 網站復原，請執行 hello [Azure 虛擬機器整備評估工具](http://azure.microsoft.com/downloads/vm-readiness-assessment/)上 Vm tooensure 它們彼此相容 Azure Vm 與 Azure Site Recovery 服務。

tooavoid 延遲問題 （這可能會導致較高的成本），確定您建立您 StorSimple 雲端應用裝置，自動化帳戶，而且儲存體帳戶中的 hello 相同的區域。

## <a name="enable-dr-for-storsimple-file-shares"></a>針對 StorSimple 檔案共用啟用 DR
Hello 的每個元件在內部部署環境，必須保護 toobe tooenable 完整的複寫和復原。 本節說明如何：

* 設定 Active Directory 和 DNS 複寫 (選擇性)
* 使用 Azure Site Recovery tooenable 保護 hello 檔案伺服器 VM 的
* 保護 StorSimple 磁碟區
* 設定 hello 網路

### <a name="set-up-active-directory-and-dns-replication-optional"></a>設定 Active Directory 和 DNS 複寫 (選擇性)
如果您想要執行 Active Directory 和 DNS，讓它們無法在 hello DR 網站的機器，您需要 tooexplicitly tooprotect hello （以便 hello 檔案的伺服器存取驗證容錯移轉之後） 保護它們。 有兩個建議的選項根據 hello 客戶的內部部署環境的 hello 複雜性。

#### <a name="option-1"></a>選項 1
如果 hello 客戶有少量應用程式，hello 整個的單一網域控制站在內部部署站台，和將會容錯移轉 hello 整個站台，則我們建議使用 Azure Site Recovery 複寫 tooreplicate hello 網域控制站機器（這僅適用於站台對站台和站台至 Azure） tooa 次要站台。

#### <a name="option-2"></a>選項 2
如果 hello 客戶具有大量的應用程式、 執行 Active Directory 樹系，而且會容錯移轉一些應用程式，一次，則我們建議您設定 hello DR 網站上的其他網域控制站 (次要網站或 Azure 中)。

請參閱太[自動化 DR 解決方案的 Active Directory 和 DNS 使用 Azure Site Recovery](../site-recovery/site-recovery-active-directory.md) hello DR 網站上可用的網域控制站時的指示。 本文件的 hello 其餘部分，我們會假設為網域控制站上可用的 hello DR 網站。

### <a name="use-azure-site-recovery-tooenable-protection-of-hello-file-server-vm"></a>使用 Azure Site Recovery tooenable 保護 hello 檔案伺服器 VM 的
此步驟需要您準備 hello 在內部部署檔案伺服器環境、 建立和準備 Azure Site Recovery 保存庫，並啟用檔案的 hello VM 的保護。

#### <a name="tooprepare-hello-on-premises-file-server-environment"></a>tooprepare hello 在內部部署檔案伺服器環境
1. 設定 hello**使用者帳戶控制**太**不要通知**。 這是必要的好讓您可以使用 Azure 自動化指令碼 tooconnect hello iSCSI 目標移轉 Azure Site Recovery 失敗之後。

   1. 按 hello Windows 鍵 + Q，並搜尋**UAC**。
   2. 選取 [變更使用者帳戶控制設定] 。
   3. 朝向 toohello 下方列拖曳 hello**不要通知**。
   4. 按一下 [確定] 然後在提示時選取 [是]。

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image1.png)
2. 在每個 hello 檔案伺服器 Vm 安裝 hello VM 代理程式。 這是必要的以便您可以在 hello 容錯移轉的 Vm 上執行 Azure 自動化指令碼。

   1. [下載 hello 代理程式](http://aka.ms/vmagentwin)太`C:\\Users\\<username>\\Downloads`。
   2. 系統管理員模式 （系統管理員身分執行），開啟 Windows PowerShell，然後輸入下列命令 toonavigate toohello 下載位置的 hello:

      `cd C:\\Users\\<username>\\Downloads\\WindowsAzureVmAgent.2.6.1198.718.rd\_art\_stable.150415-1739.fre.msi`

      > [!NOTE]
      > 視 hello 版本而定，可能會變更 hello 檔案名稱。
      >
      >
3. 按一下 [下一步] 。
4. 接受 hello**協議條款**，然後按一下**下一步**。
5. 按一下 [完成] 。
6. 使用從 StorSimple 儲存體劃分出來的磁碟區建立檔案共用。 如需詳細資訊，請參閱[使用 hello StorSimple Manager 服務 toomanage 磁碟區](storsimple-manage-volumes.md)。

   1. 在您的內部部署 Vm 上按 hello Windows 鍵 + Q，並搜尋**iSCSI**。
   2. 選取 [iSCSI 啟動器]。
   3. 選取 hello**組態** 索引標籤，並複製 hello 啟動器名稱。
   4. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
   5. 選取 hello **StorSimple**  索引標籤，然後選取 hello 包含 hello 實體裝置的 StorSimple Manager 服務。
   6. 建立磁碟區容器，然後建立磁碟區。 （這些磁碟區是針對 hello hello 檔案伺服器 Vm 上的檔案共用。） 複製 hello 啟動器名稱，並將適當的名稱，如 hello 存取控制記錄，當您建立 hello 磁碟區。
   7. 選取 hello**設定** 索引標籤並記下 hello 裝置 hello IP 位址。
   8. 在您的內部部署 Vm，請移 toohello **iSCSI 啟動器**一次，然後輸入 hello IP hello 快速連線 區段中。 按一下**快速連線**（hello 裝置現在應該已經連線）。
   9. 開啟 hello Azure 入口網站和選取 hello**磁碟區和裝置** 索引標籤。按一下 自動設定 。 您剛才建立的 hello 磁碟區應該會出現。
   10. 在 hello 入口網站中，選取 hello**裝置**索引標籤，然後選取 **建立新的虛擬裝置。** (此虛擬裝置將會在發生容錯移轉時使用)。 這個新的虛擬裝置保留在離線狀態 tooavoid 付出的額外成本。 tootake hello 虛擬裝置離線，請移 toohello**虛擬機器**區段 hello 入口網站，然後將它關閉。
   11. 請返回 toohello 內部部署 Vm，並開啟 [磁碟管理] (按 hello Windows 鍵 + X 並選取**磁碟管理**)。
   12. 您會發現某些額外的磁碟 （取決於您所建立的磁碟區的 hello 數目）。 以滑鼠右鍵按一下 hello 第一個，請選取**初始化磁碟**，然後選取**確定**。 以滑鼠右鍵按一下 hello**未配置**區段中，選取**新增簡單磁碟區**、 將它指派磁碟機代號，以及完成 hello 精靈。
   13. 針對所有 hello 磁碟重複步驟 l。 您現在可以看到所有的 hello 磁碟上**此 PC** hello Windows 檔案總管 中。
   14. 這些磁碟區上使用 hello 檔案和存放服務角色 toocreate 檔案共用。

#### <a name="toocreate-and-prepare-an-azure-site-recovery-vault"></a>toocreate 並準備 Azure Site Recovery 保存庫
請參閱 toohello [Azure Site Recovery 文件](../site-recovery/site-recovery-hyper-v-site-to-azure.md)tooget 與 Azure Site Recovery 保護 hello 檔案伺服器 VM 之前啟動。

#### <a name="tooenable-protection"></a>tooenable 保護
1. 中斷連線 hello iSCSI 目標 hello 從內部部署 Vm，您想要透過 Azure Site Recovery tooprotect:

   1. 按 Windows 鍵 +Q 並搜尋 **iSCSI**。
   2. 選取 [設定 iSCSI 啟動器] 。
   3. 中斷連接您在先前連線的 hello StorSimple 裝置。 或者，您可以關閉 hello 檔案伺服器在幾分鐘後啟用保護時。

   > [!NOTE]
   > 這會導致 hello 檔案共用 toobe 暫時無法使用。
   >
   >
2. [啟用虛擬機器保護](../site-recovery/site-recovery-hyper-v-site-to-azure.md)的 hello 檔案伺服器 VM 的 hello Azure Site Recovery 入口網站。
3. Hello 初始同步處理開始時，您可以一次重新 hello 目標的連線。 移 toohello iSCSI 啟動器，選取 hello StorSimple 裝置，然後按一下**連接**。
4. 當 hello 同步處理已完成且 hello hello VM 狀態是**保護**、 選取 hello VM、 選取 hello**設定**索引標籤，並據此更新 hello hello VM 網路 （這是 hello 網路容錯移轉 VM 該 hello 將的一部分）。 如果未顯示 hello 網路，則表示 hello 同步處理正在仍進行的作業。

### <a name="enable-protection-of-storsimple-volumes"></a>保護 StorSimple 磁碟區
如果您沒有選取 hello**啟用此磁碟區的預設備份**選項為 hello StorSimple 磁碟區，請跳過**備份原則**入 hello StorSimple Manager 服務，並建立適當的備份hello 的所有磁碟區的原則。 我們建議您設定的備份 toohello 復原點目標 (RPO) 您希望 toosee hello 應用程式的 hello 頻率。

### <a name="configure-hello-network"></a>設定 hello 網路
針對檔案伺服器 VM hello，如此 hello VM 網路會附加的 toohello 正確的 DR 網路容錯移轉之後，Azure Site Recovery 中設定網路設定。

您可以選擇 hello hello VM**複寫項目**tooconfigure hello 網路設定 索引標籤上，hello 下列圖例所示。

![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image2.png)

## <a name="create-a-recovery-plan"></a>建立復原計畫
您可以建立復原計劃在 ASR tooautomate hello 容錯移轉程序的 hello 檔案共用中。 如果發生中斷，您可以在幾分鐘後，只需要單一按一下 hello 檔案共用叫出。 tooenable 這項自動化，您需要 Azure 自動化帳戶。

#### <a name="toocreate-an-automation-account"></a>toocreate 自動化帳戶
1. 前往 Azure 入口網站 toohello &gt; **自動化**> 一節。
2. 按一下 [+ 加] 按鈕，開啟下方的刀鋒視窗。

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image11.png)

   * [名稱] - 輸入一個新的自動化帳戶
   * [訂用帳戶] - 選擇訂用帳戶
   * [資源群組] - 建立新的或選擇現有的資源群組
   * 位置-選擇位置、 將它保存在 hello 相同/地區中的 hello StorSimple 雲端應用裝置和儲存體帳戶所建立。
   * 建立 Azure 執行身分帳戶 - 選取 [是] 選項。

3. 移 toohello 自動化帳戶中，按一下**Runbook** &gt; **瀏覽圖庫**hello 自動化帳戶所有 hello 的 tooimport 所需的 runbook。
4. 新增下列 runbook 藉由尋找 hello**嚴重損壞修復**hello 圖庫中的標記：

   * 在測試容錯移轉 (TFO) 之後清除 StorSimple 磁碟區
   * 容錯移轉 StorSimple 磁碟區容器
   * 在容錯移轉之後於 StorSimple 裝置上掛接磁碟區
   * 在 Azure VM 中解除安裝自訂指令碼擴充功能
   * 啟動 StorSimple 虛擬設備

     ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image3.png)

5. 藉由選取 hello 自動化帳戶中的 hello runbook 發行所有 hello 指令碼，並按一下**編輯** &gt; **都發行**然後**是**toohello 驗證訊息。 這個步驟之後，hello **Runbook**  索引標籤會出現，如下所示：

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image4.png)

6. Hello 自動化帳戶中，選取 [hello**資產**] 索引標籤&gt;按一下**變數** &gt; **加入變數**並加入下列變數的 hello。 您可以選擇 tooencrypt 這些資產。 這些變數都是復原計劃特定變數。 如果您的復原計劃 （這樣您將建立 hello 下一個步驟中） 名稱 TestPlan，則您的變數應為 TestPlan StorSimRegKey、 TestPlan AzureSubscriptionName，等等。

   * *RecoveryPlanName***-StorSimRegKey**: hello hello StorSimple Manager 服務的登錄機碼。
   * *RecoveryPlanName***-AzureSubscriptionName**: hello hello Azure 訂用帳戶名稱。
   * *RecoveryPlanName***-ResourceName**: hello hello hello StorSimple 裝置的 StorSimple 資源名稱。
   * *RecoveryPlanName***-DeviceName**: hello 裝置具有 toobe 容錯移轉。
   * *RecoveryPlanName***-VolumeContainers**: volcon1、 volcon2、 volcon3 呈現 hello 需要 toobe 超過; 例如，失敗的裝置上的磁碟區容器以逗號分隔字串。
   * *RecoveryPlanName***-TargetDeviceName**: hello StorSimple 雲端應用裝置的 hello 容器是 toobe 容錯移轉。
   * *RecoveryPlanName***-TargetDeviceDnsName**: hello 目標裝置 hello 服務名稱 (這可以在 hello**虛擬機器**區段： hello 服務名稱是以 hello hello 相同DNS 名稱）。
   * *RecoveryPlanName***-StorageAccountName**: hello 指令碼中的 hello 儲存體帳戶名稱 （這在 hello toorun 失敗容錯移轉的 VM） 會儲存。 這可以是任何暫時有一些空間 toostore hello 指令碼的儲存體帳戶。
   * *RecoveryPlanName***-StorageAccountKey**: hello hello 上面儲存體帳戶的存取金鑰。
   * *RecoveryPlanName***-ScriptContainer**: hello hello 容器中的 hello 指令碼將會儲存在 hello 雲端名稱。 如果 hello 容器不存在，則會建立。
   * *RecoveryPlanName***-VMGUIDS**： 時保護 VM，Azure Site Recovery 指派每個 VM 的唯一識別碼，可讓容錯移轉 VM hello hello 詳細資料。 tooobtain hello VMGUID，選取 hello**復原服務**索引標籤上，按一下 **保護的項目** &gt; **保護群組** &gt; **機器** &gt; **屬性**。 如果您有多個 Vm，然後加入 hello Guid 做為以逗號分隔的字串。
   * *RecoveryPlanName***-AutomationAccountName** – hello hello 自動化帳戶已加入 hello runbook 與 hello 資產的名稱。

  例如，如果 hello hello 復原計劃的名稱是 fileServerpredayRP，那麼您**認證** & **變數**索引標籤應該會出現，如下所示將所有的 hello 資產之後。

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image5.png)

7. 移 toohello**復原服務**區段與您稍早建立的選取 hello Azure Site Recovery 保存庫。
8. 選取 hello**復原計劃 (Site Recovery)**選項**管理**群組，並建立新的復原計劃，如下所示：

   a.  按一下 [+ 復原計劃] 按鈕，開啟如下的刀鋒視窗。

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image6.png)

   b.  輸入復原計劃名稱，選擇來源、目標及部署模型值。

   c.  從 hello 保護群組的 tooinclude hello 復原計劃和按一下選取 hello Vm**確定** 按鈕。

   d.  選取您稍早建立的復原計劃中，按一下**自訂**按鈕 tooopen hello 復原方案自訂檢視。

   e.  以滑鼠右鍵按一下 [所有關閉的群組] ，然後按一下 [新增前置動作] 。

   f.  開啟插入動作刀鋒視窗中，輸入名稱，選取**主要端**toorun 選項選取 （這在您已新增 hello runbook） 的自動化帳戶，然後選取 hello 的位置中的選項**容錯移轉 StorSimple 磁碟區-容器**runbook。

   g.  以滑鼠右鍵按一下**群組 1： 啟動**按一下**新增受保護項目**選項，然後選取屬於受保護的 hello 復原計劃和按一下 toobe hello Vm**確定**按鈕。 (選用項目)。如果是已選取 VM。

   h.  以滑鼠右鍵按一下**群組 1： 啟動**按一下**後動作**選項，然後加入所有 hello 下列指令碼：

   * Start-StorSimple-Virtual-Appliance runbook
   * Fail over-StorSimple-volume-containers runbook
   * Mount-volumes-after-failover runbook
   * Uninstall-custom-script-extension runbook

   i.  上述 4 hello 指令碼在 hello 相同之後新增手動動作**群組 1： 後續步驟**> 一節。 這個動作時，您可以確認一切運作正常的 hello 點。 這個動作需要 toobe 僅新增為測試容錯移轉的一部分 (因此只選取 hello**測試容錯移轉**核取方塊)。

   j.  在 hello 手動動作，後面加上 hello**清除**指令碼使用 hello 相同的程序使用 hello 用其他 runbook。 **儲存**hello 復原計劃。

    > [!NOTE]
    > 當執行測試容錯移轉，您應該確認在 hello 手動動作步驟的所有項目，因為有 hello 目標裝置已複製的 hello StorSimple 磁碟區將會刪除的 hello 清除一部份 hello 手動動作完成之後。
    >

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image7.png)

## <a name="perform-a-test-failover"></a>執行測試容錯移轉
請參閱 toohello [Active Directory DR 解決方案](../site-recovery/site-recovery-active-directory.md)考量特定 tooActive 目錄，hello 測試容錯移轉期間的附屬指南。 hello 測試容錯移轉發生時，會在所有影響 hello 在內部部署安裝程式。 hello StorSimple 磁碟區已附加 toohello 內部部署 VM 會複製的 toohello StorSimple 在 Azure 上的雲端應用裝置。 供測試使用的 VM 在 Azure 中，會帶出和 hello 複製磁碟區附加的 toohello VM。

#### <a name="tooperform-hello-test-failover"></a>tooperform hello 測試容錯移轉
1. 在 hello Azure 入口網站，選取您的站台復原保存庫。
2. 按一下 建立 hello 檔案伺服器 VM 的 hello 復原計劃。
3. 按一下 [測試容錯移轉] 。
4. 容錯移轉發生後，將會連接到選取的 hello Azure 虛擬網路 toowhich Azure Vm。

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image8.png)
5. 按一下**確定**toobegin hello 容錯移轉。 您可以追蹤進度，藉由按 hello VM tooopen 其屬性，或是在 hello**測試容錯移轉工作**在保存庫名稱&gt;**作業** &gt; **的站台復原工作**.
6. Hello 容錯移轉完成之後，您應該也可以在 hello Azure 入口網站中出現 toosee hello 複本 Azure 機器&gt;**虛擬機器**。 您可以執行您的驗證。
7. Hello 驗證完成後，按一下 **驗證完整**。 這會清除 hello StorSimple 磁碟區和關閉 hello StorSimple 雲端應用裝置。
8. 一旦您完成時，按一下 **清除測試容錯移轉**hello 復原計劃。 在備忘稿記錄和任何 hello 與相關聯的觀察值儲存測試容錯移轉。 這將刪除 hello 測試容錯移轉期間所建立的虛擬機器。

## <a name="perform-a-planned-failover"></a>執行計劃性容錯移轉
   在計劃的容錯移轉期間 hello 內部部署檔案的伺服器關閉 VM 依正常程序以及備份 hello StorSimple 裝置上的磁碟區的快照時的雲端。 hello StorSimple 磁碟區已容錯移轉 toohello 虛擬裝置，VM 就會重新在 Azure 的複本和 hello 磁碟區已附加的 toohello VM。

#### <a name="tooperform-a-planned-failover"></a>tooperform 規劃的容錯移轉
1. 在 hello Azure 入口網站，選取 **復原服務**保存庫&gt;**復原計劃 (Site recovery)** &gt; **recoveryplan_name**建立hello 檔案伺服器 VM。
2. 在 hello 復原計劃刀鋒視窗中，按一下 **詳細** &gt;**規劃的容錯移轉**。  

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image9.png)
3. 在 hello**確認計劃的容錯移轉**刀鋒視窗中，選擇 hello 來源和目標位置，以及選取目標網路，然後按一下 hello 核取圖示 ✓ toostart hello 容錯移轉程序。
4. 建立複本虛擬機器之後，它們即會處於認可擱置中的狀態。 按一下**認可**toocommit hello 容錯移轉。
5. 複寫完成之後，hello 虛擬機器時，啟動 hello 次要位置。

## <a name="perform-a-failover"></a>執行容錯移轉
未規劃的容錯移轉期間 hello StorSimple 磁碟區已容錯移轉 toohello 虛擬裝置，VM 會帶出在 Azure 的複本和 hello 磁碟區附加的 toohello VM。

#### <a name="tooperform-a-failover"></a>tooperform 容錯移轉
1. 在 hello Azure 入口網站，選取 **復原服務**保存庫&gt;**復原計劃 (Site recovery)** &gt; **recoveryplan_name**建立hello 檔案伺服器 VM。
2. 在 hello 復原計劃刀鋒視窗中，按一下 **詳細** &gt;**容錯移轉**。  
3. 在 hello**確認容錯移轉**刀鋒視窗中，選擇 hello 來源和目標位置。
4. 選取**關閉虛擬機器並同步處理 hello 最新的資料**toospecify 站台復原應該嘗試 tooshut 關閉 hello 受保護的虛擬機器，並同步處理 hello 資料，以便 hello 最新版本的 hello 資料將會容錯移轉。
5. Hello 容錯移轉之後，hello 虛擬機器都處於認可擱置狀態。 按一下**認可**toocommit hello 容錯移轉。


## <a name="perform-a-failback"></a>執行容錯移轉
在容錯回復，StorSimple 磁碟區容器已容錯移轉後 toohello 實體裝置後執行備份。

#### <a name="tooperform-a-failback"></a>tooperform 容錯回復
1. 在 hello Azure 入口網站，選取 **復原服務**保存庫&gt;**復原計劃 (Site Recovery)** &gt; **recoveryplan_name**建立hello 檔案伺服器 VM。
2. 在 hello 復原計劃刀鋒視窗中，按一下 **詳細** &gt;**計劃的容錯移轉**。  
3. 選擇 hello 來源和目標位置中，選取 hello 適當的資料同步處理和 VM 建立選項。
4. 按一下**確定**按鈕 toostart hello 容錯回復程序。

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image10.png)

## <a name="best-practices"></a>最佳做法
### <a name="capacity-planning-and-readiness-assessment"></a>容量規劃和整備性評估
#### <a name="hyper-v-site"></a>Hyper-V 站台
使用 hello[使用者產能規劃工具](http://www.microsoft.com/download/details.aspx?id=39057)toodesign hello 伺服器、 儲存和 HYPER-V 複本環境的網路基礎結構。

#### <a name="azure"></a>Azure
您可以執行 hello [Azure 虛擬機器整備評估工具](http://azure.microsoft.com/downloads/vm-readiness-assessment/)上 Vm tooensure 它們的 Azure Vm 與 Azure Site Recovery Services 相容。 hello 整備評估工具會檢查 VM 組態，並設定不相容於 Azure 時，會發出警告。 例如，如果 C: 磁碟大小超過 127 GB，它就會提出警告。

容量規劃至少包含兩個重要程序：

* 對應內部部署 HYPER-V Vm tooAzure VM 大小 （例如 A6、 A7、 A8、 和 A9）。
* 判斷 hello 所需的網際網路頻寬。

## <a name="limitations"></a>限制
* 目前，只有 1 StorSimple 裝置可以容錯移轉 （tooa 單一 StorSimple 雲端應用裝置）。 尚未支援橫跨數個 StorSimple 裝置的檔案伺服器的 hello 案例。
* 如果您啟用 vm 保護時收到錯誤，請確定您已經中斷連線 hello iSCSI 目標。
* 分組在一起由於橫跨不同磁碟區容器的備份原則的所有 hello 磁碟區容器會一起都容錯移轉。
* 您已選擇 hello 磁碟區容器中的所有 hello 磁碟區的都容錯移轉。
* 加總 toomore，比 64 TB 無法容錯移轉，因為單一 StorSimple 雲端應用裝置 hello 最大容量是 64 TB 的磁碟區。
* 如果 hello 計劃/未規劃的容錯移轉失敗，且在 Azure 中建立 hello Vm，然後執行不清除 hello Vm。 請改為執行容錯回復。 如果您刪除 hello Vm 然後 hello 內部部署 Vm 不能設為一次。
* 容錯移轉之後，如果您不能 toosee hello 磁碟區，移 toohello Vm、 開啟磁碟管理、 重新掃描 hello 磁碟，然後使其連線。
* 在某些情況下，可能不同於 hello 字母內部 hello hello DR 網站中的磁碟機代號。 如果發生這種情況，您需要 toomanually 正確 hello 問題 hello 容錯移轉完成之後。
* Hello Azure hello 為資產的自動化帳戶中所輸入的認證必須停用多重要素驗證。 如果未停用此驗證，指令碼將不允許 toorun 自動和 hello 復原方案將會失敗。
* 容錯移轉工作逾時： hello StorSimple 指令碼將會逾時如果 hello 的磁碟區容器容錯移轉時間會比 hello Azure Site Recovery 限制每個指令碼 （目前為 120 分鐘）。
* 備份作業逾時： hello StorSimple 指令碼逾時，如果磁碟區的 hello 備份所花的時間會比 hello Azure Site Recovery 限制每個指令碼 （目前為 120 分鐘）。

  > [!IMPORTANT]
  > Hello Azure 入口網站手動執行 hello 備份，然後再次執行 hello 復原計劃。

* 複製工作逾時： hello StorSimple 指令碼逾時，如果 hello 複製的磁碟區花時間會比 hello Azure Site Recovery 限制每個指令碼 （目前為 120 分鐘）。
* 時間同步處理錯誤： hello StorSimple 指令碼錯誤指出 hello 備份不成功，即使 hello 備份成功 hello 入口網站中。 可能的原因，這可能是該 hello StorSimple 應用裝置的時間，可能會與 hello 同步 hello 時區中的目前時間。

  > [!IMPORTANT]
  > 同步處理 hello 應用裝置時間與 hello hello 時區中的目前時間。

* 應用裝置容錯移轉時發生錯誤： hello StorSimple 指令碼是否有應用裝置容錯移轉時正在執行 hello 復原計劃可能會失敗。

  > [!IMPORTANT]
  > Hello 應用裝置容錯移轉完成之後，請重新執行 hello 復原計劃。


## <a name="summary"></a>摘要
使用 Azure Site Recovery 時，您可以為有檔案共用裝載於 StorSimple 儲存體上的檔案伺服器 VM 建立完整自動化的災害復原計劃。 您可以從任何地方秒內起始 hello 容錯移轉在 hello 中斷的事件，並取得 hello 應用程式啟動並執行幾分鐘的時間。
