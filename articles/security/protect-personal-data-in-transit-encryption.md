---
title: "aaaProtect 個人資料在傳輸過程中使用 Azure 中的加密 |Microsoft 文件"
description: "在 Azure tooprotect 個人資料使用加密"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a><span data-ttu-id="0a8c6-103">Azure 加密技術：使用加密功能來保護傳輸中的個人資料</span><span class="sxs-lookup"><span data-stu-id="0a8c6-103">Azure encryption technologies: Protect personal data in transit with encryption</span></span>

<span data-ttu-id="0a8c6-104">本文將協助您了解及使用 Azure 加密技術 toosecure 資料在傳輸過程中。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-104">This article will help you understand and use Azure encryption technologies toosecure data in transit.</span></span> 

<span data-ttu-id="0a8c6-105">保護 hello 隱私權的個人資料傳送嗨網路跨是多層的深度防禦的安全性策略中不可或缺的一部分。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-105">Protecting hello privacy of personal data as it travels across hello network is an essential part of a multi-layered defense-in-depth security strategy.</span></span> <span data-ttu-id="0a8c6-106">在傳輸過程中的加密 」 是設計的 tooprevent 攻擊者攔截從所能 tooview 或使用 hello 資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-106">Encryption in transit is designed tooprevent an attacker who intercepts transmissions from being able tooview or use hello data.</span></span>

## <a name="scenario"></a><span data-ttu-id="0a8c6-107">案例</span><span class="sxs-lookup"><span data-stu-id="0a8c6-107">Scenario</span></span>

<span data-ttu-id="0a8c6-108">大型出航公司搬遷後 hello 美國，展開在 hello 地中海、 Adriatic，與波羅的海文海，以及 hello 不列顛群島其作業 toooffer 行程。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="0a8c6-109">toosupport 努力，它所取得數個較小的出航行位於義大利，德國、 丹麥和 hello 英國</span><span class="sxs-lookup"><span data-stu-id="0a8c6-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="0a8c6-110">hello 公司使用 Microsoft Azure toostore 公司資料 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="0a8c6-111">其中包含其全球客戶群的名稱、地址、電話號碼和信用卡資訊等個人識別資訊。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-111">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="0a8c6-112">它也會包含在所有位置的傳統的人力資源資訊，例如地址、 電話號碼、 稅務識別碼和醫療公司員工的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-112">It also includes traditional Human Resource information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="0a8c6-113">hello 出航列也會維護報酬和忠誠度計劃成員大型資料庫，其中包含與目前和過去的客戶的個人資訊 tootrack 關聯性。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-113">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="0a8c6-114">客戶的個人資料會輸入 hello 資料庫中，從 hello 公司遠端辦公室和位於 hello 世界各地的旅行代理程式。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-114">Personal data of customers is entered in hello database from hello company’s remote offices and from travel agents located around hello world.</span></span> <span data-ttu-id="0a8c6-115">包含客戶資訊的文件會透過 hello 網路 tooAzure 儲存體傳輸。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-115">Documents containing customer information are transferred across hello network tooAzure storage.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="0a8c6-116">問題陳述</span><span class="sxs-lookup"><span data-stu-id="0a8c6-116">Problem statement</span></span>

<span data-ttu-id="0a8c6-117">hello 公司必須保護客戶的 hello 隱私權和員工的個人資料，同時它處於傳輸 tooand 從 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-117">hello company must protect hello privacy of customers’ and employees’ personal data while it is in transit tooand from Azure services.</span></span>

## <a name="company-goal"></a><span data-ttu-id="0a8c6-118">公司目標</span><span class="sxs-lookup"><span data-stu-id="0a8c6-118">Company goal</span></span>

<span data-ttu-id="0a8c6-119">hello 公司目標 tooensure 個人資料會加密磁碟關閉時。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-119">hello company goal tooensure that personal data is encrypted when off disk.</span></span> <span data-ttu-id="0a8c6-120">如果未經授權的人員攔截 hello 關閉磁碟個人資料，它必須是會轉譯無法讀取的格式。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-120">If unauthorized persons intercept hello off-disk personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="0a8c6-121">對於使用者和系統管理員而言，套用加密應該很容易或完全透明。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-121">Applying encryption should be easy, or completely transparent, for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="0a8c6-122">解決方案</span><span class="sxs-lookup"><span data-stu-id="0a8c6-122">Solutions</span></span>

<span data-ttu-id="0a8c6-123">Azure 服務可提供多個工具和技術 toohelp 保護傳輸中的個人資料。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-123">Azure services provide multiple tools and technologies toohelp you protect personal data in transit.</span></span>

### <a name="azure-storage"></a><span data-ttu-id="0a8c6-124">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="0a8c6-124">Azure Storage</span></span>

<span data-ttu-id="0a8c6-125">Hello 雲端中儲存的資料必須周遊從 hello 用戶端，它可以是實際上都位於任何位置 hello world，toohello Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-125">Data that is stored in hello cloud must travel from hello client, which can be physically located anywhere in hello world, toohello Azure data center.</span></span> <span data-ttu-id="0a8c6-126">使用者所擷取的資料時，傳送一次，在 hello 相反的方向。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-126">When that data is retrieved by users, it travels again, in hello opposite direction.</span></span> <span data-ttu-id="0a8c6-127">資料在傳輸過程中 hello 透過公用網際網路端一定是攻擊者攔截的風險。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-127">Data that is in transit over hello public Internet is always at risk of interception by attackers.</span></span> <span data-ttu-id="0a8c6-128">它是重要 tooprotect hello 隱私權的個人資料使用傳輸層級加密 toosecure 做為它的位置之間移動。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-128">It is important tooprotect hello privacy of personal data by using transport-level encryption toosecure it as it moves between locations.</span></span>

<span data-ttu-id="0a8c6-129">hello HTTPS 通訊協定透過 hello 網際網路提供安全且加密的通訊通道。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-129">hello HTTPS protocol provides a secure, encrypted communications channel over hello Internet.</span></span> <span data-ttu-id="0a8c6-130">呼叫 REST Api 時，應該使用的 tooaccess 物件在 Azure 儲存體和 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-130">HTTPS should be used tooaccess objects in Azure Storage and when calling REST APIs.</span></span> <span data-ttu-id="0a8c6-131">使用時，強制使用 hello HTTPS 通訊協定[共用存取簽章](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)(SAS) toodelegate 存取 tooAzure 儲存物件。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-131">You enforce use of hello HTTPS protocol when using [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate access tooAzure Storage objects.</span></span> <span data-ttu-id="0a8c6-132">SAS 類型有兩種：服務 SAS 和帳戶 SAS。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-132">There are two types of SAS: Service SAS and Account SAS.</span></span>

#### <a name="how-do-i-construct-a-service-sas"></a><span data-ttu-id="0a8c6-133">如何建構服務 SAS？</span><span class="sxs-lookup"><span data-stu-id="0a8c6-133">How do I construct a Service SAS?</span></span>

<span data-ttu-id="0a8c6-134">服務的 SAS 委派存取 tooa 資源中其中一個 hello 儲存體服務 （blob、 佇列、 資料表或檔案服務）。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-134">A Service SAS delegates access tooa resource in just one of hello storage services (blob, queue, table or file service).</span></span> <span data-ttu-id="0a8c6-135">tooconstruct 服務 SAS，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="0a8c6-135">tooconstruct a Service SAS, do hello following:</span></span>

1. <span data-ttu-id="0a8c6-136">指定簽署版本欄位 hello</span><span class="sxs-lookup"><span data-stu-id="0a8c6-136">Specify hello Signed Version Field</span></span>

2. <span data-ttu-id="0a8c6-137">指定 hello 簽章資源 （Blob 檔案服務僅與）</span><span class="sxs-lookup"><span data-stu-id="0a8c6-137">Specify hello Signed Resource (Blob and File Service Only)</span></span>

3. <span data-ttu-id="0a8c6-138">指定查詢參數 tooOverride 回應標頭 （Blob 服務和只有檔案服務）</span><span class="sxs-lookup"><span data-stu-id="0a8c6-138">Specify Query Parameters tooOverride Response Headers (Blob Service and File Service Only)</span></span>

4. <span data-ttu-id="0a8c6-139">指定 hello 資料表 （表格服務僅名稱）</span><span class="sxs-lookup"><span data-stu-id="0a8c6-139">Specify hello Table Name (Table Service Only)</span></span>

5. <span data-ttu-id="0a8c6-140">指定 hello 存取原則</span><span class="sxs-lookup"><span data-stu-id="0a8c6-140">Specify hello Access Policy</span></span>

6. <span data-ttu-id="0a8c6-141">指定 hello 簽章有效性間隔</span><span class="sxs-lookup"><span data-stu-id="0a8c6-141">Specify hello Signature Validity Interval</span></span>

8. <span data-ttu-id="0a8c6-142">指定權限</span><span class="sxs-lookup"><span data-stu-id="0a8c6-142">Specify Permissions</span></span>

9. <span data-ttu-id="0a8c6-143">指定 IP 位址或 IP 範圍</span><span class="sxs-lookup"><span data-stu-id="0a8c6-143">Specify IP Address or IP Range</span></span>

10. <span data-ttu-id="0a8c6-144">指定 hello HTTP 通訊協定</span><span class="sxs-lookup"><span data-stu-id="0a8c6-144">Specify hello HTTP Protocol</span></span>

11. <span data-ttu-id="0a8c6-145">指定資料表存取範圍</span><span class="sxs-lookup"><span data-stu-id="0a8c6-145">Specify Table Access Ranges</span></span>

12. <span data-ttu-id="0a8c6-146">指定簽署識別碼 hello</span><span class="sxs-lookup"><span data-stu-id="0a8c6-146">Specify hello Signed Identifier</span></span>

13. <span data-ttu-id="0a8c6-147">指定 hello 簽章</span><span class="sxs-lookup"><span data-stu-id="0a8c6-147">Specify hello Signature</span></span>

<span data-ttu-id="0a8c6-148">如需詳細指示，請參閱[建構服務 SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN)。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-148">For more detailed instructions, see [Constructing a Service SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span></span>

#### <a name="how-do-i-construct-an-account-sas"></a><span data-ttu-id="0a8c6-149">如何建構帳戶 SAS？</span><span class="sxs-lookup"><span data-stu-id="0a8c6-149">How do I construct an Account SAS?</span></span>

<span data-ttu-id="0a8c6-150">帳戶 SAS 會將委派存取 tooresources 一或多個 hello 儲存體服務中。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-150">An Account SAS delegates access tooresources in one or more of hello storage services.</span></span> <span data-ttu-id="0a8c6-151">您也可以委派存取 tooread、 寫入和刪除 blob 容器、 資料表、 佇列和服務的 SAS 不允許的檔案共用上的作業。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-151">You can also delegate access tooread, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="0a8c6-152">帳戶 SAS 的建構是類似的服務 SA toothat。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-152">Construction of an Account SAS is similar toothat of a Service SAS.</span></span> <span data-ttu-id="0a8c6-153">如需詳細指示，請參閱[建構服務 SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-153">For detailed instructions, see [Constructing an Account SAS.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span></span>

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a><span data-ttu-id="0a8c6-154">呼叫 REST API 時如何強制使用 HTTPS？</span><span class="sxs-lookup"><span data-stu-id="0a8c6-154">How do I enforce HTTPS when calling REST APIs?</span></span>

<span data-ttu-id="0a8c6-155">tooenforce hello 使用 HTTPS 呼叫儲存體帳戶中的 REST Api tooaccess 物件時，您可以啟用安全傳輸需要 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-155">tooenforce hello use of HTTPS when calling REST APIs tooaccess objects in storage accounts, you can enable Secure Transfer Required for hello storage account.</span></span> 

1. <span data-ttu-id="0a8c6-156">在 hello Azure 入口網站，選取 **建立儲存體帳戶**，或現有的儲存體帳戶，請選取**設定**然後**組態**。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-156">In hello Azure portal, select **Create Storage Account**, or for an existing storage account, select **Settings** and then **Configuration**.</span></span>

2. <span data-ttu-id="0a8c6-157">在 [需要安全傳輸] 下，選取 [已啟用]。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-157">Under **Secure Transfer Required**, select **Enabled**.</span></span>

![建立儲存體帳戶](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

<span data-ttu-id="0a8c6-159">如需詳細指示，包括如何 tooenable 安全傳輸需要以程式設計的方式，請參閱[需要安全傳輸](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer)。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-159">For more detailed instructions, including how tooenable Secure Transfer Required programmatically, see [Require Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span></span>

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a><span data-ttu-id="0a8c6-160">如何在 Azure 檔案儲存體中加密資料？</span><span class="sxs-lookup"><span data-stu-id="0a8c6-160">How do I encrypt data in Azure File Storage?</span></span>

<span data-ttu-id="0a8c6-161">tooencrypt 資料在傳輸與[Azure 檔案儲存體](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal)，您可以使用 SMB 3.x 與 Windows 8、 8.1 及 10 和 Windows Server 2012 R2 和 Windows Server 2016。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-161">tooencrypt data in transit with [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), you can use SMB 3.x with Windows 8, 8.1, and 10 and with Windows Server 2012 R2 and Windows Server 2016.</span></span> <span data-ttu-id="0a8c6-162">當您使用 hello Azure 檔案服務時，任何未加密時連線失敗 」 保護所需的傳輸 」 已啟用。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-162">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="0a8c6-163">這包括使用 SMB 2.1、 未加密，SMB 3.0 和 hello Linux SMB 用戶端的部分類別的案例。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-163">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span>

#### <a name="azure-client-side-encryption"></a><span data-ttu-id="0a8c6-164">Azure 用戶端加密</span><span class="sxs-lookup"><span data-stu-id="0a8c6-164">Azure Client-Side Encryption</span></span>

<span data-ttu-id="0a8c6-165">當個人資料在用戶端應用程式與儲存體之間傳輸時，另一個用於保護該資料的選項是[用戶端加密](https://docs.microsoft.com/azure/storage/storage-client-side-encryption)。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-165">Another option for protecting personal data while it’s being transferred between a client application and Azure Storage is [Client-side Encryption](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span></span> <span data-ttu-id="0a8c6-166">hello 資料都會經過加密後再傳輸至 Azure 儲存體，並收到 hello 用戶端之後，當您擷取 hello 資料從 Azure 儲存體時，會解密 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-166">hello data is encrypted before being transferred into Azure Storage and when you retrieve hello data from Azure Storage, hello data is decrypted after it is received on hello client side.</span></span>

### <a name="azure-site-to-site-vpn"></a><span data-ttu-id="0a8c6-167">Azure 站對站 VPN</span><span class="sxs-lookup"><span data-stu-id="0a8c6-167">Azure Site-to-Site VPN</span></span>

<span data-ttu-id="0a8c6-168">個人在公司網路或使用者與 hello Azure 虛擬網路之間傳輸資料有效地 tooprotect 是 toouse[站對站](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)或[點對站台](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)虛擬私人網路 (VPN)。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-168">An effective way tooprotect personal data in transit between a corporate network or user and hello Azure virtual network is toouse a [site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) or [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) Virtual Private Network (VPN).</span></span> <span data-ttu-id="0a8c6-169">VPN 連線 hello 網際網路之間建立安全的加密的通道。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-169">A VPN connection creates a secure encrypted tunnel across hello Internet.</span></span>

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a><span data-ttu-id="0a8c6-170">如何建立站對站 VPN 連線？</span><span class="sxs-lookup"><span data-stu-id="0a8c6-170">How do I create a site-to-site VPN connection?</span></span>

<span data-ttu-id="0a8c6-171">站對站 VPN 連線 hello 公司網路 tooAzure 上的多個使用者。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-171">A site-to-site VPN connects multiple users on hello corporate network tooAzure.</span></span> <span data-ttu-id="0a8c6-172">toocreate hello Azure 入口網站中的站對站連接嗎 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="0a8c6-172">toocreate a site-to-site connection in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="0a8c6-173">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-173">Create a virtual network.</span></span>

2. <span data-ttu-id="0a8c6-174">指定 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-174">Specify a DNS server.</span></span>

3. <span data-ttu-id="0a8c6-175">建立 hello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-175">Create hello gateway subnet.</span></span>

4. <span data-ttu-id="0a8c6-176">建立 hello VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-176">Create hello VPN gateway.</span></span> 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. <span data-ttu-id="0a8c6-177">建立 hello 區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-177">Create hello local network gateway.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. <span data-ttu-id="0a8c6-178">設定 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-178">Configure your VPN device.</span></span>

7. <span data-ttu-id="0a8c6-179">建立 hello VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-179">Create hello VPN connection.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. <span data-ttu-id="0a8c6-180">請確認 hello VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-180">Verify hello VPN connection.</span></span>

<span data-ttu-id="0a8c6-181">如需詳細指示上如何 toocreate 網站-站台連接在 hello Azure 入口網站，請參閱 [hello Azure 入口網站中建立站台間連線]。(https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="0a8c6-181">For more detailed instructions on how toocreate a site-to-site connection in hello Azure portal, see [Create a Site-to-Site  connection in hello Azure Portal.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span></span>

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a><span data-ttu-id="0a8c6-182">如何設定點對站 VPN 連線？</span><span class="sxs-lookup"><span data-stu-id="0a8c6-182">How do I create a point-to-site VPN connection?</span></span>

<span data-ttu-id="0a8c6-183">點對站 VPN 會從個別的用戶端電腦 tooa 虛擬網路建立安全連線。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-183">A Point-to-Site VPN creates a secure connection from an individual client computer tooa virtual network.</span></span> <span data-ttu-id="0a8c6-184">當您想 tooconnect tooAzure 從遠端位置，例如從首頁，或在旅館或會議中心時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-184">This is useful when you  want tooconnect tooAzure from a remote location, such as from home or a hotel or conference center.</span></span> <span data-ttu-id="0a8c6-185">toocreate hello Azure 入口網站中的點對站連接</span><span class="sxs-lookup"><span data-stu-id="0a8c6-185">toocreate a point-to-site  connection in hello Azure portal,</span></span>

1. <span data-ttu-id="0a8c6-186">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-186">Create a virtual network.</span></span>

2. <span data-ttu-id="0a8c6-187">新增閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-187">Add a gateway subnet.</span></span>

3. <span data-ttu-id="0a8c6-188">指定 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-188">Specify a DNS server.</span></span> <span data-ttu-id="0a8c6-189">(選用)</span><span class="sxs-lookup"><span data-stu-id="0a8c6-189">(optional)</span></span>

4. <span data-ttu-id="0a8c6-190">建立虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-190">Create a virtual network gateway.</span></span>

5. <span data-ttu-id="0a8c6-191">產生憑證。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-191">Generate certificates.</span></span>

6. <span data-ttu-id="0a8c6-192">新增 hello 用戶端位址集區。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-192">Add hello client address pool.</span></span>

7. <span data-ttu-id="0a8c6-193">上傳 hello 根憑證的公開憑證資料。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-193">Upload hello root certificate public certificate data.</span></span>

8. <span data-ttu-id="0a8c6-194">產生並安裝 hello VPN 用戶端組態封裝。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-194">Generate and install hello VPN client configuration package.</span></span>

9. <span data-ttu-id="0a8c6-195">安裝匯出的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-195">Install an exported client certificate.</span></span>

10. <span data-ttu-id="0a8c6-196">連接 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-196">Connect tooAzure.</span></span>

11. <span data-ttu-id="0a8c6-197">確認您的連線。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-197">Verify your connection.</span></span>

<span data-ttu-id="0a8c6-198">如需詳細指示，請參閱[設定點對站連線 tooa VNet 使用憑證驗證： Azure 入口網站。](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="0a8c6-198">For more detailed instructions, see [Configure a Point-to-Site connection tooa VNet using certificate authentication: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span></span>

### <a name="ssltls"></a><span data-ttu-id="0a8c6-199">SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="0a8c6-199">SSL/TLS</span></span>

<span data-ttu-id="0a8c6-200">Microsoft 建議您一律使用 SSL/TLS 通訊協定 tooexchange 資料分散在不同的位置。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-200">Microsoft recommends that you always use SSL/TLS protocols tooexchange data across different locations.</span></span> <span data-ttu-id="0a8c6-201">選擇 toouse 的組織[ExpressRoute](https://docs.microsoft.com/azure/expressroute/)透過專用高速 WAN 連結 toomove 大型資料集也可以加密 hello hello 為了提高保護使用 SSL/TLS 或其他通訊協定的應用程式層級的資料。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-201">Organizations that choose toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove large data sets over a dedicated high-speed WAN link can also encrypt hello data at hello application-level using SSL/TLS or other protocols for added protection.</span></span>

### <a name="encryption-by-default"></a><span data-ttu-id="0a8c6-202">預設加密</span><span class="sxs-lookup"><span data-stu-id="0a8c6-202">Encryption by default</span></span>

<span data-ttu-id="0a8c6-203">Microsoft 會使用加密 tooprotect 資料中的 customers 與 Azure 雲端服務之間傳輸。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-203">Microsoft uses encryption tooprotect data in transit between customers and Azure cloud services.</span></span> <span data-ttu-id="0a8c6-204">如果透過 hello Azure 網站互動與 Azure 儲存體，所有交易將會透過 HTTPS 都發生。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-204">If you are interacting with Azure Storage through hello Azure Portal, all transactions occur via HTTPS.</span></span>

<span data-ttu-id="0a8c6-205">[傳輸層安全性](https://en.wikipedia.org/wiki/Transport_Layer_Security)(TLS) 是 Microsoft 資料中心內會嘗試與連接 tooMicrosoft 雲端服務的用戶端系統 toonegotiate hello 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is hello protocol that Microsoft data centers will attempt toonegotiate with client systems that connect tooMicrosoft cloud services.</span></span> <span data-ttu-id="0a8c6-206">TLS 提供增強式驗證、訊息隱私權、完整性 (可偵測訊息竄改、攔截和偽造)、互通性、演算法彈性，並方便部署和使用。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-206">TLS provides strong authentication, message privacy, and integrity (enables detection of message tampering, interception, and forgery), interoperability, algorithm flexibility, ease of deployment and use.</span></span>

<span data-ttu-id="0a8c6-207">此外，也會運用 [完整轉寄密碼](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS)，以便客戶的用戶端系統與 Microsoft 的雲端服務之間的每個連線使用唯一金鑰。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-207">[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) is also employed so that each connection between customers’ client systems and Microsoft’s cloud services use unique keys.</span></span> <span data-ttu-id="0a8c6-208">連線 tooMicrosoft 雲端服務也充分利用基礎的 RSA 2048 位元加密金鑰長度。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-208">Connections tooMicrosoft cloud services also take advantage of RSA based 2,048-bit encryption key lengths.</span></span> <span data-ttu-id="0a8c6-209">hello TLS，RSA 2048 位元金鑰長度的組合和 PFS 會讓它更為困難有人 toointercept 及存取 Microsoft 雲端服務與客戶之間傳輸的資料。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-209">hello combination of TLS, RSA 2,048-bit key lengths, and PFS makes it much  more difficult for someone toointercept and access data that is in transit between Microsoft cloud services and customers.</span></span>

<span data-ttu-id="0a8c6-210">傳輸中的資料一律會在 [Data Lake Store] 中加密 (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview)。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-210">Data in transit is always encrypted in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span></span> <span data-ttu-id="0a8c6-211">此外 tooencrypting 資料先前 toostoring toopersistent 媒體 hello 資料也都受到保護傳輸中使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-211">In addition tooencrypting data prior toostoring toopersistent media, hello data is also always secured in transit by using HTTPS.</span></span> <span data-ttu-id="0a8c6-212">HTTPS 是 hello 唯一的通訊協定支援的資料湖存放區 REST 介面的 hello。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-212">HTTPS is hello only protocol that is supported for hello Data Lake Store REST interfaces.</span></span>

## <a name="summary"></a><span data-ttu-id="0a8c6-213">摘要</span><span class="sxs-lookup"><span data-stu-id="0a8c6-213">Summary</span></span>

<span data-ttu-id="0a8c6-214">hello 公司可以完成其目標是保護這類資料的個人資料和 hello 隱私權強制使用 HTTPS 連線 tooAzure 儲存體、 使用共用存取簽章，以及啟用 hello 儲存體帳戶中的 安全傳輸需要。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-214">hello company can accomplish its goal of protecting personal data and hello privacy of such data by enforcing HTTPS connections tooAzure Storage, using Shared Access Signatures and enabling Secure Transfer Required on hello storage accounts.</span></span> <span data-ttu-id="0a8c6-215">他們也可藉由使用 SMB 3.0 連線並實作用戶端加密來保護個人資料。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-215">They can also protect personal data by using SMB 3.0 connections and implementing client-side encryption.</span></span> <span data-ttu-id="0a8c6-216">站對站 VPN 連線，從 hello 公司網路 toohello Azure 虛擬網路和點對站 VPN 連線，從個別的使用者將會建立安全通道，透過它的個人資料可以安全地傳輸。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-216">Site-to-site VPN connections from hello corporate network toohello Azure virtual network and point-to-site VPN connections from individual users will create a secure tunnel through which personal data can securely travel.</span></span> <span data-ttu-id="0a8c6-217">Microsoft 的預設加密作法會進一步保護 hello 隱私權的個人資料。</span><span class="sxs-lookup"><span data-stu-id="0a8c6-217">Microsoft’s default encryption practices will further protect hello privacy of personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a8c6-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a8c6-218">Next steps</span></span>

- [<span data-ttu-id="0a8c6-219">Azure 資料安全性和加密最佳做法</span><span class="sxs-lookup"><span data-stu-id="0a8c6-219">Azure Data Security and Encryption Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [<span data-ttu-id="0a8c6-220">規劃與設計 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="0a8c6-220">Planning and design for VPN Gateway</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [<span data-ttu-id="0a8c6-221">VPN 閘道常見問題集</span><span class="sxs-lookup"><span data-stu-id="0a8c6-221">VPN Gateway FAQ</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [<span data-ttu-id="0a8c6-222">購買及設定您的 Azure App Service 的 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="0a8c6-222">Buy and configure an SSL Certificate for your Azure App Service</span></span>](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
