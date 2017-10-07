---
title: "aaaCreate Azure 邏輯應用程式的部署範本 |Microsoft 文件"
description: "建立 Azure Resource Manager 範本以進行邏輯應用程式部署和發行管理"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 85928ec6-d7cb-488e-926e-2e5db89508ee
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 2f09445f10a376a745d6acbba94ca29d5f79fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-templates-for-logic-apps-deployment-and-release-management"></a>建立範本以進行邏輯應用程式部署和發行管理

已建立邏輯應用程式之後，您可能會想 toocreate 它做為 Azure Resource Manager 範本。
如此一來，您可以輕鬆地部署 hello 邏輯應用程式 tooany 環境或，您可能需要的資源群組。
如需 Resource Manager 範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)和[使用 Azure Resource Manager 範本部署資源](../azure-resource-manager/resource-group-template-deploy.md)。

## <a name="logic-app-deployment-template"></a>邏輯應用程式部署範本

邏輯應用程式有三個基本元件：

* **邏輯應用程式資源**： 包含等定價計劃、 位置和 hello 工作流程定義的相關資訊。
* **工作流程定義**： 描述邏輯應用程式的工作流程的步驟和 hello Logic Apps 引擎應該如何執行 hello 工作流程。
您可以在邏輯應用程式的 [程式碼檢視] 視窗中檢視此定義。
在 hello 邏輯應用程式資源中，您可以在 hello 中找到此定義`definition`屬性。
* **連線**： 參考 tooseparate 資源的安全地儲存任何連接器連接，例如連接字串和存取權杖的相關中繼資料。
Hello 邏輯應用程式資源，在邏輯應用程式會參考這些資源在 hello `parameters` > 一節。

您可以使用 [Azure 資源總管](http://resources.azure.com)等工具，檢視現有邏輯應用程式的這些所有部分。

toomake 範本的應用程式 toouse 邏輯與資源群組部署中，您必須定義 hello 資源，並視需要將參數化。
例如，如果您要部署 tooa 開發、 測試和生產環境，您可能想 toouse 不同的連接字串 tooa SQL 資料庫中每個環境。
或者，您可能會想 toodeploy 不同訂用帳戶或資源群組內。  

## <a name="create-a-logic-app-deployment-template"></a>建立邏輯應用程式部署範本

最簡單方式 toohave hello 的有效邏輯應用程式部署範本是 toouse [Visual Studio Tools for Logic Apps](logic-apps-deploy-from-vs.md)。
hello Visual Studio 工具會產生可用於任何訂閱或位置的有效的部署範本。

有一些其他工具可在您建立邏輯應用程式部署範本時提供協助。
您可以手動撰寫，也就是使用 hello 資源已經討論 toocreate 參數視。
另一個選項是 toouse[邏輯應用程式範本建立者](https://github.com/jeffhollan/LogicAppTemplateCreator)PowerShell 模組。 此開放原始碼模組會先評估 hello 邏輯應用程式和任何連接它正在使用，並接著會產生與部署的 hello 必要參數的範本資源。
比方說，如果您有邏輯應用程式，從 Azure 服務匯流排佇列接收訊息，並加入資料 tooan Azure SQL database，hello 工具可以保留所有 hello 協調流程邏輯，會參數化 hello SQL 和服務匯流排連接字串，讓他們可以設定在部署。

> [!NOTE]
> 連線必須位在 hello 與 hello 邏輯應用程式的相同資源群組。
>
>

### <a name="install-hello-logic-app-template-powershell-module"></a>安裝 hello 邏輯應用程式範本 PowerShell 模組
hello 最簡單方式 tooinstall hello 模組是透過 hello [PowerShell 資源庫](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1)，利用 hello 命令`Install-Module -Name LogicAppTemplate`。  

您也可以安裝 hello PowerShell 模組以手動方式：

1. 下載 hello 最新版本的 hello[邏輯應用程式範本建立者](https://github.com/jeffhollan/LogicAppTemplateCreator/releases)。  
2. 擷取您的 PowerShell 模組資料夾中的 hello 資料夾 (通常`%UserProfile%\Documents\WindowsPowerShell\Modules`)。

Hello 模組 toowork 具有任何租用戶和訂用帳戶的存取權的語彙基元，我們建議您的 hello 使用[ARMClient](https://github.com/projectkudu/ARMClient)命令列工具。  這篇[部落格文章 (英文)](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html) 會更詳細地討論 ARMClient。

### <a name="generate-a-logic-app-template-by-using-powershell"></a>使用 PowerShell 產生邏輯應用程式範本
安裝 PowerShell 之後，您可以使用下列命令的 hello 產生範本：

`armclient token $SubscriptionId | Get-LogicAppTemplate -LogicApp MyApp -ResourceGroup MyRG -SubscriptionId $SubscriptionId -Verbose | Out-File C:\template.json`

`$SubscriptionId`這是 hello Azure 訂用帳戶識別碼。 這一行會先取得存取權杖透過 ARMClient，則管道透過 toohello PowerShell 指令碼，然後建立 JSON 檔案中的 hello 範本。

## <a name="add-parameters-tooa-logic-app-template"></a>加入參數 tooa 邏輯應用程式範本
您建立邏輯應用程式範本之後，您可以繼續 tooadd 或修改您可能需要的參數。 比方說，如果您定義包含的資源識別碼 tooan Azure 函式或您計劃在單一部署 toodeploy 巢狀工作流程，您可以新增更多資源 tooyour 範本，並視需要參數化識別碼。 hello 一樣 tooany 參考 toocustom 應用程式開發介面或 Swagger 端點您預期 toodeploy 與每個資源群組。

## <a name="deploy-a-logic-app-template"></a>部署邏輯應用程式範本

您可以使用 powershell、 REST API 的任何工具來部署您的範本[Visual Studio Team Services Release Management](#team-services)，並透過 hello Azure 入口網站的範本部署。
此外，toostore hello 參數的值，我們建議您建立[參數檔](../azure-resource-manager/resource-group-template-deploy.md#parameter-files)。
了解如何太[部署與 Azure 資源管理員範本和 PowerShell 資源](../azure-resource-manager/resource-group-template-deploy.md)或[部署 Azure 資源管理員範本的資源和 hello Azure 入口網站](../azure-resource-manager/resource-group-template-deploy-portal.md)。

### <a name="authorize-oauth-connections"></a>授權 OAuth 連接

部署之後，hello 邏輯應用程式運作順利端對端的有效參數。
不過，您仍然必須授權 OAuth 連線 toogenerate 有效存取權杖。
tooauthorize OAuth 連線，在 [hello 邏輯應用程式的設計工具] 中開啟 hello 邏輯應用程式，並授權這些連線。 或用於自動化部署，您可以使用指令碼 tooconsent tooeach OAuth 連線。
在 GitHub 上的 [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) 專案下方有一個範例指令碼。

<a name="team-services"></a>
## <a name="visual-studio-team-services-release-management"></a>Visual Studio Team Services Release Management

部署及管理環境的常見案例是 toouse 這類工具 Visual Studio Team Services 中的發行管理使用邏輯應用程式的部署範本。 Visual Studio Team Services 包含[部署 Azure 資源群組](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup)工作，您可以新增 tooany 建置或發行管線。 您需要 toohave[服務主體](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/)授權 toodeploy，然後您可以產生 hello 發行定義。

1. 在 Release Management 中，選取 [空白]，如此就能建立空白的定義。

    ![建立空白定義][1]

2. 選擇此，最有可能包括 hello 邏輯應用程式範本以手動方式或一部分 hello 產生所需的任何資源建置程序。
3. 新增 [Azure 資源群組部署]  工作。
4. 使用設定[服務主體](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/)，並參考 hello 範本和範本參數檔案。
5. 繼續 toobuild 步驟中的任何其他環境，自動化的測試或視需要的核准者 hello 發行程序。

<!-- Image References -->
[1]: ./media/logic-apps-create-deploy-template/emptyreleasedefinition.png
