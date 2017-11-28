---
title: "計算 aaaAzure-Linux 診斷延伸模組 |Microsoft 文件"
description: "如何 tooconfigure hello Azure Linux 診斷延伸模組 （年輕人） toocollect 度量，並記錄在 Azure 中執行的 Linux Vm 所傳來的事件。"
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a><span data-ttu-id="101ec-103">使用 Linux 診斷延伸模組 toomonitor 度量和記錄檔</span><span class="sxs-lookup"><span data-stu-id="101ec-103">Use Linux Diagnostic Extension toomonitor metrics and logs</span></span>

<span data-ttu-id="101ec-104">本文件描述版本 3.0 和較新的 hello Linux 診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="101ec-104">This document describes version 3.0 and newer of hello Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="101ec-105">如需 2.3 版與更舊版本的資訊，請參閱[本文件](./classic/diagnostic-extension-v2.md)。</span><span class="sxs-lookup"><span data-stu-id="101ec-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="101ec-106">簡介</span><span class="sxs-lookup"><span data-stu-id="101ec-106">Introduction</span></span>

<span data-ttu-id="101ec-107">hello Linux 診斷延伸模組可協助 Microsoft Azure 上執行的 Linux VM 的 hello 使用者監視健全狀況。</span><span class="sxs-lookup"><span data-stu-id="101ec-107">hello Linux Diagnostic Extension helps a user monitor hello health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="101ec-108">它有下列功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="101ec-108">It has hello following capabilities:</span></span>

* <span data-ttu-id="101ec-109">會收集從 hello VM 的系統效能度量，並將它們儲存在指定的儲存體帳戶中的特定資料表中。</span><span class="sxs-lookup"><span data-stu-id="101ec-109">Collects system performance metrics from hello VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="101ec-110">擷取記錄事件從 syslog，並將它們儲存在指定的儲存體帳戶的 hello 中特定資料表。</span><span class="sxs-lookup"><span data-stu-id="101ec-110">Retrieves log events from syslog and stores them in a specific table in hello designated storage account.</span></span>
* <span data-ttu-id="101ec-111">可讓使用者 toocustomize hello 資料計量所收集和上傳。</span><span class="sxs-lookup"><span data-stu-id="101ec-111">Enables users toocustomize hello data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="101ec-112">可讓使用者 toocustomize hello syslog 設備與嚴重性層級的事件所收集和上傳。</span><span class="sxs-lookup"><span data-stu-id="101ec-112">Enables users toocustomize hello syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="101ec-113">可讓使用者 tooupload 指定的記錄檔 tooa 指定之儲存體資料表。</span><span class="sxs-lookup"><span data-stu-id="101ec-113">Enables users tooupload specified log files tooa designated storage table.</span></span>
* <span data-ttu-id="101ec-114">支援傳送嗨度量和記錄檔事件 tooarbitrary EventHub 端點和 JSON 格式的 blob 指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="101ec-114">Supports sending metrics and log events tooarbitrary EventHub endpoints and JSON-formatted blobs in hello designated storage account.</span></span>

<span data-ttu-id="101ec-115">此擴充功能適用於這兩個 Azure 部署模型。</span><span class="sxs-lookup"><span data-stu-id="101ec-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-hello-extension-in-your-vm"></a><span data-ttu-id="101ec-116">安裝在 VM 中的 hello 擴充功能</span><span class="sxs-lookup"><span data-stu-id="101ec-116">Installing hello extension in your VM</span></span>

<span data-ttu-id="101ec-117">您可以使用 hello Azure PowerShell cmdlet、 Azure CLI 指令碼或 Azure 的部署範本，以啟用這項擴充功能。</span><span class="sxs-lookup"><span data-stu-id="101ec-117">You can enable this extension by using hello Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="101ec-118">如需詳細資訊，請參閱[擴充功能](./extensions-features.md)。</span><span class="sxs-lookup"><span data-stu-id="101ec-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="101ec-119">hello Azure 入口網站無法使用的 tooenable 或設定年輕人 3.0。</span><span class="sxs-lookup"><span data-stu-id="101ec-119">hello Azure portal cannot be used tooenable or configure LAD 3.0.</span></span> <span data-ttu-id="101ec-120">相反地，它會安裝並設定 2.3 版。</span><span class="sxs-lookup"><span data-stu-id="101ec-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="101ec-121">Azure 入口網站的圖形和警示處理 hello 延伸模組的兩個版本的資料。</span><span class="sxs-lookup"><span data-stu-id="101ec-121">Azure portal graphs and alerts work with data from both versions of hello extension.</span></span>

<span data-ttu-id="101ec-122">這些安裝指示與[可下載範例組態](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json)可設定 LAD 3.0 以：</span><span class="sxs-lookup"><span data-stu-id="101ec-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="101ec-123">擷取和儲存 hello 相同度量資訊是年輕人 2.3; 所提供</span><span class="sxs-lookup"><span data-stu-id="101ec-123">capture and store hello same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="101ec-124">擷取檔案系統度量，新 tooLAD 3.0; 有用設</span><span class="sxs-lookup"><span data-stu-id="101ec-124">capture a useful set of file system metrics, new tooLAD 3.0;</span></span>
* <span data-ttu-id="101ec-125">擷取 hello 預設 syslog 集合啟用年輕人 2.3;</span><span class="sxs-lookup"><span data-stu-id="101ec-125">capture hello default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="101ec-126">啟用 hello 圖表和 VM 度量的警示的 Azure 入口網站體驗。</span><span class="sxs-lookup"><span data-stu-id="101ec-126">enable hello Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="101ec-127">hello 可下載組態只是一個範例。修改 toosuit 您自己的需求。</span><span class="sxs-lookup"><span data-stu-id="101ec-127">hello downloadable configuration is just an example; modify it toosuit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="101ec-128">必要條件</span><span class="sxs-lookup"><span data-stu-id="101ec-128">Prerequisites</span></span>

* <span data-ttu-id="101ec-129">**Azure Linux Agent 2.2.0 版或更新版本**。</span><span class="sxs-lookup"><span data-stu-id="101ec-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="101ec-130">大部分的 Azure VM Linux 資源庫映像包含版本 2.2.7 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="101ec-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="101ec-131">執行`/usr/sbin/waagent -version`hello VM 上安裝的 tooconfirm hello 版本。</span><span class="sxs-lookup"><span data-stu-id="101ec-131">Run `/usr/sbin/waagent -version` tooconfirm hello version installed on hello VM.</span></span> <span data-ttu-id="101ec-132">如果 hello VM 正在執行較舊版本的 hello 客體代理程式，請遵循[這些指示](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent)tooupdate 它。</span><span class="sxs-lookup"><span data-stu-id="101ec-132">If hello VM is running an older version of hello guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate it.</span></span>
* <span data-ttu-id="101ec-133">**Azure CLI**。</span><span class="sxs-lookup"><span data-stu-id="101ec-133">**Azure CLI**.</span></span> <span data-ttu-id="101ec-134">[設定 hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)您的電腦上的環境。</span><span class="sxs-lookup"><span data-stu-id="101ec-134">[Set up hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="101ec-135">如果您沒有 hello wget 命令： 執行`sudo apt-get install wget`。</span><span class="sxs-lookup"><span data-stu-id="101ec-135">hello wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="101ec-136">現有的 Azure 訂用帳戶和現有的儲存體帳戶內 toostore hello 資料。</span><span class="sxs-lookup"><span data-stu-id="101ec-136">An existing Azure subscription and an existing storage account within it toostore hello data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="101ec-137">範例安裝</span><span class="sxs-lookup"><span data-stu-id="101ec-137">Sample installation</span></span>

<span data-ttu-id="101ec-138">填寫 hello hello 上正確的參數前三行，然後執行此指令碼為根：</span><span class="sxs-lookup"><span data-stu-id="101ec-138">Fill in hello correct parameters on hello first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="101ec-139">hello hello 範例組態中，URL 和它的內容，是主體 toochange。</span><span class="sxs-lookup"><span data-stu-id="101ec-139">hello URL for hello sample configuration, and its contents, are subject toochange.</span></span> <span data-ttu-id="101ec-140">下載 hello 入口網站設定 JSON 檔案的副本，並針對您的需求加以自訂。</span><span class="sxs-lookup"><span data-stu-id="101ec-140">Download a copy of hello portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="101ec-141">您建構的任何範本或自動化項目應使用您自己的複本，而非每次都要下載該 URL。</span><span class="sxs-lookup"><span data-stu-id="101ec-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-hello-extension-settings"></a><span data-ttu-id="101ec-142">更新 hello 延伸模組設定</span><span class="sxs-lookup"><span data-stu-id="101ec-142">Updating hello extension settings</span></span>

<span data-ttu-id="101ec-143">您已變更您的受保護或公用設定之後，將其部署 toohello VM 執行 hello 相同的命令。</span><span class="sxs-lookup"><span data-stu-id="101ec-143">After you've changed your Protected or Public settings, deploy them toohello VM by running hello same command.</span></span> <span data-ttu-id="101ec-144">如果任何項目在 hello 設定進行變更，hello 更新設定傳送 toohello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="101ec-144">If anything changed in hello settings, hello updated settings are sent toohello extension.</span></span> <span data-ttu-id="101ec-145">年輕人重新載入 hello 組態，並自行重新啟動。</span><span class="sxs-lookup"><span data-stu-id="101ec-145">LAD reloads hello configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-hello-extension"></a><span data-ttu-id="101ec-146">從舊版的 hello 延伸模組的移轉</span><span class="sxs-lookup"><span data-stu-id="101ec-146">Migration from previous versions of hello extension</span></span>

<span data-ttu-id="101ec-147">hello hello 延伸模組的最新版本是**3.0**。</span><span class="sxs-lookup"><span data-stu-id="101ec-147">hello latest version of hello extension is **3.0**.</span></span> <span data-ttu-id="101ec-148">**任何舊版 (2.x) 皆已被取代，並會 2018 年 7 月 31 日停止發行**。</span><span class="sxs-lookup"><span data-stu-id="101ec-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="101ec-149">這項擴充功能引進 hello 擴充的重大變更 toohello 組態。</span><span class="sxs-lookup"><span data-stu-id="101ec-149">This extension introduces breaking changes toohello configuration of hello extension.</span></span> <span data-ttu-id="101ec-150">一個這類變更 tooimprove hello 安全性 hello 延伸模組。如此一來，回溯相容性 2.x 可能不會保留。</span><span class="sxs-lookup"><span data-stu-id="101ec-150">One such change was made tooimprove hello security of hello extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="101ec-151">此外，hello 擴充功能發行者針對此延伸模組是與 hello 2.x 版的 hello 發行者不同。</span><span class="sxs-lookup"><span data-stu-id="101ec-151">Also, hello Extension Publisher for this extension is different than hello publisher for hello 2.x versions.</span></span>
>
> <span data-ttu-id="101ec-152">toomigrate 從 2.x toothis 新版 hello 擴充功能，您必須先解除安裝 hello 舊擴充功能 （在 hello 舊發行者的名稱），然後安裝第 3 版的 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="101ec-152">toomigrate from 2.x toothis new version of hello extension, you must uninstall hello old extension (under hello old publisher name), then install version 3 of hello extension.</span></span>

<span data-ttu-id="101ec-153">建議：</span><span class="sxs-lookup"><span data-stu-id="101ec-153">Recommendations:</span></span>

* <span data-ttu-id="101ec-154">安裝 hello 擴充功能啟用自動的次要版本升級。</span><span class="sxs-lookup"><span data-stu-id="101ec-154">Install hello extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="101ec-155">在傳統部署模型的 Vm，指定 '3.*' hello 版本，如果您要安裝 hello 延伸模組，透過 Azure XPLAT CLI 或 Powershell。</span><span class="sxs-lookup"><span data-stu-id="101ec-155">On classic deployment model VMs, specify '3.*' as hello version if you are installing hello extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="101ec-156">Azure Resource Manager 部署模型的 Vm，包括 '"autoUpgradeMinorVersion": true' hello VM 部署範本中。</span><span class="sxs-lookup"><span data-stu-id="101ec-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in hello VM deployment template.</span></span>
* <span data-ttu-id="101ec-157">為 LAD 3.0 使用新/不同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="101ec-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="101ec-158">LAD 2.3 與 LAD 3.0 之間些許不相容，讓共用帳戶變得麻煩：</span><span class="sxs-lookup"><span data-stu-id="101ec-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="101ec-159">LAD 3.0 會將 Syslog 事件儲存在採用不同名稱的資料表中。</span><span class="sxs-lookup"><span data-stu-id="101ec-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="101ec-160">字串 hello counterSpecifier`builtin`年輕人 3.0 在不同的度量。</span><span class="sxs-lookup"><span data-stu-id="101ec-160">hello counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="101ec-161">受保護的設定</span><span class="sxs-lookup"><span data-stu-id="101ec-161">Protected settings</span></span>

<span data-ttu-id="101ec-162">這一組的組態資訊包含敏感性資訊，應加以保護以防遭公開檢視，例如儲存體認證。</span><span class="sxs-lookup"><span data-stu-id="101ec-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="101ec-163">這些設定是傳輸的 tooand hello 延伸模組，以加密形式儲存。</span><span class="sxs-lookup"><span data-stu-id="101ec-163">These settings are transmitted tooand stored by hello extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="101ec-164">名稱</span><span class="sxs-lookup"><span data-stu-id="101ec-164">Name</span></span> | <span data-ttu-id="101ec-165">值</span><span class="sxs-lookup"><span data-stu-id="101ec-165">Value</span></span>
---- | -----
<span data-ttu-id="101ec-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="101ec-166">storageAccountName</span></span> | <span data-ttu-id="101ec-167">hello 資料寫入 hello 延伸模組的 hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="101ec-167">hello name of hello storage account in which data is written by hello extension.</span></span>
<span data-ttu-id="101ec-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="101ec-168">storageAccountEndPoint</span></span> | <span data-ttu-id="101ec-169">（選擇性） hello 端點識別 hello 雲端中的 hello 儲存體帳戶存在。</span><span class="sxs-lookup"><span data-stu-id="101ec-169">(optional) hello endpoint identifying hello cloud in which hello storage account exists.</span></span> <span data-ttu-id="101ec-170">如果此設定不存在，年輕人預設 toohello Azure 公用雲端， `https://core.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="101ec-170">If this setting is absent, LAD defaults toohello Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="101ec-171">儲存體帳戶在 Azure 德國、 Azure 政府或 Azure China toouse 據以設定此值。</span><span class="sxs-lookup"><span data-stu-id="101ec-171">toouse a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="101ec-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="101ec-172">storageAccountSasToken</span></span> | <span data-ttu-id="101ec-173">[帳戶 SAS 權杖](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/)Blob 和表格服務 (`ss='bt'`)，適用於 toocontainers 和物件 (`srt='co'`)、 哪些授與新增，請建立、 列出、 更新和寫入權限 (`sp='acluw'`)。</span><span class="sxs-lookup"><span data-stu-id="101ec-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable toocontainers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="101ec-174">請勿*不*包含 hello 前置問號 （？）。</span><span class="sxs-lookup"><span data-stu-id="101ec-174">Do *not* include hello leading question-mark (?).</span></span>
<span data-ttu-id="101ec-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="101ec-175">mdsdHttpProxy</span></span> | <span data-ttu-id="101ec-176">（選擇性）HTTP proxy 所需的資訊 tooenable hello 延伸 tooconnect toohello 指定儲存體帳戶及端點。</span><span class="sxs-lookup"><span data-stu-id="101ec-176">(optional) HTTP proxy information needed tooenable hello extension tooconnect toohello specified storage account and endpoint.</span></span>
<span data-ttu-id="101ec-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="101ec-177">sinksConfig</span></span> | <span data-ttu-id="101ec-178">（選擇性）可以傳遞替代目的地 toowhich 計量和事件的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="101ec-178">(optional) Details of alternative destinations toowhich metrics and events can be delivered.</span></span> <span data-ttu-id="101ec-179">hello 以下各節會說明 hello 的 hello 延伸模組支援每個資料接收的特定詳細資料。</span><span class="sxs-lookup"><span data-stu-id="101ec-179">hello specific details of each data sink supported by hello extension are covered in hello sections that follow.</span></span>

<span data-ttu-id="101ec-180">您可以輕鬆地建構透過 hello Azure 入口網站的所需的 hello SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="101ec-180">You can easily construct hello required SAS token through hello Azure portal.</span></span>

1. <span data-ttu-id="101ec-181">選取您想要 hello 延伸 toowrite hello 一般用途儲存體帳戶 toowhich</span><span class="sxs-lookup"><span data-stu-id="101ec-181">Select hello general-purpose storage account toowhich you want hello extension toowrite</span></span>
1. <span data-ttu-id="101ec-182">選取從 hello 設定部分 hello 左側功能表的 [共用存取簽章]</span><span class="sxs-lookup"><span data-stu-id="101ec-182">Select "Shared access signature" from hello Settings part of hello left menu</span></span>
1. <span data-ttu-id="101ec-183">請如先前所述的 hello 適當章節</span><span class="sxs-lookup"><span data-stu-id="101ec-183">Make hello appropriate sections as previously described</span></span>
1. <span data-ttu-id="101ec-184">按一下 hello"產生 SAS 」 按鈕。</span><span class="sxs-lookup"><span data-stu-id="101ec-184">Click hello "Generate SAS" button.</span></span>

![image](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="101ec-186">複製 hello 產生 SAS hello storageAccountSasToken 欄位;移除 hello 前置問號 (「？ 」)。</span><span class="sxs-lookup"><span data-stu-id="101ec-186">Copy hello generated SAS into hello storageAccountSasToken field; remove hello leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="101ec-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="101ec-187">sinksConfig</span></span>

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

<span data-ttu-id="101ec-188">這個選擇性區段會定義 toowhich hello 延伸模組會將它所收集的 hello 資訊的其他目的地。</span><span class="sxs-lookup"><span data-stu-id="101ec-188">This optional section defines additional destinations toowhich hello extension sends hello information it collects.</span></span> <span data-ttu-id="101ec-189">hello 的 「 接收 」 陣列會包含每個額外的資料接收的物件。</span><span class="sxs-lookup"><span data-stu-id="101ec-189">hello "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="101ec-190">「 類型 」 屬性會決定的 hello hello hello 物件中的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="101ec-190">hello "type" attribute determines hello other attributes in hello object.</span></span>

<span data-ttu-id="101ec-191">元素</span><span class="sxs-lookup"><span data-stu-id="101ec-191">Element</span></span> | <span data-ttu-id="101ec-192">值</span><span class="sxs-lookup"><span data-stu-id="101ec-192">Value</span></span>
------- | -----
<span data-ttu-id="101ec-193">名稱</span><span class="sxs-lookup"><span data-stu-id="101ec-193">name</span></span> | <span data-ttu-id="101ec-194">使用 toorefer toothis 接收 hello 延伸模組組態中的其他位置的字串。</span><span class="sxs-lookup"><span data-stu-id="101ec-194">A string used toorefer toothis sink elsewhere in hello extension configuration.</span></span>
<span data-ttu-id="101ec-195">類型</span><span class="sxs-lookup"><span data-stu-id="101ec-195">type</span></span> | <span data-ttu-id="101ec-196">hello 類型所定義的接收。</span><span class="sxs-lookup"><span data-stu-id="101ec-196">hello type of sink being defined.</span></span> <span data-ttu-id="101ec-197">在這種情況，判斷 hello 其他值 （是否有的話）。</span><span class="sxs-lookup"><span data-stu-id="101ec-197">Determines hello other values (if any) in instances of this type.</span></span>

<span data-ttu-id="101ec-198">3.0 版的 hello Linux 診斷延伸模組支援兩種接收類型： EventHub 和 JsonBlob。</span><span class="sxs-lookup"><span data-stu-id="101ec-198">Version 3.0 of hello Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="hello-eventhub-sink"></a><span data-ttu-id="101ec-199">hello EventHub 接收</span><span class="sxs-lookup"><span data-stu-id="101ec-199">hello EventHub sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

<span data-ttu-id="101ec-200">hello"sasURL"項目，包含完整的 URL，包括 SAS 權杖，如 hello 事件中樞 toowhich 資料應經過發佈的 hello。</span><span class="sxs-lookup"><span data-stu-id="101ec-200">hello "sasURL" entry contains hello full URL, including SAS token, for hello Event Hub toowhich data should be published.</span></span> <span data-ttu-id="101ec-201">年輕人需要 SAS 命名的原則，可讓 hello 傳送宣告。</span><span class="sxs-lookup"><span data-stu-id="101ec-201">LAD requires a SAS naming a policy that enables hello Send claim.</span></span> <span data-ttu-id="101ec-202">例如：</span><span class="sxs-lookup"><span data-stu-id="101ec-202">An example:</span></span>

* <span data-ttu-id="101ec-203">建立名為 `contosohub` 的事件中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="101ec-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="101ec-204">建立事件中樞時呼叫的 hello 命名空間中`syslogmsgs`</span><span class="sxs-lookup"><span data-stu-id="101ec-204">Create an Event Hub in hello namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="101ec-205">Hello 名為事件中心上建立共用存取原則`writer`啟用 hello 傳送宣告</span><span class="sxs-lookup"><span data-stu-id="101ec-205">Create a Shared access policy on hello Event Hub named `writer` that enables hello Send claim</span></span>

<span data-ttu-id="101ec-206">如果您建立了 SAS 良好 2018 年 1 月 1 午夜 UTC 直到 hello sasURL 值可能是：</span><span class="sxs-lookup"><span data-stu-id="101ec-206">If you created a SAS good until midnight UTC on January 1, 2018, hello sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="101ec-207">如需為事件中樞產生 SAS 權杖的相關詳細資訊，請參閱[本網頁](../../event-hubs/event-hubs-authentication-and-security-model-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="101ec-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="hello-jsonblob-sink"></a><span data-ttu-id="101ec-208">hello JsonBlob 接收</span><span class="sxs-lookup"><span data-stu-id="101ec-208">hello JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="101ec-209">資料導向 tooa JsonBlob 接收器會儲存在 Azure 儲存體中的 blob。</span><span class="sxs-lookup"><span data-stu-id="101ec-209">Data directed tooa JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="101ec-210">LAD 的每個執行個體每小時會為每個接收名稱建立 Blob。</span><span class="sxs-lookup"><span data-stu-id="101ec-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="101ec-211">每個 Blob 一律包含物件的語法有效 JSON 陣列。</span><span class="sxs-lookup"><span data-stu-id="101ec-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="101ec-212">Toohello 陣列，會以不可分割方式加入新項目。</span><span class="sxs-lookup"><span data-stu-id="101ec-212">New entries are atomically added toohello array.</span></span> <span data-ttu-id="101ec-213">Blob 會儲存在名稱為 hello 接收相同的 hello 的容器。</span><span class="sxs-lookup"><span data-stu-id="101ec-213">Blobs are stored in a container with hello same name as hello sink.</span></span> <span data-ttu-id="101ec-214">hello Azure 儲存體規則的 blob 容器名稱的 JsonBlob 接收 toohello 名稱： 介於 3 到 63 個小寫英數字元的 ASCII 字元或連字號。</span><span class="sxs-lookup"><span data-stu-id="101ec-214">hello Azure storage rules for blob container names apply toohello names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="101ec-215">公用設定</span><span class="sxs-lookup"><span data-stu-id="101ec-215">Public settings</span></span>

<span data-ttu-id="101ec-216">此結構包含控制 hello hello 擴充所收集的資訊設定的不同區塊。</span><span class="sxs-lookup"><span data-stu-id="101ec-216">This structure contains various blocks of settings that control hello information collected by hello extension.</span></span> <span data-ttu-id="101ec-217">每個設定皆為選擇性。</span><span class="sxs-lookup"><span data-stu-id="101ec-217">Each setting is optional.</span></span> <span data-ttu-id="101ec-218">如果您指定 `ladCfg`，則亦須指定 `StorageAccount`。</span><span class="sxs-lookup"><span data-stu-id="101ec-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="101ec-219">元素</span><span class="sxs-lookup"><span data-stu-id="101ec-219">Element</span></span> | <span data-ttu-id="101ec-220">值</span><span class="sxs-lookup"><span data-stu-id="101ec-220">Value</span></span>
------- | -----
<span data-ttu-id="101ec-221">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="101ec-221">StorageAccount</span></span> | <span data-ttu-id="101ec-222">hello 資料寫入 hello 延伸模組的 hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="101ec-222">hello name of hello storage account in which data is written by hello extension.</span></span> <span data-ttu-id="101ec-223">必須是相同的名稱，指定在 hello hello[保護設定](#protected-settings)。</span><span class="sxs-lookup"><span data-stu-id="101ec-223">Must be hello same name as is specified in hello [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="101ec-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="101ec-224">mdsdHttpProxy</span></span> | <span data-ttu-id="101ec-225">（選擇性）如同 hello 相同[保護設定](#protected-settings)。</span><span class="sxs-lookup"><span data-stu-id="101ec-225">(optional) Same as in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="101ec-226">hello 公用值會覆寫 hello 私用的值，如果設定。</span><span class="sxs-lookup"><span data-stu-id="101ec-226">hello public value is overridden by hello private value, if set.</span></span> <span data-ttu-id="101ec-227">將 proxy 設定包含密碼，例如密碼 hello 中放入[保護設定](#protected-settings)。</span><span class="sxs-lookup"><span data-stu-id="101ec-227">Place proxy settings that contain a secret, such as a password, in hello [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="101ec-228">hello 下列各節將詳細說明 hello 其餘項目。</span><span class="sxs-lookup"><span data-stu-id="101ec-228">hello remaining elements are described in detail in hello following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="101ec-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="101ec-229">ladCfg</span></span>

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

<span data-ttu-id="101ec-230">此選擇性結構控制項 hello 的收集度量和記錄檔，傳遞 toohello Azure 度量服務和 tooother 資料接收器。</span><span class="sxs-lookup"><span data-stu-id="101ec-230">This optional structure controls hello gathering of metrics and logs for delivery toohello Azure Metrics service and tooother data sinks.</span></span> <span data-ttu-id="101ec-231">您必須指定 `performanceCounters` 或 `syslogEvents` 或是兩者。</span><span class="sxs-lookup"><span data-stu-id="101ec-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="101ec-232">您必須指定 hello`metrics`結構。</span><span class="sxs-lookup"><span data-stu-id="101ec-232">You must specify hello `metrics` structure.</span></span>

<span data-ttu-id="101ec-233">元素</span><span class="sxs-lookup"><span data-stu-id="101ec-233">Element</span></span> | <span data-ttu-id="101ec-234">值</span><span class="sxs-lookup"><span data-stu-id="101ec-234">Value</span></span>
------- | -----
<span data-ttu-id="101ec-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="101ec-235">eventVolume</span></span> | <span data-ttu-id="101ec-236">（選擇性）控制項 hello hello 儲存體資料表中建立的資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="101ec-236">(optional) Controls hello number of partitions created within hello storage table.</span></span> <span data-ttu-id="101ec-237">必須是 `"Large"`、`"Medium"` 或 `"Small"` 的其中之一。</span><span class="sxs-lookup"><span data-stu-id="101ec-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="101ec-238">如果未指定，hello 預設值是`"Medium"`。</span><span class="sxs-lookup"><span data-stu-id="101ec-238">If not specified, hello default value is `"Medium"`.</span></span>
<span data-ttu-id="101ec-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="101ec-239">sampleRateInSeconds</span></span> | <span data-ttu-id="101ec-240">（選擇性） hello 預設間隔原始 （未彙總） 的度量收集。</span><span class="sxs-lookup"><span data-stu-id="101ec-240">(optional) hello default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="101ec-241">hello 最小支援的取樣率為 15 秒。</span><span class="sxs-lookup"><span data-stu-id="101ec-241">hello smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="101ec-242">如果未指定，hello 預設值是`15`。</span><span class="sxs-lookup"><span data-stu-id="101ec-242">If not specified, hello default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="101ec-243">metrics</span><span class="sxs-lookup"><span data-stu-id="101ec-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="101ec-244">元素</span><span class="sxs-lookup"><span data-stu-id="101ec-244">Element</span></span> | <span data-ttu-id="101ec-245">值</span><span class="sxs-lookup"><span data-stu-id="101ec-245">Value</span></span>
------- | -----
<span data-ttu-id="101ec-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="101ec-246">resourceId</span></span> | <span data-ttu-id="101ec-247">設定 toowhich hello VM 所屬 hello 的 Azure 資源管理員資源識別碼 hello VM 或 hello 虛擬機器規模。</span><span class="sxs-lookup"><span data-stu-id="101ec-247">hello Azure Resource Manager resource ID of hello VM or of hello virtual machine scale set toowhich hello VM belongs.</span></span> <span data-ttu-id="101ec-248">這個設定必須也指定是否 hello 設定中使用任何 JsonBlob 接收。</span><span class="sxs-lookup"><span data-stu-id="101ec-248">This setting must be also specified if any JsonBlob sink is used in hello configuration.</span></span>
<span data-ttu-id="101ec-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="101ec-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="101ec-250">彙總度量資訊是 toobe hello 頻率計算，以及傳輸 tooAzure 度量，表示為是 8601 時間間隔。</span><span class="sxs-lookup"><span data-stu-id="101ec-250">hello frequency at which aggregate metrics are toobe computed and transferred tooAzure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="101ec-251">最小傳輸週期 hello 為 60 秒，也就是 PT1M。</span><span class="sxs-lookup"><span data-stu-id="101ec-251">hello smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="101ec-252">您必須指定至少一個 scheduledTransferPeriod。</span><span class="sxs-lookup"><span data-stu-id="101ec-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="101ec-253">範例的 hello hello performanceCounters 區段中指定的度量資訊會收集每 15 秒，或在 hello 明確定義 hello 計數器的取樣率。</span><span class="sxs-lookup"><span data-stu-id="101ec-253">Samples of hello metrics specified in hello performanceCounters section are collected every 15 seconds or at hello sample rate explicitly defined for hello counter.</span></span> <span data-ttu-id="101ec-254">如果多個 scheduledTransferPeriod 頻率出現 （hello 如範例所示），會個別計算每個彙總。</span><span class="sxs-lookup"><span data-stu-id="101ec-254">If multiple scheduledTransferPeriod frequencies appear (as in hello example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="101ec-255">performanceCounters</span><span class="sxs-lookup"><span data-stu-id="101ec-255">performanceCounters</span></span>

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

<span data-ttu-id="101ec-256">此選用小節控制 hello 度量收集。</span><span class="sxs-lookup"><span data-stu-id="101ec-256">This optional section controls hello collection of metrics.</span></span> <span data-ttu-id="101ec-257">未經處理的範例會針對每個彙總[scheduledTransferPeriod](#metrics) tooproduce 這些值：</span><span class="sxs-lookup"><span data-stu-id="101ec-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) tooproduce these values:</span></span>

* <span data-ttu-id="101ec-258">平均值</span><span class="sxs-lookup"><span data-stu-id="101ec-258">mean</span></span>
* <span data-ttu-id="101ec-259">minimum</span><span class="sxs-lookup"><span data-stu-id="101ec-259">minimum</span></span>
* <span data-ttu-id="101ec-260">maximum</span><span class="sxs-lookup"><span data-stu-id="101ec-260">maximum</span></span>
* <span data-ttu-id="101ec-261">上次收集的值</span><span class="sxs-lookup"><span data-stu-id="101ec-261">last-collected value</span></span>
* <span data-ttu-id="101ec-262">使用 toocompute hello 彙總的原始樣本的計數。</span><span class="sxs-lookup"><span data-stu-id="101ec-262">count of raw samples used toocompute hello aggregate</span></span>

<span data-ttu-id="101ec-263">元素</span><span class="sxs-lookup"><span data-stu-id="101ec-263">Element</span></span> | <span data-ttu-id="101ec-264">值</span><span class="sxs-lookup"><span data-stu-id="101ec-264">Value</span></span>
------- | -----
<span data-ttu-id="101ec-265">sinks</span><span class="sxs-lookup"><span data-stu-id="101ec-265">sinks</span></span> | <span data-ttu-id="101ec-266">（選擇性）以逗號分隔的清單名稱的接收器的 toowhich 年輕人傳送彙總的度量結果。</span><span class="sxs-lookup"><span data-stu-id="101ec-266">(optional) A comma-separated list of names of sinks toowhich LAD sends aggregated metric results.</span></span> <span data-ttu-id="101ec-267">所有彙總的度量資訊會列出已發行的 tooeach 接收。</span><span class="sxs-lookup"><span data-stu-id="101ec-267">All aggregated metrics are published tooeach listed sink.</span></span> <span data-ttu-id="101ec-268">請參閱 [sinksConfig](#sinksconfig)。</span><span class="sxs-lookup"><span data-stu-id="101ec-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="101ec-269">範例： `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="101ec-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="101ec-270">類型</span><span class="sxs-lookup"><span data-stu-id="101ec-270">type</span></span> | <span data-ttu-id="101ec-271">識別 hello 標準的 hello 實際的提供者。</span><span class="sxs-lookup"><span data-stu-id="101ec-271">Identifies hello actual provider of hello metric.</span></span>
<span data-ttu-id="101ec-272">class</span><span class="sxs-lookup"><span data-stu-id="101ec-272">class</span></span> | <span data-ttu-id="101ec-273">"Counter"，以及識別 hello hello 提供者的命名空間內的特定度量。</span><span class="sxs-lookup"><span data-stu-id="101ec-273">Together with "counter", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="101ec-274">counter</span><span class="sxs-lookup"><span data-stu-id="101ec-274">counter</span></span> | <span data-ttu-id="101ec-275">「 類別 」，以及識別 hello hello 提供者的命名空間內的特定度量。</span><span class="sxs-lookup"><span data-stu-id="101ec-275">Together with "class", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="101ec-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="101ec-276">counterSpecifier</span></span> | <span data-ttu-id="101ec-277">識別 hello hello Azure 度量命名空間內的特定度量。</span><span class="sxs-lookup"><span data-stu-id="101ec-277">Identifies hello specific metric within hello Azure Metrics namespace.</span></span>
<span data-ttu-id="101ec-278">condition</span><span class="sxs-lookup"><span data-stu-id="101ec-278">condition</span></span> | <span data-ttu-id="101ec-279">（選擇性）適用於選取 hello 物件 toowhich hello 度量的特定執行個體，或選取 hello 彙總，該物件的所有執行個體。</span><span class="sxs-lookup"><span data-stu-id="101ec-279">(optional) Selects a specific instance of hello object toowhich hello metric applies or selects hello aggregation across all instances of that object.</span></span> <span data-ttu-id="101ec-280">如需詳細資訊，請參閱 hello [ `builtin`度量定義](#metrics-supported-by-builtin)。</span><span class="sxs-lookup"><span data-stu-id="101ec-280">For more information, see hello [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="101ec-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="101ec-281">sampleRate</span></span> | <span data-ttu-id="101ec-282">是設定 hello 速率未經處理的範例，為此度量所收集的 8601 間隔。</span><span class="sxs-lookup"><span data-stu-id="101ec-282">IS 8601 interval that sets hello rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="101ec-283">如果未設定，hello 收集間隔設定 hello 值[sampleRateInSeconds](#ladcfg)。</span><span class="sxs-lookup"><span data-stu-id="101ec-283">If not set, hello collection interval is set by hello value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="101ec-284">hello 最短的受支援的取樣率為 15 秒 (PT15S)。</span><span class="sxs-lookup"><span data-stu-id="101ec-284">hello shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="101ec-285">unit</span><span class="sxs-lookup"><span data-stu-id="101ec-285">unit</span></span> | <span data-ttu-id="101ec-286">應為以下字串之一："Count"、"Bytes"、"Seconds"、"Percent"、"CountPerSecond"、"BytesPerSecond"、"Millisecond"。</span><span class="sxs-lookup"><span data-stu-id="101ec-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="101ec-287">定義 hello hello 度量單位。</span><span class="sxs-lookup"><span data-stu-id="101ec-287">Defines hello unit for hello metric.</span></span> <span data-ttu-id="101ec-288">Hello 收集資料的取用者期望 hello 收集的資料值 toomatch 此單元。</span><span class="sxs-lookup"><span data-stu-id="101ec-288">Consumers of hello collected data expect hello collected data values toomatch this unit.</span></span> <span data-ttu-id="101ec-289">LAD 會忽略此欄位。</span><span class="sxs-lookup"><span data-stu-id="101ec-289">LAD ignores this field.</span></span>
<span data-ttu-id="101ec-290">displayName</span><span class="sxs-lookup"><span data-stu-id="101ec-290">displayName</span></span> | <span data-ttu-id="101ec-291">hello （在 hello hello 相關聯的區域，設定所指定的語言） 中的標籤 toobe 附加 toothis Azure 標準中的資料。</span><span class="sxs-lookup"><span data-stu-id="101ec-291">hello label (in hello language specified by hello associated locale setting) toobe attached toothis data in Azure Metrics.</span></span> <span data-ttu-id="101ec-292">LAD 會忽略此欄位。</span><span class="sxs-lookup"><span data-stu-id="101ec-292">LAD ignores this field.</span></span>

<span data-ttu-id="101ec-293">hello counterSpecifier 是自定的識別碼。</span><span class="sxs-lookup"><span data-stu-id="101ec-293">hello counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="101ec-294">取用者的度量，例如 hello Azure 入口網站圖表和警示功能，會使用 counterSpecifier 做 hello 「 金鑰 」，以識別度量或標準的執行個體。</span><span class="sxs-lookup"><span data-stu-id="101ec-294">Consumers of metrics, like hello Azure portal charting and alerting feature, use counterSpecifier as hello "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="101ec-295">對於 `builtin` 計量，建議您使用開頭為 `/builtin/` 的 counterSpecifier 值。</span><span class="sxs-lookup"><span data-stu-id="101ec-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="101ec-296">如果您要收集度量資訊的特定執行個體，建議您附加 hello 識別碼 hello 執行個體 toohello counterSpecifier 值。</span><span class="sxs-lookup"><span data-stu-id="101ec-296">If you are collecting a specific instance of a metric, we recommend you attach hello identifier of hello instance toohello counterSpecifier value.</span></span> <span data-ttu-id="101ec-297">部分範例如下：</span><span class="sxs-lookup"><span data-stu-id="101ec-297">Some examples:</span></span>

* <span data-ttu-id="101ec-298">`/builtin/Processor/PercentIdleTime` - 所有核心的平均閒置時間</span><span class="sxs-lookup"><span data-stu-id="101ec-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="101ec-299">`/builtin/Disk/FreeSpace(/mnt)`-適用於 hello /mnt filesystem 可用空間</span><span class="sxs-lookup"><span data-stu-id="101ec-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for hello /mnt filesystem</span></span>
* <span data-ttu-id="101ec-300">`/builtin/Disk/FreeSpace` - 所有已掛接檔案系統的平均可用空間</span><span class="sxs-lookup"><span data-stu-id="101ec-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="101ec-301">年輕人都 hello Azure 入口網站預期 hello counterSpecifier 值 toomatch 任何模式。</span><span class="sxs-lookup"><span data-stu-id="101ec-301">Neither LAD nor hello Azure portal expects hello counterSpecifier value toomatch any pattern.</span></span> <span data-ttu-id="101ec-302">應與您建構 counterSpecifier 值的方式一致。</span><span class="sxs-lookup"><span data-stu-id="101ec-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="101ec-303">當您指定`performanceCounters`，年輕人一律會 tooa 資料表寫入 Azure 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="101ec-303">When you specify `performanceCounters`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="101ec-304">您可以擁有 hello 相同寫入 tooJSON blob 及/或事件中心的資料，但您無法停用儲存的資料 tooa 資料表。</span><span class="sxs-lookup"><span data-stu-id="101ec-304">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="101ec-305">所有執行個體的 hello 診斷延伸模組設定 toouse hello 相同的儲存體帳戶名稱與端點加入其標準和記錄檔 toohello 相同的資料表。</span><span class="sxs-lookup"><span data-stu-id="101ec-305">All instances of hello diagnostic extension configured toouse hello same storage account name and endpoint add their metrics and logs toohello same table.</span></span> <span data-ttu-id="101ec-306">如果太多的 Vm 所撰寫的 toohello 相同資料表的資料分割，Azure 可以進行節流處理寫入 toothat 磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="101ec-306">If too many VMs are writing toohello same table partition, Azure can throttle writes toothat partition.</span></span> <span data-ttu-id="101ec-307">設定原因項目 toobe hello eventVolume 分散到 1 （小）、 （中），10 或 100 個 （大型） 不同的資料分割。</span><span class="sxs-lookup"><span data-stu-id="101ec-307">hello eventVolume setting causes entries toobe spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="101ec-308">通常，"Medium"是足夠 tooensure 流量不會節流處理。</span><span class="sxs-lookup"><span data-stu-id="101ec-308">Usually, "Medium" is sufficient tooensure traffic is not throttled.</span></span> <span data-ttu-id="101ec-309">hello Azure 入口網站的 hello Azure 度量功能會使用這個資料表 tooproduce 圖形或 tootrigger 警示中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="101ec-309">hello Azure Metrics feature of hello Azure portal uses hello data in this table tooproduce graphs or tootrigger alerts.</span></span> <span data-ttu-id="101ec-310">hello 資料表名稱是 hello 串連這些字串：</span><span class="sxs-lookup"><span data-stu-id="101ec-310">hello table name is hello concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="101ec-311">hello"scheduledTransferPeriod"hello 彙總儲存在 hello 資料表中的值</span><span class="sxs-lookup"><span data-stu-id="101ec-311">hello "scheduledTransferPeriod" for hello aggregated values stored in hello table</span></span>
* `P10DV2S`
* <span data-ttu-id="101ec-312">Hello 格式"YYYYMMDD 」，以變更每隔 10 天的日期</span><span class="sxs-lookup"><span data-stu-id="101ec-312">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="101ec-313">例如 `WADMetricsPT1HP10DV2S20170410` 與 `WADMetricsPT1MP10DV2S20170609`。</span><span class="sxs-lookup"><span data-stu-id="101ec-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="101ec-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="101ec-314">syslogEvents</span></span>

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

<span data-ttu-id="101ec-315">此選用小節控制記錄檔事件從 syslog hello 集合。</span><span class="sxs-lookup"><span data-stu-id="101ec-315">This optional section controls hello collection of log events from syslog.</span></span> <span data-ttu-id="101ec-316">如果省略 hello 區段 syslog 事件不會擷取所有。</span><span class="sxs-lookup"><span data-stu-id="101ec-316">If hello section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="101ec-317">hello syslogEventConfiguration 集合具有一個項目感興趣的每個 syslog 設備。</span><span class="sxs-lookup"><span data-stu-id="101ec-317">hello syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="101ec-318">如果 minSeverity 是 「 無 」 特定的功能，或該功能不會完全顯示 hello 項目中，會不擷取從該設備的任何事件。</span><span class="sxs-lookup"><span data-stu-id="101ec-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in hello element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="101ec-319">元素</span><span class="sxs-lookup"><span data-stu-id="101ec-319">Element</span></span> | <span data-ttu-id="101ec-320">值</span><span class="sxs-lookup"><span data-stu-id="101ec-320">Value</span></span>
------- | -----
<span data-ttu-id="101ec-321">sinks</span><span class="sxs-lookup"><span data-stu-id="101ec-321">sinks</span></span> | <span data-ttu-id="101ec-322">以逗號分隔的清單名稱的接收器 toowhich 個別記錄事件發行。</span><span class="sxs-lookup"><span data-stu-id="101ec-322">A comma-separated list of names of sinks toowhich individual log events are published.</span></span> <span data-ttu-id="101ec-323">比對中 syslogEventConfiguration hello 限制的所有記錄檔事件會列出已發行的 tooeach 接收。</span><span class="sxs-lookup"><span data-stu-id="101ec-323">All log events matching hello restrictions in syslogEventConfiguration are published tooeach listed sink.</span></span> <span data-ttu-id="101ec-324">範例："EHforsyslog"</span><span class="sxs-lookup"><span data-stu-id="101ec-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="101ec-325">facilityName</span><span class="sxs-lookup"><span data-stu-id="101ec-325">facilityName</span></span> | <span data-ttu-id="101ec-326">Syslog 設備名稱 (例如 "LOG\_USER" 或 "LOG\_LOCAL0")。</span><span class="sxs-lookup"><span data-stu-id="101ec-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="101ec-327">請參閱 「 功能 」 一節 hello hello [syslog man 頁面](http://man7.org/linux/man-pages/man3/syslog.3.html)hello 完整清單。</span><span class="sxs-lookup"><span data-stu-id="101ec-327">See hello "facility" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span>
<span data-ttu-id="101ec-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="101ec-328">minSeverity</span></span> | <span data-ttu-id="101ec-329">Syslog 嚴重性層級 (例如 "LOG\_ERR" 或 "LOG\_INFO")。</span><span class="sxs-lookup"><span data-stu-id="101ec-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="101ec-330">請參閱 「 層級 」 一節 hello hello [syslog man 頁面](http://man7.org/linux/man-pages/man3/syslog.3.html)hello 完整清單。</span><span class="sxs-lookup"><span data-stu-id="101ec-330">See hello "level" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span> <span data-ttu-id="101ec-331">hello 擴充功能會擷取在傳送事件 toohello 設備或 hello 高於指定層級。</span><span class="sxs-lookup"><span data-stu-id="101ec-331">hello extension captures events sent toohello facility at or above hello specified level.</span></span>

<span data-ttu-id="101ec-332">當您指定`syslogEvents`，年輕人一律會 tooa 資料表寫入 Azure 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="101ec-332">When you specify `syslogEvents`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="101ec-333">您可以擁有 hello 相同寫入 tooJSON blob 及/或事件中心的資料，但您無法停用儲存的資料 tooa 資料表。</span><span class="sxs-lookup"><span data-stu-id="101ec-333">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="101ec-334">資料分割行為，這個資料表的 hello 是 hello 如所述相同`performanceCounters`。</span><span class="sxs-lookup"><span data-stu-id="101ec-334">hello partitioning behavior for this table is hello same as described for `performanceCounters`.</span></span> <span data-ttu-id="101ec-335">hello 資料表名稱是 hello 串連這些字串：</span><span class="sxs-lookup"><span data-stu-id="101ec-335">hello table name is hello concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="101ec-336">Hello 格式"YYYYMMDD 」，以變更每隔 10 天的日期</span><span class="sxs-lookup"><span data-stu-id="101ec-336">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="101ec-337">例如 `LinuxSyslog20170410` 與 `LinuxSyslog20170609`。</span><span class="sxs-lookup"><span data-stu-id="101ec-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="101ec-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="101ec-338">perfCfg</span></span>

<span data-ttu-id="101ec-339">此選擇性區段會控制任意 [OMI](https://github.com/Microsoft/omi) 查詢的執行。</span><span class="sxs-lookup"><span data-stu-id="101ec-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

<span data-ttu-id="101ec-340">元素</span><span class="sxs-lookup"><span data-stu-id="101ec-340">Element</span></span> | <span data-ttu-id="101ec-341">值</span><span class="sxs-lookup"><span data-stu-id="101ec-341">Value</span></span>
------- | -----
<span data-ttu-id="101ec-342">namespace</span><span class="sxs-lookup"><span data-stu-id="101ec-342">namespace</span></span> | <span data-ttu-id="101ec-343">（選擇性） hello OMI 命名空間中的 hello 應對其執行查詢。</span><span class="sxs-lookup"><span data-stu-id="101ec-343">(optional) hello OMI namespace within which hello query should be executed.</span></span> <span data-ttu-id="101ec-344">如果未指定，hello 預設值是"root/scx"，藉由 hello [System Center 跨平台提供者](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation)。</span><span class="sxs-lookup"><span data-stu-id="101ec-344">If unspecified, hello default value is "root/scx", implemented by hello [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="101ec-345">query</span><span class="sxs-lookup"><span data-stu-id="101ec-345">query</span></span> | <span data-ttu-id="101ec-346">hello OMI 查詢 toobe 執行。</span><span class="sxs-lookup"><span data-stu-id="101ec-346">hello OMI query toobe executed.</span></span>
<span data-ttu-id="101ec-347">資料表</span><span class="sxs-lookup"><span data-stu-id="101ec-347">table</span></span> | <span data-ttu-id="101ec-348">（選擇性） hello Azure 儲存體資料表，在 指定儲存體帳戶的 hello (請參閱[保護設定](#protected-settings))。</span><span class="sxs-lookup"><span data-stu-id="101ec-348">(optional) hello Azure storage table, in hello designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="101ec-349">frequency</span><span class="sxs-lookup"><span data-stu-id="101ec-349">frequency</span></span> | <span data-ttu-id="101ec-350">（選擇性） hello hello 查詢的執行之間的秒數。</span><span class="sxs-lookup"><span data-stu-id="101ec-350">(optional) hello number of seconds between execution of hello query.</span></span> <span data-ttu-id="101ec-351">預設值為 300 秒 (5 分鐘)；最小值為 15 秒。</span><span class="sxs-lookup"><span data-stu-id="101ec-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="101ec-352">sinks</span><span class="sxs-lookup"><span data-stu-id="101ec-352">sinks</span></span> | <span data-ttu-id="101ec-353">（選擇性）應經過發佈之其他接收 toowhich 原始範例度量結果的名稱以逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="101ec-353">(optional) A comma-separated list of names of additional sinks toowhich raw sample metric results should be published.</span></span> <span data-ttu-id="101ec-354">Hello 延伸模組或 Azure 度量，會不計算任何彙總這些未經處理的範例。</span><span class="sxs-lookup"><span data-stu-id="101ec-354">No aggregation of these raw samples is computed by hello extension or by Azure Metrics.</span></span>

<span data-ttu-id="101ec-355">必須指定 "table" 或 "sinks"，或兩者。</span><span class="sxs-lookup"><span data-stu-id="101ec-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="101ec-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="101ec-356">fileLogs</span></span>

<span data-ttu-id="101ec-357">控制項 hello 擷取的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="101ec-357">Controls hello capture of log files.</span></span> <span data-ttu-id="101ec-358">年輕人擷取新的文字行，當它們被寫入 toohello 檔案，並將它們寫入 tootable 資料列和/或任何指定的接收 （JsonBlob 或 EventHub）。</span><span class="sxs-lookup"><span data-stu-id="101ec-358">LAD captures new text lines as they are written toohello file and writes them tootable rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="101ec-359">元素</span><span class="sxs-lookup"><span data-stu-id="101ec-359">Element</span></span> | <span data-ttu-id="101ec-360">值</span><span class="sxs-lookup"><span data-stu-id="101ec-360">Value</span></span>
------- | -----
<span data-ttu-id="101ec-361">file</span><span class="sxs-lookup"><span data-stu-id="101ec-361">file</span></span> | <span data-ttu-id="101ec-362">監看 hello 記錄檔案 toobe hello 完整路徑名稱，並擷取。</span><span class="sxs-lookup"><span data-stu-id="101ec-362">hello full pathname of hello log file toobe watched and captured.</span></span> <span data-ttu-id="101ec-363">hello pathname 必須單一檔案名稱;它不能命名目錄，或包含萬用字元。</span><span class="sxs-lookup"><span data-stu-id="101ec-363">hello pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="101ec-364">資料表</span><span class="sxs-lookup"><span data-stu-id="101ec-364">table</span></span> | <span data-ttu-id="101ec-365">hello 指定儲存體中的 （選擇性） hello Azure 儲存體資料表 」 帳戶 （如指定 hello 受保護的組態中），到哪一個新行 hello"tail"hello 檔案的寫入。</span><span class="sxs-lookup"><span data-stu-id="101ec-365">(optional) hello Azure storage table, in hello designated storage account (as specified in hello protected configuration), into which new lines from hello "tail" of hello file are written.</span></span>
<span data-ttu-id="101ec-366">sinks</span><span class="sxs-lookup"><span data-stu-id="101ec-366">sinks</span></span> | <span data-ttu-id="101ec-367">（選擇性）傳送其他接收 toowhich 記錄行的名稱的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="101ec-367">(optional) A comma-separated list of names of additional sinks toowhich log lines sent.</span></span>

<span data-ttu-id="101ec-368">必須指定 "table" 或 "sinks"，或兩者。</span><span class="sxs-lookup"><span data-stu-id="101ec-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-hello-builtin-provider"></a><span data-ttu-id="101ec-369">Hello 內建提供者所支援的度量</span><span class="sxs-lookup"><span data-stu-id="101ec-369">Metrics supported by hello builtin provider</span></span>

<span data-ttu-id="101ec-370">hello builtin 度量的提供者會為資料來源的度量最有趣 tooa 組廣泛的使用者。</span><span class="sxs-lookup"><span data-stu-id="101ec-370">hello builtin metric provider is a source of metrics most interesting tooa broad set of users.</span></span> <span data-ttu-id="101ec-371">這些計量分成五大類別：</span><span class="sxs-lookup"><span data-stu-id="101ec-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="101ec-372">處理器</span><span class="sxs-lookup"><span data-stu-id="101ec-372">Processor</span></span>
* <span data-ttu-id="101ec-373">記憶體</span><span class="sxs-lookup"><span data-stu-id="101ec-373">Memory</span></span>
* <span data-ttu-id="101ec-374">網路</span><span class="sxs-lookup"><span data-stu-id="101ec-374">Network</span></span>
* <span data-ttu-id="101ec-375">檔案系統</span><span class="sxs-lookup"><span data-stu-id="101ec-375">Filesystem</span></span>
* <span data-ttu-id="101ec-376">磁碟</span><span class="sxs-lookup"><span data-stu-id="101ec-376">Disk</span></span>

### <a name="builtin-metrics-for-hello-processor-class"></a><span data-ttu-id="101ec-377">hello 處理器類別的內建度量</span><span class="sxs-lookup"><span data-stu-id="101ec-377">builtin metrics for hello Processor class</span></span>

<span data-ttu-id="101ec-378">hello 度量的處理器類別提供 hello VM 中的處理器使用量的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="101ec-378">hello Processor class of metrics provides information about processor usage in hello VM.</span></span> <span data-ttu-id="101ec-379">彙總百分比，hello 結果會是 hello 平均所有 cpu。</span><span class="sxs-lookup"><span data-stu-id="101ec-379">When aggregating percentages, hello result is hello average across all CPUs.</span></span> <span data-ttu-id="101ec-380">在兩個核心 VM，如果其中一個核心是 100%忙碌中，其他 hello 100%閒置，hello 報告 PercentIdleTime 會是 50。</span><span class="sxs-lookup"><span data-stu-id="101ec-380">In a two core VM, if one core was 100% busy and hello other was 100% idle, hello reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="101ec-381">如果每個核心已忙碌的 50 %hello 相同 hello 週期，報告結果也會是 50。</span><span class="sxs-lookup"><span data-stu-id="101ec-381">If each core was 50% busy for hello same period, hello reported result would also be 50.</span></span> <span data-ttu-id="101ec-382">在四個核心的 VM，和一個核心的 100%忙碌和 hello 閒置，其他人 hello 報告 PercentIdleTime 是 75。</span><span class="sxs-lookup"><span data-stu-id="101ec-382">In a four core VM, with one core 100% busy and hello others idle, hello reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="101ec-383">counter</span><span class="sxs-lookup"><span data-stu-id="101ec-383">counter</span></span> | <span data-ttu-id="101ec-384">意義</span><span class="sxs-lookup"><span data-stu-id="101ec-384">Meaning</span></span>
------- | -------
<span data-ttu-id="101ec-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="101ec-385">PercentIdleTime</span></span> | <span data-ttu-id="101ec-386">Hello 彙總視窗處理器在執行 hello 核心閒置迴圈期間的時間百分比</span><span class="sxs-lookup"><span data-stu-id="101ec-386">Percentage of time during hello aggregation window that processors were executing hello kernel idle loop</span></span>
<span data-ttu-id="101ec-387">PercentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="101ec-387">PercentProcessorTime</span></span> | <span data-ttu-id="101ec-388">執行非閒置執行緒的時間百分比</span><span class="sxs-lookup"><span data-stu-id="101ec-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="101ec-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="101ec-389">PercentIOWaitTime</span></span> | <span data-ttu-id="101ec-390">IO 作業 toocomplete 正在等候的時間百分比</span><span class="sxs-lookup"><span data-stu-id="101ec-390">Percentage of time waiting for IO operations toocomplete</span></span>
<span data-ttu-id="101ec-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="101ec-391">PercentInterruptTime</span></span> | <span data-ttu-id="101ec-392">執行硬體/軟體中斷與 DPC (延遲的程序呼叫) 的時間百分比</span><span class="sxs-lookup"><span data-stu-id="101ec-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="101ec-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="101ec-393">PercentUserTime</span></span> | <span data-ttu-id="101ec-394">Hello 彙總間隔期間的非閒置時間，hello 時間百分比在 使用者以一般優先權更</span><span class="sxs-lookup"><span data-stu-id="101ec-394">Of non-idle time during hello aggregation window, hello percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="101ec-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="101ec-395">PercentNiceTime</span></span> | <span data-ttu-id="101ec-396">非閒置的時間，hello 百分比降低 (nice) 的優先順序</span><span class="sxs-lookup"><span data-stu-id="101ec-396">Of non-idle time, hello percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="101ec-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="101ec-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="101ec-398">非閒置的時間，顯示花費在特殊權限 （核心） 模式的 hello 百分比</span><span class="sxs-lookup"><span data-stu-id="101ec-398">Of non-idle time, hello percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="101ec-399">hello 前四個計數器的加總應該 too100%。</span><span class="sxs-lookup"><span data-stu-id="101ec-399">hello first four counters should sum too100%.</span></span> <span data-ttu-id="101ec-400">hello 最後三個計數器也總和 too100%;它們細分 PercentProcessorTime、 PercentIOWaitTime，和 PercentInterruptTime hello 總和。</span><span class="sxs-lookup"><span data-stu-id="101ec-400">hello last three counters also sum too100%; they subdivide hello sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="101ec-401">tooobtain 單一度量彙總所有的處理器之間設定`"condition": "IsAggregate=TRUE"`。</span><span class="sxs-lookup"><span data-stu-id="101ec-401">tooobtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="101ec-402">tooobtain 特定處理器的度量，例如 hello 第二個邏輯處理器，四個核心的 VM，設定`"condition": "Name=\\"1\\""`。</span><span class="sxs-lookup"><span data-stu-id="101ec-402">tooobtain a metric for a specific processor, such as hello second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="101ec-403">邏輯處理器數目是在 hello 範圍`[0..n-1]`。</span><span class="sxs-lookup"><span data-stu-id="101ec-403">Logical processor numbers are in hello range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-hello-memory-class"></a><span data-ttu-id="101ec-404">hello 記憶體類別的內建度量</span><span class="sxs-lookup"><span data-stu-id="101ec-404">builtin metrics for hello Memory class</span></span>

<span data-ttu-id="101ec-405">hello 的度量資訊的記憶體類別提供有關記憶體使用率、 分頁和交換資訊。</span><span class="sxs-lookup"><span data-stu-id="101ec-405">hello Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="101ec-406">counter</span><span class="sxs-lookup"><span data-stu-id="101ec-406">counter</span></span> | <span data-ttu-id="101ec-407">意義</span><span class="sxs-lookup"><span data-stu-id="101ec-407">Meaning</span></span>
------- | -------
<span data-ttu-id="101ec-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="101ec-408">AvailableMemory</span></span> | <span data-ttu-id="101ec-409">可用的實體記憶體 (MiB)</span><span class="sxs-lookup"><span data-stu-id="101ec-409">Available physical memory in MiB</span></span>
<span data-ttu-id="101ec-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="101ec-410">PercentAvailableMemory</span></span> | <span data-ttu-id="101ec-411">以總記憶體百分比表示的可用實體記憶體</span><span class="sxs-lookup"><span data-stu-id="101ec-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="101ec-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="101ec-412">UsedMemory</span></span> | <span data-ttu-id="101ec-413">使用中實體記憶體 (MiB)</span><span class="sxs-lookup"><span data-stu-id="101ec-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="101ec-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="101ec-414">PercentUsedMemory</span></span> | <span data-ttu-id="101ec-415">以總記憶體百分比表示的使用中實體記憶體</span><span class="sxs-lookup"><span data-stu-id="101ec-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="101ec-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="101ec-416">PagesPerSec</span></span> | <span data-ttu-id="101ec-417">總分頁數 (讀取/寫入)</span><span class="sxs-lookup"><span data-stu-id="101ec-417">Total paging (read/write)</span></span>
<span data-ttu-id="101ec-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="101ec-418">PagesReadPerSec</span></span> | <span data-ttu-id="101ec-419">從備份存放區讀取的分頁數 (分頁檔、程式檔、對應檔等)</span><span class="sxs-lookup"><span data-stu-id="101ec-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="101ec-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="101ec-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="101ec-421">寫入 toobacking 儲存 （分頁檔、 對應的檔）</span><span class="sxs-lookup"><span data-stu-id="101ec-421">Pages written toobacking store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="101ec-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="101ec-422">AvailableSwap</span></span> | <span data-ttu-id="101ec-423">未使用的交換空間 (MiB)</span><span class="sxs-lookup"><span data-stu-id="101ec-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="101ec-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="101ec-424">PercentAvailableSwap</span></span> | <span data-ttu-id="101ec-425">以總交換空間百分比表示的未使用交換空間</span><span class="sxs-lookup"><span data-stu-id="101ec-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="101ec-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="101ec-426">UsedSwap</span></span> | <span data-ttu-id="101ec-427">已使用交換空間 (MiB)</span><span class="sxs-lookup"><span data-stu-id="101ec-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="101ec-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="101ec-428">PercentUsedSwap</span></span> | <span data-ttu-id="101ec-429">以總交換空間表示的使用中交換空間</span><span class="sxs-lookup"><span data-stu-id="101ec-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="101ec-430">此計量類別只有單一執行個體。</span><span class="sxs-lookup"><span data-stu-id="101ec-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="101ec-431">hello 「 條件 」 屬性有任何有用的設定，且應該省略。</span><span class="sxs-lookup"><span data-stu-id="101ec-431">hello "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-hello-network-class"></a><span data-ttu-id="101ec-432">hello 網路類別的內建度量</span><span class="sxs-lookup"><span data-stu-id="101ec-432">builtin metrics for hello Network class</span></span>

<span data-ttu-id="101ec-433">hello 網路類別的度量會提供個別的網路介面上開機後經過網路活動的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="101ec-433">hello Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="101ec-434">LAD 不會公開頻寬計量，該計量可從主機計量中取出。</span><span class="sxs-lookup"><span data-stu-id="101ec-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="101ec-435">counter</span><span class="sxs-lookup"><span data-stu-id="101ec-435">counter</span></span> | <span data-ttu-id="101ec-436">意義</span><span class="sxs-lookup"><span data-stu-id="101ec-436">Meaning</span></span>
------- | -------
<span data-ttu-id="101ec-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="101ec-437">BytesTransmitted</span></span> | <span data-ttu-id="101ec-438">自開機後傳送的位元組總數</span><span class="sxs-lookup"><span data-stu-id="101ec-438">Total bytes sent since boot</span></span>
<span data-ttu-id="101ec-439">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="101ec-439">BytesReceived</span></span> | <span data-ttu-id="101ec-440">自開機後收到的位元組總數</span><span class="sxs-lookup"><span data-stu-id="101ec-440">Total bytes received since boot</span></span>
<span data-ttu-id="101ec-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="101ec-441">BytesTotal</span></span> | <span data-ttu-id="101ec-442">自開機後收傳送或收到的位元組總數</span><span class="sxs-lookup"><span data-stu-id="101ec-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="101ec-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="101ec-443">PacketsTransmitted</span></span> | <span data-ttu-id="101ec-444">自開機後傳送的封包總數</span><span class="sxs-lookup"><span data-stu-id="101ec-444">Total packets sent since boot</span></span>
<span data-ttu-id="101ec-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="101ec-445">PacketsReceived</span></span> | <span data-ttu-id="101ec-446">自開機後收到的封包總數</span><span class="sxs-lookup"><span data-stu-id="101ec-446">Total packets received since boot</span></span>
<span data-ttu-id="101ec-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="101ec-447">TotalRxErrors</span></span> | <span data-ttu-id="101ec-448">自開機後接收的錯誤數</span><span class="sxs-lookup"><span data-stu-id="101ec-448">Number of receive errors since boot</span></span>
<span data-ttu-id="101ec-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="101ec-449">TotalTxErrors</span></span> | <span data-ttu-id="101ec-450">自開機後傳輸的錯誤數</span><span class="sxs-lookup"><span data-stu-id="101ec-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="101ec-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="101ec-451">TotalCollisions</span></span> | <span data-ttu-id="101ec-452">開機後經過回報 hello 網路連接埠衝突的數目</span><span class="sxs-lookup"><span data-stu-id="101ec-452">Number of collisions reported by hello network ports since boot</span></span>

 <span data-ttu-id="101ec-453">雖然此類別已執行個體化，但 LAD 不支援擷取從所有網路裝置彙總的網路計量。</span><span class="sxs-lookup"><span data-stu-id="101ec-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="101ec-454">針對特定的介面，例如 eth0，tooobtain hello 度量設定`"condition": "InstanceID=\\"eth0\\""`。</span><span class="sxs-lookup"><span data-stu-id="101ec-454">tooobtain hello metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-hello-filesystem-class"></a><span data-ttu-id="101ec-455">hello Filesystem 類別的內建度量</span><span class="sxs-lookup"><span data-stu-id="101ec-455">builtin metrics for hello Filesystem class</span></span>

<span data-ttu-id="101ec-456">hello 的度量資訊的檔案系統類別提供的檔案系統使用量的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="101ec-456">hello Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="101ec-457">因為它們可以顯示的 tooan 一般使用者 （不是根目錄），則會報告絕對值和百分比值。</span><span class="sxs-lookup"><span data-stu-id="101ec-457">Absolute and percentage values are reported as they'd be displayed tooan ordinary user (not root).</span></span>

<span data-ttu-id="101ec-458">counter</span><span class="sxs-lookup"><span data-stu-id="101ec-458">counter</span></span> | <span data-ttu-id="101ec-459">意義</span><span class="sxs-lookup"><span data-stu-id="101ec-459">Meaning</span></span>
------- | -------
<span data-ttu-id="101ec-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="101ec-460">FreeSpace</span></span> | <span data-ttu-id="101ec-461">可用磁碟空間 (位元組)</span><span class="sxs-lookup"><span data-stu-id="101ec-461">Available disk space in bytes</span></span>
<span data-ttu-id="101ec-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="101ec-462">UsedSpace</span></span> | <span data-ttu-id="101ec-463">已使用的磁碟空間 (位元組)</span><span class="sxs-lookup"><span data-stu-id="101ec-463">Used disk space in bytes</span></span>
<span data-ttu-id="101ec-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="101ec-464">PercentFreeSpace</span></span> | <span data-ttu-id="101ec-465">可用空間百分比</span><span class="sxs-lookup"><span data-stu-id="101ec-465">Percentage free space</span></span>
<span data-ttu-id="101ec-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="101ec-466">PercentUsedSpace</span></span> | <span data-ttu-id="101ec-467">已使用的空間百分比</span><span class="sxs-lookup"><span data-stu-id="101ec-467">Percentage used space</span></span>
<span data-ttu-id="101ec-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="101ec-468">PercentFreeInodes</span></span> | <span data-ttu-id="101ec-469">未使用 inode 的百分比</span><span class="sxs-lookup"><span data-stu-id="101ec-469">Percentage of unused inodes</span></span>
<span data-ttu-id="101ec-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="101ec-470">PercentUsedInodes</span></span> | <span data-ttu-id="101ec-471">所有檔案系統中已配置 (使用中) inode 總和的百分比</span><span class="sxs-lookup"><span data-stu-id="101ec-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="101ec-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="101ec-472">BytesReadPerSecond</span></span> | <span data-ttu-id="101ec-473">每秒讀取的位元組數</span><span class="sxs-lookup"><span data-stu-id="101ec-473">Bytes read per second</span></span>
<span data-ttu-id="101ec-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="101ec-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="101ec-475">每秒寫入的位元組數</span><span class="sxs-lookup"><span data-stu-id="101ec-475">Bytes written per second</span></span>
<span data-ttu-id="101ec-476">每秒位元組</span><span class="sxs-lookup"><span data-stu-id="101ec-476">BytesPerSecond</span></span> | <span data-ttu-id="101ec-477">每秒讀取或寫入的位元組數</span><span class="sxs-lookup"><span data-stu-id="101ec-477">Bytes read or written per second</span></span>
<span data-ttu-id="101ec-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="101ec-478">ReadsPerSecond</span></span> | <span data-ttu-id="101ec-479">每秒的讀取作業數</span><span class="sxs-lookup"><span data-stu-id="101ec-479">Read operations per second</span></span>
<span data-ttu-id="101ec-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="101ec-480">WritesPerSecond</span></span> | <span data-ttu-id="101ec-481">每秒的寫入作業數</span><span class="sxs-lookup"><span data-stu-id="101ec-481">Write operations per second</span></span>
<span data-ttu-id="101ec-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="101ec-482">TransfersPerSecond</span></span> | <span data-ttu-id="101ec-483">每秒的讀取或寫入作業數</span><span class="sxs-lookup"><span data-stu-id="101ec-483">Read or write operations per second</span></span>

<span data-ttu-id="101ec-484">可透過設定 `"condition": "IsAggregate=True"` 取得的所有檔案系統彙總值。</span><span class="sxs-lookup"><span data-stu-id="101ec-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="101ec-485">可透過設定 `"condition": 'Name="/mnt"'` 取得的特定已掛接檔案系統 (例如 "/mnt") 的值。</span><span class="sxs-lookup"><span data-stu-id="101ec-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-hello-disk-class"></a><span data-ttu-id="101ec-486">hello 磁碟類別的內建度量</span><span class="sxs-lookup"><span data-stu-id="101ec-486">builtin metrics for hello Disk class</span></span>

<span data-ttu-id="101ec-487">hello 磁碟類別的度量會提供磁碟裝置使用量的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="101ec-487">hello Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="101ec-488">這些統計資料套用 toohello 整個磁碟機。</span><span class="sxs-lookup"><span data-stu-id="101ec-488">These statistics apply toohello entire drive.</span></span> <span data-ttu-id="101ec-489">如果裝置上有多個檔案系統，該裝置 hello 計數器的有效地跨所有的彙總。</span><span class="sxs-lookup"><span data-stu-id="101ec-489">If there are multiple file systems on a device, hello counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="101ec-490">counter</span><span class="sxs-lookup"><span data-stu-id="101ec-490">counter</span></span> | <span data-ttu-id="101ec-491">意義</span><span class="sxs-lookup"><span data-stu-id="101ec-491">Meaning</span></span>
------- | -------
<span data-ttu-id="101ec-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="101ec-492">ReadsPerSecond</span></span> | <span data-ttu-id="101ec-493">每秒的讀取作業數</span><span class="sxs-lookup"><span data-stu-id="101ec-493">Read operations per second</span></span>
<span data-ttu-id="101ec-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="101ec-494">WritesPerSecond</span></span> | <span data-ttu-id="101ec-495">每秒的寫入作業數</span><span class="sxs-lookup"><span data-stu-id="101ec-495">Write operations per second</span></span>
<span data-ttu-id="101ec-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="101ec-496">TransfersPerSecond</span></span> | <span data-ttu-id="101ec-497">每秒的總作業數</span><span class="sxs-lookup"><span data-stu-id="101ec-497">Total operations per second</span></span>
<span data-ttu-id="101ec-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="101ec-498">AverageReadTime</span></span> | <span data-ttu-id="101ec-499">每個讀取作業的平均秒數</span><span class="sxs-lookup"><span data-stu-id="101ec-499">Average seconds per read operation</span></span>
<span data-ttu-id="101ec-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="101ec-500">AverageWriteTime</span></span> | <span data-ttu-id="101ec-501">每個寫入作業的平均秒數</span><span class="sxs-lookup"><span data-stu-id="101ec-501">Average seconds per write operation</span></span>
<span data-ttu-id="101ec-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="101ec-502">AverageTransferTime</span></span> | <span data-ttu-id="101ec-503">每個作業的平均秒數</span><span class="sxs-lookup"><span data-stu-id="101ec-503">Average seconds per operation</span></span>
<span data-ttu-id="101ec-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="101ec-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="101ec-505">已排入佇列的磁碟作業平均數</span><span class="sxs-lookup"><span data-stu-id="101ec-505">Average number of queued disk operations</span></span>
<span data-ttu-id="101ec-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="101ec-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="101ec-507">每秒讀取的位元組數</span><span class="sxs-lookup"><span data-stu-id="101ec-507">Number of bytes read per second</span></span>
<span data-ttu-id="101ec-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="101ec-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="101ec-509">每秒寫入的位元組數</span><span class="sxs-lookup"><span data-stu-id="101ec-509">Number of bytes written per second</span></span>
<span data-ttu-id="101ec-510">每秒位元組</span><span class="sxs-lookup"><span data-stu-id="101ec-510">BytesPerSecond</span></span> | <span data-ttu-id="101ec-511">每秒讀取或寫入的位元組數</span><span class="sxs-lookup"><span data-stu-id="101ec-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="101ec-512">可透過設定 `"condition": "IsAggregate=True"` 取得的所有磁碟彙總值。</span><span class="sxs-lookup"><span data-stu-id="101ec-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="101ec-513">設定特定裝置 (例如，開發人員/sdf1)，tooget 資訊`"condition": "Name=\\"/dev/sdf1\\""`。</span><span class="sxs-lookup"><span data-stu-id="101ec-513">tooget information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="101ec-514">透過 CLI 安裝與設定 LAD 3.0</span><span class="sxs-lookup"><span data-stu-id="101ec-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="101ec-515">假設您受保護的設定 hello 檔案 privateconfig.json 的檔案中，您的公用組態資訊是位在 PublicConfig.json，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="101ec-515">Assuming your protected settings are in hello file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="101ec-516">hello 命令假設您使用的 hello Azure CLI hello Azure 資源管理模式 (arm)。</span><span class="sxs-lookup"><span data-stu-id="101ec-516">hello command assumes you are using hello Azure Resource Management mode (arm) of hello Azure CLI.</span></span> <span data-ttu-id="101ec-517">tooconfigure 年輕人的傳統部署模型 (ASM) Vm，請切換太"asm 」 模式 (`azure config mode asm`)，並省略 hello 命令中的 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="101ec-517">tooconfigure LAD for classic deployment model (ASM) VMs, switch too"asm" mode (`azure config mode asm`) and omit hello resource group name in hello command.</span></span> <span data-ttu-id="101ec-518">如需詳細資訊，請參閱 hello[跨平台 CLI 文件](https://docs.microsoft.com/azure/xplat-cli-connect)。</span><span class="sxs-lookup"><span data-stu-id="101ec-518">For more information, see hello [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="101ec-519">範例 LAD 3.0 組態</span><span class="sxs-lookup"><span data-stu-id="101ec-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="101ec-520">根據 hello 之前定義，這裡的部分說明範例年輕人 3.0 延伸模組組態。</span><span class="sxs-lookup"><span data-stu-id="101ec-520">Based on hello preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="101ec-521">tooapply 範例 tooyour 本例中，您應該使用您自己的儲存體帳戶名稱、 帳戶 SAS 權杖，以及 EventHubs SAS token。</span><span class="sxs-lookup"><span data-stu-id="101ec-521">tooapply this sample tooyour case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="101ec-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="101ec-522">PrivateConfig.json</span></span>

<span data-ttu-id="101ec-523">這些私用設定會設定：</span><span class="sxs-lookup"><span data-stu-id="101ec-523">These private settings configure:</span></span>

* <span data-ttu-id="101ec-524">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="101ec-524">a storage account</span></span>
* <span data-ttu-id="101ec-525">相符的帳戶 SAS 權杖</span><span class="sxs-lookup"><span data-stu-id="101ec-525">a matching account SAS token</span></span>
* <span data-ttu-id="101ec-526">數個接收 (含 SAS 權杖的 JsonBlob 或 EventHubs)</span><span class="sxs-lookup"><span data-stu-id="101ec-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a><span data-ttu-id="101ec-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="101ec-527">PublicConfig.json</span></span>

<span data-ttu-id="101ec-528">這些公用設定會造成 LAD：</span><span class="sxs-lookup"><span data-stu-id="101ec-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="101ec-529">上傳處理器時間百分比和使用磁碟空間度量 toohello`WADMetrics*`資料表</span><span class="sxs-lookup"><span data-stu-id="101ec-529">Upload percent-processor-time and used-disk-space metrics toohello `WADMetrics*` table</span></span>
* <span data-ttu-id="101ec-530">上傳訊息從 syslog 設備 「 使用者 」 和嚴重性"info"toohello`LinuxSyslog*`資料表</span><span class="sxs-lookup"><span data-stu-id="101ec-530">Upload messages from syslog facility "user" and severity "info" toohello `LinuxSyslog*` table</span></span>
* <span data-ttu-id="101ec-531">上傳原始 OMI 查詢結果 （PercentProcessorTime 和 PercentIdleTime） toohello 名為`LinuxCPU`資料表</span><span class="sxs-lookup"><span data-stu-id="101ec-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) toohello named `LinuxCPU` table</span></span>
* <span data-ttu-id="101ec-532">上傳檔案中的 附加的行`/var/log/myladtestlog`toohello`MyLadTestLog`資料表</span><span class="sxs-lookup"><span data-stu-id="101ec-532">Upload appended lines in file `/var/log/myladtestlog` toohello `MyLadTestLog` table</span></span>

<span data-ttu-id="101ec-533">在每個案例中，也會將資料上傳至：</span><span class="sxs-lookup"><span data-stu-id="101ec-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="101ec-534">Azure Blob 儲存體 （容器名稱為 hello JsonBlob 接收中所定義）</span><span class="sxs-lookup"><span data-stu-id="101ec-534">Azure Blob storage (container name is as defined in hello JsonBlob sink)</span></span>
* <span data-ttu-id="101ec-535">EventHubs 端點 （如 hello EventHubs 接收中指定）</span><span class="sxs-lookup"><span data-stu-id="101ec-535">EventHubs endpoint (as specified in hello EventHubs sink)</span></span>

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

<span data-ttu-id="101ec-536">hello`resourceId`在 hello 組態必須符合的 hello VM 或 hello 虛擬機器規模集。</span><span class="sxs-lookup"><span data-stu-id="101ec-536">hello `resourceId` in hello configuration must match that of hello VM or hello virtual machine scale set.</span></span>

* <span data-ttu-id="101ec-537">Azure 平台度量圖表和警示知道 hello resourceId 的 hello 您正在使用的 VM。</span><span class="sxs-lookup"><span data-stu-id="101ec-537">Azure platform metrics charting and alerting knows hello resourceId of hello VM you're working on.</span></span> <span data-ttu-id="101ec-538">預期 toofind hello 資料的 VM 使用 hello resourceId hello 查閱索引鍵。</span><span class="sxs-lookup"><span data-stu-id="101ec-538">It expects toofind hello data for your VM using hello resourceId hello lookup key.</span></span>
* <span data-ttu-id="101ec-539">如果您使用 Azure 自動調整規模，hello 自動調整規模設定中的 hello resourceId 必須符合 hello resourceId 年輕人所使用。</span><span class="sxs-lookup"><span data-stu-id="101ec-539">If you use Azure autoscale, hello resourceId in hello autoscale configuration must match hello resourceId used by LAD.</span></span>
* <span data-ttu-id="101ec-540">hello resourceId 是內建的 JsonBlobs 年輕人所撰寫的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="101ec-540">hello resourceId is built into hello names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="101ec-541">檢視資料</span><span class="sxs-lookup"><span data-stu-id="101ec-541">View your data</span></span>

<span data-ttu-id="101ec-542">使用 Azure 入口網站 tooview hello 的效能資料，或設定警示：</span><span class="sxs-lookup"><span data-stu-id="101ec-542">Use hello Azure portal tooview performance data or set alerts:</span></span>

![image](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="101ec-544">hello`performanceCounters`資料一律儲存在 Azure 儲存體資料表。</span><span class="sxs-lookup"><span data-stu-id="101ec-544">hello `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="101ec-545">Azure 儲存體 API 適用於許多語言與平台。</span><span class="sxs-lookup"><span data-stu-id="101ec-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="101ec-546">傳送 tooJsonBlob 接收的資料會儲存在名為 hello 中的 hello 儲存體帳戶中的 blob[保護設定](#protected-settings)。</span><span class="sxs-lookup"><span data-stu-id="101ec-546">Data sent tooJsonBlob sinks is stored in blobs in hello storage account named in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="101ec-547">您可以使用 使用任何 Azure Blob 儲存體 Api hello blob 資料。</span><span class="sxs-lookup"><span data-stu-id="101ec-547">You can consume hello blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="101ec-548">此外，您可以使用這些 UI 工具 tooaccess hello 資料在 Azure 儲存體：</span><span class="sxs-lookup"><span data-stu-id="101ec-548">In addition, you can use these UI tools tooaccess hello data in Azure Storage:</span></span>

* <span data-ttu-id="101ec-549">Visual Studio 伺服器總管。</span><span class="sxs-lookup"><span data-stu-id="101ec-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="101ec-550">[Microsoft Azure 儲存體總管](https://azurestorageexplorer.codeplex.com/ "Azure 儲存體總管")。</span><span class="sxs-lookup"><span data-stu-id="101ec-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="101ec-551">Microsoft Azure 儲存體總管工作階段的此快照顯示 hello 產生 Azure 儲存體資料表和容器從測試 VM 上的正確設定年輕人 3.0 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="101ec-551">This snapshot of a Microsoft Azure Storage Explorer session shows hello generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="101ec-552">hello 映像不完全符合 hello[範例年輕人 3.0 組態](#an-example-lad-30-configuration)。</span><span class="sxs-lookup"><span data-stu-id="101ec-552">hello image doesn't match exactly with hello [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![image](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="101ec-554">請參閱相關的 hello [EventHubs 文件](../../event-hubs/event-hubs-what-is-event-hubs.md)toolearn tooconsume 訊息發佈 tooan EventHubs 端點的方式。</span><span class="sxs-lookup"><span data-stu-id="101ec-554">See hello relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn how tooconsume messages published tooan EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="101ec-555">後續步驟</span><span class="sxs-lookup"><span data-stu-id="101ec-555">Next steps</span></span>

* <span data-ttu-id="101ec-556">建立度量的警示[Azure 監視器](../../monitoring-and-diagnostics/insights-alerts-portal.md)hello 度量收集。</span><span class="sxs-lookup"><span data-stu-id="101ec-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for hello metrics you collect.</span></span>
* <span data-ttu-id="101ec-557">為您的計量建立[監視圖表](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="101ec-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="101ec-558">了解如何太[建立虛擬機器規模集](/azure/virtual-machines/linux/tutorial-create-vmss)使用度量的 toocontrol 自動調整。</span><span class="sxs-lookup"><span data-stu-id="101ec-558">Learn how too[create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics toocontrol autoscaling.</span></span>
