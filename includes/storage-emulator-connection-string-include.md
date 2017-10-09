hello 儲存體模擬器的共用金鑰驗證支援單一固定的帳戶及已知的驗證金鑰。 此帳戶和金鑰是 hello hello 儲存體模擬器搭配允許只共用金鑰認證。 如下：

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> hello hello 儲存體模擬器所支援的驗證金鑰僅供測試用戶端的驗證程式碼的 hello 功能。 它不提供任何安全性用途。 您不能使用您的生產儲存體帳戶與金鑰 hello 儲存體模擬器。 您不應該使用 hello 開發帳戶使用生產資料。
> 
> hello 儲存體模擬器支援僅透過 HTTP 連接。 不過，HTTPS 為建議用來存取 Azure 儲存體帳戶的生產環境中資源的通訊協定的 hello。
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a>使用快速鍵 toohello 模擬器帳戶連線
hello 最簡單方式 tooconnect toohello 儲存體模擬器從您的應用程式是 tooconfigure 參考 hello 快顯的應用程式組態檔中的連接字串`UseDevelopmentStorage=true`。 以下是範例連接字串 toohello 儲存體模擬器中*app.config*檔案： 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a>使用 hello 已知帳戶名稱和金鑰 toohello 模擬器帳戶連線
toocreate 參考 hello 模擬器帳戶名稱，以及索引鍵，您必須指定 hello 端點，每個 hello 服務您的連接字串會希望 toouse hello 連接字串中的 hello 模擬器。 這是必要的如此 hello 連接字串將參考 hello 模擬器端點，不同於生產儲存體帳戶。 例如，您的連接字串 hello 值看起來像這樣：

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

這個值是相同的 toohello 捷徑如上所示， `UseDevelopmentStorage=true`。

#### <a name="specify-an-http-proxy"></a>指定 HTTP proxy
當您要測試您的服務與 hello 儲存體模擬器，您也可以指定 HTTP proxy toouse。 這可用於偵錯對 hello 儲存體服務的作業時，觀察 HTTP 要求和回應。 toospecify proxy、 新增 hello`DevelopmentStorageProxyUri`選項 toohello 連接字串，並設定其值 toohello proxy 的 URI。 例如，以下是指向 toohello 儲存體模擬器，並且設定 HTTP proxy 的連接字串：

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

