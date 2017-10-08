---
title: "aaaWindows 通用應用程式 Engagement SDK 整合"
description: "如何 tooIntegrate 與 Windows 通用應用程式的 Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a><span data-ttu-id="f3359-103">Windows 通用 app Engagement SDK 整合</span><span class="sxs-lookup"><span data-stu-id="f3359-103">Windows Universal Apps Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f3359-104">Universal Windows</span><span class="sxs-lookup"><span data-stu-id="f3359-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="f3359-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="f3359-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="f3359-106">iOS</span><span class="sxs-lookup"><span data-stu-id="f3359-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="f3359-107">Android</span><span class="sxs-lookup"><span data-stu-id="f3359-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="f3359-108">此程序描述 hello 最簡單方式 tooactivate Engagement 分析及監視 Windows 通用應用程式中的函式。</span><span class="sxs-lookup"><span data-stu-id="f3359-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Windows Universal application.</span></span>

<span data-ttu-id="f3359-109">hello 步驟所記錄的足夠 tooactivate hello 報表所需 toocompute 關於使用者、 工作階段、 活動、 當機和 Technicals 的所有統計資料。</span><span class="sxs-lookup"><span data-stu-id="f3359-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="f3359-110">hello 報表的記錄檔所需 toocompute 其他統計資料像是事件、 錯誤和作業必須完成手動使用 hello Engagement 應用程式開發介面 (請參閱[toouse hello 如何進階標記 Windows 通用應用程式中的應用程式開發介面的 Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md)因為這些統計資料是應用程式相依。</span><span class="sxs-lookup"><span data-stu-id="f3359-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="f3359-111">支援的版本</span><span class="sxs-lookup"><span data-stu-id="f3359-111">Supported versions</span></span>
<span data-ttu-id="f3359-112">hello Mobile Engagement SDK 的 Windows 通用應用程式只可以整合到 Windows 執行階段和通用 Windows 平台為目標的應用程式：</span><span class="sxs-lookup"><span data-stu-id="f3359-112">hello Mobile Engagement SDK for Windows Universal Apps can only be integrated into Windows Runtime and Universal Windows Platform applications targeting :</span></span>

* <span data-ttu-id="f3359-113">Windows 8</span><span class="sxs-lookup"><span data-stu-id="f3359-113">Windows 8</span></span>
* <span data-ttu-id="f3359-114">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="f3359-114">Windows 8.1</span></span>
* <span data-ttu-id="f3359-115">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="f3359-115">Windows Phone 8.1</span></span>
* <span data-ttu-id="f3359-116">Windows 10 (桌上型電腦和行動裝置系列)</span><span class="sxs-lookup"><span data-stu-id="f3359-116">Windows 10 (desktop and mobile families)</span></span>

> [!NOTE]
> <span data-ttu-id="f3359-117">如果您的目標 Windows Phone Silverlight，則參考 toohello [Windows Phone Silverlight 整合程序](mobile-engagement-windows-phone-integrate-engagement.md)。</span><span class="sxs-lookup"><span data-stu-id="f3359-117">If you are targeting Windows Phone Silverlight then refer toohello [Windows Phone Silverlight integration procedure](mobile-engagement-windows-phone-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a><span data-ttu-id="f3359-118">安裝 hello Mobile Engagement 通用應用程式 SDK</span><span class="sxs-lookup"><span data-stu-id="f3359-118">Install hello Mobile Engagement Universal Apps SDK</span></span>
### <a name="all-platforms"></a><span data-ttu-id="f3359-119">所有平台</span><span class="sxs-lookup"><span data-stu-id="f3359-119">All platforms</span></span>
<span data-ttu-id="f3359-120">hello Mobile Engagement SDK 的 Windows 通用應用程式是以 Nuget 套件使用呼叫*MicrosoftAzure.MobileEngagement*。</span><span class="sxs-lookup"><span data-stu-id="f3359-120">hello Mobile Engagement SDK for Windows Universal App is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="f3359-121">您可以從 hello Visual Studio 的 Nuget 套件管理員來安裝它。</span><span class="sxs-lookup"><span data-stu-id="f3359-121">You can install it from hello Visual Studio Nuget Package Manager.</span></span>

### <a name="windows-8x-and-windows-phone-81"></a><span data-ttu-id="f3359-122">Windows 8.x 和 Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="f3359-122">Windows 8.x and Windows Phone 8.1</span></span>
<span data-ttu-id="f3359-123">NuGet 會自動部署的 hello hello SDK 資源`Resources`根目錄 hello 應用程式專案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f3359-123">NuGet automatically deploys hello SDK resources in hello `Resources` folder at hello root of your application project.</span></span>

### <a name="windows-10-universal-windows-platform-applications"></a><span data-ttu-id="f3359-124">Windows 10 通用 Windows 平台應用程式</span><span class="sxs-lookup"><span data-stu-id="f3359-124">Windows 10 Universal Windows Platform applications</span></span>
<span data-ttu-id="f3359-125">NuGet 不會自動部署在 UWP 應用程式尚未 hello SDK 資源。</span><span class="sxs-lookup"><span data-stu-id="f3359-125">NuGet does not automatically deploy hello SDK resources in your UWP application yet.</span></span> <span data-ttu-id="f3359-126">您必須手動直到資源部署前它會重新引入 NuGet 中 toodo:</span><span class="sxs-lookup"><span data-stu-id="f3359-126">You have toodo it manually until resources deployment is reintroduced in NuGet:</span></span>

1. <span data-ttu-id="f3359-127">開啟 [檔案總管]。</span><span class="sxs-lookup"><span data-stu-id="f3359-127">Open your File Explorer.</span></span>
2. <span data-ttu-id="f3359-128">瀏覽下列位置的 toohello (**x.x.x**是您要安裝的 Engagement hello 版本): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x.x**\\content\win81*</span><span class="sxs-lookup"><span data-stu-id="f3359-128">Navigate toohello following location (**x.x.x** is hello version of Engagement you are installing): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span></span>
3. <span data-ttu-id="f3359-129">拖放 hello**資源**從您的專案，Visual Studio 中的 hello 檔案總管 toohello 根資料夾。</span><span class="sxs-lookup"><span data-stu-id="f3359-129">Drag and drop hello **Resources** folder from hello file explorer toohello root of your project in Visual Studio.</span></span>
4. <span data-ttu-id="f3359-130">在 Visual Studio 中選取專案，並啟動 hello**顯示所有檔案**圖示上方 hello**方案總管 中**。</span><span class="sxs-lookup"><span data-stu-id="f3359-130">In Visual Studio select your project and activate hello **Show All files** icon on top of hello **Solution Explorer**.</span></span>
5. <span data-ttu-id="f3359-131">有些檔案未被納入 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="f3359-131">Some files are not included in hello project.</span></span> <span data-ttu-id="f3359-132">它們一次以滑鼠右鍵按一下 hello tooimport**資源**資料夾，**從專案中排除**另一個 hello 上按一下滑鼠右鍵，然後**資源**資料夾， **Include在專案中**toore-包括 hello 整個資料夾。</span><span class="sxs-lookup"><span data-stu-id="f3359-132">tooimport them at once right click on hello **Resources** folder, **Exclude from project** then another right click on hello **Resources** folder, **Include in project** toore-include hello whole folder.</span></span> <span data-ttu-id="f3359-133">所有檔案從 hello**資源**資料夾現在會包含在專案中。</span><span class="sxs-lookup"><span data-stu-id="f3359-133">All files from hello **Resources** folder are now included in your project.</span></span>

## <a name="add-hello-capabilities"></a><span data-ttu-id="f3359-134">加入 hello 功能</span><span class="sxs-lookup"><span data-stu-id="f3359-134">Add hello capabilities</span></span>
<span data-ttu-id="f3359-135">hello Engagement SDK 正確必須在順序 toowork hello Windows SDK 的一些功能。</span><span class="sxs-lookup"><span data-stu-id="f3359-135">hello Engagement SDK needs some capabilities of hello Windows SDK in order toowork properly.</span></span>

<span data-ttu-id="f3359-136">開啟您`Package.appxmanifest`檔案，並確定宣告該 hello 下列功能：</span><span class="sxs-lookup"><span data-stu-id="f3359-136">Open your `Package.appxmanifest` file and be sure that hello following capabilities are declared:</span></span>

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="f3359-137">初始化 hello Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="f3359-137">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="f3359-138">Engagement 組態</span><span class="sxs-lookup"><span data-stu-id="f3359-138">Engagement configuration</span></span>
<span data-ttu-id="f3359-139">hello Engagement 組態會集中在 hello`Resources\EngagementConfiguration.xml`專案檔。</span><span class="sxs-lookup"><span data-stu-id="f3359-139">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="f3359-140">編輯此檔案 toospecify:</span><span class="sxs-lookup"><span data-stu-id="f3359-140">Edit this file toospecify:</span></span>

* <span data-ttu-id="f3359-141">應用程式在 `<connectionString>` 和 `<\connectionString>` 標記之間的連接字串。</span><span class="sxs-lookup"><span data-stu-id="f3359-141">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="f3359-142">如果您想要在執行階段相反地，您可以呼叫 hello 下列 toospecify hello Engagement 代理程式初始化之前的方法：</span><span class="sxs-lookup"><span data-stu-id="f3359-142">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

<span data-ttu-id="f3359-143">您的應用程式的 hello 連接字串會顯示在 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="f3359-143">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="f3359-144">Engagement 初始化</span><span class="sxs-lookup"><span data-stu-id="f3359-144">Engagement initialization</span></span>
<span data-ttu-id="f3359-145">當您建立新專案時會產生一份 `App.xaml.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="f3359-145">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="f3359-146">這個類別繼承自 `Application` ，且包含的許多重要的方法。</span><span class="sxs-lookup"><span data-stu-id="f3359-146">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="f3359-147">它也會使用的 tooinitialize hello Engagement SDK。</span><span class="sxs-lookup"><span data-stu-id="f3359-147">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="f3359-148">修改 hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="f3359-148">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="f3359-149">新增 tooyour`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="f3359-149">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="f3359-150">定義一次的所有呼叫的方法 tooshare hello Engagement 初始化：</span><span class="sxs-lookup"><span data-stu-id="f3359-150">Define a method tooshare hello Engagement initialization once for all calls:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* <span data-ttu-id="f3359-151">呼叫`InitEngagement`在 hello`OnLaunched`方法：</span><span class="sxs-lookup"><span data-stu-id="f3359-151">Call `InitEngagement` in hello `OnLaunched` method:</span></span>
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* <span data-ttu-id="f3359-152">另一個應用程式或 hello 命令列啟動您的應用程式時使用自訂配置，然後 hello`OnActivated`方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="f3359-152">When your application is launched using a custom scheme, another application or hello command line then hello `OnActivated` method is called.</span></span> <span data-ttu-id="f3359-153">您的應用程式啟動時，也需要 tooinitiate hello Engagement SDK。</span><span class="sxs-lookup"><span data-stu-id="f3359-153">You also need tooinitiate hello Engagement SDK when your app is activated.</span></span> <span data-ttu-id="f3359-154">因此，覆寫 toodo`OnActivated`方法：</span><span class="sxs-lookup"><span data-stu-id="f3359-154">toodo so, override `OnActivated` method:</span></span>
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> <span data-ttu-id="f3359-155">我們強烈建議您 tooadd hello Engagement 初始化應用程式的另一個位置中。</span><span class="sxs-lookup"><span data-stu-id="f3359-155">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="f3359-156">基本報告</span><span class="sxs-lookup"><span data-stu-id="f3359-156">Basic reporting</span></span>
### <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="f3359-157">建議使用的方法：多載您的 `Page` 類別</span><span class="sxs-lookup"><span data-stu-id="f3359-157">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="f3359-158">訂單 tooactivate hello Engagement toocompute 使用者、 工作階段、 活動、 當機和技術的統計資料所需的所有 hello 記錄檔的報表，您可以只在所有您`Page`子類別是繼承自 hello`EngagementPage`類別。</span><span class="sxs-lookup"><span data-stu-id="f3359-158">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="f3359-159">以下是如何的範例 toodo 這樣的應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="f3359-159">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="f3359-160">您可以 hello 相同的動作，為您的應用程式的所有頁面。</span><span class="sxs-lookup"><span data-stu-id="f3359-160">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="f3359-161">C# 來源檔案</span><span class="sxs-lookup"><span data-stu-id="f3359-161">C# Source file</span></span>
<span data-ttu-id="f3359-162">修改您頁面的 `.xaml.cs` 檔案：</span><span class="sxs-lookup"><span data-stu-id="f3359-162">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="f3359-163">新增 tooyour`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="f3359-163">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="f3359-164">以 `EngagementPage` 取代 `Page`：</span><span class="sxs-lookup"><span data-stu-id="f3359-164">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="f3359-165">**沒有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="f3359-165">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="f3359-166">**有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="f3359-166">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="f3359-167">如果您的頁面會覆寫 hello`OnNavigatedTo`方法，是確定 toocall `base.OnNavigatedTo(e)`。</span><span class="sxs-lookup"><span data-stu-id="f3359-167">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="f3359-168">否則，不會回報 hello 活動 (hello`EngagementPage`呼叫`StartActivity`內其`OnNavigatedTo`方法)。</span><span class="sxs-lookup"><span data-stu-id="f3359-168">Otherwise,  hello activity will not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="f3359-169">XAML 檔案</span><span class="sxs-lookup"><span data-stu-id="f3359-169">XAML file</span></span>
<span data-ttu-id="f3359-170">修改您頁面的 `.xaml` 檔案：</span><span class="sxs-lookup"><span data-stu-id="f3359-170">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="f3359-171">加入 tooyour 命名空間宣告：</span><span class="sxs-lookup"><span data-stu-id="f3359-171">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="f3359-172">以 `engagement:EngagementPage` 取代 `Page`：</span><span class="sxs-lookup"><span data-stu-id="f3359-172">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="f3359-173">**沒有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="f3359-173">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="f3359-174">**有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="f3359-174">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a><span data-ttu-id="f3359-175">覆寫預設行為，hello</span><span class="sxs-lookup"><span data-stu-id="f3359-175">Override hello default behaviour</span></span>
<span data-ttu-id="f3359-176">根據預設，hello 活動名稱，以及不需額外會報告 hello 頁面 hello 類別名稱。</span><span class="sxs-lookup"><span data-stu-id="f3359-176">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="f3359-177">如果 hello 類別使用 hello"Page"後置詞，Engagement 也會移除它。</span><span class="sxs-lookup"><span data-stu-id="f3359-177">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="f3359-178">如果您想要 hello 名稱 toooverride hello 預設行為，只要加入此 tooyour 程式碼：</span><span class="sxs-lookup"><span data-stu-id="f3359-178">If you want toooverride hello default behaviour for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="f3359-179">如果您想要 tooreport 某些額外的資訊與您的活動，您可以加入這個 tooyour 程式碼：</span><span class="sxs-lookup"><span data-stu-id="f3359-179">If you want tooreport some extra informations with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="f3359-180">這些方法從呼叫 hello 內`OnNavigatedTo`頁面的方法。</span><span class="sxs-lookup"><span data-stu-id="f3359-180">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="f3359-181">替代方法：手動呼叫 `StartActivity()`</span><span class="sxs-lookup"><span data-stu-id="f3359-181">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="f3359-182">如果您無法或不想 toooverload 您`Page`類別，您可以改為啟動您的活動藉由呼叫`EngagementAgent`直接的方法。</span><span class="sxs-lookup"><span data-stu-id="f3359-182">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="f3359-183">我們建議 toocall`StartActivity`內您`OnNavigatedTo`頁面的方法。</span><span class="sxs-lookup"><span data-stu-id="f3359-183">We recommend toocall `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="f3359-184">請確定您正確地結束工作階段。</span><span class="sxs-lookup"><span data-stu-id="f3359-184">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="f3359-185">hello Windows 通用 SDK 會自動呼叫 hello `EndActivity` hello 應用程式關閉時的方法。</span><span class="sxs-lookup"><span data-stu-id="f3359-185">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="f3359-186">因此，它是**高**建議 toocall hello`StartActivity`每當 hello 使用者的 hello 活動變更時，方法和太**永不**呼叫 hello`EndActivity`方法，這個方法會傳送 tooEngagement伺服器目前的使用者具有保留 hello 應用程式，這將會影響所有的應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f3359-186">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method, this method sends tooEngagement server that current user has leave hello application, this will impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="f3359-187">進階報告</span><span class="sxs-lookup"><span data-stu-id="f3359-187">Advanced reporting</span></span>
<span data-ttu-id="f3359-188">（選擇性） 您可能會想 tooreport 應用程式特定事件、 錯誤和作業、 toodo 因此、 使用 hello 其他方法位於 hello`EngagementAgent`類別。</span><span class="sxs-lookup"><span data-stu-id="f3359-188">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="f3359-189">hello Engagement 應用程式開發介面可讓 toouse 所有參與的進階功能。</span><span class="sxs-lookup"><span data-stu-id="f3359-189">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="f3359-190">如需詳細資訊，請參閱[toouse hello 如何進階標記 Windows 通用應用程式中的應用程式開發介面的 Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md)。</span><span class="sxs-lookup"><span data-stu-id="f3359-190">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="f3359-191">進階組態</span><span class="sxs-lookup"><span data-stu-id="f3359-191">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="f3359-192">停用自動當機報告</span><span class="sxs-lookup"><span data-stu-id="f3359-192">Disable automatic crash reporting</span></span>
<span data-ttu-id="f3359-193">您可以停用報告功能的 Engagement hello 自動損毀。</span><span class="sxs-lookup"><span data-stu-id="f3359-193">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="f3359-194">然後，發生未處理的例外狀況時，Engagement 將不會執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="f3359-194">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="f3359-195">如果您計劃 toodisable 這項功能，請注意，當應用程式中，將會發生未處理的損毀，Engagement 不會傳送 hello 損毀**AND** hello 工作階段和工作將不會關閉。</span><span class="sxs-lookup"><span data-stu-id="f3359-195">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="f3359-196">toodisable 自動當機報告，也可以自訂您的組態，根據您在宣告的 hello 方式而定：</span><span class="sxs-lookup"><span data-stu-id="f3359-196">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="f3359-197">從 `EngagementConfiguration.xml` 檔案</span><span class="sxs-lookup"><span data-stu-id="f3359-197">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="f3359-198">設定報表損毀太`false`之間`<reportCrash>`和`</reportCrash>`標記。</span><span class="sxs-lookup"><span data-stu-id="f3359-198">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="f3359-199">於執行階段時從 `EngagementConfiguration` 物件</span><span class="sxs-lookup"><span data-stu-id="f3359-199">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="f3359-200">設定報表損毀 toofalse 使用 EngagementConfiguration 物件。</span><span class="sxs-lookup"><span data-stu-id="f3359-200">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="f3359-201">高載模式</span><span class="sxs-lookup"><span data-stu-id="f3359-201">Burst mode</span></span>
<span data-ttu-id="f3359-202">根據預設，hello Engagement 服務報表會即時記錄。</span><span class="sxs-lookup"><span data-stu-id="f3359-202">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="f3359-203">如果您的應用程式會報告記錄檔頻率很高，是較佳的 toobuffer hello 記錄檔和 tooreport 一次在固定時間基底 （稱為 hello 「 高載模式 」）。</span><span class="sxs-lookup"><span data-stu-id="f3359-203">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="f3359-204">toodo 因此，呼叫 hello 方法：</span><span class="sxs-lookup"><span data-stu-id="f3359-204">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="f3359-205">hello 引數是中的值**毫秒**。</span><span class="sxs-lookup"><span data-stu-id="f3359-205">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="f3359-206">在任何時間，如果您想 tooreactivate hello 即時記錄，就會呼叫 hello 方法未使用任何參數，或使用 hello 0 值。</span><span class="sxs-lookup"><span data-stu-id="f3359-206">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="f3359-207">hello 高載模式稍微增加 hello 電池壽命但有 hello Engagement 監視影響： 所有工作階段和作業的持續時間將會捨入的 toohello 高載臨界值 （因此，工作階段和短 hello 高載閾值可能不會顯示作業）。</span><span class="sxs-lookup"><span data-stu-id="f3359-207">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="f3359-208">它會建議 toouse 高載臨界值不會再於 30000 （30 秒）。</span><span class="sxs-lookup"><span data-stu-id="f3359-208">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="f3359-209">您有 toobe 感知儲存記錄檔是有限的 too300 項目。</span><span class="sxs-lookup"><span data-stu-id="f3359-209">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="f3359-210">如果傳送太長，您可能會遺失某些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f3359-210">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="f3359-211">hello 高載臨界值不能設定 tooa 期間小於 1。</span><span class="sxs-lookup"><span data-stu-id="f3359-211">hello burst threshold cannot be configured tooa period lesser than 1s.</span></span> <span data-ttu-id="f3359-212">如果您因此嘗試 toodo，hello SDK 將會顯示追蹤與 hello 錯誤，就會自動重設 toohello 預設值，也就是 0。</span><span class="sxs-lookup"><span data-stu-id="f3359-212">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, i.e., 0s.</span></span> <span data-ttu-id="f3359-213">這將會觸發即時 hello SDK tooreport hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="f3359-213">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

