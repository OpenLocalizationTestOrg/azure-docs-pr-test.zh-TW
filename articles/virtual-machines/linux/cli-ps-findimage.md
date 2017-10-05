---
title: "使用 Azure CLI 選取 Linux VM 映像 | Microsoft Docs"
description: "了解如何使用 Azure CLI 來判斷發行者、優惠、SKU 和 Marketplace VM 映像的版本。"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7a858e38-4f17-4e8e-a28a-c7f801101721
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/24/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e0c27a7ee9e9a7ab1a3b004e070fa556b56a36a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-find-linux-vm-images-in-the-azure-marketplace-with-the-azure-cli"></a><span data-ttu-id="0a46d-103">如何使用 Azure CLI 在 Azure Marketplace 中尋找 Linux VM 映像</span><span class="sxs-lookup"><span data-stu-id="0a46d-103">How to find Linux VM images in the Azure Marketplace with the Azure CLI</span></span>
<span data-ttu-id="0a46d-104">本主題描述如何在 Azure Marketplace 中使用 Azure CLI 2.0 尋找 Windows VM 映像。</span><span class="sxs-lookup"><span data-stu-id="0a46d-104">This topic describes how to use the Azure CLI 2.0 to find VM images in the Azure Marketplace.</span></span> <span data-ttu-id="0a46d-105">您可以使用此資訊，在建立 Linux VM 時指定 Marketplace 映像。</span><span class="sxs-lookup"><span data-stu-id="0a46d-105">Use this information to specify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="0a46d-106">請確定您[已安裝](/cli/azure/install-az-cli2)最新的 Azure CLI 2.0 並登入 Azure 帳戶 (`az login`)。</span><span class="sxs-lookup"><span data-stu-id="0a46d-106">Make sure that you installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in to an Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="0a46d-107">術語</span><span class="sxs-lookup"><span data-stu-id="0a46d-107">Terminology</span></span>

<span data-ttu-id="0a46d-108">您可以根據階層，在 CLI 和其他 Azure 工具中找到 Marketplace 映像：</span><span class="sxs-lookup"><span data-stu-id="0a46d-108">Marketplace images are identified in the CLI and other Azure tools according to a hierarchy:</span></span>

* <span data-ttu-id="0a46d-109">**發行者** - 建立映像的組織。</span><span class="sxs-lookup"><span data-stu-id="0a46d-109">**Publisher** - The organization that created the image.</span></span> <span data-ttu-id="0a46d-110">範例：Canonical</span><span class="sxs-lookup"><span data-stu-id="0a46d-110">Example: Canonical</span></span>
* <span data-ttu-id="0a46d-111">**供應項目** - 發行者所建立的一組相關映像。</span><span class="sxs-lookup"><span data-stu-id="0a46d-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="0a46d-112">範例：Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="0a46d-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="0a46d-113">**SKU** - 供應項目執行個體，例如發佈的主要版本。</span><span class="sxs-lookup"><span data-stu-id="0a46d-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="0a46d-114">範例：16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="0a46d-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="0a46d-115">**版本** - 映像 SKU 的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="0a46d-115">**Version** - The version number of an image SKU.</span></span> <span data-ttu-id="0a46d-116">指定映像時，您可以使用 "latest" 來取代版本號碼，這會選取發佈的最新版本。</span><span class="sxs-lookup"><span data-stu-id="0a46d-116">When specifying the image, you can replace the version number with "latest", which selects the latest version of the distribution.</span></span>

<span data-ttu-id="0a46d-117">若要指定 Marketplace 映像，您通常會使用映像 *URN*。</span><span class="sxs-lookup"><span data-stu-id="0a46d-117">To specify a Marketplace image, you typically use the image *URN*.</span></span> <span data-ttu-id="0a46d-118">URN 會結合這些值，並以冒號 (:) 字元分隔：發行者:供應項目:SKU:版本。</span><span class="sxs-lookup"><span data-stu-id="0a46d-118">The URN combines these values, separated by the colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="0a46d-119">列出常用的映像</span><span class="sxs-lookup"><span data-stu-id="0a46d-119">List popular images</span></span>

<span data-ttu-id="0a46d-120">執行 [az vm image list](/cli/azure/vm/image#list) 命令，而不包含 `--all` 選項，以查看 Azure Marketplace 中的常用 VM 映像清單。</span><span class="sxs-lookup"><span data-stu-id="0a46d-120">Run the [az vm image list](/cli/azure/vm/image#list) command, without the `--all` option, to see a list of popular VM images in the Azure Marketplace.</span></span> <span data-ttu-id="0a46d-121">例如，執行下列命令，以資料表格式顯示常用映像的快取清單：</span><span class="sxs-lookup"><span data-stu-id="0a46d-121">For example, run the following command to display a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="0a46d-122">輸出會包含 URN ([Urn] 欄中的值)，可用來指定映像。</span><span class="sxs-lookup"><span data-stu-id="0a46d-122">The output includes the URN (the value in the *Urn* column), which you use to specify the image.</span></span> <span data-ttu-id="0a46d-123">使用其中一個常用 Marketplace 映像建立 VM 時，您也可以指定 URN 別名，例如 *UbuntuLTS*。</span><span class="sxs-lookup"><span data-stu-id="0a46d-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify the URN alias, such as *UbuntuLTS*.</span></span>

```
You are viewing an offline list of images, use --all to retrieve an up-to-date list
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
...
```

## <a name="find-specific-images"></a><span data-ttu-id="0a46d-124">尋找特定映像</span><span class="sxs-lookup"><span data-stu-id="0a46d-124">Find specific images</span></span>

<span data-ttu-id="0a46d-125">若要在 Marketplace 中尋找特定 VM 映像，請使用 `az vm image list` 命令搭配 `--all` 選項。</span><span class="sxs-lookup"><span data-stu-id="0a46d-125">To find a specific VM image in the Marketplace, use the `az vm image list` command with the `--all` option.</span></span> <span data-ttu-id="0a46d-126">這個版本的命令需要一些時間才能完成，而且可能會傳回冗長的輸出，因此您通常會依 `--publisher` 或其他參數篩選清單。</span><span class="sxs-lookup"><span data-stu-id="0a46d-126">This version of the command takes some time to complete and can return lengthy output, so you usually filter the list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="0a46d-127">例如，以下命令會顯示所有的 Debian 優惠 (請記住，如果沒有 `--all` 參數，則只會搜尋通用映像的本機快取)：</span><span class="sxs-lookup"><span data-stu-id="0a46d-127">For example, the following command displays all Debian offers (remember that without the `--all` switch, it only searches the local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="0a46d-128">部分輸出：</span><span class="sxs-lookup"><span data-stu-id="0a46d-128">Partial output:</span></span> 
```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  --------------
Debian   credativ     7                  credativ:Debian:7:7.0.201602010                  7.0.201602010
Debian   credativ     7                  credativ:Debian:7:7.0.201603020                  7.0.201603020
Debian   credativ     7                  credativ:Debian:7:7.0.201604050                  7.0.201604050
Debian   credativ     7                  credativ:Debian:7:7.0.201604200                  7.0.201604200
Debian   credativ     7                  credativ:Debian:7:7.0.201606280                  7.0.201606280
Debian   credativ     7                  credativ:Debian:7:7.0.201609120                  7.0.201609120
Debian   credativ     7                  credativ:Debian:7:7.0.201611020                  7.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
Debian   credativ     8                  credativ:Debian:8:8.0.201708040                  8.0.201708040
...
```

<span data-ttu-id="0a46d-129">使用 `--location`、`--publisher` 和 `--sku` 選項套用類似的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="0a46d-129">Apply similar filters with the `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="0a46d-130">您甚至可以執行篩選的部份相符，例如搜尋 `--offer Deb` 以尋找所有 Debian 映像。</span><span class="sxs-lookup"><span data-stu-id="0a46d-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` to find all Debian images.</span></span>

<span data-ttu-id="0a46d-131">如果您未使用 `--location` 選項指定特定的位置，依預設就會傳回 `westus` 的值。</span><span class="sxs-lookup"><span data-stu-id="0a46d-131">If you don't specify a particular location with the `--location` option, the values for `westus` are returned by default.</span></span> <span data-ttu-id="0a46d-132">(執行 `az configure --defaults location=<location>` 以設定不同的預設位置。)</span><span class="sxs-lookup"><span data-stu-id="0a46d-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="0a46d-133">例如，下列命令會列出 `westeurope` 中所有的 Debian 8 個 SKU：</span><span class="sxs-lookup"><span data-stu-id="0a46d-133">For example, the following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="0a46d-134">部分輸出：</span><span class="sxs-lookup"><span data-stu-id="0a46d-134">Partial output:</span></span>

```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  -------------
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
...
```

## <a name="navigate-the-images"></a><span data-ttu-id="0a46d-135">瀏覽映像</span><span class="sxs-lookup"><span data-stu-id="0a46d-135">Navigate the images</span></span> 
<span data-ttu-id="0a46d-136">要在位置中找到映像的另一個方法是在序列中執行 [az vm image list-publishers](/cli/azure/vm/image#list-publishers)、[az vm image list-offers](/cli/azure/vm/image#list-offers) 和 [az vm image list-skus](/cli/azure/vm/image#list-skus) 命令。</span><span class="sxs-lookup"><span data-stu-id="0a46d-136">Another way to find an image in a location is to run the [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="0a46d-137">您可以使用這些命令來判斷下列的值：</span><span class="sxs-lookup"><span data-stu-id="0a46d-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="0a46d-138">列出映像發行者。</span><span class="sxs-lookup"><span data-stu-id="0a46d-138">List the image publishers.</span></span>
2. <span data-ttu-id="0a46d-139">針對指定的發行者，列出其提供項目。</span><span class="sxs-lookup"><span data-stu-id="0a46d-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="0a46d-140">針對指定的提供項目，列出其 SKU。</span><span class="sxs-lookup"><span data-stu-id="0a46d-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="0a46d-141">例如，下列命令會列出美國西部位置中的映像發行者：</span><span class="sxs-lookup"><span data-stu-id="0a46d-141">For example, the following command lists the image publishers in the West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="0a46d-142">部分輸出：</span><span class="sxs-lookup"><span data-stu-id="0a46d-142">Partial output:</span></span>

```
Location    Name
----------  ----------------------------------------------------
westus      1e
westus      4psa
westus      7isolutions
westus      a10networks
westus      abiquo
westus      accellion
westus      Acronis
westus      Acronis.Backup
westus      actian_matrix
westus      actifio
westus      activeeon
westus      adatao
...
```
<span data-ttu-id="0a46d-143">使用這項資訊從特定的發行者尋找優惠。</span><span class="sxs-lookup"><span data-stu-id="0a46d-143">Use this information to find offers from a specific publisher.</span></span> <span data-ttu-id="0a46d-144">例如，如果 Canonical 是美國西部位置的映像發行者，執行 `azure vm image list-offers` 可找到其供應項目。</span><span class="sxs-lookup"><span data-stu-id="0a46d-144">For example, if Canonical is an image publisher in the West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="0a46d-145">傳遞位置和發行者，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="0a46d-145">Pass the location and the publisher as in the following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="0a46d-146">輸出：</span><span class="sxs-lookup"><span data-stu-id="0a46d-146">Output:</span></span>

```
Location    Name
----------  -------------------------
westus      Ubuntu15.04Snappy
westus      Ubuntu15.04SnappyDocker
westus      UbunturollingSnappy
westus      UbuntuServer
westus      Ubuntu_Core
westus      Ubuntu_Snappy_Core
westus      Ubuntu_Snappy_Core_Docker
```
<span data-ttu-id="0a46d-147">您看到在美國西部區域中，Canonical 在 Azure 上發佈 **UbuntuServer** 優惠。</span><span class="sxs-lookup"><span data-stu-id="0a46d-147">You see that in the West US region, Canonical publishes the **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="0a46d-148">但是，是什麼 SKU？</span><span class="sxs-lookup"><span data-stu-id="0a46d-148">But what SKUs?</span></span> <span data-ttu-id="0a46d-149">若要取得這些值，請執行 `azure vm image list-skus`並設定您探索到的位置、發行者和優惠：</span><span class="sxs-lookup"><span data-stu-id="0a46d-149">To get those values, run `azure vm image list-skus` and set the location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="0a46d-150">輸出：</span><span class="sxs-lookup"><span data-stu-id="0a46d-150">Output:</span></span>

```
Location    Name
----------  -----------------
westus      12.04.3-LTS
westus      12.04.4-LTS
westus      12.04.5-DAILY-LTS
westus      12.04.5-LTS
westus      12.10
westus      14.04.0-LTS
westus      14.04.1-LTS
westus      14.04.2-LTS
westus      14.04.3-LTS
westus      14.04.4-LTS
westus      14.04.5-DAILY-LTS
westus      14.04.5-LTS
westus      16.04-beta
westus      16.04-DAILY-LTS
westus      16.04-LTS
westus      16.04.0-LTS
westus      16.10
westus      16.10-DAILY
westus      17.04
westus      17.04-DAILY
westus      17.10-DAILY
```

<span data-ttu-id="0a46d-151">最後，使用 `az vm image list` 命令來尋找您需要的 SKU 特定版本，例如，**16.04-LTS**：</span><span class="sxs-lookup"><span data-stu-id="0a46d-151">Finally, use the `az vm image list` command to find a specific version of the SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="0a46d-152">輸出：</span><span class="sxs-lookup"><span data-stu-id="0a46d-152">Output:</span></span>

```
Offer         Publisher    Sku        Urn                                               Version
------------  -----------  ---------  ------------------------------------------------  ---------------
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611220  16.04.201611220
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611300  16.04.201611300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612050  16.04.201612050
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612140  16.04.201612140
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612210  16.04.201612210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201701130  16.04.201701130
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702020  16.04.201702020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702200  16.04.201702200
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702210  16.04.201702210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702240  16.04.201702240
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703020  16.04.201703020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703030  16.04.201703030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703070  16.04.201703070
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703270  16.04.201703270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703280  16.04.201703280
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703300  16.04.201703300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705080  16.04.201705080
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705160  16.04.201705160
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706100  16.04.201706100
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706191  16.04.201706191
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707210  16.04.201707210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707270  16.04.201707270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708030  16.04.201708030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708110  16.04.201708110
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708151  16.04.201708151
```
## <a name="next-steps"></a><span data-ttu-id="0a46d-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a46d-153">Next steps</span></span>
<span data-ttu-id="0a46d-154">現在，您可以記下 URN 值，精確地選擇想要使用的映像。</span><span class="sxs-lookup"><span data-stu-id="0a46d-154">Now you can choose precisely the image you want to use by taking note of the URN value.</span></span> <span data-ttu-id="0a46d-155">當您使用 [az vm create](/cli/azure/vm#create) 命令建立 VM 時，請傳遞此值與 `--image` 參數。</span><span class="sxs-lookup"><span data-stu-id="0a46d-155">Pass this value with the `--image` parameter when you create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="0a46d-156">請記住，您可以使用 "latest" 來取代 URN 中的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="0a46d-156">Remember that you can optionally replace the version number in the URN with "latest".</span></span> <span data-ttu-id="0a46d-157">此版本一律為發佈的最新版本。</span><span class="sxs-lookup"><span data-stu-id="0a46d-157">This version is always the latest version of the distribution.</span></span> <span data-ttu-id="0a46d-158">若要使用 URN 資訊來快速建立虛擬機器，請參閱[使用 Azure CLI 來建立和管理 Linux VM](tutorial-manage-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="0a46d-158">To create a virtual machine quickly by using the URN information, see [Create and Manage Linux VMs with the Azure CLI](tutorial-manage-vm.md).</span></span>
