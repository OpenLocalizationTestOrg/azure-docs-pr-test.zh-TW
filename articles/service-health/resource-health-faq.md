---
title: "aaaAzure 資源健全狀況常見問題集 |Microsoft 文件"
description: "Azure 資源健康狀態的概觀"
services: Resource health
documentationcenter: dev-center-name
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/05/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fe29b2df1f9fee4b77d0100c7d872df837dc4b4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-faq"></a>Azure 資源健康狀態常見問題集
了解 hello 解答了 toocommon 有關 Azure 資源健全狀況。

## <a name="what-is-azure-resource-health"></a>何謂 Azure 資源健康狀態？
當 Azure 問題影響到您的資源健康狀態時，協助進行診斷並取得支援。 它會通知您有關 hello 目前和過去健康情況的資源，並協助您解決問題。 資源健康狀態會在您需要解決 Azure 服務問題時提供技術支援。  

## <a name="what-is-hello-resource-health-intended-for"></a>什麼是資源健全狀況適用於 hello？
一旦偵測到的問題與資源，資源健全狀況可協助您診斷 hello 根本原因。 它提供說明 toomitigate hello 問題和技術支援人員時需要更多說明 Azure 服務的問題。

## <a name="what-health-checks-are-performed-by-resource-health"></a>資源健康狀態會執行哪些健康狀態檢查？
資源健全狀況執行各種檢查，根據 hello[資源類型](resource-health-checks-resource-types.md)。 這些檢查包括設計的 tooimplement 三種問題： 
- 未規劃的事件，例如未預期的主機重新開機
- 規劃的事件，例如排程的主機作業系統更新
- 使用者動作觸發的事件，例如使用者重新啟動虛擬機器

## <a name="what-does-each-of-hello-health-status-mean"></a>每個 hello 健全狀況狀態是什麼意思？
有三個不同的健全狀態︰
- 可用： 沒有任何已知的問題中 hello 可能正影響此資源的 Azure 平台
- 無法使用： 資源健全狀況偵測到會影響 hello 資源的問題
- 未知： 資源健康情況無法判斷資源的 hello 健全狀況因為它已經停止接收其相關資訊。 

## <a name="what-does-hello-unknown-status-mean-is-something-wrong-with-my-resource"></a>功能沒有 hello 未知的狀態標準嗎？ 我的資源有什麼問題嗎？
hello 健全狀況狀態會設定 toounknown，當資源健全狀況會停止接收特定資源的相關資訊。 雖然這個狀態不是最終指示 hello 狀態 hello 資源，請在您遇到的問題，可能表示發生 Azure 的問題。

## <a name="how-can-i-get-help-for-a-resource-that-is-unavailable"></a>如何取得無法使用的資源說明？
您可以提交支援要求的 hello 資源健全狀況 刀鋒視窗。 Hello 資源無法使用時不需要支援合約與 Microsoft tooopen 要求因為平台事件。

## <a name="does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did"></a>資源健康狀態是否會區分依平台問題歸類為無法使用的案例與我所做的事情？
[是]，資源無法使用時，資源健全狀況會識別其中一個類別中的 hello 根本原因： 
-   使用者啟動的動作
-   規劃的事件 
-   未規劃的事件

在 hello 入口網站會顯示使用者起始動作使用藍色的通知圖示，而使用紅色警告圖示顯示計劃與非計劃的事件。 提供詳細資訊在 hello[資源健全狀況概觀](Resource-health-overview.md)。  

## <a name="can-i-integrate-resource-health-with-my-monitoring-tools"></a>可以將資源健康狀態與我的監視工具進行整合嗎？
資源健全狀況是您診斷及降低 Azure 服務的問題會影響您的資源服務，其設計的 toohelp。 雖然您可以使用 hello 資源健全狀況 API tooprogrammatically 取得 hello 健全狀況狀態，我們建議使用度量 toomonitor 您的資源。 一旦偵測到問題時，資源健全狀況可協助您判斷 hello 根本原因，並引導您完成動作 tooaddress 它們。 請瀏覽[Azure 監視器](https://docs.microsoft.com/azure/monitoring-and-diagnostics/)toolearn 深入了解如何使用度量 toocheck 您的資源。

## <a name="where-do-i-find-resource-health"></a>哪裡可以找到資源健康狀態？
在您登入 toohello Azure 入口網站之後，有多個方式可以存取資源健全狀況：
- 瀏覽 tooyour 資源。 在 hello 左側導覽中，選取 **資源健全狀況**
- 移 toohello Azure 監視器刀鋒視窗。  在 hello 左側導覽中，選取 **資源健全狀況**。
- 開啟 hello**說明 + 支援**刀鋒視窗中選取 hello 問號 hello 右上角的 hello 入口網站，然後選取 **說明 + 支援**。 一旦 hello 刀鋒視窗中開啟時，請選取**資源健全狀況**

您也可以使用 hello 資源健全狀況 API tooobtain hello 健全狀況的資訊資源。

## <a name="is-resource-health-available-for-all-resource-types"></a>資源健康狀態是否適用於所有的資源類型？
hello 健全狀況檢查和支援透過資源健全狀況的資源類型的清單可以找到[這裡](resource-health-checks-resource-types.md)。

## <a name="what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not"></a>如果我的資源顯示無法使用，但我認為它可以使用，該怎麼辦？
檢查資源的 hello 健全狀況下 hello 健全狀況狀態，, 您可以按一下 **報告不正確的健全狀況狀態**。 之前送出 hello 報表，您可以先 hello 選項提供您為何認為 hello 目前的健全狀況狀態不正確的其他詳細資料。

## <a name="is-resource-health-available-for-all-azure-regions"></a>資源健康狀態是否適用於所有的 Azure 區域？ 
資源健全狀況有跨所有 Azure geos，除了下列區域的 hello:
- 美國政府維吉尼亞州
- 美國政府愛荷華州
- 美國 DoD 東部
- 美國國防部中央
- 德國中部
- 德國東北部
- 中國東部
- 中國北部

## <a name="how-is-resource-health-different-from-hello-service-health-dashboard-or-hello-azure-portal-service-notifications"></a>如何為資源健全狀況不同 hello 服務健全狀況儀表板或 hello Azure 入口網站服務通知？
所提供的 hello Azure 服務健全狀況儀表板更特定的資源健全狀況所提供的 hello 資訊。

而[Azure 狀態](https://status.azure.com)和 hello 入口網站服務通知可通知您有關服務的問題會影響一組廣泛的客戶 （例如 Azure 地區）、 資源健全狀況公開才相關的更多細微性事件toohello 特定資源。 例如，如果主機意外重新啟動，資源健康狀態只會警示虛擬機器在該主機上執行的客戶。

它是重要的 toonotice 該 tooprovide 完成事件影響您的資源，資源健全狀況也在服務通知發行事件介面的可見性，而且 hello 服務健全狀況儀表板。

## <a name="do-i-need-tooactivate-resource-health-for-each-resource"></a>需要針對每個資源 tooactivate 資源健康情況嗎？
否，健康情況資訊適用於可透過資源健康狀態提供的所有資源類型。 

## <a name="do-we-need-tooenable-resource-health-for-my-organization"></a>我們讓我的組織需要 tooenable 資源健全狀況？
否。  Hello 不需要進行任何設定的 Azure 入口網站內存取 azure 資源健全狀況。

## <a name="is-resource-health-available-free-of-charge"></a>是否可免費使用資源健康狀態？
是。  Azure 資源健康狀態是免費的。

## <a name="what-are-hello-recommendations-that-resource-health-provides"></a>提供資源健全狀況的 hello 建議有哪些？
根據 hello 健全狀況狀態，資源健全狀況為您提供您所花費的疑難排解建議 hello 目標是減少 hello 時間。 如需可用的資源，hello 建議焦點放在 toosolve hello 最常見的問題客戶遇到的方式。 如果無法使用，因為在 hello 資源 tooan Azure 未規劃的事件，hello 焦點會在您的協助期間和之後 hello 復原程序。 

## <a name="next-steps"></a>後續步驟

深入了解資源健康狀態：
-  [Azure 資源健康狀態概觀](Resource-health-overview.md)
-  [可透過 Azure 資源健康狀態使用的資源類型和健康檢查](resource-health-checks-resource-types.md)
