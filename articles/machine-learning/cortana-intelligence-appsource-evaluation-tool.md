---
title: "aaaCortana 智慧方案評估工具 |Microsoft 文件"
description: "Microsoft 合作夥伴身分，以下是需要您 Cortana 智慧方案 tooAppSource toofollow toopublish 所有 hello 步驟。"
services: machine-learning
documentationcenter: 
author: AnupamMicrosoft
manager: jhubbard
editor: cgronlun
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: anupams;v-bruham;garye
ms.openlocfilehash: 76cde4e2090c121683b7026f3d80f90f64566607
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-evaluation-tool"></a>Cortana Intelligence 解決方案評估工具
## <a name="overview"></a>概觀
您可以用於 hello Cortana 智慧方案評估工具 tooassess 進階的分析解決方案符合 Microsoft 建議的最佳做法。 Microsoft 是高興的 toowork 與我們的協力廠商 (Isv / SIs) 的客戶、 轉售商與實作 tooprovide 高品質解決方案。 本指南會逐步解說的 hello 解決方案評估工具使用與您的方案 hello 程序，並說明 hello 特定的最佳作法中檢查。

## <a name="getting-started"></a>開始使用
請[下載](https://aka.ms/aa-evaluation-tool-download)並安裝 hello Cortana 智慧方案評估工具。

必要條件：
- Windows 10：[Windows 10 的官方網站](https://www.microsoft.com/en-us/windows)
- Azure PowerShell：[安裝和設定 Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0) \(英文\)。

## <a name="identifying-your-app"></a>識別您的應用程式
安裝完成後，開啟 hello 工具，並開始您第一次評估。

![開啟評估工具](./media/cortana-intelligence-appsource-evaluation-tool/1-open-evaluation-tool.png)

提供關於您解決方案的識別資訊。

![連接 Azure 訂用帳戶](./media/cortana-intelligence-appsource-evaluation-tool/2-connect-azure-subscription.png)

連接 tooyour Azure 訂用帳戶，並提供 hello 包含您的應用程式的資源群組。

![選取資源](./media/cortana-intelligence-appsource-evaluation-tool/3-select-resources.png)

一旦載入 hello 資源群組之後，請選取包含在您的方案中，找出 hello 協助工具，可能是任何資料資源的 hello 資源：
- 擷取
- 使用
- 內部

我們會使用這項資訊 toobetter 了解如何您的方案利用各種元件和 tooensure 使用者互動元件都符合最佳做法。

### <a name="ingestion"></a>擷取
擷取在此情況下表示資料從外部 hello 方案中的使用的 toopull 或 hello 方案之外的任何服務，使用到它 toopush 資料的任何資料來源。

### <a name="consumption"></a>耗用量
耗用量在此情況下表示會使用的 toopush 資料 tooend 使用者，不論是直接或間接的任何資料集。 例如：
- 從 PowerBI 中用於直接查詢的資料集。
- 在 WebApp 中查詢的資料集。

>[!NOTE]
如果特定的資源同時用於擷取和使用，請選擇 [使用]。

### <a name="internal"></a>內部
針對僅用於內部應用程式處理的任何資料資源，請使用「內部」。

接下來，您將會提示的 tooprovide 有效 hello 先前步驟中指定任何資料庫的認證：

![設定測試必要條件](./media/cortana-intelligence-appsource-evaluation-tool/4-set-test-prerequisites.png)

## <a name="solution-test-cases"></a>解決方案測試案例
hello 解決方案工具將會執行自動化測試的集合，在您的方案。

![設定測試執行](./media/cortana-intelligence-appsource-evaluation-tool/5-set-test-execution.png)

Hello 測試完成後，您就可以要求 tooprovide 說明或理由為何您的方案不符合 hello 需求。

![提供業務理由](./media/cortana-intelligence-appsource-evaluation-tool/6-provide-business-justification.png)

例如，如果您的方案發佈 tooAzure SQL DW，測試需要您 tooalso hello 評估發行 tooAzure Analysis Services。 

您的解決方案可能會使用執行 SQL Server Analysis Services (而非 Azure Analysis Services) 的 IaaS 虛擬機器。 這是可接受的 hello 測試的失敗原因。
## <a name="packaging-your-evaluation-results"></a>封裝您的評估結果
完成之後 hello 測試案例，評估封裝將會匯出的 tooa zip 檔案，將會要求您的意見反應 tooprovide hello 評估工具。 

您需要這項測試結果的評估再取得核准 toobe 加入您的方案 toobe 與 Microsoft 的 zip 檔案的 tooshare tooAppSource

![為評估工具評分](./media/cortana-intelligence-appsource-evaluation-tool/7-grade-evaluation-tool.png)

這個區段上方文章涵蓋 hello 工具的各種功能，現在讓我們檢閱此工具會評估的最佳作法的類型。

## <a name="security-evaluation-considerations"></a>安全性評估考量
### <a name="databases-should-use-azure-active-directory-authentication"></a>資料庫應使用 Azure Active Directory 驗證
任何 Azure SQL Azure SQL DW 中的或資源 hello sloution 應該啟用 Azure Active Directory (AAD) 驗證。 AAD 提供單一位置 toomanage 所有您的身分識別和角色。

| 如需下列項目的詳細資訊 | 請參閱此文章 |
| --- | --- |
| AAD 搭配 SQL Database 和 SQL 資料倉儲 | [利用 SQL Database 或 SQL 資料倉儲使用 Azure Active Directory 驗證來驗證](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication) |
| 設定和管理 AAD | [使用 SQL Database 或 SQL 資料倉儲設定和管理 Azure Active Directory 驗證](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure) |
| Azure WebApps 驗證 | [Azure App Service 中的驗證與授權](https://docs.microsoft.com/en-us/azure/app-service/app-service-authentication-overview) |
| 設定 WebApps 以搭配 AAD | [如何 tooconfigure 您 App Service 應用程式 toouse 的 Azure Active Directory 登入](https://docs.microsoft.com/en-us/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)|

### <a name="datasets-accessible-tooend-users-should-support-role-based-access-control"></a>資料集可存取 tooend 使用者應支援角色型存取控制
執行時 hello 評估工具，將會詢問 toospecify 任何報告或發行的資源。 系統會假設這些資源是提供給使用者存取，而非開發人員。 這些資源應該能提供角色型存取控制 (RBAC) 順序 tooensure 中僅能 tooaccess 授權資料是使用者。

具體而言，任何下列 Azure 資源的 hello 可以設定為使用 RBAC，並會被視為可接受：
- HDInsight 的安全，請參閱[簡介 tooHadoop 使用安全性已加入網域的 HDInsight 叢集](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-domain-joined-introduction)
- Azure SQL，請參閱 [AAD 驗證搭配 Azure SQL]( https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication)
- Azure Analysis Services，請參閱[針對 Azure Analysis Services 管理資料庫角色和使用者](https://docs.microsoft.com/azure/analysis-services/analysis-services-database-users) \(英文\)
- Azure SQL 資料倉儲 (請注意，因為 SQL DW 可支援 RBAC，因此不建議用於直接使用者存取)。

如果您使用可支援 RBAC 的不同資源類型，請指定的 hello 測試案例的理由。

### <a name="azure-data-lake-store-should-use-at-rest-encryption"></a>Azure Data Lake Store 應使用靜態加密
Azure Data Lake Store (ADLS) 支援預設使用 ADLS 受管理加密金鑰的靜態加密。 您也可以使用 Azure Key Vault 設定加密。

如需指定 ADLS 加密設定的相關資訊，請參閱[建立 Azure Data Lake Store 帳戶](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-portal#create-an-azure-data-lake-store-account)。

### <a name="azure-sql-and-azure-sql-data-warehouse-should-use-encryption"></a>Azure SQL 和 Azure SQL 資料倉儲應使用加密
Azure SQL 和 Azure SQL DW 都支援透明資料加密 (TDE)，這項功能可提供資料與記錄檔的即時加密和解密。

| 如需下列項目的詳細資訊 | 請參閱此文章 |
| --- | --- |
| 透明資料加密 (TDE) | [透明資料加密](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-tde) |
| Azure SQL 資料倉儲搭配 TDE | [SQL 資料倉儲加密 TDE TSQL](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-encryption-tde-tsql) |
| 設定 Azure SQL 以搭配 TDE | [Azure SQL Database 的透明資料加密](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database) |
| 設定 Azure SQL 以搭配 Always Encrypted | [SQL Database Always Encrypted Azure Key Vault](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-always-encrypted-azure-key-vault)|

此外 tooTDE，Azure SQL 也支援永遠加密，確保資料會經過加密的新資料加密技術不只在 rest 和在移動資料時用戶端與伺服器之間，也會處於 hello 伺服器上執行命令時使用。

### <a name="any-virtual-machines-must-be-deployed-from-hello-azure-marketplace"></a>任何虛擬機器必須部署的 hello Azure Marketplace
在順序 tooprovide 安全性 AppSource 之間的一致性層級，我們需要經過認證 Cortana 智慧方案的一部分部署任何虛擬機器，並在 hello Azure Marketplace 上發行。

toosearch hello 目前 Azure Marketplace 映像的清單，請參閱[Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute)。

如需如何 toopublish 虛擬機器的映像 Azure Marketplace 資訊，請參閱[指南 toocreate hello Azure Marketplace 的虛擬機器映像](https://docs.microsoft.com/en-us/azure/marketplace-publishing/marketplace-publishing-vm-image-creation)。

## <a name="scalability-evaluation-considerations"></a>延展性評估考量
### <a name="cortana-intelligence-solutions-should-include-a-scalable-big-data-platform"></a>Cortana Intelligence 解決方案應包含一個可調整的巨量資料平台
Cortana 智慧方案應該會調整 toovery 大型的資料大小。 在 Azure 中，這表示它們應該包含其中一個 hello 兩個小數位數 Pb 的資料平台：
- Azure Data Lake Store
- Azure SQL 資料倉儲

如果您的方案不需要支援的這些資料大小，或如果您使用替代的資料平台，請加以解釋 hello 測試案例的理由。
### <a name="cortana-intelligence-solutions-should-include-dedicated-ingestion-data-environments"></a>Cortana Intelligence 解決方案應包含專用的擷取資料環境
Cortana Intelligence 解決方案通常應避免將資料直接插入到關聯式資料來源。 未經處理資料應改為儲存在非結構化環境中，並使用 Azure Data Factory 針對任何關聯式存放區進行等冪插入/更新。

如需使用 Azure Data Factory 複製資料的詳細資訊，請參閱[教學課程：使用 Visual Studio 建立具有複製活動的管線](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-copy-activity-tutorial-using-visual-studio)。

### <a name="azure-sql-data-warehouse-should-use-polybase-for-data-ingestion"></a>Azure SQL 資料倉儲應使用 PolyBase 進行資料擷取
Azure SQL DW 支援 PolyBase 以進行可高度擴充、平行的資料擷取。 PolyBase 可讓您針對外部資料集儲存在 Azure Blob 儲存體或 Azure Data Lake Store toouse Azure SQL DW tooissue 查詢。 這提供更優異的效能的大量更新 tooalternative 方法。

如需開始使用 PolyBase 和 Azure SQL DW 的指示，請參閱[在 SQL 資料倉儲中使用 PolyBase 載入資料](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-get-started-load-with-polybase)。

如需使用 PolyBase 和 Azure SQL DW 的最佳做法詳細資訊，請參閱[在 SQL 資料倉儲中使用 PolyBase 的指南](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide)。

## <a name="availability-evaluation-considerations"></a>可用性評估考量

### <a name="datasets-accessible-tooend-users-should-support-a-large-volume-of-concurrent-users"></a>資料集可存取 tooend 使用者應支援大量的並行使用者
執行時 hello 評估工具，將會詢問 toospecify 任何報告或發行的資源。 系統會假設這些資源是提供給使用者存取，而非開發人員。 這些資源應支援中等/大型數量的並行使用者。

具體而言，Azure SQL 資料倉儲不應該 hello 唯一的資料來源可用 tooend 使用者。 如果 Azure SQL DW Power Users 提供做為資源，Azure Analysis Services 應該成為可用 tootypical 使用者。

如需關於 Azure SQL DW 並行限制的詳細資訊，請參閱 [SQL 資料倉儲中的並行存取和工作負載管理](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-develop-concurrency)。

如需 Azure Analysis Services 的詳細資訊，請參閱 [Analysis Services 概觀](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview)。

### <a name="azure-sql-resources-should-have-a-read-only-replica-for-failover"></a>Azure SQL 資源應該有唯讀複本以供容錯移轉
Azure SQL database 支援異地複寫 tooa 次要執行個體。 這個執行個體可用做為容錯移轉執行個體 tooprovide 高可用性應用程式。

如需 Azure SQL 資料庫異地複寫的詳細資訊，請參閱 [SQL Database 異地複寫概觀](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview)。

如需有關指示 tooconfigure 異地複寫適用於 Azure SQL，請參閱[設定使用 Transact SQL Azure SQL Database 的作用中地理複寫](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-transact-sql)。

### <a name="azure-sql-data-warehouse-should-have-geo-redundant-backups-enabled"></a>Azure SQL 資料倉儲應已啟用異地備援備份
Azure SQL DW 支援每日備份 toogeo 備援儲存體。 此地理複寫可確保您能夠還原 hello 資料倉儲，即使在情況下，您無法存取儲存在主要區域中的快照集。 此功能針對 Cortana Intelligence 解決方案預設為開啟，且不應該停用。

如需 Azure SQL DW 備份和還原的詳細資訊，請參閱 [SQL 資料倉儲備份](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-backups)。

### <a name="virtual-machines-should-be-configured-with-availability-sets"></a>虛擬機器應使用可用性設定組進行設定
應該設定 azure 虛擬機器的計劃性與非計劃性的維護事件順序 toominimize hello 影響的可用性設定組中。

如需有關 Azure 虛擬機器可用性的詳細資訊，請參閱[管理的 Windows Azure 虛擬機器中的 hello 可用性](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability)。

## <a name="other-evaluation-considerations"></a>其他評估考量
### <a name="cortana-intelligence-apps-should-use-a-centralized-tool-for-data-orchestration"></a>Cortana Intelligence 應用程式針對資料協調流程應使用集中式工具
使用單一工具來對資料移動及轉換進行管理和排程，能確保關鍵任務資料的一致性。 它可提供關於重試邏輯、相依性管理，警示/記錄等項目的清楚邏輯。我們建議使用 hello [Azure Data Factory](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-introduction)資料在 Azure 中的協調流程。

如果您針對資料協調流程使用 Azure Data Factory 以外的工具，請說明您使用的是哪些工具。
### <a name="azure-machine-learning-models-should-be-retrained-using-azure-data-factory"></a>Azure Machine Learning 模型應使用 Azure Data Factory 重新訓練
Azure 機器學習 (AzureML) 提供簡單 toouse 工具 hello 建立及部署的預測模型和機器學習管線。 不過，請務必生產部署這些 AzureML 模型不以單一固定資料集為基礎，但改為適應 toohello 移位 dynamics 的真實世界的現象。

如需在 AzureML 中建立重新訓練 Web 服務的詳細資訊，請參閱[以程式設計方式重新訓練機器學習服務模型](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-retrain-models-programmatically)。

如需有關如何自動化使用 Azure Data Factory 的 hello 模型定型程序的詳細資訊，請參閱[更新 Azure 機器學習模型使用的更新資源活動](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-azure-ml-update-resource-activity)。

## <a name="existing-documentation"></a>現有文件
[Microsoft Azure 認證 toogrow 業務 cloud](https://azure.microsoft.com/en-us/marketplace/programs/certified/)

[Microsoft Azure Cortana Intellignece 認證](https://azure.microsoft.com/en-us/marketplace/programs/certified/cortana/)

