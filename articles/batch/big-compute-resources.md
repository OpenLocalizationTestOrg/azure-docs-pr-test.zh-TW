---
title: "在 hello Azure 雲端中的批次和 HPC aaaResources |Microsoft 文件"
description: "列出您執行大規模的平行、 批次和高效能運算 (HPC) 工作負載在 Azure 中的技術資源 toohelp。"
services: batch, cloud-services, virtual-machines
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 6f8be911-c841-41ae-88d3-3bcfc029eb7f
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 03/17/2017
ms.author: danlep
ms.openlocfilehash: ab8ba24678bd7ec090306b501d29ca63c4fb83ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a>Azure 中的大量運算：批次和高效能運算的技術資源
這是您在 Azure 中執行大規模的平行、 批次和高效能運算 (HPC) 工作負載指南 tootechnical 資源 toohelp。 擴充您現有的批次或 HPC 工作負載 toohello Azure 的雲端，或建立新 Big Compute 解決方案使用的 Azure 服務。

## <a name="solutions-options"></a>方案選項
了解在 Azure 中 Big Compute 的選項，然後選擇 hello 正確的方法，針對您的工作負載和商務需求。

* [批次和 HPC 解決方案](batch-hpc-solutions.md)
* [影片： 使用 Azure 和 HPC hello 雲端中的 Big Compute](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a>Azure Batch
[批次](https://azure.microsoft.com/services/batch/)是平台服務，可讓您輕鬆 toocloud 啟用您的 Linux 和 Windows 應用程式和執行的工作，而不設定和管理叢集和作業的排程器。 使用 Azure 批次中的 hello SDK toointegrate 用戶端應用程式，透過不同的語言，階段資料 tooAzure，並建立工作執行管線檔案。

* [Documentation](https://azure.microsoft.com/documentation/services/batch/)
* [.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx)、[Python](http://azure-sdk-for-python.readthedocs.io/latest/)、[Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/)、[Java](http://azure.github.io/azure-sdk-for-java/) 和 [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API 參考
* [Batch 管理 .NET 程式庫](https://msdn.microsoft.com/library/mt463120.aspx) 參考
* 教學課程：開始使用[適用於 .NET 的 Azure Batch 程式庫](batch-dotnet-get-started.md)和 [Batch Python 用戶端](batch-python-tutorial.md)
* [批次論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [批次影片](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a>HPC 叢集解決方案
部署或擴充您現有 Windows 或 Linux HPC 叢集 tooAzure toorun 您大量計算的工作負載。  

### <a name="microsoft-hpc-pack"></a>Microsoft HPC Pack
HPC Pack 是建置在 Microsoft Azure 和 Windows Server 技術上的 Microsoft 免費 HPC 解決方案，可執行 Windows 和 Linux HPC 工作負載。  

* [下載 HPC Pack 2016](https://www.microsoft.com/download/details.aspx?id=54507)
* [下載 HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49922)
* [Documentation](https://technet.microsoft.com/library/jj899572.aspx)
* Azure 中的 HPC Pack 叢集選項：[Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 和 [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 
* [TooAzure 背景工作執行個體使用 HPC Pack 高載](https://technet.microsoft.com/library/gg481749.aspx)
* [TooAzure 批次使用 HPC Pack 高載](https://technet.microsoft.com/library/mt612877.aspx)
* [Windows HPC 論壇](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a>Linux 與 OSS 叢集解決方案
使用這些 Linux HPC 叢集的 Azure 範本 toodeploy。

* [加速 SLURM 叢集](https://azure.microsoft.com/documentation/templates/slurm/)和[部落格文章](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)
* [加速扭力叢集](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [使用 PBS Professional 計算格線範本 (英文)](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a>HPC 儲存體
* [Azure 上 HPC 儲存體的平行檔案系統 (英文)](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [Intel Cloud Edition for Lustre Software - Eval](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [CentOS 7.2 範本上的 BeeGFS (英文)](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a>Microsoft MPI
[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) 是 Microsoft 實作的 hello 標準開發和 hello Windows 平台上執行平行應用程式訊息傳遞介面。

* [下載 MS-MPI](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [MS-MPI 參考資料](https://msdn.microsoft.com/library/dn473458.aspx)
* [MPI 論壇](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a>計算密集型執行個體
Azure 提供[範圍的 VM 大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)，包括[需要大量計算 H 數列](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)能夠連線 tooa 後端 RDMA 網路，toorun Linux 和 Windows HPC 工作負載的執行個體。 

* [設定 Linux RDMA 叢集 toorun MPI 應用程式](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [設定 Windows RDMA 叢集使用 Microsoft HPC Pack toorun MPI 應用程式](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

針對 GPU 密集的工作負載，請參閱 [NC 和 NV 大小 (英文)](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/)。

## <a name="samples-and-demos"></a>範例和示範
* [Azure Batch C# 和 Python 程式碼範例](https://github.com/Azure/azure-batch-samples)
* [批次造船廠](https://azure.github.io/batch-shipyard/)工具組，以便於部署的批次樣式 Dockerized 工作負載 tooAzure 批次
* [doAzureParallel (英文)](http://www.github.com/Azure/doAzureParallel) R 套件 (以 Azure Batch 為基礎而建置)
* [測試磁碟機 SUSE Linux Enterprise Server for HPC](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a>相關的 Azure 服務
* [Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)
* [機器學習服務](https://azure.microsoft.com/documentation/services/machine-learning/)
* [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)
* [虛擬機器](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [虛擬機器擴展集](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [雲端服務](https://azure.microsoft.com/documentation/services/cloud-services/)
* [App Service](https://azure.microsoft.com/documentation/services/app-service/)
* [媒體服務](https://azure.microsoft.com/documentation/services/media-services/)
* [函式](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a>架構藍圖
* [用 Azure Batch 和 Azure Data Factory 的 HPC 及資料協調](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) 和[文章](../data-factory/data-factory-data-processing-using-batch.md)

## <a name="industry-solutions"></a>產業方案
* [銀行與資本市場](https://finance.azure.com/)
* [工程模擬](https://simulation.azure.com/) 

## <a name="customer-stories"></a>客戶案例
* [ANEO](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [d3View](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [Ludwig Institute of Cancer Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [Microsoft Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [明德精算顧問有限公司](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [Mitsubishi UFJ Securities International](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [Schlumberger](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [UberCloud](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a>後續步驟
* 最新的 hello 公告，請參閱 hello [Microsoft HPC 和批次小組部落格](http://blogs.technet.com/b/windowshpc/)和 hello [Azure 部落格](https://azure.microsoft.com/blog/tag/hpc/)。
* 另請參閱[批次中最新消息](https://azure.microsoft.com/updates/?service=batch)或訂閱 toohello [RSS 摘要](https://azure.microsoft.com/updates/feed/?service=batch)。

