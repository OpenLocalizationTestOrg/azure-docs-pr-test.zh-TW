---
title: "aaaTroubleshoot 雲端服務部署問題 |Microsoft 文件"
description: "沒有部署雲端服務 tooAzure 時可能遇到的一些常見的問題。 本文章提供解決方案 toosome 它們。"
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: a18ae415-0d1c-4bc4-ab6c-c1ddea02c870
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 15aea4f2b2913d95f3378b2e9762b232531f3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-deployment-problems"></a>對雲端服務部署問題進行疑難排解
當您部署雲端服務應用程式封裝 tooAzure 時，您可以從 hello 取得 hello 部署資訊**屬性**hello Azure 入口網站中的窗格。 您可以使用 hello 詳細資料中此窗格 toohelp 問題進行疑難排解 hello 雲端服務，並開啟新的支援要求時，您可以提供此資訊 tooAzure 支援。

您可以找到 hello**屬性**窗格中的，如下所示：

* 在 hello Azure 入口網站，按一下 hello 部署您的雲端服務中按一下**所有設定**，然後按一下**屬性**。
* 在 hello Azure 傳統入口網站，按一下您的雲端服務的 hello 部署，按一下**儀表板**、 hello 右下角的 hello 頁面 (在**快速概覽**)。 請注意，此窗格中並沒有「屬性」標籤。

> [!NOTE]
> 您可以複製 hello hello 內容**屬性**按一下 hello 圖示在 hello hello 窗格右上角的窗格 toohello 剪貼簿。
>
>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="problem-i-cannot-access-my-website-but-my-deployment-is-started-and-all-role-instances-are-ready"></a>問題：我無法存取我的網站，但是我已啟動部署且所有角色執行個體皆已就緒
hello hello 入口網站中顯示的網站 URL 連結不包含 hello 連接埠。 hello 網站的預設通訊埠為 80。 如果您的應用程式是在不同的通訊埠設定的 toorun，您必須新增 hello 正確的連接埠號碼 toohello URL 存取 hello 網站時。

1. 在 hello Azure 入口網站，按一下 hello 部署您的雲端服務。
2. 在 hello**屬性**窗格中的 hello Azure 入口網站，檢查 hello hello 角色執行個體的連接埠 (在**輸入端點**)。
3. 如果 hello 連接埠不是 80，新增 hello 正確的連接埠值 toohello URL，當您存取 hello 應用程式。 toospecify 非預設連接埠輸入 hello URL，後面接著冒號 （:），後面接著 hello 通訊埠編號，不含空格。

## <a name="problem-my-role-instances-recycled-without-me-doing-anything"></a>問題：我的角色執行個體無故自行回收
當 Azure 偵測到問題的節點，並因此移動角色執行個體 toonew 節點，會自動發生服務修復。 發生此情況時，您可能會看見角色執行個體自動回收。 如果 toofind 服務修復發生：

1. 在 hello Azure 入口網站，按一下 hello 部署您的雲端服務。
2. 在 hello**屬性**窗格中的 hello Azure 入口網站檢閱 hello 資訊並判斷發生服務修復期間 hello 觀察 hello 角色回收。

在主機 OS 和客體 OS 升級期間，角色大約每個月會回收一次。  
如需詳細資訊，請參閱 hello 部落格文章[角色執行個體因而重新啟動 tooOS 升級](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)

## <a name="problem-i-cannot-do-a-vip-swap-and-receive-an-error"></a>問題：我無法進行 VIP 交換並收到錯誤訊息
在部署更新進行期間不允許 VIP 交換。 部署更新可能在下列時間點自動執行：

* 新的客體作業系統可供使用時，和您設定要自動更新時。
* 服務修復執行時。

toofind out 如果自動更新，所以您無法進行 VIP 交換：

1. 在 hello Azure 入口網站，按一下 hello 部署您的雲端服務。
2. 在 hello**屬性**窗格中的 hello Azure 入口網站，看看 hello 值**狀態**。 如果是**準備**，然後檢查**上次作業**toosee 如果其中一個是最近發生的阻礙 hello VIP 交換。
3. 重複步驟 1 和 2 hello 生產環境部署。
4. 如果自動更新正在進行時，等候它 toofinish 之前嘗試 toodo hello VIP 交換。

## <a name="problem-a-role-instance-is-looping-between-started-initializing-busy-and-stopped"></a>問題：角色執行個體在 [已啟動]、[初始化中]、[忙碌] 和 [已停止] 之間循環
這種情況可能表示應用程式的程式碼、封裝或組態檔發生問題。 在此情況下，您應能 toosee hello 狀態變更每隔幾分鐘，而且 hello Azure 入口網站可能看起來像**回收**，**忙碌**，或**Initializing**。 這表示已發生某些錯誤會導致無法執行 hello 角色執行個體的 hello 應用程式。

如需有關如何 tootroubleshoot 這個問題，請參閱 hello 部落格文章[Azure PaaS 計算診斷資料](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)和[常見問題該原因角色 toorecycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md)。

## <a name="problem-my-application-stopped-working"></a>問題：我的應用程式停止運作
1. 在 hello Azure 入口網站，按一下 hello 角色執行個體。
2. 在 hello**屬性**窗格中的 hello Azure 入口網站，請考慮下列條件 tooresolve hello 您的問題：
   * 如果 hello 角色執行個體最近停止 (您可以檢查的 hello 值**中止計數**)，無法更新 hello 部署。 如果 hello 角色執行個體繼續其本身上運作，請等候 toosee。
   * 如果 hello 角色執行個體是**忙碌**，檢查您的應用程式程式碼 toosee hello [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck)處理事件。 您可能需要 tooadd 或修正某個處理此事件的程式碼。
   * 瀏覽 hello 診斷資料及疑難排解案例 hello 部落格文章[Azure PaaS 計算診斷資料](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)。

> [!WARNING]
> 如果回收您的雲端服務時，您重設 hello 部署的 hello 屬性有效地清除 hello hello 原始問題的資訊。
>
>

## <a name="next-steps"></a>後續步驟
檢視更多雲端服務的 [疑難排解文章](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) 。

toolearn tootroubleshoot 雲端服務角色如何發出使用 Azure PaaS 電腦診斷資料，請參閱[Kevin Williamson 部落格系列](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)。
