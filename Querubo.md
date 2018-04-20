---
title: IT Service Management Connector in Azure Log Analytics | Microsoft Docs
description: 'This article provides an overview of IT Service Management Connector (ITSMC) and information about how to use this solution to centrally monitor and manage the ITSM work items in Azure Log Analytics, and resolve any issues quickly.'
services: log-analytics
documentationcenter: ''
author: JYOTHIRMAISURI
manager: riyazp
editor: ''
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2018
ms.author: v-jysur
---
# <a name="connect-azure-to-itsm-tools-using-it-service-management-connector"></a><span data-ttu-id="879f7-103">Connect Azure to ITSM tools using IT Service Management Connector</span><span class="sxs-lookup"><span data-stu-id="879f7-103">Connect Azure to ITSM tools using IT Service Management Connector</span></span>

![IT Service Management Connector symbol](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="879f7-105">The IT Service Management Connector (ITSMC) allows you to connect Azure and a supported IT Service Management (ITSM) product/service.</span><span class="sxs-lookup"><span data-stu-id="879f7-105">The IT Service Management Connector (ITSMC) allows you to connect Azure and a supported IT Service Management (ITSM) product/service.</span></span>

<span data-ttu-id="879f7-106">Azure services like Log Analytics and Azure Monitor provide tools to detect, analyze and troubleshoot issues with your Azure and non-Azure resources.</span><span class="sxs-lookup"><span data-stu-id="879f7-106">Azure services like Log Analytics and Azure Monitor provide tools to detect, analyze and troubleshoot issues with your Azure and non-Azure resources.</span></span> <span data-ttu-id="879f7-107">However, the work items related to an issue  typically reside in an ITSM product/service.</span><span class="sxs-lookup"><span data-stu-id="879f7-107">However, the work items related to an issue  typically reside in an ITSM product/service.</span></span> <span data-ttu-id="879f7-108">The ITSM connector provides a bi-directional connection between Azure and ITSM tools to help you resolve issues faster.</span><span class="sxs-lookup"><span data-stu-id="879f7-108">The ITSM connector provides a bi-directional connection between Azure and ITSM tools to help you resolve issues faster.</span></span>

<span data-ttu-id="879f7-109">ITSMC supports connections with the following ITSM tools:</span><span class="sxs-lookup"><span data-stu-id="879f7-109">ITSMC supports connections with the following ITSM tools:</span></span>

-   <span data-ttu-id="879f7-110">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="879f7-110">ServiceNow</span></span>
-   <span data-ttu-id="879f7-111">System Center Service Manager</span><span class="sxs-lookup"><span data-stu-id="879f7-111">System Center Service Manager</span></span>
-   <span data-ttu-id="879f7-112">Provance</span><span class="sxs-lookup"><span data-stu-id="879f7-112">Provance</span></span>
-   <span data-ttu-id="879f7-113">Cherwell</span><span class="sxs-lookup"><span data-stu-id="879f7-113">Cherwell</span></span>

<span data-ttu-id="879f7-114">With ITSMC, you can</span><span class="sxs-lookup"><span data-stu-id="879f7-114">With ITSMC, you can</span></span>

-  <span data-ttu-id="879f7-115">Create work items in ITSM tool, based on your Azure alerts (metric alerts, Activity Log alerts and Log Analytics alerts).</span><span class="sxs-lookup"><span data-stu-id="879f7-115">Create work items in ITSM tool, based on your Azure alerts (metric alerts, Activity Log alerts and Log Analytics alerts).</span></span>
-  <span data-ttu-id="879f7-116">Optionally, you can sync your incident and change request data from your ITSM tool to an Azure Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="879f7-116">Optionally, you can sync your incident and change request data from your ITSM tool to an Azure Log Analytics workspace.</span></span>


<span data-ttu-id="879f7-117">You can start using the ITSM Connector using the following steps:</span><span class="sxs-lookup"><span data-stu-id="879f7-117">You can start using the ITSM Connector using the following steps:</span></span>

1.  [<span data-ttu-id="879f7-118">Add the ITSM Connector Solution</span><span class="sxs-lookup"><span data-stu-id="879f7-118">Add the ITSM Connector Solution</span></span>](#adding-the-it-service-management-connector-solution)
2.  [<span data-ttu-id="879f7-119">Create an ITSM connection</span><span class="sxs-lookup"><span data-stu-id="879f7-119">Create an ITSM connection</span></span>](#creating-an-itsm-connection)
3.  [<span data-ttu-id="879f7-120">Use the connection</span><span class="sxs-lookup"><span data-stu-id="879f7-120">Use the connection</span></span>](#using-the-solution)


##  <a name="adding-the-it-service-management-connector-solution"></a><span data-ttu-id="879f7-121">Adding the IT Service Management Connector Solution</span><span class="sxs-lookup"><span data-stu-id="879f7-121">Adding the IT Service Management Connector Solution</span></span>

<span data-ttu-id="879f7-122">Before you can create a connection, you need to add the ITSM Connector Solution.</span><span class="sxs-lookup"><span data-stu-id="879f7-122">Before you can create a connection, you need to add the ITSM Connector Solution.</span></span>

1.  <span data-ttu-id="879f7-123">In Azure portal, click **+ New** icon.</span><span class="sxs-lookup"><span data-stu-id="879f7-123">In Azure portal, click **+ New** icon.</span></span>

    ![Azure new resource](./media/log-analytics-itsmc/azure-add-new-resource.png)

2.  <span data-ttu-id="879f7-125">Search for **IT Service Management Connector** in the Marketplace and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="879f7-125">Search for **IT Service Management Connector** in the Marketplace and click **Create**.</span></span>

    ![Add ITSMC solution](./media/log-analytics-itsmc/add-itsmc-solution.png)

3.  <span data-ttu-id="879f7-127">In the **OMS Workspace** section, select the Azure Log Analytics workspace where you want to install the solution.</span><span class="sxs-lookup"><span data-stu-id="879f7-127">In the **OMS Workspace** section, select the Azure Log Analytics workspace where you want to install the solution.</span></span>
4.  <span data-ttu-id="879f7-128">In the **OMS Workspace Settings** section, select the ResourceGroup where you want to create the solution resource.</span><span class="sxs-lookup"><span data-stu-id="879f7-128">In the **OMS Workspace Settings** section, select the ResourceGroup where you want to create the solution resource.</span></span>

    ![ITSMC workspace](./media/log-analytics-itsmc/itsmc-solution-workspace.png)

5.  <span data-ttu-id="879f7-130">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="879f7-130">Click **Create**.</span></span>

<span data-ttu-id="879f7-131">When the solution resource is deployed, a notification appears at the top right of the window.</span><span class="sxs-lookup"><span data-stu-id="879f7-131">When the solution resource is deployed, a notification appears at the top right of the window.</span></span>


## <a name="creating-an-itsm--connection"></a><span data-ttu-id="879f7-132">Creating an ITSM  connection</span><span class="sxs-lookup"><span data-stu-id="879f7-132">Creating an ITSM  connection</span></span>

<span data-ttu-id="879f7-133">Once you have installed the solution, you can create a connection.</span><span class="sxs-lookup"><span data-stu-id="879f7-133">Once you have installed the solution, you can create a connection.</span></span>

<span data-ttu-id="879f7-134">For creating a connection, you will need to prep your ITSM tool to allow the connection from the ITSM Connector solution.</span><span class="sxs-lookup"><span data-stu-id="879f7-134">For creating a connection, you will need to prep your ITSM tool to allow the connection from the ITSM Connector solution.</span></span>  

<span data-ttu-id="879f7-135">Depending on the ITSM product you are connecting to, use the following steps :</span><span class="sxs-lookup"><span data-stu-id="879f7-135">Depending on the ITSM product you are connecting to, use the following steps :</span></span>

- [<span data-ttu-id="879f7-136">System Center Service Manager (SCSM)</span><span class="sxs-lookup"><span data-stu-id="879f7-136">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-azure)
- [<span data-ttu-id="879f7-137">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="879f7-137">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-azure)
- [<span data-ttu-id="879f7-138">Provance</span><span class="sxs-lookup"><span data-stu-id="879f7-138">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-azure)  
- [<span data-ttu-id="879f7-139">Cherwell</span><span class="sxs-lookup"><span data-stu-id="879f7-139">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-azure)

<span data-ttu-id="879f7-140">Once you have prepped your ITSM tools, follow the steps below to create a connection:</span><span class="sxs-lookup"><span data-stu-id="879f7-140">Once you have prepped your ITSM tools, follow the steps below to create a connection:</span></span>

1.  <span data-ttu-id="879f7-141">Go to **All Resources**, look for **ServiceDesk(YourWorkspaceName)**.</span><span class="sxs-lookup"><span data-stu-id="879f7-141">Go to **All Resources**, look for **ServiceDesk(YourWorkspaceName)**.</span></span>
2.  <span data-ttu-id="879f7-142">Under **WORKSPACE DATA SOURCES** in the left pane, click **ITSM Connections**.</span><span class="sxs-lookup"><span data-stu-id="879f7-142">Under **WORKSPACE DATA SOURCES** in the left pane, click **ITSM Connections**.</span></span>
    <span data-ttu-id="879f7-143">![ITSM connections](./media/log-analytics-itsmc/itsm-connections.png)</span><span class="sxs-lookup"><span data-stu-id="879f7-143">![ITSM connections](./media/log-analytics-itsmc/itsm-connections.png)</span></span>

    <span data-ttu-id="879f7-144">This page displays the list of connections.</span><span class="sxs-lookup"><span data-stu-id="879f7-144">This page displays the list of connections.</span></span>
3.  <span data-ttu-id="879f7-145">Click **Add Connection**.</span><span class="sxs-lookup"><span data-stu-id="879f7-145">Click **Add Connection**.</span></span>

    ![Add ITSM connection](./media/log-analytics-itsmc/add-new-itsm-connection.png)

4.  <span data-ttu-id="879f7-147">Specify the connection settings as described in [Configuring the ITSMC connection with your ITSM products/services article](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="879f7-147">Specify the connection settings as described in [Configuring the ITSMC connection with your ITSM products/services article](log-analytics-itsmc-connections.md).</span></span>

    > [!NOTE]

    > <span data-ttu-id="879f7-148">By default, ITSMC refreshes the connection's configuration data once in every 24 hours.</span><span class="sxs-lookup"><span data-stu-id="879f7-148">By default, ITSMC refreshes the connection's configuration data once in every 24 hours.</span></span> <span data-ttu-id="879f7-149">To refresh your connection's data instantly for any edits or template updates that you make, click the "Refresh" button displayed next to your connection.</span><span class="sxs-lookup"><span data-stu-id="879f7-149">To refresh your connection's data instantly for any edits or template updates that you make, click the "Refresh" button displayed next to your connection.</span></span>

    ![Connection refresh](./media/log-analytics-itsmc/itsmc-connections-refresh.png)


## <a name="using-the-solution"></a><span data-ttu-id="879f7-151">Using the solution</span><span class="sxs-lookup"><span data-stu-id="879f7-151">Using the solution</span></span>
   <span data-ttu-id="879f7-152">By using the ITSM Connector solution, you can create work items from Azure alerts, Log Analytics alerts  and  Log Analytics log records.</span><span class="sxs-lookup"><span data-stu-id="879f7-152">By using the ITSM Connector solution, you can create work items from Azure alerts, Log Analytics alerts  and  Log Analytics log records.</span></span>

## <a name="create-itsm-work-items-from-azure-alerts"></a><span data-ttu-id="879f7-153">Create ITSM work items from Azure alerts</span><span class="sxs-lookup"><span data-stu-id="879f7-153">Create ITSM work items from Azure alerts</span></span>

<span data-ttu-id="879f7-154">Once you have your ITSM connection created, you can create work item(s) in your ITSM tool based on Azure alerts, by using the **ITSM Action** in **Action Groups**.</span><span class="sxs-lookup"><span data-stu-id="879f7-154">Once you have your ITSM connection created, you can create work item(s) in your ITSM tool based on Azure alerts, by using the **ITSM Action** in **Action Groups**.</span></span>

<span data-ttu-id="879f7-155">Action Groups provide a modular and reusable way of triggering actions for your Azure Alerts.</span><span class="sxs-lookup"><span data-stu-id="879f7-155">Action Groups provide a modular and reusable way of triggering actions for your Azure Alerts.</span></span> <span data-ttu-id="879f7-156">You can use Action Groups with metric alerts, Activity Log alerts and Azure Log Analytics alerts in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="879f7-156">You can use Action Groups with metric alerts, Activity Log alerts and Azure Log Analytics alerts in Azure portal.</span></span>

<span data-ttu-id="879f7-157">Use the following procedure:</span><span class="sxs-lookup"><span data-stu-id="879f7-157">Use the following procedure:</span></span>

1. <span data-ttu-id="879f7-158">In Azure portal, click  **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="879f7-158">In Azure portal, click  **Monitor**.</span></span>
2. <span data-ttu-id="879f7-159">In the left pane, click  **Action groups**.</span><span class="sxs-lookup"><span data-stu-id="879f7-159">In the left pane, click  **Action groups**.</span></span> <span data-ttu-id="879f7-160">The **Add action group** window appears.</span><span class="sxs-lookup"><span data-stu-id="879f7-160">The **Add action group** window appears.</span></span>

    ![Action Groups](media/log-analytics-itsmc/action-groups.png)

3. <span data-ttu-id="879f7-162">Provide **Name** and **ShortName** for your action group.</span><span class="sxs-lookup"><span data-stu-id="879f7-162">Provide **Name** and **ShortName** for your action group.</span></span> <span data-ttu-id="879f7-163">Select the **Resource Group** and **Subscription** where you want to create your action group.</span><span class="sxs-lookup"><span data-stu-id="879f7-163">Select the **Resource Group** and **Subscription** where you want to create your action group.</span></span>

    ![Action Groups detail](media/log-analytics-itsmc/action-groups-details.png)

4. <span data-ttu-id="879f7-165">In the Actions list, select **ITSM** from the drop-down menu for **Action Type**.</span><span class="sxs-lookup"><span data-stu-id="879f7-165">In the Actions list, select **ITSM** from the drop-down menu for **Action Type**.</span></span> <span data-ttu-id="879f7-166">Provide a **Name** for the action and click **Edit details**.</span><span class="sxs-lookup"><span data-stu-id="879f7-166">Provide a **Name** for the action and click **Edit details**.</span></span>
5. <span data-ttu-id="879f7-167">Select the **Subscription** where your Log Analytics workspace is located.</span><span class="sxs-lookup"><span data-stu-id="879f7-167">Select the **Subscription** where your Log Analytics workspace is located.</span></span> <span data-ttu-id="879f7-168">Select the **Connection** name (your ITSM Connector name) followed by your Workspace name.</span><span class="sxs-lookup"><span data-stu-id="879f7-168">Select the **Connection** name (your ITSM Connector name) followed by your Workspace name.</span></span> <span data-ttu-id="879f7-169">For example, "MyITSMMConnector(MyWorkspace)."</span><span class="sxs-lookup"><span data-stu-id="879f7-169">For example, "MyITSMMConnector(MyWorkspace)."</span></span>

    ![ITSM Action details](./media/log-analytics-itsmc/itsm-action-details.png)

6. <span data-ttu-id="879f7-171">Select **Work Item** type from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="879f7-171">Select **Work Item** type from the drop-down menu.</span></span>
   <span data-ttu-id="879f7-172">Choose to use an existing template or fill the fields required by your ITSM product.</span><span class="sxs-lookup"><span data-stu-id="879f7-172">Choose to use an existing template or fill the fields required by your ITSM product.</span></span>
7. <span data-ttu-id="879f7-173">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="879f7-173">Click **OK**.</span></span>

<span data-ttu-id="879f7-174">When creating/editing an Azure alert rule, use an Action group, which has an ITSM Action.</span><span class="sxs-lookup"><span data-stu-id="879f7-174">When creating/editing an Azure alert rule, use an Action group, which has an ITSM Action.</span></span> <span data-ttu-id="879f7-175">When the alert triggers, work item is created/updated in the ITSM tool.</span><span class="sxs-lookup"><span data-stu-id="879f7-175">When the alert triggers, work item is created/updated in the ITSM tool.</span></span>

>[!NOTE]

> <span data-ttu-id="879f7-176">For information on pricing of ITSM Action, see the [pricing page](https://azure.microsoft.com/pricing/details/monitor/) for Action Groups.</span><span class="sxs-lookup"><span data-stu-id="879f7-176">For information on pricing of ITSM Action, see the [pricing page](https://azure.microsoft.com/pricing/details/monitor/) for Action Groups.</span></span>


## <a name="create-itsm-work-items-from-log-analytics-alerts"></a><span data-ttu-id="879f7-177">Create ITSM work items from Log Analytics alerts</span><span class="sxs-lookup"><span data-stu-id="879f7-177">Create ITSM work items from Log Analytics alerts</span></span>

<span data-ttu-id="879f7-178">You can configure alert rules in Azure Log Analytics portal to create work items in ITSM tool, using the following procedure.</span><span class="sxs-lookup"><span data-stu-id="879f7-178">You can configure alert rules in Azure Log Analytics portal to create work items in ITSM tool, using the following procedure.</span></span>

1. <span data-ttu-id="879f7-179">From **Log Search** window, run a log search query to view data.</span><span class="sxs-lookup"><span data-stu-id="879f7-179">From **Log Search** window, run a log search query to view data.</span></span> <span data-ttu-id="879f7-180">Query results are the source for work items.</span><span class="sxs-lookup"><span data-stu-id="879f7-180">Query results are the source for work items.</span></span>
2. <span data-ttu-id="879f7-181">In **Log Search**, click **Alert** to open the **Add Alert Rule** page.</span><span class="sxs-lookup"><span data-stu-id="879f7-181">In **Log Search**, click **Alert** to open the **Add Alert Rule** page.</span></span>

    ![Log Analytics screen](./media/log-analytics-itsmc/itsmc-work-items-for-azure-alerts.png)

3. <span data-ttu-id="879f7-183">On the **Add Alert Rule** window, provide the required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span><span class="sxs-lookup"><span data-stu-id="879f7-183">On the **Add Alert Rule** window, provide the required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="879f7-184">Select **Yes** for **ITSM Actions**.</span><span class="sxs-lookup"><span data-stu-id="879f7-184">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="879f7-185">Select your ITSM connection from the **Select Connection** list.</span><span class="sxs-lookup"><span data-stu-id="879f7-185">Select your ITSM connection from the **Select Connection** list.</span></span>
6. <span data-ttu-id="879f7-186">Provide the details as required.</span><span class="sxs-lookup"><span data-stu-id="879f7-186">Provide the details as required.</span></span>
7. <span data-ttu-id="879f7-187">To create a separate work item for each log entry of this alert, select the **Create individual work items for each log entry** checkbox.</span><span class="sxs-lookup"><span data-stu-id="879f7-187">To create a separate work item for each log entry of this alert, select the **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="879f7-188">Or</span><span class="sxs-lookup"><span data-stu-id="879f7-188">Or</span></span>

    <span data-ttu-id="879f7-189">leave this checkbox unselected to create only one work item for any number of log entries under this alert.</span><span class="sxs-lookup"><span data-stu-id="879f7-189">leave this checkbox unselected to create only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="879f7-190">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="879f7-190">Click **Save**.</span></span>

<span data-ttu-id="879f7-191">You can view the  Log Analytics alert that you created under **Settings>Alerts**.</span><span class="sxs-lookup"><span data-stu-id="879f7-191">You can view the  Log Analytics alert that you created under **Settings>Alerts**.</span></span> <span data-ttu-id="879f7-192">The corresponding ITSM connection's work items are created when the specified alert's condition is met.</span><span class="sxs-lookup"><span data-stu-id="879f7-192">The corresponding ITSM connection's work items are created when the specified alert's condition is met.</span></span>


## <a name="create-itsm-work-items-from-log-analytics-log-records"></a><span data-ttu-id="879f7-193">Create ITSM work items from Log Analytics log records</span><span class="sxs-lookup"><span data-stu-id="879f7-193">Create ITSM work items from Log Analytics log records</span></span>

<span data-ttu-id="879f7-194">You can also create work items in the connected ITSM sources directly from a log record.</span><span class="sxs-lookup"><span data-stu-id="879f7-194">You can also create work items in the connected ITSM sources directly from a log record.</span></span> <span data-ttu-id="879f7-195">This can be used to test if the connection is working properly.</span><span class="sxs-lookup"><span data-stu-id="879f7-195">This can be used to test if the connection is working properly.</span></span>


1. <span data-ttu-id="879f7-196">From **Log Search**,  search the required data, select the detail, and click **Create work item**.</span><span class="sxs-lookup"><span data-stu-id="879f7-196">From **Log Search**,  search the required data, select the detail, and click **Create work item**.</span></span>

    <span data-ttu-id="879f7-197">The **Create ITSM Work Item** window appears:</span><span class="sxs-lookup"><span data-stu-id="879f7-197">The **Create ITSM Work Item** window appears:</span></span>

    ![Log Analytics screen](media/log-analytics-itsmc/itsmc-work-items-from-azure-logs.png)

2.   <span data-ttu-id="879f7-199">Add the following details:</span><span class="sxs-lookup"><span data-stu-id="879f7-199">Add the following details:</span></span>

  - <span data-ttu-id="879f7-200">**Work item Title**: Title for the work item.</span><span class="sxs-lookup"><span data-stu-id="879f7-200">**Work item Title**: Title for the work item.</span></span>
  - <span data-ttu-id="879f7-201">**Work item Description**: Description for the new work item.</span><span class="sxs-lookup"><span data-stu-id="879f7-201">**Work item Description**: Description for the new work item.</span></span>
  - <span data-ttu-id="879f7-202">**Affected Computer**: Name of the computer where this log data was found.</span><span class="sxs-lookup"><span data-stu-id="879f7-202">**Affected Computer**: Name of the computer where this log data was found.</span></span>
  - <span data-ttu-id="879f7-203">**Select Connection**:  ITSM connection in which you want to create this work item.</span><span class="sxs-lookup"><span data-stu-id="879f7-203">**Select Connection**:  ITSM connection in which you want to create this work item.</span></span>
  - <span data-ttu-id="879f7-204">**Work item**:  Type of work item.</span><span class="sxs-lookup"><span data-stu-id="879f7-204">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="879f7-205">To use an existing work item template for an incident, click **Yes** under **Generate Work item based on Template** option and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="879f7-205">To use an existing work item template for an incident, click **Yes** under **Generate Work item based on Template** option and then click **Create**.</span></span>

    <span data-ttu-id="879f7-206">Or,</span><span class="sxs-lookup"><span data-stu-id="879f7-206">Or,</span></span>

    <span data-ttu-id="879f7-207">Click **No** if you want to provide your customized values.</span><span class="sxs-lookup"><span data-stu-id="879f7-207">Click **No** if you want to provide your customized values.</span></span>

4. <span data-ttu-id="879f7-208">Provide the appropriate values in the **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="879f7-208">Provide the appropriate values in the **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>


## <a name="visualize-and-analyze-the-incident-and-change-request-data"></a><span data-ttu-id="879f7-209">Visualize and analyze the incident and change request data</span><span class="sxs-lookup"><span data-stu-id="879f7-209">Visualize and analyze the incident and change request data</span></span>

<span data-ttu-id="879f7-210">Based on your configuration when setting up a connection, ITSM connector can sync up to 120 days of Incident and Change request data.</span><span class="sxs-lookup"><span data-stu-id="879f7-210">Based on your configuration when setting up a connection, ITSM connector can sync up to 120 days of Incident and Change request data.</span></span> <span data-ttu-id="879f7-211">The log record schema for this data is provided in the [next section](#additional-information).</span><span class="sxs-lookup"><span data-stu-id="879f7-211">The log record schema for this data is provided in the [next section](#additional-information).</span></span>

<span data-ttu-id="879f7-212">The incident and change request data can be visualized using the ITSM Connector dashboard in the solution.</span><span class="sxs-lookup"><span data-stu-id="879f7-212">The incident and change request data can be visualized using the ITSM Connector dashboard in the solution.</span></span>

![Log Analytics screen](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

<span data-ttu-id="879f7-214">The dashboard also provides information on connector status which can be used as a starting point to analyze any issues with the connections.</span><span class="sxs-lookup"><span data-stu-id="879f7-214">The dashboard also provides information on connector status which can be used as a starting point to analyze any issues with the connections.</span></span>

<span data-ttu-id="879f7-215">You can also visualize the incidents synced against the impacted computers, within the Service Map solution.</span><span class="sxs-lookup"><span data-stu-id="879f7-215">You can also visualize the incidents synced against the impacted computers, within the Service Map solution.</span></span>

<span data-ttu-id="879f7-216">Service Map automatically discovers the application components on Windows and Linux systems and maps the communication between services.</span><span class="sxs-lookup"><span data-stu-id="879f7-216">Service Map automatically discovers the application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="879f7-217">It allows you to view your servers as you think of them – as interconnected systems that deliver critical services.</span><span class="sxs-lookup"><span data-stu-id="879f7-217">It allows you to view your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="879f7-218">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span><span class="sxs-lookup"><span data-stu-id="879f7-218">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="879f7-219">[Learn more](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="879f7-219">[Learn more](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="879f7-220">If you are using the Service Map solution, you can view the service desk items created in the ITSM solutions as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="879f7-220">If you are using the Service Map solution, you can view the service desk items created in the ITSM solutions as shown in the following example:</span></span>

![Log Analytics screen](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)

<span data-ttu-id="879f7-222">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md)</span><span class="sxs-lookup"><span data-stu-id="879f7-222">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md)</span></span>


## <a name="additional-information"></a><span data-ttu-id="879f7-223">Additional information</span><span class="sxs-lookup"><span data-stu-id="879f7-223">Additional information</span></span>

### <a name="data-synced-from-itsm-product"></a><span data-ttu-id="879f7-224">Data synced from ITSM product</span><span class="sxs-lookup"><span data-stu-id="879f7-224">Data synced from ITSM product</span></span>
<span data-ttu-id="879f7-225">Incidents and change requests are synced from your ITSM product to your Log Analytics workspace based on the connection's configuration.</span><span class="sxs-lookup"><span data-stu-id="879f7-225">Incidents and change requests are synced from your ITSM product to your Log Analytics workspace based on the connection's configuration.</span></span>

<span data-ttu-id="879f7-226">The following information shows examples of data gathered by ITSMC:</span><span class="sxs-lookup"><span data-stu-id="879f7-226">The following information shows examples of data gathered by ITSMC:</span></span>

> [!NOTE]

> <span data-ttu-id="879f7-227">Depending on the work item type imported into Log Analytics, **ServiceDesk_CL** contains the following fields:</span><span class="sxs-lookup"><span data-stu-id="879f7-227">Depending on the work item type imported into Log Analytics, **ServiceDesk_CL** contains the following fields:</span></span>

<span data-ttu-id="879f7-228">**Work item:** **Incidents**</span><span class="sxs-lookup"><span data-stu-id="879f7-228">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="879f7-229">ServiceDeskWorkItemType_s="Incident"</span><span class="sxs-lookup"><span data-stu-id="879f7-229">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="879f7-230">**Fields**</span><span class="sxs-lookup"><span data-stu-id="879f7-230">**Fields**</span></span>

- <span data-ttu-id="879f7-231">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="879f7-231">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="879f7-232">Service Desk ID</span><span class="sxs-lookup"><span data-stu-id="879f7-232">Service Desk ID</span></span>
- <span data-ttu-id="879f7-233">State</span><span class="sxs-lookup"><span data-stu-id="879f7-233">State</span></span>
- <span data-ttu-id="879f7-234">Urgency</span><span class="sxs-lookup"><span data-stu-id="879f7-234">Urgency</span></span>
- <span data-ttu-id="879f7-235">Impact</span><span class="sxs-lookup"><span data-stu-id="879f7-235">Impact</span></span>
- <span data-ttu-id="879f7-236">Priority</span><span class="sxs-lookup"><span data-stu-id="879f7-236">Priority</span></span>
- <span data-ttu-id="879f7-237">Escalation</span><span class="sxs-lookup"><span data-stu-id="879f7-237">Escalation</span></span>
- <span data-ttu-id="879f7-238">Created By</span><span class="sxs-lookup"><span data-stu-id="879f7-238">Created By</span></span>
- <span data-ttu-id="879f7-239">Resolved By</span><span class="sxs-lookup"><span data-stu-id="879f7-239">Resolved By</span></span>
- <span data-ttu-id="879f7-240">Closed By</span><span class="sxs-lookup"><span data-stu-id="879f7-240">Closed By</span></span>
- <span data-ttu-id="879f7-241">Source</span><span class="sxs-lookup"><span data-stu-id="879f7-241">Source</span></span>
- <span data-ttu-id="879f7-242">Assigned To</span><span class="sxs-lookup"><span data-stu-id="879f7-242">Assigned To</span></span>
- <span data-ttu-id="879f7-243">Category</span><span class="sxs-lookup"><span data-stu-id="879f7-243">Category</span></span>
- <span data-ttu-id="879f7-244">Title</span><span class="sxs-lookup"><span data-stu-id="879f7-244">Title</span></span>
- <span data-ttu-id="879f7-245">Description</span><span class="sxs-lookup"><span data-stu-id="879f7-245">Description</span></span>
- <span data-ttu-id="879f7-246">Created Date</span><span class="sxs-lookup"><span data-stu-id="879f7-246">Created Date</span></span>
- <span data-ttu-id="879f7-247">Closed Date</span><span class="sxs-lookup"><span data-stu-id="879f7-247">Closed Date</span></span>
- <span data-ttu-id="879f7-248">Resolved Date</span><span class="sxs-lookup"><span data-stu-id="879f7-248">Resolved Date</span></span>
- <span data-ttu-id="879f7-249">Last Modified Date</span><span class="sxs-lookup"><span data-stu-id="879f7-249">Last Modified Date</span></span>
- <span data-ttu-id="879f7-250">Computer</span><span class="sxs-lookup"><span data-stu-id="879f7-250">Computer</span></span>


<span data-ttu-id="879f7-251">**Work item:** **Change Requests**</span><span class="sxs-lookup"><span data-stu-id="879f7-251">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="879f7-252">ServiceDeskWorkItemType_s="ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="879f7-252">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="879f7-253">**Fields**</span><span class="sxs-lookup"><span data-stu-id="879f7-253">**Fields**</span></span>
- <span data-ttu-id="879f7-254">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="879f7-254">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="879f7-255">Service Desk ID</span><span class="sxs-lookup"><span data-stu-id="879f7-255">Service Desk ID</span></span>
- <span data-ttu-id="879f7-256">Created By</span><span class="sxs-lookup"><span data-stu-id="879f7-256">Created By</span></span>
- <span data-ttu-id="879f7-257">Closed By</span><span class="sxs-lookup"><span data-stu-id="879f7-257">Closed By</span></span>
- <span data-ttu-id="879f7-258">Source</span><span class="sxs-lookup"><span data-stu-id="879f7-258">Source</span></span>
- <span data-ttu-id="879f7-259">Assigned To</span><span class="sxs-lookup"><span data-stu-id="879f7-259">Assigned To</span></span>
- <span data-ttu-id="879f7-260">Title</span><span class="sxs-lookup"><span data-stu-id="879f7-260">Title</span></span>
- <span data-ttu-id="879f7-261">Type</span><span class="sxs-lookup"><span data-stu-id="879f7-261">Type</span></span>
- <span data-ttu-id="879f7-262">Category</span><span class="sxs-lookup"><span data-stu-id="879f7-262">Category</span></span>
- <span data-ttu-id="879f7-263">State</span><span class="sxs-lookup"><span data-stu-id="879f7-263">State</span></span>
- <span data-ttu-id="879f7-264">Escalation</span><span class="sxs-lookup"><span data-stu-id="879f7-264">Escalation</span></span>
- <span data-ttu-id="879f7-265">Conflict Status</span><span class="sxs-lookup"><span data-stu-id="879f7-265">Conflict Status</span></span>
- <span data-ttu-id="879f7-266">Urgency</span><span class="sxs-lookup"><span data-stu-id="879f7-266">Urgency</span></span>
- <span data-ttu-id="879f7-267">Priority</span><span class="sxs-lookup"><span data-stu-id="879f7-267">Priority</span></span>
- <span data-ttu-id="879f7-268">Risk</span><span class="sxs-lookup"><span data-stu-id="879f7-268">Risk</span></span>
- <span data-ttu-id="879f7-269">Impact</span><span class="sxs-lookup"><span data-stu-id="879f7-269">Impact</span></span>
- <span data-ttu-id="879f7-270">Assigned To</span><span class="sxs-lookup"><span data-stu-id="879f7-270">Assigned To</span></span>
- <span data-ttu-id="879f7-271">Created Date</span><span class="sxs-lookup"><span data-stu-id="879f7-271">Created Date</span></span>
- <span data-ttu-id="879f7-272">Closed Date</span><span class="sxs-lookup"><span data-stu-id="879f7-272">Closed Date</span></span>
- <span data-ttu-id="879f7-273">Last Modified Date</span><span class="sxs-lookup"><span data-stu-id="879f7-273">Last Modified Date</span></span>
- <span data-ttu-id="879f7-274">Requested Date</span><span class="sxs-lookup"><span data-stu-id="879f7-274">Requested Date</span></span>
- <span data-ttu-id="879f7-275">Planned Start Date</span><span class="sxs-lookup"><span data-stu-id="879f7-275">Planned Start Date</span></span>
- <span data-ttu-id="879f7-276">Planned End Date</span><span class="sxs-lookup"><span data-stu-id="879f7-276">Planned End Date</span></span>
- <span data-ttu-id="879f7-277">Work Start Date</span><span class="sxs-lookup"><span data-stu-id="879f7-277">Work Start Date</span></span>
- <span data-ttu-id="879f7-278">Work End Date</span><span class="sxs-lookup"><span data-stu-id="879f7-278">Work End Date</span></span>
- <span data-ttu-id="879f7-279">Description</span><span class="sxs-lookup"><span data-stu-id="879f7-279">Description</span></span>
- <span data-ttu-id="879f7-280">Computer</span><span class="sxs-lookup"><span data-stu-id="879f7-280">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="879f7-281">Output data for a ServiceNow incident</span><span class="sxs-lookup"><span data-stu-id="879f7-281">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="879f7-282">Log Analytics field</span><span class="sxs-lookup"><span data-stu-id="879f7-282">Log Analytics field</span></span> | <span data-ttu-id="879f7-283">ServiceNow field</span><span class="sxs-lookup"><span data-stu-id="879f7-283">ServiceNow field</span></span> |
|:--- |:--- |
| <span data-ttu-id="879f7-284">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="879f7-284">ServiceDeskId_s</span></span>| <span data-ttu-id="879f7-285">Number</span><span class="sxs-lookup"><span data-stu-id="879f7-285">Number</span></span> |
| <span data-ttu-id="879f7-286">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="879f7-286">IncidentState_s</span></span> | <span data-ttu-id="879f7-287">State</span><span class="sxs-lookup"><span data-stu-id="879f7-287">State</span></span> |
| <span data-ttu-id="879f7-288">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="879f7-288">Urgency_s</span></span> |<span data-ttu-id="879f7-289">Urgency</span><span class="sxs-lookup"><span data-stu-id="879f7-289">Urgency</span></span> |
| <span data-ttu-id="879f7-290">Impact_s</span><span class="sxs-lookup"><span data-stu-id="879f7-290">Impact_s</span></span> |<span data-ttu-id="879f7-291">Impact</span><span class="sxs-lookup"><span data-stu-id="879f7-291">Impact</span></span>|
| <span data-ttu-id="879f7-292">Priority_s</span><span class="sxs-lookup"><span data-stu-id="879f7-292">Priority_s</span></span> | <span data-ttu-id="879f7-293">Priority</span><span class="sxs-lookup"><span data-stu-id="879f7-293">Priority</span></span> |
| <span data-ttu-id="879f7-294">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="879f7-294">CreatedBy_s</span></span> | <span data-ttu-id="879f7-295">Opened by</span><span class="sxs-lookup"><span data-stu-id="879f7-295">Opened by</span></span> |
| <span data-ttu-id="879f7-296">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="879f7-296">ResolvedBy_s</span></span> | <span data-ttu-id="879f7-297">Resolved by</span><span class="sxs-lookup"><span data-stu-id="879f7-297">Resolved by</span></span>|
| <span data-ttu-id="879f7-298">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="879f7-298">ClosedBy_s</span></span>  | <span data-ttu-id="879f7-299">Closed by</span><span class="sxs-lookup"><span data-stu-id="879f7-299">Closed by</span></span> |
| <span data-ttu-id="879f7-300">Source_s</span><span class="sxs-lookup"><span data-stu-id="879f7-300">Source_s</span></span>| <span data-ttu-id="879f7-301">Contact type</span><span class="sxs-lookup"><span data-stu-id="879f7-301">Contact type</span></span> |
| <span data-ttu-id="879f7-302">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="879f7-302">AssignedTo_s</span></span> | <span data-ttu-id="879f7-303">Assigned to</span><span class="sxs-lookup"><span data-stu-id="879f7-303">Assigned to</span></span>  |
| <span data-ttu-id="879f7-304">Category_s</span><span class="sxs-lookup"><span data-stu-id="879f7-304">Category_s</span></span> | <span data-ttu-id="879f7-305">Category</span><span class="sxs-lookup"><span data-stu-id="879f7-305">Category</span></span> |
| <span data-ttu-id="879f7-306">Title_s</span><span class="sxs-lookup"><span data-stu-id="879f7-306">Title_s</span></span>|  <span data-ttu-id="879f7-307">Short description</span><span class="sxs-lookup"><span data-stu-id="879f7-307">Short description</span></span> |
| <span data-ttu-id="879f7-308">Description_s</span><span class="sxs-lookup"><span data-stu-id="879f7-308">Description_s</span></span>|  <span data-ttu-id="879f7-309">Notes</span><span class="sxs-lookup"><span data-stu-id="879f7-309">Notes</span></span> |
| <span data-ttu-id="879f7-310">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="879f7-310">CreatedDate_t</span></span>|  <span data-ttu-id="879f7-311">Opened</span><span class="sxs-lookup"><span data-stu-id="879f7-311">Opened</span></span> |
| <span data-ttu-id="879f7-312">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="879f7-312">ClosedDate_t</span></span>| <span data-ttu-id="879f7-313">closed</span><span class="sxs-lookup"><span data-stu-id="879f7-313">closed</span></span>|
| <span data-ttu-id="879f7-314">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="879f7-314">ResolvedDate_t</span></span>|<span data-ttu-id="879f7-315">Resolved</span><span class="sxs-lookup"><span data-stu-id="879f7-315">Resolved</span></span>|
| <span data-ttu-id="879f7-316">Computer</span><span class="sxs-lookup"><span data-stu-id="879f7-316">Computer</span></span>  | <span data-ttu-id="879f7-317">Configuration item</span><span class="sxs-lookup"><span data-stu-id="879f7-317">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="879f7-318">Output data for a ServiceNow change request</span><span class="sxs-lookup"><span data-stu-id="879f7-318">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="879f7-319">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="879f7-319">Log Analytics</span></span> | <span data-ttu-id="879f7-320">ServieNow field</span><span class="sxs-lookup"><span data-stu-id="879f7-320">ServieNow field</span></span> |
|:--- |:--- |
| <span data-ttu-id="879f7-321">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="879f7-321">ServiceDeskId_s</span></span>| <span data-ttu-id="879f7-322">Number</span><span class="sxs-lookup"><span data-stu-id="879f7-322">Number</span></span> |
| <span data-ttu-id="879f7-323">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="879f7-323">CreatedBy_s</span></span> | <span data-ttu-id="879f7-324">Requested by</span><span class="sxs-lookup"><span data-stu-id="879f7-324">Requested by</span></span> |
| <span data-ttu-id="879f7-325">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="879f7-325">ClosedBy_s</span></span> | <span data-ttu-id="879f7-326">Closed by</span><span class="sxs-lookup"><span data-stu-id="879f7-326">Closed by</span></span> |
| <span data-ttu-id="879f7-327">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="879f7-327">AssignedTo_s</span></span> | <span data-ttu-id="879f7-328">Assigned to</span><span class="sxs-lookup"><span data-stu-id="879f7-328">Assigned to</span></span>  |
| <span data-ttu-id="879f7-329">Title_s</span><span class="sxs-lookup"><span data-stu-id="879f7-329">Title_s</span></span>|  <span data-ttu-id="879f7-330">Short description</span><span class="sxs-lookup"><span data-stu-id="879f7-330">Short description</span></span> |
| <span data-ttu-id="879f7-331">Type_s</span><span class="sxs-lookup"><span data-stu-id="879f7-331">Type_s</span></span>|  <span data-ttu-id="879f7-332">Type</span><span class="sxs-lookup"><span data-stu-id="879f7-332">Type</span></span> |
| <span data-ttu-id="879f7-333">Category_s</span><span class="sxs-lookup"><span data-stu-id="879f7-333">Category_s</span></span>|  <span data-ttu-id="879f7-334">Category</span><span class="sxs-lookup"><span data-stu-id="879f7-334">Category</span></span> |
| <span data-ttu-id="879f7-335">CRState_s</span><span class="sxs-lookup"><span data-stu-id="879f7-335">CRState_s</span></span>|  <span data-ttu-id="879f7-336">State</span><span class="sxs-lookup"><span data-stu-id="879f7-336">State</span></span>|
| <span data-ttu-id="879f7-337">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="879f7-337">Urgency_s</span></span>|  <span data-ttu-id="879f7-338">Urgency</span><span class="sxs-lookup"><span data-stu-id="879f7-338">Urgency</span></span> |
| <span data-ttu-id="879f7-339">Priority_s</span><span class="sxs-lookup"><span data-stu-id="879f7-339">Priority_s</span></span>| <span data-ttu-id="879f7-340">Priority</span><span class="sxs-lookup"><span data-stu-id="879f7-340">Priority</span></span>|
| <span data-ttu-id="879f7-341">Risk_s</span><span class="sxs-lookup"><span data-stu-id="879f7-341">Risk_s</span></span>| <span data-ttu-id="879f7-342">Risk</span><span class="sxs-lookup"><span data-stu-id="879f7-342">Risk</span></span>|
| <span data-ttu-id="879f7-343">Impact_s</span><span class="sxs-lookup"><span data-stu-id="879f7-343">Impact_s</span></span>| <span data-ttu-id="879f7-344">Impact</span><span class="sxs-lookup"><span data-stu-id="879f7-344">Impact</span></span>|
| <span data-ttu-id="879f7-345">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="879f7-345">RequestedDate_t</span></span>  | <span data-ttu-id="879f7-346">Requested by date</span><span class="sxs-lookup"><span data-stu-id="879f7-346">Requested by date</span></span> |
| <span data-ttu-id="879f7-347">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="879f7-347">ClosedDate_t</span></span> | <span data-ttu-id="879f7-348">Closed date</span><span class="sxs-lookup"><span data-stu-id="879f7-348">Closed date</span></span> |
| <span data-ttu-id="879f7-349">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="879f7-349">PlannedStartDate_t</span></span>  |     <span data-ttu-id="879f7-350">Planned start date</span><span class="sxs-lookup"><span data-stu-id="879f7-350">Planned start date</span></span> |
| <span data-ttu-id="879f7-351">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="879f7-351">PlannedEndDate_t</span></span>  |   <span data-ttu-id="879f7-352">Planned end date</span><span class="sxs-lookup"><span data-stu-id="879f7-352">Planned end date</span></span> |
| <span data-ttu-id="879f7-353">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="879f7-353">WorkStartDate_t</span></span>  | <span data-ttu-id="879f7-354">Actual start date</span><span class="sxs-lookup"><span data-stu-id="879f7-354">Actual start date</span></span> |
| <span data-ttu-id="879f7-355">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="879f7-355">WorkEndDate_t</span></span> | <span data-ttu-id="879f7-356">Actual end date</span><span class="sxs-lookup"><span data-stu-id="879f7-356">Actual end date</span></span>|
| <span data-ttu-id="879f7-357">Description_s</span><span class="sxs-lookup"><span data-stu-id="879f7-357">Description_s</span></span> | <span data-ttu-id="879f7-358">Description</span><span class="sxs-lookup"><span data-stu-id="879f7-358">Description</span></span> |
| <span data-ttu-id="879f7-359">Computer</span><span class="sxs-lookup"><span data-stu-id="879f7-359">Computer</span></span>  | <span data-ttu-id="879f7-360">Configuration Item</span><span class="sxs-lookup"><span data-stu-id="879f7-360">Configuration Item</span></span> |


## <a name="troubleshoot-itsm-connections"></a><span data-ttu-id="879f7-361">Troubleshoot ITSM connections</span><span class="sxs-lookup"><span data-stu-id="879f7-361">Troubleshoot ITSM connections</span></span>
1.  <span data-ttu-id="879f7-362">If connection fails from connected source's UI with an **Error in saving connection** message, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="879f7-362">If connection fails from connected source's UI with an **Error in saving connection** message, take the following steps:</span></span>
- <span data-ttu-id="879f7-363">For ServiceNow, Cherwell and Provance connections,</span><span class="sxs-lookup"><span data-stu-id="879f7-363">For ServiceNow, Cherwell and Provance connections,</span></span>  
    - <span data-ttu-id="879f7-364">ensure you correctly entered  the username, password, client ID, and client secret  for each of the connections.</span><span class="sxs-lookup"><span data-stu-id="879f7-364">ensure you correctly entered  the username, password, client ID, and client secret  for each of the connections.</span></span>  
    - <span data-ttu-id="879f7-365">check if you have sufficient privileges in the corresponding ITSM product to make the connection.</span><span class="sxs-lookup"><span data-stu-id="879f7-365">check if you have sufficient privileges in the corresponding ITSM product to make the connection.</span></span>  
- <span data-ttu-id="879f7-366">For Service Manager connections,</span><span class="sxs-lookup"><span data-stu-id="879f7-366">For Service Manager connections,</span></span>  
    - <span data-ttu-id="879f7-367">ensure that the Web app is successfully deployed and hybrid connection is created.</span><span class="sxs-lookup"><span data-stu-id="879f7-367">ensure that the Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="879f7-368">To verify the connection is successfully established with the on-prem Service Manager machine, visit the  Web app URL as detailed in the documentation for making the [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="879f7-368">To verify the connection is successfully established with the on-prem Service Manager machine, visit the  Web app URL as detailed in the documentation for making the [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>  

2.  <span data-ttu-id="879f7-369">If data from ServiceNow is not getting synced to Log Analytics, ensure that the ServiceNow instance is not sleeping.</span><span class="sxs-lookup"><span data-stu-id="879f7-369">If data from ServiceNow is not getting synced to Log Analytics, ensure that the ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="879f7-370">ServiceNow Dev Instances sometimes go to sleep when idle for a long period.</span><span class="sxs-lookup"><span data-stu-id="879f7-370">ServiceNow Dev Instances sometimes go to sleep when idle for a long period.</span></span> <span data-ttu-id="879f7-371">Else, report the issue.</span><span class="sxs-lookup"><span data-stu-id="879f7-371">Else, report the issue.</span></span>
3.  <span data-ttu-id="879f7-372">If OMS Alerts fire but work items are not created in ITSM product or configuration items are not created/linked to work items or for any other generic information, look in the following places:</span><span class="sxs-lookup"><span data-stu-id="879f7-372">If OMS Alerts fire but work items are not created in ITSM product or configuration items are not created/linked to work items or for any other generic information, look in the following places:</span></span>
 -  <span data-ttu-id="879f7-373">ITSMC: The solution shows a summary of connections/work items/computers etc. Click the tile showing **Connector Status**, which takes you to **Log Search**  with the relevant query.</span><span class="sxs-lookup"><span data-stu-id="879f7-373">ITSMC: The solution shows a summary of connections/work items/computers etc. Click the tile showing **Connector Status**, which takes you to **Log Search**  with the relevant query.</span></span> <span data-ttu-id="879f7-374">Look at the log records with LogType_S as ERROR for more information.</span><span class="sxs-lookup"><span data-stu-id="879f7-374">Look at the log records with LogType_S as ERROR for more information.</span></span>
 - <span data-ttu-id="879f7-375">**Log Search** page: view the errors/related information directly using the query `*`ServiceDeskLog_CL`*`.</span><span class="sxs-lookup"><span data-stu-id="879f7-375">**Log Search** page: view the errors/related information directly using the query `*`ServiceDeskLog_CL`*`.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="879f7-376">Troubleshoot Service Manager Web App deployment</span><span class="sxs-lookup"><span data-stu-id="879f7-376">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="879f7-377">In case of any issues with web app deployment, ensure you have sufficient permissions in the subscription mentioned to create/deploy resources.</span><span class="sxs-lookup"><span data-stu-id="879f7-377">In case of any issues with web app deployment, ensure you have sufficient permissions in the subscription mentioned to create/deploy resources.</span></span>
2.  <span data-ttu-id="879f7-378">If you get an **"Object reference not set to instance of an object"** error when you run the [script](log-analytics-itsmc-service-manager-script.md), ensure that you entered valid values  under **User Configuration** section.</span><span class="sxs-lookup"><span data-stu-id="879f7-378">If you get an **"Object reference not set to instance of an object"** error when you run the [script](log-analytics-itsmc-service-manager-script.md), ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="879f7-379">If you fail to create service bus relay namespace, ensure that the required resource provider is registered in the subscription.</span><span class="sxs-lookup"><span data-stu-id="879f7-379">If you fail to create service bus relay namespace, ensure that the required resource provider is registered in the subscription.</span></span> <span data-ttu-id="879f7-380">If not registered, manually create service bus relay namespace from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="879f7-380">If not registered, manually create service bus relay namespace from the Azure portal.</span></span> <span data-ttu-id="879f7-381">You can also create it while [creating the hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="879f7-381">You can also create it while [creating the hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from the Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="879f7-382">Contact us</span><span class="sxs-lookup"><span data-stu-id="879f7-382">Contact us</span></span>

<span data-ttu-id="879f7-383">For any queries or feedback on the IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="879f7-383">For any queries or feedback on the IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="879f7-384">Next steps</span><span class="sxs-lookup"><span data-stu-id="879f7-384">Next steps</span></span>
<span data-ttu-id="879f7-385">[Add ITSM products/services to IT Service Management Connector](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="879f7-385">[Add ITSM products/services to IT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>

            
