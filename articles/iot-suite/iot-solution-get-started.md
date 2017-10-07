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
# <a name="mydriving-iot-system-quick-start"></a>MyDriving IoT 系統：快速入門
MyDriving 是示範 hello 設計和實作典型的系統[物聯網](iot-suite-overview.md)(IoT) 解決方案，並從裝置收集遙測處理 hello 雲端中的該資料，並套用機器學習服務tooprovide 適應性回應。 hello 示範使用從您的行動電話和收集的資訊從您的車上控制系統的配接器的資料來記錄您汽車往返，相關資料。 它會使用此資料 tooprovide 意見反應您在比較 tooother 使用者驅動的樣式。

hello MyDriving 實際用途是的 tooget 您開始建立您自己的 IoT 解決方案。 但是之前，讓我們來引導您使用 hello MyDriving 應用程式本身-我們的測試使用者小組的成員。 這可讓您體驗 hello 應用程式和消費者，它後面的 hello 系統之前您深入 hello 架構。 它也為您介紹 tooHockeyApp，cool 管理的應用程式 tootest 使用者的 hello alpha 和 beta 分佈的方法。

## <a name="use-hello-mobile-experience"></a>使用 hello 行動體驗
如果您有在 Android、 iOS 或 Windows 10 裝置，您可以使用 hello MyDriving 應用程式。

### <a name="android-and-windows-10-mobile-installation"></a>Android 和 Windows 10 Mobile 安裝
在您的裝置上：

1. 允許部署應用程式：
   
   * Android：在 [設定] > [安全性] 中，允許來自 [未知來源] 的應用程式。
   * Windows 10：在 [設定] > [更新] > [適用於開發人員] 中，設定 [開發人員模式]。
2. 使用 [HockeyApp](https://rink.hockeyapp.net)登入，或登入其中，以加入我們的 beta 版測試小組。 HockeyApp 可讓您的應用程式 tootest 使用者容易 toodistribute 早期版本。
   
   如果您使用 Windows 10，使用 hello Edge 瀏覽器。
   
   如果您建置 2016年出席者，使用登入 hello 相同您註冊使用其中一種 Microsoft 按鈕 hello hello 會議的 Microsoft 帳戶電子郵件。 您已經向 HockeyApp 註冊。
   
   ![HockeyApp 登入畫面](./media/iot-solution-get-started/image1.png)
3. 下載並安裝 hello 應用程式，從這裡：
   
   * [Android](http://rink.io/spMyDrivingAndroid)
   * [Windows 10](http://rink.io/spMyDrivingUWP)
   
   有兩個項目。 安裝中的 hello 憑證**受信任的人**。 接著，安裝 hello 應用程式。

*Windows 10 行動裝置上啟動 hello 應用程式的任何問題嗎？* 可能是因為您的手機是上一次或上上一次更新的版本。 請確定您已收到 hello 最新的更新，或安裝：

* [Microsoft.NET.Native.Framework.1.2.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [Microsoft.NET.Native.Runtime.1.1.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [Microsoft.VCLibs.ARM.14.00.appx](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a>iOS 安裝
如果您參加組建 2016年，下載 hello 應用程式的 HockeyApp 上我們測試的小組成員：

1. 在您的 iOS 裝置上登入太[HockeyApp](https://rink.hockeyapp.net)。
   使用其中一個 hello Microsoft 登入按鈕和登入的 hello 同一個 Microsoft 帳戶電子郵件，您已註冊 hello 會議。 （請勿使用 hello 電子郵件和密碼欄位）。
   
   ![HockeyApp 登入畫面](./media/iot-solution-get-started/image1.png)
2. Hello HockeyApp 儀表板中選取 MyDriving 並下載它。
3. 授權來自 HockeyApp 的 hello beta 版：
   
   a. 跳過**設定** > **一般** > **設定檔和裝置管理。**
   
   b. 信任 hello**元場地 GmbH**憑證。

如果您沒有參與建置 2016年，您可以建置並自行部署 hello 應用程式：

1. 下載 hello 程式碼[從 GitHub]。
2. [使用 Xamarin]建置及部署。

尋找更多詳細資料中 hello [MyDriving 參考指南](http://aka.ms/mydrivingdocs)。

## <a name="get-an-obd-adapter-optional"></a>取得 OBD 配接器 (選擇性)
這是使這個成為實際的物聯網系統的 hello 一部分 ！ 您可以使用 hello 應用程式不含費率，但與 hello 真實的事物，更有趣，它們不是高度耗費資源。

主機板診斷 (OBD) 是您的車上 hello 註冊您的車上機庫使用 tootune 並診斷奇數的雜音會較與警告燈 hello 功能。 除非您的車上是絕佳的 antiquity，您會發現 hello 木屋給毀，通常背後 flap 下 hello 儀表板中的某處的通訊端。 與 hello 右連接器，您可以取得 hello 引擎效能的度量，並調整特定。 可以從 hello 一般地方廉價地購買 OBD 連接器。 它會連接您的手機上使用藍芽或 Wi-fi tooan 應用程式。

在此情況下，我們 tooconnect 汽車 toohello 雲端。 從 hello OBD hello 直接連接 tooyour 電話，但我們的應用程式的運作方式的轉送。 您的車上遙測直線 toohello MyDriving IoT 中樞，其中是處理 toolog 道路往返傳送，並評估程式驅動的樣式。

tooconnect OBD 裝置：

1. 檢查您的車子是否有 OBD 插座。
2. 取得 OBD 配接器：
   
   * 若是使用 Android 或 Windows 手機，您需要支援藍牙的 OBD II 配接器。 我們使用 [BAFX Products 34t5 Bluetooth OBDII Scan Tool (BAFX 產品 34t5 藍牙 OBDII 掃描工具)]。
   * 若是使用 iOS 手機，您需要支援 WiFi 的 OBD 配接器。 我們使用 [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner (ScanTool OBDLink MX Wi-Fi: OBD 配接器/診斷掃描器)]。
3. 請遵循隨附於您 OBD 配接器 tooconnect 它 tooyour 電話的 hello 指示。 請注意下列 hello:
   
   * 藍芽介面卡必須搭配 hello 電話，在 hello**設定**頁面。
   * Wi-fi 配接器必須具有在 hello 範圍 192.168.xxx.xxx 的位址。
4. 如果您擁有數部車，您可以為每部車取得個別的配接器 (最多三個)。

如果您沒有 OBD 配接器，則位置和速度的資料從 hello 電話 GPS 接收者 toohello 回結束，並將詢問您是否要 toosimulate OBD 仍會傳送 hello 應用程式。

您可以找到更多有關 hello 應用程式如何使用 hello OBD 配接器的資料，以及區段 2.1 中，「 IoT 裝置 」 中建立您自己的 OBD 裝置選項 hello [MyDriving 參考指南](http://aka.ms/mydrivingdocs)。

## <a name="use-hello-app"></a>使用 hello 應用程式
啟動 hello 應用程式。 沒有初始的快速入門 toowalk 您透過它的運作方式。

### <a name="track-your-trips"></a>追蹤您的行程
點選 hello 記錄 按鈕 （在 hello 囉 」 畫面底部的大紅色圓形） toostart 路線，並再次點選 tooend。

![追蹤路線的 hello record 按鈕的圖例](./media/iot-solution-get-started/image2.png)

每次啟動路線，如果沒有任何 OBD 裝置，您會詢問您是否 toouse hello 模擬器。

在 hello 路線結尾，點選 hello 停止 按鈕，而且您會取得摘要。

![車程摘要的範例](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a>檢閱您的行程
![上一趟車程的範例](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a>檢閱您的設定檔
![駕駛風格設定檔的範例](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a>將您的測試意見反應傳給我們
因為我們建立 MyDriving toohelp 開始使用您自己的 IoT 系統時，我們可以確定您需要 toohear 您有關它的運作方式。 若發生下列情況，請告訴我們：

* 您遇到問題或挑戰。
* 沒有擴充點，會讓它更適合 tooyour 案例。
* 您尋找更有效率的方式 tooaccomplish 特定需求。
* 您有改善 MyDriving 或這份文件的任何其他建議。

Hello MyDriving 應用程式本身，在中，您可以使用內建 HockeyApp 意見反應機制 hello： 在 iOS 和 Android，只需要為提供您的電話搖晃，或使用 hello**意見反應**功能表命令。 這將會自動附加螢幕擷取畫面，這樣我們就能知道您在說什麼。 並沒有任何不幸當機，如果 HockeyApp 收集 hello 損毀記錄檔 tootell 我們資訊，請。 您也可以提供意見反應透過 hello [HockeyApp 入口網站]。

您也可以[在 GitHub 上提出問題]，或在底下留下意見 (英文版)。

我們期待 toohearing 您 ！

## <a name="next-steps"></a>後續步驟
* 瀏覽 hello [MyDriving 參考指南](http://aka.ms/mydrivingdocs)toounderstand 我們已在如何設計和建置 hello 整個 MyDriving 系統。
* [Create and deploy a system of your own (建立及部署您自己的系統) (建立及部署您自己的系統)](iot-solution-build-system.md) 。 hello [MyDriving 參考指南](http://aka.ms/mydrivingdocs)也會引導您完成其中您要進行 hello 大多數的自訂區域。

[從 GitHub]: https://github.com/Azure-Samples/MyDriving
[使用 Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[BAFX Products 34t5 Bluetooth OBDII Scan Tool (BAFX 產品 34t5 藍牙 OBDII 掃描工具)]: http://www.amazon.com/gp/product/B005NLQAHS
[ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner (ScanTool OBDLink MX Wi-Fi: OBD 配接器/診斷掃描器)]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[HockeyApp 入口網站]: https://rink.hockeyapp.org
[在 GitHub 上提出問題]: https://github.com/Azure-Samples/MyDriving/issues
