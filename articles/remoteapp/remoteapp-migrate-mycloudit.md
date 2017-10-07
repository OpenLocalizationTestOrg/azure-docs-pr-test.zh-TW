---
title: "aaaChange hello 計費的 Azure RemoteApp |Microsoft 文件"
description: "深入了解如何 toostop 支付 Azure RemoteApp。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 8f94da9a-7848-4ddc-b7b7-d9c280ccf4d7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: mbaldwin
ms.openlocfilehash: fe3841a88978ec56829932621489e75d5dd7e673
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toomycloudit"></a>從 Azure RemoteApp tooMyCloudIT 移轉 

**您目前使用 Microsoft Azure RemoteApp 嗎？**: MyCloudIT 建置自動化的工具 toomigrate 您 Azure RemoteApp (ARA) 清查 toohello MyCloudIT 管理平台在 Microsoft Azure 上繼續 toorun 時。

**要善用 hello Azure 資源管理員入口網站**: hello MyCloudIT 平台已完成的移轉可讓立即存取 tooAzure 新的 Azure 資源管理員入口網站。 此入口網站包含所有 hello 新功能和創新提供 Microsoft azure 存取 tooVirtual 機器大小 tooensure 包括您的部署內建 toosupport hello 您企業需求。

**在您的需求的平行 tooensure hello 右方案中測試**: hello MyCloudIT 移轉工具內建 tooinitiate hello 移轉程序在平行 while 目前 ARA 使用者繼續 toouse ARA 的測試。  在您的移轉和測試皆已完成之前，您的使用者將保留於 ARA 中。  hello 移轉工具會建立 toohandle hello 一般 ARA 集合。  如果您認為您有唯一、 非標準的案例，請與我們連絡[ sales@conexlink.com ](mailto:sales@conexlink.com)讓我們可以提供量身訂做的計劃 tooassist 您移轉。

**桌面做為服務功能**： 請注意 MyCloudIT 不僅提供您習慣，hello RemoteApp 功能，但我們也提供完整桌面-即--服務每個月沒有任何最小的使用者相同成本 hello 的功能需求。

## <a name="what-we-will-do-for-you"></a>我們將為您執行哪些動作

MyCloudIT 自動化 hello 移轉，您的 Azure RemoteApp 範本從您的訂用帳戶與我們的自動的移轉工具的 Azure 資源管理員入口網站的訂用帳戶 toohello hello Azure 傳統入口網站。  

> [!NOTE]
> hello Azure RemoteApp 範本必須留在 hello 與原始的 Azure RemoteApp 部署相同 Azure 區域。  如果您在 hello 移轉期間需要 toochange Azure 區域或 Azure 訂用帳戶，請與我們連絡如需其他指引，在[ sales@conexlink.com ](mailto:sales@conexlink.com)。

如需自動化 hello 移轉程序以 hello MyCloudIT 移轉工具的詳細資訊，以閱讀下列：

1. hello 移轉工具會掃描所有的現有 ARA 部署您目前訂閱。  
2. 選取一個 ARA 集合 toomigrate 一次。  如果您有多個集合，請多次執行我們的工具。
3. 您擁有 hello 選項 toocopy hello 使用者設定檔磁碟 (UPD) tooyour 新部署，因此您可以擷取舊版的資料，或手動對應 Upd toohello 新部署。 如果您選擇 toocopy 您 Upd，我們會將儲存 hello Upd，並包含 hello UPD 名稱 tooeach 使用者名稱對應的文字檔。  hello Upd 將會複製的 tooa 伺服器共用上 hello RDSMGMT `F:\Shares\LegacyUPD` ，而且會公開透過 hello 共用`\\RDSmgmt\LegacyUPD`。 
4. 針對您目前的 ARA 部署，您的移轉不需要停機。  但是，如果任何變更都會套用 （從 ARA) toohello Upd hello 複製之後，將不儲存在 hello Azure 資源管理員入口網站中的 hello Upd 中反映這些變更。 
5. 如果您有其他的 Vm，例如網域控制站和傳統 Azure 虛擬網路中的檔案伺服器，我們將會建立現有的傳統 Azure 虛擬網路之間的對等互連的 VNet，hello 新的虛擬網路我們為您建立在 hello 新的 Azure 資源管理員入口網站。
6. 自動化的解決方案只可以建立現有的傳統 Azure 虛擬網路之間的對等互連的 VNet 和 hello 新的虛擬網路，如果您現有的 ARA 部署混合式部署。這表示您的驗證與 Windows Server Active Directory 網域控制站中現有的傳統虛擬網路的 hello。 如果我們不會建立您的集合，用於對等互連的 VNet，但您需要對等互連的 VNet，請與我們連絡以[ sales@conexlink.com ](mailto:sales@conexlink.com) ，我們會很樂意 tooconfigure VNet 對等互連不需額外成本。
7. 自動化的解決方案可確保您的 Azure DNS 設定會更新與新虛擬網路設定 tooensure hello 新部署可以連接 tooyour 現有網域控制站在 hello 傳統的 VNet。
8. 自動化的解決方案可確保沒有任何 IP 位址衝突當我們建立這個新的虛擬網路，並建立 hello VNet 對等互連若是包含現有的 Windows Server Active Directory 伺服器的部署。
9. 如果您只使用 Azure AD 進行驗證，MyCloudIT 會建立新的 Windows Server Active Directory 網域及使用 Azure AD Connect toosynchronize 使用者 hello 現有 Azure AD 執行個體之間建立的新 Windows Server Active Directory 網域的 hello由 MyCloudIT。
10. 如果您使用 Windows Server Active Directory 網域 tooauthenticate ARA 使用者，我們自動化的解決方案會連接現有的 Windows Server Active Directory 網域控制站透過對等互連的 VNet 您新 MyCloudIT 部署 tooyour。
11. 如果您使用 Azure Active Directory Domain Services 進行驗證，我們就能將您移轉，但請與我們連絡，讓我們可為您建立自訂的移轉計劃。  請傳送電子郵件太[sales@conexlink.com](mailto:sales@conexlink.com)。 
12. 一旦 hello 集合 toobe 移轉就是確認，坐請放鬆時自動化的解決方案移轉您的 ARA 集合和使用者設定檔磁碟 （選擇性） toohello 新 MyCloudIT 驅動遠端應用程式方案。
13. Hello 部署完成之後，我們重新將發佈 hello 相同 ARA，在已發行的應用程式和您的部署後，可以 toopublish 其他應用程式。

## <a name="post-migration-benefits"></a>移轉後的優點

1. 我們提供可讓您 toomanage hello 完整的生命週期的遠端應用程式部署的 hello 管理主控台。
2. 您將無法 toomanage 您虛擬機器從入口網站。  視需要啟動 / 停止及調整個別的 VM。
3. hello 管理主控台 」 提供 hello 能力 toocreate 及管理使用者 / 群組從我們的管理入口網站。
4. hello 管理主控台提供 Office 365 toocreate hello 能力 toosynchronize 使用者相同的登入體驗。
5. hello 管理主控台 」 提供 hello 能力 toocreate 其他遠端應用程式和桌面集合，而不需要重複的使用者的費用或最小的使用者需求。 
6. hello 管理主控台 」 提供 hello 能力 toopublish 新遠端應用程式的應用程式。
7. 如果您只需要您的方案在特定時間 hello 管理主控台 」 提供 hello 能力 tooschedule hello 啟動或關閉遠端應用程式部署。
8. hello 管理主控台提供 hello 能力 tooautomate hello 安裝和設定的 hello Azure Backup agent 可提供您的客戶資料的文件保留歷程記錄。
9. hello 管理主控台 」 提供存取 tooperformance 度量，您的部署。  這讓您不需要安裝額外的效能管理工具 hello 能力 tooidentify 任何潛在的效能瓶頸。
10. 如果您有多個工作階段主機，您將無法 tooenable 自動調整，只需要執行 toobe 主機正在執行的 hello 工作階段。
11. MyCloudIT 提供存取 toohello RDWeb 透過 MyCloudIT 網域名稱的閘道伺服器。  我們也會提供品牌的終端使用者的 hello 能力 toore 對應 hello URL tooa 自訂 URL。

## <a name="prerequisites-for-migration"></a>移轉的必要條件

1. 您必須擁有存取 toohello 裝載您目前的 Azure RemoteApp 解決方案的 Azure 訂用帳戶。
2. 您必須在您的訂用帳戶 toomigrate 授與我們入口網站的權限，您的範本和 toocreate/修改新 MyCloudIT 部署。
3. 請注意，Azure 遠端 App tooa 限制，因為每個集合可以只移轉三次。  如果您需要 toomigrate 集合三次以上，您可以引發票證 tooAzure tooincrease 您匯出的計數，或連絡我們，我們將會協助 hello ARA 要求 tooincrease hello 匯出計數。

## <a name="mycloudit-billing"></a>MyCloudIT 計費

請參閱[MyCloudIT 定價 RemoteApp 解決方案](https://mcitdocuments.blob.core.windows.net/terms/MyCloudIT_Pricing_Overview.pdf)(PDF) 如需詳細資訊 toopredict 和管理您整體 Azure 的成本。

如果您仍有問題，請與我們連絡[ sales@conexlink.com ](mailto:sales@conexlink.com)或監看 hello 完整的示範影片， [Azure RemoteApp 移轉工具 MyCloudIT](https://www.youtube.com/watch?v=YQ_1F-JeeLM&t=482s)。 

