---
title: "DevTest 實驗室 vm aaaCreate 自訂成品 |Microsoft 文件"
description: "了解如何 tooauthor 您自己的成品以利使用的 DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 2bd603bc1241ca6b669a3a276a677729514f0df2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a>為您的研發/測試實驗室 VM 建立自訂構件
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a>概觀
**成品**會使用的 toodeploy 和佈建 VM 之後，設定您的應用程式。 構件包含構件定義檔和其他儲存於 Git 儲存機制之資料夾中的指令碼檔案。 成品定義檔案包含 JSON 和運算式，您可以使用 toospecify 您想要在 VM 上的 tooinstall。 例如，您可以定義 hello 名稱成品、 命令 toorun 和 hello 命令執行時所使用的參數。 您可以依名稱參考 tooother 指令碼檔案中的 hello 成品定義檔案。

## <a name="artifact-definition-file-format"></a>構件定義檔格式
hello 下列範例顯示 hello 區段組成 hello 基本結構的定義檔：

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2016-11-28/dtlArtifacts.json",
      "title": "",
      "description": "",
      "iconUri": "",
      "targetOsType": "",
      "parameters": {
        "<parameterName>": {
          "type": "",
          "displayName": "",
          "description": ""
        }
      },
      "runCommand": {
        "commandToExecute": ""
      }
    }

| 元素名稱 | 必要？ | 說明 |
| --- | --- | --- |
| $schema |否 |可協助在測試 hello 有效性 hello 定義檔中的 hello JSON 結構描述檔案的位置。 |
| title |是 |顯示 hello 實驗室中的 hello 成品的名稱。 |
| 說明 |是 |顯示 hello 實驗室中的 hello 成品的描述。 |
| iconUri |否 |顯示 hello 實驗室中的 hello 圖示的 Uri。 |
| targetOsType |是 |Hello VM 成品安裝所在的作業系統。 支援的選項為：Windows 和 Linux。 |
| 參數 |否 |在電腦上執行構件安裝命令時所提供的值。 這有助於自訂您的構件。 |
| runCommand |是 |在 VM 上執行的構件安裝命令。 |

### <a name="artifact-parameters"></a>構件參數
在 hello 參數區段中的 hello 定義檔，您可以指定安裝成品時，使用者可以輸入哪些值。 您可以參考 toothese hello 成品安裝命令中的值。

您可以定義參數以 hello 下列結構：

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| 元素名稱 | 必要？ | 說明 |
| --- | --- | --- |
| 類型 |是 |參數值類型。 Hello 遵循 hello 允許類型清單，請參閱： |
| displayName |是 |Hello 參數顯示的 tooa hello 實驗室中的使用者名稱。 | |
| 說明 |是 |顯示 hello 實驗室中的 hello 參數的描述。 |

hello 允許的類型為：

* string  - 任何有效的 JSON 字串
* int - 任何有效的 JSON 整數
* bool - 任何有效的 JSON 布林值
* array - 任何有效的 JSON 陣列

## <a name="artifact-expressions-and-functions"></a>構件運算式和函式
您可以使用運算式和函式 tooconstruct hello 成品安裝命令。
運算式會括在方括號 （[和]），且安裝 hello 成品時，會進行評估。 運算式可出現在 JSON 字串值中的任何一處，並一律傳回另一個 JSON 值。 如果您需要 toouse 常值字串開頭括號 [，您必須使用兩個方括號 [[。
一般而言，您可以使用運算式具有函式 tooconstruct 值。 正如同在 JavaScript 中，函式呼叫的格式為 functionName(arg1,arg2,arg3)。

hello 下列清單顯示常見的函式：

* parameters(parameterName)-傳回 hello 成品命令執行時，會提供參數值。
* concat(arg1,arg2,arg3, …..) -     結合多個字串值。 此函數可以接受任意數目的引數。

下列範例會示範如何 hello toouse 運算式和函式 tooconstruct 值：

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a>建立自訂構件
遵循下列步驟來建立自訂的構件：

1. 安裝 JSON 編輯器-您需要 JSON 編輯器 toowork 與成品定義檔。 建議您使用 [Visual Studio 程式碼](https://code.visualstudio.com/)，這適用於 Windows、Linux 和 OS X。
2. 取得 Azure DevTest Labs 團隊所建立的範例 artifactfile.json-簽出 hello 成品我們[GitHub 儲存機制](https://github.com/Azure/azure-devtestlab)，其中我們建立了豐富的程式庫成品，協助您建立您自己的成品。 下載成品定義檔案，並進行變更 tooit toocreate 您自己的成品。
3. 請使用 IntelliSense-運用 IntelliSense toosee 的有效項目可以是使用的 tooconstruct 的成品定義檔。 您也可以查看 hello 不同的選項值的項目。 例如，編輯 hello 時，hello 的 Windows 或 Linux 的兩個選擇 IntelliSense 顯示**targetOsType**項目。
4. 存放區中的 hello 成品[git 儲存機制](devtest-lab-add-artifact-repo.md)。
   
   1. 建立其中 hello 目錄名稱是 hello 相同 hello 成品名稱當做每個成品個別的目錄。
   2. 儲存在您建立 hello 目錄中的 hello 成品定義檔案 (artifactfile.json)。
   3. 被參考的 hello 成品存放區 hello 指令碼安裝命令。
      
      構件資料夾的可能外觀範例如下：
      
      ![構件 Git 儲存機制範例](./media/devtest-lab-artifact-author/git-repo.png)
5. 新增 hello 成品儲存機制 toohello 實驗室-toohello 文章，請參閱[加入成品和範本的 Git 儲存機制](devtest-lab-add-artifact-repo.md)。

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a>相關文章
* [如何在 DevTest Labs toodiagnose 成品失敗](devtest-lab-troubleshoot-artifact-failure.md)
* [加入 VM tooexisting Azure DevTest 實驗室中使用資源管理員範本的 AD 網域](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>後續步驟
* 了解如何太[加入 Git 儲存機制成品 tooa 實驗室](devtest-lab-add-artifact-repo.md)。

