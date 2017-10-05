---
title: "Azure 的堆疊中的配額 |Microsoft 文件"
description: "系統管理員可設定配額以限制租用戶有存取權的資源的最大數量。"
services: azure-stack
documentationcenter: 
author: mattmcg
manager: byronr
editor: 
ms.assetid: 955c6dd8-cefe-42f3-af88-e11d17d22725
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 3/1/2017
ms.author: mattmcg
ms.openlocfilehash: bbefca1a60f38f18838ee6563bd26b934cd02172
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-and-view-quotas-in-azure-stack"></a>設定與檢視 Azure 堆疊中的配額
配額會定義租用戶的訂用帳戶可以佈建或取用之資源的限制。 例如，配額可能會讓租用戶，以建立最多五個 Vm。 若要加入至方案的服務，系統管理員必須設定該服務的配額設定。

配額是可設定每個服務，以及每個位置，讓系統管理員提供更精確地控制的資源耗用量。 系統管理員可以建立一或多個配額資源並將它們關聯計劃，這表示它們可提供不同的供應項目對其服務。 指定服務的配額可以從建立**資源提供者**管理刀鋒視窗，該服務。

租用戶訂閱方案包含多個計劃可以使用每個計劃中可用的所有資源。

## <a name="to-create-an-iaas-quota"></a>若要建立的 IaaS 配額
1. 在瀏覽器，移至[https://adminportal.local.azurestack.external](https://adminportal.local.azurestack.external/)。
   
   Azure 堆疊入口網站管理員身分登入 （透過使用您在部署期間所提供的認證）。
2. 選取**新增**，然後**租用戶提供 + 計劃**，然後選取**配額**。
3. 選取您要建立配額的第一個服務。 針對 IaaS 配額，請針對計算、網路與儲存體服務依照這些步驟執行。
   在此範例中，我們先為計算服務建立配額。 在**命名空間**清單中，選取**Microsoft.Compute**命名空間。
   
   > ![建立新的計算配額](./media/azure-stack-setting-quota/NewComputeQuota.PNG)
   > 
   > 
4. 選擇配額 （例如，'local'） 的定義所在的位置。
5. 在**配額設定**項目，該處會指示**設定容量配額**。 按一下此項目可設定配額設定。
6. 在**設定配額**刀鋒視窗中，您會看到所有您可以設定限制的計算資源。 每個類型都有與它相關聯的預設值。 您可以變更這些值，或者您可以選取**確定**接受預設值 刀鋒視窗底部的按鈕。
   
   > ![設定計算配額](./media/azure-stack-setting-quota/SetQuotasBladeCompute.PNG)
   > 
   > 
7. 您已設定的值，並按下之後**確定**、**配額設定**項目顯示為**設定**。 按一下**確定**建立**配額**資源。
   
   您應該會看到通知，指出正在建立配額資源。
8. 已成功建立的配額集之後，您會收到第二個通知。 計算服務配額現在已準備好要與方案產生關聯。 重複上述步驟與 網路和儲存體服務，您準備好要建立的 IaaS 方案 ！
   
   > ![配額建立成功時的通知](./media/azure-stack-setting-quota/QuotaSuccess.png)
   > 
   > 

## <a name="compute-quota-types"></a>計算配額類型
| **類型** | **預設值** | **說明** |
| --- | --- | --- |
| 虛擬機器的數目上限 |50 |訂用帳戶可以在這個位置建立的虛擬機器數目上限。 |
| 虛擬機器核心的數目上限 |100 |訂用帳戶可以在這個位置建立的核心數目上限 (例如，A3 VM 有四個核心)。 |
| 虛擬機器記憶體 (GB) 的最大數量 |150 |RAM 可佈建以 mb 為單位的最大數量 （例如，A1 VM 使用 1.75 GB 記憶體）。 |

> [!NOTE]
> 此 Technical Preview 中未限制計算配額。
> 
> 

## <a name="storage-quota-types"></a>儲存體配額類型
| **Item** | **預設值** | **說明** |
| --- | --- | --- |
| 最大容量 (GB) |500 |訂用帳戶可以在這個位置取用的總儲存體容量。 |
| 儲存體帳戶的總數 |20 |訂用帳戶可以在這個位置建立的儲存體帳戶數目上限。 |

## <a name="network-quota-types"></a>網路配額類型
| **Item** | **預設值** | **說明** |
| --- | --- | --- |
| 公用 IP 的數目上限 |50 |訂用帳戶可以在這個位置建立的公用 IP 數目上限。 |
| 虛擬網路的數目上限 |50 |訂用帳戶可以在這個位置建立的虛擬網路數目上限。 |
| 虛擬網路閘道的數目上限 |1 |訂用帳戶可以在這個位置建立的虛擬網路閘道 (VPN 閘道) 數目上限。 |
| 網路連線的數目上限 |2 |訂用帳戶可以在這個位置所有虛擬網路閘道上建立的網路連線 (點對點或站台對站台) 數目上限。 |
| 負載平衡器的數目上限 |50 |訂用帳戶可以在這個位置建立的負載平衡器數目上限。 |
| 最大 NIC |100 |訂用帳戶可以在這個位置建立的網路介面數目上限。 |
| 網路安全性群組的數目上限 |50 |訂用帳戶可以在這個位置建立的網路安全性群組數目上限。 |

##<a name="view-an-existing-quota"></a>檢視現有的配額
若要檢視現有的配額，請按一下**更多服務**>**資源提供者**和選取與您想要檢視的配額相關聯的服務。 接下來，按一下**配額**，然後選取您想要檢視的配額。
   > ![檢視現有的配額](./media/azure-stack-setting-quota/ExistingQuota.PNG)
