---
title: "在 Azure AD Domain Services 中設定安全的 LDAP (LDAPS) | Microsoft Docs"
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
ms.openlocfilehash: 5d46f376d46b8bbf3f93de57a7d4e31abdbcdb2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="1ed4b-103">針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)</span><span class="sxs-lookup"><span data-stu-id="1ed4b-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1ed4b-104">開始之前</span><span class="sxs-lookup"><span data-stu-id="1ed4b-104">Before you begin</span></span>
<span data-ttu-id="1ed4b-105">確定您已完成[工作 1 - 取得安全 LDAP 的憑證](active-directory-ds-admin-guide-configure-secure-ldap.md)。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-the-secure-ldap-certificate-to-a-pfx-file"></a><span data-ttu-id="1ed4b-106">工作 2 - 將安全 LDAP 憑證匯出到 .PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="1ed4b-106">Task 2 - export the secure LDAP certificate to a .PFX file</span></span>
<span data-ttu-id="1ed4b-107">在開始這項工作之前，請先確定您已從公共憑證授權單位取得安全的 LDAP 憑證，或已建立自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-107">Before you start this task, ensure that you have obtained the secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="1ed4b-108">執行下列步驟，將 LDAPS 憑證匯出到 .PFX 檔案。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-108">Perform the following steps, to export the LDAPS certificate to a .PFX file.</span></span>

1. <span data-ttu-id="1ed4b-109">按 [開始] 按鈕並輸入 **R**。在 [執行] 對話方塊中，輸入 **mmc**，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-109">Press the **Start** button and type **R**. In the **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![啟動 MMC 主控台](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="1ed4b-111">在 [使用者帳戶控制] 提示字元處按一下 [是]，以系統管理員身分啟動 MMC (Microsoft Management Console)。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-111">On the **User Account Control** prompt, click **YES** to launch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="1ed4b-112">在 [檔案] 功能表上，按一下 [新增/移除嵌入式管理單元...]。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-112">From the **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![新增嵌入式管理單元至 MMC 主控台](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="1ed4b-114">在 [新增或移除嵌入式管理單元] 對話方塊中，選取 [憑證] 嵌入式管理單元，然後按一下 [新增 >] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-114">In the **Add or Remove Snap-ins** dialog, select the **Certificates** snap-in, and click the **Add >** button.</span></span>

    ![新增憑證嵌入式管理單元至 MMC 主控台](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="1ed4b-116">在 [憑證嵌入式管理單元] 精靈中，選取 [電腦帳戶] 並按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-116">In the **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![新增電腦帳戶的憑證嵌入式管理單元](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="1ed4b-118">在 [選取電腦] 頁面上，選取 [本機電腦: (執行這個主控台的電腦)] 並按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-118">On the **Select Computer** page, select **Local computer: (the computer this console is running on)** and click **Finish**.</span></span>

    ![新增憑證嵌入式管理單元 - 選取電腦](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="1ed4b-120">在 [新增或移除嵌入式管理單元] 對話方塊中，按一下 [確定] 以在 MMC 中新增憑證嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-120">In the **Add or Remove Snap-ins** dialog, click **OK** to add the certificates snap-in to MMC.</span></span>

    ![新增憑證嵌入式管理單元至 MMC - 完成](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="1ed4b-122">在 MMC 視窗中，按一下以展開 [主控台根目錄] 。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-122">In the MMC window, click to expand **Console Root**.</span></span> <span data-ttu-id="1ed4b-123">您應該會看到已載入 [憑證] 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-123">You should see the Certificates snap-in loaded.</span></span> <span data-ttu-id="1ed4b-124">按一下 [憑證 (本機電腦)]  加以展開。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-124">Click **Certificates (Local Computer)** to expand.</span></span> <span data-ttu-id="1ed4b-125">按一下以依序展開 [個人] 節點和 [憑證] 節點。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-125">Click to expand the **Personal** node, followed by the **Certificates** node.</span></span>

    ![開啟個人憑證存放區](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="1ed4b-127">您應該會看到我們所建立的自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-127">You should see the self-signed certificate we created.</span></span> <span data-ttu-id="1ed4b-128">您可以檢查憑證的屬性以確定指紋符合您在建立憑證時 PowerShell 視窗上所報告的指紋。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-128">You can examine the properties of the certificate to ensure the thumbprint matches that reported on the PowerShell windows when you created the certificate.</span></span>
10. <span data-ttu-id="1ed4b-129">選取自我簽署憑證並 **按一下滑鼠右鍵**。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-129">Select the self-signed certificate and **right click**.</span></span> <span data-ttu-id="1ed4b-130">在快顯功能表中，依序選取 [所有工作] 和 [匯出...]。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-130">From the right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![匯出憑證](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="1ed4b-132">在 [憑證匯出精靈] 中按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-132">In the **Certificate Export Wizard**, click **Next**.</span></span>

    ![匯出憑證精靈](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="1ed4b-134">在 [匯出私密金鑰] 頁面上，選取 [是，匯出私密金鑰] 並按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-134">On the **Export Private Key** page, select **Yes, export the private key**, and click **Next**.</span></span>

    ![匯出憑證的私密金鑰](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="1ed4b-136">您必須匯出私密金鑰以及憑證。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-136">You MUST export the private key along with the certificate.</span></span> <span data-ttu-id="1ed4b-137">如果您提供的 PFX 未包含憑證的私密金鑰，則為受管理網域啟用安全的 LDAP 會失敗。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-137">If you provide a PFX that does not contain the private key for the certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="1ed4b-138">在 [匯出檔案格式] 頁面上，選取 [個人資訊交換 - PKCS #12 (.PFX)] 作為匯出憑證的檔案格式。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-138">On the **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as the file format for the exported certificate.</span></span>

    ![匯出憑證檔案格式](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="1ed4b-140">只有 .PFX 檔案格式受到支援。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-140">Only the .PFX file format is supported.</span></span> <span data-ttu-id="1ed4b-141">請勿將憑證匯出為 .CER 檔案格式。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-141">Do not export the certificate to the .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="1ed4b-142">在 [安全性] 頁面上選取 [密碼] 選項，然後輸入密碼來保護 .PFX 檔案。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-142">On the **Security** page, select the **Password** option and type in a password to protect the .PFX file.</span></span> <span data-ttu-id="1ed4b-143">請記住此密碼，因為下一個工作會用到它。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-143">Remember this password since it will be needed in the next task.</span></span> <span data-ttu-id="1ed4b-144">按 [下一步]  繼續進行。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-144">Click **Next** to proceed.</span></span>

    ![<span data-ttu-id="1ed4b-145">憑證匯出的密碼</span><span class="sxs-lookup"><span data-stu-id="1ed4b-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="1ed4b-146">記下此密碼。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-146">Make a note of this password.</span></span> <span data-ttu-id="1ed4b-147">在[工作 3 - 為受管理的網域啟用安全 LDAP](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md) 中針對此受管理的網域啟用安全 LDAP 時，需要這個密碼</span><span class="sxs-lookup"><span data-stu-id="1ed4b-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for the managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="1ed4b-148">在 [要匯出的檔案]  頁面上，指定檔案名稱及接收匯出憑證的位置。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-148">On the **File to Export** page, specify the file name and location where you'd like to export the certificate.</span></span>

    ![憑證匯出的路徑](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="1ed4b-150">在接下來的頁面上按一下 [完成]  ，以將憑證匯出至 PFX 檔案。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-150">On the following page, click **Finish** to export the certificate to a PFX file.</span></span> <span data-ttu-id="1ed4b-151">憑證匯出後，您應該會看到確認對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1ed4b-151">You should see confirmation dialog when the certificate has been exported.</span></span>

    ![憑證匯出完成](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="1ed4b-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1ed4b-153">Next step</span></span>
[<span data-ttu-id="1ed4b-154">工作 3 - 為受管理的網域啟用安全 LDAP</span><span class="sxs-lookup"><span data-stu-id="1ed4b-154">Task 3 - enable secure LDAP for the managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
