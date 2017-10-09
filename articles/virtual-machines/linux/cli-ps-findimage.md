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
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a>Toofind Linux VM 以 hello Azure CLI hello Azure Marketplace 中的映像
本主題描述如何 toouse hello hello Azure Marketplace 中的 Azure CLI 2.0 toofind VM 映像。 當您建立 Linux VM，請使用此資訊 toospecify Marketplace 映像。

請確定最新安裝 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)和登入 Azure 帳戶 tooan (`az login`)。

## <a name="terminology"></a>術語

Hello CLI 和其他 Azure 工具根據 tooa 階層中識別 marketplace 映像：

* **發行者**-hello 建立 hello 映像的組織。 範例：Canonical
* **供應項目** - 發行者所建立的一組相關映像。 範例：Ubuntu Server
* **SKU** - 供應項目執行個體，例如發佈的主要版本。 範例：16.04-LTS
* **版本**-hello SKU 的映像的版本號碼。 當指定 hello 映像，您可以取代 hello 版本號碼與 「 最新 」，以選取 hello hello 分配的最新的版本。

toospecify Marketplace 映像，您通常使用 hello 映像*URN*。 hello URN 結合這些值，以 hello 冒號 （:） 字元分隔：*發行者*:*提供*:*Sku*:*版本*。 


## <a name="list-popular-images"></a>列出常用的映像

執行 hello [az vm 映像清單](/cli/azure/vm/image#list)命令，hello`--all`選項、 toosee hello Azure Marketplace 中的一份受歡迎的 VM 映像。 比方說，執行下列命令 toodisplay hello 受歡迎的映像快取的清單以資料表格式：

```azurecli
az vm image list --output table
```

hello 輸出包含 hello URN (hello 中 hello 值*Urn*資料行)，而您使用 toospecify hello 映像。 當與其中一個這些常用的 Marketplace 映像建立 VM，您也可以指定 hello URN 別名，例如*UbuntuLTS*。

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

## <a name="find-specific-images"></a>尋找特定映像

toofind hello 服務商場中的特定 VM 映像使用 hello`az vm image list`命令與 hello`--all`選項。 這個版本 hello 命令需要一些時間 toocomplete，可傳回的冗長輸出，因此您通常 hello 依篩選清單`--publisher`或另一個參數。 

例如，下列命令的 hello 會顯示所有 Debian 優惠 (請記住，沒有 hello`--all`切換時，它只會搜尋 hello 的通用映像的本機快取):

```azurecli
az vm image list --offer Debian --all --output table 

```

部分輸出： 
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

套用類似的篩選器以 hello `--location`， `--publisher`，和`--sku`選項。 您甚至可以執行部分相符的篩選，例如搜尋`--offer Deb`toofind 所有 Debian 映像。

如果您未指定特定位置以 hello `--location` ，hello 的選項值`westus`依預設會傳回。 (執行 `az configure --defaults location=<location>` 以設定不同的預設位置。)

例如，下列命令的 hello 列出 Debian 8 中所有的 Sku `westeurope`:

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

部分輸出：

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

## <a name="navigate-hello-images"></a>瀏覽 hello 映像 
另一個方式 toofind 位置中的映像為 toorun hello [az vm 映像清單發行者](/cli/azure/vm/image#list-publishers)， [az vm 映像清單優惠](/cli/azure/vm/image#list-offers)，和[az vm 映像清單 sku](/cli/azure/vm/image#list-skus)序列中的命令。 您可以使用這些命令來判斷下列的值：

1. 清單 hello 映像的發行者。
2. 針對指定的發行者，列出其提供項目。
3. 針對指定的提供項目，列出其 SKU。


例如，hello 下列命令會列出 hello 美國西部位置中的 hello 映像發行者：

```azurecli
az vm image list-publishers --location westus --output table
```

部分輸出：

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
使用此資訊 toofind 提供從特定的發行者。 比方說，如果 Canonical hello 美國西部位置中的映像 「 發行者 」，其提供執行尋找`azure vm image list-offers`。 傳遞 hello 位置和 hello 發行者如 hello 下列範例所示：

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

輸出：

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
您會看到 hello 美國西部地區 Canonical 發行 hello **UbuntuServer**提供在 Azure 上。 但哪些 Sku 嗎？tooget 這些值，請執行`azure vm image list-skus`並設定 hello 位置、 發行者和已探索到的供應項目：

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

輸出：

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

最後，使用 hello`az vm image list`命令 toofind 特定版本的 hello SKU 想，比方說， **16.04 LTS**:

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

輸出：

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
## <a name="next-steps"></a>後續步驟
現在您可以選擇明確地說 hello 影像 toouse 所要採取的附註的 hello URN 值。 將此值以 hello 傳遞`--image`參數，當您建立 VM 以 hello [az vm 建立](/cli/azure/vm#create)命令。 請記住，您可以使用 「 最新 」，選擇性地取代 hello hello URN 中的版本號碼。 此版本一律為 hello hello 分配的最新的版本。 toocreate 虛擬機器，快速利用 hello URN 的詳細資訊，請參閱[建立和管理 Linux Vm 以 hello Azure CLI](tutorial-manage-vm.md)。
