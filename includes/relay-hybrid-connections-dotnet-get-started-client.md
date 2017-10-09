### <a name="create-a-console-application"></a><span data-ttu-id="add38-101">建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="add38-101">Create a console application</span></span>

<span data-ttu-id="add38-102">首先，啟動 Visual Studio，並建立新的**主控台應用程式 (.NET Framework)** 專案。</span><span class="sxs-lookup"><span data-stu-id="add38-102">First, launch Visual Studio and create a new **Console App (.NET Framework)** project.</span></span>

### <a name="add-hello-relay-nuget-package"></a><span data-ttu-id="add38-103">加入 hello 轉送 NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="add38-103">Add hello Relay NuGet package</span></span>

1. <span data-ttu-id="add38-104">Hello 新建立的專案上按一下滑鼠右鍵，然後按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="add38-104">Right-click hello newly created project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="add38-105">按一下 hello**瀏覽** 索引標籤，然後搜尋 「 Microsoft.Azure.Relay 」 和選取 hello **Microsoft Azure 轉送**項目。</span><span class="sxs-lookup"><span data-stu-id="add38-105">Click hello **Browse** tab, then search for "Microsoft.Azure.Relay" and select hello **Microsoft Azure Relay** item.</span></span> <span data-ttu-id="add38-106">按一下**安裝**toocomplete hello 安裝，然後關閉此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="add38-106">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>

### <a name="write-some-code-toosend-messages"></a><span data-ttu-id="add38-107">撰寫一些程式碼 toosend 訊息</span><span class="sxs-lookup"><span data-stu-id="add38-107">Write some code toosend messages</span></span>

1. <span data-ttu-id="add38-108">取代現有的 hello`using`在 hello 與 hello 下列 hello Program.cs 檔案最上方的陳述式`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="add38-108">Replace hello existing `using` statements at hello top of hello Program.cs file with hello following `using` statements:</span></span>
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
    ```
2. <span data-ttu-id="add38-109">新增常數 toohello `Program` hello 混合式連線詳細資料的類別。</span><span class="sxs-lookup"><span data-stu-id="add38-109">Add constants toohello `Program` class for hello hybrid connection details.</span></span> <span data-ttu-id="add38-110">方括號中的 hello 預留位置取代為 hello 建立 hello 混合式連接時取得的值。</span><span class="sxs-lookup"><span data-stu-id="add38-110">Replace hello placeholders in brackets with hello values you obtained when creating hello hybrid connection.</span></span> <span data-ttu-id="add38-111">是確定 toouse hello 完整命名空間名稱：</span><span class="sxs-lookup"><span data-stu-id="add38-111">Be sure toouse hello fully qualified namespace name:</span></span>
   
    ```csharp
    private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
    private const string ConnectionName = "{HybridConnectionName}";
    private const string KeyName = "{SASKeyName}";
    private const string Key = "{SASKey}";
    ```
3. <span data-ttu-id="add38-112">新增下列方法 toohello hello`Program`類別：</span><span class="sxs-lookup"><span data-stu-id="add38-112">Add hello following method toohello `Program` class:</span></span>
   
    ```csharp
    private static async Task RunAsync()
    {
        Console.WriteLine("Enter lines of text toosend toohello server with ENTER");
   
        // Create a new hybrid connection client
        var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
        var client = new HybridConnectionClient(new Uri(String.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
        // Initiate hello connection
        var relayConnection = await client.CreateConnectionAsync();
   
        // We run two concurrent loops on hello connection. One 
        // reads input from hello console and writes it toohello connection 
        // with a stream writer. hello other reads lines of input from hello 
        // connection with a stream reader and writes them toohello console. 
        // Entering a blank line will shut down hello write task after 
        // sending it toohello server. hello server will then cleanly shut down
        // hello connection which will terminate hello read task.
   
        var reads = Task.Run(async () => {
            // Initialize hello stream reader over hello connection
            var reader = new StreamReader(relayConnection);
            var writer = Console.Out;
            do
            {
                // Read a full line of UTF-8 text up toonewline
                string line = await reader.ReadLineAsync();
                // if hello string is empty or null, we are done.
                if (String.IsNullOrEmpty(line))
                    break;
                // Write toohello console
                await writer.WriteLineAsync(line);
            }
            while (true);
        });
   
        // Read from hello console and write toohello hybrid connection
        var writes = Task.Run(async () => {
            var reader = Console.In;
            var writer = new StreamWriter(relayConnection) { AutoFlush = true };
            do
            {
                // Read a line form hello console
                string line = await reader.ReadLineAsync();
                // Write hello line out, also when it's empty
                await writer.WriteLineAsync(line);
                // Quit when hello line was empty
                if (String.IsNullOrEmpty(line))
                    break;
            }
            while (true);
        });
   
        // Wait for both tasks toocomplete
        await Task.WhenAll(reads, writes);
        await relayConnection.CloseAsync(CancellationToken.None);
    }
    ```
4. <span data-ttu-id="add38-113">新增下列一行程式碼 toohello hello`Main`方法在 hello`Program`類別。</span><span class="sxs-lookup"><span data-stu-id="add38-113">Add hello following line of code toohello `Main` method in hello `Program` class.</span></span>
   
    ```csharp
    RunAsync().GetAwaiter().GetResult();
    ```
   
    <span data-ttu-id="add38-114">Program.cs 看起來應該會像下面這樣。</span><span class="sxs-lookup"><span data-stu-id="add38-114">Here is what your Program.cs should look like.</span></span>
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
   
    namespace Client
    {
        class Program
        {
            private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
            private const string ConnectionName = "{HybridConnectionName}";
            private const string KeyName = "{SASKeyName}";
            private const string Key = "{SASKey}";
   
            static void Main(string[] args)
            {
                RunAsync().GetAwaiter().GetResult();
            }
   
            private static async Task RunAsync()
            {
                Console.WriteLine("Enter lines of text toosend toohello server with ENTER");
   
                // Create a new hybrid connection client
                var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
                var client = new HybridConnectionClient(new Uri(String.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
                // Initiate hello connection
                var relayConnection = await client.CreateConnectionAsync();
   
                // We run two conucrrent loops on hello connection. One 
                // reads input from hello console and writes it toohello connection 
                // with a stream writer. hello other reads lines of input from hello 
                // connection with a stream reader and writes them toohello console. 
                // Entering a blank line will shut down hello write task after 
                // sending it toohello server. hello server will then cleanly shut down
                // hello connection which will terminate hello read task.
   
                var reads = Task.Run(async () => {
                    // Initialize hello stream reader over hello connection
                    var reader = new StreamReader(relayConnection);
                    var writer = Console.Out;
                    do
                    {
                        // Read a full line of UTF-8 text up toonewline
                        string line = await reader.ReadLineAsync();
                        // If hello string is empty or null, we are done.
                        if (String.IsNullOrEmpty(line))
                            break;
                        // Write toohello console
                        await writer.WriteLineAsync(line);
                    }
                    while (true);
                });
   
                // Read from hello console and write toohello hybrid connection
                var writes = Task.Run(async () => {
                    var reader = Console.In;
                    var writer = new StreamWriter(relayConnection) { AutoFlush = true };
                    do
                    {
                        // Read a line form hello console
                        string line = await reader.ReadLineAsync();
                        // Write hello line out, also when it's empty
                        await writer.WriteLineAsync(line);
                        // Quit when hello line was empty
                        if (String.IsNullOrEmpty(line))
                            break;
                    }
                    while (true);
                });
   
                // Wait for both tasks toocomplete
                await Task.WhenAll(reads, writes);
                await relayConnection.CloseAsync(CancellationToken.None);
            }
        }
    }
    ```

