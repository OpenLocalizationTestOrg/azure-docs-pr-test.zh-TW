---
title: "在 Azure 堆疊 aaaQuotas |Microsoft 文件"
description: "系統管理員設定租用戶有存取權的資源的配額 toorestrict hello 最大的數量。"
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
ms.openlocfilehash: 9770802960af102a6d497b47d95cd6ec63ce219c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-and-view-quotas-in-azure-stack"></a>設定與檢視 Azure 堆疊中的配額
配額會定義租用戶的訂用帳戶可以佈建或取用之資源的 hello 限制。 例如，配額可能會讓 toofive Vm 上建立租用戶。 tooadd 服務 tooa 計劃，系統管理員必須設定該服務的 hello 配額設定。

配額是可設定每個服務，以及每個位置，讓系統管理員 tooprovide 更精確地控制 hello 資源耗用量。 系統管理員可以建立一或多個配額資源並將它們關聯計劃，這表示它們可提供不同的供應項目對其服務。 指定服務的配額可以建立從 hello**資源提供者**管理刀鋒視窗，該服務。

訂閱 tooan 供應項目，其中包含多個計劃的租用戶可以使用每個計劃中可用的所有資源。

## <a name="toocreate-an-iaas-quota"></a>toocreate IaaS 配額
1. 在瀏覽器，移至[https://adminportal.local.azurestack.external](https://adminportal.local.azurestack.external/)。
   
   Toohello 堆疊 Azure 入口網站管理員身分登入 （透過使用您在部署期間所提供的 hello 認證）。
2. 選取**新增**，然後**租用戶提供 + 計劃**，然後選取**配額**。
3. 選取您想要的 toocreate 配額 hello 第一個服務。 IaaS 配額，請遵循下列步驟 hello 運算、 網路和儲存體服務。
   在此範例中，我們會先建立 hello 計算服務的配額。 在 hello**命名空間**清單中，選取 hello **Microsoft.Compute**命名空間。
   
   > ![建立新的計算配額](./media/azure-stack-setting-quota/NewComputeQuota.PNG)
   > 
   > 
4. 選擇 hello hello 配額 （例如，'local'） 的定義所在的位置。
5. 在 hello**配額設定**項目，該處會指示**設定容量配額**。 按一下此項目 tooconfigure hello 配額設定。
6. 在 hello**設定配額**刀鋒視窗中，您會看到所有的 hello 計算資源，您可以設定限制。 每個類型都有與它相關聯的預設值。 您可以變更這些值，或者您可以選取 hello**確定**底部 hello hello 刀鋒視窗 tooaccept hello 預設值 按鈕。
   
   > ![設定計算配額](./media/azure-stack-setting-quota/SetQuotasBladeCompute.PNG)
   > 
   > 
7. 您已設定的 hello 值並按下之後**確定**，hello**配額設定**項目顯示為**設定**。 按一下**確定**建立 hello**配額**資源。
   
   您應該會看到通知，指出正在建立 hello 配額資源。
8. 已成功建立 hello 配額集之後，您會收到第二個通知。 準備好 toobe 與方案關聯的現在 hello 計算服務配額。 重複這些步驟以 hello 網路和儲存體服務，而且您準備好 toocreate IaaS 方案 ！
   
   > ![配額建立成功時的通知](./media/azure-stack-setting-quota/QuotaSuccess.png)
   > 
   > 

## <a name="compute-quota-types"></a>計算配額類型
| **類型** | **預設值** | **說明** |
| --- | --- | --- |
| 虛擬機器的數目上限 |50 |hello 訂用帳戶可以在這個位置中建立的虛擬機器的數目上限。 |
| 虛擬機器核心的數目上限 |100 |hello 的訂用帳戶可以在這個位置中建立的核心數目上限 （例如，A3 VM 有四個核心）。 |
| 虛擬機器記憶體 (GB) 的最大數量 |150 |hello 可以佈建，以 mb 為單位的 RAM 數量最大值 （例如，A1 VM 使用 1.75 GB 記憶體）。 |

> [!NOTE]
> 此 Technical Preview 中未限制計算配額。
> 
> 

## <a name="storage-quota-types"></a>儲存體配額類型
| **Item** | **預設值** | **說明** |
| --- | --- | --- |
| 最大容量 (GB) |500 |訂用帳戶可以在這個位置取用的總儲存體容量。 |
| 儲存體帳戶的總數 |20 |hello 的訂用帳戶可以在這個位置中建立的儲存體帳戶數目上限。 |

## <a name="network-quota-types"></a>網路配額類型
| **Item** | **預設值** | **說明** |
| --- | --- | --- |
| 公用 IP 的數目上限 |50 |hello 的訂用帳戶可以在這個位置中建立的公用 Ip 數目上限。 |
| 虛擬網路的數目上限 |50 |hello 的訂用帳戶可以在這個位置中建立的虛擬網路的最大數目。 |
| 虛擬網路閘道的數目上限 |1 |hello 訂用帳戶可以在這個位置中建立的虛擬網路閘道 （VPN 閘道） 的數目上限。 |
| 網路連線的數目上限 |2 |hello 訂用帳戶可以建立在這個位置中的所有虛擬網路閘道的網路連線 （點對點或站台對站台） 的數目上限。 |
| 負載平衡器的數目上限 |50 |hello 訂用帳戶可以在這個位置中建立的負載平衡器的數目上限。 |
| 最大 NIC |100 |hello 訂用帳戶可以在這個位置中建立的網路介面的數目上限。 |
| 網路安全性群組的數目上限 |50 |hello 訂用帳戶可以在這個位置中建立的網路安全性群組的數目上限。 |

##<a name="view-an-existing-quota"></a>檢視現有的配額
tooview 現有的配額，請按一下**更多服務**>**資源提供者**，並選取 hello 與哪些 hello 想 tooview 配額相關聯的服務。 接下來，按一下**配額**，然後選取您想要 tooview 配額 hello。
   > ![檢視現有的配額](./media/azure-stack-setting-quota/ExistingQuota.PNG)
