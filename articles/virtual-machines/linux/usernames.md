---
title: "aaaSelecting 適用於 Linux 的使用者名稱 |Microsoft 文件"
description: "了解如何 tooselect 使用者名稱在 Azure 中 Linux 虛擬機器。"
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="f1241-103">在 Azure 上選取適用於 Linux 的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="f1241-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="f1241-104">在佈建在 Azure 上的 Linux 虛擬機器時，您必須指定 hello 您稍後可以使用 toolog 到 hello VM 的非根使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f1241-104">When you provision a Linux virtual machine on Azure you must specify hello name of a non-root user that you can later use toolog into hello VM.</span></span> <span data-ttu-id="f1241-105">您可以選擇 hello hello 新的使用者名稱，或如果透過佈建 hello Azure 傳統入口網站，您可以接受 hello 預設名稱 「 azureuser"。</span><span class="sxs-lookup"><span data-stu-id="f1241-105">You may choose hello name of hello new user, or if provisioning via hello Azure classic portal you can accept hello default name "azureuser".</span></span>

<span data-ttu-id="f1241-106">在大部分情況下這位使用者不存在於 hello 基底映像，並將 hello 佈建程序期間建立。</span><span class="sxs-lookup"><span data-stu-id="f1241-106">In most cases this user won't exist on hello base image and will be created during hello provisioning process.</span></span> <span data-ttu-id="f1241-107">如果 hello 使用者存在於 hello 基底 VM 映像，然後 hello Azure Linux 代理程式只會設定 hello 密碼及/或根據 hello 資訊建立 hello VM 時，您會指定該使用者的 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="f1241-107">If hello user exists on hello base VM image, then hello Azure Linux agent simply configures hello password and/or SSH key for that user based on hello information you specified when creating hello VM.</span></span>

<span data-ttu-id="f1241-108">**不過**，Linux 會定義一組不應該使用的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f1241-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="f1241-109">佈建程序將 hello**失敗**如果您嘗試 tooprovision Linux VM，使用現有的系統使用者，定義為具有 UID 0-99 之間的使用者。</span><span class="sxs-lookup"><span data-stu-id="f1241-109">hello provisioning process will **fail** if you try tooprovision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="f1241-110">典型的範例為 hello`root`使用者具有 UID 0。</span><span class="sxs-lookup"><span data-stu-id="f1241-110">A typical example is hello `root` user, which has UID 0.</span></span>

* <span data-ttu-id="f1241-111">另請參閱： [Linux 標準基礎 - 使用者 ID 範圍](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="f1241-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="f1241-112">hello 以下是 CentOS 和 Ubuntu，您應該避免使用佈建在 Azure 上的 Linux 虛擬機器時通用的內建的系統使用者的清單。</span><span class="sxs-lookup"><span data-stu-id="f1241-112">hello following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="f1241-113">這份清單不只是範例，請參閱 toohello 文件的發佈 tooensure 該 hello 使用者名稱與現有的系統使用者選擇 不會衝突。</span><span class="sxs-lookup"><span data-stu-id="f1241-113">This list is just an example, please refer toohello documentation for your distribution tooensure that hello username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="f1241-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="f1241-114">CentOS</span></span>
* <span data-ttu-id="f1241-115">abrt</span><span class="sxs-lookup"><span data-stu-id="f1241-115">abrt</span></span>
* <span data-ttu-id="f1241-116">adm</span><span class="sxs-lookup"><span data-stu-id="f1241-116">adm</span></span>
* <span data-ttu-id="f1241-117">audio</span><span class="sxs-lookup"><span data-stu-id="f1241-117">audio</span></span>
* <span data-ttu-id="f1241-118">bin</span><span class="sxs-lookup"><span data-stu-id="f1241-118">bin</span></span>
* <span data-ttu-id="f1241-119">cdrom</span><span class="sxs-lookup"><span data-stu-id="f1241-119">cdrom</span></span>
* <span data-ttu-id="f1241-120">cgred</span><span class="sxs-lookup"><span data-stu-id="f1241-120">cgred</span></span>
* <span data-ttu-id="f1241-121">daemon</span><span class="sxs-lookup"><span data-stu-id="f1241-121">daemon</span></span>
* <span data-ttu-id="f1241-122">dbus</span><span class="sxs-lookup"><span data-stu-id="f1241-122">dbus</span></span>
* <span data-ttu-id="f1241-123">dialout</span><span class="sxs-lookup"><span data-stu-id="f1241-123">dialout</span></span>
* <span data-ttu-id="f1241-124">dip</span><span class="sxs-lookup"><span data-stu-id="f1241-124">dip</span></span>
* <span data-ttu-id="f1241-125">disk</span><span class="sxs-lookup"><span data-stu-id="f1241-125">disk</span></span>
* <span data-ttu-id="f1241-126">floppy</span><span class="sxs-lookup"><span data-stu-id="f1241-126">floppy</span></span>
* <span data-ttu-id="f1241-127">ftp</span><span class="sxs-lookup"><span data-stu-id="f1241-127">ftp</span></span>
* <span data-ttu-id="f1241-128">ftp</span><span class="sxs-lookup"><span data-stu-id="f1241-128">ftp</span></span>
* <span data-ttu-id="f1241-129">games</span><span class="sxs-lookup"><span data-stu-id="f1241-129">games</span></span>
* <span data-ttu-id="f1241-130">gopher</span><span class="sxs-lookup"><span data-stu-id="f1241-130">gopher</span></span>
* <span data-ttu-id="f1241-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="f1241-131">haldaemon</span></span>
* <span data-ttu-id="f1241-132">halt</span><span class="sxs-lookup"><span data-stu-id="f1241-132">halt</span></span>
* <span data-ttu-id="f1241-133">kmem</span><span class="sxs-lookup"><span data-stu-id="f1241-133">kmem</span></span>
* <span data-ttu-id="f1241-134">lock</span><span class="sxs-lookup"><span data-stu-id="f1241-134">lock</span></span>
* <span data-ttu-id="f1241-135">lp</span><span class="sxs-lookup"><span data-stu-id="f1241-135">lp</span></span>
* <span data-ttu-id="f1241-136">mail</span><span class="sxs-lookup"><span data-stu-id="f1241-136">mail</span></span>
* <span data-ttu-id="f1241-137">man</span><span class="sxs-lookup"><span data-stu-id="f1241-137">man</span></span>
* <span data-ttu-id="f1241-138">mem</span><span class="sxs-lookup"><span data-stu-id="f1241-138">mem</span></span>
* <span data-ttu-id="f1241-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="f1241-139">nfsnobody</span></span>
* <span data-ttu-id="f1241-140">nobody</span><span class="sxs-lookup"><span data-stu-id="f1241-140">nobody</span></span>
* <span data-ttu-id="f1241-141">ntp</span><span class="sxs-lookup"><span data-stu-id="f1241-141">ntp</span></span>
* <span data-ttu-id="f1241-142">operator</span><span class="sxs-lookup"><span data-stu-id="f1241-142">operator</span></span>
* <span data-ttu-id="f1241-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="f1241-143">oprofile</span></span>
* <span data-ttu-id="f1241-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="f1241-144">postdrop</span></span>
* <span data-ttu-id="f1241-145">postfix</span><span class="sxs-lookup"><span data-stu-id="f1241-145">postfix</span></span>
* <span data-ttu-id="f1241-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="f1241-146">qpidd</span></span>
* <span data-ttu-id="f1241-147">root</span><span class="sxs-lookup"><span data-stu-id="f1241-147">root</span></span>
* <span data-ttu-id="f1241-148">rpc</span><span class="sxs-lookup"><span data-stu-id="f1241-148">rpc</span></span>
* <span data-ttu-id="f1241-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="f1241-149">rpcuser</span></span>
* <span data-ttu-id="f1241-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="f1241-150">saslauth</span></span>
* <span data-ttu-id="f1241-151">shutdown</span><span class="sxs-lookup"><span data-stu-id="f1241-151">shutdown</span></span>
* <span data-ttu-id="f1241-152">slocate</span><span class="sxs-lookup"><span data-stu-id="f1241-152">slocate</span></span>
* <span data-ttu-id="f1241-153">sshd</span><span class="sxs-lookup"><span data-stu-id="f1241-153">sshd</span></span>
* <span data-ttu-id="f1241-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="f1241-154">stapdev</span></span>
* <span data-ttu-id="f1241-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="f1241-155">stapusr</span></span>
* <span data-ttu-id="f1241-156">sync</span><span class="sxs-lookup"><span data-stu-id="f1241-156">sync</span></span>
* <span data-ttu-id="f1241-157">sys</span><span class="sxs-lookup"><span data-stu-id="f1241-157">sys</span></span>
* <span data-ttu-id="f1241-158">tape</span><span class="sxs-lookup"><span data-stu-id="f1241-158">tape</span></span>
* <span data-ttu-id="f1241-159">test</span><span class="sxs-lookup"><span data-stu-id="f1241-159">test</span></span>
* <span data-ttu-id="f1241-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="f1241-160">tcpdump</span></span>
* <span data-ttu-id="f1241-161">tty</span><span class="sxs-lookup"><span data-stu-id="f1241-161">tty</span></span>
* <span data-ttu-id="f1241-162">users</span><span class="sxs-lookup"><span data-stu-id="f1241-162">users</span></span>
* <span data-ttu-id="f1241-163">utempter</span><span class="sxs-lookup"><span data-stu-id="f1241-163">utempter</span></span>
* <span data-ttu-id="f1241-164">utmp</span><span class="sxs-lookup"><span data-stu-id="f1241-164">utmp</span></span>
* <span data-ttu-id="f1241-165">uucp</span><span class="sxs-lookup"><span data-stu-id="f1241-165">uucp</span></span>
* <span data-ttu-id="f1241-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="f1241-166">vcsa</span></span>
* <span data-ttu-id="f1241-167">video</span><span class="sxs-lookup"><span data-stu-id="f1241-167">video</span></span>
* <span data-ttu-id="f1241-168">wheel</span><span class="sxs-lookup"><span data-stu-id="f1241-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="f1241-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="f1241-169">Ubuntu</span></span>
* <span data-ttu-id="f1241-170">adm</span><span class="sxs-lookup"><span data-stu-id="f1241-170">adm</span></span>
* <span data-ttu-id="f1241-171">admin</span><span class="sxs-lookup"><span data-stu-id="f1241-171">admin</span></span>
* <span data-ttu-id="f1241-172">audio</span><span class="sxs-lookup"><span data-stu-id="f1241-172">audio</span></span>
* <span data-ttu-id="f1241-173">backup</span><span class="sxs-lookup"><span data-stu-id="f1241-173">backup</span></span>
* <span data-ttu-id="f1241-174">bin</span><span class="sxs-lookup"><span data-stu-id="f1241-174">bin</span></span>
* <span data-ttu-id="f1241-175">cdrom</span><span class="sxs-lookup"><span data-stu-id="f1241-175">cdrom</span></span>
* <span data-ttu-id="f1241-176">crontab</span><span class="sxs-lookup"><span data-stu-id="f1241-176">crontab</span></span>
* <span data-ttu-id="f1241-177">daemon</span><span class="sxs-lookup"><span data-stu-id="f1241-177">daemon</span></span>
* <span data-ttu-id="f1241-178">dialout</span><span class="sxs-lookup"><span data-stu-id="f1241-178">dialout</span></span>
* <span data-ttu-id="f1241-179">dip</span><span class="sxs-lookup"><span data-stu-id="f1241-179">dip</span></span>
* <span data-ttu-id="f1241-180">disk</span><span class="sxs-lookup"><span data-stu-id="f1241-180">disk</span></span>
* <span data-ttu-id="f1241-181">fax</span><span class="sxs-lookup"><span data-stu-id="f1241-181">fax</span></span>
* <span data-ttu-id="f1241-182">floppy</span><span class="sxs-lookup"><span data-stu-id="f1241-182">floppy</span></span>
* <span data-ttu-id="f1241-183">fuse</span><span class="sxs-lookup"><span data-stu-id="f1241-183">fuse</span></span>
* <span data-ttu-id="f1241-184">games</span><span class="sxs-lookup"><span data-stu-id="f1241-184">games</span></span>
* <span data-ttu-id="f1241-185">gnats</span><span class="sxs-lookup"><span data-stu-id="f1241-185">gnats</span></span>
* <span data-ttu-id="f1241-186">irc</span><span class="sxs-lookup"><span data-stu-id="f1241-186">irc</span></span>
* <span data-ttu-id="f1241-187">kmem</span><span class="sxs-lookup"><span data-stu-id="f1241-187">kmem</span></span>
* <span data-ttu-id="f1241-188">landscape</span><span class="sxs-lookup"><span data-stu-id="f1241-188">landscape</span></span>
* <span data-ttu-id="f1241-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="f1241-189">libuuid</span></span>
* <span data-ttu-id="f1241-190">list</span><span class="sxs-lookup"><span data-stu-id="f1241-190">list</span></span>
* <span data-ttu-id="f1241-191">lp</span><span class="sxs-lookup"><span data-stu-id="f1241-191">lp</span></span>
* <span data-ttu-id="f1241-192">mail</span><span class="sxs-lookup"><span data-stu-id="f1241-192">mail</span></span>
* <span data-ttu-id="f1241-193">man</span><span class="sxs-lookup"><span data-stu-id="f1241-193">man</span></span>
* <span data-ttu-id="f1241-194">messagebus</span><span class="sxs-lookup"><span data-stu-id="f1241-194">messagebus</span></span>
* <span data-ttu-id="f1241-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="f1241-195">mlocate</span></span>
* <span data-ttu-id="f1241-196">netdev</span><span class="sxs-lookup"><span data-stu-id="f1241-196">netdev</span></span>
* <span data-ttu-id="f1241-197">news</span><span class="sxs-lookup"><span data-stu-id="f1241-197">news</span></span>
* <span data-ttu-id="f1241-198">nobody</span><span class="sxs-lookup"><span data-stu-id="f1241-198">nobody</span></span>
* <span data-ttu-id="f1241-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="f1241-199">nogroup</span></span>
* <span data-ttu-id="f1241-200">operator</span><span class="sxs-lookup"><span data-stu-id="f1241-200">operator</span></span>
* <span data-ttu-id="f1241-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="f1241-201">plugdev</span></span>
* <span data-ttu-id="f1241-202">proxy</span><span class="sxs-lookup"><span data-stu-id="f1241-202">proxy</span></span>
* <span data-ttu-id="f1241-203">root</span><span class="sxs-lookup"><span data-stu-id="f1241-203">root</span></span>
* <span data-ttu-id="f1241-204">sasl</span><span class="sxs-lookup"><span data-stu-id="f1241-204">sasl</span></span>
* <span data-ttu-id="f1241-205">shadow</span><span class="sxs-lookup"><span data-stu-id="f1241-205">shadow</span></span>
* <span data-ttu-id="f1241-206">src</span><span class="sxs-lookup"><span data-stu-id="f1241-206">src</span></span>
* <span data-ttu-id="f1241-207">ssh</span><span class="sxs-lookup"><span data-stu-id="f1241-207">ssh</span></span>
* <span data-ttu-id="f1241-208">sshd</span><span class="sxs-lookup"><span data-stu-id="f1241-208">sshd</span></span>
* <span data-ttu-id="f1241-209">staff</span><span class="sxs-lookup"><span data-stu-id="f1241-209">staff</span></span>
* <span data-ttu-id="f1241-210">sudo</span><span class="sxs-lookup"><span data-stu-id="f1241-210">sudo</span></span>
* <span data-ttu-id="f1241-211">sync</span><span class="sxs-lookup"><span data-stu-id="f1241-211">sync</span></span>
* <span data-ttu-id="f1241-212">sys</span><span class="sxs-lookup"><span data-stu-id="f1241-212">sys</span></span>
* <span data-ttu-id="f1241-213">syslog</span><span class="sxs-lookup"><span data-stu-id="f1241-213">syslog</span></span>
* <span data-ttu-id="f1241-214">tape</span><span class="sxs-lookup"><span data-stu-id="f1241-214">tape</span></span>
* <span data-ttu-id="f1241-215">tty</span><span class="sxs-lookup"><span data-stu-id="f1241-215">tty</span></span>
* <span data-ttu-id="f1241-216">users</span><span class="sxs-lookup"><span data-stu-id="f1241-216">users</span></span>
* <span data-ttu-id="f1241-217">utmp</span><span class="sxs-lookup"><span data-stu-id="f1241-217">utmp</span></span>
* <span data-ttu-id="f1241-218">uucp</span><span class="sxs-lookup"><span data-stu-id="f1241-218">uucp</span></span>
* <span data-ttu-id="f1241-219">video</span><span class="sxs-lookup"><span data-stu-id="f1241-219">video</span></span>
* <span data-ttu-id="f1241-220">voice</span><span class="sxs-lookup"><span data-stu-id="f1241-220">voice</span></span>
* <span data-ttu-id="f1241-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="f1241-221">whoopsie</span></span>
* <span data-ttu-id="f1241-222">www-data</span><span class="sxs-lookup"><span data-stu-id="f1241-222">www-data</span></span>

