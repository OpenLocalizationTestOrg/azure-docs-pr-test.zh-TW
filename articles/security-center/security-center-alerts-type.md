---
title: "由 Azure 資訊安全中心中的型別 aaaSecurity 警示 |Microsoft 文件"
description: "這篇文章討論 hello 不同的 Azure 資訊安全中心中可用的安全性警示。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b3e7b4bc-5ee0-4280-ad78-f49998675af1
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: ee69cb9035c35f5bc2ed51f9b9d6f29486b4caf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-security-alerts-in-azure-security-center"></a>了解 Azure 資訊安全中心的安全性警示
這篇文章可協助您 toounderstand hello 不同類型的安全性警示和相關的深入資訊，都是在 Azure 資訊安全中心。 如需有關如何 toomanage 警示和事件，請參閱[中 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)。

> [!NOTE]
> tooset 向上進階偵測，升級 tooAzure 安全性 Center 標準。 提供 60 天的免費試用。 選取 tooupgrade**定價層**在 hello[安全性原則](security-center-policies.md)。 toolearn 詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/security-center/)。
>

## <a name="what-type-of-alerts-are-available"></a>可以使用何種類型的警示？
Azure 資訊安全中心使用不同的[偵測功能](security-center-detection-capabilities.md)tooalert 作為目標環境的客戶 toopotential 攻擊。 觸發 hello hello 資源做為目標、 警示以及 hello hello 攻擊的來源，這些警示會包含 hello 等重要資訊。 包含警示中的 hello 資訊依據分析使用 toodetect hello 威脅 hello 類型而異。 事件可能還會包含其他內容相關的資訊，在調查威脅時很有用。  本文章提供 hello 下列警示類型的相關資訊：

* 虛擬機器行為分析 (VMBA)
* 網路分析
* 資源分析
* 內容相關的資訊

## <a name="virtual-machine-behavioral-analysis"></a>虛擬機器行為分析
Azure 資訊安全中心可以使用行為分析 tooidentify 洩漏資源，根據虛擬機器的事件記錄檔的分析。 例如：程序建立事件和登入事件。 此外，沒有與其他支援廣泛的行銷活動的辨識項的訊號 toocheck 相互關聯。

> [!NOTE]
> 如需資訊安全中心偵測功能運作方式的詳細資訊，請參閱 [Azure 資訊安全中心的偵測功能](security-center-detection-capabilities.md)。
>

### <a name="crash-analysis"></a>損毀分析
損毀傾印記憶體分析會使用方法 toodetect 複雜惡意程式碼是無法 tooevade 傳統的安全性解決方案。 各種形式的惡意程式碼嘗試 tooreduce hello 的永遠不會寫入 toodisk，或是加密軟體元件撰寫 toodisk 偵測到的防毒產品的機率。 透過使用傳統的反惡意程式碼方法，讓 hello 惡意程式碼難以 toodetect。 不過，這種惡意程式碼可以偵測到使用記憶體分析，因為惡意程式碼必須保留在記憶體中順序 toofunction 的追蹤。

軟體損毀，損毀傾印會擷取 hello hello 損毀時的記憶體部分。 惡意程式碼中，一般應用程式或系統問題可能因為 hello 損毀。 藉由分析 hello 記憶體 hello 損毀傾印中的，資訊安全中心可以偵測技術軟體中使用 tooexploit 弱點，存取機密資料，並暗中遭到洩露的機器內持續。 這是具有最小的效能影響 toohosts hello 分析是的 hello 回資訊安全中心 」 結尾所執行。

hello 遵循欄位都是常見 toohello 損毀傾印警示範例本文中稍後出現：

* 傾印檔案以： Hello 損毀傾印檔案的名稱。
* PROCESSNAME: Hello 損毀處理序名稱。
* PROCESSVERSION: Hello 損毀處理序版本。

### <a name="shellcode-discovered"></a>探索到 Shellcode
Shellcode 是 hello 裝載惡意程式碼利用軟體弱點後執行。 此警示代表毀損傾印分析偵測到的可執行程式碼顯現經常由惡意承載執行的行為。 雖然非惡意軟體可能會執行這種行為，不過這不是一般軟體開發的實務做法。

hello Shellcode 警示範例提供下列額外欄位的 hello:

* 在記憶體中的 hello shellcode 位址： hello 位置。

以下是本類型之警示的範例：

![Shellcode 警示](./media/security-center-alerts-type/security-center-alerts-type-fig2.png)

### <a name="module-hijacking-discovered"></a>探索到模組攔截
Windows 會使用動態連結程式庫 (Dll) tooallow 軟體 tooutilize 常見 Windows 系統的功能。 DLL 劫持惡意程式碼變更時發生 hello DLL 載入順序 tooload 惡意裝載到記憶體中，可以執行任意程式碼。 此警示表示 hello 損毀傾印分析偵測到名稱類似的模組載入從兩個不同的路徑。 其中一個 hello 載入路徑是來自一般 Windows 系統二進位檔位置。

合法軟體開發人員偶爾會變更非惡意的原因，例如檢測、 擴充 hello Windows 作業系統，或擴充 Windows 應用程式的 hello DLL 載入順序。 toohelp 區分惡意與潛在良性變更 toohello DLL 載入順序時，Azure 資訊安全中心檢查載入的模組是否符合 tooa 可疑的設定檔。 這項檢查的 hello 結果指出 hello 警示 hello 「 簽章 」 欄位，而且會反映在 hello 嚴重性 hello 警示、 警示描述，以及警示的修復步驟。 tooresearch hello 模組是否合法或惡意的分析 hello hello 劫持模組副本磁碟上。 例如，您可以驗證 hello 檔案的數位簽章，或執行的防毒掃描。

此外 toohello hello 早"Shellcode 探索 」 一節所述共通的欄位，此警示提供下列欄位的 hello:

* 簽章： 表示是否 hello 劫持模組符合 tooa 可疑的行為設定檔。
* HIJACKEDMODULE: hello hello 名稱劫 Windows 系統模組。
* HIJACKEDMODULEPATH: hello hello 路徑劫 Windows 系統模組。
* Hello 劫持模組 HIJACKINGMODULEPATH: hello 路徑。

以下是本類型之警示的範例：

![模組攔截警示](./media/security-center-alerts-type/security-center-alerts-type-fig3.png)

### <a name="masquerading-windows-module-detected"></a>偵測到偽裝的 Windows 模組
惡意程式碼可能會使用 Windows 系統二進位檔 (例如，SVCHOST 一般名稱。EXE) 或模組 (例如，NTDLL。DLL) 太*blend*和混淆 hello 性質 hello 惡意軟體的系統管理員。 此警示表示 hello 損毀傾印分析偵測到該 hello 損毀傾印檔案包含使用 Windows 系統模組名稱，但不是符合其他準則典型的 Windows 模組的模組。 磁碟副本 hello 偽裝模組上的分析 hello 可能提供這個模組的 hello 合法或惡意的本質的詳細資訊。 分析可能包括︰

* 請確認該問題的 hello 檔案隨附的合法軟體套件的一部分。
* 請確認 hello 檔案的數位簽章。
* Hello 檔案上執行的防毒掃描。

此外 toohello 通用欄位前面 hello"Shellcode 探索 」 一節中所述，此警示提供下列其他欄位的 hello:

* 詳細資料： 描述 hello 模組中繼資料是否有效，以及是否 hello 模組已載入的系統路徑。
* 名稱： hello hello 偽裝 Windows 模組名稱。
* 路徑： hello 路徑 toohello 偽裝 Windows 模組。

此警示也會擷取並顯示特定欄位 hello 模組的 PE 標頭，例如 「 總和檢查碼 」 和 「 時間 」 戳記。 只有 hello 欄位會出現在 hello 模組時，才會顯示這些欄位。 請參閱 hello [Microsoft PE 和 COFF 規格](https://msdn.microsoft.com/windows/hardware/gg463119.aspx)如需詳細資訊，這些欄位上。

以下是本類型之警示的範例：

![偽裝的 Windows 警示](./media/security-center-alerts-type/security-center-alerts-type-fig4.png)

### <a name="modified-system-binary-discovered"></a>探索到修改過的系統二進位檔
惡意程式碼可能修改順序 toocovertly 存取資料的核心系統二進位碼檔案，或暗中遭到洩露的系統上保存。 此警示表示 hello 損毀傾印分析程式偵測到核心 Windows 的 OS 二進位檔，已修改記憶體中或在磁碟上。

合法軟體開發人員偶爾會為了非惡意的原因而修改記憶體中的系統模組，如 Detours 或處理應用程式相容性。 toohelp 區分惡意與潛在合法的模組時，Azure 資訊安全中心檢查 hello 修改的模組是否符合 tooa 可疑的設定檔。 這項檢查的 hello 結果會指示 hello 嚴重性 hello 警示、 警示描述，以及警示的修復步驟。

此外 toohello 通用欄位前面 hello"Shellcode 探索 」 一節中所述，此警示提供下列其他欄位的 hello:

* MODULENAME： 修改系統二進位 hello 的名稱。
* MODULEVERSION: Hello 的版本修改系統二進位檔案。

以下是本類型之警示的範例：

![系統二進位檔警示](./media/security-center-alerts-type/security-center-alerts-type-fig5.png)

### <a name="suspicious-process-executed"></a>已執行可疑的處理序
資訊安全中心識別可疑的處理程序執行 hello 目標虛擬機器，而且會觸發警示。 hello 偵測看起來不 hello 特定名稱，但看起來 hello 可執行檔的參數。 因此，即使 hello 攻擊者會重新命名可執行檔的 hello，資訊安全中心仍然可以偵測到 hello 可疑處理序。

以下是本類型之警示的範例：

![可疑的處理序警示](./media/security-center-alerts-type/security-center-alerts-type-fig6-new.png)

### <a name="multiple-domain-accounts-queried"></a>已查詢多個網域帳戶
資訊安全中心可以偵測到多個嘗試 tooquery Active Directory 網域帳戶，這是通常由期間網路探查攻擊者。 攻擊者可以利用這個技巧 tooquery hello 網域 tooidentify hello 使用者、 識別 hello 網域系統管理員帳戶，必須識別 hello 網域控制站，且也識別出 hello 潛在網域信任關係與其他網域的電腦。

以下是本類型之警示的範例：

![多個網域帳戶警示](./media/security-center-alerts-type/security-center-alerts-type-fig7-new.png)

### <a name="local-administrators-group-members-were-enumerated"></a>已列舉本機系統管理員群組成員

Windows Server 2016 和 Windows 10 中的 hello 安全性事件 4798，觸發清理程序時，資訊安全中心 」 即將 tootrigger 警示。 這種情況會發生在本機系統管理員群組列舉時，通常是由攻擊者在網路偵察期間所執行。 攻擊者可以利用這個技巧 tooquery hello 身分識別具有系統管理權限的使用者。

以下是本類型之警示的範例：

![本機系統管理員](./media/security-center-alerts-type/security-center-alerts-type-fig14-new.png)

### <a name="anomalous-mix-of-upper-and-lower-case-characters"></a>異常混用大寫和小寫字元

當它偵測到 hello 混用大寫和小寫字元，在 hello 命令列使用資訊安全中心將會觸發警示。 某些攻擊者可能會使用從區分大小寫這項技術 toohide 或雜湊型電腦的規則。

以下是本類型之警示的範例：

![異常混用](./media/security-center-alerts-type/security-center-alerts-type-fig15-new.png)

### <a name="suspected-kerberos-golden-ticket-attack"></a>可疑的 Kerberos 黃金票證攻擊

洩漏[krbtgt](https://technet.microsoft.com/library/dn745899.aspx)攻擊者 toocreate Kerberos 「 黃金票證，「 允許 hello 攻擊者 tooimpersonate 他們希望任何使用者可以使用金鑰。 資訊安全中心即將 tootrigger 警示，當它偵測到這種類型的活動。

> [!NOTE] 
> 如需 Kerberos 黃金票證的詳細資訊，請參閱 [Windows 10 認證竊取風險降低指南](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx)。

以下是本類型之警示的範例：

![黃金票證](./media/security-center-alerts-type/security-center-alerts-type-fig16-new.png)

### <a name="suspicious-account-created"></a>已建立可疑帳戶

若建立與現有內建系統管理權限帳戶非常相似的帳戶，資訊安全中心就會觸發警示。 這項技術可由攻擊者 toocreate rogue 帳戶 tooavoid 被注意到人力驗證所使用。
 
以下是本類型之警示的範例：

![可疑的帳戶](./media/security-center-alerts-type/security-center-alerts-type-fig17-new.png)

### <a name="suspicious-firewall-rule-created"></a>已建立可疑的防火牆規則

攻擊者可能會嘗試 toocircumvent 主機安全性，藉由建立自訂的防火牆規則 tooallow 惡意應用程式 toocommunicate 命令與控制，或透過 hello 網路透過 hello toolaunch 攻擊危害的主機。 資訊安全中心偵測到從可疑位置的可執行檔建立的新防火牆規則時，就會觸發警示。
 
以下是本類型之警示的範例：

![防火牆規則](./media/security-center-alerts-type/security-center-alerts-type-fig18-new.png)

### <a name="suspicious-combination-of-hta-and-powershell"></a>可疑的 HTA 和 PowerShell 組合

資訊安全中心偵測到 Microsoft HTML 應用程式主機 (HTA) 正在啟動 PowerShell 命令時會觸發警示。 這是攻擊者 toolaunch 惡意 PowerShell 指令碼所使用的技術。
 
以下是本類型之警示的範例：

![HTA 和 PS](./media/security-center-alerts-type/security-center-alerts-type-fig19-new.png)


## <a name="network-analysis"></a>網路分析
資訊安全中心網路威脅偵測的運作方式如下：從 Azure IPFIX (Internet Protocol Flow Information Export) 流量自動收集安全性資訊。 它會分析這項資訊通常相互關聯多個來源，tooidentify 威脅的資訊。

### <a name="suspicious-outgoing-traffic-detected"></a>偵測到可疑的連出流量
網路裝置可探索和剖析多 hello 與其他的系統類型相同的方式。 攻擊者通常會使用連接埠掃描或連接埠掃掠來開始攻擊。 在 hello 下一個範例中，您必須從 VM 的可疑安全殼層 (SSH) 流量。 在此案例中，可能有對外部資源的 SSH 暴力密碼破解或連接埠掃掠攻擊。

![可疑連出流量警示](./media/security-center-alerts-type/security-center-alerts-type-fig8.png)

此警示會提供資訊，您可以使用 tooidentify hello 資源所使用的 tooinitiate 這種攻擊。 此警示也會提供 tooidentify hello 入侵電腦、 hello 偵測時間，加上 hello 通訊協定和連接埠所使用的資訊。 此刀鋒視窗也可讓您可以的補救步驟的清單是使用的 toomitigate 此問題。

### <a name="network-communication-with-a-malicious-machine"></a>與惡意電腦的網路通訊
藉由利用 Microsoft 威脅情報摘要，Azure 資訊安全中心可以偵測與惡意 IP 位址通訊的遭入侵電腦。 在許多情況下，hello 惡意位址會是命令和控制中心。 在此情況下，資訊安全中心偵測到使用騎小馬載入器惡意程式碼，已完成，hello 通訊 (也稱為[Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF))。

![網路通訊警示](./media/security-center-alerts-type/security-center-alerts-type-fig9.png)

此警示所提供的資訊，可讓您所使用的 tooinitiate tooidentify hello 資源這種攻擊，hello 攻擊資源、 hello 犧牲者的 IP、 hello 攻擊者的 IP，以及 hello 偵測時間。

> [!NOTE]
> 為了保護隱私權，此螢幕擷取畫面的即時 IP 位址已遭到移除。
>
>

### <a name="possible-outgoing-denial-of-service-attack-detected"></a>偵測到可能的連出拒絕服務攻擊
異常來自一部虛擬機器的網路流量可能導致資訊安全中心 tootrigger 潛在的阻絕服務類型的攻擊。

以下是本類型之警示的範例：

![連出 DOS](./media/security-center-alerts-type/security-center-alerts-type-fig10-new.png)

## <a name="resource-analysis"></a>資源分析
資訊安全中心資源分析著重於在平台服務 (PaaS) 服務，例如以 hello hello 整合[Azure SQL Database 威脅偵測](../sql-database/sql-database-threat-detection.md)功能。 根據這些區域中的 hello 分析結果，資訊安全中心觸發程序資源相關的警示。

### <a name="potential-sql-injection"></a>潛在的 SQL 插入式攻擊
SQL 資料隱碼攻擊是惡意程式碼插入到稍後傳遞 tooan SQL Server 執行個體進行剖析和執行的字串的位置。 因為 SQL Server 會執行它收到的所有語法上有效的查詢，所以建構 SQL 陳述式的任何程序皆應檢閱其中是否有插入式攻擊弱點。 機器學習、 行為分析，以及異常偵測 toodetermine 可疑事件的執行時間可能您的 Azure SQL 資料庫中的位置，則會使用 SQL 威脅偵測。 例如：

* 離職員工嘗試的資料庫存取
* SQL 插入式攻擊
* 在使用者在家中的不尋常的存取 tooa 生產資料庫

![潛在的 SQL 插入式攻擊警示](./media/security-center-alerts-type/security-center-alerts-type-fig11.png)

在這項警示的 hello 資訊可能會使用的 tooidentify 遭受攻擊的 hello 資源、 hello 偵測時間，以及 hello 攻擊 hello 狀態。 它也提供一個連結 toofurther 調查步驟。

### <a name="vulnerability-toosql-injection"></a>弱點 tooSQL 資料隱碼
在資料庫上偵測到應用程式錯誤時，會觸發此警示。 此警示可能表示可能的弱點可能會 tooSQL 插入式攻擊。

![潛在的 SQL 插入式攻擊警示](./media/security-center-alerts-type/security-center-alerts-type-fig12-new.png)

### <a name="unusual-access-from-unfamiliar-location"></a>來自不熟悉位置的異常存取
找不到 hello 最後期間的 hello 伺服器上偵測到來自不熟悉的 IP 位址存取事件時，會觸發此警示。

![異常存取警示](./media/security-center-alerts-type/security-center-alerts-type-fig13-new.png)

## <a name="contextual-information"></a>內容相關的資訊
在調查中，分析師需要額外的內容 tooreach hello 威脅 hello 本質相關的結論以及 toomitigate 它。  例如，網路異常偵測，但不了解其他事 hello 網路上或考慮 toohello 目標資源具有它是每個硬碟 toounderstand 何種動作 tootake 下一步。 與 tooaid，安全性事件可能包含的成品、 相關的事件和資訊可能有助於 hello 調查。 hello 可用性的其他資訊會隨著 hello 偵測到威脅的型別和 hello 您環境的設定，且將無法使用所有安全性事件。

其他資訊是否可用，它將會顯示在 hello 安全性事件的警示 hello 清單下方。 這可能包括的資訊如：

- 清除事件記錄
- 從未知裝置插入的 PNP 裝置
- 不可採取動作的警示 

![異常存取警示](./media/security-center-alerts-type/security-center-alerts-type-fig20.png) 


## <a name="see-also"></a>另請參閱
在本文中，您學會有關 hello 不同警示類型的安全性資訊安全中心。 toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心處理安全性事件](security-center-incident.md)
* [Azure 資訊安全中心的偵測功能](security-center-detection-capabilities.md)
* [Azure 資訊安全中心規劃和操作指南](security-center-planning-and-operations-guide.md)
* [Azure 資訊安全中心常見問題集](security-center-faq.md)： 尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)：尋找有關 Azure 安全性與合規性的部落格文章。
