---
title: "Azure AD Connect 同步： 變更 hello Azure AD 連接同步處理服務帳戶 |Microsoft 文件"
description: "此主題說明 hello 加密金鑰和方式 tooabandon hello 密碼之後變更。"
services: active-directory
keywords: "Azure AD 同步處理服務帳戶, 密碼"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 11948ac4662f722e4f684ef6c9b9ccdc6387e60f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-azure-ad-connect-sync-service-account-password"></a>變更 hello Azure AD Connect 同步處理服務帳戶密碼
如果您變更 hello Azure AD Connect 同步處理服務帳戶密碼，hello 同步處理服務之前將無法可以開始正常您已在放棄 hello 加密金鑰並重新初始化 hello Azure AD Connect 同步處理服務帳戶密碼。 

Azure AD Connect，hello 同步處理服務的一部分使用加密金鑰 toostore hello 密碼的 hello AD DS 和 Azure AD 服務帳戶。  這些帳戶會加密，再將它們儲存在 hello 資料庫中。 

hello 加密金鑰用於保護使用[Windows 資料保護 (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx)。 DPAPI 保護 hello 加密金鑰使用 hello **hello Azure AD Connect 同步處理服務帳戶的密碼**。 

如果您需要 toochange hello 服務帳戶密碼，您就可以使用中的 hello 程序[Abandoning hello Azure AD 連接同步處理加密金鑰](#abandoning-the-azure-ad-connect-sync-encryption-key)tooaccomplish 這。  如果您因為任何原因需要 tooabandon hello 加密金鑰，也應該使用這些程序。

##<a name="issues-that-arise-from-changing-hello-password"></a>所發生的變更 hello 密碼問題
有兩件事需要 toobe 完成時變更 hello 服務帳戶密碼。

首先，您必須在 hello Windows 服務控制管理員 toochange hello 密碼。  在此問題獲得解決之前，您會看到下列錯誤︰


- 如果您嘗試 toostart hello 同步處理服務 Windows 服務控制管理員 」 中，您會收到 hello 錯誤 「**Windows 無法啟動本機電腦上的 hello Microsoft Azure AD 同步服務**"。 **錯誤 1069年: hello 服務未啟動到期 tooa 登入失敗。**"
- 在 Windows 事件檢視器，hello 系統事件記錄檔包含與錯誤**事件識別碼 7038**和訊息 「**hello ADSync 服務是在無法 toolog 如同 hello 目前已設定密碼到期，toohello 下列錯誤：hello 使用者名稱或密碼不正確。**"

第二，在特定情況下更新 hello 密碼時，如果 hello 同步處理服務無法再擷取 hello 透過 DPAPI 的加密金鑰。 沒有 hello 加密金鑰，同步處理服務無法解密，或從 hello 密碼需要的 toosynchronize hello 內部部署 AD 和 Azure AD。
您會看到如下錯誤︰

- 在 「 Windows 服務控制管理員 」 中，如果您試過 toostart hello 同步處理服務，它無法擷取 hello 加密金鑰，其錯誤而失敗 」 * * Windows 無法啟動本機電腦上的 Microsoft Azure AD Sync hello。 如需詳細資訊，檢閱 hello 系統事件記錄檔。 如果這是非 Microsoft 服務，請連絡 hello 服務廠商，並 tooservice 特有的錯誤程式碼，請參閱 * *-21451857952 * * *。 」
- 在 Windows 事件檢視器，hello 應用程式事件記錄檔包含與錯誤**事件識別碼 6028**和錯誤訊息*"**hello 伺服器加密金鑰無法存取。**"*

tooensure，您不會收到這些錯誤，請依照下列中的 hello 程序[Abandoning hello Azure AD 連接同步處理加密金鑰](#abandoning-the-azure-ad-connect-sync-encryption-key)變更 hello 密碼時。
 
## <a name="abandoning-hello-azure-ad-connect-sync-encryption-key"></a>放棄 hello Azure AD 連接同步處理加密金鑰
>[!IMPORTANT]
>hello 下列程序僅適用於 tooAzure AD Connect 組建 1.1.443.0 或更舊版本。

使用下列程序 tooabandon hello 加密金鑰的 hello。

### <a name="what-toodo-if-you-need-tooabandon-hello-encryption-key"></a>如果您需要 tooabandon hello 加密金鑰哪些 toodo

如果您需要 tooabandon hello 加密金鑰，請使用下列程序 tooaccomplish hello 這項。

1. [放棄 hello 現有的加密金鑰](#abandon-the-existing-encryption-key)

2. [提供 hello 的 hello AD DS 帳戶的密碼](#provide-the-password-of-the-ad-ds-account)

3. [重新初始化 hello hello Azure AD 同步處理帳戶密碼](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [啟動 hello 同步處理服務](#start-the-synchronization-service)

#### <a name="abandon-hello-existing-encryption-key"></a>放棄 hello 現有的加密金鑰
因此，可以建立該新的加密金鑰，請放棄 hello 現有的加密金鑰：

1. 登入 tooyour Azure AD 連線伺服器系統管理員身分。

2. 啟動新的 PowerShell 工作階段。

3. 瀏覽 toofolder:`$env:Program Files\Microsoft Azure AD Sync\bin\`

4. 執行 hello 命令：`./miiskmu.exe /a`

![Azure AD Connect 同步處理加密金鑰公用程式](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-hello-password-of-hello-ad-ds-account"></a>提供 hello 的 hello AD DS 帳戶的密碼
無法再解密 hello hello 資料庫內儲存的現有密碼，您必須 tooprovide hello 與 hello 的 hello AD DS 帳戶的密碼同步處理服務。 hello 同步處理服務會加密 hello 使用 hello 新的加密金鑰的密碼：

1. 啟動 hello Synchronization Service Manager （開始 → 同步處理服務）。
</br>![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  
2. 移 toohello**連接器** 索引標籤。
3. 選取 hello **AD 連接器**對應 tooyour 在內部部署 AD。 如果您有多個 AD 連接器時，重複下列步驟，為每個 hello。
4. 選取 [動作] 下方的 [屬性]。
5. 在 hello 快顯對話方塊中，選取 **連接 tooActive Directory 樹系**:
6. 輸入 hello hello hello AD DS 帳戶密碼**密碼**文字方塊。 如果您不知道其密碼，您必須設定 tooa 已知值，然後再執行此步驟。
7. 按一下**確定**toosave hello 新密碼] 和 [關閉 hello 快顯對話方塊。
![Azure AD Connect 同步處理加密金鑰公用程式](media/active-directory-aadconnectsync-encryption-key/key6.png)

#### <a name="reinitialize-hello-password-of-hello-azure-ad-sync-account"></a>重新初始化 hello hello Azure AD 同步處理帳戶密碼
您無法直接提供 hello hello Azure AD 服務帳戶 toohello 同步處理服務密碼。 相反地，您需要 toouse hello cmdlet**新增 ADSyncAADServiceAccount** tooreinitialize hello Azure AD 服務帳戶。 hello cmdlet 會重設 hello 帳戶密碼，並使其成為可用 toohello 同步服務：

1. Hello Azure AD Connect 的伺服器上啟動新的 PowerShell 工作階段。
2. 執行 `Add-ADSyncAADServiceAccount` Cmdlet。
3. 在 hello 快顯對話方塊中，提供 Azure AD 租用戶 hello Azure AD 全域管理員認證。
![Azure AD Connect 同步處理加密金鑰公用程式](media/active-directory-aadconnectsync-encryption-key/key7.png)
4. 如果成功，您會看到 hello PowerShell 命令提示字元。

#### <a name="start-hello-synchronization-service"></a>啟動 hello 同步處理服務
既然 hello 同步處理服務都有存取 toohello 加密金鑰，且所有 hello 密碼需要您可以重新啟動 Windows 服務控制管理員 hello hello 服務：


1. 移 tooWindows 服務控制管理員 （開始 → 服務）。
2. 選取 [Microsoft Azure AD 同步處理]，然後按一下 [重新啟動]。

## <a name="next-steps"></a>後續步驟
**概觀主題**

* [Azure AD Connect 同步處理：了解及自訂同步處理](active-directory-aadconnectsync-whatis.md)

* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)
