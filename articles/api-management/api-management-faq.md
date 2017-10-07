---
title: "aaaAzure API 管理常見問題集 |Microsoft 文件"
description: "了解 hello 回答 toocommon 問題、 模式和在 Azure API 管理的最佳作法。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 9e7cdf1b881a4dfed4bd2cfd7fbb4994f48b5f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-faqs"></a>Azure API 管理常見問題集
取得 Azure API 管理 hello 答案 toocommon 問題、 模式和最佳作法。

## <a name="contact-us"></a>與我們連絡
* [我如何可以詢問 hello Microsoft Azure API 管理小組的問題？](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question)


## <a name="frequently-asked-questions"></a>常見問題集
* [功能預覽中是什麼意思？](#what-does-it-mean-when-a-feature-is-in-preview)
* [如何保障安全 hello hello API 管理閘道與我的後端服務之間的連線？](#how-can-i-secure-the-connection-between-the-api-management-gateway-and-my-back-end-services)
* [如何將複製我 API 管理服務執行個體 tooa 新執行個體？](#how-do-i-copy-my-api-management-service-instance-to-a-new-instance)
* [我可以透過程式設計方式管理我的 API 管理執行個體嗎？](#can-i-manage-my-api-management-instance-programmatically)
* [如何新增使用者 toohello 系統管理員群組？](#how-do-i-add-a-user-to-the-administrators-group)
* [為何我想 tooadd hello 原則編輯器 中無法使用的 hello 原則？](#why-is-the-policy-that-i-want-to-add-unavailable-in-the-policy-editor)
* [如何在 API 管理中使用 API 版本設定？](#how-do-i-use-api-versioning-in-api-management)
* [如何在單一 API 中設定多個環境？](#how-do-i-set-up-multiple-environments-in-a-single-api)
* [可以使用 SOAP 搭配 API 管理嗎？](#can-i-use-soap-with-api-management)
* [是 hello API 管理閘道 IP 位址常數？我可以用在防火牆規則嗎？](#is-the-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules)
* [可以設定具有 AD FS 安全性的 OAUth 2.0 授權伺服器嗎？](#can-i-configure-an-oauth-20-authorization-server-with-adfs-security)
* [API 管理會使用何種路由方法的部署 toomultiple 地理位置？](#what-routing-method-does-api-management-use-in-deployments-to-multiple-geographic-locations)
* [可以使用 Azure Resource Manager 範本 toocreate API 管理服務執行個體嗎？](#can-i-use-an-azure-resource-manager-template-to-create-an-api-management-service-instance)
* [是否可以對後端使用自我簽署的 SSL 憑證？](#can-i-use-a-self-signed-ssl-certificate-for-a-back-end)
* [為什麼當我嘗試 tooclone GIT 儲存機制取得發生驗證錯誤？](#why-do-i-get-an-authentication-failure-when-i-try-to-clone-a-git-repository)
* [API 管理是否能搭配 Azure ExpressRoute 運作？](#does-api-management-work-with-azure-expressroute)
* [為什麼將「API 管理」部署到 Resource Manager 樣式的 VNET 中時，我們需要在這些 VNET 中有一個專用子網路？](#why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them)
* [Hello 將 API 管理部署至 VNET 時所需的最小的子網路大小為何？](#what-is-the-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet)
* [可以從一個訂用帳戶 tooanother 移動 API 管理服務嗎？](#can-i-move-an-api-management-service-from-one-subscription-to-another)
* [匯入 API 有任何限制或已知的問題嗎？](#are-there-restrictions-on-or-known-issues-with-importing-my-api)

### <a name="how-can-i-ask-hello-microsoft-azure-api-management-team-a-question"></a>我如何可以詢問 hello Microsoft Azure API 管理小組的問題？
您可以使用下列其中一個選項與我們連絡︰

* 將問題張貼在我們的 [API 管理 MSDN 論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=azureapimgmt)。
* 傳送電子郵件太<mailto:apimgmt@microsoft.com>。
* 在 hello 功能要求傳送給我們[Azure 的意見反應論壇](https://feedback.azure.com/forums/248703-api-management)。

### <a name="what-does-it-mean-when-a-feature-is-in-preview"></a>功能預覽中是什麼意思？
當一項功能處於預覽狀態時，這表示我們正在積極尋求 hello 功能如何運作為您的意見。 預覽中的功能在功能上完成，但也可確認我們進行重大變更回應 toocustomer 意見。 我們建議您不要依賴您生產環境中處於預覽狀態的功能。 如果您預覽功能上有任何意見反應，請讓我們知道透過一個 hello 連絡人選項中[方式可以我詢問 hello Microsoft Azure API 管理小組的問題？](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question)。

### <a name="how-can-i-secure-hello-connection-between-hello-api-management-gateway-and-my-back-end-services"></a>如何保障安全 hello hello API 管理閘道與我的後端服務之間的連線？
您有數個選項 toosecure hello hello API 管理閘道器與後端服務之間連線。 您可以：

* 使用 HTTP 基本驗證。 如需詳細資訊，請參閱 [設定 API 設定](api-management-howto-create-apis.md#configure-api-settings)。
* 使用 SSL 的相互驗證中所述[toosecure 後端服務在 Azure API 管理中使用用戶端憑證驗證的方式](api-management-howto-mutual-certificates.md)。
* 在您的後端服務上使用 IP 允許清單。 如果您有 Standard 或 Premium 層 API 管理執行個體，hello hello 閘道 IP 位址會維持不變。 您可以設定允許清單 tooallow 此 IP 位址。 您可以在 hello Azure 入口網站中的 hello 儀表板上取得 hello API 管理執行個體的 IP 位址。
* 連接您的 API 管理執行個體 tooan Azure 虛擬網路。

### <a name="how-do-i-copy-my-api-management-service-instance-tooa-new-instance"></a>如何將複製我 API 管理服務執行個體 tooa 新執行個體？
如果您想 toocopy API 管理執行個體 tooa 新執行個體，您會有數個選項。 您可以：

* 使用 hello 備份和還原在 API 管理中的函式。 如需詳細資訊，請參閱[如何使用 tooimplement 災害復原服務備份及還原在 Azure API 管理](api-management-howto-disaster-recovery-backup-restore.md)。
* 建立您自己的備份和還原功能，使用 hello [API 管理 REST API](https://msdn.microsoft.com/library/azure/dn776326.aspx)。 使用 hello REST API toosave，並從您想要的 hello 服務執行個體還原 hello 實體。
* 使用 Git，下載 hello 服務組態，並再將它上傳 tooa 的新執行個體。 如需詳細資訊，請參閱[如何 toosave 並設定您的 API 管理服務組態使用 Git](api-management-configuration-repository-git.md)。

### <a name="can-i-manage-my-api-management-instance-programmatically"></a>我可以透過程式設計方式管理我的 API 管理執行個體嗎？
可以，您可以使用下列各項，以程式設計方式管理 API 管理：

* hello [API 管理 REST API](https://msdn.microsoft.com/library/azure/dn776326.aspx)。
* hello [Microsoft Azure ApiManagement 服務管理程式庫 SDK](http://aka.ms/apimsdk)。
* hello[服務部署](https://msdn.microsoft.com/library/mt619282.aspx)和[服務管理](https://msdn.microsoft.com/library/mt613507.aspx)PowerShell cmdlet。

### <a name="how-do-i-add-a-user-toohello-administrators-group"></a>如何新增使用者 toohello 系統管理員群組？
以下是如何新增使用者 toohello 系統管理員群組：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 移 toohello 資源群組具有您想要 tooupdate hello API 管理執行個體。
3. 在 API 管理中，指派 hello **Api 管理參與者**角色 toohello 使用者。

現在 hello 新加入的參與者可以使用 Azure PowerShell [cmdlet](https://msdn.microsoft.com/library/mt613507.aspx)。 以下是如何 toosign 中的身為系統管理員：

1. 使用 hello `Login-AzureRmAccount` cmdlet toosign 中的。
2. 設定 hello 內容 toohello 訂用帳戶已使用的 hello 服務`Set-AzureRmContext -SubscriptionID <subscriptionGUID>`。
3. 使用 `Get-AzureRmApiManagementSsoToken -ResourceGroupName <rgName> -Name <serviceName>` 取得單一登入 URL。
4. 使用 hello URL tooaccess hello 系統管理入口網站。

### <a name="why-is-hello-policy-that-i-want-tooadd-unavailable-in-hello-policy-editor"></a>為何我想 tooadd hello 原則編輯器 中無法使用的 hello 原則？
如果您想要出現 tooadd hello 原則呈暗灰色或者陰影 hello 原則編輯器 中，務必確定您是在 hello hello 原則的正確範圍內。 每個原則陳述式可供您 toouse 特定範圍和原則區段。 tooreview hello 原則區段和領域的原則，請參閱 hello 原則使用方式區段中[API 管理原則](https://msdn.microsoft.com/library/azure/dn894080.aspx)。

### <a name="how-do-i-use-api-versioning-in-api-management"></a>如何在 API 管理中使用 API 版本設定？
您 API 管理中有幾個選項 toouse API 版本設定：

* 在 API 管理中，您可以設定應用程式開發介面 toorepresent 不同版本。 例如，您可能有兩個不同的 API (MyAPIv1 和 MyAPIv2)。 開發人員可以選擇 hello 開發人員的 hello 版本想 toouse。
* 您也可以使用不包含版本區段的服務 URL (例如 https://my.api) 來設定您的 API。 接著，在每個作業的[重寫 URL](https://msdn.microsoft.com/library/azure/dn894083.aspx#RewriteURL) 範本上設定版本區段。 例如，您的作業可以有名為 /resource 的 [URL 範本](api-management-howto-add-operations.md#url-template)和名為 /v1/Resource 的[重寫 URL](api-management-howto-add-operations.md#rewrite-url-template) 範本。 您可以變更 hello 版本區段值分別為每個作業。
* 如果您想要 tookeep hello 應用程式開發介面的服務 URL，在選取的作業中的 「 預設 」 版本區段設定原則，會使用 hello[設定後端服務](https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBackendService)原則 toochange hello 後端要求路徑。

### <a name="how-do-i-set-up-multiple-environments-in-a-single-api"></a>如何在單一 API 中設定多個環境？
tooset 多個環境，例如在測試環境和生產環境中，在單一的 API 中，您有兩個選項。 您可以：

* 主機上的不同 Api hello 同一個租用戶。
* 主機 hello 不同的租用戶中相同的 Api。

### <a name="can-i-use-soap-with-api-management"></a>可以使用 SOAP 搭配 API 管理嗎？
現在可以使用 [SOAP 傳遞](http://blogs.msdn.microsoft.com/apimanagement/2016/10/13/soap-pass-through/)支援。 系統管理員可以匯入 hello WSDL 的 SOAP 服務，以及 Azure API 管理將會建立 SOAP 前端。 開發人員入口網站文件、測試主控台、原則和分析全都適用於 SOAP 服務。

### <a name="is-hello-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules"></a>是 hello API 管理閘道 IP 位址常數？ 我可以用在防火牆規則嗎？
在 hello Standard 和 Premium 層 hello 公用 IP 位址 (VIP) hello API 管理租用戶是靜態存留期 hello hello 租用戶，但有些例外狀況。 在這些情況下的 hello IP 位址變更：

* 刪除並重新建立 hello 服務時。
* hello 服務訂用帳戶已[暫停](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states)或[警告](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states)（例如，針對 nonpayment)，然後恢復。
* 您新增或移除 （僅在 hello Developer 和 Premium 層可以使用虛擬網路） 的 Azure 虛擬網路。

多區域部署 hello 地區位址變更如果空出 hello 區域，然後恢復 （只在 hello Premium 層可以使用多區域部署）。

針對多重區域部署設定的進階層租用戶，每個區域會被指派一個公用 IP 位址。

Hello Azure 入口網站中的 hello 租用戶頁面上，您可以取得 IP 位址 （或位址，在多區域部署中的）。

### <a name="can-i-configure-an-oauth-20-authorization-server-with-ad-fs-security"></a>可以設定具有 AD FS 安全性的 OAUth 2.0 授權伺服器嗎？
如何 tooconfigure OAuth 2.0 授權伺服器與 Active Directory Federation Services (AD FS) 的安全性，請參閱的 toolearn [API 管理中的 使用 ADFS](https://phvbaars.wordpress.com/2016/02/06/using-adfs-in-api-management/)。

### <a name="what-routing-method-does-api-management-use-in-deployments-toomultiple-geographic-locations"></a>API 管理會使用何種路由方法的部署 toomultiple 地理位置？
API 管理使用 hello[效能流量路由方法](../traffic-manager/traffic-manager-routing-methods.md#priority)部署 toomultiple 地理位置中。 連入流量是路由的 toohello 最接近應用程式開發介面的閘道。 如果某個區離線，連入流量是自動路由的 toohello 下一個最接近的閘道。 深入了解[流量管理員路由方法](../traffic-manager/traffic-manager-routing-methods.md)中的路由方法。

### <a name="can-i-use-an-azure-resource-manager-template-toocreate-an-api-management-service-instance"></a>可以使用 Azure Resource Manager 範本 toocreate API 管理服務執行個體嗎？
是。 請參閱 hello [Azure API 管理服務](http://aka.ms/apimtemplate)快速入門範本。

### <a name="can-i-use-a-self-signed-ssl-certificate-for-a-back-end"></a>是否可以對後端使用自我簽署的 SSL 憑證？
是。 以下是如何 toouse 自我簽署安全通訊端層 (SSL) 憑證的後端：

1. 使用 API 管理建立[後端](https://msdn.microsoft.com/library/azure/dn935030.aspx)實體。
2. 設定 hello **skipCertificateChainValidation**屬性太**true**。
3. 如果您不想再 tooallow 自我簽署的憑證，刪除 hello 後端實體，或設定 hello **skipCertificateChainValidation**屬性太**false**。

### <a name="why-do-i-get-an-authentication-failure-when-i-try-tooclone-a-git-repository"></a>為什麼當我嘗試 tooclone Git 儲存機制取得發生驗證錯誤？
如果您使用 Git 認證管理員，或如果您正在使用 Visual Studio tooclone Git 儲存機制，您可能會遇到 hello Windows 認證 對話方塊中的已知問題。 hello 對話方塊的 限制密碼長度 too127 字元，並會進行截斷 hello Microsoft 產生密碼。 我們正在縮短 hello 密碼。 現在，請使用 Git Bash tooclone Git 儲存機制。

### <a name="does-api-management-work-with-azure-expressroute"></a>API 管理是否能搭配 Azure ExpressRoute 運作？
是。 API 管理能搭配 Azure ExpressRoute 運作。

### <a name="why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them"></a>為什麼將「API 管理」部署到 Resource Manager 樣式的 VNET 中時，我們需要在這些 VNET 中有一個專用子網路？
API 管理 hello 專用子網路的需求來自 hello 事實為基礎 （PAAS V1 層） 的傳統部署模型。 雖然我們可以部署至資源管理員 VNET （V2 層），但是會有結果 toothat。 hello Azure 中的傳統部署模型不與緊密結合 hello 資源管理員的模型，因此如果您建立 V2 層中的資源，hello V1 圖層並不知道它，可以發生的問題，例如嘗試 toouse 已配置的 IP 的 API 管理tooa NIC （根據 V2）。
有關在 Azure 中的傳統和資源管理員模型差異的詳細資訊請參閱太 toolearn[部署模型中的差異](../azure-resource-manager/resource-manager-deployment-model.md)。

### <a name="what-is-hello-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet"></a>Hello 將 API 管理部署至 VNET 時所需的最小的子網路大小為何？
hello 最小的子網路大小所需的 API 管理是的 toodeploy [/29](../virtual-network/virtual-networks-faq.md#configuration)，這是 hello Azure 支援的最小的子網路大小。

### <a name="can-i-move-an-api-management-service-from-one-subscription-tooanother"></a>可以從一個訂用帳戶 tooanother 移動 API 管理服務嗎？
是。 toolearn 作法，請參閱[移動資源 tooa 新資源群組或訂用帳戶](../azure-resource-manager/resource-group-move-resources.md)。

### <a name="are-there-restrictions-on-or-known-issues-with-importing-my-api"></a>匯入 API 有任何限制或已知的問題嗎？
Open API(Swagger)、WSDL 及 WADL 格式的[已知問題和限制](api-management-api-import-restrictions.md)。
