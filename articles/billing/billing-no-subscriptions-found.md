---
title: "aaaNo 訂用帳戶中找到的錯誤時再試一次 toosign tooAzure 入口網站或 Azure 帳戶中心 |Microsoft 文件"
description: "提供 hello 方案中沒有訂用帳戶會找到錯誤，就會發生問題時登入 tooAzure 入口網站或 Azure 帳戶中心。"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a>在 Azure 入口網站或 Azure 帳戶中心內，未於訂用帳戶中找到任何錯誤
您可能會收到 「 找不到訂閱 」 錯誤訊息，當您嘗試在 toohello toosign [Azure 入口網站](https://portal.azure.com/)或 hello [Azure 帳戶中心](https://account.windowsazure.com/Subscriptions)。 本文會提供此問題的解決方案。

## <a name="symptom"></a>徵狀

當您嘗試在 toohello toosign [Azure 入口網站](https://portal.azure.com/)或 hello [Azure 帳戶中心](https://account.windowsazure.com/Subscriptions)，您會收到下列錯誤訊息的 hello: 「 找不到訂閱 」。

## <a name="cause"></a>原因

如果您的帳戶沒有足夠的權限，就會發生這個問題。 

## <a name="solution"></a>方案

請確定您在 hello 正確的系統管理員身分登入。 帳戶系統管理員可以存取 hello 帳戶中心。 服務系統管理員 (SA) 和共同管理員 (CA) 的存取權限只有 toohello Azure 入口網站或 hello Azure 傳統入口網站。

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a>案例 1: Hello 中收到錯誤訊息[Azure 入口網站](https://portal.azure.com)

toofix 此問題：

* 請確定該 hello 正確依序按一下您的帳戶在 hello 右上方選取 Azure 目錄。

  ![選取 hello 目錄 hello hello Azure 入口網站的右上方](./media/billing-no-subscriptions-found/directory-switch.png)

* 如果 hello 右 Azure 選取目錄，但是您仍然收到 hello 錯誤訊息，[將您的帳戶作為擁有者加入](billing-add-change-azure-subscription-administrator.md)。

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a>案例 2: Hello 中收到錯誤訊息[Azure 帳戶中心](https://account.windowsazure.com/Subscriptions)

檢查您所使用的 hello 帳戶是否 hello 帳戶系統管理員。 tooverify 人員 hello 帳戶系統管理員，請遵循下列步驟：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，選取 **訂用帳戶**。
3. 選取您想 toocheck，，然後選取 hello 訂閱**設定**。
4. 選取 [屬性] 。 hello hello 訂用帳戶的帳戶管理員會顯示在 hello**帳戶管理員**方塊。

## <a name="need-help-contact-support"></a>需要協助嗎？ 請連絡支援人員。
如果您仍需要協助，[連絡支援人員](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409)tooget 快速解決您的問題。 
