---
title: "在 Azure 資訊安全中心 aaaManage 安全性警示 |Microsoft 文件"
description: "這份文件可協助您 toouse Azure 資訊安全中心功能 toomanage，以及回應 toosecurity 警示。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a>管理及回應 toosecurity Azure 資訊安全中心警示
這份文件可協助您使用 Azure 資訊安全中心 toomanage 和回應 toosecurity 警示。

> [!NOTE]
> 升級 tooAzure 安全性 Center 標準 tooenable 進階偵測。 提供 60 天的免費試用。 tooupgrade，選取定價層 hello[安全性原則](security-center-policies.md)。 請參閱[Azure 資訊安全中心定價](security-center-pricing.md)toolearn 更多。
>
>

## <a name="what-are-security-alerts"></a>什麼是安全性警示：
資訊安全中心會自動收集、 分析時，整合記錄資料從您的 Azure 資源，hello 網路和連接協力廠商解決方案，例如防火牆和 endpoint protection 解決方案，toodetect 威脅，並且減少誤判。 優先順序的安全性警示的清單會顯示在資訊安全中心，以及 hello 資訊需要 tooquickly 調查 hello 問題，並建議如何 tooremediate 攻擊。


> [!NOTE]
> 如需資訊安全中心偵測功能運作方式的詳細資訊，請閱讀 [Azure 資訊安全中心的偵測功能](security-center-detection-capabilities.md)。
>
>

## <a name="managing-security-alerts"></a>管理安全性警示
您可以檢閱您目前的警示，藉由查看 hello**安全性警示**磚。 開啟 Azure 入口網站，並遵循下方 toosee hello 步驟有關每種警示的更多詳細資料：

1. 在 hello 資訊安全中心儀表板中，您會看到 hello**安全性警示**磚。

    ![資訊安全中心的 [安全性警示] 圖格](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. 按一下 hello 磚 tooopen hello**安全性警示**刀鋒視窗，其中包含更多詳細 hello 警示如下所示。

   ![hello 安全性警示 刀鋒視窗中的資訊安全中心](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

在 hello 此刀鋒視窗的下半部是 hello 每個警示的詳細資料。 toosort，按一下您想要依 toosort hello 資料行。 每個資料行的 hello 定義如下所示：

* **描述**: hello 警示的簡短說明。
* **計數**：在特定一天偵測到這個特定類型的所有警示清單。
* **偵測到**: hello 負責觸發 hello 警示的服務。
* **日期**: hello 日期 hello 事件發生。
* **狀態**: hello 該警示的目前狀態。 狀態分為兩種：
  * **Active**： 已偵測到 hello 安全性警示。
* **嚴重性**: hello 嚴重性層級，它可以是高、 中或低。

### <a name="filtering-alerts"></a>篩選警示
您可以根據日期、狀態及嚴重性來篩選警示。 篩選警示可用於案例中您需要的安全性警示顯示 toonarrow hello 範圍。 例如，可能您想 tooaddress 就會發生在 hello 過去 24 小時您正在調查可能違反 hello 系統中的安全性警示。

1. 按一下**篩選**上 hello**安全性警示**刀鋒視窗。 hello**篩選**刀鋒視窗會開啟，並選取您想 toosee hello 日期、 狀態和嚴重性值。

    ![篩選資訊安全中心的警示](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a>回應 toosecurity 警示
選取 安全性警示 toolearn hello 事件觸發 hello 警示，以及項目，如果有的話會引導您有關需要 tootake tooremediate 攻擊。 安全性警示會依類型及日期區分。 按一下 安全性警示，會開啟刀鋒視窗中包含的 hello 分組警示清單。

![回應 toosecurity Azure 資訊安全中心警示](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

在此情況下，所觸發的 hello 警示，請參閱 toosuspicious 遠端桌面通訊協定 (RDP) 活動。 hello 第一個資料行顯示的受攻擊的資源;hello 第二個顯示多少次 hello 資源遭到攻擊。hello 第三個 hello 時間顯示 hello 攻擊。hello 第四個顯示 hello 警示; 狀態並 hello 第五個顯示 hello 嚴重性 hello 攻擊。 檢閱此資訊之後，按一下 遭到攻擊的 hello 資源，並且會在開啟的新刀鋒視窗。

![Azure 資訊安全中心中的哪些 toodo 安全性的相關警示的建議](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

在 hello**描述**欄位的這個刀鋒視窗中您會發現此事件的詳細。 適用的 hello 來源 IP 位址，以及如何提出建議時，這些額外的詳細資料提供深入了解哪些 hello 觸發的安全性警示，hello 目標資源，tooremediate。  在某些情況下，hello 來源 IP 位址會是空的 （不適用） 因為並非所有的 Windows 安全性事件記錄檔包含 hello IP 位址。

資訊安全中心所建議的 hello 補救異相應 toohello 安全性警示。 在某些情況下，您可能會有 toouse 其他的 Azure 功能 tooimplement hello 建議補救。 這種攻擊是 tooblacklist hello IP 位址，使用產生這種攻擊，例如 hello 補救[網路 ACL](../virtual-network/virtual-networks-acl.md)或[網路安全性群組](../virtual-network/virtual-networks-nsg.md)規則。

> [!NOTE]
> Hello 不同類型警示的詳細資訊，請參閱[Azure 資訊安全中心中的型別安全性警示](security-center-alerts-type.md)。
>
>

## <a name="see-also"></a>另請參閱
在本文件中，您學到如何 tooconfigure 資訊安全中心的安全性原則。 toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心處理安全性事件](security-center-incident.md)
* [Azure 資訊安全中心的偵測功能](security-center-detection-capabilities.md)
* [Azure 資訊安全中心規劃和操作指南](security-center-planning-and-operations-guide.md)
* [Azure 資訊安全中心常見問題集](security-center-faq.md)— 尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) — 尋找有關 Azure 安全性與相容性的部落格文章。
