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
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="87235-103">資料管理閘道的版本資訊</span><span class="sxs-lookup"><span data-stu-id="87235-103">Release notes for Data Management Gateway</span></span>
<span data-ttu-id="87235-104">Hello 現代資料整合的挑戰之一就是從內部部署 toocloud toomove 資料 tooand。</span><span class="sxs-lookup"><span data-stu-id="87235-104">One of hello challenges for modern data integration is toomove data tooand from on-premises toocloud.</span></span> <span data-ttu-id="87235-105">Data Factory 可讓這項整合與資料管理閘道器，這是代理程式，您可以安裝在內部部署 tooenable 混合資料移動。</span><span class="sxs-lookup"><span data-stu-id="87235-105">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises tooenable hybrid data movement.</span></span>

<span data-ttu-id="87235-106">請參閱下列文章中的資料管理閘道器的詳細資訊的 hello 和如何 toouse 它：</span><span class="sxs-lookup"><span data-stu-id="87235-106">See hello following articles for detailed information about Data Management Gateway and how toouse it:</span></span>

*  [<span data-ttu-id="87235-107">資料管理閘道</span><span class="sxs-lookup"><span data-stu-id="87235-107">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="87235-108">在內部部署和雲端之間使用 Azure Data Factory 移動資料</span><span class="sxs-lookup"><span data-stu-id="87235-108">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a><span data-ttu-id="87235-109">目前版本 (2.10.6347.7)</span><span class="sxs-lookup"><span data-stu-id="87235-109">CURRENT VERSION (2.10.6347.7)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="87235-110">增強功能</span><span class="sxs-lookup"><span data-stu-id="87235-110">Enhancements-</span></span>
- <span data-ttu-id="87235-111">您可以新增 DNS 項目 toowhitelist 服務匯流排，而不是允許清單所有 Azure IP 位址從您的防火牆 （如果需要）。</span><span class="sxs-lookup"><span data-stu-id="87235-111">You can add DNS entries toowhitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="87235-112">您可以在 Azure 入口網站上找到各自的 DNS 項目 (Data Factory-> [製作和部署] -> [閘道] -> [serviceUrls] \(在 JSON 中)</span><span class="sxs-lookup"><span data-stu-id="87235-112">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span></span>
- <span data-ttu-id="87235-113">HDFS 連接器現在支援自我簽署的公開憑證，方法是讓您略過 SSL 驗證。</span><span class="sxs-lookup"><span data-stu-id="87235-113">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span></span>
- <span data-ttu-id="87235-114">已修正︰ 閘道離線 （因為 tooclock 誤差） 更新期間的問題</span><span class="sxs-lookup"><span data-stu-id="87235-114">Fixed: Issue with gateway offline during update (due tooclock skew)</span></span>



## <a name="earlier-versions"></a><span data-ttu-id="87235-115">較早的版本</span><span class="sxs-lookup"><span data-stu-id="87235-115">Earlier versions</span></span>

## <a name="2963132"></a><span data-ttu-id="87235-116">2.9.6313.2</span><span class="sxs-lookup"><span data-stu-id="87235-116">2.9.6313.2</span></span>
### <a name="enhancements-"></a><span data-ttu-id="87235-117">增強功能</span><span class="sxs-lookup"><span data-stu-id="87235-117">Enhancements-</span></span>
-   <span data-ttu-id="87235-118">您可以新增 DNS 項目 toowhitelist 服務匯流排，而不是允許清單所有 Azure IP 位址從您的防火牆 （如果需要）。</span><span class="sxs-lookup"><span data-stu-id="87235-118">You can add DNS entries toowhitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="87235-119">以下提供更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="87235-119">More details here.</span></span>
-   <span data-ttu-id="87235-120">您現在可以複製從向上 too4.75 TB，這是區塊 blob 支援 hello 最大大小的單一區塊 blob 的資料。</span><span class="sxs-lookup"><span data-stu-id="87235-120">You can now copy data to/from a single block blob up too4.75 TB, which is hello max supported size of block blob.</span></span> <span data-ttu-id="87235-121">(之前的上限為 195 GB)。</span><span class="sxs-lookup"><span data-stu-id="87235-121">(earlier limit was 195 GB).</span></span>
-   <span data-ttu-id="87235-122">已修正：在進行複製活動期間將數個較小檔案解壓縮時發生的憶體不足問題。</span><span class="sxs-lookup"><span data-stu-id="87235-122">Fixed: Out of memory issue while unzipping several small files during copy activity.</span></span>
-   <span data-ttu-id="87235-123">已修正︰ 索引超出範圍問題從 文件 DB tooan 複製時發生內部部署 SQL Server 具有等冪性功能。</span><span class="sxs-lookup"><span data-stu-id="87235-123">Fixed: Index out of range issue while copying from Document DB tooan on-premises SQL Server with idempotency feature.</span></span>
-   <span data-ttu-id="87235-124">已修正：來自「複製精靈」的 SQL Server 清除指令碼無法在內部部署 SQL 上運作。</span><span class="sxs-lookup"><span data-stu-id="87235-124">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span></span>
-   <span data-ttu-id="87235-125">已修正︰ 在 hello 結尾空格的資料行名稱不適用於複製活動。</span><span class="sxs-lookup"><span data-stu-id="87235-125">Fixed: Column name with space at hello end does not work in copy activity.</span></span>

## <a name="28662833"></a><span data-ttu-id="87235-126">2.8.66283.3</span><span class="sxs-lookup"><span data-stu-id="87235-126">2.8.66283.3</span></span>
### <a name="enhancements-"></a><span data-ttu-id="87235-127">增強功能</span><span class="sxs-lookup"><span data-stu-id="87235-127">Enhancements-</span></span>
- <span data-ttu-id="87235-128">已修正：在閘道機器重新啟動時發生遺失認證的問題。</span><span class="sxs-lookup"><span data-stu-id="87235-128">Fixed: Issue with missing credentials on gateway machine reboot.</span></span>
- <span data-ttu-id="87235-129">已修正：使用備份檔進行閘道還原時發生的註冊問題。</span><span class="sxs-lookup"><span data-stu-id="87235-129">Fixed: Issue with registration during gateway restore using a backup file.</span></span>


## <a name="2762401"></a><span data-ttu-id="87235-130">2.7.6240.1</span><span class="sxs-lookup"><span data-stu-id="87235-130">2.7.6240.1</span></span>
### <a name="enhancements-"></a><span data-ttu-id="87235-131">增強功能</span><span class="sxs-lookup"><span data-stu-id="87235-131">Enhancements-</span></span>
- <span data-ttu-id="87235-132">已修正：從作為來源的 Oracle 讀取的十進位 Null 值不正確。</span><span class="sxs-lookup"><span data-stu-id="87235-132">Fixed: Incorrect read of Decimal null value from Oracle as source.</span></span>

## <a name="2661922"></a><span data-ttu-id="87235-133">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="87235-133">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="87235-134">新功能</span><span class="sxs-lookup"><span data-stu-id="87235-134">What’s new</span></span>
- <span data-ttu-id="87235-135">客戶可以提供關於閘道註冊體驗的意見。</span><span class="sxs-lookup"><span data-stu-id="87235-135">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="87235-136">支援新的壓縮格式︰ZIP (Deflate)</span><span class="sxs-lookup"><span data-stu-id="87235-136">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="87235-137">增強功能</span><span class="sxs-lookup"><span data-stu-id="87235-137">Enhancements-</span></span>
- <span data-ttu-id="87235-138">改善 Oracle 接收、HDFS 來源的效能。</span><span class="sxs-lookup"><span data-stu-id="87235-138">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="87235-139">針對閘道自動更新、閘道平行處理容量進行錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="87235-139">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="87235-140">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="87235-140">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="87235-141">增強功能</span><span class="sxs-lookup"><span data-stu-id="87235-141">Enhancements</span></span>
- <span data-ttu-id="87235-142">改善且更為穩固閘道註冊體驗-現在您可以在 hello 閘道註冊過程中，讓 hello 註冊體驗更能有效回應追蹤進度狀態。</span><span class="sxs-lookup"><span data-stu-id="87235-142">Improved and more robust Gateway registration experience- Now you can track progress status during hello Gateway registration process, which makes hello registration experience more responsive.</span></span>
- <span data-ttu-id="87235-143">改進的閘道還原程序-您仍然可以復原閘道，即使您沒有安裝此更新後 hello 閘道備份檔案。</span><span class="sxs-lookup"><span data-stu-id="87235-143">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have hello gateway backup file with this update.</span></span> <span data-ttu-id="87235-144">這會需要您在入口網站的 tooreset 連結的服務認證。</span><span class="sxs-lookup"><span data-stu-id="87235-144">This would require you tooreset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="87235-145">錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="87235-145">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="87235-146">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="87235-146">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="87235-147">新功能</span><span class="sxs-lookup"><span data-stu-id="87235-147">What’s new</span></span>

- <span data-ttu-id="87235-148">您現在可以在本機上儲存資料來源認證。</span><span class="sxs-lookup"><span data-stu-id="87235-148">You can now store data source credentials locally.</span></span> <span data-ttu-id="87235-149">hello 認證會加密。</span><span class="sxs-lookup"><span data-stu-id="87235-149">hello credentials are encrypted.</span></span> <span data-ttu-id="87235-150">hello 資料來源認證可以復原並使用可以從現有的閘道，所有在內部部署的 hello 匯出的 hello 備份檔案還原。</span><span class="sxs-lookup"><span data-stu-id="87235-150">hello data source credentials can be recovered and restored using hello backup file that can be exported from hello existing Gateway, all on-premises.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="87235-151">增強功能</span><span class="sxs-lookup"><span data-stu-id="87235-151">Enhancements-</span></span>

- <span data-ttu-id="87235-152">改良和更強大的閘道註冊體驗。</span><span class="sxs-lookup"><span data-stu-id="87235-152">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="87235-153">支援在複製精靈中，文字格式的 QuoteChar 組態自動偵測和改善 hello 整體格式化偵測的精確度。</span><span class="sxs-lookup"><span data-stu-id="87235-153">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve hello overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="87235-154">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="87235-154">2.3.6100.2</span></span>

- <span data-ttu-id="87235-155">複製精靈中支援 firstRowAsHeader 和 SkipLineCount 自動偵測內部部署檔案系統和 HDFS 中是否有文字檔案。</span><span class="sxs-lookup"><span data-stu-id="87235-155">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="87235-156">增強閘道與服務匯流排之間的網路連線的 hello 的穩定性</span><span class="sxs-lookup"><span data-stu-id="87235-156">Enhance hello stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="87235-157">修正幾個錯誤。</span><span class="sxs-lookup"><span data-stu-id="87235-157">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="87235-158">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="87235-158">2.2.6072.1</span></span>

*  <span data-ttu-id="87235-159">設定 HTTP proxy 使用 hello 閘道組態管理員中的 hello 閘道支援。</span><span class="sxs-lookup"><span data-stu-id="87235-159">Supports setting HTTP proxy for hello gateway using hello Gateway Configuration Manager.</span></span> <span data-ttu-id="87235-160">如果有設定，就會透過 HTTP Proxy 來存取 Azure Blob、「Azure 資料表」、Azure Data Lake 及 DocumentDB。</span><span class="sxs-lookup"><span data-stu-id="87235-160">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="87235-161">支援的標頭複製資料時，處理 TextFormat tooAzure Blob、 Azure 資料湖存放區，在內部部署檔案系統中，並在內部部署 HDFS。</span><span class="sxs-lookup"><span data-stu-id="87235-161">Supports header handling for TextFormat when copying data from/tooAzure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="87235-162">支援的資料複製附加 Blob 和分頁 Blob hello 以及已在支援區塊 Blob。</span><span class="sxs-lookup"><span data-stu-id="87235-162">Supports copying data from Append Blob and Page Blob along with hello already supported Block Blob.</span></span>
*  <span data-ttu-id="87235-163">導入了新的閘道狀態**線上 （有限制）**，除了複製精靈 」 的 hello 互動作業支援表示 hello hello 閘道的主要功能運作。</span><span class="sxs-lookup"><span data-stu-id="87235-163">Introduces a new gateway status **Online (Limited)**, which indicates that hello main functionality of hello gateway works except hello interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="87235-164">增強 hello 強固性的閘道註冊使用註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="87235-164">Enhances hello robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="87235-165">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="87235-165">2.1.6040.</span></span>

*  <span data-ttu-id="87235-166">DB2 驅動程式現在包含在 hello 閘道安裝套件。</span><span class="sxs-lookup"><span data-stu-id="87235-166">DB2 driver is included in hello gateway installation package now.</span></span> <span data-ttu-id="87235-167">您不需要 tooinstall 它分開。</span><span class="sxs-lookup"><span data-stu-id="87235-167">You do not need tooinstall it separately.</span></span>
*  <span data-ttu-id="87235-168">DB2 驅動程式現在支援 z/OS 和 DB2 for 我 (AS / 400) 以及 hello 支援平台已 （Linux、 Unix 和 Windows）。</span><span class="sxs-lookup"><span data-stu-id="87235-168">DB2 driver now supports z/OS and DB2 for i (AS/400) along with hello platforms already supported (Linux, Unix, and Windows).</span></span>
*  <span data-ttu-id="87235-169">支援使用 Azure Cosmos DB 作為內部部署資料存放區的來源或目的地</span><span class="sxs-lookup"><span data-stu-id="87235-169">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="87235-170">支援已複製的資料從/toocold/熱 blob 儲存體，以及 hello 支援一般用途儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="87235-170">Supports copying data from/toocold/hot blob storage along with hello already supported general-purpose storage account.</span></span>
*  <span data-ttu-id="87235-171">可讓您 tooconnect tooon 內部部署 SQL Server 透過閘道與遠端登入權限。</span><span class="sxs-lookup"><span data-stu-id="87235-171">Allows you tooconnect tooon-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="87235-172">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="87235-172">2.0.6013.1</span></span>

*  <span data-ttu-id="87235-173">您可以選取 hello 語言/文化特性 toobe 閘道會在手動安裝期間使用。</span><span class="sxs-lookup"><span data-stu-id="87235-173">You can select hello language/culture toobe used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="87235-174">當閘道無法如預期運作時，您可以選擇 toosend 閘道記錄檔的最後七天 tooMicrosoft toofacilitate 疑難排解的 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="87235-174">When gateway does not work as expected, you can choose toosend gateway logs of last seven days tooMicrosoft toofacilitate troubleshooting of hello issue.</span></span> <span data-ttu-id="87235-175">如果不是閘道已連線 toohello 雲端服務，您可以選擇 toosave 並封存閘道記錄檔。</span><span class="sxs-lookup"><span data-stu-id="87235-175">If gateway is not connected toohello cloud service, you can choose toosave and archive gateway logs.</span></span>  

*  <span data-ttu-id="87235-176">閘道器組態管理員的使用者介面增強功能：</span><span class="sxs-lookup"><span data-stu-id="87235-176">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="87235-177">Hello 首頁 索引標籤上進行閘道狀態更明顯可見。</span><span class="sxs-lookup"><span data-stu-id="87235-177">Make gateway status more visible on hello Home tab.</span></span>

    *  <span data-ttu-id="87235-178">重新組織並簡化控制項。</span><span class="sxs-lookup"><span data-stu-id="87235-178">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="87235-179">您可以將資料複製從儲存體使用 hello[程式碼自由複製預覽工具](data-factory-copy-data-wizard-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="87235-179">You can copy data from a storage using hello [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="87235-180">如需此功能的一般詳細資料，請參閱 [分段複製](data-factory-copy-activity-performance.md#staged-copy) 。</span><span class="sxs-lookup"><span data-stu-id="87235-180">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span>
*  <span data-ttu-id="87235-181">您可以使用資料管理閘道器 tooingress 資料直接從內部部署 SQL Server 資料庫到 Azure 機器學習。</span><span class="sxs-lookup"><span data-stu-id="87235-181">You can use Data Management Gateway tooingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="87235-182">效能改進</span><span class="sxs-lookup"><span data-stu-id="87235-182">Performance improvements</span></span>

    * <span data-ttu-id="87235-183">在無程式碼複製預覽工具中，改進對於 SQL Server 檢視結構描述或預覽的效能。</span><span class="sxs-lookup"><span data-stu-id="87235-183">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="87235-184">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="87235-184">1.12.5953.1</span></span>

*  <span data-ttu-id="87235-185">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="87235-185">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="87235-186">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="87235-186">1.11.5918.1</span></span>

*  <span data-ttu-id="87235-187">Hello 閘道事件記錄檔的大小上限已增加 1 MB too40 mb。</span><span class="sxs-lookup"><span data-stu-id="87235-187">Maximum size of hello gateway event log has been increased from 1 MB too40 MB.</span></span>

*  <span data-ttu-id="87235-188">如果在閘道自動更新期間必須重新啟動，則會顯示警告對話方塊。</span><span class="sxs-lookup"><span data-stu-id="87235-188">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="87235-189">然後或更新版本，您可以選擇 toorestart 權限。</span><span class="sxs-lookup"><span data-stu-id="87235-189">You can choose toorestart right then or later.</span></span>

*  <span data-ttu-id="87235-190">如果自動更新失敗，閘道安裝程式最多會重試自動更新 3 次。</span><span class="sxs-lookup"><span data-stu-id="87235-190">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="87235-191">效能改進</span><span class="sxs-lookup"><span data-stu-id="87235-191">Performance improvements</span></span>

    * <span data-ttu-id="87235-192">改善無程式碼複製案例中從內部部署伺服器載入大型資料表的效能。</span><span class="sxs-lookup"><span data-stu-id="87235-192">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="87235-193">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="87235-193">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="87235-194">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="87235-194">1.10.5892.1</span></span>

*  <span data-ttu-id="87235-195">效能改進</span><span class="sxs-lookup"><span data-stu-id="87235-195">Performance improvements</span></span>

*  <span data-ttu-id="87235-196">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="87235-196">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="87235-197">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="87235-197">1.9.5865.2</span></span>

*  <span data-ttu-id="87235-198">零接觸自動更新功能</span><span class="sxs-lookup"><span data-stu-id="87235-198">Zero touch auto update capability</span></span>
*  <span data-ttu-id="87235-199">閘道狀態指示器的新系統匣圖示</span><span class="sxs-lookup"><span data-stu-id="87235-199">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="87235-200">能力太 「 更新現在 」 從 hello 用戶端</span><span class="sxs-lookup"><span data-stu-id="87235-200">Ability too“Update now” from hello client</span></span>
*  <span data-ttu-id="87235-201">能力 tooset 更新排程時間</span><span class="sxs-lookup"><span data-stu-id="87235-201">Ability tooset update schedule time</span></span>
*  <span data-ttu-id="87235-202">用來開啟/關閉自動更新的 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="87235-202">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="87235-203">JSON 格式支援</span><span class="sxs-lookup"><span data-stu-id="87235-203">Support for JSON format</span></span>  
*  <span data-ttu-id="87235-204">效能改進</span><span class="sxs-lookup"><span data-stu-id="87235-204">Performance improvements</span></span>
*  <span data-ttu-id="87235-205">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="87235-205">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="87235-206">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="87235-206">1.8.5822.1</span></span>

*  <span data-ttu-id="87235-207">改善疑難排解體驗</span><span class="sxs-lookup"><span data-stu-id="87235-207">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="87235-208">效能改進</span><span class="sxs-lookup"><span data-stu-id="87235-208">Performance improvements</span></span>
*  <span data-ttu-id="87235-209">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="87235-209">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="87235-210">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="87235-210">1.7.5795.1</span></span>

*  <span data-ttu-id="87235-211">效能改進</span><span class="sxs-lookup"><span data-stu-id="87235-211">Performance improvements</span></span>
*  <span data-ttu-id="87235-212">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="87235-212">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="87235-213">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="87235-213">1.7.5764.1</span></span>

*  <span data-ttu-id="87235-214">效能改進</span><span class="sxs-lookup"><span data-stu-id="87235-214">Performance improvements</span></span>
*  <span data-ttu-id="87235-215">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="87235-215">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="87235-216">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="87235-216">1.6.5735.1</span></span>

*  <span data-ttu-id="87235-217">支援內部部署 HDFS 來源/接收器</span><span class="sxs-lookup"><span data-stu-id="87235-217">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="87235-218">效能改進</span><span class="sxs-lookup"><span data-stu-id="87235-218">Performance improvements</span></span>
*  <span data-ttu-id="87235-219">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="87235-219">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="87235-220">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="87235-220">1.6.5696.1</span></span>

*  <span data-ttu-id="87235-221">效能改進</span><span class="sxs-lookup"><span data-stu-id="87235-221">Performance improvements</span></span>
*  <span data-ttu-id="87235-222">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="87235-222">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="87235-223">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="87235-223">1.6.5676.1</span></span>

*  <span data-ttu-id="87235-224">在組態管理員上支援診斷工具</span><span class="sxs-lookup"><span data-stu-id="87235-224">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="87235-225">支援 Azure Data Factory 表格式資料來源的資料表資料行</span><span class="sxs-lookup"><span data-stu-id="87235-225">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="87235-226">針對 Azure Data Factory 支援 SQL DW</span><span class="sxs-lookup"><span data-stu-id="87235-226">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="87235-227">針對 Azure Data Factory 支援 BlobSource 和 FileSource 的 Reclusive</span><span class="sxs-lookup"><span data-stu-id="87235-227">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="87235-228">針對 Azure Data Factory 支援 BlobSink 和 FileSink 中與「二進位複製」相關的 CopyBehavior - MergeFiles、PreserveHierarchy 及 FlattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="87235-228">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="87235-229">針對 Azure Data Factory 支援複製活動報告進度</span><span class="sxs-lookup"><span data-stu-id="87235-229">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="87235-230">針對 Azure Data Factory 支援資料來源連線驗證</span><span class="sxs-lookup"><span data-stu-id="87235-230">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="87235-231">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="87235-231">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="87235-232">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="87235-232">1.6.5672.1</span></span>

*  <span data-ttu-id="87235-233">針對 Azure Data Factory 支援 ODBC 資料來源的資料表名稱</span><span class="sxs-lookup"><span data-stu-id="87235-233">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="87235-234">效能改進</span><span class="sxs-lookup"><span data-stu-id="87235-234">Performance improvements</span></span>
*  <span data-ttu-id="87235-235">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="87235-235">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="87235-236">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="87235-236">1.6.5658.1</span></span>

*  <span data-ttu-id="87235-237">針對 Azure Data Factory 支援檔案接收</span><span class="sxs-lookup"><span data-stu-id="87235-237">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="87235-238">針對 Azure Data Factory 在二進位複製中支援保留階層</span><span class="sxs-lookup"><span data-stu-id="87235-238">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="87235-239">針對 Azure Data Factory 支援複製活動等冪性</span><span class="sxs-lookup"><span data-stu-id="87235-239">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="87235-240">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="87235-240">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="87235-241">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="87235-241">1.6.5640.1</span></span>

*  <span data-ttu-id="87235-242">針對 Azure Data Factory 另外支援 3 種資料來源 (ODBC、OData、HDFS)</span><span class="sxs-lookup"><span data-stu-id="87235-242">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="87235-243">針對 Azure Data Factory 在 csv 剖析器中支援引號字元</span><span class="sxs-lookup"><span data-stu-id="87235-243">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="87235-244">壓縮支援 (BZip2)</span><span class="sxs-lookup"><span data-stu-id="87235-244">Compression support (BZip2)</span></span>
*  <span data-ttu-id="87235-245">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="87235-245">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="87235-246">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="87235-246">1.5.5612.1</span></span>

*  <span data-ttu-id="87235-247">針對 Azure Data Factory 支援 5 種關聯式資料庫 (MySQL、PostgreSQL、DB2、Teradata 和 Sybase)</span><span class="sxs-lookup"><span data-stu-id="87235-247">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="87235-248">壓縮支援 (Gzip 和 Deflate)</span><span class="sxs-lookup"><span data-stu-id="87235-248">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="87235-249">效能改進</span><span class="sxs-lookup"><span data-stu-id="87235-249">Performance improvements</span></span>
*  <span data-ttu-id="87235-250">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="87235-250">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="87235-251">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="87235-251">1.4.5549.1</span></span>

*  <span data-ttu-id="87235-252">針對 Azure Data Factory 新增 Oracle 資料來源支援</span><span class="sxs-lookup"><span data-stu-id="87235-252">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="87235-253">效能改進</span><span class="sxs-lookup"><span data-stu-id="87235-253">Performance improvements</span></span>
*  <span data-ttu-id="87235-254">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="87235-254">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="87235-255">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="87235-255">1.4.5492.1</span></span>

*  <span data-ttu-id="87235-256">支援 Microsoft Azure Data Factory 和 Office 365 Power BI 服務的統一二進位檔</span><span class="sxs-lookup"><span data-stu-id="87235-256">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="87235-257">精簡 hello 組態 UI 和註冊程序</span><span class="sxs-lookup"><span data-stu-id="87235-257">Refine hello Configuration UI and registration process</span></span>
*  <span data-ttu-id="87235-258">Azure Data Factory - 針對 SQL Server 資料來源的 Azure 輸入和輸出支援</span><span class="sxs-lookup"><span data-stu-id="87235-258">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="87235-259">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="87235-259">1.2.5303.1</span></span>

*  <span data-ttu-id="87235-260">修正逾時問題 toosupport 更耗時的資料來源連接。</span><span class="sxs-lookup"><span data-stu-id="87235-260">Fix timeout issue toosupport more time-consuming data source connections.</span></span>

### <a name="1155268"></a><span data-ttu-id="87235-261">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="87235-261">1.1.5526.8</span></span>

*  <span data-ttu-id="87235-262">在設定期間，必要條件是需要 .NET Framework 4.5.1。</span><span class="sxs-lookup"><span data-stu-id="87235-262">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="87235-263">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="87235-263">1.0.5144.2</span></span>

*  <span data-ttu-id="87235-264">沒有任何會影響 Azure Data Factory 案例的變更。</span><span class="sxs-lookup"><span data-stu-id="87235-264">No changes that affect Azure Data Factory scenarios.</span></span>
