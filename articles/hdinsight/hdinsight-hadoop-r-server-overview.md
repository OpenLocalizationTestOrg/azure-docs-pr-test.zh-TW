---
title: "aaaIntroduction 導覽 Azure HDInsight 上的伺服器 |Microsoft 文件"
description: "深入了解如何 toouse R Server 巨量資料分析的 HDInsight toocreate 應用程式上。"
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6dc21bf5-4429-435f-a0fb-eea856e0ea96
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: daf7b70a15748d66510a04da370f39c5f26eb4ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#<a name="introduction-toor-server-and-open-source-r-capabilities-on-hdinsight"></a>簡介導覽伺服器與 HDInsight 上的開放原始碼 R 功能

在 Azure 中建立 HDInsight 叢集時，可選擇 Microsoft R 伺服器作為部署選項。 這項新功能提供資料科學家，統計學家和 R 程式設計人員與視需要存取 tooscalable 分散式 HDInsight 上的分析方法。

可以是叢集 toohello 專案和工作適當調整大小，然後終止時不再需要它們。 由於它們是 Azure HDInsight 的一部分，這些叢集隨附於企業層級 24/7 支援 99.9%執行時間的 SLA，而且 hello 能力 toointegrate hello Azure 生態系統中的其他元件。

HDInsight 上的 R 伺服器提供的幾乎任何的大小，載入 tooeither Azure Blob 或資料湖存放區的資料集 hello 最新功能，如 R 為基礎的分析。 由於 R Server 根據開放原始碼 R，hello 您建置應用程式可以利用任何 hello 8000 + 開放原始碼 R 封裝。 ScaleR，Microsoft R Server 隨附的巨量資料分析封裝中的 hello 常式也會提供。

hello 邊緣節點的叢集提供方便的位置 tooconnect toohello 叢集和 toorun R 指令碼。 邊緣節點之後，您有 hello 選項執行 hello 平行處理的分散式函式的 ScaleR 跨 hello 核心的 hello 邊緣節點伺服器。 您也可以執行這些 hello hello 叢集節點之間使用 ScaleR 的 Hadoop 對應減少或 Spark 計算內容。

hello 模型或預測分析的結果可以下載的使用在內部部署。 它們也可以在 Azure 中的其他地方實際運作，特別是透過 [Azure Machine Learning Studio](http://studio.azureml.net) [Web 服務](../machine-learning/machine-learning-publish-a-machine-learning-web-service.md)。

## <a name="get-started-with-r-on-hdinsight"></a>開始使用 HDInsight 上的 R
在 HDInsight 叢集 tooinclude R 伺服器建立使用 hello Azure 入口網站的 HDInsight 叢集時，必須選取 hello R 伺服器叢集類型。 hello R 伺服器叢集類型包括 R 伺服器 hello 資料 hello 叢集節點和邊緣節點，做為 R Server 為基礎的分析的登陸區域上。 請參閱[開始使用 HDInsight 上的 R Server](hdinsight-hadoop-r-server-get-started.md)如需如何 toocreate hello 叢集的逐步解說。

## <a name="learn-about-data-storage-options"></a>了解資料儲存體選項
Hello HDFS 檔案系統的 HDInsight 叢集的預設儲存體可以與 Azure 儲存體帳戶或 Azure 資料湖存放區產生關聯。 此關聯可確保任何資料上傳在分析期間 toohello 叢集存放區由持續性。 有各種工具來處理 hello 資料傳輸 toohello 儲存您選取選項，包括 hello 入口網站為基礎的上傳機能 hello 儲存體帳戶和 hello [AzCopy](../storage/common/storage-use-azcopy.md)公用程式。

您可以 hello 選擇佈建程序，不論 hello 主要儲存體選項，使用中的 hello 叢集期間，加入存取 tooadditional Blob 和資料湖存放區。 請參閱[開始使用 HDInsight 上的 R Server](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-get-started)如需新增存取 tooadditional 帳戶資訊。 請參閱 hello 補充[R Server HDInsight 上的 Azure 儲存體選項](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-storage)文章 toolearn 深入了解使用多個儲存體帳戶。

您也可以使用[Azure 檔案](../storage/files/storage-how-to-use-files-linux.md)當做儲存選項使用 hello 邊緣節點上。 Azure 檔案可讓您 toomount Azure 儲存體 toohello Linux 檔案系統中所建立的檔案共用。 如需適用於 HDInsight 叢集上 R 伺服器的這些資料儲存體選項詳細資訊，請參閱[適用於 HDInsight 叢集上的 R 伺服器的 Azure 儲存體選項](hdinsight-hadoop-r-server-storage.md)。

## <a name="access-r-server-on-hello-cluster"></a>Hello 叢集上存取 R 伺服器
您可以連接的導覽使用瀏覽器中，提供您的 hello 邊緣節點上的伺服器 hello 佈建程序期間選擇 tooinclude RStudio 伺服器。 如果您沒有安裝它佈建 hello 叢集時，您可以稍後新增。 如需在建立叢集之後安裝 RStudio Server 的相關資訊，請參閱[在 HDInsight 叢集上安裝 RStudio Server](hdinsight-hadoop-r-server-install-r-studio.md)。 您也可以使用 SSH/PuTTY tooaccess hello R 主控台連接 toohello R Server。 

## <a name="develop-and-run-r-scripts"></a>開發和執行 R 指令碼
hello R 指令碼建立和執行可使用任何 hello 8000 + 開放原始碼 R 封裝中加入 toohello 平行處理和分散式 hello ScaleR 文件庫中可用的常式。 一般情況下，使用 R 伺服器 hello 邊緣節點執行的指令碼 hello R 解譯器中執行，該節點上。 hello 例外狀況是需要 toocall tooHadoop 對應減少 (RxHadoopMR) 或 Spark (RxSpark) 設定為運算環境的 ScaleR 函式的這些步驟。 在此情況下，hello 函式會執行分散式方式跨這些資料 （工作） hello 叢集節點會參考的 hello 資料與相關聯。 如需 hello 不同的計算內容選項的詳細資訊，請參閱[計算 R Server HDInsight 上的內容選項](hdinsight-hadoop-r-server-compute-contexts.md)。

## <a name="operationalize-a-model"></a>模型運作
完成您的資料模型化時，您可以實施為新的資料從 Azure 與內部部署的 hello 模型 toomake 預測。 這個程序稱為評分。 評分可在 HDInsight、Azure Machine Learning 或內部部署中完成。

### <a name="score-in-hdinsight"></a>在 HDInsight 中評分
在 HDInsight tooscore 撰寫呼叫模型 toomake 作為預測新資料檔案，您已載入 tooyour 儲存體帳戶的 R 函數。 然後儲存 hello 預測後 toohello 儲存體帳戶。 您可以視需要執行 hello 常式 hello 邊緣節點的叢集，或使用排程的工作上。  

### <a name="score-in-azure-machine-learning-aml"></a>Azure Machine Learning 中的評分 (AML)
使用 AML web 服務、 使用 hello tooscore 開啟來源 Azure 機器學習 R 封裝，又稱為[AzureML](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) toopublish 您為 Azure web 服務的模型。 為了方便起見，此套件是 hello 邊緣節點上預先安裝。 接著，使用機器學習 toocreate 使用者介面中的 hello 設備 hello web 服務，並視需要為計分，然後呼叫 hello web 服務。

如果您選擇此選項時，您會需要的 tooconvert 任何 ScaleR 模型物件 tooequivalent 開放原始碼模型物件的使用與 hello web 服務。 針對此轉換，您可以使用 ScaleR 強制型轉函數 (例如，適用於集成模型的 `as.randomForest()`) 來完成。

### <a name="score-on-premises"></a>內部部署評分
tooscore 內部建立您的模型之後，您可以將序列化 R、 下載，還原序列化，並會將它用於計分新資料中的 hello 模型。 您可以在使用中稍早所述的 hello 方法評分新資料[計分 HDInsight 中](#scoring-in-hdinsight)或使用[DeployR](https://deployr.revolutionanalytics.com/)。

## <a name="maintain-hello-cluster"></a>維護 hello 叢集
### <a name="install-and-maintain-r-packages"></a>安裝及維護 R 套件
大部分的 hello R 套件讓您在該處執行 R 指令碼的大部分步驟之後需要 hello 邊緣節點上。 tooinstall 其他 R 封裝 hello 邊緣節點上的，您可以使用一般的 hello`install.packages()`方法

如果您只會使用從 hello ScaleR 程式庫的常式 hello 叢集中，您通常不需要 tooinstall 其他 R 封裝上 hello 資料節點。 不過，您可能需要其他封裝 toosupport hello 使用**rxExec**或**RxDataStep** hello 資料節點上的執行。

在這些情況下，hello 其他封裝可以安裝指令碼動作以建立 hello 叢集之後。 如需詳細資訊，請參閱[建立含 R 伺服器的 HDInsight 叢集](hdinsight-hadoop-r-server-get-started.md)。   

### <a name="change-hadoop-map-reduce-memory-settings"></a>變更 Hadoop Map Reduce 記憶體設定
叢集可以執行對應減少 」 工作時是使用導覽伺服器的記憶體已修改的 toochange hello 數量。 toomodify 叢集中，使用 hello hello Azure 入口網站的刀鋒伺服器叢集透過 Apache Ambari UI。 如需有關如何 tooaccess hello Ambari UI 叢集的指示，請參閱[管理 HDInsight 叢集使用 hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)。

它也是可能 toochange hello 數量記憶體可用導覽伺服器利用 Hadoop 參數中的 hello 呼叫太**RxHadoopMR** ，如下所示：

    hadoopSwitches = "-libjars /etc/hadoop/conf -Dmapred.job.map.memory.mb=6656"  

### <a name="scale-your-cluster"></a>調整叢集的大小
現有的叢集中可以向上或向下調整透過 hello 入口網站。 藉由調整，您可以取得 hello 額外的容量，您可能需要較大的處理工作，或您可以向下調整叢集閒置時。 如需有關如何指示 tooscale 叢集中，請參閱[管理 HDInsight 叢集](hdinsight-administer-use-portal-linux.md)。

### <a name="maintain-hello-system"></a>維護 hello 系統
Hello 基礎的 HDInsight 叢集在 Linux Vm，在離峰時間執行維護 tooapply OS 修補程式和其他更新。 一般而言，將維護完成上午 3:30 執行 （根據 hello hello VM 的本機時間），每個星期一和星期四。 更新會執行的方式在不影響 hello 叢集中的多個季一次。  

因為 hello 前端節點是多餘且不是所有的資料節點會受到影響，所以任何正在執行工作，在這段期間可能會變慢。 他們仍然應該執行 toocompletion，不過。 除非發生需要重建叢集的嚴重失敗，否則您擁有的任何自訂軟體或本機資料，在這些維護事件中皆會保留。

## <a name="learn-about-ide-options-for-r-server-on-an-hdinsight-cluster"></a>了解適用於 HDInsight 叢集上 R 伺服器的 IDE 選項
HDInsight 叢集 hello Linux 邊緣節點是 hello 登陸區域 R 為基礎的分析。 新的 HDInsight 版本會提供安裝 hello 社群版本的預設選項[RStudio 伺服器](https://www.rstudio.com/products/rstudio-server/)，於瀏覽器為基礎的 IDE hello 邊緣節點上。 使用 RStudio 伺服器當作 hello 開發 IDE 並執行 R 指令碼可以大幅提高生產力，比只使用 hello R 主控台。 如果您選擇 tooadd RStudio 伺服器時建立 hello 叢集，但想 tooadd 它更新版本中，然後查看[在 HDInsight 叢集上安裝 R Studio Server](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-install-r-studio)。 +

另一個完整的 IDE 選項是 tooinstall 桌面的 IDE，並將它透過使用遠端的對應減少 」 或 「 Spark 計算內容 tooaccess hello 叢集。 選項包括 Microsoft 的 [Visual Studio R 工具](https://www.visualstudio.com/features/rtvs-vs.aspx) (RTVS)、RStudio 與 Walware 的 Eclipse 型 [StatET](http://www.walware.de/goto/statet)。

最後，您可以存取 hello R Server 主控台 hello 邊緣節點上的，輸入**R**連接透過 SSH PuTY 之後的 hello Linux 命令提示字元。 當使用 hello 主控台介面時，它是方便 toorun 的文字編輯器在另一個視窗中，R 指令碼開發和剪下並視您的指令碼的區段貼入 hello R 主控台。

## <a name="learn-about-pricing"></a>了解價格
hello 與 HDInsight 叢集與 R 伺服器相關聯的費用類似的結構 toohello 費用 hello 標準的 HDInsight 叢集。 它們所根據的 hello hello 基礎跨 hello 名稱、 資料和核心小時 uplift hello 加入的邊緣節點的 Vm 大小。 如需 HDInsight 定價，和 30 天免費試用版的 hello 可用性的詳細資訊，請參閱[HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。

## <a name="next-steps"></a>後續步驟
toolearn 深入了解如何 toouse R 伺服器與 HDInsight 叢集，請參閱下列主題中的 hello:

* [開始使用 HDInsight 上的 R 伺服器](hdinsight-hadoop-r-server-get-started.md)
* [新增 RStudio 伺服器 tooHDInsight （如果未安裝在叢集建立期間）](hdinsight-hadoop-r-server-install-r-studio.md)
* [適用於 HDInsight 中 R 伺服器的計算內容選項](hdinsight-hadoop-r-server-compute-contexts.md)
* [適用於 HDInsight R 伺服器的 Azure 儲存體選項](hdinsight-hadoop-r-server-storage.md)
