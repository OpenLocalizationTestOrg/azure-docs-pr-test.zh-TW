## <a name="configure-your-application-tooaccess-azure-storage"></a>設定您的應用程式 tooaccess Azure 儲存體
有兩種方式 tooauthenticate 您應用程式 tooaccess 存放服務：

* 共用金鑰：使用僅供測試用途的共用金鑰
* 共用存取簽章 (SAS)：使用適用於生產應用程式的 SAS

### <a name="shared-key"></a>共用金鑰
共用的金鑰驗證表示您的應用程式會使用您的帳戶名稱和帳戶金鑰 tooaccess 儲存體服務。 基於快速顯示 hello 如何 toouse 此程式庫，我們將使用此快速入門中的共用金鑰驗證。

> [!WARNING] 
> **共用金鑰驗證請只限於測試目的之用！** 您帳戶的名稱和帳戶金鑰，讓完整讀取/寫入存取 toohello 相關聯的儲存體帳戶，將會下載您的應用程式的分散式的 tooevery 人員。 這並「不是」  的實作方式，因為您的金鑰有可能遭到不受信任的用戶端破壞。
> 
> 

使用共用金鑰驗證時，您將會建立 [連接字串](../articles/storage/common/storage-configure-connection-string.md)。 hello 連接字串所組成：  

* hello **DefaultEndpointsProtocol** -您可以選擇 HTTP 或 HTTPS。 不過，強烈建議您使用 HTTPS。
* hello**帳戶名稱**-hello 的儲存體帳戶名稱
* hello**帳戶金鑰**-在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 tooyour 儲存體帳戶，然後按一下 hello**金鑰**圖示 toofind 這項資訊。
* (選擇性) **EndpointSuffix** - 這用於具有不同端點尾碼的儲存體服務，例如 Azure China 或 Azure 控管的區域。

使用共用金鑰驗證的連接字串的範例如下︰

`"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here"`

### <a name="shared-access-signatures-sas"></a>共用存取簽章 (SAS)
行動應用程式中，hello 建議使用 hello Azure 儲存體服務針對用戶端的驗證要求的方法是使用共用存取簽章 (SAS)。 SAS 可讓您 toogrant 用戶端存取 tooa 資源一段指定時間，與指定權限集。
Hello 儲存體帳戶擁有者，您將需要針對您的行動用戶端 tooconsume toogenerate SAS。 toogenerate hello SAS，您可能會想 toowrite 產生 hello SAS 散發的 toobe tooyour 用戶端的個別服務。 為了測試用途，您可以使用 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com)或 hello [Azure 入口網站](https://portal.azure.com)toogenerate SAS。 當您建立 hello SAS 時，您可以指定 hello 有效時間間隔的 hello 透過 SAS，以及 hello SAS 授權 toohello 用戶端 hello 權限。

hello 下列範例顯示如何 toouse 會 hello Microsoft Azure 儲存體總管 toogenerate SAS。

1. 如果您還沒有這麼做，[安裝 hello Microsoft Azure 儲存體總管](http://storageexplorer.com)
2. 連接 tooyour 訂用帳戶。
3. 按一下儲存體帳戶，然後在 hello 左下方的 hello [動作] 索引標籤上按一下。 您的 SAS，請按 「 取得共用存取簽章 」 toogenerate 「 連接字串 」。
4. 授與讀取和寫入權限在 hello 服務、 容器和物件層級 hello hello 儲存體帳戶的 blob 服務的 SAS 連接字串範例如下。
   
   `"SharedAccessSignature=sv=2015-04-05&ss=b&srt=sco&sp=rw&se=2016-07-21T18%3A00%3A00Z&sig=3ABdLOJZosCp0o491T%2BqZGKIhafF1nlM3MzESDDD3Gg%3D;BlobEndpoint=https://youraccount.blob.core.windows.net"`

如您所見，使用 SAS 時，您並不會在應用程式中公開您的帳戶金鑰。 您可以進一步了解 SAS 和使用 SAS 所取出的最佳作法[共用存取簽章： 了解 hello SAS 模型](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)。

