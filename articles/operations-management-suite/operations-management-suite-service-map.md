---
title: "aaaUse hello Operations Management Suite 中的服務對應方案 |Microsoft 文件"
description: "服務對應是一種 Operations Management Suite 解決方案，它會自動探索 Windows 上的應用程式元件和 Linux 系統和對應 hello 服務之間的通訊。 本文會詳細說明如何在環境中部署服務對應並將它用於各種案例。"
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: 3ceb84cc-32d7-4a7a-a916-8858ef70c0bd
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/22/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: f7c209182c9171cc520192ac13ca4d85174081b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-service-map-solution-in-operations-management-suite"></a>使用 Operations Management Suite 中的 hello 服務對應解決方案
服務對應會自動探索 Windows 和 Linux 系統上的應用程式元件和對應 hello 服務之間的通訊。 使用服務對應，您可以檢視您的伺服器，您會覺得 hello 方式： 做為傳送重要服務的互連系統。 服務對應可顯示任何 TCP 連線架構跨伺服器、 處理程序與連接埠之間的連線，而不需要以外設定 hello 代理程式安裝。

本文說明使用服務對應的 hello 詳細資料。 如需設定服務對應和啟用代理程式的相關資訊，請參閱[在 Operations Management Suite 中設定服務對應解決方案](operations-management-suite-service-map-configure.md)。


## <a name="use-cases-make-your-it-processes-dependency-aware"></a>使用案例︰讓 IT 處理序可以感知相依性

### <a name="discovery"></a>探索
服務對應會自動建置跨伺服器、處理程序和協力廠商服務的一般相依性參考對應。 它會探索並將所有的 TCP 相依性，識別意外連線、 您而定，遠端協力廠商系統和相依性 tootraditional 深色區域網路，例如 Active Directory 的對應。 服務對應會探索受管理的系統嘗試 toomake，失敗的網路連線可幫助您識別潛在的伺服器設定不正確，服務中斷與網路問題。

### <a name="incident-management"></a>事件管理
服務對應可協助避免問題隔離的 hello 猜測顯示連線系統的方式，並會影響彼此。 此外 tooidentifying 失敗的連線，它可協助識別設定不正確的負載平衡器、 令人意外或過度負載重要服務和 rogue 用戶端，例如交談 tooproduction 系統的程式開發人員電腦。 您可以使用整合式工作流程與 Operations Management Suite 變更追蹤，您也可以查看變更事件的後端的電腦或服務是否說明 hello 之事件的根本原因。

### <a name="migration-assurance"></a>移轉保證
您可以使用服務對應，有效地規劃、加速和驗證 Azure 移轉，以確保沒有遺漏任何項目，且不會發生意外的中斷。 您可以探索所有交互相依系統的需求 toomigrate 一起、 評估系統組態和容量，以及識別是否執行中的系統仍然會提供使用者或適合用於而不移轉解除委任。 Hello 移動完成之後，您可以檢查測試系統的用戶端負載和身分識別 tooverify 和客戶所連接。 如果子網路規劃與防火牆定義有問題，在服務對應對應中的連線失敗會為您需要連線的 toohello 系統。

### <a name="business-continuity"></a>業務持續性
如果您使用 Azure Site Recovery 需要定義您的應用程式環境，服務對應的 hello 復原順序說明可能會自動告訴您如何系統依賴彼此 tooensure 修復計劃是可靠。 藉由選擇的重要伺服器或群組，並檢視其用戶端，您可以識別哪些前端系統 toorecover hello 伺服器之後還原並在可用。 相反地，藉由查看重要的伺服器端的相依性，您可以識別哪些系統 toorecover 焦點系統就會還原之前。

### <a name="patch-management"></a>修補程式管理
服務對應，以顯示其他小組及伺服器相依於您的服務，因此您可以通知它們事先才進行修補系統增強 hello Operations Management Suite 系統更新評估貴用戶使用。 服務對應也可以顯示您的服務在修補並重新啟動之後是否可用且正確連線，藉此加強 Operations Management Suite 中的修補程式管理。


## <a name="mapping-overview"></a>對應概觀
服務對應的代理程式收集 hello 與伺服器上安裝這些詳細 hello 每個處理序的輸入及輸出連線 TCP 連線的所有處理序的相關資訊。 在 hello 清單中 hello 左窗格中，您可以選取電腦或群組都在指定的時間範圍內有服務對應的代理程式 toovisualize 及其相依性。 機器相依性會對應專注於特定的電腦，而它們會顯示所有 hello 機器直接 TCP 用戶端或伺服器的電腦。  機器群組對應會顯示多組伺服器及其相依性。

![服務對應概觀](media/oms-service-map/service-map-overview.png)

擴充機器 hello 對應 tooshow hello 與作用中的網路連線執行處理程序在 hello 選取時間範圍內。 展開的 tooshow 程序的詳細資料與服務對應的代理程式在遠端電腦時，只有與 hello 焦點機器進行通訊的處理序才會顯示。 無代理程式連接成 hello 焦點機器的前端機器 hello 計數會指出左邊 hello hello 處理程序連線到。 如果 hello 焦點機器正在未代理程式連線 tooa 後端的電腦，hello 後端伺服器包含在伺服器連接埠群組，以及其他連接 toohello 相同連接埠號碼。

根據預設，服務對應對應顯示 hello 30 分鐘的相依性資訊。 Hello 階段控制項在 hello 左上方，您可以使用查詢的歷程記錄的時間範圍的總 tooone 小時 tooshow hello 中尋找相依性的如何對應過去 （例如，在事件或變更發生之前）。 付費工作區的服務對應資料會儲存 30 天，免費工作區的服務對應資料則會儲存 7 天。

## <a name="status-badges-and-border-coloring"></a>狀態徽章和框線色彩
在 hello 底部 hello 對應中的每一部伺服器可以是一份狀態徽章傳達 hello 伺服器的狀態資訊。 hello 徽章指出有某些 hello 伺服器從一個 hello Operations Management Suite 方案整合的相關資訊。 按一下徽章會引導您直接 toohello hello 狀態詳細資料 hello 右窗格中。 hello 目前可用的狀態徽章包括警示、 服務台、 變更、 安全性和更新。

Hello 狀態徽章 hello 嚴重性，根據機器節點框線彩色紅色 （重大），黃色 （警告），或是藍色 （資訊）。 hello 色彩都代表任何 hello 狀態徽章的 hello 最嚴重狀態。 灰色框線代表沒有狀態指標的節點。

![狀態徽章](media/oms-service-map/status-badges.png)

## <a name="machine-groups"></a>機器群組
電腦群組可讓您 toosee 對應集中在一組伺服器，不只一個，才可看到的一個對應中的多層式應用程式或伺服器叢集的所有 hello 成員。

使用者選取的伺服器屬於群組在一起，並選擇 hello 群組的名稱。  然後，您可以選擇 tooview hello 群組的所有處理程序和連線，或檢視只有 hello 處理程序和連線的直接關聯 toohello hello 群組的其他成員。

![機器群組](media/oms-service-map/machine-group.png)

### <a name="creating-a-machine-group"></a>建立機器群組
toocreate 群組、 選取 hello 電腦您要在 hello 機器清單，然後按一下**新增 toogroup**。

![建立群組](media/oms-service-map/machine-groups-create.png)

您可以選擇**建立新**為 hello 群組命名。

![為群組命名](media/oms-service-map/machine-groups-name.png)

>[!NOTE]
>電腦群組目前限制的 too10 伺服器，但我們計劃 tooincrease 這項限制推出。

### <a name="viewing-a-group"></a>檢視群組
一旦您已建立一些群組，您可以選擇 hello 群組 索引標籤中檢視它們。

![[群組] 索引標籤](media/oms-service-map/machine-groups-tab.png)

該電腦群組，然後選取 hello 群組名稱 tooview hello 對應。
![電腦群組](media/oms-service-map/machine-group.png)hello 機器屬於 toohello 群組所述 hello 對應中的白色。

擴充 hello 群組會列出組成 hello 機器群組的 hello 機器。

![機器群組的機器](media/oms-service-map/machine-groups-machines.png)

### <a name="filter-by-processes"></a>依處理序篩選
您可以切換顯示 hello 群組中的所有處理程序和連線之間的 hello 地圖檢視，並只 hello 的直接關聯 toohello 電腦群組。  hello 預設檢視是 tooshow 所有處理程序。  您可以在 hello 上方 hello 地圖的篩選圖示，即可變更 hello 檢視。

![篩選群組](media/oms-service-map/machine-groups-filter.png)

當**所有處理程序**已選取，hello 對應會包含所有處理程序和每部 hello 電腦上的連線 hello 群組中。

![機器群組的所有處理序](media/oms-service-map/machine-groups-all.png)

如果您變更只 hello 檢視 tooshow**群組連線處理程序**，會縮小 hello 對應 tooonly 向這些處理程序和連線的直接連接 tooother 機器 hello 群組中建立的簡化的檢視。

![機器群組的已篩選處理序](media/oms-service-map/machine-groups-filtered.png)
 
### <a name="adding-machines-tooa-group"></a>新增機器 tooa 群組
tooadd 機器 tooan 現有的群組，請檢查 hello 方塊，然後再按一下 下一步的 toohello 機器**新增 toogroup**。  然後，選擇要 tooadd hello 機器 hello 群組。
 
### <a name="removing-machines-from-a-group"></a>從群組移除多部機器
在 hello 群組 清單中，展開 hello 群組名稱 toolist hello 機器 hello 電腦群組中。  然後，按一下 hello 省略符號功能表下一步 toohello 機器 tooremove 並選擇**移除**。

![從群組移除機器](media/oms-service-map/machine-groups-remove.png)

### <a name="removing-or-renaming-a-group"></a>移除或重新命名群組
按一下 hello 省略符號功能表下一步 toohello 群組名稱在 hello 群組清單中。

![機器群組功能表](media/oms-service-map/machine-groups-menu.png)


## <a name="role-icons"></a>角色圖示
某些處理序在機器上扮演特殊角色︰Web 伺服器、應用程式伺服器及資料庫等。 服務對應程序加上附註，並識別概覽 hello 角色處理程序或伺服器上所扮演的角色圖示 toohelp 機器方塊。

| 角色圖示 | 說明 |
|:--|:--|
| ![Web 伺服器](media/oms-service-map/role-web-server.png) | Web 伺服器 |
| ![應用程式伺服器](media/oms-service-map/role-application-server.png) | 應用程式伺服器 |
| ![資料庫伺服器](media/oms-service-map/role-database.png) | 資料庫伺服器 |
| ![LDAP 伺服器](media/oms-service-map/role-ldap.png) | LDAP 伺服器 |
| ![SMB 伺服器](media/oms-service-map/role-smb.png) | SMB 伺服器 |

![角色圖示](media/oms-service-map/role-icons.png)


## <a name="failed-connections"></a>失敗的連線
失敗的連線會顯示在服務對應的對應處理程序和電腦，並以紅色虛線指出用戶端系統失敗 tooreach 程序或連接埠。 如果該系統是 hello 一個嘗試 hello 無法連線，連線失敗會報告從任何具有已部署的服務對應代理程式的系統。 服務對應觀察失敗 tooestablish 的 TCP 通訊端連線的測量此處理程序。 此失敗可能源自防火牆後面，hello 用戶端或伺服器中設定不正確或無法使用遠端服務。

![失敗的連線](media/oms-service-map/failed-connections.png)

了解失敗的連線有助於疑難排解、移轉驗證、安全性分析和整體架構理解。 失敗的連接有時候無害的但它們通常指直接 tooa 問題，例如容錯移轉環境突然變得無法存取或無法 tootalk 正在雲端移轉後的兩個應用程式層級。

## <a name="client-groups"></a>用戶端群組
用戶端群組是在 hello 地圖上代表沒有相依性代理程式的用戶端電腦的方塊。 單一用戶端群組代表 hello 的個別處理序或電腦的用戶端。

![用戶端群組](media/oms-service-map/client-groups.png)

toosee hello 的用戶端群組選取 hello 群組中的 hello 伺服器的 IP 位址。 hello 群組的 hello 內容會列在 hello**用戶端群組內容**窗格。

![用戶端群組屬性](media/oms-service-map/client-group-properties.png)

## <a name="server-port-groups"></a>伺服器連接埠群組
伺服器連接埠群組是方塊，代表沒有相依性代理程式的伺服器上的伺服器連接埠。 hello 方塊包含 hello 伺服器連接埠以及連線 toothat 通訊埠與伺服器的 hello 數目的計數。 展開 hello 方塊 toosee hello 個別伺服器和連接。 如果在 [hello] 方塊中只有一部伺服器，會列出 hello 名稱或 IP 位址。

![伺服器連接埠群組](media/oms-service-map/server-port-groups.png)

## <a name="context-menu"></a>內容功能表
按一下頂端 hello hello 省略符號 （...） 的任何伺服器的權限會顯示 hello 內容功能表，該伺服器。

![失敗的連線](media/oms-service-map/context-menu.png)

### <a name="load-server-map"></a>載入伺服器對應
按一下**負載 Server 對應**會帶您 tooa hello 選取的伺服器做為新焦點機器 hello 與新的對應。

### <a name="show-self-links"></a>顯示自我連結
按一下**顯示 Self-Links**重繪 hello 伺服器節點，包括任何自我連結，這些是 TCP 連線的開始及結束於 hello 伺服器中的程序。 如果自我連結會顯示，太 hello 功能表命令變更**隱藏 Self-Links**，如此一來，您可以將它們關閉。

## <a name="computer-summary"></a>電腦摘要
hello**機器摘要**窗格包含伺服器的作業系統、 相依性計數，以及資料從其他的 Operations Management Suite 方案的概觀。 這些資料包括效能計量、服務台票證、變更追蹤、安全性和更新。

![[機器摘要] 窗格](media/oms-service-map/machine-summary.png)

## <a name="computer-and-process-properties"></a>電腦和處理序屬性
當您巡覽服務對應圖時，您可以選取機器和處理序 toogain 有關的其他內容及其屬性。 機器提供 DNS 名稱、 IPv4 位址、 CPU 和記憶體容量、 VM 類型、 作業系統和版本，最後重新啟動時間和 hello 識別碼及其 Operations Management Suite 和服務對應的代理程式的相關資訊。

![[機器屬性] 窗格](media/oms-service-map/machine-properties.png)

處理序詳細資料是收集自作業系統中繼資料，其內容與執行中的處理序有關，包括處理序名稱、處理序描述、使用者名稱和網域 (在 Windows 上)、公司名稱、產品名稱、產品版本、工作目錄、命令列，以及處理序開始時間。

![[處理序屬性] 窗格](media/oms-service-map/process-properties.png)

hello**程序摘要**窗格提供 hello 處理序的連線，包括其繫結連接埠、 輸入及輸出連線的其他資訊和失敗的連線。

![[處理序摘要] 窗格](media/oms-service-map/process-summary.png)

## <a name="operations-management-suite-alerts-integration"></a>Operations Management Suite 警示整合
服務對應整合與 hello 選取時間範圍中的 hello 選伺服器的 Operations Management Suite 警示 tooshow 引發警示。 hello 伺服器顯示的圖示，如果沒有目前的警示和 hello**機器警示**窗格會列出 hello 警示。

![[機器警示] 窗格](media/oms-service-map/machine-alerts.png)

tooenable 服務對應 toodisplay 相關警示，會建立警示規則引發特定的電腦。 toocreate 適當的警示：
- 包含子句 toogroup 電腦 (例如，**電腦間隔為 1 分鐘**)。
- 選擇 tooalert 根據度量的度量。

![警示組態](media/oms-service-map/alert-configuration.png)


## <a name="operations-management-suite-log-events-integration"></a>Operations Management Suite 記錄事件整合
服務對應與整合記錄搜尋 tooshow hello 選伺服器的所有可用的記錄事件計數 hello 選取時間範圍內。 您可以按一下 hello 清單中的事件計數 toojump tooLog 搜尋任何資料列，並查看 hello 個別記錄事件。

![[機器記錄事件] 窗格](media/oms-service-map/log-events.png)

## <a name="operations-management-suite-service-desk-integration"></a>Operations Management Suite 服務台整合
在這兩種解決方案都已啟用並設定您的 Operations Management Suite 工作區中，而自動與 hello IT 服務管理連接器的服務對應整合。 服務對應中的 hello 整合會標示為 「 服務台。 」 如需詳細資訊，請參閱[使用 IT 服務管理連接器將 ITSM 工作項目集中管理](https://docs.microsoft.com/azure/log-analytics/log-analytics-itsmc-overview)。

hello**機器服務台**窗格會列出所有 hello 選伺服器 hello 選取時間範圍內的 IT 服務管理事件。 如果沒有目前的項目和 hello 機器服務台窗格會列出這些 hello 伺服器就會顯示圖示。

![[機器服務台] 窗格](media/oms-service-map/service-desk.png)

tooopen hello 項目，在您連接 ITSM 解決方案中，按一下**檢視工作項目**。

按一下 記錄搜尋中的 hello 項目的 tooview hello 詳細資料**記錄搜尋中顯示**。


## <a name="operations-management-suite-change-tracking-integration"></a>Operations Management Suite 變更追蹤整合
當「服務對應」和「變更追蹤」這兩個解決方案皆已在 Operations Management Suite 工作區中啟用並設定時，便會自動進行整合。

hello**機器變更追蹤**窗格會列出所有變更，以最新的 hello 第一次，以及連結 toodrill 向 tooLog 搜尋其他詳細資料。

![[機器變更追蹤] 窗格](media/oms-service-map/change-tracking.png)

hello 以下影像是您可能會看到 ConfigurationChange 事件的詳細的檢視選取後**顯示在 記錄分析**。

![ConfigurationChange 事件](media/oms-service-map/configuration-change-event.png)


## <a name="operations-management-suite-performance-integration"></a>Operations Management Suite 效能整合
hello**機器效能** 窗格會顯示 hello 選伺服器的標準效能度量。 hello 度量包括 CPU 使用率、 記憶體使用量、 網路傳送和接收的位元組和一份 hello 上層處理程序，透過網路傳送和接收的位元組。 tooget hello 網路效能資料，您也必須啟用 hello Operations Management Suite 中的網路資料 2.0 方案。

![[機器效能] 窗格](media/oms-service-map/machine-performance.png)


## <a name="operations-management-suite-security-integration"></a>Operations Management Suite 安全性整合
當「服務對應」和「安全性與稽核」這兩個解決方案皆已在 Operations Management Suite 工作區中啟用並設定時，便會自動進行整合。

hello**機器安全性** 窗格會顯示 hello hello 選伺服器的 Operations Management Suite 安全性和稽核解決方案的資料。 hello 窗格會列出 hello 選取時間範圍內任何未處理的安全性問題 hello 伺服器的摘要。 按一下任何 hello 安全性問題的演習向下到記錄檔中搜尋相關的詳細資料。

![[機器安全性] 窗格](media/oms-service-map/machine-security.png)


## <a name="operations-management-suite-updates-integration"></a>Operations Management Suite 更新整合
當「服務對應」和「更新管理」這兩個解決方案皆已在 Operations Management Suite 工作區中啟用並設定時，便會自動進行整合。

hello**機器更新** 窗格會顯示 hello hello 選伺服器的 Operations Management Suite 更新管理方案的資料。 hello 窗格會列出任何遺失的更新伺服器 hello 摘要 hello 選取時間範圍內。

![[機器變更追蹤] 窗格](media/oms-service-map/machine-updates.png)

## <a name="log-analytics-records"></a>Log Analytics 記錄
服務對應的電腦和處理序清查資料可供在 Log Analytics 中進行[搜尋](../log-analytics/log-analytics-log-searches.md)。 您可以套用這個資料 tooscenarios 包含移轉規劃、 容量分析、 探索與視需要效能疑難排解。

每小時每個唯一的電腦和程序就會產生一個記錄，此外 toohello 記錄處理程序或電腦啟動或是初始 tooService 時所產生的對應字元。 這些記錄 hello 下表中都有 hello 屬性。 toofields hello hello ServiceMap Azure 資源管理員 API 中的電腦資源的對應欄位 hello 與 hello ServiceMapComputer_CL 事件中的值。 hello 欄位和值在 hello ServiceMapProcess_CL 事件 toohello 的欄位對應 hello hello ServiceMap Azure 資源管理員 API 中的處理序資源。 hello ResourceName_s 欄位符合 hello 對應的資源管理員資源 hello [名稱] 欄位。 

>[!NOTE]
>當服務對應功能成長時，這些欄位是主體 toochange。

有 tooidentify 獨特的程序和電腦，您可以使用內部產生的屬性：

- 電腦： 使用 ResourceId 或 ResourceName_s toouniquely 識別 Operations Management Suite 工作區中的電腦。
- 程序： 使用 ResourceId toouniquely 識別 Operations Management Suite 工作區中的處理序。 ResourceName_s 內是唯一的 hello hello 機器的 hello 處理序正在執行 (MachineResourceName_s) 內容 

指定的處理序和指定的時間範圍內的電腦可以存在多個記錄，因為查詢可以傳回多筆記錄的 hello 同一部電腦或處理程序。 只有 tooinclude hello 的最近記錄，加入"|重複資料刪除 ResourceId"toohello 查詢。

### <a name="servicemapcomputercl-records"></a>ServiceMapComputer_CL 記錄
類型為 *ServiceMapComputer_CL* 的記錄會有伺服器 (具有服務對應代理程式) 的清查資料。 這些記錄 hello 下表中都有 hello 屬性：

| 屬性 | 說明 |
|:--|:--|
| 類型 | *ServiceMapComputer_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | hello hello 工作區中的機器的唯一識別碼 |
| ResourceName_s | hello hello 工作區中的機器的唯一識別碼 |
| ComputerName_s | hello 電腦 FQDN |
| Ipv4Addresses_s | Hello 伺服器的 IPv4 位址的清單 |
| Ipv6Addresses_s | 一份 hello 伺服器的 IPv6 位址 |
| DnsNames_s | DNS 名稱的陣列 |
| OperatingSystemFamily_s | Windows 或 Linux |
| OperatingSystemFullName_s | hello hello 作業系統的完整名稱  |
| Bitness_s | hello 位元版本的 hello 機器 （32 位元或 64 位元）  |
| PhysicalMemory_d | hello 實體記憶體 （mb） |
| Cpus_d | hello Cpu 數目 |
| CpuSpeed_d | hello 以 mhz 為單位的 CPU 速度|
| VirtualizationState_s | *unknown**physical**virtual* *hypervisor* |
| VirtualMachineType_s | *hyperv*、*vmware* 等等 |
| VirtualMachineNativeMachineId_g | hello 其 hypervisor 所指派的 VM 識別碼 |
| VirtualMachineName_s | hello VM 的 hello 名稱 |
| BootTime_t | hello 開機時間 |



### <a name="servicemapprocesscl-type-records"></a>ServiceMapProcess_CL 類型記錄
類型為 *ServiceMapProcess_CL* 的記錄會有伺服器 (具有服務對應代理程式) 上 TCP 連線處理程序的清查資料。 這些記錄 hello 下表中都有 hello 屬性：

| 屬性 | 說明 |
|:--|:--|
| 類型 | *ServiceMapProcess_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | hello hello 工作區中的處理序的唯一識別碼 |
| ResourceName_s | hello hello 執行所在的電腦中的處理序的唯一識別碼|
| MachineResourceName_s | hello 機器 hello 資源名稱 |
| ExecutableName_s | hello hello 程序可執行檔名稱 |
| StartTime_t | hello 程序集區開始時間 |
| FirstPid_d | hello hello 程序集區中的第一個 PID |
| Description_s | hello 程序描述 |
| CompanyName_s | hello hello 公司名稱 |
| InternalName_s | hello 內部名稱 |
| ProductName_s | hello hello 產品名稱 |
| ProductVersion_s | hello 產品版本 |
| FileVersion_s | hello 檔案版本 |
| CommandLine_s | hello 命令列 |
| ExecutablePath _s | hello 路徑 toohello 可執行檔 |
| WorkingDirectory_s | hello 工作目錄 |
| UserName | hello 的 hello 處理序執行的帳戶 |
| UserDomain | hello 的 hello 處理序執行的網域 |


## <a name="sample-log-searches"></a>記錄檔搜尋範例

### <a name="list-all-known-machines"></a>列出所有已知的機器
Type=ServiceMapComputer_CL | dedup ResourceId

### <a name="list-hello-physical-memory-capacity-of-all-managed-computers"></a>列出所有受管理電腦的 hello 實體記憶體容量。
Type=ServiceMapComputer_CL | select PhysicalMemory_d, ComputerName_s | Dedup ResourceId

### <a name="list-computer-name-dns-ip-and-os"></a>列出電腦名稱、DNS、IP 和 OS。
Type=ServiceMapComputer_CL | select ComputerName_s, OperatingSystemFullName_s, DnsNames_s, IPv4Addresses_s  | dedup ResourceId

### <a name="find-all-processes-with-sql-in-hello-command-line"></a>Hello 命令列中找到以"sql"的所有處理程序
Type=ServiceMapProcess_CL CommandLine_s = \*sql\* | dedup ResourceId

### <a name="find-a-machine-most-recent-record-by-resource-name"></a>以資源名稱尋找機器 (最新的記錄)
Type=ServiceMapComputer_CL "m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId

### <a name="find-a-machine-most-recent-record-by-ip-address"></a>以 IP 位址尋找機器 (最新的記錄)
Type=ServiceMapComputer_CL "10.229.243.232" | dedup ResourceId

### <a name="list-all-known-processes-on-a-specified-machine"></a>列出指定機器上的所有已知處理序
Type=ServiceMapProcess_CL MachineResourceName_s="m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId

### <a name="list-all-computers-running-sql"></a>列出所有執行 SQL 的電腦
Type=ServiceMapComputer_CL ResourceName_s IN {Type=ServiceMapProcess_CL \*sql\* | Distinct MachineResourceName_s} | dedup ResourceId | Distinct ComputerName_s

### <a name="list-all-unique-product-versions-of-curl-in-my-datacenter"></a>列出資料中心內所有唯一 curl 產品版本
Type=ServiceMapProcess_CL ExecutableName_s=curl | Distinct ProductVersion_s

### <a name="create-a-computer-group-of-all-computers-running-centos"></a>為所有執行 CentOS 的電腦建立電腦群組
Type=ServiceMapComputer_CL OperatingSystemFullName_s = \*CentOS\* | Distinct ComputerName_s


## <a name="rest-api"></a>REST API
Hello 伺服器、 處理序及相依性的所有資料在服務對應透過 hello[服務對應 REST API](https://docs.microsoft.com/rest/api/servicemap/)。


## <a name="diagnostic-and-usage-data"></a>診斷和使用量資料
Microsoft 會自動收集貴用戶使用服務對應服務的 hello 的使用方式和效能資料。 Microsoft 會使用此資料 tooprovide 並提升 hello 品質、 安全性與 hello 服務對應服務的完整性。 tooprovide 正確且有效率地疑難排解功能，hello 資料包括您的軟體，例如作業系統和版本、 IP 位址、 DNS 名稱，以及工作站名稱 hello 組態相關資訊。 Microsoft 不會收集姓名、地址或其他連絡資訊。

如需有關資料收集與使用方式的詳細資訊，請參閱 hello [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=512132)。


## <a name="next-steps"></a>後續步驟
深入了解[記錄搜尋](../log-analytics/log-analytics-log-searches.md)服務對應所收集的記錄分析 tooretrieve 資料中。


## <a name="troubleshooting"></a>疑難排解
請參閱 hello[疑難排解 hello 設定服務對應文件區段](operations-management-suite-service-map-configure.md#troubleshooting)。


## <a name="feedback"></a>意見反應
您對「服務對應」或這份文件有任何意見反應要提供給我們嗎？  請瀏覽我們的[使用者意見頁面](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map) \(英文\)，您可以在此頁面提出功能建議或對現有的建議進行投票。
