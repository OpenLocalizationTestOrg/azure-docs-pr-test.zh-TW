---
title: "aaaSelect Linux VM 映像以 hello Azure CLI |Microsoft 文件"
description: "了解如何 toouse hello Azure CLI toodetermine hello 發行者、 方案、 SKU 和 Marketplace 的 VM 映像的版本。"
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
ms.openlocfilehash: 0b115b8654bc156b5bfadba53a6b002a105acb68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a><span data-ttu-id="3e082-103">Toofind Linux VM 以 hello Azure CLI hello Azure Marketplace 中的映像</span><span class="sxs-lookup"><span data-stu-id="3e082-103">How toofind Linux VM images in hello Azure Marketplace with hello Azure CLI</span></span>
<span data-ttu-id="3e082-104">本主題描述如何 toouse hello hello Azure Marketplace 中的 Azure CLI 2.0 toofind VM 映像。</span><span class="sxs-lookup"><span data-stu-id="3e082-104">This topic describes how toouse hello Azure CLI 2.0 toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="3e082-105">當您建立 Linux VM，請使用此資訊 toospecify Marketplace 映像。</span><span class="sxs-lookup"><span data-stu-id="3e082-105">Use this information toospecify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="3e082-106">請確定最新安裝 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)和登入 Azure 帳戶 tooan (`az login`)。</span><span class="sxs-lookup"><span data-stu-id="3e082-106">Make sure that you installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in tooan Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="3e082-107">術語</span><span class="sxs-lookup"><span data-stu-id="3e082-107">Terminology</span></span>

<span data-ttu-id="3e082-108">Hello CLI 和其他 Azure 工具根據 tooa 階層中識別 marketplace 映像：</span><span class="sxs-lookup"><span data-stu-id="3e082-108">Marketplace images are identified in hello CLI and other Azure tools according tooa hierarchy:</span></span>

* <span data-ttu-id="3e082-109">**發行者**-hello 建立 hello 映像的組織。</span><span class="sxs-lookup"><span data-stu-id="3e082-109">**Publisher** - hello organization that created hello image.</span></span> <span data-ttu-id="3e082-110">範例：Canonical</span><span class="sxs-lookup"><span data-stu-id="3e082-110">Example: Canonical</span></span>
* <span data-ttu-id="3e082-111">**供應項目** - 發行者所建立的一組相關映像。</span><span class="sxs-lookup"><span data-stu-id="3e082-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="3e082-112">範例：Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="3e082-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="3e082-113">**SKU** - 供應項目執行個體，例如發佈的主要版本。</span><span class="sxs-lookup"><span data-stu-id="3e082-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="3e082-114">範例：16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="3e082-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="3e082-115">**版本**-hello SKU 的映像的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="3e082-115">**Version** - hello version number of an image SKU.</span></span> <span data-ttu-id="3e082-116">當指定 hello 映像，您可以取代 hello 版本號碼與 「 最新 」，以選取 hello hello 分配的最新的版本。</span><span class="sxs-lookup"><span data-stu-id="3e082-116">When specifying hello image, you can replace hello version number with "latest", which selects hello latest version of hello distribution.</span></span>

<span data-ttu-id="3e082-117">toospecify Marketplace 映像，您通常使用 hello 映像*URN*。</span><span class="sxs-lookup"><span data-stu-id="3e082-117">toospecify a Marketplace image, you typically use hello image *URN*.</span></span> <span data-ttu-id="3e082-118">hello URN 結合這些值，以 hello 冒號 （:） 字元分隔：*發行者*:*提供*:*Sku*:*版本*。</span><span class="sxs-lookup"><span data-stu-id="3e082-118">hello URN combines these values, separated by hello colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="3e082-119">列出常用的映像</span><span class="sxs-lookup"><span data-stu-id="3e082-119">List popular images</span></span>

<span data-ttu-id="3e082-120">執行 hello [az vm 映像清單](/cli/azure/vm/image#list)命令，hello`--all`選項、 toosee hello Azure Marketplace 中的一份受歡迎的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="3e082-120">Run hello [az vm image list](/cli/azure/vm/image#list) command, without hello `--all` option, toosee a list of popular VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="3e082-121">比方說，執行下列命令 toodisplay hello 受歡迎的映像快取的清單以資料表格式：</span><span class="sxs-lookup"><span data-stu-id="3e082-121">For example, run hello following command toodisplay a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="3e082-122">hello 輸出包含 hello URN (hello 中 hello 值*Urn*資料行)，而您使用 toospecify hello 映像。</span><span class="sxs-lookup"><span data-stu-id="3e082-122">hello output includes hello URN (hello value in hello *Urn* column), which you use toospecify hello image.</span></span> <span data-ttu-id="3e082-123">當與其中一個這些常用的 Marketplace 映像建立 VM，您也可以指定 hello URN 別名，例如*UbuntuLTS*。</span><span class="sxs-lookup"><span data-stu-id="3e082-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify hello URN alias, such as *UbuntuLTS*.</span></span>

```
You are viewing an offline list of images, use --all tooretrieve an up-to-date list
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

## <a name="find-specific-images"></a><span data-ttu-id="3e082-124">尋找特定映像</span><span class="sxs-lookup"><span data-stu-id="3e082-124">Find specific images</span></span>

<span data-ttu-id="3e082-125">toofind hello 服務商場中的特定 VM 映像使用 hello`az vm image list`命令與 hello`--all`選項。</span><span class="sxs-lookup"><span data-stu-id="3e082-125">toofind a specific VM image in hello Marketplace, use hello `az vm image list` command with hello `--all` option.</span></span> <span data-ttu-id="3e082-126">這個版本 hello 命令需要一些時間 toocomplete，可傳回的冗長輸出，因此您通常 hello 依篩選清單`--publisher`或另一個參數。</span><span class="sxs-lookup"><span data-stu-id="3e082-126">This version of hello command takes some time toocomplete and can return lengthy output, so you usually filter hello list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="3e082-127">例如，下列命令的 hello 會顯示所有 Debian 優惠 (請記住，沒有 hello`--all`切換時，它只會搜尋 hello 的通用映像的本機快取):</span><span class="sxs-lookup"><span data-stu-id="3e082-127">For example, hello following command displays all Debian offers (remember that without hello `--all` switch, it only searches hello local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="3e082-128">部分輸出：</span><span class="sxs-lookup"><span data-stu-id="3e082-128">Partial output:</span></span> 
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

<span data-ttu-id="3e082-129">套用類似的篩選器以 hello `--location`， `--publisher`，和`--sku`選項。</span><span class="sxs-lookup"><span data-stu-id="3e082-129">Apply similar filters with hello `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="3e082-130">您甚至可以執行部分相符的篩選，例如搜尋`--offer Deb`toofind 所有 Debian 映像。</span><span class="sxs-lookup"><span data-stu-id="3e082-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` toofind all Debian images.</span></span>

<span data-ttu-id="3e082-131">如果您未指定特定位置以 hello `--location` ，hello 的選項值`westus`依預設會傳回。</span><span class="sxs-lookup"><span data-stu-id="3e082-131">If you don't specify a particular location with hello `--location` option, hello values for `westus` are returned by default.</span></span> <span data-ttu-id="3e082-132">(執行 `az configure --defaults location=<location>` 以設定不同的預設位置。)</span><span class="sxs-lookup"><span data-stu-id="3e082-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="3e082-133">例如，下列命令的 hello 列出 Debian 8 中所有的 Sku `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="3e082-133">For example, hello following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="3e082-134">部分輸出：</span><span class="sxs-lookup"><span data-stu-id="3e082-134">Partial output:</span></span>

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

## <a name="navigate-hello-images"></a><span data-ttu-id="3e082-135">瀏覽 hello 映像</span><span class="sxs-lookup"><span data-stu-id="3e082-135">Navigate hello images</span></span> 
<span data-ttu-id="3e082-136">另一個方式 toofind 位置中的映像為 toorun hello [az vm 映像清單發行者](/cli/azure/vm/image#list-publishers)， [az vm 映像清單優惠](/cli/azure/vm/image#list-offers)，和[az vm 映像清單 sku](/cli/azure/vm/image#list-skus)序列中的命令。</span><span class="sxs-lookup"><span data-stu-id="3e082-136">Another way toofind an image in a location is toorun hello [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="3e082-137">您可以使用這些命令來判斷下列的值：</span><span class="sxs-lookup"><span data-stu-id="3e082-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="3e082-138">清單 hello 映像的發行者。</span><span class="sxs-lookup"><span data-stu-id="3e082-138">List hello image publishers.</span></span>
2. <span data-ttu-id="3e082-139">針對指定的發行者，列出其提供項目。</span><span class="sxs-lookup"><span data-stu-id="3e082-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="3e082-140">針對指定的提供項目，列出其 SKU。</span><span class="sxs-lookup"><span data-stu-id="3e082-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="3e082-141">例如，hello 下列命令會列出 hello 美國西部位置中的 hello 映像發行者：</span><span class="sxs-lookup"><span data-stu-id="3e082-141">For example, hello following command lists hello image publishers in hello West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="3e082-142">部分輸出：</span><span class="sxs-lookup"><span data-stu-id="3e082-142">Partial output:</span></span>

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
<span data-ttu-id="3e082-143">使用此資訊 toofind 提供從特定的發行者。</span><span class="sxs-lookup"><span data-stu-id="3e082-143">Use this information toofind offers from a specific publisher.</span></span> <span data-ttu-id="3e082-144">比方說，如果 Canonical hello 美國西部位置中的映像 「 發行者 」，其提供執行尋找`azure vm image list-offers`。</span><span class="sxs-lookup"><span data-stu-id="3e082-144">For example, if Canonical is an image publisher in hello West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="3e082-145">傳遞 hello 位置和 hello 發行者如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="3e082-145">Pass hello location and hello publisher as in hello following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="3e082-146">輸出：</span><span class="sxs-lookup"><span data-stu-id="3e082-146">Output:</span></span>

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
<span data-ttu-id="3e082-147">您會看到 hello 美國西部地區 Canonical 發行 hello **UbuntuServer**提供在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="3e082-147">You see that in hello West US region, Canonical publishes hello **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="3e082-148">但哪些 Sku 嗎？tooget 這些值，請執行`azure vm image list-skus`並設定 hello 位置、 發行者和已探索到的供應項目：</span><span class="sxs-lookup"><span data-stu-id="3e082-148">But what SKUs? tooget those values, run `azure vm image list-skus` and set hello location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="3e082-149">輸出：</span><span class="sxs-lookup"><span data-stu-id="3e082-149">Output:</span></span>

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

<span data-ttu-id="3e082-150">最後，使用 hello`az vm image list`命令 toofind 特定版本的 hello SKU 想，比方說， **16.04 LTS**:</span><span class="sxs-lookup"><span data-stu-id="3e082-150">Finally, use hello `az vm image list` command toofind a specific version of hello SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="3e082-151">輸出：</span><span class="sxs-lookup"><span data-stu-id="3e082-151">Output:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="3e082-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3e082-152">Next steps</span></span>
<span data-ttu-id="3e082-153">現在您可以選擇明確地說 hello 影像 toouse 所要採取的附註的 hello URN 值。</span><span class="sxs-lookup"><span data-stu-id="3e082-153">Now you can choose precisely hello image you want toouse by taking note of hello URN value.</span></span> <span data-ttu-id="3e082-154">將此值以 hello 傳遞`--image`參數，當您建立 VM 以 hello [az vm 建立](/cli/azure/vm#create)命令。</span><span class="sxs-lookup"><span data-stu-id="3e082-154">Pass this value with hello `--image` parameter when you create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="3e082-155">請記住，您可以使用 「 最新 」，選擇性地取代 hello hello URN 中的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="3e082-155">Remember that you can optionally replace hello version number in hello URN with "latest".</span></span> <span data-ttu-id="3e082-156">此版本一律為 hello hello 分配的最新的版本。</span><span class="sxs-lookup"><span data-stu-id="3e082-156">This version is always hello latest version of hello distribution.</span></span> <span data-ttu-id="3e082-157">toocreate 虛擬機器，快速利用 hello URN 的詳細資訊，請參閱[建立和管理 Linux Vm 以 hello Azure CLI](tutorial-manage-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="3e082-157">toocreate a virtual machine quickly by using hello URN information, see [Create and Manage Linux VMs with hello Azure CLI](tutorial-manage-vm.md).</span></span>
