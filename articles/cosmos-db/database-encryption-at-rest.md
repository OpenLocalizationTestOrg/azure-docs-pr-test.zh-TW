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
ms.openlocfilehash: d8967d4504a8ccabb444c7f3d5635e2d00f287c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-database-encryption-at-rest"></a><span data-ttu-id="ad5f1-103">Azure Cosmos DB 資料庫待用加密</span><span class="sxs-lookup"><span data-stu-id="ad5f1-103">Azure Cosmos DB database encryption at rest</span></span>

<span data-ttu-id="ad5f1-104">「待用加密」是一個用來描述加密靜態儲存裝置 (例如固態硬碟 (SSD) 和硬碟 (HDD)) 上資料的常見用語。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-104">Encryption at rest is a phrase that commonly refers to the encryption of data on nonvolatile storage devices, such as solid state drives (SSDs) and hard disk drives (HDDs).</span></span> <span data-ttu-id="ad5f1-105">Cosmos DB 會在 SSD 上儲存其主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-105">Cosmos DB stores its primary databases on SSDs.</span></span> <span data-ttu-id="ad5f1-106">其媒體附件和備份會儲存在通常由 HDD 備份的 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-106">Its media attachments and backups are stored in Azure Blob storage, which is generally backed up by HDDs.</span></span> <span data-ttu-id="ad5f1-107">在針對 Cosmos DB 發行待用加密之後，您所有的資料庫、媒體附件及備份都會進行加密。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-107">With the release of encryption at rest for Cosmos DB, all your databases, media attachments, and backups are encrypted.</span></span> <span data-ttu-id="ad5f1-108">您的資料現在會在傳輸過程 (透過網路) 和待用 (位於靜態儲存裝置上) 期間進行加密，提供您端對端的加密。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-108">Your data is now encrypted in transit (over the network) and at rest (nonvolatile storage), giving you end-to-end encryption.</span></span>

<span data-ttu-id="ad5f1-109">Cosmos DB 是一種 PaaS 服務，使用起來非常容易。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-109">As a PaaS service, Cosmos DB is very easy to use.</span></span> <span data-ttu-id="ad5f1-110">由於儲存在 Cosmos DB 中的所有使用者資料都會在待用和傳輸過程期間進行加密，因此您不必採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-110">Because all user data stored in Cosmos DB is encrypted at rest and in transport, you don't have to take any action.</span></span> <span data-ttu-id="ad5f1-111">換句話說，待用加密預設便會「開啟」。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-111">Another way to put this is that encryption at rest is "on" by default.</span></span> <span data-ttu-id="ad5f1-112">沒有關閉或開啟的控制項。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-112">There are no controls to turn it off or on.</span></span> <span data-ttu-id="ad5f1-113">在提供這項功能的同時，我們會繼續符合[可用性和效能 SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db)。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-113">We provide this feature while we continue to meet our [availability and performance SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db).</span></span>

## <a name="implement-encryption-at-rest"></a><span data-ttu-id="ad5f1-114">實作待用加密</span><span class="sxs-lookup"><span data-stu-id="ad5f1-114">Implement encryption at rest</span></span>

<span data-ttu-id="ad5f1-115">待用加密是使用數種安全性技術來實作的，這些技術包括安全金鑰儲存體系統、加密的網路，以及密碼編譯 API。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-115">Encryption at rest is implemented by using a number of security technologies, including secure key storage systems, encrypted networks, and cryptographic APIs.</span></span> <span data-ttu-id="ad5f1-116">負責解密及處理資料的系統，必須和負責管理金鑰的系統進行通訊。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-116">Systems that decrypt and process data have to communicate with systems that manage keys.</span></span> <span data-ttu-id="ad5f1-117">下圖顯示加密資料儲存體和金鑰管理的分隔方式。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-117">The diagram shows how storage of encrypted data and the management of keys is separated.</span></span> 

![設計圖表](./media/database-encryption-at-rest/design-diagram.png)

<span data-ttu-id="ad5f1-119">使用者要求的基本流程如下：</span><span class="sxs-lookup"><span data-stu-id="ad5f1-119">The basic flow of a user request is as follows:</span></span>
- <span data-ttu-id="ad5f1-120">準備好使用者資料庫帳戶，並透過向管理服務資源提供者提出要求來擷取儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-120">The user database account is made ready, and storage keys are retrieved via a request to the Management Service Resource Provider.</span></span>
- <span data-ttu-id="ad5f1-121">使用者透過 HTTPS/安全傳輸建立與 Cosmos DB 的連線</span><span class="sxs-lookup"><span data-stu-id="ad5f1-121">A user creates a connection to Cosmos DB via HTTPS/secure transport.</span></span> <span data-ttu-id="ad5f1-122">(SDK 會對詳細資料進行抽象處理)。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-122">(The SDKs abstract the details.)</span></span>
- <span data-ttu-id="ad5f1-123">使用者透過先前所建立的安全連線，傳送要儲存的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-123">The user sends a JSON document to be stored over the previously created secure connection.</span></span>
- <span data-ttu-id="ad5f1-124">為 JSON 文件編製索引 (除非使用者已關閉編製索引)。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-124">The JSON document is indexed unless the user has turned off indexing.</span></span>
- <span data-ttu-id="ad5f1-125">JSON 文件和索引資料皆寫入安全儲存體。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-125">Both the JSON document and index data are written to secure storage.</span></span>
- <span data-ttu-id="ad5f1-126">系統會定期自安全儲存體讀取資料，並備份到 Azure 加密 Blob 存放區。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-126">Periodically, data is read from the secure storage and backed up to the Azure Encrypted Blob Store.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="ad5f1-127">常見問題集</span><span class="sxs-lookup"><span data-stu-id="ad5f1-127">Frequently asked questions</span></span>

### <a name="q-how-much-more-does-azure-storage-cost-if-storage-service-encryption-is-enabled"></a><span data-ttu-id="ad5f1-128">問︰如果已啟用儲存體服務加密，Azure 儲存體的成本會多出多少？</span><span class="sxs-lookup"><span data-stu-id="ad5f1-128">Q: How much more does Azure Storage cost if Storage Service Encryption is enabled?</span></span>
<span data-ttu-id="ad5f1-129">答：沒有任何額外成本。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-129">A: There is no additional cost.</span></span>

### <a name="q-who-manages-the-encryption-keys"></a><span data-ttu-id="ad5f1-130">問︰誰負責管理加密金鑰？</span><span class="sxs-lookup"><span data-stu-id="ad5f1-130">Q: Who manages the encryption keys?</span></span>
<span data-ttu-id="ad5f1-131">答︰金鑰是由 Microsoft 管理。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-131">A: The keys are managed by Microsoft.</span></span>

### <a name="q-how-often-are-encryption-keys-rotated"></a><span data-ttu-id="ad5f1-132">問︰加密金鑰多久輪替一次？</span><span class="sxs-lookup"><span data-stu-id="ad5f1-132">Q: How often are encryption keys rotated?</span></span>
<span data-ttu-id="ad5f1-133">答：Microsoft 針對加密金鑰輪替有一套 Cosmos DB 會遵循的內部方針。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-133">A: Microsoft has a set of internal guidelines for encryption key rotation, which Cosmos DB follows.</span></span> <span data-ttu-id="ad5f1-134">不會發佈特定方針。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-134">The specific guidelines are not published.</span></span> <span data-ttu-id="ad5f1-135">Microsoft 會發佈[安全性開發週期 (SDL)](https://www.microsoft.com/sdl/default.aspx)，這會視為內部指導方針的子集，其中包含對開發人員很實用的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-135">Microsoft does publish the [Security Development Lifecycle (SDL)](https://www.microsoft.com/sdl/default.aspx), which is seen as a subset of internal guidance and has useful best practices for developers.</span></span>

### <a name="q-can-i-use-my-own-encryption-keys"></a><span data-ttu-id="ad5f1-136">問︰我是否可以使用自己的加密金鑰？</span><span class="sxs-lookup"><span data-stu-id="ad5f1-136">Q: Can I use my own encryption keys?</span></span>
<span data-ttu-id="ad5f1-137">答：Cosmos DB 是一種 PaaS 服務，我們也很努力地讓這個服務容易使用。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-137">A: Cosmos DB is a PaaS service, and we worked hard to keep the service easy to use.</span></span> <span data-ttu-id="ad5f1-138">我們注意到會詢問此問題的使用者，通常是想詢問有關符合如 PCI-DSS 等合規性需求的 Proxy 問題。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-138">We've noticed this question is often asked as a proxy question for meeting a compliance requirement like PCI-DSS.</span></span> <span data-ttu-id="ad5f1-139">建置這項功能時，我們已與合規性稽核人員合作，以確保使用 Cosmos DB 的客戶能夠在不需要自行管理金鑰的情況下滿足他們的需求。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-139">As part of building this feature, we worked with compliance auditors to ensure that customers who use Cosmos DB meet their requirements without the need to manage keys themselves.</span></span>
<span data-ttu-id="ad5f1-140">因此，我們目前不提供讓使用者自行管理金鑰的選項。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-140">As a result, we currently do not offer users the option to burden themselves with key management.</span></span>

### <a name="q-what-regions-have-encryption-turned-on"></a><span data-ttu-id="ad5f1-141">問：有哪些區域已開啟加密？</span><span class="sxs-lookup"><span data-stu-id="ad5f1-141">Q: What regions have encryption turned on?</span></span>
<span data-ttu-id="ad5f1-142">答：所有的 Azure Cosmos DB 區域皆已針對所有使用者資料開啟加密。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-142">A: All Azure Cosmos DB regions have encryption turned on for all user data.</span></span>

### <a name="q-does-encryption-affect-the-performance-latency-and-throughput-slas"></a><span data-ttu-id="ad5f1-143">問︰加密會影響效能延遲和輸送量 SLA 嗎？</span><span class="sxs-lookup"><span data-stu-id="ad5f1-143">Q: Does encryption affect the performance latency and throughput SLAs?</span></span>
<span data-ttu-id="ad5f1-144">答︰現在所有現有和新的帳戶都啟用待用加密，但是效能 SLA 沒有任何影響或變化。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-144">A: There is no impact or changes to the performance SLAs now that encryption at rest is enabled for all existing and new accounts.</span></span> <span data-ttu-id="ad5f1-145">您可以在 [Cosmos DB SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db) 頁面閱讀更多資訊以查看最新的保證。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-145">You can read more on the [SLA for Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db) page to see the latest guarantees.</span></span>

### <a name="q-does-the-local-emulator-support-encryption-at-rest"></a><span data-ttu-id="ad5f1-146">問︰本機模擬器支援待用加密嗎？</span><span class="sxs-lookup"><span data-stu-id="ad5f1-146">Q: Does the local emulator support encryption at rest?</span></span>
<span data-ttu-id="ad5f1-147">答︰模擬器是獨立的開發/測試工具，不使用受管理 Cosmos DB 服務所使用的金鑰管理服務。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-147">A: The emulator is a standalone dev/test tool and does not use the key management services that the managed Cosmos DB service uses.</span></span> <span data-ttu-id="ad5f1-148">我們建議您在儲存機密模擬器測試資料的磁碟機上啟用 BitLocker。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-148">Our recommendation is to enable BitLocker on drives where you are storing sensitive emulator test data.</span></span> <span data-ttu-id="ad5f1-149">[模擬器支援變更預設資料目錄](local-emulator.md)，也支援使用已知位置。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-149">The [emulator supports changing the default data directory](local-emulator.md) as well as using a well-known location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad5f1-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ad5f1-150">Next steps</span></span>

<span data-ttu-id="ad5f1-151">如需 Cosmos DB 安全性及最新改進的概觀，請參閱 [Azure Cosmos DB 資料庫安全性](database-security.md)。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-151">For an overview of Cosmos DB security and the latest improvements, see [Azure Cosmos DB database security](database-security.md).</span></span>
<span data-ttu-id="ad5f1-152">如需 Microsoft 認證的詳細資訊，請參閱 [Azure 信任中心](https://azure.microsoft.com/en-us/support/trust-center/)。</span><span class="sxs-lookup"><span data-stu-id="ad5f1-152">For more information about Microsoft certifications, see the [Azure Trust Center](https://azure.microsoft.com/en-us/support/trust-center/).</span></span>
