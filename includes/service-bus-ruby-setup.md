## <a name="create-a-ruby-application"></a><span data-ttu-id="a4460-101">建立 Ruby 應用程式</span><span class="sxs-lookup"><span data-stu-id="a4460-101">Create a Ruby application</span></span>
<span data-ttu-id="a4460-102">如需指示，請參閱[在 Azure 上建立 Ruby 應用程式](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)。</span><span class="sxs-lookup"><span data-stu-id="a4460-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="a4460-103">設定應用程式以使用服務匯流排</span><span class="sxs-lookup"><span data-stu-id="a4460-103">Configure Your application to Use Service Bus</span></span>
<span data-ttu-id="a4460-104">若要使用服務匯流排，請下載並使用 Azure Ruby 套件，其中包含一組能與儲存體 REST 服務通訊的便利程式庫。</span><span class="sxs-lookup"><span data-stu-id="a4460-104">To use Service Bus, download and use the Azure Ruby package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="a4460-105">使用 RubyGems 來取得套件</span><span class="sxs-lookup"><span data-stu-id="a4460-105">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="a4460-106">使用命令列介面，例如 **PowerShell** (Windows)、**Terminal** (Mac) 或 **Bash** (Unix)。</span><span class="sxs-lookup"><span data-stu-id="a4460-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="a4460-107">在命令視窗中鍵入 "gem install azure" 以安裝 Gem 和相依性。</span><span class="sxs-lookup"><span data-stu-id="a4460-107">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="a4460-108">匯入封裝</span><span class="sxs-lookup"><span data-stu-id="a4460-108">Import the package</span></span>
<span data-ttu-id="a4460-109">使用您偏好的文字編輯器，將以下內容加入至您打算使用儲存體的 Ruby 檔案頂端：</span><span class="sxs-lookup"><span data-stu-id="a4460-109">Using your favorite text editor, add the following to the top of the Ruby file in which you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="a4460-110">設定服務匯流排連接</span><span class="sxs-lookup"><span data-stu-id="a4460-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="a4460-111">您可以使用下列程式碼來設定命名空間、金鑰名稱、金鑰、簽署者和主機的值︰</span><span class="sxs-lookup"><span data-stu-id="a4460-111">Use the following code to set the values of namespace, name of the key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="a4460-112">將命名空間值設為您建立的值而非整個 URL。</span><span class="sxs-lookup"><span data-stu-id="a4460-112">Set the namespace value to the value you created rather than the entire URL.</span></span> <span data-ttu-id="a4460-113">例如，使用 **"yourexamplenamespace"** 而非 "yourexamplenamespace.servicebus.windows.net"。</span><span class="sxs-lookup"><span data-stu-id="a4460-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
