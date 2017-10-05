---
title: "為您的 DevTest Labs VM 建立自訂構件 | Microsoft Docs"
description: "了解如何撰寫自己的構件以用於研發/測試實驗室"
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
ms.openlocfilehash: 2412033daa1d97860dd9f380178622b1ddc590c0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="725e7-103">為您的研發/測試實驗室 VM 建立自訂構件</span><span class="sxs-lookup"><span data-stu-id="725e7-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="725e7-104">概觀</span><span class="sxs-lookup"><span data-stu-id="725e7-104">Overview</span></span>
<span data-ttu-id="725e7-105">**構件** 是在佈建 VM 之後用來部署和設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="725e7-105">**Artifacts** are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="725e7-106">構件包含構件定義檔和其他儲存於 Git 儲存機制之資料夾中的指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="725e7-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="725e7-107">構件定義檔是由 JSON 和可用來指定您想要在 VM 上安裝的運算式所組成。</span><span class="sxs-lookup"><span data-stu-id="725e7-107">Artifact definition files consist of JSON and expressions that you can use to specify what you want to install on a VM.</span></span> <span data-ttu-id="725e7-108">例如，您可以定義構件名稱、要執行的命令，以及命令執行時使其可供使用的參數。</span><span class="sxs-lookup"><span data-stu-id="725e7-108">For example, you can define the name of an artifact, command to run, and parameters that are made available when the command is run.</span></span> <span data-ttu-id="725e7-109">您可以依照名稱來參考構件定義檔中的其他指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="725e7-109">You can refer to other script files within the artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="725e7-110">構件定義檔格式</span><span class="sxs-lookup"><span data-stu-id="725e7-110">Artifact definition file format</span></span>
<span data-ttu-id="725e7-111">下列範例顯示組成定義檔基本結構的區段：</span><span class="sxs-lookup"><span data-stu-id="725e7-111">The following example shows the sections that make up the basic structure of a definition file:</span></span>

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

| <span data-ttu-id="725e7-112">元素名稱</span><span class="sxs-lookup"><span data-stu-id="725e7-112">Element name</span></span> | <span data-ttu-id="725e7-113">必要？</span><span class="sxs-lookup"><span data-stu-id="725e7-113">Required?</span></span> | <span data-ttu-id="725e7-114">說明</span><span class="sxs-lookup"><span data-stu-id="725e7-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="725e7-115">$schema</span><span class="sxs-lookup"><span data-stu-id="725e7-115">$schema</span></span> |<span data-ttu-id="725e7-116">否</span><span class="sxs-lookup"><span data-stu-id="725e7-116">No</span></span> |<span data-ttu-id="725e7-117">JSON 結構描述檔案的位置，此檔案可協助測試定義檔的有效性。</span><span class="sxs-lookup"><span data-stu-id="725e7-117">Location of the JSON schema file that helps in testing the validity of the definition file.</span></span> |
| <span data-ttu-id="725e7-118">title</span><span class="sxs-lookup"><span data-stu-id="725e7-118">title</span></span> |<span data-ttu-id="725e7-119">是</span><span class="sxs-lookup"><span data-stu-id="725e7-119">Yes</span></span> |<span data-ttu-id="725e7-120">實驗室中顯示的構件名稱。</span><span class="sxs-lookup"><span data-stu-id="725e7-120">Name of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="725e7-121">說明</span><span class="sxs-lookup"><span data-stu-id="725e7-121">description</span></span> |<span data-ttu-id="725e7-122">是</span><span class="sxs-lookup"><span data-stu-id="725e7-122">Yes</span></span> |<span data-ttu-id="725e7-123">實驗室中顯示的構件說明。</span><span class="sxs-lookup"><span data-stu-id="725e7-123">Description of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="725e7-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="725e7-124">iconUri</span></span> |<span data-ttu-id="725e7-125">否</span><span class="sxs-lookup"><span data-stu-id="725e7-125">No</span></span> |<span data-ttu-id="725e7-126">實驗室中顯示的圖示 URI。</span><span class="sxs-lookup"><span data-stu-id="725e7-126">Uri of the icon displayed in the lab.</span></span> |
| <span data-ttu-id="725e7-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="725e7-127">targetOsType</span></span> |<span data-ttu-id="725e7-128">是</span><span class="sxs-lookup"><span data-stu-id="725e7-128">Yes</span></span> |<span data-ttu-id="725e7-129">構件安裝所在之 VM 的作業系統。</span><span class="sxs-lookup"><span data-stu-id="725e7-129">Operating system of the VM where artifact is installed.</span></span> <span data-ttu-id="725e7-130">支援的選項為：Windows 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="725e7-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="725e7-131">參數</span><span class="sxs-lookup"><span data-stu-id="725e7-131">parameters</span></span> |<span data-ttu-id="725e7-132">否</span><span class="sxs-lookup"><span data-stu-id="725e7-132">No</span></span> |<span data-ttu-id="725e7-133">在電腦上執行構件安裝命令時所提供的值。</span><span class="sxs-lookup"><span data-stu-id="725e7-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="725e7-134">這有助於自訂您的構件。</span><span class="sxs-lookup"><span data-stu-id="725e7-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="725e7-135">runCommand</span><span class="sxs-lookup"><span data-stu-id="725e7-135">runCommand</span></span> |<span data-ttu-id="725e7-136">是</span><span class="sxs-lookup"><span data-stu-id="725e7-136">Yes</span></span> |<span data-ttu-id="725e7-137">在 VM 上執行的構件安裝命令。</span><span class="sxs-lookup"><span data-stu-id="725e7-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="725e7-138">構件參數</span><span class="sxs-lookup"><span data-stu-id="725e7-138">Artifact parameters</span></span>
<span data-ttu-id="725e7-139">在定義檔的參數區段中，您會指定使用者可在安裝構件時輸入的值。</span><span class="sxs-lookup"><span data-stu-id="725e7-139">In the parameters section of the definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="725e7-140">您可以在構件安裝命令中參考這些值。</span><span class="sxs-lookup"><span data-stu-id="725e7-140">You can refer to these values in the artifact install command.</span></span>

<span data-ttu-id="725e7-141">您會定義結構如下的參數：</span><span class="sxs-lookup"><span data-stu-id="725e7-141">You define parameters with the following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="725e7-142">元素名稱</span><span class="sxs-lookup"><span data-stu-id="725e7-142">Element name</span></span> | <span data-ttu-id="725e7-143">必要？</span><span class="sxs-lookup"><span data-stu-id="725e7-143">Required?</span></span> | <span data-ttu-id="725e7-144">說明</span><span class="sxs-lookup"><span data-stu-id="725e7-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="725e7-145">類型</span><span class="sxs-lookup"><span data-stu-id="725e7-145">type</span></span> |<span data-ttu-id="725e7-146">是</span><span class="sxs-lookup"><span data-stu-id="725e7-146">Yes</span></span> |<span data-ttu-id="725e7-147">參數值類型。</span><span class="sxs-lookup"><span data-stu-id="725e7-147">Type of parameter value.</span></span> <span data-ttu-id="725e7-148">請參閱下列清單以了解允許的類型：</span><span class="sxs-lookup"><span data-stu-id="725e7-148">See the following list for the allowed types:</span></span> |
| <span data-ttu-id="725e7-149">displayName</span><span class="sxs-lookup"><span data-stu-id="725e7-149">displayName</span></span> |<span data-ttu-id="725e7-150">是</span><span class="sxs-lookup"><span data-stu-id="725e7-150">Yes</span></span> |<span data-ttu-id="725e7-151">為實驗室中的使用者顯示的參數名稱。</span><span class="sxs-lookup"><span data-stu-id="725e7-151">Name of the parameter that is displayed to a user in the lab.</span></span> | |
| <span data-ttu-id="725e7-152">說明</span><span class="sxs-lookup"><span data-stu-id="725e7-152">description</span></span> |<span data-ttu-id="725e7-153">是</span><span class="sxs-lookup"><span data-stu-id="725e7-153">Yes</span></span> |<span data-ttu-id="725e7-154">在實驗室中顯示的參數說明。</span><span class="sxs-lookup"><span data-stu-id="725e7-154">Description of the parameter that is displayed in the lab.</span></span> |

<span data-ttu-id="725e7-155">允許的類型為：</span><span class="sxs-lookup"><span data-stu-id="725e7-155">The allowed types are:</span></span>

* <span data-ttu-id="725e7-156">string  - 任何有效的 JSON 字串</span><span class="sxs-lookup"><span data-stu-id="725e7-156">string – any valid JSON string</span></span>
* <span data-ttu-id="725e7-157">int - 任何有效的 JSON 整數</span><span class="sxs-lookup"><span data-stu-id="725e7-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="725e7-158">bool - 任何有效的 JSON 布林值</span><span class="sxs-lookup"><span data-stu-id="725e7-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="725e7-159">array - 任何有效的 JSON 陣列</span><span class="sxs-lookup"><span data-stu-id="725e7-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="725e7-160">構件運算式和函式</span><span class="sxs-lookup"><span data-stu-id="725e7-160">Artifact expressions and functions</span></span>
<span data-ttu-id="725e7-161">您可以使用運算式和函式來建構構件安裝命令。</span><span class="sxs-lookup"><span data-stu-id="725e7-161">You can use expression and functions to construct the artifact install command.</span></span>
<span data-ttu-id="725e7-162">運算式是以方括號 ([ 與 ]) 括住，並會在安裝構件後加以評估。</span><span class="sxs-lookup"><span data-stu-id="725e7-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when the artifact is installed.</span></span> <span data-ttu-id="725e7-163">運算式可出現在 JSON 字串值中的任何一處，並一律傳回另一個 JSON 值。</span><span class="sxs-lookup"><span data-stu-id="725e7-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="725e7-164">如果您必須使用開頭為括號 [ 的常數字串，您必須使用兩個括號 [[。</span><span class="sxs-lookup"><span data-stu-id="725e7-164">If you need to use a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="725e7-165">通常您會使用運算式搭配函式來建構值。</span><span class="sxs-lookup"><span data-stu-id="725e7-165">Typically, you use expressions with functions to construct a value.</span></span> <span data-ttu-id="725e7-166">正如同在 JavaScript 中，函式呼叫的格式為 functionName(arg1,arg2,arg3)。</span><span class="sxs-lookup"><span data-stu-id="725e7-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="725e7-167">下列清單顯示常見的函式：</span><span class="sxs-lookup"><span data-stu-id="725e7-167">The following list shows common functions:</span></span>

* <span data-ttu-id="725e7-168">parameters(parameterName) - 傳回在執行構件命令時所提供的參數值。</span><span class="sxs-lookup"><span data-stu-id="725e7-168">parameters(parameterName) - Returns a parameter value that is provided when the artifact command is run.</span></span>
* <span data-ttu-id="725e7-169">concat(arg1,arg2,arg3, …..) -     結合多個字串值。</span><span class="sxs-lookup"><span data-stu-id="725e7-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="725e7-170">此函數可以接受任意數目的引數。</span><span class="sxs-lookup"><span data-stu-id="725e7-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="725e7-171">下列範例示範如何使用運算式和函式來建構值：</span><span class="sxs-lookup"><span data-stu-id="725e7-171">The following example shows how to use expression and functions to construct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="725e7-172">建立自訂構件</span><span class="sxs-lookup"><span data-stu-id="725e7-172">Create a custom artifact</span></span>
<span data-ttu-id="725e7-173">遵循下列步驟來建立自訂的構件：</span><span class="sxs-lookup"><span data-stu-id="725e7-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="725e7-174">安裝 JSON 編輯器 - 您需要 JSON 編輯器才能使用構件定義檔。</span><span class="sxs-lookup"><span data-stu-id="725e7-174">Install a JSON editor - You need a JSON editor to work with artifact definition files.</span></span> <span data-ttu-id="725e7-175">建議您使用 [Visual Studio 程式碼](https://code.visualstudio.com/)，這適用於 Windows、Linux 和 OS X。</span><span class="sxs-lookup"><span data-stu-id="725e7-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="725e7-176">取得範例 artifactfile.json - 在我們的 [GitHub 存放庫](https://github.com/Azure/azure-devtestlab)中查看 Azure 研發/測試實驗室小組所建立的構件，我們在其中建立了豐富的構件庫，可協助您建立自己的構件。</span><span class="sxs-lookup"><span data-stu-id="725e7-176">Get a sample artifactfile.json - Check out the artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="725e7-177">下載構件定義檔，並對它進行變更以建立您自己的構件。</span><span class="sxs-lookup"><span data-stu-id="725e7-177">Download an artifact definition file and make changes to it to create your own artifacts.</span></span>
3. <span data-ttu-id="725e7-178">利用 IntelliSense - 運用 IntelliSense 來查看可用於建構構件定義檔的有效元素。</span><span class="sxs-lookup"><span data-stu-id="725e7-178">Make use of IntelliSense - Leverage IntelliSense to see valid elements that can be used to construct an artifact definition file.</span></span> <span data-ttu-id="725e7-179">您也可以看到適用於元素值的不同選項。</span><span class="sxs-lookup"><span data-stu-id="725e7-179">You can also see the different options for values of an element.</span></span> <span data-ttu-id="725e7-180">例如，IntelliSense 會在您編輯 **targetOsType** 元素時顯示 Windows 或 Linux 這兩個選項。</span><span class="sxs-lookup"><span data-stu-id="725e7-180">For example, IntelliSense show you the two choices of Windows or Linux when editing the **targetOsType** element.</span></span>
4. <span data-ttu-id="725e7-181">將構件儲存於 [Git 存放庫](devtest-lab-add-artifact-repo.md)中。</span><span class="sxs-lookup"><span data-stu-id="725e7-181">Store the artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="725e7-182">針對每個構件建立個別的目錄，目錄名稱必須與構件名稱相同。</span><span class="sxs-lookup"><span data-stu-id="725e7-182">Create a separate directory for each artifact where the directory name is the same as the artifact name.</span></span>
   2. <span data-ttu-id="725e7-183">將構件定義檔 (artifactfile.json) 儲存於您建立的目錄中。</span><span class="sxs-lookup"><span data-stu-id="725e7-183">Store the artifact definition file (artifactfile.json) in the directory you created.</span></span>
   3. <span data-ttu-id="725e7-184">儲存從構件安裝命令參考的指令碼。</span><span class="sxs-lookup"><span data-stu-id="725e7-184">Store the scripts that are referenced from the artifact install command.</span></span>
      
      <span data-ttu-id="725e7-185">構件資料夾的可能外觀範例如下：</span><span class="sxs-lookup"><span data-stu-id="725e7-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![構件 Git 儲存機制範例](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="725e7-187">將構件存放庫新增至實驗室 - 請參閱[新增成品和範本的 Git 存放庫](devtest-lab-add-artifact-repo.md)一文。</span><span class="sxs-lookup"><span data-stu-id="725e7-187">Add the artifacts repository to the lab - Refer to the article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="725e7-188">相關文章</span><span class="sxs-lookup"><span data-stu-id="725e7-188">Related articles</span></span>
* [<span data-ttu-id="725e7-189">如何診斷 DevTest Labs 中的構件失敗</span><span class="sxs-lookup"><span data-stu-id="725e7-189">How to diagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* <span data-ttu-id="725e7-190">[Join a VM to existing AD Domain using a resource manager template in Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs) (在 Azure DevTest Labs 中使用 Resource Manager 範本將 VM 加入至現有 AD 網域)</span><span class="sxs-lookup"><span data-stu-id="725e7-190">[Join a VM to existing AD Domain using a resource manager template in Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)</span></span>

## <a name="next-steps"></a><span data-ttu-id="725e7-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="725e7-191">Next steps</span></span>
* <span data-ttu-id="725e7-192">了解如何 [將 Git 構件儲存機制加入實驗室](devtest-lab-add-artifact-repo.md)。</span><span class="sxs-lookup"><span data-stu-id="725e7-192">Learn how to [add a Git artifact repository to a lab](devtest-lab-add-artifact-repo.md).</span></span>

