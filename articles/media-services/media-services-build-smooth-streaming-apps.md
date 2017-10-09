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
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="ef940-103">如何 tooBuild Smooth Streaming Windows 市集應用程式</span><span class="sxs-lookup"><span data-stu-id="ef940-103">How tooBuild a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="ef940-104">hello Smooth Streaming Client SDK for Windows 8 可讓開發人員 toobuild Windows 市集應用程式可以播放隨選及即時的 Smooth Streaming 內容。</span><span class="sxs-lookup"><span data-stu-id="ef940-104">hello Smooth Streaming Client SDK for Windows 8 enables developers toobuild Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="ef940-105">此外 toohello 基本播放的 Smooth Streaming 內容，hello SDK 也提供豐富的功能，例如 Microsoft PlayReady 保護，品質等級的限制，Live DVR、 切換、 狀態更新 （例如品質等級變更為接聽的音訊資料流) 和錯誤事件，等等。</span><span class="sxs-lookup"><span data-stu-id="ef940-105">In addition toohello basic playback of Smooth Streaming content, hello SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="ef940-106">Hello 支援功能的詳細資訊，請參閱 hello[版本資訊](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes)。</span><span class="sxs-lookup"><span data-stu-id="ef940-106">For more information of hello supported features, see hello [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="ef940-107">如需詳細資訊，請參閱 [Player Framework for Windows 8](http://playerframework.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="ef940-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="ef940-108">本教學課程包含四個課程：</span><span class="sxs-lookup"><span data-stu-id="ef940-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="ef940-109">建立基本的 Smooth Streaming 市集應用程式</span><span class="sxs-lookup"><span data-stu-id="ef940-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="ef940-110">將滑桿 tooControl hello 媒體進度列</span><span class="sxs-lookup"><span data-stu-id="ef940-110">Add a Slider Bar tooControl hello Media Progress</span></span>
3. <span data-ttu-id="ef940-111">選取 Smooth Streaming 資料流</span><span class="sxs-lookup"><span data-stu-id="ef940-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="ef940-112">選取 Smooth Streaming 曲目</span><span class="sxs-lookup"><span data-stu-id="ef940-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef940-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="ef940-113">Prerequisites</span></span>
* <span data-ttu-id="ef940-114">Windows 8 32 位元或 64 位元。</span><span class="sxs-lookup"><span data-stu-id="ef940-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="ef940-115">您可以從 MSDN 取得 [Windows 8 Enterprise 評估版](http://msdn.microsoft.com/evalcenter/jj554510.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="ef940-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="ef940-116">Visual Studio 2012 或 Visual Studio Express 2012 (或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="ef940-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="ef940-117">您可以取得從 hello 試用版[這裡](http://www.microsoft.com/visualstudio/11/downloads)。</span><span class="sxs-lookup"><span data-stu-id="ef940-117">You can get hello trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="ef940-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home)(英文)。</span><span class="sxs-lookup"><span data-stu-id="ef940-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="ef940-119">您可以從 MSDN 開發人員程式碼範例 （程式碼庫） 下載完成 hello 方案，每個單元：</span><span class="sxs-lookup"><span data-stu-id="ef940-119">hello completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="ef940-120">[課程 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - 簡單 Windows 8 Smooth Streaming Media Player，</span><span class="sxs-lookup"><span data-stu-id="ef940-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="ef940-121">[課程 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - 具有滑動軸控制項的簡單 Windows 8 Smooth Streaming Media Player，</span><span class="sxs-lookup"><span data-stu-id="ef940-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="ef940-122">[課程 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - 具有串流選擇的 Windows 8 Smooth Streaming Media Player，</span><span class="sxs-lookup"><span data-stu-id="ef940-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="ef940-123">[課程 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) - 具有追蹤選擇的 Windows 8 Smooth Streaming Media Player。</span><span class="sxs-lookup"><span data-stu-id="ef940-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="ef940-124">課程 1：建立基本的 Smooth Streaming 市集應用程式</span><span class="sxs-lookup"><span data-stu-id="ef940-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="ef940-125">在這一課，您將建立 Windows 市集應用程式使用 MediaElement 控制項 tooplay Smooth Streaming 內容。</span><span class="sxs-lookup"><span data-stu-id="ef940-125">In this lesson, you will create a Windows Store application with a MediaElement control tooplay Smooth Stream content.</span></span>  <span data-ttu-id="ef940-126">hello 執行的應用程式看起來像：</span><span class="sxs-lookup"><span data-stu-id="ef940-126">hello running application looks like:</span></span>

![Smooth Streaming Windows Store application example][PlayerApplication]

<span data-ttu-id="ef940-128">如需關於開發 Windows 市集應用程式的詳細資訊，請參閱 [開發 Windows 8 適用的好用應用程式](http://msdn.microsoft.com/windows/apps/br229512.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ef940-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="ef940-129">這一課包含下列程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-129">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="ef940-130">建立 Windows 市集專案</span><span class="sxs-lookup"><span data-stu-id="ef940-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="ef940-131">設計 hello 使用者介面 (XAML)</span><span class="sxs-lookup"><span data-stu-id="ef940-131">Design hello user interface (XAML)</span></span>
3. <span data-ttu-id="ef940-132">修改 hello 程式碼後置檔案</span><span class="sxs-lookup"><span data-stu-id="ef940-132">Modify hello code behind file</span></span>
4. <span data-ttu-id="ef940-133">編譯和測試 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="ef940-133">Compile and test hello application</span></span>

<span data-ttu-id="ef940-134">**toocreate 的 Windows 市集專案**</span><span class="sxs-lookup"><span data-stu-id="ef940-134">**toocreate a Windows Store project**</span></span>

1. <span data-ttu-id="ef940-135">執行 Visual Studio 2012 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ef940-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="ef940-136">從 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="ef940-136">From hello **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="ef940-137">Hello 新增專案 對話方塊，從類型或選取 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="ef940-137">From hello New Project dialog, type or select  hello following values:</span></span>

| <span data-ttu-id="ef940-138">名稱</span><span class="sxs-lookup"><span data-stu-id="ef940-138">Name</span></span> | <span data-ttu-id="ef940-139">值</span><span class="sxs-lookup"><span data-stu-id="ef940-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="ef940-140">範本群組</span><span class="sxs-lookup"><span data-stu-id="ef940-140">Template group</span></span> |<span data-ttu-id="ef940-141">已安裝/範本/Visual C#/Windows 市集</span><span class="sxs-lookup"><span data-stu-id="ef940-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="ef940-142">範本</span><span class="sxs-lookup"><span data-stu-id="ef940-142">Template</span></span> |<span data-ttu-id="ef940-143">空白應用程式 (XAML)</span><span class="sxs-lookup"><span data-stu-id="ef940-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="ef940-144">名稱</span><span class="sxs-lookup"><span data-stu-id="ef940-144">Name</span></span> |<span data-ttu-id="ef940-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="ef940-145">SSPlayer</span></span> |
| <span data-ttu-id="ef940-146">位置</span><span class="sxs-lookup"><span data-stu-id="ef940-146">Location</span></span> |<span data-ttu-id="ef940-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="ef940-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="ef940-148">方案名稱</span><span class="sxs-lookup"><span data-stu-id="ef940-148">Solution Name</span></span> |<span data-ttu-id="ef940-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="ef940-149">SSPlayer</span></span> |
| <span data-ttu-id="ef940-150">為方案建立目錄</span><span class="sxs-lookup"><span data-stu-id="ef940-150">Create directory for solution</span></span> |<span data-ttu-id="ef940-151">(已選取)</span><span class="sxs-lookup"><span data-stu-id="ef940-151">(selected)</span></span> |

1. <span data-ttu-id="ef940-152">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="ef940-152">Click **OK**.</span></span>

<span data-ttu-id="ef940-153">**tooadd 參考 toohello Smooth Streaming Client SDK**</span><span class="sxs-lookup"><span data-stu-id="ef940-153">**tooadd a reference toohello Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="ef940-154">從 方案總管 中，在 SSPlayer 上按一下滑鼠右鍵，然後按一下加入參考。</span><span class="sxs-lookup"><span data-stu-id="ef940-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="ef940-155">輸入或選取下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-155">Type or select hello following values:</span></span>

| <span data-ttu-id="ef940-156">名稱</span><span class="sxs-lookup"><span data-stu-id="ef940-156">Name</span></span> | <span data-ttu-id="ef940-157">值</span><span class="sxs-lookup"><span data-stu-id="ef940-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="ef940-158">參考群組</span><span class="sxs-lookup"><span data-stu-id="ef940-158">Reference group</span></span> |<span data-ttu-id="ef940-159">Windows/延伸</span><span class="sxs-lookup"><span data-stu-id="ef940-159">Windows/Extensions</span></span> |
| <span data-ttu-id="ef940-160">參考</span><span class="sxs-lookup"><span data-stu-id="ef940-160">Reference</span></span> |<span data-ttu-id="ef940-161">選取 Microsoft Smooth Streaming Client SDK for Windows 8 和 Microsoft Visual C++ Runtime Package</span><span class="sxs-lookup"><span data-stu-id="ef940-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="ef940-162">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="ef940-162">Click **OK**.</span></span> 

<span data-ttu-id="ef940-163">在新增之後 hello 參考，您必須選取 hello 目標平台 （x64 或 x86），將參考加入並不適用於任何 CPU 平台組態。</span><span class="sxs-lookup"><span data-stu-id="ef940-163">After adding hello references, you must select hello targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="ef940-164">在方案總管中，您會看到這些加入的參考具有黃色警告標記。</span><span class="sxs-lookup"><span data-stu-id="ef940-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="ef940-165">**toodesign hello 播放程式使用者介面**</span><span class="sxs-lookup"><span data-stu-id="ef940-165">**toodesign hello player user interface**</span></span>

1. <span data-ttu-id="ef940-166">在 [方案總管] 中，按兩下**MainPage.xaml** tooopen 在 hello 設計檢視。</span><span class="sxs-lookup"><span data-stu-id="ef940-166">From Solution Explorer, double click **MainPage.xaml** tooopen it in hello design view.</span></span>
2. <span data-ttu-id="ef940-167">找出 hello **&lt;方格&gt;**和 **&lt;/Grid&gt;** 標記 hello XAML 檔案，並貼上 hello 下列程式碼之間 hello 兩個標記：</span><span class="sxs-lookup"><span data-stu-id="ef940-167">Locate hello **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags hello XAML file, and paste hello following code between hello two tags:</span></span>

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
   
   <span data-ttu-id="ef940-168">hello MediaElement 控制項是使用的 tooplayback 媒體。</span><span class="sxs-lookup"><span data-stu-id="ef940-168">hello MediaElement control is used tooplayback media.</span></span> <span data-ttu-id="ef940-169">名為 sliderProgress hello 滑桿控制項將使用 hello 下一個課程 toocontrol hello 媒體進行中。</span><span class="sxs-lookup"><span data-stu-id="ef940-169">hello slider control named sliderProgress will be used in hello next lesson toocontrol hello media progress.</span></span>
3. <span data-ttu-id="ef940-170">按**CTRL + S** toosave hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="ef940-170">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="ef940-171">hello MediaElement 控制項不支援 Smooth Streaming 內容的現成。</span><span class="sxs-lookup"><span data-stu-id="ef940-171">hello MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="ef940-172">tooenable hello Smooth Streaming 支援，您必須註冊 hello Smooth Streaming 位元組資料流的副檔名與 MIME 類型的處理常式。</span><span class="sxs-lookup"><span data-stu-id="ef940-172">tooenable hello Smooth Streaming support, you must register hello Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="ef940-173">tooregister，您可以使用 hello MediaExtensionManager.RegisterByteStremHandler 方法 hello Windows.Media 命名空間。</span><span class="sxs-lookup"><span data-stu-id="ef940-173">tooregister, you use hello MediaExtensionManager.RegisterByteStremHandler method of hello Windows.Media namespace.</span></span>

<span data-ttu-id="ef940-174">在此 XAML 檔案中，某些事件處理常式會與 hello 控制項相關聯。</span><span class="sxs-lookup"><span data-stu-id="ef940-174">In this XAML file, some event handlers are associated with hello controls.</span></span>  <span data-ttu-id="ef940-175">您必須定義那些事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="ef940-175">You must define those event handlers.</span></span>

<span data-ttu-id="ef940-176">**toomodify hello 的程式碼後置檔案**</span><span class="sxs-lookup"><span data-stu-id="ef940-176">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="ef940-177">從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視程式碼。</span><span class="sxs-lookup"><span data-stu-id="ef940-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="ef940-178">在 hello hello 檔案頂端，加入 hello 下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="ef940-178">At hello top of hello file, add hello following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="ef940-179">在 hello hello 開頭**MainPage**類別中，加入下列資料成員的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-179">At hello beginning of hello **MainPage** class, add hello following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="ef940-180">結尾 hello hello **MainPage**建構函式，新增下列兩行 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-180">At hello end of hello **MainPage** constructor, add hello following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="ef940-181">結尾 hello hello **MainPage**類別中，貼上下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-181">At hello end of hello **MainPage** class, paste hello following code:</span></span>
   
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

<span data-ttu-id="ef940-182">hello sliderProgress_PointerPressed 事件處理常式是此處所定義。</span><span class="sxs-lookup"><span data-stu-id="ef940-182">hello sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="ef940-183">有多個 works toodo tooget 它運作，這會涵蓋 hello 這個教學課程的下一課。</span><span class="sxs-lookup"><span data-stu-id="ef940-183">There are more works toodo tooget it working, which will be covered in hello next lesson of this tutorial.</span></span>
6. <span data-ttu-id="ef940-184">按**CTRL + S** toosave hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="ef940-184">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="ef940-185">hello 完成的 hello 程式碼後置檔案應該看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="ef940-185">hello finished hello code behind file shall look like this:</span></span>

![Codeview in Visual Studio of Smooth Streaming Windows Store application][CodeViewPic]

<span data-ttu-id="ef940-187">**toocompile 和測試 hello 應用程式**</span><span class="sxs-lookup"><span data-stu-id="ef940-187">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="ef940-188">從 hello**建置**功能表上，按一下  **Configuration Manager**。</span><span class="sxs-lookup"><span data-stu-id="ef940-188">From hello **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="ef940-189">變更**作用中的方案平台**toomatch 開發平台。</span><span class="sxs-lookup"><span data-stu-id="ef940-189">Change **Active solution platform** toomatch your development platform.</span></span>
3. <span data-ttu-id="ef940-190">按**F6** toocompile hello 專案。</span><span class="sxs-lookup"><span data-stu-id="ef940-190">Press **F6** toocompile hello project.</span></span> 
4. <span data-ttu-id="ef940-191">按**F5** toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef940-191">Press **F5** toorun hello application.</span></span>
5. <span data-ttu-id="ef940-192">在 hello 頂端 hello 應用程式，您可以使用預設的 hello Smooth Streaming URL，或輸入另一個。</span><span class="sxs-lookup"><span data-stu-id="ef940-192">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="ef940-193">按一下 [設定來源] 。</span><span class="sxs-lookup"><span data-stu-id="ef940-193">Click **Set Source**.</span></span> <span data-ttu-id="ef940-194">因為**自動播放**hello 應該自動播放媒體，預設會啟用。</span><span class="sxs-lookup"><span data-stu-id="ef940-194">Because **Auto Play** is enabled by default, hello media shall play automatically.</span></span>  <span data-ttu-id="ef940-195">您可以控制 hello 媒體使用 hello**播放**，**暫停**和**停止**按鈕。</span><span class="sxs-lookup"><span data-stu-id="ef940-195">You can control hello media using hello **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="ef940-196">您可以控制使用 hello 垂直滑桿 hello 媒體磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ef940-196">You can control hello media volume using hello vertical slider.</span></span>  <span data-ttu-id="ef940-197">不過 hello 水平滑桿控制 hello 媒體進行完全尚未實作。</span><span class="sxs-lookup"><span data-stu-id="ef940-197">However hello horizontal slider for controlling hello media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="ef940-198">您已完成課程 1。</span><span class="sxs-lookup"><span data-stu-id="ef940-198">You have completed lesson1.</span></span>  <span data-ttu-id="ef940-199">在這一課，您可以使用 MediaElement 控制項 tooplayback Smooth Streaming 內容。</span><span class="sxs-lookup"><span data-stu-id="ef940-199">In this lesson, you use a MediaElement control tooplayback Smooth Streaming content.</span></span>  <span data-ttu-id="ef940-200">Hello 下一課，您會加入滑桿 toocontrol hello 進度的 hello Smooth Streaming 內容。</span><span class="sxs-lookup"><span data-stu-id="ef940-200">In hello next lesson, you will add a slider toocontrol hello progress of hello Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a><span data-ttu-id="ef940-201">第 2 課： 加入滑桿 tooControl hello 媒體進度列</span><span class="sxs-lookup"><span data-stu-id="ef940-201">Lesson 2: Add a Slider Bar tooControl hello Media Progress</span></span>

<span data-ttu-id="ef940-202">在第 1 課中，您可以建立 Windows 市集應用程式使用 MediaElement XAML 控制項 tooplayback Smooth Streaming 媒體內容。</span><span class="sxs-lookup"><span data-stu-id="ef940-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control tooplayback Smooth Streaming media content.</span></span>  <span data-ttu-id="ef940-203">它包含一些基本媒體功能 (例如啟動、停止和暫停)。</span><span class="sxs-lookup"><span data-stu-id="ef940-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="ef940-204">在這一課，您會加入滑桿列控制項 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef940-204">In this lesson, you will add a slider bar control toohello application.</span></span>

<span data-ttu-id="ef940-205">在本教學課程中，我們將使用計時器 tooupdate hello 鎏  彸依據 hello 的 hello MediaElement 控制項目前的位置。</span><span class="sxs-lookup"><span data-stu-id="ef940-205">In this tutorial, we will use a timer tooupdate hello slider position based on hello current position of hello MediaElement control.</span></span>  <span data-ttu-id="ef940-206">hello 滑桿開始和結束時間也需要 toobe 更新發生實況內容。</span><span class="sxs-lookup"><span data-stu-id="ef940-206">hello slider start and end time also need toobe updated in case of live content.</span></span>  <span data-ttu-id="ef940-207">這可以 hello 適應性來源更新事件中進一步處理。</span><span class="sxs-lookup"><span data-stu-id="ef940-207">This can be better handled in hello adaptive source update event.</span></span>

<span data-ttu-id="ef940-208">媒體來源是一種產生媒體資料的物件。</span><span class="sxs-lookup"><span data-stu-id="ef940-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="ef940-209">hello 來源解析程式會採用 URL 或位元組資料流，並建立該內容的 hello 適當的媒體來源。</span><span class="sxs-lookup"><span data-stu-id="ef940-209">hello source resolver takes a URL or byte stream and creates hello appropriate media source for that content.</span></span>  <span data-ttu-id="ef940-210">hello 來源解析程式是 hello hello 應用程式 toocreate 媒體來源的標準方式。</span><span class="sxs-lookup"><span data-stu-id="ef940-210">hello source resolver is hello standard way for hello applications toocreate media sources.</span></span> 

<span data-ttu-id="ef940-211">這一課包含下列程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-211">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="ef940-212">註冊 hello Smooth Streaming 的處理常式</span><span class="sxs-lookup"><span data-stu-id="ef940-212">Register hello Smooth Streaming handler</span></span> 
2. <span data-ttu-id="ef940-213">加入 hello 適應性來源管理員層級的事件處理常式</span><span class="sxs-lookup"><span data-stu-id="ef940-213">Add hello adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="ef940-214">加入 hello 適應性來源層級的事件處理常式</span><span class="sxs-lookup"><span data-stu-id="ef940-214">Add hello adaptive source level event handlers</span></span>
4. <span data-ttu-id="ef940-215">新增 MediaElement 事件處理常式</span><span class="sxs-lookup"><span data-stu-id="ef940-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="ef940-216">新增滑動軸相關程式碼</span><span class="sxs-lookup"><span data-stu-id="ef940-216">Add slider bar related code</span></span>
6. <span data-ttu-id="ef940-217">編譯和測試 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="ef940-217">Compile and test hello application</span></span>

<span data-ttu-id="ef940-218">**tooregister hello Smooth Streaming 位元組資料流處理常式，並傳入 hello propertyset**</span><span class="sxs-lookup"><span data-stu-id="ef940-218">**tooregister hello Smooth Streaming byte-stream handler and pass hello propertyset**</span></span>

1. <span data-ttu-id="ef940-219">從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視程式碼。</span><span class="sxs-lookup"><span data-stu-id="ef940-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="ef940-220">在 hello hello 檔案開頭，加入 hello 下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="ef940-220">At hello beginning of hello file, add hello following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="ef940-221">在 MainPage 類別 hello hello 開頭，加入下列資料成員的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-221">At hello beginning of hello MainPage class, add hello following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="ef940-222">內部 hello **MainPage**建構函式，加入下列程式碼之後 hello hello**這。初始化 Components();**行與 hello 上一課中寫入 hello 註冊程式碼行：</span><span class="sxs-lookup"><span data-stu-id="ef940-222">Inside hello **MainPage** constructor, add hello following code after hello **this.Initialize Components();** line and hello registration code lines written in hello previous lesson:</span></span>

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="ef940-223">內部 hello **MainPage**建構函式，修改 hello 兩 RegisterByteStreamHandler 方法 tooadd hello 制定參數：</span><span class="sxs-lookup"><span data-stu-id="ef940-223">Inside hello **MainPage** constructor, modify hello two RegisterByteStreamHandler methods tooadd hello forth parameters:</span></span>

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
6. <span data-ttu-id="ef940-224">按**CTRL + S** toosave hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="ef940-224">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="ef940-225">**tooadd hello 適應性來源管理員層級的事件處理常式**</span><span class="sxs-lookup"><span data-stu-id="ef940-225">**tooadd hello adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="ef940-226">從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視程式碼。</span><span class="sxs-lookup"><span data-stu-id="ef940-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="ef940-227">內部 hello **MainPage**類別中，加入下列資料成員的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-227">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="ef940-228">private AdaptiveSource adaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="ef940-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="ef940-229">結尾 hello hello **MainPage**類別中，新增下列事件處理常式的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-229">At hello end of hello **MainPage** class, add hello following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="ef940-230">結尾 hello hello **MainPage**建構函式，加入下列行 toosubscribe toohello 彈性的來源開啟事件 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-230">At hello end of hello **MainPage** constructor, add hello following line toosubscribe toohello adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="ef940-231">按**CTRL + S** toosave hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="ef940-231">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="ef940-232">**tooadd 適應性來源層級的事件處理常式**</span><span class="sxs-lookup"><span data-stu-id="ef940-232">**tooadd adaptive source level event handlers**</span></span>

1. <span data-ttu-id="ef940-233">從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視程式碼。</span><span class="sxs-lookup"><span data-stu-id="ef940-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="ef940-234">內部 hello **MainPage**類別中，加入下列資料成員的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-234">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="ef940-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span><span class="sxs-lookup"><span data-stu-id="ef940-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="ef940-236">結尾 hello hello **MainPage**類別中，新增下列事件處理常式的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-236">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

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
4. <span data-ttu-id="ef940-237">結尾 hello hello **mediaElement AdaptiveSourceOpened**方法，加入下列程式碼 toosubscribe toohello 事件 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-237">At hello end of hello **mediaElement AdaptiveSourceOpened** method, add hello following code toosubscribe toohello events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="ef940-238">按**CTRL + S** toosave hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="ef940-238">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="ef940-239">hello 相同事件可用的自動調整來源 manger 層級，也可以用於處理功能一般 tooall 媒體中的項目 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef940-239">hello same events are available on Adaptive Source manger level as well, which can be used for handling functionality common tooall media elements in hello app.</span></span> <span data-ttu-id="ef940-240">每個 AdaptiveSource 都包含自己專屬的事件，而且所有 AdaptiveSource 事件都會在 AdaptiveSourceManager 下階層式列出。</span><span class="sxs-lookup"><span data-stu-id="ef940-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="ef940-241">**tooadd 媒體項目事件處理常式**</span><span class="sxs-lookup"><span data-stu-id="ef940-241">**tooadd Media Element event handlers**</span></span>

1. <span data-ttu-id="ef940-242">從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視程式碼。</span><span class="sxs-lookup"><span data-stu-id="ef940-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="ef940-243">結尾 hello hello **MainPage**類別中，新增下列事件處理常式的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-243">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

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
3. <span data-ttu-id="ef940-244">結尾 hello hello **MainPage**建構函式，加入下列程式碼 toosubscript toohello 事件 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-244">At hello end of hello **MainPage** constructor, add hello following code toosubscript toohello events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="ef940-245">按**CTRL + S** toosave hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="ef940-245">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="ef940-246">**tooadd 滑桿列相關的程式碼**</span><span class="sxs-lookup"><span data-stu-id="ef940-246">**tooadd slider bar related code**</span></span>

1. <span data-ttu-id="ef940-247">從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視程式碼。</span><span class="sxs-lookup"><span data-stu-id="ef940-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="ef940-248">在 hello hello 檔案開頭，加入 hello 下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="ef940-248">At hello beginning of hello file, add hello following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="ef940-249">內部 hello **MainPage**類別中，加入下列資料成員的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-249">Inside hello **MainPage** class, add hello following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="ef940-250">結尾 hello hello **MainPage**建構函式，加入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-250">At hello end of hello **MainPage** constructor, add hello following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="ef940-251">結尾 hello hello **MainPage**類別中，加入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-251">At hello end of hello **MainPage** class, add hello following code:</span></span>

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
><span data-ttu-id="ef940-252">CoreDispatcher 是使用的 toomake toohello UI 執行緒從非 UI 執行緒的變更。</span><span class="sxs-lookup"><span data-stu-id="ef940-252">CoreDispatcher is used toomake changes toohello UI thread from non UI Thread.</span></span> <span data-ttu-id="ef940-253">如果發送器執行緒上的瓶頸，開發人員可以選擇 toouse 發送器提供 UI 項目最初打算 tooupdate。</span><span class="sxs-lookup"><span data-stu-id="ef940-253">In case of bottleneck on dispatcher thread, developer can choose toouse dispatcher provided by UI-element he/she intends tooupdate.</span></span>  <span data-ttu-id="ef940-254">例如：</span><span class="sxs-lookup"><span data-stu-id="ef940-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="ef940-255">結尾 hello hello **mediaElement_AdaptiveSourceStatusUpdated**方法，加入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-255">At hello end of hello **mediaElement_AdaptiveSourceStatusUpdated** method, add hello following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="ef940-256">結尾 hello hello **MediaOpened**方法，加入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-256">At hello end of hello **MediaOpened** method, add hello following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="ef940-257">按**CTRL + S** toosave hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="ef940-257">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="ef940-258">**toocompile 和測試 hello 應用程式**</span><span class="sxs-lookup"><span data-stu-id="ef940-258">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="ef940-259">按**F6** toocompile hello 專案。</span><span class="sxs-lookup"><span data-stu-id="ef940-259">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="ef940-260">按**F5** toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef940-260">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="ef940-261">在 hello 頂端 hello 應用程式，您可以使用預設的 hello Smooth Streaming URL，或輸入另一個。</span><span class="sxs-lookup"><span data-stu-id="ef940-261">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="ef940-262">按一下 [設定來源] 。</span><span class="sxs-lookup"><span data-stu-id="ef940-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="ef940-263">測試 hello 滑動軸。</span><span class="sxs-lookup"><span data-stu-id="ef940-263">Test hello slider bar.</span></span>

<span data-ttu-id="ef940-264">您已完成課程 2。</span><span class="sxs-lookup"><span data-stu-id="ef940-264">You have completed lesson 2.</span></span>  <span data-ttu-id="ef940-265">在這一課，您會加入滑桿 tooapplication。</span><span class="sxs-lookup"><span data-stu-id="ef940-265">In this lesson you added a slider tooapplication.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="ef940-266">課程 3：選取 Smooth Streaming 資料流</span><span class="sxs-lookup"><span data-stu-id="ef940-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="ef940-267">Smooth Streaming 是能夠 toostream 內容都是由 hello 檢視器可選取多個語言音訊音軌。</span><span class="sxs-lookup"><span data-stu-id="ef940-267">Smooth Streaming is capable toostream content with multiple language audio tracks that are selectable by hello viewers.</span></span>  <span data-ttu-id="ef940-268">在這一課，您將啟用檢視器 tooselect 資料流。</span><span class="sxs-lookup"><span data-stu-id="ef940-268">In this lesson, you will enable viewers tooselect streams.</span></span> <span data-ttu-id="ef940-269">這一課包含下列程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-269">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="ef940-270">修改 hello XAML 檔案</span><span class="sxs-lookup"><span data-stu-id="ef940-270">Modify hello XAML file</span></span>
2. <span data-ttu-id="ef940-271">修改 hello 碼 behand 檔案</span><span class="sxs-lookup"><span data-stu-id="ef940-271">Modify hello code behand file</span></span>
3. <span data-ttu-id="ef940-272">編譯和測試 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="ef940-272">Compile and test hello application</span></span>

<span data-ttu-id="ef940-273">**toomodify hello XAML 檔案**</span><span class="sxs-lookup"><span data-stu-id="ef940-273">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="ef940-274">從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視設計工具。</span><span class="sxs-lookup"><span data-stu-id="ef940-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="ef940-275">找出&lt;Grid.RowDefinitions&gt;，並讓它們看起來像是修改 hello RowDefinitions:</span><span class="sxs-lookup"><span data-stu-id="ef940-275">Locate &lt;Grid.RowDefinitions&gt;, and modify hello RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="ef940-276">內部 hello&lt;方格&gt;&lt;/Grid&gt;標記，可讓您新增 hello 下列程式碼 toodefine listbox 控制項，讓使用者可以看到 hello 份可用的資料流，並選取資料流：</span><span class="sxs-lookup"><span data-stu-id="ef940-276">Inside hello &lt;Grid&gt;&lt;/Grid&gt; tags, add hello following code toodefine a listbox control, so users can see hello list of available streams, and select streams:</span></span>

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
4. <span data-ttu-id="ef940-277">按**CTRL + S** toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="ef940-277">Press **CTRL+S** toosave hello changes.</span></span>

<span data-ttu-id="ef940-278">**toomodify hello 的程式碼後置檔案**</span><span class="sxs-lookup"><span data-stu-id="ef940-278">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="ef940-279">從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視程式碼。</span><span class="sxs-lookup"><span data-stu-id="ef940-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="ef940-280">在 hello SSPlayer 命名空間中，加入新的類別：</span><span class="sxs-lookup"><span data-stu-id="ef940-280">Inside hello SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="ef940-281">在 MainPage 類別 hello hello 開頭，加入下列變數定義的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-281">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="ef940-282">在 hello MainPage 類別中，加入下列區域的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-282">Inside hello MainPage class, add hello following region:</span></span>
   
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
5. <span data-ttu-id="ef940-283">找出 hello mediaElement_ManifestReady 方法，請新增下列程式碼中的 hello 函式的 hello 結尾 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-283">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="ef940-284">因此就緒 MediaElement 資訊清單時，hello 程式碼取得一份 hello 可用的資料流，並於其中填入 hello 清單 hello UI 清單方塊。</span><span class="sxs-lookup"><span data-stu-id="ef940-284">So when MediaElement manifest is ready, hello code gets a list of hello available streams, and populates hello UI list box with hello list.</span></span>
6. <span data-ttu-id="ef940-285">內部 hello MainPage 類別中，找出 hello UI 按鈕按一下事件地區，然後再加入下列函式定義的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-285">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="ef940-286">**toocompile 和測試 hello 應用程式**</span><span class="sxs-lookup"><span data-stu-id="ef940-286">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="ef940-287">按**F6** toocompile hello 專案。</span><span class="sxs-lookup"><span data-stu-id="ef940-287">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="ef940-288">按**F5** toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef940-288">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="ef940-289">在 hello 頂端 hello 應用程式，您可以使用預設的 hello Smooth Streaming URL，或輸入另一個。</span><span class="sxs-lookup"><span data-stu-id="ef940-289">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="ef940-290">按一下 [設定來源] 。</span><span class="sxs-lookup"><span data-stu-id="ef940-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="ef940-291">hello 預設語言為 audio_eng。</span><span class="sxs-lookup"><span data-stu-id="ef940-291">hello default language is audio_eng.</span></span> <span data-ttu-id="ef940-292">請嘗試 tooswitch audio_eng 和 audio_es 之間。</span><span class="sxs-lookup"><span data-stu-id="ef940-292">Try tooswitch between audio_eng and audio_es.</span></span> <span data-ttu-id="ef940-293">每當，選取新的資料流，您必須按一下 hello 送出按鈕。</span><span class="sxs-lookup"><span data-stu-id="ef940-293">Everytime, you select a new stream, you must click hello Submit button.</span></span>

<span data-ttu-id="ef940-294">您已完成課程 3。</span><span class="sxs-lookup"><span data-stu-id="ef940-294">You have completed lesson 3.</span></span>  <span data-ttu-id="ef940-295">在這一課，您可以將 hello 功能 toochoose 資料流。</span><span class="sxs-lookup"><span data-stu-id="ef940-295">In this lesson, you add hello functionality toochoose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="ef940-296">課程 4：選取 Smooth Streaming 曲目</span><span class="sxs-lookup"><span data-stu-id="ef940-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="ef940-297">Smooth Streaming 簡報可以包含多個以不同品質等級 (位元速率) 和解析度編碼的視訊檔案。</span><span class="sxs-lookup"><span data-stu-id="ef940-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="ef940-298">在這一課，您將啟用使用者 tooselect 追蹤。</span><span class="sxs-lookup"><span data-stu-id="ef940-298">In this lesson, you will enable users tooselect tracks.</span></span> <span data-ttu-id="ef940-299">這一課包含下列程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-299">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="ef940-300">修改 hello XAML 檔案</span><span class="sxs-lookup"><span data-stu-id="ef940-300">Modify hello XAML file</span></span>
2. <span data-ttu-id="ef940-301">修改 hello 碼 behand 檔案</span><span class="sxs-lookup"><span data-stu-id="ef940-301">Modify hello code behand file</span></span>
3. <span data-ttu-id="ef940-302">編譯和測試 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="ef940-302">Compile and test hello application</span></span>

<span data-ttu-id="ef940-303">**toomodify hello XAML 檔案**</span><span class="sxs-lookup"><span data-stu-id="ef940-303">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="ef940-304">從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視設計工具。</span><span class="sxs-lookup"><span data-stu-id="ef940-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="ef940-305">找出 hello&lt;方格&gt;hello 名稱標記**gridStreamAndBitrateSelection**，新增下列程式碼結尾 hello hello 標記 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-305">Locate hello &lt;Grid&gt; tag with hello name **gridStreamAndBitrateSelection**, append hello following code at hello end of hello tag:</span></span>
   
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
3. <span data-ttu-id="ef940-306">按**CTRL + S** toosave 他變更</span><span class="sxs-lookup"><span data-stu-id="ef940-306">Press **CTRL+S** toosave he changes</span></span>

<span data-ttu-id="ef940-307">**toomodify hello 的程式碼後置檔案**</span><span class="sxs-lookup"><span data-stu-id="ef940-307">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="ef940-308">從 方案總管 中，在 MainPage.xaml 上按一下滑鼠右鍵，然後按一下檢視程式碼。</span><span class="sxs-lookup"><span data-stu-id="ef940-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="ef940-309">在 hello SSPlayer 命名空間中，加入新的類別：</span><span class="sxs-lookup"><span data-stu-id="ef940-309">Inside hello SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="ef940-310">在 MainPage 類別 hello hello 開頭，加入下列變數定義的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-310">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="ef940-311">在 hello MainPage 類別中，加入下列區域的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-311">Inside hello MainPage class, add hello following region:</span></span>
   
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
5. <span data-ttu-id="ef940-312">找出 hello mediaElement_ManifestReady 方法，請新增下列程式碼中的 hello 函式的 hello 結尾 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-312">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="ef940-313">內部 hello MainPage 類別中，找出 hello UI 按鈕按一下事件地區，然後再加入下列函式定義的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef940-313">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="ef940-314">**toocompile 和測試 hello 應用程式**</span><span class="sxs-lookup"><span data-stu-id="ef940-314">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="ef940-315">按**F6** toocompile hello 專案。</span><span class="sxs-lookup"><span data-stu-id="ef940-315">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="ef940-316">按**F5** toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef940-316">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="ef940-317">在 hello 頂端 hello 應用程式，您可以使用預設的 hello Smooth Streaming URL，或輸入另一個。</span><span class="sxs-lookup"><span data-stu-id="ef940-317">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="ef940-318">按一下 [設定來源] 。</span><span class="sxs-lookup"><span data-stu-id="ef940-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="ef940-319">根據預設，會選取所有 hello 曲目 hello 視訊資料流。</span><span class="sxs-lookup"><span data-stu-id="ef940-319">By default, all of hello tracks of hello video stream are selected.</span></span> <span data-ttu-id="ef940-320">tooexperiment hello 位元速率的變更，您可以選取 hello 最低位元速率，，然後選取 hello 最高的位元速率可用。</span><span class="sxs-lookup"><span data-stu-id="ef940-320">tooexperiment hello bit rate changes, you can select hello lowest bit rate available, and then select hello highest bit rate available.</span></span> <span data-ttu-id="ef940-321">您必須在每次變更之後按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="ef940-321">You must click Submit after each change.</span></span>  <span data-ttu-id="ef940-322">您可以看到 hello 視訊品質的變更。</span><span class="sxs-lookup"><span data-stu-id="ef940-322">You can see hello video quality changes.</span></span>

<span data-ttu-id="ef940-323">您已完成課程 4。</span><span class="sxs-lookup"><span data-stu-id="ef940-323">You have completed lesson 4.</span></span>  <span data-ttu-id="ef940-324">在這一課，您可以將 hello 功能 toochoose 追蹤。</span><span class="sxs-lookup"><span data-stu-id="ef940-324">In this lesson, you add hello functionality toochoose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ef940-325">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="ef940-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ef940-326">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="ef940-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="ef940-327">其他資源：</span><span class="sxs-lookup"><span data-stu-id="ef940-327">Other Resources:</span></span>
* [<span data-ttu-id="ef940-328">如何 toobuild Smooth Streaming Windows 8 JavaScript 應用程式與進階功能</span><span class="sxs-lookup"><span data-stu-id="ef940-328">How toobuild a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="ef940-329">Smooth Streaming 技術概觀 (英文)</span><span class="sxs-lookup"><span data-stu-id="ef940-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

