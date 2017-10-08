---
title: "aaaManage 存取 tooAzure 計費使用角色 |Microsoft 文件"
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: 5937fac5ffa5ca204eb03a1dcbc5e800b3d5eb74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a>管理 Azure 中使用角色型存取控制的存取 toobilling 資訊

您可以藉由指派一個 hello 下列使用者角色 tooyour 訂用帳戶授與存取您小組的 Azure 帳單資訊 toomembers： 帳戶系統管理員、 服務系統管理員、 共同管理員、 擁有者、 參與者，讀取器和計費的讀取器。 他們必須在 hello 存取 toobilling 資訊[Azure 入口網站](https://portal.azure.com/)，而且可以使用 hello[計費 Api](billing-usage-rate-card-overview.md) tooprogrammatically 取得發票 （一次選擇單元） 和使用方式詳細資料。 如需有關角色授權者及角色功能的詳細資訊，請參閱 [Azure RBAC 中的角色](../active-directory/role-based-access-built-in-roles.md)。

## <a name="opt-in"></a>允許其他使用者 tooaccess 發票

hello 帳戶系統管理員必須選擇使用 hello [Azure 入口網站](https://portal.azure.com/)允許存取 tooinvoices 給其他使用者，以及透過 API。

1. 因為 hello 帳戶系統管理員，選取您的訂閱 hello 從[訂用帳戶 刀鋒視窗](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)Azure 入口網站中。

1. 選取**發票**然後**存取 tooinvoices**。

    ![螢幕擷取畫面顯示如何 toodelegate 存取 tooinvoices](./media/billing-manage-access/AA-optin.png)

1. 開啟**上**hello 存取後面接著儲存變更 hello tooallow 使用者訂用帳戶已設定領域的角色 toodownload 發票中。

    ![螢幕擷取畫面顯示開啟的關閉 toodelegate 存取 tooinvoice](./media/billing-manage-access/AA-optinAllow.png)

選擇允許服務系統管理員、 共同管理員、 擁有者、 參與者，讀取器和計費的讀取器上 hello 訂用帳戶 toodownload PDF 發票 hello Azure 入口網站中。 不過，早於 2016 年 12 月的發票都有可用的唯一 toohello 帳戶系統管理員現在。

hello 帳戶系統管理員也可以設定透過電子郵件傳送 toohave 發票。 詳細資訊，請參閱 toolearn[電子郵件中取得您的發票](billing-download-azure-invoice-daily-usage-date.md)。

## <a name="adding-users-toohello-billing-reader-role"></a>新增使用者 toohello 計費的讀取器角色

hello 計費的讀取器角色都有唯讀存取 toosubscription 帳單資訊在 Azure 入口網站和 Vm 和儲存體帳戶之類的任何存取 tooservices。 指派 hello 計費的讀取器角色 toosomeone 需要存取 toohello 訂用帳戶的計費資訊，但不 hello 能力 toomanage Azure 服務。 此角色適用於組織內只負責執行 Azure 訂用帳戶之財務和成本管理的使用者。

1. 選取您的訂閱 hello 從[訂用帳戶 刀鋒視窗](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)Azure 入口網站中。

1. 選取 存取控制 (IAM)，然後按一下新增。

    ![螢幕擷取畫面顯示 IAM 在 hello 訂用帳戶 刀鋒視窗](./media/billing-manage-access/select-iam.PNG)

1. 選擇**計費的讀取器**在 hello**選取角色**頁面。

    ![螢幕擷取畫面顯示計費 hello 快顯視窗檢視中的讀取器](./media/billing-manage-access/select-roles.PNG)

1. 輸入 hello hello 使用者 tooinvite，然後按一下 電子郵件**確定**toosend hello 邀請。

    ![顯示 tooenter 電子郵件 tooinvite 某人的螢幕擷取畫面](./media/billing-manage-access/add-user.PNG)

1. 請依照指示中的 hello 邀請電子郵件 toolog 當做計費的讀取器。

    ![螢幕擷取畫面，顯示哪些 hello 計費的讀取器可以在 Azure 入口網站中看到](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> hello 計費的讀取器功能處於預覽狀態，並還不支援企業 (EA) 訂用帳戶或非全域的雲端。

## <a name="adding-users-tooother-roles"></a>新增使用者 tooother 角色

具備其他角色 (例如「擁有者」和「參與者」) 的使用者不僅可存取帳單資訊，還可存取 Azure 服務。 toomanage 這些角色，請參閱[hello 訂用帳戶或服務管理的新增或變更 Azure 系統管理員角色](billing-add-change-azure-subscription-administrator.md)。

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a>誰可以存取 hello[帳戶中心](https://account.windowsazure.com)？

Hello 帳戶系統管理員可以登入 toohello 帳戶中心。 hello 帳戶系統管理員是 hello 合法 hello 訂用帳戶擁有者。 根據預設，hello 註冊或人購買 hello Azure 訂用帳戶為 hello 帳戶系統管理員，除非 hello[訂用帳戶擁有權已轉移](billing-subscription-transfer.md)toosomebody 其他。 hello 帳戶系統管理員可以建立訂閱、 取消訂用帳戶、 變更 hello 帳單地址訂用帳戶，以及管理 hello 訂用帳戶的存取原則。

## <a name="need-help-contact-support"></a>需要協助嗎？ 請連絡支援人員。

如果您仍有進一步的問題，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。
