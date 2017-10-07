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
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="9e66d-103">針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)</span><span class="sxs-lookup"><span data-stu-id="9e66d-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9e66d-104">開始之前</span><span class="sxs-lookup"><span data-stu-id="9e66d-104">Before you begin</span></span>
<span data-ttu-id="9e66d-105">確定您已完成[工作 1 - 取得安全 LDAP 的憑證](active-directory-ds-admin-guide-configure-secure-ldap.md)。</span><span class="sxs-lookup"><span data-stu-id="9e66d-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a><span data-ttu-id="9e66d-106">工作 2-匯出 hello 安全 LDAP 的憑證 tooa。PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="9e66d-106">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>
<span data-ttu-id="9e66d-107">啟動這項工作之前，請確定您已從公開憑證授權單位取得 hello 安全 LDAP 的憑證，或已建立自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="9e66d-107">Before you start this task, ensure that you have obtained hello secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="9e66d-108">執行下列步驟的 hello、 tooexport hello LDAPS 憑證 tooa。PFX 檔案。</span><span class="sxs-lookup"><span data-stu-id="9e66d-108">Perform hello following steps, tooexport hello LDAPS certificate tooa .PFX file.</span></span>

1. <span data-ttu-id="9e66d-109">按 hello**啟動**按鈕並輸入**R**。在 hello**執行**對話方塊中，輸入**mmc**按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="9e66d-109">Press hello **Start** button and type **R**. In hello **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![啟動 hello MMC 主控台](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="9e66d-111">在 hello**使用者帳戶控制**提示字元中，按一下 **是**toolaunch MMC (Microsoft Management Console) 系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="9e66d-111">On hello **User Account Control** prompt, click **YES** toolaunch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="9e66d-112">從 hello**檔案**功能表上，按一下 **新增/移除嵌入式管理單元...**.</span><span class="sxs-lookup"><span data-stu-id="9e66d-112">From hello **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![新增 tooMMC 嵌入式管理單元主控台](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="9e66d-114">在 [hello**新增或移除嵌入式管理單元**對話方塊中，選取 hello**憑證**嵌入式管理單元，按一下 hello**新增 >** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9e66d-114">In hello **Add or Remove Snap-ins** dialog, select hello **Certificates** snap-in, and click hello **Add >** button.</span></span>

    ![新增憑證嵌入式管理單元 tooMMC 主控台](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="9e66d-116">在 hello**憑證嵌入式管理單元**精靈中，選取**電腦帳戶**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="9e66d-116">In hello **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![新增電腦帳戶的憑證嵌入式管理單元](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="9e66d-118">在 hello**選取電腦**頁面上，選取**本機電腦: （執行這個主控台 hello 電腦）**按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="9e66d-118">On hello **Select Computer** page, select **Local computer: (hello computer this console is running on)** and click **Finish**.</span></span>

    ![新增憑證嵌入式管理單元 - 選取電腦](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="9e66d-120">在 [hello**新增或移除嵌入式管理單元**] 對話方塊中，按一下**確定**tooadd hello 憑證嵌入式管理單元 tooMMC。</span><span class="sxs-lookup"><span data-stu-id="9e66d-120">In hello **Add or Remove Snap-ins** dialog, click **OK** tooadd hello certificates snap-in tooMMC.</span></span>

    ![新增憑證嵌入式管理單元 tooMMC-完成](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="9e66d-122">在 hello MMC 視窗中，按一下 tooexpand**主控台根目錄**。</span><span class="sxs-lookup"><span data-stu-id="9e66d-122">In hello MMC window, click tooexpand **Console Root**.</span></span> <span data-ttu-id="9e66d-123">您應該會看到的 hello 憑證嵌入式管理單元載入。</span><span class="sxs-lookup"><span data-stu-id="9e66d-123">You should see hello Certificates snap-in loaded.</span></span> <span data-ttu-id="9e66d-124">按一下**憑證 （本機電腦）** tooexpand。</span><span class="sxs-lookup"><span data-stu-id="9e66d-124">Click **Certificates (Local Computer)** tooexpand.</span></span> <span data-ttu-id="9e66d-125">按一下 tooexpand hello**個人**節點，後面接著 hello**憑證**節點。</span><span class="sxs-lookup"><span data-stu-id="9e66d-125">Click tooexpand hello **Personal** node, followed by hello **Certificates** node.</span></span>

    ![開啟個人憑證存放區](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="9e66d-127">您應該會看到 hello 我們建立的自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="9e66d-127">You should see hello self-signed certificate we created.</span></span> <span data-ttu-id="9e66d-128">您可以查看 hello hello 憑證 tooensure hello 指紋相符項目所報告的 hello 的 PowerShell 視窗中，當您建立 hello 憑證內容。</span><span class="sxs-lookup"><span data-stu-id="9e66d-128">You can examine hello properties of hello certificate tooensure hello thumbprint matches that reported on hello PowerShell windows when you created hello certificate.</span></span>
10. <span data-ttu-id="9e66d-129">選取 hello 自我簽署的憑證和**以滑鼠右鍵按一下**。</span><span class="sxs-lookup"><span data-stu-id="9e66d-129">Select hello self-signed certificate and **right click**.</span></span> <span data-ttu-id="9e66d-130">從 hello 以滑鼠右鍵按一下功能表上，選取**所有工作**選取**匯出...**.</span><span class="sxs-lookup"><span data-stu-id="9e66d-130">From hello right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![匯出憑證](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="9e66d-132">在 hello**憑證匯出精靈**，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="9e66d-132">In hello **Certificate Export Wizard**, click **Next**.</span></span>

    ![匯出憑證精靈](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="9e66d-134">在 hello**匯出私密金鑰**頁面上，選取**是，匯出 hello 私密金鑰**，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="9e66d-134">On hello **Export Private Key** page, select **Yes, export hello private key**, and click **Next**.</span></span>

    ![匯出憑證的私密金鑰](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="9e66d-136">您必須匯出 hello 私密金鑰以及 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="9e66d-136">You MUST export hello private key along with hello certificate.</span></span> <span data-ttu-id="9e66d-137">如果您提供 PFX 不包含 hello hello 憑證私密金鑰，請啟用安全 LDAP 的受管理的網域會失敗。</span><span class="sxs-lookup"><span data-stu-id="9e66d-137">If you provide a PFX that does not contain hello private key for hello certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="9e66d-138">在 hello**匯出檔案格式**頁面上，選取**個人資訊交換-PKCS #12 (。PFX)** hello 的 hello 檔案格式匯出憑證。</span><span class="sxs-lookup"><span data-stu-id="9e66d-138">On hello **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as hello file format for hello exported certificate.</span></span>

    ![匯出憑證檔案格式](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="9e66d-140">只有 hello。支援 PFX 檔案格式。</span><span class="sxs-lookup"><span data-stu-id="9e66d-140">Only hello .PFX file format is supported.</span></span> <span data-ttu-id="9e66d-141">不要匯出 hello 憑證 toohello。CER 檔案格式。</span><span class="sxs-lookup"><span data-stu-id="9e66d-141">Do not export hello certificate toohello .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="9e66d-142">在 hello**安全性**頁面上，選取 hello**密碼**選項然後輸入密碼 tooprotect hello。PFX 檔案。</span><span class="sxs-lookup"><span data-stu-id="9e66d-142">On hello **Security** page, select hello **Password** option and type in a password tooprotect hello .PFX file.</span></span> <span data-ttu-id="9e66d-143">請記住這個密碼，因為它會需要 hello 下一項工作。</span><span class="sxs-lookup"><span data-stu-id="9e66d-143">Remember this password since it will be needed in hello next task.</span></span> <span data-ttu-id="9e66d-144">按一下**下一步**tooproceed。</span><span class="sxs-lookup"><span data-stu-id="9e66d-144">Click **Next** tooproceed.</span></span>

    ![<span data-ttu-id="9e66d-145">憑證匯出的密碼</span><span class="sxs-lookup"><span data-stu-id="9e66d-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="9e66d-146">記下此密碼。</span><span class="sxs-lookup"><span data-stu-id="9e66d-146">Make a note of this password.</span></span> <span data-ttu-id="9e66d-147">您需要時啟用此受管理的網域中的安全 LDAP[工作 3-啟用安全 LDAP 的 hello 受管理的網域](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="9e66d-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for hello managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="9e66d-148">在 hello**檔案 tooExport**頁面上，指定 hello 檔案名稱和位置 tooexport hello 憑證的位置。</span><span class="sxs-lookup"><span data-stu-id="9e66d-148">On hello **File tooExport** page, specify hello file name and location where you'd like tooexport hello certificate.</span></span>

    ![憑證匯出的路徑](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="9e66d-150">在 hello 遵循頁面上，按一下**完成**tooexport hello 憑證 tooa PFX 檔案。</span><span class="sxs-lookup"><span data-stu-id="9e66d-150">On hello following page, click **Finish** tooexport hello certificate tooa PFX file.</span></span> <span data-ttu-id="9e66d-151">已匯出 hello 憑證時，應該會看到確認對話方塊。</span><span class="sxs-lookup"><span data-stu-id="9e66d-151">You should see confirmation dialog when hello certificate has been exported.</span></span>

    ![憑證匯出完成](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="9e66d-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9e66d-153">Next step</span></span>
[<span data-ttu-id="9e66d-154">工作 3-啟用安全 LDAP 的 hello 受管理的網域</span><span class="sxs-lookup"><span data-stu-id="9e66d-154">Task 3 - enable secure LDAP for hello managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
