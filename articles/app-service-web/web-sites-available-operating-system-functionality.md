---
title: "Azure App Service 上 aaaOperating 系統功能"
description: "了解 hello OS 功能可用 tooweb 應用程式、 行動應用程式後端，以及在 Azure App Service API 應用程式"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 39d5514f-0139-453a-b52e-4a1c06d8d914
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 695188c48102b10ece326fba8d50a5f55b03b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="operating-system-functionality-on-azure-app-service"></a>Azure App Service 上的作業系統功能
這篇文章描述就是可用 tooall 應用程式上執行的 hello 通用基準作業系統功能[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)。 此功能包含檔案、網路、登錄存取、診斷記錄和事件。 

<a id="tiers"></a>

## <a name="app-service-plan-tiers"></a>App Service 計劃層
App Service 會在多租用戶裝載環境中執行客戶應用程式。 應用程式部署在 hello**免費**和**共用**層中背景工作處理序共用的虛擬機器上部署的 hello 中應用程式時執行**標準**和**Premium**特別為 hello 單一客戶與相關聯的應用程式專用的虛擬機器上執行的各層。

因為應用程式的服務支援縮放順暢不同層之間，hello 安全性設定強制執行的應用程式服務的應用程式維持 hello 相同。 這可確保，應用程式不突然不同的行為，從某一層 tooanother 切換應用程式服務方案時，非預期的方式失敗。

<a id="developmentframeworks"></a>

## <a name="development-frameworks"></a>開發架構
應用程式服務定價層控制項 hello 計算資源 （CPU、 磁碟儲存體、 記憶體和網路輸出） 數量可用 tooapps。 不過，hello 廣度 tooapps 可用的 framework 功能仍會的 hello 相同不論 hello 縮放層級。

App Service 支援各種開發架構，包含 ASP.NET、傳統 ASP、node.js、PHP 和 Python，在 IIS 中這些架構全都以擴充功能形式執行。 在訂單 toosimplify 並正規化安全性設定，App Service 應用程式通常執行 hello 各種開發架構的預設設定。 其中一個方法 tooconfiguring 應用程式原本 toocustomize hello API 介面區和每個個別的開發架構的功能。 App Service 採取了更普通的方式，也就是不論應用程式開發架構為何，均啟用作業系統功能的一般基礎。

hello 下列各節摘要說明 hello 作業系統功能可用 tooApp 服務應用程式的一般類型。

<a id="FileAccess"></a>

## <a name="file-access"></a>檔案存取
App Service 中的各種磁碟機，包含本機磁碟機和網路磁碟機。

<a id="LocalDrives"></a>

### <a name="local-drives"></a>本機磁碟機
基本上，App Service 為 hello Azure PaaS （平台即服務） 基礎結構上執行的服務。 為一個結果，hello 本機的磁碟機的 「 附加 」 tooa 虛擬機器會 hello 相同磁碟機類型可用 tooany 背景工作角色在 Azure 中執行。 這包括在作業系統磁碟機 (D:\ 磁碟機 hello)、 包含 Azure 套件 cspkg 檔案專屬的應用程式服務 （和 無法存取 toocustomers），應用程式磁碟機和 「 使用者 」 的磁碟機 (hello C:\ 磁碟機)，其大小會因 hello 大小hello VM。

<a id="NetworkDrives"></a>

### <a name="network-drives-aka-unc-shares"></a>網路磁碟機 (亦稱為 UNC 共用)
可讓應用程式部署和維護的簡單的應用程式服務的 hello 唯一層面的其中一個是所有的使用者內容會儲存在 UNC 共用一組上。 此模型將輕易對應 toohello 的內容儲存在內部部署 web 裝載有多個負載平衡伺服器的環境使用的常見模式。 

在 App Service 中，每個資料中心內都已建立許多 UNC 共用。 每個資料中心的所有客戶的 hello 使用者內容的百分比會配置的 tooeach UNC 共用。 此外，所有的單一客戶的訂閱 hello 檔案內容永遠會放在 hello 相同 UNC 共用。 

請注意，由於 toohow 雲端服務運作，hello 特定虛擬機器負責裝載 UNC 共用將會隨時間變更。 這樣會保證，因為它們會向上和向下回到 hello 正常操作程序雲端期間，將會不同的虛擬機器掛接 UNC 共用。 基於這個理由，應用程式應該永遠不會進行硬式編碼的假設，經過一段時間會保持穩定的 UNC 檔案路徑中的 hello 機器資訊。 相反地，它們應該使用方便 hello*項*絕對路徑**D:\home\site**應用程式服務所提供。 此項的絕對路徑會提供的可攜式應用程式和-使用者-無從驗證的方法參考 tooone 自己應用程式。 使用**D:\home\site**，其中一個可以從應用程式 tooapp 傳送共用的檔案，而不需要 tooconfigure 每項傳輸是新的絕對路徑。

<a id="TypesOfFileAccess"></a>

### <a name="types-of-file-access-granted-tooan-app"></a>類型的檔案存取權授與 tooan 應用程式
在資料中心內的特定 UNC 共用上，每個客戶的訂用帳戶都有一個保留的目錄結構。 客戶可能會有多個應用程式特定資料中心內建立，所以所有屬於 tooa 單一客戶訂用帳戶的 hello 目錄會建立在 hello 相同 UNC 共用。 hello 共用可能包括例如內容、 錯誤和診斷的記錄檔和較早版本的原始檔控制所建立的 hello 應用程式的目錄。 如預期般，客戶的應用程式目錄所讀取和寫入存取，在執行階段 hello 應用程式的應用程式程式碼。

Hello 上的本機磁碟機附加 toohello 虛擬機器以執行應用程式、 應用程式服務保留 hello 應用程式專屬的暫存本機儲存體的 C:\ 磁碟機上的空間區塊。 雖然有完整讀取/寫入存取 tooits 自己暫存本機儲存體，儲存體，實際上不會預期的 toobe hello 應用程式程式碼直接使用的應用程式。 相反地，hello 意圖是 IIS 和 web 應用程式架構的 tooprovide 暫存檔案儲存體。 應用程式服務也會限制 hello 暫存本機儲存體可用 tooeach 應用程式 tooprevent 個別的應用程式耗用過多的本機檔案存放裝置的數量。

應用程式服務如何使用暫存本機儲存體的兩個範例是暫存 ASP.NET 檔案的 hello 目錄和 hello 目錄的 IIS 壓縮的檔案。 hello ASP.NET 編譯系統做為暫存編譯快取位置使用 hello"Temporary ASP.NET Files"目錄。 IIS 會使用 hello"IIS Temporary Compressed Files"目錄 toostore 壓縮回應的輸出。 這兩種類型的檔案使用狀況 （以及其他項目） 會重新對應應用程式服務 tooper 應用程式暫存本機儲存體中。 此重新對應可確保功能如預期般繼續運作。

App Service 中的每個應用程式執行，稱為隨機唯一的低權限背景工作處理序識別 hello"應用程式集區識別碼 」，這裡進一步說明： [http://www.iis.net/learn/manage/configuring-security/application-pool-identities](http://www.iis.net/learn/manage/configuring-security/application-pool-identities). 應用程式程式碼會使用這個身分識別為基本的唯讀存取 toohello 作業系統磁碟機 (D:\ 磁碟機 hello)。 這表示應用程式程式碼可以列出通用目錄結構和讀取作業系統磁碟機上的通用檔案。 雖然這可能會出現 toobe 稍微廣泛層級的存取權，hello 相同的目錄都可存取檔案，而且當您佈建背景工作角色在 Azure 中的託管服務，並讀取 hello 磁碟機內容。 

<a name="multipleinstances"></a>

### <a name="file-access-across-multiple-instances"></a>跨越多個執行個體的檔案存取
hello 主目錄包含應用程式的內容，而且應用程式程式碼可以寫入 tooit。 如果多個執行個體上執行應用程式，hello 主目錄是所有執行個體之間共用，讓所有的執行個體，請參閱 「 hello 相同的目錄。 因此，比方說，如果應用程式儲存 toohello 主目錄時上, 傳的檔案，這些檔案是立即可用 tooall 執行個體。 

<a id="NetworkAccess"></a>

## <a name="network-access"></a>網路存取
應用程式程式碼可以使用 TCP/IP，以及基礎 UDP 通訊協定 toomake 傳出網路連線 tooInternet 可存取的端點公開外部服務。 應用程式可以使用這些相同的通訊協定 tooconnect tooservices 內 Azure &#151; 例如，藉由建立 HTTPS 連線 tooSQL 資料庫。

也是有限的功能，應用程式 tooestablish 一個本機回送連接，而且具有該本機回送通訊端接聽應用程式。 此功能存在於主要 tooenable 應用程式接聽本機回送通訊端，其功能的一部分。 請注意每個應用程式會看到 「 私人 」 的回送連接。"A"的應用程式無法接聽 tooa"B"的應用程式所建立的本機回送通訊端。

此外，還支援具名管道作為共同執行應用程式的不同處理序之間的處理序間通訊 (IPC) 機制。 例如，hello IIS FastCGI 模組會依賴具名管道 toocoordinate hello 個別處理程序，執行 PHP 網頁。

<a id="Code"></a>

## <a name="code-execution-processes-and-memory"></a>程式碼執行、處理序和記憶體
如先前所述，應用程式會使用隨機應用程式集區身分識別在低權限的背景工作角色處理序內部執行。 應用程式程式碼必須存取 toohello 記憶體空間與 hello 工作者處理序，以及 CGI 處理序或其他應用程式可能會產生任何子處理序相關聯。 不過，一個應用程式無法存取 hello 記憶體或資料的另一個應用程式，即使它是在 hello 相同的虛擬機器。

應用程式可以執行利用支援的 Web 開發架構撰寫的指令碼或頁面。 應用程式服務未設定任何 web 架構設定 toomore 限制模式。 例如，應用程式服務上執行的 ASP.NET 應用程式以 「 完整 」 信任執行，以相對於的 tooa 更多限制的信任模式。 Web 架構，包括傳統 ASP 和 ASP.NET 中，可以呼叫像 hello Windows 作業系統上的預設註冊的 ADO (ActiveX Data Objects) 同處理序的 COM 元件 （但未超出處理程序的 COM 元件）。

應用程式可以繁衍和執行任意程式碼。 像繁衍 （spawn） 命令殼層或 PowerShell 指令碼時允許的應用程式 toodo 項目。 不過，即使從應用程式，可執行程式，則可以產生任意程式碼和程序和指令碼是 toohello 仍受限制的權限授與 toohello 父應用程式集區。 例如，應用程式可以繁衍 （spawn) 會輸出 HTTP 呼叫的可執行檔，但同一個執行檔無法嘗試 toounbind hello IP 位址的虛擬機器從其 NIC 進行傳出的網路呼叫 toolow 權限的程式碼，但嘗試 tooreconfigure 網路設定的虛擬機器上需要系統管理權限。

<a id="Diagnostics"></a>

## <a name="diagnostics-logs-and-events"></a>診斷記錄和事件
另一組資料的某些應用程式嘗試 tooaccess 的記錄資訊。 App Service 中執行的記錄資訊可用 toocode hello 類型包含診斷和記錄檔也更容易存取 toohello 應用程式的應用程式所產生的資訊。 

比方說，是使用中的應用程式所產生的 W3C HTTP 記錄檔可用 hello 網路中的記錄目錄的共用位置建立 hello 應用程式中，或如果客戶的 blob 儲存體中，您可以使用已設定的 W3C 記錄 toostorage。 hello 第二種選項可讓大量的記錄檔 toobe 收集不含 hello 風險超出 hello 與網路共用相關聯的檔案儲存體限制。

同樣地，從.NET 應用程式的資訊可以也被記錄使用選項 toowrite hello.NET 追蹤和診斷基礎結構，即時地診斷 hello 追蹤資訊 tooeither hello 應用程式的網路共用，或者 tooa blob 儲存體位置。

區域不是使用 tooapps 的診斷記錄和追蹤的是 Windows ETW 事件和常見的 Windows 事件記錄檔 （例如系統、 應用程式及安全性事件記錄檔）。 因為 ETW 追蹤資訊可能會檢視整部電腦 (hello right 的 Acl），讀取和寫入存取 tooETW 事件將會遭到封鎖。 開發人員可能會注意到該應用程式開發介面呼叫 tooread 和寫入的 ETW 事件及一般的 Windows 事件記錄檔顯示 toowork，但這是因為應用程式服務 「 假裝"hello 呼叫使其顯示 toosucceed。 事實上，hello 應用程式程式碼沒有包含存取 toothis 事件資料。

<a id="RegistryAccess"></a>

## <a name="registry-access"></a>登錄存取
應用程式有唯讀存取 toomuch （雖然不是全部） 的 hello 登錄 hello 虛擬機器上執行。 在實務上，這表示允許唯讀存取 toohello 本機 Users 群組的登錄機碼是由應用程式存取。 目前不支援讀取或寫入存取的 hello 登錄一個區域是 hello HKEY\_目前\_使用者登錄區。

被封鎖的寫入存取 toohello 登錄，包括存取 tooany 每位使用者的登錄機碼。 Hello 應用程式的觀點而言，寫入權限 toohello 登錄應永遠不會依賴 hello Azure 環境中應用程式可以 （且沒有），因為取得不同的虛擬機器之間移轉。 hello 只永續性的可寫入儲存體可由應用程式相依於是 hello hello 應用程式服務 UNC 共用上儲存的每個應用程式內容的目錄結構。 

## <a name="more-information"></a>詳細資訊

[Azure Web 應用程式沙箱](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)-hello 大部分最新的應用程式服務的 hello 執行環境相關資訊。 此頁面是直接由應用程式服務開發團隊 hello 維護。

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 


