---
title: "aaaWhat 是 Data Science 虛擬機器嗎？ | Microsoft Docs"
description: "如何 tooget 啟動重要的分析案例與資料科學虛擬機器。"
keywords: "資料科學工具、資料科學虛擬機器、資料科學工具、linux 資料科學"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d4f91270-dbd2-4290-ab2b-b7bfad0b2703
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;bradsev
ms.openlocfilehash: 18c7a75208671c663f3b6be6ee8d0bf666772e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-cloud-based-data-science-virtual-machine-for-linux-and-windows"></a>簡介 toohello 適用於 Linux 和 Windows 雲端 Data Science 虛擬機器
hello 資料科學虛擬機器 (DSVM) 是專為執行資料科學內建的 Microsoft Azure 雲端上的自訂的 VM 映像。 它有許多常用的資料科學與其他工具，預先安裝和預先設定 toojump 開始建置的進階分析的智慧型應用程式。 我們提供 Windows Server 和 Linux 版。 我們提供了 Server 2016 和 Server 2012 的 Windows 版 DSVM。 我們提供 hello DSVM Ubuntu 16.04 LTS 和 OpenLogic 7.2 CentOS 為基礎的 Linux 發行版本上的 Linux 的版本。 

本主題討論您可以執行以 hello 資料科學 VM、 說明一些 hello 使用 hello VM 的重要案例，逐項列出 hello hello Windows 和 Linux 版本上使用的重要功能以及提供指示 tooget 啟動使用它們的方式。

## <a name="what-can-i-do-with-hello-data-science-virtual-machine"></a>我可以 hello Data Science 虛擬機器用來做什麼？
hello 目標 hello Data Science 虛擬機器是在所有技能等級與角色和人事鎖資料科學環境 tooprovide 資料專業人員。 如果您已自行推出相當的環境，此 VM 可為您節省可觀的時間。 相反地，立即在新建立的 VM 執行個體中啟動您的資料科學專案。 

hello 資料科學 VM 是設計，以及設定成使用廣泛的狀況。 您可以在您的專案需要變更時，相應增加或相應減少您的環境。 您會無法 toouse 慣用的語言 tooprogram 資料科學工作。 您可以安裝其他工具，並為您的特定需求自訂 hello 系統。

## <a name="key-scenarios"></a>主要案例
本節提供一些重要的案例，可以部署的 hello 資料科學 VM。

### <a name="preconfigured-analytics-desktop-in-hello-cloud"></a>預先設定 hello 雲端中的分析桌面
hello 資料科學 VM 提供資料科學小組尋找 tooreplace 本機桌面與受管理的雲端桌面的基準組態。 此基準可確保在小組的所有 hello 資料科學家有一致的安裝過程中，使用哪些 tooverify 實驗，並將升級的共同作業。 它也會藉由減少 hello sysadmin 負擔減少成本，以及需要 tooevaluate，安裝及維護 hello hello 時間儲存各種軟體套件所需 toodo 進階分析。  

### <a name="data-science-training-and-education"></a>資料科學訓練和教育
企業訓練與教育學者，通常教導資料科學類別提供虛擬機器映像 tooensure 學生有一致的安裝程式，而且 hello 範例如預期般運作。 hello 資料科學 VM 會隨環境建立一致的安裝程式，以減輕 hello 支援和不相容的挑戰。 這些環境需要 toobe 建置經常，特別是針對較短的定型類別，本質上獲益。

### <a name="on-demand-elastic-capacity-for-large-scale-projects"></a>大型專案的隨選彈性容量
資料科學黑客松 (Hackathon)/競賽或大型資料模型化和探索需要相應放大硬體容量，通常是很短的期間。 hello 資料科學 VM 可協助複寫 hello 資料科學環境快速地視需要，請允許需要強大的運算資源 toobe 實驗的向外延展伺服器上執行。

### <a name="short-term-experimentation-and-evaluation"></a>短期實驗和評估
hello 資料科學 VM 可以使用的 tooevaluate 或工具深入了解 Microsoft R Server，SQL Server，例如 Visual Studio 工具、 Jupyter，深入學習 / ML 工具套件，以及新工具熱門項目 hello 社群搭配最少的安裝工作。 因為 hello 資料科學 VM 可以快速地設定，所以它可以套用其他短期的使用案例，例如複寫已發行的實驗，執行下列逐步解說中線上工作階段或會議教學課程示範。

### <a name="deep-learning"></a>深入學習
hello 資料科學 VM 可以用於定型模型，深入學習演算法使用 GPU （圖形處理單元） 型硬體上。 使用 VM 擴充功能的 Azure 雲端的人員，DSVM 可協助您根據需要 hello 雲端上使用 GPU 基礎硬體。 其中一個可以切換 tooa GPU 定型大型模型時，根據 VM，或需要適當的高速計算時保留 hello 相同的作業系統磁碟。  DSVM hello Windows Server 2016 版本包含預先安裝的 GPU 驅動程式，架構和 GPU 的 hello 深入學習演算法的版本。 在 hello Linux，深入學習 GPU 上才會啟用 hello [Data Science 虛擬機器的 Linux (Ubuntu) 版本](http://aka.ms/dsvm/ubuntu)。 您可以在此情況下所有 hello 深入學習架構都將後援 toohello CPU 模式部署 hello Ubuntu/Windows-2016年版本的資料科學 VM toonon GPU 基礎 Azure 虛擬機器。 之前，針對 Windows Server 2012，我們發行了[深入學習工具組](http://aka.ms/dsvm/deeplearning)，但現在我們建議您針對 Windows 型深入學習工作負載使用 Windows Server 2016。 hello DSVM hello CentOS 為基礎的 Linux 版本包含只有 hello CPU 建立 hello 深入學習工具 CNTK、 Tensorflow （MXNet） 的部分，但是不會顯示 hello GPU 驅動程式和架構，預先安裝。 

## <a name="whats-included-in-hello-data-science-vm"></a>什麼包含在 hello 資料科學 VM？
hello Data Science 虛擬機器都有許多常用的資料科學和深入學習工具已安裝並設定。 它也包含工具，可讓您輕鬆 toowork 與各種 Azure 的資料與分析產品。 您可以瀏覽，並在大型資料集使用 hello Microsoft R Server 或 SQL Server 2016 上建立預測模型。 許多其他工具從 hello 開放原始碼社群和 Microsoft 也會包含在內，以及範例程式碼與筆記型電腦。 hello 表逐項列出並比較 hello hello Windows 和 hello Data Science 虛擬機器的 Linux 版本中包含的主要元件。


| **工具**                                                           | **Windows 版本** | **Linux 版本** |
| :------------------------------------------------------------------ |:-------------------:|:------------------:|
| 已預先安裝熱門套件的 [Microsoft R Open](https://mran.microsoft.com/open/)   |Y                      | Y             |
| [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/) Developer Edition 包括： <br />  &nbsp;&nbsp;&nbsp;&nbsp;* [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started) 平行和分散式高效能 R 架構<br />  &nbsp;&nbsp;&nbsp;&nbsp;* [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction) - Microsoft 的最新 ML 演算法 <br />  &nbsp;&nbsp;&nbsp;&nbsp;* [R 實作](https://msdn.microsoft.com/microsoft-r/operationalize/about)                                            |Y                      | Y <br/> (MicrosoftML 尚無法使用)|
| [Microsoft Office](https://products.office.com/en-us/business/office-365-proplus-business-software) Pro-Plus 含共用啟用 - Excel、Word 和 PowerPoint   |Y                      |N              |
| 已預先安裝熱門套件的 [Anaconda Python](https://www.continuum.io/) 2.7、3.5    |Y                      |Y              |
| 已預先安裝 Julia 語言熱門套件的 [JuliaPro](https://juliacomputing.com/products/juliapro.html)                         |Y                      |Y              |
| 關聯式資料庫                                                            | [SQL Server 2016 SP1](https://www.microsoft.com/sql-server/sql-server-2016) <br/> Developer Edition| [PostgreSQL](https://www.postgresql.org/) |
| 資料庫工具                                                       | * SQL Server Management Studio <br/>* SQL Server Integration Services<br/>* [bcp、sqlcmd](https://docs.microsoft.com/sql/tools/command-prompt-utility-reference-database-engine)<br /> * ODBC/JDBC 驅動程式| * [SQuirreL SQL](http://squirrel-sql.sourceforge.net/) (查詢工具)， <br /> * bcp、sqlcmd <br /> * ODBC/JDBC 驅動程式|
| 可調整資料庫中分析與 SQL Server R 服務 | Y     |N              |
| 採用下列核心的 **[Jupyter Notebook Server](http://jupyter.org/) ，**                                  | Y     | Y |
|     &nbsp;&nbsp;&nbsp;&nbsp;* R | Y | Y |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Python 2.7 & 3.5 | Y | Y |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Julia | Y | Y |
|     &nbsp;&nbsp;&nbsp;&nbsp;* PySpark | N | Y |
|     &nbsp;&nbsp;&nbsp;&nbsp;* [Sparkmagic](https://github.com/jupyter-incubator/sparkmagic) | N | Y (僅限 Ubuntu) |
|     &nbsp;&nbsp;&nbsp;&nbsp;* SparkR     | N | Y |
| JupyterHub (多使用者筆記型電腦伺服器)| N | Y |
| **開發工具、IDE 和程式碼編輯器**| | |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Visual Studio 2017 (Community Edition)](https://www.visualstudio.com/community/) >含 Git Plugin、Azure HDInsight (Hadoop)、Data Lake、SQL Server Data Tools、[Node.js](https://github.com/Microsoft/nodejstools)、[Python](http://aka.ms/ptvs) 和 [Visual Studio R 工具 (RTVS)](http://microsoft.github.io/RTVS-docs/) | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Visual Studio Code](https://code.visualstudio.com/) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [RStudio Desktop](https://www.rstudio.com/products/rstudio/#Desktop) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [RStudio Server](https://www.rstudio.com/products/rstudio/#Server) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [PyCharm](https://www.jetbrains.com/pycharm/) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Atom](https://atom.io/) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Juno (Julia IDE)](http://junolab.org/)| Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* Vim 和 Emacs | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* Git 和 GitBash | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* OpenJDK | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* .Net Framework | Y | N |
| PowerBI Desktop | Y | N |
| Sdk tooaccess Azure 與服務的 Cortana 智慧套件 | Y | Y |
| **資料移動和管理工具** | | |
| &nbsp;&nbsp;&nbsp;&nbsp;* Azure 儲存體總管 | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Azure CLI](https://docs.microsoft.com/cli/azure/overview) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* Azure Powershell | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Azcopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy) | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Adlcopy(Azure Data Lake 儲存體)](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob) | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [DocDB 資料移轉工具](https://docs.microsoft.com/azure/documentdb/documentdb-import-data) | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Microsoft Data Management Gateway](https://msdn.microsoft.com/library/dn879362.aspx)：在 OnPrem 與雲端之間移動資料 | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* Unix/Linux 命令列公用程式 | Y | Y |
| [Apache Drill](http://drill.apache.org) for Data exploration | Y | Y |
| **機器學習工具** |||
| &nbsp;&nbsp;&nbsp;&nbsp;* 與 [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) (R、Python) 整合 | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Xgboost](https://github.com/dmlc/xgboost) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Weka](http://www.cs.waikato.ac.nz/ml/weka/) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Rattle](http://rattle.togaware.com/) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [LightGBM](https://github.com/Microsoft/LightGBM) | N | Y (僅限 Ubuntu) |
| &nbsp;&nbsp;&nbsp;&nbsp;* [H2O](https://www.h2o.ai/h2o/) | N | Y (僅限 Ubuntu) |
| **GPU 型 Deep Learning Tools** |Windows Server 2016 版  |Ubuntu 版 |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Microsoft 辨識工具組 (CNTK)](http://cntk.ai) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Tensorflow](https://www.tensorflow.org/) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [MXNet](http://mxnet.io/) | Y | Y|
| &nbsp;&nbsp;&nbsp;&nbsp;* [Caffe 和 Caffe2](https://github.com/caffe2/caffe2) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Torch](http://torch.ch/) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Theano](https://github.com/Theano/Theano) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Keras](https://keras.io/)| N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [NVidia Digits](https://github.com/NVIDIA/DIGITS) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [CUDA、CUDNN、Nvidia 驅動程式](https://developer.nvidia.com/cuda-toolkit) | Y | Y |
| **巨量資料平台 (僅限 Devtest)**|||
| &nbsp;&nbsp;&nbsp;&nbsp;* 本機獨立 [Spark](http://spark.apache.org/) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* 本機 [Hadoop](http://hadoop.apache.org/) (HDFS、YARN) | N | Y |



## <a name="how-tooget-started-with-hello-windows-data-science-vm"></a>以 Windows 資料科學 VM hello tooget 啟動的方式
* 瀏覽至建立所需的 hello Windows DSVM edition 執行個體
  * [Windows Server 2016 型 DSVM](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft-ads.windows-data-science-vm)
  
  或 
  * [Windows Server 2012 型 DSVM](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/)，以建立所需的 Windows DSVM 版本執行個體 
* 按一下 hello**現在取得 IT**  按鈕。
* 登入 toohello VM 從遠端桌面使用 hello hello VM 的建立時指定的認證。
* 可用，toodiscover 並啟動 hello 工具按一下 hello**啟動**功能表。

## <a name="get-started-with-hello-linux-data-science-vm"></a>開始使用 Linux 資料科學 VM hello
* 建立 hello 預期的執行個體 Linux DSVM 瀏覽過的版本
  * [Ubuntu 型 DSVM](http://aka.ms/dsvm/ubuntu)

  或

  * [OpenLogic CentOS 型 DSVM](http://aka.ms/dsvm/centos)，以建立所需的 Linux DSVM 版本執行個體

  
* 按一下 hello**立即下載** 按鈕。
* 登入 toohello VM 從 SSH 用戶端，例如 Putty 或 SSH 命令，使用您指定當您建立 hello VM 的 hello 認證。
* 在 hello 殼層提示字元中輸入 dsvm 多資訊。
* 圖形化的桌面，下載您的用戶端平台的 hello X2Go 用戶端[這裡](http://wiki.x2go.org/doku.php/doc:installation:x2goclient)遵循 hello Linux 資料科學 VM 文件中的 hello 指示[佈建 hello Linux Data Science 虛擬機器](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).

## <a name="next-steps"></a>後續步驟
### <a name="for-hello-windows-data-science-vm"></a>Hello Windows 資料科學 VM
* 如需有關如何 toorun 特定工具 hello Windows 版本上可用的詳細資訊，請參閱[Microsoft Data Science 虛擬機器的佈建 hello](machine-learning-data-science-provision-vm.md)和
* 如需有關如何 tooperform 各種工作所需的資料科學專案 hello Windows VM 上，請參閱[十個項目，您可以在 hello 資料科學虛擬機器執行](machine-learning-data-science-vm-do-ten-things.md)。

### <a name="for-hello-linux-data-science-vm"></a>Hello Linux 資料科學 VM
* 如需有關如何 toorun 特定工具 hello Linux 版本上可用的詳細資訊，請參閱[Linux Data Science 虛擬機器的佈建 hello](machine-learning-data-science-linux-dsvm-intro.md)。
* 逐步解說中，為您示範如何 tooperform 幾個常見的資料科學工作以 hello Linux VM，請參閱[hello Linux Data Science 虛擬機器上的資料科學](machine-learning-data-science-linux-dsvm-walkthrough.md)。

