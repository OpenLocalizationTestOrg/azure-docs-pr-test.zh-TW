---
title: "設定端點傳統 Windows VM 上 aaaSet |Microsoft 文件"
description: "針對 Windows VM 在 Azure 傳統入口網站 tooallow 通訊 hello 與 Windows Azure 中虛擬機器學習 tooset 個端點。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a>如何 tooset 個在 Azure 中的傳統 Windows 虛擬機器上的端點
您在 Azure 中使用 hello 傳統部署模型中建立的虛擬機器可以透過與在其他虛擬機器的私人網路通道自動進行通訊的所有 Windows 都 hello 相同雲端服務或虛擬網路。 不過，在 hello 網際網路或其他虛擬網路上的電腦需要端點 toodirect hello 輸入的網路流量 tooa 虛擬機器。 本文也適用於 [Linux 虛擬機器](../../linux/classic/setup-endpoints.md)。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

在 hello**資源管理員**部署模型，使用已設定端點**網路安全性群組 (Nsg)**。 如需詳細資訊，請參閱[允許外部存取 tooyour VM 使用 hello Azure 入口網站](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

當您建立 Windows 虛擬機器在 hello Azure 入口網站中時，遠端桌面和 Windows PowerShell 遠端執行功能一樣的一般端點會通常為您自動建立。 視需要建立 hello 虛擬機器時或之後，您可以設定其他端點。

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>後續步驟
* toouse Azure PowerShell cmdlet tooset，VM 端點，請參閱[Add-azureendpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx)。
* toouse Azure PowerShell cmdlet toomanage ACL 的端點，請參閱[管理存取控制清單 (Acl) 端點使用 PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md)。
* 如果在 hello Resource Manager 部署模型中建立虛擬機器，您也可以使用 Azure PowerShell[建立網路安全性群組](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md)toocontrol 流量 toohello VM。
