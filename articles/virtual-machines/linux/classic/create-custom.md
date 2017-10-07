---
title: "傳統 Linux VM，使用 aaaCreate hello Azure CLI 1.0 |Microsoft 文件"
description: "了解如何 toocreate Linux 虛擬機器使用 Azure CLI 1.0 hello hello 傳統部署模型"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a>與傳統 Linux VM 的 tooCreate hello Azure CLI 1.0 的方式
> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 Hello 資源管理員版本，請參閱[這裡](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

本主題描述如何 toocreate Linux 虛擬機器 (VM) 與使用 Azure CLI 1.0 hello hello 傳統部署模型。 我們使用 Linux 映像，從可用的 hello**映像**在 Azure 上。 hello Azure CLI 1.0，提供下列設定選項，和其他項目 hello:

* Hello VM tooa 虛擬網路連線
* 加入 hello VM tooan 現有雲端服務
* 新增 hello VM tooan 現有儲存體帳戶
* 新增 hello VM tooan 可用性設定組或位置

> [!IMPORTANT]
> 如果您希望您 VM toouse 虛擬網路，讓您能連接 tooit 直接以主機名稱或設定跨單位連線，請確定您在建立 hello VM 時指定 hello 虛擬網路。 只有在您建立 hello VM 時，VM 可能會設定的 toojoin 虛擬網路。 如需虛擬網路的詳細資訊，請參閱 [Azure 虛擬網路概觀](http://go.microsoft.com/fwlink/p/?LinkID=294063)。
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a>如何使用 Linux VM 的 toocreate hello 傳統部署模型
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

