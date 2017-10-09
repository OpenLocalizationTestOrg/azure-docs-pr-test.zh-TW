---
title: "適用於 Windows Vm 在 Azure 中保留維護 aaaVM |Microsoft 文件"
description: "針對記憶體保留更新的就地 VM 移轉。"
services: virtual-machines-windows
documentationcenter: 
author: 
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: 
ms.openlocfilehash: 544a2dcca52bb3ac51d341bceaf4ba3e7c71fd82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vm-preserving-maintenance-in-place-vm-migration"></a>VM 保留維護 (就地 VM 移轉)

雖然 hello 的大部分更新不有任何影響 toohosted Vm，有些情況是其中更新 toocomponents 或服務會導致最少的干擾 toorunning Vm （不含 hello 虛擬機器的完整重新開機）。

這些更新是透過可進行就地即時移轉 (也稱為「記憶體保留更新」) 的技術來完成。 在更新 hello 主機時，hello 虛擬機器被放入 「 暫停 」 狀態，雖然 hello 必要更新和修補程式，適用於裝載環境 （例如基礎作業系統） 的 hello 保留在 RAM 而 hello 記憶體。
然後在暫停的 30 秒內繼續 hello 虛擬機器。
繼續之後, hello hello 虛擬機器的時鐘會自動同步處理。

並非所有的更新可以使用這項機制，來部署，但在短暫的延遲期間，指定部署更新，在此方式可大幅減少影響 toovirtual 機器。

多重執行個體更新 (可用性設定組中的 VM) 一次只會套用到一個更新網域。

這些更新對某些應用程式的影響可能比對其他應用程式更大。 應用程式執行即時事件處理、 媒體串流處理或轉碼或高輸送量網路案例，例如，可能無法設計的 tootolerate 暫停 30 秒。 虛擬機器中執行的應用程式可以了解即將推出的更新呼叫 hello[排程的事件](../virtual-machines-scheduled-events.md)API 的 hello [Azure 中繼資料服務](../virtual-machines-instancemetadataservice-overview.md)。
