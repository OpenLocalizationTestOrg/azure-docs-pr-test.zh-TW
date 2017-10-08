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
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a>匯入和匯出 DNS 區域檔案中使用 Azure CLI 1.0 hello 

這篇文章會引導您使用 Azure DNS tooimport 及匯出 DNS 區域檔案 hello Azure CLI 1.0 的方式。

## <a name="introduction-toodns-zone-migration"></a>簡介 tooDNS 區域移轉

DNS 區域檔案是文字檔，其中包含 hello 區域中的每個網域名稱系統 (DNS) 記錄的詳細資料。 它會遵循標準格式，使其適合於在 DNS 系統之間傳送 DNS 記錄。 使用區域檔案是快速、 可靠及方便 tootransfer 入或移出 Azure DNS 的 DNS 區域。

Azure DNS 支援匯入和匯出使用 hello Azure 命令列介面 (CLI) 的區域檔案。 區域檔案匯入**不**目前支援透過 Azure PowerShell 或 hello Azure 入口網站。

hello Azure CLI 1.0 是跨平台命令列工具，可用來管理 Azure 服務。 它是適用於從 hello hello Windows、 Mac 和 Linux 平台[Azure 下載頁面](https://azure.microsoft.com/downloads/)。 跨平台支援在進行匯入和匯出區域檔案，因為 hello 最常見的名稱伺服器軟體而言很重要[繫結](https://www.isc.org/downloads/bind/)，通常會在 Linux 上執行。

> [!NOTE]
> 目前有兩個 hello Azure CLI 版本。 CLI1.0 以 Node.js 為基礎，且命令以「azure」開頭。
> CLI2.0 以 Python 為基礎，且命令以「az」開頭。 雖然支援區域檔案匯入兩個版本中，我們建議使用 hello CLI1.0 命令，此頁面中所述。

## <a name="obtain-your-existing-dns-zone-file"></a>取得現有的 DNS 區域檔案

DNS 區域檔案匯入 Azure DNS 之前，您會需要 tooobtain hello 區域檔案的副本。 此檔案的 hello 來源取決於目前裝載 hello DNS 區域的位置。

* 如果您的 DNS 區域，由合作夥伴服務 （例如網域註冊機構、 專用的 DNS 主機服務提供者或替代的雲端提供者），該服務應該提供 hello 能力 toodownload hello DNS 區域檔案。
* 如果您的 DNS 區域主控 Windows DNS，hello hello 區域檔案的預設資料夾是**%systemroot%\system32\dns**。 hello 完整路徑 tooeach 區域檔案也會顯示在 [hello**一般**hello DNS 主控台] 索引標籤。
* 如果使用繫結裝載您的 DNS 區域，hello 繫結的組態檔中指定的 hello 區域檔案中每個區域的 hello 位置**named.conf**。

> [!NOTE]
> 下載自 GoDaddy 的區域檔案會有些微非標準格式。 您需要 toocorrect 此之前，您將這些區域檔案匯入 Azure DNS。
>
> Hello RDATA 的每個 DNS 記錄中的 DNS 名稱指定為完整名稱，但是沒有終止"。"這表示其他 DNS 系統會將這些名稱解譯為相對名稱。 您需要： tooedit hello 區域檔案 tooappend hello 終止 」。 「 tootheir 名稱之前您匯入 Azure DNS。
>
> 例如，hello"www 3600 CNAME contoso.com 中 」 的 CNAME 記錄應變更太"www 3600 IN CNAME contoso.com"。
> (結尾附加「.」)。

## <a name="import-a-dns-zone-file-into-azure-dns"></a>將 DNS 區域檔案匯入 Azure DNS

匯入區域檔案會在 Azure DNS 中建立新區域 (如果區域不存在)。 如果 hello 區域已經存在，hello hello 區域檔案中的資料錄集必須與合併 hello 現有資料錄集。

### <a name="merge-behavior"></a>合併行為

* 預設會合併現有和新的記錄集。 合併的資料錄集內相同的記錄會進行重複資料刪除。
* 或者，藉由指定 hello`--force`選項，hello 匯入程序來取代現有的資料錄集，與新的資料錄集。 不會移除現有的記錄集並沒有對應的記錄設定 hello 匯入的區域檔案中。
* 當合併資料錄集時，hello toolive (TTL) 預先存在的資料錄集的使用時間。 當`--force`是 hello hello 新資料錄集的 TTL 會使用。
* 啟動授權 (SOA) 參數 (除了`host`) 一定會取自 hello 匯入的區域檔案，而不論是否`--force`用。 同樣地，在 hello 區域的 apex 設定 hello 名稱伺服器記錄，hello TTL 一定是取自 hello 匯入的區域檔案。
* 匯入的 CNAME 記錄不會取代現有的 CNAME 記錄以相同的名稱，除非 hello hello`--force`指定參數。
* CNAME 記錄與另一筆記錄之間發生衝突時的 hello 相同名稱但不同類型 （不論它現有或新）、 hello 現有的記錄會保留。 這是獨立的 hello 使用`--force`。

### <a name="additional-information-about-importing"></a>匯入的其他資訊

hello 下列注意事項提供在 hello 區域相關的其他技術詳細資料匯入程序。

* hello`$TTL`指示詞是選擇性的而且受支援。 若未`$TTL`指示詞，匯入記錄，卻不明確的 TTL 設為 tooa 預設值為 3600 秒的 TTL。 當兩個記錄中 hello 相同的資料錄集指定不同的 Eap-ttls，使用 hello 較低的值。
* hello`$ORIGIN`指示詞是選擇性的而且受支援。 若未`$ORIGIN`設定 hello 預設使用的值是 hello hello 命令列上指定的區域名稱 (加上終止 hello"。")。
* hello`$INCLUDE`和`$GENERATE`指示詞不支援。
* 支援這些記錄類型：A、AAAA、CNAME、MX、NS、SOA、SRV 和 TXT。
* hello SOA 記錄會自動建立 Azure DNS 區域建立時。 當您匯入區域檔案時，將所有 SOA 參數都取自 hello 區域檔案*除了*hello`host`參數。 這個參數會使用 Azure DNS 所提供的 hello 值。 這是因為此參數必須參考 toohello 主要名稱伺服器提供的 Azure DNS。
* 設定在 hello 區域的 apex hello 名稱伺服器記錄也會建立自動由 Azure DNS 建立 hello 區域時。 只有 hello TTL 此記錄集的匯入。 這些記錄包含 hello Azure DNS 所提供的名稱伺服器名稱。 hello 記錄資料不會覆寫 hello hello 匯入的區域檔案中包含的值。
* 在公開預覽期間，Azure DNS 僅支援單一字串 TXT 記錄。 Multistring TXT 記錄都是串連與遭到截斷 too255 字元。

### <a name="cli-format-and-values"></a>CLI 格式和值

hello Azure CLI 命令 tooimport DNS 區域的 hello 格式如下：

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

值：

* `<resource group>`是 hello hello 資源群組名稱 hello Azure DNS 區域。
* `<zone name>`這是 hello hello 區域名稱。
* `<zone file name>`這是 hello 路徑/名稱 hello 區域檔案 toobe 匯入。

如果具有此名稱的區域不存在 hello 資源群組中，它會為您建立。 如果 hello 區域已經存在，hello 匯入的資料錄集與合併現有的資料錄集。 toooverwrite hello 現有資料錄集，使用 hello`--force`選項。

區域檔案，而不實際匯入它使用 hello tooverify hello 格式`--parse-only`選項。

### <a name="step-1-import-a-zone-file"></a>步驟 1. 匯入區域檔案

tooimport hello 區域的區域檔案**contoso.com**。

1. Tooyour Azure 訂用帳戶使用的登入 hello Azure CLI 1.0。

    ```azurecli
    azure login
    ```

2. 選取您想 toocreate 新的 DNS 區域的 hello 訂用帳戶。

    ```azurecli
    azure account set <subscription name>
    ```

3. Azure DNS 是 Azure 資源管理員服務，因此 hello Azure CLI 必須交換的 tooResource 管理員模式。

    ```azurecli
    azure config mode arm
    ```

4. 使用 hello Azure DNS 服務之前，您必須註冊訂用帳戶 toouse hello Microsoft.Network 資源提供者。 (每個訂用帳戶只需執行一次此作業)。

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. 如果您還沒有已經，您也需要 toocreate 資源管理員資源群組。

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. tooimport hello 區域**contoso.com** hello 檔案從**contoso.com.txt**到新的 DNS 區域 hello 資源群組中**myresourcegroup**，執行 hello 命令`azure network dns zone import`.<BR>這個命令載入 hello 區域檔案，並將它剖析。 hello 命令執行一系列的命令在 hello Azure DNS 服務 toocreate hello 區域和所有 hello 記錄都設定 hello 區域中。 在 hello 主控台視窗中，以及任何錯誤或警告的 hello 命令報告進度。 數列中建立資料錄集，因為可能需要幾分鐘的時間 tooimport 大型區域檔案。

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a>步驟 2. 確認 hello 區域

tooverify hello DNS 區域 hello 檔案匯入之後，您可以使用任何一種 hello 下列方法：

* 您可以使用下列 Azure CLI 命令的 hello 列出 hello 記錄：

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* 您可以使用 hello PowerShell cmdlet 列出 hello 記錄`Get-AzureRmDnsRecordSet`。
* 您可以使用`nslookup`tooverify hello 記錄的名稱解析。 因為 hello 區域不尚未委派，會明確需要 toospecify hello 正確 Azure DNS 名稱伺服器。 hello 下列範例顯示如何 tooretrieve hello 名稱伺服器名稱指定 toohello 區域。 IT 也會示範如何使用 tooquery hello"www"記錄`nslookup`。

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

### <a name="step-3-update-dns-delegation"></a>步驟 3. 更新 DNS 委派

確認該 hello 區域已正確匯入，您需要 tooupdate hello DNS 委派 toopoint toohello 之後 Azure DNS 名稱伺服器。 如需詳細資訊，請參閱 hello 文章[更新 hello DNS 委派](dns-domain-delegation.md)。

## <a name="export-a-dns-zone-file-from-azure-dns"></a>從 Azure DNS 匯出 DNS 區域檔案

hello Azure CLI 命令 tooimport DNS 區域的 hello 格式如下：

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

值：

* `<resource group>`是 hello hello 資源群組名稱 hello Azure DNS 區域。
* `<zone name>`這是 hello hello 區域名稱。
* `<zone file name>`這是 hello 路徑/名稱 hello 區域檔案 toobe 匯出。

為 「 hello 區域匯入，您必須先 toosign 中的，選擇您的訂用，並設定 hello Azure CLI toouse Resource Manager 模式。

### <a name="tooexport-a-zone-file"></a>tooexport 區域檔案

1. 登入 tooyour Azure 訂用帳戶使用 Azure CLI hello。

    ```azurecli
    azure login
    ```

2. 選取您想 toocreate DNS 區域的 hello 訂用帳戶。

    ```azurecli
    azure account set <subscription name>
    ```

3. Azure DNS 是僅能以 Azure 資源管理員運作的服務。 hello Azure CLI 必須交換的 tooResource 管理員模式。

    ```azurecli
    azure config mode arm
    ```

4. tooexport hello 現有 Azure DNS 區域**contoso.com**資源群組中**myresourcegroup** toohello 檔案**contoso.com.txt** （hello 目前的資料夾中），執行`azure network dns zone export`. 呼叫 hello Azure DNS 服務 tooenumerate 此命令會在 hello 區域記錄集，並匯出 hello 結果 tooa 繫結相容區域檔案。

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
