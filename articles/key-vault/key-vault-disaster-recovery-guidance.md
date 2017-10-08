---
title: "在 Azure 金鑰保存庫會影響 Azure 服務中斷的 hello 事件 aaaWhat toodo |Microsoft 文件"
description: "了解哪些 toodo hello 事件的 Azure 服務中斷影響 Azure 金鑰保存庫中。"
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a>Azure 金鑰保存庫的可用性與備援
Azure 金鑰保存庫功能備援性 toomake 確保您的金鑰和密碼保持可用 tooyour 應用程式即使 hello 的個別元件服務失敗的多個圖的層。

hello 金鑰保存庫的內容都會複寫 hello 區域與 tooa 次要區域內至少 150 英哩離開但 hello 內相同的地理位置。 這可維持您金鑰和密碼的高持久性。 請參閱 hello [Azure 配對區域](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions)如需詳細資訊，針對特定區域對文件。

如果 hello 金鑰保存庫服務內的個別元件失敗，hello 區域內的其他元件中的步驟 tooserve 您要求 toomake 確定沒有任何功能降低。 您不需要 tootake 任何動作 tootrigger 這。 它會自動發生，且將透明 tooyou。

自動路由在 hello 罕見事件中的整個 Azure 區域，就無法使用，您對 Azure 金鑰保存庫，在該區域中的 hello 要求 (*容錯*) tooa 次要區域。 Hello 主要區域再次可用時，要求會路由回到 (*無法回*) toohello 主要區域。 同樣地，您不需要 tootake 任何動作因為這會自動發生。

有幾個警告 toobe 留意：

* 在 hello 事件中的區域容錯移轉，可能需要幾分鐘，讓 hello 服務 toofail。 在這段期間發出的要求可能會失敗，直到 hello 容錯移轉完成為止。
* 容錯移轉完成之後，您的金鑰保存庫會處於唯讀模式。 在此模式中支援的要求是：
  * 列出金鑰保存庫
  * 取得金鑰保存庫的屬性
  * 列出密碼
  * 取得密碼
  * 列出金鑰
  * 取得金鑰 (的屬性)
  * 加密
  * 解密
  * 包裝
  * 解除包裝
  * Verify
  * 簽署
  * 備份
* 在容錯移轉進行容錯回復之後，所有要求類型 (包括讀取「和」寫入要求) 都會可供使用。

