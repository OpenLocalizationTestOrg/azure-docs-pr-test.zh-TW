---
title: "aaaAdmins 管理使用者和裝置的 Azure MFA |Microsoft 文件"
description: "這說明如何 toochange 使用者設定，例如強制 hello 使用者 toodo hello 證明程序一次。"
documentationcenter: 
services: multi-factor-authentication
author: kgremban
manager: femila
ms.assetid: aac3b922-7cc1-428c-9044-273579aa7b5a
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8c35435e4f6504014d9a4f6f1b837639c3b53481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-user-settings-with-azure-multi-factor-authentication-in-hello-cloud"></a>管理與 hello 雲端中的 Azure Multi-factor Authentication 使用者設定
身為管理員，您可以管理下列使用者和裝置設定的 hello:

* 一次需要使用者 tooprovide 連絡方法
* 刪除應用程式密碼
* 要求在所有受信任的裝置上使用 MFA 

## <a name="require-users-tooprovide-contact-methods-again"></a>一次需要使用者 tooprovide 連絡方法
這項設定會強制 hello 使用者 toocomplete hello 註冊程序一次。 非瀏覽器應用程式可以繼續 toowork 如果 hello 使用者為其具有應用程式密碼。  您可以刪除 hello 使用者應用程式密碼也選取**刪除選取的 hello 使用者所產生的所有現有應用程式密碼**。

### <a name="how-toorequire-users-tooprovide-contact-methods-again"></a>如何 toorequire 使用者 tooprovide 的連絡方法一次
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 左側選取**Azure Active Directory** > **使用者和群組** > **所有使用者**。
3. 選取 [多重要素驗證]。 hello multi-factor authentication 頁面隨即開啟。 
4. 請檢查 hello 方塊下一步 toohello 使用者或使用者，您會希望 toomanage。 快速步驟選項的清單會出現在右邊的 hello。 
5. 選取 [管理使用者設定]。
6. 核取方塊 hello**要求選取的使用者再次 tooprovide 連絡方法**。
   ![提供連絡方法](./media/multi-factor-authentication-manage-users-and-devices/reproofup.png)
7. 按一下 [儲存] 。
8. 按一下 [關閉]。

## <a name="delete-users-existing-app-passwords"></a>刪除使用者現有的應用程式密碼
這項設定會刪除所有使用者建立的 hello 應用程式密碼。 與這些應用程式密碼相關的非瀏覽器應用程式會停止運作，直到建立新應用程式密碼為止。

### <a name="how-toodelete-users-existing-app-passwords"></a>如何 toodelete 使用者現有的應用程式密碼
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 左側選取**Azure Active Directory** > **使用者和群組** > **所有使用者**。
3. 選取 [多重要素驗證]。 hello multi-factor authentication 頁面隨即開啟。 
6. 請檢查 hello 方塊下一步 toohello 使用者或使用者，您會希望 toomanage。 快速步驟選項的清單會出現在右邊的 hello。 
7. 選取 [管理使用者設定]。
8. 核取方塊 hello**刪除選取的 hello 使用者所產生的所有現有應用程式密碼**。
   ![刪除應用程式密碼](./media/multi-factor-authentication-manage-users-and-devices/deleteapppasswords.png)
9. 按一下 [儲存] 。
10. 按一下 [關閉]。

## <a name="restore-mfa-on-all-remembered-devices-for-a-user"></a>在使用者已記住的所有裝置上還原 MFA
其中一個 hello 可設定功能的 Azure Multi-factor Authentication Server 會為使用者提供做為受信任的 hello 選項 toomark 裝置。 如需詳細資訊，請參閱[設定 Azure Multi-Factor Authentication 設定](multi-factor-authentication-whats-next.md#remember-multi-factor-authentication-for-devices-that-users-trust)。

使用者可以在其一般的裝置上設定天數內選擇退出雙步驟驗證。 如果帳戶遭到洩露時或遺失的受信任的裝置，您需要 toobe 無法 tooremove hello 信任狀態，而且需要雙步驟驗證一次。

hello**所有記住的裝置上還原多重要素驗證**設定表示該 hello 使用者下次登入時，不論它們是否選擇 toomark 時將會挑戰 tooperform 雙步驟驗證 hello 其以受信任的裝置。 

### <a name="how-toorestore-mfa-on-all-suspended-devices-for-a-user"></a>如何在使用者的所有已暫停的裝置上的 toorestore MFA
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 左側選取**Azure Active Directory** > **使用者和群組** > **所有使用者**。
3. 選取 [多重要素驗證]。 hello multi-factor authentication 頁面隨即開啟。 
6. 請檢查 hello 方塊下一步 toohello 使用者或使用者，您會希望 toomanage。 快速步驟選項的清單會出現在右邊的 hello。 
7. 選取 [管理使用者設定]。
8. 核取方塊 hello**所有記住的裝置上還原多重要素驗證**
   ![刪除應用程式密碼](./media/multi-factor-authentication-manage-users-and-devices/rememberdevices.png)
9. 按一下 [儲存] 。
10. 按一下 [關閉]。

## <a name="next-steps"></a>後續步驟

- 取得有關的詳細資訊太[設定 Azure Multi-factor Authentication 設定](multi-factor-authentication-whats-next.md)

- 如果您的使用者需要協助時，會將它們向指出 hello[進行兩步驟驗證的使用者指南](./end-user/multi-factor-authentication-end-user.md)
