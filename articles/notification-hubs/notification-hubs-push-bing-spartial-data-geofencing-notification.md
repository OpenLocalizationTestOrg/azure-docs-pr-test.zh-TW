---
title: "Azure 通知中樞與 Bing 的空間資料的 aaaGeo 納入範圍的推播通知 |Microsoft 文件"
description: "在本教學課程中，您將學習如何以位置為基礎的 toodeliver 將推播通知 Azure 通知中樞與 Bing 的空間資料。"
services: notification-hubs
documentationcenter: windows
keywords: "推播通知,推播通知"
author: dend
manager: yuaxu
editor: dend
ms.assetid: f41beea1-0d62-4418-9ffc-c9d70607a1b7
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/31/2016
ms.author: dendeli
ms.openlocfilehash: d6efe473537f2159240c53e780741f12619c045d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a>使用 Azure 通知中樞和 Bing 空間資料為推播通知加上地理柵欄
> [!NOTE]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02)。
> 
> 

在本教學課程中，您將學習如何以位置為基礎的 toodeliver 將推播通知 Azure 通知中樞與 Bing 空間資料，從利用通用 Windows 平台應用程式中。

## <a name="prerequisites"></a>必要條件
首先和最重要，您需要確定您有所有 hello 軟體和服務先決條件 toomake:

* [Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) 或更新版本 ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) 也行)。 
* 最新版本的 hello [Azure SDK](https://azure.microsoft.com/downloads/)。 
* [Bing 地圖服務開發人員中心帳戶](https://www.bingmapsportal.com/) (您可以免費建立帳戶並將此帳戶關聯到您的 Microsoft 帳戶)。 

## <a name="getting-started"></a>開始使用
讓我們藉由建立 hello 專案開始。 在 Visual Studio 中，開始 [空白應用程式 (通用 Windows)] 類型的新專案。

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

Hello 專案建立完成之後，您應該有 hello 應用程式本身的 hello 控管。 現在讓我們設定 hello 異地隔離基礎結構的所有項目。 我們會持續 toouse Bing 的此服務，因為沒有公用的 REST API 端點，讓我們 tooquery 特定位置框架：

    http://spatial.virtualearth.net/REST/v1/data/

您將需要 toospecify hello 下列參數 tooget 運作：

* **資料來源識別碼**和**資料來源名稱** – 在 Bing 地圖服務 API 中，資料來源包含了各種分門別類的中繼資料，例如營業據點和營業時間。 您可以在此了解其相關資訊。 
* **實體名稱**– hello hello 通知想 toouse 作為參考點的實體。 
* **Bing 地圖服務 API 金鑰**– 這是當您建立 hello Bing 開發人員中心帳戶稍早取得的 hello 金鑰。

就來看看深入了解在 hello 設定每個以上的 hello 元件。

## <a name="setting-up-hello-data-source"></a>設定 hello 資料來源
您可以在 hello Bing 地圖服務開發人員中心中執行動作。 只要按一下**資料來源**hello 上方導覽列，然後選取在**管理資料來源**。

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

如果您已不使用 Bing Maps API 之前，很可能不會有任何資料來源存在，因此您只可以建立一個新上傳資料 tooa 資料來源上的。 請確定您填寫所有必要的 hello 欄位：

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

您可能會懷疑 – 何謂 hello 資料檔案和項目應該您要上傳嗎？ 基於 hello 這項測試，我們就可以使用管道為基礎的畫面格的區域 hello San Francisco waterfront hello 範例：

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

上述的 hello 代表此實體：

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

只複製並貼到新檔案的上述 hello 字串，然後將它儲存成**NotificationHubsGeofence.pipe**，並將它上傳 hello Bing 開發人員中心中。

> [!NOTE]
> 您可能會提示的 toospecify hello 的新索引鍵**主要金鑰**不同 hello**查詢索引鍵**。 只要建立新的金鑰透過 hello 儀表板和重新整理 hello 資料來源上傳頁面。
> 
> 

之後您上傳 hello 資料檔案，您必須確定您 hello 資料來源發行 toomake。 

跳過**管理資料來源**，如同我們上方、 hello 清單中尋找您的資料來源，按一下**發行**在 hello**動作**資料行。 在位元，您應該會看到您的資料來源中 hello**發行資料來源** 索引標籤：

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

如果您按一下**編輯**，您將可以一眼 toosee 我們見於哪些位置：

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

此時，hello 入口網站不會顯示 hello 界限，我們建立的 hello geofence – 我們只需要指定 hello 位置是在 hello 右邊區域的確認。

現在您有 hello 資料來源的所有 hello 需求。 tooget hello 詳細資料，對於 hello API 呼叫，在 hello Bing 地圖服務開發人員中心，hello 要求 URL 上的按一下**資料來源**選取**資料來源資訊**。

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

hello**查詢 URL**是我們在這裡之後。 這是依據我們可以執行查詢 toocheck 是否 hello 裝置目前的位置 hello 界限內的 hello 端點。 此核取，我們只需要的 tooexecute GET 呼叫 hello 查詢 URL，針對下列參數附加 hello tooperform:

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

如此一來，您會指定目標時間點，我們取得 hello 裝置的 Bing 地圖服務會自動執行 hello 計算 toosee，它是否 hello geofence 內。 一旦您執行瀏覽器 （或 cURL） hello 要求時，您會收到標準 JSON 回應：

![](./media/notification-hubs-geofence/bing-maps-json.png)

這個回應只會發生在 hello 點實際上 hello 指定界限內。 如果不在邊界內，您將會收到空白的 **results** 分類︰

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a>設定 hello UWP 應用程式
現在，我們已經準備好的 hello 資料來源時，我們可以開始處理 hello 我們稍早引導的 UWP 應用程式。

首先，我們必須啟用應用程式的位置服務。 toodo，連按兩下`Package.appxmanifest`檔案**方案總管 中**。

![](./media/notification-hubs-geofence/vs-package-manifest.png)

Hello 封裝屬性 索引標籤中所開啟，按一下**功能**，並確定您選取**位置**:

![](./media/notification-hubs-geofence/vs-package-location.png)

為已宣告 hello 位置功能，建立新的資料夾中名為方案`Core`，並加入新的檔案，稱為`LocationHelper.cs`:

![](./media/notification-hubs-geofence/vs-location-helper.png)

hello`LocationHelper`類別本身是相當基本此時 – 它是讓我們透過 hello 系統 API tooobtain hello 使用者位置：

    using System;
    using System.Threading.Tasks;
    using Windows.Devices.Geolocation;

    namespace NotificationHubs.Geofence.Core
    {
        public class LocationHelper
        {
            private static readonly uint AppDesiredAccuracyInMeters = 10;

            public async static Task<Geoposition> GetCurrentLocation()
            {
                var accessStatus = await Geolocator.RequestAccessAsync();
                switch (accessStatus)
                {
                    case GeolocationAccessStatus.Allowed:
                        {
                            Geolocator geolocator = new Geolocator { DesiredAccuracyInMeters = AppDesiredAccuracyInMeters };

                            return await geolocator.GetGeopositionAsync();
                        }
                    default:
                        {
                            return null;
                        }
                }
            }

        }
    }

您可以閱讀更多有關取得 hello hello 官方 UWP 應用程式中的使用者的位置[MSDN 文件](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx)。

toocheck hello 位置擷取實際運作，開啟您的主頁面的 hello 程式碼端 (`MainPage.xaml.cs`)。 建立新的事件處理常式，如 hello `Loaded` hello 中的事件`MainPage`建構函式：

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

hello 實作 hello 事件處理常式如下所示：

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

請注意我們宣告為非同步 hello 處理常式因為`GetCurrentLocation`是 awaitable，並因此需要 toobe 非同步內容中執行。 此外，因為在某些情況下我們最後可能會與 null 的位置 （例如 hello 位置服務停用或 hello 應用程式被拒絕的權限 tooaccess 位置），我們需要 toomake 確定它適當處理 null 檢查。

執行 hello 應用程式。 請確定您允許其存取位置︰

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

一次 hello 應用程式會啟動，您應該能夠 toosee hello 座標在 hello**輸出**視窗：

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

現在您已經瞭解的位置擷取 works – 覺得可用 tooremove hello 測試事件處理常式的載入因為我們將不會使用它不再。

hello 下一個步驟是 toocapture 位置變更。 為此，請回復 toohello`LocationHelper`類別，然後將 hello 事件處理常式`PositionChanged`:

    geolocator.PositionChanged += Geolocator_PositionChanged;

hello 實作將會顯示 hello 位置座標在 hello**輸出**視窗：

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a>Hello 後端設定
下載 hello [.NET 後端範例從 GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers)。 Hello 下載完成之後，請開啟 hello`NotifyUsers`資料夾，然後後續 – hello`NotifyUsers.sln`檔案。

設定 hello `AppBackend` hello 與專案**啟始專案**並啟動它。

![](./media/notification-hubs-geofence/vs-startup-project.png)

hello 專案已經設定的 toosend 推播通知 tootarget 裝置，因此我們必須 toodo 只有兩個項目 – 抽換 hello 正確的連接字串 hello 通知中樞，並將界限識別 toosend hello 通知時，才 hello使用者是 hello geofence 內。

tooconfigure hello 連接字串，在 hello`Models`資料夾開啟`Notifications.cs`。 hello`NotificationHubClient.CreateClientFromConnectionString`函式應該包含您就可以在 hello 的通知中樞的 hello 資訊[Azure 入口網站](https://portal.azure.com)(查看內部 hello**存取原則**刀鋒視窗中的**設定**)。 儲存 hello 更新的組態檔。

現在我們需要 toocreate 模型 hello Bing Maps API 結果。 hello 是以滑鼠右鍵按一下 hello 的最簡單方式 toodo`Models`資料夾，**新增** > **類別**。 將它命名為 `GeofenceBoundary.cs` 一旦完成，將從我們討論 hello 第一個區段中和使用 Visual Studio 中的 hello API 回應複製 hello JSON**編輯** > **貼** > **貼上 JSON做為類別**。 

這樣一來，我們會確保該 hello 物件完全依設計會還原序列化。 所產生的類別集應該會與下面類似︰

    namespace AppBackend.Models
    {
        public class Rootobject
        {
            public D d { get; set; }
        }

        public class D
        {
            public string __copyright { get; set; }
            public Result[] results { get; set; }
        }

        public class Result
        {
            public __Metadata __metadata { get; set; }
            public string EntityID { get; set; }
            public string Name { get; set; }
            public float Longitude { get; set; }
            public float Latitude { get; set; }
            public string Boundary { get; set; }
            public string Confidence { get; set; }
            public string Locality { get; set; }
            public string AddressLine { get; set; }
            public string AdminDistrict { get; set; }
            public string CountryRegion { get; set; }
            public string PostalCode { get; set; }
        }

        public class __Metadata
        {
            public string uri { get; set; }
        }
    }

接下來，開啟 `Controllers` > `NotificationsController.cs`。 我們需要 tootweak hello Post 呼叫 tooaccount hello 目標經度和緯度。 因此，只要加入兩個的字串 toohello 函式簽章 –`latitude`和`longitude`。

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

建立新的類別稱為 hello 專案內`ApiHelper.cs`– 我們將使用它 tooconnect tooBing toocheck 點界限交集。 實作類似下面的 `IsPointWithinBounds` 函式︰

    public class ApiHelper
    {
        public static readonly string ApiEndpoint = "{YOUR_QUERY_ENDPOINT}?spatialFilter=intersects(%27POINT%20({0}%20{1})%27)&$format=json&key={2}";
        public static readonly string ApiKey = "{YOUR_API_KEY}";

        public static bool IsPointWithinBounds(string longitude,string latitude)
        {
            var json = new WebClient().DownloadString(string.Format(ApiEndpoint, longitude, latitude, ApiKey));
            var result = JsonConvert.DeserializeObject<Rootobject>(json);
            if (result.d.results != null && result.d.results.Count() > 0)
            {
                return true;
            }
            else
            {
                return false;
            }
        }
    }

> [!NOTE]
> 請確定 toosubstitute hello API 端點，與您稍早取得的 hello Bing （相同適用於 toohello API 金鑰） 的開發人員中心的 hello 查詢 URL。 
> 
> 

如果有結果 toohello 查詢，hello 指定的點，就表示是 hello geofence hello 界限內所以我們決定傳回`true`。 如果不有任何結果，Bing 就告訴 hello 點外部 hello 查閱框架內，所以我們決定傳回`false`。

回到`NotificationsController.cs`，建立 hello switch 陳述式前的檢查：

    if (ApiHelper.IsPointWithinBounds(longitude, latitude))
    {
        switch (pns.ToLower())
        {
            case "wns":
                //// Windows 8.1 / Windows Phone 8.1
                var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                // Windows 10 specific Action Center support
                toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                break;
        }
    }

這樣一來，hello 通知只會傳送 hello 點 hello 界限內時。

## <a name="testing-push-notifications-in-hello-uwp-app"></a>在 hello UWP 應用程式中測試推播通知
返回 toohello UWP 應用程式，我們現在應該能夠 tootest 通知。 在 hello`LocationHelper`類別，建立新的函數 – `SendLocationToBackend`:

    public static async Task SendLocationToBackend(string pns, string userTag, string message, string latitude, string longitude)
    {
        var POST_URL = "http://localhost:8741/api/notifications?pns=" +
            pns + "&to_tag=" + userTag + "&latitude=" + latitude + "&longitude=" + longitude;

        using (var httpClient = new HttpClient())
        {
            try
            {
                await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                    System.Text.Encoding.UTF8, "application/json"));
            }
            catch (Exception ex)
            {
                Debug.WriteLine(ex.Message);
            }
        }
    }

> [!NOTE]
> 交換 hello `POST_URL` toohello hello 上一節中建立您已部署的 web 應用程式的位置。 現在，它是確定 toorun 它在本機，但是當您處理部署公用版本，您將需要 toohost 使用外部提供者。
> 
> 

現在請確定我們註冊推播通知的 hello UWP 應用程式。 在 Visual Studio 中，按一下**專案** > **儲存** > **與 hello 市集建立關聯的應用程式**。

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

一旦您登入 tooyour 開發人員帳戶，請確定您選取現有的應用程式或另外新建一個 hello 封裝關聯。 

請前往 toohello 開發人員中心開啟 hello 您剛才建立的應用程式。 按一下 [服務] > [推播通知] > [線上服務網站]。

![](./media/notification-hubs-geofence/ms-live-services.png)

Hello 在網站上，記下 hello**應用程式密碼**和 hello**封裝 SID**。 您必須同時在 hello Azure 入口網站 – 開啟 通知中樞，請按一下**設定** > **Notification Services** > **Windows (WNS)**和所需的 hello 欄位中輸入 hello 資訊。

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

按一下 [儲存] 。

在 [方案總管] 中，以滑鼠右鍵按一下 [參考]，然後選取 [管理 NuGet 套件]。 我們需要 tooadd 參考 toohello **Microsoft Azure 服務匯流排 managed 程式庫**– 只搜尋`WindowsAzure.Messaging.Managed`並將它加入 tooyour 專案。

![](./media/notification-hubs-geofence/vs-nuget.png)

為了測試用途，我們可以建立 hello`MainPage_Loaded`事件處理常式一次，並加入此程式碼片段 tooit:

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

上述的 hello 與 hello 通知中樞註冊 hello 應用程式。 您已準備好 toogo ！ 

在`LocationHelper`，內部 hello`Geolocator_PositionChanged`處理常式，您可以新增測試程式碼會強制使 hello 位置 hello geofence 內的部分：

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

因為我們不傳遞 hello 真實座標 （這可能不是 hello 界限內 hello 時間），並使用預先定義的測試值，我們會看到顯示更新通知：

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a>後續步驟
有幾個步驟，您可能需要 toofollow 加法 toohello 上方 toomake 確定 hello 方案可實際執行中。

首先和最重要，您可能需要 tooensure geofences 是動態的。 這將需要一些額外的工作，以在 hello 現有資料來源內的順序 toobe 無法 tooupload 新界限的 hello Bing 應用程式開發介面。 請參閱 hello [Bing 空間資料服務 API 文件](https://msdn.microsoft.com/library/ff701734.aspx)如需有關 hello 主旨。

第二，在您工作 tooensure hello 傳遞是 toohello 右參與者，您可能會想 tootarget 它們透過[標記](notification-hubs-tags-segment-push-message.md)。

如上所示的 hello 解決方案會說明的案例，其中可能有各種不同的目標平台，所以我們並未限制 hello 地理圍欄 toosystem 特定功能。 話雖如此，hello 通用 Windows 平台提供的功能，太[偵測 geofences 右--蜪鎏](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence)。

如需有關通知中樞功能的詳細資訊，請查看我們的 [說明文件入口網站](https://azure.microsoft.com/documentation/services/notification-hubs/)。

