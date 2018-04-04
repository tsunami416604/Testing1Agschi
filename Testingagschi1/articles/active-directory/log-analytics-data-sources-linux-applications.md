---
title: "在 OMS Log Analytics 中收集 Linux 应用程序性能数据 | Microsoft Docs"
description: "本文提供了有关对用于 Linux 的 OMS 代理进行配置以收集 MySQL 和 Apache HTTP Server 的性能计数器的详细信息。"
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 04ea6f728e59ec8b47e54fe45e1adc6cbbfb85ff
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2017
---
# <a name="collect-performance-counters-for-linux-applications-in-log-analytics"></a><span data-ttu-id="ecd7b-103">在 Log Analytics 中收集 Linux 应用程序的性能计数器</span><span class="sxs-lookup"><span data-stu-id="ecd7b-103">Collect performance counters for Linux applications in Log Analytics</span></span> 
<span data-ttu-id="ecd7b-104">本文提供了有关对[用于 Linux 的 OMS 代理](https://github.com/Microsoft/OMS-Agent-for-Linux)进行配置以收集特定应用程序的性能计数器的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-104">This article provides details for configuring the [OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) to collect performance counters for specific applications.</span></span>  <span data-ttu-id="ecd7b-105">本文中包括的应用程序有：</span><span class="sxs-lookup"><span data-stu-id="ecd7b-105">The applications included in this article are:</span></span>  

- [<span data-ttu-id="ecd7b-106">MySQL</span><span class="sxs-lookup"><span data-stu-id="ecd7b-106">MySQL</span></span>](#MySQL)
- [<span data-ttu-id="ecd7b-107">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-107">Apache HTTP Server</span></span>](#apache-http-server)

## <a name="mysql"></a><span data-ttu-id="ecd7b-108">MySQL</span><span class="sxs-lookup"><span data-stu-id="ecd7b-108">MySQL</span></span>
<span data-ttu-id="ecd7b-109">如果安装 OMS 代理时在计算机上检测到 MySQL 服务器或 MariaDB 服务器，则会自动安装 MySQL 服务器的性能监视提供程序。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-109">If MySQL Server or MariaDB Server is detected on the computer when the OMS agent is installed, a performance monitoring provider for MySQL Server will be automatically installed.</span></span> <span data-ttu-id="ecd7b-110">此提供程序连接到本地 MySQL/MariaDB 服务器以公开性能统计信息。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-110">This provider connects to the local MySQL/MariaDB server to expose performance statistics.</span></span> <span data-ttu-id="ecd7b-111">必须配置 MySQL 用户凭据，以便提供程序能够访问 MySQL 服务器。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-111">MySQL user credentials must be configured so that the provider can access the MySQL Server.</span></span>

### <a name="configure-mysql-credentials"></a><span data-ttu-id="ecd7b-112">配置 MySQL 凭据</span><span class="sxs-lookup"><span data-stu-id="ecd7b-112">Configure MySQL credentials</span></span>
<span data-ttu-id="ecd7b-113">MySQL OMI 提供程序需要预先配置 MySQL 用户并安装 MySQL 客户端库，才能从 MySQL 实例中查询性能和运行状况信息。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-113">The MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order to query the performance and health information from the MySQL instance.</span></span>  <span data-ttu-id="ecd7b-114">这些凭据存储在 Linux 代理上存储的一个身份验证文件中。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-114">These credentials are stored in an authentication file that's stored on the Linux agent.</span></span>  <span data-ttu-id="ecd7b-115">该身份验证文件指定了 MySQL 实例正在侦听的绑定地址和端口以及用于收集指标的凭据。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-115">The authentication file specifies what bind-address and port the MySQL instance is listening on and what credentials to use to gather metrics.</span></span>  

<span data-ttu-id="ecd7b-116">在安装用于 Linux 的 OMS 代理期间，MySQL OMI 提供程序会在 MySQL my.cnf 配置文件（默认位置）中扫描绑定地址和端口并对 MySQL OMI 身份验证文件进行部分设置。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-116">During installation of the OMS Agent for Linux the MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set the MySQL OMI authentication file.</span></span>

<span data-ttu-id="ecd7b-117">MySQL 身份验证文件存储在 `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth` 处。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-117">The MySQL authentication file is stored at `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`.</span></span>


### <a name="authentication-file-format"></a><span data-ttu-id="ecd7b-118">身份验证文件格式</span><span class="sxs-lookup"><span data-stu-id="ecd7b-118">Authentication file format</span></span>
<span data-ttu-id="ecd7b-119">下面是 MySQL OMI 身份验证文件的格式</span><span class="sxs-lookup"><span data-stu-id="ecd7b-119">Following is the format for the MySQL OMI authentication file</span></span>

    [Port]=[Bind-Address], [username], [Base64 encoded Password]
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    AutoUpdate=[true|false]

<span data-ttu-id="ecd7b-120">下表描述了身份验证文件中的条目。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-120">The entries in the authentication file are described in the following table.</span></span>

| <span data-ttu-id="ecd7b-121">属性</span><span class="sxs-lookup"><span data-stu-id="ecd7b-121">Property</span></span> | <span data-ttu-id="ecd7b-122">说明</span><span class="sxs-lookup"><span data-stu-id="ecd7b-122">Description</span></span> |
|:--|:--|
| <span data-ttu-id="ecd7b-123">端口</span><span class="sxs-lookup"><span data-stu-id="ecd7b-123">Port</span></span> | <span data-ttu-id="ecd7b-124">表示 MySQL 实例正在侦听的当前端口。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-124">Represents the current port the MySQL instance is listening on.</span></span> <span data-ttu-id="ecd7b-125">端口 0 指定后面的属性用于默认实例。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-125">Port 0 specifies that the properties following are used for default instance.</span></span> |
| <span data-ttu-id="ecd7b-126">Bind-Address</span><span class="sxs-lookup"><span data-stu-id="ecd7b-126">Bind-Address</span></span>| <span data-ttu-id="ecd7b-127">当前 MySQL 绑定地址。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-127">Current MySQL bind-address.</span></span> |
| <span data-ttu-id="ecd7b-128">username</span><span class="sxs-lookup"><span data-stu-id="ecd7b-128">username</span></span>| <span data-ttu-id="ecd7b-129">用来监视 MySQL 服务器实例的 MySQL 用户。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-129">MySQL user used to use to monitor the MySQL server instance.</span></span> |
| <span data-ttu-id="ecd7b-130">Base64 编码的密码</span><span class="sxs-lookup"><span data-stu-id="ecd7b-130">Base64 encoded Password</span></span>| <span data-ttu-id="ecd7b-131">MySQL 监视用户的密码（采用 Base64 编码）。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-131">Password of the MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="ecd7b-132">AutoUpdate</span><span class="sxs-lookup"><span data-stu-id="ecd7b-132">AutoUpdate</span></span>| <span data-ttu-id="ecd7b-133">指定当升级 MySQL OMI 提供程序时，是否将重新扫描 my.cnf 文件中的更改并覆盖 MySQL OMI 身份验证文件。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-133">Specifies whether to rescan for changes in the my.cnf file and overwrite the MySQL OMI Authentication file when the MySQL OMI Provider is upgraded.</span></span> |

### <a name="default-instance"></a><span data-ttu-id="ecd7b-134">默认实例</span><span class="sxs-lookup"><span data-stu-id="ecd7b-134">Default instance</span></span>
<span data-ttu-id="ecd7b-135">MySQL OMI 身份验证文件可以定义一个默认的实例和端口号，以便更轻松地管理一台 Linux 主机上的多个 MySQL 实例。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-135">The MySQL OMI authentication file can define a default instance and port number to make managing multiple MySQL instances on one Linux host easier.</span></span>  <span data-ttu-id="ecd7b-136">端口为 0 的实例代表默认实例。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-136">The default instance is denoted by an instance with port 0.</span></span> <span data-ttu-id="ecd7b-137">所有其他实例都将继承在默认实例中设置的属性，除非它们指定了不同的值。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-137">All additional instances will inherit properties set from the default instance unless they specify different values.</span></span> <span data-ttu-id="ecd7b-138">例如，如果添加了在端口“3308”上侦听的 MySQL 实例，则将使用默认实例的绑定地址、用户名和 Base64 编码的密码来尝试和监视在端口 3308 上侦听的实例。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-138">For example, if MySQL instance listening on port ‘3308’ is added, the default instance’s bind-address, username, and Base64 encoded password will be used to try and monitor the instance listening on 3308.</span></span> <span data-ttu-id="ecd7b-139">如果 3308 上的实例绑定到了另一个地址，且使用相同的 MySQL 用户名和密码对，则只需要指定绑定地址，并且将继承其他属性。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-139">If the instance on 3308 is bound to another address and uses the same MySQL username and password pair only the bind-address is needed, and the other properties will be inherited.</span></span>

<span data-ttu-id="ecd7b-140">下表提供了示例实例设置</span><span class="sxs-lookup"><span data-stu-id="ecd7b-140">The following table has example instance settings</span></span> 

| <span data-ttu-id="ecd7b-141">说明</span><span class="sxs-lookup"><span data-stu-id="ecd7b-141">Description</span></span> | <span data-ttu-id="ecd7b-142">文件</span><span class="sxs-lookup"><span data-stu-id="ecd7b-142">File</span></span> |
|:--|:--|
| <span data-ttu-id="ecd7b-143">默认实例和端口为 3308 的实例。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-143">Default instance and instance with port 3308.</span></span> | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=, ,`<br>`AutoUpdate=true` |
| <span data-ttu-id="ecd7b-144">默认实例和端口为 3308 且采用不同用户名和密码的实例。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-144">Default instance and instance with port 3308 and different user name and password.</span></span> | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=127.0.1.1, myuser2,cGluaGVhZA==`<br>`AutoUpdate=true` |


### <a name="mysql-omi-authentication-file-program"></a><span data-ttu-id="ecd7b-145">MySQL OMI 身份验证文件程序</span><span class="sxs-lookup"><span data-stu-id="ecd7b-145">MySQL OMI Authentication File Program</span></span>
<span data-ttu-id="ecd7b-146">随 MySQL OMI 提供程序安装了一个 MySQL OMI 身份验证文件程序，可以使用该程序来编辑 MySQL OMI 身份验证文件。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-146">Included with the installation of the MySQL OMI provider is a MySQL OMI authentication file program which can be used to edit the MySQL OMI Authentication file.</span></span> <span data-ttu-id="ecd7b-147">可以在以下位置找到该身份验证文件程序。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-147">The authentication file program can be found at the following location.</span></span>

    /opt/microsoft/mysql-cimprov/bin/mycimprovauth

> [!NOTE]
> <span data-ttu-id="ecd7b-148">凭据文件必须可供 omsagent 帐户读取。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-148">The credentials file must be readable by the omsagent account.</span></span> <span data-ttu-id="ecd7b-149">建议以 omsgent 身份运行 mycimprovauth 命令。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-149">Running the mycimprovauth command as omsgent is recommended.</span></span>

<span data-ttu-id="ecd7b-150">下表提供了有关 mycimprovauth 的使用语法的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-150">The following table provides details on the syntax for using mycimprovauth.</span></span>

| <span data-ttu-id="ecd7b-151">操作</span><span class="sxs-lookup"><span data-stu-id="ecd7b-151">Operation</span></span> | <span data-ttu-id="ecd7b-152">示例</span><span class="sxs-lookup"><span data-stu-id="ecd7b-152">Example</span></span> | <span data-ttu-id="ecd7b-153">说明</span><span class="sxs-lookup"><span data-stu-id="ecd7b-153">Description</span></span>
|:--|:--|:--|
| <span data-ttu-id="ecd7b-154">autoupdate *false\\</span><span class="sxs-lookup"><span data-stu-id="ecd7b-154">autoupdate **false\\</span></span>|<span data-ttu-id="ecd7b-155">true**</span><span class="sxs-lookup"><span data-stu-id="ecd7b-155">true*</span></span> | <span data-ttu-id="ecd7b-156">mycimprovauth autoupdate false</span><span class="sxs-lookup"><span data-stu-id="ecd7b-156">mycimprovauth autoupdate false</span></span> | <span data-ttu-id="ecd7b-157">设置在重新启动或更新时是否会自动更新身份验证文件。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-157">Sets whether or not the authentication file will be automatically updated on restart or update.</span></span> |
| <span data-ttu-id="ecd7b-158">default *bind-address username password*</span><span class="sxs-lookup"><span data-stu-id="ecd7b-158">default *bind-address username password*</span></span> | <span data-ttu-id="ecd7b-159">mycimprovauth default 127.0.0.1 root pwd</span><span class="sxs-lookup"><span data-stu-id="ecd7b-159">mycimprovauth default 127.0.0.1 root pwd</span></span> | <span data-ttu-id="ecd7b-160">在 MySQL OMI 身份验证文件中设置默认实例。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-160">Sets the default instance in the MySQL OMI authentication file.</span></span><br><span data-ttu-id="ecd7b-161">应当以纯文本输入密码字段 - MySQL OMI 身份验证文件中的密码将是 Base 64 编码的。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-161">The password field should be entered in plain text - the password in the MySQL OMI authentication file will be Base 64 encoded.</span></span> |
| <span data-ttu-id="ecd7b-162">delete *default\\</span><span class="sxs-lookup"><span data-stu-id="ecd7b-162">delete *default\\</span></span>|<span data-ttu-id="ecd7b-163">port_num*</span><span class="sxs-lookup"><span data-stu-id="ecd7b-163">port_num*</span></span> | <span data-ttu-id="ecd7b-164">mycimprovauth 3308</span><span class="sxs-lookup"><span data-stu-id="ecd7b-164">mycimprovauth 3308</span></span> | <span data-ttu-id="ecd7b-165">删除由默认值或端口号指定的实例。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-165">Deletes the specified instance by either default or by port number.</span></span> |
| <span data-ttu-id="ecd7b-166">help</span><span class="sxs-lookup"><span data-stu-id="ecd7b-166">help</span></span> | <span data-ttu-id="ecd7b-167">mycimprov help</span><span class="sxs-lookup"><span data-stu-id="ecd7b-167">mycimprov help</span></span> | <span data-ttu-id="ecd7b-168">输出可使用的命令列表。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-168">Prints out a list of commands to use.</span></span> |
| <span data-ttu-id="ecd7b-169">print</span><span class="sxs-lookup"><span data-stu-id="ecd7b-169">print</span></span> | <span data-ttu-id="ecd7b-170">mycimprov print</span><span class="sxs-lookup"><span data-stu-id="ecd7b-170">mycimprov print</span></span> | <span data-ttu-id="ecd7b-171">输出易于阅读的 MySQL OMI 身份验证文件。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-171">Prints out an easy to read MySQL OMI authentication file.</span></span> |
| <span data-ttu-id="ecd7b-172">update port_num *bind-address username password*</span><span class="sxs-lookup"><span data-stu-id="ecd7b-172">update port_num *bind-address username password*</span></span> | <span data-ttu-id="ecd7b-173">mycimprov update 3307 127.0.0.1 root pwd</span><span class="sxs-lookup"><span data-stu-id="ecd7b-173">mycimprov update 3307 127.0.0.1 root pwd</span></span> | <span data-ttu-id="ecd7b-174">更新指定的实例，或添加该实例（如果它不存在）。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-174">Updates the specified instance or adds the instance if it does not exist.</span></span> |

<span data-ttu-id="ecd7b-175">以下示例命令为 localhost 上的 MySQL 服务器定义了一个默认用户帐户。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-175">The following example commands define a default user account for the MySQL server on localhost.</span></span>  <span data-ttu-id="ecd7b-176">应当以纯文本输入密码字段 - MySQL OMI 身份验证文件中的密码将是 Base 64 编码的</span><span class="sxs-lookup"><span data-stu-id="ecd7b-176">The password field should be entered in plain text - the password in the MySQL OMI authentication file will be Base 64 encoded</span></span>

    sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>'
    sudo /opt/omi/bin/service_control restart

### <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="ecd7b-177">MySQL 性能计数器所需的数据库权限</span><span class="sxs-lookup"><span data-stu-id="ecd7b-177">Database Permissions Required for MySQL Performance Counters</span></span>
<span data-ttu-id="ecd7b-178">MySQL 用户需要访问以下查询来收集 MySQL 服务器性能数据。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-178">The MySQL User requires access to the following queries to collect MySQL Server performance data.</span></span> 

    SHOW GLOBAL STATUS;
    SHOW GLOBAL VARIABLES:


<span data-ttu-id="ecd7b-179">MySQL 用户还需要对以下默认表具有 SELECT 访问权限。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-179">The MySQL user also requires SELECT access to the following default tables.</span></span>

- <span data-ttu-id="ecd7b-180">information_schema</span><span class="sxs-lookup"><span data-stu-id="ecd7b-180">information_schema</span></span>
- <span data-ttu-id="ecd7b-181">mysql</span><span class="sxs-lookup"><span data-stu-id="ecd7b-181">mysql.</span></span> 

<span data-ttu-id="ecd7b-182">可以通过运行以下授予命令来授予这些特权。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-182">These privileges can be granted by running the following grant commands.</span></span>

    GRANT SELECT ON information_schema.* TO ‘monuser’@’localhost’;
    GRANT SELECT ON mysql.* TO ‘monuser’@’localhost’;


> [!NOTE]
> <span data-ttu-id="ecd7b-183">要向 MySQL 监视用户授予权限，执行授权的用户必须具有 'GRANT option' 特权以及要授予的特权。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-183">To grant permissions to a MySQL monitoring user the granting user must have the ‘GRANT option’ privilege as well as the privilege being granted.</span></span>

### <a name="define-performance-counters"></a><span data-ttu-id="ecd7b-184">定义性能计数器</span><span class="sxs-lookup"><span data-stu-id="ecd7b-184">Define performance counters</span></span>

<span data-ttu-id="ecd7b-185">将用于 Linux 的 OMS 代理配置为将数据发送到 Log Analytics 后，必须配置要收集的性能计数器。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-185">Once you configure the OMS Agent for Linux to send data to Log Analytics, you must configure the performance counters to collect.</span></span>  <span data-ttu-id="ecd7b-186">请对下表中的计数器使用 [Log Analytics 中的 Windows 和 Linux 性能数据来源](log-analytics-data-sources-windows-events.md)中所述的过程。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-186">Use the procedure in [Windows and Linux performance data sources in Log Analytics](log-analytics-data-sources-windows-events.md) with the counters in the following table.</span></span>

| <span data-ttu-id="ecd7b-187">对象名称</span><span class="sxs-lookup"><span data-stu-id="ecd7b-187">Object Name</span></span> | <span data-ttu-id="ecd7b-188">计数器名称</span><span class="sxs-lookup"><span data-stu-id="ecd7b-188">Counter Name</span></span> |
|:--|:--|
| <span data-ttu-id="ecd7b-189">MySQL 数据库</span><span class="sxs-lookup"><span data-stu-id="ecd7b-189">MySQL Database</span></span> | <span data-ttu-id="ecd7b-190">磁盘空间(字节)</span><span class="sxs-lookup"><span data-stu-id="ecd7b-190">Disk Space in Bytes</span></span> |
| <span data-ttu-id="ecd7b-191">MySQL 数据库</span><span class="sxs-lookup"><span data-stu-id="ecd7b-191">MySQL Database</span></span> | <span data-ttu-id="ecd7b-192">表</span><span class="sxs-lookup"><span data-stu-id="ecd7b-192">Tables</span></span> |
| <span data-ttu-id="ecd7b-193">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-193">MySQL Server</span></span> | <span data-ttu-id="ecd7b-194">中止的连接百分比</span><span class="sxs-lookup"><span data-stu-id="ecd7b-194">Aborted Connection Pct</span></span> |
| <span data-ttu-id="ecd7b-195">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-195">MySQL Server</span></span> | <span data-ttu-id="ecd7b-196">连接使用百分比</span><span class="sxs-lookup"><span data-stu-id="ecd7b-196">Connection Use Pct</span></span> |
| <span data-ttu-id="ecd7b-197">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-197">MySQL Server</span></span> | <span data-ttu-id="ecd7b-198">磁盘空间使用(字节)</span><span class="sxs-lookup"><span data-stu-id="ecd7b-198">Disk Space Use in Bytes</span></span> |
| <span data-ttu-id="ecd7b-199">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-199">MySQL Server</span></span> | <span data-ttu-id="ecd7b-200">全表扫描百分比</span><span class="sxs-lookup"><span data-stu-id="ecd7b-200">Full Table Scan Pct</span></span> |
| <span data-ttu-id="ecd7b-201">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-201">MySQL Server</span></span> | <span data-ttu-id="ecd7b-202">InnoDB 缓冲池命中百分比</span><span class="sxs-lookup"><span data-stu-id="ecd7b-202">InnoDB Buffer Pool Hit Pct</span></span> |
| <span data-ttu-id="ecd7b-203">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-203">MySQL Server</span></span> | <span data-ttu-id="ecd7b-204">InnoDB 缓冲池使用百分比</span><span class="sxs-lookup"><span data-stu-id="ecd7b-204">InnoDB Buffer Pool Use Pct</span></span> |
| <span data-ttu-id="ecd7b-205">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-205">MySQL Server</span></span> | <span data-ttu-id="ecd7b-206">InnoDB 缓冲池使用百分比</span><span class="sxs-lookup"><span data-stu-id="ecd7b-206">InnoDB Buffer Pool Use Pct</span></span> |
| <span data-ttu-id="ecd7b-207">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-207">MySQL Server</span></span> | <span data-ttu-id="ecd7b-208">键缓存命中百分比</span><span class="sxs-lookup"><span data-stu-id="ecd7b-208">Key Cache Hit Pct</span></span> |
| <span data-ttu-id="ecd7b-209">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-209">MySQL Server</span></span> | <span data-ttu-id="ecd7b-210">键缓存使用百分比</span><span class="sxs-lookup"><span data-stu-id="ecd7b-210">Key Cache Use Pct</span></span> |
| <span data-ttu-id="ecd7b-211">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-211">MySQL Server</span></span> | <span data-ttu-id="ecd7b-212">键缓存写入百分比</span><span class="sxs-lookup"><span data-stu-id="ecd7b-212">Key Cache Write Pct</span></span> |
| <span data-ttu-id="ecd7b-213">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-213">MySQL Server</span></span> | <span data-ttu-id="ecd7b-214">查询缓存命中百分比</span><span class="sxs-lookup"><span data-stu-id="ecd7b-214">Query Cache Hit Pct</span></span> |
| <span data-ttu-id="ecd7b-215">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-215">MySQL Server</span></span> | <span data-ttu-id="ecd7b-216">查询缓存修剪百分比</span><span class="sxs-lookup"><span data-stu-id="ecd7b-216">Query Cache Prunes Pct</span></span> |
| <span data-ttu-id="ecd7b-217">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-217">MySQL Server</span></span> | <span data-ttu-id="ecd7b-218">查询缓存使用百分比</span><span class="sxs-lookup"><span data-stu-id="ecd7b-218">Query Cache Use Pct</span></span> |
| <span data-ttu-id="ecd7b-219">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-219">MySQL Server</span></span> | <span data-ttu-id="ecd7b-220">表缓存命中百分比</span><span class="sxs-lookup"><span data-stu-id="ecd7b-220">Table Cache Hit Pct</span></span> |
| <span data-ttu-id="ecd7b-221">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-221">MySQL Server</span></span> | <span data-ttu-id="ecd7b-222">表缓存使用百分比</span><span class="sxs-lookup"><span data-stu-id="ecd7b-222">Table Cache Use Pct</span></span> |
| <span data-ttu-id="ecd7b-223">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-223">MySQL Server</span></span> | <span data-ttu-id="ecd7b-224">表锁争用百分比</span><span class="sxs-lookup"><span data-stu-id="ecd7b-224">Table Lock Contention Pct</span></span> |

## <a name="apache-http-server"></a><span data-ttu-id="ecd7b-225">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-225">Apache HTTP Server</span></span> 
<span data-ttu-id="ecd7b-226">如果安装 omsagent 捆绑包时在计算机上检测到 Apache HTTP Server，则会自动安装 Apache HTTP Server 的性能监视提供程序。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-226">If Apache HTTP Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server will be automatically installed.</span></span> <span data-ttu-id="ecd7b-227">此提供程序依赖于必须加载到 Apache HTTP Server 才能访问性能数据的一个 Apache 模块。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-227">This provider relies on an Apache module that must be loaded into the Apache HTTP Server in order to access performance data.</span></span> <span data-ttu-id="ecd7b-228">可以使用以下命令加载该模块：</span><span class="sxs-lookup"><span data-stu-id="ecd7b-228">The module can be loaded with the following command:</span></span>
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="ecd7b-229">要卸载 Apache 监视模块，请运行以下命令︰</span><span class="sxs-lookup"><span data-stu-id="ecd7b-229">To unload the Apache monitoring module, run the following command:</span></span>
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```

### <a name="define-performance-counters"></a><span data-ttu-id="ecd7b-230">定义性能计数器</span><span class="sxs-lookup"><span data-stu-id="ecd7b-230">Define performance counters</span></span>

<span data-ttu-id="ecd7b-231">将用于 Linux 的 OMS 代理配置为将数据发送到 Log Analytics 后，必须配置要收集的性能计数器。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-231">Once you configure the OMS Agent for Linux to send data to Log Analytics, you must configure the performance counters to collect.</span></span>  <span data-ttu-id="ecd7b-232">请对下表中的计数器使用 [Log Analytics 中的 Windows 和 Linux 性能数据来源](log-analytics-data-sources-windows-events.md)中所述的过程。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-232">Use the procedure in [Windows and Linux performance data sources in Log Analytics](log-analytics-data-sources-windows-events.md) with the counters in the following table.</span></span>

| <span data-ttu-id="ecd7b-233">对象名称</span><span class="sxs-lookup"><span data-stu-id="ecd7b-233">Object Name</span></span> | <span data-ttu-id="ecd7b-234">计数器名称</span><span class="sxs-lookup"><span data-stu-id="ecd7b-234">Counter Name</span></span> |
|:--|:--|
| <span data-ttu-id="ecd7b-235">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-235">Apache HTTP Server</span></span> | <span data-ttu-id="ecd7b-236">繁忙工作线程数</span><span class="sxs-lookup"><span data-stu-id="ecd7b-236">Busy Workers</span></span> |
| <span data-ttu-id="ecd7b-237">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-237">Apache HTTP Server</span></span> | <span data-ttu-id="ecd7b-238">空闲工作线程数</span><span class="sxs-lookup"><span data-stu-id="ecd7b-238">Idle Workers</span></span> |
| <span data-ttu-id="ecd7b-239">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-239">Apache HTTP Server</span></span> | <span data-ttu-id="ecd7b-240">繁忙工作线程数百分比</span><span class="sxs-lookup"><span data-stu-id="ecd7b-240">Pct Busy Workers</span></span> |
| <span data-ttu-id="ecd7b-241">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="ecd7b-241">Apache HTTP Server</span></span> | <span data-ttu-id="ecd7b-242">CPU 百分比总计</span><span class="sxs-lookup"><span data-stu-id="ecd7b-242">Total Pct CPU</span></span> |
| <span data-ttu-id="ecd7b-243">Apache 虚拟主机</span><span class="sxs-lookup"><span data-stu-id="ecd7b-243">Apache Virtual Host</span></span> | <span data-ttu-id="ecd7b-244">每分钟错误数 - 客户端</span><span class="sxs-lookup"><span data-stu-id="ecd7b-244">Errors per Minute - Client</span></span> |
| <span data-ttu-id="ecd7b-245">Apache 虚拟主机</span><span class="sxs-lookup"><span data-stu-id="ecd7b-245">Apache Virtual Host</span></span> | <span data-ttu-id="ecd7b-246">每分钟错误数 - 服务器</span><span class="sxs-lookup"><span data-stu-id="ecd7b-246">Errors per Minute - Server</span></span> |
| <span data-ttu-id="ecd7b-247">Apache 虚拟主机</span><span class="sxs-lookup"><span data-stu-id="ecd7b-247">Apache Virtual Host</span></span> | <span data-ttu-id="ecd7b-248">每个请求的 KB 数</span><span class="sxs-lookup"><span data-stu-id="ecd7b-248">KB per Request</span></span> |
| <span data-ttu-id="ecd7b-249">Apache 虚拟主机</span><span class="sxs-lookup"><span data-stu-id="ecd7b-249">Apache Virtual Host</span></span> | <span data-ttu-id="ecd7b-250">每秒的请求的 KB 数</span><span class="sxs-lookup"><span data-stu-id="ecd7b-250">Requests KB per Second</span></span> |
| <span data-ttu-id="ecd7b-251">Apache 虚拟主机</span><span class="sxs-lookup"><span data-stu-id="ecd7b-251">Apache Virtual Host</span></span> | <span data-ttu-id="ecd7b-252">每秒的请求数</span><span class="sxs-lookup"><span data-stu-id="ecd7b-252">Requests per Second</span></span> |



## <a name="next-steps"></a><span data-ttu-id="ecd7b-253">后续步骤</span><span class="sxs-lookup"><span data-stu-id="ecd7b-253">Next steps</span></span>
* <span data-ttu-id="ecd7b-254">从 Linux 代理[收集性能计数器](log-analytics-data-sources-performance-counters.md)。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-254">[Collect performance counters](log-analytics-data-sources-performance-counters.md) from Linux agents.</span></span>
* <span data-ttu-id="ecd7b-255">了解[日志搜索](log-analytics-log-searches.md)以便分析从数据源和解决方案中收集的数据。</span><span class="sxs-lookup"><span data-stu-id="ecd7b-255">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 