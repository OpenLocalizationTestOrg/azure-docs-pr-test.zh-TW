---
title: "aaaOMS 適用於 Linux 的 Azure 虛擬機器擴充功能 |Microsoft 文件"
description: "部署 hello 使用虛擬機器擴充功能的 Linux 虛擬機器上的 OMS 代理程式。"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a><span data-ttu-id="43946-103">適用於 Linux 的 OMS 虛擬機器擴充功能</span><span class="sxs-lookup"><span data-stu-id="43946-103">OMS virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="43946-104">概觀</span><span class="sxs-lookup"><span data-stu-id="43946-104">Overview</span></span>

<span data-ttu-id="43946-105">Operations Management Suite (OMS) 可提供雲端和內部部署資產的監視、警示和警示補救功能。</span><span class="sxs-lookup"><span data-stu-id="43946-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="43946-106">發行 hello OMS Agent for Linux 的虛擬機器擴充功能和 Microsoft 支援。</span><span class="sxs-lookup"><span data-stu-id="43946-106">hello OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span></span> <span data-ttu-id="43946-107">hello 延伸模組會安裝 Azure 的虛擬機器上的 hello OMS 代理程式，並註冊到現有的 OMS 工作區的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="43946-107">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="43946-108">此文件詳細資料 hello 支援平台、 組態和部署選項 hello OMS 虛擬機器擴充功能適用於 Linux。</span><span class="sxs-lookup"><span data-stu-id="43946-108">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43946-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="43946-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="43946-110">作業系統</span><span class="sxs-lookup"><span data-stu-id="43946-110">Operating system</span></span>

<span data-ttu-id="43946-111">hello OMS 代理程式延伸模組可以執行這些 Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="43946-111">hello OMS Agent extension can be run against these Linux distributions.</span></span>

| <span data-ttu-id="43946-112">配送映像</span><span class="sxs-lookup"><span data-stu-id="43946-112">Distribution</span></span> | <span data-ttu-id="43946-113">版本</span><span class="sxs-lookup"><span data-stu-id="43946-113">Version</span></span> |
|---|---|
| <span data-ttu-id="43946-114">CentOS Linux</span><span class="sxs-lookup"><span data-stu-id="43946-114">CentOS Linux</span></span> | <span data-ttu-id="43946-115">5、6 和 7</span><span class="sxs-lookup"><span data-stu-id="43946-115">5, 6, and 7</span></span> |
| <span data-ttu-id="43946-116">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="43946-116">Oracle Linux</span></span> | <span data-ttu-id="43946-117">5、6 和 7</span><span class="sxs-lookup"><span data-stu-id="43946-117">5, 6, and 7</span></span> |
| <span data-ttu-id="43946-118">Red Hat Enterprise Linux Server</span><span class="sxs-lookup"><span data-stu-id="43946-118">Red Hat Enterprise Linux Server</span></span> | <span data-ttu-id="43946-119">5、6 和 7</span><span class="sxs-lookup"><span data-stu-id="43946-119">5, 6 and 7</span></span> |
| <span data-ttu-id="43946-120">Debian GNU/Linux</span><span class="sxs-lookup"><span data-stu-id="43946-120">Debian GNU/Linux</span></span> | <span data-ttu-id="43946-121">6、7 和 8</span><span class="sxs-lookup"><span data-stu-id="43946-121">6, 7, and 8</span></span> |
| <span data-ttu-id="43946-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="43946-122">Ubuntu</span></span> | <span data-ttu-id="43946-123">12.04 LTS、14.04 LTS、15.04、15.10、16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="43946-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span></span> |
| <span data-ttu-id="43946-124">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="43946-124">SUSE Linux Enterprise Server</span></span> | <span data-ttu-id="43946-125">11 和 12</span><span class="sxs-lookup"><span data-stu-id="43946-125">11 and 12</span></span> |

### <a name="internet-connectivity"></a><span data-ttu-id="43946-126">網際網路連線</span><span class="sxs-lookup"><span data-stu-id="43946-126">Internet connectivity</span></span>

<span data-ttu-id="43946-127">hello 適用於 Linux 的 OMS 代理程式延伸模組需要該 hello 目標虛擬機器已連接的 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="43946-127">hello OMS Agent extension for Linux requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="43946-128">擴充功能結構描述</span><span class="sxs-lookup"><span data-stu-id="43946-128">Extension schema</span></span>

<span data-ttu-id="43946-129">hello 下列 JSON 顯示 hello hello OMS 代理程式延伸結構描述。</span><span class="sxs-lookup"><span data-stu-id="43946-129">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="43946-130">hello 延伸模組需要 hello 工作區識別碼和工作區金鑰從 hello 目標 OMS 工作區。hello OMS 入口網站中可以找到這些值。</span><span class="sxs-lookup"><span data-stu-id="43946-130">hello extension requires hello workspace ID and workspace key from hello target OMS workspace; these values can be found in hello OMS portal.</span></span> <span data-ttu-id="43946-131">Hello 工作區金鑰應該視為機密資料，因為它應該儲存在受保護的設定。</span><span class="sxs-lookup"><span data-stu-id="43946-131">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="43946-132">Azure VM 延伸模組保護的設定資料加密，且只能解密 hello 目標虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="43946-132">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="43946-133">請注意，**workspaceId** 和 **workspaceKey** 區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="43946-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a><span data-ttu-id="43946-134">屬性值</span><span class="sxs-lookup"><span data-stu-id="43946-134">Property values</span></span>

| <span data-ttu-id="43946-135">名稱</span><span class="sxs-lookup"><span data-stu-id="43946-135">Name</span></span> | <span data-ttu-id="43946-136">值 / 範例</span><span class="sxs-lookup"><span data-stu-id="43946-136">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="43946-137">apiVersion</span><span class="sxs-lookup"><span data-stu-id="43946-137">apiVersion</span></span> | <span data-ttu-id="43946-138">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="43946-138">2015-06-15</span></span> |
| <span data-ttu-id="43946-139">publisher</span><span class="sxs-lookup"><span data-stu-id="43946-139">publisher</span></span> | <span data-ttu-id="43946-140">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="43946-140">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="43946-141">類型</span><span class="sxs-lookup"><span data-stu-id="43946-141">type</span></span> | <span data-ttu-id="43946-142">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="43946-142">OmsAgentForLinux</span></span> |
| <span data-ttu-id="43946-143">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="43946-143">typeHandlerVersion</span></span> | <span data-ttu-id="43946-144">1.4</span><span class="sxs-lookup"><span data-stu-id="43946-144">1.4</span></span> |
| <span data-ttu-id="43946-145">workspaceId (例如)</span><span class="sxs-lookup"><span data-stu-id="43946-145">workspaceId (e.g)</span></span> | <span data-ttu-id="43946-146">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="43946-146">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="43946-147">workspaceKey (例如)</span><span class="sxs-lookup"><span data-stu-id="43946-147">workspaceKey (e.g)</span></span> | <span data-ttu-id="43946-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="43946-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="43946-149">範本部署</span><span class="sxs-lookup"><span data-stu-id="43946-149">Template deployment</span></span>

<span data-ttu-id="43946-150">也可以使用 Azure Resource Manager 範本部署 Azure VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="43946-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="43946-151">部署一或多個虛擬機器需要 post 部署設定，例如登入 tooOMS 時，範本很理想。</span><span class="sxs-lookup"><span data-stu-id="43946-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding tooOMS.</span></span> <span data-ttu-id="43946-152">包含 hello OMS 代理程式 VM 擴充功能的範例資源管理員範本可找到 hello [Azure 快速入門圖庫](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm)。</span><span class="sxs-lookup"><span data-stu-id="43946-152">A sample Resource Manager template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span></span> 

<span data-ttu-id="43946-153">可以巢狀方式置於 hello 虛擬機器的資源，或放在 hello 根或資源管理員 JSON 範本的最上層 hello JSON 設定虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="43946-153">hello JSON configuration for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="43946-154">hello 放置 hello JSON 組態會影響 hello hello 資源名稱和類型的值。</span><span class="sxs-lookup"><span data-stu-id="43946-154">hello placement of hello JSON configuration affects hello value of hello resource name and type.</span></span> <span data-ttu-id="43946-155">如需詳細資訊，請參閱[設定子資源的名稱和類型](../../azure-resource-manager/resource-manager-template-child-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="43946-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="43946-156">hello 下列範例假設 hello OMS 擴充功能位於 hello 虛擬機器資源。</span><span class="sxs-lookup"><span data-stu-id="43946-156">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="43946-157">巢狀 hello 延伸模組資源、 hello JSON 會放置於 hello `"resources": []` hello 虛擬機器的物件。</span><span class="sxs-lookup"><span data-stu-id="43946-157">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

<span data-ttu-id="43946-158">根目錄 hello hello 範本 hello 擴充 JSON 時，hello 資源名稱包含參考 toohello 父虛擬機器，並 hello 類型會反映 hello 巢狀的組態。</span><span class="sxs-lookup"><span data-stu-id="43946-158">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span>  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a><span data-ttu-id="43946-159">Azure CLI 部署</span><span class="sxs-lookup"><span data-stu-id="43946-159">Azure CLI deployment</span></span>

<span data-ttu-id="43946-160">hello Azure CLI 可以是使用的 toodeploy hello OMS 代理程式 VM 延伸模組 tooan 現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="43946-160">hello Azure CLI can be used toodeploy hello OMS Agent VM extension tooan existing virtual machine.</span></span> <span data-ttu-id="43946-161">取代為 hello OMS 金鑰和 OMS 識別碼從 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="43946-161">Replace hello OMS key and OMS ID with those from your OMS workspace.</span></span> 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="43946-162">疑難排解與支援</span><span class="sxs-lookup"><span data-stu-id="43946-162">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="43946-163">疑難排解</span><span class="sxs-lookup"><span data-stu-id="43946-163">Troubleshoot</span></span>

<span data-ttu-id="43946-164">從 hello Azure 入口網站，也可以使用 Azure CLI hello，可以擷取有關 hello 部署狀態的延伸模組的資料。</span><span class="sxs-lookup"><span data-stu-id="43946-164">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="43946-165">toosee hello 部署狀態的延伸模組指定的 vm，執行下列命令使用 hello hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="43946-165">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="43946-166">延伸模組執行輸出記錄的 toohello 之後，檔案：</span><span class="sxs-lookup"><span data-stu-id="43946-166">Extension execution output is logged toohello following file:</span></span>

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a><span data-ttu-id="43946-167">錯誤碼及其意義</span><span class="sxs-lookup"><span data-stu-id="43946-167">Error codes and their meanings</span></span>

| <span data-ttu-id="43946-168">錯誤碼</span><span class="sxs-lookup"><span data-stu-id="43946-168">Error Code</span></span> | <span data-ttu-id="43946-169">意義</span><span class="sxs-lookup"><span data-stu-id="43946-169">Meaning</span></span> | <span data-ttu-id="43946-170">可能的動作</span><span class="sxs-lookup"><span data-stu-id="43946-170">Possible Action</span></span> |
| :---: | --- | --- |
| <span data-ttu-id="43946-171">10</span><span class="sxs-lookup"><span data-stu-id="43946-171">10</span></span> | <span data-ttu-id="43946-172">VM 已連接的 tooan OMS 工作區</span><span class="sxs-lookup"><span data-stu-id="43946-172">VM is already connected tooan OMS workspace</span></span> | <span data-ttu-id="43946-173">tooconnect hello VM toohello 工作區中 hello 延伸結構描述，指定在公用的設定中設定 stopOnMultipleConnections toofalse 或移除這個屬性。</span><span class="sxs-lookup"><span data-stu-id="43946-173">tooconnect hello VM toohello workspace specified in hello extension schema, set stopOnMultipleConnections toofalse in public settings or remove this property.</span></span> <span data-ttu-id="43946-174">針對此 VM 所連線的每個工作區都會向此 VM 計費一次。</span><span class="sxs-lookup"><span data-stu-id="43946-174">This VM gets billed once for each workspace it is connected to.</span></span> |
| <span data-ttu-id="43946-175">11</span><span class="sxs-lookup"><span data-stu-id="43946-175">11</span></span> | <span data-ttu-id="43946-176">無效的設定提供 toohello 延伸模組</span><span class="sxs-lookup"><span data-stu-id="43946-176">Invalid config provided toohello extension</span></span> | <span data-ttu-id="43946-177">請遵循 hello 前面範例 tooset 部署所需的所有屬性值。</span><span class="sxs-lookup"><span data-stu-id="43946-177">Follow hello preceding examples tooset all property values necessary for deployment.</span></span> |
| <span data-ttu-id="43946-178">12</span><span class="sxs-lookup"><span data-stu-id="43946-178">12</span></span> | <span data-ttu-id="43946-179">已鎖定 hello 以 dpkg 封裝管理員</span><span class="sxs-lookup"><span data-stu-id="43946-179">hello dpkg package manager is locked</span></span> | <span data-ttu-id="43946-180">請確定所有以 dpkg 更新作業 hello 電腦上的完成，然後重試。</span><span class="sxs-lookup"><span data-stu-id="43946-180">Make sure all dpkg update operations on hello machine have finished and retry.</span></span> |
| <span data-ttu-id="43946-181">20</span><span class="sxs-lookup"><span data-stu-id="43946-181">20</span></span> | <span data-ttu-id="43946-182">啟用提前呼叫</span><span class="sxs-lookup"><span data-stu-id="43946-182">Enable called prematurely</span></span> | <span data-ttu-id="43946-183">[更新 hello Azure Linux 代理程式](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent)toohello 最新可用版本。</span><span class="sxs-lookup"><span data-stu-id="43946-183">[Update hello Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello latest available version.</span></span> |
| <span data-ttu-id="43946-184">51</span><span class="sxs-lookup"><span data-stu-id="43946-184">51</span></span> | <span data-ttu-id="43946-185">Hello VM 的作業系統不支援這項擴充功能</span><span class="sxs-lookup"><span data-stu-id="43946-185">This extension is not supported on hello VM's operation system</span></span> | |
| <span data-ttu-id="43946-186">55</span><span class="sxs-lookup"><span data-stu-id="43946-186">55</span></span> | <span data-ttu-id="43946-187">無法連接 toohello Microsoft Operations Management Suite 服務</span><span class="sxs-lookup"><span data-stu-id="43946-187">Cannot connect toohello Microsoft Operations Management Suite service</span></span> | <span data-ttu-id="43946-188">核取 hello 系統有網際網路存取權，或已提供有效的 HTTP proxy。</span><span class="sxs-lookup"><span data-stu-id="43946-188">Check that hello system either has Internet access, or that a valid HTTP proxy has been provided.</span></span> <span data-ttu-id="43946-189">此外，請檢查 hello 正確性的 hello 工作區識別碼。</span><span class="sxs-lookup"><span data-stu-id="43946-189">Additionally, check hello correctness of hello workspace ID.</span></span> |

<span data-ttu-id="43946-190">其他疑難排解資訊位於 hello [OMS 的代理程式-為-Linux 疑難排解指南](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#)。</span><span class="sxs-lookup"><span data-stu-id="43946-190">Additional troubleshooting information can be found on hello [OMS-Agent-for-Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span></span>

### <a name="support"></a><span data-ttu-id="43946-191">支援</span><span class="sxs-lookup"><span data-stu-id="43946-191">Support</span></span>

<span data-ttu-id="43946-192">如果您需要更多說明，在本文中的任何時間點，您可以連絡 hello 上 hello Azure 專家[MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/en-us/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="43946-192">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="43946-193">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="43946-193">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="43946-194">移 toohello [Azure 支援服務網站](https://azure.microsoft.com/en-us/support/options/)並選取 取得支援。</span><span class="sxs-lookup"><span data-stu-id="43946-194">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="43946-195">使用 Azure 所支援的相關資訊，請參閱 hello [Microsoft Azure 支援常見問題集](https://azure.microsoft.com/en-us/support/faq/)。</span><span class="sxs-lookup"><span data-stu-id="43946-195">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
