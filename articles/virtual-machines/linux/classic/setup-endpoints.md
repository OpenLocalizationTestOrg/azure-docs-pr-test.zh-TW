---
title: "個傳統的 Linux VM 上端點的 aaaSet |Microsoft 文件"
description: "針對 Linux VM 在 Azure 傳統入口網站 tooallow 通訊 hello 與 Azure 中 Linux 虛擬機器學習 tooset 個端點"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a>如何 tooset 向上 Linux 傳統 Azure 中虛擬機器上的端點
您在 Azure 中使用 hello 傳統部署模型中建立的所有 Linux 虛擬機器可以自動透過都通訊與 hello 中其他虛擬機器的私人網路通道相同雲端服務或虛擬網路。 不過，在 hello 網際網路或其他虛擬網路上的電腦需要端點 toodirect hello 輸入的網路流量 tooa 虛擬機器。 本文也適用於 [Windows 虛擬機器](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

在 hello**資源管理員**部署模型，使用已設定端點**網路安全性群組 (Nsg)**。 如需詳細資訊，請參閱[開啟連接埠和端點](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

當您建立 Linux 虛擬機器在 hello Azure 入口網站中時，端點的安全殼層 (SSH) 是通常為您自動建立。 視需要建立 hello 虛擬機器時或之後，您可以設定其他端點。

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>後續步驟
* 您也可以建立的 VM 端點使用 hello [Azure 命令列介面](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。 執行 hello **azure vm 端點，請建立**命令。
* 如果在 hello Resource Manager 部署模型中建立虛擬機器，您也可以使用資源管理員模式中的 hello Azure CLI[建立網路安全性群組](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md)toocontrol 流量 toohello VM。
