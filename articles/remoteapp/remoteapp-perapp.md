---
title: "aaaPublish 應用程式 tooindividual 使用者的 Azure RemoteApp 集合 （預覽） |Microsoft 文件"
description: "了解如何發行應用程式 tooindividual 使用者，而不是根據 Azure RemoteApp 中的群組，而定。"
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a>發行的 Azure RemoteApp 集合 （預覽） 中的應用程式 tooindividual 使用者
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

這篇文章說明如何在 Azure RemoteApp 集合 toopublish 應用程式 tooindividual 使用者。 這是在 Azure RemoteApp 中，目前在私人預覽和可用的唯一 tooselect 早期採用者供評估之用的新功能。

Azure RemoteApp 原本啟用發行應用程式的方式只有一種： hello 系統管理員會將應用程式從 hello 映像的發佈並可看見 tooall hello 集合中的使用者。

常見的案例是的 tooinclude 許多應用程式在單一的映像，部署一個集合的順序 tooreduce 管理成本。 有時候，並非所有應用程式都是相關 tooall 使用者 – 系統管理員喜歡 toopublish tooindividual 應用程式的使用者，讓他們無法看到其摘要的應用程式中不必要的應用程式。

現在 Azure RemoteApp 已提供這項功能，但目前為受限制的預覽功能。 Hello 新功能的簡短摘要如下：

1. 集合可以設定成兩種模式之一：
   
   * hello 原始集合模式中，集合中的所有使用者可以都查看所有已發行應用程式的位置。 這是 hello 預設模式。
   * hello 新應用程式模式中，使用者只看到應用程式已被明確指派 toothem
2. 在 hello 時刻 hello 應用程式模式下才可以啟用使用 Azure RemoteApp PowerShell cmdlet。
   
   * 當設定 tooapplication 模式 hello 集合中的使用者指派無法透過 hello Azure 入口網站進行管理。 使用者指派具有 toobe 透過 PowerShell cmdlet 來管理。
3. 使用者只會看到 hello 應用程式直接發行 toothem。 不過，它還是可能對使用者 toolaunch hello hello 映像上可用的其他應用程式藉由直接在 hello 作業系統中存取它們。
   
   * 這項功能不會提供安全的應用程式鎖定它只會限制摘要的 hello 應用程式中的可見性。
   * 如果您需要 tooisolate 使用者從應用程式，您必須 toouse 個別集合的。

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a>如何 tooget Azure RemoteApp PowerShell cmdlet
tootry hello 新預覽的功能，您將需要 toouse Azure PowerShell cmdlet。 它是目前不可能 toouse hello Azure Management 入口網站 tooenable hello 新應用程式發行模式。

首先，請確定您擁有 hello [Azure PowerShell 模組](/powershell/azure/overview)安裝。

然後啟動在系統管理員模式下，執行下列 cmdlet 的 hello hello PowerShell 主控台：

        Add-AzureAccount

它會提示您輸入 Azure 使用者名稱和密碼。 一旦登入，您將無法 toorun Azure RemoteApp cmdlet 針對您的 Azure 訂用帳戶。

## <a name="how-toocheck-which-mode-a-collection-is-in"></a>如何 toocheck 集合是在哪個模式下
執行下列 cmdlet 的 hello:

        Get-AzureRemoteAppCollection <collectionName>

![核取 hello 收集模式](./media/remoteapp-perapp/araacllelvel.png)

hello AclLevel 屬性可以有下列值的 hello:

* 集合： hello 原始發行模式。 所有使用者都能看到所有已發佈的應用程式。
* 應用程式： hello 新發行的模式。 使用者會看到只有 hello 應用程式直接發佈 toothem。

## <a name="how-tooswitch-tooapplication-publishing-mode"></a>如何 tooswitch tooapplication 發佈模式
執行下列 cmdlet 的 hello:

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

應用程式的發行狀態將會保留： 一開始的所有使用者會都看到所有 hello 原始發行的應用程式。

## <a name="how-toolist-users-who-can-see-a-specific-application"></a>如何 toolist，使用者可以看到特定的應用程式
執行下列 cmdlet 的 hello:

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

這樣就會列出所有使用者都可以看到 hello 應用程式。

注意： 您可以看見 hello 應用程式的別名 （在上述的 hello 語法中稱為 「 應用程式的別名"） 執行 Get AzureRemoteAppProgram CollectionName <collectionName>。

## <a name="how-tooassign-an-application-tooa-user"></a>如何 tooassign 應用程式 tooa 使用者
執行下列 cmdlet 的 hello:

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

hello 使用者現在會看見 hello hello Azure RemoteApp 用戶端中的應用程式，且將無法 tooconnect tooit。

## <a name="how-tooremove-an-application-from-a-user"></a>如何 tooremove 使用者從應用程式
執行下列 cmdlet 的 hello:

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a>提供意見反應
歡迎您提供有關這項預覽功能的意見反應和建議。 請填寫 hello[調查](http://www.instant.ly/s/FDdrb)toolet 我們知道您的想法。

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a>沒機會 tootry hello 預覽功能嗎？
如果您未參與 hello 預覽尚未，請使用這項[調查](http://www.instant.ly/s/AY83p)toorequest 存取。

