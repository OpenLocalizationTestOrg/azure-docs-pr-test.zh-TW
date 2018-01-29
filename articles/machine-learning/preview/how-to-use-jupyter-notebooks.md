---
title: "如何在 Azure Machine Learning Workbench 中使用 Jupyter Notebook | Microsoft Docs"
description: "使用 Azure Machine Learning Workbench 的 Jupyter Notebook 功能指南"
services: machine-learning
author: rastala
ms.author: roastala
manager: haining
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.topic: article
ms.date: 11/09/2017
ms.openlocfilehash: 9d8a9f1c32578abff1d98e093469e1a780f6cd80
ms.sourcegitcommit: 1d8612a3c08dc633664ed4fb7c65807608a9ee20
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="how-to-use-jupyter-notebook-in-azure-machine-learning-workbench"></a>如何在 Azure Machine Learning Workbench 中使用 Jupyter Notebook

Azure Machine Learning Workbench 透過它與 Jupyter Notebook 的整合，來支援互動式資料科學實驗。 本文說明如何有效地運用此功能，來增加互動式資料科學實驗的速率及品質。

## <a name="prerequisites"></a>必要條件
- [安裝與建立 Azure Machine Learning](quickstart-installation.md)。
- 熟悉 [Jupyter Notebook](http://jupyter.org/) \(英文\)，因為本文不會教導如何使用 Jupyter。

## <a name="jupyter-notebook-architecture"></a>Jupyter Notebook 架構
概括而言，Jupyter Notebook 架構包含三個元件，每個均可在不同的計算環境中執行：

- **用戶端**：接收使用者輸入並顯示轉譯的輸出
- **伺服器**：裝載筆記本檔案 (.ipynb 檔案) 的網頁伺服器
- **核心**：實際執行筆記本資料格的執行階段環境

如需詳細資訊，請參閱官方 [Jupyter 文件](http://jupyter.readthedocs.io/en/latest/architecture/how_jupyter_ipython_work.html) \(英文\)。 下圖描述此用戶端、伺服器和核心架構如何對應到 Azure ML 中的元件。

![筆記本架構](media/how-to-use-jupyter-notebooks/how-to-use-jupyter-notebooks-architecture.png)

## <a name="kernels-in-azure-ml-workbench-notebook"></a>Azure ML Workbench 筆記本中的核心
在專案的 `aml_config` 資料夾中設定回合組態和計算目標，就能在 Azure ML Workbench 中存取許多不同核心。 藉由發出 `az ml computetarget attach` 命令來新增計算目標，相當於新增核心。

>[!NOTE]
>如需更多執行組態與計算目標的詳細資料，請檢閱[設定執行](experimentation-service-configuration.md)。

### <a name="kernel-naming-convention"></a>核心命名慣例
核心通常會以 "\<專案名稱> \<執行組態名稱>" 格式來命名。 例如，如果您在名為 _myIris_ 的專案中擁有名為 _docker-python_ 的執行組態，則當您開啟 Jupyter Notebook 時，就能在核心清單中找到名為 "myIris docker-python" 的核心。

Workbench 目前支援下列類型的核心。

### <a name="local-python-kernel"></a>本機 Python 核心
此 Python 核心支援在本機電腦上執行。 它會與 Azure Machine Learning 的執行歷程記錄支援整合。 核心名稱通常是 "my_project_name local"。

>[!NOTE]
>請勿使用「Python 3 」核心。 它是 Jupyter 預設提供的獨立核心。 它不會與 Azure Machine Learning 的功能整合。

### <a name="python-kernel-in-docker-local-or-remote"></a>Docker (本機或遠端) 中的 Python 核心
此 Python 核心會在您本機電腦上或遠端 Linux VM 上的 Docker 容器中執行。 核心名稱通常是 "my_project docker"。 相關聯的 `docker.runconfig` 檔案具有已設為 `Python` 的 `Framework` 欄位。

### <a name="pyspark-kernel-in-docker-local-or-remote"></a>Docker (本機或遠端) 中的 PySpark 核心
此 PySpark 核心會在您的本機電腦上或遠端 Linux VM 上，於 Docker 容器內部執行的 Spark 內容中執行指令碼。 核心名稱通常是 "my_project docker"。 相關聯的 `docker.runconfig` 檔案具有已設為 `PySpark` 的 `Framework` 欄位。

### <a name="pyspark-kernel-on-hdinsight-cluster"></a>HDInsight 叢集上的 PySpark 核心
此核心會在遠端 HDInsight 叢集中執行，而您已連接該叢集作為專案的計算目標。 核心名稱通常是 "my_project my_hdi"。 

>[!IMPORTANT]
>在 HDI 計算目標的 `.compute` 檔案中，您必須將 `yarnDeployMode` 欄位變更為 `client` (預設值是 `cluster`)，才能使用此核心。 

## <a name="start-jupyter-server-from-the-workbench"></a>從 Workbench 啟動 Jupyter 伺服器
從 Azure Machine Learning Workbench，可透過 Workbench 的 [筆記本] 索引標籤存取筆記本。Classifying Iris (將蝴蝶花分類) 範例專案包含 `iris.ipynb` 範例筆記本。

![筆記本索引標籤](media/how-to-use-jupyter-notebooks/how-to-use-jupyter-notebooks-01.png)

在 Azure Machine Learning Workbench 中開啟筆記本時，即會以**預覽模式**在它自己的文件索引標籤中顯示它。 這是不需要執行 Jupyter 伺服器及核心的唯讀檢視。

![筆記本預覽](media/how-to-use-jupyter-notebooks/how-to-use-jupyter-notebooks-02.png)

按一下 [啟動筆記本伺服器] 按鈕，即會啟動 Jupyter 伺服器，然後將筆記本切換至**編輯模式**。 熟悉的 Jupyter Notebook 使用者介面會以內嵌於 Workbench 中的形式顯示。 您現在可以從 [核心] 功能表設定核心，並啟動您的互動式筆記本工作階段。 

>[!NOTE]
>請注意，針對非本機的核心，如果您第一次使用它，則可能需要一兩分鐘的時間才會啟動。 您可以從 CLI 視窗執行 `az ml experiment prepare` 命令來準備計算目標，讓核心能夠在備妥計算目標之後更快速啟動。

![編輯模式](media/how-to-use-jupyter-notebooks/how-to-use-jupyter-notebooks-04.png)

這是完全互動的 Jupyter Notebook 體驗。 這個視窗支援所有一般的筆記本操作和鍵盤快速鍵，但某些檔案操作例外，因為它們可以透過 Workbench [筆記本] 索引標籤和 [檔案] 索引標籤來完成。

## <a name="start-jupyter-server-from-command-line"></a>從命令列啟動 Jupyter 伺服器
您也可以從命令列視窗發出 `az ml notebook start` 來啟動筆記本工作階段：
```
$ az ml notebook start
[I 10:14:25.455 NotebookApp] The port 8888 is already in use, trying another port.
[I 10:14:25.464 NotebookApp] Serving notebooks from local directory: /Users/johnpelak/Desktop/IrisDemo
[I 10:14:25.465 NotebookApp] 0 active kernels 
[I 10:14:25.465 NotebookApp] The Jupyter Notebook is running at: http://localhost:8889/?token=1f0161ab88b22fc83f2083a93879ec5e8d0ec18490f0b953
[I 10:14:25.465 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 10:14:25.466 NotebookApp] 
    
    Copy/paste this URL into your browser when you connect for the first time,
    to login with a token:
        http://localhost:8889/?token=1f0161ab88b22fc83f2083a93879ec5e8d0ec18490f0b953
[I 10:14:25.759 NotebookApp] Accepting one-time-token-authenticated connection from ::1
[I 10:16:52.970 NotebookApp] Kernel started: 7f8932e0-89b9-48b4-b5d0-e8f48d1da159
[I 10:16:53.854 NotebookApp] Adapting to protocol v5.1 for kernel 7f8932e0-89b9-48b4-b5d0-e8f48d1da159
```
隨即會使用 Jupyter 伺服器自動啟動您的預設瀏覽器並指向專案主目錄。 您也可以使用 CLI 視窗中顯示的 URL 和 Token，本機啟動其他瀏覽器視窗。 

![專案儀表板](media/how-to-use-jupyter-notebooks/how-to-use-jupyter-notebooks-07.png)

您現在可以按一下 `.ipynb` 筆記本檔案、開啟它並設定核心 (如果尚未設定)，然後啟動您的互動式工作階段。

![專案儀表板](media/how-to-use-jupyter-notebooks/how-to-use-jupyter-notebooks-08.png)

## <a name="use-magic-commands-to-manage-experiments"></a>使用 magic 命令來管理實驗

您可以在筆記本資料格中使用 [magic 命令](http://ipython.readthedocs.io/en/stable/interactive/magics.html)，來追蹤執行歷程記錄和儲存輸出，例如模型或資料集。

若要追蹤個別筆記本資料格的執行，使用 "%azureml history on" magic 命令。 開啟歷程記錄之後，每一個資料格執行將在執行歷程記錄中顯示為一個項目。

```
%azureml history on
from azureml.logging import get_azureml_logger
logger = get_azureml_logger()
logger.log("Cell","Load Data")
```

若要關閉資料格執行追蹤，使用 "%azureml history off" magic 命令。

您可以使用 "%azureml upload" magic 命令來儲存您的執行的模型和資料檔案。 在指定執行的執行歷程記錄檢視中，已儲存的物件會顯示為輸出。

```
modelpath = os.path.join("outputs","model.pkl")
with open(modelpath,"wb") as f:
    pickle.dump(model,f)
%azureml upload outputs/model.pkl
```

>[!NOTE]
>輸出都必須儲存到名為 "outputs" 的資料夾。

## <a name="next-steps"></a>後續步驟
- 若要了解如何使用 Jupyter Notebook，請造訪 [Jupyter 官方文件](http://jupyter-notebook.readthedocs.io/en/latest/) \(英文\)。    
- 若要更深入了解 Azure ML 測試執行環境，請檢閱 [Azure Machine Learning 測試服務概觀](experimentation-service-configuration.md)

