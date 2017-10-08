---
title: "aaaAzure 詞彙-Azure 字典 |Microsoft 文件"
description: "Hello Azure 平台上使用 hello Azure 詞彙 toounderstand 雲端術語。 這個簡短的 Azure 字典提供 Azure 的常見雲端術語定義。"
keywords: "Azure 字典、雲端術語、Azure 詞彙、詞彙定義、雲端詞彙"
services: na
documentationcenter: na
author: MonicaRush
manager: jhubbard
editor: 
ms.assetid: d7ac12f7-24b5-4bcd-9e4d-3d76fbd8d297
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: monicar
ms.openlocfilehash: 486bbbfc71a48a6ebc39b14f7ab71f8604b7a6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-glossary-a-dictionary-of-cloud-terminology-on-hello-azure-platform"></a>Microsoft Azure 詞彙： hello Azure 平台上的雲端用語的字典

hello Microsoft Azure 詞彙是簡短的 hello Azure 平台的雲端用語的字典。 另請參閱：

* [Microsoft Azure 和 Amazon Web Services](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/) - Azure 服務及其 AWS 對應項目的定義。<!-- I propose toolink toohttps://azure.microsoft.com/en-us/services/ instead of this -->
* [雲端運算詞彙](https://azure.microsoft.com/overview/cloud-computing-dictionary/) - 一般產業雲端詞彙。

## <a name="account"></a>帳戶
已使用 tooaccess 並管理 Azure 訂用帳戶的帳戶。 它通常具有稱為 Azure 帳戶，即使帳戶可以是任何一項都 tooas： 現有的工作、 學校或個人 Microsoft 帳戶或 Office 365 使用者名稱和密碼。 您也可以建立帳戶 toomanage Azure 訂用帳戶時註冊 hello[免費試用版](https://azure.microsoft.com)。  
請參閱[註冊 Office 365 帳戶與 Azure 訂用帳戶](billing/billing-use-existing-office-365-account-azure-subscription.md)和[帳戶，您可以使用在 toosign](active-directory/active-directory-how-subscriptions-associated-directory.md)。

## <a name="api-app"></a>API 應用程式
[App Service 應用程式](#app-service-app)的另一個名稱。

## <a name="app-service-app"></a>App Service 應用程式
hello 計算資源， [Azure App Service](app-service/app-service-value-prop-what-is.md)提供裝載[網站或 web 應用程式](app-service-web/app-service-web-overview.md)， [web API](app-service-api/app-service-api-apps-why-best-platform.md)，或[行動裝置應用程式後端](app-service-mobile/app-service-mobile-value-prop.md). App Service 應用程式也會參照的 tooas*應用程式服務*， *web 應用程式*， *API apps*，和*行動裝置應用程式*。

## <a name="availability-set"></a>可用性設定組
虛擬機器的集合在一起管理 tooprovide 應用程式的備援性和可靠性。 hello 使用可用性設定組可確保在計劃性或非計劃性的維護事件期間至少一部虛擬機器時可用。  
請參閱[管理的 Windows 虛擬機器的 hello 可用性](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)和[管理 hello 的 Linux 虛擬機器的可用性](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="classic-model"></a>Azure 傳統部署模型
有兩個[部署模型](resource-manager-deployment-model.md)Azure 中使用 toodeploy 資源 （hello 新的模型是 Azure 資源管理員）。 某些 Azure 服務支援只 hello Resource Manager 部署的模型、 有些支援只 hello 傳統部署模型，和部分支援這兩種。 每個 Azure 服務的 hello 文件指定其支援的模型。

## <a name="cli"></a>Azure 命令列介面 (CLI)
命令列介面可以使用的 toomanage Azure 服務從 Windows、 macOS 和 Linux。  可以管理某些服務或服務功能，僅透過 PowerShell 或 hello CLI。 請參閱 [Azure CLI 2.0](/cli/azure/overview)

## <a name="powershell"></a>Azure PowerShell
命令列介面 toomanage Azure 服務透過命令列中，從 Windows 電腦。 可以管理某些服務或服務功能，僅透過 PowerShell 或 hello CLI。
請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)

## <a name="arm-model"></a>Azure Resource Manager 部署模型
有兩個[部署模型](resource-manager-deployment-model.md)（hello 其他是 hello 傳統部署模型） 的 Microsoft Azure 中使用 toodeploy 資源。 某些 Azure 服務支援只 hello Resource Manager 部署的模型、 有些支援只 hello 傳統部署模型，和部分支援這兩種。 每個 Azure 服務的 hello 文件指定其支援的模型。

## <a name="fault-domain"></a>容錯網域
hello 集合可能失敗的 hello 相同可用性設定組中的虛擬機器的時間。 範例之一是位於一個機架中的電腦群組，這組電腦會共用通用電源和網路開關。 在 Azure 中，多個容錯網域之間自動隔開 hello 可用性設定組中的虛擬機器。  
請參閱[管理的 Windows 虛擬機器的 hello 可用性](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)或[管理 hello 的 Linux 虛擬機器的可用性](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)  

## <a name="geo"></a>地區
針對資料常駐定義且通常包含兩個以上區域的界限。 hello 界限可能內或超過國家 （地區） 的框線，並受到稅法規。 每個地理區域至少擁有一個區域。 地理區域的範例為亞太地區和日本。 也稱為 *地理位置*。  
請參閱 [Azure 區域](best-practices-availability-paired-regions.md)

## <a name="geo-replication"></a>異地複寫
自動複寫內容，例如 blob、 資料表和佇列內的區域組的 hello 程序。  
請參閱 [Azure SQL Database 的主動式異地複寫](sql-database/sql-database-geo-replication-overview.md)
<!-- hello meaning of "geo" in this term seems toobe different than hello meaning provided in hello "geo" entry -->

## <a name="image"></a>image
包含 hello 作業系統和應用程式組態可以使用的 toocreate 任意數目的虛擬機器的檔案。 在 Azure 中有兩種類型的映像：VM 映像和作業系統映像。 VM 映像包含作業系統和建立 hello 映像時，所有磁碟都附加 tooa 虛擬機器。 作業系統映像只包含通用的作業系統且不含任何資料磁碟組態。  
請參閱[瀏覽和選取的 Windows 虛擬機器映像中使用 PowerShell 或 hello CLI Azure](virtual-machines/windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="limits"></a>限制
hello 可以建立或 hello 可達到的效能基準測試的資源數目。 限制通常會與訂用帳戶、服務和供應項目相關聯。  
請參閱 [Azure 訂用帳戶和服務限制、配額與限制](azure-subscription-service-limits.md)

## <a name="load-balancer"></a>負載平衡器
網路上電腦之間分散連入流量的資源。 在 Azure 中，負載平衡器會將流量 toovirtual 機器中負載平衡器集定義。 [負載平衡器](load-balancer/load-balancer-overview.md) 可以是面向網際網路的，也可以是內部的。  

## <a name="mobile-app"></a>行動裝置應用程式
[App Service 應用程式](#app-service-app)的另一個名稱。

## <a name="offer"></a>提供項目
hello 定價、 信用額度，與相關的條款適用 tooan Azure 訂用帳戶。  
請參閱 hello [Azure 優惠詳細資料頁面](https://azure.microsoft.com/support/legal/offer-details/)

## <a name="portal"></a>入口網站
hello 安全的 web 入口網站使用 toodeploy 和管理 Azure 服務。  有兩個入口網站： hello [Azure 入口網站](http://portal.azure.com/)和 hello[傳統入口網站](http://manage.windowsazure.com/)。 有些服務可用於這兩個入口網站，而其他人，才可以使用其中一或 hello 其他。 hello [Azure 入口網站的可用性圖表](https://azure.microsoft.com/features/azure-portal/availability/)列出可在哪一個入口網站中的服務。

## <a name="region"></a>region
地理區域內不會跨越國界且包含一或多個資料中心的地區。 定價、 地區服務和提供項目類型會公開在 hello 區域層級。 在區域通常會與另一個區域，可以是 up tooseveral 離開數百英哩配對。 區域配對可用來做為災害復原及高可用性案例的機制。 也稱為 tooas*位置*。  
請參閱 [Azure 區域](best-practices-availability-paired-regions.md)

## <a name="resource"></a>資源
Azure 方案一部分的項目。 每個 Azure 服務可讓您 toodeploy 不同類型的資源，例如資料庫或虛擬機器。   
請參閱 [Azure Resource Manager 概觀](azure-resource-manager/resource-group-overview.md)

## <a name="resource-group"></a>資源群組
資源管理員中的容器，可保留應用程式的相關資源。 hello 資源群組可包含所有的 hello 資源的應用程式或以邏輯方式分組這些資源。 您可以決定要如何 tooallocate 資源 tooresource 根據錯誤群組構成 hello 最適合您的組織。  
請參閱 [Azure Resource Manager 概觀](azure-resource-manager/resource-group-overview.md)

## <a name="arm-template"></a>Resource Manager 範本
在 JSON 檔案，以宣告方式定義一個或多個 Azure 資源，以及定義 hello 之間的相依性部署資源。 一致的方式和重複 hello 範本可以使用的 toodeploy hello 資源。  
請參閱[編寫 Azure Resource Manager 範本](resource-group-authoring-templates.md)

## <a name="resource-provider"></a>資源提供者
提供您可以部署及管理透過資源管理員的 hello 資源的服務。 每個資源提供者會提供以使用已部署的 hello 資源的作業。 資源提供者可以存取透過 hello Azure 入口網站，Azure PowerShell，以及幾個程式的 Sdk。  
請參閱 [Azure Resource Manager 概觀](azure-resource-manager/resource-group-overview.md)

## <a name="role"></a>角色
用於控制 toousers、 群組和服務可以指派的存取方式。 角色是無法 tooperform 動作，例如建立、 管理，以及在 Azure 資源上讀取。  
請參閱 [RBAC：內建角色](active-directory/role-based-access-built-in-roles.md)

## <a name="sla"></a>服務等級協定 (SLA)
Microsoft 的承諾描述適用於執行時間和連接的 hello 協議。 每個 Azure 服務都有特定的 SLA。  
請參閱[服務等級協定](https://azure.microsoft.com/support/legal/sla/)

## <a name="sas"></a>共用存取簽章 (SAS)
可讓您 tooa toogrant 有限存取的資源，而不會讓您的帳戶金鑰簽章。 例如， [Azure 儲存體使用 SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) toogrant 用戶端存取 tooobjects，例如 blob。 [IoT 中樞會使用 SAS](iot-hub/iot-hub-devguide-security.md#security-tokens) toogrant 裝置的權限 toosend 遙測。

## <a name="storage-account"></a>storage account
可讓您的帳戶存取 Azure 儲存體中的 toohello Azure Blob、 佇列、 表格和檔案服務。 hello 儲存體帳戶名稱定義 hello Azure 儲存體資料物件的唯一命名空間。  
請參閱[關於 Azure 儲存體帳戶](storage/common/storage-create-storage-account.md)

## <a name="subscription"></a>訂用帳戶
客戶的合約，讓他們 tooobtain Azure 的 Microsoft 服務。 hello 訂用帳戶定價和相關的詞彙所控管 hello 供應項目選擇 hello 訂用帳戶。
請參閱 [Microsoft 線上訂用帳戶合約](https://azure.microsoft.com/support/legal/subscription-agreement/)和 [Azure 訂用帳戶如何與 Azure Active Directory 產生關聯](active-directory/active-directory-how-subscriptions-associated-directory.md)

## <a name="tag"></a>tag
可讓您根據管理或帳單的 tooyour 需求 toocategorize 資源索引詞彙。 當您有複雜的資源集合時，您可以使用標記 toovisualize 資產 hello 方式可以讓 hello 最有意義。 例如，您可以標記您的組織中具有類似的角色，或屬於 toohello 資源相同的部門。  
請參閱[使用標記 tooorganize 您的 Azure 資源](resource-group-using-tags.md)

## <a name="update-domain"></a>更新網域
hello hello 在更新的虛擬機器的可用性設定組的集合相同的時間。 Hello 期間一起重新相同更新網域中的虛擬機器規劃的維護。 Azure 永遠不會一次重新啟動多個更新網域。 也稱為 tooas 升級網域。  
請參閱[管理的 Windows 虛擬機器的 hello 可用性](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)和[管理 hello 的 Linux 虛擬機器的可用性](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vm"></a>虛擬機器
hello 軟體實作的執行作業系統的實體電腦。 可以在同時執行多部虛擬機器 hello 相同硬體。 在 Azure 中，虛擬機器適用於各種大小。  
請參閱[虛擬機器文件](https://azure.microsoft.com/documentation/services/virtual-machines/)

## <a name="vm-extension"></a>虛擬機器擴充功能
資源實作行為或功能，是協助的運作或 hello 能力提供 toointeract 執行的電腦與其他程式。 比方說，您無法使用 hello VM 存取延伸 tooreset 或修改 Azure 的虛擬機器上的遠端存取值。
<!-- This definition seems obscure toome; maybe a list of examples would work better than a conceptual definition? -->
請參閱[關於虛擬機器擴充功能和功能 (Windows)](virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 或[關於虛擬機器擴充功能和功能 (Linux)](virtual-machines/linux/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vnet"></a>虛擬網路
一種網路，可提供與所有其他 Azure 租用戶隔離之 Azure 資源間的連線能力。 [Azure VPN 閘道](vpn-gateway/vpn-gateway-about-vpngateways.md)可讓您建立虛擬網路之間及[虛擬網路與內部部署網路之間](vpn-gateway/vpn-gateway-plan-design.md)的連線。 您也可以完全控制 hello IP 位址區塊、 DNS 設定、 安全性原則和虛擬網路內的路由表。  
請參閱[虛擬網路概觀](virtual-network/virtual-networks-overview.md)  

## <a name="web-app"></a>Web 應用程式
[App Service 應用程式](#app-service-app)的另一個名稱。

## <a name="see-also"></a>另請參閱

* [開始使用 Azure](https://azure.microsoft.com/get-started/)
* [雲端資源中心](https://azure.microsoft.com/resources/)  
* [讓 Azure 助您擴展商務應用程式](https://azure.microsoft.com/overview/business-apps-on-azure/)
* [Azure 之於您的資料中心](https://azure.microsoft.com/overview/business-apps-on-azure/)

