---
title: "使用 Azure CLI 1.0 將網域區域匯入和匯出至 Azure DNS | Microsoft Docs"
description: "了解如何使用 Azure CLI 1.0 匯入和匯出 DNS 區域檔案至 Azure DNS"
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
ms.openlocfilehash: d6d3fa7aa0e8b2462b3a6b4b66d3d87ab5535314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="import-and-export-a-dns-zone-file-using-the-azure-cli-10"></a><span data-ttu-id="2b325-103">使用 Azure CLI 1.0 匯入和匯出 DNS 區域檔案</span><span class="sxs-lookup"><span data-stu-id="2b325-103">Import and export a DNS zone file using the Azure CLI 1.0</span></span> 

<span data-ttu-id="2b325-104">本文會引導您了解如何使用 Azure CLI 1.0 匯入和匯出 Azure DNS 的 DNS 區域檔案。</span><span class="sxs-lookup"><span data-stu-id="2b325-104">This article walks you through how to import and export DNS zone files for Azure DNS using the Azure CLI 1.0.</span></span>

## <a name="introduction-to-dns-zone-migration"></a><span data-ttu-id="2b325-105">DNS 區域移轉簡介</span><span class="sxs-lookup"><span data-stu-id="2b325-105">Introduction to DNS zone migration</span></span>

<span data-ttu-id="2b325-106">DNS 區域檔案是一個文字檔，其中包含區域中每筆網域名稱系統 (DNS) 記錄的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2b325-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in the zone.</span></span> <span data-ttu-id="2b325-107">它會遵循標準格式，使其適合於在 DNS 系統之間傳送 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="2b325-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="2b325-108">使用區域檔案是從 Azure DNS 移入或移出 DNS 區域的快速、可靠又方便的方法。</span><span class="sxs-lookup"><span data-stu-id="2b325-108">Using a zone file is a quick, reliable, and convenient way to transfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="2b325-109">Azure DNS 支援使用 Azure 命令列介面 (CLI) 匯入和匯出區域檔案。</span><span class="sxs-lookup"><span data-stu-id="2b325-109">Azure DNS supports importing and exporting zone files by using the Azure command-line interface (CLI).</span></span> <span data-ttu-id="2b325-110">目前並「不」支援透過 Azure PowerShell 或 Azure 入口網站進行區域檔案匯入。</span><span class="sxs-lookup"><span data-stu-id="2b325-110">Zone file import is **not** currently supported via Azure PowerShell or the Azure portal.</span></span>

<span data-ttu-id="2b325-111">Azure CLI 1.0 是用來管理 Azure 服務的跨平台命令列工具。</span><span class="sxs-lookup"><span data-stu-id="2b325-111">The Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="2b325-112">它可從 [Azure 下載頁面](https://azure.microsoft.com/downloads/)取得，且適用於 Windows、Mac 及 Linux 平台。</span><span class="sxs-lookup"><span data-stu-id="2b325-112">It is available for the Windows, Mac, and Linux platforms from the [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="2b325-113">跨平台支援對於匯入和匯出區域檔案十分重要，因為最常見的名稱伺服器軟體 [BIND](https://www.isc.org/downloads/bind/) 通常會在 Linux 上執行。</span><span class="sxs-lookup"><span data-stu-id="2b325-113">Cross-platform support is important for importing and exporting zone files, because the most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="2b325-114">目前提供兩個版本的 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="2b325-114">There are currently two versions of the Azure CLI.</span></span> <span data-ttu-id="2b325-115">CLI1.0 以 Node.js 為基礎，且命令以「azure」開頭。</span><span class="sxs-lookup"><span data-stu-id="2b325-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="2b325-116">CLI2.0 以 Python 為基礎，且命令以「az」開頭。</span><span class="sxs-lookup"><span data-stu-id="2b325-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="2b325-117">雖然這兩個版本都支援區域檔案匯入，我們建議使用 CLI1.0 命令，如本頁面中所述。</span><span class="sxs-lookup"><span data-stu-id="2b325-117">While zone file import is supported in both versions, we recommend using the CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="2b325-118">取得現有的 DNS 區域檔案</span><span class="sxs-lookup"><span data-stu-id="2b325-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="2b325-119">將 DNS 區域檔案匯入 Azure DNS 之前，您必須取得區域檔案的複本。</span><span class="sxs-lookup"><span data-stu-id="2b325-119">Before you import a DNS zone file into Azure DNS, you need to obtain a copy of the zone file.</span></span> <span data-ttu-id="2b325-120">此檔案的來源取決於目前裝載 DNS 區域的位置。</span><span class="sxs-lookup"><span data-stu-id="2b325-120">The source of this file depends on where the DNS zone is currently hosted.</span></span>

* <span data-ttu-id="2b325-121">如果 DNS 區域是由合作夥伴服務 (例如網域註冊機構、專用 DNS 主機服務提供者或其他雲端提供者) 託管，該服務應提供下載 DNS 區域檔案的能力。</span><span class="sxs-lookup"><span data-stu-id="2b325-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide the ability to download the DNS zone file.</span></span>
* <span data-ttu-id="2b325-122">如果 DNS 區域託管在 Windows DNS 上，區域檔案的預設資料夾是 **%systemroot%\system32\dns**。</span><span class="sxs-lookup"><span data-stu-id="2b325-122">If your DNS zone is hosted on Windows DNS, the default folder for the zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="2b325-123">DNS 主控台的 [一般] 索引標籤上，也會顯示每個區域檔案的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="2b325-123">The full path to each zone file also shows on the **General** tab of the DNS console.</span></span>
* <span data-ttu-id="2b325-124">如果使用 BIND 裝載 DNS 區域，則 BIND 組態檔 **named.conf**中會指定每個區域的區域檔案位置。</span><span class="sxs-lookup"><span data-stu-id="2b325-124">If your DNS zone is hosted by using BIND, the location of the zone file for each zone is specified in the BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="2b325-125">下載自 GoDaddy 的區域檔案會有些微非標準格式。</span><span class="sxs-lookup"><span data-stu-id="2b325-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="2b325-126">您必須先修正格式，再將這些區域檔案匯入 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="2b325-126">You need to correct this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="2b325-127">每個 DNS 記錄 RDATA 中的 DNS 名稱會指定為完整名稱，但是結尾沒有「.」。這表示其他 DNS 系統會將這些名稱解譯為相對名稱。</span><span class="sxs-lookup"><span data-stu-id="2b325-127">DNS names in the RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="2b325-128">將區域檔案匯入 Azure DNS 之前，您必須先加以編輯，以將結尾的 "." 附加至這些名稱。</span><span class="sxs-lookup"><span data-stu-id="2b325-128">You need to edit the zone file to append the terminating "." to their names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="2b325-129">例如，CNAME 記錄「www 3600 IN CNAME contoso.com」應變更為「www 3600 IN CNAME contoso.com.」。</span><span class="sxs-lookup"><span data-stu-id="2b325-129">For example, the CNAME record "www 3600 IN CNAME contoso.com" should be changed to "www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="2b325-130">(結尾附加「.」)。</span><span class="sxs-lookup"><span data-stu-id="2b325-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="2b325-131">將 DNS 區域檔案匯入 Azure DNS</span><span class="sxs-lookup"><span data-stu-id="2b325-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="2b325-132">匯入區域檔案會在 Azure DNS 中建立新區域 (如果區域不存在)。</span><span class="sxs-lookup"><span data-stu-id="2b325-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="2b325-133">如果區域已經存在，則區域檔案中的記錄集必須與現有的記錄集合併。</span><span class="sxs-lookup"><span data-stu-id="2b325-133">If the zone already exists, the record sets in the zone file must be merged with the existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="2b325-134">合併行為</span><span class="sxs-lookup"><span data-stu-id="2b325-134">Merge behavior</span></span>

* <span data-ttu-id="2b325-135">預設會合併現有和新的記錄集。</span><span class="sxs-lookup"><span data-stu-id="2b325-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="2b325-136">合併的資料錄集內相同的記錄會進行重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="2b325-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="2b325-137">或者，透過指定 `--force` 選項，匯入程序會以新的記錄集取代現有記錄集。</span><span class="sxs-lookup"><span data-stu-id="2b325-137">Alternatively, by specifying the `--force` option, the import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="2b325-138">不會移除在匯入的區域檔案中沒有對應記錄集的現有記錄集。</span><span class="sxs-lookup"><span data-stu-id="2b325-138">Existing record sets that do not have a corresponding record set in the imported zone file are not be removed.</span></span>
* <span data-ttu-id="2b325-139">合併記錄集時，會使用預先存在之記錄集的存留時間 (TTL)。</span><span class="sxs-lookup"><span data-stu-id="2b325-139">When record sets are merged, the time to live (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="2b325-140">使用 `--force` 時，會使用新記錄集的 TTL。</span><span class="sxs-lookup"><span data-stu-id="2b325-140">When `--force` is used, the TTL of the new record set is used.</span></span>
* <span data-ttu-id="2b325-141">無論是否使用 `--force`，起始點授權 (SOA) 參數 (`host` 除外) 一律取自匯入的區域檔案。</span><span class="sxs-lookup"><span data-stu-id="2b325-141">Start of Authority (SOA) parameters (except `host`) are always taken from the imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="2b325-142">同樣地，對於位於區域頂點的名稱伺服器記錄集，TTL 一律取自匯入的區域檔案。</span><span class="sxs-lookup"><span data-stu-id="2b325-142">Similarly, for the name server record set at the zone apex, the TTL is always taken from the imported zone file.</span></span>
* <span data-ttu-id="2b325-143">除非指定 `--force` 參數，否則匯入的 CNAME 記錄不會取代具有相同名稱的現有 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="2b325-143">An imported CNAME record does not replace an existing CNAME record with the same name unless the `--force` parameter is specified.</span></span>
* <span data-ttu-id="2b325-144">當 CNAME 記錄與另一筆同名但不同類型的記錄 (不論何者是現有或新的記錄) 之間發生衝突時，會保留現有的記錄。</span><span class="sxs-lookup"><span data-stu-id="2b325-144">When a conflict arises between a CNAME record and another record of the same name but different type (regardless of which is existing or new), the existing record is retained.</span></span> <span data-ttu-id="2b325-145">這與使用 `--force`無關。</span><span class="sxs-lookup"><span data-stu-id="2b325-145">This is independent of the use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="2b325-146">匯入的其他資訊</span><span class="sxs-lookup"><span data-stu-id="2b325-146">Additional information about importing</span></span>

<span data-ttu-id="2b325-147">下列幾點提供有關區域匯入程序的其他技術詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2b325-147">The following notes provide additional technical details about the zone import process.</span></span>

* <span data-ttu-id="2b325-148">`$TTL` 指示詞為選擇性並受到支援。</span><span class="sxs-lookup"><span data-stu-id="2b325-148">The `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="2b325-149">若未提供 `$TTL` 指示詞，會匯入沒有明確 TTL 的記錄，並設定為預設 TTL 3600 秒。</span><span class="sxs-lookup"><span data-stu-id="2b325-149">When no `$TTL` directive is given, records without an explicit TTL are imported set to a default TTL of 3600 seconds.</span></span> <span data-ttu-id="2b325-150">如果相同資料錄集中有兩筆記錄指定不同的 TTL，則會使用較低的值。</span><span class="sxs-lookup"><span data-stu-id="2b325-150">When two records in the same record set specify different TTLs, the lower value is used.</span></span>
* <span data-ttu-id="2b325-151">`$ORIGIN` 指示詞為選擇性並受到支援。</span><span class="sxs-lookup"><span data-stu-id="2b325-151">The `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="2b325-152">若未設定 `$ORIGIN` ，則使用的預設值是在命令列上指定的區域名稱 (加上結尾的 ".")。</span><span class="sxs-lookup"><span data-stu-id="2b325-152">When no `$ORIGIN` is set, the default value used is the zone name as specified on the command line (plus the terminating ".").</span></span>
* <span data-ttu-id="2b325-153">`$INCLUDE` 和 `$GENERATE` 指示詞不受支援。</span><span class="sxs-lookup"><span data-stu-id="2b325-153">The `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="2b325-154">支援這些記錄類型：A、AAAA、CNAME、MX、NS、SOA、SRV 和 TXT。</span><span class="sxs-lookup"><span data-stu-id="2b325-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="2b325-155">Azure DNS 會在建立區域時，自動建立 SOA 記錄。</span><span class="sxs-lookup"><span data-stu-id="2b325-155">The SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="2b325-156">當您匯入區域檔案時，所有 SOA 參數都會取自該區域檔案，但 `host` 參數*除外*。</span><span class="sxs-lookup"><span data-stu-id="2b325-156">When you import a zone file, all SOA parameters are taken from the zone file *except* the `host` parameter.</span></span> <span data-ttu-id="2b325-157">這個參數會使用 Azure DNS 所提供的值。</span><span class="sxs-lookup"><span data-stu-id="2b325-157">This parameter uses the value provided by Azure DNS.</span></span> <span data-ttu-id="2b325-158">這是因為此參數必須參照 Azure DNS 所提供的主要名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="2b325-158">This is because this parameter must refer to the primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="2b325-159">Azure DNS 也會在建立區域時，自動建立位於區域頂點的名稱伺服器記錄集。</span><span class="sxs-lookup"><span data-stu-id="2b325-159">The name server record set at the zone apex is also created automatically by Azure DNS when the zone is created.</span></span> <span data-ttu-id="2b325-160">只會匯入此記錄集的 TTL。</span><span class="sxs-lookup"><span data-stu-id="2b325-160">Only the TTL of this record set is imported.</span></span> <span data-ttu-id="2b325-161">這些記錄包含 Azure DNS 所提供的名稱伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="2b325-161">These records contain the name server names provided by Azure DNS.</span></span> <span data-ttu-id="2b325-162">所匯入區域檔案中包含的值不會覆寫記錄資料。</span><span class="sxs-lookup"><span data-stu-id="2b325-162">The record data is not overwritten by the values contained in the imported zone file.</span></span>
* <span data-ttu-id="2b325-163">在公開預覽期間，Azure DNS 僅支援單一字串 TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="2b325-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="2b325-164">Multistring TXT 記錄會串連起來並截斷為 255 個字元。</span><span class="sxs-lookup"><span data-stu-id="2b325-164">Multistring TXT records are be concatenated and truncated to 255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="2b325-165">CLI 格式和值</span><span class="sxs-lookup"><span data-stu-id="2b325-165">CLI format and values</span></span>

<span data-ttu-id="2b325-166">用來匯入 DNS 區域的 Azure CLI 命令格式為：</span><span class="sxs-lookup"><span data-stu-id="2b325-166">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="2b325-167">值：</span><span class="sxs-lookup"><span data-stu-id="2b325-167">Values:</span></span>

* <span data-ttu-id="2b325-168">`<resource group>` 是 Azure DNS 中區域的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="2b325-168">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="2b325-169">`<zone name>` 是區域的名稱。</span><span class="sxs-lookup"><span data-stu-id="2b325-169">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="2b325-170">`<zone file name>` 是要匯入之區域檔案的路徑/名稱。</span><span class="sxs-lookup"><span data-stu-id="2b325-170">`<zone file name>` is the path/name of the zone file to be imported.</span></span>

<span data-ttu-id="2b325-171">如果資源群組中不存在具有此名稱的區域，則會為您建立。</span><span class="sxs-lookup"><span data-stu-id="2b325-171">If a zone with this name does not exist in the resource group, it is created for you.</span></span> <span data-ttu-id="2b325-172">如果區域已經存在，則匯入的記錄集會與現有的記錄集合併。</span><span class="sxs-lookup"><span data-stu-id="2b325-172">If the zone already exists, the imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="2b325-173">若要覆寫現有的記錄集，請使用 `--force` 選項。</span><span class="sxs-lookup"><span data-stu-id="2b325-173">To overwrite the existing record sets, use the `--force` option.</span></span>

<span data-ttu-id="2b325-174">若要確認區域檔案的格式，但不實際進行匯入，請使用 `--parse-only` 選項。</span><span class="sxs-lookup"><span data-stu-id="2b325-174">To verify the format of a zone file without actually importing it, use the `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="2b325-175">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="2b325-175">Step 1.</span></span> <span data-ttu-id="2b325-176">匯入區域檔案</span><span class="sxs-lookup"><span data-stu-id="2b325-176">Import a zone file</span></span>

<span data-ttu-id="2b325-177">匯入 **contoso.com**區域的區域檔案。</span><span class="sxs-lookup"><span data-stu-id="2b325-177">To import a zone file for the zone **contoso.com**.</span></span>

1. <span data-ttu-id="2b325-178">使用 Azure CLI 1.0 登入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b325-178">Sign in to your Azure subscription by using the Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="2b325-179">選取您要建立新的 DNS 區域的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b325-179">Select the subscription where you want to create your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="2b325-180">Azure DNS 是僅供 Azure 資源管理員使用的服務，因此 Azure CLI 必須切換到資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="2b325-180">Azure DNS is an Azure Resource Manager-only service, so the Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="2b325-181">使用 Azure DNS 服務之前，您必須註冊您的訂用帳戶才能使用 Microsoft.Network 資源提供者</span><span class="sxs-lookup"><span data-stu-id="2b325-181">Before you use the Azure DNS service, you must register your subscription to use the Microsoft.Network resource provider.</span></span> <span data-ttu-id="2b325-182">(每個訂用帳戶只需執行一次此作業)。</span><span class="sxs-lookup"><span data-stu-id="2b325-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="2b325-183">如果您還沒有 Resource Manager 資源群組，您也必須加以建立。</span><span class="sxs-lookup"><span data-stu-id="2b325-183">If you don't have one already, you also need to create a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="2b325-184">若要將 **contoso.com.txt** 檔案中的 **contoso.com** 區域匯入至 **myresourcegroup** 資源群組中的新 DNS 區域，請執行命令 `azure network dns zone import`。</span><span class="sxs-lookup"><span data-stu-id="2b325-184">To import the zone **contoso.com** from the file **contoso.com.txt** into a new DNS zone in the resource group **myresourcegroup**, run the command `azure network dns zone import`.</span></span><BR><span data-ttu-id="2b325-185">此命令會載入並剖析該區域檔案。</span><span class="sxs-lookup"><span data-stu-id="2b325-185">This command loads the zone file and parse it.</span></span> <span data-ttu-id="2b325-186">此命令會在 Azure DNS 服務上執行一系列的命令，以建立區域和區域中的所有記錄集。</span><span class="sxs-lookup"><span data-stu-id="2b325-186">The command executes a series of commands on the Azure DNS service to create the zone and all the record sets in the zone.</span></span> <span data-ttu-id="2b325-187">此命令會在主控台視窗中報告進度，以及任何的錯誤或警告。</span><span class="sxs-lookup"><span data-stu-id="2b325-187">The command reports progress in the console window, along with any errors or warnings.</span></span> <span data-ttu-id="2b325-188">由於記錄集是以系列方式建立，可能需要幾分鐘的時間來匯入大型的區域檔案。</span><span class="sxs-lookup"><span data-stu-id="2b325-188">Because record sets are created in series, it may take a few minutes to import a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-the-zone"></a><span data-ttu-id="2b325-189">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="2b325-189">Step 2.</span></span> <span data-ttu-id="2b325-190">確認區域</span><span class="sxs-lookup"><span data-stu-id="2b325-190">Verify the zone</span></span>

<span data-ttu-id="2b325-191">若要在匯入檔案之後確認 DNS 區域，您可以使用下列任何一個方法︰</span><span class="sxs-lookup"><span data-stu-id="2b325-191">To verify the DNS zone after you import the file, you can use any one of the following methods:</span></span>

* <span data-ttu-id="2b325-192">您可以使用下列 Azure CLI 命令來列出記錄：</span><span class="sxs-lookup"><span data-stu-id="2b325-192">You can list the records by using the following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="2b325-193">您可以使用 PowerShell Cmdlet `Get-AzureRmDnsRecordSet`來列出記錄。</span><span class="sxs-lookup"><span data-stu-id="2b325-193">You can list the records by using the PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="2b325-194">您可以使用 `nslookup` 來驗證記錄的名稱解析。</span><span class="sxs-lookup"><span data-stu-id="2b325-194">You can use `nslookup` to verify name resolution for the records.</span></span> <span data-ttu-id="2b325-195">因為尚未委派區域，所以您必須明確指定正確的 Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="2b325-195">Because the zone isn't delegated yet, you need to specify the correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="2b325-196">下列範例顯示如何擷取已指派給區域的名稱伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="2b325-196">The following sample shows how to retrieve the name server names assigned to the zone.</span></span> <span data-ttu-id="2b325-197">IT 也會示範如何使用 `nslookup`查詢 "www" 記錄。</span><span class="sxs-lookup"><span data-stu-id="2b325-197">IT also shows how to query the "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up the DNS Record Set "@" of type "NS"
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

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="2b325-198">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="2b325-198">Step 3.</span></span> <span data-ttu-id="2b325-199">更新 DNS 委派</span><span class="sxs-lookup"><span data-stu-id="2b325-199">Update DNS delegation</span></span>

<span data-ttu-id="2b325-200">確認已正確匯入區域之後，必須更新 DNS 委派以指向 Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="2b325-200">After you have verified that the zone has been imported correctly, you need to update the DNS delegation to point to the Azure DNS name servers.</span></span> <span data-ttu-id="2b325-201">如需詳細資訊，請參閱 [更新 DNS 委派](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="2b325-201">For more information, see the article [Update the DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="2b325-202">從 Azure DNS 匯出 DNS 區域檔案</span><span class="sxs-lookup"><span data-stu-id="2b325-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="2b325-203">用來匯入 DNS 區域的 Azure CLI 命令格式為：</span><span class="sxs-lookup"><span data-stu-id="2b325-203">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="2b325-204">值：</span><span class="sxs-lookup"><span data-stu-id="2b325-204">Values:</span></span>

* <span data-ttu-id="2b325-205">`<resource group>` 是 Azure DNS 中區域的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="2b325-205">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="2b325-206">`<zone name>` 是區域的名稱。</span><span class="sxs-lookup"><span data-stu-id="2b325-206">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="2b325-207">`<zone file name>` 是要匯出之區域檔案的路徑/名稱。</span><span class="sxs-lookup"><span data-stu-id="2b325-207">`<zone file name>` is the path/name of the zone file to be exported.</span></span>

<span data-ttu-id="2b325-208">和區域匯入時一樣，您必須先登入，選擇訂用帳戶，然後設定 Azure CLI 以使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="2b325-208">As with the zone import, you first need to sign in, choose your subscription, and configure the Azure CLI to use Resource Manager mode.</span></span>

### <a name="to-export-a-zone-file"></a><span data-ttu-id="2b325-209">匯出區域檔案</span><span class="sxs-lookup"><span data-stu-id="2b325-209">To export a zone file</span></span>

1. <span data-ttu-id="2b325-210">使用 Azure CLI 登入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b325-210">Sign in to your Azure subscription by using the Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="2b325-211">選取您要建立 DNS 區域的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b325-211">Select the subscription where you want to create your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="2b325-212">Azure DNS 是僅能以 Azure 資源管理員運作的服務。</span><span class="sxs-lookup"><span data-stu-id="2b325-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="2b325-213">Azure CLI 必須切換為資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="2b325-213">The Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="2b325-214">若要將 **myresourcegroup** 資源群組中的現有 Azure DNS 區域 **contoso.com** 匯出至 **contoso.com.txt** 檔案 (在目前資料夾中)，請執行 `azure network dns zone export`。</span><span class="sxs-lookup"><span data-stu-id="2b325-214">To export the existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** to the file **contoso.com.txt** (in the current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="2b325-215">此命令會呼叫 Azure DNS 服務，以列舉區域中的記錄集，並將結果匯出至 BIND 相容的區域檔案。</span><span class="sxs-lookup"><span data-stu-id="2b325-215">This command  calls the Azure DNS service to enumerate record sets in the zone and export the results to a BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
