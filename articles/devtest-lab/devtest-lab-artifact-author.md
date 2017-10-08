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
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="267a1-103">為您的研發/測試實驗室 VM 建立自訂構件</span><span class="sxs-lookup"><span data-stu-id="267a1-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="267a1-104">概觀</span><span class="sxs-lookup"><span data-stu-id="267a1-104">Overview</span></span>
<span data-ttu-id="267a1-105">**成品**會使用的 toodeploy 和佈建 VM 之後，設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="267a1-105">**Artifacts** are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="267a1-106">構件包含構件定義檔和其他儲存於 Git 儲存機制之資料夾中的指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="267a1-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="267a1-107">成品定義檔案包含 JSON 和運算式，您可以使用 toospecify 您想要在 VM 上的 tooinstall。</span><span class="sxs-lookup"><span data-stu-id="267a1-107">Artifact definition files consist of JSON and expressions that you can use toospecify what you want tooinstall on a VM.</span></span> <span data-ttu-id="267a1-108">例如，您可以定義 hello 名稱成品、 命令 toorun 和 hello 命令執行時所使用的參數。</span><span class="sxs-lookup"><span data-stu-id="267a1-108">For example, you can define hello name of an artifact, command toorun, and parameters that are made available when hello command is run.</span></span> <span data-ttu-id="267a1-109">您可以依名稱參考 tooother 指令碼檔案中的 hello 成品定義檔案。</span><span class="sxs-lookup"><span data-stu-id="267a1-109">You can refer tooother script files within hello artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="267a1-110">構件定義檔格式</span><span class="sxs-lookup"><span data-stu-id="267a1-110">Artifact definition file format</span></span>
<span data-ttu-id="267a1-111">hello 下列範例顯示 hello 區段組成 hello 基本結構的定義檔：</span><span class="sxs-lookup"><span data-stu-id="267a1-111">hello following example shows hello sections that make up hello basic structure of a definition file:</span></span>

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

| <span data-ttu-id="267a1-112">元素名稱</span><span class="sxs-lookup"><span data-stu-id="267a1-112">Element name</span></span> | <span data-ttu-id="267a1-113">必要？</span><span class="sxs-lookup"><span data-stu-id="267a1-113">Required?</span></span> | <span data-ttu-id="267a1-114">說明</span><span class="sxs-lookup"><span data-stu-id="267a1-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="267a1-115">$schema</span><span class="sxs-lookup"><span data-stu-id="267a1-115">$schema</span></span> |<span data-ttu-id="267a1-116">否</span><span class="sxs-lookup"><span data-stu-id="267a1-116">No</span></span> |<span data-ttu-id="267a1-117">可協助在測試 hello 有效性 hello 定義檔中的 hello JSON 結構描述檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="267a1-117">Location of hello JSON schema file that helps in testing hello validity of hello definition file.</span></span> |
| <span data-ttu-id="267a1-118">title</span><span class="sxs-lookup"><span data-stu-id="267a1-118">title</span></span> |<span data-ttu-id="267a1-119">是</span><span class="sxs-lookup"><span data-stu-id="267a1-119">Yes</span></span> |<span data-ttu-id="267a1-120">顯示 hello 實驗室中的 hello 成品的名稱。</span><span class="sxs-lookup"><span data-stu-id="267a1-120">Name of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="267a1-121">說明</span><span class="sxs-lookup"><span data-stu-id="267a1-121">description</span></span> |<span data-ttu-id="267a1-122">是</span><span class="sxs-lookup"><span data-stu-id="267a1-122">Yes</span></span> |<span data-ttu-id="267a1-123">顯示 hello 實驗室中的 hello 成品的描述。</span><span class="sxs-lookup"><span data-stu-id="267a1-123">Description of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="267a1-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="267a1-124">iconUri</span></span> |<span data-ttu-id="267a1-125">否</span><span class="sxs-lookup"><span data-stu-id="267a1-125">No</span></span> |<span data-ttu-id="267a1-126">顯示 hello 實驗室中的 hello 圖示的 Uri。</span><span class="sxs-lookup"><span data-stu-id="267a1-126">Uri of hello icon displayed in hello lab.</span></span> |
| <span data-ttu-id="267a1-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="267a1-127">targetOsType</span></span> |<span data-ttu-id="267a1-128">是</span><span class="sxs-lookup"><span data-stu-id="267a1-128">Yes</span></span> |<span data-ttu-id="267a1-129">Hello VM 成品安裝所在的作業系統。</span><span class="sxs-lookup"><span data-stu-id="267a1-129">Operating system of hello VM where artifact is installed.</span></span> <span data-ttu-id="267a1-130">支援的選項為：Windows 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="267a1-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="267a1-131">參數</span><span class="sxs-lookup"><span data-stu-id="267a1-131">parameters</span></span> |<span data-ttu-id="267a1-132">否</span><span class="sxs-lookup"><span data-stu-id="267a1-132">No</span></span> |<span data-ttu-id="267a1-133">在電腦上執行構件安裝命令時所提供的值。</span><span class="sxs-lookup"><span data-stu-id="267a1-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="267a1-134">這有助於自訂您的構件。</span><span class="sxs-lookup"><span data-stu-id="267a1-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="267a1-135">runCommand</span><span class="sxs-lookup"><span data-stu-id="267a1-135">runCommand</span></span> |<span data-ttu-id="267a1-136">是</span><span class="sxs-lookup"><span data-stu-id="267a1-136">Yes</span></span> |<span data-ttu-id="267a1-137">在 VM 上執行的構件安裝命令。</span><span class="sxs-lookup"><span data-stu-id="267a1-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="267a1-138">構件參數</span><span class="sxs-lookup"><span data-stu-id="267a1-138">Artifact parameters</span></span>
<span data-ttu-id="267a1-139">在 hello 參數區段中的 hello 定義檔，您可以指定安裝成品時，使用者可以輸入哪些值。</span><span class="sxs-lookup"><span data-stu-id="267a1-139">In hello parameters section of hello definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="267a1-140">您可以參考 toothese hello 成品安裝命令中的值。</span><span class="sxs-lookup"><span data-stu-id="267a1-140">You can refer toothese values in hello artifact install command.</span></span>

<span data-ttu-id="267a1-141">您可以定義參數以 hello 下列結構：</span><span class="sxs-lookup"><span data-stu-id="267a1-141">You define parameters with hello following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="267a1-142">元素名稱</span><span class="sxs-lookup"><span data-stu-id="267a1-142">Element name</span></span> | <span data-ttu-id="267a1-143">必要？</span><span class="sxs-lookup"><span data-stu-id="267a1-143">Required?</span></span> | <span data-ttu-id="267a1-144">說明</span><span class="sxs-lookup"><span data-stu-id="267a1-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="267a1-145">類型</span><span class="sxs-lookup"><span data-stu-id="267a1-145">type</span></span> |<span data-ttu-id="267a1-146">是</span><span class="sxs-lookup"><span data-stu-id="267a1-146">Yes</span></span> |<span data-ttu-id="267a1-147">參數值類型。</span><span class="sxs-lookup"><span data-stu-id="267a1-147">Type of parameter value.</span></span> <span data-ttu-id="267a1-148">Hello 遵循 hello 允許類型清單，請參閱：</span><span class="sxs-lookup"><span data-stu-id="267a1-148">See hello following list for hello allowed types:</span></span> |
| <span data-ttu-id="267a1-149">displayName</span><span class="sxs-lookup"><span data-stu-id="267a1-149">displayName</span></span> |<span data-ttu-id="267a1-150">是</span><span class="sxs-lookup"><span data-stu-id="267a1-150">Yes</span></span> |<span data-ttu-id="267a1-151">Hello 參數顯示的 tooa hello 實驗室中的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="267a1-151">Name of hello parameter that is displayed tooa user in hello lab.</span></span> | |
| <span data-ttu-id="267a1-152">說明</span><span class="sxs-lookup"><span data-stu-id="267a1-152">description</span></span> |<span data-ttu-id="267a1-153">是</span><span class="sxs-lookup"><span data-stu-id="267a1-153">Yes</span></span> |<span data-ttu-id="267a1-154">顯示 hello 實驗室中的 hello 參數的描述。</span><span class="sxs-lookup"><span data-stu-id="267a1-154">Description of hello parameter that is displayed in hello lab.</span></span> |

<span data-ttu-id="267a1-155">hello 允許的類型為：</span><span class="sxs-lookup"><span data-stu-id="267a1-155">hello allowed types are:</span></span>

* <span data-ttu-id="267a1-156">string  - 任何有效的 JSON 字串</span><span class="sxs-lookup"><span data-stu-id="267a1-156">string – any valid JSON string</span></span>
* <span data-ttu-id="267a1-157">int - 任何有效的 JSON 整數</span><span class="sxs-lookup"><span data-stu-id="267a1-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="267a1-158">bool - 任何有效的 JSON 布林值</span><span class="sxs-lookup"><span data-stu-id="267a1-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="267a1-159">array - 任何有效的 JSON 陣列</span><span class="sxs-lookup"><span data-stu-id="267a1-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="267a1-160">構件運算式和函式</span><span class="sxs-lookup"><span data-stu-id="267a1-160">Artifact expressions and functions</span></span>
<span data-ttu-id="267a1-161">您可以使用運算式和函式 tooconstruct hello 成品安裝命令。</span><span class="sxs-lookup"><span data-stu-id="267a1-161">You can use expression and functions tooconstruct hello artifact install command.</span></span>
<span data-ttu-id="267a1-162">運算式會括在方括號 （[和]），且安裝 hello 成品時，會進行評估。</span><span class="sxs-lookup"><span data-stu-id="267a1-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when hello artifact is installed.</span></span> <span data-ttu-id="267a1-163">運算式可出現在 JSON 字串值中的任何一處，並一律傳回另一個 JSON 值。</span><span class="sxs-lookup"><span data-stu-id="267a1-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="267a1-164">如果您需要 toouse 常值字串開頭括號 [，您必須使用兩個方括號 [[。</span><span class="sxs-lookup"><span data-stu-id="267a1-164">If you need toouse a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="267a1-165">一般而言，您可以使用運算式具有函式 tooconstruct 值。</span><span class="sxs-lookup"><span data-stu-id="267a1-165">Typically, you use expressions with functions tooconstruct a value.</span></span> <span data-ttu-id="267a1-166">正如同在 JavaScript 中，函式呼叫的格式為 functionName(arg1,arg2,arg3)。</span><span class="sxs-lookup"><span data-stu-id="267a1-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="267a1-167">hello 下列清單顯示常見的函式：</span><span class="sxs-lookup"><span data-stu-id="267a1-167">hello following list shows common functions:</span></span>

* <span data-ttu-id="267a1-168">parameters(parameterName)-傳回 hello 成品命令執行時，會提供參數值。</span><span class="sxs-lookup"><span data-stu-id="267a1-168">parameters(parameterName) - Returns a parameter value that is provided when hello artifact command is run.</span></span>
* <span data-ttu-id="267a1-169">concat(arg1,arg2,arg3, …..) -     結合多個字串值。</span><span class="sxs-lookup"><span data-stu-id="267a1-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="267a1-170">此函數可以接受任意數目的引數。</span><span class="sxs-lookup"><span data-stu-id="267a1-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="267a1-171">下列範例會示範如何 hello toouse 運算式和函式 tooconstruct 值：</span><span class="sxs-lookup"><span data-stu-id="267a1-171">hello following example shows how toouse expression and functions tooconstruct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="267a1-172">建立自訂構件</span><span class="sxs-lookup"><span data-stu-id="267a1-172">Create a custom artifact</span></span>
<span data-ttu-id="267a1-173">遵循下列步驟來建立自訂的構件：</span><span class="sxs-lookup"><span data-stu-id="267a1-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="267a1-174">安裝 JSON 編輯器-您需要 JSON 編輯器 toowork 與成品定義檔。</span><span class="sxs-lookup"><span data-stu-id="267a1-174">Install a JSON editor - You need a JSON editor toowork with artifact definition files.</span></span> <span data-ttu-id="267a1-175">建議您使用 [Visual Studio 程式碼](https://code.visualstudio.com/)，這適用於 Windows、Linux 和 OS X。</span><span class="sxs-lookup"><span data-stu-id="267a1-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="267a1-176">取得 Azure DevTest Labs 團隊所建立的範例 artifactfile.json-簽出 hello 成品我們[GitHub 儲存機制](https://github.com/Azure/azure-devtestlab)，其中我們建立了豐富的程式庫成品，協助您建立您自己的成品。</span><span class="sxs-lookup"><span data-stu-id="267a1-176">Get a sample artifactfile.json - Check out hello artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="267a1-177">下載成品定義檔案，並進行變更 tooit toocreate 您自己的成品。</span><span class="sxs-lookup"><span data-stu-id="267a1-177">Download an artifact definition file and make changes tooit toocreate your own artifacts.</span></span>
3. <span data-ttu-id="267a1-178">請使用 IntelliSense-運用 IntelliSense toosee 的有效項目可以是使用的 tooconstruct 的成品定義檔。</span><span class="sxs-lookup"><span data-stu-id="267a1-178">Make use of IntelliSense - Leverage IntelliSense toosee valid elements that can be used tooconstruct an artifact definition file.</span></span> <span data-ttu-id="267a1-179">您也可以查看 hello 不同的選項值的項目。</span><span class="sxs-lookup"><span data-stu-id="267a1-179">You can also see hello different options for values of an element.</span></span> <span data-ttu-id="267a1-180">例如，編輯 hello 時，hello 的 Windows 或 Linux 的兩個選擇 IntelliSense 顯示**targetOsType**項目。</span><span class="sxs-lookup"><span data-stu-id="267a1-180">For example, IntelliSense show you hello two choices of Windows or Linux when editing hello **targetOsType** element.</span></span>
4. <span data-ttu-id="267a1-181">存放區中的 hello 成品[git 儲存機制](devtest-lab-add-artifact-repo.md)。</span><span class="sxs-lookup"><span data-stu-id="267a1-181">Store hello artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="267a1-182">建立其中 hello 目錄名稱是 hello 相同 hello 成品名稱當做每個成品個別的目錄。</span><span class="sxs-lookup"><span data-stu-id="267a1-182">Create a separate directory for each artifact where hello directory name is hello same as hello artifact name.</span></span>
   2. <span data-ttu-id="267a1-183">儲存在您建立 hello 目錄中的 hello 成品定義檔案 (artifactfile.json)。</span><span class="sxs-lookup"><span data-stu-id="267a1-183">Store hello artifact definition file (artifactfile.json) in hello directory you created.</span></span>
   3. <span data-ttu-id="267a1-184">被參考的 hello 成品存放區 hello 指令碼安裝命令。</span><span class="sxs-lookup"><span data-stu-id="267a1-184">Store hello scripts that are referenced from hello artifact install command.</span></span>
      
      <span data-ttu-id="267a1-185">構件資料夾的可能外觀範例如下：</span><span class="sxs-lookup"><span data-stu-id="267a1-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![構件 Git 儲存機制範例](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="267a1-187">新增 hello 成品儲存機制 toohello 實驗室-toohello 文章，請參閱[加入成品和範本的 Git 儲存機制](devtest-lab-add-artifact-repo.md)。</span><span class="sxs-lookup"><span data-stu-id="267a1-187">Add hello artifacts repository toohello lab - Refer toohello article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="267a1-188">相關文章</span><span class="sxs-lookup"><span data-stu-id="267a1-188">Related articles</span></span>
* [<span data-ttu-id="267a1-189">如何在 DevTest Labs toodiagnose 成品失敗</span><span class="sxs-lookup"><span data-stu-id="267a1-189">How toodiagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="267a1-190">加入 VM tooexisting Azure DevTest 實驗室中使用資源管理員範本的 AD 網域</span><span class="sxs-lookup"><span data-stu-id="267a1-190">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="267a1-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="267a1-191">Next steps</span></span>
* <span data-ttu-id="267a1-192">了解如何太[加入 Git 儲存機制成品 tooa 實驗室](devtest-lab-add-artifact-repo.md)。</span><span class="sxs-lookup"><span data-stu-id="267a1-192">Learn how too[add a Git artifact repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

