---
title: "aaaIntro tooMicrosoft Azure |Microsoft 文件"
description: "新 tooMicrosoft Azure 嗎？ Get hello 的基本概觀服務它提供附範例的方式會很有用。"
services: " "
documentationcenter: .net
author: rboucher
manager: carolz
editor: 
ms.assetid: 6f47f711-2208-4c21-8c1d-826a54c05c29
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2015
ms.author: robb
ms.openlocfilehash: 6791506abe813e19ca7b04d78d35cb46352a9028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-microsoft-azure"></a>Microsoft Azure 簡介
Microsoft Azure 是 Microsoft 的 hello 公用雲端的應用程式平台。  這篇文章的 hello 目標是您的基礎了解 Azure 中的 hello 基本概念，即使您不知道的任何項目雲端運算的 toogive。

**如何 tooread 這篇文章**

Azure 會不斷增加所有 hello 時間，因此很容易 tooget 多載。  Hello 基本服務，而這在本文中，會先列出，並前往 tooadditional 服務上的開頭。 這不表示您無法使用只 hello 其他服務本身，但是 hello 基本服務組成 hello 核心 Azure 中執行的應用程式。

**提供意見反應**

您的意見反應非常寶貴。 本文應可提供 Azure 的實際概觀。 如果不存在，請告訴我們在 hello hello 頁面底部的 hello 註解區段中。 在提供詳細資料 toosee 和 tooimprove hello 發行項的方式，您所預期。  

## <a name="hello-components-of-azure"></a>hello Azure 元件
Azure 服務分組類別在 hello 管理入口網站和各種視覺輔助工具，例如 hello[何謂 Azure 資訊圖](https://azure.microsoft.com/documentation/infographics/azure/)。 hello 管理入口網站是您的使用 toomanage 大部分 （但非全部） 服務在 Azure 中。

此發行項將會使用**不同組織**tootalk 有關服務根據類似的函式和 toocall 大一部分的重要子服務。  

![Azure 元件](./media/fundamentals-introduction-to-azure/AzureComponentsIntroNew780.png)   
 圖：Azure 提供可存取網際網路、在 Azure 資料中心執行的應用程式服務。

## <a name="management-portal"></a>管理入口網站
Azure 有 web 介面呼叫 hello[管理入口網站](http://manage.windowsazure.com)，可讓系統管理員 tooaccess 及管理大部分，但不是所有 Azure 功能。  通常，Microsoft 會淘汰舊之前釋放 hello 更新 UI 中的入口網站 beta。 hello，另一個較稱為 hello [「 Azure 預覽入口網站 」](https://portal.azure.com/)。

當這兩個入口網站都在作用中時，通常會有很長的重疊。 雖然這兩個入口網站都會出現核心服務，但不是這兩個入口網站都會提供所有的功能。 較新的服務可能會顯示在 hello 較新入口網站第一次和較舊的服務和功能可能只存在於 hello 舊。  這裡 hello 訊息時，如果您找不到項目在 hello 較舊的入口網站，請檢查 hello 較新版本，反之亦然。

## <a name="compute"></a>計算
Hello 雲端平台沒有最基本的事情之一是執行應用程式。 Hello Azure 計算模型中每個都有它自己的角色 tooplay。

您可以分別使用這些技術，或為您的應用程式結合成視需要的 toocreate hello 右 foundation。 hello 方法，您可以選擇取決於哪些問題您正嘗試 toosolve。

### <a name="azure-virtual-machines"></a>Azure 虛擬機器
![Azure 虛擬機器 ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_VirtualMachinesIntroNew_12345.png)   
*圖： Azure 虛擬機器可讓您完整控制 hello 雲端中的虛擬機器執行個體。*

hello 能力 toocreate，視虛擬機器是否從標準映像或您提供，可以是非常有用。 這種方法 (通常稱為「基礎結構即服務」(IaaS)) 就是 Azure 虛擬機器所提供的方法。 圖 2 顯示的組合，虛擬機器 (VM) 執行以及如何從 VHD toocreate 其中一個。  

toocreate VM，您可以指定哪些 VHD toouse 和 hello VM 的大小。  您再支付 hello 時間 VM 正在執行中的 hello。 您付費的 hello 分鐘以及只它正在執行，仍保持 hello VHD 可用的最小的儲存體費用。 Azure 提供存貨 Vhd （稱為 「 影像 」） 包含從可開機作業系統 toostart 的圖庫。 這些包括 Microsoft 和合作夥伴選項，例如 Windows Server 和 Linux、SQL Server、Oracle 等。 您正在可用 toocreate Vhd 和映像，並上傳您自己。 您甚至可以上傳僅包含資料的 VHD，然後從執行中的 VM 存取這些資料。

只要來自 hello VHD，您可以持續儲存 VM 正在執行時所做的任何變更。 hello 下次您從該 VHD 建立 VM 事項挑選離開的地方。 hello 回 hello 虛擬機器的 Vhd 會儲存在我們談論更新版本的 Azure 儲存體 blob。  這表示您取得您的 Vm 將不會消失到期 toohardware 和磁碟失敗的備援性 tooensure。 它也可能 toocopy hello 變更 VHD 移出 Azure，然後在本機執行。

您的應用程式中執行一或多個虛擬機器，這會根據您如何建立它之前，或決定 toocreate 它從頭現在。

此運算可以許多不同的問題使用的 tooaddress 的非常一般方法 toocloud。

**虛擬機器案例**

1. **開發/測試**-您可能需要使用 toocreate 便宜開發和測試平台，當您完成使用它可以關機。 您也可以建立和執行採用您喜愛語言和程式庫的應用程式。 這些應用程式可以使用任何 hello Azure 所提供的資料管理選項，而且您也可以選擇 SQL Server 或在一個或多個虛擬機器中執行的另一個 DBMS toouse。
2. **移動應用程式 tooAzure (增益 shift)** -「 增益 shift 」 是指 toomoving 您的應用程式很多方式與使用堆高機 toomove 大型物件。  您 「 增益 」 hello VHD 從您的本機資料中心，和 「 shift"它 tooAzure 加並在該處執行。  您通常會有 toodo 一些工作 tooremove 相依的其他系統。 如果有太多的相依性，您可以改用選項 3。  
3. **擴充您的資料中心** - 使用 Azure VM 作為內部部屬資料中心的擴充功能，用來執行 SharePoint 或其他應用程式。 toosupport，很可能 toocreate hello 雲端中的 Windows 網域的 Azure Vm 中執行 Active Directory。 您可以使用 Azure 虛擬網路 （稍後提及） tootie 您區域網路與網路在 Azure 中在一起。

### <a name="web-apps"></a>Web Apps
![Azure Web Apps ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_AzureWebsitesIntroNew_12345.png)   
 *圖： Azure Web 應用程式會執行網站應用程式 hello 定域機組中而不需要 toomanage hello 基礎 web 伺服器。*

Hello 最常見的作業人員進行這項 hello 雲端中的其中一個會執行網站和 web 應用程式。 Azure 虛擬機器允許您為此，但它仍會保留您 hello 負責管理一或多個 Vm 和 hello 基礎作業系統。 雲端服務 Web 角色可以辦得到，但部署與管理他們仍需進行管理工作。  如果您只想網站的其他人負責 hello 為您的系統管理工作嗎？

這正是 Web Apps 所提供的功能。 此計算模型提供了受管理的 web 環境中使用 hello Azure 管理入口網站以及應用程式開發介面。 您可以將現有的網站應用程式移至 Web 應用程式保持不變，或您可以建立一個新直接在 hello 雲端中。 網站開始執行之後，您可以新增或移除執行個體，以動態方式在它們之間依賴 Azure Web Apps tooload 平衡要求。 Azure 應用程式提供的共用的選項，您的網站執行所在虛擬機器與其他網站中，並可讓站台 toorun 它自己的 VM 中的標準選項。 hello 標準選項也可讓您增加 hello （運算能力） 的大小視您的執行個體。

對於開發目的而言，Web Apps 支援 .NET、PHP、Node.js、Java 和 Python 以及可用於關聯式儲存的 SQL Database 和 MySQL (來自 Microsoft 的合作夥伴 ClearDB)。 此外，它還提供了好幾個熱門應用程式 (包括 WordPress、Joomla 和 Drupal) 的內建支援。 hello 目標是 tooprovide 低成本、 可擴充和在 hello 公用雲端中建立網站和 web 應用程式廣泛地有用的平台。

**Web Apps 案例**

Web 應用程式是預定的 toobe 公司、 開發人員及 web 設計機構很有用。 對於公司行號而言，這是一個易於管理、可擴充、高度安全且高度可用的解決方案，很適合用於執行平台服務網站。 當您需要 tooset 網站規模時，它使用 Azure Web 應用程式的最佳 toostart 且繼續執行 tooCloud 服務之後，您需要不是可用的功能。 請參閱 hello 結尾 hello 更多的連結可幫助您 toochoose hello 選項之間的 「 計算 」 一節。

### <a name="cloud-services"></a>雲端服務
![Azure 雲端服務](./media/fundamentals-introduction-to-azure/CloudServicesIntroNew.png)   
*圖： Azure 雲端服務提供一個位置 toorun 具有高擴充性自訂程式碼的平台上做為服務 (PaaS) 環境*

假設您想 toobuild 雲端應用程式可支援許多同時連接的使用者，不需要太多系統管理，且永遠不會中斷。 您可能已建立的軟體廠商，比方說的決定 tooembrace 軟體即服務 (SaaS) 所建置的應用程式 hello 雲端中的其中一個版本。 或者，您可能才剛開始建立一個預計能快速成長的消費者應用程式。 如果您在 Azure 上建置，則應使用哪一個執行模型？

Azure Web Apps 允許建立此種 Web 應用程式，但有一些限制。 例如，您沒有系統管理權限，這表示您無法任意安裝軟體。 Azure 虛擬機器可讓您更多的彈性，包括系統管理存取權，您一定可以使用它 toobuild 極具擴充性的應用程式，而您必須在 toohandle 各種可靠性及管理您自己。 您想要為選項，可讓您 hello 的控制項，您需要但是也會處理大部分的 hello 工作所需的可靠性及管理。

這正是 Azure 雲端服務所提供的。 這項技術非常明確設計可擴充、 可靠且 toosupport 和低-系統管理應用程式中，而且通常所謂平台即服務 (PaaS) 的範例。 toouse，您建立的應用程式使用 hello 技術的選擇，例如 C#、 Java、 PHP、 Python、 Node.js 或其他項目。 然後，程式碼執行中執行的 Windows Server 版本的虛擬機器 （參考的 tooas 執行個體）。

但是，這些 Vm 是不同的 hello 的建立與 Azure 虛擬機器。 一方面，Azure 會自行管理 VM，並執行諸如安裝作業系統修補程式及自動發行修補後的新映像等作業。 這表示您的應用程式不應該維護在 web 或背景工作角色執行個體; 的狀態它應該改為放在 hello hello 下一節中所述的 Azure 資料管理選項之一。 此外，Azure 也會監控這些 VM，並重新啟動任何失敗的 VM。 您可以設定雲端服務 tooautomatically 回應 toodemand 中建立更多或較少的執行個體。 這可讓您增加 toohandle 使用量，然後按一下 小數位數較少的使用量時，不支付盡可能如此。

您有兩個角色 toochoose 從您建立執行個體時，Windows Server 為基礎。 hello hello 兩個之間的主要差異在於 web 角色的執行個體執行 IIS，而沒有背景工作角色執行個體。 同時管理在 hello 相同的方式，不過，和的常見的應用程式 toouse 這兩個。 比方說，web 角色執行個體可能接受來自使用者的要求，然後將其傳遞 tooa 背景工作角色執行個體進行處理。 tooscale 應用程式中的向上或向下，您可以要求 Azure 建立的任何一個角色的多個執行個體，或關閉現有的執行個體。 與類似 tooAzure 虛擬機器，您收費 hello 時間執行每個 web 或背景工作角色執行個體。

**雲端服務案例**

當您需要更多控制權 hello 平台與 Azure Web 應用程式所提供，但不需要對 hello 基礎作業系統的控制，雲端服務會理想 toosupport 大量向外的延展。

#### <a name="choosing-a-compute-model"></a>選擇計算模型
hello 頁面[Azure Web 應用程式、 雲端服務和虛擬機器的比較](app-service-web/choose-web-site-cloud-service-vm.md)提供更詳細的資訊 toochoose 計算模型。

## <a name="data-management"></a>資料管理
應用程式都需要資料，而不同類型的應用程式會需要不同類型的資料。 因為這個緣故，Azure 會提供數個不同的方式 toostore 並管理資料。 Azure 提供許多儲存體選項，但這些選項全都是專為非常堅固耐用的儲存體所設計的。  與任何一種選項，總是會有 3 份資料跨 Azure 資料中心-6，如果您允許 Azure toouse 異地備援 tooback 向上 tooanother 資料中心至少 300 英哩離開保持同步。     

### <a name="in-virtual-machines"></a>在虛擬機器中
hello 能力 toorun SQL Server 或另一個 DBMS VM，建立與 Azure 虛擬機器中的已被提及。 請注意，這個選項不受限制的 toorelational 系統;您也可用 toorun NoSQL 技術，例如 MongoDB 和 Cassandra。 執行您自己的資料庫系統會直接 it 複寫什麼我們自己的資料中心使用 tooin-，但也需要處理該 DBMS hello 管理。  在其他選項，Azure 會處理多個或所有 hello 為您的管理工作。

同樣地，hello hello 虛擬機器狀態，且您建立或上傳任何其他資料磁碟備份 blob 儲存體所支援 （我們稍後討論的）。  

### <a name="azure-sql-database"></a>Azure SQL Database
![Azure 儲存體 SQL Database](./media/fundamentals-introduction-to-azure/StorageAzureSQLDatabaseIntroNew.png)   

*圖： Azure SQL Database 提供 hello 雲端中受管理的關聯式資料庫服務。*

針對關聯式儲存體，Azure 會提供 hello 功能的 SQL 資料庫。 不要讓 hello 命名欺騙您。 這與在 Windows Server 上運作之 SQL Server 所提供的傳統 SQL Database 有所不同。  

之前稱為 SQL Azure，Azure SQL Database 提供所有 hello 關聯式資料庫管理系統，包括不可部分完成的交易同時存取資料時維持資料完整性、 ANSI SQL 查詢，以及熟悉的程式設計的多個使用者的主要功能模型。 如同 SQL Server，可以使用 Entity Framework、ADO.NET、JDBC 和其他熟悉的資料存取技術來存取 SQL Database。 它也支援大部分的 hello T-SQL 語言，以及 SQL Server 工具，例如 SQL Server Management Studio。 對於熟悉 SQL Server (或其他關聯式資料庫) 的使用者而言，使用 SQL Database 比較直接了當。

SQL 資料庫不是只 DBMS 中 hello 雲端 it 的 PaaS 服務。 您仍然會控制您的資料以及誰可以存取它，但是 SQL Database 會負責處理 hello grunt 系統管理工作，例如管理 hello 硬體基礎結構，並會自動保留向上 toodate hello 資料庫和作業系統軟體。 SQL Database 還提供高可用性、自動備份、時間點還原功能，以及可以複寫在不同地理區域上的複本。  

**SQL Database 的案例**

如果您要建立的 Azure 應用程式 （使用任何 hello 計算模型） 需要關聯式儲存體，SQL 資料庫可以是一個不錯的選項。 執行外部 hello 雲端應用程式也可以使用這項服務，因此有許多其他案例。 例如，各種用戶端系統 (包括桌上型電腦、膝上型電腦、平板電腦和手機) 皆可存取儲存在 SQL Database 中的資料。 因為 SQL Database 透過複寫提供內建高可用性，所以使用 SQL Database 有助於讓停機時間減至最少。

### <a name="tables"></a>資料表
![Azure 儲存體資料表](./media/fundamentals-introduction-to-azure/StorageTablesIntroNew.png)  

*圖： Azure 資料表提供一般的 NoSQL 方法 toostore 資料。*

因為此功能屬於稱為「Azure 儲存體」大型功能的一部分，它有時候又會被叫做不同的名稱。 如果您看到 「 資料表 」、 「 Azure 表格 」 或 「 儲存體資料表 」，則所有 hello 相同的動作。  

並不困惑 hello 名稱： 這項技術並不提供關聯式儲存體。 事實上，這是一個稱為索引鍵/值存放區的 NoSQL 方法範例。 Azure 資料表可讓應用程式儲存各種類型的屬性，例如字串、整數和日期。 然後，應用程式可提供該群組的唯一主索引鍵，進而擷取一組屬性。 而複雜的作業不支援聯結，例如資料表提供快速存取 tootyped 資料。 它們也很容易擴充，以單一資料表可以 toohold 不如 tb 的資料。 和比對他們為了簡單起見，資料表通常較不昂貴 toouse 比 SQL Database 的關聯式儲存體。

**資料表的案例**

假設您想要 toocreate Azure 應用程式需要快速存取 tootyped 資料，可能很多，但不需要 tooperform 複雜的 SQL 查詢此資料。 例如，假設您要建立的取用者應用程式的每個使用者需要 toostore 客戶設定檔資訊。 您的應用程式正在 toobe 相當常用，因此您需要 tooallow 大量資料，但您不會與儲存它，超過這個資料擷取簡單的方式。 這是完全 hello 案例，Azure 資料表有意義。

### <a name="blobs"></a>Blob
![Azure 儲存體 Blob](./media/fundamentals-introduction-to-azure/StorageBlobsIntroNew.png)    
*圖：Azure Blob 提供非結構化二進位資料。*  

Azure Blob (一次 「 Blob 儲存體 」 和就 「 儲存體 Blob"都是 hello 相同的動作) 是設計的 toostore 非結構化的二進位資料。 如同資料表，二進位大型物件提供了便宜的儲存體，單一 Blob 可以多達 1TB 的容量。 Azure 應用程式也可以使用 Azure 磁碟機，讓 Blob 得以為 Azure 執行個體中掛接的 Windows 檔案系統提供永續性儲存體。 hello 應用程式看到一般的 Windows 檔案，但 hello 內容實際上儲存在 blob。

Blob 儲存體可用於許多其他 Azure 功能 (包括虛擬機器)，所以它一定也可以處理您的工作負載。

**Blob 的案例**

儲存視訊、大量檔案或其他二進位資訊的應用程式，可以將 Blob 當作簡單、便宜的儲存體。 Blob 也經常與其他服務搭配使用，如內容傳遞網路 (我們將於稍後討論)。  

### <a name="import--export"></a>匯入 / 匯出
![Azure Import Export Service](./media/fundamentals-introduction-to-azure/ImportExportIntroNew.png)  

*圖： Azure 匯入 / 匯出提供 hello 能力 tooship 從 Azure 實體硬碟機 tooor 更快速且成本較低的大量資料匯入或匯出。*  

有時候您會想 toomove 大量資料至 Azure。 這可能會花費很長的時間 (或許要幾天的時間)，並使用許多頻寬。 在這些情況下，您可以使用 Azure 匯入/匯出、 直接 tooAzure 資料中心，其中 Microsoft 將 hello 將資料傳送到 blob 儲存體，讓您 tooship Bitlocker 加密 3.5"SATA 硬碟。  Hello 上傳完成之後，Microsoft 提供了 hello 磁碟機後 tooyou。  您也可以要求大量的 Blob 儲存體中的資料要匯出到硬碟上，並傳送後的 tooyou 透過郵件。

**匯入/匯出的案例**

* **大型資料移轉**-每當您有大量的資料 (Tb)，您想要 tooupload tooAzure hello 匯入/匯出服務通常會更快且可能比傳送嗨透過廉價網際網路。 在 blob 中 hello 資料之後，您可以處理它成為其他表單，例如資料表儲存體或 SQL 資料庫。
* **封存資料復原**-您可以使用匯入/匯出 toohave Microsoft 傳輸大量資料儲存在 Azure Blob 儲存體 tooa 存放裝置傳送，則具有該裝置傳送您想要回復 tooa 位置。 由於這需要一些時間，所以並不適合災難復原。 它比較適合您不需要快速存取的封存資料。

### <a name="file-service"></a>檔案服務
![Azure 檔案服務](./media/fundamentals-introduction-to-azure/FileServiceIntroNew.png)    
*圖： Azure 檔案服務提供的 SMB \\ \\server\share hello 雲端中執行的應用程式的路徑。*

在內部，它是一般 toohave 大量的檔案存放裝置可以存取透過 hello 伺服器訊息區塊 (SMB) 通訊協定使用\\ \\Server\share 格式。 Azure 現在有服務，可讓您 toouse 此通訊協定 hello 雲端中。 在 Azure 中執行的應用程式可以使用熟悉的檔案系統 Api 如 ReadFile 和 WriteFile 的 Vm 之間的 tooshare 檔案使用它。 此外，也可存取 hello 檔案在 hello 透過 REST 介面，可讓您在內部部署的 hello tooaccess 共用也設定虛擬網路時相同的時間。 Azure 檔案之上 hello blob 服務，讓它所繼承 hello 相同可用性、 持續性、 延展性及內建於 Azure 儲存體異地備援。

**Azure 檔案的案例**

* **移轉現有的應用程式 toohello 雲端**-其更容易 toomigrate 在內部部署應用程式 toohello 雲端使用檔案的檔案就會共用 tooshare hello 應用程式的各部分之間的資料。 每個 VM 會連線 toohello 檔案共用，然後可讀取並寫入檔案，就像它會根據內部檔案共用。
* **共用應用程式設定**-分散式應用程式的常見模式為 toohave 在集中位置，從許多不同的虛擬機器可存取的組態檔。 這些組態檔可以儲存在 Azure 檔案共用中，並由所有應用程式執行個體進行存取。 hello 設定也可以透過 hello REST 介面，可讓世界各地存取 toohello 組態檔來管理。
* **診斷共用** - 您可以儲存並共用診斷檔案，如記錄、度量及損毀傾印。 擁有這些檔案可透過 SMB 的 hello 和 REST 介面可讓應用程式 toouse 各種不同的分析工具，以處理及分析 hello 診斷資料。
* **開發/測試/Debug** -當開發人員或系統管理員使用 hello 雲端中虛擬機器上他們通常需要一組工具或公用程式。 在每台虛擬機器上安裝與散佈這些公用程式相當費時。 Azure 檔案時，開發人員或系統管理員可以在檔案共用上儲存最愛的工具，並從任何虛擬機器連線 toothem。

## <a name="networking"></a>網路
Azure 會立即執行分散 hello 世界各地的許多資料中心。 當您執行的應用程式，或儲存資料時，您可以選取一或多個這些資料中心 toouse。 您也可以連接 toothese 資料中心，以各種方式使用 hello 服務下方。

### <a name="virtual-network"></a>虛擬網路
![VirtualNetwork](./media/fundamentals-introduction-to-azure/VirtualNetworkIntroNew.png)   

*圖： 虛擬網路提供 hello 雲端中的私人網路讓不同的服務可以彼此通訊 tooeach，或 tooon 內部部署資源如果您設定 VPN 的跨單位連線。*  

一個實用的方式 toouse 公用雲端是 tootreat 它自己的資料中心的延伸。

因為您可依照需求建立 VM，然後在不再需要這些 VM 時移除 (並停止付費)，而僅只在有需要時擁有運算能力。 以及 Azure 虛擬機器可讓您建立 Vm 執行 SharePoint、 Active Directory 和其他熟悉的內部部署軟體，因為這種方法可以使用您已經有的 hello 應用程式。

toomake 這非常有用，不過，您的使用者應該 toobe 無法 tootreat 這些應用程式在您自己的資料中心內執行一樣。 這正是 Azure 虛擬網路所容許的。 使用的 VPN 閘道裝置，系統管理員可以設定虛擬私人網路 (VPN) 您的區域網路與您在 Azure 中部署的 tooa 虛擬網路的 Vm 之間。 因為您指派自己 IP v4 位址 toohello 雲端的 Vm，它們會出現 toobe 自己網路上。 您的組織中的使用者可以存取這些 Vm hello 應用程式包含如同他們在本機執行一樣。

如需規劃與建立適合您的虛擬網路詳細資訊，請參閱 [虛擬網路](virtual-network/virtual-networks-overview.md)。

### <a name="express-route"></a>ExpressRoute
![ExpressRoute](./media/fundamentals-introduction-to-azure/ExpressRouteIntroNew.png)   

*圖： ExpressRoute 使用 Azure 虛擬網路，但透過將連接路由傳送速度專用線路，而不是 hello 公用網際網路。*  

如果您需要比 Azure 虛擬網路連線可提供還要高的頻寬或安全性，您可以考慮 ExpressRoute。 在某些情況下，ExpressRoute 還可為您節省開支。 您仍需在 Azure 中，虛擬網路但 hello Azure 與您的站台之間的連結使用專用的連接，不會通過 hello 公用網際網路。 在排序 toouse 這項服務，您將需要 toohave 協議與網路服務提供者或交換服務提供者。

設定 ExpressRoute 連線需要更多時間，並計劃，所以您可能會想 toostart 使用站對站 VPN 時，然後移轉 tooan ExpressRoute 連線。

如需 ExpressRoute 的詳細資訊，請參閱 [ExpressRoute 技術概觀](expressroute/expressroute-introduction.md)。

### <a name="traffic-manager"></a>流量管理員
![TrafficManager](./media/fundamentals-introduction-to-azure/TrafficManagerIntroNew.png)   

*圖： Azure Traffic Manager 可讓您 tooroute 全域流量 tooyour 服務根據智慧型規則。*

如果多個資料中心中執行 Azure 應用程式，您可以橫跨 hello 應用程式的執行個體以聰明的方式使用 Azure Traffic Manager tooroute 使用者要求。 您也可以路由傳送流量不在 Azure 中執行，只要進行存取的 tooservices hello 網際網路。  

Azure 與使用者，只要單一組件中的 hello world 應用程式可能只有一個 Azure 資料中心內執行。 使用者的應用程式周圍 hello world，不過散佈，是在多個資料中心，更 toorun 可能甚至全部都。 在此第二個情況下，您所面對的問題： 如何執行您以智慧方式指示使用者 tooapplication 執行個體？ 大部分的 hello 時間，您可能想每個使用者 tooaccess hello 資料中心最接近 tooher，因為它可能會提供其 hello 最佳回應時間。 但如果 hello 應用程式的執行個體已多載或無法使用？ 在此情況下，它會自動成為 nice toodirect 她要求 tooanother 資料中心。 這正是 Azure 流量管理員的功用。

hello 擁有者的應用程式定義的規則，指定使用者的要求如何導向的 toodatacenters，則依賴 Traffic Manager toocarry 出這些規則。 比方說，使用者可能通常會導向的 toohello 最接近的 Azure 資料中心，但從其預設的資料中心的 hello 回應時間超過 hello 回應時間，從其他資料中心時傳送 tooanother 其中一個。 有許多使用者的全域分散式應用程式，這類的內建的服務 toohandle 問題是很有用。

Traffic manager 會使用目錄名稱服務 (DNS) tooroute 使用者 tooservice 端點，但是進一步流量不會繼續透過 Traffic Manager 會建立該連接。 這會防止流量管理員變成瓶頸，而導致您的服務通訊變慢。

## <a name="developer-services"></a>開發人員服務
Azure 提供許多工具 toohelp 開發人員和 IT 專業人員建立及維護 hello 雲端中的應用程式。  

### <a name="azure-sdk"></a>Azure SDK
在 2008 中，回 hello 第一次的發行前版本的 Azure 支援只有.NET 開發。 不過，您現在可以用很多種語言建立 Azure 應用程式。 Microsoft 目前提供 .NET、Java、PHP、Node.js、Ruby 和 Python 語言特有的 SDK。 此外，還有一般 Azure SDK 可提供任何語言 (如 C++) 的基本支援。  

這些 SDK 可協助您建置、部署及管理 Azure 應用程式。 從 [www.microsoftazure.com](https://azure.microsoft.com/downloads/) 或 GitHub 即可取得 SDK，並可搭配 Visual Studio 和 Eclipse 使用。 Azure 還提供開發人員可以使用任何編輯器或開發環境中，包括部署應用程式從 Linux 和 Macintosh 系統的 tooAzure 工具的命令列工具。

除了協助您建置 Azure 應用程式，這些 SDK 還提供了用戶端程式庫，協助您建立使用 Azure 服務的軟體。 比方說，您可能會建置應用程式可讀取和寫入 Azure blob，或建立部署 Azure 應用程式透過 hello Azure 的管理介面的工具。

### <a name="visual-studio-team-services"></a>Visual Studio Team Services
Visual Studio Team Services 是涵蓋數字的服務，協助 toodevelop hello Azure 中的應用程式的行銷名稱。

tooavoid 混淆-它不提供裝載或以 Web 為基礎的版本的 Visual Studio。 您仍然需要本機執行的 Visual Studio 版本。 但它提供了許多其他非常有用的工具。

它並不包含稱為 Team Foundation Service 的託管來源控制系統，該系統提供了版本控制和工作項目追蹤等功能。  如果您偏好使用 Git 進行版本控制，您也可以做得到。 而且您可以區分 hello 您專案所使用的原始檔控制系統。 您可以無限制的私用 team 專案存取從任何位置中建立 hello world。  

Visual Studio Team Services 提供負載測試服務。 您可以執行在 hello 雲端中的 Vm 上的 Visual Studio 中建立的負載測試。 您指定 hello 使用者總人數之想 tooload 測試，和 Visual Studio Team Services 自動將判斷需要多少的代理程式時，加速所需的 hello 虛擬機器和執行負載測試。 如果您是 MSDN 訂閱者，您每個月將會獲得數以千計的免費負載測試使用者分鐘數。

Visual Studio Team Services 亦可支援具備如連續整合組建、工作流程看板和虛擬小組室等功能的便捷開發。

**Visual Studio Team Services Scenarios**

Visual Studio Team Services 是個不錯的選擇需要 toocollaborate 全球和 hello 基礎結構中沒有位置 toodo 因此公司。 您可以在數分鐘內完成設定、選擇來源控制系統，並於當天開始撰寫程式碼及組建。  hello 小組工具提供位置，以便協調並共同作業和 hello 其他工具提供 hello 分析所需 tootest 快速調整應用程式。

但已在內部部署系統的組織可以測試 Visual Studio Team Services toosee 中的新專案會更有效率。   

### <a name="application-insights"></a>Application Insights
![Application Insights](./media/fundamentals-introduction-to-azure/ApplicationInsights.png)  

*圖：Application Insights 可監視即時 Web 或裝置應用程式的效能和使用情形。*

當您已發佈您的應用程式 - 無論是在行動裝置、桌上型電腦或 web 瀏覽器上執行 - Application Insights 都會告訴您執行方式和使用者如何使用它。 它會保留的計數為損毀和回應緩慢，提醒您如果 hello 圖表跨無法接受的臨界值，並協助您診斷任何問題。

當您開發的新功能時，計劃 toomeasure 它與使用者的成功與否。 藉由分析使用模式，您將了解什麼最適合客戶，並在每個開發週期中加強您的應用程式。

雖然它裝載在 Azure 中，Application Insights 仍適用於廣泛且日漸成長的應用程式範圍，無論是否在 Azure 中皆然。 J2EE 和 ASP.NET web 應用程式，以及 iOS、Android、OSX 和 Windows 應用程式皆涵蓋在內。 遙測寄 hello 應用程式，以建置 SDK toobe 分析，並顯示 hello 在 Azure 中的 Application Insights 服務。

如果您想更具特製化的分析，將匯出 hello 遙測資料流 tooa 資料庫或 tooPower BI 或任何其他工具。

**Application Insights 案例**

您正在開發應用程式。 它可能是 web 應用程式、裝置應用程式或具備 web 後端的裝置應用程式。

* 微調 hello 效能的應用程式之後發行，或在時負載測試。  Application Insights 遙測彙總所有 hello 安裝執行個體，和您呈現的圖表的回應時間、 要求和例外狀況計數、 相依性回應時間和其他效能指標。 這些內容可協助您微調應用程式的效能。 您可以插入程式碼 tooreport 更特定的資料，如果您需要它。
* 偵測及診斷即時應用程式中的問題。 如果效能指標超越可接受的臨界值，您可以透過電子郵件取得警示。 您可以調查特定使用者工作階段，例如 toosee hello 之要求造成的例外狀況。
* 追蹤每個新功能的使用方式 tooassess hello 的成功。 當您設計新的使用者劇本時，規劃 toomeasure 多少使用，以及使用者是否達到預期的目標。 Application Insights 可讓您的網頁檢視等基本使用量資料，您可以更詳細地插入程式碼 tootrack hello 使用者經驗。

### <a name="automation"></a>自動化
沒有人喜歡 toowaste 時間進行 hello 一再重複處理相同的手冊。 提供一項 azure 自動化您 toocreate，如監視、 管理和部署 Azure 環境中的資源。  

Automation hello 幕後使用"的 runbook"，它會使用 Windows PowerShell 工作流程 （相對於就像一般 PowerShell)。 Runbook 的用意在於 toobe 執行而不需使用者互動。 PowerShell 工作流程可讓在沿著 hello 的檢查點儲存指令碼 toobe hello 狀態的方式。 如果發生失敗，就不需要 toostart 從 hello 開頭的指令碼。 您可以在 hello 最後一個檢查點重新啟動它程式。 這樣一來節省大量的工作，每個可能的失敗嘗試 toomake hello 指令碼的控制代碼。

**自動化案例**

Azure 自動化是不錯的選擇 tooautomate hello 手動、 長時間執行、 易發生錯誤及重複性在 Azure 中。

### <a name="api-management"></a>API 管理
建立及發行應用程式的程式設計介面 (Api) 在 hello 上網際網路時常見的方式 tooprovide 服務 tooapplications。 如果這些服務的 resellable （例如，天氣資料），組織可以讓其他第三方 tooaccess 相同服務的費用。 當您擴充 toomore 夥伴時，通常會需要 toooptimize 和控制存取。  有些合作夥伴甚至可能需要不同格式的 hello 資料。

Azure API 管理方便組織 toopublish Api toopartners、 員工及協力廠商開發人員安全且依比例。 它提供不同的應用程式開發介面端點，並且做為 proxy toocall hello 實際的端點，同時提供服務，例如快取、 轉換、 節流、 存取控制和分析彙總。

**API 管理案例**

例如，假設您的公司有一組裝置，全部都需要 toocall 後 tooa 中央服務 tooget 資料--例如，託運公司擁有的裝置 hello 路段圖上的每個卡車中。  當然 hello 公司會希望 tooset 向上系統 tootrack 是自己的卡車讓它確實可以預測和更新的傳遞時間。 它可以因此得知卡車數量並適當地加以規劃。  每個卡車需要回撥 tooa 中央位置與它的定位和速度資料，以及可能有多個裝置。

因此可能會傳送公司的 hello 的客戶也可以從取得此位置的資料。  hello 客戶可以使用它 tooknow 幅度產品會有 tootravel，其中這些困難，支付沿著特定路由 （如果結合這些付費 tooship） 多少它們。 如果傳送公司的 hello 已彙總此資料，許多客戶可能支付費用。  但是然後 hello 傳送公司必須 tooprovide toogive 客戶 hello 資料的方式。 一旦提供存取 toocustomers，它們可能不需要控制 hello 資料查詢的頻率。 這些使用者必須 tooprovide 有關哪些人可以存取哪些資料的規則。 所有這些規則必須 toobe 內建於其外部應用程式開發介面。 這正是為什麼您需要 API 管理的協助。  

## <a name="identity-and-access"></a>身分識別與存取
大多數應用程式都會使用身分識別。 得知使用者的身分，應用程式便可判斷要如何與該使用者互動。 Azure 會提供服務 toohelp 追蹤識別，以及將它整合到您可能已使用的身分識別存放區。

### <a name="active-directory"></a>Active Directory
如同大部分的目錄服務，Azure Active Directory 會儲存使用者和其所屬的 hello 組織的相關資訊。 它可讓使用者登入，然後提供語彙基元呈現這些 tooapplications tooprove 其身分識別。 此外，還能夠同步處理使用者資訊與在本機網路中內部部署上執行的 Windows Server Active Directory。 雖然 hello 機制和 Azure Active Directory 使用的資料格式不是與 Windows Server Active Directory 中所使用的相同，它會執行的 hello 函式會有相當類似。

它的重要 toounderstand，Azure Active Directory 的設計主要是使用雲端應用程式。 例如，在 Azure 或其他雲端平台上執行的應用程式均可使用。 此外，Microsoft 擁有的雲端應用程式 (如 Office 365 應用程式) 也可使用。 如果您想 tooextend 您的資料中心到 hello 雲端中使用 Azure 虛擬機器和 Azure 虛擬網路，不過，Azure Active Directory 無法 hello 正確的選擇。 相反地，您會想 toorun Windows Server Active Directory 中的虛擬機器。

toolet 應用程式存取其所含的 hello 資訊、 Azure Active Directory 提供稱為 「 Azure Active Directory Graph RESTful API。 此 API 可讓您在任何平台存取目錄物件和 hello 它們之間的關聯性上執行的應用程式。  例如，授權的應用程式可能會使用此 API toolearn，關於使用者、 hello 他屬於的群組，以及其他資訊。 應用程式也可以查看其使用者的身分證圖形讓它們更有效地使用人員之間的 hello 連接之間的關聯性。

此服務，Azure Active Directory 存取控制，另一個功能簡化了應用程式 tooaccept 識別資訊從 Facebook、 Google、 Windows Live ID 和其他常見的身分識別提供者。 不需要 hello 應用程式 toounderstand hello 不同資料格式和每個這些提供者所使用的通訊協定，存取控制轉譯為所有的單一通用格式。 此外，還可讓應用程式接受從一或多個 Active Directory 網域的登入。 比方說，廠商提供 SaaS 應用程式可能會在每個其客戶的單一登入 toohello 應用程式中使用 Azure Active Directory 存取控制 toogive 使用者。

目錄服務是內部部署運算的核心支柱。 不應該是意外，它們也很重要 hello 雲端中。

### <a name="multi-factor-authentication"></a>Multi-Factor Authentication
![Azure Multi-Factor Authentication](./media/fundamentals-introduction-to-azure/MFAIntroNew.png)   

*圖： Multi-Factor Authentication 提供 hello 功能的應用程式 tooverify 多種形式的識別*

安全性總是很重要。 多因素驗證 (MFA) 可協助確保只有使用者本身可存取他們的帳戶。 MFA (又稱為雙因素驗證或 "2FA") 要求使用者提供使用者登入和交易的三種身分識別驗證方法中的其中兩種。

* 您知道的某些資訊 (通常是密碼)
* 您擁有的某些東西 (不容易輕易複製的信任裝置，例如電話)
* 您身上的某些特徵 (生物識別技術)

因此當使用者登入時，您可以要求它們 tooalso 確認其身分識別與行動裝置應用程式、 電話或簡訊，搭配其密碼。 根據預設，Azure Active Directory 支援 hello 使用密碼作為其唯一的驗證方法的使用者登入。您可以使用 MFA 與 Azure AD 或自訂應用程式和目錄中的，使用 hello MFA SDK。 您也可以將它與內部部署應用程式搭配使用，方法是使用 Multi-Factor Authentication Server。

**MFA 案例**

敏感帳戶 (例如銀行登入) 和原始程式碼存取 (未經授權的存取可能會有高財務成本或智慧財產權成本) 的登入防護。   

## <a name="mobile"></a>行動
如果您要建立的行動裝置應用程式，Azure 可以協助 hello 雲端中儲存資料、 驗證使用者，並不需要您 toowrite 更多的自訂程式碼傳送推播通知。

當然，您可以建立行動應用程式使用虛擬機器、 雲端服務或 Web 應用程式的 hello 後端，而您可以花更少時間寫入 hello 基礎服務元件會使用 Azure 的服務。

### <a name="mobile-apps"></a>Mobile Apps
![Mobile Apps](./media/fundamentals-introduction-to-azure/MobileServicesIntroNew.png)

*圖：Mobile Apps 為應用程式提供與行動裝置通訊時經常需要用到的功能。*

Azure Mobile Apps 提供許多有用的功能，可讓您減少花費在建置行動裝置應用程式後端的時間。 它可讓您 toodo 簡單佈建和管理 SQL Database 中儲存的資料。 利用伺服器端程式碼，即可輕鬆地使用其他資料儲存選項，如 Blob 儲存體或 MongoDB。 Mobile Apps 提供通知支援，但在某些情況下，您可以改為使用「通知中樞」(如後續所述)。  hello 服務也有 REST API 行動應用程式可以呼叫 tooget 完成的工作。 行動應用程式也會提供 hello 能力 tooauthenticate 使用者透過 Microsoft 和 Active Directory 及其他已知的身分識別提供者，例如 Facebook、 Twitter 和 Google。   

您可以使用其他 Azure 服務，例如服務匯流排和背景工作角色，並連接 tooon 內部部署系統。 您甚至可以使用第 3 個合作對象附加元件，從 hello Azure 市集 （例如電子郵件的 SendGrid) tooprovide 額外的功能。

原生用戶端程式庫，進行 Android、 iOS、 HTML/JavaScript、 Windows Phone 和 Windows 市集使其更容易 toodevelop 應用程式在所有主要行動平台上。 REST API 可讓 toouse 行動服務資料和應用程式在不同的平台上驗證功能。 單一行動服務可支援多個用戶端應用程式，所以您可在各種裝置上提供一致的使用者經驗。

因為 Azure 已經支援大規模，您可以處理 hello 流量，當您的應用程式變得更普遍。  支援監視和記錄 toohelp 疑難排解問題，以及管理效能。

### <a name="notification-hubs"></a>通知中樞
![NotificationHubs](./media/fundamentals-introduction-to-azure/NotificationHubsIntroNew.png)  

*圖：「通知中樞」為應用程式提供與行動裝置通訊時經常需要用到的功能。*

雖然您可以在 Azure 行動應用程式中撰寫程式碼 toodo 通知，通知中心會是最佳化的 toobroadcast 數以百萬計的高度個人化的推播通知分鐘內。  您不需要 tooworry 相關詳細資料，例如行動電信業者或裝置製造商。 您可以透過單一 API 呼叫，即可鎖定個人或數百萬位使用者。

通知中心是設計的 toowork 與任何後端。 您可以使用 Azure 行動應用程式、 自訂的後端中任何提供者上執行的 hello 雲端或內部部署後端。

**通知中樞案例**如果您已撰寫行動遊戲玩家所花費的開啟位置，您可能需要 toonotify 玩家 2 的玩家 1 完成其開啟。 如果您只需要 toodo，您就可以使用行動應用程式。 但如果您有 100,000 名使用者播放您的遊戲且想 toosend 機密免費提供 tooeveryone，通知中心 hello 更好的選擇的時間。

您可以傳送重大消息，低延遲的運動事件，以及產品公告通知 toomillions 的使用者。 因此，員工不需要檢查電子郵件或其他通知的應用程式 toostay tooconstantly，企業可以通知通訊的相關新時間機密，例如業務潛在客戶、 員工。 您也可以傳送多因素驗證所需的一次性密碼。

## <a name="back-up"></a>備份
每個企業需要 toobackup 和還原資料。 您可以使用 Azure toobackup 並還原您的應用程式是否在 hello 雲端或內部部署。 Azure 提供不同的選項 toohelp 根據備份 hello 類型而定。

### <a name="site-recovery"></a>站台復原
Azure Site Recovery （先前稱為 HYPER-V 復原管理員） 可協助您保護重要的應用程式在站台之間協調 hello 複寫和復原。 站台復原提供根據 hyper-v、 VMWare 或 SAN tooyour 自己次要站台、 tooa 主機服務提供者站台或 tooAzure 功能 tooprotect 應用程式，並避免 hello 成本以及複雜性的建立和管理您自己的次要位置。 Azure 會加密資料，通訊，而且您擁有 hello 選項太啟用資料靜止的加密。

它會持續監視 hello 健全狀況，您的服務，可協助將自動 hello hello 主要資料中心在網站中斷的 hello 事件中的服務以正確順序的復原。 虛擬機器可以處於中協調的方式 toohelp 還原服務快速，甚至針對複雜的多層式工作負載。

Site Recovery 使用現有的技術，例如 Hyper-V 複本、System Center 和 SQL Server Always On。 請查看 [Azure Site Recovery 概觀](site-recovery/site-recovery-overview.md) ，以了解更多詳細資料。

### <a name="azure-backup"></a>Azure 備份
![Azure 備份](./media/fundamentals-introduction-to-azure/AzureBackupIntroNew.png)  

*圖： Azure Backup 備份資料從內部部署 Windows Server 到 hello 的雲端。*  

Azure 備份會備份資料從內部部署伺服器到 hello 的雲端執行 Windows Server。 您可以直接從 Windows Server 2012、 Windows Server 2012 Essentials 或 System Center 2012-Data Protection Manager 中的 hello 備份工具來管理您的備份。 或者，您也可以使用專業的備份代理程式。

由於備份會在傳輸前會先加密，並在 Azure 中以加密方式儲存，且受到您所上傳的憑證保護，因此資料較為安全。 hello 服務會使用相同的備援和高可用性的資料保護找到 Azure 儲存體中的 hello。  您可以選擇執行完整或增量備份，並依照定期排程或立即備份檔案和資料夾。 Toohello 雲端備份資料之後，授權的使用者可以輕鬆地復原備份 tooany 伺服器。 它也提供可設定的資料保留原則、 資料壓縮和資料傳輸節流，您可以管理 hello 成本 toostore 和傳送資料。

**Azure 備份的案例**

如果您已經在使用 Windows Server 或 System Center，Azure 備份會是備份您的伺服器檔案系統、虛擬機器和 SQL Server 資料庫的自然解決方案。  它可與加密、疏鬆和壓縮檔案搭配使用。 有一些限制，因此您應該[檢查 hello Azure 備份的必要元件](http://technet.microsoft.com/library/dn296608.aspx)第一次。

## <a name="messaging-and-integration"></a>傳訊與整合
不論它做什麼，程式碼經常需要 toointeract 與其他程式碼。  在有些情況下，只需要基本佇列訊息而已。 而在其他情況下，則需要更複雜的互動。 Azure 提供幾個不同的方式 toosolve 這些問題。 圖 5 說明 hello 的選擇。

### <a name="queues"></a>佇列
![Azure 服務匯流排轉送](./media/fundamentals-introduction-to-azure/QueuesIntroNew.png)

*圖：佇列可讓您在應用程式的各組件之間進行鬆散耦合，而且可以讓您調整規模。*  

佇列是一個簡單構想：一個應用程式可將訊息放入佇列中，而該訊息最終會由其他應用程式所讀取。 如果您的應用程式需要只這個簡單的服務，Azure 佇列可能 hello 最好的選擇。

Hello 方式 hello Azure 成長經過一段時間，因為 Azure 儲存體佇列和服務匯流排佇列會提供類似的佇列服務。 hello 相當技術白皮書中有討論原因讓您會想透過 hello toouse 其中一個其他的 hello 原因[Azure 佇列和服務匯流排佇列-比較和對比](http://msdn.microsoft.com/library/azure/hh767287.aspx)。  在許多案例中，任一種都適用。

**佇列案例**

有一個佇列常見的用法今天是與背景工作角色執行個體中的 web 角色執行個體通訊的 toolet hello 相同雲端服務應用程式。

例如，假設您建立一個可供分享視訊的 Azure 應用程式。 hello 應用程式包含 PHP 執行的程式碼可讓使用者上傳並觀看影片，以及實作的 C# 會轉譯程式的背景工作角色上傳的 web 角色中視訊成各種格式。

當 web 角色執行個體是從使用者取得新的視訊時，它可以 hello 視訊儲存為 blob，然後傳送訊息 tooa 背景工作角色透過佇列，告訴它其中 toofind 這個新視訊。 背景工作角色的執行個體-it 不層面 hello 佇列中的讀取接著一個會 hello 訊息，以及執行所需的 hello hello 背景視訊的翻譯。

結構化的應用程式在這種方式可讓非同步處理，而且更 hello 應用程式更容易 tooscale，因為獨立差異性 hello web 角色執行個體和背景工作角色執行個體數目。 您也可以使用以觸發程序 tooscale hello 數目增加和減少的背景工作角色的 hello 佇列大小。 過高時，則新增更多角色。 當它取得較低時，您可以減少執行角色 toosave money 的 hello 數目。  

您可以在應用程式的許多不同部分之間使用相同的模式，即使他們不使用 Web 和背景工作角色亦同。  它可讓您視需要增加和減少 hello 佇列的任一邊 tooscale hello 組件，並需要處理時間。

### <a name="service-bus"></a>服務匯流排
是否在資料中心，在行動裝置，或其他地方的 hello 雲端中執行應用程式需要 toointeract。 Azure 服務匯流排 hello 目標是執行幾乎任何地方 toolet 應用程式交換資料。

在加法 toohello 佇列 （一對一） 稍早所述，服務匯流排也提供 tooother 通訊方法。

#### <a name="service-bus-relay"></a>Service Bus 轉送
![Azure 服務匯流排轉送](./media/fundamentals-introduction-to-azure/ServiceBusRelayIntroNew.png)

*圖：服務匯流排轉送允許位在防火牆不同側的應用程式進行通訊。*

服務匯流排 」 可讓其轉送服務，透過直接通訊提供安全的方式 toointeract 通過防火牆。 服務匯流排轉送來啟用應用程式 toocommunicate 交換訊息，透過端點裝載在 hello 雲端中，而不是在本機。

**服務匯流排轉送案例**

透過服務匯流排通訊的應用程式有可能是在其他雲端平台上執行的 Azure 應用程式或軟體。 它們也可以是外部 hello 雲端，不過執行的應用程式。 例如，假設有一家航空公司在自有資料中心內的電腦中提供訂位服務。 hello airline 需要 tooexpose 這些服務 toomany 用戶端，包括從機場、 保留代理程式的終端機，或甚至客戶電話簽入 kiosk。 它可能會使用服務匯流排 toodo 這各種應用程式建立 hello 鬆散偶合的互動。

#### <a name="service-bus-topics-and-subscriptions"></a>服務匯流排主題和訂用帳戶
![Azure 服務匯流排主題](./media/fundamentals-introduction-to-azure/ServiceBusTopicsSubsIntroNew.png)   
 *圖： Service Bus 主題可讓多個應用程式 toopost 訊息以及其他符合特定準則的應用程式 toosubscribe tooreceive 訊息。*

服務匯流排提供一個稱為主題和訂用帳戶的發佈與訂用帳戶機制。 發佈/訂閱，與應用程式可以傳送訊息 tooa 主題，而其他應用程式可以建立訂閱 toothis 主題。 這可讓一組應用程式，讓相同的訊息被讀取多個收件者的 hello 之間的一對多的通訊。

**服務匯流排主題和訂用帳戶案例**

每當您要設定的所有重要的是，許多訊息，但各種下游系統只會需要這些通訊 toolisten toodiffering 子集，服務匯流排主題和訂用帳戶是個好選項。

### <a name="biztalk-services"></a>BizTalk 服務
![BizTalk 服務](./media/fundamentals-introduction-to-azure/BizTalkServicesIntroNew.png)   
 *圖： BizTalk 服務提供 hello 能力 tootransform XML 訊息格式 hello 雲端中。*

有時候，您會需要連接使用不同訊息格式進行通訊的系統。 很常見的商業 toohave 不同的資料庫結構描述和 XML 訊息格式，即使使用通用的標準。 而不是撰寫自訂程式碼很多，您可以使用 BizTalk Server 在內部部署 toointegrate 各種系統。  Azure BizTalk 服務提供 hello 相同類型的服務，但 hello 雲端中。 您可以針對只您使用，並像您會具有 tooon 內部，不必擔心小數位數付費。

**BizTalk 服務案例**

企業對企業 (B2B) 互動通常需要此類型的轉譯。  例如，建置飛機需求 tooorder 從它的組件的公司是各種零件供應商。 它會有許多零件供應商。  訂單應該自動化的 toogo 直接從 hello 飛機建造商系統將 hello 供應商系統。  沒有商務想 toochange 其核心系統和訊息格式，並不太可能非常這些格式是 hello 相同。 BizTalk 服務可以使用訊息，並轉譯個 hello 新格式的兩種方式。 其中一個 hello 飛機供應商可以 hello 工作 tootranslate 或 hello 各種供應商可以根據誰會想多個控制項 hello 數量及所需的轉譯。     

## <a name="compute-assistance"></a>運算協助
Azure 提供服務不需要 toorun 所有 hello 時間的協助。  

### <a name="scheduler"></a>排程器
![Azure 排程器](./media/fundamentals-introduction-to-azure/SchedulerIntroNew.png)   
*圖： Azure 排程器提供方式 tooschedule 作業在特定持續期間內的特定時間。*

有時候應用程式只會需要 toorun 在特定時間。 在 Azure 上，您可以在這種類型的應用程式，而不是讓應用程式繼續執行 24x7 等候資料 tooprocess 只儲存金錢。 Azure 排程器可讓您 tooschedule 時應用程式應該根據執行的時間與行事曆的間隔。 它非常可靠，並確認即使網路、機器和資料中心發生故障，程序也會照樣執行。 使用 hello 排程器 REST API toomanage 這些動作。

排程的警示發生時，排程器傳送 HTTP 或 HTTPS 訊息 tooa 特定端點，或可以將訊息放在儲存體佇列。  因此您需要 toohave 應用程式具有可存取的端點，或將監視儲存體佇列。 然後一旦到達 hello 訊息，它可以執行任何動作來進行程式設計。

**排程器案例**

* 重複的應用程式動作： 例如，服務可能定期從 twitter 取得資料與 hello 資料收集為一般摘要。
* 每日維護：記錄處理或剪除、執行備份及其他間歇性排程工作。
* 在夜間執行的工作。
* Web 應用程式工作，如每日剪除記錄、執行備份及其他維護工作。 系統管理員可以選擇 toobackup 她資料庫 hello 每天上午 1 未來 9 個月，例如。

hello 排程器 API 可讓您 toocreate、 更新、 刪除、 檢視和管理工作集合和排程的工作以程式設計的方式。

## <a name="performance"></a>效能
效能對應用程式總是很重要。 應用程式通常 tooaccess 反覆 hello 相同的資料。 其中一種方式 tooimprove 效能 tookeep 一份該資料更接近 toohello 應用程式，所以降至最低的 hello 次需要 tooretrieve 它。 Azure 為此提供了不同的服務：

### <a name="azure-caching"></a>Azure 快取
![Azure 快取](./media/fundamentals-introduction-to-azure/AzureCacheIntroNew.png)   
 **圖：Azure 應用程式可以快取記憶體內部資料，並甚至在許多不同的背景工作角色中將其分割**

存取在任何 Azure 資料管理服務 (SQL Database、資料表或 Blob) 中儲存的資料時，速度會相當快。 但存取記憶體內部儲存的資料時，速度則更加快速。 因此，保留經常存取之資料的記憶體內部複本，可以改善應用程式效能。 您可以使用 Azure 的記憶體中快取 toodo 這個。

雲端服務應用程式可以將資料儲存在此快取，然後擷取直接而不需要 tooaccess 永續性儲存體。 內部應用程式的 Vm，或提供的 Vm 所專用單獨 toocaching 可以維護 hello 快取。 在任一情況下，可以發佈 hello 快取，hello 資料其中散佈跨 Azure 資料中心內的多個 Vm。

Azure 具備許多不同的快取技術，而這些技術已隨著時間出現轉型。 為了 hello 它們所導入，沒有共用的角色中，管理與 Redis 快取。 hello 共用快取是較舊技術，您不應該使用它來建立新的實作。 hello 受管理快取的 hello hello 角色中的相同功能快取，但做為受管理的服務之外的 hello Azure 管理入口網站。 hello Redis 快取為預覽狀態。 hello Redis 實作 hello 的功能的最大數目，並建議您在撰寫新的快取程式碼時。

**Azure 快取案例**

重複讀取 產品類別目錄的應用程式可能會受益於使用這種快取，比方說，自 hello 資料之後需要將予以提供更快速。 hello 技術也支援鎖定，讓它能與讀取/寫入，以及唯讀資料。 和 ASP.NET 應用程式可以使用只在組態變更的 hello 服務 toostore 工作階段資料。

### <a name="content-delivery-network"></a>內容傳遞網路
![Azure CDN](./media/fundamentals-introduction-to-azure/CDNIntroNew.png)   
 **圖： 的 blob 複本可以在 hello 世界各地的站台快取。**

假設您需要將由 hello 世界各地的使用者存取 toostore blob 資料。 可能是視訊 hello 最新世界 Cup 相符項目，例如，驅動程式更新或熱門的電子書。 有助於將 hello 資料的複本儲存在多個 Azure 資料中心，但是如果有大量使用者，則可能不足夠。 為了更好的效能，您可以使用 hello Azure CDN。

hello CDN 會有不同的站台周圍 hello world，每個都能將複本的 Azure blob 儲存。 hello hello world 的某些部分的使用者存取特定 blob，第一次 hello 其所含的資訊會複製從 Azure 資料中心到本機 CDN 儲存體的地理位置中。 在此之後，組件的 hello world 的存取會使用 hello blob 複製 hello CDN 中快取-它們不需要 toogo 所有 hello 方式 toohello 最接近的 Azure 資料中心。 hello 結果是由使用者 hello 世界各地的更快速存取 toofrequently 存取資料。

**CDN 案例**

常見 Media Services toodeliver 視訊全球 toouse CDN 它。 視訊通常為大檔案且需要很多頻寬。  本頁其他位置會針對媒體服務進行討論。

## <a name="big-data-and-big-compute"></a>大數據與大量運算
### <a name="hdinsight-hadoop"></a>HDInsight (Hadoop)
![HDInsight](./media/fundamentals-introduction-to-azure/HDInsightIntroNew.png)   
 **圖： HDInsight 有助於 hello 大量處理的大量資料**

許多年，hello 大量的資料分析尚未建置關聯式 DBMS 的資料倉儲中儲存關聯式資料上執行。 這種商務分析仍是很重要，並會很長的時間 toocome。 但如果想 tooanalyze hello 資料是大的關聯式資料庫就無法加以處理嗎？ 並假設 hello 資料不是關聯式嗎？ 舉例來說，此資料可能是資料中心的伺服器記錄檔，或感應器過去的事件資料，或是其他資料。 在這類情況下，您會有所謂的巨量資料問題。 您需要其他方法。

Hadoop 今天來分析巨量資料的 hello 主控項技術。 Apache 開放原始碼專案，這項技術使用 hello Hadoop 分散式檔案系統 (HDFS)，儲存資料，然後讓開發人員建立 MapReduce 工作 tooanalyze 該資料。 HDFS 會將分散資料到多部伺服器，則平行處理的每一項，讓 hello 巨量資料的 hello MapReduce 工作的執行區塊。

HDInsight 是服務的 hello hello Azure Apache Hadoop 為基礎名稱。 HDInsight 可讓 HDFS hello 叢集上儲存資料，並將它分散多個 Vm。 它也會將分散 MapReduce 工作的 hello 邏輯到那些 Vm。 在內部部署 Hadoop 資料為處理本機-hello 邏輯，而 hello 資料上運作，如同 hello 相同的 VM-和以平行方式，以提升效能。 此外，HDInsight 也可以在採用 Blob 的 Azure Storage Vault (ASV) 中儲存資料。  使用 ASV 可讓您 toosave 金錢，因為您可以刪除不在使用中，當您的 HDInsight 叢集，但仍保留 hello 雲端中的資料。

HDinsight 支援，hello Hadoop 生態系統的其他元件，包括 Hive 和 Pig。 Microsoft 也已經建立元件，可讓您更容易 toowork HDInsight 所產生的資料使用傳統 BI 工具，例如 hello HiveODBC 配接器和使用 Excel 的資料瀏覽器。

### <a name="high-performance-computing-big-compute"></a>高效能計算 (大量計算)
其中最具吸引力方式 toouse hello 雲端平台是 toorun 高效能運算 (HPC) 和其他 「 Big Compute 」 應用程式。 範例包括特製化的工程應用程式建置 toouse hello 工業標準訊息傳遞介面 (MPI)，以及所謂窘迫平行應用程式，這類財務風險模型。

hello Big Compute 的本質 hello 在許多電腦上執行程式碼相同的時間。 在 Azure 上，這表示同時執行多個虛擬機器所有平行 toosolve 工作發生問題。 這樣做需要某些方式 tooresources 和 tooschedule 應用程式，亦即，toodistribute 工作橫跨這些執行個體。 Microsoft 的免費 HPC Pack 及其他計算叢集解決方案可以執行 Azure 計算和基礎結構服務 tooadd 容量隨 tooan 內部部署計算叢集或執行 Big Compute 應用程式完全在 hello Azure，利用在正常雲端。

Azure 提供範圍的 VM 執行個體大小搭配不同的組態，包括 CPU 核心數、 記憶體、 磁碟容量，以及不同的應用程式的其他特性 toomeet hello 需求。 hello 最近推出的 A8 和 A9 執行個體適用於許多運算密集工作負載，以及平行 MPI 應用程式特別的是，擁有高速、 多核心 Cpu 以及大量的記憶體。 在某些情況下設定 hello 利用低延遲高輸送量應用程式網路包含平行 MPI 應用程式的最大效率的遠端直接記憶體存取 (RDMA) 技術的 hello 雲端中。

Azure 還為大量計算應用程式開發人員和合作夥伴提供一組完整的計算功能、服務、架構選擇及開發工具。 Azure 支援自訂 Big Compute 工作流程涉及特定的資料的工作流程及作業和工作排程模式可調整的 toothousands 計算核心。

## <a name="media"></a>媒體
![Azure 媒體服務](./media/fundamentals-introduction-to-azure/MediaServicesIntroNew.png)   
 **圖： Media Services 是提供視訊與 hello 世界各地的其他媒體 tooclients 應用程式的平台。**

視訊構成了現今網際網路流量的一大部分，其所佔的比例日益提高。 尚未提供 hello 網站上的視訊不簡單。 有許多變數，例如 hello 編碼演算法和 hello 顯示 hello 使用者畫面的解析度。 視訊也通常會面臨需求，例如星期六晚上突然增加時有許多人會決定他們想 toowatch 線上影片 toohave 暴增。

因為其大受歡迎，所以建立許多使用視訊的新應用程式將會萬無一失。 但所有的這些部分需要 toosolve hello 的相同問題，以及讓每個解決這些問題，其本身沒有任何意義。 更好的方法是 toocreate 提供許多應用程式 toouse 常見解決方案的平台。 並且建立這個平台 hello 雲端中的提供的一些明顯的優點。 它可以是廣泛使用隨用隨付為基礎，它也可以處理 hello 變化性視訊應用程式通常會面臨的需求。

Azure 媒體服務可處理此問題。 其提供一組雲端元件，讓人們得以使用視訊和其他媒體更輕鬆地建立及執行應用程式。

如 hello 圖所示，Media Services 提供一組元件使用影片和其他媒體的應用程式。 例如，它包含媒體元件 tooupload 影片內嵌到媒體服務 （其中會儲存在 Azure Blob 中）、 支援各種視訊和音訊格式的編碼元件、 內容保護元件，可提供數位版權管理將廣告插入視訊資料流、 進行串流處理、 元件及其他元件。 Microsoft 合作夥伴也可以提供元件 hello 平台，然後讓 Microsoft 發佈這些元件，並代表它開立其帳單。

使用此平台的應用程式可以在 Azure 上或其他地方執行。 例如，桌面應用程式的視訊生產房屋可能允許使用者上載視訊 tooMedia 服務再處理它以各種方式。 或者，在 Azure 上執行的雲端內容的管理服務可能會依賴 Media Services tooprocess 並發佈視訊。 每個應用程式執行的任一處，任何會選擇哪些元件需要 toouse，透過 rest 式介面進行存取。

toodistribute 便會產生、 應用程式可以使用 hello Azure CDN，另一個 CDN，或只傳送直接 bits toousers。 但是，無論其送達的方式為何，各種用戶端系統 (包括 Windows、Macintosh、HTML 5、iOS、Android、Windows Phone、Flash 和 Silverlight) 均可取用以媒體服務建立的視訊。 hello 的目標是 toomake 它更容易 toocreate 現代媒體應用程式。

**參考**

媒體服務的運作方式的更視覺化檢視，請下載 hello [Azure 媒體服務海報][Azure Media Services Poster]。

## <a name="commerce"></a>商業
轉換 hello 崛起軟體即服務，我們要如何建立應用程式。 同時也改變我們銷售應用程式的方式。 因為 SaaS 應用程式位於 hello 雲端，合理的潛在客戶應該看起來的線上解決方案。 這項變更適用於 toodata 以及 tooapplications。 為什麼不應該人員尋找 toohello 雲端市面上取得的資料集？ Microsoft 解決以上兩個以 hello 這些考量[Azure Marketplace](https://azure.microsoft.com/marketplace/)。

![Azure 商業](./media/fundamentals-introduction-to-azure/CommerceIntroNew.png)   
 **圖：您可利用 Azure Marketplace 和 Azure Store 尋找和購買 Azure 應用程式和商業資料集，並將他們當作 Azure 應用程式的一部分使用。**

hello hello 兩者之間的差異是，Marketplace 超出 hello Azure 管理入口網站中，但可以存取 hello 存放區，從內 hello 入口網站。 潛在客戶可以搜尋 toofind Azure 符合其需求的應用程式。 客戶也可以搜尋商業資料集，包括人口統計資料、財務資料、地理資料等。 當他們尋找所要的項目時，他們可以存取它從 hello 廠商直接透過 hello Marketplace 或存放區的 web 位置，或在某些情況下，從 hello 管理入口網站。 應用程式也可以使用 hello Bing 搜尋應用程式開發介面透過 hello Marketplace，讓它們存取 toohello 網頁搜尋結果。

**商務案例**

SendGrid 是 hello Azure 市集，可讓您 toosend 電子郵件中的應用程式。 它提供了如可靠的傳遞和統計資料等其他功能。  您可以購買此應用程式及相關的服務而非自行嘗試 toobuild 這類基礎結構。  

## <a name="getting-started"></a>開始使用
現在，您擁有 hello 大圖片 hello 下一個步驟是 toowrite Azure 應用程式第一次。 選擇您的語言，[取得 hello 適當 SDK](/downloads/)，並繼續。 雲端運算是 hello 新預設值-立即開始使用。

[Azure Media Services Poster]: http://azure.microsoft.com/documentation/infographics/media-services/
