---
title: "Office 365 使用者帳戶的 aaaHow toouse Azure RemoteApp |Microsoft 文件"
description: "深入了解如何與我的 Office 365 使用者帳戶的 Azure RemoteApp toouse"
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: aba70fd3-60b0-4b44-9321-1ab18760ccd5
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d2dbed2a6838adf9bb0f7508eb7dcecb0a74a62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-remoteapp-with-office-365-user-accounts"></a>如何使用 Office 365 使用者帳戶的 Azure RemoteApp toouse
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

如果您有 Office 365 訂閱，您有 Azure Active Directory 儲存使用者名稱和密碼使用 tooaccess Office 365 服務。 比方說，當您的使用者啟用 Office 365 ProPlus 在驗證對 Azure AD toocheck 授權。 大部分的客戶會像 toouse hello 相同目錄與 Azure RemoteApp。

如果您正在部署 Azure RemoteApp，您最有可能會使用與不同 Azure AD 相關聯的 Azure 訂用帳戶。 在排序 toouse Office 365 目錄，您將需要 toomove hello 至該目錄的 Azure 訂用帳戶。

如需如何資訊 toodeploy Office 365 用戶端應用程式，請參閱[如何 toouse 您 Office 365 訂用帳戶與 Azure RemoteApp 一起](remoteapp-officesubscription.md)。

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a>階段 1：註冊免費的 Office 365 Azure Active Directory 訂用帳戶
如果您使用 hello Azure 傳統入口網站，使用中的 hello 步驟[註冊免費的 Azure Active Directory 訂閱](https://technet.microsoft.com/library/dn832618.aspx)tooget 系統管理存取權 tooyour Azure AD 透過 hello Azure 管理入口網站。 做為此程序的 hello 結果您也應該能夠 toolog 到 hello Azure 入口網站並請參閱您的目錄那里 – 此時不會看到更因為 hello 您 Azure RemoteApp 搭配使用的完整的 Azure 訂用帳戶是在不同的目錄。

記住 hello 名稱和您在此步驟中建立的 hello 系統管理員帳戶的密碼 – 第 2 階段會需要它們。

如果您使用 hello Azure 入口網站，請參閱[如何 tooregister 並啟用免費的 Azure Active Directory 使用 Office 365 入口網站](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/)。

## <a name="phase-2-change-hello-azure-ad-associated-with-your-azure-subscription"></a>階段 2： 變更 hello Azure AD 與 Azure 訂用帳戶關聯。
我們 toochange 您 Azure 訂用帳戶從其目前的目錄到我們與工作階段 1 中的 hello Office 365 目錄。

請依照下列所述的 hello 指示[Azure RemoteApp 中的變更 hello Azure Active Directory 租用戶](remoteapp-changetenant.md)。 請特別注意 toohello 下列步驟：

* 步驟 1：如果您已在此訂用帳戶中部署 Azure RemoteApp (ARA)，在嘗試執行任何動作之前，請先確定您會從任何 ARA 集合中移除所有的 Azure AD 使用者帳戶。 或者，您可以考慮刪除任何現有的集合。
* 步驟 2：這是一個重要的步驟。 您需要 toouse Microsoft 帳戶 (例如@outlook.com) 做為服務管理員 hello 訂用帳戶; 這是因為我們不能有任何使用者帳戶，從 hello 現有 Azure AD 附加 toohello 訂用帳戶 – 如果我們這樣做，我們將不會無法 toomove 它 tooa不同的 Azure AD。
* 步驟 #4： 加入時的現有目錄，hello 系統會要求您使用 hello 系統管理員帳戶 toosign 該目錄。 請確定 toouse hello 系統管理員帳戶，從第 1 階段。
* 步驟 5： 變更 hello 訂用帳戶 tooyour Office 365 directory hello 父目錄。 hello 最後的結果是，在 設定-> 您的訂閱列出 hello Office 365 目錄的訂用帳戶。 
  ![變更 hello 訂閱 hello 父目錄](./media/remoteapp-o365user/settings.png)

此時您 Azure RemoteApp 訂用帳戶都與您 Office 365 Azure AD。您可以使用 hello 現有 Office 365 使用者帳戶與 Azure RemoteApp 一起 ！

