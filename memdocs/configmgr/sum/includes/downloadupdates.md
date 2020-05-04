1.  Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin ve **yazılım güncelleştirmeleri** düğümünü seçin.  

2.  Aşağıdaki yöntemlerden birini kullanarak yüklenecek yazılım güncelleştirmesini seçin:  

    -   **Yazılım güncelleştirme grupları** düğümünden bir veya daha fazla yazılım güncelleştirme grubu seçin. Ardından Şeritteki **İndir** ' e tıklayın.  

    -   **Tüm yazılım güncelleştirmeleri** düğümünden bir veya daha fazla yazılım güncelleştirmesi seçin. Ardından Şeritteki **İndir** ' e tıklayın.  

        > [!NOTE]  
        >  **Tüm yazılım güncelleştirmeleri** düğümünde Configuration Manager, yalnızca son 30 gün Içinde yayınlanan **kritik** ve **güvenlik** sınıflandırmasına sahip yazılım güncelleştirmelerini görüntüler.  

        > [!TIP]  
        >  **Tüm yazılım güncelleştirmeleri** düğümünde görüntülenen yazılım güncelleştirmelerini filtrelemek Için **Ölçüt Ekle** ' ye tıklayın. Sık kullandığınız arama ölçütlerini kaydedin ve sonra **arama** sekmesinde kaydedilen aramaları yönetin.  


3.  Yazılım güncelleştirmelerini Indirme Sihirbazı 'nın **dağıtım paketi** sayfasında, aşağıdaki ayarları yapılandırın:  

    -  **Dağıtım paketini seçin**: Dağıtımda olan yazılım güncelleştirmeleri için mevcut bir dağıtım paketini seçmek için bu ayarı seçin.  

        > [!NOTE]  
        >  Sitenin Seçili dağıtım paketine daha önce indirildiği yazılım güncelleştirmeleri yeniden indirilmeyecektir.  

    -  **Yeni dağıtım paketi oluştur**: Dağıtımdaki yazılım güncelleştirmeleri için yeni bir dağıtım paketi oluşturmak için bu ayarı seçin. Aşağıdaki ayarları yapılandırın:  

        -   **Ad**: Dağıtım paketinin adını belirtir. Paketin, paket içeriğini kısaca açıklayan benzersiz bir adı olmalıdır. 50 karakterle sınırlıdır.  

        -   **Açıklama**: Dağıtım paketiyle ilgili bilgi sağlayan bir açıklama belirtin. İsteğe bağlı Açıklama 127 karakterle sınırlıdır.    

        -   **Paket kaynağı**: Yazılım güncelleştirmesi kaynak dosyalarının konumunu belirtir. Kaynak konumu için bir ağ yolu yazın (örneğin `\\server\sharename\path`,) veya ağ konumunu bulmak için **Araştır** ' a tıklayın. Sonraki sayfaya geçmeden önce dağıtım paketi kaynak dosyaları için paylaşılan klasör oluşturun.  

             - Belirtilen konumu başka bir yazılım dağıtım paketinin kaynağı olarak kullanamazsınız.  

             - Dağıtım paketini Configuration Manager oluşturulduktan sonra dağıtım paketi özelliklerinde paket kaynak konumunu değiştirebilirsiniz. Bunu yaparsanız, öncelikle özgün paket kaynağındaki içeriği yeni paket kaynak konumuna kopyalayın.  

             -  SMS sağlayıcısının bilgisayar hesabı ve yazılım güncelleştirmelerini indirmek için Sihirbazı çalıştıran kullanıcı, indirme konumuna **yazma** izinlerine sahip olmalıdır. İndirme konumuna erişimi kısıtlayın. Bu kısıtlama, saldırganların yazılım güncelleştirme kaynak dosyalarıyla izinsiz değiştirilme riskini azaltır.  

        - **İkili değişiklik çoğaltmasını etkinleştir**: siteler arasındaki ağ trafiğini en aza indirmek için bu ayarı etkinleştirin. İkili farklar çoğaltması (BDR), paket içeriğinin tamamını güncelleştirmek yerine yalnızca pakette değiştirilen içeriği güncelleştirir. Daha fazla bilgi için bkz. [ikili farklar çoğaltması](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

4.  **Dağıtım noktaları** sayfasında, yazılım güncelleştirme dosyalarını barındıracak dağıtım noktalarını veya dağıtım noktası gruplarını belirtin. Dağıtım noktaları hakkında daha fazla bilgi için bkz. [Dağıtım noktası yapılandırmaları](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Bu sayfa sadece yeni yazılım güncelleştirme dağıtım paketi oluşturduğunuzda kullanılabilir.  

5.  **Dağıtım ayarları** sayfası, yalnızca yeni bir yazılım güncelleştirme dağıtım paketi oluşturduğunuzda kullanılabilir. Aşağıdaki ayarları belirtin:  

    -   **Dağıtım önceliği**: Bu ayarı, dağıtım paketi için dağıtım önceliğini belirtmek için kullanın. Dağıtım önceliği, dağıtım paketi alt sitelerdeki dağıtım noktalarına gönderildiğinde geçerlidir. Dağıtım paketleri öncelik sırasıyla gönderilir: yüksek, orta veya düşük. Benzer önceliklere sahip paketler oluşturulma sıralarına göre gönderilir. Biriktirme listesi yoksa, paket önceliğe bakılmaksızın hemen işlenir. Varsayılan olarak, site, **Orta** önceliğe sahip paketleri gönderir.  

    -   **İsteğe bağlı dağıtım Için etkinleştir**: Bu özellik ve istemcinin geçerli sınır grubunda yapılandırılmış dağıtım noktalarına isteğe bağlı içerik dağıtımını etkinleştirmek için bu ayarı kullanın. Bu ayarı etkinleştirdiğinizde, yönetim noktası bir istemci paket içeriğini istediğinde ve içerik kullanılabilir olmadığında, dağıtım Yöneticisi 'nin içeriği bu dağıtım noktalarına dağıtması için bir tetikleyici oluşturur. Daha fazla bilgi için bkz. [isteğe bağlı içerik dağıtımı](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).  

    -   **Önceden hazırlanan dağıtım noktası ayarları**: Bu ayarı, önceden hazırlanmış dağıtım noktalarına içeriğin nasıl dağıtılmasını istediğinizi belirtmek için kullanın. Aşağıdaki seçeneklerden birini belirleyin:  

        -   **Paketler dağıtım noktalarına atandığında içeriği otomatik olarak indir**: Bu ayarı, önceden hazırlama ayarlarını yoksaymak ve içeriği dağıtım noktasına dağıtmak için kullanın.   

        -   **Yalnızca dağıtım noktasındaki içerik değişikliklerini indir**: Bu ayarı, dağıtım noktasındaki başlangıç içeriğini önceden hazırlamak ve ardından içerik değişikliklerini dağıtım noktasında dağıtmak için kullanın.  

        -   **Bu paketin içeriğini dağıtım noktasına el ile kopyala**: Bu ayarı, her zaman dağıtım noktasındaki içeriği önceden hazırlamak için kullanın. Bu seçenek varsayılandır.  

        İçeriğin dağıtım noktalarına önceden hazırlanması hakkında daha fazla bilgi için bkz. [Önceden hazırlanmış içeriği kullanma](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  


6.  **Yükleme konumu** sayfasında, Configuration Manager yazılım güncelleştirme kaynak dosyalarını indirmek için kullanacağı konumu belirtin. Aşağıdaki seçeneklerden birini kullanın:  

    -   **Yazılım güncelleştirmelerini İnternet 'Ten indir**: yazılım güncelleştirmelerini İnternet 'teki konumundan indirmek için bu ayarı seçin. Bu seçenek varsayılandır.  

    -   **Yazılım güncelleştirmelerini Ağımdaki bir konumdan indir**: yazılım güncelleştirmelerini yerel bir dizinden veya paylaşılan klasörden indirmek için bu ayarı seçin. Bu ayar, Sihirbazı çalıştıran bilgisayarın İnternet erişimi olmadığında yararlıdır. İnternet erişimi olan herhangi bir bilgisayar, yazılım güncelleştirmelerini indirebilir indirebilir. Ardından, bunları, Sihirbazı çalıştıran bilgisayardan erişilebilen yerel ağda bir yerde saklayın.  


7.  **Dil seçimi** sayfasında, sitenin seçili yazılım güncelleştirmelerini indirdiği dilleri seçin. Site yalnızca seçili dillerde kullanılabiliyorsa bu güncelleştirmeleri indirir. Dile özgü olmayan yazılım güncelleştirmeleri her zaman indirilir. Varsayılan olarak, sihirbaz, yazılım güncelleştirme noktası özelliklerinde yapılandırdığınız dilleri seçer. Sonraki sayfaya geçmeden önce en az bir dil seçilmelidir. Yalnızca bir yazılım güncelleştirmesinin desteklemediği dilleri seçtiğinizde, güncelleştirme için indirme başarısız olur.  

8. **Özet** sayfasında, sihirbazda seçtiğiniz ayarları doğrulayın ve ardından **İleri** ' ye tıklayarak yazılım güncelleştirmelerini indirin.  

9. **Tamamlama** sayfasında, yazılım güncelleştirmelerinin başarıyla indirildiğini doğrulayın ve ardından **Kapat**' a tıklayın.  
