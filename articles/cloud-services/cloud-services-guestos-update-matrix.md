---
title: "關於 aaaLearn hello 最新的 Azure 客體作業系統版本 |Microsoft 文件"
description: "hello Azure 雲端服務客體作業系統的最新版本新聞與 SDK 相容性。"
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
ms.date: 8/24/2017
ms.author: raiye
ms.openlocfilehash: 7274f5a68a32ce91bdede77e1443cdb8053c07ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-guest-os-releases-and-sdk-compatibility-matrix"></a>Azure 客體 OS 版次與 SDK 相容性矩陣
您提供最新的 Azure 客體 OS 版本的雲端服務的 hello 的最新資訊。 此資訊協助您在客體 OS停用之前規劃升級路徑。 如果您設定角色 toouse*自動*客體 OS 更新中所述[Azure 客體 OS 更新設定][Azure Guest OS Update Settings]，不需要您先閱讀此頁面。

> [!IMPORTANT]
> 此頁面適用於 tooCloud 服務 web 和背景工作角色，在客體作業系統上執行。 它會**不會套用**tooIaaS 虛擬機器。
>
>


> [!NOTE]
> RSS 摘要的 hello 最近已被取代。 請密切注意即將推出的全新摘要更新！
>
>

確定哪些客體作業系統或如何 hello 的 hello 客體 OS 版本的工作？ 請閱讀 [本節內容](#how-it-works) 。

## <a name="news-updates"></a>新聞更新

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

###### <a name="june-5-2017"></a>**2017 年 6 月 5 日**
5 月客體 OS 已發行。

###### <a name="may-17-2017"></a>**2017 年 5 月 17 日**
Tooa 安全性的問題，因為我們要停用下列 2016 年 12 月和年 1 月 2017 hello 沒有 hello 的 OS 版本[修正]從 hello 入口網站： WA-客體-OS-5.4_201612-01，WA-客體-OS-4.39_201612-01，WA-客體-OS-3.46_WA 201612-01-客體-OS-2.59_201701-01

###### <a name="may-12-2017"></a>**2017 年 5 月 12 日**
5 月客體 OS 的首度發行期間從 5 月 12 日開始，預訂的正式發行日為 6 月 13 日。

###### <a name="april-18-2017"></a>**2017 年 4 月 18 日**
4 月客體 OS 的首度發行期間從 4 月 18 日開始，預訂的正式發行日為 5 月 9 日。

###### <a name="april-10-2017"></a>**2017 年 4 月 10 日**
3 月的客體 OS 的度發行期間從 2017 年 3 月 14 日開始，預訂發行日為 2017 年 4 月 10 日。

###### <a name="january-10-2017"></a>**2017 年 1 月 10 日**
hello 年 1 月客體 OS 包含只會影響作業系統系列 2 (Windows 2008 Server R2) 的修補程式。 因此，我們已發行只 hello OS 系列 2 的映像 (WA-客體-OS-2.59_201701-01) 本月份。 針對所有其他作業系統系列，hello 年 12 月 OS (201612-01） 保持最新 hello。


## <a name="releases"></a>版次
## <a name="family-5-releases"></a>系列 5 版次
**Windows Server, 2016**

安裝的 .NET Framework：4.0、4.5、4.5.1、4.5.2、4.6、4.6.1、4.6.2

> [!NOTE]
> 日期與 * 是主體 toochange。
>
> hello OS 系列 5 RDP 密碼必須至少 10 個字元。
>

| 組態字串 | 發行日期 | 停用日期 | 到期日期 |
| --- | --- | --- | --- |
| WA-GUEST-OS-5.10_201708-01 |2017 年 8 月 24 日 |Post 5.12 |TBD |
| WA-GUEST-OS-5.9_201707-01 |2017 年 8 月 3 日 |Post 5.11 |TBD |
| WA-GUEST-OS-5.8_201706-01 |2017 年 7 月 7 日 |Post 5.10 |TBD |
|~~WA-GUEST-OS-5.7_201705-01~~ |2017 年 6 月 5 日 |2017 年 8 月 24 日 |TBD |
|~~WA-GUEST-OS-5.6_201704-01~~ |2017 年 5 月 9 日 |2017 年 8 月 3 日 |TBD |
|~~WA-GUEST-OS-5.5_201703-01~~ |2017 年 4 月 10 日 |2017 年 7 月 7 日 |TBD |
|~~WA-GUEST-OS-5.4_201612-01~~ |2017 年 1 月 10 日 |2017 年 6 月 5 日|TBD |
|~~WA-GUEST-OS-5.3_201611-01~~ |2016 年 12 月 14 日 |2017 年 5 月 9 日 |TBD |
|~~WA-GUEST-OS-5.2_201610-02~~ |2016 年 11 月 1 日 |2017 年 4 月 10 日 |TBD |

## <a name="family-4-releases"></a>系列 4 版次
**Windows Server 2012 R2**

支援 .NET 4.0、4.5、4.5.1、4.5.2

> [!NOTE]
> 日期與 * 是主體 toochange
>
>

| 組態字串 | 發行日期 | 停用日期 | 到期日期 |
| --- | --- | --- | --- |
| WA-GUEST-OS-4.45_201708-01 |2017 年 8 月 24 日 |Post 4.47 |TBD |
| WA-GUEST-OS-4.44_201707-01 |2017 年 8 月 3 日 |Post 4.46 |TBD |
| WA-GUEST-OS-4.43_201706-01 |2017 年 7 月 7 日 |Post 4.45 |TBD |
|~~WA-GUEST-OS-4.42_201705-01~~ |2017 年 6 月 5 日 |2017 年 8 月 24 日 |TBD |
|~~WA-GUEST-OS-4.41_201704-01~~ |2017 年 5 月 9 日 |2017 年 8 月 3 日 |TBD |
|~~WA-GUEST-OS-4.40_201703-01~~ |2017 年 4 月 10 日 |2017 年 7 月 7 日 |TBD |
|~~WA-GUEST-OS-4.39_201612-01~~ |2017 年 1 月 10 日 |2017 年 6 月 5 日 |TBD |
|~~WA-GUEST-OS-4.38_201611-01~~ |2016 年 12 月 14 日 |2017 年 5 月 9 日 |TBD |
|~~WA-GUEST-OS-4.37_201610-02~~ |2016 年 11 月 16 日 |2017 年 4 月 10 日 |TBD |
|~~WA-GUEST-OS-4.36_201609-01~~ |2016 年 10 月 13 日 |2017 年 1 月 14 日 |TBD |
|~~WA-GUEST-OS-4.35_201608-01~~ |2016 年 9 月 13 日 |2016 年 12 月 16 日 |TBD |
|~~WA-GUEST-OS-4.34_201607-01~~ |2016 年 8 月 8 日 |2016 年 11 月 13 日 |TBD |


## <a name="family-3-releases"></a>系列 3 版次
**Windows Server 2012**

支援 .NET 4.0、4.5、4.5.1、4.5.2

> [!NOTE]
> 日期與 * 是主體 toochange
>
>

| 組態字串 | 發行日期 | 停用日期 | 到期日期 |
| --- | --- | --- | --- |
| WA-GUEST-OS-3.52_201708-01 |2017 年 8 月 24 日 |Post 3.54 |TBD |
| WA-GUEST-OS-3.51_201707-01 |2017 年 8 月 3 日 |Post 3.53 |TBD |
| WA-GUEST-OS-3.50_201706-01 |2017 年 7 月 7 日 |Post 3.52 |TBD |
|~~WA-GUEST-OS-3.49_201705-01~~ |2017 年 6 月 5 日 |2017 年 8 月 24 日 |TBD |
|~~WA-GUEST-OS-3.48_201704-01~~ |2017 年 5 月 9 日 |2017 年 8 月 3 日 |TBD |
|~~WA-GUEST-OS-3.47_201703-01~~ |2017 年 4 月 10 日 |2017 年 7 月 7 日 |TBD |
|~~WA-GUEST-OS-3.46_201612-01~~ |2017 年 1 月 10 日 |2017 年 6 月 5 日 |TBD |
|~~WA-GUEST-OS-3.45_201611-01~~ |2016 年 12 月 14 日 |2017 年 5 月 9 日 |TBD |
|~~WA-GUEST-OS-3.44_201610-02~~ |2016 年 11 月 16 日 |2017 年 5 月 1 日 |TBD |
|~~WA-GUEST-OS-3.43_201609-01~~ |2016 年 10 月 13 日 |2017 年 1 月 14 日 |TBD |
|~~WA-GUEST-OS-3.42_201608-01~~ |2016 年 9 月 13 日 |2016 年 12 月 16 日 |TBD |
|~~WA-GUEST-OS-3.41_201607-01~~ |2016 年 8 月 8 日 |2016 年 11 月 13 日 |TBD |


## <a name="family-2-releases"></a>系列 2 版次
**Windows Server 2008 R2 SP1**

支援 .NET 3.5、4.0、4.5、4.5.1、4.5.2

> [!NOTE]
> 日期與 * 是主體 toochange
>
>

| 組態字串 | 發行日期 | 停用日期 | 到期日期 |
| --- | --- | --- | --- |
| WA-GUEST-OS-2.65_201708-01 |2017 年 8 月 24 日 |Post 2.67 |TBD |
| WA-GUEST-OS-2.64_201707-01 |2017 年 8 月 3 日 |Post 2.66 |TBD |
| WA-GUEST-OS-2.63_201706-01 |2017 年 7 月 7 日 |Post 2.65 |TBD |
|~~WA-GUEST-OS-2.62_201705-01~~ |2017 年 6 月 5 日 |2017 年 8 月 24 日 |TBD |
|~~WA-GUEST-OS-2.61_201704-01~~ |2017 年 5 月 9 日 |2017 年 8 月 3 日 |TBD |
|~~WA-GUEST-OS-2.60_201703-01~~ |2017 年 4 月 10 日 |2017 年 7 月 7 日 |TBD |
|~~WA-GUEST-OS-2.59_201701-01~~ |2017 年 1 月 10 日 |2017 年 6 月 5 日 |TBD |
|~~WA-GUEST-OS-2.58_201612-01~~ |2017 年 1 月 10 日 |2017 年 5 月 9 日|TBD |
|~~WA-GUEST-OS-2.57_201611-01~~ |2016 年 12 月 14 日 |2017 年 4 月 10 日 |TBD |
|~~WA-GUEST-OS-2.56_201610-02~~ |2016 年 11 月 16 日 |2017 年 2 月 10 日 |TBD |
|~~WA-GUEST-OS-2.55_201609-01~~ |2016 年 10 月 13 日 |2017 年 1 月 14 日 |TBD |
|~~WA-GUEST-OS-2.54_201608-01~~ |2016 年 9 月 13 日 |2016 年 12 月 16 日 |TBD |
|~~WA-GUEST-OS-2.53_201607-01~~ |2016 年 8 月 8 日 |2016 年 11 月 13 日 |TBD |



## <a name="msrc-patch-updates"></a>MSRC 修補程式更新
hello 的隨附於每個月的客體作業系統版本的修補程式清單為可用[這裡][patches]。

## <a name="sdk-support"></a>SDK 支援
即使 hello [hello Azure SDK 的淘汰原則][ retire policy sdk]表示只有上述 2.2 版本是支援的特定客體 OS 系列允許您 toouse 較早版本。 您應該一律使用 hello 最新支援的 SDK。

| 客體作業系統系列 | 相容的 SDK 版本 |
| --- | --- |
| 5 |版本 2.9.5.1+ |
| 4 |版本 2.1+ |
| 3 |版本 1.8+ |
| 2 |版本 1.3+ |
| 1 |版本 1.0+ |

## <a name="guest-os-release-information"></a>客體作業系統版次資訊
有三個重要 tooGuest OS 釋放的日期：**釋放**日期**停用**日期，以及**到期**日期。 客體 OS hello 入口網站中，可以選擇作為 hello 目標客體 OS 時，就會視為可用。 當客體 OS 到達 hello**停用**日期，它會從 Azure 中移除。 不過，以該客體 OS 為目標的任何雲端服務將仍正常運作。

hello 視窗之間 hello**停用**日期和 hello**到期**日期為您提供一個較新的客體 OS tooone 緩衝區 tooeasily 轉換。 如果您使用*自動*做為客體作業系統，您將一律位於 hello 最新版本，而且不需要 tooworry 資訊，請設定為已過期。

當 hello**到期**成功，任何雲端服務，仍在使用該客體作業系統將會停止、 已刪除，或強制 tooupgrade 的日期。 閱讀更多有關 hello 淘汰原則[這裡][retirepolicy]。

## <a name="guest-os-family-version-explanation"></a>客體 OS 系列版本說明
hello 客體 OS 系列以 Microsoft Windows Server 的發行版本。 hello 客體 OS 是 hello 基礎作業系統上執行 Azure 雲端服務。 每一個客體作業系統都有系列、版本和版次號碼。

* **Guest OS family**  
  是客體 OS 所根據的 Windows Server 作業系統版次。 例如，「系列 3」  以 Windows Server 2012 為基礎。
* **客體 OS 版本**  
  特定 tooa 客體 OS 系列映像加上相關[Microsoft Security Response Center (MSRC)] [ msrc]產生可以在 hello 日期 hello 新版客體 OS 修補程式。 不一定包含所有修補程式。

    編號從 0 開始，每增加一組新的更新就加 1。 必要時才會顯示尾端的零。 亦即，2.10 版是與 2.1 版不同且更新的版本。
* **客體 OS 版次**  
  是指客體 OS 版本的再發行版次。 如果 Microsoft 在測試期間發現問題而需要變更時，就會推出再發行版次。 hello 最新版本一定會取代任何先前釋放，公用與否。 hello Azure 入口網站只會允許使用者指定版本的 toopick hello 最新版本。 在先前的版本上執行的部署通常不強制升級視 hello 的 hello bug 的嚴重性而定。

在 hello 面範例中，2 是 hello 系列，12 是 hello 版本，"rel2"是 hello 版本。

**客體作業系統版次** - 2.12 rel2

**此版次的組態字串** - WA-GUEST-OS-2.12_201208-02

客體 OS 的 hello 組態字串具有此相同的資訊內嵌在以及顯示該發行考量哪些 MSRC 修補程式的日期。 在此範例中，向上 tooand 包括 2012 年 8 月產生的 Windows Server 2008 R2 的 MSRC 修補程式已以納入考量。 只有唯獨具體 toothat 版本的 Windows Server 隨附。 例如，如果 MSRC 修補程式套用 tooMicrosoft Office，它將不會包含因為該產品並非 hello Windows Server 的基底映像的一部分。

## <a name="guest-os-system-update-process"></a>客體作業系統的系統更新程序
此頁面包含即將推出的客體作業系統版次的相關資訊。 客戶表示想 tooknow 版次，因為其雲端服務角色設定過 「 自動的 」 更新將會重新開機時。 客體作業系統版次通常會發生至少五 （5） 天 hello MSRC 更新之後，就會發生在 hello 每個月的第二個星期二的版本。 新的版本包括在所有 hello 相關 MSRC 修補程式的每個客體 OS 系列。

Microsoft Azure 正持續發行更新。 hello 客體 OS 是 hello 管線中的只能有一個這類更新。 在版本可能會受到許多因素太多 toolist 這裡。 此外，Azure 實際上是在成千上萬個電腦上執行。 這表示它是不可能 toogive 的確切日期和時間，當您的角色將重新啟動。 我們計劃 toolimit 正在處理，或控制重新開機時間。

當已發行客體 OS 的 hello 新版本中時，可能需要的時間 toofully 傳播至整個 Azure。 因為服務更新的 toohello 新的客體 OS，會重新啟動接受更新網域。 服務設定 toouse 「 自動 」 更新，會先取得版次。 Hello 更新之後，您會看見 hello 新的客體作業系統版本列出為您的服務在 hello Azure 入口網站。 此期間可能再度發行版次。 某些版本可能會部署一段較長的時間，有好幾個星期 hello 正式發行日期之後，可能不會自動升級重新啟動。 一旦可以使用客體作業系統，您可以再明確選擇該版本從 hello 入口網站，或在組態檔中。

大量上重新啟動和指標 toomore 資訊技術詳細資料的來賓和主機作業系統更新的重要資訊，請參閱 hello MSDN 部落格文章 <<c0> [ 角色執行個體因而重新啟動 tooOS 升級][ restarts].

如果您手動更新客體作業系統，請參閱 hello[客體作業系統淘汰原則][ retirepolicy]如需詳細資訊。

## <a name="guest-os-supportability-and-retirement-policy"></a>客體作業系統可支援性和淘汰原則
hello 客體 OS 可支援性和淘汰原則說明[這裡][retirepolicy]。

[Install .NET on a Cloud Service Role]: https://azure.microsoft.com/en-us/documentation/articles/cloud-services-dotnet-install-dotnet/?WT.mc_id=azurebg_email_Trans_963_RevisedNET_Update
[Azure Guest OS Update Settings]: cloud-services-how-to-configure.md
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
[修正]: https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
