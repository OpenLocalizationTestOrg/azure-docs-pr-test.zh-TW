---
title: "使用 Azure 通知中樞和 Bing 空間資料為推播通知加上地理柵欄 | Microsoft Docs"
description: "在本教學課程中，您將學習如何使用 Azure 通知中樞和 Bing 空間資料來傳遞以位置為基礎的推播通知。"
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
ms.openlocfilehash: b2a84e0479aac9ded08bb64e1ea20ddee6636cce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="fc783-104">使用 Azure 通知中樞和 Bing 空間資料為推播通知加上地理柵欄</span><span class="sxs-lookup"><span data-stu-id="fc783-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="fc783-105">若要完成此教學課程，您必須具備有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fc783-105">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="fc783-106">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fc783-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fc783-107">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02)。</span><span class="sxs-lookup"><span data-stu-id="fc783-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="fc783-108">在本教學課程中，您將學習如何從通用 Windows 平台應用程式，運用 Azure 通知中樞和 Bing 空間資料來傳遞以位置為基礎的推播通知。</span><span class="sxs-lookup"><span data-stu-id="fc783-108">In this tutorial, you will learn how to deliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc783-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="fc783-109">Prerequisites</span></span>
<span data-ttu-id="fc783-110">首先，您必須確定您擁有所有必要的軟體和服務︰</span><span class="sxs-lookup"><span data-stu-id="fc783-110">First and foremost, you need to make sure that you have all the software and service pre-requisites:</span></span>

* <span data-ttu-id="fc783-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) 或更新版本 ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) 也行)。</span><span class="sxs-lookup"><span data-stu-id="fc783-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="fc783-112">最新版的 [Azure SDK](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="fc783-112">Latest version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="fc783-113">[Bing 地圖服務開發人員中心帳戶](https://www.bingmapsportal.com/) (您可以免費建立帳戶並將此帳戶關聯到您的 Microsoft 帳戶)。</span><span class="sxs-lookup"><span data-stu-id="fc783-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="fc783-114">開始使用</span><span class="sxs-lookup"><span data-stu-id="fc783-114">Getting Started</span></span>
<span data-ttu-id="fc783-115">一開始請先建立專案。</span><span class="sxs-lookup"><span data-stu-id="fc783-115">Let’s start by creating the project.</span></span> <span data-ttu-id="fc783-116">在 Visual Studio 中，開始 [空白應用程式 (通用 Windows)] 類型的新專案。</span><span class="sxs-lookup"><span data-stu-id="fc783-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="fc783-117">建立好專案之後，您應該就能控管應用程式本身。</span><span class="sxs-lookup"><span data-stu-id="fc783-117">Once the project creation is complete, you should have the harness for the app itself.</span></span> <span data-ttu-id="fc783-118">現在讓我們來進行地理柵欄基礎結構的各項設定。</span><span class="sxs-lookup"><span data-stu-id="fc783-118">Now let’s set up everything for the geo-fencing infrastructure.</span></span> <span data-ttu-id="fc783-119">由於我們會使用 Bing 服務來進行這項作業，因此會有可供我們查詢特定位置框架的公用 REST API 端點︰</span><span class="sxs-lookup"><span data-stu-id="fc783-119">Because we are going to use Bing services for this, there is a public REST API endpoint that allows us to query specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="fc783-120">您必須指定下列參數以讓端點開始運作︰</span><span class="sxs-lookup"><span data-stu-id="fc783-120">You will need to specify the following parameters to get it working:</span></span>

* <span data-ttu-id="fc783-121">**資料來源識別碼**和**資料來源名稱** – 在 Bing 地圖服務 API 中，資料來源包含了各種分門別類的中繼資料，例如營業據點和營業時間。</span><span class="sxs-lookup"><span data-stu-id="fc783-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="fc783-122">您可以在此了解其相關資訊。</span><span class="sxs-lookup"><span data-stu-id="fc783-122">You can read more about those here.</span></span> 
* <span data-ttu-id="fc783-123">**實體名稱** – 您想要作為通知參考點的實體。</span><span class="sxs-lookup"><span data-stu-id="fc783-123">**Entity Name** – the entity you want to use as a reference point for the notification.</span></span> 
* <span data-ttu-id="fc783-124">**Bing 地圖服務 API 金鑰** – 這是您稍早建立 Bing 開發人員中心帳戶時取得的金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc783-124">**Bing Maps API Key** – this is the key that you obtained earlier when you created the Bing Dev Center account.</span></span>

<span data-ttu-id="fc783-125">接著讓我們來深入了解上述各個項目的設定。</span><span class="sxs-lookup"><span data-stu-id="fc783-125">Let’s do a deep-dive on the setup for each of the elements above.</span></span>

## <a name="setting-up-the-data-source"></a><span data-ttu-id="fc783-126">設定資料來源</span><span class="sxs-lookup"><span data-stu-id="fc783-126">Setting up the data source</span></span>
<span data-ttu-id="fc783-127">您可以在 Bing 地圖服務開發人員中心進行此設定。</span><span class="sxs-lookup"><span data-stu-id="fc783-127">You can do it in the Bing Maps Dev Center.</span></span> <span data-ttu-id="fc783-128">請直接按一下上方導覽列中的 [資料來源]，然後選取 [管理資料來源]。</span><span class="sxs-lookup"><span data-stu-id="fc783-128">Simply click on **Data sources** in the top navigation bar and select **Manage Data Sources**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="fc783-129">如果您之前未曾用過 Bing 地圖服務 API，裡面很可能不會有任何資料來源，因此您可以直接按一下 [上傳資料到資料來源] 來建立新的資料來源。</span><span class="sxs-lookup"><span data-stu-id="fc783-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data to a data source.</span></span> <span data-ttu-id="fc783-130">請確實填寫所有必要欄位︰</span><span class="sxs-lookup"><span data-stu-id="fc783-130">Make sure you fill out all the required fields:</span></span>

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="fc783-131">您可能想知道什麼是資料檔案，以及應該上傳什麼資料？</span><span class="sxs-lookup"><span data-stu-id="fc783-131">You might be wondering – what is the data file and what should you be uploading?</span></span> <span data-ttu-id="fc783-132">就這項測試來說，我們可以直接使用框起舊金山濱水區的管道式範例︰</span><span class="sxs-lookup"><span data-stu-id="fc783-132">For the purposes of this test, we can just use the sample pipe-based that frames an area of the San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="fc783-133">上述程式碼代表以下實體︰</span><span class="sxs-lookup"><span data-stu-id="fc783-133">The above represents this entity:</span></span>

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="fc783-134">直接將上述字串複製並貼到新檔案、將它另存為 **NotificationHubsGeofence.pipe**，然後上傳到 Bing 開發人員中心。</span><span class="sxs-lookup"><span data-stu-id="fc783-134">Simply copy and paste the string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in the Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="fc783-135">您可能會收到提示，要求您為 [主要金鑰] 指定不同於 [查詢金鑰] 的新金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc783-135">You might be prompted to specify a new key for the **Master Key** that is different from the **Query Key**.</span></span> <span data-ttu-id="fc783-136">請直接透過儀表板建立新的金鑰，然後重新整理資料來源上傳頁面。</span><span class="sxs-lookup"><span data-stu-id="fc783-136">Simply create a new key through the dashboard and refresh the data source upload page.</span></span>
> 
> 

<span data-ttu-id="fc783-137">上傳資料檔案後，您必須確實發佈資料來源。</span><span class="sxs-lookup"><span data-stu-id="fc783-137">Once you upload the data file, you will need to make sure that you publish the data source.</span></span> 

<span data-ttu-id="fc783-138">移至 **[管理資料來源]** \(方法同前)、在清單中找到您的資料來源，然後按一下 [動作] 欄中的 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="fc783-138">Go to **Manage Data Sources**, just like we did above, find your data source in the list and click on **Publish** in the **Actions** column.</span></span> <span data-ttu-id="fc783-139">不用多久，您應該就會在 [已發佈的資料來源]  索引標籤中看到您的資料來源︰</span><span class="sxs-lookup"><span data-stu-id="fc783-139">In a bit, you should see your data source in the **Published Data Sources** tab:</span></span>

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="fc783-140">如果您按一下 [編輯] ，將可以一眼看到我們在其中引進的所有位置︰</span><span class="sxs-lookup"><span data-stu-id="fc783-140">If you click **Edit**, you will be able to see at a glance what locations we introduced in it:</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="fc783-141">此時，入口網站並不會顯示我們建立之地理柵欄的邊界，我們只需要確認指定的位置位於適當區域內。</span><span class="sxs-lookup"><span data-stu-id="fc783-141">At this point, the portal does not show you the boundaries for the geofence that we created – all we need is a confirmation that the location specified is in the right vicinity.</span></span>

<span data-ttu-id="fc783-142">現在您已符合資料來源的所有要求。</span><span class="sxs-lookup"><span data-stu-id="fc783-142">Now you have all the requirements for the data source.</span></span> <span data-ttu-id="fc783-143">若要取得 API 呼叫之要求 URL 的詳細資料，請在 Bing 地圖服務開發人員中心按一下 [資料來源]，然後選取 [資料來源資訊]。</span><span class="sxs-lookup"><span data-stu-id="fc783-143">To get the details on the request URL for the API call, in the Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="fc783-144">在這裡我們要找的是 [查詢 URL]  。</span><span class="sxs-lookup"><span data-stu-id="fc783-144">The **Query URL** is what we’re after here.</span></span> <span data-ttu-id="fc783-145">我們可以對此端點執行查詢，以檢查裝置目前是否位於某個位置的邊界內。</span><span class="sxs-lookup"><span data-stu-id="fc783-145">This is the endpoint against which we can execute queries to check whether the device is currently within the boundaries of a location or not.</span></span> <span data-ttu-id="fc783-146">若要執行這項檢查，我們只需要對查詢 URL 執行 GET 呼叫，並附加下列參數︰</span><span class="sxs-lookup"><span data-stu-id="fc783-146">To perform this check, we simply need to execute a GET call against the query URL, with the following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="fc783-147">這樣一來，您將會指定取自裝置的目標位置點，而且 Bing 地圖服務會自動執行計算以確定裝置是否位於地理柵欄內。</span><span class="sxs-lookup"><span data-stu-id="fc783-147">That way you're specifying a target point that we obtain from the device and Bing Maps will automatically perform the calculations to see whether it is within the geofence.</span></span> <span data-ttu-id="fc783-148">一旦您透過瀏覽器 (或 cURL) 執行要求，您將會收到標準 JSON 回應︰</span><span class="sxs-lookup"><span data-stu-id="fc783-148">Once you execute the request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](./media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="fc783-149">只有當位置點確實位於指定邊界內時，才會出現此回應。</span><span class="sxs-lookup"><span data-stu-id="fc783-149">This response only happens when the point is actually within the designated boundaries.</span></span> <span data-ttu-id="fc783-150">如果不在邊界內，您將會收到空白的 **results** 分類︰</span><span class="sxs-lookup"><span data-stu-id="fc783-150">If it is not, you will get an empty **results** bucket:</span></span>

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-the-uwp-application"></a><span data-ttu-id="fc783-151">設定 UWP 應用程式</span><span class="sxs-lookup"><span data-stu-id="fc783-151">Setting up the UWP application</span></span>
<span data-ttu-id="fc783-152">現在我們已經備妥資料來源，接下來我們可以開始處理稍早啟動的 UWP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc783-152">Now that we have the data source ready, we can start working on the UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="fc783-153">首先，我們必須啟用應用程式的位置服務。</span><span class="sxs-lookup"><span data-stu-id="fc783-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="fc783-154">若要這樣做，請按兩下 [方案總管] 中的 `Package.appxmanifest` 檔案。</span><span class="sxs-lookup"><span data-stu-id="fc783-154">To do this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](./media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="fc783-155">在剛剛開啟的 [套件屬性] 索引標籤中按一下 [功能]，並確實選取 [位置]：</span><span class="sxs-lookup"><span data-stu-id="fc783-155">In the package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](./media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="fc783-156">因為已宣告位置功能，請在方案中建立名為 `Core` 的新資料夾，並在其中新增稱為 `LocationHelper.cs` 的新檔案：</span><span class="sxs-lookup"><span data-stu-id="fc783-156">As the location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](./media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="fc783-157">`LocationHelper` 類別本身在這個階段的用途相當基本，就只是允許我們透過系統 API 取得使用者位置︰</span><span class="sxs-lookup"><span data-stu-id="fc783-157">The `LocationHelper` class itself is fairly basic at this point – all it does is allow us to obtain the user location through the system API:</span></span>

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

<span data-ttu-id="fc783-158">若想深入了解如何在 UWP 應用程式中取得使用者位置，請參閱官方的 [MSDN 文件](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fc783-158">You can read more about getting the user’s location in UWP apps in the official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="fc783-159">若要確認實際上是否能取得位置，請開啟主頁面的程式碼端 (`MainPage.xaml.cs`)。</span><span class="sxs-lookup"><span data-stu-id="fc783-159">To check that the location acquisition is actually working, open the code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="fc783-160">在 `MainPage` 建構函式中為 `Loaded` 事件建立新的事件處理常式︰</span><span class="sxs-lookup"><span data-stu-id="fc783-160">Create a new event handler for the `Loaded` event in the `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="fc783-161">事件處理常式的實作如下︰</span><span class="sxs-lookup"><span data-stu-id="fc783-161">The implementation of the event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="fc783-162">請注意，因為 `GetCurrentLocation` 不必是即時資訊，並因此需要以非同步方式執行，所以我們將處理常式宣告為非同步。</span><span class="sxs-lookup"><span data-stu-id="fc783-162">Notice that we declared the handler as async because `GetCurrentLocation` is awaitable, and therefore requires to be executed in an async context.</span></span> <span data-ttu-id="fc783-163">此外，因為在某些情況下我們可能會得到空值的位置 (例如位置服務已停用或應用程式用來存取位置的權限遭到拒絕)，因此我們需要確定它會透過空值檢查進行適當處理。</span><span class="sxs-lookup"><span data-stu-id="fc783-163">Also, because under certain circumstances we might end up with a null location (e.g. the location services are disabled or the application was denied permissions to access location), we need to make sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="fc783-164">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc783-164">Run the application.</span></span> <span data-ttu-id="fc783-165">請確定您允許其存取位置︰</span><span class="sxs-lookup"><span data-stu-id="fc783-165">Make sure you allow location access:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="fc783-166">一旦應用程式啟動，您應該就能在 [輸出]  視窗中看到座標︰</span><span class="sxs-lookup"><span data-stu-id="fc783-166">Once the application launches, you should be able to see the coordinates in the **Output** window:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="fc783-167">現在您知道能正常取得位置了，接著您可以放心移除用於 Loaded 的測試事件處理常式，因為我們不會再用到它。</span><span class="sxs-lookup"><span data-stu-id="fc783-167">Now you know that location acquisition works – feel free to remove the test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="fc783-168">下一步是擷取位置變更。</span><span class="sxs-lookup"><span data-stu-id="fc783-168">The next step is to capture location changes.</span></span> <span data-ttu-id="fc783-169">為此，讓我們回到 `LocationHelper` 類別，並新增用於 `PositionChanged` 的事件處理常式：</span><span class="sxs-lookup"><span data-stu-id="fc783-169">For that, let’s go back to the `LocationHelper` class and add the event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="fc783-170">實作後將會在 [輸出]  視窗中顯示位置座標︰</span><span class="sxs-lookup"><span data-stu-id="fc783-170">The implementation will show the location coordinates in the **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-the-backend"></a><span data-ttu-id="fc783-171">設定後端</span><span class="sxs-lookup"><span data-stu-id="fc783-171">Setting up the backend</span></span>
<span data-ttu-id="fc783-172">從 GitHub 下載 [.NET 後端範例](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers)。</span><span class="sxs-lookup"><span data-stu-id="fc783-172">Download the [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="fc783-173">下載完成後，依序開啟 `NotifyUsers` 資料夾和 `NotifyUsers.sln` 檔案。</span><span class="sxs-lookup"><span data-stu-id="fc783-173">Once the download completes, open the `NotifyUsers` folder, and subsequently – the `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="fc783-174">將 `AppBackend` 專案設定為 [啟始專案] 並加以啟動。</span><span class="sxs-lookup"><span data-stu-id="fc783-174">Set the `AppBackend` project as the **StartUp Project** and launch it.</span></span>

![](./media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="fc783-175">專案已設定為會將推播通知傳送至目標裝置，所以我們只需要做兩件事：交換出用於通知中樞的正確連接字串，並新增邊界識別以便只在使用者位於地理柵欄內時才傳送通知。</span><span class="sxs-lookup"><span data-stu-id="fc783-175">The project is already configured to send push notifications to target devices, so we’ll need to do only two things – swap out the right connection string for the notification hub and add boundary identification to send the notification only when the user is within the geofence.</span></span>

<span data-ttu-id="fc783-176">若要設定連接字串，請開啟 `Models` 資料夾內的 `Notifications.cs`。</span><span class="sxs-lookup"><span data-stu-id="fc783-176">To configure the connection string, in the `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="fc783-177">`NotificationHubClient.CreateClientFromConnectionString` 函式應該會包含可在 [Azure 入口網站](https://portal.azure.com)內取得之通知中樞的相關資訊 (請查看 [設定] 的 [存取原則] 刀鋒視窗內部)。</span><span class="sxs-lookup"><span data-stu-id="fc783-177">The `NotificationHubClient.CreateClientFromConnectionString` function should contain the information about your notification hub that you can get in the [Azure Portal](https://portal.azure.com) (look inside the **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="fc783-178">儲存經過更新的組態檔。</span><span class="sxs-lookup"><span data-stu-id="fc783-178">Save the updated configuration file.</span></span>

<span data-ttu-id="fc783-179">現在我們需要為 Bing 地圖服務 API 結果建立模型。</span><span class="sxs-lookup"><span data-stu-id="fc783-179">Now we need to create a model for the Bing Maps API result.</span></span> <span data-ttu-id="fc783-180">若要這麼做，最簡單的方式是以滑鼠右鍵按一下 `Models` 資料夾，然後選取 [新增] > [類別]。</span><span class="sxs-lookup"><span data-stu-id="fc783-180">The easiest way to do that is right-click on the `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="fc783-181">將它命名為 `GeofenceBoundary.cs`</span><span class="sxs-lookup"><span data-stu-id="fc783-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="fc783-182">完成後，從我們在第一節所討論的 API 回應複製 JSON，然後在 Visual Studio 中使用 [編輯] > [選擇性貼上] > [貼上 JSON 做為類別]。</span><span class="sxs-lookup"><span data-stu-id="fc783-182">Once done, copy the JSON from the API response that we discussed in the first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="fc783-183">這樣一來，我們就能確保物件將會確實依其設計目的還原序列化。</span><span class="sxs-lookup"><span data-stu-id="fc783-183">That way we ensure that the object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="fc783-184">所產生的類別集應該會與下面類似︰</span><span class="sxs-lookup"><span data-stu-id="fc783-184">Your resulting class set should resemble this:</span></span>

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

<span data-ttu-id="fc783-185">接下來，開啟 `Controllers` > `NotificationsController.cs`。</span><span class="sxs-lookup"><span data-stu-id="fc783-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="fc783-186">我們需要調整 Post 呼叫以說明目標經緯度。</span><span class="sxs-lookup"><span data-stu-id="fc783-186">We need to tweak the Post call to account for the target longitude and latitude.</span></span> <span data-ttu-id="fc783-187">為此，請直接新增下列兩個字串到函式簽章：`latitude` 和 `longitude`。</span><span class="sxs-lookup"><span data-stu-id="fc783-187">For that, simply add two strings to the function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="fc783-188">在稱為 `ApiHelper.cs` 的專案內建立新類別，我們將使用它來連線到 Bing，以確認位置點邊界的交叉點。</span><span class="sxs-lookup"><span data-stu-id="fc783-188">Create a new class within the project called `ApiHelper.cs` – we’ll use it to connect to Bing to check point boundary intersections.</span></span> <span data-ttu-id="fc783-189">實作類似下面的 `IsPointWithinBounds` 函式︰</span><span class="sxs-lookup"><span data-stu-id="fc783-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

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
> <span data-ttu-id="fc783-190">請務必將 API 端點替換為您稍早從 Bing 開發人員中心取得的查詢 URL (API 金鑰也要如此處理)。</span><span class="sxs-lookup"><span data-stu-id="fc783-190">Make sure to substitute the API endpoint with the query URL that you obtained earlier from the Bing Dev Center (same applies to the API key).</span></span> 
> 
> 

<span data-ttu-id="fc783-191">如果查詢後有得到結果，這表示指定位置點位於地理柵欄邊界內，因此我們會傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="fc783-191">If there are results to the query, that means that the specified point is within the boundaries of the geofence, so we return `true`.</span></span> <span data-ttu-id="fc783-192">如果查詢不到任何結果，Bing 就會告訴我們位置點位於查閱框架外部，因此我們會傳回 `false`。</span><span class="sxs-lookup"><span data-stu-id="fc783-192">If there are no results, Bing is telling us that the point is outside the lookup frame, so we return `false`.</span></span>

<span data-ttu-id="fc783-193">回到 `NotificationsController.cs`，在 switch 陳述式前建立檢查︰</span><span class="sxs-lookup"><span data-stu-id="fc783-193">Back in `NotificationsController.cs`, create a check right before the switch statement:</span></span>

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

<span data-ttu-id="fc783-194">這樣一來，就只會在位置點位於邊界內時才傳送通知。</span><span class="sxs-lookup"><span data-stu-id="fc783-194">That way, the notification is only sent when the point is within the boundaries.</span></span>

## <a name="testing-push-notifications-in-the-uwp-app"></a><span data-ttu-id="fc783-195">在 UWP 應用程式中測試推播通知</span><span class="sxs-lookup"><span data-stu-id="fc783-195">Testing push notifications in the UWP app</span></span>
<span data-ttu-id="fc783-196">回到 UWP 應用程式，現在我們應該能夠測試通知了。</span><span class="sxs-lookup"><span data-stu-id="fc783-196">Going back to the UWP app, we should now be able to test notifications.</span></span> <span data-ttu-id="fc783-197">在 `LocationHelper` 類別內建立新函式 `SendLocationToBackend`：</span><span class="sxs-lookup"><span data-stu-id="fc783-197">Within the `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

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
> <span data-ttu-id="fc783-198">將 `POST_URL` 替換為我們在上一節建立的所部署 Web 應用程式的位置。</span><span class="sxs-lookup"><span data-stu-id="fc783-198">Swap the `POST_URL` to the location of your deployed web application that we created in the previous section.</span></span> <span data-ttu-id="fc783-199">現在您可以在本機加以執行，但是由於您要著手部署公用版本，因此您必須使用外部提供者來進行裝載。</span><span class="sxs-lookup"><span data-stu-id="fc783-199">For now, it’s OK to run it locally, but as you work on deploying a public version, you will need to host it with an external provider.</span></span>
> 
> 

<span data-ttu-id="fc783-200">現在，讓我們來確實為 UWP 應用程式註冊推播通知。</span><span class="sxs-lookup"><span data-stu-id="fc783-200">Let’s now make sure that we register the UWP app for push notifications.</span></span> <span data-ttu-id="fc783-201">在 Visual Studio 中，按一下 [專案] > [市集] > [將應用程式與市集建立關聯]。</span><span class="sxs-lookup"><span data-stu-id="fc783-201">In Visual Studio, click on **Project** > **Store** > **Associate app with the store**.</span></span>

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="fc783-202">一旦您登入開發人員帳戶，請務必選取現有應用程式或建立新應用程式並讓封裝與其建立關聯。</span><span class="sxs-lookup"><span data-stu-id="fc783-202">Once you sign in to your developer account, make sure you select an existing app or create a new one and associate the package with it.</span></span> 

<span data-ttu-id="fc783-203">移至開發人員中心，然後開啟您剛剛建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc783-203">Go to the Dev Center and open the app that you just created.</span></span> <span data-ttu-id="fc783-204">按一下 [服務] > [推播通知] > [線上服務網站]。</span><span class="sxs-lookup"><span data-stu-id="fc783-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](./media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="fc783-205">記下網站上的 [應用程式密碼] 和 [套件 SID]。</span><span class="sxs-lookup"><span data-stu-id="fc783-205">On the site, take note of the **Application Secret** and the **Package SID**.</span></span> <span data-ttu-id="fc783-206">在 Azure 入口網站中需要用到這兩個項目；開啟通知中樞、按一下 [設定] > [通知服務] > [Windows (WNS)]，然後在必要欄位中輸入資訊。</span><span class="sxs-lookup"><span data-stu-id="fc783-206">You will need both in the Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter the information in the required fields.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="fc783-207">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="fc783-207">Click on **Save**.</span></span>

<span data-ttu-id="fc783-208">在 [方案總管] 中，以滑鼠右鍵按一下 [參考]，然後選取 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="fc783-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="fc783-209">我們需要新增 **Microsoft Azure 服務匯流排受管理程式庫**的參考；只要搜尋 `WindowsAzure.Messaging.Managed` 並將它新增至專案即可。</span><span class="sxs-lookup"><span data-stu-id="fc783-209">We will need to add a reference to the **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it to your project.</span></span>

![](./media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="fc783-210">為了進行測試，我們可以再次建立 `MainPage_Loaded` 事件處理常式，並對其新增下列程式碼片段︰</span><span class="sxs-lookup"><span data-stu-id="fc783-210">For testing purposes, we can create the `MainPage_Loaded` event handler once again, and add this code snippet to it:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays the registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="fc783-211">上述程式碼使用通知中樞註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc783-211">The above registers the app with the notification hub.</span></span> <span data-ttu-id="fc783-212">現在可以開時進行了！</span><span class="sxs-lookup"><span data-stu-id="fc783-212">You are ready to go!</span></span> 

<span data-ttu-id="fc783-213">在 `LocationHelper` 的 `Geolocator_PositionChanged` 處理常式內，您可以新增一段測試程式碼以強制將位置放在地理柵欄內︰</span><span class="sxs-lookup"><span data-stu-id="fc783-213">In `LocationHelper`, inside the `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put the location inside the geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="fc783-214">因為我們不會傳遞實際座標 (目前可能不在邊界內)，而是使用預先定義的測試值，因此會在更新時看到通知出現︰</span><span class="sxs-lookup"><span data-stu-id="fc783-214">Because we are not passing the real coordinates (which might not be within the boundaries at the moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="fc783-215">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc783-215">What’s next?</span></span>
<span data-ttu-id="fc783-216">除了上述步驟外，您可能還需要遵循幾個步驟以確定方案已可用於生產環境。</span><span class="sxs-lookup"><span data-stu-id="fc783-216">There are a couple of steps that you might need to follow in addition to the above to make sure that the solution is production-ready.</span></span>

<span data-ttu-id="fc783-217">首先，您可能需要確保地理柵欄是動態的。</span><span class="sxs-lookup"><span data-stu-id="fc783-217">First and foremost, you might need to ensure that geofences are dynamic.</span></span> <span data-ttu-id="fc783-218">這需要對 Bing API 進行一些額外處理，才能在現有資料來源內上傳新邊界。</span><span class="sxs-lookup"><span data-stu-id="fc783-218">This will require some extra work with the Bing API in order to be able to upload new boundaries within the existing data source.</span></span> <span data-ttu-id="fc783-219">如需這方面的詳細資訊，請參閱 [Bing 空間資料服務 API 說明文件](https://msdn.microsoft.com/library/ff701734.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="fc783-219">Consult the [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on the subject.</span></span>

<span data-ttu-id="fc783-220">接著，由於您要確保會對正確的參與者進行傳遞，因此您可以透過 [標記](notification-hubs-tags-segment-push-message.md)功能鎖定這些人。</span><span class="sxs-lookup"><span data-stu-id="fc783-220">Second, as you are working to ensure that the delivery is done to the right participants, you might want to target them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="fc783-221">在上述方案所說明的案例中，您可能會有各種不同目標平台，因此我們並未限制只有系統特有功能才能使用地理柵欄。</span><span class="sxs-lookup"><span data-stu-id="fc783-221">The solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit the geofencing to system-specific capabilities.</span></span> <span data-ttu-id="fc783-222">也就是說，通用 Windows 平台內建提供了相關功能來 [偵測地理柵欄](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence)。</span><span class="sxs-lookup"><span data-stu-id="fc783-222">That said, the Universal Windows Platform offers capabilities to [detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="fc783-223">如需有關通知中樞功能的詳細資訊，請查看我們的 [說明文件入口網站](https://azure.microsoft.com/documentation/services/notification-hubs/)。</span><span class="sxs-lookup"><span data-stu-id="fc783-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>

