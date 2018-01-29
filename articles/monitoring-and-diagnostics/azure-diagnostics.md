---
title: "Azure 診斷概觀 | Microsoft Docs"
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
ms.openlocfilehash: 0c6e4d9d2a3744f607b72364f3944c700acd070c
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="what-is-azure-diagnostics"></a>什麼是 Azure 診斷
Azure 診斷是 Azure 中可對部署的應用程式啟用診斷資料收集的功能。 您可以使用來自許多不同來源的診斷延伸模組。 目前支援的有 Azure 雲端服務 Web 和背景工作角色、執行 Microsoft Windows 的 Azure 虛擬機器，以及 Service Fabric。 其他 Azure 服務都有自己個別的診斷。

## <a name="data-you-can-collect"></a>您可以收集的資料
Azure 診斷可收集下列資料類型：

| 資料來源 | 說明 |
| --- | --- |
| 效能計數器 |作業系統和自訂效能計數器 |
| 應用程式記錄檔 |追蹤您應用程式寫入的訊息 |
| Windows 事件記錄檔 |傳送至 Windows 事件記錄系統的資訊 |
| .NET 事件來源 |使用 .NET [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) 類別的程式碼編寫事件 |
| IIS 記錄檔 |IIS 網站的相關資訊 |
| 以資訊清單為基礎的 ETW |針對任何程序所產生之 Windows 事件所進行的事件追蹤 |
| 損毀傾印 |應用程式損毀時之程序狀態的相關資訊 |
| 自訂錯誤記錄檔 |您的應用程式或服務所建立的記錄檔 |
| Azure 診斷基礎結構記錄檔 |診斷本身的相關資訊 |

Azure 診斷擴充可以將這項資料傳送到 Azure 儲存體帳戶，或傳送到 [Application Insights](../application-insights/app-insights-cloudservices.md) 之類的服務。 資料可用來進行偵錯和疑難排解、測量效能、監視資源使用量、流量分析和容量規劃，以及稽核。

## <a name="versioning"></a>版本控制
請參閱 [Azure 診斷版本歷程記錄](azure-diagnostics-versioning-history.md)。

## <a name="next-steps"></a>後續步驟
請選擇您嘗試要在哪個服務上收集診斷資料，並使用下列文件來開始。 如需特定工作的參考，請使用一般的 Azure 診斷連結。

## <a name="web-apps"></a>Web 應用程式
請注意，Web Apps 不會使用 Azure 診斷。 在 [Web Apps](../app-service/web-sites-enable-diagnostic-log.md) 上尋找同等的資訊

## <a name="cloud-services-using-azure-diagnostics"></a>使用 Azure 診斷的雲端服務
* 如果您使用 Visual Studio，請參閱[使用 Visual Studio 來追蹤雲端服務應用程式](../vs-azure-tools-debug-cloud-services-virtual-machines.md)來開始。 否則，請參閱
* [如何使用 Azure 診斷來監視雲端服務](../cloud-services/cloud-services-how-to-monitor.md)
* [在雲端服務應用程式中設定 Azure 診斷](../cloud-services/cloud-services-dotnet-diagnostics.md)

如需更進階的主題，請參閱

* [搭配適用於雲端服務的 Application Insights 來使用 Azure 診斷](../application-insights/app-insights-cloudservices.md)
* [使用 Azure 診斷追蹤雲端服務應用程式的流程](../cloud-services/cloud-services-dotnet-diagnostics-trace-flow.md)
* [使用 PowerShell 在雲端服務上設定診斷](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="virtual-machines-using-azure-diagnostics"></a>使用 Azure 診斷的虛擬機器
* 如果您使用 Visual Studio，請參閱[使用 Visual Studio 來追蹤 Microsoft Azure 虛擬機器](../vs-azure-tools-debug-cloud-services-virtual-machines.md)來開始。 否則，請參閱
* [在 Azure 虛擬機器上設定 Azure 診斷](../virtual-machines-dotnet-diagnostics.md)

如需更進階的主題，請參閱

* [使用 PowerShell 在 Azure 虛擬機器上設定診斷](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [使用 Azure Resource Manager 範本建立具有監視和診斷的 Windows 虛擬機器](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="service-fabric-using-azure-diagnostics"></a>使用 Azure 診斷的 Service Fabric
請參閱[監視 Service Fabric 應用程式](../service-fabric/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)來開始。 當您抵達這篇文章所在網頁時，可以利用左側的導覽樹狀目錄前往許多其他的 Service Fabric 診斷文章。

## <a name="general-azure-diagnostics-articles"></a>一般的 Azure 診斷文章
* [Azure 診斷結構描述組態](https://msdn.microsoft.com/library/azure/mt634524.aspx) ：了解如何變更結構描述檔來收集和路由診斷資料。 請注意，您也可以使用 Visual Studio 來變更結構描述檔。
* [Azure 診斷資料在 Azure 儲存體中的儲存方式](../cloud-services/cloud-services-dotnet-diagnostics-storage.md)：知道寫入診斷資料的資料表及 Blob 名稱。
* 了解如何[在 Azure 診斷中使用效能計數器](../cloud-services/cloud-services-dotnet-diagnostics-performance-counters.md)。
* 了解如何[將 Azure 診斷資訊路由到 Application Insights](azure-diagnostics-configure-application-insights.md)
* 如果您在開始診斷，或是在 Azure 儲存體資料表中尋找資料時遇到問題，請參閱[針對 Azure 診斷進行疑難排解](azure-diagnostics-troubleshooting.md)
