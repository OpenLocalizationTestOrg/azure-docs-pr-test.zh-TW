---
title: "aaaHow toogenerate 和傳輸受 HSM 保護金鑰的 Azure 金鑰保存庫 |Microsoft 文件"
description: "使用此發行項 toohelp 規劃、 產生，和然後再將您自己的 HSM 保護的金鑰 toouse 使用 Azure 金鑰保存庫。 也稱為 BYOK 或「攜帶您自己的金鑰」。"
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="f16dc-104">如何為 Azure 金鑰保存庫的 toogenerate 並傳輸受 HSM 保護金鑰</span><span class="sxs-lookup"><span data-stu-id="f16dc-104">How toogenerate and transfer HSM-protected keys for Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="f16dc-105">簡介</span><span class="sxs-lookup"><span data-stu-id="f16dc-105">Introduction</span></span>
<span data-ttu-id="f16dc-106">為求保險，當您使用 Azure 金鑰保存庫，您可以匯入或硬體安全性模組 (Hsm)，絕不能離開 hello HSM 界限中產生的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f16dc-106">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="f16dc-107">此案例中通常是參照的 tooas*整合您自己金鑰*，或 BYOK。</span><span class="sxs-lookup"><span data-stu-id="f16dc-107">This scenario is often referred tooas *bring your own key*, or BYOK.</span></span> <span data-ttu-id="f16dc-108">hello Hsm 是的 FIPS 140-2 Level 2 驗證。</span><span class="sxs-lookup"><span data-stu-id="f16dc-108">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="f16dc-109">Azure 金鑰保存庫會使用 Thales nShield 系列 Hsm tooprotect 您的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f16dc-109">Azure Key Vault uses Thales nShield family of HSMs tooprotect your keys.</span></span>

<span data-ttu-id="f16dc-110">使用此主題 toohelp 規劃、 產生，和然後再將您自己與 Azure 金鑰保存庫的 HSM 保護的金鑰 toouse hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="f16dc-110">Use hello information in this topic toohelp you plan for, generate, and then transfer your own HSM-protected keys toouse with Azure Key Vault.</span></span>

<span data-ttu-id="f16dc-111">此功能不適用於 Azure China。</span><span class="sxs-lookup"><span data-stu-id="f16dc-111">This functionality is not available for Azure China.</span></span>

> [!NOTE]
> <span data-ttu-id="f16dc-112">如需 Azure 金鑰保存庫的詳細資訊，請參閱 [什麼是 Azure 金鑰保存庫？](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="f16dc-112">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
>
> <span data-ttu-id="f16dc-113">如需入門教學課程，其中包括建立受 HSM 保護之金鑰的金鑰保存庫，請參閱 [開始使用 Azure 金鑰保存庫](key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="f16dc-113">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>
>
>

<span data-ttu-id="f16dc-114">有關產生及透過 hello 網際網路傳輸受 HSM 保護金鑰的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="f16dc-114">More information about generating and transferring an HSM-protected key over hello Internet:</span></span>

* <span data-ttu-id="f16dc-115">您可以產生 hello 金鑰從離線工作站，能減少 hello 攻擊面。</span><span class="sxs-lookup"><span data-stu-id="f16dc-115">You generate hello key from an offline workstation, which reduces hello attack surface.</span></span>
* <span data-ttu-id="f16dc-116">hello 金鑰進行加密與金鑰交換金鑰 (KEK) 」 是傳送的 toohello Azure 金鑰保存庫 Hsm 之前會持續加密。</span><span class="sxs-lookup"><span data-stu-id="f16dc-116">hello key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred toohello Azure Key Vault HSMs.</span></span> <span data-ttu-id="f16dc-117">只有 hello 加密的金鑰版本會離開 hello 原始工作站。</span><span class="sxs-lookup"><span data-stu-id="f16dc-117">Only hello encrypted version of your key leaves hello original workstation.</span></span>
* <span data-ttu-id="f16dc-118">hello 工具組會繫結您的金鑰 toohello Azure 金鑰保存庫安全園地租用戶金鑰上設定屬性。</span><span class="sxs-lookup"><span data-stu-id="f16dc-118">hello toolset sets properties on your tenant key that binds your key toohello Azure Key Vault security world.</span></span> <span data-ttu-id="f16dc-119">因此在 hello Azure 金鑰保存庫 Hsm 接收和解密金鑰後，只有這些 Hsm 可使用它。</span><span class="sxs-lookup"><span data-stu-id="f16dc-119">So after hello Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="f16dc-120">無法匯出您的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f16dc-120">Your key cannot be exported.</span></span> <span data-ttu-id="f16dc-121">這個繫結是由 hello Thales Hsm 強制執行。</span><span class="sxs-lookup"><span data-stu-id="f16dc-121">This binding is enforced by hello Thales HSMs.</span></span>
* <span data-ttu-id="f16dc-122">hello 金鑰交換金鑰 (KEK) 」 是使用的 tooencrypt 您的金鑰在 hello Azure 金鑰保存庫 Hsm 內部產生並不是可匯出。</span><span class="sxs-lookup"><span data-stu-id="f16dc-122">hello Key Exchange Key (KEK) that is used tooencrypt your key is generated inside hello Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="f16dc-123">hello Hsm 強制執行可能沒有外部 hello Hsm hello KEK 版本。</span><span class="sxs-lookup"><span data-stu-id="f16dc-123">hello HSMs enforce that there can be no clear version of hello KEK outside hello HSMs.</span></span> <span data-ttu-id="f16dc-124">此外，hello 工具組包含了 thales 該 hello KEK 無法匯出，且在 Thales 製造的正版 HSM 內部產生的證明。</span><span class="sxs-lookup"><span data-stu-id="f16dc-124">In addition, hello toolset includes attestation from Thales that hello KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="f16dc-125">hello 工具組包含了 thales 的 hello Azure 金鑰保存庫安全園地也在 Thales 製造的正版 HSM 產生的證明。</span><span class="sxs-lookup"><span data-stu-id="f16dc-125">hello toolset includes attestation from Thales that hello Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="f16dc-126">這證明證明 Microsoft 正在使用正版硬體 tooyou。</span><span class="sxs-lookup"><span data-stu-id="f16dc-126">This attestation proves tooyou that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="f16dc-127">Microsoft 會在每個地理區域使用不同的 KEK 和不同的「安全世界」。</span><span class="sxs-lookup"><span data-stu-id="f16dc-127">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="f16dc-128">這項分隔可確保您的金鑰可以是只在加密該 hello 地區資料中心內。</span><span class="sxs-lookup"><span data-stu-id="f16dc-128">This separation ensures that your key can be used only in data centers in hello region in which you encrypted it.</span></span> <span data-ttu-id="f16dc-129">例如，來自歐洲客戶的金鑰不能在北美或亞洲的資料中心使用。</span><span class="sxs-lookup"><span data-stu-id="f16dc-129">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="f16dc-130">Thales HSM 和 Microsoft 服務的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f16dc-130">More information about Thales HSMs and Microsoft services</span></span>
<span data-ttu-id="f16dc-131">Thales 是提供服務資料加密和網路安全性解決方案 toohello 金融服務、 高科技、 製造、 政府及科技。</span><span class="sxs-lookup"><span data-stu-id="f16dc-131">Thales e-Security is a leading global provider of data encryption and cyber security solutions toohello financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="f16dc-132">40 年追蹤記錄，以保護公司和政府資訊中，Thales 解決方案會使用四個 hello 五個最大能源和太空公司。</span><span class="sxs-lookup"><span data-stu-id="f16dc-132">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of hello five largest energy and aerospace companies.</span></span> <span data-ttu-id="f16dc-133">另外還有 22 個北大西洋公約組織國家也在使用他們的解決方案，而且全世界有超過 80% 的付款交易都受其保障。</span><span class="sxs-lookup"><span data-stu-id="f16dc-133">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="f16dc-134">Microsoft 與 Thales tooenhance hello 狀態封面的 Hsm 的合作。</span><span class="sxs-lookup"><span data-stu-id="f16dc-134">Microsoft has collaborated with Thales tooenhance hello state of art for HSMs.</span></span> <span data-ttu-id="f16dc-135">這些增強功能可讓您 tooget hello 一般託管服務的好處不必放棄您金鑰的控制權。</span><span class="sxs-lookup"><span data-stu-id="f16dc-135">These enhancements enable you tooget hello typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="f16dc-136">具體來說，這些增強功能可讓 Microsoft 管理 hello Hsm，如此不需要。</span><span class="sxs-lookup"><span data-stu-id="f16dc-136">Specifically, these enhancements let Microsoft manage hello HSMs so that you do not have to.</span></span> <span data-ttu-id="f16dc-137">為雲端服務、 Azure 金鑰保存庫會依據迅速 toomeet 升高貴組織的使用方式。</span><span class="sxs-lookup"><span data-stu-id="f16dc-137">As a cloud service, Azure Key Vault scales up at short notice toomeet your organization’s usage spikes.</span></span> <span data-ttu-id="f16dc-138">在 hello 相同時間，在 Microsoft 的 Hsm 內部保護您的金鑰： 您保留 hello 金鑰生命週期的控制權，因為您產生 hello 金鑰，並將它傳輸 tooMicrosoft 的 Hsm。</span><span class="sxs-lookup"><span data-stu-id="f16dc-138">At hello same time, your key is protected inside Microsoft’s HSMs: You retain control over hello key lifecycle because you generate hello key and transfer it tooMicrosoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="f16dc-139">實作 Azure 金鑰保存庫的自備金鑰 (BYOK)</span><span class="sxs-lookup"><span data-stu-id="f16dc-139">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>
<span data-ttu-id="f16dc-140">使用 hello 下列資訊和程序，如果您將會產生您自己的 HSM 保護金鑰並將其傳輸 tooAzure 金鑰保存庫 — hello 攜帶您自己的金鑰 (BYOK) 案例。</span><span class="sxs-lookup"><span data-stu-id="f16dc-140">Use hello following information and procedures if you will generate your own HSM-protected key and then transfer it tooAzure Key Vault—hello bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="f16dc-141">BYOK 的必要條件</span><span class="sxs-lookup"><span data-stu-id="f16dc-141">Prerequisites for BYOK</span></span>
<span data-ttu-id="f16dc-142">請參閱 hello 下表的必要條件清單為 Azure 金鑰保存庫整合您自己的金鑰 (BYOK)。</span><span class="sxs-lookup"><span data-stu-id="f16dc-142">See hello following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="f16dc-143">需求</span><span class="sxs-lookup"><span data-stu-id="f16dc-143">Requirement</span></span> | <span data-ttu-id="f16dc-144">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f16dc-144">More information</span></span> |
| --- | --- |
| <span data-ttu-id="f16dc-145">訂用帳戶 tooAzure</span><span class="sxs-lookup"><span data-stu-id="f16dc-145">A subscription tooAzure</span></span> |<span data-ttu-id="f16dc-146">toocreate Azure 金鑰保存庫，您需要 Azure 訂用帳戶：[申請免費試用版](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="f16dc-146">toocreate an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="f16dc-147">hello Azure 金鑰保存庫 Premium 服務層 toosupport 受 HSM 保護的金鑰</span><span class="sxs-lookup"><span data-stu-id="f16dc-147">hello Azure Key Vault Premium service tier toosupport HSM-protected keys</span></span> |<span data-ttu-id="f16dc-148">如需 Azure 金鑰保存庫 hello 服務層和功能的詳細資訊，請參閱 hello [Azure 金鑰保存庫定價](https://azure.microsoft.com/pricing/details/key-vault/)網站。</span><span class="sxs-lookup"><span data-stu-id="f16dc-148">For more information about hello service tiers and capabilities for Azure Key Vault, see hello [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="f16dc-149">Thales HSM、智慧卡和支援軟體</span><span class="sxs-lookup"><span data-stu-id="f16dc-149">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="f16dc-150">您必須擁有存取 tooa Thales 硬體安全性模組並具備 Thales Hsm 的基礎操作知識。</span><span class="sxs-lookup"><span data-stu-id="f16dc-150">You must have access tooa Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="f16dc-151">請參閱[Thales 硬體安全性模組](https://www.thales-esecurity.com/msrms/buy)相容模型或 HSM，如果您還沒有 toopurchase hello 清單。</span><span class="sxs-lookup"><span data-stu-id="f16dc-151">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for hello list of compatible models, or toopurchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="f16dc-152">hello 下列硬體和軟體：</span><span class="sxs-lookup"><span data-stu-id="f16dc-152">hello following hardware and software:</span></span><ol><li><span data-ttu-id="f16dc-153">離線 x64 工作站、至少為 Windows 7 的 Windows 作業系統，以及至少為 11.50 版的 Thales nShield 軟體。</span><span class="sxs-lookup"><span data-stu-id="f16dc-153">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="f16dc-154">如果此工作站執行 Windows 7，您必須[安裝 Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe)。</span><span class="sxs-lookup"><span data-stu-id="f16dc-154">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="f16dc-155">工作站連接的 toohello 網際網路且具有至少 Windows 作業系統的 Windows 7 和[Azure PowerShell](/powershell/azure/overview) **最小版本 1.1.0**安裝。</span><span class="sxs-lookup"><span data-stu-id="f16dc-155">A workstation that is connected toohello Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](/powershell/azure/overview) **minimum version 1.1.0** installed.</span></span></li><li><span data-ttu-id="f16dc-156">至少有 16 MB 可用空間的 USB 磁碟機或其他可攜式儲存裝置。</span><span class="sxs-lookup"><span data-stu-id="f16dc-156">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="f16dc-157">基於安全性理由，我們建議 hello 第一個工作站不是連接的 tooa 網路。</span><span class="sxs-lookup"><span data-stu-id="f16dc-157">For security reasons, we recommend that hello first workstation is not connected tooa network.</span></span> <span data-ttu-id="f16dc-158">不過，在程式設計方面並不強迫採取這項建議。</span><span class="sxs-lookup"><span data-stu-id="f16dc-158">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="f16dc-159">請注意，hello 接下來的指示，在此工作站參照的 tooas hello 中斷連線的工作站。</span><span class="sxs-lookup"><span data-stu-id="f16dc-159">Note that in hello instructions that follow, this workstation is referred tooas hello disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="f16dc-160">此外，如果您的租用戶金鑰適用於生產網路中，我們建議您使用的第二部個別工作站 toodownload hello 工具組和上傳 hello 租用戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="f16dc-160">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation toodownload hello toolset and upload hello tenant key.</span></span> <span data-ttu-id="f16dc-161">但為了測試用途，您可以使用如 hello 第一個 hello 相同的工作站。</span><span class="sxs-lookup"><span data-stu-id="f16dc-161">But for testing purposes, you can use hello same workstation as hello first one.</span></span><br/><br/><span data-ttu-id="f16dc-162">請注意，在 hello 接下來的指示，此第二部工作站參照的 tooas hello 連線網際網路的工作站。</span><span class="sxs-lookup"><span data-stu-id="f16dc-162">Note that in hello instructions that follow, this second workstation is referred tooas hello Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a><span data-ttu-id="f16dc-163">產生並傳輸您的金鑰 tooAzure 金鑰保存庫 HSM</span><span class="sxs-lookup"><span data-stu-id="f16dc-163">Generate and transfer your key tooAzure Key Vault HSM</span></span>
<span data-ttu-id="f16dc-164">您將使用下列五個步驟 toogenerate hello，並傳輸您的金鑰 tooan Azure 金鑰保存庫 HSM:</span><span class="sxs-lookup"><span data-stu-id="f16dc-164">You will use hello following five steps toogenerate and transfer your key tooan Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="f16dc-165">步驟 1：準備網際網路連線的工作站</span><span class="sxs-lookup"><span data-stu-id="f16dc-165">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="f16dc-166">步驟 2：準備中斷連線的工作站</span><span class="sxs-lookup"><span data-stu-id="f16dc-166">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="f16dc-167">步驟 3：產生您的金鑰</span><span class="sxs-lookup"><span data-stu-id="f16dc-167">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="f16dc-168">步驟 4：準備要傳輸的金鑰</span><span class="sxs-lookup"><span data-stu-id="f16dc-168">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="f16dc-169">步驟 5： 傳送您的金鑰 tooAzure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="f16dc-169">Step 5: Transfer your key tooAzure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="f16dc-170">步驟 1：準備網際網路連線的工作站</span><span class="sxs-lookup"><span data-stu-id="f16dc-170">Step 1: Prepare your Internet-connected workstation</span></span>
<span data-ttu-id="f16dc-171">第一個步驟中，請勿 hello 下列程序，您會連接的 toohello 網際網路的工作站上。</span><span class="sxs-lookup"><span data-stu-id="f16dc-171">For this first step, do hello following procedures on your workstation that is connected toohello Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="f16dc-172">步驟 1.1：安裝 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f16dc-172">Step 1.1: Install Azure PowerShell</span></span>
<span data-ttu-id="f16dc-173">從 hello 連線網際網路的工作站，下載並安裝 hello Azure PowerShell 模組包含 hello cmdlet toomanage Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="f16dc-173">From hello Internet-connected workstation, download and install hello Azure PowerShell module that includes hello cmdlets toomanage Azure Key Vault.</span></span> <span data-ttu-id="f16dc-174">這需要得最低版本為 0.8.13。</span><span class="sxs-lookup"><span data-stu-id="f16dc-174">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="f16dc-175">如需安裝指示，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="f16dc-175">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="f16dc-176">步驟 1.2：取得您的 Azure 訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="f16dc-176">Step 1.2: Get your Azure subscription ID</span></span>
<span data-ttu-id="f16dc-177">啟動 Azure PowerShell 工作階段，並使用下列命令的 hello 登入 tooyour Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="f16dc-177">Start an Azure PowerShell session and sign in tooyour Azure account by using hello following command:</span></span>

        Add-AzureAccount
<span data-ttu-id="f16dc-178">在 [hello] 快顯瀏覽器視窗中，輸入您的 Azure 帳戶使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f16dc-178">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="f16dc-179">然後，使用 hello [Get-azuresubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0)命令：</span><span class="sxs-lookup"><span data-stu-id="f16dc-179">Then, use hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span></span>

        Get-AzureSubscription
<span data-ttu-id="f16dc-180">從 hello 輸出，找出 hello 識別碼 hello 訂用帳戶將用於 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="f16dc-180">From hello output, locate hello ID for hello subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="f16dc-181">您稍後將需要此訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="f16dc-181">You will need this subscription ID later.</span></span>

<span data-ttu-id="f16dc-182">請勿關閉 hello Azure PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="f16dc-182">Do not close hello Azure PowerShell window.</span></span>

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="f16dc-183">步驟 1.3： 下載 Azure 金鑰保存庫 hello BYOK 工具組</span><span class="sxs-lookup"><span data-stu-id="f16dc-183">Step 1.3: Download hello BYOK toolset for Azure Key Vault</span></span>
<span data-ttu-id="f16dc-184">前往 Microsoft 下載中心 toohello 和[下載 hello Azure 金鑰保存庫 BYOK 工具組](http://www.microsoft.com/download/details.aspx?id=45345)地理區域或 Azure 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="f16dc-184">Go toohello Microsoft Download Center and [download hello Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="f16dc-185">使用 hello 下列資訊 tooidentify hello 封裝名稱 toodownload 以及其對應的 SHA 256 封裝的雜湊：</span><span class="sxs-lookup"><span data-stu-id="f16dc-185">Use hello following information tooidentify hello package name toodownload and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="f16dc-186">**美國：**</span><span class="sxs-lookup"><span data-stu-id="f16dc-186">**United States:**</span></span>

<span data-ttu-id="f16dc-187">KeyVault-BYOK-Tools-UnitedStates.zip</span><span class="sxs-lookup"><span data-stu-id="f16dc-187">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="f16dc-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span><span class="sxs-lookup"><span data-stu-id="f16dc-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span></span>

- - -
<span data-ttu-id="f16dc-189">**歐洲︰**</span><span class="sxs-lookup"><span data-stu-id="f16dc-189">**Europe:**</span></span>

<span data-ttu-id="f16dc-190">KeyVault-BYOK-Tools-Europe.zip</span><span class="sxs-lookup"><span data-stu-id="f16dc-190">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="f16dc-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span><span class="sxs-lookup"><span data-stu-id="f16dc-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span></span>

- - -
<span data-ttu-id="f16dc-192">**亞洲︰**</span><span class="sxs-lookup"><span data-stu-id="f16dc-192">**Asia:**</span></span>

<span data-ttu-id="f16dc-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span><span class="sxs-lookup"><span data-stu-id="f16dc-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="f16dc-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span><span class="sxs-lookup"><span data-stu-id="f16dc-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span></span>

- - -
<span data-ttu-id="f16dc-195">**拉丁美洲︰**</span><span class="sxs-lookup"><span data-stu-id="f16dc-195">**Latin America:**</span></span>

<span data-ttu-id="f16dc-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span><span class="sxs-lookup"><span data-stu-id="f16dc-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="f16dc-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span><span class="sxs-lookup"><span data-stu-id="f16dc-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span></span>

- - -
<span data-ttu-id="f16dc-198">**日本︰**</span><span class="sxs-lookup"><span data-stu-id="f16dc-198">**Japan:**</span></span>

<span data-ttu-id="f16dc-199">KeyVault-BYOK-Tools-Japan.zip</span><span class="sxs-lookup"><span data-stu-id="f16dc-199">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="f16dc-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span><span class="sxs-lookup"><span data-stu-id="f16dc-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span></span>

- - -
<span data-ttu-id="f16dc-201">**韓國：**</span><span class="sxs-lookup"><span data-stu-id="f16dc-201">**Korea:**</span></span>

<span data-ttu-id="f16dc-202">KeyVault-BYOK-Tools-Korea.zip</span><span class="sxs-lookup"><span data-stu-id="f16dc-202">KeyVault-BYOK-Tools-Korea.zip</span></span>

<span data-ttu-id="f16dc-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span><span class="sxs-lookup"><span data-stu-id="f16dc-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span></span>

- - -
<span data-ttu-id="f16dc-204">**澳大利亞：**</span><span class="sxs-lookup"><span data-stu-id="f16dc-204">**Australia:**</span></span>

<span data-ttu-id="f16dc-205">KeyVault-BYOK-Tools-Australia.zip</span><span class="sxs-lookup"><span data-stu-id="f16dc-205">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="f16dc-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span><span class="sxs-lookup"><span data-stu-id="f16dc-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span></span>

- - -
[<span data-ttu-id="f16dc-207">**Azure Government:**</span><span class="sxs-lookup"><span data-stu-id="f16dc-207">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="f16dc-208">KeyVault-BYOK-Tools-USGovCloud.zip</span><span class="sxs-lookup"><span data-stu-id="f16dc-208">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="f16dc-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span><span class="sxs-lookup"><span data-stu-id="f16dc-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span></span>

- - -
<span data-ttu-id="f16dc-210">**美國政府國防部：**</span><span class="sxs-lookup"><span data-stu-id="f16dc-210">**US Government DOD:**</span></span>

<span data-ttu-id="f16dc-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span><span class="sxs-lookup"><span data-stu-id="f16dc-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span></span>

<span data-ttu-id="f16dc-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span><span class="sxs-lookup"><span data-stu-id="f16dc-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span></span>

- - -
<span data-ttu-id="f16dc-213">**加拿大：**</span><span class="sxs-lookup"><span data-stu-id="f16dc-213">**Canada:**</span></span>

<span data-ttu-id="f16dc-214">KeyVault-BYOK-Tools-Canada.zip</span><span class="sxs-lookup"><span data-stu-id="f16dc-214">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="f16dc-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span><span class="sxs-lookup"><span data-stu-id="f16dc-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span></span>

- - -
<span data-ttu-id="f16dc-216">**德國：**</span><span class="sxs-lookup"><span data-stu-id="f16dc-216">**Germany:**</span></span>

<span data-ttu-id="f16dc-217">KeyVault-BYOK-Tools-Germany.zip</span><span class="sxs-lookup"><span data-stu-id="f16dc-217">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="f16dc-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span><span class="sxs-lookup"><span data-stu-id="f16dc-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span></span>

- - -
<span data-ttu-id="f16dc-219">**印度：**</span><span class="sxs-lookup"><span data-stu-id="f16dc-219">**India:**</span></span>

<span data-ttu-id="f16dc-220">KeyVault-BYOK-Tools-India.zip</span><span class="sxs-lookup"><span data-stu-id="f16dc-220">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="f16dc-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span><span class="sxs-lookup"><span data-stu-id="f16dc-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span></span>

- - -
<span data-ttu-id="f16dc-222">**英國：**</span><span class="sxs-lookup"><span data-stu-id="f16dc-222">**United Kingdom:**</span></span>

<span data-ttu-id="f16dc-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span><span class="sxs-lookup"><span data-stu-id="f16dc-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="f16dc-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span><span class="sxs-lookup"><span data-stu-id="f16dc-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span></span>

- - -

<span data-ttu-id="f16dc-225">您已下載 BYOK 工具組，從您的 Azure PowerShell 工作階段，使用 hello toovalidate hello 完整性[Get-filehash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f16dc-225">toovalidate hello integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

    Get-FileHash KeyVault-BYOK-Tools-*.zip

<span data-ttu-id="f16dc-226">hello 工具組包含下列 hello:</span><span class="sxs-lookup"><span data-stu-id="f16dc-226">hello toolset includes hello following:</span></span>

* <span data-ttu-id="f16dc-227">具有以 **BYOK-KEK-pkg-**</span><span class="sxs-lookup"><span data-stu-id="f16dc-227">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="f16dc-228">具有以 **BYOK-SecurityWorld-pkg-**</span><span class="sxs-lookup"><span data-stu-id="f16dc-228">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="f16dc-229">名為 **verifykeypackage.py** 的 python 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f16dc-229">A python script named **verifykeypackage.py.**</span></span>
* <span data-ttu-id="f16dc-230">名為 **KeyTransferRemote.exe** 的命令列可執行檔和相關聯的 DLL。</span><span class="sxs-lookup"><span data-stu-id="f16dc-230">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="f16dc-231">Visual C++ 可轉散發套件，名為 **vcredist_x64.exe**。</span><span class="sxs-lookup"><span data-stu-id="f16dc-231">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="f16dc-232">複製 hello 封裝 tooa USB 磁碟機或其他可攜式儲存裝置。</span><span class="sxs-lookup"><span data-stu-id="f16dc-232">Copy hello package tooa USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="f16dc-233">步驟 2：準備中斷連線的工作站</span><span class="sxs-lookup"><span data-stu-id="f16dc-233">Step 2: Prepare your disconnected workstation</span></span>
<span data-ttu-id="f16dc-234">第二個步驟中，請勿 hello 下列程序不是連接的 tooa 網路 （網際網路 hello 或您的內部網路） 的 hello 工作站上。</span><span class="sxs-lookup"><span data-stu-id="f16dc-234">For this second step, do hello following procedures on hello workstation that is not connected tooa network (either hello Internet or your internal network).</span></span>

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="f16dc-235">步驟 2.1： 準備中斷連線的 hello 工作站使用 Thales HSM</span><span class="sxs-lookup"><span data-stu-id="f16dc-235">Step 2.1: Prepare hello disconnected workstation with Thales HSM</span></span>
<span data-ttu-id="f16dc-236">在 Windows 電腦上安裝 hello nCipher (Thales) 支援軟體，再附加 Thales HSM toothat 電腦。</span><span class="sxs-lookup"><span data-stu-id="f16dc-236">Install hello nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM toothat computer.</span></span>

<span data-ttu-id="f16dc-237">確定該 hello Thales 工具位於您的路徑 (**%nfast_home%\bin**)。</span><span class="sxs-lookup"><span data-stu-id="f16dc-237">Ensure that hello Thales tools are in your path (**%nfast_home%\bin**).</span></span> <span data-ttu-id="f16dc-238">例如，輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="f16dc-238">For example, type hello following:</span></span>

        set PATH=%PATH%;"%nfast_home%\bin"

<span data-ttu-id="f16dc-239">如需詳細資訊，請參閱隨附 hello Thales HSM 的 hello 使用者指南。</span><span class="sxs-lookup"><span data-stu-id="f16dc-239">For more information, see hello user guide included with hello Thales HSM.</span></span>

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a><span data-ttu-id="f16dc-240">步驟 2.2： 安裝 hello BYOK 工具組在 hello 中斷連線的工作站上</span><span class="sxs-lookup"><span data-stu-id="f16dc-240">Step 2.2: Install hello BYOK toolset on hello disconnected workstation</span></span>
<span data-ttu-id="f16dc-241">複製 hello BYOK 工具組封裝從 hello USB 磁碟機或其他可攜式儲存裝置，並執行再 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="f16dc-241">Copy hello BYOK toolset package from hello USB drive or other portable storage, and then do hello following:</span></span>

1. <span data-ttu-id="f16dc-242">Hello 下載封裝中的 hello 檔案解壓縮至任何資料夾中。</span><span class="sxs-lookup"><span data-stu-id="f16dc-242">Extract hello files from hello downloaded package into any folder.</span></span>
2. <span data-ttu-id="f16dc-243">從該資料夾執行 vcredist_x64.exe。</span><span class="sxs-lookup"><span data-stu-id="f16dc-243">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="f16dc-244">請遵循 hello 指示 toohello for Visual Studio 2013 安裝 hello Visual c + + 執行階段元件。</span><span class="sxs-lookup"><span data-stu-id="f16dc-244">Follow hello instructions toohello install hello Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="f16dc-245">步驟 3：產生您的金鑰</span><span class="sxs-lookup"><span data-stu-id="f16dc-245">Step 3: Generate your key</span></span>
<span data-ttu-id="f16dc-246">第三個步驟中，請勿 hello hello 中斷連線的工作站上，下列程序。</span><span class="sxs-lookup"><span data-stu-id="f16dc-246">For this third step, do hello following procedures on hello disconnected workstation.</span></span> <span data-ttu-id="f16dc-247">toocomplete 此步驟中您的 HSM 必須在初始化模式。</span><span class="sxs-lookup"><span data-stu-id="f16dc-247">toocomplete this step your HSM must be in initialization mode.</span></span> 


### <a name="step-31-change-hello-hsm-mode-tooi"></a><span data-ttu-id="f16dc-248">步驟 3.1： 變更 hello HSM 模式 too'I'</span><span class="sxs-lookup"><span data-stu-id="f16dc-248">Step 3.1: Change hello HSM mode too'I'</span></span>
<span data-ttu-id="f16dc-249">如果您使用 Thales nShield 邊緣，toochange hello 模式： 1。</span><span class="sxs-lookup"><span data-stu-id="f16dc-249">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="f16dc-250">使用 hello 模式按鈕 toohighlight hello 必要的模式。</span><span class="sxs-lookup"><span data-stu-id="f16dc-250">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="f16dc-251">2.</span><span class="sxs-lookup"><span data-stu-id="f16dc-251">2.</span></span> <span data-ttu-id="f16dc-252">在幾秒內，按住不放 hello 清除 按鈕的秒數。</span><span class="sxs-lookup"><span data-stu-id="f16dc-252">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="f16dc-253">Hello 模式變更時，如果 hello 新模式 LED 停止閃爍，則維持亮燈。</span><span class="sxs-lookup"><span data-stu-id="f16dc-253">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="f16dc-254">hello 狀態 LED 可能不規則快閃數秒鐘，然後閃爍 hello 裝置已就緒時，定期。</span><span class="sxs-lookup"><span data-stu-id="f16dc-254">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="f16dc-255">否則，hello 裝置仍會留在 hello 目前的模式，與 hello 適當模式 LED 亮起。</span><span class="sxs-lookup"><span data-stu-id="f16dc-255">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>

### <a name="step-32-create-a-security-world"></a><span data-ttu-id="f16dc-256">步驟 3.2：建立安全世界</span><span class="sxs-lookup"><span data-stu-id="f16dc-256">Step 3.2: Create a security world</span></span>
<span data-ttu-id="f16dc-257">啟動命令提示字元並執行 Thales new-world 程式 hello。</span><span class="sxs-lookup"><span data-stu-id="f16dc-257">Start a command prompt and run hello Thales new-world program.</span></span>

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

<span data-ttu-id="f16dc-258">此程式會**安全園地**檔案位於 %nfast_kmdata%\local\world，對應 toohello C:\ProgramData\nCipher\Key Management Data\local 資料夾對應。</span><span class="sxs-lookup"><span data-stu-id="f16dc-258">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds toohello C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="f16dc-259">您可以使用不同的值為 hello 仲裁，但是在本例中，您可以提示的 tooenter 三卡片和 pin，針對每個。</span><span class="sxs-lookup"><span data-stu-id="f16dc-259">You can use different values for hello quorum but in our example, you’re prompted tooenter three blank cards and pins for each one.</span></span> <span data-ttu-id="f16dc-260">然後，任兩張卡片提供完整存取 toohello 安全園地。</span><span class="sxs-lookup"><span data-stu-id="f16dc-260">Then, any two cards give full access toohello security world.</span></span> <span data-ttu-id="f16dc-261">這些卡片將成為 hello**系統管理員卡組**hello 新安全園地。</span><span class="sxs-lookup"><span data-stu-id="f16dc-261">These cards become hello **Administrator Card Set** for hello new security world.</span></span>

<span data-ttu-id="f16dc-262">然後 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="f16dc-262">Then do hello following:</span></span>

* <span data-ttu-id="f16dc-263">Hello world 檔案備份。</span><span class="sxs-lookup"><span data-stu-id="f16dc-263">Back up hello world file.</span></span> <span data-ttu-id="f16dc-264">安全和保護 hello world 檔案、 hello 系統管理員卡及其 pin 碼，並確定沒有一個人可存取 toomore 比一張牌。</span><span class="sxs-lookup"><span data-stu-id="f16dc-264">Secure and protect hello world file, hello Administrator Cards, and their pins, and make sure that no single person has access toomore than one card.</span></span>

### <a name="step-33-change-hello-hsm-mode-tooo"></a><span data-ttu-id="f16dc-265">步驟 3.3： 變更 hello HSM 模式 too'O'</span><span class="sxs-lookup"><span data-stu-id="f16dc-265">Step 3.3: Change hello HSM mode too'O'</span></span>
<span data-ttu-id="f16dc-266">如果您使用 Thales nShield 邊緣，toochange hello 模式： 1。</span><span class="sxs-lookup"><span data-stu-id="f16dc-266">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="f16dc-267">使用 hello 模式按鈕 toohighlight hello 必要的模式。</span><span class="sxs-lookup"><span data-stu-id="f16dc-267">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="f16dc-268">2.</span><span class="sxs-lookup"><span data-stu-id="f16dc-268">2.</span></span> <span data-ttu-id="f16dc-269">在幾秒內，按住不放 hello 清除 按鈕的秒數。</span><span class="sxs-lookup"><span data-stu-id="f16dc-269">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="f16dc-270">Hello 模式變更時，如果 hello 新模式 LED 停止閃爍，則維持亮燈。</span><span class="sxs-lookup"><span data-stu-id="f16dc-270">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="f16dc-271">hello 狀態 LED 可能不規則快閃數秒鐘，然後閃爍 hello 裝置已就緒時，定期。</span><span class="sxs-lookup"><span data-stu-id="f16dc-271">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="f16dc-272">否則，hello 裝置仍會留在 hello 目前的模式，與 hello 適當模式 LED 亮起。</span><span class="sxs-lookup"><span data-stu-id="f16dc-272">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>


### <a name="step-34-validate-hello-downloaded-package"></a><span data-ttu-id="f16dc-273">步驟 3.4： 驗證下載的 hello 套件</span><span class="sxs-lookup"><span data-stu-id="f16dc-273">Step 3.4: Validate hello downloaded package</span></span>
<span data-ttu-id="f16dc-274">這個步驟是選擇性但建議使用，因此，您可以驗證下列 hello:</span><span class="sxs-lookup"><span data-stu-id="f16dc-274">This step is optional but recommended so that you can validate hello following:</span></span>

* <span data-ttu-id="f16dc-275">已從正版 Thales HSM 產生 hello 隨附於 hello 工具組的金鑰交換金鑰。</span><span class="sxs-lookup"><span data-stu-id="f16dc-275">hello Key Exchange Key that is included in hello toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="f16dc-276">已在正版 Thales HSM 中產生的 hello 隨附於 hello 工具組的安全園地的 hello 雜湊。</span><span class="sxs-lookup"><span data-stu-id="f16dc-276">hello hash of hello Security World that is included in hello toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="f16dc-277">hello 金鑰交換金鑰為非可匯出。</span><span class="sxs-lookup"><span data-stu-id="f16dc-277">hello Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="f16dc-278">toovalidate hello 下載封裝，hello HSM 必須連接、 電源已開啟，而且必須具有安全園地上 （例如您剛才建立的其中一個 hello)。</span><span class="sxs-lookup"><span data-stu-id="f16dc-278">toovalidate hello downloaded package, hello HSM must be connected, powered on, and must have a security world on it (such as hello one you’ve just created).</span></span>
>
>

<span data-ttu-id="f16dc-279">toovalidate hello 下載封裝：</span><span class="sxs-lookup"><span data-stu-id="f16dc-279">toovalidate hello downloaded package:</span></span>

1. <span data-ttu-id="f16dc-280">輸入一個 hello 下列程式碼，根據您的地理區域或 Azure 的執行個體，以執行 hello verifykeypackage.py 指令碼：</span><span class="sxs-lookup"><span data-stu-id="f16dc-280">Run hello verifykeypackage.py script by typing one of hello following, depending on your geographic region or instance of Azure:</span></span>

   * <span data-ttu-id="f16dc-281">北美洲：</span><span class="sxs-lookup"><span data-stu-id="f16dc-281">For North America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="f16dc-282">歐洲：</span><span class="sxs-lookup"><span data-stu-id="f16dc-282">For Europe:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="f16dc-283">亞洲：</span><span class="sxs-lookup"><span data-stu-id="f16dc-283">For Asia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="f16dc-284">拉丁美洲：</span><span class="sxs-lookup"><span data-stu-id="f16dc-284">For Latin America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="f16dc-285">日本：</span><span class="sxs-lookup"><span data-stu-id="f16dc-285">For Japan:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="f16dc-286">韓國︰</span><span class="sxs-lookup"><span data-stu-id="f16dc-286">For Korea:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * <span data-ttu-id="f16dc-287">澳大利亞：</span><span class="sxs-lookup"><span data-stu-id="f16dc-287">For Australia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="f16dc-288">如[Azure 政府](https://azure.microsoft.com/features/gov/)，它會使用的 Azure hello 美國政府執行個體：</span><span class="sxs-lookup"><span data-stu-id="f16dc-288">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="f16dc-289">美國政府國防部：</span><span class="sxs-lookup"><span data-stu-id="f16dc-289">For US Government DOD:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * <span data-ttu-id="f16dc-290">針對加拿大：</span><span class="sxs-lookup"><span data-stu-id="f16dc-290">For Canada:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="f16dc-291">針對德國：</span><span class="sxs-lookup"><span data-stu-id="f16dc-291">For Germany:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="f16dc-292">針對印度︰</span><span class="sxs-lookup"><span data-stu-id="f16dc-292">For India:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > <span data-ttu-id="f16dc-293">hello Thales 軟體包含 python，位於 %NFAST_HOME%\python\bin</span><span class="sxs-lookup"><span data-stu-id="f16dc-293">hello Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     >
     >
2. <span data-ttu-id="f16dc-294">確認您看到 hello 下列表示成功驗證：**結果： 成功**</span><span class="sxs-lookup"><span data-stu-id="f16dc-294">Confirm that you see hello following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="f16dc-295">此指令碼會驗證 hello 簽章者鏈結，向上 toohello Thales 根金鑰。</span><span class="sxs-lookup"><span data-stu-id="f16dc-295">This script validates hello signer chain up toohello Thales root key.</span></span> <span data-ttu-id="f16dc-296">此根金鑰的 hello 雜湊內嵌於 hello 指令碼，且其值必須為**59178a47 de508c3f 291277ee 184f46c4 f1d9c639**。</span><span class="sxs-lookup"><span data-stu-id="f16dc-296">hello hash of this root key is embedded in hello script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="f16dc-297">您也可以確認此值分別造訪 hello [Thales 網站](http://www.thalesesec.com/)。</span><span class="sxs-lookup"><span data-stu-id="f16dc-297">You can also confirm this value separately by visiting hello [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="f16dc-298">您現在準備好 toocreate 新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f16dc-298">You’re now ready toocreate a new key.</span></span>

### <a name="step-35-create-a-new-key"></a><span data-ttu-id="f16dc-299">步驟 3.5：建立新的金鑰</span><span class="sxs-lookup"><span data-stu-id="f16dc-299">Step 3.5: Create a new key</span></span>
<span data-ttu-id="f16dc-300">產生的金鑰使用 hello Thales **generatekey**程式。</span><span class="sxs-lookup"><span data-stu-id="f16dc-300">Generate a key by using hello Thales **generatekey** program.</span></span>

<span data-ttu-id="f16dc-301">執行下列命令 toogenerate hello 按鍵 hello:</span><span class="sxs-lookup"><span data-stu-id="f16dc-301">Run hello following command toogenerate hello key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="f16dc-302">當您執行此命令時，請使用下列指示：</span><span class="sxs-lookup"><span data-stu-id="f16dc-302">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="f16dc-303">hello 參數*保護*toohello 值必須設定**模組**，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f16dc-303">hello parameter *protect* must be set toohello value **module**, as shown.</span></span> <span data-ttu-id="f16dc-304">這會建立受模組保護的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f16dc-304">This creates a module-protected key.</span></span> <span data-ttu-id="f16dc-305">hello BYOK 工具組不支援 OCS 保護的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f16dc-305">hello BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="f16dc-306">取代 hello 值*contosokey* hello **ident**和**contosokey**與任何字串值。</span><span class="sxs-lookup"><span data-stu-id="f16dc-306">Replace hello value of *contosokey* for hello **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="f16dc-307">toominimize 系統管理負擔並降低 hello 風險的錯誤，我們建議您使用相同的兩個值的 hello。</span><span class="sxs-lookup"><span data-stu-id="f16dc-307">toominimize administrative overheads and reduce hello risk of errors, we recommend that you use hello same value for both.</span></span> <span data-ttu-id="f16dc-308">hello **ident**值必須包含數字、 虛線和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="f16dc-308">hello **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="f16dc-309">hello 的 pubexp 保留空白 （預設值） 在此範例中，但您可以指定特定的值。</span><span class="sxs-lookup"><span data-stu-id="f16dc-309">hello pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="f16dc-310">如需詳細資訊，請參閱 hello Thales 文件。</span><span class="sxs-lookup"><span data-stu-id="f16dc-310">For more information, see hello Thales documentation.</span></span>

<span data-ttu-id="f16dc-311">此命令會使用名稱開頭為您的 %NFAST_KMDATA%\local 資料夾中建立信號化金鑰檔案**key_simple_**，後面接著 hello **ident** hello 命令中指定。</span><span class="sxs-lookup"><span data-stu-id="f16dc-311">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by hello **ident** that was specified in hello command.</span></span> <span data-ttu-id="f16dc-312">例如：**key_simple_contosokey**。</span><span class="sxs-lookup"><span data-stu-id="f16dc-312">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="f16dc-313">此檔案包含已加密的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f16dc-313">This file contains an encrypted key.</span></span>

<span data-ttu-id="f16dc-314">在安全的位置備份此語彙基元化金鑰檔案。</span><span class="sxs-lookup"><span data-stu-id="f16dc-314">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f16dc-315">當您稍後將傳輸您的金鑰 tooAzure 金鑰保存庫時，Microsoft 無法將此金鑰後 tooyou，因此是極為重要，您的金鑰和安全園地安全地備份。</span><span class="sxs-lookup"><span data-stu-id="f16dc-315">When you later transfer your key tooAzure Key Vault, Microsoft cannot export this key back tooyou so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="f16dc-316">如需備份金鑰的指引及最佳作法，請連絡 Thales。</span><span class="sxs-lookup"><span data-stu-id="f16dc-316">Contact Thales for guidance and best practices for backing up your key.</span></span>
>
>

<span data-ttu-id="f16dc-317">您會立即準備 tootransfer 您金鑰的 tooAzure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="f16dc-317">You are now ready tootransfer your key tooAzure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="f16dc-318">步驟 4：準備要傳輸的金鑰</span><span class="sxs-lookup"><span data-stu-id="f16dc-318">Step 4: Prepare your key for transfer</span></span>
<span data-ttu-id="f16dc-319">第四個步驟中，請勿 hello hello 中斷連線的工作站上，下列程序。</span><span class="sxs-lookup"><span data-stu-id="f16dc-319">For this fourth step, do hello following procedures on hello disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="f16dc-320">步驟 4.1：使用降低權限建立金鑰的複本</span><span class="sxs-lookup"><span data-stu-id="f16dc-320">Step 4.1: Create a copy of your key with reduced permissions</span></span>

<span data-ttu-id="f16dc-321">開啟新的命令提示字元，變更 hello 目前的目錄 toohello 位置您解壓縮 hello BYOK zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="f16dc-321">Open a new command prompt and change hello current directory toohello location where you unzipped hello BYOK zip file.</span></span> <span data-ttu-id="f16dc-322">tooreduce hello 權限，在您的金鑰，請從命令提示字元上執行 hello 下列程式碼，根據您的地理區域或 Azure 的執行個體的其中一個：</span><span class="sxs-lookup"><span data-stu-id="f16dc-322">tooreduce hello permissions on your key, from a command prompt, run one of hello following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="f16dc-323">北美洲：</span><span class="sxs-lookup"><span data-stu-id="f16dc-323">For North America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="f16dc-324">歐洲：</span><span class="sxs-lookup"><span data-stu-id="f16dc-324">For Europe:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="f16dc-325">亞洲：</span><span class="sxs-lookup"><span data-stu-id="f16dc-325">For Asia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="f16dc-326">拉丁美洲：</span><span class="sxs-lookup"><span data-stu-id="f16dc-326">For Latin America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="f16dc-327">日本：</span><span class="sxs-lookup"><span data-stu-id="f16dc-327">For Japan:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="f16dc-328">韓國︰</span><span class="sxs-lookup"><span data-stu-id="f16dc-328">For Korea:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* <span data-ttu-id="f16dc-329">澳大利亞：</span><span class="sxs-lookup"><span data-stu-id="f16dc-329">For Australia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="f16dc-330">如[Azure 政府](https://azure.microsoft.com/features/gov/)，它會使用的 Azure hello 美國政府執行個體：</span><span class="sxs-lookup"><span data-stu-id="f16dc-330">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="f16dc-331">美國政府國防部：</span><span class="sxs-lookup"><span data-stu-id="f16dc-331">For US Government DOD:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* <span data-ttu-id="f16dc-332">針對加拿大：</span><span class="sxs-lookup"><span data-stu-id="f16dc-332">For Canada:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="f16dc-333">針對德國：</span><span class="sxs-lookup"><span data-stu-id="f16dc-333">For Germany:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="f16dc-334">針對印度︰</span><span class="sxs-lookup"><span data-stu-id="f16dc-334">For India:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

<span data-ttu-id="f16dc-335">當您執行此命令時，取代*contosokey* hello 與相同的值中指定**步驟 3.5： 建立新的金鑰**從 hello[產生您的金鑰](#step-3-generate-your-key)步驟。</span><span class="sxs-lookup"><span data-stu-id="f16dc-335">When you run this command, replace *contosokey* with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="f16dc-336">系統會詢問 tooplug 您安全園地系統管理的卡片。</span><span class="sxs-lookup"><span data-stu-id="f16dc-336">You are asked tooplug in your security world admin cards.</span></span>

<span data-ttu-id="f16dc-337">Hello 命令完成時，您會看到**結果： 成功**hello 降低權限金鑰副本 hello 名為 key_xferacId_ 的檔案，而且<contosokey>。</span><span class="sxs-lookup"><span data-stu-id="f16dc-337">When hello command completes, you see **Result: SUCCESS** and hello copy of your key with reduced permissions are in hello file named key_xferacId_<contosokey>.</span></span>

<span data-ttu-id="f16dc-338">您可能會檢查 hello ACL 使用下列命令使用 hello Thales 公用程式：</span><span class="sxs-lookup"><span data-stu-id="f16dc-338">You may inspects hello ACLS using following commands using hello Thales utilities:</span></span>

* <span data-ttu-id="f16dc-339">aclprint.py：</span><span class="sxs-lookup"><span data-stu-id="f16dc-339">aclprint.py:</span></span>

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="f16dc-340">kmfile-dump.exe：</span><span class="sxs-lookup"><span data-stu-id="f16dc-340">kmfile-dump.exe:</span></span>

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="f16dc-341">當您執行這些命令時，取代 contosokey 以相同的值中指定的 hello**步驟 3.5： 建立新的金鑰**從 hello[產生您的金鑰](#step-3-generate-your-key)步驟。</span><span class="sxs-lookup"><span data-stu-id="f16dc-341">When you run these commands, replace contosokey with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="f16dc-342">步驟 4.2：使用 Microsoft 的金鑰交換金鑰來加密您的金鑰</span><span class="sxs-lookup"><span data-stu-id="f16dc-342">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>
<span data-ttu-id="f16dc-343">執行下列命令，根據您的地理區域或 Azure 的執行個體的 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="f16dc-343">Run one of hello following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="f16dc-344">北美洲：</span><span class="sxs-lookup"><span data-stu-id="f16dc-344">For North America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="f16dc-345">歐洲：</span><span class="sxs-lookup"><span data-stu-id="f16dc-345">For Europe:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="f16dc-346">亞洲：</span><span class="sxs-lookup"><span data-stu-id="f16dc-346">For Asia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="f16dc-347">拉丁美洲：</span><span class="sxs-lookup"><span data-stu-id="f16dc-347">For Latin America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="f16dc-348">日本：</span><span class="sxs-lookup"><span data-stu-id="f16dc-348">For Japan:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="f16dc-349">韓國︰</span><span class="sxs-lookup"><span data-stu-id="f16dc-349">For Korea:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="f16dc-350">澳大利亞：</span><span class="sxs-lookup"><span data-stu-id="f16dc-350">For Australia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="f16dc-351">如[Azure 政府](https://azure.microsoft.com/features/gov/)，它會使用的 Azure hello 美國政府執行個體：</span><span class="sxs-lookup"><span data-stu-id="f16dc-351">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="f16dc-352">美國政府國防部：</span><span class="sxs-lookup"><span data-stu-id="f16dc-352">For US Government DOD:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="f16dc-353">針對加拿大：</span><span class="sxs-lookup"><span data-stu-id="f16dc-353">For Canada:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="f16dc-354">針對德國：</span><span class="sxs-lookup"><span data-stu-id="f16dc-354">For Germany:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="f16dc-355">針對印度︰</span><span class="sxs-lookup"><span data-stu-id="f16dc-355">For India:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="f16dc-356">當您執行此命令時，請使用下列指示：</span><span class="sxs-lookup"><span data-stu-id="f16dc-356">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="f16dc-357">取代*contosokey*用 toogenerate hello 索引鍵中的 hello 識別碼**步驟 3.5： 建立新的金鑰**從 hello[產生您的金鑰](#step-3-generate-your-key)步驟。</span><span class="sxs-lookup"><span data-stu-id="f16dc-357">Replace *contosokey* with hello identifier that you used toogenerate hello key in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="f16dc-358">取代*SubscriptionID* hello hello 包含金鑰保存庫的 Azure 訂用帳戶 id。</span><span class="sxs-lookup"><span data-stu-id="f16dc-358">Replace *SubscriptionID* with hello ID of hello Azure subscription that contains your key vault.</span></span> <span data-ttu-id="f16dc-359">擷取此值先前在**步驟 1.2： 取得您的 Azure 訂用帳戶 ID**從 hello[準備連線網際網路的工作站](#step-1-prepare-your-internet-connected-workstation)步驟。</span><span class="sxs-lookup"><span data-stu-id="f16dc-359">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from hello [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="f16dc-360">以用於輸出檔案名稱的標籤取代 *ContosoFirstHSMKey*。</span><span class="sxs-lookup"><span data-stu-id="f16dc-360">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="f16dc-361">當成功完成時，它會顯示**結果： 成功**，而且具有下列名稱的 hello hello 目前資料夾中沒有新的檔案： KeyTransferPackage-*ContosoFirstHSMkey*.byok</span><span class="sxs-lookup"><span data-stu-id="f16dc-361">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in hello current folder that has hello following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a><span data-ttu-id="f16dc-362">步驟 4.3： 複製您金鑰傳輸封裝 toohello 連線網際網路的工作站</span><span class="sxs-lookup"><span data-stu-id="f16dc-362">Step 4.3: Copy your key transfer package toohello Internet-connected workstation</span></span>
<span data-ttu-id="f16dc-363">使用從 hello 上一個步驟 (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour 連線網際網路的工作站的 USB 磁碟機或其他可攜式儲存裝置 toocopy hello 輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="f16dc-363">Use a USB drive or other portable storage toocopy hello output file from hello previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a><span data-ttu-id="f16dc-364">步驟 5： 傳送您的金鑰 tooAzure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="f16dc-364">Step 5: Transfer your key tooAzure Key Vault</span></span>
<span data-ttu-id="f16dc-365">最後一個步驟中，在 hello 連線網際網路的工作站上，使用 hello [Add-azurekeyvaultkey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload hello 金鑰傳輸封裝，您所複製的 hello 中斷連線的工作站 toohello Azure 金鑰保存庫 HSM:</span><span class="sxs-lookup"><span data-stu-id="f16dc-365">For this final step, on hello Internet-connected workstation, use hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload hello key transfer package that you copied from hello disconnected workstation toohello Azure Key Vault HSM:</span></span>

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

<span data-ttu-id="f16dc-366">如果 hello 上傳成功時，您會看到您剛才加入的 hello 金鑰顯示的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="f16dc-366">If hello upload is successful, you see displayed hello properties of hello key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f16dc-367">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f16dc-367">Next steps</span></span>
<span data-ttu-id="f16dc-368">您現在可以在您的金鑰保存庫中使用這個受 HSM 保護的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f16dc-368">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="f16dc-369">如需詳細資訊，請參閱 hello**如果您想 toouse 硬體安全性模組 (HSM)** > 一節中 hello[開始使用 Azure 金鑰保存庫](key-vault-get-started.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="f16dc-369">For more information, see hello **If you want toouse a hardware security module (HSM)** section in hello [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>
