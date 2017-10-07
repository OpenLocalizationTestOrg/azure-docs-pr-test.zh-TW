---
title: "aaaHow toouse Xamarin 從 Blob 儲存體 |Microsoft 文件"
description: "hello Xamarin 的 Azure 儲存體用戶端程式庫可讓開發人員 toocreate iOS、 Android 和 Windows 市集應用程式使用其原生使用者介面。 本教學課程示範如何 toouse Xamarin toocreate 使用 Azure Blob 儲存體的應用程式。"
services: storage
documentationcenter: xamarin
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 44cb845d-cf78-4942-95b8-952da4f9a2c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 688484fc560b5c89ed1692f5cbf5713aa8fc90a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-xamarin"></a><span data-ttu-id="7e5eb-104">如何 toouse Xamarin 從 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="7e5eb-104">How toouse Blob Storage from Xamarin</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a><span data-ttu-id="7e5eb-105">概觀</span><span class="sxs-lookup"><span data-stu-id="7e5eb-105">Overview</span></span>
<span data-ttu-id="7e5eb-106">Xamarin 可讓開發人員 toouse 共用 C# 程式碼基底 toocreate iOS、 Android 和 Windows 市集應用程式使用其原生使用者介面。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-106">Xamarin enables developers toouse a shared C# codebase toocreate iOS, Android, and Windows Store apps with their native user interfaces.</span></span> <span data-ttu-id="7e5eb-107">本教學課程示範如何 toouse 與 Xamarin 應用程式的 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-107">This tutorial shows you how toouse Azure Blob storage with a Xamarin application.</span></span> <span data-ttu-id="7e5eb-108">如果您想要深入了解 Azure 儲存體，toolearn 在探究 hello 程式碼之前，請參閱[簡介 tooMicrosoft Azure 儲存體](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-108">If you'd like toolearn more about Azure Storage, before diving into hello code, see [Introduction tooMicrosoft Azure Storage](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a><span data-ttu-id="7e5eb-109">建立新的 Xamarin 應用程式</span><span class="sxs-lookup"><span data-stu-id="7e5eb-109">Create a new Xamarin Application</span></span>
<span data-ttu-id="7e5eb-110">針對此教學課程，我們將建立以 Android、iOS 和 Windows 為目標的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-110">For this tutorial, we'll be creating an app that targets Android, iOS, and Windows.</span></span> <span data-ttu-id="7e5eb-111">此應用程式只會建立容器，並將 blob 上傳到此容器。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-111">This app will simply create a container and upload a blob into this container.</span></span> <span data-ttu-id="7e5eb-112">我們將使用 Visual Studio 在 Windows 中，但 hello 建立 macOS 上使用 Xamarin Studio 的應用程式時，就可以套用相同 datacenter 的知識。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-112">We'll be using Visual Studio on Windows, but hello same learnings can be applied when creating an app using Xamarin Studio on macOS.</span></span>

<span data-ttu-id="7e5eb-113">請遵循這些步驟 toocreate 您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="7e5eb-113">Follow these steps toocreate your application:</span></span>

1. <span data-ttu-id="7e5eb-114">下載並安裝 [Xamarin for Visual Studio](https://www.xamarin.com/download)(若您尚未這麼做)。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-114">If you haven't already, download and install [Xamarin for Visual Studio](https://www.xamarin.com/download).</span></span>
2. <span data-ttu-id="7e5eb-115">開啟 Visual Studio，建立一個空的應用程式 (原生可攜式)︰[檔案] > [新增] > [專案] > [跨平台] > [空的應用程式 (原生可攜式)]。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-115">Open Visual Studio, and create a Blank App (Native Portable): **File > New > Project > Cross-Platform > Blank App(Native Portable)**.</span></span>
3. <span data-ttu-id="7e5eb-116">以滑鼠右鍵按一下方案 hello 方案總管 窗格中的，選取**管理方案的 NuGet 套件**。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-116">Right-click your solution in hello Solution Explorer pane and select **Manage NuGet Packages for Solution**.</span></span> <span data-ttu-id="7e5eb-117">搜尋**WindowsAzure.Storage**並安裝最新穩定版本 tooall 專案 hello 方案中。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-117">Search for **WindowsAzure.Storage** and install hello latest stable version tooall projects in your solution.</span></span>
4. <span data-ttu-id="7e5eb-118">建置並執行專案。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-118">Build and run your project.</span></span>

<span data-ttu-id="7e5eb-119">您現在應該有 tooclick 遞增計數器的按鈕可讓您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-119">You should now have an application that allows you tooclick a button which increments a counter.</span></span>

## <a name="create-container-and-upload-blob"></a><span data-ttu-id="7e5eb-120">建立容器並上傳 blob</span><span class="sxs-lookup"><span data-stu-id="7e5eb-120">Create container and upload blob</span></span>
<span data-ttu-id="7e5eb-121">接下來，在您`(Portable)`專案中，您會加入一些程式碼太`MyClass.cs`。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-121">Next, under your `(Portable)` project, you'll add some code too`MyClass.cs`.</span></span> <span data-ttu-id="7e5eb-122">此程式碼會建立一個容器，並上傳 Blob 到此容器中。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-122">This code creates a container and uploads a blob into this container.</span></span> <span data-ttu-id="7e5eb-123">`MyClass.cs`看起來應該像 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="7e5eb-123">`MyClass.cs` should look like hello following:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Threading.Tasks;

namespace XamarinApp
{
    public class MyClass
    {
        public MyClass ()
        {
        }

        public static async Task performBlobOperation()
        {
            // Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here");

            // Create hello blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference tooa previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create hello container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference tooa blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create hello "myblob" blob with hello text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

<span data-ttu-id="7e5eb-124">請確定 tooreplace"your_account_name_here"和"your_account_key_here 」 與您實際的帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-124">Make sure tooreplace "your_account_name_here" and "your_account_key_here" with your actual account name and account key.</span></span> 

<span data-ttu-id="7e5eb-125">所有專案都的參考 tooyour 可攜式專案-這表示您可以將所有共用的程式碼撰寫的其中一個您 iOS、 Android 和 Windows Phone 放置，並使用它在所有您的專案。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-125">Your iOS, Android, and Windows Phone projects all have references tooyour Portable project - meaning you can write all of your shared code in one place and use it across all of your projects.</span></span> <span data-ttu-id="7e5eb-126">您現在可以新增下列一行程式碼 tooeach 專案 toostart 如何利用 hello:`MyClass.performBlobOperation()`</span><span class="sxs-lookup"><span data-stu-id="7e5eb-126">You can now add hello following line of code tooeach project toostart taking advantage: `MyClass.performBlobOperation()`</span></span>

### <a name="xamarinappdroid--mainactivitycs"></a><span data-ttu-id="7e5eb-127">XamarinApp.Droid > MainActivity.cs</span><span class="sxs-lookup"><span data-stu-id="7e5eb-127">XamarinApp.Droid > MainActivity.cs</span></span>

```csharp
using Android.App;
using Android.Widget;
using Android.OS;

namespace XamarinApp.Droid
{
    [Activity (Label = "XamarinApp.Droid", MainLauncher = true, Icon = "@drawable/icon")]
    public class MainActivity : Activity
    {
        int count = 1;

        protected override async void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);

            button.Click += delegate {
                button.Text = string.Format ("{0} clicks!", count++);
            };

            await MyClass.performBlobOperation();
            }
        }
    }
}
```

### <a name="xamarinappios--viewcontrollercs"></a><span data-ttu-id="7e5eb-128">XamarinApp.iOS > ViewController.cs</span><span class="sxs-lookup"><span data-stu-id="7e5eb-128">XamarinApp.iOS > ViewController.cs</span></span>

```csharp
using System;
using UIKit;

namespace XamarinApp.iOS
{
    public partial class ViewController : UIViewController
    {
        int count = 1;

        public ViewController (IntPtr handle) : base (handle)
        {
        }

        public override async void ViewDidLoad ()
        {
            int count = 1;

            public ViewController (IntPtr handle) : base (handle)
            {
            }

            public override async void ViewDidLoad ()
            {
                base.ViewDidLoad ();
                // Perform any additional setup after loading hello view, typically from a nib.
                Button.AccessibilityIdentifier = "myButton";
                Button.TouchUpInside += delegate {
                    var title = string.Format ("{0} clicks!", count++);
                    Button.SetTitle (title, UIControlState.Normal);
                };

                await MyClass.performBlobOperation();
            }

            public override void DidReceiveMemoryWarning ()
            {
                base.DidReceiveMemoryWarning ();
                // Release any cached data, images, etc that aren't in use.
            }
        }
    }
}
```

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a><span data-ttu-id="7e5eb-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="7e5eb-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span></span>

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// hello Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated toowithin a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        int count = 1;

        public MainPage()
        {
            this.InitializeComponent();

            this.NavigationCacheMode = NavigationCacheMode.Required;
        }

        /// <summary>
        /// Invoked when this page is about toobe displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used tooconfigure hello page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about toobe displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used tooconfigure hello page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling hello hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using hello NavigationHelper provided by some templates,
                // this event is handled for you.
                Button.Click += delegate {
                    var title = string.Format("{0} clicks!", count++);
                    Button.Content = title;
                };

                await MyClass.performBlobOperation();
            }
        }
    }
}
```

## <a name="run-hello-application"></a><span data-ttu-id="7e5eb-130">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="7e5eb-130">Run hello application</span></span>
<span data-ttu-id="7e5eb-131">您現在可以在 Android 或 Windows Phone 模擬器中執行這個應用程式。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-131">You can now run this application in an Android or Windows Phone emulator.</span></span> <span data-ttu-id="7e5eb-132">您也可以在 iOS 模擬器中執行此應用程式，但這需要 Mac 作業系統。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-132">You can also run this application in an iOS emulator, but this will require a Mac.</span></span> <span data-ttu-id="7e5eb-133">如需有關如何 toodo，請閱讀 hello 文件的特定指示[連接 Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span><span class="sxs-lookup"><span data-stu-id="7e5eb-133">For specific instructions on how toodo this, please read hello documentation for [connecting Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span></span>

<span data-ttu-id="7e5eb-134">一旦您執行您的應用程式時，它會建立 hello 容器`mycontainer`儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-134">Once you run your app, it will create hello container `mycontainer` in your Storage account.</span></span> <span data-ttu-id="7e5eb-135">它應該包含 hello blob `myblob`，其具有 hello 文字`Hello, world!`。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-135">It should contain hello blob, `myblob`, which has hello text, `Hello, world!`.</span></span> <span data-ttu-id="7e5eb-136">您可以驗證，請使用 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-136">You can verify this by using hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e5eb-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7e5eb-137">Next steps</span></span>
<span data-ttu-id="7e5eb-138">在本教學課程中，您學到如何 toocreate 在 Xamarin 的跨平台應用程式使用 Azure 儲存體，特別將焦點放在 Blob 儲存體中的其中一個案例。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-138">In this tutorial, you learned how toocreate a cross-platform application in Xamarin that uses Azure Storage, specifically focusing on one scenario in Blob Storage.</span></span> <span data-ttu-id="7e5eb-139">不過，除了 Blob 儲存體以外，您還可以處理更多，例如資料表、檔案和佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="7e5eb-139">However, you can do a lot more with not only Blob Storage, but also with Table, File, and Queue Storage.</span></span> <span data-ttu-id="7e5eb-140">請查看下列多個發行項 toolearn hello:</span><span class="sxs-lookup"><span data-stu-id="7e5eb-140">Please check out hello following articles toolearn more:</span></span>

* [<span data-ttu-id="7e5eb-141">以 .NET 開始使用 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="7e5eb-141">Get started with Azure Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="7e5eb-142">以 .NET 開始使用 Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="7e5eb-142">Get started with Azure Table storage using .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="7e5eb-143">以 .NET 開始使用 Azure 佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="7e5eb-143">Get started with Azure Queue storage using .NET</span></span>](../queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="7e5eb-144">在 Windows 上開始使用 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="7e5eb-144">Get started with Azure File storage on Windows</span></span>](../files/storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

