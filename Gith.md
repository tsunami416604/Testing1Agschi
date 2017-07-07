<properties
    pageTitle="VMA RCA"
    description="RCA - Kapsayıcı kapatma - E17 IOPS sınırı"
    infoBubbleText="Son yeniden başlatma işlemi bulundu. Ayrıntıları sağda görebilirsiniz."
    service="microsoft.compute"
    resource="virtualmachines"
    authors="jozender"
    displayOrder=""
    articleId="UnexpectedVMReboot_E17_IOPS_Limit"
    diagnosticScenario="UnexpectedVMReboot"
    selfHelpType="rca"
    supportTopicIds="32411816"
    resourceTags="windows, linux"
    productPesIds="14749"
    cloudEnvironments="public"
/>

# <a name="we-ran-diagnostics-on-your-resource-and-found-an-issue"></a>Kaynağınız üzerinde tanılama işlemi gerçekleştirdik ve bir sorun bulduk

<!--issueDescription-->
**<!--$StartTime--> StartTime <!--/$StartTime--> (UTC)** ile **<!--$EndTime--> EndTime <!--/$EndTime--> (UTC)** saatleri arasında kullanılamaz duruma geldiğini belirledik.
Bu beklenmeyen durum, sanal makinenizin çalışmakta olduğu fiziksel konak düğümü ile Sanal Sabit Disklerinizin (VHD) bulunduğu Azure Depolama hizmetleri arasında **geçici GÇ işlemi zaman aşımları** algılanması sonucu tetiklenen **Azure tarafından başlatılan VM kapatma işleminden** kaynaklanmıştır.
<!--/issueDescription-->

Azure Standart Depolama disklerinin her VHD için 500 IOPS sınırı vardır.  [Azure Sanal Makineler hizmetini En İyi Depolama Performansı için yapılandırma](http://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx) amacına dönük olarak en iyilerinden birkaçını belirledik<br> İş yüküne bağlı olarak bölüştürülmüş bir disk kullanmak veya Konuk VM içindeki Depolama Alanlarını yaplandırmak, sorunun azalmasına yardımcı olabilir.  Sorun devam ederse Premium Depolama’ya geçmeyi de göz önünde bulundurabilirsiniz.<br>
 
Azure’daki uygulamanızın koruma ve yedeklilik düzeyini artırmak için iki veya daha fazla sanal makineyi bir kullanılabilirlik kümesinde gruplandırmanız önerilir.<br>
Yüksek kullanılabilirlik seçenekleri hakkında daha fazla bilgi edinmek için lütfen aşağıdaki makalelere başvurun:<br>
* [Sanal makinelerin kullanılabilirliğini yönetme](https://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability)<br>
* [Sanal makinelerin kullanılabilirliğini yapılandırma](https://azure.microsoft.com/documentation/articles/virtual-machines-how-to-configure-availability)
* [Yönetilen Disklere Genel Bakış](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview)<br>

Microsoft Azure, Azure Portal’da kaynak durumu ve sorun giderme bilgilerine de erişim sağlar.<br>
Azure Kaynak Durumu hakkında daha fazla bilgi edinmek için lütfen aşağıdaki makaleye başvurun:<br>
* [Gelecekte bu senaryoyla ilgili sorunları gidermek üzere Kaynak Durumu Merkezini anlama ve kullanma](https://docs.microsoft.com/azure/resource-health/resource-health-overview)<br>

Bu nedenle yaşamış olabileceğiniz sorunlardan dolayı özür dileriz. Platform sorunu nedeniyle Sanal Makinelerin kullanılabilirliğini etkileyen olay sayısını azaltmak için platformu geliştirme konusunda durmaksızın çalışıyoruz.
