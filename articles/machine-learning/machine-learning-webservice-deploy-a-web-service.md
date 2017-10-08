---
title: "新的 web 服務，Azure Machine Learning 中 aaaDeploying |Microsoft 文件"
description: "hello 工作流程的部署是 ARM 型 web 服務"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a>部署新的 Web 服務
Microsoft Azure Machine learning 現在提供 web 服務為基礎的[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)允許新的計費計劃選項，或部署您的 web 服務 toomultiple 區域。

hello 一般工作流程 toodeploy 使用 Microsoft Azure 機器學習 Web 服務的 web 服務是：

* 建立預測性實驗
* 進行部署
* 設定其名稱
* 計費方案
* 進行測試
* 加以取用。

hello 下列圖形說明 hello 工作流程。

![Web 服務部署工作流程][1]

## <a name="deploy-web-service-from-studio"></a>從 Studio 部署 Web 服務
toodeploy 做為新的 web 服務實驗中。 登入 hello Machine Learning Studio 並建立新的預測 web 服務。 

**注意**︰如果您已將實驗部署為傳統 Web 服務，您就無法將它部署為新的 Web 服務。

按一下**執行**底部 hello hello 試驗畫布，然後按一下**部署 Web 服務**和**部署 Web 服務 [New]**。 hello 部署的 hello Machine Learning Web 服務管理員 頁面將會開啟。

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a>機器學習 Web 服務管理員部署實驗頁面
在 hello 部署實驗 頁面上，輸入 hello web 服務的名稱。
選取定價方案。 如果您有現有的定價方案，您可以選取它，否則您必須建立新的價格計劃 hello 服務。 

1. 在 hello**價格計劃**下拉式清單中，選取現有的方案或選取 hello**選取新的計畫**選項。
2. 在**計劃名稱**，輸入會識別在帳單上的 hello 計劃的名稱。
3. 選取其中一個 hello**每月的計劃層**。 請注意，hello 計劃層預設 toohello 預設區域計劃您的 web 服務是部署的 toothat 區域。

按一下**部署**和您的 web 服務的 hello 快速入門頁面隨即開啟。

## <a name="quickstart-page"></a>快速入門頁面
hello web 服務快速入門 頁面提供您存取和指引 hello 最常見的工作，您將建立新的 web 服務之後執行。 從這裡您可以輕鬆地存取這兩個 hello**測試**頁面和**取用**頁面。

## <a name="testing-your-web-service"></a>測試您的 Web 服務
從 hello 快速入門 頁面上，按一下測試 web 服務在一般工作。   

tootest hello web 服務做為要求-回應服務 (RR):

* 按一下**測試**hello 功能表列上。
* 按一下 [要求-回應] 。
* Hello 實驗的輸入資料行中輸入適當的值。
* 按一下 [測試要求-回應] 。

您的結果會顯示 hello 右手邊的 hello 頁面上。

tootest 批次執行服務 (BES) web 服務，您將使用 CSV 檔案：

* 按一下**測試**hello 功能表列上。
* 按一下 [批次] 。
* 在您的輸入，按一下 瀏覽並瀏覽 tooyour 範例資料檔。
* 按一下 [ **測試**]。

您的測試 hello 狀態會顯示下**測試批次作業**。

## <a name="consuming-your-web-service"></a>取用您的 Web 服務
部署為 Web 服務時，Azure Machine Learning 實驗所提供的 REST API，可供各種裝置和平台使用。 這是因為 hello 簡單的 REST API 接受和回應使用 JSON 格式的訊息。 hello Azure Machine Learning 入口網站提供的程式碼可以用在 R、 C# 和 Python toocall hello web 服務。

您可以在 hello Consuming 頁面上找到：

* hello API 金鑰，URI 的使用中應用程式 web 服務。
* Excel 和 web 應用程式範本 tookick 開始耗用量程序。
* 您開始在 C#、 python 和 R tooget 的範例程式碼。

如需有關如何使用 web 服務的詳細資訊，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)。

## <a name="next-steps"></a>後續步驟
如需有關如何取用 Web 服務的詳細資訊，請參閱︰

[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)

[Azure Machine Learning Web 服務：部署和取用](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
