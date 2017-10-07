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
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="6746a-104">使用 Azure 通知中樞和 Bing 空間資料為推播通知加上地理柵欄</span><span class="sxs-lookup"><span data-stu-id="6746a-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="6746a-105">toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6746a-105">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="6746a-106">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6746a-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6746a-107">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02)。</span><span class="sxs-lookup"><span data-stu-id="6746a-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="6746a-108">在本教學課程中，您將學習如何以位置為基礎的 toodeliver 將推播通知 Azure 通知中樞與 Bing 空間資料，從利用通用 Windows 平台應用程式中。</span><span class="sxs-lookup"><span data-stu-id="6746a-108">In this tutorial, you will learn how toodeliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6746a-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="6746a-109">Prerequisites</span></span>
<span data-ttu-id="6746a-110">首先和最重要，您需要確定您有所有 hello 軟體和服務先決條件 toomake:</span><span class="sxs-lookup"><span data-stu-id="6746a-110">First and foremost, you need toomake sure that you have all hello software and service pre-requisites:</span></span>

* <span data-ttu-id="6746a-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) 或更新版本 ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) 也行)。</span><span class="sxs-lookup"><span data-stu-id="6746a-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="6746a-112">最新版本的 hello [Azure SDK](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="6746a-112">Latest version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="6746a-113">[Bing 地圖服務開發人員中心帳戶](https://www.bingmapsportal.com/) (您可以免費建立帳戶並將此帳戶關聯到您的 Microsoft 帳戶)。</span><span class="sxs-lookup"><span data-stu-id="6746a-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="6746a-114">開始使用</span><span class="sxs-lookup"><span data-stu-id="6746a-114">Getting Started</span></span>
<span data-ttu-id="6746a-115">讓我們藉由建立 hello 專案開始。</span><span class="sxs-lookup"><span data-stu-id="6746a-115">Let’s start by creating hello project.</span></span> <span data-ttu-id="6746a-116">在 Visual Studio 中，開始 [空白應用程式 (通用 Windows)] 類型的新專案。</span><span class="sxs-lookup"><span data-stu-id="6746a-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="6746a-117">Hello 專案建立完成之後，您應該有 hello 應用程式本身的 hello 控管。</span><span class="sxs-lookup"><span data-stu-id="6746a-117">Once hello project creation is complete, you should have hello harness for hello app itself.</span></span> <span data-ttu-id="6746a-118">現在讓我們設定 hello 異地隔離基礎結構的所有項目。</span><span class="sxs-lookup"><span data-stu-id="6746a-118">Now let’s set up everything for hello geo-fencing infrastructure.</span></span> <span data-ttu-id="6746a-119">我們會持續 toouse Bing 的此服務，因為沒有公用的 REST API 端點，讓我們 tooquery 特定位置框架：</span><span class="sxs-lookup"><span data-stu-id="6746a-119">Because we are going toouse Bing services for this, there is a public REST API endpoint that allows us tooquery specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="6746a-120">您將需要 toospecify hello 下列參數 tooget 運作：</span><span class="sxs-lookup"><span data-stu-id="6746a-120">You will need toospecify hello following parameters tooget it working:</span></span>

* <span data-ttu-id="6746a-121">**資料來源識別碼**和**資料來源名稱** – 在 Bing 地圖服務 API 中，資料來源包含了各種分門別類的中繼資料，例如營業據點和營業時間。</span><span class="sxs-lookup"><span data-stu-id="6746a-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="6746a-122">您可以在此了解其相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6746a-122">You can read more about those here.</span></span> 
* <span data-ttu-id="6746a-123">**實體名稱**– hello hello 通知想 toouse 作為參考點的實體。</span><span class="sxs-lookup"><span data-stu-id="6746a-123">**Entity Name** – hello entity you want toouse as a reference point for hello notification.</span></span> 
* <span data-ttu-id="6746a-124">**Bing 地圖服務 API 金鑰**– 這是當您建立 hello Bing 開發人員中心帳戶稍早取得的 hello 金鑰。</span><span class="sxs-lookup"><span data-stu-id="6746a-124">**Bing Maps API Key** – this is hello key that you obtained earlier when you created hello Bing Dev Center account.</span></span>

<span data-ttu-id="6746a-125">就來看看深入了解在 hello 設定每個以上的 hello 元件。</span><span class="sxs-lookup"><span data-stu-id="6746a-125">Let’s do a deep-dive on hello setup for each of hello elements above.</span></span>

## <a name="setting-up-hello-data-source"></a><span data-ttu-id="6746a-126">設定 hello 資料來源</span><span class="sxs-lookup"><span data-stu-id="6746a-126">Setting up hello data source</span></span>
<span data-ttu-id="6746a-127">您可以在 hello Bing 地圖服務開發人員中心中執行動作。</span><span class="sxs-lookup"><span data-stu-id="6746a-127">You can do it in hello Bing Maps Dev Center.</span></span> <span data-ttu-id="6746a-128">只要按一下**資料來源**hello 上方導覽列，然後選取在**管理資料來源**。</span><span class="sxs-lookup"><span data-stu-id="6746a-128">Simply click on **Data sources** in hello top navigation bar and select **Manage Data Sources**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="6746a-129">如果您已不使用 Bing Maps API 之前，很可能不會有任何資料來源存在，因此您只可以建立一個新上傳資料 tooa 資料來源上的。</span><span class="sxs-lookup"><span data-stu-id="6746a-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data tooa data source.</span></span> <span data-ttu-id="6746a-130">請確定您填寫所有必要的 hello 欄位：</span><span class="sxs-lookup"><span data-stu-id="6746a-130">Make sure you fill out all hello required fields:</span></span>

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="6746a-131">您可能會懷疑 – 何謂 hello 資料檔案和項目應該您要上傳嗎？</span><span class="sxs-lookup"><span data-stu-id="6746a-131">You might be wondering – what is hello data file and what should you be uploading?</span></span> <span data-ttu-id="6746a-132">基於 hello 這項測試，我們就可以使用管道為基礎的畫面格的區域 hello San Francisco waterfront hello 範例：</span><span class="sxs-lookup"><span data-stu-id="6746a-132">For hello purposes of this test, we can just use hello sample pipe-based that frames an area of hello San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="6746a-133">上述的 hello 代表此實體：</span><span class="sxs-lookup"><span data-stu-id="6746a-133">hello above represents this entity:</span></span>

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="6746a-134">只複製並貼到新檔案的上述 hello 字串，然後將它儲存成**NotificationHubsGeofence.pipe**，並將它上傳 hello Bing 開發人員中心中。</span><span class="sxs-lookup"><span data-stu-id="6746a-134">Simply copy and paste hello string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in hello Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="6746a-135">您可能會提示的 toospecify hello 的新索引鍵**主要金鑰**不同 hello**查詢索引鍵**。</span><span class="sxs-lookup"><span data-stu-id="6746a-135">You might be prompted toospecify a new key for hello **Master Key** that is different from hello **Query Key**.</span></span> <span data-ttu-id="6746a-136">只要建立新的金鑰透過 hello 儀表板和重新整理 hello 資料來源上傳頁面。</span><span class="sxs-lookup"><span data-stu-id="6746a-136">Simply create a new key through hello dashboard and refresh hello data source upload page.</span></span>
> 
> 

<span data-ttu-id="6746a-137">之後您上傳 hello 資料檔案，您必須確定您 hello 資料來源發行 toomake。</span><span class="sxs-lookup"><span data-stu-id="6746a-137">Once you upload hello data file, you will need toomake sure that you publish hello data source.</span></span> 

<span data-ttu-id="6746a-138">跳過**管理資料來源**，如同我們上方、 hello 清單中尋找您的資料來源，按一下**發行**在 hello**動作**資料行。</span><span class="sxs-lookup"><span data-stu-id="6746a-138">Go too**Manage Data Sources**, just like we did above, find your data source in hello list and click on **Publish** in hello **Actions** column.</span></span> <span data-ttu-id="6746a-139">在位元，您應該會看到您的資料來源中 hello**發行資料來源** 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="6746a-139">In a bit, you should see your data source in hello **Published Data Sources** tab:</span></span>

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="6746a-140">如果您按一下**編輯**，您將可以一眼 toosee 我們見於哪些位置：</span><span class="sxs-lookup"><span data-stu-id="6746a-140">If you click **Edit**, you will be able toosee at a glance what locations we introduced in it:</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="6746a-141">此時，hello 入口網站不會顯示 hello 界限，我們建立的 hello geofence – 我們只需要指定 hello 位置是在 hello 右邊區域的確認。</span><span class="sxs-lookup"><span data-stu-id="6746a-141">At this point, hello portal does not show you hello boundaries for hello geofence that we created – all we need is a confirmation that hello location specified is in hello right vicinity.</span></span>

<span data-ttu-id="6746a-142">現在您有 hello 資料來源的所有 hello 需求。</span><span class="sxs-lookup"><span data-stu-id="6746a-142">Now you have all hello requirements for hello data source.</span></span> <span data-ttu-id="6746a-143">tooget hello 詳細資料，對於 hello API 呼叫，在 hello Bing 地圖服務開發人員中心，hello 要求 URL 上的按一下**資料來源**選取**資料來源資訊**。</span><span class="sxs-lookup"><span data-stu-id="6746a-143">tooget hello details on hello request URL for hello API call, in hello Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="6746a-144">hello**查詢 URL**是我們在這裡之後。</span><span class="sxs-lookup"><span data-stu-id="6746a-144">hello **Query URL** is what we’re after here.</span></span> <span data-ttu-id="6746a-145">這是依據我們可以執行查詢 toocheck 是否 hello 裝置目前的位置 hello 界限內的 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="6746a-145">This is hello endpoint against which we can execute queries toocheck whether hello device is currently within hello boundaries of a location or not.</span></span> <span data-ttu-id="6746a-146">此核取，我們只需要的 tooexecute GET 呼叫 hello 查詢 URL，針對下列參數附加 hello tooperform:</span><span class="sxs-lookup"><span data-stu-id="6746a-146">tooperform this check, we simply need tooexecute a GET call against hello query URL, with hello following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="6746a-147">如此一來，您會指定目標時間點，我們取得 hello 裝置的 Bing 地圖服務會自動執行 hello 計算 toosee，它是否 hello geofence 內。</span><span class="sxs-lookup"><span data-stu-id="6746a-147">That way you're specifying a target point that we obtain from hello device and Bing Maps will automatically perform hello calculations toosee whether it is within hello geofence.</span></span> <span data-ttu-id="6746a-148">一旦您執行瀏覽器 （或 cURL） hello 要求時，您會收到標準 JSON 回應：</span><span class="sxs-lookup"><span data-stu-id="6746a-148">Once you execute hello request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](./media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="6746a-149">這個回應只會發生在 hello 點實際上 hello 指定界限內。</span><span class="sxs-lookup"><span data-stu-id="6746a-149">This response only happens when hello point is actually within hello designated boundaries.</span></span> <span data-ttu-id="6746a-150">如果不在邊界內，您將會收到空白的 **results** 分類︰</span><span class="sxs-lookup"><span data-stu-id="6746a-150">If it is not, you will get an empty **results** bucket:</span></span>

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a><span data-ttu-id="6746a-151">設定 hello UWP 應用程式</span><span class="sxs-lookup"><span data-stu-id="6746a-151">Setting up hello UWP application</span></span>
<span data-ttu-id="6746a-152">現在，我們已經準備好的 hello 資料來源時，我們可以開始處理 hello 我們稍早引導的 UWP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6746a-152">Now that we have hello data source ready, we can start working on hello UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="6746a-153">首先，我們必須啟用應用程式的位置服務。</span><span class="sxs-lookup"><span data-stu-id="6746a-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="6746a-154">toodo，連按兩下`Package.appxmanifest`檔案**方案總管 中**。</span><span class="sxs-lookup"><span data-stu-id="6746a-154">toodo this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](./media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="6746a-155">Hello 封裝屬性 索引標籤中所開啟，按一下**功能**，並確定您選取**位置**:</span><span class="sxs-lookup"><span data-stu-id="6746a-155">In hello package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](./media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="6746a-156">為已宣告 hello 位置功能，建立新的資料夾中名為方案`Core`，並加入新的檔案，稱為`LocationHelper.cs`:</span><span class="sxs-lookup"><span data-stu-id="6746a-156">As hello location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](./media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="6746a-157">hello`LocationHelper`類別本身是相當基本此時 – 它是讓我們透過 hello 系統 API tooobtain hello 使用者位置：</span><span class="sxs-lookup"><span data-stu-id="6746a-157">hello `LocationHelper` class itself is fairly basic at this point – all it does is allow us tooobtain hello user location through hello system API:</span></span>

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

<span data-ttu-id="6746a-158">您可以閱讀更多有關取得 hello hello 官方 UWP 應用程式中的使用者的位置[MSDN 文件](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6746a-158">You can read more about getting hello user’s location in UWP apps in hello official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="6746a-159">toocheck hello 位置擷取實際運作，開啟您的主頁面的 hello 程式碼端 (`MainPage.xaml.cs`)。</span><span class="sxs-lookup"><span data-stu-id="6746a-159">toocheck that hello location acquisition is actually working, open hello code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="6746a-160">建立新的事件處理常式，如 hello `Loaded` hello 中的事件`MainPage`建構函式：</span><span class="sxs-lookup"><span data-stu-id="6746a-160">Create a new event handler for hello `Loaded` event in hello `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="6746a-161">hello 實作 hello 事件處理常式如下所示：</span><span class="sxs-lookup"><span data-stu-id="6746a-161">hello implementation of hello event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="6746a-162">請注意我們宣告為非同步 hello 處理常式因為`GetCurrentLocation`是 awaitable，並因此需要 toobe 非同步內容中執行。</span><span class="sxs-lookup"><span data-stu-id="6746a-162">Notice that we declared hello handler as async because `GetCurrentLocation` is awaitable, and therefore requires toobe executed in an async context.</span></span> <span data-ttu-id="6746a-163">此外，因為在某些情況下我們最後可能會與 null 的位置 （例如 hello 位置服務停用或 hello 應用程式被拒絕的權限 tooaccess 位置），我們需要 toomake 確定它適當處理 null 檢查。</span><span class="sxs-lookup"><span data-stu-id="6746a-163">Also, because under certain circumstances we might end up with a null location (e.g. hello location services are disabled or hello application was denied permissions tooaccess location), we need toomake sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="6746a-164">執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6746a-164">Run hello application.</span></span> <span data-ttu-id="6746a-165">請確定您允許其存取位置︰</span><span class="sxs-lookup"><span data-stu-id="6746a-165">Make sure you allow location access:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="6746a-166">一次 hello 應用程式會啟動，您應該能夠 toosee hello 座標在 hello**輸出**視窗：</span><span class="sxs-lookup"><span data-stu-id="6746a-166">Once hello application launches, you should be able toosee hello coordinates in hello **Output** window:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="6746a-167">現在您已經瞭解的位置擷取 works – 覺得可用 tooremove hello 測試事件處理常式的載入因為我們將不會使用它不再。</span><span class="sxs-lookup"><span data-stu-id="6746a-167">Now you know that location acquisition works – feel free tooremove hello test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="6746a-168">hello 下一個步驟是 toocapture 位置變更。</span><span class="sxs-lookup"><span data-stu-id="6746a-168">hello next step is toocapture location changes.</span></span> <span data-ttu-id="6746a-169">為此，請回復 toohello`LocationHelper`類別，然後將 hello 事件處理常式`PositionChanged`:</span><span class="sxs-lookup"><span data-stu-id="6746a-169">For that, let’s go back toohello `LocationHelper` class and add hello event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="6746a-170">hello 實作將會顯示 hello 位置座標在 hello**輸出**視窗：</span><span class="sxs-lookup"><span data-stu-id="6746a-170">hello implementation will show hello location coordinates in hello **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a><span data-ttu-id="6746a-171">Hello 後端設定</span><span class="sxs-lookup"><span data-stu-id="6746a-171">Setting up hello backend</span></span>
<span data-ttu-id="6746a-172">下載 hello [.NET 後端範例從 GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers)。</span><span class="sxs-lookup"><span data-stu-id="6746a-172">Download hello [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="6746a-173">Hello 下載完成之後，請開啟 hello`NotifyUsers`資料夾，然後後續 – hello`NotifyUsers.sln`檔案。</span><span class="sxs-lookup"><span data-stu-id="6746a-173">Once hello download completes, open hello `NotifyUsers` folder, and subsequently – hello `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="6746a-174">設定 hello `AppBackend` hello 與專案**啟始專案**並啟動它。</span><span class="sxs-lookup"><span data-stu-id="6746a-174">Set hello `AppBackend` project as hello **StartUp Project** and launch it.</span></span>

![](./media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="6746a-175">hello 專案已經設定的 toosend 推播通知 tootarget 裝置，因此我們必須 toodo 只有兩個項目 – 抽換 hello 正確的連接字串 hello 通知中樞，並將界限識別 toosend hello 通知時，才 hello使用者是 hello geofence 內。</span><span class="sxs-lookup"><span data-stu-id="6746a-175">hello project is already configured toosend push notifications tootarget devices, so we’ll need toodo only two things – swap out hello right connection string for hello notification hub and add boundary identification toosend hello notification only when hello user is within hello geofence.</span></span>

<span data-ttu-id="6746a-176">tooconfigure hello 連接字串，在 hello`Models`資料夾開啟`Notifications.cs`。</span><span class="sxs-lookup"><span data-stu-id="6746a-176">tooconfigure hello connection string, in hello `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="6746a-177">hello`NotificationHubClient.CreateClientFromConnectionString`函式應該包含您就可以在 hello 的通知中樞的 hello 資訊[Azure 入口網站](https://portal.azure.com)(查看內部 hello**存取原則**刀鋒視窗中的**設定**)。</span><span class="sxs-lookup"><span data-stu-id="6746a-177">hello `NotificationHubClient.CreateClientFromConnectionString` function should contain hello information about your notification hub that you can get in hello [Azure Portal](https://portal.azure.com) (look inside hello **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="6746a-178">儲存 hello 更新的組態檔。</span><span class="sxs-lookup"><span data-stu-id="6746a-178">Save hello updated configuration file.</span></span>

<span data-ttu-id="6746a-179">現在我們需要 toocreate 模型 hello Bing Maps API 結果。</span><span class="sxs-lookup"><span data-stu-id="6746a-179">Now we need toocreate a model for hello Bing Maps API result.</span></span> <span data-ttu-id="6746a-180">hello 是以滑鼠右鍵按一下 hello 的最簡單方式 toodo`Models`資料夾，**新增** > **類別**。</span><span class="sxs-lookup"><span data-stu-id="6746a-180">hello easiest way toodo that is right-click on hello `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="6746a-181">將它命名為 `GeofenceBoundary.cs`</span><span class="sxs-lookup"><span data-stu-id="6746a-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="6746a-182">一旦完成，將從我們討論 hello 第一個區段中和使用 Visual Studio 中的 hello API 回應複製 hello JSON**編輯** > **貼** > **貼上 JSON做為類別**。</span><span class="sxs-lookup"><span data-stu-id="6746a-182">Once done, copy hello JSON from hello API response that we discussed in hello first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="6746a-183">這樣一來，我們會確保該 hello 物件完全依設計會還原序列化。</span><span class="sxs-lookup"><span data-stu-id="6746a-183">That way we ensure that hello object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="6746a-184">所產生的類別集應該會與下面類似︰</span><span class="sxs-lookup"><span data-stu-id="6746a-184">Your resulting class set should resemble this:</span></span>

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

<span data-ttu-id="6746a-185">接下來，開啟 `Controllers` > `NotificationsController.cs`。</span><span class="sxs-lookup"><span data-stu-id="6746a-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="6746a-186">我們需要 tootweak hello Post 呼叫 tooaccount hello 目標經度和緯度。</span><span class="sxs-lookup"><span data-stu-id="6746a-186">We need tootweak hello Post call tooaccount for hello target longitude and latitude.</span></span> <span data-ttu-id="6746a-187">因此，只要加入兩個的字串 toohello 函式簽章 –`latitude`和`longitude`。</span><span class="sxs-lookup"><span data-stu-id="6746a-187">For that, simply add two strings toohello function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="6746a-188">建立新的類別稱為 hello 專案內`ApiHelper.cs`– 我們將使用它 tooconnect tooBing toocheck 點界限交集。</span><span class="sxs-lookup"><span data-stu-id="6746a-188">Create a new class within hello project called `ApiHelper.cs` – we’ll use it tooconnect tooBing toocheck point boundary intersections.</span></span> <span data-ttu-id="6746a-189">實作類似下面的 `IsPointWithinBounds` 函式︰</span><span class="sxs-lookup"><span data-stu-id="6746a-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

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
> <span data-ttu-id="6746a-190">請確定 toosubstitute hello API 端點，與您稍早取得的 hello Bing （相同適用於 toohello API 金鑰） 的開發人員中心的 hello 查詢 URL。</span><span class="sxs-lookup"><span data-stu-id="6746a-190">Make sure toosubstitute hello API endpoint with hello query URL that you obtained earlier from hello Bing Dev Center (same applies toohello API key).</span></span> 
> 
> 

<span data-ttu-id="6746a-191">如果有結果 toohello 查詢，hello 指定的點，就表示是 hello geofence hello 界限內所以我們決定傳回`true`。</span><span class="sxs-lookup"><span data-stu-id="6746a-191">If there are results toohello query, that means that hello specified point is within hello boundaries of hello geofence, so we return `true`.</span></span> <span data-ttu-id="6746a-192">如果不有任何結果，Bing 就告訴 hello 點外部 hello 查閱框架內，所以我們決定傳回`false`。</span><span class="sxs-lookup"><span data-stu-id="6746a-192">If there are no results, Bing is telling us that hello point is outside hello lookup frame, so we return `false`.</span></span>

<span data-ttu-id="6746a-193">回到`NotificationsController.cs`，建立 hello switch 陳述式前的檢查：</span><span class="sxs-lookup"><span data-stu-id="6746a-193">Back in `NotificationsController.cs`, create a check right before hello switch statement:</span></span>

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

<span data-ttu-id="6746a-194">這樣一來，hello 通知只會傳送 hello 點 hello 界限內時。</span><span class="sxs-lookup"><span data-stu-id="6746a-194">That way, hello notification is only sent when hello point is within hello boundaries.</span></span>

## <a name="testing-push-notifications-in-hello-uwp-app"></a><span data-ttu-id="6746a-195">在 hello UWP 應用程式中測試推播通知</span><span class="sxs-lookup"><span data-stu-id="6746a-195">Testing push notifications in hello UWP app</span></span>
<span data-ttu-id="6746a-196">返回 toohello UWP 應用程式，我們現在應該能夠 tootest 通知。</span><span class="sxs-lookup"><span data-stu-id="6746a-196">Going back toohello UWP app, we should now be able tootest notifications.</span></span> <span data-ttu-id="6746a-197">在 hello`LocationHelper`類別，建立新的函數 – `SendLocationToBackend`:</span><span class="sxs-lookup"><span data-stu-id="6746a-197">Within hello `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

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
> <span data-ttu-id="6746a-198">交換 hello `POST_URL` toohello hello 上一節中建立您已部署的 web 應用程式的位置。</span><span class="sxs-lookup"><span data-stu-id="6746a-198">Swap hello `POST_URL` toohello location of your deployed web application that we created in hello previous section.</span></span> <span data-ttu-id="6746a-199">現在，它是確定 toorun 它在本機，但是當您處理部署公用版本，您將需要 toohost 使用外部提供者。</span><span class="sxs-lookup"><span data-stu-id="6746a-199">For now, it’s OK toorun it locally, but as you work on deploying a public version, you will need toohost it with an external provider.</span></span>
> 
> 

<span data-ttu-id="6746a-200">現在請確定我們註冊推播通知的 hello UWP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6746a-200">Let’s now make sure that we register hello UWP app for push notifications.</span></span> <span data-ttu-id="6746a-201">在 Visual Studio 中，按一下**專案** > **儲存** > **與 hello 市集建立關聯的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6746a-201">In Visual Studio, click on **Project** > **Store** > **Associate app with hello store**.</span></span>

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="6746a-202">一旦您登入 tooyour 開發人員帳戶，請確定您選取現有的應用程式或另外新建一個 hello 封裝關聯。</span><span class="sxs-lookup"><span data-stu-id="6746a-202">Once you sign in tooyour developer account, make sure you select an existing app or create a new one and associate hello package with it.</span></span> 

<span data-ttu-id="6746a-203">請前往 toohello 開發人員中心開啟 hello 您剛才建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6746a-203">Go toohello Dev Center and open hello app that you just created.</span></span> <span data-ttu-id="6746a-204">按一下 [服務] > [推播通知] > [線上服務網站]。</span><span class="sxs-lookup"><span data-stu-id="6746a-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](./media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="6746a-205">Hello 在網站上，記下 hello**應用程式密碼**和 hello**封裝 SID**。</span><span class="sxs-lookup"><span data-stu-id="6746a-205">On hello site, take note of hello **Application Secret** and hello **Package SID**.</span></span> <span data-ttu-id="6746a-206">您必須同時在 hello Azure 入口網站 – 開啟 通知中樞，請按一下**設定** > **Notification Services** > **Windows (WNS)**和所需的 hello 欄位中輸入 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="6746a-206">You will need both in hello Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter hello information in hello required fields.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="6746a-207">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6746a-207">Click on **Save**.</span></span>

<span data-ttu-id="6746a-208">在 [方案總管] 中，以滑鼠右鍵按一下 [參考]，然後選取 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="6746a-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="6746a-209">我們需要 tooadd 參考 toohello **Microsoft Azure 服務匯流排 managed 程式庫**– 只搜尋`WindowsAzure.Messaging.Managed`並將它加入 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="6746a-209">We will need tooadd a reference toohello **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it tooyour project.</span></span>

![](./media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="6746a-210">為了測試用途，我們可以建立 hello`MainPage_Loaded`事件處理常式一次，並加入此程式碼片段 tooit:</span><span class="sxs-lookup"><span data-stu-id="6746a-210">For testing purposes, we can create hello `MainPage_Loaded` event handler once again, and add this code snippet tooit:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="6746a-211">上述的 hello 與 hello 通知中樞註冊 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6746a-211">hello above registers hello app with hello notification hub.</span></span> <span data-ttu-id="6746a-212">您已準備好 toogo ！</span><span class="sxs-lookup"><span data-stu-id="6746a-212">You are ready toogo!</span></span> 

<span data-ttu-id="6746a-213">在`LocationHelper`，內部 hello`Geolocator_PositionChanged`處理常式，您可以新增測試程式碼會強制使 hello 位置 hello geofence 內的部分：</span><span class="sxs-lookup"><span data-stu-id="6746a-213">In `LocationHelper`, inside hello `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put hello location inside hello geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="6746a-214">因為我們不傳遞 hello 真實座標 （這可能不是 hello 界限內 hello 時間），並使用預先定義的測試值，我們會看到顯示更新通知：</span><span class="sxs-lookup"><span data-stu-id="6746a-214">Because we are not passing hello real coordinates (which might not be within hello boundaries at hello moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="6746a-215">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6746a-215">What’s next?</span></span>
<span data-ttu-id="6746a-216">有幾個步驟，您可能需要 toofollow 加法 toohello 上方 toomake 確定 hello 方案可實際執行中。</span><span class="sxs-lookup"><span data-stu-id="6746a-216">There are a couple of steps that you might need toofollow in addition toohello above toomake sure that hello solution is production-ready.</span></span>

<span data-ttu-id="6746a-217">首先和最重要，您可能需要 tooensure geofences 是動態的。</span><span class="sxs-lookup"><span data-stu-id="6746a-217">First and foremost, you might need tooensure that geofences are dynamic.</span></span> <span data-ttu-id="6746a-218">這將需要一些額外的工作，以在 hello 現有資料來源內的順序 toobe 無法 tooupload 新界限的 hello Bing 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="6746a-218">This will require some extra work with hello Bing API in order toobe able tooupload new boundaries within hello existing data source.</span></span> <span data-ttu-id="6746a-219">請參閱 hello [Bing 空間資料服務 API 文件](https://msdn.microsoft.com/library/ff701734.aspx)如需有關 hello 主旨。</span><span class="sxs-lookup"><span data-stu-id="6746a-219">Consult hello [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on hello subject.</span></span>

<span data-ttu-id="6746a-220">第二，在您工作 tooensure hello 傳遞是 toohello 右參與者，您可能會想 tootarget 它們透過[標記](notification-hubs-tags-segment-push-message.md)。</span><span class="sxs-lookup"><span data-stu-id="6746a-220">Second, as you are working tooensure that hello delivery is done toohello right participants, you might want tootarget them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="6746a-221">如上所示的 hello 解決方案會說明的案例，其中可能有各種不同的目標平台，所以我們並未限制 hello 地理圍欄 toosystem 特定功能。</span><span class="sxs-lookup"><span data-stu-id="6746a-221">hello solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit hello geofencing toosystem-specific capabilities.</span></span> <span data-ttu-id="6746a-222">話雖如此，hello 通用 Windows 平台提供的功能，太[偵測 geofences 右--蜪鎏](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence)。</span><span class="sxs-lookup"><span data-stu-id="6746a-222">That said, hello Universal Windows Platform offers capabilities too[detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="6746a-223">如需有關通知中樞功能的詳細資訊，請查看我們的 [說明文件入口網站](https://azure.microsoft.com/documentation/services/notification-hubs/)。</span><span class="sxs-lookup"><span data-stu-id="6746a-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>

