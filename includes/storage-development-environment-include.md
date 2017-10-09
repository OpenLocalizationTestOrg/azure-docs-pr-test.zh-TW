## <a name="set-up-your-development-environment"></a>設定開發環境
接下來，設定 Visual Studio 中開發環境，因此您已經準備好 tootry hello 本指南中的程式碼範例。

### <a name="create-a-windows-console-application-project"></a>建立 Windows 主控台應用程式專案
在 Visual Studio 中，建立新的 Windows 主控台應用程式。 下列步驟的 hello 顯示 toocreate 2017，不過，hello 步驟的 Visual Studio 中的主控台應用程式的方式類似在其他版本的 Visual Studio。

1. 選取 [檔案] > [新增] > [專案]
2. 選取 [安裝] > [範本] > [Visual C#] > [Windows 傳統桌面]
3. 選取 **主控台應用程式 (.NET Framework)**
4. 輸入您的應用程式的名稱在 hello**名稱：**欄位
5. 選取 [確定]

![Visual Studio 中的專案建立對話方塊](./media/storage-development-environment-include/storage-development-environment-include-1.png)

本教學課程中的所有程式碼範例可加入 toohello`Main()`的主控台應用程式的方法`Program.cs`檔案。

您可以在任何類型的.NET 應用程式，包括 Azure 雲端服務或 web 應用程式和桌上型電腦與行動應用程式中使用 hello Azure 儲存體用戶端程式庫。 在本指南中，為求簡化，我們會使用主控台應用程式。

### <a name="use-nuget-tooinstall-hello-required-packages"></a>使用 NuGet tooinstall hello 必要封裝
有兩個封裝，您需要 tooreference 專案 toocomplete 在本教學課程：

* [Microsoft Azure 儲存體用戶端程式庫適用於.NET](https://www.nuget.org/packages/WindowsAzure.Storage/)： 此封裝提供以程式設計方式存取 toodata 儲存體帳戶中的資源。
* [適用於 .NET 的 Microsoft Azure Configuration Manager 程式庫](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)︰此套件提供一個類別，無論您的應用程式於何處執行，均可用來剖析組態檔中的連接字串。

您可以使用 NuGet tooobtain 這兩個封裝。 請遵循下列步驟：

1. 在 [方案總管] 中以滑鼠右鍵按一下專案，然後選擇 [管理 NuGet 封裝]。
2. 線上搜尋"WindowsAzure.Storage"，然後按一下**安裝**tooinstall hello 儲存體用戶端程式庫和其相依性。
3. 線上搜尋"WindowsAzure.ConfigurationManager 」，然後按一下**安裝**tooinstall hello Azure 組態管理員。

> [!NOTE]
> hello 儲存體用戶端程式庫封裝也會包含在 hello [Azure SDK for.NET](https://azure.microsoft.com/downloads/)。 不過，我們建議您也從永遠有 hello hello 用戶端程式庫的最新版本的 NuGet tooensure 安裝 hello 儲存體用戶端程式庫。
> 
> 在不是從 WCF 資料服務的 NuGet 上可用的 hello ODataLib 封裝來解析 hello hello 適用於.NET 的儲存體用戶端程式庫中的 ODataLib 相依性。 hello ODataLib 程式庫可以下載直接或透過 NuGet 您程式碼專案所參考。 hello hello 儲存體用戶端程式庫所使用特定 ODataLib 封裝包括[OData](http://nuget.org/packages/Microsoft.Data.OData/)， [Edm](http://nuget.org/packages/Microsoft.Data.Edm/)，和[空間](http://nuget.org/packages/System.Spatial/)。 雖然這些程式庫類別所使用的 hello Azure 資料表儲存體，它們是必要的相依性以 hello 儲存體用戶端程式庫的程式設計。
> 
> 

### <a name="determine-your-target-environment"></a>決定您的目標環境
您有兩個環境選項執行本指南中的 hello 範例：

* 您可以針對 Azure 儲存體帳戶 hello 雲端中執行您的程式碼。 
* 您可以對 hello Azure 儲存體模擬器中執行您的程式碼。 hello 儲存體模擬器是模擬 hello 雲端中的 Azure 儲存體帳戶的本機環境。 hello 模擬器是進行測試和偵錯您的程式碼，在開發您的應用程式時可用的選項。 hello 模擬器會使用已知的帳戶和金鑰。 如需詳細資訊，請參閱[使用 hello Azure 儲存體模擬器進行開發和測試](../articles/storage/common/storage-use-emulator.md)

如果您的目標儲存體帳戶 hello 雲端中的，複製 hello Azure 入口網站儲存體帳戶的 hello 主要存取金鑰。 如需詳細資訊，請參閱 [檢視和複製儲存體存取金鑰](../articles/storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys)。

> [!NOTE]
> 您可以針對 hello 儲存體模擬器 tooavoid 支出任何 Azure 儲存體相關聯的成本。 不過，如果您選擇 tootarget Azure 儲存體帳戶 hello 雲端中，執行本教學課程的成本將會造成影響。
> 
> 

### <a name="configure-your-storage-connection-string"></a>設定儲存體連接字串
hello 適用於.NET 的 Azure 儲存體用戶端程式庫支援使用儲存體連接字串 tooconfigure 端點和認證來存取儲存體服務。 最佳的方式 toomaintain hello 您儲存體連接字串是在組態檔中。 

如需連接字串的詳細資訊，請參閱[設定儲存體的連接字串 tooAzure](../articles/storage/common/storage-configure-connection-string.md)。

> [!NOTE]
> 儲存體帳戶金鑰是儲存體帳戶的類似 toohello 根密碼。 永遠是小心 tooprotect 儲存體帳戶金鑰。 避免將其散發 tooother 使用者，硬式編碼，或將它儲存為可存取 tooothers 純文字檔案中。 重新產生金鑰使用 hello Azure 入口網站，如果您認為可能已受到危害。
> 
> 

tooconfigure 您的連接字串、 開啟 hello`app.config`從 Visual Studio 中的 [方案總管] 的檔案。 新增的 hello hello 內容`<appSettings>`如下所示的項目。 取代`account-name`hello 儲存體帳戶名稱和`account-key`與您的帳戶存取金鑰：

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key" />
    </appSettings>
</configuration>
```

例如，組態設定會如下顯示：

```xml
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=GMuzNHjlB3S9itqZJHHCnRkrokLkcSyW7yK9BRbGp0ENePunLPwBgpxV1Z/pVo9zpem/2xSHXkMqTHHLcx8XRA==" />
```

tootarget hello 儲存體模擬器，您可以使用對應 toohello 已知帳戶名稱和金鑰的捷徑。 在此情況下，您的連接字串設定會是︰

```xml
<add key="StorageConnectionString" value="UseDevelopmentStorage=true;" />
```

