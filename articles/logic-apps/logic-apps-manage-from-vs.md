---
title: "在 Visual Studio-Azure 邏輯應用程式中的 aaaManage logic apps |Microsoft 文件"
description: "使用 Visual Studio Cloud Explorer 管理邏輯應用程式和其他 Azure 資產"
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a>使用 Visual Studio Cloud Explorer 管理邏輯應用程式

雖然 hello [Azure 入口網站](https://portal.azure.com/)toodesign 為您提供絕佳的方式和管理 Azure 邏輯應用程式，您可以使用 Visual Studio Cloud Explorer 管理許多 Azure 資產，包括邏輯應用程式。 Visual Studio Cloud Explorer 可讓您瀏覽、管理、編輯和下載已發佈的 Logic Apps。 管理工作包括啟用、停用及檢視執行歷程記錄。 

您必須先安裝和設定適用於 Azure Logic Apps 的 Visual Studio 工具，才能在 Visual Studio 中存取及管理 Logic Apps。 

## <a name="prerequisites"></a>必要條件

* [Visual Studio 2015 或 Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* [最新的 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 或更新版本)
* [Visual Studio Cloud Explorer](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* 使用 hello 內嵌設計工具時，存取 toohello web

## <a name="install-visual-studio-tools-for-logic-apps"></a>安裝適用於 Logic Apps 的 Visual Studio 工具

安裝 hello 必要條件之後，請下載並安裝適用於 Visual Studio hello Azure 邏輯應用程式工具。

1. 開啟 Visual Studio。 在 hello**工具**功能表上，選取**擴充功能和更新**。
2. 展開 hello**線上**類別讓您可以搜尋線上 hello Visual Studio 組件庫中。
3. 瀏覽或搜尋 [Logic Apps]，直到您找出 [Azure Logic Apps Tools for Visual Studio]。
4. toodownload 和安裝 hello 副檔名，請按一下**下載**。
5. 在安裝好之後重新啟動 Visual Studio。

> [!NOTE]
> toodownload hello Azure 邏輯應用程式 Tools for Visual Studio 會直接移 toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9)。

## <a name="browse-for-logic-apps-in-cloud-explorer"></a>在 Cloud Explorer 中瀏覽邏輯應用程式

1.  在 hello tooopen Cloud Explorer**檢視**功能表上，選擇**Cloud Explorer**。
2.  依資源群組或資源類型瀏覽邏輯應用程式。 

    * 如果您瀏覽資源類型，選取您的 Azure 訂用帳戶中，展開 hello **Logic Apps**區段，然後選取 應用程式邏輯。 
    * 如果您瀏覽資源群組，展開具有應用程式邏輯，hello 資源群組，並選取邏輯應用程式。

    tooview 命令邏輯應用程式中，請以滑鼠右鍵按一下應用程式邏輯，或在 Cloud Explorer hello 下方，選擇從 hello**動作**功能表。

    ![瀏覽邏輯應用程式](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a>使用 Logic Apps 設計工具編輯邏輯應用程式

您可以從雲端總管 中，開啟目前部署的邏輯應用程式在 hello hello Azure 入口網站中使用相同的設計工具。 

* tooedit 邏輯應用程式，在 Cloud Explorer 中的以滑鼠右鍵按一下應用程式邏輯，並選取**使用邏輯應用程式編輯器開啟**。 

* toopublish 更新 toohello 雲端選擇**發行**。 

* toostart 新的執行中，選擇**執行觸發程序**。

![Logic Apps 設計工具](./media/logic-apps-manage-from-vs/designer.png)

Hello 設計工具中，您也可以**下載**邏輯應用程式。 此動作自動參數化 hello 邏輯應用程式定義，並將 hello 定義儲存為 Azure Resource Manager 部署範本。 您可以加入這個部署範本 tooyour Azure 資源群組專案。

## <a name="browse-your-logic-app-run-history"></a>瀏覽邏輯應用程式執行歷程記錄

tooview hello 執行歷程記錄的應用程式邏輯，以滑鼠右鍵按一下應用程式邏輯，並選取**開啟執行歷程記錄**。 tooreorder 程式執行歷程記錄，根據任何 hello 屬性顯示，請選取 hello 資料行標頭。

![執行記錄](media/logic-apps-manage-from-vs/runs.png)

tooshow hello 執行歷程記錄執行個體，因此您可以檢閱 hello 執行的結果，包括 hello 輸入和輸出來自每個步驟中，按兩下其中一個 hello 執行執行個體。

![步驟所產生的執行歷程記錄結果、輸入和輸出](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a>後續步驟

* [建立第一個邏輯應用程式](logic-apps-create-a-logic-app.md)
* [在 Visual Studio 中設計、建置和部署 Logic Apps](logic-apps-deploy-from-vs.md)
* [檢視常見的範例和案例](logic-apps-examples-and-scenarios.md)
* [影片：Automate business processes with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694) (使用 Azure Logic Apps 自動化商業程序)
* [影片：Integrate your systems with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462) (整合您的系統與 Azure Logic Apps)
