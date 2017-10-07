---
title: "aaaWindows Phone Silverlight Engagement SDK 整合"
description: "如何使用 Windows Phone Silverlight 應用程式的 Azure Mobile Engagement tooIntegrate"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="a1f08-103">Windows Phone Silverlight Engagement SDK 整合</span><span class="sxs-lookup"><span data-stu-id="a1f08-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a1f08-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="a1f08-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="a1f08-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="a1f08-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="a1f08-106">iOS</span><span class="sxs-lookup"><span data-stu-id="a1f08-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="a1f08-107">Android</span><span class="sxs-lookup"><span data-stu-id="a1f08-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="a1f08-108">此程序描述 hello 最簡單方式 tooactivate Azure Mobile Engagement 的分析和監視您的 Windows Phone Silverlight 應用程式中的函式。</span><span class="sxs-lookup"><span data-stu-id="a1f08-108">This procedure describes hello simplest way tooactivate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="a1f08-109">hello 步驟所記錄的足夠 tooactivate hello 報表所需 toocompute 關於使用者、 工作階段、 活動、 當機和 Technicals 的所有統計資料。</span><span class="sxs-lookup"><span data-stu-id="a1f08-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="a1f08-110">hello 報表的記錄檔所需 toocompute 其他統計資料像是事件、 錯誤和作業必須完成手動使用 hello Engagement 應用程式開發介面 (請參閱[toouse hello 如何進階標記您的 Windows Phone Silverlight 應用程式中的應用程式開發介面的 Mobile Engagement](mobile-engagement-windows-phone-use-engagement-api.md)下面） 因為這些統計資料是應用程式相依。</span><span class="sxs-lookup"><span data-stu-id="a1f08-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="a1f08-111">支援的版本</span><span class="sxs-lookup"><span data-stu-id="a1f08-111">Supported versions</span></span>
<span data-ttu-id="a1f08-112">hello Mobile Engagement SDK for Windows Silverlight 只可以整合到應用程式為目標：</span><span class="sxs-lookup"><span data-stu-id="a1f08-112">hello Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="a1f08-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="a1f08-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="a1f08-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="a1f08-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="a1f08-115">如果您的目標 Windows Phone 8.1 (非 Silverlight)，請參閱 toohello [Windows 通用整合程序](mobile-engagement-windows-store-integrate-engagement.md)。</span><span class="sxs-lookup"><span data-stu-id="a1f08-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer toohello [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="a1f08-116">安裝 hello Mobile Engagement Silverlight SDK</span><span class="sxs-lookup"><span data-stu-id="a1f08-116">Install hello Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="a1f08-117">hello Mobile Engagement SDK for Windows Silverlight 是以 Nuget 套件使用呼叫*MicrosoftAzure.MobileEngagement*。</span><span class="sxs-lookup"><span data-stu-id="a1f08-117">hello Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="a1f08-118">您可以從 hello Visual Studio 的 Nuget 套件管理員來安裝它。</span><span class="sxs-lookup"><span data-stu-id="a1f08-118">You can install it from hello Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="a1f08-119">加入 hello 功能</span><span class="sxs-lookup"><span data-stu-id="a1f08-119">Add hello capabilities</span></span>
<span data-ttu-id="a1f08-120">hello Engagement SDK 正確需要 hello Windows Phone Silverlight SDK toowork 順序中的某些功能。</span><span class="sxs-lookup"><span data-stu-id="a1f08-120">hello Engagement SDK needs some capabilities of hello Windows Phone Silverlight SDK in order toowork properly.</span></span>

<span data-ttu-id="a1f08-121">開啟您`WMAppManifest.xml`檔案，並確定在 hello 中宣告的下列功能的 hello`Capabilities`面板：</span><span class="sxs-lookup"><span data-stu-id="a1f08-121">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared in hello `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="a1f08-122">初始化 hello Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="a1f08-122">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="a1f08-123">Engagement 組態</span><span class="sxs-lookup"><span data-stu-id="a1f08-123">Engagement configuration</span></span>
<span data-ttu-id="a1f08-124">hello Engagement 組態會集中在 hello`Resources\EngagementConfiguration.xml`專案檔。</span><span class="sxs-lookup"><span data-stu-id="a1f08-124">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="a1f08-125">編輯此檔案 toospecify:</span><span class="sxs-lookup"><span data-stu-id="a1f08-125">Edit this file toospecify :</span></span>

* <span data-ttu-id="a1f08-126">應用程式在 `<connectionString>` 和 `<\connectionString>` 標記之間的連接字串。</span><span class="sxs-lookup"><span data-stu-id="a1f08-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="a1f08-127">如果您想要在執行階段相反地，您可以呼叫 hello 下列 toospecify hello Engagement 代理程式初始化之前的方法：</span><span class="sxs-lookup"><span data-stu-id="a1f08-127">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="a1f08-128">您的應用程式的 hello 連接字串會顯示在 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="a1f08-128">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="a1f08-129">Engagement 初始化</span><span class="sxs-lookup"><span data-stu-id="a1f08-129">Engagement initialization</span></span>
<span data-ttu-id="a1f08-130">當您建立新專案時會產生一份 `App.xaml.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="a1f08-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="a1f08-131">這個類別繼承自 `Application` ，且包含的許多重要的方法。</span><span class="sxs-lookup"><span data-stu-id="a1f08-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="a1f08-132">它也會使用的 tooinitialize hello Engagement SDK。</span><span class="sxs-lookup"><span data-stu-id="a1f08-132">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="a1f08-133">修改 hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="a1f08-133">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="a1f08-134">新增 tooyour`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="a1f08-134">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="a1f08-135">插入`EngagementAgent.Instance.Init`在 hello`Application_Launching`方法：</span><span class="sxs-lookup"><span data-stu-id="a1f08-135">Insert `EngagementAgent.Instance.Init` in hello `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="a1f08-136">插入`EngagementAgent.Instance.OnActivated`在 hello`Application_Activated`方法：</span><span class="sxs-lookup"><span data-stu-id="a1f08-136">Insert `EngagementAgent.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="a1f08-137">我們強烈建議您 tooadd hello Engagement 初始化應用程式的另一個位置中。</span><span class="sxs-lookup"><span data-stu-id="a1f08-137">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span> <span data-ttu-id="a1f08-138">不過，請注意該 hello`EngagementAgent.Instance.Init`專用的執行緒，而不是在 hello UI 執行緒執行方法。</span><span class="sxs-lookup"><span data-stu-id="a1f08-138">However, be aware that hello `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on hello UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="a1f08-139">基本報告</span><span class="sxs-lookup"><span data-stu-id="a1f08-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="a1f08-140">建議使用的方法：多載您的 `PhoneApplicationPage` 類別</span><span class="sxs-lookup"><span data-stu-id="a1f08-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="a1f08-141">訂單 tooactivate hello Engagement toocompute 使用者、 工作階段、 活動、 當機和技術的統計資料所需的所有 hello 記錄檔的報表，您可以只在所有您`PhoneApplicationPage`子類別是繼承自 hello`EngagementPage`類別。</span><span class="sxs-lookup"><span data-stu-id="a1f08-141">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="a1f08-142">以下是如何的範例 toodo 這樣的應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="a1f08-142">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="a1f08-143">您可以 hello 相同的動作，為您的應用程式的所有頁面。</span><span class="sxs-lookup"><span data-stu-id="a1f08-143">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="a1f08-144">C# 來源檔案</span><span class="sxs-lookup"><span data-stu-id="a1f08-144">C# Source file</span></span>
<span data-ttu-id="a1f08-145">修改您的頁面 `.xaml.cs` 檔案：</span><span class="sxs-lookup"><span data-stu-id="a1f08-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="a1f08-146">新增 tooyour`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="a1f08-146">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="a1f08-147">以 `EngagementPage` 取代 `PhoneApplicationPage`：</span><span class="sxs-lookup"><span data-stu-id="a1f08-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="a1f08-148">**沒有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="a1f08-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="a1f08-149">**有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="a1f08-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="a1f08-150">如果您的頁面是繼承自 hello`OnNavigatedTo`方法，要特別小心 toolet hello`base.OnNavigatedTo(e)`呼叫。</span><span class="sxs-lookup"><span data-stu-id="a1f08-150">If your page inherits from hello `OnNavigatedTo` method, be careful toolet hello `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="a1f08-151">否則，將不會報告 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="a1f08-151">Otherwise, hello activity will not be reported.</span></span> <span data-ttu-id="a1f08-152">事實上，hello`EngagementPage`呼叫`StartActivity`內 hello`OnNavigatedTo`方法。</span><span class="sxs-lookup"><span data-stu-id="a1f08-152">Indeed, hello `EngagementPage` is calling `StartActivity` inside hello `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="a1f08-153">XAML 檔案</span><span class="sxs-lookup"><span data-stu-id="a1f08-153">XAML file</span></span>
<span data-ttu-id="a1f08-154">修改您的頁面 `.xaml` 檔案：</span><span class="sxs-lookup"><span data-stu-id="a1f08-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="a1f08-155">加入 tooyour 命名空間宣告：</span><span class="sxs-lookup"><span data-stu-id="a1f08-155">Add tooyour namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="a1f08-156">以 `engagement:EngagementPage` 取代 `phone:PhoneApplicationPage`：</span><span class="sxs-lookup"><span data-stu-id="a1f08-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="a1f08-157">**沒有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="a1f08-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="a1f08-158">**有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="a1f08-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a><span data-ttu-id="a1f08-159">覆寫 hello 預設行為</span><span class="sxs-lookup"><span data-stu-id="a1f08-159">Override hello default behavior</span></span>
<span data-ttu-id="a1f08-160">根據預設，hello 活動名稱，以及不需額外會報告 hello 頁面 hello 類別名稱。</span><span class="sxs-lookup"><span data-stu-id="a1f08-160">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="a1f08-161">如果 hello 類別使用 hello"Page"後置詞，Engagement 也會移除它。</span><span class="sxs-lookup"><span data-stu-id="a1f08-161">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="a1f08-162">如果您想要 hello 名稱 toooverride hello 預設行為，只要加入此 tooyour 程式碼：</span><span class="sxs-lookup"><span data-stu-id="a1f08-162">If you want toooverride hello default behavior for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="a1f08-163">如果您想要 tooreport 一些額外的資訊與您的活動，您可以加入這個 tooyour 程式碼：</span><span class="sxs-lookup"><span data-stu-id="a1f08-163">If you want tooreport some extra information with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="a1f08-164">這些方法從呼叫 hello 內`OnNavigatedTo`頁面的方法。</span><span class="sxs-lookup"><span data-stu-id="a1f08-164">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="a1f08-165">替代方法：手動呼叫 `StartActivity()`</span><span class="sxs-lookup"><span data-stu-id="a1f08-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="a1f08-166">如果您無法或不想 toooverload 您`PhoneApplicationPage`類別，您可以改為啟動您的活動藉由呼叫`EngagementAgent`直接的方法。</span><span class="sxs-lookup"><span data-stu-id="a1f08-166">If you cannot or do not want toooverload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="a1f08-167">我們建議您於 PhoneApplicationPage 的 `OnNavigatedTo` 方法內呼叫 `StartActivity`。</span><span class="sxs-lookup"><span data-stu-id="a1f08-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="a1f08-168">請確定您正確地結束工作階段。</span><span class="sxs-lookup"><span data-stu-id="a1f08-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="a1f08-169">hello SDK 會自動呼叫 hello `EndActivity` hello 應用程式關閉時的方法。</span><span class="sxs-lookup"><span data-stu-id="a1f08-169">hello SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="a1f08-170">因此，它是**高**建議 toocall hello`StartActivity`每當 hello 使用者的 hello 活動變更時，方法和太**永不**呼叫 hello`EndActivity`方法。</span><span class="sxs-lookup"><span data-stu-id="a1f08-170">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="a1f08-171">這個方法會傳送訊息 toohello Engagement 伺服器 hello 目前使用者離開 hello 應用程式，且這會影響所有的應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a1f08-171">This method sends a message toohello Engagement server that hello current user has left hello application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="a1f08-172">進階報告</span><span class="sxs-lookup"><span data-stu-id="a1f08-172">Advanced reporting</span></span>
<span data-ttu-id="a1f08-173">（選擇性） 您可能會想 tooreport 應用程式特定事件、 錯誤和作業、 toodo 因此、 使用 hello 其他方法位於 hello`EngagementAgent`類別。</span><span class="sxs-lookup"><span data-stu-id="a1f08-173">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="a1f08-174">hello Engagement 應用程式開發介面可讓 toouse 所有參與的進階功能。</span><span class="sxs-lookup"><span data-stu-id="a1f08-174">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="a1f08-175">如需詳細資訊，請參閱[toouse hello 如何進階標記您的 Windows Phone Silverlight 應用程式中的應用程式開發介面的 Mobile Engagement](mobile-engagement-windows-phone-use-engagement-api.md)。</span><span class="sxs-lookup"><span data-stu-id="a1f08-175">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="a1f08-176">進階組態</span><span class="sxs-lookup"><span data-stu-id="a1f08-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="a1f08-177">停用自動當機報告</span><span class="sxs-lookup"><span data-stu-id="a1f08-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="a1f08-178">您可以停用報告功能的 Engagement hello 自動損毀。</span><span class="sxs-lookup"><span data-stu-id="a1f08-178">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="a1f08-179">然後，發生未處理的例外狀況時，Engagement 將不會執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="a1f08-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="a1f08-180">如果您計劃 toodisable 這項功能，請注意，當應用程式中，將會發生未處理的損毀，Engagement 不會傳送 hello 損毀**AND** hello 工作階段和工作，就不會關閉它。</span><span class="sxs-lookup"><span data-stu-id="a1f08-180">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** it will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="a1f08-181">toodisable 自動當機報告，也可以自訂您的組態，根據您在宣告的 hello 方式而定：</span><span class="sxs-lookup"><span data-stu-id="a1f08-181">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="a1f08-182">從 `EngagementConfiguration.xml` 檔案</span><span class="sxs-lookup"><span data-stu-id="a1f08-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="a1f08-183">設定報表損毀太`false`之間`<reportCrash>`和`</reportCrash>`標記。</span><span class="sxs-lookup"><span data-stu-id="a1f08-183">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="a1f08-184">於執行階段時從 `EngagementConfiguration` 物件</span><span class="sxs-lookup"><span data-stu-id="a1f08-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="a1f08-185">設定報表損毀 toofalse 使用 EngagementConfiguration 物件。</span><span class="sxs-lookup"><span data-stu-id="a1f08-185">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="a1f08-186">高載模式</span><span class="sxs-lookup"><span data-stu-id="a1f08-186">Burst mode</span></span>
<span data-ttu-id="a1f08-187">根據預設，hello Engagement 服務報表會即時記錄。</span><span class="sxs-lookup"><span data-stu-id="a1f08-187">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="a1f08-188">如果您的應用程式會報告記錄檔頻率很高，是較佳的 toobuffer hello 記錄檔和 tooreport 一次在固定時間基底 （稱為 hello 「 高載模式 」）。</span><span class="sxs-lookup"><span data-stu-id="a1f08-188">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="a1f08-189">toodo 因此，呼叫 hello 方法：</span><span class="sxs-lookup"><span data-stu-id="a1f08-189">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="a1f08-190">hello 引數是中的值**毫秒**。</span><span class="sxs-lookup"><span data-stu-id="a1f08-190">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="a1f08-191">在任何時間，如果您想 tooreactivate hello 即時記錄，就會呼叫 hello 方法未使用任何參數，或使用 hello 0 值。</span><span class="sxs-lookup"><span data-stu-id="a1f08-191">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="a1f08-192">hello 高載模式稍微增加 hello 電池壽命但有 hello Engagement 監視影響： 所有工作階段和作業的持續時間將會捨入的 toohello 高載臨界值 （因此，工作階段和短 hello 高載閾值可能不會顯示作業）。</span><span class="sxs-lookup"><span data-stu-id="a1f08-192">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="a1f08-193">它會建議 toouse 高載臨界值不會再於 30000 （30 秒）。</span><span class="sxs-lookup"><span data-stu-id="a1f08-193">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="a1f08-194">您有 toobe 感知儲存記錄檔是有限的 too300 項目。</span><span class="sxs-lookup"><span data-stu-id="a1f08-194">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="a1f08-195">如果傳送太長，您可能會遺失某些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a1f08-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="a1f08-196">hello 高載臨界值不能設定較小者 tooa 期間比一秒。</span><span class="sxs-lookup"><span data-stu-id="a1f08-196">hello burst threshold cannot be configured tooa period lesser than one second.</span></span> <span data-ttu-id="a1f08-197">如果您因此嘗試 toodo，hello SDK 將會顯示追蹤與 hello 錯誤，就會自動重設 toohello 預設值，也就是零秒。</span><span class="sxs-lookup"><span data-stu-id="a1f08-197">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, that is, zero seconds.</span></span> <span data-ttu-id="a1f08-198">這將會觸發即時 hello SDK tooreport hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="a1f08-198">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

