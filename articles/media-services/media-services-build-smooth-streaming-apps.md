---
title: "aaaSmooth Streaming Windows 市集應用程式教學課程 |Microsoft 文件"
description: "了解 toouse Azure Media Services toocreate XML MediaElement 的 C# Windows 市集應用程式如何控制 tooplayback Smooth Streaming 內容。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0fa5d8c5-3d5f-4886-ae55-fb6de4f5256d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: juliako
ms.openlocfilehash: b02aa2c7f68fe22a23ea846d72fdd23bfba2b19c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a>如何 tooBuild Smooth Streaming Windows 市集應用程式

hello Smooth Streaming Client SDK for Windows 8 可讓開發人員 toobuild Windows 市集應用程式可以播放隨選及即時的 Smooth Streaming 內容。 此外 toohello 基本播放的 Smooth Streaming 內容，hello SDK 也提供豐富的功能，例如 Microsoft PlayReady 保護，品質等級的限制，Live DVR、 切換、 狀態更新 （例如品質等級變更為接聽的音訊資料流) 和錯誤事件，等等。 Hello 支援功能的詳細資訊，請參閱 hello[版本資訊](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes)。 如需詳細資訊，請參閱 [Player Framework for Windows 8](http://playerframework.codeplex.com/)。 

本教學課程包含四個課程：

1. 建立基本的 Smooth Streaming 市集應用程式
2. 將滑桿 tooControl hello 媒體進度列
3. 選取 Smooth Streaming 資料流
4. 選取 Smooth Streaming 曲目

## <a name="prerequisites"></a>必要條件
* Windows 8 32 位元或 64 位元。 您可以從 MSDN 取得 [Windows 8 Enterprise 評估版](http://msdn.microsoft.com/evalcenter/jj554510.aspx) 。
* Visual Studio 2012 或 Visual Studio Express 2012 (或更新版本)。 您可以取得從 hello 試用版[這裡](http://www.microsoft.com/visualstudio/11/downloads)。
* [Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home)(英文)。

您可以從 MSDN 開發人員程式碼範例 （程式碼庫） 下載完成 hello 方案，每個單元： 

* [課程 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - 簡單 Windows 8 Smooth Streaming Media Player， 
* [課程 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - 具有滑動軸控制項的簡單 Windows 8 Smooth Streaming Media Player， 
* [課程 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - 具有串流選擇的 Windows 8 Smooth Streaming Media Player，  
* [課程 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) - 具有追蹤選擇的 Windows 8 Smooth Streaming Media Player。

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a>課程 1：建立基本的 Smooth Streaming 市集應用程式

在這一課，您將建立 Windows 市集應用程式使用 MediaElement 控制項 tooplay Smooth Streaming 內容。  hello 執行的應用程式看起來像：

![Smooth Streaming Windows Store application example][PlayerApplication]

如需關於開發 Windows 市集應用程式的詳細資訊，請參閱 [開發 Windows 8 適用的好用應用程式](http://msdn.microsoft.com/windows/apps/br229512.aspx)。 這一課包含下列程序的 hello:

1. 建立 Windows 市集專案
2. 設計 hello 使用者介面 (XAML)
3. 修改 hello 程式碼後置檔案
4. 編譯和測試 hello 應用程式

**toocreate 的 Windows 市集專案**

1. 執行 Visual Studio 2012 或更新版本。
2. 從 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。
3. Hello 新增專案 對話方塊，從類型或選取 hello 下列值：

| 名稱 | 值 |
| --- | --- |
| 範本群組 |已安裝/範本/Visual C#/Windows 市集 |
| 範本 |空白應用程式 (XAML) |
| 名稱 |SSPlayer |
| 位置 |C:\SSTutorials |
| 方案名稱 |SSPlayer |
| 為方案建立目錄 |(已選取) |

1. 按一下 [確定] 。

**tooadd 參考 toohello Smooth Streaming Client SDK**

1. 從 方案總管 中，在 SSPlayer 上按一下滑鼠右鍵，然後按一下加入參考。
2. 輸入或選取下列值的 hello:

| 名稱 | 值 |
| --- | --- |
| 參考群組 |Windows/延伸 |
| 參考 |選取 Microsoft Smooth Streaming Client SDK for Windows 8 和 Microsoft Visual C++ Runtime Package |

1. 按一下 [確定] 。 

在新增之後 hello 參考，您必須選取 hello 目標平台 （x64 或 x86），將參考加入並不適用於任何 CPU 平台組態。  在方案總管中，您會看到這些加入的參考具有黃色警告標記。

**toodesign hello 播放程式使用者介面**

1. 在 [方案總管] 中，按兩下**MainPage.xaml** tooopen 在 hello 設計檢視。
2. 找出 hello **&lt;方格&gt;**和 **&lt;/Grid&gt;** 標記 hello XAML 檔案，並貼上 hello 下列程式碼之間 hello 兩個標記：

         <Grid.RowDefinitions>

            <RowDefinition Height="20"/>    <!-- spacer -->
            <RowDefinition Height="50"/>    <!-- media controls -->
            <RowDefinition Height="100*"/>  <!-- media element -->
            <RowDefinition Height="80*"/>   <!-- media stream and track selection -->
            <RowDefinition Height="50"/>    <!-- status bar -->
         </Grid.RowDefinitions>

         <StackPanel Name="spMediaControl" Grid.Row="1" Orientation="Horizontal">
            <TextBlock x:Name="tbSource" Text="Source :  " FontSize="16" FontWeight="Bold" VerticalAlignment="Center" />
            <TextBox x:Name="txtMediaSource" Text="http://ecn.channel9.msdn.com/o9/content/smf/smoothcontent/elephantsdream/Elephants_Dream_1024-h264-st-aac.ism/manifest" FontSize="10" Width="700" Margin="0,4,0,10" />
            <Button x:Name="btnSetSource" Content="Set Source" Width="111" Height="43" Click="btnSetSource_Click"/>
            <Button x:Name="btnPlay" Content="Play" Width="111" Height="43" Click="btnPlay_Click"/>
            <Button x:Name="btnPause" Content="Pause"  Width="111" Height="43" Click="btnPause_Click"/>
            <Button x:Name="btnStop" Content="Stop"  Width="111" Height="43" Click="btnStop_Click"/>
            <CheckBox x:Name="chkAutoPlay" Content="Auto Play" Height="55" Width="Auto" IsChecked="{Binding AutoPlay, ElementName=mediaElement, Mode=TwoWay}"/>
            <CheckBox x:Name="chkMute" Content="Mute" Height="55" Width="67" IsChecked="{Binding IsMuted, ElementName=mediaElement, Mode=TwoWay}"/>
         </StackPanel>

         <StackPanel Name="spMediaElement" Grid.Row="2" Height="435" Width="1072"
                    HorizontalAlignment="Center" VerticalAlignment="Center">
            <MediaElement x:Name="mediaElement" Height="356" Width="924" MinHeight="225"
                          HorizontalAlignment="Center" VerticalAlignment="Center" 
                          AudioCategory="BackgroundCapableMedia" />
            <StackPanel Orientation="Horizontal">
                <Slider x:Name="sliderProgress" Width="924" Height="44"
                        HorizontalAlignment="Center" VerticalAlignment="Center"
                        PointerPressed="sliderProgress_PointerPressed"/>
                <Slider x:Name="sliderVolume" 
                        HorizontalAlignment="Right" VerticalAlignment="Center" Orientation="Vertical" 
                        Height="79" Width="148" Minimum="0" Maximum="1" StepFrequency="0.1" 
                        Value="{Binding Volume, ElementName=mediaElement, Mode=TwoWay}" 
                        ToolTipService.ToolTip="{Binding Value, RelativeSource={RelativeSource Mode=Self}}"/>
            </StackPanel>
         </StackPanel>

         <StackPanel Name="spStatus" Grid.Row="4" Orientation="Horizontal">
            <TextBlock x:Name="tbStatus" Text="Status :  " 
               FontSize="16" FontWeight="Bold" VerticalAlignment="Center" HorizontalAlignment="Center" />
            <TextBox x:Name="txtStatus" FontSize="10" Width="700" VerticalAlignment="Center"/>
         </StackPanel>
   
   hello MediaElement 控制項是使用的 tooplayback 媒體。 名為 sliderProgress hello 滑桿控制項將使用 hello 下一個課程 toocontrol hello 媒體進行中。
3. 按**CTRL + S** toosave hello 檔案。

hello MediaElement 控制項不支援 Smooth Streaming 內容的現成。 tooenable hello Smooth Streaming 支援，您必須註冊 hello Smooth Streaming 位元組資料流的副檔名與 MIME 類型的處理常式。  tooregister，您可以使用 hello MediaExtensionManager.RegisterByteStremHandler 方法 hello Windows.Media 命名空間。

在此 XAML 檔案中，某些事件處理常式會與 hello 控制項相關聯。  您必須定義那些事件處理常式。

**toomodify hello 的程式碼後置檔案**

1. 從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視程式碼。
2. 在 hello hello 檔案頂端，加入 hello 下列 using 陳述式：
   
        using Windows.Media;
3. 在 hello hello 開頭**MainPage**類別中，加入下列資料成員的 hello:
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. 結尾 hello hello **MainPage**建構函式，新增下列兩行 hello:
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. 結尾 hello hello **MainPage**類別中，貼上下列程式碼的 hello:
   
         # region UI Button Click Events
         private void btnPlay_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Play();
         txtStatus.Text = "MediaElement is playing ...";
         }
         private void btnPause_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Pause();
         txtStatus.Text = "MediaElement is paused";
         }
         private void btnSetSource_Click(object sender, RoutedEventArgs e)
         {

         sliderProgress.Value = 0;
         mediaElement.Source = new Uri(txtMediaSource.Text);

         if (chkAutoPlay.IsChecked == true)
         {
             txtStatus.Text = "MediaElement is playing ...";
         }
         else
         {
             txtStatus.Text = "Click hello Play button tooplay hello media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek tooposition " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

hello sliderProgress_PointerPressed 事件處理常式是此處所定義。  有多個 works toodo tooget 它運作，這會涵蓋 hello 這個教學課程的下一課。
6. 按**CTRL + S** toosave hello 檔案。

hello 完成的 hello 程式碼後置檔案應該看起來像這樣：

![Codeview in Visual Studio of Smooth Streaming Windows Store application][CodeViewPic]

**toocompile 和測試 hello 應用程式**

1. 從 hello**建置**功能表上，按一下  **Configuration Manager**。
2. 變更**作用中的方案平台**toomatch 開發平台。
3. 按**F6** toocompile hello 專案。 
4. 按**F5** toorun hello 應用程式。
5. 在 hello 頂端 hello 應用程式，您可以使用預設的 hello Smooth Streaming URL，或輸入另一個。 
6. 按一下 [設定來源] 。 因為**自動播放**hello 應該自動播放媒體，預設會啟用。  您可以控制 hello 媒體使用 hello**播放**，**暫停**和**停止**按鈕。  您可以控制使用 hello 垂直滑桿 hello 媒體磁碟區。  不過 hello 水平滑桿控制 hello 媒體進行完全尚未實作。 

您已完成課程 1。  在這一課，您可以使用 MediaElement 控制項 tooplayback Smooth Streaming 內容。  Hello 下一課，您會加入滑桿 toocontrol hello 進度的 hello Smooth Streaming 內容。

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a>第 2 課： 加入滑桿 tooControl hello 媒體進度列

在第 1 課中，您可以建立 Windows 市集應用程式使用 MediaElement XAML 控制項 tooplayback Smooth Streaming 媒體內容。  它包含一些基本媒體功能 (例如啟動、停止和暫停)。  在這一課，您會加入滑桿列控制項 toohello 應用程式。

在本教學課程中，我們將使用計時器 tooupdate hello 鎏  彸依據 hello 的 hello MediaElement 控制項目前的位置。  hello 滑桿開始和結束時間也需要 toobe 更新發生實況內容。  這可以 hello 適應性來源更新事件中進一步處理。

媒體來源是一種產生媒體資料的物件。  hello 來源解析程式會採用 URL 或位元組資料流，並建立該內容的 hello 適當的媒體來源。  hello 來源解析程式是 hello hello 應用程式 toocreate 媒體來源的標準方式。 

這一課包含下列程序的 hello:

1. 註冊 hello Smooth Streaming 的處理常式 
2. 加入 hello 適應性來源管理員層級的事件處理常式
3. 加入 hello 適應性來源層級的事件處理常式
4. 新增 MediaElement 事件處理常式
5. 新增滑動軸相關程式碼
6. 編譯和測試 hello 應用程式

**tooregister hello Smooth Streaming 位元組資料流處理常式，並傳入 hello propertyset**

1. 從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視程式碼。
2. 在 hello hello 檔案開頭，加入 hello 下列 using 陳述式：

        using Microsoft.Media.AdaptiveStreaming;
3. 在 MainPage 類別 hello hello 開頭，加入下列資料成員的 hello:

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. 內部 hello **MainPage**建構函式，加入下列程式碼之後 hello hello**這。初始化 Components();**行與 hello 上一課中寫入 hello 註冊程式碼行：

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. 內部 hello **MainPage**建構函式，修改 hello 兩 RegisterByteStreamHandler 方法 tooadd hello 制定參數：

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass hello propertyset. 
         // http://*.ism/manifest URI resources will be resolved by Byte-stream handler.
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "text/xml", 
            propertySet );
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "application/vnd.ms-sstr+xml", 
         propertySet);
6. 按**CTRL + S** toosave hello 檔案。

**tooadd hello 適應性來源管理員層級的事件處理常式**

1. 從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視程式碼。
2. 內部 hello **MainPage**類別中，加入下列資料成員的 hello:
   
     private AdaptiveSource adaptiveSource = null;
3. 結尾 hello hello **MainPage**類別中，新增下列事件處理常式的 hello:
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. 結尾 hello hello **MainPage**建構函式，加入下列行 toosubscribe toohello 彈性的來源開啟事件 hello:
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. 按**CTRL + S** toosave hello 檔案。

**tooadd 適應性來源層級的事件處理常式**

1. 從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視程式碼。
2. 內部 hello **MainPage**類別中，加入下列資料成員的 hello:
   
     private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;
3. 結尾 hello hello **MainPage**類別中，新增下列事件處理常式的 hello:

         # region Adaptive Source Level Events
         private void mediaElement_ManifestReady(AdaptiveSource sender, ManifestReadyEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
            manifestObject = args.AdaptiveSource.Manifest;
         }

         private void mediaElement_AdaptiveSourceStatusUpdated(AdaptiveSource sender, AdaptiveSourceStatusUpdatedEventArgs args)
         {

            adaptiveSourceStatusUpdate = args;
         }

         private void mediaElement_AdaptiveSourceFailed(AdaptiveSource sender, AdaptiveSourceFailedEventArgs args)
         {

            txtStatus.Text = "Error: " + args.HttpResponse;
         }

         # endregion Adaptive Source Level Events
4. 結尾 hello hello **mediaElement AdaptiveSourceOpened**方法，加入下列程式碼 toosubscribe toohello 事件 hello:
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. 按**CTRL + S** toosave hello 檔案。

hello 相同事件可用的自動調整來源 manger 層級，也可以用於處理功能一般 tooall 媒體中的項目 hello 應用程式。 每個 AdaptiveSource 都包含自己專屬的事件，而且所有 AdaptiveSource 事件都會在 AdaptiveSourceManager 下階層式列出。

**tooadd 媒體項目事件處理常式**

1. 從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視程式碼。
2. 結尾 hello hello **MainPage**類別中，新增下列事件處理常式的 hello:

         # region Media Element Event Handlers
         private void MediaOpened(object sender, RoutedEventArgs e)
         {

            txtStatus.Text = "MediaElement opened";
         }

         private void MediaFailed(object sender, ExceptionRoutedEventArgs e)
         {

            txtStatus.Text= "MediaElement failed: " + e.ErrorMessage;
         }

         private void MediaEnded(object sender, RoutedEventArgs e)
         {

            txtStatus.Text ="MediaElement ended.";
         }

         # endregion Media Element Event Handlers
3. 結尾 hello hello **MainPage**建構函式，加入下列程式碼 toosubscript toohello 事件 hello:

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. 按**CTRL + S** toosave hello 檔案。

**tooadd 滑桿列相關的程式碼**

1. 從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視程式碼。
2. 在 hello hello 檔案開頭，加入 hello 下列 using 陳述式：
      
        using Windows.UI.Core;
3. 內部 hello **MainPage**類別中，加入下列資料成員的 hello:
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. 結尾 hello hello **MainPage**建構函式，加入下列程式碼的 hello:
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. 結尾 hello hello **MainPage**類別中，加入下列程式碼的 hello:

         # region sliderMediaPlayer
         private double SliderFrequency(TimeSpan timevalue)
         {

            long absvalue = 0;
            double stepfrequency = -1;

            if (manifestObject != null)
            {
                absvalue = manifestObject.Duration - (long)manifestObject.StartTime;
            }
            else
            {
                absvalue = mediaElement.NaturalDuration.TimeSpan.Ticks;
            }

            TimeSpan totalDVRDuration = new TimeSpan(absvalue);

            if (totalDVRDuration.TotalMinutes >= 10 && totalDVRDuration.TotalMinutes < 30)
            {
               stepfrequency = 10;
            }
            else if (totalDVRDuration.TotalMinutes >= 30 
                     && totalDVRDuration.TotalMinutes < 60)
            {
                stepfrequency = 30;
            }
            else if (totalDVRDuration.TotalHours >= 1)
            {
                stepfrequency = 60;
            }

            return stepfrequency;
         }

         void updateSliderPositionoNTicks(object sender, object e)
         {

            sliderProgress.Value = mediaElement.Position.TotalSeconds;
         }

         public void setupTimer()
         {

            sliderPositionUpdateDispatcher = new DispatcherTimer();
            sliderPositionUpdateDispatcher.Interval = new TimeSpan(0, 0, 0, 0, 300);
            startTimer();
         }

         public void startTimer()
         {

            sliderPositionUpdateDispatcher.Tick += updateSliderPositionoNTicks;
            sliderPositionUpdateDispatcher.Start();
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderStartTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.StartTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Minimum = absvalue;
            });
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderEndTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Maximum = absvalue;
            });
         }

         # endregion sliderMediaPlayer
      
>[!NOTE]
>CoreDispatcher 是使用的 toomake toohello UI 執行緒從非 UI 執行緒的變更。 如果發送器執行緒上的瓶頸，開發人員可以選擇 toouse 發送器提供 UI 項目最初打算 tooupdate。  例如：
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. 結尾 hello hello **mediaElement_AdaptiveSourceStatusUpdated**方法，加入下列程式碼的 hello:

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. 結尾 hello hello **MediaOpened**方法，加入下列程式碼的 hello:

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. 按**CTRL + S** toosave hello 檔案。

**toocompile 和測試 hello 應用程式**

1. 按**F6** toocompile hello 專案。 
2. 按**F5** toorun hello 應用程式。
3. 在 hello 頂端 hello 應用程式，您可以使用預設的 hello Smooth Streaming URL，或輸入另一個。 
4. 按一下 [設定來源] 。 
5. 測試 hello 滑動軸。

您已完成課程 2。  在這一課，您會加入滑桿 tooapplication。 

## <a name="lesson-3-select-smooth-streaming-streams"></a>課程 3：選取 Smooth Streaming 資料流
Smooth Streaming 是能夠 toostream 內容都是由 hello 檢視器可選取多個語言音訊音軌。  在這一課，您將啟用檢視器 tooselect 資料流。 這一課包含下列程序的 hello:

1. 修改 hello XAML 檔案
2. 修改 hello 碼 behand 檔案
3. 編譯和測試 hello 應用程式

**toomodify hello XAML 檔案**

1. 從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視設計工具。
2. 找出&lt;Grid.RowDefinitions&gt;，並讓它們看起來像是修改 hello RowDefinitions:
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. 內部 hello&lt;方格&gt;&lt;/Grid&gt;標記，可讓您新增 hello 下列程式碼 toodefine listbox 控制項，讓使用者可以看到 hello 份可用的資料流，並選取資料流：

         <Grid Name="gridStreamAndBitrateSelection" Grid.Row="3">
            <Grid.RowDefinitions>
                <RowDefinition Height="300"/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="250*"/>
                <ColumnDefinition Width="250*"/>
            </Grid.ColumnDefinitions>
            <StackPanel Name="spStreamSelection" Grid.Row="1" Grid.Column="0">
                <StackPanel Orientation="Horizontal">
                    <TextBlock Name="tbAvailableStreams" Text="Available Streams:" FontSize="16" VerticalAlignment="Center"></TextBlock>
                    <Button Name="btnChangeStreams" Content="Submit" Click="btnChangeStream_Click"/>
                </StackPanel>
                <ListBox x:Name="lbAvailableStreams" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                    ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
                    <ListBox.ItemTemplate>
                        <DataTemplate>
                            <CheckBox Content="{Binding Name}" IsChecked="{Binding isChecked, Mode=TwoWay}" />
                        </DataTemplate>
                    </ListBox.ItemTemplate>
                </ListBox>
            </StackPanel>
         </Grid>
4. 按**CTRL + S** toosave hello 變更。

**toomodify hello 的程式碼後置檔案**

1. 從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視程式碼。
2. 在 hello SSPlayer 命名空間中，加入新的類別：
   
        #region class Stream
   
        public class Stream
        {
            private IManifestStream stream;
            public bool isCheckedValue;
            public string name;
   
            public string Name
            {
                get { return name; }
                set { name = value; }
            }
   
            public IManifestStream ManifestStream
            {
                get { return stream; }
                set { stream = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    // mMke hello video stream always checked.
                    if (stream.Type == MediaStreamType.Video)
                    {
                        isCheckedValue = true;
                    }
                    else
                    {
                        isCheckedValue = value;
                    }
                }
            }
   
            public Stream(IManifestStream streamIn)
            {
                stream = streamIn;
                name = stream.Name;
            }
        }
        #endregion class Stream
3. 在 MainPage 類別 hello hello 開頭，加入下列變數定義的 hello:
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. 在 hello MainPage 類別中，加入下列區域的 hello:
   
        #region stream selection
        ///<summary>
        ///Functionality tooselect streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from hello mediaElement_ManifestReady event handler 
        // tooretrieve hello streams and populate them toohello local data members.
        public void getStreams(Manifest manifestObject)
        {
            availableStreams = new List<Stream>();
            availableVideoStreams = new List<Stream>();
            availableAudioStreams = new List<Stream>();
            availableTextStreams = new List<Stream>();
   
            try
            {
                for (int i = 0; i<manifestObject.AvailableStreams.Count; i++)
                {
                    Stream newStream = new Stream(manifestObject.AvailableStreams[i]);
                    newStream.isChecked = false;
   
                    //populate hello stream lists based on hello types
                    availableStreams.Add(newStream);
   
                    switch (newStream.ManifestStream.Type)
                    {
                        case MediaStreamType.Video:
                            availableVideoStreams.Add(newStream);
                            break;
                        case MediaStreamType.Audio:
                            availableAudioStreams.Add(newStream);
                            break;
                        case MediaStreamType.Text:
                            availableTextStreams.Add(newStream);
                            break;
                    }
   
                    // Select hello default selected streams from hello manifest.
                    for (int j = 0; j<manifestObject.SelectedStreams.Count; j++)
                    {
                        string selectedStreamName = manifestObject.SelectedStreams[j].Name;
                        if (selectedStreamName.Equals(newStream.Name))
                        {
                            newStream.isChecked = true;
                            break;
                        }
                    }
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function set hello list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update hello stream check box list on hello UI
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableStreams.ItemsSource = availableStreams; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function creates a selected streams list
        private void createSelectedStreamsList(List<IManifestStream> selectedStreams)
        {
            bool isOneVideoSelected = false;
            bool isOneAudioSelected = false;
   
            // Only one video stream can be selected
            for (int j = 0; j<availableVideoStreams.Count; j++)
            {
                if (availableVideoStreams[j].isChecked && (!isOneVideoSelected))
                {
                    selectedStreams.Add(availableVideoStreams[j].ManifestStream);
                    isOneVideoSelected = true;
                }
            }
   
            // Select hello frist video stream from hello list if no video stream is selected
            if (!isOneVideoSelected)
            {
                availableVideoStreams[0].isChecked = true;
                selectedStreams.Add(availableVideoStreams[0].ManifestStream);
            }
   
            // Only one audio stream can be selected
            for (int j = 0; j<availableAudioStreams.Count; j++)
            {
                if (availableAudioStreams[j].isChecked && (!isOneAudioSelected))
                {
                    selectedStreams.Add(availableAudioStreams[j].ManifestStream);
                    isOneAudioSelected = true;
                    txtStatus.Text = "hello audio stream is changed too" + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select hello frist audio stream from hello list if no audio steam is selected.
            if (!isOneAudioSelected)
            {
                availableAudioStreams[0].isChecked = true;
                selectedStreams.Add(availableAudioStreams[0].ManifestStream);
            }
   
            // Multiple text streams are supported.
            for (int j = 0; j < availableTextStreams.Count; j++)
            {
                if (availableTextStreams[j].isChecked)
                {
                    selectedStreams.Add(availableTextStreams[j].ManifestStream);
                }
            }
        }
   
        // Change streams on a smooth streaming presentation with multiple video streams.
        private async void changeStreams(List<IManifestStream> selectStreams)
        {
            try
            {
                IReadOnlyList<IStreamChangedResult> returnArgs =
                    await manifestObject.SelectStreamsAsync(selectStreams);
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
        #endregion stream selection
5. 找出 hello mediaElement_ManifestReady 方法，請新增下列程式碼中的 hello 函式的 hello 結尾 hello:
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    因此就緒 MediaElement 資訊清單時，hello 程式碼取得一份 hello 可用的資料流，並於其中填入 hello 清單 hello UI 清單方塊。
6. 內部 hello MainPage 類別中，找出 hello UI 按鈕按一下事件地區，然後再加入下列函式定義的 hello:
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

**toocompile 和測試 hello 應用程式**

1. 按**F6** toocompile hello 專案。 
2. 按**F5** toorun hello 應用程式。
3. 在 hello 頂端 hello 應用程式，您可以使用預設的 hello Smooth Streaming URL，或輸入另一個。 
4. 按一下 [設定來源] 。 
5. hello 預設語言為 audio_eng。 請嘗試 tooswitch audio_eng 和 audio_es 之間。 每當，選取新的資料流，您必須按一下 hello 送出按鈕。

您已完成課程 3。  在這一課，您可以將 hello 功能 toochoose 資料流。

## <a name="lesson-4-select-smooth-streaming-tracks"></a>課程 4：選取 Smooth Streaming 曲目
Smooth Streaming 簡報可以包含多個以不同品質等級 (位元速率) 和解析度編碼的視訊檔案。 在這一課，您將啟用使用者 tooselect 追蹤。 這一課包含下列程序的 hello:

1. 修改 hello XAML 檔案
2. 修改 hello 碼 behand 檔案
3. 編譯和測試 hello 應用程式

**toomodify hello XAML 檔案**

1. 從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視設計工具。
2. 找出 hello&lt;方格&gt;hello 名稱標記**gridStreamAndBitrateSelection**，新增下列程式碼結尾 hello hello 標記 hello:
   
         <StackPanel Name="spBitRateSelection" Grid.Row="1" Grid.Column="1">
         <StackPanel Orientation="Horizontal">
             <TextBlock Name="tbBitRate" Text="Available Bitrates:" FontSize="16" VerticalAlignment="Center"/>
             <Button Name="btnChangeTracks" Content="Submit" Click="btnChangeTrack_Click" />
         </StackPanel>
         <ListBox x:Name="lbAvailableVideoTracks" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                  ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
             <ListBox.ItemTemplate>
                 <DataTemplate>
                     <CheckBox Content="{Binding Bitrate}" IsChecked="{Binding isChecked, Mode=TwoWay}"/>
                 </DataTemplate>
             </ListBox.ItemTemplate>
         </ListBox>
         </StackPanel>
3. 按**CTRL + S** toosave 他變更

**toomodify hello 的程式碼後置檔案**

1. 從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視程式碼。
2. 在 hello SSPlayer 命名空間中，加入新的類別：
   
        #region class Track
        public class Track
        {
            private IManifestTrack trackInfo;
            public string _bitrate;
            public bool isCheckedValue;
   
            public IManifestTrack TrackInfo
            {
                get { return trackInfo; }
                set { trackInfo = value; }
            }
   
            public string Bitrate
            {
                get { return _bitrate; }
                set { _bitrate = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    isCheckedValue = value;
                }
            }
   
            public Track(IManifestTrack trackInfoIn)
            {
                trackInfo = trackInfoIn;
                _bitrate = trackInfoIn.Bitrate.ToString();
            }
            //public Track() { }
        }
        #endregion class Track
3. 在 MainPage 類別 hello hello 開頭，加入下列變數定義的 hello:
   
        private List<Track> availableTracks;
4. 在 hello MainPage 類別中，加入下列區域的 hello:
   
        #region track selection
        /// <summary>
        /// Functionality tooselect video streams
        /// </summary>
   
        /// This Function gets hello tracks for hello selected video stream
        public void getTracks(Manifest manifestObject)
        {
            availableTracks = new List<Track>();
   
            IManifestStream videoStream = getVideoStream();
            IReadOnlyList<IManifestTrack> availableTracksLocal = videoStream.AvailableTracks;
            IReadOnlyList<IManifestTrack> selectedTracksLocal = videoStream.SelectedTracks;
   
            try
            {
                for (int i = 0; i < availableTracksLocal.Count; i++)
                {
                    Track thisTrack = new Track(availableTracksLocal[i]);
                    thisTrack.isChecked = true;
   
                    for (int j = 0; j < selectedTracksLocal.Count; j++)
                    {
                        string selectedTrackName = selectedTracksLocal[j].Bitrate.ToString();
                        if (selectedTrackName.Equals(thisTrack.Bitrate))
                        {
                            thisTrack.isChecked = true;
                            break;
                        }
                    }
                    availableTracks.Add(thisTrack);
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = e.Message;
            }
        }
   
        // This function gets hello video stream that is playing
        private IManifestStream getVideoStream()
        {
            IManifestStream videoStream = null;
            for (int i = 0; i < manifestObject.SelectedStreams.Count; i++)
            {
                if (manifestObject.SelectedStreams[i].Type == MediaStreamType.Video)
                {
                    videoStream = manifestObject.SelectedStreams[i];
                    break;
                }
            }
            return videoStream;
        }
   
        // This function set hello UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update hello track check box list on hello UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of hello selected tracks.
        private void createSelectedTracksList(List<IManifestTrack> selectedTracks)
        {
            // Create a list of selected tracks
            for (int j = 0; j < availableTracks.Count; j++)
            {
                if (availableTracks[j].isCheckedValue == true)
                {
                    selectedTracks.Add(availableTracks[j].TrackInfo);
                }
            }
        }
   
        // This function selects hello tracks based on user selection 
        private void changeTracks(List<IManifestTrack> selectedTracks)
        {
            IManifestStream videoStream = getVideoStream();
            try
            {
                videoStream.SelectTracks(selectedTracks);
            }
            catch (Exception ex)
            {
                txtStatus.Text = ex.Message;
            }
        }
        #endregion track selection
5. 找出 hello mediaElement_ManifestReady 方法，請新增下列程式碼中的 hello 函式的 hello 結尾 hello:
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. 內部 hello MainPage 類別中，找出 hello UI 按鈕按一下事件地區，然後再加入下列函式定義的 hello:
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

**toocompile 和測試 hello 應用程式**

1. 按**F6** toocompile hello 專案。 
2. 按**F5** toorun hello 應用程式。
3. 在 hello 頂端 hello 應用程式，您可以使用預設的 hello Smooth Streaming URL，或輸入另一個。 
4. 按一下 [設定來源] 。 
5. 根據預設，會選取所有 hello 曲目 hello 視訊資料流。 tooexperiment hello 位元速率的變更，您可以選取 hello 最低位元速率，，然後選取 hello 最高的位元速率可用。 您必須在每次變更之後按一下 [提交]。  您可以看到 hello 視訊品質的變更。

您已完成課程 4。  在這一課，您可以將 hello 功能 toochoose 追蹤。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a>其他資源：
* [如何 toobuild Smooth Streaming Windows 8 JavaScript 應用程式與進階功能](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [Smooth Streaming 技術概觀 (英文)](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

