---
title: "aaaProvision hello 資料科學 Linux 虛擬機器的 (Ubuntu) 在 Azure 上 |Microsoft 文件"
description: "設定和建立資料科學 Linux 的虛擬機器的 (Ubuntu) Azure toodo 分析和機器學習。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3bab0ab9-3ea5-41a6-a62a-8c44fdbae43b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 037c126c0a35d8065fc89c591089df73d2b91425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-data-science-virtual-machine-for-linux-ubuntu"></a>佈建 hello Data Science 虛擬機器，適用於 Linux (Ubuntu)
hello 適用於 Linux 的 Data Science 虛擬機器是 Ubuntu 基礎虛擬機器映像，可讓您輕鬆 tooget 開始深入學習在 Azure 上使用。 深入學習工具包含：

  * [Caffe](http://caffe.berkeleyvision.org/)︰一種深入學習架構，講求速度、表現度及模組化
  * [Caffe2](https://github.com/caffe2/caffe2)：Caffe 的跨平台版本
  * [運算網路工具組 (CNTK)](https://github.com/Microsoft/CNTK)︰來自 Microsoft Research 的深入學習軟體工具組
  * [H2O](https://www.h2o.ai/)開放原始碼巨量資料平台和圖形化使用者介面
  * [Keras](https://keras.io/)：以 Python 撰寫且適用於 Theano 和 TensorFlow 的高層級類神經網路 API
  * [MXNet](http://mxnet.io/)：彈性、有效率的深入學習程式庫，包含許多語言繫結
  * [NVIDIA DIGITS](https://developer.nvidia.com/digits)：一種圖形化系統，可簡化常見的深入學習工作
  * [TensorFlow](https://www.tensorflow.org/)︰Google 提供的機器智慧開放原始碼程式庫
  * [Theano](http://deeplearning.net/software/theano/)：一種 Python 程式庫，可定義、最佳化和有效地評估涉及多維陣列的數學運算式
  * [Torch](http://torch.ch/)︰廣泛支援機器學習演算法的科學運算架構
  * CUDA、 cuDNN 和 hello NVIDIA 驅動程式
  * 許多範例 Jupyter 筆記本

所有的程式庫是 hello GPU 版本中，不過它們也會在 hello CPU 上執行。

hello Data Science 虛擬機器，適用於 Linux 也包含常用的工具，用於資料科學和開發活動，包括：

* Microsoft R Server Developer Edition 含 Microsoft R Open
* Anaconda Python 散發套件 (2.7 版和 3.5 版)，包括常用的資料分析程式庫
* JuliaPro - 使用受歡迎科學和資料分析程式庫的 Julia 語言策劃分佈
* 獨立 Spark 執行個體和單一節點 Hadoop (HDFS、Yarn)
* JupyterHub - 多使用者的 Jupyter Notebook 伺服器，支援 R、Python、PySpark、Julia 核心
* Azure 儲存體總管
* 用於管理 Azure 資源的 Azure 命令列介面 (CLI)
* 機器學習工具
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit)︰快速的機器學習系統，支援像是線上、雜湊，allreduce、簡化、learning2search、主動和互動式學習的技術
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/)︰提供快速且正確的推進式決策樹實作的工具
  * [Rattle](http://rattle.togaware.com/)︰一種圖形化工具，可幫助您輕鬆地開始使用 R 中的資料分析和機器學習
  * [LightGBM](https://github.com/Microsoft/LightGBM)︰快速、分散式的高效能漸層提升架構
* Java、Python、node.js、Ruby、PHP 中的 Azure SDK
* R 和 Python 語言的程式庫，可用於 Azure Machine Learning 和其他 Azure 服務
* 開發工具和編輯器 (RStudio、PyCharm、IntelliJ、Emacs、vim)


執行資料科學涉及反覆進行一連串的工作︰

1. 尋找、載入和前置處理資料
2. 建置和測試模型
3. 部署的智慧型應用程式中的耗用量的 hello 模型

資料科學家可以使用各種工具 toocomplete 這些工作。 它可以是相當耗時 toofind hello 適當 hello 軟體版本，然後並 toodownload，編譯時，安裝這些版本。

hello 適用於 Linux 的 Data Science 虛擬機器可以大幅簡化此項負擔。 它使用 toojump 開始分析專案。 它可讓您 toowork 上不同的語言，包括 R、 Python、 SQL、 Java 和 c + + 中的工作。 hello hello VM 中包含 Azure SDK 可讓您 toobuild hello Microsoft 雲端平台，在 Linux 上使用各種服務的應用程式。 此外，您有存取 tooother 語言，例如 Ruby、 Perl、 PHP 和 node.js，也會預先安裝。

這個資料科學 VM 映像沒有任何軟體費用。 您付費只 hello Azure 硬體使用量費用，都會根據 hello hello 您佈建的虛擬機器大小進行評估。 詳細 hello 計算費用位於 hello [hello Azure Marketplace 上的 VM 清單頁面](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm/)。

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>其他版本的 hello Data Science 虛擬機器
A [CentOS](machine-learning-data-science-linux-dsvm-intro.md)影像也會提供、 與許多 hello 相同工具會以 hello Ubuntu 映像。 亦提供 [Windows](machine-learning-data-science-provision-vm.md) 映像。

## <a name="prerequisites"></a>必要條件
您必須先具有 Azure 訂用帳戶，才可以建立 Linux 適用的資料科學虛擬機器。 tooobtain 其中一個，請參閱[取得 Azure 免費試用](https://azure.microsoft.com/free/)。

## <a name="create-your-data-science-virtual-machine-for-linux"></a>建立 Linux 適用的資料科學虛擬機器
以下是 hello 步驟 toocreate hello Data Science 虛擬機器，適用於 Linux 的執行個體：

1. 瀏覽 toohello 虛擬機器上 hello 列出[Azure 入口網站](https://portal.azure.com/#create/microsoft-ads.linux-data-science-vm-ubuntulinuxdsvmubuntu)。
2. 按一下**建立**（底部 hello） hello 精靈 toobring。![設定資料-科學-vm](./media/machine-learning-data-science-dsvm-ubuntu-intro/configure-data-science-virtual-machine.png)
3. hello 下列各節提供使用 toocreate hello Microsoft Data Science 虛擬機器的每個 hello 步驟 hello 精靈 （列舉 hello 方 hello 前面圖） 中的 hello 輸入。 以下是 hello 所需的輸入 tooconfigure 每個步驟：
   
   a. **基本**：
   
   * **名稱**：您建立的資料科學伺服器名稱。
   * **使用者名稱**：第一個帳戶登入識別碼。
   * **密碼**︰第一個帳戶密碼 (您可以使用 SSH 公開金鑰來代替密碼)。
   * **訂用帳戶**： 如果您有多個訂閱，選取 hello 上哪些 hello 機器是 toobe 建立，並計費。 您必須有此訂用帳戶的資源建立權限。
   * **資源群組**：您可以建立新群組或使用現有的群組。
   * **位置**: hello 選取最適合的資料中心。 通常它是 hello 資料中心有大部分的資料，或為最接近 tooyour 最快的網路存取的實體位置。
   
   b. ：
   
   * 選取其中一個符合您的功能需求和成本條件約束的 hello 伺服器類型。 選取**檢視所有**toosee VM 大小的更多選擇。 針對 GPU 訓練選取一個 NC 類別的 VM。
   
   c. **設定**：
   
   * **磁碟類型**：如果您偏好固態硬碟 (SSD)，請選擇 [進階]， 否則請選擇 [標準]。 GPU VM 需要標準磁碟。
   * **儲存體帳戶**： 您可以在您的訂閱中建立新的 Azure 儲存體帳戶，或使用現有 hello hello 選擇的相同位置**基本概念**hello 精靈的步驟。
   * **其他參數**： 在大部分情況下，您只使用 hello 預設值。 hello 特定欄位的說明 tooconsider 非預設值，暫留在 hello 資訊連結。
   
   d. **摘要**：
   
   * 請確認您輸入的所有資訊都正確無誤。
   
   e. ：
   
   * toostart hello 佈建中，按一下**購買**。 Toohello 使用條款 hello 交易時，會提供的連結。 hello VM 並沒有任何額外的費用，超出您選擇在 hello hello 伺服器大小的 hello 計算**大小**步驟。

hello 佈建時間大約 5-10 分鐘。 hello 佈建的 hello 狀態會顯示在 hello Azure 入口網站。

## <a name="how-tooaccess-hello-data-science-virtual-machine-for-linux"></a>Tooaccess 適用於 Linux hello Data Science 虛擬機器的方式
在建立 VM 的 hello 之後, 您可以使用 SSH 登入 tooit。 使用您在 hello hello 帳戶認證**基本概念**> 一節的步驟 3 的 hello 文字殼層介面。 在 Windows 上，您可以下載 SSH 用戶端工具，例如 [Putty](http://www.putty.org)。 如果您偏好的圖形化的桌面 （X Windows 系統），您可以使用 X11 轉寄 Putty 上或安裝 hello X2Go 用戶端。

> [!NOTE]
> hello X2Go 用戶端執行會明顯優於 X11 轉寄測試。 我們建議使用 hello X2Go 用戶端桌面圖形化介面。
> 
> 

## <a name="installing-and-configuring-x2go-client"></a>安裝和設定 X2Go 用戶端
hello Linux VM 已佈建 X2Go 伺服器與準備好 tooaccept 用戶端連線。 tooconnect toohello Linux VM 圖形化的桌面，請勿 hello 遵循您的用戶端上：

1. 下載並安裝來自您用戶端的平台的 hello X2Go client [X2Go](http://wiki.x2go.org/doku.php/doc:installation:x2goclient)。    
2. 執行 hello X2Go 用戶端，並選取**新的工作階段**。 會開啟具有多個索引標籤的組態視窗。 輸入下列設定參數的 hello:
   * **[工作階段] 索引標籤**：
     * **主機**: hello 主機名稱或 IP 位址，您的 Linux 資料科學 VM。
     * **登入**: hello Linux VM 上的使用者名稱。
     * **SSH 連接埠**： 保留 22，hello 預設值。
     * **工作階段類型**： 變更 hello 值 tooXFCE。 Hello Linux VM 目前僅支援 XFCE 桌面。
   * **媒體 索引標籤**： 您可以關閉聲音支援和用戶端列印，如果您不需要 toouse 它們。
   * **共用資料夾**： 如果您想從您的用戶端機器 hello Linux VM 上裝載的目錄，新增您想使用此索引標籤上的 VM hello tooshare hello 用戶端機器目錄。

您使用 hello SSH 用戶端或 XFCE hello X2Go 用戶端透過圖形化的桌面登入 toohello VM 之後，您就準備好 toostart 使用 hello 工具所安裝及設定 hello VM 上。 在 XFCE，您可以看到應用程式的捷徑功能表和桌面圖示的許多 hello 工具。

## <a name="tools-installed-on-hello-data-science-virtual-machine-for-linux"></a>Hello Data Science 虛擬機器上安裝適用於 Linux 工具
### <a name="deep-learning-libraries"></a>深入學習程式庫

#### <a name="cntk"></a>CNTK
hello Microsoft 認知 Toolki-也稱為 CNTK-是開放原始碼，深入了解工具組。 Hello 根和 py35 Conda 環境中使用 Python 繫結。 它也會有已在 hello 路徑的命令列工具 (cntk)。

您可以在 JupyterHub 中找到範例 Python 筆記本。 toorun 在 hello 命令列中的基本範例會執行下列命令在 hello 介面中的 hello:

    cd /home/[USERNAME]/notebooks/CNTK/HelloWorld-LogisticRegression
    cntk configFile=lr_bs.cntk makeMode=false command=Train

如需詳細資訊，請參閱 hello CNTK 區段[GitHub](https://github.com/Microsoft/CNTK)，和 hello [CNTK wiki](https://github.com/Microsoft/CNTK/wiki)。

#### <a name="caffe"></a>Caffe
Caffe 是深層學習架構從 hello Berkeley 願景與學習中心。 它位於 /opt/caffe。 您可以在 /opt/caffe/examples 中找到範例。

#### <a name="caffe2"></a>Caffe2
Caffe2 是來自 Facebook (以 Caffe 為基礎而建置) 的深入學習架構。 Python 2.7 hello Conda 根環境中使用。 tooactivate 它從 hello 命令介面執行 hello 下列：

    source /anaconda/bin/activate root

您可以在 JupyterHub 找到一些範例筆記本。

#### <a name="h2o"></a>H2O
H2O 是快速、記憶體內的分散式機器學習和預測性分析平台。 Python 封裝會安裝在這兩種 hello 根和 py35 Anaconda 環境。 同時也會安裝 R 封裝。 從執行 hello commandline toostart H2O `java -jar /dsvm/tools/h2o/current/h2o.jar`; 有各種[命令列選項](http://docs.h2o.ai/h2o/latest-stable/h2o-docs/starting-h2o.html#from-the-command-line)您可能想 tooconfigure。 可以藉由瀏覽 toohttp://localhost:54321 tooget 啟動存取 hello 流程 Web UI。 您也可以在 JupyterHub 找到範例筆記本。

#### <a name="keras"></a>Keras
Keras 是以 Python 撰寫的高層級類神經網路 API，可在 Tensorflow 或 Theano 上執行。 在 hello 根和 py35 Python 環境中使用。 

#### <a name="mxnet"></a>MXNet
MXNet 是兼具效率和彈性的深入學習架構。 它有包含在 hello DSVM R，並將 Python 繫結。 範例筆記本內含在 JupyterHub 中，而範例程式碼則位於 /dsvm/samples/mxnet。

#### <a name="nvidia-digits"></a>NVIDIA DIGITS
hello NVIDIA 深入學習 GPU 訓練系統，稱為 數字，為系統 toosimplify 常見深入學習工作，例如管理資料、 設計和 GPU 在系統上，定型類神經網路和監視的進階視覺化的即時效能。 

DIGITS 是做為服務 (稱為 digits) 提供。 啟動 hello 服務，並瀏覽 toohttp://localhost:5000 tooget 啟動。

數字也會安裝為 Python 模組中 hello Conda 根環境。

#### <a name="tensorflow"></a>TensorFlow
TensorFlow 是 Google 的深入學習程式庫。 它是使用資料流程圖進行數值計算的開放原始碼軟體程式庫。 TensorFlow 位於 hello py35 Python 環境，並將某些範例筆記本併入 JupyterHub。

#### <a name="theano"></a>Theano
Theano 是能進行高效數值計算的 Python 程式庫。 在 hello 根和 py35 Python 環境中使用。 

#### <a name="torch"></a>Torch
Torch 是廣泛支援機器學習演算法的科學運算架構。 它可在 /dsvm/tools/torch，而且 hello th 互動式工作階段和 luarocks 封裝管理員可在 hello 命令列。 範例位於 /dsvm/samples/torch。

PyTorch 也會提供 hello 根 Anaconda 環境。 範例位於 /dsvm/samples/pytorch。

### <a name="microsoft-r-server"></a>Microsoft R 伺服器
R 是其中一種 hello 進行資料分析和機器學習最受歡迎的語言。 如果您想要您的分析 toouse R，hello VM 會有 Microsoft R Server （女士） 以 hello Microsoft R Open (MRO) 和運算核心程式庫 (MKL)。 hello MKL 最佳化分析的演算法中常見的數學運算作業。 MRO 為 100%相容 CRAN R 和任何 hello R 文件庫中 CRAN 發行可以安裝在 hello MRO 上。 MRS 可讓您將 R 模型調整和實施到 Web 服務。 您可以編輯您的 R 程式中的 hello 預設編輯器，例如 RStudio、 vi 或 Emacs 之一。 如果您使用 hello Emacs 編輯器 中，請注意該 hello Emacs 套件 ESS （Emacs 來說統計資料），這可簡化使用 R 檔案內 hello Emacs 編輯器 中，已預先安裝。

toolaunch R 主控台中，您只需要輸入**R** hello shell 中。 這會帶您 tooan 互動式環境。 toodevelop R 程式，您通常會使用 vi，Emacs 等編輯器，然後執行 R 中的 hello 指令碼使用 RStudio、 您的完整圖形化的 IDE 環境 toodevelop R 程式。

另外還有 tooinstall hello 的 R 指令碼[前 20 R 封裝](http://www.kdnuggets.com/2015/06/top-20-r-packages.html)如果您想要。 在 hello R 互動式介面，您可以輸入 （如所述） 之後，就可以執行這個指令碼**R** hello shell 中。  

### <a name="python"></a>Python
為了能夠使用 Python 進行開發，我們已安裝了 Anaconda Python 散佈 2.7 與 3.5。 此分佈包含 hello 基底 Python 以及大約 300 個 hello 最受歡迎的數學、 工程團隊和資料分析封裝。 您可以使用 hello 預設文字編輯器。 此外，您也可以使用 Spyder，這是與 Anaconda Python 散發套件配套的 Python IDE。 Spyder 需要圖形化桌面或 X11 轉寄。 快顯 tooSpyder hello 圖形桌面中提供。

由於我們有 Python 2.7 和 3.5，您需要 toospecifically 啟動您想在 hello 上的 toowork 目前工作階段所需的 hello Python 版本 （conda 環境）。 hello 啟動程序設定 Python 的 hello 路徑變數 toohello 所需的的版本。

tooactivate hello Python 2.7 conda 環境中，從 hello 命令介面執行 hello 下列：

    source /anaconda/bin/activate root

Python 2.7 安裝於「/anaconda/bin」 。

tooactivate hello Python 3.5 conda 環境中，從 hello 命令介面執行 hello 下列：

    source /anaconda/bin/activate py35


Python 3.5 安裝於 */anaconda/envs/py35/bin*上。

tooinvoke Python 互動式工作階段，只要輸入**python** hello shell 中。 如果您在圖形化介面，或有 X11 轉寄集組成，您可以輸入**pycharm** toolaunch hello PyCharm Python IDE。

tooinstall 額外的 Python 程式庫需要 toorun```conda```或````pip````sudo 下命令，並提供 hello Python 封裝管理員的完整路徑 （conda 或 pip） tooinstall toohello 正確 Python 環境。 例如：

    sudo /anaconda/bin/pip install <package> #for Python 2.7 environment
    sudo /anaconda/envs/py35/bin/pip install <package> # for Python 3.5 environment


### <a name="jupyter-notebook"></a>Jupyter 筆記本
hello Anaconda 發佈也隨附 Jupyter 筆記本、 環境 tooshare 程式碼和分析。 hello Jupyter 筆記本是透過 JupyterHub 存取。 您可以使用本機 Linux 使用者名稱和密碼來登入。

hello Jupyter 筆記本伺服器已預先設定 Python 2、 Python 3 與 R 核心。 沒有名為"Jupyter 筆記本"toolaunch hello 瀏覽器 tooaccess hello 筆記本伺服器桌面的圖示。 如果您是透過 SSH 或 X2Go 用戶端 hello VM 上，您也可以造訪[https://localhost:8000 /](https://localhost:8000/) tooaccess hello Jupyter 筆記本伺服器。

> [!NOTE]
> 如果您收到任何憑證警告，請繼續。
> 
> 

您可以從任何主機存取 hello Jupyter 筆記本伺服器。 只要輸入 https://\<VM DNS 名稱或 IP 位址\>:8000/

> [!NOTE]
> 連接埠 8000 預設會開啟在 hello 防火牆 hello VM 已佈建時。
> 
> 

我們有封裝範例筆記本-一個在 Python，一個在。之後您使用本機 Linux 使用者名稱和密碼驗證 toohello Jupyter 筆記本，您可以在 hello 筆記本首頁上看到 hello 連結 toohello 範例。 您可以選取來建立新的記事本**新增**，然後 hello 適當的語言的核心。 如果您沒有看見 hello**新增**按鈕，再按一下 hello **Jupyter**在 hello hello 筆記本伺服器的最上層左的 toogo toohello 首頁上的圖示。

### <a name="apache-spark-standalone"></a>獨立 Apache Spark 
Apache Spark 的獨立執行個體是預先安裝在您開發在本機上的 Spark 應用程式第一次才能測試和部署大型叢集上的 Linux DSVM toohelp hello。 您可以透過 hello Jupyter 核心執行 PySpark 程式。 當您開啟 Jupyter 並按一下 [新增] 按鈕 hello，您會看到一份可用的核心。 hello"Spark-Python 」 是可讓您建置 Spark 使用 Python 語言的應用程式的 hello PySpark 核心。 您也可以使用類似您二手 PyCharm 或 Spyder toobuild Python IDE 程式。 因為這是獨立執行個體，hello 呼叫用戶端程式中執行的 hello Spark 堆疊。 如此便可更快速並輕鬆 tootroubleshoot 問題比較 toodeveloping 的 Spark 叢集。 

您可以在 hello Jupyter ($HOME/筆記本/SparkML/pySpark) 主目錄下的 hello"SparkML"目錄中找到的 Jupyter 上提供範例 PySpark 筆記本。 

如果您是針對 Spark 在 R 中進行程式設計，您可以使用 Microsoft R 伺服器、SparkR 或 sparklyr。 

Microsoft R Server 中的 Spark 內容中執行，您必須之前 toodo 一次安裝程式步驟 tooenable 本機的單一節點 Hadoop HDFS 和 Yarn 執行個體。 根據預設，Hadoop 服務已安裝，但在 hello DSVM 上停用。 順序 tooenable 中，您需要 toorun hello 做為根 hello 第一次下列命令：

    echo -e 'y\n' | ssh-keygen -t rsa -P '' -f ~hadoop/.ssh/id_rsa
    cat ~hadoop/.ssh/id_rsa.pub >> ~hadoop/.ssh/authorized_keys
    chmod 0600 ~hadoop/.ssh/authorized_keys
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa.pub
    chown hadoop:hadoop ~hadoop/.ssh/authorized_keys
    systemctl start hadoop-namenode hadoop-datanode hadoop-yarn

您可以停止 hello Hadoop 相關服務，您不需要它們執行時````systemctl stop hadoop-namenode hadoop-datanode hadoop-yarn````展示如何 toodevelop 和測試 MRS 遠端 Spark 內容 （即 hello 獨立 Spark 執行個體上 hello DSVM） 中的，而且提供 hello中可用的範例`/dsvm/samples/MRS`目錄。 

### <a name="ides-and-editors"></a>IDE 和編輯器
您可以選擇數個程式碼編輯器。 這包括 vi/VIM、Emacs、PyCharm、RStudio 和 IntelliJ。 IntelliJ、 RStudio 和 PyCharm 圖形編輯器，而且需要您 toobe 登入 tooa 圖形桌面 toouse 它們。 這些編輯器有桌面和應用程式功能表快速鍵 toolaunch 它們。

**VIM** 和 **Emacs** 是文字型編輯器。 Emacs，我們已安裝附加套件呼叫 Emacs 來說統計資料 (ESS)，可使用 R hello Emacs 編輯器中更容易。 如需詳細資訊，請參閱 [ESS](http://ess.r-project.org/)。

**LaTex**透過 hello texlive 封裝及 Emacs 附加元件安裝[auctex](https://www.gnu.org/software/auctex/manual/auctex/auctex.html)套件，可簡化撰寫內 Emacs LaTex 文件。  

### <a name="databases"></a>資料庫

#### <a name="graphical-sql-client"></a>圖形化 SQL 用戶端
**松鼠 SQL**，圖形化的 SQL 用戶端已提供 tooconnect toodifferent 資料庫 （例如 Microsoft SQL Server 和 MySQL） 以及 toorun SQL 查詢。 您可以將它執行從圖形化的桌面工作階段 （例如使用 hello X2Go 用戶端）。 tooinvoke 松鼠 SQL，您可以啟動從 hello hello 桌面上的圖示，或執行 hello hello shell 之上，下列命令。

    /usr/local/squirrel-sql-3.7/squirrel-sql.sh

Hello 第一次使用之前，設定您的驅動程式和資料庫的別名。 hello JDBC 驅動程式會位於：

*/usr/share/java/jdbcdrivers*

如需詳細資訊，請參閱 [SQuirrel SQL](http://squirrel-sql.sourceforge.net/index.php?page=screenshots)。

#### <a name="command-line-tools-for-accessing-microsoft-sql-server"></a>存取 Microsoft SQL Server 用的命令列工具
適用於 SQL Server 的 hello ODBC 驅動程式套件也會隨附兩個命令列工具：

**bcp**: hello bcp 公用程式在大量複製的 Microsoft SQL Server 執行個體和資料檔案之間的資料以使用者指定的格式。 hello bcp 公用程式可以使用的 tooimport 大量新資料列到 SQL Server 資料表或資料表至資料檔案的 tooexport 資料。 tooimport 資料到資料表，您必須使用為該資料表中，建立格式檔案，或了解 hello 資料表結構的 hello hello 適用於其資料行的資料類型。

如需詳細資訊，請參閱 [連接 bcp](https://msdn.microsoft.com/library/hh568446.aspx)。

**sqlcmd**： 您可以輸入與 hello sqlcmd 公用程式，以及系統程序的 TRANSACT-SQL 陳述式和指令碼在 hello 命令提示字元的檔案。 這個公用程式利用 ODBC tooexecute TRANSACT-SQL 批次。

如需詳細資訊，請參閱 [使用 sqlcmd 連接](https://msdn.microsoft.com/library/hh568447.aspx)。

> [!NOTE]
> 此公用程式在 Linux 和 Windows 平台之間有一些差異。 請參閱 hello 文件，如需詳細資訊。
> 
> 

#### <a name="database-access-libraries"></a>資料庫存取程式庫
沒有可使用 R，並將 Python tooaccess 資料庫中的媒體櫃。

* 在 R hello **RODBC**封裝或**dplyr**封裝可讓您 tooquery 或 hello 資料庫伺服器上執行 SQL 陳述式。
* 以 Python，hello **pyodbc** hello 基礎層程式庫提供使用 ODBC 的資料庫存取權。  

### <a name="azure-tools"></a>Azure 工具
hello VM 上安裝下列 Azure tools 的 hello:

* **Azure 命令列介面**: hello Azure CLI toocreate 可讓您和管理 Azure 資源，透過殼層命令。 tooinvoke hello Azure tools，只要輸入**azure 說明**。 如需詳細資訊，請參閱 hello [Azure CLI 文件頁面](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。
* **Microsoft Azure 儲存體總管**: Microsoft Azure 儲存體總管是透過您儲存在 Azure 儲存體帳戶和 tooupload 和下載資料 tooand 從 Azure blob 中的 hello 物件使用的 toobrowse 圖形化工具。 您可以從 hello 桌面捷徑圖示來存取儲存體總管。 從殼層命令提示字元叫用它則是輸入 **StorageExplorer**。 您需要從 X2Go 用戶端登入 toobe 或者 X11 轉寄組上。
* **Azure 程式庫**: hello 以下是一些 hello 預先安裝的程式庫。
  
  * **Python**: hello Azure 相關程式庫中已安裝的 Python **azure**， **azureml**， **pydocumentdb**，和**pyodbc**. 與 hello 前三個程式庫，您可以存取 Azure 儲存體服務、 Azure 機器學習和 Azure Cosmos DB （在 Azure 上的 NoSQL 資料庫）。 hello 第四個程式庫，pyodbc （以及 hello Microsoft ODBC driver for SQL Server)，可讓存取 tooSQL 伺服器，Azure SQL Database 和 Azure SQL 資料倉儲來自 Python 使用 ODBC 介面。 輸入**pip 清單**toosee 所有 hello 列出文件庫。 此命令在兩個 hello Python 2.7 和 3.5 環境是確定 toorun。
  * **R**: hello Azure 相關程式庫中 R 安裝**AzureML**和**RODBC**。
  * **Java**: hello Azure Java 文件庫清單位於 hello 目錄**/dsvm/sdk/AzureSDKJava** hello VM 上。 hello 關鍵的程式庫是 Azure 儲存體和管理應用程式開發介面、 Azure Cosmos DB、 和 JDBC 驅動程式適用於 SQL Server。  

您可以存取 hello [Azure 入口網站](https://portal.azure.com)從 hello 預先安裝 Firefox 瀏覽器。 在 hello Azure 入口網站，您可以建立、 管理及監視 Azure 資源。

### <a name="azure-machine-learning"></a>Azure Machine Learning
Azure Machine Learning 是完全受管理的雲端服務，可讓您 toobuild、 部署和共用的預測分析解決方案。 您可以從 Azure Machine Learning Studio 中建置實驗和模型。 可以從 hello data science 虛擬機器上的網頁瀏覽器中存取造訪[Microsoft Azure Machine Learning](https://studio.azureml.net)。

TooAzure Machine Learning Studio 在您登入之後，您必須存取 tooan 實驗，您可以在其中建立 hello 機器學習演算法的邏輯流程的畫布。 您也必須裝載於 Azure Machine Learning 存取 tooa Jupyter 筆記本，並可以緊密地與 Machine Learning Studio 中的 hello 實驗。 實施 hello 機器學習模型，您已建立根據它們包裝在 web 服務介面。 這可讓從 hello 機器學習模型的任何語言 tooinvoke 預測中撰寫的用戶端。 如需詳細資訊，請參閱 hello[機器學習服務文件](https://azure.microsoft.com/documentation/services/machine-learning/)。

您可以也 hello VM，在建置您的模型中 R 或 Python，然後再將它部署在 Azure Machine Learning 的生產環境中。 我們已經在 R 安裝程式庫 (**AzureML**)，並將 Python (**azureml**) tooenable 這項功能。

如需在 R 和 Python toodeploy 模型 Azure 機器學習到如何資訊，請參閱[十個項目，您可以在 hello 資料科學虛擬機器執行](machine-learning-data-science-vm-do-ten-things.md)（特別是，hello > 一節 < 建置模型使用 R 或 Python 和實施這些使用 Azure Machine Learning"）。

> [!NOTE]
> 這些指示所撰寫的 hello 資料科學 VM hello Windows 版本。 但是有提供有關部署模型 tooAzure 機器學習的 hello 資訊適用 toohello Linux VM。
> 
> 

### <a name="machine-learning-tools"></a>機器學習工具
hello VM 隨附幾個機器學習工具和預先編譯和預先安裝在本機的演算法。 其中包含：

* **Vowpal Wabbit**：快速線上學習演算法。
* **xgboost**：提供最佳化推進式決策樹演算法的工具。
* **Rattle**：以 R 為基礎的圖形化工具，可輕鬆地進行資料瀏覽和模組化。
* **Python**：Anaconda Python 會與含有像是 Scikit-learn 的程式庫的機器學習演算法進行配套。 您可以安裝其他程式庫使用 hello`pip install`命令。
* **LightGBM**︰以決策樹演算法為基礎的一種快速、分散式的高效能漸層提升架構。
* **R**： 豐富的機器學習服務函數可用於。部份 hello 預先安裝的程式庫將 lm、 glm、 randomForest、 rpart。 您可以執行下列命令來安裝其他程式庫：
  
        install.packages(<lib name>)

以下是一些 hello 的其他資訊第一次三個機器學習工具 hello 清單中。

#### <a name="vowpal-wabbit"></a>Vowpal Wabbit
Vowpal Wabbit 是一個機器學習系統，其會使用像是線上、雜湊，allreduce、簡化、learning2search、主動和互動式學習的技術。

toorun hello 工具上非常基本的範例中，請勿 hello 遵循：

    cp -r /dsvm/tools/VowpalWabbit/demo vwdemo
    cd vwdemo
    vw house_dataset

該目錄中有其他更大的示範。 如需有關 VW 的詳細資訊，請參閱[GitHub 的這一節](https://github.com/JohnLangford/vowpal_wabbit)，和 hello [Vowpal Wabbit wiki](https://github.com/JohnLangford/vowpal_wabbit/wiki)。

#### <a name="xgboost"></a>XGBoost
這是針對推進式決策 (樹) 演算法設計及最佳化的的程式庫。 此文件庫 hello 目標在於機器 toohello 極端 toopush hello 計算限制需要 tooprovide 大型的樹狀結構促進可擴充、 可攜，而且精確。

它提供了命令列以及 R 程式庫。

toouse 在 R 中的此程式庫，您可以啟動互動式的 R 工作階段 (只要輸入**R** hello shell 中)，以及負載 hello 程式庫。

以下是簡單的範例，您可以在 R 提示字元中執行︰

    library(xgboost)

    data(agaricus.train, package='xgboost')
    data(agaricus.test, package='xgboost')
    train <- agaricus.train
    test <- agaricus.test
    bst <- xgboost(data = train$data, label = train$label, max.depth = 2,
                    eta = 1, nthread = 2, nround = 2, objective = "binary:logistic")
    pred <- predict(bst, test$data)

toorun hello xgboost 命令列中，以下是在 hello 介面中的 hello 命令 tooexecute:

    cp -r /dsvm/tools/xgboost/demo/binary_classification/ xgboostdemo
    cd xgboostdemo
    xgboost mushroom.conf


.Model 檔案會寫入指定的 toohello 目錄。 如需此示範範例的相關資訊，請參閱 [GitHub](https://github.com/dmlc/xgboost/tree/master/demo/binary_classification)。

如需 xgboost 的詳細資訊，請參閱 hello [xgboost 文件頁面](https://xgboost.readthedocs.org/en/latest/)，且其[GitHub 儲存機制](https://github.com/dmlc/xgboost)。

#### <a name="rattle"></a>Rattle
祕 (hello **R** **A**nalytical **T**ool **T**o **L**贏得**E**asily) 會使用以 GUI 為基礎的資料探索和模型。 它會顯示統計和視覺化資料，可以輕易地建立模型的轉換資料的摘要，建置 hello 資料從受監督和不受監督模式，以圖形方式顯示 hello 的模型效能並分數新資料集。 它也會產生 R 程式碼中，複寫 hello UI 中的 hello 作業可以直接在 R 中執行，或做為起點來進行進一步分析。

祕 toorun，您會需要 toobe 圖形桌面登入工作階段中。 在 hello 終端機中，輸入```R```tooenter hello R 環境。 在 hello R 提示字元中輸入下列命令的 hello:

    library(rattle)
    rattle()

現在，將會開啟具有一組索引標籤的圖形化介面。 以下是的 hello 快速入門中祕需要 toouse 範例天氣資料集的步驟，並建立模型。 在某些 hello 執行下列步驟，您會提示的 tooautomatically 安裝，並載入 hello 系統還沒有某些必要的 R 封裝。

> [!NOTE]
> 如果您沒有存取 tooinstall hello 套件 hello 系統目錄 （hello 預設值） 中，您可能會針對您 R 主控台視窗 tooinstall 封裝 tooyour 個人文件庫中看到的提示。 如果您看到這些提示，請回答 「是」  。
> 
> 

1. 按一下 [Execute (執行)] 。
2. 對話方塊會出現，詢問您您 toouse hello 範例天氣資料集。 按一下**是**tooload hello 範例。
3. 按一下 hello**模型** 索引標籤。
4. 按一下**Execute** toobuild 決策樹。
5. 按一下**繪製**toodisplay hello 決策樹。
6. 按一下 hello**樹系**選項按鈕，然後按一下  **Execute** toobuild 隨機樹系。
7. 按一下 hello**評估** 索引標籤。
8. 按一下 hello**風險**選項按鈕，然後按一下  **Execute** toodisplay 兩風險 （累計） 效能繪圖。
9. 按一下 hello**記錄** 索引標籤 tooshow hello 產生 hello 上述操作的 R 程式碼。
   (由於 tooa bug 的祕 hello 目前版本中，您需要 tooinsert  *#* 字元前面*匯出此記錄檔...* hello 文字 hello 記錄檔中。)
10. 按一下 hello**匯出**按鈕 toosave hello R 指令碼檔名為*weather_script。R* toohello 主資料夾。

您可以結束祕和。現在您可以修改產生的 hello R 指令碼，或使用它，因為它是 toorun 它隨時 toorepeat hello 祕 UI 中完成的所有項目。 特別為初學者所設計在 R 中，這是可以輕鬆地 tooquickly 執行分析和機器學習在簡單的圖形化介面中，自動產生程式碼中 R toomodify 時及/或深入了解。

## <a name="next-steps"></a>後續步驟
以下是如何繼續進行學習和探索的方式：

* hello [hello Data Science 虛擬機器，適用於 Linux 上的資料科學](machine-learning-data-science-linux-dsvm-walkthrough.md)逐步解說將示範如何 tooperform 幾個常見的資料科學工作以 hello 這裡佈建的 Linux 資料科學 VM。 
* 瀏覽的 hello 各種資料科學工具上的嘗試進行這篇文章中所述的 hello 工具 hello 資料科學 VM。 您也可以執行*dsvm 多資訊*hello shell 之上，如需 hello VM 上安裝的 hello 工具基本簡介和指標 toomore 資訊 hello 虛擬機器內。  
* 了解如何使用有系統地 toobuild 端對端分析解決方案 hello[資料科學的小組流程](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)。
* 請瀏覽 hello [Cortana 分析圖庫](http://gallery.cortanaanalytics.com)的機器學習服務與資料分析範例，使用 hello Cortana Analytics suite 這套。

