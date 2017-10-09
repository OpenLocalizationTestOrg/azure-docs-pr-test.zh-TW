### <a name="record-names"></a>記錄名稱

在 Azure DNS 中，記錄是使用相對名稱來指定。 A*完整*網域名稱 (FQDN) 包含 hello 區域名稱，而*相對*名稱並不會。 例如，hello 相對記錄名稱 'www' hello 區域 'contoso.com' 中提供 hello 完整的記錄名稱 'www.contoso.com'。

*Apex*記錄是在 hello 根目錄的 DNS 記錄 (或*apex*) 的 DNS 區域。 例如，在 hello DNS 區域 'contoso.com' apex 記錄也有 hello 完整限定的名稱 'contoso.com' (這有時候稱為*naked*網域)。  依照慣例，hello 相對名稱 ' @' 是使用的 toorepresent apex 記錄。

### <a name="record-types"></a>記錄類型

每一筆 DNS 記錄都有名稱和類型。 記錄會組織成各種型別根據 toohello 它們包含的資料。 hello 最常見的類型為 'A' 記錄，其對應名稱 tooan IPv4 位址。 另一個常見的類型為 'MX' 記錄，其對應名稱 tooa 郵件伺服器。

Azure DNS 支援所有常見的 DNS 記錄類型：A、AAAA、CNAME、MX、NS、PTR、SOA、SRV 和 TXT。 請注意，[SPF 記錄是使用 TXT 記錄表示](../articles/dns/dns-zones-records.md#spf-records)。

### <a name="record-sets"></a>記錄集

有時候您需要 toocreate 一個以上的 DNS 記錄，具有給定名稱和型別。 例如，假設 hello 'www.contoso.com' 的網站裝載於兩個不同的 IP 位址。 hello 網站需要兩個不同的記錄，其中每個 IP 位址。 以下是記錄集的範例：

    www.contoso.com.        3600    IN    A    134.170.185.46
    www.contoso.com.        3600    IN    A    134.170.188.221

Azure DNS 使用「記錄集」來管理所有 DNS 記錄。 資料錄集 (也稱為*資源*記錄集) 是有相同名稱，以及屬於 hello hello 的 DNS 記錄在區域中的 hello 集合相同的型別。 大部分的記錄集只包含單一記錄。 不過，類似上述其中一個 hello 範例中設定記錄包含多個記錄，並不常見。

例如，假設您已經建立 A 記錄 'www' hello 'contoso.com' 」 區域中，指向 toohello IP 位址 '134.170.185.46' （hello 第一筆記錄上述）。  toocreate hello 第二筆記錄會將記錄 toohello 現有記錄的設定，，而不是建立一組額外的記錄。

hello SOA 和 CNAME 記錄類型是例外狀況。 hello DNS 標準不允許以 hello 相同的名稱，這些類型的多筆記錄，因此這些資料錄集只能包含單一記錄。
