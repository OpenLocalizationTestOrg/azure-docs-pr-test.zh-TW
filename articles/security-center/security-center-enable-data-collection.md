---
title: "aaaEnable Azure 資訊安全中心中的資料收集 |Microsoft 文件"
description: " 深入了解如何在 Azure 資訊安全中心 tooenable 資料收集。 "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 411d7bae-c9d4-4e83-be63-9f2f2312b075
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 78bbf9a3d852095e2a1387c1606ff4bbb778a0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-data-collection-in-azure-security-center"></a>在 Azure 資訊安全中心啟用資料收集

> [!NOTE]
> 從開始早期年 6 月 2017年，資訊安全中心將會使用 hello Microsoft Monitoring Agent toocollect 及儲存資料。 詳細資訊，請參閱 toolearn [Azure 安全性 Center 平台移轉](security-center-platform-migration.md)。 本文章中的 hello 資訊表示資訊安全中心功能之後轉換 toohello Microsoft Monitoring Agent。
>
>

資訊安全中心會收集從虛擬機器 (Vm) tooassess 其資訊安全狀態、 提供安全性建議事項，並警示您 toothreats。 當您第一次存取資訊安全中心時，您的訂用帳戶中有 hello 選項 tooenable 資料收集的所有 vm。 如果未啟用資料收集，資訊安全中心會建議您開啟 hello 該訂用帳戶的安全性原則中的資料收集。

啟用資料收集時，對所有現有的資訊安全中心會佈建 hello Microsoft Monitoring Agent 支援 Azure 虛擬機器和建立任何新的。 Microsoft Monitoring Agent hello 掃描的各種安全性相關設定。 此外，hello 作業系統引發的事件記錄檔事件。 這類資料的範例包括︰作業系統類型和版本、作業系統記錄檔 (Windows 事件記錄檔)、執行中程序、電腦名稱、IP 位址、已登入的使用者和租用戶識別碼。 hello Microsoft Monitoring Agent 會讀取事件記錄項目和組態，並將複製 hello 資料 tooyour 工作區中的進行分析。 hello Microsoft Monitoring Agent 也會複製損毀傾印檔案 tooyour 工作區。

如果您使用 hello 免費層的資訊安全中心，您可以關閉 hello 安全性原則中的資料收集停用資料收集，從虛擬機器。 停用資料收集會限制 VM 的安全性評估。 詳細資訊，請參閱 toolearn[停用資料收集](#disabling-data-collection)。 即使已停用資料集合，仍然會啟用 VM 磁碟快照集和構件集合。 需要訂閱 hello 標準層的資訊安全中心上的資料收集。

> [!NOTE]
> 深入了解資訊安全中心的免費和標準[定價層](security-center-pricing.md)。
>
>

## <a name="implement-hello-recommendation"></a>實作 hello 建議

> [!NOTE]
> 本文件介紹 hello 服務使用的範例部署。 本文件不是一份逐步解說指南。
>
>

1. 在 hello**建議**刀鋒視窗中，選取**啟用訂用帳戶的資料收集**。  這會開啟 hello**開啟資料收集**刀鋒視窗。
   ![建議刀鋒視窗][2]
2. 在 hello**開啟資料收集**刀鋒視窗中，選取您的訂用帳戶。 hello**安全性原則**該訂用帳戶 刀鋒視窗隨即開啟。
3. 在 hello**安全性原則**刀鋒視窗中，選取**上**下**資料收集**tooautomatically 收集記錄檔。 開啟所有目前和新的資料集合會佈建 hello 上監視功能延伸模組支援 hello 訂用帳戶中的 Vm。
4. 選取 [ **儲存**]。
5. 選取 [確定] 。

## <a name="disabling-data-collection"></a>停用資料收集
如果您使用 hello 免費層的資訊安全中心，您可以關閉 hello 安全性原則中的資料收集停用在任何時間從虛擬機器的資料收集。 需要訂閱 hello 標準層的資訊安全中心上的資料收集。

1. 傳回 toohello**資訊安全中心**刀鋒視窗，然後選取 hello**原則**磚。 這會開啟 hello**安全性原則定義每個訂閱的原則**刀鋒視窗。
   ![選取 hello 原則磚][5]
2. 在 hello**安全性原則定義每個訂閱的原則**刀鋒視窗中，選取 hello 訂用帳戶，您會希望 toodisable 資料收集。
3. hello**安全性原則**該訂用帳戶 刀鋒視窗隨即開啟。  選取 [資料收集] 底下的 [關閉]。
4. 選取**儲存**hello 頂端功能區中。

## <a name="next-steps"></a>後續步驟
本文章向您說明如何 tooimplement 會 hello 資訊安全中心建議"啟用資料收集。 」 toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)-了解如何 toomanage 和回應 toosecurity 警示。
* [監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
- [Azure 資訊安全中心資料安全性](security-center-data-security.md) - 了解資訊安全中心如何管理及保護其中的資料。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-取得最新 Azure 安全性消息 hello 和資訊。

<!--Image references-->
[2]: ./media/security-center-enable-data-collection/recommendations.png
[3]: ./media/security-center-enable-data-collection/data-collection.png
[4]: ./media/security-center-enable-data-collection/storage-account.png
[5]: ./media/security-center-enable-data-collection/policy.png
[6]: ./media/security-center-enable-data-collection/disable-data-collection.png
