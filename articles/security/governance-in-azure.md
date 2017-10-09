---
title: "在 Azure 中的 aaaGovernance |Microsoft 文件"
description: "深入了解雲端運算服務，其中包含寬的選取範圍的計算執行個體 （& s） 可以自動 toomeet hello 需求的應用程式或企業上下調整的服務。"
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: TomSh
ms.openlocfilehash: 956e82e92f4232c24069bdb79fed5315f1d6486f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="governance-in-azure"></a>Azure 中的治理

我們知道安全性是 hello 定域機組中的其中一個工作，而且重要，您會看到 Azure 安全性的精確且即時資訊。 Tootake 利用其廣泛的安全性工具和功能的其中一個 hello 最佳原因 toouse Azure 應用程式與服務。 這些工具和功能協助您更 hello 安全 Azure 平台上可能 toocreate 安全解決方案。

您進一步了解控管控制項 hello 陣列從這兩個 hello 客戶的實作在 Microsoft Azure 內，而且 Microsoft operations' 檢視方塊，本文中，「 控管中 Azure 」，會寫入提供 hello 查看全方位 toohelp適用於 Microsoft Azure 的管理功能。

## <a name="azure-platform"></a>Azure 平台

Azure 是一個公用雲端服務平台，支援廣泛的作業系統、程式設計語言、架構、工具、資料庫及裝置。 它可以透過 Docker 整合執行 Linux 容器；使用 JavaScript、Python、.NET、PHP、Java 及 Node.js 建置應用程式；為 iOS、Android 及 Windows 裝置建置後端。 Azure 公用雲端服務支援相同的技術數百萬的開發人員和 IT 專業人員已經依賴和信任的 hello。

當您建置，或移轉到 IT 資產時，您依賴該組織的能力 tooprotect 應用程式和 hello 服務與 hello 控制項資料的公用雲端服務提供者提供 toomanage hello 安全性您雲端架構資產。

從裝載吸引數百萬的客戶同時 hello 設備 tooapplications 設計 azure 的基礎結構，並提供的企業符合安全性需求的可信任基礎。 此外，Azure 提供您許多的安全性選項和 hello 能力 toocontrol 它們可讓您可以自訂的組織部署的安全性 toomeet hello 獨特需求。

本文件有助於了解 Azure 治理功能如何協助您滿足這些需求。

## <a name="abstract"></a>摘要

Microsoft Azure 雲端控管可提供的整合式的稽核和顧問的方法，來檢閱及通知其使用方式的 hello Azure 平台的組織。 Microsoft Azure 雲端控管代表 toohello 的決策程序、 條件和原則相關以 hello 規劃、 架構、 擷取、 部署、 操作及管理雲端的運算。

toocreate Microsoft Azure 雲端控管的計劃，您需要 tootake hello 人員、 程序，以及目前技術的地方，深入了解，然後建置架構可簡化 IT tooconsistently 支援同時提供結束的商務需求hello 彈性 toouse hello 強大功能的 Microsoft Azure 的使用者。

本白皮書說明在 Microsoft Azure 中更深入治理 IT 資源的方式。 這份文件可協助您了解內建的 tooMicrosoft Azure hello 安全性和管理功能。

hello 下面是這份文件中討論的主要 hello 控管問題：

- 針對組織目標實作原則、流程及程序。

- 符合組織標準的安全性及持續符合合規性

- 警示和監視

## <a name="implementation-of-policies-processes-and-procedures"></a>實作原則、流程及程序 

管理已建立 hello 資訊安全性原則和作業的持續性的角色和責任 toooversee 的實作整個 Azure。 Microsoft Azure 管理會負責監督安全性和持續性小組 (包括協力廠商) 在相對應作業上所採取的作法，並促進符合安全性原則、程序及標準的合規性。

以下是發展的 hello 因素：

- 帳戶佈建

- 訂用帳戶控制

- 角色型存取控制

- 資源管理

- 資源追蹤

- 重要資源控制

- 應用程式開發介面存取 tooBilling 資訊

- 網路控制

## <a name="account-provisioning"></a>帳戶佈建

定義帳戶階層的主要步驟 toouse 和結構公司內的 Azure 服務，而 hello 核心控管結構。 發生與 hello 企業協議的客戶，客戶可以進一步細分成部門、 帳戶和最後，訂閱 hello 環境。

![帳戶佈建](./media/governance-in-azure/security-governance-in-azure-fig1.png)

如果您沒有 enterprise 合約，請考慮使用[Azure 標記](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)在訂用帳戶層級 toodefine 階層。 Azure 訂用帳戶是 hello 基本的單位，其中包含所有資源。 它也可在 Azure 中定義數個限制，例如核心、資源等的數目。訂用帳戶可以包含[資源群組](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)，其中可以包含資源。 那三個層級需套用 [RBAC](https://docs.microsoft.com/azure/api-management/api-management-role-based-access-control) 準則。

每個企業不同和使用 Azure 標記發生非企業客戶的 hello 階層可讓針對極大彈性的 Azure hello 公司內的組織方式。 在部署之前在 Microsoft Azure 中的資源，您應該實際的階層，並了解 hello 影響帳單、 資源的存取和複雜性。

## <a name="subscription-controls"></a>訂用帳戶控制

訂用帳戶能控制資源使用量的報告與計費方式。 訂用帳戶可以針對個別的計費與付款進行設定。 如先前所述，單一 Azure 帳戶底下可以有多個訂用帳戶。 訂用帳戶可以是多個部門在公司使用的 toodetermine hello Azure 資源使用量。

例如，如果某個公司有 IT、HR 及行銷部門，而這些部門都在執行不同的專案。 根據每個部門 hello 的 Azure 資源，例如虛擬機器的使用方式，就可以據此計費。 由此我們可以控制每個部門的 hello 財務。

Azure 訂用帳戶會建立三個參數：

- 唯一的訂閱者識別碼

- 計費位置

- 可用資源集合

各個會包含一個 Microsoft 帳戶識別碼、 信用卡號碼和 hello 套完整的 Azure 服務-雖然 Microsoft 會強制執行耗用量限制，視 hello 訂用帳戶類型而定。

Azure 註冊階層會定義服務在企業合約內的結構方式。 hello 企業版入口網站可讓客戶根據靈活的階層，可自訂的 tooan 組織的獨特需求 Enterprise 合約相關聯的 toodivide 存取 tooAzure 資源。 hello 階層模式以便 hello 相關聯的計費及存取資源可以精確地佔用之，應該要符合組織的管理和地理結構。

hello 三個高階模式功能、 業務單位，而且地理，並使用部門的系統管理建構帳戶群組。 在每個部門中，可以將訂用帳戶指派給帳戶，這能在 Azure 中建立計費和數個重要限制 (例如 VM 數目、儲存體帳戶等) 的隔閡。

![訂用帳戶控制](./media/governance-in-azure/security-governance-in-azure-fig2.png)


針對具有企業合約的組織，Azure 訂用帳戶會遵循四個層級的階層：

- 企業註冊系統管理員

- 部門系統管理員

- 帳戶擁有者

- 服務管理員

此階層控管 hello 下列：

- 計費關聯性

- 帳戶管理

- 角色型存取控制 (RBAC) tooartifacts

- 界線/限制

- 界線

  - 使用量和計費 (費率卡片會以優惠數目為基礎)

  - 限制

  - 虛擬網路

- 附加 too1 AAD （1 AAD 是許多訂閱相關聯）

- 相關聯的 tooan enterprise 註冊帳戶

## <a name="role-based-access-controls"></a>角色型存取控制

Azure 最初發行時，存取控制項 tooa 訂用帳戶已基本： 系統管理員或共同管理員。 存取 tooa 訂用帳戶中 hello 傳統模型隱含存取 tooall hello 資源 hello 入口網站中。 這種欠缺更細微的控制會造成訂閱 tooprovide 合理的存取控制層級進行 Azure 註冊 toohello 激增。

![角色型存取控制](./media/governance-in-azure/security-governance-in-azure-fig3.png)

不再需要此種訂用帳戶激增情況。 以角色為基礎的存取控制，您可以將使用者指派給 toostandard 角色 （例如通用的 「 讀取器 」 和 「 寫入器 」 類型的角色）。 您也可以定義自訂角色。

[Azure 角色型存取控制 (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) 可以對 Azure 進行更細緻的存取權管理。 使用 RBAC 時，您可以授與只 hello 少量的存取權，使用者需要 tooperform 他們的工作。 安全性導向公司應該專注於讓員工 hello 所需的確切權限。 太多權限公開帳戶 tooattackers。 權限太少則會讓員工無法有效率地完成工作。 Azure「角色型存取控制」(RBAC) 可以為 Azure 提供更細緻的存取管理來協助解決這個問題。 RBAC 可協助您 toosegregate 責任您小組和授與唯一 hello 的內存取 toousers 他們需要 tooperform 他們的工作。 您可以不授與每個人 Azure 訂用帳戶或資源中無限制的權限，而是只允許執行特定的動作。

例如，使用 RBAC toolet 一位員工管理訂用帳戶中的虛擬機器，而另一個可以管理 SQL 資料庫內 hello 相同訂用帳戶。

Azure RBAC 具有三個套用 tooall 資源類型的基本角色：

- **擁有者**具有完整存取 tooall 資源，包括 hello 右 toodelegate 存取 tooothers。

- **參與者**可以建立及管理 Azure 資源的所有類型，但無法授與存取 tooothers。

- **讀者** 可以檢視現有的 Azure 資源。

hello RBAC 角色在 Azure 中的 hello rest 允許特定的 Azure 資源管理。 例如，hello 虛擬機器參與者角色可讓 hello 使用者 toocreate 及管理虛擬機器。 它沒有提供這些存取 toohello 虛擬網路或 hello hello 虛擬機器的子網路連線到。

[RBAC 內建角色](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles)清單 hello Azure 中可用的角色。 它會指定 hello 作業和每個內建的角色會授與 toousers 的範圍。

藉由指派 hello 適當 RBAC 角色 toousers、 群組和應用程式在特定範圍授與存取權。 訂用帳戶、 資源群組或單一資源，可以是 hello 範圍的角色指派。 在父範圍中指派的角色也會授與存取內含 toohello 子系。

例如，具有存取 tooa 資源群組的使用者可以管理其中的內容，例如網站、 虛擬機器，以及子網路的所有 hello 資源。

Azure RBAC 僅支援管理操作的 hello Azure 中的資源 hello Azure 入口網站和 Azure 資源管理員 Api。 它無法授權 Azure 資源的所有資料層級作業。 例如，您可以授權有人 toomanage 儲存體帳戶，但不是 toohello blob 或儲存體帳戶內的資料表無法。 同樣地，SQL database 的管理、 但不是 hello 資料表內。

如果您需要有關 RBAC 如何協助您管理存取權的詳細資訊，請參閱 [什麼是角色型存取控制](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)。

您也可以[建立自訂安全性角色](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles)所有存取控制 (RBAC) 如果 hello 內建角色都不符合您的特定存取都需要。 您可以使用建立自訂角色[Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell)， [Azure 命令列介面 (CLI)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-azure-cli)，和 hello [REST API](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-rest)。 內建的角色，就像 toousers、 群組和應用程式在訂用帳戶、 資源群組和資源的範圍可以指派自訂的角色。

在每個訂用帳戶，您可以授與向上 too2000 角色指派。

## <a name="resource-management"></a>資源管理

Azure 中原本提供 hello 傳統部署模型。 在此模型中，每個資源存在於獨立;沒有方法 toogroup 相互關聯的資源。 相反地，您必須追蹤組成您的方案或應用程式中，哪些資源，並請記得 toomanage toomanually 中協調的方式。

toodeploy 方案，您必須建立個別透過 hello 傳統入口網站的每個資源，或建立指令碼部署 hello 正確的順序中的所有 hello 資源 tooeither。 toodelete 方案，您必須 toodelete 每個資源個別。 您無法輕易套用和更新相關資源的存取控制原則。 最後，您無法套用標籤 tooresources toolabel 這些條款，可協助您監視您的資源和管理計費。

在 2014 中，Azure 會導入了資源管理員，加入的資源群組的 hello 概念。 資源群組是共用共同生命週期的資源容器。 hello Resource Manager 部署模型有數個優點：

- 您可以部署、 管理及監視所有的 hello 服務，您的解決方案，為群組，而不是個別處理這些服務。

- 您可以在整個生命週期中重複部署方案，並確信您的資源會以一致的狀態部署。

- 您可以套用存取控制 tooall 資源在資源群組中，而且這些原則會自動套用新的資源新增 toohello 資源群組時。

- 您可以將標籤套用 tooresources toologically 組織您的訂用帳戶中的所有 hello 資源。

- 您可以使用 JavaScript Object Notation (JSON) toodefine hello 基礎結構，您的解決方案。 hello JSON 檔案稱為 Resource Manager 範本。

- 您可以定義 hello 資源，所以它們部署在 hello 正確的順序之間的相依性。

![資源管理](./media/governance-in-azure/security-governance-in-azure-fig4.png)

資源管理員可讓您 tooput 資源成有意義的群組管理、 計費，或自然親和性。 如先前所述，Azure 有兩個部署模型。 在稍早 hello[傳統模型](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model)，hello 的基本管理單位已 hello 訂用帳戶。 您很難 toobreak 向訂用帳戶，導致 toohello 建立大量的訂用帳戶內的資源。 使用 hello 資源管理員模型時，我們可了解資源群組的 hello 簡介。

資源群組是存放 Azure 方案相關資源的容器。 [hello 資源群組](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)可以包含所有 hello 資源 hello 解決方案或您想 toomanage 為群組的資源。 您決定要如何 tooallocate 資源 tooresource 根據錯誤群組構成 hello 最適合您的組織。

如需範本的建議，請參閱[建立 Azure Resource Manager 範本的最佳做法](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices)。

Azure 資源管理員會分析 hello 正確的順序會建立 tooensure 資源的相依性。 如果某個資源依賴另一個資源的值 (例如需要儲存體帳戶以供磁碟使用的虛擬機器)，您必須設定相依性。

>[!Note]
>如需詳細資訊，請參閱 [定義 Azure Resource Manager 範本中的相依性](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-define-dependencies)。

您也可以使用 hello 範本更新 toohello 基礎結構。 例如，您可以將資源 tooyour 方案，並將已部署的 hello 資源設定規則。 如果 hello 範本會指定建立資源，但該資源已存在，Azure 資源管理員會執行更新，而不是建立新的資產。 Azure 資源管理員更新 hello 現有資產 toohello 相同狀態做為它就是當新的。

當您需要其他的作業，例如安裝不包含在 hello 安裝的軟體時，資源管理員會提供擴充功能案例。

## <a name="resource-tracking"></a>資源追蹤

當您組織中的使用者加入資源 toohello 訂用帳戶時，會變得越來越重要 tooassociate 與 hello 適當部門、 客戶及環境的資源。 您可以將附加的中繼資料 tooresources 透過標記。 您使用[標記](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)tooprovide hello 資源或 hello 擁有者資訊。 標記 toonot 只彙總與群組資源數種方式可讓您，不過基於計費的 hello 使用該資料。

當您有複雜的資源群組和資源，而且需要 toovisualize 這些資產，可透過 hello 大部分意義 tooyou hello 方式，請使用標記。 例如，您可以標記您的組織中具有類似的角色，或屬於 toohello 資源相同的部門。

沒有標記，您的組織中的使用者可以建立多個資源，可能會難以 toolater 識別及管理。 比方說，您可能需要 toodelete 專案的所有 hello 資源。 如果這些資源不會標記為 hello 專案，您必須手動尋找它們。 標記可以是重要的方式，讓您 tooreduce 不必要的成本，您的訂用帳戶中。

資源不需要在 hello tooreside 相同資源群組 tooshare 標記。 您可以建立您自己標記分類 tooensure 您組織中的所有使用者都使用通用標記，而不是使用者不小心套用稍微不同的標籤 （例如 「 部門 」 而不是 「 部門 」）。

資源原則可讓您組織的 toocreate 標準規則。 您可以建立原則，確保資源都會加上 hello 適當的值。

> [!Note]
> 如需詳細資訊，請參閱[套用標籤的資源原則](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags)。

您也可以檢視透過 hello Azure 入口網站已加上標籤的資源。

hello[使用量報告](https://docs.microsoft.com/azure/billing/billing-understand-your-bill)針對您的訂閱包含標記的名稱和值，這可讓您依標記的 toobreak 出成本。

> [!Note]
> 如需標記的詳細資訊，請參閱[使用標記 tooorganize 您的 Azure 資源](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)。

hello 下列限制適用於 tootags:

- 每個資源或資源群組最多可以有 15 個標記索引鍵/值組。 這項限制只適用於直接套用 tootags toohello 資源群組或資源。 資源群組可以包含許多資源，其各自有 15 個標記索引鍵/值組。

- hello 標記名稱為有限的 too512 字元。

- hello 標記值為有限的 too256 字元。

- 套用標籤 toohello 資源群組不會繼承該資源群組中的 hello 資源。

如果您有超過 15 的值，您需要 tooassociate 與資源，請使用 JSON 字串 hello 標記值。 hello JSON 字串可以包含許多值套用的 tooa 單一標記索引鍵。

### <a name="tags-and-billing"></a>標記與計費

標籤可讓您 toogroup 計費資料。 比方說，如果您執行於不同的組織多個 Vm，請依成本中心使用 hello 標記 toogroup 使用量。 您也可以使用標記 toocategorize 成本由執行階段環境。例如，在生產環境中執行的 vm hello 計費的使用量。

您可以擷取有關透過 hello 標記資訊[Azure 資源使用量和 RateCard Api](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview)或 hello 使用量逗點分隔值 (CSV) 檔案。 您可以下載 hello 使用量檔案從 hello [Azure 帳戶入口網站](https://account.windowsazure.com/)或[EA 入口網站](https://ea.azure.com/)。

>[!Note]
> 如需有關以程式設計方式存取 toobilling 資訊的詳細資訊，請參閱[深入了解您的 Microsoft Azure 資源耗用量](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview)。 若為 REST API 作業，請參閱 [Azure 計費 REST API 參考](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c)。

當您下載之服務的支援和計費標籤 hello 使用 CSV 時，hello 標籤會顯示 hello 標記 資料行中。

## <a name="critical-resource-controls"></a>重要資源控制

您的組織加入核心服務 toohello 訂用帳戶，變得越來越重要 tooensure 這些服務的可用 tooavoid 業務中斷。 [資源鎖定](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources)讓您修改或刪除這些裝置會有重大影響您的應用程式或雲端基礎結構上的高價值資源 toorestrict 作業。 您可以套用鎖定 tooa 訂用帳戶、 資源群組或資源。 一般而言，您可以套用鎖定 toofoundational 資源，例如虛擬網路、 閘道和儲存體帳戶。

資源鎖定目前支援兩個值︰CanNotDelete 和 ReadOnly。 CanNotDelete 表示 （使用 hello 適當的權限） 的使用者仍然可以讀取或修改資源，但不能予以刪除。 ReadOnly 表示經過授權的使用者無法刪除或修改資源。

資源管理員鎖定套用在 hello 管理平面組成太傳送作業中發生的 toooperations<https://management.azure.com>。 hello 鎖定不會限制其資源如何執行他們自己的函式。 限制資源的變更，但沒有限制資源的作業。 例如，SQL Database 的 ReadOnly 鎖定可防止您刪除或修改 hello 資料庫，但它不會阻止您建立、 更新或刪除 hello 資料庫中的資料。

套用**ReadOnly**可能會造成 toounexpected 結果，因為看起來雖然某些作業讀取作業需要其他動作。 例如，放置**ReadOnly**儲存體帳戶上的鎖定可防止所有使用者列出 hello 索引鍵。 hello 清單索引鍵作業透過 POST 要求因為 hello 傳回索引鍵是可用的寫入作業。

![重要資源控制](./media/governance-in-azure/security-governance-in-azure-fig5.png)

另一個範例中，應用程式服務資源上放置唯讀鎖定可防止 Visual Studio 伺服器總管顯示 hello 資源的檔案，因為該互動需要寫入權限。

不同於以角色為基礎的存取控制，您可以使用管理鎖定 tooapply 限制跨所有使用者和角色。 toolearn 有關設定權限的使用者和角色，請參閱[Azure 角色型存取控制](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure)。

當您套用在父範圍的鎖定時，該範圍內的所有資源都繼承 hello 相同的鎖定。 即使您稍後新增的資源會繼承 hello 父系中的 hello 鎖定。 hello hello 繼承中限制最嚴格的鎖定會優先使用。

toocreate 或刪除管理鎖定，您必須擁有存取 tooMicrosoft.Authorization/_或 Microsoft.Authorization/locks/_動作。 Hello 內建角色時，只有**擁有者**和**使用者存取系統管理員**授與這些動作。

## <a name="api-access-toobilling-information"></a>應用程式開發介面存取 toobilling 資訊

使用 Azure 計費 Api toopull 使用情形和資源資料到您的慣用的資料分析工具。 hello Azure 資源使用量和 RateCard 應用程式開發介面可協助您準確地預測和管理您的成本。 hello Api 會實作成資源提供者和 hello 系列 hello Azure 資源管理員所公開的應用程式開發介面的一部分。

### <a name="azure-resource-usage-api-preview"></a>Azure 資源使用情況 API (預覽)

使用 hello Azure[資源使用量 API](https://msdn.microsoft.com/library/azure/mt219003) tooget 估計 Azure 耗用量資料。 hello API 包括：

- **Azure 角色型存取控制**-設定存取原則在 hello [Azure 入口網站](https://portal.azure.com/)或透過[Azure PowerShell cmdlet](https://docs.microsoft.com/powershell/azure/overview) toospecify 哪些使用者或應用程式進行存取toohello 訂用帳戶的使用量資料。 呼叫端必須使用標準的 Azure Active Directory 權杖進行驗證。 加入 hello 呼叫端 tooeither hello 計費的讀取器，讀取器、 擁有者或參與者角色 tooget 存取 toohello 使用量資料特定的 Azure 訂用帳戶。

- **每小時或每日彙總** - 呼叫端可以指定要 Azure 使用情況資料的每小時值區或每日值區。 hello 預設值是每日。

- **執行個體中繼資料 （包括資源標記）** – 取得執行個體層級詳細資料，例如 hello 完整的資源 uri (/subscriptions/ {訂閱 id} / …)，hello 資源群組資訊和資源標記。 這個中繼資料可協助您確定的方式，並以程式設計方式配置 hello 標記，例如跨充電的使用案例使用方式。

- **資源的中繼資料**-資源詳細資料，例如 hello 計量表的名稱、 計量表類別目錄、 計量表子類別目錄、 單位和區域提供 hello 呼叫者更深入了解什麼對於使用。 我們也正在 tooalign 資源的中繼資料術語跨 hello Azure 入口網站、 Azure 使用量 CSV，計費 CSV、 EA 和其他公開體驗，讓資料相互關聯跨體驗 toolet。

- **所有優惠類型的使用情況** – 所有優惠類型 (例如隨收隨付、MSDN、貨幣承諾、貨幣信用額度和 EA) 皆有提供使用情況資料。

**Azure 資源 RateCard API (預覽)**

使用 hello Azure 資源 RateCard API tooget hello 可用的 Azure 資源的清單，並估計每個定價資訊。 hello API 包括：

- **Azure 角色型存取控制**-hello Azure 入口網站上設定存取原則，或透過使用者或應用程式可以取得 Azure PowerShell cmdlet toospecify 存取 toohello RateCard 資料。 呼叫端必須使用標準的 Azure Active Directory 權杖進行驗證。 加入 hello 呼叫端 tooeither hello 讀取器、 擁有者或參與者角色 tooget 存取 toohello 使用量資料特定的 Azure 訂用帳戶。

- **支援隨收隨付、MSDN、貨幣承諾、貨幣信用額度優惠 (不支援 EA)** - 此 API 提供 Azure 優惠層級費率資訊。 此 API 的 hello 呼叫端必須傳入 hello 優惠資訊 tooget 資源詳細資料和率。 因為 EA 優惠已自訂每個註冊的速率，我們目前無法 tooprovide EA 率。 以下是一些 hello 實現具有 hello 使用量與 hello RateCard Api hello 組合的案例：

- **Azure 花 hello 月**-hello 月支出 hello 使用量和 RateCard Api tooget 更深入了解您的雲端使用 hello 組合。 您可以每小時分析 hello 和估計每日的值區的使用量和計量。

- **設定警示**– 使用 hello 使用量及 hello RateCard Api tooget 估計雲端耗用量和費用，並設定資源或貨幣型警示。

- **預測的帳單**– 取得您的估計耗用量和雲端的支出，和套用機器學習演算法 toopredict 哪些 hello bill 會結尾 hello hello 計費週期。

- **成本分析前耗用量**– 使用多少帳單會套用至您的預期使用量時移動工作負載 tooAzure hello RateCard API toopredict。 如果您有其他的雲端或私人雲端中的現有工作負載時，您也可以對應與 hello Azure 率 tooget 花較佳的估計值，Azure 的使用方式。 此估計可讓您 hello 能力 toopivot 上提供的服務，並隨用隨付，超出的 hello 其他優惠類型之間的比較，例如貨幣承諾與貨幣信貸。 hello API 也可讓您 hello 能力 toosee 成本差異區域，並可讓您 toodo 假設成本分析 toohelp 進行的部署決策。

- **分析**-您可以判斷它是否符合成本效益 toorun 工作負載在另一個區域中，或在另一個組態的 hello Azure 資源。 Hello 您所使用的 Azure 區域根據 azure 資源的成本可能會不同。

- 您也可以判斷另一個 Azure 優惠類型是否會在 Azure 資源上提供更好的費率。

## <a name="networking-controls"></a>網路控制

存取 tooresources 可以是內部 （在 hello 公司的網路） 或外部 (透過 hello 網際網路)。 它是方便使用者在您的組織 tooinadvertently put 的資源在 hello 錯誤的位置，然後可能會開啟 toomalicious 存取。 如同使用在內部部署裝置，企業必須加入適當的控制項 tooensure Azure 使用者做出 hello 正確的決策。

![網路控制](./media/governance-in-azure/security-governance-in-azure-fig6.png)

針對訂用帳戶治理，我們會找出可提供基本存取控制的核心資源。 hello 核心資源所組成：

### <a name="network-connectivity"></a>網路連線

[虛擬網路](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)是子網路的容器物件。 雖然並非絕對必要，通常使用連接的應用程式 toointernal 公司資源時。 hello Azure 虛擬網路服務可讓您 toosecurely 連接的 Azure 資源 tooeach 其他與虛擬網路 (Vnet)。

VNet 是網路的您自己 hello 雲端中的表示法。 VNet 是 hello 的隔離的邏輯專用的 Azure 雲端 tooyour 訂用帳戶。 您也可以連接的 Vnet tooyour 在內部部署網路。

以下為 Azure 虛擬網路的功能：

- **隔離**︰VNet 會彼此隔離。 您可以建立個別的開發、 測試和生產環境的 Vnet 該使用 hello 相同的 CIDR 位址區塊。 相反地，您可以建立多個使用不同 CIDR 位址區塊的 VNet 並將這些網路連接在一起。 您可以將 VNet 分成多個子網路。 Azure 提供的內部名稱解析的 Vm 和雲端服務角色執行個體連接 tooa VNet。 您可以選擇性地設定 VNet toouse 您自己的 DNS 伺服器，而不是使用 Azure 的內部名稱解析。

- **網際網路連線**： 連接的 tooa VNet 擁有的所有 Azure 虛擬機器 (VM) 和雲端服務角色執行個體存取 toohello 網際網路，根據預設。 視需要您也可以啟用輸入的存取 toospecific 資源。

- **Azure 資源連接**: Azure 資源，例如雲端服務和 Vm 可以連接的 toohello 相同的 VNet。 hello 資源可以連接 tooeach 其他使用私人 IP 位址，即使它們位於不同子網路。 Azure 預設之間提供路由子網路、 Vnet，與在內部部署網路，因此您不需要 tooconfigure，管理路由。

- **VNet 連線**: Vnet 可以是其他連接的 tooeach，讓資源連線 tooany VNet toocommunicate 與任何其他 VNet 上的任何資源。

- **在內部部署連線**: Vnet 必須透過網路與 Azure 之間的私人網路連線或透過站對站 VPN 連線的連線的 tooon 內部網路是透過網際網路 hello。

- **流量篩選**︰可以依照來源 IP 位址和連接埠、目的地 IP 位址和連接埠以及通訊協定，對 VM 和雲端服務角色執行個體網路流量進行輸入及輸出的篩選。

- **路由**︰您可以透過設定自己的路由，或使用透過網路閘道的 BGP 路由，選擇性地覆寫 Azure 的預設路由。

## <a name="network-access-controls"></a>網路存取控制

[網路安全性群組](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)類似防火牆和 hello 網路上提供規則的方式資源可以 「 交談 」。 它們提供更精確地控制如何 / 如果 toohello 網際網路或其他子網路中的可以連接的子網路 （或虛擬機器） hello 相同虛擬網路。

網路安全性群組 (NSG) 包含可允許或拒絕網路流量 tooresources 連接 tooAzure 虛擬網路 (VNet) 安全性規則的清單。 Nsg 可以是相關聯的 toosubnets，個別 Vm （傳統），或個別的網路介面 (NIC) 附加 tooVMs （資源管理員）。

當 NSG 相關聯的 tooa 子網路，hello 規則適用於 tooall 資源連線的 toohello 子網路。 流量可以進一步限制也關聯 NSG tooa VM 或 nic。

## <a name="security-and-continuous-compliance-with-organizational-standards"></a>符合組織標準的安全性及持續符合合規性

每個企業都有不同的需求，而每個企業都能透過雲端解決方案取得不同的好處。 儘管如此，所有種類的客戶預設具有 hello 移動 toohello 雲端相關的相同基本考量。 他們想要 tooretain 控制其資料，並希望同時維持透明度與相容性保持在安全和私用，該資料 toobe。

客戶想要從雲端提供者取得的是：

- **安全資料**時認可 hello 雲端可提供增加的資料安全性和系統管理控制，IT 領導者仍而言，移轉 toohello 雲端將會讓它們更容易遭受 toohackers 比其目前內部的解決方案。

- **資料私密性**：對企業來說，私人雲端服務也帶來了獨特的隱私問題。 當公司 toohello 雲端 toosave 查看基礎結構成本，並改善其彈性，它們也擔心會遺失其資料的儲存位置、 誰正在存取它，並取得使用方式的控制。

- **讓我們控制**即使它們利用 hello 雲端 toodeploy 更多的創新方案，公司是非常擔心會遺失其資料的控制權。 hello 最近揭露的政府機關存取客戶資料，透過法律及法務額外的方式，讓某些 Cio hello 雲端中儲存其資料時請小心。

- **升級透明度**雖然安全性、 隱私權和控制項很重要的 toobusiness 決策者，他們也想 hello 能力 tooindependently 確認其資料所儲存的方式，存取，以及受保護。

- **維護性**hello 複雜度及範圍標準出口法規之限制為公司展開雲端技術的使用，請繼續 tooevolve。 公司需要 tooknow 會符合其規範標準，及該相容性會發展為法規經過一段時間的變更。

## <a name="security-configuration-monitoring-and-alerting"></a>安全性設定，監視和警示

Azure 訂閱者可從多種裝置管理其雲端環境，這些裝置包括管理工作站、開發人員的電腦，甚至是具有工作專用權限的特殊權限使用者裝置。 在某些情況下，透過網頁型主控台，例如 hello Azure 入口網站執行管理功能。 在其他情況下，可能會從內部部署系統直接連線 tooAzure 透過虛擬私人網路 (Vpn)、 終端機服務、 用戶端應用程式通訊協定，或 （以程式設計的方式） hello Azure 服務管理 API (SMAPI)。 此外，用戶端端點也可以加入網域或是遭到隔離且不受管理，例如平板電腦或智慧型手機。

雖然多個存取和管理功能提供一組豐富的選項，但變化性可以加入極大的風險 tooa 雲端部署。 可能很難 toomanage，追蹤和稽核系統管理動作。 這些變化可能也會導入透過非法的存取 tooclient 端點，用來管理雲端服務的安全性威脅。 使用一般工作站或私人工作站來開發和管理基礎結構將會打開無法預期的威脅媒介，例如網頁瀏覽 (例如水坑攻擊) 或電子郵件 (例如社交工程和網路釣魚)。

監視、 記錄和稽核提供進行追蹤，以及了解管理活動，但它不一定可行 tooaudit 中的所有動作都完成到期 toohello 所產生的資料數量的詳細資料。 稽核的 hello 管理原則的 hello 效率是最佳作法，不過。

Azure 安全性控管，從 AD DS Gpo toocontrol 所有 hello 系統管理員 Windows 介面，如檔案共用。 將管理工作站納入稽核、監視和記錄程序內。 追蹤所有系統管理員和開發人員的存取和使用活動。

### <a name="azure-security-center"></a>Azure 資訊安全中心

hello [Azure 資訊安全中心](https://docs.microsoft.com/azure/security-center/security-center-intro)提供 hello 安全性狀態的 hello 訂閱中資源的中央檢視，並提供建議，協助防止遭盜用的資源。 它可以啟用更細微的原則 （例如，套用原則 toospecific 資源群組可讓它們可以明智地處理其對 toohello 風險 hello 企業 tootailor）。

![Azure 資訊安全中心](./media/governance-in-azure/security-governance-in-azure-fig7.png)

資訊安全中心能提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理，協助偵測原先可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。 啟用後[安全性原則](https://docs.microsoft.com/azure/security-center/security-center-policies)訂用帳戶的資源資訊安全中心會分析 hello 安全性資源 tooidentify 的潛在弱點的風險。 您可以立即取得網路組態的相關資訊。

Azure 資訊安全中心是針對 Azure 訂用帳戶內所有資源的最佳做法分析及安全性原則管理組合。 這項功能強大且容易 toouse 工具可讓安全性小組和風險人員 tooprevent，偵測，並回應 toosecurity 威脅，因為它會自動收集並分析從您的 Azure 資源、 hello 網路和協力廠商解決方案，例如安全性資料反惡意程式碼程式和防火牆。

此外，Azure 資訊安全中心適用於進階的分析，包括機器學習和行為分析，同時利用從 Microsoft 產品和服務，Microsoft 數位犯罪單元 (DCU)，hello hello Microsoft 通用的威脅情報Security Response Center (MSRC) 和外部的摘要。 [安全性控管](https://www.credera.com/blog/credera-site/azure-governance-part-4-other-tools-in-the-toolbox/)可廣泛套用在 hello 訂用帳戶層級或縮小 toospecific，套用的細微需求 tooindividual 透過原則定義的資源。

最後，Azure 資訊安全中心會分析這些原則為基礎的資源安全性健全狀況，並使用此 tooprovide 見解儀表板和警示的事件，例如惡意程式碼偵測或惡意的 IP 連線嘗試。

>[!Note]
> 如需有關如何 tooapply 建議事項，讀取[實作 Azure 資訊安全中心中的安全性建議](https://docs.microsoft.com/azure/security-center/security-center-recommendations)。

資訊安全中心會收集從虛擬機器 tooassess 其資訊安全狀態、 提供安全性建議事項，並警示您 toothreats。 當您第一次存取資訊安全中心時，訂用帳戶中的所有虛擬機器都會啟用資料收集。 建議使用資料收集，但您可以選擇不使用由[停用資料收集](https://docs.microsoft.com/azure/security-center/security-center-faq)hello 資訊安全中心原則中。

最後，Azure 資訊安全中心是開放式平台，可讓 Microsoft 夥伴和獨立軟體廠商 toocreate 軟體連接到 Azure 資訊安全中心 tooenhance 其功能。

Azure 資訊安全中心會監視下列 Azure 資源的 hello:

- 虛擬機器 (VM) (包括雲端服務)

- Azure 虛擬網路

- Azure SQL 服務

- 與您的 Azure 訂用帳戶整合的合作夥伴解決方案，例如位於 VM 和 [App Service 環境](https://docs.microsoft.com/azure/app-service/app-service-app-service-environments-readme)上的 Web 應用程式防火牆。

### <a name="operations-management-suite"></a>Operations Management Suite

hello OMS 軟體開發和服務小組的資訊安全和[控管程式](https://github.com/Microsoft/azure-docs/blob/master/articles/log-analytics/log-analytics-security.md)支援其商務需求，並依照遵守 toolaws 出口法規之限制[Microsoft Azure 信任中心](https://azure.microsoft.com/support/trust-center/)和[Microsoft 信任中心的相容性](https://www.microsoft.com/TrustCenter/Compliance/default.aspx)。 上述位置也會描述 OMS 是如何建立安全性需求、識別安全性控制，以及管理和監視風險。 每年我們都會檢閱原則、標準、程序和指導方針。

每個 OMS 開發小組成員都會獲得正式的應用程式安全性訓練。 在內部，我們使用版本控制系統來開發軟體。 每個軟體專案受到 hello 版本控制系統。

Microsoft 備有會監看及評估 Microsoft 中所有服務的安全性和法規遵循小組。 資訊安全人員組成 hello 小組，他們不會產生關聯以 hello 工程部門開發 OMS。 hello 安全人員具有自己管理鏈結，並進行獨立的產品和服務 tooensure 安全性與相容性評估。

Operations Management Suite (也稱為 OMS) 是從 hello 開始 hello 雲端中所設計的管理服務的集合。 與其部署及管理內部部署資源，OMS 元件會完全裝載於 Azure 中。 需要進行的設定很少，您可以在幾分鐘內完成啟動並執行。

![Operations Manager Suite](./media/governance-in-azure/security-governance-in-azure-fig8.png)

只是因為執行的 OMS 服務並不表示 hello 雲端，無法有效地管理您的內部部署環境。

將代理程式放在任何 Windows 或 Linux 電腦，您的資料中心，並將傳送資料 tooLog 分析，以及其他所有資料分析會收集從雲端或內部部署服務。 使用 Azure Backup 和 Azure Site Recovery tooleverage hello 雲端備份和高可用性的內部部署資源。

Hello 雲端中的 Runbook 通常無法存取您的內部部署資源，但您可以在一個或多部電腦上安裝代理程式太將要裝載您的資料中心中的 runbook。 當您啟動 runbook 時，您只指定您要讓 toorun hello 雲端或在本機的背景工作上。

OMS hello 核心功能是由一組在 Azure 中執行的服務提供。 每個服務提供特定的管理功能，以及您可以結合服務 tooachieve 不同管理案例。

![Operations Manager Suite](./media/governance-in-azure/security-governance-in-azure-fig9.JPG)

Azure Operation Manager 會透過提供管理解決方案來延伸其功能性。 [管理解決方案](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions)是預先封裝的邏輯集合，會實作能運用一或多項 OMS 服務的管理案例。

![Azure 作業管理](./media/governance-in-azure/security-governance-in-azure-fig10.png)

從 Microsoft 和協力廠商，您可以在 OMS 中輕鬆地加入您的投資 tooyour Azure 訂用帳戶 tooincrease hello 值可使用不同的解決方案。

身為合作夥伴，您可以建立您自己的解決方案 toosupport 應用程式和服務，並提供給他們 toousers 透過 hello Azure Marketplace 或快速啟動範本。

## <a name="performance-alerting-and-monitoring"></a>效能警示和監視

### <a name="alerting"></a>警示

警示是監視 Azure 資源度量、事件或記錄，並在您所指定條件符合時的通知方法。

**不同 Azure 服務中的警示**

警示可跨不同的服務使用，包括：

- Application Insights：允許 Web 測試及計量警示。

>[!Note]
> 請參閱 [ Application Insights 中設定警示](https://docs.microsoft.com/azure/application-insights/app-insights-alerts)和[監視任何網站的可用性和回應性](https://docs.microsoft.com/azure/application-insights/app-insights-monitor-web-app-availability)。

- 記錄分析 (Operations Management Suite): 可讓活動與診斷記錄檔 tooLog 分析 hello 路由傳送。 Operations Management Suite 可允許度量、記錄和其他警示類型。

>[!Note]
> 如需詳細資訊，請參閱 [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-alerts) 中的＜警示＞。

- Azure 監視器：允許根據計量值和活動記錄檔事件的警示。 您可以使用 hello [Azure 監視 REST API](https://msdn.microsoft.com/library/dn931943.aspx) toomanage 警示。

>[!Note]
> 如需詳細資訊，請參閱[使用 hello Azure 入口網站、 PowerShell 或 hello 命令列介面 toocreate 警示](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-alerts-portal)。

### <a name="monitoring"></a>監視

您雲端應用程式中的效能問題可能會對企業產生影響。 透過多個互連的元件和頻繁的發行，隨時都可能導致效能降低。 此外，如果您正在開發應用程式，您的使用者通常會找出測試時未發現的問題。 您應該立即，這些問題的相關資訊，並已進行診斷與修正 hello 問題的工具。 Microsoft Azure 提供多種工具來識別這些問題。

**如何監視我的 Azure 雲端應用程式？**

有多種工具可用來監視 Azure 應用程式和服務。 其中有些功能會重疊。 這是部分原因歷程記錄和部分到期 toohello 模糊開發和作業的應用程式之間。

以下是 hello 主要工具：

- **Azure 監視器**是用以監視 Azure 上執行之服務的基本工具。 它會提供您相關的服務，且周圍環境的 hello hello 輸送量的基礎結構層級資料。 如果您要管理您的應用程式在 Azure 中，決定是否 tooscale 向上或向下的資源，然後 Azure 監視器可讓您使用什麼 toostart。

- **Application Insights** 可用來開發，並作為監視生產環境的解決方案。 它的運作方式是將套件安裝到您的應用程式，因此可讓您更深入檢視內部情形。 它的資料包括相依性的回應時間、例外狀況追蹤、偵錯快照集、執行設定檔。 它提供功能強大的智慧工具來分析所有此遙測這兩個 toohelp 您偵錯應用程式和 toohelp 您了解使用者與它的行為。 您可以分辨是否突然增加回應時間是因為 toosomething 中應用程式或某些外部 resourcing 問題。 如果您使用 Visual Studio hello 應用程式有問題，您可以採取右 toohello 問題行程式碼，您可以修正此問題。

- **記錄分析**適用於需要 tootune 在生產環境中執行的應用程式的效能和計畫維護。 它是 Azure 中的基本工具。 它會收集，並從多個來源、 彙總資料，但仍有延遲 10 too15 分鐘的時間。 它會針對 Azure、內部部署及協力廠商的雲端式基礎結構 (例如 Amazon Web 服務) 提供整體 IT 管理解決方案。 它提供更豐富的工具 tooanalyze 資料跨多個來源、 跨所有記錄檔，讓複雜的查詢和上指定的條件可以主動警示。 您甚至可以將自訂資料收集到其中央存放庫，如此便能查詢並將其視覺化。

- **System Center Operations Manager (SCOM)** 可用來管理及監視大型雲端安裝。 您可能已經熟悉它做為適用於內部部署 Windows Sever 和 Hyper-V 型雲端的管理工具，但它也可以與 Azure 應用程式整合並加以管理。 在其他方面，它可以在現有的即時應用程式上安裝 Application Insights。 如果應用程式當機，它會在短時間內通知您。


## <a name="next-steps"></a>後續步驟

- [建立 Azure Resource Manager 範本的最佳做法](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices)。

- [實作 Azure 訂用帳戶治理的範例](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-subscription-examples)。

- [Microsoft Azure Government](https://docs.microsoft.com/azure/azure-government/) \(英文\)。
