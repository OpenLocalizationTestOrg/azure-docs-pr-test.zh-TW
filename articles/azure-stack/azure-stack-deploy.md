---
title: "aaaAzure 堆疊開發套件的部署必要條件 |Microsoft 文件"
description: "檢視 Azure 堆疊開發套件 （雲端操作員） 的 hello 環境和硬體需求。"
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
ms.openlocfilehash: 126c851651354b6f3d61c4627ab0c1de9da12ba9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-deployment-prerequisites"></a><span data-ttu-id="f0a5a-103">Azure Stack 部署先決條件</span><span class="sxs-lookup"><span data-stu-id="f0a5a-103">Azure Stack deployment prerequisites</span></span>
<span data-ttu-id="f0a5a-104">部署 Azure 堆疊之前[開發套件](azure-stack-poc.md)，請確定您的電腦符合下列需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="f0a5a-104">Before you deploy Azure Stack [Development Kit](azure-stack-poc.md), make sure your computer meets hello following requirements:</span></span>


## <a name="hardware"></a><span data-ttu-id="f0a5a-105">硬體</span><span class="sxs-lookup"><span data-stu-id="f0a5a-105">Hardware</span></span>
| <span data-ttu-id="f0a5a-106">元件</span><span class="sxs-lookup"><span data-stu-id="f0a5a-106">Component</span></span> | <span data-ttu-id="f0a5a-107">最小值</span><span class="sxs-lookup"><span data-stu-id="f0a5a-107">Minimum</span></span> | <span data-ttu-id="f0a5a-108">建議</span><span class="sxs-lookup"><span data-stu-id="f0a5a-108">Recommended</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f0a5a-109">磁碟機：作業系統</span><span class="sxs-lookup"><span data-stu-id="f0a5a-109">Disk drives: Operating System</span></span> |<span data-ttu-id="f0a5a-110">1 個 OS 磁碟 (SSD 或 HDD)，最少有 200 GB 供系統磁碟分割使用</span><span class="sxs-lookup"><span data-stu-id="f0a5a-110">1 OS disk with minimum of 200 GB available for system partition (SSD or HDD)</span></span> |<span data-ttu-id="f0a5a-111">1 個 OS 磁碟 (SSD 或 HDD)，最少有 200 GB 供系統磁碟分割使用</span><span class="sxs-lookup"><span data-stu-id="f0a5a-111">1 OS disk with minimum of 200 GB available for system partition (SSD or HDD)</span></span> |
| <span data-ttu-id="f0a5a-112">磁碟機：一般開發套件資料*</span><span class="sxs-lookup"><span data-stu-id="f0a5a-112">Disk drives: General development kit data*</span></span> |<span data-ttu-id="f0a5a-113">4 個磁碟。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-113">4 disks.</span></span> <span data-ttu-id="f0a5a-114">每個磁碟 (SSD 或 HDD) 提供最少 140 GB 的容量。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-114">Each disk provides a minimum of 140 GB of capacity (SSD or HDD).</span></span> <span data-ttu-id="f0a5a-115">將會使用所有可用的磁碟。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-115">All available disks will be used.</span></span> |<span data-ttu-id="f0a5a-116">4 個磁碟。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-116">4 disks.</span></span> <span data-ttu-id="f0a5a-117">每個磁碟 (SSD 或 HDD) 至少提供 250 GB 的容量。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-117">Each disk provides a minimum of 250 GB of capacity (SSD or HDD).</span></span> <span data-ttu-id="f0a5a-118">將會使用所有可用的磁碟。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-118">All available disks will be used.</span></span> |
| <span data-ttu-id="f0a5a-119">計算：CPU</span><span class="sxs-lookup"><span data-stu-id="f0a5a-119">Compute: CPU</span></span> |<span data-ttu-id="f0a5a-120">雙插槽：12 個實體核心 (總計)</span><span class="sxs-lookup"><span data-stu-id="f0a5a-120">Dual-Socket: 12 Physical Cores (total)</span></span> |<span data-ttu-id="f0a5a-121">雙插槽：16 個實體核心 (總計)</span><span class="sxs-lookup"><span data-stu-id="f0a5a-121">Dual-Socket: 16 Physical Cores (total)</span></span> |
| <span data-ttu-id="f0a5a-122">計算：記憶體</span><span class="sxs-lookup"><span data-stu-id="f0a5a-122">Compute: Memory</span></span> |<span data-ttu-id="f0a5a-123">96 GB RAM</span><span class="sxs-lookup"><span data-stu-id="f0a5a-123">96 GB RAM</span></span> |<span data-ttu-id="f0a5a-124">128 GB 的 RAM （這是 hello 最小 toosupport PaaS 資源提供者）。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-124">128 GB RAM (This is hello minimum toosupport PaaS resource providers.)</span></span>|
| <span data-ttu-id="f0a5a-125">計算：BIOS</span><span class="sxs-lookup"><span data-stu-id="f0a5a-125">Compute: BIOS</span></span> |<span data-ttu-id="f0a5a-126">啟用 Hyper-V (支援 SLAT)</span><span class="sxs-lookup"><span data-stu-id="f0a5a-126">Hyper-V Enabled (with SLAT support)</span></span> |<span data-ttu-id="f0a5a-127">啟用 Hyper-V (支援 SLAT)</span><span class="sxs-lookup"><span data-stu-id="f0a5a-127">Hyper-V Enabled (with SLAT support)</span></span> |
| <span data-ttu-id="f0a5a-128">網路：NIC</span><span class="sxs-lookup"><span data-stu-id="f0a5a-128">Network: NIC</span></span> |<span data-ttu-id="f0a5a-129">NIC 所需的 Windows Server 2012 R2 憑證；不需特殊的功能</span><span class="sxs-lookup"><span data-stu-id="f0a5a-129">Windows Server 2012 R2 Certification required for NIC; no specialized features required</span></span> |<span data-ttu-id="f0a5a-130">NIC 所需的 Windows Server 2012 R2 憑證；不需特殊的功能</span><span class="sxs-lookup"><span data-stu-id="f0a5a-130">Windows Server 2012 R2 Certification required for NIC; no specialized features required</span></span> |
| <span data-ttu-id="f0a5a-131">HW 標誌憑證</span><span class="sxs-lookup"><span data-stu-id="f0a5a-131">HW logo certification</span></span> |[<span data-ttu-id="f0a5a-132">Windows Server 2012 R2 認證</span><span class="sxs-lookup"><span data-stu-id="f0a5a-132">Certified for Windows Server 2012 R2</span></span>](http://windowsservercatalog.com/results.aspx?&chtext=&cstext=&csttext=&chbtext=&bCatID=1333&cpID=0&avc=79&ava=0&avq=0&OR=1&PGS=25&ready=0) |[<span data-ttu-id="f0a5a-133">Windows Server 2012 R2 認證</span><span class="sxs-lookup"><span data-stu-id="f0a5a-133">Certified for Windows Server 2012 R2</span></span>](http://windowsservercatalog.com/results.aspx?&chtext=&cstext=&csttext=&chbtext=&bCatID=1333&cpID=0&avc=79&ava=0&avq=0&OR=1&PGS=25&ready=0) |

<span data-ttu-id="f0a5a-134">\*您將需要一個以上這建議容量，如果您計劃新增許多 hello [marketplace 項目](azure-stack-download-azure-marketplace-item.md)從 Azure。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-134">\*You will need more than this recommended capacity if you plan on adding many of hello [marketplace items](azure-stack-download-azure-marketplace-item.md) from Azure.</span></span>

<span data-ttu-id="f0a5a-135">**資料磁碟機組態：**所有資料磁碟機必須是都 hello 相同類型 （所有 SAS 或 SATA 所有） 和容量。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-135">**Data disk drive configuration:** All data drives must be of hello same type (all SAS or all SATA) and capacity.</span></span> <span data-ttu-id="f0a5a-136">如果使用 SAS 磁碟機，hello 磁碟機必須連接透過 （提供任何的 MPIO 支援多重路徑） 的單一路徑。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-136">If SAS disk drives are used, hello disk drives must be attached via a single path (no MPIO, multi-path support is provided).</span></span>

<span data-ttu-id="f0a5a-137">**HBA 組態選項**</span><span class="sxs-lookup"><span data-stu-id="f0a5a-137">**HBA configuration options**</span></span>

* <span data-ttu-id="f0a5a-138">(慣用) 簡單 HBA</span><span class="sxs-lookup"><span data-stu-id="f0a5a-138">(Preferred) Simple HBA</span></span>
* <span data-ttu-id="f0a5a-139">RAID HBA – 介面卡必須設定為「穿通」模式</span><span class="sxs-lookup"><span data-stu-id="f0a5a-139">RAID HBA – Adapter must be configured in “pass through” mode</span></span>
* <span data-ttu-id="f0a5a-140">RAID HBA – 磁碟應設定為單一磁碟、RAID 0</span><span class="sxs-lookup"><span data-stu-id="f0a5a-140">RAID HBA – Disks should be configured as Single-Disk, RAID-0</span></span>

<span data-ttu-id="f0a5a-141">**支援的匯流排和媒體類型組合**</span><span class="sxs-lookup"><span data-stu-id="f0a5a-141">**Supported bus and media type combinations**</span></span>

* <span data-ttu-id="f0a5a-142">SATA HDD</span><span class="sxs-lookup"><span data-stu-id="f0a5a-142">SATA HDD</span></span>
* <span data-ttu-id="f0a5a-143">SAS HDD</span><span class="sxs-lookup"><span data-stu-id="f0a5a-143">SAS HDD</span></span>
* <span data-ttu-id="f0a5a-144">RAID HDD</span><span class="sxs-lookup"><span data-stu-id="f0a5a-144">RAID HDD</span></span>
* <span data-ttu-id="f0a5a-145">RAID SSD (如果 hello 媒體類型為 unknown 未指定\*)</span><span class="sxs-lookup"><span data-stu-id="f0a5a-145">RAID SSD (If hello media type is unspecified/unknown\*)</span></span>
* <span data-ttu-id="f0a5a-146">SATA SSD + SATA HDD</span><span class="sxs-lookup"><span data-stu-id="f0a5a-146">SATA SSD + SATA HDD</span></span>
* <span data-ttu-id="f0a5a-147">SAS SSD + SAS HDD</span><span class="sxs-lookup"><span data-stu-id="f0a5a-147">SAS SSD + SAS HDD</span></span>

<span data-ttu-id="f0a5a-148">\*不具備傳遞功能的 RAID 控制器無法辨識 hello 媒體類型。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-148">\* RAID controllers without pass-through capability can’t recognize hello media type.</span></span> <span data-ttu-id="f0a5a-149">這類控制站會將 SSD 和 HDD，皆標示為未指定。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-149">Such controllers will mark both HDD and SSD as Unspecified.</span></span> <span data-ttu-id="f0a5a-150">在此情況下，hello SSD 將當做永續性儲存體，而不是快取的裝置。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-150">In that case, hello SSD will be used as persistent storage instead of caching devices.</span></span> <span data-ttu-id="f0a5a-151">因此，您可以部署在這些 Ssd 上的 hello 開發套件。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-151">Therefore, you can deploy hello development kit on those SSDs.</span></span>

<span data-ttu-id="f0a5a-152">**範例 HBA**：傳遞模式中的 LSI 9207-8i、LSI-9300-8i 或 LSI-9265-8i</span><span class="sxs-lookup"><span data-stu-id="f0a5a-152">**Example HBAs**: LSI 9207-8i, LSI-9300-8i, or LSI-9265-8i in pass-through mode</span></span>

<span data-ttu-id="f0a5a-153">範例 OEM 設定可供使用。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-153">Sample OEM configurations are available.</span></span>

## <a name="operating-system"></a><span data-ttu-id="f0a5a-154">作業系統</span><span class="sxs-lookup"><span data-stu-id="f0a5a-154">Operating system</span></span>
|  | <span data-ttu-id="f0a5a-155">**需求**</span><span class="sxs-lookup"><span data-stu-id="f0a5a-155">**Requirements**</span></span> |
| --- | --- |
| <span data-ttu-id="f0a5a-156">**作業系統版本**</span><span class="sxs-lookup"><span data-stu-id="f0a5a-156">**OS Version**</span></span> |<span data-ttu-id="f0a5a-157">Windows Server 2012 R2 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-157">Windows Server 2012 R2 or later.</span></span> <span data-ttu-id="f0a5a-158">hello 作業系統版本不是那麼重要之前 hello 部署開始，當您將 hello 主機電腦開機成 hello hello Azure 堆疊安裝中包含的 VHD。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-158">hello operating system version isn’t critical before hello deployment starts, as you'll boot hello host computer into hello VHD that's included in hello Azure Stack installation.</span></span> <span data-ttu-id="f0a5a-159">hello 作業系統和所有必要的修補程式已整合至 hello 映像中。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-159">hello OS and all required patches are already integrated into hello image.</span></span> <span data-ttu-id="f0a5a-160">請勿使用任何 Windows Server 的執行個體使用 hello 開發套件中的任何索引鍵 tooactivate。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-160">Don’t use any keys tooactivate any Windows Server instances used in hello development kit.</span></span> |

## <a name="deployment-requirements-check-tool"></a><span data-ttu-id="f0a5a-161">部署需求檢查工具</span><span class="sxs-lookup"><span data-stu-id="f0a5a-161">Deployment requirements check tool</span></span>
<span data-ttu-id="f0a5a-162">安裝之後 hello 作業系統，您可以使用 hello[部署適用於 Azure 堆疊檢查程式](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b)tooconfirm 硬體是否符合所有 hello 需求。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-162">After installing hello operating system, you can use hello [Deployment Checker for Azure Stack](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b) tooconfirm that your hardware meets all hello requirements.</span></span>

## <a name="account-requirements"></a><span data-ttu-id="f0a5a-163">帳戶需求</span><span class="sxs-lookup"><span data-stu-id="f0a5a-163">Account requirements</span></span>
<span data-ttu-id="f0a5a-164">一般而言，您會透過網際網路連線，您可以在此連接 tooMicrosoft Azure 部署 hello 開發套件。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-164">Typically, you deploy hello development kit with internet connectivity, where you can connect tooMicrosoft Azure.</span></span> <span data-ttu-id="f0a5a-165">在此情況下，您必須設定 Azure Active Directory (Azure AD) 帳戶 toodeploy hello 開發套件。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-165">In this case, you must configure an Azure Active Directory (Azure AD) account toodeploy hello development kit.</span></span>

<span data-ttu-id="f0a5a-166">如果您的環境不是連接的 toohello 網際網路或您不想 toouse Azure AD，您也可以使用 Active Directory Federation Services (AD FS) 來部署 「 Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-166">If your environment is not connected toohello internet, or you don't want toouse Azure AD, you can deploy Azure Stack by using Active Directory Federation Services (AD FS).</span></span> <span data-ttu-id="f0a5a-167">hello 開發套件包含它自己的 AD FS 與 Active Directory 網域服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-167">hello development kit includes its own AD FS and Active Directory Domain Services instances.</span></span> <span data-ttu-id="f0a5a-168">如果您部署使用此選項，您不需要事先帳戶 tooset。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-168">If you deploy by using this option, you don't have tooset up accounts ahead of time.</span></span>

>[!NOTE]
<span data-ttu-id="f0a5a-169">如果您部署使用 hello AD FS 選項，您必須重新部署 Azure 堆疊 tooswitch tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-169">If you deploy by using hello AD FS option, you must redeploy Azure Stack tooswitch tooAzure AD.</span></span>

### <a name="azure-active-directory-accounts"></a><span data-ttu-id="f0a5a-170">Azure Active Directory 帳戶</span><span class="sxs-lookup"><span data-stu-id="f0a5a-170">Azure Active Directory accounts</span></span>
<span data-ttu-id="f0a5a-171">toodeploy Azure 堆疊使用的 Azure AD 帳戶，執行 hello 部署 PowerShell 指令碼之前，您必須準備好 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-171">toodeploy Azure Stack by using an Azure AD account, you must prepare an Azure AD account before you run hello deployment PowerShell script.</span></span> <span data-ttu-id="f0a5a-172">這個帳戶會成為 hello Azure AD 租用戶的全域管理員 hello。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-172">This account becomes hello Global Admin for hello Azure AD tenant.</span></span> <span data-ttu-id="f0a5a-173">它已與 Azure Active Directory 和 Graph API 的互動的所有 Azure 堆疊服務都使用 tooprovision 和委派的應用程式和服務主體。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-173">It's used tooprovision and delegate applications and service principals for all Azure Stack services that interact with Azure Active Directory and Graph API.</span></span> <span data-ttu-id="f0a5a-174">它也會使用做為 hello hello 預設提供者訂用帳戶 （您之後可以變更） 擁有者。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-174">It's also used as hello owner of hello default provider subscription (which you can later change).</span></span> <span data-ttu-id="f0a5a-175">您可以使用此帳戶，就可登入 tooyour Azure 堆疊系統的系統管理員入口網站。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-175">You can log in tooyour Azure Stack system’s administrator portal by using this account.</span></span>

1. <span data-ttu-id="f0a5a-176">建立 Azure AD 帳戶，至少一個 Azure AD 的 hello 目錄管理員。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-176">Create an Azure AD account that is hello directory administrator for at least one Azure AD.</span></span> <span data-ttu-id="f0a5a-177">如果您已經有一個這樣的帳戶，則可以使用該帳戶。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-177">If you already have one, you can use that.</span></span> <span data-ttu-id="f0a5a-178">否則，您可以到下列網址免費建立一個帳戶：[http://azure.microsoft.com/en-us/pricing/free-trial/](http://azure.microsoft.com/pricing/free-trial/) (如果在中國，請改為前往 <http://go.microsoft.com/fwlink/?LinkID=717821>)。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-178">Otherwise, you can create one for free at [http://azure.microsoft.com/en-us/pricing/free-trial/](http://azure.microsoft.com/pricing/free-trial/) (in China, visit <http://go.microsoft.com/fwlink/?LinkID=717821> instead).</span></span> <span data-ttu-id="f0a5a-179">如果您計劃 toolater[向 Azure 註冊 Azure 堆疊](azure-stack-register.md)，您也必須擁有訂用帳戶中新建立的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-179">If you plan toolater [register Azure Stack with Azure](azure-stack-register.md), you must also have a subscription in this newly created account.</span></span>
   
    <span data-ttu-id="f0a5a-180">儲存的步驟 6 中使用這些認證[部署 hello 開發套件](azure-stack-run-powershell-script.md#deploy-the-development-kit)。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-180">Save these credentials for use in step 6 of [Deploy hello development kit](azure-stack-run-powershell-script.md#deploy-the-development-kit).</span></span> <span data-ttu-id="f0a5a-181">這個「服務管理員」帳戶可以設定和管理資源雲端、使用者帳戶、租用戶方案、配額及價格。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-181">This *service administrator* account can configure and manage resource clouds, user accounts, tenant plans, quotas, and pricing.</span></span> <span data-ttu-id="f0a5a-182">在 hello 入口網站建立網站雲端、 虛擬機器私人雲端、 建立方案，便能管理使用者訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-182">In hello portal, they can create website clouds, virtual machine private clouds, create plans, and manage user subscriptions.</span></span>
2. <span data-ttu-id="f0a5a-183">[建立](azure-stack-add-new-user-aad.md)至少一個帳戶，讓您可以登入租用戶身分 toohello 開發套件。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-183">[Create](azure-stack-add-new-user-aad.md) at least one account so that you can sign in toohello development kit as a tenant.</span></span>
   
   | <span data-ttu-id="f0a5a-184">**Azure Active Directory 帳戶**</span><span class="sxs-lookup"><span data-stu-id="f0a5a-184">**Azure Active Directory account**</span></span> | <span data-ttu-id="f0a5a-185">**是否支援？**</span><span class="sxs-lookup"><span data-stu-id="f0a5a-185">**Supported?**</span></span> |
   | --- | --- |
   | <span data-ttu-id="f0a5a-186">具備有效公用 Azure 訂用帳戶的公司或學校帳戶</span><span class="sxs-lookup"><span data-stu-id="f0a5a-186">Work or school account with valid Public Azure Subscription</span></span> |<span data-ttu-id="f0a5a-187">是</span><span class="sxs-lookup"><span data-stu-id="f0a5a-187">Yes</span></span> |
   | <span data-ttu-id="f0a5a-188">具備有效的公用 Azure 訂用帳戶之 Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="f0a5a-188">Microsoft Account with valid Public Azure Subscription</span></span> |<span data-ttu-id="f0a5a-189">是</span><span class="sxs-lookup"><span data-stu-id="f0a5a-189">Yes</span></span> |
   | <span data-ttu-id="f0a5a-190">具備有效中國 Azure 訂用帳戶的公司或學校帳戶</span><span class="sxs-lookup"><span data-stu-id="f0a5a-190">Work or school account with valid China Azure Subscription</span></span> |<span data-ttu-id="f0a5a-191">是</span><span class="sxs-lookup"><span data-stu-id="f0a5a-191">Yes</span></span> |
   | <span data-ttu-id="f0a5a-192">具備有效美國政府 Azure 訂用帳戶的公司或學校帳戶</span><span class="sxs-lookup"><span data-stu-id="f0a5a-192">Work or school account with valid US Government Azure Subscription</span></span> |<span data-ttu-id="f0a5a-193">是</span><span class="sxs-lookup"><span data-stu-id="f0a5a-193">Yes</span></span> |

## <a name="network"></a><span data-ttu-id="f0a5a-194">網路</span><span class="sxs-lookup"><span data-stu-id="f0a5a-194">Network</span></span>
### <a name="switch"></a><span data-ttu-id="f0a5a-195">Switch</span><span class="sxs-lookup"><span data-stu-id="f0a5a-195">Switch</span></span>
<span data-ttu-id="f0a5a-196">一個可用的通訊埠的交換器 hello 開發套件的電腦上。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-196">One available port on a switch for hello development kit machine.</span></span>  

<span data-ttu-id="f0a5a-197">hello 開發套件的電腦支援連接 tooa 交換器存取連接埠或主幹連接埠。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-197">hello development kit machine supports connecting tooa switch access port or trunk port.</span></span> <span data-ttu-id="f0a5a-198">Hello 交換器上所不需的任何特殊的功能。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-198">No specialized features are required on hello switch.</span></span> <span data-ttu-id="f0a5a-199">如果您使用主幹連接埠，或者如果您需要 tooconfigure VLAN ID，您有 tooprovide hello 做為部署參數的 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-199">If you are using a trunk port or if you need tooconfigure a VLAN ID, you have tooprovide hello VLAN ID as a deployment parameter.</span></span> <span data-ttu-id="f0a5a-200">您可以看到在 hello 範例[部署參數清單](azure-stack-run-powershell-script.md)。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-200">You can see examples in hello [list of deployment parameters](azure-stack-run-powershell-script.md).</span></span>

### <a name="subnet"></a><span data-ttu-id="f0a5a-201">子網路</span><span class="sxs-lookup"><span data-stu-id="f0a5a-201">Subnet</span></span>
<span data-ttu-id="f0a5a-202">不會連接 hello 開發套件機器 toohello 下列子網路：</span><span class="sxs-lookup"><span data-stu-id="f0a5a-202">Do not connect hello development kit machine toohello following subnets:</span></span>

* <span data-ttu-id="f0a5a-203">192.168.200.0/24</span><span class="sxs-lookup"><span data-stu-id="f0a5a-203">192.168.200.0/24</span></span>
* <span data-ttu-id="f0a5a-204">192.168.100.0/27</span><span class="sxs-lookup"><span data-stu-id="f0a5a-204">192.168.100.0/27</span></span>
* <span data-ttu-id="f0a5a-205">192.168.101.0/26</span><span class="sxs-lookup"><span data-stu-id="f0a5a-205">192.168.101.0/26</span></span>
* <span data-ttu-id="f0a5a-206">192.168.102.0/24</span><span class="sxs-lookup"><span data-stu-id="f0a5a-206">192.168.102.0/24</span></span>
* <span data-ttu-id="f0a5a-207">192.168.103.0/25</span><span class="sxs-lookup"><span data-stu-id="f0a5a-207">192.168.103.0/25</span></span>
* <span data-ttu-id="f0a5a-208">192.168.104.0/25</span><span class="sxs-lookup"><span data-stu-id="f0a5a-208">192.168.104.0/25</span></span>

<span data-ttu-id="f0a5a-209">這些子網路會保留給 hello hello 開發套件環境內的內部網路。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-209">These subnets are reserved for hello internal networks within hello development kit environment.</span></span>

### <a name="ipv4ipv6"></a><span data-ttu-id="f0a5a-210">IPv4/IPv6</span><span class="sxs-lookup"><span data-stu-id="f0a5a-210">IPv4/IPv6</span></span>
<span data-ttu-id="f0a5a-211">僅支援 IPv4。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-211">Only IPv4 is supported.</span></span> <span data-ttu-id="f0a5a-212">您無法建立 IPv6 網路。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-212">You cannot create IPv6 networks.</span></span>

### <a name="dhcp"></a><span data-ttu-id="f0a5a-213">DHCP</span><span class="sxs-lookup"><span data-stu-id="f0a5a-213">DHCP</span></span>
<span data-ttu-id="f0a5a-214">請確定有為 NIC 連線到該 hello hello 網路上可用的 DHCP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-214">Make sure there is a DHCP server available on hello network that hello NIC connects to.</span></span> <span data-ttu-id="f0a5a-215">如果 DHCP 無法使用，您必須準備其他除了 hello 其中一個主機使用靜態 IPv4 網路。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-215">If DHCP is not available, you must prepare an additional static IPv4 network besides hello one used by host.</span></span> <span data-ttu-id="f0a5a-216">您必須提供該 IP 位址和閘道作為部署參數。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-216">You must provide that IP address and gateway as a deployment parameter.</span></span> <span data-ttu-id="f0a5a-217">您可以看到在 hello 範例[部署參數清單](azure-stack-run-powershell-script.md)。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-217">You can see examples in hello [list of deployment parameters](azure-stack-run-powershell-script.md).</span></span>

### <a name="internet-access"></a><span data-ttu-id="f0a5a-218">網際網路存取</span><span class="sxs-lookup"><span data-stu-id="f0a5a-218">Internet access</span></span>
<span data-ttu-id="f0a5a-219">Azure 堆疊需要存取 toohello 網際網路，直接或透過 transparent proxy。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-219">Azure Stack requires access toohello Internet, either directly or through a transparent proxy.</span></span> <span data-ttu-id="f0a5a-220">Azure 堆疊不支援 web proxy tooenable 網際網路存取的 hello 的組態。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-220">Azure Stack does not support hello configuration of a web proxy tooenable Internet access.</span></span> <span data-ttu-id="f0a5a-221">Hello 主機 IP 和 hello 新的 IP 指派的 toohello MA-BGPNAT01 （透過 DHCP 或靜態 IP） 必須能夠 tooaccess 網際網路。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-221">Both hello host IP and hello new IP assigned toohello MAS-BGPNAT01 (by DHCP or static IP) must be able tooaccess Internet.</span></span> <span data-ttu-id="f0a5a-222">Hello graph.windows.net 和 login.microsoftonline.com 網域下使用連接埠 80 和 443。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-222">Ports 80 and 443 are used under hello graph.windows.net and login.microsoftonline.com domains.</span></span>

## <a name="telemetry"></a><span data-ttu-id="f0a5a-223">遙測</span><span class="sxs-lookup"><span data-stu-id="f0a5a-223">Telemetry</span></span>

<span data-ttu-id="f0a5a-224">遙測可協助我們打造未來的 Azure Stack 版本。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-224">Telemetry helps us shape future versions of Azure Stack.</span></span> <span data-ttu-id="f0a5a-225">它可讓我們快速回應 toofeedback、 提供新功能，並改善品質。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-225">It lets us respond quickly toofeedback, provide new features, and improve quality.</span></span> <span data-ttu-id="f0a5a-226">Microsoft Azure Stack 包含 Windows Server 2016 和 SQL Server 2014。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-226">Microsoft Azure Stack includes Windows Server 2016 and SQL Server 2014.</span></span> <span data-ttu-id="f0a5a-227">這些產品都不會變更預設值，並 hello Microsoft 企業隱私權聲明會說明這兩。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-227">Neither of these products are changed from default settings and both are described by hello Microsoft Enterprise Privacy Statement.</span></span> <span data-ttu-id="f0a5a-228">Azure 堆疊也會包含已修改過的 toosend 遙測 tooMicrosoft 開放原始碼軟體。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-228">Azure Stack also contains open source software which has not been modified toosend telemetry tooMicrosoft.</span></span> <span data-ttu-id="f0a5a-229">以下是一些 Azure Stack 遙測資料範例：</span><span class="sxs-lookup"><span data-stu-id="f0a5a-229">Here are some examples of Azure Stack telemetry data:</span></span>

- <span data-ttu-id="f0a5a-230">部署註冊資訊</span><span class="sxs-lookup"><span data-stu-id="f0a5a-230">deployment registration information</span></span>
- <span data-ttu-id="f0a5a-231">開啟和關閉警示時</span><span class="sxs-lookup"><span data-stu-id="f0a5a-231">when an alert is opened and closed</span></span>
- <span data-ttu-id="f0a5a-232">網路資源的 hello 數目</span><span class="sxs-lookup"><span data-stu-id="f0a5a-232">hello number of network resources</span></span>

<span data-ttu-id="f0a5a-233">toosupport 遙測資料流程中，連接埠 443 (HTTPS) 必須在您的網路中開啟。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-233">toosupport telemetry data flow, port 443 (HTTPS) must be open in your network.</span></span> <span data-ttu-id="f0a5a-234">https://vortex-win.data.microsoft.com hello 用戶端端點。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-234">hello client endpoint is https://vortex-win.data.microsoft.com.</span></span>

<span data-ttu-id="f0a5a-235">如果您不想要 Azure 堆疊 tooprovide 遙測，您可以在 hello 開發套件主機和 hello 的基礎結構虛擬機器如下所述將它關閉。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-235">If you don’t want tooprovide telemetry for Azure Stack, you can turn it off on hello development kit host and hello infrastructure virtual machines as explained below.</span></span>

### <a name="turn-off-telemetry-on-hello-development-kit-host-optional"></a><span data-ttu-id="f0a5a-236">關閉 hello 開發套件主機上的遙測 （選擇性）</span><span class="sxs-lookup"><span data-stu-id="f0a5a-236">Turn off telemetry on hello development kit host (optional)</span></span>

>[!NOTE]
<span data-ttu-id="f0a5a-237">如果您想要關閉遙測 tooturn hello 開發套件主應用程式，您必須執行之前執行 hello 部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-237">If you want tooturn off telemetry for hello development kit host, you must do so before you run hello deployment script.</span></span>

<span data-ttu-id="f0a5a-238">之前[執行 hello asdk installer.ps1 指令碼]()toodeploy hello 開發套件主應用程式、 開機進入 hello CloudBuilder.vhdx 和 hello 執行的下列指令碼在提升權限的 PowerShell 視窗中：</span><span class="sxs-lookup"><span data-stu-id="f0a5a-238">Before [running hello asdk-installer.ps1 script]() toodeploy hello development kit host, boot into hello CloudBuilder.vhdx and run hello following script in an elevated PowerShell window:</span></span>
```powershell
### Get current AllowTelmetry value on DVM Host
(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name AllowTelemetry).AllowTelemetry
### Set & Get updated AllowTelemetry value for ASDK-Host 
Set-ItemProperty-Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name "AllowTelemetry" -Value '0'  
(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name AllowTelemetry).AllowTelemetry
```

<span data-ttu-id="f0a5a-239">設定**AllowTelemetry** too0 關閉 Windows 和 Azure 堆疊部署的遙測。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-239">Setting **AllowTelemetry** too0 turns off telemetry for both Windows and Azure Stack deployment.</span></span> <span data-ttu-id="f0a5a-240">只有關鍵的安全性事件 hello 作業系統會傳送。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-240">Only critical security events from hello operating system are sent.</span></span> <span data-ttu-id="f0a5a-241">hello 設定的所有主機和基礎結構的 Vm，都控制 Windows 遙測，並向外延展作業發生時，會重新套用 toonew 節點/Vm。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-241">hello setting controls Windows telemetry across all hosts and infrastructure VMs, and is reapplied toonew nodes/VMs when scale-out operations occur.</span></span>


### <a name="turn-off-telemetry-on-hello-infrastructure-virtual-machines-optional"></a><span data-ttu-id="f0a5a-242">關閉 hello 基礎結構的虛擬機器上的遙測 （選擇性）</span><span class="sxs-lookup"><span data-stu-id="f0a5a-242">Turn off telemetry on hello infrastructure virtual machines (optional)</span></span>

<span data-ttu-id="f0a5a-243">Hello 部署後成功，請執行下列指令碼在提升權限的 PowerShell 視窗中 （如 hello AzureStack\AzureStackAdmin 使用者) hello 開發套件主機上的 hello:</span><span class="sxs-lookup"><span data-stu-id="f0a5a-243">After hello deployment is successful, run hello following script in an elevated PowerShell window (as hello AzureStack\AzureStackAdmin user) on hello development kit host:</span></span>

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

<span data-ttu-id="f0a5a-244">請參閱 SQL Server 遙測 tooconfigure[如何 tooconfigure SQL Server 2016](https://support.microsoft.com/en-us/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft)。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-244">tooconfigure SQL Server telemetry, see [How tooconfigure SQL Server 2016](https://support.microsoft.com/en-us/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft).</span></span>

### <a name="usage-reporting"></a><span data-ttu-id="f0a5a-245">使用量回報</span><span class="sxs-lookup"><span data-stu-id="f0a5a-245">Usage reporting</span></span>

<span data-ttu-id="f0a5a-246">透過註冊，Azure 堆疊也是設定的 tooforward 使用量資訊 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-246">Through registration, Azure Stack is also configured tooforward usage information tooAzure.</span></span> <span data-ttu-id="f0a5a-247">使用量回報是與遙測分別控制的。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-247">Usage reporting is controlled independently from telemetry.</span></span> <span data-ttu-id="f0a5a-248">您可以關閉使用方式報告時[註冊](azure-stack-register.md)Github 上使用 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-248">You can turn off usage reporting when [registering](azure-stack-register.md) by using hello script on Github.</span></span> <span data-ttu-id="f0a5a-249">只要組 hello **$reportUsage**參數太**$false**。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-249">Just set hello **$reportUsage** parameter too**$false**.</span></span>

<span data-ttu-id="f0a5a-250">使用量資料會格式化為中所述的 hello[報表 Azure 堆疊使用方式資料 tooAzure](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-usage-reporting)。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-250">Usage data is formatted as detailed in hello [Report Azure Stack usage data tooAzure](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-usage-reporting).</span></span> <span data-ttu-id="f0a5a-251">「Azure Stack 開發套件」使用者實際上無須付費。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-251">Azure Stack Development Kit users are not actually charged.</span></span> <span data-ttu-id="f0a5a-252">此功能包含在 hello 開發套件，以便您可以測試的 toosee 使用方式報表的運作方式。</span><span class="sxs-lookup"><span data-stu-id="f0a5a-252">This functionality is included in hello development kit so that you can test toosee how usage reporting works.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="f0a5a-253">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0a5a-253">Next steps</span></span>
[<span data-ttu-id="f0a5a-254">下載 hello Azure 堆疊開發套件部署套件</span><span class="sxs-lookup"><span data-stu-id="f0a5a-254">Download hello Azure Stack development kit deployment package</span></span>](https://azure.microsoft.com/overview/azure-stack/try/?v=try)

[<span data-ttu-id="f0a5a-255">部署 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="f0a5a-255">Deploy Azure Stack development kit</span></span>](azure-stack-run-powershell-script.md)

