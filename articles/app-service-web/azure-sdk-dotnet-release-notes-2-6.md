---
title: "aaaAzure SDK for.NET 2.6 版本資訊"
description: "Azure SDK for .NET 2.6 版本資訊"
services: app-service/web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: b45853d5-a2b8-4962-a22d-579cb36ae14c
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: ac613cf20da4f731fab6f35ccbf6dbeaf18c0ec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-26-release-notes"></a>Azure SDK for .NET 2.6 版本資訊
本文件包含 hello hello Azure SDK for.NET 2.6 版的版本資訊。 

Azure SDK 2.6 中，您可以開發雲端服務 (PaaS) 為目標應用程式.NET 4.5.2 或.NET 4.6 前提是您手動安裝 hello 目標.NET Framework 上 hello 雲端服務角色。 請參閱 [在雲端服務角色上安裝 .NET](http://go.microsoft.com/fwlink/?LinkID=309796)。

## <a name="service-bus-updates"></a>服務匯流排更新
* 事件中心： 
  
  * 現在藉由公開事件中心的其他發行者端點，可在傳送事件時提供目標存取控制。
  * 其他的穩定性和改進加入 tooEvent 中心功能。
  * 在訊息和事件中心內，加入 WebSocket 上的 Amqp 通訊協定支援。

## <a name="hdinsight-tools-for-visual-studio-updates"></a>HDInsight Tools for Visual Studio 更新
* **IntelliSense 的增強功能**：遠端中繼資料建議
  
    HDInsight Tools for Visual Studio 現在支援在編輯 Hive 指令碼時取得遠端中繼資料。 例如，您可以輸入**選取 * FROM**且將顯示所有 hello 資料表名稱。 此外，指定資料表之後將會顯示 hello 資料行名稱。
* **HDInsight 模擬器支援**
  
    現在 HDInsight Tools for Visual Studio 支援連接 tooHDInsight 模擬器中，因此您無法在本機開發您的 Hive 指令碼，而不會引進任何費用，再執行這些指令碼，針對您的 HDInsight 叢集。 
  
    如需詳細資訊，請參閱太[此手冊](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409)。
* **HDInsight Tools for Visual Studio 支援一般的 Hadoop 叢集** (預覽)
  
    現在 HDInsight Tools for Visual Studio 支援一般的 Hadoop 叢集，因此您可以使用 HDInsight Tools for Visual Studio toodo hello 下列：
  
  * tooyour 叢集連線 
  * 使用增強式 IntelliSense/自動完成支援來撰寫 Hive 查詢、 
  * 檢視您的叢集與直覺的 UI 中所有的 hello 作業。 
    
    如需詳細資訊，請參閱太[此手冊](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409)。

## <a name="in-role-cache-updates"></a>角色中快取更新
* **角色中快取**已更新的 toouse **Microsoft Azure 儲存體 SDK** 4.3 版。 到目前為止，hello **In-role Cache**已使用 Azure 儲存體 SDK 1.7 版。
  
    客戶使用 Azure SDK 2.5 或以下應該更新 tooAzure SDK 2.6 和移動 toohello 新版的 Azure 儲存體 SDK。 
  
    在此時間的 Azure 儲存體版本 2011年-08-18 是排程的 toobe 移除 2016 年 8 月 1 日。 此時必須完成從 Azure SDK 2.5 或低於 too2.6 的角色中快取的任何移轉作業。 如需有關 Azure 儲存體 2011年-08-18 版的 hello 淘汰的詳細資訊，請參閱[Microsoft Azure 儲存體服務版本移除的更新： 副檔名 too2016](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx)。

> [!IMPORTANT]
> 我們將發表 hello 2016 年 11 月 30 日，停用 Azure 受管理快取服務與 Azure 角色中快取。 我們建議您移轉 tooAzure Redis 快取在此停用的準備。 如需日期和移轉指南的詳細資訊，請參閱 [我適合使用哪個 Azure 快取服務？](../redis-cache/cache-faq.md#which-azure-cache-offering-is-right-for-me)
> 
> 

## <a name="azure-app-service-tools"></a>Azure App Service 工具
hello 下列項目已更新在 hello Azure SDK 2.6 版本。

* Azure 發行增強 tooinclude Azure API 應用程式做為部署目標。
* API 的應用程式佈建功能 tooenable 使用者與應用程式開發介面應用程式建立佈建功能。
* 伺服器總管變更 tooreflect 新應用程式服務 節點，依資源群組分組的 Web、 行動裝置版和 API 應用程式。
* 加入 Azure API 應用程式用戶端軌跡加入 toomost C# 專案，將會啟用自動產生的 Swagger 啟用 API 應用程式在使用者的 Azure 訂用帳戶中執行。
* [伺服器總管] 中的 API Apps 工具和 App Service 節點僅可以在 Visual Studio 2013 中使用。 

## <a name="azure-resource-manager-tools-updates"></a>Azure 資源管理員工具更新
hello Azure 資源管理員工具已更新的 tooinclude 範本的虛擬機器、 網路和存放裝置。 hello JSON 的編輯體驗已經更新的 tooinclude 新大綱檢視的範本與 hello 能力 tooedit hello 範本使用 JSON 片段。 從 Visual Studio 部署的範本會使用與 hello 專案提供，因此 toohello 指令碼所做的變更將會使用由 Visual Studio 的 PowerShell 指令碼。

## <a name="diagnostics-improvements-for-cloud-services"></a>雲端服務的診斷改良功能
Azure SDK 2.6 再度支援收集 hello Azure 計算模擬器中的診斷記錄檔，並傳送 toodevelopment 儲存體。 任何診斷記錄 （包括應用程式追蹤記錄檔，追蹤 Windows (ETW) 記錄檔、 效能計數器、 基礎結構記錄檔和 windows 事件記錄檔的事件） 產生 hello 應用程式在 hello 模擬器中執行時可以是轉移的 toodevelopment診斷記錄正在本機電腦的儲存體 tooverify。 

現在可以讓您更輕鬆 toouse 不同診斷儲存體帳戶不同環境的 hello 服務組態 (.cscfg) 檔中指定 hello 診斷儲存體帳戶。 有一些值得注意的差異之間 hello 連接字串在 Azure SDK 2.4 和 Azure SDK 2.6 中的運作方式。 如需有關如何 toouse hello 診斷儲存體連接字串，以及它如何影響您的專案，請參閱[設定 Azure 雲端服務的診斷功能](http://go.microsoft.com/fwlink/?LinkID=532784)。

## <a name="breaking-changes"></a>重大變更
### <a name="azure-resource-manager-tools"></a>Azure 資源管理員工具
* hello**雲端部署專案**專案類型提供 hello Azure SDK 2.5 已重新命名過**Azure 資源群組**。
* **雲端部署專案**2.6 中可用的 hello Azure SDK 2.5 中建立的專案類型，但從 Visual Studio 部署的 hello 範本將會失敗。 不過，部署以 hello PowerShell 指令碼仍可正常之前一樣。  如需詳細資訊 toouse**雲端部署專案**在閱讀本 2.6[張貼](http://go.microsoft.com/fwlink/?LinkID=534086)。

## <a name="known-issues"></a>已知問題
* 收集診斷記錄檔中 hello 模擬器需要 64 位元作業系統。 在 32 位元的作業系統上執行時，將無法收集診斷記錄檔。 這並不會影響任何其他模擬器功能。 
* 2015 年 4 月 29 日發行的 Azure SDK 2.6 有兩個問題： 
  
  * 通用應用程式無法載入 Visual Studio 2015 中，hello 機器上安裝 Azure SDK 2.6 時。
  * 在 Visual Studio 2013 和 Visual Studio 2015 的 Visual Studio 變得沒有回應，並損毀時顯示以 hello 訊息 「 模擬器設定診斷 」 對話方塊，偵錯雲端服務專案會失敗。
    
    更新 tooAzure SDK 2.6 已於 2015 年 5 月 18 日發行。 hello 更新的版本是 2.6.30508.1601;它包含如上面所述的兩個問題的修正程式。 您可以識別 hello hello 組建 SDK，從 控制台-> 程式和功能-> Microsoft Azure Tools for Microsoft 的 Visual Studio 2013 – 而 v 2.6。 hello 版本 欄會顯示 hello 組建編號。
    
    如果您仍然遇到 hello 上述問題，安裝 hello 最新版本的 hello Azure SDK 2.6 [VS 2012](http://go.microsoft.com/fwlink/p/?linkid=323511&clcid=0x409)， [VS 2013](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)或[VS 2015](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)。

## <a name="see-also"></a>另請參閱
[支援和 hello Azure SDK for.NET 和 Api 的停用資訊](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

