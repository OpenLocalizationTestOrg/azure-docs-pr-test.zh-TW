---
title: "aaaTen 項目，您可以在 hello Data Science 虛擬機器 |Microsoft 文件"
description: "Hello 資料科學虛擬機器上執行各種資料瀏覽和模型化工作。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 145dfe3e-2bd2-478f-9b6e-99d97d789c62
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;weig;bradsev
ms.openlocfilehash: 4dfe22f14f00208c63e26ce44b05123c9ac4b850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a>您可以執行 hello 資料科學虛擬機器上的十個項目
hello Microsoft 資料科學虛擬機器 (DSVM) 是功能強大的資料科學開發環境，可讓您 tooperform 各種資料探索和模型工作。 hello 環境包含已建置及配套幾個常見的資料與分析工具，可讓您輕鬆 tooget 快速地開始使用您的分析，在內部部署、 雲端或混合式部署。 hello DSVM 與許多 Azure 服務密切合作，且無法 tooread 和處理已儲存在 Azure、 在 Azure SQL 資料倉儲、 Azure 資料湖、 Azure 儲存體，或在 Azure Cosmos DB 的資料。 它也可以利用 Azure Machine Learning 和 Azure Data Factory 等其他分析工具。

本文章中我們逐步引導您 toouse 您 DSVM tooperform 各種資料科學工作以及與其他 Azure 服務互動。 以下是一些您可以在 hello DSVM 所執行的 hello 事項：

1. 瀏覽資料並開發模型，在本機上使用 Microsoft R Server Python DSVM hello
2. 使用 Python 2，Python 3 Microsoft R R 的延展性和效能而設計的企業就緒版本的瀏覽器上的資料搭配使用 Jupyter 筆記本 tooexperiment
3. 在 Azure Machine Learning 上實作使用 R 和 Python 建置的模型，以便用戶端應用程式使用簡單的 Web 服務介面存取您的模型
4. 使用 Azure 入口網站或 Powershell 管理您的 Azure 資源
5. 建立 Azure 檔案儲存體作為 DSVM 上可掛接的磁碟機，以擴充您的儲存空間並與整個小組共用大型資料集/程式碼
6. 與您使用 GitHub 的小組共用程式碼，並存取您的儲存機制使用 hello 預先安裝的 Git 用戶端-Git Bash Git GUI。
7. 存取各種 Azure 資料和分析服務，例如 Azure Blob 儲存體，Azure Data Lake、Azure HDInsight (Hadoop)、Azure Cosmos DB、Azure SQL 資料倉儲和資料庫
8. 建立報表和儀表板使用 hello hello DSVM 上預先安裝的 Power BI Desktop，並將其部署的 hello 雲端
9. 動態調整您的專案需要您 DSVM toomeet
10. 在虛擬機器上安裝其他工具   

> [!NOTE]
> 其他使用費用 適用於許多 hello 其他資料儲存體和分析服務本文所列。 請參閱 toohello [Azure 定價](https://azure.microsoft.com/pricing/)頁面以取得詳細資料。
> 
> 

**必要條件**

* 您需要 Azure 訂用帳戶。 您可以在[這裡](https://azure.microsoft.com/free/)註冊免費試用。
* 指示佈建 hello Azure 入口網站上的 Data Science 虛擬機器位於[建立虛擬機器](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm)。

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a>1.使用 Microsoft R Server 或 Python 探索資料和開發模型
您可以在 hello DSVM 使用語言，例如 R，並將 Python toodo 資料分析。

，您可以使用稱為 「 Revolution R Enterprise 8.0"hello 桌面 hello [開始] 功能表上找到的 IDE。 Microsoft 已提供額外的程式庫最上層 hello 開啟來源/CRAN R tooenable 可擴充分析和 hello 能力 tooanalyze 資料大於允許的執行平行區塊的分析 hello 記憶體大小。 您也可以安裝您選擇的 R IDE，例如 [RStudio](https://www.rstudio.com/products/rstudio-desktop/)。

Python，您可以使用像是 Visual Studio Community 版本具有 hello Python Tools for Visual Studio (PTVS) 預先安裝的擴充功能的 IDE。 根據預設，PTVS 上只設定基本的 Python 2.7 (不含任何分析程式庫，如 SciKit、Pandas)。 在訂單 tooenable Anaconda Python 2.7 和 3.5 中，您需要 toodo hello 下列：

* 建立瀏覽過的每個版本的自訂環境**工具** -> **Python Tools** -> **Python 環境**，然後按一下"**+ 自訂**「 在 Visual Studio 2015 Community 版本 hello
* 提供的描述，並設定 hello 環境做為前置詞路徑*c:\anaconda* Anaconda Python 2.7 或*c:\anaconda\envs\py35* Anaconda Python 3.5
* 按一下**自動偵測**然後**套用**toosave hello 環境。

以下是 Visual Studio 中看起來像哪些 hello 自訂環境設定。

![PTVS 設定](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

請參閱 hello [PTVS 文件](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it)的其他詳細資料 toocreate Python 環境。

現在您會設定 toocreate 新的 Python 專案。 瀏覽過**檔案** -> **新增** -> **專案** -> **Python**選取 hello 類型您要建置的 Python 應用程式。 您可以設定 hello Python 環境的 hello 目前專案 toohello 所需的版本 (Anaconda 2.7 或 3.5 為目標): 以滑鼠右鍵按一下 hello **Python 環境**，選取**新增/移除 Python 環境**，和然後選取所需的 hello 環境 tooassociate 與 hello 專案。 您可以找到更多有關如何使用與 PTVS hello 產品[文件](https://github.com/Microsoft/PTVS/wiki)頁面。

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a>2.Jupyter 筆記本 tooexplore 和模型資料搭配使用 Python 或 R
hello Jupyter 筆記本是功能強大的環境，提供資料探索和模型的瀏覽器型"IDE"。 Jupyter 筆記本中，您可以使用 Python 2、 Python 3 或 R （開放原始碼和 Microsoft R Server hello）。

hello 開始功能表圖示上按一下 toolaunch hello Jupyter 筆記本 / 標題為 桌面圖示**Jupyter 筆記本**。 在 hello DSVM 您也可以瀏覽過"https://localhost:9999 /"tooaccess hello 木星筆記型電腦。 如果它會提示您輸入密碼，請使用 hello 中提供的指示***如何 toocreate hello Jupyter 筆記本伺服器上的強式密碼***區段 hello[佈建 hello Microsoft Data Science 虛擬機器](machine-learning-data-science-provision-vm.md)主題 toocreate 強式密碼 tooaccess hello Jupyter 筆記本。 

一旦您已開啟 hello 筆記本，您應該會看到包含幾個範例筆記本 hello DSVM 到預先封裝的目錄。 現在您可以：

* 按一下 hello 筆記本 toosee hello 程式碼。
* 按 **SHIFT-ENTER**執行每個儲存格。
* 按一下以執行 hello 整個筆記本**儲存格** -> **執行**
* hello Jupyter 圖示 （左上角） 上按一下，然後按一下以建立新的記事本**新增**hello 右，然後選擇 hello 筆記本語言 （也稱為核心） 上的按鈕。   

> [!NOTE]
> 目前我們支援 Python 2.7、 Python 3.5 和 r hello R 核心開放原始碼 R 以及 hello 企業中支援的程式設計可擴充的 Microsoft R Server。   
> 
> 

當您在 hello 筆記本可以瀏覽資料、 建立 hello 模型、 測試 hello 模型使用您所選擇的程式庫。

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a>3.使用 R 或 Python 建置模型並且使用 Azure Machine Learning 實作
一旦您已經建置和驗證模型 hello 的下一個步驟通常是 toodeploy 它到實際執行環境。 這可讓您的用戶端應用程式 tooinvoke hello 模型預測即時或批次模式為基礎。 Azure Machine Learning 提供機制 toooperationalize Python 或 R 中所建立的模型。

當您作業化您在 Azure Machine Learning 中的模型時，web 服務會公開以允許用戶端的傳入輸入參數，且收到 hello 模型中的預測，為輸出 toomake REST 呼叫。   

> [!NOTE]
> 如果您不尚未已註冊 Azure Machine Learning，您可以取得免費工作區或標準的工作區瀏覽 hello [Azure Machine Learning Studio](https://studio.azureml.net/)首頁上，按一下 在 「 取得已啟動 」。   
> 
> 

### <a name="build-and-operationalize-python-models"></a>建置和實作 Python 模型
以下是在 Python Jupyter 筆記本中建立簡單的模型使用 hello SciKit 學習程式庫開發程式碼的程式碼片段。

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

hello 方法使用 toodeploy 您 python 模型 tooAzure Machine Learning 會包裝 hello 的預測 hello 模型到函式和裝飾與 hello 預先安裝 Azure Machine Learning python 程式庫所提供的屬性，代表您的 Azure 機器Learning 工作區識別碼、 API 金鑰，以及 hello 輸入和傳回參數。  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

用戶端現在可以讓呼叫 toohello web 服務。 沒有建構 hello REST API 要求的便利包裝函式。 以下是範例程式碼 tooconsume hello web 服務。

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> hello Azure Machine Learning 文件庫只支援 Python 2.7 目前。   
> 
> 

### <a name="build-and-operationalize-r-models"></a>建置和實作 R 模型
您可以部署以類似 toohow 基於 Python 的方式內建 hello Data Science 虛擬機器或其他 Azure 機器學習到的 R 模型。 她 hello 步驟：

* 建立工作區識別碼和驗證語彙基元 hello 下列程式碼範例所示 settings.json 檔案 tooprovide。
* 寫入包裝函式以進行 hello 模型的預測函數。
* 呼叫```publishWebService```在 hello Azure Machine Learning 文件庫 toopass hello 函式包裝函式中。  

以下是 hello 程序和程式碼的程式碼片段可以是使用的 tooset up、 建置、 發行和取用 Azure Machine Learning 中的 web 服務的模型。

#### <a name="setup"></a>設定
1. 輸入安裝 hello 機器學習 R 封裝```install.packages("AzureML")```Revolution R Enterprise 8.0 IDE 或您的 R IDE 中。
2. 從[這裡](https://cran.r-project.org/bin/windows/Rtools/)下載 RTools。 您需要 hello zip 公用程式在 hello 路徑 （和具名的 zip.exe） toooperationalize R 封裝到機器學習。
3. 建立 settings.json 底下的檔名的目錄```.azureml```主目錄底下，輸入 hello 參數與您的 Azure Machine Learning 工作區：

settings.json 檔案結構：

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a>以 R 建置模型並在 Azure Machine Learning 中發佈
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function toopublish based on hello model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a>使用 Azure Machine Learning 中部署的 hello 模型
tooconsume hello 模型從用戶端應用程式中的，我們使用向上 hello hello Azure Machine Learning 文件庫 toolook 發佈 web 服務的名稱使用 hello `services` API 呼叫 toodetermine hello 端點。 然後您只需要呼叫 hello`consume`函式，並傳入 hello 資料框架 toobe 預測。
下列程式碼的 hello 是使用的 tooconsume hello 模型發佈為 Azure Machine Learning web 服務。

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

可以找到 hello Azure 機器學習 R 程式庫的詳細資訊[這裡](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf)。

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a>4.使用 Azure 入口網站或 Powershell 管理您的 Azure 資源
hello DSVM 不僅可讓您 toobuild 分析解決方案上進行本機 hello 虛擬機器，但也允許 tooaccess Microsoft Azure 雲端服務。 Azure 提供數個可從 DSVM 管理和存取的計算、儲存、資料分析服務和其他服務。

tooadminister 您的 Azure 訂用帳戶和雲端資源可以使用瀏覽器和點 toothe [Azure 入口網站](https://portal.azure.com)。 您的 Azure 訂用帳戶和資源，透過指令碼，您也可以使用 Azure Powershell tooadminister。
您可以從捷徑 hello 桌面上執行 Azure Powershell 或 hello 從開始功能表標題為 「 Microsoft Azure Powershell 」。 如需如何使用 Windows Powershell 指令碼管理 Azure 訂用帳戶和資源的詳細資訊，請參閱 [Microsoft Azure Powershell 文件](../powershell-azure-resource-manager.md) 。

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a>5.使用共用的檔案系統來擴充您的儲存空間
資料科學家可以共用大型資料集、 程式碼或 hello 小組內的其他資源。 hello DSVM 本身有大約 70 GB 的可用空間。 tooextend 您的儲存體，您可以使用 hello Azure 檔案服務，然後將其裝載在 hello DSVM 或存取透過 REST API。   

> [!NOTE]
> hello hello Azure 檔案服務共用的空間上限是 5 TB，個別的檔案大小上限為 1 TB。   
> 
> 

您可以使用 Azure Powershell toocreate Azure 檔案服務共用。 以下是在 Azure PowerShell toocreate Azure 檔案服務共用的 hello 指令碼 toorun。

    # Authenticate tooAzure.
    Login-AzureRmAccount
    # Select your subscription
    Get-AzureRmSubscription –SubscriptionName "<your subscription name>" | Select-AzureRmSubscription
    # Create a new resource group.
    New-AzureRmResourceGroup -Name <dsvmdatarg>
    # Create a new storage account. You can reuse existing storage account if you wish.
    New-AzureRmStorageAccount -Name <mydatadisk> -ResourceGroupName <dsvmdatarg> -Location "<Azure Data Center Name For eg. South Central US>" -Type "Standard_LRS"
    # Set your current working storage account
    Set-AzureRmCurrentStorageAccount –ResourceGroupName "<dsvmdatarg>" –StorageAccountName <mydatadisk>

    # Create a Azure File Service Share
    $s = New-AzureStorageShare <<teamsharename>>
    # Create a directory under hello FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List hello share tooconfirm that everything worked
    Get-AzureStorageFile -Share $s


您現在已建立 Azure 檔案共用，即可將它掛接在 Azure 的任何虛擬機器中。 強烈建議該 hello VM 處於相同的 Azure 資料中心為 hello 儲存體帳戶 tooavoid 延遲和資料傳輸費用。 以下是您可以在 Azure Powershell 執行的 DSVM hello hello 命令 toomount hello 磁碟機。

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


現在您可以在 hello VM 上的任何標準磁碟機一樣，存取此磁碟機。

## <a name="6-share-code-with-your-team-using-github"></a>6.使用 GitHub 與您的小組共用程式碼
GitHub 是可以在哪裡找到大量的範例程式碼和來源使用共用的 hello 開發人員社群的各種技術的不同工具的程式碼儲存機制。 它會使用 Git hello hello 的程式碼檔案的技術 tootrack 和存放區版本。 GitHub 也是平台可讓您建立您自己的儲存機制 toostore 您的小組共用的程式碼和文件，實作版本控制以及控制擁有存取 tooview 和程式碼撰寫。 請瀏覽 hello [GitHub 說明網頁](https://help.github.com/)如需有關使用 Git。 您可以使用 GitHub 做為其中一個 hello 方式 toocollaborate，與您的小組、 使用 hello 社群所開發的程式碼，並提供程式碼後 toohello 社群。

hello DSVM 已上線時載入用戶端工具與命令列中以及 GUI tooaccess GitHub 儲存機制以兩者。 使用 Git 及 GitHub hello 命令列工具 toowork 稱為 Git Bash。 Hello DSVM 上安裝 visual Studio 有 hello Git 擴充功能。 您可以找到這些工具 hello 開始功能表和 hello 桌面啟動圖示。

toodownload 程式碼從 GitHub 儲存機制中，您使用 hello```git clone```命令。 例如 toodownload 資料科學儲存機制 Microsoft 所發行到 hello 目前目錄中您可以執行下列命令，當您在 hello ```git-bash```。

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

在 Visual Studio 中，您可以執行 hello 相同的複製作業。 下列螢幕擷取畫面的 hello 顯示 tooaccess Git 及 GitHub 工具在 Visual Studio 中的方式。

![Visual Studio 中的 Git](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

您可以尋找在 Git toowork 使用您的 GitHub 儲存機制從 github.com 上可用的數個資源的詳細資訊。hello[小祕技](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf)是有用的參考。

## <a name="7-access-various-azure-data-and-analytics-services"></a>7.存取各種 Azure 資料和分析服務
### <a name="azure-blob"></a>Azure Blob
Azure blob 是可靠、划算的雲端儲存體，可存放大型和小型的資料。 讓我們看看如何移動資料 tooAzure Blob 和 Azure Blob 中所儲存的存取資料。

**必要條件**

* **從 [Azure 入口網站](https://portal.azure.com)建立 Azure Blob 儲存體帳戶。**

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* 確認該 hello 預先安裝命令列 AzCopy 工具位於```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```。 執行此工具時，您可以加入 hello 目錄包含 hello azcopy.exe tooyour 環境變數 tooavoid 輸入 hello 完整命令的路徑。 如需 AzCopy 工具的詳細資訊，請參閱太[AzCopy 文件](../storage/common/storage-use-azcopy.md)
* 啟動 hello Azure 儲存體總管工具。 您可以從 [Microsoft Azure 儲存體總管](http://storageexplorer.com/)下載此工具。 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

**將資料從 VM tooAzure Blob 移： AzCopy**

將本機檔案和 blob 儲存體之間 toomove 資料，您可以在命令列使用 AzCopy 或 PowerShell:

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

取代**C:\myfolder** toohello 儲存您的檔案位置的路徑**mystorageaccount** tooyour blob 儲存體帳戶名稱， **mycontainer** toohello 容器名稱， **儲存體帳戶金鑰**tooyour blob 儲存體存取金鑰。 您可以在 [Azure 入口網站](https://portal.azure.com)中尋找您的儲存體帳戶認證。

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

在 PowerShell 或從命令提示字元執行 AzCopy 命令。 以下是使用 AzCopy 命令的一些範例：

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



一旦您執行您的 AzCopy 命令 toocopy tooan Azure blob，您會看到您的檔案會出現在 Azure 儲存體總管很快。

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

**將資料從 VM tooAzure Blob 移： Azure 儲存體總管**

您也可以使用 Azure 儲存體總管在 VM 中上載 hello 本機檔案的資料：

* tooupload 資料 tooa 容器、 選取 hello 目標容器，按一下 hello**上傳** 按鈕。![儲存體總管中上傳](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)
* 按一下 hello **...**方 hello toohello**檔案**方塊選取一個或多個檔案 tooupload hello 檔案系統中，按一下**上傳**toobegin hello 檔案上載。![上傳檔案 tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)

**從 Azure Blob 讀取資料：Machine Learning 讀取器模組**

您可以使用 Azure Machine Learning Studio**資料匯入模組**tooread 資料從您的 blob。

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

**從 Azure Blob 讀取資料：Python ODBC**

您可以使用**BlobService**媒體櫃 tooread 資料直接從 Jupyter 筆記本或 Python 程式中的 blob。

首先，匯入所需的封裝：

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random

然後插入您的 Azure Blob 帳戶認證並從 Blob 讀取資料：

    CONTAINERNAME = 'xxx'
    STORAGEACCOUNTNAME = 'xxxx'
    STORAGEACCOUNTKEY = 'xxxxxxxxxxxxxxxx'
    BLOBNAME = 'nyctaxidataset/nyctaxitrip/trip_data_1.csv'
    localfilename = 'trip_data_1.csv'
    LOCALDIRECTORY = os.getcwd()
    LOCALFILE =  os.path.join(LOCALDIRECTORY, localfilename)

    #download from blob
    t1 = time.time()
    blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
    blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILE)
    t2 = time.time()
    print(("It takes %s seconds toodownload "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'hello size of hello data is: %d rows and  %d columns' % df1.shape

hello 資料被視為資料框架中：

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a>Azure 資料湖
Azure Data Lake 儲存體是巨量資料分析工作負載的超大規模儲存機制，與 Hadoop 分散式檔案系統 (HDFS) 相容。 它可搭配 hello Hadoop 生態系統和 hello Azure Data Lake Analytics。 我們會示範如何將資料移入 hello Azure 資料湖存放區，並執行使用 Azure Data Lake Analytics 分析。

**必要條件**

* 在 [Azure 入口網站](https://portal.azure.com)中建立 Azure Data Lake Analytics。

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* hello **Azure Data Lake Tools**中**Visual Studio**位於這[連結](https://www.microsoft.com/download/details.aspx?id=49504)hello hello 虛擬機器上的 Visual Studio Community Edition 上已安裝。 之後啟動 Visual Studio，並記錄您 Azure 訂用帳戶中，您應該會看到您的 Azure 資料分析帳戶和 hello 的 Visual Studio 的左面板中的儲存體。

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

**將資料從 VM tooData Lake 移： Azure Data Lake 總管**

您可以使用**Azure Data Lake 總管**tooupload 資料從虛擬機器 tooData Lake 的存放裝置中的 hello 本機檔案。

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

您也可以建立資料管線 tooproductionize 您從 Azure Data Lake 的資料移動 tooor 使用 hello [Azure 資料 Factory(ADF)](https://azure.microsoft.com/services/data-factory/)。 我們參照 toothis[文章](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/)tooguide 您透過 hello 步驟 toobuild hello 資料管線。

**從 Azure Blob tooData 湖讀取資料： U-SQL**

如果您的資料位於 Azure Blob 儲存體中，您可以在 U-SQL 查詢中從 Azure 儲存體 Blob 直接讀取資料。 之前撰寫 U SQL 查詢，請確定您的 blob 儲存體帳戶是連結的 tooyour Azure 資料湖。 跳過**Azure 入口網站**，尋找您的 Azure Data Lake Analytics 儀表板，按一下**加入資料來源**，選取儲存體類型太**Azure 儲存體**並插入您的 Azure 儲存體帳戶名稱和金鑰。 您已無法 tooreference hello 資料儲存在 hello 儲存體帳戶。

![輸入儲存體帳戶和金鑰](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

在 Visual Studio 中，您可以從 blob 儲存體讀取資料、 執行一些資料操作、 特徵設計和輸出 hello 產生資料 tooeither Azure 資料湖或 Azure Blob 儲存體。 當您參考 blob 儲存體中的 hello 資料時，使用**wasb: / /**; 當您參考 Azure Data Lake，使用中的 hello 資料**swbhdfs: / /**

![資料框架](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

您可以使用下列 U SQL 查詢，在 Visual Studio 中的 hello:

    @a =
        EXTRACT medallion string,
                hack_license string,
                vendor_id string,
                rate_code string,
                store_and_fwd_flag string,
                pickup_datetime string,
                dropoff_datetime string,
                passenger_count int,
                trip_time_in_secs double,
                trip_distance double,
                pickup_longitude string,
                pickup_latitude string,
                dropoff_longitude string,
                dropoff_latitude string

        FROM "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Input Data File Name>"
        USING Extractors.Csv();

    @b =
        SELECT vendor_id,
        COUNT(medallion) AS cnt_medallion,
        SUM(passenger_count) AS cnt_passenger,
        AVG(trip_distance) AS avg_trip_dist,
        MIN(trip_distance) AS min_trip_dist,
        MAX(trip_distance) AS max_trip_dist,
        AVG(trip_time_in_secs) AS avg_trip_time
        FROM @a
        GROUP BY vendor_id;

    OUTPUT @b   
    too"swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    too"wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



您的查詢會提交的 toohello 伺服器之後，會顯示圖表，顯示您工作的 hello 狀態。

![作業狀態圖表](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

**查詢資料湖中的資料：U-SQL**

Hello 資料集是內嵌至 Azure 資料湖之後，您可以使用[U-SQL 語言](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md)tooquery 和瀏覽 hello 資料。 U SQL 語言是類似的 tooT SQL，但結合從 C# 的某些功能，讓使用者都可以寫入自訂的模組、 使用者定義函式和等等。Hello 上一個步驟中，您可以使用 hello 指令碼。

已提交的 tooserver，tripdata_summary hello 查詢之後。CSV 可以在稍後**Azure Data Lake 總管**，您可以預覽 hello 資料，以滑鼠右鍵按一下 hello 檔案。

![Azure Data Lake Explorer 中的檔案](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

toosee hello 檔案資訊：

![檔案摘要](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a>HDInsight Hadoop 叢集
Azure HDInsight 是 hello 雲端上的 Apache Hadoop、 Spark、 HBase 和 Storm 受管理的服務。 您可以輕鬆地處理從 hello data science 虛擬機器的 Azure HDInsight 叢集。

**必要條件**

* 從 [Azure 入口網站](https://portal.azure.com)建立 Azure Blob 儲存體帳戶。 這個儲存體帳戶是使用的 toostore 資料 HDInsight 叢集。

![建立 Azure Blob 儲存體帳戶](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* 從 [Azure 入口網站](machine-learning-data-science-customize-hadoop-cluster.md)
  
  * 您必須連結 hello 時就會建立使用您的 HDInsight 叢集建立的儲存體帳戶。 這個儲存體帳戶用來存取可處理 hello 叢集內的資料。

![建立與 HDInsight 叢集連結 toostorage 帳戶](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* 您必須啟用**遠端存取**toohello 建立後的 hello 叢集前端節點。 請記住您在此處指定 （不同於所指定的 hello 在其建立的叢集） hello 遠端存取認證： hello 後續程序中需要它們。

![啟用遠端存取](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* 建立 Azure Machine Learning 工作區。 您的機器學習實驗將會儲存在此 Machine Learning 工作區中。 選取 hello 反白顯示在入口網站中的選項，hello 下列螢幕擷取畫面所示：

![建立 Azure Machine Learning 工作區](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* 然後輸入 hello 參數，您的工作區

![輸入 Machine Learning 工作區參數](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* 使用 IPython Notebook 上傳資料。 第一個所需的匯入封裝，插入的認證，請在儲存體帳戶中建立資料庫，然後載入資料 tooHDI 叢集。

        #Import required Packages
        import pyodbc
        import time as time
        import json
        import os
        import urllib
        import urllib2
        import warnings
        import re
        import pandas as pd
        import matplotlib.pyplot as plt
        from azure.storage.blob import BlobService
        warnings.filterwarnings("ignore", category=UserWarning, module='urllib2')


        #Create hello connection tooHive using ODBC
        SERVER_NAME='xxx.azurehdinsight.net'
        DATABASE_NAME='nyctaxidb'
        USERID='xxx'
        PASSWORD='xxxx'
        DB_DRIVER='Microsoft Hive ODBC Driver'
        driver = 'DRIVER={' + DB_DRIVER + '}'
        server = 'Host=' + SERVER_NAME + ';Port=443'
        database = 'Schema=' + DATABASE_NAME
        hiveserv = 'HiveServerType=2'
        auth = 'AuthMech=6'
        uid = 'UID=' + USERID
        pwd = 'PWD=' + PASSWORD
        CONNECTION_STRING = ';'.join([driver,server,database,hiveserv,auth,uid,pwd])
        connection = pyodbc.connect(CONNECTION_STRING, autocommit=True)
        cursor=connection.cursor()


        #Create Hive database and tables
        queryString = "create database if not exists nyctaxidb;"
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.trip
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            rate_code string,
                            store_and_fwd_flag string,
                            pickup_datetime string,
                            dropoff_datetime string,
                            passenger_count int,
                            trip_time_in_secs double,
                            trip_distance double,
                            pickup_longitude double,
                            pickup_latitude double,
                            dropoff_longitude double,
                            dropoff_latitude double)  
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.fare
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            pickup_datetime string,
                            payment_type string,
                            fare_amount double,
                            surcharge double,
                            mta_tax double,
                            tip_amount double,
                            tolls_amount double,
                            total_amount double)
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)


        #Upload data from blob storage tooHDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* 或者，您可以依照這[逐步解說](machine-learning-data-science-process-hive-walkthrough.md)tooupload NYC 計程車資料 tooHDI 叢集。 主要步驟包括：
  
  * AzCopy： 下載公用 blob tooyour 本機資料夾從壓縮的 CSV
  * AzCopy： 上傳解壓縮的 CSV 的從本機資料夾 tooHDI 叢集
  * 登入 hello Hadoop 叢集前端節點，並準備進行探勘測試的資料分析

Hello 資料是載入的 tooHDI 叢集之後，您可以檢查您在 Azure 儲存體總管 中的資料。 而您會在 HDI 叢集中建立資料庫 nyctaxidb。

**資料探索：Python 中的 Hive 查詢**

由於 hello 資料在 Hadoop 叢集，您可以使用 hello pyodbc 封裝 tooconnect tooHadoop 叢集與使用 Hive toodo 瀏覽和特徵設計查詢資料庫。 您可以檢視 hello hello 必要的步驟中建立的現有資料表。

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![檢視現有的表格](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

讓我們看看 hello 中的記錄數的每個月份和 hello 頻率 （雪人） 或不在 hello 路線資料表：

    queryString = """
        select month, count(*) from nyctaxidb.trip group by month;
        """
    results = pd.read_sql(queryString,connection)

    %matplotlib inline

    results.columns = ['month', 'trip_count']
    df = results.copy()
    df.index = df['month']
    df['trip_count'].plot(kind='bar')


![每個月的記錄數繪圖](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Number_Records_by_Month_v3.PNG)

    queryString = """
        SELECT tipped, COUNT(*) AS tip_freq
        FROM
        (
            SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
            FROM nyctaxidb.fare
        )tc
        GROUP BY tipped;
        """
    results = pd.read_sql(queryString,connection)

    results.columns = ['tipped', 'trip_count']
    df = results.copy()
    df.index = df['tipped']
    df['trip_count'].plot(kind='bar')


![小費頻率繪圖](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Frequency_tip_or_not_v3.PNG)

我們可以也計算 hello 收取位置與 dropoff 位置之間的距離，然後比較 toohello 成為距離。

    queryString = """
                    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
                        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
                        *radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
                        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
                        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
                        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*
                        pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance
                        from nyctaxidb.trip
                        where month=1
                            and pickup_longitude between -90 and -30
                            and pickup_latitude between 30 and 90
                            and dropoff_longitude between -90 and -30
                            and dropoff_latitude between 30 and 90;
                """
    results = pd.read_sql(queryString,connection)
    results.head(5)


![上下車資料表](./media/machine-learning-data-science-vm-do-ten-things/Exploration_compute_pickup_dropoff_distance_v2.PNG)

    results.columns = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude',
                       'dropoff_latitude', 'trip_distance', 'trip_time_in_secs', 'direct_distance']
    df = results.loc[results['trip_distance']<=100] #remove outliers
    df = df.loc[df['direct_distance']<=100] #remove outliers
    plt.scatter(df['direct_distance'], df['trip_distance'])


![收取/dropoff 距離 tootrip 距離的圖](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

現在讓我們準備縮減取樣 (1%) 資料集，以便進行模型分析。 我們可以在 Machine Learning 讀取器模組中使用此資料。

        queryString = """
        create  table if not exists nyctaxi_downsampled_dataset_testNEW (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\\n'
        stored as textfile;
        """
        cursor.execute(queryString)

        --- now insert contents of hello join into hello preceding internal table

        queryString = """
        insert overwrite table nyctaxi_downsampled_dataset_testNEW
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class
        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance,
        rand() as sample_key

        from trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01
        """
        cursor.execute(queryString)

在一段時間之後, 您可以看到已經載入 hello 資料在 Hadoop 叢集：

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![資料表](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

**使用 Machine Learning 從 HDI 讀取資料：讀取器模組**

您也可以使用 hello**讀取器**Machine Learning Studio tooaccess hello 資料庫 Hadoop 叢集中的模組中。 插入的 HDI 叢集 hello 認證，Azure 儲存體帳戶 tooenable 建置正執行機器學習模型 HDI 叢集在使用資料庫。

![讀取器模組屬性](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

hello 評分資料集之後可以檢視：

![檢視已評分的資料集](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a>Azure SQL 資料倉儲和資料庫
Azure SQL 資料倉儲是彈性的資料倉儲即服務，具有企業層級的 SQL Server 體驗。

您可以依照 hello 指示在此提供佈建 Azure SQL 資料倉儲[文章](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md)。 一旦您佈建 Azure SQL 資料倉儲，您可以使用這個[逐步解說](machine-learning-data-science-process-sqldw-walkthrough.md)toodo 上傳的資料，探索和使用 hello SQL 資料倉儲內的資料模型。

#### <a name="azure-cosmos-db"></a>Azure Cosmos DB
Azure Cosmos DB 是 hello 雲端的 NoSQL 資料庫。 它可讓您 toowork 類似 JSON 文件，並可讓您 toostore 和查詢 hello 文件。

您需要的 hello DSVM 下列每個必要條件步驟 tooaccess Azure Cosmos DB toodo hello。

1. 安裝 DocumentDB Python SDK (從命令提示字元執行 ```pip install pydocumentdb``` )
2. 從 [Azure 入口網站](https://portal.azure.com)建立 Azure Cosmos DB 帳戶和資料庫
3. 從下載 < Azure Cosmos DB 移轉工具 >[這裡](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d)並解壓縮您選擇的 tooa 目錄
4. 匯入 JSON 資料 （火山資料） 儲存在[公用 blob](https://cahandson.blob.core.windows.net/samples/volcano.json)到 Cosmos DB，利用下列命令參數 toohello 移轉工具 (dtui.exe hello hello Cosmos DB 移轉工具的安裝所在的目錄中)。 輸入 hello 來源和目標位置，使用這些參數：
   
    /s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1

一旦您匯入 hello 資料，您可以移 tooJupyter 然後開啟 hello 筆記本標題為*DocumentDBSample*包含 python 程式碼 tooaccess DocumentDB 並執行一些基本的查詢。 您可以進一步了解 Cosmos DB 瀏覽 hello 服務[文件頁面](https://docs.microsoft.com/azure/cosmos-db/)。

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a>8.建立報表和儀表板使用 hello Power BI Desktop
讓我們將視覺化 hello 在 Power BI toogain 視覺化資料的深入 hello 之前 Cosmos DB 範例中的 hello 火山 JSON 檔案。 會提供在 hello 詳細的步驟[Power BI 文件](../cosmos-db/powerbi-visualize.md)。 Hello 高階步驟如下：

1. 開啟 Power BI Desktop 並執行「取得資料」。 指定與 hello URL: https://cahandson.blob.core.windows.net/samples/volcano.json
2. 您應該會看見 hello JSON 記錄清單以匯入
3. 轉換 hello 清單 tooa 資料表，以便讓 Power BI 可以搭配 hello 相同
4. 展開即可 hello hello 資料行展開圖示 (hello 一個 hello hello 方 hello 資料行上的 「 向的左鍵和向右箭號 」 圖示)
5. 請注意，該位置是「記錄」欄位。 展開 hello 記錄，然後選取 只 hello 座標。 座標是清單資料行
6. 將新資料行 tooconvert hello 清單座標的資料行加入至逗號分隔 LatLong 資料行串連 hello 座標欄位使用 hello 公式中的 hello 兩個項目```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```。
7. 轉換 hello```Elevation```資料行 tooDecimal 和選取 hello**關閉**和**套用**。

而不是上述步驟，您可以貼上下列指令碼中使用的 hello 步驟的程式碼的 hello hello 可讓您的查詢語言的 toowrite hello 資料轉換的 Power BI 中的 進階編輯器。

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



您現在會有您 Power BI 資料模型中的 hello 資料。 您的 Power BI Desktop 應該如下所示：

![Power BI 桌面](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

您可以開始建立報表和視覺效果使用 hello 資料模型。 您可以遵循這個 hello 步驟[Power BI 文件](../cosmos-db/powerbi-visualize.md#build-the-reports)toobuild 報表。 hello 最終結果是，看起來像 hello 下列報表。

![Power BI Desktop 報告檢視 - Power BI 連接器](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a>9.動態調整您的專案需要您 DSVM toomeet
您可以調整您的專案需要 hello DSVM toomeet 上下。 如果您不需要 toouse hello VM hello 夜晚或週末中，您可以只關閉 hello VM 從 hello [Azure 入口網站](https://portal.azure.com)。

> [!NOTE]
> 如果您使用只 hello 作業系統關機按鈕 hello VM 上，您就會產生計算費用。  
> 
> 

如果您需要 toohandle 某些大規模的分析，而且需要更多的 CPU 和 （或） 記憶體及/或磁碟容量，您可以找到 CPU 核心、 記憶體容量和磁碟型別 （包括固態硬碟） 符合您的計算和預算需求方面的 VM 大小的大型選項。 hello 的 Vm 以及其每小時的計算定價的完整清單位於 hello [Azure 虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/)頁面。

同樣地，如果您需要處理的 VM 容量減少 (例如： 您將主要工作負載 tooa Hadoop 或 Spark 叢集，以)，您可以從 hello hello 叢集調降規模[Azure 入口網站](https://portal.azure.com)或傳送您的 VM toohello 設定執行個體。 以下為螢幕擷取畫面。

![VM 執行個體設定](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a>10.在虛擬機器上安裝其他工具
我們有封裝數個工具，我們相信是許多 hello 常見的資料分析需求，而且應該儲存您時間避免 tooinstall 一個環境並設定您，以節省成本支付只資源，您可以 tooaddress使用。

您可以利用其他 Azure 的資料和分析服務剖析此發行項 tooenhance 分析環境。 我們了解，在某些情況下您的需求可能需要額外的工具，包括一些專屬的協力廠商工具。 您具有完整系統管理權限 hello 虛擬機器 tooinstall 新所需的工具。 您也可以在 Python 和 R 中安裝其他未預先安裝的封裝。 對於 Python，您可以使用 ```conda``` 或 ```pip```。 中，您可以使用 hello```install.packages()```在 hello R 主控台或使用 hello IDE，並選擇 "**封裝** -> **安裝套件...**".

## <a name="summary"></a>摘要
這些是一些您可以在 hello Microsoft Data Science 虛擬機器上執行的 hello 事項。 有更多項目，您可以執行 toomake 它有效分析環境。

