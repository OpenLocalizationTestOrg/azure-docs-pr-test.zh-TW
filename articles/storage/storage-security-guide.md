---
title: "aaaAzure 儲存安全性指南 |Microsoft 文件"
description: "詳細資料 hello 許多方法保護 Azure 儲存體，包括但不是限於的 tooRBAC、 儲存體服務加密、 用戶端加密、 SMB 3.0 和 Azure 磁碟加密。"
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 6f931d94-ef5a-44c6-b1d9-8a3c9c327fb2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: d406ff0d6b45c6107d0276ad9e65c331078ce792
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-guide"></a>Azure 儲存體安全性指南
## <a name="overview"></a>概觀
Azure 儲存體提供一組完整的安全性功能，同時讓開發人員 toobuild 安全的應用程式。 可以使用角色型存取控制與 Azure Active Directory 來保護本身的 hello 儲存體帳戶。 您可以使用[用戶端加密](storage-client-side-encryption.md)、HTTPS 或 SMB 3.0，在應用程式和 Azure 之間進行傳輸時保護資料的安全。 資料可以設定自動加密時寫入 toobe tooAzure 儲存體使用[儲存體服務加密 (SSE)](storage-service-encryption.md)。 虛擬機器所使用的作業系統和資料磁碟可以設定使用加密的 toobe [Azure 磁碟加密](../security/azure-security-disk-encryption.md)。 Azure 儲存體中的委派的存取 toohello 資料物件可以被授與使用[共用存取簽章](storage-dotnet-shared-access-signature-part-1.md)。

本文將提供這其中每個可搭配 Azure 儲存體使用的安全性功能概觀。 會提供連結，以提供每項功能的詳細資料，因此您可以輕鬆地執行 tooarticles 進一步調查每個主題上的。

以下是本文章涵蓋 hello 主題 toobe:

* [管理平面安全性](#management-plane-security) – 保護儲存體帳戶

  hello 管理平面 hello 使用資源 toomanage 包含儲存體帳戶。 在本節中，我們將討論 hello Azure Resource Manager 部署模型和 toouse 角色型存取控制 (RBAC) toocontrol tooyour 儲存體帳戶的存取方式。 我們也會討論管理儲存體帳戶金鑰以及如何 tooregenerate 它們。
* [平面的資料安全性](#data-plane-security)– 保護存取 tooYour 資料

  在本節中，我們將查看允許存取 toohello 實際的資料物件，在儲存體帳戶，例如 blob、 檔案、 佇列和資料表，使用共用存取簽章和預存存取原則。 我們將涵蓋服務層級的 SAS 和帳戶層級的 SAS。 我們也會看到如何 toolimit 存取 tooa 特定 IP 位址 （或 IP 位址範圍）、 toolimit hello 通訊協定使用 tooHTTPS，以及如何不需等到它的共用存取簽章 toorevoke tooexpire。
* [傳輸中加密](#encryption-in-transit)

  本章節將討論如何 toosecure 資料時可以傳送傳入或傳出 Azure 儲存體。 我們將討論建議使用 HTTPS 和 hello 加密使用 Azure 檔案共用的 SMB 3.0 的 hello。 我們也將看看用戶端加密，可讓您 tooencrypt hello 資料傳輸到儲存體用戶端應用程式之前和 toodecrypt hello 資料超出儲存體傳輸後。
* [待用加密](#encryption-at-rest)

  我們會討論儲存體服務加密 (SSE) 中，和如何加以啟用儲存體帳戶，導致您的區塊 blob，分頁 blob，並附加寫入 tooAzure 存放裝置時自動加密的 blob。 我們也將探討如何使用 Azure 磁碟加密，並瀏覽 hello 基本差異和與用戶端加密與 SSE 磁碟加密的情況。 我們將簡短探討美國政府電腦適用的 FIPS 相符性。
* 使用[儲存體分析](#storage-analytics)tooaudit 存取 Azure 儲存體

  本節討論如何 toofind 在 hello 儲存體分析記錄檔資訊的要求。 我們會查看實際的儲存體分析記錄資料，請參閱如何 toodiscern 是否與提出要求 hello 儲存體帳戶金鑰，以共用存取簽章，或以匿名方式，以及是否成功或失敗。
* [使用 CORS 啟用以瀏覽器為基礎的用戶端](#Cross-Origin-Resource-Sharing-CORS)

  本節討論如何 tooallow 跨原始資源共用 (CORS)。 我們將討論跨網域存取，以及如何 toohandle 它 hello CORS 功能內建到 Azure 儲存體。

## <a name="management-plane-security"></a>管理平面安全性
hello 管理平面包含會影響本身 hello 儲存體帳戶的作業。 例如，您可以建立或刪除儲存體帳戶、 訂用帳戶中取得的儲存體帳戶清單、 擷取 hello 儲存體帳戶金鑰，或重新產生 hello 儲存體帳戶金鑰。

當您建立新的儲存體帳戶時，可以選取傳統或資源管理員的部署模型。 在 Azure 中建立資源的 hello 傳統模式只允許想到存取 toohello 訂用帳戶和依次 hello 儲存體帳戶。

此指南著重於 hello 資源管理員模型，這是建議的方式來建立儲存體帳戶的 hello。 與 hello 資源管理員的儲存體帳戶，而不提供存取 toohello 整個訂用帳戶，您可以控制更有限的層級 toohello 管理平面，使用角色型存取控制 (RBAC) 上的存取。

### <a name="how-toosecure-your-storage-account-with-role-based-access-control-rbac"></a>如何 toosecure 您的儲存體帳戶使用角色型存取控制 (RBAC)
讓我們討論何謂 RBAC 及使用方式。 每一個 Azure 訂用帳戶都具有 Azure Active Directory。 使用者、 群組和從該目錄的應用程式可以被授與存取 toomanage hello Azure 訂用帳戶中的使用資源 hello Resource Manager 部署模型。 這是參考的 tooas 角色型存取控制 (RBAC)。 toomanage 這存取，您可以使用 hello [Azure 入口網站](https://portal.azure.com/)，hello [Azure CLI 工具](../cli-install-nodejs.md)， [PowerShell](/powershell/azureps-cmdlets-docs)，或使用 hello [Azure 儲存體資源提供者 REST Api](https://msdn.microsoft.com/library/azure/mt163683.aspx).

使用 hello 資源管理員模型時，您可以將 hello 儲存體帳戶資源群組和控制存取 toohello 管理平面中的該特定的儲存體帳戶，使用 Azure Active Directory。 例如，您可以提供特定使用者 hello 能力 tooaccess hello 儲存體帳戶金鑰，而其他使用者可以檢視 hello 儲存體帳戶資訊，但無法存取 hello 儲存體帳戶金鑰。

#### <a name="granting-access"></a>授與存取權
指派適當 RBAC 角色 toousers hello、 群組和應用程式，在 hello 權限範圍授與的存取。 toogrant 存取 toohello 整個訂用帳戶，您可以指派 hello 訂用帳戶層級角色。 您可以授與權限本身 toohello 資源群組來授與存取 tooall 的資源群組中的 hello 資源。 您也可以指派特定的角色 toospecific 資源，例如儲存體帳戶。

以下是您需要有關使用 RBAC tooaccess hello Azure 儲存體帳戶的管理作業 tooknow hello 重點：

* 當您指派存取權時，您基本上會指派您想要 toohave 存取角色 toohello 帳戶。 您可以控制存取 toohello 作業使用 toomanage 該儲存體帳戶，但不是 toohello 資料 hello 帳戶中的物件。 例如，您可以授與權限 tooretrieve hello 屬性 hello 儲存體帳戶 （例如備援），但非 tooa 容器或 Blob 儲存體中的容器中的資料。
* 有人 toohave 權限 tooaccess hello hello 儲存體帳戶中的資料物件，提供權限 tooread hello 儲存體帳戶金鑰，該使用者可以接著使用這些金鑰 tooaccess hello blob、 佇列、 表格和檔案。
* 角色可以指派 tooa 特定使用者帳戶、 使用者或 tooa 特定應用程式的群組。
* 每個角色都有「動作」與「沒有動作」清單。 比方說，hello 虛擬機器參與者角色具有 「 Listkey"的動作，可讓 hello 儲存體帳戶金鑰 toobe 讀取。 hello 參與者有 [沒有動作]，例如更新 hello hello Active Directory 中使用者的存取權。
* 儲存體的角色包括 （但不限於） 下列 hello:

  * 擁有者 – 他們可以管理一切，包括存取權。
  * 參與者-它們可以執行任何動作 hello 擁有者可以執行除了指派存取權。 擁有此角色的使用者可檢視及重新產生 hello 儲存體帳戶金鑰。 與 hello 儲存體帳戶金鑰，就可以存取 hello 資料物件。
  * 讀取者-它們可以檢視 hello 儲存體帳戶，但機密資料的相關資訊。 例如，如果您指派 hello 儲存體帳戶 toosomeone 上的讀取器權限的角色，他們可以檢視 hello hello 儲存體帳戶內容，但是它們無法 toohello 屬性進行任何變更或檢視 hello 儲存體帳戶金鑰。
  * 儲存體帳戶參與者 – 他們可以管理 hello 儲存體帳戶 – 他們可以讀取 hello 訂用帳戶的資源群組和資源，以及建立和管理訂用帳戶資源群組部署。 它們也可以存取 hello 儲存體帳戶金鑰 」，而表示他們可以存取 hello 資料平面。
  * 使用者存取系統管理員 – 他們可以管理使用者存取 toohello 儲存體帳戶。 例如，他們可以授與讀取器存取 tooa 特定使用者。
  * 虛擬機器參與者 – 他們可以管理虛擬機器，但不是 hello 儲存體帳戶 toowhich 它們連線。 這個角色可以列出 hello 儲存體帳戶金鑰，表示 hello 指派這個角色的使用者 toowhom 可以更新 hello 資料平面。

    為了讓使用者 toocreate 虛擬機器，它們有 toobe 無法 toocreate hello 對應 VHD 檔案儲存體帳戶中。 toodo，他們需要 toobe 無法 tooretrieve hello 儲存體帳戶金鑰，並將它傳遞 toohello 應用程式開發介面建立 hello VM。 因此，它們必須有此權限，讓它們可以列出 hello 儲存體帳戶金鑰。
* hello 能力 toodefine 自訂角色是可讓您 toocompose 清單中的動作可以在 Azure 資源執行的可用動作的一組功能。
* hello 使用者擁有 toobe 之前您可以指派角色 toothem 需要設定您的 Azure Active Directory 中。
* 您可以建立報表的人員授與/撤銷的存取權，或從其，而且在使用 PowerShell 哪些 scope 種類或 hello Azure CLI。

#### <a name="resources"></a>資源
* [Azure Active Directory 角色型存取控制](../active-directory/role-based-access-control-configure.md)

  這篇文章說明 hello Azure Active Directory 角色型存取控制和其運作方式。
* [RBAC：內建角色](../active-directory/role-based-access-built-in-roles.md)

  這篇文章會說明所有 hello 中 RBAC 中可用的內建角色。
* [了解資源管理員部署和傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)

  本文說明 hello 資源管理員部署和傳統部署模型，並說明使用 hello 資源管理員和資源群組的 hello 好處。 它說明 hello Azure 計算、 網路和存放裝置提供者在 hello 資源管理員模式下運作的方式。
* [管理角色型存取控制以 hello REST API](../active-directory/role-based-access-control-manage-access-rest.md)

  本文將說明如何 toouse hello REST API toomanage RBAC。
* [Azure 儲存體資源提供者 REST API 參考](https://msdn.microsoft.com/library/azure/mt163683.aspx)

  這是您可以使用 Api toomanage 儲存體帳戶以程式設計方式 hello 的 hello 參考。
* [使用 Azure 資源管理員 API 的開發人員指南 tooauth](http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/)

  本文示範如何使用 tooauthenticate hello 資源管理員 Api。
* [來自Ignite 且適用於 Microsoft Azure 的角色型存取控制](https://channel9.msdn.com/events/Ignite/2015/BRK2707)

  這是連結 tooa 大會 hello 2015 MS Ignite 影片在 Channel 9 上。 在此工作階段，它們討論存取管理和報告功能，在 Azure 中，並瀏覽保護存取 tooAzure 訂用帳戶使用 Azure Active Directory 的最佳作法。

### <a name="managing-your-storage-account-keys"></a>管理儲存體帳戶金鑰
索引鍵是由 Azure 建立的以及 hello 儲存體帳戶名稱，512 位元字串的儲存體帳戶可以是使用的 tooaccess hello 資料物件儲存在 hello 儲存體帳戶，例如 blob、 資料表、 佇列訊息，以及 Azure 檔案共用上的檔案內的實體。 控制存取 toohello 儲存體帳戶金鑰控制存取該儲存體帳戶的 toohello 資料平面。

每個儲存體帳戶有兩個索引鍵參考 tooas 「 索引鍵 1 」 和 「 索引鍵 2 」 中 hello [Azure 入口網站](http://portal.azure.com/)在 hello PowerShell cmdlet。 這些可以使用其中一種方法，包括但不是限於的 toousing hello 以手動方式重新產生[Azure 入口網站](https://portal.azure.com/)，PowerShell、 hello Azure CLI，或以程式設計方式使用 hello.NET 儲存體用戶端程式庫或 hello Azure儲存體服務 REST API。

有任意數目的理由 tooregenerate 儲存體帳戶金鑰。

* 您可能會基於安全性理由定期重新產生它們。
* 如果某人 toohack 管理的應用程式，並擷取已硬式編碼，或儲存在組態檔中的 hello 金鑰授與完整存取 tooyour 儲存體帳戶，就會重新產生儲存體帳戶金鑰。
* 如果您的小組使用的儲存體總管應用程式，會保留 hello 儲存體帳戶金鑰，而其中 hello 小組成員會保留另一種情況的金鑰重新產生。 hello 應用程式會繼續 toowork，提供他們存取 tooyour 儲存體帳戶之後它們消失。 這是實際 hello 主要原因建立這些帳戶層級共用存取簽章 – 您可以使用帳戶層級 SA，而不是儲存在組態檔中的 hello 便捷鍵。

#### <a name="key-regeneration-plan"></a>金鑰重新產生計畫
您不希望您使用沒有一些規劃 toojust hello 重新產生金鑰。 如果您這樣做，您無法剪下關閉所有存取 toothat 儲存體帳戶，這樣可能會導致主要中斷。 這就是為什麼要有兩個金鑰。 您一次應該重新產生一個金鑰。

重新產生金鑰之前，先確定您有一份所有應用程式相依於 hello 儲存體帳戶，以及您在 Azure 中使用的其他服務。 例如，如果您使用 Azure Media Services 相依於儲存體帳戶，您必須重新同步處理 hello 存取金鑰與媒體服務之後您重新產生 hello 金鑰。 如果您使用任何儲存體總管之類的應用程式，您將需要 tooprovide hello 新金鑰 toothose 應用程式以及。 請注意，是否您有的 Vm 的 VHD 檔案會儲存在 hello 儲存體帳戶時，它們將不會受到重新產生 hello 儲存體帳戶金鑰。

您可以重新產生您 hello Azure 入口網站中的索引鍵。 一旦重新產生金鑰會佔用 too10 跨儲存體服務的分鐘 toobe 同步處理。

當您準備好時，這裡是 hello 一般程序詳述如何，您應該變更您的金鑰。 在此情況下，hello 假設是您目前使用索引鍵 1，而且要 toochange 的所有項目 toouse 改為索引鍵 2。

1. 重新產生金鑰 2 tooensure 很安全。 您可以在 hello Azure 入口網站中。
2. 在所有儲存 hello 儲存體金鑰的 hello 應用程式中，變更 hello 儲存體金鑰 toouse 索引鍵 2 的新值。 測試並發行 hello 應用程式。
3. 在所有的 hello 應用程式和服務都已啟動並執行成功，重新產生金鑰 1。 如此可確保任何人都將不再有 toowhom 您未明確提供 hello 新的金鑰存取 toohello 儲存體帳戶。

如果您目前使用索引鍵 2，您可以使用相同的處理序，但是反向 hello 索引鍵名稱的 hello。

您可以移轉在幾天，透過變更每個應用程式 toouse hello 新金鑰並將它發行。 它們全部完成之後，您應該也要返回並重新產生 hello 舊金鑰，讓它無法再運作。

另一個選項是 tooput hello 儲存體帳戶金鑰[Azure 金鑰保存庫](https://azure.microsoft.com/services/key-vault/)做為密碼，而且您的應用程式擷取 hello 索引鍵那里。 然後當您重新產生 hello 金鑰並更新 hello Azure 金鑰保存庫，hello 應用程式將不會需要 toobe 重新部署，因為它們會自動挑選 hello hello Azure 金鑰保存庫中的新金鑰。 請注意，您可以擁有 hello 應用程式讀取 hello 機碼每次需要它，或您可以在記憶體中快取和它失敗時使用它，如果擷取 hello 金鑰一次 hello Azure 金鑰保存庫。

使用 Azure 金鑰保存庫，也會增加儲存體金鑰的安全性層級。 如果您使用這個方法時，您將不必 hello 儲存體金鑰的硬式編碼組態檔中，會移除該途徑的人取得存取 toohello 金鑰沒有特定的權限。

使用 Azure 金鑰保存庫的另一個優點是您也可以控制使用 Azure Active Directory 存取 tooyour 金鑰。 這表示您可以授與存取 toohello 少數需要 tooretrieve hello 索引鍵，從 Azure 金鑰保存庫，且熟悉的其他應用程式，將不會無法 tooaccess hello 機碼，不必授與他們權限特別的應用程式。

注意： 建議 toouse 僅 hello 的其中一個索引鍵中的所有應用程式在 hello 相同的時間。 如果您使用某些地方的索引鍵 1 與索引鍵 2 的其他人，您將不會無法 toorotate 您的金鑰，而不讓您無法存取某些應用程式。

#### <a name="resources"></a>資源
* [關於 Azure 儲存體帳戶](storage-create-storage-account.md#regenerate-storage-access-keys)

  本文提供儲存體帳戶的概觀，並討論如何檢視、複製和重新產生儲存體存取金鑰。
* [Azure 儲存體資源提供者 REST API 參考](https://msdn.microsoft.com/library/mt163683.aspx)

  本文章包含有關擷取 hello 儲存體帳戶金鑰和重新產生 hello 儲存體帳戶金鑰的連結 toospecific 文件使用 hello REST API 的 Azure 帳戶。 注意︰這適用於 Resource Manager 儲存體帳戶。
* [儲存體帳戶的相關作業](https://msdn.microsoft.com/library/ee460790.aspx)

  在 hello 儲存體服務管理員 REST API 參考本文章包含連結 toospecific 發行項上擷取和重新產生 hello 使用 hello REST API 的儲存體帳戶金鑰。 注意： 這是 hello 傳統儲存體帳戶。
* [說再見 tookey 管理 – 管理使用 Azure AD 存取 tooAzure 儲存體資料](http://www.dushyantgill.com/blog/2015/04/26/say-goodbye-to-key-management-manage-access-to-azure-storage-data-using-azure-ad/)

  本文將說明如何 toouse Active Directory toocontrol 存取 tooyour Azure 金鑰保存庫中的 Azure 儲存體金鑰。 它也會示範如何 toouse Azure 自動化作業每小時 tooregenerate hello 索引鍵。

## <a name="data-plane-security"></a>資料平面安全性
平面的資料安全性是指 toohello 方法使用的 toosecure hello 資料物件儲存在 Azure 儲存體 – hello blob、 佇列、 表格和檔案。 我們已看到方法 tooencrypt hello 資料和安全性的 hello 資料傳輸期間，但您移有關 toohello 物件允許存取嗎？

基本上有兩種方法來控制存取 toohello 的資料物件本身。 hello 第一個是由控制存取 toohello 儲存體帳戶金鑰，且 hello 第二個使用共用存取簽章 toogrant 存取 toospecific 資料物件的一段特定時間。

一個例外狀況 toonote 是您可以藉由設定 hello 據以保留 hello blob 的 hello 容器的存取層級允許公用存取 tooyour blob。 如果您設定容器 tooBlob 或容器的存取權時，它會允許對該容器中的 hello blob 的公開讀取權限。 這表示具有 URL 指向 tooa blob 容器中的任何人都可以在瀏覽器中開啟它，而不需要使用共用存取簽章，或必須要有 hello 儲存體帳戶金鑰。

### <a name="storage-account-keys"></a>儲存體帳戶金鑰
儲存體帳戶金鑰是由 Azure 的 hello 儲存體帳戶名稱，以及可以是使用的 tooaccess hello 資料儲存物件 hello 儲存體帳戶中建立的 512 位元字串。

例如，您可以讀取 blob，撰寫 tooqueues、 建立資料表，和修改檔案。 許多這些動作可以透過 hello Azure 入口網站，或使用許多儲存體總管應用程式的其中一個。 您也可以撰寫程式碼 toouse hello REST API 或其中一個 hello 儲存體用戶端程式庫 tooperform 這些作業。

因為在 hello hello 章節中討論[管理平面安全性](#management-plane-security)的傳統儲存體帳戶可授與完整存取 toohello Azure 訂用帳戶中，提供存取 toohello 儲存體金鑰。 使用 hello Azure Resource Manager 模型的儲存體帳戶存取 toohello 儲存體金鑰可以由角色型存取控制 (RBAC)。

### <a name="how-toodelegate-access-tooobjects-in-your-account-using-shared-access-signatures-and-stored-access-policies"></a>Toodelegate 存取 tooobjects 帳戶使用共用存取簽章和預存存取原則中的方式
共用存取簽章是字串，包含可能是安全性權杖附加 tooa toodelegate 存取 toostorage 物件可讓您的 URI，並指定條件約束，例如 hello 權限和存取 hello 日期/時間範圍。

您可以授與存取 tooblobs、 容器、 佇列訊息、 檔案和資料表。 資料表中，您可以實際授與權限 tooaccess 某個範圍的 hello 資料表中的實體藉由指定 hello 磁碟分割和資料列的索引鍵範圍 toowhich 想 hello 使用者 toohave 存取權。 例如，如果您有資料分割索引鍵為地理狀態儲存的資料，您可以讓某人存取 toojust hello 資料加州的。

在另一個範例中，您可能會提供 web 應用程式，讓它 toowrite 項目 tooa 佇列 SAS 權杖，並提供背景工作角色應用程式從 hello SAS 權杖 tooget 訊息排入佇列，並進行處理。 或者，您可以讓一位客戶可以使用 tooupload 圖片 tooa 容器中 Blob 儲存體，並為這些圖片提供 web 應用程式的權限 tooread SAS 權杖。 在這兩種情況下，沒有的重要性分離 – 每個應用程式可以指定只 hello 存取它們需要在排序 tooperform 其工作。 這是透過 hello 使用共用存取簽章。

#### <a name="why-you-want-toouse-shared-access-signatures"></a>為什麼要 toouse 共用存取簽章
為什麼需要 toouse SA，而不是只提供儲存體帳戶金鑰，也就是這麼多容易？ 釋出儲存體帳戶金鑰，就像是共用儲存體 kingdom hello 索引鍵。 它會授與完整存取權限。 其他使用者無法使用您的金鑰，並上傳其整個音樂媒體櫃 tooyour 儲存體帳戶。 他們可能也會使用受病毒感染的版本來取代您的檔案或竊取您的資料。 提供無限制的存取 tooyour 儲存體帳戶是應該不能草率的事物。

搭配共用存取簽章，您可以提供用戶端只需要有限的時間內的 hello 權限。 例如，如果有人已上傳 blob tooyour 帳戶，您可以授與他們 （當然，取決於 hello hello blob 大小） 剛好足夠時間 tooupload hello blob 的寫入權限。 如果您改變心意，您可以撤銷該存取權。

此外，您可以指定使用 SAS 所提出的要求會限制的 tooa 特定 IP 位址或 IP 位址範圍外部 tooAzure。 您也可以要求使用特定通訊協定 (HTTPS 或 HTTP/HTTPS) 來提出要求。 這表示如果您只想 tooallow HTTPS 流量，您可以設定所需的 hello 通訊協定 tooHTTPS，而 HTTP 流量將會封鎖。

#### <a name="definition-of-a-shared-access-signature"></a>定義共用存取簽章
共用存取簽章是一組查詢參數附加 toohello URL 指向 hello 資源

提供資訊 hello 存取允許與 hello 的哪些 hello 允許存取的時間長度。 以下是範例。這個 URI 會提供五分鐘的讀取權限 tooa blob。 請注意，SAS 查詢參數必須以 URL 編碼，例如 %3A 用於冒號 (:) 或 %20 用於空格。

```
http://mystorage.blob.core.windows.net/mycontainer/myblob.txt (URL toohello blob)
?sv=2015-04-05 (storage service version)
&st=2015-12-10T22%3A18%3A26Z (start time, in UTC time and URL encoded)
&se=2015-12-10T22%3A23%3A26Z (end time, in UTC time and URL encoded)
&sr=b (resource is a blob)
&sp=r (read access)
&sip=168.1.5.60-168.1.5.70 (requests can only come from this range of IP addresses)
&spr=https (only allow HTTPS requests)
&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D (signature used for hello authentication of hello SAS)
```

#### <a name="how-hello-shared-access-signature-is-authenticated-by-hello-azure-storage-service"></a>共用存取簽章驗證的 hello hello Azure 儲存體服務的方式
Hello 儲存體服務收到 hello 要求時，它會採用 hello 輸入的查詢參數，並建立簽章使用 hello 相同的方法，如 hello 呼叫端程式。 然後，它會比較兩個簽章 hello。 如果他們同意，則請 hello 儲存體服務可以檢查 hello 儲存體服務版本 toomake 確認它有效、 確認 hello 目前的日期和時間設定 hello 指定視窗內，請要求確定 hello 存取對應等 toohello 所提出的要求。

比方說，我們上述 url 中，如果 hello URL 指向 tooa 檔案，而不是 blob，此要求會失敗，因為它會指定 blob 的共用存取簽章是該 hello。 如果 hello REST 呼叫的命令是 tooupdate blob，它會失敗，因為 hello 共用存取簽章卻指定只有讀取權限允許的。

#### <a name="types-of-shared-access-signatures"></a>共用存取簽章的類型
* 服務層級 SAS 可以是使用的 tooaccess 儲存體帳戶中的特定資源。 一些範例要擷取的容器中的 blob 清單、 下載 blob，更新資料表中的實體、 加入訊息 tooa 佇列或上傳檔案 tooa 檔案共用。
* 帳戶層級 SAS 可以是使用的 tooaccess 任何項目可以用於服務層級 SAS。 此外，它可以提供給服務層級 SAS，例如 hello 能力 toocreate 容器、 資料表、 佇列和檔案共用不允許的選項 tooresources。 您也可以指定存取 toomultiple 服務一次。 例如，您可能會提供給該人員存取 tooboth blob 和檔案儲存體帳戶中。

#### <a name="creating-an-sas-uri"></a>建立 SAS URI
1. 您可以視需要建立臨機操作的 URI，定義所有 hello 查詢參數的每一次。

   這真的很有彈性，但如果您每次都有一組類似的邏輯參數，使用預存存取原則會是個不錯的做法。
2. 您可以針對整個容器、檔案共用、表格或佇列建立預存存取原則。 然後您可以使用它作為 hello hello 您所建立的 SAS Uri。 您可以輕鬆地撤銷以預存存取原則為基礎的權限。 您可以向上 too5 原則定義在每個容器、 佇列、 資料表或檔案共用上。

   比方說，如果您要 toohave 許多人讀取特定容器中的 hello blob、 您可以建立預存存取原則，指出 「 請提供讀取權限 」 和任何其他設定會 hello 相同每次。 然後您可以建立使用 hello hello 預存存取原則設定，並指定到期日期/時間 hello SAS URI。 hello 利用這是您沒有 toospecify 所有 hello 每次查詢參數。

#### <a name="revocation"></a>撤銷
假設您的 SAS 已遭洩漏，或者您想 toochange 它因為公司的安全性或法規遵循需求。 您要如何撤銷存取 tooa 資源使用該 SAS？ 這取決於您要建立 hello SAS URI 的方式。

如果您使用臨機操作的 URI，會有三個選項。 您可以發出短的到期原則 SAS 權杖，並只需等候 hello SAS tooexpire。 您可以重新命名或刪除 hello 資源 （假設 hello 語彙基元為已設定領域的 tooa 單一物件）。 您可以變更 hello 儲存體帳戶金鑰。 這最後一個選項有很大的影響，視多少服務使用該儲存體帳戶，並可能不是您想 toodo 不某些計畫。

如果您使用 SAS，衍生自預存存取原則，您可以移除存取權撤銷 hello 預存存取原則-只可以變更它，因此已過期，或完全移除它。 這會立即生效，並使每個使用該預存存取原則建立的 SAS 失效。 更新或移除 hello 預存存取原則，可能會影響使用者存取該特定容器、 檔案共用、 資料表或佇列透過 SAS，但如果 hello 用戶端會寫入，因此他們要求新的 SAS hello 舊變成無效時，這將可以正常運作。

因為使用 SAS，衍生自預存存取原則讓您 hello 能力 toorevoke SAS 立即，它是 hello 建議的最佳作法 tooalways 使用盡可能，預存存取原則。

#### <a name="resources"></a>資源
如需詳細資訊，使用共用存取簽章和預存存取原則，完整的範例，請參閱下列文章 toohello:

* 這些是 hello 的參考文件。

  * [服務 SAS](https://msdn.microsoft.com/library/dn140256.aspx)

    本文提供使用服務層級 SAS 搭配 Blob、佇列、表格範圍及檔案的範例。
  * [建構服務 SAS](https://msdn.microsoft.com/library/dn140255.aspx)
  * [建構帳戶 SAS](https://msdn.microsoft.com/library/mt584140.aspx)
* 這些是使用 hello.NET 用戶端程式庫 toocreate 共用存取簽章和預存存取原則的教學課程。

  * [使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md)
  * [共用存取簽章，第 2 部分： 建立和使用以 hello Blob 服務 SAS](storage-dotnet-shared-access-signature-part-2.md)

    這篇文章包含 hello SAS 模型、 共用存取簽章的範例的說明，hello 最佳作法建議使用的 SAS。 也將討論是 hello 撤銷的 hello 授與的權限。
* 依 IP 位址 (IP ACL) 限制存取

  * [什麼是端點存取控制清單 (ACL)？](../virtual-network/virtual-networks-acl.md)
  * [建構服務 SAS](https://msdn.microsoft.com/library/azure/dn140255.aspx)

    這是用於服務層級 SAS; hello 參考文件它包含的範例 IP 執行 Acl。
  * [建構帳戶 SAS](https://msdn.microsoft.com/library/azure/mt584140.aspx)

    這是針對帳戶層級 SAS; hello 參考文件它包含的範例 IP 執行 Acl。
* 驗證

  * [Hello Azure 儲存體服務的驗證](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* 共用存取簽章入門教學課程

  * [SAS 入門教學課程](https://github.com/Azure-Samples/storage-dotnet-sas-getting-started)

## <a name="encryption-in-transit"></a>傳輸中加密
### <a name="transport-level-encryption--using-https"></a>Transport-Level Encryption – Using HTTPS
您應該採取的 Azure 儲存體資料 tooensure hello 安全性的另一個步驟是 tooencrypt hello hello 用戶端與 Azure 儲存體之間的資料。 hello 第一個建議的做法是 tooalways 使用 hello [HTTPS](https://en.wikipedia.org/wiki/HTTPS)通訊協定，可確保透過安全通訊 hello 公用網際網路。

toohave 安全通訊通道，您應該一律使用 HTTPS 呼叫 hello REST Api 或存取物件的儲存體中時。 此外，**共用存取簽章**，可能會使用的 toodelegate 存取 tooAzure 儲存物件，包含選項 toospecify 時使用共用存取簽章，如此可確保任何人都可以使用 HTTPS 通訊協定，只有 hello送出使用 SAS 權杖的連結，將會使用 hello 適當的通訊協定。

呼叫儲存體帳戶中的 hello REST Api tooaccess 物件，藉由啟用時，您可以強制使用 HTTPS hello[安全傳輸需要](storage-require-secure-transfer.md)hello 儲存體帳戶。 啟用此選項後，使用 HTTP 的連線將被拒絕。

### <a name="using-encryption-during-transit-with-azure-file-shares"></a>傳輸期間透過 Azure 檔案共用使用加密
Azure 檔案儲存體使用 hello REST API 時，支援 HTTPS，但已為 SMB 檔案共用附加 tooa VM 更常使用。 SMB 2.1 不支援加密，因此連線之內，才允許 hello 相同 Azure 中的區域。 不過，SMB 3.0 支援加密，和可在 Windows Server 2012 R2、 Windows 8、 Windows 8.1 和 Windows 10 中，允許跨區域存取甚至 hello 桌面上的存取。

請注意，雖然您可以使用 Azure 檔案共用，unix，hello Linux SMB 用戶端還不支援加密，因此只允許存取 Azure 的區域內。 適用於 Linux 的加密支援位於 hello 藍圖 Linux 開發人員負責 SMB 的功能。 當他們新增加密時，您會有 hello 相同的功能，以存取 Linux 上的 Azure 檔案共用的 Windows 一樣。

您可以強制 hello 使用加密 hello Azure 檔案服務與啟用[安全傳輸需要](storage-require-secure-transfer.md)hello 儲存體帳戶。 如果使用 hello REST Api，都需要 HTTPs。 針對 SMB，只有支援加密的 SMB 連線可以成功連線。

#### <a name="resources"></a>資源
* [如何 toouse Linux 的 Azure 檔案儲存體](storage-how-to-use-files-linux.md)

  本文將說明如何 toomount Azure 檔案共用上的 Linux 系統和上傳/下載檔案。
* [在 Windows 上開始使用 Azure 檔案儲存體](storage-dotnet-how-to-use-files.md)

  本文件提供 Azure 檔案共用的概觀以及如何 toomount，並用使用 PowerShell 和.NET。
* [Azure 檔案儲存體內部](https://azure.microsoft.com/blog/inside-azure-file-storage/)

  本文章宣佈 hello 公開上市的 Azure 檔案儲存體，並提供 hello SMB 3.0 加密相關的技術詳細資料。

### <a name="using-client-side-encryption-toosecure-data-that-you-send-toostorage"></a>使用您傳送 toostorage 用戶端加密 toosecure 資料
另一個可協助您確保在用戶端應用程式和儲存體之間傳輸時資料安全性的選項是用戶端加密。 hello 資料之前要傳輸至 Azure 儲存體加密。 當擷取 hello 資料從 Azure 儲存體，hello 資料解密後收到 hello 用戶端。 即使將 hello 網路上加密 hello 資料時，我們建議，您也可以使用 HTTPS，因為它具有內建的協助降低影響 hello hello 資料完整性的網路錯誤的資料完整性檢查。

用戶端加密也是加密在靜止時，資料的方法，如 hello 資料會以加密格式儲存。 我們將討論這 hello > 一節中詳細說明上[加密在靜止](#encryption-at-rest)。

## <a name="encryption-at-rest"></a>待用加密
有三個 Azure 功能可提供待用加密。 Azure 磁碟加密是使用的 tooencrypt hello OS 和資料磁碟中的 IaaS 虛擬機器。 其他兩個 hello; 用戶端加密和 SSE – 使用的 tooencrypt 資料在 Azure 儲存體。 讓我們看看每一個，然後進行比較，並查看每一個的使用時機。

雖然您可以使用用戶端加密 tooencrypt hello 資料傳輸 （這也會以加密格式儲存體中儲存） 中，您可能偏好 hello 傳輸期間 toosimply 使用 HTTPS 和有 hello 資料 toobe 自動加密時，它的方式儲存。 有兩種方式 toodo 這-Azure 磁碟加密和 SSE。 使用其中一種 toodirectly 加密的 Vm，所使用的 OS 和資料磁碟上的 hello 資料和其他 hello 是使用的 tooencrypt 資料寫入 tooAzure Blob 儲存體。

### <a name="storage-service-encryption-sse"></a>儲存體服務加密 (SSE)
SSE 可讓您 toorequest 寫入它 tooAzure 儲存體時，hello 儲存體服務會自動加密 hello 資料。 當您從 Azure 儲存體讀取 hello 資料時，將會解密 hello 儲存體服務，在傳回之前。 這可讓您 toosecure 您的資料，而不需要 toomodify 程式碼，或是將加入程式碼 tooany 應用程式。

這是套用 toohello 整個儲存體帳戶的設定。 您可以啟用和停用此功能藉由變更 hello hello 設定值。 toodo，您可以使用 hello Azure 網站、 PowerShell hello Azure CLI、 hello 儲存體資源提供者 REST API 或 hello.NET 儲存體用戶端程式庫。 根據預設，SSE 已關閉。

在這個階段中，會由 Microsoft 管理 hello hello 加密所使用的索引鍵。 我們一開始產生 hello 索引鍵，並管理 hello 安全儲存體的 hello 索引鍵為 hello 定期輪替，由內部 Microsoft 原則定義。 Hello 未來，您會取得 hello 能力 toomanage 加密金鑰，並提供 Microsoft 管理的金鑰的移轉路徑 toocustomer 管理的金鑰。

這項功能是可供使用 hello Resource Manager 部署模型所建立的 Standard 和 Premium 儲存體帳戶。 SSE 適用於僅 tooblock blob 時，分頁 blob，並附加 blob。 hello 其他類型的資料，包括資料表、 佇列和檔案，將不會加密。

啟用 SSE 並 hello 資料寫入 tooBlob 儲存體時，只加密資料。 啟用或停用 SSE 並不會影響現有的資料。 換句話說，當您啟用此加密時，它將不返回並加密已經存在的資料也不會解密已存在於當您停用 SSE hello 資料。

如果您想 toouse 與傳統儲存體帳戶的這項功能，您可以建立新的資源管理員儲存體帳戶，並使用 AzCopy toocopy hello 資料 toohello 新帳戶。

### <a name="client-side-encryption"></a>用戶端加密
討論 hello 加密傳輸中的 hello 資料時，我們曾提及用戶端加密。 這項功能可讓您 tooprogrammatically 加密再將它傳送 hello 網路 toobe 寫入 tooAzure 存放裝置，透過用戶端應用程式中的資料和 tooprogrammatically 擷取從 Azure 儲存體後解密資料。

這提供在傳輸中的加密，但它也提供 hello 靜止的加密功能。 請注意，雖然 hello 資料已加密傳輸中，我們仍建議使用 HTTPS tootake 優點 hello 內建的資料完整性檢查，協助減輕影響 hello hello 資料完整性的網路錯誤。

位置，您可以將此範例是如果您有 web 應用程式將 blob 儲存和擷取 blob，而您想 hello 應用程式和資料 toobe 儘可能安全。 在此情況下，您會使用用戶端加密。 hello hello 用戶端與 hello Azure Blob 服務之間的流量包含加密的 hello 資源，並沒有人可以解譯 hello 資料在傳輸過程中的 deserialization 到您的私用 blob。

用戶端加密是內建 hello Java 和 hello.NET 儲存體用戶端程式庫，接著使用 hello Azure 金鑰保存庫 Api，讓您 tooimplement 很容易。 會使用 hello 信封的技術，且會儲存每個儲存體物件中的 hello 加密所使用的中繼資料加密及解密 hello 資料 hello 程序。 例如，對 blob，它將它儲存在 hello blob 中繼資料，而佇列，就會加入它 tooeach 佇列訊息。

Hello 加密本身，您可以產生和管理加密金鑰。 您也可以使用 hello Azure 儲存體用戶端程式庫所產生的金鑰，或者您可以擁有 hello Azure 金鑰保存庫產生 hello 的索引鍵。 您可以將加密金鑰儲存於內部部署金鑰儲存體中，或將它們儲存在 Azure 金鑰保存庫中。 Azure 金鑰保存庫可讓您 toogrant 存取 toohello 密碼在 Azure 金鑰保存庫 toospecific 使用者使用 Azure Active Directory。 這表示不只是任何人都可以用來讀取 hello Azure 金鑰保存庫，和擷取您所使用的用戶端加密 hello 索引鍵。

#### <a name="resources"></a>資源
* [在 Microsoft Azure 儲存體中使用 Azure 金鑰保存庫加密和解密 blob](storage-encrypt-decrypt-blobs-key-vault.md)

  本文將說明如何使用 Azure 金鑰保存庫，包括如何 toocreate hello KEK，並將它儲存在 hello 保存庫中使用 PowerShell toouse 用戶端加密。
* [Microsoft Azure 儲存體的用戶端加密和 Azure Key Vault 金鑰保存庫](storage-client-side-encryption.md)

  本文章提供用戶端加密的說明，並提供使用 hello 儲存體用戶端程式庫 tooencrypt 和解密資源從 hello 四個儲存體服務的範例。 它也會討論 Azure 金鑰保存庫。

### <a name="using-azure-disk-encryption-tooencrypt-disks-used-by-your-virtual-machines"></a>使用 Azure 磁碟加密 tooencrypt 磁碟供您的虛擬機器
「Azure 磁碟加密」是一個新功能。 這項功能可讓您 tooencrypt hello OS 磁碟和 IaaS 虛擬機器使用的資料磁碟。 適用於 Windows、 hello 磁碟會使用業界標準的 BitLocker 加密技術來加密。 適用於 Linux，hello 磁碟會使用 hello DM Crypt 技術來加密。 這是與整合 Azure 金鑰保存庫 tooallow 您 toocontrol 和管理 hello 磁碟加密金鑰。

hello 解決方案支援 IaaS Vm 的下列案例，當啟用 Microsoft Azure 中的 hello:

* 與 Azure 金鑰保存庫整合
* 標準層 VM：[A、D、DS、G、GS 等系列 IaaS VM](https://azure.microsoft.com/pricing/details/virtual-machines/)
* 在 Windows 和 Linux IaaS VM 上啟用加密
* 為 Windows IaaS VM 的 OS 和資料磁碟機停用加密
* 為 Linux IaaS VM 的資料磁碟機停用加密
* 在執行 Windows 用戶端 OS 的 IaaS VM 上啟用加密
* 在具有掛接路徑的磁碟區上啟用加密
* 在使用 mdadm 設定了等量磁碟 (RAID) 的 Linux VM 上啟用加密
* 在使用資料磁碟適用之 LVM 的 Linux VM 上啟用加密
* 在使用儲存空間設定的 Windows VM 上啟用加密
* 所有 Azure 公用區域皆受到支援

hello 方案不支援下列案例、 功能和技術 hello 版本中的 hello:

* 基本層 IaaS VM
* 在 Linux IaaS VM 的 OS 磁碟機上停用加密
* 使用 hello 傳統 VM 建立方法所建立的 IaaS Vm
* 與您的內部部署金鑰管理服務整合
* Azure 檔案儲存體 (共用檔案系統)、網路檔案系統 (NFS)、動態磁碟區，以及使用軟體型 RAID 系統設定的 Windows VM


> [!NOTE]
> Linux OS 磁碟加密目前支援下列 Linux 散發套件 hello: RHEL 7.2、 CentOS 7.2n 和 Ubuntu 16.04。
>
>

此功能可確保虛擬機器磁碟上的所有待用資料都會在 Azure 儲存體中加密。

#### <a name="resources"></a>資源
* [Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)

### <a name="comparison-of-azure-disk-encryption-sse-and-client-side-encryption"></a>Azure 磁碟加密、SSE 和用戶端加密的比較
#### <a name="iaas-vms-and-their-vhd-files"></a>IaaS VM 及其 VHD 檔案
對於 IaaS VM 所使用的磁碟，建議使用 Azure 磁碟加密。 您可以開啟 SSE tooencrypt hello VHD 檔案使用的 tooback 那些磁碟在 Azure 儲存體，但是它只會加密新寫入的資料。 這表示如果您建立的 VM，然後 hello 保存 hello VHD 檔案的儲存體帳戶上啟用 SSE hello 所做的變更將會加密，不 hello 原始 VHD 檔案。

如果您使用建立 VM 從 hello Azure Marketplace 映像，就會執行 Azure[淺層複製](https://en.wikipedia.org/wiki/Object_copying)hello 映像 tooyour 的 Azure 儲存體，並儲存體帳戶未加密即使您已啟用 SSE。 它會建立 hello VM 並啟動更新 hello 映像之後，SSE 會啟動 hello 資料加密。 基於這個理由，是最佳 toouse，如果您想要它們完全加密從 hello Azure Marketplace 中的映像建立 Azure Vm 上的磁碟加密。

如果您加入至 Azure 的預先加密的 VM 從內部部署，您會是能 tooupload hello 加密金鑰 tooAzure 金鑰保存庫，並且繼續使用您已使用內部部署該 vm 的 hello 加密。 Azure 磁碟加密是啟用的 toohandle 此案例。

如果您有未加密的 VHD 從內部部署，您可以將它上傳至 hello 圖庫做為自訂映像，並佈建將 VM 從它。 如果您這樣使用 hello 資源管理員範本，您可以要求它 tooturn Azure 磁碟加密時它 hello VM 會開機。

當您新增的資料磁碟，並裝載在 hello VM 上時，您可以在 Azure 磁碟加密上開啟該資料磁碟。 便會先加密該資料做為本機磁碟，然後 hello 服務管理層也會這樣對儲存體延遲寫入 hello 存放裝置內容會經過加密。

#### <a name="client-side-encryption"></a>用戶端加密
用戶端加密是 hello 加密您的資料，因為它會加密傳輸中之前，會加密在靜止 hello 資料的最安全的方法。 不過，但它要求您加入程式碼 tooyour 應用程式使用儲存體，您可能不想 toodo。 在這些情況下，您可以為您的資料在傳輸中和靜止 SSE tooencrypt hello 資料使用 HTTPs。

透過用戶端加密，您可以加密表格實體、訊息佇列和 Blob。 使用 SSE，您只能加密 Blob。 如果您需要資料表和佇列資料 toobe 加密時，您應該使用用戶端加密。

用戶端加密是完全由 hello 應用程式管理。 這是 hello 最安全的方式，但沒有需要您 toomake 以程式設計方式變更 tooyour 應用程式而且備妥的金鑰管理程序。 當您想 hello 時使用此額外的安全性，在傳輸中和您想要加密您儲存的資料 toobe。

用戶端加密 hello 用戶端上的更多負載，而且您在 tooaccount 這個延展性的計劃，特別是如果您已加密及傳輸大量資料。

#### <a name="storage-service-encryption-sse"></a>儲存體服務加密 (SSE)
SSE 是由 Azure 儲存體所管理。 使用 SSE 不提供 hello 安全性 hello 中的資料傳輸，但它未加密 hello 資料寫入 tooAzure 儲存體。 使用此功能時 hello 效能上沒有任何影響。

您只能使用 SSE 來加密區塊 Blob、附加 Blob 及分頁 Blob。 如果您需要 tooencrypt 資料表資料或佇列資料，您應該考慮使用用戶端加密。

如果您沒有封存或是您使用做為基礎來建立新的虛擬機器的 VHD 檔案的程式庫，您可以建立新的儲存體帳戶、 啟用 SSE，並再上傳 hello VHD 檔案 toothat 帳戶。 這些 VHD 檔案將會由 Azure 儲存體加密。

如果您有 Azure 磁碟加密 hello 磁碟中的 VM 和 SSE hello 持有 hello VHD 檔案的儲存體帳戶上啟用已啟用，它將可以正常運作。它會導致任何新寫入的資料加密兩次。

## <a name="storage-analytics"></a>儲存體分析
### <a name="using-storage-analytics-toomonitor-authorization-type"></a>使用儲存體分析 toomonitor 授權類型
每個儲存體帳戶，您可以啟用 Azure 儲存體分析 tooperform 記錄，並儲存度量資料。 當您想要 toocheck hello 效能度量的儲存體帳戶，或需要 tootroubleshoot 儲存體帳戶，因為您會遇到效能問題時，這是很棒的工具 toouse。

另一份資料，您可以在 hello 儲存體分析記錄檔中看到是存取儲存體時使用的其他人的 hello 驗證方法。 例如，使用 Blob 儲存體，您所見即使用共用存取簽章或 hello 儲存體帳戶金鑰，或如果公用存取的 hello blob。

這可以是非常有幫助您緊密會保護存取 toostorage 如果項目。 比方說，在 Blob 儲存體中，您可以設定所有 hello 容器 tooprivate 和整個應用程式實作 hello SAS 服務使用。 然後您可以檢查 hello 記錄定期 toosee 如果使用 hello 儲存體帳戶金鑰，這可能表示有安全性的漏洞，存取您的 blob 或 hello blob 是公用的但它們不應該是。

#### <a name="what-do-hello-logs-look-like"></a>請勿 hello 記錄外觀為何？
之後您啟用 hello 儲存體帳戶計量，透過 hello Azure 入口網站記錄、 分析資料將會開始 tooaccumulate 快速。 hello 記錄檔和度量的每項服務位於不同;hello 記錄只會在活動中沒有該儲存體帳戶，而每隔一分鐘、 每小時或每一天，根據您設定的方式，將會記錄 hello 度量時寫入。

hello 記錄檔會儲存在名為 $logs hello 儲存體帳戶中的容器中的區塊 blob。 啟用儲存體分析時，會自動建立此容器。 一旦建立此容器之後，就無法予以刪除，但您可以刪除其內容。

Hello $logs 容器下的資料夾，每個服務，而且再有子資料夾 hello 年/月/日/小時。 在小時，只要編號 hello 記錄檔。 這是什麼 hello 目錄結構看起來像：

![記錄檔的檢視](./media/storage-security-guide/image1.png)

會記錄每個要求 tooAzure 儲存體。 以下是顯示 hello 較少的第一個欄位的記錄檔的快照集。

![記錄檔的快照](./media/storage-security-guide/image2.png)

您可以查看您可以使用 hello 記錄 tootrack 任何一種呼叫 tooa 儲存體帳戶。

#### <a name="what-are-all-of-those-fields-for"></a>這些所有欄位的用途為何？
沒有下列 hello 資源中所列的發行項提供 hello hello 清單 hello 記錄檔並使用來進行中的許多欄位。 以下是 hello 清單的欄位順序：

![記錄檔中欄位的快照](./media/storage-security-guide/image3.png)

我們有興趣 hello GetBlob，項目，以及如何就會進行驗證，因此我們需要 toolook 作業類型 Get-Blob"的項目，以及檢查 hello 要求狀態 (4<sup>th</sup>資料行) 和 hello 授權類型 (8<sup>th</sup>資料行)。

例如，在 hello 第一次上述 hello 清單中的幾個資料列、 hello 要求狀態是 「 成功 」 和 hello 授權類型為 「 已驗證 」。 這表示 hello 要求已驗證使用 hello 儲存體帳戶金鑰。

#### <a name="how-are-my-blobs-being-authenticated"></a>如何驗證我的 Blob？
以下提供三個我們感興趣的案例。

1. hello blob 時為公用，且它使用沒有共用存取簽章的 URL 來存取。 在此情況下，hello 要求狀態是 「 AnonymousSuccess"和 hello 授權類型為 「 匿名 」。

   1.0;2015-11-17T02:01:29.0488963Z;GetBlob;**AnonymousSuccess**;200;124;37;**anonymous**;;mystorage…
2. hello blob 是私人的而且搭配共用存取簽章。 在此情況下，hello 要求狀態是 「 SASSuccess"和 hello 授權類型為"sas"。

   1.0;2015-11-16T18:30:05.6556115Z;GetBlob;**SASSuccess**;200;416;64;**sas**;;mystorage…
3. hello blob 是私人的而且 hello 儲存體金鑰已使用的 tooaccess 它。 Hello 要求狀態是在此情況下，「**成功**"，而且 hello 授權類型 」**驗證**"。

   1.0;2015-11-16T18:32:24.3174537Z;GetBlob;**Success**;206;59;22;**authenticated**;mystorage…

您可以使用 hello Microsoft Message Analyzer tooview 和分析這些記錄檔。 它包含搜尋和篩選功能。 比方說，您可能想 toosearch 的執行個體的 GetBlob toosee 如果 hello 使用量不如預期，也就是 toomake 確定其他人不不適當地存取儲存體帳戶。

#### <a name="resources"></a>資源
* [Storage Analytics](storage-analytics.md)

  這篇文章是儲存體分析的概觀以及如何 tooenable 它們。
* [儲存體分析記錄檔格式](https://msdn.microsoft.com/library/azure/hh343259.aspx)

  本文說明 hello 儲存體分析記錄格式，並詳細資料 hello 可用欄位另有規定，包括驗證類型，表示 hello hello 要求使用的驗證類型。
* [監視 hello Azure 入口網站中的儲存體帳戶](storage-monitor-storage-account.md)

  本文將說明如何 tooconfigure 監視的度量和記錄的儲存體帳戶。
* [使用 Azure 儲存體度量和記錄、AzCopy 和 Message Analyzer 進行端對端疑難排解](storage-e2e-troubleshooting.md)

  這篇文章討論有關使用儲存體分析 hello 進行疑難排解，並顯示如何 toouse hello Microsoft Message Analyzer。
* [Microsoft Message Analyzer 操作指南](https://technet.microsoft.com/library/jj649776.aspx)

  這篇文章 hello 參考 hello Microsoft Message Analyzer，而且包含連結 tooa 教學課程 」、 「 快速入門中和 「 功能摘要。

## <a name="cross-origin-resource-sharing-cors"></a>跨原始來源資源分享 (CORS)
### <a name="cross-domain-access-of-resources"></a>跨網域存取資源
在某一個網域中執行的 Web 瀏覽器對來自不同網域的資源提出 HTTP 要求時，這稱為跨原始來源的 HTTP 要求。 例如，來自 contoso.com 的 HTML 網頁會對裝載於 fabrikam.blob.core.windows.net 上的 jpeg 提出要求。 基於安全性理由，瀏覽器會限制從指令碼 (例如 JavaScript) 內初始化的跨原始來源 HTTP 要求。 這表示當一些 JavaScript 程式碼，在 contoso.com 上的網頁要求上 fabrikam.blob.core.windows.net 該 jpeg，hello 瀏覽器將不允許 hello 要求。

用途這有與 Azure 儲存體 toodo？ 如果您要將靜態資產，例如 JSON 或 XML 資料檔案儲存在 Blob 儲存體使用儲存體帳戶呼叫 Fabrikam、 hello 資產的 hello 網域是 fabrikam.blob.core.windows.net，以及 hello contoso.com web 應用程式不會無法 tooaccess 它們使用 JavaScript，因為 hello 網域不同。 這也是如果您正在 toocall hello – 例如，資料表儲存體 – Azure 儲存體服務的其中一個會傳回 JSON 資料 toobe hello JavaScript 用戶端所處理，則為 true。

#### <a name="possible-solutions"></a>可能的解決方案
其中一種方式 tooresolve 這是 tooassign"storage.contoso.com"toofabrikam.blob.core.windows.net 類似的自訂網域。 hello 問題是，您只能指派該自訂網域 tooone 儲存體帳戶。 如果多個儲存體帳戶中儲存 hello 資產嗎？

另一個方式 tooresolve 這是 toohave hello web 應用程式 act 為 hello 儲存體呼叫的 proxy。 這表示如果您要上傳檔案 tooBlob 儲存體，hello web 應用程式會是直接在本機寫入並再將它複製 tooBlob 存放裝置，或者它會讀取所有內容到記憶體又接著加以寫 tooBlob 儲存體。 或者，您可以撰寫的專用的 web 應用程式 （例如 Web API) 上傳 hello 檔案在本機，並將其寫入 tooBlob 儲存體。 無論如何，您必須 tooaccount 該函式，當決定 hello 延展性需求。

#### <a name="how-can-cors-help"></a>CORS 如何提供協助？
Azure 儲存體可讓您 tooenable CORS – 跨原始資源共用。 每個儲存體帳戶，您可以指定可存取該儲存體帳戶中的 hello 資源的網域。 例如，在我們以上所述的案例，我們可以 hello fabrikam.blob.core.windows.net 儲存體帳戶上啟用 CORS，並設定它 tooallow 存取 toocontoso.com。然後 hello web 應用程式 contoso.com 可以直接存取 fabrikam.blob.core.windows.net 中的 hello 資源。

一件事 toonote 是 CORS 允許存取，但它不提供驗證所需的所有非公用存取的儲存體資源。 這表示您只能存取 blob 這些是公用，或包含共用存取簽章提供您如果 hello 適當的權限。 表格、佇列和檔案沒有公用存取權且需要 SAS。

根據預設，所有服務上都會停用 CORS。 您可以使用 hello REST API 或 hello 儲存體用戶端程式庫 toocall 其中 hello 方法 tooset hello 服務原則，以啟用 CORS。 當您這樣做時，就會在 XML 中包含 CORS 規則。 以下是使用儲存體帳戶的 hello Blob 服務的 hello 設定服務屬性作業已設定的 CORS 規則的範例。 您可以執行該作業使用 hello 儲存體用戶端程式庫或 hello REST Api 針對 Azure 儲存體。

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

以下是每一列的意義︰

* **AllowedOrigins**這會告訴哪些不相符的網域可以要求並接收 hello 儲存體服務中的資料。 這表示，contoso.com 和 fabrikam.com 可以針對特定的儲存體帳戶向 Blob 儲存體要求資料。 您也可以設定此 tooa 萬用字元 (\*) tooallow 所有網域 tooaccess 都要求。
* **AllowedMethods**這是發出 hello 要求時，可以使用的方法 （HTTP 要求動詞命令） hello 清單。 在此範例中，只允許 PUT 和 GET。 您可以設定此 tooa 萬用字元 (\*) 使用的所有方法 toobe tooallow。
* **AllowedHeaders** hello 提出 hello 要求時，可以指定 hello 原始網域的標頭的要求。 在此範例中，允許以 x-ms-meta-data、x-ms-meta-target 及 x-ms-meta-abc 開頭的所有中繼資料標頭。 hello 萬用字元 (\*) 表示 hello 任何標頭開頭指定允許前置詞。
* **ExposedHeaders**這樣做會告知 hello 瀏覽器 toohello 要求簽發者應公開的回應標頭。 在此範例中，將公開任何以 "x-ms-meta-" 開頭的標頭。
* **MaxAgeInSeconds**這是 hello 的瀏覽器將會快取預檢 OPTIONS 要求 hello 的時間長度上限。 （如需 hello 預檢要求的詳細資訊，請檢查 hello 第一篇文章下方）。

#### <a name="resources"></a>資源
如需 CORS 和如何 tooenable，請簽出這些資源。

* [Hello Azure.com 上的 Azure 儲存體服務的跨原始資源共用 (CORS) 支援](storage-cors-support.md)

  本文章提供 CORS 和 tooset hello 規則 hello 不同儲存體服務之方式的概觀。
* [Hello MSDN 上的 Azure 儲存體服務的跨原始資源共用 (CORS) 支援](https://msdn.microsoft.com/library/azure/dn535601.aspx)

  這是 hello hello Azure 儲存體服務的 CORS 支援的參考文件集。 這有連結 tooarticles 套用 tooeach 儲存體服務，顯示範例和說明 hello CORS 檔案中的每個項目。
* [Microsoft Azure 儲存體︰CORS 簡介](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/02/03/windows-azure-storage-introducing-cors.aspx)

  這是連結 toohello 初始部落格文章宣佈適用於 CORS 和顯示方式 toouse 它。

## <a name="frequently-asked-questions-about-azure-storage-security"></a>關於 Azure 儲存體安全性的常見問題集
1. **如何確認我無法使用 hello HTTPS 通訊協定將傳入或傳出 Azure 儲存體的 hello blob hello 完整性？**

   如果因故需要的 toouse HTTP 而非 HTTPS 與您正在使用區塊 blob，您可以使用 MD5 檢查 toohelp 會驗證要傳輸的 hello blob hello 完整性。 這有助於提供保護以防止發生網路/傳輸層錯誤，但不一定是媒介攻擊。

   如果您可以使用 HTTPS 來提供傳輸層安全性，則使用 MD5 檢查是多餘且不必要的。

   如需詳細資訊，請簽出 hello [Azure Blob MD5 概觀](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/02/18/windows-azure-blob-md5-overview.aspx)。
2. **Hello 美國的 FIPS 相容的情況為何為何？**

   hello 美國聯邦資訊處理標準 (FIPS) 定義由美國核准使用的密碼編譯演算法美國聯邦政府 hello 保護機密資料的電腦系統。 啟用 FIPS 模式在 Windows server 或桌面會告知 hello OS 應僅 FIPS 驗證的密碼編譯演算法。 如果應用程式不相容的演算法，將會中斷 hello 應用程式。 以 framework 4.5.2 或更高版本，hello 應用程式時自動切換 hello 的密碼編譯演算法 toouse FIPS 相容演算法 hello 電腦處於啟用 FIPS 模式。

   Microsoft 保留向上 tooeach 客戶 toodecide 是否 tooenable FIPS 模式。 我們認為沒有沒有充分的理由，不是主體 toogovernment 法規 tooenable FIPS 模式預設的客戶。

   **資源**

* [Why We’re Not Recommending "FIPS Mode" Anymore (為什麼我們不再建議「FIPS 模式」)](http://blogs.technet.com/b/secguide/archive/2014/04/07/why-we-re-not-recommending-fips-mode-anymore.aspx)

  此部落格文章提供 FIPS 概觀，並說明他們為什麼預設不啟用 FIPS 模式。
* [FIPS 140 Validation (FIPS 140 驗證)](https://technet.microsoft.com/library/cc750357.aspx)

  本文提供如何 Microsoft 產品和密碼編譯模組符合 hello FIPS 標準 hello 美國地區資訊的相關資訊。
* [Windows XP 和 Windows 的更新版本中「系統密碼編譯︰使用符合 FIPS 規範的演算法進行加密，雜湊，以及簽章」安全性設定的效果](https://support.microsoft.com/kb/811833)

  這篇文章討論 hello 使用 FIPS 模式中較舊的 Windows 電腦的相關資訊。
