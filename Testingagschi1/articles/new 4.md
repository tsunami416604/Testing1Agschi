---
title: "Stretch 対応データベースの復元 (Stretch Database) | Microsoft Docs"
ms.custom: 
ms.date: 07/06/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cebc1f6d-d5ea-460d-ae60-d047d29c2723
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: Human Translation
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: 179935cc6a15d076737d12b4fa6fac28f354db3c
ms.contentlocale: ja-jp
ms.lasthandoff: 07/29/2017

---
# <a name="restore-stretch-enabled-databases-stretch-database"></a><span data-ttu-id="20280-102">Stretch 対応データベースの復元 (Stretch Database)</span><span class="sxs-lookup"><span data-stu-id="20280-102">Restore Stretch-enabled databases (Stretch Database)</span></span>
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  <span data-ttu-id="20280-103">さまざまな種類の失敗、エラー、障害から修復する必要が生じたときに、バックアップされたデータベースを復元します。</span><span class="sxs-lookup"><span data-stu-id="20280-103">Restore a backed up database when necessary to recover from many types of failures, errors, and disasters.</span></span>
  
  <span data-ttu-id="20280-104">バックアップの詳細については、「 [Stretch 対応データベースのバックアップ](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="20280-104">For more info about backup, see [Backup Stretch-enabled databases](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md).</span></span>

> [!TIP]
> <span data-ttu-id="20280-105">バックアップは、完全な高可用性とビジネス継続性ソリューションの一部にすぎません。</span><span class="sxs-lookup"><span data-stu-id="20280-105">Backup is only one part of a complete high availability and business continuity solution.</span></span> <span data-ttu-id="20280-106">高可用性の詳細については、「 [高可用性ソリューション](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="20280-106">For more info about high availability, see [High Availability Solutions](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md).</span></span>

## <a name="restore-your-sql-server-data"></a><span data-ttu-id="20280-107">SQL Server データの復元</span><span class="sxs-lookup"><span data-stu-id="20280-107">Restore your SQL Server data</span></span>
<span data-ttu-id="20280-108">ハードウェアの障害または破損から復元するには、Stretch 対応 SQL Server データベースをバックアップから復元します。</span><span class="sxs-lookup"><span data-stu-id="20280-108">To recover from hardware failure or corruption, restore the Stretch-enabled SQL Server database from a backup.</span></span> <span data-ttu-id="20280-109">現在使用中の SQL Server の復元方法を引き続き使用できます。</span><span class="sxs-lookup"><span data-stu-id="20280-109">You can continue to use the SQL Server restore methods that you currently use.</span></span> <span data-ttu-id="20280-110">詳細については、「 [復元と復旧の概要](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="20280-110">For more info, see [Restore and Recovery Overview](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).</span></span>

<span data-ttu-id="20280-111">SQL Server データベースを復元した後に、ストアド プロシージャ **sys.sp_rda_reauthorize_db** を実行して、Stretch 対応の SQL Server データベースとリモートの Azure データベース間の接続を再確立する必要があります。</span><span class="sxs-lookup"><span data-stu-id="20280-111">After you restore the SQL Server database, you have to run the stored procedure **sys.sp_rda_reauthorize_db** to re-establish the connection between the Stretch-enabled SQL Server database and the remote Azure database.</span></span> <span data-ttu-id="20280-112">詳細については、「 [SQL Server データベースと Azure リモート データベース間の接続を復元する](#reconnect)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="20280-112">For more info, see [Restore the connection between the SQL Server database and the remote Azure database](#reconnect).</span></span>

## <a name="restore-your-remote-azure-data"></a><span data-ttu-id="20280-113">リモートの Azure データの復元</span><span class="sxs-lookup"><span data-stu-id="20280-113">Restore your remote Azure data</span></span>

### <a name="recover-a-live-azure-database"></a><span data-ttu-id="20280-114">Azure ライブ データベースの復旧</span><span class="sxs-lookup"><span data-stu-id="20280-114">Recover a live Azure database</span></span>
<span data-ttu-id="20280-115">Azure の SQL Server Stretch Database サービスでは、Azure Storage スナップショットを使用して、少なくとも 8 時間ごとにすべてのライブ データのスナップショットを撮ります。</span><span class="sxs-lookup"><span data-stu-id="20280-115">The SQL Server Stretch Database service on Azure snapshots all live data at least every 8 hours using Azure Storage Snapshots.</span></span> <span data-ttu-id="20280-116">これらのスナップショットは 7 日間保存されます。</span><span class="sxs-lookup"><span data-stu-id="20280-116">These snapshots are maintained for 7 days.</span></span> <span data-ttu-id="20280-117">これにより、過去 7 日間から最後にスナップショットが撮られた時点までの少なくとも 21 の時点のいずれかの状態にデータを復元できます。</span><span class="sxs-lookup"><span data-stu-id="20280-117">This allows you to restore the data to one of at least 21 points in time within the past 7 days up to the time when the last snapshot was taken.</span></span>

<span data-ttu-id="20280-118">Azure ポータルを使用して、Azure ライブ データベースを過去の状態に復元するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="20280-118">To restore a live Azure database to an earlier point in time by using the Azure portal, do the following things.</span></span>

1. <span data-ttu-id="20280-119">[Azure ポータル][]にログインします。</span><span class="sxs-lookup"><span data-stu-id="20280-119">Log in to the [Azure portal][].</span></span>
2. <span data-ttu-id="20280-120">画面左側の **[参照]** を選択し、 **[SQL デーベース]**を選択します。</span><span class="sxs-lookup"><span data-stu-id="20280-120">On the left side of the screen select **BROWSE** and then select **SQL Databases**.</span></span>
3. <span data-ttu-id="20280-121">使用中のデータベースに移動して選択します。</span><span class="sxs-lookup"><span data-stu-id="20280-121">Navigate to your database and select it.</span></span>
4. <span data-ttu-id="20280-122">データベース ブレードの上部にある **[復元]**をクリックします。</span><span class="sxs-lookup"><span data-stu-id="20280-122">At the top of the database blade, click **Restore**.</span></span>
5. <span data-ttu-id="20280-123">新しい **データベース名**を指定し、 **[復元ポイント]** を選択してから **[作成]**をクリックします。</span><span class="sxs-lookup"><span data-stu-id="20280-123">Specify a new **Database name**, select a **Restore Point** and then click **Create**.</span></span>
6. <span data-ttu-id="20280-124">データベースの復元処理が開始され、 **[通知]**を使用して監視できます。</span><span class="sxs-lookup"><span data-stu-id="20280-124">The database restore process will begin and can be monitored using **NOTIFICATIONS**.</span></span>

### <a name="recover-a-deleted-azure-database"></a><span data-ttu-id="20280-125">削除された Azure データベースの復旧</span><span class="sxs-lookup"><span data-stu-id="20280-125">Recover a deleted Azure database</span></span>
<span data-ttu-id="20280-126">Azure の SQL Server Stretch Database サービスでは、データベースが削除される前にデータベースのスナップショットが撮られ、7 日間保持されます。</span><span class="sxs-lookup"><span data-stu-id="20280-126">The SQL Server Stretch Database service on Azure takes a database snapshot before a database is dropped and retains it for 7 days.</span></span> <span data-ttu-id="20280-127">それ以降、ライブ データベースからのスナップショットは保持されなくなります。</span><span class="sxs-lookup"><span data-stu-id="20280-127">After this occurs, it no longer retains snapshots from the live database.</span></span> <span data-ttu-id="20280-128">これにより、削除された時点にデータベースを復元できます。</span><span class="sxs-lookup"><span data-stu-id="20280-128">This lets you restore a deleted database to the point when it was deleted.</span></span>

<span data-ttu-id="20280-129">Azure ポータルを使用して、削除された Azure データベースをその時点の状態に復元するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="20280-129">To restore a deleted Azure database to the point when it was deletedby using the Azure portal, do the following things.</span></span>

1. <span data-ttu-id="20280-130">[Azure ポータル][]にログインします。</span><span class="sxs-lookup"><span data-stu-id="20280-130">Log in to the [Azure portal][].</span></span>
2. <span data-ttu-id="20280-131">画面左側の **[参照]** を選択し、 **[SQL Servers]**を選択します。</span><span class="sxs-lookup"><span data-stu-id="20280-131">On the left side of the screen select **BROWSE** and then select **SQL Servers**.</span></span>
3. <span data-ttu-id="20280-132">使用中のサーバーに移動して選択します。</span><span class="sxs-lookup"><span data-stu-id="20280-132">Navigate to your server and select it.</span></span>
4. <span data-ttu-id="20280-133">サーバーのブレードで [操作] まで下へスクロールし、 **[削除されたデータベース]** タイルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="20280-133">Scroll down to Operations on your server's blade, click the **Deleted Databases** tile.</span></span>
5. <span data-ttu-id="20280-134">復元する削除されたデータベースを選択します。</span><span class="sxs-lookup"><span data-stu-id="20280-134">Select the deleted database you want to restore.</span></span>
5. <span data-ttu-id="20280-135">新しい **データベース名** を指定し、 **[作成]**をクリックします。</span><span class="sxs-lookup"><span data-stu-id="20280-135">Specify a new **Database name** and click **Create**.</span></span>
6. <span data-ttu-id="20280-136">データベースの復元処理が開始され、 **[通知]**を使用して監視できます。</span><span class="sxs-lookup"><span data-stu-id="20280-136">The database restore process will begin and can be monitored using **NOTIFICATIONS**.</span></span>

## <span data-ttu-id="20280-137"><a name="reconnect"></a>SQL Server データベースと Azure リモート データベース間の接続を復元する</span><span class="sxs-lookup"><span data-stu-id="20280-137"><a name="reconnect"></a>Restore the connection between the SQL Server database and the remote Azure database</span></span>

1.  <span data-ttu-id="20280-138">異なる名前または異なるリージョンの復元された Azure データベースに接続するには、ストアド プロシージャ [sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) を実行して、以前の Azure データベースから切断します。</span><span class="sxs-lookup"><span data-stu-id="20280-138">If you're going to connect to a restored Azure database with a different name or in a different region, run the stored procedure [sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) to disconnect from the previous Azure database.</span></span>  
  
2.  <span data-ttu-id="20280-139">ストアド プロシージャ [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) を実行してローカルの Stretch 対応データベースを Azure データベースに再接続します。</span><span class="sxs-lookup"><span data-stu-id="20280-139">Run the stored procedure [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) to reconnect the local Stretch-enabled database to the Azure database.</span></span>  
  
    -   <span data-ttu-id="20280-140">既存のデータベース スコープ資格情報を sysname または varchar(128) 値として指定します。</span><span class="sxs-lookup"><span data-stu-id="20280-140">Provide the existing database scoped credential as a sysname or a varchar(128) value.</span></span> <span data-ttu-id="20280-141">(varchar(max) は使用しないでください)。資格情報の名前はビュー **sys.database_scoped_credentials** で参照できます。</span><span class="sxs-lookup"><span data-stu-id="20280-141">(Don't use varchar(max).) You can look up the credential name in the view **sys.database_scoped_credentials**.</span></span>  
  
    -   <span data-ttu-id="20280-142">リモート データのコピーを作成するかどうかを指定し、コピーに接続します (推奨)。</span><span class="sxs-lookup"><span data-stu-id="20280-142">Specify whether to make a copy of the remote data and connect to the copy (recommended).</span></span>  
  
    ```tsql  
    USE <Stretch-enabled database name>;
    GO
    EXEC sp_rda_reauthorize_db
        @credential = N'<existing_database_scoped_credential_name>',
        @with_copy = 1 ;  
    GO  
    ```  
    
  ## <a name="see-also"></a><span data-ttu-id="20280-143">参照</span><span class="sxs-lookup"><span data-stu-id="20280-143">See Also</span></span>  
 [<span data-ttu-id="20280-144">Stretch 対応データベースのバックアップ</span><span class="sxs-lookup"><span data-stu-id="20280-144">Backup Stretch-enabled databases</span></span>](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
 <span data-ttu-id="20280-145">[Stretch Database の管理とトラブルシューティング](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md) </span><span class="sxs-lookup"><span data-stu-id="20280-145">[Manage and troubleshoot Stretch Database](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md) </span></span>  
 <span data-ttu-id="20280-146">[sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 
 [sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)</span><span class="sxs-lookup"><span data-stu-id="20280-146">[sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 
 [sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)</span></span>  
[<span data-ttu-id="20280-147">SQL Server データベースのバックアップと復元</span><span class="sxs-lookup"><span data-stu-id="20280-147">Back Up and Restore of SQL Server Databases</span></span>](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
 
 <span data-ttu-id="20280-148">[Azure ポータル]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="20280-148">[Azure portal]: https://portal.azure.com/</span></span>
 

