---
title: "了解最新的 Azure 客體 OS 版次 | Microsoft Docs"
description: "Azure 雲端服務客體作業系統的發行最新消息和 SDK 相容性。"
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 6306cafe-1153-44c7-8554-623b03d59a34
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 1/4/2018
ms.author: raiye
ms.openlocfilehash: e645d57dfff040eb05f4d395fac058b2b485933b
ms.sourcegitcommit: d6984ef8cc057423ff81efb4645af9d0b902f843
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="azure-guest-os-releases-and-sdk-compatibility-matrix"></a>Azure 客體 OS 版次與 SDK 相容性矩陣
提供適用於雲端服務的最新 Azure 客體作業系統版次的最新資訊。 此資訊協助您在客體 OS停用之前規劃升級路徑。 如果您將角色設定成使用「自動」客體 OS 更新 (如 [Azure 客體 OS 更新設定][Azure Guest OS Update Settings]所述)，就不一定要閱讀此頁面。

> [!IMPORTANT]
> 此頁面適用於客體作業系統上執行的雲端服務 Web 角色和背景工作角色。 不適用  於 IaaS 虛擬機器。
>
>


> [!TIP]
>  請訂閱[客體 OS 更新 RSS 摘要]，以接收有關所有客體 OS 變更的最及時性通知。
>
>

> [!IMPORTANT]
> 從 11 月首度發行開始，僅支援最新 2 版的客體 OS，並可在 Azure 入口網站取得。
>
>

不確定客體 OS 為何或客體 OS 版次如何工作？ 請閱讀 [本節內容](#how-it-works) 。

## <a name="news-updates"></a>新聞更新
###### <a name="january-4-2018"></a>**2018 年 1 月 4 日**
已釋放年 1 月客體作業系統的 OS 系列 4 (WA-客體-OS-4.50_201801-01) & 5 (WA-客體-OS-5.15_201801-01) 並包含重要的安全性修補程式。  

###### <a name="january-4-2018"></a>**2018 年 1 月 4 日**
年 12 月客體 OS 已發行。

###### <a name="december-14-2017"></a>**2017 年 12 月 14 日**
11 月客體 OS 已發行。

###### <a name="november-8-2017"></a>**2017 年 11 月 8 日**
10 月客體 OS 已發行。

###### <a name="october-6-2017"></a>**2017 年 10 月 6 日**
9 月客體 OS 已發行。 在 Windows Server 2016 年 9 月版本中，預設會啟用 netfx3。 如果客戶的工作流程要求他們使用 4.x 執行階段來執行 .NET 2.x 應用程式，或如果他們執行了 .NET 2.x 應用程式、處理了錯誤，然後執行了.NET 4.x 應用程式，就應該在客戶的 OnStart 中新增 ‘dism /online /disable-feature /featurename:netfx3’。

###### <a name="september-14-2017"></a>**2017 年 9 月 14 日**
9 月客體 OS 的首度發行期間從 9 月 14 日開始，預訂的正式發行日為 10 月 9 日。

###### <a name="august-24-2017"></a>**2017 年 8 月 24 日**
8 月客體 OS 已發行。

###### <a name="august-3-2017"></a>**2017 年 8 月 3 日**
7 月客體 OS 已發行。

###### <a name="july-19-2017"></a>**2017 年 7 月 19 日**
7 月客體 OS 的首度發行期間從 7 月 19 日開始，預訂的正式發行日為 8 月 8 日。

###### <a name="july-7-2017"></a>**2017 年 7 月 7 日**
6 月客體 OS 已發行。

###### <a name="june-16-2017"></a>**2017 年 6 月 16 日**
6 月客體 OS 的首度發行期間從 6 月 16 日開始，預訂的正式發行日為 7 月 11 日。


## <a name="releases"></a>版次
## <a name="family-5-releases"></a>系列 5 版次
**Windows Server 2016**

安裝的 .NET Framework：4.0、4.5、4.5.1、4.5.2、4.6、4.6.1、4.6.2

> [!NOTE]
> 具有 * 的日期可能會變更。
>
> 作業系統系列 5 的 RDP 密碼至少需要 10 個字元。
>

| 組態字串 | 發行日期 | 停用日期 | 到期日期 |
| --- | --- | --- | --- |
| WA-客體-OS-5.15_201801-01 |2018 年 1 月 4 日 |Post 5.17 |TBD |
| WA-客體-OS-5.14_201712-01 |2018 年 1 月 4 日 |Post 5.16 |TBD |
| WA-客體-OS-5.13_201711-01 |2017 年 12 月 14 日 |Post 5.15 |TBD |
|~~WA-客體-OS-5.12_201710-02~~ |2017 年 11 月 8 日 |2018 年 1 月 4 日 |TBD |
|~~WA-客體-OS-5.11_201709-01~~ |2017 年 10 月 6 日 |2017 年 12 月 14 日 |TBD |
|~~WA-客體-OS-5.10_201708-01~~ |2017 年 8 月 24 日 |2017 年 12 月 14 日 |TBD |
|~~WA-GUEST-OS-5.9_201707-01~~ |2017 年 8 月 3 日 |2017 年 11 月 8 日 |TBD |
|~~WA-GUEST-OS-5.8_201706-01~~ |2017 年 7 月 7 日 |2017 年 10 月 6 日 |TBD |
|~~WA-GUEST-OS-5.7_201705-01~~ |2017 年 6 月 5 日 |2017 年 8 月 24 日 |TBD |
|~~WA-GUEST-OS-5.6_201704-01~~ |2017 年 5 月 9 日 |2017 年 8 月 3 日 |TBD |
|~~WA-GUEST-OS-5.5_201703-01~~ |2017 年 4 月 10 日 |2017 年 7 月 7 日 |TBD |
|~~WA-GUEST-OS-5.4_201612-01~~ |2017 年 1 月 10 日 |2017 年 6 月 5 日|TBD |

## <a name="family-4-releases"></a>系列 4 版次
**Windows Server 2012 R2**

安裝的 .NET Framework：4.0、4.5、4.5.1、4.5.2

> [!NOTE]
> 具有 * 的日期可能會變更
>
>

| 組態字串 | 發行日期 | 停用日期 | 到期日期 |
| --- | --- | --- | --- |
| WA-客體-OS-4.50_201801-01 |2018 年 1 月 4 日 |Post 4.52 |TBD |
| WA-客體-OS-4.49_201712-01 |2018 年 1 月 4 日 |Post 4.51 |TBD |
| WA-客體-OS-4.48_201711-01 |2017 年 12 月 14 日 |Post 4.50 |TBD |
|~~WA-客體-OS-4.47_201710-02~~ |2017 年 11 月 8 日 |2018 年 1 月 4 日 |TBD |
|~~WA-客體-OS-4.46_201709-01~~ |2017 年 10 月 6 日 |2017 年 12 月 14 日 |TBD |
|~~WA-客體-OS-4.45_201708-01~~ |2017 年 8 月 24 日 |2017 年 12 月 14 日 |TBD |
|~~WA-GUEST-OS-4.44_201707-01~~ |2017 年 8 月 3 日 |2017 年 11 月 8 日 |TBD |
|~~WA-GUEST-OS-4.43_201706-01~~ |2017 年 7 月 7 日 |2017 年 10 月 6 日 |TBD |
|~~WA-GUEST-OS-4.42_201705-01~~ |2017 年 6 月 5 日 |2017 年 8 月 24 日 |TBD |
|~~WA-GUEST-OS-4.41_201704-01~~ |2017 年 5 月 9 日 |2017 年 8 月 3 日 |TBD |
|~~WA-GUEST-OS-4.40_201703-01~~ |2017 年 4 月 10 日 |2017 年 7 月 7 日 |TBD |
|~~WA-GUEST-OS-4.39_201612-01~~ |2017 年 1 月 10 日 |2017 年 6 月 5 日 |TBD |

## <a name="family-3-releases"></a>系列 3 版次
**Windows Server 2012**

安裝的 .NET Framework：4.0、4.5、4.5.1、4.5.2

> [!NOTE]
> 具有 * 的日期可能會變更
>
>

| 組態字串 | 發行日期 | 停用日期 | 到期日期 |
| --- | --- | --- | --- |
| WA-客體-OS-3.56_201712-01 |2018 年 1 月 4 日 |Post 3.58 |TBD |
| WA-客體-OS-3.55_201711-01 |2017 年 12 月 14 日 |Post 3.57 |TBD |
|~~WA-客體-OS-3.54_201710-02~~ |2017 年 11 月 8 日 |2018 年 1 月 4 日 |TBD |
|~~WA-客體-OS-3.53_201709-01~~ |2017 年 10 月 6 日 |2017 年 12 月 14 日 |TBD |
|~~WA-客體-OS-3.52_201708-01~~ |2017 年 8 月 24 日 |2017 年 12 月 14 日 |TBD |
|~~WA-GUEST-OS-3.51_201707-01~~ |2017 年 8 月 3 日 |2017 年 11 月 8 日 |TBD |
|~~WA-GUEST-OS-3.50_201706-01~~ |2017 年 7 月 7 日 |2017 年 10 月 6 日 |TBD |
|~~WA-GUEST-OS-3.49_201705-01~~ |2017 年 6 月 5 日 |2017 年 8 月 24 日 |TBD |
|~~WA-GUEST-OS-3.48_201704-01~~ |2017 年 5 月 9 日 |2017 年 8 月 3 日 |TBD |
|~~WA-GUEST-OS-3.47_201703-01~~ |2017 年 4 月 10 日 |2017 年 7 月 7 日 |TBD |
|~~WA-GUEST-OS-3.46_201612-01~~ |2017 年 1 月 10 日 |2017 年 6 月 5 日 |TBD |

## <a name="family-2-releases"></a>系列 2 版次
**Windows Server 2008 R2 SP1**

安裝的 .NET Framework：3.5、4.0、4.5、4.5.1、4.5.2

> [!NOTE]
> 具有 * 的日期可能會變更
>
>

| 組態字串 | 發行日期 | 停用日期 | 到期日期 |
| --- | --- | --- | --- |
| WA-客體-OS-2.69_201712-01 |2018 年 1 月 4 日 |Post 2.71 |TBD |
| WA-客體-OS-2.68_201711-01 |2017 年 12 月 14 日 |Post 2.70 |TBD |
|~~WA-客體-OS-2.67_201710-02~~ |2017 年 11 月 8 日 |2018 年 1 月 4 日 |TBD |
|~~WA-客體-OS-2.66_201709-01~~ |2017 年 10 月 6 日 |2017 年 12 月 14 日 |TBD |
|~~WA-客體-OS-2.65_201708-01~~ |2017 年 8 月 24 日 |2017 年 12 月 14 日 |TBD |
|~~WA-GUEST-OS-2.64_201707-01~~ |2017 年 8 月 3 日 |2017 年 11 月 8 日 |TBD |
|~~WA-GUEST-OS-2.63_201706-01~~ |2017 年 7 月 7 日 |2017 年 10 月 6 日 |TBD |
|~~WA-GUEST-OS-2.62_201705-01~~ |2017 年 6 月 5 日 |2017 年 8 月 24 日 |TBD |
|~~WA-GUEST-OS-2.61_201704-01~~ |2017 年 5 月 9 日 |2017 年 8 月 3 日 |TBD |
|~~WA-GUEST-OS-2.60_201703-01~~ |2017 年 4 月 10 日 |2017 年 7 月 7 日 |TBD |
|~~WA-GUEST-OS-2.59_201701-01~~ |2017 年 1 月 10 日 |2017 年 6 月 5 日 |TBD |
|~~WA-GUEST-OS-2.58_201612-01~~ |2017 年 1 月 10 日 |2017 年 5 月 9 日|TBD |


## <a name="msrc-patch-updates"></a>MSRC 修補程式更新
[這裡][patches]提供每月客體 OS 版次隨附的修補程式清單。

## <a name="sdk-support"></a>SDK 支援
雖然 [Azure SDK 的淘汰原則][retire policy sdk]指出只支援 2.2 以上的版本，但特定客體 OS 系列仍允許您使用更舊的版本。 您應該一律使用最新版本的支援 SDK。

| 客體作業系統系列 | 相容的 SDK 版本 |
| --- | --- |
| 5 |版本 2.9.5.1+ |
| 4 |版本 2.1+ |
| 3 |版本 1.8+ |
| 2 |版本 1.3+ |
| 1 |版本 1.0+ |

## <a name="guest-os-release-information"></a>客體作業系統版次資訊
有三個重要的客體 OS 版次日期：**發行**日期、**停用**日期，以及**到期**日期。 客體 OS 在入口網站時會視為可用，且可以選擇作為目標客體 OS。 當客體 OS 觸達**停用**日期時，會從 Azure 中移除。 不過，以該客體 OS 為目標的任何雲端服務將仍正常運作。

**停用**日期和**到期**日期之間的時間範圍，提供一個緩衝區，讓您可以輕鬆從一個客體 OS 轉換到到較新的客體 OS。 如果您使用「自動化」  作為客體 OS，則一律會是最新版本，不必擔心過期問題。

當**到期**日期已過，任何仍在使用該客體 OS 的雲端服務將會遭到停止、刪除或強制升級。 您可以從[這裡][retirepolicy]閱讀更多有關淘汰原則的資訊。

## <a name="guest-os-family-version-explanation"></a>客體 OS 系列版本說明
客體作業系統系列以 Microsoft Windows Server 的發行版本為基礎。 客體作業系統是指執行 Azure 雲端服務的基礎作業系統。 每一個客體作業系統都有系列、版本和版次號碼。

* **Guest OS family**  
  是客體 OS 所根據的 Windows Server 作業系統版次。 例如，「系列 3」  以 Windows Server 2012 為基礎。
* **客體 OS 版本**  
  客體 OS 系列映像特定，加上新客體 OS 版本產生當天可用的相關 [Microsoft Security Response Center (MSRC)][msrc] 修補程式。 不一定包含所有修補程式。

    編號從 0 開始，每增加一組新的更新就加 1。 必要時才會顯示尾端的零。 亦即，2.10 版是與 2.1 版不同且更新的版本。
* **客體 OS 版次**  
  是指客體 OS 版本的再發行版次。 如果 Microsoft 在測試期間發現問題而需要變更時，就會推出再發行版次。 最新的版次一律取代任何先前的版次，無論是否公開都一樣。 Azure 入口網站只允許使用者挑選特定版本的最新版次。 視錯誤的嚴重性而定，通常不會強制升級舊版次上執行的部署。

在下列範例中，2 是系列，12 是版本，"rel2" 是版次。

**客體作業系統版次** - 2.12 rel2

**此版次的組態字串** - WA-GUEST-OS-2.12_201208-02

客體作業系統的組態字串內嵌這項相同的資訊，還附上指出該版次考量哪些 MSRC 修補程式的日期。 在此範例中，針對 Widows Server 2008 R2 推出的 MSRC 修補程式 (達到且包含 2012 年 8 月) 已考量納入。 只會包含明確適用於該 Windows Server 版本的修補程式。 例如，如果某個 MSRC 修補程式適用於 Microsoft Office，則不會納入，因為該產品不是 Windows Server 基本映像的一部分。

## <a name="guest-os-system-update-process"></a>客體作業系統的系統更新程序
此頁面包含即將推出的客體作業系統版次的相關資訊。 客戶表示想要知道何時推出版次，因為他們的雲端服務角色如果設為「自動」更新，將重新啟動。 在每月第二個星期二發行 MSRC 更新後，通常至少五 (5) 天才會推出客體作業系統版次。 新版次包含每個客體作業系統系列的相關 MSRC 修補程式。

Microsoft Azure 正持續發行更新。 客體作業系統只是這過程中的一項更新。 影響版次的因素太多，無法在這裡完整列出。 此外，Azure 實際上是在成千上萬個電腦上執行。 這表示不可能指出您的角色重新啟動的確切日期和時間。 我們正進行規劃來限制或控制重新開機時間。

新版次的客體作業系統發行時，需要一段時間才會完全傳播到整個 Azure。 當服務更新到新的客體作業系統時，它們會重新啟動，讓更新網域生效。 設為「自動」更新的服務會最先取得一個版次。 更新之後，您在 Azure 入口網站中會看到您的服務列出新的客體作業系統版本。 此期間可能再度發行版次。 某些版本的部署期間可能很長，而且在官方發行日期之後，可能經過許多個星期都還不會進行自動升級重新啟動。 當客體作業系統推出時，您可以從入口網站或組態檔中明確地選擇該版本。

如需有關重新啟動的大量實用資訊，以及客體和主機 OS 更新的更多技術細節線索，請參閱標題為[角色執行個體因作業系統升級而重新啟動 (英文)][restarts] 的 MSDN 部落格文章。

如果您手動更新客體 OS，請參閱[客體 OS 淘汰原則][retirepolicy]以取得詳細資訊。

## <a name="guest-os-supportability-and-retirement-policy"></a>客體作業系統可支援性和淘汰原則
如需客體 OS 可支援性和淘汰原則的說明，請參閱[這裡][retirepolicy]。

[客體 OS 更新 RSS 摘要]: https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/master/GuestOS/GuestOSFeed.xml
[Install .NET on a Cloud Service Role]: https://azure.microsoft.com/en-us/documentation/articles/cloud-services-dotnet-install-dotnet/?WT.mc_id=azurebg_email_Trans_963_RevisedNET_Update
[Azure Guest OS Update Settings]: cloud-services-how-to-configure-portal.md
[ssl3 announcement]: http://azure.microsoft.com/blog/2014/12/09/azure-security-ssl-3-0-update/
[Microsoft Security Advisory 3009008]: https://technet.microsoft.com/library/security/3009008.aspx
[ssl3-fixit]: http://go.microsoft.com/?linkid=9863266
[MS14-066]: https://technet.microsoft.com/library/security/ms14-066.aspx
[MS14-046]: https://technet.microsoft.com/library/security/ms14-046.aspx
[retire policy sdk]: https://msdn.microsoft.com/library/dn479282.aspx
[server and gos]: https://msdn.microsoft.com/library/dn775043.aspx
[azuresupport]: http://azure.microsoft.com/support/options/
[net install pkg]: http://www.microsoft.com/download/details.aspx?id=42643
[msrc]: http://www.microsoft.com/security/msrc/default.aspx
[update guest os portal]: https://msdn.microsoft.com/library/gg433101.aspx
[update guest os svc]: https://msdn.microsoft.com/library/gg456324.aspx
[restarts]: http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx
[patches]: cloud-services-guestos-msrc-releases.md
[retirepolicy]: cloud-services-guestos-retirement-policy.md
[fam1retire]: cloud-services-guestos-family1-retirement.md
[fix]: https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
