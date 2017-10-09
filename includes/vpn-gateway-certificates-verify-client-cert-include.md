如果您有連線問題，請檢查下列項目 hello:

- 如果您已匯出的用戶端憑證，請確定，您在匯出為.pfx 檔案使用 hello 預設值 '包含的所有憑證路徑中的 hello 憑證盡可能'。 當您匯出它使用此值時，也會一併匯出 hello 根憑證資訊。 Hello 憑證 hello 用戶端電腦上安裝時，會再會 hello 用戶端電腦上同時安裝 hello.pfx 檔案包含此 hello 根憑證。 hello 用戶端電腦必須安裝 hello 根憑證資訊。 toocheck，跳過**管理使用者憑證**並瀏覽過**受信任的根 Certification Authorities\Certificates**。 請確認已列出該 hello 根憑證。 必須要有為了讓驗證 toowork hello 根憑證。

- 如果您使用的憑證，發出使用企業 CA 解決方案有驗證問題，請檢查 hello hello 用戶端憑證的驗證順序。 您可以檢查 hello 驗證清單順序，按兩下 hello 用戶端憑證，並將太**詳細資料 > 增強金鑰使用方法**。 請確定 hello 清單會顯示 「 用戶端驗證 」 為 hello 第一個項目。 如果沒有，您需要的 tooissue hello 與 hello hello 清單中的第一個項目具有用戶端驗證的使用者範本為基礎的用戶端憑證。

- 如需其他 P2S 疑難排解詳細資訊，請參閱[針對 P2S 連線進行疑難排解](../articles/vpn-gateway/vpn-gateway-troubleshoot-vpn-point-to-site-connection-problems.md)。