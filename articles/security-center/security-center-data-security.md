---
title: "aaaAzure 安全性中心的資料安全性 |Microsoft 文件"
description: "本文件說明如何在 Azure 資訊安全中心管理和保護資料。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 33f2c9f4-21aa-4f0c-9e5e-4cd1223e39d7
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: yurid
ms.openlocfilehash: 30f8b11272dc5df6d485608abdaa62ba57e63f23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-data-security"></a>Azure 資訊安全中心資料安全性
toohelp 客戶防止、 偵測及回應 toothreats，Azure 資訊安全中心會收集並處理安全性相關的資料，包括組態資訊、 中繼資料、 事件記錄檔、 損毀傾印檔案，等等。 Microsoft 遵守 toostrict 相容性與安全性指導方針 — 從 toooperating 服務撰寫程式碼。

本文說明如何在 Azure 資訊安全中心管理和保護資料。

>[!NOTE] 
>從開始早期年 6 月 2017年，資訊安全中心將會使用 hello Microsoft Monitoring Agent toocollect 及儲存資料。 請參閱[Azure 安全性 Center 平台移轉](security-center-platform-migration.md)toolearn 更多。 本文章中的 hello 資訊表示資訊安全中心功能之後轉換 toohello Microsoft Monitoring Agent。
>


## <a name="data-sources"></a>資料來源
Azure 資訊安全中心會分析資料，從下列來源 tooprovide 可見性為您的安全性狀態的 hello、 識別的弱點可能會建議防護功能，以及偵測到作用中威脅：

- Azure 服務： 使用您已部署藉由與該服務的資源提供者通訊 hello Azure 服務組態相關資訊。
- 網路流量︰使用從 Microsoft 的基礎結構取樣的網路流量中繼資料，例如來源/目的地 IP/連接埠、封包大小和網路通訊協定。
- 合作夥伴解決方案：使用整合式合作夥伴解決方案 (例如防火牆和反惡意程式碼解決方案) 的安全性警示。 
- 您的虛擬機器和伺服器：使用設定資訊以及安全性事件的相關資訊，例如來自您虛擬機器的 Windows 事件和稽核記錄、IIS 記錄、syslog 訊息和損毀傾印檔。 此外，建立警示時，Azure 資訊安全中心可能會產生影響的 hello VM 磁碟的快照集並擷取 hello VM 磁碟，例如登錄檔，進行鑑識調查的機器成品相關的 toohello 警示。


## <a name="data-protection"></a>資料保護
**資料隔離**: hello 服務在每個元件上，資料以邏輯方式分開。 每個組織加上標記的所有資料。 這項標記作業在整個 hello 資料生命週期持續發生，它會強制執行各種層級的 hello 服務。

**資料存取**： 中順序 tooprovide 安全性建議和調查潛在的安全性威脅，Microsoft 人員可能存取收集的資訊，或由 Azure 服務，包括損毀傾印檔案，分析處理建立事件，VM磁碟的快照，並且可能會不小心包含客戶資料或個人資料與您的虛擬機器的成品。 我們將遵守 toohello [Microsoft Online Services 條款及隱私權聲明](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)，Microsoft 將不使用客戶資料，或衍生自它的資訊進行任何廣告或類似的商業用途處理的狀態。 我們只會為您的 Azure 服務，包括用途與提供這些服務相容的所需 tooprovide 使用客戶資料。 您會保留所有的權限 tooCustomer 資料。

**資料使用**： 使用模式，Microsoft 威脅情報看到跨多個租用戶 tooenhance 我們預防和偵測功能之後，我們這樣中所述的 hello 隱私權承諾根據我們[隱私權陳述式](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx)。

## <a name="data-location"></a>資料位置

**您 Workspace(s)**: hello 遵循 Geos，針對指定的工作區，以及從 Azure 虛擬機器，包括損毀傾印，以及某些類型的警示資料收集的資料會儲存在最近的工作區中的 hello。 

| VM 地區                        | 工作區地區 |
|-------------------------------|---------------|
| 美國、巴西、加拿大 | 美國 |
| 歐洲，英國        | 歐洲        |
| 亞太地區、日本、印度    | 亞太地區  |
| 澳大利亞                     | 澳大利亞     |

 
VM 磁碟快照集會儲存在 hello 相同 hello VM 磁碟儲存體帳戶。
 
虛擬機器和伺服器執行其他環境中，於例如內部部署，您可以指定 hello 工作區和儲存收集的資料區域。 

**Azure 資訊安全中心儲存體**： 地域儲存安全性警示，包括夥伴警示的詳細資訊，根據 hello toohello 位置相關 Azure 資源，而安全性健全狀況狀態的相關資訊和建議是集中儲存在 hello 是美國和歐洲根據 toocustomer 的位置。
Azure 資訊安全中心會收集損毀傾印檔案的暫時複本並加以分析，以取得惡意探索嘗試和成功入侵的證明。 Azure 資訊安全中心會執行這項分析內 hello 同一地區，因為 hello 工作區中，並刪除 hello 的暫時副本，當分析完成。

機器成品都會儲存在集中為 hello VM hello 相同的區域。 


## <a name="managing-data-collection-from-virtual-machines"></a>從虛擬機器管理資料收集

當您啟用 Azure 中的資訊安全中心時，已針對每個 Azure 訂用帳戶開啟資料收集。 您也可以開啟資料收集 hello Azure 資訊安全中心的安全性原則 區段中訂用帳戶。 資料收集為開啟時，對所有現有的 Azure 資訊安全中心會佈建 hello Microsoft Monitoring Agent 支援 Azure 虛擬機器和建立任何新的。 hello Microsoft 監視代理程式會掃描的各種安全性相關的組態和事件到[Windows 事件追蹤](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx)(ETW) 追蹤。 此外，hello 作業系統會執行 hello 機器中的 hello 期間引發事件記錄檔事件。 這類資料的範例包括︰作業系統類型和版本、作業系統記錄檔 (Windows 事件記錄檔)、執行中程序、電腦名稱、IP 位址、已登入的使用者和租用戶識別碼。 Microsoft Monitoring Agent hello 讀取事件記錄項目，並 ETW 追蹤，並將其複製 tooyour workspace(s) 進行分析。 hello Microsoft Monitoring Agent 也會將損毀傾印檔案 tooyour workspace(s) 複製。

如果您使用 Azure 安全性中心可用，您也可以停用資料收集 hello 安全性原則中的虛擬機器。 需要訂閱 hello 標準層上的資料收集。 即使已停用資料集合，仍然會啟用VM 磁碟快照集和構件集合。


## <a name="see-also"></a>另請參閱
在本文件中，您已了解如何在 Azure 資訊安全中心管理和保護資料。 toolearn 進一步了解 Azure 資訊安全中心，請參閱：

* [Azure 資訊安全中心計劃與作業指南](security-center-planning-and-operations-guide.md)— 了解如何 tooplan 並了解 hello 設計考量 tooadopt Azure 資訊安全中心。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)— 了解如何 toomonitor hello 您的 Azure 資源的健全狀況
* [Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) — 了解如何 toomanage 和回應 toosecurity 警示
* [監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)— 了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)— 尋找使用 hello 服務相關的常見問題集
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) — 尋找有關 Azure 安全性與相容性的部落格文章。
