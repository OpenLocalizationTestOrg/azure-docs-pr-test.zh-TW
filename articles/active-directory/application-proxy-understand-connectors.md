---
title: "aaaUnderstand Azure AD 應用程式 Proxy 連接器 |Microsoft 文件"
description: "涵蓋有關 Azure AD 應用程式 Proxy 連接器 hello 基本概念。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 294cb26803ef7cf8be9f3af0678d6d2e64f6cc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-ad-application-proxy-connectors"></a>了解 Azure AD 應用程式 Proxy 連接器

連接器是讓 Azure AD 應用程式 Proxy 運作的關鍵。 它們是簡單且容易 toodeploy 和維護和進階功能強大。 本文將告訴您哪些連接器，其運作方式以及一些建議 toooptimize 您的部署。 

## <a name="what-is-an-application-proxy-connector"></a>什麼是應用程式 Proxy 連接器

連接器是坐在內部部署，並促進 hello 輸出連線 toohello 應用程式 Proxy 服務的輕量級代理程式。 必須有存取 toohello 後端應用程式的 Windows 伺服器上安裝連接器。 您可以將連接器組織成與處理流量 toospecific 應用程式的每個群組的連接器群組。 連接器的負載平衡，並可協助您的網路結構 toooptimize。 

## <a name="requirements-and-deployment"></a>需求和部署

toodeploy 應用程式 Proxy 成功，您必須至少一個連接器，但我們建議下列兩個或多個大於提供恢復功能。 Windows Server 2012 R2 或 2016年的機器上安裝 hello 連接器。 hello 連接器需要 toobe 無法 toocommunicate hello 應用程式 Proxy 服務以及您所發行的 hello 在內部部署應用程式。 

如需 hello hello 連接器伺服器的網路需求的詳細資訊，請參閱[開始使用應用程式 Proxy 並安裝連接器](active-directory-application-proxy-enable.md)。

## <a name="maintenance"></a>維護 
hello 連接器與 hello 服務處理的所有 hello 高可用性工作。 它們可以動態新增或移除。 新要求到達每次它會路由的 tooone hello 連接器的目前可用。 如果連接器暫時無法使用，它不會回應 toothis 流量。

hello 連接器是無狀態，與 hello 電腦上有任何組態資料。 hello 他們儲存的資料是 hello 設定連接 hello 服務和其驗證憑證。 當他們連線 toohello 服務時，它們會提取 hello 所需的所有設定資料，而且每隔幾分鐘的時間重新整理。

連接器也輪詢是否 hello 伺服器 toofind hello 連接器較新版本。 如果找到，hello 連接器自行更新。

您可以監視您的連接器，從 hello 機器，執行使用 hello 事件記錄檔和效能計數器。 或者，您可以檢視其狀態從 hello 應用程式 Proxy hello Azure 入口網站頁面：

 ![Azure AD 應用程式 Proxy 連接器](./media/application-proxy-understand-connectors/app-proxy-connectors.png)

您不需要 toomanually 刪除未使用的連接器。 當執行連接器時，它會保持有效在連接 toohello 服務。 未使用的連接器會標記為_非作用中_，且將在未作用 10 天之後移除。 如果您想 toouninstall 連接器，不過，hello 連接器服務和 hello Updater 服務從伺服器解除安裝 hello。 重新啟動電腦 toofully 移除 hello 服務。

## <a name="automatic-updates"></a>自動更新

Azure AD 提供的所有部署的 hello 連接器的自動更新。 只要 hello 應用程式 Proxy 連接器更新程式服務正在執行，會自動更新的連接器。 如果您沒有看到 hello 連接器更新程式服務在您的伺服器上，您需要[重新安裝您的連接器](active-directory-application-proxy-enable.md)tooget 任何更新。 

如果您不想 toowait 自動更新 toocome tooyour 連接器，您可以執行手動升級。 移 toohello[連接器的下載頁面](https://download.msappproxy.net/subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/connector/download)hello 伺服器上，您的連接器並選取**下載**。 此程序就會啟動 hello 本機連接器的升級。 

為租用戶與多個連接器 hello 自動更新目標一個連接器，在您的環境中的每個群組 tooprevent 停機時間的時間。 

如果是下列情況，連接器更新時可能會遭遇停機︰  
- 您只有一個連接器。 tooavoid 這個停機時間並提升高可用性，建議您安裝第二個連接器和[建立連接器群組](active-directory-application-proxy-connectors-azure-portal.md)。  
- 連接器已交易的 hello 中間 hello 更新開始時。 雖然遺失 hello 起始交易，則您的瀏覽器自動重試 hello 作業，或您可以重新整理您的頁面。 重新傳送嗨要求，hello 流量時，路由的 tooa 備份連接器。

## <a name="creating-connector-groups"></a>建立連接器群組

連接器群組可讓您 tooassign 特定連接器 tooserve 特定應用程式。 您可以的連接器的數字群組在一起，並接著每個應用程式 tooa 將群組指派。 

連接器群組可讓您更輕鬆 toomanage 大型部署。 它們也會改善延遲租用戶的應用程式裝載在不同的區域，因為您可以建立以位置為基礎的連接器群組 tooserve 只有本機應用程式。 

toolearn 進一步了解連接器群組，請參閱[發行應用程式在不同的網路和使用連接器群組的位置](active-directory-application-proxy-connectors-azure-portal.md)。

## <a name="security-and-networking"></a>安全性和網路服務

連接器可以安裝在外面 toosend 要求 toohello 應用程式 Proxy 服務的 hello 網路上的任何位置。 重要的是該 hello 執行電腦 hello 連接器也有存取 tooyour 應用程式。 您可以在您的公司網路內或在 hello 雲端執行的虛擬機器上安裝連接器。 可以在非軍事區域 (DMZ) 內執行連接器，但並非必要，因為所有流量都是輸出的，因此您的網路都能保持安全。

連接器僅會傳送輸出要求。 hello 傳出流量會傳送 toohello 應用程式 Proxy 服務和 toohello 發行的應用程式。 您不需要 tooopen 輸入連接埠，因為流量流這兩種方式，一旦建立工作階段為止。 您尚未 tooset 之間 hello 連接器的負載平衡設定，或透過您的防火牆設定的傳入的存取。 

如需設定輸出防火牆規則的詳細資訊，請參閱[使用現有的內部部署 Proxy 伺服器](application-proxy-working-with-proxy-servers.md)。

使用 hello [Azure AD 應用程式 Proxy 連接器連接埠測試工具](https://aadap-portcheck.connectorporttest.msappproxy.net/)tooverify 連接器可達到 hello 應用程式 Proxy 服務。 最少，請確定 hello 美國中部地區和 hello 區域最接近 tooyou 具有所有綠色的核取記號。 除此之外，綠色勾選記號越多代表恢復能力越佳。 

## <a name="performance-and-scalability"></a>效能和延展性

Hello 應用程式 Proxy 服務的小數位數是透明的但小數位數是連接器的因素。 您需要 toohave 足夠連接器 toohandle 尖峰流量。 不過，您不需要 tooconfigure 負載平衡，因為連接器群組內的所有連接器自動都負載平衡。

接點是無狀態，因為它們不會影響的使用者或工作階段的 hello 數目。 相反地，其會回應 toohello 要求數目以及其裝載大小。 以標準 Web 流量而言，一台普通電腦每秒可以處理幾千個要求。 hello 特定容量取決於 hello 確切的電腦的特性。 

hello 連接器效能受限於 CPU 和網路功能。 CPU 效能需要 SSL 加密和解密，但網路是重要的 tooget 快速連線 toohello 應用程式，在 Azure 中的 hello 線上服務。

相反地，連接器發行需要較少的記憶體。 hello 線上服務會處理大部分的 hello 處理和所有未經驗證的流量。 因應 hello 雲端中的所有項目是完成 hello 雲端中。 

會影響效能的另一個因素是 hello 品質 hello 網路之間 hello 連接器，包括： 

* **hello 線上服務**： 緩慢或高延遲連線 toohello Azure 影響 hello 連接器效能的應用程式 Proxy 服務。 Hello 獲得最佳效能，請使用 Express Route 連接組織 tooAzure。 否則，必須確定該連接 tooAzure 會盡可能有效率地處理網路團隊。 
* **hello 後端應用程式**： 在某些情況下，有其他 hello 連接器與 hello 後端應用程式可能變慢或無法連線之間的 proxy。 tootroubleshoot 此案例中，開啟瀏覽器從 hello 連接器伺服器，然後再次嘗試 tooaccess hello 應用程式。 如果您在 Azure 中執行 hello 連接器，但 hello 應用程式會在內部部署，hello 體驗可能會使用者的預期。
* **hello 網域控制站**: hello 連接器上執行 SSO 使用 Kerberos 限制委派，如果他們傳送嗨要求 toohello 後端之前，先連絡 hello 網域控制站。 hello 連接器具有的 Kerberos 票證快取，但在忙碌的環境中 hello 回應 hello 網域控制站可能會影響效能。 在 Azure 中執行、但與內部部署之網域控制器通訊的連接器會更常發生這個問題。 

如需將您網路最佳化的詳細資訊，請參閱[使用 Azure Active Directory 應用程式 Proxy 時的網路拓撲考量](application-proxy-network-topology-considerations.md)。

## <a name="domain-joining"></a>加入網域

連接器可以在未加入網域的電腦上執行。 不過，如果您想單一登入 (SSO) tooapplications 使用整合式 Windows 驗證 (IWA)，您需要加入網域的電腦。 在此情況下，hello 連接器的電腦必須可以執行的聯結的 tooa 網域[Kerberos](https://web.mit.edu/kerberos)限制委派，代表 hello 的 hello 使用者發行的應用程式。

連接器也可以聯結的 toodomains 或有部分信任中或僅限 tooread 網域控制站的樹系。

## <a name="connector-deployments-on-hardened-environments"></a>強化環境上的連接器部署

連接器部署通常都直截了當，不需要特殊組態。 不過，應該考量一些獨特的情況︰

* 限制 hello 輸出流量的組織必須[開啟必要的連接埠](active-directory-application-proxy-enable.md#open-your-ports)。
* 與 FIPS 相容的電腦可能會需要的 toochange 其組態 tooallow hello 連接器處理程序 toogenerate 並儲存憑證。
* 網路要求該問題 hello 鎖定其環境 hello 程序為基礎的組織有 toomake 確定這兩個連接器服務已啟用的 tooaccess 所有所需的連接埠和 Ip。
* 在某些情況下，輸出的正向 proxy 可能會中斷 hello 雙向的憑證驗證，並導致 hello 通訊 toofail。

## <a name="connector-authentication"></a>連接器驗證

tooprovide 安全的服務，連接器 tooauthenticate 朝 hello 服務，且 hello 服務具有 tooauthenticate 朝 hello 連接器。 進行此驗證 hello 連接器起始 hello 連線時，使用用戶端和伺服器憑證。 此方式 hello 系統管理員的使用者名稱和密碼不會儲存在 hello 連接器電腦上。

使用 hello 憑證是特定 toohello 應用程式 Proxy 服務。 建立 hello 初始註冊期間便會自動更新 hello 連接器每隔幾個月。 

如果未連接連接器 toohello 幾個月，其憑證的服務可能已過時。 在此情況下，解除安裝再重新安裝 hello 連接器 tootrigger 註冊。 您可以執行下列 PowerShell 命令的 hello:

```
Import-module AppProxyPSModule
Register-AppProxyConnector
```

## <a name="under-hello-hood"></a>Hello 幕後

連接器根據 Windows Server Web 應用程式 Proxy，因此大部分的 hello 相同的管理工具，包括 Windows 事件記錄檔

 ![管理事件記錄檔以 hello 事件檢視器](./media/application-proxy-understand-connectors/event-view-window.png)

和 Windows 效能計數器管理事件記錄。 

 ![加入以 hello 效能監視器計數器 toohello 連接器](./media/application-proxy-understand-connectors/performance-monitor.png)

hello 連接器有系統管理員和工作階段記錄檔。 hello 系統管理記錄檔包含索引鍵的事件和其錯誤。 hello 工作階段記錄檔包含所有的 hello 交易，而且其處理詳細資料。 

toosee hello 記錄，到 toohello 事件檢視器中，開啟 hello**檢視**功能表上，並啟用**顯示分析與偵錯記錄檔**。 然後，讓他們 toostart 收集事件。 這些記錄不會出現在 Windows Server 2012 R2 中的 Web 應用程式 Proxy hello 連接器會根據較新版本。

您可以檢查 hello hello 服務 視窗中的 hello 服務狀態。 hello 連接器包含兩個 Windows 服務： hello 實際的連接器，以及 hello 更新程式。 兩者都必須執行所有的 hello 時間。

 ![AzureAD 服務本機](./media/application-proxy-understand-connectors/aad-connector-services.png)

## <a name="next-steps"></a>後續步驟


* [使用連接器群組在個別的網路和位置上發佈應用程式](active-directory-application-proxy-connectors-azure-portal.md)
* [使用現有的內部部署 Proxy 伺服器](application-proxy-working-with-proxy-servers.md)
* [針對應用程式 Proxy 和連接器錯誤進行疑難排解](active-directory-application-proxy-troubleshoot.md)
* [Toosilently hello Azure AD 應用程式 Proxy 連接器的安裝方式](active-directory-application-proxy-silent-installation.md)

