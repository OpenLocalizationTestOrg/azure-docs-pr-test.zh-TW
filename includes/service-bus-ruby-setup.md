## <a name="create-a-ruby-application"></a><span data-ttu-id="e2d29-101">建立 Ruby 應用程式</span><span class="sxs-lookup"><span data-stu-id="e2d29-101">Create a Ruby application</span></span>
<span data-ttu-id="e2d29-102">如需指示，請參閱[在 Azure 上建立 Ruby 應用程式](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)。</span><span class="sxs-lookup"><span data-stu-id="e2d29-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="e2d29-103">設定您的應用程式 tooUse 服務匯流排</span><span class="sxs-lookup"><span data-stu-id="e2d29-103">Configure Your application tooUse Service Bus</span></span>
<span data-ttu-id="e2d29-104">服務匯流排 toouse 下載，並使用 hello Azure Ruby 封裝，其中包含一組與 hello 儲存體服務 REST 服務通訊的便利性程式庫。</span><span class="sxs-lookup"><span data-stu-id="e2d29-104">toouse Service Bus, download and use hello Azure Ruby package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="e2d29-105">使用 RubyGems tooobtain hello 套件</span><span class="sxs-lookup"><span data-stu-id="e2d29-105">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="e2d29-106">使用命令列介面，例如 **PowerShell** (Windows)、**Terminal** (Mac) 或 **Bash** (Unix)。</span><span class="sxs-lookup"><span data-stu-id="e2d29-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="e2d29-107">輸入健身安裝 azure 」 在 hello 命令視窗 tooinstall hello 健身和相依性。</span><span class="sxs-lookup"><span data-stu-id="e2d29-107">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="e2d29-108">匯入 hello 封裝</span><span class="sxs-lookup"><span data-stu-id="e2d29-108">Import hello package</span></span>
<span data-ttu-id="e2d29-109">使用您慣用的文字編輯器 中，加入下列 toohello 頂端 hello Ruby hello 想 toouse 儲存體的檔案：</span><span class="sxs-lookup"><span data-stu-id="e2d29-109">Using your favorite text editor, add hello following toohello top of hello Ruby file in which you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="e2d29-110">設定服務匯流排連接</span><span class="sxs-lookup"><span data-stu-id="e2d29-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="e2d29-111">使用 hello 下列程式碼的命名空間、 名稱 hello tooset hello 值金鑰、 金鑰、 簽署人和主機：</span><span class="sxs-lookup"><span data-stu-id="e2d29-111">Use hello following code tooset hello values of namespace, name of hello key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="e2d29-112">設定您建立而不是 hello 整個 URL hello 命名空間值 toohello 值。</span><span class="sxs-lookup"><span data-stu-id="e2d29-112">Set hello namespace value toohello value you created rather than hello entire URL.</span></span> <span data-ttu-id="e2d29-113">例如，使用 **"yourexamplenamespace"** 而非 "yourexamplenamespace.servicebus.windows.net"。</span><span class="sxs-lookup"><span data-stu-id="e2d29-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
