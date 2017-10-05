---
title: "Azure Linux 虛擬機器指導方針 | Microsoft Docs"
description: "了解將 Linux 虛擬機器部署到 Azure 中的關鍵設計和實作指導方針"
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 740767d7-9a40-407b-93e7-c29dd976ffd7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.openlocfilehash: 2d886795b301ab79272cae10a53831fd44c18f10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-virtual-machines-guidelines-for-linux"></a>適用於 Linux 的 Azure 虛擬機器指導方針
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

本文著重於了解在 Azure 環境內建立及管理虛擬機器 (VM) 的必要計畫步驟。

## <a name="implementation-guidelines-for-vms"></a>VM 的實作指導方針
决策：

* 您針對各種應用程式層級和基礎結構元件將需要多少 VM？
* 每個 VM 需要什麼 CPU 和記憶體資源？而儲存體需求為何？

工作：

* 定義應用程式的工作負載，以及 VM 所需的資源。
* 以適當的 VM 大小和儲存體類型，對齊每個 VM 的資源需求。
* 針對基礎結構的不同層級和元件定義您的資源群組。
* 定義您的 VM 命名慣例。
* 使用 Azure CLI、入口網站，或 Resource Manager 範本建立 VM。

## <a name="virtual-machines"></a>虛擬機器
您 Azure 環境內的其中一個主要資源很可能是 VM。 這個資源是您執行應用程式、資料庫、驗證服務等項目的位置。

請務必了解 [不同的 VM 大小](sizes.md) ，以根據效能和成本觀點正確評估您環境的大小。 如果您的 VM 沒有足夠的 CPU 核心數或記憶體，無論您的應用程式設計及開發得多好，它的效能都會受到影響。 做為開始，請檢閱每個 VM 系列的建議工作負載，並決定在基礎結構中要用於每個元件的 VM 大小。 您可以在部署後 [變更 VM 的大小](change-vm-size.md) 。

儲存體在 VM 效能中扮演重要的角色。 您可以選擇使用一般旋轉磁碟的標準儲存體，或是選擇使用 SSD 磁碟的進階儲存體，以取得高 I/O 工作負載和尖端效能。 針對 VM 大小，有一些選取儲存媒體的成本考量。 您可以閱讀 [storage infrastructure guidelines (儲存體基礎結構指導方針) 一文](infrastructure-storage-solutions-guidelines.md) ，以了解針對 VM 的最佳效能設計適當儲存體的方式。

## <a name="resource-groups"></a>資源群組
VM 之類的元件會以邏輯方式分組，以方便使用 [Azure 資源群組](../../azure-resource-manager/resource-group-overview.md)進行管理和維護。 透過使用資源群組，您可以建立、管理並監視組成特定應用程式的所有資源。 您也可以實作 [角色型存取控制](../../active-directory/role-based-access-control-what-is.md) ，以授與小組中的其他人員存取所需資源的權限。 請花上一點時間計畫您的資源群組和角色指派。 實際設計並實作資源群組有數個不同的方式，因此請務必閱讀 [資源群組指導方針一文](infrastructure-resource-groups-guidelines.md) ，以了解建置 VM 的最佳做法。

## <a name="templates"></a>範本
您可以建置範本 (由宣告式 JSON 檔案定義) 以建立您的 VM。 範本除了 VM 之外，通常也會建置必要的儲存體、網路、網路介面、IP 位址等。 您可以針對開發和測試目的使用範本來建立一致且可重現的環境，以輕鬆複寫生產環境，反之亦然。 您可以深入了解[建置並使用範本](../../azure-resource-manager/resource-group-overview.md#template-deployment)，以了解將它們用於建立及部署 VM 的方式。

## <a name="next-steps"></a>後續步驟
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

