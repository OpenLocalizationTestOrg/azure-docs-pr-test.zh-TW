---
title: "aaaHow tootag Azure Linux 虛擬機器 |Microsoft 文件"
description: "深入了解標記使用 hello Resource Manager 部署模型在 Azure 中建立的 Azure Linux 虛擬機器。"
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: 0e99ea66a87b7e00eb21a2f72dd2bce8673778dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a>如何在 Azure 中 Linux 虛擬機器 tootag
本文說明不同的方式 tootag Azure 中 Linux 虛擬機器，透過 hello Resource Manager 部署模型。 標記是使用者定義的成對「索引鍵/值」，可直接置於資源或資源群組。 Azure 目前支援向上 too15 標記每個資源與資源群組。 標籤可能會放在資源上建立 hello 時，或加入 tooan 現有的資源。 請注意，支援透過 hello Resource Manager 部署模型只能建立資源標記。

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a>透過 Azure CLI 進行標記
toobegin，[安裝及設定 hello Azure CLI](../../xplat-cli-azure-resource-manager.md) ，並確定您是在 Resource Manager 模式 (`azure config mode arm`)。

您可以檢視所有屬性指定的虛擬機器，包括 hello 標記，請使用此命令：

        azure vm show -g MyResourceGroup -n MyTestVM

tooadd hello Azure CLI 透過新的 VM 標記，您可以使用 hello`azure vm set`命令以及 hello 標記參數**-t**:

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

tooremove 所有標記，您可以使用 hello **– T**中 hello 參數`azure vm set`命令。

        azure vm set – g MyResourceGroup –n MyTestVM -T


現在，我們已套用標籤 tooour 資源 Azure CLI，並 hello 入口網站，讓我們看看 hello 使用量詳細資料 toosee hello 標記 hello 計費入口網站中。

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>後續步驟
* toolearn 深入了解標記您的 Azure 資源，請參閱[Azure 資源管理員概觀][ Azure Resource Manager Overview]和[使用標記 tooorganize Azure 資源][ Using Tags tooorganize your Azure Resources].
* toosee 如何標記可以協助您管理您使用的 Azure 資源，請參閱[了解您的 Azure 帳單][ Understanding your Azure Bill]和[深入了解您的 Microsoft Azure 資源耗用量][Gain insights into your Microsoft Azure resource consumption].

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
