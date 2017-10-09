---
title: "使用 Azure PowerShell 的 Azure Redis 快取 aaaManage |Microsoft 文件"
description: "深入了解如何使用 Azure PowerShell 的 Azure Redis cache tooperform 系統管理工作。"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a><span data-ttu-id="071c1-103">使用 Azure PowerShell 管理 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="071c1-103">Manage Azure Redis Cache with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="071c1-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="071c1-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="071c1-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="071c1-105">Azure CLI</span></span>](cache-manage-cli.md)
> 
> 

<span data-ttu-id="071c1-106">本主題說明您如何 tooperform 常見工作建立、 更新及如何調整您的 Azure Redis 快取執行個體，tooregenerate 存取金鑰，以及如何 tooview 您的快取的資訊。</span><span class="sxs-lookup"><span data-stu-id="071c1-106">This topic shows you how tooperform common tasks such as create, update, and scale your Azure Redis Cache instances, how tooregenerate access keys, and how tooview information about your caches.</span></span> <span data-ttu-id="071c1-107">如需 Azure Redis 快取的 PowerShell Cmdlet 完整清單，請參閱 [Azure Redis 快取的 Cmdlet](https://msdn.microsoft.com/library/azure/mt634513.aspx)。</span><span class="sxs-lookup"><span data-stu-id="071c1-107">For a complete list of Azure Redis Cache PowerShell cmdlets, see [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="071c1-108">如需 hello 傳統部署模型的詳細資訊，請參閱[Azure Resource Manager vs 傳統部署： 了解部署模型及 hello 資源的狀態](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics)。</span><span class="sxs-lookup"><span data-stu-id="071c1-108">For more information about hello classic deployment model, see [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="071c1-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="071c1-109">Prerequisites</span></span>
<span data-ttu-id="071c1-110">如果您已安裝 Azure PowerShell，其必須是 Azure PowerShell 1.0.0 或更新的版本。</span><span class="sxs-lookup"><span data-stu-id="071c1-110">If you have already installed Azure PowerShell, you must have Azure PowerShell version 1.0.0 or later.</span></span> <span data-ttu-id="071c1-111">您可以檢查您使用此命令在 hello Azure PowerShell 命令提示字元安裝的 Azure PowerShell hello 版本。</span><span class="sxs-lookup"><span data-stu-id="071c1-111">You can check hello version of Azure PowerShell that you have installed with this command at hello Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version


<span data-ttu-id="071c1-112">首先，您必須登入 tooAzure 與此命令。</span><span class="sxs-lookup"><span data-stu-id="071c1-112">First, you must log in tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="071c1-113">在 Microsoft Azure 登入的 hello 對話方塊中指定您的 Azure 帳戶並將其密碼的 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="071c1-113">Specify hello email address of your Azure account and its password in hello Microsoft Azure sign-in dialog.</span></span>

<span data-ttu-id="071c1-114">接下來，如果您有多個 Azure 訂用帳戶，您需要 tooset 您 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="071c1-114">Next, if you have multiple Azure subscriptions, you need tooset your Azure subscription.</span></span> <span data-ttu-id="071c1-115">toosee 一份您目前的訂用帳戶，執行此命令。</span><span class="sxs-lookup"><span data-stu-id="071c1-115">toosee a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="071c1-116">toospecify hello 訂用帳戶，執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="071c1-116">toospecify hello subscription, run hello following command.</span></span> <span data-ttu-id="071c1-117">在下列範例的 hello，hello 訂用帳戶名稱是`ContosoSubscription`。</span><span class="sxs-lookup"><span data-stu-id="071c1-117">In hello following example, hello subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

<span data-ttu-id="071c1-118">您可以使用 Windows PowerShell 的 Azure 資源管理員之前，您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="071c1-118">Before you can use Windows PowerShell with Azure Resource Manager, you need hello following:</span></span>

* <span data-ttu-id="071c1-119">Windows PowerShell 3.0 或 4.0 版本。</span><span class="sxs-lookup"><span data-stu-id="071c1-119">Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="071c1-120">toofind hello 版本的 Windows PowerShell，輸入：`$PSVersionTable`並確認 hello 值`PSVersion`3.0 或 4.0。</span><span class="sxs-lookup"><span data-stu-id="071c1-120">toofind hello version of Windows PowerShell, type:`$PSVersionTable` and verify hello value of `PSVersion` is 3.0 or 4.0.</span></span> <span data-ttu-id="071c1-121">tooinstall 相容的版本，請參閱[Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595)或[Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855)。</span><span class="sxs-lookup"><span data-stu-id="071c1-121">tooinstall a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="071c1-122">tooget 詳細說明您在此教學課程中，使用 hello Get-help 指令程式中看到任何 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="071c1-122">tooget detailed help for any cmdlet you see in this tutorial, use hello Get-Help cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="071c1-123">例如，tooget 說明 hello `New-AzureRmRedisCache` cmdlet，類型：</span><span class="sxs-lookup"><span data-stu-id="071c1-123">For example, tooget help for hello `New-AzureRmRedisCache` cmdlet, type:</span></span>

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a><span data-ttu-id="071c1-124">如何 tooconnect tooother 雲端</span><span class="sxs-lookup"><span data-stu-id="071c1-124">How tooconnect tooother clouds</span></span>
<span data-ttu-id="071c1-125">根據預設 hello Azure 環境是`AzureCloud`，它代表 hello 全域 Azure 的雲端執行個體。</span><span class="sxs-lookup"><span data-stu-id="071c1-125">By default hello Azure environment is `AzureCloud`, which represents hello global Azure cloud instance.</span></span> <span data-ttu-id="071c1-126">tooconnect tooa 不同的執行個體，使用 hello`Add-AzureRmAccount`命令與 hello`-Environment`或-`EnvironmentName` hello 所需的環境或環境名稱的命令列參數。</span><span class="sxs-lookup"><span data-stu-id="071c1-126">tooconnect tooa different instance, use hello `Add-AzureRmAccount` command with hello `-Environment` or -`EnvironmentName` command line switch with hello desired environment or environment name.</span></span>

<span data-ttu-id="071c1-127">可用的環境，執行 hello toosee hello 清單`Get-AzureRmEnvironment`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="071c1-127">toosee hello list of available environments, run hello `Get-AzureRmEnvironment` cmdlet.</span></span>

### <a name="tooconnect-toohello-azure-government-cloud"></a><span data-ttu-id="071c1-128">tooconnect toohello Azure 政府雲端</span><span class="sxs-lookup"><span data-stu-id="071c1-128">tooconnect toohello Azure Government Cloud</span></span>
<span data-ttu-id="071c1-129">tooconnect toohello Azure 政府雲端，使用其中一個 hello 下列命令。</span><span class="sxs-lookup"><span data-stu-id="071c1-129">tooconnect toohello Azure Government Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

<span data-ttu-id="071c1-130">或</span><span class="sxs-lookup"><span data-stu-id="071c1-130">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

<span data-ttu-id="071c1-131">toocreate hello Azure 政府雲端，使用其中一個 hello 下列位置中的快取。</span><span class="sxs-lookup"><span data-stu-id="071c1-131">toocreate a cache in hello Azure Government Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="071c1-132">美國政府維吉尼亞州</span><span class="sxs-lookup"><span data-stu-id="071c1-132">USGov Virginia</span></span>
* <span data-ttu-id="071c1-133">美國政府愛荷華州</span><span class="sxs-lookup"><span data-stu-id="071c1-133">USGov Iowa</span></span>

<span data-ttu-id="071c1-134">如需 hello Azure 政府雲端的詳細資訊，請參閱[Microsoft Azure 政府](https://azure.microsoft.com/features/gov/)和[Microsoft Azure 政府開發人員指南](../azure-government-developer-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="071c1-134">For more information about hello Azure Government Cloud, see [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) and [Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>

### <a name="tooconnect-toohello-azure-china-cloud"></a><span data-ttu-id="071c1-135">tooconnect toohello Azure 中國雲端</span><span class="sxs-lookup"><span data-stu-id="071c1-135">tooconnect toohello Azure China Cloud</span></span>
<span data-ttu-id="071c1-136">tooconnect toohello Azure 中國雲端，使用其中一個 hello 下列命令。</span><span class="sxs-lookup"><span data-stu-id="071c1-136">tooconnect toohello Azure China Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

<span data-ttu-id="071c1-137">或</span><span class="sxs-lookup"><span data-stu-id="071c1-137">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

<span data-ttu-id="071c1-138">toocreate hello Azure 中國雲端，使用其中一個 hello 下列位置中的快取。</span><span class="sxs-lookup"><span data-stu-id="071c1-138">toocreate a cache in hello Azure China Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="071c1-139">中國東部</span><span class="sxs-lookup"><span data-stu-id="071c1-139">China East</span></span>
* <span data-ttu-id="071c1-140">中國北部</span><span class="sxs-lookup"><span data-stu-id="071c1-140">China North</span></span>

<span data-ttu-id="071c1-141">如需 hello Azure 中國雲端的詳細資訊，請參閱[AzureChinaCloud azure 在中國的 21Vianet 所操作](http://www.windowsazure.cn/)。</span><span class="sxs-lookup"><span data-stu-id="071c1-141">For more information about hello Azure China Cloud, see [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span>

### <a name="tooconnect-toomicrosoft-azure-germany"></a><span data-ttu-id="071c1-142">tooconnect tooMicrosoft Azure 德國</span><span class="sxs-lookup"><span data-stu-id="071c1-142">tooconnect tooMicrosoft Azure Germany</span></span>
<span data-ttu-id="071c1-143">tooconnect tooMicrosoft Azure 德國，使用其中一個 hello 下列命令。</span><span class="sxs-lookup"><span data-stu-id="071c1-143">tooconnect tooMicrosoft Azure Germany, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


<span data-ttu-id="071c1-144">或</span><span class="sxs-lookup"><span data-stu-id="071c1-144">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

<span data-ttu-id="071c1-145">toocreate Microsoft Azure 德國，使用其中一個 hello 下列位置中的快取。</span><span class="sxs-lookup"><span data-stu-id="071c1-145">toocreate a cache in Microsoft Azure Germany, use one of hello following locations.</span></span>

* <span data-ttu-id="071c1-146">德國中部</span><span class="sxs-lookup"><span data-stu-id="071c1-146">Germany Central</span></span>
* <span data-ttu-id="071c1-147">德國東北部</span><span class="sxs-lookup"><span data-stu-id="071c1-147">Germany Northeast</span></span>

<span data-ttu-id="071c1-148">如需有關 Microsoft Azure (德國) 的詳細資訊，請參閱 [Microsoft Azure (德國)](https://azure.microsoft.com/overview/clouds/germany/)。</span><span class="sxs-lookup"><span data-stu-id="071c1-148">For more information about Microsoft Azure Germany, see [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span></span>

### <a name="properties-used-for-azure-redis-cache-powershell"></a><span data-ttu-id="071c1-149">用於 Azure Redis 快取 PowerShell 的屬性</span><span class="sxs-lookup"><span data-stu-id="071c1-149">Properties used for Azure Redis Cache PowerShell</span></span>
<span data-ttu-id="071c1-150">下表中的 hello 包含屬性和描述常用的參數時建立和管理您使用 Azure PowerShell 的 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="071c1-150">hello following table contains properties and descriptions for commonly used parameters when creating and managing your Azure Redis Cache instances using Azure PowerShell.</span></span>

| <span data-ttu-id="071c1-151">參數</span><span class="sxs-lookup"><span data-stu-id="071c1-151">Parameter</span></span> | <span data-ttu-id="071c1-152">說明</span><span class="sxs-lookup"><span data-stu-id="071c1-152">Description</span></span> | <span data-ttu-id="071c1-153">預設值</span><span class="sxs-lookup"><span data-stu-id="071c1-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="071c1-154">名稱</span><span class="sxs-lookup"><span data-stu-id="071c1-154">Name</span></span> |<span data-ttu-id="071c1-155">Hello 快取的名稱</span><span class="sxs-lookup"><span data-stu-id="071c1-155">Name of hello cache</span></span> | |
| <span data-ttu-id="071c1-156">位置</span><span class="sxs-lookup"><span data-stu-id="071c1-156">Location</span></span> |<span data-ttu-id="071c1-157">Hello 快取的位置</span><span class="sxs-lookup"><span data-stu-id="071c1-157">Location of hello cache</span></span> | |
| <span data-ttu-id="071c1-158">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="071c1-158">ResourceGroupName</span></span> |<span data-ttu-id="071c1-159">哪些 toocreate hello 快取中的資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="071c1-159">Resource group name in which toocreate hello cache</span></span> | |
| <span data-ttu-id="071c1-160">大小</span><span class="sxs-lookup"><span data-stu-id="071c1-160">Size</span></span> |<span data-ttu-id="071c1-161">hello hello 快取大小。</span><span class="sxs-lookup"><span data-stu-id="071c1-161">hello size of hello cache.</span></span> <span data-ttu-id="071c1-162">有效值為：P1、P2、P3、P4、C0、C1、C2、C3、C4、C5、C6、250MB、1GB、2.5GB、6GB、13GB、26GB、53GB</span><span class="sxs-lookup"><span data-stu-id="071c1-162">Valid values are: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span></span> |<span data-ttu-id="071c1-163">1GB</span><span class="sxs-lookup"><span data-stu-id="071c1-163">1GB</span></span> |
| <span data-ttu-id="071c1-164">ShardCount</span><span class="sxs-lookup"><span data-stu-id="071c1-164">ShardCount</span></span> |<span data-ttu-id="071c1-165">hello 分區 toocreate 使用啟用叢集建立進階版快取時數。</span><span class="sxs-lookup"><span data-stu-id="071c1-165">hello number of shards toocreate when creating a premium cache with clustering enabled.</span></span> <span data-ttu-id="071c1-166">有效值為：1、2、3、4、5、6、7、8、9、10</span><span class="sxs-lookup"><span data-stu-id="071c1-166">Valid values are: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></span> | |
| <span data-ttu-id="071c1-167">SKU</span><span class="sxs-lookup"><span data-stu-id="071c1-167">SKU</span></span> |<span data-ttu-id="071c1-168">指定 hello hello 快取的 SKU。</span><span class="sxs-lookup"><span data-stu-id="071c1-168">Specifies hello SKU of hello cache.</span></span> <span data-ttu-id="071c1-169">有效值為：Basic、Standard、Premium</span><span class="sxs-lookup"><span data-stu-id="071c1-169">Valid values are: Basic, Standard, Premium</span></span> |<span data-ttu-id="071c1-170">標準</span><span class="sxs-lookup"><span data-stu-id="071c1-170">Standard</span></span> |
| <span data-ttu-id="071c1-171">RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="071c1-171">RedisConfiguration</span></span> |<span data-ttu-id="071c1-172">指定 Redis 組態設定。</span><span class="sxs-lookup"><span data-stu-id="071c1-172">Specifies Redis configuration settings.</span></span> <span data-ttu-id="071c1-173">如需每個設定的詳細資訊，請參閱下列資訊 hello [RedisConfiguration 屬性](#redisconfiguration-properties)資料表。</span><span class="sxs-lookup"><span data-stu-id="071c1-173">For details on each setting, see hello following [RedisConfiguration properties](#redisconfiguration-properties) table.</span></span> | |
| <span data-ttu-id="071c1-174">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="071c1-174">EnableNonSslPort</span></span> |<span data-ttu-id="071c1-175">指出是否已啟用 hello 非 SSL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="071c1-175">Indicates whether hello non-SSL port is enabled.</span></span> |<span data-ttu-id="071c1-176">False</span><span class="sxs-lookup"><span data-stu-id="071c1-176">False</span></span> |
| <span data-ttu-id="071c1-177">MaxMemoryPolicy</span><span class="sxs-lookup"><span data-stu-id="071c1-177">MaxMemoryPolicy</span></span> |<span data-ttu-id="071c1-178">這個參數已被取代，請改用 RedisConfiguration。</span><span class="sxs-lookup"><span data-stu-id="071c1-178">This parameter has been deprecated - use RedisConfiguration instead.</span></span> | |
| <span data-ttu-id="071c1-179">StaticIP</span><span class="sxs-lookup"><span data-stu-id="071c1-179">StaticIP</span></span> |<span data-ttu-id="071c1-180">當裝載您的快取在 VNET 中，指定唯一的 IP 位址 hello 快取的 hello 子網路中。</span><span class="sxs-lookup"><span data-stu-id="071c1-180">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="071c1-181">如果未提供，其中一個會為您選擇從 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="071c1-181">If not provided, one is chosen for you from hello subnet.</span></span> | |
| <span data-ttu-id="071c1-182">子網路</span><span class="sxs-lookup"><span data-stu-id="071c1-182">Subnet</span></span> |<span data-ttu-id="071c1-183">裝載您的快取在 VNET 中，指定哪些 toodeploy hello 快取以 hello hello 子網路名稱。</span><span class="sxs-lookup"><span data-stu-id="071c1-183">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="071c1-184">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="071c1-184">VirtualNetwork</span></span> |<span data-ttu-id="071c1-185">當裝載您的 VNET 中的快取指定的資源識別碼 hello hello 哪些 toodeploy hello 快取中的 VNET。</span><span class="sxs-lookup"><span data-stu-id="071c1-185">When hosting your cache in a VNET, specifies hello resource ID of hello VNET in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="071c1-186">KeyType</span><span class="sxs-lookup"><span data-stu-id="071c1-186">KeyType</span></span> |<span data-ttu-id="071c1-187">指定的便捷鍵 tooregenerate 更新存取金鑰時。</span><span class="sxs-lookup"><span data-stu-id="071c1-187">Specifies which access key tooregenerate when renewing access keys.</span></span> <span data-ttu-id="071c1-188">有效值為：Primary、Secondary</span><span class="sxs-lookup"><span data-stu-id="071c1-188">Valid values are: Primary, Secondary</span></span> | |

### <a name="redisconfiguration-properties"></a><span data-ttu-id="071c1-189">RedisConfiguration 屬性</span><span class="sxs-lookup"><span data-stu-id="071c1-189">RedisConfiguration properties</span></span>
| <span data-ttu-id="071c1-190">屬性</span><span class="sxs-lookup"><span data-stu-id="071c1-190">Property</span></span> | <span data-ttu-id="071c1-191">說明</span><span class="sxs-lookup"><span data-stu-id="071c1-191">Description</span></span> | <span data-ttu-id="071c1-192">定價層</span><span class="sxs-lookup"><span data-stu-id="071c1-192">Pricing tiers</span></span> |
| --- | --- | --- |
| <span data-ttu-id="071c1-193">rdb-backup-enabled</span><span class="sxs-lookup"><span data-stu-id="071c1-193">rdb-backup-enabled</span></span> |<span data-ttu-id="071c1-194">是否已啟用 [Redis 資料持續性](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="071c1-194">Whether [Redis data persistence](cache-how-to-premium-persistence.md) is enabled</span></span> |<span data-ttu-id="071c1-195">僅限進階版</span><span class="sxs-lookup"><span data-stu-id="071c1-195">Premium only</span></span> |
| <span data-ttu-id="071c1-196">rdb-storage-connection-string</span><span class="sxs-lookup"><span data-stu-id="071c1-196">rdb-storage-connection-string</span></span> |<span data-ttu-id="071c1-197">hello 連接字串 toohello 儲存體帳戶[Redis 資料持續性](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="071c1-197">hello connection string toohello storage account for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="071c1-198">僅限進階版</span><span class="sxs-lookup"><span data-stu-id="071c1-198">Premium only</span></span> |
| <span data-ttu-id="071c1-199">rdb-backup-frequency</span><span class="sxs-lookup"><span data-stu-id="071c1-199">rdb-backup-frequency</span></span> |<span data-ttu-id="071c1-200">hello 備份頻率[Redis 資料持續性](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="071c1-200">hello backup frequency for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="071c1-201">僅限進階版</span><span class="sxs-lookup"><span data-stu-id="071c1-201">Premium only</span></span> |
| <span data-ttu-id="071c1-202">maxmemory-reserved</span><span class="sxs-lookup"><span data-stu-id="071c1-202">maxmemory-reserved</span></span> |<span data-ttu-id="071c1-203">設定 hello[保留記憶體](cache-configure.md#maxmemory-policy-and-maxmemory-reserved)非快取的處理程序</span><span class="sxs-lookup"><span data-stu-id="071c1-203">Configures hello [memory reserved](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for non-cache processes</span></span> |<span data-ttu-id="071c1-204">標準和進階</span><span class="sxs-lookup"><span data-stu-id="071c1-204">Standard and Premium</span></span> |
| <span data-ttu-id="071c1-205">maxmemory-policy</span><span class="sxs-lookup"><span data-stu-id="071c1-205">maxmemory-policy</span></span> |<span data-ttu-id="071c1-206">設定 hello[收回原則](cache-configure.md#maxmemory-policy-and-maxmemory-reserved)hello 快取</span><span class="sxs-lookup"><span data-stu-id="071c1-206">Configures hello [eviction policy](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for hello cache</span></span> |<span data-ttu-id="071c1-207">所有定價層</span><span class="sxs-lookup"><span data-stu-id="071c1-207">All pricing tiers</span></span> |
| <span data-ttu-id="071c1-208">notify-keyspace-events</span><span class="sxs-lookup"><span data-stu-id="071c1-208">notify-keyspace-events</span></span> |<span data-ttu-id="071c1-209">設定 [Keyspace 通知](cache-configure.md#keyspace-notifications-advanced-settings)</span><span class="sxs-lookup"><span data-stu-id="071c1-209">Configures [keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings)</span></span> |<span data-ttu-id="071c1-210">標準和進階</span><span class="sxs-lookup"><span data-stu-id="071c1-210">Standard and Premium</span></span> |
| <span data-ttu-id="071c1-211">hash-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="071c1-211">hash-max-ziplist-entries</span></span> |<span data-ttu-id="071c1-212">設定小型彙總資料類型的 [記憶體最佳化](http://redis.io/topics/memory-optimization)</span><span class="sxs-lookup"><span data-stu-id="071c1-212">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="071c1-213">標準和進階</span><span class="sxs-lookup"><span data-stu-id="071c1-213">Standard and Premium</span></span> |
| <span data-ttu-id="071c1-214">hash-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="071c1-214">hash-max-ziplist-value</span></span> |<span data-ttu-id="071c1-215">設定小型彙總資料類型的 [記憶體最佳化](http://redis.io/topics/memory-optimization)</span><span class="sxs-lookup"><span data-stu-id="071c1-215">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="071c1-216">標準和進階</span><span class="sxs-lookup"><span data-stu-id="071c1-216">Standard and Premium</span></span> |
| <span data-ttu-id="071c1-217">set-max-intset-entries</span><span class="sxs-lookup"><span data-stu-id="071c1-217">set-max-intset-entries</span></span> |<span data-ttu-id="071c1-218">設定小型彙總資料類型的 [記憶體最佳化](http://redis.io/topics/memory-optimization)</span><span class="sxs-lookup"><span data-stu-id="071c1-218">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="071c1-219">標準和進階</span><span class="sxs-lookup"><span data-stu-id="071c1-219">Standard and Premium</span></span> |
| <span data-ttu-id="071c1-220">zset-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="071c1-220">zset-max-ziplist-entries</span></span> |<span data-ttu-id="071c1-221">設定小型彙總資料類型的 [記憶體最佳化](http://redis.io/topics/memory-optimization)</span><span class="sxs-lookup"><span data-stu-id="071c1-221">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="071c1-222">標準和進階</span><span class="sxs-lookup"><span data-stu-id="071c1-222">Standard and Premium</span></span> |
| <span data-ttu-id="071c1-223">zset-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="071c1-223">zset-max-ziplist-value</span></span> |<span data-ttu-id="071c1-224">設定小型彙總資料類型的 [記憶體最佳化](http://redis.io/topics/memory-optimization)</span><span class="sxs-lookup"><span data-stu-id="071c1-224">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="071c1-225">標準和進階</span><span class="sxs-lookup"><span data-stu-id="071c1-225">Standard and Premium</span></span> |
| <span data-ttu-id="071c1-226">資料庫</span><span class="sxs-lookup"><span data-stu-id="071c1-226">databases</span></span> |<span data-ttu-id="071c1-227">設定資料庫的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="071c1-227">Configures hello number of databases.</span></span> <span data-ttu-id="071c1-228">這個屬性僅可以在建立快取時設定。</span><span class="sxs-lookup"><span data-stu-id="071c1-228">This property can be configured only at cache creation.</span></span> |<span data-ttu-id="071c1-229">標準和進階</span><span class="sxs-lookup"><span data-stu-id="071c1-229">Standard and Premium</span></span> |

## <a name="toocreate-a-redis-cache"></a><span data-ttu-id="071c1-230">toocreate Redis 快取</span><span class="sxs-lookup"><span data-stu-id="071c1-230">toocreate a Redis Cache</span></span>
<span data-ttu-id="071c1-231">建立新的 Azure Redis 快取執行個體使用 hello[新增 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="071c1-231">New Azure Redis Cache instances are created using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="071c1-232">hello 第一次您使用 hello Azure 入口網站的訂用帳戶中建立 Redis 快取 hello 入口網站註冊 hello`Microsoft.Cache`該訂用帳戶的命名空間。</span><span class="sxs-lookup"><span data-stu-id="071c1-232">hello first time you create a Redis cache in a subscription using hello Azure portal, hello portal registers hello `Microsoft.Cache` namespace for that subscription.</span></span> <span data-ttu-id="071c1-233">如果您嘗試 toocreate hello 先 Redis 快取中使用 PowerShell 的訂用帳戶，您必須先註冊使用下列命令; hello 該命名空間否則指令程式，例如`New-AzureRmRedisCache`和`Get-AzureRmRedisCache`失敗。</span><span class="sxs-lookup"><span data-stu-id="071c1-233">If you attempt toocreate hello first Redis cache in a subscription using PowerShell, you must first register that namespace using hello following command; otherwise cmdlets such as `New-AzureRmRedisCache` and `Get-AzureRmRedisCache` fail.</span></span>
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

<span data-ttu-id="071c1-234">一份可用的參數及描述 toosee `New-AzureRmRedisCache`，請執行 hello 下列命令。</span><span class="sxs-lookup"><span data-stu-id="071c1-234">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="071c1-235">toocreate 預設參數，執行下列命令的 hello 與快取。</span><span class="sxs-lookup"><span data-stu-id="071c1-235">toocreate a cache with default parameters, run hello following command.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

<span data-ttu-id="071c1-236">`ResourceGroupName``Name`，和`Location`是必要的參數，但 hello 其餘部分是選擇性的而且有預設值。</span><span class="sxs-lookup"><span data-stu-id="071c1-236">`ResourceGroupName`, `Name`, and `Location` are required parameters, but hello rest are optional and have default values.</span></span> <span data-ttu-id="071c1-237">執行 hello 前一個命令建立的標準 SKU Azure Redis 快取執行個體與 hello 指定的名稱、 位置和資源群組與 hello 非 SSL 連接埠停用的大小為 1GB。</span><span class="sxs-lookup"><span data-stu-id="071c1-237">Running hello previous command creates a Standard SKU Azure Redis Cache instance with hello specified name, location, and resource group, that is 1 GB in size with hello non-SSL port disabled.</span></span>

<span data-ttu-id="071c1-238">toocreate 進階版快取中，指定大小為 P1 (6 GB-60 GB)，P2 (13 GB-130 GB)，P3 (26 GB-260 GB) 或 P4 (53 GB-530 GB)。</span><span class="sxs-lookup"><span data-stu-id="071c1-238">toocreate a premium cache, specify a size of P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), or P4 (53 GB - 530 GB).</span></span> <span data-ttu-id="071c1-239">tooenable 叢集中，指定使用 hello 分區計數`ShardCount`參數。</span><span class="sxs-lookup"><span data-stu-id="071c1-239">tooenable clustering, specify a shard count using hello `ShardCount` parameter.</span></span> <span data-ttu-id="071c1-240">hello 下列範例會建立 P1 進階版快取 3 分區。</span><span class="sxs-lookup"><span data-stu-id="071c1-240">hello following example creates a P1 premium cache with 3 shards.</span></span> <span data-ttu-id="071c1-241">P1 進階版快取大小，為 6 GB，因為我們指定三個分區 hello 大小總計為 18 GB (3 x 6 GB)。</span><span class="sxs-lookup"><span data-stu-id="071c1-241">A P1 premium cache is 6 GB in size, and since we specified three shards hello total size is 18 GB (3 x 6 GB).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

<span data-ttu-id="071c1-242">hello toospecify 值`RedisConfiguration`參數時，括住內部 hello 值`{}`做為索引鍵/值組喜歡`@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`。</span><span class="sxs-lookup"><span data-stu-id="071c1-242">toospecify values for hello `RedisConfiguration` parameter, enclose hello values inside `{}` as key/value pairs like `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span></span> <span data-ttu-id="071c1-243">hello 下列範例會建立具有標準 1 GB 快取`allkeys-random`maxmemory 原則和 keyspace 通知設有`KEA`。</span><span class="sxs-lookup"><span data-stu-id="071c1-243">hello following example creates a standard 1 GB cache with `allkeys-random` maxmemory policy and keyspace notifications configured with `KEA`.</span></span> <span data-ttu-id="071c1-244">如需詳細資訊，請參閱 [Keyspace 通知 (進階設定)](cache-configure.md#keyspace-notifications-advanced-settings) 和[記憶體原則](cache-configure.md#memory-policies)。</span><span class="sxs-lookup"><span data-stu-id="071c1-244">For more information, see [Keyspace notifications (advanced settings)](cache-configure.md#keyspace-notifications-advanced-settings) and [Memory policies](cache-configure.md#memory-policies).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a><span data-ttu-id="071c1-245">設定快取建立期間 tooconfigure hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="071c1-245">tooconfigure hello databases setting during cache creation</span></span>
<span data-ttu-id="071c1-246">hello`databases`可以設定只有在快取建立期間設定。</span><span class="sxs-lookup"><span data-stu-id="071c1-246">hello `databases` setting can be configured only during cache creation.</span></span> <span data-ttu-id="071c1-247">hello 下列範例會建立高階 P3 48 資料庫時使用 hello (26 GB) 快取[新增 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="071c1-247">hello following example creates a premium P3 (26 GB) cache with 48 databases using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

<span data-ttu-id="071c1-248">如需有關 hello`databases`屬性，請參閱[預設 Azure Redis 快取伺服器組態](cache-configure.md#default-redis-server-configuration)。</span><span class="sxs-lookup"><span data-stu-id="071c1-248">For more information on hello `databases` property, see [Default Azure Redis Cache server configuration](cache-configure.md#default-redis-server-configuration).</span></span> <span data-ttu-id="071c1-249">如需有關建立快取使用 hello[新增 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx)指令程式，請參閱先前的 hello [toocreate Redis 快取](#to-create-a-redis-cache)> 一節。</span><span class="sxs-lookup"><span data-stu-id="071c1-249">For more information on creating a cache using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, see hello previous [toocreate a Redis Cache](#to-create-a-redis-cache) section.</span></span>

## <a name="tooupdate-a-redis-cache"></a><span data-ttu-id="071c1-250">tooupdate Redis 快取</span><span class="sxs-lookup"><span data-stu-id="071c1-250">tooupdate a Redis cache</span></span>
<span data-ttu-id="071c1-251">Azure Redis 快取執行個體都會更新使用 hello[組 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="071c1-251">Azure Redis Cache instances are updated using hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span></span>

<span data-ttu-id="071c1-252">一份可用的參數及描述 toosee `Set-AzureRmRedisCache`，請執行 hello 下列命令。</span><span class="sxs-lookup"><span data-stu-id="071c1-252">toosee a list of available parameters and their descriptions for `Set-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="071c1-253">hello`Set-AzureRmRedisCache`指令程式可以使用的 tooupdate 屬性，例如`Size`， `Sku`， `EnableNonSslPort`，和 hello`RedisConfiguration`值。</span><span class="sxs-lookup"><span data-stu-id="071c1-253">hello `Set-AzureRmRedisCache` cmdlet can be used tooupdate properties such as `Size`, `Sku`, `EnableNonSslPort`, and hello `RedisConfiguration` values.</span></span> 

<span data-ttu-id="071c1-254">hello 下列的命令更新 hello hello Redis 快取 maxmemory 原則命名 myCache。</span><span class="sxs-lookup"><span data-stu-id="071c1-254">hello following command updates hello maxmemory-policy for hello Redis Cache named myCache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a><span data-ttu-id="071c1-255">tooscale Redis 快取</span><span class="sxs-lookup"><span data-stu-id="071c1-255">tooscale a Redis cache</span></span>
<span data-ttu-id="071c1-256">`Set-AzureRmRedisCache`可以是使用的 tooscale Azure Redis 快取執行個體時 hello `Size`， `Sku`，或`ShardCount`修改屬性。</span><span class="sxs-lookup"><span data-stu-id="071c1-256">`Set-AzureRmRedisCache` can be used tooscale an Azure Redis cache instance when hello `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> 

> [!NOTE]
> <span data-ttu-id="071c1-257">調整快取使用 PowerShell 是主體 toohello 相同的限制和指導方針調整快取從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="071c1-257">Scaling a cache using PowerShell is subject toohello same limits and guidelines as scaling a cache from hello Azure portal.</span></span> <span data-ttu-id="071c1-258">您可以調整 tooa 不同定價層與 hello 下列限制。</span><span class="sxs-lookup"><span data-stu-id="071c1-258">You can scale tooa different pricing tier with hello following restrictions.</span></span>
> 
> * <span data-ttu-id="071c1-259">您無法調整從較高定價層 tooa 較低的定價層。</span><span class="sxs-lookup"><span data-stu-id="071c1-259">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
> * <span data-ttu-id="071c1-260">您無法從延展**Premium**快取下 tooa**標準**或**基本**快取。</span><span class="sxs-lookup"><span data-stu-id="071c1-260">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
> * <span data-ttu-id="071c1-261">您無法從延展**標準**快取下 tooa**基本**快取。</span><span class="sxs-lookup"><span data-stu-id="071c1-261">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
> * <span data-ttu-id="071c1-262">您可以調整從**基本**快取 tooa**標準**快取，但是您無法變更在 hello hello 大小相同的時間。</span><span class="sxs-lookup"><span data-stu-id="071c1-262">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="071c1-263">如果您需要不同的大小，您可以執行後續的縮放作業 toohello 預期大小。</span><span class="sxs-lookup"><span data-stu-id="071c1-263">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
> * <span data-ttu-id="071c1-264">您無法從延展**基本**快取直接 tooa **Premium**快取。</span><span class="sxs-lookup"><span data-stu-id="071c1-264">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="071c1-265">您必須從延展**基本**太**標準**一個縮放作業，然後從**標準**太**Premium**中後續的縮放比例作業。</span><span class="sxs-lookup"><span data-stu-id="071c1-265">You must scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
> * <span data-ttu-id="071c1-266">您無法從較大的向下 toohello 延展**C0 250 MB**大小。</span><span class="sxs-lookup"><span data-stu-id="071c1-266">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>
> 
> <span data-ttu-id="071c1-267">如需詳細資訊，請參閱[如何 tooScale Azure Redis 快取](cache-how-to-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="071c1-267">For more information, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>
> 
> 

<span data-ttu-id="071c1-268">hello 下列範例示範如何 tooscale 快取命名`myCache`tooa 2.5 GB 的快取。</span><span class="sxs-lookup"><span data-stu-id="071c1-268">hello following example shows how tooscale a cache named `myCache` tooa 2.5 GB cache.</span></span> <span data-ttu-id="071c1-269">請注意，此命令可用於基本或標準快取。</span><span class="sxs-lookup"><span data-stu-id="071c1-269">Note that this command works for both a Basic or a Standard cache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="071c1-270">發出此命令之後，會傳回 hello 快取的 hello 狀態 (類似 toocalling `Get-AzureRmRedisCache`)。</span><span class="sxs-lookup"><span data-stu-id="071c1-270">After this command is issued, hello status of hello cache is returned (similar toocalling `Get-AzureRmRedisCache`).</span></span> <span data-ttu-id="071c1-271">請注意該 hello`ProvisioningState`是`Scaling`。</span><span class="sxs-lookup"><span data-stu-id="071c1-271">Note that hello `ProvisioningState` is `Scaling`.</span></span>

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

<span data-ttu-id="071c1-272">Hello 調整大小作業完成時，hello`ProvisioningState`變更太`Succeeded`。</span><span class="sxs-lookup"><span data-stu-id="071c1-272">When hello scaling operation is complete, hello `ProvisioningState` changes too`Succeeded`.</span></span> <span data-ttu-id="071c1-273">如果您需要 toomake 後續的縮放作業，例如從基本 tooStandard 變更，然後變更 hello 大小，您必須等到 hello 先前作業已完成，或您收到類似 toohello 下列錯誤。</span><span class="sxs-lookup"><span data-stu-id="071c1-273">If you need toomake a subsequent scaling operation, such as changing from Basic tooStandard and then changing hello size, you must wait until hello previous operation is complete or you receive an error similar toohello following.</span></span>

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a><span data-ttu-id="071c1-274">tooget Redis 快取資訊</span><span class="sxs-lookup"><span data-stu-id="071c1-274">tooget information about a Redis cache</span></span>
<span data-ttu-id="071c1-275">您可以擷取有關資訊快取使用 hello [Get AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="071c1-275">You can retrieve information about a cache using hello [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span></span>

<span data-ttu-id="071c1-276">一份可用的參數及描述 toosee `Get-AzureRmRedisCache`，請執行 hello 下列命令。</span><span class="sxs-lookup"><span data-stu-id="071c1-276">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="071c1-277">tooreturn hello 目前訂用帳戶，所有快取的資訊執行`Get-AzureRmRedisCache`不含任何參數。</span><span class="sxs-lookup"><span data-stu-id="071c1-277">tooreturn information about all caches in hello current subscription, run `Get-AzureRmRedisCache` without any parameters.</span></span>

    Get-AzureRmRedisCache

<span data-ttu-id="071c1-278">在特定的資源群組中，所有快取的 tooreturn 資訊執行`Get-AzureRmRedisCache`以 hello`ResourceGroupName`參數。</span><span class="sxs-lookup"><span data-stu-id="071c1-278">tooreturn information about all caches in a specific resource group, run `Get-AzureRmRedisCache` with hello `ResourceGroupName` parameter.</span></span>

    Get-AzureRmRedisCache -ResourceGroupName myGroup

<span data-ttu-id="071c1-279">tooreturn 資訊特定的快取中，執行`Get-AzureRmRedisCache`以 hello`Name`參數包含 hello 名稱 hello 快取及 hello`ResourceGroupName`與包含該快取的 hello 資源群組的參數。</span><span class="sxs-lookup"><span data-stu-id="071c1-279">tooreturn information about a specific cache, run `Get-AzureRmRedisCache` with hello `Name` parameter containing hello name of hello cache, and hello `ResourceGroupName` parameter with hello resource group containing that cache.</span></span>

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a><span data-ttu-id="071c1-280">Redis 快取的 tooretrieve hello 便捷鍵</span><span class="sxs-lookup"><span data-stu-id="071c1-280">tooretrieve hello access keys for a Redis cache</span></span>
<span data-ttu-id="071c1-281">tooretrieve hello 快取的存取金鑰，您可以使用 hello [Get AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="071c1-281">tooretrieve hello access keys for your cache, you can use hello [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span></span>

<span data-ttu-id="071c1-282">一份可用的參數及描述 toosee `Get-AzureRmRedisCacheKey`，請執行 hello 下列命令。</span><span class="sxs-lookup"><span data-stu-id="071c1-282">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="071c1-283">金鑰快取，呼叫 hello tooretrieve hello `Get-AzureRmRedisCacheKey` cmdlet 並快取的 hello 名稱傳入 hello hello 包含 hello 快取的資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="071c1-283">tooretrieve hello keys for your cache, call hello `Get-AzureRmRedisCacheKey` cmdlet and pass in hello name of your cache hello name of hello resource group that contains hello cache.</span></span>

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a><span data-ttu-id="071c1-284">tooregenerate Redis 快取的存取金鑰</span><span class="sxs-lookup"><span data-stu-id="071c1-284">tooregenerate access keys for your Redis cache</span></span>
<span data-ttu-id="071c1-285">tooregenerate hello 快取的存取金鑰，您可以使用 hello[新增 AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="071c1-285">tooregenerate hello access keys for your cache, you can use hello [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span></span>

<span data-ttu-id="071c1-286">一份可用的參數及描述 toosee `New-AzureRmRedisCacheKey`，請執行 hello 下列命令。</span><span class="sxs-lookup"><span data-stu-id="071c1-286">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="071c1-287">tooregenerate hello 主要或次要金鑰為快取，呼叫 hello `New-AzureRmRedisCacheKey` cmdlet，並傳入 hello 名稱、 資源群組，並指定`Primary`或`Secondary`hello`KeyType`參數。</span><span class="sxs-lookup"><span data-stu-id="071c1-287">tooregenerate hello primary or secondary key for your cache, call hello `New-AzureRmRedisCacheKey` cmdlet and pass in hello name, resource group, and specify either `Primary` or `Secondary` for hello `KeyType` parameter.</span></span> <span data-ttu-id="071c1-288">在下列範例的 hello，重新產生快取的 hello 次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="071c1-288">In hello following example, hello secondary access key for a cache is regenerated.</span></span>

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a><span data-ttu-id="071c1-289">toodelete Redis 快取</span><span class="sxs-lookup"><span data-stu-id="071c1-289">toodelete a Redis cache</span></span>
<span data-ttu-id="071c1-290">toodelete Redis 快取中，使用 hello[移除 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="071c1-290">toodelete a Redis cache, use hello [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span></span>

<span data-ttu-id="071c1-291">一份可用的參數及描述 toosee `Remove-AzureRmRedisCache`，請執行 hello 下列命令。</span><span class="sxs-lookup"><span data-stu-id="071c1-291">toosee a list of available parameters and their descriptions for `Remove-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="071c1-292">在下列範例的 hello，hello 具名快取`myCache`已移除。</span><span class="sxs-lookup"><span data-stu-id="071c1-292">In hello following example, hello cache named `myCache` is removed.</span></span>

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a><span data-ttu-id="071c1-293">tooimport Redis 快取</span><span class="sxs-lookup"><span data-stu-id="071c1-293">tooimport a Redis cache</span></span>
<span data-ttu-id="071c1-294">您可以將資料匯入 Azure Redis 快取執行個體使用 hello `Import-AzureRmRedisCache` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="071c1-294">You can import data into an Azure Redis Cache instance using hello `Import-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="071c1-295">匯入/匯出僅供 [進階層](cache-premium-tier-intro.md) 快取使用。</span><span class="sxs-lookup"><span data-stu-id="071c1-295">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="071c1-296">如需匯入/匯出的詳細資訊，請參閱 [在 Azure Redis 快取中匯入與匯出資料](cache-how-to-import-export-data.md)。</span><span class="sxs-lookup"><span data-stu-id="071c1-296">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="071c1-297">一份可用的參數及描述 toosee `Import-AzureRmRedisCache`，請執行 hello 下列命令。</span><span class="sxs-lookup"><span data-stu-id="071c1-297">toosee a list of available parameters and their descriptions for `Import-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="071c1-298">hello 下列命令從匯入資料至 Azure Redis 快取 hello SAS uri 所指定的 hello blob。</span><span class="sxs-lookup"><span data-stu-id="071c1-298">hello following command imports data from hello blob specified by hello SAS uri into Azure Redis Cache.</span></span>

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a><span data-ttu-id="071c1-299">tooexport Redis 快取</span><span class="sxs-lookup"><span data-stu-id="071c1-299">tooexport a Redis cache</span></span>
<span data-ttu-id="071c1-300">您可以從使用 hello Azure Redis 快取執行個體匯出資料`Export-AzureRmRedisCache`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="071c1-300">You can export data from an Azure Redis Cache instance using hello `Export-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="071c1-301">匯入/匯出僅供 [進階層](cache-premium-tier-intro.md) 快取使用。</span><span class="sxs-lookup"><span data-stu-id="071c1-301">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="071c1-302">如需匯入/匯出的詳細資訊，請參閱 [在 Azure Redis 快取中匯入與匯出資料](cache-how-to-import-export-data.md)。</span><span class="sxs-lookup"><span data-stu-id="071c1-302">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="071c1-303">一份可用的參數及描述 toosee `Export-AzureRmRedisCache`，請執行 hello 下列命令。</span><span class="sxs-lookup"><span data-stu-id="071c1-303">toosee a list of available parameters and their descriptions for `Export-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="071c1-304">hello 下列命令將資料匯出到 hello SAS uri 所指定的 hello 容器 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="071c1-304">hello following command exports data from an Azure Redis Cache instance into hello container specified by hello SAS uri.</span></span>

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a><span data-ttu-id="071c1-305">tooreboot Redis 快取</span><span class="sxs-lookup"><span data-stu-id="071c1-305">tooreboot a Redis cache</span></span>
<span data-ttu-id="071c1-306">您可以重新啟動您的 Azure Redis 快取執行個體使用 hello `Reset-AzureRmRedisCache` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="071c1-306">You can reboot your Azure Redis Cache instance using hello `Reset-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="071c1-307">重新啟動僅適用於 [進階層](cache-premium-tier-intro.md) 快取。</span><span class="sxs-lookup"><span data-stu-id="071c1-307">Reboot is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="071c1-308">如需重新啟動快取的詳細資訊，請參閱 [快取管理 - 重新啟動](cache-administration.md#reboot)。</span><span class="sxs-lookup"><span data-stu-id="071c1-308">For more information about rebooting your cache, see [Cache administration - reboot](cache-administration.md#reboot).</span></span>
> 
> 

<span data-ttu-id="071c1-309">一份可用的參數及描述 toosee `Reset-AzureRmRedisCache`，請執行 hello 下列命令。</span><span class="sxs-lookup"><span data-stu-id="071c1-309">toosee a list of available parameters and their descriptions for `Reset-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="071c1-310">hello 下列命令重新啟動這兩個節點的 hello 指定快取。</span><span class="sxs-lookup"><span data-stu-id="071c1-310">hello following command reboots both nodes of hello specified cache.</span></span>

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a><span data-ttu-id="071c1-311">後續步驟</span><span class="sxs-lookup"><span data-stu-id="071c1-311">Next steps</span></span>
<span data-ttu-id="071c1-312">toolearn 進一步了解使用 Windows PowerShell 有了 Azure，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="071c1-312">toolearn more about using Windows PowerShell with Azure, see hello following resources:</span></span>

* [<span data-ttu-id="071c1-313">MSDN 上的 Azure Redis 快取 Cmdlet 文件</span><span class="sxs-lookup"><span data-stu-id="071c1-313">Azure Redis Cache cmdlet documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* <span data-ttu-id="071c1-314">[Azure 資源管理員 Cmdlet](http://go.microsoft.com/fwlink/?LinkID=394765)： 了解 toouse hello Azure Resource Manager 模組中的 hello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="071c1-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): Learn toouse hello cmdlets in hello Azure Resource Manager module.</span></span>
* <span data-ttu-id="071c1-315">[使用資源群組您的 Azure 資源 toomanage](../azure-resource-manager/resource-group-template-deploy-portal.md)： 了解如何 toocreate 和管理 hello Azure 入口網站中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="071c1-315">[Using Resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md): Learn how toocreate and manage resource groups in hello Azure portal.</span></span>
* <span data-ttu-id="071c1-316">[Azure 部落格](http://blogs.msdn.com/windowsazure)：深入了解 Azure 的新功能。</span><span class="sxs-lookup"><span data-stu-id="071c1-316">[Azure blog](http://blogs.msdn.com/windowsazure): Learn about new features in Azure.</span></span>
* <span data-ttu-id="071c1-317">[Windows PowerShell 部落格](http://blogs.msdn.com/powershell)：深入了解 Windows PowerShell 的新功能。</span><span class="sxs-lookup"><span data-stu-id="071c1-317">[Windows PowerShell blog](http://blogs.msdn.com/powershell): Learn about new features in Windows PowerShell.</span></span>
* <span data-ttu-id="071c1-318">["Hey, Scripting Guy!"部落格](http://blogs.technet.com/b/heyscriptingguy/)： 從 Windows PowerShell 社群 hello 取得真實世界的秘訣和技巧。</span><span class="sxs-lookup"><span data-stu-id="071c1-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Get real-world tips and tricks from hello Windows PowerShell community.</span></span>

