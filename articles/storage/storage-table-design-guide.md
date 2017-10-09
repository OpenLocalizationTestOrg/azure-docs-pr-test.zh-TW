---
title: "儲存體資料表設計指南 aaaAzure |Microsoft 文件"
description: "在 Azure 資料表儲存體中設計可擴充且高效能的資料表"
services: storage
documentationcenter: na
author: jasonnewyork
manager: tadb
editor: tysonn
ms.assetid: 8e228b0c-2998-4462-8101-9f16517393ca
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 02/28/2017
ms.author: jahogg
ms.openlocfilehash: bbac5e83fe994c1ba1408dd43367fbcfca6a2148
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-table-design-guide-designing-scalable-and-performant-tables"></a>Azure 儲存體資料表設計指南：設計可調整且效用佳的資料表
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

toodesign 可擴充和高效能的資料表，您必須考慮許多因素，例如效能、 延展性和成本。 如果您先前所設計的關聯式資料庫結構描述，這些考量會熟悉 tooyou，但有一些 hello Azure 表格服務的儲存體模型和關聯式模型之間的相似之處，另外還有許多重要差異。 這些差異通常會導致 toovery 不同的設計，看起來可能違反直覺或錯誤 toosomeone 熟悉關聯式資料庫，但其執行進行不錯的方法，如果您要設計的 NoSQL 索引鍵/值存放區，例如 hello Azure 表格服務。 許多設計差異將會反映 hello 事實 hello 表格服務是設計的 toosupport 雲端規模應用程式可以包含數十億個實體 （在關聯式資料庫詞彙中的資料列） 的資料，或是必須支援極高的資料集交易量： 因此，您需要以不同的方式，需將資料的儲存 toothink 及了解 hello 表格服務的運作方式。 更進一步 （和較低的成本），設計良好的 NoSQL 資料存放區可以啟用方案 tooscale 比使用關聯式資料庫的解決方案。 本指南針對這些主題為您提供協助。  

## <a name="about-hello-azure-table-service"></a>關於 hello Azure 資料表服務
本章節強調一些 hello 關鍵功能 hello 表格服務會特別相關 toodesigning 的效能和延展性。 如果您是新 tooAzure 儲存體和 hello 表格服務，先閱讀[簡介 tooMicrosoft Azure 儲存體](storage-introduction.md)和[開始使用適用於.NET 的 Azure 資料表儲存體使用](storage-dotnet-how-to-use-tables.md)再讀取這個 hello 餘數發行項。 雖然本指南的 hello 焦點是 hello 表格服務，它會包含一些 hello Azure 佇列和 Blob 服務，以及您如何使用這些以及 hello 方案中的表格服務的討論。  

什麼是 hello 表格服務？ 如您預期從 hello 名稱，hello 表格服務會使用表格式格式 toostore 資料。 在 hello 標準術語，hello 資料表的每個資料列代表實體，而 hello 資料行存放區 hello 該實體的各種屬性。 每個實體有一組索引鍵 toouniquely 識別它，並用 hello 表格服務的時間戳記資料行 tootrack hello 實體上次更新時 （這會自動與您無法以手動方式覆寫 hello 時間戳記任意值）。 hello 表格服務會使用這個上次修改時間戳記 (LMT) toomanage 開放式並行存取。  

> [!NOTE]
> hello 表格服務 REST API 作業還會傳回**ETag** hello 上次修改時間戳記 (LMT) 從它衍生的值。 我們將使用這份文件中 hello 條款 ETag 和 LMT 交換因為兩者參考 toohello 相同基礎資料。  
> 
> 

hello 下列範例顯示簡單的資料表設計 toostore employee 和 department 實體。 許多 hello 範例所示稍後在本指南根據這個簡單的設計。  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td>行銷</td>
<td>00001</td>
<td>2014-08-22T00:50:32Z</td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>姓氏</th>
<th>年齡</th>
<th>電子郵件</th>
</tr>
<tr>
<td>Don</td>
<td>Hall</td>
<td>34</td>
<td>donh@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>行銷</td>
<td>00002</td>
<td>2014-08-22T00:50:34Z</td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>姓氏</th>
<th>年齡</th>
<th>電子郵件</th>
</tr>
<tr>
<td>Jun</td>
<td>Cao</td>
<td>47</td>
<td>junc@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>行銷</td>
<td>系所</td>
<td>2014-08-22T00:50:30Z</td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>行銷</td>
<td>153</td>
</tr>
</table>
</td>
</tr>
<tr>
<td>銷售</td>
<td>00010</td>
<td>2014-08-22T00:50:44Z</td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>姓氏</th>
<th>年齡</th>
<th>電子郵件</th>
</tr>
<tr>
<td>Ken</td>
<td>Kwok</td>
<td>23</td>
<td>kenk@contoso.com</td>
</tr>
</table>
</td>
</tr>
</table>


目前為止，這會非常類似 tooa 資料表關聯式資料庫中尋找具有 hello 正在 hello 強制的資料行的主要差異和 hello 能力 toostore 多個實體中的型別 hello 相同的資料表。 此外，每個這類 hello 使用者定義的屬性**FirstName**或**年齡**具有資料類型，例如整數或字串，就像關聯式資料庫中的資料行。 雖然不同於在關聯式資料庫中，屬性不需要的資料表服務表示 hello hello 無結構描述性質 hello 相同資料型別上的每個實體。 toostore 複雜資料型別，在單一屬性中的，您必須使用序列化的格式，例如 JSON 或 XML。 如需 hello 資料表服務，例如支援資料類型、 支援的日期範圍、 命名規則和大小限制的詳細資訊，請參閱[了解 hello 表格服務資料模型](http://msdn.microsoft.com/library/azure/dd179338.aspx)。

如您所見，您所選擇的**PartitionKey**和**RowKey**是基本 toogood 資料表設計。 儲存在資料表中的每個實體都必須有一個獨一無二的 **PartitionKey** 和 **RowKey** 組合。 如同關聯式資料庫資料表中的索引鍵，hello **PartitionKey**和**RowKey**的值是索引的 toocreate，可讓快速查閱叢集索引，不過，hello 表格服務不會建立任何次要索引，使這些都是 hello 只有兩個索引的屬性 （稍後說明的 hello 模式的某些顯示您可以解決此明顯的限制）。  

資料表由一或多個資料分割所組成，如您所見，hello 的許多設計的決策，您就會選擇適合周圍**PartitionKey**和**RowKey** toooptimize 您的方案。 方案可以僅由單一資料表組成 (其中組織成資料分割的所有實體)，但方案通常會有多個資料表。 資料表可幫助您 toologically 組織您的實體，協助您管理存取權 toohello 資料來使用存取控制清單，您可以卸除整個資料表，使用單一儲存體作業。  

### <a name="table-partitions"></a>資料表的資料分割
hello 帳戶名稱、 資料表名稱和**PartitionKey**一起找出 hello hello hello 表格服務儲存 hello 實體的儲存體服務中的資料分割。 正在 hello 定址配置之實體的一部分，以及資料分割定義交易的範圍 (請參閱[實體群組交易](#entity-group-transactions)下方)，以及表單的 hello 表格服務的可調整的 hello 基準。 如需分割的詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md)。  

Hello 表格服務，在個別節點服務一個或多個完成資料分割並且 hello 服務標尺的動態負載平衡節點間的資料分割。 如果節點是在負載之下，hello 表格服務可以*分割*到不同節點上的該節點所服務的 hello 範圍的資料分割; 當流量 subsides，hello 服務可以*合併*hello 資料分割的範圍是從無訊息的節點備份到單一節點上。  

如需有關 hello 的 hello 內部詳細資料表格服務，以及特別是如何 hello 服務管理資料分割，請參閱 hello 紙張[Microsoft Azure 儲存體： 高可用雲端儲存體服務具有強式一致性](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).  

### <a name="entity-group-transactions"></a>實體群組交易
在 hello 表格服務中，實體群組交易 (EGTs) 會是 hello 只有內建的機制，跨多個實體執行不可部分完成的更新。 EGTs 也會參照的 tooas*批次交易*某些文件中。 EGTs 僅能對儲存在 hello 的實體相同的資料分割 (共用 hello 給定資料表中的相同資料分割索引鍵)，所以每當您需要跨多個實體的不可部分完成的交易行為您需要這些實體是位於 hello 的 tooensure 相同的資料分割。 這通常是將多個實體類型保留在 hello 相同資料表 （和資料分割），並且不使用不同的實體類型的多個資料表的原因。 單一 EGT 最多可以操作 100 個實體。  如果您送出多個並行 EGTs 處理是重要的 tooensure 這些 EGTs 不會被操作上是常見跨 EGTs 否則處理可能會因為延遲的實體。

EGTs 也會導入 tooevaluate 在設計中潛在的取捨： 使用多個資料分割會增加應用程式的 hello 延展性，因為 Azure 有更多的機會，負載平衡要求到節點，但這可能會限制 hello您的應用程式 tooperform 不可部分完成交易的能力和維護您資料的強式一致性。 此外，有特定的延展性目標層級 hello 的磁碟分割，可能會限制 hello 輸送量的交易，您可以預期會發生的單一節點： 如需有關 hello Azure 儲存體帳戶和 hello 資料表的延展性目標服務，請參閱[Azure 儲存體延展性和效能目標](storage-scalability-targets.md)。 本指南稍後的章節討論各種設計策略，協助您管理此類，取捨，並討論如何 toochoose 您的資料分割索引鍵根據 hello 特定需求的用戶端應用程式。  

### <a name="capacity-considerations"></a>容量考量
hello 下表包含一些 hello 索引鍵值 toobe 注意當您設計的資料表服務方案：  

| Azure 儲存體帳戶的容量總計 | 500 TB |
| --- | --- |
| Azure 儲存體帳戶中的資料表數目 |僅限於 hello hello 儲存體帳戶容量 |
| 資料表中的資料分割數目 |僅限於 hello hello 儲存體帳戶容量 |
| 資料分割中的實體數目 |僅限於 hello hello 儲存體帳戶容量 |
| 個別實體的大小 |向上 too1 MB，最多 255 個屬性 (包括 hello **PartitionKey**， **RowKey**，和**時間戳記**) |
| 大小的 hello **PartitionKey** |向上 too1 KB 大小的字串 |
| 大小的 hello **RowKey** |向上 too1 KB 大小的字串 |
| 實體群組交易的大小 |交易可以包含最多 100 個實體，而且 hello 承載必須小於 4 MB 的大小。 一個 EGT 只能更新實體一次。 |

如需詳細資訊，請參閱[了解 hello 表格服務資料模型](http://msdn.microsoft.com/library/azure/dd179338.aspx)。  

### <a name="cost-considerations"></a>成本考量
資料表儲存體比較便宜，但您應該包含這兩個容量使用方式與 hello 數量的交易的成本估計值做為評估版的 hello 表格服務會使用任何解決方案的一部分。 不過，在許多案例中將反正規化或重複的資料儲存在順序 tooimprove hello 效能或延展性，您是方案的有效的方法 tootake。 如需定價的詳細資訊，請參閱 [Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/)。  

## <a name="guidelines-for-table-design"></a>資料表設計指導方針
這些清單摘要的一些 hello 主要的方針，您應該記住當您要設計您的資料表，與本指南會解決所有中更詳細地更新版本。 這些方針有非常不同於您通常會依照關聯式資料庫設計的 hello 指導方針。  

設計您的資料表服務方案 toobe*讀取*有效率：

* ***設計大量讀取應用程式中的查詢。*** 當您在設計您的資料表時，思考 hello 查詢 （特別是 hello 延遲敏感的），以執行您的想法方式，就會更新您的實體之前。 透過這樣的方式，通常可造就一個有效率且高效能的解決方案。  
* ***在查詢中同時指定 PartitionKey 和 RowKey。*** *點查詢*之類這些 hello 最有效率的資料表服務查詢。  
* ***考慮儲存重複的實體副本。*** 資料表儲存體是廉價因此請考慮儲存 hello 同一個實體多次 （具有不同索引鍵） tooenable 更有效率的查詢。  
* ***考慮將資料反正規化。*** 資料表儲存體十分便宜，所以建議您考慮將資料反正規化。 例如，儲存摘要實體的彙總資料的查詢只需要 tooaccess 單一實體。  
* ***使用複合索引鍵值。*** hello 只有您所擁有的索引鍵是**PartitionKey**和**RowKey**。 例如，使用複合的索引鍵值 tooenable 替代索引鍵的存取路徑 tooentities。  
* ***使用查詢預測。*** 您可以減少 hello 您使用查詢，選取剛才 hello 欄位，您需要傳送 hello 網路上的資料量。  

設計您的資料表服務方案 toobe*寫入*有效率：  

* ***不要建立熱分割。*** 選擇您的要求 toospread 可讓您的索引鍵之間的任何時間點上的多個資料分割。  
* ***避免流量尖峰。*** 平滑 hello 流量透過合理的時間，並避免的流量尖峰。
* ***不一定要為每個實體的類型建立個別的資料表。*** 當您在實體類型之間都需要不可部分完成交易時，您可以儲存這些多個實體類型中相同資料分割中 hello hello 相同的資料表。
* ***請考慮 hello 必須達到的最大輸送量。*** 您必須留意 hello hello 表格服務的延展性目標，並確保您的設計將不會造成您 tooexceed 它們。  

當您閱讀本指南時，您會看到將這些原則全都納入實作的範例。  

## <a name="design-for-querying"></a>查詢的設計
需要大量、 密集寫入的磁碟或 hello 兩者的混合，可能會讀取資料表服務解決方案。 在設計您的資料表服務 toosupport 有效率地讀取作業時，本節將著重於 hello 事項 toobear 記住。 一般而言，支援有效讀取作業的設計，也可兼顧寫入作業的效率。 不過，有其他考量 toobear 記住當設計 toosupport 寫入作業，hello 下一節中討論[設計用於資料修改](#design-for-data-modification)。

設計您的資料表服務方案 tooenable 很好的起點 tooread 資料有效率地為 tooask"何種查詢將我的應用程式需要 tooexecute tooretrieve hello 資料需要從 hello 表格服務 」？  

> [!NOTE]
> 以 hello 表格服務，請務必 tooget hello 正確設計最前面位置，所以它會發生困難而且昂貴 toochange 於稍後。 例如，在關聯式資料庫中通常很可能 tooaddress 效能問題，只要加入索引 tooan 現有資料庫： 這不是以 hello 表格服務的選項。  
> 
> 

本節著重於 hello 設計來查詢資料表時，您必須解決的重要問題。 本章節涵蓋的 hello 主題包括：

* [您選擇的 PartitionKey 和 RowKey 對查詢效能有何影響](#how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance)
* [選擇適當的 PartitionKey](#choosing-an-appropriate-partitionkey)
* [最佳化 hello 表格服務的查詢](#optimizing-queries-for-the-table-service)
* [在 hello 表格服務中排序資料](#sorting-data-in-the-table-service)

### <a name="how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance"></a>您選擇的 PartitionKey 和 RowKey 對查詢效能有何影響
hello 下列範例會假設 hello 表格服務會儲存員工實體具有下列結構的 hello (大部分 hello 範例省略 hello**時間戳記**為了清楚起見屬性):  

| *資料行名稱* | *資料類型* |
| --- | --- |
| **PartitionKey** (部門名稱) |String |
| **RowKey** (員工識別碼) |String |
| **名字** |String |
| **姓氏** |String |
| **年齡** |Integer |
| **EmailAddress** |String |

hello 前一節[Azure 資料表服務概觀](#overview)描述一些 hello 的主要功能 hello Azure 表格服務具有直接影響查詢的設計。 這是因為在 hello 設計資料表服務查詢的一般指導方針。 請注意，用在 hello 以下範例中的 hello 篩選語法與 hello 表格服務 REST API 的詳細資訊，請參閱[查詢實體](http://msdn.microsoft.com/library/azure/dd179421.aspx)。  

* A***點查詢***hello 最有效查閱 toouse，而且建議 toobe 用於高容量查閱或需要最低延遲的查閱。 這類查詢可以非常有效率的方式使用 hello 索引 toolocate 個別的實體，藉由指定 兩者 hello **PartitionKey**和**RowKey**值。 例如：$filter=(PartitionKey eq 'Sales') and (RowKey eq '2')  
* 第二個最是***範圍查詢***使用 hello **PartitionKey**和篩選的範圍上**RowKey**值 tooreturn 多個實體。 hello **PartitionKey**值，識別特定的資料分割，以及 hello **RowKey**值會識別該資料分割中的 hello 實體的子集。 例如：$filter=PartitionKey eq 'Sales' and RowKey ge 'S' and RowKey lt 'T'  
* 第三個最佳是***資料分割掃描***使用 hello **PartitionKey**和另一個非索引鍵屬性，而且該篩選可能會傳回一個以上的實體。 hello **PartitionKey**值會識別特定資料分割，以及 hello 屬性值，則選取該資料分割中的 hello 實體的子集。 例如：$filter=PartitionKey eq 'Sales' and LastName eq 'Smith'  
* A***資料表掃描***不包含 hello **PartitionKey**和就非常沒有效率，因為它會搜尋所有組成您的資料表，接著的所有相符實體的 hello 磁碟分割。 它會執行資料表掃描，不論您的篩選器是否使用 hello **RowKey**。 例如：$filter=LastName eq 'Jones'  
* 傳回多個實體的查詢，在傳回時會以 **PartitionKey** 和 **RowKey** 順序排序。 選擇 tooavoid hello client 中的，就可以做到 hello 實體**RowKey**定義 hello 最常見的排序次序。  

請注意，使用"**或**"篩選器根據的 toospecify **RowKey**值產生資料分割掃描並不會被視為範圍查詢。 因此，您應該避免會使用下列篩選條件的搜尋：例如 $filter=PartitionKey eq 'Sales' and (RowKey eq '121' or RowKey eq '322')  

如需使用 hello 儲存體用戶端程式庫 tooexecute 有效率的查詢的用戶端程式碼範例，請參閱：  

* [執行點查詢使用 hello 儲存體用戶端程式庫](#executing-a-point-query-using-the-storage-client-library)
* [使用 LINQ 擷取多個實體](#retrieving-multiple-entities-using-linq)
* [伺服器端預測](#server-side-projection)  

如需範例，可以處理多個實體的用戶端程式碼的型別儲存在 hello 相同資料表中，請參閱：  

* [使用異質性實體類型](#working-with-heterogeneous-entity-types)  

### <a name="choosing-an-appropriate-partitionkey"></a>選擇適當的 PartitionKey
您所選擇的**PartitionKey**應該平衡 hello 需要 tooenables hello 使用 EGTs （tooensure 一致性） hello 需求 toodistribute 對您的實體之間的多個資料分割 (tooensure 靈活的解決方案)。  

其中一種方式，您可以在單一磁碟分割，儲存您的實體，但這可能會限制您的方案 hello 延展性，並可避免 hello 表格服務進行可以 tooload 平衡要求。 在 hello 其他極端的做法是，您可以儲存一個實體，每個資料分割，這會是可高度擴充和讓 hello 資料表服務 tooload 平衡要求，但這會讓您無法使用實體群組交易。  

最理想的**PartitionKey**是指 toouse 有效率的查詢可讓您和您的方案具有足夠的磁碟分割 tooensure 延展性功能。 一般而言，您會發現您的實體將具有適當的屬性，可將您的實體分散到足夠的磁碟分割。

> [!NOTE]
> 例如，在儲存使用者或員工相關資訊的系統中，UserID 可以是一個良好的 PartitionKey。 您可能需要數個指定的使用者識別碼做為 hello 資料分割索引鍵的實體。 儲存使用者相關資料的每個實體會分組到單一資料分割，因此這些實體可透過實體群組交易來存取，同時仍具有高擴充性。
> 
> 

還有其他考量，在您選擇的**PartitionKey** toohow 會插入、 更新和刪除實體相關的： hello 參閱[設計用於資料修改](#design-for-data-modification)下方。  

### <a name="optimizing-queries-for-hello-table-service"></a>最佳化 hello 表格服務的查詢
hello 表格服務會自動索引您的實體使用 hello **PartitionKey**和**RowKey**值中的單一叢集索引，因此 hello 點查詢是 hello toouse 最有效率的原因. 不過，有一些 hello hello 上的叢集索引沒有索引以外， **PartitionKey**和**RowKey**。

許多設計必須符合需求 tooenable 查閱的多個準則為基礎的實體。 比方說，根據電子郵件、員工識別碼或姓氏找出員工實體。 下列 hello > 一節中的模式 hello[資料表設計模式](#table-design-patterns)解決這些類型的需求，並描述的 hello 事實 hello 表格服務不會提供次要索引的解決方式：  

* [內部資料分割的次要索引模式](#intra-partition-secondary-index-pattern)-儲存多個複本的每一個實體使用不同**RowKey**值 (hello 中相同的資料分割) tooenable 快速又有效率查閱和替代排序所使用的訂單不同**RowKey**值。  
* [間的資料分割的次要索引模式](#inter-partition-secondary-index-pattern)-儲存多個複本的每個實體使用不同 RowKey 值在不同的磁碟分割或個別的資料表 tooenable 快速並有效查閱和替代排序訂單使用不同的**RowKey**值。  
* [索引實體模式](#index-entities-pattern)-維護索引實體 tooenable 有效率的搜尋傳回的實體清單。  

### <a name="sorting-data-in-hello-table-service"></a>在 hello 表格服務中排序資料
hello 表格服務會傳回以遞增方式排序依據的實體**PartitionKey**再依據**RowKey**。 這些金鑰為字串值和數字值正確地排序的 tooensure 應該 tooa 固定長度轉換成，它們填補零。 例如，如果 hello 員工識別碼值您做 hello **RowKey**是整數值，您應將轉換成員工識別碼**123**太**00000123**。  

許多應用程式有 toouse 資料排序順序不同的需求： 例如，排序員工，依名稱，或加入日期。 下列 hello > 一節中的模式 hello[資料表設計模式](#table-design-patterns)定址實體 tooalternate 排序順序的方式：  

* [內部資料分割的次要索引模式](#intra-partition-secondary-index-pattern)-儲存每個實體使用不同 RowKey 值的多個複本 (hello 中相同的資料分割) tooenable 快速又有效率查閱和替代排序訂單使用的不同 RowKey 值。  
* [間的資料分割的次要索引模式](#inter-partition-secondary-index-pattern)-存放區使用不同 RowKey 值快速 tooenable 個別的資料表中的個別資料分割中每個實體的多個複本，並使用不同 RowKey 的有效率查閱和替代排序訂單值。
* [記錄檔結尾模式](#log-tail-pattern)-擷取 hello  *n* 實體最近加入 tooa 資料分割使用**RowKey**以反向的日期和時間順序排序的值。  

## <a name="design-for-data-modification"></a>資料修改的設計
本節著重於 hello 設計考量最佳化插入、 更新和刪除。 在某些情況下，您需要針對查詢最佳化的資料修改，就像您一樣的關聯式資料庫設計 （雖然 hello 方法來管理 hello 設計的設計最佳化的設計之間 tooevaluate hello 取捨缺點是關聯式資料庫中不同）。 hello 區段[資料表設計模式](#table-design-patterns)描述 hello 表格服務的一些詳細的設計模式，並強調一些這些取捨當中。 在實務上，您會發現許多針對查詢實體而最佳化的設計也適用於修改實體。  

### <a name="optimizing-hello-performance-of-insert-update-and-delete-operations"></a>Hello 效能最佳化的 insert、 update 和 delete 作業
tooupdate 或刪除實體，您必須是能夠 tooidentify 它使用 hello **PartitionKey**和**RowKey**值。 在這一方面，您所選擇的**PartitionKey**和**RowKey**修改實體應該遵循的類似準則 tooyour 選擇 toosupport 點查詢，因為您想要為 tooidentify 實體盡可能有效率地。 您不想 toouse 效率不佳的磁碟分割或資料表掃描 toolocate 順序 toodiscover hello 中的實體**PartitionKey**和**RowKey**值需要 tooupdate，或將它刪除。  

下列 hello > 一節中的模式 hello[資料表設計模式](#table-design-patterns)解決 hello，最佳化效能，或插入、 更新和刪除作業：  

* [高容量刪除模式](#high-volume-delete-pattern)-啟用 hello 刪除大量實體藉由在自己的個別資料表中儲存為同時刪除所有 hello 實體; 您刪除 hello 實體 hello 資料表中刪除。  
* [資料序列模式](#data-series-pattern)-存放區完整的資料數列中要求您進行的單一實體 toominimize hello 數字。  
* [寬實體模式](#wide-entities-pattern)-以上 252 屬性搭配使用多個實體的實體 toostore 邏輯實體。  
* [大型實體模式](#large-entities-pattern)-使用 blob 儲存體 toostore 大型屬性值。  

### <a name="ensuring-consistency-in-your-stored-entities"></a>確保預存實體中的一致性
hello 其他的最佳化資料修改會影響您所選擇的索引鍵的關鍵因素如何 tooensure 使用不可部分完成交易的一致性。 您只能使用實體儲存在 hello EGT toooperate 相同的資料分割。  

下列 hello > 一節中的模式 hello[資料表設計模式](#table-design-patterns)管理一致性的位址：  

* [內部資料分割的次要索引模式](#intra-partition-secondary-index-pattern)-儲存多個複本的每一個實體使用不同**RowKey**值 (hello 中相同的資料分割) tooenable 快速又有效率查閱和替代排序所使用的訂單不同**RowKey**值。  
* [間的資料分割的次要索引模式](#inter-partition-secondary-index-pattern)-儲存多個複本的每個實體使用不同 RowKey 值在不同的磁碟分割或個別的資料表 tooenable 快速並有效查閱和替代排序訂單使用不同的**RowKey**值。  
* [最終一致的交易模式](#eventually-consistent-transactions-pattern) - 使用 Azure 佇列，跨資料分割界限或儲存體系統界限啟用最終一致的行為。
* [索引實體模式](#index-entities-pattern)-維護索引實體 tooenable 有效率的搜尋傳回的實體清單。  
* [非正規化模式](#denormalization-pattern)-合併的相關資料一起在單一實體 tooenable 您 tooretrieve 所有 hello 您需要使用單點查詢的資料。  
* [資料序列模式](#data-series-pattern)-存放區完整的資料數列中要求您進行的單一實體 toominimize hello 數字。  

如需實體群組交易資訊，請參閱 hello 節[實體群組交易](#entity-group-transactions)。  

### <a name="ensuring-your-design-for-efficient-modifications-facilitates-efficient-queries"></a>確保您針對有效率的修改所做的設計有助於提升查詢效率
在許多情況下，有效率的查詢結果中有效的修改，但您的設計應該一律評估是否這是您的特定案例的 hello 狀況。 某些 hello > 一節中的 hello 模式[資料表設計模式](#table-design-patterns)明確評估查詢及修改實體之間的利弊得失，您應該一律納入帳戶 hello 數目每種作業類型。  

下列 hello > 一節中的模式 hello[資料表設計模式](#table-design-patterns)位址之間的有效率的查詢設計和設計有效率的資料修改的利弊得失：  

* [複合索引鍵模式](#compound-key-pattern)-使用複合**RowKey**值 tooenable 用戶端 toolookup 相關資料的單一點查詢。  
* [記錄檔結尾模式](#log-tail-pattern)-擷取 hello  *n* 實體最近加入 tooa 資料分割使用**RowKey**以反向的日期和時間順序排序的值。  

## <a name="encrypting-table-data"></a>加密資料表的資料
hello.NET Azure 儲存體用戶端程式庫支援加密的字串插入的實體屬性和取代作業。 hello 加密字串 hello 服務上儲存為二進位屬性，而它們會轉換後 toostrings 解密之後。    

對於資料表，此外 toohello 加密原則，使用者必須指定 hello 屬性 toobe 加密。 作法是指定 [EncryptProperty] 屬性 (針對衍生自 TableEntity 的 POCO 實體)，或在要求選項中指定加密解析程式。 加密解析程式是委派，接受資料分割索引鍵、資料列索引鍵和屬性名稱，然後傳回布林值，指出是否應該加密該屬性。 在加密期間，是否應該加密屬性，同時寫入 toohello 網路 hello 用戶端程式庫時，會使用此資訊 toodecide。 hello 委派也提供 hello 可能性的邏輯屬性加密的方式。 (例如，如果 X，則加密屬性 A，否則加密屬性 A 和 B。)請注意，就是不必要的 tooprovide 讀取或查詢實體時此資訊。

請注意目前不支援合併。 屬性的子集可能已加密先前使用不同的金鑰，因為只要合併 hello 新內容，並更新 hello 中繼資料會導致資料遺失。 合併 需要進行額外的服務從 hello 服務呼叫 tooread hello 預先存在的實體，或使用每個屬性的新機碼，這兩者都不適用基於效能的考量。     

如需加密資料表資料的相關資訊，請參閱 [Microsoft Azure 儲存體的用戶端加密和 Azure 金鑰保存庫](storage-client-side-encryption.md)。  

## <a name="modelling-relationships"></a>模型化關聯性
建立網域模型是 hello 設計複雜系統的關鍵步驟。 一般而言，使用模型處理程序 tooidentify 實體 hello 和 hello 商務網域 hello 兩者為方法 toounderstand 間的關聯性，並通知 hello 設計您的系統。 本節著重於轉譯 hello hello 表格服務的網域模型 toodesigns 中找到常見關聯性類型。 從邏輯資料模型 tooa 實體基礎的 NoSQL 資料模型對應 hello 程序是設計在關聯式資料庫時使用與非常不同。 關聯式資料庫設計通常會假設資料正規化的程序，針對最小化備援 – 和宣告式的查詢功能的摘要方式 hello 實作 hello 資料庫的運作方式的最佳化。  

### <a name="one-to-many-relationships"></a>一對多關聯性
商業網域物件之間常會產生一對多關聯性：例如，一個部門有許多員工。 表格服務每個與專業人員和可能相關 toohello 特定案例的優缺點 hello 中有數種方式 tooimplement 一對多關聯性。  

請考慮數以萬計的部門和員工實體，其中每個部門各有許多員工以及每位員工與一個特定部門相關聯的大型多國 hello 範例。 其中一個方法是 toostore 不同部門 」 和 「 員工實體，這類：  

![][1]

這個範例會示範根據 hello hello 型別之間隱含的一對多關聯性**PartitionKey**值。 每個部門可以有許多員工。  

此範例也示範 department 實體，並在其相關的員工實體 hello 相同的資料分割。 您可以選擇 toouse 不同資料分割、 資料表或甚至 hello 不同的實體類型的儲存體帳戶。  

另一個方法是 toodenormalize 資料與存放區唯一的員工實體未標準化的部門資料 hello 下列範例所示。 在特定案例中，這個反正規化的方法可能無法最佳 hello 如果您需要部門經理需求 toobe 無法 toochange hello 詳細資料，因為 toodo 這需要 tooupdate hello 部門中的每一位員工。  

![][2]

如需詳細資訊，請參閱 hello[非正規化模式](#denormalization-pattern)本指南稍後的。  

hello 下表摘要說明 hello 優缺點的每個儲存員工和部門有一對多關聯性的實體的上述 hello 方法。 您也應該考慮您預期的頻率 tooperform 各種作業： 可能是可接受 toohave 包括昂貴的作業，如果該作業只會發生不常的設計。  

<table>
<tr>
<th>方法</th>
<th>優點</th>
<th>缺點</th>
</tr>
<tr>
<td>個別的實體類型、相同的資料分割、相同的資料表</td>
<td>
<ul>
<li>您可以使用單一作業更新部門實體。</li>
<li>如果您有需求 toomodify department 實體，您可以使用 EGT toomaintain 一致性每當您更新/插入/刪除的員工實體。 例如，假設您維護每個部門的部門員工計數。</li>
</ul>
</td>
<td>
<ul>
<li>可能需要 tooretrieve 同時使用 employee 和 department 實體，對於某些用戶端活動。</li>
<li>儲存體作業中發生 hello 相同資料分割。 在交易量偏高時，這可能會導致熱點。</li>
<li>您無法移動使用 EGT 員工的 tooa 新部門。</li>
</ul>
</td>
</tr>
<tr>
<td>個別的實體類型、不同的資料分割或資料表或儲存體帳戶</td>
<td>
<ul>
<li>您可以使用單一作業更新部門實體或員工實體。</li>
<li>在大量交易的磁碟區，這可能有助於在多個資料分割之間散佈 hello 負載。</li>
</ul>
</td>
<td>
<ul>
<li>可能需要 tooretrieve 同時使用 employee 和 department 實體，對於某些用戶端活動。</li>
<li>您無法使用 EGTs toomaintain 一致性時您更新/插入/刪除員工和更新的部門。 例如，更新某個部門實體中的員工計數。</li>
<li>您無法移動使用 EGT 員工的 tooa 新部門。</li>
</ul>
</td>
</tr>
<tr>
<td>去正規化為單一實體類型</td>
<td>
<ul>
<li>您可以擷取與單一要求所需的所有 hello 資訊。</li>
</ul>
</td>
<td>
<ul>
<li>如果您需要 tooupdate 部門資訊 （這需要您 tooupdate 所有 hello 員工在部門），可能高度耗費資源的 toomaintain 一致性。</li>
</ul>
</td>
</tr>
</table>

如何選擇這些選項，與其中一個 hello 專業人員之間及缺點是最重要的是，取決於特定應用程式案例。 例如，頻率您修改部門實體;您的所有員工查詢都需要 hello 其他部門資訊; 嗎如何關閉是否 toohello 分割區或儲存體帳戶的延展性限制？  

### <a name="one-to-one-relationships"></a>一對一關聯性
網域模型的實體之間可能會包含一對一關聯性。 如果您需要 tooimplement hello 表格服務中的一對一關聯性，您也必須選擇在需要時 tooretrieve 這兩個 toolink hello 兩個相關的實體的方式。 這個連結可以是隱含、 根據慣例，以在 hello 索引鍵值，或明確 hello 形式儲存連結**PartitionKey**和**RowKey**中每個實體 tooits 值相關實體。 如需您是否應該儲存 hello 的討論相關實體在 hello 相同的資料分割，請參閱 hello 節[一對多關聯性](#one-to-many-relationships)。  

請注意，有也可能會導致您 tooimplement 一對一關聯性中 hello 表格服務的實作考量：  

* 處理大型實體 (如需詳細資訊，請參閱 [大型實體模式](#large-entities-pattern))。  
* 實作存取控制 (如需詳細資訊，請參閱 [使用共用存取簽章控制存取](#controlling-access-with-shared-access-signatures))。  

### <a name="join-in-hello-client"></a>加入在 hello 用戶端
雖然 hello 表格服務有方式 toomodel 關聯性，您應該記住 hello 兩個主要的原因 hello 表格服務的使用是延展性和效能。 如果您發現模型許多危害 hello 效能和延展性的方案的關聯性，您應該請詢問自己是否必要 toobuild 所有 hello 到資料表設計的資料關聯性。 您可能是無法 toosimplify hello 設計，並且改善 hello 延展性和效能的方案，如果您讓用戶端應用程式執行任何必要的聯結。  

比方說，如果您有小型的資料表，其中包含不經常變更的資料，然後您可以使用一次擷取這項資料而 hello 用戶端上快取它。 這樣做可避免重複的往返 tooretrieve hello 相同的資料。 在 hello 範例中我們已經探討本指南中，hello 組的小型組織中的部門可可能 toobe 小且不常很適合做為用戶端應用程式可以下載一次的資料和快取做為查閱資料的變更。  

### <a name="inheritance-relationships"></a>繼承關聯性
如果用戶端應用程式使用一組形成部分繼承關聯性 toorepresent 商務實體的類別，您可以輕鬆地保存 hello 表格服務中的這些實體。 例如，您可能必須遵循一組類別定義在用戶端應用程式中的 hello 其中**人員**是 abstract 類別。

![][3]

您可以保存 hello 兩個實體的類別在 hello 使用單一的 Person 資料表，使用實體中看起來像這樣的表格服務的執行個體：  

![][4]

如需使用的 hello 相同用戶端程式碼中的資料表中的多個實體類型的詳細資訊，請參閱 hello 節[使用異質實體類型](#working-with-heterogeneous-entity-types)本指南稍後的。 這會提供如何 toorecognize hello 用戶端程式碼中的實體類型的範例。  

## <a name="table-design-patterns"></a>資料表設計模式
在先前章節中，您已經知道某些詳細的討論如何 toooptimize 資料表設計這兩個擷取的實體資料，使用查詢與插入、 更新和刪除實體資料。 本節將說明一些適用於資料表服務方案的模式。 此外，您會看到您可以實際上定址方式的一些 hello 問題和缺點引發先前在本指南中。 hello 圖摘要說明 hello hello 不同模式之間的關聯性：  

![][5]

上面的 hello 模式對應反白顯示的某些模式 （藍色） 與本指南中所述的反向模式 （橘色） 之間的關聯性。 當然還有許多其他模式也值得考量。 例如，表格服務的 hello 重要案例的其中一個是 toouse hello[具體化檢視模式](https://msdn.microsoft.com/library/azure/dn589782.aspx)從 hello[命令查詢責任隔離 (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx)模式。  

### <a name="intra-partition-secondary-index-pattern"></a>內部資料分割次要索引模式
儲存多個複本的每一個實體使用不同**RowKey**值 (hello 中相同的資料分割) 使用不同的訂單 tooenable 快速又有效率查閱和替代排序**RowKey**值。 複本之間的更新可以使用 EGT 保持一致。  

#### <a name="context-and-problem"></a>內容和問題
hello 表格服務會自動索引使用 hello 實體**PartitionKey**和**RowKey**值。 這可讓用戶端應用程式 tooretrieve 有效率地使用這些值的實體。 例如，使用 hello 資料表結構，如下所示，用戶端應用程式可以使用點查詢 tooretrieve 個別員工實體使用 hello 部門名稱和 hello 員工識別碼 (hello **PartitionKey**和**RowKey**值)。 用戶端也可以擷取每個部門內以員工識別碼排序的實體。

![][6]

如果您也想 toobe 無法 toofind 根據 hello 另一個屬性值，例如電子郵件地址的員工實體，您必須使用效率較低的資料分割掃描 toofind 相符項目。 這是因為 hello 表格服務不會提供次要索引。 此外，沒有任何選項 toorequest 以不同順序排序的員工清單**RowKey**順序。  

#### <a name="solution"></a>方案
toowork 周圍 hello 缺乏次要索引，您可以儲存多個複本的每個實體，以使用不同的每個複本**RowKey**值。 如果您儲存實體 hello 結構如下所示，您就可以有效率地擷取根據電子郵件地址或員工識別碼的員工實體。hello hello 的前置詞值**RowKey**，"empid_"和"email_ 」 可讓您 tooquery 一位員工或員工的範圍使用的電子郵件地址或員工識別碼範圍。  

![][7]

下列兩個 （一個查閱的員工識別碼和一個依電子郵件地址查閱） 的篩選準則的 hello 同時指定點查詢：  

* $filter=(PartitionKey eq 'Sales') and (RowKey eq 'empid_000223')  
* $filter=(PartitionKey eq 'Sales') and (RowKey eq 'email_jonesj@contoso.com')  

如果您查詢某一範圍的員工實體，您可以指定範圍依員工識別碼排序或藉由查詢的實體中 hello hello 適當的前置詞以電子郵件地址順序排序的範圍**RowKey**。  

* toofind hello 具有所有員工 hello 銷售部門的員工識別碼 hello 範圍 000100 too000199 中都使用： $filter = (PartitionKey eq 'Sales') 與 (RowKey ge 'empid_000100') 和 (RowKey le 'empid_000199')  
* 所有電子郵件地址開頭為 hello 與 hello hello 銷售部門的員工 toofind 字母 'a' 的使用： $filter = (PartitionKey eq 'Sales') 與 (RowKey ge 'email_a') 和 (RowKey lt 'email_b')  
  
  請注意，上述的 hello 範例中使用的 hello 篩選語法與 hello 表格服務 REST API 的詳細資訊，請參閱[查詢實體](http://msdn.microsoft.com/library/azure/dd179421.aspx)。  

#### <a name="issues-and-considerations"></a>問題和考量
請考慮 hello 時決定下列點如何 tooimplement 這種模式：  

* 資料表儲存體是相對低廉 toouse 因此 hello 成本負擔的儲存重複的資料不應該是主要的考量。 不過，您應該一定會評估 hello 成本您根據您的的儲存需求的設計，並只能新增重複的實體 toosupport hello 查詢將會執行用戶端應用程式。  
* 由於 hello 次要索引的實體儲存在 hello 相同資料分割以 hello 原始實體中，您應確定不會超過 hello 個別的資料分割的延展性目標。  
* 您可以將重複的實體彼此一致以不可分割方式使用 EGTs tooupdate hello 兩份 hello 實體。 這表示，您應該將實體的所有複本都存放在 hello 相同的資料分割。 如需詳細資訊，請參閱 hello 節[使用實體群組交易](#entity-group-transactions)。  
* hello 值為 hello **RowKey**必須是唯一的每個實體。 請考慮使用複合索引鍵值。  
* 填補數值 hello **RowKey** （例如 hello 員工識別碼 000223），可讓更正排序和篩選依據的上下限之間。  
* 您不一定需要 tooduplicate 所有 hello 屬性的實體。 例如，如果 hello 查閱 hello 實體使用 hello 電子郵件的查詢以處理 hello **RowKey**永遠都不需要 hello 員工的年齡，這些實體可能會有下列結構的 hello:

![][8]

* 通常更好的 toostore 重複的資料，並確保您可以擷取您需要使用單一查詢的所有 hello 資料，比 toouse 一個查詢 toolocate 實體和另一個 toolookup hello 所需的資料。  

#### <a name="when-toouse-this-pattern"></a>當 toouse 此模式
當用戶端應用程式需要使用各種不同的金鑰，當您的用戶端需要不同排序順序中的 tooretrieve 實體 tooretrieve 實體以及您可以識別每個使用不同的唯一值的實體，請使用此模式。 不過，您應該確定您要執行 hello 不同實體查閱時請不要超過 hello 資料分割的延展性限制**RowKey**值。  

#### <a name="related-patterns-and-guidance"></a>相關的模式和指導方針
hello 下列模式和指導方針也可能是相關實作此模式時：  

* [間分割次要索引模式](#inter-partition-secondary-index-pattern)
* [複合索引鍵模式](#compound-key-pattern)
* [實體群組交易](#entity-group-transactions)
* [使用異質性實體類型](#working-with-heterogeneous-entity-types)

### <a name="inter-partition-secondary-index-pattern"></a>間資料分割次要索引模式
儲存多個複本的每一個實體使用不同**RowKey**值不同的磁碟分割或個別資料表 tooenable 快速又有效率查閱，以及使用不同的替代排序次序**RowKey**值。  

#### <a name="context-and-problem"></a>內容和問題
hello 表格服務會自動索引使用 hello 實體**PartitionKey**和**RowKey**值。 這可讓用戶端應用程式 tooretrieve 有效率地使用這些值的實體。 例如，使用 hello 資料表結構，如下所示，用戶端應用程式可以使用點查詢 tooretrieve 個別員工實體使用 hello 部門名稱和 hello 員工識別碼 (hello **PartitionKey**和**RowKey**值)。 用戶端也可以擷取每個部門內以員工識別碼排序的實體。  

![][9]

如果您也想 toobe 無法 toofind 根據 hello 另一個屬性值，例如電子郵件地址的員工實體，您必須使用效率較低的資料分割掃描 toofind 相符項目。 這是因為 hello 表格服務不會提供次要索引。 此外，沒有任何選項 toorequest 以不同順序排序的員工清單**RowKey**順序。  

您會預期極大量的交易，針對這些實體，而且想 toominimize hello 風險的 hello 節流設定您的用戶端的表格服務。  

#### <a name="solution"></a>方案
toowork 周圍 hello 缺乏次要索引，您可以儲存多個複本的每個實體，每個複本使用不同**PartitionKey**和**RowKey**值。 如果您儲存實體 hello 結構如下所示，您就可以有效率地擷取根據電子郵件地址或員工識別碼的員工實體。hello hello 的前置詞值**PartitionKey**，"empid_"和"email_ 」 可讓您 tooidentify 索引您要查詢 toouse。  

![][10]

下列兩個 （一個查閱的員工識別碼和一個依電子郵件地址查閱） 的篩選準則的 hello 同時指定點查詢：  

* $filter=(PartitionKey eq 'empid_Sales') and (RowKey eq '000223')
* $filter=(PartitionKey eq 'email_Sales') and (RowKey eq 'jonesj@contoso.com')  

如果您查詢某一範圍的員工實體，您可以指定範圍依員工識別碼排序或藉由查詢的實體中 hello hello 適當的前置詞以電子郵件地址順序排序的範圍**RowKey**。  

* 所有 hello 中的員工的 toofind hello 與員工識別碼 hello 範圍中的銷售部門**000100**太**000199**依照員工識別碼順序使用： $filter = (PartitionKey eq ' empid_Sales') 和 (RowKey ge '000100') 和 (RowKey le '000199')  
* toofind hello 開頭為 'a' 以電子郵件地址的銷售部門的所有 hello 員工電子都郵件地址順序使用： $filter = (PartitionKey eq ' email_Sales') 和 (RowKey ge 'a') 和 (RowKey lt 'b')  

請注意，上述的 hello 範例中使用的 hello 篩選語法與 hello 表格服務 REST API 的詳細資訊，請參閱[查詢實體](http://msdn.microsoft.com/library/azure/dd179421.aspx)。  

#### <a name="issues-and-considerations"></a>問題和考量
請考慮 hello 時決定下列點如何 tooimplement 這種模式：  

* 您可以保留重複的實體彼此最終一致使用 hello[最終保持一致的交易模式](#eventually-consistent-transactions-pattern)toomaintain hello 主要和次要索引實體。  
* 資料表儲存體是相對低廉 toouse 因此 hello 成本負擔的儲存重複的資料不應該是主要的考量。 不過，您應該一定會評估 hello 成本您根據您的的儲存需求的設計，並只能新增重複的實體 toosupport hello 查詢將會執行用戶端應用程式。  
* hello 值為 hello **RowKey**必須是唯一的每個實體。 請考慮使用複合索引鍵值。  
* 填補數值 hello **RowKey** （例如 hello 員工識別碼 000223），可讓更正排序和篩選依據的上下限之間。  
* 您不一定需要 tooduplicate 所有 hello 屬性的實體。 例如，如果 hello 查閱 hello 實體使用 hello 電子郵件的查詢以處理 hello **RowKey**永遠都不需要 hello 員工的年齡，這些實體可能會有下列結構的 hello:
  
  ![][11]
* 這是通常較佳的 toostore 重複的資料，並確認您可以擷取非實體使用 toouse 一個查詢 toolocate hello 次要索引，您必須使用單一查詢的所有 hello 資料，而且另一個 toolookup hello hello 主索引中的必要的資料。  

#### <a name="when-toouse-this-pattern"></a>當 toouse 此模式
當用戶端應用程式需要使用各種不同的金鑰，當您的用戶端需要不同排序順序中的 tooretrieve 實體 tooretrieve 實體以及您可以識別每個使用不同的唯一值的實體，請使用此模式。 使用此模式，當您想要執行 hello 不同實體查閱時超過 hello 資料分割的延展性限制 tooavoid **RowKey**值。  

#### <a name="related-patterns-and-guidance"></a>相關的模式和指導方針
hello 下列模式和指導方針也可能是相關實作此模式時：  

* [最終一致的交易模式](#eventually-consistent-transactions-pattern)  
* [內部資料分割次要索引模式](#intra-partition-secondary-index-pattern)  
* [複合索引鍵模式](#compound-key-pattern)  
* [實體群組交易](#entity-group-transactions)  
* [使用異質性實體類型](#working-with-heterogeneous-entity-types)  

### <a name="eventually-consistent-transactions-pattern"></a>最終一致的交易模式
使用 Azure 佇列，跨資料分割界限或儲存體系統界限啟用最終一致的行為。  

#### <a name="context-and-problem"></a>內容和問題
EGTs 跨多個實體以共用 hello 啟用不可部分完成的交易相同的資料分割索引鍵。 效能和延展性的原因，您可能會決定 toostore 實體具有一致性需求，在不同的磁碟分割或不同的儲存體系統中： 在此案例中，您無法使用 EGTs toomaintain 一致性。 例如，您可能必須之間的需求 toomaintain 最終一致性：  

* 儲存在相同的資料表，在不同的資料表中不同的儲存體帳戶中的 hello 中兩個不同的資料分割的實體。  
* Blob 儲存在 Blob 服務的 hello 而且儲存在 hello 表格服務中的實體。  
* 實體檔案系統中儲存在 hello 表格服務和檔案。  
* 實體在 hello 表格服務中儲存，但使用 hello Azure 搜尋服務編製索引。  

#### <a name="solution"></a>方案
藉由使用 Azure 佇列，您可以實作解決方案，提供跨兩個或多個資料分割或儲存系統的最終一致性。
這個方法 tooillustrate，假設您有需求 toobe 無法 tooarchive 舊員工實體。 舊的員工實體很少受到查詢，應從處理目前員工的任何活動中排除。 tooimplement 在職員工存放 hello 這項需求**目前**資料表和舊的員工的 hello**封存**資料表。 封存員工會要求您從 hello toodelete hello 實體**目前**資料表，並新增 hello 實體 toohello**封存**資料表，但是您無法使用 EGT tooperform 這兩項操作。 tooavoid 失敗會導致實體 tooappear，這兩個或兩資料表中的 hello 風險，hello 保存作業必須是最終保持一致。 hello 順序圖概述此作業中的 hello 步驟。 例外狀況的路徑中的 hello 文字後面提供更多詳細資料。  

![][12]

用戶端會將訊息放在 Azure 佇列，在此範例 tooarchive 員工 #456 起始 hello 封存作業。 背景工作角色輪詢 hello 佇列的新訊息。發現，它會讀取 hello 訊息，並會隱藏的複本保留 hello 佇列上。 hello 背景工作角色旁的 hello 實體複本會從提取 hello**目前**資料表中，將複本插入 hello**封存**資料表，然後按一下 刪除 hello hello 從原始**目前**資料表。 最後，如果沒有任何錯誤 hello 先前步驟中的，hello 背景工作角色會從 hello 佇列刪除 hello 隱藏的訊息。  

在此範例中，步驟 4 中插入 hello 員工 hello**封存**資料表。 它可以在檔案系統中新增 hello Blob 服務中的 hello 員工 tooa blob 或檔案。  

#### <a name="recovering-from-failures"></a>從失敗復原
很重要的 hello 中步驟的作業**4**和**5**必須*等冪*當 hello 背景工作角色需要 toorestart hello 封存作業。 如果您使用 hello 表格服務，如步驟**4**您應該使用 「 插入或取代 」 作業; 步驟**5**應該使用 「 如果刪除存在"hello 您使用的用戶端程式庫中的作業。 如果您使用其他儲存體系統，您必須使用適當的冪等作業。  

如果 hello 背景工作角色一直沒有完成步驟**6**，然後將逾時 hello 訊息會重新出現在 hello 佇列之後隨時可供 hello 背景工作角色 tootry tooreprocess 它。 hello 背景工作角色可以檢查 hello 佇列的訊息已讀取的次數，而且，如果有必要，請傳送 tooa 是 「 滯礙 」 訊息以便調查的旗標來區隔佇列。 如需有關讀取訊息排入佇列，並檢查 hello 清除佇列計數，請參閱[Get Messages](https://msdn.microsoft.com/library/azure/dd179474.aspx)。  

從資料表和佇列服務的 hello 有些錯誤是暫時性的錯誤，和用戶端應用程式應包含適當的重試邏輯 toohandle 它們。  

#### <a name="issues-and-considerations"></a>問題和考量
請考慮 hello 時決定下列點如何 tooimplement 這種模式：  

* 此方案不提供交易隔離。 比方說，用戶端無法讀取 hello**目前**和**封存**資料表 hello 背景工作角色的時間步驟之間**4**和**5**，並請參閱hello 資料不一致檢視。 請注意，hello 資料能維持一致最後。  
* 您必須確定步驟 4 和 5 會在順序 tooensure 最終一致性等冪。  
* 您可以藉由使用多個佇列和背景工作角色執行個體調整 hello 方案。  

#### <a name="when-toouse-this-pattern"></a>當 toouse 此模式
當您想 tooguarantee 存在於不同的磁碟分割或資料表中的實體之間的最終一致性時，請使用此模式。 您可以延伸 hello 表格服務以及 hello Blob 服務和其他非 Azure 儲存體資料來源，例如資料庫或 hello 檔案系統作業此模式 tooensure 最終一致性。  

#### <a name="related-patterns-and-guidance"></a>相關的模式和指導方針
hello 下列模式和指導方針也可能是相關實作此模式時：  

* [實體群組交易](#entity-group-transactions)  
* [合併或取代](#merge-or-replace)  

> [!NOTE]
> 如果交易隔離是重要的 tooyour 解決方案，您應該考慮重新設計資料表 tooenable 您 toouse EGTs。  
> 
> 

### <a name="index-entities-pattern"></a>索引實體模式
維護索引實體 tooenable 有效率的搜尋傳回的實體清單。  

#### <a name="context-and-problem"></a>內容和問題
hello 表格服務會自動索引使用 hello 實體**PartitionKey**和**RowKey**值。 這可讓用戶端應用程式 tooretrieve 有效率地使用點查詢的實體。 例如，使用 hello 資料表結構，如下所示，用戶端應用程式可以有效率地擷取個別員工實體使用 hello 部門名稱和 hello 員工識別碼 (hello **PartitionKey**和**RowKey**).  

![][13]

如果您也想 toobe 無法 tooretrieve 員工實體的清單會根據 hello 另一個非唯一屬性值，例如其最後一個名稱，您必須使用效率較低的資料分割掃描 toofind 相符項目，而不是使用索引 toolook 它們直接啟動。 這是因為 hello 表格服務不會提供次要索引。  

#### <a name="solution"></a>方案
依姓氏與 hello 實體結構，如上所示，您必須維護的員工識別碼清單的 tooenable 查閱。 如果您想 tooretrieve hello 員工實體具有特定的最後一個名稱，例如 Jones，您必須先找出 Jones 做為其最後一個名稱，與員工的員工識別碼 hello 清單，然後再擷取這些員工實體。 有三個主要的選項，可儲存的員工識別碼 hello 清單：  

* 使用 Blob 儲存體。  
* 索引中建立實體 hello 相同資料分割以 hello 員工實體。  
* 在個別的資料分割或資料表中建立索引實體。  

<u>選項 1：使用 Blob 儲存體</u>  

Hello 第一個選項，您建立的每個唯一的姓氏，以及每個 blob 存放區中的 blob 清單的 hello **PartitionKey** （部門） 和**RowKey** （員工識別碼），最後，在員工的值名稱。 當您新增或刪除員工就應該確保 hello 相關 blob hello 內容是最終與 hello 員工實體保持一致。  

<u>選項 2:</u>中的建立索引實體 hello 相同的資料分割  

Hello 第二個選項，使用索引的實體儲存 hello 下列資料：  

![][14]

hello **EmployeeIDs**屬性包含員工的員工識別碼的清單，hello 最後一個名稱儲存在 hello **RowKey**。  

hello 下列步驟概述您要加入新的員工，如果您使用 hello 第二個選項時所應遵循的 hello 程序。 在此範例中，我們新增識別碼 000152 且最後一個名稱 Jones hello 銷售部門的員工：  

1. 擷取與 hello 索引實體**PartitionKey**實值 「 銷售 」 與 hello **RowKey**值"Jones。 」 儲存在步驟 2 中的 hello 這個實體 toouse 的 ETag。  
2. 建立實體群組交易 （也就是說，批次作業），將新員工實體 hello (**PartitionKey**值 「 銷售 」 和**RowKey**值"000152")，並更新 hello 索引實體 (**PartitionKey**值 「 銷售 」 和**RowKey**值"Jones") 在 hello EmployeeIDs 欄位中加入 hello 新員工識別碼 toohello 清單。 如需實體群組交易的詳細資訊，請參閱 [實體群組交易](#entity-group-transactions)。  
3. 如果 hello 實體群組交易失敗，因為開放式並行存取錯誤 （其他人就已修改 hello 索引實體），則您需要 toostart 透過在步驟 1 一次。  

如果您使用 hello 第二個選項，您可以使用類似的方法 toodeleting 員工。 變更員工的姓氏會稍微複雜，因為您將需要更新三個實體的實體群組交易 tooexecute: hello 員工實體、 hello 索引實體 hello 舊的最後一個名稱，與 hello 索引實體 hello 新的最後一個名稱。 您必須再進行任何變更順序，然後您可以使用 tooperform hello 更新使用開放式並行存取 tooretrieve hello ETag 值擷取每個實體。  

hello 下列步驟將概略說明當您需要 toolook 上所有的 hello 員工，具有給定部門中最後一個名稱，如果您使用 hello 第二個選項時，您應該遵循的 hello 程序。 在此範例中，我們會查閱姓氏 Jones hello 銷售部門的所有 hello 員工：  

1. 擷取與 hello 索引實體**PartitionKey**實值 「 銷售 」 與 hello **RowKey**值"Jones。 」  
2. 剖析員工識別碼 hello EmployeeIDs 欄位中的 hello 的清單。  
3. 如果您需要每個這些員工 （例如電子郵件地址） 的其他資訊，擷取每個使用 hello 員工實體**PartitionKey**值 「 銷售 」 和**RowKey**中的值您在步驟 2 中取得的員工 hello 清單。  

<u>選項 3：</u>在個別的資料分割或資料表中建立索引實體  

Hello 第三個選項，使用索引的實體儲存 hello 下列資料：  

![][15]

hello **EmployeeIDs**屬性包含員工的員工識別碼的清單，hello 最後一個名稱儲存在 hello **RowKey**。  

Hello 第三個選項時，您無法使用 EGTs toomaintain 一致性，因為 hello 索引實體是位於不同的磁碟分割，從 hello 員工實體。 您應該確保 hello 索引實體最終與 hello 員工實體保持一致。  

#### <a name="issues-and-considerations"></a>問題和考量
請考慮 hello 時決定下列點如何 tooimplement 這種模式：  

* 此解決方案需要比對實體的至少兩個查詢 tooretrieve： 有一個 tooquery hello 索引實體 tooobtain hello 清單**RowKey**值，然後再來是查詢 tooretrieve hello 清單中的每個實體。  
* 鑑於個別的實體大小上限為 1 MB，選項 #2 和 hello 方案中的選項 #3 假設 hello 清單的任何特定姓氏的員工識別碼絕不會是大於 1 MB。 如果員工識別碼 hello 清單可能 toobe 大於 1 MB 的大小，使用選項 #1，並儲存在 blob 儲存體中的 hello 索引資料。  
* 如果您使用選項 #2 （使用 EGTs toohandle 加入和刪除員工，以及變更員工的姓氏） 您必須評估 hello 磁碟區的交易將會很接近給定資料分割中的 hello 延展性限制。 在 hello 情況下，您應該考慮使用佇列 toohandle hello update 最終一致方案 （#1 選項或選項 #3） 要求，並可讓您 toostore 索引實體在不同的磁碟分割，從 hello 員工實體。  
* 此解決方案中的選項 #2 會假設您想 toolook 向上依部門中的最後一個名稱： 例如，您想 tooretrieve 姓氏 Jones hello 銷售部門的員工清單。 如果您想 toobe 無法 toolook 向上所有 hello 員工姓氏 Jones hello 整個組織內，使用 #1 選項或選項 #3。
* 您可以實作以佇列為基礎的解決方案，提供最終一致性 (請參閱 hello[最終保持一致的交易模式](#eventually-consistent-transactions-pattern)如需詳細資訊)。  

#### <a name="when-toouse-this-pattern"></a>當 toouse 此模式
當您想 toolookup 的所有共用通用的屬性值，例如 hello 姓氏 Jones 具有所有員工的實體集時，請使用此模式。  

#### <a name="related-patterns-and-guidance"></a>相關的模式和指導方針
hello 下列模式和指導方針也可能是相關實作此模式時：  

* [複合索引鍵模式](#compound-key-pattern)  
* [最終一致的交易模式](#eventually-consistent-transactions-pattern)  
* [實體群組交易](#entity-group-transactions)  
* [使用異質性實體類型](#working-with-heterogeneous-entity-types)  

### <a name="denormalization-pattern"></a>反正規化模式
合併相關的資料集中單一實體 tooenable 您 tooretrieve 所有 hello 您需要使用單點查詢的資料。  

#### <a name="context-and-problem"></a>內容和問題
在關聯式資料庫中，您通常會正規化資料 tooremove 重複導致多個資料表中擷取資料的查詢。 如果您在 Azure 資料表中的將資料標準化您，您必須先從 hello 用戶端 toohello 伺服器 tooretrieve 多次往返相關的資料。 例如下, 面顯示 hello 資料表結構需要兩個四捨五入部門的往返 tooretrieve hello 詳細資料： 一個 toofetch hello department 實體中員工包含 hello 經理識別碼和另一個要求 toofetch hello 管理員的詳細資料實體。  

![][16]

#### <a name="solution"></a>方案
而是 hello 資料存放在兩個不同的實體，反正規化 hello 資料並在 hello department 實體中保留一份 hello 管理員詳細資料。 例如：  

![][17]

與部門實體儲存含有這些屬性，您現在可以擷取您需要使用點查詢的部門相關的所有 hello 詳細資料。  

#### <a name="issues-and-considerations"></a>問題和考量
請考慮 hello 時決定下列點如何 tooimplement 這種模式：  

* 儲存資料兩次還有一些相關的成本負擔。 hello 獲益 （造成較少的要求 toohello 儲存體服務） 通常超過 hello 臨界增加儲存成本 (此成本部分的位移和交易的 hello 數目減少您需要 toofetch hello 詳細資料部門）。  
* 您必須維護 hello hello 儲存經理的相關資訊的兩個實體一致性。 您可以處理 hello 一致性問題使用 EGTs tooupdate 單一不可部分完成交易中的多個實體： 在此情況下，hello department 實體和 hello hello 部門經理的員工實體會儲存在 hello 相同的資料分割。  

#### <a name="when-toouse-this-pattern"></a>當 toouse 此模式
當您經常需要 toolook 相關資訊，請使用此模式。 此模式會減少您的用戶端必須讓它需要的 tooretrieve hello 資料查詢的 hello 數目。  

#### <a name="related-patterns-and-guidance"></a>相關的模式和指導方針
hello 下列模式和指導方針也可能是相關實作此模式時：  

* [複合索引鍵模式](#compound-key-pattern)  
* [實體群組交易](#entity-group-transactions)  
* [使用異質性實體類型](#working-with-heterogeneous-entity-types)

### <a name="compound-key-pattern"></a>複合索引鍵模式
使用複合**RowKey**值 tooenable 用戶端 toolookup 相關資料的單一點查詢。  

#### <a name="context-and-problem"></a>內容和問題
在關聯式資料庫中，它是在查詢中的自然 toouse 聯結 tooreturn 相關資料 toohello 用戶端，單一查詢中的部分。 例如，您可能會使用 hello 員工識別碼 toolook 相關實體，其包含的效能，並且該員工來檢閱資料的清單。  

假設您使用下列結構的 hello hello 資料表服務中儲存員工實體：  

![][18]

您也需要相關 tooreviews toostore 歷程記錄資料和每年 hello 位員工的效能，曾為您的組織，而且您需要 toobe 無法 tooaccess 依年度的這項資訊。 其中一個選項是 toocreate 儲存實體具有下列結構的 hello 的另一個資料表：  

![][19]

請注意，這會很接近您可能會決定 tooduplicate hello 新實體 tooenable 部分資訊 （例如名字和姓氏） 您 tooretrieve 單一要求您的資料。 不過，您無法維護強式一致性，因為您不能以不可分割方式使用 EGT tooupdate hello 兩個實體。  

#### <a name="solution"></a>方案
將新的實體類型儲存在原始資料表使用實體具有下列結構的 hello:  

![][20]

請注意如何 hello **RowKey**現在的組合索引鍵所組成的 hello 員工識別碼和 hello 年度 hello 檢閱資料，可讓您 tooretrieve hello 員工的效能，並檢閱與單一實體的單一要求的資料。  

下列範例中的 hello 概要說明如何擷取所有 hello 檢閱資料 （例如 employee 000123 hello 銷售部門) 的特定員工的：  

$filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000123') and (RowKey lt 'empid_000124')&$select=RowKey,Manager Rating,Peer Rating,Comments  

#### <a name="issues-and-considerations"></a>問題和考量
請考慮 hello 時決定下列點如何 tooimplement 這種模式：  

* 您應該使用適當的分隔字元，可讓您輕鬆 tooparse hello **RowKey**值： 例如， **000123_2012**。  
* 您也在相同資料分割包含 hello 的相關的資料的其他實體的 hello 儲存此實體相同的員工，這表示您可以使用 EGTs toomaintain 強式一致性。
* 您應該考慮頻率您將查詢 hello 資料 toodetermine 此模式是否適當。  例如，如果您將存取不常 hello 檢閱資料和 hello 主要員工資料通常您應該讓它們保持為不同的實體。  

#### <a name="when-toouse-this-pattern"></a>當 toouse 此模式
當您需要 toostore 其中一個或多個相關實體您查詢經常會使用這個模式。  

#### <a name="related-patterns-and-guidance"></a>相關的模式和指導方針
hello 下列模式和指導方針也可能是相關實作此模式時：  

* [實體群組交易](#entity-group-transactions)  
* [使用異質性實體類型](#working-with-heterogeneous-entity-types)  
* [最終一致的交易模式](#eventually-consistent-transactions-pattern)  

### <a name="log-tail-pattern"></a>記錄結尾模式
擷取 hello  *n* 實體最近加入 tooa 資料分割使用**RowKey**以反向的日期和時間順序排序的值。  

#### <a name="context-and-problem"></a>內容和問題
常見的需求是能夠 tooretrieve hello 最近建立的實體，例如 hello 十個最新費用報銷送出的員工。 資料表查詢支援**$top**第一次查詢作業 tooreturn hello  *n* 從一組實體： 集合中沒有任何對等查詢作業 tooreturn hello 最後 n 個實體。  

#### <a name="solution"></a>方案
使用的存放區 hello 實體**RowKey** ，自然反向排序日期/時間順序使用，因此 hello 最新的項目永遠都是 hello hello 資料表中的第一個。  

例如，toobe 無法 tooretrieve hello 員工所提交的十個最新費用報銷，您可以使用衍生自 hello 目前日期/時間反向刻度值。 hello 下列 C# 程式碼範例會示範其中一種方式 toocreate 適當"反轉刻度"的值為**RowKey**從 hello 最近 toohello 最舊的排序：  

`string invertedTicks = string.Format("{0:D19}", DateTime.MaxValue.Ticks - DateTime.UtcNow.Ticks);`  

您可以取得使用下列程式碼的 hello toohello 日期時間值：  

`DateTime dt = new DateTime(DateTime.MaxValue.Ticks - Int64.Parse(invertedTicks));`  

hello 資料表查詢看起來像這樣：  

`https://myaccount.table.core.windows.net/EmployeeExpense(PartitionKey='empid')?$top=10`  

#### <a name="issues-and-considerations"></a>問題和考量
請考慮 hello 時決定下列點如何 tooimplement 這種模式：  

* 您必須對 hello 反向刻度值加上前置零進行填補 tooensure hello 字串值排序如預期般。  
* 您必須留意的 hello 在 hello 層級資料分割的延展性目標。 請留意不要建立熱點資料分割。  

#### <a name="when-toouse-this-pattern"></a>當 toouse 此模式
使用此模式需要反向的日期/時間順序 tooaccess 實體時，或當您需要 tooaccess hello 是最近加入的實體。  

#### <a name="related-patterns-and-guidance"></a>相關的模式和指導方針
hello 下列模式和指導方針也可能是相關實作此模式時：  

* [在前面加上/附加反向模式](#prepend-append-anti-pattern)  
* [擷取實體](#retrieving-entities)  

### <a name="high-volume-delete-pattern"></a>大量刪除模式
藉由將同時刪除所有 hello 實體都儲存在他們自己的個別資料表; 中啟用 hello 刪除大量實體您刪除 hello 實體 hello 資料表中刪除。  

#### <a name="context-and-problem"></a>內容和問題
許多應用程式刪除舊的資料不再需要 toobe 可用 tooa 用戶端應用程式，或該 hello 應用程式已封存 tooanother 儲存媒體。 您通常可以依日期識別這類資料： 例如，您有需求 toodelete 記錄是 60 天以前的所有登入要求。  

一個可能的設計是 toouse hello 日期和時間在 hello hello 登入要求**RowKey**:  

![][21]

這個方法可避免分割區的作用，因為 hello 應用程式可以插入和刪除不同的磁碟分割中每個使用者的登入實體。 不過，這種方法可能會很耗費資源和耗時如果您有大量的實體，因為先 tooperform 資料表掃描順序 tooidentify 中所有的 hello 實體 toodelete，而且則必須刪除舊的每個實體。 請注意，您可以藉由批次處理多個刪除要求到 EGTs 減少 hello 往返 toohello 需要 server toodelete hello 舊的實體數目。  

#### <a name="solution"></a>方案
為每天的登入嘗試使用個別的資料表。 當您要插入的實體，並刪除舊的實體是現在只要刪除一個資料表的每一天的問題，您可以使用上述 tooavoid 熱點 hello 實體設計 （單一儲存體作業） 而不是尋找及刪除上百和無數每日的個別登入實體。  

#### <a name="issues-and-considerations"></a>問題和考量
請考慮 hello 時決定下列點如何 tooimplement 這種模式：  

* 您的設計是否支援其他應用程式將使用 hello 資料，例如查閱特定實體、 連結和其他資料或產生的彙總資訊的方式？  
* 您的設計在插入新實體時是否可避免產生熱點？  
* 預期的延遲，如果您想 tooreuse hello 相同後刪除的資料表名稱。 它是較佳的 tooalways 使用唯一資料表名稱。  
* 預期某些節流，當您第一次使用新的資料表，而 hello 表格服務會學習 hello 存取模式和節點之間分配 hello 資料分割。 您應該考慮您需要 toocreate 新資料表的頻率。  

#### <a name="when-toouse-this-pattern"></a>當 toouse 此模式
使用此模式，當您有大量的實體，您必須刪除 hello 在相同的時間。  

#### <a name="related-patterns-and-guidance"></a>相關的模式和指導方針
hello 下列模式和指導方針也可能是相關實作此模式時：  

* [實體群組交易](#entity-group-transactions)
* [修改實體](#modifying-entities)  

### <a name="data-series-pattern"></a>資料序列模式
存放區中單一實體 toominimize hello 的許多要求您進行完整的資料數列。  

#### <a name="context-and-problem"></a>內容和問題
常見的案例是針對應用程式 toostore 一系列的資料，它通常需要 tooretrieve 一次。 例如，您的應用程式可能會記錄每個員工傳送每小時的 IM 訊息數目，然後使用 每位使用者透過傳送的訊息數目 hello 上述 24 小時內的這個資訊 tooplot。 一個設計可能會為每位員工的 toostore 24 實體：  

![][22]

與這個設計中，可以輕鬆地找到並更新每一位員工的 hello 實體 tooupdate 只要 hello 應用程式需要 tooupdate hello 訊息計數值。 不過，tooretrieve hello 資訊 tooplot hello 前 24 小時的 hello 活動的圖表，您必須擷取 24 的實體。  

#### <a name="solution"></a>方案
使用下列的設計，含有個別屬性 toostore hello 訊息計數每小時的 hello:  

![][23]

與這個設計中，您可以使用合併作業 tooupdate hello 訊息計數員工的特定小時。 現在，您可以擷取您需要使用要求的單一實體 tooplot hello 圖表的所有 hello 資訊。  

#### <a name="issues-and-considerations"></a>問題和考量
請考慮 hello 時決定下列點如何 tooimplement 這種模式：  

* 完整的資料數列不符合單一實體 （實體最多可以有 too252 屬性），如果使用替代的資料存放區，例如 blob。  
* 如果您有多個用戶端同時更新實體，您將需要 toouse hello **ETag** tooimplement 開放式並行存取。 如果您有許多用戶端，則預期應會有激烈的爭用情況。  

#### <a name="when-toouse-this-pattern"></a>當 toouse 此模式
當您需要 tooupdate 並擷取個別實體與相關聯的資料數列時，請使用此模式。  

#### <a name="related-patterns-and-guidance"></a>相關的模式和指導方針
hello 下列模式和指導方針也可能是相關實作此模式時：  

* [大型實體模式](#large-entities-pattern)  
* [合併或取代](#merge-or-replace)  
* [最終一致性的交易模式](#eventually-consistent-transactions-pattern)（如果您 hello 資料數列在儲存 blob）  

### <a name="wide-entities-pattern"></a>寬型實體模式
使用多個實體的實體 toostore 邏輯實體具有多個 252 的屬性。  

#### <a name="context-and-problem"></a>內容和問題
個別實體可以擁有 252 個以上的屬性 （不含 hello 強制系統屬性），而且無法將超過 1 MB 的資料儲存在總計。 在關聯式資料庫中，您通常得到 round hello 大小之資料列的任何限制，加入新的資料表，以及強制執行它們之間的 1 對 1 關聯性。  

#### <a name="solution"></a>方案
使用 hello 表格服務，您可以儲存多個實體 toorepresent 252 多個屬性的單一大型的商務物件。 比方說，如果您想 toostore hello IM 傳送之訊息的每個員工的 hello 過去 365 天內的數字計數，您可以使用下列兩個實體使用不同的結構描述的設計 hello:  

![][24]

如果您需要 toomake 需要更新它們彼此同步處理兩個實體 tookeep 的變更，您可以使用 EGT。 否則，您可以使用單一合併作業 tooupdate hello 訊息計數的特定日期。 所有您必須擷取這兩個實體，您可以使用兩個同時使用的有效要求執行個別員工的 hello 資料 tooretrieve **PartitionKey**和**RowKey**值。  

#### <a name="issues-and-considerations"></a>問題和考量
請考慮 hello 時決定下列點如何 tooimplement 這種模式：  

* 擷取完成的邏輯實體牽涉到兩個以上的儲存體交易： 一個 tooretrieve 實際實體。  

#### <a name="when-toouse-this-pattern"></a>當 toouse 此模式
當需要 toostore 實體其大小或屬性的數目超過 hello 限制個別實體中 hello 表格服務，請使用此模式。  

#### <a name="related-patterns-and-guidance"></a>相關的模式和指導方針
hello 下列模式和指導方針也可能是相關實作此模式時：  

* [實體群組交易](#entity-group-transactions)
* [合併或取代](#merge-or-replace)

### <a name="large-entities-pattern"></a>大型實體模式
使用 blob 儲存體 toostore 大型屬性值。  

#### <a name="context-and-problem"></a>內容和問題
個別實體無法儲存總計超過 1 MB 的資料。 如果一或多個屬性的儲存值，這個值會導致實體 tooexceed hello 總大小，您無法儲存整個實體的 hello hello 表格服務中。  

#### <a name="solution"></a>方案
如果實體的大小超過 1 MB，因為一個或多個屬性包含大量的資料，您可以在 hello Blob 服務中儲存資料，然後將 hello hello blob 位址儲存在 hello 實體中的屬性。 比方說，您可以在 hello 之員工的相片儲存在 blob 儲存體，並將連結 toohello 相片儲存在 hello**相片**員工實體的屬性：  

![][25]

#### <a name="issues-and-considerations"></a>問題和考量
請考慮 hello 時決定下列點如何 tooimplement 這種模式：  

* toomaintain 最終一致性 hello 表格服務中的 hello 實體與 hello Blob 服務中的 hello 資料之間使用 hello[最終保持一致的交易模式](#eventually-consistent-transactions-pattern)toomaintain 您的實體。
* 擷取完整實體牽涉到兩個以上的儲存體交易： 一個 tooretrieve hello 實體和一個 tooretrieve hello blob 資料。  

#### <a name="when-toouse-this-pattern"></a>當 toouse 此模式
當您需要其大小超過個別實體 hello 表格服務中的 hello 限制 toostore 實體時，請使用此模式。  

#### <a name="related-patterns-and-guidance"></a>相關的模式和指導方針
hello 下列模式和指導方針也可能是相關實作此模式時：  

* [最終一致的交易模式](#eventually-consistent-transactions-pattern)  
* [寬型實體模式](#wide-entities-pattern)

<a name="prepend-append-anti-pattern"></a>

### <a name="prependappend-anti-pattern"></a>在前面加上/附加反向模式
您的跨多個資料分割分配 hello 插入大量插入時，增加延展性。  

#### <a name="context-and-problem"></a>內容和問題
前面加上或附加的實體儲存 tooyour 實體通常會導致第一次加入新的實體 toohello hello 應用程式或最後一個資料分割的資料分割的順序。 在此情況下，所有在任何指定時間的 hello 插入 hello 跨多個節點，插入相同的資料分割，建立負載平衡時，防止 hello 表格服務的作用中未進行，而且可能會造成您的應用程式 toohit hello 延展性資料分割的目標。 例如，如果您的應用程式記錄檔的網路與資源存取的員工，然後如下所示的實體結構可能會導致 hello 目前的小時資料分割成為作用點，如果交易 hello 量分別達到 hello 的延展性目標個別的資料分割：  

![][26]

#### <a name="solution"></a>方案
hello 下列替代實體結構可避免任何特定資料分割的作用區為 hello 應用程式記錄檔事件：  

![][27]

請注意此範例如何同時 hello **PartitionKey**和**RowKey**是複合的索引鍵。 hello **PartitionKey**橫跨多個資料分割使用 hello 部門和員工識別碼 toodistribute hello 記錄。  

#### <a name="issues-and-considerations"></a>問題和考量
請考慮 hello 時決定下列點如何 tooimplement 這種模式：  

* 沒有 hello 替代索引鍵結構可避免熱資料分割上建立插入有效率地支援 hello 查詢可讓用戶端應用程式嗎？  
* 您預期的磁碟區的交易表示，您可能 tooreach hello 個別的資料分割的延展性目標而進行節流處理 hello 儲存體服務？  

#### <a name="when-toouse-this-pattern"></a>當 toouse 此模式
您的磁碟區的交易時可能 tooresult 中節流 hello 儲存體服務，當您存取熱資料分割時，請避免 hello 前面加上/附加反面模式。  

#### <a name="related-patterns-and-guidance"></a>相關的模式和指導方針
hello 下列模式和指導方針也可能是相關實作此模式時：  

* [複合索引鍵模式](#compound-key-pattern)  
* [記錄檔結尾模式](#log-tail-pattern)  
* [修改實體](#modifying-entities)  

### <a name="log-data-anti-pattern"></a>記錄資料反向模式
一般而言，您應該使用 hello Blob 服務，而不是 hello 資料表服務 toostore 記錄檔資料。  

#### <a name="context-and-problem"></a>內容和問題
一般使用案例記錄的資料是 tooretrieve 的特定日期/時間範圍的記錄項目選取： 例如，您想的 toofind 所有 hello 錯誤和嚴重訊息 15:04 15:06 在特定日期之間的應用程式記錄。 您不想 toouse hello 日期和時間 hello 記錄訊息 toodetermine hello 磁碟分割的儲存記錄檔項目，:，熱資料分割中的結果因為在任何時候，會共用所有 hello 記錄實體 hello 相同**PartitionKey**值 (請參閱 hello 節[前面加上/附加反面模式](#prepend-append-anti-pattern))。 例如，下列實體記錄檔訊息的結構描述的 hello 會導致熱資料分割因為 hello 應用程式會寫入所有的記錄訊息 toohello hello 目前的日期和小時的資料分割：  

![][28]

在此範例中，hello **RowKey**包括 hello 記錄訊息 tooensure 記錄訊息會儲存日期/時間順序排列的 hello 日期和時間，並包含訊息識別碼，如果多個記錄檔訊息共用相同的日期和時間的 hello。  

另一個方法是 toouse **PartitionKey**這可確保 hello 應用程式將訊息寫入一個範圍內的資料分割。 比方說，如果 hello 記錄檔訊息的 hello 來源提供跨多個資料分割方式 toodistribute 訊息，您可以使用下列項目結構描述的 hello:  

![][29]

不過，與此結構描述的 hello 問題是所有 hello 必須搜尋的記錄檔訊息的特定時間範圍為該 tooretrieve hello 資料表中的每個資料分割。

#### <a name="solution"></a>方案
hello 前一個區段反白顯示的 hello 問題嘗試 toouse 的 hello 資料表服務 toostore 記錄項目和建議的兩個，令人滿意，設計。 其中一種解決方案導致 tooa 熱資料分割的記錄檔訊息; 寫入的效能不佳的 hello 風險hello 其他解決方案導致查詢效能不佳因為 hello 需求 tooscan hello 資料表 tooretrieve 記錄檔訊息的特定時間範圍中每個資料分割。 Blob 儲存體提供更好的解決方案，這種案例，這是 Azure 儲存體分析存放區 hello 記錄資料收集。  

本節將概述如何儲存體分析記錄檔將資料儲存在 blob 儲存體當做此方法 toostoring 資料，您通常查詢範圍的說明。  

Storage Analytics 會以分隔格式將記錄訊息儲存在多個 Blob 中。 hello 分隔的格式可輕鬆用戶端應用程式 tooparse hello 資料 hello 記錄檔訊息中。  

儲存體分析會使用命名慣例，可讓您 toolocate hello blob （或 blob） 包含您要搜尋的 hello 記錄檔訊息的 blob。 例如，名為"queue/2014/07/31/1800/000001.log"blob 包含相關 toohello hello 小時 18:00 31 自 2014 年 7 月開始的佇列服務的記錄檔訊息。 hello"000001"表示這是第一個記錄檔 hello 這段期間的。 儲存體分析也會記錄第一次的 hello hello 時間戳記和訊息在 hello blob 的中繼資料儲存在 hello 檔案中的最後一個記錄。 針對 blob 儲存體可讓您尋找 blob 的名稱前置詞為基礎的容器中的 hello API: toolocate 包含佇列的所有 hello blob 都記錄資料 hello 小時 18:00 開始，您可以使用 hello 前置詞"佇列/2014年/07/31/1800。 」  

儲存體分析內部緩衝區記錄訊息和定期更新 hello 適當 blob 或建立一個新 hello 最新批次的記錄項目。 這可減少 hello 數目的寫入它必須執行 toohello blob 服務。  

如果您在自己的應用程式中實作類似方案，您必須考慮如何 toomanage hello （情形，請撰寫每個記錄項目 tooblob 儲存體） 的可靠性及成本和延展性之間的取捨 (在您的應用程式中緩衝處理更新，撰寫這些 tooblob 儲存批次）。  

#### <a name="issues-and-considerations"></a>問題和考量
請考慮下列點決定 toostore 資料的記錄時的 hello:  

* 如果您建立的資料表設計可避免產生潛在的熱點資料分割，您可能會發現您無法有效率地存取記錄資料。  
* tooprocess 記錄資料，用戶端通常需要 tooload 多筆記錄。  
* 雖然記錄資料通常是結構化的，Blob 儲存體會是較佳的方案。  

### <a name="implementation-considerations"></a>實作考量
當您實作 hello 先前章節所述的 hello 模式時，本節會討論一些 hello 考量 toobear 記住。 本章節的大部分會使用以 C# 撰寫的範例使用 hello 儲存體用戶端程式庫 （4.3.0 版 hello 撰寫本文時）。  

### <a name="retrieving-entities"></a>擷取實體
Hello > 一節中所述[設計查詢](#design-for-querying)，hello 最有效率的查詢是點查詢。 不過，在某些情況下您可能需要 tooretrieve 多個實體。 本章節描述使用儲存體用戶端程式庫 hello 一些常見方法 tooretrieving 實體。  

#### <a name="executing-a-point-query-using-hello-storage-client-library"></a>執行點查詢使用 hello 儲存體用戶端程式庫
最簡單方式 tooexecute hello 點查詢為 toouse hello**擷取**資料表作業，如下列 C# 程式碼片段的 hello 擷取與實體中所示**PartitionKey**值 「 銷售 」 和**RowKey**的值"212":  

```csharp
TableOperation retrieveOperation = TableOperation.Retrieve<EmployeeEntity>("Sales", "212");
var retrieveResult = employeeTable.Execute(retrieveOperation);
if (retrieveResult.Result != null)
{
    EmployeeEntity employee = (EmployeeEntity)retrieveResult.Result;
    ...
}  
```

請注意此範例預期 hello 實體的方式，它會擷取的型別 toobe **EmployeeEntity**。  

#### <a name="retrieving-multiple-entities-using-linq"></a>使用 LINQ 擷取多個實體
您可以搭配使用 LINQ 與儲存體用戶端程式庫，並指定具有 **where** 子句的查詢，以擷取多個實體。 tooavoid 資料表掃描，您應該永遠包含 hello **PartitionKey**中 hello 值其中子句，並盡可能 hello **RowKey**值 tooavoid 資料表和資料分割掃描。 hello 表格服務支援一組有限的比較運算子 （大於、 大於或等於、 小於、 小於或等於、 等於、 且不等於） toouse hello 其中子句。 hello 下列 C# 程式碼片段會尋找所有 hello 員工開頭的"B"與 (假設該 hello **RowKey**存放區 hello 姓氏) hello 銷售部門 (假設 hello **PartitionKey**儲存 hello 部門名稱）：  

```csharp
TableQuery<EmployeeEntity> employeeQuery = employeeTable.CreateQuery<EmployeeEntity>();
var query = (from employee in employeeQuery
            where employee.PartitionKey == "Sales" &&
            employee.RowKey.CompareTo("B") >= 0 &&
            employee.RowKey.CompareTo("C") < 0
            select employee).AsTableQuery();
var employees = query.Execute();  
```

請注意如何 hello 查詢同時指定**RowKey**和**PartitionKey** tooensure 更佳的效能。  

hello 下列程式碼範例示範相當於使用 hello fluent API 的功能 (如需 fluent Api 一般情況下，請參閱[設計 fluent 應用程式開發的應用程式開發介面的最佳作法](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):  

```csharp
TableQuery<EmployeeEntity> employeeQuery = new TableQuery<EmployeeEntity>().Where(
    TableQuery.CombineFilters(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition(
    "PartitionKey", QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.GenerateFilterCondition(
    "RowKey", QueryComparisons.GreaterThanOrEqual, "B")
),
TableOperators.And,
TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "C")
    )
);
var employees = employeeTable.ExecuteQuery(employeeQuery);  
```

> [!NOTE]
> hello 範例會建立多個**CombineFilters**方法 tooinclude hello 三個篩選條件。  
> 
> 

#### <a name="retrieving-large-numbers-of-entities-from-a-query"></a>從查詢擷取大量實體
最佳查詢會根據 **PartitionKey** 值和 **RowKey** 值傳回個別實體。 不過，在某些情況下您可能必須需求 tooreturn hello 相同分割區，或甚至從多個資料分割從多個實體。  

您應該一律會完整測試 hello 應用程式的效能，在這類案例。  

針對 hello 表格服務的查詢可能會傳回 1,000 個實體最多一次，而且執行五秒的最大值。 如果 hello 結果集包含超過 1,000 個實體，但如果 hello 查詢未於五秒，內完成，或者如果 hello 查詢跨越 hello 資料分割界限，hello 表格服務會傳回接續 token 的 tooenable hello 用戶端應用程式 toorequest hello下一個實體的集合。 如需接續權杖如何運作的詳細資訊，請參閱 [查詢逾時和分頁](http://msdn.microsoft.com/library/azure/dd135718.aspx)。  

如果您使用 hello 儲存體用戶端程式庫，它可以自動處理接續 token，因為它從 hello 表格服務會傳回實體。 hello 下列 C# 程式碼範例使用 hello 儲存體用戶端程式庫會自動處理接續 token 如果 hello 表格服務在回應中傳回：  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

var employees = employeeTable.ExecuteQuery(employeeQuery);
foreach (var emp in employees)
{
        ...
}  
```

下列 C# 程式碼的 hello 明確地處理接續 token:  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

TableContinuationToken continuationToken = null;

do
{
        var employees = employeeTable.ExecuteQuerySegmented(
        employeeQuery, continuationToken);
    foreach (var emp in employees)
    {
    ...
    }
    continuationToken = employees.ContinuationToken;
} while (continuationToken != null);  
```

藉由明確使用接續 token，您可以控制您的應用程式時擷取 hello 下一個區段的資料。 例如，如果用戶端應用程式可讓使用者透過儲存在資料表中的 hello 實體的 toopage，使用者可以決定不 toopage 透過讓您的應用程式只會使用接續 token tooretrieve hello 接下來，由 hello 查詢所擷取的所有 hello 實體當 hello 使用者已完成透過 hello 目前區段中的所有 hello 實體分頁區段。 這種方法有幾項優點：  

* 它可讓您從 hello 表格服務資料 tooretrieve toolimit hello 數量和移 hello 網路。  
* 它可讓您 tooperform 非同步 IO.NET 中。  
* 它可讓您 tooserialize hello 接續權杖 toopersistent 儲存體，您可以繼續在 hello 事件中的應用程式當機。  

> [!NOTE]
> 接續權杖通常會傳回包含 1000 個實體的區段，但也可能較少。 這也是如果您限制 hello 使用的查詢傳回的項目數目 hello 案例**採取**tooreturn hello 第 n 個實體符合查閱準則： hello 表格服務可能會傳回包含少於一個沿著 n 個實體的區段使用接續 token 的 tooenable 您 tooretrieve hello 剩餘的實體。  
> 
> 

hello 下列 C# 程式碼會示範區段內傳回的實體 toomodify hello 數目的方式：  

```csharp
employeeQuery.TakeCount = 50;  
```

#### <a name="server-side-projection"></a>伺服器端預測
單一實體可以有 too255 內容，並是 up too1 MB 的大小。 查詢 hello 資料表擷取實體時，您可能不需要所有的 hello 屬性，並可避免不必要地傳送資料 （toohelp 降低延遲和成本）。 您可以使用您所需要的伺服器端投影 tootransfer 只 hello 屬性。 hello 下列範例是擷取只 hello**電子郵件**屬性 (連同**PartitionKey**， **RowKey**，**時間戳記**，和**ETag**) 從 hello hello 查詢所選取的實體。  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
List<string> columns = new List<string>() { "Email" };
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter).Select(columns);

var entities = employeeTable.ExecuteQuery(employeeQuery);
foreach (var e in entities)
{
        Console.WriteLine("RowKey: {0}, EmployeeEmail: {1}", e.RowKey, e.Email);
}  
```

請注意如何 hello **RowKey**值為止，即使它不包含屬性 tooretrieve hello 清單中。  

### <a name="modifying-entities"></a>修改實體
hello 儲存體用戶端程式庫可讓您 toomodify 所插入、 刪除和更新的實體儲存 hello 表格服務中的實體。 您可以使用 EGTs toobatch 多個插入、 更新和刪除作業所需一起 tooreduce hello 的往返次數，並改善 hello 效能，您的方案。  

請注意 hello 儲存體用戶端程式庫通常執行 EGT 時擲回例外狀況包含 hello 造成 hello 批次 toofail hello 實體的索引。 當您偵錯使用 EGT 的程式碼時，這會很有幫助。  

您也應該考量您的設計會如何影響用戶端應用程式處理並行存取和更新作業的方式。  

#### <a name="managing-concurrency"></a>管理並行存取
根據預設，hello 表格服務會實作開放式並行存取檢查等級的個別實體的 hello**插入**，**合併**，和**刪除**作業，雖然您可以針對用戶端 tooforce hello 資料表服務 toobypass 這些檢查。 如需如何 hello 表格服務會管理並行存取的詳細資訊，請參閱[管理 Microsoft Azure 儲存體中的並行存取](storage-concurrency.md)。  

#### <a name="merge-or-replace"></a>合併或取代
hello**取代**方法 hello **TableOperation**類別一律會取代 hello 表格服務中的 hello 完整實體。 如果您未包含屬性 hello 要求中儲存的 hello 實體中存在該屬性時，會移除 hello 要求屬性從 hello 儲存實體。 除非您想 tooremove 明確來自預存的實體的屬性，您必須在 hello 要求中包含的每個屬性。  

您可以使用 hello**合併**方法 hello **TableOperation**類別 tooreduce hello 您傳送給 toohello 表格服務時要 tooupdate 實體的資料量。 hello**合併**方法會取代 hello 實體 hello 要求中包含的屬性值中的 hello 儲存實體中的任何屬性，但保留不變 hello 中的任何屬性儲存 hello 要求中未包含的實體。 如果您有大型的實體，且只需 tooupdate 少數的要求中的屬性，這非常有用。  

> [!NOTE]
> hello**取代**和**合併**方法都失敗 hello 實體不存在。 或者，您可以使用 hello **InsertOrReplace**和**InsertOrMerge**建立新的實體，如果不存在的方法。  
> 
> 

### <a name="working-with-heterogeneous-entity-types"></a>使用異質性實體類型
hello 表格服務是*無結構描述*資料表存放區，它表示單一資料表可以儲存多個類型，提供更多的彈性設計的實體。 hello 下列範例說明儲存同時使用 employee 和 department 實體的資料表：  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>名字</th>
<th>姓氏</th>
<th>年齡</th>
<th>電子郵件</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>名字</th>
<th>姓氏</th>
<th>年齡</th>
<th>電子郵件</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>名字</th>
<th>姓氏</th>
<th>年齡</th>
<th>電子郵件</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

請注意，每個實體仍必須要有 **PartitionKey**、**RowKey** 和 **Timestamp** 值，但是可以有任何屬性集。 此外，沒有任何實體的型別 tooindicate hello，除非您選擇 toostore 某處該資訊。 有兩種方式來識別 hello 實體類型：  

* 在前面加上 hello 實體型別 toohello **RowKey** (或可能是 hello **PartitionKey**)。 例如 **EMPLOYEE_000123**，或以 **DEPARTMENT_SALES** 做為 **RowKey** 值。  
* 使用的個別屬性 toorecord hello 實體類型 hello 下表所示。  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>名字</th>
<th>姓氏</th>
<th>年齡</th>
<th>電子郵件</th>
</tr>
<tr>
<td>員工</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>名字</th>
<th>姓氏</th>
<th>年齡</th>
<th>電子郵件</th>
</tr>
<tr>
<td>員工</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>department</td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>名字</th>
<th>姓氏</th>
<th>年齡</th>
<th>電子郵件</th>
</tr>
<tr>
<td>員工</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

hello 第一個選項，前面加上 hello 實體型別 toohello **RowKey**，適合不同類型的兩個實體可能有 hello 可能是否相同機碼值。 它也會群組相同的型別一起 hello 資料分割中的 hello 的實體。  

hello 本章節所討論的技術是特別有關 toohello 討論[繼承關聯性](#inheritance-relationships)hello > 一節中本指南前面提及[模型的關聯性](#modelling-relationships)。  

> [!NOTE]
> 您應該考慮 hello 實體型別值 tooenable 用戶端應用程式 tooevolve POCO 物件中加入版本編號，並使用不同版本。  
> 
> 

hello 本節其餘部分描述的一些 hello 儲存體用戶端程式庫中的 hello 功能來協助使用多個實體類型中 hello 相同資料表。  

#### <a name="retrieving-heterogeneous-entity-types"></a>擷取異質性實體類型
如果您使用 hello 儲存體用戶端程式庫，您必須使用多個實體類型的三個選項。  

如果您知道 hello hello 實體儲存與特定類型**RowKey**和**PartitionKey**值，那麼當您擷取 hello 前兩個範例所示的 hello 實體時，您可以指定 hello 實體類型擷取型別實體**EmployeeEntity**:[執行點查詢使用儲存體用戶端程式庫 hello](#executing-a-point-query-using-the-storage-client-library)和[擷取多個實體使用 LINQ](#retrieving-multiple-entities-using-linq).  

hello 第二個選項為 toouse hello **DynamicTableEntity**類型 （屬性包），而不是具象的 POCO 實體類型 （這個選項可能也改善效能，因為沒有任何需要 tooserialize 和還原序列化 hello 實體太。網路類型）。 hello 下列 C# 程式碼可能 hello 資料表中擷取多個不同類型的實體，但是會傳回所有的實體做**DynamicTableEntity**執行個體。 然後它會使用 hello **EntityType**屬性 toodetermine hello 類型的每個實體：  

```csharp
string filter = TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("PartitionKey",
    QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("RowKey",
                    QueryComparisons.GreaterThanOrEqual, "B"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey",
        QueryComparisons.LessThan, "F")
    )
);
TableQuery<DynamicTableEntity> entityQuery =
    new TableQuery<DynamicTableEntity>().Where(filter);
var employees = employeeTable.ExecuteQuery(entityQuery);

IEnumerable<DynamicTableEntity> entities = employeeTable.ExecuteQuery(entityQuery);
foreach (var e in entities)
{
EntityProperty entityTypeProperty;
if (e.Properties.TryGetValue("EntityType", out entityTypeProperty))
{
    if (entityTypeProperty.StringValue == "Employee")
    {
        // Use entityTypeProperty, RowKey, PartitionKey, Etag, and Timestamp
        }
    }
}  
```

請注意該 tooretrieve 其他屬性，您必須使用 hello **TryGetValue**方法上 hello**屬性**屬性 hello **DynamicTableEntity**類別。  

第三個選項是使用 hello toocombine **DynamicTableEntity**型別和**EntityResolver**執行個體。 這可讓您在 hello tooresolve toomultiple POCO 類型相同的查詢。 在此範例中，hello **EntityResolver**委派使用 hello **EntityType**屬性 toodistinguish hello 查詢所傳回的 hello 兩個類型的實體之間。 hello**解決**方法會使用 hello**解析程式**委派 tooresolve **DynamicTableEntity**執行個體太**TableEntity**執行個體。  

```csharp
EntityResolver<TableEntity> resolver = (pk, rk, ts, props, etag) =>
{

        TableEntity resolvedEntity = null;
        if (props["EntityType"].StringValue == "Department")
        {
        resolvedEntity = new DepartmentEntity();
        }
        else if (props["EntityType"].StringValue == "Employee")
        {
        resolvedEntity = new EmployeeEntity();
        }
        else throw new ArgumentException("Unrecognized entity", "props");

        resolvedEntity.PartitionKey = pk;
        resolvedEntity.RowKey = rk;
        resolvedEntity.Timestamp = ts;
        resolvedEntity.ETag = etag;
        resolvedEntity.ReadEntity(props, null);
        return resolvedEntity;
};

string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<DynamicTableEntity> entityQuery =
        new TableQuery<DynamicTableEntity>().Where(filter);

var entities = employeeTable.ExecuteQuery(entityQuery, resolver);
foreach (var e in entities)
{
        if (e is DepartmentEntity)
        {
    ...
        }
        if (e is EmployeeEntity)
        {
    ...
        }
}  
```

#### <a name="modifying-heterogeneous-entity-types"></a>修改異質性實體類型
您不需要實體 toodelete tooknow hello 類型，以及您一律知道 hello 類型的實體，當您將它插入。 不過，您可以使用**DynamicTableEntity**輸入 tooupdate 實體，而不需要知道它的類型和不使用 POCO 實體類別。 hello 下列程式碼範例會擷取單一實體，並檢查 hello **EmployeeCount**屬性存在，然後再更新它。  

```csharp
TableResult result =
        employeeTable.Execute(TableOperation.Retrieve(partitionKey, rowKey));
DynamicTableEntity department = (DynamicTableEntity)result.Result;

EntityProperty countProperty;

if (!department.Properties.TryGetValue("EmployeeCount", out countProperty))
{
        throw new
        InvalidOperationException("Invalid entity, EmployeeCount property not found.");
}
countProperty.Int32Value += 1;
employeeTable.Execute(TableOperation.Merge(department));  
```

### <a name="controlling-access-with-shared-access-signatures"></a>使用共用存取簽章控制存取
您可以使用共用存取簽章 (SAS) 權杖 tooenable 用戶端應用程式 toomodify （和查詢） 直接不直接與 hello 表格服務的 hello 需要 tooauthenticate 資料表實體。 一般而言，有三個主要優點在於 toousing SAS 應用程式中：  

* 您不需要 toodistribute 您的儲存體帳戶金鑰 tooan 不安全平台 （例如行動裝置） 順序 tooallow 該裝置 tooaccess 和修改 hello 表格服務中的實體。  
* 您可以將某些 hello 工作卸載該 web 和背景工作角色執行中管理您的實體 tooclient 裝置，例如終端使用者電腦和行動裝置。  
* 您可以指派受條件約束和時間限制組的使用權限 tooa 用戶端 （例如 toospecific 資源允許唯讀存取）。  

如需 hello 表格服務搭配使用 SAS 權杖的詳細資訊，請參閱[使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md)。  

不過，您仍必須產生 hello SAS 權杖來授與用戶端 hello 表格服務中的應用程式 toohello 實體： 您應該這麼做有 tooyour 儲存體帳戶金鑰安全存取的環境中。 一般而言，您可以使用 web 或背景工作角色 toogenerate hello SAS 權杖，然後傳遞 toohello 用戶端應用程式需要存取 tooyour 實體。 因為仍有負荷參與產生與傳遞 SAS 權杖 tooclients，您應該考慮如何最佳 tooreduce 這種負荷，尤其是在大量狀況。  

很可能 toogenerate SAS 權杖授與存取的資料表中的 hello 實體 tooa 子集。 根據預設，您會建立 SAS 權杖的一整個資料表，但也可能 toospecify 多種該 hello SAS 權杖授與存取 tooeither **PartitionKey**值或一系列**PartitionKey**和**RowKey**值。 您可能會選擇 toogenerate SAS 權杖，針對個別使用者的系統，每個使用者的 SAS 權杖只允許它們存取 tootheir 自己實體在 hello 表格服務。  

### <a name="asynchronous-and-parallel-operations"></a>非同步和平行作業
假設您要跨多個資料分割分散您的要求，您可以使用非同步或平行查詢來改善輸送量和用戶端的回應性。
例如，您可以用兩個或更多背景工作角色執行個體，以平行方式存取您的資料表。 您無法個別的背景工作角色負責特定集合的資料分割，或只需要多個背景工作角色執行個體，每個無法 tooaccess 所有 hello 資料表中的資料分割。  

在用戶端執行個體中，您可以藉由以非同步方式執行儲存作業來提高輸送量。 hello 儲存體用戶端程式庫可讓您輕鬆 toowrite 非同步查詢的修改。 例如，您可能會開始 hello 同步方法，可擷取所有資料分割中的 hello 實體 hello 下列 C# 程式碼所示：  

```csharp
private static void ManyEntitiesQuery(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

        TableContinuationToken continuationToken = null;

        do
        {
        var employees = employeeTable.ExecuteQuerySegmented(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
    {
        ...
    }
        continuationToken = employees.ContinuationToken;
        } while (continuationToken != null);
}  
```

因此該 hello 查詢執行以非同步方式，如下所示，您可以輕鬆地修改這段程式碼：  

```csharp
private static async Task ManyEntitiesQueryAsync(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);
        TableContinuationToken continuationToken = null;

        do
        {
        var employees = await employeeTable.ExecuteQuerySegmentedAsync(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
        {
            ...
        }
        continuationToken = employees.ContinuationToken;
            } while (continuationToken != null);
}  
```

在非同步範例中，您可以看到從 hello 同步版本的 hello 下列變更：  

* hello 方法簽章現在包含 hello**非同步**修飾詞，並傳回**工作**執行個體。  
* 而不是呼叫 hello **ExecuteSegmented**方法 tooretrieve 結果、 hello 方法現在呼叫 hello **ExecuteSegmentedAsync**方法，並使用 hello **await**修飾詞tooretrieve 會以非同步方式產生。  

hello 用戶端應用程式可以呼叫這個方法多次 (具有不同的值為 hello**部門**參數)，每個查詢將會在另一個執行緒上執行。  

請注意，沒有任何非同步版的 hello **Execute**方法在 hello **TableQuery**類別，因為 hello **IEnumerable**介面不支援非同步列舉型別。  

您也可以透過非同步方式插入、更新和刪除實體。 hello 下列 C# 範例會示範簡單的同步方法 tooinsert 或取代員工實體：  

```csharp
private static void SimpleEmployeeUpsert(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = employeeTable
        .Execute(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

您可以輕鬆地修改這段程式碼，使 hello 更新會以非同步方式，如下所示執行：  

```csharp
private static async Task SimpleEmployeeUpsertAsync(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = await employeeTable
        .ExecuteAsync(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

在非同步範例中，您可以看到從 hello 同步版本的 hello 下列變更：  

* hello 方法簽章現在包含 hello**非同步**修飾詞，並傳回**工作**執行個體。  
* 而不是呼叫 hello **Execute**方法 tooupdate hello 實體、 hello 方法現在呼叫 hello **ExecuteAsync**方法，並使用 hello **await** tooretrieve 修飾詞以非同步方式產生。  

hello 用戶端應用程式可以呼叫這類，多個非同步方法，而且每個方法引動過程會在個別的執行緒上執行。  

### <a name="credits"></a>學分
我們想要遵循的 hello Azure 團隊的成員 toothank hello: Dominic Betts、 Jason Hogg、 Jean Ghanem、 Jai Haridas、 Jeff Irwin、 Vamshidhar Kommineni、 Vinay Shah Serdar Ozler 以及 Microsoft DX 從 Tom Hollander。 

我們也想依照其寶貴的意見反應檢閱循環期間 Microsoft MVP toothank hello: Igor Papirov 和 Edward Bakker。

[1]: ./media/storage-table-design-guide/storage-table-design-IMAGE01.png
[2]: ./media/storage-table-design-guide/storage-table-design-IMAGE02.png
[3]: ./media/storage-table-design-guide/storage-table-design-IMAGE03.png
[4]: ./media/storage-table-design-guide/storage-table-design-IMAGE04.png
[5]: ./media/storage-table-design-guide/storage-table-design-IMAGE05.png
[6]: ./media/storage-table-design-guide/storage-table-design-IMAGE06.png
[7]: ./media/storage-table-design-guide/storage-table-design-IMAGE07.png
[8]: ./media/storage-table-design-guide/storage-table-design-IMAGE08.png
[9]: ./media/storage-table-design-guide/storage-table-design-IMAGE09.png
[10]: ./media/storage-table-design-guide/storage-table-design-IMAGE10.png
[11]: ./media/storage-table-design-guide/storage-table-design-IMAGE11.png
[12]: ./media/storage-table-design-guide/storage-table-design-IMAGE12.png
[13]: ./media/storage-table-design-guide/storage-table-design-IMAGE13.png
[14]: ./media/storage-table-design-guide/storage-table-design-IMAGE14.png
[15]: ./media/storage-table-design-guide/storage-table-design-IMAGE15.png
[16]: ./media/storage-table-design-guide/storage-table-design-IMAGE16.png
[17]: ./media/storage-table-design-guide/storage-table-design-IMAGE17.png
[18]: ./media/storage-table-design-guide/storage-table-design-IMAGE18.png
[19]: ./media/storage-table-design-guide/storage-table-design-IMAGE19.png
[20]: ./media/storage-table-design-guide/storage-table-design-IMAGE20.png
[21]: ./media/storage-table-design-guide/storage-table-design-IMAGE21.png
[22]: ./media/storage-table-design-guide/storage-table-design-IMAGE22.png
[23]: ./media/storage-table-design-guide/storage-table-design-IMAGE23.png
[24]: ./media/storage-table-design-guide/storage-table-design-IMAGE24.png
[25]: ./media/storage-table-design-guide/storage-table-design-IMAGE25.png
[26]: ./media/storage-table-design-guide/storage-table-design-IMAGE26.png
[27]: ./media/storage-table-design-guide/storage-table-design-IMAGE27.png
[28]: ./media/storage-table-design-guide/storage-table-design-IMAGE28.png
[29]: ./media/storage-table-design-guide/storage-table-design-IMAGE29.png

