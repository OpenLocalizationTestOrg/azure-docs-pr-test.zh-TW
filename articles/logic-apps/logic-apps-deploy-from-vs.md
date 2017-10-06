---
title: "aaaCreate、 建置及部署 Visual Studio-Azure 邏輯應用程式中的 logic apps |Microsoft 文件"
description: "建立 Visual Studio 專案，讓您能夠設計、建置和部署 Azure Logic Apps。"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a>在 Visual Studio 中設計、建置和部署 Azure Logic Apps

雖然 hello [Azure 入口網站](https://portal.azure.com/)toocreate 為您提供絕佳的方式和管理 Azure 邏輯應用程式，您可以使用 Visual Studio 設計、 建置和部署您的 logic apps。 Visual Studio 提供豐富的工具，像是 hello 邏輯應用程式的設計工具為您 toocreate 邏輯應用程式、 設定部署和自動化範本和部署 tooany 環境。 

Azure 邏輯應用程式，以啟動 tooget 深入了解[如何 toocreate hello Azure 入口網站中的第一個邏輯應用程式](logic-apps-create-a-logic-app.md)。

## <a name="installation-steps"></a>安裝步驟

tooinstall 和設定 Visual Studio tools for Azure 邏輯應用程式，請遵循下列步驟。

### <a name="prerequisites"></a>必要條件

* [Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) 或 Visual Studio 2015
* [最新的 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 或更新版本)
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* 使用 hello 內嵌設計工具時，存取 toohello web

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a>安裝適用於 Azure Logic Apps 的 Visual Studio 工具

之後您安裝 hello 必要條件：

1. 開啟 Visual Studio。 在 hello**工具**功能表上，選取**擴充功能和更新**。
2. 展開 hello**線上**類別讓您可以在線上搜尋。
3. 瀏覽或搜尋 [Logic Apps]，直到您找出 [Azure Logic Apps Tools for Visual Studio]。
4. toodownload 和安裝 hello 副檔名，請按一下**下載**。
5. 在安裝好之後重新啟動 Visual Studio。

> [!NOTE]
> 您也可以下載[Azure 邏輯應用程式 Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551)和 hello [Azure 邏輯應用程式 Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio)直接從 Visual Studio Marketplace hello。

完成安裝之後，您可以使用邏輯應用程式的設計工具來 hello Azure 資源群組專案。

## <a name="create-your-project"></a>建立專案

1. 在 hello**檔案**功能表上，移過**新增**，然後選取**專案**。 或 tooadd 太現有方案中，移至您的專案 tooan**新增**，然後選取**新專案**。

    ![[檔案] 功能表](./media/logic-apps-deploy-from-vs/filemenu.png)

2. 在 hello**新專案**視窗中，尋找**雲端**，並選取**Azure 資源群組**。 將您的專案命名，然後按一下 [確定]。

    ![加入新的專案](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. 選取 hello**邏輯應用程式**toouse 為您建立空白的邏輯應用程式的部署範本的範本。 選取您的範本後，按一下 [確定]。

    ![選取 [邏輯應用程式] 範本](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    您現在已加入邏輯應用程式專案 tooyour 方案。 
    在 [hello 方案總管] 中，您部署的檔案應該會出現。

    ![部署檔案](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a>利用邏輯應用程式設計工具建立邏輯應用程式

當您有 Azure 資源群組專案包含邏輯應用程式時，您可以 hello 邏輯應用程式的設計工具中開啟 Visual Studio toocreate 您的工作流程。 

> [!NOTE]
> hello 設計工具需要網際網路連線太查詢可用的屬性和資料的連接器。 例如，如果您使用 hello Dynamics CRM Online 連接器，hello 設計工具會查詢您的 CRM 執行個體 tooshow 可用自訂與預設屬性。

1. 以滑鼠右鍵按一下 `<template>.json` 檔案，然後選取 [使用邏輯應用程式設計工具來開啟]。 (`Ctrl+L`)

2. 選擇部署範本的 Azure 訂用帳戶、資源群組和位置。

    > [!NOTE]
    > 在設計邏輯應用程式時將會建立 API 連線資源，以在設計期間查詢屬性。 Visual Studio 在設計階段期間，這些連接將使用您選取的資源群組 toocreate。 tooview 或變更任何應用程式開發介面連接 toohello Azure 入口網站，請瀏覽**API 連線**。

    ![訂用帳戶選擇器](./media/logic-apps-deploy-from-vs/designer_picker.png)

    hello 設計工具會使用 hello 定義在 hello`<template>.json`轉譯的檔案。

4. 建立並設計邏輯應用程式。 會使用變更來更新部署範本。

    ![Visual Studio 中的邏輯應用程式設計工具](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

Visual Studio 會加入`Microsoft.Web/connections`資源過您的資源檔案的任何連線邏輯應用程式需要 toofunction。 這些連接屬性可以設定部署時，並在部署之後，管理**API 連線**hello Azure 入口網站中。

### <a name="switch-toojson-code-view"></a>切換 tooJSON 程式碼檢視

tooshow hello 邏輯應用程式，選取 hello 的 JSON 表示法**程式碼檢視**在 hello hello 設計工具底部的索引標籤。

tooswitch 回 toohello 完整資源 JSON，以滑鼠右鍵按一下 hello`<template>.json`檔案，然後選取**開啟**。

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a>加入相依的資源 tooVisual Studio 部署範本的參考

當您希望邏輯應用程式 tooreference 相依資源時，您可以使用[Azure Resource Manager 範本函式](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions)在邏輯應用程式部署範本中。 比方說，您可能會想您邏輯應用程式 tooreference 您想要讓 toodeploy，隨應用程式邏輯一起 Azure 功能或整合帳戶。 遵循這些指導方針，關於 toouse 參數，在您部署範本，因此，hello 邏輯應用程式的設計工具中正確轉譯的方式。 

您可以在這些類型的觸發程序和動作中使用邏輯應用程式參數︰

*   子工作流程
*   函式應用程式
*   APIM 呼叫
*   API 連線執行階段 URL
*   API 連線路徑

您可以使用範本函式，例如 parameters、variables、resourceId、concat 等等。例如，以下是如何取代 hello Azure 函式的資源識別碼：

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

以及您想使用參數的位置︰

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
另一個範例中，您可以參數化的 hello 服務匯流排傳送訊息作業：

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> host.runtimeUrl 是選擇性的，如果存在的話，可以從您的範本中移除。
> 


> [!NOTE] 
> Hello 邏輯應用程式的設計工具 toowork 時使用參數，您必須提供預設值，例如：
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a>儲存您的邏輯應用程式

toosave 在任何時候，應用程式邏輯移過**檔案** > **儲存**。 (`Ctrl+S`) 

如果應用程式邏輯會有任何錯誤，當您儲存您的應用程式時，它們會出現在 hello Visual Studio**輸出**視窗。

## <a name="deploy-your-logic-app-from-visual-studio"></a>從 Visual Studio 部署邏輯應用程式

設定應用程式之後，只要幾個步驟，就能從 Visual Studio 直接部署。 

1. 在方案總管 中，以滑鼠右鍵按一下您的專案，並跳過**部署** > **新部署...**

    ![新增部署](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. 當提示您時，請登入 tooyour Azure 訂用帳戶。 

3. 現在，您必須選取 hello hello 想 toodeploy 邏輯應用程式的資源群組的詳細資料。 完成後，選取 [部署]。

    > [!NOTE]
    > 請確定您選取 hello 正確的範本和參數檔案 hello 資源群組。 例如，如果您想 toodeploy tooa 生產環境中，選擇 hello 生產參數檔案。

    ![部署 tooresource 群組](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    hello 部署狀態會顯示在 hello**輸出**視窗。 
    您可能必須 tooselect **Azure 佈建**在 hello**顯示輸出來源**清單。

    ![部署狀態輸出](./media/logic-apps-deploy-from-vs/output.png)

在 hello 未來，您可以編輯原始檔控制中的應用程式邏輯，並使用 Visual Studio toodeploy 新版本。

> [!NOTE]
> 如果您直接變更 hello Azure 入口網站中的 hello 定義，當從 Visual Studio 部署下一次時，會覆寫這些變更。 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a>新增邏輯應用程式 tooan 現有資源群組專案

如果您有現有的資源群組專案時，您可以加入邏輯應用程式 toothat 專案 hello [JSON 大綱] 視窗中。 您也可以加入另一個邏輯應用程式，以及您先前建立的 hello 應用程式。

1. 開啟 hello`<template>.json`檔案。

2. tooopen hello JSON 大綱 視窗中，跳過**檢視** > **其他視窗** > **JSON 大綱**。

3. tooadd 資源 toohello 範本檔，按一下**加入資源**在 hello hello [JSON 大綱] 視窗的頂端。 或在 hello [JSON 大綱] 視窗，以滑鼠右鍵按一下**資源**，然後選取**加入新的資源**。

    ![[JSON 大綱] 視窗](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. 在 hello**加入資源**對話方塊中，尋找並選取**邏輯應用程式**。 為您的邏輯應用程式命名，然後選擇 [新增]。

    ![新增資源](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a>後續步驟

* [使用 Visual Studio Cloud Explorer 管理邏輯應用程式](logic-apps-manage-from-vs.md)
* [檢視常見的範例和案例](logic-apps-examples-and-scenarios.md)
* [了解如何 tooautomate 商務程序與 Azure 邏輯應用程式](http://channel9.msdn.com/Events/Build/2016/T694)
* [深入了解如何 toointegrate 系統與 Azure 邏輯應用程式](http://channel9.msdn.com/Events/Build/2016/P462)
