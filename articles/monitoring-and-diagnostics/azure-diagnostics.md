---
title: "Azure 診斷的 aaaOverview |Microsoft 文件"
description: "使用 Azure 診斷來在雲端服務、虛擬機器及 Service Fabric 中進行偵錯、測量效能、監視、流量分析等。"
services: multiple
documentationcenter: .net
author: rboucher
manager: 
editor: 
ms.assetid: baad40d8-c915-4f93-b486-8b160bf33463
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/18/2017
ms.author: robb
ms.openlocfilehash: 2a03a96a37091894d7ab16120c125116e4bf462a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-diagnostics"></a>什麼是 Azure 診斷
Azure 診斷是在啟用 hello 集合上部署的應用程式的診斷資料的 Azure 中的 hello 功能。 您可以從不同來源的大量使用 hello 診斷延伸模組。 目前支援的有 Azure 雲端服務 Web 和背景工作角色、執行 Microsoft Windows 的 Azure 虛擬機器，以及 Service Fabric。 其他 Azure 服務都有自己個別的診斷。

## <a name="data-you-can-collect"></a>您可以收集的資料
Azure 診斷可收集下列類型的資料的 hello:

| 資料來源 | 說明 |
| --- | --- |
| 效能計數器 |作業系統和自訂效能計數器 |
| 應用程式記錄檔 |追蹤您應用程式寫入的訊息 |
| Windows 事件記錄檔 |傳送 toohello Windows 事件記錄系統資訊 |
| .NET 事件來源 |撰寫使用 hello.NET 事件的程式碼[EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx)類別 |
| IIS 記錄檔 |IIS 網站的相關資訊 |
| 以資訊清單為基礎的 ETW |針對任何程序所產生之 Windows 事件所進行的事件追蹤 |
| 損毀傾印 |應用程式當機 hello hello 事件中的 hello 程序狀態資訊 |
| 自訂錯誤記錄檔 |您的應用程式或服務所建立的記錄檔 |
| Azure 診斷基礎結構記錄檔 |診斷本身的相關資訊 |

hello Azure 診斷擴充功能可以傳送這個資料 tooan Azure 儲存體帳戶，或傳送像 tooservices [Application Insights](../application-insights/app-insights-cloudservices.md)。 您可以使用 hello 資料的偵錯和疑難排解、 測量效能、 監視資源使用狀況、 流量分析和容量規劃，以及稽核。

## <a name="versioning"></a>版本控制
請參閱 [Azure 診斷版本歷程記錄](azure-diagnostics-versioning-history.md)。

## <a name="next-steps"></a>後續步驟
選擇哪一個服務想 toocollect 診斷，並使用下列文章 tooget 啟動 hello。 用於特定工作的參考 hello 一般的 Azure 診斷的連結。

## <a name="web-apps"></a>Web Apps
請注意，Web Apps 不會使用 Azure 診斷。 尋找在 hello 相等資訊[Web 應用程式](../app-service-web/web-sites-enable-diagnostic-log.md)

## <a name="cloud-services-using-azure-diagnostics"></a>使用 Azure 診斷的雲端服務
* 如果使用 Visual Studio，請參閱[使用 Visual Studio tootrace 雲端服務應用程式](../vs-azure-tools-debug-cloud-services-virtual-machines.md)tooget 啟動。 否則，請參閱
* [Toomonitor 雲端服務使用 Azure 診斷](../cloud-services/cloud-services-how-to-monitor.md)
* [在雲端服務應用程式中設定 Azure 診斷](../cloud-services/cloud-services-dotnet-diagnostics.md)

如需更進階的主題，請參閱

* [搭配適用於雲端服務的 Application Insights 來使用 Azure 診斷](../application-insights/app-insights-cloudservices.md)
* [追蹤雲端服務應用程式使用 Azure 診斷的 hello 流程](../cloud-services/cloud-services-dotnet-diagnostics-trace-flow.md)
* [雲端服務上使用 PowerShell tooset 診斷](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="virtual-machines-using-azure-diagnostics"></a>使用 Azure 診斷的虛擬機器
* 如果使用 Visual Studio，請參閱[使用 Visual Studio tootrace Azure 虛擬機器](../vs-azure-tools-debug-cloud-services-virtual-machines.md)tooget 啟動。 否則，請參閱
* [在 Azure 虛擬機器上設定 Azure 診斷](../virtual-machines-dotnet-diagnostics.md)

如需更進階的主題，請參閱

* [Azure 虛擬機器上使用 PowerShell tooset 診斷](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [使用 Azure Resource Manager 範本建立具有監視和診斷的 Windows 虛擬機器](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="service-fabric-using-azure-diagnostics"></a>使用 Azure 診斷的 Service Fabric
請參閱[監視 Service Fabric 應用程式](../service-fabric/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)來開始。 使用左後您 toothis 發行項的 hello hello 瀏覽樹狀目錄中許多其他的 Service Fabric 診斷文章。

## <a name="general-azure-diagnostics-articles"></a>一般的 Azure 診斷文章
* [Azure 診斷的結構描述組態](https://msdn.microsoft.com/library/azure/mt634524.aspx)-了解如何 toochange hello 結構描述檔案 toocollect 和路由傳送診斷資料。 請注意，您也可以使用 Visual Studio toochange hello 結構描述檔案。
* [Azure 診斷資料如何儲存在 Azure 儲存體](../cloud-services/cloud-services-dotnet-diagnostics-storage.md)-知道 hello hello 資料表和 blob hello 診斷資料所寫入之名稱。
* 了解太[Azure 診斷中使用效能計數器](../cloud-services/cloud-services-dotnet-diagnostics-performance-counters.md)。
* 了解太[路由 Azure 診斷資訊 tooApplication Insights](azure-diagnostics-configure-application-insights.md)
* 如果您在開始診斷，或是在 Azure 儲存體資料表中尋找資料時遇到問題，請參閱[針對 Azure 診斷進行疑難排解](azure-diagnostics-troubleshooting.md)
