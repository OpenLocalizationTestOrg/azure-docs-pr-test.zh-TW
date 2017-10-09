---
title: "aaaRun Azure 批次的端對端工作而不需要撰寫程式碼 （預覽） |Microsoft 文件"
description: "建立 hello Azure CLI toocreate 批次集區、 工作和工作的範本檔案。"
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
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="f631f-103">使用 Azure Batch CLI 範本和檔案傳輸 (預覽)</span><span class="sxs-lookup"><span data-stu-id="f631f-103">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="f631f-104">使用 Azure CLI hello 很可能 toorun 批次作業，而不需要撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="f631f-104">Using hello Azure CLI it is possible toorun Batch jobs without writing code.</span></span>

<span data-ttu-id="f631f-105">可建立及使用以 hello Azure CLI，讓批次集區、 工作和工作 toobe 建立範本檔案。</span><span class="sxs-lookup"><span data-stu-id="f631f-105">Template files can be created and used with hello Azure CLI that allow Batch pools, jobs, and tasks toobe created.</span></span> <span data-ttu-id="f631f-106">作業輸入的檔可以輕鬆地上載 hello 與 hello 批次帳戶與工作輸出檔下載相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f631f-106">Job input files can be easily uploaded to hello storage account associated with hello Batch account and job output files downloaded.</span></span>

## <a name="overview"></a><span data-ttu-id="f631f-107">概觀</span><span class="sxs-lookup"><span data-stu-id="f631f-107">Overview</span></span>

<span data-ttu-id="f631f-108">延伸模組 toohello Azure CLI 啟用批次 toobe 使用端對端的使用者不是開發人員。</span><span class="sxs-lookup"><span data-stu-id="f631f-108">An extension toohello Azure CLI enables Batch toobe used end-to-end by users who are not developers.</span></span> <span data-ttu-id="f631f-109">可以建立的集區、 輸入的資料上傳，工作與相關聯的工作建立，以及 hello 產生輸出資料下載 – 沒有必要的程式碼 hello CLI 直接使用或已整合到指令碼。</span><span class="sxs-lookup"><span data-stu-id="f631f-109">A pool can be created, input data uploaded, jobs and associated tasks created, and hello resulting output data downloaded – no code required, hello CLI being used directly or being integrated into scripts.</span></span>

<span data-ttu-id="f631f-110">批次範本建置 hello [hello Azure CLI 中現有的批次支援](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation)toospecify 屬性值的 hello 建立集區、 工作、 工作和其他項目允許 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="f631f-110">Batch templates build on hello [existing Batch support in hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) that allows JSON files toospecify property values for hello creation of pools, jobs, tasks, and other items.</span></span> <span data-ttu-id="f631f-111">與批次範本 hello 下列功能會加入透過極限 hello JSON 檔案：</span><span class="sxs-lookup"><span data-stu-id="f631f-111">With Batch templates, hello following capabilities are added over what is possible with hello JSON files:</span></span>

-   <span data-ttu-id="f631f-112">可以定義參數。</span><span class="sxs-lookup"><span data-stu-id="f631f-112">Parameters can be defined.</span></span> <span data-ttu-id="f631f-113">使用 hello 範本時，只有 hello 參數值會指定的 toocreate hello 的項目，hello 的範本主體中指定其他項目屬性值。</span><span class="sxs-lookup"><span data-stu-id="f631f-113">When hello template is used, only hello parameter values are specified toocreate hello item, with other item property values being specified in hello template body.</span></span> <span data-ttu-id="f631f-114">了解批次和應用程式 toobe 執行批次的使用者可以建立範本，指定集區、 工作和工作屬性值。</span><span class="sxs-lookup"><span data-stu-id="f631f-114">A user who understands Batch and the applications toobe run by Batch can create templates, specifying pool, job, and task property values.</span></span> <span data-ttu-id="f631f-115">較不熟悉批次和 （或） 應用程式的使用者只需要定義 hello 參數 toospecify hello 值。</span><span class="sxs-lookup"><span data-stu-id="f631f-115">A user less familiar with Batch and/or the applications only needs toospecify hello values for hello defined parameters.</span></span>

-   <span data-ttu-id="f631f-116">作業工作 factory 建立一個或多個作業，避免 hello 與相關聯的工作需要許多建立的工作定義 toobe 和大幅簡化提交作業。</span><span class="sxs-lookup"><span data-stu-id="f631f-116">Job task factories create one or more tasks associated with a job, avoiding hello need for many task definitions toobe created and significantly simplifying job submission.</span></span>


<span data-ttu-id="f631f-117">輸入的資料檔案需 toobe 提供給工作，通常會產生輸出資料檔案。</span><span class="sxs-lookup"><span data-stu-id="f631f-117">Input data files need toobe supplied for jobs and output data files are often produced.</span></span> <span data-ttu-id="f631f-118">儲存體帳戶相關聯，根據預設，每一批次帳戶和檔案可以輕鬆地轉移的 tooand 從撰寫任何程式碼使用 CLI，此儲存體帳戶並所需的任何儲存體認證。</span><span class="sxs-lookup"><span data-stu-id="f631f-118">A storage account is associated, by default, with each Batch account and files can be easily transferred tooand from this storage account using the CLI, with no coding and no storage credentials required.</span></span>

<span data-ttu-id="f631f-119">例如，[ffmpeg](http://ffmpeg.org/) 是常用的應用程式，可處理音訊和視訊檔案。</span><span class="sxs-lookup"><span data-stu-id="f631f-119">For example, [ffmpeg](http://ffmpeg.org/) is a popular application that processes audio and video files.</span></span> <span data-ttu-id="f631f-120">hello Azure 批次 CLI 可以是使用的 tooinvoke ffmpeg tootranscode 來源視訊檔案 toodifferent 解析度。</span><span class="sxs-lookup"><span data-stu-id="f631f-120">hello Azure Batch CLI can be used tooinvoke ffmpeg tootranscode source video files toodifferent resolutions.</span></span>

-   <span data-ttu-id="f631f-121">會建立集區範本。</span><span class="sxs-lookup"><span data-stu-id="f631f-121">A pool template is created.</span></span> <span data-ttu-id="f631f-122">建立 hello 範本的 hello 使用者知道如何 toocall hello ffmpeg 應用程式和其的需求。它們指定 hello 適當的作業系統，VM 容量，ffmpeg 方式是安裝 （從應用程式封裝或使用封裝管理員，例如），和其他集區的屬性值。</span><span class="sxs-lookup"><span data-stu-id="f631f-122">hello user creating hello template knows how toocall hello ffmpeg application and its requirements; they specify hello appropriate OS, VM size, how ffmpeg is installed (from an application package or using a package manager, for example), and other pool property values.</span></span> <span data-ttu-id="f631f-123">因此只有 hello 集區識別碼和 Vm 數目使用 hello 範本時，需要 toobe 指定，會建立參數。</span><span class="sxs-lookup"><span data-stu-id="f631f-123">Parameters are created so when hello template is used, only hello pool id and number of VMs need toobe specified.</span></span>

-   <span data-ttu-id="f631f-124">會建立作業範本。</span><span class="sxs-lookup"><span data-stu-id="f631f-124">A job template is created.</span></span> <span data-ttu-id="f631f-125">hello 使用者建立 hello 範本知道如何 ffmpeg 需求 toobe 叫用 tootranscode 來源視訊 tooa 不同的解決方案，並指定 hello 工作命令列。它們也會知道已 hello 來源視訊檔案，包含與工作，每個輸入檔所需的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f631f-125">hello user creating hello template knows how ffmpeg needs toobe invoked tootranscode source video tooa different resolution and specifies hello task command line; they also know that there is a folder containing hello source video files, with a task required per input file.</span></span>

-   <span data-ttu-id="f631f-126">使用者所擁有的視訊檔案 tootranscode 一組會先建立集區使用 hello 集區範本，請指定唯一的 hello 集區識別碼和所需的 Vm 數目。</span><span class="sxs-lookup"><span data-stu-id="f631f-126">An end user with a set of video files tootranscode first creates a pool using hello pool template, specifying only hello pool id and number of VMs required.</span></span> <span data-ttu-id="f631f-127">然後，他們可以上傳 hello 來源檔案 tootranscode。</span><span class="sxs-lookup"><span data-stu-id="f631f-127">They can then upload hello source files tootranscode.</span></span> <span data-ttu-id="f631f-128">工作可以再使用提交 hello 工作範本，指定只有 hello 集區識別碼和上傳的 hello 來源檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="f631f-128">A job can then be submitted using hello job template, specifying only hello pool id and location of hello source files uploaded.</span></span> <span data-ttu-id="f631f-129">建立 hello 批次作業，請使用每個輸入檔案所產生的一項工作。</span><span class="sxs-lookup"><span data-stu-id="f631f-129">hello Batch job is created, with one task per input file being generated.</span></span> <span data-ttu-id="f631f-130">最後，hello 轉碼輸出檔可能會下載。</span><span class="sxs-lookup"><span data-stu-id="f631f-130">Finally, hello transcoded output files can be download.</span></span>

## <a name="installation"></a><span data-ttu-id="f631f-131">安裝</span><span class="sxs-lookup"><span data-stu-id="f631f-131">Installation</span></span>

<span data-ttu-id="f631f-132">hello 範本和檔案傳輸的功能需要安裝擴充功能 toobe。</span><span class="sxs-lookup"><span data-stu-id="f631f-132">hello template and file transfer capabilities require an extension toobe installed.</span></span>

<span data-ttu-id="f631f-133">如需有關如何查看 tooinstall hello Azure CLI 指示[安裝 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="f631f-133">For instructions on how tooinstall hello Azure CLI see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="f631f-134">一次 hello Azure CLI 安裝之後，可以安裝擴充功能，使用下列的 CLI 命令的批次 hello:</span><span class="sxs-lookup"><span data-stu-id="f631f-134">Once hello Azure CLI has been installed, hello Batch extension can be installed using the following CLI command:</span></span>

```azurecli
az component update --add batch-extensions --allow-third-party
```

<span data-ttu-id="f631f-135">如需 hello 批次的擴充功能的詳細資訊，請參閱[Microsoft Azure 批次 CLI 擴充功能的 Windows、 Mac 和 Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux)。</span><span class="sxs-lookup"><span data-stu-id="f631f-135">For more information about hello Batch extension, see [Microsoft Azure Batch CLI Extensions for Windows, Mac and Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span></span>

## <a name="templates"></a><span data-ttu-id="f631f-136">範本</span><span class="sxs-lookup"><span data-stu-id="f631f-136">Templates</span></span>

<span data-ttu-id="f631f-137">Azure 批次 CLI hello 可讓項目，例如集區、 工作和工作 toobe 藉由指定包含屬性名稱和值的 JSON 檔案建立。</span><span class="sxs-lookup"><span data-stu-id="f631f-137">hello Azure Batch CLI allows items such as pools, jobs, and tasks toobe created by specifying a JSON file containing property names and values.</span></span> <span data-ttu-id="f631f-138">例如：</span><span class="sxs-lookup"><span data-stu-id="f631f-138">For example:</span></span>

```azurecli
az batch pool create –-json-file AppPool.json
```

<span data-ttu-id="f631f-139">Azure 批次是類似 tooAzure 資源管理員範本，在功能和語法。</span><span class="sxs-lookup"><span data-stu-id="f631f-139">Azure Batch templates are similar tooAzure Resource Manager templates, in functionality and syntax.</span></span> <span data-ttu-id="f631f-140">這些屬性的 JSON 檔案所含的項目屬性名稱和值，但新增下列主要概念的 hello:</span><span class="sxs-lookup"><span data-stu-id="f631f-140">They are JSON files that contain item property names and values, but add hello following main concepts:</span></span>

-   <span data-ttu-id="f631f-141">**參數**</span><span class="sxs-lookup"><span data-stu-id="f631f-141">**Parameters**</span></span>

    -   <span data-ttu-id="f631f-142">允許屬性值 toobe 區段中指定主體，以只需要 toobe 時使用 hello 範本所提供的參數值。</span><span class="sxs-lookup"><span data-stu-id="f631f-142">Allow property values toobe specified in a body section, with only parameter values needing toobe supplied when hello template is used.</span></span> <span data-ttu-id="f631f-143">例如，hello 完整定義集區可以架設在 hello 本文和集區識別碼; 針對定義只有一個參數只包含集區的識別碼字串因此需要提供 toobe toocreate 集區。</span><span class="sxs-lookup"><span data-stu-id="f631f-143">For example, hello complete definition for a pool could be placed in hello body and only one parameter defined for pool id; only a pool id string therefore needs toobe supplied toocreate a pool.</span></span>
        
    -   <span data-ttu-id="f631f-144">hello 的範本主體可以用來撰寫的其他人了解的批次及 hello 應用程式 toobe 執行批次。當 hello 範本時，必須提供只有 hello 作者定義參數的值。</span><span class="sxs-lookup"><span data-stu-id="f631f-144">hello template body can be authored by someone with knowledge of Batch and hello applications toobe run by Batch; only values for hello author-defined parameters must be supplied when hello template is used.</span></span> <span data-ttu-id="f631f-145">不含使用者 hello 深入的批次和/或應用程式知識因此可以使用的範本。</span><span class="sxs-lookup"><span data-stu-id="f631f-145">A user without hello in-depth Batch and/or application knowledge can therefore use the templates.</span></span>

-   <span data-ttu-id="f631f-146">**變數**</span><span class="sxs-lookup"><span data-stu-id="f631f-146">**Variables**</span></span>

    -   <span data-ttu-id="f631f-147">允許簡單或複雜的參數值 toobe 在一個位置指定與 hello 範本主體中的一個或多個地方使用。</span><span class="sxs-lookup"><span data-stu-id="f631f-147">Allow simple or complex parameter values toobe specified in one place and used in one or more places in hello template body.</span></span> <span data-ttu-id="f631f-148">變數可以簡化和縮小 hello hello 範本，以及讓它更容易維護保留其中一個位置 toochange 屬性可能會變更其值。</span><span class="sxs-lookup"><span data-stu-id="f631f-148">Variables can simplify and reduce hello size of hello template, as well as make it more maintainable by having one location toochange properties whose value may change.</span></span>

-   <span data-ttu-id="f631f-149">**較高層級的建構**</span><span class="sxs-lookup"><span data-stu-id="f631f-149">**Higher-level constructs**</span></span>

    -   <span data-ttu-id="f631f-150">尚無法使用 hello 批次 Api 中的 hello 範本中使用較高層級的某些建構。</span><span class="sxs-lookup"><span data-stu-id="f631f-150">Some higher-level constructs are available in hello template that are not yet available in hello Batch APIs.</span></span> <span data-ttu-id="f631f-151">例如，工作 factory 可以建立 hello 作業使用的通用的工作定義的多個工作的工作範本定義。</span><span class="sxs-lookup"><span data-stu-id="f631f-151">For example, a task factory can be defined in a job template that creates multiple tasks for hello job using a common task definition.</span></span> <span data-ttu-id="f631f-152">這些建構函式會避免 hello 需要 toocode 來動態建立多個 JSON 檔案，例如每個工作中，一個檔案，以及建立指令碼檔案 tooinstall 應用程式透過封裝管理員 中，例如。</span><span class="sxs-lookup"><span data-stu-id="f631f-152">These constructs avoid hello need toocode to dynamically create multiple JSON files, such as one file per task, as well as create script files tooinstall applications via a package manager, for example.</span></span>

    -   <span data-ttu-id="f631f-153">在某些點，適用這些建構函式可能會加入 toothe 批次服務和中可用的 hello 批次 Api、 Ui 等等。</span><span class="sxs-lookup"><span data-stu-id="f631f-153">At some point, where applicable, these constructs may be added toothe Batch service and available in hello Batch APIs, UIs, etc.</span></span>

### <a name="pool-templates"></a><span data-ttu-id="f631f-154">集區範本</span><span class="sxs-lookup"><span data-stu-id="f631f-154">Pool templates</span></span>

<span data-ttu-id="f631f-155">此外 hello 集區範本所支援的參數和變數，遵循較高層級建構的 hello toohello 標準範本功能：</span><span class="sxs-lookup"><span data-stu-id="f631f-155">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello pool template:</span></span>

-   <span data-ttu-id="f631f-156">**套件參考**</span><span class="sxs-lookup"><span data-stu-id="f631f-156">**Package references**</span></span>

    -   <span data-ttu-id="f631f-157">（選擇性） 可讓軟體 toobe 複製 toopool 節點使用封裝管理員。</span><span class="sxs-lookup"><span data-stu-id="f631f-157">Optionally allows software toobe copied toopool nodes by using package managers.</span></span> <span data-ttu-id="f631f-158">指定 hello 封裝管理員 」 和 「 套件識別碼。</span><span class="sxs-lookup"><span data-stu-id="f631f-158">hello package manager and package id are specified.</span></span> <span data-ttu-id="f631f-159">所能 toodeclare 一或多個封裝可避免 hello 需要 toocreate 取得所需的 hello 封裝的指令碼、 安裝 hello 指令碼，並在集區中的每個節點上執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f631f-159">Being able toodeclare one or more packages avoids hello need toocreate a script that gets hello required packages, install hello script, and run hello script on each pool node.</span></span>

<span data-ttu-id="f631f-160">hello 下面是範例的安裝，且僅會建立 Linux Vm 的集區與 ffmpeg 範本需要集區識別碼字串和 hello 數量的 Vm 提供 toobe toouse:</span><span class="sxs-lookup"><span data-stu-id="f631f-160">hello following is an example of a template that creates a pool of Linux VMs with ffmpeg installed and only requires a pool id string and hello number of VMs toobe supplied toouse:</span></span>

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
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

<span data-ttu-id="f631f-161">如果 hello 範本檔案命名為_集區 ffmpeg.json_，然後 hello 範本會叫用，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f631f-161">If hello template file was named _pool-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a><span data-ttu-id="f631f-162">作業範本</span><span class="sxs-lookup"><span data-stu-id="f631f-162">Job templates</span></span>

<span data-ttu-id="f631f-163">此外 hello 工作範本所支援的參數和變數，遵循較高層級建構的 hello toohello 標準範本功能：</span><span class="sxs-lookup"><span data-stu-id="f631f-163">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello job template:</span></span>

-   <span data-ttu-id="f631f-164">**工作 Factory**</span><span class="sxs-lookup"><span data-stu-id="f631f-164">**Task factory**</span></span>

    -   <span data-ttu-id="f631f-165">會從一個工作定義中建立作業的多個工作。</span><span class="sxs-lookup"><span data-stu-id="f631f-165">Creates multiple tasks for a job from one task definition.</span></span> <span data-ttu-id="f631f-166">支援三種工作 Factory – 參數整理、每個檔案的工作和工作集合。</span><span class="sxs-lookup"><span data-stu-id="f631f-166">Three types of task factory are supported – parametric sweep, task per file, and task collection.</span></span>

<span data-ttu-id="f631f-167">hello 以下是範例會建立工作以 ffmpeg 轉碼 MP4 視訊檔案 tooone 的兩個較低的解析度，以使用每個來源視訊檔案建立一個工作的範本：</span><span class="sxs-lookup"><span data-stu-id="f631f-167">hello following is an example of a template that creates a job that uses ffmpeg to transcode MP4 video files tooone of two lower resolutions, with one task created per source video file:</span></span>

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
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

<span data-ttu-id="f631f-168">如果 hello 範本檔案命名為_作業 ffmpeg.json_，然後 hello 範本會叫用，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f631f-168">If hello template file was named _job-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a><span data-ttu-id="f631f-169">檔案群組和檔案傳輸</span><span class="sxs-lookup"><span data-stu-id="f631f-169">File groups and file transfer</span></span>

<span data-ttu-id="f631f-170">大部分的作業與工作都需要輸入檔，並且會產生輸出檔。</span><span class="sxs-lookup"><span data-stu-id="f631f-170">Most jobs and tasks require input files and produce output files.</span></span> <span data-ttu-id="f631f-171">這兩個輸入檔和輸出檔通常需要 toobe 傳輸，從 hello 用戶端 toohello 節點，或從 hello 節點 toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="f631f-171">Both input files and output files typically need toobe transferred, either from hello client toohello node, or from hello node toohello client.</span></span> <span data-ttu-id="f631f-172">hello Azure 批次 CLI 延伸抽象化抽離的檔案傳輸，而且會運用 hello 儲存體帳戶所建立的每個批次帳戶的預設值。</span><span class="sxs-lookup"><span data-stu-id="f631f-172">hello Azure Batch CLI extension abstracts away file transfer and utilizes hello storage account that is created by default for each Batch account.</span></span>

<span data-ttu-id="f631f-173">檔案群組等同 tooa hello Azure 儲存體帳戶中建立的容器。</span><span class="sxs-lookup"><span data-stu-id="f631f-173">A file group equates tooa container that is created in hello Azure storage account.</span></span> <span data-ttu-id="f631f-174">hello 檔案群組可能會有子資料夾。</span><span class="sxs-lookup"><span data-stu-id="f631f-174">hello file group may have subfolders.</span></span>

<span data-ttu-id="f631f-175">hello 批次 CLI 延伸模組會提供來自用戶端 tooa 指定的檔案群組的檔案上傳和下載檔案，從指定的檔案群組 tooa 用戶端 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="f631f-175">hello Batch CLI extension provides commands for uploading files from client tooa specified file group and downloading files from hello specified file group tooa client.</span></span>

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

<span data-ttu-id="f631f-176">集區和工作的範本可讓儲存在檔案群組 toobe 為複製到集區的節點上指定的檔案或集區關閉節點恢復 tooa 檔案群組。</span><span class="sxs-lookup"><span data-stu-id="f631f-176">Pool and job templates allow files stored in file groups toobe specified for copy onto pool nodes or off pool nodes back tooa file group.</span></span> <span data-ttu-id="f631f-177">比方說，在先前指定的工作範本，hello 檔案群組 「 ffmpeg-輸入 」，被指定 hello 工作 factory 為 hello 的 hello 來源視訊檔案複製到的轉碼; hello 節點上的位置hello 檔案群組"ffmpeg-output"作為 hello 位置 hello 轉碼輸出檔案的位置複製 toofrom hello 節點執行每項工作。</span><span class="sxs-lookup"><span data-stu-id="f631f-177">For example, in the job template specified previously, hello file group “ffmpeg-input” is specified for hello task factory as hello location of hello source video files copied down onto hello node for transcoding; hello file group “ffmpeg-output” is used as hello location where hello transcoded output files are copied toofrom hello node running each task.</span></span>

## <a name="summary"></a><span data-ttu-id="f631f-178">摘要</span><span class="sxs-lookup"><span data-stu-id="f631f-178">Summary</span></span>

<span data-ttu-id="f631f-179">範本和檔案傳輸支援目前已加入 toohello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="f631f-179">Template and file transfer support have currently been added only toohello Azure CLI.</span></span> <span data-ttu-id="f631f-180">hello 目標是可讓使用者不需要使用 hello 批次應用程式開發介面，例如研究人員、 IT 使用者等 toodevelop 程式碼的批次 toousers tooexpand hello 對象。</span><span class="sxs-lookup"><span data-stu-id="f631f-180">hello goal is tooexpand hello audience that can use Batch toousers who do not need toodevelop code using hello Batch APIs, such as researchers, IT users, and so on.</span></span> <span data-ttu-id="f631f-181">沒有程式碼撰寫，非常了解 Azure 批次及 hello 應用程式 toobe 批次所執行的使用者可以建立集區和工作建立的範本。</span><span class="sxs-lookup"><span data-stu-id="f631f-181">Without coding, users with knowledge of Azure, Batch, and hello applications toobe run by Batch can create templates for pool and job creation.</span></span> <span data-ttu-id="f631f-182">範本參數，與未批次和 hello 的應用程式的詳細知識，使用者可以使用 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="f631f-182">With template parameters, users without detailed knowledge of Batch and hello applications can use hello templates.</span></span>

<span data-ttu-id="f631f-183">嘗試 hello hello Azure CLI 的批次延伸模組，並提供任何意見反應或改善建議，可能是在 hello 註解，如這篇文章，或透過 hello [Azure Batch 論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch)。</span><span class="sxs-lookup"><span data-stu-id="f631f-183">Try out hello Batch extension for hello Azure CLI and provide us with any feedback or suggestions, either in hello comments for this article or via hello [Azure Batch forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f631f-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f631f-184">Next steps</span></span>

- <span data-ttu-id="f631f-185">請參閱 hello 批次範本部落格文章：[執行 Azure 批次作業使用 hello Azure CLI – 沒有所需的程式碼](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/)。</span><span class="sxs-lookup"><span data-stu-id="f631f-185">See hello Batch templates blog post: [Running Azure Batch jobs using hello Azure CLI – no code required](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span></span>
- <span data-ttu-id="f631f-186">詳細的安裝與使用文件、 範例和原始程式碼位於 hello [Azure GitHub 儲存機制](https://github.com/Azure/azure-batch-cli-extensions)。</span><span class="sxs-lookup"><span data-stu-id="f631f-186">Detailed installation and usage documentation, samples, and source code are available in hello [Azure GitHub repository](https://github.com/Azure/azure-batch-cli-extensions).</span></span>
