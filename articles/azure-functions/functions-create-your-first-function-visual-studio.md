---
title: "使用 Visual Studio 在 Azure 中的第一個函式的 aaaCreate |Microsoft 文件"
description: "建立及使用 Azure 函式 Tools for Visual Studio 發行簡單的 HTTP 觸發函式 tooAzure。"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函式, 事件處理, 計算, 無伺服器架構"
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 07/05/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 851e5b98dcc2da00334620896a0ea31f566589f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-visual-studio"></a>使用 Visual Studio 建立第一個函式

Azure 的函式可讓您在無伺服器環境中執行您的程式碼，而不需要 toofirst 建立 VM，或發行 web 應用程式。

在本主題中，您將學會如何 toouse hello Azure 函式 toocreate 的 Visual Studio 2017 工具及測試在本機上的"hello world"函式。 然後，您將發行 hello 函式程式碼 tooAzure。 這些工具可在 Visual Studio 2017 版本 15.3，hello Azure 的開發工作負載的部分或更新版本。

![Visual Studio 專案中的 Azure Functions 程式碼](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a>必要條件

toocomplete 此教學課程，安裝：

* [Visual Studio 2017 版本 15.3](https://www.visualstudio.com/vs/preview/)，包括 hello **Azure 開發**工作負載。

    ![安裝 Visual Studio 2017 hello Azure 開發的工作負載](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    您安裝或升級 tooVisual Studio 2017 15.3 版本之後，您可能也需要 toomanually update hello Visual Studio 2017 工具 Azure 函式。 您可以更新從 hello hello 工具**工具**下的單**擴充功能和更新...**  > **更新** > **Visual Studio Marketplace** > **Azure 函式和 Web 工作工具** > **更新**。 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a>在 Visual Studio 中建立 Azure Functions 專案

[!INCLUDE [Create a project using hello Azure Functions template](../../includes/functions-vstools-create.md)]

既然您已經建立 hello 專案，您可以建立您的第一個函式。

## <a name="create-hello-function"></a>建立 hello 函式

1. 在 [方案總管] 中，於專案節點上按一下滑鼠右鍵，然後選取 [新增] > [新增項目]。 選取 [Azure Function]，然後按一下 [新增]。

2. 選取 [HttpTrigger]，輸入 [函式名稱]，針對 [存取權限] 選取 [匿名]，然後按一下 [建立]。 從任何用戶端的 HTTP 要求來存取建立 hello 函式。 

    ![建立新的 Azure Function](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    程式碼檔案會加入 tooyour 專案，其中包含實作您的函式程式碼的類別。 此程式碼是以範本為基礎，會接收名稱值並將其回應回去。 hello **FunctionName**屬性設定函式的 hello 名稱。 hello **HttpTrigger**屬性會指出觸發 hello 函式的 hello 訊息。 

    ![函式程式碼檔案](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

您現在已建立 HTTP 觸發的函式，可以在本機電腦上進行測試。

## <a name="test-hello-function-locally"></a>在本機測試 hello 函式

Azure Functions Core Tools 可讓您在本機開發電腦上執行 Azure Functions 專案。 您必須提示的 tooinstall 這些工具 hello 從 Visual Studio 啟動函式的第一次。  

1. tootest 您的函式，請按 F5。 如果出現提示，請接受從 Visual Studio toodownload hello 要求，並安裝 Azure 函式核心 (CLI) 工具。  您也可能需要 tooenable 防火牆例外，好讓 hello 工具可以處理 HTTP 要求。

2. 複製 hello URL 從 hello Azure 函式執行階段函式的輸出。  

    ![Azure 本機執行階段](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. 貼入您的瀏覽器位址列中的 hello hello HTTP 要求的 URL。 附加 hello 查詢字串`&name=<yourname>`toothis URL，然後執行 hello 要求。 hello 下列顯示 hello 回應 hello 瀏覽器 toohello 本機 GET 要求傳回的 hello 函式： 

    ![函式 localhost 回應 hello 瀏覽器中](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. 按一下 偵錯，toostop hello**停止**hello Visual Studio 工具列上的按鈕。

確認 hello 函式會在本機電腦上正確地執行之後，它是時間 toopublish hello 專案 tooAzure。

## <a name="publish-hello-project-tooazure"></a>發行 hello 專案 tooAzure

您的 Azure 訂用帳戶中必須具有函式應用程式，才可以發佈您的專案。 您可以直接從 Visual Studio 建立函式應用程式。

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a>在 Azure 中測試您的函式

1. 複製 hello 發行設定檔 頁面中的 hello 的 hello 函式應用程式的基底 URL。 取代 hello `localhost:port` hello URL 測試與 hello 新的基底 URL 在本機的 hello 函式時所使用的部分。 如往常一般，請確定 tooappend hello 查詢字串`&name=<yourname>`toothis URL，然後執行 hello 要求。

    呼叫您的 HTTP hello URL 觸發函式看起來像這樣：

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. 貼入您的瀏覽器位址列中的 hello HTTP 要求的這個新的 URL。 hello 下列顯示 hello 回應 hello 瀏覽器 toohello 遠端 GET 要求傳回的 hello 函式： 

    ![Hello 瀏覽器中回應時間函式](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a>後續步驟

您使用 Visual Studio toocreate C# 函式應用程式使用的簡單 HTTP 觸發函式。 

+ toolearn 如何 tooconfigure 專案 toosupport 其他類型的觸發程序，以及繫結，請參閱 hello[設定 hello 專案以進行本機開發](functions-develop-vs.md#configure-the-project-for-local-development)一節中[Azure 函式 Tools for Visual Studio](functions-develop-vs.md)。
+ toolearn 深入了解本機測試和偵錯使用 hello Azure 函式的核心工具，請參閱[程式碼和在本機測試 Azure 函式](functions-run-local.md)。 
+ toolearn 進一步了解開發函式做為.NET 類別庫，請參閱[使用.NET 類別庫來搭配 Azure 函式](functions-dotnet-class-library.md)。 

