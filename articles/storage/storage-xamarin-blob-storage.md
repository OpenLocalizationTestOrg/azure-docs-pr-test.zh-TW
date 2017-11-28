---
title: "如何使用 Xamarin 的 Blob 儲存體 | Microsoft Docs"
description: "適用於 Xamarin 的 Azure 儲存體用戶端程式庫可讓開發人員使用其原生的使用者介面以建立 iOS、Android 和 Windows 市集應用程式。 本教學課程示範如何使用 Xamarin 來建立使用 Azure Blob 儲存體的應用程式。"
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
ms.openlocfilehash: 0952c0e7189dd360098744a7e19b04cd330cb617
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-blob-storage-from-xamarin"></a><span data-ttu-id="28e19-104">如何使用 Xamarin 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="28e19-104">How to use Blob Storage from Xamarin</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a><span data-ttu-id="28e19-105">Overview</span><span class="sxs-lookup"><span data-stu-id="28e19-105">Overview</span></span>
<span data-ttu-id="28e19-106">Xamarin 可讓開發人員使用共用的 C# 程式碼基底，使用其原生的使用者介面以建立 iOS、Android 和 Windows 市集應用程式。</span><span class="sxs-lookup"><span data-stu-id="28e19-106">Xamarin enables developers to use a shared C# codebase to create iOS, Android, and Windows Store apps with their native user interfaces.</span></span> <span data-ttu-id="28e19-107">本教學課程會示範如何搭配 Xamarin 應用程式使用 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="28e19-107">This tutorial shows you how to use Azure Blob storage with a Xamarin application.</span></span> <span data-ttu-id="28e19-108">如果您想要深入了解 Azure 儲存體，在一頭栽進程式碼之前，請先參閱 [Microsoft Azure 儲存體簡介](storage-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="28e19-108">If you'd like to learn more about Azure Storage, before diving into the code, see [Introduction to Microsoft Azure Storage](storage-introduction.md).</span></span>

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a><span data-ttu-id="28e19-109">建立新的 Xamarin 應用程式</span><span class="sxs-lookup"><span data-stu-id="28e19-109">Create a new Xamarin Application</span></span>
<span data-ttu-id="28e19-110">針對此教學課程，我們將建立以 Android、iOS 和 Windows 為目標的應用程式。</span><span class="sxs-lookup"><span data-stu-id="28e19-110">For this tutorial, we'll be creating an app that targets Android, iOS, and Windows.</span></span> <span data-ttu-id="28e19-111">此應用程式只會建立容器，並將 blob 上傳到此容器。</span><span class="sxs-lookup"><span data-stu-id="28e19-111">This app will simply create a container and upload a blob into this container.</span></span> <span data-ttu-id="28e19-112">我們將在 Windows 上使用 Visual Studio，但是在 macOS 上使用 Xamarin Studio 建立應用程式時，可以套用相同的做法。</span><span class="sxs-lookup"><span data-stu-id="28e19-112">We'll be using Visual Studio on Windows, but the same learnings can be applied when creating an app using Xamarin Studio on macOS.</span></span>

<span data-ttu-id="28e19-113">請遵循下列步驟來建立應用程式：</span><span class="sxs-lookup"><span data-stu-id="28e19-113">Follow these steps to create your application:</span></span>

1. <span data-ttu-id="28e19-114">下載並安裝 [Xamarin for Visual Studio](https://www.xamarin.com/download)(若您尚未這麼做)。</span><span class="sxs-lookup"><span data-stu-id="28e19-114">If you haven't already, download and install [Xamarin for Visual Studio](https://www.xamarin.com/download).</span></span>
2. <span data-ttu-id="28e19-115">開啟 Visual Studio，建立一個空的應用程式 (原生可攜式)︰[檔案] > [新增] > [專案] > [跨平台] > [空的應用程式 (原生可攜式)]。</span><span class="sxs-lookup"><span data-stu-id="28e19-115">Open Visual Studio, and create a Blank App (Native Portable): **File > New > Project > Cross-Platform > Blank App(Native Portable)**.</span></span>
3. <span data-ttu-id="28e19-116">以滑鼠右鍵按一下 [方案總管] 窗格中的方案，然後選取 [管理方案的 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="28e19-116">Right-click your solution in the Solution Explorer pane and select **Manage NuGet Packages for Solution**.</span></span> <span data-ttu-id="28e19-117">搜尋 **WindowsAzure.Storage**，將最新穩定版安裝到您方案中的所有專案。</span><span class="sxs-lookup"><span data-stu-id="28e19-117">Search for **WindowsAzure.Storage** and install the latest stable version to all projects in your solution.</span></span>
4. <span data-ttu-id="28e19-118">建置並執行專案。</span><span class="sxs-lookup"><span data-stu-id="28e19-118">Build and run your project.</span></span>

<span data-ttu-id="28e19-119">您現在應該有一個應用程式，在您按一下按鈕時就會遞增計數器。</span><span class="sxs-lookup"><span data-stu-id="28e19-119">You should now have an application that allows you to click a button which increments a counter.</span></span>

## <a name="create-container-and-upload-blob"></a><span data-ttu-id="28e19-120">建立容器並上傳 blob</span><span class="sxs-lookup"><span data-stu-id="28e19-120">Create container and upload blob</span></span>
<span data-ttu-id="28e19-121">接下來，在您的 `(Portable)` 專案之下，將一些程式碼加入 `MyClass.cs`。</span><span class="sxs-lookup"><span data-stu-id="28e19-121">Next, under your `(Portable)` project, you'll add some code to `MyClass.cs`.</span></span> <span data-ttu-id="28e19-122">此程式碼會建立一個容器，並上傳 Blob 到此容器中。</span><span class="sxs-lookup"><span data-stu-id="28e19-122">This code creates a container and uploads a blob into this container.</span></span> <span data-ttu-id="28e19-123">`MyClass.cs` 看起來應該如下所示︰</span><span class="sxs-lookup"><span data-stu-id="28e19-123">`MyClass.cs` should look like the following:</span></span>

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

            // Create the blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference to a previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create the container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference to a blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create the "myblob" blob with the text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

<span data-ttu-id="28e19-124">務必將 "your_account_name_here" 和 "your_account_key_here" 取代為您的實際帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="28e19-124">Make sure to replace "your_account_name_here" and "your_account_key_here" with your actual account name and account key.</span></span> 

<span data-ttu-id="28e19-125">您的 iOS、Android 和 Windows Phone 專案都會有可攜式專案的參考，這表示您可以在單一位置撰寫所有的共用程式碼，而且可以在所有專案中使用該程式碼。</span><span class="sxs-lookup"><span data-stu-id="28e19-125">Your iOS, Android, and Windows Phone projects all have references to your Portable project - meaning you can write all of your shared code in one place and use it across all of your projects.</span></span> <span data-ttu-id="28e19-126">您現在可以將下列程式碼行加入每個專案，以開始利用：`MyClass.performBlobOperation()`</span><span class="sxs-lookup"><span data-stu-id="28e19-126">You can now add the following line of code to each project to start taking advantage: `MyClass.performBlobOperation()`</span></span>

### <a name="xamarinappdroid--mainactivitycs"></a><span data-ttu-id="28e19-127">XamarinApp.Droid > MainActivity.cs</span><span class="sxs-lookup"><span data-stu-id="28e19-127">XamarinApp.Droid > MainActivity.cs</span></span>

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

            // Set our view from the "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from the layout resource,
            // and attach an event to it
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

### <a name="xamarinappios--viewcontrollercs"></a><span data-ttu-id="28e19-128">XamarinApp.iOS > ViewController.cs</span><span class="sxs-lookup"><span data-stu-id="28e19-128">XamarinApp.iOS > ViewController.cs</span></span>

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
                // Perform any additional setup after loading the view, typically from a nib.
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

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a><span data-ttu-id="28e19-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="28e19-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span></span>

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated to within a Frame.
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
        /// Invoked when this page is about to be displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used to configure the page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about to be displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used to configure the page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling the hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using the NavigationHelper provided by some templates,
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

## <a name="run-the-application"></a><span data-ttu-id="28e19-130">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="28e19-130">Run the application</span></span>
<span data-ttu-id="28e19-131">您現在可以在 Android 或 Windows Phone 模擬器中執行這個應用程式。</span><span class="sxs-lookup"><span data-stu-id="28e19-131">You can now run this application in an Android or Windows Phone emulator.</span></span> <span data-ttu-id="28e19-132">您也可以在 iOS 模擬器中執行此應用程式，但這需要 Mac 作業系統。</span><span class="sxs-lookup"><span data-stu-id="28e19-132">You can also run this application in an iOS emulator, but this will require a Mac.</span></span> <span data-ttu-id="28e19-133">如需具體的做法指示，請閱讀 [將 Visual Studio 連接到 Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span><span class="sxs-lookup"><span data-stu-id="28e19-133">For specific instructions on how to do this, please read the documentation for [connecting Visual Studio to a Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span></span>

<span data-ttu-id="28e19-134">一旦您執行應用程式，它會在您的儲存體帳戶中建立 `mycontainer` 容器。</span><span class="sxs-lookup"><span data-stu-id="28e19-134">Once you run your app, it will create the container `mycontainer` in your Storage account.</span></span> <span data-ttu-id="28e19-135">它應該包含 blob `myblob`，其具有文字 `Hello, world!`。</span><span class="sxs-lookup"><span data-stu-id="28e19-135">It should contain the blob, `myblob`, which has the text, `Hello, world!`.</span></span> <span data-ttu-id="28e19-136">您可以使用 [Microsoft Azure 儲存體總管](http://storageexplorer.com/)來驗證。</span><span class="sxs-lookup"><span data-stu-id="28e19-136">You can verify this by using the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="28e19-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="28e19-137">Next steps</span></span>
<span data-ttu-id="28e19-138">在本教學課程中，您已學會如何在使用 Azure 儲存體的 Xamarin 中建立跨平台的應用程式，尤其將焦點放在 Blob 儲存體中的一個案例中。</span><span class="sxs-lookup"><span data-stu-id="28e19-138">In this tutorial, you learned how to create a cross-platform application in Xamarin that uses Azure Storage, specifically focusing on one scenario in Blob Storage.</span></span> <span data-ttu-id="28e19-139">不過，除了 Blob 儲存體以外，您還可以處理更多，例如資料表、檔案和佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="28e19-139">However, you can do a lot more with not only Blob Storage, but also with Table, File, and Queue Storage.</span></span> <span data-ttu-id="28e19-140">若要深入了解，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="28e19-140">Please check out the following articles to learn more:</span></span>

* [<span data-ttu-id="28e19-141">以 .NET 開始使用 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="28e19-141">Get started with Azure Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="28e19-142">以 .NET 開始使用 Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="28e19-142">Get started with Azure Table storage using .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="28e19-143">以 .NET 開始使用 Azure 佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="28e19-143">Get started with Azure Queue storage using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="28e19-144">在 Windows 上開始使用 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="28e19-144">Get started with Azure File storage on Windows</span></span>](storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

