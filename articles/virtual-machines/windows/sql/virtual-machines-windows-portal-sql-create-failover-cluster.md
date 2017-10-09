---
title: "aaaSQL Server FCI 的 Azure 虛擬機器 |Microsoft 文件"
description: "這篇文章說明如何 toocreate SQL Server 容錯移轉叢集執行個體的 Azure 虛擬機器上。"
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a>在 Azure 虛擬機器上設定 SQL Server 容錯移轉叢集執行個體

這篇文章說明如何 toocreate SQL Server 容錯移轉叢集執行個體 (FCI) 資源管理員模型中的 Azure 虛擬機器上。 這個解決方案會使用[儲存空間直接存取 Windows Server 2016 Datacenter edition \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)以軟體為基礎的虛擬 SAN，同步處理之間 hello 節點 (Azure Vm) 中的 hello 儲存體 （資料磁碟）Windows 叢集。 S2D 是 Windows Server 2016 中的新功能。

hello 下圖顯示 hello 完整解決方案 Azure 虛擬機器上：

![可用性群組](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

上述圖表會顯示 hello:

- 兩部位於 Windows 容錯移轉叢集中的 Azure 虛擬機器。 位於容錯移轉叢集中的虛擬機器也稱為「叢集節點」或「節點」。
- 每部虛擬機器有兩個以上的資料磁碟。
- S2D hello hello 資料磁碟上的資料同步處理，並顯示 hello 同步處理儲存體與儲存體集區。
- hello 存放集區提供叢集共用磁碟區 (CSV) toohello 容錯移轉叢集。
- hello SQL Server FCI 的叢集角色會使用 hello CSV hello 資料磁碟機。
- Azure 負載平衡器 toohold hello IP 位址 hello SQL Server FCI。
- Azure 可用性設定組保存 hello 的所有資源。

   >[!NOTE]
   >所有的 Azure 資源都在 hello 圖表 hello 中相同的資源群組。

如需有關 S2D 的詳細資料，請參閱 [Windows Server 2016 Datacenter 版本儲存空間直接存取 \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)。

S2D 支援兩種類型的架構 - 交集和超交集。 本文件中的 hello 架構是超聚合。 上的超聚合式基礎結構上的芳鄰 hello 儲存體 hello 該主機叢集的 hello 應用程式的相同的伺服器。 在這種架構，hello 儲存體是每個 SQL Server FCI 節點上。

### <a name="example-azure-template"></a>Azure 範本範例

從範本，您可以在 Azure 中建立 hello 整個方案。 範本的範例可用於 hello GitHub [Azure 快速入門範本](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad)。 此範例並非為任何特定工作負載而設計或測試。 您可以使用 S2D 儲存體連接的 tooyour 網域執行 hello 範本 toocreate SQL Server FCI。 您可以評估 hello 範本，並修改您的目的。

## <a name="before-you-begin"></a>開始之前

有幾件事，您需要 tooknow 和幾個事項您備妥後再繼續。

### <a name="what-tooknow"></a>哪些 tooknow
您應該了解 operational hello 下列技術：

- [Windows 叢集技術](http://technet.microsoft.com/library/hh831579.aspx)
-  [SQL Server 容錯移轉叢集執行個體](http://msdn.microsoft.com/library/ms189134.aspx)。

此外，您應該有基本認識的 hello 下列技術：

- [在 Windows Server 2016 中使用儲存空間直接存取的超交集解決方案](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [Azure 資源群組](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a>哪些 toohave

這篇文章中的 hello 指示之前，您應該已經有：

- Microsoft Azure 訂用帳戶。
- Azure 虛擬機器上的 Windows 網域。
- 具有權限 toocreate 物件 hello Azure 虛擬機器中的帳戶。
- Azure 虛擬網路和子網路具有足夠的 IP 位址空間，來 hello 下列元件：
   - 兩部虛擬機器。
   - hello 容錯移轉叢集 IP 位址。
   - 每個 FCI 上一個 IP 位址。
- Hello Azure 網路，指向 toohello 網域控制站上設定的 DNS。

備妥這些先決條件後，便可繼續建置您的容錯移轉叢集。 hello 第一個步驟是 toocreate hello 虛擬機器。

## <a name="step-1-create-virtual-machines"></a>步驟 1：建立虛擬機器

1. 登入 toohello [Azure 入口網站](http://portal.azure.com)與您的訂用帳戶。

1. [建立 Azure 可用性設定組](../tutorial-availability-sets.md)。

   hello 可用性設定虛擬機器群組橫跨容錯網域和更新網域。 hello 可用性設定組可確保您的應用程式不受到單一失敗點，像是 hello 網路交換器或是伺服器機架的 hello 電源裝置。

   如果您尚未建立虛擬機器 hello 資源群組，請在您建立 Azure 可用性設定組時執行動作。 如果您使用 hello Azure 入口網站 toocreate hello 可用性設定組，下列步驟 hello:

   - 在 hello Azure 入口網站，按一下   **+**  tooopen hello Azure Marketplace。 搜尋 [可用性設定組]。
   - 按一下 [可用性設定組]。
   - 按一下 [建立] 。
   - 在 hello**建立可用性設定組**刀鋒視窗中，設定下列值的 hello:
      - **名稱**: hello 可用性設定組的名稱。
      - **訂用帳戶**：您的 Azure 訂用帳戶。
      - **資源群組**： 如果您想 toouse 現有的群組，請按一下**使用現有**和從 hello 下拉式清單選取 hello 群組。 否則選擇**新建**輸入 hello 群組的名稱。
      - **位置**： 將您計劃 toocreate hello 位置設定您的虛擬機器。
      - **故障網域**： 使用 hello 預設 (3)。
      - **更新網域**： 使用 hello 預設 (5)。
   - 按一下**建立**toocreate hello 可用性設定組。

1. Hello 中建立虛擬機器 hello 可用性設定組。

   佈建 hello Azure 可用性設定組中的兩個 SQL Server 虛擬機器。 如需指示，請參閱[hello Azure 入口網站中的 SQL Server 虛擬機器佈建](virtual-machines-windows-portal-sql-server-provision.md)。

   將兩部虛擬機器放置於：

   - 在 hello 您的可用性設定組的相同 Azure 資源群組內。
   - 在 hello 相同網路為您的網域控制站。
   - 有足夠 IP 位址空間存放兩部虛擬機器，與最終會用於此叢集的所有 FCI 的子網路上。
   - 在 hello Azure 可用性設定組。   

      >[!IMPORTANT]
      >建立虛擬機器後，您無法設定或變更可用性設定組。

   選擇從 hello Azure Marketplace 的映像。 您可以使用 Marketplace 映像，包括 Windows Server 和 SQL Server 或只是 hello Windows 伺服器。 如需詳細資料，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](../../virtual-machines-windows-sql-server-iaas-overview.md)

   hello 官方 SQL Server 映像 hello Azure 圖庫中的包含已安裝的 SQL Server 執行個體，再加上 hello SQL Server 安裝軟體和 hello 必要索引鍵。

   選擇 hello 右側的影像，根據您想要的 toohow toopay hello 的 SQL Server 授權：

   - **支付每使用量授權**: hello 每分鐘費用這些映像包括 hello SQL Server 授權：
      - **Windows Server Datacenter 2016 上的 SQL Server 2016 Enterprise 版本**
      - **Windows Server Datacenter 2016 上的 SQL Server 2016 Standard 版本**
      - **Windows Server Datacenter 2016 上的 SQL Server 2016 Developer 版本**

   - **自備授權 (BYOL)**

      - **{BYOL} Windows Server Datacenter 2016 上的 SQL Server 2016 Enterprise 版本**
      - **{BYOL} Windows Server Datacenter 2016 上的 SQL Server 2016 Standard 版本**

   >[!IMPORTANT]
   >建立 hello 虛擬機器之後，移除 hello 單獨預先安裝的 SQL Server 執行個體。 設定 hello 容錯移轉叢集和 S2D 之後，您將使用 hello 預先安裝的 SQL Server 媒體 toocreate hello SQL Server FCI。

   或者，您可以使用 Azure Marketplace 映像只 hello 作業系統。 選擇**Windows Server 2016 Datacenter**映像和安裝 SQL Server FCI hello 設定 hello 容錯移轉叢集和 S2D 之後。 此映像不包含 SQL Server 安裝媒體。 將 hello 安裝媒體放在您可以在其中執行 hello SQL Server 安裝的每一部伺服器的位置。

1. Azure 建立虛擬機器之後，請使用 RDP 連線 tooeach 虛擬機器。

   當您第一次使用 RDP 連線 tooa 虛擬機器時，hello 電腦詢問您是否 tooallow 此 PC toobe hello 網路上可探索。 按一下 [是] 。

1. 如果您使用其中一個 hello SQL Server 為基礎的虛擬機器映像，移除 hello SQL Server 執行個體。

   - 在 [程式和功能] 中，以滑鼠右鍵按一下 [Microsoft SQL Server 2016 (64 位元)] 然後按一下 [解除安裝/變更]。
   - 按一下 [移除] 。
   - 選取 hello 預設執行個體。
   - 移除所有在 [Database Engine 服務] 下的功能。 請勿移除 [共用功能]。 請參閱下列圖片的 hello:

      ![移除功能](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - 按一下 下一步，然後按一下移除。

1. <a name="ports"></a>開啟 hello 防火牆連接埠。

   每個虛擬機器上，開啟下列連接埠上的 Windows 防火牆 hello hello。

   | 目的 | TCP 連接埠 | 注意事項
   | ------ | ------ | ------
   | SQL Server | 1433 | 適用於 SDL Server 預設執行個體的一般連接埠。 如果您使用映像從 hello 組件庫時，會自動開啟此連接埠。
   | 健全狀況探查 | 59999 | 任何開啟的 TCP 連接埠。 在稍後步驟中，設定 hello 負載平衡器[健全狀況探查](#probe)和 hello 叢集 toouse 此連接埠。  

1. 新增儲存體 toohello 虛擬機器。 如需詳細資訊，請參閱[新增儲存區](../../../storage/common/storage-premium-storage.md)。

   每部虛擬機器需要至少兩個資料磁碟。

   連接原始磁碟 - 非 NTFS 格式的磁碟。
      >[!NOTE]
      >若您連接 NTFS 格式的磁碟，您只能啟用 S2D 而無法進行磁碟適用性檢查。  

   將附加兩個 Premium 儲存體 （SSD 磁碟） tooeach VM 的最小值。 建議使用 P30 (1 TB) 或以上的磁碟。

   設定主機快取太**唯讀**。

   您在實際執行環境中使用的 hello 儲存容量取決於您的工作負載。 本文中所述的 hello 值是展示和測試。

1. [新增 hello 虛擬機器 tooyour 預先存在的網域](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain)。

Hello 虛擬機器所建立及設定之後，您可以設定 hello 容錯移轉叢集。

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a>步驟 2： 設定 S2D hello Windows 容錯移轉叢集

hello 下一個步驟是與 S2D tooconfigure hello 容錯移轉叢集。 在此步驟中，您要執行 hello 下列子步驟：

1. 新增 Windows 容錯移轉叢集功能
1. 驗證 hello 叢集
1. 建立 hello 容錯移轉叢集
1. 建立 hello 雲端見證
1. 新增儲存體

### <a name="add-windows-failover-clustering-feature"></a>新增 Windows 容錯移轉叢集功能

1. toobegin，與使用網域帳戶屬於本機系統管理員，且具有權限 toocreate 物件在 Active Directory 中的 RDP 連接 toohello 第一部虛擬機器。 此帳戶用於 hello 其他 hello 組態。

1. [將容錯移轉叢集功能 tooeach 虛擬機器加入](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms)。

   hello tooinstall hello UI 中，從容錯移轉叢集功能，下列步驟在兩部虛擬機器上。
   - 在 伺服器管理員 中，按一下 管理，然後按一下新增角色及功能。
   - 在**新增角色及功能精靈**，按一下 **下一步**直到太**選取功能**。
   - 在 [選取功能] 中，按一下 [容錯移轉叢集]。 包含所有必要的功能和 hello 管理工具。 按一下 [新增功能]。
   - 按一下**下一步**，然後按一下**完成**tooinstall hello 功能。

   tooinstall hello 容錯移轉叢集功能使用 PowerShell，執行下列其中一個 hello 虛擬機器上從系統管理員 PowerShell 工作階段的指令碼的 hello。

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

供參考，hello 接下來的步驟會遵循底下的步驟 3 的 hello 指示[使用儲存空間直接存取 Windows Server 2016 中的超聚合式方案](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct)。

### <a name="validate-hello-cluster"></a>驗證 hello 叢集

本指南是指在 tooinstructions[驗證叢集](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation)。

驗證 hello 叢集在 hello UI 或 PowerShell。

toovalidate hello 叢集以 hello UI，請勿 hello 其中 hello 虛擬機器中的下列步驟。

1. 在 [伺服器管理員] 中，按一下 [工具]，然後按一下 [容錯移轉叢集管理員]。
1. 在 [容錯移轉叢集管理員] 中，按一下 [動作]，然後按一下 [驗證設定...]。
1. 按一下 [下一步] 。
1. 在**選取伺服器或叢集**，型別 hello 兩部虛擬機器名稱。
1. 在 [測試選項] 中，選擇 [僅執行我選取的測試]。 按一下 [下一步] 。
1. 在 [測試選取範圍] 中，選取**儲存體**以外的所有測試。 請參閱下列圖片的 hello:

   ![驗證測試](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. 按一下 [下一步] 。
1. 在 [確認] 中，，按一下 [下一步]。

hello**驗證設定精靈**執行 hello 驗證測試。

使用 PowerShell，執行下列其中一個 hello 虛擬機器上從系統管理員 PowerShell 工作階段的指令碼的 hello toovalidate hello 叢集。

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

驗證 hello 叢集後，請建立 hello 容錯移轉叢集。

### <a name="create-hello-failover-cluster"></a>建立 hello 容錯移轉叢集

本指南是指太[建立 hello 容錯移轉叢集](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster)。

toocreate hello 容錯移轉叢集，您必須：
- hello hello 變成 hello 叢集節點的虛擬機器名稱。
- Hello 容錯移轉叢集的名稱
- Hello 容錯移轉叢集的 IP 位址。 您可以使用 hello 未使用的 IP 位址相同 Azure 虛擬網路和子網路為 hello 叢集節點。

hello 遵循 PowerShell 建立容錯移轉叢集。 更新 hello hello 名稱 hello 節點 （hello 虛擬機器名稱） 的指令碼和 hello Azure VNET 中可用的 IP 位址：

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a>建立雲端見證

雲端見證儲存在 Azure 儲存體 Blob 中，是一種新型的叢集仲裁見證。 這會移除 hello 需要個別的虛擬機器裝載見證共用。

1. [建立雲端 hello 容錯移轉叢集的見證](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness)。

1. 建立 Blob 容器。

1. 儲存 hello 存取金鑰，然後 hello 容器 URL。

1. 設定 hello 容錯移轉叢集的叢集仲裁見證。 請參閱，[設定 hello 仲裁見證 hello 使用者介面中的]。(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) hello UI 中。

### <a name="add-storage"></a>新增儲存體

S2D hello 磁碟需要 toobe 空白，且不含資料分割或其他資料。 請依照下列 tooclean 磁碟[本指南中步驟的 hello](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks)。

1. [啟用儲存空間直接存取 \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct)。

   下列 PowerShell hello 可讓儲存空間 direct。  

   ```PowerShell
   Enable-ClusterS2D
   ```

   在**容錯移轉叢集管理員**，您現在可以看到 hello 存放集區。

1. [建立磁碟區](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes)。

   S2D hello 功能之一是它會自動建立儲存集區，當您啟用它。 現在您已經準備就緒 toocreate 磁碟區。 hello PowerShell commandlet`New-Volume`自動化 hello 磁碟區建立程序，包括格式、 新增 toohello 叢集和建立叢集共用磁碟區 (CSV)。 下列範例中的 hello 建立 800 gb CSV。

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   完成此命令後，系統會將 800 GB 的磁碟區掛接為叢集資源。 hello 磁碟區位於`C:\ClusterStorage\Volume1\`。

   hello 下列圖表顯示 S2D 的叢集共用磁碟區：

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a>步驟 3︰測試容錯移轉叢集的容錯移轉

在 [容錯移轉叢集管理員] 中，確認您可以移動 hello 儲存體資源 toohello 其他叢集節點。 如果您可以連接 toohello 容錯移轉叢集與**容錯移轉叢集管理員**並且從一個節點 toohello 其他移動 hello 存放裝置，您就準備好 tooconfigure hello FCI。

## <a name="step-4-create-sql-server-fci"></a>步驟 4：建立 SDL Server FCI

設定 hello 容錯移轉叢集與所有叢集元件包括儲存體之後，您可以建立 SQL Server FCI hello。

1. 使用 RDP 連線 toohello 第一部虛擬機器。

1. 在**容錯移轉叢集管理員**，請確定所有叢集核心資源在 hello 第一部虛擬機器上。 如果有必要，請移動所有資源 toothis 虛擬機器。

1. 找出 hello 安裝媒體。 如果 hello 虛擬機器可使用其中一個 hello Azure Marketplace 映像，是位於 hello 媒體`C:\SQLServer_<version number>_Full`。 按一下 [設定] 。

1. 在 hello **SQL Server 安裝中心**，按一下 **安裝**。

1. 按一下 [安裝新的 SQL Server 容錯移轉叢集]。 請遵循 hello hello 精靈 tooinstall hello SQL Server FCI 中的指示。

   hello FCI 資料目錄需要 toobe 叢集存放裝置上。 S2D，它不共用的磁碟，而每個伺服器上的掛接點 tooa 磁碟區。 S2D 同步處理兩個節點之間的 hello 磁碟區。 hello 磁碟區會顯示 toohello 叢集與叢集共用磁碟區。 用於 hello 資料目錄中的 hello CSV 掛接點。

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. Hello 精靈完成之後，安裝程式會安裝 SQL Server FCI hello 第一個節點上。

1. 安裝程式已成功安裝 hello FCI hello 第一個節點上之後，請使用 RDP 連線 toohello 第二個節點。

1. 開啟 hello **SQL Server 安裝中心**。 按一下 [安裝]。

1. 按一下**新增節點 tooa SQL Server 容錯移轉叢集**。 遵循 hello hello 精靈 tooinstall SQL server 中的指示，並將此伺服器 toohello FCI。

   >[!NOTE]
   >如果您使用 Azure Marketplace 的資源庫映像與 SQL Server，SQL Server 工具已隨附 hello 映像。 如果您未使用此映像，請個別安裝 hello SQL Server 工具。 請參閱[下載 Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx)。

## <a name="step-5-create-azure-load-balancer"></a>步驟 5：建立 Azure Load Balancer

Azure 虛擬機器，在叢集上使用負載平衡器 toohold 一次需要 toobe 一個叢集節點上的 IP 位址。 在此解決方案中，hello 負載平衡器會保存 hello hello SQL Server FCI 的 IP 位址。

[建立並設定 Azure Load Balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)。

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a>在 hello Azure 入口網站中建立 hello 負載平衡器

toocreate hello 負載平衡器：

1. 在 hello Azure 入口網站，移 toohello 資源群組與 hello 虛擬機器。

1. 按一下 [+ 新增]。 搜尋 hello Marketplace 的**負載平衡器**。 按一下 [負載平衡器]。

1. 按一下 [建立] 。

1. 設定具有 hello 負載平衡器：

   - **名稱**： 可識別 hello 負載平衡器的名稱。
   - **型別**: hello 負載平衡器可以是公用或私用。 私用的負載平衡器可從 hello 相同的 VNET。 大部分的 Azure 應用程式都能使用私人負載平衡器。 如果您的應用程式需要存取 tooSQL 伺服器直接透過網際網路 hello，請使用公用負載平衡器。
   - **虛擬網路**: hello 做為 hello 虛擬機器相同網路。
   - **子網路**: hello hello 虛擬機器相同的子網路。
   - **私用 IP 位址**: hello 相同的 IP 位址指派給 toohello SQL Server FCI 的叢集網路資源。
   - **訂用帳戶**：您的 Azure 訂用帳戶。
   - **資源群組**： 使用 hello 相同資源群組，做為虛擬機器。
   - **位置**： 使用 hello 相同做為虛擬機器的 Azure 位置。
   請參閱下列圖片的 hello:

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a>Hello 負載平衡器後端集區設定

1. 傳回與 hello 虛擬機器 toohello Azure 資源群組，並找出 hello 新增負載平衡器。 您可能必須 toorefresh hello 檢視 hello 資源群組上。 按一下 hello 負載平衡器。

1. 在 hello 負載平衡器刀鋒視窗中，按一下 **後端集區**。

1. 按一下**+ 加**tooadd 後端集區。

1. 輸入 hello 後端集區的名稱。

1. 按一下 [+ 新增虛擬機器]。

1. 在 hello**選擇虛擬機器**刀鋒視窗中，按一下 **選擇可用性設定組**。

1. 選擇 hello 可用性設定組放置於 hello SQL Server 虛擬機器。

1. 在 hello**選擇虛擬機器**刀鋒視窗中，按一下 **選擇 hello 虛擬機器**。

   在 Azure 入口網站看起來應該類似下列圖片的 hello:

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. 按一下**選取**上 hello**選擇虛擬機器**刀鋒視窗。

1. 按兩次 [確定]  。

### <a name="configure-a-load-balancer-health-probe"></a>設定負載平衡器健全狀況探查

1. 在 hello 負載平衡器刀鋒視窗中，按一下 **健全狀況探查**。

1. 按一下 [+ 新增]。

1. 在 hello**新增健全狀況探查**刀鋒視窗中， <a name="probe"></a>設定 hello 健全狀況探查參數：

   - **名稱**: hello 健全狀況探查的名稱。
   - **通訊協定**：TCP。
   - **連接埠**： 設定 tooan 可用的 TCP 通訊埠。 此連接埠需要開啟防火牆的連接埠。 使用 hello[相同的連接埠](#ports)您在 hello 防火牆設定 hello 健全狀況探查。
   - **間隔**：5 秒。
   - **狀況不良臨界值**：2 次連續失敗。

1. 按一下 [確定]。

### <a name="set-load-balancing-rules"></a>設定負載平衡規則

1. 在 hello 負載平衡器刀鋒視窗中，按一下 **負載平衡規則**。

1. 按一下 [+ 新增]。

1. 設定 hello 負載平衡規則參數：

   - **名稱**: hello 負載平衡規則的名稱。
   - **前端 IP 位址**: hello IP 位址用於 hello SQL Server FCI 的叢集網路資源。
   - **連接埠**: hello SQL Server FCI TCP 通訊埠設定。 hello 預設執行個體的連接埠為 1433年。
   - **後端連接埠**： 這個值一律使用相同連接埠的 hello 與 hello**連接埠**值，當您啟用**浮動 IP （伺服器直接回傳）**。
   - **後端集區**： 使用 hello 後端集區名稱，您先前設定。
   - **健全狀況探查**： 您先前設定的使用 hello 健全狀況探查。
   - **工作階段持續性**：無。
   - **閒置逾時 (分鐘)**：4。
   - **浮動 IP (伺服器直接回傳)**：已啟用。

1. 按一下 [確定] 。

## <a name="step-6-configure-cluster-for-probe"></a>步驟 6：設定探查叢集

在 PowerShell 中設定 hello 叢集探查連接埠參數。

tooset hello 叢集探查連接埠參數，請更新您的環境中的下列指令碼的 hello 中的變數。

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a>步驟 7：測試 FCI 容錯移轉

測試容錯移轉的 hello FCI toovalidate 叢集功能。 下列步驟 hello:

1. 使用 RDP 連線 tooone hello SQL Server FCI 的叢集節點。

1. 開啟 [容錯移轉叢集管理員]。 按一下 [角色]。 請注意哪個節點擁有 hello SQL Server FCI 角色中。

1. 以滑鼠右鍵按一下 hello SQL Server FCI 角色。

1. 按一下 [移動]，然後按一下 [最佳可行節點]。

**容錯移轉叢集管理員**顯示 hello 角色和其資源變成離線狀態。 hello 資源移動，然後上線在 hello 另一個節點。

### <a name="test-connectivity"></a>測試連線能力

tootest 連線，hello tooanother 虛擬機器中的記錄檔相同的虛擬網路。 開啟**SQL Server Management Studio**並連接 toohello SQL Server FCI 的名稱。

>[!NOTE]
>如有需要，您可以[下載 SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx)。

## <a name="limitations"></a>限制
Azure 虛擬機器，在 Microsoft Distributed Transaction Coordinator (DTC) 不支援在 Fci 上因為 hello 負載平衡器不支援 hello RPC 連接埠。

## <a name="see-also"></a>另請參閱

[透過遠端桌面 (Azure) 設定 S2D](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

[具有儲存空間直接存取的超交集解決方案](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)。

[儲存空間直接存取概觀](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[適用於 S2D 的 SQL Server 支援](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
