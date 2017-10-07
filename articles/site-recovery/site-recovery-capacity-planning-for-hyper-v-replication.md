---
title: "站台復原 aaaRun hello HYPER-V 產能規劃工具 |Microsoft 文件"
description: "本文說明如何 toorun hello Azure Site recovery 的 HYPER-V 產能規劃工具"
services: site-recovery
documentationcenter: na
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 2bc3832f-4d6e-458d-bf0c-f00567200ca0
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: b853598e5cd290c48b59794ba48eefc72ac8ded6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-hyper-v-capacity-planner-tool-for-site-recovery"></a>執行站台復原的 hello HYPER-V 產能規劃工具

Azure Site Recovery 部署的一部分，您需要 toofigure 出您的複寫和頻寬需求。 站台復原的 hello HYPER-V 產能規劃工具可協助您 toodo，HYPER-V 虛擬機器複寫。

本文說明如何 toorun hello HYPER-V 產能規劃工具。 應使用此工具，連同中的 hello 資訊[的容量規劃站台復原](site-recovery-capacity-planner.md)。

## <a name="before-you-start"></a>開始之前
您在主要站台中 HYPER-V 伺服器或叢集節點上執行 hello 工具。 toorun hello 工具 hello HYPER-V 主機伺服器必須：

* 作業系統︰Windows Server 2012 或 2012 R2
* 記憶體：20 MB (最低要求)
* CPU：5% 額外負荷 (最低要求)
* 磁碟空間：5 MB (最低要求)

執行 hello 工具之前，您會需要 tooprepare hello 主要站台。 如果您要複寫之間兩個內部部署網站和您想要 toocheck 頻寬，您需要 tooprepare 複本伺服器。

## <a name="step-1-prepare-hello-primary-site"></a>步驟 1： 準備 hello 主要站台

1. Hello 主要站台上進行所有 hello 您想要的 HYPER-V Vm 的清單，tooreplicate 和 hello HYPER-V 主機/叢集是。 hello 工具可在多個獨立的主機，或單一叢集，但不可兩者同時執行。 它也需要 toorun 分別針對每個作業系統，因此您應該收集 HYPER-V 伺服器的相關資訊，如下所示：

   * Windows Server 2012 獨立伺服器
   * Windows Server 2012 叢集
   * Windows Server 2012 R2 獨立伺服器
   * Windows Server 2012 R2 叢集
2. 啟用遠端存取 tooWMI 所有 hello 與 HYPER-V 主機與叢集上。 每個伺服器/叢集上執行此命令，確定防火牆規則 toomake 與使用者權限設定：

        netsh firewall set service RemoteAdmin enable
3. 在伺服器和叢集上啟用效能監視，如下所示：

   * 開啟 hello Windows 防火牆以 hello**進階安全性**嵌入式管理單元，然後啟用 hello 下列輸入規則和： **COM + 網路存取 (DCOM IN)** hello 中的所有規則和**遠端事件記錄檔管理群組**。

## <a name="step-2-prepare-a-replica-server-on-premises-tooon-premises-replication"></a>步驟 2： 準備複本伺服器 （在內部部署 tooon 內部部署複寫）
您不需要 toodo 這如果您要複寫 tooAzure。

我們建議您使用單一的 HYPER-V 主機設定為復原伺服器，讓 dummy VM 可能會與複寫的 tooit toocheck 頻寬。  您可以略過此步驟，但除非您這樣做，您將無法能 toomeasure 頻寬。

1. 如果您想 toouse hello 複本叢集節點設定 HYPER-V 複本代理人：

   * 在 [伺服器管理員] 中，開啟 [容錯移轉叢集管理員]。
   * Toohello 叢集連線，反白顯示 hello 叢集名稱，然後按一下**動作** > **設定角色**tooopen hello 高可用性精靈 」。
   * 在 [選取角色] 中，選取 [Hyper-V 複本代理人]。 Hello 精靈中提供**NetBIOS 名稱**和 hello **IP 位址**toobe 做為 hello 連接點 toohello 叢集 （稱為用戶端存取點）。 hello **HYPER-V 複本代理人**會設定，導致您應該會注意到用戶端存取點名稱。
   * 請確認該 hello HYPER-V 複本代理人角色順利連線，且可以 hello 叢集的所有節點之間容錯移轉。 toodo，hello 角色上按一下滑鼠右鍵，指向太**移動**，然後按一下**選取節點**。 選取節點 > [確定]。
   * 如果您使用憑證式驗證，請確定每個叢集節點，然後 hello 所有已安裝的 hello 憑證的用戶端存取點。
2. 啟用複本伺服器：

   * 叢集開啟失敗叢集管理員]，連接 toohello 叢集，按一下 [**角色**> 選取角色 >**複寫設定** > **啟用此叢集做為複本伺服器**。 如果您使用叢集作為 hello 複本時，您會需要 toohave hello HYPER-V 複本代理人角色以及 hello 主要網站中的 hello 叢集上。
   * 若是獨立伺服器，請開啟 [Hyper-V 管理員]。 在 hello**動作**] 窗格中，按一下 [ **HYPER-V 設定**hello 伺服器要 tooenable，然後在**複寫組態**按一下**啟用此功能做為複本伺服器的電腦**。
3. 設定驗證：

   * 在**驗證與連接埠**，選取 tooauthenticate hello 主要伺服器與 hello 驗證連接埠的方式。 如果您使用憑證按一下**選取憑證**tooselect 其中一個。 使用 Kerberos hello hello 主要和復原 HYPER-V 主機是否相同的網域或信任網域中。 針對不同的網域或工作群組部署使用憑證。
   * 在**授權與存放裝置**，允許**任何**驗證 （主要） 伺服器 toosend 複寫資料 toothis 複本伺服器。

     ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image1.png)
   * 執行**netsh http show servicestate**，toocheck 該 hello 接聽程式正在執行的 hello 通訊協定/您指定連接埠：  
4. 設定防火牆： HYPER-V 在安裝期間，會建立防火牆規則 tooallow 流量 hello 預設連接埠 （443 上 HTTPS，Kerberos 上 80） 上。 啟用這些規則，如下所示：
  - 叢集 (443) 上的憑證驗證：``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"}}``
  - 叢集 (80) 上的 Kerberos 驗證︰``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"}}``
  - 獨立伺服器上的憑證驗證︰``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"``
  - 獨立伺服器上的 Kerberos 驗證︰``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"``

## <a name="step-3-run-hello-capacity-planner-tool"></a>步驟 3： 執行 hello 產能規劃工具
當您準備好您的主要站台，並設定復原伺服器之後，您可以執行 hello 工具。

1. [下載](https://www.microsoft.com/download/details.aspx?id=39057)hello 工具，從 Microsoft 下載中心 hello。
2. 執行 hello 工具，從一個 hello 主要伺服器 （或 hello hello 主要叢集中節點的其中一個）。 Hello.exe 檔，以滑鼠右鍵按一下，然後選擇 **系統管理員身分執行**。
3. 在**開始之前**，指定您想要多久 toocollect 資料。 我們建議您在實際執行小時 tooensure 資料是代表執行 hello 工具。 如果您只想要 toovalidate 網路連線，您可以為一分鐘只進行收集。

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image2.png)
4. 在**主要站台的詳細資料**、 指定獨立主機，hello 伺服器名稱或 FQDN，或叢集指定 hello hello 用戶端的 FQDN 接受點、 叢集名稱或在 hello 叢集中任何節點，然後再按一下**下一步**. hello 工具會自動偵測 hello hello 執行的伺服器名稱。 可以監視的 Vm hello 工具拾取 hello 指定的伺服器。

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image3.png)
5. 在**複本網站詳細資料**，如果您要複寫 tooAzure，或如果您要複寫 tooa 次要資料中心，而且您尚未設定複本伺服器，選取**略過測試牽涉到複本站台**。 如果您要複寫 tooa 次要資料中心，當您設定複本類型輸入 hello 獨立伺服器或 hello 用戶端存取點的 FQDN hello 叢集**伺服器名稱 （或） HYPER-V 複本代理人 CAP**。

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image4.png)
6. 在**延伸複本詳細資料**，啟用**略過 hello 測試涉及擴充複本站台**。 這些測試不受 Site Recovery 支援。
7. 在**選擇 Vm tooReplicate**、 hello 工具連線 toohello 伺服器或叢集，並顯示 Vm 和 hello 主要伺服器上執行的磁碟，根據 hello 設定您在上指定 hello**主要站台的詳細資料**頁面。 已針對複寫啟用 VM，不會顯示未執行的項目。 選取您想要的 toocollect 度量 hello Vm。 自動選取 hello Vhd 太收集 hello Vm 的資料。
8. 如果您已設定複本伺服器或叢集，在**網路資訊**，指定將 hello 主要和複本站台，以及選取 hello 憑證之間使用近似 hello 您認為 WAN 頻寬，如果您已設定憑證驗證。

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image5.png)
9. 在**摘要**，檢查 hello 設定，然後按一下**下一步**toobegin 收集度量。 工具的進度和狀態會顯示在 hello**計算容量**頁面。 當 hello 工具完成執行時，按一下 **檢視報告**tooview hello 輸出。 根據預設，報告和記錄檔會儲存在 **%systemdrive%\Users\Public\Documents\Capacity Planner**。

   ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image6.png)

## <a name="step-4-interpret-hello-results"></a>步驟 4： 解譯 hello 結果

以下是 hello 重要的指標。 您可以忽略未列在這裡的度量。 它們與 Site Recovery 不相關。

### <a name="on-premises-tooon-premises-replication"></a>在內部部署 tooon 內部部署複寫

* Hello 主要主機的計算，記憶體上複寫的影響
* 複寫 hello 的主要修復主機的存放磁碟空間，，IOPS 的影響
* 差異複寫所需的總頻寬 (Mbps)
* Hello 主要主機與 hello 復原主機 (Mbps) 之間的觀察到的網路頻寬
* 使用中的平行傳輸 hello 兩個主機/叢集之間的 hello 理想數目的建議

### <a name="on-premises-tooazure-replication"></a>在內部部署 tooAzure 複寫

* Hello 主要主機的計算，記憶體上複寫的影響
* 複寫 hello 主要主機的存放磁碟空間，IOPS 的影響
* 差異複寫所需的總頻寬 (Mbps)

## <a name="more-resources"></a>其他資源
* 如需 hello 工具的詳細資訊，讀取隨附 hello 工具下載 hello 文件。
* 觀看 hello 工具在 Keith Mayer 的逐步解說[TechNet 部落格](http://blogs.technet.com/b/keithmayer/archive/2014/02/27/guided-hands-on-lab-capacity-planner-for-windows-server-2012-hyper-v-replica.aspx)。
* [取得 hello 結果](site-recovery-performance-and-scaling-testing-on-premises-to-on-premises.md)我們效能測試在內部部署 tooon 內部部署 HYPER-V 複寫

## <a name="next-steps"></a>後續步驟

容量規劃完成之後，您就可以開始部署 Site Recovery：

* [在 VMM 雲端 tooAzure 複寫 HYPER-V Vm](site-recovery-vmm-to-azure.md)
* [複寫 （無 VMM) 的 HYPER-V Vm tooAzure](site-recovery-hyper-v-site-to-azure.md)
* [在 VMM 站台間複寫 Hyper-V VM](site-recovery-vmm-to-vmm.md)
