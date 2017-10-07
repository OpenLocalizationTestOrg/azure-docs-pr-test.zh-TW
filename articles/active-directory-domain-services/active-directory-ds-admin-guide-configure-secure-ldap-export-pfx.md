---
title: "aaaConfigure 安全 LDAP (LDAPS) 在 Azure AD 網域服務中 |Microsoft 文件"
description: "針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 356b28f8392b0e203df9c81177ec842d52866c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)

## <a name="before-you-begin"></a>開始之前
確定您已完成[工作 1 - 取得安全 LDAP 的憑證](active-directory-ds-admin-guide-configure-secure-ldap.md)。


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a>工作 2-匯出 hello 安全 LDAP 的憑證 tooa。PFX 檔案
啟動這項工作之前，請確定您已從公開憑證授權單位取得 hello 安全 LDAP 的憑證，或已建立自我簽署的憑證。

執行下列步驟的 hello、 tooexport hello LDAPS 憑證 tooa。PFX 檔案。

1. 按 hello**啟動**按鈕並輸入**R**。在 hello**執行**對話方塊中，輸入**mmc**按一下**確定**。

    ![啟動 hello MMC 主控台](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. 在 hello**使用者帳戶控制**提示字元中，按一下 **是**toolaunch MMC (Microsoft Management Console) 系統管理員身分。
3. 從 hello**檔案**功能表上，按一下 **新增/移除嵌入式管理單元...**.

    ![新增 tooMMC 嵌入式管理單元主控台](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. 在 [hello**新增或移除嵌入式管理單元**對話方塊中，選取 hello**憑證**嵌入式管理單元，按一下 hello**新增 >** ] 按鈕。

    ![新增憑證嵌入式管理單元 tooMMC 主控台](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. 在 hello**憑證嵌入式管理單元**精靈中，選取**電腦帳戶**按一下**下一步**。

    ![新增電腦帳戶的憑證嵌入式管理單元](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. 在 hello**選取電腦**頁面上，選取**本機電腦: （執行這個主控台 hello 電腦）**按一下**完成**。

    ![新增憑證嵌入式管理單元 - 選取電腦](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. 在 [hello**新增或移除嵌入式管理單元**] 對話方塊中，按一下**確定**tooadd hello 憑證嵌入式管理單元 tooMMC。

    ![新增憑證嵌入式管理單元 tooMMC-完成](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. 在 hello MMC 視窗中，按一下 tooexpand**主控台根目錄**。 您應該會看到的 hello 憑證嵌入式管理單元載入。 按一下**憑證 （本機電腦）** tooexpand。 按一下 tooexpand hello**個人**節點，後面接著 hello**憑證**節點。

    ![開啟個人憑證存放區](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. 您應該會看到 hello 我們建立的自我簽署的憑證。 您可以查看 hello hello 憑證 tooensure hello 指紋相符項目所報告的 hello 的 PowerShell 視窗中，當您建立 hello 憑證內容。
10. 選取 hello 自我簽署的憑證和**以滑鼠右鍵按一下**。 從 hello 以滑鼠右鍵按一下功能表上，選取**所有工作**選取**匯出...**.

    ![匯出憑證](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. 在 hello**憑證匯出精靈**，按一下 **下一步**。

    ![匯出憑證精靈](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. 在 hello**匯出私密金鑰**頁面上，選取**是，匯出 hello 私密金鑰**，按一下 **下一步**。

    ![匯出憑證的私密金鑰](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > 您必須匯出 hello 私密金鑰以及 hello 憑證。 如果您提供 PFX 不包含 hello hello 憑證私密金鑰，請啟用安全 LDAP 的受管理的網域會失敗。
    >
    >
13. 在 hello**匯出檔案格式**頁面上，選取**個人資訊交換-PKCS #12 (。PFX)** hello 的 hello 檔案格式匯出憑證。

    ![匯出憑證檔案格式](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > 只有 hello。支援 PFX 檔案格式。 不要匯出 hello 憑證 toohello。CER 檔案格式。
    >
    >
14. 在 hello**安全性**頁面上，選取 hello**密碼**選項然後輸入密碼 tooprotect hello。PFX 檔案。 請記住這個密碼，因為它會需要 hello 下一項工作。 按一下**下一步**tooproceed。

    ![憑證匯出的密碼 ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > 記下此密碼。 您需要時啟用此受管理的網域中的安全 LDAP[工作 3-啟用安全 LDAP 的 hello 受管理的網域](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
    >
    >
15. 在 hello**檔案 tooExport**頁面上，指定 hello 檔案名稱和位置 tooexport hello 憑證的位置。

    ![憑證匯出的路徑](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. 在 hello 遵循頁面上，按一下**完成**tooexport hello 憑證 tooa PFX 檔案。 已匯出 hello 憑證時，應該會看到確認對話方塊。

    ![憑證匯出完成](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a>後續步驟
[工作 3-啟用安全 LDAP 的 hello 受管理的網域](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
