---
title: "aaaAzure Active Directory Connect Health 作業"
description: "本文說明可以在您部署 Azure AD Connect Health 之後執行的其他作業。"
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 86cc3840-60fb-43f9-8b2a-8598a9df5c94
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 1dddcee0bca3150ce08621c045a92a1b3ad9df30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-connect-health-operations"></a>Azure Active Directory Connect Health 作業
本主題描述 hello 各種作業，您可以執行使用 Azure Active Directory (Azure AD) 連線的健全狀況。

## <a name="enable-email-notifications"></a>啟用電子郵件通知
警示會指出您的身分識別基礎結構不是狀況良好時，您可以設定 hello Azure AD Connect Health 服務 toosend 電子郵件通知。 產生警示和解決警示時會發生這種情況。

![Azure AD Connect Health 電子郵件通知設定的螢幕擷取畫面](./media/active-directory-aadconnect-health/email_noti_discover.png)

> [!NOTE]
> 依預設會啟用電子郵件通知。
>
>

### <a name="tooenable-azure-ad-connect-health-email-notifications"></a>tooenable Azure AD Connect Health 電子郵件通知
1. 開啟 hello**警示**刀鋒視窗中，您會想 tooreceive 電子郵件通知的 hello 服務。
2. 在 hello 動作列中，按一下**通知設定**。
3. 在 hello 電子郵件通知交換器中，選取**ON**。
4. 如果您想要所有全域管理員 tooreceive 電子郵件通知，請選取 [hello] 核取方塊。
5. 如果您想在任何其他的電子郵件地址 tooreceive 電子郵件通知，來指定 hello**其他電子郵件收件者**方塊。 這份清單中，從電子郵件地址 tooremove hello 項目上按一下滑鼠右鍵，然後選取**刪除**。
6. toofinalize hello 變更，按一下**儲存**。 只有在您儲存之後，變更才會生效。

## <a name="delete-a-server-or-service-instance"></a>刪除伺服器或服務執行個體

在某些情況下，您可能想 tooremove 從受監視的伺服器。 以下是您的需要 tooknow tooremove hello Azure AD Connect Health 服務中的伺服器。

當您要刪除伺服器時，請注意下列 hello:

* 這個動作會停止從該伺服器收集任何進一步的資料。 此伺服器會從監視服務的 hello 移除。 此動作之後, 您不能 tooview 新警示、 監視或此伺服器的使用方式分析資料。
* 此動作不會解除安裝 hello 健康情況代理程式從您的伺服器。 如果您不解除安裝然後再執行此步驟中的 hello 健康情況代理程式，您可能會看到 hello 伺服器上的錯誤相關的 toohello 健康情況代理程式。
* 此動作不會刪除 hello 從這部伺服器已收集的資料。 根據 hello Azure 資料保留原則會刪除該資料。
* 之後執行此動作，如果您想要監視 toostart hello 相同的伺服器同樣地，您必須解除安裝，並在此伺服器上重新安裝 hello 健康情況代理程式。

### <a name="toodelete-a-server-from-hello-azure-ad-connect-health-service"></a>toodelete hello Azure AD Connect Health 服務中的伺服器
適用於 Active Directory 同盟服務 (AD FS) 和 Azure AD Connect (Sync) 的 Azure AD Connect Health：

1. 開啟 hello**伺服器**刀鋒視窗中的 hello**伺服器清單**選取 hello 伺服器名稱 toobe 刀鋒視窗中移除。
2. 在 hello**伺服器**刀鋒視窗中的，在 hello 動作列中，按一下**刪除**。
3. 確認 hello 確認方塊中輸入 hello 伺服器名稱。
4. 按一下 [刪除] 。

Azure AD Connect Health for Azure Active Directory Domain Services：

1. 開啟 hello**網域控制站**儀表板。
2. 選取 hello 網域控制站 toobe 移除。
3. 在 hello 動作列中，按一下**選取 刪除**。
4. 確認 hello 動作 toodelete hello 伺服器。
5. 按一下 [刪除] 。

### <a name="delete-a-service-instance-from-azure-ad-connect-health-service"></a>從 Azure AD Connect Health 服務刪除服務執行個體
在某些情況下，您可能想 tooremove 服務執行個體。 以下是您需要 tooknow tooremove 服務執行個體從 hello Azure AD Connect Health 服務。

當您要刪除的服務執行個體時，請注意下列 hello:

* 這個動作會移除從監視服務的 hello hello 目前服務執行個體。
* 此動作不解除安裝或移除任何受監視的此服務執行個體一部分 hello 伺服器 hello 健康情況代理程式。 如果您不解除安裝然後再執行此步驟中的 hello 健康情況代理程式，您可能會看到錯誤相關的 toohello 健康情況代理程式在 hello 伺服器上。
* 此服務執行個體的所有資料會根據 hello Azure 資料保留原則都刪除。
* 執行此動作之後，如果您想 toostart 監視 hello 服務時，解除安裝，並在 hello 的所有伺服器上重新安裝 hello 健康情況代理程式。 執行此動作之後，如果您想要監視相同的伺服器同樣地，解除安裝、 重新安裝，然後將註冊的 hello toostart 會 hello 健康情況代理程式在該伺服器上。

#### <a name="toodelete-a-service-instance-from-hello-azure-ad-connect-health-service"></a>toodelete 從 hello Azure AD Connect Health 服務的服務執行個體
1. 開啟 hello**服務**刀鋒視窗中的 hello**服務清單**刀鋒視窗中的選取您想 tooremove hello service 識別碼 （陣列名稱）。
2. 在 hello**伺服器**刀鋒視窗中的，在 hello 動作列中，按一下**刪除**。
3. 確認 hello 確認方塊中輸入 hello 服務名稱 (例如： sts.contoso.com)。
4. 按一下 [刪除] 。
   <br><br>

[//]: # (Start of RBAC section)
## <a name="manage-access-with-role-based-access-control"></a>使用角色型存取控制來管理存取
[角色型存取控制 (RBAC)](../role-based-access-control-configure.md) Azure AD Connect Health 提供存取 toousers 和全域系統管理員以外的群組。 RBAC 角色 toohello 適合使用者和群組，並提供一個機制，在您的目錄 toolimit hello 全域管理員。

### <a name="roles"></a>角色
Azure AD Connect Health 支援 hello 下列內建的角色：

| 角色 | 權限 |
| --- | --- |
| 擁有者 |擁有者可以使用*管理存取*（例如，指派角色 tooa 使用者或群組），*檢視的所有資訊*（例如，都檢視警示） 從 hello 入口網站，和*變更設定*(例如，電子郵件通知） 在 Azure AD Connect Health。 <br>預設會指派此角色給 Azure AD 全域管理員，而且無法變更。 |
| 參與者 |參與者可以*檢視的所有資訊*（例如，都檢視警示） 從 hello 入口網站，和*變更設定*（例如，電子郵件通知） 在 Azure AD Connect Health。 |
| 讀取者 |讀取器可以*檢視的所有資訊*（例如，都檢視警示） 從 Azure AD Connect Health 內 hello 入口網站。 |

所有其他的角色 （例如使用者存取系統管理員或 DevTest 實驗室使用者） 有 Azure AD Connect Health，在不影響 tooaccess，即使 hello 入口網站體驗中的 hello 角色可用。

### <a name="access-scope"></a>存取範圍
Azure AD Connect Health 支援在兩個層級上管理存取：

* **所有服務執行個體**： 這是建議的路徑，在大部分情況下的 hello。 它可以在 Azure AD Connect Health 所監視的所有角色類型上，控制所有服務執行個體的存取 (例如 AD FS 伺服陣列)。
* **服務執行個體**： 在某些情況下，您可能需要根據角色型別或由服務執行個體的 toosegregate 存取。 在此情況下，您可以管理 hello 服務執行個體層級的存取。  

權限授與使用者是否有權存取在 hello 目錄或服務執行個體層級。

### <a name="allow-users-or-groups-access-tooazure-ad-connect-health"></a>允許使用者或群組存取 tooAzure AD Connect Health
hello 下列步驟示範如何存取 tooallow。
#### <a name="step-1-select-hello-appropriate-access-scope"></a>步驟 1： 選取 hello 適當的存取範圍
使用者存取在 hello tooallow*所有服務執行個體*Azure AD Connect Health，開啟 hello Azure AD Connect Health 中的 [主要] 刀鋒視窗中的層級。<br>

#### <a name="step-2-add-users-and-groups-and-assign-roles"></a>步驟 2：新增使用者和群組及指派角色
1. 從 hello**設定**區段中，按一下**使用者**。<br>
   ![Azure AD Connect Health RBAC 主要刀鋒視窗的螢幕擷取畫面，已醒目提示 [使用者]](./media/active-directory-aadconnect-health/RBAC_main_blade.png)
2. 選取 [新增] 。
3. 在 hello**選取角色** 窗格中，選取一個角色 (例如，**擁有者**)。<br>
   ![Azure AD Connect Health RBAC [使用者] 視窗的螢幕擷取畫面](./media/active-directory-aadconnect-health/RBAC_add.png)
4. 輸入 hello 名稱或識別碼 hello 目標使用者或群組。 您可以選取一個或多個使用者或群組在 hello 相同的時間。 按一下 [選取] 。
   ![Azure AD Connect Health RBAC [使用者] 視窗的螢幕擷取畫面](./media/active-directory-aadconnect-health/RBAC_select_users.png)
5. 選取 [確定] 。<br>
6. Hello 角色指派完成後，hello 使用者和群組會出現在 hello 清單中。<br>
   ![Azure AD Connect Health RBAC [使用者] 視窗的螢幕擷取畫面，已醒目提示新使用者](./media/active-directory-aadconnect-health/RBAC_user_list.png)

現在 hello 列出使用者和群組都可以存取，根據 tootheir 指派角色。

> [!NOTE]
> * 全域管理員一定會有完整存取 tooall hello 作業，但全域系統管理員帳戶不會出現在上述清單中的 hello。
> * Azure AD Connect Health 內不支援 hello 邀請使用者功能。
>
>

#### <a name="step-3-share-hello-blade-location-with-users-or-groups"></a>步驟 3： 共用 hello 刀鋒視窗位置與使用者或群組
1. 指派權限之後，使用者就可以前往[這裡](http://aka.ms/aadconnecthealth)來存取 Azure AD Connect Health。
2. Hello 刀鋒視窗，hello 使用者可以釘選 hello 刀鋒視窗中或它 toohello 儀表板的不同部分。 只要按一下 hello **Pin toodashboard**圖示。<br>
   ![Azure AD Connect Health RBAC 釘選刀鋒視窗的螢幕擷取畫面，已醒目提示釘選圖示](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)

> [!NOTE]
> 具有 hello 讀取者角色指派的使用者不能 tooget Azure AD Connect Health 延伸 hello Azure Marketplace。 hello 使用者所以無法執行 hello 需要 「 建立 」 作業 toodo。 hello 使用者仍然可以取得上述連結會 toohello toohello 刀鋒視窗。 對於後續的使用方式，hello 使用者可以釘選 hello 刀鋒視窗 toohello 儀表板。
>
>

### <a name="remove-users-or-groups"></a>移除使用者或群組
您可以移除使用者或群組加入 tooAzure AD 連線健全狀況 RBAC。 只要以滑鼠右鍵按一下 hello 使用者或群組，然後選取 **移除**。<br>
![Azure AD Connect Health RBAC [使用者] 視窗的螢幕擷取畫面，已醒目提示 [移除]](./media/active-directory-aadconnect-health/RBAC_remove.png)

[//]: # (End of RBAC section)

## <a name="next-steps"></a>後續步驟
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health 代理程式安裝](active-directory-aadconnect-health-agent-install.md)
* [在 AD FS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adfs.md)
* [使用 Azure AD Connect Health 進行同步處理](active-directory-aadconnect-health-sync.md)
* [在 AD DS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health 常見問題集](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health 版本歷程記錄](active-directory-aadconnect-health-version-history.md)
