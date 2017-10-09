<span data-ttu-id="9ff4a-101">hello[適用於.NET 的 Microsoft Azure Configuration Manager 程式庫](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)剖析從組態檔的連接字串提供的類別。</span><span class="sxs-lookup"><span data-stu-id="9ff4a-101">hello [Microsoft Azure Configuration Manager Library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) provides a class for parsing a connection string from a configuration file.</span></span> <span data-ttu-id="9ff4a-102">hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx)類別剖析無論 hello 用戶端應用程式在 hello 桌面上，在 Azure 的虛擬機器，或在 Azure 雲端服務中的行動裝置上執行的組態設定。</span><span class="sxs-lookup"><span data-stu-id="9ff4a-102">hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) class parses configuration settings regardless of whether hello client application is running on hello desktop, on a mobile device, in an Azure virtual machine, or in an Azure cloud service.</span></span>

<span data-ttu-id="9ff4a-103">tooreference hello CloudConfigurationManager 封裝，加入下列 hello`using`指示詞：</span><span class="sxs-lookup"><span data-stu-id="9ff4a-103">tooreference hello CloudConfigurationManager package, add hello following `using` directive:</span></span>

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

<span data-ttu-id="9ff4a-104">以下是示範如何 tooretrieve 連接字串從組態檔的範例：</span><span class="sxs-lookup"><span data-stu-id="9ff4a-104">Here's an example that shows how tooretrieve a connection string from a configuration file:</span></span>

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

<span data-ttu-id="9ff4a-105">使用 hello Azure 組態管理員是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="9ff4a-105">Using hello Azure Configuration Manager is optional.</span></span> <span data-ttu-id="9ff4a-106">您也可以使用像是 hello.NET Framework API [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx)類別。</span><span class="sxs-lookup"><span data-stu-id="9ff4a-106">You can also use an API like hello .NET Framework's [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) class.</span></span>

