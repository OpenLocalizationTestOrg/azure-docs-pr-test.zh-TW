---
title: "Azure 自動化帳戶的記錄分析 aaaUnlink |Microsoft 文件"
description: "本文章提供如何 toounlink Azure 自動化帳戶從 OMS 工作區的概觀。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a>如何 toounlink 您的自動化帳戶從記錄分析工作區

Azure 自動化整合記錄分析 toonot 只支援主動式監視之 runbook 工作的所有的自動化帳戶，但也是必要時您匯入下列相依於記錄分析解決方案的 hello:

* [更新管理](../operations-management-suite/oms-solution-update-management.md)
* [變更追蹤](../log-analytics/log-analytics-change-tracking.md)
* [於下班時間啟動/停止 VM](automation-solution-vm-management.md)
 
如果您決定您不再想 toointegrate 記錄分析您的自動化帳戶，您可以取消連結您的帳戶，直接從 hello Azure 入口網站。  在繼續之前，您需要先 tooremove hello 解決方案稍早所提及，否則此程序將無法再繼續。  Hello 特定方案的檢閱 hello 主題您已匯入所需的 toounderstand hello 步驟 tooremove 它。  

移除這些方案之後可以執行下列步驟 toounlink hello 自動化帳戶。

## <a name="unlink-workspace"></a>取消連結工作區

1. 從 hello Azure 入口網站，開啟您的自動化帳戶，然後在 hello 自動化帳戶 刀鋒視窗，在 hello 帳戶 刀鋒視窗中，選取**取消連結工作區**。<br><br> ![取消連結工作區選項](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)<br><br>  
2. 在 hello 取消連結工作區刀鋒視窗中，按一下 **取消連結 worksapce**。<br><br> ![取消連結工作區刀鋒視窗](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png)。<br><br>  您會收到確認您想 tooproceed 提示。<br><br>
3. 但是 Azure 自動化會嘗試 toounlink hello 帳戶記錄分析工作區，您可以追蹤在 hello 進度**通知**hello 功能表。

如果您使用 hello 更新管理解決方案，或者您可能想 tooremove hello 下列 hello 方案中移除之後不再需要的項目。

* 更新排程。  每個都會有名稱符合您所建立的 hello 更新部署）

* 建立 hello 方案的混合式背景工作群組。  每個將命名為同樣的太 machine1.contoso.com_9ceb8108-26 c 9-4051-b6b3-227600d715c8)。

如果您在離峰時間方案時使用 hello 啟動/停止 Vm，或者您可能想 tooremove hello 下列 hello 方案中移除之後不再需要的項目。

* 啟動及停止 VM Runbook 排程 
* 啟動及停止 VM Runbook
* 變數   

## <a name="next-steps"></a>後續步驟

tooreconfigure 您自動化帳戶 toointegrate，OMS 記錄分析，請參閱[自動化 tooLog 分析 (OMS) 從轉寄工作狀態和作業資料流](automation-manage-send-joblogs-log-analytics.md)。 
