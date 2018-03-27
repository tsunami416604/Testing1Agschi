---
title: IT služby konektoru Management v Azure Log Analytics | Microsoft Docs
description: Tento článek obsahuje přehled IT služby správy konektoru (ITSMC) a informace o tom, jak používat toto řešení centrálně monitorovat a spravovat ITSM pracovních položek v Azure Log Analytics a rychle vyřešit všechny problémy.
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
ms.openlocfilehash: a51b96641c80a6575c64f58fa09e0bf6078e4185
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/23/2018
---
# <a name="connect-azure-to-itsm-tools-using-it-service-management-connector"></a><span data-ttu-id="66e7a-103">Připojení Azure k nástrojům ITSM pomocí konektoru služby správy IT</span><span class="sxs-lookup"><span data-stu-id="66e7a-103">Connect Azure to ITSM tools using IT Service Management Connector</span></span>

![Symbol konektoru služby správy IT](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="66e7a-105">Konektor pro správu služby IT (ITSMC) umožňuje připojit Azure a podporovaných produktu nebo služby IT služby správy (ITSM).</span><span class="sxs-lookup"><span data-stu-id="66e7a-105">The IT Service Management Connector (ITSMC) allows you to connect Azure and a supported IT Service Management (ITSM) product/service.</span></span>

<span data-ttu-id="66e7a-106">Azure services jako analýzy protokolů a monitorování Azure poskytuje nástroje ke zjišťování, analýze a řešení problémů s Azure a prostředky mimo Azure.</span><span class="sxs-lookup"><span data-stu-id="66e7a-106">Azure services like Log Analytics and Azure Monitor provide tools to detect, analyze and troubleshoot issues with your Azure and non-Azure resources.</span></span> <span data-ttu-id="66e7a-107">Pracovní položky související s problém obvykle však nacházet v produktu nebo službě ITSM.</span><span class="sxs-lookup"><span data-stu-id="66e7a-107">However, the work items related to an issue  typically reside in an ITSM product/service.</span></span> <span data-ttu-id="66e7a-108">Konektor ITSM poskytuje obousměrné připojení mezi Azure a ITSM nástroje k řešení problémů rychlejší.</span><span class="sxs-lookup"><span data-stu-id="66e7a-108">The ITSM connector provides a bi-directional connection between Azure and ITSM tools to help you resolve issues faster.</span></span>

<span data-ttu-id="66e7a-109">ITSMC podporuje připojení s následující ITSM nástroje:</span><span class="sxs-lookup"><span data-stu-id="66e7a-109">ITSMC supports connections with the following ITSM tools:</span></span>

-   <span data-ttu-id="66e7a-110">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="66e7a-110">ServiceNow</span></span>
-   <span data-ttu-id="66e7a-111">System Center Service Manager</span><span class="sxs-lookup"><span data-stu-id="66e7a-111">System Center Service Manager</span></span>
-   <span data-ttu-id="66e7a-112">Provance</span><span class="sxs-lookup"><span data-stu-id="66e7a-112">Provance</span></span>
-   <span data-ttu-id="66e7a-113">Cherwell</span><span class="sxs-lookup"><span data-stu-id="66e7a-113">Cherwell</span></span>

<span data-ttu-id="66e7a-114">S ITSMC můžete</span><span class="sxs-lookup"><span data-stu-id="66e7a-114">With ITSMC, you can</span></span>

-  <span data-ttu-id="66e7a-115">Vytváření pracovních položek v nástroji ITSM, na základě vaší Azure výstrah (metriky výstrahy, protokol aktivit výstrahy a upozornění analýzy protokolů).</span><span class="sxs-lookup"><span data-stu-id="66e7a-115">Create work items in ITSM tool, based on your Azure alerts (metric alerts, Activity Log alerts and Log Analytics alerts).</span></span>
-  <span data-ttu-id="66e7a-116">Volitelně můžete synchronizovat vašeho incidentu a změnit data žádosti z vaší ITSM nástroj k pracovnímu prostoru analýzy protokolů Azure.</span><span class="sxs-lookup"><span data-stu-id="66e7a-116">Optionally, you can sync your incident and change request data from your ITSM tool to an Azure Log Analytics workspace.</span></span>


<span data-ttu-id="66e7a-117">Můžete začít používat konektor ITSM pomocí následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="66e7a-117">You can start using the ITSM Connector using the following steps:</span></span>

1.  [<span data-ttu-id="66e7a-118">Přidat řešení ITSM konektoru</span><span class="sxs-lookup"><span data-stu-id="66e7a-118">Add the ITSM Connector Solution</span></span>](#adding-the-it-service-management-connector-solution)
2.  [<span data-ttu-id="66e7a-119">Vytvoření připojení k ITSM</span><span class="sxs-lookup"><span data-stu-id="66e7a-119">Create an ITSM connection</span></span>](#creating-an-itsm-connection)
3.  [<span data-ttu-id="66e7a-120">Používat připojení</span><span class="sxs-lookup"><span data-stu-id="66e7a-120">Use the connection</span></span>](#using-the-solution)


##  <a name="adding-the-it-service-management-connector-solution"></a><span data-ttu-id="66e7a-121">Přidání IT řešení pro správu konektoru služby</span><span class="sxs-lookup"><span data-stu-id="66e7a-121">Adding the IT Service Management Connector Solution</span></span>

<span data-ttu-id="66e7a-122">Před vytvořením připojení, je nutné přidat řešení ITSM konektor.</span><span class="sxs-lookup"><span data-stu-id="66e7a-122">Before you can create a connection, you need to add the ITSM Connector Solution.</span></span>

1.  <span data-ttu-id="66e7a-123">Na portálu Azure, klikněte na tlačítko **+ nový** ikonu.</span><span class="sxs-lookup"><span data-stu-id="66e7a-123">In Azure portal, click **+ New** icon.</span></span>

    ![Azure nový prostředek](./media/log-analytics-itsmc/azure-add-new-resource.png)

2.  <span data-ttu-id="66e7a-125">Vyhledejte **IT Service Management Connector** Marketplace a klikněte na **vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="66e7a-125">Search for **IT Service Management Connector** in the Marketplace and click **Create**.</span></span>

    ![Přidat ITSMC řešení](./media/log-analytics-itsmc/add-itsmc-solution.png)

3.  <span data-ttu-id="66e7a-127">V **pracovním prostorem OMS** vyberte pracovní prostor analýzy protokolů Azure, kam chcete nainstalovat řešení.</span><span class="sxs-lookup"><span data-stu-id="66e7a-127">In the **OMS Workspace** section, select the Azure Log Analytics workspace where you want to install the solution.</span></span>
4.  <span data-ttu-id="66e7a-128">V **nastavení pracovního prostoru OMS** vyberte ResourceGroup, kde chcete vytvořit prostředek řešení.</span><span class="sxs-lookup"><span data-stu-id="66e7a-128">In the **OMS Workspace Settings** section, select the ResourceGroup where you want to create the solution resource.</span></span>

    ![Pracovní prostor ITSMC](./media/log-analytics-itsmc/itsmc-solution-workspace.png)

5.  <span data-ttu-id="66e7a-130">Klikněte na možnost **Vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="66e7a-130">Click **Create**.</span></span>

<span data-ttu-id="66e7a-131">Po nasazení řešení prostředků oznámení se zobrazí v horní pravé části okna.</span><span class="sxs-lookup"><span data-stu-id="66e7a-131">When the solution resource is deployed, a notification appears at the top right of the window.</span></span>


## <a name="creating-an-itsm--connection"></a><span data-ttu-id="66e7a-132">Vytvoření připojení k ITSM</span><span class="sxs-lookup"><span data-stu-id="66e7a-132">Creating an ITSM  connection</span></span>

<span data-ttu-id="66e7a-133">Po instalaci řešení, můžete vytvořit připojení.</span><span class="sxs-lookup"><span data-stu-id="66e7a-133">Once you have installed the solution, you can create a connection.</span></span>

<span data-ttu-id="66e7a-134">Pro vytvoření připojení, musíte připravená data vaše ITSM nástroje umožňující připojení z řešení ITSM konektor.</span><span class="sxs-lookup"><span data-stu-id="66e7a-134">For creating a connection, you will need to prep your ITSM tool to allow the connection from the ITSM Connector solution.</span></span>  

<span data-ttu-id="66e7a-135">V závislosti na produkt ITSM, ke kterému se připojujete použijte následující postup:</span><span class="sxs-lookup"><span data-stu-id="66e7a-135">Depending on the ITSM product you are connecting to, use the following steps :</span></span>

- [<span data-ttu-id="66e7a-136">System Center Service Manager (SCSM)</span><span class="sxs-lookup"><span data-stu-id="66e7a-136">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-azure)
- [<span data-ttu-id="66e7a-137">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="66e7a-137">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-azure)
- [<span data-ttu-id="66e7a-138">Provance</span><span class="sxs-lookup"><span data-stu-id="66e7a-138">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-azure)  
- [<span data-ttu-id="66e7a-139">Cherwell</span><span class="sxs-lookup"><span data-stu-id="66e7a-139">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-azure)

<span data-ttu-id="66e7a-140">Jakmile máte prepped vaše ITSM nástrojů, použijte následující postup k vytvoření připojení:</span><span class="sxs-lookup"><span data-stu-id="66e7a-140">Once you have prepped your ITSM tools, follow the steps below to create a connection:</span></span>

1.  <span data-ttu-id="66e7a-141">Přejděte na **všechny prostředky**, vyhledejte **ServiceDesk(YourWorkspaceName)**.</span><span class="sxs-lookup"><span data-stu-id="66e7a-141">Go to **All Resources**, look for **ServiceDesk(YourWorkspaceName)**.</span></span>
2.  <span data-ttu-id="66e7a-142">V části **zdroje dat pracovního prostoru** v levém podokně klikněte na **ITSM připojení**.</span><span class="sxs-lookup"><span data-stu-id="66e7a-142">Under **WORKSPACE DATA SOURCES** in the left pane, click **ITSM Connections**.</span></span>
    <span data-ttu-id="66e7a-143">![ITSM připojení](./media/log-analytics-itsmc/itsm-connections.png)</span><span class="sxs-lookup"><span data-stu-id="66e7a-143">![ITSM connections](./media/log-analytics-itsmc/itsm-connections.png)</span></span>

    <span data-ttu-id="66e7a-144">Tato stránka zobrazuje seznam připojení.</span><span class="sxs-lookup"><span data-stu-id="66e7a-144">This page displays the list of connections.</span></span>
3.  <span data-ttu-id="66e7a-145">Klikněte na tlačítko **přidat připojení**.</span><span class="sxs-lookup"><span data-stu-id="66e7a-145">Click **Add Connection**.</span></span>

    ![Přidat připojení ITSM](./media/log-analytics-itsmc/add-new-itsm-connection.png)

4.  <span data-ttu-id="66e7a-147">Zadejte nastavení připojení, jak je popsáno v [konfiguraci připojení ITSMC s váš článek produktů nebo služeb ITSM](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="66e7a-147">Specify the connection settings as described in [Configuring the ITSMC connection with your ITSM products/services article](log-analytics-itsmc-connections.md).</span></span>

    > [!NOTE]

    > <span data-ttu-id="66e7a-148">Ve výchozím nastavení aktualizuje ITSMC připojení konfigurační data jednou za každých 24 hodin.</span><span class="sxs-lookup"><span data-stu-id="66e7a-148">By default, ITSMC refreshes the connection's configuration data once in every 24 hours.</span></span> <span data-ttu-id="66e7a-149">Aktualizovat připojení k data okamžitě pro úpravy nebo aktualizace šablony, které provedete, klikněte na tlačítko "Aktualizace" zobrazí vedle připojení.</span><span class="sxs-lookup"><span data-stu-id="66e7a-149">To refresh your connection's data instantly for any edits or template updates that you make, click the "Refresh" button displayed next to your connection.</span></span>

    ![Aktualizace připojení](./media/log-analytics-itsmc/itsmc-connections-refresh.png)


## <a name="using-the-solution"></a><span data-ttu-id="66e7a-151">Použití řešení</span><span class="sxs-lookup"><span data-stu-id="66e7a-151">Using the solution</span></span>
   <span data-ttu-id="66e7a-152">Pomocí konektoru ITSM řešení můžete vytvořit pracovní položky z Azure výstrahy, analýzy protokolů výstrahy a analýzy protokolů záznamy protokolu.</span><span class="sxs-lookup"><span data-stu-id="66e7a-152">By using the ITSM Connector solution, you can create work items from Azure alerts, Log Analytics alerts  and  Log Analytics log records.</span></span>

## <a name="create-itsm-work-items-from-azure-alerts"></a><span data-ttu-id="66e7a-153">Vytváření pracovních položek ITSM z Azure výstrah</span><span class="sxs-lookup"><span data-stu-id="66e7a-153">Create ITSM work items from Azure alerts</span></span>

<span data-ttu-id="66e7a-154">Až budete mít ITSM připojení vytvořit, můžete vytvořit pracovní položky (položek) v nástroji vaší ITSM podle Azure výstrahy, pomocí **ITSM akce** v **skupiny akcí**.</span><span class="sxs-lookup"><span data-stu-id="66e7a-154">Once you have your ITSM connection created, you can create work item(s) in your ITSM tool based on Azure alerts, by using the **ITSM Action** in **Action Groups**.</span></span>

<span data-ttu-id="66e7a-155">Akce skupiny poskytují modulární a opakovaně použitelné způsob spouštění akcí pro upozornění Azure.</span><span class="sxs-lookup"><span data-stu-id="66e7a-155">Action Groups provide a modular and reusable way of triggering actions for your Azure Alerts.</span></span> <span data-ttu-id="66e7a-156">Můžete vytvořit skupiny akcí s metriky výstrahy, protokol aktivit výstrahy a upozornění Azure Log Analytics na portálu Azure.</span><span class="sxs-lookup"><span data-stu-id="66e7a-156">You can use Action Groups with metric alerts, Activity Log alerts and Azure Log Analytics alerts in Azure portal.</span></span>

<span data-ttu-id="66e7a-157">Použijte následující postup:</span><span class="sxs-lookup"><span data-stu-id="66e7a-157">Use the following procedure:</span></span>

1. <span data-ttu-id="66e7a-158">Na portálu Azure, klikněte na tlačítko **monitorování**.</span><span class="sxs-lookup"><span data-stu-id="66e7a-158">In Azure portal, click  **Monitor**.</span></span>
2. <span data-ttu-id="66e7a-159">V levém podokně klikněte na **skupiny akcí**.</span><span class="sxs-lookup"><span data-stu-id="66e7a-159">In the left pane, click  **Action groups**.</span></span> <span data-ttu-id="66e7a-160">**Přidat skupinu akce** se zobrazí v okně.</span><span class="sxs-lookup"><span data-stu-id="66e7a-160">The **Add action group** window appears.</span></span>

    ![Skupiny akcí](media/log-analytics-itsmc/action-groups.png)

3. <span data-ttu-id="66e7a-162">Zadejte **název** a **ShortName** pro skupinu pro akce.</span><span class="sxs-lookup"><span data-stu-id="66e7a-162">Provide **Name** and **ShortName** for your action group.</span></span> <span data-ttu-id="66e7a-163">Vyberte **skupiny prostředků** a **předplatné** kde chcete vytvořit skupině Akce.</span><span class="sxs-lookup"><span data-stu-id="66e7a-163">Select the **Resource Group** and **Subscription** where you want to create your action group.</span></span>

    ![Podrobnosti skupiny akce](media/log-analytics-itsmc/action-groups-details.png)

4. <span data-ttu-id="66e7a-165">Vyberte v seznamu akcí **ITSM** z rozevírací nabídky pro **typ akce**.</span><span class="sxs-lookup"><span data-stu-id="66e7a-165">In the Actions list, select **ITSM** from the drop-down menu for **Action Type**.</span></span> <span data-ttu-id="66e7a-166">Zadejte **název** pro akci a klikněte na tlačítko **upravit podrobnosti**.</span><span class="sxs-lookup"><span data-stu-id="66e7a-166">Provide a **Name** for the action and click **Edit details**.</span></span>
5. <span data-ttu-id="66e7a-167">Vyberte **předplatné** kde je umístěn pracovní prostor analýzy protokolů.</span><span class="sxs-lookup"><span data-stu-id="66e7a-167">Select the **Subscription** where your Log Analytics workspace is located.</span></span> <span data-ttu-id="66e7a-168">Vyberte **připojení** name (název vašeho konektoru ITSM), za nímž následuje název pracovního prostoru.</span><span class="sxs-lookup"><span data-stu-id="66e7a-168">Select the **Connection** name (your ITSM Connector name) followed by your Workspace name.</span></span> <span data-ttu-id="66e7a-169">Například "MyITSMMConnector(MyWorkspace)".</span><span class="sxs-lookup"><span data-stu-id="66e7a-169">For example, "MyITSMMConnector(MyWorkspace)."</span></span>

    ![Podrobnosti o ITSM akce](./media/log-analytics-itsmc/itsm-action-details.png)

6. <span data-ttu-id="66e7a-171">Vyberte **pracovní položka** typu z rozevírací nabídky.</span><span class="sxs-lookup"><span data-stu-id="66e7a-171">Select **Work Item** type from the drop-down menu.</span></span>
   <span data-ttu-id="66e7a-172">Vyberte existující šablony nebo vyplnit pole, která vyžaduje vaše ITSM produktu.</span><span class="sxs-lookup"><span data-stu-id="66e7a-172">Choose to use an existing template or fill the fields required by your ITSM product.</span></span>
7. <span data-ttu-id="66e7a-173">Klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="66e7a-173">Click **OK**.</span></span>

<span data-ttu-id="66e7a-174">Při vytváření nebo úpravách Azure pravidla výstrahy, použijte skupinu akce, který má ITSM akce.</span><span class="sxs-lookup"><span data-stu-id="66e7a-174">When creating/editing an Azure alert rule, use an Action group, which has an ITSM Action.</span></span> <span data-ttu-id="66e7a-175">Když se aktivuje výstraha, pracovní položky je vytvořit nebo aktualizovat v nástroj ITSM.</span><span class="sxs-lookup"><span data-stu-id="66e7a-175">When the alert triggers, work item is created/updated in the ITSM tool.</span></span>

>[!NOTE]

> <span data-ttu-id="66e7a-176">Informace o cenách ITSM akce najdete v tématu [stránce s cenami](https://azure.microsoft.com/pricing/details/monitor/) pro akce skupiny.</span><span class="sxs-lookup"><span data-stu-id="66e7a-176">For information on pricing of ITSM Action, see the [pricing page](https://azure.microsoft.com/pricing/details/monitor/) for Action Groups.</span></span>


## <a name="create-itsm-work-items-from-log-analytics-alerts"></a><span data-ttu-id="66e7a-177">Vytváření pracovních položek ITSM z výstrah analýzy protokolů</span><span class="sxs-lookup"><span data-stu-id="66e7a-177">Create ITSM work items from Log Analytics alerts</span></span>

<span data-ttu-id="66e7a-178">Pravidla výstrah můžete nakonfigurovat na portálu Azure Log Analytics k vytváření pracovních položek v nástroji ITSM, pomocí následujícího postupu.</span><span class="sxs-lookup"><span data-stu-id="66e7a-178">You can configure alert rules in Azure Log Analytics portal to create work items in ITSM tool, using the following procedure.</span></span>

1. <span data-ttu-id="66e7a-179">Z **hledání protokolů** okně Spustit protokolu vyhledávací dotaz. Chcete-li zobrazit data.</span><span class="sxs-lookup"><span data-stu-id="66e7a-179">From **Log Search** window, run a log search query to view data.</span></span> <span data-ttu-id="66e7a-180">Výsledky dotazu jsou zdroj pro pracovní položky.</span><span class="sxs-lookup"><span data-stu-id="66e7a-180">Query results are the source for work items.</span></span>
2. <span data-ttu-id="66e7a-181">V **hledání protokolů**, klikněte na tlačítko **výstrahy** otevřete **přidat pravidlo výstrahy** stránky.</span><span class="sxs-lookup"><span data-stu-id="66e7a-181">In **Log Search**, click **Alert** to open the **Add Alert Rule** page.</span></span>

    ![Obrazovka analýzy protokolů](./media/log-analytics-itsmc/itsmc-work-items-for-azure-alerts.png)

3. <span data-ttu-id="66e7a-183">Na **přidat pravidlo výstrahy** okno, zadejte požadované podrobnosti pro **název**, **závažnost**, **vyhledávací dotaz**, a **výstrah kritéria** (časová okna/metrika měří období).</span><span class="sxs-lookup"><span data-stu-id="66e7a-183">On the **Add Alert Rule** window, provide the required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="66e7a-184">Vyberte **Ano** pro **ITSM akce**.</span><span class="sxs-lookup"><span data-stu-id="66e7a-184">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="66e7a-185">Vyberte ITSM připojení z **vyberte připojení** seznamu.</span><span class="sxs-lookup"><span data-stu-id="66e7a-185">Select your ITSM connection from the **Select Connection** list.</span></span>
6. <span data-ttu-id="66e7a-186">Zadejte podrobnosti podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="66e7a-186">Provide the details as required.</span></span>
7. <span data-ttu-id="66e7a-187">Vytvořit samostatný pracovní položku pro každé položky protokolu této výstrahy, vyberte **vytvořit jednotlivé pracovní položky pro každý záznam protokolu** zaškrtávací políčko.</span><span class="sxs-lookup"><span data-stu-id="66e7a-187">To create a separate work item for each log entry of this alert, select the **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="66e7a-188">Nebo</span><span class="sxs-lookup"><span data-stu-id="66e7a-188">Or</span></span>

    <span data-ttu-id="66e7a-189">nechte toto políčko Zrušit vytvořit pouze jeden pracovní položku pro libovolný počet záznamů protokolu v rámci této výstrahy.</span><span class="sxs-lookup"><span data-stu-id="66e7a-189">leave this checkbox unselected to create only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="66e7a-190">Klikněte na **Uložit**.</span><span class="sxs-lookup"><span data-stu-id="66e7a-190">Click **Save**.</span></span>

<span data-ttu-id="66e7a-191">Můžete zobrazit výstrahy analýzy protokolů, který jste vytvořili v části **Nastavení > výstrahy**.</span><span class="sxs-lookup"><span data-stu-id="66e7a-191">You can view the  Log Analytics alert that you created under **Settings>Alerts**.</span></span> <span data-ttu-id="66e7a-192">Pracovní položky odpovídající ITSM připojení vytvářejí, když je splněna podmínka zadaný výstrahy.</span><span class="sxs-lookup"><span data-stu-id="66e7a-192">The corresponding ITSM connection's work items are created when the specified alert's condition is met.</span></span>


## <a name="create-itsm-work-items-from-log-analytics-log-records"></a><span data-ttu-id="66e7a-193">Vytváření pracovních položek ITSM ze záznamů protokolu analýzy protokolů</span><span class="sxs-lookup"><span data-stu-id="66e7a-193">Create ITSM work items from Log Analytics log records</span></span>

<span data-ttu-id="66e7a-194">Můžete také vytvořit pracovní položky v připojených zdrojů ITSM přímo z záznam protokolu.</span><span class="sxs-lookup"><span data-stu-id="66e7a-194">You can also create work items in the connected ITSM sources directly from a log record.</span></span> <span data-ttu-id="66e7a-195">To slouží k otestování, pokud připojení funguje správně.</span><span class="sxs-lookup"><span data-stu-id="66e7a-195">This can be used to test if the connection is working properly.</span></span>


1. <span data-ttu-id="66e7a-196">Z **hledání protokolů**hledání požadovaných dat, vyberte podrobností a klikněte na tlačítko **vytvořit pracovní položka**.</span><span class="sxs-lookup"><span data-stu-id="66e7a-196">From **Log Search**,  search the required data, select the detail, and click **Create work item**.</span></span>

    <span data-ttu-id="66e7a-197">**Vytvoření pracovní položky ITSM** zobrazí se okno:</span><span class="sxs-lookup"><span data-stu-id="66e7a-197">The **Create ITSM Work Item** window appears:</span></span>

    ![Obrazovka analýzy protokolů](media/log-analytics-itsmc/itsmc-work-items-from-azure-logs.png)

2.   <span data-ttu-id="66e7a-199">Přidejte následující podrobnosti:</span><span class="sxs-lookup"><span data-stu-id="66e7a-199">Add the following details:</span></span>

  - <span data-ttu-id="66e7a-200">**Název pracovní položky**: název pro pracovní položku.</span><span class="sxs-lookup"><span data-stu-id="66e7a-200">**Work item Title**: Title for the work item.</span></span>
  - <span data-ttu-id="66e7a-201">**Pracovní položky Popis**: popis novou pracovní položku.</span><span class="sxs-lookup"><span data-stu-id="66e7a-201">**Work item Description**: Description for the new work item.</span></span>
  - <span data-ttu-id="66e7a-202">**Vliv na počítače**: název počítače, kde tato data protokolu byla nalezena.</span><span class="sxs-lookup"><span data-stu-id="66e7a-202">**Affected Computer**: Name of the computer where this log data was found.</span></span>
  - <span data-ttu-id="66e7a-203">**Vyberte připojení**: ITSM připojení, ve kterém chcete vytvořit tuto pracovní položku.</span><span class="sxs-lookup"><span data-stu-id="66e7a-203">**Select Connection**:  ITSM connection in which you want to create this work item.</span></span>
  - <span data-ttu-id="66e7a-204">**Pracovní položka**: typ pracovní položky.</span><span class="sxs-lookup"><span data-stu-id="66e7a-204">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="66e7a-205">Chcete-li použít existující šablonu pracovní položky pro incidentu, klikněte na tlačítko **Ano** pod **generovat pracovní položka založený na šabloně** a potom klikněte na **vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="66e7a-205">To use an existing work item template for an incident, click **Yes** under **Generate Work item based on Template** option and then click **Create**.</span></span>

    <span data-ttu-id="66e7a-206">Nebo:</span><span class="sxs-lookup"><span data-stu-id="66e7a-206">Or,</span></span>

    <span data-ttu-id="66e7a-207">Klikněte na tlačítko **ne** Pokud chcete zadat vlastní hodnoty.</span><span class="sxs-lookup"><span data-stu-id="66e7a-207">Click **No** if you want to provide your customized values.</span></span>

4. <span data-ttu-id="66e7a-208">Zadejte odpovídající hodnoty v **typu Kontakt**, **dopad**, **naléhavost**, **kategorie**, a **dílčí kategorie** textová pole a pak klikněte na tlačítko **vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="66e7a-208">Provide the appropriate values in the **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>


## <a name="visualize-and-analyze-the-incident-and-change-request-data"></a><span data-ttu-id="66e7a-209">Vizualizace a analyzovat incidentu a změnit data požadavku</span><span class="sxs-lookup"><span data-stu-id="66e7a-209">Visualize and analyze the incident and change request data</span></span>

<span data-ttu-id="66e7a-210">V závislosti na vaší konfiguraci při nastavování připojení ITSM konektor synchronizovat až 120 dní incidentů a změn dat požadavku.</span><span class="sxs-lookup"><span data-stu-id="66e7a-210">Based on your configuration when setting up a connection, ITSM connector can sync up to 120 days of Incident and Change request data.</span></span> <span data-ttu-id="66e7a-211">Je součástí schéma záznam protokolu pro tato data [další části](#additional-information).</span><span class="sxs-lookup"><span data-stu-id="66e7a-211">The log record schema for this data is provided in the [next section](#additional-information).</span></span>

<span data-ttu-id="66e7a-212">Pomocí řídicího panelu ITSM konektor v řešení můžete vizualizovat data požadavku incidentů a změn.</span><span class="sxs-lookup"><span data-stu-id="66e7a-212">The incident and change request data can be visualized using the ITSM Connector dashboard in the solution.</span></span>

![Obrazovka analýzy protokolů](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

<span data-ttu-id="66e7a-214">Řídicí panel obsahuje také informace o stav konektoru, který můžete použít jako východisko analyzovat problémy s připojení.</span><span class="sxs-lookup"><span data-stu-id="66e7a-214">The dashboard also provides information on connector status which can be used as a starting point to analyze any issues with the connections.</span></span>

<span data-ttu-id="66e7a-215">Také můžete vizualizovat incidenty synchronizovat proti ovlivněné počítače, v rámci řešení mapy služeb.</span><span class="sxs-lookup"><span data-stu-id="66e7a-215">You can also visualize the incidents synced against the impacted computers, within the Service Map solution.</span></span>

<span data-ttu-id="66e7a-216">Mapa služeb automaticky vyhledá součásti aplikace v systémech Windows a Linux a mapuje komunikace mezi službami.</span><span class="sxs-lookup"><span data-stu-id="66e7a-216">Service Map automatically discovers the application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="66e7a-217">Umožňuje zobrazit vaše servery co možná z nich – jako vzájemně propojena systémy, které doručují důležité služby.</span><span class="sxs-lookup"><span data-stu-id="66e7a-217">It allows you to view your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="66e7a-218">Mapy služeb zobrazí připojení mezi servery, procesy, a vyžaduje porty mezi žádné připojení TCP architektura žádnou konfiguraci, jiné než instalace agenta.</span><span class="sxs-lookup"><span data-stu-id="66e7a-218">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="66e7a-219">[Další informace](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="66e7a-219">[Learn more](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="66e7a-220">Pokud používáte řešení mapy služeb, můžete zobrazit položky služby podpory, které jsou vytvořené v ITSM řešení, jak je znázorněno v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="66e7a-220">If you are using the Service Map solution, you can view the service desk items created in the ITSM solutions as shown in the following example:</span></span>

![Obrazovka analýzy protokolů](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)

<span data-ttu-id="66e7a-222">Další informace: [mapy služeb](../operations-management-suite/operations-management-suite-service-map.md)</span><span class="sxs-lookup"><span data-stu-id="66e7a-222">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md)</span></span>


## <a name="additional-information"></a><span data-ttu-id="66e7a-223">Další informace</span><span class="sxs-lookup"><span data-stu-id="66e7a-223">Additional information</span></span>

### <a name="data-synced-from-itsm-product"></a><span data-ttu-id="66e7a-224">Synchronizované z produktu ITSM dat</span><span class="sxs-lookup"><span data-stu-id="66e7a-224">Data synced from ITSM product</span></span>
<span data-ttu-id="66e7a-225">Incidenty a žádosti o změnu jsou synchronizované z vašeho produktu ITSM do pracovního prostoru analýzy protokolů na základě konfigurace připojení.</span><span class="sxs-lookup"><span data-stu-id="66e7a-225">Incidents and change requests are synced from your ITSM product to your Log Analytics workspace based on the connection's configuration.</span></span>

<span data-ttu-id="66e7a-226">Tyto informace jsou uvedeny příklady podle dat shromažďovaných funkcí ITSMC:</span><span class="sxs-lookup"><span data-stu-id="66e7a-226">The following information shows examples of data gathered by ITSMC:</span></span>

> [!NOTE]

> <span data-ttu-id="66e7a-227">V závislosti na typu pracovní položky naimportovat do analýzy protokolů **ServiceDesk_CL** obsahuje následující pole:</span><span class="sxs-lookup"><span data-stu-id="66e7a-227">Depending on the work item type imported into Log Analytics, **ServiceDesk_CL** contains the following fields:</span></span>

<span data-ttu-id="66e7a-228">**Pracovní položka:** **incidenty**</span><span class="sxs-lookup"><span data-stu-id="66e7a-228">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="66e7a-229">ServiceDeskWorkItemType_s="Incident"</span><span class="sxs-lookup"><span data-stu-id="66e7a-229">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="66e7a-230">**Pole**</span><span class="sxs-lookup"><span data-stu-id="66e7a-230">**Fields**</span></span>

- <span data-ttu-id="66e7a-231">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="66e7a-231">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="66e7a-232">ID služby podpory</span><span class="sxs-lookup"><span data-stu-id="66e7a-232">Service Desk ID</span></span>
- <span data-ttu-id="66e7a-233">Stav</span><span class="sxs-lookup"><span data-stu-id="66e7a-233">State</span></span>
- <span data-ttu-id="66e7a-234">Naléhavosti</span><span class="sxs-lookup"><span data-stu-id="66e7a-234">Urgency</span></span>
- <span data-ttu-id="66e7a-235">Dopad</span><span class="sxs-lookup"><span data-stu-id="66e7a-235">Impact</span></span>
- <span data-ttu-id="66e7a-236">Priorita</span><span class="sxs-lookup"><span data-stu-id="66e7a-236">Priority</span></span>
- <span data-ttu-id="66e7a-237">Eskalace</span><span class="sxs-lookup"><span data-stu-id="66e7a-237">Escalation</span></span>
- <span data-ttu-id="66e7a-238">Vytvořil(a)</span><span class="sxs-lookup"><span data-stu-id="66e7a-238">Created By</span></span>
- <span data-ttu-id="66e7a-239">Vyřešil</span><span class="sxs-lookup"><span data-stu-id="66e7a-239">Resolved By</span></span>
- <span data-ttu-id="66e7a-240">Uzavřené</span><span class="sxs-lookup"><span data-stu-id="66e7a-240">Closed By</span></span>
- <span data-ttu-id="66e7a-241">Zdroj</span><span class="sxs-lookup"><span data-stu-id="66e7a-241">Source</span></span>
- <span data-ttu-id="66e7a-242">Přiřazené k</span><span class="sxs-lookup"><span data-stu-id="66e7a-242">Assigned To</span></span>
- <span data-ttu-id="66e7a-243">Kategorie</span><span class="sxs-lookup"><span data-stu-id="66e7a-243">Category</span></span>
- <span data-ttu-id="66e7a-244">Nadpis</span><span class="sxs-lookup"><span data-stu-id="66e7a-244">Title</span></span>
- <span data-ttu-id="66e7a-245">Popis</span><span class="sxs-lookup"><span data-stu-id="66e7a-245">Description</span></span>
- <span data-ttu-id="66e7a-246">Datum vytvoření</span><span class="sxs-lookup"><span data-stu-id="66e7a-246">Created Date</span></span>
- <span data-ttu-id="66e7a-247">Datum uzavření</span><span class="sxs-lookup"><span data-stu-id="66e7a-247">Closed Date</span></span>
- <span data-ttu-id="66e7a-248">Datum vyřešení</span><span class="sxs-lookup"><span data-stu-id="66e7a-248">Resolved Date</span></span>
- <span data-ttu-id="66e7a-249">Datum poslední změny</span><span class="sxs-lookup"><span data-stu-id="66e7a-249">Last Modified Date</span></span>
- <span data-ttu-id="66e7a-250">Počítač</span><span class="sxs-lookup"><span data-stu-id="66e7a-250">Computer</span></span>


<span data-ttu-id="66e7a-251">**Pracovní položka:** **žádosti o změnu**</span><span class="sxs-lookup"><span data-stu-id="66e7a-251">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="66e7a-252">ServiceDeskWorkItemType_s="ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="66e7a-252">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="66e7a-253">**Pole**</span><span class="sxs-lookup"><span data-stu-id="66e7a-253">**Fields**</span></span>
- <span data-ttu-id="66e7a-254">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="66e7a-254">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="66e7a-255">ID služby podpory</span><span class="sxs-lookup"><span data-stu-id="66e7a-255">Service Desk ID</span></span>
- <span data-ttu-id="66e7a-256">Vytvořil(a)</span><span class="sxs-lookup"><span data-stu-id="66e7a-256">Created By</span></span>
- <span data-ttu-id="66e7a-257">Uzavřené</span><span class="sxs-lookup"><span data-stu-id="66e7a-257">Closed By</span></span>
- <span data-ttu-id="66e7a-258">Zdroj</span><span class="sxs-lookup"><span data-stu-id="66e7a-258">Source</span></span>
- <span data-ttu-id="66e7a-259">Přiřazené k</span><span class="sxs-lookup"><span data-stu-id="66e7a-259">Assigned To</span></span>
- <span data-ttu-id="66e7a-260">Nadpis</span><span class="sxs-lookup"><span data-stu-id="66e7a-260">Title</span></span>
- <span data-ttu-id="66e7a-261">Typ</span><span class="sxs-lookup"><span data-stu-id="66e7a-261">Type</span></span>
- <span data-ttu-id="66e7a-262">Kategorie</span><span class="sxs-lookup"><span data-stu-id="66e7a-262">Category</span></span>
- <span data-ttu-id="66e7a-263">Stav</span><span class="sxs-lookup"><span data-stu-id="66e7a-263">State</span></span>
- <span data-ttu-id="66e7a-264">Eskalace</span><span class="sxs-lookup"><span data-stu-id="66e7a-264">Escalation</span></span>
- <span data-ttu-id="66e7a-265">Konflikt stavu</span><span class="sxs-lookup"><span data-stu-id="66e7a-265">Conflict Status</span></span>
- <span data-ttu-id="66e7a-266">Naléhavosti</span><span class="sxs-lookup"><span data-stu-id="66e7a-266">Urgency</span></span>
- <span data-ttu-id="66e7a-267">Priorita</span><span class="sxs-lookup"><span data-stu-id="66e7a-267">Priority</span></span>
- <span data-ttu-id="66e7a-268">Riziko</span><span class="sxs-lookup"><span data-stu-id="66e7a-268">Risk</span></span>
- <span data-ttu-id="66e7a-269">Dopad</span><span class="sxs-lookup"><span data-stu-id="66e7a-269">Impact</span></span>
- <span data-ttu-id="66e7a-270">Přiřazené k</span><span class="sxs-lookup"><span data-stu-id="66e7a-270">Assigned To</span></span>
- <span data-ttu-id="66e7a-271">Datum vytvoření</span><span class="sxs-lookup"><span data-stu-id="66e7a-271">Created Date</span></span>
- <span data-ttu-id="66e7a-272">Datum uzavření</span><span class="sxs-lookup"><span data-stu-id="66e7a-272">Closed Date</span></span>
- <span data-ttu-id="66e7a-273">Datum poslední změny</span><span class="sxs-lookup"><span data-stu-id="66e7a-273">Last Modified Date</span></span>
- <span data-ttu-id="66e7a-274">Požadovaná data</span><span class="sxs-lookup"><span data-stu-id="66e7a-274">Requested Date</span></span>
- <span data-ttu-id="66e7a-275">Plánované počáteční datum</span><span class="sxs-lookup"><span data-stu-id="66e7a-275">Planned Start Date</span></span>
- <span data-ttu-id="66e7a-276">Naplánované koncové datum</span><span class="sxs-lookup"><span data-stu-id="66e7a-276">Planned End Date</span></span>
- <span data-ttu-id="66e7a-277">Pracovní počáteční datum</span><span class="sxs-lookup"><span data-stu-id="66e7a-277">Work Start Date</span></span>
- <span data-ttu-id="66e7a-278">Pracovní koncové datum</span><span class="sxs-lookup"><span data-stu-id="66e7a-278">Work End Date</span></span>
- <span data-ttu-id="66e7a-279">Popis</span><span class="sxs-lookup"><span data-stu-id="66e7a-279">Description</span></span>
- <span data-ttu-id="66e7a-280">Počítač</span><span class="sxs-lookup"><span data-stu-id="66e7a-280">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="66e7a-281">Výstupní data pro ServiceNow incident</span><span class="sxs-lookup"><span data-stu-id="66e7a-281">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="66e7a-282">Pole analýzy protokolů</span><span class="sxs-lookup"><span data-stu-id="66e7a-282">Log Analytics field</span></span> | <span data-ttu-id="66e7a-283">ServiceNow pole</span><span class="sxs-lookup"><span data-stu-id="66e7a-283">ServiceNow field</span></span> |
|:--- |:--- |
| <span data-ttu-id="66e7a-284">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-284">ServiceDeskId_s</span></span>| <span data-ttu-id="66e7a-285">Číslo</span><span class="sxs-lookup"><span data-stu-id="66e7a-285">Number</span></span> |
| <span data-ttu-id="66e7a-286">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-286">IncidentState_s</span></span> | <span data-ttu-id="66e7a-287">Stav</span><span class="sxs-lookup"><span data-stu-id="66e7a-287">State</span></span> |
| <span data-ttu-id="66e7a-288">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-288">Urgency_s</span></span> |<span data-ttu-id="66e7a-289">Naléhavosti</span><span class="sxs-lookup"><span data-stu-id="66e7a-289">Urgency</span></span> |
| <span data-ttu-id="66e7a-290">Impact_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-290">Impact_s</span></span> |<span data-ttu-id="66e7a-291">Dopad</span><span class="sxs-lookup"><span data-stu-id="66e7a-291">Impact</span></span>|
| <span data-ttu-id="66e7a-292">Priority_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-292">Priority_s</span></span> | <span data-ttu-id="66e7a-293">Priorita</span><span class="sxs-lookup"><span data-stu-id="66e7a-293">Priority</span></span> |
| <span data-ttu-id="66e7a-294">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-294">CreatedBy_s</span></span> | <span data-ttu-id="66e7a-295">Otevřít</span><span class="sxs-lookup"><span data-stu-id="66e7a-295">Opened by</span></span> |
| <span data-ttu-id="66e7a-296">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-296">ResolvedBy_s</span></span> | <span data-ttu-id="66e7a-297">Vyřešil(a)</span><span class="sxs-lookup"><span data-stu-id="66e7a-297">Resolved by</span></span>|
| <span data-ttu-id="66e7a-298">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-298">ClosedBy_s</span></span>  | <span data-ttu-id="66e7a-299">Uzavřené</span><span class="sxs-lookup"><span data-stu-id="66e7a-299">Closed by</span></span> |
| <span data-ttu-id="66e7a-300">Source_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-300">Source_s</span></span>| <span data-ttu-id="66e7a-301">Obraťte se na typ</span><span class="sxs-lookup"><span data-stu-id="66e7a-301">Contact type</span></span> |
| <span data-ttu-id="66e7a-302">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-302">AssignedTo_s</span></span> | <span data-ttu-id="66e7a-303">Přiřazeno</span><span class="sxs-lookup"><span data-stu-id="66e7a-303">Assigned to</span></span>  |
| <span data-ttu-id="66e7a-304">Category_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-304">Category_s</span></span> | <span data-ttu-id="66e7a-305">Kategorie</span><span class="sxs-lookup"><span data-stu-id="66e7a-305">Category</span></span> |
| <span data-ttu-id="66e7a-306">Title_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-306">Title_s</span></span>|  <span data-ttu-id="66e7a-307">Krátký popis</span><span class="sxs-lookup"><span data-stu-id="66e7a-307">Short description</span></span> |
| <span data-ttu-id="66e7a-308">Description_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-308">Description_s</span></span>|  <span data-ttu-id="66e7a-309">Poznámky</span><span class="sxs-lookup"><span data-stu-id="66e7a-309">Notes</span></span> |
| <span data-ttu-id="66e7a-310">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="66e7a-310">CreatedDate_t</span></span>|  <span data-ttu-id="66e7a-311">Opened</span><span class="sxs-lookup"><span data-stu-id="66e7a-311">Opened</span></span> |
| <span data-ttu-id="66e7a-312">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="66e7a-312">ClosedDate_t</span></span>| <span data-ttu-id="66e7a-313">zavřené</span><span class="sxs-lookup"><span data-stu-id="66e7a-313">closed</span></span>|
| <span data-ttu-id="66e7a-314">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="66e7a-314">ResolvedDate_t</span></span>|<span data-ttu-id="66e7a-315">Vyřešené</span><span class="sxs-lookup"><span data-stu-id="66e7a-315">Resolved</span></span>|
| <span data-ttu-id="66e7a-316">Počítač</span><span class="sxs-lookup"><span data-stu-id="66e7a-316">Computer</span></span>  | <span data-ttu-id="66e7a-317">položky konfigurace</span><span class="sxs-lookup"><span data-stu-id="66e7a-317">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="66e7a-318">Výstupní data pro ServiceNow žádost o změnu</span><span class="sxs-lookup"><span data-stu-id="66e7a-318">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="66e7a-319">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="66e7a-319">Log Analytics</span></span> | <span data-ttu-id="66e7a-320">ServieNow pole</span><span class="sxs-lookup"><span data-stu-id="66e7a-320">ServieNow field</span></span> |
|:--- |:--- |
| <span data-ttu-id="66e7a-321">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-321">ServiceDeskId_s</span></span>| <span data-ttu-id="66e7a-322">Číslo</span><span class="sxs-lookup"><span data-stu-id="66e7a-322">Number</span></span> |
| <span data-ttu-id="66e7a-323">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-323">CreatedBy_s</span></span> | <span data-ttu-id="66e7a-324">Žadatel</span><span class="sxs-lookup"><span data-stu-id="66e7a-324">Requested by</span></span> |
| <span data-ttu-id="66e7a-325">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-325">ClosedBy_s</span></span> | <span data-ttu-id="66e7a-326">Uzavřené</span><span class="sxs-lookup"><span data-stu-id="66e7a-326">Closed by</span></span> |
| <span data-ttu-id="66e7a-327">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-327">AssignedTo_s</span></span> | <span data-ttu-id="66e7a-328">Přiřazeno</span><span class="sxs-lookup"><span data-stu-id="66e7a-328">Assigned to</span></span>  |
| <span data-ttu-id="66e7a-329">Title_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-329">Title_s</span></span>|  <span data-ttu-id="66e7a-330">Krátký popis</span><span class="sxs-lookup"><span data-stu-id="66e7a-330">Short description</span></span> |
| <span data-ttu-id="66e7a-331">Type_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-331">Type_s</span></span>|  <span data-ttu-id="66e7a-332">Typ</span><span class="sxs-lookup"><span data-stu-id="66e7a-332">Type</span></span> |
| <span data-ttu-id="66e7a-333">Category_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-333">Category_s</span></span>|  <span data-ttu-id="66e7a-334">Kategorie</span><span class="sxs-lookup"><span data-stu-id="66e7a-334">Category</span></span> |
| <span data-ttu-id="66e7a-335">CRState_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-335">CRState_s</span></span>|  <span data-ttu-id="66e7a-336">Stav</span><span class="sxs-lookup"><span data-stu-id="66e7a-336">State</span></span>|
| <span data-ttu-id="66e7a-337">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-337">Urgency_s</span></span>|  <span data-ttu-id="66e7a-338">Naléhavosti</span><span class="sxs-lookup"><span data-stu-id="66e7a-338">Urgency</span></span> |
| <span data-ttu-id="66e7a-339">Priority_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-339">Priority_s</span></span>| <span data-ttu-id="66e7a-340">Priorita</span><span class="sxs-lookup"><span data-stu-id="66e7a-340">Priority</span></span>|
| <span data-ttu-id="66e7a-341">Risk_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-341">Risk_s</span></span>| <span data-ttu-id="66e7a-342">Riziko</span><span class="sxs-lookup"><span data-stu-id="66e7a-342">Risk</span></span>|
| <span data-ttu-id="66e7a-343">Impact_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-343">Impact_s</span></span>| <span data-ttu-id="66e7a-344">Dopad</span><span class="sxs-lookup"><span data-stu-id="66e7a-344">Impact</span></span>|
| <span data-ttu-id="66e7a-345">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="66e7a-345">RequestedDate_t</span></span>  | <span data-ttu-id="66e7a-346">Požadovaná data</span><span class="sxs-lookup"><span data-stu-id="66e7a-346">Requested by date</span></span> |
| <span data-ttu-id="66e7a-347">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="66e7a-347">ClosedDate_t</span></span> | <span data-ttu-id="66e7a-348">Datum uzavření</span><span class="sxs-lookup"><span data-stu-id="66e7a-348">Closed date</span></span> |
| <span data-ttu-id="66e7a-349">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="66e7a-349">PlannedStartDate_t</span></span>  |     <span data-ttu-id="66e7a-350">Plánované počáteční datum</span><span class="sxs-lookup"><span data-stu-id="66e7a-350">Planned start date</span></span> |
| <span data-ttu-id="66e7a-351">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="66e7a-351">PlannedEndDate_t</span></span>  |   <span data-ttu-id="66e7a-352">Plánované koncové datum</span><span class="sxs-lookup"><span data-stu-id="66e7a-352">Planned end date</span></span> |
| <span data-ttu-id="66e7a-353">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="66e7a-353">WorkStartDate_t</span></span>  | <span data-ttu-id="66e7a-354">Skutečné počáteční datum</span><span class="sxs-lookup"><span data-stu-id="66e7a-354">Actual start date</span></span> |
| <span data-ttu-id="66e7a-355">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="66e7a-355">WorkEndDate_t</span></span> | <span data-ttu-id="66e7a-356">Skutečné koncové datum</span><span class="sxs-lookup"><span data-stu-id="66e7a-356">Actual end date</span></span>|
| <span data-ttu-id="66e7a-357">Description_s</span><span class="sxs-lookup"><span data-stu-id="66e7a-357">Description_s</span></span> | <span data-ttu-id="66e7a-358">Popis</span><span class="sxs-lookup"><span data-stu-id="66e7a-358">Description</span></span> |
| <span data-ttu-id="66e7a-359">Počítač</span><span class="sxs-lookup"><span data-stu-id="66e7a-359">Computer</span></span>  | <span data-ttu-id="66e7a-360">Položky konfigurace</span><span class="sxs-lookup"><span data-stu-id="66e7a-360">Configuration Item</span></span> |


## <a name="troubleshoot-itsm-connections"></a><span data-ttu-id="66e7a-361">Řešení potíží s ITSM připojení</span><span class="sxs-lookup"><span data-stu-id="66e7a-361">Troubleshoot ITSM connections</span></span>
1.  <span data-ttu-id="66e7a-362">Pokud připojení selže z uživatelského rozhraní připojené zdroje s **Chyba při ukládání připojení** zpráva, proveďte následující kroky:</span><span class="sxs-lookup"><span data-stu-id="66e7a-362">If connection fails from connected source's UI with an **Error in saving connection** message, take the following steps:</span></span>
- <span data-ttu-id="66e7a-363">Pro připojení ServiceNow, Cherwell a Provance</span><span class="sxs-lookup"><span data-stu-id="66e7a-363">For ServiceNow, Cherwell and Provance connections,</span></span>  
           <span data-ttu-id="66e7a-364"> -   Zkontrolujte správně zadali uživatelské jméno, heslo, ID klienta a tajný klíč klienta pro jednotlivá připojení.</span><span class="sxs-lookup"><span data-stu-id="66e7a-364">- ensure you correctly entered  the username, password, client ID, and client secret  for each of the connections.</span></span>  
           <span data-ttu-id="66e7a-365"> -   Zkontrolujte, pokud máte dostatečná oprávnění v rámci odpovídající ITSM produktu pro připojení.</span><span class="sxs-lookup"><span data-stu-id="66e7a-365">- check if you have sufficient privileges in the corresponding ITSM product to make the connection.</span></span>  
- <span data-ttu-id="66e7a-366">U připojení k portálu Service Manager</span><span class="sxs-lookup"><span data-stu-id="66e7a-366">For Service Manager connections,</span></span>  
           <span data-ttu-id="66e7a-367">- Zajistěte, aby webová aplikace je úspěšně nasazen a hybridní připojení se vytvoří.</span><span class="sxs-lookup"><span data-stu-id="66e7a-367">- ensure that the Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="66e7a-368">Ověřte připojení se úspěšně naváže na místní počítač portálu Service Manager, najdete na adresu URL webové aplikace podle popisu v dokumentaci k provádění [hybridní připojení](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="66e7a-368">To verify the connection is successfully established with the on-prem Service Manager machine, visit the  Web app URL as detailed in the documentation for making the [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>  

2.  <span data-ttu-id="66e7a-369">Pokud není získávání synchronizovat data z ServiceNow k analýze protokolů, zajistěte, aby ServiceNow instance není pozastaveno.</span><span class="sxs-lookup"><span data-stu-id="66e7a-369">If data from ServiceNow is not getting synced to Log Analytics, ensure that the ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="66e7a-370">Instance ServiceNow Dev někdy přejděte do režimu spánku při nečinnosti, po dlouhou dobu.</span><span class="sxs-lookup"><span data-stu-id="66e7a-370">ServiceNow Dev Instances sometimes go to sleep when idle for a long period.</span></span> <span data-ttu-id="66e7a-371">Jinak ohlaste daný problém.</span><span class="sxs-lookup"><span data-stu-id="66e7a-371">Else, report the issue.</span></span>
3.  <span data-ttu-id="66e7a-372">Pokud OMS výstrahy fire, ale pracovní položky nejsou vytvořeny v produktu ITSM nebo položek konfigurace nejsou vytvořen nebo propojené pracovní položky nebo další obecné informace, podívejte se na těchto místech:</span><span class="sxs-lookup"><span data-stu-id="66e7a-372">If OMS Alerts fire but work items are not created in ITSM product or configuration items are not created/linked to work items or for any other generic information, look in the following places:</span></span>
 -   -  <span data-ttu-id="66e7a-373">ITSMC: Řešení zobrazuje souhrnné údaje o připojení nebo pracovní položky nebo počítače atd. Klikněte na dlaždici zobrazující **stav konektoru**, což trvá, abyste **hledání protokolů** s relevantní dotazu.</span><span class="sxs-lookup"><span data-stu-id="66e7a-373">ITSMC: The solution shows a summary of connections/work items/computers etc. Click the tile showing **Connector Status**, which takes you to **Log Search**  with the relevant query.</span></span> <span data-ttu-id="66e7a-374">Podívejte se na záznamy protokolu s LogType_S jako chyba. Další informace.</span><span class="sxs-lookup"><span data-stu-id="66e7a-374">Look at the log records with LogType_S as ERROR for more information.</span></span>
 - <span data-ttu-id="66e7a-375">**Protokolu vyhledávání** stránky: zobrazení chyb/souvisejících informací o přímo pomocí dotazu *typ = ServiceDeskLog_CL*.</span><span class="sxs-lookup"><span data-stu-id="66e7a-375">**Log Search** page: view the errors/related information directly using the query *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="66e7a-376">Řešení potíží s nasazení aplikace webového portálu Service Manager</span><span class="sxs-lookup"><span data-stu-id="66e7a-376">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="66e7a-377">V případě jakékoliv problémy s nasazení webové aplikace zkontrolujte, zda že máte dostatečná oprávnění v rámci předplatného uvedených vytvořit nebo nasadit prostředky.</span><span class="sxs-lookup"><span data-stu-id="66e7a-377">In case of any issues with web app deployment, ensure you have sufficient permissions in the subscription mentioned to create/deploy resources.</span></span>
2.  <span data-ttu-id="66e7a-378">Pokud dojde **"Objektu odkaz není nastaven na instanci objektu"** Chyba při spuštění [skriptu](log-analytics-itsmc-service-manager-script.md), zkontrolujte, zda jste zadali platné hodnoty v části **konfigurace uživatele** části .</span><span class="sxs-lookup"><span data-stu-id="66e7a-378">If you get an **"Object reference not set to instance of an object"** error when you run the [script](log-analytics-itsmc-service-manager-script.md), ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="66e7a-379">Pokud se vám nepodaří vytvoření oboru názvů service bus relay, ujistěte se, že zprostředkovatel požadovaný prostředek je zaregistrován v rámci předplatného.</span><span class="sxs-lookup"><span data-stu-id="66e7a-379">If you fail to create service bus relay namespace, ensure that the required resource provider is registered in the subscription.</span></span> <span data-ttu-id="66e7a-380">Pokud není zaregistrovaný, ručně vytvořte obor názvů předávání sběrnice z portálu Azure.</span><span class="sxs-lookup"><span data-stu-id="66e7a-380">If not registered, manually create service bus relay namespace from the Azure portal.</span></span> <span data-ttu-id="66e7a-381">Můžete také vytvořit ji při [vytvoření hybridního připojení](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) z portálu Azure.</span><span class="sxs-lookup"><span data-stu-id="66e7a-381">You can also create it while [creating the hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from the Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="66e7a-382">Kontaktujte nás</span><span class="sxs-lookup"><span data-stu-id="66e7a-382">Contact us</span></span>

<span data-ttu-id="66e7a-383">Pro dotazy nebo zpětnou vazbu na správu konektoru služby IT, kontaktujte nás na adrese [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="66e7a-383">For any queries or feedback on the IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="66e7a-384">Další postup</span><span class="sxs-lookup"><span data-stu-id="66e7a-384">Next steps</span></span>
<span data-ttu-id="66e7a-385">[Přidání ITSM produktů nebo služeb do konektoru služby správy IT](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="66e7a-385">[Add ITSM products/services to IT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
