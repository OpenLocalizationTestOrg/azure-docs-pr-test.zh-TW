## <a name="create-a-ruby-application"></a>建立 Ruby 應用程式
如需指示，請參閱[在 Azure 上建立 Ruby 應用程式](../articles/virtual-machines/linux/classic/ruby-rails-web-app.md)。

## <a name="configure-your-application-to-use-service-bus"></a>設定應用程式以使用服務匯流排
若要使用服務匯流排，請下載並使用 Azure Ruby 套件，其中包含一組能與儲存體 REST 服務通訊的便利程式庫。

### <a name="use-rubygems-to-obtain-the-package"></a>使用 RubyGems 來取得套件
1. 使用命令列介面，例如 **PowerShell** (Windows)、**Terminal** (Mac) 或 **Bash** (Unix)。
2. 在命令視窗中鍵入 "gem install azure" 以安裝 Gem 和相依性。

### <a name="import-the-package"></a>匯入封裝
使用您偏好的文字編輯器，將以下內容加入至您打算使用儲存體的 Ruby 檔案頂端：

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a>設定服務匯流排連接
您可以使用下列程式碼來設定命名空間、金鑰名稱、金鑰、簽署者和主機的值︰

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

將命名空間值設為您建立的值而非整個 URL。 例如，使用 **"yourexamplenamespace"** 而非 "yourexamplenamespace.servicebus.windows.net"。
