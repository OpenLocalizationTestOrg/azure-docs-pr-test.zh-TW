---
title: "aaaHow tooresize Linux VM 以 hello Azure CLI 1.0 |Microsoft 文件"
description: "如何 tooscale 向上或向下 Linux 虛擬機器，藉由變更調整 hello VM 大小。"
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a>使用 Azure CLI 1.0 來調整 Linux VM 大小

## <a name="overview"></a>概觀

佈建虛擬機器 (VM) 之後，您可以調整 hello VM 向上或向下藉由變更 hello [VM 大小][vm-sizes]。 在某些情況下，您必須先取消配置 hello VM。 這種情況 hello 新大小不是在裝載 hello VM hello 硬體叢集上使用。

本文將說明如何使用 hello Linux VM 的 tooresize [Azure CLI][azure-cli]。

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- [Azure CLI 1.0](#resize-a-linux-vm) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI


## <a name="resize-a-linux-vm"></a>重新調整 Linux VM 的大小
tooresize VM，執行下列步驟的 hello。

1. 執行下列 CLI 命令的 hello。 此命令會列出 hello hello hello VM 所在的硬體叢集可用的 VM 大小。
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. 如果 hello 需要列出大小，請執行下列命令 tooresize hello VM hello。
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    hello VM 會重新啟動此程序期間。 Hello 重新啟動之後，您現有的作業系統和資料磁碟將會重新對應。 Hello 暫存磁碟的任何項目將會遺失。
   
    使用 hello`--enable-boot-diagnostics`選項可讓[開機診斷][boot-diagnostics]，toolog 任何錯誤的相關的 toostartup。
3. 否則，視 hello 大小未列出，執行下列命令 toodeallocate hello VM、 調整其大小，然後再重新啟動 hello VM hello。
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > 解除配置 hello VM 也會釋放指派 toohello VM 的任何動態 IP 位址。 不會影響 hello OS 和資料磁碟。
   > 
   > 

## <a name="next-steps"></a>後續步驟
如需提高延展性，可執行多個 VM 執行個體並相應放大。如需詳細資訊，請參閱[在虛擬機器擴展集中自動調整 Linux 機器][scale-set]。 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
