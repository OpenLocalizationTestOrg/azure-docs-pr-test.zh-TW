---
title: "Azure 計算 - Linux 診斷擴充功能 | Microsoft Docs"
description: "如何設定 Azure Linux 診斷擴充功能 (LAD) 從 Azure 中執行的 Linux VM 中收集計量並記錄事件。"
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 525d706bd709ae72f2dca1c21e06db533ccf32b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-linux-diagnostic-extension-to-monitor-metrics-and-logs"></a><span data-ttu-id="4f2b9-103">使用 Linux 診斷擴充功能監視計量與記錄</span><span class="sxs-lookup"><span data-stu-id="4f2b9-103">Use Linux Diagnostic Extension to monitor metrics and logs</span></span>

<span data-ttu-id="4f2b9-104">本文件說明 3.0 版與更新版本的 Linux 診斷擴充功能。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-104">This document describes version 3.0 and newer of the Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f2b9-105">如需 2.3 版與更舊版本的資訊，請參閱[本文件](./classic/diagnostic-extension-v2.md)。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="4f2b9-106">簡介</span><span class="sxs-lookup"><span data-stu-id="4f2b9-106">Introduction</span></span>

<span data-ttu-id="4f2b9-107">Linux 診斷擴充功能可協助使用者監視在 Microsoft Azure 上執行的 Linux VM 其健康情況。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-107">The Linux Diagnostic Extension helps a user monitor the health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="4f2b9-108">它可提供下列功能：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-108">It has the following capabilities:</span></span>

* <span data-ttu-id="4f2b9-109">從 VM 收集系統效能計量，並儲存在所指定儲存體帳戶的特定資料表中。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-109">Collects system performance metrics from the VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="4f2b9-110">從 Syslog 擷取記錄事件，並儲存在所指定儲存體帳戶的特定資料表中。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-110">Retrieves log events from syslog and stores them in a specific table in the designated storage account.</span></span>
* <span data-ttu-id="4f2b9-111">讓使用者自訂要收集並上傳的資料計量。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-111">Enables users to customize the data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="4f2b9-112">可讓使用者自訂 Syslog 設備，以及要收集並上傳的事件其嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-112">Enables users to customize the syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="4f2b9-113">讓使用者將指定的記錄檔上傳至指定的儲存體資料表。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-113">Enables users to upload specified log files to a designated storage table.</span></span>
* <span data-ttu-id="4f2b9-114">支援傳送計量與事件記錄至所指定儲存體帳戶中的任意 EventHub 端點與 JSON 格式的 blob。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-114">Supports sending metrics and log events to arbitrary EventHub endpoints and JSON-formatted blobs in the designated storage account.</span></span>

<span data-ttu-id="4f2b9-115">此擴充功能適用於這兩個 Azure 部署模型。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-the-extension-in-your-vm"></a><span data-ttu-id="4f2b9-116">在 VM 中安裝擴充功能</span><span class="sxs-lookup"><span data-stu-id="4f2b9-116">Installing the extension in your VM</span></span>

<span data-ttu-id="4f2b9-117">您可以使用 Azure PowerShell Cmdlet、Azure CLI 指令碼或 Azure 部署範本啟用此擴充功能。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-117">You can enable this extension by using the Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="4f2b9-118">如需詳細資訊，請參閱[擴充功能](./extensions-features.md)。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="4f2b9-119">Azure 入口網站無法用於啟用或設定 LAD 3.0。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-119">The Azure portal cannot be used to enable or configure LAD 3.0.</span></span> <span data-ttu-id="4f2b9-120">相反地，它會安裝並設定 2.3 版。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="4f2b9-121">Azure 入口網站圖形和警示會使用這兩個版本中的資料。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-121">Azure portal graphs and alerts work with data from both versions of the extension.</span></span>

<span data-ttu-id="4f2b9-122">這些安裝指示與[可下載範例組態](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json)可設定 LAD 3.0 以：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="4f2b9-123">擷取與儲存 LAD 2.3 所提供的相同計量；</span><span class="sxs-lookup"><span data-stu-id="4f2b9-123">capture and store the same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="4f2b9-124">擷取一組實用的檔案系統計量，這是 LAD 3.0 的新功能；</span><span class="sxs-lookup"><span data-stu-id="4f2b9-124">capture a useful set of file system metrics, new to LAD 3.0;</span></span>
* <span data-ttu-id="4f2b9-125">擷取 LAD 2.3 啟用的預設 Syslog 集合；</span><span class="sxs-lookup"><span data-stu-id="4f2b9-125">capture the default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="4f2b9-126">讓 Azure 入口網站能夠對 VM 計量繪製圖表與發出警示。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-126">enable the Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="4f2b9-127">可下載組態只是範例，可修改以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-127">The downloadable configuration is just an example; modify it to suit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4f2b9-128">必要條件</span><span class="sxs-lookup"><span data-stu-id="4f2b9-128">Prerequisites</span></span>

* <span data-ttu-id="4f2b9-129">**Azure Linux Agent 2.2.0 版或更新版本**。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="4f2b9-130">大部分的 Azure VM Linux 資源庫映像包含版本 2.2.7 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="4f2b9-131">執行 `/usr/sbin/waagent -version` 以確認安裝在 VM 上的版本。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-131">Run `/usr/sbin/waagent -version` to confirm the version installed on the VM.</span></span> <span data-ttu-id="4f2b9-132">如果 VM 執行的是舊版客體代理程式，請依照[這些指示](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent)更新。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-132">If the VM is running an older version of the guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) to update it.</span></span>
* <span data-ttu-id="4f2b9-133">**Azure CLI**。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-133">**Azure CLI**.</span></span> <span data-ttu-id="4f2b9-134">在您電腦上[設定 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) 環境。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-134">[Set up the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="4f2b9-135">Wget 命令，如果您沒有：請執行 `sudo apt-get install wget`。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-135">The wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="4f2b9-136">現有的 Azure 訂用帳戶與其中現有的儲存體帳戶以儲存資料。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-136">An existing Azure subscription and an existing storage account within it to store the data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="4f2b9-137">範例安裝</span><span class="sxs-lookup"><span data-stu-id="4f2b9-137">Sample installation</span></span>

<span data-ttu-id="4f2b9-138">在前三行中填入正確參數，然後以根使用者身分執行此指令碼：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-138">Fill in the correct parameters on the first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login to Azure first before anything else
az login

# Select the subscription containing the storage account
az account set --subscription <your_azure_subscription_id>

# Download the sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build the VM resource ID. Replace storage account name and resource ID in the public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build the protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure to install and enable the extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="4f2b9-139">範例組態的 URL 及其內容可能會變更。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-139">The URL for the sample configuration, and its contents, are subject to change.</span></span> <span data-ttu-id="4f2b9-140">下載入口網站設定 JSON 檔案的複本，並針對您的需求自訂。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-140">Download a copy of the portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="4f2b9-141">您建構的任何範本或自動化項目應使用您自己的複本，而非每次都要下載該 URL。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-the-extension-settings"></a><span data-ttu-id="4f2b9-142">更新擴充功能設定</span><span class="sxs-lookup"><span data-stu-id="4f2b9-142">Updating the extension settings</span></span>

<span data-ttu-id="4f2b9-143">在您變更自己的受保護或公開設定後，請執行相同的命令將設定部署到 VM。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-143">After you've changed your Protected or Public settings, deploy them to the VM by running the same command.</span></span> <span data-ttu-id="4f2b9-144">如果設定有任何的變更，系統會將更新後設定傳送至擴充功能。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-144">If anything changed in the settings, the updated settings are sent to the extension.</span></span> <span data-ttu-id="4f2b9-145">LAD 會重新載入組態並自行重新啟動。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-145">LAD reloads the configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-the-extension"></a><span data-ttu-id="4f2b9-146">自舊版擴充功能移轉</span><span class="sxs-lookup"><span data-stu-id="4f2b9-146">Migration from previous versions of the extension</span></span>

<span data-ttu-id="4f2b9-147">擴充功能的最新版本是 **3.0**。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-147">The latest version of the extension is **3.0**.</span></span> <span data-ttu-id="4f2b9-148">**任何舊版 (2.x) 皆已被取代，並會 2018 年 7 月 31 日停止發行**。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f2b9-149">此擴充功能為擴充功能組態帶來突破性的改變。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-149">This extension introduces breaking changes to the configuration of the extension.</span></span> <span data-ttu-id="4f2b9-150">這一項改變可提升擴充功能安全性，也因此不會再維持與 2.x 的回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-150">One such change was made to improve the security of the extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="4f2b9-151">此外，此擴充功能的擴充功能發行者與 2.x 版的發行者不同。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-151">Also, the Extension Publisher for this extension is different than the publisher for the 2.x versions.</span></span>
>
> <span data-ttu-id="4f2b9-152">若要從 2.x 移轉至新版的擴充功能，您必須解除安裝舊版擴充功能 (在舊發行者名稱下)，然後安裝 3 版的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-152">To migrate from 2.x to this new version of the extension, you must uninstall the old extension (under the old publisher name), then install version 3 of the extension.</span></span>

<span data-ttu-id="4f2b9-153">建議：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-153">Recommendations:</span></span>

* <span data-ttu-id="4f2b9-154">透過啟用的自動次要版本升級安裝擴充功能。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-154">Install the extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="4f2b9-155">如果您正透過 Azure XPLAT CLI 或 Powershell 安裝擴充功能，請在傳統部署模型 VM 上指定版本為「3.*」。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-155">On classic deployment model VMs, specify '3.*' as the version if you are installing the extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="4f2b9-156">在 Azure Resource Manager 部署模型 VM 上的 VM 部署範本中包含「"autoUpgradeMinorVersion": true」。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in the VM deployment template.</span></span>
* <span data-ttu-id="4f2b9-157">為 LAD 3.0 使用新/不同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="4f2b9-158">LAD 2.3 與 LAD 3.0 之間些許不相容，讓共用帳戶變得麻煩：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="4f2b9-159">LAD 3.0 會將 Syslog 事件儲存在採用不同名稱的資料表中。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="4f2b9-160">`builtin` 計量的 counterSpecifier 字串在 LAD 3.0 中不同。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-160">The counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="4f2b9-161">受保護的設定</span><span class="sxs-lookup"><span data-stu-id="4f2b9-161">Protected settings</span></span>

<span data-ttu-id="4f2b9-162">這一組的組態資訊包含敏感性資訊，應加以保護以防遭公開檢視，例如儲存體認證。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="4f2b9-163">這些設定會以加密的形式傳輸到擴充功能並加以儲存。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-163">These settings are transmitted to and stored by the extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "the storage account to receive data",
    "storageAccountEndPoint": "the hostname suffix for the cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="4f2b9-164">名稱</span><span class="sxs-lookup"><span data-stu-id="4f2b9-164">Name</span></span> | <span data-ttu-id="4f2b9-165">值</span><span class="sxs-lookup"><span data-stu-id="4f2b9-165">Value</span></span>
---- | -----
<span data-ttu-id="4f2b9-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="4f2b9-166">storageAccountName</span></span> | <span data-ttu-id="4f2b9-167">擴充功能寫入資料的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-167">The name of the storage account in which data is written by the extension.</span></span>
<span data-ttu-id="4f2b9-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="4f2b9-168">storageAccountEndPoint</span></span> | <span data-ttu-id="4f2b9-169">(選擇性) 可識別儲存體帳戶所在雲端的端點。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-169">(optional) The endpoint identifying the cloud in which the storage account exists.</span></span> <span data-ttu-id="4f2b9-170">如果沒有此設定，LAD 會預設為 Azure 公用雲端，`https://core.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-170">If this setting is absent, LAD defaults to the Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="4f2b9-171">若要使用 Azure 德國、Azure Government 或 Azure 中國中的儲存體帳戶，請相應地設定此值。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-171">To use a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="4f2b9-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="4f2b9-172">storageAccountSasToken</span></span> | <span data-ttu-id="4f2b9-173">Blob 與資料表服務 (`ss='bt'`) 的 [帳戶 SAS 權杖](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/)，適用於容器與物件 (`srt='co'`)，可授與新增、建立、列示、更新與寫入權限 (`sp='acluw'`)。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable to containers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="4f2b9-174">請*勿*包含前置問號 (?)。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-174">Do *not* include the leading question-mark (?).</span></span>
<span data-ttu-id="4f2b9-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="4f2b9-175">mdsdHttpProxy</span></span> | <span data-ttu-id="4f2b9-176">(選擇性) 啟用擴充功能以連線所指定儲存體帳戶和端點時所需的 HTTP proxy 資訊。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-176">(optional) HTTP proxy information needed to enable the extension to connect to the specified storage account and endpoint.</span></span>
<span data-ttu-id="4f2b9-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="4f2b9-177">sinksConfig</span></span> | <span data-ttu-id="4f2b9-178">(選擇性) 可將計量與事件傳遞至的替代目的地詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-178">(optional) Details of alternative destinations to which metrics and events can be delivered.</span></span> <span data-ttu-id="4f2b9-179">以下各節包含擴充功能所支援每個資料接收的特定詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-179">The specific details of each data sink supported by the extension are covered in the sections that follow.</span></span>

<span data-ttu-id="4f2b9-180">您可以輕鬆地透過 Azure 入口網站建構所需的 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-180">You can easily construct the required SAS token through the Azure portal.</span></span>

1. <span data-ttu-id="4f2b9-181">選取您要將擴充功能寫入的一般用途儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="4f2b9-181">Select the general-purpose storage account to which you want the extension to write</span></span>
1. <span data-ttu-id="4f2b9-182">從左側功能表的 [設定] 部分中選取 [共用存取簽章]</span><span class="sxs-lookup"><span data-stu-id="4f2b9-182">Select "Shared access signature" from the Settings part of the left menu</span></span>
1. <span data-ttu-id="4f2b9-183">依前述設定適當的區段</span><span class="sxs-lookup"><span data-stu-id="4f2b9-183">Make the appropriate sections as previously described</span></span>
1. <span data-ttu-id="4f2b9-184">按一下 [產生 SAS] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-184">Click the "Generate SAS" button.</span></span>

![image](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="4f2b9-186">將產生的 SAS 複製到 [storageAccountSasToken] 欄位；移除前置問號 ("?")。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-186">Copy the generated SAS into the storageAccountSasToken field; remove the leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="4f2b9-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="4f2b9-187">sinksConfig</span></span>

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

<span data-ttu-id="4f2b9-188">此選擇性區段會定義額外的目的地，讓擴充功能可將收集到的資訊傳送到該目的地。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-188">This optional section defines additional destinations to which the extension sends the information it collects.</span></span> <span data-ttu-id="4f2b9-189">"sink" 陣列包含每個額外資料接收的物件。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-189">The "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="4f2b9-190">"type" 屬性可決定物件中的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-190">The "type" attribute determines the other attributes in the object.</span></span>

<span data-ttu-id="4f2b9-191">元素</span><span class="sxs-lookup"><span data-stu-id="4f2b9-191">Element</span></span> | <span data-ttu-id="4f2b9-192">值</span><span class="sxs-lookup"><span data-stu-id="4f2b9-192">Value</span></span>
------- | -----
<span data-ttu-id="4f2b9-193">名稱</span><span class="sxs-lookup"><span data-stu-id="4f2b9-193">name</span></span> | <span data-ttu-id="4f2b9-194">用來在擴充功能組態中的其他位置參考此接收的字串。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-194">A string used to refer to this sink elsewhere in the extension configuration.</span></span>
<span data-ttu-id="4f2b9-195">類型</span><span class="sxs-lookup"><span data-stu-id="4f2b9-195">type</span></span> | <span data-ttu-id="4f2b9-196">正在定義的接收類型。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-196">The type of sink being defined.</span></span> <span data-ttu-id="4f2b9-197">決定此類型執行個體中的其他值 (若有的話)。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-197">Determines the other values (if any) in instances of this type.</span></span>

<span data-ttu-id="4f2b9-198">3.0 版的 Linux 診斷擴充功能支援兩種接收類型：EventHub 與 JsonBlob。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-198">Version 3.0 of the Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="the-eventhub-sink"></a><span data-ttu-id="4f2b9-199">EventHub 接收</span><span class="sxs-lookup"><span data-stu-id="4f2b9-199">The EventHub sink</span></span>

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

<span data-ttu-id="4f2b9-200">"sasURL" 項目包含完整的 URL，包括 SAS 權杖，適用於應將資料發佈至的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-200">The "sasURL" entry contains the full URL, including SAS token, for the Event Hub to which data should be published.</span></span> <span data-ttu-id="4f2b9-201">LAD 需要 SAS 命名可啟用 Send 宣告的原則。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-201">LAD requires a SAS naming a policy that enables the Send claim.</span></span> <span data-ttu-id="4f2b9-202">例如：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-202">An example:</span></span>

* <span data-ttu-id="4f2b9-203">建立名為 `contosohub` 的事件中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="4f2b9-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="4f2b9-204">在名為 `syslogmsgs` 的命名空間建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="4f2b9-204">Create an Event Hub in the namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="4f2b9-205">在啟用 Send 宣告且名為 `writer` 的事件中樞上建立共用存取原則</span><span class="sxs-lookup"><span data-stu-id="4f2b9-205">Create a Shared access policy on the Event Hub named `writer` that enables the Send claim</span></span>

<span data-ttu-id="4f2b9-206">如果您已建立一個在 2018 年 1 月 1 日 UTC 午夜之前會維持良好的 SAS，則 sasURL 值會是：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-206">If you created a SAS good until midnight UTC on January 1, 2018, the sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="4f2b9-207">如需為事件中樞產生 SAS 權杖的相關詳細資訊，請參閱[本網頁](../../event-hubs/event-hubs-authentication-and-security-model-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="the-jsonblob-sink"></a><span data-ttu-id="4f2b9-208">JsonBlob 接收</span><span class="sxs-lookup"><span data-stu-id="4f2b9-208">The JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="4f2b9-209">導向至 JsonBlob 的資料儲存在 Azure 儲存體的 Blob 中。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-209">Data directed to a JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="4f2b9-210">LAD 的每個執行個體每小時會為每個接收名稱建立 Blob。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="4f2b9-211">每個 Blob 一律包含物件的語法有效 JSON 陣列。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="4f2b9-212">新項目會自動新增至陣列中。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-212">New entries are atomically added to the array.</span></span> <span data-ttu-id="4f2b9-213">Blob 會儲存在與接收相同名稱的容器中。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-213">Blobs are stored in a container with the same name as the sink.</span></span> <span data-ttu-id="4f2b9-214">Blob 容器名稱的 Azure 儲存體規則也適用於 JsonBlob 接收的名稱：3 到 63 個小寫英字數 ASCII 字元或破折號。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-214">The Azure storage rules for blob container names apply to the names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="4f2b9-215">公用設定</span><span class="sxs-lookup"><span data-stu-id="4f2b9-215">Public settings</span></span>

<span data-ttu-id="4f2b9-216">此結構包含各種設定區段，可控制擴充功能收集的資訊。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-216">This structure contains various blocks of settings that control the information collected by the extension.</span></span> <span data-ttu-id="4f2b9-217">每個設定皆為選擇性。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-217">Each setting is optional.</span></span> <span data-ttu-id="4f2b9-218">如果您指定 `ladCfg`，則亦須指定 `StorageAccount`。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "the storage account to receive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="4f2b9-219">元素</span><span class="sxs-lookup"><span data-stu-id="4f2b9-219">Element</span></span> | <span data-ttu-id="4f2b9-220">值</span><span class="sxs-lookup"><span data-stu-id="4f2b9-220">Value</span></span>
------- | -----
<span data-ttu-id="4f2b9-221">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="4f2b9-221">StorageAccount</span></span> | <span data-ttu-id="4f2b9-222">擴充功能寫入資料的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-222">The name of the storage account in which data is written by the extension.</span></span> <span data-ttu-id="4f2b9-223">必須與在[保護設定](#protected-settings)中指定的名稱相同。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-223">Must be the same name as is specified in the [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="4f2b9-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="4f2b9-224">mdsdHttpProxy</span></span> | <span data-ttu-id="4f2b9-225">(選擇性) 與[受保護的設定](#protected-settings)相同。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-225">(optional) Same as in the [Protected settings](#protected-settings).</span></span> <span data-ttu-id="4f2b9-226">公用值會被私用值 (若有設定) 覆寫。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-226">The public value is overridden by the private value, if set.</span></span> <span data-ttu-id="4f2b9-227">將包含祕密 (例如密碼) 的 Proxy 設定設置在[受保護的設定](#protected-settings)中。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-227">Place proxy settings that contain a secret, such as a password, in the [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="4f2b9-228">以下各節會詳細說明其餘的元素。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-228">The remaining elements are described in detail in the following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="4f2b9-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="4f2b9-229">ladCfg</span></span>

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

<span data-ttu-id="4f2b9-230">此選擇性結構會控制計量與記錄的收集，以傳遞至 Azure 計量與其他資料接收。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-230">This optional structure controls the gathering of metrics and logs for delivery to the Azure Metrics service and to other data sinks.</span></span> <span data-ttu-id="4f2b9-231">您必須指定 `performanceCounters` 或 `syslogEvents` 或是兩者。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="4f2b9-232">您必須指定 `metrics` 結構。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-232">You must specify the `metrics` structure.</span></span>

<span data-ttu-id="4f2b9-233">元素</span><span class="sxs-lookup"><span data-stu-id="4f2b9-233">Element</span></span> | <span data-ttu-id="4f2b9-234">值</span><span class="sxs-lookup"><span data-stu-id="4f2b9-234">Value</span></span>
------- | -----
<span data-ttu-id="4f2b9-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="4f2b9-235">eventVolume</span></span> | <span data-ttu-id="4f2b9-236">(選擇性) 控制在儲存體資料表中建立的分割區數目。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-236">(optional) Controls the number of partitions created within the storage table.</span></span> <span data-ttu-id="4f2b9-237">必須是 `"Large"`、`"Medium"` 或 `"Small"` 的其中之一。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="4f2b9-238">若未指定，則預設值為 `"Medium"`。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-238">If not specified, the default value is `"Medium"`.</span></span>
<span data-ttu-id="4f2b9-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="4f2b9-239">sampleRateInSeconds</span></span> | <span data-ttu-id="4f2b9-240">(選擇性) 原始 (未彙總) 計量集合之間的預設間隔。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-240">(optional) The default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="4f2b9-241">支援的最小採樣速率為 15 秒。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-241">The smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="4f2b9-242">若未指定，則預設值為 `15`。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-242">If not specified, the default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="4f2b9-243">metrics</span><span class="sxs-lookup"><span data-stu-id="4f2b9-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="4f2b9-244">元素</span><span class="sxs-lookup"><span data-stu-id="4f2b9-244">Element</span></span> | <span data-ttu-id="4f2b9-245">值</span><span class="sxs-lookup"><span data-stu-id="4f2b9-245">Value</span></span>
------- | -----
<span data-ttu-id="4f2b9-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="4f2b9-246">resourceId</span></span> | <span data-ttu-id="4f2b9-247">VM 所屬之 VM 或虛擬機器擴展集的 Azure Resource Manager 資源 ID。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-247">The Azure Resource Manager resource ID of the VM or of the virtual machine scale set to which the VM belongs.</span></span> <span data-ttu-id="4f2b9-248">如果在組態中使用任何的 JsonBlob 接收，則亦須指定此設定。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-248">This setting must be also specified if any JsonBlob sink is used in the configuration.</span></span>
<span data-ttu-id="4f2b9-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="4f2b9-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="4f2b9-250">系統會計算彙總計量的頻率並傳輸至 Azure 計量 (以 IS 8601 時間間隔表示)。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-250">The frequency at which aggregate metrics are to be computed and transferred to Azure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="4f2b9-251">最小傳輸期間為 60 秒，亦即 PT1M。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-251">The smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="4f2b9-252">您必須指定至少一個 scheduledTransferPeriod。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="4f2b9-253">系統每隔 15 秒或以為計數器明確定義的採樣速率收集在 performanceCounters 區段中指定的計量樣本。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-253">Samples of the metrics specified in the performanceCounters section are collected every 15 seconds or at the sample rate explicitly defined for the counter.</span></span> <span data-ttu-id="4f2b9-254">如果顯示多個 scheduledTransferPeriod 頻率 (如範例所述)，則會獨立計算每個彙總。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-254">If multiple scheduledTransferPeriod frequencies appear (as in the example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="4f2b9-255">performanceCounters</span><span class="sxs-lookup"><span data-stu-id="4f2b9-255">performanceCounters</span></span>

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

<span data-ttu-id="4f2b9-256">此選擇性區段會控制計量的收集。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-256">This optional section controls the collection of metrics.</span></span> <span data-ttu-id="4f2b9-257">系統會彙總每個 [scheduledTransferPeriod](#metrics) 原始樣本以產生以下的值：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) to produce these values:</span></span>

* <span data-ttu-id="4f2b9-258">平均值</span><span class="sxs-lookup"><span data-stu-id="4f2b9-258">mean</span></span>
* <span data-ttu-id="4f2b9-259">minimum</span><span class="sxs-lookup"><span data-stu-id="4f2b9-259">minimum</span></span>
* <span data-ttu-id="4f2b9-260">maximum</span><span class="sxs-lookup"><span data-stu-id="4f2b9-260">maximum</span></span>
* <span data-ttu-id="4f2b9-261">上次收集的值</span><span class="sxs-lookup"><span data-stu-id="4f2b9-261">last-collected value</span></span>
* <span data-ttu-id="4f2b9-262">用於計算彙總的原始樣本計數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-262">count of raw samples used to compute the aggregate</span></span>

<span data-ttu-id="4f2b9-263">元素</span><span class="sxs-lookup"><span data-stu-id="4f2b9-263">Element</span></span> | <span data-ttu-id="4f2b9-264">值</span><span class="sxs-lookup"><span data-stu-id="4f2b9-264">Value</span></span>
------- | -----
<span data-ttu-id="4f2b9-265">sinks</span><span class="sxs-lookup"><span data-stu-id="4f2b9-265">sinks</span></span> | <span data-ttu-id="4f2b9-266">(選擇性) 以逗號分隔的接收名稱清單，LAD 會將彙總的計量結果傳送至此清單。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-266">(optional) A comma-separated list of names of sinks to which LAD sends aggregated metric results.</span></span> <span data-ttu-id="4f2b9-267">系統會將所有彙總的計量發佈至每個列出的接收。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-267">All aggregated metrics are published to each listed sink.</span></span> <span data-ttu-id="4f2b9-268">請參閱 [sinksConfig](#sinksconfig)。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="4f2b9-269">範例： `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="4f2b9-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="4f2b9-270">類型</span><span class="sxs-lookup"><span data-stu-id="4f2b9-270">type</span></span> | <span data-ttu-id="4f2b9-271">識別計量的實際提供者。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-271">Identifies the actual provider of the metric.</span></span>
<span data-ttu-id="4f2b9-272">class</span><span class="sxs-lookup"><span data-stu-id="4f2b9-272">class</span></span> | <span data-ttu-id="4f2b9-273">與 "counter" 一起使用，可識別提供者命名空間內的特定計量。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-273">Together with "counter", identifies the specific metric within the provider's namespace.</span></span>
<span data-ttu-id="4f2b9-274">counter</span><span class="sxs-lookup"><span data-stu-id="4f2b9-274">counter</span></span> | <span data-ttu-id="4f2b9-275">與 "class" 一起使用，可識別提供者命名空間內的特定計量。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-275">Together with "class", identifies the specific metric within the provider's namespace.</span></span>
<span data-ttu-id="4f2b9-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="4f2b9-276">counterSpecifier</span></span> | <span data-ttu-id="4f2b9-277">可識別 Azure 計量命名空間內的特定計量。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-277">Identifies the specific metric within the Azure Metrics namespace.</span></span>
<span data-ttu-id="4f2b9-278">condition</span><span class="sxs-lookup"><span data-stu-id="4f2b9-278">condition</span></span> | <span data-ttu-id="4f2b9-279">(選擇性) 選取會套用計量之物件的特定執行個體，或選取該物件所有執行個體的彙總。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-279">(optional) Selects a specific instance of the object to which the metric applies or selects the aggregation across all instances of that object.</span></span> <span data-ttu-id="4f2b9-280">如需詳細資訊，請參閱[`builtin`計量定義](#metrics-supported-by-builtin)。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-280">For more information, see the [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="4f2b9-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="4f2b9-281">sampleRate</span></span> | <span data-ttu-id="4f2b9-282">IS 8601 間隔，可設定收集此計量原始樣本的速率。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-282">IS 8601 interval that sets the rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="4f2b9-283">如果未設定，則會由 [sampleRateInSeconds](#ladcfg) 的值設定收集間隔。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-283">If not set, the collection interval is set by the value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="4f2b9-284">支援的最短採樣速率為 15 秒 (PT15S)。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-284">The shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="4f2b9-285">unit</span><span class="sxs-lookup"><span data-stu-id="4f2b9-285">unit</span></span> | <span data-ttu-id="4f2b9-286">應為以下字串之一："Count"、"Bytes"、"Seconds"、"Percent"、"CountPerSecond"、"BytesPerSecond"、"Millisecond"。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="4f2b9-287">定義計量的單位。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-287">Defines the unit for the metric.</span></span> <span data-ttu-id="4f2b9-288">收集資料的取用者預期收集的資料值符合這個單位。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-288">Consumers of the collected data expect the collected data values to match this unit.</span></span> <span data-ttu-id="4f2b9-289">LAD 會忽略此欄位。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-289">LAD ignores this field.</span></span>
<span data-ttu-id="4f2b9-290">displayName</span><span class="sxs-lookup"><span data-stu-id="4f2b9-290">displayName</span></span> | <span data-ttu-id="4f2b9-291">在 Azure 計量中要附加至此資料的標籤 (採用相關聯地區設定所指定的語言)。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-291">The label (in the language specified by the associated locale setting) to be attached to this data in Azure Metrics.</span></span> <span data-ttu-id="4f2b9-292">LAD 會忽略此欄位。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-292">LAD ignores this field.</span></span>

<span data-ttu-id="4f2b9-293">counterSpecifier 是任意的識別碼。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-293">The counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="4f2b9-294">如 Azure 入口網站的圖表與警示功能等計量的使用者，會使用 counterSpecifier 作為識別計量或計量執行個體的「鑰匙」。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-294">Consumers of metrics, like the Azure portal charting and alerting feature, use counterSpecifier as the "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="4f2b9-295">對於 `builtin` 計量，建議您使用開頭為 `/builtin/` 的 counterSpecifier 值。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="4f2b9-296">如果您正在收集計量的特定執行個體，建議您將執行個體的識別碼附加至 counterSpecifier 值。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-296">If you are collecting a specific instance of a metric, we recommend you attach the identifier of the instance to the counterSpecifier value.</span></span> <span data-ttu-id="4f2b9-297">部分範例如下：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-297">Some examples:</span></span>

* <span data-ttu-id="4f2b9-298">`/builtin/Processor/PercentIdleTime` - 所有核心的平均閒置時間</span><span class="sxs-lookup"><span data-stu-id="4f2b9-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="4f2b9-299">`/builtin/Disk/FreeSpace(/mnt)` - /mnt 檔案系統的可用空間</span><span class="sxs-lookup"><span data-stu-id="4f2b9-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for the /mnt filesystem</span></span>
* <span data-ttu-id="4f2b9-300">`/builtin/Disk/FreeSpace` - 所有已掛接檔案系統的平均可用空間</span><span class="sxs-lookup"><span data-stu-id="4f2b9-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="4f2b9-301">LAD 或 Azure 入口網站皆不預期 counterSpecifier 值符合任何模式。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-301">Neither LAD nor the Azure portal expects the counterSpecifier value to match any pattern.</span></span> <span data-ttu-id="4f2b9-302">應與您建構 counterSpecifier 值的方式一致。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="4f2b9-303">當您指定 `performanceCounters` 時，LAD 一律將資料寫入 Azure 儲存體中的資料表。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-303">When you specify `performanceCounters`, LAD always writes data to a table in Azure storage.</span></span> <span data-ttu-id="4f2b9-304">您可以將相同的資料寫入 JSON Blob 和/或事件中樞，但您無法禁止將資料儲存至資料表。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-304">You can have the same data written to JSON blobs and/or Event Hubs, but you cannot disable storing data to a table.</span></span> <span data-ttu-id="4f2b9-305">診斷擴充功能中所有設定為使用相同儲存體帳戶名稱與端點的執行個體，會將其計量與記錄新增至相同的資料表。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-305">All instances of the diagnostic extension configured to use the same storage account name and endpoint add their metrics and logs to the same table.</span></span> <span data-ttu-id="4f2b9-306">如果有過多的 VM 寫入相同的資料表分割區，Azure 會將這些寫入節流至該分割區。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-306">If too many VMs are writing to the same table partition, Azure can throttle writes to that partition.</span></span> <span data-ttu-id="4f2b9-307">eventVolume 設定會造成這些項目散布在 1 (小)、10 (中) 或 100 (大) 個不同的分割區。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-307">The eventVolume setting causes entries to be spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="4f2b9-308">通常「中」便足以確定不會將流量節流。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-308">Usually, "Medium" is sufficient to ensure traffic is not throttled.</span></span> <span data-ttu-id="4f2b9-309">Azure 入口網站的 Azure 計量功能會使用此資料表中的資料產生圖形或觸發警示。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-309">The Azure Metrics feature of the Azure portal uses the data in this table to produce graphs or to trigger alerts.</span></span> <span data-ttu-id="4f2b9-310">資料表名稱是這些字串的串連：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-310">The table name is the concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="4f2b9-311">儲存在資料表中彙總值的 "scheduledTransferPeriod"</span><span class="sxs-lookup"><span data-stu-id="4f2b9-311">The "scheduledTransferPeriod" for the aggregated values stored in the table</span></span>
* `P10DV2S`
* <span data-ttu-id="4f2b9-312">格式為 "YYYYMMDD" 的日期，每 10 天變更一次</span><span class="sxs-lookup"><span data-stu-id="4f2b9-312">A date, in the form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="4f2b9-313">例如 `WADMetricsPT1HP10DV2S20170410` 與 `WADMetricsPT1MP10DV2S20170609`。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="4f2b9-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="4f2b9-314">syslogEvents</span></span>

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

<span data-ttu-id="4f2b9-315">此選擇性區段會控制從 Syslog 收集記錄事件。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-315">This optional section controls the collection of log events from syslog.</span></span> <span data-ttu-id="4f2b9-316">如果省略該區段，則完全不會擷取 Syslog 事件。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-316">If the section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="4f2b9-317">syslogEventConfiguration 集合對每個感興趣的 Syslog 設備都會一個項目。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-317">The syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="4f2b9-318">如果特定設備的 minSeverity 為 "NONE"，或如果該設備完全未顯示在元素中，則不會從該設備中擷取事件。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in the element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="4f2b9-319">元素</span><span class="sxs-lookup"><span data-stu-id="4f2b9-319">Element</span></span> | <span data-ttu-id="4f2b9-320">值</span><span class="sxs-lookup"><span data-stu-id="4f2b9-320">Value</span></span>
------- | -----
<span data-ttu-id="4f2b9-321">sinks</span><span class="sxs-lookup"><span data-stu-id="4f2b9-321">sinks</span></span> | <span data-ttu-id="4f2b9-322">系統會將個別記錄事件發佈至的接收名稱清單，以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-322">A comma-separated list of names of sinks to which individual log events are published.</span></span> <span data-ttu-id="4f2b9-323">符合 syslogEventConfiguration 中限制的所有記錄事件會發佈至每個所列的接收。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-323">All log events matching the restrictions in syslogEventConfiguration are published to each listed sink.</span></span> <span data-ttu-id="4f2b9-324">範例："EHforsyslog"</span><span class="sxs-lookup"><span data-stu-id="4f2b9-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="4f2b9-325">facilityName</span><span class="sxs-lookup"><span data-stu-id="4f2b9-325">facilityName</span></span> | <span data-ttu-id="4f2b9-326">Syslog 設備名稱 (例如 "LOG\_USER" 或 "LOG\_LOCAL0")。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="4f2b9-327">請參閱 [Syslog 手冊頁](http://man7.org/linux/man-pages/man3/syslog.3.html)中的「設備」(英文) 一節，以取得完整清單。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-327">See the "facility" section of the [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for the full list.</span></span>
<span data-ttu-id="4f2b9-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="4f2b9-328">minSeverity</span></span> | <span data-ttu-id="4f2b9-329">Syslog 嚴重性層級 (例如 "LOG\_ERR" 或 "LOG\_INFO")。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="4f2b9-330">請參閱 [Syslog 手冊頁](http://man7.org/linux/man-pages/man3/syslog.3.html)中的「層級」(英文) 一節，以取得完整清單。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-330">See the "level" section of the [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for the full list.</span></span> <span data-ttu-id="4f2b9-331">擴充功能會擷取傳送到在指定層級或以上的設備。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-331">The extension captures events sent to the facility at or above the specified level.</span></span>

<span data-ttu-id="4f2b9-332">當您指定 `syslogEvents` 時，LAD 一律將資料寫入 Azure 儲存體中的資料表。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-332">When you specify `syslogEvents`, LAD always writes data to a table in Azure storage.</span></span> <span data-ttu-id="4f2b9-333">您可以將相同的資料寫入 JSON Blob 和/或事件中樞，但您無法禁止將資料儲存至資料表。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-333">You can have the same data written to JSON blobs and/or Event Hubs, but you cannot disable storing data to a table.</span></span> <span data-ttu-id="4f2b9-334">此資料表的分割行為如同所述的 `performanceCounters`。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-334">The partitioning behavior for this table is the same as described for `performanceCounters`.</span></span> <span data-ttu-id="4f2b9-335">資料表名稱是這些字串的串連：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-335">The table name is the concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="4f2b9-336">格式為 "YYYYMMDD" 的日期，每 10 天變更一次</span><span class="sxs-lookup"><span data-stu-id="4f2b9-336">A date, in the form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="4f2b9-337">例如 `LinuxSyslog20170410` 與 `LinuxSyslog20170609`。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="4f2b9-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="4f2b9-338">perfCfg</span></span>

<span data-ttu-id="4f2b9-339">此選擇性區段會控制任意 [OMI](https://github.com/Microsoft/omi) 查詢的執行。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

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

<span data-ttu-id="4f2b9-340">元素</span><span class="sxs-lookup"><span data-stu-id="4f2b9-340">Element</span></span> | <span data-ttu-id="4f2b9-341">值</span><span class="sxs-lookup"><span data-stu-id="4f2b9-341">Value</span></span>
------- | -----
<span data-ttu-id="4f2b9-342">namespace</span><span class="sxs-lookup"><span data-stu-id="4f2b9-342">namespace</span></span> | <span data-ttu-id="4f2b9-343">(選擇性) 應執行查詢的 OMI 命名空間。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-343">(optional) The OMI namespace within which the query should be executed.</span></span> <span data-ttu-id="4f2b9-344">如果未指定，則預設值為 "root/scx"，此值由[系統中心跨平台提供者](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation) (英文) 實作。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-344">If unspecified, the default value is "root/scx", implemented by the [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="4f2b9-345">query</span><span class="sxs-lookup"><span data-stu-id="4f2b9-345">query</span></span> | <span data-ttu-id="4f2b9-346">欲執行的 OMI 查詢。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-346">The OMI query to be executed.</span></span>
<span data-ttu-id="4f2b9-347">資料表</span><span class="sxs-lookup"><span data-stu-id="4f2b9-347">table</span></span> | <span data-ttu-id="4f2b9-348">(選擇性) 所指定儲存體帳戶中的 Azure 儲存體資料表 (請參閱[受保護的設定](#protected-settings))。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-348">(optional) The Azure storage table, in the designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="4f2b9-349">frequency</span><span class="sxs-lookup"><span data-stu-id="4f2b9-349">frequency</span></span> | <span data-ttu-id="4f2b9-350">(選擇性) 執行查詢之間的秒數。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-350">(optional) The number of seconds between execution of the query.</span></span> <span data-ttu-id="4f2b9-351">預設值為 300 秒 (5 分鐘)；最小值為 15 秒。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="4f2b9-352">sinks</span><span class="sxs-lookup"><span data-stu-id="4f2b9-352">sinks</span></span> | <span data-ttu-id="4f2b9-353">(選擇性) 原始樣本計量結果應發佈至的額外接收名稱，以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-353">(optional) A comma-separated list of names of additional sinks to which raw sample metric results should be published.</span></span> <span data-ttu-id="4f2b9-354">擴充功能或 Azure 計量不會計算這些原始樣本的彙總。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-354">No aggregation of these raw samples is computed by the extension or by Azure Metrics.</span></span>

<span data-ttu-id="4f2b9-355">必須指定 "table" 或 "sinks"，或兩者。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="4f2b9-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="4f2b9-356">fileLogs</span></span>

<span data-ttu-id="4f2b9-357">控制記錄檔的擷取。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-357">Controls the capture of log files.</span></span> <span data-ttu-id="4f2b9-358">LAD 會在新文字行寫入檔案時擷取這些文字行，並寫入資料表資料列和/或任何指定的接收 (JsonBlob 或 EventHub)。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-358">LAD captures new text lines as they are written to the file and writes them to table rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="4f2b9-359">元素</span><span class="sxs-lookup"><span data-stu-id="4f2b9-359">Element</span></span> | <span data-ttu-id="4f2b9-360">值</span><span class="sxs-lookup"><span data-stu-id="4f2b9-360">Value</span></span>
------- | -----
<span data-ttu-id="4f2b9-361">file</span><span class="sxs-lookup"><span data-stu-id="4f2b9-361">file</span></span> | <span data-ttu-id="4f2b9-362">欲監看與擷取的記錄檔完整路徑名稱。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-362">The full pathname of the log file to be watched and captured.</span></span> <span data-ttu-id="4f2b9-363">路徑名稱必須命名單一檔案，不能命名目錄或包含萬用字元。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-363">The pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="4f2b9-364">資料表</span><span class="sxs-lookup"><span data-stu-id="4f2b9-364">table</span></span> | <span data-ttu-id="4f2b9-365">(選擇性) 所指定儲存體帳戶中的 Azure 儲存體資料表 (如受保護組態中指定)，檔案「尾端」的新行會寫入至此資料表。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-365">(optional) The Azure storage table, in the designated storage account (as specified in the protected configuration), into which new lines from the "tail" of the file are written.</span></span>
<span data-ttu-id="4f2b9-366">sinks</span><span class="sxs-lookup"><span data-stu-id="4f2b9-366">sinks</span></span> | <span data-ttu-id="4f2b9-367">(選擇性) 將記錄行傳送至的額外接收名稱清單，以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-367">(optional) A comma-separated list of names of additional sinks to which log lines sent.</span></span>

<span data-ttu-id="4f2b9-368">必須指定 "table" 或 "sinks"，或兩者。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-the-builtin-provider"></a><span data-ttu-id="4f2b9-369">內建提供者支援的計量</span><span class="sxs-lookup"><span data-stu-id="4f2b9-369">Metrics supported by the builtin provider</span></span>

<span data-ttu-id="4f2b9-370">內建的計量提供者為一組廣泛使用者最感興趣的計量來源。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-370">The builtin metric provider is a source of metrics most interesting to a broad set of users.</span></span> <span data-ttu-id="4f2b9-371">這些計量分成五大類別：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="4f2b9-372">處理器</span><span class="sxs-lookup"><span data-stu-id="4f2b9-372">Processor</span></span>
* <span data-ttu-id="4f2b9-373">記憶體</span><span class="sxs-lookup"><span data-stu-id="4f2b9-373">Memory</span></span>
* <span data-ttu-id="4f2b9-374">網路</span><span class="sxs-lookup"><span data-stu-id="4f2b9-374">Network</span></span>
* <span data-ttu-id="4f2b9-375">檔案系統</span><span class="sxs-lookup"><span data-stu-id="4f2b9-375">Filesystem</span></span>
* <span data-ttu-id="4f2b9-376">磁碟</span><span class="sxs-lookup"><span data-stu-id="4f2b9-376">Disk</span></span>

### <a name="builtin-metrics-for-the-processor-class"></a><span data-ttu-id="4f2b9-377">處理器類別的內建計量</span><span class="sxs-lookup"><span data-stu-id="4f2b9-377">builtin metrics for the Processor class</span></span>

<span data-ttu-id="4f2b9-378">計量的處理器類別會提供 VM 中處理器使用量的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-378">The Processor class of metrics provides information about processor usage in the VM.</span></span> <span data-ttu-id="4f2b9-379">彙總百分比時，結果為所有 CPU 的平均。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-379">When aggregating percentages, the result is the average across all CPUs.</span></span> <span data-ttu-id="4f2b9-380">在一個雙核心 VM 中，如果某個核心 100% 忙碌，另一個則 100% 閒置，則回報的 PercentIdleTime 會是 50。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-380">In a two core VM, if one core was 100% busy and the other was 100% idle, the reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="4f2b9-381">如果每個核心在同一期間皆為 50% 忙碌，則回報的結果也會是 50。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-381">If each core was 50% busy for the same period, the reported result would also be 50.</span></span> <span data-ttu-id="4f2b9-382">在一個四核心 VM 中，如果某個核心 100% 忙碌，另外三個閒置，則回報的 PercentIdleTime 會是 75。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-382">In a four core VM, with one core 100% busy and the others idle, the reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="4f2b9-383">counter</span><span class="sxs-lookup"><span data-stu-id="4f2b9-383">counter</span></span> | <span data-ttu-id="4f2b9-384">意義</span><span class="sxs-lookup"><span data-stu-id="4f2b9-384">Meaning</span></span>
------- | -------
<span data-ttu-id="4f2b9-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="4f2b9-385">PercentIdleTime</span></span> | <span data-ttu-id="4f2b9-386">彙總時間範圍期間，處理器執行核心閒置迴圈的百分比</span><span class="sxs-lookup"><span data-stu-id="4f2b9-386">Percentage of time during the aggregation window that processors were executing the kernel idle loop</span></span>
<span data-ttu-id="4f2b9-387">PercentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="4f2b9-387">PercentProcessorTime</span></span> | <span data-ttu-id="4f2b9-388">執行非閒置執行緒的時間百分比</span><span class="sxs-lookup"><span data-stu-id="4f2b9-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="4f2b9-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="4f2b9-389">PercentIOWaitTime</span></span> | <span data-ttu-id="4f2b9-390">等待 IO 作業完成的時間百分比</span><span class="sxs-lookup"><span data-stu-id="4f2b9-390">Percentage of time waiting for IO operations to complete</span></span>
<span data-ttu-id="4f2b9-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="4f2b9-391">PercentInterruptTime</span></span> | <span data-ttu-id="4f2b9-392">執行硬體/軟體中斷與 DPC (延遲的程序呼叫) 的時間百分比</span><span class="sxs-lookup"><span data-stu-id="4f2b9-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="4f2b9-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="4f2b9-393">PercentUserTime</span></span> | <span data-ttu-id="4f2b9-394">在彙總時間範圍期間的非閒置時間中，對一般優先順序以上的使用者花費時間的百分比</span><span class="sxs-lookup"><span data-stu-id="4f2b9-394">Of non-idle time during the aggregation window, the percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="4f2b9-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="4f2b9-395">PercentNiceTime</span></span> | <span data-ttu-id="4f2b9-396">在非閒置時間中，對較低 (好) 的優先順序花費的時間百分比</span><span class="sxs-lookup"><span data-stu-id="4f2b9-396">Of non-idle time, the percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="4f2b9-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="4f2b9-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="4f2b9-398">在非閒置時間中，在具特殊權限 (核心) 模式中花費的百分比</span><span class="sxs-lookup"><span data-stu-id="4f2b9-398">Of non-idle time, the percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="4f2b9-399">前四個計數器的總和應為 100%。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-399">The first four counters should sum to 100%.</span></span> <span data-ttu-id="4f2b9-400">最後三個計數器的總和也是 100%，再細分 PercentProcessorTime、PercentIOWaitTime 與 PercentInterruptTime 的總和。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-400">The last three counters also sum to 100%; they subdivide the sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="4f2b9-401">若要取得彙總所有處理器而得的單一計量，請設定 `"condition": "IsAggregate=TRUE"`。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-401">To obtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="4f2b9-402">若要取得特定處理器的計量，例如四核心 VM 的第二個邏輯處理器，請設定 `"condition": "Name=\\"1\\""`。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-402">To obtain a metric for a specific processor, such as the second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="4f2b9-403">邏輯處理器數目在範圍 `[0..n-1]` 內。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-403">Logical processor numbers are in the range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-the-memory-class"></a><span data-ttu-id="4f2b9-404">記處理器類別的內建計量</span><span class="sxs-lookup"><span data-stu-id="4f2b9-404">builtin metrics for the Memory class</span></span>

<span data-ttu-id="4f2b9-405">計量的記憶體類別提供有關記憶體使用率、分頁及交換的資訊。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-405">The Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="4f2b9-406">counter</span><span class="sxs-lookup"><span data-stu-id="4f2b9-406">counter</span></span> | <span data-ttu-id="4f2b9-407">意義</span><span class="sxs-lookup"><span data-stu-id="4f2b9-407">Meaning</span></span>
------- | -------
<span data-ttu-id="4f2b9-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="4f2b9-408">AvailableMemory</span></span> | <span data-ttu-id="4f2b9-409">可用的實體記憶體 (MiB)</span><span class="sxs-lookup"><span data-stu-id="4f2b9-409">Available physical memory in MiB</span></span>
<span data-ttu-id="4f2b9-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="4f2b9-410">PercentAvailableMemory</span></span> | <span data-ttu-id="4f2b9-411">以總記憶體百分比表示的可用實體記憶體</span><span class="sxs-lookup"><span data-stu-id="4f2b9-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="4f2b9-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="4f2b9-412">UsedMemory</span></span> | <span data-ttu-id="4f2b9-413">使用中實體記憶體 (MiB)</span><span class="sxs-lookup"><span data-stu-id="4f2b9-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="4f2b9-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="4f2b9-414">PercentUsedMemory</span></span> | <span data-ttu-id="4f2b9-415">以總記憶體百分比表示的使用中實體記憶體</span><span class="sxs-lookup"><span data-stu-id="4f2b9-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="4f2b9-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="4f2b9-416">PagesPerSec</span></span> | <span data-ttu-id="4f2b9-417">總分頁數 (讀取/寫入)</span><span class="sxs-lookup"><span data-stu-id="4f2b9-417">Total paging (read/write)</span></span>
<span data-ttu-id="4f2b9-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="4f2b9-418">PagesReadPerSec</span></span> | <span data-ttu-id="4f2b9-419">從備份存放區讀取的分頁數 (分頁檔、程式檔、對應檔等)</span><span class="sxs-lookup"><span data-stu-id="4f2b9-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="4f2b9-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="4f2b9-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="4f2b9-421">寫入備份存放區的頁面 (分頁檔、對應檔等)</span><span class="sxs-lookup"><span data-stu-id="4f2b9-421">Pages written to backing store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="4f2b9-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="4f2b9-422">AvailableSwap</span></span> | <span data-ttu-id="4f2b9-423">未使用的交換空間 (MiB)</span><span class="sxs-lookup"><span data-stu-id="4f2b9-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="4f2b9-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="4f2b9-424">PercentAvailableSwap</span></span> | <span data-ttu-id="4f2b9-425">以總交換空間百分比表示的未使用交換空間</span><span class="sxs-lookup"><span data-stu-id="4f2b9-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="4f2b9-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="4f2b9-426">UsedSwap</span></span> | <span data-ttu-id="4f2b9-427">已使用交換空間 (MiB)</span><span class="sxs-lookup"><span data-stu-id="4f2b9-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="4f2b9-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="4f2b9-428">PercentUsedSwap</span></span> | <span data-ttu-id="4f2b9-429">以總交換空間表示的使用中交換空間</span><span class="sxs-lookup"><span data-stu-id="4f2b9-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="4f2b9-430">此計量類別只有單一執行個體。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="4f2b9-431">"condition" 屬性無有用的設定，應予以省略。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-431">The "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-the-network-class"></a><span data-ttu-id="4f2b9-432">網路類別的內建計量</span><span class="sxs-lookup"><span data-stu-id="4f2b9-432">builtin metrics for the Network class</span></span>

<span data-ttu-id="4f2b9-433">計量的網路類別提供自開機後，個別網路介面上網路活動的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-433">The Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="4f2b9-434">LAD 不會公開頻寬計量，該計量可從主機計量中取出。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="4f2b9-435">counter</span><span class="sxs-lookup"><span data-stu-id="4f2b9-435">counter</span></span> | <span data-ttu-id="4f2b9-436">意義</span><span class="sxs-lookup"><span data-stu-id="4f2b9-436">Meaning</span></span>
------- | -------
<span data-ttu-id="4f2b9-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="4f2b9-437">BytesTransmitted</span></span> | <span data-ttu-id="4f2b9-438">自開機後傳送的位元組總數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-438">Total bytes sent since boot</span></span>
<span data-ttu-id="4f2b9-439">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="4f2b9-439">BytesReceived</span></span> | <span data-ttu-id="4f2b9-440">自開機後收到的位元組總數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-440">Total bytes received since boot</span></span>
<span data-ttu-id="4f2b9-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="4f2b9-441">BytesTotal</span></span> | <span data-ttu-id="4f2b9-442">自開機後收傳送或收到的位元組總數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="4f2b9-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="4f2b9-443">PacketsTransmitted</span></span> | <span data-ttu-id="4f2b9-444">自開機後傳送的封包總數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-444">Total packets sent since boot</span></span>
<span data-ttu-id="4f2b9-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="4f2b9-445">PacketsReceived</span></span> | <span data-ttu-id="4f2b9-446">自開機後收到的封包總數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-446">Total packets received since boot</span></span>
<span data-ttu-id="4f2b9-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="4f2b9-447">TotalRxErrors</span></span> | <span data-ttu-id="4f2b9-448">自開機後接收的錯誤數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-448">Number of receive errors since boot</span></span>
<span data-ttu-id="4f2b9-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="4f2b9-449">TotalTxErrors</span></span> | <span data-ttu-id="4f2b9-450">自開機後傳輸的錯誤數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="4f2b9-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="4f2b9-451">TotalCollisions</span></span> | <span data-ttu-id="4f2b9-452">自開機後網路連接埠回報的衝突數目</span><span class="sxs-lookup"><span data-stu-id="4f2b9-452">Number of collisions reported by the network ports since boot</span></span>

 <span data-ttu-id="4f2b9-453">雖然此類別已執行個體化，但 LAD 不支援擷取從所有網路裝置彙總的網路計量。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="4f2b9-454">若要取得特定介面 (例如 eth0) 的計量，請設定 `"condition": "InstanceID=\\"eth0\\""`。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-454">To obtain the metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-the-filesystem-class"></a><span data-ttu-id="4f2b9-455">檔案系統類別的內建計量</span><span class="sxs-lookup"><span data-stu-id="4f2b9-455">builtin metrics for the Filesystem class</span></span>

<span data-ttu-id="4f2b9-456">計量的檔案系統類別提供檔案系統使用量的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-456">The Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="4f2b9-457">當對一般使用者 (非根使用者) 顯示這些資訊時，系統會回報絕對值與百分比值。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-457">Absolute and percentage values are reported as they'd be displayed to an ordinary user (not root).</span></span>

<span data-ttu-id="4f2b9-458">counter</span><span class="sxs-lookup"><span data-stu-id="4f2b9-458">counter</span></span> | <span data-ttu-id="4f2b9-459">意義</span><span class="sxs-lookup"><span data-stu-id="4f2b9-459">Meaning</span></span>
------- | -------
<span data-ttu-id="4f2b9-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="4f2b9-460">FreeSpace</span></span> | <span data-ttu-id="4f2b9-461">可用磁碟空間 (位元組)</span><span class="sxs-lookup"><span data-stu-id="4f2b9-461">Available disk space in bytes</span></span>
<span data-ttu-id="4f2b9-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="4f2b9-462">UsedSpace</span></span> | <span data-ttu-id="4f2b9-463">已使用的磁碟空間 (位元組)</span><span class="sxs-lookup"><span data-stu-id="4f2b9-463">Used disk space in bytes</span></span>
<span data-ttu-id="4f2b9-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="4f2b9-464">PercentFreeSpace</span></span> | <span data-ttu-id="4f2b9-465">可用空間百分比</span><span class="sxs-lookup"><span data-stu-id="4f2b9-465">Percentage free space</span></span>
<span data-ttu-id="4f2b9-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="4f2b9-466">PercentUsedSpace</span></span> | <span data-ttu-id="4f2b9-467">已使用的空間百分比</span><span class="sxs-lookup"><span data-stu-id="4f2b9-467">Percentage used space</span></span>
<span data-ttu-id="4f2b9-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="4f2b9-468">PercentFreeInodes</span></span> | <span data-ttu-id="4f2b9-469">未使用 inode 的百分比</span><span class="sxs-lookup"><span data-stu-id="4f2b9-469">Percentage of unused inodes</span></span>
<span data-ttu-id="4f2b9-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="4f2b9-470">PercentUsedInodes</span></span> | <span data-ttu-id="4f2b9-471">所有檔案系統中已配置 (使用中) inode 總和的百分比</span><span class="sxs-lookup"><span data-stu-id="4f2b9-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="4f2b9-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="4f2b9-472">BytesReadPerSecond</span></span> | <span data-ttu-id="4f2b9-473">每秒讀取的位元組數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-473">Bytes read per second</span></span>
<span data-ttu-id="4f2b9-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="4f2b9-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="4f2b9-475">每秒寫入的位元組數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-475">Bytes written per second</span></span>
<span data-ttu-id="4f2b9-476">每秒位元組</span><span class="sxs-lookup"><span data-stu-id="4f2b9-476">BytesPerSecond</span></span> | <span data-ttu-id="4f2b9-477">每秒讀取或寫入的位元組數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-477">Bytes read or written per second</span></span>
<span data-ttu-id="4f2b9-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="4f2b9-478">ReadsPerSecond</span></span> | <span data-ttu-id="4f2b9-479">每秒的讀取作業數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-479">Read operations per second</span></span>
<span data-ttu-id="4f2b9-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="4f2b9-480">WritesPerSecond</span></span> | <span data-ttu-id="4f2b9-481">每秒的寫入作業數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-481">Write operations per second</span></span>
<span data-ttu-id="4f2b9-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="4f2b9-482">TransfersPerSecond</span></span> | <span data-ttu-id="4f2b9-483">每秒的讀取或寫入作業數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-483">Read or write operations per second</span></span>

<span data-ttu-id="4f2b9-484">可透過設定 `"condition": "IsAggregate=True"` 取得的所有檔案系統彙總值。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="4f2b9-485">可透過設定 `"condition": 'Name="/mnt"'` 取得的特定已掛接檔案系統 (例如 "/mnt") 的值。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-the-disk-class"></a><span data-ttu-id="4f2b9-486">磁碟類別的內建計量</span><span class="sxs-lookup"><span data-stu-id="4f2b9-486">builtin metrics for the Disk class</span></span>

<span data-ttu-id="4f2b9-487">計量的磁碟類別提供磁碟裝置使用量的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-487">The Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="4f2b9-488">這些統計資料會套用到整個磁碟機。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-488">These statistics apply to the entire drive.</span></span> <span data-ttu-id="4f2b9-489">如果裝置上有多個檔案系統，該裝置的計數器實際上是所有檔案系統的彙總。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-489">If there are multiple file systems on a device, the counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="4f2b9-490">counter</span><span class="sxs-lookup"><span data-stu-id="4f2b9-490">counter</span></span> | <span data-ttu-id="4f2b9-491">意義</span><span class="sxs-lookup"><span data-stu-id="4f2b9-491">Meaning</span></span>
------- | -------
<span data-ttu-id="4f2b9-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="4f2b9-492">ReadsPerSecond</span></span> | <span data-ttu-id="4f2b9-493">每秒的讀取作業數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-493">Read operations per second</span></span>
<span data-ttu-id="4f2b9-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="4f2b9-494">WritesPerSecond</span></span> | <span data-ttu-id="4f2b9-495">每秒的寫入作業數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-495">Write operations per second</span></span>
<span data-ttu-id="4f2b9-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="4f2b9-496">TransfersPerSecond</span></span> | <span data-ttu-id="4f2b9-497">每秒的總作業數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-497">Total operations per second</span></span>
<span data-ttu-id="4f2b9-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="4f2b9-498">AverageReadTime</span></span> | <span data-ttu-id="4f2b9-499">每個讀取作業的平均秒數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-499">Average seconds per read operation</span></span>
<span data-ttu-id="4f2b9-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="4f2b9-500">AverageWriteTime</span></span> | <span data-ttu-id="4f2b9-501">每個寫入作業的平均秒數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-501">Average seconds per write operation</span></span>
<span data-ttu-id="4f2b9-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="4f2b9-502">AverageTransferTime</span></span> | <span data-ttu-id="4f2b9-503">每個作業的平均秒數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-503">Average seconds per operation</span></span>
<span data-ttu-id="4f2b9-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="4f2b9-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="4f2b9-505">已排入佇列的磁碟作業平均數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-505">Average number of queued disk operations</span></span>
<span data-ttu-id="4f2b9-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="4f2b9-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="4f2b9-507">每秒讀取的位元組數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-507">Number of bytes read per second</span></span>
<span data-ttu-id="4f2b9-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="4f2b9-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="4f2b9-509">每秒寫入的位元組數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-509">Number of bytes written per second</span></span>
<span data-ttu-id="4f2b9-510">每秒位元組</span><span class="sxs-lookup"><span data-stu-id="4f2b9-510">BytesPerSecond</span></span> | <span data-ttu-id="4f2b9-511">每秒讀取或寫入的位元組數</span><span class="sxs-lookup"><span data-stu-id="4f2b9-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="4f2b9-512">可透過設定 `"condition": "IsAggregate=True"` 取得的所有磁碟彙總值。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="4f2b9-513">若要取得特定裝置的資訊 (例如，/dev/sdf1) 請設定 `"condition": "Name=\\"/dev/sdf1\\""`。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-513">To get information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="4f2b9-514">透過 CLI 安裝與設定 LAD 3.0</span><span class="sxs-lookup"><span data-stu-id="4f2b9-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="4f2b9-515">假設您的受保護設定在 PrivateConfig.json 檔案中，您的公用組態資訊在 PublicConfig.json 中，請執行此命令：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-515">Assuming your protected settings are in the file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="4f2b9-516">此命令假設您使用 Azure CLI 的 Azure Resource Management 模組 (arm)。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-516">The command assumes you are using the Azure Resource Management mode (arm) of the Azure CLI.</span></span> <span data-ttu-id="4f2b9-517">若要為傳統部署模型 (ASM) VM 設定 LAD，請切換成 "asm" 模式 (`azure config mode asm`)，並省略命令中的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-517">To configure LAD for classic deployment model (ASM) VMs, switch to "asm" mode (`azure config mode asm`) and omit the resource group name in the command.</span></span> <span data-ttu-id="4f2b9-518">如需詳細資訊，請參閱[跨平台 CLI 文件](https://docs.microsoft.com/azure/xplat-cli-connect)。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-518">For more information, see the [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="4f2b9-519">範例 LAD 3.0 組態</span><span class="sxs-lookup"><span data-stu-id="4f2b9-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="4f2b9-520">根據前述的定義，以下為範例 LAD 3.0 擴充功能及一些說明。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-520">Based on the preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="4f2b9-521">若要將此範例套用到您的案例，您應使用自己的儲存體帳戶、帳戶 SAS 權杖，以及 EventHubs SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-521">To apply this sample to your case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="4f2b9-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="4f2b9-522">PrivateConfig.json</span></span>

<span data-ttu-id="4f2b9-523">這些私用設定會設定：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-523">These private settings configure:</span></span>

* <span data-ttu-id="4f2b9-524">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="4f2b9-524">a storage account</span></span>
* <span data-ttu-id="4f2b9-525">相符的帳戶 SAS 權杖</span><span class="sxs-lookup"><span data-stu-id="4f2b9-525">a matching account SAS token</span></span>
* <span data-ttu-id="4f2b9-526">數個接收 (含 SAS 權杖的 JsonBlob 或 EventHubs)</span><span class="sxs-lookup"><span data-stu-id="4f2b9-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

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

### <a name="publicconfigjson"></a><span data-ttu-id="4f2b9-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="4f2b9-527">PublicConfig.json</span></span>

<span data-ttu-id="4f2b9-528">這些公用設定會造成 LAD：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="4f2b9-529">將 percent-processor-time 與 used-disk-space 計量上傳至 `WADMetrics*` 資料表</span><span class="sxs-lookup"><span data-stu-id="4f2b9-529">Upload percent-processor-time and used-disk-space metrics to the `WADMetrics*` table</span></span>
* <span data-ttu-id="4f2b9-530">將 Syslog 設備 "user" 與嚴重性 "info" 上傳至 `LinuxSyslog*` 資料表</span><span class="sxs-lookup"><span data-stu-id="4f2b9-530">Upload messages from syslog facility "user" and severity "info" to the `LinuxSyslog*` table</span></span>
* <span data-ttu-id="4f2b9-531">將原始 OMI 查詢結果 (PercentProcessorTime 與 PercentIdleTime) 上傳至名為 `LinuxCPU` 的資料表</span><span class="sxs-lookup"><span data-stu-id="4f2b9-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) to the named `LinuxCPU` table</span></span>
* <span data-ttu-id="4f2b9-532">將檔案 `/var/log/myladtestlog` 中附加的行上傳至 `MyLadTestLog` 資料表</span><span class="sxs-lookup"><span data-stu-id="4f2b9-532">Upload appended lines in file `/var/log/myladtestlog` to the `MyLadTestLog` table</span></span>

<span data-ttu-id="4f2b9-533">在每個案例中，也會將資料上傳至：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="4f2b9-534">Azure Blob 儲存體 (容器名稱如同 JsonBlob 接收中定義的名稱)</span><span class="sxs-lookup"><span data-stu-id="4f2b9-534">Azure Blob storage (container name is as defined in the JsonBlob sink)</span></span>
* <span data-ttu-id="4f2b9-535">EventHubs 端點 (如同在 EventHubs 接收中指定)</span><span class="sxs-lookup"><span data-stu-id="4f2b9-535">EventHubs endpoint (as specified in the EventHubs sink)</span></span>

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

<span data-ttu-id="4f2b9-536">組態中的 `resourceId` 必須與 VM 或虛擬機器擴展集中的相符。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-536">The `resourceId` in the configuration must match that of the VM or the virtual machine scale set.</span></span>

* <span data-ttu-id="4f2b9-537">Azure 平台計量的圖表與警示功能知道您正在使用的 VM 其資源 ID。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-537">Azure platform metrics charting and alerting knows the resourceId of the VM you're working on.</span></span> <span data-ttu-id="4f2b9-538">該功能應使用查閱索引鍵的 resourceId 尋找您 VM 的資料。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-538">It expects to find the data for your VM using the resourceId the lookup key.</span></span>
* <span data-ttu-id="4f2b9-539">如果您使用 Azure 自動調整，則自動調整組態中的 resourceId 必須符合 LAD 使用的 resourceId。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-539">If you use Azure autoscale, the resourceId in the autoscale configuration must match the resourceId used by LAD.</span></span>
* <span data-ttu-id="4f2b9-540">resourceId 內建在 LAD 所寫入 JsonBlob 的名稱中。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-540">The resourceId is built into the names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="4f2b9-541">檢視資料</span><span class="sxs-lookup"><span data-stu-id="4f2b9-541">View your data</span></span>

<span data-ttu-id="4f2b9-542">使用 Azure 入口網站檢視效能資料或集合警示：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-542">Use the Azure portal to view performance data or set alerts:</span></span>

![image](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="4f2b9-544">`performanceCounters` 資料一律儲存在 Azure 儲存體資料表中。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-544">The `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="4f2b9-545">Azure 儲存體 API 適用於許多語言與平台。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="4f2b9-546">傳送到 JsonBlob 接收的資料會儲存在[受保護的設定](#protected-settings)中所指定儲存體帳戶的 Blob 中。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-546">Data sent to JsonBlob sinks is stored in blobs in the storage account named in the [Protected settings](#protected-settings).</span></span> <span data-ttu-id="4f2b9-547">您可以使用任何 Azure Blob 儲存體 API 取用 Blob 資料。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-547">You can consume the blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="4f2b9-548">此外，您可以使用這些 UI 工具存取 Azure 儲存體中的資料：</span><span class="sxs-lookup"><span data-stu-id="4f2b9-548">In addition, you can use these UI tools to access the data in Azure Storage:</span></span>

* <span data-ttu-id="4f2b9-549">Visual Studio 伺服器總管。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="4f2b9-550">[Microsoft Azure 儲存體總管](https://azurestorageexplorer.codeplex.com/ "Azure 儲存體總管")。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="4f2b9-551">Microsoft Azure 儲存體總管工作階段的這個快照顯示從測試 VM 上正確設定的 LAD 3.0 擴充功能產生的 Azure 儲存體資料表及容器。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-551">This snapshot of a Microsoft Azure Storage Explorer session shows the generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="4f2b9-552">影像不完全符合[範例 LAD 3.0 組態](#an-example-lad-30-configuration)。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-552">The image doesn't match exactly with the [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![image](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="4f2b9-554">請參閱相關的 [EventHubs 資訊](../../event-hubs/event-hubs-what-is-event-hubs.md)，以了解如何取用發佈至 EventHubs 端點的訊息。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-554">See the relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) to learn how to consume messages published to an EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f2b9-555">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4f2b9-555">Next steps</span></span>

* <span data-ttu-id="4f2b9-556">在 [Azure 監視器](../../monitoring-and-diagnostics/insights-alerts-portal.md)中為您收集的計量建立計量警示。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for the metrics you collect.</span></span>
* <span data-ttu-id="4f2b9-557">為您的計量建立[監視圖表](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="4f2b9-558">了解如何使用計量[建立虛擬機器擴展集](/azure/virtual-machines/linux/tutorial-create-vmss)以控制自動調整。</span><span class="sxs-lookup"><span data-stu-id="4f2b9-558">Learn how to [create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics to control autoscaling.</span></span>
