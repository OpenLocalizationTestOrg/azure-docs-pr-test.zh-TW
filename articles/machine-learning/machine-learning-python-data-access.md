---
title: "Machine Learning python azure Python 用戶端程式庫 aaaAccess 資料集 |Microsoft 文件"
description: "安裝和使用 Python 用戶端程式庫 tooaccess hello 和管理 Azure Machine Learning 資料安全地從本機 Python 環境。"
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a>使用 Python 使用 hello Azure Machine Learning python azure Python 用戶端程式庫的存取資料集
Microsoft Azure Machine Learning python azure Python 用戶端程式庫的 hello 預覽可以啟用安全存取 tooyour 本機的 Python 環境的 Azure Machine Learning 資料集，並啟用 hello 建立和管理的工作區中的資料集。

本主題提供如何執行以下作業的指示：

* 安裝 hello Machine Learning python azure Python 用戶端程式庫 
* 存取和上傳資料集，包括如何指示 tooget 授權 tooaccess 來自本機 Python 環境的 Azure Machine Learning 資料集
* 存取實驗中的中繼資料集
* 使用 hello Python 用戶端程式庫 tooenumerate 資料集、 存取中繼資料、 讀取資料集 hello 內容、 建立新的資料集以及更新現有的資料集

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="prerequisites"></a>必要條件
hello Python 用戶端程式庫已經過測試，在下列環境的 hello:

* Windows、Mac 及 Linux
* Python 2.7、3.3 及 3.4

它會相依於下列套件 hello 時：

* requests
* python-dateutil
* pandas

我們建議使用，例如 Python 發佈[Anaconda](http://continuum.io/downloads#all)或[Canopy](https://store.enthought.com/downloads/)，它會使用 Python，IPython 與上面所列的 hello 三個封裝安裝。 雖然不一定需要 IPython，但它是以互動方式操作和虛擬化資料的絕佳環境。

### <a name="installation"></a>如何 tooinstall hello Azure Machine Learning python azure Python 用戶端程式庫
hello Azure Machine Learning python azure Python 用戶端程式庫也必須是本主題所述安裝的 toocomplete hello 工作。 它是可從 hello [Python 封裝索引](https://pypi.python.org/pypi/azureml)。 tooinstall 它在 Python 環境中，執行下列命令，從本機 Python 環境的 hello:

    pip install azureml

或者，您可以下載並安裝來自 hello 來源上[github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python)。

    python setup.py install

如果您有安裝在您的電腦上的 git，您可以使用 pip tooinstall 直接從 hello git 儲存機制：

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <a name="datasetAccess"></a>使用 Studio 程式碼片段 tooaccess 資料集
hello Python 用戶端程式庫可讓您以程式設計方式存取 tooyour 現有資料集已執行的實驗中。

從 hello Studio web 介面，您可以產生程式碼片段，其中包括所有 hello 所需的資訊 toodownload 及還原序列化為熊資料框架物件，您位置的電腦上的資料集。

### <a name="security"></a>資料存取安全性
hello Studio 所提供的工作區識別碼和授權，包括與 hello Python 用戶端程式庫搭配使用的程式碼片段語彙基元。 這些提供完整存取 tooyour 工作區，必須受到保護，像是密碼一樣。

基於安全性理由，hello 程式碼片段時，才功能已設定為其角色的可用 toousers**擁有者**hello 工作區。 您的角色會顯示 Azure Machine Learning Studio 中的 hello**使用者**頁面**設定**。

![安全性][security]

如果您的角色未設定為**擁有者**，您可以要求 toobe reinvited 作為擁有者，或要求擁有者 hello hello 工作區 tooprovide 您與 hello 程式碼片段。

tooobtain hello 授權權杖，您可以執行 hello 下列其中一種：

* 向擁有者要求權杖。 擁有者可以從他們的工作區在 Studio 中的 hello [設定] 頁面存取其授權權杖。 選取**設定**從左窗格中，然後按一下 hello**授權權杖**toosee hello 主要和次要的語彙基元。  雖然主要 hello 次要授權權杖可以用 hello 程式碼片段中，建議的擁有者只能共用 hello 次要授權權杖。

![授權權杖](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* 要求升級 toobe toorole 的擁有者。  toodo 這 hello 工作區需要 toofirst 的目前擁有者移除您從 hello] 工作區，然後重新邀請您 tooit 作為擁有者。

一旦開發人員取得 hello 工作區識別碼和授權權杖，它們會是能 tooaccess hello 工作區中使用 hello 程式碼片段，不論其角色。

授權權杖上 hello 管理**授權權杖**頁面**設定**。 您可以重新產生它們，但此程序撤銷存取 toohello 之前語彙基元。

### <a name="accessingDatasets"></a>從本機 Python 應用程式存取資料集
1. 在機器學習 Studio 中，按一下 [**資料集**hello hello 左側的導覽列中。
2. 選取您想要 tooaccess hello 資料集。 您可以選取任何的 hello 資料集從 hello**我的資料集**清單或從 hello**範例**清單。
3. 從 hello 底部工具列中按一下**產生的資料存取程式碼**。 如果 hello 資料與 hello Python 用戶端程式庫不相容的格式，此按鈕會停用。
   
    ![資料集][datasets]
4. 從出現的 hello 視窗選取 hello 程式碼片段，並將它複製 tooyour 剪貼簿。
   
    ![存取程式碼][dataset-access-code]
5. Hello 程式碼貼到您本機的 Python 應用程式的 hello 筆記本。
   
    ![筆記本][ipython-dataset]

## <a name="accessingIntermediateDatasets"></a>存取機器學習服務實驗中的中繼資料
在 hello Machine Learning Studio 中執行實驗之後，就可能 tooaccess hello 中繼資料集從 hello 輸出節點的模組。 中繼資料集是指當模型工具執行時
為中繼步驟建立和使用的資料。

Hello 資料格式為 hello Python 用戶端程式庫相容時，可以存取中繼資料集。

hello 支援下列格式 (這些常數會在 hello`azureml.DataTypeIds`類別):

* 純文字
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

您可以判斷 hello 格式，將滑鼠游標停留在模組輸出節點。 它會顯示並以工具提示中的 hello 節點名稱。

某些 hello 模組，例如 hello[分割][ split]模組，名為輸出 tooa 格式`Dataset`，hello Python 用戶端程式庫不支援的。

![資料集格式][dataset-format]

您需要 toouse 轉換模組，例如[轉換 tooCSV][convert-to-csv]，tooget 輸出成支援的格式。

![GenericCSV 格式][csv-format]

hello 下列步驟示範的範例會建立一個試驗、 執行及存取 hello 中繼資料集。

1. 建立新實驗。
2. 插入 [成人收入普查二進位分類資料集]  模組。
3. 插入[分割][ split]模組，並連接其輸入的 toohello 資料集模組輸出。
4. 插入[轉換 tooCSV] [ convert-to-csv]模組，並連接的 hello 其輸入的 tooone[分割][ split]模組會輸出。
5. 儲存 hello 實驗中，執行並等候它 toofinish 執行。
6. 按一下 hello 輸出節點上 hello[轉換 tooCSV] [ convert-to-csv]模組。
7. Hello 操作功能表出現時，選取**產生的資料存取程式碼**。
   
    ![內容功能表][experiment]
8. 選取 hello 程式碼片段，並將它從出現的 hello 視窗複製 tooyour 剪貼簿。
   
    ![存取程式碼][intermediate-dataset-access-code]
9. 在筆記本中，貼上 hello 程式碼。
   
    ![筆記本][ipython-intermediate-dataset]
10. 您可以視覺化使用 matplotlib hello 資料。 這會顯示 hello age 資料行的長條圖中：
    
    ![長條圖][ipython-histogram]

## <a name="clientApis"></a>使用 hello Machine Learning python azure Python 用戶端程式庫 tooaccess、 讀取、 建立及管理資料集
### <a name="workspace"></a>工作區
hello 工作區是 hello hello Python 用戶端程式庫的進入點。 提供 hello`Workspace`工作區識別碼和授權權杖 toocreate 類別執行個體：

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a>列舉資料集
tooenumerate 指定的工作區中的所有資料集：

    for ds in ws.datasets:
        print(ds.name)

tooenumerate 只 hello 使用者建立資料集：

    for ds in ws.user_datasets:
        print(ds.name)

tooenumerate 只 hello 範例資料集：

    for ds in ws.example_datasets:
        print(ds.name)

您可以依名稱 (區分大小寫) 存取資料集：

    ds = ws.datasets['my dataset name']

或您可以依索引來存取：

    ds = ws.datasets[0]


### <a name="metadata"></a>中繼資料
資料集有中繼資料，加法 toocontent 中。 （中繼資料集是例外狀況 toothis 規則和並沒有任何中繼資料）。

在建立時指派 hello 使用者一些中繼資料值：

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

其他則是由 Azure ML 指派的值：

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

請參閱 hello`SourceDataset`多個在 hello 可用的中繼資料的類別。

### <a name="read-contents"></a>讀取內容
hello 程式碼片段 Machine Learning Studio 所提供的自動下載並 hello 資料集 tooa 熊資料框架物件還原序列化。 這是以 hello`to_dataframe`方法：

    frame = ds.to_dataframe()

如果您偏好 toodownload hello 未經處理資料，並自行執行 hello 還原序列化時，這是一個選項。 在 hello 的時刻，這是 hello 的格式，例如 'ARFF'，無法還原序列化的 hello Python 用戶端程式庫的唯一選項。

以文字 tooread hello 內容：

    text_data = ds.read_as_text()

為二進位 tooread hello 內容：

    binary_data = ds.read_as_binary()

您也可以開啟資料流 toohello 內容：

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a>建立新的資料集
hello Python 用戶端程式庫可讓您從您的 Python 程式 tooupload 資料集。 這些資料集接著可在您的工作區中使用。

如果您將資料熊資料框架中，使用下列程式碼的 hello:

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

如果您的資料已經序列化，則可以使用：

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

hello Python 用戶端程式庫是無法 tooserialize 熊資料框架 toohello 下列格式 (這些常數會在 hello`azureml.DataTypeIds`類別):

* 純文字
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

### <a name="update-an-existing-dataset"></a>更新現有資料集
如果您嘗試 tooupload 新的資料集，以符合現有的資料集的名稱，您應該取得衝突錯誤。

tooupdate 現有的資料集，您必須先 tooget 參考 toohello 現有資料集：

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

然後使用`update_from_dataframe`hello Azure 上的資料集 tooserialize 和取代 hello 內容：

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

如果您想 tooserialize hello 資料 tooa 不同格式時，指定選擇性的 hello 值`data_type_id`參數。

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

指定給 hello 的值，您可以選擇設定新的描述`description`參數。

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

您可以選擇設定新的名稱所指定的值為 hello`name`參數。 從現在起，您會擷取 hello 資料集使用僅 hello 新名稱。 下列程式碼的 hello 更新 hello 資料、 名稱和描述。

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

hello `data_type_id`，`name`和`description`參數為選擇性，預設 tootheir 先前的值。 hello`dataframe`參數永遠是必要項。

如果您的資料已經序列化，請使用 `update_from_raw_data`，而不是 `update_from_dataframe`： 如果您只傳入 `raw_data`，而不是 `dataframe`，其會以類似方式運作。

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

