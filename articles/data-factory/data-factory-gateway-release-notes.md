---
title: "資料管理閘道器 aaaRelease 資訊 |Microsoft 文件"
description: "資料管理閘道 tory 版本資訊"
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a>資料管理閘道的版本資訊
Hello 現代資料整合的挑戰之一就是從內部部署 toocloud toomove 資料 tooand。 Data Factory 可讓這項整合與資料管理閘道器，這是代理程式，您可以安裝在內部部署 tooenable 混合資料移動。

請參閱下列文章中的資料管理閘道器的詳細資訊的 hello 和如何 toouse 它：

*  [資料管理閘道](data-factory-data-management-gateway.md)
*  [在內部部署和雲端之間使用 Azure Data Factory 移動資料](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a>目前版本 (2.10.6347.7)

### <a name="enhancements-"></a>增強功能
- 您可以新增 DNS 項目 toowhitelist 服務匯流排，而不是允許清單所有 Azure IP 位址從您的防火牆 （如果需要）。 您可以在 Azure 入口網站上找到各自的 DNS 項目 (Data Factory-> [製作和部署] -> [閘道] -> [serviceUrls] \(在 JSON 中)
- HDFS 連接器現在支援自我簽署的公開憑證，方法是讓您略過 SSL 驗證。
- 已修正︰ 閘道離線 （因為 tooclock 誤差） 更新期間的問題



## <a name="earlier-versions"></a>較早的版本

## <a name="2963132"></a>2.9.6313.2
### <a name="enhancements-"></a>增強功能
-   您可以新增 DNS 項目 toowhitelist 服務匯流排，而不是允許清單所有 Azure IP 位址從您的防火牆 （如果需要）。 以下提供更多詳細資料。
-   您現在可以複製從向上 too4.75 TB，這是區塊 blob 支援 hello 最大大小的單一區塊 blob 的資料。 (之前的上限為 195 GB)。
-   已修正：在進行複製活動期間將數個較小檔案解壓縮時發生的憶體不足問題。
-   已修正︰ 索引超出範圍問題從 文件 DB tooan 複製時發生內部部署 SQL Server 具有等冪性功能。
-   已修正：來自「複製精靈」的 SQL Server 清除指令碼無法在內部部署 SQL 上運作。
-   已修正︰ 在 hello 結尾空格的資料行名稱不適用於複製活動。

## <a name="28662833"></a>2.8.66283.3
### <a name="enhancements-"></a>增強功能
- 已修正：在閘道機器重新啟動時發生遺失認證的問題。
- 已修正：使用備份檔進行閘道還原時發生的註冊問題。


## <a name="2762401"></a>2.7.6240.1
### <a name="enhancements-"></a>增強功能
- 已修正：從作為來源的 Oracle 讀取的十進位 Null 值不正確。

## <a name="2661922"></a>2.6.6192.2
### <a name="whats-new"></a>新功能
- 客戶可以提供關於閘道註冊體驗的意見。
- 支援新的壓縮格式︰ZIP (Deflate)

### <a name="enhancements-"></a>增強功能
- 改善 Oracle 接收、HDFS 來源的效能。
- 針對閘道自動更新、閘道平行處理容量進行錯誤修正。


## <a name="2561641"></a>2.5.6164.1
### <a name="enhancements"></a>增強功能
- 改善且更為穩固閘道註冊體驗-現在您可以在 hello 閘道註冊過程中，讓 hello 註冊體驗更能有效回應追蹤進度狀態。
- 改進的閘道還原程序-您仍然可以復原閘道，即使您沒有安裝此更新後 hello 閘道備份檔案。 這會需要您在入口網站的 tooreset 連結的服務認證。
- 錯誤修正。

## <a name="2461511"></a>2.4.6151.1

### <a name="whats-new"></a>新功能

- 您現在可以在本機上儲存資料來源認證。 hello 認證會加密。 hello 資料來源認證可以復原並使用可以從現有的閘道，所有在內部部署的 hello 匯出的 hello 備份檔案還原。

### <a name="enhancements-"></a>增強功能

- 改良和更強大的閘道註冊體驗。
- 支援在複製精靈中，文字格式的 QuoteChar 組態自動偵測和改善 hello 整體格式化偵測的精確度。

## <a name="2361002"></a>2.3.6100.2

- 複製精靈中支援 firstRowAsHeader 和 SkipLineCount 自動偵測內部部署檔案系統和 HDFS 中是否有文字檔案。
- 增強閘道與服務匯流排之間的網路連線的 hello 的穩定性
- 修正幾個錯誤。


## <a name="2260721"></a>2.2.6072.1

*  設定 HTTP proxy 使用 hello 閘道組態管理員中的 hello 閘道支援。 如果有設定，就會透過 HTTP Proxy 來存取 Azure Blob、「Azure 資料表」、Azure Data Lake 及 DocumentDB。
*  支援的標頭複製資料時，處理 TextFormat tooAzure Blob、 Azure 資料湖存放區，在內部部署檔案系統中，並在內部部署 HDFS。
*  支援的資料複製附加 Blob 和分頁 Blob hello 以及已在支援區塊 Blob。
*  導入了新的閘道狀態**線上 （有限制）**，除了複製精靈 」 的 hello 互動作業支援表示 hello hello 閘道的主要功能運作。
*  增強 hello 強固性的閘道註冊使用註冊金鑰。

## <a name="216040"></a>2.1.6040.

*  DB2 驅動程式現在包含在 hello 閘道安裝套件。 您不需要 tooinstall 它分開。
*  DB2 驅動程式現在支援 z/OS 和 DB2 for 我 (AS / 400) 以及 hello 支援平台已 （Linux、 Unix 和 Windows）。
*  支援使用 Azure Cosmos DB 作為內部部署資料存放區的來源或目的地
*  支援已複製的資料從/toocold/熱 blob 儲存體，以及 hello 支援一般用途儲存體帳戶。
*  可讓您 tooconnect tooon 內部部署 SQL Server 透過閘道與遠端登入權限。  

## <a name="2060131"></a>2.0.6013.1

*  您可以選取 hello 語言/文化特性 toobe 閘道會在手動安裝期間使用。

*  當閘道無法如預期運作時，您可以選擇 toosend 閘道記錄檔的最後七天 tooMicrosoft toofacilitate 疑難排解的 hello 問題。 如果不是閘道已連線 toohello 雲端服務，您可以選擇 toosave 並封存閘道記錄檔。  

*  閘道器組態管理員的使用者介面增強功能：

    *  Hello 首頁 索引標籤上進行閘道狀態更明顯可見。

    *  重新組織並簡化控制項。

    *  您可以將資料複製從儲存體使用 hello[程式碼自由複製預覽工具](data-factory-copy-data-wizard-tutorial.md)。 如需此功能的一般詳細資料，請參閱 [分段複製](data-factory-copy-activity-performance.md#staged-copy) 。
*  您可以使用資料管理閘道器 tooingress 資料直接從內部部署 SQL Server 資料庫到 Azure 機器學習。

*  效能改進

    * 在無程式碼複製預覽工具中，改進對於 SQL Server 檢視結構描述或預覽的效能。

## <a name="11259531"></a>1.12.5953.1

*  錯誤修正

## <a name="11159181"></a>1.11.5918.1

*  Hello 閘道事件記錄檔的大小上限已增加 1 MB too40 mb。

*  如果在閘道自動更新期間必須重新啟動，則會顯示警告對話方塊。 然後或更新版本，您可以選擇 toorestart 權限。

*  如果自動更新失敗，閘道安裝程式最多會重試自動更新 3 次。

*  效能改進

    * 改善無程式碼複製案例中從內部部署伺服器載入大型資料表的效能。

*  錯誤修正

## <a name="11058921"></a>1.10.5892.1

*  效能改進

*  錯誤修正

## <a name="1958652"></a>1.9.5865.2

*  零接觸自動更新功能
*  閘道狀態指示器的新系統匣圖示
*  能力太 「 更新現在 」 從 hello 用戶端
*  能力 tooset 更新排程時間
*  用來開啟/關閉自動更新的 PowerShell 指令碼
*  JSON 格式支援  
*  效能改進
*  錯誤修正

## <a name="1858221"></a>1.8.5822.1

*  改善疑難排解體驗
*  效能改進
*  錯誤修正

### <a name="1757951"></a>1.7.5795.1

*  效能改進
*  錯誤修正

### <a name="1757641"></a>1.7.5764.1

*  效能改進
*  錯誤修正

### <a name="1657351"></a>1.6.5735.1

*  支援內部部署 HDFS 來源/接收器
*  效能改進
*  錯誤修正

### <a name="1656961"></a>1.6.5696.1

*  效能改進
*  錯誤修正

### <a name="1656761"></a>1.6.5676.1

*  在組態管理員上支援診斷工具
*  支援 Azure Data Factory 表格式資料來源的資料表資料行
*  針對 Azure Data Factory 支援 SQL DW
*  針對 Azure Data Factory 支援 BlobSource 和 FileSource 的 Reclusive
*  針對 Azure Data Factory 支援 BlobSink 和 FileSink 中與「二進位複製」相關的 CopyBehavior - MergeFiles、PreserveHierarchy 及 FlattenHierarchy
*  針對 Azure Data Factory 支援複製活動報告進度
*  針對 Azure Data Factory 支援資料來源連線驗證
*  錯誤修正

### <a name="1656721"></a>1.6.5672.1

*  針對 Azure Data Factory 支援 ODBC 資料來源的資料表名稱
*  效能改進
*  錯誤修正

### <a name="1656581"></a>1.6.5658.1

*  針對 Azure Data Factory 支援檔案接收
*  針對 Azure Data Factory 在二進位複製中支援保留階層
*  針對 Azure Data Factory 支援複製活動等冪性
*  錯誤修正

### <a name="1656401"></a>1.6.5640.1

*  針對 Azure Data Factory 另外支援 3 種資料來源 (ODBC、OData、HDFS)
*  針對 Azure Data Factory 在 csv 剖析器中支援引號字元
*  壓縮支援 (BZip2)
*  錯誤修正

### <a name="1556121"></a>1.5.5612.1

*  針對 Azure Data Factory 支援 5 種關聯式資料庫 (MySQL、PostgreSQL、DB2、Teradata 和 Sybase)
*  壓縮支援 (Gzip 和 Deflate)
*  效能改進
*  錯誤修正

### <a name="1455491"></a>1.4.5549.1

*  針對 Azure Data Factory 新增 Oracle 資料來源支援
*  效能改進
*  錯誤修正

### <a name="1454921"></a>1.4.5492.1

*  支援 Microsoft Azure Data Factory 和 Office 365 Power BI 服務的統一二進位檔
*  精簡 hello 組態 UI 和註冊程序
*  Azure Data Factory - 針對 SQL Server 資料來源的 Azure 輸入和輸出支援

### <a name="1253031"></a>1.2.5303.1

*  修正逾時問題 toosupport 更耗時的資料來源連接。

### <a name="1155268"></a>1.1.5526.8

*  在設定期間，必要條件是需要 .NET Framework 4.5.1。

### <a name="1051442"></a>1.0.5144.2

*  沒有任何會影響 Azure Data Factory 案例的變更。
