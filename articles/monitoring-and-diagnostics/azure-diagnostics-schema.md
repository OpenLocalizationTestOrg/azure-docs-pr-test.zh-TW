---
title: "aaaAzure 診斷副檔名組態結構描述版本與歷程記錄 |Microsoft 文件"
description: "在 Azure 虛擬機器、 VM 規模集、 Service Fabric 和雲端服務的相關 toocollecting 效能計數器。"
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
ms.openlocfilehash: 854ad118f660810aa38703670284794d658142c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-extention-configuration-schema-versions-and-history"></a><span data-ttu-id="0bc3f-103">Azure 診斷延伸模組的設定結構描述版本和歷程記錄</span><span class="sxs-lookup"><span data-stu-id="0bc3f-103">Azure Diagnostics extention configuration schema versions and history</span></span>
<span data-ttu-id="0bc3f-104">此頁面索引 Azure 診斷擴充功能的結構描述版本隨附於 hello Microsoft Azure SDK 的一部分。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-104">This page indexes Azure Diagnostics extension schema versions shipped as part of hello Microsoft Azure SDK.</span></span>  

> [!NOTE]
> <span data-ttu-id="0bc3f-105">hello Azure 診斷擴充功能是 hello 元件使用 toocollect 效能計數器和其他統計資料：</span><span class="sxs-lookup"><span data-stu-id="0bc3f-105">hello Azure Diagnostics extension is hello component used toocollect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="0bc3f-106">Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0bc3f-106">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="0bc3f-107">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="0bc3f-107">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="0bc3f-108">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0bc3f-108">Service Fabric</span></span> 
> - <span data-ttu-id="0bc3f-109">雲端服務</span><span class="sxs-lookup"><span data-stu-id="0bc3f-109">Cloud Services</span></span> 
> - <span data-ttu-id="0bc3f-110">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="0bc3f-110">Network Security Groups</span></span>
> 
> <span data-ttu-id="0bc3f-111">此頁面只在您使用其中一個服務時才相關。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-111">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="0bc3f-112">hello Azure 診斷延伸模組可搭配 Azure 監視、 Application Insights 和記錄分析等其他 Microsoft 診斷產品。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-112">hello Azure Diagnostics extension is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span> <span data-ttu-id="0bc3f-113">如需詳細資訊，請參閱 [Microsoft 監視工具概觀](monitoring-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-113">For more information see [Microsoft Monitoring Tools Overview](monitoring-overview.md).</span></span>

## <a name="azure-sdk-and-diagnostics-versions-shipping-chart"></a><span data-ttu-id="0bc3f-114">Azure SDK 和診斷版本推出方式圖表</span><span class="sxs-lookup"><span data-stu-id="0bc3f-114">Azure SDK and diagnostics versions shipping chart</span></span>  

|<span data-ttu-id="0bc3f-115">Azure SDK 版本</span><span class="sxs-lookup"><span data-stu-id="0bc3f-115">Azure SDK version</span></span> | <span data-ttu-id="0bc3f-116">診斷擴充功能版本</span><span class="sxs-lookup"><span data-stu-id="0bc3f-116">Diagnostics extension version</span></span> | <span data-ttu-id="0bc3f-117">模型</span><span class="sxs-lookup"><span data-stu-id="0bc3f-117">Model</span></span>|  
|------------------|-------------------------------|------|  
|<span data-ttu-id="0bc3f-118">1.x</span><span class="sxs-lookup"><span data-stu-id="0bc3f-118">1.x</span></span>               |<span data-ttu-id="0bc3f-119">1.0</span><span class="sxs-lookup"><span data-stu-id="0bc3f-119">1.0</span></span>                            |<span data-ttu-id="0bc3f-120">外掛程式</span><span class="sxs-lookup"><span data-stu-id="0bc3f-120">plug-in</span></span>|  
|<span data-ttu-id="0bc3f-121">2.0 - 2.4</span><span class="sxs-lookup"><span data-stu-id="0bc3f-121">2.0 - 2.4</span></span>         |<span data-ttu-id="0bc3f-122">1.0</span><span class="sxs-lookup"><span data-stu-id="0bc3f-122">1.0</span></span>                            |<span data-ttu-id="0bc3f-123">外掛程式</span><span class="sxs-lookup"><span data-stu-id="0bc3f-123">plug-in</span></span>|  
|<span data-ttu-id="0bc3f-124">2.5</span><span class="sxs-lookup"><span data-stu-id="0bc3f-124">2.5</span></span>               |<span data-ttu-id="0bc3f-125">1.2</span><span class="sxs-lookup"><span data-stu-id="0bc3f-125">1.2</span></span>                            |<span data-ttu-id="0bc3f-126">擴充功能</span><span class="sxs-lookup"><span data-stu-id="0bc3f-126">extension</span></span>|  
|<span data-ttu-id="0bc3f-127">2.6</span><span class="sxs-lookup"><span data-stu-id="0bc3f-127">2.6</span></span>               |<span data-ttu-id="0bc3f-128">1.3</span><span class="sxs-lookup"><span data-stu-id="0bc3f-128">1.3</span></span>                            |<span data-ttu-id="0bc3f-129">"</span><span class="sxs-lookup"><span data-stu-id="0bc3f-129">"</span></span>|  
|<span data-ttu-id="0bc3f-130">2.7</span><span class="sxs-lookup"><span data-stu-id="0bc3f-130">2.7</span></span>               |<span data-ttu-id="0bc3f-131">1.4</span><span class="sxs-lookup"><span data-stu-id="0bc3f-131">1.4</span></span>                            |<span data-ttu-id="0bc3f-132">"</span><span class="sxs-lookup"><span data-stu-id="0bc3f-132">"</span></span>|  
|<span data-ttu-id="0bc3f-133">2.8</span><span class="sxs-lookup"><span data-stu-id="0bc3f-133">2.8</span></span>               |<span data-ttu-id="0bc3f-134">1.5</span><span class="sxs-lookup"><span data-stu-id="0bc3f-134">1.5</span></span>                            |<span data-ttu-id="0bc3f-135">"</span><span class="sxs-lookup"><span data-stu-id="0bc3f-135">"</span></span>|  
|<span data-ttu-id="0bc3f-136">2.9</span><span class="sxs-lookup"><span data-stu-id="0bc3f-136">2.9</span></span>               |<span data-ttu-id="0bc3f-137">1.6</span><span class="sxs-lookup"><span data-stu-id="0bc3f-137">1.6</span></span>                            |<span data-ttu-id="0bc3f-138">"</span><span class="sxs-lookup"><span data-stu-id="0bc3f-138">"</span></span>|
|<span data-ttu-id="0bc3f-139">2.96</span><span class="sxs-lookup"><span data-stu-id="0bc3f-139">2.96</span></span>              |<span data-ttu-id="0bc3f-140">1.7</span><span class="sxs-lookup"><span data-stu-id="0bc3f-140">1.7</span></span>                            |<span data-ttu-id="0bc3f-141">"</span><span class="sxs-lookup"><span data-stu-id="0bc3f-141">"</span></span>|
|<span data-ttu-id="0bc3f-142">2.96</span><span class="sxs-lookup"><span data-stu-id="0bc3f-142">2.96</span></span>              |<span data-ttu-id="0bc3f-143">1.8</span><span class="sxs-lookup"><span data-stu-id="0bc3f-143">1.8</span></span>                            |<span data-ttu-id="0bc3f-144">"</span><span class="sxs-lookup"><span data-stu-id="0bc3f-144">"</span></span>|
|<span data-ttu-id="0bc3f-145">2.96</span><span class="sxs-lookup"><span data-stu-id="0bc3f-145">2.96</span></span>              |<span data-ttu-id="0bc3f-146">1.8.1</span><span class="sxs-lookup"><span data-stu-id="0bc3f-146">1.8.1</span></span>                          |<span data-ttu-id="0bc3f-147">"</span><span class="sxs-lookup"><span data-stu-id="0bc3f-147">"</span></span>|
|<span data-ttu-id="0bc3f-148">2.96</span><span class="sxs-lookup"><span data-stu-id="0bc3f-148">2.96</span></span>              |<span data-ttu-id="0bc3f-149">1.9</span><span class="sxs-lookup"><span data-stu-id="0bc3f-149">1.9</span></span>                            |<span data-ttu-id="0bc3f-150">"</span><span class="sxs-lookup"><span data-stu-id="0bc3f-150">"</span></span>|



 <span data-ttu-id="0bc3f-151">Azure 診斷 1.0 版第一次隨附在外掛程式模型--這表示安裝 hello Azure SDK 之後，您會收到 hello 版本隨附於它的 Azure 診斷。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-151">Azure Diagnostics version 1.0 first shipped in a plug-in model -- meaning that when you installed hello Azure SDK, you got hello version of Azure diagnostics shipped with it.</span></span>  

 <span data-ttu-id="0bc3f-152">SDK 2.5 （診斷 1.2 版），從 Azure 診斷發生 tooan 延伸模型。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-152">Starting with SDK 2.5 (diagnostics version 1.2), Azure diagnostics went tooan extension model.</span></span> <span data-ttu-id="0bc3f-153">hello 工具 tooutilize 新功能只用於較新的 Azure Sdk，但使用 Azure 診斷的任何服務將會收取 hello 傳送新版直接從 Azure。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-153">hello tools tooutilize new features were only available in newer Azure SDKs, but any service using Azure diagnostics would pick up hello latest shipping version directly from Azure.</span></span> <span data-ttu-id="0bc3f-154">比方說，仍在使用 SDK 2.5 的任何人都可以載入 hello 最新版本中所顯示 hello 上表中，不論他們使用 hello 較新的功能。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-154">For example, anyone still using SDK 2.5 would be loading hello latest version shown in hello previous table, regardless if they are using hello newer features.</span></span>  

## <a name="schemas-index"></a><span data-ttu-id="0bc3f-155">結構描述索引</span><span class="sxs-lookup"><span data-stu-id="0bc3f-155">Schemas index</span></span>  
<span data-ttu-id="0bc3f-156">不同版本的 Azure 診斷會使用不同的組態結構描述。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-156">Different versions of Azure diagnostics use different configuration schemas.</span></span> 

[<span data-ttu-id="0bc3f-157">Azure 診斷 1.0 組態結構描述</span><span class="sxs-lookup"><span data-stu-id="0bc3f-157">Diagnostics 1.0 Configuration Schema</span></span>](azure-diagnostics-schema-1dot0.md)  

[<span data-ttu-id="0bc3f-158">Azure 診斷 1.2 組態結構描述</span><span class="sxs-lookup"><span data-stu-id="0bc3f-158">Diagnostics 1.2 Configuration Schema</span></span>](azure-diagnostics-schema-1dot2.md)  

[<span data-ttu-id="0bc3f-159">診斷 1.3 和更新版本的組態結構描述</span><span class="sxs-lookup"><span data-stu-id="0bc3f-159">Diagnostics 1.3 and later Configuration Schema</span></span>](azure-diagnostics-schema-1dot3-and-later.md)  

## <a name="version-history"></a><span data-ttu-id="0bc3f-160">版本歷程記錄</span><span class="sxs-lookup"><span data-stu-id="0bc3f-160">Version history</span></span>


### <a name="diagnostics-extension-19"></a><span data-ttu-id="0bc3f-161">診斷擴充功能 1.9 版</span><span class="sxs-lookup"><span data-stu-id="0bc3f-161">Diagnostics extension 1.9</span></span> 
<span data-ttu-id="0bc3f-162">已新增 Docker 支援。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-162">Added Docker support.</span></span>


### <a name="diagnostics-extension-181"></a><span data-ttu-id="0bc3f-163">診斷擴充功能 1.8.1 版</span><span class="sxs-lookup"><span data-stu-id="0bc3f-163">Diagnostics extension 1.8.1</span></span> 
<span data-ttu-id="0bc3f-164">可以在 hello 私用組態中指定的 SAS 權杖，而不是儲存體帳戶金鑰。如果提供的 SAS 權杖，則會忽略 hello 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-164">Can specify a SAS token instead of a storage account key in hello private config. If a SAS token is provided, hello storage account key is ignored.</span></span>


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


### <a name="diagnostics-extension-18"></a><span data-ttu-id="0bc3f-165">診斷擴充功能 1.8 版</span><span class="sxs-lookup"><span data-stu-id="0bc3f-165">Diagnostics extension 1.8</span></span> 
<span data-ttu-id="0bc3f-166">加入儲存體類型 tooPublicConfig。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-166">Added Storage Type tooPublicConfig.</span></span> <span data-ttu-id="0bc3f-167">StorageType 可以是 Table、Blob、TableAndBlob。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-167">StorageType can be *Table*, *Blob*, *TableAndBlob*.</span></span> <span data-ttu-id="0bc3f-168">*資料表*hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-168">*Table* is hello default.</span></span>


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


### <a name="diagnostics-extension-17"></a><span data-ttu-id="0bc3f-169">診斷擴充功能 1.7 版</span><span class="sxs-lookup"><span data-stu-id="0bc3f-169">Diagnostics extension 1.7</span></span> 
<span data-ttu-id="0bc3f-170">加入的 hello 能力 tooroute tooEventHub。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-170">Added hello ability tooroute tooEventHub.</span></span>

### <a name="diagnostics-extension-15"></a><span data-ttu-id="0bc3f-171">診斷延伸模組 1.5 版</span><span class="sxs-lookup"><span data-stu-id="0bc3f-171">Diagnostics extension 1.5</span></span>
<span data-ttu-id="0bc3f-172">加入 hello 接收器元素與 hello 能力 toosend 診斷資料太[Application Insights](../application-insights/app-insights-cloudservices.md)讓它更容易 toodiagnose 問題跨您應用程式，以及 hello 系統和基礎結構層級。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-172">Added hello sinks element and hello ability toosend diagnostics data too[Application Insights](../application-insights/app-insights-cloudservices.md) making it easier toodiagnose issues across your application as well as hello system and infrastructure level.</span></span>

### <a name="azure-sdk-26-and-diagnostics-extension-13"></a><span data-ttu-id="0bc3f-173">Azure SDK 2.6 和診斷擴充功能 1.3 版</span><span class="sxs-lookup"><span data-stu-id="0bc3f-173">Azure SDK 2.6 and diagnostics extension 1.3</span></span> 
<span data-ttu-id="0bc3f-174">Visual Studio 中的雲端服務專案，進行下列變更 hello。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-174">For Cloud Service projects in Visual Studio, hello following changes were made.</span></span> <span data-ttu-id="0bc3f-175">（這些變更也適用於 Azure SDK toolater 版本。）</span><span class="sxs-lookup"><span data-stu-id="0bc3f-175">(These changes also apply toolater versions of Azure SDK.)</span></span>

* <span data-ttu-id="0bc3f-176">hello 本機模擬器現在支援診斷。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-176">hello local emulator now supports diagnostics.</span></span> <span data-ttu-id="0bc3f-177">這表示您可以收集診斷資料，並確認您的應用程式會建立 hello 正確的追蹤時您正在開發和測試 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-177">This means you can collect diagnostics data and ensure your application is creating hello right traces while you're developing and testing in Visual Studio.</span></span> <span data-ttu-id="0bc3f-178">hello 連接字串`UseDevelopmentStorage=true`時，您在 Visual Studio 中執行雲端服務專案，使用 hello Azure 儲存體模擬器，請啟用收集診斷資料。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-178">hello connection string `UseDevelopmentStorage=true` enables diagnostics data collection while you're running your cloud service project in Visual Studio by using hello Azure storage emulator.</span></span> <span data-ttu-id="0bc3f-179">所有診斷資料都收集 hello （開發儲存體） 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-179">All diagnostics data is collected in hello (Development Storage) storage account.</span></span>
* <span data-ttu-id="0bc3f-180">hello 診斷儲存體帳戶連接字串 (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) 再一次儲存 hello 服務組態 (.cscfg) 檔中。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-180">hello diagnostics storage account connection string (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) is stored once again in hello service configuration (.cscfg) file.</span></span> <span data-ttu-id="0bc3f-181">在 Azure SDK 2.5 hello 診斷儲存體帳戶指定 hello diagnostics.wadcfgx 檔案中。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-181">In Azure SDK 2.5 hello diagnostics storage account was specified in hello diagnostics.wadcfgx file.</span></span>

<span data-ttu-id="0bc3f-182">有一些值得注意的差異之間 hello 連接字串已在 Azure SDK 2.4 及更早版本的運作，而且在 Azure SDK 2.6 和更新版本，它的運作方式。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-182">There are some notable differences between how hello connection string worked in Azure SDK 2.4 and earlier and how it works in Azure SDK 2.6 and later.</span></span>

* <span data-ttu-id="0bc3f-183">在 Azure SDK 2.4 及更早版本，hello 已使用的連接字串做為執行階段 hello 診斷外掛程式 tooget hello 儲存體帳戶資訊的傳輸診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-183">In Azure SDK 2.4 and earlier, hello connection string was used as a runtime by hello diagnostics plugin tooget hello storage account information for transferring diagnostics logs.</span></span>
* <span data-ttu-id="0bc3f-184">在 Azure SDK 2.6 和更新版本，hello 診斷連接字串使用 Visual Studio tooconfigure hello 診斷延伸模組以在發行期間的 hello 適當的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-184">In Azure SDK 2.6 and later, hello diagnostics connection string is used by Visual Studio tooconfigure hello diagnostics extension with hello appropriate storage account information during publishing.</span></span> <span data-ttu-id="0bc3f-185">hello 連接字串可讓您定義不同的服務組態，Visual Studio 在發行時使用不同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-185">hello connection string lets you define different storage accounts for different service configurations that Visual Studio will use when publishing.</span></span> <span data-ttu-id="0bc3f-186">不過，因為 （在 Azure SDK 2.5) 已無法再使用 hello 診斷外掛程式，hello.cscfg 檔案本身無法啟用 hello 診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-186">However, because hello diagnostics plugin is no longer available (after Azure SDK 2.5), hello .cscfg file by itself can't enable hello Diagnostics Extension.</span></span> <span data-ttu-id="0bc3f-187">您有透過 Visual Studio 或 PowerShell 之類的工具來分別 tooenable hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-187">You have tooenable hello extension separately through tools such as Visual Studio or PowerShell.</span></span>
* <span data-ttu-id="0bc3f-188">toosimplify hello 程序使用 PowerShell 設定 hello 診斷延伸模組，從 Visual Studio 的 hello 封裝輸出也包含 hello 公用組態 XML，每個角色的 hello 診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-188">toosimplify hello process of configuring hello diagnostics extension with PowerShell, hello package output from Visual Studio also contains hello public configuration XML for hello diagnostics extension for each role.</span></span> <span data-ttu-id="0bc3f-189">Visual Studio 使用 hello 診斷連接字串 toopopulate hello 儲存體帳戶資訊出現在 hello 公用組態。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-189">Visual Studio uses hello diagnostics connection string toopopulate hello storage account information present in hello public configuration.</span></span> <span data-ttu-id="0bc3f-190">hello 公用組態檔 hello 擴充功能 資料夾中建立，並遵循 Paasdiagnostics.<rolename>.pubconfig.xml 的 hello 模式。<RoleName>.模式。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-190">hello public config files are created in hello Extensions folder and follow hello pattern PaaSDiagnostics.<RoleName>.PubConfig.xml.</span></span> <span data-ttu-id="0bc3f-191">任何 PowerShell 部署可以使用此模式 toomap 每個組態 tooa 角色。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-191">Any PowerShell based deployments can use this pattern toomap each configuration tooa Role.</span></span>
* <span data-ttu-id="0bc3f-192">hello hello.cscfg 檔案中的連接字串也會使用 hello Azure 入口網站 tooaccess hello 診斷資料，它可以出現在 hello**監視** 索引標籤 hello 連接字串是所需的 tooconfigure hello 服務 tooshow 詳細資訊hello 入口網站中的監視資料。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-192">hello connection string in hello .cscfg file is also used by hello Azure portal tooaccess hello diagnostics data so it can appear in hello **Monitoring** tab. hello connection string is needed tooconfigure hello service tooshow verbose monitoring data in hello portal.</span></span>

#### <a name="migrating-projects-tooazure-sdk-26-and-later"></a><span data-ttu-id="0bc3f-193">移轉專案 tooAzure SDK 2.6 和更新版本</span><span class="sxs-lookup"><span data-stu-id="0bc3f-193">Migrating projects tooAzure SDK 2.6 and later</span></span>
<span data-ttu-id="0bc3f-194">當移轉從 Azure SDK 2.5 tooAzure SDK 2.6 或更新版本，如果您在診斷儲存體帳戶，指定在 hello.wadcfgx 檔案中，然後它會留在那裡。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-194">When migrating from Azure SDK 2.5 tooAzure SDK 2.6 or later, if you had a diagnostics storage account specified in hello .wadcfgx file, then it will stay there.</span></span> <span data-ttu-id="0bc3f-195">tootake 優點 hello 彈性使用不同的儲存體帳戶的不同存放裝置組態，您必須加入 hello 連接字串 tooyour 專案 toomanually。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-195">tootake advantage of hello flexibility of using different storage accounts for different storage configurations, you'll have toomanually add hello connection string tooyour project.</span></span> <span data-ttu-id="0bc3f-196">如果您從 Azure SDK 2.4 或較早 tooAzure SDK 2.6 移轉專案，然後 hello 的診斷連接字串會保留。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-196">If you're migrating a project from Azure SDK 2.4 or earlier tooAzure SDK 2.6, then hello diagnostics connection strings are preserved.</span></span> <span data-ttu-id="0bc3f-197">不過，請注意 hello 變更連接字串中的處理方式在 Azure SDK 2.6 中所述的 hello 上一節。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-197">However, please note hello changes in how connection strings are treated in Azure SDK 2.6 as specified in hello previous section.</span></span>

#### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a><span data-ttu-id="0bc3f-198">Visual Studio 如何決定 hello 診斷儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="0bc3f-198">How Visual Studio determines hello diagnostics storage account</span></span>
* <span data-ttu-id="0bc3f-199">如果 hello.cscfg 檔案中指定診斷連接字串，Visual Studio 會使用 tooconfigure hello 診斷擴充功能發行時，並在封裝期間產生 hello 公用組態 xml 檔案時。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-199">If a diagnostics connection string is specified in hello .cscfg file, Visual Studio uses it tooconfigure hello diagnostics extension when publishing, and when generating hello public configuration xml files during packaging.</span></span>
* <span data-ttu-id="0bc3f-200">如果 hello.cscfg 檔案中不指定任何診斷連接字串，然後 Visual Studio 會回復指定 hello.wadcfgx 檔案 tooconfigure hello 診斷擴充功能發行時及產生 hello 公用 toousing hello 儲存體帳戶設定 xml 檔案封裝時。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-200">If no diagnostics connection string is specified in hello .cscfg file, then Visual Studio falls back toousing hello storage account specified in hello .wadcfgx file tooconfigure hello diagnostics extension when publishing, and generating hello public configuration xml files when packaging.</span></span>
* <span data-ttu-id="0bc3f-201">hello.cscfg 檔案中的 hello 診斷連接字串的優先順序高於 hello hello.wadcfgx 檔案中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-201">hello diagnostics connection string in hello .cscfg file takes precedence over hello storage account in hello .wadcfgx file.</span></span> <span data-ttu-id="0bc3f-202">如果診斷連接字串 hello.cscfg 檔案中指定然後 Visual Studio 會使用，並忽略.wadcfgx 中的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-202">If a diagnostics connection string is specified in hello .cscfg file, then Visual Studio uses that and ignores hello storage account in .wadcfgx.</span></span>

#### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a><span data-ttu-id="0bc3f-203">功能沒有 hello 「 更新開發儲存體連接字串...」</span><span class="sxs-lookup"><span data-stu-id="0bc3f-203">What does hello "Update development storage connection strings…"</span></span> <span data-ttu-id="0bc3f-204">作用為何？</span><span class="sxs-lookup"><span data-stu-id="0bc3f-204">checkbox do?</span></span>
<span data-ttu-id="0bc3f-205">hello 核取方塊**更新開發儲存體連接字串以供診斷和快取，使用 Microsoft Azure 儲存體帳戶認證發行 tooMicrosoft Azure 時**可讓您方便 tooupdate 任何開發儲存體帳戶連接字串與 hello 發行期間指定的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-205">hello checkbox for **Update development storage connection strings for Diagnostics and Caching with Microsoft Azure storage account credentials when publishing tooMicrosoft Azure** gives you a convenient way tooupdate any development storage account connection strings with hello Azure storage account specified during publishing.</span></span>

<span data-ttu-id="0bc3f-206">例如，假設您選取此核取方塊並 hello 診斷連接字串指定`UseDevelopmentStorage=true`。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-206">For example, suppose you select this checkbox and hello diagnostics connection string specifies `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="0bc3f-207">當您發行 hello 專案 tooAzure 時，Visual Studio 會自動更新 hello 診斷連接字串與 hello hello 發行精靈中指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-207">When you publish hello project tooAzure, Visual Studio will automatically update hello diagnostics connection string with hello storage account you specified in hello Publish wizard.</span></span> <span data-ttu-id="0bc3f-208">不過，如果實際的儲存體帳戶指定為 hello 診斷連接字串，然後該帳戶改用。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-208">However, if a real storage account was specified as hello diagnostics connection string, then that account is used instead.</span></span>

### <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a><span data-ttu-id="0bc3f-209">Azure SDK 2.4 及更舊版本和 Azure SDK 2.5 及更新版本之間的診斷功能差異</span><span class="sxs-lookup"><span data-stu-id="0bc3f-209">Diagnostics functionality differences between Azure SDK 2.4 and earlier and Azure SDK 2.5 and later</span></span>
<span data-ttu-id="0bc3f-210">如果您要升級您的專案，從 Azure SDK 2.4 tooAzure SDK 2.5 或更新版本，您應該謹記在心 hello 下列診斷功能差異。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-210">If you're upgrading your project from Azure SDK 2.4 tooAzure SDK 2.5 or later, you should bear in mind hello following diagnostics functionality differences.</span></span>

* <span data-ttu-id="0bc3f-211">**組態 API 已被取代** – 診斷的程式設計組態可在 Azure SDK 2.4 或更舊版本中使用，但在 Azure SDK 2.5 及更新版本中已被取代。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-211">**Configuration APIs are deprecated** – Programmatic configuration of diagnostics is available in Azure SDK 2.4 or earlier versions, but is deprecated in Azure SDK 2.5 and later.</span></span> <span data-ttu-id="0bc3f-212">如果您的診斷組態目前定義在程式碼中，您將需要 tooreconfigure 從頭診斷 tookeep 工作順序中的 hello 移轉專案中的這些設定。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-212">If your diagnostics configuration is currently defined in code, you'll need tooreconfigure those settings from scratch in hello migrated project in order for diagnostics tookeep working.</span></span> <span data-ttu-id="0bc3f-213">hello Azure SDK 2.4 的診斷組態檔是 diagnostics.wadcfg，是 diagnostics.wadcfgx Azure SDK 2.5 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-213">hello diagnostics configuration file for Azure SDK 2.4 is diagnostics.wadcfg, and diagnostics.wadcfgx for Azure SDK 2.5 and later.</span></span>
* <span data-ttu-id="0bc3f-214">**雲端服務應用程式的診斷功能只能在 hello 角色層級，不是在 hello 執行個體層級設定。**</span><span class="sxs-lookup"><span data-stu-id="0bc3f-214">**Diagnostics for cloud service applications can only be configured at hello role level, not at hello instance level.**</span></span>
* <span data-ttu-id="0bc3f-215">**每次您部署應用程式時，會更新 hello 診斷組態**– 如果您從 [伺服器總管] 中變更診斷組態，然後重新部署您的應用程式，這可能會造成同位檢查問題。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-215">**Every time you deploy your app, hello diagnostics configuration is updated** – This can cause parity issues if you change your diagnostics configuration from Server Explorer and then redeploy your app.</span></span>
* <span data-ttu-id="0bc3f-216">**在 Azure SDK 2.5 和更新版本，hello 診斷組態檔中，未在程式碼中設定損毀傾印**– 如果您有程式碼中設定損毀傾印，您就必須 toomanually 傳送嗨組態從程式碼 toohello 組態檔由於 hello 損毀傾印不傳送 hello 移轉 tooAzure SDK 2.6 期間。</span><span class="sxs-lookup"><span data-stu-id="0bc3f-216">**In Azure SDK 2.5 and later, crash dumps are configured in hello diagnostics configuration file, not in code** – If you have crash dumps configured in code, you'll have toomanually transfer hello configuration from code toohello configuration file, because hello crash dumps aren't transferred during hello migration tooAzure SDK 2.6.</span></span>

