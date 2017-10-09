hello[適用於.NET 的 Microsoft Azure Configuration Manager 程式庫](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)剖析從組態檔的連接字串提供的類別。 hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx)類別剖析無論 hello 用戶端應用程式在 hello 桌面上，在 Azure 的虛擬機器，或在 Azure 雲端服務中的行動裝置上執行的組態設定。

tooreference hello CloudConfigurationManager 封裝，加入下列 hello`using`指示詞：

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

以下是示範如何 tooretrieve 連接字串從組態檔的範例：

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

使用 hello Azure 組態管理員是選擇性的。 您也可以使用像是 hello.NET Framework API [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx)類別。

