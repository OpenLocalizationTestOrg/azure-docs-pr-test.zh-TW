---
title: "您的物聯網從 hello 地面向上 aaaSecuring |Microsoft 文件"
description: "本文說明 Microsoft Azure IoT 套件 hello hello 內建安全性功能"
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 10252dfa-8313-4a97-9bd6-a3f1345dd3be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: a97e8cea753641e1e3c895f44e3fde1e5739d665
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-from-hello-ground-up"></a>從 hello 地面物聯網安全性
hello 物聯網 (IoT) 會造成唯一安全性、 隱私權和相容性挑戰 toobusinesses 全球。 與傳統網路技術，其中這些問題心力都圍繞軟體和實作的方式，不同的是 IoT 有關 hello e-security 與 hello 實體領域聚合時會發生什麼事。 保護 IoT 解決方案需要確保安全佈建裝置，這些裝置與 hello 雲端，以及在處理與儲存期間 hello 雲端中的安全資料保護之間的安全連線。 但是，會針對這類功能運作的是資源受限的裝置、根據地理位置分佈的部署，以及解決方案中的大量裝置。

這篇文章探討 hello Microsoft Azure IoT 套件提供安全且私用的物聯網雲端解決方案的方式。 hello Azure IoT 套件提供完整的端對端解決方案，具有 hello 接地從每個階段內建的安全性。 Microsoft 在安全軟體開發屬於 hello 軟體工程實務上，在我們的數十根目錄長時間的安全軟體開發體驗。 tooensure，安全性開發週期 (SDL) 是 hello 基本開發方法，與主機的基礎結構層級安全性服務，例如操作安全性保證 (OSA) 和 hello Microsoft 數位犯罪單元，結合Microsoft Security Response Center，以及 Microsoft 惡意程式碼防護中心。 

hello Azure IoT 套件提供的獨特功能，這會導致佈建、 連接到，並將資料儲存從 IoT 裝置輕鬆和透明，最重要的是，安全。 在本文中，我們檢驗 hello Azure IoT 套件的安全性功能和部署策略 tooensure 安全性、 隱私權和相容性難題的解決。 

## <a name="introduction"></a>簡介
hello 物聯網 (IoT) hello wave 的 hello 未來企業立即供應項目並真實世界的商機 tooreduce 成本、 增加營收，並轉換其商務。 許多企業來說，不過，會因為遲疑 toodeploy IoT 其組織中的有關安全性、 隱私權和相容性的到期 tooconcerns。 主要的考量點來自 hello IoT 基礎結構，其合併 hello e-security 和一起外衍生出其他個別風險這些兩個環境中的實體環境的 hello 唯一性。 IoT 的安全性相關的程式碼的裝置上執行、 提供裝置和使用者驗證、 定義明確的擁有權的裝置 （以及這些裝置所產生的資料），以及正在 tooensuring hello 完整性彈性 toocyber 和實體攻擊。 

接著，是 hello 隱私權問題。 公司希望資料收集過程透明化，例如，要收集哪些資料及原因、可查看資料的人員、可控制存取的人員等。 最後，有的 hello 設備 hello 人員操作，以及一般安全性問題和維護的相容性的業界標準的問題。

指定 hello 安全性、 隱私權、 透明度、 和相容性考量，選擇 hello 右 IoT 解決方案提供者會保留一項挑戰。 編結在一起時 IoT 軟體和服務提供的各種廠商供應的各個部分，導入了安全性、 隱私權、 透明度、 和相容性，這可能是硬式 toodetect，徒修正的間隙。 hello 選擇的 hello 右邊 IoT 軟體和服務提供者根據尋找提供者具有執行跨越縱向和地理位置，但也無法在安全和透明的方式 tooscale 之服務的豐富經驗。 同樣地，它有助於 hello 選取提供者 toohave 十年的經驗與開發安全數十億個全世界的電腦上執行的軟體和有 hello 能力 tooappreciate hello 威脅架構之下所造成的 hello 網際網路這個新世界的項目。

## <a name="secure-infrastructure-from-hello-ground-up"></a>從接地 hello 的安全基礎結構
hello [Microsoft 雲端](https://www.microsoft.com/enterprise/microsoftcloud/default.aspx#fbid=WzBsRQi6aGk)基礎結構支援多個 10 億個客戶 127 國家 （地區）。 繪製上建置企業軟體，並且在 hello world 中最大線上服務執行某些 hello 我們數十長時間的經驗，我們提供更高層級的增強式的安全性、 隱私權、 規範和威脅防護做法多數客戶可能比達到自己。

我們[安全性開發週期 (SDL)](https://www.microsoft.com/sdl/)提供必要的全公司的開發程序，嵌入到 hello 整個軟體生命週期的安全性需求。 toohelp 確定操作活動遵循 hello 相同的層級的安全性做法，我們使用嚴格的安全性指導方針，在我們的營運安全性保證 (OSA) 程序中配置。 我們也正在進行驗證，我們符合我們的相容性義務，並且我們可以參與透過 hello 的表現，包括 hello 數位犯罪單位 Microsoft、 Microsoft Security 中心建立廣泛的安全性工作的第三方稽核公司，以處理Response Center 和 Microsoft 惡意程式碼防護中心。

## <a name="microsoft-azure---secure-iot-infrastructure-for-your-business"></a>Microsoft Azure - 適用於貴公司的安全 IoT 基礎結構
Microsoft Azure 提供完整的雲端解決方案，結合不斷成長的整合式的雲端服務集合的其中一個 — 分析、 機器學習服務、 儲存體、 安全性、 網路及 web — 領先業界的承諾 toohello 保護與資料的隱私權。 我們[假設破壞](https://azure.microsoft.com/blog/red-teaming-using-cutting-edge-threat-simulation-to-harden-the-microsoft-enterprise-cloud/)策略是使用 「 紅色 」 組成的專門的小組的軟體安全性專家模擬攻擊中，測試 Azure toodetect hello 能力、 新興的威脅，保護及復原的漏洞。 我們[全域事件回應](https://www.microsoft.com/TrustCenter/Security/DesignOpSecurity)小組解決 hello 時鐘 toomitigate hello 效果的攻擊和惡意活動。 hello 小組遵循建立事件管理、 通訊，與復原的程序，並可探索和可預測的介面會使用內部及外部夥伴。

我們的系統會提供持續的入侵偵測與防護、阻斷服務攻擊防護、一般滲透測試，以及可協助識別及緩解威脅的法務工具。 [多因素驗證](../multi-factor-authentication/multi-factor-authentication.md)使用者 tooaccess hello 網路提供了額外的安全性。 並針對 hello 應用程式和 hello 主機提供者，提供存取控制、 監視、 反惡意程式碼、 的弱點可能會掃描、 套用修補程式，以及設定管理。

Microsoft Azure IoT 套件 hello 利用 hello 安全性和隱私權的內建於 hello Azure 平台，以及我們 SDL 和 OSA 程序進行安全的開發和作業的所有 Microsoft 軟體。 這些程序提供保護基礎結構、 網路保護及身分識別與管理功能基本 toohello 安全性的任何方案。 

hello [Azure IoT 中樞](../iot-hub/iot-hub-what-is-iot-hub.md)內 hello [IoT 套件](iot-suite-what-is-azure-iot.md)提供完全受管理的服務，可讓 Azure 服務，例如IoT裝置之間可靠且安全的雙向通訊[Azure Machine Learning](../machine-learning/machine-learning-what-is-machine-learning.md)和[Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md)使用每一裝置的安全性認證和存取控制。

toobest 通訊 hello Azure IoT 套件內建的安全性和隱私權功能，我們已細分成三個主要安全性區域 hello hello 套件。 

![Azure IoT 套件](media/securing-iot-ground-up/securing-iot-ground-up-fig3.png)

### <a name="secure-device-provisioning-and-authentication"></a>保護裝置佈建和驗證
hello Azure IoT 套件保護裝置，當它們 hello 欄位中提供每個裝置，可供 hello IoT 基礎結構 toocommunicate 與 hello 裝置在作業時唯一識別索引鍵。 hello 程序是快速和輕鬆 tooset 組成。 hello 與 hello 裝置與 hello Azure IoT 中樞之間的所有通訊中使用的語彙基元的使用者選取的裝置識別碼 form hello 基礎產生索引鍵。

裝置識別碼可以在製造期間 (例如硬體信任模組中的快閃記憶體) 與裝置產生關聯，或者可以使用現有的固定識別碼做為 Proxy (例如 CPU 序號)。 變更這個 hello 裝置中的識別資訊並不簡單，因為它是重要的 toointroduce 邏輯裝置識別碼，萬一 hello 基礎裝置的硬體變更，但會維持為邏輯裝置 hello hello 相同也一樣。 在某些情況下，裝置身分識別的 hello 關聯可以發生在 （也就是已驗證的欄位工程師實際設定新的裝置與 hello 方案後端通訊時發生） 的裝置部署時間。 hello [Azure IoT 中樞身分識別登錄](../iot-hub/iot-hub-devguide.md)提供安全地儲存裝置的身分識別與安全性金鑰的解決方案。 新增一或多個裝置身分識別 tooan 允許清單或封鎖清單，啟用裝置存取的完整控制權。

Azure IoT 中樞存取控制原則 hello 雲端中的啟用，啟用和停用任何裝置身分識別，提供方式 toodisassociate 從 IoT 部署時所需的裝置。 裝置的這個關聯和取消關聯是以每個裝置身分識別為根據。

其他裝置的安全性功能包括下列 hello:

* 裝置不會接受未經要求的網訊連接。 它們會以僅限輸出的方式建立所有連接和路由。 裝置 tooreceive hello 後端的命令，如 hello 裝置必須在初始連線 toocheck 的任何暫止命令 tooprocess。 一旦安全地建立 hello 裝置與 IoT 中樞之間的連線，從 hello 雲端 toohello 裝置和裝置 toohello 傳訊雲端可傳送以透明的方式。  
* 裝置只在連接 tooor 建立路由 toowell 已知服務與這些是否對等，例如 Azure IoT 中樞。
* 系統層級的授權和驗證會使用每一裝置的身分識別，讓存取認證和權限能近乎即時撤銷。

### <a name="secure-connectivity"></a>安全的連線
訊息傳遞的持久性是所有 IoT 解決方案的重要功能。 hello 需要 toodurably 傳遞命令及/或接收來自裝置的資料會加上底線 hello 事實 IoT 裝置所連線透過網際網路，hello 或其他類似的網路可能不可靠。 Azure IoT 中樞提供雲端與裝置的通知以回應 toomessages 系統之間的傳訊的持久性。 額外的耐久性，傳訊達成方式是在 hello IoT 中樞 tooseven 天遙測和兩天進行命令的快取訊息。

效率是重要的 tooensure 節省資源和資源限制的環境中的作業。 Azure IoT 中樞，啟用的通訊效率支援 HTTPS （HTTP 安全），hello 業界標準安全 hello 常用的 http 通訊協定版本。 Azure IoT 中樞支援的進階訊息佇列通訊協定 (AMQP) 和訊息佇列遙測傳輸 (MQTT)，不只是根據資源使用的效率而設計，同時也可進行可靠的訊息傳遞。 

延展性需要 hello 能力 toosecurely interoperate 與各種不同的裝置。 Azure IoT 中樞讓安全連線 tooboth IP 啟用，而且未啟用 IP 的裝置。 啟用 IP 的裝置都能 toodirectly 連接，並以透過安全連線的 hello IoT 中樞通訊。 未啟用 IP 的裝置是資源受限的，只能透過短距離通訊協定 (例如 Zwave、ZigBee 和藍芽) 來連接。 領域閘道使用的 tooaggregate 這些裝置，並執行通訊協定轉譯 tooenable 安全雙向通訊與 hello 雲端。

其他連接的安全性功能包括下列 hello:

* hello 裝置與 Azure IoT 中樞，或閘道及 Azure IoT 中樞，間的通訊路徑會保護使用業界標準傳輸層安全性 (TLS) 與使用 X.509 通訊協定來進行驗證的 Azure IoT 中樞。
* 從未經要求即傳入的連接順序 tooprotect 裝置，在 Azure IoT 中樞未開啟任何連接 toohello 裝置。 hello 裝置起始所有連線。 
* Azure IoT 中樞長期存放裝置的訊息，並等候 hello 裝置 tooconnect。 這些命令會儲存兩天內，讓裝置連線偶發性，toopower 或連線的考量，因為 tooreceive 這些命令。 Azure IoT 中樞會維護每個裝置的每一裝置佇列。

### <a name="secure-processing-and-storage-in-hello-cloud"></a>安全處理和 hello 雲端中的儲存體
從加密的通訊 tooprocessing hello 雲端中的資料，hello Azure IoT 套件可協助保護資料的安全。 它提供彈性 tooimplement 其他加密和管理的安全性金鑰。 使用 Azure Active Directory (AAD) 進行使用者驗證和授權，Azure IoT 套件可以提供以原則為基礎的授權模型 hello 雲端中的資料能夠讓您輕鬆存取的管理可以稽核和檢閱。 此模型也可讓幾近即時撤銷存取 toodata hello 雲端中與裝置連線 toohello Azure IoT 套件。

Hello 雲端中的資料之後，它可以處理及儲存任何使用者定義的工作流程中。 Hello 資料存取 tooeach 組件受到與 Azure Active Directory，視使用的 hello 儲存體服務而定。

因為金鑰可能需要重新佈建 toobe hello IoT 基礎結構所使用的所有索引鍵儲存在安全存放裝置，以透過 hello 能力 tooroll 中的 hello 雲端。 資料可以儲存在[Azure Cosmos DB](../documentdb/documentdb-introduction.md)或[SQL 資料庫](../sql-database/sql-database-faq.md)，啟用 hello 所需的安全性層級的定義。 此外，Azure 提供的方式 toomonitor 和稽核所有存取 tooyour 資料 tooalert 您的任何入侵或未經授權的存取。

## <a name="conclusion"></a>結論
hello 物聯網開頭為您的事情： hello 重要大部分 toobusinesses 的項目。 IoT 可以降低成本、 增加營收，並轉換商務提供令人讚嘆的值 tooa 商務。 此轉換成功主要是取決於選擇 hello 右 IoT 軟體和服務提供者。 這表示尋找提供者，其不僅可藉由了解企業需要與需求來催化這個轉型，也會提供使用安全性、隱私權、透明度及相容性建置的服務和軟體做為主要設計考量。 Microsoft 已開發和部署安全的軟體和服務的豐富經驗，並向 toobe 領導者繼續的物聯網這個新的存留期。 

根據設計，啟用安全資產 tooimprove 效率、 磁碟機操作效能 tooenable 創新，監視 Microsoft Azure IoT 套件 hello 建置安全性量值中，並且採用進階的資料分析 tootransform 企業。 其朝向安全性、 多個安全性功能，以及設計模式的分層方式，使用 Azure IoT 套件可協助部署基礎結構可以是受信任的 tootransform 任何企業。 

## <a name="additional-information"></a>其他資訊
每個 Azure IoT 套件預先設定的方案建立 Azure 服務，例如 hello 下列執行的個體：

* [**Azure IoT 中樞**](https://azure.microsoft.com/services/iot-hub/)： 您的閘道連接 hello 雲端太 「 動作 」。 您可以調整每個中樞和處理大量資料磁碟區的連線 toomillions 與每一裝置的驗證支援，協助您保護您的方案。
* [**Azure Cosmos DB**](https://azure.microsoft.com/services/documentdb/)： 管理裝置 hello 的中繼資料的半結構化資料的可擴充、 完全編製索引的資料庫服務您佈建，例如屬性、 組態和安全性內容。 Cosmos DB 提供高效能且高輸送量的處理、無從驗證結構描述的資料索引編製，以及豐富的 SQL 查詢介面。
* [**Azure Stream Analytics**](https://azure.microsoft.com/services/stream-analytics/)： 即時資料流處理，可讓您 toorapidly hello 雲端中開發和部署低成本分析方案 toouncover 即時深入資訊從裝置、 感應器、 基礎結構，並應用程式。 從此完全受管理服務的 hello 資料可以調整 tooany 磁碟區，但仍然達到高輸送量、 低延遲、 和恢復功能。
* [**Azure 應用程式服務**](https://azure.microsoft.com/services/app-service/)： 雲端平台 toobuild 強大 web 和行動裝置應用程式連接的任何位置; toodata hello 雲端或內部部署中。 建置吸引客戶參與的 iOS、Android 和 Windows 版行動應用程式。 整合您的軟體為服務 (SaaS) 和企業應用程式的全新連線 toodozens 的雲端服務和企業應用程式。 您最愛的語言和 IDE 中的程式碼 —.NET、 Node.js、 PHP、 Python 或 Java — toobuild 的 web 應用程式和應用程式開發介面比以往更快。
* [**邏輯應用程式**](https://azure.microsoft.com/services/app-service/logic/): hello Logic Apps 功能的 Azure 應用程式服務可協助整合 IoT 解決方案 tooyour 現有的業務系統和自動化工作流程處理序。 邏輯應用程式可讓開發人員 toodesign 工作流程的觸發程序從開始，然後再執行一系列的步驟-規則和使用功能強大的連接器 toointegrate 與您的商務程序的動作。 邏輯應用程式提供的方塊外連線 tooa vast 的生態系統 SaaS，雲端為基礎，並在內部部署應用程式。
* [**Azure blob 儲存體**](https://azure.microsoft.com/services/storage/)： 您的裝置傳送 toohello 雲端的 hello 資料的可靠且經濟的雲端儲存體。

## <a name="next-steps"></a>後續步驟
toolearn 有關保護您的 IoT 解決方案的詳細資訊，請參閱：

* [IoT 安全性最佳做法][lnk-security-best-practices]
* [IoT 安全性架構][lnk-security-architecture]
* [保護您的 IoT 部署][lnk-security-deployment]

[lnk-security-best-practices]: iot-security-best-practices.md
[lnk-security-architecture]: iot-security-architecture.md
[lnk-security-deployment]: iot-suite-security-deployment.md

您也可以探索 hello 的某些其他特性和功能 hello IoT 套件預先設定的解決方案：

* [預先設定的預防性維護解決方案概觀][lnk-predictive-overview]
* [IoT 套件的常見問題集][lnk-faq]

您可以閱讀 IoT 中樞中的安全性[控制存取 tooIoT 中樞][ lnk-devguide-security] hello IoT 中樞開發人員指南 》 中。

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md
