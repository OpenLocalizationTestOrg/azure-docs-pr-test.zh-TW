---
title: "選取 Linux 的使用者名稱 | Microsoft Docs"
description: "了解如何在 Azure 中選取適用於 Linux 虛擬機器的使用者名稱。"
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
ms.openlocfilehash: 1874d72e5f88816036667932371ff28704d186c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="8d8cb-103">在 Azure 上選取適用於 Linux 的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="8d8cb-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="8d8cb-104">在 Azure 上佈建 Linux 虛擬機器時，您必須指定非根使用者的名稱供稍後使用，以使用登入 VM。</span><span class="sxs-lookup"><span data-stu-id="8d8cb-104">When you provision a Linux virtual machine on Azure you must specify the name of a non-root user that you can later use to log into the VM.</span></span> <span data-ttu-id="8d8cb-105">您可以選擇新使用者的名稱；如果是透過 Azure 傳統入口網站佈建，可以使用預設名稱「azureuser」。</span><span class="sxs-lookup"><span data-stu-id="8d8cb-105">You may choose the name of the new user, or if provisioning via the Azure classic portal you can accept the default name "azureuser".</span></span>

<span data-ttu-id="8d8cb-106">在大多數的情況中，這位使用者不會存在於基本映像中，而是會在佈建程序期間建立。</span><span class="sxs-lookup"><span data-stu-id="8d8cb-106">In most cases this user won't exist on the base image and will be created during the provisioning process.</span></span> <span data-ttu-id="8d8cb-107">若此使用者存在於基本 VM 映像，則 Azure Linux 代理程式只會根據建立 VM 時所指定的資訊，為該使用者設定密碼及 (或) SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="8d8cb-107">If the user exists on the base VM image, then the Azure Linux agent simply configures the password and/or SSH key for that user based on the information you specified when creating the VM.</span></span>

<span data-ttu-id="8d8cb-108">**不過**，Linux 會定義一組不應該使用的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="8d8cb-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="8d8cb-109">如果您嘗試使用現有的系統使用者 (定義為具有 UID 0-99 的使用者) 佈建 Linux VM，佈建程序將 **失敗** 。</span><span class="sxs-lookup"><span data-stu-id="8d8cb-109">The provisioning process will **fail** if you try to provision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="8d8cb-110">常見的範例是 `root` 使用者，其 UID 為 0。</span><span class="sxs-lookup"><span data-stu-id="8d8cb-110">A typical example is the `root` user, which has UID 0.</span></span>

* <span data-ttu-id="8d8cb-111">另請參閱： [Linux 標準基礎 - 使用者 ID 範圍](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="8d8cb-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="8d8cb-112">以下是在 Azure 上佈建 Linux 虛擬機器時應避免使用的 CentOS 和 Ubuntu 常見內建系統使用者清單。</span><span class="sxs-lookup"><span data-stu-id="8d8cb-112">The following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="8d8cb-113">此清單只是範例，請參閱散發套件的文件，以確保您所選擇的使用者名稱沒有與現有的系統使用者衝突。</span><span class="sxs-lookup"><span data-stu-id="8d8cb-113">This list is just an example, please refer to the documentation for your distribution to ensure that the username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="8d8cb-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="8d8cb-114">CentOS</span></span>
* <span data-ttu-id="8d8cb-115">abrt</span><span class="sxs-lookup"><span data-stu-id="8d8cb-115">abrt</span></span>
* <span data-ttu-id="8d8cb-116">adm</span><span class="sxs-lookup"><span data-stu-id="8d8cb-116">adm</span></span>
* <span data-ttu-id="8d8cb-117">audio</span><span class="sxs-lookup"><span data-stu-id="8d8cb-117">audio</span></span>
* <span data-ttu-id="8d8cb-118">bin</span><span class="sxs-lookup"><span data-stu-id="8d8cb-118">bin</span></span>
* <span data-ttu-id="8d8cb-119">cdrom</span><span class="sxs-lookup"><span data-stu-id="8d8cb-119">cdrom</span></span>
* <span data-ttu-id="8d8cb-120">cgred</span><span class="sxs-lookup"><span data-stu-id="8d8cb-120">cgred</span></span>
* <span data-ttu-id="8d8cb-121">daemon</span><span class="sxs-lookup"><span data-stu-id="8d8cb-121">daemon</span></span>
* <span data-ttu-id="8d8cb-122">dbus</span><span class="sxs-lookup"><span data-stu-id="8d8cb-122">dbus</span></span>
* <span data-ttu-id="8d8cb-123">dialout</span><span class="sxs-lookup"><span data-stu-id="8d8cb-123">dialout</span></span>
* <span data-ttu-id="8d8cb-124">dip</span><span class="sxs-lookup"><span data-stu-id="8d8cb-124">dip</span></span>
* <span data-ttu-id="8d8cb-125">disk</span><span class="sxs-lookup"><span data-stu-id="8d8cb-125">disk</span></span>
* <span data-ttu-id="8d8cb-126">floppy</span><span class="sxs-lookup"><span data-stu-id="8d8cb-126">floppy</span></span>
* <span data-ttu-id="8d8cb-127">ftp</span><span class="sxs-lookup"><span data-stu-id="8d8cb-127">ftp</span></span>
* <span data-ttu-id="8d8cb-128">ftp</span><span class="sxs-lookup"><span data-stu-id="8d8cb-128">ftp</span></span>
* <span data-ttu-id="8d8cb-129">games</span><span class="sxs-lookup"><span data-stu-id="8d8cb-129">games</span></span>
* <span data-ttu-id="8d8cb-130">gopher</span><span class="sxs-lookup"><span data-stu-id="8d8cb-130">gopher</span></span>
* <span data-ttu-id="8d8cb-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="8d8cb-131">haldaemon</span></span>
* <span data-ttu-id="8d8cb-132">halt</span><span class="sxs-lookup"><span data-stu-id="8d8cb-132">halt</span></span>
* <span data-ttu-id="8d8cb-133">kmem</span><span class="sxs-lookup"><span data-stu-id="8d8cb-133">kmem</span></span>
* <span data-ttu-id="8d8cb-134">lock</span><span class="sxs-lookup"><span data-stu-id="8d8cb-134">lock</span></span>
* <span data-ttu-id="8d8cb-135">lp</span><span class="sxs-lookup"><span data-stu-id="8d8cb-135">lp</span></span>
* <span data-ttu-id="8d8cb-136">mail</span><span class="sxs-lookup"><span data-stu-id="8d8cb-136">mail</span></span>
* <span data-ttu-id="8d8cb-137">man</span><span class="sxs-lookup"><span data-stu-id="8d8cb-137">man</span></span>
* <span data-ttu-id="8d8cb-138">mem</span><span class="sxs-lookup"><span data-stu-id="8d8cb-138">mem</span></span>
* <span data-ttu-id="8d8cb-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="8d8cb-139">nfsnobody</span></span>
* <span data-ttu-id="8d8cb-140">nobody</span><span class="sxs-lookup"><span data-stu-id="8d8cb-140">nobody</span></span>
* <span data-ttu-id="8d8cb-141">ntp</span><span class="sxs-lookup"><span data-stu-id="8d8cb-141">ntp</span></span>
* <span data-ttu-id="8d8cb-142">operator</span><span class="sxs-lookup"><span data-stu-id="8d8cb-142">operator</span></span>
* <span data-ttu-id="8d8cb-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="8d8cb-143">oprofile</span></span>
* <span data-ttu-id="8d8cb-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="8d8cb-144">postdrop</span></span>
* <span data-ttu-id="8d8cb-145">postfix</span><span class="sxs-lookup"><span data-stu-id="8d8cb-145">postfix</span></span>
* <span data-ttu-id="8d8cb-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="8d8cb-146">qpidd</span></span>
* <span data-ttu-id="8d8cb-147">root</span><span class="sxs-lookup"><span data-stu-id="8d8cb-147">root</span></span>
* <span data-ttu-id="8d8cb-148">rpc</span><span class="sxs-lookup"><span data-stu-id="8d8cb-148">rpc</span></span>
* <span data-ttu-id="8d8cb-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="8d8cb-149">rpcuser</span></span>
* <span data-ttu-id="8d8cb-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="8d8cb-150">saslauth</span></span>
* <span data-ttu-id="8d8cb-151">shutdown</span><span class="sxs-lookup"><span data-stu-id="8d8cb-151">shutdown</span></span>
* <span data-ttu-id="8d8cb-152">slocate</span><span class="sxs-lookup"><span data-stu-id="8d8cb-152">slocate</span></span>
* <span data-ttu-id="8d8cb-153">sshd</span><span class="sxs-lookup"><span data-stu-id="8d8cb-153">sshd</span></span>
* <span data-ttu-id="8d8cb-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="8d8cb-154">stapdev</span></span>
* <span data-ttu-id="8d8cb-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="8d8cb-155">stapusr</span></span>
* <span data-ttu-id="8d8cb-156">sync</span><span class="sxs-lookup"><span data-stu-id="8d8cb-156">sync</span></span>
* <span data-ttu-id="8d8cb-157">sys</span><span class="sxs-lookup"><span data-stu-id="8d8cb-157">sys</span></span>
* <span data-ttu-id="8d8cb-158">tape</span><span class="sxs-lookup"><span data-stu-id="8d8cb-158">tape</span></span>
* <span data-ttu-id="8d8cb-159">test</span><span class="sxs-lookup"><span data-stu-id="8d8cb-159">test</span></span>
* <span data-ttu-id="8d8cb-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="8d8cb-160">tcpdump</span></span>
* <span data-ttu-id="8d8cb-161">tty</span><span class="sxs-lookup"><span data-stu-id="8d8cb-161">tty</span></span>
* <span data-ttu-id="8d8cb-162">users</span><span class="sxs-lookup"><span data-stu-id="8d8cb-162">users</span></span>
* <span data-ttu-id="8d8cb-163">utempter</span><span class="sxs-lookup"><span data-stu-id="8d8cb-163">utempter</span></span>
* <span data-ttu-id="8d8cb-164">utmp</span><span class="sxs-lookup"><span data-stu-id="8d8cb-164">utmp</span></span>
* <span data-ttu-id="8d8cb-165">uucp</span><span class="sxs-lookup"><span data-stu-id="8d8cb-165">uucp</span></span>
* <span data-ttu-id="8d8cb-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="8d8cb-166">vcsa</span></span>
* <span data-ttu-id="8d8cb-167">video</span><span class="sxs-lookup"><span data-stu-id="8d8cb-167">video</span></span>
* <span data-ttu-id="8d8cb-168">wheel</span><span class="sxs-lookup"><span data-stu-id="8d8cb-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="8d8cb-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="8d8cb-169">Ubuntu</span></span>
* <span data-ttu-id="8d8cb-170">adm</span><span class="sxs-lookup"><span data-stu-id="8d8cb-170">adm</span></span>
* <span data-ttu-id="8d8cb-171">admin</span><span class="sxs-lookup"><span data-stu-id="8d8cb-171">admin</span></span>
* <span data-ttu-id="8d8cb-172">audio</span><span class="sxs-lookup"><span data-stu-id="8d8cb-172">audio</span></span>
* <span data-ttu-id="8d8cb-173">backup</span><span class="sxs-lookup"><span data-stu-id="8d8cb-173">backup</span></span>
* <span data-ttu-id="8d8cb-174">bin</span><span class="sxs-lookup"><span data-stu-id="8d8cb-174">bin</span></span>
* <span data-ttu-id="8d8cb-175">cdrom</span><span class="sxs-lookup"><span data-stu-id="8d8cb-175">cdrom</span></span>
* <span data-ttu-id="8d8cb-176">crontab</span><span class="sxs-lookup"><span data-stu-id="8d8cb-176">crontab</span></span>
* <span data-ttu-id="8d8cb-177">daemon</span><span class="sxs-lookup"><span data-stu-id="8d8cb-177">daemon</span></span>
* <span data-ttu-id="8d8cb-178">dialout</span><span class="sxs-lookup"><span data-stu-id="8d8cb-178">dialout</span></span>
* <span data-ttu-id="8d8cb-179">dip</span><span class="sxs-lookup"><span data-stu-id="8d8cb-179">dip</span></span>
* <span data-ttu-id="8d8cb-180">disk</span><span class="sxs-lookup"><span data-stu-id="8d8cb-180">disk</span></span>
* <span data-ttu-id="8d8cb-181">fax</span><span class="sxs-lookup"><span data-stu-id="8d8cb-181">fax</span></span>
* <span data-ttu-id="8d8cb-182">floppy</span><span class="sxs-lookup"><span data-stu-id="8d8cb-182">floppy</span></span>
* <span data-ttu-id="8d8cb-183">fuse</span><span class="sxs-lookup"><span data-stu-id="8d8cb-183">fuse</span></span>
* <span data-ttu-id="8d8cb-184">games</span><span class="sxs-lookup"><span data-stu-id="8d8cb-184">games</span></span>
* <span data-ttu-id="8d8cb-185">gnats</span><span class="sxs-lookup"><span data-stu-id="8d8cb-185">gnats</span></span>
* <span data-ttu-id="8d8cb-186">irc</span><span class="sxs-lookup"><span data-stu-id="8d8cb-186">irc</span></span>
* <span data-ttu-id="8d8cb-187">kmem</span><span class="sxs-lookup"><span data-stu-id="8d8cb-187">kmem</span></span>
* <span data-ttu-id="8d8cb-188">landscape</span><span class="sxs-lookup"><span data-stu-id="8d8cb-188">landscape</span></span>
* <span data-ttu-id="8d8cb-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="8d8cb-189">libuuid</span></span>
* <span data-ttu-id="8d8cb-190">list</span><span class="sxs-lookup"><span data-stu-id="8d8cb-190">list</span></span>
* <span data-ttu-id="8d8cb-191">lp</span><span class="sxs-lookup"><span data-stu-id="8d8cb-191">lp</span></span>
* <span data-ttu-id="8d8cb-192">mail</span><span class="sxs-lookup"><span data-stu-id="8d8cb-192">mail</span></span>
* <span data-ttu-id="8d8cb-193">man</span><span class="sxs-lookup"><span data-stu-id="8d8cb-193">man</span></span>
* <span data-ttu-id="8d8cb-194">messagebus</span><span class="sxs-lookup"><span data-stu-id="8d8cb-194">messagebus</span></span>
* <span data-ttu-id="8d8cb-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="8d8cb-195">mlocate</span></span>
* <span data-ttu-id="8d8cb-196">netdev</span><span class="sxs-lookup"><span data-stu-id="8d8cb-196">netdev</span></span>
* <span data-ttu-id="8d8cb-197">news</span><span class="sxs-lookup"><span data-stu-id="8d8cb-197">news</span></span>
* <span data-ttu-id="8d8cb-198">nobody</span><span class="sxs-lookup"><span data-stu-id="8d8cb-198">nobody</span></span>
* <span data-ttu-id="8d8cb-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="8d8cb-199">nogroup</span></span>
* <span data-ttu-id="8d8cb-200">operator</span><span class="sxs-lookup"><span data-stu-id="8d8cb-200">operator</span></span>
* <span data-ttu-id="8d8cb-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="8d8cb-201">plugdev</span></span>
* <span data-ttu-id="8d8cb-202">proxy</span><span class="sxs-lookup"><span data-stu-id="8d8cb-202">proxy</span></span>
* <span data-ttu-id="8d8cb-203">root</span><span class="sxs-lookup"><span data-stu-id="8d8cb-203">root</span></span>
* <span data-ttu-id="8d8cb-204">sasl</span><span class="sxs-lookup"><span data-stu-id="8d8cb-204">sasl</span></span>
* <span data-ttu-id="8d8cb-205">shadow</span><span class="sxs-lookup"><span data-stu-id="8d8cb-205">shadow</span></span>
* <span data-ttu-id="8d8cb-206">src</span><span class="sxs-lookup"><span data-stu-id="8d8cb-206">src</span></span>
* <span data-ttu-id="8d8cb-207">ssh</span><span class="sxs-lookup"><span data-stu-id="8d8cb-207">ssh</span></span>
* <span data-ttu-id="8d8cb-208">sshd</span><span class="sxs-lookup"><span data-stu-id="8d8cb-208">sshd</span></span>
* <span data-ttu-id="8d8cb-209">staff</span><span class="sxs-lookup"><span data-stu-id="8d8cb-209">staff</span></span>
* <span data-ttu-id="8d8cb-210">sudo</span><span class="sxs-lookup"><span data-stu-id="8d8cb-210">sudo</span></span>
* <span data-ttu-id="8d8cb-211">sync</span><span class="sxs-lookup"><span data-stu-id="8d8cb-211">sync</span></span>
* <span data-ttu-id="8d8cb-212">sys</span><span class="sxs-lookup"><span data-stu-id="8d8cb-212">sys</span></span>
* <span data-ttu-id="8d8cb-213">syslog</span><span class="sxs-lookup"><span data-stu-id="8d8cb-213">syslog</span></span>
* <span data-ttu-id="8d8cb-214">tape</span><span class="sxs-lookup"><span data-stu-id="8d8cb-214">tape</span></span>
* <span data-ttu-id="8d8cb-215">tty</span><span class="sxs-lookup"><span data-stu-id="8d8cb-215">tty</span></span>
* <span data-ttu-id="8d8cb-216">users</span><span class="sxs-lookup"><span data-stu-id="8d8cb-216">users</span></span>
* <span data-ttu-id="8d8cb-217">utmp</span><span class="sxs-lookup"><span data-stu-id="8d8cb-217">utmp</span></span>
* <span data-ttu-id="8d8cb-218">uucp</span><span class="sxs-lookup"><span data-stu-id="8d8cb-218">uucp</span></span>
* <span data-ttu-id="8d8cb-219">video</span><span class="sxs-lookup"><span data-stu-id="8d8cb-219">video</span></span>
* <span data-ttu-id="8d8cb-220">voice</span><span class="sxs-lookup"><span data-stu-id="8d8cb-220">voice</span></span>
* <span data-ttu-id="8d8cb-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="8d8cb-221">whoopsie</span></span>
* <span data-ttu-id="8d8cb-222">www-data</span><span class="sxs-lookup"><span data-stu-id="8d8cb-222">www-data</span></span>

