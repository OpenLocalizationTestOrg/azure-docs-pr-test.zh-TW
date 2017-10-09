---
title: "aaaEnable Azure 資訊安全中心中的透明資料加密 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議事項 * * 啟用透明資料加密 * *。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a>在 Azure 資訊安全中心啟用透明資料加密
如果尚未啟用 TDE，Azure 資訊安全中心將建議您在 SQL Database 上啟用透明資料加密 (TDE)。 TDE 會保護資料，並協助您符合法規遵循需求加密資料庫、 相關聯的備份以及交易記錄檔，在其餘部分，而不需要變更 tooyour 應用程式。 toolearn 更看到[Azure SQL Database 的透明資料加密](https://msdn.microsoft.com/library/dn948096)。

這項建議適用於 toohello; 僅限 Azure SQL 服務不包含 SQL 虛擬機器上執行。

> [!NOTE]
> 本文件介紹 hello 服務使用的範例部署。  這不是逐步指南。
>
>

## <a name="implement-hello-recommendation"></a>實作 hello 建議
1. 在 hello**建議**刀鋒視窗中，選取**啟用透明資料加密**。
   ![啟用透明資料加密][1]
2. 這會開啟 hello **SQL 資料庫上啟用透明資料加密**刀鋒視窗。 選取上的 SQL 資料庫 tooenable TDE。
   ![選取上的 SQL DB tooenable TDE][2]
3. 在 [hello**透明資料加密**刀鋒視窗中，選取**ON**下資料加密，然後選取**儲存**hello hello] 刀鋒視窗的頂端功能區中。
   ![開啟 TDE][3]

   一旦啟用了 TDE hello 選取 SQL 資料庫 hello**加密狀態**也會變更**加密**。    

   ![加密狀態][4]

## <a name="see-also"></a>另請參閱
本文章向您說明如何 tooimplement 會 hello 資訊安全中心建議 「 啟用透明資料加密 」。 toolearn 深入了解 SQL TDE，請參閱 hello 下列資訊：

* [Azure SQL Database 的透明資料加密](https://msdn.microsoft.com/library/dn948096)
* [開始使用透明資料加密 (TDE)](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。
* [監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-取得最新 Azure 安全性消息 hello 和資訊。

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
