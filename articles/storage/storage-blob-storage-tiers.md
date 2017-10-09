---
title: "cool aaaAzure blob 儲存體 |Microsoft 文件"
description: "Azure Blob 儲存體的儲存層會根據存取模式，為物件資料提供具成本效益的儲存體。 hello 酷炫的儲存層最適合用於較不常存取的資料。"
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: eb33ed4f-1b17-4fd6-82e2-8d5372800eef
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/05/2017
ms.author: mihauss
ms.openlocfilehash: 56fae3fdae31a6958ebae01fd96a0366e70ae938
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-blob-storage-hot-and-cool-storage-tiers"></a>Azure Blob 儲存體︰經常性存取與非經常性存取儲存層
## <a name="overview"></a>概觀
Azure 儲存體會為 Blob 物件儲存體提供兩個儲存層，所以您可根據您的資料使用方式，以最符合成本效益的方式進行儲存。 hello Azure**熱儲存層**最適合用於儲存經常存取的資料。 hello Azure**酷炫的儲存層**最適合用於儲存，而且不常存取長時間執行的資料。 Hello 酷炫的儲存層中的資料可容許較低的可用性，但仍需要高持久性和類似的時間來存取和輸送量特性做為熱資料。 對於非經常性存取資料而言，稍微較低的可用性 SLA 和更高的存取成本是可接受的取捨，可讓儲存體成本降低許多。

現在，指數的速度成長 hello 雲端中儲存的資料。 擴充的儲存體需要成本 toomanage，很有幫助 tooorganize 資料為基礎的屬性，例如存取頻率和規劃的保留期限。 Hello 雲端中儲存的資料可能會不同方面如何產生、 處理，並存取其存留期。 有些資料在其存留期內會積極地存取及修改。 某些資料存取常見問題及早在其存留期間，存取卸除大幅 hello 資料年齡為。 某些資料 hello 定域機組中維持閒置很少是，如果曾，存取一次儲存。

上述每個資料存取案例均受惠於針對特定存取模式最佳化的差異化儲存層。 Hello 引入的作用中且酷炫的儲存層，使用 Azure Blob 儲存體現在解決這需要使用不同的儲存層會分隔定價模型。

## <a name="blob-storage-accounts"></a>Blob 儲存體帳戶
**Blob 儲存體帳戶** 是特殊的儲存體帳戶，可將非結構化資料儲存為 Azure 儲存體中的 Blob (物件)。 使用 Blob 儲存體帳戶，您現在可以選擇之間作用中且酷炫的儲存層 toostore cool 較低的儲存體成本，較不常存取的資料和更經常存取的存放區的低成本的存取熱資料。 Blob 儲存體帳戶是類似 tooyour 現有一般用途的儲存體帳戶共用所有 hello 絕佳的持續性、 可用性、 延展性和效能的功能，您使用，包括區塊 blob 的 100 %api 一致性以及附加 blob。

> [!NOTE]
> Blob 儲存體帳戶僅支援區塊和附加 Blob，不支援分頁 Blob。
> 
> 

Blob 儲存體帳戶公開 hello**存取層**屬性，可讓您 toospecify hello 儲存層做**作用**或**Cool**根據 hello 資料儲存在 hello帳戶。 如果沒有在 hello 使用量模式中的資料變更，您也可以切換這些儲存層，在任何時間之間。

> [!NOTE]
> 變更 hello 儲存層可能會導致產生額外費用。 請參閱 hello[定價和計費](storage-blob-storage-tiers.md#pricing-and-billing)> 一節以取得詳細資料。
> 
> 

Hello 熱儲存層的範例使用案例包括：

* 在使用中或預期的 toobe （從讀取和寫入） 經常存取的資料。
* 分段進行處理和最終移轉 toohello 酷炫的儲存層的資料。

Hello 酷炫的儲存層的範例使用案例包括：

* 備份、封存和災害復原資料集。
* 較舊的媒體內容不會經常不再檢視，但時，預期的 toobe 可立即存取。
* 需要 toobe 的大型資料集有效地儲存成本，而供未來處理所收集的詳細資料。 (例如，科學資料、來自製造工廠的原始遙測資料等長期儲存)
* 即使已處理成最終可用格式，但還是需要保存的原始資料。 (例如，轉碼成其他格式之後的原始媒體檔案)
* 相容性，而且需要長時間儲存 toobe 且難以曾經存取的封存資料。 (例如，保全攝影機錄影畫面、醫療機構的舊 X 光/MRI、金融服務的客服電話錄音和文字記錄)

如需儲存體帳戶的詳細資訊，請參閱 [關於 Azure 儲存體帳戶](storage-create-storage-account.md) 。

應用程式只需要封鎖，或附加 blob 儲存體，我們建議使用 Blob 儲存體帳戶，利用 hello tootake 區分計價模型的階層式儲存。 但是，我們了解這可能不是可能在某些情況下，使用一般用途儲存體帳戶會是 hello 方式 toogo，例如：

* 您需要 toouse 資料表、 佇列，或檔案，且想您的 blob 儲存在 hello 相同儲存體帳戶。 請注意，任何技術的優點 toostoring 這些 hello 除了擁有 hello 相同共用金鑰使用相同帳戶中。
* 您仍然需要 toouse hello 傳統部署模型。 Blob 儲存體帳戶，才可透過 hello Azure Resource Manager 部署模型。
* 您需要 toouse 分頁 blob。 Blob 儲存體帳戶不支援分頁 Blob。 我們通常建議使用區塊 Blob，除非您對分頁 Blob 有特定的需求。
* 您使用新版 hello[儲存體服務 REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx)低於 2014年-02-14，或是用戶端程式庫的版本低於 4.x，並無法升級您的應用程式。

> [!NOTE]
> 目前所有的 Azure 區域都支援 Blob 儲存體帳戶。
> 
> 

## <a name="comparison-between-hello-storage-tiers"></a>Hello 儲存層之間的比較
hello 下表會反白顯示 hello 比較兩個儲存層 hello:

<table border="1" cellspacing="0" cellpadding="0" style="border: 1px solid #000000;">
<col width="250">
<col width="250">
<col width="250">
<tbody>
<tr>
    <td><strong><center></center></strong></td>
    <td><strong><center>經常性存取儲存層</center></strong></td>
    <td><strong><center>非經常性存取儲存層</center></strong></td
</tr>
<tr>
    <td><strong><center>可用性</center></strong></td>
    <td><center>99.9%</center></td>
    <td><center>99%</center></td>
</tr>
<tr>
    <td><strong><center>可用性<br>(RA-GRS 讀取)</center></strong></td>
    <td><center>99.99%</center></td>
    <td><center>99.9%</center></td>
</tr>
<tr>
    <td><strong><center>使用費用</center></strong></td>
    <td><center>儲存成本較高<br>存取和交易成本較低</center></td>
    <td><center>儲存成本較低<br>存取和交易成本較高</center></td>
</tr>
<tr>
    <td><strong><center>最小物件大小<center></strong></td>
    <td colspan="2"><center>N/A</center></td>
</tr>
<tr>
    <td><strong><center>最小儲存持續時間<center></strong></td>
    <td colspan="2"><center>N/A</center></td>
</tr>
<tr>
    <td><strong><center>延遲<br>（時間 toofirst 位元組）<center></strong></td>
    <td colspan="2"><center>毫秒</center></td>
</tr>
<tr>
    <td><strong><center>延展性和效能目標<center></strong></td>
    <td colspan="2"><center>與一般用途儲存體帳戶相同</center></td>
</tr>
</tbody>
</table>

> [!NOTE]
> Blob 儲存體帳戶支援 hello 相同的效能和延展性目標為一般用途儲存體帳戶。 如需詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md) (英文)。
> 
> 

## <a name="pricing-and-billing"></a>價格和計費
Blob 儲存體帳戶會將新的定價模型用於根據 hello 儲存層的 blob 儲存體。 當使用 Blob 儲存體帳戶時，適用於 hello 遵循計費考量：

* **儲存體成本**： 此外 toohello 儲存的資料量，儲存資料的 hello 成本有所不同 hello 儲存層。 hello 每 gb 的成本會更低，比 hello 熱儲存層的 hello 酷炫的儲存層。
* **資料存取成本**: hello 酷炫的儲存層中的資料，您將支付每 gb 的資料存取需要付費讀取和寫入。
* **交易成本**︰這兩層都有每筆交易的費用。 不過，hello 酷炫的儲存層的 hello 每筆交易成本高於的 hello 熱儲存層。
* **地理複寫資料傳輸成本**： 這只適用於 tooaccounts 異地複寫設定，包括 GRS 和 RA-GRS。 異地複寫資料傳輸會產生每 GB 費用。
* **輸出資料傳輸成本**︰輸出資料傳輸 (從 Azure 區域傳出的資料) 會產生每 GB 頻寬使用量費用，與一般用途的儲存體帳戶一致。
* **變更 hello 儲存層**： 從 cool toohot 變更 hello 儲存層將會產生費用的相等 tooreading 所有現有的每個轉換的 hello 儲存體帳戶中的 hello 資料。 Hello 相反地，從熱 toocool 變更 hello 儲存層將免費提供的成本。

> [!NOTE]
> 在排序 tooallow 使用者 tootry hello 出新的儲存層和驗證功能 post 啟動，hello 費用從 cool toohot 變更 hello 儲存層將會就免除關閉年 6 月 30 2016年之前。 從 7 月 1 日 2016年開始，hello 費用就是從 cool toohot 套用的 tooall 轉換。 如需 hello 計價模型的 Blob 儲存體帳戶的詳細資訊，請參閱[Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/)頁面。 如需 hello 傳出資料的詳細資訊請參閱傳輸費用，[資料傳輸定價詳細資料](https://azure.microsoft.com/pricing/details/data-transfers/)頁面。
> 
> 

## <a name="quick-start"></a>快速啟動
在本節中，我們將示範下列案例使用 hello Azure 入口網站的 hello:

* 如何 toocreate Blob 儲存體帳戶。
* 如何 toomanage Blob 儲存體帳戶。

### <a name="using-hello-azure-portal"></a>使用 hello Azure 入口網站
#### <a name="create-a-blob-storage-account-using-hello-azure-portal"></a>建立 Blob 儲存體帳戶使用 hello Azure 入口網站
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，選取 **新增** > **資料 + 儲存體** > **儲存體帳戶**。
3. 輸入儲存體帳戶的名稱。
   
    此名稱必須是全域唯一的。它會當做 hello URL 的一部分使用 tooaccess hello 物件 hello 儲存體帳戶中。  
4. 選取**資源管理員**為 hello 部署模型。
   
    階層式的儲存只能使用資源管理員的儲存體帳戶。這是建議的新資源部署模型的 hello。 如需詳細資訊，請參閱 hello [Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)。  
5. 在 hello 帳戶類型 下拉式清單中，選取  **Blob 儲存體**。
   
    這是您在其中選取 hello 儲存體帳戶類型。 階層式的儲存不適用於一般用途的儲存體。您僅供以 hello Blob 儲存體類型的帳戶。     
   
    請注意，當您選取此選項，hello 效能層，會設定 tooStandard。 無法使用與 hello 高階效能層階層式的儲存。
6. 選取 hello hello 儲存體帳戶的複寫選項： **LRS**， **GRS**，或**RA-GRS**。 hello 預設值是**RA-GRS**。
   
    LRS = 本機備援儲存體。GRS = 地理備援儲存體 （2 地區）。RA-GRS 是讀取權限的地理備援儲存體 （2 區域具有讀取存取 toohello 第二個）。
   
    如需 Azure 儲存體複寫選項的詳細資訊，請參閱 [Azure 儲存體複寫](storage-redundancy.md)。
7. 針對您的需求選取 hello 右邊的儲存層： 集 hello**存取層**tooeither **Cool**或**作用**。 hello 預設值是**作用**。
8. 選取您想在其中 toocreate hello 新儲存體帳戶的 hello 訂用帳戶。
9. 指定新的資源群組，或選取現有的資源群組。 如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。
10. 選取儲存體帳戶的 hello 地區。
11. 按一下**建立**toocreate hello 儲存體帳戶。

#### <a name="change-hello-storage-tier-of-a-blob-storage-account-using-hello-azure-portal"></a>變更 hello 儲存層的 Blob 儲存體帳戶使用 hello Azure 入口網站
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. toonavigate tooyour 儲存體帳戶，選取所有的資源，然後選取 儲存體帳戶。
3. 在 hello 設定刀鋒視窗中，按一下 **組態**tooview 和/或變更 hello 帳戶設定。
4. 針對您的需求選取 hello 右邊的儲存層： 集 hello**存取層**tooeither **Cool**或**作用**。
5. 按一下 儲存在 hello hello 刀鋒視窗最上方。

> [!NOTE]
> 變更 hello 儲存層可能會導致產生額外費用。 請參閱 hello[定價和計費](storage-blob-storage-tiers.md#pricing-and-billing)> 一節以取得詳細資料。
> 
> 

## <a name="evaluating-and-migrating-tooblob-storage-accounts"></a>評估和移轉 tooBlob 儲存體帳戶
hello 本節的目的是 toohelp 使用者 toomake smooth 轉換 toousing Blob 儲存體帳戶。 有兩個使用者案例：

* 您有現有的一般用途儲存體帳戶，並想 tooevaluate 變更 tooa 與 hello 右邊的儲存層的 Blob 儲存體帳戶。
* 您已決定 toouse Blob 儲存體帳戶或已經有一個，而且要 tooevaluate 是否應該使用 hello 熱或酷炫的儲存層。

在這兩種情況下，hello 首先會是 tooestimate hello 成本儲存和存取資料的 Blob 儲存體帳戶中儲存和比較針對您目前的成本。

### <a name="evaluating-blob-storage-account-tiers"></a>評估 Blob 儲存體帳戶層
中的儲存和存取儲存在 Blob 儲存體帳戶中的資料順序 tooestimate hello 成本，您將需要 tooevaluate 您現有的使用模式，或接近您的預期的使用模式。 一般情況下，您會想 tooknow:

* 您的儲存體使用情況 – 目前儲存多少資料，以及每個月的變化情況為何？
* 您儲存體的存取模式-多少資料正被讀取和寫入的 toohello 帳戶 （包括新的資料）？ 有多少交易用於資料存取，而它們是何種交易？

#### <a name="monitoring-existing-storage-accounts"></a>監視現有的儲存體帳戶
toomonitor 現有的儲存體帳戶和收集資料，您可以利用 Azure 儲存體分析的執行記錄，並提供儲存體帳戶的度量資料。
儲存體分析可儲存有關要求 toohello 一般用途儲存體帳戶以及 Blob 儲存體帳戶的 Blob 儲存體服務的彙總的交易統計資料和容量資料的度量。
此資料會儲存在已知資料表中 hello 相同儲存體帳戶。

如需詳細資訊，請參閱[關於儲存體分析度量](https://msdn.microsoft.com/library/azure/hh343258.aspx)和[儲存體分析度量資料表結構描述](https://msdn.microsoft.com/library/azure/hh343264.aspx)

> [!NOTE]
> Blob 儲存體帳戶公開 hello 表格服務端點，僅適用於儲存和存取該帳戶的 hello 度量資料。
> 
> 

toomonitor hello Blob 儲存體服務的 hello 存放裝置耗用量，您將需要 tooenable hello 容量度量。
使用此啟用，容量儲存體帳戶之 Blob 服務，針對每日記錄和記錄的資料為資料表的項目寫入 toohello *$MetricsCapacityBlob*資料表內 hello 相同儲存體帳戶。

toomonitor hello 資料存取模式的 hello Blob 儲存體服務，您將需要 tooenable hello 每小時交易度量應用程式開發介面層級。
與此啟用，每個 API 交易是每小時的彙總資料和記錄資料表項目寫入 toohello 為*$MetricsHourPrimaryTransactionsBlob*資料表內 hello 相同儲存體帳戶。 hello *$MetricsHourSecondaryTransactionsBlob*資料表記錄 hello 交易 toohello 次要端點發生 RA-GRS 儲存體帳戶。

> [!NOTE]
> 如果您已有一般用途的儲存體帳戶，並在中儲存分頁 blob 和虛擬機器磁碟以及區塊和附加 blob 資料，就不適用此估計程序。 這是因為您將無法區別容量的交易度量僅根據 hello 型別之 blob 的區塊及附加 blob 可以是移轉 tooa Blob 儲存體帳戶。
> 
> 

tooget 資料使用和存取模式的良好近似值，我們建議您選擇規則的使用方式，代表 hello 度量的保留期限，並藉此推斷。
其中一個選項是 tooretain hello 度量資料的 7 天和收集 hello 資料進行分析 hello hello 月份結尾的每週。
另一個選項是 hello tooretain hello 度量資料過去 30 天內收集及分析和 hello 資料結尾 hello hello 30 天的期限。

如需啟用、收集和檢視度量資料的詳細資訊，請參閱 [啟用 Azure 儲存體度量和檢視度量資料](storage-enable-and-view-metrics.md)。

> [!NOTE]
> 就如同一般使用者資料，儲存、存取和下載分析資料也需付費。
> 
> 

#### <a name="utilizing-usage-metrics-tooestimate-costs"></a>利用使用度量 tooestimate 成本
##### <a name="storage-costs"></a>儲存成本
hello hello 容量度量資料表中的最新項目*$MetricsCapacityBlob* hello 資料列索引鍵與*'data'*顯示 hello 供使用者資料的儲存容量。
hello hello 容量度量資料表中的最新項目*$MetricsCapacityBlob* hello 資料列索引鍵與*'分析'*顯示 hello hello 分析記錄檔所使用的儲存容量。

接著可以使用這兩個使用者資料與分析資料記錄 （如果啟用） 此總容量使用 tooestimate hello 成本 hello 儲存體帳戶中儲存資料。
hello 相同方法也可用來估計儲存體成本區塊，並附加一般用途儲存體帳戶中的 blob。

##### <a name="transaction-costs"></a>交易成本
hello 總和*'TotalBillableRequests'*，在 api hello 交易中的所有項目度量表會指出 hello 總該特定 API 的交易數。 *例如*，hello 總數*'GetBlob'*使用 hello 資料列索引鍵的所有項目為可計費的要求總數的 hello 總和可以計算在指定時間的交易*' 使用者資訊。GetBlob'*。

順序 tooestimate Blob 儲存體帳戶的交易成本，您必須向分成三個群組的 hello 交易 toobreak 因為它們的方式不同價格。

* 寫入 'PutBlob'、'PutBlock'、'PutBlockList'、'AppendBlock'、'ListBlobs'、'ListContainers'、'CreateContainer'、'SnapshotBlob' 和 'CopyBlob' 等交易。
* 刪除 'DeleteBlob' 和 'DeleteContainer' 等交易。
* 所有其他交易

在一般用途儲存體帳戶的順序 tooestimate 交易成本，您需要 tooaggregate 無論 hello 作業/應用程式開發介面的所有交易。

##### <a name="data-access-and-geo-replication-data-transfer-costs"></a>資料存取和異地複寫資料傳輸費用
雖然未提供儲存體分析 hello 資料量讀取和寫入 tooa 儲存體帳戶，它可以來概略估計藉由查看 hello 交易度量資料表。
hello 總和*'TotalIngress'*資料表在 hello 交易度量 api 的所有項目該特定應用程式開發介面的指出 hello 總量，以位元組為單位的輸入資料。
同樣地 hello 總和*'TotalEgress'*指出 hello 的輸出資料，以位元組為單位的總容量。

順序 tooestimate hello 資料存取的成本 Blob 儲存體帳戶，您必須使用 toobreak 向 hello 分成兩個群組的交易。

* 來估計 hello 數量 hello 儲存體帳戶中擷取的資料，請查看 hello 總和*'TotalEgress'*主要 hello *'GetBlob'*和*'Copyblob 應用程式開發'*作業。
* 您可以藉由查看 hello 總和估計寫入 toohello 儲存體帳戶的資料的 hello 數量*'TotalIngress'*主要 hello *'PutBlob'*， *'PutBlock'*， *'Copyblob 應用程式開發'*和*'AppendBlock'*作業。

hello 異地備援 blob 儲存體帳戶也可以透過 hello 估計 hello GRS 或 RA-GRS 儲存體帳戶發生寫入的資料量的計算的資料傳輸的成本。

> [!NOTE]
> 如需計算使用 hello 熱或酷炫的儲存層的 hello 成本更詳細範例，請看看 hello 標題*'什麼是作用和 Cool 存取層，以及如何應該判斷哪一個 toouse' 嗎？* 在 hello [Azure 儲存體定價頁面](https://azure.microsoft.com/pricing/details/storage/)。
> 
> 

### <a name="migrating-existing-data"></a>移轉現有的資料
Blob 儲存體帳戶專門用於儲存區塊和附加 Blob。 現有的一般用途儲存體帳戶、 toostore 資料表、 佇列、 檔案和磁碟，以及 blob，可讓您不能轉換的 tooBlob 儲存體帳戶。 toouse hello 儲存層，您會需要 toocreate 新 Blob 儲存體帳戶，並將現有的資料移轉到新建立的 hello 帳戶。

您可以使用下列方法 toomigrate 現有資料至 Blob 儲存體帳戶，從內部部署存放裝置、 協力廠商雲端存放裝置提供者，或從現有的一般用途儲存體帳戶在 Azure 中的 hello:

#### <a name="azcopy"></a>AzCopy
AzCopy 是專為高效能的資料 tooand 複製從 Azure 儲存體設計的 Windows 命令列公用程式。 您可以使用 從內部部署儲存體裝置 AzCopy toocopy 資料到 Blob 儲存體帳戶從現有的一般用途儲存體帳戶或 tooupload 資料，將 Blob 儲存體帳戶。

如需詳細資訊，請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)。

#### <a name="data-movement-library"></a>資料移動程式庫
Azure 儲存體的資料移動.NET 程式庫根據 hello 核心資料移動架構提供 AzCopy。 hello 程式庫設計的高效能、 可靠且簡單的資料傳輸作業類似 tooAzCopy。 這可讓您的 hello 所提供的功能 AzCopy 應用程式中原本就不需要執行與監視外部的執行個體的 AzCopy toodeal tootake 完整優點。

如需詳細資訊，請參閱 [適用於 .Net 的 Azure 儲存體資料移動程式庫](https://github.com/Azure/azure-storage-net-data-movement)

#### <a name="rest-api-or-client-library"></a>REST API 或用戶端程式庫
您可以建立自訂應用程式 toomigrate 資料到 Blob 儲存體帳戶，使用其中一種 hello Azure 用戶端程式庫或 hello Azure 儲存體服務 REST API。 Azure 儲存體針對以下多種語言和平台提供豐富的用戶端程式庫：例如 .NET、Java、C++、Node.JS、PHP、Ruby 和 Python。 hello 用戶端程式庫提供進階的功能，例如重試邏輯、 記錄和並行上傳。 您也可以直接對 hello REST API，可以呼叫任何提出 HTTP/HTTPS 要求的語言所開發。

如需詳細資訊，請參閱 [開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md)。

> [!NOTE]
> 使用用戶端加密進行加密的 blob 存放區與 hello blob 儲存的加密相關中繼資料。 是關鍵的 hello blob 中繼資料，而且特別是 hello 加密相關中繼資料，會保留，應該確保任何複製機制。 如果您複製 hello blob，如果沒有這個中繼資料，hello blob 內容將無法擷取一次。 如需有關加密相關中繼資料的詳細資訊，請參閱 [Azure 儲存體用戶端加密](storage-client-side-encryption.md)。
> 
> 

## <a name="faqs"></a>常見問題集
1. **現有的儲存體帳戶是否仍然可用？**
   
    是，現有的儲存體帳戶仍然可用，且價格或功能不變。  它們並沒有 hello 能力 toochoose 儲存層，將不會在未來的 hello 擁有階層處理功能。
2. **為何和何時應該開始使用 Blob 儲存體帳戶？**
   
    Blob 儲存體帳戶專門用來儲存 blob，並讓我們 toointroduce 新 blob 為中心的功能。 從現在開始，Blob 儲存體帳戶，會根據此帳戶類型會引進 hello 建議的方式將 blob 儲存為未來的功能，例如階層式儲存體階層處理。 不過，它已啟動 tooyou 當您想要 toomigrate 根據您的業務需求。
3. **可以將轉換我現有的儲存體帳戶 tooa Blob 儲存體帳戶嗎？**
   
    否。 Blob 儲存體帳戶是不同類型的儲存體帳戶，您將需要 toocreate 新它與以上所述，將資料移轉。
4. **可以儲存物件 hello 中這兩個儲存層中相同的帳戶嗎？**
   
    hello *'存取層'*屬性表示 hello 儲存層會在帳戶層級設定，並套用 tooall 物件，該帳戶中的。 您無法在物件層級設定 hello 存取層的屬性。
5. **可以變更 hello 儲存層的 我的 Blob 儲存體帳戶嗎？**
   
    是。 您將會無法 toochange hello 儲存層所設定的 hello *'存取層'* hello 儲存體帳戶上的屬性。 變更 hello 儲存層將會套用 tooall hello 帳戶中所儲存的物件。 從熱 toocool 變更 hello 儲存層將不會產生任何費用，而從 cool toohot 變更將會產生每次讀取 hello 帳戶中的所有 hello 資料 GB 成本。
6. **頻率可以變更 hello 儲存層的 我的 Blob 儲存體帳戶？**
   
    雖然我們不會強制執行限制 hello 儲存層可以變更的頻率，請留意從 cool toohot 變更 hello 儲存層會產生明顯的費用。 我們不建議您經常變更 hello 儲存層。
7. **Hello 酷炫的儲存層中的 hello blob 的行為會有所不同比 hello 的 hello 熱儲存層中？**
   
    Hello 熱儲存層中的 blob 擁有 hello 相同延遲為一般用途儲存體帳戶中的 blob。 Hello 酷炫的儲存層中的 blob 的一般用途儲存體帳戶中有以 blob 形式類似延遲 （以毫秒為單位）。
   
    Hello 酷炫的儲存層中的 blob 會比有較稍低可用性服務等級 (SLA) 儲存在 hello 熱儲存層中的 hello blob。 如需詳細資訊，請參閱 [儲存體的 SLA](https://azure.microsoft.com/support/legal/sla/storage)。
8. **可以將分頁 Blob 和虛擬機器磁碟儲存在 Blob 儲存體帳戶嗎？**
   
    Blob 儲存體帳戶僅支援區塊和附加 Blob，不支援分頁 Blob。 Azure 虛擬機器磁碟都由分頁 blob，因此 Blob 儲存體帳戶不能使用的 toostore 虛擬機器磁碟。 不過它是區塊 blob，Blob 儲存體帳戶中的 hello 虛擬機器磁碟的可能 toostore 備份。
9. **我需要 toochange 我現有的應用程式 toouse Blob 儲存體帳戶？**
   
    對區塊和附加 Blob 而言，Blob 儲存體帳戶與一般用途儲存體帳戶的 API 完全一致。 只要您的應用程式是使用區塊 blob，或附加 blob，而您使用 hello 2014-02-14 版的 hello[儲存體服務 REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx)以上應用程式應該處理。 如果您使用較舊版本的 hello 通訊協定，則您必須 tooupdate 您應用程式 toouse hello 新版本，以 toowork 順暢地搭配這兩種類型的儲存體帳戶。 一般情況下，我們一律建議使用 hello 的儲存體帳戶類型不論您使用的最新版本。
10. **使用者經驗是否會有所改變？**
    
    Blob 儲存體帳戶是用於儲存區塊的非常類似 tooa 一般用途儲存體帳戶和附加 blob，並支援所有的 hello 重要功能的 Azure 儲存體，包括高持久性和可用性、 延展性、 效能和安全性。 Hello 功能和限制特定 tooBlob 儲存體帳戶和其上方的所有項目已提出的儲存層以外其他維持 hello 相同。

## <a name="next-steps"></a>後續步驟
### <a name="evaluate-blob-storage-accounts"></a>評估 Blob 儲存體帳戶
[檢查各區域的 Blob 儲存體帳戶可用性](https://azure.microsoft.com/regions/#services)

[啟用 Azure 儲存體計量以評估您目前的儲存體帳戶使用量](storage-enable-and-view-metrics.md)

[檢查各區域的 Blob 儲存體價格](https://azure.microsoft.com/pricing/details/storage/)

[檢查資料傳輸價格](https://azure.microsoft.com/pricing/details/data-transfers/)

### <a name="start-using-blob-storage-accounts"></a>開始使用 Blob 儲存體帳戶
[開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md)

[從 Azure 儲存體移動資料 tooand](storage-moving-data.md)

[使用 AzCopy 命令列公用程式的 hello 傳輸資料](storage-use-azcopy.md)

[瀏覽及探索您的儲存體帳戶](http://storageexplorer.com/)

