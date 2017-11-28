---
title: "無須撰寫程式碼即可執行 Azure Batch 作業端對端 (預覽) | Microsoft Docs"
description: "建立 Azure CLI 的範本檔案來建立 Batch 集區、作業和工作。"
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: 6b91466da46d1f4ca9f25bf1718be783603efc58
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="6c63b-103">使用 Azure Batch CLI 範本和檔案傳輸 (預覽)</span><span class="sxs-lookup"><span data-stu-id="6c63b-103">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="6c63b-104">使用 Azure CLI 就可直接執行 Batch 作業而不需要撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="6c63b-104">Using the Azure CLI it is possible to run Batch jobs without writing code.</span></span>

<span data-ttu-id="6c63b-105">可建立範本檔案並與 Azure CLI 搭配使用，從而建立 Batch 集區、作業和工作。</span><span class="sxs-lookup"><span data-stu-id="6c63b-105">Template files can be created and used with the Azure CLI that allow Batch pools, jobs, and tasks to be created.</span></span> <span data-ttu-id="6c63b-106">可以輕鬆地將作業輸入檔案上傳至與 Batch 帳戶和已下載之作業輸出檔案相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6c63b-106">Job input files can be easily uploaded to the storage account associated with the Batch account and job output files downloaded.</span></span>

## <a name="overview"></a><span data-ttu-id="6c63b-107">概觀</span><span class="sxs-lookup"><span data-stu-id="6c63b-107">Overview</span></span>

<span data-ttu-id="6c63b-108">Azure CLI 的擴充功能可讓非開發人員的使用者端對端使用 Batch。</span><span class="sxs-lookup"><span data-stu-id="6c63b-108">An extension to the Azure CLI enables Batch to be used end-to-end by users who are not developers.</span></span> <span data-ttu-id="6c63b-109">可以建立集區、上傳輸入資料、建立作業和相關聯的工作，並下載產生的輸出資料 – 無需任何程式碼，會直接使用 CLI 或加以整合到指令碼。</span><span class="sxs-lookup"><span data-stu-id="6c63b-109">A pool can be created, input data uploaded, jobs and associated tasks created, and the resulting output data downloaded – no code required, the CLI being used directly or being integrated into scripts.</span></span>

<span data-ttu-id="6c63b-110">Batch 範本會建置在 [Azure CLI 中的現有 Batch 支援](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation)上，可讓 JSON 檔案指定建立集區、作業、工作及其他項目的屬性值。</span><span class="sxs-lookup"><span data-stu-id="6c63b-110">Batch templates build on the [existing Batch support in the Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) that allows JSON files to specify property values for the creation of pools, jobs, tasks, and other items.</span></span> <span data-ttu-id="6c63b-111">透過 Batch 範本，可對 JSON 檔案的可行項目新增下列功能：</span><span class="sxs-lookup"><span data-stu-id="6c63b-111">With Batch templates, the following capabilities are added over what is possible with the JSON files:</span></span>

-   <span data-ttu-id="6c63b-112">可以定義參數。</span><span class="sxs-lookup"><span data-stu-id="6c63b-112">Parameters can be defined.</span></span> <span data-ttu-id="6c63b-113">使用範本時，只會指定要建立項目的參數值，其他項目的屬性值則是在範本主體中指定。</span><span class="sxs-lookup"><span data-stu-id="6c63b-113">When the template is used, only the parameter values are specified to create the item, with other item property values being specified in the template body.</span></span> <span data-ttu-id="6c63b-114">了解 Batch 及 Batch 所要執行之應用程式的使用者可以建立範本，並指定集區、作業和工作屬性值。</span><span class="sxs-lookup"><span data-stu-id="6c63b-114">A user who understands Batch and the applications to be run by Batch can create templates, specifying pool, job, and task property values.</span></span> <span data-ttu-id="6c63b-115">較不熟悉 Batch 和/或應用程式的使用者，只需要指定已定義之參數的值。</span><span class="sxs-lookup"><span data-stu-id="6c63b-115">A user less familiar with Batch and/or the applications only needs to specify the values for the defined parameters.</span></span>

-   <span data-ttu-id="6c63b-116">作業工作 Factory 會建立一或多個與作業相關聯的工作，讓您既不必建立許多工作定義，又可大幅簡化作業的提交程序。</span><span class="sxs-lookup"><span data-stu-id="6c63b-116">Job task factories create one or more tasks associated with a job, avoiding the need for many task definitions to be created and significantly simplifying job submission.</span></span>


<span data-ttu-id="6c63b-117">必須為作業提供輸入資料檔案，通常會產生輸出資料檔案。</span><span class="sxs-lookup"><span data-stu-id="6c63b-117">Input data files need to be supplied for jobs and output data files are often produced.</span></span> <span data-ttu-id="6c63b-118">根據預設，儲存體帳戶會與每個 Batch 帳戶相關聯，且可以使用 CLI 輕鬆地將檔案向這個儲存體帳戶往來傳輸，不必編寫程式碼也不需要任何儲存體認證。</span><span class="sxs-lookup"><span data-stu-id="6c63b-118">A storage account is associated, by default, with each Batch account and files can be easily transferred to and from this storage account using the CLI, with no coding and no storage credentials required.</span></span>

<span data-ttu-id="6c63b-119">例如，[ffmpeg](http://ffmpeg.org/) 是常用的應用程式，可處理音訊和視訊檔案。</span><span class="sxs-lookup"><span data-stu-id="6c63b-119">For example, [ffmpeg](http://ffmpeg.org/) is a popular application that processes audio and video files.</span></span> <span data-ttu-id="6c63b-120">Azure Batch CLI 可以用來叫用 ffmpeg，將來源視訊檔案轉碼為不同的解析度。</span><span class="sxs-lookup"><span data-stu-id="6c63b-120">The Azure Batch CLI can be used to invoke ffmpeg to transcode source video files to different resolutions.</span></span>

-   <span data-ttu-id="6c63b-121">會建立集區範本。</span><span class="sxs-lookup"><span data-stu-id="6c63b-121">A pool template is created.</span></span> <span data-ttu-id="6c63b-122">建立範本的使用者知道如何呼叫 ffmpeg 應用程式及其需求；他們會指定適當的 OS、VM 大小、ffmpeg 的安裝方式 (例如，從應用程式套件或使用套件管理員)，和其他集區屬性值。</span><span class="sxs-lookup"><span data-stu-id="6c63b-122">The user creating the template knows how to call the ffmpeg application and its requirements; they specify the appropriate OS, VM size, how ffmpeg is installed (from an application package or using a package manager, for example), and other pool property values.</span></span> <span data-ttu-id="6c63b-123">會建立參數，因此當使用範本時，只需要指定集區識別碼和 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="6c63b-123">Parameters are created so when the template is used, only the pool id and number of VMs need to be specified.</span></span>

-   <span data-ttu-id="6c63b-124">會建立作業範本。</span><span class="sxs-lookup"><span data-stu-id="6c63b-124">A job template is created.</span></span> <span data-ttu-id="6c63b-125">建立範本的使用者知道要將來源視訊轉碼為不同解析度所需要叫用 ffmpeg 的方式，且會指定工作命令列；他們也知道會有包含來源視訊檔案的資料夾，以及每個輸入檔案所需的工作。</span><span class="sxs-lookup"><span data-stu-id="6c63b-125">The user creating the template knows how ffmpeg needs to be invoked to transcode source video to a different resolution and specifies the task command line; they also know that there is a folder containing the source video files, with a task required per input file.</span></span>

-   <span data-ttu-id="6c63b-126">需要將一組視訊檔案進行轉碼的使用者會先使用集區範本來建立集區，從而僅指定集區識別碼和所需的 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="6c63b-126">An end user with a set of video files to transcode first creates a pool using the pool template, specifying only the pool id and number of VMs required.</span></span> <span data-ttu-id="6c63b-127">接著，他們可以上傳要轉換的來源檔案。</span><span class="sxs-lookup"><span data-stu-id="6c63b-127">They can then upload the source files to transcode.</span></span> <span data-ttu-id="6c63b-128">然後可以使用作業範本來提交作業，從而僅指定集區識別碼和已上傳來源檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="6c63b-128">A job can then be submitted using the job template, specifying only the pool id and location of the source files uploaded.</span></span> <span data-ttu-id="6c63b-129">將會建立 Batch 作業，每個所產生的輸入檔案會有一項工作。</span><span class="sxs-lookup"><span data-stu-id="6c63b-129">The Batch job is created, with one task per input file being generated.</span></span> <span data-ttu-id="6c63b-130">最後，可以下載轉碼的輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="6c63b-130">Finally, the transcoded output files can be download.</span></span>

## <a name="installation"></a><span data-ttu-id="6c63b-131">安裝</span><span class="sxs-lookup"><span data-stu-id="6c63b-131">Installation</span></span>

<span data-ttu-id="6c63b-132">範本和檔案傳輸功能需要安裝擴充功能。</span><span class="sxs-lookup"><span data-stu-id="6c63b-132">The template and file transfer capabilities require an extension to be installed.</span></span>

<span data-ttu-id="6c63b-133">如需有關如何安裝 Azure CLI 的指示，請參閱[安裝 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="6c63b-133">For instructions on how to install the Azure CLI see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="6c63b-134">一旦安裝 Azure CLI 之後，可以使用下列 CLI 命令來安裝 Batch 擴充功能：</span><span class="sxs-lookup"><span data-stu-id="6c63b-134">Once the Azure CLI has been installed, the Batch extension can be installed using the following CLI command:</span></span>

```azurecli
az component update --add batch-extensions --allow-third-party
```

<span data-ttu-id="6c63b-135">如需 Batch 擴充功能的詳細資訊，請參閱[適用於 Windows、Mac 和 Linux 的 Microsoft Azure Batch CLI 擴充功能](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux)。</span><span class="sxs-lookup"><span data-stu-id="6c63b-135">For more information about the Batch extension, see [Microsoft Azure Batch CLI Extensions for Windows, Mac and Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span></span>

## <a name="templates"></a><span data-ttu-id="6c63b-136">範本</span><span class="sxs-lookup"><span data-stu-id="6c63b-136">Templates</span></span>

<span data-ttu-id="6c63b-137">Azure Batch CLI 可允許建立諸如集區、作業和工作等項目，方法是指定包含屬性名稱和值的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="6c63b-137">The Azure Batch CLI allows items such as pools, jobs, and tasks to be created by specifying a JSON file containing property names and values.</span></span> <span data-ttu-id="6c63b-138">例如：</span><span class="sxs-lookup"><span data-stu-id="6c63b-138">For example:</span></span>

```azurecli
az batch pool create –-json-file AppPool.json
```

<span data-ttu-id="6c63b-139">Azure Batch 範本在功能和語法方面類似於 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="6c63b-139">Azure Batch templates are similar to Azure Resource Manager templates, in functionality and syntax.</span></span> <span data-ttu-id="6c63b-140">這些是包含項目屬性名稱和值的 JSON 檔案，但新增下列主要概念：</span><span class="sxs-lookup"><span data-stu-id="6c63b-140">They are JSON files that contain item property names and values, but add the following main concepts:</span></span>

-   <span data-ttu-id="6c63b-141">**參數**</span><span class="sxs-lookup"><span data-stu-id="6c63b-141">**Parameters**</span></span>

    -   <span data-ttu-id="6c63b-142">允許在主體區段中指定屬性值，包含僅於使用此範本時需要提供的參數值。</span><span class="sxs-lookup"><span data-stu-id="6c63b-142">Allow property values to be specified in a body section, with only parameter values needing to be supplied when the template is used.</span></span> <span data-ttu-id="6c63b-143">例如，集區的完整定義可放在主體中，且僅針對集區識別碼定義一個參數；因此，只需要提供一個集區識別碼字串即可建立集區。</span><span class="sxs-lookup"><span data-stu-id="6c63b-143">For example, the complete definition for a pool could be placed in the body and only one parameter defined for pool id; only a pool id string therefore needs to be supplied to create a pool.</span></span>
        
    -   <span data-ttu-id="6c63b-144">可由了解 Batch 和由 Batch 執行之應用程式的人員撰寫範本主體；僅在使用此範本時，才必須提供作者定義參數的值。</span><span class="sxs-lookup"><span data-stu-id="6c63b-144">The template body can be authored by someone with knowledge of Batch and the applications to be run by Batch; only values for the author-defined parameters must be supplied when the template is used.</span></span> <span data-ttu-id="6c63b-145">因此，未深入了解 Batch 和/或應用程式知識的使用者可以使用此範本。</span><span class="sxs-lookup"><span data-stu-id="6c63b-145">A user without the in-depth Batch and/or application knowledge can therefore use the templates.</span></span>

-   <span data-ttu-id="6c63b-146">**變數**</span><span class="sxs-lookup"><span data-stu-id="6c63b-146">**Variables**</span></span>

    -   <span data-ttu-id="6c63b-147">允許在單一位置中指定簡單或複雜的參數值，並在範本主體的一個或多個位置加以使用。</span><span class="sxs-lookup"><span data-stu-id="6c63b-147">Allow simple or complex parameter values to be specified in one place and used in one or more places in the template body.</span></span> <span data-ttu-id="6c63b-148">變數可以簡化和降低範本的大小，並讓它更易於維護，方法是具備一個位置，將需要變更值的屬性加以變更。</span><span class="sxs-lookup"><span data-stu-id="6c63b-148">Variables can simplify and reduce the size of the template, as well as make it more maintainable by having one location to change properties whose value may change.</span></span>

-   <span data-ttu-id="6c63b-149">**較高層級的建構**</span><span class="sxs-lookup"><span data-stu-id="6c63b-149">**Higher-level constructs**</span></span>

    -   <span data-ttu-id="6c63b-150">部分在範本中可使用的較高層級建構尚無法在 Batch API 中使用。</span><span class="sxs-lookup"><span data-stu-id="6c63b-150">Some higher-level constructs are available in the template that are not yet available in the Batch APIs.</span></span> <span data-ttu-id="6c63b-151">例如，可在作業範本中定義的工作 Factory，會使用通用的工作定義來建立作業的多個工作。</span><span class="sxs-lookup"><span data-stu-id="6c63b-151">For example, a task factory can be defined in a job template that creates multiple tasks for the job using a common task definition.</span></span> <span data-ttu-id="6c63b-152">這些建構不需要編碼即可動態建立多個 JSON 檔案，例如每個工作一個檔案，以及建立指令碼檔，透過例如套件管理員來安裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c63b-152">These constructs avoid the need to code to dynamically create multiple JSON files, such as one file per task, as well as create script files to install applications via a package manager, for example.</span></span>

    -   <span data-ttu-id="6c63b-153">在某些適用的情況下，可能會將這些建構新增至 Batch 服務，且適用於 Batch API、UI 等等。</span><span class="sxs-lookup"><span data-stu-id="6c63b-153">At some point, where applicable, these constructs may be added to the Batch service and available in the Batch APIs, UIs, etc.</span></span>

### <a name="pool-templates"></a><span data-ttu-id="6c63b-154">集區範本</span><span class="sxs-lookup"><span data-stu-id="6c63b-154">Pool templates</span></span>

<span data-ttu-id="6c63b-155">除了標準參數和變數的範本功能，集區範本也支援下列較高層級的建構：</span><span class="sxs-lookup"><span data-stu-id="6c63b-155">In addition to the standard template capabilities of parameters and variables, the following higher-level constructs are supported by the pool template:</span></span>

-   <span data-ttu-id="6c63b-156">**套件參考**</span><span class="sxs-lookup"><span data-stu-id="6c63b-156">**Package references**</span></span>

    -   <span data-ttu-id="6c63b-157">使用套件管理員選擇性地讓軟體複製到集區節點。</span><span class="sxs-lookup"><span data-stu-id="6c63b-157">Optionally allows software to be copied to pool nodes by using package managers.</span></span> <span data-ttu-id="6c63b-158">會指定套件管理員和套件識別碼。</span><span class="sxs-lookup"><span data-stu-id="6c63b-158">The package manager and package id are specified.</span></span> <span data-ttu-id="6c63b-159">能夠宣告一個或多個套件，從而免於建立取得必要套件的指令碼、安裝指令碼，並在每個集區節點上執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="6c63b-159">Being able to declare one or more packages avoids the need to create a script that gets the required packages, install the script, and run the script on each pool node.</span></span>

<span data-ttu-id="6c63b-160">以下範例是建立已安裝 ffmpeg 之 Linux VM 集區的範本，且只需要集區識別碼字串和所提供的 VM 數目以使用：</span><span class="sxs-lookup"><span data-stu-id="6c63b-160">The following is an example of a template that creates a pool of Linux VMs with ffmpeg installed and only requires a pool id string and the number of VMs to be supplied to use:</span></span>

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "The number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "The pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

<span data-ttu-id="6c63b-161">如果範本檔名為 _pool-ffmpeg.json_，則會叫用範本，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6c63b-161">If the template file was named _pool-ffmpeg.json_, then the template would be invoked as follows:</span></span>

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a><span data-ttu-id="6c63b-162">作業範本</span><span class="sxs-lookup"><span data-stu-id="6c63b-162">Job templates</span></span>

<span data-ttu-id="6c63b-163">除了標準參數和變數的範本功能，作業範本也支援下列較高層級的建構：</span><span class="sxs-lookup"><span data-stu-id="6c63b-163">In addition to the standard template capabilities of parameters and variables, the following higher-level constructs are supported by the job template:</span></span>

-   <span data-ttu-id="6c63b-164">**工作 Factory**</span><span class="sxs-lookup"><span data-stu-id="6c63b-164">**Task factory**</span></span>

    -   <span data-ttu-id="6c63b-165">會從一個工作定義中建立作業的多個工作。</span><span class="sxs-lookup"><span data-stu-id="6c63b-165">Creates multiple tasks for a job from one task definition.</span></span> <span data-ttu-id="6c63b-166">支援三種工作 Factory – 參數整理、每個檔案的工作和工作集合。</span><span class="sxs-lookup"><span data-stu-id="6c63b-166">Three types of task factory are supported – parametric sweep, task per file, and task collection.</span></span>

<span data-ttu-id="6c63b-167">以下範例是建立作業的範本，該作業會使用 ffmpeg 將 MP4 視訊檔案轉碼為兩個較低的解析度之一，其中每個來源視訊檔案會建立一個工作：</span><span class="sxs-lookup"><span data-stu-id="6c63b-167">The following is an example of a template that creates a job that uses ffmpeg to transcode MP4 video files to one of two lower resolutions, with one task created per source video file:</span></span>

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "The name of Azure Batch pool which runs the job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "The name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

<span data-ttu-id="6c63b-168">如果範本檔名為 _job-ffmpeg.json_，則會叫用範本，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6c63b-168">If the template file was named _job-ffmpeg.json_, then the template would be invoked as follows:</span></span>

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a><span data-ttu-id="6c63b-169">檔案群組和檔案傳輸</span><span class="sxs-lookup"><span data-stu-id="6c63b-169">File groups and file transfer</span></span>

<span data-ttu-id="6c63b-170">大部分的作業與工作都需要輸入檔，並且會產生輸出檔。</span><span class="sxs-lookup"><span data-stu-id="6c63b-170">Most jobs and tasks require input files and produce output files.</span></span> <span data-ttu-id="6c63b-171">輸入檔和輸出檔通常需要進行傳送，不論是從用戶端傳送至節點，還是從節點傳送至用戶端。</span><span class="sxs-lookup"><span data-stu-id="6c63b-171">Both input files and output files typically need to be transferred, either from the client to the node, or from the node to the client.</span></span> <span data-ttu-id="6c63b-172">Azure Batch CLI 擴充功能可將檔案傳輸抽象化抽離，並且使用依預設針對每個 Batch 帳戶所建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6c63b-172">The Azure Batch CLI extension abstracts away file transfer and utilizes the storage account that is created by default for each Batch account.</span></span>

<span data-ttu-id="6c63b-173">檔案群組等同於在 Azure 儲存體帳戶中建立的容器。</span><span class="sxs-lookup"><span data-stu-id="6c63b-173">A file group equates to a container that is created in the Azure storage account.</span></span> <span data-ttu-id="6c63b-174">檔案群組可具有子資料夾。</span><span class="sxs-lookup"><span data-stu-id="6c63b-174">The file group may have subfolders.</span></span>

<span data-ttu-id="6c63b-175">Batch CLI 擴充功能會提供命令，以供您從用戶端將檔案上傳到指定的檔案群組，以及從指定的檔案群組將檔案下載到用戶端。</span><span class="sxs-lookup"><span data-stu-id="6c63b-175">The Batch CLI extension provides commands for uploading files from client to a specified file group and downloading files from the specified file group to a client.</span></span>

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

<span data-ttu-id="6c63b-176">集區和作業範本允許指定儲存在檔案群組中的檔案，以複製到集區節點上，或從集區節點複製回到檔案群組。</span><span class="sxs-lookup"><span data-stu-id="6c63b-176">Pool and job templates allow files stored in file groups to be specified for copy onto pool nodes or off pool nodes back to a file group.</span></span> <span data-ttu-id="6c63b-177">例如，在先前指定的作業範本中，會指定工作 Factory 的 “ffmpeg-input” 檔案群組，作為向下複製到節點以進行轉碼之來源視訊檔案的位置；“ffmpeg-output” 檔案群組則是用來作為從執行每項工作的節點複製轉碼輸出檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="6c63b-177">For example, in the job template specified previously, the file group “ffmpeg-input” is specified for the task factory as the location of the source video files copied down onto the node for transcoding; the file group “ffmpeg-output” is used as the location where the transcoded output files are copied to from the node running each task.</span></span>

## <a name="summary"></a><span data-ttu-id="6c63b-178">摘要</span><span class="sxs-lookup"><span data-stu-id="6c63b-178">Summary</span></span>

<span data-ttu-id="6c63b-179">目前僅已將範本和檔案傳輸支援新增至 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="6c63b-179">Template and file transfer support have currently been added only to the Azure CLI.</span></span> <span data-ttu-id="6c63b-180">目標旨在將可使用 Batch 的對象拓展到不需要使用 Batch API 來開發程式碼的使用者，例如研究人員、IT 使用者等等。</span><span class="sxs-lookup"><span data-stu-id="6c63b-180">The goal is to expand the audience that can use Batch to users who do not need to develop code using the Batch APIs, such as researchers, IT users, and so on.</span></span> <span data-ttu-id="6c63b-181">無需程式碼撰寫，了解 Azure、Batch 和 Batch 所要執行之應用程式的使用者可以建立集區和作業建立的範本。</span><span class="sxs-lookup"><span data-stu-id="6c63b-181">Without coding, users with knowledge of Azure, Batch, and the applications to be run by Batch can create templates for pool and job creation.</span></span> <span data-ttu-id="6c63b-182">利用範本參數，未深入了解 Batch 和應用程式的使用者就可以使用範本。</span><span class="sxs-lookup"><span data-stu-id="6c63b-182">With template parameters, users without detailed knowledge of Batch and the applications can use the templates.</span></span>

<span data-ttu-id="6c63b-183">請試用 Azure CLI 的 Batch 擴充功能，並利用本文的評論或透過 [Azure Batch 論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch)將您的意見或建議告訴我們。</span><span class="sxs-lookup"><span data-stu-id="6c63b-183">Try out the Batch extension for the Azure CLI and provide us with any feedback or suggestions, either in the comments for this article or via the [Azure Batch forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c63b-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c63b-184">Next steps</span></span>

- <span data-ttu-id="6c63b-185">請參閱 Batch 範本部落格文章：[使用 Azure CLI 執行 Azure Batch 作業 – 不需要程式碼](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/)。</span><span class="sxs-lookup"><span data-stu-id="6c63b-185">See the Batch templates blog post: [Running Azure Batch jobs using the Azure CLI – no code required](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span></span>
- <span data-ttu-id="6c63b-186">您可在 [Azure GitHub 存放庫](https://github.com/Azure/azure-batch-cli-extensions)中取得詳細的安裝與使用文件、範例和原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="6c63b-186">Detailed installation and usage documentation, samples, and source code are available in the [Azure GitHub repository](https://github.com/Azure/azure-batch-cli-extensions).</span></span>
