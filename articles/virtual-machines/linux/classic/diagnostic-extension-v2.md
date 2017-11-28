---
title: "aaaMonitoring Linux VM 的 VM 延伸模組與 |Microsoft 文件"
description: "了解如何 toouse hello Linux 診斷延伸模組 toomonitor hello 效能和診斷資料，在 Azure 中 Linux 虛擬機器。"
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: cf7bfebca8c0367941f7a975417f60fe2e2dab25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-linux-diagnostic-extension-toomonitor-hello-performance-and-diagnostic-data-of-a-linux-vm"></a><span data-ttu-id="213f1-103">使用 hello Linux 診斷延伸模組 toomonitor hello 效能和診斷資料的 Linux VM</span><span class="sxs-lookup"><span data-stu-id="213f1-103">Use hello Linux Diagnostic Extension toomonitor hello performance and diagnostic data of a Linux VM</span></span>

<span data-ttu-id="213f1-104">本文件說明 2.3 版 hello Linux 診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="213f1-104">This document describes version 2.3 of hello Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="213f1-105">此版本已被取代，且可能會在 2018 年 6 月 30 日之後取消發佈。</span><span class="sxs-lookup"><span data-stu-id="213f1-105">This version is deprecated, and it may be unpublished any time after June 30, 2018.</span></span> <span data-ttu-id="213f1-106">3.0 版已取代該版本。</span><span class="sxs-lookup"><span data-stu-id="213f1-106">It has been replaced by version 3.0.</span></span> <span data-ttu-id="213f1-107">如需詳細資訊，請參閱 hello [3.0 版的 hello Linux 診斷延伸模組的文件](../diagnostic-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="213f1-107">For more information, see hello [documentation for version 3.0 of hello Linux Diagnostic Extension](../diagnostic-extension.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="213f1-108">簡介</span><span class="sxs-lookup"><span data-stu-id="213f1-108">Introduction</span></span>

<span data-ttu-id="213f1-109">(**注意**: hello Linux 診斷延伸模組是開放上[GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic)其中第一次發行 hello hello 擴充功能上最新的資訊。</span><span class="sxs-lookup"><span data-stu-id="213f1-109">(**Note**: hello Linux Diagnostic Extension is open-sourced on [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) where hello most current information on hello extension is first published.</span></span> <span data-ttu-id="213f1-110">您可能會想 toocheck hello [GitHub 頁面](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic)第一次。)</span><span class="sxs-lookup"><span data-stu-id="213f1-110">You might want toocheck hello [GitHub page](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) first.)</span></span>

<span data-ttu-id="213f1-111">hello Linux 診斷延伸模組可協助使用者監視 hello Microsoft Azure 執行的 Linux Vm。</span><span class="sxs-lookup"><span data-stu-id="213f1-111">hello Linux Diagnostic Extension helps a user monitor hello Linux VMs that are running on Microsoft Azure.</span></span> <span data-ttu-id="213f1-112">它有下列功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="213f1-112">It has hello following capabilities:</span></span>

* <span data-ttu-id="213f1-113">會收集和上傳 hello Linux VM toohello 使用者的儲存體資料表，包括診斷及 syslog 資訊中的 hello 系統效能資訊。</span><span class="sxs-lookup"><span data-stu-id="213f1-113">Collects and uploads hello system performance information from hello Linux VM toohello user's storage table, including diagnostic and syslog information.</span></span>
* <span data-ttu-id="213f1-114">可讓使用者 toocustomize hello 資料度量資訊會收集和上傳。</span><span class="sxs-lookup"><span data-stu-id="213f1-114">Enables users toocustomize hello data metrics that will be collected and uploaded.</span></span>
* <span data-ttu-id="213f1-115">可讓使用者 tooupload 指定的記錄檔 tooa 指定之儲存體資料表。</span><span class="sxs-lookup"><span data-stu-id="213f1-115">Enables users tooupload specified log files tooa designated storage table.</span></span>

<span data-ttu-id="213f1-116">在目前版本 2.3 hello，hello 資料包括：</span><span class="sxs-lookup"><span data-stu-id="213f1-116">In hello current version 2.3, hello data includes:</span></span>

* <span data-ttu-id="213f1-117">所有 Linux Rsyslog 記錄檔，包括系統、安全性及應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="213f1-117">All Linux Rsyslog logs, including system, security, and application logs.</span></span>
* <span data-ttu-id="213f1-118">所有的系統資料上所指定[hello System Center 跨平台解決方案網站](https://scx.codeplex.com/wikipage?title=xplatproviders)。</span><span class="sxs-lookup"><span data-stu-id="213f1-118">All system data that's specified on [hello System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
* <span data-ttu-id="213f1-119">使用者指定的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="213f1-119">User-specified log files.</span></span>

<span data-ttu-id="213f1-120">這項擴充功能的運作方式與傳統的 hello 和資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="213f1-120">This extension works with both hello classic and Resource Manager deployment models.</span></span>

### <a name="current-version-of-hello-extension-and-deprecation-of-old-versions"></a><span data-ttu-id="213f1-121">新版的 hello 擴充功能和已被取代的舊版本</span><span class="sxs-lookup"><span data-stu-id="213f1-121">Current version of hello extension and deprecation of old versions</span></span>

<span data-ttu-id="213f1-122">hello hello 延伸模組的最新版本是**2.3**，和**會取代任何舊版本 （2.0、 2.1 和 2.2），而且未發行的本年度 (2017) 結束**。</span><span class="sxs-lookup"><span data-stu-id="213f1-122">hello latest version of hello extension is **2.3**, and **any old versions (2.0, 2.1, and 2.2) will be deprecated and unpublished by end of this year (2017)**.</span></span> <span data-ttu-id="213f1-123">如果您停用自動次要版本升級安裝 hello Linux 診斷延伸模組，強烈建議您解除安裝 hello 擴充功能，並重新安裝已啟用自動的次要版本升級。</span><span class="sxs-lookup"><span data-stu-id="213f1-123">If you installed hello Linux Diagnostic extension with automatic minor version upgrade disabled, it's strongly recommended that you uninstall hello extension and reinstall it with automatic minor version upgrade enabled.</span></span> <span data-ttu-id="213f1-124">在傳統 (ASM) Vm，您可以達到這個目的藉由指定 '2.*' hello 版本，如果您要安裝 hello 延伸模組，透過 Azure XPLAT CLI 或 Powershell。</span><span class="sxs-lookup"><span data-stu-id="213f1-124">On classic (ASM) VMs, you can achieve this by specifying '2.*' as hello version if you are installing hello extension through Azure XPLAT CLI or Powershell.</span></span> <span data-ttu-id="213f1-125">在 ARM Vm 上您可以達到這包括 '"autoUpgradeMinorVersion": true' hello VM 部署範本中。</span><span class="sxs-lookup"><span data-stu-id="213f1-125">On ARM VMs, you can achieve this by including '"autoUpgradeMinorVersion": true' in hello VM deployment template.</span></span> <span data-ttu-id="213f1-126">此外，hello 延伸模組的任何新的安裝應有 hello 自動次要版本升級已開啟選項。</span><span class="sxs-lookup"><span data-stu-id="213f1-126">Also, any new installation of hello extension should have hello auto minor version upgrade option turned on.</span></span>

## <a name="enable-hello-extension"></a><span data-ttu-id="213f1-127">啟用 hello 擴充功能</span><span class="sxs-lookup"><span data-stu-id="213f1-127">Enable hello extension</span></span>

<span data-ttu-id="213f1-128">您可以啟用此延伸模組使用 hello [Azure 入口網站](https://portal.azure.com/#)，Azure PowerShell 或 Azure CLI 指令碼。</span><span class="sxs-lookup"><span data-stu-id="213f1-128">You can enable this extension by using hello [Azure portal](https://portal.azure.com/#), Azure PowerShell, or Azure CLI scripts.</span></span>

<span data-ttu-id="213f1-129">tooview 並設定 hello 系統的效能資料直接從 hello Azure 入口網站，請遵循[hello Azure 部落格上的這些步驟](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/)。</span><span class="sxs-lookup"><span data-stu-id="213f1-129">tooview and configure hello system and performance data directly from hello Azure portal, follow [these steps on hello Azure blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span></span>

<span data-ttu-id="213f1-130">本文著重在如何 tooenable 和使用 Azure CLI 命令設定 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="213f1-130">This article focuses on how tooenable and configure hello extension by using Azure CLI commands.</span></span> <span data-ttu-id="213f1-131">這可讓您直接從 hello 儲存體資料表的 tooread 並檢視 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="213f1-131">This allows you tooread and view hello data directly from hello storage table.</span></span>

<span data-ttu-id="213f1-132">請注意，此處所述的 hello 組態方法不適用於 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="213f1-132">Note that hello configuration methods that are described here won't work for hello Azure portal.</span></span> <span data-ttu-id="213f1-133">tooview 和設定 hello 系統和效能資料，直接從 hello Azure 入口網站中，必須透過 hello 入口網站啟用 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="213f1-133">tooview and configure hello system and performance data directly from hello Azure portal, hello extension must be enabled through hello portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="213f1-134">必要條件</span><span class="sxs-lookup"><span data-stu-id="213f1-134">Prerequisites</span></span>

* <span data-ttu-id="213f1-135">**Azure Linux Agent 2.0.6 版或更新版本**。</span><span class="sxs-lookup"><span data-stu-id="213f1-135">**Azure Linux Agent version 2.0.6 or later**.</span></span>

  <span data-ttu-id="213f1-136">請注意，大部分的 Azure VM Linux 資源庫映像包含版本 2.0.6 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="213f1-136">Note that most Azure VM Linux gallery images include version 2.0.6 or later.</span></span> <span data-ttu-id="213f1-137">您可以執行**WAAgent-版本**tooconfirm hello VM 所安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="213f1-137">You can run **WAAgent -version** tooconfirm which version is installed on hello VM.</span></span> <span data-ttu-id="213f1-138">如果 hello VM 執行早於 2.0.6 版本，您可以依照[這些指示在 GitHub 上的](https://github.com/Azure/WALinuxAgent "指示")tooupdate 它。</span><span class="sxs-lookup"><span data-stu-id="213f1-138">If hello VM is running a version that's earlier than 2.0.6, you can follow [these instructions on GitHub](https://github.com/Azure/WALinuxAgent "instructions") tooupdate it.</span></span>
* <span data-ttu-id="213f1-139">**Azure CLI**。</span><span class="sxs-lookup"><span data-stu-id="213f1-139">**Azure CLI**.</span></span> <span data-ttu-id="213f1-140">請遵循[本指南中的有關安裝 CLI](../../../cli-install-nodejs.md) tooset hello Azure CLI 環境，您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="213f1-140">Follow [this guidance for installing CLI](../../../cli-install-nodejs.md) tooset up hello Azure CLI environment on your machine.</span></span> <span data-ttu-id="213f1-141">安裝 Azure CLI 之後，您可以使用 hello **azure**命令從命令列介面 （Bash、 終端機或命令提示字元） tooaccess hello Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="213f1-141">After Azure CLI is installed, you can use hello **azure** command from your command-line interface (Bash, Terminal, or command prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="213f1-142">例如：</span><span class="sxs-lookup"><span data-stu-id="213f1-142">For example:</span></span>

  * <span data-ttu-id="213f1-143">執行 **azure vm extension set --help** 取得詳細的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="213f1-143">Run **azure vm extension set --help** for detailed help information.</span></span>
  * <span data-ttu-id="213f1-144">執行**azure 登入**toosign tooAzure 中的。</span><span class="sxs-lookup"><span data-stu-id="213f1-144">Run **azure login** toosign in tooAzure.</span></span>
  * <span data-ttu-id="213f1-145">執行**azure vm 清單**toolist 所有 hello 您尚未在 Azure 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="213f1-145">Run **azure vm list** toolist all hello virtual machines that you have on Azure.</span></span>
* <span data-ttu-id="213f1-146">儲存體帳戶 toostore hello 資料。</span><span class="sxs-lookup"><span data-stu-id="213f1-146">A storage account toostore hello data.</span></span> <span data-ttu-id="213f1-147">您必須是先前所建立的儲存體帳戶名稱和存取金鑰 tooupload hello 資料 tooyour 存放裝置。</span><span class="sxs-lookup"><span data-stu-id="213f1-147">You will need a storage account name that was created previously and an access key tooupload hello data tooyour storage.</span></span>

## <a name="use-hello-azure-cli-command-tooenable-hello-linux-diagnostic-extension"></a><span data-ttu-id="213f1-148">使用 hello Azure CLI 命令 tooenable hello Linux 診斷延伸模組</span><span class="sxs-lookup"><span data-stu-id="213f1-148">Use hello Azure CLI command tooenable hello Linux Diagnostic Extension</span></span>

### <a name="scenario-1-enable-hello-extension-with-hello-default-data-set"></a><span data-ttu-id="213f1-149">案例 1.</span><span class="sxs-lookup"><span data-stu-id="213f1-149">Scenario 1.</span></span> <span data-ttu-id="213f1-150">啟用 hello 與 hello 預設資料集的延伸模組</span><span class="sxs-lookup"><span data-stu-id="213f1-150">Enable hello extension with hello default data set</span></span>

<span data-ttu-id="213f1-151">在版本 2.3 或更新版本中，將收集的 hello 預設資料包括：</span><span class="sxs-lookup"><span data-stu-id="213f1-151">In version 2.3 or later, hello default data that will be collected includes:</span></span>

* <span data-ttu-id="213f1-152">所有 Rsyslog 資訊 (包括系統、安全性及應用程式記錄檔)。</span><span class="sxs-lookup"><span data-stu-id="213f1-152">All Rsyslog information (including system, security, and application logs).</span></span>  
* <span data-ttu-id="213f1-153">一組核心基礎系統資料。</span><span class="sxs-lookup"><span data-stu-id="213f1-153">A core set of basis system data.</span></span> <span data-ttu-id="213f1-154">請注意 hello 完整資料集，會說明 hello [System Center 跨平台解決方案網站](https://scx.codeplex.com/wikipage?title=xplatproviders)。</span><span class="sxs-lookup"><span data-stu-id="213f1-154">Note that hello full data set is described on hello [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
  <span data-ttu-id="213f1-155">如果您想 tooenable 額外的資料，繼續在案例 2 和 3 中的 hello 執行步驟。</span><span class="sxs-lookup"><span data-stu-id="213f1-155">If you want tooenable extra data, continue with hello steps in Scenarios 2 and 3.</span></span>

<span data-ttu-id="213f1-156">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="213f1-156">Step 1.</span></span> <span data-ttu-id="213f1-157">建立名為 privateconfig.json 的檔案以 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="213f1-157">Create a file named PrivateConfig.json with hello following content:</span></span>

    {
        "storageAccountName" : "hello storage account tooreceive data",
        "storageAccountKey" : "hello key of hello account"
    }

<span data-ttu-id="213f1-158">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="213f1-158">Step 2.</span></span> <span data-ttu-id="213f1-159">執行 **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**。</span><span class="sxs-lookup"><span data-stu-id="213f1-159">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.</span></span>

### <a name="scenario-2-customize-hello-performance-monitor-metrics"></a><span data-ttu-id="213f1-160">案例 2.</span><span class="sxs-lookup"><span data-stu-id="213f1-160">Scenario 2.</span></span> <span data-ttu-id="213f1-161">自訂 hello 效能監視度量</span><span class="sxs-lookup"><span data-stu-id="213f1-161">Customize hello performance monitor metrics</span></span>

<span data-ttu-id="213f1-162">本章節描述如何 toocustomize hello 效能和診斷資料的資料表。</span><span class="sxs-lookup"><span data-stu-id="213f1-162">This section describes how toocustomize hello performance and diagnostic data table.</span></span>

<span data-ttu-id="213f1-163">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="213f1-163">Step 1.</span></span> <span data-ttu-id="213f1-164">建立名為 privateconfig.json 的檔案，以案例 1 所述的 hello 內容的檔案。</span><span class="sxs-lookup"><span data-stu-id="213f1-164">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="213f1-165">同時也建立名為 PublicConfig.json 的檔案。</span><span class="sxs-lookup"><span data-stu-id="213f1-165">Also create a file named PublicConfig.json.</span></span> <span data-ttu-id="213f1-166">指定您想要 toocollect hello 特定資料。</span><span class="sxs-lookup"><span data-stu-id="213f1-166">Specify hello particular data you want toocollect.</span></span>

<span data-ttu-id="213f1-167">所有支援的提供者和變數，參考 hello [System Center 跨平台解決方案網站](https://scx.codeplex.com/wikipage?title=xplatproviders)。</span><span class="sxs-lookup"><span data-stu-id="213f1-167">For all supported providers and variables, reference hello [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span> <span data-ttu-id="213f1-168">您可以擁有多個查詢，並將其儲存在多個資料表中，藉由附加多個查詢 toohello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="213f1-168">You can have multiple queries and store them in multiple tables by appending more queries toohello script.</span></span>

<span data-ttu-id="213f1-169">根據預設，永遠都會收集 hello Rsyslog 資料。</span><span class="sxs-lookup"><span data-stu-id="213f1-169">By default, hello Rsyslog data is always collected.</span></span>

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


<span data-ttu-id="213f1-170">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="213f1-170">Step 2.</span></span> <span data-ttu-id="213f1-171">執行 **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**。</span><span class="sxs-lookup"><span data-stu-id="213f1-171">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

### <a name="scenario-3-upload-your-own-log-files"></a><span data-ttu-id="213f1-172">案例 3.</span><span class="sxs-lookup"><span data-stu-id="213f1-172">Scenario 3.</span></span> <span data-ttu-id="213f1-173">上傳您自己的記錄檔</span><span class="sxs-lookup"><span data-stu-id="213f1-173">Upload your own log files</span></span>

<span data-ttu-id="213f1-174">本章節描述如何 toocollect 和上傳的特定記錄檔檔案 tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="213f1-174">This section describes how toocollect and upload specific log files tooyour storage account.</span></span> <span data-ttu-id="213f1-175">您需要 toospecify 這兩個 hello 路徑 tooyour 記錄檔案和 hello 名稱 hello 資料表所在 toostore 您的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="213f1-175">You need toospecify both hello path tooyour log file and hello name of hello table where you want toostore your log.</span></span> <span data-ttu-id="213f1-176">您可以加入多個檔案/資料表項目 toohello 指令碼，以建立多個記錄檔。</span><span class="sxs-lookup"><span data-stu-id="213f1-176">You can create multiple log files by adding multiple file/table entries toohello script.</span></span>

<span data-ttu-id="213f1-177">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="213f1-177">Step 1.</span></span> <span data-ttu-id="213f1-178">建立名為 privateconfig.json 的檔案，以案例 1 所述的 hello 內容的檔案。</span><span class="sxs-lookup"><span data-stu-id="213f1-178">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="213f1-179">然後建立名為 PublicConfig.json hello 下列的其他檔案內容：</span><span class="sxs-lookup"><span data-stu-id="213f1-179">Then create another file named PublicConfig.json with hello following content:</span></span>

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

<span data-ttu-id="213f1-180">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="213f1-180">Step 2.</span></span> <span data-ttu-id="213f1-181">執行 `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`。</span><span class="sxs-lookup"><span data-stu-id="213f1-181">Run `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span></span>

<span data-ttu-id="213f1-182">請注意，這項設定在擴充功能版本先前 too2.3 hello，所有的記錄寫入太`/var/log/mysql.err`太可能會重複`/var/log/syslog`(或`/var/log/messages`根據 hello Linux distro) 以及。</span><span class="sxs-lookup"><span data-stu-id="213f1-182">Note that with this setting on hello extension versions prior too2.3, all logs written too`/var/log/mysql.err` might be duplicated too`/var/log/syslog` (or `/var/log/messages` depending on hello Linux distro) as well.</span></span> <span data-ttu-id="213f1-183">如果您想要 tooavoid 記錄此複本，您可以排除記錄`local6`記錄 rsyslog 組態中的功能。</span><span class="sxs-lookup"><span data-stu-id="213f1-183">If you'd like tooavoid this duplicate logging, you can exclude logging of `local6` facility logs in your rsyslog configuration.</span></span> <span data-ttu-id="213f1-184">它相依於 hello Linux distro 中，但在 Ubuntu 14.04 系統上，hello 檔案 toomodify`/etc/rsyslog.d/50-default.conf`而且您可以取代 hello 列`*.*;auth,authpriv.none -/var/log/syslog`太`*.*;auth,authpriv,local6.none -/var/log/syslog`。</span><span class="sxs-lookup"><span data-stu-id="213f1-184">It depends on hello Linux distro, but on an Ubuntu 14.04 system, hello file toomodify is `/etc/rsyslog.d/50-default.conf` and you can replace hello line `*.*;auth,authpriv.none -/var/log/syslog` too`*.*;auth,authpriv,local6.none -/var/log/syslog`.</span></span> <span data-ttu-id="213f1-185">已修正此問題在 hello 最新 hotfix 版本的 2.3 (2.3.9007)，因此如果您擁有 hello 擴充功能版本 2.3，應該不會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="213f1-185">This issue is fixed in hello latest hotfix release of 2.3 (2.3.9007), so if you have hello extension version 2.3, this issue should not happen.</span></span> <span data-ttu-id="213f1-186">如果仍有即使之後重新啟動您的 VM，請與我們連絡，並協助我們進行疑難排解，hello 最新的 hotfix 版本不會自動安裝。</span><span class="sxs-lookup"><span data-stu-id="213f1-186">If it still does even after restarting your VM, please contact us and help us troubleshoot why hello latest hotfix version is not installed automatically.</span></span>

### <a name="scenario-4-stop-hello-extension-from-collecting-any-logs"></a><span data-ttu-id="213f1-187">案例 4.</span><span class="sxs-lookup"><span data-stu-id="213f1-187">Scenario 4.</span></span> <span data-ttu-id="213f1-188">停止收集任何記錄檔的 hello 延伸模組</span><span class="sxs-lookup"><span data-stu-id="213f1-188">Stop hello extension from collecting any logs</span></span>

<span data-ttu-id="213f1-189">本章節描述 toostop hello 延伸模組，從收集的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="213f1-189">This section describes how toostop hello extension from collecting logs.</span></span> <span data-ttu-id="213f1-190">即使使用本次將仍會啟動並執行 hello 監視代理程式處理序的附註。</span><span class="sxs-lookup"><span data-stu-id="213f1-190">Note that hello monitoring agent process will be still up and running even with this reconfiguration.</span></span> <span data-ttu-id="213f1-191">如果您想要 toostop hello 完全監視代理程式處理序，您可以藉由停用 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="213f1-191">If you'd like toostop hello monitoring agent process completely, you can do so by disabling hello extension.</span></span> <span data-ttu-id="213f1-192">hello 命令 toodisable hello 延伸模組是`azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`。</span><span class="sxs-lookup"><span data-stu-id="213f1-192">hello command toodisable hello extension is `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span></span>

<span data-ttu-id="213f1-193">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="213f1-193">Step 1.</span></span> <span data-ttu-id="213f1-194">建立名為 privateconfig.json 的檔案，以案例 1 所述的 hello 內容的檔案。</span><span class="sxs-lookup"><span data-stu-id="213f1-194">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="213f1-195">建立名為 hello 遵循 PublicConfig.json 的另一個檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="213f1-195">Create another file named PublicConfig.json with hello following content:</span></span>

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


<span data-ttu-id="213f1-196">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="213f1-196">Step 2.</span></span> <span data-ttu-id="213f1-197">執行 **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**。</span><span class="sxs-lookup"><span data-stu-id="213f1-197">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

## <a name="review-your-data"></a><span data-ttu-id="213f1-198">檢閱資料</span><span class="sxs-lookup"><span data-stu-id="213f1-198">Review your data</span></span>

<span data-ttu-id="213f1-199">hello 效能和診斷資料會儲存在 Azure 儲存體資料表中。</span><span class="sxs-lookup"><span data-stu-id="213f1-199">hello performance and diagnostic data are stored in an Azure Storage table.</span></span> <span data-ttu-id="213f1-200">檢閱[如何 toouse 從 Ruby 的 Azure 資料表儲存體](../../../cosmos-db/table-storage-how-to-use-ruby.md)toolearn tooaccess hello 儲存體中的 hello 資料資料表使用 Azure CLI 指令碼的方式。</span><span class="sxs-lookup"><span data-stu-id="213f1-200">Review [How toouse Azure Table Storage from Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn how tooaccess hello data in hello storage table by using Azure CLI scripts.</span></span>

<span data-ttu-id="213f1-201">此外，您可以使用下列 UI 工具 tooaccess hello 資料：</span><span class="sxs-lookup"><span data-stu-id="213f1-201">In addition, you can use following UI tools tooaccess hello data:</span></span>

1. <span data-ttu-id="213f1-202">Visual Studio 伺服器總管。</span><span class="sxs-lookup"><span data-stu-id="213f1-202">Visual Studio Server Explorer.</span></span> <span data-ttu-id="213f1-203">移 tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="213f1-203">Go tooyour storage account.</span></span> <span data-ttu-id="213f1-204">Hello VM 執行大約五分鐘之後，您會看到 hello 四個預設資料表:"LinuxCpu"、"LinuxDisk"、"LinuxMemory 」 和 「 Linuxsyslog"。</span><span class="sxs-lookup"><span data-stu-id="213f1-204">After hello VM runs for about five minutes, you'll see hello four default tables: “LinuxCpu”, ”LinuxDisk”, ”LinuxMemory”, and ”Linuxsyslog”.</span></span> <span data-ttu-id="213f1-205">按兩下 hello 資料表名稱 tooview hello 資料。</span><span class="sxs-lookup"><span data-stu-id="213f1-205">Double-click hello table names tooview hello data.</span></span>
1. <span data-ttu-id="213f1-206">[Azure 儲存體總管](https://azurestorageexplorer.codeplex.com/ "Azure 儲存體總管")。</span><span class="sxs-lookup"><span data-stu-id="213f1-206">[Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

![image](./media/diagnostic-extension/no1.png)

<span data-ttu-id="213f1-208">如果您已啟用 fileCfg 或 perfCfg （如案例 2 和 3 所述），您可以使用 Visual Studio 伺服器總管和 Azure 儲存體總管 tooview 非預設的資料。</span><span class="sxs-lookup"><span data-stu-id="213f1-208">If you've enabled fileCfg or perfCfg (as described in Scenarios 2 and 3), you can use Visual Studio Server Explorer and Azure Storage Explorer tooview non-default data.</span></span>

## <a name="known-issues"></a><span data-ttu-id="213f1-209">已知問題</span><span class="sxs-lookup"><span data-stu-id="213f1-209">Known issues</span></span>

* <span data-ttu-id="213f1-210">hello Rsyslog 資訊和客戶指定記錄檔只可透過指令碼存取。</span><span class="sxs-lookup"><span data-stu-id="213f1-210">hello Rsyslog information and customer-specified log file can only be accessed via scripting.</span></span>
