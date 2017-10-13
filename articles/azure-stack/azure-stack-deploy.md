---
title: "Azure Stack 開發套件部署先決條件 | Microsoft Docs"
description: "檢視 Azure Stack 開發套件 (雲端操作員) 的環境和硬體需求。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 32a21d9b-ee42-417d-8e54-98a7f90f7311
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/11/2017
ms.author: erikje
ms.openlocfilehash: 73e7efb7d789fe12846d68066c0927bb123831a2
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="azure-stack-deployment-prerequisites"></a><span data-ttu-id="b3f0f-103">Azure Stack 部署先決條件</span><span class="sxs-lookup"><span data-stu-id="b3f0f-103">Azure Stack deployment prerequisites</span></span>

<span data-ttu-id="b3f0f-104">適用於：Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="b3f0f-104">*Applies to: Azure Stack Development Kit*</span></span>

<span data-ttu-id="b3f0f-105">部署 [Azure Stack 開發套件](azure-stack-poc.md)之前，請先確定您的電腦符合下列需求：</span><span class="sxs-lookup"><span data-stu-id="b3f0f-105">Before you deploy [Azure Stack Development Kit](azure-stack-poc.md), make sure your computer meets the following requirements:</span></span>


## <a name="hardware"></a><span data-ttu-id="b3f0f-106">硬體</span><span class="sxs-lookup"><span data-stu-id="b3f0f-106">Hardware</span></span>
| <span data-ttu-id="b3f0f-107">元件</span><span class="sxs-lookup"><span data-stu-id="b3f0f-107">Component</span></span> | <span data-ttu-id="b3f0f-108">最小值</span><span class="sxs-lookup"><span data-stu-id="b3f0f-108">Minimum</span></span> | <span data-ttu-id="b3f0f-109">建議</span><span class="sxs-lookup"><span data-stu-id="b3f0f-109">Recommended</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b3f0f-110">磁碟機：作業系統</span><span class="sxs-lookup"><span data-stu-id="b3f0f-110">Disk drives: Operating System</span></span> |<span data-ttu-id="b3f0f-111">1 個 OS 磁碟 (SSD 或 HDD)，最少有 200 GB 供系統磁碟分割使用</span><span class="sxs-lookup"><span data-stu-id="b3f0f-111">1 OS disk with minimum of 200 GB available for system partition (SSD or HDD)</span></span> |<span data-ttu-id="b3f0f-112">1 個 OS 磁碟 (SSD 或 HDD)，最少有 200 GB 供系統磁碟分割使用</span><span class="sxs-lookup"><span data-stu-id="b3f0f-112">1 OS disk with minimum of 200 GB available for system partition (SSD or HDD)</span></span> |
| <span data-ttu-id="b3f0f-113">磁碟機：一般開發套件資料*</span><span class="sxs-lookup"><span data-stu-id="b3f0f-113">Disk drives: General development kit data*</span></span> |<span data-ttu-id="b3f0f-114">4 個磁碟。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-114">4 disks.</span></span> <span data-ttu-id="b3f0f-115">每個磁碟 (SSD 或 HDD) 提供最少 140 GB 的容量。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-115">Each disk provides a minimum of 140 GB of capacity (SSD or HDD).</span></span> <span data-ttu-id="b3f0f-116">將會使用所有可用的磁碟。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-116">All available disks will be used.</span></span> |<span data-ttu-id="b3f0f-117">4 個磁碟。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-117">4 disks.</span></span> <span data-ttu-id="b3f0f-118">每個磁碟 (SSD 或 HDD) 至少提供 250 GB 的容量。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-118">Each disk provides a minimum of 250 GB of capacity (SSD or HDD).</span></span> <span data-ttu-id="b3f0f-119">將會使用所有可用的磁碟。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-119">All available disks will be used.</span></span> |
| <span data-ttu-id="b3f0f-120">計算：CPU</span><span class="sxs-lookup"><span data-stu-id="b3f0f-120">Compute: CPU</span></span> |<span data-ttu-id="b3f0f-121">雙插槽：12 個實體核心 (總計)</span><span class="sxs-lookup"><span data-stu-id="b3f0f-121">Dual-Socket: 12 Physical Cores (total)</span></span> |<span data-ttu-id="b3f0f-122">雙插槽：16 個實體核心 (總計)</span><span class="sxs-lookup"><span data-stu-id="b3f0f-122">Dual-Socket: 16 Physical Cores (total)</span></span> |
| <span data-ttu-id="b3f0f-123">計算：記憶體</span><span class="sxs-lookup"><span data-stu-id="b3f0f-123">Compute: Memory</span></span> |<span data-ttu-id="b3f0f-124">96 GB RAM</span><span class="sxs-lookup"><span data-stu-id="b3f0f-124">96 GB RAM</span></span> |<span data-ttu-id="b3f0f-125">128 GB RAM (這是支援 PaaS 資源提供者的下限)。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-125">128 GB RAM (This is the minimum to support PaaS resource providers.)</span></span>|
| <span data-ttu-id="b3f0f-126">計算：BIOS</span><span class="sxs-lookup"><span data-stu-id="b3f0f-126">Compute: BIOS</span></span> |<span data-ttu-id="b3f0f-127">啟用 Hyper-V (支援 SLAT)</span><span class="sxs-lookup"><span data-stu-id="b3f0f-127">Hyper-V Enabled (with SLAT support)</span></span> |<span data-ttu-id="b3f0f-128">啟用 Hyper-V (支援 SLAT)</span><span class="sxs-lookup"><span data-stu-id="b3f0f-128">Hyper-V Enabled (with SLAT support)</span></span> |
| <span data-ttu-id="b3f0f-129">網路：NIC</span><span class="sxs-lookup"><span data-stu-id="b3f0f-129">Network: NIC</span></span> |<span data-ttu-id="b3f0f-130">NIC 所需的 Windows Server 2012 R2 憑證；不需特殊的功能</span><span class="sxs-lookup"><span data-stu-id="b3f0f-130">Windows Server 2012 R2 Certification required for NIC; no specialized features required</span></span> |<span data-ttu-id="b3f0f-131">NIC 所需的 Windows Server 2012 R2 憑證；不需特殊的功能</span><span class="sxs-lookup"><span data-stu-id="b3f0f-131">Windows Server 2012 R2 Certification required for NIC; no specialized features required</span></span> |
| <span data-ttu-id="b3f0f-132">HW 標誌憑證</span><span class="sxs-lookup"><span data-stu-id="b3f0f-132">HW logo certification</span></span> |[<span data-ttu-id="b3f0f-133">Windows Server 2012 R2 認證</span><span class="sxs-lookup"><span data-stu-id="b3f0f-133">Certified for Windows Server 2012 R2</span></span>](http://windowsservercatalog.com/results.aspx?&chtext=&cstext=&csttext=&chbtext=&bCatID=1333&cpID=0&avc=79&ava=0&avq=0&OR=1&PGS=25&ready=0) |[<span data-ttu-id="b3f0f-134">Windows Server 2012 R2 認證</span><span class="sxs-lookup"><span data-stu-id="b3f0f-134">Certified for Windows Server 2012 R2</span></span>](http://windowsservercatalog.com/results.aspx?&chtext=&cstext=&csttext=&chbtext=&bCatID=1333&cpID=0&avc=79&ava=0&avq=0&OR=1&PGS=25&ready=0) |

<span data-ttu-id="b3f0f-135">\*如果您打算從 Azure 新增許多[市集項目](azure-stack-download-azure-marketplace-item.md)，則您所需的容量將比這個建議的容量多。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-135">\*You will need more than this recommended capacity if you plan on adding many of the [marketplace items](azure-stack-download-azure-marketplace-item.md) from Azure.</span></span>

<span data-ttu-id="b3f0f-136">**資料磁碟機組態：**所有資料磁碟機都必須具有相同的類型 (全部都是 SAS 或全部都是 SATA) 和容量。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-136">**Data disk drive configuration:** All data drives must be of the same type (all SAS or all SATA) and capacity.</span></span> <span data-ttu-id="b3f0f-137">如果使用 SAS 磁碟機，則該磁碟機必須透過單一路徑連結 (不支援 MPIO 多重路徑)。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-137">If SAS disk drives are used, the disk drives must be attached via a single path (no MPIO, multi-path support is provided).</span></span>

<span data-ttu-id="b3f0f-138">**HBA 組態選項**</span><span class="sxs-lookup"><span data-stu-id="b3f0f-138">**HBA configuration options**</span></span>

* <span data-ttu-id="b3f0f-139">(慣用) 簡單 HBA</span><span class="sxs-lookup"><span data-stu-id="b3f0f-139">(Preferred) Simple HBA</span></span>
* <span data-ttu-id="b3f0f-140">RAID HBA – 介面卡必須設定為「穿通」模式</span><span class="sxs-lookup"><span data-stu-id="b3f0f-140">RAID HBA – Adapter must be configured in “pass through” mode</span></span>
* <span data-ttu-id="b3f0f-141">RAID HBA – 磁碟應設定為單一磁碟、RAID 0</span><span class="sxs-lookup"><span data-stu-id="b3f0f-141">RAID HBA – Disks should be configured as Single-Disk, RAID-0</span></span>

<span data-ttu-id="b3f0f-142">**支援的匯流排和媒體類型組合**</span><span class="sxs-lookup"><span data-stu-id="b3f0f-142">**Supported bus and media type combinations**</span></span>

* <span data-ttu-id="b3f0f-143">SATA HDD</span><span class="sxs-lookup"><span data-stu-id="b3f0f-143">SATA HDD</span></span>
* <span data-ttu-id="b3f0f-144">SAS HDD</span><span class="sxs-lookup"><span data-stu-id="b3f0f-144">SAS HDD</span></span>
* <span data-ttu-id="b3f0f-145">RAID HDD</span><span class="sxs-lookup"><span data-stu-id="b3f0f-145">RAID HDD</span></span>
* <span data-ttu-id="b3f0f-146">RAID SSD (如果媒體類型為未指定/不明\*)</span><span class="sxs-lookup"><span data-stu-id="b3f0f-146">RAID SSD (If the media type is unspecified/unknown\*)</span></span>
* <span data-ttu-id="b3f0f-147">SATA SSD + SATA HDD</span><span class="sxs-lookup"><span data-stu-id="b3f0f-147">SATA SSD + SATA HDD</span></span>
* <span data-ttu-id="b3f0f-148">SAS SSD + SAS HDD</span><span class="sxs-lookup"><span data-stu-id="b3f0f-148">SAS SSD + SAS HDD</span></span>

<span data-ttu-id="b3f0f-149">\* 不具備穿通功能的 RAID 控制器無法辨識媒體類型。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-149">\* RAID controllers without pass-through capability can’t recognize the media type.</span></span> <span data-ttu-id="b3f0f-150">這類控制站會將 SSD 和 HDD，皆標示為未指定。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-150">Such controllers will mark both HDD and SSD as Unspecified.</span></span> <span data-ttu-id="b3f0f-151">在此情況下，SSD 會當作永續性儲存體使用，而非快取裝置。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-151">In that case, the SSD will be used as persistent storage instead of caching devices.</span></span> <span data-ttu-id="b3f0f-152">因此，您可以在那些 SSD 上部署開發套件。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-152">Therefore, you can deploy the development kit on those SSDs.</span></span>

<span data-ttu-id="b3f0f-153">**範例 HBA**：傳遞模式中的 LSI 9207-8i、LSI-9300-8i 或 LSI-9265-8i</span><span class="sxs-lookup"><span data-stu-id="b3f0f-153">**Example HBAs**: LSI 9207-8i, LSI-9300-8i, or LSI-9265-8i in pass-through mode</span></span>

<span data-ttu-id="b3f0f-154">範例 OEM 設定可供使用。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-154">Sample OEM configurations are available.</span></span>

## <a name="operating-system"></a><span data-ttu-id="b3f0f-155">作業系統</span><span class="sxs-lookup"><span data-stu-id="b3f0f-155">Operating system</span></span>
|  | <span data-ttu-id="b3f0f-156">**需求**</span><span class="sxs-lookup"><span data-stu-id="b3f0f-156">**Requirements**</span></span> |
| --- | --- |
| <span data-ttu-id="b3f0f-157">**作業系統版本**</span><span class="sxs-lookup"><span data-stu-id="b3f0f-157">**OS Version**</span></span> |<span data-ttu-id="b3f0f-158">Windows Server 2012 R2 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-158">Windows Server 2012 R2 or later.</span></span> <span data-ttu-id="b3f0f-159">作業系統版本在部署開始前並不重要，因為您將會讓主機電腦開機進入 Azure Stack 安裝所包含的 VHD。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-159">The operating system version isn’t critical before the deployment starts, as you'll boot the host computer into the VHD that's included in the Azure Stack installation.</span></span> <span data-ttu-id="b3f0f-160">OS 和所有必要的修補程式都已經整合到該映像中。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-160">The OS and all required patches are already integrated into the image.</span></span> <span data-ttu-id="b3f0f-161">請勿使用任何金鑰來啟用開發套件中使用的任何 Windows Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-161">Don’t use any keys to activate any Windows Server instances used in the development kit.</span></span> |

## <a name="deployment-requirements-check-tool"></a><span data-ttu-id="b3f0f-162">部署需求檢查工具</span><span class="sxs-lookup"><span data-stu-id="b3f0f-162">Deployment requirements check tool</span></span>
<span data-ttu-id="b3f0f-163">安裝作業系統之後，您可以使用[適用於 Azure Stack 的部署檢查程式](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b)來確認您的硬體符合所有需求。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-163">After installing the operating system, you can use the [Deployment Checker for Azure Stack](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b) to confirm that your hardware meets all the requirements.</span></span>

## <a name="account-requirements"></a><span data-ttu-id="b3f0f-164">帳戶需求</span><span class="sxs-lookup"><span data-stu-id="b3f0f-164">Account requirements</span></span>
<span data-ttu-id="b3f0f-165">通常，您會在有網際網路連線能力的情況下部署開發套件，以便連線到 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-165">Typically, you deploy the development kit with internet connectivity, where you can connect to Microsoft Azure.</span></span> <span data-ttu-id="b3f0f-166">在此情況下，您必須設定 Azure Active Directory (Azure AD) 帳戶以部署開發套件。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-166">In this case, you must configure an Azure Active Directory (Azure AD) account to deploy the development kit.</span></span>

<span data-ttu-id="b3f0f-167">如果您的環境未連線到網際網路，或您不想要使用 Azure AD，則可以使用「Active Directory 同盟服務」(AD FS) 來部署 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-167">If your environment is not connected to the internet, or you don't want to use Azure AD, you can deploy Azure Stack by using Active Directory Federation Services (AD FS).</span></span> <span data-ttu-id="b3f0f-168">開發套件包含自己的 AD FS 和 Active Directory Domain Services 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-168">The development kit includes its own AD FS and Active Directory Domain Services instances.</span></span> <span data-ttu-id="b3f0f-169">如果使用這個選項來部署，就不需要事先設定帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-169">If you deploy by using this option, you don't have to set up accounts ahead of time.</span></span>

>[!NOTE]
<span data-ttu-id="b3f0f-170">如果您使用 AD FS 選項來部署，則必須重新部署 Azure Stack 以切換到 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-170">If you deploy by using the AD FS option, you must redeploy Azure Stack to switch to Azure AD.</span></span>

### <a name="azure-active-directory-accounts"></a><span data-ttu-id="b3f0f-171">Azure Active Directory 帳戶</span><span class="sxs-lookup"><span data-stu-id="b3f0f-171">Azure Active Directory accounts</span></span>
<span data-ttu-id="b3f0f-172">若要使用 Azure AD 帳戶來部署 Azure Stack，您必須在執行部署 PowerShell 指令碼之前，先備妥 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-172">To deploy Azure Stack by using an Azure AD account, you must prepare an Azure AD account before you run the deployment PowerShell script.</span></span> <span data-ttu-id="b3f0f-173">這個帳戶會成為 Azure AD 租用戶的「全域系統管理員」。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-173">This account becomes the Global Admin for the Azure AD tenant.</span></span> <span data-ttu-id="b3f0f-174">它可用來為與 Azure Active Directory 和「圖形 API」互動的所有 Azure Stack 服務佈建及委派應用程式和服務主體。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-174">It's used to provision and delegate applications and service principals for all Azure Stack services that interact with Azure Active Directory and Graph API.</span></span> <span data-ttu-id="b3f0f-175">它也用來作為預設提供者訂用帳戶 (您可以稍後變更此訂用帳戶) 的擁有者。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-175">It's also used as the owner of the default provider subscription (which you can later change).</span></span> <span data-ttu-id="b3f0f-176">您可以使用這個帳戶來登入 Azure Stack 系統的系統管理員入口網站。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-176">You can log in to your Azure Stack system’s administrator portal by using this account.</span></span>

1. <span data-ttu-id="b3f0f-177">建立至少是一個 Azure AD 之目錄系統管理員的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-177">Create an Azure AD account that is the directory administrator for at least one Azure AD.</span></span> <span data-ttu-id="b3f0f-178">如果您已經有一個這樣的帳戶，則可以使用該帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-178">If you already have one, you can use that.</span></span> <span data-ttu-id="b3f0f-179">否則，您可以到下列網址免費建立一個帳戶：[http://azure.microsoft.com/en-us/pricing/free-trial/](http://azure.microsoft.com/pricing/free-trial/) (如果在中國，請改為前往 <http://go.microsoft.com/fwlink/?LinkID=717821>)。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-179">Otherwise, you can create one for free at [http://azure.microsoft.com/en-us/pricing/free-trial/](http://azure.microsoft.com/pricing/free-trial/) (in China, visit <http://go.microsoft.com/fwlink/?LinkID=717821> instead).</span></span> <span data-ttu-id="b3f0f-180">如果您打算稍後[向 Azure 註冊 Azure Stack](azure-stack-register.md)，則也必須在這個新建立的帳戶中有一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-180">If you plan to later [register Azure Stack with Azure](azure-stack-register.md), you must also have a subscription in this newly created account.</span></span>
   
    <span data-ttu-id="b3f0f-181">儲存這些認證，以供在[部署開發套件](azure-stack-run-powershell-script.md#deploy-the-development-kit)的步驟 6 中使用。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-181">Save these credentials for use in step 6 of [Deploy the development kit](azure-stack-run-powershell-script.md#deploy-the-development-kit).</span></span> <span data-ttu-id="b3f0f-182">這個「服務管理員」帳戶可以設定和管理資源雲端、使用者帳戶、租用戶方案、配額及價格。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-182">This *service administrator* account can configure and manage resource clouds, user accounts, tenant plans, quotas, and pricing.</span></span> <span data-ttu-id="b3f0f-183">在此入口網站中，這些管理員可以建立網站雲端、虛擬機器私人雲端、建立方案，以及管理使用者訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-183">In the portal, they can create website clouds, virtual machine private clouds, create plans, and manage user subscriptions.</span></span>
2. <span data-ttu-id="b3f0f-184">至少[建立](azure-stack-add-new-user-aad.md)一個帳戶，以便您能夠以租用戶身分登入開發套件。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-184">[Create](azure-stack-add-new-user-aad.md) at least one account so that you can sign in to the development kit as a tenant.</span></span>
   
   | <span data-ttu-id="b3f0f-185">**Azure Active Directory 帳戶**</span><span class="sxs-lookup"><span data-stu-id="b3f0f-185">**Azure Active Directory account**</span></span> | <span data-ttu-id="b3f0f-186">**是否支援？**</span><span class="sxs-lookup"><span data-stu-id="b3f0f-186">**Supported?**</span></span> |
   | --- | --- |
   | <span data-ttu-id="b3f0f-187">具備有效公用 Azure 訂用帳戶的公司或學校帳戶</span><span class="sxs-lookup"><span data-stu-id="b3f0f-187">Work or school account with valid Public Azure Subscription</span></span> |<span data-ttu-id="b3f0f-188">是</span><span class="sxs-lookup"><span data-stu-id="b3f0f-188">Yes</span></span> |
   | <span data-ttu-id="b3f0f-189">具備有效的公用 Azure 訂用帳戶之 Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="b3f0f-189">Microsoft Account with valid Public Azure Subscription</span></span> |<span data-ttu-id="b3f0f-190">是</span><span class="sxs-lookup"><span data-stu-id="b3f0f-190">Yes</span></span> |
   | <span data-ttu-id="b3f0f-191">具備有效中國 Azure 訂用帳戶的公司或學校帳戶</span><span class="sxs-lookup"><span data-stu-id="b3f0f-191">Work or school account with valid China Azure Subscription</span></span> |<span data-ttu-id="b3f0f-192">是</span><span class="sxs-lookup"><span data-stu-id="b3f0f-192">Yes</span></span> |
   | <span data-ttu-id="b3f0f-193">具備有效美國政府 Azure 訂用帳戶的公司或學校帳戶</span><span class="sxs-lookup"><span data-stu-id="b3f0f-193">Work or school account with valid US Government Azure Subscription</span></span> |<span data-ttu-id="b3f0f-194">是</span><span class="sxs-lookup"><span data-stu-id="b3f0f-194">Yes</span></span> |

## <a name="network"></a><span data-ttu-id="b3f0f-195">網路</span><span class="sxs-lookup"><span data-stu-id="b3f0f-195">Network</span></span>
### <a name="switch"></a><span data-ttu-id="b3f0f-196">Switch</span><span class="sxs-lookup"><span data-stu-id="b3f0f-196">Switch</span></span>
<span data-ttu-id="b3f0f-197">一個在開發套件機器交換器上的可用連接埠。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-197">One available port on a switch for the development kit machine.</span></span>  

<span data-ttu-id="b3f0f-198">開發套件機器支援連線到交換器存取連接埠或主幹連接埠。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-198">The development kit machine supports connecting to a switch access port or trunk port.</span></span> <span data-ttu-id="b3f0f-199">此交換器不需要有任何特殊的功能。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-199">No specialized features are required on the switch.</span></span> <span data-ttu-id="b3f0f-200">如果您使用主幹連接埠，或如果您需要設定 VLAN ID，就必須提供 VLAN ID 作為部署參數。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-200">If you are using a trunk port or if you need to configure a VLAN ID, you have to provide the VLAN ID as a deployment parameter.</span></span> <span data-ttu-id="b3f0f-201">若要查看範例，請參閱[開發參數清單](azure-stack-run-powershell-script.md)。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-201">You can see examples in the [list of deployment parameters](azure-stack-run-powershell-script.md).</span></span>

### <a name="subnet"></a><span data-ttu-id="b3f0f-202">子網路</span><span class="sxs-lookup"><span data-stu-id="b3f0f-202">Subnet</span></span>
<span data-ttu-id="b3f0f-203">請勿將開發套件機器連線到下列子網路：</span><span class="sxs-lookup"><span data-stu-id="b3f0f-203">Do not connect the development kit machine to the following subnets:</span></span>

* <span data-ttu-id="b3f0f-204">192.168.200.0/24</span><span class="sxs-lookup"><span data-stu-id="b3f0f-204">192.168.200.0/24</span></span>
* <span data-ttu-id="b3f0f-205">192.168.100.0/27</span><span class="sxs-lookup"><span data-stu-id="b3f0f-205">192.168.100.0/27</span></span>
* <span data-ttu-id="b3f0f-206">192.168.101.0/26</span><span class="sxs-lookup"><span data-stu-id="b3f0f-206">192.168.101.0/26</span></span>
* <span data-ttu-id="b3f0f-207">192.168.102.0/24</span><span class="sxs-lookup"><span data-stu-id="b3f0f-207">192.168.102.0/24</span></span>
* <span data-ttu-id="b3f0f-208">192.168.103.0/25</span><span class="sxs-lookup"><span data-stu-id="b3f0f-208">192.168.103.0/25</span></span>
* <span data-ttu-id="b3f0f-209">192.168.104.0/25</span><span class="sxs-lookup"><span data-stu-id="b3f0f-209">192.168.104.0/25</span></span>

<span data-ttu-id="b3f0f-210">這些子網路是保留給在開發套件環境中的內部網路使用的。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-210">These subnets are reserved for the internal networks within the development kit environment.</span></span>

### <a name="ipv4ipv6"></a><span data-ttu-id="b3f0f-211">IPv4/IPv6</span><span class="sxs-lookup"><span data-stu-id="b3f0f-211">IPv4/IPv6</span></span>
<span data-ttu-id="b3f0f-212">僅支援 IPv4。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-212">Only IPv4 is supported.</span></span> <span data-ttu-id="b3f0f-213">您無法建立 IPv6 網路。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-213">You cannot create IPv6 networks.</span></span>

### <a name="dhcp"></a><span data-ttu-id="b3f0f-214">DHCP</span><span class="sxs-lookup"><span data-stu-id="b3f0f-214">DHCP</span></span>
<span data-ttu-id="b3f0f-215">請確定該網路上有可用的 DHCP 伺服器，供 NIC 與其連線。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-215">Make sure there is a DHCP server available on the network that the NIC connects to.</span></span> <span data-ttu-id="b3f0f-216">如果無法使用 DHCP，則除了主機所使用的網路之外，您還必須準備其他靜態 IPv4 網路。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-216">If DHCP is not available, you must prepare an additional static IPv4 network besides the one used by host.</span></span> <span data-ttu-id="b3f0f-217">您必須提供該 IP 位址和閘道作為部署參數。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-217">You must provide that IP address and gateway as a deployment parameter.</span></span> <span data-ttu-id="b3f0f-218">若要查看範例，請參閱[開發參數清單](azure-stack-run-powershell-script.md)。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-218">You can see examples in the [list of deployment parameters](azure-stack-run-powershell-script.md).</span></span>

### <a name="internet-access"></a><span data-ttu-id="b3f0f-219">網際網路存取</span><span class="sxs-lookup"><span data-stu-id="b3f0f-219">Internet access</span></span>
<span data-ttu-id="b3f0f-220">Azure Stack 需要能夠直接或透過 Transparent Proxy 存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-220">Azure Stack requires access to the Internet, either directly or through a transparent proxy.</span></span> <span data-ttu-id="b3f0f-221">Azure Stack 不支援設定 Web Proxy 來啟用網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-221">Azure Stack does not support the configuration of a web proxy to enable Internet access.</span></span> <span data-ttu-id="b3f0f-222">指派給 MAS-BGPNAT01 (透過 DHCP 或靜態 IP) 的主機 IP 和新 IP 都必須能夠存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-222">Both the host IP and the new IP assigned to the MAS-BGPNAT01 (by DHCP or static IP) must be able to access Internet.</span></span> <span data-ttu-id="b3f0f-223">連接埠 80 和 443 會用在 graph.windows.net 和 login.microsoftonline.com 網域下。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-223">Ports 80 and 443 are used under the graph.windows.net and login.microsoftonline.com domains.</span></span>

## <a name="telemetry"></a><span data-ttu-id="b3f0f-224">遙測</span><span class="sxs-lookup"><span data-stu-id="b3f0f-224">Telemetry</span></span>

<span data-ttu-id="b3f0f-225">遙測可協助我們打造未來的 Azure Stack 版本。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-225">Telemetry helps us shape future versions of Azure Stack.</span></span> <span data-ttu-id="b3f0f-226">它可讓我們快速回應意見反應、提供新功能，以及改善品質。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-226">It lets us respond quickly to feedback, provide new features, and improve quality.</span></span> <span data-ttu-id="b3f0f-227">Microsoft Azure Stack 包含 Windows Server 2016 和 SQL Server 2014。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-227">Microsoft Azure Stack includes Windows Server 2016 and SQL Server 2014.</span></span> <span data-ttu-id="b3f0f-228">這兩個產品的預設設定都未變更，且在「Microsoft Enterprise 隱私權聲明」中都有說明。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-228">Neither of these products are changed from default settings and both are described by the Microsoft Enterprise Privacy Statement.</span></span> <span data-ttu-id="b3f0f-229">Azure Stack 也包含尚未修改以傳送遙測給 Microsoft 的開放原始碼軟體。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-229">Azure Stack also contains open source software which has not been modified to send telemetry to Microsoft.</span></span> <span data-ttu-id="b3f0f-230">以下是一些 Azure Stack 遙測資料範例：</span><span class="sxs-lookup"><span data-stu-id="b3f0f-230">Here are some examples of Azure Stack telemetry data:</span></span>

- <span data-ttu-id="b3f0f-231">部署註冊資訊</span><span class="sxs-lookup"><span data-stu-id="b3f0f-231">deployment registration information</span></span>
- <span data-ttu-id="b3f0f-232">開啟和關閉警示時</span><span class="sxs-lookup"><span data-stu-id="b3f0f-232">when an alert is opened and closed</span></span>
- <span data-ttu-id="b3f0f-233">網路資源數目</span><span class="sxs-lookup"><span data-stu-id="b3f0f-233">the number of network resources</span></span>

<span data-ttu-id="b3f0f-234">若要支援遙測資料流程，必須在您的網路中開放連接埠 443 (HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-234">To support telemetry data flow, port 443 (HTTPS) must be open in your network.</span></span> <span data-ttu-id="b3f0f-235">用戶端端點是 https://vortex-win.data.microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-235">The client endpoint is https://vortex-win.data.microsoft.com.</span></span>

<span data-ttu-id="b3f0f-236">如果您不想要提供 Azure Stack 的遙測，您可以在開發套件主機和基礎結構虛擬機器上關閉它，如以下所述。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-236">If you don’t want to provide telemetry for Azure Stack, you can turn it off on the development kit host and the infrastructure virtual machines as explained below.</span></span>

### <a name="turn-off-telemetry-on-the-development-kit-host-optional"></a><span data-ttu-id="b3f0f-237">在開發套件主機上關閉遙測 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="b3f0f-237">Turn off telemetry on the development kit host (optional)</span></span>

>[!NOTE]
<span data-ttu-id="b3f0f-238">如果您想要關閉開發套件主機的遙測，您必須在執行部署指令碼前執行此操作。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-238">If you want to turn off telemetry for the development kit host, you must do so before you run the deployment script.</span></span>

<span data-ttu-id="b3f0f-239">在[執行 asdk-installer.ps1 指令碼]()以部署開發套件主機之前，先開機進入 CloudBuilder.vhdx，然後在已提高權限的 PowerShell 視窗中執行下列指令碼：</span><span class="sxs-lookup"><span data-stu-id="b3f0f-239">Before [running the asdk-installer.ps1 script]() to deploy the development kit host, boot into the CloudBuilder.vhdx and run the following script in an elevated PowerShell window:</span></span>
```powershell
### Get current AllowTelmetry value on DVM Host
(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name AllowTelemetry).AllowTelemetry
### Set & Get updated AllowTelemetry value for ASDK-Host 
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name "AllowTelemetry" -Value '0'  
(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name AllowTelemetry).AllowTelemetry
```

<span data-ttu-id="b3f0f-240">將 **AllowTelemetry** 設定為 0 會同時關閉 Windows 和 Azure Stack 部署的遙測。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-240">Setting **AllowTelemetry** to 0 turns off telemetry for both Windows and Azure Stack deployment.</span></span> <span data-ttu-id="b3f0f-241">系統只會傳送來自作業系統的重大安全性事件。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-241">Only critical security events from the operating system are sent.</span></span> <span data-ttu-id="b3f0f-242">這些設定會控制所有主機和基礎結構 VM 的 Windows 遙測，並且在進行向外延展作業時會重新套用到新的節點/VM。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-242">The setting controls Windows telemetry across all hosts and infrastructure VMs, and is reapplied to new nodes/VMs when scale-out operations occur.</span></span>


### <a name="turn-off-telemetry-on-the-infrastructure-virtual-machines-optional"></a><span data-ttu-id="b3f0f-243">在基礎結構虛擬機器上關閉遙測 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="b3f0f-243">Turn off telemetry on the infrastructure virtual machines (optional)</span></span>

<span data-ttu-id="b3f0f-244">順利完成部署之後，請在開發套件主機上，於已提高權限的 PowerShell 視窗中執行下列指令碼 (以 AzureStack\AzureStackAdmin 使用者身分)：</span><span class="sxs-lookup"><span data-stu-id="b3f0f-244">After the deployment is successful, run the following script in an elevated PowerShell window (as the AzureStack\AzureStackAdmin user) on the development kit host:</span></span>

```powershell
$AzSVMs= get-vm |  where {$_.Name -like "AzS-*"}
### Show current AllowTelemetry value for all AzS-VMs
invoke-command -computername $AzSVMs.name {(Get-ItemProperty -Path `
"HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" -Name AllowTelemetry).AllowTelemetry}
### Set & Get updated AllowTelemetry value for all AzS-VMs
invoke-command -computername $AzSVMs.name {Set-ItemProperty -Path `
"HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" -Name "AllowTelemetry" -Value '0'}
invoke-command -computername $AzSVMs.name {(Get-ItemProperty -Path `
"HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" -Name AllowTelemetry).AllowTelemetry}
```

<span data-ttu-id="b3f0f-245">若要設定 SQL Server 遙測，請參閱[如何設定 SQL Server 2016](https://support.microsoft.com/en-us/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft)。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-245">To configure SQL Server telemetry, see [How to configure SQL Server 2016](https://support.microsoft.com/en-us/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft).</span></span>

### <a name="usage-reporting"></a><span data-ttu-id="b3f0f-246">使用量回報</span><span class="sxs-lookup"><span data-stu-id="b3f0f-246">Usage reporting</span></span>

<span data-ttu-id="b3f0f-247">透過註冊，Azure Stack 也會設定為將使用量資訊轉送給 Azure。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-247">Through registration, Azure Stack is also configured to forward usage information to Azure.</span></span> <span data-ttu-id="b3f0f-248">使用量回報是與遙測分別控制的。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-248">Usage reporting is controlled independently from telemetry.</span></span> <span data-ttu-id="b3f0f-249">您可以使用 Github 上的指令碼在[註冊](azure-stack-register.md)時關閉使用量回報。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-249">You can turn off usage reporting when [registering](azure-stack-register.md) by using the script on Github.</span></span> <span data-ttu-id="b3f0f-250">只要將 **$reportUsage** 參數設定為 **$false** 即可。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-250">Just set the **$reportUsage** parameter to **$false**.</span></span>

<span data-ttu-id="b3f0f-251">若要深入了解使用量資料的格式，請參閱[向 Azure 回報 Azure Stack 使用量資料](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-usage-reporting) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-251">Usage data is formatted as detailed in the [Report Azure Stack usage data to Azure](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-usage-reporting).</span></span> <span data-ttu-id="b3f0f-252">「Azure Stack 開發套件」使用者實際上無須付費。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-252">Azure Stack Development Kit users are not actually charged.</span></span> <span data-ttu-id="b3f0f-253">此功能包含在開發套件中，因此您可以測試來了解使用量回報的運作方式。</span><span class="sxs-lookup"><span data-stu-id="b3f0f-253">This functionality is included in the development kit so that you can test to see how usage reporting works.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="b3f0f-254">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3f0f-254">Next steps</span></span>
[<span data-ttu-id="b3f0f-255">下載 Azure Stack 開發套件部署套件</span><span class="sxs-lookup"><span data-stu-id="b3f0f-255">Download the Azure Stack development kit deployment package</span></span>](https://azure.microsoft.com/overview/azure-stack/try/?v=try)

[<span data-ttu-id="b3f0f-256">部署 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="b3f0f-256">Deploy Azure Stack development kit</span></span>](azure-stack-run-powershell-script.md)

