---
title: "Azure Machine Learning Web 服務：部署和取用 | Microsoft Docs"
description: "部署和使用 Web 服務的資源。"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a>Azure Machine Learning Web 服務：部署和取用
您可以使用 Azure 機器學習 toodeploy 機器學習服務工作流程與模型做為 web 服務。 這些 web 服務接著可以使用的 toocall hello 機器學習模型，從應用程式透過 hello 網際網路 toodo 預測即時或批次模式。 因為 hello web 服務是 RESTful，您可以從各種程式設計語言與平台，例如.NET 和 Java，並從應用程式，例如 Excel 加以呼叫。

hello 下一個區段提供連結 toowalkthroughs、 程式碼，以及文件 toohelp 協助您開始。

## <a name="deploy-a-web-service"></a>部署 Web 服務
### <a name="with-azure-machine-learning-studio"></a>使用 Azure Machine Learning Studio
Machine Learning Studio 和 hello Microsoft Azure 機器學習 Web 服務入口網站可協助您部署和管理 web 服務，而不需要撰寫程式碼。

hello 下列連結提供有關的一般資訊 toodeploy 新的 web 服務：

* 如需有關如何 toodeploy 新的 web 服務為基礎的 Azure 資源管理員中，請參閱概觀[部署新的 web 服務](machine-learning-webservice-deploy-a-web-service.md)。
* 如需逐步解說如何 toodeploy web 服務，請參閱[部署 Azure Machine Learning web 服務](machine-learning-publish-a-machine-learning-web-service.md)。
* 如需完整的逐步解說有關 toocreate 和部署 web 服務，請參閱[逐步解說步驟 1： 建立機器學習服務工作區](machine-learning-walkthrough-1-create-ml-workspace.md)。
* 如需部署 Web 服務的特定範例，請參閱︰

  * [逐步解說步驟 5： 部署的 hello Azure Machine Learning web 服務](machine-learning-walkthrough-5-publish-web-service.md)
  * [如何 toodeploy web 服務 toomultiple 區域](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a>使用 Web 服務資源提供者 API (Azure Resource Manager API)
web 服務的 hello Azure 機器學習資源提供者可讓部署及管理的 web 服務使用 REST API 呼叫。 如需詳細資訊，請參閱 [Machine Learning Web 服務 (REST)](/rest/api/machinelearning/index) 參考資料。

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a>使用 PowerShell Cmdlet
用於 Web 服務的 Azure Machine Learning 資源提供者，可利用 PowerShell Cmdlet 來部署和管理 Web 服務。

toouse hello cmdlet，您必須先登入 tooyour 從 hello PowerShell 環境中的 Azure 帳戶使用 hello[新增 AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet。 如果您不熟悉如何 toocall PowerShell 命令的採用資源管理員，請參閱[使用 Azure PowerShell 的 Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account)。

tooexport 您預測進行實驗，請使用[此範例程式碼](https://github.com/ritwik20/AzureML-WebServices)。 從 hello 程式碼建立 hello.exe 檔案之後，您可以輸入：

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

執行 hello 應用程式建立 web 服務的 JSON 範本。 toouse hello 範本 toodeploy web 服務，您必須新增 hello 下列資訊：

* 儲存體帳戶名稱和金鑰

    您可以從任一 hello 取得 hello 儲存體帳戶名稱和金鑰[Azure 入口網站](https://portal.azure.com/)或 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)。
* 承諾用量方案識別碼

    您可以從 hello 取得 hello 計劃 ID [Azure 機器學習 Web 服務](https://services.azureml.net)入口網站登入，然後按一下方案名稱。

將活動當做子系的 hello 加入 toohello JSON 範本*屬性*hello 節點相同層級為 hello *MachineLearningWorkspace*節點。

以下是範例：

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

請參閱下列文章 hello 和範例程式碼的其他詳細資料：

* [Azure Machine Learning Cmdlet](https://msdn.microsoft.com/library/azure/mt767952.aspx) 參考資料。
* GitHub 上的範例 [逐步解說](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt)

## <a name="consume-hello-web-services"></a>使用 hello web 服務
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a>從 hello Azure 機器學習 Web 服務使用者介面 （測試）
您可以測試您的 web 服務從 hello Azure 機器學習 Web 服務入口網站。 這包括測試 hello 要求-回應服務 (RR)，批次執行服務 (BES) 介面。

* [部署新的 Web 服務](machine-learning-webservice-deploy-a-web-service.md)
* [部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)
* [逐步解說步驟 5： 部署的 hello Azure Machine Learning web 服務](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a>從 Excel
您可以下載使用 hello web 服務的 Excel 範本：

* [從 Excel 使用 Azure Machine Learning Web 服務](machine-learning-consuming-from-excel.md)
* [適用於 Azure Machine Learning Web 服務的 Excel 增益集](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a>從以 REST 為基礎的用戶端
Azure Machine Learning Web 服務是 RESTful API。 您可以使用這些 Api，從各種平台，例如.NET、 Python、 R、 Java、 等 hello**取用**頁面為您的 web 服務上 hello [Microsoft Azure 機器學習 Web 服務入口網站](https://services.azureml.net)具有範例程式碼，可協助您開始使用。 如需詳細資訊，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)。
