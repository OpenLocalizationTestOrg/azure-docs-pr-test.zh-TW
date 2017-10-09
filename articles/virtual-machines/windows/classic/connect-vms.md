---
title: "雲端服務中的 Windows Vm aaaConnect |Microsoft 文件"
description: "Windows 虛擬機器以 hello 傳統部署模型 tooan Azure 雲端服務或虛擬網路建立連接。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c1cbc802-4352-4d2e-9e49-4ccbd955324b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: d19dc555694eab8a7e790c970cfb5e6a53aa7a7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-virtual-machines-created-with-hello-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a>使用與虛擬網路或雲端服務的 hello 傳統部署模型建立的 Windows 虛擬機器連線
> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

一定會與 hello 傳統部署模型所建立的 Windows 虛擬機器放置在雲端服務。 hello 雲端服務做為容器，並透過 hello 網際網路提供唯一的公開 DNS 名稱、 公用 IP 位址，以及一組端點 tooaccess hello 虛擬機器。 hello 雲端服務是在虛擬網路中，但並非必要條件。 您也可以 [透過虛擬網路或雲端服務來連線 Linux 虛擬機器](../../linux/classic/connect-vms.md)。

如果雲端服務不在虛擬網路中，就稱為 *獨立* 雲端服務。 hello 獨立雲端服務中的虛擬機器與其他虛擬機器使用通訊 hello 其他虛擬機器的公用 DNS 名稱，和 hello 流量，透過網際網路 hello。 如果雲端服務是虛擬網路，hello 虛擬機器，雲端服務可以與 hello 虛擬網路中的所有其他虛擬機器沒有任何流量傳送 hello 網際網路上通訊。

如果您將您的虛擬機器中的 hello 相同獨立雲端服務，您仍然可以使用負載平衡和可用性設定組。 如需詳細資訊，請參閱[負載平衡虛擬機器](../../virtual-machines-windows-load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)和[管理虛擬機器可用性 hello](../../virtual-machines-windows-manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 不過，您無法組織 hello 子網路上的虛擬機器，或將獨立雲端服務 tooyour 在內部部署網路連線。 以下是範例：

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a>後續步驟
建立虛擬機器之後，就是個好主意太[新增資料磁碟](attach-disk.md)讓您的服務和工作負載有位置 toostore 資料。
