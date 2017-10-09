## <a name="create-a-ruby-application"></a>建立 Ruby 應用程式
如需指示，請參閱[在 Azure 上建立 Ruby 應用程式](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)。

## <a name="configure-your-application-toouse-service-bus"></a>設定您的應用程式 tooUse 服務匯流排
服務匯流排 toouse 下載，並使用 hello Azure Ruby 封裝，其中包含一組與 hello 儲存體服務 REST 服務通訊的便利性程式庫。

### <a name="use-rubygems-tooobtain-hello-package"></a>使用 RubyGems tooobtain hello 套件
1. 使用命令列介面，例如 **PowerShell** (Windows)、**Terminal** (Mac) 或 **Bash** (Unix)。
2. 輸入健身安裝 azure 」 在 hello 命令視窗 tooinstall hello 健身和相依性。

### <a name="import-hello-package"></a>匯入 hello 封裝
使用您慣用的文字編輯器 中，加入下列 toohello 頂端 hello Ruby hello 想 toouse 儲存體的檔案：

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a>設定服務匯流排連接
使用 hello 下列程式碼的命名空間、 名稱 hello tooset hello 值金鑰、 金鑰、 簽署人和主機：

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

設定您建立而不是 hello 整個 URL hello 命名空間值 toohello 值。 例如，使用 **"yourexamplenamespace"** 而非 "yourexamplenamespace.servicebus.windows.net"。
