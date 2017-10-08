---
title: "aaaView 公用 IP 位址消耗 Azure 堆疊 |Microsoft 文件"
description: "系統管理員可以檢視區域中的 hello 耗用量的公用 IP 位址"
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: darmour
editor: 
ms.assetid: 0f77be49-eafe-4886-8c58-a17061e8120f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/18/2017
ms.author: scottnap
ms.openlocfilehash: 771c011d133a030218b011cf94bbb8055f8996ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-public-ip-address-consumption-in-azure-stack"></a>檢視 Azure Stack 中的公用 IP 位址使用
是雲端系統管理員，您可以檢視 hello tootenants hello 仍然可供配置的公用 IP 位址的數目和中的已配置的公用 IP 位址的 hello 百分比已配置的公用 IP 位址數目位置。

hello**公用 IP 集區使用量**磚會顯示 hello 總數已取用所有公用的 IP 位址集區，在 hello 光纖上的公用 IP 位址是否已用過的租用戶 IaaS VM 執行個體，網狀架構基礎結構服務或所明確建立的租用戶的公用 IP 位址資源。

hello 這個磚的目的是 toogive Azure 堆疊 administrators 的 hello 已耗用在這個位置的公用 IP 位址的總次數。 這可協助系統管理員判斷其是否即將耗盡此資源。

在 hello**資源提供者**，**網路**刀鋒視窗，hello**公用 IP 位址**下的功能表項目**租用戶資源**只列出公用 IP 位址已*明確建立租用戶*。 因此，hello 數目**用於**hello 上的公用 IP 位址**公用 IP 集區使用量**磚永遠是不同 （大於） hello hello 上的數字**公用 IP 位址**下圖格**租用戶資源**。

## <a name="view-hello-public-ip-address-usage-information"></a>檢視 hello 公用 IP 位址使用狀況資訊
tooview hello 的總數已取用 hello 區域中的公用 IP 位址：

1. 在 hello Azure 堆疊管理員入口網站，按一下 **更多服務**下**管理資源**，按一下**資源提供者**。
2. 從 hello 清單**資源提供者**，選取**網路**。
3. hello**網路**刀鋒視窗會顯示 hello**公用 IP 集區使用量**磚中 hello**概觀**> 一節。

![網路資源提供者刀鋒視窗](media/azure-stack-viewing-public-ip-address-consumption/image01.png)

請記住該 hello**用於**數字代表 hello 的公用 IP 位址數目，從所有公用 IP 位址集區的位置指派。 hello**免費**數字代表 hello 的所有公用 IP 位址集區未指派，而且仍然可以使用從公用 IP 位址數目。 hello **%used**數字代表 hello 數目，使用或指派位址的所有公用的 IP 位址集區，在該位置中的公用 IP 位址的 hello 總數的百分比。

## <a name="view-hello-public-ip-addresses-that-were-created-by-tenant-subscriptions"></a>檢視 hello 公用 IP 位址所建立的租用戶訂用帳戶
toosee 清單的公用 IP 位址所明確建立的租用戶訂用帳戶，在特定區域中，按一下**公用 IP 位址**下**租用戶資源**。

![租用戶公用 IP 位址](media/azure-stack-viewing-public-ip-address-consumption/image02.png)

您可能會注意到某些已動態配置的公用 IP 位址會出現在 hello 清單，但沒有尚未與其相關聯的位址。 這是因為 hello 位址資源網路資源提供者，但不是在 hello 網路控制卡尚未建立。

hello 網路控制卡不會指派一個位址 toothis 資源，直到實際繫結的 tooan 介面、 網路介面卡 (NIC)、 負載平衡器或虛擬網路閘道。 Hello 公用 IP 位址是繫結的 tooan 介面、 hello 網路控制卡配置 IP 位址 tooit，並出現在 hello**位址**欄位。

## <a name="view-hello-public-ip-address-information-summary-table"></a>檢視 hello 公用 IP 位址資訊摘要表格
有不同的案例數目的公用 IP 位址會指派判斷 hello 位址是否出現在一個清單，或另一個。

| **公用 IP 位址指派案例** | **顯示於使用方式摘要** | **顯示於租用戶公用 IP 位址清單** |
| --- | --- | --- |
| 動態公用 IP 位址尚未指派 tooan NIC 或負載平衡器 （暫時） |否 |是 |
| 動態公用 IP 位址指派 tooan NIC 或負載平衡器。 |是 |是 |
| 靜態公用 IP 位址指派 tooa 租用戶 NIC 或負載平衡器。 |是 |是 |
| 靜態公用 IP 位址指派 tooa 網狀架構基礎結構服務端點。 |是 |否 |
| 公用 IP 位址以隱含方式建立 IaaS VM 執行個體，並用於 hello 虛擬網路上的輸出 NAT。 這些被建立 hello 幕後每當租用戶建立 VM 執行個體，讓 Vm 可以傳送出 toohello 網際網路的資訊。 |是 |否 |

## <a name="next-steps"></a>後續步驟
[在 Azure Stack 中管理儲存體帳戶](azure-stack-manage-storage-accounts.md)