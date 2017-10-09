---
title: "aaaLearn toomanage AzureML web 服務使用 API 管理 |Microsoft 文件"
description: "顯示如何 toomanage AzureML web 服務以使用 API 管理指南。"
keywords: "機器學習,api 管理"
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a>了解如何 toomanage AzureML web 服務以使用 API 管理
## <a name="overview"></a>概觀
本指南也說明如何 tooquickly 開始使用 API 管理 toomanage AzureML web 服務。

## <a name="what-is-azure-api-management"></a>什麼是 Azure API 管理？
Azure API 管理是一項 Azure 服務，可讓您藉由定義使用者存取、使用節流設定和儀表板監視，來管理 REST API 端點。 如需 Azure API 管理的詳細資訊，請按一下 [這裡](https://azure.microsoft.com/services/api-management/) 。 按一下[這裡](../api-management/api-management-get-started.md)上 tooget 如何開始使用 Azure API 管理指南。 這是本指南所依據的另一份指南，涵蓋更多主題，包括通知組態、定價層、回應處理、使用者驗證、建立產品、開發人員訂用帳戶和使用量儀表板。

## <a name="what-is-azureml"></a>什麼是 AzureML？
AzureML 是一項 Azure 服務的機器學習服務，可讓您 tooeasily 組建、 部署及共用進階的分析解決方案。 如需 AzureML 的詳細資訊，請按一下 [這裡](https://azure.microsoft.com/services/machine-learning/) 。

## <a name="prerequisites"></a>必要條件
toocomplete 本指南中，您需要：

* 一個 Azure 帳戶。 如果您沒有 Azure 帳戶，按一下[這裡](https://azure.microsoft.com/pricing/free-trial/)的詳細資料 toocreate 免費試用帳戶。
* AzureML 帳戶。 如果您沒有 AzureML 帳戶，按一下[這裡](https://studio.azureml.net/)的詳細資料 toocreate 免費試用帳戶。
* hello 工作區、 服務及部署為 web 服務 AzureML 實驗 api_key。 按一下[這裡](machine-learning-create-experiment.md)如 toocreate AzureML 的進行實驗的詳細資訊。 按一下[這裡](machine-learning-publish-a-machine-learning-web-service.md)如 toodeploy AzureML 實驗為 web 服務的方式的詳細資訊。 或者，附錄 A 中的方式 toocreate 和測試簡單 AzureML 實驗，並將其部署為 web 服務的指示。

## <a name="create-an-api-management-instance"></a>建立 API 管理執行個體
以下是使用 API 管理 toomanage hello 步驟 AzureML web 服務。 首先建立服務執行個體。 登入 toohello[傳統入口網站](https://manage.windowsazure.com/)按一下**新增** > **應用程式服務** > **API 管理** > **建立**。

![建立執行個體](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

指定唯一的 **URL**。 本指南使用**demoazureml** – 您將需要 toochoose 項目不同。 選擇所需的 hello**訂用帳戶**和**區域**服務執行個體。 之後您的選擇，請按一下 hello 下一步 按鈕。

![建立服務 1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

指定的值為 hello**組織名稱**。 本指南使用**demoazureml** – 您將需要 toochoose 項目不同。 輸入您的電子郵件地址中 hello**系統管理員電子郵件**欄位。 此電子郵件地址用於從 hello API 管理系統的通知。

![建立服務 2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

按一下 [hello] 核取方塊 toocreate 您服務執行個體。 *因此會佔用 toothirty 分鐘的時間，建立新服務 toobe*。

## <a name="create-hello-api"></a>建立 hello API
一旦建立 hello 服務執行個體，hello 下一個步驟是 toocreate hello API。 API 包含可自用戶端應用程式叫用的一組作業。 應用程式開發介面作業會代理 tooexisting web 服務。 本指南會建立現有 AzureML RR 和 BES web 服務的 proxy toohello 應用程式開發介面。

應用程式開發介面建立和設定從 hello API 發行者入口網站，可從 hello Azure 傳統入口網站存取。 tooreach hello 發行者入口網站中，選取您的服務執行個體。

![選取服務執行個體](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

按一下**管理**API 管理服務的 hello Azure 傳統入口網站中。

![管理服務](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

按一下**Api**從 hello **API 管理**hello 左、，然後按一下功能表**新增應用程式開發介面**。

![API 管理功能表](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

型別**AzureML 示範 API**為 hello **Web API 名稱**。 型別**https://ussouthcentral.services.azureml.net**為 hello **Web 服務 URL**。 型別**azureml 示範**為 hello **Web API URL 尾碼**。 請檢查**HTTPS**為 hello **Web API URL**配置。 在 [產品] 中，選取 [Starter]。 完成後，請按一下**儲存**toocreate hello 應用程式開發介面。

![加入新的 API](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a>新增 hello 作業
按一下**加入作業**tooadd 作業 toothis 應用程式開發介面。

![加入作業](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

hello**新作業**視窗會顯示與 hello**簽章**預設會選取索引標籤。

## <a name="add-rrs-operation"></a>加入 RRS 作業
先建立 hello AzureML RR 服務的作業。 選取**POST**為 hello **HTTP 指令動詞**。 型別**/workspaces/ {工作區} /services/ {服務} / 執行？ api 版本 = {microsoft.authorization} （& s) 詳細資料 = {詳細資料}**為 hello **URL 範本**。 型別**RR 執行**為 hello**顯示名稱**。

![加入 RRS 作業簽章](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

按一下**回應** > **新增**上 hello，然後選取**200 確定**。 按一下**儲存**toosave 這項作業。

![加入 RRS 作業回應](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a>加入 BES 作業
螢幕擷取畫面的不包括 hello BES 作業，因為它們是非常類似 toothose 新增 hello RR 作業。

### <a name="submit-but-not-start-a-batch-execution-job"></a>提交 (但不啟動) 批次執行工作
按一下**加入作業**tooadd hello AzureML BES 作業 toohello 應用程式開發介面。 選取**POST** hello **HTTP 指令動詞**。 型別**/workspaces/ {工作區} /services/ {服務} / 作業？ api 版本 = {microsoft.authorization}** hello **URL 範本**。 型別**BES 提交**hello**顯示名稱**。 按一下**回應** > **新增**上 hello，然後選取**200 確定**。 按一下**儲存**toosave 這項作業。

### <a name="start-a-batch-execution-job"></a>啟動批次執行工作
按一下**加入作業**tooadd hello AzureML BES 作業 toohello 應用程式開發介面。 選取**POST** hello **HTTP 指令動詞**。 型別**/workspaces/ {工作區} /services/ {服務} /jobs/ {jobid}] / [開始嗎？ 如果 api 版本 = {microsoft.authorization}** hello **URL 範本**。 型別**BES 啟動**hello**顯示名稱**。 按一下**回應** > **新增**上 hello，然後選取**200 確定**。 按一下**儲存**toosave 這項作業。

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a>收到 hello 狀態或批次執行作業的結果
按一下**加入作業**tooadd hello AzureML BES 作業 toohello 應用程式開發介面。 選取**取得**hello **HTTP 指令動詞**。 型別**/workspaces/ {工作區} /services/ {服務} /jobs/ {jobid}？ api 版本 = {microsoft.authorization}** hello **URL 範本**。 型別**BES 狀態**hello**顯示名稱**。 按一下**回應** > **新增**上 hello，然後選取**200 確定**。 按一下**儲存**toosave 這項作業。

### <a name="delete-a-batch-execution-job"></a>刪除批次執行工作
按一下**加入作業**tooadd hello AzureML BES 作業 toohello 應用程式開發介面。 選取**刪除**hello **HTTP 指令動詞**。 型別**/workspaces/ {工作區} /services/ {服務} /jobs/ {jobid}？ api 版本 = {microsoft.authorization}** hello **URL 範本**。 型別**BES 刪除**hello**顯示名稱**。 按一下**回應** > **新增**上 hello，然後選取**200 確定**。 按一下**儲存**toosave 這項作業。

## <a name="call-an-operation-from-hello-developer-portal"></a>從 hello 開發人員入口網站呼叫作業
作業可以直接從 hello 開發人員入口網站，可提供便利的方式 tooview 呼叫，並測試應用程式開發介面的 hello 作業。 在此快速入門步驟中您會呼叫 hello **RR 執行**方法已加入 toohello **AzureML 示範 API**。 按一下**開發人員入口網站**功能表在 hello hello hello 傳統入口網站的右上方。

![開發人員入口網站](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

按一下**Api**從 hello 最上層功能表，然後再按一下**AzureML 示範 API** toosee hello 可用的作業。

![demoazureml API](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

選取**RR 執行**hello 作業。 按一下 [試試看] 。

![試試看](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

要求參數，輸入您**工作區**，**服務**， **2.0** hello **microsoft.authorization**，和**true**hello**詳細資料**。 您可以找到您**工作區**和**服務**hello AzureML web 服務儀表板中 (請參閱**測試 hello web 服務**附錄 A 中)。

在 [要求標頭] 中，按一下 [新增標頭] 並輸入 **Content-Type** 和 **application/json**，然後按一下 [新增標頭] 並輸入 **Authorization** 和 **Bearer <YOUR AZUREML SERVICE API-KEY>**。 您可以找到您**api 金鑰**hello AzureML web 服務儀表板中 (請參閱**測試 hello web 服務**附錄 A 中)。

型別**{[輸入] 5d: {"input1": {"ColumnNames": ["Col2"]"值 」: [["This is 你好"]]}}，"GlobalParameters": {}}** hello 要求主體。

![AzureML 示範 API](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

按一下 [傳送] 。

![傳送](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

叫用作業之後，hello 開發人員入口網站會顯示 hello**要求 URL** hello 後端服務，從 hello**回應狀態**，hello**回應標頭**，和任何**回應內容**。

![回應狀態](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a>附錄 A - 建立及測試簡單的 AzureML Web 服務
### <a name="creating-hello-experiment"></a>建立 hello 實驗
以下是建立簡單的 AzureML 實驗，並將它部署為 web 服務的 hello 步驟。 web 服務會接受 hello 做為輸入任意文字資料行，並傳回一組以整數表示的功能。 例如：

| 文字 | 雜湊的文字 |
| --- | --- |
| 這是美好的一天 |1 1 2 2 0 2 0 1 |

首先，使用您選擇的瀏覽器瀏覽至： [https://studio.azureml.net/](https://studio.azureml.net/)並輸入您的認證 toolog 中。 接下來，建立新的空白實驗。

![搜尋實驗範本](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

將它重新命名過**SimpleFeatureHashingExperiment**。 展開 [儲存的資料集]，將 [來自 Amazon 的書籍評論] 拖曳到您的實驗。

![簡單的特徵雜湊實驗](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

展開 [資料轉換] 和 [操作]，將 [選取資料集中的資料行] 拖曳到您的實驗。 連接**書籍檢閱從 Amazon**太**資料集中選取的資料行**。

![選取資料行](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

按一下 選取資料集中的資料行，然後按一下啟動資料行選取器 並選取 Col2。 按一下 hello 核取記號 tooapply 這些變更。

![選取資料行](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

展開**文字分析**拖曳**特徵雜湊**到 hello 實驗。 連接**資料集中選取的資料行**太**特徵雜湊**。

![連接專案資料行](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

型別**3** hello**雜湊位元大小**。 這會建立 8 (23) 個資料行。

![雜湊位元大小](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

此時，您可能會想 tooclick**執行**tootest hello 實驗。

![執行](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a>建立 Web 服務
現在建立 Web 服務。 展開 [Web 服務]，將 [輸入] 拖曳到您的實驗。 連接**輸入**太**特徵雜湊**。 另將 [輸出]  拖曳到您的實驗。 連接**輸出**太**特徵雜湊**。

![輸出至特徵雜湊](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

按一下 [發佈 Web 服務] 。

![發佈 Web 服務](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

按一下**是**toopublish hello 實驗。

![[是] 表示發佈](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a>測試 hello web 服務
AzureML Web 服務是由 RSS (要求/回應服務) 和 BES (批次執行服務) 端點所組成。 RSS 適用於同步執行。 BES 適用於非同步工作執行。 您的 web 服務與 hello 以下的範例 Python 來源 tootest，您可能需要 toodownload 和安裝 hello Azure SDK for Python (請參閱：[如何 tooinstall Python](../python-how-to-install.md))。

您也需要 hello**工作區**，**服務**，和**api_key**的 hello 範例來源的下列實驗。 您可以按一下找到 hello 工作區和服務**要求/回應**或**批次執行**hello web 服務儀表板在您實驗。

![尋找工作區和服務](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

您可以找到 hello **api_key**按一下實驗 hello web 服務儀表板中的。

![尋找 API 金鑰](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a>測試 RRS 端點
##### <a name="test-button"></a>測試按鈕
輕鬆 tootest hello RR 端點是 tooclick**測試**hello web 服務儀表板上。

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

在 [col2] 中，輸入**這是美好的一天**。 按一下 hello 核取記號。

![輸入資料](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

您會看到類似下列畫面：

![範例輸出](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a>範例程式碼
另一個方式 tootest RR 您是從用戶端程式碼。 如果您按一下**要求/回應**在 hello 儀表板和捲動 toohello 底部，您會看到範例程式碼的 C#、 Python 和。您也會看到 hello 語法的 hello RR 要求，包括 hello 要求 URI、 標頭和主體。

本指南顯示一個運作正常的 Python 範例。 您將需要 toomodify 它以 hello**工作區**，**服務**，和**api_key**的實驗。

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a>測試 BES 端點
按一下**批次執行**hello 儀表板和捲動 toohello 下方。 您會看到的範例程式碼的 C#、 Python 和。您也會看到 hello 語法的 hello BES 要求 toosubmit 作業、 啟動工作、 取得 hello 狀態或作業的結果和刪除作業。

本指南顯示一個運作正常的 Python 範例。 您需要 toomodify 它以 hello**工作區**，**服務**，和**api_key**的實驗。 此外，您需要 toomodify hello**儲存體帳戶名稱**，**儲存體帳戶金鑰**，和**儲存體容器名稱**。 最後，您將需要 hello toomodify hello 位置**輸入的檔**和 hello hello 位置**輸出檔**。

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
