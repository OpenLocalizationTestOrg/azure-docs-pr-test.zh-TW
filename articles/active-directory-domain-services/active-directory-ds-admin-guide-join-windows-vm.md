---
title: "Azure Active Directory 網域服務： 加入 Windows Server VM tooa 受管理的網域 |Microsoft 文件"
description: "Windows Server 虛擬機器加入 tooAzure AD 網域服務"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 74dbdb33-05db-4d47-badc-0d7bb6d0c8cb
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1e85833b42bd51f3b3df067d6c5b69253459bec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain"></a>加入 Windows Server 虛擬機器 tooa 受管理的網域
> [!div class="op_single_selector"]
> * [Azure 傳統入口網站 - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

本文章將示範如何 toojoin 虛擬機器執行 Windows Server 2012 R2 tooan Azure AD 網域服務會管理使用 hello Azure 傳統入口網站的網域。

## <a name="step-1-create-hello-windows-server-virtual-machine"></a>步驟 1： 建立 hello Windows Server 虛擬機器
遵循 hello 中所述的 hello 指示[建立執行 Windows hello Azure 傳統入口網站中的虛擬機器](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)教學課程。 這個新建立的虛擬機器的 tooensure 聯結 toohello 務必相同虛擬網路，您已啟用 Azure AD 網域服務。 hello [快速建立] 選項不會讓您 toojoin hello 虛擬機器 tooa 虛擬網路。 因此，您需要 toouse hello ' 位於 從組件庫 」 選項 toocreate hello 虛擬機器。

執行下列步驟 toocreate hello Windows 虛擬機器聯結的 toohello 虛擬網路已啟用 Azure AD 網域服務。

1. 在 hello Azure 傳統入口網站，hello 在 hello hello 視窗底部的命令列上按一下 **新增**。
2. 在 [計算] 底下，依序按一下 [虛擬機器] 和 [從資源庫]。
3. hello 第一個畫面可讓您**選擇映像**您從虛擬機器的可用的映像的 hello 清單。 挑選 hello 適當的映像。

    ![選取映像](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)
4. hello 第二個畫面可讓您選取的電腦名稱、 大小，以及管理使用者名稱和密碼。 您的應用程式或工作負載，請使用 hello 層和所需大小 toorun。 您在這裡所挑選的 hello 使用者名稱為 hello 機器的本機系統管理員使用者。 請勿在此輸入網域使用者帳戶的認證。

    ![設定虛擬機器](./media/active-directory-domain-services-admin-guide/create-windows-vm-config.png)
5. hello 第三個畫面可讓您設定網路功能、 儲存體和可用性的資源。 請選取您已啟用 Azure AD 網域服務，從 hello hello 虛擬網路**區域/同質群組/虛擬網路**下拉式清單。 指定**雲端服務 DNS 名稱**為適合 hello 虛擬機器。

    ![選取虛擬機器的虛擬網路](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

   > [!WARNING]
   > 請確定您加入 hello 虛擬機器 toohello 已啟用 Azure AD 網域服務的相同虛擬網路。 如此一來，可以看到 hello 網域 hello 虛擬機器，並執行工作，例如將 hello 網域。 如果您選擇 toocreate hello 虛擬機器在不同的虛擬網路中，已啟用 Azure AD 網域服務的虛擬網路的 toohello 虛擬網路的連線。
   >
   >
6. hello 第四個畫面可讓您安裝 hello VM 代理程式，並設定一些 hello 可用擴充功能。

    ![完成](./media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
7. Hello 傳統入口網站建立 hello 虛擬機器之後，會列出下 hello hello 新虛擬機器**虛擬機器**節點。 Hello 虛擬機器和雲端服務會自動啟動，而其狀態會列為**執行**。

    ![虛擬機器已啟動並執行](./media/active-directory-domain-services-admin-guide/create-windows-vm-running.png)

## <a name="step-2-connect-toohello-windows-server-virtual-machine-using-hello-local-administrator-account"></a>步驟 2： 連接 toohello 使用 hello 本機系統管理員帳戶的 Windows Server 虛擬機器
現在，我們連接 toohello 新建立的 Windows Server 虛擬機器，toojoin 它 toohello 網域。 使用您指定當建立 hello 的虛擬機器，tooconnect tooit hello 本機系統管理員認證。

執行下列步驟 tooconnect toohello 虛擬機器的 hello。

1. 瀏覽過**虛擬機器**hello 傳統入口網站中的節點。 選取您在步驟 1 中建立的 hello 虛擬機器，然後按一下**連接**hello 在 hello hello 視窗底部的命令列上。

    ![TooWindows 虛擬機器連線](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. hello 傳統入口網站會提示您 tooopen 或儲存 '.rdp' 副檔名的檔案，這是使用的 tooconnect toohello 虛擬機器。 下載完成時，請按一下 tooopen hello 檔案。
3. Hello 登入提示字元之下，輸入您**本機系統管理員認證**，您建立 hello 虛擬機器時所指定。 例如，我們在此範例中使用 'localhost\mahesh'。

此時，您應該登入 toohello 新建立的 Windows 虛擬機器使用本機系統管理員認證。 hello 下一個步驟是 toojoin hello 虛擬機器 toohello 網域。

## <a name="step-3-join-hello-windows-server-virtual-machine-toohello-aad-ds-managed-domain"></a>步驟 3： 加入 hello Windows Server 虛擬機器 toohello AAD DS 受管理的網域
執行下列步驟 toojoin hello Windows Server 虛擬機器 toohello AAD DS 受管理的網域中的 hello。

1. 連接 toohello Windows Server，步驟 2 中所示。 從 hello 開始 畫面開啟**伺服器管理員**。
2. 按一下**本機伺服器**hello hello 伺服器管理員 視窗的左窗格中。

    ![啟動虛擬機器上的伺服器管理員](./media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)
3. 按一下**WORKGROUP**下 hello**屬性**> 一節。 在 hello**系統屬性**屬性頁上，按一下 **變更**toojoin hello 網域。

    ![[系統屬性] 頁面](./media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)
4. 指定 hello 網域名稱，您的 Azure AD 網域服務受管理網域中 hello**網域**文字方塊中，按一下 **確定**。

    ![指定 hello 網域 toobe 聯結](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)
5. 您會提示的 tooenter 認證 toojoin hello 網域。 請確定您**指定使用者隸屬 toohello AAD DC 系統管理員的 hello 認證**群組。 只有此群組的成員有權限 toojoin 機器 toohello 受管理的網域。

    ![指定用於加入網域的認證](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)
6. 您可以使用其中一種 hello 下列方式來指定認證：

   * UPN 格式： 指定 hello hello 使用者帳戶的 UPN 尾碼，Azure AD 中的設定。 在此範例中，hello 使用者 'bob' hello UPN 尾碼是 'bob@domainservicespreview.onmicrosoft.com'。
   * SAMAccountName 格式： 您可以在 hello SAMAccountName 格式指定 hello 帳戶名稱。 在此範例中，hello 使用者 'bob' 需要 tooenter 'CONTOSO100\bob'。

     > [!NOTE]
     > **我們建議使用 hello UPN 格式 toospecify 認證。** 如果使用者的 UPN 前置詞太長 （例如，'joereallylongnameuser'） 自動產生可能 hello SAMAccountName。 如果多個使用者擁有的 hello Azure AD 租用戶中，其 SAMAccountName 格式相同的 UPN 首碼 (例如，' bob') 可能會由自動產生 hello 服務。 在這些情況下，hello UPN 格式可以可靠地使用 toolog toohello 網域中的。
     >
     >
7. 順利加入網域後，您會看到下列訊息出現歡迎您 toohello 網域 hello。 重新啟動 hello 網域聯結作業 toocomplete hello 虛擬機器。

    ![歡迎使用 toohello 網域](./media/active-directory-domain-services-admin-guide/join-domain-done.png)

## <a name="troubleshooting-domain-join"></a>針對加入網域進行疑難排解
### <a name="connectivity-issues"></a>連線能力問題
如果無法 toofind hello 網域 hello 虛擬機器，請參閱 toohello 下列疑難排解步驟：

* 請確認 hello 虛擬機器連線的 toohello 相同虛擬網路，您已啟用網域服務中。 如果沒有，hello 虛擬機器無法 tooconnect toohello 網域網域，因此無法 toojoin hello 網域。
* 如果 hello 虛擬機器連線的 tooanother 虛擬網路，請確定此虛擬網路是連線的 toohello 虛擬網路已啟用網域服務。
* 嘗試使用 tooping hello 網域使用 hello 的 hello 受管理的網域 (例如，' ping contoso100.com') 的網域名稱。 如果您因此無法 toodo，再試一次 tooping hello IP 位址的 hello 網域 hello 頁面上顯示您已啟用 Azure AD 網域服務 (例如，' ping 10.0.0.4')。 如果您不能 tooping hello IP 位址，但未 hello 網域時，DNS 可能設定不正確。 您可能不為 hello 虛擬網路的 DNS 伺服器設定 hello 網域 hello IP 的位址。
* 嘗試排清 hello hello 虛擬機器 ('ipconfig /flushdns') 上的 DNS 解析程式快取。

如果您收到 toohello 對話方塊，詢問認證 toojoin hello 網域，表示您沒有連線問題。

### <a name="credentials-related-issues"></a>與認證相關的問題
請參閱下列步驟，如果您無法使用認證，而且無法 toojoin hello 網域 toohello。

* 請嘗試使用 hello UPN 格式 toospecify 認證。 hello SAMAccountName 為您的帳戶可能是自動產生如果有多個使用者以相同的 UPN 租用戶中的前置詞，或若您的 UPN 前置過度長的 hello。 因此，您可能會與所預期或使用您在內部部署網域中不同 hello SAMAccountName 格式，為您的帳戶。
* Toouse hello 所屬 toohello ' AAD DC Administrators' 群組 toojoin 機器 toohello 受管理的網域使用者帳戶的認證再試一次。
* 請確定您有[啟用密碼同步處理](active-directory-ds-getting-started-password-sync.md)根據 hello hello 快速入門指南中所述的步驟。
* 請務必使用 hello hello 使用者的 UPN，Azure AD 中的設定 (例如，'bob@domainservicespreview.onmicrosoft.com') 中的 toosign。
* 請確定您已經等候夠長的密碼同步處理 toocomplete hello 快速入門指南中所指定。

## <a name="related-content"></a>相關內容
* [Azure AD Domain Services - 入門指南](active-directory-ds-getting-started.md)
* [Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)](active-directory-ds-admin-guide-administer-domain.md)
