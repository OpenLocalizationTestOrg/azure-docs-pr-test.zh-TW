---
title: "Smooth Streaming Windows 市集應用程式教學課程 | Microsoft Docs"
description: "了解如何使用 Azure 媒體服務建立可用 XML MediaElement 控制項來播放 Smooth Streaming 內容的 C# Windows 市集應用程式。"
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
ms.openlocfilehash: c9bb3b1915543fea3561cb309f55c4e8a74ded6d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-build-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="5bf23-103">如何建置 Smooth Streaming Windows 市集應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf23-103">How to Build a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="5bf23-104">Smooth Streaming Client SDK for Windows 8 可讓開發人員建置能夠播放隨選與即時 Smooth Streaming 內容的 Windows 市集應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf23-104">The Smooth Streaming Client SDK for Windows 8 enables developers to build Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="5bf23-105">除了將 Smooth Streaming 內容進行基本播放，SDK 也提供 Microsoft PlayReady 保護、品質等級限制、Live DVR、音訊資料流切換、接聽狀態更新 (例如品質等級變更) 和錯誤事件等這類豐富的功能。</span><span class="sxs-lookup"><span data-stu-id="5bf23-105">In addition to the basic playback of Smooth Streaming content, the SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="5bf23-106">如需所支援功能的詳細資訊，請參閱 [版本資訊](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes)(英文)。</span><span class="sxs-lookup"><span data-stu-id="5bf23-106">For more information of the supported features, see the [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="5bf23-107">如需詳細資訊，請參閱 [Player Framework for Windows 8](http://playerframework.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="5bf23-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="5bf23-108">本教學課程包含四個課程：</span><span class="sxs-lookup"><span data-stu-id="5bf23-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="5bf23-109">建立基本的 Smooth Streaming 市集應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf23-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="5bf23-110">新增滑動軸以控制媒體進度</span><span class="sxs-lookup"><span data-stu-id="5bf23-110">Add a Slider Bar to Control the Media Progress</span></span>
3. <span data-ttu-id="5bf23-111">選取 Smooth Streaming 資料流</span><span class="sxs-lookup"><span data-stu-id="5bf23-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="5bf23-112">選取 Smooth Streaming 曲目</span><span class="sxs-lookup"><span data-stu-id="5bf23-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bf23-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="5bf23-113">Prerequisites</span></span>
* <span data-ttu-id="5bf23-114">Windows 8 32 位元或 64 位元。</span><span class="sxs-lookup"><span data-stu-id="5bf23-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="5bf23-115">您可以從 MSDN 取得 [Windows 8 Enterprise 評估版](http://msdn.microsoft.com/evalcenter/jj554510.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="5bf23-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="5bf23-116">Visual Studio 2012 或 Visual Studio Express 2012 (或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="5bf23-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="5bf23-117">您可以從 [這裡](http://www.microsoft.com/visualstudio/11/downloads)取得試用版。</span><span class="sxs-lookup"><span data-stu-id="5bf23-117">You can get the trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="5bf23-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home)(英文)。</span><span class="sxs-lookup"><span data-stu-id="5bf23-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="5bf23-119">您可以從 MSDN 開發人員程式碼範例 (Code Gallery) 下載每個課程的已完成解答：</span><span class="sxs-lookup"><span data-stu-id="5bf23-119">The completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="5bf23-120">[課程 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - 簡單 Windows 8 Smooth Streaming Media Player，</span><span class="sxs-lookup"><span data-stu-id="5bf23-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="5bf23-121">[課程 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - 具有滑動軸控制項的簡單 Windows 8 Smooth Streaming Media Player，</span><span class="sxs-lookup"><span data-stu-id="5bf23-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="5bf23-122">[課程 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - 具有串流選擇的 Windows 8 Smooth Streaming Media Player，</span><span class="sxs-lookup"><span data-stu-id="5bf23-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="5bf23-123">[課程 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) - 具有追蹤選擇的 Windows 8 Smooth Streaming Media Player。</span><span class="sxs-lookup"><span data-stu-id="5bf23-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="5bf23-124">課程 1：建立基本的 Smooth Streaming 市集應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf23-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="5bf23-125">在本課程中，您將建立 Windows 市集應用程式，並使其具有 MediaElement 控制項來播放 Smooth Stream 內容。</span><span class="sxs-lookup"><span data-stu-id="5bf23-125">In this lesson, you will create a Windows Store application with a MediaElement control to play Smooth Stream content.</span></span>  <span data-ttu-id="5bf23-126">執行中的應用程式看起來如下：</span><span class="sxs-lookup"><span data-stu-id="5bf23-126">The running application looks like:</span></span>

![Smooth Streaming Windows Store application example][PlayerApplication]

<span data-ttu-id="5bf23-128">如需關於開發 Windows 市集應用程式的詳細資訊，請參閱 [開發 Windows 8 適用的好用應用程式](http://msdn.microsoft.com/windows/apps/br229512.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5bf23-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="5bf23-129">本課程包含下列程序：</span><span class="sxs-lookup"><span data-stu-id="5bf23-129">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="5bf23-130">建立 Windows 市集專案</span><span class="sxs-lookup"><span data-stu-id="5bf23-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="5bf23-131">設計使用者介面 (XAML)</span><span class="sxs-lookup"><span data-stu-id="5bf23-131">Design the user interface (XAML)</span></span>
3. <span data-ttu-id="5bf23-132">修改程式碼後置檔案</span><span class="sxs-lookup"><span data-stu-id="5bf23-132">Modify the code behind file</span></span>
4. <span data-ttu-id="5bf23-133">編譯和測試應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf23-133">Compile and test the application</span></span>

<span data-ttu-id="5bf23-134">**建立 Windows 市集專案**</span><span class="sxs-lookup"><span data-stu-id="5bf23-134">**To create a Windows Store project**</span></span>

1. <span data-ttu-id="5bf23-135">執行 Visual Studio 2012 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="5bf23-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="5bf23-136">從 [檔案] 功能表中，按一下 [新增]，再按 [專案]。</span><span class="sxs-lookup"><span data-stu-id="5bf23-136">From the **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="5bf23-137">從 [新增專案] 對話方塊中，輸入或選取下列值：</span><span class="sxs-lookup"><span data-stu-id="5bf23-137">From the New Project dialog, type or select  the following values:</span></span>

| <span data-ttu-id="5bf23-138">名稱</span><span class="sxs-lookup"><span data-stu-id="5bf23-138">Name</span></span> | <span data-ttu-id="5bf23-139">值</span><span class="sxs-lookup"><span data-stu-id="5bf23-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5bf23-140">範本群組</span><span class="sxs-lookup"><span data-stu-id="5bf23-140">Template group</span></span> |<span data-ttu-id="5bf23-141">已安裝/範本/Visual C#/Windows 市集</span><span class="sxs-lookup"><span data-stu-id="5bf23-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="5bf23-142">範本</span><span class="sxs-lookup"><span data-stu-id="5bf23-142">Template</span></span> |<span data-ttu-id="5bf23-143">空白應用程式 (XAML)</span><span class="sxs-lookup"><span data-stu-id="5bf23-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="5bf23-144">名稱</span><span class="sxs-lookup"><span data-stu-id="5bf23-144">Name</span></span> |<span data-ttu-id="5bf23-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="5bf23-145">SSPlayer</span></span> |
| <span data-ttu-id="5bf23-146">位置</span><span class="sxs-lookup"><span data-stu-id="5bf23-146">Location</span></span> |<span data-ttu-id="5bf23-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="5bf23-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="5bf23-148">方案名稱</span><span class="sxs-lookup"><span data-stu-id="5bf23-148">Solution Name</span></span> |<span data-ttu-id="5bf23-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="5bf23-149">SSPlayer</span></span> |
| <span data-ttu-id="5bf23-150">為方案建立目錄</span><span class="sxs-lookup"><span data-stu-id="5bf23-150">Create directory for solution</span></span> |<span data-ttu-id="5bf23-151">(已選取)</span><span class="sxs-lookup"><span data-stu-id="5bf23-151">(selected)</span></span> |

1. <span data-ttu-id="5bf23-152">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5bf23-152">Click **OK**.</span></span>

<span data-ttu-id="5bf23-153">**新增 Smooth Streaming Client SDK 的參考**</span><span class="sxs-lookup"><span data-stu-id="5bf23-153">**To add a reference to the Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="5bf23-154">從 [方案總管] 中，在 [SSPlayer] 上按一下滑鼠右鍵，然後按一下 [加入參考]。</span><span class="sxs-lookup"><span data-stu-id="5bf23-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="5bf23-155">輸入或選取下列值：</span><span class="sxs-lookup"><span data-stu-id="5bf23-155">Type or select the following values:</span></span>

| <span data-ttu-id="5bf23-156">名稱</span><span class="sxs-lookup"><span data-stu-id="5bf23-156">Name</span></span> | <span data-ttu-id="5bf23-157">值</span><span class="sxs-lookup"><span data-stu-id="5bf23-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5bf23-158">參考群組</span><span class="sxs-lookup"><span data-stu-id="5bf23-158">Reference group</span></span> |<span data-ttu-id="5bf23-159">Windows/延伸</span><span class="sxs-lookup"><span data-stu-id="5bf23-159">Windows/Extensions</span></span> |
| <span data-ttu-id="5bf23-160">參考</span><span class="sxs-lookup"><span data-stu-id="5bf23-160">Reference</span></span> |<span data-ttu-id="5bf23-161">選取 Microsoft Smooth Streaming Client SDK for Windows 8 和 Microsoft Visual C++ Runtime Package</span><span class="sxs-lookup"><span data-stu-id="5bf23-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="5bf23-162">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5bf23-162">Click **OK**.</span></span> 

<span data-ttu-id="5bf23-163">加入參考之後，您必須選取目標平台 (x64 或 x86)，而加入參考在「任何 CPU 平台」組態中將沒有作用。</span><span class="sxs-lookup"><span data-stu-id="5bf23-163">After adding the references, you must select the targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="5bf23-164">在方案總管中，您會看到這些加入的參考具有黃色警告標記。</span><span class="sxs-lookup"><span data-stu-id="5bf23-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="5bf23-165">**設計播放程式使用者介面**</span><span class="sxs-lookup"><span data-stu-id="5bf23-165">**To design the player user interface**</span></span>

1. <span data-ttu-id="5bf23-166">從 [方案總管] 中，按兩下 [MainPage.xaml]  ，以設計檢視來開啟它。</span><span class="sxs-lookup"><span data-stu-id="5bf23-166">From Solution Explorer, double click **MainPage.xaml** to open it in the design view.</span></span>
2. <span data-ttu-id="5bf23-167">在 XAML 檔案中找到 **&lt;Grid&gt;** 和 **&lt;/Grid&gt;** 標籤，然後在這兩個標籤之間貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="5bf23-167">Locate the **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags the XAML file, and paste the following code between the two tags:</span></span>

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
   
   <span data-ttu-id="5bf23-168">MediaElement 控制項會用來播放媒體。</span><span class="sxs-lookup"><span data-stu-id="5bf23-168">The MediaElement control is used to playback media.</span></span> <span data-ttu-id="5bf23-169">下一個課程將使用名稱為 sliderProgress 的滑動軸控制項來控制媒體進度。</span><span class="sxs-lookup"><span data-stu-id="5bf23-169">The slider control named sliderProgress will be used in the next lesson to control the media progress.</span></span>
3. <span data-ttu-id="5bf23-170">按 **CTRL+S** 儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="5bf23-170">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="5bf23-171">MediaElement 控制項預設不支援 Smooth Streaming 內容。</span><span class="sxs-lookup"><span data-stu-id="5bf23-171">The MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="5bf23-172">若要啟用 Smooth Streaming 支援，您必須依副檔名和 MIME 類型來註冊 Smooth Streaming 位元組資料流處理常式。</span><span class="sxs-lookup"><span data-stu-id="5bf23-172">To enable the Smooth Streaming support, you must register the Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="5bf23-173">若要註冊，請使用 Windows.Media 命名空間的 MediaExtensionManager.RegisterByteStremHandler 方法。</span><span class="sxs-lookup"><span data-stu-id="5bf23-173">To register, you use the MediaExtensionManager.RegisterByteStremHandler method of the Windows.Media namespace.</span></span>

<span data-ttu-id="5bf23-174">在此 XAML 檔案中，有些事件處理常式會與控制項相關聯。</span><span class="sxs-lookup"><span data-stu-id="5bf23-174">In this XAML file, some event handlers are associated with the controls.</span></span>  <span data-ttu-id="5bf23-175">您必須定義那些事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="5bf23-175">You must define those event handlers.</span></span>

<span data-ttu-id="5bf23-176">**修改程式碼後置檔案**</span><span class="sxs-lookup"><span data-stu-id="5bf23-176">**To modify the code behind file**</span></span>

1. <span data-ttu-id="5bf23-177">從 [方案總管] 中，在 [MainPage.xaml] 上按一下滑鼠右鍵，然後按一下 [檢視程式碼]。</span><span class="sxs-lookup"><span data-stu-id="5bf23-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="5bf23-178">在檔案的頂端，新增下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="5bf23-178">At the top of the file, add the following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="5bf23-179">在 **MainPage** 類別的開頭，新增下列資料成員：</span><span class="sxs-lookup"><span data-stu-id="5bf23-179">At the beginning of the **MainPage** class, add the following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="5bf23-180">在 **MainPage** 建構函式的結尾，新增下列兩行：</span><span class="sxs-lookup"><span data-stu-id="5bf23-180">At the end of the **MainPage** constructor, add the following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="5bf23-181">在 **MainPage** 類別結尾貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="5bf23-181">At the end of the **MainPage** class, paste the following code:</span></span>
   
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
             txtStatus.Text = "Click the Play button to play the media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek to position " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

<span data-ttu-id="5bf23-182">這裡在定義 sliderProgress_PointerPressed 事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="5bf23-182">The sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="5bf23-183">還需要進行其他工作，才能讓它運作，在本教學課程的下一個課程中，將會涵蓋這項資訊。</span><span class="sxs-lookup"><span data-stu-id="5bf23-183">There are more works to do to get it working, which will be covered in the next lesson of this tutorial.</span></span>
6. <span data-ttu-id="5bf23-184">按 **CTRL+S** 儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="5bf23-184">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="5bf23-185">完成的程式碼後置檔案看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="5bf23-185">The finished the code behind file shall look like this:</span></span>

![Codeview in Visual Studio of Smooth Streaming Windows Store application][CodeViewPic]

<span data-ttu-id="5bf23-187">**編譯和測試應用程式**</span><span class="sxs-lookup"><span data-stu-id="5bf23-187">**To compile and test the application**</span></span>

1. <span data-ttu-id="5bf23-188">從 [建置] 功能表中，按一下 [組態管理員]。</span><span class="sxs-lookup"><span data-stu-id="5bf23-188">From the **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="5bf23-189">變更 [使用中的方案平台]  ，以符合您的開發平台。</span><span class="sxs-lookup"><span data-stu-id="5bf23-189">Change **Active solution platform** to match your development platform.</span></span>
3. <span data-ttu-id="5bf23-190">按 **F6** 鍵編譯專案。</span><span class="sxs-lookup"><span data-stu-id="5bf23-190">Press **F6** to compile the project.</span></span> 
4. <span data-ttu-id="5bf23-191">按 **F5** 鍵執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf23-191">Press **F5** to run the application.</span></span>
5. <span data-ttu-id="5bf23-192">在應用程式頂端，您可以使用預設 Smooth Streaming URL，或輸入不同的 Smooth Streaming URL。</span><span class="sxs-lookup"><span data-stu-id="5bf23-192">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="5bf23-193">按一下 [設定來源] 。</span><span class="sxs-lookup"><span data-stu-id="5bf23-193">Click **Set Source**.</span></span> <span data-ttu-id="5bf23-194">因為預設會啟用 [自動播放]  ，所以應該會自動播放媒體。</span><span class="sxs-lookup"><span data-stu-id="5bf23-194">Because **Auto Play** is enabled by default, the media shall play automatically.</span></span>  <span data-ttu-id="5bf23-195">您可以使用 [播放]、[暫停] 和 [停止] 按鈕來控制媒體。</span><span class="sxs-lookup"><span data-stu-id="5bf23-195">You can control the media using the **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="5bf23-196">您可以使用垂直滑動軸來控制媒體音量。</span><span class="sxs-lookup"><span data-stu-id="5bf23-196">You can control the media volume using the vertical slider.</span></span>  <span data-ttu-id="5bf23-197">不過，尚未完整實作用於控制媒體進度的水平滑動軸。</span><span class="sxs-lookup"><span data-stu-id="5bf23-197">However the horizontal slider for controlling the media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="5bf23-198">您已完成課程 1。</span><span class="sxs-lookup"><span data-stu-id="5bf23-198">You have completed lesson1.</span></span>  <span data-ttu-id="5bf23-199">在本課程中，您使用 MediaElement 控制項來播放 Smooth Streaming 內容。</span><span class="sxs-lookup"><span data-stu-id="5bf23-199">In this lesson, you use a MediaElement control to playback Smooth Streaming content.</span></span>  <span data-ttu-id="5bf23-200">在下一個課程中，您將新增滑動軸來控制 Smooth Streaming 內容的進度。</span><span class="sxs-lookup"><span data-stu-id="5bf23-200">In the next lesson, you will add a slider to control the progress of the Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-to-control-the-media-progress"></a><span data-ttu-id="5bf23-201">課程 2：新增滑動軸以控制媒體進度</span><span class="sxs-lookup"><span data-stu-id="5bf23-201">Lesson 2: Add a Slider Bar to Control the Media Progress</span></span>

<span data-ttu-id="5bf23-202">在課程 1 中，您已建立 Windows 市集應用程式，並使其具有 MediaElement XAML 控制項來播放 Smooth Streaming 媒體內容。</span><span class="sxs-lookup"><span data-stu-id="5bf23-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control to playback Smooth Streaming media content.</span></span>  <span data-ttu-id="5bf23-203">它包含一些基本媒體功能 (例如啟動、停止和暫停)。</span><span class="sxs-lookup"><span data-stu-id="5bf23-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="5bf23-204">在本課程中，您將在應用程式中新增滑動軸控制項。</span><span class="sxs-lookup"><span data-stu-id="5bf23-204">In this lesson, you will add a slider bar control to the application.</span></span>

<span data-ttu-id="5bf23-205">在本教學課程中，我們將使用計時器，以根據 MediaElement 控制項的目前位置來更新滑動軸位置。</span><span class="sxs-lookup"><span data-stu-id="5bf23-205">In this tutorial, we will use a timer to update the slider position based on the current position of the MediaElement control.</span></span>  <span data-ttu-id="5bf23-206">如果是即時內容，則還需要更新滑動軸開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="5bf23-206">The slider start and end time also need to be updated in case of live content.</span></span>  <span data-ttu-id="5bf23-207">這可以透過調適性來源更新事件獲得更恰當的處理。</span><span class="sxs-lookup"><span data-stu-id="5bf23-207">This can be better handled in the adaptive source update event.</span></span>

<span data-ttu-id="5bf23-208">媒體來源是一種產生媒體資料的物件。</span><span class="sxs-lookup"><span data-stu-id="5bf23-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="5bf23-209">來源解析程式會接受 URL 或位元組資料流，然後為該內容建立適當的媒體來源。</span><span class="sxs-lookup"><span data-stu-id="5bf23-209">The source resolver takes a URL or byte stream and creates the appropriate media source for that content.</span></span>  <span data-ttu-id="5bf23-210">來源解析程式是應用程式建立媒體來源的標準方式。</span><span class="sxs-lookup"><span data-stu-id="5bf23-210">The source resolver is the standard way for the applications to create media sources.</span></span> 

<span data-ttu-id="5bf23-211">本課程包含下列程序：</span><span class="sxs-lookup"><span data-stu-id="5bf23-211">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="5bf23-212">註冊 Smooth Streaming 處理常式</span><span class="sxs-lookup"><span data-stu-id="5bf23-212">Register the Smooth Streaming handler</span></span> 
2. <span data-ttu-id="5bf23-213">新增調適性來源管理員層級事件處理常式</span><span class="sxs-lookup"><span data-stu-id="5bf23-213">Add the adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="5bf23-214">新增調適性來源層級事件處理常式</span><span class="sxs-lookup"><span data-stu-id="5bf23-214">Add the adaptive source level event handlers</span></span>
4. <span data-ttu-id="5bf23-215">新增 MediaElement 事件處理常式</span><span class="sxs-lookup"><span data-stu-id="5bf23-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="5bf23-216">新增滑動軸相關程式碼</span><span class="sxs-lookup"><span data-stu-id="5bf23-216">Add slider bar related code</span></span>
6. <span data-ttu-id="5bf23-217">編譯和測試應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf23-217">Compile and test the application</span></span>

<span data-ttu-id="5bf23-218">**註冊 Smooth Streaming 位元組資料流處理常式並傳遞屬性集**</span><span class="sxs-lookup"><span data-stu-id="5bf23-218">**To register the Smooth Streaming byte-stream handler and pass the propertyset**</span></span>

1. <span data-ttu-id="5bf23-219">從 [方案總管] 中，在 [MainPage.xaml] 上按一下滑鼠右鍵，然後按一下 [檢視程式碼]。</span><span class="sxs-lookup"><span data-stu-id="5bf23-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="5bf23-220">在檔案的開頭，新增下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="5bf23-220">At the beginning of the file, add the following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="5bf23-221">在 MainPage 類別的開頭，新增下列資料成員：</span><span class="sxs-lookup"><span data-stu-id="5bf23-221">At the beginning of the MainPage class, add the following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="5bf23-222">在 **MainPage** 建構函式內，於 **this.Initialize Components();** 行以及上一個課程中所寫的註冊程式碼行的後面新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="5bf23-222">Inside the **MainPage** constructor, add the following code after the **this.Initialize Components();** line and the registration code lines written in the previous lesson:</span></span>

        // Gets the default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value to AdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="5bf23-223">在 **MainPage** 建構函式內，修改兩個 RegisterByteStreamHandler 方法以新增 forth 參數：</span><span class="sxs-lookup"><span data-stu-id="5bf23-223">Inside the **MainPage** constructor, modify the two RegisterByteStreamHandler methods to add the forth parameters:</span></span>

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass the propertyset. 
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
6. <span data-ttu-id="5bf23-224">按 **CTRL+S** 儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="5bf23-224">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="5bf23-225">**新增調適性來源管理員層級事件處理常式**</span><span class="sxs-lookup"><span data-stu-id="5bf23-225">**To add the adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="5bf23-226">從 [方案總管] 中，在 [MainPage.xaml] 上按一下滑鼠右鍵，然後按一下 [檢視程式碼]。</span><span class="sxs-lookup"><span data-stu-id="5bf23-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="5bf23-227">在 [MainPage]  類別內，新增下列資料成員：</span><span class="sxs-lookup"><span data-stu-id="5bf23-227">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="5bf23-228">private AdaptiveSource adaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="5bf23-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="5bf23-229">在 **MainPage** 類別的結尾，新增下列事件處理常式：</span><span class="sxs-lookup"><span data-stu-id="5bf23-229">At the end of the **MainPage** class, add the following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="5bf23-230">在 **MainPage** 建構函式的結尾，新增下行以訂閱調適性來源開放事件：</span><span class="sxs-lookup"><span data-stu-id="5bf23-230">At the end of the **MainPage** constructor, add the following line to subscribe to the adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="5bf23-231">按 **CTRL+S** 儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="5bf23-231">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="5bf23-232">**新增調適性來源層級事件處理常式**</span><span class="sxs-lookup"><span data-stu-id="5bf23-232">**To add adaptive source level event handlers**</span></span>

1. <span data-ttu-id="5bf23-233">從 [方案總管] 中，在 [MainPage.xaml] 上按一下滑鼠右鍵，然後按一下 [檢視程式碼]。</span><span class="sxs-lookup"><span data-stu-id="5bf23-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="5bf23-234">在 [MainPage]  類別內，新增下列資料成員：</span><span class="sxs-lookup"><span data-stu-id="5bf23-234">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="5bf23-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span><span class="sxs-lookup"><span data-stu-id="5bf23-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="5bf23-236">在 **MainPage** 類別的結尾，新增下列事件處理常式：</span><span class="sxs-lookup"><span data-stu-id="5bf23-236">At the end of the **MainPage** class, add the following event handlers:</span></span>

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
4. <span data-ttu-id="5bf23-237">在 **mediaElement AdaptiveSourceOpened** 方法的結尾，新增下列程式碼以訂閱事件：</span><span class="sxs-lookup"><span data-stu-id="5bf23-237">At the end of the **mediaElement AdaptiveSourceOpened** method, add the following code to subscribe to the events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="5bf23-238">按 **CTRL+S** 儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="5bf23-238">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="5bf23-239">在調適性來源管理員層級也有相同的事件，可用於處理應用程式中所有媒體元素通用的功能。</span><span class="sxs-lookup"><span data-stu-id="5bf23-239">The same events are available on Adaptive Source manger level as well, which can be used for handling functionality common to all media elements in the app.</span></span> <span data-ttu-id="5bf23-240">每個 AdaptiveSource 都包含自己專屬的事件，而且所有 AdaptiveSource 事件都會在 AdaptiveSourceManager 下階層式列出。</span><span class="sxs-lookup"><span data-stu-id="5bf23-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="5bf23-241">**新增媒體元素事件處理常式**</span><span class="sxs-lookup"><span data-stu-id="5bf23-241">**To add Media Element event handlers**</span></span>

1. <span data-ttu-id="5bf23-242">從 [方案總管] 中，在 [MainPage.xaml] 上按一下滑鼠右鍵，然後按一下 [檢視程式碼]。</span><span class="sxs-lookup"><span data-stu-id="5bf23-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="5bf23-243">在 **MainPage** 類別的結尾，新增下列事件處理常式：</span><span class="sxs-lookup"><span data-stu-id="5bf23-243">At the end of the **MainPage** class, add the following event handlers:</span></span>

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
3. <span data-ttu-id="5bf23-244">在 **MainPage** 建構函式的結尾，新增下列程式碼以訂閱事件：</span><span class="sxs-lookup"><span data-stu-id="5bf23-244">At the end of the **MainPage** constructor, add the following code to subscript to the events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="5bf23-245">按 **CTRL+S** 儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="5bf23-245">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="5bf23-246">**新增滑動軸相關程式碼**</span><span class="sxs-lookup"><span data-stu-id="5bf23-246">**To add slider bar related code**</span></span>

1. <span data-ttu-id="5bf23-247">從 [方案總管] 中，在 [MainPage.xaml] 上按一下滑鼠右鍵，然後按一下 [檢視程式碼]。</span><span class="sxs-lookup"><span data-stu-id="5bf23-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="5bf23-248">在檔案的開頭，新增下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="5bf23-248">At the beginning of the file, add the following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="5bf23-249">在 [MainPage]  類別內，新增下列資料成員：</span><span class="sxs-lookup"><span data-stu-id="5bf23-249">Inside the **MainPage** class, add the following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="5bf23-250">在 **MainPage** 建構函式的結尾，新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="5bf23-250">At the end of the **MainPage** constructor, add the following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="5bf23-251">在 **MainPage** 類別的結尾，新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="5bf23-251">At the end of the **MainPage** class, add the following code:</span></span>

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
><span data-ttu-id="5bf23-252">CoreDispatcher 用來從非 UI 執行緒對 UI 執行緒進行變更。</span><span class="sxs-lookup"><span data-stu-id="5bf23-252">CoreDispatcher is used to make changes to the UI thread from non UI Thread.</span></span> <span data-ttu-id="5bf23-253">如果發送器執行緒發生瓶頸，開發人員可以選擇使用自己想要更新之 UI-element 所提供的發送器。</span><span class="sxs-lookup"><span data-stu-id="5bf23-253">In case of bottleneck on dispatcher thread, developer can choose to use dispatcher provided by UI-element he/she intends to update.</span></span>  <span data-ttu-id="5bf23-254">例如：</span><span class="sxs-lookup"><span data-stu-id="5bf23-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="5bf23-255">在 **mediaElement_AdaptiveSourceStatusUpdated** 方法的結尾，新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="5bf23-255">At the end of the **mediaElement_AdaptiveSourceStatusUpdated** method, add the following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="5bf23-256">在 **MediaOpened** 方法的結尾，新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="5bf23-256">At the end of the **MediaOpened** method, add the following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="5bf23-257">按 **CTRL+S** 儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="5bf23-257">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="5bf23-258">**編譯和測試應用程式**</span><span class="sxs-lookup"><span data-stu-id="5bf23-258">**To compile and test the application**</span></span>

1. <span data-ttu-id="5bf23-259">按 **F6** 鍵編譯專案。</span><span class="sxs-lookup"><span data-stu-id="5bf23-259">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="5bf23-260">按 **F5** 鍵執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf23-260">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="5bf23-261">在應用程式頂端，您可以使用預設 Smooth Streaming URL，或輸入不同的 Smooth Streaming URL。</span><span class="sxs-lookup"><span data-stu-id="5bf23-261">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="5bf23-262">按一下 [設定來源] 。</span><span class="sxs-lookup"><span data-stu-id="5bf23-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="5bf23-263">測試滑動軸。</span><span class="sxs-lookup"><span data-stu-id="5bf23-263">Test the slider bar.</span></span>

<span data-ttu-id="5bf23-264">您已完成課程 2。</span><span class="sxs-lookup"><span data-stu-id="5bf23-264">You have completed lesson 2.</span></span>  <span data-ttu-id="5bf23-265">在本課程中，您將在應用程式中新增滑動軸。</span><span class="sxs-lookup"><span data-stu-id="5bf23-265">In this lesson you added a slider to application.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="5bf23-266">課程 3：選取 Smooth Streaming 資料流</span><span class="sxs-lookup"><span data-stu-id="5bf23-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="5bf23-267">Smooth Streaming 可以串流含多個曲目可供檢視器選取的內容。</span><span class="sxs-lookup"><span data-stu-id="5bf23-267">Smooth Streaming is capable to stream content with multiple language audio tracks that are selectable by the viewers.</span></span>  <span data-ttu-id="5bf23-268">在本課程中，您將讓檢視器選取資料流。</span><span class="sxs-lookup"><span data-stu-id="5bf23-268">In this lesson, you will enable viewers to select streams.</span></span> <span data-ttu-id="5bf23-269">本課程包含下列程序：</span><span class="sxs-lookup"><span data-stu-id="5bf23-269">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="5bf23-270">修改 XAML 檔案</span><span class="sxs-lookup"><span data-stu-id="5bf23-270">Modify the XAML file</span></span>
2. <span data-ttu-id="5bf23-271">修改程式碼後置檔案</span><span class="sxs-lookup"><span data-stu-id="5bf23-271">Modify the code behand file</span></span>
3. <span data-ttu-id="5bf23-272">編譯和測試應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf23-272">Compile and test the application</span></span>

<span data-ttu-id="5bf23-273">**修改 XAML 檔案**</span><span class="sxs-lookup"><span data-stu-id="5bf23-273">**To modify the XAML file**</span></span>

1. <span data-ttu-id="5bf23-274">從 [方案總管] 中，在 [MainPage.xaml] 上按一下滑鼠右鍵，然後按一下 [檢視設計工具]。</span><span class="sxs-lookup"><span data-stu-id="5bf23-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="5bf23-275">找到 &lt;Grid.RowDefinitions&gt;，並修改 RowDefinitions，讓它們看起來如下：</span><span class="sxs-lookup"><span data-stu-id="5bf23-275">Locate &lt;Grid.RowDefinitions&gt;, and modify the RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="5bf23-276">在 &lt;Grid&gt;&lt;/Grid&gt; 標籤內，新增下列程式碼以定義 listbox 控制項，讓使用者可以看到可用資料流清單並選取資料流：</span><span class="sxs-lookup"><span data-stu-id="5bf23-276">Inside the &lt;Grid&gt;&lt;/Grid&gt; tags, add the following code to define a listbox control, so users can see the list of available streams, and select streams:</span></span>

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
4. <span data-ttu-id="5bf23-277">按 **CTRL+S** 儲存變更。</span><span class="sxs-lookup"><span data-stu-id="5bf23-277">Press **CTRL+S** to save the changes.</span></span>

<span data-ttu-id="5bf23-278">**修改程式碼後置檔案**</span><span class="sxs-lookup"><span data-stu-id="5bf23-278">**To modify the code behind file**</span></span>

1. <span data-ttu-id="5bf23-279">從 [方案總管] 中，在 [MainPage.xaml] 上按一下滑鼠右鍵，然後按一下 [檢視程式碼]。</span><span class="sxs-lookup"><span data-stu-id="5bf23-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="5bf23-280">在 SSPlayer 命名空間內，新增類別：</span><span class="sxs-lookup"><span data-stu-id="5bf23-280">Inside the SSPlayer namespace, add a new class:</span></span>
   
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
                    // mMke the video stream always checked.
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
3. <span data-ttu-id="5bf23-281">在 MainPage 類別的開頭，新增下列變數定義：</span><span class="sxs-lookup"><span data-stu-id="5bf23-281">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="5bf23-282">在 MainPage 類別內，新增下列區域：</span><span class="sxs-lookup"><span data-stu-id="5bf23-282">Inside the MainPage class, add the following region:</span></span>
   
        #region stream selection
        ///<summary>
        ///Functionality to select streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from the mediaElement_ManifestReady event handler 
        // to retrieve the streams and populate them to the local data members.
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
   
                    //populate the stream lists based on the types
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
   
                    // Select the default selected streams from the manifest.
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
   
        // This function set the list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update the stream check box list on the UI
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
   
            // Select the frist video stream from the list if no video stream is selected
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
                    txtStatus.Text = "The audio stream is changed to " + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select the frist audio stream from the list if no audio steam is selected.
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
5. <span data-ttu-id="5bf23-283">找到 mediaElement_ManifestReady 方法，並在函數的結尾附加下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="5bf23-283">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="5bf23-284">因此，當 MediaElement 資訊清單就緒時，程式碼會取得可用資料流清單，並將這份清單填入 UI 清單方塊。</span><span class="sxs-lookup"><span data-stu-id="5bf23-284">So when MediaElement manifest is ready, the code gets a list of the available streams, and populates the UI list box with the list.</span></span>
6. <span data-ttu-id="5bf23-285">在 MainPage 類別中，找到 UI 按鈕並按一下事件區域，再新增下列函式定義：
</span><span class="sxs-lookup"><span data-stu-id="5bf23-285">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on the presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="5bf23-286">**編譯和測試應用程式**</span><span class="sxs-lookup"><span data-stu-id="5bf23-286">**To compile and test the application**</span></span>

1. <span data-ttu-id="5bf23-287">按 **F6** 鍵編譯專案。</span><span class="sxs-lookup"><span data-stu-id="5bf23-287">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="5bf23-288">按 **F5** 鍵執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf23-288">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="5bf23-289">在應用程式頂端，您可以使用預設 Smooth Streaming URL，或輸入不同的 Smooth Streaming URL。</span><span class="sxs-lookup"><span data-stu-id="5bf23-289">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="5bf23-290">按一下 [設定來源] 。</span><span class="sxs-lookup"><span data-stu-id="5bf23-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="5bf23-291">預設語言為 audio_eng。</span><span class="sxs-lookup"><span data-stu-id="5bf23-291">The default language is audio_eng.</span></span> <span data-ttu-id="5bf23-292">嘗試在 audio_eng 與 audio_es 之間切換。</span><span class="sxs-lookup"><span data-stu-id="5bf23-292">Try to switch between audio_eng and audio_es.</span></span> <span data-ttu-id="5bf23-293">每次您選取新的資料流時，都必須按一下 [提交] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5bf23-293">Everytime, you select a new stream, you must click the Submit button.</span></span>

<span data-ttu-id="5bf23-294">您已完成課程 3。</span><span class="sxs-lookup"><span data-stu-id="5bf23-294">You have completed lesson 3.</span></span>  <span data-ttu-id="5bf23-295">在本課程中，您新增了選擇資料流的功能。</span><span class="sxs-lookup"><span data-stu-id="5bf23-295">In this lesson, you add the functionality to choose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="5bf23-296">課程 4：選取 Smooth Streaming 曲目</span><span class="sxs-lookup"><span data-stu-id="5bf23-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="5bf23-297">Smooth Streaming 簡報可以包含多個以不同品質等級 (位元速率) 和解析度編碼的視訊檔案。</span><span class="sxs-lookup"><span data-stu-id="5bf23-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="5bf23-298">在本課程中，您將讓使用者選取曲目。</span><span class="sxs-lookup"><span data-stu-id="5bf23-298">In this lesson, you will enable users to select tracks.</span></span> <span data-ttu-id="5bf23-299">本課程包含下列程序：</span><span class="sxs-lookup"><span data-stu-id="5bf23-299">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="5bf23-300">修改 XAML 檔案</span><span class="sxs-lookup"><span data-stu-id="5bf23-300">Modify the XAML file</span></span>
2. <span data-ttu-id="5bf23-301">修改程式碼後置檔案</span><span class="sxs-lookup"><span data-stu-id="5bf23-301">Modify the code behand file</span></span>
3. <span data-ttu-id="5bf23-302">編譯和測試應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf23-302">Compile and test the application</span></span>

<span data-ttu-id="5bf23-303">**修改 XAML 檔案**</span><span class="sxs-lookup"><span data-stu-id="5bf23-303">**To modify the XAML file**</span></span>

1. <span data-ttu-id="5bf23-304">從 [方案總管] 中，在 [MainPage.xaml] 上按一下滑鼠右鍵，然後按一下 [檢視設計工具]。</span><span class="sxs-lookup"><span data-stu-id="5bf23-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="5bf23-305">找到名稱為 **gridStreamAndBitrateSelection** 的 &lt;Grid&gt; 標籤，並在標籤的結尾附加下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="5bf23-305">Locate the &lt;Grid&gt; tag with the name **gridStreamAndBitrateSelection**, append the following code at the end of the tag:</span></span>
   
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
3. <span data-ttu-id="5bf23-306">按 **CTRL+S** 儲存變更。</span><span class="sxs-lookup"><span data-stu-id="5bf23-306">Press **CTRL+S** to save he changes</span></span>

<span data-ttu-id="5bf23-307">**修改程式碼後置檔案**</span><span class="sxs-lookup"><span data-stu-id="5bf23-307">**To modify the code behind file**</span></span>

1. <span data-ttu-id="5bf23-308">從 [方案總管] 中，在 [MainPage.xaml] 上按一下滑鼠右鍵，然後按一下 [檢視程式碼]。</span><span class="sxs-lookup"><span data-stu-id="5bf23-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="5bf23-309">在 SSPlayer 命名空間內，新增類別：</span><span class="sxs-lookup"><span data-stu-id="5bf23-309">Inside the SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="5bf23-310">在 MainPage 類別的開頭，新增下列變數定義：</span><span class="sxs-lookup"><span data-stu-id="5bf23-310">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="5bf23-311">在 MainPage 類別內，新增下列區域：</span><span class="sxs-lookup"><span data-stu-id="5bf23-311">Inside the MainPage class, add the following region:</span></span>
   
        #region track selection
        /// <summary>
        /// Functionality to select video streams
        /// </summary>
   
        /// This Function gets the tracks for the selected video stream
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
   
        // This function gets the video stream that is playing
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
   
        // This function set the UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update the track check box list on the UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of the selected tracks.
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
   
        // This function selects the tracks based on user selection 
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
5. <span data-ttu-id="5bf23-312">找到 mediaElement_ManifestReady 方法，並在函數的結尾附加下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="5bf23-312">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="5bf23-313">在 MainPage 類別中，找到 UI 按鈕並按一下事件區域，再新增下列函式定義：
</span><span class="sxs-lookup"><span data-stu-id="5bf23-313">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on the presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="5bf23-314">**編譯和測試應用程式**</span><span class="sxs-lookup"><span data-stu-id="5bf23-314">**To compile and test the application**</span></span>

1. <span data-ttu-id="5bf23-315">按 **F6** 鍵編譯專案。</span><span class="sxs-lookup"><span data-stu-id="5bf23-315">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="5bf23-316">按 **F5** 鍵執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf23-316">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="5bf23-317">在應用程式頂端，您可以使用預設 Smooth Streaming URL，或輸入不同的 Smooth Streaming URL。</span><span class="sxs-lookup"><span data-stu-id="5bf23-317">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="5bf23-318">按一下 [設定來源] 。</span><span class="sxs-lookup"><span data-stu-id="5bf23-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="5bf23-319">預設會選取視訊資料流的所有曲目。</span><span class="sxs-lookup"><span data-stu-id="5bf23-319">By default, all of the tracks of the video stream are selected.</span></span> <span data-ttu-id="5bf23-320">若要試驗位元速率變更，您可以選取可用的最低位元速率，然後選取可用的最高位元速率。</span><span class="sxs-lookup"><span data-stu-id="5bf23-320">To experiment the bit rate changes, you can select the lowest bit rate available, and then select the highest bit rate available.</span></span> <span data-ttu-id="5bf23-321">您必須在每次變更之後按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="5bf23-321">You must click Submit after each change.</span></span>  <span data-ttu-id="5bf23-322">您可以看到視訊品質變更。</span><span class="sxs-lookup"><span data-stu-id="5bf23-322">You can see the video quality changes.</span></span>

<span data-ttu-id="5bf23-323">您已完成課程 4。</span><span class="sxs-lookup"><span data-stu-id="5bf23-323">You have completed lesson 4.</span></span>  <span data-ttu-id="5bf23-324">在本課程中，您新增了選擇追蹤的功能。</span><span class="sxs-lookup"><span data-stu-id="5bf23-324">In this lesson, you add the functionality to choose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="5bf23-325">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="5bf23-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5bf23-326">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="5bf23-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="5bf23-327">其他資源：</span><span class="sxs-lookup"><span data-stu-id="5bf23-327">Other Resources:</span></span>
* [<span data-ttu-id="5bf23-328">如何建置具有進階功能的 Smooth Streaming Windows 8 JavaScript 應用程式 (英文)</span><span class="sxs-lookup"><span data-stu-id="5bf23-328">How to build a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="5bf23-329">Smooth Streaming 技術概觀 (英文)</span><span class="sxs-lookup"><span data-stu-id="5bf23-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

