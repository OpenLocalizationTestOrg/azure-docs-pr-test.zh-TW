---
title: "使用 Azure PowerShell 管理 Azure Redis 快取 | Microsoft Docs"
description: "了解如何使用 Azure PowerShell 執行 Azure Redis 快取的管理工作。"
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
ms.openlocfilehash: 0a5c95eab3fd01f611fc049e80c5c506857e0b81
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a><span data-ttu-id="d4ce5-103">使用 Azure PowerShell 管理 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="d4ce5-103">Manage Azure Redis Cache with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d4ce5-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4ce5-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="d4ce5-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d4ce5-105">Azure CLI</span></span>](cache-manage-cli.md)
> 
> 

<span data-ttu-id="d4ce5-106">本主題顯示如何執行一般工作，例如建立、更新及調整 Azure Redis 快取執行個體，如何重新產生存取金鑰，以及如何檢視您的快取的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-106">This topic shows you how to perform common tasks such as create, update, and scale your Azure Redis Cache instances, how to regenerate access keys, and how to view information about your caches.</span></span> <span data-ttu-id="d4ce5-107">如需 Azure Redis 快取的 PowerShell Cmdlet 完整清單，請參閱 [Azure Redis 快取的 Cmdlet](https://msdn.microsoft.com/library/azure/mt634513.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-107">For a complete list of Azure Redis Cache PowerShell cmdlets, see [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="d4ce5-108">如需傳統部署模型的詳細資訊，請參閱 [Azure Resource Manager 與傳統部署比較：了解資源的部署模型和狀態](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics)。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-108">For more information about the classic deployment model, see [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4ce5-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="d4ce5-109">Prerequisites</span></span>
<span data-ttu-id="d4ce5-110">如果您已安裝 Azure PowerShell，其必須是 Azure PowerShell 1.0.0 或更新的版本。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-110">If you have already installed Azure PowerShell, you must have Azure PowerShell version 1.0.0 or later.</span></span> <span data-ttu-id="d4ce5-111">您可以在 Azure PowerShell 命令提示字元下使用這個命令來檢查已安裝的 Azure PowerShell 版本。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-111">You can check the version of Azure PowerShell that you have installed with this command at the Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version


<span data-ttu-id="d4ce5-112">首先，您必須使用此命令登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-112">First, you must log in to Azure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="d4ce5-113">在 [Microsoft Azure 登入] 對話方塊中，指定 Azure 帳戶的電子郵件地址和密碼。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-113">Specify the email address of your Azure account and its password in the Microsoft Azure sign-in dialog.</span></span>

<span data-ttu-id="d4ce5-114">接下來，如果您有多個 Azure 訂用帳戶，請設定 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-114">Next, if you have multiple Azure subscriptions, you need to set your Azure subscription.</span></span> <span data-ttu-id="d4ce5-115">如果想查看目前的訂用帳戶清單，請執行這個命令。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-115">To see a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="d4ce5-116">若要指定訂用帳戶，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-116">To specify the subscription, run the following command.</span></span> <span data-ttu-id="d4ce5-117">在下列範例中，訂用帳戶的名稱為 `ContosoSubscription`。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-117">In the following example, the subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

<span data-ttu-id="d4ce5-118">在將 Windows PowerShell 與 Azure 資源管理員搭配使用之前，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="d4ce5-118">Before you can use Windows PowerShell with Azure Resource Manager, you need the following:</span></span>

* <span data-ttu-id="d4ce5-119">Windows PowerShell 3.0 或 4.0 版本。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-119">Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="d4ce5-120">若要找出 Windows PowerShell 的版本，輸入：`$PSVersionTable`，並確認 `PSVersion` 的值是 3.0 或 4.0。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-120">To find the version of Windows PowerShell, type:`$PSVersionTable` and verify the value of `PSVersion` is 3.0 or 4.0.</span></span> <span data-ttu-id="d4ce5-121">若要安裝相容版本，請參閱 [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) 或 [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855)。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-121">To install a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="d4ce5-122">若要取得您在本教學課程中任何所見 Cmdlet 的詳細說明，請使用 Get-Help Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-122">To get detailed help for any cmdlet you see in this tutorial, use the Get-Help cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="d4ce5-123">例如，如需取得 `New-AzureRmRedisCache` Cmdlet 的說明，請輸入：</span><span class="sxs-lookup"><span data-stu-id="d4ce5-123">For example, to get help for the `New-AzureRmRedisCache` cmdlet, type:</span></span>

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-to-connect-to-other-clouds"></a><span data-ttu-id="d4ce5-124">如何連線到其他雲端</span><span class="sxs-lookup"><span data-stu-id="d4ce5-124">How to connect to other clouds</span></span>
<span data-ttu-id="d4ce5-125">根據預設，Azure 環境是 `AzureCloud`，其代表全域 Azure 雲端執行個體。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-125">By default the Azure environment is `AzureCloud`, which represents the global Azure cloud instance.</span></span> <span data-ttu-id="d4ce5-126">若要連線至不同的執行個體，請使用 `Add-AzureRmAccount` 命令搭配 `-Environment` 或使用 -`EnvironmentName` 命令列參數搭配所需的環境或環境名稱。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-126">To connect to a different instance, use the `Add-AzureRmAccount` command with the `-Environment` or -`EnvironmentName` command line switch with the desired environment or environment name.</span></span>

<span data-ttu-id="d4ce5-127">若要查看可用環境的清單，請執行 `Get-AzureRmEnvironment` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-127">To see the list of available environments, run the `Get-AzureRmEnvironment` cmdlet.</span></span>

### <a name="to-connect-to-the-azure-government-cloud"></a><span data-ttu-id="d4ce5-128">連線到 Azure Government 雲端</span><span class="sxs-lookup"><span data-stu-id="d4ce5-128">To connect to the Azure Government Cloud</span></span>
<span data-ttu-id="d4ce5-129">如果要連線到 Azure Government 雲端，請使用下列其中一個命令。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-129">To connect to the Azure Government Cloud, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

<span data-ttu-id="d4ce5-130">或</span><span class="sxs-lookup"><span data-stu-id="d4ce5-130">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

<span data-ttu-id="d4ce5-131">如果要在 Azure Government 雲端建立快取，請使用下列其中一個位置。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-131">To create a cache in the Azure Government Cloud, use one of the following locations.</span></span>

* <span data-ttu-id="d4ce5-132">美國政府維吉尼亞州</span><span class="sxs-lookup"><span data-stu-id="d4ce5-132">USGov Virginia</span></span>
* <span data-ttu-id="d4ce5-133">美國政府愛荷華州</span><span class="sxs-lookup"><span data-stu-id="d4ce5-133">USGov Iowa</span></span>

<span data-ttu-id="d4ce5-134">如需 Azure Government 雲端的詳細資訊，請參閱 [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) 和 [Microsoft Azure Government 開發人員指南](../azure-government-developer-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-134">For more information about the Azure Government Cloud, see [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) and [Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>

### <a name="to-connect-to-the-azure-china-cloud"></a><span data-ttu-id="d4ce5-135">連線到 Azure 中國雲端</span><span class="sxs-lookup"><span data-stu-id="d4ce5-135">To connect to the Azure China Cloud</span></span>
<span data-ttu-id="d4ce5-136">如果要連線到 Azure 中國雲端，請使用下列其中一個命令。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-136">To connect to the Azure China Cloud, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

<span data-ttu-id="d4ce5-137">或</span><span class="sxs-lookup"><span data-stu-id="d4ce5-137">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

<span data-ttu-id="d4ce5-138">如果要在 Azure 中國雲端建立快取，請使用下列其中一個位置。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-138">To create a cache in the Azure China Cloud, use one of the following locations.</span></span>

* <span data-ttu-id="d4ce5-139">中國東部</span><span class="sxs-lookup"><span data-stu-id="d4ce5-139">China East</span></span>
* <span data-ttu-id="d4ce5-140">中國北部</span><span class="sxs-lookup"><span data-stu-id="d4ce5-140">China North</span></span>

<span data-ttu-id="d4ce5-141">如需 Azure 中國雲端的詳細資訊，請參閱 [由中國的世紀互聯營運的 Azure 中國雲端](http://www.windowsazure.cn/)。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-141">For more information about the Azure China Cloud, see [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span>

### <a name="to-connect-to-microsoft-azure-germany"></a><span data-ttu-id="d4ce5-142">連線到 Microsoft Azure (德國)</span><span class="sxs-lookup"><span data-stu-id="d4ce5-142">To connect to Microsoft Azure Germany</span></span>
<span data-ttu-id="d4ce5-143">若要連線到 Microsoft Azure (德國)，請使用下列其中一個命令。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-143">To connect to Microsoft Azure Germany, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


<span data-ttu-id="d4ce5-144">或</span><span class="sxs-lookup"><span data-stu-id="d4ce5-144">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

<span data-ttu-id="d4ce5-145">若要在 Microsoft Azure (德國) 中建立快取，請使用下列其中一個位置。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-145">To create a cache in Microsoft Azure Germany, use one of the following locations.</span></span>

* <span data-ttu-id="d4ce5-146">德國中部</span><span class="sxs-lookup"><span data-stu-id="d4ce5-146">Germany Central</span></span>
* <span data-ttu-id="d4ce5-147">德國東北部</span><span class="sxs-lookup"><span data-stu-id="d4ce5-147">Germany Northeast</span></span>

<span data-ttu-id="d4ce5-148">如需有關 Microsoft Azure (德國) 的詳細資訊，請參閱 [Microsoft Azure (德國)](https://azure.microsoft.com/overview/clouds/germany/)。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-148">For more information about Microsoft Azure Germany, see [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span></span>

### <a name="properties-used-for-azure-redis-cache-powershell"></a><span data-ttu-id="d4ce5-149">用於 Azure Redis 快取 PowerShell 的屬性</span><span class="sxs-lookup"><span data-stu-id="d4ce5-149">Properties used for Azure Redis Cache PowerShell</span></span>
<span data-ttu-id="d4ce5-150">下表為使用 Azure PowerShell 建立和管理 Azure Redis 快取執行個體時，常用參數的屬性和說明。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-150">The following table contains properties and descriptions for commonly used parameters when creating and managing your Azure Redis Cache instances using Azure PowerShell.</span></span>

| <span data-ttu-id="d4ce5-151">參數</span><span class="sxs-lookup"><span data-stu-id="d4ce5-151">Parameter</span></span> | <span data-ttu-id="d4ce5-152">說明</span><span class="sxs-lookup"><span data-stu-id="d4ce5-152">Description</span></span> | <span data-ttu-id="d4ce5-153">預設值</span><span class="sxs-lookup"><span data-stu-id="d4ce5-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4ce5-154">Name</span><span class="sxs-lookup"><span data-stu-id="d4ce5-154">Name</span></span> |<span data-ttu-id="d4ce5-155">快取的名稱</span><span class="sxs-lookup"><span data-stu-id="d4ce5-155">Name of the cache</span></span> | |
| <span data-ttu-id="d4ce5-156">位置</span><span class="sxs-lookup"><span data-stu-id="d4ce5-156">Location</span></span> |<span data-ttu-id="d4ce5-157">快取的位置</span><span class="sxs-lookup"><span data-stu-id="d4ce5-157">Location of the cache</span></span> | |
| <span data-ttu-id="d4ce5-158">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="d4ce5-158">ResourceGroupName</span></span> |<span data-ttu-id="d4ce5-159">資源群組名稱，將在其中建立快取</span><span class="sxs-lookup"><span data-stu-id="d4ce5-159">Resource group name in which to create the cache</span></span> | |
| <span data-ttu-id="d4ce5-160">大小</span><span class="sxs-lookup"><span data-stu-id="d4ce5-160">Size</span></span> |<span data-ttu-id="d4ce5-161">快取的大小。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-161">The size of the cache.</span></span> <span data-ttu-id="d4ce5-162">有效值為：P1、P2、P3、P4、C0、C1、C2、C3、C4、C5、C6、250MB、1GB、2.5GB、6GB、13GB、26GB、53GB</span><span class="sxs-lookup"><span data-stu-id="d4ce5-162">Valid values are: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span></span> |<span data-ttu-id="d4ce5-163">1GB</span><span class="sxs-lookup"><span data-stu-id="d4ce5-163">1GB</span></span> |
| <span data-ttu-id="d4ce5-164">ShardCount</span><span class="sxs-lookup"><span data-stu-id="d4ce5-164">ShardCount</span></span> |<span data-ttu-id="d4ce5-165">在啟用叢集的情況下建立進階快取時要建立的分區數目。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-165">The number of shards to create when creating a premium cache with clustering enabled.</span></span> <span data-ttu-id="d4ce5-166">有效值為：1、2、3、4、5、6、7、8、9、10</span><span class="sxs-lookup"><span data-stu-id="d4ce5-166">Valid values are: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></span> | |
| <span data-ttu-id="d4ce5-167">SKU</span><span class="sxs-lookup"><span data-stu-id="d4ce5-167">SKU</span></span> |<span data-ttu-id="d4ce5-168">指定快取的 SKU。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-168">Specifies the SKU of the cache.</span></span> <span data-ttu-id="d4ce5-169">有效值為：Basic、Standard、Premium</span><span class="sxs-lookup"><span data-stu-id="d4ce5-169">Valid values are: Basic, Standard, Premium</span></span> |<span data-ttu-id="d4ce5-170">標準</span><span class="sxs-lookup"><span data-stu-id="d4ce5-170">Standard</span></span> |
| <span data-ttu-id="d4ce5-171">RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="d4ce5-171">RedisConfiguration</span></span> |<span data-ttu-id="d4ce5-172">指定 Redis 組態設定。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-172">Specifies Redis configuration settings.</span></span> <span data-ttu-id="d4ce5-173">如需每個設定的詳細資訊，請參閱以下的 [RedisConfiguration 屬性](#redisconfiguration-properties) 表格。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-173">For details on each setting, see the following [RedisConfiguration properties](#redisconfiguration-properties) table.</span></span> | |
| <span data-ttu-id="d4ce5-174">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="d4ce5-174">EnableNonSslPort</span></span> |<span data-ttu-id="d4ce5-175">指出是否已啟用非 SSL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-175">Indicates whether the non-SSL port is enabled.</span></span> |<span data-ttu-id="d4ce5-176">False</span><span class="sxs-lookup"><span data-stu-id="d4ce5-176">False</span></span> |
| <span data-ttu-id="d4ce5-177">MaxMemoryPolicy</span><span class="sxs-lookup"><span data-stu-id="d4ce5-177">MaxMemoryPolicy</span></span> |<span data-ttu-id="d4ce5-178">這個參數已被取代，請改用 RedisConfiguration。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-178">This parameter has been deprecated - use RedisConfiguration instead.</span></span> | |
| <span data-ttu-id="d4ce5-179">StaticIP</span><span class="sxs-lookup"><span data-stu-id="d4ce5-179">StaticIP</span></span> |<span data-ttu-id="d4ce5-180">當快取是裝載在 VNET 中，為快取在子網路中指定唯一 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-180">When hosting your cache in a VNET, specifies a unique IP address in the subnet for the cache.</span></span> <span data-ttu-id="d4ce5-181">如果未提供，則會從子網路中為您選擇一個。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-181">If not provided, one is chosen for you from the subnet.</span></span> | |
| <span data-ttu-id="d4ce5-182">子網路</span><span class="sxs-lookup"><span data-stu-id="d4ce5-182">Subnet</span></span> |<span data-ttu-id="d4ce5-183">當快取是裝載在 VNET 中，指定要在其中部署快取的子網路。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-183">When hosting your cache in a VNET, specifies the name of the subnet in which to deploy the cache.</span></span> | |
| <span data-ttu-id="d4ce5-184">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="d4ce5-184">VirtualNetwork</span></span> |<span data-ttu-id="d4ce5-185">當快取是裝載在 VNET 中，指定要在其中部署快取的 VNET 之資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-185">When hosting your cache in a VNET, specifies the resource ID of the VNET in which to deploy the cache.</span></span> | |
| <span data-ttu-id="d4ce5-186">KeyType</span><span class="sxs-lookup"><span data-stu-id="d4ce5-186">KeyType</span></span> |<span data-ttu-id="d4ce5-187">指定更新存取金鑰時要重新產生哪一個存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-187">Specifies which access key to regenerate when renewing access keys.</span></span> <span data-ttu-id="d4ce5-188">有效值為：Primary、Secondary</span><span class="sxs-lookup"><span data-stu-id="d4ce5-188">Valid values are: Primary, Secondary</span></span> | |

### <a name="redisconfiguration-properties"></a><span data-ttu-id="d4ce5-189">RedisConfiguration 屬性</span><span class="sxs-lookup"><span data-stu-id="d4ce5-189">RedisConfiguration properties</span></span>
| <span data-ttu-id="d4ce5-190">屬性</span><span class="sxs-lookup"><span data-stu-id="d4ce5-190">Property</span></span> | <span data-ttu-id="d4ce5-191">說明</span><span class="sxs-lookup"><span data-stu-id="d4ce5-191">Description</span></span> | <span data-ttu-id="d4ce5-192">定價層</span><span class="sxs-lookup"><span data-stu-id="d4ce5-192">Pricing tiers</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4ce5-193">rdb-backup-enabled</span><span class="sxs-lookup"><span data-stu-id="d4ce5-193">rdb-backup-enabled</span></span> |<span data-ttu-id="d4ce5-194">是否已啟用 [Redis 資料持續性](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="d4ce5-194">Whether [Redis data persistence](cache-how-to-premium-persistence.md) is enabled</span></span> |<span data-ttu-id="d4ce5-195">僅限進階版</span><span class="sxs-lookup"><span data-stu-id="d4ce5-195">Premium only</span></span> |
| <span data-ttu-id="d4ce5-196">rdb-storage-connection-string</span><span class="sxs-lookup"><span data-stu-id="d4ce5-196">rdb-storage-connection-string</span></span> |<span data-ttu-id="d4ce5-197">[Redis 資料持續性](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="d4ce5-197">The connection string to the storage account for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="d4ce5-198">僅限進階版</span><span class="sxs-lookup"><span data-stu-id="d4ce5-198">Premium only</span></span> |
| <span data-ttu-id="d4ce5-199">rdb-backup-frequency</span><span class="sxs-lookup"><span data-stu-id="d4ce5-199">rdb-backup-frequency</span></span> |<span data-ttu-id="d4ce5-200">[Redis 資料持續性](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="d4ce5-200">The backup frequency for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="d4ce5-201">僅限進階版</span><span class="sxs-lookup"><span data-stu-id="d4ce5-201">Premium only</span></span> |
| <span data-ttu-id="d4ce5-202">maxmemory-reserved</span><span class="sxs-lookup"><span data-stu-id="d4ce5-202">maxmemory-reserved</span></span> |<span data-ttu-id="d4ce5-203">設定非快取程序的 [保留記憶體](cache-configure.md#maxmemory-policy-and-maxmemory-reserved)</span><span class="sxs-lookup"><span data-stu-id="d4ce5-203">Configures the [memory reserved](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for non-cache processes</span></span> |<span data-ttu-id="d4ce5-204">標準和進階</span><span class="sxs-lookup"><span data-stu-id="d4ce5-204">Standard and Premium</span></span> |
| <span data-ttu-id="d4ce5-205">maxmemory-policy</span><span class="sxs-lookup"><span data-stu-id="d4ce5-205">maxmemory-policy</span></span> |<span data-ttu-id="d4ce5-206">設定快取的 [收回原則](cache-configure.md#maxmemory-policy-and-maxmemory-reserved)</span><span class="sxs-lookup"><span data-stu-id="d4ce5-206">Configures the [eviction policy](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for the cache</span></span> |<span data-ttu-id="d4ce5-207">所有定價層</span><span class="sxs-lookup"><span data-stu-id="d4ce5-207">All pricing tiers</span></span> |
| <span data-ttu-id="d4ce5-208">notify-keyspace-events</span><span class="sxs-lookup"><span data-stu-id="d4ce5-208">notify-keyspace-events</span></span> |<span data-ttu-id="d4ce5-209">設定 [Keyspace 通知](cache-configure.md#keyspace-notifications-advanced-settings)</span><span class="sxs-lookup"><span data-stu-id="d4ce5-209">Configures [keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings)</span></span> |<span data-ttu-id="d4ce5-210">標準和進階</span><span class="sxs-lookup"><span data-stu-id="d4ce5-210">Standard and Premium</span></span> |
| <span data-ttu-id="d4ce5-211">hash-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="d4ce5-211">hash-max-ziplist-entries</span></span> |<span data-ttu-id="d4ce5-212">設定小型彙總資料類型的 [記憶體最佳化](http://redis.io/topics/memory-optimization)</span><span class="sxs-lookup"><span data-stu-id="d4ce5-212">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="d4ce5-213">標準和進階</span><span class="sxs-lookup"><span data-stu-id="d4ce5-213">Standard and Premium</span></span> |
| <span data-ttu-id="d4ce5-214">hash-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="d4ce5-214">hash-max-ziplist-value</span></span> |<span data-ttu-id="d4ce5-215">設定小型彙總資料類型的 [記憶體最佳化](http://redis.io/topics/memory-optimization)</span><span class="sxs-lookup"><span data-stu-id="d4ce5-215">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="d4ce5-216">標準和進階</span><span class="sxs-lookup"><span data-stu-id="d4ce5-216">Standard and Premium</span></span> |
| <span data-ttu-id="d4ce5-217">set-max-intset-entries</span><span class="sxs-lookup"><span data-stu-id="d4ce5-217">set-max-intset-entries</span></span> |<span data-ttu-id="d4ce5-218">設定小型彙總資料類型的 [記憶體最佳化](http://redis.io/topics/memory-optimization)</span><span class="sxs-lookup"><span data-stu-id="d4ce5-218">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="d4ce5-219">標準和進階</span><span class="sxs-lookup"><span data-stu-id="d4ce5-219">Standard and Premium</span></span> |
| <span data-ttu-id="d4ce5-220">zset-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="d4ce5-220">zset-max-ziplist-entries</span></span> |<span data-ttu-id="d4ce5-221">設定小型彙總資料類型的 [記憶體最佳化](http://redis.io/topics/memory-optimization)</span><span class="sxs-lookup"><span data-stu-id="d4ce5-221">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="d4ce5-222">標準和進階</span><span class="sxs-lookup"><span data-stu-id="d4ce5-222">Standard and Premium</span></span> |
| <span data-ttu-id="d4ce5-223">zset-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="d4ce5-223">zset-max-ziplist-value</span></span> |<span data-ttu-id="d4ce5-224">設定小型彙總資料類型的 [記憶體最佳化](http://redis.io/topics/memory-optimization)</span><span class="sxs-lookup"><span data-stu-id="d4ce5-224">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="d4ce5-225">標準和進階</span><span class="sxs-lookup"><span data-stu-id="d4ce5-225">Standard and Premium</span></span> |
| <span data-ttu-id="d4ce5-226">資料庫</span><span class="sxs-lookup"><span data-stu-id="d4ce5-226">databases</span></span> |<span data-ttu-id="d4ce5-227">設定資料庫數目。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-227">Configures the number of databases.</span></span> <span data-ttu-id="d4ce5-228">這個屬性僅可以在建立快取時設定。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-228">This property can be configured only at cache creation.</span></span> |<span data-ttu-id="d4ce5-229">標準和進階</span><span class="sxs-lookup"><span data-stu-id="d4ce5-229">Standard and Premium</span></span> |

## <a name="to-create-a-redis-cache"></a><span data-ttu-id="d4ce5-230">建立 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="d4ce5-230">To create a Redis Cache</span></span>
<span data-ttu-id="d4ce5-231">使用 [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) Cmdlet 建立新的 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-231">New Azure Redis Cache instances are created using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4ce5-232">您第一次使用 Azure 入口網站在訂用帳戶中建立 Redis 快取時，入口網站會為該訂用帳戶註冊 `Microsoft.Cache` 命名空間。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-232">The first time you create a Redis cache in a subscription using the Azure portal, the portal registers the `Microsoft.Cache` namespace for that subscription.</span></span> <span data-ttu-id="d4ce5-233">如果您嘗試使用 PowerShell 在訂用帳戶中建立第一個 Redis 快取，您必須先使用下列命令註冊該命名空間；否則 Cmdlet (例如 `New-AzureRmRedisCache` 和 `Get-AzureRmRedisCache`) 會失敗。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-233">If you attempt to create the first Redis cache in a subscription using PowerShell, you must first register that namespace using the following command; otherwise cmdlets such as `New-AzureRmRedisCache` and `Get-AzureRmRedisCache` fail.</span></span>
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

<span data-ttu-id="d4ce5-234">若要查看 `New-AzureRmRedisCache`的可用參數清單及其說明，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-234">To see a list of available parameters and their descriptions for `New-AzureRmRedisCache`, run the following command.</span></span>

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
        The New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of the redis cache to create.

        -ResourceGroupName <String>
            Name of resource group in which to create the redis cache.

        -Location <String>
            Location in which to create the redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of the redis cache. The default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. The default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            The 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting to set
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, the default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            The number of shards to create on a Premium Cluster Cache.

        -VirtualNetwork <String>
            The exact ARM resource ID of the virtual network to deploy the redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="d4ce5-235">若要使用預設參數建立快取，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-235">To create a cache with default parameters, run the following command.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

<span data-ttu-id="d4ce5-236">`ResourceGroupName`、`Name` 和 `Location` 是必要參數，其餘則為選擇性的而且有預設值。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-236">`ResourceGroupName`, `Name`, and `Location` are required parameters, but the rest are optional and have default values.</span></span> <span data-ttu-id="d4ce5-237">執行先前的命令會建立標準 SKU Azure Redis 快取執行個體，具有指定的名稱、位置和資源群組，大小為 1 GB，且停用非 SSL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-237">Running the previous command creates a Standard SKU Azure Redis Cache instance with the specified name, location, and resource group, that is 1 GB in size with the non-SSL port disabled.</span></span>

<span data-ttu-id="d4ce5-238">若要建立進階快取，請指定大小為 P1 (6 GB - 60 GB)、P2 (13 GB - 130 GB)、P3 (26 GB - 260 GB) 或 P4 (53 GB - 530 GB)。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-238">To create a premium cache, specify a size of P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), or P4 (53 GB - 530 GB).</span></span> <span data-ttu-id="d4ce5-239">若要啟用叢集，使用 `ShardCount` 參數指定分區計數。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-239">To enable clustering, specify a shard count using the `ShardCount` parameter.</span></span> <span data-ttu-id="d4ce5-240">下列範例會建立具有 3 個分區的 P1 進階快取。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-240">The following example creates a P1 premium cache with 3 shards.</span></span> <span data-ttu-id="d4ce5-241">P1 進階快取的大小為 6 GB，因為我們指定三個分區，大小總計為 18 GB (3 x 6 GB)。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-241">A P1 premium cache is 6 GB in size, and since we specified three shards the total size is 18 GB (3 x 6 GB).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

<span data-ttu-id="d4ce5-242">若要指定 `RedisConfiguration` 參數的值，以索引鍵/值組的方式將值括在 `{}` 內，例如 `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-242">To specify values for the `RedisConfiguration` parameter, enclose the values inside `{}` as key/value pairs like `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span></span> <span data-ttu-id="d4ce5-243">下列範例會建立標準 1 GB 快取，具有 `allkeys-random` maxmemory 原則，且 keyspace 通知設為 `KEA`。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-243">The following example creates a standard 1 GB cache with `allkeys-random` maxmemory policy and keyspace notifications configured with `KEA`.</span></span> <span data-ttu-id="d4ce5-244">如需詳細資訊，請參閱 [Keyspace 通知 (進階設定)](cache-configure.md#keyspace-notifications-advanced-settings) 和[記憶體原則](cache-configure.md#memory-policies)。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-244">For more information, see [Keyspace notifications (advanced settings)](cache-configure.md#keyspace-notifications-advanced-settings) and [Memory policies](cache-configure.md#memory-policies).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="to-configure-the-databases-setting-during-cache-creation"></a><span data-ttu-id="d4ce5-245">在快取建立期間設定資料庫設定</span><span class="sxs-lookup"><span data-stu-id="d4ce5-245">To configure the databases setting during cache creation</span></span>
<span data-ttu-id="d4ce5-246">`databases` 設定僅可以在快取建立期間設定。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-246">The `databases` setting can be configured only during cache creation.</span></span> <span data-ttu-id="d4ce5-247">下列範例會使用 [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) Cmdlet 建立具有 48 個資料庫的進階 P3 (26 GB) 快取。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-247">The following example creates a premium P3 (26 GB) cache with 48 databases using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

<span data-ttu-id="d4ce5-248">如需 `databases` 屬性的詳細資訊，請參閱 [預設的 Azure Redis 快取伺服器組態](cache-configure.md#default-redis-server-configuration)。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-248">For more information on the `databases` property, see [Default Azure Redis Cache server configuration](cache-configure.md#default-redis-server-configuration).</span></span> <span data-ttu-id="d4ce5-249">如需使用 [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) Cmdlet 建立快取的詳細資訊，請參閱先前的[建立 Redis 快取](#to-create-a-redis-cache)一節。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-249">For more information on creating a cache using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, see the previous [To create a Redis Cache](#to-create-a-redis-cache) section.</span></span>

## <a name="to-update-a-redis-cache"></a><span data-ttu-id="d4ce5-250">更新 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="d4ce5-250">To update a Redis cache</span></span>
<span data-ttu-id="d4ce5-251">使用 [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) Cmdlet 更新 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-251">Azure Redis Cache instances are updated using the [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span></span>

<span data-ttu-id="d4ce5-252">若要查看 `Set-AzureRmRedisCache`的可用參數清單及其說明，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-252">To see a list of available parameters and their descriptions for `Set-AzureRmRedisCache`, run the following command.</span></span>

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
        The Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of the redis cache to update.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        -Size <String>
            Size of the redis cache. The default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. The default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            The 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting to set
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. The default value is null and no change will be made to the
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            The number of shards to create on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="d4ce5-253">`Set-AzureRmRedisCache` Cmdlet 可用來更新屬性，例如 `Size`、`Sku`、`EnableNonSslPort` 和 `RedisConfiguration` 的值。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-253">The `Set-AzureRmRedisCache` cmdlet can be used to update properties such as `Size`, `Sku`, `EnableNonSslPort`, and the `RedisConfiguration` values.</span></span> 

<span data-ttu-id="d4ce5-254">下列命令會更新名為 myCache 的 Redis 快取的 maxmemory-policy。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-254">The following command updates the maxmemory-policy for the Redis Cache named myCache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="to-scale-a-redis-cache"></a><span data-ttu-id="d4ce5-255">調整 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="d4ce5-255">To scale a Redis cache</span></span>
<span data-ttu-id="d4ce5-256">修改 `Size`、`Sku` 或 `ShardCount` 屬性時，可用 `Set-AzureRmRedisCache` 調整 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-256">`Set-AzureRmRedisCache` can be used to scale an Azure Redis cache instance when the `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> 

> [!NOTE]
> <span data-ttu-id="d4ce5-257">使用 PowerShell 調整快取，和從 Azure 入口網站調整快取有相同的限制和準則。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-257">Scaling a cache using PowerShell is subject to the same limits and guidelines as scaling a cache from the Azure portal.</span></span> <span data-ttu-id="d4ce5-258">您可以調整具有下列限制的不同定價層。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-258">You can scale to a different pricing tier with the following restrictions.</span></span>
> 
> * <span data-ttu-id="d4ce5-259">您無法從較高的定價層調整至較低的定價層。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-259">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
> * <span data-ttu-id="d4ce5-260">您無法從**進階**快取向下調整至**標準**或**基本**快取。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-260">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
> * <span data-ttu-id="d4ce5-261">您無法從**標準**快取向下調整到**基本**快取。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-261">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
> * <span data-ttu-id="d4ce5-262">您可以從**基本**快取調整到**標準**快取，但您無法同時變更大小。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-262">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="d4ce5-263">如果您需要不同的大小，您可以進行後續調整作業，調整到您需要的大小。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-263">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
> * <span data-ttu-id="d4ce5-264">您無法直接從**基本**快取調整至**進階**快取。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-264">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="d4ce5-265">您必須在單一調整作業中從**基本**調整至**標準**，然後在後續的調整作業中從**標準**調整至**進階**。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-265">You must scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
> * <span data-ttu-id="d4ce5-266">您無法從較大的大小向下調整至 **C0 (250 MB)** 的大小。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-266">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>
> 
> <span data-ttu-id="d4ce5-267">如需詳細資訊，請參閱 [如何調整 Azure Redis 快取](cache-how-to-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-267">For more information, see [How to Scale Azure Redis Cache](cache-how-to-scale.md).</span></span>
> 
> 

<span data-ttu-id="d4ce5-268">下列範例示範如何將名為 `myCache` 的快取調整為 2.5 GB 快取。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-268">The following example shows how to scale a cache named `myCache` to a 2.5 GB cache.</span></span> <span data-ttu-id="d4ce5-269">請注意，此命令可用於基本或標準快取。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-269">Note that this command works for both a Basic or a Standard cache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="d4ce5-270">發出此命令之後，會傳回快取的狀態 (類似於呼叫 `Get-AzureRmRedisCache`)。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-270">After this command is issued, the status of the cache is returned (similar to calling `Get-AzureRmRedisCache`).</span></span> <span data-ttu-id="d4ce5-271">請注意，`ProvisioningState` 為 `Scaling`。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-271">Note that the `ProvisioningState` is `Scaling`.</span></span>

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

<span data-ttu-id="d4ce5-272">當調整作業完成時，`ProvisioningState` 會變更為 `Succeeded`。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-272">When the scaling operation is complete, the `ProvisioningState` changes to `Succeeded`.</span></span> <span data-ttu-id="d4ce5-273">如果您需要進行後續的調整作業，例如先從基本變更為標準，然後再變更大小，您必須等到先前作業完成，否則會收到類似下列的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-273">If you need to make a subsequent scaling operation, such as changing from Basic to Standard and then changing the size, you must wait until the previous operation is complete or you receive an error similar to the following.</span></span>

    Set-AzureRmRedisCache : Conflict: The resource '...' is not in a stable state, and is currently unable to accept the update request.

## <a name="to-get-information-about-a-redis-cache"></a><span data-ttu-id="d4ce5-274">取得 Redis 快取的資訊</span><span class="sxs-lookup"><span data-stu-id="d4ce5-274">To get information about a Redis cache</span></span>
<span data-ttu-id="d4ce5-275">您可以使用 [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) Cmdlet 擷取快取的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-275">You can retrieve information about a cache using the [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span></span>

<span data-ttu-id="d4ce5-276">若要查看 `Get-AzureRmRedisCache`的可用參數清單及其說明，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-276">To see a list of available parameters and their descriptions for `Get-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in the specified resource group or all caches in the current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        The Get-AzureRmRedisCache cmdlet gets the details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in the specified resource group.

        If no parameters are given than it will return details about all caches the current subscription.

    PARAMETERS
        -Name <String>
            The name of the cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns the details for the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns the details of the cache specified by Name. If only the ResourceGroup
            parameter is provided, then details for all caches in the resource group are returned.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="d4ce5-277">若要傳回目前訂用帳戶中所有快取的相關資訊，請不帶任何參數執行 `Get-AzureRmRedisCache`。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-277">To return information about all caches in the current subscription, run `Get-AzureRmRedisCache` without any parameters.</span></span>

    Get-AzureRmRedisCache

<span data-ttu-id="d4ce5-278">若要傳回特定資源群組中所有快取的相關資訊，請執行 `Get-AzureRmRedisCache` 並使用 `ResourceGroupName` 參數。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-278">To return information about all caches in a specific resource group, run `Get-AzureRmRedisCache` with the `ResourceGroupName` parameter.</span></span>

    Get-AzureRmRedisCache -ResourceGroupName myGroup

<span data-ttu-id="d4ce5-279">若要傳回特定快取的相關資訊，請執行 `Get-AzureRmRedisCache`，並使用 `Name` 參數包含快取名稱，和 `ResourceGroupName` 參數包含快取的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-279">To return information about a specific cache, run `Get-AzureRmRedisCache` with the `Name` parameter containing the name of the cache, and the `ResourceGroupName` parameter with the resource group containing that cache.</span></span>

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

## <a name="to-retrieve-the-access-keys-for-a-redis-cache"></a><span data-ttu-id="d4ce5-280">擷取 Redis 快取的存取金鑰</span><span class="sxs-lookup"><span data-stu-id="d4ce5-280">To retrieve the access keys for a Redis cache</span></span>
<span data-ttu-id="d4ce5-281">若要擷取您快取的存取金鑰，您可以使用 [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-281">To retrieve the access keys for your cache, you can use the [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span></span>

<span data-ttu-id="d4ce5-282">若要查看 `Get-AzureRmRedisCacheKey`的可用參數清單及其說明，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-282">To see a list of available parameters and their descriptions for `Get-AzureRmRedisCacheKey`, run the following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets the accesskeys for the specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        The Get-AzureRmRedisCacheKey cmdlet gets the access keys for the specified cache.

    PARAMETERS
        -Name <String>
            Name of the redis cache.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="d4ce5-283">若要擷取您快取的金鑰，請呼叫 `Get-AzureRmRedisCacheKey` Cmdlet，並傳入快取的名稱以及包含快取的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-283">To retrieve the keys for your cache, call the `Get-AzureRmRedisCacheKey` cmdlet and pass in the name of your cache the name of the resource group that contains the cache.</span></span>

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="to-regenerate-access-keys-for-your-redis-cache"></a><span data-ttu-id="d4ce5-284">重新產生 Redis 快取的存取金鑰</span><span class="sxs-lookup"><span data-stu-id="d4ce5-284">To regenerate access keys for your Redis cache</span></span>
<span data-ttu-id="d4ce5-285">若要重新產生您快取的存取金鑰，可以使用 [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-285">To regenerate the access keys for your cache, you can use the [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span></span>

<span data-ttu-id="d4ce5-286">若要查看 `New-AzureRmRedisCacheKey`的可用參數清單及其說明，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-286">To see a list of available parameters and their descriptions for `New-AzureRmRedisCacheKey`, run the following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates the access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        The New-AzureRmRedisCacheKey cmdlet regenerate the access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of the redis cache.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        -KeyType <String>
            Specifies whether to regenerate the primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When the Force parameter is provided, the specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="d4ce5-287">若要重新產生快取的主要或次要金鑰，請呼叫 `New-AzureRmRedisCacheKey` Cmdlet，並傳入名稱、資源群組，且針對 `KeyType` 參數指定 `Primary` 或 `Secondary`。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-287">To regenerate the primary or secondary key for your cache, call the `New-AzureRmRedisCacheKey` cmdlet and pass in the name, resource group, and specify either `Primary` or `Secondary` for the `KeyType` parameter.</span></span> <span data-ttu-id="d4ce5-288">在下列範例中，會重新產生快取的次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-288">In the following example, the secondary access key for a cache is regenerated.</span></span>

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want to regenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="to-delete-a-redis-cache"></a><span data-ttu-id="d4ce5-289">刪除 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="d4ce5-289">To delete a Redis cache</span></span>
<span data-ttu-id="d4ce5-290">若要刪除 Redis 快取，請使用 [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-290">To delete a Redis cache, use the [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span></span>

<span data-ttu-id="d4ce5-291">若要查看 `Remove-AzureRmRedisCache`的可用參數清單及其說明，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-291">To see a list of available parameters and their descriptions for `Remove-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        The Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of the redis cache to remove.

        -ResourceGroupName <String>
            Name of the resource group of the cache to remove.

        -Force
            When the Force parameter is provided, the cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes the cache and does not return any value. If the PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating the success of the operatio

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="d4ce5-292">在下列範例中，會移除名為 `myCache` 的快取。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-292">In the following example, the cache named `myCache` is removed.</span></span>

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want to remove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="to-import-a-redis-cache"></a><span data-ttu-id="d4ce5-293">匯入 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="d4ce5-293">To import a Redis cache</span></span>
<span data-ttu-id="d4ce5-294">您可以使用 `Import-AzureRmRedisCache` Cmdlet 將資料匯入 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-294">You can import data into an Azure Redis Cache instance using the `Import-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4ce5-295">匯入/匯出僅供 [進階層](cache-premium-tier-intro.md) 快取使用。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-295">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="d4ce5-296">如需匯入/匯出的詳細資訊，請參閱 [在 Azure Redis 快取中匯入與匯出資料](cache-how-to-import-export-data.md)。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-296">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="d4ce5-297">若要查看 `Import-AzureRmRedisCache`的可用參數清單及其說明，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-297">To see a list of available parameters and their descriptions for `Import-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs to Azure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Import-AzureRmRedisCache cmdlet imports data from the specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into the cache.

        -Format <String>
            Format for the blob.  Currently "rdb" is the only supported, with other formats expected in the future.

        -Force
            When the Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If the PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating the success of the
            operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="d4ce5-298">以下命令能將資料從 SAS URI 所指定的 blob 匯入 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-298">The following command imports data from the blob specified by the SAS uri into Azure Redis Cache.</span></span>

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="to-export-a-redis-cache"></a><span data-ttu-id="d4ce5-299">匯出 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="d4ce5-299">To export a Redis cache</span></span>
<span data-ttu-id="d4ce5-300">您可以使用 `Export-AzureRmRedisCache` Cmdlet 從 Azure Redis 快取執行個體匯出資料。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-300">You can export data from an Azure Redis Cache instance using the `Export-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4ce5-301">匯入/匯出僅供 [進階層](cache-premium-tier-intro.md) 快取使用。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-301">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="d4ce5-302">如需匯入/匯出的詳細資訊，請參閱 [在 Azure Redis 快取中匯入與匯出資料](cache-how-to-import-export-data.md)。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-302">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="d4ce5-303">若要查看 `Export-AzureRmRedisCache`的可用參數清單及其說明，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-303">To see a list of available parameters and their descriptions for `Export-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache to a specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache to a specified container.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -Prefix <String>
            Prefix to use for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for the blob.  Currently "rdb" is the only supported, with other formats expected in the future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If the PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating the success of the operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="d4ce5-304">以下命令能將資料從 Azure Redis 快取執行個體匯出到 SAS URI 所指定的容器。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-304">The following command exports data from an Azure Redis Cache instance into the container specified by the SAS uri.</span></span>

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="to-reboot-a-redis-cache"></a><span data-ttu-id="d4ce5-305">重新啟動 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="d4ce5-305">To reboot a Redis cache</span></span>
<span data-ttu-id="d4ce5-306">您可以使用 `Reset-AzureRmRedisCache` Cmdlet 重新啟動 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-306">You can reboot your Azure Redis Cache instance using the `Reset-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4ce5-307">重新啟動僅適用於 [進階層](cache-premium-tier-intro.md) 快取。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-307">Reboot is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="d4ce5-308">如需重新啟動快取的詳細資訊，請參閱 [快取管理 - 重新啟動](cache-administration.md#reboot)。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-308">For more information about rebooting your cache, see [Cache administration - reboot](cache-administration.md#reboot).</span></span>
> 
> 

<span data-ttu-id="d4ce5-309">若要查看 `Reset-AzureRmRedisCache`的可用參數清單及其說明，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-309">To see a list of available parameters and their descriptions for `Reset-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Reset-AzureRmRedisCache cmdlet reboots the specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -RebootType <String>
            Which node to reboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard to reboot when rebooting a premium cache with clustering enabled.

        -Force
            When the Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If the PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating the success of the operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="d4ce5-310">以下命令會重新啟動指定快取的兩個節點。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-310">The following command reboots both nodes of the specified cache.</span></span>

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a><span data-ttu-id="d4ce5-311">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d4ce5-311">Next steps</span></span>
<span data-ttu-id="d4ce5-312">若要深入了解如何將 Windows PowerShell 與 Azure 搭配使用，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="d4ce5-312">To learn more about using Windows PowerShell with Azure, see the following resources:</span></span>

* [<span data-ttu-id="d4ce5-313">MSDN 上的 Azure Redis 快取 Cmdlet 文件</span><span class="sxs-lookup"><span data-stu-id="d4ce5-313">Azure Redis Cache cmdlet documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* <span data-ttu-id="d4ce5-314">[Azure Resource Manager Cmdlet](http://go.microsoft.com/fwlink/?LinkID=394765)：了解如何使用 Azure Resource Manager 模組中的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): Learn to use the cmdlets in the Azure Resource Manager module.</span></span>
* <span data-ttu-id="d4ce5-315">[使用資源群組管理 Azure 資源](../azure-resource-manager/resource-group-template-deploy-portal.md)：了解如何在 Azure 入口網站中建立和管理資源群組。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-315">[Using Resource groups to manage your Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md): Learn how to create and manage resource groups in the Azure portal.</span></span>
* <span data-ttu-id="d4ce5-316">[Azure 部落格](http://blogs.msdn.com/windowsazure)：深入了解 Azure 的新功能。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-316">[Azure blog](http://blogs.msdn.com/windowsazure): Learn about new features in Azure.</span></span>
* <span data-ttu-id="d4ce5-317">[Windows PowerShell 部落格](http://blogs.msdn.com/powershell)：深入了解 Windows PowerShell 的新功能。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-317">[Windows PowerShell blog](http://blogs.msdn.com/powershell): Learn about new features in Windows PowerShell.</span></span>
* <span data-ttu-id="d4ce5-318">["Hey, Scripting Guy!"部落格](http://blogs.technet.com/b/heyscriptingguy/)：從 Windows PowerShell 社群中取得實際的秘訣及訣竅。</span><span class="sxs-lookup"><span data-stu-id="d4ce5-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Get real-world tips and tricks from the Windows PowerShell community.</span></span>

