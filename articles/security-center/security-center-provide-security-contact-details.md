---
title: "aaaProvide 安全性連絡人詳細資料中 Azure 資訊安全中心 |Microsoft 文件"
description: "本文件示範 tooprovide 安全性如何連絡 Azure 資訊安全中心中的詳細資料。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 6c378c9c84c6e4fce70b2541e4cc121018700269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a>在 Azure 資訊安全中心提供安全性連絡人詳細資料
Azure 資訊安全中心會建議您針對您的 Azure 訂用帳戶提供安全性連絡人詳細資料 (如果您還沒有這麼做)。 這項資訊將供 Microsoft toocontact 您如果 hello Microsoft Security Response Center (MSRC) 探索非法或未經授權的合作對象已存取您的客戶資料。 MSRC 執行選取的安全性監視的 hello Azure 網路和基礎結構，並接收來自第三方 threat intelligence 和濫用抱怨。

在 hello 每日第一個警示的而且僅針對高嚴重性警示時傳送電子郵件通知。 電子郵件喜好設定只能針對訂用帳戶原則設定。 在訂用帳戶內的資源群組會繼承這些設定。

> [!NOTE]
> 本文件介紹 hello 服務使用的範例部署。  這不是逐步指南。
>
>

## <a name="implement-hello-recommendation"></a>實作 hello 建議
1. 在 hello**建議**刀鋒視窗中，選取**提供安全性連絡人詳細資料**。
   ![提供安全性連絡人][1]
2. 這會開啟刀鋒視窗中 hello**提供安全性連絡人詳細資料**。 在 選取 hello Azure 訂用帳戶 tooprovide 連絡資訊。
   ![提供安全性連絡人詳細資料][2]
3. 第二個 [提供安全性連絡人詳細資料]  刀鋒視窗隨即開啟。

   * 輸入 hello 安全性連絡人的電子郵件地址或以逗號分隔地址。 沒有任何限制 toohello 數字，您可以輸入的電子郵件地址。
   * 輸入一個安全性連絡人國際電話號碼。
   * tooreceive 有關高嚴重性警示的電子郵件開啟 hello 選項**傳送給我以電子郵件警示的相關**。
   * 在 hello 未來，您可以 hello 選項 toosend 電子郵件通知 toosubscription 擁有者。 此選項目前無法使用。
   * 選取**確定**tooapply hello 安全性連絡資訊 tooyour 訂用帳戶。

## <a name="see-also"></a>另請參閱
toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。
* [監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-取得最新 Azure 安全性消息 hello 和資訊。

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
