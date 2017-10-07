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
# <a name="how-toouse-blob-storage-from-xamarin"></a>如何 toouse Xamarin 從 Blob 儲存體
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a>概觀
Xamarin 可讓開發人員 toouse 共用 C# 程式碼基底 toocreate iOS、 Android 和 Windows 市集應用程式使用其原生使用者介面。 本教學課程示範如何 toouse 與 Xamarin 應用程式的 Azure Blob 儲存體。 如果您想要深入了解 Azure 儲存體，toolearn 在探究 hello 程式碼之前，請參閱[簡介 tooMicrosoft Azure 儲存體](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)。

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a>建立新的 Xamarin 應用程式
針對此教學課程，我們將建立以 Android、iOS 和 Windows 為目標的應用程式。 此應用程式只會建立容器，並將 blob 上傳到此容器。 我們將使用 Visual Studio 在 Windows 中，但 hello 建立 macOS 上使用 Xamarin Studio 的應用程式時，就可以套用相同 datacenter 的知識。

請遵循這些步驟 toocreate 您的應用程式：

1. 下載並安裝 [Xamarin for Visual Studio](https://www.xamarin.com/download)(若您尚未這麼做)。
2. 開啟 Visual Studio，建立一個空的應用程式 (原生可攜式)︰[檔案] > [新增] > [專案] > [跨平台] > [空的應用程式 (原生可攜式)]。
3. 以滑鼠右鍵按一下方案 hello 方案總管 窗格中的，選取**管理方案的 NuGet 套件**。 搜尋**WindowsAzure.Storage**並安裝最新穩定版本 tooall 專案 hello 方案中。
4. 建置並執行專案。

您現在應該有 tooclick 遞增計數器的按鈕可讓您的應用程式。

## <a name="create-container-and-upload-blob"></a>建立容器並上傳 blob
接下來，在您`(Portable)`專案中，您會加入一些程式碼太`MyClass.cs`。 此程式碼會建立一個容器，並上傳 Blob 到此容器中。 `MyClass.cs`看起來應該像 hello 下列：

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

請確定 tooreplace"your_account_name_here"和"your_account_key_here 」 與您實際的帳戶名稱和帳戶金鑰。 

所有專案都的參考 tooyour 可攜式專案-這表示您可以將所有共用的程式碼撰寫的其中一個您 iOS、 Android 和 Windows Phone 放置，並使用它在所有您的專案。 您現在可以新增下列一行程式碼 tooeach 專案 toostart 如何利用 hello:`MyClass.performBlobOperation()`

### <a name="xamarinappdroid--mainactivitycs"></a>XamarinApp.Droid > MainActivity.cs

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

### <a name="xamarinappios--viewcontrollercs"></a>XamarinApp.iOS > ViewController.cs

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

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a>XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs

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

## <a name="run-hello-application"></a>執行 hello 應用程式
您現在可以在 Android 或 Windows Phone 模擬器中執行這個應用程式。 您也可以在 iOS 模擬器中執行此應用程式，但這需要 Mac 作業系統。 如需有關如何 toodo，請閱讀 hello 文件的特定指示[連接 Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)

一旦您執行您的應用程式時，它會建立 hello 容器`mycontainer`儲存體帳戶中。 它應該包含 hello blob `myblob`，其具有 hello 文字`Hello, world!`。 您可以驗證，請使用 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com/)。

## <a name="next-steps"></a>後續步驟
在本教學課程中，您學到如何 toocreate 在 Xamarin 的跨平台應用程式使用 Azure 儲存體，特別將焦點放在 Blob 儲存體中的其中一個案例。 不過，除了 Blob 儲存體以外，您還可以處理更多，例如資料表、檔案和佇列儲存體。 請查看下列多個發行項 toolearn hello:

* [以 .NET 開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md)
* [以 .NET 開始使用 Azure 表格儲存體](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [以 .NET 開始使用 Azure 佇列儲存體](../queues/storage-dotnet-how-to-use-queues.md)
* [在 Windows 上開始使用 Azure 檔案儲存體](../files/storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

