---
title: "aaaAzure Service Fabric 安全性最佳作法 |Microsoft 文件"
description: "本文提供一組 Azure Service Fabric 安全性的最佳做法。"
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
ms.openlocfilehash: 483a21240da17d56bb4641653093ddcbad379d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-best-practices"></a>Azure Service Fabric 安全性最佳做法
在 Azure 上部署應用程式很快速、輕鬆且符合成本效益。 部署雲端應用程式中實際的有用 toohave 之前的最佳做法 tooassist 評估您的應用程式針對清單重要和建議的最佳作法。

Azure Service Fabric 是分散式的系統平台，可讓您輕鬆 toopackage、 部署及管理可擴充且可靠的 microservices。 服務網狀架構也會討論 hello 在開發和管理雲端應用程式的重大挑戰。 開發人員與管理員能夠避免複雜的基礎結構問題，專注於實作關鍵且嚴格要求之可調整、可信賴且可管理的工作負載。 

針對每個最佳做法，我們會說明︰

-   哪些 hello 最佳作法是
-   為什麼要 tooenable 該最佳作法
-   如果您無法 tooenable hello 最佳作法，可能 hello 結果
-   如何了解 tooenable hello 最佳作法

我們目前已有下列安全性最佳作法時，Azure Service Fabric hello:

-   使用 Azure 資源 Manager(ARM) 範本和服務網狀架構 Azure PowerShell 模組 toocreate 安全叢集
-   使用 X.509 憑證
-   設定安全性原則
-   Reliable Actors 安全性設定
-   設定 Azure Service Fabric 的 SSL
-   Azure Service Fabric 的網路隔離/安全性
-   設定金鑰保存庫以提供安全性
-   指派使用者 tooroles


## <a name="best-practices-for-securing-your-cluster"></a>保護叢集的最佳做法

**概觀**

一律使用安全的叢集
-   叢集安全性 - 使用憑證
-   用戶端存取 (系統管理員和唯讀) - 使用 AAD

使用自動化部署
-   使用指令碼 toogenerate、 部署和彙總機密資料
-   Hello 密碼 KV，為所有其他用戶端存取使用 AD
-   任何人應該不具有存取 toothem 未經驗證。

此外，請考慮下列 hello:
-   使用網路安全性群組 (NSG) 建立 DMZ
-   您的叢集使用叢集 Vm 或 toomanage 跳躍伺服器 tooRDP

叢集必須是安全的 tooprevent 未經授權的使用者連接 tooyour 叢集，尤其是當它已在其上執行的實際執行工作負載。 雖然可能 toocreate 不安全的叢集，這樣做可讓匿名使用者 tooconnect tooit，如果它會公開管理端點 toohello 公用網際網路。

技術用 tooimplement 這些案例。 hello[叢集安全性案例](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security)是：

-   節點-安全性-本保護 hello Vm 與 hello 叢集中的電腦之間的通訊。 這可確保只有授權的 toojoin hello 叢集的電腦可以參與裝載應用程式和服務 hello 叢集中。
在 Azure 上執行的叢集或在 Windows 上執行的獨立叢集可以使用[憑證安全性](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security)或針對 Windows Server 機器使用 [Windows 安全性](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-windows-security)。
-   用戶端對節點安全性-本保護 Service Fabric 用戶端與 hello 叢集中的個別節點之間的通訊。
-   角色型存取控制 (RBAC)-您指定 hello 系統管理員和使用者用戶端角色的叢集建立 hello 次藉由提供不同的身分識別 （憑證，AAD 等） 針對每個。
-   安全性建議-Azure 適用的叢集，我們建議您為節點對節點安全性使用用戶端的安全性 tooauthenticate AAD 和憑證。

tooconfigure hello 獨立 Windows 叢集，請參閱[獨立 windows 叢集進行設定](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest)。

使用 Azure Resource Manager 範本和服務網狀架構 Azure PowerShell 模組 toocreate 安全叢集。
[此處](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm)提供的逐步指南可逐步引導您使用 Azure Resource Manager 在 Azure 中設定安全的 Azure Service Fabric 叢集。

使用您的叢集 hello Azure Resource Manager 範本 toocustomize
-   設定 VM VHD 的受管理儲存體

使用 hello Azure Resource Manager 範本 toodrive 變更 tooyour 資源群組
-   輕鬆進行設定管理
-   稽核

將叢集設定視為程式碼
-   徹底檢查選擇 toodeploy hello 組態
-   請避免直接使用隱含命令 tootweak 資源

Hello 的許多層面[Service Fabric 應用程式生命週期](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-lifecycle)可以自動化。 [Azure Service Fabric PowerShell 模組](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications#upload-the-application-package)會將部署、升級、移除和測試 Azure Service Fabric 應用程式的常見工作自動化。 也可使用應用程式管理的 Managed 和 HTTP API。

## <a name="use-x509-certificates"></a>使用 X.509 憑證
請務必使用 X.509 憑證或 Windows 安全性來保護叢集。 在叢集建立期間只能設定安全性而且不可能 tooenable 安全性之後建立 hello 叢集。

如果您要指定[叢集憑證](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security)，設定 ClusterCredentialType tooX509 hello 值。 如果您指定的外部連接的伺服器憑證時，設定 hello ServerCredentialType tooX509。

-   執行生產環境工作負載之叢集中所使用的憑證應該是使用已正確設定的 Windows Server 憑證服務來建立，或是從已核准的憑證授權單位 (CA) 取得。
-   絕對不要在生產環境中使用以 MakeCert.exe 這類工具建立的暫時或測試憑證。
-   您可以使用自我簽署憑證，但應該只用於測試叢集，不應該在生產環境中使用。

如果 hello 叢集是較不安全。 任何人都可以匿名方式連線並執行管理作業，所以一律要使用 X.509 憑證或 Windows 安全性來保護生產叢集。

更多如何 tooenable 憑證中 service fabric 叢集，請參閱，toolearn[新增或移除憑證的 service fabric 叢集](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure)。

## <a name="configure-security-policies"></a>設定安全性原則
Service Fabric 也有助於安全 hello 資源所使用的應用程式中的 hello 使用者帳戶-部署的 hello 時段，例如、 檔案、 目錄和憑證。 如此一來，即使在共用主控環境中，執行中的應用程式就不會彼此干擾。

-   使用 Active Directory 網域群組或使用者： 您可以執行 Active Directory 使用者或群組帳戶的 hello 服務 hello 認證。 這是在您網域內的內部部署 Active Directory，與 Azure Active Directory (Azure AD) 無關。 使用網域使用者或群組，然後您可以存取其他資源 （例如，檔案共用） 的 hello 網域中已授與權限。

-   指定 HTTP 和 HTTPS 端點的安全性存取原則： 如果您套用 RunAs 原則 tooa 服務 hello 服務資訊清單宣告使用 hello HTTP 通訊協定的端點資源，您必須指定連接埠配置 toothese SecurityAccessPolicy tooensure端點會正確地存取控制列 hello 服務執行的 RunAs 使用者帳戶。 否則，http.sys 並沒有存取 toohello 服務，而失敗，將呼叫收到 hello 用戶端。
toolearn 更啟用服務網狀架構，請參閱 < 安全性原則[設定您的應用程式的安全性原則](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-runas-security)。

## <a name="reliable-actors-security-configuration"></a>Reliable Actors 安全性設定
服務網狀架構 Reliable Actors 是 hello 執行者設計模式的實作。 如同任何軟體設計模式中，是否 toouse 特定的模式會根據軟體設計問題 hello 決策符合 hello 模式。

做為一般的指導，請考慮 hello actor 模式 toomodel 您的問題或案例如果：
-   您的問題領域涉及大量 (數千個或更多) 小型、獨立且隔離的狀態和邏輯單位。
-   您想使用單一執行緒的物件不需要重大的互動，舉凡外部元件，包括跨的執行者集合查詢狀態 toowork。
-   您的動作項目執行個體將不會藉由發出 I/O 作業，使用無法預期的延遲來封鎖呼叫端。

在 Service Fabric 動作項目會實作在 hello Reliable Actors framework： 動作項目模式的應用程式架構之上[Service Fabric 可靠服務](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-introduction)。 您撰寫的每個 Reliable Actor 服務實際上都是已資料分割的具狀態可靠服務。
每個動作項目定義為動作項目類型的執行個體，相同 toohello 方式.NET 物件的.NET 型別執行個體。 例如，可能實作計算機 hello 功能動作項目類型，可能是該類型的不同節點分散叢集的許多參與者。 每一個這類的動作項目都有唯一的動作項目識別碼識別。

[複寫器的安全性組態](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-actors-kvsactorstateprovider-configuration)會用在複寫期間使用的 toosecure hello 通訊通道。 這表示服務無法看到彼此的複寫流量，確保 hello 資料，則高可用性的安全。 依預設，空白的安全性組態區段會妨礙複寫安全性。
複寫器的組態設定，負責建立 hello 動作項目狀態提供者狀態可靠 hello 複寫器。

## <a name="configure-ssl-for-azure-service-fabric"></a>設定 Azure Service Fabric 的 SSL

伺服器驗證： [Authenticates](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) hello 叢集管理端點 tooa 管理用戶端，以便 hello 管理用戶端會知道它正在交涉 toohello 實際叢集。 此憑證也會提供[SSL](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) hello HTTPS 管理 API 和透過 HTTPS 的 Service Fabric 總管。
您必須為您的叢集取得自訂網域名稱。 當您從 CA 要求憑證時，hello 憑證的主體名稱必須符合 hello 自訂網域名稱用於您的叢集。

tooconfigure SSL 應用程式，您必須先 tooget 已簽署的憑證授權單位 (CA)，受信任的協力廠商簽發憑證，針對此用途的 SSL 憑證。 如果您還沒有其中一個，您會需要公司銷售的 SSL 憑證的其中一個 tooobtain。

hello 憑證必須符合下列需求的 SSL 憑證在 Azure 中的 hello:
-   hello 憑證必須包含私密金鑰。
-   金鑰交換，可匯出 tooa 個人資訊交換 (.pfx) 檔案，就必須建立 hello 憑證。
-   hello 憑證的主體名稱必須符合 hello 用網域 tooaccess hello 雲端服務。 您無法從 hello cloudapp.net 網域的憑證授權單位 (CA) 取得 SSL 憑證。 您必須取得的自訂網域名稱 toouse 時存取您的服務。 當您從 CA 要求憑證時，hello 憑證的主體名稱必須符合 hello 自訂網域名稱使用 tooaccess 您的應用程式。 例如，如果您的自訂網域名稱為 contoso.com，則您需向 CA 要求 **.contoso.com** 或 **www.contoso.com.** 憑證。
-   hello 憑證必須使用至少 2048年位元加密。

HTTP 是不安全，並且很主旨 tooeavesdropping 攻擊，因為 hello hello web 瀏覽器 toohello web 伺服器或其他端點之間傳送的資料會以純文字傳送。 這表示攻擊者可以攔截並檢視敏感性資料，例如信用卡詳細資料和帳戶登入。 當資料使用 HTTPS 透過瀏覽器傳送或張貼時，SSL 可確保這類資訊經過加密及保護以避免遭到攔截。

詳細資訊，請參閱 toolearn，[設定 azure 應用程式的 SSL](https://docs.microsoft.com/azure/cloud-services/cloud-services-configure-ssl-certificate)。

## <a name="network-isolationsecurity-with-azure-service-fabric"></a>Azure Service Fabric 的網路隔離/安全性
使用[Azure 資源管理員 (ARM) 範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates)設定三個節點類型的範例為安全的叢集和 toocontrol hello 傳入和傳出網路流量使用網路安全性群組。

hello 範本具有每 hello 虛擬機器規模 set(VMSS) toocontrol hello 流量進出 hello VMSS 網路安全性群組。 做為預設值，hello 規則會設定所有 hello 流量所需的 tooallow hello 系統服務與 hello 應用程式連接埠 hello 範本中指定。 檢閱這些規則並進行變更 toofit 您的需求，包括加入任何新的應用程式。

如需詳細資訊，請參閱 [Azure Service Fabric - 常見網路案例](https://docs.microsoft.com/azure/service-fabric/service-fabric-patterns-networking)。

## <a name="set-up-a-key-vault-for-security"></a>設定金鑰保存庫以提供安全性
憑證用於 Service Fabric tooprovide 驗證和加密 toosecure 叢集，而它的應用程式的各個層面。

服務網狀架構會使用 X.509 憑證 toosecure 叢集，並提供應用程式的安全性功能。 您也使用金鑰保存庫[管理憑證](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure)在 Azure 中的 Service Fabric 叢集。 在 Azure 中部署叢集時，會負責建立 Service Fabric 叢集的 hello Azure 資源提供者就會從金鑰保存庫提取憑證，並 hello 叢集 Vm 上進行安裝。

hello 之間的關聯性[Azure 金鑰保存庫](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)、 service fabric 叢集，並使用憑證時它會建立叢集儲存在金鑰保存庫中的 hello Azure 資源提供者。

**建立資源群組**hello 第一個步驟是 toocreate 特別針對金鑰保存庫的資源群組。 我們建議您將 hello 金鑰保存庫放入自己的資源群組。 這個動作可讓您移除 hello 運算和存放裝置資源群組，包括 hello 資源群組包含 Service Fabric 叢集，而不會遺失您的金鑰和密碼。 包含金鑰保存庫中的 hello 資源群組必須在 hello 與正在使用它的 hello 叢集相同的區域。

**在 hello 新資源群組中建立金鑰保存庫**部署 tooallow hello 計算資源提供者從它的 tooget 憑證，並將它安裝在虛擬機器執行個體，就必須啟用 hello 金鑰保存庫。
更多如何查看 tooset Azure 金鑰保存庫註冊，toolearn[開始使用 Azure 金鑰保存庫](https://docs.microsoft.com/azure/key-vault/key-vault-get-started)。

## <a name="assign-users-roles"></a>對使用者指派角色
您已建立 hello 應用程式 toorepresent 您的叢集之後，您的使用者 toohello 將角色指派支援的 Service Fabric： 唯讀和系統管理員。您可以使用 hello Azure 傳統入口網站來指派 hello 角色。

>[!Note]
> 如需 Service Fabric 中角色的詳細資訊，請參閱 [角色型存取控制 (適用於 Service Fabric 用戶端)](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles)。

Azure Service Fabric 支援兩種不同的存取控制類型的用戶端的連線的 tooa [Service Fabric 叢集](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm)： 系統管理員和使用者。 存取控制可讓 hello 叢集系統管理員 toolimit 存取 toocertain 叢集作業會針對不同使用者群組，讓 hello 叢集更安全。

## <a name="next-steps"></a>後續步驟
- 設定 Service Fabric [開發環境](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started)。
- 了解 [Service Fabric 支援選項](https://docs.microsoft.com/azure/service-fabric/service-fabric-support)。

