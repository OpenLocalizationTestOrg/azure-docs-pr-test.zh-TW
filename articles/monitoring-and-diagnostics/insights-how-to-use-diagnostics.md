---
title: "aaaEnable 監視和 Microsoft Azure 中的診斷 |Microsoft 文件"
description: "深入了解如何針對您在 Azure 中的資源的診斷 tooset。"
author: rboucher
manager: carolz
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: af1947a9-c211-4aa1-8924-880a86240be4
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 865d010c5846fff6d871e20eca2bc4ac35028354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-monitoring-and-diagnostics"></a>啟用監視和診斷
在 hello [Azure 入口網站](https://portal.azure.com)，可以設定資源的相關豐富、 頻繁，監視和診斷資料。 您也可以使用 hello [REST API](https://msdn.microsoft.com/library/azure/dn931932.aspx)或[.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooconfigure 診斷以程式設計的方式。

在 Azure 中的診斷、監視和計量資料會被儲存到您所選擇的儲存體帳戶。 這可讓您 toouse 任何 tooling tooread hello 資料，存放裝置總管 」 tooPower BI toothird 合作對象的工具。

## <a name="when-you-create-a-resource"></a>建立資源的時機
大部分服務可讓您 tooenable 診斷當您首次在 hello 建立[Azure 入口網站](https://portal.azure.com)。

1. 跳過**新增**並選擇您感興趣的 hello 資源。
2. 選取 [ **選用組態**]。
    ![診斷刀鋒視窗](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)
3. 選取 [診斷]，然後按一下 [開啟]。 您將需要您想要儲存的診斷 toobe toochoose hello 儲存體帳戶。 您將支付儲存體和交易的一般資料費率當您傳送診斷 tooa 儲存體帳戶。
4. 按一下**確定**和建立 hello 資源。

## <a name="change-settings-for-an-existing-resource"></a>變更現有資源的設定
如果您已經建立的資源，而您想 toochange hello 診斷設定 （資料收集，例如 toochange hello 層級），您可以在 hello Azure 入口網站中的該權限。

1. 移 toohello 資源，然後按一下 hello**設定**命令。
2. 選取 [ **診斷**]。
3. hello**診斷**刀鋒視窗都具有所有 hello 可能的診斷和監視該資源的集合資料。 某些資源您也可以選擇**保留**hello 資料，tooclean 的原則進行從儲存體帳戶。
    ![儲存體診斷](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)
4. 一旦您已選擇您的設定，請按一下 hello**儲存**命令。 它可能需要一點時資料 tooshow 監視設定，如果您要啟用它 hello 第一次。

### <a name="categories-of-data-collection-for-virtual-machines"></a>虛擬機器的資料收集類別
虛擬機器的所有標準和記錄檔會都記錄在一分鐘的時間間隔，因此您可以一律 hello 大部分新的資訊關於您的電腦。

* **基本計量** ：有關您的虛擬機器的健康情況計量，例如處理器與記憶體
* **網路和 Web 計量** ：有關您的網路連線與 Web 服務的計量
* **.NET 度量**: hello.NET 和 ASP.NET 應用程式的相關虛擬機器上執行的度量
* **SQL 計量** ：如果您執行的是 Microsoft SQL 服務，這會是其效能計量
* **Windows 事件應用程式記錄檔**： 傳送 toohello 應用程式通道的 Windows 事件
* **Windows 事件系統記錄檔**: toohello 系統通道傳送的 Windows 事件。 此事件同時包含來自 [Microsoft 反惡意程式碼](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409)(英文) 的所有事件。
* **Windows 事件安全性記錄檔**: toohello 安全性通道傳送的 Windows 事件
* **診斷基礎結構記錄檔**: hello 診斷收集基礎結構的相關記錄
* **IIS 記錄檔** ：有關 IIS 伺服器的記錄

請注意，此時不支援的 Linux 特定散發，而且，hello 客體代理程式必須安裝在 hello 虛擬機器。

## <a name="next-steps"></a>後續步驟
* 每當發生作業事件或計量超過臨界值時，[接收警示通知](insights-receive-alert-notifications.md)。
* [監視服務計量](insights-how-to-customize-monitoring.md)toomake 確定您的服務可用，並能繼續回應。
* [自動調整執行個體計數](insights-how-to-scale.md)toomake 確定您的服務標尺依照需求。
* [監視應用程式效能](../application-insights/app-insights-azure-web-apps.md)如果您想 toounderstand 完全如何您的程式碼執行 hello 雲端中。
* [檢視事件和活動記錄檔](insights-debugging-with-events.md)toolearn 所有發生在您的服務中的項目。
* [追蹤服務健全狀況](insights-service-health.md)toofind 出 Azure 時遇到效能降低或服務中斷。

