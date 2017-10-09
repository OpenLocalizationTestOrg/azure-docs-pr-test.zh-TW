---
title: "規劃 Azure 搜尋 aaaCapacity |Microsoft 文件"
description: "在「Azure 搜尋服務」中調整分割區和複本電腦資源，其中每個資源都是以計費搜尋單位來計價。"
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 1dc16afe-56f9-439d-8874-1733ae1a2b74
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 02/08/2017
ms.author: heidist
ms.openlocfilehash: 4bbbb929a36b932ea7af12e494ca095d98b9005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-resource-levels-for-query-and-indexing-workloads-in-azure-search"></a>在 Azure 搜尋服務中調整適用於查詢和編製索引工作負載的資源等級
之後您[選擇定價層](search-sku-tier.md)和[佈建搜尋服務](search-create-service-portal.md)，hello 下一個步驟是 toooptionally 增加 hello 數目的複本或您的服務所使用的資料分割。 每一層都提供固定的計費單位數目。 這篇文章說明如何 tooallocate 這些單位 tooachieve 最佳的設定您的查詢執行、 編製索引和儲存體需求之間取得平衡。

資源組態時，使用您設定服務在 hello[基本層](http://aka.ms/azuresearchbasic)或其中一個 hello[標準層次](search-limits-quotas-capacity.md)。 對於這些層的可計費服務，購買容量就是增加「搜尋單位」(SU)，每個分割區和複本會計為一個 SU。 

使用較少 SU，帳單費用也會相應降低。 計費是作用中，只要設定 hello 服務。 如果您暫時並不使用的服務，hello tooavoid 計費已刪除 hello 服務，然後在需要時重新建立的唯一方式。

> [!Note]
> 刪除服務會刪除它上面的一切。 Azure 搜尋服務內沒有任何機制可備份和還原持續性搜尋資料。 tooredeploy 現有索引上新的服務，您應該執行 hello 用程式 toocreate，並將其載入到原先。 

## <a name="terminology-partitions-and-replicas"></a>術語：分割區和複本
資料分割和複本都是 hello 回搜尋服務的主要資源。

| 資源 | 定義 |
|----------|------------|
|*分割數* | 為讀寫作業 (例如，在重建或重新整理索引時) 提供索引儲存體和 I/O。|
|複本 | 執行個體的 hello search 服務，使用主要 tooload 平衡查詢作業。 每個複本一律會裝載一份索引。 如果您有 12 複本時，會有 12 副本載入 hello 服務上的每個索引。|

> [!NOTE]
> 沒有任何方法 toodirectly 操作，或管理在複本上執行的索引。 一份在每個複本的每個索引是 hello 服務架構的一部分。
>

## <a name="how-tooallocate-partitions-and-replicas"></a>如何 tooallocate 資料分割和複本
在「Azure 搜尋服務」中，一開始會為服務配置由一個分割區和一個複本組成的最低層級資源。 如果階層支援，您便可以增量調整運算資源，方法是在您需要較多的儲存體和 I/O 時新增分割區，或新增更多複本來因應較大的查詢磁碟區或提供較佳的效能。 單一服務必須有足夠的資源 toohandle （編製索引和查詢） 的所有工作負載。 您無法將多個服務之間的工作負載再加以細分。

tooincrease 或變更 hello 配置的複本和資料分割，我們建議使用 hello Azure 入口網站。 hello 入口網站會強制執行限制保持低於最大限制的可行組合：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)選取 hello 搜尋服務。
2. 在**設定**，開啟 hello**標尺**刀鋒視窗，然後使用 hello 滑桿 tooincrease 或減少 hello 資料分割和複本數目。

如果您需要指令碼或程式碼為基礎的佈建方法，hello[管理 REST API](https://msdn.microsoft.com/library/azure/dn832687.aspx)是替代 toohello 入口網站。

一般而言，搜尋應用程式需要比資料分割，多個複本，特別是當 hello 服務作業偏差查詢工作負載。 hello 區段上[高可用性](#HA)解釋為什麼。

> [!NOTE]
> 佈建服務之後，它不能升級的 tooa 較高 SKU。 您將需要 toocreate hello 新階層的搜尋服務，並重新載入您的索引。 請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)服務佈建的說明。
>
>

<a id="HA"></a>

## <a name="high-availability"></a>高可用性
因為它很簡單，而且相對上快速 tooscale，通常建議您啟動其中包含一個資料分割和一個或兩個複本，然後再為查詢磁碟區的向上延展建置。 對於在 hello Basic 或 S1 層的許多服務，一個資料分割會提供足夠的儲存體和 I/O （在每個資料分割的 15 億個文件）。

查詢工作負載主要是在複本上執行。 如果您需要更多的輸送量或高可用性，可能會需要額外的複本。

針對高可用性的一般建議為：

* 針對唯讀工作負載 (查詢)，需有 2 個複本才能達到高可用性
* 針對讀寫工作負載 (查詢再加上新增、更新或刪除個別文件時的索引編製)，需有 3 個或更多個複本才能達到高可用性

「Azure 搜尋服務」的「服務等級協定」(SLA) 是針對查詢作業和由新增、更新或刪除文件所組成的索引更新。

### <a name="index-availability-during-a-rebuild"></a>索引在重建期間的可用性

Azure 搜尋的高可用性與 tooqueries 和索引不需要重建索引的更新。 如果您刪除某個欄位、 變更資料類型，或重新命名欄位，您將需要 toorebuild hello 索引。 toorebuild hello 索引，您必須刪除 hello 編製索引，重新建立 hello 索引並重新載入 hello 資料。

> [!NOTE]
> 您可以加入新欄位 tooan Azure 搜尋索引而不需重建 hello 索引。 hello 新欄位 hello 值將是已經在 hello 索引中的所有文件為 null。

toomaintain 索引重建期間的可用性，您必須有一份 hello 索引具有不同的名稱上相同名稱不同的服務，然後提供 重新導向或容錯移轉邏輯程式碼中的 hello 的 hello 相同的服務，或複製的 hello 編製索引。

## <a name="disaster-recovery"></a>災害復原
目前沒有任何內建的機制可進行災害復原。 新增資料分割或複本會達成災害復原目標的 hello 錯誤策略。 hello 最常見的方法是藉由設定另一個地區內的第二個搜尋服務的 tooadd hello 服務層級的備援性。 如同在索引重建期間的可用性，hello 重新導向或容錯移轉邏輯必須來自您的程式碼。

## <a name="increase-query-performance-with-replicas"></a>利用複本提高查詢效能
查詢延遲是一項指標，代表需要額外的複本。 一般而言，改善查詢效能的第一個步驟是此資源的更多的 tooadd。 當您加入複本，hello 索引的其他複本會回到線上 toosupport 更大的查詢工作負載和多個複本 hello tooload 平衡 hello 要求。

我們目前無法提供硬估計上每秒查詢數 (QPS): 查詢效能取決於 hello hello 複雜度查詢和競爭的工作負載。 平均來說，一個「基本」或 S1 SKU 複本可以提供大約 15 QPS 的服務，但您的輸送量會因為查詢的複雜性 (多面向查詢較為複雜) 和網路延遲而較高或較低。 此外，務必 toorecognize，雖然新增複本必定會增加規模和效能，hello 結果不是完全線性： 加入三個複本，並不保證倍的輸送量。

有關 QPS，包含針對您的工作負載，估計 QPS 方法 toolearn 看到[管理您的搜尋服務](search-manage.md)。

## <a name="increase-indexing-performance-with-partitions"></a>使用資料分割提高編製索引的效能
要求近乎即時資料重新整理的搜尋應用程式，按比例需要比複本更多的資料分割數。 新增資料分割可將讀取/寫入作業分配到更大量的計算資源。 它也提供更多磁碟空間來儲存額外的索引和文件。

較大的索引會花費較長的 tooquery。 這麼一來，您可能會發現每個資料分割中每個累加式的增加在複本中都需要有較小但按比例的增加。 您的查詢和查詢磁碟區的 hello 複雜性會分解到查詢執行的開啟速度。

## <a name="basic-tier-partition-and-replica-combinations"></a>基本層：資料分割與複本組合
基本服務可以有一個資料分割，並向上 toothree 複本，針對三個 SUs 最大限制。 hello 只可調整的資源是複本。 您至少需要 2 個複本，才能在查詢上達到高可用性。

<a id="chart"></a>

## <a name="standard-tiers-partition-and-replica-combinations"></a>標準層：分割區和複本的組合
下表顯示 hello SUs 必要的 toosupport 組合複本和資料分割、 主旨 toohello 36 SU 限制時，所有標準層次。

|   | **1 個資料分割** | **2 個資料分割** | **3 個資料分割** | **4 個資料分割** | **6 個資料分割** | **12 個資料分割** |
| --- | --- | --- | --- | --- | --- | --- |
| **1 個複本** |1 SU |2 SU |3 SU |4 SU |6 SU |12 SU |
| **2 個複本** |2 SU |4 SU |6 SU |8 SU |12 SU |24 SU |
| **3 個複本** |3 SU |6 SU |9 SU |12 SU |18 SU |36 SU |
| **4 個複本** |4 SU |8 SU |12 SU |16 SU |24 SU |N/A |
| **5 個複本** |5 SU |10 SU |15 SU |20 SU |30 SU |N/A |
| **6 個複本** |6 SU |12 SU |18 SU |24 SU |36 SU |N/A |
| **12 個複本** |12 SU |24 SU |36 SU |N/A |N/A |N/A |

SUs、 定價和容量中詳細說明 hello Azure 網站上。 如需詳細資訊，請參閱[定價詳細資料](https://azure.microsoft.com/pricing/details/search/)。

> [!NOTE]
> 複本和資料分割的 hello 數目將平均分割成 12 (具體而言，1、 2、 3、 4、 6、 12)。 這是因為「Azure 搜尋服務」會將每個索引預先劃分成 12 個分區，以便將其平均散佈到所有分割區。 例如，如果您的服務有三個資料分割，並建立索引，每個資料分割將會包含四個分區的 hello 索引。 如何將索引的 Azure 搜尋分區化是實作詳細資料，主旨 toochange 在未來的版本。 Hello 數字現在為 12，雖然您不應預期的數字 tooalways 是 hello 未來 12。
>
>

## <a name="billing-formula-for-replica-and-partition-resources"></a>複本和分割區資源的計費公式
計算特定組合使用多少 SUs hello 公式是 hello 產品的複本和資料分割，或 (R X P = 24)。 例如， 3 個複本乘以 3 個資料分割為 9 個 SU 費用。

每個 SU 成本取決於 hello 層，速率較低每單位計費比標準的基本。 如需每一層的費率，請參閱 [定價詳細資料](https://azure.microsoft.com/pricing/details/search/)。
