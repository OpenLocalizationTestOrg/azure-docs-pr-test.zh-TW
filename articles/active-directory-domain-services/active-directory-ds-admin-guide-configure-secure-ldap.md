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
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="76b52-103">針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)</span><span class="sxs-lookup"><span data-stu-id="76b52-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="76b52-104">本文說明如何為 Azure AD 網域服務受管理網域啟用安全的輕量型目錄存取通訊協定 (LDAPS)。</span><span class="sxs-lookup"><span data-stu-id="76b52-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="76b52-105">安全的 LDAP 亦稱為「透過安全通訊端層 (SSL)/傳輸層安全性 (TLS) 的輕量型目錄存取通訊協定 (LDAP)」。</span><span class="sxs-lookup"><span data-stu-id="76b52-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="76b52-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="76b52-106">Before you begin</span></span>
<span data-ttu-id="76b52-107">本文所列 tooperform hello 工作，您必須：</span><span class="sxs-lookup"><span data-stu-id="76b52-107">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="76b52-108">有效的 **Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="76b52-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="76b52-109">**Azure AD 目錄** - 與內部部署目錄或僅限雲端的目錄同步處理。</span><span class="sxs-lookup"><span data-stu-id="76b52-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="76b52-110">**Azure AD 網域服務**必須啟用 hello Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="76b52-110">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="76b52-111">如果您尚未這樣做，請遵循 hello 中所述的所有 hello 工作[入門指南](active-directory-ds-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="76b52-111">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="76b52-112">A**憑證使用 toobe tooenable 安全 LDAP**。</span><span class="sxs-lookup"><span data-stu-id="76b52-112">A **certificate toobe used tooenable secure LDAP**.</span></span>

   * <span data-ttu-id="76b52-113">**建議** - 從受信任的公共憑證授權單位取得憑證。</span><span class="sxs-lookup"><span data-stu-id="76b52-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="76b52-114">這是更安全的組態選項。</span><span class="sxs-lookup"><span data-stu-id="76b52-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="76b52-115">或者，您也可以選擇太[建立自我簽署的憑證](#task-1---obtain-a-certificate-for-secure-ldap)如本文稍後所示。</span><span class="sxs-lookup"><span data-stu-id="76b52-115">Alternately, you may also choose too[create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a><span data-ttu-id="76b52-116">Hello 安全 LDAP 的憑證需求</span><span class="sxs-lookup"><span data-stu-id="76b52-116">Requirements for hello secure LDAP certificate</span></span>
<span data-ttu-id="76b52-117">取得每個 hello 遵循的指導方針，才能啟用安全 LDAP 的有效憑證。</span><span class="sxs-lookup"><span data-stu-id="76b52-117">Acquire a valid certificate per hello following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="76b52-118">如果您嘗試 tooenable，發生失敗的無效/不正確的憑證與您受管理的網域安全 LDAP。</span><span class="sxs-lookup"><span data-stu-id="76b52-118">You encounter failures if you try tooenable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="76b52-119">**受信任簽發者**-hello 憑證必須由電腦連接 toohello 使用安全 LDAP 的受管理的網域信任授權單位發行。</span><span class="sxs-lookup"><span data-stu-id="76b52-119">**Trusted issuer** - hello certificate must be issued by an authority trusted by computers connecting toohello managed domain using secure LDAP.</span></span> <span data-ttu-id="76b52-120">此授權單位可能是受這些電腦信任的公開憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="76b52-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="76b52-121">**存留期**-hello 憑證必須是有效的最少 hello 接下來 3-6 個月。</span><span class="sxs-lookup"><span data-stu-id="76b52-121">**Lifetime** - hello certificate must be valid for at least hello next 3-6 months.</span></span> <span data-ttu-id="76b52-122">Hello 憑證到期時中斷安全 LDAP 存取 tooyour 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="76b52-122">Secure LDAP access tooyour managed domain is disrupted when hello certificate expires.</span></span>
3. <span data-ttu-id="76b52-123">**主體名稱**-hello hello 憑證的主體名稱必須是受管理的網域的萬用字元。</span><span class="sxs-lookup"><span data-stu-id="76b52-123">**Subject name** - hello subject name on hello certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="76b52-124">比方說，如果您的網域名稱為 'contoso100.com'，hello 憑證的主體名稱必須是 ' *。 contoso100.com'。</span><span class="sxs-lookup"><span data-stu-id="76b52-124">For instance, if your domain is named 'contoso100.com', hello certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="76b52-125">設定 hello DNS 名稱 （主旨替代名稱） toothis 萬用字元名稱。</span><span class="sxs-lookup"><span data-stu-id="76b52-125">Set hello DNS name (subject alternate name) toothis wildcard name.</span></span>
4. <span data-ttu-id="76b52-126">**金鑰使用方法**-hello 之後使用，必須設定 hello 憑證的數位簽章和金鑰加密。</span><span class="sxs-lookup"><span data-stu-id="76b52-126">**Key usage** - hello certificate must be configured for hello following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="76b52-127">**憑證目的**-hello 憑證必須是有效的 SSL 伺服器驗證。</span><span class="sxs-lookup"><span data-stu-id="76b52-127">**Certificate purpose** - hello certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="76b52-128">**企業憑證授權單位︰**Azure AD Domain Services 不支援使用貴組織的企業憑證授權單位所簽發的安全 LDAP 憑證。</span><span class="sxs-lookup"><span data-stu-id="76b52-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="76b52-129">這項限制是因為 hello 服務不信任您的企業 CA 根憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="76b52-129">This restriction is because hello service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="76b52-130">工作 1 - 取得安全 LDAP 的憑證</span><span class="sxs-lookup"><span data-stu-id="76b52-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="76b52-131">hello 第一項工作需要取得憑證，用於安全 LDAP 存取 toohello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="76b52-131">hello first task involves obtaining a certificate used for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="76b52-132">您有兩個選擇：</span><span class="sxs-lookup"><span data-stu-id="76b52-132">You have two options:</span></span>

* <span data-ttu-id="76b52-133">從憑證授權單位取得憑證。</span><span class="sxs-lookup"><span data-stu-id="76b52-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="76b52-134">hello 授權單位可能會公開憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="76b52-134">hello authority may be a public certification authority.</span></span>
* <span data-ttu-id="76b52-135">建立自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="76b52-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="76b52-136">選項 A (建議選項) - 從憑證授權單位取得安全的 LDAP 憑證</span><span class="sxs-lookup"><span data-stu-id="76b52-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="76b52-137">如果您的組織從公開憑證授權單位取得憑證，您需要 tooobtain hello 安全 LDAP 的憑證從該公用憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="76b52-137">If your organization obtains its certificates from a public certification authority, you need tooobtain hello secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="76b52-138">當要求憑證，請確定您符合所有中所述的 hello 需求[hello 安全 LDAP 的憑證需求](#requirements-for-the-secure-ldap-certificate)。</span><span class="sxs-lookup"><span data-stu-id="76b52-138">When requesting a certificate, ensure that you satisfy all hello requirements outlined in [Requirements for hello secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="76b52-139">需要使用安全 LDAP tooconnect toohello 受管理的網域的用戶端電腦必須信任簽發者 hello hello 安全 LDAP 的憑證。</span><span class="sxs-lookup"><span data-stu-id="76b52-139">Client computers that need tooconnect toohello managed domain using secure LDAP must trust hello issuer of hello secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="76b52-140">選項 B - 為安全的 LDAP 建立自我簽署的憑證</span><span class="sxs-lookup"><span data-stu-id="76b52-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="76b52-141">如果您不希望 toouse 從公開憑證授權單位的憑證，您可以選擇 toocreate 自我簽署的憑證安全 ldap。</span><span class="sxs-lookup"><span data-stu-id="76b52-141">If you do not expect toouse a certificate from a public certification authority, you may choose toocreate a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="76b52-142">**使用 PowerShell 建立自我簽署憑證**</span><span class="sxs-lookup"><span data-stu-id="76b52-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="76b52-143">在您的 Windows 電腦上開啟 新的 PowerShell 視窗，做為**管理員**和型別 hello 下列命令，toocreate 新的自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="76b52-143">On your Windows computer, open a new PowerShell window as **Administrator** and type hello following commands, toocreate a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="76b52-144">在上述範例的 hello，取代 '*。 contoso100.com' hello DNS 網域名稱是受管理的網域。例如，如果您建立受管理的網域，稱為 'contoso100.onmicrosoft.com' 取代 '*。 contoso100.com' hello 上述指令碼在' *。 contoso100.onmicrosoft.com')。</span><span class="sxs-lookup"><span data-stu-id="76b52-144">In hello preceding sample, replace '*.contoso100.com' with hello DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in hello above script with '*.contoso100.onmicrosoft.com').</span></span>

![選取 Azure AD 目錄](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="76b52-146">hello 新建立的自我簽署的憑證放置在 hello 本機電腦的憑證存放區中。</span><span class="sxs-lookup"><span data-stu-id="76b52-146">hello newly created self-signed certificate is placed in hello local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="76b52-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="76b52-147">Next step</span></span>
[<span data-ttu-id="76b52-148">工作 2-匯出 hello 安全 LDAP 的憑證 tooa。PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="76b52-148">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
