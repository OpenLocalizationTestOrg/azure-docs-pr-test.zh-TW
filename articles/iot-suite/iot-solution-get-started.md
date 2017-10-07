---
title: "MyDriving Azure IoT 範例：快速入門 | Microsoft Docs"
description: "開始使用應用程式的方式的完整示範 tooarchitect IoT 系統使用 Microsoft Azure，包括資料流分析、 機器學習和事件中心。"
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: f40ea71b-5721-4a6b-a886-53c2e9dffe8f
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 03/25/2016
ms.author: harikm
ms.openlocfilehash: 411b9a992deb22b915f8291d8559e2917d976b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="mydriving-iot-system-quick-start"></a><span data-ttu-id="e8632-103">MyDriving IoT 系統：快速入門</span><span class="sxs-lookup"><span data-stu-id="e8632-103">MyDriving IoT system: Quick start</span></span>
<span data-ttu-id="e8632-104">MyDriving 是示範 hello 設計和實作典型的系統[物聯網](iot-suite-overview.md)(IoT) 解決方案，並從裝置收集遙測處理 hello 雲端中的該資料，並套用機器學習服務tooprovide 適應性回應。</span><span class="sxs-lookup"><span data-stu-id="e8632-104">MyDriving is a system that demonstrates hello design and implementation of a typical [Internet of Things](iot-suite-overview.md) (IoT) solution that gathers telemetry from devices, processes that data in hello cloud, and applies machine learning tooprovide an adaptive response.</span></span> <span data-ttu-id="e8632-105">hello 示範使用從您的行動電話和收集的資訊從您的車上控制系統的配接器的資料來記錄您汽車往返，相關資料。</span><span class="sxs-lookup"><span data-stu-id="e8632-105">hello demonstration logs data about your car trips, by using data from both your mobile phone and an adapter that collects information from your car’s control system.</span></span> <span data-ttu-id="e8632-106">它會使用此資料 tooprovide 意見反應您在比較 tooother 使用者驅動的樣式。</span><span class="sxs-lookup"><span data-stu-id="e8632-106">It uses this data tooprovide feedback on your driving style in comparison tooother users.</span></span>

<span data-ttu-id="e8632-107">hello MyDriving 實際用途是的 tooget 您開始建立您自己的 IoT 解決方案。</span><span class="sxs-lookup"><span data-stu-id="e8632-107">hello real purpose of MyDriving is tooget you started in creating your own IoT solution.</span></span> <span data-ttu-id="e8632-108">但是之前，讓我們來引導您使用 hello MyDriving 應用程式本身-我們的測試使用者小組的成員。</span><span class="sxs-lookup"><span data-stu-id="e8632-108">But before that, let’s get you going with hello MyDriving app itself--as a member of our test user team.</span></span> <span data-ttu-id="e8632-109">這可讓您體驗 hello 應用程式和消費者，它後面的 hello 系統之前您深入 hello 架構。</span><span class="sxs-lookup"><span data-stu-id="e8632-109">This gives you an experience of hello app and hello system behind it as a consumer, before you delve into hello architecture.</span></span> <span data-ttu-id="e8632-110">它也為您介紹 tooHockeyApp，cool 管理的應用程式 tootest 使用者的 hello alpha 和 beta 分佈的方法。</span><span class="sxs-lookup"><span data-stu-id="e8632-110">It also introduces you tooHockeyApp, a cool way of managing hello alpha and beta distributions of your apps tootest users.</span></span>

## <a name="use-hello-mobile-experience"></a><span data-ttu-id="e8632-111">使用 hello 行動體驗</span><span class="sxs-lookup"><span data-stu-id="e8632-111">Use hello mobile experience</span></span>
<span data-ttu-id="e8632-112">如果您有在 Android、 iOS 或 Windows 10 裝置，您可以使用 hello MyDriving 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e8632-112">You can use hello MyDriving app if you have an Android, iOS, or Windows 10 device.</span></span>

### <a name="android-and-windows-10-mobile-installation"></a><span data-ttu-id="e8632-113">Android 和 Windows 10 Mobile 安裝</span><span class="sxs-lookup"><span data-stu-id="e8632-113">Android and Windows 10 Mobile installation</span></span>
<span data-ttu-id="e8632-114">在您的裝置上：</span><span class="sxs-lookup"><span data-stu-id="e8632-114">On your device:</span></span>

1. <span data-ttu-id="e8632-115">允許部署應用程式：</span><span class="sxs-lookup"><span data-stu-id="e8632-115">Allow development apps:</span></span>
   
   * <span data-ttu-id="e8632-116">Android：在 [設定] > [安全性] 中，允許來自 [未知來源] 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e8632-116">Android: In **Settings** > **Security**, allow apps from **Unknown sources**.</span></span>
   * <span data-ttu-id="e8632-117">Windows 10：在 [設定] > [更新] > [適用於開發人員] 中，設定 [開發人員模式]。</span><span class="sxs-lookup"><span data-stu-id="e8632-117">Windows 10: In **Settings** > **Updates** > **For Developers**, set **Developer mode**.</span></span>
2. <span data-ttu-id="e8632-118">使用 [HockeyApp](https://rink.hockeyapp.net)登入，或登入其中，以加入我們的 beta 版測試小組。</span><span class="sxs-lookup"><span data-stu-id="e8632-118">Join our beta test team by signing up with, or signing in to, [HockeyApp](https://rink.hockeyapp.net).</span></span> <span data-ttu-id="e8632-119">HockeyApp 可讓您的應用程式 tootest 使用者容易 toodistribute 早期版本。</span><span class="sxs-lookup"><span data-stu-id="e8632-119">HockeyApp makes it easy toodistribute early releases of your app tootest users.</span></span>
   
   <span data-ttu-id="e8632-120">如果您使用 Windows 10，使用 hello Edge 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="e8632-120">If you’re using Windows 10, use hello Edge browser.</span></span>
   
   <span data-ttu-id="e8632-121">如果您建置 2016年出席者，使用登入 hello 相同您註冊使用其中一種 Microsoft 按鈕 hello hello 會議的 Microsoft 帳戶電子郵件。</span><span class="sxs-lookup"><span data-stu-id="e8632-121">If you were a Build 2016 attendee, sign in with hello same Microsoft account email that you registered for hello conference, by using one of hello Microsoft buttons.</span></span> <span data-ttu-id="e8632-122">您已經向 HockeyApp 註冊。</span><span class="sxs-lookup"><span data-stu-id="e8632-122">You’re already signed up with HockeyApp.</span></span>
   
   ![HockeyApp 登入畫面](./media/iot-solution-get-started/image1.png)
3. <span data-ttu-id="e8632-124">下載並安裝 hello 應用程式，從這裡：</span><span class="sxs-lookup"><span data-stu-id="e8632-124">Download and install hello app from here:</span></span>
   
   * [<span data-ttu-id="e8632-125">Android</span><span class="sxs-lookup"><span data-stu-id="e8632-125">Android</span></span>](http://rink.io/spMyDrivingAndroid)
   * [<span data-ttu-id="e8632-126">Windows 10</span><span class="sxs-lookup"><span data-stu-id="e8632-126">Windows 10</span></span>](http://rink.io/spMyDrivingUWP)
   
   <span data-ttu-id="e8632-127">有兩個項目。</span><span class="sxs-lookup"><span data-stu-id="e8632-127">There are two items.</span></span> <span data-ttu-id="e8632-128">安裝中的 hello 憑證**受信任的人**。</span><span class="sxs-lookup"><span data-stu-id="e8632-128">Install hello certificate in **Trusted People**.</span></span> <span data-ttu-id="e8632-129">接著，安裝 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e8632-129">Then install hello app.</span></span>

<span data-ttu-id="e8632-130">*Windows 10 行動裝置上啟動 hello 應用程式的任何問題嗎？*</span><span class="sxs-lookup"><span data-stu-id="e8632-130">*Any issues starting hello app on Windows 10 Mobile?*</span></span> <span data-ttu-id="e8632-131">可能是因為您的手機是上一次或上上一次更新的版本。</span><span class="sxs-lookup"><span data-stu-id="e8632-131">Your phone might be an update or two behind.</span></span> <span data-ttu-id="e8632-132">請確定您已收到 hello 最新的更新，或安裝：</span><span class="sxs-lookup"><span data-stu-id="e8632-132">Make sure you've got hello latest updates, or install:</span></span>

* [<span data-ttu-id="e8632-133">Microsoft.NET.Native.Framework.1.2.appx</span><span class="sxs-lookup"><span data-stu-id="e8632-133">Microsoft.NET.Native.Framework.1.2.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [<span data-ttu-id="e8632-134">Microsoft.NET.Native.Runtime.1.1.appx</span><span class="sxs-lookup"><span data-stu-id="e8632-134">Microsoft.NET.Native.Runtime.1.1.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [<span data-ttu-id="e8632-135">Microsoft.VCLibs.ARM.14.00.appx</span><span class="sxs-lookup"><span data-stu-id="e8632-135">Microsoft.VCLibs.ARM.14.00.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a><span data-ttu-id="e8632-136">iOS 安裝</span><span class="sxs-lookup"><span data-stu-id="e8632-136">iOS installation</span></span>
<span data-ttu-id="e8632-137">如果您參加組建 2016年，下載 hello 應用程式的 HockeyApp 上我們測試的小組成員：</span><span class="sxs-lookup"><span data-stu-id="e8632-137">If you attended Build 2016, download hello app as a member of our test team on HockeyApp:</span></span>

1. <span data-ttu-id="e8632-138">在您的 iOS 裝置上登入太[HockeyApp](https://rink.hockeyapp.net)。</span><span class="sxs-lookup"><span data-stu-id="e8632-138">On your iOS device, sign in too[HockeyApp](https://rink.hockeyapp.net).</span></span>
   <span data-ttu-id="e8632-139">使用其中一個 hello Microsoft 登入按鈕和登入的 hello 同一個 Microsoft 帳戶電子郵件，您已註冊 hello 會議。</span><span class="sxs-lookup"><span data-stu-id="e8632-139">Use one of hello Microsoft sign-in buttons, and sign in with hello same Microsoft account email that you registered with hello conference.</span></span> <span data-ttu-id="e8632-140">（請勿使用 hello 電子郵件和密碼欄位）。</span><span class="sxs-lookup"><span data-stu-id="e8632-140">(Don’t use hello email and password fields.)</span></span>
   
   ![HockeyApp 登入畫面](./media/iot-solution-get-started/image1.png)
2. <span data-ttu-id="e8632-142">Hello HockeyApp 儀表板中選取 MyDriving 並下載它。</span><span class="sxs-lookup"><span data-stu-id="e8632-142">In hello HockeyApp dashboard, select MyDriving and download it.</span></span>
3. <span data-ttu-id="e8632-143">授權來自 HockeyApp 的 hello beta 版：</span><span class="sxs-lookup"><span data-stu-id="e8632-143">Authorize hello beta release from HockeyApp:</span></span>
   
   <span data-ttu-id="e8632-144">a.</span><span class="sxs-lookup"><span data-stu-id="e8632-144">a.</span></span> <span data-ttu-id="e8632-145">跳過**設定** > **一般** > **設定檔和裝置管理。**</span><span class="sxs-lookup"><span data-stu-id="e8632-145">Go too**Settings** > **General** > **Profiles and Device Management.**</span></span>
   
   <span data-ttu-id="e8632-146">b.</span><span class="sxs-lookup"><span data-stu-id="e8632-146">b.</span></span> <span data-ttu-id="e8632-147">信任 hello**元場地 GmbH**憑證。</span><span class="sxs-lookup"><span data-stu-id="e8632-147">Trust hello **Bit Stadium GmbH** certificate.</span></span>

<span data-ttu-id="e8632-148">如果您沒有參與建置 2016年，您可以建置並自行部署 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="e8632-148">If you didn’t attend Build 2016, you can build and deploy hello app yourself:</span></span>

1. <span data-ttu-id="e8632-149">下載 hello 程式碼[從 GitHub]。</span><span class="sxs-lookup"><span data-stu-id="e8632-149">Download hello code [from GitHub].</span></span>
2. <span data-ttu-id="e8632-150">[使用 Xamarin]建置及部署。</span><span class="sxs-lookup"><span data-stu-id="e8632-150">Build and deploy by [using Xamarin].</span></span>

<span data-ttu-id="e8632-151">尋找更多詳細資料中 hello [MyDriving 參考指南](http://aka.ms/mydrivingdocs)。</span><span class="sxs-lookup"><span data-stu-id="e8632-151">Find more details in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="get-an-obd-adapter-optional"></a><span data-ttu-id="e8632-152">取得 OBD 配接器 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="e8632-152">Get an OBD adapter (optional)</span></span>
<span data-ttu-id="e8632-153">這是使這個成為實際的物聯網系統的 hello 一部分 ！</span><span class="sxs-lookup"><span data-stu-id="e8632-153">This is hello part that makes this a real Internet of Things system!</span></span> <span data-ttu-id="e8632-154">您可以使用 hello 應用程式不含費率，但與 hello 真實的事物，更有趣，它們不是高度耗費資源。</span><span class="sxs-lookup"><span data-stu-id="e8632-154">You can use hello app without one, but it’s more fun with hello real thing, and they aren’t expensive.</span></span>

<span data-ttu-id="e8632-155">主機板診斷 (OBD) 是您的車上 hello 註冊您的車上機庫使用 tootune 並診斷奇數的雜音會較與警告燈 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="e8632-155">On-board diagnostics (OBD) is hello feature of your car that hello garage uses tootune up your car and diagnose odd noises and warning lamps.</span></span> <span data-ttu-id="e8632-156">除非您的車上是絕佳的 antiquity，您會發現 hello 木屋給毀，通常背後 flap 下 hello 儀表板中的某處的通訊端。</span><span class="sxs-lookup"><span data-stu-id="e8632-156">Unless your car is of great antiquity, you’ll find a socket somewhere in hello cabin, typically behind a flap under hello dashboard.</span></span> <span data-ttu-id="e8632-157">與 hello 右連接器，您可以取得 hello 引擎效能的度量，並調整特定。</span><span class="sxs-lookup"><span data-stu-id="e8632-157">With hello right connector, you can get metrics of hello engine’s performance and make certain adjustments.</span></span> <span data-ttu-id="e8632-158">可以從 hello 一般地方廉價地購買 OBD 連接器。</span><span class="sxs-lookup"><span data-stu-id="e8632-158">An OBD connector can be purchased cheaply from hello usual places.</span></span> <span data-ttu-id="e8632-159">它會連接您的手機上使用藍芽或 Wi-fi tooan 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e8632-159">It connects by using Bluetooth or Wi-Fi tooan app on your phone.</span></span>

<span data-ttu-id="e8632-160">在此情況下，我們 tooconnect 汽車 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="e8632-160">In this case, we’re going tooconnect your car toohello cloud.</span></span> <span data-ttu-id="e8632-161">從 hello OBD hello 直接連接 tooyour 電話，但我們的應用程式的運作方式的轉送。</span><span class="sxs-lookup"><span data-stu-id="e8632-161">hello direct connection from hello OBD is tooyour phone, but our app works as a relay.</span></span> <span data-ttu-id="e8632-162">您的車上遙測直線 toohello MyDriving IoT 中樞，其中是處理 toolog 道路往返傳送，並評估程式驅動的樣式。</span><span class="sxs-lookup"><span data-stu-id="e8632-162">Your car's telemetry is sent straight toohello MyDriving IoT hub, where it's processed toolog your road trips and assess your driving style.</span></span>

<span data-ttu-id="e8632-163">tooconnect OBD 裝置：</span><span class="sxs-lookup"><span data-stu-id="e8632-163">tooconnect an OBD device:</span></span>

1. <span data-ttu-id="e8632-164">檢查您的車子是否有 OBD 插座。</span><span class="sxs-lookup"><span data-stu-id="e8632-164">Check that your car has an OBD socket.</span></span>
2. <span data-ttu-id="e8632-165">取得 OBD 配接器：</span><span class="sxs-lookup"><span data-stu-id="e8632-165">Obtain an OBD adapter:</span></span>
   
   * <span data-ttu-id="e8632-166">若是使用 Android 或 Windows 手機，您需要支援藍牙的 OBD II 配接器。</span><span class="sxs-lookup"><span data-stu-id="e8632-166">If you're using an Android or Windows phone, you need a Bluetooth-enabled OBD II adapter.</span></span> <span data-ttu-id="e8632-167">我們使用 [BAFX Products 34t5 Bluetooth OBDII Scan Tool (BAFX 產品 34t5 藍牙 OBDII 掃描工具)]。</span><span class="sxs-lookup"><span data-stu-id="e8632-167">We used [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span></span>
   * <span data-ttu-id="e8632-168">若是使用 iOS 手機，您需要支援 WiFi 的 OBD 配接器。</span><span class="sxs-lookup"><span data-stu-id="e8632-168">If you're using an iOS phone, you need a Wi-Fi-enabled OBD adapter.</span></span> <span data-ttu-id="e8632-169">我們使用 [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner (ScanTool OBDLink MX Wi-Fi: OBD 配接器/診斷掃描器)]。</span><span class="sxs-lookup"><span data-stu-id="e8632-169">We used [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span></span>
3. <span data-ttu-id="e8632-170">請遵循隨附於您 OBD 配接器 tooconnect 它 tooyour 電話的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="e8632-170">Follow hello instructions that come with your OBD adapter tooconnect it tooyour phone.</span></span> <span data-ttu-id="e8632-171">請注意下列 hello:</span><span class="sxs-lookup"><span data-stu-id="e8632-171">Keep hello following in mind:</span></span>
   
   * <span data-ttu-id="e8632-172">藍芽介面卡必須搭配 hello 電話，在 hello**設定**頁面。</span><span class="sxs-lookup"><span data-stu-id="e8632-172">A Bluetooth adapter must be paired with hello phone, on hello **Settings** page.</span></span>
   * <span data-ttu-id="e8632-173">Wi-fi 配接器必須具有在 hello 範圍 192.168.xxx.xxx 的位址。</span><span class="sxs-lookup"><span data-stu-id="e8632-173">A Wi-Fi adapter must have an address in hello range 192.168.xxx.xxx.</span></span>
4. <span data-ttu-id="e8632-174">如果您擁有數部車，您可以為每部車取得個別的配接器 (最多三個)。</span><span class="sxs-lookup"><span data-stu-id="e8632-174">If you have several cars, you can get a separate adapter for each (maximum of three).</span></span>

<span data-ttu-id="e8632-175">如果您沒有 OBD 配接器，則位置和速度的資料從 hello 電話 GPS 接收者 toohello 回結束，並將詢問您是否要 toosimulate OBD 仍會傳送 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e8632-175">If you don’t have an OBD adapter, hello app will still send location and speed data from hello phone's GPS receiver toohello back end and will ask if you want toosimulate an OBD.</span></span>

<span data-ttu-id="e8632-176">您可以找到更多有關 hello 應用程式如何使用 hello OBD 配接器的資料，以及區段 2.1 中，「 IoT 裝置 」 中建立您自己的 OBD 裝置選項 hello [MyDriving 參考指南](http://aka.ms/mydrivingdocs)。</span><span class="sxs-lookup"><span data-stu-id="e8632-176">You can find out more about how hello app uses data from hello OBD adapter and about options for creating your own OBD device in section 2.1, "IoT Devices," in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="use-hello-app"></a><span data-ttu-id="e8632-177">使用 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e8632-177">Use hello app</span></span>
<span data-ttu-id="e8632-178">啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e8632-178">Start hello app.</span></span> <span data-ttu-id="e8632-179">沒有初始的快速入門 toowalk 您透過它的運作方式。</span><span class="sxs-lookup"><span data-stu-id="e8632-179">There’s an initial Quickstart toowalk you through how it works.</span></span>

### <a name="track-your-trips"></a><span data-ttu-id="e8632-180">追蹤您的行程</span><span class="sxs-lookup"><span data-stu-id="e8632-180">Track your trips</span></span>
<span data-ttu-id="e8632-181">點選 hello 記錄 按鈕 （在 hello 囉 」 畫面底部的大紅色圓形） toostart 路線，並再次點選 tooend。</span><span class="sxs-lookup"><span data-stu-id="e8632-181">Tap hello record button (big red circle at hello bottom of hello screen) toostart a trip, and tap again tooend.</span></span>

![追蹤路線的 hello record 按鈕的圖例](./media/iot-solution-get-started/image2.png)

<span data-ttu-id="e8632-183">每次啟動路線，如果沒有任何 OBD 裝置，您會詢問您是否 toouse hello 模擬器。</span><span class="sxs-lookup"><span data-stu-id="e8632-183">Each time you start a trip, if there’s no OBD device, you’ll be asked if you want toouse hello simulator.</span></span>

<span data-ttu-id="e8632-184">在 hello 路線結尾，點選 hello 停止 按鈕，而且您會取得摘要。</span><span class="sxs-lookup"><span data-stu-id="e8632-184">At hello end of a trip, tap hello stop button, and you get a summary.</span></span>

![車程摘要的範例](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a><span data-ttu-id="e8632-186">檢閱您的行程</span><span class="sxs-lookup"><span data-stu-id="e8632-186">Review your trips</span></span>
![上一趟車程的範例](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a><span data-ttu-id="e8632-188">檢閱您的設定檔</span><span class="sxs-lookup"><span data-stu-id="e8632-188">Review your profile</span></span>
![駕駛風格設定檔的範例](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a><span data-ttu-id="e8632-190">將您的測試意見反應傳給我們</span><span class="sxs-lookup"><span data-stu-id="e8632-190">Send us your test feedback</span></span>
<span data-ttu-id="e8632-191">因為我們建立 MyDriving toohelp 開始使用您自己的 IoT 系統時，我們可以確定您需要 toohear 您有關它的運作方式。</span><span class="sxs-lookup"><span data-stu-id="e8632-191">Because we created MyDriving toohelp jumpstart your own IoT systems, we certainly want toohear from you about how well it works.</span></span> <span data-ttu-id="e8632-192">若發生下列情況，請告訴我們：</span><span class="sxs-lookup"><span data-stu-id="e8632-192">Let us know if:</span></span>

* <span data-ttu-id="e8632-193">您遇到問題或挑戰。</span><span class="sxs-lookup"><span data-stu-id="e8632-193">You run into difficulties or challenges.</span></span>
* <span data-ttu-id="e8632-194">沒有擴充點，會讓它更適合 tooyour 案例。</span><span class="sxs-lookup"><span data-stu-id="e8632-194">There is an extension point that would make it more suitable tooyour scenario.</span></span>
* <span data-ttu-id="e8632-195">您尋找更有效率的方式 tooaccomplish 特定需求。</span><span class="sxs-lookup"><span data-stu-id="e8632-195">You find a more efficient way tooaccomplish certain needs.</span></span>
* <span data-ttu-id="e8632-196">您有改善 MyDriving 或這份文件的任何其他建議。</span><span class="sxs-lookup"><span data-stu-id="e8632-196">You have any other suggestions for improving MyDriving or this documentation.</span></span>

<span data-ttu-id="e8632-197">Hello MyDriving 應用程式本身，在中，您可以使用內建 HockeyApp 意見反應機制 hello： 在 iOS 和 Android，只需要為提供您的電話搖晃，或使用 hello**意見反應**功能表命令。</span><span class="sxs-lookup"><span data-stu-id="e8632-197">Within hello MyDriving app itself, you can use hello built-in HockeyApp feedback mechanism: on iOS and Android, just give your phone a shake, or use hello **Feedback** menu command.</span></span> <span data-ttu-id="e8632-198">這將會自動附加螢幕擷取畫面，這樣我們就能知道您在說什麼。</span><span class="sxs-lookup"><span data-stu-id="e8632-198">This will automatically attach a screenshot, so that we’ll know what you’re talking about.</span></span> <span data-ttu-id="e8632-199">並沒有任何不幸當機，如果 HockeyApp 收集 hello 損毀記錄檔 tootell 我們資訊，請。</span><span class="sxs-lookup"><span data-stu-id="e8632-199">And if there are any unfortunate crashes, HockeyApp collects hello crash logs tootell us about them.</span></span> <span data-ttu-id="e8632-200">您也可以提供意見反應透過 hello [HockeyApp 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="e8632-200">You can also give feedback through hello [HockeyApp portal].</span></span>

<span data-ttu-id="e8632-201">您也可以[在 GitHub 上提出問題]，或在底下留下意見 (英文版)。</span><span class="sxs-lookup"><span data-stu-id="e8632-201">You can also file an [issue on GitHub], or leave a comment below (en-us edition).</span></span>

<span data-ttu-id="e8632-202">我們期待 toohearing 您 ！</span><span class="sxs-lookup"><span data-stu-id="e8632-202">We look forward toohearing from you!</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8632-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e8632-203">Next steps</span></span>
* <span data-ttu-id="e8632-204">瀏覽 hello [MyDriving 參考指南](http://aka.ms/mydrivingdocs)toounderstand 我們已在如何設計和建置 hello 整個 MyDriving 系統。</span><span class="sxs-lookup"><span data-stu-id="e8632-204">Explore hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) toounderstand how we’ve designed and built hello entire MyDriving system.</span></span>
* <span data-ttu-id="e8632-205">[Create and deploy a system of your own (建立及部署您自己的系統) (建立及部署您自己的系統)](iot-solution-build-system.md) 。</span><span class="sxs-lookup"><span data-stu-id="e8632-205">[Create and deploy a system of your own](iot-solution-build-system.md) by using our Azure Resource Manager scripts.</span></span> <span data-ttu-id="e8632-206">hello [MyDriving 參考指南](http://aka.ms/mydrivingdocs)也會引導您完成其中您要進行 hello 大多數的自訂區域。</span><span class="sxs-lookup"><span data-stu-id="e8632-206">hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) also guides you through areas where you’ll make hello most customizations.</span></span>

[從 GitHub]: https://github.com/Azure-Samples/MyDriving
[使用 Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[BAFX Products 34t5 Bluetooth OBDII Scan Tool (BAFX 產品 34t5 藍牙 OBDII 掃描工具)]: http://www.amazon.com/gp/product/B005NLQAHS
[ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner (ScanTool OBDLink MX Wi-Fi: OBD 配接器/診斷掃描器)]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[HockeyApp 入口網站]: https://rink.hockeyapp.org
[在 GitHub 上提出問題]: https://github.com/Azure-Samples/MyDriving/issues
