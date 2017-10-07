---
title: "503 服務無法使用 」 錯誤 aaaFix 502 不正確的閘道，|Microsoft 文件"
description: "針對 Azure App Service 所裝載之 Web 應用程式的「502 不正確的閘道」和「503 服務無法使用」錯誤進行疑難排解。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "502 不正確的閘道、503 服務無法使用、錯誤 503、錯誤 502"
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a>對您的 Azure Web 應用程式中「502 不正確的閘道」和「503 服務無法使用」的 HTTP 錯誤進行疑難排解
在裝載於 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)的 Web 應用程式中「502 不正確的閘道」和「503 服務無法使用」是常見的錯誤。 本文可協助您對這些錯誤進行疑難排解。

如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和 hello 堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。 或者，您也可以提出 Azure 支援事件。 移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)，然後按一下 **取得支援**。

## <a name="symptom"></a>徵狀
當您瀏覽 toohello web 應用程式時，它會傳回 HTTP 錯誤"502 不正確的閘道 」 或 HTTP"503 服務無法使用 」 錯誤。

## <a name="cause"></a>原因
此問題通常是因為應用程式層級問題所造成，例如：

* 要求耗費過長的時間
* 應用程式的記憶體/CPU 使用率過高
* 應用程式當機到期 tooan 例外狀況。

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a>疑難排解步驟 toosolve"502 不正確的閘道 」 和 「 503 服務無法使用 」 錯誤
疑難排解可以分成三種不同的工作，依序為：

1. [觀察和監視應用程式行為](#observe)
2. [收集資料](#collect)
3. [減少 hello 問題](#mitigate)

[App Service Web Apps](/services/app-service/web/) 在每個步驟均提供您各種選項。

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1.觀察和監視應用程式行為
#### <a name="track-service-health"></a>追蹤服務健全狀況
每次發生服務中斷或效能降低時，Microsoft Azure 就會發出公告。 您可以在 hello 追蹤 hello hello 服務健全狀況[Azure 入口網站](https://portal.azure.com/)。 如需詳細資訊，請參閱[追蹤服務健全狀況](../monitoring-and-diagnostics/insights-service-health.md)。

#### <a name="monitor-your-web-app"></a>監視 Web 應用程式
如果您的應用程式有任何問題，此選項可讓您 toofind 出。 在您的 web 應用程式] 刀鋒視窗中，按一下 [hello**要求與錯誤**磚。 hello**度量**刀鋒視窗會顯示您可以加入所有 hello 度量。

某些您可能希望您的 web 應用程式 toomonitor hello 度量

* 平均記憶體工作集
* 平均回應時間
* CPU 時間
* 記憶體工作集
* 要求

![監視 Web 應用程式，以解決 502 不正確的閘道和 503 服務無法使用的 HTTP 錯誤](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

如需詳細資訊，請參閱：

* [監視 Azure App Service 中的 Web Apps](web-sites-monitor.md)
* [接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a>2.收集資料
#### <a name="use-hello-azure-app-service-support-portal"></a>使用 hello Azure 應用程式服務支援入口網站
Web 應用程式為您提供 hello 能力 tootroubleshoot 問題相關的 tooyour web 應用程式藉由查看 HTTP 記錄檔、 事件記錄檔、 處理序傾印，等等。 您可以利用我們位於 **http://&lt;your app name>.scm.azurewebsites.net/Support** 的支援入口網站，存取所有這方面的資訊。

hello Azure 應用程式服務支援入口網站為您提供三個個別的索引標籤 toosupport hello 三個步驟的一般疑難排解的情況下：

1. 觀察目前的行為
2. 收集診斷資訊及執行 hello 內建的分析器來分析
3. 減輕問題

如果立即發生 hello 問題，請按一下**分析** > **診斷** > **現在診斷**toocreate 為您的診斷工作階段這將會收集 HTTP 記錄，事件檢視器記錄檔，記憶體傾印、 PHP 錯誤記錄檔和 PHP 處理報表。

一旦 hello 資料收集時，它也會在 hello 資料執行分析，並提供 HTML 報表。

如果您想 toodownload hello 資料，根據預設，它就會儲存在 hello D:\home\data\DaaS 資料夾中。

如需有關 hello Azure 應用程式服務支援入口網站的詳細資訊，請參閱[Azure 網站的網站擴充功能的新更新 tooSupport](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites)。

#### <a name="use-hello-kudu-debug-console"></a>使用 hello Kudu 偵錯主控台
Web Apps 隨附可用於偵錯、探索、上傳檔案的偵錯主控台，以及可以取得您環境相關資訊的 JSON 端點。 這稱為 hello *Kudu 主控台*或 hello *SCM 儀表板*web 應用程式。

您可以將 toohello 連結存取這個儀表板**https://&lt;應用程式名稱 >.scm.azurewebsites.net/**。

Kudu 提供的 hello 事項包括：

* 您的應用程式的環境設定
* 記錄檔串流
* 診斷傾印
* 您可以執行 Powershell Cmdlet 和基本 DOS 命令的偵錯主控台。

Kudu 另一個有用功能是，如果您的應用程式會擲回第一個出現的例外狀況，您可以使用 Kudu 與 hello SysInternals 工具 Procdump toocreate 記憶體傾印。 這些記憶體傾印是 hello 程序的快照集，並經常可協助您疑難排解您 web 應用程式更複雜的問題。

如需有關 Kudu 可用功能的詳細資訊，請參閱 [您應該知道的 Azure 網站線上工具](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/)。

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3.減少 hello 問題
#### <a name="scale-hello-web-app"></a>標尺 hello web 應用程式
在 Azure 應用程式服務，以增加的效能和輸送量，您可以調整 hello 小數位數，執行您的應用程式。 向上擴充 web 應用程式牽涉到兩個相關的動作： 變更您應用程式服務計劃 tooa 較高的定價層，以及設定某些設定之後您切換 toohello 更高的定價層。

如需有關調整的詳細資訊，請參閱 [在 Azure App Service 中調整 Web 應用程式規模](web-sites-scale.md)。

此外，您可以選擇 toorun 多個執行個體上的應用程式。 這不僅提供您更強大的處理能力，同時也提供您一定程度的容錯量。 如果 hello 程序關閉上一個執行個體，hello 其他執行個體將仍然繼續服務的要求。

您可以設定 hello toobe 手動或自動縮放比例。

#### <a name="use-autoheal"></a>使用 AutoHeal
AutoHeal 回收 hello 取決於您選擇 （例如組態變更、 要求、 記憶體為基礎的限制或 hello 時間需要 tooexecute 要求） 設定您的應用程式的背景工作處理序。 大部分的 hello 時間回收 hello 程序是 hello 最快方式 toorecover 問題。 您永遠可以重新啟動 hello web 應用程式從直接在 hello Azure 入口網站中的，雖然 AutoHeal 會自動替您完成。 您只需要 toodo 是 hello web 應用程式的根 web.config 中新增一些觸發程序。 請注意，這些設定會在 hello 相同方式即使您的應用程式並不是其中一個.Net。

如需詳細資訊，請參閱 [自動修復 Azure 網站](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/)。

#### <a name="restart-hello-web-app"></a>重新啟動 hello web 應用程式
這通常是 hello 最簡單方式 toorecover 從單次發生問題。 在 [hello [Azure 入口網站](https://portal.azure.com/)，在您的 web 應用程式] 刀鋒視窗中，您擁有 hello 選項 toostop 或重新啟動您的應用程式。

 ![重新啟動應用程式 toosolve HTTP 錯誤 502 不正確的閘道和 503 服務無法使用](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

您也可以使用 Azure Powershell 管理 Web 應用程式。 如需詳細資訊，請參閱 [將 Azure PowerShell 與 Azure 資源管理員搭配使用](../powershell-azure-resource-manager.md)。

