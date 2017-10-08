---
title: "Azure 自動化資料 aaaManaging |Microsoft 文件"
description: "本文章包含用於管理 Azure 自動化環境的多個主題。  目前將資料保留和備份 Azure 自動化災害復原併入 Azure 自動化中。"
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 2896f129-82e3-43ce-b9ee-a3860be0423a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/201
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 46a164d864c4956c90ab689ca159fff6f6c08028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-automation-data"></a>管理 Azure 自動化資料
本文章包含用於管理 Azure 自動化環境的多個主題。

## <a name="data-retention"></a>資料保留
當您刪除 Azure 自動化中的資源時，會將它保留 90 天作為稽核用途，之後才永久移除。  您無法看到，或使用在這段期間的 hello 資源。  此原則也適用於 tooresources 屬於 tooan 自動化帳戶刪除。

Azure 自動化會自動刪除並永久移除超過 90 天的工作。

hello 下表摘要說明不同資源的 hello 保留原則。

| 資料 | 原則 |
|:--- |:--- |
| 帳戶 |Hello 帳戶被刪除的使用者後的 90 天永久移除。 |
| Assets |Hello 資產被使用者刪除，或 hello 之後的 90 天的使用者刪除保存 hello 資產帳戶之後的 90 天永久移除。 |
| 模組 |Hello 模組已被使用者刪除，或 hello 之後的 90 天的使用者刪除保存 hello 模組帳戶之後的 90 天永久移除。 |
| Runbook |Hello 資源已被使用者刪除，或在 hello 後的 90 天保存 hello 資源帳戶刪除使用者之後的 90 天永久移除。 |
| 工作 |在上次修改日期的 90 天後刪除並永久移除。 這可能是 hello 作業完成、 已停止或暫停之後。 |
| 節點組態/MOF 檔案 |舊的節點組態會在新的節點組態產生之後的 90 天永久移除。 |
| DSC 節點 |使用 Azure 入口網站或 hello 的自動化帳戶從取消註冊 hello 節點之後的 90 天永久移除[取消註冊 AzureRMAutomationDscNode](https://msdn.microsoft.com/library/mt603500.aspx)中 Windows PowerShell cmdlet。 移除的節點也會永久保存在使用者刪除 hello 節點的 hello 帳戶之後的 90 天。 |
| 節點報告 |該節點產生新的報告之後的 90 天永久移除 |

hello 保留原則適用於 tooall 使用者，而且目前無法進行自訂。

不過，如果您需要 tooretain 資料的時間更長的時間，您可以轉送 runbook 作業記錄檔 tooLog 分析。  如需詳細資訊，請檢閱[轉寄 Azure 自動化工作資料 tooOMS 記錄分析](automation-manage-send-joblogs-log-analytics.md)。   

## <a name="backing-up-azure-automation"></a>備份 Azure 自動化
當您刪除 Microsoft Azure 中的自動化帳戶時，會刪除 hello 帳戶中的所有物件，包括 runbook、 模組、 組態、 設定、 工作和資產。 hello 帳戶被刪除後，就無法復原 hello 物件。  您可以使用下列的自動化帳戶的資訊 toobackup hello 內容，然後再刪除 hello。 

### <a name="runbooks"></a>Runbook
您可以匯出 runbook tooscript 檔案使用 hello Azure 管理入口網站或 hello [Get-azureautomationrunbookdefinition](https://msdn.microsoft.com/library/dn690269.aspx)中 Windows PowerShell cmdlet。  可以將這些指令碼檔案匯入到另一個自動化帳戶，如 [建立或匯入 Runbook](https://msdn.microsoft.com/library/dn643637.aspx)中所述。

### <a name="integration-modules"></a>整合模組
您無法從 Azure 自動化匯出整合模組。  您必須確定它們的外部 hello 自動化帳戶。

### <a name="assets"></a>Assets
您無法從 Azure 自動化匯出 [資產](https://msdn.microsoft.com/library/dn939988.aspx) 。  使用 hello Azure 管理入口網站，您必須注意 hello 的變數、 認證、 憑證、 連接和排程的詳細資料。  然後必須手動建立您匯入到另一個自動化的 Runbook 所使用的任何資產。

您可以使用[Azure cmdlet](https://msdn.microsoft.com/library/dn690262.aspx) tooretrieve 詳細資料的未加密的資產，然後將它們儲存供日後參考，或在另一個自動化帳戶中建立對等的資產。

您無法擷取加密的變數或 hello 密碼欄位的認證使用 cmdlet 的 hello 值。  如果您不知道這些值，則您可以擷取 runbook 使用 hello [Get-automationvariable](https://msdn.microsoft.com/library/dn940012.aspx)和[Get-automationpscredential](https://msdn.microsoft.com/library/dn940015.aspx)活動。

您無法從 Azure 自動化匯出憑證。  您必須確定 Azure 外部有任何憑證可供使用。

### <a name="dsc-configurations"></a>DSC 組態
您可以匯出組態 tooscript 檔案使用 hello Azure 管理入口網站或 hello[匯出 AzureRmAutomationDscConfiguration](https://msdn.microsoft.com/library/mt603485.aspx)中 Windows PowerShell cmdlet。 這些組態可以匯入並用於另一個自動化帳戶中。

## <a name="geo-replication-in-azure-automation"></a>Azure 自動化中的異地複寫
帳戶資料 tooa 不同的地理區域備援地理複寫，在 Azure 自動化帳戶中的標準備份。 設定您的帳戶時，您可以選擇主要區域，然後次要區域 tooit 自動指派。 hello 次要資料，從 hello 主要區域中，複製會持續更新以防資料遺失。  

下表中的 hello 顯示 hello 可用的主要和次要區域配對。

| 主要 | 次要 |
| --- | --- |
| 美國中南部 |美國中北部 |
| 美國東部 2 |美國中部 |
| 西歐 |北歐 |
| 東南亞 |東亞 |
| 日本東部 |日本西部 |

在主要區域資料會遺失 hello 的罕見事件，Microsoft 會嘗試 toorecover 它。 如果無法復原 hello 主要資料，然後執行地理容錯移轉且 hello 受影響的客戶將會通知關於此透過其訂用帳戶。

