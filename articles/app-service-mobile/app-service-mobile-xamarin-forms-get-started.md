---
title: "開始使用行動應用程式，使用 Xamarin.Forms aaaGet"
description: "請遵循此教學課程 toostart 使用 Xamarin.Forms 開發的行動應用程式"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a><span data-ttu-id="fa55f-103">建立 Xamarin.Forms 應用程式</span><span class="sxs-lookup"><span data-stu-id="fa55f-103">Create a Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="fa55f-104">概觀</span><span class="sxs-lookup"><span data-stu-id="fa55f-104">Overview</span></span>
<span data-ttu-id="fa55f-105">本教學課程會示範如何 tooadd 雲端後端服務 tooa Xamarin.Forms 行動應用程式使用 hello 做為 hello 後端的 Azure App Service 行動應用程式功能。</span><span class="sxs-lookup"><span data-stu-id="fa55f-105">This tutorial shows you how tooadd a cloud-based back-end service tooa Xamarin.Forms mobile app by using hello Mobile Apps feature of Azure App Service as hello back end.</span></span> <span data-ttu-id="fa55f-106">您會同時建立新的 Mobile Apps 後端，以及可在 Azure 中儲存應用程式資料的簡易待辦事項清單 Xamarin.Forms 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa55f-106">You create both a new Mobile Apps back end and a simple to-do list Xamarin.Forms app that stores app data in Azure.</span></span>

<span data-ttu-id="fa55f-107">完成本教學課程是所有其他 Xamarin.Forms 應用程式的行動應用程式教學課程的必要條件。</span><span class="sxs-lookup"><span data-stu-id="fa55f-107">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Forms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa55f-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="fa55f-108">Prerequisites</span></span>
<span data-ttu-id="fa55f-109">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="fa55f-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="fa55f-110">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa55f-110">An active Azure account.</span></span> <span data-ttu-id="fa55f-111">如果您沒有帳戶，您可以註冊 Azure 的試用版，並取得向上 too10 可用的行動應用程式，即使您在試用結束後，仍可以繼續使用。</span><span class="sxs-lookup"><span data-stu-id="fa55f-111">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="fa55f-112">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="fa55f-112">For more information, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="fa55f-113">Visual Studio 和 Xamarin。</span><span class="sxs-lookup"><span data-stu-id="fa55f-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="fa55f-114">如需資訊，請參閱 hello[設定及安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx)頁面。</span><span class="sxs-lookup"><span data-stu-id="fa55f-114">For information, see hello [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) page.</span></span>

* <span data-ttu-id="fa55f-115">已安裝 Xcode v7.0 或更新版本以及 Xamarin Studio Community 的 Mac。</span><span class="sxs-lookup"><span data-stu-id="fa55f-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="fa55f-116">如需相關資訊，請參閱[設定及安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) 及[針對 Mac 使用者設定、安裝和驗證](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN)。</span><span class="sxs-lookup"><span data-stu-id="fa55f-116">For information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Set up, install, and verify for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-a-new-mobile-apps-back-end"></a><span data-ttu-id="fa55f-117">建立新的 Mobile Apps 後端</span><span class="sxs-lookup"><span data-stu-id="fa55f-117">Create a new Mobile Apps back end</span></span>

<span data-ttu-id="fa55f-118">toocreate 新行動裝置應用程式備份結束時，請不要 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="fa55f-118">toocreate a new Mobile Apps back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="fa55f-119">您現在已設定您的行動用戶端應用程式可以使用的 Mobile Apps 後端。</span><span class="sxs-lookup"><span data-stu-id="fa55f-119">You have now set up a Mobile Apps back end that your mobile client applications can use.</span></span> <span data-ttu-id="fa55f-120">接下來，您下載的簡單的待辦事項清單後端伺服器專案，然後將它發行 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="fa55f-120">Next, you download a server project for a simple to-do list back end and then publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="fa55f-121">設定 hello 伺服器專案</span><span class="sxs-lookup"><span data-stu-id="fa55f-121">Configure hello server project</span></span>

<span data-ttu-id="fa55f-122">tooconfigure hello 伺服器專案 toouse hello Node.js 或.NET 後端，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="fa55f-122">tooconfigure hello server project toouse either hello Node.js or .NET back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a><span data-ttu-id="fa55f-123">下載並執行 hello Xamarin.Forms 方案</span><span class="sxs-lookup"><span data-stu-id="fa55f-123">Download and run hello Xamarin.Forms solution</span></span>

<span data-ttu-id="fa55f-124">您可以下載 hello 方案中任一種方式。</span><span class="sxs-lookup"><span data-stu-id="fa55f-124">You can download hello solution in either of two ways.</span></span> <span data-ttu-id="fa55f-125">下載 tooa Mac Xamarin Studio 中開啟或下載它 tooa Windows 電腦和 Visual Studio 中開啟建置 hello iOS 應用程式使用網路的 Mac。</span><span class="sxs-lookup"><span data-stu-id="fa55f-125">Download it tooa Mac and open it in Xamarin Studio, or download it tooa Windows computer and open it in Visual Studio by using a networked Mac for building hello iOS app.</span></span> <span data-ttu-id="fa55f-126">如需詳細資訊，請參閱[設定及安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fa55f-126">For more information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>

<span data-ttu-id="fa55f-127">Mac 或 Windows 的電腦上，hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="fa55f-127">On a Mac or Windows computer, do hello following:</span></span>

1. <span data-ttu-id="fa55f-128">移 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="fa55f-128">Go toohello [Azure portal].</span></span>

2. <span data-ttu-id="fa55f-129">在 hello**設定**刀鋒視窗中的行動應用程式下**行動**，選取**開始** > **Xamarin.Forms**。</span><span class="sxs-lookup"><span data-stu-id="fa55f-129">On hello **Settings** blade for your mobile app, under **Mobile**, select **Get Started** > **Xamarin.Forms**.</span></span> <span data-ttu-id="fa55f-130">在**步驟 3** 之下，選取 [建立新的應用程式]，然後選取 [下載]。</span><span class="sxs-lookup"><span data-stu-id="fa55f-130">Under **step 3**, select  **Create a new app**, and then select **Download**.</span></span>

   <span data-ttu-id="fa55f-131">這個動作會下載包含連線的 tooyour 行動裝置應用程式的用戶端應用程式的專案。</span><span class="sxs-lookup"><span data-stu-id="fa55f-131">This action downloads a project that contains a client application that's connected tooyour mobile app.</span></span> <span data-ttu-id="fa55f-132">儲存 hello 壓縮的專案檔案 tooyour 本機電腦，並記下您儲存的位置。</span><span class="sxs-lookup"><span data-stu-id="fa55f-132">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>

3. <span data-ttu-id="fa55f-133">解壓縮您下載的 hello 專案，然後再將它開啟在 Xamarin Studio (Mac) 或 Visual Studio (Windows) 中。</span><span class="sxs-lookup"><span data-stu-id="fa55f-133">Extract hello project that you downloaded, and then open it in Xamarin Studio (Mac) or Visual Studio (Windows).</span></span>

   ![在 Xamarin Studio 中解壓縮的專案][9]

   ![在 Visual Studio 中解壓縮的專案][8]

## <a name="optional-run-hello-ios-project"></a><span data-ttu-id="fa55f-136">（選擇性）執行 hello iOS 專案</span><span class="sxs-lookup"><span data-stu-id="fa55f-136">(Optional) Run hello iOS project</span></span>
<span data-ttu-id="fa55f-137">在本節中，您可以執行 hello Xamarin iOS 專案，適用於 iOS 裝置。</span><span class="sxs-lookup"><span data-stu-id="fa55f-137">In this section, you run hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="fa55f-138">如果未使用 iOS 裝置，可以略過這一節。</span><span class="sxs-lookup"><span data-stu-id="fa55f-138">You can skip this section if you are not working with iOS devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="fa55f-139">在 Xamarin Studio 中</span><span class="sxs-lookup"><span data-stu-id="fa55f-139">In Xamarin Studio</span></span>
1. <span data-ttu-id="fa55f-140">Hello iOS 專案，以滑鼠右鍵按一下，然後選取**設定為啟始專案**。</span><span class="sxs-lookup"><span data-stu-id="fa55f-140">Right-click hello iOS project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="fa55f-141">在 hello**執行**功能表上，選取**開始偵錯**toobuild hello 專案和 hello iPhone 模擬器中啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa55f-141">On hello **Run** menu, select **Start Debugging** toobuild hello project and start hello app in hello iPhone emulator.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="fa55f-142">在 Visual Studio 中</span><span class="sxs-lookup"><span data-stu-id="fa55f-142">In Visual Studio</span></span>
1. <span data-ttu-id="fa55f-143">Hello iOS 專案，以滑鼠右鍵按一下，然後選取**設定為啟始專案**。</span><span class="sxs-lookup"><span data-stu-id="fa55f-143">Right-click hello iOS project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="fa55f-144">在 hello**建置**功能表上，選取**Configuration Manager**。</span><span class="sxs-lookup"><span data-stu-id="fa55f-144">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="fa55f-145">在 hello **Configuration Manager**對話方塊中，選取 hello**建置**和**部署**下一步 toohello iOS 專案的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="fa55f-145">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello iOS project.</span></span>

4. <span data-ttu-id="fa55f-146">toobuild hello 專案和 hello 應用程式開始在 hello iPhone 模擬器中，選取 hello **F5**索引鍵。</span><span class="sxs-lookup"><span data-stu-id="fa55f-146">toobuild hello project and start hello app in hello iPhone emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fa55f-147">如果您有建置 hello 專案的問題，請執行 hello NuGet 套件管理員和更新 toohello 最新版本的 hello Xamarin 支援封裝。</span><span class="sxs-lookup"><span data-stu-id="fa55f-147">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="fa55f-148">快速入門專案可能會變慢 tooupdate toohello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="fa55f-148">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="fa55f-149">在 hello 應用程式中，輸入有意義的文字，例如*深入了解 Xamarin*，，然後選取 hello 加號 (**+**)。</span><span class="sxs-lookup"><span data-stu-id="fa55f-149">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][10]

    <span data-ttu-id="fa55f-150">這個動作會傳送新的行動應用程式後端裝載於 Azure post 要求 toohello。</span><span class="sxs-lookup"><span data-stu-id="fa55f-150">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="fa55f-151">Hello 要求的資料會插入至 hello TodoItem 資料表。</span><span class="sxs-lookup"><span data-stu-id="fa55f-151">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="fa55f-152">Hello 資料表中儲存的項目會傳回由 hello 回行動應用程式結束，而且 hello hello 清單中顯示資料。</span><span class="sxs-lookup"><span data-stu-id="fa55f-152">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fa55f-153">您可以找到存取您的行動應用程式後端 hello TodoItemManager.cs C# 檔案中的 hello 可攜式類別庫專案的方案中的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="fa55f-153">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-android-project"></a><span data-ttu-id="fa55f-154">（選擇性）執行 hello Android 專案</span><span class="sxs-lookup"><span data-stu-id="fa55f-154">(Optional) Run hello Android project</span></span>
<span data-ttu-id="fa55f-155">在本節中，您可以執行 hello Xamarin droid 專案 for Android。</span><span class="sxs-lookup"><span data-stu-id="fa55f-155">In this section, you run hello Xamarin droid project for Android.</span></span> <span data-ttu-id="fa55f-156">如果未使用 Android 裝置，可以略過這一節。</span><span class="sxs-lookup"><span data-stu-id="fa55f-156">You can skip this section if you are not working with Android devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="fa55f-157">在 Xamarin Studio 中</span><span class="sxs-lookup"><span data-stu-id="fa55f-157">In Xamarin Studio</span></span>

1. <span data-ttu-id="fa55f-158">Hello Android 專案，以滑鼠右鍵按一下，然後選取**設定為啟始專案**。</span><span class="sxs-lookup"><span data-stu-id="fa55f-158">Right-click hello Android project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="fa55f-159">toobuild hello 專案並開始 hello 應用程式在 Android 模擬器中，在 hello**執行**功能表上，選取**開始偵錯**。</span><span class="sxs-lookup"><span data-stu-id="fa55f-159">toobuild hello project and start hello app in an Android emulator, on hello **Run** menu, select **Start Debugging**.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="fa55f-160">在 Visual Studio 中</span><span class="sxs-lookup"><span data-stu-id="fa55f-160">In Visual Studio</span></span>

1. <span data-ttu-id="fa55f-161">Hello Android (Droid) 專案，以滑鼠右鍵按一下，然後選取**設定為啟始專案**。</span><span class="sxs-lookup"><span data-stu-id="fa55f-161">Right-click hello Android (Droid) project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="fa55f-162">在 hello**建置**功能表上，選取**Configuration Manager**。</span><span class="sxs-lookup"><span data-stu-id="fa55f-162">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="fa55f-163">在 hello **Configuration Manager**對話方塊中，選取 hello**建置**和**部署**核取方塊下一步 toohello Android 專案。</span><span class="sxs-lookup"><span data-stu-id="fa55f-163">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Android project.</span></span>

4. <span data-ttu-id="fa55f-164">toobuild hello 專案並開始 hello 應用程式在 Android 模擬器中，選取 hello **F5**索引鍵。</span><span class="sxs-lookup"><span data-stu-id="fa55f-164">toobuild hello project and start hello app in an Android emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fa55f-165">如果您有建置 hello 專案的問題，請執行 hello NuGet 套件管理員和更新 toohello 最新版本的 hello Xamarin 支援封裝。</span><span class="sxs-lookup"><span data-stu-id="fa55f-165">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="fa55f-166">快速入門專案可能會變慢 tooupdate toohello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="fa55f-166">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="fa55f-167">在 hello 應用程式中，輸入有意義的文字，例如*深入了解 Xamarin*，，然後選取 hello 加號 (**+**)。</span><span class="sxs-lookup"><span data-stu-id="fa55f-167">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][11]
    
    <span data-ttu-id="fa55f-168">這個動作會傳送新的行動應用程式後端裝載於 Azure post 要求 toohello。</span><span class="sxs-lookup"><span data-stu-id="fa55f-168">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="fa55f-169">Hello 要求的資料會插入至 hello TodoItem 資料表。</span><span class="sxs-lookup"><span data-stu-id="fa55f-169">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="fa55f-170">Hello 資料表中儲存的項目會傳回由 hello 回行動應用程式結束，而且 hello hello 清單中顯示資料。</span><span class="sxs-lookup"><span data-stu-id="fa55f-170">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="fa55f-171">您可以找到存取您的行動應用程式後端 hello TodoItemManager.cs C# 檔案中的 hello 可攜式類別庫專案的方案中的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="fa55f-171">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-windows-project"></a><span data-ttu-id="fa55f-172">（選擇性）執行 Windows hello 的專案</span><span class="sxs-lookup"><span data-stu-id="fa55f-172">(Optional) Run hello Windows project</span></span>

<span data-ttu-id="fa55f-173">在本節中，您可以執行 hello Xamarin WinApp 專案，適用於 Windows 裝置。</span><span class="sxs-lookup"><span data-stu-id="fa55f-173">In this section, you run hello Xamarin WinApp project for Windows devices.</span></span> <span data-ttu-id="fa55f-174">如果未使用 Windows 裝置，可以略過這一節。</span><span class="sxs-lookup"><span data-stu-id="fa55f-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="fa55f-175">在 Visual Studio 中</span><span class="sxs-lookup"><span data-stu-id="fa55f-175">In Visual Studio</span></span>

1. <span data-ttu-id="fa55f-176">任何 hello Windows 專案，以滑鼠右鍵按一下，然後選取**設定為啟始專案**。</span><span class="sxs-lookup"><span data-stu-id="fa55f-176">Right-click any of hello Windows projects, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="fa55f-177">在 hello**建置**功能表上，選取**Configuration Manager**。</span><span class="sxs-lookup"><span data-stu-id="fa55f-177">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="fa55f-178">在 hello **Configuration Manager**對話方塊中，選取 hello**建置**和**部署**您選擇的核取方塊下一步 toohello Windows 專案。</span><span class="sxs-lookup"><span data-stu-id="fa55f-178">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Windows project that you chose.</span></span>

4. <span data-ttu-id="fa55f-179">toobuild hello 專案並開始 hello 應用程式在 Windows 模擬器中，選取 hello **F5**索引鍵。</span><span class="sxs-lookup"><span data-stu-id="fa55f-179">toobuild hello project and start hello app in a Windows emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fa55f-180">如果您有建置 hello 專案的問題，請執行 hello NuGet 套件管理員和更新 toohello 最新版本的 hello Xamarin 支援封裝。</span><span class="sxs-lookup"><span data-stu-id="fa55f-180">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="fa55f-181">快速入門專案可能會變慢 tooupdate toohello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="fa55f-181">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="fa55f-182">在 hello 應用程式中，輸入有意義的文字，例如*深入了解 Xamarin*，，然後選取 hello 加號 (**+**)。</span><span class="sxs-lookup"><span data-stu-id="fa55f-182">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    <span data-ttu-id="fa55f-183">這個動作會傳送新的行動應用程式後端裝載於 Azure post 要求 toohello。</span><span class="sxs-lookup"><span data-stu-id="fa55f-183">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="fa55f-184">Hello 要求的資料會插入至 hello TodoItem 資料表。</span><span class="sxs-lookup"><span data-stu-id="fa55f-184">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="fa55f-185">Hello 資料表中儲存的項目會傳回由 hello 回行動應用程式結束，而且 hello hello 清單中顯示資料。</span><span class="sxs-lookup"><span data-stu-id="fa55f-185">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    ![][12]
    
    > [!NOTE]
    > <span data-ttu-id="fa55f-186">您可以找到存取您的行動應用程式後端 hello TodoItemManager.cs C# 檔案中的 hello 可攜式類別庫專案的方案中的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="fa55f-186">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="next-steps"></a><span data-ttu-id="fa55f-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fa55f-187">Next steps</span></span>

* [<span data-ttu-id="fa55f-188">新增驗證 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="fa55f-188">Add authentication tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="fa55f-189">深入了解如何 tooauthenticate 使用者身分識別提供者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa55f-189">Learn how tooauthenticate users of your app with an identity provider.</span></span>

* [<span data-ttu-id="fa55f-190">新增推播通知 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="fa55f-190">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)  
  <span data-ttu-id="fa55f-191">了解如何 tooadd 推播通知支援 tooyour 應用程式，並設定行動應用程式後端 toouse Azure 通知中樞 toosend hello 推播通知。</span><span class="sxs-lookup"><span data-stu-id="fa55f-191">Learn how tooadd push notifications support tooyour app and configure your Mobile Apps back end toouse Azure Notification Hubs toosend hello push notifications.</span></span>

* [<span data-ttu-id="fa55f-192">啟用應用程式的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="fa55f-192">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="fa55f-193">深入了解如何使用行動應用程式的應用程式的 tooadd 離線支援後端。</span><span class="sxs-lookup"><span data-stu-id="fa55f-193">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="fa55f-194">使用離線同步，即便在沒有網路連線的情況下，您也能檢視、新增或修改行動裝置應用程式的資料。</span><span class="sxs-lookup"><span data-stu-id="fa55f-194">With offline sync, you can view, add, or modify your mobile app's data, even when there is no network connection.</span></span>

* [<span data-ttu-id="fa55f-195">針對行動裝置應用程式使用 hello 受管理的用戶端</span><span class="sxs-lookup"><span data-stu-id="fa55f-195">Use hello managed client for Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)  
  <span data-ttu-id="fa55f-196">了解如何以 hello toowork 管理您的 Xamarin 應用程式中的用戶端 SDK。</span><span class="sxs-lookup"><span data-stu-id="fa55f-196">Learn how toowork with hello managed client SDK in your Xamarin app.</span></span>

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure 入口網站]: https://portal.azure.com/
