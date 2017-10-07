---
title: "aaa 開始使用 Azure 自動化 |Microsoft 文件"
description: "本文章會提供 Azure 自動化服務的概觀，藉由檢閱 hello 設計與實作中的詳細資料準備 tooonboard hello Azure marketplace 供應項目。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 434e8ea28c55ff9bda1d2e46a7a6b8378a3baa0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation"></a>開始使用 Azure 自動化

此使用者入門指南介紹 Azure 自動化的核心概念相關的 toohello 部署。 如果您在 Azure 中的新 tooAutomation 或使用自動化工作流程軟體，例如 System Center Orchestrator 的經驗，本指南將協助您了解如何 tooprepare 和上架的自動化。  之後，您會準備 toobegin 開發以支援您的處理程序自動化需求的 runbook。 


## <a name="automation-architecture-overview"></a>自動化架構概觀

![Azure 自動化概觀](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Azure 自動化是以提供可擴充又可靠，多租用戶的服務 (SaaS) 應用程式的軟體環境 tooautomate 與 runbook 處理和管理組態變更 tooWindows 及使用預期狀態設定的 Linux 系統(DSC) 中其他 Azure 雲端服務或在內部部署。 您自動化帳戶中的實體 (如 Runbook、資產、執行身分帳戶) 會與您的訂用帳戶和其他訂閱中的其他自動化帳戶隔離。  

您在 Azure 中執行的 Runbook 會在自動化沙箱上執行，而這些沙箱裝載於 Azure 平台即服務 (PaaS) 虛擬機器中。  自動化沙箱可為 Runbook 執行的下列所有層面提供租用戶隔離 – 模組、儲存體、 憶體、網路通訊、作業串流等。這個角色是由管理 hello 服務並不能從您的 Azure 或 Azure 自動化帳戶，您 toocontrol 的存取。         

tooautomate hello 部署及管理的資源在本機資料中心或其他雲端服務，建立自動化帳戶之後, 您可以指定一或多個機器 toorun hello[混合式 Runbook 背景工作 」 (HRW)](automation-hybrid-runbook-worker.md)角色。  每個 HRW 需要 hello Microsoft 管理代理程式連接 tooa 記錄分析工作區與自動化帳戶。  記錄分析是使用的 toobootstrap hello 安裝中，維護 hello Microsoft 管理代理程式，並監視 hello HRW hello 功能。  這些都是透過 Azure 自動化的 runbook 和 hello 指令 toorun 的 hello 傳遞。

您可以為您的 runbook 部署多個 HRW tooprovide 高可用性、 負載平衡 runbook 作業，且在某些情況下專門用它們來特定工作負載或環境。  hello Microsoft Monitoring Agent hello HRW 上的起始通訊以 hello 自動化服務透過 TCP 連接埠 443，而沒有任何輸入的防火牆需求。  當您有 runbook 上 HRW hello 環境內執行，而且您想要針對其他電腦或在該環境中的服務 hello runbook tooperform 管理工作，可能會那里 runbook 可 hello 其他連接埠必須能夠存取。  如果您的 IT 安全性原則不允許您的網路 tooconnect toohello 網際網路上的電腦，請檢閱 hello 文件[OMS 閘道](../log-analytics/log-analytics-oms-gateway.md)，做為 proxy 的 hello HRW toocollect 工作的狀態和接收的設定資訊您的自動化帳戶。

Hello hello 電腦上 hello 本機系統帳戶內容中執行 HRW 上執行的 Runbook，這是 hello 建議的安全性內容時 hello 本機的 Windows 電腦上執行系統管理動作。 如果您想針對 hello 本機電腦以外的資源 hello runbook toorun 工作時，您可能需要 toodefine hello 自動化帳戶，您可以用來存取從 hello runbook，並且使用 tooauthenticate 與 hello 外部資源的安全認證資產。 您可以使用[認證](automation-credentials.md)，[憑證](automation-certificates.md)，和[連接](automation-connections.md)cmdlet 可讓您可以驗證它們，toospecify 認證讓您與您在 runbook 中的資產。

儲存在 Azure 自動化 DSC 設定可以直接套用的 tooAzure 虛擬機器。 其他實體和虛擬機器可以從 hello Azure Automation DSC 提取伺服器要求組態。  如需管理您在內部部署實體或虛擬 Windows 和 Linux 系統的組態，您不需要 toodeploy 任何基礎結構 toosupport hello 自動化 DSC 提取伺服器，只的對外網際網路存取從受 Automation DSC 的每個系統 toobe透過 TCP 連接埠 443 toohello OMS 服務進行通訊。   

## <a name="prerequisites"></a>必要條件

### <a name="automation-dsc"></a>自動化 DSC
Azure 自動化 DSC 可以用的 toomanage 各種機器：

* 執行 Windows 或 Linux 的 Azure 虛擬機器 (傳統)
* 執行 Windows 或 Linux 的 Azure 虛擬機器
* 執行 Windows 或 Linux 的 Amazon Web Services (AWS) 虛擬機器
* 位於內部部署或 Azure 或 AWS 以外之雲端中的實體/虛擬 Windows 電腦
* 位於內部部署或 Azure 或 AWS 以外之雲端中的實體/虛擬 Linux 電腦

Windows Azure 自動化 toobe 無法 toocommunicate hello PowerShell DSC 代理程式必須安裝 hello 最新版本的 WMF 5。 hello 最新版 hello [PowerShell DSC for Linux 的代理程式](https://www.microsoft.com/en-us/download/details.aspx?id=49150)必須安裝 Linux toobe 無法 toocommunicate 與 Azure 自動化。

### <a name="hybrid-runbook-worker"></a>Hybrid Runbook Worker  
當指定電腦 toorun 混合式 runbook 作業，此電腦必須已 hello 下列：

* Windows Server 2012 或更新版本
* Windows PowerShell 4.0 或更新版本。  我們建議來增加可靠性的 hello 電腦上安裝 Windows PowerShell 5.0。 您可以從 hello 下載 hello 新版[Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=50395)
* 至少雙核心
* 至少 4 GB 的 RAM

### <a name="permissions-required-toocreate-automation-account"></a>所需的權限 toocreate 自動化帳戶
toocreate 或更新自動化帳戶，您必須遵循特定的權限的 hello 和必要的使用權限 toocomplete 本主題。   
 
* 在訂單 toocreate 自動化帳戶，您的 AD 使用者帳戶需要 toobe 加入的 tooa 角色與權限相等 toohello 擁有者角色 Microsoft.Automation 資源的發行項中所述[Azure 自動化中的角色型存取控制](automation-role-based-access-control.md).  
* 如果設定太 hello 應用程式登錄設定**是**，Azure AD 租用戶中的非系統管理使用者可以[註冊 AD 應用程式](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions)。  如果設定太 hello 應用程式登錄設定**否**，執行此動作的 hello 使用者必須是 Azure AD 中的全域管理員。 

如果您不是成員的 hello 訂用帳戶的 Active Directory 執行個體加入 toohello 全域系統管理員/共同管理員的角色 hello 訂用帳戶之前，您會做為來賓新增 tooActive 目錄。 在此情況下，您會收到 「 您沒有權限 toocreate...」 在 hello 警告**加入自動化帳戶**刀鋒視窗。 Toohello 全域系統管理員/共同管理員角色首先會從 hello 訂用帳戶的 Active Directory 執行個體，並重新加入 toomake 加入的使用者其完整的使用者在 Active Directory 中。 tooverify，請在此情況下，從 hello **Azure Active Directory** hello Azure 入口網站，選取在窗格**使用者和群組**，選取**所有使用者**和選取 hello 之後特定使用者，則選取**設定檔**。 hello 值 hello**使用者類型**hello 使用者設定檔 下的屬性不可等於**客體**。

## <a name="authentication-planning"></a>驗證規劃
Azure 自動化可讓您針對資源 tooautomate 工作在 Azure 中，在內部，與其他雲端提供者。  為了讓 runbook tooperform 必要的動作，它必須具有權限 toosecurely 存取 hello 資源 hello hello 訂用帳戶內所需的最小權限。  

### <a name="what-is-an-automation-account"></a>什麼是自動化帳戶 
您針對在 Azure 自動化中使用 hello Azure 指令程式的資源執行的所有 hello 自動化工作來都驗證 tooAzure 使用 Azure Active Directory 組織身分識別認證基礎驗證。  自動化帳戶是您用於 toohello 入口 tooconfigure toosign 並使用 Azure 資源的 hello 帳戶不同。  包含帳戶的自動化資源是 hello 下列：

* **憑證** - 包含用來從 Runbook 或 DSC 設定進行驗證的憑證，或予以新增。
* **連線**-包含驗證和組態資訊所需 tooconnect tooan 外部服務或應用程式從 runbook 或 DSC 設定。
* **認證**-為 PSCredential 物件，其中包含例如使用者名稱和密碼所需的安全性認證 tooauthenticate 從 runbook 或 DSC 設定。
* **整合模組**-是 PowerShell 模組隨附於 Azure 自動化帳戶 toomake 使用 runbook 和 DSC 設定內的 cmdlet。
* **排程** - 包含可在指定的時間 (包括週期性頻率) 啟動或停止 Runbook 的排程。
* **變數** - 包含 Runbook 或 DSC 設定提供的值。
* **DSC 設定**-PowerShell 指令碼說明如何 tooconfigure 作業系統功能或設定，或在 Windows 或 Linux 電腦上安裝應用程式。  
* **Runbook** 是一組工作，可在以 Windows PowerShell 為基礎的 Azure 自動化中執行一些自動程序。    

每個自動化帳戶的 hello 自動化資源與單一 Azure 區域相關聯，但自動化帳戶可以管理您的訂用帳戶中的所有 hello 資源。 如果您有需要的資料和資源 toobe 隔離的 tooa 特定地區的原則，請在不同的區域中建立自動化帳戶。

> [!NOTE]
> 自動化帳戶和它們所包含的 hello 資源 hello Azure 入口網站中建立，無法在 hello Azure 傳統入口網站存取。 如果您想 toomanage，這些帳戶或其使用 Windows PowerShell 的資源，您必須使用 hello Azure 資源管理員模組。
> 

當您在 hello Azure 入口網站中建立自動化帳戶時，您會自動建立兩個驗證實體：

* 執行身分帳戶。 此帳戶會在 Azure Active Directory (Azure AD) 中建立服務主體，並建立一個憑證。 它也會指派 hello 參與者角色型存取控制 (RBAC)，可使用 runbook 來管理資源管理員資源。
* 傳統執行身分帳戶。 此帳戶上傳管理憑證，使用 runbook 時，所使用的 toomanage 傳統資源。

以角色為基礎的存取控制使用的允許動作 tooan Azure AD 使用者帳戶和執行身分帳戶的 Azure Resource Manager toogrant，驗證該服務主體。  讀取[Azure 自動化文件中的角色型存取控制](automation-role-based-access-control.md)以取得進一步資訊 toohelp 開發您的模型來管理自動化的權限。  

#### <a name="authentication-methods"></a>驗證方法
hello 下表摘要說明 Azure Automation 支援的每個環境的 hello 不同的驗證方法。

| 方法 | 環境 
| --- | --- | 
| Azure 執行身分和傳統執行身分帳戶 |Azure Resource Manager 和 Azure 傳統部署 |  
| Azure AD 使用者帳戶 |Azure Resource Manager 和 Azure 傳統部署 |  
| Windows 驗證 |本機資料中心或其他雲端提供者使用 hello Hybrid Runbook Worker |  
| AWS 認證 |Amazon Web Services |  

在 hello**如何 to\Authentication 和安全性**區段中，支援文章提供概觀和實作步驟 tooconfigure 驗證這些環境中，不論是透過現有或新的帳戶專門用於該環境。  Hello Azure 執行身分與傳統執行身分帳戶，hello 主題[更新自動化執行身分帳戶](automation-create-runas-account.md)描述如何 tooupdate 您現有的自動化帳戶以 hello 執行身分帳戶從 hello 入口網站，或如果不是使用 PowerShell最初設定與執行身分或傳統執行身分帳戶。 如果您想要 toocreate 執行身分和傳統執行身分帳戶與您的企業憑證授權單位 (CA) 所核發的憑證，檢閱如何 toocreate hello 帳戶使用此發行項 toolearn 這項設定。     
 
## <a name="network-planning"></a>網路規劃
Hello Hybrid Runbook Worker tooconnect tooand 註冊使用 Microsoft Operations Management Suite (OMS)，它必須有存取 toohello 連接埠號碼，hello Url 如下所述。  此外，這是 toohello[連接埠和所需的 Url hello Microsoft Monitoring Agent](../log-analytics/log-analytics-windows-agents.md#network) tooconnect tooOMS。 如果您使用 proxy 伺服器 hello 代理程式與 hello OMS 服務之間進行通訊時，您會需要 tooensure，hello 適當資源可供存取。 如果您使用防火牆 toorestrict 存取 toohello 網際網路時，您需要 tooconfigure 您防火牆 toopermit 存取。

下列清單 hello 連接埠和 Url 的所需的 hello Hybrid Runbook Worker toocommunicate 與自動化的 hello 資訊。

* 連接埠︰只需要 TCP 443 以便進行傳出網際網路存取
* 全域 URL：*.azure-automation.net

如果您有一個定義特定區域的自動化帳戶，您想要與該地區的資料中心的 toorestrict 通訊 hello 下表提供 hello DNS 記錄的每個區域。

| **區域** | **DNS 記錄** |
| --- | --- |
| 美國中南部 |scus-jobruntimedata-prod-su1.azure-automation.net |
| 美國東部 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| 美國中西部 | wcus-jobruntimedata-prod-su1.azure-automation.net |
| 西歐 |we-jobruntimedata-prod-su1.azure-automation.net |
| 北歐 |ne-jobruntimedata-prod-su1.azure-automation.net |
| 加拿大中部 |cc-jobruntimedata-prod-su1.azure-automation.net |
| 東南亞 |sea-jobruntimedata-prod-su1.azure-automation.net |
| 印度中部 |cid-jobruntimedata-prod-su1.azure-automation.net |
| 日本東部 |jpe-jobruntimedata-prod-su1.azure-automation.net |
| 澳大利亞東南部 |ase-jobruntimedata-prod-su1.azure-automation.net |
| 英國南部 | uks-jobruntimedata-prod-su1.azure-automation.net |
| 美國政府維吉尼亞州 | usge-jobruntimedata-prod-su1.azure-automation.us |

如需 IP 位址，而不是名稱的清單，請下載並檢閱 hello [Azure 資料中心 IP 位址](https://www.microsoft.com/download/details.aspx?id=41653)來自 hello Microsoft 下載中心的 xml 檔案。 

> [!NOTE]
> 此檔案包含 hello IP 位址範圍 （包括運算、 SQL 和儲存體的範圍） 用於 hello Microsoft Azure 資料中心。 更新的檔案會公佈每週以反映目前部署的 hello 範圍和任何後續變更 toohello IP 範圍。 出現在 hello 檔案中的新範圍將不用於 hello 資料中心至少一週。 請下載 hello 新的 xml 檔案每週和您的站台上執行 hello 必要的變更 toocorrectly 識別服務在 Azure 中執行。 快速路由使用者可能注意到這個檔案使用 tooupdate hello BGP 公告的 hello Azure 空間每個月的第一週。 
> 

## <a name="creating-an-automation-account"></a>建立自動化帳戶

有不同的方式，您可以在 hello Azure 入口網站中建立自動化帳戶。  下表中的 hello 介紹每種類型的部署經驗，以及它們之間的差異。  

|方法 | 說明 |
|-------|-------------|
| 從 hello Marketplace 選取自動化和控制 | 供應項目，建立自動化帳戶，以及 OMS 工作區連結 tooone 另一個 hello 相同資源群組和區域。  與 OMS 的整合也包括使用記錄分析 toomonitor 的 hello 優點和 runbook 工作狀態和作業資料流分析經過一段時間和運用進階的功能 tooescalate 或調查問題。 hello 供應項目也會將部署 hello 變更追蹤及更新管理解決方案，可依預設會啟用。 |
| 從 hello Marketplace 選取自動化 | 建立新的或現有的資源群組不是連結的 tooan OMS 工作區，且不包含任何可用的方案從 hello 自動化和控制供應項目中的自動化帳戶。 這是為您介紹 tooAutomation 具有基本設定，並可協助您了解 toowrite runbook、 DSC 設定，以及使用 hello hello 服務的能力。 |
| 選取的管理解決方案 | 如果您選取的方案 – **[更新管理](../operations-management-suite/oms-solution-update-management.md)**， **[離峰時間期間的開始/停止 Vm](automation-solution-vm-management.md)**，或 **[變更追蹤](../log-analytics/log-analytics-change-tracking.md)**它們 tooselect 現有的自動化和 OMS 工作區中，會提示您，或提供 hello 選項 toocreate 同時做為所需的 hello 方案 toobe 部署您的訂用帳戶中。 |

本主題會引導您建立自動化帳戶和 OMS 工作區的上架 hello 自動化和控制供應項目。  獨立的自動化測試或 toopreview hello 服務帳戶，檢閱下列文章的 hello toocreate[建立獨立的自動化帳戶](automation-create-standalone-account.md)。  

### <a name="create-automation-account-integrated-with-oms"></a>建立與 OMS 整合的自動化帳戶
hello 建議方法 tooonboard 自動化是從 hello Marketplace 選取 hello 自動化和控制供應項目。  這會建立兩個自動化帳戶，並建立 OMS 工作區，包括 hello 選項 tooinstall hello 管理解決方案，可與 hello 供應項目與 hello 整合。  

1. 登入 toohello hello 訂用帳戶系統管理員角色的成員且 hello 訂用帳戶的共同管理員帳戶的 Azure 入口網站。

2. 按一下 [新增] 。<br><br> ![在 Azure 入口網站中選取 [新增] 選項](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  

3. 搜尋**自動化**，然後在 hello 搜尋結果選取**自動化和控制***。<br><br> ![從 Marketplace 搜尋並選取 [自動化與控制]](media/automation-offering-get-started/automation-portal-martketplace-select-automationandcontrol.png)。<br>   

4. 閱讀 hello 描述 hello 供應項目之後, 按**建立**。  

5. 在 hello**自動化和控制**設定刀鋒視窗中，選取**OMS 工作區**。  在 hello **OMS 工作區**刀鋒視窗中，選取 OMS 工作區連結的 toohello hello 自動化帳戶的同一個 Azure 訂閱時，或建立 OMS 工作區。  如果您沒有 OMS 工作區，選取**建立新的工作區**在 hello **OMS 工作區**刀鋒視窗中執行下列 hello: 
   - 指定的名稱 hello 新**OMS 工作區**。
   - 選取**訂用帳戶**toolink tooby 從清單中選取 hello 下拉式清單選取 hello 預設值是否不適當。
   - 對於 [資源群組]，您可以建立資源群組，或選取現有的資源群組。  
   - 選取 [位置] 。  Hello 可用的唯一位置就是目前**澳洲東南部**，**美國東部**，**東南亞**，**中央美國西部**，和**西歐**。
   - 選取 **定價層**。  hello 方案提供兩個層級： 釋放與每個節點 (OMS) 層。  hello 免費層的資料收集的每日保留週期及 runbook 工作執行階段的分鐘數的 hello 數量的上限。  hello 每個節點 (OMS) 的層上 hello 每日收集的資料量沒有限制。  
   - 選取 [自動化帳戶]。  如果您要建立新的 OMS 工作區，您都必須 tooalso 建立自動化帳戶，與 hello 新 OMS 工作區之前，指定包含您的 Azure 訂用帳戶、 資源群組與區域相關聯。  您可以選取**建立自動化帳戶**在 hello**自動化帳戶**刀鋒視窗中，提供下列 hello: 
  - 在 hello**名稱**欄位中，輸入 hello hello 自動化帳戶名稱。

    所有其他選項會自動填入根據選取的 hello OMS 工作區，不能修改這些選項。  Azure 執行身分帳戶是 hello 供應項目 hello 預設驗證方法。  一旦您按一下**確定**、 hello 組態選項會進行驗證，並建立 hello 自動化帳戶。  您可以追蹤其進度下的**通知**hello 功能表。 

    不然，選取現有的自動化執行身分帳戶。  您選取的 hello 帳戶不能連結的 tooanother OMS 工作區，否則 hello 刀鋒視窗中顯示通知訊息。  如果已經連結，您需要 tooselect 不同的自動化執行身分帳戶，或建立一個。

    完成之後 hello 所需的資訊，請按一下**建立**。  hello 資訊會驗證，而且會建立 hello 自動化帳戶 」 和 「 執行身分帳戶。  您會返回 toohello **OMS 工作區**刀鋒視窗會自動。  

6. 提供所需的 hello 資訊在 hello 之後**OMS 工作區**刀鋒視窗中，按一下 **建立**。  在驗證 hello 資訊並建立 hello 工作區時，您可以追蹤在其進度**通知**hello 功能表。  您會返回 toohello**將方案加入**刀鋒視窗。  

7. 在 hello**自動化和控制**設定刀鋒視窗中，確認您想 tooinstall hello 建議預先選取的方案。 如果您取消選取任何項目，可以稍後再個別安裝。  

8. 按一下**建立**tooproceed 上架自動化與 OMS 工作區。 驗證所有設定，然後它會試著 toodeploy hello 供應項目，您的訂用帳戶中。  此程序可能需要幾秒 toocomplete，而且您可以追蹤在其進度**通知**hello 功能表。 

Hello 供應項目是就緒之後，您可以開始建立工作以 hello 的 runbook，您啟用的管理解決方案，請部署[混合式 Runbook 背景工作](automation-hybrid-runbook-worker.md)角色或開始使用[記錄分析](https://docs.microsoft.com/azure/log-analytics)產生的雲端或內部部署環境中的資源 toocollect 資料。   

## <a name="next-steps"></a>後續步驟
* 您可藉由檢閱[測試 Azure 自動化執行身分帳戶驗證](automation-verify-runas-authentication.md)，確認新的自動化帳戶可以驗證 Azure 資源。
* tooget 入門建立 runbook，請先檢閱 hello[自動化的 runbook 類型](automation-runbook-types.md)支援和相關考量，在您開始撰寫前。


