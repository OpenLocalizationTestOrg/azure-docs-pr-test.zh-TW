---
title: "aaaAzure 安全性中心疑難排解指南 |Microsoft 文件"
description: "這份文件可協助 tootroubleshoot Azure 資訊安全中心中的問題。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 44462de6-2cc5-4672-b1d3-dbb4749a28cd
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 78b3c49eb66fe3a4f80efbba3a47a87b039c07ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-troubleshooting-guide"></a>Azure 資訊安全中心疑難排解指南
本指南適用於資訊技術 (IT) 專業人員、 資訊安全性分析師和雲端系統管理員的組織使用 Azure 資訊安全中心，而且必須 tootroubleshoot 資訊安全中心相關的問題。

>[!NOTE] 
>從開始早期年 6 月 2017年，資訊安全中心會使用 hello Microsoft Monitoring Agent toocollect 和存放區資料。 請參閱[Azure 安全性 Center 平台移轉](security-center-platform-migration.md)toolearn 更多。 本文章中的 hello 資訊表示資訊安全中心功能之後轉換 toohello Microsoft Monitoring Agent。
>

## <a name="troubleshooting-guide"></a>疑難排解指南
本指南說明如何 tootroubleshoot 資訊安全中心相關的問題。 大部分的 hello 疑難排解完成資訊安全中心會進行第一次查看 hello[稽核記錄檔](https://azure.microsoft.com/updates/audit-logs-in-azure-preview-portal/)hello 記錄失敗的元件。 透過稽核記錄檔，您可以判斷︰

* 已發生的作業
* 誰 hello 作業
* Hello 作業發生時
* hello hello 作業狀態
* 其他屬性，以幫助您 hello 值研究 hello 作業

hello 稽核記錄檔會包含在您的資源上執行所有寫入作業 (PUT、 POST、 DELETE)，但不包括讀取的作業 (GET)。

## <a name="microsoft-monitoring-agent"></a>Microsoft Monitoring Agent
資訊安全中心使用 hello Microsoft Monitoring Agent – 這是使用相同的代理程式的 hello Operations Management Suite，記錄分析服務 – toocollect 安全性資料從 Azure 虛擬機器的 hello。 已啟用資料收集和 hello 代理程式已正確安裝在 hello 目標電腦之後，應該在執行 hello 程序：

* HealthService.exe

如果您開啟 hello 服務管理主控台 (services.msc)，您也會看到 hello Microsoft Monitoring Agent 服務正在執行如下所示：

![服務](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig5.png)

toosee 您擁有 hello 代理程式的版本，開啟**工作管理員**，hello 中**處理程序** 索引標籤找出 hello **Microsoft Monitoring Agent 服務**，以滑鼠右鍵按一下它，按一下**屬性**。 在 hello**詳細資料**索引標籤上，尋找 hello 檔案版本，如下所示：

![檔案](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig6.png)
   

## <a name="microsoft-monitoring-agent-installation-scenarios"></a>Microsoft Monitoring Agent 安裝案例
有兩個安裝案例，您的電腦上安裝 Microsoft Monitoring Agent hello 時可以產生不同的結果。 支援的 hello 案例包括：

* **資訊安全中心會自動安裝的代理程式**： 在此案例中您將無法 tooview hello 警示位置、 資訊安全中心和搜尋記錄檔中的。 您會收到電子郵件通知 toohello 電子郵件地址的 hello 訂閱 hello 資源所屬 hello 安全性原則中設定。
.
* **在 VM 上手動安裝代理程式位於 Azure**： 在此案例中，如果您使用下載並安裝之前手動 tooFebruary 2017 代理程式，您將會無法 tooview hello 警示 hello 資訊安全中心入口網站中的，只有當您篩選 hello訂閱 hello 工作區所屬的。 在中篩選 hello 訂閱 hello 資源上的屬於的案例，您不是能 toosee 任何警示。 您會收到電子郵件通知 toohello 電子郵件地址的所屬的工作區中的訂閱 hello hello hello 安全性原則中設定。

>[!NOTE]
> tooavoid hello 行為 hello 中說明的第二，請確定您下載 hello hello 代理程式的最新版本。
> 

## <a name="troubleshooting-monitoring-agent-network-requirements"></a>針對監視代理程式網路需求進行疑難排解
代理程式與資訊安全中心的 tooconnect tooand 暫存器，它們必須存取 toonetwork 資源，包括 hello 連接埠號碼和網域 Url。

- Proxy 伺服器，您需要 hello 資源在代理程式設定中設定適當的 proxy 伺服器的 tooensure。 閱讀這篇文章取得更多資訊[toochange hello proxy 設定的方式](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-windows-agents#configure-proxy-settings)。
- 限制存取 toohello 網際網路的防火牆，您需要 tooconfigure 您防火牆 toopermit 存取 tooOMS。 您不需要在代理程式設定中進行任何動作。

hello 下表會顯示通訊所需的資源。

| 代理程式資源 | 連接埠 | 略過 HTTPS 檢查 |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | 是 |
| *.oms.opinsights.azure.com | 443 | 是 |
| *.blob.core.windows.net | 443 | 是 |
| *.azure-automation.net | 443 | 是 |

如果您遇到與 hello 代理程式的登入問題，請確定 tooread hello 文章[tootroubleshoot Operations Management Suite 登入的發出方式](https://support.microsoft.com/en-us/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues)。


## <a name="troubleshooting-endpoint-protection-not-working-properly"></a>針對端點保護無法正常運作的問題進行疑難排解

hello 客體代理程式是否 hello 父處理序的所有項目 hello [Microsoft 反惡意程式碼](../security/azure-security-antimalware.md)延伸模組就是。 Hello 客體代理程式處理序失敗時，可能也會失敗 hello hello 客體代理程式的子處理序形式執行的 Microsoft Antimalware。  在這類案例中是建議的 tooverify hello 下列選項：

- 如果 hello 目標 VM 是自訂映像，而 hello hello VM 建立者永遠不會安裝客體代理程式。
- 如果 hello 目標 Linux VM，而不是 Windows VM，然後安裝 Linux VM 上的 hello Windows hello 反惡意程式碼擴充功能版本將會失敗。 hello Linux 客體代理程式有特定需求方面 OS 版本和所需的封裝，如果不符合這些需求 hello VM 代理程式將無法運作那里可能。 
- 如果使用較舊版本的客體代理程式建立 hello VM。 如果資料，您應該注意一些舊的代理程式可能無法自動更新本身 toohello 較新版本中，這可能會導致 toothis 問題。 如果建立自己的映像，請一律使用 hello 最新版客體代理程式。
- 某些協力廠商系統管理軟體可能會停用 hello 客體代理程式，或封鎖存取 toocertain 檔案位置。 如果您有協力廠商安裝在您的 VM 上，請確定該 hello 代理程式位於 hello 排除清單。
- 某些防火牆設定或網路安全性群組 (NSG) 可能會封鎖網路流量 tooand 從客體代理程式。
- 某些存取控制清單 (ACL) 可能會防止磁碟存取。
- 磁碟空間不足可能會封鎖 hello 客體代理程式無法正常運作。 

依預設 hello Microsoft 反惡意程式碼使用者介面已停用，讀取[對 Azure 資源管理員的 Vm 部署後啟用 Microsoft 反惡意程式碼使用者介面](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/09/enabling-microsoft-antimalware-user-interface-post-deployment/)如需有關如何 tooenable 如果您需要它。

## <a name="troubleshooting-problems-loading-hello-dashboard"></a>載入 hello 儀表板的問題疑難排解

如果您遇到問題載入 hello 資訊安全中心儀表板，請確定註冊 hello 訂閱 tooSecurity 中心 （也就是 hello 第一位使用者開啟資訊安全中心與 hello 訂用帳戶的其中一個） 該 hello 使用者以及 hello 使用者希望 tooturn資料收集應該*擁有者*或*參與者*hello 訂用帳戶。 從該時間點也使用對使用者*讀取器*hello 在訂用帳戶可以看到 hello 儀表板/警示/建議/原則。

## <a name="contacting-microsoft-support"></a>連絡 Microsoft 支援服務
可以使用這份文件中提供的 hello 指導方針來識別一些問題，您也可以找到的其他項目記錄在 hello 資訊安全中心公用[論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureSecurityCenter)。 不過，如果您需要進一步疑難排解，您可以使用 **Azure 入口網站**開啟新的支援要求，如下所示︰ 

![Microsoft 支援服務](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig2.png)


## <a name="see-also"></a>另請參閱
在本文件中，您學到如何 tooconfigure Azure 資訊安全中心中的安全性原則。 toolearn 進一步了解 Azure 資訊安全中心，請參閱 hello 下列資訊：

* [Azure 資訊安全中心計劃與作業指南](security-center-planning-and-operations-guide.md)— 了解如何 tooplan 並了解 hello 設計考量 tooadopt Azure 資訊安全中心。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)— 了解如何 toomonitor hello 您的 Azure 資源的健全狀況
* [Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) — 了解如何 toomanage 和回應 toosecurity 警示
* [監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)— 了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)— 尋找使用 hello 服務相關的常見問題集
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) — 尋找有關 Azure 安全性與相容性的部落格文章。

