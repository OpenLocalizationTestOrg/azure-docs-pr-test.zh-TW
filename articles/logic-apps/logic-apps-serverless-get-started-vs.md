---
title: "aaaBuild Visual Studio 中的無伺服器應用程式 |Microsoft 文件"
description: "開始使用您建立、 部署和管理 Visual Studio 中的 hello 應用程式在本指南的第一個無伺服器應用程式。"
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 74530eea6060ffe2139f7c9d6daab8a46f808162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-serverless-app-in-visual-studio-with-logic-apps-and-functions"></a>在 Visual Studio 中使用 Logic Apps 和 Functions 建置邏輯應用程式

Azure 中的無伺服器工具和功能可讓您快速開發和部署雲端應用程式。  本文件著重於如何 tooget 建立無伺服器的應用程式的 Visual Studio 中啟動。  如需 Azure 中的無伺服器概觀，請參閱[這篇文章](logic-apps-serverless-overview.md)。

## <a name="getting-everything-ready"></a>備妥一切

以下是 hello 所需必要條件 toobuild 無伺服器的應用程式，從 Visual Studio:

* [Visual Studio 2017](https://www.visualstudio.com/vs/) 或 Visual Studio 2015 - Community、Professional 或 Enterprise
* [Logic Apps Tools for Visual Studio](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551)
* [最新的 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 或更新版本)
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* [Azure 功能的核心工具](https://www.npmjs.com/package/azure-functions-core-tools)toodebug 本機函式
* 當使用 hello 內嵌邏輯應用程式的設計工具時，存取 toohello web

## <a name="getting-started-with-a-deployment-template"></a>開始使用部署範本

Azure 中是在資源群組內管理資源。  資源群組是資源的邏輯群組。  資源群組可用來部署和管理資源集合。  對於 Azure 中的無伺服器應用程式，我們的資源群組包含 Azure Logic Apps 和 Azure Functions。  藉由使用 Visual Studio 中的 hello 資源群組專案，我們目前無法 toodevelop、 管理及部署 hello 整個應用程式做為單一的資產。

### <a name="create-a-resource-group-project-in-visual-studio"></a>在 Visual Studio 中建立資源群組

1. 在 Visual Studio 中，按一下 tooadd**新專案**
1. 在 hello**雲端**分類中，選取 toocreate Azure**資源群組**專案  
 * 如果您看不 hello 類別或專案列出，請確定您擁有 hello Azure SDK for Visual Studio 安裝
1. 為 hello 專案的名稱和位置，然後選取**確定**toocreate Visual Studio 會提示 tooselect 範本。  您可以選擇 toostart 空白、 邏輯應用程式的開頭或其他資源。  不過，在此情況下我們使用我們的無伺服器的應用程式以啟動 Azure 快速入門範本 tooget。
1. 選取從 tooshow 範本**Azure 快速入門**![選取 Azure 快速入門範本][1]
1. 選取 hello 無伺服器快速入門範本： **101-logic-app-and-function-app**按一下**[確定]**

hello 快速入門範本建立資源群組專案中的部署範本。  hello 範本包含簡單的邏輯應用程式呼叫 Azure 函式，並傳回 hello 結果。  如果您開啟 hello`azuredeploy.json`檔案中的 hello 方案總管 中，您會看到 hello hello 無伺服器應用程式的資源。

## <a name="deploying-hello-serverless-application"></a>部署的 hello 無伺服器應用程式

您可以開啟 Visual Studio 中的 hello 邏輯應用程式的視覺化設計工具之前，需要 toobe 預先部署的 Azure 資源群組。  這可讓 hello 設計工具 toocreate 及使用連線 tooresources 服務 hello 邏輯應用程式中。  啟動 tooget，我們只需要建立 toodeploy hello 方案。

1. 以滑鼠右鍵按一下 hello 專案在 Visual Studio 中，選取**部署**，並建立**新增**部署![選取新的資源部署][2]
1. 選取有效的 Azure 訂用帳戶和資源群組
1. 選取太**部署**hello 方案
1. 輸入 hello hello 邏輯應用程式的名稱和 hello Azure 函式應用程式中。  hello Azure 函式需要名稱 toobe 全域唯一

hello 無伺服器方案部署到 hello 指定的資源群組。  如果您看一下 hello**輸出**在 Visual Studio 中，您可以看到 hello 部署的 hello 狀態。

## <a name="editing-hello-logic-app-in-visual-studio"></a>編輯 Visual Studio 中的 hello 邏輯應用程式

一旦 hello 方案已經部署到任何資源群組，可以是使用的 tooedit hello 視覺化設計工具，而且讓變更 toohello 邏輯應用程式。

1. 以滑鼠右鍵按一下 hello `azuredeploy.json` hello 方案總管 中的檔案，然後選取**開啟使用邏輯應用程式設計師**
1. 選取 hello**資源群組**和**位置**hello 解決方案已部署 tooand 選取**[確定]**

hello 邏輯應用程式的視覺化設計工具現在應該可以看到與 Visual Studio。  您可以繼續 tooadd 步驟中，修改 hello 工作流程，並儲存變更。  您也可以從 Visual Studio 建立邏輯應用程式。  如果您以滑鼠右鍵按一下 hello**資源**hello 範本在導覽中，您可以選擇 tooadd**邏輯應用程式**toohello 專案。  Hello 沒有視覺化設計工具中載入的空白 logic apps 預先部署至資源群組。

### <a name="managing-and-viewing-run-history-for-a-deployed-logic-app"></a>管理和檢視已部署之邏輯應用程式的執行歷程記錄

您也可以管理，並檢視部署在 Azure 中的 logic apps hello 執行歷程記錄。  如果您開啟 hello **Cloud Explorer**工具或在 Visual Studio 中，您可以以滑鼠右鍵按一下任何邏輯應用程式，並選擇 tooedit，停用，檢視內容中，檢視執行歷程記錄。  按一下 編輯也可讓您 toodownload 已發行的邏輯應用程式到 Visual Studio 資源群組專案。  這表示，即使您開始建置 hello Azure 入口網站中的應用程式邏輯，您仍可以將它匯入及管理從 Visual Studio。

## <a name="developing-an-azure-function-in-visual-studio"></a>在 Visual Studio 中開發 Azure 函式

hello 部署範本部署 hello hello 中指定的 git 儲存機制的 hello 方案中所包含的任何 Azure 函式`azuredeploy.json`變數。  如果您撰寫函式中的專案 hello 方案時，將它簽入原始檔控制 （GitHub、 Visual Studio Team Services 等），並更新 hello`repo`變數 hello 範本將會部署 hello Azure 函式。

### <a name="creating-an-azure-function-project"></a>建立 Azure 函式專案

如果使用 JavaScript、 Python、 F #、 Bash、 批次或 PowerShell，請遵循 hello [hello CLI 函式中的步驟](../azure-functions/functions-run-local.md)toocreate 專案。  如果開發的函式，在 C# 中，您可以使用[C# 類別庫](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/)hello Azure 函式的 hello 目前方案中。

## <a name="next-steps"></a>後續步驟

* [深入了解如何 toobuild 無伺服器的社交儀表板](logic-apps-scenario-social-serverless.md)
* [從 Visual Studio Cloud Explorer 管理邏輯應用程式](logic-apps-manage-from-vs.md)
* [邏輯應用程式工作流程定義語言](logic-apps-workflow-definition-language.md)

<!-- Image references -->
[1]: ./media/logic-apps-serverless-get-started-vs/select-template.png
[2]: ./media/logic-apps-serverless-get-started-vs/deploy.png
