---
title: "aaaBatch 和 hello 雲端-Azure 中的 HPC 解決方案 |Microsoft 文件"
description: "了解批次和高效能計算 (HPC 和 Big Compute) 案例，以及在 Azure 中的解決方案選項"
services: batch, virtual-machines, cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: aab5401d-2baf-4cf2-bf20-ad224de33888
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c5a3c8859d1f95040bcdad15942a815d71eb4486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="batch-and-hpc-solutions-for-large-scale-computing-workloads"></a>大規模運算工作負載的 Batch 和 HPC 解決方案

Azure 針對批次和高效能運算 (HPC) 提供有效、可調整的雲端解決方案 - 又稱為「Big Compute」 。 在這裡了解有關 Big Compute 工作負載和 Azure 的服務 toosupport 它們，或直接跳過[解決方案案例](#scenarios)本文稍後。 本文的主要技術決策者、 IT 經理和獨立軟體廠商，但其他 IT 專業人員和開發人員可以使用 it toofamiliarize 本身與這些解決方案。

組織有大規模的運算問題：工程設計和分析、影像轉譯、複雜模型、Monte Carlo 模擬和財務風險計算等等。 Azure 可協助組織使用 hello 資源、 小數位數和排程必須解決這些問題。 有了 Azure，組織就可以：

* 建立混合式解決方案，擴充內部部署 HPC 叢集 toooffload 尖峰工作負載 toohello 雲端
* 完全在 Azure 中執行 HPC 叢集工具和工作負載
* 使用受管理和可擴充的 Azure 服務，例如[批次](https://azure.microsoft.com/documentation/services/batch/)toorun 運算密集工作負載，而不需要 toodeploy 和管理運算基礎結構

雖然超出本文的 hello 範圍，Azure 也提供開發人員和合作夥伴一組完整的功能、 架構選擇和開發工具 toobuild 大型、 自訂 Big Compute 工作流程。 而持續成長的合作夥伴生態系統是準備 toohelp 讓 Big Compute 工作負載在 hello Azure 雲端中具生產力。

## <a name="batch-and-hpc-applications"></a>批次和 HPC 應用程式
不同於 Web 應用程式和許多特定業務應用程式、批次和 HPC 應用程式擁有既定的開始和結束，而且它們可以排程或隨選執行，有時候數小時或更久。 大部分可分成兩個主要類別：*本質平行*（有時稱為 「 窘迫平行 」，因為 hello 解決的問題適合以平行方式在多部電腦或處理器 toorunning） 和*緊密結合*。 Hello 下表針對這些應用程式類型有關的詳細資訊，請參閱。 某些 Azure 方案方法更好一個類型或 hello 其他工作。

> [!NOTE]
> 在 Batch 和 HPC 解決方案中，應用程式正在執行的執行個體通常稱為「作業」，而每項作業可能會分成「工作」。 和 hello hello 應用程式的叢集的計算資源通常稱為*計算節點*。
> 
> 

| 類型 | 特性 | 範例 |
| --- | --- | --- |
| **本質平行**<br/><br/>![本質平行][parallel] |• 個別的電腦獨立執行應用程式邏輯<br/><br/> • 新增電腦可讓 hello 應用 tooscale 而且減少計算時間<br/><br/>• 應用程式包含個別的可執行檔，或是分成用戶端叫用的服務群組 (服務導向的架構、或 SOA、應用程式) |• 財務風險模型<br/><br/>• 影像轉譯和影像處理<br/><br/>• 媒體編碼及轉碼<br/><br/>• 蒙地卡羅模擬<br/><br/>• 軟體測試 |
| **Tightly coupled**<br/><br/>![Tightly coupled][coupled] |• 應用程式需要計算節點 toointeract 或交換中繼結果<br/><br/>• 計算節點可能會使用通訊 hello 訊息傳遞介面 (MPI)，針對平行計算常見的通訊協定<br/><br/>• hello 應用程式是機密 toonetwork 延遲和頻寬<br/><br/>• 可以改善應用程式效能，方法是使用支援高速網路技術，例如 InfiniBand 和遠端直接記憶體存取 (RDMA) 的計算基礎結構 |• 石油與天然氣貯存槽模型<br/><br/>• 工程設計和分析，例如計算流體動力學<br/><br/>• 實體模擬，例如車輛碰撞和核子反應<br/><br/>• 天氣預報 |

### <a name="considerations-for-running-batch-and-hpc-applications-in-hello-cloud"></a>Hello 雲端中執行批次和 HPC 應用程式的考量
您可以輕易地移轉會在內部部署 HPC 叢集 tooAzure 或 tooa （跨內部部署） 的混合式環境中設計的 toorun 的許多應用程式。 不過，可能會有一些限制或考量，包括：

* **雲端資源的可用性**-根據 hello 類型使用的雲端計算資源，您可能不能 toorely 機器上的執行作業時。 處理狀態和進度檢查指向常見技術 toohandle 可能暫時性失敗，以及更多視需要使用雲端資源時。
* **資料存取**-通常可在企業的群集，例如 NFS、 資料存取技術可能需要 hello 雲端中的特殊設定。 或者，您可能需要 hello 雲端 tooadopt 不同的資料存取的作法和模式。
* **資料移動**-如果要讓處理大量的資料，策略是雲端存放裝置和 toocompute 資源所需的 toomove hello 資料的應用程式。 您可能需要高速跨單位網路，例如 [Azure ExpressRoute](https://azure.microsoft.com/services/expressroute/)。 也請考慮法律、法規或原則對儲存或存取該資料的限制。
* **授權**-請 hello 授權的任何商業應用程式的廠商或在執行的其他限制 hello 雲端。 並非所有廠商都提供隨用隨付授權。 您可能需要您的解決方案，tooplan hello 雲端中的授權伺服器或連接 tooan 在內部部署授權伺服器。

### <a name="big-compute-or-big-data"></a>大量運算或巨量資料？
hello 除以 Big Compute 和巨量資料的應用程式之間的線不一定顯而易見，而且有些應用程式可能同時擁有兩者的特性。 兩者都涉及執行大規模計算，通常是在電腦的叢集上。 但 hello 方案方法和支援的工具可以不同。

• **Big Compute**傾向 tooinvolve 應用程式倚賴 CPU 能力和記憶體，例如工程模擬、 財務風險模型和數位轉譯。 hello Big Compute 解決方案的基礎結構可能包含與專用多核心處理器 tooperform 原始計算，以及特殊、 高速網路硬體 tooconnect hello 電腦。

• **巨量資料**可解決單一電腦或資料庫管理系統無法管理的大量資料之資料分析問題。 範例包括大量 Web 記錄或其他商業智慧資料。 巨量資料通常會有更詳細的磁碟容量和 I/O 效能比對 CPU 能力 toorely。 另外還有專門巨量資料的工具，像是 Apache Hadoop toomanage hello 叢集和磁碟分割 hello 資料。 (如需 Azure HDInsight 和其他 Azure Hadoop 解決方案的相關資訊，請參閱 [Hadoop](https://azure.microsoft.com/solutions/hadoop/)。)

## <a name="compute-management-and-job-scheduling"></a>計算管理和作業排程
執行批次和 HPC 應用程式通常包括*叢集管理員*和*作業排程器*toohelp 管理叢集的計算資源並配置它們執行 hello 作業的 toohello 應用程式。 這些函式可能會透過不同的工具或某種整合式工具或服務來完成。

* **叢集管理員** - 佈建、發行及管理計算資源 (或運算節點)。 叢集管理員可能會自動安裝作業系統映像和計算節點上的應用程式調整計算資源，根據 toodemands，並監視 hello 效能的 hello 節點。
* **工作排程器**-指定 hello 資源 （例如處理器或記憶體） 應用程式需求，並 hello 條件時執行。 工作排程器會維護工作的佇列，並配置資源 toothem 根據指派的優先權或其他特性。

叢集和作業排程工具，windows 和 Linux 架構叢集可以移轉以及 tooAzure。 例如， [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029)，Microsoft 針對 Windows 和 Linux HPC 工作負載的免費計算叢集解決方案，提供數個在 Azure 中執行的選項。 您也可以建立 Linux 叢集扭力等 SLURM toorun 開放原始碼工具。 您也必須將商業方格解決方案 tooAzure，例如[TIBCO DataSynapse GridServer](https://azure.microsoft.com/blog/tibco-datasynapse-comes-to-the-azure-marketplace/)， [IBM 頻譜號交響曲和號交響曲 LSF](https://azure.microsoft.com/blog/ibm-and-microsoft-azure-support-spectrum-symphony-and-spectrum-lsf/)，和[Univa 方格引擎](http://www.univa.com/products/grid-engine)。

Hello 下列各節所示，您也可以充分利用 Azure 服務 toomanage 計算資源，並排程工作不 （或除了） 傳統的叢集管理工具。

## <a name="scenarios"></a>案例
以下是三種常見案例 toorun Big Compute 工作負載在 Azure 中使用現有的 HPC 叢集解決方案、 Azure 服務或 hello 兩者的組合。 選擇每個案例的重要考量事項都會列出，但並不詳盡。 更多可用 hello 您可能會在您的方案中使用 Azure 服務的相關晚 hello 文件中。

| 案例 | 為何選擇它？ |
| --- | --- | --- |
| **Burst HPC 叢集 tooAzure**<br/><br/>[![叢集高載][burst_cluster]](./media/batch-hpc-solutions/burst_cluster.png) <br/><br/> 深入了解：<br/>• [TooAzure 背景工作執行個體使用 HPC Pack 高載](https://technet.microsoft.com/library/gg481749.aspx)<br/><br/>• [使用 HPC Pack 安裝混合式計算叢集](../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)<br/><br/>• [TooAzure 批次使用 HPC Pack 高載](https://technet.microsoft.com/library/mt612877.aspx)<br/><br/> |• 結合 [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) 或其他內部部署叢集與混合式解決方案中的其他 Azure 資源。<br/><br/>• 擴充您 Big Compute 工作負載 toorun，平台上的為服務 (PaaS) 虛擬機器執行個體 （目前僅限 Windows Server)。<br/><br/>• 使用選擇性 Azure 虛擬網路來存取內部部署授權伺服器或資料存放區 |
| **在 Azure 中完整建立 HPC 叢集**<br/><br/>[![IaaS 中的叢集][iaas_cluster]](./media/batch-hpc-solutions/iaas_cluster.png)<br/><br/>深入了解：<br/>• [Azure 中的 HPC 叢集解決方案](big-compute-resources.md)<br/><br/> |• 在標準或自訂 Windows 或 Linux 基礎結構即服務 (IaaS) 虛擬機器上快速且一致地部署您的應用程式和叢集工具。<br/><br/>• 使用 hello 工作排程您選擇的方案，以執行各種 Big Compute 工作負載。<br/><br/>• 使用其他 Azure 服務，包括網路和存放裝置 toocreate 完成雲端為基礎的解決方案。 |
| **平行應用程式 tooAzure 外延展**<br/><br/>[![Azure Batch][batch_proc]](./media/batch-hpc-solutions/batch_proc.png)<br/><br/>深入了解：<br/>• [Azure Batch 的基本概念](batch-technical-overview.md)<br/><br/>•[快速入門適用於.NET 的 hello Azure Batch 程式庫](batch-dotnet-get-started.md) |• 開發[Azure Batch](https://azure.microsoft.com/documentation/services/batch/) tooscale 出各種 Big Compute 工作負載 toorun 上的 Windows 或 Linux 虛擬機器的集區。<br/><br/>• 使用 Azure 平台服務 toomanage 部署和自動調整的虛擬機器、 工作排程、 災害復原、 資料移動、 相依性管理和應用程式部署。 |

## <a name="azure-services-for-big-compute"></a>適合大量運算的 Azure 服務
以下是更多關於 hello 運算、 資料、 網路及相關的服務可以結合的 Big Compute 解決方案和工作流程。 如需詳細指引，在 Azure 的服務，請參閱 hello Azure 服務[文件](https://azure.microsoft.com/documentation/)。 hello[案例](#scenarios)稍早在本文章中顯示 使用這些服務的一些方法。

> [!NOTE]
> Azure 定期導入了對於您的案例可能有用的新服務。 如果您有疑問，請連絡 [Azure 合作夥伴](https://pinpoint.microsoft.com/en-US/search?keyword=azure)或寄電子郵件到 *bigcompute@microsoft.com*。
> 
> 

### <a name="compute-services"></a>計算服務
Azure 計算服務是 hello 核心 Big Compute 解決方案和 hello 不同的計算服務供應項目優勢針對不同的案例。 在基本層級中，這些服務會提供 Azure 使用 Windows Server HYPER-V 技術所提供的虛擬機器計算執行個體上的應用程式 toorun 不同的模式。 這些執行個體可以執行標準和自訂的 Linux 和 Windows 作業系統和工具。 Azure 可以讓您選擇 [執行個體大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ，搭配 CPU 核心、記憶體、磁碟容量和其他特性等不同組態。 根據您的需求，您可以調整 hello 執行個體 toothousands 的核心，然後向下延展時需要較少的資源。

> [!NOTE]
> 利用 hello Azure[需要大量計算執行個體，例如 hello H 數列](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)tooimprove hello 效能和延展性的 HPC 工作負載。 這些執行個體也支援需要低延遲及高輸送量應用程式網路的平行 MPI 應用程式。 也可用為[N 數列](../virtual-machines/windows/sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)NVIDIA Gpu tooexpand hello 範圍的計算和視覺效果的案例，在 Azure 中的 Vm。  
> 
> 

| 服務 | 說明 |
| --- | --- |
| **[虛擬機器](https://azure.microsoft.com/documentation/services/virtual-machines/)**<br/><br/> |• 使用 Microsoft Hyper-V 技術來提供計算基礎結構即服務 (IaaS)<br/><br/>• Tooflexibly 佈建可讓您和管理永續性雲端電腦從標準 Windows Server 或 Linux 映像，從 hello [Azure Marketplace](https://azure.microsoft.com/marketplace/)，或您提供的映像和資料磁碟<br/><br/>部署及管理 • [VM 規模集](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)toobuild 大規模服務從相同的虛擬機器的自動調整 tooincrease 或減少容量自動<br/><br/>• 執行內部部署計算叢集工具和應用程式完全 hello 雲端中<br/><br/> |
| **[雲端服務](https://azure.microsoft.com/documentation/services/cloud-services/)**<br/><br/> |• 可以在背景工作角色執行個體中執行大量運算應用程式，這是執行 Windows Server 版本，而且完全受 Azure 管理的虛擬機器<br/><br/>• 啟用管理負荷低且在平台即服務 (PaaS) 模型中執行的可調整、可靠應用程式<br/><br/>• 可能會需要額外的工具或與內部部署 HPC 叢集解決方案的開發 toointegrate |
| **[批次](https://azure.microsoft.com/documentation/services/batch/)**<br/><br/> |• 在完全受管理的服務中執行大規模的平行與批次工作負載<br/><br/>• 提供作業排程和自動調整受管理的虛擬機器集區<br/><br/>• 可讓開發人員 toobuild 及執行應用程式做為服務或雲端啟用現有的應用程式<br/> |

### <a name="storage-services"></a>儲存體服務
大量運算解決方案通常會在一組輸入資料上操作，並產生其結果的資料。 Big Compute 解決方案中使用的 hello Azure 儲存體服務包括：

* [Blob、資料表和佇列儲存體](https://azure.microsoft.com/documentation/services/storage/) - 分別管理大量非結構化資料、NoSQL 資料，和工作流程和通訊的訊息。 例如，對於大型的技術資料集，或針對 hello 輸入映像，您可以使用 blob 儲存體或媒體檔案您應用程式的程序。 您可以在解決方案中使用佇列以速行非同步通訊。 請參閱[簡介 tooMicrosoft Azure 儲存體](../storage/common/storage-introduction.md)。
* [Azure 檔案儲存體](https://azure.microsoft.com/services/storage/files/)-共用常用檔案和在 Azure 中使用的資料 hello 標準 SMB 通訊協定，所需的一些 HPC 叢集解決方案。
* [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) -超 Apache Hadoop 分散式檔案系統提供了適用於批次，即時的 hello 雲端和互動式分析。

### <a name="data-and-analysis-services"></a>資料和分析服務
若干大量運算案例牽涉到大型資料流，或會產生需要進一步處理或分析的資料。 Azure 提供幾種資料和分析服務，包括︰

* [Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) - 建置資料導向的工作流程 (管線)，以聯結、彙總和轉換來自內部部署、雲端型和網際網路資料存放區的資料。
* [SQL Database](https://azure.microsoft.com/documentation/services/sql-database/) -提供 hello 的受管理的服務中的 Microsoft SQL Server 關聯式資料庫管理系統的主要功能。
* [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/) -部署和佈建 Windows Server 或 linux Apache Hadoop 叢集在 hello 雲端 toomanage、 分析和報告巨量資料。
* [機器學習服務](https://azure.microsoft.com/documentation/services/machine-learning/) - 可幫助您在完全管理的服務中建立、測試、操作和管理預測分析解決方案。

### <a name="additional-services"></a>其他服務
Big Compute 解決方案可能需要其他 Azure 服務 tooconnect tooresources 內部部署或在其他環境中。 範例包括：

* [虛擬網路](https://azure.microsoft.com/documentation/services/virtual-network/)-Azure tooconnect Azure 資源 tooeach 其他或 tooyour 在內部部署資料中心 」 中建立邏輯隔離的區段。 透過跨單位虛擬網路，Big Compute 應用程式可存取內部部署資料、Active Directory 服務和授權伺服器
* [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) - 可在 Microsoft 資料中心和內部部署或共置環境中的基礎結構之間建立私人連線。 ExpressRoute hello 網際網路提供較高的安全性、 多個可靠性、 更快的速度和低延遲比一般的連線。
* [服務匯流排](https://azure.microsoft.com/documentation/services/service-bus/)-提供應用程式的幾項機制 toocommunicate 或交換資料，不論它們位於在 Azure 上、 另一個雲端平台上，或是在資料中心。

## <a name="next-steps"></a>後續步驟
* 請參閱[技術資源，批次和 HPC](big-compute-resources.md) toofind 技術指引 toobuild 您的方案。
* 與合作夥伴討論 Azure 選項，包括 Cycle Computing、Rescale 和 UberCloud。
* 閱讀 [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)、[Altair](https://azure.microsoft.com/blog/availability-of-altair-radioss-rdma-on-microsoft-azure/), [ANSYS](https://azure.microsoft.com/blog/ansys-cfd-and-microsoft-azure-perform-the-best-hpc-scalability-in-the-cloud/) 和 [d3VIEW](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088) 所提供的 Azure Big Compute 解決方案。
* 最新的 hello 公告，請參閱 hello [Microsoft HPC 和批次小組部落格](http://blogs.technet.com/b/windowshpc/)和 hello [Azure 部落格](https://azure.microsoft.com/blog/tag/hpc/)。

<!--Image references-->
[parallel]: ./media/batch-hpc-solutions/parallel.png
[coupled]: ./media/batch-hpc-solutions/coupled.png
[iaas_cluster]: ./media/batch-hpc-solutions/iaas_cluster.png
[burst_cluster]: ./media/batch-hpc-solutions/burst_cluster.png
[batch_proc]: ./media/batch-hpc-solutions/batch_proc.png
