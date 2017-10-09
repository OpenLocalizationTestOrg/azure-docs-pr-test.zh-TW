---
title: "aaaAzure 存放裝置效能和延展性檢查清單 |Microsoft 文件"
description: "在開發具效能的應用程式中使用 Azure 儲存體的實證做法檢查清單。"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 959d831b-a4fd-4634-a646-0d2c0c462ef8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c2970c055d460070288d1810e4a77a7f056a4137
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-performance-and-scalability-checklist"></a>Microsoft Azure 儲存體效能與延展性檢查清單
## <a name="overview"></a>概觀
Hello hello Microsoft Azure 儲存體服務版本，Microsoft 開發了數實證作法為以高效能的方式使用這些服務，並且這篇文章提供 tooconsolidate hello 其中最重要成檢查清單樣式清單。 這篇文章的 hello 用意是 toohelp 應用程式開發人員，確認它們正在使用 Azure 儲存體和 toohelp 它們找出其他經過證實的作法，應考慮採用經過證實的作法。 這篇文章不會嘗試 toocover 每個可能的效能和擴充性最佳化 — 小的影響或廣泛適用排除它。 hello 應用程式的行為的 toohello 範圍可以預測進行設計時，它會在早期介意有用 tookeep tooavoid 設計所會遇到效能問題。  

使用 Azure 儲存體的每個應用程式開發人員應該採取 hello 時間 tooread 本文中，並檢查 他或她的應用程式遵循每個 hello 證明下面所列的作法。  

## <a name="checklist"></a>檢查清單
本文會證明 hello 作法組織成 hello 下列群組中。 已經實證做法的適用對象：  

* 所有 Azure 儲存體服務 (Blob、資料表、佇列和檔案)
* Blob
* 資料表
* 佇列  

| 完成 | 領域 | 類別 | 問題 |
| --- | --- | --- | --- |
| &nbsp; | 所有服務 |延展性目標 |[設計應用程式 tooavoid 即將 hello 延展性目標嗎？](#subheading1) |
| &nbsp; | 所有服務 |延展性目標 |[是您的命名慣例設計 tooenable 進一步負載平衡嗎？](#subheading47) |
| &nbsp; | 所有服務 |網路 |[用戶端端裝置有夠高的頻寬及需要低度延遲 tooachieve hello 效能？](#subheading2) |
| &nbsp; | 所有服務 |網路 |[用戶端裝置是否有足夠高的品質連結？](#subheading3) |
| &nbsp; | 所有服務 |網路 |[Hello 用戶端應用程式是否位於 <"近乎 hello 儲存體帳戶？](#subheading4) |
| &nbsp; | 所有服務 |內容發佈 |[您是否會使用 CDN 進行內容發佈？](#subheading5) |
| &nbsp; | 所有服務 |直接用戶端存取 |[您使用 SAS 和 CORS tooallow 直接存取 toostorage 而非 proxy？](#subheading6) |
| &nbsp; | 所有服務 |快取 |[您的應用程式是否會針對重複使用和極少變更的資料進行快取？](#subheading7) |
| &nbsp; | 所有服務 |快取 |[您的應用程式是否會批次執行更新 (在用戶端快取更新，然後以大型集合的方式上傳)？](#subheading8) |
| &nbsp; | 所有服務 |.NET 組態 |[您已設定您的用戶端 toouse 足夠數目的並行連線嗎？](#subheading9) |
| &nbsp; | 所有服務 |.NET 組態 |[您已設定.NET toouse 足夠的執行緒數目？](#subheading10) |
| &nbsp; | 所有服務 |.NET 組態 |[您使用的是已改善記憶體回收的 .NET 4.5 或更新版本嗎？](#subheading11) |
| &nbsp; | 所有服務 |平行處理原則 |[您已確保，讓您的用戶端功能 」 或 「 hello 延展性目標不多載平行處理原則適當地限定嗎？](#subheading12) |
| &nbsp; | 所有服務 |工具 |[您可以使用 Microsoft hello 最新版本會提供用戶端程式庫和工具？](#subheading13) |
| &nbsp; | 所有服務 |重試 |[您是否針對節流錯誤和逾時使用指數輪詢重試原則？](#subheading14) |
| &nbsp; | 所有服務 |重試 |[您的應用程式是否避免重試不能再嘗試的錯誤？](#subheading15) |
| &nbsp; | Blob |延展性目標 |[您是嘔有大量的用戶端並行存取單一物件？](#subheading46) |
| &nbsp; | Blob |延展性目標 |[您的應用程式仍使用單一 blob 的 hello 頻寬或作業的延展性目標內？](#subheading16) |
| &nbsp; | Blob |複製 Blob |[您是否以有效的方式複製 Blob？](#subheading17) |
| &nbsp; | Blob |複製 Blob |[您是否使用 AzCopy 進行 Blob 的大量複製？](#subheading18) |
| &nbsp; | Blob |複製 Blob |[您使用 Azure 匯入/匯出 tootransfer 非常大量的資料？](#subheading19) |
| &nbsp; | Blob |使用中繼資料 |[您是否將 Blob 相關的常用中繼資料儲存在它的中繼資料內？](#subheading20) |
| &nbsp; | Blob |快速上傳 |[當快速嘗試 tooupload 一個 blob，您要上傳區塊，以平行方式？](#subheading21) |
| &nbsp; | Blob |快速上傳 |[當快速嘗試 tooupload 許多 blob，您要上傳 blob 以平行方式？](#subheading22) |
| &nbsp; | Blob |正確的 Blob 類型 |[您是否在適當的時機使用分頁 Blob 或區塊 Blob？](#subheading23) |
| &nbsp; | 資料表 |延展性目標 |[是您接近 hello 延展性目標的每秒的實體嗎？](#subheading24) |
| &nbsp; | 資料表 |組態 |[您是否使用 JSON 來處理資料表要求？](#subheading25) |
| &nbsp; | 資料表 |組態 |[您關閉了 Nagle tooimprove hello 效能的小型要求嗎？](#subheading26) |
| &nbsp; | 資料表 |資料表和資料分割 |[您是否已正確分割您的資料？](#subheading27) |
| &nbsp; | 資料表 |常用資料分割 |[您是否避免只開頭附加和只結尾附加模式？](#subheading28) |
| &nbsp; | 資料表 |常用資料分割 |[您的插入/更新是否散佈到許多資料分割中？](#subheading29) |
| &nbsp; | 資料表 |查詢範圍 |[您所設計點查詢 toobe 在大部分情況下，與資料表查詢 toobe 謹慎使用您結構描述的 tooallow 嗎？](#subheading30) |
| &nbsp; | 資料表 |查詢密度 |[您的查詢是否通常只掃描並傳回應用程式將使用的列？](#subheading31) |
| &nbsp; | 資料表 |限制傳回資料 |[您會使用篩選 tooavoid 傳回的實體不需要用到嗎？](#subheading32) |
| &nbsp; | 資料表 |限制傳回資料 |[您使用投影 tooavoid 傳回不需要的屬性？](#subheading33) |
| &nbsp; | 資料表 |反正規化 |[使得嘗試 tooget 資料時，避免效率不佳的查詢或多個讀取的要求有未標準化資料嗎？](#subheading34) |
| &nbsp; | 資料表 |插入/更新/刪除 |[您會批次要求需要 toobe 交易式，或者可以在 hello 相同時間 tooreduce 往返嗎？](#subheading35) |
| &nbsp; | 資料表 |插入/更新/刪除 |[您會避免擷取實體只 toodetermine toocall 是否插入或更新？](#subheading36) |
| &nbsp; | 資料表 |插入/更新/刪除 |[您是否考慮將經常會被一起擷取的一系列資料，以屬性的方式儲存在單一實體中 (而非儲存在多個實體中)？](#subheading37) |
| &nbsp; | 資料表 |插入/更新/刪除 |[針對總是會被一起擷取並可以批次執行方式寫入的實體 (例如時間序列資料)，您是否考慮使用 Blob (而非資料表)？](#subheading38) |
| &nbsp; | 佇列 |延展性目標 |[每秒的訊息是您接近 hello 延展性目標嗎？](#subheading39) |
| &nbsp; | 佇列 |組態 |[您關閉了 Nagle tooimprove hello 效能的小型要求嗎？](#subheading40) |
| &nbsp; | 佇列 |訊息大小 |[Compact tooimprove hello 效能 hello 佇列的是您的郵件？](#subheading41) |
| &nbsp; | 佇列 |大量擷取 |[您是否在單一 "Get" 操作中擷取多則訊息？](#subheading42) |
| &nbsp; | 佇列 |輪詢頻率 |[正在輪詢經常看得見您的應用程式的延遲足夠 tooreduce hello？](#subheading43) |
| &nbsp; | 佇列 |更新訊息 |[您使用 UpdateMessage toostore 進度中處理訊息，避免必須 tooreprocess hello 整個訊息，如果發生錯誤？](#subheading44) |
| &nbsp; | 佇列 |架構 |[您使用佇列 toomake 整個應用程式更具擴充性透過獨立然後維持長時間執行工作負載超出 hello 關鍵路徑和小數位數？](#subheading45) |

## <a name="allservices"></a>所有服務
此區段會列出實證適用 toohello 使用任何 hello Azure 儲存體服務 （blob、 資料表、 佇列或檔案） 的作法。  

### <a name="subheading1"></a>延展性目標
每個 hello Azure 儲存體服務具有延展性目標容量 (GB)，交易率和頻寬。 如果您的應用程式接近或超過任何 hello 延展性目標，它可能會遇到增加了的交易延遲或節流。 當儲存體服務會先調節應用程式時，hello 服務會開始 tooreturn 「 503 伺服器忙碌中 」 或 「 500 作業逾時 」 錯誤代碼的某些儲存體交易。 本節將討論這兩個具有延展性目標和頻寬延展性目標的 hello 一般方法 toodealing 特別。 處理個別的儲存體服務的後續章節將討論在 hello 內容中的該特定服務的延展性目標：  

* [Blob 頻寬和每秒要求數](#subheading16)
* [每秒的資料表實體](#subheading24)
* [每秒佇列訊息](#subheading39)  

#### <a name="sub1bandwidth"></a>所有服務的頻寬延展性目標
Hello 撰寫本文時，在 hello 美國地理備援儲存體 (GRS) 帳戶中的 hello 頻寬目標都是 10 gb / 秒 (Gbps) 的輸入 （資料會傳送 toohello 儲存體帳戶） 和 20 Gbps 輸出 （hello 儲存體帳戶所送出的資料）。 本機備援儲存體 (LRS) 帳戶，hello 限制較高的-20 Gbps 針對 ingress 和 egress 30 gbps 之間。  國際頻寬可能有較低的限制，您可以在我們的 [延展性目標頁面](http://msdn.microsoft.com/library/azure/dn249410.aspx)上找到此資訊。  如需有關 hello 儲存體備援選項的詳細資訊，請參閱中的 hello 連結[實用資源](#sub1useful)下方。  

#### <a name="what-toodo-when-approaching-a-scalability-target"></a>接近的延展性目標時，哪些 toodo
如果您的應用程式已接近 hello 單一儲存體帳戶的延展性目標，請考慮採用下列方法 hello 的其中一個：  

* 考慮會導致應用程式 tooapproach 的 hello 工作負載，或超出 hello 延展性目標。 可以在設計以不同的方式較少的頻寬或容量或較少的交易 toouse 嗎？
* 如果應用程式必須超過 hello 延展性目標的其中一個，您應該建立多個儲存體帳戶和資料分割應用程式資料的多個儲存體帳戶間。 如果您使用此模式，則是確定 toodesign 您的應用程式，讓您可以新增更多的儲存體帳戶中 hello 未來進行負載平衡。 在撰寫本文時，每個 Azure 訂用帳戶可以有 too100 儲存體帳戶。  除了儲存資料、進行交易或傳輸資料等使用方式外，儲存體帳戶也不會有其他費用。
* 如果您的應用程式叫用 hello 頻寬目標時，請考慮壓縮 hello 用戶端 tooreduce hello 所需的頻寬 toosend hello 資料 toohello 儲存體服務中的資料。  請注意，在節省頻寬並提高網路效能的同時，這也可能出現某些負面影響。  您應該評估這個到期 toohello 其他的處理需求來壓縮和解壓縮資料 hello 用戶端中的 hello 效能影響。 此外，儲存壓縮的資料可讓更困難 tootroubleshoot 問題，因為它可能是使用標準工具更難 tooview 儲存資料。
* 如果您的應用程式叫用 hello 延展性目標時，請確定您使用指數型輪詢重試 (請參閱[重試](#subheading14))。  它的較佳 toomake 確定永遠不會處理 hello 延展性目標 （透過使用其中一個方法上方的 hello），但這可確保您的應用程式將不會只維持快速重試，進行節流變差的 hello。  

#### <a name="useful-resources"></a>有用資源
下列連結查看 hello 提供延展性目標的其他詳細資料：

* 如需延展性目標的資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md) 。
* 請參閱[Azure 儲存體複寫](storage-redundancy.md)hello 部落格文章和[Azure 儲存體備援選項和讀取權限地理備援儲存體](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx)有關儲存體備援選項。
* 如需 Azure 服務定價的最新資訊，請參閱 [Azure 定價](https://azure.microsoft.com/pricing/overview/)。  

### <a name="subheading47"></a>分割區命名慣例
Azure 儲存體使用範圍架構的資料分割配置 tooscale 和負載平衡 hello 系統。 hello 資料分割索引鍵已使用的 toopartition 資料成範圍，而且這些範圍系統中都是負載平衡 hello。 這表示例如語彙排序 （例如 msftpayroll、 msftperformance、 msftemployees 等等），或使用時間戳記 （log20160101、 log20160102、 log20160102 等等） 的命名慣例將共享 toohello 資料分割正在潛在共置於 hello相同資料分割伺服器上，直到負載平衡作業會將它們分成較小的範圍。 例如，容器內的所有 blob 會都提供由單一伺服器上，直到 hello 負載這些 blob 需要進一步重新平衡 hello 分割區範圍。 同樣地，一群輕的帳戶，以語彙順序排列其名稱可能會提供服務由單一伺服器 hello 直到載入上一個或所有這些帳戶都需要它們 toobe 分割跨越多個資料分割伺服器。 每項負載平衡作業可能會影響 hello 延遲的儲存體呼叫 hello 作業期間。 hello 系統的能力 toohandle 突然出現尖峰流量 tooa 磁碟分割的單一資料分割伺服器 hello 延展性受限於直到 hello 負載平衡作業已盡力而為中，重新平衡 hello 資料分割索引鍵範圍。  

您可以依照這類作業某些最佳作法 tooreduce hello 頻率。  

* 請檢查您使用的帳戶、 容器、 blob、 資料表和佇列，密切 hello 命名慣例。 請考慮使用最符合您需求的雜湊函數，在帳戶名稱前加上 3 位數的雜湊。  
* 如果您將組織資料，可使用時間戳記或數字識別元，則必須 tooensure 您不使用僅附加 （或僅前面加上） 的流量模式。 這些模式並不適合範圍為基礎系統、 分割及無法負責人 tooall hello 流量進入 tooa 單一資料分割和限制 hello 系統從有效負載平衡。 比方說，如果您有每日使用時間戳記，例如 yyyymmdd，然後 hello 的所有流量 blob 物件的每日作業的作業會導向 tooa 單一物件由單一資料分割伺服器。 看看是否會限制每個 blob 的 hello 和限制您的需求和分解成多個 blob 的這項作業，如有需要請考慮每個資料分割。 同樣地，如果您在資料表中儲存時間序列資料，可能是 hello 的所有流量導向 toohello 最後一部分 hello 索引鍵的命名空間。 如果您必須使用時間戳記或數字的識別碼，作為前置詞 hello 識別碼與 3 位數雜湊或時間戳記前置詞 hello 秒數部分 hello 時間，例如 ssyyyymmdd hello 案例。 如果定期執行列出和查詢作業，請選擇會限制查詢次數的雜湊函數。 其他情況，隨機的前置詞即足以應付。  
* 其他資料分割配置使用 Azure 儲存體中的 hello 的詳細資訊，請參閱 hello sosp 文件[這裡](http://sigops.org/sosp/sosp11/current/2011-Cascais/printable/11-calder.pdf)。

### <a name="networking"></a>網路
Hello API 呼叫上述不相關，而通常 hello 實體網路的條件約束 hello 應用程式效能造成顯著的影響。 hello 以下說明的某些使用者可能會遇到的限制。  

#### <a name="client-network-capability"></a>用戶端網路功能
##### <a name="subheading2"></a>輸送量
為了使頻寬，hello 問題通常是 hello hello 用戶端功能。 例如，當單一儲存體帳戶可處理 10 Gbps 以上的輸入時 (請參閱[頻寬延展性目標](#sub1bandwidth))，「 小型 」 的 Azure 背景工作角色執行個體中的 hello 網路速度，才能夠大約 100 Mbps。 較大型的 Azure 執行個體擁有較大容量的 NIC，因此，如果您需要單一機器的較高網路限制，您應考慮使用較大型的執行個體或更多的 VM。 如果您要從開啟的內部部署應用程式存取儲存體服務，則 hello 相同規則適用於： 了解 hello 的 hello 用戶端裝置和 hello 網路連線 toohello Azure 儲存體位置的網路功能，並可改善這些視或設計您的應用程式 toowork 內其功能。  

##### <a name="subheading3"></a>連結品質
與任何網路使用方式一樣，請留意導致錯誤和封包遺失的網路狀況將會減慢有效的輸送量。  使用 WireShark 或 NetMon 可能有助於診斷此問題。  

##### <a name="useful-resources"></a>有用資源
如需虛擬機器大小與所配置頻寬的詳細資訊，請參閱 [Windows VM 大小](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)或 [Linux VM 大小](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。  

#### <a name="subheading4"></a>位置
在任何分散式環境中，放置 hello 附近 toohello 伺服器的用戶端傳遞 hello 達到最佳效能。 存取 Azure 儲存體與 hello 最低延遲，請針對您的用戶端 hello 最佳位置是 hello 內相同的 Azure 區域。 例如，如果您擁有使用 Azure 儲存體的 Azure 網站，您應將這兩者置於單一區域內 (例如，美國西部或東南亞)。 這樣會減少 hello 延遲與成本的 hello — hello 撰寫本文時，在單一區域內的頻寬是免費的。  

如果您的用戶端應用程式不會裝載在 Azure 中 （例如行動裝置應用程式或內部部署企業服務），然後再次將 hello 儲存體帳戶放在附近 toohello 裝置存取它，區域將通常降低延遲。 如果您的用戶端分散的十分廣泛 (例如，有些用戶端在北美，有些在歐洲)，則您應考慮使用多個儲存體帳戶：一個位於北美地區，一個位於歐洲地區。 這將有助於 tooreduce 延遲兩個區域中的使用者。 這種方法時，通常更容易 tooimplement hello 資料 hello 應用程式存放區為特定 tooindividual users，而且不需要儲存體帳戶之間複寫資料。  廣泛的內容發佈，建議使用 CDN – 請參閱 hello 下一節，如需詳細資訊。  

### <a name="subheading5"></a>內容發佈
有時候，在位於相同的內容 toomany 使用者 （例如產品示範 hello 首頁上的網站中使用的視訊），應用程式需求 tooserve hello hello 同一個或多個區域。 在此案例中，您應該使用內容傳遞網路 (CDN)，例如 Azure CDN，hello CDN 會使用 Azure 儲存體，當做 hello hello 資料來源。 不同的 Azure 儲存體帳戶存在於單一區域，無法將內容傳遞低延遲 tooother 區域，Azure CDN 會使用伺服器 hello 世界各地的多個資料中心內。 此外，CDN 通常可以支援比單一儲存體帳戶高很多的輸出限制。  

如需 Azure CDN 的詳細資訊，請參閱 [Azure CDN](https://azure.microsoft.com/services/cdn/)。  

### <a name="subheading6"></a>使用 SAS 和 CORS
當您需要 JavaScript 等使用者 web 瀏覽器或 Azure 儲存體中的行動電話應用程式 tooaccess 資料中的 tooauthorize 程式碼時，其中一個方法是 toouse 做為 proxy 的 web 角色中的應用程式： hello 使用者的裝置驗證 hello web 角色，其在開啟驗證與 hello 儲存體服務。 如此一來，您可以避免在未受到保護的裝置上公開您的儲存體帳戶金鑰。 然而，這會造成較大的工作負擔 hello web 角色上因為 hello 使用者的裝置之間傳送的 hello 的所有資料和 hello 儲存體服務都必須經過 hello web 角色。 您可以避免跨原始資源共用標頭 」 (CORS) 搭配使用共用存取簽章 (SAS)，有時也做為 proxy 使用 web 角色 hello 儲存體服務。 使用 SAS 時，您可以讓您的使用者裝置 toomake 要求直接 tooa 儲存體服務透過有限的存取語彙基元。 比方說，如果使用者想 tooupload 相片 tooyour 應用程式時，web 角色就可以產生並傳送 toohello 使用者的裝置會授與權限 toowrite tooa 特定 blob 或容器 hello （hello SAS 權杖過期前） 的 下一步 30 分鐘的 SAS 權杖。

一般來說，在瀏覽器將不允許 JavaScript 等"PUT"tooanother 網域一個網域 tooperform 作業特定的網站所裝載的網頁中。 例如，如果您裝載 web 角色在"contosomarketing.cloudapp.net 」，並想 toouse 用戶端端 JavaScript tooupload"contosoproducts.blob.core.windows.net"blob tooyour 儲存體帳戶，hello 瀏覽器的 「 相同來源原則 」 將禁止這作業。 CORS 是瀏覽器的功能，可讓 hello 目標網域 （在此案例的 hello 儲存體帳戶） toocommunicate toohello 瀏覽器信任要求源自於 hello 來源網域中 （在此案例的 hello 的 web 角色）。  

這些技術可協助您避免 Web 應用程式上的不必要負荷 (和瓶頸)。  

#### <a name="useful-resources"></a>有用資源
如需 SAS 的詳細資訊，請參閱[共用存取簽章，第 1 部分： 了解 hello SAS 模型](../storage-dotnet-shared-access-signature-part-1.md)。  

如需有關 CORS 的詳細資訊，請參閱[hello Azure 儲存體服務的跨原始資源共用 (CORS) 支援](http://msdn.microsoft.com/library/azure/dn535601.aspx)。  

### <a name="caching"></a>快取
#### <a name="subheading7"></a>取得資料
一般來說，從服務中一次取得資料勝過分兩次取得資料。 請考慮 MVC web 應用程式執行 web 角色已從 hello 儲存體服務 tooserve 內容 tooa 使用者擷取 50 MB blob 中的 hello 範例。 hello 應用程式無法擷取該相同 blob 每次使用者要求，或它可以快取在本機 toodisk 和重複使用 hello 快取的版本的後續使用者要求。 此外，每當使用者要求 hello 資料時，hello 應用程式可以發出 GET 與條件式標頭修改時間，這會避免發生 hello 整個 blob。 如果它尚未被修改。 您可以套用這個相同的模式 tooworking 資料表實體。  

在某些情況下，您可能會決定您的應用程式可以假設該 hello blob 擷取它，而且，在此期間 hello 期間應用程式不需要 toocheck 如果 hello blob 已修改後的短暫仍然有效。

設定、 查閱和 hello 應用程式永遠會使用其他資料是很好的候選項快取。  

如需如何 tooget blob 的內容 toodiscover hello 的上次修改日期的範例使用.NET，請參閱[設定和擷取屬性和中繼資料](../blobs/storage-properties-metadata.md)。 如需條件式下載的詳細資訊，請參閱 [有條件地重新整理 Blob 的本機複本](http://msdn.microsoft.com/library/azure/dd179371.aspx)。  

#### <a name="subheading8"></a>以批次方式上傳資料
在某些應用程式案例中，您可以在本機彙總資料，然後以批次方式將它定期上傳，而非立即上傳每一份資料。 例如，web 應用程式可能會保留的活動記錄檔： hello 應用程式可能是上傳的每個活動的詳細資料發生視為資料表實體 （這需要許多儲存體作業），或其無法儲存活動詳細資料 tooa 本機記錄檔，然後按一下以分隔的檔案 tooa blob 定期上傳所有活動詳細資料。 如果每個記錄項目大小為 1 KB，您可以上傳千分位在單一的 「 Put Blob 」 交易 （您可以將 blob 上傳的總大小，在單一交易中 too64MB）。 當然，如果 hello 本機電腦當機前 toohello 上傳，您將可能遺失某些記錄檔資料： hello 應用程式開發人員必須設計為用戶端裝置 hello 可能性或上傳失敗。  如果 hello 活動資料需要 toobe 下載的時間範圍 （不是單一活動），blob 會建議資料表。

### <a name="net-configuration"></a>.NET 組態
如果使用 hello.NET Framework，此區段會列出您可以使用 toomake 顯著的效能改善的數個快速的組態設定。  如果使用其他語言，請檢查 toosee 如果類似的概念適用於您所選擇的語言。  

#### <a name="subheading9"></a>提高預設的連線限制
在.NET 中，下列程式碼的 hello 增加 hello 預設連線限制 （這通常是 2 的用戶端環境中或在伺服器環境中的 10） too100。 一般而言，您應該設定應用程式所使用的執行緒 hello 值 tooapproximately hello 的數目。  

```csharp
ServicePointManager.DefaultConnectionLimit = 100; //(Or More)  
```

您必須設定 hello 連線限制，才開啟任何連接。  

其他程式設計語言，請參閱該語言的文件 toodetermine tooset hello 連線的數量限制。  

如需詳細資訊，請參閱 hello 部落格文章[Web 服務： 並行連線](http://blogs.msdn.com/b/darrenj/archive/2005/03/07/386655.aspx)。  

#### <a name="subheading10"></a>如果使用同步程式碼搭配 Async Task，則提高 ThreadPool 的執行緒數量下限
此程式碼將會增加 hello 執行緒集區最小值：  

```csharp
ThreadPool.SetMinThreads(100,100); //(Determine hello right number for your application)  
```

如需詳細資訊，請參閱 [ThreadPool.SetMinThreads 方法](http://msdn.microsoft.com/library/system.threading.threadpool.setminthreads%28v=vs.110%29.aspx)。  

#### <a name="subheading11"></a>充分運用 .NET 4.5 記憶體回收
Hello 用戶端應用程式的伺服器記憶體回收中的效能改進的 tootake 優點適用於.NET 4.5 或更新版本。

如需詳細資訊，請參閱 hello 文章[概觀的效能改進中.NET 4.5](http://msdn.microsoft.com/magazine/hh882452.aspx)。  

### <a name="subheading12"></a>無限制的平行處理原則
雖然平行處理原則可能很大的效能，請小心使用 unbounded 平行處理原則 （hello 執行緒及/或平行要求數目沒有限制） tooupload 或下載資料、 使用多個工作者 tooaccess 多個資料分割 (容器、 佇列，或資料表資料分割） 中請 hello 相同儲存體帳戶或 tooaccess hello 中的多個項目相同的資料分割。 Hello 平行處理原則未繫結，如果您的應用程式可以超過 hello 用戶端裝置的功能，或者 hello 導致較長的延遲和節流的儲存體帳戶的延展性目標。  

### <a name="subheading13"></a>儲存體用戶端程式庫和工具
一律使用最新版 Microsoft 提供的用戶端程式庫 hello 和工具。 在 hello 撰寫本文時，有適用於.NET、 Windows Phone、 Windows 執行階段、 Java 和 c + + 的用戶端程式庫，以及針對其他語言的預覽文件庫。 此外，Microsoft 也推出 PowerShell Cmdlet 和 Azure CLI 命令，可與 Azure 儲存體搭配使用。 Microsoft 主動開發這些工具與效能，請注意，保持 toodate hello 最新的服務版本，並確保這些 helper 能夠處理許多 hello 內部通過驗證的效能最佳。  

### <a name="retries"></a>重試
#### <a name="subheading14"></a>節流/ServerBusy
在某些情況下，hello 儲存體服務會進行節流處理您的應用程式或可能只是無法 tooserve hello 要求，因為 toosome 暫時性狀況與傳回 「 500 逾時 」 或 「 503 伺服器忙碌中 」 訊息。  如果您的應用程式即將任何 hello 延展性目標，或是 hello 系統會重新平衡您的資料分割的資料 tooallow 的較高的輸送量，也可能會發生。  hello 用戶端應用程式通常應該重試 hello 作業會造成這類錯誤： 嘗試的 hello 相同要求稍後才會成功。 不過，如果 hello 儲存體服務節流處理您的應用程式，因為它超出延展性目標或即使 hello 服務因其他原因是無法 tooserve hello 提出要求時，積極重試通常會使 hello 問題更加複雜。 基於這個理由，您應該使用指數回關 （hello 用戶端程式庫預設 toothis 行為）。 例如，您的應用程式可能會在 2 秒後進行重試、然後 4 秒、然後 10 秒、然後 30 秒，最後會完全放棄。 這個行為會導致您的應用程式會大幅降低其 hello 服務上的負載，而非 exacerbating 任何問題。  

請注意，連接錯誤可重試，因為它們不是節流的 hello 結果，而且會預期的 toobe 暫時性。  

#### <a name="subheading15"></a>無法重試的錯誤
hello 用戶端程式庫並知道哪些錯誤可重試，而且並不是。 不過，如果您正在撰寫自己的程式碼對 hello 儲存體 REST API，請記住一些您應該不會重試的錯誤： 例如，400 （不正確的要求） 回應指出該 hello 用戶端應用程式傳送的要求，因為無法處理它未預期的格式。 重新傳送此要求會導致 hello 相同的回應每次，因此沒有在重試該點。 如果您正在撰寫自己的程式碼對 hello 儲存體 REST API，請留意哪些 hello 錯誤碼平均值和 hello 的正確方式 tooretry （或停用） 針對每一項。  

#### <a name="useful-resources"></a>有用資源
如需儲存體錯誤碼的詳細資訊，請參閱[狀態和錯誤碼](http://msdn.microsoft.com/library/azure/dd179382.aspx)hello Microsoft Azure 網站上。  

## <a name="blobs"></a>Blob
在加法 toohello 證實的作法[所有服務](#allservices)先前所述，證明作法 hello 下列套用特別 toohello blob 服務。  

### <a name="blob-specific-scalability-targets"></a>Blob 特定的延展性目標
#### <a name="subheading46"></a>並行存取單一物件的多個用戶端
如果您有大量的並行存取單一物件的用戶端必須 tooconsider 每個物件和儲存體帳戶延展性目標。 hello 確切數目的用戶端可以存取的單一物件，將要求的用戶端 hello 物件同時 hello hello 物件大小的 hello 數目等因素而有所不同，網路狀況等。

如果透過散發 hello 物件從網站的影像或視訊等 CDN 服務，則您應該使用 CDN。 請參閱 [這裡](#subheading5)。

在其他情況下，例如其中 hello 資料是機密的科學模擬您有兩個選項。 hello 第一個是的 toostagger 存取您的工作負載存取這類 hello 物件在一段時間與同步存取。 或者，您可以暫時複製因而增加 hello 每個物件，以及跨儲存體帳戶的 IOPS 總數的 hello 物件 toomultiple 儲存體帳戶。 在有限的測試，我們發現，大約 25 Vm 無法同時下載由發佈 100 GB 的 blob，以平行方式 （每個 VM 的平行處理 hello 下載使用 32 個執行緒）。 如果您有 100 個用戶端需要 tooaccess hello 物件時，先將它複製 tooa 第二個儲存體帳戶，擁有 hello 前 50 個 Vm 存取 hello 第一個 blob 然後 hello 50 第二個 Vm 存取 hello 第二個 blob。 結果將會視您的應用程式行為而有所不同，因此您應該在設計期間進行測試。 

#### <a name="subheading16"></a>每個 Blob 的頻寬和作業
您可以讀取或寫入 tooa 單一 blob 在向上 tooa 最大值為 60 MB/秒 (這是大約 480 的 mbps 之間超過 hello 許多用戶端網路功能 (包括 hello hello 用戶端裝置上的實體 NIC)。 此外，單一 blob 最多可支援 too500 每秒要求數。 如果您有多個用戶端需要 tooread hello 相同的 blob，並可能會超過這些限制，您應該考慮使用 CDN 發佈 hello blob。  

如需 Blob 的目標輸送量詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md)。  

### <a name="copying-and-moving-blobs"></a>複製與移動 Blob
#### <a name="subheading17"></a>複製 Blob
跨帳戶 hello 儲存體 REST API 2012-02-12 版導入的 hello 有用能力 toocopy blob： 用戶端應用程式可以指示 hello 儲存體服務 toocopy 從 （可能位於不同的儲存體帳戶），另一個來源 blob，然後讓 hello服務會以非同步方式執行 hello 複製。 這可以大幅降低 hello hello 應用程式時您是從其他儲存體帳戶將資料移轉，因為您不需要 toodownload 與 hello 資料上傳所需的頻寬。  

一個考量，不過的不是，當儲存體帳戶之間進行複製，任何時間保證 hello 複製完成。 如果您的應用程式需要的 toocomplete blob 快速複製您能夠控制，它可能更好的 toocopy hello blob 下載它 tooa VM，然後將它上傳 toohello 目的地。  在此情況下的完整可預測性，請確定 hello 複製在執行由 hello 中執行的 VM 相同的 Azure 區域，或其他網路狀況可能 （和可能會） 會影響您複製的效能。  此外，您可以透過程式設計方式監視 hello 進度的非同步複本。  

請注意，相同的儲存體帳戶本身通常會迅速完成的 hello 內複製。  

如需詳細資訊，請參閱 [複製 Blob](http://msdn.microsoft.com/library/azure/dd894037.aspx)。  

#### <a name="subheading18"></a>使用 AzCopy
hello Azure 儲存體團隊發行了命令列工具 」 AzCopy"也就是它們的 toohelp 具有大量傳送至、 和儲存體帳戶間的許多 blob。  此工具已針對此案例進行最佳化，且可達到高傳輸率。  建議在大量上傳、下載和複製案例中使用此工具。 詳細資訊，請參閱 toolearn 和下載，請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)。  

#### <a name="subheading19"></a>Azure 匯入/匯出服務
Hello Azure 儲存體非常大量的資料 (超過 1 TB)，提供 hello 匯入/匯出服務，以便允許上傳和下載從 blob 儲存體傳送的硬碟機。  您可以讓硬碟機上的資料並將它上傳，tooMicrosoft 或傳送空白的硬碟機 tooMicrosoft toodownload 資料。  如需詳細資訊，請參閱[使用 hello Microsoft Azure 匯入/匯出服務 tooTransfer 資料 tooBlob 儲存體](../storage-import-export-service.md)。  這可以是比上傳/下載此磁碟區資料的 hello 網路上更有效率。  

### <a name="subheading20"></a>使用中繼資料
hello blob 服務支援標頭的要求，其中包含有關 hello blob 的中繼資料。 例如，如果您的應用程式需要相片的 hello EXIF 資料，它無法擷取 hello 相片，並將它解壓縮。 toosave 頻寬並提升效能，您的應用程式無法 hello EXIF 將資料儲存在 hello blob 的中繼資料時 hello 應用程式上傳相片 hello： 您可以再擷取 hello EXIF 資料使用只有 HEAD 要求的中繼資料中節省大量頻寬並且 hello 處理時間所需 tooextract hello EXIF 資料讀取每個時間 hello blob。 這會是適用於您只需要 hello 中繼資料，並不 hello 完整 blob 的內容的情況。  請注意只有 8 KB 的中繼資料，可以儲存每個 blob （hello 服務不會接受要求 toostore 超過該值），所以如果該大小無法容納 hello 資料，您可能不是這種方法可以 toouse。  

如需如何 tooget blob 的中繼資料使用的.NET，請參閱[設定和擷取屬性和中繼資料](../blobs/storage-properties-metadata.md)。  

### <a name="uploading-fast"></a>快速上傳
tooupload blobs 快速，第一個問題 tooanswer hello 是： 您上傳 blob 的一或多個？  使用以下指南根據您的案例 toodetermine hello 正確方法 toouse hello。  

#### <a name="subheading21"></a>快速上傳一個大型 Blob
單一大型 blob 快速 tooupload，用戶端應用程式應上傳的區塊或以平行方式 （要注意 hello 個別 blob 和整體 hello 儲存體帳戶的延展性目標） 的頁面。  請注意，hello 官方 Microsoft 薽俇 RTM 儲存體用戶端程式庫 （.NET、 Java） hello 能力 toodo 這。  針對每個 hello 文件庫中，使用以下指定的物件屬性 tooset hello 並行存取層級的 hello:  

* .NET： 集 ParallelOperationThreadCount 用 BlobRequestOptions 物件 toobe 上。
* Java/Android：使用 BlobRequestOptions.setConcurrentRequestCount()
* Node.js： 使用 parallelOperationThreadCount 任一 hello 要求選項或 hello blob 服務上。
* C + +: 使用 hello blob_request_options:: set_parallelism_factor 方法。

#### <a name="subheading22"></a>快速上傳多個 Blob
tooupload 許多快速，blob 上傳 blob 以平行方式。 這是較快，單一 blob 一次使用上載平行區塊上傳因為它會將 hello 上載分散到多個資料分割的 hello 儲存體服務。 單一 Blob 僅支援 60 MB/秒 (大約是 480 Mbps) 的輸送量。 Hello 撰寫本文時，美國 LRS 帳戶最多可支援 too20 Gbps 輸入，這可能會遠比 hello 輸送量受到個別的 blob。  [AzCopy](#subheading18) 依預設會執行平行上傳，在此案例中我們建議使用此方法。  

### <a name="subheading23"></a>選擇 blob 的 hello 正確的型別
Azure 儲存體支援兩種 Blob：分頁 Blob 和區塊 Blob。 針對特定的使用案例，hello 效能和延展性的方案，將會影響您選擇的 blob 類型。 有效率地在 tooupload 大量資料時，區塊 blob 非常適當： 例如，用戶端應用程式可能需要 tooupload 相片或視訊 tooblob 儲存體。 分頁 blob 適合如果 hello 應用程式需要 tooperform 隨機寫入在 hello 資料： 例如，Azure Vhd 會儲存為分頁 blob。  

如需詳細資訊，請參閱 [了解區塊 Blob、附加 Blob 和分頁 Blob](http://msdn.microsoft.com/library/azure/ee691964.aspx)。  

## <a name="tables"></a>資料表
在加法 toohello 證實的作法[所有服務](#allservices)先前所述，證明作法 hello 下列套用特別 toohello 表格服務。  

### <a name="subheading24"></a>資料表特定的延展性目標
中的整個儲存體帳戶的加法 toohello 頻寬限制，資料表具有下列特定的延展性限制的 hello。  請注意，hello 系統將負載平衡流量的增加，但如果您的流量具有量突然暴增，您可能不是 立即無法 tooget 此磁碟區的輸送量。  如果您的模式有暴增、 toosee 節流，您應該會和/或逾時期間 hello 高載 hello 儲存體服務作為自動負載平衡移出您的資料表。  緩時變通常根本上有更好的結果，適當地讓 hello 系統時間 tooload 餘額。  

#### <a name="entities-per-second-account"></a>每秒的實體數 (帳戶)
hello 延展性限制存取的資料表為向上 too20，000 實體 (每一個 1 KB) 每秒的帳戶。  一般來說，已插入、更新、刪除或掃描的每個實體都會算在這個目標內。  因此包含 100 個實體的批次插入會算為 100 個實體。  掃描 1,000 個實體並傳回 5 的查詢會算為 1,000 個實體。  

#### <a name="entities-per-second-partition"></a>每秒的實體數 (資料分割)
在單一資料分割，hello 延展性目標為存取資料表為 2000 實體 (每一個 1 KB) 每秒，使用 hello 相同計數 hello 上一節中所述。  

### <a name="configuration"></a>組態
此區段會列出您可以在 hello 表格服務中使用 toomake 顯著的效能改善的數個快速的組態設定：  

#### <a name="subheading25"></a>使用 JSON
開始儲存體服務版本 2013年-08-15，hello 表格服務支援使用 JSON 而不 hello 以 XML 為基礎的 AtomPub 格式，將資料表資料傳輸。 這可以減少裝載大小最多可達 75%，並可大幅提升應用程式的 hello 效能。

如需詳細資訊，請參閱文章 hello [Microsoft Azure 資料表： JSON 簡介](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/05/windows-azure-tables-introducing-json.aspx)和[表格服務作業的裝載格式](http://msdn.microsoft.com/library/azure/dn535600.aspx)。

#### <a name="subheading26"></a>關閉 Nagle
跨 TCP/IP 網路表示 tooimprove 網路效能廣泛實作的 Nagle 演算法。 不過，它並非是所有情況下的最佳作法 (例如高互動式環境)。 Azure 儲存體而言的 Nagle 演算法 hello 要求 toohello 資料表和佇列服務，效能有負面影響，您應該停用的話。  

如需詳細資訊，請參閱我們的部落格文章[Nagle 的演算法是不好記往小要求](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx)，其中說明 Nagle 的演算法為何不良互動資料表和佇列的要求，並示範如何 toodisable 在您的用戶端應用程式。  

### <a name="schema"></a>結構描述
代表及查詢資料的方式是 hello 最大單一因素會影響 hello hello 表格服務的效能。 雖然每個應用程式都有所不同，本節將概述與下列項目相關的部分一般已經實證做法：  

* 資料表設計
* 有效率的查詢
* 有效率的資料更新  

#### <a name="subheading27"></a>資料表和資料分割
資料表會被分為幾個資料分割。 儲存的每個實體資料分割中共用 hello 相同的資料分割索引鍵與具有唯一資料列的索引鍵 tooidentify 在該資料分割。 資料分割提供了優點，但也同時引進延展性限制。  

* 優點： 您可以更新相同資料分割，包含 too100 不同儲存體作業 （限制為 4 MB 的大小總計） 的單一、 不可部分完成的批次交易中的 hello 中的實體。 假設 hello 相同數目的實體 toobe 擷取，您也可以查詢內的單一資料分割的資料比橫跨資料分割 （雖然閱讀，以取得進一步的查詢資料表資料的建議） 的資料，更有效率。
* 延展性限制： 存取 tooentities 儲存在單一磁碟分割不能是負載平衡因為資料分割支援不可部分完成的批次交易。 基於這個理由，hello 延展性目標為每個個別的資料表資料分割會低於 hello 表格服務的整體。  

因為這些特性的資料表和資料分割，您應該採用下列設計原則的 hello:  

* 用戶端應用程式經常更新，或查詢的 hello 應該位於相同的邏輯單元的工作中的資料 hello 相同的資料分割。  這可能是因為您的應用程式正在彙總寫入，或您想要利用 tootake 不可部分完成的批次作業。  另外，在單一查詢中，查詢單一資料分割中的資料會比查詢跨資料分割中的資料還要有效率。
* 用戶端應用程式不會插入/更新或查詢的 hello 應該位於相同的邏輯單元的工作 （單一查詢或批次更新） 中的資料的不同磁碟分割。  一個重要的原因是沒有 toohello 數目限制在單一資料表中，資料分割索引鍵以便有數百萬個資料分割索引鍵不是問題，並不會影響效能。  比方說，如果您的應用程式具有使用者登入受歡迎的網站，做為 hello 資料分割索引鍵使用 hello 使用者識別碼可能是不錯的選擇。  

#### <a name="hot-partitions"></a>常用資料分割
熱資料分割是接收不當比例的百分比表示的 hello 流量 tooan 帳戶，且不能負載平衡因為它是單一磁碟分割。  一般來說，可以用下列兩種方法其中之一來建立常用資料分割：  

##### <a name="subheading28"></a>只開頭附加和只結尾附加模式
hello 「 僅附加 」 模式是其中所有 （或幾乎全部） 的 hello 流量 tooa 指定 PK 增加和減少相應 toohello 目前的時間。  例如，如果您的應用程式使用 hello 目前日期做為記錄資料的資料分割索引鍵。  這會導致所有 hello 移 toohello 在資料表中，最後一個資料分割的插入和 hello 系統無法載入平衡，因為所有的 hello 寫入都是您的資料表進行 toohello 結尾。  如果 hello 流量 toothat 資料分割的磁碟區超過 hello 資料分割層級的延展性目標，然後它會導致節流。  它是 toomultiple 資料分割，則會傳送流量的更佳 tooensure tooenable 負載平衡 hello 會透過您的資料表要求。  

##### <a name="subheading29"></a>高流量資料
如果您單一資料分割中的資料分割配置結果，只具有遠比其他分割區使用的資料，也可能會看到節流該資料分割接近 hello 的單一資料分割的延展性目標。  確定您沒有單一的資料分割配置結果分割區接近 hello 延展性目標的更佳 toomake 它。  

#### <a name="querying"></a>查詢
本章節描述經過證實的作法，來查詢 hello 表格服務。  

##### <a name="subheading30"></a>查詢範圍
有數種方式 toospecify hello 實體 tooquery 的範圍。  hello 以下是每個 hello 使用的討論。  

一般情況下，以免掃描 （查詢大於單一實體），但如果必須掃描 tooorganize 您的資料，讓您掃描擷取 hello 資料，您需要不含掃描，或傳回大量不需要的實體。  

###### <a name="point-queries"></a>點查詢
點查詢只會擷取一個實體。 它會藉由指定 hello 資料分割索引鍵和 hello 實體 tooretrieve 資料列索引鍵。 這些查詢非常有效率，您應盡可能地加以使用。  

###### <a name="partition-queries"></a>資料分割查詢
資料分割查詢是指可擷取一組共用常見分割索引鍵之資料的查詢。 一般而言，hello 查詢加法 tooa 資料分割索引鍵中指定的資料列索引鍵值的範圍或某些實體屬性的值範圍。 這些查詢會比點查詢沒有效率，且應謹慎使用。  

###### <a name="table-queries"></a>資料表查詢
資料表查詢是指可擷取一組不共用常見分割索引鍵之實體的查詢。 這些查詢非常沒有效率，您應盡量避免使用。  

##### <a name="subheading31"></a>查詢密度
在查詢效率的另一個關鍵因素是 hello 數字，傳回做為比較的 toohello 數掃描的 toofind hello 傳回設定實體的實體。 如果您的應用程式執行資料表查詢與屬性值的篩選，僅有 1%的 hello 資料共用，hello 查詢會掃描 100 個實體，它會傳回每一個實體。 hello 資料表延展性目標討論先前所有 toohello 實體數目的掃描，和方面不 hello 傳回的實體數目： 低查詢密度，很容易造成 hello 資料表服務 toothrottle 您的應用程式因為必須掃描這麼多您所需實體 tooretrieve hello 實體。  請參閱下一節 hello 上[非正規化](#subheading34)如需有關如何 tooavoid 這。  

##### <a name="limiting-hello-amount-of-data-returned"></a>限制 hello 數量的傳回資料
###### <a name="subheading32"></a>篩選
在您知道，查詢會傳回實體，您不需要 hello 用戶端應用程式中，請考慮使用篩選 tooreduce hello 大小為 hello 集傳回。 Hello 實體不會傳回 toohello 用戶端時仍算 hello 延展性限制，會因為 hello 降低網路承載大小改善應用程式效能，並將其 hello 的用戶端應用程式必須處理的實體數目減少.  請參閱上述附註上[查詢密度](#subheading31)，不過 – hello 延展性目標關聯 toohello 實體數目的掃描，以便篩選出許多實體的查詢可能仍然會導致節流，即使傳回幾個實體。  

###### <a name="subheading33"></a>投射
如果用戶端應用程式需要僅提供有限的屬性，從資料表中的 hello 實體，您可以使用傳回的資料集的 hello 投影 toolimit hello 大小。 使用篩選，這有助於 tooreduce 網路負載和用戶端處理。  

##### <a name="subheading34"></a>反正規化
不同於使用關聯式資料庫，hello 經過證實的作法，有效率地查詢資料表的資料會導致 toodenormalizing 您的資料。 也就是複製 hello 中多個實體有相同的資料 (其中每個索引鍵中，您可以使用 toofind hello 資料) 實體的查詢必須掃描 toofind hello 資料 hello 用戶端需求，而不是需要大量實體 toofind tooscan toominimize hello 數目您的應用程式必須 hello 資料。  例如，電子商務網站中，您可能想 toofind 依排序的這兩個 hello 客戶 ID （給我此客戶的訂單） 和依 hello 日期 （給我訂單日期）。  在資料表儲存體，它是最佳的 toostore hello 實體 （或參考 tooit） 兩次-一次使用客戶識別碼，一次 toofacilitate 尋找 hello 日期的資料表名稱、 PK 和 RK toofacilitate 尋找。  

#### <a name="insertupdatedelete"></a>插入/更新/刪除
本章節描述經過證實的作法，修改儲存在 hello 表格服務中的實體。  

##### <a name="subheading35"></a>批次處理
批次交易已知為實體群組交易 (ETG) 在 Azure 儲存體。ETG 內的所有 hello 作業都必須在單一資料表中的單一資料分割上。 請盡可能使用 ETGs tooperform 插入、 更新和刪除批次中。 這可以降低用戶端應用程式 toohello 伺服器 hello 的往返次數、 可減少 hello 數目的可計費的交易 （ETG 會計算為計費的單一交易，而且只能包含 too100 儲存體作業），以及啟用 不可部分完成更新 （所有作業成功或失敗 ETG 內所有）。 具有高延遲的環境 (例如行動裝置) 將會因為使用 ETG 而獲得極大的好處。  

##### <a name="subheading36"></a>Upsert
您應盡可能地使用資料表 **Upsert** 作業。 **Upsert** 有兩種類型，這兩種類型都會比傳統的 **Insert** 和 **Update** 作業還要有效率：  

* **InsertOrMerge**： 當您想 tooupload hello 實體屬性的子集時，請使用此但不確定是否 hello 實體已經存在。 如果 hello 實體存在，此呼叫更新 hello 屬性包含在 hello **Upsert**作業，而且不會保留所有現有的屬性，如果 hello 實體不存在，它會插入 hello 新實體。 這是在查詢中，類似 toousing 投影，您只需要 tooupload hello 屬性會變更的。
* **InsertOrReplace**： 當您想要 tooupload 全新的實體，但您不確定是否已經存在時使用它。 您應該只使用這在您知道該 hello 新上傳實體是完全正確，因為它完全覆寫 hello 舊實體。 例如，您想儲存使用者的目前位置，不論 hello 應用程式之前已儲存 hello 使用者; 位置資料的 tooupdate hello 實體hello 新位置的實體已完成，且您不需要從先前的任何實體的任何資訊。

##### <a name="subheading37"></a>在單一實體中儲存資料序列
某些情況下，應用程式所儲存的它經常需要 tooretrieve 一次的資料數列： 例如，應用程式可能會追蹤 CPU 使用量一段時間順序 tooplot 輪流 hello 資料的圖表中從 hello 過去 24 小時。 其中一個方法是每小時，與每個實體代表特定的時間和儲存該小時內的 hello CPU 使用量的 toohave 一個資料表實體。 tooplot 這項資料，hello 應用程式必須保存從 hello hello 資料最新的 24 小時 tooretrieve hello 實體。  

或者，您的應用程式時，可以為個別的單一實體屬性的每小時儲存 hello CPU 使用量： tooupdate 每小時依您的應用程式可以使用單一**InsertOrMerge Upsert** hello 呼叫 tooupdate hello 值最新的小時。 tooplot hello 資料，hello 應用程式只需要 tooretrieve 單一實體而不是 24，讓非常有效率的查詢 (請參閱上面討論的上[查詢範圍](#subheading30))。

##### <a name="subheading38"></a>在 Blob 中儲存結構化資料
有時候，結構化資料好像應該要以資料表方式呈現，但實體範圍總是會被一起擷取，並可批次插入。  記錄檔是這個狀況的良好範例。  在此案例中，您可以批次處理數分鐘的記錄，然後也總是一次擷取數分鐘的記錄。  在此情況下，效能，對於較佳的 toouse blob，而不是資料表，因為您可以大幅減少 hello 數目寫入/傳回物件，以及通常 hello 需要提出的要求數目。  

## <a name="queues"></a>佇列
在加法 toohello 證實的作法[所有服務](#allservices)先前所述，證明作法 hello 下列套用特別 toohello 佇列服務。  

### <a name="subheading39"></a>延展性限制
單一佇列每秒可以處理大約 2000 則訊息 (每則訊息 1 KB) (每個 AddMessage、GetMessage 和 DeleteMessage 在此算一則訊息)。 如果這是不足以執行您的應用程式，您應該使用多個佇列，並分散到它們的 hello 訊息。  

在 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md)上檢視目前的延展性目標。  

### <a name="subheading40"></a>關閉 Nagle
請參閱 hello 一節討論 hello Nagle 演算法的資料表設定 — hello Nagle 演算法通常不正確的佇列要求 hello 效能，而且您應該停用。  

### <a name="subheading41"></a>訊息大小
佇列效能和延展性會隨著訊息大小增加而減少。 您應該將只 hello 資訊 hello 收件者需要在訊息中。  

### <a name="subheading42"></a>批次擷取
您可以擷取 too32 從單一作業中佇列的訊息。 這可以減少往返數目 hello hello 用戶端應用程式，這特別適用於環境中，行動裝置，例如從，含高延遲。  

### <a name="subheading43"></a>佇列輪詢間隔
大部分的應用程式輪詢訊息從佇列中，可以是其中一種 hello 交易，該應用程式的最大的來源。 請明智地選取輪詢間隔： 輪詢頻率太高可能會導致應用程式 tooapproach hello hello 佇列的延展性目標。 不過，200,000 交易 $0.01 （在 hello 撰寫時），在單一處理器輪詢之後每個月份的第二個成本小於 15 分因此成本, 不通常會影響您所選擇的輪詢間隔的因素。  

如需最新成本資訊，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/storage/)。  

### <a name="subheading44"></a>UpdateMessage
您可以使用**UpdateMessage** tooincrease hello 過了隱藏逾時或 tooupdate 狀態資訊的訊息。 雖然這是功能強大，請記住，每個**UpdateMessage**作業會計入 hello 延展性目標。 但是，這可能會更有效率的方式，比起作業中傳遞一個佇列 toohello 接下來，hello 工作的每個步驟完成時，工作流程。 使用 hello **UpdateMessage**作業可讓您的應用程式 toosave hello 的作業狀態 toohello 訊息，然後繼續進行工作，而非重新佇列 hello 訊息，如 hello hello 作業每次在步驟完成下一個步驟。  

如需詳細資訊，請參閱 hello 文章[如何： 變更佇列的訊息內容 hello](../queues/storage-dotnet-how-to-use-queues.md#change-the-contents-of-a-queued-message)。  

### <a name="subheading45"></a>應用程式架構
您應該使用佇列 toomake 可擴充您應用程式架構。 hello 下列列出一些您可以使用佇列 toomake 更具擴充性應用程式：  

* 您可以處理所使用的工作佇列 toocreate 待辦項目，且平滑應用程式中的工作負載。 例如，您無法排入佇列要求使用者 tooperform 處理器密集的工作例如調整大小上傳映像。
* 您可以使用應用程式的佇列 toodecouple 部分，讓您獨立擴充。 例如，Web 前端可以將使用者的調查結果放到佇列中，以供日後分析與儲存。 您可以加入多個背景工作角色執行個體 tooprocess hello 佇列所需的資料。  

## <a name="conclusion"></a>結論
本文會討論一些最常見的 hello 證明最佳化效能，當使用 Azure 儲存體的作法。 我們鼓勵每個應用程式開發人員 tooassess 他們的應用程式，針對每個 hello 上述作法，請考慮在其應用程式使用 Azure 儲存體的 hello 建議 tooget 絕佳效能上運作。
