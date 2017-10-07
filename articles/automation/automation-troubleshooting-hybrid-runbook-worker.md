---
title: "Azure 自動化 Hybrid Runbook Worker aaaTroubleshoot |Microsoft 文件"
description: "描述 hello 徵狀、 原因和解決最常見的 Hybrid Runbook Worker 在 Azure 自動化中所發出的 hello。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 02c6606e-8924-4328-a196-45630c2255e9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: magoedte
ms.openlocfilehash: 292af517c88d1ffd21262a286ccc079e7270bfad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-tips-for-hybrid-runbook-worker"></a>混合式 Runbook 背景工作角色的疑難排解提示

本文章提供疑難排解的錯誤，您可能會遇到與自動化 Hybrid Runbook Worker，並建議可能的解決方案 tooresolve 說明它們。

## <a name="a-runbook-job-terminates-with-a-status-of-suspended"></a>Runbook 作業在暫止狀態下終止

您的 runbook 會暫停嘗試 tooexecute 後，馬上它三次。 可能會干擾 hello runbook 無法順利完成的情況，而且 hello 相關的錯誤訊息不包含任何表示原因的詳細資訊。 本文章提供問題相關的 toohello Hybrid Runbook Worker runbook 執行失敗的疑難排解步驟。

如果這份文件中並未提及您的 Azure 問題，請瀏覽 hello Azure 論壇上[MSDN 和 hello 堆疊溢位](https://azure.microsoft.com/support/forums/)。 您可以在這些論壇張貼您的問題或太[@AzureSupport Twitter 上](https://twitter.com/AzureSupport)。 此外，您可以藉由選取檔案 Azure 支援人員要求**取得支援**上 hello [Azure 支援](https://azure.microsoft.com/support/options/)站台。

### <a name="symptom"></a>徵狀
Runbook 執行會失敗並會傳回錯誤的 hello，"hello 作業動作 'Activate' 無法執行，因為 hello 處理序意外停止。 hello 工作動作嘗試 3 次。 」

有幾個 hello 錯誤可能原因： 

1. hello 混合式背景工作會在 proxy 或防火牆後面
2. hello 電腦 hello 混合式背景工作上執行小於最小的 hello 比[硬體需求](automation-offering-get-started.md#hybrid-runbook-worker)  
3. hello runbook 無法向本機資源

#### <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a>原因 1︰Hybrid Runbook Worker 位在 Proxy 或防火牆後方
混合式 Runbook 背景工作執行的 hello 電腦 hello 位於防火牆或 proxy 伺服器並不能允許或正確設定傳出的網路存取。

#### <a name="solution"></a>方案
確認 hello 電腦具有對外存取 too*.azure automation.net 連接埠 443。 

#### <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a>原因 2︰電腦未滿足最低硬體需求
執行的 hello 應該符合 Hybrid Runbook Worker 的電腦 hello 最低硬體需求，再指定它 toohost 這項功能。 否則，根據 hello 資源使用的其他背景處理序和執行期間，runbook 所造成的競爭情形，hello 電腦會變得過度使用，並會造成 runbook 作業延遲或逾時。 

#### <a name="solution"></a>方案
先確認 hello 電腦指定 toorun hello Hybrid Runbook Worker 的功能符合 hello 最低硬體需求。  若是如此，監視 CPU 和記憶體使用率 toodetermine Windows hello 的混合式 Runbook 背景工作處理序的效能之間的任何相互關聯。  如果沒有記憶體或 CPU 不足的壓力，這可能表示 hello 需要 tooupgrade 或加入額外的處理器或增加記憶體 tooaddress hello 資源瓶頸並解決 hello 錯誤。 或者，選取不同的計算資源可支援 hello 最小需求並縮放工作負載需求指出是必要的增加時。         

#### <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a>原因 3：Runbook 無法使用本機資源驗證

#### <a name="solution"></a>方案
檢查 hello **Microsoft SMA**事件記錄檔中描述的對應事件*Win32 處理序已結束，代碼 [4294967295]*。  hello 這個錯誤的原因是您未在 runbook 中設定驗證或未指定 hello 執行身分認證的 hello Hybrid worker 群組。  請檢閱[Runbook 權限](automation-hrw-run-runbooks.md#runbook-permissions)tooconfirm 您已正確設定驗證您的 runbook。  

## <a name="next-steps"></a>後續步驟

如需針對自動化中的其他問題進行疑難排解的協助，請參閱[針對 Azure 自動化進行疑難排解](automation-troubleshooting-automation-errors.md) 