---
title: "Azure 診斷擴充功能的組態結構描述版本和歷程記錄 | Microsoft Docs"
description: "與收集 Azure 虛擬機器、VM 擴展集、Service Fabric 和雲端服務中的效能計數器有關。"
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/16/2017
ms.author: robb
ms.openlocfilehash: 119e8a237f24cdc80a1ab8e376f2b308c9eada05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-extention-configuration-schema-versions-and-history"></a><span data-ttu-id="6d36d-103">Azure 診斷延伸模組的設定結構描述版本和歷程記錄</span><span class="sxs-lookup"><span data-stu-id="6d36d-103">Azure Diagnostics extention configuration schema versions and history</span></span>
<span data-ttu-id="6d36d-104">針對隨附於 Microsoft Azure SDK 的 Azure 診斷擴充功能組態結構描述版本，此頁面會建立其索引。</span><span class="sxs-lookup"><span data-stu-id="6d36d-104">This page indexes Azure Diagnostics extension schema versions shipped as part of the Microsoft Azure SDK.</span></span>  

> [!NOTE]
> <span data-ttu-id="6d36d-105">Azure 診斷擴充功能這個元件可用來收集下列項目的效能計數器和其他統計資料︰</span><span class="sxs-lookup"><span data-stu-id="6d36d-105">The Azure Diagnostics extension is the component used to collect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="6d36d-106">Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="6d36d-106">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="6d36d-107">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="6d36d-107">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="6d36d-108">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6d36d-108">Service Fabric</span></span> 
> - <span data-ttu-id="6d36d-109">雲端服務</span><span class="sxs-lookup"><span data-stu-id="6d36d-109">Cloud Services</span></span> 
> - <span data-ttu-id="6d36d-110">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="6d36d-110">Network Security Groups</span></span>
> 
> <span data-ttu-id="6d36d-111">此頁面只在您使用其中一個服務時才相關。</span><span class="sxs-lookup"><span data-stu-id="6d36d-111">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="6d36d-112">Azure 診斷擴充功能要與 Azure 監視器、Application Insights 和 Log Analytics 等其他 Microsoft 診斷產品搭配使用。</span><span class="sxs-lookup"><span data-stu-id="6d36d-112">The Azure Diagnostics extension is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span> <span data-ttu-id="6d36d-113">如需詳細資訊，請參閱 [Microsoft 監視工具概觀](monitoring-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6d36d-113">For more information see [Microsoft Monitoring Tools Overview](monitoring-overview.md).</span></span>

## <a name="azure-sdk-and-diagnostics-versions-shipping-chart"></a><span data-ttu-id="6d36d-114">Azure SDK 和診斷版本推出方式圖表</span><span class="sxs-lookup"><span data-stu-id="6d36d-114">Azure SDK and diagnostics versions shipping chart</span></span>  

|<span data-ttu-id="6d36d-115">Azure SDK 版本</span><span class="sxs-lookup"><span data-stu-id="6d36d-115">Azure SDK version</span></span> | <span data-ttu-id="6d36d-116">診斷擴充功能版本</span><span class="sxs-lookup"><span data-stu-id="6d36d-116">Diagnostics extension version</span></span> | <span data-ttu-id="6d36d-117">模型</span><span class="sxs-lookup"><span data-stu-id="6d36d-117">Model</span></span>|  
|------------------|-------------------------------|------|  
|<span data-ttu-id="6d36d-118">1.x</span><span class="sxs-lookup"><span data-stu-id="6d36d-118">1.x</span></span>               |<span data-ttu-id="6d36d-119">1.0</span><span class="sxs-lookup"><span data-stu-id="6d36d-119">1.0</span></span>                            |<span data-ttu-id="6d36d-120">外掛程式</span><span class="sxs-lookup"><span data-stu-id="6d36d-120">plug-in</span></span>|  
|<span data-ttu-id="6d36d-121">2.0 - 2.4</span><span class="sxs-lookup"><span data-stu-id="6d36d-121">2.0 - 2.4</span></span>         |<span data-ttu-id="6d36d-122">1.0</span><span class="sxs-lookup"><span data-stu-id="6d36d-122">1.0</span></span>                            |<span data-ttu-id="6d36d-123">外掛程式</span><span class="sxs-lookup"><span data-stu-id="6d36d-123">plug-in</span></span>|  
|<span data-ttu-id="6d36d-124">2.5</span><span class="sxs-lookup"><span data-stu-id="6d36d-124">2.5</span></span>               |<span data-ttu-id="6d36d-125">1.2</span><span class="sxs-lookup"><span data-stu-id="6d36d-125">1.2</span></span>                            |<span data-ttu-id="6d36d-126">擴充功能</span><span class="sxs-lookup"><span data-stu-id="6d36d-126">extension</span></span>|  
|<span data-ttu-id="6d36d-127">2.6</span><span class="sxs-lookup"><span data-stu-id="6d36d-127">2.6</span></span>               |<span data-ttu-id="6d36d-128">1.3</span><span class="sxs-lookup"><span data-stu-id="6d36d-128">1.3</span></span>                            |<span data-ttu-id="6d36d-129">"</span><span class="sxs-lookup"><span data-stu-id="6d36d-129">"</span></span>|  
|<span data-ttu-id="6d36d-130">2.7</span><span class="sxs-lookup"><span data-stu-id="6d36d-130">2.7</span></span>               |<span data-ttu-id="6d36d-131">1.4</span><span class="sxs-lookup"><span data-stu-id="6d36d-131">1.4</span></span>                            |<span data-ttu-id="6d36d-132">"</span><span class="sxs-lookup"><span data-stu-id="6d36d-132">"</span></span>|  
|<span data-ttu-id="6d36d-133">2.8</span><span class="sxs-lookup"><span data-stu-id="6d36d-133">2.8</span></span>               |<span data-ttu-id="6d36d-134">1.5</span><span class="sxs-lookup"><span data-stu-id="6d36d-134">1.5</span></span>                            |<span data-ttu-id="6d36d-135">"</span><span class="sxs-lookup"><span data-stu-id="6d36d-135">"</span></span>|  
|<span data-ttu-id="6d36d-136">2.9</span><span class="sxs-lookup"><span data-stu-id="6d36d-136">2.9</span></span>               |<span data-ttu-id="6d36d-137">1.6</span><span class="sxs-lookup"><span data-stu-id="6d36d-137">1.6</span></span>                            |<span data-ttu-id="6d36d-138">"</span><span class="sxs-lookup"><span data-stu-id="6d36d-138">"</span></span>|
|<span data-ttu-id="6d36d-139">2.96</span><span class="sxs-lookup"><span data-stu-id="6d36d-139">2.96</span></span>              |<span data-ttu-id="6d36d-140">1.7</span><span class="sxs-lookup"><span data-stu-id="6d36d-140">1.7</span></span>                            |<span data-ttu-id="6d36d-141">"</span><span class="sxs-lookup"><span data-stu-id="6d36d-141">"</span></span>|
|<span data-ttu-id="6d36d-142">2.96</span><span class="sxs-lookup"><span data-stu-id="6d36d-142">2.96</span></span>              |<span data-ttu-id="6d36d-143">1.8</span><span class="sxs-lookup"><span data-stu-id="6d36d-143">1.8</span></span>                            |<span data-ttu-id="6d36d-144">"</span><span class="sxs-lookup"><span data-stu-id="6d36d-144">"</span></span>|
|<span data-ttu-id="6d36d-145">2.96</span><span class="sxs-lookup"><span data-stu-id="6d36d-145">2.96</span></span>              |<span data-ttu-id="6d36d-146">1.8.1</span><span class="sxs-lookup"><span data-stu-id="6d36d-146">1.8.1</span></span>                          |<span data-ttu-id="6d36d-147">"</span><span class="sxs-lookup"><span data-stu-id="6d36d-147">"</span></span>|
|<span data-ttu-id="6d36d-148">2.96</span><span class="sxs-lookup"><span data-stu-id="6d36d-148">2.96</span></span>              |<span data-ttu-id="6d36d-149">1.9</span><span class="sxs-lookup"><span data-stu-id="6d36d-149">1.9</span></span>                            |<span data-ttu-id="6d36d-150">"</span><span class="sxs-lookup"><span data-stu-id="6d36d-150">"</span></span>|



 <span data-ttu-id="6d36d-151">Azure 診斷 1.0 版最早是隨附於外掛程式模型中，這表示當您安裝 Azure SDK 時，即會取得隨附於其中的 Azure 診斷版本。</span><span class="sxs-lookup"><span data-stu-id="6d36d-151">Azure Diagnostics version 1.0 first shipped in a plug-in model -- meaning that when you installed the Azure SDK, you got the version of Azure diagnostics shipped with it.</span></span>  

 <span data-ttu-id="6d36d-152">從 SDK 2.5 (診斷版本 1.2) 開始，Azure 診斷變成延伸模型。</span><span class="sxs-lookup"><span data-stu-id="6d36d-152">Starting with SDK 2.5 (diagnostics version 1.2), Azure diagnostics went to an extension model.</span></span> <span data-ttu-id="6d36d-153">運用新功能的工具只能在較新的 Azure SDK 中取得，但是，任何使用 Azure 診斷的服務都能直接從 Azure 挑選最新的上市版本。</span><span class="sxs-lookup"><span data-stu-id="6d36d-153">The tools to utilize new features were only available in newer Azure SDKs, but any service using Azure diagnostics would pick up the latest shipping version directly from Azure.</span></span> <span data-ttu-id="6d36d-154">例如，仍在使用 SDK 2.5 的任何使用者都可以載入上表所示的最新版本，而不論使用者是否正在使用較新的功能。</span><span class="sxs-lookup"><span data-stu-id="6d36d-154">For example, anyone still using SDK 2.5 would be loading the latest version shown in the previous table, regardless if they are using the newer features.</span></span>  

## <a name="schemas-index"></a><span data-ttu-id="6d36d-155">結構描述索引</span><span class="sxs-lookup"><span data-stu-id="6d36d-155">Schemas index</span></span>  
<span data-ttu-id="6d36d-156">不同版本的 Azure 診斷會使用不同的組態結構描述。</span><span class="sxs-lookup"><span data-stu-id="6d36d-156">Different versions of Azure diagnostics use different configuration schemas.</span></span> 

[<span data-ttu-id="6d36d-157">Azure 診斷 1.0 組態結構描述</span><span class="sxs-lookup"><span data-stu-id="6d36d-157">Diagnostics 1.0 Configuration Schema</span></span>](azure-diagnostics-schema-1dot0.md)  

[<span data-ttu-id="6d36d-158">Azure 診斷 1.2 組態結構描述</span><span class="sxs-lookup"><span data-stu-id="6d36d-158">Diagnostics 1.2 Configuration Schema</span></span>](azure-diagnostics-schema-1dot2.md)  

[<span data-ttu-id="6d36d-159">診斷 1.3 和更新版本的組態結構描述</span><span class="sxs-lookup"><span data-stu-id="6d36d-159">Diagnostics 1.3 and later Configuration Schema</span></span>](azure-diagnostics-schema-1dot3-and-later.md)  

## <a name="version-history"></a><span data-ttu-id="6d36d-160">版本歷程記錄</span><span class="sxs-lookup"><span data-stu-id="6d36d-160">Version history</span></span>


### <a name="diagnostics-extension-19"></a><span data-ttu-id="6d36d-161">診斷擴充功能 1.9 版</span><span class="sxs-lookup"><span data-stu-id="6d36d-161">Diagnostics extension 1.9</span></span> 
<span data-ttu-id="6d36d-162">已新增 Docker 支援。</span><span class="sxs-lookup"><span data-stu-id="6d36d-162">Added Docker support.</span></span>


### <a name="diagnostics-extension-181"></a><span data-ttu-id="6d36d-163">診斷擴充功能 1.8.1 版</span><span class="sxs-lookup"><span data-stu-id="6d36d-163">Diagnostics extension 1.8.1</span></span> 
<span data-ttu-id="6d36d-164">可以在私用組態中指定 SAS 權杖 (而不是儲存體帳戶金鑰)。</span><span class="sxs-lookup"><span data-stu-id="6d36d-164">Can specify a SAS token instead of a storage account key in the private config.</span></span> <span data-ttu-id="6d36d-165">如果提供 SAS 權杖，系統會忽略儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="6d36d-165">If a SAS token is provided, the storage account key is ignored.</span></span>


```json
{
    "storageAccountName": "diagstorageaccount",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    }
}
```

```xml
<PrivateConfig>
    <StorageAccount name="diagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    <SecondaryStorageAccounts>
        <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
</PrivateConfig>
```


### <a name="diagnostics-extension-18"></a><span data-ttu-id="6d36d-166">診斷擴充功能 1.8 版</span><span class="sxs-lookup"><span data-stu-id="6d36d-166">Diagnostics extension 1.8</span></span> 
<span data-ttu-id="6d36d-167">已在 PublicConfig 中新增儲存體類型。</span><span class="sxs-lookup"><span data-stu-id="6d36d-167">Added Storage Type to PublicConfig.</span></span> <span data-ttu-id="6d36d-168">StorageType 可以是 Table、Blob、TableAndBlob。</span><span class="sxs-lookup"><span data-stu-id="6d36d-168">StorageType can be *Table*, *Blob*, *TableAndBlob*.</span></span> <span data-ttu-id="6d36d-169">Table 是預設值。</span><span class="sxs-lookup"><span data-stu-id="6d36d-169">*Table* is the default.</span></span>


```json
{
    "WadCfg": {
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```xml
<PublicConfig>
    <WadCfg />
    <StorageAccount>diagstorageaccount</StorageAccount>
    <StorageType>TableAndBlob</StorageType>
</PublicConfig>
```


### <a name="diagnostics-extension-17"></a><span data-ttu-id="6d36d-170">診斷擴充功能 1.7 版</span><span class="sxs-lookup"><span data-stu-id="6d36d-170">Diagnostics extension 1.7</span></span> 
<span data-ttu-id="6d36d-171">已新增路由至 EventHub 的能力。</span><span class="sxs-lookup"><span data-stu-id="6d36d-171">Added the ability to route to EventHub.</span></span>

### <a name="diagnostics-extension-15"></a><span data-ttu-id="6d36d-172">診斷延伸模組 1.5 版</span><span class="sxs-lookup"><span data-stu-id="6d36d-172">Diagnostics extension 1.5</span></span>
<span data-ttu-id="6d36d-173">已增加接收器元素以及將診斷資料傳送至 [Application Insights](../application-insights/app-insights-cloudservices.md) 的能力，因此可更容易在應用程式以及系統和基礎結構層級中診斷問題。</span><span class="sxs-lookup"><span data-stu-id="6d36d-173">Added the sinks element and the ability to send diagnostics data to [Application Insights](../application-insights/app-insights-cloudservices.md) making it easier to diagnose issues across your application as well as the system and infrastructure level.</span></span>

### <a name="azure-sdk-26-and-diagnostics-extension-13"></a><span data-ttu-id="6d36d-174">Azure SDK 2.6 和診斷擴充功能 1.3 版</span><span class="sxs-lookup"><span data-stu-id="6d36d-174">Azure SDK 2.6 and diagnostics extension 1.3</span></span> 
<span data-ttu-id="6d36d-175">我們已對 Visual Studio 中的雲端服務專案進行下列變更。</span><span class="sxs-lookup"><span data-stu-id="6d36d-175">For Cloud Service projects in Visual Studio, the following changes were made.</span></span> <span data-ttu-id="6d36d-176">(這些變更也套用至更新版的 Azure SDK)。</span><span class="sxs-lookup"><span data-stu-id="6d36d-176">(These changes also apply to later versions of Azure SDK.)</span></span>

* <span data-ttu-id="6d36d-177">本機模擬器現在支援診斷。</span><span class="sxs-lookup"><span data-stu-id="6d36d-177">The local emulator now supports diagnostics.</span></span> <span data-ttu-id="6d36d-178">這表示您可以收集診斷資料並確保您在 Visual Studio 中進行開發及測試時，您的應用程式在建立正確的追蹤。</span><span class="sxs-lookup"><span data-stu-id="6d36d-178">This means you can collect diagnostics data and ensure your application is creating the right traces while you're developing and testing in Visual Studio.</span></span> <span data-ttu-id="6d36d-179">當您在 Visual Studio 中使用 Azure 儲存體模擬器來執行您的雲端服務專案時，連接字串 `UseDevelopmentStorage=true` 會啟用診斷資料收集。</span><span class="sxs-lookup"><span data-stu-id="6d36d-179">The connection string `UseDevelopmentStorage=true` enables diagnostics data collection while you're running your cloud service project in Visual Studio by using the Azure storage emulator.</span></span> <span data-ttu-id="6d36d-180">所有的診斷資料都會收集到 (開發儲存體) 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="6d36d-180">All diagnostics data is collected in the (Development Storage) storage account.</span></span>
* <span data-ttu-id="6d36d-181">診斷儲存體帳戶連接字串 (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) 會再一次儲存在服務組態 (.cscfg) 檔中。</span><span class="sxs-lookup"><span data-stu-id="6d36d-181">The diagnostics storage account connection string (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) is stored once again in the service configuration (.cscfg) file.</span></span> <span data-ttu-id="6d36d-182">在 Azure SDK 2.5 中，診斷儲存體帳戶會在 diagnostics.wadcfgx 檔案中指定。</span><span class="sxs-lookup"><span data-stu-id="6d36d-182">In Azure SDK 2.5 the diagnostics storage account was specified in the diagnostics.wadcfgx file.</span></span>

<span data-ttu-id="6d36d-183">連接字串在 Azure SDK 2.4 及更舊版本和 Azure SDK 2.6 及更新版本中的運作方式有一些顯著的差異。</span><span class="sxs-lookup"><span data-stu-id="6d36d-183">There are some notable differences between how the connection string worked in Azure SDK 2.4 and earlier and how it works in Azure SDK 2.6 and later.</span></span>

* <span data-ttu-id="6d36d-184">在 Azure SDK 2.4 及更舊版本中，階段診斷外掛程式使用連接字串做為執行階段，以取得用於傳輸診斷記錄檔的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="6d36d-184">In Azure SDK 2.4 and earlier, the connection string was used as a runtime by the diagnostics plugin to get the storage account information for transferring diagnostics logs.</span></span>
* <span data-ttu-id="6d36d-185">在 Azure SDK 2.6 及更新版本中，Visual studio 會使用診斷連接字串，在發佈期間設定內含適當儲存體帳戶資訊的診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="6d36d-185">In Azure SDK 2.6 and later, the diagnostics connection string is used by Visual Studio to configure the diagnostics extension with the appropriate storage account information during publishing.</span></span> <span data-ttu-id="6d36d-186">連接字串可讓您為 Visual Studio 在發佈時將使用的不同服務組態定義不同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d36d-186">The connection string lets you define different storage accounts for different service configurations that Visual Studio will use when publishing.</span></span> <span data-ttu-id="6d36d-187">不過，因為診斷外掛程式 (在 Azure SDK 2.5 之後) 不再提供使用，所以 .cscfg 檔案本身無法啟用診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="6d36d-187">However, because the diagnostics plugin is no longer available (after Azure SDK 2.5), the .cscfg file by itself can't enable the Diagnostics Extension.</span></span> <span data-ttu-id="6d36d-188">您必須個別透過 Visual Studio 或 PowerShell 等工具啟用延伸模組。</span><span class="sxs-lookup"><span data-stu-id="6d36d-188">You have to enable the extension separately through tools such as Visual Studio or PowerShell.</span></span>
* <span data-ttu-id="6d36d-189">為了使用 PowerShell 簡化診斷延伸模組的設定程序，從 Visual Studio 的封裝輸出也包含每個角色之診斷延伸模組的公用組態 XML。</span><span class="sxs-lookup"><span data-stu-id="6d36d-189">To simplify the process of configuring the diagnostics extension with PowerShell, the package output from Visual Studio also contains the public configuration XML for the diagnostics extension for each role.</span></span> <span data-ttu-id="6d36d-190">Visual Studio 使用診斷連接字串填入出現在公用組態的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="6d36d-190">Visual Studio uses the diagnostics connection string to populate the storage account information present in the public configuration.</span></span> <span data-ttu-id="6d36d-191">公用設定檔會在延伸模組資料夾中建立並遵循模式 PaaSDiagnostics<RoleName>.PubConfig.xml。</span><span class="sxs-lookup"><span data-stu-id="6d36d-191">The public config files are created in the Extensions folder and follow the pattern PaaSDiagnostics.<RoleName>.PubConfig.xml.</span></span> <span data-ttu-id="6d36d-192">任何以 PowerShell 為基礎的部署都可以使用此模式將每個組態對應至角色。</span><span class="sxs-lookup"><span data-stu-id="6d36d-192">Any PowerShell based deployments can use this pattern to map each configuration to a Role.</span></span>
* <span data-ttu-id="6d36d-193">Azure 入口網站也會使用 .cscfg 檔案中的連接字串來存取診斷資料，所以它也可以出現在 [監視]  索引標籤中。</span><span class="sxs-lookup"><span data-stu-id="6d36d-193">The connection string in the .cscfg file is also used by the Azure portal to access the diagnostics data so it can appear in the **Monitoring** tab.</span></span> <span data-ttu-id="6d36d-194">若要在入口網站中顯示詳細監視資料，必須要有連接字串。</span><span class="sxs-lookup"><span data-stu-id="6d36d-194">The connection string is needed to configure the service to show verbose monitoring data in the portal.</span></span>

#### <a name="migrating-projects-to-azure-sdk-26-and-later"></a><span data-ttu-id="6d36d-195">將專案移轉至 Azure SDK 2.6 及、更新版本</span><span class="sxs-lookup"><span data-stu-id="6d36d-195">Migrating projects to Azure SDK 2.6 and later</span></span>
<span data-ttu-id="6d36d-196">從 Azure SDK 2.5 移轉至 Azure SDK 2.6 或更新版本時，如果您在 .wadcfgx 檔案中指定診斷儲存體帳戶，它就會留在那裡。</span><span class="sxs-lookup"><span data-stu-id="6d36d-196">When migrating from Azure SDK 2.5 to Azure SDK 2.6 or later, if you had a diagnostics storage account specified in the .wadcfgx file, then it will stay there.</span></span> <span data-ttu-id="6d36d-197">若要針對不同儲存體組態充分利用不同儲存體帳戶的靈活性，您必須手動將連接字串加入專案。</span><span class="sxs-lookup"><span data-stu-id="6d36d-197">To take advantage of the flexibility of using different storage accounts for different storage configurations, you'll have to manually add the connection string to your project.</span></span> <span data-ttu-id="6d36d-198">如果您將專案從 Azure SDK 2.4 或更早版本移轉至 Azure SDK 2.6，系統會保留診斷連接字串。</span><span class="sxs-lookup"><span data-stu-id="6d36d-198">If you're migrating a project from Azure SDK 2.4 or earlier to Azure SDK 2.6, then the diagnostics connection strings are preserved.</span></span> <span data-ttu-id="6d36d-199">不過，請注意上一節中指定之 Azure SDK 2.6 中連接字串處理方式的變更。</span><span class="sxs-lookup"><span data-stu-id="6d36d-199">However, please note the changes in how connection strings are treated in Azure SDK 2.6 as specified in the previous section.</span></span>

#### <a name="how-visual-studio-determines-the-diagnostics-storage-account"></a><span data-ttu-id="6d36d-200">Visual Studio 如何決定診斷儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="6d36d-200">How Visual Studio determines the diagnostics storage account</span></span>
* <span data-ttu-id="6d36d-201">如果在 .cscfg 檔案中指定診斷連接字串，Visual Studio 會在發佈時，以及在封裝期間產生公用組態 xml 檔案時使用它來設定診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="6d36d-201">If a diagnostics connection string is specified in the .cscfg file, Visual Studio uses it to configure the diagnostics extension when publishing, and when generating the public configuration xml files during packaging.</span></span>
* <span data-ttu-id="6d36d-202">如果未在 .cscfg 檔案中指定診斷連接字串，Visual Studio 會回復到在發佈時，以及在封裝期間產生公用組態 xml 檔案時使用在 .wadcfgx 檔案中指定的儲存體帳戶來設定診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="6d36d-202">If no diagnostics connection string is specified in the .cscfg file, then Visual Studio falls back to using the storage account specified in the .wadcfgx file to configure the diagnostics extension when publishing, and generating the public configuration xml files when packaging.</span></span>
* <span data-ttu-id="6d36d-203">在 .cscfg 檔案中的診斷連接字串的優先順序高於 .wadcfgx 檔案中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d36d-203">The diagnostics connection string in the .cscfg file takes precedence over the storage account in the .wadcfgx file.</span></span> <span data-ttu-id="6d36d-204">如果在 .cscfg 檔案中指定診斷連接字串，Visual Studio 會使用它並忽略 .wadcfgx 中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d36d-204">If a diagnostics connection string is specified in the .cscfg file, then Visual Studio uses that and ignores the storage account in .wadcfgx.</span></span>

#### <a name="what-does-the-update-development-storage-connection-strings-checkbox-do"></a><span data-ttu-id="6d36d-205">「更新開發儲存體連接字串...」核取方塊的</span><span class="sxs-lookup"><span data-stu-id="6d36d-205">What does the "Update development storage connection strings…"</span></span> <span data-ttu-id="6d36d-206">作用為何？</span><span class="sxs-lookup"><span data-stu-id="6d36d-206">checkbox do?</span></span>
<span data-ttu-id="6d36d-207">[在發佈至 Microsoft Azure 時使用 Microsoft Azure 儲存體帳戶認證更新診斷和快取的開發儲存體連接字串]  核取方塊提供便利的方式，使用發佈期間指定的 Azure 儲存體帳戶更新任何開發儲存體帳戶連接字串。</span><span class="sxs-lookup"><span data-stu-id="6d36d-207">The checkbox for **Update development storage connection strings for Diagnostics and Caching with Microsoft Azure storage account credentials when publishing to Microsoft Azure** gives you a convenient way to update any development storage account connection strings with the Azure storage account specified during publishing.</span></span>

<span data-ttu-id="6d36d-208">例如，假設您選取此核取方塊，診斷連接字串就會指定 `UseDevelopmentStorage=true`。</span><span class="sxs-lookup"><span data-stu-id="6d36d-208">For example, suppose you select this checkbox and the diagnostics connection string specifies `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="6d36d-209">當您將專案發佈至 Azure 時，Visual Studio 會自動使用您在 [發佈] 精靈中指定的儲存體帳戶更新診斷連接字串。</span><span class="sxs-lookup"><span data-stu-id="6d36d-209">When you publish the project to Azure, Visual Studio will automatically update the diagnostics connection string with the storage account you specified in the Publish wizard.</span></span> <span data-ttu-id="6d36d-210">不過，如果將實際的儲存體帳戶指定為診斷連接字串，則會改用該帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d36d-210">However, if a real storage account was specified as the diagnostics connection string, then that account is used instead.</span></span>

### <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a><span data-ttu-id="6d36d-211">Azure SDK 2.4 及更舊版本和 Azure SDK 2.5 及更新版本之間的診斷功能差異</span><span class="sxs-lookup"><span data-stu-id="6d36d-211">Diagnostics functionality differences between Azure SDK 2.4 and earlier and Azure SDK 2.5 and later</span></span>
<span data-ttu-id="6d36d-212">如果您要將專案從 Azure SDK 2.4 更新為 Azure SDK 2.5 或更新版本，您應該謹記下列診斷功能差異。</span><span class="sxs-lookup"><span data-stu-id="6d36d-212">If you're upgrading your project from Azure SDK 2.4 to Azure SDK 2.5 or later, you should bear in mind the following diagnostics functionality differences.</span></span>

* <span data-ttu-id="6d36d-213">**組態 API 已被取代** – 診斷的程式設計組態可在 Azure SDK 2.4 或更舊版本中使用，但在 Azure SDK 2.5 及更新版本中已被取代。</span><span class="sxs-lookup"><span data-stu-id="6d36d-213">**Configuration APIs are deprecated** – Programmatic configuration of diagnostics is available in Azure SDK 2.4 or earlier versions, but is deprecated in Azure SDK 2.5 and later.</span></span> <span data-ttu-id="6d36d-214">如果診斷組態目前以程式碼定義，您將需要在移轉專案中從頭開始進行這些設定才能讓診斷保持運作。</span><span class="sxs-lookup"><span data-stu-id="6d36d-214">If your diagnostics configuration is currently defined in code, you'll need to reconfigure those settings from scratch in the migrated project in order for diagnostics to keep working.</span></span> <span data-ttu-id="6d36d-215">Azure SDK 2.4 的診斷組態檔是 diagnostics.wadcfg，而 diagnostics.wadcfgx 是 Azure SDK 2.5 及更新版本的診斷組態檔。</span><span class="sxs-lookup"><span data-stu-id="6d36d-215">The diagnostics configuration file for Azure SDK 2.4 is diagnostics.wadcfg, and diagnostics.wadcfgx for Azure SDK 2.5 and later.</span></span>
* <span data-ttu-id="6d36d-216">**雲端服務應用程式的診斷只能在角色層級設定，而不是在執行個體層級。**</span><span class="sxs-lookup"><span data-stu-id="6d36d-216">**Diagnostics for cloud service applications can only be configured at the role level, not at the instance level.**</span></span>
* <span data-ttu-id="6d36d-217">**每次部署您的應用程式時，都會更新診斷組態** – 如果您從 [伺服器總管] 變更診斷組態並重新部署您的應用程式，會導致同位檢查的問題。</span><span class="sxs-lookup"><span data-stu-id="6d36d-217">**Every time you deploy your app, the diagnostics configuration is updated** – This can cause parity issues if you change your diagnostics configuration from Server Explorer and then redeploy your app.</span></span>
* <span data-ttu-id="6d36d-218">**在 Azure SDK 2.5 及更新版本中，損毀傾印不會以診斷組態檔設定** – 如果您以程式碼設定損毀傾印，您必須手動將組態從程式碼傳輸至組態檔中，因為損毀傾印不會在移轉至 Azure SDK 2.6 期間傳輸。</span><span class="sxs-lookup"><span data-stu-id="6d36d-218">**In Azure SDK 2.5 and later, crash dumps are configured in the diagnostics configuration file, not in code** – If you have crash dumps configured in code, you'll have to manually transfer the configuration from code to the configuration file, because the crash dumps aren't transferred during the migration to Azure SDK 2.6.</span></span>

