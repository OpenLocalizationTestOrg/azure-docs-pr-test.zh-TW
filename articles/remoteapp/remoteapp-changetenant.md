---
title: "在 Azure RemoteApp aaaChange hello Azure Active Directory 租用戶 |Microsoft 文件"
description: "了解 toochange hello Azure Active Directory 租用戶與 Azure RemoteApp 的相關聯"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 20faf169-6e48-428a-8bdd-f231daff19fa
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d0928b099b7fcfb3ab16077e295d7aaf519c3653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-azure-active-directory-tenant-in-azure-remoteapp"></a>變更 Azure RemoteApp 中的 hello Azure Active Directory 租用戶
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

Azure RemoteApp 使用 Azure Active Directory (Azure AD) tooallow 使用者存取權。 您可以使用 Azure RemoteApp 中的 hello 只有 Azure AD 租用戶為 hello 與 hello Azure 訂用帳戶相關聯。 您可以檢視相關聯的 hello 訂用帳戶上 hello**設定**hello 入口網站頁面中的。 查看 hello**目錄**hello 上的資料行**訂閱** 索引標籤。

> [!NOTE]
> 此變更 toosucceed，如先移除 hello 現有 Azure Active Directory 租用戶中所有的 Azure RemoteApp 集合的所有使用者。 toodo 這個，請移 toohello Azure 入口網站中，移 toohello **Azure RemoteApp**索引標籤上，開啟每個 Azure RemoteApp 集合。 移 toohello**使用者**索引標籤，並移除屬於 tooyour 目前的 Azure Active Directory 租用戶的使用者。 針對所有現有 Azure RemoteApp 集合重複進行。 不這麼做，就能 toocreate 或修補程式集合。
> 
> 

如果您想 toouse 不同的租用戶時，使用這些步驟 toochange hello 關聯與您的訂用帳戶：

1. 在 hello 入口網站移除任何 Azure AD 使用者 toowhich 您已獲得存取 tooAzure RemoteApp 集合。 (請參閱上述步驟的 hello 注意事項 toodo 這。)
2. 設定 Microsoft 帳戶 （先前稱為 Live ID） hello 服務系統管理員身分。 （不知道您已經是否 hello 服務系統管理員？ 您可以按一下 [設定] -> [系統管理員] 來查看。)接下來，以下是變更的方法：
   
   1. 按一下 hello 右上角中的 hello 使用者，然後按一下**檢視我的帳單**。
   2. 按一下 hello 訂用帳戶。 然後，在 hello 新頁面上，向下捲動並按一下**編輯訂用帳戶詳細資料**hello 右中。 （hello 中間右下方，如果一種可協助您找到它。）
   3. 輸入 hello Microsoft 帳戶 hello 使用者應該 hello 服務系統管理員。
3. 現在，登出 hello 入口網站，然後傳回以 hello hello 先前步驟中所指定的 Microsoft 帳戶登入。
4. 依序按一下 [新增] > [應用程式服務] > [Active Directory] > [目錄] > [自訂建立]。
5. 在 [目錄] 下方，選擇 [使用現有的目錄]。 我們會 toohave toosign 超出 hello 入口網站現在，您可以選擇**我已準備好立即登出的 toobe**。
6. 簽署回 hello 入口網站的 hello 目錄全域管理員為您想要 tooadd。 (如果您還不是全域管理員，您將會經歷一回的登入然後登出。)
7. 如果您想要 toouse 您現有的 AD 租用戶與您訂用帳戶登入後會詢問您。 按一下 繼續，然後按一下立即登出。
8. 同樣地，登入，並返回太**設定]-> [訂閱**。 選取您的訂用帳戶，然後按一下編輯目錄 。 選取您想 toouse hello Azure AD 租用戶。

您現在可以使用 Azure RemoteApp 中的 hello 新的 Azure AD 租用戶 toocontrol 存取 toohello Azure 訂用帳戶和 tooconfigure 使用者存取權。

