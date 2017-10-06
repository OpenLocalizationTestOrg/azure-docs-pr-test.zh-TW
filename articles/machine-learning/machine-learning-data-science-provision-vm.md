---
title: "aaaProvision hello Microsoft Data Science 虛擬機器 |Microsoft 文件"
description: "在 Azure 上設定和建立資料科學虛擬機器以進行分析和機器學習。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e1467c0f-497b-48f7-96a0-7f806a7bec0b
ms.service: machine-learning
ms.workload: data-services
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 907a3bdc7e480d05e8e245f5e50d632900fcf471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-microsoft-data-science-virtual-machine"></a>佈建 hello Microsoft Data Science 虛擬機器
hello Microsoft Data Science 虛擬機器是 Windows Azure 虛擬機器 (VM) 映像預先安裝並設定通常用於資料分析和機器學習的數個常用工具。 包含 hello 工具包括：

* Microsoft R Server Developer Edition
* Anaconda Python 散佈
* Jupyter notebook (使用 R、Python 核心)
* Visual Studio Community 版本
* Power BI 桌面
* SQL Server 2016 Developer Edition
* 機器學習服務與資料分析工具
  * [運算網路工具組 (CNTK)](https://github.com/Microsoft/CNTK)︰來自 Microsoft Research 的深層學習軟體工具組。
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit)︰快速的機器學習系統，支援像是線上、雜湊，allreduce、簡化、learning2search、主動和互動式學習的技術。
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/)︰提供快速且正確的推進式決策樹實作的工具。
  * [祕](http://rattle.togaware.com/)(輕鬆 hello R 分析工具 tooLearn): 一種工具，可讓您開始使用資料分析和機器學習中很容易，與以 GUI 為基礎的資料瀏覽、 R 和自動產生的 R 程式碼與模型化。
  * [mxnet](https://github.com/dmlc/mxnet)︰效率和彈性的深入學習架構
  * [Weka](http://www.cs.waikato.ac.nz/ml/weka/)︰Java 中的視覺化資料採礦和機器學習服務軟體。
  * [Apache Drill](https://drill.apache.org/)：適用於 Hadoop、NoSQL 和雲端儲存體的無結構描述 SQL 查詢引擎。  支援 ODBC 和 JDBC 介面 tooenable 查詢 NoSQL 以及 PowerBI、 Excel、 Tableau 等標準的 BI 工具中的檔案。
* R 和 Python 語言的程式庫，可用於 Azure Machine Learning 和其他 Azure 服務
* 包括 Git Bash toowork 具有來源包括 GitHub，Visual Studio Team Services 的程式碼儲存機制的 Git
* Windows 連接埠，含可透過命令提示字元存取的數個熱門 Linux 命令列公用程式 (包括 awk、sed、perl、grep、find、wget 及 curl 等)。 

執行資料科學涉及反覆進行一連串的工作︰

1. 尋找、載入和前置處理資料
2. 建置和測試模型
3. 部署的智慧型應用程式中的耗用量的 hello 模型

資料科學家可以使用各種工具 toocomplete 這些工作。 它可以是相當耗時 toofind hello 適當 hello 軟體版本，然後下載並安裝它們。 hello Microsoft Data Science 虛擬機器也可以藉由在 Azure 上的已備妥要使用映像，可佈建提供預先安裝和設定所有數個的常用工具簡化此項負擔。 

hello Microsoft Data Science 虛擬機器以啟動分析專案。 它可讓您 toowork 上各種不同的語言包括 R、 Python、 SQL 和 C# 中的工作。 Visual Studio 提供 IDE toodevelop 並測試是方便 toouse 程式碼。 hello hello VM 中包含 Azure SDK 可讓您 toobuild Microsoft 的雲端平台上使用各種服務的應用程式。 

這個資料科學 VM 映像沒有任何軟體費用。 您只需支付 hello Azure 使用量費用的相依 hello hello 您佈建的虛擬機器大小。 詳細 hello 計算費用，請參閱 hello 定價詳細資料 區段上 hello [Data Science 虛擬機器](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/)頁面。 

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>其他版本的 hello Data Science 虛擬機器
A [CentOS](machine-learning-data-science-linux-dsvm-intro.md)影像也會提供、 與許多 hello 相同工具會以 hello Windows 映像。 亦提供 [Ubuntu](machine-learning-data-science-dsvm-ubuntu-intro.md) 映像，其中包含許多類似的工具及深入學習架構。

## <a name="prerequisites"></a>必要條件
您可以建立 Microsoft Data Science 虛擬機器之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**: tooobtain 一個，請參閱[取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* **Azure 儲存體帳戶**: toocreate 一個，請參閱[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。 或者，可以建立 hello 儲存體帳戶，如果不想讓 toouse 現有的帳戶建立 hello VM 的 hello 程序的一部分。

## <a name="create-your-microsoft-data-science-virtual-machine"></a>建立 Microsoft 資料科學虛擬機器
以下是 hello 步驟 toocreate hello Microsoft Data Science 虛擬機器的執行個體：

1. 瀏覽 toohello 虛擬機器上列出[Azure 入口網站](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm)。
2. 選取 hello**建立**hello 底部 toobe 納入精靈按鈕。![設定資料-科學-vm](./media/machine-learning-data-science-provision-vm/configure-data-science-virtual-machine.png)
3. Microsoft Data Science 虛擬機器需要 hello 精靈用 toocreate hello**輸入**每 hello**五個步驟**列舉此圖中的 hello。 以下是 hello 所需的輸入 tooconfigure 每個步驟：
   
   1. **基本概念**
      
      1. **名稱**：您建立的資料科學伺服器名稱。
      2. **使用者名稱**：系統管理員帳戶登入識別碼。
      3. **密碼**：系統管理員帳戶密碼。
      4. **訂用帳戶**： 如果您有多個訂閱，選取 hello 上哪些 hello 機器是 toobe 建立，並計費。
      5. **資源群組**：您可以建立新群組或使用現有的群組。
      6. **位置**: hello 選取最適合的資料中心。 通常它是 hello 資料中心有大部分的資料，或為最接近 tooyour 最快的網路存取的實體位置。
   2. **大小**： 選取其中一個符合您的功能需求和成本條件約束的 hello 伺服器類型。 您可以藉由選取 [檢視全部] 取得更多的 VM 大小的選項。
   3. **設定**：
      
      1. **磁碟類型**：如果您偏好固態硬碟 (SSD)，請選擇「高階」，否則請選擇「標準」。
      2. **儲存體帳戶**： 您可以在您的訂用帳戶中建立新的 Azure 儲存體帳戶，或使用現有 hello 相同*位置*hello 上，選擇**基本概念**hello 精靈的步驟。
      3. **其他參數**： 通常您只使用 hello 預設值。 如果您想 tooconsider hello 使用非預設值，您可以停留 hello hello 特定欄位的說明資訊的連結。
   4. **摘要**：請確認您輸入的所有資訊都正確無誤。
   5. **購買**： 按一下**購買**toostart hello 佈建。 Toohello 使用條款 hello 交易時，會提供的連結。 hello VM 並沒有任何額外的費用，超出您選擇在 hello hello 伺服器大小的 hello 計算**大小**步驟。 

> [!NOTE]
> hello 佈建時間約 10 20 分鐘。 hello 佈建的 hello 狀態會顯示在 hello Azure 入口網站。
> 
> 

## <a name="how-tooaccess-hello-microsoft-data-science-virtual-machine"></a>如何 tooaccess hello Microsoft Data Science 虛擬機器
一次 hello 建立 VM 時，您可以使用遠端桌面至使用您在前述的 hello 中設定的 hello 系統管理員帳戶認證**基本概念**> 一節。 

一旦建立並佈建 VM，您就準備好 toostart 使用 hello 工具所安裝及設定它。 有開始功能表方塊與桌面圖示的許多 hello 工具。 

## <a name="how-toocreate-a-strong-password-for-jupyter-and-start-hello-notebook-server"></a>如何 toocreate Jupyter 與開始的強式密碼 hello 筆記本伺服器
根據預設，hello Jupyter 筆記本伺服器已預先設定，但是 hello VM 上停用，直到您設定 Jupyter 密碼。 toocreate hello Jupyter 筆記本伺服器 hello 電腦上安裝的強式密碼，執行下列命令，從命令提示字元上 hello 資料科學虛擬機器或按兩下 hello 桌面捷徑我們所提供的 hello 呼叫**Jupyter 設定密碼 （& s) 開始**從本機 VM 系統管理員帳戶。

    C:\dsvm\tools\setup\JupyterSetPasswordAndStart.cmd

請遵循 hello 訊息，然後選擇強式密碼，當系統提示您。

hello 上述指令碼建立的密碼雜湊和存放區在 hello Jupyter 組態檔位於： **C:\ProgramData\jupyter\jupyter_notebook_config.py** hello 參數名稱 底下***c。NotebookApp.password***。

hello 指令碼也會啟用，並在 hello 背景中執行 hello Jupyter 伺服器。 Jupyter 伺服器建立稱為 windows hello WIndows 工作排程器工作**Start_IPython_Notebook**。  您可能有 toowait 對於幾秒鐘後再開啟您的瀏覽器中的 hello 筆記本設定 hello 密碼。 請參閱 hello 下面的一節**Jupyter 筆記本**上 tooaccess hello Jupyter 筆記本伺服器的方式。 


## <a name="tools-installed-on-hello-microsoft-data-science-virtual-machine"></a>Hello Microsoft Data Science 虛擬機器上安裝工具

### <a name="microsoft-r-server-developer-edition"></a>Microsoft R Server Developer Edition
如果您是供您分析想 toouse R，hello VM 已安裝 Microsoft R Server Developer edition。 Microsoft R Server 是一個能夠廣泛部署的企業級分析平台，以支援的 R 為基礎，可調整規模且十分安全。 R Server 可支援各種不同的巨量資料的統計資料、 預測模型和機器學習功能，支援分析 – 瀏覽、 分析、 視覺化和模型化 hello 完整範圍。 藉由使用並擴充開放原始碼 R、 Microsoft R Server 是與 R 指令碼、 函數和 CRAN 封裝，tooanalyze 企業規模的資料完全相容。 它也會解決開放來源 R hello 記憶體限制加入平行和區塊處理的資料。 這可讓您針對遠大於什麼適合放入主記憶體中的資料進行 toorun 分析。  Visual Studio Community Edition 包含在 hello VM 包含 hello 適用於 Visual Studio 擴充功能，提供完整的 IDE 使用 r 的 R 工具您也可以下載並使用其他 Ide，以及例如[RStudio](http://www.rstudio.com)。 

### <a name="python"></a>Python
為了能夠使用 Python 進行開發，我們已安裝了 Anaconda Python 散佈 2.7 與 3.5。 此分佈包含 hello 基底 Python 以及大約 300 個 hello 最受歡迎的數學、 工程團隊和資料分析封裝。 您可以使用 Python Tools for Visual Studio (PTVS) 內 hello Visual Studio 2015 Community 版本或其中一個 hello Ide 隨同 Anaconda 閒置或 Spyder 等安裝。 您可以啟動下列其中一種藉由搜尋 hello 搜尋列上 (**Win** + **S**索引鍵)。

> [!NOTE]
> toopoint hello Python Tools for Visual Studio 在 Anaconda Python 2.7 和 3.5，您會需要針對每個版本 toocreate 自訂環境。 tooset hello Visual Studio 2015 Community 版本，在這些環境路徑太巡覽**工具** -> **Python Tools** -> **Python 環境** ，然後按一下 **+ 自訂**。 
> 
> 

Anaconda Python 2.7 安裝在 C:\Anaconda 之下，Anaconda Python 3.5 則安裝在 c:\Anaconda\envs\py35 之下。 如需詳細步驟，請參閱 [PTVS 文件](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) 。 

### <a name="jupyter-notebook"></a>Jupyter Notebook
Jupyter 筆記本、 與環境 tooshare 程式碼分析也提供 anaconda 發佈。 Jupyter Notebook 伺服器已經預先設定 Python 2.7、Python 3.4、Python 3.5 及 R 核心。 桌面圖示，名為"Jupyter 筆記本 toolaunch hello 瀏覽器 tooaccess hello 筆記本伺服器。 如果您是透過遠端桌面的 hello VM 上，您也可以造訪[https://localhost:9999 /](https://localhost:9999/) tooaccess hello Jupyter 筆記本伺服器登入時 toohello VM。

> [!NOTE]
> 如果您收到任何憑證警告，請繼續。 
> 
> 

我們有封裝數個範例筆記本中 Python 和 hello Jupyter 筆記本顯示如何使用 Microsoft R Server、 SQL Server 2016 R 服務 （資料庫內分析）、 Python、 Microsoft 認知 ToolKit (CNTK)，深入學習和其他 Azure toowork一旦您登入 tooJupyter 技術。 Toohello Jupyter 筆記本使用您在前述步驟中建立的 hello 密碼進行驗證後，您可以在 hello 筆記本首頁上看到 hello 連結 toohello 範例。 

### <a name="visual-studio-2015-community-edition"></a>Visual Studio 2015 Community 版本
Hello VM 上安裝的 visual Studio Community 版本。 它是免費版的 hello 供評估之用，對於小型小組，您可以使用的 microsoft 受歡迎的 IDE。 您可以簽出授權條款的 hello[這裡](https://www.visualstudio.com/support/legal/mt171547)。  開啟 Visual Studio，連按兩下 hello 桌面圖示或 hello**啟動**功能表。 您也可以使用 **Win** + **S** 並輸入 “Visual Studio” 來搜尋程式。 之後，您就可以使用像是 C#、Python、R 及 node.js 等語言來建立專案。 外掛程式會一併安裝，可讓您方便 toowork 與 Azure 資料目錄、 Azure HDInsight Hadoop (Spark） 和 Azure 資料湖等 Azure 服務。 

> [!NOTE]
> 您可能會收到訊息，表示您的評估期間已過期。 輸入您的 Microsoft 帳戶認證，或建立新的免費帳戶 tooget 存取 toohello Visual Studio Community 版本。 
> 
> 

### <a name="sql-server-2016-developer-edition"></a>SQL Server 2016 Developer Edition
開發人員的 SQL Server 2016 與 R Services toorun 資料庫中的分析會提供的版本上 hello VM。 R 服務提供用於開發和部署智慧型應用程式的平台。 您可以使用 hello 功能強大且豐富的 R 語言和 hello hello 社群 toocreate 模型的許多封裝的 SQL Server 資料產生預測。 您可以保持關閉 toohello 的分析資料，因為 R 服務 （資料庫） 整合 hello R 語言與 SQL Server。 這可減少 hello 成本和移動資料相關聯的安全性風險。

> [!NOTE]
> hello SQL Server 2016 developer edition 僅用於開發和測試用途。 需要授權 toorun 它在生產環境中。 
> 
> 

您可以存取 hello SQL server 啟動**SQL Server Management Studio**。 VM 名稱會擴展為 hello 伺服器名稱。 使用 Windows 驗證時 hello Windows 上的系統管理員身分登入。 當您在 SQL Server Management Studio 中，可以建立其他使用者、建立資料庫、匯入資料以及執行 SQL 查詢。 

使用 Microsoft R，執行下列其中一個命令的 hello tooenable 資料庫在分析 SQL Server management studio 中的動作 hello 伺服器系統管理員身分登入之後的時間。 

        CREATE LOGIN [%COMPUTERNAME%\SQLRUserGroup] FROM WINDOWS 

        (Please replace hello %COMPUTERNAME% with your VM name)


### <a name="azure"></a>Azure
Hello VM 上，會安裝數個 Azure 工具：

* 沒有桌面捷徑 tooaccess hello Azure SDK 文件。 
* **AzCopy**： 使用 toomove 資料進出您的 Microsoft Azure 儲存體帳戶。 toosee 使用量，型別**Azcopy**在命令提示字元 toosee hello 使用量。 
* **Microsoft Azure 儲存體總管**： 使用 toobrowse 透過您已儲存您的 Azure 儲存體帳戶並傳輸資料 tooand 從 Azure 儲存體中的 hello 物件。 您可以輸入**存放裝置總管**搜尋或尋找在其上 hello Windows [開始] 功能表 tooaccess 這項工具。 
* **Adlcopy**： 使用 toomove 資料 tooAzure Data Lake。 toosee 使用量，型別**adlcopy**命令提示字元中。 
* **dtui**： 使用 toomove 資料 tooand 從 Azure Cosmos DB hello 雲端上的 NoSQL 資料庫。 在命令提示字元中輸入 **dtui** 。 
* **Microsoft 資料管理閘道**︰可在內部部署資料來源和雲端之間移動資料。 其使用於 Azure Data Factory 之類的工具。 
* **Microsoft Azure Powershell**： 使用的工具 tooadminister 您的 Azure 資源 hello Powershell 指令碼語言，也會安裝在您的 VM。 

### <a name="power-bi"></a>Power BI
toohelp 您儀表板和建置絕佳的視覺效果，hello **Power BI Desktop**已安裝。 使用此工具 toopull 資料來自不同來源 tooauthor 儀表板和報表和 toopublish 它們 toohello 雲端。 如需資訊，請參閱 hello [Power BI](http://powerbi.microsoft.com)站台。 您可以在 hello [開始] 功能表上找到 Power BI desktop。 

> [!NOTE]
> 您需要 Office 365 帳戶 tooaccess Power BI。 
> 
> 

## <a name="additional-microsoft-development-tools"></a>其他 Microsoft 開發工具
hello [ **Microsoft Web Platform Installer** ](https://www.microsoft.com/web/downloads/platform.aspx)可以使用的 toodiscover 並下載其他的 Microsoft 開發工具。 此外，也提供在 hello Microsoft Data Science 虛擬機器桌面上的捷徑 toohello 工具。  

## <a name="important-directories-on-hello-vm"></a>在 hello VM 上的重要目錄
| Item | 目錄 |
| --- | --- |
| Jupyter Notebook 伺服器組態 |C:\ProgramData\jupyter |
| Jupyter Notebook 範例的主目錄 |c:\dsvm\notebooks |
| 其他範例 |c:\dsvm\samples |
| Anaconda (預設值︰Python 2.7) |c:\Anaconda |
| Anaconda Python 3.5 環境 |c:\Anaconda\envs\py35 |
| R 伺服器 (獨立式) 執行個體目錄 (以 R3.2.2 為基礎的預設 R 執行個體) |C:\Program Files\Microsoft SQL Server\130\R_SERVER |
| R 伺服器 (資料庫內) 執行個體目錄 (R3.2.2) |C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES |
| Microsoft R Open (R3.3.1) 執行個體目錄 |C:\Program Files\Microsoft\MRO-3.3.1 |
| 其他工具 |c:\dsvm\tools |

> [!NOTE]
> Hello 1.5.0 （早於 2016 年 9 月 3 日) 之前建立的 Microsoft Data Science 虛擬機器的執行個體的使用稍有不同的目錄結構與 hello 前面表格中所指定。 
> 
> 

## <a name="next-steps"></a>後續步驟
以下是一些下一個步驟 toocontinue，您學習和瀏覽。 

* 瀏覽的 hello 按一下 hello hello 資料科學 VM 上的各種資料科學工具開始功能表和簽出 hello 列在 [hello] 功能表上的工具。
* 瀏覽過**C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\RevoScaleR\demoScripts**範例使用 R，支援資料分析企業規模的 hello RevoScaleR 文件庫。  
* 閱讀文章 hello: [10 個項目，您可以在 hello 資料科學虛擬機器執行](http://aka.ms/dsvmtenthings)
* 了解如何 toobuild 結束 tooend 分析解決方案有系統地使用 hello[資料科學的小組流程](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)。
* 請瀏覽 hello [Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)的機器學習服務與資料分析範例，使用 hello Cortana 智慧套件。 我們也已經提供圖示上 hello**啟動**功能表和桌面上 hello hello 虛擬機器 toothis 庫。

