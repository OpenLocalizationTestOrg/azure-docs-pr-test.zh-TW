---
title: "aaaImport 及匯出網域區域檔案 tooAzure DNS 使用 Azure CLI 1.0 |Microsoft 文件"
description: "了解如何 tooimport 及匯出 DNS 區域檔案 tooAzure DNS 使用 Azure CLI 1.0"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a><span data-ttu-id="2ea17-103">匯入和匯出 DNS 區域檔案中使用 Azure CLI 1.0 hello</span><span class="sxs-lookup"><span data-stu-id="2ea17-103">Import and export a DNS zone file using hello Azure CLI 1.0</span></span> 

<span data-ttu-id="2ea17-104">這篇文章會引導您使用 Azure DNS tooimport 及匯出 DNS 區域檔案 hello Azure CLI 1.0 的方式。</span><span class="sxs-lookup"><span data-stu-id="2ea17-104">This article walks you through how tooimport and export DNS zone files for Azure DNS using hello Azure CLI 1.0.</span></span>

## <a name="introduction-toodns-zone-migration"></a><span data-ttu-id="2ea17-105">簡介 tooDNS 區域移轉</span><span class="sxs-lookup"><span data-stu-id="2ea17-105">Introduction tooDNS zone migration</span></span>

<span data-ttu-id="2ea17-106">DNS 區域檔案是文字檔，其中包含 hello 區域中的每個網域名稱系統 (DNS) 記錄的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2ea17-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in hello zone.</span></span> <span data-ttu-id="2ea17-107">它會遵循標準格式，使其適合於在 DNS 系統之間傳送 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="2ea17-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="2ea17-108">使用區域檔案是快速、 可靠及方便 tootransfer 入或移出 Azure DNS 的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="2ea17-108">Using a zone file is a quick, reliable, and convenient way tootransfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="2ea17-109">Azure DNS 支援匯入和匯出使用 hello Azure 命令列介面 (CLI) 的區域檔案。</span><span class="sxs-lookup"><span data-stu-id="2ea17-109">Azure DNS supports importing and exporting zone files by using hello Azure command-line interface (CLI).</span></span> <span data-ttu-id="2ea17-110">區域檔案匯入**不**目前支援透過 Azure PowerShell 或 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="2ea17-110">Zone file import is **not** currently supported via Azure PowerShell or hello Azure portal.</span></span>

<span data-ttu-id="2ea17-111">hello Azure CLI 1.0 是跨平台命令列工具，可用來管理 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="2ea17-111">hello Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="2ea17-112">它是適用於從 hello hello Windows、 Mac 和 Linux 平台[Azure 下載頁面](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="2ea17-112">It is available for hello Windows, Mac, and Linux platforms from hello [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="2ea17-113">跨平台支援在進行匯入和匯出區域檔案，因為 hello 最常見的名稱伺服器軟體而言很重要[繫結](https://www.isc.org/downloads/bind/)，通常會在 Linux 上執行。</span><span class="sxs-lookup"><span data-stu-id="2ea17-113">Cross-platform support is important for importing and exporting zone files, because hello most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="2ea17-114">目前有兩個 hello Azure CLI 版本。</span><span class="sxs-lookup"><span data-stu-id="2ea17-114">There are currently two versions of hello Azure CLI.</span></span> <span data-ttu-id="2ea17-115">CLI1.0 以 Node.js 為基礎，且命令以「azure」開頭。</span><span class="sxs-lookup"><span data-stu-id="2ea17-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="2ea17-116">CLI2.0 以 Python 為基礎，且命令以「az」開頭。</span><span class="sxs-lookup"><span data-stu-id="2ea17-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="2ea17-117">雖然支援區域檔案匯入兩個版本中，我們建議使用 hello CLI1.0 命令，此頁面中所述。</span><span class="sxs-lookup"><span data-stu-id="2ea17-117">While zone file import is supported in both versions, we recommend using hello CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="2ea17-118">取得現有的 DNS 區域檔案</span><span class="sxs-lookup"><span data-stu-id="2ea17-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="2ea17-119">DNS 區域檔案匯入 Azure DNS 之前，您會需要 tooobtain hello 區域檔案的副本。</span><span class="sxs-lookup"><span data-stu-id="2ea17-119">Before you import a DNS zone file into Azure DNS, you need tooobtain a copy of hello zone file.</span></span> <span data-ttu-id="2ea17-120">此檔案的 hello 來源取決於目前裝載 hello DNS 區域的位置。</span><span class="sxs-lookup"><span data-stu-id="2ea17-120">hello source of this file depends on where hello DNS zone is currently hosted.</span></span>

* <span data-ttu-id="2ea17-121">如果您的 DNS 區域，由合作夥伴服務 （例如網域註冊機構、 專用的 DNS 主機服務提供者或替代的雲端提供者），該服務應該提供 hello 能力 toodownload hello DNS 區域檔案。</span><span class="sxs-lookup"><span data-stu-id="2ea17-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide hello ability toodownload hello DNS zone file.</span></span>
* <span data-ttu-id="2ea17-122">如果您的 DNS 區域主控 Windows DNS，hello hello 區域檔案的預設資料夾是**%systemroot%\system32\dns**。</span><span class="sxs-lookup"><span data-stu-id="2ea17-122">If your DNS zone is hosted on Windows DNS, hello default folder for hello zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="2ea17-123">hello 完整路徑 tooeach 區域檔案也會顯示在 [hello**一般**hello DNS 主控台] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2ea17-123">hello full path tooeach zone file also shows on hello **General** tab of hello DNS console.</span></span>
* <span data-ttu-id="2ea17-124">如果使用繫結裝載您的 DNS 區域，hello 繫結的組態檔中指定的 hello 區域檔案中每個區域的 hello 位置**named.conf**。</span><span class="sxs-lookup"><span data-stu-id="2ea17-124">If your DNS zone is hosted by using BIND, hello location of hello zone file for each zone is specified in hello BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="2ea17-125">下載自 GoDaddy 的區域檔案會有些微非標準格式。</span><span class="sxs-lookup"><span data-stu-id="2ea17-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="2ea17-126">您需要 toocorrect 此之前，您將這些區域檔案匯入 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="2ea17-126">You need toocorrect this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="2ea17-127">Hello RDATA 的每個 DNS 記錄中的 DNS 名稱指定為完整名稱，但是沒有終止"。"這表示其他 DNS 系統會將這些名稱解譯為相對名稱。</span><span class="sxs-lookup"><span data-stu-id="2ea17-127">DNS names in hello RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="2ea17-128">您需要： tooedit hello 區域檔案 tooappend hello 終止 」。 「 tootheir 名稱之前您匯入 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="2ea17-128">You need tooedit hello zone file tooappend hello terminating "." tootheir names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="2ea17-129">例如，hello"www 3600 CNAME contoso.com 中 」 的 CNAME 記錄應變更太"www 3600 IN CNAME contoso.com"。</span><span class="sxs-lookup"><span data-stu-id="2ea17-129">For example, hello CNAME record "www 3600 IN CNAME contoso.com" should be changed too"www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="2ea17-130">(結尾附加「.」)。</span><span class="sxs-lookup"><span data-stu-id="2ea17-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="2ea17-131">將 DNS 區域檔案匯入 Azure DNS</span><span class="sxs-lookup"><span data-stu-id="2ea17-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="2ea17-132">匯入區域檔案會在 Azure DNS 中建立新區域 (如果區域不存在)。</span><span class="sxs-lookup"><span data-stu-id="2ea17-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="2ea17-133">如果 hello 區域已經存在，hello hello 區域檔案中的資料錄集必須與合併 hello 現有資料錄集。</span><span class="sxs-lookup"><span data-stu-id="2ea17-133">If hello zone already exists, hello record sets in hello zone file must be merged with hello existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="2ea17-134">合併行為</span><span class="sxs-lookup"><span data-stu-id="2ea17-134">Merge behavior</span></span>

* <span data-ttu-id="2ea17-135">預設會合併現有和新的記錄集。</span><span class="sxs-lookup"><span data-stu-id="2ea17-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="2ea17-136">合併的資料錄集內相同的記錄會進行重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="2ea17-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="2ea17-137">或者，藉由指定 hello`--force`選項，hello 匯入程序來取代現有的資料錄集，與新的資料錄集。</span><span class="sxs-lookup"><span data-stu-id="2ea17-137">Alternatively, by specifying hello `--force` option, hello import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="2ea17-138">不會移除現有的記錄集並沒有對應的記錄設定 hello 匯入的區域檔案中。</span><span class="sxs-lookup"><span data-stu-id="2ea17-138">Existing record sets that do not have a corresponding record set in hello imported zone file are not be removed.</span></span>
* <span data-ttu-id="2ea17-139">當合併資料錄集時，hello toolive (TTL) 預先存在的資料錄集的使用時間。</span><span class="sxs-lookup"><span data-stu-id="2ea17-139">When record sets are merged, hello time toolive (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="2ea17-140">當`--force`是 hello hello 新資料錄集的 TTL 會使用。</span><span class="sxs-lookup"><span data-stu-id="2ea17-140">When `--force` is used, hello TTL of hello new record set is used.</span></span>
* <span data-ttu-id="2ea17-141">啟動授權 (SOA) 參數 (除了`host`) 一定會取自 hello 匯入的區域檔案，而不論是否`--force`用。</span><span class="sxs-lookup"><span data-stu-id="2ea17-141">Start of Authority (SOA) parameters (except `host`) are always taken from hello imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="2ea17-142">同樣地，在 hello 區域的 apex 設定 hello 名稱伺服器記錄，hello TTL 一定是取自 hello 匯入的區域檔案。</span><span class="sxs-lookup"><span data-stu-id="2ea17-142">Similarly, for hello name server record set at hello zone apex, hello TTL is always taken from hello imported zone file.</span></span>
* <span data-ttu-id="2ea17-143">匯入的 CNAME 記錄不會取代現有的 CNAME 記錄以相同的名稱，除非 hello hello`--force`指定參數。</span><span class="sxs-lookup"><span data-stu-id="2ea17-143">An imported CNAME record does not replace an existing CNAME record with hello same name unless hello `--force` parameter is specified.</span></span>
* <span data-ttu-id="2ea17-144">CNAME 記錄與另一筆記錄之間發生衝突時的 hello 相同名稱但不同類型 （不論它現有或新）、 hello 現有的記錄會保留。</span><span class="sxs-lookup"><span data-stu-id="2ea17-144">When a conflict arises between a CNAME record and another record of hello same name but different type (regardless of which is existing or new), hello existing record is retained.</span></span> <span data-ttu-id="2ea17-145">這是獨立的 hello 使用`--force`。</span><span class="sxs-lookup"><span data-stu-id="2ea17-145">This is independent of hello use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="2ea17-146">匯入的其他資訊</span><span class="sxs-lookup"><span data-stu-id="2ea17-146">Additional information about importing</span></span>

<span data-ttu-id="2ea17-147">hello 下列注意事項提供在 hello 區域相關的其他技術詳細資料匯入程序。</span><span class="sxs-lookup"><span data-stu-id="2ea17-147">hello following notes provide additional technical details about hello zone import process.</span></span>

* <span data-ttu-id="2ea17-148">hello`$TTL`指示詞是選擇性的而且受支援。</span><span class="sxs-lookup"><span data-stu-id="2ea17-148">hello `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="2ea17-149">若未`$TTL`指示詞，匯入記錄，卻不明確的 TTL 設為 tooa 預設值為 3600 秒的 TTL。</span><span class="sxs-lookup"><span data-stu-id="2ea17-149">When no `$TTL` directive is given, records without an explicit TTL are imported set tooa default TTL of 3600 seconds.</span></span> <span data-ttu-id="2ea17-150">當兩個記錄中 hello 相同的資料錄集指定不同的 Eap-ttls，使用 hello 較低的值。</span><span class="sxs-lookup"><span data-stu-id="2ea17-150">When two records in hello same record set specify different TTLs, hello lower value is used.</span></span>
* <span data-ttu-id="2ea17-151">hello`$ORIGIN`指示詞是選擇性的而且受支援。</span><span class="sxs-lookup"><span data-stu-id="2ea17-151">hello `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="2ea17-152">若未`$ORIGIN`設定 hello 預設使用的值是 hello hello 命令列上指定的區域名稱 (加上終止 hello"。")。</span><span class="sxs-lookup"><span data-stu-id="2ea17-152">When no `$ORIGIN` is set, hello default value used is hello zone name as specified on hello command line (plus hello terminating ".").</span></span>
* <span data-ttu-id="2ea17-153">hello`$INCLUDE`和`$GENERATE`指示詞不支援。</span><span class="sxs-lookup"><span data-stu-id="2ea17-153">hello `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="2ea17-154">支援這些記錄類型：A、AAAA、CNAME、MX、NS、SOA、SRV 和 TXT。</span><span class="sxs-lookup"><span data-stu-id="2ea17-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="2ea17-155">hello SOA 記錄會自動建立 Azure DNS 區域建立時。</span><span class="sxs-lookup"><span data-stu-id="2ea17-155">hello SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="2ea17-156">當您匯入區域檔案時，將所有 SOA 參數都取自 hello 區域檔案*除了*hello`host`參數。</span><span class="sxs-lookup"><span data-stu-id="2ea17-156">When you import a zone file, all SOA parameters are taken from hello zone file *except* hello `host` parameter.</span></span> <span data-ttu-id="2ea17-157">這個參數會使用 Azure DNS 所提供的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="2ea17-157">This parameter uses hello value provided by Azure DNS.</span></span> <span data-ttu-id="2ea17-158">這是因為此參數必須參考 toohello 主要名稱伺服器提供的 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="2ea17-158">This is because this parameter must refer toohello primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="2ea17-159">設定在 hello 區域的 apex hello 名稱伺服器記錄也會建立自動由 Azure DNS 建立 hello 區域時。</span><span class="sxs-lookup"><span data-stu-id="2ea17-159">hello name server record set at hello zone apex is also created automatically by Azure DNS when hello zone is created.</span></span> <span data-ttu-id="2ea17-160">只有 hello TTL 此記錄集的匯入。</span><span class="sxs-lookup"><span data-stu-id="2ea17-160">Only hello TTL of this record set is imported.</span></span> <span data-ttu-id="2ea17-161">這些記錄包含 hello Azure DNS 所提供的名稱伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="2ea17-161">These records contain hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="2ea17-162">hello 記錄資料不會覆寫 hello hello 匯入的區域檔案中包含的值。</span><span class="sxs-lookup"><span data-stu-id="2ea17-162">hello record data is not overwritten by hello values contained in hello imported zone file.</span></span>
* <span data-ttu-id="2ea17-163">在公開預覽期間，Azure DNS 僅支援單一字串 TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="2ea17-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="2ea17-164">Multistring TXT 記錄都是串連與遭到截斷 too255 字元。</span><span class="sxs-lookup"><span data-stu-id="2ea17-164">Multistring TXT records are be concatenated and truncated too255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="2ea17-165">CLI 格式和值</span><span class="sxs-lookup"><span data-stu-id="2ea17-165">CLI format and values</span></span>

<span data-ttu-id="2ea17-166">hello Azure CLI 命令 tooimport DNS 區域的 hello 格式如下：</span><span class="sxs-lookup"><span data-stu-id="2ea17-166">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="2ea17-167">值：</span><span class="sxs-lookup"><span data-stu-id="2ea17-167">Values:</span></span>

* <span data-ttu-id="2ea17-168">`<resource group>`是 hello hello 資源群組名稱 hello Azure DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="2ea17-168">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="2ea17-169">`<zone name>`這是 hello hello 區域名稱。</span><span class="sxs-lookup"><span data-stu-id="2ea17-169">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="2ea17-170">`<zone file name>`這是 hello 路徑/名稱 hello 區域檔案 toobe 匯入。</span><span class="sxs-lookup"><span data-stu-id="2ea17-170">`<zone file name>` is hello path/name of hello zone file toobe imported.</span></span>

<span data-ttu-id="2ea17-171">如果具有此名稱的區域不存在 hello 資源群組中，它會為您建立。</span><span class="sxs-lookup"><span data-stu-id="2ea17-171">If a zone with this name does not exist in hello resource group, it is created for you.</span></span> <span data-ttu-id="2ea17-172">如果 hello 區域已經存在，hello 匯入的資料錄集與合併現有的資料錄集。</span><span class="sxs-lookup"><span data-stu-id="2ea17-172">If hello zone already exists, hello imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="2ea17-173">toooverwrite hello 現有資料錄集，使用 hello`--force`選項。</span><span class="sxs-lookup"><span data-stu-id="2ea17-173">toooverwrite hello existing record sets, use hello `--force` option.</span></span>

<span data-ttu-id="2ea17-174">區域檔案，而不實際匯入它使用 hello tooverify hello 格式`--parse-only`選項。</span><span class="sxs-lookup"><span data-stu-id="2ea17-174">tooverify hello format of a zone file without actually importing it, use hello `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="2ea17-175">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="2ea17-175">Step 1.</span></span> <span data-ttu-id="2ea17-176">匯入區域檔案</span><span class="sxs-lookup"><span data-stu-id="2ea17-176">Import a zone file</span></span>

<span data-ttu-id="2ea17-177">tooimport hello 區域的區域檔案**contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="2ea17-177">tooimport a zone file for hello zone **contoso.com**.</span></span>

1. <span data-ttu-id="2ea17-178">Tooyour Azure 訂用帳戶使用的登入 hello Azure CLI 1.0。</span><span class="sxs-lookup"><span data-stu-id="2ea17-178">Sign in tooyour Azure subscription by using hello Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="2ea17-179">選取您想 toocreate 新的 DNS 區域的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ea17-179">Select hello subscription where you want toocreate your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="2ea17-180">Azure DNS 是 Azure 資源管理員服務，因此 hello Azure CLI 必須交換的 tooResource 管理員模式。</span><span class="sxs-lookup"><span data-stu-id="2ea17-180">Azure DNS is an Azure Resource Manager-only service, so hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="2ea17-181">使用 hello Azure DNS 服務之前，您必須註冊訂用帳戶 toouse hello Microsoft.Network 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="2ea17-181">Before you use hello Azure DNS service, you must register your subscription toouse hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="2ea17-182">(每個訂用帳戶只需執行一次此作業)。</span><span class="sxs-lookup"><span data-stu-id="2ea17-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="2ea17-183">如果您還沒有已經，您也需要 toocreate 資源管理員資源群組。</span><span class="sxs-lookup"><span data-stu-id="2ea17-183">If you don't have one already, you also need toocreate a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="2ea17-184">tooimport hello 區域**contoso.com** hello 檔案從**contoso.com.txt**到新的 DNS 區域 hello 資源群組中**myresourcegroup**，執行 hello 命令`azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="2ea17-184">tooimport hello zone **contoso.com** from hello file **contoso.com.txt** into a new DNS zone in hello resource group **myresourcegroup**, run hello command `azure network dns zone import`.</span></span><BR><span data-ttu-id="2ea17-185">這個命令載入 hello 區域檔案，並將它剖析。</span><span class="sxs-lookup"><span data-stu-id="2ea17-185">This command loads hello zone file and parse it.</span></span> <span data-ttu-id="2ea17-186">hello 命令執行一系列的命令在 hello Azure DNS 服務 toocreate hello 區域和所有 hello 記錄都設定 hello 區域中。</span><span class="sxs-lookup"><span data-stu-id="2ea17-186">hello command executes a series of commands on hello Azure DNS service toocreate hello zone and all hello record sets in hello zone.</span></span> <span data-ttu-id="2ea17-187">在 hello 主控台視窗中，以及任何錯誤或警告的 hello 命令報告進度。</span><span class="sxs-lookup"><span data-stu-id="2ea17-187">hello command reports progress in hello console window, along with any errors or warnings.</span></span> <span data-ttu-id="2ea17-188">數列中建立資料錄集，因為可能需要幾分鐘的時間 tooimport 大型區域檔案。</span><span class="sxs-lookup"><span data-stu-id="2ea17-188">Because record sets are created in series, it may take a few minutes tooimport a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a><span data-ttu-id="2ea17-189">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="2ea17-189">Step 2.</span></span> <span data-ttu-id="2ea17-190">確認 hello 區域</span><span class="sxs-lookup"><span data-stu-id="2ea17-190">Verify hello zone</span></span>

<span data-ttu-id="2ea17-191">tooverify hello DNS 區域 hello 檔案匯入之後，您可以使用任何一種 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="2ea17-191">tooverify hello DNS zone after you import hello file, you can use any one of hello following methods:</span></span>

* <span data-ttu-id="2ea17-192">您可以使用下列 Azure CLI 命令的 hello 列出 hello 記錄：</span><span class="sxs-lookup"><span data-stu-id="2ea17-192">You can list hello records by using hello following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="2ea17-193">您可以使用 hello PowerShell cmdlet 列出 hello 記錄`Get-AzureRmDnsRecordSet`。</span><span class="sxs-lookup"><span data-stu-id="2ea17-193">You can list hello records by using hello PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="2ea17-194">您可以使用`nslookup`tooverify hello 記錄的名稱解析。</span><span class="sxs-lookup"><span data-stu-id="2ea17-194">You can use `nslookup` tooverify name resolution for hello records.</span></span> <span data-ttu-id="2ea17-195">因為 hello 區域不尚未委派，會明確需要 toospecify hello 正確 Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="2ea17-195">Because hello zone isn't delegated yet, you need toospecify hello correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="2ea17-196">hello 下列範例顯示如何 tooretrieve hello 名稱伺服器名稱指定 toohello 區域。</span><span class="sxs-lookup"><span data-stu-id="2ea17-196">hello following sample shows how tooretrieve hello name server names assigned toohello zone.</span></span> <span data-ttu-id="2ea17-197">IT 也會示範如何使用 tooquery hello"www"記錄`nslookup`。</span><span class="sxs-lookup"><span data-stu-id="2ea17-197">IT also shows how tooquery hello "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="2ea17-198">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="2ea17-198">Step 3.</span></span> <span data-ttu-id="2ea17-199">更新 DNS 委派</span><span class="sxs-lookup"><span data-stu-id="2ea17-199">Update DNS delegation</span></span>

<span data-ttu-id="2ea17-200">確認該 hello 區域已正確匯入，您需要 tooupdate hello DNS 委派 toopoint toohello 之後 Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="2ea17-200">After you have verified that hello zone has been imported correctly, you need tooupdate hello DNS delegation toopoint toohello Azure DNS name servers.</span></span> <span data-ttu-id="2ea17-201">如需詳細資訊，請參閱 hello 文章[更新 hello DNS 委派](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="2ea17-201">For more information, see hello article [Update hello DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="2ea17-202">從 Azure DNS 匯出 DNS 區域檔案</span><span class="sxs-lookup"><span data-stu-id="2ea17-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="2ea17-203">hello Azure CLI 命令 tooimport DNS 區域的 hello 格式如下：</span><span class="sxs-lookup"><span data-stu-id="2ea17-203">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="2ea17-204">值：</span><span class="sxs-lookup"><span data-stu-id="2ea17-204">Values:</span></span>

* <span data-ttu-id="2ea17-205">`<resource group>`是 hello hello 資源群組名稱 hello Azure DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="2ea17-205">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="2ea17-206">`<zone name>`這是 hello hello 區域名稱。</span><span class="sxs-lookup"><span data-stu-id="2ea17-206">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="2ea17-207">`<zone file name>`這是 hello 路徑/名稱 hello 區域檔案 toobe 匯出。</span><span class="sxs-lookup"><span data-stu-id="2ea17-207">`<zone file name>` is hello path/name of hello zone file toobe exported.</span></span>

<span data-ttu-id="2ea17-208">為 「 hello 區域匯入，您必須先 toosign 中的，選擇您的訂用，並設定 hello Azure CLI toouse Resource Manager 模式。</span><span class="sxs-lookup"><span data-stu-id="2ea17-208">As with hello zone import, you first need toosign in, choose your subscription, and configure hello Azure CLI toouse Resource Manager mode.</span></span>

### <a name="tooexport-a-zone-file"></a><span data-ttu-id="2ea17-209">tooexport 區域檔案</span><span class="sxs-lookup"><span data-stu-id="2ea17-209">tooexport a zone file</span></span>

1. <span data-ttu-id="2ea17-210">登入 tooyour Azure 訂用帳戶使用 Azure CLI hello。</span><span class="sxs-lookup"><span data-stu-id="2ea17-210">Sign in tooyour Azure subscription by using hello Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="2ea17-211">選取您想 toocreate DNS 區域的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ea17-211">Select hello subscription where you want toocreate your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="2ea17-212">Azure DNS 是僅能以 Azure 資源管理員運作的服務。</span><span class="sxs-lookup"><span data-stu-id="2ea17-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="2ea17-213">hello Azure CLI 必須交換的 tooResource 管理員模式。</span><span class="sxs-lookup"><span data-stu-id="2ea17-213">hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="2ea17-214">tooexport hello 現有 Azure DNS 區域**contoso.com**資源群組中**myresourcegroup** toohello 檔案**contoso.com.txt** （hello 目前的資料夾中），執行`azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="2ea17-214">tooexport hello existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** toohello file **contoso.com.txt** (in hello current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="2ea17-215">呼叫 hello Azure DNS 服務 tooenumerate 此命令會在 hello 區域記錄集，並匯出 hello 結果 tooa 繫結相容區域檔案。</span><span class="sxs-lookup"><span data-stu-id="2ea17-215">This command  calls hello Azure DNS service tooenumerate record sets in hello zone and export hello results tooa BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
