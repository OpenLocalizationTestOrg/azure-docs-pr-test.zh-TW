.NET 應用程式可以使用 hello **StackExchange.Redis**快取用戶端，可以使用 NuGet 封裝，它可簡化 hello 設定快取的用戶端應用程式的 Visual Studio 中設定。 

> [!NOTE]
> 如需詳細資訊，請參閱 hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github 頁面和 hello [StackExchange.Redis 快取的用戶端文件](http://github.com/StackExchange/StackExchange.Redis#documentation)。
> 
> 

tooconfigure 用戶端應用程式，在 Visual Studio 中使用 hello StackExchange.Redis NuGet 封裝，以滑鼠右鍵按一下中的 hello 專案**方案總管 中**選擇**管理 NuGet 封裝**。 

![Manage NuGet packages](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

型別**StackExchange.Redis**或**StackExchange.Redis.StrongName** hello 搜尋文字方塊中，從 hello 結果中，選取 hello 所需的版本，然後按一下**安裝**。

> [!NOTE]
> 如果您偏好 toouse hello 的強式名稱版本**StackExchange.Redis**用戶端程式庫中，選擇**StackExchange.Redis.StrongName**; 否則選擇**StackExchange.Redis**.
> 
> 

![StackExchange.Redis NuGet package](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

hello NuGet 封裝下載並新增 hello hello StackExchange.Redis 快取用戶端與您用戶端應用程式 tooaccess Azure Redis 快取所需的組件參考。

> [!NOTE]
> 如果您先前已設定您的專案 toouse StackExchange.Redis，您可以檢查更新 toohello 封裝從 hello **NuGet 套件管理員**。 如 toocheck 和安裝更新版本的 hello StackExchange.Redis NuGet 封裝，按一下**更新**在 hello hello **NuGet 套件管理員**視窗。 如果更新 toohello StackExchange.Redis NuGet 封裝功能，您可以更新您的專案 toouse hello 更新版本。
> 
> 

您也可以按一下 安裝 hello StackExchange.Redis NuGet 封裝**NuGet 套件管理員**， **Package Manager Console**從 hello**工具**功能表，然後執行 hello下列命令從 hello **Package Manager Console**視窗。
    
```
Install-Package StackExchange.Redis
```
