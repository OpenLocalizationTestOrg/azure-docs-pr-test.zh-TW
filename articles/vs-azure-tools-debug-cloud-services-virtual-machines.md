---
title: "aaaDebugging Azure 雲端服務或在 Visual Studio 中的虛擬機器 |Microsoft 文件"
description: "在 Visual Studio 中進行雲端服務或虛擬機器的偵錯"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 945e06e0-2100-41af-b218-72347367ddab
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 32a326430021ba2ea9317a6a71fa005d4b87c273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-an-azure-cloud-service-or-virtual-machine-in-visual-studio"></a>在 Visual Studio 中進行 Azure 雲端服務或虛擬機器的偵錯
Visual Studio 提供您偵錯 Azure 雲端服務和虛擬機器的不同選項。

## <a name="debug-your-cloud-service-on-your-local-computer"></a>在您的本機電腦上偵錯您的雲端服務
您可以儲存時間和金錢使用 hello Azure 計算模擬器 toodebug 您的雲端服務在本機電腦上。 透過在部署服務之前於本機偵錯服務，您可以改善可靠性和效能，而不需支付運算時間。 不過，某些錯誤可能只有當您在 Azure 中執行雲端服務本身時才會發生。 如果您啟用遠端偵錯時您發佈您的服務，然後附加 hello 偵錯工具 tooa 角色執行個體，您可以偵錯這些錯誤。

hello 模擬器會模擬 hello Azure 計算服務，並使您可以測試和偵錯雲端服務，在部署之前，您的本機環境中執行。 hello 模擬器控點 hello 角色執行個體的生命週期，並提供存取 toosimulated 資源，例如本機儲存體。 當您偵錯，或從 Visual Studio 執行您的服務時，它會自動啟動 hello 模擬器做為背景應用程式，並接著將部署服務 toohello 模擬器。 Hello 本機環境中執行時您可以使用指定 hello 模擬器 tooview 您的服務。 您可以執行 hello 完整版本或 hello hello emulator express 版本。 （從 Azure 2.3 開始，hello 精簡版本 hello 模擬器是 hello 預設值）。請參閱[使用 Emulator Express tooRun 和雲端服務在本機偵錯](https://msdn.microsoft.com/library/dn339018.aspx)。

### <a name="toodebug-your-cloud-service-on-your-local-computer"></a>您的雲端服務在本機電腦的 toodebug
1. 在 hello 功能表列上選擇 **偵錯**，**開始偵錯**toorun Azure 雲端服務專案。 或者，您可以按 F5。 您會看到計算模擬器的 hello 訊息正在啟動。 Hello 模擬器啟動時，hello 系統匣圖示會加以確認。

    ![Hello 系統匣中的 azure 模擬器](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC783828.png)
2. 以顯示 hello 使用者介面的 hello 計算模擬器在 hello 通知區域中，開啟 hello hello Azure 圖示的捷徑功能表，然後選取**顯示計算模擬器 UI**。

    hello UI hello 左的窗格會顯示目前的 hello 服務部署 toohello 計算模擬器和 hello 角色執行個體，每個服務執行。 Hello 右窗格中，您可以選擇 hello 服務或角色 toodisplay 生命週期、 記錄和診斷資訊。 如果您將 hello 焦點放在 hello 的包含視窗的上邊界時，它會展開 toofill hello 右窗格。
3. 逐步執行 hello 應用程式選取命令上 hello**偵錯**功能表，並在您的程式碼中設定中斷點。 當您逐步執行 hello hello 偵錯工具中的應用程式，hello 窗格會更新 hello hello 應用程式目前狀態。 當您停止偵錯時，會刪除 hello 應用程式部署。 如果您的應用程式包含 web 角色，而且您已經設定 hello 啟動動作屬性 toostart hello web 瀏覽器，Visual Studio 會在 hello 瀏覽器中啟動 web 應用程式。 如果您變更 hello hello 服務組態中的角色執行個體的數目，您必須停止雲端服務，並再重新啟動偵錯，以便您可以偵錯 hello 角色的這些新執行個體。

    **注意：**當您停止執行或偵錯您的服務，hello 本機計算模擬器和儲存體模擬器並不會停止。 您必須明確停止它們從 hello 通知區域。

## <a name="debug-a-cloud-service-in-azure"></a>在 Azure 中偵錯雲端服務
toodebug 雲端服務從遠端電腦，您必須啟用這項功能明確當您部署雲端服務，因此需要執行角色執行個體的 hello 虛擬機器上安裝服務 (例如 msvsmon.exe)。 如果您未啟用遠端偵錯發行 hello 服務時，您會有 toorepublish hello 服務已啟用遠端偵錯。

如果您啟用雲端服務的遠端偵錯，它不會出現效能降低或產生其他費用。 因為用戶端使用 hello 服務可能會受到負面影響，您不應使用實際執行服務時，遠端偵錯。

> [!NOTE]
> 當您發行雲端服務，從 Visual Studio 時，您可以啟用**IntelliTrace**中的任何角色服務該目標 hello.NET Framework 4 或.NET Framework 4.5 的 hello。 使用**IntelliTrace**，您可以檢查角色執行個體在 hello 過去發生的事件，並重現當時的 hello 內容。 請參閱[使用 IntelliTrace 和 Visual Studio 偵錯發佈的雲端服務](http://go.microsoft.com/fwlink/?LinkID=623016)和[使用 IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx)。
>
>

### <a name="tooenable-remote-debugging-for-a-cloud-service"></a>tooenable 遠端偵錯雲端服務
1. 開啟 hello hello Azure 專案的捷徑功能表，然後選取**發行**。
2. 選取 hello**臨時**環境和 hello**偵錯**組態。

    這只是指導方針。 您可以選擇 toorun 實際執行環境中的測試環境。 不過，您可能會影響使用者如果您啟用遠端偵錯 hello 實際執行環境。 您可以選擇 hello 發行組態，但 hello 偵錯組態會讓偵錯更容易。

    ![選擇 hello 偵錯組態](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746717.gif)
3. 請遵循 hello 往常的步驟，但選取的 hello**啟用遠端偵錯工具的所有角色**hello 核取方塊**進階設定** 索引標籤。

    ![偵錯組態](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746718.gif)

### <a name="tooattach-hello-debugger-tooa-cloud-service-in-azure"></a>tooattach hello 偵錯工具 tooa Azure 中雲端服務
1. 在伺服器總管 中，展開您的雲端服務的 hello 節點。
2. 開啟 hello hello 角色或角色執行個體 toowhich 您想 tooattach，，然後選取的快顯功能表**附加偵錯工具**。

    如果您偵錯角色，hello Visual Studio 偵錯工具會附加 tooeach 該角色執行個體。 hello 偵錯工具會在中斷點 hello 第一個角色執行個體執行該行程式碼並符合中斷點條件時中斷。 如果您偵錯執行個體，hello 偵錯工具會附加 tooonly 執行個體並且在該特定執行個體執行該行程式碼並符合時於中斷點中斷 hello 中斷點的條件。

    ![附加偵錯工具](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746719.gif)
3. Hello 偵錯工具附加 tooan 執行個體之後，請如往常般進行偵錯。 hello 偵錯工具會自動附加 toohello 適當的主控件程序，您的角色。 角色是根據哪些 hello、 hello 偵錯工具附加 toow3wp.exe、 WaWorkerHost.exe 或 WaIISHost.exe。 tooverify hello 程序 toowhich hello 偵錯工具附加，依序展開 [伺服器總管] 中的 hello 執行個體節點。 如需有關 Azure 程序的詳細資訊，請參閱[ Azure 角色架構](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx)。

    ![選取程式碼類型對話方塊](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
4. tooidentify hello 處理序附加 toowhich hello 偵錯工具中，開啟 hello 處理序] 對話方塊，在 hello 功能表列選擇 [偵錯、 Windows、 處理程序。 (鍵盤： Ctrl + Alt + Z) toodetach 特定的處理序中，開啟其捷徑功能表，，然後選取**中斷處理序**。 或者，在伺服器總管 中找出 hello 執行個體節點、 尋找 hello 程序、 開啟其捷徑功能表，，然後選取**中斷處理序**。

    ![偵錯處理序](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC690787.gif)

> [!WARNING]
> 進行遠端偵錯時，避免長時間在中斷點停止運作。 Azure 會將已停止的時間超過幾分鐘的時間為沒有回應，並停止傳送流量 toothat 執行個體的處理序。 如果您停止太久，msvsmon.exe 就會中斷 hello 程序。
>
>

toodetach hello 偵錯工具從您的執行個體或角色、 hello 角色或執行個體，您在偵錯，然後選取開啟 hello 快顯功能表中的所有處理序**中斷偵錯工具**。

## <a name="limitations-of-remote-debugging-in-azure"></a>在 Azure 中遠端偵錯的限制
從 Azure SDK 2.3，遠端偵錯具有下列限制的 hello。

* 若啟用遠端偵錯，您無法在具有超過 25 個執行個體的任何角色中發佈雲端服務。
* hello 偵錯工具會使用連接埠 30400 too30424、 31400 too31424 和 32400 too32424。 如果您在這些連接埠的任何嘗試 toouse，不是您的服務，以及其中一個 hello 下列錯誤訊息記錄中會顯示 hello 活動 azure 可以 toopublish:

  * 驗證對 hello.csdef 檔 hello.cscfg 檔案時發生錯誤。
    hello 保留連接埠範圍 'range' 端點 Microsoft.WindowsAzure.Plugins.RemoteDebugger.Connector 的角色 '角色' 與已經定義的連接埠或範圍重疊。
  * 配置失敗。 請稍後再重試、 嘗試減少 hello VM 大小或角色執行個體數目，或嘗試部署 tooa 不同的區域。

## <a name="debugging-azure-virtual-machines"></a>偵錯 Azure 虛擬機器
您可以在 Visual Studio 中使用伺服器總管偵錯 Azure 虛擬機器上執行的程式。 當您啟用 Azure 的虛擬機器上的遠端偵錯時，Azure 會在 hello 虛擬機器上安裝 hello 遠端偵錯延伸模組。 然後，您可以附加 tooprocesses hello 虛擬機器上的，而偵錯像平常一樣。

> [!NOTE]
> 透過 hello Azure 資源管理員堆疊所建立的虛擬機器可使用 Cloud Explorer 在 Visual Studio 2015 遠端偵錯。 如需詳細資訊，請參閱 [使用雲端總管管理 Azure 資源](http://go.microsoft.com/fwlink/?LinkId=623031)。
>
>

### <a name="toodebug-an-azure-virtual-machine"></a>toodebug Azure 虛擬機器
1. 在伺服器總管 中，展開 hello 虛擬機器節點以及您想 toodebug hello 虛擬機器選取 hello 節點。
2. 開啟 hello 操作功能表，然後選取**啟用偵錯**。 當系統詢問您是否確定要 tooenable 偵錯 hello 虛擬機器上，選取如果**是**。

    Azure 上偵錯 hello 虛擬機器 tooenable 安裝 hello 遠端偵錯延伸模組。

    ![虛擬機器啟用偵錯命令](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Azure 活動記錄檔](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
3. Hello 遠端偵錯延伸模組可讓您完成安裝之後，開啟 hello 虛擬機器的內容功能表，然後選取 **附加偵錯工具...**

    Azure hello 虛擬機器上取得 hello 處理序的清單，並顯示 hello 附加 tooProcess 對話方塊中。

    ![附加偵錯工具命令](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
4. 在 hello**附加 tooProcess**對話方塊中，選取**選取**toolimit hello 結果清單 tooshow hello 類型才要 toodebug 的程式碼。 您可以偵錯 32 或 64 位元 Managed 程式碼、原生程式碼或兩者。

    ![選取程式碼類型對話方塊](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
5. 選取您想 toodebug hello 虛擬機器上的，然後選取 「 hello 」 處理序**附加**。 例如，您可能會選擇 hello w3wp.exe 處理程序，如果您想 toodebug hello 虛擬機器上的 web 應用程式。 如需詳細資訊，請參閱[在 Visual Studio 中偵錯一或多個處理序](https://msdn.microsoft.com/library/jj919165.aspx)和 [Azure 角色架構](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx)。

## <a name="create-a-web-project-and-a-virtual-machine-for-debugging"></a>建立 Web 專案和虛擬機器進行偵錯
發行 Azure 專案之前, 您可能會覺得有用的 tootest 中所包含的環境，支援偵錯和測試案例中，而且您可以在其中安裝測試和監控程式。 這是一種方式 toodo tooremotely 偵錯的虛擬機器上的應用程式。

Visual Studio ASP.NET 專案提供選項 toocreate 實用的虛擬機器，您可以使用應用程式測試。 hello 虛擬機器包括一般需要的端點，例如 PowerShell、 遠端桌面和 WebDeploy。

### <a name="toocreate-a-web-project-and-a-virtual-machine-for-debugging"></a>toocreate web 專案和虛擬機器以便偵錯
1. 在 Visual Studio 中，建立新的 ASP.NET Web 應用程式。
2. 在 hello 新增 ASP.NET 專案對話方塊中，在 hello Azure 區段中，選擇 **虛擬機器**hello 下拉式清單方塊中。 保留 hello**建立遠端資源**選取核取方塊。 選取**確定**tooproceed。

    hello **Azure 上建立虛擬機器** 對話方塊隨即出現。

    ![建立 ASP.NET Web 專案對話方塊](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746723.png)

    **注意：**系統會詢問 toosign 中 tooyour Azure 帳戶如果您沒有已登入。

1. 選取 hello hello 虛擬機器的各種設定，然後選取 **確定**。 如需詳細資訊，請參閱 [虛擬機器](http://go.microsoft.com/fwlink/?LinkId=623033) 。

    您輸入的 DNS 名稱的 hello 名稱會 hello hello 虛擬機器名稱。

    ![在 Azure 上建立虛擬機器對話方塊](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746724.png)

    Azure 會建立 hello 虛擬機器，然後佈建並設定 hello 端點，例如遠端桌面和 Web Deploy
2. Hello 虛擬機器完全設定之後，請在伺服器總管 中選取 hello 虛擬機器的節點。
3. 開啟 hello 操作功能表，然後選取**啟用偵錯**。 當系統詢問您是否確定要 tooenable 偵錯 hello 虛擬機器上，選取如果**是**。

    Azure 會安裝 hello 遠端偵錯擴充功能 toohello 虛擬機器 tooenable 偵錯。

    ![虛擬機器啟用偵錯命令](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Azure 活動記錄檔](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
4. 如 [HOW TO：在 Visual Studio 中使用單鍵發佈來部署 Web 專案](https://msdn.microsoft.com/library/dd465337.aspx)所述，發佈您的專案。 因為您想要對 hello hello 虛擬機器 toodebug**設定**頁面 hello**發行 Web**精靈中，選取**偵錯**作為 hello 組態。 這樣可確保程式碼符號在偵錯時可供使用。

    ![發佈設定](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718349.png)
5. 在 hello**檔案發行選項**，選取**移除目的端的其他檔案**如果 hello 專案已經部署在較早的時間。
6. 在伺服器總管中的 hello 虛擬機器的操作功能表上 hello 專案發行之後選取**附加偵錯工具...**

    Azure hello 虛擬機器上取得 hello 處理序的清單，並顯示 hello 附加 tooProcess 對話方塊中。

    ![附加偵錯工具命令](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
7. 在 hello**附加 tooProcess**對話方塊中，選取**選取**toolimit hello 結果清單 tooshow hello 類型才要 toodebug 的程式碼。 您可以偵錯 32 或 64 位元 Managed 程式碼、原生程式碼或兩者。

    ![選取程式碼類型對話方塊](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
8. 選取您想 toodebug hello 虛擬機器上的，然後選取 「 hello 」 處理序**附加**。 例如，您可能會選擇 hello w3wp.exe 處理程序，如果您想 toodebug hello 虛擬機器上的 web 應用程式。 如需詳細資訊，請參閱 [在 Visual Studio 中偵錯一或多個處理序](https://msdn.microsoft.com/library/jj919165.aspx) 。

## <a name="next-steps"></a>後續步驟
* 使用**Intellitrace** toocollect 的呼叫與從發行伺服器的事件記錄檔。 請參閱 [使用 IntelliTrace 和 Visual Studio 偵錯發佈的雲端服務](http://go.microsoft.com/fwlink/?LinkID=623016)。
* 使用**Azure 診斷**toolog 是否在 hello 開發環境中，或在 Azure 中執行 hello 角色的詳細資訊從角色中的程式碼執行。 請參閱 [使用 Azure 診斷收集記錄資料](http://go.microsoft.com/fwlink/p/?LinkId=400450)。
