---
title: "aaaTroubleshoot Azure 虛擬網路閘道與連線-Azure CLI 1.0 |Microsoft 文件"
description: "此頁面說明 toouse hello Azure 網路監看員如何疑難排解 Azure CLI 1.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: a0511689d773f9c7216b0fe5470e27f754eb600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a><span data-ttu-id="5d9ed-103">使用 Azure 網路監看員 Azure CLI 1.0 來針對虛擬網路閘道和連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="5d9ed-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="5d9ed-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="5d9ed-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="5d9ed-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d9ed-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="5d9ed-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5d9ed-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="5d9ed-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5d9ed-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="5d9ed-108">REST API</span><span class="sxs-lookup"><span data-stu-id="5d9ed-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="5d9ed-109">網路監看員會提供許多功能與 toounderstanding 您在 Azure 中的網路資源。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="5d9ed-110">這些功能的其中之一便是資源疑難排解。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="5d9ed-111">疑難排解資源可以透過 hello 入口網站、 PowerShell、 CLI 或 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="5d9ed-112">呼叫時，網路監看員會檢查 hello 的虛擬網路閘道或連線的健全狀況，並傳回其發現。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="5d9ed-113">本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="5d9ed-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="5d9ed-114">Before you begin</span></span>

<span data-ttu-id="5d9ed-115">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="5d9ed-116">如需支援的閘道類型清單，請瀏覽[支援的閘道類型](/network-watcher-troubleshoot-overview.md#supported-gateway-types)。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-116">For a list of supported gateway types visit, [Supported Gateway types](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="5d9ed-117">概觀</span><span class="sxs-lookup"><span data-stu-id="5d9ed-117">Overview</span></span>

<span data-ttu-id="5d9ed-118">疑難排解資源提供 hello 功能的虛擬網路閘道與連線發生問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-118">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="5d9ed-119">當提出要求時 tooresource 疑難排解記錄檔正在檢查和查詢。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-119">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="5d9ed-120">檢查完成時，會傳回 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-120">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="5d9ed-121">疑難排解要求是長時間執行的資源要求，但這可能需要多個分鐘 tooreturn 結果。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-121">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="5d9ed-122">hello 疑難排解記錄檔會儲存在指定的儲存體帳戶的容器。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-122">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="5d9ed-123">擷取虛擬網路閘道連線</span><span class="sxs-lookup"><span data-stu-id="5d9ed-123">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="5d9ed-124">在此範例中，系統會對連線執行資源疑難排解。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-124">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="5d9ed-125">您也可以將它傳遞給虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-125">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="5d9ed-126">hello 下列 cmdlet 會列出 hello vpn 連線的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-126">hello following cmdlet lists hello vpn-connections in a resource group.</span></span>

```azurecli
azure network vpn-connection list -g resourceGroupName
```

<span data-ttu-id="5d9ed-127">您也可以執行 hello 命令 toosee hello 連線訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-127">You can also run hello command toosee hello connections in a subscription.</span></span>

```azurecli
azure network vpn-connection list -s subscription
```

<span data-ttu-id="5d9ed-128">一旦您擁有 hello hello 連接名稱，您可以執行這個命令 tooget 其資源識別碼：</span><span class="sxs-lookup"><span data-stu-id="5d9ed-128">Once you have hello name of hello connection, you can run this command tooget its resource Id:</span></span>

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a><span data-ttu-id="5d9ed-129">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5d9ed-129">Create a storage account</span></span>

<span data-ttu-id="5d9ed-130">疑難排解資源傳回 hello hello 資源健全狀況的相關資料，它也會儲存記錄檔 tooa 儲存體帳戶 toobe 檢閱。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-130">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="5d9ed-131">在此步驟中，我們會建立儲存體帳戶，如果已有現有的儲存體帳戶，您也可以使用它。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="5d9ed-132">建立 hello 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5d9ed-132">Create hello storage account</span></span>

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. <span data-ttu-id="5d9ed-133">取得 hello 儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="5d9ed-133">Get hello storage account keys</span></span>

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. <span data-ttu-id="5d9ed-134">建立 hello 容器</span><span class="sxs-lookup"><span data-stu-id="5d9ed-134">Create hello container</span></span>

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="5d9ed-135">執行網路監看員資源疑難排解</span><span class="sxs-lookup"><span data-stu-id="5d9ed-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="5d9ed-136">疑難排解資源以 hello `network watcher troubleshoot` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-136">You troubleshoot resources with hello `network watcher troubleshoot` cmdlet.</span></span> <span data-ttu-id="5d9ed-137">我們會傳送 hello cmdlet hello 資源群組、 hello hello 網路監看員，hello hello 連接識別碼的名稱 hello hello 的儲存體帳戶的識別碼和 hello 路徑 toohello blob toostore hello 疑難排解中的結果。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-137">We pass hello cmdlet hello resource group, hello name of hello Network Watcher, hello Id of hello connection, hello Id of hello storage account, and hello path toohello blob toostore hello troubleshoot results in.</span></span>

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

<span data-ttu-id="5d9ed-138">一旦您執行 hello cmdlet，網路監看員會檢閱 hello 資源 tooverify hello 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-138">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="5d9ed-139">它會傳回 hello 結果 toohello shell，並將指定 hello 儲存體帳戶中的 hello 結果的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-139">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="5d9ed-140">了解 hello 結果</span><span class="sxs-lookup"><span data-stu-id="5d9ed-140">Understanding hello results</span></span>

<span data-ttu-id="5d9ed-141">動作的 hello 文字上 tooresolve hello 問題的方式，提供一般指引。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-141">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="5d9ed-142">Hello 問題，可以採取的動作，如果是其他指南提供的連結。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-142">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="5d9ed-143">Hello 案例中的任何其他指引，hello 回應提供 hello url tooopen 支援案例。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-143">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="5d9ed-144">如需回應 hello 和時要包含的 hello 屬性的詳細資訊，請瀏覽[網路監看員疑難排解概觀](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="5d9ed-144">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="5d9ed-145">如需從 azure 儲存體帳戶下載檔案的指示，請參閱太[開始使用適用於.NET 的 Azure Blob 儲存體使用](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-145">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="5d9ed-146">另一項可用工具為儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="5d9ed-147">儲存體總管的詳細資訊可以在這裡找到在 hello 下列連結：[存放裝置總管](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="5d9ed-147">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d9ed-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d9ed-148">Next steps</span></span>

<span data-ttu-id="5d9ed-149">如果設定已變更為該停止 VPN 連線能力，請參閱[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)tootrack 向 hello 網路安全性群組和安全性規則，可能會有問題。</span><span class="sxs-lookup"><span data-stu-id="5d9ed-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
