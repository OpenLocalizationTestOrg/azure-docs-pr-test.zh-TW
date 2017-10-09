每個連線 tooa 的用戶端電腦使用點對站台的 VNet 必須安裝用戶端憑證。 hello 用戶端憑證是從 hello 根憑證產生並安裝在每部用戶端電腦上。 如果未安裝有效的用戶端憑證，而且 hello 用戶端會嘗試 tooconnect toohello VNet，驗證將會失敗。

您可以針對每個用戶端，產生唯一的憑證，或者您可以使用相同憑證的多個用戶端 hello。 hello 利用 toogenerating 唯一用戶端憑證是 hello 能力 toorevoke 單一憑證。 否則，如果多個用戶端使用 hello 相同的用戶端憑證，您需要 toorevoke，toogenerate 也可以為所有 hello 使用該憑證 tooauthenticate 的用戶端安裝新的憑證。

您可以產生用戶端憑證使用下列方法 hello:

- **企業憑證︰**

  - 如果您使用企業憑證解決方案時，產生用戶端憑證與 hello 通用名稱值格式 'name@yourdomain.com'，而不是 hello '網域名稱 \ 使用者名稱' 格式。
  - 請確定 hello 用戶端憑證以與 hello 在 hello 使用清單中，第一個項目具有 「 用戶端驗證 ' hello 'User' 憑證範本為基礎，而不是智慧卡登入等。您可以按兩下 hello 用戶端憑證，並檢視檢查 hello 憑證**詳細資料 > 增強金鑰使用方法**。

- **自我簽署的根憑證：**務必遵循其中一種以下 hello P2S 憑證文章 hello 步驟。 否則，hello 您建立的用戶端憑證，將無法使用 P2S 連線相容，並嘗試 tooconnect 時，用戶端會收到錯誤訊息。 其中一個 hello 下列文章中的 hello 步驟產生相容的用戶端憑證： 

  * [Windows 10 PowerShell 指示](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientcert)： 這些指示需要 Windows 10 和 PowerShell toogenerate 憑證。 產生的 hello 憑證可以安裝在任何支援 P2S 用戶端。
  * [MakeCert 指示](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site-makecert.md)： 使用 MakeCert，如果您沒有存取 tooa Windows 10 電腦 toouse toogenerate 憑證。 MakeCert 已被取代，但您仍然可以使用 MakeCert toogenerate 憑證。 產生的 hello 憑證可以安裝在任何支援 P2S 用戶端。

  當您從使用上述指示 hello 的自我簽署的根憑證產生用戶端憑證時，它具有電腦上自動安裝 hello toogenerate 有使用它。 如果您想 tooinstall 另一部用戶端電腦上的用戶端憑證，您需要 tooexport 成.pfx，連同 hello 整個憑證鏈結。 這會建立.pfx 檔案，其中包含所需 hello 用戶端 toosuccessfully 驗證 hello 根憑證資訊。 步驟 tooexport 憑證，請參閱[憑證-匯出用戶端憑證](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientexport)。
