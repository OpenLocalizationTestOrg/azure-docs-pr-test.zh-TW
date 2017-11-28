---
title: "資料庫待用加密：Azure Cosmos DB | Microsoft Docs"
description: "了解 Azure Cosmos DB 如何提供所有資料的預設加密。"
services: cosmos-db
author: voellm
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 99725c52-d7ca-4bfa-888b-19b1569754d3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: voellm
ms.openlocfilehash: d52d55fe45fdd18394166ec7ccd6e46e8f8f434b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-encryption-at-rest"></a><span data-ttu-id="8a593-103">Azure Cosmos DB 資料庫待用加密</span><span class="sxs-lookup"><span data-stu-id="8a593-103">Azure Cosmos DB database encryption at rest</span></span>

<span data-ttu-id="8a593-104">靜態加密是片語時，通常是指 toohello 加密非動態儲存裝置上的資料，例如固態磁碟機 (Ssd) 和硬碟 (Hdd)。</span><span class="sxs-lookup"><span data-stu-id="8a593-104">Encryption at rest is a phrase that commonly refers toohello encryption of data on nonvolatile storage devices, such as solid state drives (SSDs) and hard disk drives (HDDs).</span></span> <span data-ttu-id="8a593-105">Cosmos DB 會在 SSD 上儲存其主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="8a593-105">Cosmos DB stores its primary databases on SSDs.</span></span> <span data-ttu-id="8a593-106">其媒體附件和備份會儲存在通常由 HDD 備份的 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="8a593-106">Its media attachments and backups are stored in Azure Blob storage, which is generally backed up by HDDs.</span></span> <span data-ttu-id="8a593-107">Hello Cosmos db 靜止的加密版本會加密所有您的資料庫、 媒體附件和備份。</span><span class="sxs-lookup"><span data-stu-id="8a593-107">With hello release of encryption at rest for Cosmos DB, all your databases, media attachments, and backups are encrypted.</span></span> <span data-ttu-id="8a593-108">您的資料現在在傳輸過程中加密 （透過 hello 網路），並在靜止 （靜態儲存體），讓您端對端加密。</span><span class="sxs-lookup"><span data-stu-id="8a593-108">Your data is now encrypted in transit (over hello network) and at rest (nonvolatile storage), giving you end-to-end encryption.</span></span>

<span data-ttu-id="8a593-109">您可以非常輕易 toouse PaaS 服務，Cosmos DB 原狀。</span><span class="sxs-lookup"><span data-stu-id="8a593-109">As a PaaS service, Cosmos DB is very easy toouse.</span></span> <span data-ttu-id="8a593-110">因為儲存 Cosmos DB 中的所有使用者資料已都加密待用和傳輸中，您不需要 tootake 任何動作。</span><span class="sxs-lookup"><span data-stu-id="8a593-110">Because all user data stored in Cosmos DB is encrypted at rest and in transport, you don't have tootake any action.</span></span> <span data-ttu-id="8a593-111">這是在加密的另一個方式 tooput 其餘部分是 「 on 」 預設。</span><span class="sxs-lookup"><span data-stu-id="8a593-111">Another way tooput this is that encryption at rest is "on" by default.</span></span> <span data-ttu-id="8a593-112">不有任何控制項 tooturn 它關閉或開啟。</span><span class="sxs-lookup"><span data-stu-id="8a593-112">There are no controls tooturn it off or on.</span></span> <span data-ttu-id="8a593-113">我們會提供這項功能，我們會持續 toomeet 我們[效能和可用性的 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db)。</span><span class="sxs-lookup"><span data-stu-id="8a593-113">We provide this feature while we continue toomeet our [availability and performance SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db).</span></span>

## <a name="implement-encryption-at-rest"></a><span data-ttu-id="8a593-114">實作待用加密</span><span class="sxs-lookup"><span data-stu-id="8a593-114">Implement encryption at rest</span></span>

<span data-ttu-id="8a593-115">待用加密是使用數種安全性技術來實作的，這些技術包括安全金鑰儲存體系統、加密的網路，以及密碼編譯 API。</span><span class="sxs-lookup"><span data-stu-id="8a593-115">Encryption at rest is implemented by using a number of security technologies, including secure key storage systems, encrypted networks, and cryptographic APIs.</span></span> <span data-ttu-id="8a593-116">解密及處理資料的系統有 toocommunicate 的系統管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="8a593-116">Systems that decrypt and process data have toocommunicate with systems that manage keys.</span></span> <span data-ttu-id="8a593-117">hello 圖表會顯示儲存體加密的資料與 hello 管理的索引鍵分隔的方式。</span><span class="sxs-lookup"><span data-stu-id="8a593-117">hello diagram shows how storage of encrypted data and hello management of keys is separated.</span></span> 

![設計圖表](./media/database-encryption-at-rest/design-diagram.png)

<span data-ttu-id="8a593-119">使用者要求的 hello 基本流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="8a593-119">hello basic flow of a user request is as follows:</span></span>
- <span data-ttu-id="8a593-120">hello 使用者資料庫的帳戶會成為準備好，並透過要求 toohello 管理服務資源提供者擷取儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="8a593-120">hello user database account is made ready, and storage keys are retrieved via a request toohello Management Service Resource Provider.</span></span>
- <span data-ttu-id="8a593-121">使用者建立透過 HTTPS/安全傳輸的連線 tooCosmos DB。</span><span class="sxs-lookup"><span data-stu-id="8a593-121">A user creates a connection tooCosmos DB via HTTPS/secure transport.</span></span> <span data-ttu-id="8a593-122">（Sdk 抽象 hello 詳細資料的 hello）。</span><span class="sxs-lookup"><span data-stu-id="8a593-122">(hello SDKs abstract hello details.)</span></span>
- <span data-ttu-id="8a593-123">hello 使用者傳送 JSON 文件 toobe 儲存一段 hello 先前建立安全連線。</span><span class="sxs-lookup"><span data-stu-id="8a593-123">hello user sends a JSON document toobe stored over hello previously created secure connection.</span></span>
- <span data-ttu-id="8a593-124">hello JSON 文件會編製索引，除非 hello 使用者已關閉的索引。</span><span class="sxs-lookup"><span data-stu-id="8a593-124">hello JSON document is indexed unless hello user has turned off indexing.</span></span>
- <span data-ttu-id="8a593-125">Hello JSON 文件和索引資料會寫入 toosecure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="8a593-125">Both hello JSON document and index data are written toosecure storage.</span></span>
- <span data-ttu-id="8a593-126">定期從 hello 安全儲存體讀取資料及備份 toohello Azure 加密 Blob 存放區。</span><span class="sxs-lookup"><span data-stu-id="8a593-126">Periodically, data is read from hello secure storage and backed up toohello Azure Encrypted Blob Store.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="8a593-127">常見問題集</span><span class="sxs-lookup"><span data-stu-id="8a593-127">Frequently asked questions</span></span>

### <a name="q-how-much-more-does-azure-storage-cost-if-storage-service-encryption-is-enabled"></a><span data-ttu-id="8a593-128">問︰如果已啟用儲存體服務加密，Azure 儲存體的成本會多出多少？</span><span class="sxs-lookup"><span data-stu-id="8a593-128">Q: How much more does Azure Storage cost if Storage Service Encryption is enabled?</span></span>
<span data-ttu-id="8a593-129">答：沒有任何額外成本。</span><span class="sxs-lookup"><span data-stu-id="8a593-129">A: There is no additional cost.</span></span>

### <a name="q-who-manages-hello-encryption-keys"></a><span data-ttu-id="8a593-130">問： 誰管理 hello 加密金鑰？</span><span class="sxs-lookup"><span data-stu-id="8a593-130">Q: Who manages hello encryption keys?</span></span>
<span data-ttu-id="8a593-131">答： hello 金鑰是由 Microsoft 管理。</span><span class="sxs-lookup"><span data-stu-id="8a593-131">A: hello keys are managed by Microsoft.</span></span>

### <a name="q-how-often-are-encryption-keys-rotated"></a><span data-ttu-id="8a593-132">問︰加密金鑰多久輪替一次？</span><span class="sxs-lookup"><span data-stu-id="8a593-132">Q: How often are encryption keys rotated?</span></span>
<span data-ttu-id="8a593-133">答：Microsoft 針對加密金鑰輪替有一套 Cosmos DB 會遵循的內部方針。</span><span class="sxs-lookup"><span data-stu-id="8a593-133">A: Microsoft has a set of internal guidelines for encryption key rotation, which Cosmos DB follows.</span></span> <span data-ttu-id="8a593-134">不會發行 hello 的特定指導方針。</span><span class="sxs-lookup"><span data-stu-id="8a593-134">hello specific guidelines are not published.</span></span> <span data-ttu-id="8a593-135">Microsoft 並未發行 hello[安全性開發週期 (SDL)](https://www.microsoft.com/sdl/default.aspx)，被視為是子集內部的指引以及開發人員已經很有用的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="8a593-135">Microsoft does publish hello [Security Development Lifecycle (SDL)](https://www.microsoft.com/sdl/default.aspx), which is seen as a subset of internal guidance and has useful best practices for developers.</span></span>

### <a name="q-can-i-use-my-own-encryption-keys"></a><span data-ttu-id="8a593-136">問︰我是否可以使用自己的加密金鑰？</span><span class="sxs-lookup"><span data-stu-id="8a593-136">Q: Can I use my own encryption keys?</span></span>
<span data-ttu-id="8a593-137">答： cosmos DB 是 PaaS 服務，且我們致力硬 tookeep hello 服務簡單 toouse。</span><span class="sxs-lookup"><span data-stu-id="8a593-137">A: Cosmos DB is a PaaS service, and we worked hard tookeep hello service easy toouse.</span></span> <span data-ttu-id="8a593-138">我們注意到會詢問此問題的使用者，通常是想詢問有關符合如 PCI-DSS 等合規性需求的 Proxy 問題。</span><span class="sxs-lookup"><span data-stu-id="8a593-138">We've noticed this question is often asked as a proxy question for meeting a compliance requirement like PCI-DSS.</span></span> <span data-ttu-id="8a593-139">建立這項功能的一部分，我們致力與相容性稽核員 tooensure 使用 Cosmos DB 客戶符合其需求沒有 hello 需要 toomanage 金鑰本身。</span><span class="sxs-lookup"><span data-stu-id="8a593-139">As part of building this feature, we worked with compliance auditors tooensure that customers who use Cosmos DB meet their requirements without hello need toomanage keys themselves.</span></span>
<span data-ttu-id="8a593-140">如此一來，我們目前不提供使用者 hello 選項 tooburden 本身與金鑰管理。</span><span class="sxs-lookup"><span data-stu-id="8a593-140">As a result, we currently do not offer users hello option tooburden themselves with key management.</span></span>

### <a name="q-what-regions-have-encryption-turned-on"></a><span data-ttu-id="8a593-141">問：有哪些區域已開啟加密？</span><span class="sxs-lookup"><span data-stu-id="8a593-141">Q: What regions have encryption turned on?</span></span>
<span data-ttu-id="8a593-142">答：所有的 Azure Cosmos DB 區域皆已針對所有使用者資料開啟加密。</span><span class="sxs-lookup"><span data-stu-id="8a593-142">A: All Azure Cosmos DB regions have encryption turned on for all user data.</span></span>

### <a name="q-does-encryption-affect-hello-performance-latency-and-throughput-slas"></a><span data-ttu-id="8a593-143">問： 沒有加密會影響 hello 效能延遲和輸送量的 Sla 嗎？</span><span class="sxs-lookup"><span data-stu-id="8a593-143">Q: Does encryption affect hello performance latency and throughput SLAs?</span></span>
<span data-ttu-id="8a593-144">答： 沒有任何影響或變更 toohello 效能 Sla 現在，所有現有和新的帳戶已啟用靜態加密。</span><span class="sxs-lookup"><span data-stu-id="8a593-144">A: There is no impact or changes toohello performance SLAs now that encryption at rest is enabled for all existing and new accounts.</span></span> <span data-ttu-id="8a593-145">閱讀更多在 hello [SLA Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db)頁面 toosee hello 最新的保證。</span><span class="sxs-lookup"><span data-stu-id="8a593-145">You can read more on hello [SLA for Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db) page toosee hello latest guarantees.</span></span>

### <a name="q-does-hello-local-emulator-support-encryption-at-rest"></a><span data-ttu-id="8a593-146">問： hello 本機模擬器，可支援靜態加密？</span><span class="sxs-lookup"><span data-stu-id="8a593-146">Q: Does hello local emulator support encryption at rest?</span></span>
<span data-ttu-id="8a593-147">答： hello 模擬器是獨立的開發/測試工具，並不會使用 hello hello managed 的 Cosmos DB 服務所使用的金鑰管理服務。</span><span class="sxs-lookup"><span data-stu-id="8a593-147">A: hello emulator is a standalone dev/test tool and does not use hello key management services that hello managed Cosmos DB service uses.</span></span> <span data-ttu-id="8a593-148">我們建議您儲存機密模擬器測試資料的磁碟機上的 tooenable BitLocker。</span><span class="sxs-lookup"><span data-stu-id="8a593-148">Our recommendation is tooenable BitLocker on drives where you are storing sensitive emulator test data.</span></span> <span data-ttu-id="8a593-149">hello[模擬器支援將變更 hello 預設資料目錄](local-emulator.md)也可使用的已知位置。</span><span class="sxs-lookup"><span data-stu-id="8a593-149">hello [emulator supports changing hello default data directory](local-emulator.md) as well as using a well-known location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a593-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8a593-150">Next steps</span></span>

<span data-ttu-id="8a593-151">如需 Cosmos DB 安全性和 hello 最新的增強功能的概觀，請參閱[Azure Cosmos DB 資料庫安全性](database-security.md)。</span><span class="sxs-lookup"><span data-stu-id="8a593-151">For an overview of Cosmos DB security and hello latest improvements, see [Azure Cosmos DB database security](database-security.md).</span></span>
<span data-ttu-id="8a593-152">如需有關 Microsoft 認證的詳細資訊，請參閱 hello [Azure 信任中心](https://azure.microsoft.com/en-us/support/trust-center/)。</span><span class="sxs-lookup"><span data-stu-id="8a593-152">For more information about Microsoft certifications, see hello [Azure Trust Center](https://azure.microsoft.com/en-us/support/trust-center/).</span></span>
