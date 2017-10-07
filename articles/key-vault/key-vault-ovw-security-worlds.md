---
ms.assetid: 
title: "aaaAzure 金鑰保存庫安全園地 |Microsoft 文件"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 1995119c9e9886829d6c50af921f275d10e382f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a>Azure Key Vault 安全世界和地理界限

Azure Key Vault 是多租用戶服務，並且在每個 Azure 位置使用硬體安全模組 (HSM) 的集區。 

所有的 Hsm 在 hello 的 Azure 位置上相同的地理區域共用 hello 相同的密碼編譯界限 （Thales 安全園地）。 例如，美國東部和共用美國西部 hello 相同的安全園地，因為它們隸屬 toohello 美國地理位置。 同樣地，所有的 Azure 位置，在日本共用 hello 相同的安全園地和所有的 Azure 位置，澳洲、 印度、 等等。 

## <a name="backup-and-restore-behavior"></a>備份與還原行為

其中一個 Azure 位置可以是金鑰保存庫的金鑰建立的備份還原 tooa 金鑰保存庫中其他的 Azure 位置，只要這些條件都成立：

- 這兩個 hello Azure 位置所屬 toohello 相同的地理位置
- 這兩個金鑰保存庫 hello 隸屬 toohello 相同的 Azure 訂用帳戶

比方說，印度西部金鑰保存庫中的索引鍵中的指定訂用帳戶所建立的備份只能還原的 tooanother hello 在金鑰保存庫相同的訂用帳戶和地理位置。印度西部、 印度中部或印度南部及印度。

## <a name="regions-and-products"></a>區域和產品

- [Azure 區域](https://azure.microsoft.com/regions/)
- [依區域的 Microsoft 產品](https://azure.microsoft.com/regions/services/)

區域是對應的 toosecurity 領域，顯示為在 hello 資料表中的主要標頭：

在 hello 產品中由區域發行項，例如 hello**美洲** 索引標籤包含東部 US，美國中部、 美國西部所有對應 toohello 美洲區域。 

>[!NOTE]
>例外狀況是美國 DOD 東部和美國 DOD 中部有自己的安全世界。 

同樣地，在 hello**歐洲**索引標籤，北歐和西歐都對應 toohello 歐洲地區。 hello 相同也是如此上 hello**亞太地區** 索引標籤。



