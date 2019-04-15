---
title: Hochverfügbarkeit von Azure Virtual Machines für SAP NetWeaver | Microsoft-Dokumentation
description: Handbuch zum Thema „Hohe Verfügbarkeit“ für SAP NetWeaver auf virtuellen Azure-Computern
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: msjuergent
manager: patfilot
editor: ''
tags: azure-resource-manager
keywords: ''
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/24/2019
ms.author: juergent
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b3a4f3b37b0dc4d74b03ffcfa61c97fbb571d57f
ms.sourcegitcommit: 04716e13cc2ab69da57d61819da6cd5508f8c422
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/02/2019
ms.locfileid: "58848664"
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms"></a><span data-ttu-id="7a8b4-103">Hochverfügbarkeit von SAP NetWeaver auf virtuellen Azure-Computern</span><span class="sxs-lookup"><span data-stu-id="7a8b4-103">High availability for SAP NetWeaver on Azure VMs</span></span>

[767598]:https://launchpad.support.sap.com/#/notes/767598
[773830]:https://launchpad.support.sap.com/#/notes/773830
[826037]:https://launchpad.support.sap.com/#/notes/826037
[965908]:https://launchpad.support.sap.com/#/notes/965908
[1031096]:https://launchpad.support.sap.com/#/notes/1031096
[1139904]:https://launchpad.support.sap.com/#/notes/1139904
[1173395]:https://launchpad.support.sap.com/#/notes/1173395
[1245200]:https://launchpad.support.sap.com/#/notes/1245200
[1409604]:https://launchpad.support.sap.com/#/notes/1409604
[1558958]:https://launchpad.support.sap.com/#/notes/1558958
[1585981]:https://launchpad.support.sap.com/#/notes/1585981
[1588316]:https://launchpad.support.sap.com/#/notes/1588316
[1590719]:https://launchpad.support.sap.com/#/notes/1590719
[1597355]:https://launchpad.support.sap.com/#/notes/1597355
[1605680]:https://launchpad.support.sap.com/#/notes/1605680
[1619720]:https://launchpad.support.sap.com/#/notes/1619720
[1619726]:https://launchpad.support.sap.com/#/notes/1619726
[1619967]:https://launchpad.support.sap.com/#/notes/1619967
[1750510]:https://launchpad.support.sap.com/#/notes/1750510
[1752266]:https://launchpad.support.sap.com/#/notes/1752266
[1757924]:https://launchpad.support.sap.com/#/notes/1757924
[1757928]:https://launchpad.support.sap.com/#/notes/1757928
[1758182]:https://launchpad.support.sap.com/#/notes/1758182
[1758496]:https://launchpad.support.sap.com/#/notes/1758496
[1772688]:https://launchpad.support.sap.com/#/notes/1772688
[1814258]:https://launchpad.support.sap.com/#/notes/1814258
[1882376]:https://launchpad.support.sap.com/#/notes/1882376
[1909114]:https://launchpad.support.sap.com/#/notes/1909114
[1922555]:https://launchpad.support.sap.com/#/notes/1922555
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1941500]:https://launchpad.support.sap.com/#/notes/1941500
[1956005]:https://launchpad.support.sap.com/#/notes/1956005
[1973241]:https://launchpad.support.sap.com/#/notes/1973241
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2002167]:https://launchpad.support.sap.com/#/notes/2002167
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2039619]:https://launchpad.support.sap.com/#/notes/2039619
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[sap-installation-guides]:http://service.sap.com/instguides

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:https://docs.microsoft.com/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md
[dbms-guide-2.1]:../../virtual-machines-windows-sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:../../virtual-machines-windows-sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:../../virtual-machines-windows-sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:../../virtual-machines-windows-sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:../../virtual-machines-windows-sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:../../virtual-machines-windows-sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:../../virtual-machines-windows-sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:../../virtual-machines-windows-sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:../../virtual-machines-windows-sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:../../virtual-machines-windows-sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:../../virtual-machines-windows-sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:../../virtual-machines-windows-sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:../../virtual-machines-windows-sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:../../virtual-machines-windows-sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:../../virtual-machines-windows-sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:../../virtual-machines-windows-sap-deployment-guide.md
[deployment-guide-2.2]:../../virtual-machines-windows-sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94
[deployment-guide-3.1.2]:../../virtual-machines-windows-sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:../../virtual-machines-windows-sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:../../virtual-machines-windows-sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:../../virtual-machines-windows-sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:../../virtual-machines-windows-sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:../../virtual-machines-windows-sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:../../virtual-machines-windows-sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:../../virtual-machines-windows-sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc
[deployment-guide-4.4.2]:../../virtual-machines-windows-sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542
[deployment-guide-4.4]:../../virtual-machines-windows-sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d
[deployment-guide-4.5.1]:../../virtual-machines-windows-sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4
[deployment-guide-4.5.2]:../../virtual-machines-windows-sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f
[deployment-guide-4.5]:../../virtual-machines-windows-sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca
[deployment-guide-5.1]:../../virtual-machines-windows-sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:../../virtual-machines-windows-sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:../../virtual-machines-windows-sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8

[deployment-guide-configure-monitoring-scenario-1]:../../virtual-machines-windows-sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b
[deployment-guide-configure-proxy]:../../virtual-machines-windows-sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:../../virtual-machines-windows-sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:../../virtual-machines-windows-sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:../../virtual-machines-windows-sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:../../virtual-machines-windows-sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:../../virtual-machines-windows-sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:../../virtual-machines-windows-sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:../../virtual-machines-windows-sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:../../virtual-machines-windows-sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:../../virtual-machines-windows-sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b

[deploy-template-cli]:../../../resource-group-template-deploy.md#deploy-with-azure-cli-for-mac-linux-and-windows
[deploy-template-portal]:../../../resource-group-template-deploy.md#deploy-with-the-preview-portal
[deploy-template-powershell]:../../../resource-group-template-deploy.md#deploy-with-powershell

[dr-guide-classic]:https://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:../../virtual-machines-windows-sap-get-started.md
[getting-started-dbms]:../../virtual-machines-windows-sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:../../virtual-machines-windows-sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:../../virtual-machines-windows-sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:https://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11]:planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92

[planning-guide-figure-100]:media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:high-availability-guide.md
[sap-ha-guide-1]:high-availability-guide.md#217c5479-5595-4cd8-870d-15ab00d4f84c
[sap-ha-guide-2]:high-availability-guide.md#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-3]:high-availability-guide.md#42156640c6-01cf-45a9-b225-4baa678b24f1
[sap-ha-guide-3.1]:high-availability-guide.md#f76af273-1993-4d83-b12d-65deeae23686
[sap-ha-guide-3.2]:high-availability-guide.md#3e85fbe0-84b1-4892-87af-d9b65ff91860
[sap-ha-guide-4]:high-availability-guide.md#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-4.1]:high-availability-guide.md#1a3c5408-b168-46d6-99f5-4219ad1b1ff2
[sap-ha-guide-5]:high-availability-guide.md#fdfee875-6e66-483a-a343-14bbaee33275
[sap-ha-guide-5.1]:high-availability-guide.md#be21cf3e-fb01-402b-9955-54fbecf66592
[sap-ha-guide-5.2]:high-availability-guide.md#ff7a9a06-2bc5-4b20-860a-46cdb44669cd
[sap-ha-guide-6]:high-availability-guide.md#2ddba413-a7f5-4e4e-9a51-87908879c10a
[sap-ha-guide-6.1]:high-availability-guide.md#1a464091-922b-48d7-9d08-7cecf757f341
[sap-ha-guide-6.2]:high-availability-guide.md#44641e18-a94e-431f-95ff-303ab65e0bcb
[sap-ha-guide-7]:high-availability-guide.md#2e3fec50-241e-441b-8708-0b1864f66dfa
[sap-ha-guide-7.1]:high-availability-guide.md#93faa747-907e-440a-b00a-1ae0a89b1c0e
[sap-ha-guide-7.2]:high-availability-guide.md#f559c285-ee68-4eec-add1-f60fe7b978db
[sap-ha-guide-7.2.1]:high-availability-guide.md#b5b1fd0b-1db4-4d49-9162-de07a0132a51
[sap-ha-guide-7.3]:high-availability-guide.md#ddd878a0-9c2f-4b8e-8968-26ce60be1027
[sap-ha-guide-7.4]:high-availability-guide.md#045252ed-0277-4fc8-8f46-c5a29694a816
[sap-ha-guide-8]:high-availability-guide.md#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:high-availability-guide.md#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.2]:high-availability-guide.md#7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310
[sap-ha-guide-8.3]:high-availability-guide.md#47d5300a-a830-41d4-83dd-1a0d1ffdbe6a
[sap-ha-guide-8.4]:high-availability-guide.md#b22d7b3b-4343-40ff-a319-097e13f62f9e
[sap-ha-guide-8.5]:high-availability-guide.md#9fbd43c0-5850-4965-9726-2a921d85d73f
[sap-ha-guide-8.6]:high-availability-guide.md#84c019fe-8c58-4dac-9e54-173efd4b2c30
[sap-ha-guide-8.7]:high-availability-guide.md#7a8f3e9b-0624-4051-9e41-b73fff816a9e
[sap-ha-guide-8.8]:high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.9]:high-availability-guide.md#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.10]:high-availability-guide.md#e69e9a34-4601-47a3-a41c-d2e11c626c0c
[sap-ha-guide-8.11]:high-availability-guide.md#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:high-availability-guide.md#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:high-availability-guide.md#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.2]:high-availability-guide.md#e49a4529-50c9-4dcf-bde7-15a0c21d21ca
[sap-ha-guide-8.12.2.1]:high-availability-guide.md#06260b30-d697-4c4d-b1c9-d22c0bd64855
[sap-ha-guide-8.12.2.2]:high-availability-guide.md#4c08c387-78a0-46b1-9d27-b497b08cac3d
[sap-ha-guide-8.12.3]:high-availability-guide.md#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:high-availability-guide.md#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:high-availability-guide.md#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097
[sap-ha-guide-9.1.2]:high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0
[sap-ha-guide-9.1.3]:high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556
[sap-ha-guide-9.1.4]:high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761
[sap-ha-guide-9.1.5]:high-availability-guide.md#4498c707-86c0-4cde-9c69-058a7ab8c3ac
[sap-ha-guide-9.2]:high-availability-guide.md#85d78414-b21d-4097-92b6-34d8bcb724b7
[sap-ha-guide-9.3]:high-availability-guide.md#8a276e16-f507-4071-b829-cdc0a4d36748
[sap-ha-guide-9.4]:high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a
[sap-ha-guide-9.5]:high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5
[sap-ha-guide-9.6]:high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772
[sap-ha-guide-10]:high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9
[sap-ha-guide-10.1]:high-availability-guide.md#65fdef0f-9f94-41f9-b314-ea45bbfea445
[sap-ha-guide-10.2]:high-availability-guide.md#5e959fa9-8fcd-49e5-a12c-37f6ba07b916
[sap-ha-guide-10.3]:high-availability-guide.md#755a6b93-0099-4533-9f6d-5c9a613878b5

[sap-ha-multi-sid-guide]:high-availability-multi-sid.md (SAP-Multi-SID-Konfiguration mit Hochverfügbarkeit)


[sap-ha-guide-figure-1000]:media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../networking/networking-overview.md
[sap-pam]:https://support.sap.com/pam (SAP-Produktverfügbarkeitsmatrix [Product Availability Matrix, PAM])
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[storage-azure-cli]:../../../storage/common/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../../storage/common/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../../storage/common/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../../storage/common/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../windows/disks-types.md
[storage-redundancy]:../../../storage/common/storage-redundancy.md
[storage-scalability-targets]:../../../storage/common/storage-scalability-targets.md
[storage-use-azcopy]:../../../storage/common/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../../linux/attach-disk-portal.md
[virtual-machines-windows-attach-disk-portal]:../../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../azure-resource-manager/resource-group-overview.md
[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../../linux/capture-image.md#capture-the-vm
[virtual-machines-windows-capture-image]:../../virtual-machines-windows-capture-image.md
[virtual-machines-windows-capture-image-capture]:../../virtual-machines-windows-capture-image.md#capture-the-vm
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:../../virtual-machines-windows-sizes.md
[virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]:../../windows/sql/virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md
[virtual-machines-windows-portal-sql-alwayson-int-listener]:../../windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md
[virtual-machines-upload-image-windows-resource-manager]:../../virtual-machines-windows-upload-image.md
[virtual-machines-windows-tutorial]:../../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../linux/multiple-nics.md
[virtual-network-deploy-multinic-arm-ps]:../windows/multiple-nics.md
[virtual-network-deploy-multinic-arm-template]:../../../virtual-network/template-samples.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../../virtual-network/manage-virtual-network.md#create-a-virtual-network
[virtual-networks-manage-dns-in-vnet]:../../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../../virtual-network/virtual-network-deploy-multinic-classic-ps.md
[virtual-networks-nsg]:../../../virtual-network/security-overview.md
[virtual-networks-reserved-private-ip]:../../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md


<span data-ttu-id="7a8b4-111">Azure Virtual Machines eignet sich als Lösung für Organisationen, die Compute-, Speicher- und Netzwerkressourcen in kürzester Zeit und ohne langwierige Beschaffungszyklen benötigen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-111">Azure Virtual Machines is the solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="7a8b4-112">Sie können Azure Virtual Machines verwenden, um klassische Anwendungen wie SAP NetWeaver-basiertes ABAP und Java sowie einen ABAP+Java-Stapel bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-112">You can use Azure Virtual Machines to deploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="7a8b4-113">Erweitern Sie die Zuverlässigkeit und Verfügbarkeit ohne zusätzliche lokale Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-113">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="7a8b4-114">Azure Virtual Machines unterstützt die standortübergreifende Konnektivität, sodass Sie Azure Virtual Machines in die lokalen Domänen, privaten Clouds und die SAP-Systemumgebung Ihrer Organisation integrieren können.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-114">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="7a8b4-115">In diesem Artikel werden die Schritte beschrieben, mit denen Sie hoch verfügbare SAP-Systeme in Azure mit dem Azure Resource Manager-Bereitstellungsmodell bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-115">In this article, we cover the steps that you can take to deploy high-availability SAP systems in Azure by using the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="7a8b4-116">Dabei werden die folgenden Hauptaufgaben behandelt:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-116">We walk you through these major tasks:</span></span>

* <span data-ttu-id="7a8b4-117">Die richtigen SAP-Installationshandbücher und -hinweise finden Sie im Abschnitt [Ressourcen][sap-ha-guide-2].</span><span class="sxs-lookup"><span data-stu-id="7a8b4-117">Find the right SAP Notes and installation guides, listed in the [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="7a8b4-118">Dieser Artikel ergänzt die SAP-Dokumentation und -Hinweise zur Installation. Diese stellen die primären Ressourcen für das Installieren und Bereitstellen von SAP-Software auf bestimmten Plattformen dar.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-118">This article complements SAP installation documentation and SAP Notes, which are the primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="7a8b4-119">Informieren Sie sich über die Unterschiede zwischen dem Azure Resource Manager-Bereitstellungsmodell und dem klassischen Azure-Bereitstellungsmodell.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-119">Learn the differences between the Azure Resource Manager deployment model and the Azure classic deployment model.</span></span>
* <span data-ttu-id="7a8b4-120">Informieren Sie sich über die Quorummodi für das Windows Server-Failoverclustering, damit Sie das für Ihre Azure-Bereitstellung geeignete Modell auswählen können.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-120">Learn about Windows Server Failover Clustering quorum modes, so you can select the model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="7a8b4-121">Informieren Sie sich über freigegebenen Speicher für das Windows Server-Failoverclustering in Azure-Diensten.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-121">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="7a8b4-122">Informieren Sie sich darüber, wie Sie Single Point of Failure-Komponenten wie Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) und Datenbank-Managementsysteme (DBMS) sowie redundante Komponenten wie SAP-Anwendungsserver in Azure schützen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-122">Learn how to help protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="7a8b4-123">Arbeiten Sie ein Schritt-für-Schritt-Beispiel einer Installation und Konfiguration eines SAP-Systems mit hoher Verfügbarkeit in einem Windows Server-Failoverclustering-Cluster in Azure mit dem Azure Resource Manager durch.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-123">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="7a8b4-124">Informieren Sie sie über die weiteren erforderlichen Schritte zum Verwenden von Windows Server-Failoverclustering in Azure, die bei einer lokalen Bereitstellung nicht erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-124">Learn about additional steps required to use Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="7a8b4-125">Zur Vereinfachung der Bereitstellung und Konfiguration verwenden wir in diesem Artikel die Resource Manager-Vorlagen für hohe Verfügbarkeit bei SAP mit drei Ebenen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-125">To simplify deployment and configuration, in this article, we use the SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="7a8b4-126">Die Vorlagen automatisieren die Bereitstellung der gesamten Infrastruktur, die Sie für ein SAP-System mit hoher Verfügbarkeit benötigen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-126">The templates automate deployment of the entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="7a8b4-127">Außerdem unterstützt die Infrastruktur die SAPS-Größenfestlegung (SAP Application Performance Standard) Ihres SAP-Systems.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-127">The infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> <span data-ttu-id="7a8b4-128">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="7a8b4-128">Prerequisites</span></span>
<span data-ttu-id="7a8b4-129">Achten Sie vor Beginn darauf, dass die in den folgenden Abschnitten beschriebenen Voraussetzungen erfüllt sind.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-129">Before you start, make sure that you meet the prerequisites that are described in the following sections.</span></span> <span data-ttu-id="7a8b4-130">Überprüfen Sie darüber hinaus alle Ressourcen im Abschnitt [Ressourcen][sap-ha-guide-2].</span><span class="sxs-lookup"><span data-stu-id="7a8b4-130">Also, be sure to check all resources listed in the [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="7a8b4-131">In diesem Artikel verwenden wir Azure Resource Manager-Vorlagen für [SAP NetWeaver mit drei Ebenen](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-131">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span></span> <span data-ttu-id="7a8b4-132">Eine hilfreiche Übersicht über die Vorlagen finden Sie unter [Azure Resource Manager-Vorlagen für SAP](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-132">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> <span data-ttu-id="7a8b4-133">Ressourcen</span><span class="sxs-lookup"><span data-stu-id="7a8b4-133">Resources</span></span>
<span data-ttu-id="7a8b4-134">In diesen Artikeln werden SAP-Bereitstellungen in Azure behandelt:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-134">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="7a8b4-135">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide] (Azure Virtual Machines – Planung und Implementierung für SAP NetWeaver)</span><span class="sxs-lookup"><span data-stu-id="7a8b4-135">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="7a8b4-136">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide] (Azure Virtual Machines – Bereitstellung für SAP NetWeaver)</span><span class="sxs-lookup"><span data-stu-id="7a8b4-136">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="7a8b4-137">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide] (Azure Virtual Machines – DBMS-Bereitstellung für SAP NetWeaver)</span><span class="sxs-lookup"><span data-stu-id="7a8b4-137">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="7a8b4-138">[Hochverfügbarkeit von Azure Virtual Machines für SAP NetWeaver (dieses Handbuch)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="7a8b4-138">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="7a8b4-139">Sofern möglich, wird ein Link zum entsprechenden SAP-Installationshandbuch bereitgestellt (siehe [SAP-Installationshandbücher][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-139">Whenever possible, we give you a link to the referring SAP installation guide (see the [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="7a8b4-140">Wenn Sie Informationen zu den Voraussetzungen und zum Installationsvorgang benötigen, sollten Sie die SAP NetWeaver-Installationshandbücher sorgfältig lesen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-140">For prerequisites and information about the installation process, it's a good idea to read the SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="7a8b4-141">Dieser Artikel behandelt nur die spezifischen Aufgaben für SAP NetWeaver-basierte Systeme, die Sie mit Azure Virtual Machines verwenden können.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-141">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="7a8b4-142">Diese SAP-Hinweise beziehen sich auf das Thema SAP in Azure:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-142">These SAP Notes are related to the topic of SAP in Azure:</span></span>

| <span data-ttu-id="7a8b4-143">Hinweisnummer</span><span class="sxs-lookup"><span data-stu-id="7a8b4-143">Note number</span></span> | <span data-ttu-id="7a8b4-144">Titel</span><span class="sxs-lookup"><span data-stu-id="7a8b4-144">Title</span></span> |
| --- | --- |
| <span data-ttu-id="7a8b4-145">[1928533]</span><span class="sxs-lookup"><span data-stu-id="7a8b4-145">[1928533]</span></span> |<span data-ttu-id="7a8b4-146">SAP-Anwendungen auf Azure: Unterstützte Produkte und Größen</span><span class="sxs-lookup"><span data-stu-id="7a8b4-146">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="7a8b4-147">[2015553]</span><span class="sxs-lookup"><span data-stu-id="7a8b4-147">[2015553]</span></span> |<span data-ttu-id="7a8b4-148">SAP auf Microsoft Azure: Voraussetzungen für die Unterstützung</span><span class="sxs-lookup"><span data-stu-id="7a8b4-148">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="7a8b4-149">[1999351]</span><span class="sxs-lookup"><span data-stu-id="7a8b4-149">[1999351]</span></span> |<span data-ttu-id="7a8b4-150">Enhanced Azure Monitoring for SAP (Erweiterte Azure-Überwachung für SAP)</span><span class="sxs-lookup"><span data-stu-id="7a8b4-150">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="7a8b4-151">[2178632]</span><span class="sxs-lookup"><span data-stu-id="7a8b4-151">[2178632]</span></span> |<span data-ttu-id="7a8b4-152">Wichtige Überwachungsmetriken für SAP in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="7a8b4-152">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="7a8b4-153">[1999351]</span><span class="sxs-lookup"><span data-stu-id="7a8b4-153">[1999351]</span></span> |<span data-ttu-id="7a8b4-154">Virtualisierung unter Windows: Erweiterte Überwachung</span><span class="sxs-lookup"><span data-stu-id="7a8b4-154">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="7a8b4-155">[2243692]</span><span class="sxs-lookup"><span data-stu-id="7a8b4-155">[2243692]</span></span> |<span data-ttu-id="7a8b4-156">Verwendung von Azure Storage Premium (SSD) für SAP-DBMS-Instanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-156">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="7a8b4-157">Informieren Sie sich auch über die [Einschränkungen von Azure-Abonnements][azure-subscription-service-limits-subscription], einschließlich der allgemeinen Standard- und Maximaleinschränkungen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-157">Learn more about the [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a><span data-ttu-id="7a8b4-158">Vergleich zwischen dem Azure Resource Manager- und dem klassischen Azure-Bereitstellungsmodell für SAP mit hoher Verfügbarkeit</span><span class="sxs-lookup"><span data-stu-id="7a8b4-158">High-availability SAP with Azure Resource Manager vs. the Azure classic deployment model</span></span>
<span data-ttu-id="7a8b4-159">Das Azure Resource Manager-Bereitstellungsmodell und das klassische Azure-Bereitstellungsmodell unterscheiden sich in den folgenden Bereichen:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-159">The Azure Resource Manager and Azure classic deployment models are different in the following areas:</span></span>

- <span data-ttu-id="7a8b4-160">Ressourcengruppen</span><span class="sxs-lookup"><span data-stu-id="7a8b4-160">Resource groups</span></span>
- <span data-ttu-id="7a8b4-161">Abhängigkeit des internen Azure Load Balancer von der Azure-Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="7a8b4-161">Azure internal load balancer dependency on the Azure resource group</span></span>
- <span data-ttu-id="7a8b4-162">Unterstützung für SAP-Multi-SID-Szenarien</span><span class="sxs-lookup"><span data-stu-id="7a8b4-162">Support for SAP multi-SID scenarios</span></span>

### <a name="f76af273-1993-4d83-b12d-65deeae23686"></a> <span data-ttu-id="7a8b4-163">Ressourcengruppen</span><span class="sxs-lookup"><span data-stu-id="7a8b4-163">Resource groups</span></span>
<span data-ttu-id="7a8b4-164">In Azure Resource Manager können Sie mit Ressourcengruppen alle Anwendungsressourcen im Azure-Abonnement verwalten.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-164">In Azure Resource Manager, you can use resource groups to manage all the application resources in your Azure subscription.</span></span> <span data-ttu-id="7a8b4-165">Bei einem integrierten Ansatz in einer Ressourcengruppe haben alle Ressourcen denselben Lebenszyklus.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-165">An integrated approach, in a resource group, all resources have the same life cycle.</span></span> <span data-ttu-id="7a8b4-166">So werden z.B. alle Ressourcen zur gleichen Zeit erstellt und gelöscht.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-166">For example, all resources are created at the same time and they are deleted at the same time.</span></span> <span data-ttu-id="7a8b4-167">Weitere Informationen zu [Ressourcengruppen](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-167">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> <span data-ttu-id="7a8b4-168">Abhängigkeit des internen Azure Load Balancer von der Azure-Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="7a8b4-168">Azure internal load balancer dependency on the Azure resource group</span></span>

<span data-ttu-id="7a8b4-169">Beim klassischen Azure-Bereitstellungsmodell besteht eine Abhängigkeit zwischen dem internen Azure Load Balancer (Azure Load Balancer-Dienst) und der Clouddienstgruppe.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-169">In the Azure classic deployment model, there is a dependency between the Azure internal load balancer (Azure Load Balancer service) and the cloud service group.</span></span> <span data-ttu-id="7a8b4-170">Für jeden internen Load Balancer wird eine Clouddienstgruppe benötigt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-170">Every internal load balancer needs one cloud service group.</span></span>

<span data-ttu-id="7a8b4-171">In Azure Resource Manager benötigen Sie keine Azure-Ressourcengruppe, um den Azure Load Balancer zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-171">In Azure Resource Manager, you don't need an Azure resource group to use Azure Load Balancer.</span></span> <span data-ttu-id="7a8b4-172">Die Umgebung ist einfacher und flexibler.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-172">The environment is simpler and more flexible.</span></span>

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="7a8b4-173">Unterstützung für SAP-Multi-SID-Szenarien</span><span class="sxs-lookup"><span data-stu-id="7a8b4-173">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="7a8b4-174">In Azure Resource Manager können Sie mehrere SAP-SID-ASCS/SCS-Instanzen in einem Cluster installieren.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-174">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="7a8b4-175">Instanzen mit mehreren SIDs sind möglich, weil für jeden internen Azure Load Balancer mehrere IP-Adressen unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-175">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="7a8b4-176">Wenn Sie das klassische Azure-Bereitstellungsmodell verwenden möchten, befolgen Sie die Schritte in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](https://go.microsoft.com/fwlink/?LinkId=613056) (SAP NetWeaver in Azure: Clustering von SAP ASCS/SCS-Instanzen mit dem Windows Server-Failoverclustering in Azure mit SIOS DataKeeper).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-176">To use the Azure classic deployment model, follow the procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](https://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a8b4-177">Es wird dringend empfohlen, das Azure Resource Manager-Bereitstellungsmodell für Ihre SAP-Installationen zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-177">We strongly recommend that you use the Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="7a8b4-178">Es bietet viele Vorteile, die beim klassischen Bereitstellungsmodell nicht zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-178">It offers many benefits that are not available in the classic deployment model.</span></span> <span data-ttu-id="7a8b4-179">Erfahren Sie mehr über Azure-[Bereitstellungsmodelle][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span><span class="sxs-lookup"><span data-stu-id="7a8b4-179">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> <span data-ttu-id="7a8b4-180">Windows Server-Failoverclustering</span><span class="sxs-lookup"><span data-stu-id="7a8b4-180">Windows Server Failover Clustering</span></span>
<span data-ttu-id="7a8b4-181">Windows Server-Failoverclustering ist die Grundlage für eine SAP ASCS/SCS-Installation und ein DBMS in Windows mit hoher Verfügbarkeit.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-181">Windows Server Failover Clustering is the foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="7a8b4-182">Bei einem Failovercluster handelt es sich um eine Gruppe von 1+n unabhängigen Servern, die zur Steigerung der Verfügbarkeit von Anwendungen und Diensten zusammenarbeiten.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-182">A failover cluster is a group of 1+n independent servers (nodes) that work together to increase the availability of applications and services.</span></span> <span data-ttu-id="7a8b4-183">Wenn ein Knotenfehler auftritt, berechnet das Windows Server-Failoverclustering die Anzahl von Fehlern, die auftreten können, während trotzdem ein fehlerfreier Cluster für die Bereitstellung der Anwendungen und Dienste aufrechterhalten wird.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-183">If a node failure occurs, Windows Server Failover Clustering calculates the number of failures that can occur while maintaining a healthy cluster to provide applications and services.</span></span> <span data-ttu-id="7a8b4-184">Sie können zwischen verschiedenen Quorummodi wählen, um das Failoverclustering zu erzielen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-184">You can choose from different quorum modes to achieve failover clustering.</span></span>

### <a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> <span data-ttu-id="7a8b4-185">Quorummodi</span><span class="sxs-lookup"><span data-stu-id="7a8b4-185">Quorum modes</span></span>
<span data-ttu-id="7a8b4-186">Sie können zwischen vier Quorummodi auswählen, wenn Sie das Windows Server-Failoverclustering verwenden:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-186">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="7a8b4-187">**Knotenmehrheit:**</span><span class="sxs-lookup"><span data-stu-id="7a8b4-187">**Node Majority**.</span></span> <span data-ttu-id="7a8b4-188">Jeder Knoten des Clusters kann abstimmen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-188">Each node of the cluster can vote.</span></span> <span data-ttu-id="7a8b4-189">Der Cluster funktioniert nur mit der Mehrheit der Stimmen, d.h. mit mehr als der Hälfte der Stimmen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-189">The cluster functions only with a majority of votes, that is, with more than half the votes.</span></span> <span data-ttu-id="7a8b4-190">Diese Option wird für Cluster mit einer ungeraden Anzahl von Knoten empfohlen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-190">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="7a8b4-191">So können z.B. drei Knoten in einem Cluster mit sieben Knoten einen Ausfall verursachen. Der Cluster erreicht immer noch eine Mehrheit und wird weiterhin ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-191">For example, three nodes in a seven-node cluster can fail, and the cluster stills achieves a majority and continues to run.</span></span>  
* <span data-ttu-id="7a8b4-192">**Knoten- und Datenträgermehrheit:**</span><span class="sxs-lookup"><span data-stu-id="7a8b4-192">**Node and Disk Majority**.</span></span> <span data-ttu-id="7a8b4-193">Alle Knoten plus ein festgelegter Datenträger im Clusterspeicher (der Datenträgerzeuge) können abstimmen, solange sie verfügbar sind und kommunizieren.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-193">Each node and a designated disk (a disk witness) in the cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="7a8b4-194">Der Cluster funktioniert nur mit der Mehrheit der Stimmen, d.h. mit mehr als der Hälfte der Stimmen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-194">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="7a8b4-195">Dieser Modus ist in einer Clusterumgebung mit einer geraden Anzahl von Knoten sinnvoll.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-195">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="7a8b4-196">Solange die Hälfte der Knoten sowie der Datenträgerzeuge online sind, verbleibt der Cluster in einem ordnungsgemäßen Zustand.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-196">If half the nodes and the disk are online, the cluster remains in a healthy state.</span></span>
* <span data-ttu-id="7a8b4-197">**Knoten- und Dateifreigabemehrheit:**</span><span class="sxs-lookup"><span data-stu-id="7a8b4-197">**Node and File Share Majority**.</span></span> <span data-ttu-id="7a8b4-198">Alle Knoten sowie eine vom Administrator erstellte zugewiesene Dateifreigabe (der Dateifreigabenzeuge) können abstimmen – unabhängig davon, ob die Knoten und Dateifreigaben verfügbar sind und kommunizieren.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-198">Each node plus a designated file share (a file share witness) that the administrator creates can vote, regardless of whether the nodes and file share are available and in communication.</span></span> <span data-ttu-id="7a8b4-199">Der Cluster funktioniert nur mit der Mehrheit der Stimmen, d.h. mit mehr als der Hälfte der Stimmen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-199">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="7a8b4-200">Dieser Modus ist in einer Clusterumgebung mit einer geraden Anzahl von Knoten sinnvoll.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-200">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="7a8b4-201">Er ähnelt dem Modus mit Knoten- und Datenträgermehrheit, verwendet jedoch einen Dateifreigabenzeugen anstelle eines Datenträgerzeugen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-201">It's similar to the Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="7a8b4-202">Die Implementierung dieses Modus ist einfach, doch wenn die Dateifreigabe selbst nicht hoch verfügbar ist, kann diese Lösung ein Single Point of Failure (SPOF) sein.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-202">This mode is easy to implement, but if the file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="7a8b4-203">**Keine Mehrheit: nur Datenträger**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-203">**No Majority: Disk Only**.</span></span> <span data-ttu-id="7a8b4-204">Der Cluster hat ein Quorum, wenn ein Knoten verfügbar ist und mit einem bestimmten Datenträger im Clusterspeicher kommuniziert.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-204">The cluster has a quorum if one node is available and in communication with a specific disk in the cluster storage.</span></span> <span data-ttu-id="7a8b4-205">Nur die Knoten, die auch mit diesem Datenträger kommunizieren, können dem Cluster beitreten.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-205">Only the nodes that also are in communication with that disk can join the cluster.</span></span> <span data-ttu-id="7a8b4-206">Die Verwendung dieses Modus wird nicht empfohlen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-206">We recommend that you do not use this mode.</span></span>

## <a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> <span data-ttu-id="7a8b4-207">Lokales Windows Server-Failoverclustering</span><span class="sxs-lookup"><span data-stu-id="7a8b4-207">Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="7a8b4-208">Abbildung 1 zeigt einen Cluster mit zwei Knoten.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-208">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="7a8b4-209">Wenn die Netzwerkverbindung zwischen den Knoten unterbrochen wird, aber beide Knoten weiter ausgeführt werden, bestimmt ein Quorumdatenträger oder eine Quorumdateifreigabe, welcher Knoten die Clusteranwendungen und -dienste weiter bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-209">If the network connection between the nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue to provide the cluster's applications and services.</span></span> <span data-ttu-id="7a8b4-210">Der Knoten, der Zugriff auf den Quorumdatenträger oder die Quorumdateifreigabe hat, ist derjenige, der die weitere Ausführung der Dienste gewährleistet.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-210">The node that has access to the quorum disk or file share is the node that ensures that services continue.</span></span>

<span data-ttu-id="7a8b4-211">Da in diesem Beispiel ein Cluster mit zwei Knoten verwendet wird, verwenden wir den Quorummodus „Knoten- und Dateifreigabemehrheit“.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-211">Because this example uses a two-node cluster, we use the Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="7a8b4-212">Der Modus „Knoten- und Datenträgermehrheit“ ist auch eine mögliche Option.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-212">The Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="7a8b4-213">In einer Produktionsumgebung wird die Verwendung eines Quorumdatenträgers empfohlen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-213">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="7a8b4-214">Sie können die Technologien für die Netzwerk- und Speichersysteme verwenden, um diese hoch verfügbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-214">You can use network and storage system technology to make it highly available.</span></span>

![Abbildung 1: Beispiel für eine Konfiguration des Windows Server-Failoverclusterings für SAP ASCS/SCS in Azure][sap-ha-guide-figure-1000]

<span data-ttu-id="7a8b4-216">_**Abbildung 1:** Beispiel für eine Konfiguration des Windows Server-Failoverclusterings für SAP ASCS/SCS in Azure_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-216">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> <span data-ttu-id="7a8b4-217">Freigegebener Speicher</span><span class="sxs-lookup"><span data-stu-id="7a8b4-217">Shared storage</span></span>
<span data-ttu-id="7a8b4-218">Abbildung 1 zeigt auch einen Cluster mit zwei Knoten und freigegebenem Speicher.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-218">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="7a8b4-219">In einem lokalen Cluster mit freigegebenem Speicher erkennen alle Knoten im Cluster den freigegebenen Speicher.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-219">In an on-premises shared storage cluster, all nodes in the cluster detect shared storage.</span></span> <span data-ttu-id="7a8b4-220">Mithilfe eines Sperrmechanismus werden die Daten vor Beschädigung geschützt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-220">A locking mechanism protects the data from corruption.</span></span> <span data-ttu-id="7a8b4-221">Alle Knoten können erkennen, wenn ein anderer Knoten ausfällt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-221">All nodes can detect if another node fails.</span></span> <span data-ttu-id="7a8b4-222">Wenn ein Knoten ausfällt, übernehmen die restlichen den Besitz der Speicherressourcen und stellen die Verfügbarkeit der Dienste sicher.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-222">If one node fails, the remaining node takes ownership of the storage resources and ensures the availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="7a8b4-223">Sie benötigen bei einigen DBMS-Anwendungen wie SQL Server für Hochverfügbarkeit keine freigegebenen Datenträger.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-223">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="7a8b4-224">SQL Server Always On führt die Replikation von DBMS-Daten- und -Protokolldateien vom lokalen Datenträger eines Clusterknotens auf den lokalen Datenträger eines anderen Clusterknotens durch.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-224">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="7a8b4-225">In diesem Fall ist bei der Windows-Clusterkonfiguration kein freigegebener Datenträger erforderlich.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-225">In that case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> <span data-ttu-id="7a8b4-226">Netzwerk und Namensauflösung</span><span class="sxs-lookup"><span data-stu-id="7a8b4-226">Networking and name resolution</span></span>
<span data-ttu-id="7a8b4-227">Clientcomputer erreichen den Cluster über eine virtuelle IP-Adresse und den virtuellen Hostnamen, der vom DNS-Server bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-227">Client computers reach the cluster over a virtual IP address and a virtual host name that the DNS server provides.</span></span> <span data-ttu-id="7a8b4-228">Die lokalen Knoten und der DNS-Server können mehrere IP-Adressen verwenden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-228">The on-premises nodes and the DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="7a8b4-229">Bei einer normalen Konfiguration können Sie zwei oder mehr Netzwerkverbindungen verwenden:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-229">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="7a8b4-230">Eine dedizierte Verbindung mit dem Speicher</span><span class="sxs-lookup"><span data-stu-id="7a8b4-230">A dedicated connection to the storage</span></span>
* <span data-ttu-id="7a8b4-231">Eine clusterinterne Netzwerkverbindung für den Takt</span><span class="sxs-lookup"><span data-stu-id="7a8b4-231">A cluster-internal network connection for the heartbeat</span></span>
* <span data-ttu-id="7a8b4-232">Ein von den Clients verwendetes öffentliches Netzwerk zum Herstellen der Verbindung mit dem Cluster</span><span class="sxs-lookup"><span data-stu-id="7a8b4-232">A public network that clients use to connect to the cluster</span></span>

## <a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> <span data-ttu-id="7a8b4-233">Windows Server-Failoverclustering in Azure</span><span class="sxs-lookup"><span data-stu-id="7a8b4-233">Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="7a8b4-234">Im Vergleich mit Bare-Metal- oder privaten Cloudbereitstellungen sind für virtuelle Azure-Computer zusätzliche Schritte erforderlich, um Windows Server-Failoverclustering zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-234">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="7a8b4-235">Wenn Sie einen freigegebenen Clusterdatenträger erstellen, müssen Sie mehrere IP-Adressen und virtuelle Hostnamen für die SAP ASCS/SCS-Instanz festlegen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-235">When you build a shared cluster disk, you need to set several IP addresses and virtual host names for the SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="7a8b4-236">In diesem Artikel werden die wichtigsten Konzepte und die zusätzlichen Schritte besprochen, die erforderlich sind, um einen SAP Central Services-Cluster mit hoher Verfügbarkeit in Azure zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-236">In this article, we discuss key concepts and the additional steps required to build an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="7a8b4-237">Wir zeigen Ihnen, wie Sie das Drittanbietertool SIOS DataKeeper einrichten und den internen Load Balancer von Azure konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-237">We show you how to set up the third-party tool SIOS DataKeeper, and how to configure the Azure internal load balancer.</span></span> <span data-ttu-id="7a8b4-238">Mit diesen Tools können Sie einen Windows-Failovercluster mit einem Dateifreigabenzeugen in Azure erstellen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-238">You can use these tools to create a Windows failover cluster with a file share witness in Azure.</span></span>

![Abbildung 2: Konfiguration des Windows Server-Failoverclusterings in Azure ohne freigegebenen Datenträger][sap-ha-guide-figure-1001]

<span data-ttu-id="7a8b4-240">_**Abbildung 2:** Konfiguration des Windows Server-Failoverclusterings in Azure ohne freigegebenen Datenträger_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-240">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> <span data-ttu-id="7a8b4-241">Freigegebener Datenträger in Azure mit SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="7a8b4-241">Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="7a8b4-242">Sie benötigen freigegebenen Clusterspeicher für eine hoch verfügbare SAP ASCS/SCS-Instanz.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-242">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="7a8b4-243">Ab September 2016 bietet Azure keinen freigegebenen Speicher zum Erstellen eines Clusters mit freigegebenem Speicher mehr an.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-243">As of September 2016, Azure doesn't offer shared storage that you can use to create a shared storage cluster.</span></span> <span data-ttu-id="7a8b4-244">Die Drittanbietersoftware SIOS DataKeeper Cluster Edition ermöglicht es Ihnen, einen gespiegelten Speicher zu erstellen, der freigegebenen Clusterspeicher simuliert.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-244">You can use third-party software SIOS DataKeeper Cluster Edition to create a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="7a8b4-245">Die SIOS-Lösung bietet eine synchrone Datenreplikation in Echtzeit.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-245">The SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="7a8b4-246">Eine freigegebene Datenträgerressource für einen Cluster wird folgendermaßen erstellt:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-246">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="7a8b4-247">Fügen Sie eine zusätzliche Azure-VHD an sämtliche virtuelle Computer (VMs) in einer Windows-Clusterkonfiguration an.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-247">Attach an additional Azure virtual hard disk (VHD) to each of the virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="7a8b4-248">Führen Sie SIOS DataKeeper Cluster Edition auf beiden virtuellen Computerknoten aus.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-248">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="7a8b4-249">Konfigurieren Sie SIOS DataKeeper Cluster Edition so, dass synchron der Inhalt des zusätzlich angehängten VHD-Volumes vom virtuellen Quellcomputer im zusätzlich angehängten VHD-Volume des virtuellen Zielcomputers gespiegelt wird.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-249">Configure SIOS DataKeeper Cluster Edition so that it mirrors the content of the additional VHD attached volume from the source virtual machine to the additional VHD attached volume of the target virtual machine.</span></span> <span data-ttu-id="7a8b4-250">SIOS DataKeeper abstrahiert die lokalen Quell- und Zielvolumes und präsentiert diese beim Windows Server-Failoverclustering als einen freigegebenen Datenträger.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-250">SIOS DataKeeper abstracts the source and target local volumes, and then presents them to Windows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="7a8b4-251">Weitere Informationen zu [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-251">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Abbildung 3: Konfiguration des Windows Server-Failoverclusterings in Azure mit SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="7a8b4-253">_**Abbildung 3:** Konfiguration des Windows Server-Failoverclusterings in Azure mit SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-253">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="7a8b4-254">Sie benötigen bei einigen DBMS-Produkten wie SQL Server für Hochverfügbarkeit keine freigegebenen Datenträger.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-254">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="7a8b4-255">SQL Server Always On führt die Replikation von DBMS-Daten- und -Protokolldateien vom lokalen Datenträger eines Clusterknotens auf den lokalen Datenträger eines anderen Clusterknotens durch.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-255">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="7a8b4-256">In diesem Fall ist bei der Windows-Clusterkonfiguration kein freigegebener Datenträger erforderlich.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-256">In this case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> <span data-ttu-id="7a8b4-257">Namensauflösung in Azure</span><span class="sxs-lookup"><span data-stu-id="7a8b4-257">Name resolution in Azure</span></span>
<span data-ttu-id="7a8b4-258">Die Azure-Cloudplattform bietet keine Möglichkeit, virtuelle IP-Adressen, z.B. Floating IP-Adressen, zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-258">The Azure cloud platform doesn't offer the option to configure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="7a8b4-259">Sie benötigen eine alternative Lösung für die Einrichtung einer virtuellen IP-Adresse, um die Clusterressource in der Cloud zu erreichen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-259">You need an alternative solution to set up a virtual IP address to reach the cluster resource in the cloud.</span></span>
<span data-ttu-id="7a8b4-260">Azure stellt über den Azure Load Balancer-Dienst einen internen Lastenausgleich zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-260">Azure has an internal load balancer in the Azure Load Balancer service.</span></span> <span data-ttu-id="7a8b4-261">Mit dem internen Load Balancer erreichen Clients den Cluster über die virtuelle IP-Adresse des Clusters.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-261">With the internal load balancer, clients reach the cluster over the cluster virtual IP address.</span></span>
<span data-ttu-id="7a8b4-262">Sie müssen den internen Load Balancer in der Ressourcengruppe bereitstellen, die die Clusterknoten enthält.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-262">You need to deploy the internal load balancer in the resource group that contains the cluster nodes.</span></span> <span data-ttu-id="7a8b4-263">Anschließend konfigurieren Sie alle erforderlichen Portweiterleitungsregeln mithilfe der Testports des internen Load Balancers.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-263">Then, configure all necessary port forwarding rules with the probe ports of the internal load balancer.</span></span>
<span data-ttu-id="7a8b4-264">Die Clients können über den virtuellen Hostnamen eine Verbindung herstellen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-264">The clients can connect via the virtual host name.</span></span> <span data-ttu-id="7a8b4-265">Der DNS-Server löst die IP-Adresse des Clusters auf. Der interne Load Balancer übernimmt die Weiterleitung an den aktiven Knoten des Clusters.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-265">The DNS server resolves the cluster IP address, and the internal load balancer handles port forwarding to the active node of the cluster.</span></span>

## <a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> <span data-ttu-id="7a8b4-266">Hohe Verfügbarkeit von SAP NetWeaver in Azure Infrastructure-as-a-Service (IaaS)</span><span class="sxs-lookup"><span data-stu-id="7a8b4-266">SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="7a8b4-267">Um Hochverfügbarkeit für SAP-Anwendungen zu erreichen, z.B. für SAP-Softwarekomponenten, müssen Sie die folgenden Komponenten schützen:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-267">To achieve SAP application high availability, such as for SAP software components, you need to protect the following components:</span></span>

* <span data-ttu-id="7a8b4-268">SAP-Anwendungsserverinstanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-268">SAP Application Server instance</span></span>
* <span data-ttu-id="7a8b4-269">SAP ASCS/SCS-Instanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-269">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="7a8b4-270">DBMS-Server</span><span class="sxs-lookup"><span data-stu-id="7a8b4-270">DBMS server</span></span>

<span data-ttu-id="7a8b4-271">Weitere Informationen zum Schützen von SAP-Komponenten in Szenarien mit hoher Verfügbarkeit finden Sie unter [Azure Virtual Machines planning and implementation for SAP NetWeaver](planning-guide.md) (Azure Virtual Machines – Planung und Implementierung für SAP NetWeaver).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-271">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver](planning-guide.md).</span></span>

### <a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> <span data-ttu-id="7a8b4-272">Hohe Verfügbarkeit für SAP-Anwendungsserver</span><span class="sxs-lookup"><span data-stu-id="7a8b4-272">High-availability SAP Application Server</span></span>
<span data-ttu-id="7a8b4-273">Für die SAP-Anwendungsserver und -Dialoginstanzen ist meist keine spezielle hoch verfügbare Lösung erforderlich.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-273">You usually don't need a specific high-availability solution for the SAP Application Server and dialog instances.</span></span> <span data-ttu-id="7a8b4-274">Sie erreichen Hochverfügbarkeit durch Redundanz und durch Konfiguration mehrerer Dialoginstanzen in verschiedenen Instanzen von virtuellen Azure-Computern.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-274">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="7a8b4-275">Es müssen mindestens zwei SAP-Anwendungsinstanzen auf zwei Instanzen von virtuellen Azure-Computern installiert sein.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-275">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Abbildung 4: Hochverfügbarkeit für SAP-Anwendungsserver][sap-ha-guide-figure-2000]

<span data-ttu-id="7a8b4-277">_**Abbildung 4:** Hochverfügbarkeit für SAP-Anwendungsserver_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-277">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="7a8b4-278">Alle virtuellen Computer, auf denen SAP-Anwendungsserverinstanzen gehostet werden, müssen in derselben Azure-Verfügbarkeitsgruppe platziert werden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-278">You must place all virtual machines that host SAP Application Server instances in the same Azure availability set.</span></span> <span data-ttu-id="7a8b4-279">Eine Azure-Verfügbarkeitsgruppe stellt Folgendes sicher:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-279">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="7a8b4-280">Alle virtuellen Computer sind Teil derselben Upgradedomäne.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-280">All virtual machines are part of the same upgrade domain.</span></span> <span data-ttu-id="7a8b4-281">Eine Upgradedomäne stellt beispielsweise sicher, dass die virtuellen Computer nicht gleichzeitig mit geplanten Wartungsausfallzeiten aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-281">An upgrade domain, for example, makes sure that the virtual machines aren't updated at the same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="7a8b4-282">Alle virtuellen Computer sind Teil derselben Fehlerdomäne.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-282">All virtual machines are part of the same fault domain.</span></span> <span data-ttu-id="7a8b4-283">Eine Fehlerdomäne stellt beispielsweise bei der Bereitstellung virtueller Computer sicher, dass kein Single Point of Failure Auswirkungen auf die Verfügbarkeit aller virtuellen Computer hat.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-283">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects the availability of all virtual machines.</span></span>

<span data-ttu-id="7a8b4-284">Erfahren Sie mehr über das [Verwalten der Verfügbarkeit virtueller Computer][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="7a8b4-284">Learn more about how to [manage the availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="7a8b4-285">Da das Azure-Speicherkonto ein potenzieller Single Point of Failure sein kann, benötigen Sie unbedingt mindestens zwei Azure-Speicherkonten, auf die mindestens zwei virtuelle Computer verteilt sind.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-285">Because the Azure storage account is a potential single point of failure, it's important to have at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="7a8b4-286">In einer idealen Konfiguration würden die Datenträger jedes virtuellen Computers, auf dem eine SAP-Dialoginstanz ausgeführt wird, in einem anderen Speicherkonto bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-286">In an ideal setup, the disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> <span data-ttu-id="7a8b4-287">Hohe Verfügbarkeit für SAP ASCS/SCS-Instanzen</span><span class="sxs-lookup"><span data-stu-id="7a8b4-287">High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="7a8b4-288">Abbildung 5 ist ein Beispiel für eine SAP ASCS/SCS-Instanz mit hoher Verfügbarkeit.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-288">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Abbildung 5: Hohe Verfügbarkeit für SAP ASCS/SCS-Instanzen][sap-ha-guide-figure-2001]

<span data-ttu-id="7a8b4-290">_**Abbildung 5:** Hochverfügbarkeit für SAP ASCS/SCS-Instanzen_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-290">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> <span data-ttu-id="7a8b4-291">Hohe Verfügbarkeit für SAP ASCS/SCS-Instanzen mit Windows Server-Failoverclustering in Azure</span><span class="sxs-lookup"><span data-stu-id="7a8b4-291">SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="7a8b4-292">Im Vergleich mit Bare-Metal- oder privaten Cloudbereitstellungen sind für virtuelle Azure-Computer zusätzliche Schritte erforderlich, um Windows Server-Failoverclustering zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-292">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="7a8b4-293">Zum Erstellen eines Windows-Failoverclusters sind für das Clustern einer SAP ASCS/SCS-Instanz ein freigegebener Clusterdatenträger, mehrere IP-Adressen und virtuelle Hostnamen und ein interner Azure Load Balancer erforderlich.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-293">To build a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="7a8b4-294">Dies wird später in diesem Artikel ausführlicher erläutert.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-294">We discuss this in more detail later in the article.</span></span>

![Abbildung 6: Konfiguration des Windows Server-Failoverclusterings für eine SAP ASCS/SCS-Instanz in Azure mit SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="7a8b4-296">_**Abbildung 6:** Konfiguration des Windows Server-Failoverclusterings für eine SAP ASCS/SCS-Instanz in Azure mit SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-296">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a><span data-ttu-id="7a8b4-297">Hohe Verfügbarkeit für DBMS-Instanzen</span><span class="sxs-lookup"><span data-stu-id="7a8b4-297">High-availability DBMS instance</span></span>
<span data-ttu-id="7a8b4-298">Das DBMS ist auch eine zentrale Kontaktstelle in einem SAP-System.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-298">The DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="7a8b4-299">Sie sollten es mit einer Lösung mit hoher Verfügbarkeit schützen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-299">You need to protect it by using a high-availability solution.</span></span> <span data-ttu-id="7a8b4-300">Abbildung 7 zeigt eine SQL Server Always On-Lösung mit hoher Verfügbarkeit in Azure unter Verwendung von Windows Server-Failoverclustering und des internen Azure Load Balancers.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-300">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and the Azure internal load balancer.</span></span> <span data-ttu-id="7a8b4-301">SQL Server Always On repliziert DBMS-Daten- und -Protokolldateien mithilfe seiner eigenen DBMS-Replikation.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-301">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="7a8b4-302">In diesem Fall benötigen Sie keine freigegebenen Clusterdatenträger, sodass die gesamte Einrichtung vereinfacht wird.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-302">In this case, you don't need cluster shared disks, which simplifies the entire setup.</span></span>

![Abbildung 7: Beispiel für ein hoch verfügbares SAP-DBMS mit SQL Server Always On][sap-ha-guide-figure-2003]

<span data-ttu-id="7a8b4-304">_**Abbildung 7:** Beispiel für ein hoch verfügbares SAP-DBMS mit SQL Server Always On_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-304">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="7a8b4-305">Weitere Informationen zum Clustering von SQL Server in Azure mithilfe des Azure Resource Manager-Bereitstellungsmodells finden Sie in den folgenden Artikeln:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-305">For more information about clustering SQL Server in Azure by using the Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="7a8b4-306">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual] (Manuelles Konfigurieren einer AlwaysOn-Verfügbarkeitsgruppe in Azure Virtual Machines mit dem Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="7a8b4-306">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="7a8b4-307">[Configure an Azure internal load balancer for an AlwaysOn availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener] (Konfigurieren eines internen Azure Load Balancer für eine AlwaysOn-Verfügbarkeitsgruppe in Azure)</span><span class="sxs-lookup"><span data-stu-id="7a8b4-307">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> <span data-ttu-id="7a8b4-308">End-to-End-Bereitstellungsszenarios mit hoher Verfügbarkeit</span><span class="sxs-lookup"><span data-stu-id="7a8b4-308">End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="7a8b4-309">Bereitstellungsszenario mit Architekturvorlage 1</span><span class="sxs-lookup"><span data-stu-id="7a8b4-309">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="7a8b4-310">Abbildung 8 zeigt ein Beispiel für eine SAP NetWeaver-Architektur mit hoher Verfügbarkeit in Azure für **ein** SAP-System.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-310">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="7a8b4-311">Dieses Szenario wird wie folgt eingerichtet:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-311">This scenario is set up as follows:</span></span>

- <span data-ttu-id="7a8b4-312">Ein dedizierter Cluster wird für die SAP ASCS/SCS-Instanz verwendet.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-312">One dedicated cluster is used for the SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="7a8b4-313">Ein dedizierter Cluster wird für die DBMS-Instanz verwendet.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-313">One dedicated cluster is used for the DBMS instance.</span></span>
- <span data-ttu-id="7a8b4-314">SAP-Anwendungsserverinstanzen werden auf eigenen dedizierten VMs bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-314">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Abbildung 8: SAP-Architekturvorlage 1 für Hochverfügbarkeit mit dediziertem Cluster für ASCS/SCS und DBMS][sap-ha-guide-figure-2004]

<span data-ttu-id="7a8b4-316">_**Abbildung 8:** SAP-Architekturvorlage 1 für Hochverfügbarkeit mit dediziertem Cluster für ASCS/SCS und DBMS_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-316">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="7a8b4-317">Bereitstellungsszenario mit Architekturvorlage 2</span><span class="sxs-lookup"><span data-stu-id="7a8b4-317">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="7a8b4-318">Abbildung 9 zeigt ein Beispiel für eine SAP NetWeaver-Architektur mit hoher Verfügbarkeit in Azure für **ein** SAP-System.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-318">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="7a8b4-319">Dieses Szenario wird wie folgt eingerichtet:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-319">This scenario is set up as follows:</span></span>

- <span data-ttu-id="7a8b4-320">Ein dedizierter Cluster wird für die SAP ASCS/SCS-Instanz **und** für die DBMS verwendet.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-320">One dedicated cluster is used for **both** the SAP ASCS/SCS instance and the DBMS.</span></span>
- <span data-ttu-id="7a8b4-321">SAP-Anwendungsserverinstanzen werden auf eigenen dedizierten VMs bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-321">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Abbildung 9: SAP-Architekturvorlage 2 für Hochverfügbarkeit mit dediziertem Cluster für ASCS/SCS und dediziertem Cluster für DBMS][sap-ha-guide-figure-2005]

<span data-ttu-id="7a8b4-323">_**Abbildung 9:** SAP-Architekturvorlage 2 für Hochverfügbarkeit mit dediziertem Cluster für ASCS/SCS und dediziertem Cluster für DBMS_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-323">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="7a8b4-324">Bereitstellungsszenario mit Architekturvorlage 3</span><span class="sxs-lookup"><span data-stu-id="7a8b4-324">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="7a8b4-325">Abbildung 10 zeigt ein Beispiel für eine SAP NetWeaver-Architektur mit hoher Verfügbarkeit in Azure für **zwei** SAP-Systeme mit &lt;SID1&gt; und &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-325">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="7a8b4-326">Dieses Szenario wird wie folgt eingerichtet:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-326">This scenario is set up as follows:</span></span>

- <span data-ttu-id="7a8b4-327">Ein dedizierter Cluster wird **sowohl** für die SAP ASCS/SCS SID1-Instanz *als auch* für die SAP ASCS/SCS SID2-Instanz (ein Cluster) verwendet.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-327">One dedicated cluster is used for **both** the SAP ASCS/SCS SID1 instance *and* the SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="7a8b4-328">Ein dedizierter Cluster wird für DBMS SID1 verwendet, und ein anderer dedizierter Cluster wird für DBMS SID2 verwendet (zwei Cluster).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-328">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="7a8b4-329">SAP-Anwendungsserverinstanzen für das SAP-System SID1 verfügen über eigene dedizierte VMs.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-329">SAP Application Server instances for the SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="7a8b4-330">SAP-Anwendungsserverinstanzen für das SAP-System SID2 verfügen über eigene dedizierte VMs.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-330">SAP Application Server instances for the SAP system SID2 have their own dedicated VMs.</span></span>

![Abbildung 10: SAP-Architekturvorlage 3 für Hochverfügbarkeit mit dediziertem Cluster für verschiedene ASCS/SCS-Instanzen][sap-ha-guide-figure-6003]

<span data-ttu-id="7a8b4-332">_**Abbildung 10:** SAP-Architekturvorlage 3 für Hochverfügbarkeit mit dediziertem Cluster für verschiedene ASCS/SCS-Instanzen_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-332">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> <span data-ttu-id="7a8b4-333">Vorbereiten der Infrastruktur</span><span class="sxs-lookup"><span data-stu-id="7a8b4-333">Prepare the infrastructure</span></span>

### <a name="prepare-the-infrastructure-for-architectural-template-1"></a><span data-ttu-id="7a8b4-334">Vorbereiten der Infrastruktur für Architekturvorlage 1</span><span class="sxs-lookup"><span data-stu-id="7a8b4-334">Prepare the infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="7a8b4-335">Azure Resource Manager-Vorlagen für SAP vereinfachen die Bereitstellung der erforderlichen Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-335">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="7a8b4-336">Die Vorlagen mit drei Ebenen in Azure Resource Manager unterstützen auch Szenarien mit hoher Verfügbarkeit, z.B. in Architekturvorlage 1, die über zwei Cluster verfügt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-336">The three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="7a8b4-337">Jeder Cluster ist ein SAP-Single Point of Failure für SAP ASCS/SCS und das DBMS.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-337">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="7a8b4-338">Hier können Sie die Azure Resource Manager-Vorlagen für das in diesem Artikel beschriebene Beispielszenario abrufen:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-338">Here's where you can get Azure Resource Manager templates for the example scenario we describe in this article:</span></span>

* [<span data-ttu-id="7a8b4-339">Azure Marketplace-Image</span><span class="sxs-lookup"><span data-stu-id="7a8b4-339">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="7a8b4-340">Benutzerdefiniertes Image</span><span class="sxs-lookup"><span data-stu-id="7a8b4-340">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)

<span data-ttu-id="7a8b4-341">So bereiten Sie die Infrastruktur für Architekturvorlage 1 vor</span><span class="sxs-lookup"><span data-stu-id="7a8b4-341">To prepare the infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="7a8b4-342">Wählen Sie im Azure-Portal auf dem Blatt **Parameter** im Feld **SYSTEMAVAILABILITY** die Option **HA**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-342">In the Azure portal, on the **Parameters** blade, in the **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Abbildung 11: Festlegen von Azure Resource Manager-Parametern für die Hochverfügbarkeit von SAP][sap-ha-guide-figure-3000]

<span data-ttu-id="7a8b4-344">_**Abbildung 11:** Festlegen von Azure Resource Manager-Parametern für die Hochverfügbarkeit von SAP_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-344">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="7a8b4-345">Mit den Vorlagen wird Folgendes erstellt:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-345">The templates create:</span></span>

  * <span data-ttu-id="7a8b4-346">**Virtuelle Computer:**</span><span class="sxs-lookup"><span data-stu-id="7a8b4-346">**Virtual machines**:</span></span>
    * <span data-ttu-id="7a8b4-347">Virtuelle Computer für SAP-Anwendungsserver: <*SAP-System-SID*>-di-<*Anzahl*></span><span class="sxs-lookup"><span data-stu-id="7a8b4-347">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="7a8b4-348">Virtuelle Computer für den ASCS/SCS-Cluster: <*SAP-System-SID*>-ascs-<*Anzahl*></span><span class="sxs-lookup"><span data-stu-id="7a8b4-348">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="7a8b4-349">DBMS-Cluster: <*SAP-System-SID*>-db-<*Anzahl*></span><span class="sxs-lookup"><span data-stu-id="7a8b4-349">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="7a8b4-350">**Netzwerkkarten für alle virtuellen Computer mit zugeordneten IP-Adressen:**</span><span class="sxs-lookup"><span data-stu-id="7a8b4-350">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="7a8b4-351"><*SAP-System-SID*&gt;-nic-di-&lt;*Anzahl*></span><span class="sxs-lookup"><span data-stu-id="7a8b4-351"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="7a8b4-352"><*SAP-System-SID*&gt;-nic-ascs-&lt;*Anzahl*></span><span class="sxs-lookup"><span data-stu-id="7a8b4-352"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="7a8b4-353"><*SAP-System-SID*&gt;-nic-db-&lt;*Anzahl*></span><span class="sxs-lookup"><span data-stu-id="7a8b4-353"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="7a8b4-354">**Azure-Speicherkonten**</span><span class="sxs-lookup"><span data-stu-id="7a8b4-354">**Azure storage accounts**</span></span>

  * <span data-ttu-id="7a8b4-355">**Verfügbarkeitsgruppen** für:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-355">**Availability groups** for:</span></span>
    * <span data-ttu-id="7a8b4-356">Virtuelle Computer für SAP-Anwendungsserver: <*SAP-System-SID*>-avset-di</span><span class="sxs-lookup"><span data-stu-id="7a8b4-356">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="7a8b4-357">Virtuelle Computer für den SAP ASCS/SCS-Cluster: <*SAP-System-SID*>-avset-ascs</span><span class="sxs-lookup"><span data-stu-id="7a8b4-357">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="7a8b4-358">Virtuelle Computer für das DBMS: <*SAP-System-SID*>-avset-db</span><span class="sxs-lookup"><span data-stu-id="7a8b4-358">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="7a8b4-359">**Interner Azure Load Balancer:**</span><span class="sxs-lookup"><span data-stu-id="7a8b4-359">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="7a8b4-360">Mit allen Ports für die ASCS/SCS-Instanz und IP-Adresse <*SAP-System-SID*>-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="7a8b4-360">With all ports for the ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="7a8b4-361">Mit allen Ports für das SQL Server-DBMS und IP-Adresse <*SAP-System-SID*>-lb-db</span><span class="sxs-lookup"><span data-stu-id="7a8b4-361">With all ports for the SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="7a8b4-362">**Netzwerksicherheitsgruppe:** &lt;*SAP-System-SID*&gt;-nsg-ascs-0</span><span class="sxs-lookup"><span data-stu-id="7a8b4-362">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="7a8b4-363">Mit einem offenen externen RDP-Port (Remote Desktop Protocol) zum virtuellen Computer <*SAP-System-SID*>-ascs-0</span><span class="sxs-lookup"><span data-stu-id="7a8b4-363">With an open external Remote Desktop Protocol (RDP) port to the <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="7a8b4-364">Sämtliche IP-Adressen für die Netzwerkkarten und den internen Azure Load Balancer sind standardmäßig **dynamisch**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-364">All IP addresses of the network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="7a8b4-365">Ändern Sie diese in **statische** IP-Adressen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-365">Change them to **static** IP addresses.</span></span> <span data-ttu-id="7a8b4-366">Die Vorgehensweise wird weiter unten in diesem Artikel beschrieben.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-366">We describe how to do this later in the article.</span></span>
>
>

### <a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> <span data-ttu-id="7a8b4-367">Bereitstellen virtueller Computer mit Verbindungen mit dem Unternehmensnetzwerk (standortübergreifend) für die Verwendung in der Produktion</span><span class="sxs-lookup"><span data-stu-id="7a8b4-367">Deploy virtual machines with corporate network connectivity (cross-premises) to use in production</span></span>
<span data-ttu-id="7a8b4-368">Stellen Sie für SAP-Produktionssysteme virtuelle Azure-Computer mit einer [(standortübergreifenden) Verbindung mit dem Unternehmensnetzwerk][planning-guide-2.2] bereit. Verwenden Sie dazu ein Azure-Site-to-Site-VPN oder Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-368">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="7a8b4-369">Sie können Ihre Azure Virtual Network-Instanz verwenden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-369">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="7a8b4-370">Das virtuelle Netzwerk und das Subnetz wurden bereits erstellt und vorbereitet.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-370">The virtual network and subnet have already been created and prepared.</span></span>
>
>

1. <span data-ttu-id="7a8b4-371">Wählen Sie im Azure-Portal auf dem Blatt **Parameter** im Feld **NEWOREXISTINGSUBNET** die Option **existing**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-371">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2. <span data-ttu-id="7a8b4-372">Fügen Sie im Feld **SUBNETID** die vollständige Zeichenfolge Ihrer vorbereiteten Subnetz-ID für das Azure-Netzwerk ein, in dem Sie Ihre virtuellen Azure-Computer bereitstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-372">In the **SUBNETID** box, add the full string of your prepared Azure network SubnetID where you plan to deploy your Azure virtual machines.</span></span>
3. <span data-ttu-id="7a8b4-373">Führen Sie diesen PowerShell-Befehl aus, um eine Liste mit allen Azure-Netzwerksubnetzen abzurufen:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-373">To get a list of all Azure network subnets, run this PowerShell command:</span></span>

   ```PowerShell
   (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
   ```

   <span data-ttu-id="7a8b4-374">Das Feld **ID** zeigt die **SUBNETID** an.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-374">The **ID** field shows the **SUBNETID**.</span></span>
4. <span data-ttu-id="7a8b4-375">Führen Sie diesen PowerShell-Befehl aus, um eine Liste mit allen **SUBNETID**-Werten abzurufen:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-375">To get a list of all **SUBNETID** values, run this PowerShell command:</span></span>

   ```PowerShell
   (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
   ```

   <span data-ttu-id="7a8b4-376">Die **SUBNETID** sieht in etwa wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-376">The **SUBNETID** looks like this:</span></span>

   ```
   /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
   ```

### <a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> <span data-ttu-id="7a8b4-377">Bereitstellen von auf die Cloud beschränkten SAP-Instanzen für Tests und Demos</span><span class="sxs-lookup"><span data-stu-id="7a8b4-377">Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="7a8b4-378">Sie können Ihr SAP-System mit hoher Verfügbarkeit in einem reinen Cloudbereitstellungsmodell bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-378">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="7a8b4-379">Diese Art der Bereitstellung eignet sich hauptsächlich für Demonstrations- und Testzwecke.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-379">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="7a8b4-380">Es eignet sich nicht für den Einsatz in Produktionsumgebungen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-380">It's not suited for production use cases.</span></span>

- <span data-ttu-id="7a8b4-381">Wählen Sie im Azure-Portal auf dem Blatt **Parameter** im Feld **NEWOREXISTINGSUBNET** die Option **new**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-381">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="7a8b4-382">Lassen Sie das Feld **SUBNETID** leer.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-382">Leave the **SUBNETID** field empty.</span></span>

  <span data-ttu-id="7a8b4-383">Das virtuelle Azure-Netzwerk und das Subnetz werden von der Azure Resource Manager-Vorlage für SAP automatisch erstellt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-383">The SAP Azure Resource Manager template automatically creates the Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="7a8b4-384">Außerdem müssen Sie mindestens einen dedizierten virtuellen Computer für Active Directory und DNS in der gleichen Instanz von Azure Virtual Network bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-384">You also need to deploy at least one dedicated virtual machine for Active Directory and DNS in the same Azure Virtual Network instance.</span></span> <span data-ttu-id="7a8b4-385">Die Vorlage erstellt diese virtuellen Computer nicht.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-385">The template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-the-infrastructure-for-architectural-template-2"></a><span data-ttu-id="7a8b4-386">Vorbereiten der Infrastruktur für Architekturvorlage 2</span><span class="sxs-lookup"><span data-stu-id="7a8b4-386">Prepare the infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="7a8b4-387">Sie können diese Azure Resource Manager-Vorlage für SAP zur Vereinfachung der Bereitstellung der erforderlichen Infrastrukturressourcen für SAP-Architekturvorlage 2 verwenden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-387">You can use this Azure Resource Manager template for SAP to help simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="7a8b4-388">Azure Resource Manager-Vorlagen für dieses Bereitstellungsszenario sind hier verfügbar:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-388">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="7a8b4-389">Azure Marketplace-Image</span><span class="sxs-lookup"><span data-stu-id="7a8b4-389">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="7a8b4-390">Benutzerdefiniertes Image</span><span class="sxs-lookup"><span data-stu-id="7a8b4-390">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)


### <a name="prepare-the-infrastructure-for-architectural-template-3"></a><span data-ttu-id="7a8b4-391">Vorbereiten der Infrastruktur für Architekturvorlage 3</span><span class="sxs-lookup"><span data-stu-id="7a8b4-391">Prepare the infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="7a8b4-392">Sie können die Infrastruktur vorbereiten und SAP für **Multi-SID** konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-392">You can prepare the infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="7a8b4-393">Beispielsweise können Sie eine weitere SAP ASCS/SCS-Instanz einer *vorhandenen* Clusterkonfiguration hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-393">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="7a8b4-394">Weitere Informationen finden Sie unter [Konfigurieren einer zusätzlichen SAP ASCS/SCS-Instanz in einer vorhandenen Clusterkonfiguration zum Erstellen einer Multi-SID-SAP-Konfiguration in Azure Resource Manager][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="7a8b4-394">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration to create an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="7a8b4-395">Wenn Sie einen neuen Multi-SID-Cluster erstellen möchten, können Sie die Multi-SID-[Schnellstartvorlagen auf GitHub](https://github.com/Azure/azure-quickstart-templates) verwenden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-395">If you want to create a new multi-SID cluster, you can use the multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="7a8b4-396">Sie müssen die folgenden drei Vorlagen bereitstellen, um einen neuen Multi-SID-Cluster zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-396">To create a new multi-SID cluster, you need to deploy the following three templates:</span></span>

* [<span data-ttu-id="7a8b4-397">ASCS/SCS-Vorlage</span><span class="sxs-lookup"><span data-stu-id="7a8b4-397">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="7a8b4-398">Datenbankvorlage</span><span class="sxs-lookup"><span data-stu-id="7a8b4-398">Database template</span></span>](#database-template)
* [<span data-ttu-id="7a8b4-399">Anwendungsservervorlage</span><span class="sxs-lookup"><span data-stu-id="7a8b4-399">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="7a8b4-400">Die folgenden Abschnitte enthalten weitere Details zu den Vorlagen und Parametern, die Sie in den Vorlagen angeben müssen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-400">The following sections have more details about the templates and the parameters you need to provide in the templates.</span></span>

#### <a name="ASCS-SCS-template"></a> <span data-ttu-id="7a8b4-401">ASCS/SCS-Vorlage</span><span class="sxs-lookup"><span data-stu-id="7a8b4-401">ASCS/SCS template</span></span>

<span data-ttu-id="7a8b4-402">Mit der ASCS/SCS-Vorlage werden zwei virtuelle Computer bereitgestellt, die Sie verwenden können, um einen Windows-Failovercluster zum Hosten von mehreren ASCS/SCS-Instanzen zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-402">The ASCS/SCS template deploys two virtual machines that you can use to create a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="7a8b4-403">Geben Sie in der [ASCS/SCS-Multi-SID-Vorlage][sap-templates-3-tier-multisid-xscs-marketplace-image] Werte für die folgenden Parameter ein, um die Vorlage einzurichten:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-403">To set up the ASCS/SCS multi-SID template, in the [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image], enter values for the following parameters:</span></span>

  - <span data-ttu-id="7a8b4-404">**Ressourcenpräfix**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-404">**Resource Prefix**.</span></span>  <span data-ttu-id="7a8b4-405">Legen Sie das Ressourcenpräfix fest, um alle Ressourcen, die während der Bereitstellung erstellt werden, mit einem Präfix zu versehen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-405">Set the resource prefix, which is used to prefix all resources that are created during the deployment.</span></span> <span data-ttu-id="7a8b4-406">Da die Ressourcen nicht nur zu einem einzigen SAP-System gehören, ist das Präfix der Ressource nicht die SID eines einzigen SAP-Systems.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-406">Because the resources do not belong to only one SAP system, the prefix of the resource is not the SID of one SAP system.</span></span>  <span data-ttu-id="7a8b4-407">Das Präfix muss zwischen **drei und sechs Zeichen** lang sein.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-407">The prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="7a8b4-408">**Stapeltyp**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-408">**Stack Type**.</span></span> <span data-ttu-id="7a8b4-409">Wählen Sie den Stapeltyp des SAP-Systems aus.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-409">Select the stack type of the SAP system.</span></span> <span data-ttu-id="7a8b4-410">Abhängig vom Stapeltyp hat der Azure Load Balancer eine (nur ABAP oder Java) oder zwei (ABAP+Java) private IP-Adressen pro SAP-System.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-410">Depending on the stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="7a8b4-411">**Betriebssystemtyp**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-411">**OS Type**.</span></span> <span data-ttu-id="7a8b4-412">Wählen Sie das Betriebssystem des virtuellen Computers aus.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-412">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="7a8b4-413">**Anzahl von SAP-Systemen**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-413">**SAP System Count**.</span></span> <span data-ttu-id="7a8b4-414">Wählen Sie die Anzahl von SAP-Systemen aus, die Sie in diesem Cluster installieren möchten.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-414">Select the number of SAP systems you want to install in this cluster.</span></span>
  -  <span data-ttu-id="7a8b4-415">**Systemverfügbarkeit**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-415">**System Availability**.</span></span> <span data-ttu-id="7a8b4-416">Wählen Sie **HA** (Hohe Verfügbarkeit).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-416">Select **HA**.</span></span>
  -  <span data-ttu-id="7a8b4-417">**Administratorbenutzername und Administratorkennwort**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-417">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="7a8b4-418">Erstellen Sie einen neuen Benutzer, der verwendet werden kann, um sich am Computer anzumelden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-418">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="7a8b4-419">**Neues oder vorhandenes Subnetz**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-419">**New Or Existing Subnet**.</span></span> <span data-ttu-id="7a8b4-420">Legen Sie fest, ob ein neues virtuelles Netzwerk und Subnetz erstellt oder ein vorhandenes Subnetz verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-420">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="7a8b4-421">Wenn Sie bereits über ein virtuelles Netzwerk verfügen, das mit dem lokalen Netzwerk verbunden ist, wählen Sie hier **vorhanden** aus.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-421">If you already have a virtual network that is connected to your on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="7a8b4-422">**Subnetz-ID**. Wenn Sie die VM in einem vorhandenen VNET bereitstellen möchten, in dem Sie ein Subnetz definiert haben, dem die VM zugewiesen werden soll, geben Sie die ID dieses spezifischen Subnetzes an.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-422">**Subnet Id**. If you want to deploy the VM into an existing VNet where you have a subnet defined the VM should be assigned to, name the ID of that specific subnet.</span></span> <span data-ttu-id="7a8b4-423">Die ID hat normalerweise das folgende Format: /subscriptions/<*Abonnement-ID*>/resourceGroups/<*Name der Ressourcengruppe*>/providers/Microsoft.Network/virtualNetworks/<*Name des virtuellen Netzwerks*>/subnets/<*Name des Subnetzes*></span><span class="sxs-lookup"><span data-stu-id="7a8b4-423">The ID usually looks like this: /subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="7a8b4-424">Die Vorlage stellt eine Azure Load Balancer-Instanz bereit, die mehrere SAP-Systeme unterstützt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-424">The template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="7a8b4-425">Die ASCS-Instanzen werden für die Instanznummer 00, 10, 20... konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-425">The ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="7a8b4-426">Die SCS-Instanzen werden für die Instanznummer 01, 11, 21... konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-426">The SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="7a8b4-427">Die Instanzen von ASCS Enqueue Replication Server (ERS) (nur Linux) werden für die Instanznummern 02, 12, 22 usw. konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-427">The ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="7a8b4-428">Die SCS ERS-Instanzen (nur Linux) werden für die Instanznummer 03, 13, 23... konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-428">The SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="7a8b4-429">Der Load Balancer enthält 1 VIP (2 für Linux), 1 VIP für ASCS/SCS und 1 VIP für ERS (nur Linux).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-429">The load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="7a8b4-430">Die folgende Liste enthält alle Lastenausgleichsregeln (wobei x für die Nummer des SAP-Systems steht, z.B. 1, 2, 3...):</span><span class="sxs-lookup"><span data-stu-id="7a8b4-430">The following list contains all load balancing rules (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="7a8b4-431">Windows-spezifische Ports für jedes SAP-System: 445, 5985</span><span class="sxs-lookup"><span data-stu-id="7a8b4-431">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="7a8b4-432">ASCS-Ports (Instanznummer x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span><span class="sxs-lookup"><span data-stu-id="7a8b4-432">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="7a8b4-433">SCS-Ports (Instanznummer x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span><span class="sxs-lookup"><span data-stu-id="7a8b4-433">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="7a8b4-434">ASCS ERS-Ports unter Linux (Instanznummer x2): 33x2, 5x213, 5x214, 5x216</span><span class="sxs-lookup"><span data-stu-id="7a8b4-434">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="7a8b4-435">SCS ERS-Ports unter Linux (Instanznummer x3): 33x3, 5x313, 5x314, 5x316</span><span class="sxs-lookup"><span data-stu-id="7a8b4-435">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="7a8b4-436">Der Lastenausgleich wird so konfiguriert, dass die folgenden Testports verwendet werden (wobei x die Nummer des SAP-Systems ist, z.B. 1, 2, 3...).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-436">The load balancer is configured to use the following probe ports (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="7a8b4-437">ASCS/SCS – Testport des internen Lastenausgleichs: 620x0</span><span class="sxs-lookup"><span data-stu-id="7a8b4-437">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="7a8b4-438">ERS – Testport des internen Lastenausgleichs (nur Linux): 621x2</span><span class="sxs-lookup"><span data-stu-id="7a8b4-438">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <a name="database-template"></a> <span data-ttu-id="7a8b4-439">Datenbankvorlage</span><span class="sxs-lookup"><span data-stu-id="7a8b4-439">Database template</span></span>

<span data-ttu-id="7a8b4-440">Mit der Datenbankvorlage werden ein oder zwei virtuelle Computer bereitgestellt, die Sie zum Installieren des relationalen Datenbankverwaltungssystems (RDBMS) für ein SAP-System verwenden können.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-440">The database template deploys one or two virtual machines that you can use to install the relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="7a8b4-441">Wenn Sie z.B. eine ASCS/SCS-Vorlage für fünf SAP-Systeme bereitstellen, müssen Sie diese Vorlage fünfmal bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-441">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="7a8b4-442">Geben Sie in der [Datenbank-Multi-SID-Vorlage][sap-templates-3-tier-multisid-db-marketplace-image] Werte für die folgenden Parameter ein, um die Vorlage einzurichten:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-442">To set up the database multi-SID template, in the [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image], enter values for the following parameters:</span></span>

- <span data-ttu-id="7a8b4-443">**SAP-System-ID**. Geben Sie die SAP-System-ID des SAP-Systems ein, das Sie installieren möchten.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-443">**Sap System Id**. Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="7a8b4-444">Die ID wird als Präfix für die Ressourcen verwendet, die bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-444">The ID will be used as a prefix for the resources that are deployed.</span></span>
- <span data-ttu-id="7a8b4-445">**Betriebssystemtyp**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-445">**Os Type**.</span></span> <span data-ttu-id="7a8b4-446">Wählen Sie das Betriebssystem des virtuellen Computers aus.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-446">Select the operating system of the virtual machines.</span></span>
- <span data-ttu-id="7a8b4-447">**Dbtype**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-447">**Dbtype**.</span></span> <span data-ttu-id="7a8b4-448">Wählen Sie den Typ der Datenbank, die Sie auf dem Cluster installieren möchten.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-448">Select the type of the database you want to install on the cluster.</span></span> <span data-ttu-id="7a8b4-449">Wählen Sie **SQL**, wenn Sie Microsoft SQL Server installieren möchten.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-449">Select **SQL** if you want to install Microsoft SQL Server.</span></span> <span data-ttu-id="7a8b4-450">Wählen Sie **HANA**, wenn Sie SAP HANA auf den virtuellen Computern installieren möchten.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-450">Select **HANA** if you plan to install SAP HANA on the virtual machines.</span></span> <span data-ttu-id="7a8b4-451">Stellen Sie sicher, dass Sie den richtigen Betriebssystemtyp auswählen: Wählen Sie **Windows** für SQL und eine Linux-Distribution für HANA aus.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-451">Make sure to select the correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="7a8b4-452">Der Azure Load Balancer, der mit den virtuellen Computern verbunden ist, wird so konfiguriert, dass er den ausgewählten Datenbanktyp unterstützt:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-452">The Azure Load Balancer that is connected to the virtual machines will be configured to support the selected database type:</span></span>
  * <span data-ttu-id="7a8b4-453">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-453">**SQL**.</span></span> <span data-ttu-id="7a8b4-454">Der Lastenausgleich ist auf Port 1433 wirksam.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-454">The load balancer will load-balance port 1433.</span></span> <span data-ttu-id="7a8b4-455">Stellen Sie sicher, dass dieser Port für Ihr SQL Server AlwaysOn-Setup verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-455">Make sure to use this port for your SQL Server Always On setup.</span></span>
  * <span data-ttu-id="7a8b4-456">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-456">**HANA**.</span></span> <span data-ttu-id="7a8b4-457">Der Lastenausgleich ist auf den Ports 35015 und 35017 wirksam.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-457">The load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="7a8b4-458">Stellen Sie sicher, dass Sie SAP HANA mit Instanznummer **50** installieren.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-458">Make sure to install SAP HANA with instance number **50**.</span></span>
  <span data-ttu-id="7a8b4-459">Der Lastenausgleich verwendet den Testport 62550.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-459">The load balancer will use probe port 62550.</span></span>
- <span data-ttu-id="7a8b4-460">**SAP-Systemgröße**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-460">**Sap System Size**.</span></span> <span data-ttu-id="7a8b4-461">Legen Sie die Anzahl von SAPS fest, die vom neuen System bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-461">Set the number of SAPS the new system will provide.</span></span> <span data-ttu-id="7a8b4-462">Wenn Sie nicht sicher sind, wie viele SAPS das System benötigt, wenden Sie sich an den SAP-Technologiepartner oder Systemintegrator.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-462">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
- <span data-ttu-id="7a8b4-463">**Systemverfügbarkeit**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-463">**System Availability**.</span></span> <span data-ttu-id="7a8b4-464">Wählen Sie **HA** (Hohe Verfügbarkeit).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-464">Select **HA**.</span></span>
- <span data-ttu-id="7a8b4-465">**Administratorbenutzername und Administratorkennwort**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-465">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="7a8b4-466">Erstellen Sie einen neuen Benutzer, der verwendet werden kann, um sich am Computer anzumelden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-466">Create a new user that can be used to sign in to the machine.</span></span>
- <span data-ttu-id="7a8b4-467">**Subnetz-ID**. Geben Sie die ID des Subnetzes ein, das Sie während der Bereitstellung der ASCS/SCS-Vorlage verwendet haben, oder die ID des Subnetzes, das als Teil der ASCS/SCS-Vorlagenbereitstellung erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-467">**Subnet Id**. Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>

#### <a name="application-servers-template"></a> <span data-ttu-id="7a8b4-468">Anwendungsservervorlage</span><span class="sxs-lookup"><span data-stu-id="7a8b4-468">Application servers template</span></span>

<span data-ttu-id="7a8b4-469">Die Anwendungsservervorlage stellt zwei oder mehr virtuelle Computer bereit, die als SAP-Anwendungsserverinstanzen für ein SAP-System verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-469">The application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="7a8b4-470">Wenn Sie z.B. eine ASCS/SCS-Vorlage für fünf SAP-Systeme bereitstellen, müssen Sie diese Vorlage fünfmal bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-470">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="7a8b4-471">Geben Sie in der [Anwendungsserver-Multi-SID-Vorlage][sap-templates-3-tier-multisid-apps-marketplace-image] Werte für die folgenden Parameter ein, um die Vorlage einzurichten:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-471">To set up the application servers multi-SID template, in the [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image], enter values for the following parameters:</span></span>

  -  <span data-ttu-id="7a8b4-472">**SAP-System-ID**. Geben Sie die SAP-System-ID des SAP-Systems ein, das Sie installieren möchten.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-472">**Sap System Id**. Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="7a8b4-473">Die ID wird als Präfix für die Ressourcen verwendet, die bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-473">The ID will be used as a prefix for the resources that are deployed.</span></span>
  -  <span data-ttu-id="7a8b4-474">**Betriebssystemtyp**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-474">**Os Type**.</span></span> <span data-ttu-id="7a8b4-475">Wählen Sie das Betriebssystem des virtuellen Computers aus.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-475">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="7a8b4-476">**SAP-Systemgröße**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-476">**Sap System Size**.</span></span> <span data-ttu-id="7a8b4-477">Die Anzahl von SAPS, die vom neuen System bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-477">The number of SAPS the new system will provide.</span></span> <span data-ttu-id="7a8b4-478">Wenn Sie nicht sicher sind, wie viele SAPS das System benötigt, wenden Sie sich an den SAP-Technologiepartner oder Systemintegrator.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-478">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="7a8b4-479">**Systemverfügbarkeit**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-479">**System Availability**.</span></span> <span data-ttu-id="7a8b4-480">Wählen Sie **HA** (Hohe Verfügbarkeit).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-480">Select **HA**.</span></span>
  -  <span data-ttu-id="7a8b4-481">**Administratorbenutzername und Administratorkennwort**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-481">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="7a8b4-482">Erstellen Sie einen neuen Benutzer, der verwendet werden kann, um sich am Computer anzumelden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-482">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="7a8b4-483">**Subnetz-ID**. Geben Sie die ID des Subnetzes ein, das Sie während der Bereitstellung der ASCS/SCS-Vorlage verwendet haben, oder die ID des Subnetzes, das als Teil der ASCS/SCS-Vorlagenbereitstellung erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-483">**Subnet Id**. Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>


### <a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> <span data-ttu-id="7a8b4-484">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="7a8b4-484">Azure virtual network</span></span>
<span data-ttu-id="7a8b4-485">Bei unserem Beispiel ist der Adressbereich des virtuellen Azure-Netzwerks 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-485">In our example, the address space of the Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="7a8b4-486">Es gibt ein Subnetz mit dem Namen **Subnet** und dem Adressbereich 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-486">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="7a8b4-487">Alle virtuellen Computer und internen Load Balancer werden in diesem virtuellen Netzwerk bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-487">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a8b4-488">Nehmen Sie keine Änderungen an den Netzwerkeinstellungen innerhalb des Gastbetriebssystems vor.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-488">Don't make any changes to the network settings inside the guest operating system.</span></span> <span data-ttu-id="7a8b4-489">Dies schließt IP-Adressen, DNS-Server und Subnetz ein.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-489">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="7a8b4-490">Konfigurieren Sie alle Einstellungen für Ihr Netzwerk in Azure.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-490">Configure all your network settings in Azure.</span></span> <span data-ttu-id="7a8b4-491">Der DHCP-Dienst (Dynamic Host Configuration Protocol) übermittelt diese Einstellungen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-491">The Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> <span data-ttu-id="7a8b4-492">DNS-IP-Adressen</span><span class="sxs-lookup"><span data-stu-id="7a8b4-492">DNS IP addresses</span></span>

<span data-ttu-id="7a8b4-493">Führen Sie die folgenden Schritte aus, um die erforderlichen DNS-IP-Adressen festzulegen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-493">To set the required DNS IP addresses, do the following steps.</span></span>

1. <span data-ttu-id="7a8b4-494">Stellen Sie im Azure-Portal auf dem Blatt **DNS-Server** sicher, dass die Option **DNS-Server** für Ihr virtuelles Netzwerk auf **Custom DNS** (Benutzerdefiniertes DNS) festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-494">In the Azure portal, on the **DNS servers** blade, make sure that your virtual network **DNS servers** option is set to **Custom DNS**.</span></span>
2. <span data-ttu-id="7a8b4-495">Wählen Sie die Einstellungen basierend auf dem Typ des Netzwerks aus.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-495">Select your settings based on the type of network you have.</span></span> <span data-ttu-id="7a8b4-496">Weitere Informationen finden Sie in den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-496">For more information, see the following resources:</span></span>
   * <span data-ttu-id="7a8b4-497">[Konnektivität des Unternehmensnetzwerks (standortübergreifend)][planning-guide-2.2]: Fügen Sie die IP-Adressen der lokalen DNS-Server hinzu.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-497">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add the IP addresses of the on-premises DNS servers.</span></span>  
   <span data-ttu-id="7a8b4-498">Sie können lokale DNS-Server auf die virtuellen Computer erweitern, die in Azure ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-498">You can extend on-premises DNS servers to the virtual machines that are running in Azure.</span></span> <span data-ttu-id="7a8b4-499">In diesem Szenario können Sie die IP-Adressen der virtuellen Azure-Computer hinzufügen, auf denen den DNS-Dienst ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-499">In that scenario, you can add the IP addresses of the Azure virtual machines on which you run the DNS service.</span></span>
   * <span data-ttu-id="7a8b4-500">Für in Azure isolierte Bereitstellungen Stellen Sie eine zusätzliche VM in der gleichen Virtual Network-Instanz bereit, die auch als DNS-Server fungiert.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-500">For deployments isolated in Azure: Deploy an additional virtual machine in the same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="7a8b4-501">Fügen Sie die IP-Adressen der virtuellen Azure-Computer hinzu, die Sie zum Ausführen des DNS-Diensts eingerichtet haben.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-501">Add the IP addresses of the Azure virtual machines that you've set up to run DNS service.</span></span>

   ![Abbildung 12: Konfigurieren von DNS-Servern für Azure Virtual Network][sap-ha-guide-figure-3001]

   <span data-ttu-id="7a8b4-503">_**Abbildung 12:** Konfigurieren von DNS-Servern für Azure Virtual Network_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-503">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

   > [!NOTE]
   > <span data-ttu-id="7a8b4-504">Wenn Sie die IP-Adressen der DNS-Server ändern, müssen Sie die virtuellen Azure-Computer neu starten, damit die Änderung übernommen und an die neuen DNS-Server übertragen wird.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-504">If you change the IP addresses of the DNS servers, you need to restart the Azure virtual machines to apply the change and propagate the new DNS servers.</span></span>
   >
   >

<span data-ttu-id="7a8b4-505">In unserem Beispiel ist der DNS-Dienst auf den folgenden virtuellen Windows-Computern installiert und konfiguriert:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-505">In our example, the DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="7a8b4-506">Rolle für virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="7a8b4-506">Virtual machine role</span></span> | <span data-ttu-id="7a8b4-507">Hostname für virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="7a8b4-507">Virtual machine host name</span></span> | <span data-ttu-id="7a8b4-508">Name der Netzwerkkarte</span><span class="sxs-lookup"><span data-stu-id="7a8b4-508">Network card name</span></span> | <span data-ttu-id="7a8b4-509">Statische IP-Adresse</span><span class="sxs-lookup"><span data-stu-id="7a8b4-509">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7a8b4-510">Erster DNS-Server</span><span class="sxs-lookup"><span data-stu-id="7a8b4-510">First DNS server</span></span> |<span data-ttu-id="7a8b4-511">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="7a8b4-511">domcontr-0</span></span> |<span data-ttu-id="7a8b4-512">pr1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="7a8b4-512">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="7a8b4-513">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="7a8b4-513">10.0.0.10</span></span> |
| <span data-ttu-id="7a8b4-514">Zweiter DNS-Server</span><span class="sxs-lookup"><span data-stu-id="7a8b4-514">Second DNS server</span></span> |<span data-ttu-id="7a8b4-515">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="7a8b4-515">domcontr-1</span></span> |<span data-ttu-id="7a8b4-516">pr1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="7a8b4-516">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="7a8b4-517">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="7a8b4-517">10.0.0.11</span></span> |

### <a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> <span data-ttu-id="7a8b4-518">Hostnamen und statische IP-Adressen für die SAP ASCS/SCS-Clusterinstanz und -DBMS-Clusterinstanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-518">Host names and static IP addresses for the SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="7a8b4-519">Für lokale Bereitstellungen benötigen Sie diese reservierten Hostnamen und IP-Adressen:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-519">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="7a8b4-520">Rolle des virtuellen Hosts</span><span class="sxs-lookup"><span data-stu-id="7a8b4-520">Virtual host name role</span></span> | <span data-ttu-id="7a8b4-521">Name des virtuellen Hosts</span><span class="sxs-lookup"><span data-stu-id="7a8b4-521">Virtual host name</span></span> | <span data-ttu-id="7a8b4-522">Virtuelle statische IP-Adresse</span><span class="sxs-lookup"><span data-stu-id="7a8b4-522">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7a8b4-523">SAP ASCS/SCS – erster virtueller Host im Cluster (für die Clusterverwaltung)</span><span class="sxs-lookup"><span data-stu-id="7a8b4-523">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="7a8b4-524">pr1-ascs-vir</span><span class="sxs-lookup"><span data-stu-id="7a8b4-524">pr1-ascs-vir</span></span> |<span data-ttu-id="7a8b4-525">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="7a8b4-525">10.0.0.42</span></span> |
| <span data-ttu-id="7a8b4-526">SAP ASCS/SCS-Instanz – virtueller Hostname</span><span class="sxs-lookup"><span data-stu-id="7a8b4-526">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="7a8b4-527">pr1-ascs-sap</span><span class="sxs-lookup"><span data-stu-id="7a8b4-527">pr1-ascs-sap</span></span> |<span data-ttu-id="7a8b4-528">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="7a8b4-528">10.0.0.43</span></span> |
| <span data-ttu-id="7a8b4-529">SAP-DBMS – zweiter virtueller Host im Cluster (Clusterverwaltung)</span><span class="sxs-lookup"><span data-stu-id="7a8b4-529">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="7a8b4-530">pr1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="7a8b4-530">pr1-dbms-vir</span></span> |<span data-ttu-id="7a8b4-531">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="7a8b4-531">10.0.0.32</span></span> |

<span data-ttu-id="7a8b4-532">Bei der Erstellung des Clusters erstellen Sie die virtuellen Hostnamen **pr1-ascs-vir** und **pr1-dbms-vir** und die zugehörigen IP-Adressen, die den Cluster selbst verwalten.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-532">When you create the cluster, create the virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and the associated IP addresses that manage the cluster itself.</span></span> <span data-ttu-id="7a8b4-533">Informationen zur Vorgehensweise finden Sie unter [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1] (Erfassen von Clusterknoten in einer Clusterkonfiguration).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-533">For information about how to do this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="7a8b4-534">Sie können die anderen beiden virtuellen Hostnamen **pr1-ascs-sap** und **pr1-dbms-sap** und die zugeordneten IP-Adressen manuell auf dem DNS-Server erstellen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-534">You can manually create the other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and the associated IP addresses, on the DNS server.</span></span> <span data-ttu-id="7a8b4-535">Die SAP ASCS/SCS-Clusterinstanz und die DBMS-Clusterinstanz verwenden diese Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-535">The clustered SAP ASCS/SCS instance and the clustered DBMS instance use these resources.</span></span> <span data-ttu-id="7a8b4-536">Informationen zur Vorgehensweise finden Sie unter [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1] (Erstellen eines virtuellen Hostnamens für die SAP ASCS/SCS-Clusterinstanz).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-536">For information about how to do this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> <span data-ttu-id="7a8b4-537">Festlegen der statischen IP-Adressen für die beiden virtuellen SAP-Computer</span><span class="sxs-lookup"><span data-stu-id="7a8b4-537">Set static IP addresses for the SAP virtual machines</span></span>
<span data-ttu-id="7a8b4-538">Nach der Bereitstellung der virtuellen Computer für Ihren Cluster müssen Sie statische IP-Adressen für alle virtuellen Computer festlegen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-538">After you deploy the virtual machines to use in your cluster, you need to set static IP addresses for all virtual machines.</span></span> <span data-ttu-id="7a8b4-539">Sie führen diesen Schritt in der Azure Virtual Network-Konfiguration und nicht im Gastbetriebssystem aus.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-539">Do this in the Azure Virtual Network configuration, and not in the guest operating system.</span></span>

1. <span data-ttu-id="7a8b4-540">Wählen Sie im Azure-Portal **Ressourcengruppe** > **Netzwerkkarte** > **Einstellungen** > **IP-Adresse**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-540">In the Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2. <span data-ttu-id="7a8b4-541">Wählen Sie auf dem Blatt **IP-Adressen** unter **Zuweisung** die Option **Statisch**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-541">On the **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="7a8b4-542">Geben Sie im Feld **IP-Adresse** die IP-Adresse ein, die Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-542">In the **IP address** box, enter the IP address that you want to use.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7a8b4-543">Wenn Sie die IP-Adresse der Netzwerkkarte ändern, müssen Sie die virtuellen Azure-Computer neu starten, um die Änderung zu übernehmen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-543">If you change the IP address of the network card, you need to restart the Azure virtual machines to apply the change.</span></span>  
   >
   >

   ![Abbildung 13: Festlegen der statischen IP-Adressen für die Netzwerkkarten der einzelnen VMs][sap-ha-guide-figure-3002]

   <span data-ttu-id="7a8b4-545">_**Abbildung 13:** Festlegen der statischen IP-Adressen für die Netzwerkkarten der einzelnen VMs_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-545">_**Figure 13:** Set static IP addresses for the network card of each virtual machine_</span></span>

   <span data-ttu-id="7a8b4-546">Wiederholen Sie diesen Schritt für alle Netzwerkschnittstellen, d.h. für alle virtuellen Computer, einschließlich der virtuellen Computer, die Sie für den Active Directory-/DNS-Dienst verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-546">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want to use for your Active Directory/DNS service.</span></span>

<span data-ttu-id="7a8b4-547">In unserem Beispiel verwenden wir die folgenden virtuellen Computer und statischen IP-Adressen:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-547">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="7a8b4-548">Rolle für virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="7a8b4-548">Virtual machine role</span></span> | <span data-ttu-id="7a8b4-549">Hostname für virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="7a8b4-549">Virtual machine host name</span></span> | <span data-ttu-id="7a8b4-550">Name der Netzwerkkarte</span><span class="sxs-lookup"><span data-stu-id="7a8b4-550">Network card name</span></span> | <span data-ttu-id="7a8b4-551">Statische IP-Adresse</span><span class="sxs-lookup"><span data-stu-id="7a8b4-551">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7a8b4-552">Erste SAP-Anwendungsserverinstanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-552">First SAP Application Server instance</span></span> |<span data-ttu-id="7a8b4-553">pr1-di-0</span><span class="sxs-lookup"><span data-stu-id="7a8b4-553">pr1-di-0</span></span> |<span data-ttu-id="7a8b4-554">pr1-nic-di-0</span><span class="sxs-lookup"><span data-stu-id="7a8b4-554">pr1-nic-di-0</span></span> |<span data-ttu-id="7a8b4-555">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="7a8b4-555">10.0.0.50</span></span> |
| <span data-ttu-id="7a8b4-556">Zweite SAP-Anwendungsserverinstanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-556">Second SAP Application Server instance</span></span> |<span data-ttu-id="7a8b4-557">pr1-di-1</span><span class="sxs-lookup"><span data-stu-id="7a8b4-557">pr1-di-1</span></span> |<span data-ttu-id="7a8b4-558">pr1-nic-di-1</span><span class="sxs-lookup"><span data-stu-id="7a8b4-558">pr1-nic-di-1</span></span> |<span data-ttu-id="7a8b4-559">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="7a8b4-559">10.0.0.51</span></span> |
| <span data-ttu-id="7a8b4-560">...</span><span class="sxs-lookup"><span data-stu-id="7a8b4-560">...</span></span> |<span data-ttu-id="7a8b4-561">...</span><span class="sxs-lookup"><span data-stu-id="7a8b4-561">...</span></span> |<span data-ttu-id="7a8b4-562">...</span><span class="sxs-lookup"><span data-stu-id="7a8b4-562">...</span></span> |<span data-ttu-id="7a8b4-563">...</span><span class="sxs-lookup"><span data-stu-id="7a8b4-563">...</span></span> |
| <span data-ttu-id="7a8b4-564">Letzte SAP-Anwendungsserverinstanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-564">Last SAP Application Server instance</span></span> |<span data-ttu-id="7a8b4-565">pr1-di-5</span><span class="sxs-lookup"><span data-stu-id="7a8b4-565">pr1-di-5</span></span> |<span data-ttu-id="7a8b4-566">pr1-nic-di-5</span><span class="sxs-lookup"><span data-stu-id="7a8b4-566">pr1-nic-di-5</span></span> |<span data-ttu-id="7a8b4-567">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="7a8b4-567">10.0.0.55</span></span> |
| <span data-ttu-id="7a8b4-568">Erster Clusterknoten für die ASCS/SCS-Instanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-568">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="7a8b4-569">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="7a8b4-569">pr1-ascs-0</span></span> |<span data-ttu-id="7a8b4-570">pr1-nic-ascs-0</span><span class="sxs-lookup"><span data-stu-id="7a8b4-570">pr1-nic-ascs-0</span></span> |<span data-ttu-id="7a8b4-571">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="7a8b4-571">10.0.0.40</span></span> |
| <span data-ttu-id="7a8b4-572">Zweiter Clusterknoten für die ASCS/SCS-Instanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-572">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="7a8b4-573">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="7a8b4-573">pr1-ascs-1</span></span> |<span data-ttu-id="7a8b4-574">pr1-nic-ascs-1</span><span class="sxs-lookup"><span data-stu-id="7a8b4-574">pr1-nic-ascs-1</span></span> |<span data-ttu-id="7a8b4-575">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="7a8b4-575">10.0.0.41</span></span> |
| <span data-ttu-id="7a8b4-576">Erster Clusterknoten für die DBMS-Instanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-576">First cluster node for DBMS instance</span></span> |<span data-ttu-id="7a8b4-577">pr1-db-0</span><span class="sxs-lookup"><span data-stu-id="7a8b4-577">pr1-db-0</span></span> |<span data-ttu-id="7a8b4-578">pr1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="7a8b4-578">pr1-nic-db-0</span></span> |<span data-ttu-id="7a8b4-579">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="7a8b4-579">10.0.0.30</span></span> |
| <span data-ttu-id="7a8b4-580">Zweiter Clusterknoten für die DBMS-Instanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-580">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="7a8b4-581">pr1-db-1</span><span class="sxs-lookup"><span data-stu-id="7a8b4-581">pr1-db-1</span></span> |<span data-ttu-id="7a8b4-582">pr1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="7a8b4-582">pr1-nic-db-1</span></span> |<span data-ttu-id="7a8b4-583">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="7a8b4-583">10.0.0.31</span></span> |

### <a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> <span data-ttu-id="7a8b4-584">Festlegen der statischen IP-Adresse für den internen Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="7a8b4-584">Set a static IP address for the Azure internal load balancer</span></span>

<span data-ttu-id="7a8b4-585">Die Azure Resource Manager-Vorlage für SAP erstellt einen internen Azure Load Balancer, der für den Cluster der SAP ASCS/SCS-Instanz und den DBMS-Cluster verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-585">The SAP Azure Resource Manager template creates an Azure internal load balancer that is used for the SAP ASCS/SCS instance cluster and the DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a8b4-586">Die IP-Adresse des virtuellen Hostnamens von SAP ASCS/SCS ist mit der IP-Adresse des internen Load Balancers **pr1-lb-ascs** für die SAP ASCS/SCS-Instanz identisch.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-586">The IP address of the virtual host name of the SAP ASCS/SCS is the same as the IP address of the SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="7a8b4-587">Die IP-Adresse des virtuellen Namens des DBMS ist mit der IP-Adresse des internen Load Balancers **pr1-lb-dbms** für das DBMS identisch.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-587">The IP address of the virtual name of the DBMS is the same as the IP address of the DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="7a8b4-588">So legen Sie eine statische IP-Adresse für den internen Azure Load Balancer fest</span><span class="sxs-lookup"><span data-stu-id="7a8b4-588">To set a static IP address for the Azure internal load balancer:</span></span>

1. <span data-ttu-id="7a8b4-589">Bei der ersten Bereitstellung wird die IP-Adresse des internen Load Balancers auf **Dynamisch** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-589">The initial deployment sets the internal load balancer IP address to **Dynamic**.</span></span> <span data-ttu-id="7a8b4-590">Wählen Sie im Azure-Portal auf dem Blatt **IP-Adressen** unter **Zuweisung** die Option **Statisch**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-590">In the Azure portal, on the **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2. <span data-ttu-id="7a8b4-591">Legen Sie die IP-Adresse des internen Load Balancers **pr1-lb-ascs** auf die IP-Adresse des virtuellen Hostnamens der SAP ASCS/SCS-Instanz fest.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-591">Set the IP address of the internal load balancer **pr1-lb-ascs** to the IP address of the virtual host name of the SAP ASCS/SCS instance.</span></span>
3. <span data-ttu-id="7a8b4-592">Legen Sie die IP-Adresse des internen Load Balancers **pr1-lb-dbms** auf die IP-Adresse des virtuellen Hostnamens der DBMS-Instanz fest.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-592">Set the IP address of the internal load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

   ![Abbildung 14: Festlegen der statischen IP-Adressen für den internen Lastenausgleich der SAP ASCS/SCS-Instanz][sap-ha-guide-figure-3003]

   <span data-ttu-id="7a8b4-594">_**Abbildung 14:** Festlegen der statischen IP-Adressen für den internen Lastenausgleich der SAP ASCS/SCS-Instanz_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-594">_**Figure 14:** Set static IP addresses for the internal load balancer for the SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="7a8b4-595">In unserem Beispiel verwenden wir zwei interne Azure Load Balancer mit diesen statischen IP-Adressen:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-595">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="7a8b4-596">Rolle des internen Azure Load Balancers</span><span class="sxs-lookup"><span data-stu-id="7a8b4-596">Azure internal load balancer role</span></span> | <span data-ttu-id="7a8b4-597">Name des internen Azure Load Balancers</span><span class="sxs-lookup"><span data-stu-id="7a8b4-597">Azure internal load balancer name</span></span> | <span data-ttu-id="7a8b4-598">Statische IP-Adresse</span><span class="sxs-lookup"><span data-stu-id="7a8b4-598">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7a8b4-599">Interner Load Balancer für die SAP ASCS/SCS-Instanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-599">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="7a8b4-600">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="7a8b4-600">pr1-lb-ascs</span></span> |<span data-ttu-id="7a8b4-601">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="7a8b4-601">10.0.0.43</span></span> |
| <span data-ttu-id="7a8b4-602">Interner Load Balancer für das SAP-DBMS</span><span class="sxs-lookup"><span data-stu-id="7a8b4-602">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="7a8b4-603">pr1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="7a8b4-603">pr1-lb-dbms</span></span> |<span data-ttu-id="7a8b4-604">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="7a8b4-604">10.0.0.33</span></span> |


### <a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> <span data-ttu-id="7a8b4-605">Standardregeln für den ASCS/SCS-Lastenausgleich für den internen Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="7a8b4-605">Default ASCS/SCS load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="7a8b4-606">Die Azure Resource Manager-Vorlage für SAP erstellt alle erforderlichen Ports:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-606">The SAP Azure Resource Manager template creates the ports you need:</span></span>
* <span data-ttu-id="7a8b4-607">Eine ABAP ASCS-Instanz mit der Standardinstanznummer **00**</span><span class="sxs-lookup"><span data-stu-id="7a8b4-607">An ABAP ASCS instance, with the default instance number **00**</span></span>
* <span data-ttu-id="7a8b4-608">Eine Java SCS-Instanz mit der Standardinstanznummer **01**</span><span class="sxs-lookup"><span data-stu-id="7a8b4-608">A Java SCS instance, with the default instance number **01**</span></span>

<span data-ttu-id="7a8b4-609">Wenn Sie Ihre SAP ASCS/SCS-Instanz installieren, müssen Sie die Standardinstanznummer **00** für Ihre ABAP ASCS-Instanz und die Standardinstanznummer **01** für Ihre Java SCS-Instanz verwenden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-609">When you install your SAP ASCS/SCS instance, you must use the default instance number **00** for your ABAP ASCS instance and the default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="7a8b4-610">Als Nächstes erstellen Sie erforderliche Endpunkte für den internen Lastenausgleich für die SAP NetWeaver-Ports.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-610">Next, create required internal load balancing endpoints for the SAP NetWeaver ports.</span></span>

<span data-ttu-id="7a8b4-611">Für die Erstellung von erforderlichen Endpunkten für den internen Lastenausgleich erstellen Sie zuerst diese Endpunkte für den internen Lastenausgleich für die SAP NetWeaver ABAP ASCS-Ports:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-611">To create required internal load balancing endpoints, first, create these load balancing endpoints for the SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="7a8b4-612">Dienst/Name der Lastenausgleichsregel</span><span class="sxs-lookup"><span data-stu-id="7a8b4-612">Service/load balancing rule name</span></span> | <span data-ttu-id="7a8b4-613">Standardportnummern</span><span class="sxs-lookup"><span data-stu-id="7a8b4-613">Default port numbers</span></span> | <span data-ttu-id="7a8b4-614">Konkrete Ports für (ASCS-Instanz mit Instanznummer 00) (ERS mit 10)</span><span class="sxs-lookup"><span data-stu-id="7a8b4-614">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7a8b4-615">Enqueue-Server/ *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-615">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="7a8b4-616">32<*Instanznummer*></span><span class="sxs-lookup"><span data-stu-id="7a8b4-616">32<*InstanceNumber*></span></span> |<span data-ttu-id="7a8b4-617">3200</span><span class="sxs-lookup"><span data-stu-id="7a8b4-617">3200</span></span> |
| <span data-ttu-id="7a8b4-618">ABAP-Message-Server/ *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-618">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="7a8b4-619">36<*Instanznummer*></span><span class="sxs-lookup"><span data-stu-id="7a8b4-619">36<*InstanceNumber*></span></span> |<span data-ttu-id="7a8b4-620">3600</span><span class="sxs-lookup"><span data-stu-id="7a8b4-620">3600</span></span> |
| <span data-ttu-id="7a8b4-621">Interne ABAP-Nachricht/ *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-621">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="7a8b4-622">39<*Instanznummer*></span><span class="sxs-lookup"><span data-stu-id="7a8b4-622">39<*InstanceNumber*></span></span> |<span data-ttu-id="7a8b4-623">3900</span><span class="sxs-lookup"><span data-stu-id="7a8b4-623">3900</span></span> |
| <span data-ttu-id="7a8b4-624">Message-Server HTTP/ *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-624">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="7a8b4-625">81<*Instanznummer*></span><span class="sxs-lookup"><span data-stu-id="7a8b4-625">81<*InstanceNumber*></span></span> |<span data-ttu-id="7a8b4-626">8100</span><span class="sxs-lookup"><span data-stu-id="7a8b4-626">8100</span></span> |
| <span data-ttu-id="7a8b4-627">SAP Start Service ASCS HTTP/ *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-627">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="7a8b4-628">5<*Instanznummer*>13</span><span class="sxs-lookup"><span data-stu-id="7a8b4-628">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="7a8b4-629">50013</span><span class="sxs-lookup"><span data-stu-id="7a8b4-629">50013</span></span> |
| <span data-ttu-id="7a8b4-630">SAP Start Service ASCS HTTPS/ *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-630">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="7a8b4-631">5<*Instanznummer*>14</span><span class="sxs-lookup"><span data-stu-id="7a8b4-631">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="7a8b4-632">50014</span><span class="sxs-lookup"><span data-stu-id="7a8b4-632">50014</span></span> |
| <span data-ttu-id="7a8b4-633">Enqueue-Replikation/ *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-633">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="7a8b4-634">5<*Instanznummer*>16</span><span class="sxs-lookup"><span data-stu-id="7a8b4-634">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="7a8b4-635">50016</span><span class="sxs-lookup"><span data-stu-id="7a8b4-635">50016</span></span> |
| <span data-ttu-id="7a8b4-636">SAP Start Service ERS HTTP *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-636">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="7a8b4-637">5<*Instanznummer*>13</span><span class="sxs-lookup"><span data-stu-id="7a8b4-637">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="7a8b4-638">51013</span><span class="sxs-lookup"><span data-stu-id="7a8b4-638">51013</span></span> |
| <span data-ttu-id="7a8b4-639">SAP Start Service ERS HTTP *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-639">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="7a8b4-640">5<*Instanznummer*>14</span><span class="sxs-lookup"><span data-stu-id="7a8b4-640">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="7a8b4-641">51014</span><span class="sxs-lookup"><span data-stu-id="7a8b4-641">51014</span></span> |
| <span data-ttu-id="7a8b4-642">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-642">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="7a8b4-643">5985</span><span class="sxs-lookup"><span data-stu-id="7a8b4-643">5985</span></span> |
| <span data-ttu-id="7a8b4-644">Dateifreigabe *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-644">File Share *Lbrule445*</span></span> | |<span data-ttu-id="7a8b4-645">445</span><span class="sxs-lookup"><span data-stu-id="7a8b4-645">445</span></span> |

<span data-ttu-id="7a8b4-646">_**Tabelle 1:** Portnummern der SAP NetWeaver ABAP ASCS-Instanzen_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-646">_**Table 1:** Port numbers of the SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="7a8b4-647">Erstellen Sie anschließend diese Endpunkte für den Lastenausgleich für die SAP NetWeaver Java SCS-Ports:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-647">Then, create these load balancing endpoints for the SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="7a8b4-648">Dienst/Name der Lastenausgleichsregel</span><span class="sxs-lookup"><span data-stu-id="7a8b4-648">Service/load balancing rule name</span></span> | <span data-ttu-id="7a8b4-649">Standardportnummern</span><span class="sxs-lookup"><span data-stu-id="7a8b4-649">Default port numbers</span></span> | <span data-ttu-id="7a8b4-650">Konkrete Ports für (SCS-Instanz mit Instanznummer 01) (ERS mit 11)</span><span class="sxs-lookup"><span data-stu-id="7a8b4-650">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7a8b4-651">Enqueue-Server/ *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-651">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="7a8b4-652">32<*Instanznummer*></span><span class="sxs-lookup"><span data-stu-id="7a8b4-652">32<*InstanceNumber*></span></span> |<span data-ttu-id="7a8b4-653">3201</span><span class="sxs-lookup"><span data-stu-id="7a8b4-653">3201</span></span> |
| <span data-ttu-id="7a8b4-654">Gateway-Server/ *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-654">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="7a8b4-655">33<*Instanznummer*></span><span class="sxs-lookup"><span data-stu-id="7a8b4-655">33<*InstanceNumber*></span></span> |<span data-ttu-id="7a8b4-656">3301</span><span class="sxs-lookup"><span data-stu-id="7a8b4-656">3301</span></span> |
| <span data-ttu-id="7a8b4-657">Java-Message-Server/ *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-657">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="7a8b4-658">39<*Instanznummer*></span><span class="sxs-lookup"><span data-stu-id="7a8b4-658">39<*InstanceNumber*></span></span> |<span data-ttu-id="7a8b4-659">3901</span><span class="sxs-lookup"><span data-stu-id="7a8b4-659">3901</span></span> |
| <span data-ttu-id="7a8b4-660">Message-Server-HTTP/ *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-660">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="7a8b4-661">81<*Instanznummer*></span><span class="sxs-lookup"><span data-stu-id="7a8b4-661">81<*InstanceNumber*></span></span> |<span data-ttu-id="7a8b4-662">8101</span><span class="sxs-lookup"><span data-stu-id="7a8b4-662">8101</span></span> |
| <span data-ttu-id="7a8b4-663">SAP Start Service SCS HTTP/ *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-663">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="7a8b4-664">5<*Instanznummer*>13</span><span class="sxs-lookup"><span data-stu-id="7a8b4-664">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="7a8b4-665">50113</span><span class="sxs-lookup"><span data-stu-id="7a8b4-665">50113</span></span> |
| <span data-ttu-id="7a8b4-666">SAP Start Service SCS HTTPS/ *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-666">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="7a8b4-667">5<*Instanznummer*>14</span><span class="sxs-lookup"><span data-stu-id="7a8b4-667">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="7a8b4-668">50114</span><span class="sxs-lookup"><span data-stu-id="7a8b4-668">50114</span></span> |
| <span data-ttu-id="7a8b4-669">Enqueue-Replikation/ *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-669">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="7a8b4-670">5<*Instanznummer*>16</span><span class="sxs-lookup"><span data-stu-id="7a8b4-670">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="7a8b4-671">50116</span><span class="sxs-lookup"><span data-stu-id="7a8b4-671">50116</span></span> |
| <span data-ttu-id="7a8b4-672">SAP Start Service ERS HTTP *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-672">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="7a8b4-673">5<*Instanznummer*>13</span><span class="sxs-lookup"><span data-stu-id="7a8b4-673">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="7a8b4-674">51113</span><span class="sxs-lookup"><span data-stu-id="7a8b4-674">51113</span></span> |
| <span data-ttu-id="7a8b4-675">SAP Start Service ERS HTTP *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-675">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="7a8b4-676">5<*Instanznummer*>14</span><span class="sxs-lookup"><span data-stu-id="7a8b4-676">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="7a8b4-677">51114</span><span class="sxs-lookup"><span data-stu-id="7a8b4-677">51114</span></span> |
| <span data-ttu-id="7a8b4-678">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-678">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="7a8b4-679">5985</span><span class="sxs-lookup"><span data-stu-id="7a8b4-679">5985</span></span> |
| <span data-ttu-id="7a8b4-680">Dateifreigabe *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="7a8b4-680">File Share *Lbrule445*</span></span> | |<span data-ttu-id="7a8b4-681">445</span><span class="sxs-lookup"><span data-stu-id="7a8b4-681">445</span></span> |

<span data-ttu-id="7a8b4-682">_**Tabelle 2:** Portnummern der SAP NetWeaver Java SCS-Instanzen_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-682">_**Table 2:** Port numbers of the SAP NetWeaver Java SCS instances_</span></span>

![Abbildung 15: Standardregeln für den ASCS/SCS-Lastenausgleich für den internen Azure Load Balancer][sap-ha-guide-figure-3004]

<span data-ttu-id="7a8b4-684">_**Abbildung 15:** Standardregeln für den ASCS/SCS-Lastenausgleich für den internen Azure Load Balancer_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-684">_**Figure 15:** Default ASCS/SCS load balancing rules for the Azure internal load balancer_</span></span>

<span data-ttu-id="7a8b4-685">Legen Sie die IP-Adresse des Lastenausgleichs **pr1-lb-dbms** auf die IP-Adresse des virtuellen Hostnamens der DBMS-Instanz fest.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-685">Set the IP address of the load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

### <a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> <span data-ttu-id="7a8b4-686">Ändern der Standardregeln für den ASCS/SCS-Lastenausgleich für den internen Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="7a8b4-686">Change the ASCS/SCS default load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="7a8b4-687">Wenn Sie andere Nummern für die SAP ASCS- oder SCS-Instanzen verwenden möchten, müssen Sie die Namen und Werte der entsprechenden Ports in der Standardeinstellung ändern.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-687">If you want to use different numbers for the SAP ASCS or SCS instances, you must change the names and values of their ports from default values.</span></span>

1. <span data-ttu-id="7a8b4-688">Wählen Sie im Azure-Portal **<*SID*>-lb-ascs load balancer** > **Lastenausgleichsregeln**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-688">In the Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2. <span data-ttu-id="7a8b4-689">Ändern Sie für alle zur SAP ASCS- oder SCS-Instanz gehörenden Lastenausgleichsregeln die folgenden Werte:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-689">For all load balancing rules that belong to the SAP ASCS or SCS instance, change these values:</span></span>

   * <span data-ttu-id="7a8b4-690">NAME</span><span class="sxs-lookup"><span data-stu-id="7a8b4-690">Name</span></span>
   * <span data-ttu-id="7a8b4-691">Port</span><span class="sxs-lookup"><span data-stu-id="7a8b4-691">Port</span></span>
   * <span data-ttu-id="7a8b4-692">Back-End-Port</span><span class="sxs-lookup"><span data-stu-id="7a8b4-692">Back-end port</span></span>

   <span data-ttu-id="7a8b4-693">Wenn Sie z.B. die Standardnummer der ASCS-Instanz von 00 in 31 ändern möchten, müssen Sie die Änderungen für alle in Tabelle 1 aufgeführten Ports durchführen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-693">For example, if you want to change the default ASCS instance number from 00 to 31, you need to make the changes for all ports listed in Table 1.</span></span>

   <span data-ttu-id="7a8b4-694">Dies ist ein Beispiel einer Änderung für den Port *lbrule3200*.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-694">Here's an example of an update for port *lbrule3200*.</span></span>

   ![Abbildung 16: Ändern der Standardregeln für den ASCS/SCS-Lastenausgleich für den internen Azure Load Balancer][sap-ha-guide-figure-3005]

   <span data-ttu-id="7a8b4-696">_**Abbildung 16:** Ändern der Standardregeln für den ASCS/SCS-Lastenausgleich für den internen Azure Load Balancer_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-696">_**Figure 16:** Change the ASCS/SCS default load balancing rules for the Azure internal load balancer_</span></span>

### <a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> <span data-ttu-id="7a8b4-697">Hinzufügen virtueller Windows-Computer zur Domäne</span><span class="sxs-lookup"><span data-stu-id="7a8b4-697">Add Windows virtual machines to the domain</span></span>

<span data-ttu-id="7a8b4-698">Nachdem Sie den virtuellen Computern eine statische IP-Adresse zugewiesen haben, fügen Sie die virtuellen Computer der Domäne hinzu.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-698">After you assign a static IP address to the virtual machines, add the virtual machines to the domain.</span></span>

![Abbildung 17: Hinzufügen einer VM zu einer Domäne][sap-ha-guide-figure-3006]

<span data-ttu-id="7a8b4-700">_**Abbildung 17:** Hinzufügen einer VM zu einer Domäne_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-700">_**Figure 17:** Add a virtual machine to a domain_</span></span>

### <a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> <span data-ttu-id="7a8b4-701">Hinzufügen von Registrierungseinträgen auf beiden Clusterknoten für eine SAP ASCS/SCS-Instanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-701">Add registry entries on both cluster nodes of the SAP ASCS/SCS instance</span></span>

<span data-ttu-id="7a8b4-702">Der Azure Load Balancer verfügt über einen internen Load Balancer, der Verbindungen schließt, wenn sich diese für einen festgelegten Zeitraum im Leerlauf befinden (Leerlaufzeitlimit).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-702">Azure Load Balancer has an internal load balancer that closes connections when the connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="7a8b4-703">SAP-Workprozesse öffnen in Dialoginstanzen Verbindungen mit dem SAP-Enqueue-Prozess, sobald die erste Enqueue-/Dequeue-Anforderung gesendet werden muss.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-703">SAP work processes in dialog instances open connections to the SAP enqueue process as soon as the first enqueue/dequeue request needs to be sent.</span></span> <span data-ttu-id="7a8b4-704">Diese Verbindungen bleiben in der Regel bestehen, bis der Workprozess oder Enqueue-Prozess neu gestartet wird.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-704">These connections usually remain established until the work process or the enqueue process restarts.</span></span> <span data-ttu-id="7a8b4-705">Wenn sich die Verbindung für einen festgelegten Zeitraum im Leerlauf befindet, schließt der interne Azure Load Balancer aber die Verbindungen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-705">However, if the connection is idle for a set period of time, the Azure internal load balancer closes the connections.</span></span> <span data-ttu-id="7a8b4-706">Dies stellt kein Problem dar, da der SAP-Arbeitsprozesses die Verbindung mit dem Enqueue-Prozess erneut herstellt, wenn sie nicht mehr vorhanden sein sollte.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-706">This isn't a problem because the SAP work process reestablishes the connection to the enqueue process if it no longer exists.</span></span> <span data-ttu-id="7a8b4-707">Diese Aktivitäten werden in den Entwickler-Traces von SAP-Prozessen dokumentiert, sie erstellen jedoch eine große Menge an zusätzlichen Inhalten in diesen Traces.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-707">These activities are documented in the developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="7a8b4-708">Daher wird empfohlen, die TCP/IP-Einstellungen `KeepAliveTime` und `KeepAliveInterval` auf beiden Clusterknoten zu ändern.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-708">It's a good idea to change the TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="7a8b4-709">Kombinieren Sie diese Änderungen an den TCP/IP-Parametern mit SAP-Profilparametern, die weiter unten in diesem Artikel beschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-709">Combine these changes in the TCP/IP parameters with SAP profile parameters, described later in the article.</span></span>

<span data-ttu-id="7a8b4-710">Fügen Sie zuerst diese Windows-Registrierungseinträge auf beiden Windows-Clusterknoten für SAP ASCS/SCS hinzu, um die Registrierungseinträge auf beiden Clusterknoten der SAP ASCS/SCS-Instanz hinzuzufügen:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-710">To add registry entries on both cluster nodes of the SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="7a8b4-711">path</span><span class="sxs-lookup"><span data-stu-id="7a8b4-711">Path</span></span> | <span data-ttu-id="7a8b4-712">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="7a8b4-712">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="7a8b4-713">Variablenname</span><span class="sxs-lookup"><span data-stu-id="7a8b4-713">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="7a8b4-714">Variablentyp</span><span class="sxs-lookup"><span data-stu-id="7a8b4-714">Variable type</span></span> |<span data-ttu-id="7a8b4-715">REG_DWORD-Wert (dezimal)</span><span class="sxs-lookup"><span data-stu-id="7a8b4-715">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="7a8b4-716">Wert</span><span class="sxs-lookup"><span data-stu-id="7a8b4-716">Value</span></span> |<span data-ttu-id="7a8b4-717">120000</span><span class="sxs-lookup"><span data-stu-id="7a8b4-717">120000</span></span> |
| <span data-ttu-id="7a8b4-718">Link zur Dokumentation</span><span class="sxs-lookup"><span data-stu-id="7a8b4-718">Link to documentation</span></span> |[https://technet.microsoft.com/library/cc957549.aspx](https://technet.microsoft.com/library/cc957549.aspx) |

<span data-ttu-id="7a8b4-719">_**Tabelle 3:** Ändern des ersten TCP/IP-Parameters_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-719">_**Table 3:** Change the first TCP/IP parameter_</span></span>

<span data-ttu-id="7a8b4-720">Fügen Sie diese Windows-Registrierungseinträge dann auf beiden Windows-Clusterknoten für SAP ASCS/SCS hinzu:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-720">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="7a8b4-721">path</span><span class="sxs-lookup"><span data-stu-id="7a8b4-721">Path</span></span> | <span data-ttu-id="7a8b4-722">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="7a8b4-722">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="7a8b4-723">Variablenname</span><span class="sxs-lookup"><span data-stu-id="7a8b4-723">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="7a8b4-724">Variablentyp</span><span class="sxs-lookup"><span data-stu-id="7a8b4-724">Variable type</span></span> |<span data-ttu-id="7a8b4-725">REG_DWORD-Wert (dezimal)</span><span class="sxs-lookup"><span data-stu-id="7a8b4-725">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="7a8b4-726">Wert</span><span class="sxs-lookup"><span data-stu-id="7a8b4-726">Value</span></span> |<span data-ttu-id="7a8b4-727">120000</span><span class="sxs-lookup"><span data-stu-id="7a8b4-727">120000</span></span> |
| <span data-ttu-id="7a8b4-728">Link zur Dokumentation</span><span class="sxs-lookup"><span data-stu-id="7a8b4-728">Link to documentation</span></span> |[https://technet.microsoft.com/library/cc957548.aspx](https://technet.microsoft.com/library/cc957548.aspx) |

<span data-ttu-id="7a8b4-729">_**Tabelle 4:** Ändern des zweiten TCP/IP-Parameters_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-729">_**Table 4:** Change the second TCP/IP parameter_</span></span>

<span data-ttu-id="7a8b4-730">**Starten Sie beide Clusterknoten neu, um die Änderungen zu übernehmen.**</span><span class="sxs-lookup"><span data-stu-id="7a8b4-730">**To apply the changes, restart both cluster nodes**.</span></span>

### <a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> <span data-ttu-id="7a8b4-731">Einrichten eines Windows Server-Failoverclustering-Clusters für eine SAP ASCS/SCS-Instanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-731">Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="7a8b4-732">Das Einrichten eines Windows Server-Failoverclustering-Clusters für eine SAP ASCS/SCS-Instanz umfasst diese Aufgaben:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-732">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="7a8b4-733">Erfassen der Clusterknoten in einer Clusterkonfiguration</span><span class="sxs-lookup"><span data-stu-id="7a8b4-733">Collecting the cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="7a8b4-734">Konfigurieren eines Cluster-Dateifreigabenzeugen</span><span class="sxs-lookup"><span data-stu-id="7a8b4-734">Configuring a cluster file share witness</span></span>

#### <a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> <span data-ttu-id="7a8b4-735">Erfassen der Clusterknoten in einer Clusterkonfiguration</span><span class="sxs-lookup"><span data-stu-id="7a8b4-735">Collect the cluster nodes in a cluster configuration</span></span>

1. <span data-ttu-id="7a8b4-736">Fügen Sie im Assistenten zum Hinzufügen von Rollen und Features beiden Clusterknoten das Failoverclustering hinzu.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-736">In the Add Role and Features Wizard, add failover clustering to both cluster nodes.</span></span>
2. <span data-ttu-id="7a8b4-737">Richten Sie den Failovercluster mit dem Failovercluster-Manager ein.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-737">Set up the failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="7a8b4-738">Wählen Sie im Failovercluster-Manager die Option **Cluster erstellen**, und fügen Sie dann nur den Namen des ersten Clusters (Knoten A) hinzu. Fügen Sie den zweiten Knoten noch nicht hinzu. Dies führen Sie in einem späteren Schritt durch.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-738">In Failover Cluster Manager, select **Create Cluster**, and then add only the name of the first cluster, node A. Do not add the second node yet; you'll add the second node in a later step.</span></span>

   ![Abbildung 18: Hinzufügen eines Namens für den Server oder die VM des ersten Clusterknotens][sap-ha-guide-figure-3007]

   <span data-ttu-id="7a8b4-740">_**Abbildung 18:** Hinzufügen eines Namens für den Server oder die VM des ersten Clusterknotens_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-740">_**Figure 18:** Add the server or virtual machine name of the first cluster node_</span></span>

3. <span data-ttu-id="7a8b4-741">Geben Sie den Netzwerknamen (Name des virtuellen Hosts) des Clusters ein.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-741">Enter the network name (virtual host name) of the cluster.</span></span>

   ![Abbildung 19: Eingeben des Clusternamens][sap-ha-guide-figure-3008]

   <span data-ttu-id="7a8b4-743">_**Abbildung 19:** Eingeben des Clusternamens_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-743">_**Figure 19:** Enter the cluster name_</span></span>

4. <span data-ttu-id="7a8b4-744">Führen Sie nach dem Erstellen des Clusters einen Test zur Überprüfung des Clusters durch.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-744">After you've created the cluster, run a cluster validation test.</span></span>

   ![Abbildung 20: Ausführen der Clusterüberprüfung][sap-ha-guide-figure-3009]

   <span data-ttu-id="7a8b4-746">_**Abbildung 20:** Ausführen der Clusterüberprüfung_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-746">_**Figure 20:** Run the cluster validation check_</span></span>

   <span data-ttu-id="7a8b4-747">Sie können an diesem Punkt im Prozess sämtliche Warnungen zu Datenträgern ignorieren.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-747">You can ignore any warnings about disks at this point in the process.</span></span> <span data-ttu-id="7a8b4-748">Sie fügen später einen Dateifreigabenzeugen und die freigegebenen SIOS-Datenträger hinzu.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-748">You'll add a file share witness and the SIOS shared disks later.</span></span> <span data-ttu-id="7a8b4-749">In dieser Phase müssen Sie noch kein Quorum berücksichtigen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-749">At this stage, you don't need to worry about having a quorum.</span></span>

   ![Abbildung 21: Kein Quorumdatenträger gefunden][sap-ha-guide-figure-3010]

   <span data-ttu-id="7a8b4-751">_**Abbildung 21:** Kein Quorumdatenträger gefunden_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-751">_**Figure 21:** No quorum disk is found_</span></span>

   ![Abbildung 22: Die Hauptclusterressource benötigt eine neue IP-Adresse.][sap-ha-guide-figure-3011]

   <span data-ttu-id="7a8b4-753">_**Abbildung 22:** Die Hauptclusterressource benötigt eine neue IP-Adresse._</span><span class="sxs-lookup"><span data-stu-id="7a8b4-753">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5. <span data-ttu-id="7a8b4-754">Ändern Sie die IP-Adresse des Hauptclusterdiensts.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-754">Change the IP address of the core cluster service.</span></span> <span data-ttu-id="7a8b4-755">Der Cluster kann erst gestartet werden, nachdem Sie die IP-Adresse des Hauptclusterdiensts geändert haben, da die IP-Adresse der Serverpunkte auf einen der Knoten des virtuellen Computers zeigt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-755">The cluster can't start until you change the IP address of the core cluster service, because the IP address of the server points to one of the virtual machine nodes.</span></span> <span data-ttu-id="7a8b4-756">Dies wird auf der Seite **Eigenschaften** der IP-Ressource des Hauptclusterdiensts durchgeführt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-756">Do this on the **Properties** page of the core cluster service's IP resource.</span></span>

   <span data-ttu-id="7a8b4-757">Wir müssen z.B. dem virtuellen Hostnamen des Clusters **pr1-ascs-vir** eine IP-Adresse (im Beispiel **10.0.0.42**) zuweisen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-757">For example, we need to assign an IP address (in our example, **10.0.0.42**) for the cluster virtual host name **pr1-ascs-vir**.</span></span>

   ![Abbildung 23: Ändern der IP-Adresse im Dialogfeld „Eigenschaften“][sap-ha-guide-figure-3012]

   <span data-ttu-id="7a8b4-759">_**Abbildung 23:** Ändern der IP-Adresse im Dialogfeld **Eigenschaften**_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-759">_**Figure 23:** In the **Properties** dialog box, change the IP address_</span></span>

   ![Abbildung 24: Zuweisen der für den Cluster reservierten IP-Adresse][sap-ha-guide-figure-3013]

   <span data-ttu-id="7a8b4-761">_**Abbildung 24:** Zuweisen der für den Cluster reservierten IP-Adresse_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-761">_**Figure 24:** Assign the IP address that is reserved for the cluster_</span></span>

6. <span data-ttu-id="7a8b4-762">Versetzen Sie den Namen des virtuellen Hosts für den Cluster in den Onlinezustand.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-762">Bring the cluster virtual host name online.</span></span>

   ![Abbildung 25: Hauptclusterdienst im laufenden Betrieb mit korrekter IP-Adresse][sap-ha-guide-figure-3014]

   <span data-ttu-id="7a8b4-764">_**Abbildung 25:** Hauptclusterdienst im laufenden Betrieb mit korrekter IP-Adresse_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-764">_**Figure 25:** Cluster core service is up and running, and with the correct IP address_</span></span>

7. <span data-ttu-id="7a8b4-765">Fügen Sie den zweiten Clusterknoten hinzu.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-765">Add the second cluster node.</span></span>

   <span data-ttu-id="7a8b4-766">Nachdem der Hauptclusterdienst in Betrieb ist, können Sie den zweiten Clusterknoten hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-766">Now that the core cluster service is up and running, you can add the second cluster node.</span></span>

   ![Abbildung 26: Hinzufügen des zweiten Clusterknotens][sap-ha-guide-figure-3015]

   <span data-ttu-id="7a8b4-768">_**Abbildung 26:** Hinzufügen des zweiten Clusterknotens_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-768">_**Figure 26:** Add the second cluster node_</span></span>

8. <span data-ttu-id="7a8b4-769">Geben Sie einen Namen für zweiten Clusterknotenhost ein.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-769">Enter a name for the second cluster node host.</span></span>

   ![Abbildung 27: Eingeben des Namens für den zweiten Clusterknotenhost][sap-ha-guide-figure-3016]

   <span data-ttu-id="7a8b4-771">_**Abbildung 27:** Eingeben des Namens für den zweiten Clusterknotenhost_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-771">_**Figure 27:** Enter the second cluster node host name_</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="7a8b4-772">Stellen Sie sicher, dass das Kontrollkästchen **Der gesamte geeignete Speicher soll dem Cluster hinzugefügt werden** **NICHT** aktiviert wird.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-772">Be sure that the **Add all eligible storage to the cluster** check box is **NOT** selected.</span></span>  
   >
   >

   ![Abbildung 28: Kontrollkästchen nicht aktivieren][sap-ha-guide-figure-3017]

   <span data-ttu-id="7a8b4-774">_**Abbildung 28:** Kontrollkästchen **nicht** aktivieren_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-774">_**Figure 28:** Do **not** select the check box_</span></span>

   <span data-ttu-id="7a8b4-775">Sie können Warnungen zu Quorum und Datenträgern ignorieren.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-775">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="7a8b4-776">Sie konfigurieren das Quorum und die Freigabe der Datenträger später in [Installieren von SIOS DataKeeper Cluster Edition für SAP ASCS/SCS-Clusterfreigabe-Datenträger][sap-ha-guide-8.12.3].</span><span class="sxs-lookup"><span data-stu-id="7a8b4-776">You'll set the quorum and share the disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

   ![Abbildung 29: Ignorieren der Warnungen zum Datenträgerquorum][sap-ha-guide-figure-3018]

   <span data-ttu-id="7a8b4-778">_**Abbildung 29:** Ignorieren der Warnungen zum Datenträgerquorum_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-778">_**Figure 29:** Ignore warnings about the disk quorum_</span></span>


#### <a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> <span data-ttu-id="7a8b4-779">Konfigurieren eines Cluster-Dateifreigabenzeugen</span><span class="sxs-lookup"><span data-stu-id="7a8b4-779">Configure a cluster file share witness</span></span>

<span data-ttu-id="7a8b4-780">Das Konfigurieren eines Cluster-Dateifreigabenzeugen umfasst die folgenden Aufgaben:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-780">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="7a8b4-781">Erstellen einer Dateifreigabe</span><span class="sxs-lookup"><span data-stu-id="7a8b4-781">Creating a file share</span></span>
- <span data-ttu-id="7a8b4-782">Festlegen des Dateifreigabenzeugen-Quorums im Failovercluster-Manager</span><span class="sxs-lookup"><span data-stu-id="7a8b4-782">Setting the file share witness quorum in Failover Cluster Manager</span></span>

##### <a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> <span data-ttu-id="7a8b4-783">Erstellen einer Dateifreigabe</span><span class="sxs-lookup"><span data-stu-id="7a8b4-783">Create a file share</span></span>

1. <span data-ttu-id="7a8b4-784">Wählen Sie anstelle eines Quorumdatenträgers einen Dateifreigabenzeugen aus.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-784">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="7a8b4-785">Diese Option wird von SIOS DataKeeper unterstützt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-785">SIOS DataKeeper supports this option.</span></span>

   <span data-ttu-id="7a8b4-786">In den Beispielen in diesem Artikel befindet sich der Dateifreigabenzeuge auf dem Active Directory-/DNS-Server, der in Azure ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-786">In the examples in this article, the file share witness is on the Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="7a8b4-787">Der Dateifreigabenzeuge heißt **domcontr 0**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-787">The file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="7a8b4-788">Da Sie eine VPN-Verbindung mit Azure (Site-to-Site-VPN oder Azure ExpressRoute) konfiguriert hätten, ist Ihr Active Directory-/DNS-Dienst lokal und nicht für die Ausführung eines Dateifreigabenzeugen geeignet.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-788">Because you would have configured a VPN connection to Azure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable to run a file share witness.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7a8b4-789">Wenn Ihr Active Directory-/DNS-Dienst nur lokal ausgeführt wird, konfigurieren Sie keinen Dateifreigabenzeugen auf dem lokalen Windows-Betriebssystem mit Active Directory/DNS.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-789">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on the Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="7a8b4-790">Die Netzwerklatenz zwischen Clusterknoten in Azure und lokalen Active Directory-/DNS-Diensten wäre zu hoch und könnte Verbindungsprobleme verursachen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-790">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="7a8b4-791">Konfigurieren Sie den Dateifreigabenzeugen unbedingt auf einem virtuellen Azure-Computer, der in der Nähe des Clusterknotens betrieben wird.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-791">Be sure to configure the file share witness on an Azure virtual machine that is running close to the cluster node.</span></span>  
   >
   >

   <span data-ttu-id="7a8b4-792">Das Quorumlaufwerk benötigt mindestens 1.024 MB freien Speicherplatz.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-792">The quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="7a8b4-793">Für das Quorumlaufwerk empfehlen wir die Verwendung von 2.048 MB freiem Speicherplatz.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-793">We recommend 2,048 MB of free space for the quorum drive.</span></span>

2. <span data-ttu-id="7a8b4-794">Fügen Sie das Clusternamenobjekt hinzu.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-794">Add the cluster name object.</span></span>

   ![Abbildung 30: Zuweisen der Berechtigungen für die Freigabe für das Clusternamenobjekt][sap-ha-guide-figure-3019]

   <span data-ttu-id="7a8b4-796">_**Abbildung 30:** Zuweisen der Berechtigungen für die Freigabe für das Clusternamenobjekt_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-796">_**Figure 30:** Assign the permissions on the share for the cluster name object_</span></span>

   <span data-ttu-id="7a8b4-797">Vergewissern Sie sich, dass die Berechtigungen das Ändern von Daten auf der Freigabe für das Clusternamenobjekt zulassen (im Beispiel **pr1-ascs-vir$**).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-797">Be sure that the permissions include the authority to change data in the share for the cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3. <span data-ttu-id="7a8b4-798">Wählen Sie **Hinzufügen** aus, um das Clusternamenobjekt der Liste hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-798">To add the cluster name object to the list, select **Add**.</span></span> <span data-ttu-id="7a8b4-799">Ändern Sie den Filter, um zusätzlich zu den in Abbildung 31 dargestellten Objekten auch Computerobjekte einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-799">Change the filter to check for computer objects, in addition to those shown in Figure 31.</span></span>

   ![Abbildung 31: Ändern des Objekttyps, um Computer einzuschließen][sap-ha-guide-figure-3020]

   <span data-ttu-id="7a8b4-801">_**Abbildung 31:** Ändern des Objekttyps, um Computer einzuschließen_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-801">_**Figure 31:** Change the Object Types to include computers_</span></span>

   ![Abbildung 32: Aktivieren des Kontrollkästchens „Computer“][sap-ha-guide-figure-3021]

   <span data-ttu-id="7a8b4-803">_**Abbildung 32:** Aktivieren des Kontrollkästchens **Computer**_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-803">_**Figure 32:** Select the **Computers** check box_</span></span>

4. <span data-ttu-id="7a8b4-804">Geben Sie das Clusternamenobjekt ein, wie in Abbildung 31 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-804">Enter the cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="7a8b4-805">Da der Datensatz bereits erstellt wurde, können Sie die Berechtigungen ändern (siehe Abbildung 30).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-805">Because the record has already been created, you can change the permissions, as shown in Figure 30.</span></span>

5. <span data-ttu-id="7a8b4-806">Wählen Sie die Registerkarte **Sicherheit** für die Freigabe aus, und legen Sie anschließend ausführlichere Berechtigungen für das Clusternamenobjekt fest.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-806">Select the **Security** tab of the share, and then set more detailed permissions for the cluster name object.</span></span>

   ![Abbildung 33: Festlegen der Sicherheitsattribute für das Clusternamenobjekt im Dateifreigabequorum][sap-ha-guide-figure-3022]

   <span data-ttu-id="7a8b4-808">_**Abbildung 33:** Festlegen der Sicherheitsattribute für das Clusternamenobjekt im Dateifreigabequorum_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-808">_**Figure 33:** Set the security attributes for the cluster name object on the file share quorum_</span></span>

##### <a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> <span data-ttu-id="7a8b4-809">Festlegen des Dateifreigabenzeugen-Quorums im Failovercluster-Manager</span><span class="sxs-lookup"><span data-stu-id="7a8b4-809">Set the file share witness quorum in Failover Cluster Manager</span></span>

1. <span data-ttu-id="7a8b4-810">Öffnen Sie den Assistenten zum Konfigurieren des Clusterquorums.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-810">Open the Configure Quorum Setting Wizard.</span></span>

   ![Abbildung 34: Starten des Assistenten zum Konfigurieren des Clusterquorums][sap-ha-guide-figure-3023]

   <span data-ttu-id="7a8b4-812">_**Abbildung 34:** Starten des Assistenten zum Konfigurieren des Clusterquorums_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-812">_**Figure 34:** Start the Configure Cluster Quorum Setting Wizard_</span></span>

2. <span data-ttu-id="7a8b4-813">Wählen Sie auf der Seite **Quorumkonfiguration auswählen** die Option **Quorumzeugen auswählen**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-813">On the **Select Quorum Configuration** page, select **Select the quorum witness**.</span></span>

   ![Abbildung 35: Verfügbare Quorumkonfigurationen][sap-ha-guide-figure-3024]

   <span data-ttu-id="7a8b4-815">_**Abbildung 35:** Verfügbare Quorumkonfigurationen_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-815">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3. <span data-ttu-id="7a8b4-816">Wählen Sie auf der Seite **Quorumzeuge auswählen** die Option **Dateifreigabenzeugen konfigurieren**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-816">On the **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

   ![Abbildung 36: Auswählen des Dateifreigabenzeugen][sap-ha-guide-figure-3025]

   <span data-ttu-id="7a8b4-818">_**Abbildung 36:** Auswählen des Dateifreigabenzeugen_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-818">_**Figure 36:** Select the file share witness_</span></span>

4. <span data-ttu-id="7a8b4-819">Geben Sie den UNC-Pfad zur Dateifreigabe ein (im Beispiel \\domcontr-0\FSW).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-819">Enter the UNC path to the file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="7a8b4-820">Wählen Sie **Weiter** aus, um eine Liste der Änderungen anzuzeigen, die Sie vornehmen können.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-820">To see a list of the changes you can make, select **Next**.</span></span>

   ![Abbildung 37: Festlegen des Dateifreigabespeicherorts für die Zeugenfreigabe][sap-ha-guide-figure-3026]

   <span data-ttu-id="7a8b4-822">_**Abbildung 37:** Festlegen des Dateifreigabespeicherorts für die Zeugenfreigabe_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-822">_**Figure 37:** Define the file share location for the witness share_</span></span>

5. <span data-ttu-id="7a8b4-823">Wählen Sie die gewünschten Änderungen und dann **Weiter** aus.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-823">Select the changes you want, and then select **Next**.</span></span> <span data-ttu-id="7a8b4-824">Sie müssen den Cluster erfolgreich neu konfigurieren, wie in Abbildung 38 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-824">You need to successfully reconfigure the cluster configuration as shown in Figure 38.</span></span>  

   ![Abbildung 38: Bestätigung der Neukonfiguration des Clusters][sap-ha-guide-figure-3027]

   <span data-ttu-id="7a8b4-826">_**Abbildung 38:** Bestätigung der Neukonfiguration des Clusters_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-826">_**Figure 38:** Confirmation that you've reconfigured the cluster_</span></span>

<span data-ttu-id="7a8b4-827">Nach der erfolgreichen Installation des Windows-Failoverclusters müssen an einigen Schwellenwerten Änderungen vorgenommen werden, um die Failovererkennung den Bedingungen in Azure anzupassen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-827">After installing the Windows Failover Cluster successfully, changes need to be made to some thresholds to adapt failover detection to conditions in Azure.</span></span> <span data-ttu-id="7a8b4-828">Die zu ändernden Parameter sind in diesem Blog dokumentiert: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span><span class="sxs-lookup"><span data-stu-id="7a8b4-828">The parameters to be changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="7a8b4-829">Vorausgesetzt, dass Ihre beiden virtuellen Computer, die die Windows-Clusterkonfiguration für ASCS/SCS erstellen, sich im gleichen Subnetz befinden, müssen die folgenden Parameter in diese Werte geändert werden:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-829">Assuming that your two VMs that build the Windows Cluster Configuration for ASCS/SCS are in the same SubNet, the following parameters need to be changed to these values:</span></span>
- <span data-ttu-id="7a8b4-830">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="7a8b4-830">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="7a8b4-831">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="7a8b4-831">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="7a8b4-832">Diese Einstellungen wurden von Kunden getestet und boten einerseits einen guten Kompromiss, um flexibel genug zu sein.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-832">These settings were tested with customers and provided a good compromise to be resilient enough on the one side.</span></span> <span data-ttu-id="7a8b4-833">Andererseits ermöglichten diese Einstellungen unter realen Fehlerbedingungen der SAP-Software bzw. bei Knoten-/VM-Fehlern ein genügend schnelles Failover.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-833">On the other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> <span data-ttu-id="7a8b4-834">Installieren von SIOS DataKeeper Cluster Edition für den SAP ASCS/SCS-Clusterfreigabe-Datenträger</span><span class="sxs-lookup"><span data-stu-id="7a8b4-834">Install SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="7a8b4-835">Sie verfügen nun über eine funktionierende Windows Server-Failoverclusteringkonfiguration in Azure.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-835">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="7a8b4-836">Um eine SAP ASCS/SCS-Instanz installieren zu können, benötigen Sie jedoch eine freigegebene Datenträgerressource.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-836">But, to install an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="7a8b4-837">Sie können die erforderlichen freigegebenen Datenträgerressourcen nicht in Azure erstellen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-837">You cannot create the shared disk resources you need in Azure.</span></span> <span data-ttu-id="7a8b4-838">SIOS DataKeeper Cluster Edition ist eine Drittanbieterlösung, die Sie zum Erstellen von freigegebenen Datenträgerressourcen verwenden können.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-838">SIOS DataKeeper Cluster Edition is a third-party solution you can use to create shared disk resources.</span></span>

<span data-ttu-id="7a8b4-839">Das Installieren von SIOS DataKeeper Cluster Edition für SAP ASCS/SCS-Clusterfreigabe-Datenträger umfasst die folgenden Aufgaben:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-839">Installing SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="7a8b4-840">Hinzufügen von .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="7a8b4-840">Adding the .NET Framework 3.5</span></span>
- <span data-ttu-id="7a8b4-841">Installieren von SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="7a8b4-841">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="7a8b4-842">Einrichten von SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="7a8b4-842">Setting up SIOS DataKeeper</span></span>

#### <a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> <span data-ttu-id="7a8b4-843">Hinzufügen von .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="7a8b4-843">Add the .NET Framework 3.5</span></span>
<span data-ttu-id="7a8b4-844">Microsoft .NET Framework 3.5 wird unter Windows Server 2012 R2 nicht automatisch aktiviert oder installiert.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-844">The Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="7a8b4-845">Da .NET Framework für SIOS DataKeeper auf allen Knoten erforderlich ist, auf denen Sie DataKeeper installieren, müssen Sie .NET Framework 3.5 unter dem Gastbetriebssystem aller virtuellen Computer im Cluster installieren.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-845">Because SIOS DataKeeper requires the .NET Framework to be on all nodes that you install DataKeeper on, you must install the .NET Framework 3.5 on the guest operating system of all virtual machines in the cluster.</span></span>

<span data-ttu-id="7a8b4-846">Es gibt zwei Möglichkeiten, .NET Framework 3.5 hinzuzufügen:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-846">There are two ways to add the .NET Framework 3.5:</span></span>

- <span data-ttu-id="7a8b4-847">Verwenden Sie den Assistenten zum Hinzufügen von Rollen und Features in Windows, der in Abbildung 39 dargestellt ist.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-847">Use the Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![Abbildung 39: Installieren von .NET Framework 3.5 mithilfe des Assistenten zum Hinzufügen von Rollen und Features][sap-ha-guide-figure-3028]

  <span data-ttu-id="7a8b4-849">_**Abbildung 39:** Installieren von .NET Framework 3.5 mithilfe des Assistenten zum Hinzufügen von Rollen und Features_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-849">_**Figure 39:** Install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

  ![Abbildung 40: Statusanzeige für die Installation von .NET Framework 3.5 mit dem Assistenten zum Hinzufügen von Rollen und Features][sap-ha-guide-figure-3029]

  <span data-ttu-id="7a8b4-851">_**Abbildung 40:** Statusanzeige für die Installation von .NET Framework 3.5 mit dem Assistenten zum Hinzufügen von Rollen und Features_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-851">_**Figure 40:** Installation progress bar when you install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="7a8b4-852">Verwenden Sie das Befehlszeilentool „dism.exe“.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-852">Use the command-line tool dism.exe.</span></span> <span data-ttu-id="7a8b4-853">Für diese Art von Installation benötigen Sie Zugriff auf das Verzeichnis „SxS“ auf dem Windows-Installationsmedium.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-853">For this type of installation, you need to access the SxS directory on the Windows installation media.</span></span> <span data-ttu-id="7a8b4-854">Geben Sie an einer Eingabeaufforderung mit erhöhten Rechten Folgendes ein:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-854">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <a name="dd41d5a2-8083-415b-9878-839652812102"></a> <span data-ttu-id="7a8b4-855">Installieren von SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="7a8b4-855">Install SIOS DataKeeper</span></span>

<span data-ttu-id="7a8b4-856">Installieren Sie SIOS DataKeeper Cluster Edition auf jedem Knoten im Cluster.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-856">Install SIOS DataKeeper Cluster Edition on each node in the cluster.</span></span> <span data-ttu-id="7a8b4-857">Erstellen Sie eine synchronisierte Spiegelung, und simulieren Sie dann freigegebenen Clusterspeicher, um mit SIOS DataKeeper virtuellen freigegebenen Speicher zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-857">To create virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="7a8b4-858">Erstellen Sie vor der Installation der SIOS-Software den Domänenbenutzer **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-858">Before you install the SIOS software, create the domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="7a8b4-859">Fügen Sie den Benutzer **DataKeeperSvc** der Gruppe **Lokale Administratoren** auf beiden Clusterknoten hinzu.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-859">Add the **DataKeeperSvc** user to the **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="7a8b4-860">So installieren Sie SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="7a8b4-860">To install SIOS DataKeeper:</span></span>

1. <span data-ttu-id="7a8b4-861">Installieren Sie die SIOS-Software auf beiden Clusterknoten.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-861">Install the SIOS software on both cluster nodes.</span></span>

   ![SIOS-Installationsprogramm][sap-ha-guide-figure-3030]

   ![Abbildung 41: Erste Seite der SIOS DataKeeper-Installation][sap-ha-guide-figure-3031]

   <span data-ttu-id="7a8b4-864">_**Abbildung 41:** Erste Seite der SIOS DataKeeper-Installation_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-864">_**Figure 41:** First page of the SIOS DataKeeper installation_</span></span>

2. <span data-ttu-id="7a8b4-865">Wählen Sie in dem in Abbildung 42 dargestellten Dialogfeld **Ja** aus.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-865">In the dialog box shown in Figure 42, select **Yes**.</span></span>

   ![Abbildung 42: Benachrichtigung über die Deaktivierung eines Diensts in DataKeeper][sap-ha-guide-figure-3032]

   <span data-ttu-id="7a8b4-867">_**Abbildung 42:** Benachrichtigung über die Deaktivierung eines Diensts in DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-867">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3. <span data-ttu-id="7a8b4-868">Wir raten Ihnen, im Dialogfeld, das in Abbildung 43 dargestellt ist, die Option **Domänen- oder Serverkonto** zu wählen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-868">In the dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

   ![Abbildung 43: Benutzerauswahl für SIOS DataKeeper][sap-ha-guide-figure-3033]

   <span data-ttu-id="7a8b4-870">_**Abbildung 43:** Benutzerauswahl für SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-870">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4. <span data-ttu-id="7a8b4-871">Geben Sie den Benutzernamen für das Domänenkonto und die Kennwörter ein, die Sie für SIOS DataKeeper erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-871">Enter the domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

   ![Abbildung 44: Eingeben des Domänenbenutzernamens und des Kennworts für die SIOS DataKeeper-Installation][sap-ha-guide-figure-3034]

   <span data-ttu-id="7a8b4-873">_**Abbildung 44:** Eingeben des Domänenbenutzernamens und des Kennworts für die SIOS DataKeeper-Installation_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-873">_**Figure 44:** Enter the domain user name and password for the SIOS DataKeeper installation_</span></span>

5. <span data-ttu-id="7a8b4-874">Installieren Sie den Lizenzschlüssel für Ihre SIOS DataKeeper-Instanz, wie in Abbildung 45 gezeigt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-874">Install the license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

   ![Abbildung 45: Eingeben Ihres SIOS DataKeeper-Lizenzschlüssels][sap-ha-guide-figure-3035]

   <span data-ttu-id="7a8b4-876">_**Abbildung 45:** Eingeben Ihres SIOS DataKeeper-Lizenzschlüssels_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-876">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6. <span data-ttu-id="7a8b4-877">Starten Sie den virtuellen Computer neu, wenn Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-877">When prompted, restart the virtual machine.</span></span>

#### <a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> <span data-ttu-id="7a8b4-878">Einrichten von SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="7a8b4-878">Set up SIOS DataKeeper</span></span>

<span data-ttu-id="7a8b4-879">Nach der Installation von SIOS DataKeeper auf beiden Knoten müssen Sie mit der Konfiguration beginnen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-879">After you install SIOS DataKeeper on both nodes, you need to start the configuration.</span></span> <span data-ttu-id="7a8b4-880">Ziel der Konfiguration ist eine synchrone Datenreplikation zwischen den zusätzlichen VHDs, die Sie an jeden virtuellen Computer angefügt haben.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-880">The goal of the configuration is to have synchronous data replication between the additional VHDs attached to each of the virtual machines.</span></span>

1. <span data-ttu-id="7a8b4-881">Starten Sie das DataKeeper-Tool für die Verwaltung und Konfiguration, und wählen Sie dann **Verbindung mit Server herstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-881">Start the DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="7a8b4-882">(In Abbildung 46 ist diese Option rot markiert.)</span><span class="sxs-lookup"><span data-stu-id="7a8b4-882">(In Figure 46, this option is circled in red.)</span></span>

   ![Abbildung 46: SIOS DataKeeper-Tool für die Verwaltung und Konfiguration][sap-ha-guide-figure-3036]

   <span data-ttu-id="7a8b4-884">_**Abbildung 46:** SIOS DataKeeper-Tool für die Verwaltung und Konfiguration_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-884">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2. <span data-ttu-id="7a8b4-885">Geben Sie den Namen oder die TCP/IP-Adresse des ersten Knotens, mit dem das Tool für die Verwaltung und Konfiguration eine Verbindung herstellen soll, und im zweiten Schritt den zweiten Knoten ein.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-885">Enter the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and, in a second step, the second node.</span></span>

   ![Abbildung 47: Eingeben des Namens oder der TCP/IP-Adresse des ersten Knotens, mit dem das Tool für die Verwaltung und Konfiguration eine Verbindung herstellen soll, und im zweiten Schritt Eingeben des zweiten Knotens][sap-ha-guide-figure-3037]

   <span data-ttu-id="7a8b4-887">_**Abbildung 47:** Eingeben des Namens oder der TCP/IP-Adresse des ersten Knotens, mit dem das Tool für die Verwaltung und Konfiguration eine Verbindung herstellen soll, und im zweiten Schritt Eingeben des zweiten Knotens_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-887">_**Figure 47:** Insert the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and in a second step, the second node_</span></span>

3. <span data-ttu-id="7a8b4-888">Erstellen Sie den Replikationsauftrag zwischen den beiden Knoten.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-888">Create the replication job between the two nodes.</span></span>

   ![Abbildung 48: Erstellen eines Replikationsauftrags][sap-ha-guide-figure-3038]

   <span data-ttu-id="7a8b4-890">_**Abbildung 48:** Erstellen eines Replikationsauftrags_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-890">_**Figure 48:** Create a replication job_</span></span>

   <span data-ttu-id="7a8b4-891">Ein Assistent führt Sie durch die Erstellung eines Replikationsauftrags.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-891">A wizard guides you through the process of creating a replication job.</span></span>
4. <span data-ttu-id="7a8b4-892">Definieren Sie Name, TCP/IP-Adresse und Datenträgervolume des Quellknotens.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-892">Define the name, TCP/IP address, and disk volume of the source node.</span></span>

   ![Abbildung 49: Festlegen des Namens für den Replikationsauftrag][sap-ha-guide-figure-3039]

   <span data-ttu-id="7a8b4-894">_**Abbildung 49:** Festlegen des Namens für den Replikationsauftrag_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-894">_**Figure 49:** Define the name of the replication job_</span></span>

   ![Abbildung 50: Definieren der Basisdaten für den Knoten, der der aktuelle Quellknoten sein soll][sap-ha-guide-figure-3040]

   <span data-ttu-id="7a8b4-896">_**Abbildung 50:** Definieren der Basisdaten für den Knoten, der der aktuelle Quellknoten sein soll_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-896">_**Figure 50:** Define the base data for the node, which should be the current source node_</span></span>

5. <span data-ttu-id="7a8b4-897">Definieren Sie Name, TCP/IP-Adresse und Datenträgervolume des Zielknotens.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-897">Define the name, TCP/IP address, and disk volume of the target node.</span></span>

   ![Abbildung 51: Definieren der Basisdaten für den Knoten, der der aktuelle Zielknoten sein soll][sap-ha-guide-figure-3041]

   <span data-ttu-id="7a8b4-899">_**Abbildung 51:** Definieren der Basisdaten für den Knoten, der der aktuelle Zielknoten sein soll_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-899">_**Figure 51:** Define the base data for the node, which should be the current target node_</span></span>

6. <span data-ttu-id="7a8b4-900">Definieren Sie die Komprimierungsalgorithmen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-900">Define the compression algorithms.</span></span> <span data-ttu-id="7a8b4-901">Für unser Beispiel wird das Komprimieren des Replikationsdatenstroms empfohlen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-901">In our example, we recommend that you compress the replication stream.</span></span> <span data-ttu-id="7a8b4-902">Insbesondere in Situationen mit erneuter Synchronisierung wird die dafür erforderliche Dauer durch die Komprimierung des Replikationsdatenstroms erheblich verkürzt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-902">Especially in resynchronization situations, the compression of the replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="7a8b4-903">Beachten Sie, dass die Komprimierung CPU- und Arbeitsspeicherressourcen eines virtuellen Computers verbraucht.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-903">Note that compression uses the CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="7a8b4-904">Wenn die Komprimierungsrate zunimmt, steigt auch die Menge der erforderlichen CPU-Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-904">As the compression rate increases, so does the volume of CPU resources used.</span></span> <span data-ttu-id="7a8b4-905">Sie können diese Einstellung auch später anpassen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-905">You also can adjust this setting later.</span></span>

7. <span data-ttu-id="7a8b4-906">Eine weitere Einstellung, die Sie überprüfen müssen, ist, ob die Replikation asynchron oder synchron erfolgt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-906">Another setting you need to check is whether the replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="7a8b4-907">*Wenn Sie SAP ASCS/SCS-Konfigurationen schützen, müssen Sie die synchrone Replikation verwenden*.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-907">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

   ![Abbildung 52: Festlegen der Replikationsdetails][sap-ha-guide-figure-3042]

   <span data-ttu-id="7a8b4-909">_**Abbildung 52:** Festlegen der Replikationsdetails_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-909">_**Figure 52:** Define replication details_</span></span>

8. <span data-ttu-id="7a8b4-910">Definieren Sie, ob das Volume, das vom Replikationsauftrag repliziert wird, gegenüber einer Windows Server-Failoverclustering-Clusterkonfiguration als freigegebener Datenträger dargestellt werden sollte.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-910">Define whether the volume that is replicated by the replication job should be represented to a Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="7a8b4-911">Für die SAP ASCS/SCS-Konfiguration wählen Sie **Ja** aus, damit der Windows-Cluster das replizierte Volume als freigegebenen Datenträger erkennt, das als Clustervolume verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-911">For the SAP ASCS/SCS configuration, select **Yes** so that the Windows cluster sees the replicated volume as a shared disk that it can use as a cluster volume.</span></span>

   ![Abbildung 53: Klicken auf „Ja“, um das replizierte Volume als Clustervolume festzulegen][sap-ha-guide-figure-3043]

   <span data-ttu-id="7a8b4-913">_**Abbildung 53:** Klicken auf **Ja**, um das replizierte Volume als Clustervolume festzulegen_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-913">_**Figure 53:** Select **Yes** to set the replicated volume as a cluster volume_</span></span>

   <span data-ttu-id="7a8b4-914">Nachdem das Volume erstellt wurde, zeigt das DataKeeper-Tool für die Verwaltung und Konfiguration an, dass der Replikationsauftrag aktiv ist.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-914">After the volume is created, the DataKeeper Management and Configuration tool shows that the replication job is active.</span></span>

   ![Abbildung 54: Die synchrone Spiegelung von DataKeeper für den SAP ASCS/SCS-Freigabedatenträger ist aktiv.][sap-ha-guide-figure-3044]

   <span data-ttu-id="7a8b4-916">_**Abbildung 54:** Die synchrone Spiegelung von DataKeeper für den SAP ASCS/SCS-Freigabedatenträger ist aktiv._</span><span class="sxs-lookup"><span data-stu-id="7a8b4-916">_**Figure 54:** DataKeeper synchronous mirroring for the SAP ASCS/SCS share disk is active_</span></span>

   <span data-ttu-id="7a8b4-917">Der Failovercluster-Manager zeigt nun den Datenträger als DataKeeper-Datenträger an, wie in Abbildung 55 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-917">Failover Cluster Manager now shows the disk as a DataKeeper disk, as shown in Figure 55.</span></span>

   ![Abbildung 55: Anzeige des von DataKeeper replizierten Datenträgers im Failovercluster-Manager][sap-ha-guide-figure-3045]

   <span data-ttu-id="7a8b4-919">_**Abbildung 55:** Anzeige des von DataKeeper replizierten Datenträgers im Failovercluster-Manager_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-919">_**Figure 55:** Failover Cluster Manager shows the disk that DataKeeper replicated_</span></span>

## <a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> <span data-ttu-id="7a8b4-920">Installieren des SAP NetWeaver-Systems</span><span class="sxs-lookup"><span data-stu-id="7a8b4-920">Install the SAP NetWeaver system</span></span>

<span data-ttu-id="7a8b4-921">Das DBMS-Setup wird hier nicht beschrieben, da die Einrichtung vom verwendeten DBMS abhängt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-921">We won't describe the DBMS setup because setups vary depending on the DBMS system you use.</span></span> <span data-ttu-id="7a8b4-922">Jedoch wird davon ausgegangen, dass auf hohe Verfügbarkeit bezogene Aspekte des DBMS mit den Funktionen verwaltet werden, die verschiedene DBMS-Hersteller für Azure unterstützen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-922">However, we assume that high-availability concerns with the DBMS are addressed with the functionalities the different DBMS vendors support for Azure.</span></span> <span data-ttu-id="7a8b4-923">Beispiele hierfür sind Always On oder Datenbankspiegelung für SQL Server und Oracle Data Guard für Oracle-Datenbanken.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-923">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="7a8b4-924">In dem Szenario in diesem Artikel haben wir keinen zusätzlichen Schutz für das DBMS hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-924">In the scenario we use in this article, we didn't add more protection to the DBMS.</span></span>

<span data-ttu-id="7a8b4-925">Es sind keine Besonderheiten zu berücksichtigen, wenn unterschiedliche DBMS-Dienste mit dieser Art von SAP ASCS/SCS-Clusterkonfiguration in Azure interagieren.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-925">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="7a8b4-926">Der Installationsvorgang von SAP NetWeaver ABAP-, Java- und ABAP+Java-Systemen ist nahezu identisch.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-926">The installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="7a8b4-927">Der wichtigste Unterschied ist, dass ein SAP ABAP-System eine ASCS-Instanz hat.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-927">The most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="7a8b4-928">Das SAP Java-System hat eine SCS-Instanz.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-928">The SAP Java system has one SCS instance.</span></span> <span data-ttu-id="7a8b4-929">Das SAP ABAP+Java-System hat eine ASCS- und eine SCS-Instanz, die in der gleichen Microsoft-Failoverclustergruppe ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-929">The SAP ABAP+Java system has one ASCS instance and one SCS instance running in the same Microsoft failover cluster group.</span></span> <span data-ttu-id="7a8b4-930">Unterschiede bei der Installation der einzelnen SAP NetWeaver-Installationsstapel werden explizit angegeben.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-930">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="7a8b4-931">Sie können davon ausgehen, dass alle anderen Teile gleich sind.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-931">You can assume that all other parts are the same.</span></span>  
>
>

### <a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> <span data-ttu-id="7a8b4-932">Installieren von SAP mit einer hoch verfügbaren ASCS/SCS-Instanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-932">Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a8b4-933">Achten Sie darauf, nicht die Auslagerungsdatei auf von DataKeeper gespiegelten Volumes zu platzieren.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-933">Be sure not to place your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="7a8b4-934">DataKeeper unterstützt keine gespiegelten Volumes.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-934">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="7a8b4-935">Belassen Sie die Auslagerungsdatei auf dem temporären Laufwerk D eines virtuellen Azure-Computers (dies ist auch die Standardeinstellung).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-935">You can leave your page file on the temporary drive D of an Azure virtual machine, which is the default.</span></span> <span data-ttu-id="7a8b4-936">Wenn sie sich noch nicht dort befindet, verschieben Sie die Windows-Auslagerungsdatei auf Laufwerk D des virtuellen Azure-Computers.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-936">If it's not already there, move the Windows page file to drive D of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="7a8b4-937">Das Installieren von SAP mit einer ASCS/SCS-Instanz mit hoher Verfügbarkeit umfasst die folgenden Aufgaben:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-937">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="7a8b4-938">Erstellen eines virtuellen Hostnamens für die SAP ASCS/SCS-Clusterinstanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-938">Creating a virtual host name for the clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="7a8b4-939">Installieren des ersten SAP-Clusterknotens</span><span class="sxs-lookup"><span data-stu-id="7a8b4-939">Installing the SAP first cluster node</span></span>
- <span data-ttu-id="7a8b4-940">Ändern des SAP-Profils der ASCS/SCS-Instanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-940">Modifying the SAP profile of the ASCS/SCS instance</span></span>
- <span data-ttu-id="7a8b4-941">Hinzufügen eines Testports</span><span class="sxs-lookup"><span data-stu-id="7a8b4-941">Adding a probe port</span></span>
- <span data-ttu-id="7a8b4-942">Öffnen des Windows-Firewall-Testports</span><span class="sxs-lookup"><span data-stu-id="7a8b4-942">Opening the Windows firewall probe port</span></span>

#### <a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> <span data-ttu-id="7a8b4-943">Erstellen eines virtuellen Hostnamens für die SAP ASCS/SCS-Clusterinstanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-943">Create a virtual host name for the clustered SAP ASCS/SCS instance</span></span>

1. <span data-ttu-id="7a8b4-944">Erstellen Sie im Windows-DNS-Manager einen DNS-Eintrag für den virtuellen Hostnamen der ASCS/SCS-Instanz.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-944">In the Windows DNS manager, create a DNS entry for the virtual host name of the ASCS/SCS instance.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="7a8b4-945">Die IP-Adresse, die Sie dem virtuellen Hostnamen der ASCS/SCS-Instanz zuweisen, muss mit der IP-Adresse identisch sein, die Sie dem Azure Load Balancer zugeordnet haben (**<*SID*>-lb-ascs**).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-945">The IP address that you assign to the virtual host name of the ASCS/SCS instance must be the same as the IP address that you assigned to Azure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
   >
   >

   <span data-ttu-id="7a8b4-946">Die IP-Adresse des virtuellen Hostnamens der SAP ASCS/SCS-Instanz (**pr1-ascs-sap**) ist mit der IP-Adresse des Azure Load Balancers (**pr1-lb-ascs**) identisch.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-946">The IP address of the virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is the same as the IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

   ![Abbildung 56: Festlegen des DNS-Eintrags für den virtuellen SAP ASCS/SCS-Clusternamen und der TCP/IP-Adresse][sap-ha-guide-figure-3046]

   <span data-ttu-id="7a8b4-948">_**Abbildung 56:** Festlegen des DNS-Eintrags für den virtuellen SAP ASCS/SCS-Clusternamen und der TCP/IP-Adresse_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-948">_**Figure 56:** Define the DNS entry for the SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2. <span data-ttu-id="7a8b4-949">Wählen Sie zum Definieren der IP-Adresse, die dem virtuellen Hostnamen zugewiesen ist, die Option **DNS-Manager** > **Domäne**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-949">To define the IP address assigned to the virtual host name, select **DNS Manager** > **Domain**.</span></span>

   ![Abbildung 57: Neuer virtueller Name und TCP/IP-Adresse für die SAP ASCS/SCS-Clusterkonfiguration][sap-ha-guide-figure-3047]

   <span data-ttu-id="7a8b4-951">_**Abbildung 57:** Neuer virtueller Name und TCP/IP-Adresse für die SAP ASCS/SCS-Clusterkonfiguration_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-951">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> <span data-ttu-id="7a8b4-952">Installieren des ersten SAP-Clusterknotens</span><span class="sxs-lookup"><span data-stu-id="7a8b4-952">Install the SAP first cluster node</span></span>

1. <span data-ttu-id="7a8b4-953">Führen Sie die Option für den ersten Clusterknoten auf Clusterknoten A aus, z.B. auf dem Host **pr1-ascs-0**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-953">Execute the first cluster node option on cluster node A. For example, on the **pr1-ascs-0** host.</span></span>
2. <span data-ttu-id="7a8b4-954">Wählen Sie Folgendes aus, um für den internen Azure Load Balancer die Standardports beizubehalten:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-954">To keep the default ports for the Azure internal load balancer, select:</span></span>

   * <span data-ttu-id="7a8b4-955">**ABAP-System**: **ASCS**-Instanznummer **00**</span><span class="sxs-lookup"><span data-stu-id="7a8b4-955">**ABAP system**: **ASCS** instance number **00**</span></span>
   * <span data-ttu-id="7a8b4-956">**Java-System**: **SCS**-Instanznummer **01**</span><span class="sxs-lookup"><span data-stu-id="7a8b4-956">**Java system**: **SCS** instance number **01**</span></span>
   * <span data-ttu-id="7a8b4-957">**ABAP + Java-System**: **ASCS**-Instanznummer **00** und **SCS**-Instanznummer **01**</span><span class="sxs-lookup"><span data-stu-id="7a8b4-957">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

   <span data-ttu-id="7a8b4-958">Um andere Instanznummern als 00 für eine ABAP ASCS-Instanz und 01 für eine Java SCS-Instanz zu verwenden, müssen Sie zunächst die Standardregeln für den Lastenausgleich durch den internen Azure Load Balancer ändern. Dieser Vorgang wird in [Ändern der Standardregeln für den ASCS/SCS-Lastenausgleich durch den internen Azure Load Balancer][sap-ha-guide-8.9] beschrieben.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-958">To use instance numbers other than 00 for the ABAP ASCS instance and 01 for the Java SCS instance, first you need to change the Azure internal load balancer default load balancing rules, described in [Change the ASCS/SCS default load balancing rules for the Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="7a8b4-959">Die nächsten Aufgaben sind in der SAP-Dokumentation für die Standardinstallation nicht beschrieben.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-959">The next few tasks aren't described in the standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="7a8b4-960">Die SAP-Installationsdokumentation beschreibt, wie der erste ASCS/SCS-Clusterknoten installiert wird.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-960">The SAP installation documentation describes how to install the first ASCS/SCS cluster node.</span></span>
>
>

#### <a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> <span data-ttu-id="7a8b4-961">Ändern des SAP-Profils der ASCS/SCS-Instanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-961">Modify the SAP profile of the ASCS/SCS instance</span></span>

<span data-ttu-id="7a8b4-962">Sie müssen einen neuen Profilparameter hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-962">You need to add a new profile parameter.</span></span> <span data-ttu-id="7a8b4-963">Dieser Profilparameter verhindert das Schließen von Verbindungen zwischen SAP-Workprozessen und dem Enqueue-Server, wenn diese sich zu lange im Leerlauf befinden.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-963">The profile parameter prevents connections between SAP work processes and the enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="7a8b4-964">Dieses Problem wurde bereits unter [Hinzufügen von Registrierungseinträgen auf beiden Clusterknoten für eine SAP ASCS/SCS-Instanz][sap-ha-guide-8.11] erwähnt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-964">We mentioned the problem scenario in [Add registry entries on both cluster nodes of the SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="7a8b4-965">In diesem Abschnitt haben wir auch zwei Änderungen an grundlegenden TCP/IP-Verbindungsparametern vorgenommen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-965">In that section, we also introduced two changes to some basic TCP/IP connection parameters.</span></span> <span data-ttu-id="7a8b4-966">In einem zweiten Schritt müssen Sie den Enqueue-Server für das Senden eines `keep_alive`-Signals konfigurieren, damit die Verbindungen nicht den Schwellenwert für den Leerlauf des internen Azure Load Balancers erreichen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-966">In a second step, you need to set the enqueue server to send a `keep_alive` signal so that the connections don't hit the Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="7a8b4-967">So ändern Sie das SAP-Profil der ASCS/SCS-Instanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-967">To modify the SAP profile of the ASCS/SCS instance:</span></span>

1. <span data-ttu-id="7a8b4-968">Fügen Sie diesen Profilparameter dem Profil der SAP ASCS/SCS-Instanz hinzu:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-968">Add this profile parameter to the SAP ASCS/SCS instance profile:</span></span>

   ```
   enque/encni/set_so_keepalive = true
   ```
   <span data-ttu-id="7a8b4-969">Bei unserem Beispiel lautet der Pfad:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-969">In our example, the path is:</span></span>

   `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

   <span data-ttu-id="7a8b4-970">Beispiel für das Profil einer SAP SCS-Instanz und den zugehörigen Pfad:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-970">For example, to the SAP SCS instance profile and corresponding path:</span></span>

   `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2. <span data-ttu-id="7a8b4-971">Starten Sie die SAP ASCS/SCS-Instanz neu, um die Änderungen zu übernehmen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-971">To apply the changes, restart the SAP ASCS /SCS instance.</span></span>

#### <a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> <span data-ttu-id="7a8b4-972">Hinzufügen eines Testports</span><span class="sxs-lookup"><span data-stu-id="7a8b4-972">Add a probe port</span></span>

<span data-ttu-id="7a8b4-973">Nutzen Sie die Testfunktionalität des internen Lastenausgleichs, damit die gesamte Clusterkonfiguration mit Azure Load Balancer funktioniert.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-973">Use the internal load balancer's probe functionality to make the entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="7a8b4-974">Der interne Azure Load Balancer verteilt in der Regel die eingehende Workload gleichmäßig auf die beteiligten virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-974">The Azure internal load balancer usually distributes the incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="7a8b4-975">Allerdings funktioniert dies bei einigen Clusterkonfigurationen nicht, da nur eine Instanz aktiv ist.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-975">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="7a8b4-976">Die andere Instanz ist passiv und kann daher keine Workload annehmen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-976">The other instance is passive and can't accept any of the workload.</span></span> <span data-ttu-id="7a8b4-977">Eine Testfunktion ist hilfreich, wenn der interne Azure Load Balancer die Workload nur einer aktiven Instanz zuweist.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-977">A probe functionality helps when the Azure internal load balancer assigns work only to an active instance.</span></span> <span data-ttu-id="7a8b4-978">Mit der Testfunktion kann der internen Load Balancer erkennen, welche Instanzen aktiv sind, und dann nur dieser Instanz Workload zuweisen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-978">With the probe functionality, the internal load balancer can detect which instances are active, and then target only the instance with the workload.</span></span>

<span data-ttu-id="7a8b4-979">So fügen Sie einen Testport hinzu</span><span class="sxs-lookup"><span data-stu-id="7a8b4-979">To add a probe port:</span></span>

1. <span data-ttu-id="7a8b4-980">Überprüfen Sie die aktuelle **ProbePort**-Einstellung, indem Sie den folgenden PowerShell-Befehl ausführen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-980">Check the current **ProbePort** setting by running the following PowerShell command.</span></span> <span data-ttu-id="7a8b4-981">Führen Sie ihn auf einem virtuellen Computer in der Clusterkonfiguration aus.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-981">Execute it from within one of the virtual machines in the cluster configuration.</span></span>

   ```PowerShell
   $SAPSID = "PR1"     # SAP <SID>

   $SAPNetworkIPClusterName = "SAP $SAPSID IP"
   Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
   ```

2. <span data-ttu-id="7a8b4-982">Definieren Sie einen Testport.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-982">Define a probe port.</span></span> <span data-ttu-id="7a8b4-983">Die Standardnummer für den Testport ist **0**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-983">The default probe port number is **0**.</span></span> <span data-ttu-id="7a8b4-984">In unserem Beispiel verwenden wir als Testport **62000**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-984">In our example, we use probe port **62000**.</span></span>

   ![Abbildung 58: Der Testport der Clusterkonfiguration ist standardmäßig 0.][sap-ha-guide-figure-3048]

   <span data-ttu-id="7a8b4-986">_**Abbildung 58:** Der Standardtestport der Clusterkonfiguration ist 0._</span><span class="sxs-lookup"><span data-stu-id="7a8b4-986">_**Figure 58:** The default cluster configuration probe port is 0_</span></span>

   <span data-ttu-id="7a8b4-987">Die Portnummer ist in Azure Resource Manager-Vorlagen für SAP definiert.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-987">The port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="7a8b4-988">Sie können die Portnummer in PowerShell zuweisen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-988">You can assign the port number in PowerShell.</span></span>

   <span data-ttu-id="7a8b4-989">Führen Sie das folgende PowerShell-Skript aus, um einen neuen ProbePort-Wert für die Clusterressource **SAP <*SID*> IP** festzulegen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-989">To set a new ProbePort value for the **SAP <*SID*> IP** cluster resource, run the following PowerShell script.</span></span> <span data-ttu-id="7a8b4-990">Aktualisieren Sie die PowerShell-Variablen für Ihre Umgebung.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-990">Update the PowerShell variables for your environment.</span></span> <span data-ttu-id="7a8b4-991">Nach dem Ausführen des Skripts werden Sie aufgefordert, die SAP-Clustergruppe neu zu starten, um die Änderungen zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-991">After the script runs, you'll be prompted to restart the SAP cluster group to activate the changes.</span></span>

   ```PowerShell
   $SAPSID = "PR1"      # SAP <SID>
   $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

   Clear-Host
   $SAPClusterRoleName = "SAP $SAPSID"
   $SAPIPresourceName = "SAP $SAPSID IP"
   $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
   $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
   $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
   $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
   $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
   $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
   $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

   $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

   Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
   Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

   Write-Host
   Write-Host "Current probe port property of the SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
   Write-Host
   Write-Host "Setting the new probe port property of the SAP cluster resource '$SAPIPresourceName' to '$ProbePort' ..." -ForegroundColor Cyan
   Write-Host

   $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

   Write-Host

   $ActivateChanges = Read-Host "Do you want to take restart SAP cluster role '$SAPClusterRoleName', to activate the changes (yes/no)?"

   if($ActivateChanges -eq "yes"){
   Write-Host
   Write-Host "Activating changes..." -ForegroundColor Cyan

   Write-Host
   write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
   Stop-ClusterResource -Name $SAPIPresourceName
   sleep 5

   Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
   Start-ClusterGroup -Name $SAPClusterRoleName

   Write-Host "New ProbePort parameter is active." -ForegroundColor Green
   Write-Host

   Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
   Write-Host
   Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
   }else
   {
   Write-Host "Changes are not activated."
   }
   ```

   <span data-ttu-id="7a8b4-992">Überprüfen Sie, nachdem Sie die Clusterrolle **SAP <*SID*>** online geschaltet haben, ob **ProbePort** auf den neuen Wert festgelegt wurde.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-992">After you bring the **SAP <*SID*>** cluster role online, verify that **ProbePort** is set to the new value.</span></span>

   ```PowerShell
   $SAPSID = "PR1"     # SAP <SID>

   $SAPNetworkIPClusterName = "SAP $SAPSID IP"
   Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

   ```

   ![Abbildung 59: Testen des Clusterports nach dem Festlegen des neuen Werts][sap-ha-guide-figure-3049]

   <span data-ttu-id="7a8b4-994">_**Abbildung 59:** Testen des Clusterports nach dem Festlegen des neuen Werts_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-994">_**Figure 59:** Probe the cluster port after you set the new value_</span></span>

#### <a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> <span data-ttu-id="7a8b4-995">Öffnen des Windows-Firewall-Testports</span><span class="sxs-lookup"><span data-stu-id="7a8b4-995">Open the Windows firewall probe port</span></span>

<span data-ttu-id="7a8b4-996">Sie müssen einen Windows-Firewall-Testport auf beiden Clusterknoten öffnen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-996">You need to open a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="7a8b4-997">Verwenden Sie das folgende Skript, um einen Windows-Firewall-Testport zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-997">Use the following script to open a Windows firewall probe port.</span></span> <span data-ttu-id="7a8b4-998">Aktualisieren Sie die PowerShell-Variablen für Ihre Umgebung.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-998">Update the PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="7a8b4-999">Die Einstellung **ProbePort** wurde auf **62000** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-999">The **ProbePort** is set to **62000**.</span></span> <span data-ttu-id="7a8b4-1000">Sie können nun auf die Dateifreigabe **\\\ascsha-clsap\sapmnt** von anderen Hosts zugreifen, z.B. **ascsha-dbas**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1000">Now you can access the file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> <span data-ttu-id="7a8b4-1001">Installieren der Datenbankinstanz</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1001">Install the database instance</span></span>

<span data-ttu-id="7a8b4-1002">Führen Sie für die Installation der Datenbankinstanz die in der SAP-Installationsdokumentation beschriebene Vorgehensweise durch.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1002">To install the database instance, follow the process described in the SAP installation documentation.</span></span>

### <a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> <span data-ttu-id="7a8b4-1003">Installieren des zweiten Clusterknotens</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1003">Install the second cluster node</span></span>

<span data-ttu-id="7a8b4-1004">Führen Sie zum Installieren des zweiten Clusterknotens die Schritte im SAP-Installationshandbuch aus.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1004">To install the second cluster, follow the steps in the SAP installation guide.</span></span>

### <a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> <span data-ttu-id="7a8b4-1005">Ändern des Starttyps der Windows-Dienstinstanz für SAP ERS</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1005">Change the start type of the SAP ERS Windows service instance</span></span>

<span data-ttu-id="7a8b4-1006">Ändern Sie den Starttyp der Windows-Dienste für SAP ERS auf beiden Clusterknoten in **Automatisch (Verzögerter Start)**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1006">Change the start type of the SAP ERS Windows service to **Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Abbildung 60: Ändern des Starttyps der SAP ERS-Instanz in „Automatisch (Verzögerter Start)“][sap-ha-guide-figure-3050]

<span data-ttu-id="7a8b4-1008">_**Abbildung 60:** Ändern des Starttyps der SAP ERS-Instanz in „Automatisch (Verzögerter Start)“_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1008">_**Figure 60:** Change the service type for the SAP ERS instance to delayed automatic_</span></span>

### <a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> <span data-ttu-id="7a8b4-1009">Installieren des primären SAP-Anwendungsservers</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1009">Install the SAP Primary Application Server</span></span>

<span data-ttu-id="7a8b4-1010">Installieren Sie die PAS-Instanz (primärer Anwendungsserver) <*SID*>-di-0 auf dem virtuellen Computer, den Sie als Host für den PAS vorgesehen haben.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1010">Install the Primary Application Server (PAS) instance <*SID*>-di-0 on the virtual machine that you've designated to host the PAS.</span></span> <span data-ttu-id="7a8b4-1011">Es bestehen keine Abhängigkeiten mit spezifischen Einstellungen für Azure oder DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1011">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> <span data-ttu-id="7a8b4-1012">Installieren des zusätzlichen SAP-Anwendungsservers</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1012">Install the SAP Additional Application Server</span></span>

<span data-ttu-id="7a8b4-1013">Installieren Sie einen zusätzlichen SAP-Anwendungsserver (Additional Application Server, AAS) auf allen virtuellen Computern, die Sie als Hosts von SAP-Anwendungsserverinstanzen festgelegt haben.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1013">Install an SAP Additional Application Server (AAS) on all the virtual machines that you've designated to host an SAP Application Server instance.</span></span> <span data-ttu-id="7a8b4-1014">Beispielsweise auf <*SID*>-di-1 bis <*SID*>-di-&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1014">For example, on <*SID*>-di-1 to <*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="7a8b4-1015">Die Installation eines SAP NetWeaver-Systems mit hoher Verfügbarkeit ist hiermit abgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1015">This finishes the installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="7a8b4-1016">Als Nächstes stehen die Failovertests an.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1016">Next, proceed with failover testing.</span></span>
>


## <a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> <span data-ttu-id="7a8b4-1017">Testen des Failovers der SAP ASCS/SCS-Instanz und der SIOS-Replikation</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1017">Test the SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="7a8b4-1018">Mit dem Failovercluster-Manager und dem SIOS DataKeeper-Tool für die Verwaltung und Konfiguration können Sie das Failover für eine SAP ASCS/SCS-Instanz und die SIOS-Datenträgerreplikation ganz einfach testen und überwachen.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1018">It's easy to test and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and the SIOS DataKeeper Management and Configuration tool.</span></span>

### <a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> <span data-ttu-id="7a8b4-1019">Die SAP ASCS/SCS-Instanz wird auf Clusterknoten A ausgeführt</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1019">SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="7a8b4-1020">Die Clustergruppe **SAP PR1** wird auf dem Clusterknoten A ausgeführt, z.B. auf **pr1-ascs-0**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1020">The **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="7a8b4-1021">Weisen Sie den freigegebenen Datenträger S, der Teil der Clustergruppe **SAP PR1** ist und von der ASCS/SCS-Instanz verwendet wird, dem Clusterknoten A zu.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1021">Assign the shared disk drive S, which is part of the **SAP PR1** cluster group, and which the ASCS/SCS instance uses, to cluster node A.</span></span>

![Abbildung 61: Failovercluster-Manager: Die SAP-Clustergruppe <SID> wird auf Clusterknoten A ausgeführt.][sap-ha-guide-figure-5000]

<span data-ttu-id="7a8b4-1023">_**Abbildung 61:** Failovercluster-Manager: Die SAP-Clustergruppe <*SID*> wird auf Clusterknoten A ausgeführt._</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1023">_**Figure 61:** Failover Cluster Manager: The SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="7a8b4-1024">Im SIOS DataKeeper-Tool für die Verwaltung und Konfiguration erkennen Sie, dass die Daten auf dem freigegebenen Datenträger synchron vom Quellvolume S auf Clusterknoten A auf das Zielvolume S auf Clusterknoten B repliziert werden, also z.B. von **pr1-ascs-0 [10.0.0.40]** nach **pr1-ascs-1 [10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1024">In the SIOS DataKeeper Management and Configuration tool, you can see that the shared disk data is synchronously replicated from the source volume drive S on cluster node A to the target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** to **pr1-ascs-1 [10.0.0.41]**.</span></span>

![Abbildung 62: Replizieren des lokalen Volumes von Clusterknoten A auf Clusterknoten B in SIOS DataKeeper][sap-ha-guide-figure-5001]

<span data-ttu-id="7a8b4-1026">_**Abbildung 62:** Replizieren des lokalen Volumes von Clusterknoten A auf Clusterknoten B in SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1026">_**Figure 62:** In SIOS DataKeeper, replicate the local volume from cluster node A to cluster node B_</span></span>

### <a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> <span data-ttu-id="7a8b4-1027">Failover von Knoten A auf Knoten B</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1027">Failover from node A to node B</span></span>

1. <span data-ttu-id="7a8b4-1028">Wählen Sie eine dieser Optionen, um ein Failover der SAP-Clustergruppe <*SID*> von Clusterknoten A auf Clusterknoten B auszulösen:</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1028">Choose one of these options to initiate a failover of the SAP <*SID*> cluster group from cluster node A to cluster node B:</span></span>
   - <span data-ttu-id="7a8b4-1029">Mithilfe des Failovercluster-Managers</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1029">Use Failover Cluster Manager</span></span>  
   - <span data-ttu-id="7a8b4-1030">Mithilfe der Failovercluster-PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1030">Use Failover Cluster PowerShell</span></span>

   ```PowerShell
   $SAPSID = "PR1"     # SAP <SID>

   $SAPClusterGroup = "SAP $SAPSID"
   Move-ClusterGroup -Name $SAPClusterGroup

   ```
2. <span data-ttu-id="7a8b4-1031">Durch einen Neustart von Clusterknoten A im Windows-Gastbetriebssystem (dadurch wird ein automatisches Failover der SAP-Clustergruppe <*SID*> von Knoten A auf Knoten B ausgelöst).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1031">Restart cluster node A within the Windows guest operating system (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
3. <span data-ttu-id="7a8b4-1032">Durch einen Neustart von Clusterknoten A im Azure-Portal (dadurch wird ein automatisches Failover der SAP-Clustergruppe <*SID*> von Knoten A auf Knoten B ausgelöst).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1032">Restart cluster node A from the Azure portal (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
4. <span data-ttu-id="7a8b4-1033">Durch einen Neustart von Clusterknoten A mit Azure PowerShell (dadurch wird ein automatisches Failover der SAP-Clustergruppe <*SID*> von Knoten A auf Knoten B ausgelöst).</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1033">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>

   <span data-ttu-id="7a8b4-1034">Nach dem Failover wird die SAP-Clustergruppe <*SID*> auf dem Clusterknoten B ausgeführt, z.B. auf **pr1-ascs-1**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1034">After failover, the SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

   ![Abbildung 63: Failovercluster-Manager: Die SAP-Clustergruppe <SID> wird auf Clusterknoten B ausgeführt.][sap-ha-guide-figure-5002]

   <span data-ttu-id="7a8b4-1036">_**Abbildung 63**: Failovercluster-Manager: Die SAP-Clustergruppe <*SID*> wird auf Clusterknoten B ausgeführt._</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1036">_**Figure 63**: In Failover Cluster Manager, the SAP <*SID*> cluster group is running on cluster node B_</span></span>

   <span data-ttu-id="7a8b4-1037">Der freigegebene Datenträger wird jetzt auf Clusterknoten B bereitgestellt. SIOS DataKeeper repliziert Daten vom Quellvolume S auf Clusterknoten B auf das Zielvolume S auf Clusterknoten A, also z.B. von **pr1-ascs-1 [10.0.0.41]** nach **pr1-ascs-0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1037">The shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B to target volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** to **pr1-ascs-0 [10.0.0.40]**.</span></span>

   ![Abbildung 64: SIOS DataKeeper repliziert das lokale Volume von Clusterknoten B auf Clusterknoten A.][sap-ha-guide-figure-5003]

   <span data-ttu-id="7a8b4-1039">_**Abbildung 64:** SIOS DataKeeper repliziert das lokale Volume von Clusterknoten B auf Clusterknoten A._</span><span class="sxs-lookup"><span data-stu-id="7a8b4-1039">_**Figure 64:** SIOS DataKeeper replicates the local volume from cluster node B to cluster node A_</span></span>
