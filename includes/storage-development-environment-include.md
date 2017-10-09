## <a name="set-up-your-development-environment"></a><span data-ttu-id="93a34-101">設定開發環境</span><span class="sxs-lookup"><span data-stu-id="93a34-101">Set up your development environment</span></span>
<span data-ttu-id="93a34-102">接下來，設定 Visual Studio 中開發環境，因此您已經準備好 tootry hello 本指南中的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="93a34-102">Next, set up your development environment in Visual Studio so you're ready tootry hello code examples in this guide.</span></span>

### <a name="create-a-windows-console-application-project"></a><span data-ttu-id="93a34-103">建立 Windows 主控台應用程式專案</span><span class="sxs-lookup"><span data-stu-id="93a34-103">Create a Windows console application project</span></span>
<span data-ttu-id="93a34-104">在 Visual Studio 中，建立新的 Windows 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="93a34-104">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="93a34-105">下列步驟的 hello 顯示 toocreate 2017，不過，hello 步驟的 Visual Studio 中的主控台應用程式的方式類似在其他版本的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="93a34-105">hello following steps show you how toocreate a console application in Visual Studio 2017, however, hello steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="93a34-106">選取 [檔案] > [新增] > [專案]</span><span class="sxs-lookup"><span data-stu-id="93a34-106">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="93a34-107">選取 [安裝] > [範本] > [Visual C#] > [Windows 傳統桌面]</span><span class="sxs-lookup"><span data-stu-id="93a34-107">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="93a34-108">選取 **主控台應用程式 (.NET Framework)**</span><span class="sxs-lookup"><span data-stu-id="93a34-108">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="93a34-109">輸入您的應用程式的名稱在 hello**名稱：**欄位</span><span class="sxs-lookup"><span data-stu-id="93a34-109">Enter a name for your application in hello **Name:** field</span></span>
5. <span data-ttu-id="93a34-110">選取 [確定]</span><span class="sxs-lookup"><span data-stu-id="93a34-110">Select **OK**</span></span>

![Visual Studio 中的專案建立對話方塊](./media/storage-development-environment-include/storage-development-environment-include-1.png)

<span data-ttu-id="93a34-112">本教學課程中的所有程式碼範例可加入 toohello`Main()`的主控台應用程式的方法`Program.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="93a34-112">All code examples in this tutorial can be added toohello `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="93a34-113">您可以在任何類型的.NET 應用程式，包括 Azure 雲端服務或 web 應用程式和桌上型電腦與行動應用程式中使用 hello Azure 儲存體用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="93a34-113">You can use hello Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="93a34-114">在本指南中，為求簡化，我們會使用主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="93a34-114">In this guide, we use a console application for simplicity.</span></span>

### <a name="use-nuget-tooinstall-hello-required-packages"></a><span data-ttu-id="93a34-115">使用 NuGet tooinstall hello 必要封裝</span><span class="sxs-lookup"><span data-stu-id="93a34-115">Use NuGet tooinstall hello required packages</span></span>
<span data-ttu-id="93a34-116">有兩個封裝，您需要 tooreference 專案 toocomplete 在本教學課程：</span><span class="sxs-lookup"><span data-stu-id="93a34-116">There are two packages you need tooreference in your project toocomplete this tutorial:</span></span>

* <span data-ttu-id="93a34-117">[Microsoft Azure 儲存體用戶端程式庫適用於.NET](https://www.nuget.org/packages/WindowsAzure.Storage/)： 此封裝提供以程式設計方式存取 toodata 儲存體帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="93a34-117">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access toodata resources in your storage account.</span></span>
* <span data-ttu-id="93a34-118">[適用於 .NET 的 Microsoft Azure Configuration Manager 程式庫](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)︰此套件提供一個類別，無論您的應用程式於何處執行，均可用來剖析組態檔中的連接字串。</span><span class="sxs-lookup"><span data-stu-id="93a34-118">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="93a34-119">您可以使用 NuGet tooobtain 這兩個封裝。</span><span class="sxs-lookup"><span data-stu-id="93a34-119">You can use NuGet tooobtain both packages.</span></span> <span data-ttu-id="93a34-120">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="93a34-120">Follow these steps:</span></span>

1. <span data-ttu-id="93a34-121">在 [方案總管] 中以滑鼠右鍵按一下專案，然後選擇 [管理 NuGet 封裝]。</span><span class="sxs-lookup"><span data-stu-id="93a34-121">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="93a34-122">線上搜尋"WindowsAzure.Storage"，然後按一下**安裝**tooinstall hello 儲存體用戶端程式庫和其相依性。</span><span class="sxs-lookup"><span data-stu-id="93a34-122">Search online for "WindowsAzure.Storage" and click **Install** tooinstall hello Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="93a34-123">線上搜尋"WindowsAzure.ConfigurationManager 」，然後按一下**安裝**tooinstall hello Azure 組態管理員。</span><span class="sxs-lookup"><span data-stu-id="93a34-123">Search online for "WindowsAzure.ConfigurationManager" and click **Install** tooinstall hello Azure Configuration Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="93a34-124">hello 儲存體用戶端程式庫封裝也會包含在 hello [Azure SDK for.NET](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="93a34-124">hello Storage Client Library package is also included in hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="93a34-125">不過，我們建議您也從永遠有 hello hello 用戶端程式庫的最新版本的 NuGet tooensure 安裝 hello 儲存體用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="93a34-125">However, we recommend that you also install hello Storage Client Library from NuGet tooensure that you always have hello latest version of hello client library.</span></span>
> 
> <span data-ttu-id="93a34-126">在不是從 WCF 資料服務的 NuGet 上可用的 hello ODataLib 封裝來解析 hello hello 適用於.NET 的儲存體用戶端程式庫中的 ODataLib 相依性。</span><span class="sxs-lookup"><span data-stu-id="93a34-126">hello ODataLib dependencies in hello Storage Client Library for .NET are resolved by hello ODataLib packages available on NuGet, not from WCF Data Services.</span></span> <span data-ttu-id="93a34-127">hello ODataLib 程式庫可以下載直接或透過 NuGet 您程式碼專案所參考。</span><span class="sxs-lookup"><span data-stu-id="93a34-127">hello ODataLib libraries can be downloaded directly or referenced by your code project through NuGet.</span></span> <span data-ttu-id="93a34-128">hello hello 儲存體用戶端程式庫所使用特定 ODataLib 封裝包括[OData](http://nuget.org/packages/Microsoft.Data.OData/)， [Edm](http://nuget.org/packages/Microsoft.Data.Edm/)，和[空間](http://nuget.org/packages/System.Spatial/)。</span><span class="sxs-lookup"><span data-stu-id="93a34-128">hello specific ODataLib packages used by hello Storage Client Library are [OData](http://nuget.org/packages/Microsoft.Data.OData/), [Edm](http://nuget.org/packages/Microsoft.Data.Edm/), and [Spatial](http://nuget.org/packages/System.Spatial/).</span></span> <span data-ttu-id="93a34-129">雖然這些程式庫類別所使用的 hello Azure 資料表儲存體，它們是必要的相依性以 hello 儲存體用戶端程式庫的程式設計。</span><span class="sxs-lookup"><span data-stu-id="93a34-129">While these libraries are used by hello Azure Table storage classes, they are required dependencies for programming with hello Storage Client Library.</span></span>
> 
> 

### <a name="determine-your-target-environment"></a><span data-ttu-id="93a34-130">決定您的目標環境</span><span class="sxs-lookup"><span data-stu-id="93a34-130">Determine your target environment</span></span>
<span data-ttu-id="93a34-131">您有兩個環境選項執行本指南中的 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="93a34-131">You have two environment options for running hello examples in this guide:</span></span>

* <span data-ttu-id="93a34-132">您可以針對 Azure 儲存體帳戶 hello 雲端中執行您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="93a34-132">You can run your code against an Azure Storage account in hello cloud.</span></span> 
* <span data-ttu-id="93a34-133">您可以對 hello Azure 儲存體模擬器中執行您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="93a34-133">You can run your code against hello Azure storage emulator.</span></span> <span data-ttu-id="93a34-134">hello 儲存體模擬器是模擬 hello 雲端中的 Azure 儲存體帳戶的本機環境。</span><span class="sxs-lookup"><span data-stu-id="93a34-134">hello storage emulator is a local environment that emulates an Azure Storage account in hello cloud.</span></span> <span data-ttu-id="93a34-135">hello 模擬器是進行測試和偵錯您的程式碼，在開發您的應用程式時可用的選項。</span><span class="sxs-lookup"><span data-stu-id="93a34-135">hello emulator is a free option for testing and debugging your code while your application is under development.</span></span> <span data-ttu-id="93a34-136">hello 模擬器會使用已知的帳戶和金鑰。</span><span class="sxs-lookup"><span data-stu-id="93a34-136">hello emulator uses a well-known account and key.</span></span> <span data-ttu-id="93a34-137">如需詳細資訊，請參閱[使用 hello Azure 儲存體模擬器進行開發和測試](../articles/storage/common/storage-use-emulator.md)</span><span class="sxs-lookup"><span data-stu-id="93a34-137">For more information, see [Use hello Azure Storage Emulator for Development and Testing](../articles/storage/common/storage-use-emulator.md)</span></span>

<span data-ttu-id="93a34-138">如果您的目標儲存體帳戶 hello 雲端中的，複製 hello Azure 入口網站儲存體帳戶的 hello 主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="93a34-138">If you are targeting a storage account in hello cloud, copy hello primary access key for your storage account from hello Azure portal.</span></span> <span data-ttu-id="93a34-139">如需詳細資訊，請參閱 [檢視和複製儲存體存取金鑰](../articles/storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys)。</span><span class="sxs-lookup"><span data-stu-id="93a34-139">For more information, see [View and copy storage access keys](../articles/storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

> [!NOTE]
> <span data-ttu-id="93a34-140">您可以針對 hello 儲存體模擬器 tooavoid 支出任何 Azure 儲存體相關聯的成本。</span><span class="sxs-lookup"><span data-stu-id="93a34-140">You can target hello storage emulator tooavoid incurring any costs associated with Azure Storage.</span></span> <span data-ttu-id="93a34-141">不過，如果您選擇 tootarget Azure 儲存體帳戶 hello 雲端中，執行本教學課程的成本將會造成影響。</span><span class="sxs-lookup"><span data-stu-id="93a34-141">However, if you do choose tootarget an Azure storage account in hello cloud, costs for performing this tutorial will be negligible.</span></span>
> 
> 

### <a name="configure-your-storage-connection-string"></a><span data-ttu-id="93a34-142">設定儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="93a34-142">Configure your storage connection string</span></span>
<span data-ttu-id="93a34-143">hello 適用於.NET 的 Azure 儲存體用戶端程式庫支援使用儲存體連接字串 tooconfigure 端點和認證來存取儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="93a34-143">hello Azure Storage Client Library for .NET supports using a storage connection string tooconfigure endpoints and credentials for accessing storage services.</span></span> <span data-ttu-id="93a34-144">最佳的方式 toomaintain hello 您儲存體連接字串是在組態檔中。</span><span class="sxs-lookup"><span data-stu-id="93a34-144">hello best way toomaintain your storage connection string is in a configuration file.</span></span> 

<span data-ttu-id="93a34-145">如需連接字串的詳細資訊，請參閱[設定儲存體的連接字串 tooAzure](../articles/storage/common/storage-configure-connection-string.md)。</span><span class="sxs-lookup"><span data-stu-id="93a34-145">For more information about connection strings, see [Configure a Connection String tooAzure Storage](../articles/storage/common/storage-configure-connection-string.md).</span></span>

> [!NOTE]
> <span data-ttu-id="93a34-146">儲存體帳戶金鑰是儲存體帳戶的類似 toohello 根密碼。</span><span class="sxs-lookup"><span data-stu-id="93a34-146">Your storage account key is similar toohello root password for your storage account.</span></span> <span data-ttu-id="93a34-147">永遠是小心 tooprotect 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="93a34-147">Always be careful tooprotect your storage account key.</span></span> <span data-ttu-id="93a34-148">避免將其散發 tooother 使用者，硬式編碼，或將它儲存為可存取 tooothers 純文字檔案中。</span><span class="sxs-lookup"><span data-stu-id="93a34-148">Avoid distributing it tooother users, hard-coding it, or saving it in a plain-text file that is accessible tooothers.</span></span> <span data-ttu-id="93a34-149">重新產生金鑰使用 hello Azure 入口網站，如果您認為可能已受到危害。</span><span class="sxs-lookup"><span data-stu-id="93a34-149">Regenerate your key using hello Azure portal if you believe it may have been compromised.</span></span>
> 
> 

<span data-ttu-id="93a34-150">tooconfigure 您的連接字串、 開啟 hello`app.config`從 Visual Studio 中的 [方案總管] 的檔案。</span><span class="sxs-lookup"><span data-stu-id="93a34-150">tooconfigure your connection string, open hello `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="93a34-151">新增的 hello hello 內容`<appSettings>`如下所示的項目。</span><span class="sxs-lookup"><span data-stu-id="93a34-151">Add hello contents of hello `<appSettings>` element shown below.</span></span> <span data-ttu-id="93a34-152">取代`account-name`hello 儲存體帳戶名稱和`account-key`與您的帳戶存取金鑰：</span><span class="sxs-lookup"><span data-stu-id="93a34-152">Replace `account-name` with hello name of your storage account, and `account-key` with your account access key:</span></span>

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

<span data-ttu-id="93a34-153">例如，組態設定會如下顯示：</span><span class="sxs-lookup"><span data-stu-id="93a34-153">For example, your configuration setting appears similar to:</span></span>

```xml
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=GMuzNHjlB3S9itqZJHHCnRkrokLkcSyW7yK9BRbGp0ENePunLPwBgpxV1Z/pVo9zpem/2xSHXkMqTHHLcx8XRA==" />
```

tootarget hello 儲存體模擬器，您可以使用對應 toohello 已知帳戶名稱和金鑰的捷徑。 <span data-ttu-id="93a34-155">在此情況下，您的連接字串設定會是︰</span><span class="sxs-lookup"><span data-stu-id="93a34-155">In that case, your connection string setting is:</span></span>

```xml
<add key="StorageConnectionString" value="UseDevelopmentStorage=true;" />
```

