---
title: "開始使用 Azure 記錄分析工作區的 aaaGet |Microsoft 文件"
description: "您可以在幾分鐘之內啟動並執行 Log Analytics 工作區。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 508716de-72d3-4c06-9218-1ede631f23a6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/08/2017
ms.author: magoedte
ms.openlocfilehash: 442a9258a37ee79e8f0b45759ef24b5e3dae0130
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-log-analytics-workspace"></a>開始使用 Log Analytics 工作區
您可以使用 Azure Log Analytics 快速啟動並執行，以協助您評估從 IT 基礎結構收集到的營運情報。 運用本文，您可以輕鬆地開始對您所收集的資料進行瀏覽、分析並採取動作，一切「免費」。

這份文件做為簡介 tooLog 使用簡短的教學課程 toowalk 分析您透過在 Azure 中的基本部署，以便您可以開始使用 hello 服務。 hello 儲存在 Azure 中的管理資料的邏輯容器會呼叫工作區。 您已檢閱這項資訊，並完成您的評估之後，您可以移除 hello 評估工作區。 本文屬教學課程，因此不會探討業務需求、規劃或架構方面的指引。

>[!NOTE]
>如果您使用 Microsoft Azure 政府雲端 hello，使用[Azure 政府監視 + 管理文件](https://docs.microsoft.com/azure/azure-government/documentation-government-services-monitoringandmanagement#log-analytics)改為。

以下是快速查看 hello 用程序 tooget 啟動：

![程序流程圖](./media/log-analytics-get-started/onboard-oms.png)

## <a name="1-create-an-azure-account-and-sign-in"></a>1 建立 Azure 帳戶並登入

如果您還沒有 Azure 帳戶，您會需要 toocreate 一個 toouse 記錄分析。 您可以建立可使用 30 天的[免費帳戶](https://azure.microsoft.com/free/)，以便存取任何 Azure 服務。

### <a name="toocreate-a-free-account-and-sign-in"></a>toocreate 免費帳戶，登入
1. 請依照下列指示 hello[建立免費的 Azure 帳戶](https://azure.microsoft.com/free/)。
2. 移 toohello [Azure 入口網站](https://portal.azure.com)並登入。

## <a name="2-create-a-workspace"></a>2 建立工作區

hello 下一個步驟是 toocreate 工作區。

1. 在 hello Azure 入口網站中，搜尋 hello Marketplace 中的服務的 hello 清單的*記錄分析*，然後選取**記錄分析**。  
    ![Azure 入口網站](./media/log-analytics-get-started/log-analytics-portal.png)
2. 按一下**建立**，然後選取 適用於下列項目 hello 的選項：
   * **OMS 工作區** - 輸入工作區的名稱。
   * **訂用帳戶**-如果您有多個訂用帳戶，選擇您想要與新工作區 hello tooassociate hello。
   * **資源群組**
   * **位置**
   * **定價層**  
       ![快速建立](./media/log-analytics-get-started/oms-onboard-quick-create.png)
3. 按一下**確定**toosee 的工作區清單。
4. 在 hello Azure 入口網站中選取工作區 toosee 其詳細資料。       
    ![工作區詳細資料](./media/log-analytics-get-started/oms-onboard-workspace-details.png)         

## <a name="3-upgrade-workspace-toonew-log-search"></a>3 的升級工作區 toonew 記錄搜尋
已發行新的記錄分析查詢語言，並在它的順序 tootake 優點，您需要 tooconvert 您的工作區。  如果已升級您的工作區中裝載的 hello 區域，您應該會看到 tooconvert 邀請您工作區的 hello 頂端紫色橫幅。 hello 升級屬自願參加，並不會影響您使用記錄分析和您新增任何方案的體驗。  

如進一步資訊 toounderstand hello 優點、 考量和程序 tooupgrade，請參閱[升級 Azure Log Analytics toonew 記錄搜尋](log-analytics-log-search-upgrade.md)。  

## <a name="4-add-solutions-and-solution-offerings"></a>4 新增解決方案和解決方案供應項目

接下來，新增管理解決方案和解決方案供應項目。 管理解決方案是邏輯、視覺效果和資料擷取規則的集合，可提供針對特定問題領域進行計量的樞紐分析。 解決方案供應項目是管理解決方案的組合。

新增解決方案 tooyour 工作區可讓記錄分析 toocollect 各種資料連接的 tooyour 工作區中使用的代理程式的電腦。 我們會於稍後討論如何啟用代理程式。

### <a name="tooadd-solutions-and-solution-offerings"></a>tooadd 方案和解決方案供應項目

1. 在 Azure 入口網站中，按一下**新增**，然後在 hello**搜尋 hello marketplace**方塊中，輸入**活動記錄分析**然後按 ENTER 鍵。
2. 中的所有項目 hello 刀鋒視窗中，選取**活動記錄分析**，然後按一下**建立**。  
    ![活動 Log Analytics](./media/log-analytics-get-started/activity-log-analytics.png)  
3. 在 hello*管理方案名稱*刀鋒視窗中，選取您想 tooassociate 與 hello 管理解決方案的工作區。
4. 按一下 [建立] 。  
    ![解決方案工作區](./media/log-analytics-get-started/solution-workspace.png)  
5. 重複步驟 1-4 tooadd:
    - hello**安全性和規範**服務供應項目與 hello 反惡意程式碼評估和安全性和稽核解決方案。
    - hello**自動化和控制**服務供應項目與 hello 自動化 Hybrid Worker、 變更追蹤 （也稱為 「 更新管理 」） 的系統更新評估 」 解決方案。 當您新增 hello 解決方案供應項目時，您必須建立自動化帳戶。  
        ![自動化帳戶](./media/log-analytics-get-started/automation-account.png)  
6. 您可以檢視您加入 tooyour 工作區瀏覽過的 hello 管理解決方案**記錄分析** > **訂閱** > ***的工作區名稱*** > **概觀**。 您加入的 hello 管理解決方案的磚會顯示。  
    >[!NOTE]
    >因為我們尚未連接的任何代理程式 toohello 工作區，您看不 hello 方案您加入的任何資料。  

    ![沒有資料的解決方案圖格](./media/log-analytics-get-started/solutions-no-data.png)

## <a name="4-create-a-vm-and-onboard-an-agent"></a>4 建立 VM 並啟用代理程式

接下來，在 Azure 中建立簡單的虛擬機器。 建立 VM 時，內建的 hello OMS 代理程式 tooenable 之後它。 啟用 hello 代理程式 hello VM 啟動資料收集，並傳送資料 tooLog 分析。

### <a name="toocreate-a-virtual-machine"></a>toocreate 虛擬機器

- 請依照下列指示 hello [hello Azure 入口網站中建立第一個 Windows 虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md)並啟動 hello 新的虛擬機器。

### <a name="connect-hello-virtual-machine-toolog-analytics"></a>連接 hello 虛擬機器 tooLog 分析

- 請依照下列指示 hello[連接 Azure 虛擬機器 tooLog 分析](log-analytics-azure-vm-extension.md)tooconnect hello VM tooLog 分析使用 hello Azure 入口網站。

## <a name="6-view-and-act-on-data"></a>6 檢視和處理資料

先前，您已啟用 hello 活動記錄分析解決方案和 hello 安全性與相容性和自動化和控制服務供應項目。 接下來，我們要開始查看解決方案所收集的資料和記錄搜尋中的結果。

toostart，看看會從方案內顯示的資料。 然後，查看一些透過記錄搜尋所取得的記錄搜尋。 Toocombine 可讓您記錄搜尋，並相互關聯您環境內多個來源的任何電腦資料。 如需詳細資訊，請參閱[記錄中記錄分析搜尋](log-analytics-log-searches.md)或如果您轉換您的工作區 toohello 新的查詢語言，請參閱[了解記錄中記錄分析會搜尋](log-analytics-log-search-new.md)。 

### <a name="tooview-antimalware-data"></a>tooview 反惡意程式碼的資料

1. 在 hello Azure 入口網站中瀏覽過**記錄分析** > ***您的工作區***。
2. 在您的工作區的 hello 刀鋒視窗底下**一般**，按一下 **概觀**。  
    ![概觀](./media/log-analytics-get-started/overview.png)
3. 按一下 hello**反惡意程式碼評定**磚。 在此範例中，您可以看到電腦上已安裝 Windows Defender，但其簽章已過期。  
    ![反惡意程式碼](./media/log-analytics-get-started/solution-antimalware.png)
4. 例如下,**保護狀態**，按一下**簽章已過期**hello 電腦具有過期的簽章的相關 tooopen 記錄搜尋和檢視詳細資料。 在此範例中，記下該 hello 電腦的名稱是*getstarted*。 如果有多部電腦使用過期的簽章，它們會全部顯示在 hello 記錄搜尋結果。  
    ![反惡意程式碼已過期](./media/log-analytics-get-started/antimalware-search.png)

### <a name="tooview-security-and-audit-data"></a>tooview 安全性和稽核資料

1. 在您的工作區的 hello 刀鋒視窗底下**一般**，按一下 **概觀**。  
2. 按一下 hello**安全性和稽核**磚。 在此範例中，您會看到兩個值得注意的問題︰有一部電腦遺漏重大更新，另有一部電腦的保護不足。  
    ![安全性和稽核](./media/log-analytics-get-started/security-audit.png)
3. 例如下,**值得注意的問題**，按一下**缺少重大更新的電腦**缺少重大更新的電腦的相關 tooopen 記錄搜尋和檢視詳細資料。 在此範例中，總共遺漏了 1 個重大更新和 63 個其他更新。  
    ![安全性和稽核記錄搜尋](./media/log-analytics-get-started/security-audit-log-search.png)

### <a name="tooview-and-act-on-system-update-data"></a>tooview，並針對系統更新資料

1. 在您的工作區的 hello 刀鋒視窗底下**一般**，按一下 **概觀**。  
2. 按一下 hello**系統更新評估**磚。 在此範例中，您會看到有一部名為 getstarted 的 Windows 電腦需要重大更新，另有一部電腦需要定義更新。  
    ![系統更新](./media/log-analytics-get-started/system-updates.png)
3. 例如下,**遺失更新**，按一下**重大更新**缺少重大更新的電腦的相關 tooopen 記錄搜尋和檢視詳細資料。 在此範例中，有一個遺漏的更新以及一個必要更新。  
    ![系統更新記錄搜尋](./media/log-analytics-get-started/system-updates-log-search.png)
4. 移 toohello [Operations Management Suite](http://microsoft.com/oms)網站並使用您的 Azure 帳戶登入。 如果登入，請注意 hello 解決方案的資訊是您已在 hello Azure 入口網站中看到的類似 toowhat。  
    ![OMS 入口網站](./media/log-analytics-get-started/oms-portal.png)
5. 按一下 hello**更新管理**磚。
6. 在 hello 更新管理儀表板，請注意，hello 系統更新的資訊類似 toohello 系統更新的資訊 hello Azure 入口網站中所見。 不過，hello**管理更新部署**是新的磚。 按一下 hello**管理更新部署**磚。  
    ![更新管理圖格](./media/log-analytics-get-started/update-management.png)
7. 在 hello**更新部署**頁面上，按一下**新增**toocreate*更新執行*。  
    ![更新部署](./media/log-analytics-get-started/update-management-update-deployments.png)
8.  在 hello**新更新的部署**頁面上，輸入 hello 更新部署的名稱，然後選取電腦 tooupdate (在此範例中， *getstarted*)，選擇的排程，然後按一下**儲存**.  
    ![新增部署](./media/log-analytics-get-started/new-deployment.png)  
    儲存 hello 更新部署後，您會看見 hello 排程更新。  
    ![已排程的更新](./media/log-analytics-get-started/scheduled-update.png)  
    Hello 更新執行完成之後，hello 狀態顯示**已經完成**。
    ![已完成的更新](./media/log-analytics-get-started/completed-update.png)
9. Hello 更新執行完成之後，您可以檢視是否 hello 執行成功，您可以檢視有關哪些更新，套用的詳細資料。

## <a name="after-evaluation"></a>評估之後

在本教學課程中，您已在虛擬機器上安裝代理程式，並快速開始使用。 您遵循的 hello 步驟已快速又簡單。 不過，大型組織和企業的內部部署 IT 基礎結構大多較複雜。 因此，從這些複雜的環境中收集資料會採用額外的規劃和投入時間比 hello 教學課程。 檢閱 hello 遵循連結 toohelpful 發行項的下一個步驟一節中的 hello 資訊。

您可以選擇性地移除使用本教學課程中建立的 hello 工作區。

## <a name="next-steps"></a>後續步驟
* 深入了解連接[Windows 代理程式](log-analytics-windows-agents.md)tooLog 分析。
* 深入了解連接[Operations Manager 代理程式](log-analytics-om-agents.md)tooLog 分析。
* [新增記錄分析解決方案從 hello 解決方案資源庫](log-analytics-add-solutions.md)tooadd 功能和收集資料。
* 讓您熟悉[記錄搜尋](log-analytics-log-searches.md)tooview 詳細解決方案所收集的資訊。
