---
title: "aaaAzure 服務網狀架構安全性概觀 |Microsoft 文件"
description: "本文章提供 hello Azure service fabric 安全性的概觀。"
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: ec5355983c5d59f4e0c3b855965f03ac47f1a4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-overview"></a>Azure Service Fabric 安全性概觀
[Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview)是分散式的系統平台，可讓您輕鬆 toopackage，部署及管理可擴充且可靠的微服務。 Service Fabric 處理 hello 在開發和管理雲端應用程式的重大挑戰。 開發人員與管理員能夠避免複雜的基礎結構問題，專注於實作關鍵且嚴格要求之可調整、可信賴且可管理的工作負載。

Azure Service Fabric 安全性概觀本文著重於 hello 下列區域：

-   保護您的叢集
-   監視和診斷
-   使用憑證提供保護
-   角色型存取控制 (RBAC)
-   使用 Windows 安全性保護叢集
-   在 Service Fabric 中設定應用程式安全性
-   保護 Azure Service Fabric 安全性中服務的通訊安全

## <a name="securing-your-cluster"></a>保護您的叢集
Azure Service Fabric 是 orchestrator 服務的跨叢集的電腦，叢集必須是安全的 tooprevent 未經授權的使用者連接 tooyour 叢集，尤其是當它已在其上執行的實際執行工作負載。 雖然可能 toocreate 不安全的叢集，這樣做可讓匿名使用者 tooconnect tooit，如果它會公開管理端點 toohello 公用網際網路。

本節概略說明 hello 安全性案例的叢集在 Azure 或獨立執行，並 hello 各種所用技術 tooimplement 這些案例。 hello 叢集安全性案例包括：

-   節點對節點安全性
-   用戶端對節點安全性

### <a name="node-to-node-security"></a>節點對節點安全性
保護 hello Vm 或 hello 叢集中的機器之間的通訊。 這可確保只有授權的 toojoin hello 叢集的電腦可以參與裝載應用程式和服務 hello 叢集中。

在 Azure 上執行的叢集或在 Windows 上執行的獨立叢集可以使用[憑證安全性](https://msdn.microsoft.com/library/ff649801.aspx)或針對 Windows Server 機器使用 [Windows 安全性](https://msdn.microsoft.com/library/ff649396.aspx)。

**節點對節點憑證安全性**

服務網狀架構會使用 X.509 伺服器憑證，當您建立叢集時，您指定為 hello 節點型別組態的一部分。 若要快速了解這些憑證是什麼，以及如何取得或建立這些憑證，請參閱[這篇文章](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/working-with-certificates)。

憑證的安全性設定時建立 hello 叢集透過 hello Azure 入口網站、 Azure Resource Manager 範本或獨立 JSON 範本。 您可以指定用於憑證變換的主要憑證和選用次要憑證。 hello 您指定的主要和次要憑證應不同於 hello 管理用戶端以及您針對指定的唯讀用戶端憑證[用戶端對節點安全性](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security)。

### <a name="client-to-node-security"></a>用戶端對節點安全性
使用用戶端身分識別來設定用戶端 toonode 安全性。 tooestablish 之間的信任的用戶端與 hello 叢集中，您必須設定 hello 叢集 tooknow 可以信任哪些用戶端身分識別。 這有兩種不同的方式可以完成：

-   指定可以連接的 hello 網域群組使用者或
-   指定可以連接的 hello 網域節點使用者。

Service Fabric 支援兩種不同的存取控制類型的用戶端的連線的 tooa Service Fabric 叢集：

-   系統管理員
-   User

存取控制提供 hello hello 能力叢集系統管理員 toolimit 存取 toocertain 類型的使用者，使 hello 叢集更安全的不同群組的叢集操作。 系統管理員具有完整存取 toomanagement 功能 （包括讀取/寫入功能）。 使用者，根據預設，具有讀取權限 toomanagement 功能 （例如，查詢功能） 和 hello 能力 tooresolve 應用程式和服務。

**用戶端對節點憑證安全性**

用戶端對節點憑證的安全性設定時建立 hello 叢集透過 hello Azure 入口網站中，資源管理員範本或藉由指定的系統管理員用戶端憑證及/或使用者的用戶端憑證的獨立 JSON 範本。 hello 管理用戶端和使用者用戶端憑證指定應該不同於您指定的節點到節點安全性 hello 主要和次要憑證。

連接 toohello 叢集使用 hello 管理憑證的用戶端具有完整存取 toomanagement 功能。 連接 toohello 叢集使用 hello 唯讀使用者用戶端憑證的用戶端擁有讀取權限 toomanagement 功能。 在 word 中，這些憑證用於 hello 角色為基礎的存取控制 (RBAC)。

讀取 Azure[設定叢集，利用 Azure 資源管理員範本](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm)toolearn tooconfigure 憑證安全性在叢集中的方式。

**Azure 上的用戶端對節點 Azure Active Directory (AAD) 安全性**

在 Azure 上執行的叢集也可以保護存取使用 Azure Active Directory (AAD) toohello 管理端點。 請參閱[設定叢集，利用 Azure 資源管理員範本](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm)如需如何 toocreate hello 需要 AAD 成品時，如何 toopopulate 期間叢集建立和 tooconnect toothose 之後叢集的方式。

AAD 讓組織 （又稱為租用戶） toomanage 使用者存取 tooapplications，它們分成網頁型登入 UI 的應用程式和原生用戶端體驗的應用程式。

Service Fabric 叢集提供數個進入點 tooits 的管理功能，包括 hello web Service Fabric Explorer 和 Visual Studio。 如此一來，您會建立兩個 AAD 應用程式 toocontrol 存取 toohello 叢集、 一個 web 應用程式和一個原生應用程式。
Azure 的叢集，建議您使用用戶端的安全性 tooauthenticate AAD 和憑證節點對節點的安全性。

對於獨立 Windows Server 叢集，如果您有 Windows Server 2012 R2 和 Active Directory，建議您使用 Windows 安全性與群組管理帳戶 (GMA)。 否則仍然使用 Windows 安全性與 Windows 帳戶。

## <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>對 Azure Service Fabric 進行監視和診斷
[監視和診斷](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-overview)是重大 toodeveloping 測試和任何環境中部署應用程式和服務。 如果您要規劃和實作監視和診斷功能，以協助確保應用程式和服務可在本機開發環境或生產環境中如預期般運作，Service Fabric 解決方案就是理想之選。

從安全性觀點來看，hello 主要目標的監視和診斷要：

-   偵測及診斷可能是由於在 tooa 安全性事件的硬體和基礎結構問題。
-   偵測可能提供入侵指標 (Indicator of Compromise，IoC) 的軟體和應用程式問題。
-   了解資源耗用量 toohelp 避免不小心阻絕服務。

hello 整體的工作流程的監視和診斷包含三個步驟：

-   **事件產生：**這包括在 hello 基礎結構 （叢集） 和應用程式 / 服務層級的事件記錄檔、 追蹤 （自訂的事件）。 深入了解[基礎結構層級事件](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-infra)和[應用程式層級事件](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-app)toounderstand 所提供內容和 tooadd 如何進一步檢測。
-   **事件彙總：**產生的事件需要 toobe 收集並彙總，然後才能顯示。 我們通常建議使用[Azure 診斷](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-wad)（比較類似 tooagent 為基礎的記錄檔集合） 或[EventFlow](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow) （同處理序記錄檔集合）。
-   **分析：**事件需要 toobe 視覺化且可存取某些格式、 tooallow 分析及顯示所需。 有數個很好的平台 toohello 分析和視覺效果的監視和診斷資料時存在於 hello 市場。 hello 建議的兩個是[OMS](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-oms)和[Application Insights](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-appinsights)到期 tootheir 更佳的整合服務的網狀架構。

您也可以使用[Azure 監視器](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)toomonitor 許多 hello Azure Service Fabric 叢集建立所在的資源。

監視是不同的服務可以觀賞健全狀況和 hello 健康情況模型階層中的任何項目載入跨服務和報表的健全狀況。 這可協助防止將不會偵測根據 hello 檢視的單一服務的錯誤。 Watchdogs 也是很好的起點 toohost 程式碼執行修復動作，而不需使用者互動 （例如，在特定時間間隔內清除記錄檔儲存體中）。 您可以在[這裡](https://azure.microsoft.com/resources/samples/service-fabric-watchdog-service/)找到範例監視程式服務實作。

## <a name="secure-using-certificates"></a>使用憑證提供保護
它使用的憑證，會告訴如何 toosecure hello 溝通 hello 獨立 Windows 叢集的不同節點，以及如何 tooauthenticate 連接的用戶端 toothis 叢集會使用 X.509 憑證。 這樣可以確保，只有授權的使用者可以存取 hello 叢集 hello 部署之應用程式執行管理工作。 建立 hello 叢集時，應該 hello 叢集上啟用憑證安全性。

### <a name="x509-certificates-and-service-fabric"></a>X.509 憑證和 Service Fabric
X.509 數位憑證是常用的 tooauthenticate 用戶端和伺服器與 tooencrypt 以及數位簽署訊息。

hello 下表列出您必須在叢集設定的 hello 憑證：

|憑證資訊設定 |說明|
|-------------------------------|-----------|
|ClusterCertificate|    此憑證是在叢集上的 hello 節點之間需要的 toosecure hello 通訊。 您可以使用兩個不同的憑證 (主要和次要) 進行更新。|
|ServerCertificate| 當它嘗試 tooconnect toothis 叢集時，此憑證會呈現 toohello 用戶端。 您可以使用兩個不同的伺服器憑證 (主要和次要) 進行更新。|
|ClientCertificateThumbprints|  這是一組您想 tooinstall hello 驗證用戶端上的憑證。|
|ClientCertificateCommonNames|  設定 hello 的一般名稱的第一個用戶端憑證 hello hello CertificateCommonName。 hello CertificateIssuerThumbprint 是 hello hello 簽發者，此憑證的指紋。|
|ReverseProxyCertificate|   這是選擇性的憑證，可以指定是否要讓 toosecure 您[反向 Proxy](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy)。|

如需保護憑證的詳細資訊，[請按一下這裡](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security)。

## <a name="role-based-access-control-rbac"></a>角色型存取控制 (RBAC)
存取控制可讓 hello 叢集系統管理員 toolimit 存取 toocertain 叢集作業會針對不同使用者群組，讓 hello 叢集更安全。 兩個不同的存取控制項類型支援連接 tooa 叢集的用戶端： 系統管理員角色和使用者角色。

系統管理員具有完整存取 toomanagement 功能 （包括讀取/寫入功能）。 使用者，根據預設，具有讀取權限 toomanagement 功能 （例如，查詢功能） 和 hello 能力 tooresolve 應用程式和服務。

您指定 hello 系統管理員和使用者用戶端角色 hello 叢集建立時提供不同的身分識別 （憑證，AAD 等） 針對每個。 如需有關 hello 預設存取控制設定，以及如何 toochange hello 預設設定的詳細資訊，請參閱[角色型存取控制服務網狀架構用戶端](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles)。

## <a name="secure-standalone-cluster-using-windows-security"></a>使用 Windows 安全性保護獨立叢集
tooprevent 未經授權存取 tooa Service Fabric 叢集，您必須保護 hello 叢集。 Hello 叢集中執行生產工作負載時，安全性是特別重要。 本主題描述如何使用 Windows 安全性的 tooconfigure 節點對節點和用戶端對節點安全性 hello 追蹤檔案。

**使用 gMSA 設定 Windows 安全性**

藉由設定已設定的節點 toonode 安全性[ClustergMSAIdentity](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-windows-security)當 service fabric 需要 toorun 下 gMSA。 在訂單 toobuild 節點之間的信任關係，他們必須撰寫知道彼此的存在。

使用 ClientIdentities 設定用戶端 toonode 安全性。 在用戶端與 hello 叢集之間的順序 tooestablish 信任，您必須設定 hello 叢集 tooknow 可以信任哪些用戶端身分識別。

**使用電腦群組設定 Windows 安全性**

使用 ClusterIdentity，如果您想 toouse 機器群組在 Active Directory 網域內的設定會設定節點 toonode 安全性。 如需詳細資訊，請參閱[在 Active Directory 中建立電腦群組 (Create a Machine Group in Active Directory)](https://msdn.microsoft.com/library/aa545347)。

用戶端對節點安全性是使用 ClientIdentities 來設定的。 tooestablish 之間的信任的用戶端與 hello 叢集中，您必須設定 hello 叢集 tooknow hello 用戶端 hello 叢集的身分識別可以信任。 您可以透過兩種不同方式建立信任︰

-   指定可以連接的 hello 網域群組使用者。
-   指定可以連接的 hello 網域節點使用者。

## <a name="configure-application-security-in-service-fabric"></a>在 Service Fabric 中設定應用程式安全性
### <a name="managing-secrets-in-service-fabric-applications"></a>管理 Service Fabric 應用程式中的密碼
此方法可協助管理 Service Fabric 應用程式中的密碼。 密碼可以是任何機密資訊，例如儲存體連接字串、密碼或其他不會以純文字處理的值。

這種方法使用[Azure 金鑰保存庫](https://docs.microsoft.com/azure/key-vault/key-vault-whatis)toomanage 金鑰和密碼。 不過，應用程式中使用的密碼是雲端 tooallow 無從驗證平台應用程式部署的 toobe tooa 叢集裝載的任何位置。 此流程有四個主要步驟︰

-   取得資料編密憑證。
-   在您的叢集安裝 hello 憑證。
-   時部署應用程式與 hello 憑證加密密碼的值，並將它們插入服務 Settings.xml 組態檔。
-   讀取加密值超出 Settings.xml 解密與 hello 相同的加密憑證。

>[!Note]
>深入了解[管理 Service Fabric 應用程式中的密碼](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management)。

### <a name="configure-security-policies-for-your-application"></a>設定應用程式的安全性原則
使用 Azure Service Fabric 安全性，您可以協助安全 hello 叢集中不同的使用者帳戶下執行的應用程式。 服務網狀架構安全性也有助於安全 hello 資源所使用的應用程式中的 hello 使用者帳戶-部署的 hello 時段，例如、 檔案、 目錄和憑證。 如此一來，即使在共用主控環境中，執行中的應用程式就不會彼此干擾。
hello 步驟包括：

-   設定服務安裝程式的進入點的 hello 原則。
-   從安裝程式進入點啟動 PowerShell 命令。
-   使用主控台重新導向進行本機偵錯。
-   設定服務程式碼封裝的原則。
-   為 HTTP 和 HTTPS 端點指派安全性存取原則。

## <a name="secure-communication-for-services-in-azure-service-fabric-security"></a>保護 Azure Service Fabric 安全性中服務的通訊安全
安全性是 hello 通訊的最重要的層面的其中一個。 hello 可靠的服務應用程式架構會提供數的預先建立的通訊堆疊，可以使用的 tooimprove 安全性的工具。

-   [協助保護使用服務遠端處理時的服務安全](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication)。
-   [協助保護使用 WCF 通訊堆疊時的服務安全](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication#help-secure-a-service-when-youre-using-a-wcf-based-communication-stack)。

## <a name="next-steps"></a>後續步驟
- 如需叢集安全性的概念資訊，請參閱[使用 Resource Manager 範本在 Azure 中建立叢集](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm)和 [Azure 入口網站](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal)。
- 如需詳細資訊，請參閱 [Service Fabric 叢集安全性](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security)。
