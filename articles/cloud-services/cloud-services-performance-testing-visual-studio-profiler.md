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
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a>在 hello Azure 計算模擬器使用 hello Visual Studio 分析工具中測試 hello 的雲端服務在本機的效能
各種不同的工具和技術可供測試的雲端服務的 hello 效能。
當您發行雲端服務 tooAzure 時，您可以收集分析資料，然後進行分析的 Visual Studio 在本機中所述[Azure 應用程式程式碼剖析][1]。
您也可以使用各種不同的效能計數器，診斷 tootrack 中, 所述[在 Azure 中使用效能計數器][2]。
您也可能想 tooprofile hello 計算模擬器中的本機應用程式再將其部署 toohello 雲端。

本文涵蓋 hello CPU 取樣程式碼剖析方法，能夠以 hello 模擬器在本機完成。 CPU 取樣不是非常侵入式的分析方法。 指定的取樣間隔 hello 分析工具會擷取 hello 呼叫堆疊的快照。 hello 資料需要經過一段時間，收集及顯示報表中。 這種程式碼剖析方法通常會 tooindicate 其中密集的應用程式中大部分的 hello CPU 工作進行，則為。  這讓您在 hello 機會 toofocus hello [最忙碌路徑]，其中您的應用程式花 hello 最多時間。

## <a name="1-configure-visual-studio-for-profiling"></a>1：設定 Visual Studio 進行分析
首先，有些 Visual Studio 組態選項可能在進行分析時很實用。 toomake 意義 hello 分析報告，您將需要符號 （.pdb 檔案），您的應用程式以及系統程式庫的符號。 您會想 toomake 確定您參考 hello 使用符號伺服器。 toodo 這在 hello**工具**在 Visual Studio 的功能表中選擇 **選項**，然後選擇 **偵錯**，然後**符號**。 請確定 Microsoft Symbol Servers 列在 [符號檔 (.pdb) 位置] 下方。  您也可以參考 http://referencesource.microsoft.com/symbols，其中可能有其他符號檔案。

![符號選項][4]

如有需要，您可以簡化 hello 會報告該 hello 分析工具會產生藉由設定 Just My Code。 啟用 Just My Code，與函式的呼叫堆疊已經過簡化，以便呼叫完全內部 toolibraries 而 hello.NET Framework 會隱藏 hello 報表。 在 hello**工具**功能表上，選擇**選項**。 然後展開 hello**效能工具** 節點，然後選擇 **一般**。 選取 hello 核取方塊**啟用 Just My Code 以進行分析工具報告**。

![Just My Code 選項][17]

您可以將這些指示與現有專案或新的專案搭配使用。  如果您建立新的專案 tootry hello 如下所述的技巧，選擇 C# **Azure 雲端服務**專案，然後選取**Web 角色**和**背景工作角色**。

![Azure 雲端服務專案角色][5]

比方說的目的，將某些程式碼 tooyour 專案會耗用大量時間，並示範一些明顯的效能問題。 例如，加入下列程式碼 tooa 背景工作角色專案的 hello:

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

呼叫此程式碼從 hello RunAsync hello 背景工作角色的 RoleEntryPoint 衍生類別中的方法。 （忽略 hello 警告 hello 方法以同步方式執行）。

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

建置並搭配 hello 的方案組態設定得您的雲端服務在本機執行但不偵錯 (Ctrl + F5)，**發行**。 這可確保所有檔案和資料夾會建立在本機執行 hello 應用程式，並可確保所有 hello 模擬器已都啟動。 請從背景工作角色執行的 hello 工作列 tooverify 啟動 hello 計算模擬器 UI。

## <a name="2-attach-tooa-process"></a>2： 附加 tooa 處理序
除了啟動從 hello Visual Studio 2010 IDE 來分析 hello 應用程式，您必須將附加 hello profiler tooa 執行程序。 

tooattach hello profiler tooa 程序，在 hello**分析**功能表上，選擇**Profiler**和**附加/卸離**。

![附加設定檔選項][6]

背景工作角色中，尋找 hello WaWorkerHost.exe 程序。

![WaWorkerHost 程序][7]

如果您的專案資料夾位於網路磁碟機，hello 分析工具會要求您 tooprovide 程式碼剖析報告的另一個位置 toosave hello。

 您也可以藉由附加 tooWaIISHost.exe 附加 tooa web 角色。
如果您的應用程式中有多個背景工作角色處理序，您需要 toouse hello processID toodistinguish 它們。 您可以藉由存取 hello 處理程序物件，以程式設計方式查詢 hello processID。 比方說，如果您在角色中加入 hello RoleEntryPoint 衍生類別的這個程式碼 toohello Run 方法，您可以查看記錄檔中 hello 計算模擬器 UI tooknow 以何種處理程序 tooconnect。

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

開始 hello 計算模擬器 UI tooview hello 記錄。

![啟動 hello 計算模擬器 UI][8]

Hello 背景工作角色記錄主控台視窗 hello 計算模擬器 UI 中按一下來開啟 hello 主控台視窗的標題列上。 您可以看到 hello hello 記錄檔中的處理序識別碼。

![檢視處理序識別碼][9]

您已經附加，一個在您的應用程式 UI （如有需要） tooreproduce hello 案例中執行 hello 步驟。

當您想 toostop 程式碼剖析時，請選擇 hello**停止程式碼剖析**連結。

![停止分析選項][10]

## <a name="3-view-performance-reports"></a>3：檢視效能報告
您的應用程式的 hello 效能報表會顯示。

此時，hello 分析工具會停止執行，將資料儲存在.vsp 檔，並顯示的報表會顯示此資料的分析。

![分析工具報告][11]

如果您看到 String.wstrcpy hello 中最忙碌路徑] 中，按一下 [Just My Code toochange hello 檢視 tooshow 使用者程式碼。  如果您看到 String.Concat，再試一次按下 hello 顯示所有程式碼 按鈕。

您應該會看到 hello 串連方法和 String.Concat 佔用大量 hello 執行時間。

![報告的分析][12]

如果您在本文中加入 hello 字串串連的程式碼，您應該會看到這個 hello 工作清單中的警告。 您也可能會看到警告，表示過量的記憶體回收，這是因為 toohello 數字的字串，建立和處置。

![效能警告][14]

## <a name="4-make-changes-and-compare-performance"></a>4：進行變更與比較效能
您也可以比較程式碼變更之前和之後的 hello 效能。  停止 hello 執行程序，並編輯 hello 碼 tooreplace hello 字串串連運算 hello 使用 StringBuilder 的：

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

執行另一個回合的效能測試，然後和比較 hello 效能。 在 [hello 效能總管] 中，如果 hello 執行位於 hello 相同工作階段，您可以只選取兩個報表，開啟 hello 捷徑功能表，並選擇**比較效能報告**。 如果您想 toocompare 與另一個效能工作階段中執行，請開啟 hello**分析**功能表上，選擇 **比較效能報告**。 在出現的 hello 對話方塊方塊中指定這兩個檔案。

![比較效能報告選項][15]

hello 報表反白顯示 hello 兩次執行之間的差異。

![比較報告][16]

恭喜！ 您開始使用與 hello 分析工具。

## <a name="troubleshooting"></a>疑難排解
* 確定您正在分析發行組建並開始而不進行偵錯。
* 如果 hello 附加/卸離選項未啟用 hello 分析工具 功能表上，執行 hello 效能精靈。
* 使用應用程式的 hello 計算模擬器 UI tooview hello 狀態。 
* 如果您有在 hello 模擬器中啟動應用程式的問題，或附加 hello 程式碼剖析工具，關閉 hello 計算模擬器，然後重新啟動它。 如果無法解決 hello 問題，請嘗試重新啟動。 如果您使用 hello 計算模擬器 toosuspend 和移除執行中部署，可能會發生此問題。
* 如果您有使用任何命令，從命令列程式碼剖析的 hello，特別是 hello 全域設定，確定已呼叫 VSPerfClrEnv /globaloff VsPerfMon.exe 已關閉。
* 如果在取樣，您會看見 hello 訊息 「 PRF0025： 未收集任何資料，「 hello 附加 toohas CPU 活動的程序的核取。 未執行任何計算工作的應用程式可能不會產生任何取樣資料。  此外，也可以 hello 處理序結束之前已完成的任何取樣。 Hello Run 方法，用於您要分析的角色的核取 toosee 不會終止。

## <a name="next-steps"></a>後續步驟
檢測 Azure hello 模擬器中的二進位檔不支援在 hello Visual Studio 分析工具，但如果您想 tootest 記憶體配置時，程式碼剖析時，您可以選擇該選項。 您也可以選擇並行分析，這可協助您判斷執行緒是否會浪費時間競爭鎖定，或階層互動分析，這可協助您追蹤效能問題的應用程式層之間的互動時最經常之間 hello 資料層和背景工作角色。  您可以檢視您的應用程式產生的 hello 資料庫查詢，並使用程式碼剖析資料 tooimprove hello 資料庫貴用戶使用的 hello。 如需階層互動分析資訊，請參閱 hello 部落格文章[逐步解說： 使用 hello 階層互動分析工具，在 Visual Studio Team System 2010][3]。

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
