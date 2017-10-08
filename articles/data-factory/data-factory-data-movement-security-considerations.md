---
title: "Azure Data Factory 中的資料移動的 aaaSecurity 考量 |Microsoft 文件"
description: "了解如何在 Azure Data Factory 中保護資料移動。"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 4bfce8884df14ad5b94e28ad3dfcf7025e2130a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---security-considerations-for-data-movement"></a>Azure Data Factory - 資料移動的安全性考量
## <a name="introduction"></a>簡介
這篇文章描述 Azure Data Factory 中的資料移動服務使用 toosecure 您資料的基本安全性基礎結構。 Azure Data Factory 管理資源建置在 Azure 安全性基礎結構上，並使用 Azure 提供的所有可能安全性措施。

在 Data Factory 方案中，您可以建立一或多個資料 [管線](data-factory-create-pipelines.md)。 管線是一起執行某個工作的活動所組成的邏輯群組。 這些管線位於 hello hello 資料處理站建立所在的區域。 

即使 Data Factory 僅提供**美國西部**，**美國東部**，和**北歐**區域，hello 資料移動服務可供使用[全域中數個區域](data-factory-data-movement-activities.md#global)。 Data Factory 服務會確保資料不會離開地理區域，/ 區域除非您明確指示 hello 服務 toouse 替代地區如果 hello 資料移動服務不是尚未部署 toothat 區域。 

Azure Data Factory 本身除了用於雲端資料存放區的已連結服務認證 (會使用憑證加密) 之外，並不會儲存任何資料。 它可讓您建立資料驅動型工作流程 tooorchestrate 之間資料移動的[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)和處理的資料使用[計算服務](data-factory-compute-linked-services.md)內部或其他區域中環境。 它也可讓您太[監視和管理工作流程](data-factory-monitor-manage-pipelines.md)同時以程式設計方式使用和 UI 機制。

使用 Azure Data Factory 進行的資料移動已通過下列各項規範的「認證」：
-   [HIPAA/HITECH](https://www.microsoft.com/en-us/trustcenter/Compliance/HIPAA)  
-   [ISO/IEC 27001](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27001)  
-   [ISO/IEC 27018](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27018) 
-   [CSA STAR](https://www.microsoft.com/en-us/trustcenter/Compliance/CSA-STAR-Certification)
     
如果您想要在 Azure 的符合性與 Azure 保護本身的基礎結構的方式，請瀏覽 hello [Microsoft 信任中心](https://www.microsoft.com/TrustCenter/default.aspx)。 

在本文中，我們來檢閱 hello 下列兩個資料移動案例中的安全性考量： 

- **雲端案例** - 在此案例中，可透過網際網路公開存取您的來源和目的地。 這些包括受管理的雲端儲存體服務 (例如「Azure 儲存體」、「Azure SQL 資料倉儲」、Azure SQL Database、Azure Data Lake Store、Amazon S3、Amazon Redshift)、SaaS 服務 (例如 Salesforce)，以及 Web 通訊協定 (例如 FTP 和 OData)。 如需完整的支援資料來源清單，請參閱[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。
- **混合式案例**-在此案例中，您的來源或目的地位於防火牆後方，或在內部部署公司網路或 hello 資料存放區是在私人網路 / 虛擬網路 （最常 hello 來源），而且不是可公開存取. 裝載在虛擬機器上的資料庫伺服器也屬於此案例的涵蓋範圍。

## <a name="cloud-scenarios"></a>雲端案例
###<a name="securing-data-store-credentials"></a>保護資料存放區認證
Azure Data Factory 可透過使用「受 Microsoft 管理的憑證」來「加密」資料存放區認證，為這些認證提供保護。 這些憑證每隔「兩年」會輪替一次 (包括憑證更新和憑證移轉)。 這些已加密的認證會安全地儲存在「受 Azure Data Factory 管理服務管理的 Azure 儲存體」中。 如需有關「Azure 儲存體」安全性的詳細資訊，請參閱 [Azure 儲存體安全性概觀](../security/security-storage-overview.md)。

### <a name="data-encryption-in-transit"></a>傳輸中資料加密
如果 hello 雲端資料存放區支援 HTTPS 或 TLS 時，Data Factory 中的資料移動服務之間的所有資料都傳輸和雲端資料存放區會透過 HTTPS 或 TLS 的安全通道。

> [!NOTE]
> 所有連線太**Azure SQL Database**和**Azure SQL 資料倉儲**一律需要加密 (SSL/TLS)，資料傳輸 tooand 從 hello 資料庫時發生。 撰寫使用 JSON 編輯器的管線，時新增 hello**加密**屬性並將它設定太**true**在 hello**連接字串**。 當您使用 hello[複製精靈](data-factory-azure-copy-wizard.md)，hello 精靈預設會設定這個屬性。 如**Azure 儲存體**，您可以使用**HTTPS** hello 連接字串中。

### <a name="data-encryption-at-rest"></a>待用資料加密
有些資料存放區支援待用資料加密。 建議您為這些資料存放區啟用資料加密機制。 

#### <a name="azure-sql-data-warehouse"></a>Azure SQL 資料倉儲
Azure SQL 資料倉儲中的透明資料加密 (TDE) 會協助防範惡意活動的 hello 威脅所執行的即時加密與解密的靜止資料。 此行為是透明的 toohello 用戶端。 如需詳細資訊，請參閱[保護 SQL 資料倉儲中的資料庫](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md)。

#### <a name="azure-sql-database"></a>Azure SQL Database
Azure SQL Database 也支援透明資料加密 (TDE)，協助防範惡意活動的 hello 威脅，藉由執行 hello 資料的即時加密與解密，而不需要變更 toohello 應用程式。 此行為是透明的 toohello 用戶端。 若要深入了解，請參閱 [Azure SQL Database 的透明資料加密](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)。 

#### <a name="azure-data-lake-store"></a>Azure Data Lake Store
Azure 資料湖存放區也會提供資料儲存在 hello 帳戶加密。 啟用時，資料湖存放區會自動保存之前加密資料，並擷取功能，讓透明 toohello 用戶端存取 hello 資料之前解密。 如需詳細資訊，請參閱 [Azure Data Lake Store 安全性](../data-lake-store/data-lake-store-security-overview.md)。 

#### <a name="azure-blob-storage-and-azure-table-storage"></a>Azure Blob 儲存體和 Azure 資料表儲存體
Azure Blob 儲存體和 Azure 資料表儲存體支援儲存體服務加密 (SSE) 中，可自動加密您的資料之前保存 toostorage 和之前擷取的解密。 如需詳細資訊，請參閱[待用資料的 Azure 儲存體服務加密](../storage/common/storage-service-encryption.md)。

#### <a name="amazon-s3"></a>Amazon S3
Amazon S3 同時支援用戶端和伺服器的待用資料加密。 如需詳細資訊，請參閱[使用加密來保護資料 (英文)](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingEncryption.html)。 目前，Data Factory 並不支援虛擬私人雲端 (VPC) 內的 Amazon S3。

#### <a name="amazon-redshift"></a>Amazon Redshift
Amazon Redshift 支援叢集待用資料加密。 如需詳細資訊，請參閱 [Amazon Redshift 資料庫加密 (英文)](http://docs.aws.amazon.com/redshift/latest/mgmt/working-with-db-encryption.html)。 目前，Data Factory 並不支援 VPC 內的 Amazon Redshift。 

#### <a name="salesforce"></a>Salesforce
Salesforce 支援「Shield 平台加密」，可加密所有檔案、附件、自訂欄位。 如需詳細資訊，請參閱[Web 伺服器 OAuth 驗證流程的了解 hello](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_web_server_oauth_flow.htm)。  

## <a name="hybrid-scenarios-using-data-management-gateway"></a>混合式案例 (使用資料管理閘道)
混合式案例需要安裝在與內部網路或虛擬網路 (Azure) 或是虛擬的私人雲端 (Amazon) 內的資料管理閘道器 toobe。 hello 閘道必須能夠 tooaccess hello 本機資料存放區。 如需 hello 閘道的詳細資訊，請參閱[資料管理閘道器](data-factory-data-management-gateway.md)。 

![「資料管理閘道」的通道](media/data-factory-data-movement-security-considerations/data-management-gateway-channels.png)

hello**命令通道**可讓在 Data Factory 中的資料移動服務和資料管理閘道器之間的通訊。 hello 通訊包含資訊相關的 toohello 活動。 hello 資料通道會用於內部部署資料存放區和雲端資料存放區之間傳送資料。    

### <a name="on-premises-data-store-credentials"></a>內部部署資料存放區認證
您在內部部署資料存放區的 hello 認證儲存在本機 （不在 hello 雲端）。 您可以透過三種不同的方式設定這些認證。 

- 從「Azure 入口網站」/「複製精靈」透過 HTTPS 使用**純文字** (較不安全)。 hello 認證會傳遞純文字 toohello 在內部部署閘道中。
- **從複製精靈使用 JavaScript 密碼編譯程式庫**。
- 使用 **Click-Once 型認證管理員應用程式**。 hello 按一下-一旦具有存取 toohello 閘道，並設定 hello 資料存放區認證 hello 在內部部署機器上執行應用程式。 此選項和下一個是 hello hello 最安全選項。 hello 認證管理員應用程式，根據預設，hello 連接埠 8050 機器上使用 「 hello 與閘道進行安全通訊。  
- 使用[新增 AzureRmDataFactoryEncryptValue](/powershell/module/azurerm.datafactories/New-AzureRmDataFactoryEncryptValue) PowerShell cmdlet tooencrypt 認證。 hello cmdlet 會使用該閘道是設定的 toouse tooencrypt hello 認證 hello 憑證。 您可以使用此 cmdlet 所傳回的 hello 加密認證並將它新增到太**EncryptedCredential** hello 的項目**connectionString** hello JSON 檔案中，您使用以 hello [新 AzureRmDataFactoryLinkedService](/powershell/module/azurerm.datafactories/new-azurermdatafactorylinkedservice) cmdlet 或在 hello 入口網站中的 hello Data Factory 編輯器中的 hello JSON 片段。 此選項與 hello 依序按一下-應用程式之後 hello 最安全選項。 

#### <a name="javascript-cryptography-library-based-encryption"></a>JavaScript 密碼編譯程式庫型加密
您可以加密資料存放區認證使用[JavaScript 密碼編譯程式庫](https://www.microsoft.com/download/details.aspx?id=52439)從 hello[複製精靈](data-factory-copy-wizard.md)。 當您選取此選項時，hello 複製精靈會擷取 hello 閘道的公用金鑰，並使用它 tooencrypt hello 資料存放區認證。 hello 認證會解密 hello 閘道電腦，再受到 Windows 的[DPAPI](https://msdn.microsoft.com/library/ms995355.aspx)。

**支援的瀏覽器：**IE8、IE9、IE10、IE11、Microsoft Edge，以及最新版 Firefox、Chrome、Opera、Safari 瀏覽器。 

#### <a name="click-once-credentials-manager-app"></a>Click-Once 認證管理員應用程式
您可以啟動 hello 按一下-一旦基礎從 Azure 入口網站/複製精靈的 認證管理員應用程式中撰寫管線時。 此應用程式可確保您的認證不會以純文字透過傳送 hello 網路。 根據預設，它會使用 hello 連接埠**8050**上 hello 與閘道進行安全通訊。 您可以視需要變更此連接埠。  
  
![Hello 閘道的 HTTPS 連接埠](media/data-factory-data-movement-security-considerations/https-port-for-gateway.png)

「資料管理閘道」目前使用單一「憑證」。 Hello 閘道安裝期間會建立此憑證 (適用於的 tooData 2016 年 11 月之後建立的管理閘道器和 2.4.xxxx.x 版本或更新版本)。 您可以使用自己的 SSL/TLS 憑證來取代此憑證。 此憑證由 hello 按一下-一旦認證管理員應用程式 toosecurely 連接 toohello 閘道機器設定資料存放區認證。 它會儲存資料存放區認證安全地在內部使用 hello Windows [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx) hello 與閘道的電腦上。 

> [!NOTE]
> 較舊版本 2.3.xxxx.x 或 2016 年 11 月之前已安裝的閘道繼續 toouse 認證加密並儲存在雲端上。 即使您升級 hello 閘道 toohello 最新版本，hello 認證也無法移轉的 tooan 在內部部署機器    
  
| 閘道版本 (建立時) | 認證儲存位置 | 認證加密/安全性 | 
| --------------------------------- | ------------------ | --------- |  
| 低於或等於 2.3.xxxx.x | 雲端 | 使用憑證 （不同於其中一個認證管理員應用程式所使用的 hello） 進行加密 | 
| 高於或等於 2.4.xxxx.x | 內部部署 | 透過 DPAPI 進行保護 | 
  

### <a name="encryption-in-transit"></a>傳輸中加密
所有的資料傳輸是透過安全通道**HTTPS**和**TLS over TCP** tooprevent 攔截攻擊與 Azure 服務進行通訊。
 
您也可以使用[IPSec VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md)或[Express Route](../expressroute/expressroute-introduction.md) toofurther hello 安全通訊通道，您在內部部署網路與 Azure 之間。

虛擬網路是網路的您 hello 雲端中的邏輯表示法。 您可以藉由設定 IPSec VPN （站對站） 或 （私人互連） Express Route 連線在內部部署網路 tooyour Azure 虛擬網路 (VNet)       

hello 下表摘要說明 hello 網路和閘道設定建議的混合式資料移動的來源和目的地位置的不同組合為基礎。

| 來源 | 目的地 | 網路組態 | 閘道安裝 |
| ------ | ----------- | --------------------- | ------------- | 
| 內部部署 | 部署在虛擬網路中的虛擬機器和雲端服務 | IPSec VPN (點對站或站台對站台) | 閘道可以安裝在內部部署環境或 VNet 中的 Azure 虛擬機器 (VM) 上 | 
| 內部部署 | 部署在虛擬網路中的虛擬機器和雲端服務 | ExpressRoute (私用對等) | 閘道可以安裝在內部部署環境或 VNet 中的 Azure VM 上 | 
| 內部部署 | 具有公用端點的 Azure 型服務 | ExpressRoute (公用對等) | 閘道必須安裝在內部部署環境 | 

hello 下列影像顯示 hello 使用量資料管理閘道器的內部部署資料庫與 Azure 服務使用 Express route 和 IPSec VPN （使用虛擬網路） 之間移動資料：

**ExpressRoute：**
 
![使用 ExpressRoute 搭配閘道](media/data-factory-data-movement-security-considerations/express-route-for-gateway.png) 

**IPSec VPN：**

![IPSec VPN 搭配閘道](media/data-factory-data-movement-security-considerations/ipsec-vpn-for-gateway.png)

### <a name="firewall-configurations-and-whitelisting-ip-address-of-gateway"></a>防火牆組態及將閘道的 IP 位址加入白名單

#### <a name="firewall-requirements-for-on-premisesprivate-network"></a>內部部署/私人網路的防火牆需求  
在企業中，**公司防火牆**hello 組織的 hello 中央路由器上執行。 而且， **Windows 防火牆**hello 的 hello 閘道已安裝的本機電腦上執行精靈。 

hello 欞礹怮薽**輸出連接埠**和網域需求 hello**公司防火牆**。

| 網域名稱 | 輸出連接埠 | 說明 |
| ------------ | -------------- | ----------- | 
| `*.servicebus.windows.net` | 443、80 | Hello 閘道 tooconnect toodata 移動服務需 Data Factory 中 |
| `*.core.windows.net` | 443 | 由 hello 閘道 tooconnect tooAzure 儲存體帳戶，當您使用 hello[分段複製](data-factory-copy-activity-performance.md#staged-copy)功能。 | 
| `*.frontend.clouddatahub.net` | 443 | Hello 閘道 tooconnect toohello Azure Data Factory 服務所需。 | 
| `*.database.windows.net` | 1433   | (選擇性) 當您的目的地是 Azure SQL Database/「Azure SQL 資料倉儲」時，需要提供此資訊。 使用 hello 分段複製功能 toocopy 資料 tooAzure SQL 資料庫/Azure SQL 資料倉儲，而不需要開啟 hello 通訊埠 1433年。 | 
| `*.azuredatalakestore.net` | 443 | (選擇性) 當您的目的地是 Azure Data Lake Store 時，需要提供此資訊。 | 

> [!NOTE] 
> 您可以有 toomanage 連接埠/允許清單網域在 hello 視需要個別的資料來源的公司防火牆層級。 此表格僅使用 Azure SQL Database、「Azure SQL 資料倉儲」、Azure Data Lake Store 作為範例。   

hello 欞礹怮薽**輸入連接埠**需求 hello **windows 防火牆**。

| 輸入連接埠 | 說明 | 
| ------------- | ----------- | 
| 8050 (TCP) | 所需的 hello 認證管理員應用程式 toosecurely 組認證 hello 閘道上的內部部署資料存放區。 | 

![閘道連接埠需求](media\data-factory-data-movement-security-considerations/gateway-port-requirements.png) 

#### <a name="ip-configurations-whitelisting-in-data-store"></a>資料存放區中的 IP 組態/白名單設定
Hello 雲端中的某些資料存放區也需要存取它們的 hello 機器的 IP 位址的允許清單。 確定 hello 閘道機器 hello IP 位址在允許清單中適當設定防火牆。

hello 下列雲端資料存放區需要 hello 閘道機器的 IP 位址的允許清單。 根據預設，這些資料存放區，部分可能不需要 hello IP 位址的允許清單。 

- [Azure SQL Database](../sql-database/sql-database-firewall-configure.md) 
- [Azure SQL 資料倉儲](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal)
- [Azure Data Lake Store](../data-lake-store/data-lake-store-secure-data.md#set-ip-address-range-for-data-access)
- [Azure Cosmos DB](../documentdb/documentdb-firewall-support.md)
- [Amazon Redshift](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) 

## <a name="frequently-asked-questions"></a>常見問題集

**問題：**可 hello 閘道之間共用不同的 data factory 嗎？
**答：**我們尚未支援這項功能。 我們正積極處理這個問題。

**問題：** hello 閘道 toowork hello 連接埠需求為何？
**回答：**閘道會以 HTTP 為基礎的連線 tooopen 網際網路。 hello**輸出連接埠 443 和 80**必須針對閘道 toomake 開啟此連接。 開啟**輸入連接埠 8050**只能在 hello 機器層級 （不在公司防火牆層級） 的憑證管理員應用程式。 如果使用 Azure SQL Database 或 Azure SQL 資料倉儲做為來源 / 目的地，則您需要 tooopen **1433年**以及連接埠。 如需詳細資訊，請參閱[防火牆組態及將 IP 位址加入白名單](#firewall-configurations-and-whitelisting-ip-address-of gateway)一節。 

**問：**閘道有什麼憑證需求？
**回答：**目前閘道需要憑證來安全地設定資料存放區認證供 hello 認證管理員應用程式。 此憑證是自我簽署的憑證建立和設定的 hello 閘道安裝程式。 您可以改用自己的 TLS/SSL 憑證。 如需詳細資訊，請參閱 [Click-Once 認證管理員應用程式](#click-once-credentials-manager-app)一節。 

## <a name="next-steps"></a>後續步驟
如需有關複製活動效能的資訊，請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)。

 
