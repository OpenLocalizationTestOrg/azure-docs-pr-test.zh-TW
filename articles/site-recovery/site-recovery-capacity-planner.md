---
title: "在 Azure 中的 aaaEstimate 複寫容量 |Microsoft 文件"
description: "當複寫與 Azure Site Recovery 時使用此發行項 tooestimate 容量"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: 54d10e50dd4fc1b875273c7fc0f38f0e85dadddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="plan-capacity-for-protecting-virtual-machines-and-physical-servers-in-azure-site-recovery"></a>針對 Azure Site Recovery 中的虛擬機器和實體伺服器保護規劃容量

hello Azure 站台復原容量規劃工具可協助您 toofigure 出容量需求複寫 HYPER-V Vm、 VMware Vm 及 Windows/Linux 實體伺服器，使用 Azure Site Recovery 時。

使用您的來源環境和工作負載的 hello 站台復原容量規劃 tooanalyze、 估計頻寬需求和伺服器資源所需的 hello 來源位置，以及您需要在 hello 目標中的 hello 資源 （虛擬機器和存放裝置等等），位置。

您可以透過幾種模式來執行 hello 工具：

* **快速規劃**: hello 工具以此模式執行的 tooget 網路和伺服器投影根據 Vm、 磁碟、 存放裝置和變更速率平均數目。
* **詳細的規劃**： 在此模式中，執行 hello 工具，並提供每個工作負載在 VM 層級的詳細資料。 分析 VM 相容性，並取得網路和伺服器預測。

## <a name="before-you-start"></a>開始之前


1. 收集您的環境的資訊，包括 VM、每個 VM 的磁碟、每個磁碟的儲存體。
2. 識別複寫資料的每日變更 (流失) 率。 toodo 這樣：

   * 如果您要複寫 HYPER-V Vm，然後下載 hello [HYPER-V 容量規劃工具](https://www.microsoft.com/download/details.aspx?id=39057)tooget hello 變更率。 [深入了解](site-recovery-capacity-planning-for-hyper-v-replication.md) 此工具。 我們建議您執行此工具透過週 toocapture 平均值。
   * 如果您要複寫的 VMware 虛擬機器，請使用 hello [Azure 站台復原部署規劃](./site-recovery-deployment-planner.md)出 hello toofigure 變換率。
   * 如果您要複寫的實體伺服器，您需要 tooestimate 手動。

## <a name="run-hello-quick-planner"></a>執行快速的計劃者 hello
1. 下載並開啟 hello [Azure 站台復原容量規劃](http://aka.ms/asr-capacity-planner-excel)工具。 您需要 toorun 巨集，因此選取 tooenable 編輯和啟用內容出現提示時。
2. 在**選取規劃類型**選取**快速的計劃者**hello 清單方塊中。

   ![開始使用](./media/site-recovery-capacity-planner/getting-started.png)
3. 在 hello**容量規劃**工作表中，輸入 hello 所需的資訊。 您必須填寫所有 hello 欄位 hello 以下螢幕擷取畫面中以紅色圈起來。

   * 在**選取您的案例**，選擇**HYPER-V tooAzure**或**VMware/實體 tooAzure**。
   * 在**平均每日資料變更速率 （%）**，置於您收集使用 hello 的 hello 資訊[HYPER-V 容量規劃工具](site-recovery-capacity-planning-for-hyper-v-replication.md)或 hello [Azure 站台復原部署規劃](./site-recovery-deployment-planner.md).  
   * **壓縮**只適用於 toocompression 複寫 VMware Vm 或實體伺服器 tooAzure 時提供。 我們的估計 30%或更多，但是可以修改 hello 所需的設定。 複寫 HYPER-V Vm tooAzure 壓縮，您可以使用第三方應用裝置，例如 Riverbed。
   * 在 [保留期輸入] 中，指定保留複本的時間長度。 如果您要在 VMware 或實體伺服器複寫，請以天為單位輸入 hello 值。 如果您要複寫 HYPER-V，請以小時為單位指定 hello 時間。
   * 在**應該完成的時數的初始複寫的虛擬機器的 hello 批次**和**的每個初始複寫的批次的虛擬機器數目**，輸入所使用的設定toocompute 初始複寫的需求。  部署站台復原時，應該上傳 hello 整個初始資料集。

   ![輸入](./media/site-recovery-capacity-planner/inputs.png)
4. 您已將它放在 hello 來源環境的 hello 值之後，顯示的輸出將包括：

   * **差異複寫所需的頻寬** (MB/秒)。 差異複寫的網路頻寬被計算 hello 平均每日資料變更速率。
   * **初始複寫所需的頻寬** (MB/秒)。 您將放在 hello 初始複寫值會計算針對初始複寫的網路頻寬。
   * **（以 gb 為單位） 所需儲存體**是 hello 總 Azure 儲存體所需。
   * **在標準儲存體帳戶的總 IOPS**根據 hello 總計的標準儲存體帳戶在 8 千個 IOPS 單位的大小計算。  Hello 快速的計劃，hello 數目會根據計算所有 hello 來源 Vm 磁碟和每日資料變更速率。 如 hello 詳細的規劃、 hello 值為導出根據的總數的對應的 toostandard Azure Vm 的 Vm，資料變更率在那些 Vm 上。
   * **標準儲存體帳戶數目**hello Vm 提供的標準儲存體帳戶所需 tooprotect hello 總數。 標準儲存體帳戶在標準儲存體中的所有 hello Vm 之間，可以保存向上 too20000 IOPS 和 500 的 IOPS 的最多可支援每個磁碟。
   * **Blob 所需的磁碟數目**提供 hello 會在 Azure 儲存體中建立的磁碟數目。
   * **Premium 儲存體帳戶所需數目**hello Vm 提供的進階儲存體帳戶所需 tooprotect hello 總數。 具有高 IOPS (超過 20000) 的來源 VM 需要進階儲存體帳戶。 進階儲存體帳戶可以阻擋 too80000 IOPS。
   * **高階儲存體的總 IOPS**根據 hello 總進階儲存體帳戶上 256 K IOPS 單位的大小計算。  Hello 快速的計劃，hello 數目會根據計算所有 hello 來源 Vm 磁碟和每日資料變更速率。 如 hello 詳細的規劃、 hello 值為根據的導出的 hello 總數的對應的 toopremium Azure VM （DS 與 GS 系列） Vm，hello 資料變更率在那些 Vm 上。
   * **設定所需的伺服器數目**顯示多少設定伺服器部署所需 hello。
   * **所需的額外的處理序伺服器數目**顯示額外的處理序伺服器是否需要在 hello 組態伺服器執行預設的加法 toohello 處理序伺服器。
   * **100 %hello 來源上的其他儲存體**顯示 hello 來源位置中是否需要額外的存放裝置。

   ![輸出](./media/site-recovery-capacity-planner/output.png)

## <a name="run-hello-detailed-planner"></a>執行 hello 詳細的規劃

1. 下載並開啟 hello [Azure 站台復原容量規劃](http://aka.ms/asr-capacity-planner-excel)工具。 您需要 toorun 巨集，因此選取 tooenable 編輯和啟用內容出現提示時。
2. 在**選取規劃類型**，選取**詳細規劃**hello 清單方塊中。

   ![開始使用](./media/site-recovery-capacity-planner/getting-started-2.png)
3. 在 hello**工作負載限定性條件**工作表中，輸入 hello 所需的資訊。 您必須填寫所有欄位標記的 hello。

   * 在**處理器核心**，來源伺服器上指定 hello 的核心數總計。
   * 在**以 mb 為單位的記憶體配置**，hello RAM 大小指定為來源伺服器。
   * hello**的 Nic 數目**，指定來源伺服器上的網路介面卡的 hello 數目。
   * 在**總計 （以 gb 為單位） 的儲存體**，指定 hello hello VM 儲存體的大小總計。 比方說，如果 hello 來源伺服器有 3 個磁碟具有 500 GB，然後總儲存體大小是 1500 GB。
   * 在**連接的磁碟數目**，指定的來源伺服器的磁碟 hello 總數。
   * 在**磁碟容量使用率**，指定 hello 平均使用率。
   * 在**每日變更速率 （%）**，指定 hello 每日資料變更率的來源伺服器。
   * 在**對應 Azure 大小**，輸入您想 toomap hello Azure VM 大小。 如果您不要 toodo 此以手動方式，請按一下**計算 IaaS Vm**。如果您輸入的手動設定，然後按一下計算 IaaS Vm，因為 hello 計算程序會自動識別 hello Azure VM 大小的最符合項目可能會覆寫 hello 手動設定。

   ![工作負載限定性條件](./media/site-recovery-capacity-planner/workload-qualification.png)
4. 如果您按一下 [計算 IaaS VM]  ，它會執行動作如下：

   * 驗證 hello 必要輸入。
   * 計算 IOPS，並建議 hello 最佳的 Azure VM aize 適用於複寫 tooAzure 相符的每個 Vm。 如果無法偵測適當的 Azure VM 大小，則會發出錯誤。 例如，如果 hello 磁碟數目以 65，發出錯誤因為 Azure VM hello 最大大小為 64。
   * 建議可用於 Azure VM 的儲存體帳戶。
   * 計算 hello 的標準儲存體帳戶和 hello 工作負載所需的進階儲存體帳戶的總數目。 捲動 tooview hello Azure 儲存體類型和可用的來源伺服器的 hello 儲存體帳戶。
   * 完成，並排序 hello 其餘 hello 必要的儲存體類型 （standard 或 premium） 指派給 VM，並連接磁碟的 hello 數目為基礎的資料表。 對於所有 Vm 符合 Azure 的 hello 需求，hello 資料行**限定是 VM？**顯示**是**。 如果 VM 無法備份 tooAzure，會顯示錯誤。

資料行 AA tooAE 輸出，且可以提供每個 VM 的資訊。

![工作負載限定性條件](./media/site-recovery-capacity-planner/workload-qualification-2.png)

### <a name="example"></a>範例
做為六個 Vm hello 值 hello 表所示的範例，hello 工具會計算，並指派 hello 最佳的 Azure VM 比對和 hello Azure 儲存體需求。

![工作負載限定性條件](./media/site-recovery-capacity-planner/workload-qualification-3.png)

* 在 hello 範例輸出，請注意下列 hello:

  * hello 第一個資料行是 hello Vm、 磁碟和變換的驗證資料行。
  * 五個 VM 需要兩個標準儲存體帳戶和一個進階儲存體帳戶。
  * VM3 不適合保護，因為一或多個磁碟超過 1 TB。
  * VM1 和 vm2 的情況，則可以使用 hello 第一個標準儲存體帳戶
  * VM4 可以使用 hello 第二個標準儲存體帳戶。
  * VM5 和 VM6 需要進階儲存體帳戶，兩者都可以使用單一帳戶。

    > [!NOTE]
    > 在標準和進階儲存體 IOPS 會計算在 hello VM 層級，而不是在磁碟層級。 標準的虛擬機器可以處理向上 too500 每個磁碟的 IOPS。 如果磁碟的 IOPS 大於 500，則您需要進階儲存體。 不過，如果磁碟的 IOPS 超過 500，但是 IOPS hello 總計 VM 磁碟是 hello 內支援標準 Azure VM 限制 （VM 大小，配接器，CPU、 記憶體數量的磁碟數目），然後 hello 規劃會挑選 standard VM 和不 hello DS 或 GS 系列。 您必須具有適當 DS 或 GS 系列 VM 的 toomanually 更新 hello 對應 Azure 大小儲存格。


所有 hello 詳細資料都已就緒之後，請按一下**提交資料 toohello 規劃工具**tooopen hello**容量規劃**工作負載都會反白顯示，tooshow 無論或不是可進行保護。

### <a name="submit-data-in-hello-capacity-planner"></a>送出 hello 容量規劃中的資料
1. 當您開啟 hello**容量規劃**擴展工作表會根據您所指定的 hello 設定。 hello 的 word 「 工作負載 」 會出現在 hello**紅外線輸入來源**資料格，hello 輸入的 tooshow 為 hello**工作負載限定性條件**工作表。
2. 如果您想 toomake 變更時，您需要 toomodify hello**工作負載限定性條件**工作表，然後按一下**提交資料 toohello 規劃工具**一次。  

   ![容量規劃](./media/site-recovery-capacity-planner/capacity-planner.png)
