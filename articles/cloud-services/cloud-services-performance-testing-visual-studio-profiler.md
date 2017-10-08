---
title: "雲端服務在本機 hello 計算模擬器中 aaaProfiling |Microsoft 文件"
services: cloud-services
description: "與 hello Visual Studio 分析工具調查雲端服務中的效能問題"
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
tags: 
ms.assetid: 25e40bf3-eea0-4b0b-9f4a-91ffe797f6c3
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: fc37c85dad4db4cc0310f73afad56fc0fe5f3963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a><span data-ttu-id="08db2-103">在 hello Azure 計算模擬器使用 hello Visual Studio 分析工具中測試 hello 的雲端服務在本機的效能</span><span class="sxs-lookup"><span data-stu-id="08db2-103">Testing hello Performance of a Cloud Service Locally in hello Azure Compute Emulator Using hello Visual Studio Profiler</span></span>
<span data-ttu-id="08db2-104">各種不同的工具和技術可供測試的雲端服務的 hello 效能。</span><span class="sxs-lookup"><span data-stu-id="08db2-104">A variety of tools and techniques are available for testing hello performance of cloud services.</span></span>
<span data-ttu-id="08db2-105">當您發行雲端服務 tooAzure 時，您可以收集分析資料，然後進行分析的 Visual Studio 在本機中所述[Azure 應用程式程式碼剖析][1]。</span><span class="sxs-lookup"><span data-stu-id="08db2-105">When you publish a cloud service tooAzure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="08db2-106">您也可以使用各種不同的效能計數器，診斷 tootrack 中, 所述[在 Azure 中使用效能計數器][2]。</span><span class="sxs-lookup"><span data-stu-id="08db2-106">You can also use diagnostics tootrack a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="08db2-107">您也可能想 tooprofile hello 計算模擬器中的本機應用程式再將其部署 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="08db2-107">You might also want tooprofile your application locally in hello compute emulator before deploying it toohello cloud.</span></span>

<span data-ttu-id="08db2-108">本文涵蓋 hello CPU 取樣程式碼剖析方法，能夠以 hello 模擬器在本機完成。</span><span class="sxs-lookup"><span data-stu-id="08db2-108">This article covers hello CPU Sampling method of profiling, which can be done locally in hello emulator.</span></span> <span data-ttu-id="08db2-109">CPU 取樣不是非常侵入式的分析方法。</span><span class="sxs-lookup"><span data-stu-id="08db2-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="08db2-110">指定的取樣間隔 hello 分析工具會擷取 hello 呼叫堆疊的快照。</span><span class="sxs-lookup"><span data-stu-id="08db2-110">At a designated sampling interval, hello profiler takes a snapshot of hello call stack.</span></span> <span data-ttu-id="08db2-111">hello 資料需要經過一段時間，收集及顯示報表中。</span><span class="sxs-lookup"><span data-stu-id="08db2-111">hello data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="08db2-112">這種程式碼剖析方法通常會 tooindicate 其中密集的應用程式中大部分的 hello CPU 工作進行，則為。</span><span class="sxs-lookup"><span data-stu-id="08db2-112">This method of profiling tends tooindicate where in a computationally intensive application most of hello CPU work is being done.</span></span>  <span data-ttu-id="08db2-113">這讓您在 hello 機會 toofocus hello [最忙碌路徑]，其中您的應用程式花 hello 最多時間。</span><span class="sxs-lookup"><span data-stu-id="08db2-113">This gives you hello opportunity toofocus on hello "hot path" where your application is spending hello most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="08db2-114">1：設定 Visual Studio 進行分析</span><span class="sxs-lookup"><span data-stu-id="08db2-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="08db2-115">首先，有些 Visual Studio 組態選項可能在進行分析時很實用。</span><span class="sxs-lookup"><span data-stu-id="08db2-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="08db2-116">toomake 意義 hello 分析報告，您將需要符號 （.pdb 檔案），您的應用程式以及系統程式庫的符號。</span><span class="sxs-lookup"><span data-stu-id="08db2-116">toomake sense of hello profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="08db2-117">您會想 toomake 確定您參考 hello 使用符號伺服器。</span><span class="sxs-lookup"><span data-stu-id="08db2-117">You'll want toomake sure that you reference hello available symbol servers.</span></span> <span data-ttu-id="08db2-118">toodo 這在 hello**工具**在 Visual Studio 的功能表中選擇 **選項**，然後選擇 **偵錯**，然後**符號**。</span><span class="sxs-lookup"><span data-stu-id="08db2-118">toodo this, on hello **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="08db2-119">請確定 Microsoft Symbol Servers 列在 [符號檔 (.pdb) 位置] 下方。</span><span class="sxs-lookup"><span data-stu-id="08db2-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="08db2-120">您也可以參考 http://referencesource.microsoft.com/symbols，其中可能有其他符號檔案。</span><span class="sxs-lookup"><span data-stu-id="08db2-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![符號選項][4]

<span data-ttu-id="08db2-122">如有需要，您可以簡化 hello 會報告該 hello 分析工具會產生藉由設定 Just My Code。</span><span class="sxs-lookup"><span data-stu-id="08db2-122">If desired, you can simplify hello reports that hello profiler generates by setting Just My Code.</span></span> <span data-ttu-id="08db2-123">啟用 Just My Code，與函式的呼叫堆疊已經過簡化，以便呼叫完全內部 toolibraries 而 hello.NET Framework 會隱藏 hello 報表。</span><span class="sxs-lookup"><span data-stu-id="08db2-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal toolibraries and hello .NET Framework are hidden from hello reports.</span></span> <span data-ttu-id="08db2-124">在 hello**工具**功能表上，選擇**選項**。</span><span class="sxs-lookup"><span data-stu-id="08db2-124">On hello **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="08db2-125">然後展開 hello**效能工具** 節點，然後選擇 **一般**。</span><span class="sxs-lookup"><span data-stu-id="08db2-125">Then expand hello **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="08db2-126">選取 hello 核取方塊**啟用 Just My Code 以進行分析工具報告**。</span><span class="sxs-lookup"><span data-stu-id="08db2-126">Select hello checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Just My Code 選項][17]

<span data-ttu-id="08db2-128">您可以將這些指示與現有專案或新的專案搭配使用。</span><span class="sxs-lookup"><span data-stu-id="08db2-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="08db2-129">如果您建立新的專案 tootry hello 如下所述的技巧，選擇 C# **Azure 雲端服務**專案，然後選取**Web 角色**和**背景工作角色**。</span><span class="sxs-lookup"><span data-stu-id="08db2-129">If you create a new project tootry hello techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Azure 雲端服務專案角色][5]

<span data-ttu-id="08db2-131">比方說的目的，將某些程式碼 tooyour 專案會耗用大量時間，並示範一些明顯的效能問題。</span><span class="sxs-lookup"><span data-stu-id="08db2-131">For example purposes, add some code tooyour project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="08db2-132">例如，加入下列程式碼 tooa 背景工作角色專案的 hello:</span><span class="sxs-lookup"><span data-stu-id="08db2-132">For example, add hello following code tooa worker role project:</span></span>

    public class Concatenator
    {
        public static string Concatenate(int number)
        {
            int count;
            string s = "";
            for (count = 0; count < number; count++)
            {
                s += "\n" + count.ToString();
            }
            return s;
        }
    }

<span data-ttu-id="08db2-133">呼叫此程式碼從 hello RunAsync hello 背景工作角色的 RoleEntryPoint 衍生類別中的方法。</span><span class="sxs-lookup"><span data-stu-id="08db2-133">Call this code from hello RunAsync method in hello worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="08db2-134">（忽略 hello 警告 hello 方法以同步方式執行）。</span><span class="sxs-lookup"><span data-stu-id="08db2-134">(Ignore hello warning about hello method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="08db2-135">建置並搭配 hello 的方案組態設定得您的雲端服務在本機執行但不偵錯 (Ctrl + F5)，**發行**。</span><span class="sxs-lookup"><span data-stu-id="08db2-135">Build and run your cloud service locally without debugging (Ctrl+F5), with hello solution configuration set too**Release**.</span></span> <span data-ttu-id="08db2-136">這可確保所有檔案和資料夾會建立在本機執行 hello 應用程式，並可確保所有 hello 模擬器已都啟動。</span><span class="sxs-lookup"><span data-stu-id="08db2-136">This ensures that all files and folders are created for running hello application locally, and ensures that all hello emulators are started.</span></span> <span data-ttu-id="08db2-137">請從背景工作角色執行的 hello 工作列 tooverify 啟動 hello 計算模擬器 UI。</span><span class="sxs-lookup"><span data-stu-id="08db2-137">Start hello Compute Emulator UI from hello taskbar tooverify that your worker role is running.</span></span>

## <a name="2-attach-tooa-process"></a><span data-ttu-id="08db2-138">2： 附加 tooa 處理序</span><span class="sxs-lookup"><span data-stu-id="08db2-138">2: Attach tooa process</span></span>
<span data-ttu-id="08db2-139">除了啟動從 hello Visual Studio 2010 IDE 來分析 hello 應用程式，您必須將附加 hello profiler tooa 執行程序。</span><span class="sxs-lookup"><span data-stu-id="08db2-139">Instead of profiling hello application by starting it from hello Visual Studio 2010 IDE, you must attach hello profiler tooa running process.</span></span> 

<span data-ttu-id="08db2-140">tooattach hello profiler tooa 程序，在 hello**分析**功能表上，選擇**Profiler**和**附加/卸離**。</span><span class="sxs-lookup"><span data-stu-id="08db2-140">tooattach hello profiler tooa process, on hello **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![附加設定檔選項][6]

<span data-ttu-id="08db2-142">背景工作角色中，尋找 hello WaWorkerHost.exe 程序。</span><span class="sxs-lookup"><span data-stu-id="08db2-142">For a worker role, find hello WaWorkerHost.exe process.</span></span>

![WaWorkerHost 程序][7]

<span data-ttu-id="08db2-144">如果您的專案資料夾位於網路磁碟機，hello 分析工具會要求您 tooprovide 程式碼剖析報告的另一個位置 toosave hello。</span><span class="sxs-lookup"><span data-stu-id="08db2-144">If your project folder is on a network drive, hello profiler will ask you tooprovide another location toosave hello profiling reports.</span></span>

 <span data-ttu-id="08db2-145">您也可以藉由附加 tooWaIISHost.exe 附加 tooa web 角色。</span><span class="sxs-lookup"><span data-stu-id="08db2-145">You can also attach tooa web role by attaching tooWaIISHost.exe.</span></span>
<span data-ttu-id="08db2-146">如果您的應用程式中有多個背景工作角色處理序，您需要 toouse hello processID toodistinguish 它們。</span><span class="sxs-lookup"><span data-stu-id="08db2-146">If there are multiple worker role processes in your application, you need toouse hello processID toodistinguish them.</span></span> <span data-ttu-id="08db2-147">您可以藉由存取 hello 處理程序物件，以程式設計方式查詢 hello processID。</span><span class="sxs-lookup"><span data-stu-id="08db2-147">You can query hello processID programmatically by accessing hello Process object.</span></span> <span data-ttu-id="08db2-148">比方說，如果您在角色中加入 hello RoleEntryPoint 衍生類別的這個程式碼 toohello Run 方法，您可以查看記錄檔中 hello 計算模擬器 UI tooknow 以何種處理程序 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="08db2-148">For example, if you add this code toohello Run method of hello RoleEntryPoint-derived class in a role, you can look at the log in hello Compute Emulator UI tooknow what process tooconnect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="08db2-149">開始 hello 計算模擬器 UI tooview hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="08db2-149">tooview hello log, start hello Compute Emulator UI.</span></span>

![啟動 hello 計算模擬器 UI][8]

<span data-ttu-id="08db2-151">Hello 背景工作角色記錄主控台視窗 hello 計算模擬器 UI 中按一下來開啟 hello 主控台視窗的標題列上。</span><span class="sxs-lookup"><span data-stu-id="08db2-151">Open hello worker role log console window in hello Compute Emulator UI by clicking on hello console window's title bar.</span></span> <span data-ttu-id="08db2-152">您可以看到 hello hello 記錄檔中的處理序識別碼。</span><span class="sxs-lookup"><span data-stu-id="08db2-152">You can see hello process ID in hello log.</span></span>

![檢視處理序識別碼][9]

<span data-ttu-id="08db2-154">您已經附加，一個在您的應用程式 UI （如有需要） tooreproduce hello 案例中執行 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="08db2-154">One you've attached, perform hello steps in your application's UI (if needed) tooreproduce hello scenario.</span></span>

<span data-ttu-id="08db2-155">當您想 toostop 程式碼剖析時，請選擇 hello**停止程式碼剖析**連結。</span><span class="sxs-lookup"><span data-stu-id="08db2-155">When you want toostop profiling, choose hello **Stop Profiling** link.</span></span>

![停止分析選項][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="08db2-157">3：檢視效能報告</span><span class="sxs-lookup"><span data-stu-id="08db2-157">3: View performance reports</span></span>
<span data-ttu-id="08db2-158">您的應用程式的 hello 效能報表會顯示。</span><span class="sxs-lookup"><span data-stu-id="08db2-158">hello performance report for your application is displayed.</span></span>

<span data-ttu-id="08db2-159">此時，hello 分析工具會停止執行，將資料儲存在.vsp 檔，並顯示的報表會顯示此資料的分析。</span><span class="sxs-lookup"><span data-stu-id="08db2-159">At this point, hello profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![分析工具報告][11]

<span data-ttu-id="08db2-161">如果您看到 String.wstrcpy hello 中最忙碌路徑] 中，按一下 [Just My Code toochange hello 檢視 tooshow 使用者程式碼。</span><span class="sxs-lookup"><span data-stu-id="08db2-161">If you see String.wstrcpy in hello Hot Path, click on Just My Code toochange hello view tooshow user code only.</span></span>  <span data-ttu-id="08db2-162">如果您看到 String.Concat，再試一次按下 hello 顯示所有程式碼 按鈕。</span><span class="sxs-lookup"><span data-stu-id="08db2-162">If you see String.Concat, try pressing hello Show All Code button.</span></span>

<span data-ttu-id="08db2-163">您應該會看到 hello 串連方法和 String.Concat 佔用大量 hello 執行時間。</span><span class="sxs-lookup"><span data-stu-id="08db2-163">You should see hello Concatenate method and String.Concat taking up a large portion of hello execution time.</span></span>

![報告的分析][12]

<span data-ttu-id="08db2-165">如果您在本文中加入 hello 字串串連的程式碼，您應該會看到這個 hello 工作清單中的警告。</span><span class="sxs-lookup"><span data-stu-id="08db2-165">If you added hello string concatenation code in this article, you should see a warning in hello Task List for this.</span></span> <span data-ttu-id="08db2-166">您也可能會看到警告，表示過量的記憶體回收，這是因為 toohello 數字的字串，建立和處置。</span><span class="sxs-lookup"><span data-stu-id="08db2-166">You may also see a warning that there is an excessive amount of garbage collection, which is due toohello number of strings that are created and disposed.</span></span>

![效能警告][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="08db2-168">4：進行變更與比較效能</span><span class="sxs-lookup"><span data-stu-id="08db2-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="08db2-169">您也可以比較程式碼變更之前和之後的 hello 效能。</span><span class="sxs-lookup"><span data-stu-id="08db2-169">You can also compare hello performance before and after a code change.</span></span>  <span data-ttu-id="08db2-170">停止 hello 執行程序，並編輯 hello 碼 tooreplace hello 字串串連運算 hello 使用 StringBuilder 的：</span><span class="sxs-lookup"><span data-stu-id="08db2-170">Stop hello running process, and edit hello code tooreplace hello string concatenation operation with hello use of StringBuilder:</span></span>

    public static string Concatenate(int number)
    {
        int count;
        System.Text.StringBuilder builder = new System.Text.StringBuilder("");
        for (count = 0; count < number; count++)
        {
             builder.Append("\n" + count.ToString());
        }
        return builder.ToString();
    }

<span data-ttu-id="08db2-171">執行另一個回合的效能測試，然後和比較 hello 效能。</span><span class="sxs-lookup"><span data-stu-id="08db2-171">Do another performance run, and then compare hello performance.</span></span> <span data-ttu-id="08db2-172">在 [hello 效能總管] 中，如果 hello 執行位於 hello 相同工作階段，您可以只選取兩個報表，開啟 hello 捷徑功能表，並選擇**比較效能報告**。</span><span class="sxs-lookup"><span data-stu-id="08db2-172">In hello Performance Explorer, if hello runs are in hello same session, you can just select both reports, open hello shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="08db2-173">如果您想 toocompare 與另一個效能工作階段中執行，請開啟 hello**分析**功能表上，選擇 **比較效能報告**。</span><span class="sxs-lookup"><span data-stu-id="08db2-173">If you want toocompare with a run in another performance session, open hello **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="08db2-174">在出現的 hello 對話方塊方塊中指定這兩個檔案。</span><span class="sxs-lookup"><span data-stu-id="08db2-174">Specify both files in hello dialog box that appears.</span></span>

![比較效能報告選項][15]

<span data-ttu-id="08db2-176">hello 報表反白顯示 hello 兩次執行之間的差異。</span><span class="sxs-lookup"><span data-stu-id="08db2-176">hello reports highlight differences between hello two runs.</span></span>

![比較報告][16]

<span data-ttu-id="08db2-178">恭喜！</span><span class="sxs-lookup"><span data-stu-id="08db2-178">Congratulations!</span></span> <span data-ttu-id="08db2-179">您開始使用與 hello 分析工具。</span><span class="sxs-lookup"><span data-stu-id="08db2-179">You've gotten started with hello profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="08db2-180">疑難排解</span><span class="sxs-lookup"><span data-stu-id="08db2-180">Troubleshooting</span></span>
* <span data-ttu-id="08db2-181">確定您正在分析發行組建並開始而不進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="08db2-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="08db2-182">如果 hello 附加/卸離選項未啟用 hello 分析工具 功能表上，執行 hello 效能精靈。</span><span class="sxs-lookup"><span data-stu-id="08db2-182">If hello Attach/Detach option is not enabled on hello Profiler menu, run hello Performance Wizard.</span></span>
* <span data-ttu-id="08db2-183">使用應用程式的 hello 計算模擬器 UI tooview hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="08db2-183">Use hello Compute Emulator UI tooview hello status of your application.</span></span> 
* <span data-ttu-id="08db2-184">如果您有在 hello 模擬器中啟動應用程式的問題，或附加 hello 程式碼剖析工具，關閉 hello 計算模擬器，然後重新啟動它。</span><span class="sxs-lookup"><span data-stu-id="08db2-184">If you have problems starting applications in hello emulator, or attaching hello profiler, shut down hello compute emulator and restart it.</span></span> <span data-ttu-id="08db2-185">如果無法解決 hello 問題，請嘗試重新啟動。</span><span class="sxs-lookup"><span data-stu-id="08db2-185">If that doesn't solve hello problem, try rebooting.</span></span> <span data-ttu-id="08db2-186">如果您使用 hello 計算模擬器 toosuspend 和移除執行中部署，可能會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="08db2-186">This problem can occur if you use hello Compute Emulator toosuspend and remove running deployments.</span></span>
* <span data-ttu-id="08db2-187">如果您有使用任何命令，從命令列程式碼剖析的 hello，特別是 hello 全域設定，確定已呼叫 VSPerfClrEnv /globaloff VsPerfMon.exe 已關閉。</span><span class="sxs-lookup"><span data-stu-id="08db2-187">If you have used any of hello profiling commands from the command line, especially hello global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="08db2-188">如果在取樣，您會看見 hello 訊息 「 PRF0025： 未收集任何資料，「 hello 附加 toohas CPU 活動的程序的核取。</span><span class="sxs-lookup"><span data-stu-id="08db2-188">If when sampling, you see hello message "PRF0025: No data was collected," check that hello process you attached toohas CPU activity.</span></span> <span data-ttu-id="08db2-189">未執行任何計算工作的應用程式可能不會產生任何取樣資料。</span><span class="sxs-lookup"><span data-stu-id="08db2-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="08db2-190">此外，也可以 hello 處理序結束之前已完成的任何取樣。</span><span class="sxs-lookup"><span data-stu-id="08db2-190">It's also possible that hello process exited before any sampling was done.</span></span> <span data-ttu-id="08db2-191">Hello Run 方法，用於您要分析的角色的核取 toosee 不會終止。</span><span class="sxs-lookup"><span data-stu-id="08db2-191">Check toosee that hello Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08db2-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="08db2-192">Next Steps</span></span>
<span data-ttu-id="08db2-193">檢測 Azure hello 模擬器中的二進位檔不支援在 hello Visual Studio 分析工具，但如果您想 tootest 記憶體配置時，程式碼剖析時，您可以選擇該選項。</span><span class="sxs-lookup"><span data-stu-id="08db2-193">Instrumenting Azure binaries in hello emulator is not supported in hello Visual Studio profiler, but if you want tootest memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="08db2-194">您也可以選擇並行分析，這可協助您判斷執行緒是否會浪費時間競爭鎖定，或階層互動分析，這可協助您追蹤效能問題的應用程式層之間的互動時最經常之間 hello 資料層和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="08db2-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between hello data tier and a worker role.</span></span>  <span data-ttu-id="08db2-195">您可以檢視您的應用程式產生的 hello 資料庫查詢，並使用程式碼剖析資料 tooimprove hello 資料庫貴用戶使用的 hello。</span><span class="sxs-lookup"><span data-stu-id="08db2-195">You can view hello database queries that your app generates and use hello profiling data tooimprove your use of hello database.</span></span> <span data-ttu-id="08db2-196">如需階層互動分析資訊，請參閱 hello 部落格文章[逐步解說： 使用 hello 階層互動分析工具，在 Visual Studio Team System 2010][3]。</span><span class="sxs-lookup"><span data-stu-id="08db2-196">For information about tier interaction profiling, see hello blog post [Walkthrough: Using hello Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

[1]: http://msdn.microsoft.com/library/azure/hh369930.aspx
[2]: http://msdn.microsoft.com/library/azure/hh411542.aspx
[3]: http://blogs.msdn.com/b/habibh/archive/2009/06/30/walkthrough-using-the-tier-interaction-profiler-in-visual-studio-team-system-2010.aspx
[4]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally09.png
[5]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally10.png
[6]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally02.png
[7]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally05.png
[8]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally010.png
[9]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally07.png
[10]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally06.png
[11]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally03.png
[12]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally011.png
[14]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally04.png 
[15]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally013.png
[16]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally012.png
[17]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally08.png
