使用的 toospecifying 哪些電子郵件伺服器允許指定的網域名稱代表 toosend 電子郵件的寄件者原則架構 (SPF) 記錄。  正確設定 SPF 記錄是重要的 tooprevent 標示為 垃圾郵件' 電子郵件的收件者。

hello DNS Rfc 中推出新的 'SPF' 記錄類型 toosupport 這種情況。 toosupport 較舊的名稱伺服器，它們也允許 hello hello TXT 記錄類型 toospecify SPF 記錄使用。  模稜兩可能導致 tooconfusion，已由解決[RFC 7208](http://tools.ietf.org/html/rfc7208#section-3.1)。  這說明 SPF 記錄應該只能使用建立 hello TXT 記錄類型，且該 hello SPF 記錄類型已被取代。

**SPF 記錄受到 Azure DNS，並應使用 hello TXT 記錄類型建立。** 不支援 hello 過時 SPF 記錄類型。 當[DNS 區域檔案匯入](../articles/dns/dns-import-export.md)，任何使用 hello SPF 記錄類型的 SPF 記錄會轉換 toohello TXT 記錄類型。
