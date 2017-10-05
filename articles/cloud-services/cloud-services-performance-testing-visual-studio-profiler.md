---
title: "在本機的計算模擬器中分析雲端服務 | Microsoft Docs"
services: cloud-services
description: "使用 Visual Studio 分析工具調查雲端服務中的效能問題"
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
ms.openlocfilehash: 51c8192d8312dc5cf546b4c357aeecf6f19d56b8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="testing-the-performance-of-a-cloud-service-locally-in-the-azure-compute-emulator-using-the-visual-studio-profiler"></a><span data-ttu-id="5292e-103">使用 Visual Studio 分析工具，在 Azure 計算模擬器中本機測試雲端服務的效能</span><span class="sxs-lookup"><span data-stu-id="5292e-103">Testing the Performance of a Cloud Service Locally in the Azure Compute Emulator Using the Visual Studio Profiler</span></span>
<span data-ttu-id="5292e-104">各種工具和技術可用於測試雲端服務的效能。</span><span class="sxs-lookup"><span data-stu-id="5292e-104">A variety of tools and techniques are available for testing the performance of cloud services.</span></span>
<span data-ttu-id="5292e-105">當您將雲端服務發佈至 Azure 時，可以讓 Visual Studio 收集分析資料，然後在本機分析它 (如[分析雲端服務][11] 中所述)。</span><span class="sxs-lookup"><span data-stu-id="5292e-105">When you publish a cloud service to Azure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="5292e-106">您也可以使用診斷來追蹤各種效能計數器 (如[在 Azure 中使用效能計數器][2]中所述)。</span><span class="sxs-lookup"><span data-stu-id="5292e-106">You can also use diagnostics to track a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="5292e-107">您也可能想要先在計算模擬器中本機分析應用程式，再將之部署至雲端。</span><span class="sxs-lookup"><span data-stu-id="5292e-107">You might also want to profile your application locally in the compute emulator before deploying it to the cloud.</span></span>

<span data-ttu-id="5292e-108">本文涵蓋進行分析的「CPU 取樣」方法，這可以在模擬器上本機完成。</span><span class="sxs-lookup"><span data-stu-id="5292e-108">This article covers the CPU Sampling method of profiling, which can be done locally in the emulator.</span></span> <span data-ttu-id="5292e-109">CPU 取樣不是非常侵入式的分析方法。</span><span class="sxs-lookup"><span data-stu-id="5292e-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="5292e-110">分析工具會按指定的取樣間隔取得呼叫堆疊的快照集。</span><span class="sxs-lookup"><span data-stu-id="5292e-110">At a designated sampling interval, the profiler takes a snapshot of the call stack.</span></span> <span data-ttu-id="5292e-111">會收集一段時間的資料，而且資料會顯示在報告中。</span><span class="sxs-lookup"><span data-stu-id="5292e-111">The data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="5292e-112">此分析方法傾向指出在計算密集應用程式中的哪個位置完成大部分的 CPU 工作。</span><span class="sxs-lookup"><span data-stu-id="5292e-112">This method of profiling tends to indicate where in a computationally intensive application most of the CPU work is being done.</span></span>  <span data-ttu-id="5292e-113">這可讓您有機會聚焦在應用程式耗用最多時間的「最忙碌路徑」。</span><span class="sxs-lookup"><span data-stu-id="5292e-113">This gives you the opportunity to focus on the "hot path" where your application is spending the most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="5292e-114">1：設定 Visual Studio 進行分析</span><span class="sxs-lookup"><span data-stu-id="5292e-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="5292e-115">首先，有些 Visual Studio 組態選項可能在進行分析時很實用。</span><span class="sxs-lookup"><span data-stu-id="5292e-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="5292e-116">若要讓分析報告發揮作用，您需要應用程式的符號 (.pdb 檔案)，也需要系統庫的符號。</span><span class="sxs-lookup"><span data-stu-id="5292e-116">To make sense of the profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="5292e-117">您會希望確定參考可用的符號伺服器。</span><span class="sxs-lookup"><span data-stu-id="5292e-117">You'll want to make sure that you reference the available symbol servers.</span></span> <span data-ttu-id="5292e-118">若要這樣做，請在 Visual Studio 的 [工具] 功能表上，依序選擇 [選項]、[偵錯] 和 [符號]。</span><span class="sxs-lookup"><span data-stu-id="5292e-118">To do this, on the **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="5292e-119">請確定 Microsoft Symbol Servers 列在 [符號檔 (.pdb) 位置] 下方。</span><span class="sxs-lookup"><span data-stu-id="5292e-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="5292e-120">您也可以參考 http://referencesource.microsoft.com/symbols，其中可能有其他符號檔案。</span><span class="sxs-lookup"><span data-stu-id="5292e-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![符號選項][4]

<span data-ttu-id="5292e-122">如有需要，您可以設定 Just My Code 來簡化分析工具所產生的報告。</span><span class="sxs-lookup"><span data-stu-id="5292e-122">If desired, you can simplify the reports that the profiler generates by setting Just My Code.</span></span> <span data-ttu-id="5292e-123">啟用 Just My Code 之後，會簡化函式呼叫堆疊，因此報告中會隱藏整個是程式庫和 .NET Framework 的內部呼叫。</span><span class="sxs-lookup"><span data-stu-id="5292e-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal to libraries and the .NET Framework are hidden from the reports.</span></span> <span data-ttu-id="5292e-124">在 [工具] 功能表上，選擇 [選項]。</span><span class="sxs-lookup"><span data-stu-id="5292e-124">On the **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="5292e-125">然後展開 [效能工具] 節點，並選擇 [一般]。</span><span class="sxs-lookup"><span data-stu-id="5292e-125">Then expand the **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="5292e-126">選取 [啟用 Just My Code 以進行分析工具報告] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5292e-126">Select the checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Just My Code 選項][17]

<span data-ttu-id="5292e-128">您可以將這些指示與現有專案或新的專案搭配使用。</span><span class="sxs-lookup"><span data-stu-id="5292e-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="5292e-129">如果您建立新的專案來嘗試上面所述的技術，請選擇 C# [Azure 雲端服務] 專案，然後選取 [Web 角色] 和 [背景工作角色]。</span><span class="sxs-lookup"><span data-stu-id="5292e-129">If you create a new project to try the techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Azure 雲端服務專案角色][5]

<span data-ttu-id="5292e-131">舉例來說，會在專案中新增某個程式碼，而這個程式碼耗用許多時間，並且示範某個明顯的效能問題。</span><span class="sxs-lookup"><span data-stu-id="5292e-131">For example purposes, add some code to your project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="5292e-132">例如，將下列程式碼新增至背景工作角色專案：</span><span class="sxs-lookup"><span data-stu-id="5292e-132">For example, add the following code to a worker role project:</span></span>

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

<span data-ttu-id="5292e-133">請在背景工作角色的 RoleEntryPoint 衍生類別中，從 RunAsync 方法呼叫此程式碼。</span><span class="sxs-lookup"><span data-stu-id="5292e-133">Call this code from the RunAsync method in the worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="5292e-134">(忽略有關同步執行方法的警告。)</span><span class="sxs-lookup"><span data-stu-id="5292e-134">(Ignore the warning about the method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace the following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="5292e-135">在方案組態設定為 [發行] 的情況下，在本機建置和執行雲端服務，而不要進行偵錯 (Ctrl+F5)。</span><span class="sxs-lookup"><span data-stu-id="5292e-135">Build and run your cloud service locally without debugging (Ctrl+F5), with the solution configuration set to **Release**.</span></span> <span data-ttu-id="5292e-136">這確保建立在本機執行應用程式的所有檔案和資料夾，並確保已啟動所有模擬器。</span><span class="sxs-lookup"><span data-stu-id="5292e-136">This ensures that all files and folders are created for running the application locally, and ensures that all the emulators are started.</span></span> <span data-ttu-id="5292e-137">從工作列啟動 Compute Emulator UI，以驗證您的背景工作角色執行中。</span><span class="sxs-lookup"><span data-stu-id="5292e-137">Start the Compute Emulator UI from the taskbar to verify that your worker role is running.</span></span>

## <a name="2-attach-to-a-process"></a><span data-ttu-id="5292e-138">2：連結至程序</span><span class="sxs-lookup"><span data-stu-id="5292e-138">2: Attach to a process</span></span>
<span data-ttu-id="5292e-139">您必須將分析工具連結至執行中程序，而不是從 Visual Studio 2010 IDE 啟動應用程式來分析應用程式。</span><span class="sxs-lookup"><span data-stu-id="5292e-139">Instead of profiling the application by starting it from the Visual Studio 2010 IDE, you must attach the profiler to a running process.</span></span> 

<span data-ttu-id="5292e-140">若要將分析工具連結至程序，請在 [分析] 功能表上選擇 [分析工具] 和 [連結/中斷連結]。</span><span class="sxs-lookup"><span data-stu-id="5292e-140">To attach the profiler to a process, on the **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![附加設定檔選項][6]

<span data-ttu-id="5292e-142">若為背景工作角色，請尋找 WaWorkerHost.exe 程序。</span><span class="sxs-lookup"><span data-stu-id="5292e-142">For a worker role, find the WaWorkerHost.exe process.</span></span>

![WaWorkerHost 程序][7]

<span data-ttu-id="5292e-144">如果您的專案資料夾位於網路磁碟機上，則分析工具會要求您提供另一個位置來儲存分析報告。</span><span class="sxs-lookup"><span data-stu-id="5292e-144">If your project folder is on a network drive, the profiler will ask you to provide another location to save the profiling reports.</span></span>

 <span data-ttu-id="5292e-145">您也可以藉由連結至 WaIISHost.exe 來連結至 Web 角色。</span><span class="sxs-lookup"><span data-stu-id="5292e-145">You can also attach to a web role by attaching to WaIISHost.exe.</span></span>
<span data-ttu-id="5292e-146">如果您的應用程式中有多個背景工作角色程序，則需使用 processID 進行區別。</span><span class="sxs-lookup"><span data-stu-id="5292e-146">If there are multiple worker role processes in your application, you need to use the processID to distinguish them.</span></span> <span data-ttu-id="5292e-147">您可以存取 Process 物件，以透過程式設計方式查詢 processID。</span><span class="sxs-lookup"><span data-stu-id="5292e-147">You can query the processID programmatically by accessing the Process object.</span></span> <span data-ttu-id="5292e-148">例如，如果您將此程式碼新增至角色中 RoleEntryPoint 衍生類別的 Run 方法，則可以查看計算模擬器 UI 中的記錄，得知要連線的程序。</span><span class="sxs-lookup"><span data-stu-id="5292e-148">For example, if you add this code to the Run method of the RoleEntryPoint-derived class in a role, you can look at the log in the Compute Emulator UI to know what process to connect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="5292e-149">若要檢視記錄，請啟動計算模擬器 UI。</span><span class="sxs-lookup"><span data-stu-id="5292e-149">To view the log, start the Compute Emulator UI.</span></span>

![啟動計算模擬器 UI][8]

<span data-ttu-id="5292e-151">按一下主控台視窗的標題列，以在計算模擬器 UI 中開啟背景工作角色記錄主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="5292e-151">Open the worker role log console window in the Compute Emulator UI by clicking on the console window's title bar.</span></span> <span data-ttu-id="5292e-152">您可以在記錄中看到程序 ID。</span><span class="sxs-lookup"><span data-stu-id="5292e-152">You can see the process ID in the log.</span></span>

![檢視處理序識別碼][9]

<span data-ttu-id="5292e-154">連結之後，請在應用程式 UI 中執行步驟 (需要時) 來重現案例。</span><span class="sxs-lookup"><span data-stu-id="5292e-154">One you've attached, perform the steps in your application's UI (if needed) to reproduce the scenario.</span></span>

<span data-ttu-id="5292e-155">當您想要停止分析時，請選擇 [停止分析] 連結。</span><span class="sxs-lookup"><span data-stu-id="5292e-155">When you want to stop profiling, choose the **Stop Profiling** link.</span></span>

![停止分析選項][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="5292e-157">3：檢視效能報告</span><span class="sxs-lookup"><span data-stu-id="5292e-157">3: View performance reports</span></span>
<span data-ttu-id="5292e-158">會顯示您應用程式的效能報告。</span><span class="sxs-lookup"><span data-stu-id="5292e-158">The performance report for your application is displayed.</span></span>

<span data-ttu-id="5292e-159">此時，分析工具會停止執行、以 .vsp 檔案儲存資料，並顯示可顯示此資料分析的報告。</span><span class="sxs-lookup"><span data-stu-id="5292e-159">At this point, the profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![分析工具報告][11]

<span data-ttu-id="5292e-161">如果您在「最忙碌路徑」中看到 String.wstrcpy，請按一下 Just My Code 變更檢視，只顯示使用者程式碼。</span><span class="sxs-lookup"><span data-stu-id="5292e-161">If you see String.wstrcpy in the Hot Path, click on Just My Code to change the view to show user code only.</span></span>  <span data-ttu-id="5292e-162">如果您看到 String.Concat，請嘗試按 [顯示所有程式碼] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5292e-162">If you see String.Concat, try pressing the Show All Code button.</span></span>

<span data-ttu-id="5292e-163">您應該會看到 Concatenate 方法和 String.Concat 耗用大部分的執行時間。</span><span class="sxs-lookup"><span data-stu-id="5292e-163">You should see the Concatenate method and String.Concat taking up a large portion of the execution time.</span></span>

![報告的分析][12]

<span data-ttu-id="5292e-165">如果您已在本文中新增字串串連碼，則應該會在 [工作清單] 中看到警告。</span><span class="sxs-lookup"><span data-stu-id="5292e-165">If you added the string concatenation code in this article, you should see a warning in the Task List for this.</span></span> <span data-ttu-id="5292e-166">您也可能會看到有大量記憶體回收的警告，原因是建立和處置的字串數目。</span><span class="sxs-lookup"><span data-stu-id="5292e-166">You may also see a warning that there is an excessive amount of garbage collection, which is due to the number of strings that are created and disposed.</span></span>

![效能警告][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="5292e-168">4：進行變更與比較效能</span><span class="sxs-lookup"><span data-stu-id="5292e-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="5292e-169">您也可以在變更程式碼之前和之後比較效能。</span><span class="sxs-lookup"><span data-stu-id="5292e-169">You can also compare the performance before and after a code change.</span></span>  <span data-ttu-id="5292e-170">請停止執行中流程並編輯程式碼，以使用 StringBuilder 取代字串串連作業：</span><span class="sxs-lookup"><span data-stu-id="5292e-170">Stop the running process, and edit the code to replace the string concatenation operation with the use of StringBuilder:</span></span>

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

<span data-ttu-id="5292e-171">請進行另一個效能執行，然後比較效能。</span><span class="sxs-lookup"><span data-stu-id="5292e-171">Do another performance run, and then compare the performance.</span></span> <span data-ttu-id="5292e-172">在 [效能總管] 中，如果這些執行都位於相同的工作階段中，則只能選取兩份報告，並開啟捷徑功能表，然後選擇 [比較效能報告]。</span><span class="sxs-lookup"><span data-stu-id="5292e-172">In the Performance Explorer, if the runs are in the same session, you can just select both reports, open the shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="5292e-173">如果您想要與另一個效能工作階段中的執行進行比較，請開啟 [分析] 功能表，然後選擇 [比較效能報告]。</span><span class="sxs-lookup"><span data-stu-id="5292e-173">If you want to compare with a run in another performance session, open the **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="5292e-174">請在顯示的對話方塊中指定兩個檔案。</span><span class="sxs-lookup"><span data-stu-id="5292e-174">Specify both files in the dialog box that appears.</span></span>

![比較效能報告選項][15]

<span data-ttu-id="5292e-176">報告會反白顯示兩個執行之間的差異。</span><span class="sxs-lookup"><span data-stu-id="5292e-176">The reports highlight differences between the two runs.</span></span>

![比較報告][16]

<span data-ttu-id="5292e-178">恭喜！</span><span class="sxs-lookup"><span data-stu-id="5292e-178">Congratulations!</span></span> <span data-ttu-id="5292e-179">您已開始使用分析工具。</span><span class="sxs-lookup"><span data-stu-id="5292e-179">You've gotten started with the profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5292e-180">疑難排解</span><span class="sxs-lookup"><span data-stu-id="5292e-180">Troubleshooting</span></span>
* <span data-ttu-id="5292e-181">確定您正在分析發行組建並開始而不進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="5292e-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="5292e-182">如果未在 [分析工具] 功能表上啟用 [連結/中斷連結] 選項，請執行 [效能精靈]。</span><span class="sxs-lookup"><span data-stu-id="5292e-182">If the Attach/Detach option is not enabled on the Profiler menu, run the Performance Wizard.</span></span>
* <span data-ttu-id="5292e-183">使用計算模擬器 UI 檢視您應用程式的狀態。</span><span class="sxs-lookup"><span data-stu-id="5292e-183">Use the Compute Emulator UI to view the status of your application.</span></span> 
* <span data-ttu-id="5292e-184">如果您在模擬器中啟動應用程式或是連結分析工具時發生問題，請關閉並重新啟動計算模擬器。</span><span class="sxs-lookup"><span data-stu-id="5292e-184">If you have problems starting applications in the emulator, or attaching the profiler, shut down the compute emulator and restart it.</span></span> <span data-ttu-id="5292e-185">如果這樣未解決問題，請嘗試重新開機。</span><span class="sxs-lookup"><span data-stu-id="5292e-185">If that doesn't solve the problem, try rebooting.</span></span> <span data-ttu-id="5292e-186">如果您使用計算模擬器來暫停和移除執行中部署，則可能會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="5292e-186">This problem can occur if you use the Compute Emulator to suspend and remove running deployments.</span></span>
* <span data-ttu-id="5292e-187">如果您已從命令列使用任何分析命令 (尤其是全域設定)，請確定已呼叫 VSPerfClrEnv /globaloff，並已關閉 VsPerfMon.exe。</span><span class="sxs-lookup"><span data-stu-id="5292e-187">If you have used any of the profiling commands from the command line, especially the global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="5292e-188">取樣時，如果您看到訊息 [PRF0025: No data was collected]，請確認您所連結的程序具有 CPU 活動。</span><span class="sxs-lookup"><span data-stu-id="5292e-188">If when sampling, you see the message "PRF0025: No data was collected," check that the process you attached to has CPU activity.</span></span> <span data-ttu-id="5292e-189">未執行任何計算工作的應用程式可能不會產生任何取樣資料。</span><span class="sxs-lookup"><span data-stu-id="5292e-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="5292e-190">在執行任何取樣之前，也可能已結束程序。</span><span class="sxs-lookup"><span data-stu-id="5292e-190">It's also possible that the process exited before any sampling was done.</span></span> <span data-ttu-id="5292e-191">請確認所分析角色的 Run 方法未終止。</span><span class="sxs-lookup"><span data-stu-id="5292e-191">Check to see that the Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5292e-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5292e-192">Next Steps</span></span>
<span data-ttu-id="5292e-193">在 Visual Studio 分析工具中，不支援在模擬器中檢測 Azure 二進位，但是，如果您想要測試記憶體配置，則可以在分析時選擇該選項。</span><span class="sxs-lookup"><span data-stu-id="5292e-193">Instrumenting Azure binaries in the emulator is not supported in the Visual Studio profiler, but if you want to test memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="5292e-194">您也可以選擇並行分析來協助您判斷執行緒是否浪費時間來競爭鎖定，或選擇階層互動分析來協助您追蹤在應用程式階層之間互動時的效能問題 (最常發生在資料層與背景工作角色之間)。</span><span class="sxs-lookup"><span data-stu-id="5292e-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between the data tier and a worker role.</span></span>  <span data-ttu-id="5292e-195">您可以檢視應用程式所產生的資料庫查詢，以及使用分析資料來提高資料庫的使用。</span><span class="sxs-lookup"><span data-stu-id="5292e-195">You can view the database queries that your app generates and use the profiling data to improve your use of the database.</span></span> <span data-ttu-id="5292e-196">如需階層互動分析的詳細資訊，請參閱部落格文章[逐步介紹：在 Visual Studio Team System 2010 中使用階層互動分析][3]。</span><span class="sxs-lookup"><span data-stu-id="5292e-196">For information about tier interaction profiling, see the blog post [Walkthrough: Using the Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

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
