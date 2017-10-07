---
title: "Azure 記錄分析 Surface Hub aaaMonitor |Microsoft 文件"
description: "使用 hello Surface Hub 方案 tootrack hello 的健全狀況 Surface Hub 和了解它們的使用方式。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 623d30e749cafdd4a34ba0c5b3408164f1b4a95b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-tootrack-their-health"></a>記錄分析 tootrack 與它們的健全狀況監視 Surface Hub

![Surface Hub 符號](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

本文說明如何使用 hello Surface Hub 方案以 hello Microsoft Operations Management Suite (OMS) 的記錄分析 toomonitor Microsoft Surface Hub 裝置中。 記錄分析協助您，以及了解如何在使用追蹤 Surface Hub hello 健全狀況。

每個 Surface Hub 已安裝 Microsoft Monitoring Agent 的 hello。 它透過 hello 代理程式，您可以從 Surface Hub tooOMS 傳送資料。 記錄檔從您到 Surface Hub 和都是讀取，則會傳送 toohello OMS 服務。 問題 like 伺服器處於離線狀態，hello 行事曆不同步，或無法至 Skype toolog hello 裝置帳戶是否會顯示在 OMS 中 hello Surface Hub 儀表板中。 使用 hello 資料 hello 儀表板中，您可以識別未執行，或發生其他問題，並可能套用 hello 偵測到問題的修正程式的裝置。

## <a name="installing-and-configuring-hello-solution"></a>安裝和設定 hello 方案
使用下列資訊 tooinstall hello 並設定 hello 方案。 在順序 toomanage 您到 Surface Hub hello Microsoft Operations Management Suite (OMS)，從您將需要下列的 hello:

* 有效的訂用帳戶太[OMS](http://www.microsoft.com/oms)。
* [OMS 訂用帳戶](https://azure.microsoft.com/pricing/details/log-analytics/)層級將支援 hello 數目要 toomonitor 的裝置。 OMS 的價格取決於已註冊多少裝置裝置以及要處理多少資料。 您會想 tootake 這考量 Surface Hub 首度發行計劃時。

接下來，您會加入 OMS 訂用帳戶 tooyour 現有 Microsoft Azure 訂用帳戶，或建立新的工作區，以直接透過 hello OMS 入口網站。 使用哪一種方法的詳細指示請參閱[開始使用 Log Analytics](log-analytics-get-started.md)。 一旦設定 hello OMS 訂用帳戶之後，有兩種方式 tooenroll Surface Hub 裝置：

* 自動透過 Intune 註冊
* 在 Surface Hub 裝置上手動透過 [設定] 註冊

## <a name="set-up-monitoring"></a>設定監視
您可以監視 hello 健全狀況和您在 OMS 中使用記錄分析的 Surface Hub 的活動。 您可以註冊 hello Surface Hub 在 OMS 中，使用 Intune，或在本機使用**設定**上 hello Surface Hub。

## <a name="connect-surface-hubs-toooms-through-intune"></a>透過 Intune 連線到 Surface Hub tooOMS
您將需要 hello 工作區識別碼和管理 Surface Hub 的 hello OMS 工作區的工作區金鑰。 您可以取得 hello OMS 入口網站中。

Intune 是一項 Microsoft 產品，可讓您 toocentrally 管理 hello OMS 組態設定會套用的 tooone 或多個裝置。 請遵循這些步驟 tooconfigure 您透過 Intune 的裝置：

1. 登入 tooIntune。
2. 瀏覽過**設定** > **連線來源**。
3. 建立或編輯 hello Surface Hub 範本為基礎的原則。
4. 瀏覽 toohello OMS (Azure Operational Insights) 區段的 hello 原則，並新增 hello*工作區識別碼*和*工作區金鑰*toohello 原則。
5. 儲存 hello 原則。
6. Hello 原則關聯的裝置 hello 適當的群組。

   ![Intune 原則](./media/log-analytics-surface-hubs/intune.png)

然後，Intune 會同步 hello OMS 設定處理與 hello hello 目標群組中，您的 OMS 工作區中註冊的裝置。

## <a name="connect-surface-hubs-toooms-using-hello-settings-app"></a>連接到 Surface Hub tooOMS 使用 hello 設定應用程式
您將需要 hello 工作區識別碼和管理 Surface Hub 的 hello OMS 工作區的工作區金鑰。 您可以取得 hello OMS 入口網站中。

如果您不使用 Intune toomanage 您的環境，您可以註冊裝置以手動方式透過**設定**上每個 Surface Hub:

1. 從您的 Surface Hub 開啟 [設定]。
2. 輸入當系統提示您 hello 裝置系統管理員認證。
3. 按一下**此裝置**，和在 hello**監視**，按一下 **設定 OMS 設定**。
4. 選取 [啟用監視]。
5. 在 hello OMS 設定對話方塊中，輸入 hello**工作區識別碼**和型別 hello**工作區金鑰**。  
   ![設定](./media/log-analytics-surface-hubs/settings.png)
6. 按一下**確定**toocomplete hello 組態。

出現確認訊息會告訴您 hello OMS 組態已成功套用 toohello 裝置。 如果資料，會出現訊息，指出該 hello 代理程式已成功連接 toohello OMS 服務。 hello 裝置接著會開始傳送資料 tooOMS，您可以在其中檢視和處理它。

## <a name="monitor-surface-hubs"></a>監視 Surface Hub
使用 OMS 監視 Surface Hub 和監視任何已註冊的裝置極為類似。

1. 登入 toohello OMS 入口網站。
2. 瀏覽 toohello Surface Hub 方案套件儀表板。
3. 會顯示裝置的健康狀態。

   ![Surface Hub 的儀表板](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

您可以根據現有或自訂的記錄檔搜尋來建立[警示](log-analytics-alerts.md)。 使用 OMS 會收集從 Surface Hub hello 資料 hello，您可以搜尋問題和 hello 條件，您定義您的裝置上的警示。

## <a name="next-steps"></a>後續步驟
* 使用[記錄中記錄分析搜尋](log-analytics-log-searches.md)tooview 詳細 Surface Hub 資料。
* 建立[警示](log-analytics-alerts.md)toonotify 您 Surface Hub 發生問題時。
