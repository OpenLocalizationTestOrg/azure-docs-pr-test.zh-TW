---
title: "Azure 雲端服務的 aaaVirtual 機器大小 |Microsoft 文件"
description: "列出 Azure 雲端服務 web 和背景工作角色 hello 不同的虛擬機器大小 （與識別碼）。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1127c23e-106a-47c1-a2e9-40e6dda640f6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 93d91a67afc352f3d18c31e0dd5cf976bf46350c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-cloud-services"></a>雲端服務的大小
本主題描述 hello 可用大小和選項的雲端服務角色執行個體 （web 角色和背景工作角色）。 它也提供了解規劃 toouse 這些資源時的部署考量 toobe。 每種大小都有一個識別碼，可讓您放入[服務定義檔](cloud-services-model-and-package.md#csdef)。 每種大小的價格位於 hello[雲端服務定價](https://azure.microsoft.com/pricing/details/cloud-services/)頁面。

> [!NOTE]
> toosee 相關 Azure 的限制，請參閱[Azure 訂用帳戶和服務限制、 配額和條件約束](../azure-subscription-service-limits.md)
>
>

## <a name="sizes-for-web-and-worker-role-instances"></a>用於 Web 和背景工作角色執行個體的大小
在 Azure 上有多個標準大小 toochoose 從。 這些大小的一些考量事項包括：

* D 系列 Vm 是需要較高運算能力和暫存磁碟效能的設計的 toorun 應用程式。 D 系列 Vm 提供更快的處理器、 記憶體-核心比率較高，以及固態硬碟 (SSD) hello 暫存磁碟。 如需詳細資訊，請參閱 < hello 公告 hello Azure 部落格上[新 D 系列虛擬機器大小](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/)。
* Dv2 系列，後續 toohello 原始的 D 系列、 功能更強大的 CPU。 hello Dv2 數列 CPU 大約是 35%速度 hello D 系列 CPU。 它基礎 hello 最新的層代 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) 處理器，以 hello Intel 快速提升技術 2.0，最高 too3.1 GHz。 hello Dv2 數列有 hello 相同的記憶體和磁碟組態，如 hello D 系列。
* G 系列 Vm 提供 hello 最多記憶體，並在有 Intel Xeon E5 V3 系列處理器的主機上執行。
* hello A 系列 Vm 可以部署在不同硬體類型及處理器。 hello 大小是節流處理，根據 hello 硬體，用於執行執行個體，不論 hello 硬體部署的 hello toooffer 一致的處理器效能。 toodetermine hello 實體硬體部署此大小，查詢 hello 虛擬硬體從 hello 虛擬機器內。
* hello A0 大小是過度訂閱 hello 實體硬體上。 只有這個特定大小，其他客戶部署可能會影響 hello 執行工作負載效能。 hello 相對效能如下所述做 hello 預期基準，15%的主旨 tooan 近似變化。

hello hello 虛擬機器大小會影響定價 hello。 hello 大小也會影響 hello hello 虛擬機器的處理、 記憶體和儲存體容量。 儲存體成本是單獨根據 hello 儲存體帳戶中使用的頁面計算。 如需詳細資訊，請參閱[雲端服務價格詳細資料](https://azure.microsoft.com/pricing/details/cloud-services/)和 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/storage/)。

hello 下列考量可協助您決定大小：

* hello 大小 A8 A11 和 H 數列也是*大量計算執行個體*。 設計和適合需要大量計算執行這些大小的 hello 硬體和網路密集應用程式，包括高效能運算 (HPC) 叢集應用程式、 建模和模擬。 hello A8 A11 數列使用 Intel Xeon E5-2670 @ 2.6 GHZ 和 hello H 數列使用 Intel Xeon E5 2667 v3，3.2 GHz @。 如需有關使用這些大小的詳細資訊與考量，請參閱[高效能計算 VM 大小](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
* Dv2 系列、D 系列和 G 系列是要求更快速的 CPU、更好的本機磁碟效能，或有更高記憶體需求之應用程式的最佳選擇。 它們為許多企業級應用程式提供了強大的組合。
* 某些 hello Azure 資料中心內的實體主機可能不支援較大的虛擬機器大小，例如 A5 – A11。 如此一來，您可能會看到 hello 錯誤訊息**失敗 tooconfigure 虛擬機器 {machine name}**或**失敗 toocreate 虛擬機器 {machine name}**新的現有虛擬機器 tooa 調整大小時大小;在 2013 年 4 月 16 日; 之前建立的虛擬網路中建立新的虛擬機器或加入新的虛擬機器 tooan 現有雲端服務。 請參閱[錯誤: 「 無法 tooconfigure 虛擬機器 」](https://social.msdn.microsoft.com/Forums/9693f56c-fcd3-4d42-850e-5e3b56c7d6be/error-failed-to-configure-virtual-machine-with-a5-a6-or-a7-vm-size?forum=WAVirtualMachinesforWindows)上每個部署案例的因應措施的 hello 支援論壇。
* 您的訂閱也可能會限制 hello 您可以部署特定大小系列中的核心數目。 tooincrease 配額限制時，請連絡 Azure 支援。

## <a name="performance-considerations"></a>效能考量
我們已經建立 hello 概念 hello Azure 計算單位 (ACU) tooprovide 的方式來比較跨越 Azure Sku 和 tooidentify 的 SKU 是最有可能 toosatisfy 計算 (CPU) 效能的效能需求。  ACU 目前是以「小型 (Standard_A1)」VM 為標準 (數值為 100)，而所有其他 SKU 則大致上代表該 SKU 在執行標準基準測試上可以快多少。

> [!IMPORTANT]
> hello ACU 是只是指導方針。 您的工作負載的 hello 結果會有所不同。
>
>

<br>

| SKU 系列 | ACU/核心 |
| --- | --- |
| [ExtraSmall](#a-series) |50 |
| [Small-ExtraLarge](#a-series) |100 |
| [A5-7](#a-series) |100 |
| [Standard_A1-8v2](#av2-series) |100 |
| [Standard_A2m-8mv2](#av2-series) |100 |
| [A8-A11](#a-series) |225* |
| [D1-14](#d-series) |160 |
| [D1-15v2](#dv2-series) |210 - 250* |
| [G1-5](#g-series) |180 - 240* |
| [H](#h-series) |290 - 300* |

標記為 ACUs * 使用 Intel® 快速技術 tooincrease CPU 頻率，並提供效能提升。 hello hello boost 數量可以隨著 hello VM 大小、 工作負載，以及在 hello 上執行其他工作負載相同的主機。

## <a name="size-tables"></a>大小資料表
hello 下列表格顯示 hello 大小和它們所提供的 hello 容量。

* 儲存容量會以 GiB 或是 1024^3 位元組為單位顯示。 當比較磁碟以 GB 為單位 (1000年 ^3 個位元組) toodisks 以 GiB (1024年 ^3) 請記住，GiB 中指定的容量數字可能會出現較小。 例如，1023 GiB = 1098.4 GB
* 磁碟輸送量是以每秒輸入/輸出作業 (IOPS) 和 MBps 進行測量，其中 MBps = 10^6 位元組/每秒。
* 資料磁碟可以在快取模式或取消快取模式下運作。 快取的資料磁碟的作業，hello 主機快取模式設定太**ReadOnly**或**ReadWrite**。 對於未快取的資料磁碟的作業，hello 主機快取模式設定太**無**。
* 最大網路頻寬是 hello 最大彙總的頻寬配置，並指派每個 VM 的型別。 hello 最大頻寬 可提供適用於選取 hello 右 VM 類型 tooensure 適當的網路容量指導。 當您移動之間低 」、 「 中度 」、 高和極高，hello 輸送量會據此增加。 實際的網路效能將取決於許多因素，包括網路和應用程式負載，以及應用程式的網路設定。

## <a name="a-series"></a>A 系列
| 大小            | CPU 核心 | 記憶體：GiB  | 本機 HDD: GiB       | 最大 NIC / 網路頻寬 |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| 特小型      | 1         | 0.768        | 20                   | 1 / 低 |
| 小型           | 1         | 1.75         | 225                  | 1 / 中 |
| 中型          | 2         | 3.5 GB       | 490                  | 1 / 中 |
| 大型           | 4         | 7            | 1000                 | 2 / 高 |
| 特大型      | 8         | 14           | 2040                 | 4 / 高 |
| A5              | 2         | 14           | 490                  | 1 / 中 |
| A6              | 4         | 28           | 1000                 | 2 / 高 |
| A7              | 8         | 56           | 2040                 | 4 / 高 |

## <a name="a-series---compute-intensive-instances"></a>A 系列 - 大量計算執行個體
如需有關使用這些大小的資訊與考量，請參閱[高效能計算 VM 大小](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

| 大小            | CPU 核心 | 記憶體：GiB  | 本機 HDD: GiB       | 最大 NIC / 網路頻寬 |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| A8*             |8          | 56           | 1817                 | 2 / 高 |
| A9*             |16         | 112          | 1817                 | 4 / 非常高 |
| A10             |8          | 56           | 1817                 | 2 / 高 |
| A11             |16         | 112          | 1817                 | 4 / 非常高 |

\*支援 RDMA

## <a name="av2-series"></a>Av2 系列

| 大小            | CPU 核心 | 記憶體：GiB  | 本機 SSD: GiB       | 最大 NIC / 網路頻寬 |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_A1_v2  | 1         | 2            | 10                   | 1 / 中                 |
| Standard_A2_v2  | 2         | 4            | 20                   | 2 / 中                 |
| Standard_A4_v2  | 4         | 8            | 40                   | 4 / 高                     |
| Standard_A8_v2  | 8         | 16           | 80                   | 8 / 高                     |
| Standard_A2m_v2 | 2         | 16           | 20                   | 2 / 中                 |
| Standard_A4m_v2 | 4         | 32           | 40                   | 4 / 高                     |
| Standard_A8m_v2 | 8         | 64           | 80                   | 8 / 高                     |


## <a name="d-series"></a>D 系列
| 大小            | CPU 核心 | 記憶體：GiB  | 本機 SSD: GiB       | 最大 NIC / 網路頻寬 |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| 標準_D1     | 1         | 3.5          | 50                   | 1 / 中 |
| 標準_D2     | 2         | 7            | 100                  | 2 / 高 |
| 標準_D3     | 4         | 14           | 200                  | 4 / 高 |
| 標準_D4     | 8         | 28           | 400                  | 8 / 高 |
| 標準_D11    | 2         | 14           | 100                  | 2 / 高 |
| 標準_D12    | 4         | 28           | 200                  | 4 / 高 |
| 標準_D13    | 8         | 56           | 400                  | 8 / 高 |
| 標準_D14    | 16        | 112          | 800                  | 8 / 非常高 |

## <a name="dv2-series"></a>Dv2 系列
| 大小            | CPU 核心 | 記憶體：GiB  | 本機 SSD: GiB       | 最大 NIC / 網路頻寬 |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_D1_v2  | 1         | 3.5          | 50                   | 1 / 中 |
| Standard_D2_v2  | 2         | 7            | 100                  | 2 / 高 |
| Standard_D3_v2  | 4         | 14           | 200                  | 4 / 高 |
| Standard_D4_v2  | 8         | 28           | 400                  | 8 / 高 |
| Standard_D5_v2  | 16        | 56           | 800                  | 8 / 極高 |
| Standard_D11_v2 | 2         | 14           | 100                  | 2 / 高 |
| Standard_D12_v2 | 4         | 28           | 200                  | 4 / 高 |
| Standard_D13_v2 | 8         | 56           | 400                  | 8 / 高 |
| Standard_D14_v2 | 16        | 112          | 800                  | 8 / 極高 |
| Standard_D15_v2 | 20        | 140          | 1,000                | 8 / 極高 |

## <a name="g-series"></a>G 系列
| 大小            | CPU 核心 | 記憶體：GiB  | 本機 SSD: GiB       | 最大 NIC / 網路頻寬 |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_G1     | 2         | 28           | 384                  |1 / 高 |
| Standard_G2     | 4         | 56           | 768                  |2 / 高 |
| Standard_G3     | 8         | 112          | 1,536                |4 / 非常高 |
| Standard_G4     | 16        | 224          | 3,072                |8 / 極高 |
| Standard_G5     | 32        | 448          | 6,144                |8 / 極高 |

## <a name="h-series"></a>H 系列
Azure H 系列虛擬機器是 hello 下一個產生高效能運算 Vm 旨在高階運算需求，例如屬於分子模型和計算流體動力學。 這些 8 和 16 核心 Vm 之上 hello Intel Haswell E5 2667 V3 處理器技術將設為特色 DDR4 記憶體和本機 ssd 儲存體。

此外 toohello 大量 CPU 能力 hello H 系列提供低延遲 RDMA 網路使用 FDR InfiniBand 和數個記憶體組態 toosupport 記憶體密集運算需求的不同選項。

| 大小            | CPU 核心 | 記憶體：GiB  | 本機 SSD: GiB       | 最大 NIC / 網路頻寬 |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_H8     | 8         | 56           | 1000                 | 8 / 高 |
| Standard_H16    | 16        | 112          | 2000                 | 8 / 非常高 |
| Standard_H8m    | 8         | 112          | 1000                 | 8 / 高 |
| Standard_H16m   | 16        | 224          | 2000                 | 8 / 非常高 |
| Standard_H16r*  | 16        | 112          | 2000                 | 8 / 非常高 |
| Standard_H16mr* | 16        | 224          | 2000                 | 8 / 非常高 |

\*支援 RDMA

## <a name="configure-sizes-for-cloud-services"></a>設定雲端服務大小
您可以指定 hello 的角色執行個體的虛擬機器大小為 hello hello 所描述的服務模型的一部分[服務定義檔](cloud-services-model-and-package.md#csdef)。 hello hello 角色大小會決定 CPU 核心數、 hello 記憶體容量，以及配置給執行個體的 tooa hello 本機檔案系統大小的 hello 數目。 選擇您的應用程式資源需求為基礎的 hello 角色大小。

以下是範例設定 hello 角色大小 toobe [Standard_D2](#general-purpose-d) Web 角色執行個體：

```xml
<WorkerRole name="Worker1" vmsize="Standard_D2">
...
</WorkerRole>
```

## <a name="changing-hello-size-of-an-existing-role"></a>變更現有角色的 hello 大小

為您的工作負載的變更或新的 VM 大小，就可以使用 hello 本質，您可能想 toochange hello 您的角色大小。 因此，您必須變更您的服務定義檔中的 hello VM 大小 （如上所示），重新封裝您的雲端服務，並將它部署 toodo。 不可能 toochange VM 大小，直接從 hello 入口網站或 PowerShell。

>[!TIP]
> 您可能會想 toouse 不同的 VM 大小為您的角色在不同環境 （例如。 測試與生產環境)。 其中一種方式 toodo 這是 toocreate 多個服務定義 (.csdef) 檔案，在您的專案，然後在您使用 hello CSPack 工具的自動化建置期間建立不同的雲端服務封裝每個環境。 進一步了解雲端的 hello 元素 toolearn 服務封裝和如何 toocreate 它們，請參閱[何謂 hello 雲端服務模型，以及如何封裝嗎？](cloud-services-model-and-package.md)
>
>

## <a name="get-a-list-of-sizes"></a>取得大小清單
您可以使用 PowerShell 或 REST API tooget 大小清單 hello。 hello REST API 會記載[這裡](https://msdn.microsoft.com/library/azure/dn469422.aspx)。 hello 下列程式碼是會列出所有目前可用的 hello 大小為雲端服務的 PowerShell 命令。

```powershell
Get-AzureRoleSize | where SupportedByWebWorkerRoles -eq $true | select InstanceSize
```

## <a name="next-steps"></a>後續步驟
* 了解 [Azure 訂用帳戶和服務限制、配額與限制](../azure-subscription-service-limits.md)。
* 進一步了解 HPC 工作負載的[有關高效能計算 VM 大小](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
