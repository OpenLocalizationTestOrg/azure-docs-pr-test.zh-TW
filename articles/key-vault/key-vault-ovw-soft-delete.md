---
ms.assetid: 
title: "aaaAzure 金鑰保存庫虛刪除 |Microsoft 文件"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/10/2017
ms.openlocfilehash: 1b402c58db6f25ae4ae5e2720786fa81eb0e839a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-soft-delete-overview"></a>Azure Key Vault 虛刪除概觀

金鑰保存庫虛刪除功能可讓 hello 刪除保存庫與保存庫的物件，稱為 「 虛刪除的復原。 具體來說，我們解決 hello 下列案例：

- 可復原的 Key Vault 刪除支援
- 可復原的 Key Vault 物件刪除支援 (物件的範例如： 金鑰、密碼和憑證)

## <a name="supporting-interfaces"></a>支援的介面

hello 虛刪除功能是一開始可透過 hello 其餘部分，.NET / C# 和 PowerShell 介面。 如需詳細資訊，這些參考 toohello 參考[金鑰保存庫參考](https://docs.microsoft.com/azure/key-vault/)。

## <a name="scenarios"></a>案例

Azure Key Vault 是由 Azure Resource Manager 管理的追蹤資源。 Azure Resource Manager 也會指定妥善定義的刪除行為，而成功的「刪除」作業必須使資源無法再被存取。 hello 刪除是否意外或故意情況下，hello 虛刪除功能位址 hello 復原刪除的 hello 物件。

1. 在 hello 一般案例中，使用者可能不小心刪除金鑰保存庫或金鑰保存庫的物件。如果該金鑰保存庫或金鑰保存庫物件已預先決定的期間內的可復原 toobe，hello 使用者可能會恢復 hello 刪除作業，並復原其資料。

2. 在不同的案例中，惡意使用者可能會嘗試 toodelete 金鑰保存庫或金鑰保存庫的物件，例如金鑰在保存庫，toocause 業務中斷。 Hello 刪除 hello 金鑰保存庫或金鑰保存庫的物件區隔開 hello 實際刪除基礎資料的 hello 可以做為安全起見，比方說，限制的權限的資料刪除 tooa 不同，信任的角色。 實際上，此方法這需要作業仲裁，否則可能導致直接的資料遺失。

### <a name="soft-delete-behavior"></a>虛刪除行為

利用此功能，hello 金鑰保存庫上的刪除作業，或金鑰保存庫的物件是虛刪除，有效地保留 hello 資源為指定的保留期限，讓該 hello 物件 hello 外觀刪除時。 進一步 hello 服務會提供一個機制，來復原刪除的 hello 物件，基本上復原 hello 刪除。 

虛刪除是選擇性的 Key Vault 行為，在此版本中**預設未啟用**。 如需啟用虛刪除金鑰保存庫的詳細資訊，請參閱 hello hello 參考您的選擇，hello 介面中的特定指導方針[金鑰保存庫參考](https://docs.microsoft.com/azure/key-vault/)。

### <a name="key-vault-recovery"></a>Key Vault 復原

一旦刪除金鑰保存庫，hello 服務會建立下 hello 訂用帳戶，加入足夠的中繼資料進行復原的 proxy 資源。 hello proxy 資源是預存的物件，用於 hello 與 hello 刪除金鑰保存庫相同的位置。 

### <a name="key-vault-object-recovery"></a>Key Vault 物件復原

一旦刪除金鑰保存庫物件，例如機碼，hello 服務會將 hello 物件處於已刪除狀態，使它無法存取 tooany 擷取作業。 處於此狀態時，hello 金鑰保存庫的物件只能列出，復原，或強制/永久刪除。 

在 hello 相同時間、 金鑰保存庫會排程的基礎資料的對應 toohello 刪除 hello hello 刪除金鑰保存庫或預先決定的保留間隔之後執行的金鑰保存庫物件。 hello DNS 記錄對應 toohello 的保存庫也會保留 hello hello 保留間隔持續時間。

### <a name="soft-delete-retention-period"></a>虛刪除保留期限

虛刪除的資源預設會保留 90 天的時間。 在 hello 虛刪除保留間隔內，hello 下列適用於：

- 您可能會列出所有的 hello 金鑰保存庫和金鑰保存庫中的物件，您的訂用帳戶以及存取其相關的刪除和復原資訊 hello 虛刪除狀態。
    - 只有具備特殊權限的使用者可以列出已刪除的保存庫。 我們建議使用者建立具有這些特殊權限的自訂角色，以處理刪除的保存庫。
- 無法在 hello 建立相同名稱的 hello 與金鑰保存庫相同的位置。相對的只要該金鑰的保存庫包含 hello 的物件，金鑰保存庫物件就無法建立在指定的保存庫中相同名稱和哪個是處於已刪除的狀態 
- 只有特別特殊權限的使用者可能會藉由發出 hello 對應 proxy 資源上的復原命令還原金鑰保存庫或金鑰保存庫的物件。
    - hello 使用者角色的成員 hello 自訂，擁有 hello 權限 toocreate hello 資源群組下的金鑰保存庫可以還原 hello 保存庫。
- 只有特別特殊權限的使用者強制可能刪除金鑰保存庫或金鑰保存庫的物件發出刪除命令 hello 對應 proxy 資源上。

復原金鑰保存庫或金鑰保存庫物件，除非在 hello 結束 hello 保留間隔 hello 服務會執行清除虛刪除的 hello 金鑰保存庫或金鑰保存庫的物件和其內容。 資源刪除作業無法重新排程。

### <a name="permitted-purge"></a>允許的清除作業

永久刪除、 清除、 金鑰保存庫可透過 hello proxy 資源的 POST 作業，而需要特殊權限。 一般而言，只有 hello 訂用帳戶擁有者將能夠 toopurge 金鑰保存庫。 hello POST 作業觸發程序 hello 立即且無法復原刪除該保存庫。 

例外狀況 toothis 是 hello 情況 hello Azure 訂用帳戶已被標示為*undeletable*。 在此情況下，只有 hello 服務然後可能會執行 hello 實際刪除，而且也這麼做為排程的處理序。 



