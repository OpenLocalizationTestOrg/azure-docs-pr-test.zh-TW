---
title: "針對 Azure 虛擬網路閘道和連線進行疑難排解 - Azure CLI 1.0 | Microsoft Docs"
description: "此頁面說明如何使用 Azure 網路監看員來針對 Azure CLI 1.0 進行疑難排解"
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
ms.openlocfilehash: 9de4b2a0bdda7ffbd269883877a708d67312092f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a><span data-ttu-id="1795a-103">使用 Azure 網路監看員 Azure CLI 1.0 來針對虛擬網路閘道和連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="1795a-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="1795a-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="1795a-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="1795a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1795a-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="1795a-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1795a-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="1795a-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1795a-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="1795a-108">REST API</span><span class="sxs-lookup"><span data-stu-id="1795a-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="1795a-109">網路監看員提供了許多功能，因為它的作用就是為了讓您了解您在 Azure 中的網路資源。</span><span class="sxs-lookup"><span data-stu-id="1795a-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="1795a-110">這些功能的其中之一便是資源疑難排解。</span><span class="sxs-lookup"><span data-stu-id="1795a-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="1795a-111">您可以透過入口網站、PowerShell、CLI 或 REST API 呼叫資源疑難排解。</span><span class="sxs-lookup"><span data-stu-id="1795a-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="1795a-112">一經呼叫，網路監看員就會檢查虛擬網路閘道或連線的健全狀況，並傳回其調查結果。</span><span class="sxs-lookup"><span data-stu-id="1795a-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="1795a-113">本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="1795a-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="1795a-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="1795a-114">Before you begin</span></span>

<span data-ttu-id="1795a-115">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="1795a-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="1795a-116">如需支援的閘道類型清單，請瀏覽[支援的閘道類型](/network-watcher-troubleshoot-overview.md#supported-gateway-types)。</span><span class="sxs-lookup"><span data-stu-id="1795a-116">For a list of supported gateway types visit, [Supported Gateway types](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="1795a-117">概觀</span><span class="sxs-lookup"><span data-stu-id="1795a-117">Overview</span></span>

<span data-ttu-id="1795a-118">資源疑難排解可讓您針對虛擬網路閘道和連線所發生的問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="1795a-118">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="1795a-119">在要求進行資源疑難排解後，便會查詢並檢查記錄。</span><span class="sxs-lookup"><span data-stu-id="1795a-119">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="1795a-120">檢查完成時，就會傳回結果。</span><span class="sxs-lookup"><span data-stu-id="1795a-120">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="1795a-121">資源疑難排解要求是執行時間很長的要求，可能需要幾分鐘的時間才會傳回結果。</span><span class="sxs-lookup"><span data-stu-id="1795a-121">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="1795a-122">疑難排解記錄會儲存在指定儲存體帳戶的容器中。</span><span class="sxs-lookup"><span data-stu-id="1795a-122">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="1795a-123">擷取虛擬網路閘道連線</span><span class="sxs-lookup"><span data-stu-id="1795a-123">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="1795a-124">在此範例中，系統會對連線執行資源疑難排解。</span><span class="sxs-lookup"><span data-stu-id="1795a-124">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="1795a-125">您也可以將它傳遞給虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="1795a-125">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="1795a-126">下列 Cmdlet 會列出資源群組中的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="1795a-126">The following cmdlet lists the vpn-connections in a resource group.</span></span>

```azurecli
azure network vpn-connection list -g resourceGroupName
```

<span data-ttu-id="1795a-127">您也可以執行命令來查看訂用帳戶中的連線。</span><span class="sxs-lookup"><span data-stu-id="1795a-127">You can also run the command to see the connections in a subscription.</span></span>

```azurecli
azure network vpn-connection list -s subscription
```

<span data-ttu-id="1795a-128">在取得連線的名稱之後，您可以執行此命令來取得其資源識別碼︰</span><span class="sxs-lookup"><span data-stu-id="1795a-128">Once you have the name of the connection, you can run this command to get its resource Id:</span></span>

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a><span data-ttu-id="1795a-129">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="1795a-129">Create a storage account</span></span>

<span data-ttu-id="1795a-130">資源疑難排解會傳回資源健全狀況的相關資料，它也會將記錄儲存到儲存體帳戶以供檢閱。</span><span class="sxs-lookup"><span data-stu-id="1795a-130">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="1795a-131">在此步驟中，我們會建立儲存體帳戶，如果已有現有的儲存體帳戶，您也可以使用它。</span><span class="sxs-lookup"><span data-stu-id="1795a-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="1795a-132">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="1795a-132">Create the storage account</span></span>

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. <span data-ttu-id="1795a-133">取得儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="1795a-133">Get the storage account keys</span></span>

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. <span data-ttu-id="1795a-134">建立容器</span><span class="sxs-lookup"><span data-stu-id="1795a-134">Create the container</span></span>

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="1795a-135">執行網路監看員資源疑難排解</span><span class="sxs-lookup"><span data-stu-id="1795a-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="1795a-136">您可以使用 `network watcher troubleshoot` Cmdlet 對資源進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="1795a-136">You troubleshoot resources with the `network watcher troubleshoot` cmdlet.</span></span> <span data-ttu-id="1795a-137">我們會將資源群組、網路監看員名稱、連線識別碼、儲存體帳戶識別碼，以及用以儲存疑難排解結果之 Blob 的路徑傳遞給此 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="1795a-137">We pass the cmdlet the resource group, the name of the Network Watcher, the Id of the connection, the Id of the storage account, and the path to the blob to store the troubleshoot results in.</span></span>

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

<span data-ttu-id="1795a-138">在執行此 Cmdlet 後，網路監看員會檢閱資源以驗證其健康狀態。</span><span class="sxs-lookup"><span data-stu-id="1795a-138">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="1795a-139">它會將結果傳回殼層，並將結果的記錄儲存在指定的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="1795a-139">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="1795a-140">了解結果</span><span class="sxs-lookup"><span data-stu-id="1795a-140">Understanding the results</span></span>

<span data-ttu-id="1795a-141">動作文字會提供有關如何解決問題的一般指引。</span><span class="sxs-lookup"><span data-stu-id="1795a-141">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="1795a-142">如果問題有可行動作，則會提供附有其他指引的連結。</span><span class="sxs-lookup"><span data-stu-id="1795a-142">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="1795a-143">如果沒有其他指引，回應中會提供 URL 以供您開啟支援案例。</span><span class="sxs-lookup"><span data-stu-id="1795a-143">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="1795a-144">如需回應屬性和所含內容的詳細資訊，請瀏覽[網路監看員疑難排解概觀](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1795a-144">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="1795a-145">如需從 Azure 儲存體帳戶下載檔案的指示，請參閱[以 .NET 開始使用 Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="1795a-145">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="1795a-146">另一項可用工具為儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="1795a-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="1795a-147">有關儲存體總管的詳細資訊可以在下列連結找到︰[儲存體總管](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="1795a-147">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="1795a-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1795a-148">Next steps</span></span>

<span data-ttu-id="1795a-149">如果設定已變更而停止了 VPN 連線，請參閱[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)以追蹤可能有問題的網路安全性群組和安全性規則。</span><span class="sxs-lookup"><span data-stu-id="1795a-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
