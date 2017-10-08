---
title: "aaaUsing hello 系統管理員和使用者入口網站在 Azure 堆疊 |Microsoft 文件"
description: "了解 hello Azure 堆疊中 hello 系統管理員和使用者入口網站之間的差異。"
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: 02c7ff03-874e-4951-b591-28166b7a7a79
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: twooley
ms.openlocfilehash: 5e940749917e4aade26483a79bcc238346bf94f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-administrator-and-user-portals-in-azure-stack"></a>使用 Azure 堆疊中的 hello 系統管理員和使用者入口網站

Azure 堆疊; 中有兩個入口網站hello 管理員入口網站和 hello 使用者入口網站 (也稱為 tooas hello*租用戶*入口網站)。 hello 入口網站是由個別執行個體的 Azure 資源管理員支援。

hello 下表顯示如何 tooconnect toohello 入口網站和 Azure 堆疊開發套件環境中的 tooResource 管理員端點。

|  入口網站 | 入口網站 URL | Resource Manager 端點 URL |   
| -------- | ------------- | ------- |  
| 系統管理員 | https://adminportal.local.azurestack.external  | https://adminmanagement.local.azurestack.external  |  
| User | https://portal.local.azurestack.external | https://management.local.azurestack.external  |
| | |

## <a name="hello-administrator-portal"></a>hello 管理員入口網站

hello 管理員入口網站可讓雲端操作員 tooperform 系統管理和操作工作。 雲端操作員可執行下列工作：
* 監視健康情況和警示
* 管理容量
* 填入 hello marketplace
* 建立方案和產品
* 為租用戶建立訂用帳戶

雲端操作員也可以建立資源，例如虛擬機器、虛擬網路和儲存體帳戶。

 ![hello 管理員入口網站](media/azure-stack-manage-portals/image1.png)

 ## <a name="hello-user-portal"></a>hello 使用者入口網站

 hello 使用者入口網站不提供存取 tooany hello 管理或操作功能的 hello 管理員入口網站。 在 hello 使用者入口網站，使用者可以訂閱 toopublic 優惠，並使用都可透過這些服務的 hello 服務。

  ![hello 使用者入口網站](media/azure-stack-manage-portals/image2.png)
 
 ## <a name="subscription-behavior"></a>訂用帳戶行為
 
 請確定您了解 hello 遵循 hello 兩個入口網站中的訂用帳戶行為之間的差異。

 系統管理員入口網站：
* 沒有可用 hello 管理員入口網站中只有一個訂用帳戶。 此訂用帳戶為 hello*預設提供者訂閱*。 您無法加入 hello 管理員入口網站使用任何其他訂用帳戶。
* 雲端操作員，您可以從 hello 管理員入口網站訂用帳戶加入為您的使用者 （包括您自己）。 （包括您自己） 的使用者可以存取和使用這些訂用帳戶，從 hello 使用者入口網站。

  >[!NOTE]
  Hello Azure 資源管理員分離，因為訂用帳戶不會跨越入口網站。 例如，如果您為雲端操作員登入 toohello 使用者入口網站，您無法存取 hello 預設提供者訂用帳戶。 因此，您不需要存取 tooany 管理功能。 您可從公用產品為自己建立訂用帳戶，但系統仍會將您視為租用戶使用者。

使用者入口網站：
* 在 hello 使用者入口網站的帳戶可以有多個訂用帳戶。

  >[!NOTE]
  Hello 套件在開發環境中，如果租用戶使用者所屬 toohello 相同的目錄 hello 雲端操作員，它們不會封鎖在 toohello 管理員入口網站登入。 不過，就無法存取任何 hello 管理功能。 此外，它們無法加入訂用帳戶或存取提供可用 toothem 源自 hello 使用者入口網站中。

## <a name="next-steps"></a>後續步驟

[連接 tooAzure 堆疊](azure-stack-connect-azure-stack.md)

[Azure Stack 中的區域管理](azure-stack-region-management.md)
