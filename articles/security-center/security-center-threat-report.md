---
title: "資訊安全中心 threat intelligence 報表 aaaAzure |Microsoft 文件"
description: "這份文件可協助您 toouse Azure 安全性中心威脅智慧型報告期間調查 toofind 有關安全性警示的詳細資訊。"
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5662e312-e8c2-4736-974e-576eeb333484
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: c888cfac1dd8b057616a6b8e6c6f6b67b552f2e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-threat-intelligence-report"></a>Azure 資訊安全中心威脅情報報告
本文件說明 Azure 資訊安全中心威脅情報報告可如何協助您深入了解產生安全性警示的威脅。

## <a name="what-is-a-threat-intelligence-report"></a>何謂威脅情報報告？
資訊安全中心威脅偵測的運作方式是監視從您的 Azure 資源、 hello 網路和連線的交易夥伴方案的安全性資訊。 它會分析這項資訊通常相互關聯多個來源，tooidentify 威脅的資訊。 此程序屬於 hello 資訊安全中心[偵測功能](security-center-detection-capabilities.md)。

當資訊安全中心識別到威脅時，便會觸發[安全性警示](security-center-managing-and-responding-alerts.md)，其內含關於特定事件的詳細資訊，包括修復方面的建議。 tooassist 事件回應小組調查並補救威脅，資訊安全中心包含威脅情報包含報表的 hello 威脅所偵測到，包括下列資訊的相關資訊:

* 攻擊者的身分識別或關聯 (如果有提供這項資訊)
* 攻擊者的目標
* 目前和過往的攻擊活動 (如果有提供這項資訊)
* 攻擊者的策略、工具和程序
* 關聯的入侵指標 (IoC)，例如 URL 和檔案雜湊
* Victimology，也就是 hello 產業和地理普遍性 tooassist 您在判斷您的 Azure 資源有風險
* 緩和與修復資訊

> [!NOTE]
> hello 任何特定的報表中的資訊數量而異。hello 層級的詳細資料根據 hello 惡意程式碼的活動和普遍性而定。
>
>

資訊安全中心有三種類型的威脅的報表，所以可能會相應 toohello 攻擊。 可用的 hello 報告為：

* **群組活動報告**︰提供攻擊者、其目標和策略的深入探討。
* **活動報告**︰著重說明特定攻擊活動的詳細資料。
* **威脅 [摘要] 報表**： 涵蓋所有 hello hello 先前的兩個報表中的項目。

這種類型的資訊會很有幫助期間 hello[事件回應](security-center-incident-response.md)處理序中，沒有 hello 攻擊、 hello 攻擊者的動機，以及正在進行調查 toounderstand hello 來源 toodo toomitigate 這繼續進行後續步驟發生問題。

## <a name="how-tooaccess-hello-threat-intelligence-report"></a>如何 tooaccess hello threat intelligence 報表嗎？
您可以檢閱您目前的警示，藉由查看 hello**安全性警示**磚。 開啟 hello Azure 入口網站，並遵循以下 toosee hello 步驟有關每種警示的更多詳細資料：

1. 在 hello 資訊安全中心儀表板中，您會看到 hello**安全性警示**磚。
2. 按一下 hello 磚 tooopen hello**安全性警示**刀鋒視窗，其中包含 hello 警示的更多詳細資料，然後按一下您想 tooobtain hello 安全性警示中的詳細資訊的相關。

    ![安全性警示](./media/security-center-threat-report/security-center-threat-report-fig1.png)
3. 在此情況下 hello**可疑的處理程序執行**刀鋒視窗會顯示 hello hello 圖所示的 hello 警示的詳細資料：

    ![安全性警示詳細資料](./media/security-center-threat-report/security-center-threat-report-fig2.png)
4. hello 可用於每個安全性警示的資訊數量而異相應 toohello 類型的警示。 在 hello**報表**您有一個連結 toohello threat intelligence 報表的欄位。 按一下連結，便會出現另一個含有 PDF 檔案的瀏覽器視窗。

   ![儲存體選擇](./media/security-center-threat-report/security-center-threat-report-fig3.png)

從這裡您可以下載的 hello 偵測到此報表和讀取 hello 安全性問題的 PDF，並根據所提供的 hello 資訊採取動作。

## <a name="see-also"></a>另請參閱
在本文件中，您已了解 Azure 資訊安全中心威脅情報報告如何在安全性警示調查期間幫上忙。 toolearn 進一步了解 Azure 資訊安全中心，請參閱 hello 下列資訊：

* [Azure 資訊安全中心常見問題集](security-center-faq.md)。 尋找有關使用 hello 服務常見問題。
* [善用 Azure 資訊安全中心進行事件回應](security-center-incident-response.md)
* [Azure 資訊安全中心的偵測功能](security-center-detection-capabilities.md)
* [Azure 資訊安全中心規劃和操作指南](security-center-planning-and-operations-guide.md)。 深入了解如何 tooplan 並了解 hello 設計考量 tooadopt Azure 資訊安全中心。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)。 深入了解如何 toomanage 和回應 toosecurity 警示。
* [在 Azure 資訊安全中心處理安全性事件](security-center-incident.md)
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)。 尋找有關 Azure 安全性與相容性的部落格文章。
