您可以使用透過企業解決方案產生的根憑證 (建議)，也可以產生自我簽署憑證。 建立 hello 根憑證之後, 匯出 hello 公開憑證資料 （不 hello 私密金鑰） 成 base-64 編碼 X.509.cer 檔案，並上傳 hello 公開憑證資料 tooAzure。

* **企業憑證：**如果您是使用企業解決方案，則可以使用現有的憑證鏈結。 取得您想 toouse hello 根憑證的 hello.cer 檔案。
* **自我簽署的根憑證：**如果您不使用企業憑證解決方案，您需要 toocreate 自我簽署的根憑證。 請務必遵循其中一種以下 hello P2S 憑證文章 hello 步驟。 否則，hello 您建立的憑證，將無法使用 P2S 連線相容，並嘗試 tooconnect 時，用戶端會收到連接錯誤。 其中一個 hello 下列文章中的 hello 步驟產生相容的憑證：

  * [Windows 10 PowerShell 指示](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md)： 這些指示需要 Windows 10 和 PowerShell toogenerate 憑證。 Hello 根憑證，從產生的用戶端憑證可以安裝在任何支援 P2S 用戶端。
  * [MakeCert 指示](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site-makecert.md)： 使用 MakeCert，如果您沒有存取 tooa Windows 10 電腦 toouse toogenerate 憑證。 MakeCert 已被取代，但您仍然可以使用 MakeCert toogenerate 憑證。 Hello 根憑證，從產生的用戶端憑證可以安裝在任何支援 P2S 用戶端。
