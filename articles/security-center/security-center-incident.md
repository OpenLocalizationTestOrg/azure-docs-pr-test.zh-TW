---
title: "在 Azure 資訊安全中心 aaaHandling 安全性警示 |Microsoft 文件"
description: "這份文件可協助您 toouse Azure 資訊安全中心功能 toohandle 安全性事件。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: edb911c298a2ce93cd0ea5b22ce002005040090f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a>在 Azure 資訊安全中心處理安全性事件
分級和調查安全性警示可能會很費時甚至 hello 熟練安全性分析師和許多很難 tooeven 知道哪裡 toobegin。 使用[分析](security-center-detection-capabilities.md)tooconnect hello 資訊之間相異[安全性警示](security-center-managing-and-responding-alerts.md)、 資訊安全中心可以提供攻擊行銷活動的單一檢視，和所有 hello 相關警示 – 您可以快速了解採用何種動作 hello 攻擊者，以及哪些資源受到影響。

本文將討論如何 toouse 安全性警示功能的資訊安全中心 tooassist 您處理安全性事件。

## <a name="what-is-a-security-incident"></a>什麼是安全性事件？
在資訊安全中心內，安全性事件是符合 [攻擊鏈](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) 模式之資源的所有警示彙總。 事件會出現在 hello[安全性警示](security-center-managing-and-responding-alerts.md)磚和刀鋒視窗。 事件會顯示 hello 相關警示清單，可讓您 tooobtain 每次出現的詳細資訊。

## <a name="managing-security-incidents"></a>管理安全性事件
您可以藉由查看 hello 安全性警示磚檢閱目前的安全性事件。 存取 hello Azure 入口網站，並遵循每個安全性事件的詳細的 toosee hello 步驟：

1. 在 hello 資訊安全中心儀表板中，您會看到 hello**安全性警示**磚。

    ![資訊安全中心的 [安全性警示] 圖格](./media/security-center-incident/security-center-incident-fig1.png)

2. 按一下此磚 tooexpand，如果安全性事件偵測到，它會出現在 hello 安全性警示圖形如下所示：

    ![安全性事件](./media/security-center-incident/security-center-incident-fig2.png)

3. 請注意 hello 安全性事件描述有不同的圖示比較 tooother 警示。 按一下以 tooview 更詳細說明有關此事件。

    ![安全性事件](./media/security-center-incident/security-center-incident-fig3.png)

4. 在 hello**事件**刀鋒視窗，您將查看更多的詳細說明關於此安全性事件，其中包括完整描述，其嚴重性 （即在此情況下高），其目前狀態 (在此情況下仍*主動*，這表示 hello 使用者尚未採取動作 tooit-作法是以滑鼠右鍵按一下在 hello hello 事件**安全性警示**刀鋒視窗)，hello 遭受攻擊的資源 (在此情況下*VM1*)，hello hello 事件的修復步驟，而且 hello 下方窗格中，您必須已包含在此事件中的 hello 警示。 如果您想 tooobtain 上每個警示的詳細資訊，直接按一下它和另一個刀鋒視窗上的開啟，如下所示：

    ![安全性事件](./media/security-center-incident/security-center-incident-fig4.png)

在這個刀鋒視窗上的 hello 資訊而異相應 toohello 警示。 讀取[中 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)如需有關如何 toomanage 這些警示。 關於這項功能的一些重要考量︰

* 新的篩選器可讓您 toocustomize 檢視 tooIncident，警示，或兩者。
* 相同的警示可以存在的事件 （如果適用），以及顯示為獨立警示 toobe 一部分的 hello。

## <a name="see-also"></a>另請參閱
在本文件中，您學會如何 toouse hello 資訊安全中心的安全性事件功能。 toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [管理及回應 toosecurity Azure 資訊安全中心警示](security-center-managing-and-responding-alerts.md)
* [Azure 資訊安全中心的偵測功能](security-center-detection-capabilities.md)
* [Azure 資訊安全中心規劃和操作指南](security-center-planning-and-operations-guide.md)
* [管理及回應 toosecurity Azure 資訊安全中心警示](security-center-managing-and-responding-alerts.md)
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-- 尋找有關 Azure 安全性與相容性的部落格文章。
