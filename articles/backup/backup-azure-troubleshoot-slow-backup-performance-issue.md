---
title: "aaaTroubleshoot 緩慢的備份檔案和資料夾在 Azure 備份 |Microsoft 文件"
description: "提供疑難排解指引 toohelp 診斷 hello 的 Azure 備份的效能問題的原因"
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.assetid: e379180a-db13-4e0c-90e4-28e5dd6f5b14
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 21d79bbd03c2706bc43fcc7c14020cffd6b919c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-backup-of-files-and-folders-in-azure-backup"></a>疑難排解 Azure 備份的檔案和資料夾備份速度緩慢問題
本文章提供疑難排解指引 toohelp 您 hello 的檔案和資料夾備份的效能變慢的原因時診斷您使用 Azure Backup。 當您使用 Azure Backup agent tooback hello 檔案時，hello 備份程序可能要花超過預期。 此延遲時間可能被因為一或多個 hello 下列：

* [正在備份的 hello 電腦上沒有效能瓶頸。](#cause1)
* [另一個處理程序或防毒軟體會干擾 hello Azure 備份程序。](#cause2)
* [hello 備份代理程式在 Azure 虛擬機器 (VM) 上執行。](#cause3)  
* [您正在備份大量 (數百萬計) 的檔案。](#cause4)

在開始進行疑難排解的問題之前，我們建議您下載並安裝 hello[最新的 Azure 備份代理程式](http://aka.ms/azurebackup_agent)。 我們請經常更新 toohello 備份代理程式 toofix 各種問題，新增的功能，並改善效能。

我們也強烈建議您檢閱 hello [Azure 備份服務常見問題集](backup-azure-backup-faq.md)toomake 確定未發生任何 hello 常見的組態問題。

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

<a id="cause1"></a>

## <a name="cause-performance-bottlenecks-on-hello-computer"></a>原因： Hello 電腦上的效能瓶頸
正在備份的 hello 電腦上的瓶頸，可能會造成延遲。 例如，hello 電腦的能力 tooread 或寫入 toodisk，或透過 hello 網路可用頻寬 toosend 資料可能會造成瓶頸。

Windows 提供的內建的工具，稱為[效能監視器](https://technet.microsoft.com/magazine/2008.08.pulse.aspx)(Perfmon) toodetect 這些瓶頸。

以下是能幫助您診斷最佳化備份瓶頸的一些效能計數器和範圍。

| 計數器 | 狀態 |
| --- | --- |
| 邏輯磁碟 (實體磁碟)--% 閒置 |• 100%閒置 too50%閒置 = 狀況良好</br>• 49%閒置 too20%閒置 = 警告或監視</br>• 19%閒置 too0%閒置 = 重大或超出規格 |
| 邏輯磁碟 (實體磁碟)--% 平均磁碟的讀取或寫入秒數 |• 0.001 ms too0.015 ms = 狀況良好</br>• 0.015 ms too0.025 ms = 警告或監視</br>• 0.026 毫秒或更長 = 嚴重或超出規範 |
| 邏輯磁碟 (實體磁碟)--(所有執行個體) 目前的磁碟佇列長度 |80 個要求超過 6 分鐘 |
| 記憶體--集區未分頁位元組 |• 耗用不到 60% 集區 = 狀況良好<br>• 61%too80%的集區取用 = 警告或監視</br>• 耗用超過 80% 集區 = 重大或超出規範 |
| 記憶體--集區分頁位元組 |• 耗用不到 60% 集區 = 狀況良好</br>• 61%too80%的集區取用 = 警告或監視</br>• 耗用超過 80% 集區 = 重大或超出規範 |
| 記憶體--可用 MB 數 |• 50% 以上的可用記憶體可供使用 = 狀況良好</br>• 25% 的可用記憶體可供使用 = 監視</br>• 10% 的可用記憶體可供使用 = 警告</br>• 不到 100 MB 或 5% 的可用記憶體可供使用 = 重大或超出規範 |
| 處理器--\% 處理器時間 (所有執行個體) |• 已消耗低於 60% = 狀況良好</br>• 61%too90%耗用 = 監視器或警告</br>• 91%too100%耗用 = 重大 |

> [!NOTE]
> 如果您判斷 hello 基礎結構的 hello 問題，我們建議您重組 hello 磁碟定期以提升效能。
>
>

<a id="cause2"></a>

## <a name="cause-another-process-or-antivirus-software-interfering-with-azure-backup"></a>原因：有其他處理程序或防毒軟體在干擾 Azure 備份
我們已看到幾個執行個體，其中 hello Windows 系統中的其他處理序已產生負面影響 hello Azure 備份代理程式處理序的效能。 例如，如果您使用 hello Azure Backup agent 和其他程式 tooback 資料，或如果防毒軟體正在執行且已鎖定檔案 toobe 備份，hello 檔案上的多個鎖定可能會造成競爭的情況。 在此情況下，hello 備份可能會失敗，或 hello 工作花費時間超出預期。

hello 最佳建議，在此案例中是關閉 hello tooturn 其他備份程式 toosee 是否 hello hello Azure 備份代理程式的備份時間變更。 通常，確定未執行多個備份作業在 hello 同時是足夠 tooprevent 其會影響彼此。

防毒程式，我們建議您排除 hello 下列檔案和位置：

* 將 C:\Program Files\Microsoft Azure Recovery Services Agent\bin\cbengine.exe 做為處理程序
* C:\Program Files\Microsoft Azure Recovery Services Agent\ 資料夾
* 可用的位置 （如果您不使用 hello 標準位置）

<a id="cause3"></a>

## <a name="cause-backup-agent-running-on-an-azure-virtual-machine"></a>原因：Azure 虛擬機器上執行的備份代理程式
如果您在 VM 上執行 hello 備份代理程式，效能會低於當您執行它在實體電腦上。 這是預期行為，因為 tooIOPS 限制。  不過，您可以藉由切換 hello 資料磁碟機正在備份 tooAzure 高階儲存體最佳化 hello 效能。 我們正努力修正這個問題，並 hello 修正將可在未來的版本。

<a id="cause4"></a>

## <a name="cause-backing-up-a-large-number-millions-of-files"></a>原因：備份大量的 (數百萬計) 檔案
移動大量資料所花費的時間會比移動較少量資料更久。 在某些情況下，相關的備份時間 toonot 只 hello hello 資料，但是也 hello 數目的檔案或資料夾的大小。 特別是當包含數百萬個小型檔案 (幾個位元組 tooa 幾 kb) 正在備份。

在您正在備份 hello 資料，並將它移 tooAzure，Azure 會同時分類您的檔案，就會發生這種行為。 在某些罕見的情況下，hello 目錄作業可能花費時間超出預期。

下列標記的 hello 可協助您了解 hello 瓶頸，並據以處理 hello 接下來的步驟：

* **UI 會顯示 hello 資料傳輸進度**。 仍要傳輸 hello 資料。 hello 網路頻寬或 hello 資料大小可能會造成延遲。
* **UI 未顯示 hello 資料傳輸進度**。 開啟 hello 記錄檔位於 C:\Microsoft Azure 復原服務 Agent\Temp，然後檢查 hello FileProvider::EndData hello 記錄檔中的項目。 此項目表示 hello 資料傳送完成，並發生 hello 目錄作業。 不要取消 hello 備份工作。 相反地，等候一段時間 hello 目錄作業 toofinish。 如果 hello 問題持續發生，請連絡[Azure 支援](https://portal.azure.com/#create/Microsoft.Support)。
