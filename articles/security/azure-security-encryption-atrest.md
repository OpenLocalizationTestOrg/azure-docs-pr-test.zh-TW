---
title: "aaaMicrosoft Azure 資料--靜態加密 |Microsoft 文件"
description: "本文提供的 Microsoft Azure 資料加密概觀在 rest、 hello 整體的功能，以及一般考量。"
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: TomSh
ms.assetid: 9dcb190e-e534-4787-bf82-8ce73bf47dba
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: yurid
ms.openlocfilehash: d74d103e4fd7585543b4f039877af7d742a6b2e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-encryption-at-rest"></a>Azure 資料靜態加密
有多個工具，根據 tooyour 公司的安全性與相容性需求的 Microsoft Azure toosafeguard 資料內。 本文著重在資料如何在整個 Microsoft Azure 保護靜止、 討論 hello 參與 hello 資料保護實作中，各種元件，並檢閱 hello 不同的金鑰管理保護方法的優缺點。 

靜態加密是常見的安全性需求。 Microsoft Azure 的好處是，組織就可以達到靜態加密而不需要實作 hello 成本和管理與 hello 自訂金鑰管理解決方案的風險。 組織可以 hello 選擇讓 Azure 完全管理靜態加密。 此外，組織會有各種選項 tooclosely 管理加密或加密金鑰。

## <a name="what-is-encryption-at-rest"></a>什麼是靜態加密？
靜態加密是指 toohello 密碼編譯編碼 （加密） 的資料時，它會保存。 hello 加密 Azure 中的其他設計使用 tooencrypt 對稱式加密和解密大量快速地根據 tooa 的簡單概念模型的資料：

- 對稱式加密金鑰是使用的 tooencrypt 資料，因為它會保存 
- hello 相同的加密金鑰是使用的 toodecrypt 該資料，因為它已準備好用於記憶體中
- 資料可能會進行分割，不同的金鑰可能會用於每個分割區
- 金鑰必須儲存在安全的位置，以限制存取 toocertain 身分識別和記錄金鑰使用方法的存取控制原則。 通常使用非對稱式加密 toofurther 限制存取加密資料加密金鑰 (hello 中討論*金鑰階層*在本文稍後)

hello 上述說明 hello 高層級的一般項目靜態加密。 在實務上，金鑰管理和控制情節，以及級別和可用性保證，都需要其他建構。 以下將說明 Microsoft Azure 靜態加密的概念和元件。

## <a name="hello-purpose-of-encryption-at-rest"></a>加密在靜止的 hello 目的
靜態加密會是預定的 tooprovide 資料靜止的資料保護 （如上面所述。）對資料靜止的攻擊包括嘗試 tooobtain 實體存取 toohello 硬體的 hello 儲存資料，以及洩露 hello 再包含的資料。 在這類攻擊中，伺服器的硬碟機可能有已 mishandled 讓攻擊者 tooremove hello 硬碟的維護期間。 更新 hello 攻擊者會 hello 硬碟放在其控制項 tooattempt tooaccess hello 資料的電腦。 

設計的 tooprevent hello 攻擊者存取 hello 未加密資料，方法是確保資料會加密磁碟的 hello 靜止的加密。 如果攻擊者 tooobtain 具有這類的硬式磁碟機加密資料，以及沒有存取 toohello 加密金鑰，hello 攻擊者不會危害 hello 資料不需要很棒的困難。 在這類案例中，攻擊者 tooattempt 攻擊，也就是更複雜的加密資料和資源耗用比存取未加密的硬碟機上的資料。 基於這個理由，強烈建議您使用靜態加密，且對許多組織而言是高優先順序的需求。 

在某些情況下，組織需要資料治理及合規性的用途時，也必須使用靜態加密。 諸如 HIPAA、PCI 和 FedRAMP 等產業和政府法規以及國際法規需求，都是透過有關資料保護和加密需求的程序和原則來設定特定的保護措施。 這些眾多法規中，靜態加密是符合規範的資料管理和保護所需的必要量值。 

此外 toocompliance 和法規要求，加密在靜止應該察覺為深度防禦平台功能。 當 Microsoft 相容的平台提供服務，應用程式，且資料、 完整的功能和安全性實體，資料存取控制和稽核時，它會是重要 tooprovide 其他 「 重疊 」 安全性措施 hello 的其中一個案例中其他安全性量值就會失敗。 靜態加密會提供這類額外的防禦機制。

Microsoft 雲端服務和 tooprovide 客戶適用的管理性的加密金鑰和存取 toologs 時使用加密金鑰的顯示中是認可的 tooproviding 加密其餘選項。 此外，Microsoft 朝向 hello 目標是讓預設加密在靜止的所有客戶資料。

## <a name="azure-encryption-at-rest-components"></a>Azure 靜態加密元件

如先前所述，hello 的目標加密在靜止是保存在磁碟的資料以密碼加密金鑰加密。 tooachieve 金鑰建立、 儲存、 存取控制和管理的 hello 加密金鑰，必須提供保護該目標。 詳細資料可能有所差異，但在 Rest 實作的 Azure 服務加密可描述方面 hello 下方然後在 hello 下列圖表中說明的概念。

![元件](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig1.png)

### <a name="azure-key-vault"></a>Azure 金鑰保存庫

hello hello 加密金鑰和存取控制 toothose 金鑰的儲存位置是在其他模型的中央 tooan 加密。 hello 金鑰需要 toobe 高度保全但可管理所指定的使用者和可用 toospecific 服務。 Azure 服務，Azure 金鑰保存庫是 hello 建議使用金鑰存放裝置解決方案，並提供常見的管理體驗提供服務。 索引鍵所儲存及管理在金鑰保存庫，且可以提供存取 tooa 金鑰保存庫，toousers 或服務。 Azure Key Vault 支援客戶建立金鑰或匯入客戶金鑰，可供在客戶管理的加密金鑰情節下使用。

### <a name="azure-active-directory"></a>Azure Active Directory

權限 toouse hello 金鑰儲存在 Azure 金鑰保存庫，toomanage 或 tooaccess 它們加密在 Rest 加密和解密，可以獲得 tooAzure Active Directory 帳戶。 

### <a name="key-hierarchy"></a>金鑰階層

靜態加密實作中，通常會使用一個以上的加密金鑰。 非對稱加密可用來建立 hello 信任和金鑰存取和管理所需的驗證。 對稱式加密對於大量加密和解密效率較高，允許更強式的加密和更佳的效能。 此外，限制 hello 使用的單一加密的金鑰減少 hello 索引鍵的 hello 風險會受到危害，和必須取代的索引鍵時 hello 重新加密的成本。 tooleverage hello 優點的非對稱和對稱式加密和限制 hello 使用和公開的單一金鑰，Azure rest 模型加密會使用 hello 下列類型的索引鍵所組成的索引鍵階層：

- **資料加密金鑰 (DEK)** – 則 AES256 使用對稱金鑰 tooencrypt 磁碟分割或資料區塊。  單一資源可能會有多個分割區和多個資料加密金鑰。 使用不同金鑰將每個資料區塊進行加密，會使密碼編譯分析攻擊更加困難。 需要存取 tooDEKs hello 資源提供者或應用程式執行個體是加密和解密特定區塊。 DEK 取代以新的金鑰時只 hello 其相關聯的區塊中的資料必須以 hello 新的金鑰重新加密。
- **加密金鑰 (KEK)** – 的非對稱式加密金鑰使用 tooencrypt hello 資料加密金鑰。 使用金鑰加密金鑰可讓 hello 本身 toobe 加密，並控制資料加密金鑰。 hello 實體，其具有存取 toohello KEK 可能不同於需要 hello DEK hello 實體。 這可讓實體 toobroker 存取 toohello DEK hello 目的是確保每個 DEK toospecific 資料分割的有限存取權。 由於 hello KEK 必要的 toodecrypt hello Dek，hello KEK 實際上就是單一點，藉以 Dek 可以有效地刪除所刪除的 hello KEK。

hello 資料加密金鑰，以 hello 金鑰加密金鑰加密會分開儲存，而且使用該金鑰加密與金鑰的加密金鑰可以取得任何資料加密金鑰存取 toohello 的實體。 支援不同模型的金鑰儲存。 我們將討論稍後 hello 下一節詳細說明每個模型。

## <a name="data-encryption-models"></a>資料加密模型

了解 hello 各種加密模式，以及其優缺點是基本的了解如何 hello Azure 實作加密在靜止的各種資源提供者。 這些定義所有資源提供者之間共用 Azure tooensure 通用語言和分類。 

伺服器端加密有三種情節：

- 使用服務管理金鑰的伺服器端加密
    - Azure 資源提供者執行 hello 加密和解密作業
    - Microsoft 管理 hello 金鑰
    - 完整的雲端功能

- 在 Azure Key Vault 中使用客戶管理金鑰的伺服器端加密
    - Azure 資源提供者執行 hello 加密和解密作業
    - 客戶透過 Azure Key Vault 控制金鑰
    - 完整的雲端功能

- 在客戶控制的硬碟上使用客戶管理金鑰的伺服器端加密
    - Azure 資源提供者執行 hello 加密和解密作業
    - 客戶在客戶控制的硬體上控制金鑰
    - 完整的雲端功能

針對用戶端加密，請考慮 hello 下列：

- Azure 服務無法查看解密的資料
- 客戶在內部部署環境 (或其他安全的儲存區中) 管理或儲存金鑰。 索引鍵不是使用 tooAzure 服務
- 縮減的雲端功能

在 Azure 分割成兩個主要群組中的 hello 支援加密模型: 「 用戶端加密 」 和 「 伺服器端加密 」 做為先前所述。 請注意，獨立於其他模型 hello 加密使用的 Azure 服務永遠建議 hello 使用 TLS 或 HTTPS 等安全傳輸。 因此，加密傳輸中的應該 hello 傳輸通訊協定來處理，而且不應該決定在 rest 模型 toouse 加密的主要因素。

### <a name="client-encryption-model"></a>用戶端加密模型

用戶端加密模型是指 tooencryption hello 資源提供者或 Azure 外部執行的 hello 服務或呼叫應用程式。 在 Azure 中的 hello 服務應用程式或 hello 客戶資料中心內執行的應用程式，可以執行 hello 加密。 在任一情況下，利用此加密模型時，hello Azure 資源提供者以任何方式接收的資料，而 hello 能力 toodecrypt hello 資料不加密的 blob，或具有存取 toohello 加密金鑰。 在此模型中，hello 金鑰管理由 hello 呼叫服務/應用程式，且完全不透明 toohello Azure 服務。

![用戶端](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig2.png)

### <a name="server-side-encryption-model"></a>伺服器端加密模型

伺服器端加密模型，請參閱 tooencryption hello Azure 服務所執行。 Hello 資源提供者會在該模型中，執行 hello 加密和解密作業。 例如，Azure 儲存體可能在純文字作業中接收資料，並會在內部執行 hello 加密和解密。 hello 資源提供者可能會使用根據提供組態的 hello hello 客戶或由 Microsoft 所管理的加密金鑰。 

![伺服器](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig3.png)

### <a name="server-side-encryption-key-management-models"></a>伺服器端加密金鑰管理模型

每個 rest 模型 hello 伺服器端加密表示特殊的金鑰管理的特性。 這包括，如何建立，並儲存加密金鑰為以及 hello 存取模型，以及 hello 金鑰循環程序。 

#### <a name="server-side-encryption-using-service-managed-keys"></a>使用服務管理金鑰的伺服器端加密

許多客戶，hello 基本需求是 hello 資料的 tooensure 靜止時加密。 使用服務管理金鑰的伺服器端加密啟用這個模型可讓客戶 toomark hello 特定資源 （儲存體帳戶、 SQL 資料庫等） 進行加密，並讓所有金鑰管理層面，例如金鑰、 旋轉和備份tooMicrosoft。 大部分的 Azure 服務，通常支援靜態加密支援卸載 hello 加密金鑰 tooAzure hello 管理此模型。 hello Azure 資源提供者建立 hello 金鑰、 將它們放置在安全的儲存體，和擷取它們需要時。 這表示，hello 服務具有完整存取 toohello 金鑰 hello 服務具有 hello 認證生命週期管理的完整控制權。

![受管理](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig4.png)

使用管理服務金鑰因此快速伺服器端加密可以滿足 hello 需要 toohave 加密在靜止與低負擔 toohello 客戶。 可用時客戶通常會開啟 hello hello 目標訂用帳戶和資源提供者的 Azure 入口網站，並檢查方塊，表示他們想 hello 資料 toobe 加密。 在部分 Resource Manager 中，使用服務管理金鑰的伺服器端加密預設為開啟。 

具有完整存取 toostore hello 服務建立及管理 hello 金鑰，並表示伺服器端加密，使用 Microsoft 受管理的金鑰。 雖然某些客戶可能會希望 toomanage hello 索引鍵，因為他們認為他們可以確保更高的安全性，hello 成本和風險的自訂金鑰存放裝置解決方案相關聯時應該考慮評估此模型。 在許多情況下組織可能會決定資源條件約束或風險的內部部署解決方案可能大於 hello 雲端管理 hello 加密其他金鑰的風險。  不過，此模型可能無法完全的需求 toocontrol hello 建立組織或 hello 加密金鑰或 toohave 不同人員的生命週期管理 （亦即，管理 hello 服務所服務的加密金鑰隔離的金鑰管理從 hello hello 服務整體管理模型)。

##### <a name="key-access"></a>金鑰存取

使用與管理服務金鑰的伺服器端加密時，hello 建立金鑰，儲存和服務存取所有由 hello 服務管理。 一般而言，hello 基本 Azure 資源提供者會將是關閉 toohello 資料，並可迅速 hello 金鑰加密金鑰時，才能存取儲存在安全的內部存放區的存放區中的 hello 資料加密金鑰。

**優點**

- 簡單設定
- Microsoft 會管理金鑰輪替、備份與備援
- 客戶沒有 hello 實作或 hello 風險的自訂金鑰管理配置相關聯的成本。

**缺點**

- 沒有客戶的控制權 hello 加密金鑰 （金鑰規格、 生命週期、 撤銷等等）
- Hello 服務整體管理模型沒有能力 toosegregate 金鑰管理

#### <a name="server-side-encryption-using-customer-managed-keys-in-azure-key-vault"></a>在 Azure Key Vault 中使用客戶管理的金鑰的伺服器端加密 

Hello 需求是 tooencrypt hello 待用的資料，而控制項 hello 加密金鑰的客戶可以使用伺服器端加密使用金鑰保存庫中的客戶管理的金鑰。 某些服務可能會只有 hello 根主要加密金鑰儲存在 Azure 金鑰保存庫中，存放區 hello 內部位置較接近 toohello 資料加密資料加密金鑰。 在案例客戶可以將自己金鑰 tooKey 保存庫 (BYOK – 攜帶您自己的金鑰，) 或產生新的並使用它們 tooencrypt hello 所需資源。 Hello 資源提供者執行 hello 加密和解密作業它會使用 hello 設定金鑰所加密的所有作業的 hello 根機碼。 

##### <a name="key-access"></a>金鑰存取

hello 伺服器端加密模型與 Azure 金鑰保存庫中的受管理的客戶索引鍵牽涉到 hello 服務存取 hello 金鑰 tooencrypt 和視需要的解密。 加密其他金鑰都會透過存取控制原則授與該服務身分識別存取 tooreceive hello 金鑰存取 tooa 服務。 代表相關聯的訂用帳戶上所執行的 Azure 服務，可以使用該訂用帳戶內該服務的身分識別來加以設定。 hello 服務才能執行 Azure Active Directory 驗證並接收識別代表 hello 訂閱該服務本身之驗證語彙基元。 該語彙基元駭客接著可呈現的 tooKey 保存庫 tooobtain 金鑰它具有存取權。

使用加密金鑰的作業，服務身分識別可被授與存取 tooany 的 hello 下列作業： 解密、 加密，unwrapKey、 wrapKey、 驗證、 登入、 取得、 列出、 更新、 建立、 匯入、 刪除、 備份和還原。

tooobtain 加密或解密該 hello UnwrapKey （tooget hello 解密金鑰） 和 WrapKey (tooinsert 金鑰保存庫時建立新的金鑰索引鍵中) 必須具有執行服務執行個體的資源管理員 rest hello 服務身分識別資料中使用的金鑰。


>[!NOTE] 
>如需詳細資訊，在金鑰保存庫上授權看到 hello 保護您的金鑰保存庫頁面中 hello [Azure Key Vault 文件](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)。 

**優點**

- Hello 金鑰的完整控制權使用 – hello 客戶的控制下的 hello 客戶的金鑰保存庫中管理金鑰的加密。
- 能力 tooencrypt 多個服務 tooone master
- 可以隔離金鑰管理從 hello 服務整體管理模型
- 可跨區域定義服務與金鑰位置

**缺點**

- 客戶對於金鑰存取管理擁有完全責任
- 客戶對於金鑰生命週期管理擁有完全責任
- 安裝與設定的其他額外負荷

#### <a name="server-side-encryption-using-service-managed-keys-in-customer-controlled-hardware"></a>在客戶控制的硬碟上，使用服務管理金鑰的伺服器端加密

其中 hello 需求 tooencrypt hello 待用並管理 Microsoft 的控制之外的專屬儲存機制中的 hello 金鑰的情況下，某些 Azure 服務可讓 hello 主機您自己金鑰 (HYOK) 金鑰管理模型。 在此模型中，hello 服務必須從外部網站擷取 hello 金鑰因此受影響的效能和可用性保證，並設定為更複雜。 此外，由於 hello 服務沒有存取 toohello DEK 期間 hello 加密和解密作業 hello 整體的安全性保證，此模型是索引鍵是在 Azure 金鑰保存庫中的客戶管理的類似 toowhen hello。  如此一來，此模型不適用於大部分的組織，除非他們擁有迫切的特定金鑰管理需求。 Toothese 限制，因為大部分的 Azure 服務不支援使用伺服器管理的金鑰所控制的客戶硬體中的伺服器端加密。

##### <a name="key-access"></a>金鑰存取

使用伺服器端加密使用管理服務金鑰客戶控制硬體時 hello 客戶所設定的系統上維護 hello 索引鍵。 支援這個模型的 azure 服務可提供方法來建立安全連線 tooa 客戶提供的金鑰存放區。

**優點**

- 使用 hello 根金鑰的完整控制權 – 客戶提供存放區所管理的金鑰加密
- 能力 tooencrypt 多個服務 tooone master
- 可以隔離金鑰管理從 hello 服務整體管理模型
- 可跨區域定義服務與金鑰位置

**缺點**

- 對於金鑰儲存、安全性、效能和可用性擁有完全責任
- 對於金鑰存取管理擁有完全責任
- 對於金鑰生命週期管理擁有完全責任
- 重要的安裝、設定和進行中的維護成本
- 增加的網路可用性 hello 客戶資料中心與 Azure 資料中心之間的相依性。

## <a name="encryption-at-rest-in-microsoft-cloud-services"></a>Microsoft 雲端服務中的靜態加密

這三種雲端模型中全都是使用 Microsoft 雲端服務：IaaS、PaaS、SaaS。 下列範例說明它們如何符合每個模型：

- 參照 tooas 做為伺服器或 SaaS，例如 Office 365 的 hello 雲端所提供的應用程式的軟體軟體服務。
- 平台服務的客戶利用他們的應用程式中的 hello 雲端使用 hello 雲端中的物件，例如儲存體、 分析和服務匯流排 」 功能。
- 基礎結構服務或基礎結構即服務 (IaaS) 中的客戶部署作業系統及應用程式所裝載的 hello 雲端和可能利用其他雲端服務。

### <a name="encryption-at-rest-for-saas-customers"></a>SaaS 客戶的靜態加密

軟體即服務 (SaaS) 客戶通常會啟用或可在每個服務中使用靜態加密。 Office 365 服務有幾個選項用於客戶 tooverify 或啟用加密在靜止。 如需 Office 365 服務的相關資訊，請參閱 Office 365 的資料加密技術。

### <a name="encryption-at-rest-for-paas-customers"></a>PaaS 客戶的靜態加密

平台即服務 (PaaS) 客戶資料通常會位於應用程式執行環境，並且使用 toostore 客戶資料的任何 Azure 資源提供者。 在 其他選項可用 tooyou toosee hello 加密檢查 hello 表中的 hello 存放裝置和應用程式平台，您使用。 支援，其中每個資源提供者提供連結 tooinstructions 啟用靜態加密。 

### <a name="encryption-at-rest-for-iaas-customers"></a>IaaS 客戶的靜態加密

基礎結構即服務 (IaaS) 客戶可以有各種不同的使用中服務和應用程式。 IaaS 服務可以在其 Azure 裝載的虛擬機器和使用 Azure 磁碟加密的 VHD 中啟用靜態加密。 

#### <a name="encrypted-storage"></a>加密的儲存體

諸如 PaaS、IaaS 等解決方案可以運用儲存資料靜態加密的其他 Azure 服務。 在這些情況下，您可以啟用在 Rest 支援 hello 加密所提供每個已使用的 Azure 服務。 下表的 hello 列舉 hello 主要儲存體、 服務和應用程式平台和 hello 模型支援靜態加密。 有支援，會提供連結 tooinstructions 啟用靜態加密。 

#### <a name="encrypted-compute"></a>加密的計算

在其餘方案完整的加密需要資料永遠不會以未加密形式保存該 hello。 在使用時，可以在本機保存在記憶體中，資料的資料，以各種方式，包括 hello Windows 分頁檔、 損毀傾印和任何記錄 hello 伺服器載入 hello 上應用程式可能會執行。 tooensure 這項資料會加密在靜止 IaaS 應用程式可以在 Azure IaaS 虛擬機器 （Windows 或 Linux） 和虛擬磁碟上使用 Azure 磁碟加密。 

#### <a name="custom-encryption-at-rest"></a>自訂靜態加密

建議您盡可能讓 IaaS 應用程式運用任何已使用 Azure 服務所提供的 Azure 磁碟加密及靜態加密選項。 在某些情況下，例如異常加密需求或非 Azure 架構存放裝置，IaaS 應用程式的開發人員可能需要在 tooimplement 加密 rest 本身。 IaaS 解決方案的開發人員可以運用某些 Azure 元件，更妥善與 Azure 管理和客戶期望進行整合。 具體來說，開發人員應該使用 hello Azure 金鑰保存庫服務 tooprovide 安全金鑰儲存，以及客戶提供一致的金鑰管理選項，與大部分的 Azure 平台服務。 此外，自訂的解決方案應該使用 Azure 受管理的服務身分識別 tooenable 服務帳戶 tooaccess 加密金鑰。 如需關於 Azure Key Vault 和受管理服務身分識別的開發人員資訊，請參閱其個別的 SDK。

## <a name="azure-resource-providers-encryption-model-support"></a>Azure 資源提供者加密模型支援

Microsoft Azure 服務每個支援一或多個其他模型 hello 加密。 某些服務，不過，一或多個 hello 加密模型不可能適用。 此外，服務可能會在不同的排程發行支援這些情節。 本章節描述在撰寫本文為每個 hello 主要 Azure 的資料儲存體服務的 hello 階段的 rest 支援 hello 加密。

### <a name="azure-disk-encryption"></a>Azure 磁碟加密

任何使用 Azure 基礎結構即服務 (IaaS) 功能的客戶都可透過 Azure 磁碟加密讓其 IaaS VM 和磁碟達到靜態加密。 如需有關 Azure 磁碟加密看到 hello [Azure 磁碟加密文件](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)。

#### <a name="azure-storage"></a>Azure 儲存體

Azure Blob 和檔案支援伺服器端加密情節，以及客戶加密資料 (用戶端加密) 的靜態加密。

- 伺服器端：使用 Azure Blob 儲存體的客戶可以在每個 Azure 儲存體資源帳戶上啟用靜態加密。 一次啟用的伺服器端加密，會以透明的方式進行 toohello 應用程式。 如需詳細資訊，請參閱[靜態加密的 Azure 儲存體服務加密](https://docs.microsoft.com/azure/storage/storage-service-encryption)。
- 用戶端：受支援 Azure Blob 的用戶端加密。 當您使用用戶端加密客戶 hello 資料加密並上傳 hello 資料為加密的 blob。 金鑰管理的方式是 hello 客戶。 如需詳細資訊，請參閱 [Microsoft Azure 儲存體的用戶端加密和 Azure Key Vault](https://docs.microsoft.com/azure/storage/storage-client-side-encryption)。


#### <a name="sql-azure"></a>SQL Azure

SQL Azure 目前支援 Microsoft 受管理服務端和用戶端加密情節的靜態加密。

支援的伺服器稱為 「 透明資料加密的 hello SQL 功能目前提供加密。 一旦 SQL Azure 客戶啟用 TDE 後，就會為他們自動建立和管理金鑰。 Hello 資料庫和伺服器層級，可以啟用靜態加密。 自 2017 年 6 月起，[透明資料加密 (TDE)](https://msdn.microsoft.com/library/bb934049.aspx) 依預設將會在新建立的資料庫上啟用。

支援的 SQL Azure 資料的用戶端加密透過 hello[永遠加密](https://msdn.microsoft.com/library/mt163865.aspx)功能。 永遠加密會使用 hello 用戶端所建立及儲存的金鑰。 客戶可以儲存在 Windows 憑證存放區、 Azure 金鑰保存庫或本機硬體安全性模組中的 hello 主要金鑰。 使用 SQL Server Management Studio，SQL 使用者選擇索引鍵他們想 toouse tooencrypt 哪個資料行。

|                                  |                |                     | **加密模型**             |                              |        |
|----------------------------------|----------------|---------------------|------------------------------|------------------------------|--------|
|                                  |                |                     |                              |                              | **用戶端** |
|                                  | **金鑰管理** | **服務管理的金鑰** | **在 Key Vault 中管理的客戶** | **在內部部署管理的客戶** |        |
| **儲存體和資料庫**            |                |                     |                              |                              |        |
| 磁碟 (IaaS)                      |                | -                   | 是                          | 是*                         | -      |
| SQL Server (IaaS)                |                | 是                 | 是                          | 是                          | 是    |
| SQL Azure (PaaS)                 |                | 是                 | 預覽                      | -                            | 是    |
| Azure 儲存體 (區塊/分頁 Blob) |                | 是                 | 預覽                      | -                            | 是    |
| Azure 儲存體 (檔案)            |                | 是                 | -                            | -                            | -      |
| Azure 儲存體 (資料表、佇列)   |                | -                   | -                            | -                            | 是    |
| Cosmos DB (文件 DB)          |                | 是                 | -                            | -                            | -      |
| StorSimple                       |                | 是                 | -                            | -                            | 是    |
| 備份                           |                | -                   | -                            | -                            | 是    |
| **智慧和分析**       |                |                     |                              |                              |        |
| Azure Data Factory               |                | 是                 | -                            | -                            | -      |
| Azure Machine Learning           |                | -                   | 預覽                      | -                            | -      |
| Azure 串流分析           |                | 是                 | -                            | -                            | -      |
| HDInsights (Azure Blob 儲存體)  |                | 是                 | -                            | -                            | -      |
| HDInsights (Data Lake 儲存體)   |                | 是                 | -                            | -                            | -      |
| Azure Data Lake Store            |                | 是                 | 是                          | -                            | -      |
| Azure 資料目錄               |                | 是                 | -                            | -                            | -      |
| Power BI                         |                | 是                 | -                            | -                            | -      |
| **IoT 服務**                     |                |                     |                              |                              |        |
| IoT 中樞                          |                | -                   | -                            | -                            | 是    |
| 服務匯流排                      |                | -              | -                            | -                            | 是    |
| 事件中樞                       |                | -             | -                            | -                            | -      |


## <a name="conclusion"></a>結論

重要 tooMicrosoft 是儲存在 Azure 服務的客戶資料的保護。 所有 Azure 裝載服務都已認可的 tooproviding 加密，其他選項。 諸如 Azure 儲存體、SQL Azure 與金鑰分析和智慧服務等基本的服務，都已經提供靜態加密選項。 這些服務有部分會支援客戶控制的金鑰和用戶端加密，以及服務管理的金鑰和加密。 Microsoft Azure 服務針對要在其他可用性強化加密和新的選項已計劃預覽和公開上市 hello 未來幾個月。

