---
title: "aaaAzure Mobile Engagement 示範應用程式 |Microsoft 文件"
description: "說明何處 toodownload，toouse，與使用 Azure Mobile Engagement hello 優點示範應用程式"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: f624d5aa-254b-4ad0-96a3-f00e6c3a2c97
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2016
ms.author: piyushjo
ms.openlocfilehash: 9ff0df0d21e1bad6aff573db49304a55593df1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-demo-app"></a>Azure Mobile Engagement 示範應用程式
我們之前發行的 Azure Mobile Engagement 示範應用程式**iOS**， **Android**，和**Windows**平台 toohelp 您 toofind 實用資源和深入了解行動裝置參與。

hello 應用程式可協助您：

* 輕鬆地找到有用的連結 tooMobile Engagement 資源，例如視訊、 文件、 hello 支援論壇，並 toogo tooraise 功能要求的位置。
* Mobile Engagement tooget 意見，為您自己的行動應用程式所支援的經驗範例通知。
* 如何使用參考實作 toostudy tooimplement Mobile Engagement 到您自己的應用程式。 您可以學習如何：
  
  * 收集分析資料。
  * 實作例如「全螢幕插入」或「快顯」等類型的進階通知案例。
  * 實作問卷調查和投票。
  * 實作無訊息推播與資料推播案例。   

## <a name="app-installation"></a>應用程式安裝
此應用程式有下列應用程式市集的 hello:

* **Windows Universal 示範應用程式**
  
  * 下載 hello 應用程式在 hello [Windows 應用程式市集](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2)。
  * hello 應用程式是以 Windows 10 通用應用程式開發。 hello 原始程式碼位於[GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows)。
* **iOS 示範應用程式**：
  
  * 下載 hello 應用程式在 hello [Apple store](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090)。
  * hello 應用程式被開發 iOS Swift 中。 hello 原始程式碼位於[GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios)。
* **Android 示範應用程式**：
  
  * 下載 hello 應用程式在 hello [Google Play 商店](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement)。
  * hello 原始程式碼位於[GitHub](https://github.com/Azure/azure-mobile-engagement-app-android)。

![Windows Universal 示範應用程式][1]

![iOS 示範應用程式][2]
![Android 示範應用程式][3]

## <a name="usage"></a>使用量
您可以使用此應用程式中 hello 下列方法：

**下載您的裝置上的 hello 應用程式從 hello （稍早所提供） 的應用程式市集連結：**

> [!IMPORTANT]
> 您不需要 Azure 帳戶，或需要 tooconnect hello 應用程式 tooa 後端。 hello 應用程式的獨立運作。
> 
> 

* 在您的裝置上進行 hello 應用程式之後，您可以瀏覽 hello 左側功能表 toofind hello 實用資源有關 Mobile Engagement 中的 hello 連結。
* 我們已加入 hello[服務的 RSS 摘要](https://aka.ms/azmerssfeed)入此應用程式，讓您一律更新有關嗨最新產品更新。
* 您也可以瀏覽 hello 範例通知案例 tooexperience hello 類型的每個平台支援由 Mobile Engagement 的通知。 這些通知可 hello 通知體驗，也就是從 hello Mobile Engagement 平台的相同 toosending hello 通知您有本機-也就是說，您可以按一下 hello 上的按鈕 hello 螢幕 tooshow 經驗。

![Windows 版應用程式功能表][4]

![適用於 iOS 的應用程式功能表][5]
![適用於 Android 的應用程式功能表][6]

**從 hello （稍早所提供） 的 GitHub 連結下載 hello 原始程式碼：**

* 您已經下載 hello 原始程式碼之後，則會開啟適用於 iOS、 Android 和 Visual Studio for Windows 的 Android Studio XCode-hello 個別的開發環境中。
* 接下來應該遵循我們[基本 SDK 整合步驟](mobile-engagement-windows-store-dotnet-get-started.md)此應用程式 tooits，這樣您能 tooconnect 擁有 Mobile Engagement 後端執行個體。
  * 您需要 tooconfigure hello 應用程式中的連接字串。
  * 您也需要 tooconfigure hello 推播通知的平台應用程式。
* 您會發現該 hello 應用程式本身已檢測與 Mobile Engagement。 因此，當您開啟 hello 應用程式連接它 toohello 後端之後，您會無法 toosee hello 使用者工作階段、 活動、 事件和等等，在 [hello**監視器**] 索引標籤。
* 您也可以從您的 Mobile Engagement 執行個體，而不是使用本機通知可以 toosend 通知 toothis 應用程式。
  
  * 在此新增您的裝置做為測試裝置使用 hello **Get hello 裝置識別碼**hello 應用程式中的功能表項目。 此能提供您裝置識別碼，接著您會向平台後端執行個體註冊為測試裝置。
    
    ![Windows 上的裝置識別碼][7]
    
    ![在 iOS 上的裝置識別碼][8]
    ![在 Android 上的裝置識別碼][9]

## <a name="key-features-of-hello-demo-app"></a>Hello 示範應用程式的主要功能
* 如先前所述，與此應用程式，您的所有的 hello 資源 Mobile Engagement 手中。 Hello 左側功能表上，您可以瀏覽 hello 連結。
* 您可以體驗每種平台的應用程式外通知。 這些通知可以作為傳遞**僅限通知**、 其中按一下 hello 通知只會開啟 hello 應用程式的原生螢幕 (使用**深層連結**)-或**Web公告**，其中您可以提供其他 HTML 內容從 hello 回 Mobile Engagement 結束 toobe hello 通知按一下時顯示。
  
    ![應用程式外通知][29]
* 在 iOS 上，您必須 tooclose hello 應用程式 toosee hello 跨應用程式或系統推播通知。 您可以查看 hello 此處的實作新增**動作按鈕**，像 hello，應該是跨應用程式的通知加入的 toothis*意見反應*和*共用*（以便hello 使用者可以採取動作的權限本身 hello 通知）。
  
    ![iOS 上的應用程式外通知][11] ![在 iOS 上顯示的應用程式外通知][14]
* 在 Android 上，hello 選項支援加入多行文字 (**大文字**) 或通知映像 (**大圖片**) toohello 通知，以及 hello**動作按鈕**（如 ios 支援）。
  
    ![Android 上的應用程式外通知][12] ![在 Android 上顯示的應用程式外通知][15]
* 在 Windows 10 中，您可以看到 hello 通知 hello PC 上的樣子。 此通知也會出現在 Windows 10 hello**通知中心**。 不支援新增**動作按鈕**在 hello Windows SDK 中的 hello 時刻。
  
    ![Windows 上的應用程式外通知][10] ![Windows 上的應用程式外顯示][13]
* 您可以體驗每種平台的預設「應用程式內通知」。 這是兩個步驟的體驗，當中會先顯示 [通知] 視窗。 當您按一下它時，它會開啟全螢幕**公告**、 hello 下列螢幕擷取畫面所示。 這項公告 hello 內容來自於您的 Mobile Engagement 後端執行個體。 hello SDK 有 hello 範本通知和公告。 您可以輕鬆地自訂它們，hello 加入我們的標誌和色彩本示範應用程式中所示。  
  
    ![Windows 上的應用程式內通知][16]
  
    ![iOS 上的應用程式內通知][17]  ![Android 上的應用程式內通知][18]
  
    **iOS**、**Android**
* 您也可以使用 hello**類別**Mobile Engagement toocustomize 的功能，此預設體驗。 Hello 示範應用程式，我們已經示範兩個常用方式 toochange hello 體驗的 hello 通知。 請注意該 hello 類別功能尚未支援 hello Windows SDK 中。
  
    **全螢幕插入：**
  
    ![應用程式內通知 - 插入類別][30]
  
    ![iOS 上的插入類別][21]     ![Android 上的插入類別][22]
  
    **快顯通知：**
  
    ![應用程式內通知 - 快顯類別][31]
  
    ![iOS 上的快顯通知][19]    ![Android 上的快顯通知][20]

**iOS**、**Android**

* Mobile Engagement 也支援特殊類型的應用程式內通知，稱為 **投票**。 這可讓您快速問卷調查 tooyour 分割應用程式使用者 toosend。 您可以將問題和選項，針對每個問題，如下列螢幕擷取畫面的 hello 所示。 這就取得顯示應用程式內通知 toohello 應用程式使用者的身分。   
  
    ![輪詢通知][32]
  
    ![Windows 上的問卷調查][26]
  
    ![iOS 上的問卷調查][27]   ![Android 上的問卷調查][28]

**iOS**、**Android**

* Mobile Engagement 也支援傳送無聲 **資料推送** 通知。 您可以利用這些通知，傳送資料從您的服務 （例如 hello JSON 資料 hello 下列範例中），您可以在您的應用程式中處理，並採取某些動作。 例如，方式變更的項目 hello 價格選擇性地使用資料推播通知。
  
    ![資料推送通知推播通知][33]
  
    ![Windows 上的資料推送通知][23]
  
    ![iOS 上的資料推送通知][24]  ![Android 上的資料推送通知][25]

**iOS**、**Android**

> [!NOTE]
> 按一下即可檢視詳細的逐步指示，針對任何這些通知**的指示，請按一下這裡 toosend Mobile Engagement 平台的這些通知**任何範例通知螢幕上。
> 
> 

[1]: ./media/mobile-engagement-demo-apps/home-windows.png
[2]: ./media/mobile-engagement-demo-apps/home-ios.png
[3]: ./media/mobile-engagement-demo-apps/home-android.png
[4]: ./media/mobile-engagement-demo-apps/menu-windows.png
[5]: ./media/mobile-engagement-demo-apps/menu-ios.png
[6]: ./media/mobile-engagement-demo-apps/menu-android.png
[7]: ./media/mobile-engagement-demo-apps/device-id-windows.png
[8]: ./media/mobile-engagement-demo-apps/device-id-ios.png
[9]: ./media/mobile-engagement-demo-apps/device-id-android.png
[10]: ./media/mobile-engagement-demo-apps/out-of-app-windows.png
[11]: ./media/mobile-engagement-demo-apps/out-of-app-ios.png
[12]: ./media/mobile-engagement-demo-apps/out-of-app-android.png
[13]: ./media/mobile-engagement-demo-apps/out-of-app-display-windows.png
[14]: ./media/mobile-engagement-demo-apps/out-of-app-display-ios.png
[15]: ./media/mobile-engagement-demo-apps/out-of-app-display-android.png
[16]: ./media/mobile-engagement-demo-apps/in-app-windows.png
[17]: ./media/mobile-engagement-demo-apps/in-app-ios.png
[18]: ./media/mobile-engagement-demo-apps/in-app-android.png
[19]: ./media/mobile-engagement-demo-apps/pop-up-ios.png
[20]: ./media/mobile-engagement-demo-apps/pop-up-android.png
[21]: ./media/mobile-engagement-demo-apps/interstitial-ios.png
[22]: ./media/mobile-engagement-demo-apps/interstitial-android.png
[23]: ./media/mobile-engagement-demo-apps/data-push-windows.png
[24]: ./media/mobile-engagement-demo-apps/data-push-ios.png
[25]: ./media/mobile-engagement-demo-apps/data-push-android.png
[26]: ./media/mobile-engagement-demo-apps/survey-windows.png
[27]: ./media/mobile-engagement-demo-apps/survey-ios.png
[28]: ./media/mobile-engagement-demo-apps/survey-android.png
[29]: ./media/mobile-engagement-demo-apps/out-of-app.png
[30]: ./media/mobile-engagement-demo-apps/in-app-interstitial.png
[31]: ./media/mobile-engagement-demo-apps/in-app-pop-up.png
[32]: ./media/mobile-engagement-demo-apps/notification-poll.png
[33]: ./media/mobile-engagement-demo-apps/notification-data-push.png
