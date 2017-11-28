---
title: "如何為 Azure 金鑰保存庫產生並傳輸受 HSM 保護的金鑰 | Microsoft Docs"
description: "使用這份文件協助您規劃、產生，並傳輸受 HSM 保護的金鑰，以搭配 Azure 金鑰保存庫使用。 也稱為 BYOK 或「攜帶您自己的金鑰」。"
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
ms.openlocfilehash: 5dbee1221f64045c64fecb344de1e03b2183dfb1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-generate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="65aa9-104">如何為 Azure 金鑰保存庫產生並傳輸受 HSM 保護的金鑰</span><span class="sxs-lookup"><span data-stu-id="65aa9-104">How to generate and transfer HSM-protected keys for Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="65aa9-105">簡介</span><span class="sxs-lookup"><span data-stu-id="65aa9-105">Introduction</span></span>
<span data-ttu-id="65aa9-106">為了加強保證，當您使用 Azure 金鑰保存庫時，您可以在硬體安全模組 (HSM) 中匯入或產生無需離開 HSM 界限的金鑰。</span><span class="sxs-lookup"><span data-stu-id="65aa9-106">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="65aa9-107">此案例通常稱為 *自備金鑰*或 BYOK。</span><span class="sxs-lookup"><span data-stu-id="65aa9-107">This scenario is often referred to as *bring your own key*, or BYOK.</span></span> <span data-ttu-id="65aa9-108">HSM 已通過 FIPS 140-2 Level 2 驗證。</span><span class="sxs-lookup"><span data-stu-id="65aa9-108">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="65aa9-109">Azure 金鑰保存庫使用 Thales nShield 系列 HSM 來保護您的金鑰。</span><span class="sxs-lookup"><span data-stu-id="65aa9-109">Azure Key Vault uses Thales nShield family of HSMs to protect your keys.</span></span>

<span data-ttu-id="65aa9-110">使用本主題中的資訊，協助您規劃、產生然後傳送自己受 HSM 保護的金鑰，以搭配使用 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="65aa9-110">Use the information in this topic to help you plan for, generate, and then transfer your own HSM-protected keys to use with Azure Key Vault.</span></span>

<span data-ttu-id="65aa9-111">此功能不適用於 Azure China。</span><span class="sxs-lookup"><span data-stu-id="65aa9-111">This functionality is not available for Azure China.</span></span>

> [!NOTE]
> <span data-ttu-id="65aa9-112">如需 Azure 金鑰保存庫的詳細資訊，請參閱 [什麼是 Azure 金鑰保存庫？](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="65aa9-112">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
>
> <span data-ttu-id="65aa9-113">如需入門教學課程，其中包括建立受 HSM 保護之金鑰的金鑰保存庫，請參閱 [開始使用 Azure 金鑰保存庫](key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="65aa9-113">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>
>
>

<span data-ttu-id="65aa9-114">有關產生及透過網際網路傳輸受 HSM 保護之金鑰的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="65aa9-114">More information about generating and transferring an HSM-protected key over the Internet:</span></span>

* <span data-ttu-id="65aa9-115">您可以從離線工作站產生金鑰，可減少受攻擊面。</span><span class="sxs-lookup"><span data-stu-id="65aa9-115">You generate the key from an offline workstation, which reduces the attack surface.</span></span>
* <span data-ttu-id="65aa9-116">此金鑰利用金鑰交換金鑰 (KEK) 加密，且加密狀態會維持到金鑰傳輸至 Azure 金鑰保存庫 HSM 為止。</span><span class="sxs-lookup"><span data-stu-id="65aa9-116">The key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred to the Azure Key Vault HSMs.</span></span> <span data-ttu-id="65aa9-117">只有加密版本的金鑰會離開原始工作站。</span><span class="sxs-lookup"><span data-stu-id="65aa9-117">Only the encrypted version of your key leaves the original workstation.</span></span>
* <span data-ttu-id="65aa9-118">工具組會在將您的金鑰繫結至 Azure 金鑰保存庫安全世界的租用戶金鑰上設定屬性。</span><span class="sxs-lookup"><span data-stu-id="65aa9-118">The toolset sets properties on your tenant key that binds your key to the Azure Key Vault security world.</span></span> <span data-ttu-id="65aa9-119">因此，在 Azure 金鑰保存庫 HSM 接收和解密您的金鑰之後，只有這些 HSM 可使用它。</span><span class="sxs-lookup"><span data-stu-id="65aa9-119">So after the Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="65aa9-120">無法匯出您的金鑰。</span><span class="sxs-lookup"><span data-stu-id="65aa9-120">Your key cannot be exported.</span></span> <span data-ttu-id="65aa9-121">這個繫結是由 Thales HSM 強制執行。</span><span class="sxs-lookup"><span data-stu-id="65aa9-121">This binding is enforced by the Thales HSMs.</span></span>
* <span data-ttu-id="65aa9-122">用來解密金鑰的金鑰互換金鑰 (KEK) 產生於 Azure 金鑰保存庫 HSM 內且不可匯出。</span><span class="sxs-lookup"><span data-stu-id="65aa9-122">The Key Exchange Key (KEK) that is used to encrypt your key is generated inside the Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="65aa9-123">HSM 會強制執行使 HSM 外部沒有明確版本的 KEK。</span><span class="sxs-lookup"><span data-stu-id="65aa9-123">The HSMs enforce that there can be no clear version of the KEK outside the HSMs.</span></span> <span data-ttu-id="65aa9-124">此外，工具組包含了來自 Thales 的證明，代表 KEK 不可匯出，且產生於 Thales 製造的正版 HSM 內部。</span><span class="sxs-lookup"><span data-stu-id="65aa9-124">In addition, the toolset includes attestation from Thales that the KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="65aa9-125">工具組包含了來自 Thales 的證明，代表 Azure 金鑰保存庫安全世界也產生於 Thales 製造的正版 HSM 上。</span><span class="sxs-lookup"><span data-stu-id="65aa9-125">The toolset includes attestation from Thales that the Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="65aa9-126">這個證書向您證明 Microsoft 正在使用正版硬體。</span><span class="sxs-lookup"><span data-stu-id="65aa9-126">This attestation proves to you that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="65aa9-127">Microsoft 會在每個地理區域使用不同的 KEK 和不同的「安全世界」。</span><span class="sxs-lookup"><span data-stu-id="65aa9-127">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="65aa9-128">這種區隔可確保您的金鑰只能用在您加密它時所在區域中的資料中心。</span><span class="sxs-lookup"><span data-stu-id="65aa9-128">This separation ensures that your key can be used only in data centers in the region in which you encrypted it.</span></span> <span data-ttu-id="65aa9-129">例如，來自歐洲客戶的金鑰不能在北美或亞洲的資料中心使用。</span><span class="sxs-lookup"><span data-stu-id="65aa9-129">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="65aa9-130">Thales HSM 和 Microsoft 服務的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="65aa9-130">More information about Thales HSMs and Microsoft services</span></span>
<span data-ttu-id="65aa9-131">Thales e-Security 是金融服務的資料加密和網路安全性解決方案、高科技、製造業、政府和技術部門的領先全域提供者。</span><span class="sxs-lookup"><span data-stu-id="65aa9-131">Thales e-Security is a leading global provider of data encryption and cyber security solutions to the financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="65aa9-132">透過保護企業及政府資訊的 40 年追蹤記錄，目前規模最大的五間能源和航太公司中有四間都在使用 Thales 解決方案。</span><span class="sxs-lookup"><span data-stu-id="65aa9-132">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of the five largest energy and aerospace companies.</span></span> <span data-ttu-id="65aa9-133">另外還有 22 個北大西洋公約組織國家也在使用他們的解決方案，而且全世界有超過 80% 的付款交易都受其保障。</span><span class="sxs-lookup"><span data-stu-id="65aa9-133">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="65aa9-134">Microsoft 已與 thales 合作增強 HSM 的開發狀態。</span><span class="sxs-lookup"><span data-stu-id="65aa9-134">Microsoft has collaborated with Thales to enhance the state of art for HSMs.</span></span> <span data-ttu-id="65aa9-135">這些增強內容可讓您取得裝載服務的典型優勢，而且不用放棄金鑰的控制權。</span><span class="sxs-lookup"><span data-stu-id="65aa9-135">These enhancements enable you to get the typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="65aa9-136">具體而言，這些增強內容可讓 Microsoft 管理 HSM，如此您就不必費心管理。</span><span class="sxs-lookup"><span data-stu-id="65aa9-136">Specifically, these enhancements let Microsoft manage the HSMs so that you do not have to.</span></span> <span data-ttu-id="65aa9-137">做為雲端服務，Azure 金鑰保存庫無需通知就會相應增加，以符合組織的使用尖峰。</span><span class="sxs-lookup"><span data-stu-id="65aa9-137">As a cloud service, Azure Key Vault scales up at short notice to meet your organization’s usage spikes.</span></span> <span data-ttu-id="65aa9-138">在此同時，您的金鑰也會在 Microsoft 的 HSM 內部受到保護：您可以保留金鑰生命週期的控制權，因為您會產生金鑰並將它傳輸給 Microsoft 的 HSM。</span><span class="sxs-lookup"><span data-stu-id="65aa9-138">At the same time, your key is protected inside Microsoft’s HSMs: You retain control over the key lifecycle because you generate the key and transfer it to Microsoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="65aa9-139">實作 Azure 金鑰保存庫的自備金鑰 (BYOK)</span><span class="sxs-lookup"><span data-stu-id="65aa9-139">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>
<span data-ttu-id="65aa9-140">如果您將產生您自己受 HSM 保護的金鑰，然後將它傳輸到 Azure 金鑰保存庫，請使用下列資訊和程序—自備金鑰 (BYOK) 案例。</span><span class="sxs-lookup"><span data-stu-id="65aa9-140">Use the following information and procedures if you will generate your own HSM-protected key and then transfer it to Azure Key Vault—the bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="65aa9-141">BYOK 的必要條件</span><span class="sxs-lookup"><span data-stu-id="65aa9-141">Prerequisites for BYOK</span></span>
<span data-ttu-id="65aa9-142">請參閱下表的必要條件清單以取得 Azure 金鑰保存庫的自備金鑰 (BYOK)。</span><span class="sxs-lookup"><span data-stu-id="65aa9-142">See the following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="65aa9-143">需求</span><span class="sxs-lookup"><span data-stu-id="65aa9-143">Requirement</span></span> | <span data-ttu-id="65aa9-144">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="65aa9-144">More information</span></span> |
| --- | --- |
| <span data-ttu-id="65aa9-145">Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="65aa9-145">A subscription to Azure</span></span> |<span data-ttu-id="65aa9-146">若要建立 Azure 金鑰保存庫，您需要 Azure 訂用帳戶： [註冊免費試用](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="65aa9-146">To create an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="65aa9-147">可支援受 HSM 保護之金鑰的 Azure 金鑰保存庫進階服務層</span><span class="sxs-lookup"><span data-stu-id="65aa9-147">The Azure Key Vault Premium service tier to support HSM-protected keys</span></span> |<span data-ttu-id="65aa9-148">如需 Azure 金鑰保存庫的服務層和功能的詳細資訊，請參閱 [Azure 金鑰保存庫價格](https://azure.microsoft.com/pricing/details/key-vault/) 網站。</span><span class="sxs-lookup"><span data-stu-id="65aa9-148">For more information about the service tiers and capabilities for Azure Key Vault, see the [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="65aa9-149">Thales HSM、智慧卡和支援軟體</span><span class="sxs-lookup"><span data-stu-id="65aa9-149">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="65aa9-150">您必須存取 Thales 硬體安全模組和 Thales HSM 的基本操作知識。</span><span class="sxs-lookup"><span data-stu-id="65aa9-150">You must have access to a Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="65aa9-151">請參閱 [Thales 硬體安全模組](https://www.thales-esecurity.com/msrms/buy) 以取得相容模型的清單，或者如果您沒有 HSM，請購買 HSM。</span><span class="sxs-lookup"><span data-stu-id="65aa9-151">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for the list of compatible models, or to purchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="65aa9-152">下列的硬體和軟體︰</span><span class="sxs-lookup"><span data-stu-id="65aa9-152">The following hardware and software:</span></span><ol><li><span data-ttu-id="65aa9-153">離線 x64 工作站、至少為 Windows 7 的 Windows 作業系統，以及至少為 11.50 版的 Thales nShield 軟體。</span><span class="sxs-lookup"><span data-stu-id="65aa9-153">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="65aa9-154">如果此工作站執行 Windows 7，您必須[安裝 Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe)。</span><span class="sxs-lookup"><span data-stu-id="65aa9-154">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="65aa9-155">連線至網際網路且 Windows 作業系統至少為 Windows 7 的工作站，並已安裝至少為 [1.1.0 版的 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="65aa9-155">A workstation that is connected to the Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](/powershell/azure/overview) **minimum version 1.1.0** installed.</span></span></li><li><span data-ttu-id="65aa9-156">至少有 16 MB 可用空間的 USB 磁碟機或其他可攜式儲存裝置。</span><span class="sxs-lookup"><span data-stu-id="65aa9-156">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="65aa9-157">基於安全性理由，建議第一個工作站不要連線到網路。</span><span class="sxs-lookup"><span data-stu-id="65aa9-157">For security reasons, we recommend that the first workstation is not connected to a network.</span></span> <span data-ttu-id="65aa9-158">不過，在程式設計方面並不強迫採取這項建議。</span><span class="sxs-lookup"><span data-stu-id="65aa9-158">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="65aa9-159">請注意，在接下來的指示中，此工作站稱為中斷連線的工作站。</span><span class="sxs-lookup"><span data-stu-id="65aa9-159">Note that in the instructions that follow, this workstation is referred to as the disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="65aa9-160">此外，如果您的租用戶金鑰適用於生產網路，建議您使用第二個另外的工作站來下載工具組和上傳租用戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="65aa9-160">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation to download the toolset and upload the tenant key.</span></span> <span data-ttu-id="65aa9-161">但如果只是測試，您可以直接使用第一個工作站。</span><span class="sxs-lookup"><span data-stu-id="65aa9-161">But for testing purposes, you can use the same workstation as the first one.</span></span><br/><br/><span data-ttu-id="65aa9-162">請注意，在接下來的指示中，此第二個工作站稱為網際網路連線的工作站。</span><span class="sxs-lookup"><span data-stu-id="65aa9-162">Note that in the instructions that follow, this second workstation is referred to as the Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-to-azure-key-vault-hsm"></a><span data-ttu-id="65aa9-163">產生金鑰並將其傳輸至 Azure 金鑰保存庫 HSM</span><span class="sxs-lookup"><span data-stu-id="65aa9-163">Generate and transfer your key to Azure Key Vault HSM</span></span>
<span data-ttu-id="65aa9-164">您將使用下列五個步驟產生金鑰並將其傳輸至 Azure 金鑰保存庫 HSM：</span><span class="sxs-lookup"><span data-stu-id="65aa9-164">You will use the following five steps to generate and transfer your key to an Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="65aa9-165">步驟 1：準備網際網路連線的工作站</span><span class="sxs-lookup"><span data-stu-id="65aa9-165">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="65aa9-166">步驟 2：準備中斷連線的工作站</span><span class="sxs-lookup"><span data-stu-id="65aa9-166">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="65aa9-167">步驟 3：產生您的金鑰</span><span class="sxs-lookup"><span data-stu-id="65aa9-167">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="65aa9-168">步驟 4：準備要傳輸的金鑰</span><span class="sxs-lookup"><span data-stu-id="65aa9-168">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="65aa9-169">步驟 5：將金鑰傳輸至 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="65aa9-169">Step 5: Transfer your key to Azure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="65aa9-170">步驟 1：準備網際網路連線的工作站</span><span class="sxs-lookup"><span data-stu-id="65aa9-170">Step 1: Prepare your Internet-connected workstation</span></span>
<span data-ttu-id="65aa9-171">在第一個步驟中，請在連線到網際網路的工作站上執行下列程序。</span><span class="sxs-lookup"><span data-stu-id="65aa9-171">For this first step, do the following procedures on your workstation that is connected to the Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="65aa9-172">步驟 1.1：安裝 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="65aa9-172">Step 1.1: Install Azure PowerShell</span></span>
<span data-ttu-id="65aa9-173">從網際網路連線的工作站，下載並安裝 Azure PowerShell 模組，其包含 cmdlet 以管理 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="65aa9-173">From the Internet-connected workstation, download and install the Azure PowerShell module that includes the cmdlets to manage Azure Key Vault.</span></span> <span data-ttu-id="65aa9-174">這需要得最低版本為 0.8.13。</span><span class="sxs-lookup"><span data-stu-id="65aa9-174">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="65aa9-175">如需安裝指示，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="65aa9-175">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="65aa9-176">步驟 1.2：取得您的 Azure 訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="65aa9-176">Step 1.2: Get your Azure subscription ID</span></span>
<span data-ttu-id="65aa9-177">使用下列命令開始 Azure PowerShell 工作階段，並登入您的 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="65aa9-177">Start an Azure PowerShell session and sign in to your Azure account by using the following command:</span></span>

        Add-AzureAccount
<span data-ttu-id="65aa9-178">在快顯瀏覽器視窗中，輸入您的 Azure 帳戶使用者名稱與密碼。</span><span class="sxs-lookup"><span data-stu-id="65aa9-178">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="65aa9-179">然後，使用 [Get-azuresubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) 命令：</span><span class="sxs-lookup"><span data-stu-id="65aa9-179">Then, use the [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span></span>

        Get-AzureSubscription
<span data-ttu-id="65aa9-180">從輸出中，找出您將用於 Azure 金鑰保存庫的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="65aa9-180">From the output, locate the ID for the subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="65aa9-181">您稍後將需要此訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="65aa9-181">You will need this subscription ID later.</span></span>

<span data-ttu-id="65aa9-182">請勿關閉 Azure PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="65aa9-182">Do not close the Azure PowerShell window.</span></span>

### <a name="step-13-download-the-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="65aa9-183">步驟 1.3：下載 Azure 金鑰保存庫的 BYOK 工具組</span><span class="sxs-lookup"><span data-stu-id="65aa9-183">Step 1.3: Download the BYOK toolset for Azure Key Vault</span></span>
<span data-ttu-id="65aa9-184">移至 Microsoft 下載中心並為您的地理區域或 Azure 執行個體 [下載 Azure 金鑰保存庫 BYOK 工具組](http://www.microsoft.com/download/details.aspx?id=45345) 。</span><span class="sxs-lookup"><span data-stu-id="65aa9-184">Go to the Microsoft Download Center and [download the Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="65aa9-185">使用下列資訊來識別要下載封裝雜湊與其對應的 SHA-256 封裝雜湊︰</span><span class="sxs-lookup"><span data-stu-id="65aa9-185">Use the following information to identify the package name to download and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="65aa9-186">**美國：**</span><span class="sxs-lookup"><span data-stu-id="65aa9-186">**United States:**</span></span>

<span data-ttu-id="65aa9-187">KeyVault-BYOK-Tools-UnitedStates.zip</span><span class="sxs-lookup"><span data-stu-id="65aa9-187">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="65aa9-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span><span class="sxs-lookup"><span data-stu-id="65aa9-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span></span>

- - -
<span data-ttu-id="65aa9-189">**歐洲︰**</span><span class="sxs-lookup"><span data-stu-id="65aa9-189">**Europe:**</span></span>

<span data-ttu-id="65aa9-190">KeyVault-BYOK-Tools-Europe.zip</span><span class="sxs-lookup"><span data-stu-id="65aa9-190">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="65aa9-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span><span class="sxs-lookup"><span data-stu-id="65aa9-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span></span>

- - -
<span data-ttu-id="65aa9-192">**亞洲︰**</span><span class="sxs-lookup"><span data-stu-id="65aa9-192">**Asia:**</span></span>

<span data-ttu-id="65aa9-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span><span class="sxs-lookup"><span data-stu-id="65aa9-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="65aa9-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span><span class="sxs-lookup"><span data-stu-id="65aa9-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span></span>

- - -
<span data-ttu-id="65aa9-195">**拉丁美洲︰**</span><span class="sxs-lookup"><span data-stu-id="65aa9-195">**Latin America:**</span></span>

<span data-ttu-id="65aa9-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span><span class="sxs-lookup"><span data-stu-id="65aa9-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="65aa9-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span><span class="sxs-lookup"><span data-stu-id="65aa9-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span></span>

- - -
<span data-ttu-id="65aa9-198">**日本︰**</span><span class="sxs-lookup"><span data-stu-id="65aa9-198">**Japan:**</span></span>

<span data-ttu-id="65aa9-199">KeyVault-BYOK-Tools-Japan.zip</span><span class="sxs-lookup"><span data-stu-id="65aa9-199">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="65aa9-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span><span class="sxs-lookup"><span data-stu-id="65aa9-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span></span>

- - -
<span data-ttu-id="65aa9-201">**韓國：**</span><span class="sxs-lookup"><span data-stu-id="65aa9-201">**Korea:**</span></span>

<span data-ttu-id="65aa9-202">KeyVault-BYOK-Tools-Korea.zip</span><span class="sxs-lookup"><span data-stu-id="65aa9-202">KeyVault-BYOK-Tools-Korea.zip</span></span>

<span data-ttu-id="65aa9-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span><span class="sxs-lookup"><span data-stu-id="65aa9-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span></span>

- - -
<span data-ttu-id="65aa9-204">**澳大利亞：**</span><span class="sxs-lookup"><span data-stu-id="65aa9-204">**Australia:**</span></span>

<span data-ttu-id="65aa9-205">KeyVault-BYOK-Tools-Australia.zip</span><span class="sxs-lookup"><span data-stu-id="65aa9-205">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="65aa9-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span><span class="sxs-lookup"><span data-stu-id="65aa9-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span></span>

- - -
[<span data-ttu-id="65aa9-207">**Azure Government:**</span><span class="sxs-lookup"><span data-stu-id="65aa9-207">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="65aa9-208">KeyVault-BYOK-Tools-USGovCloud.zip</span><span class="sxs-lookup"><span data-stu-id="65aa9-208">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="65aa9-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span><span class="sxs-lookup"><span data-stu-id="65aa9-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span></span>

- - -
<span data-ttu-id="65aa9-210">**美國政府國防部：**</span><span class="sxs-lookup"><span data-stu-id="65aa9-210">**US Government DOD:**</span></span>

<span data-ttu-id="65aa9-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span><span class="sxs-lookup"><span data-stu-id="65aa9-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span></span>

<span data-ttu-id="65aa9-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span><span class="sxs-lookup"><span data-stu-id="65aa9-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span></span>

- - -
<span data-ttu-id="65aa9-213">**加拿大：**</span><span class="sxs-lookup"><span data-stu-id="65aa9-213">**Canada:**</span></span>

<span data-ttu-id="65aa9-214">KeyVault-BYOK-Tools-Canada.zip</span><span class="sxs-lookup"><span data-stu-id="65aa9-214">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="65aa9-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span><span class="sxs-lookup"><span data-stu-id="65aa9-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span></span>

- - -
<span data-ttu-id="65aa9-216">**德國：**</span><span class="sxs-lookup"><span data-stu-id="65aa9-216">**Germany:**</span></span>

<span data-ttu-id="65aa9-217">KeyVault-BYOK-Tools-Germany.zip</span><span class="sxs-lookup"><span data-stu-id="65aa9-217">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="65aa9-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span><span class="sxs-lookup"><span data-stu-id="65aa9-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span></span>

- - -
<span data-ttu-id="65aa9-219">**印度：**</span><span class="sxs-lookup"><span data-stu-id="65aa9-219">**India:**</span></span>

<span data-ttu-id="65aa9-220">KeyVault-BYOK-Tools-India.zip</span><span class="sxs-lookup"><span data-stu-id="65aa9-220">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="65aa9-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span><span class="sxs-lookup"><span data-stu-id="65aa9-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span></span>

- - -
<span data-ttu-id="65aa9-222">**英國：**</span><span class="sxs-lookup"><span data-stu-id="65aa9-222">**United Kingdom:**</span></span>

<span data-ttu-id="65aa9-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span><span class="sxs-lookup"><span data-stu-id="65aa9-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="65aa9-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span><span class="sxs-lookup"><span data-stu-id="65aa9-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span></span>

- - -

<span data-ttu-id="65aa9-225">若要驗證您已下載之 BYOK 工具組的完整性，請從您的 Azure PowerShell 工作階段，使用 [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="65aa9-225">To validate the integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use the [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

    Get-FileHash KeyVault-BYOK-Tools-*.zip

<span data-ttu-id="65aa9-226">工具組包含下列各項：</span><span class="sxs-lookup"><span data-stu-id="65aa9-226">The toolset includes the following:</span></span>

* <span data-ttu-id="65aa9-227">具有以 **BYOK-KEK-pkg-**</span><span class="sxs-lookup"><span data-stu-id="65aa9-227">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="65aa9-228">具有以 **BYOK-SecurityWorld-pkg-**</span><span class="sxs-lookup"><span data-stu-id="65aa9-228">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="65aa9-229">名為 **verifykeypackage.py** 的 python 指令碼。</span><span class="sxs-lookup"><span data-stu-id="65aa9-229">A python script named **verifykeypackage.py.**</span></span>
* <span data-ttu-id="65aa9-230">名為 **KeyTransferRemote.exe** 的命令列可執行檔和相關聯的 DLL。</span><span class="sxs-lookup"><span data-stu-id="65aa9-230">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="65aa9-231">Visual C++ 可轉散發套件，名為 **vcredist_x64.exe**。</span><span class="sxs-lookup"><span data-stu-id="65aa9-231">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="65aa9-232">將封裝複製到 USB 磁碟機或其他可攜式儲存裝置。</span><span class="sxs-lookup"><span data-stu-id="65aa9-232">Copy the package to a USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="65aa9-233">步驟 2：準備中斷連線的工作站</span><span class="sxs-lookup"><span data-stu-id="65aa9-233">Step 2: Prepare your disconnected workstation</span></span>
<span data-ttu-id="65aa9-234">在第二個步驟中，請在未連線到網路 (網際網路或內部網路) 的工作站上執行下列程序。</span><span class="sxs-lookup"><span data-stu-id="65aa9-234">For this second step, do the following procedures on the workstation that is not connected to a network (either the Internet or your internal network).</span></span>

### <a name="step-21-prepare-the-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="65aa9-235">步驟 2.1：準備使用 Thales HSM 的中斷連線工作站</span><span class="sxs-lookup"><span data-stu-id="65aa9-235">Step 2.1: Prepare the disconnected workstation with Thales HSM</span></span>
<span data-ttu-id="65aa9-236">在 Windows 電腦上安裝 nCipher (Thales) 支援軟體，然後將 Thales HSM 附加至該電腦。</span><span class="sxs-lookup"><span data-stu-id="65aa9-236">Install the nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM to that computer.</span></span>

<span data-ttu-id="65aa9-237">確定 Thales 工具位於您的路徑 (**%nfast_home%\bin**)。</span><span class="sxs-lookup"><span data-stu-id="65aa9-237">Ensure that the Thales tools are in your path (**%nfast_home%\bin**).</span></span> <span data-ttu-id="65aa9-238">例如，輸入下列內容：</span><span class="sxs-lookup"><span data-stu-id="65aa9-238">For example, type the following:</span></span>

        set PATH=%PATH%;"%nfast_home%\bin"

<span data-ttu-id="65aa9-239">如需詳細資訊，請參閱 Thales HSM 內附的使用者指南。</span><span class="sxs-lookup"><span data-stu-id="65aa9-239">For more information, see the user guide included with the Thales HSM.</span></span>

### <a name="step-22-install-the-byok-toolset-on-the-disconnected-workstation"></a><span data-ttu-id="65aa9-240">步驟 2.2：在中斷連線的工作站上安裝 BYOK 工具組</span><span class="sxs-lookup"><span data-stu-id="65aa9-240">Step 2.2: Install the BYOK toolset on the disconnected workstation</span></span>
<span data-ttu-id="65aa9-241">從 USB 磁碟機或其他可攜式儲存裝置複製 BYOK 工具組封裝，然後執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="65aa9-241">Copy the BYOK toolset package from the USB drive or other portable storage, and then do the following:</span></span>

1. <span data-ttu-id="65aa9-242">將檔案從下載的封裝解壓縮至任何資料夾。</span><span class="sxs-lookup"><span data-stu-id="65aa9-242">Extract the files from the downloaded package into any folder.</span></span>
2. <span data-ttu-id="65aa9-243">從該資料夾執行 vcredist_x64.exe。</span><span class="sxs-lookup"><span data-stu-id="65aa9-243">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="65aa9-244">遵循指示以安裝 Visual Studio 2013 的 Visual C++ 執行階段元件。</span><span class="sxs-lookup"><span data-stu-id="65aa9-244">Follow the instructions to the install the Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="65aa9-245">步驟 3：產生您的金鑰</span><span class="sxs-lookup"><span data-stu-id="65aa9-245">Step 3: Generate your key</span></span>
<span data-ttu-id="65aa9-246">在第三個步驟中，請在中斷連線的工作站上執行下列程序。</span><span class="sxs-lookup"><span data-stu-id="65aa9-246">For this third step, do the following procedures on the disconnected workstation.</span></span> <span data-ttu-id="65aa9-247">若要完成此步驟，您的 HSM 必須是初始化模式。</span><span class="sxs-lookup"><span data-stu-id="65aa9-247">To complete this step your HSM must be in initialization mode.</span></span> 


### <a name="step-31-change-the-hsm-mode-to-i"></a><span data-ttu-id="65aa9-248">步驟 3.1︰將 HSM 模式變更為 I</span><span class="sxs-lookup"><span data-stu-id="65aa9-248">Step 3.1: Change the HSM mode to 'I'</span></span>
<span data-ttu-id="65aa9-249">如果您使用 Thales nShield Edge，則變更模式︰1。</span><span class="sxs-lookup"><span data-stu-id="65aa9-249">If you are using Thales nShield Edge, to change the mode: 1.</span></span> <span data-ttu-id="65aa9-250">使用 [Mode (模式)] 按鈕來反白顯示必要的模式。</span><span class="sxs-lookup"><span data-stu-id="65aa9-250">Use the Mode button to highlight the required mode.</span></span> <span data-ttu-id="65aa9-251">2.</span><span class="sxs-lookup"><span data-stu-id="65aa9-251">2.</span></span> <span data-ttu-id="65aa9-252">在幾秒鐘之內，按住 [Clear (清除)] 按鈕幾秒鐘。</span><span class="sxs-lookup"><span data-stu-id="65aa9-252">Within a few seconds, press and hold the Clear button for a couple of seconds.</span></span> <span data-ttu-id="65aa9-253">如果模式變更，新模式的 LED 會停止閃爍，並保持亮燈。</span><span class="sxs-lookup"><span data-stu-id="65aa9-253">If the mode changes, the new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="65aa9-254">狀態 LED 可能會不規則閃爍幾秒鐘的時間，當裝置就緒後則規則地閃爍。</span><span class="sxs-lookup"><span data-stu-id="65aa9-254">The Status LED might flash irregularly for a few seconds and then flashes regularly when the device is ready.</span></span> <span data-ttu-id="65aa9-255">否則，裝置會維持目前的模式，適當的模式 LED 會亮起。</span><span class="sxs-lookup"><span data-stu-id="65aa9-255">Otherwise, the device remains in the current mode, with the appropriate mode LED lit.</span></span>

### <a name="step-32-create-a-security-world"></a><span data-ttu-id="65aa9-256">步驟 3.2：建立安全世界</span><span class="sxs-lookup"><span data-stu-id="65aa9-256">Step 3.2: Create a security world</span></span>
<span data-ttu-id="65aa9-257">啟動命令提示字元並執行 Thales new-world 程式。</span><span class="sxs-lookup"><span data-stu-id="65aa9-257">Start a command prompt and run the Thales new-world program.</span></span>

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

<span data-ttu-id="65aa9-258">此程式會在 %NFAST_KMDATA%\local\world 建立**安全世界**檔案，並對應到 C:\ProgramData\nCipher\Key Management Data\local 資料夾。</span><span class="sxs-lookup"><span data-stu-id="65aa9-258">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds to the C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="65aa9-259">您可以使用不同的值進行仲裁，但是在我們的範例中，系統會提示您輸入三個空白的卡片和其個別的 pin。</span><span class="sxs-lookup"><span data-stu-id="65aa9-259">You can use different values for the quorum but in our example, you’re prompted to enter three blank cards and pins for each one.</span></span> <span data-ttu-id="65aa9-260">然後，任兩張卡片可提供安全世界的完整存取權。</span><span class="sxs-lookup"><span data-stu-id="65aa9-260">Then, any two cards give full access to the security world.</span></span> <span data-ttu-id="65aa9-261">這些卡片將成為新安全世界的 **系統管理員卡組** 。</span><span class="sxs-lookup"><span data-stu-id="65aa9-261">These cards become the **Administrator Card Set** for the new security world.</span></span>

<span data-ttu-id="65aa9-262">然後執行以下動作：</span><span class="sxs-lookup"><span data-stu-id="65aa9-262">Then do the following:</span></span>

* <span data-ttu-id="65aa9-263">備份世界檔案。</span><span class="sxs-lookup"><span data-stu-id="65aa9-263">Back up the world file.</span></span> <span data-ttu-id="65aa9-264">保障和保護世界檔案、系統管理員卡及其 pin，並確定沒有一個人可存取多張卡。</span><span class="sxs-lookup"><span data-stu-id="65aa9-264">Secure and protect the world file, the Administrator Cards, and their pins, and make sure that no single person has access to more than one card.</span></span>

### <a name="step-33-change-the-hsm-mode-to-o"></a><span data-ttu-id="65aa9-265">步驟 3.3︰將 HSM 模式變更為 O</span><span class="sxs-lookup"><span data-stu-id="65aa9-265">Step 3.3: Change the HSM mode to 'O'</span></span>
<span data-ttu-id="65aa9-266">如果您使用 Thales nShield Edge，則變更模式︰1。</span><span class="sxs-lookup"><span data-stu-id="65aa9-266">If you are using Thales nShield Edge, to change the mode: 1.</span></span> <span data-ttu-id="65aa9-267">使用 [Mode (模式)] 按鈕來反白顯示必要的模式。</span><span class="sxs-lookup"><span data-stu-id="65aa9-267">Use the Mode button to highlight the required mode.</span></span> <span data-ttu-id="65aa9-268">2.</span><span class="sxs-lookup"><span data-stu-id="65aa9-268">2.</span></span> <span data-ttu-id="65aa9-269">在幾秒鐘之內，按住 [Clear (清除)] 按鈕幾秒鐘。</span><span class="sxs-lookup"><span data-stu-id="65aa9-269">Within a few seconds, press and hold the Clear button for a couple of seconds.</span></span> <span data-ttu-id="65aa9-270">如果模式變更，新模式的 LED 會停止閃爍，並保持亮燈。</span><span class="sxs-lookup"><span data-stu-id="65aa9-270">If the mode changes, the new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="65aa9-271">狀態 LED 可能會不規則閃爍幾秒鐘的時間，當裝置就緒後則規則地閃爍。</span><span class="sxs-lookup"><span data-stu-id="65aa9-271">The Status LED might flash irregularly for a few seconds and then flashes regularly when the device is ready.</span></span> <span data-ttu-id="65aa9-272">否則，裝置會維持目前的模式，適當的模式 LED 會亮起。</span><span class="sxs-lookup"><span data-stu-id="65aa9-272">Otherwise, the device remains in the current mode, with the appropriate mode LED lit.</span></span>


### <a name="step-34-validate-the-downloaded-package"></a><span data-ttu-id="65aa9-273">步驟 3.4：驗證下載的封裝</span><span class="sxs-lookup"><span data-stu-id="65aa9-273">Step 3.4: Validate the downloaded package</span></span>
<span data-ttu-id="65aa9-274">此步驟為選擇性但建議使用，以便您可以驗證下列項目：</span><span class="sxs-lookup"><span data-stu-id="65aa9-274">This step is optional but recommended so that you can validate the following:</span></span>

* <span data-ttu-id="65aa9-275">工具組中包含的金鑰交換金鑰已從正版 Thales HSM 中產生。</span><span class="sxs-lookup"><span data-stu-id="65aa9-275">The Key Exchange Key that is included in the toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="65aa9-276">工具組中包含的安全世界雜湊已在正版 Thales HSM 中產生。</span><span class="sxs-lookup"><span data-stu-id="65aa9-276">The hash of the Security World that is included in the toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="65aa9-277">金鑰交換金鑰不可匯出。</span><span class="sxs-lookup"><span data-stu-id="65aa9-277">The Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="65aa9-278">若要驗證下載的封裝，HSM 必須連線、開啟電源，而且必須在其上具有安全世界 (如同您剛才所建立的那一個)。</span><span class="sxs-lookup"><span data-stu-id="65aa9-278">To validate the downloaded package, the HSM must be connected, powered on, and must have a security world on it (such as the one you’ve just created).</span></span>
>
>

<span data-ttu-id="65aa9-279">驗證下載的封裝：</span><span class="sxs-lookup"><span data-stu-id="65aa9-279">To validate the downloaded package:</span></span>

1. <span data-ttu-id="65aa9-280">根據您的地理區域或 Azure 的執行個體輸入下列其中一個區域，以執行 verifykeypackage.py 指令碼：</span><span class="sxs-lookup"><span data-stu-id="65aa9-280">Run the verifykeypackage.py script by typing one of the following, depending on your geographic region or instance of Azure:</span></span>

   * <span data-ttu-id="65aa9-281">北美洲：</span><span class="sxs-lookup"><span data-stu-id="65aa9-281">For North America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="65aa9-282">歐洲：</span><span class="sxs-lookup"><span data-stu-id="65aa9-282">For Europe:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="65aa9-283">亞洲：</span><span class="sxs-lookup"><span data-stu-id="65aa9-283">For Asia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="65aa9-284">拉丁美洲：</span><span class="sxs-lookup"><span data-stu-id="65aa9-284">For Latin America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="65aa9-285">日本：</span><span class="sxs-lookup"><span data-stu-id="65aa9-285">For Japan:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="65aa9-286">韓國︰</span><span class="sxs-lookup"><span data-stu-id="65aa9-286">For Korea:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * <span data-ttu-id="65aa9-287">澳大利亞：</span><span class="sxs-lookup"><span data-stu-id="65aa9-287">For Australia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="65aa9-288">對於 [Azure Government](https://azure.microsoft.com/features/gov/)，它會使用美國政府的 Azure 執行個體：</span><span class="sxs-lookup"><span data-stu-id="65aa9-288">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="65aa9-289">美國政府國防部：</span><span class="sxs-lookup"><span data-stu-id="65aa9-289">For US Government DOD:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * <span data-ttu-id="65aa9-290">針對加拿大：</span><span class="sxs-lookup"><span data-stu-id="65aa9-290">For Canada:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="65aa9-291">針對德國：</span><span class="sxs-lookup"><span data-stu-id="65aa9-291">For Germany:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="65aa9-292">針對印度︰</span><span class="sxs-lookup"><span data-stu-id="65aa9-292">For India:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > <span data-ttu-id="65aa9-293">Thales 軟體包含 %NFAST_HOME%\python\bin 中的 python</span><span class="sxs-lookup"><span data-stu-id="65aa9-293">The Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     >
     >
2. <span data-ttu-id="65aa9-294">確認您看到下列訊息，表示驗證成功： **Result: SUCCESS**</span><span class="sxs-lookup"><span data-stu-id="65aa9-294">Confirm that you see the following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="65aa9-295">此指令碼會驗證簽章者鏈結到 Thales 根金鑰。</span><span class="sxs-lookup"><span data-stu-id="65aa9-295">This script validates the signer chain up to the Thales root key.</span></span> <span data-ttu-id="65aa9-296">此根金鑰的雜湊內嵌於指令碼中，而且其值應為 **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**。</span><span class="sxs-lookup"><span data-stu-id="65aa9-296">The hash of this root key is embedded in the script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="65aa9-297">您也可以造訪 [Thales 網站](http://www.thalesesec.com/)以另行確認此值。</span><span class="sxs-lookup"><span data-stu-id="65aa9-297">You can also confirm this value separately by visiting the [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="65aa9-298">您現在可以開始建立新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="65aa9-298">You’re now ready to create a new key.</span></span>

### <a name="step-35-create-a-new-key"></a><span data-ttu-id="65aa9-299">步驟 3.5：建立新的金鑰</span><span class="sxs-lookup"><span data-stu-id="65aa9-299">Step 3.5: Create a new key</span></span>
<span data-ttu-id="65aa9-300">使用 Thales **generatekey** 程式產生金鑰。</span><span class="sxs-lookup"><span data-stu-id="65aa9-300">Generate a key by using the Thales **generatekey** program.</span></span>

<span data-ttu-id="65aa9-301">執行下列命令來產生金鑰：</span><span class="sxs-lookup"><span data-stu-id="65aa9-301">Run the following command to generate the key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="65aa9-302">當您執行此命令時，請使用下列指示：</span><span class="sxs-lookup"><span data-stu-id="65aa9-302">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="65aa9-303">參數 *protect* 必須如所示般設定為值 **module**。</span><span class="sxs-lookup"><span data-stu-id="65aa9-303">The parameter *protect* must be set to the value **module**, as shown.</span></span> <span data-ttu-id="65aa9-304">這會建立受模組保護的金鑰。</span><span class="sxs-lookup"><span data-stu-id="65aa9-304">This creates a module-protected key.</span></span> <span data-ttu-id="65aa9-305">BYOK 工具組不支援受 OCS 保護的金鑰。</span><span class="sxs-lookup"><span data-stu-id="65aa9-305">The BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="65aa9-306">以任意字串值取代 **ident** 和 **plainname** 的 *contosokey* 值。</span><span class="sxs-lookup"><span data-stu-id="65aa9-306">Replace the value of *contosokey* for the **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="65aa9-307">若要將系統管理負擔降至最低並減少錯誤的風險，建議您同時對兩者使用相同的值。</span><span class="sxs-lookup"><span data-stu-id="65aa9-307">To minimize administrative overheads and reduce the risk of errors, we recommend that you use the same value for both.</span></span> <span data-ttu-id="65aa9-308">**Ident** 值只能包含數字、連字號和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="65aa9-308">The **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="65aa9-309">在這個範例中，Pubexp 保留空白 (預設值)，但是您可以指定特定值。</span><span class="sxs-lookup"><span data-stu-id="65aa9-309">The pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="65aa9-310">如需詳細資訊，請參閱 Thales 文件。</span><span class="sxs-lookup"><span data-stu-id="65aa9-310">For more information, see the Thales documentation.</span></span>

<span data-ttu-id="65aa9-311">此命令會在您的 %NFAST_KMDATA%\local 資料夾建立名稱開頭為 **key_simple_** 的語彙基元化金鑰檔案，後面接著在命令中指定的 **ident**。</span><span class="sxs-lookup"><span data-stu-id="65aa9-311">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by the **ident** that was specified in the command.</span></span> <span data-ttu-id="65aa9-312">例如：**key_simple_contosokey**。</span><span class="sxs-lookup"><span data-stu-id="65aa9-312">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="65aa9-313">此檔案包含已加密的金鑰。</span><span class="sxs-lookup"><span data-stu-id="65aa9-313">This file contains an encrypted key.</span></span>

<span data-ttu-id="65aa9-314">在安全的位置備份此語彙基元化金鑰檔案。</span><span class="sxs-lookup"><span data-stu-id="65aa9-314">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65aa9-315">當您稍後將您的金鑰傳輸至 Azure 金鑰保存庫時，Microsoft 就無法將此金鑰匯出給您，因此，請務必安全地備份您的金鑰和安全世界。</span><span class="sxs-lookup"><span data-stu-id="65aa9-315">When you later transfer your key to Azure Key Vault, Microsoft cannot export this key back to you so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="65aa9-316">如需備份金鑰的指引及最佳作法，請連絡 Thales。</span><span class="sxs-lookup"><span data-stu-id="65aa9-316">Contact Thales for guidance and best practices for backing up your key.</span></span>
>
>

<span data-ttu-id="65aa9-317">您現在已準備好將金鑰傳輸至 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="65aa9-317">You are now ready to transfer your key to Azure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="65aa9-318">步驟 4：準備要傳輸的金鑰</span><span class="sxs-lookup"><span data-stu-id="65aa9-318">Step 4: Prepare your key for transfer</span></span>
<span data-ttu-id="65aa9-319">在第四個步驟中，請在中斷連線的工作站上執行下列程序。</span><span class="sxs-lookup"><span data-stu-id="65aa9-319">For this fourth step, do the following procedures on the disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="65aa9-320">步驟 4.1：使用降低權限建立金鑰的複本</span><span class="sxs-lookup"><span data-stu-id="65aa9-320">Step 4.1: Create a copy of your key with reduced permissions</span></span>

<span data-ttu-id="65aa9-321">開啟新的命令提示字元，並將目前的目錄變更為解壓縮 BYOK ZIP 檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="65aa9-321">Open a new command prompt and change the current directory to the location where you unzipped the BYOK zip file.</span></span> <span data-ttu-id="65aa9-322">若要減少金鑰的權限，請從命令提示字元，根據您的地理區域或 Azure 執行個體，執行下列其中一個區域：</span><span class="sxs-lookup"><span data-stu-id="65aa9-322">To reduce the permissions on your key, from a command prompt, run one of the following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="65aa9-323">北美洲：</span><span class="sxs-lookup"><span data-stu-id="65aa9-323">For North America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="65aa9-324">歐洲：</span><span class="sxs-lookup"><span data-stu-id="65aa9-324">For Europe:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="65aa9-325">亞洲：</span><span class="sxs-lookup"><span data-stu-id="65aa9-325">For Asia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="65aa9-326">拉丁美洲：</span><span class="sxs-lookup"><span data-stu-id="65aa9-326">For Latin America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="65aa9-327">日本：</span><span class="sxs-lookup"><span data-stu-id="65aa9-327">For Japan:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="65aa9-328">韓國︰</span><span class="sxs-lookup"><span data-stu-id="65aa9-328">For Korea:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* <span data-ttu-id="65aa9-329">澳大利亞：</span><span class="sxs-lookup"><span data-stu-id="65aa9-329">For Australia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="65aa9-330">對於 [Azure Government](https://azure.microsoft.com/features/gov/)，它會使用美國政府的 Azure 執行個體：</span><span class="sxs-lookup"><span data-stu-id="65aa9-330">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="65aa9-331">美國政府國防部：</span><span class="sxs-lookup"><span data-stu-id="65aa9-331">For US Government DOD:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* <span data-ttu-id="65aa9-332">針對加拿大：</span><span class="sxs-lookup"><span data-stu-id="65aa9-332">For Canada:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="65aa9-333">針對德國：</span><span class="sxs-lookup"><span data-stu-id="65aa9-333">For Germany:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="65aa9-334">針對印度︰</span><span class="sxs-lookup"><span data-stu-id="65aa9-334">For India:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

<span data-ttu-id="65aa9-335">當您執行此命令時，請以您從[產生您的金鑰](#step-3-generate-your-key)步驟的**步驟 3.5：建立新的金鑰**中指定的相同值取代 *contosokey*。</span><span class="sxs-lookup"><span data-stu-id="65aa9-335">When you run this command, replace *contosokey* with the same value you specified in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="65aa9-336">系統會要求您插入您的安全世界系統管理員卡。</span><span class="sxs-lookup"><span data-stu-id="65aa9-336">You are asked to plug in your security world admin cards.</span></span>

<span data-ttu-id="65aa9-337">此命令完成時，您會看到 **Result: SUCCESS**，而降低權限的金鑰複本會在名為 key_xferacId_<contosokey> 的檔案中。</span><span class="sxs-lookup"><span data-stu-id="65aa9-337">When the command completes, you see **Result: SUCCESS** and the copy of your key with reduced permissions are in the file named key_xferacId_<contosokey>.</span></span>

<span data-ttu-id="65aa9-338">您可使用 Thales 公用程式，以下列命令檢查 ACLS：</span><span class="sxs-lookup"><span data-stu-id="65aa9-338">You may inspects the ACLS using following commands using the Thales utilities:</span></span>

* <span data-ttu-id="65aa9-339">aclprint.py：</span><span class="sxs-lookup"><span data-stu-id="65aa9-339">aclprint.py:</span></span>

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="65aa9-340">kmfile-dump.exe：</span><span class="sxs-lookup"><span data-stu-id="65aa9-340">kmfile-dump.exe:</span></span>

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="65aa9-341">當您執行這些命令時，請以您從[產生您的金鑰](#step-3-generate-your-key)步驟的**步驟 3.5：建立新的金鑰**指定的相同值取代 contosokey。</span><span class="sxs-lookup"><span data-stu-id="65aa9-341">When you run these commands, replace contosokey with the same value you specified in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="65aa9-342">步驟 4.2：使用 Microsoft 的金鑰交換金鑰來加密您的金鑰</span><span class="sxs-lookup"><span data-stu-id="65aa9-342">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>
<span data-ttu-id="65aa9-343">根據您的地理區域或 Azure 執行個體，執行下列其中一個命令：</span><span class="sxs-lookup"><span data-stu-id="65aa9-343">Run one of the following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="65aa9-344">北美洲：</span><span class="sxs-lookup"><span data-stu-id="65aa9-344">For North America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65aa9-345">歐洲：</span><span class="sxs-lookup"><span data-stu-id="65aa9-345">For Europe:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65aa9-346">亞洲：</span><span class="sxs-lookup"><span data-stu-id="65aa9-346">For Asia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65aa9-347">拉丁美洲：</span><span class="sxs-lookup"><span data-stu-id="65aa9-347">For Latin America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65aa9-348">日本：</span><span class="sxs-lookup"><span data-stu-id="65aa9-348">For Japan:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65aa9-349">韓國︰</span><span class="sxs-lookup"><span data-stu-id="65aa9-349">For Korea:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65aa9-350">澳大利亞：</span><span class="sxs-lookup"><span data-stu-id="65aa9-350">For Australia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65aa9-351">對於 [Azure Government](https://azure.microsoft.com/features/gov/)，它會使用美國政府的 Azure 執行個體：</span><span class="sxs-lookup"><span data-stu-id="65aa9-351">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65aa9-352">美國政府國防部：</span><span class="sxs-lookup"><span data-stu-id="65aa9-352">For US Government DOD:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65aa9-353">針對加拿大：</span><span class="sxs-lookup"><span data-stu-id="65aa9-353">For Canada:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65aa9-354">針對德國：</span><span class="sxs-lookup"><span data-stu-id="65aa9-354">For Germany:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65aa9-355">針對印度︰</span><span class="sxs-lookup"><span data-stu-id="65aa9-355">For India:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="65aa9-356">當您執行此命令時，請使用下列指示：</span><span class="sxs-lookup"><span data-stu-id="65aa9-356">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="65aa9-357">請以您在*產生您的金鑰*步驟的**步驟 3.5：建立新的金鑰**中用來產生金鑰的識別碼取代 [contosokey](#step-3-generate-your-key) 。</span><span class="sxs-lookup"><span data-stu-id="65aa9-357">Replace *contosokey* with the identifier that you used to generate the key in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="65aa9-358">以包含金鑰保存庫的 Azure 訂用帳戶識別碼取代 *SubscriptionID* 。</span><span class="sxs-lookup"><span data-stu-id="65aa9-358">Replace *SubscriptionID* with the ID of the Azure subscription that contains your key vault.</span></span> <span data-ttu-id="65aa9-359">您先前已在 **步驟 1.2：取得 Azure 訂用帳戶識別碼** 中從 [準備網際網路連線的工作站](#step-1-prepare-your-internet-connected-workstation) 步驟擷取過這個值。</span><span class="sxs-lookup"><span data-stu-id="65aa9-359">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from the [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="65aa9-360">以用於輸出檔案名稱的標籤取代 *ContosoFirstHSMKey*。</span><span class="sxs-lookup"><span data-stu-id="65aa9-360">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="65aa9-361">當此動作成功完成時，會顯示 **Result: SUCCESS** ，而且目前的資料夾中會有新的檔案，其名稱如下：KeyTransferPackage-*ContosoFirstHSMkey*.byok</span><span class="sxs-lookup"><span data-stu-id="65aa9-361">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in the current folder that has the following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-43-copy-your-key-transfer-package-to-the-internet-connected-workstation"></a><span data-ttu-id="65aa9-362">步驟 4.3：將金鑰傳輸封裝複製到網際網路連線的工作站</span><span class="sxs-lookup"><span data-stu-id="65aa9-362">Step 4.3: Copy your key transfer package to the Internet-connected workstation</span></span>
<span data-ttu-id="65aa9-363">使用 USB 磁碟機或其他可攜式儲存裝置，將上一個步驟的輸出檔案 (KeyTransferPackage-ContosoFirstHSMkey.byok) 複製到網際網路連線的工作站。</span><span class="sxs-lookup"><span data-stu-id="65aa9-363">Use a USB drive or other portable storage to copy the output file from the previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) to your Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-to-azure-key-vault"></a><span data-ttu-id="65aa9-364">步驟 5：將金鑰傳輸至 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="65aa9-364">Step 5: Transfer your key to Azure Key Vault</span></span>
<span data-ttu-id="65aa9-365">針對這最後一個步驟，在連線到網際網路的工作站上，使用 [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) Cmdlet，將您從已中斷連線的工作站複製的金鑰傳輸套件上傳到「Azure 金鑰保存庫 HSM」：</span><span class="sxs-lookup"><span data-stu-id="65aa9-365">For this final step, on the Internet-connected workstation, use the [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet to upload the key transfer package that you copied from the disconnected workstation to the Azure Key Vault HSM:</span></span>

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

<span data-ttu-id="65aa9-366">如果上傳成功，就會顯示您剛才加入之金鑰的屬性。</span><span class="sxs-lookup"><span data-stu-id="65aa9-366">If the upload is successful, you see displayed the properties of the key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65aa9-367">後續步驟</span><span class="sxs-lookup"><span data-stu-id="65aa9-367">Next steps</span></span>
<span data-ttu-id="65aa9-368">您現在可以在您的金鑰保存庫中使用這個受 HSM 保護的金鑰。</span><span class="sxs-lookup"><span data-stu-id="65aa9-368">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="65aa9-369">如需詳細資訊，請參閱 **開始使用 Azure 金鑰保存庫** 教學課程中的 [如果您想要使用硬體安全模組 (HSM)](key-vault-get-started.md) 一節。</span><span class="sxs-lookup"><span data-stu-id="65aa9-369">For more information, see the **If you want to use a hardware security module (HSM)** section in the [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>
