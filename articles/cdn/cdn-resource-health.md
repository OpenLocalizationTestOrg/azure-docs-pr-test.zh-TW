---
title: "aaaMonitor hello 健全狀況的 Azure CDN 資源 |Microsoft 文件"
description: "了解如何 toomonitor hello Azure CDN 資源使用 Azure 資源健全狀況的健全狀況。"
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a>監視 Azure CDN 資源 hello 健全狀況
  
Azure CDN 資源健康狀態是 [Azure 資源健康狀態](../resource-health/resource-health-overview.md)的子集。  您可以使用 Azure 資源健全狀況 toomonitor hello 健全狀況的 CDN 資源，並接收可採取動作的指導方針 tootroubleshoot 問題。

>[!IMPORTANT] 
>Azure CDN 資源健全狀況只有目前帳戶 hello 全域 CDN 傳遞和 API 功能的健全狀況。  Azure CDN 資源健康情況不會驗證個別的 CDN 端點。
>
>摘要 Azure CDN 資源健全狀況的 hello 訊號可能是 up too15 分鐘的延遲。

## <a name="how-toofind-azure-cdn-resource-health"></a>如何 toofind Azure CDN 資源健全狀況

1. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 tooyour 的 CDN 設定檔。

2. 按一下 hello**設定** 按鈕。

    ![設定按鈕](./media/cdn-resource-health/cdn-profile-settings.png)

3. 在 [支援與疑難排解] 下方，按一下 [資源健康狀態]。

    ![CDN 資源健康狀態](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
>您也可以尋找 hello 中列出的 CDN 資源*資源健全狀況*磚中 hello*說明 + 支援*刀鋒視窗。  您可以快速取得太*說明 + 支援*按一下 hello 圈選起來**嗎？** hello 右上角的 hello 入口網站。
>
> ![說明 + 支援](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a>Azure CDN 特定的訊息

下面，您可以找到相關的 tooAzure CDN 資源健全狀況狀態。

|訊息 | 建議的動作 |
|---|---|
|您可能已停止、移除或錯誤設定一或多個 CDN 端點 | 您可能已停止、移除或錯誤設定一或多個 CDN 端點。|
|很抱歉，目前無法使用 hello CDN 管理服務 | 回到這裡查看狀態更新。如果問題持續發生 hello 預期的解決時間之後，請連絡支援服務。|
|很抱歉，您的 CDN 端點可能受到我們的部分 CDN 提供者持續出現之問題所影響 | 回到這裡查看狀態更新。如何使用 hello 疑難排解工具 toolearn tootest 您的原點和 CDN 端點。如果問題持續發生 hello 預期的解決時間之後，請連絡支援服務。 |
|很抱歉，CDN 端點設定變更發生了傳播延遲 | 回到這裡查看狀態更新。如果您的組態變更不會完全傳播 hello 預期時間，請連絡支援。|
|很抱歉，我們遇到問題載入 hello 補充入口網站 | 回到這裡查看狀態更新。如果問題持續發生 hello 預期的解決時間之後，請連絡支援服務。|
很抱歉，我們的部分 CDN 提供者發生了問題 | 回到這裡查看狀態更新。如果問題持續發生 hello 預期的解決時間之後，請連絡支援服務。 |

## <a name="next-steps"></a>後續步驟

- [閱讀 Azure 資源健康狀態的概觀](../resource-health/resource-health-overview.md)
- [針對 CDN 壓縮的問題進行疑難排解](./cdn-troubleshoot-compression.md)
- [針對 404 錯誤的問題進行疑難排解](./cdn-troubleshoot-endpoint.md)