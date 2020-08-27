## <a name="enable-windows-10-automatic-enrollment"></a>Windows 10 otomatik kayıt özelliğini etkinleştirme

Otomatik kayıt, kullanıcıların Windows 10 cihazlarını Intune’a kaydetmesine olanak tanır. Kayıt için kullanıcılar, kişisel cihazlarına iş hesaplarını ekler veya şirkete ait cihazları Azure Active Directory’ye ekler. Arka planda cihaz kaydolur ve Azure Active Directory’ye katılır. Kaydedildikten sonra cihaz, Intune ile yönetilir.

**Önkoşullar**

- Azure Active Directory Premium aboneliği ([deneme aboneliği](https://go.microsoft.com/fwlink/?LinkID=816845))
- Microsoft Intune aboneliği

### <a name="configure-automatic-mdm-enrollment"></a>Otomatik MDM kaydını yapılandırma

1. [Azure Portal](https://portal.azure.com)oturum açın ve **Azure Active Directory**' ı seçin.

   ![Azure portalının ekran görüntüsü](../enrollment/media/windows-enroll/auto-enroll-azure-main.png)

2. **Mobility (MDM ve MAM)** seçeneğini belirleyin.

   ![Azure portalının ekran görüntüsü](../enrollment/media/windows-enroll/auto-enroll-mdm.png)

3. **Microsoft Intune**'u seçin.

   ![Azure portalının ekran görüntüsü](../enrollment/media/windows-enroll/auto-enroll-intune.png)

4. **MDM Kullanıcı kapsamını** yapılandırın. Hangi kullanıcıların cihazlarının Microsoft Intune tarafından yönetilmesi gerektiğini belirtin. Bu Windows 10 cihazlar, Microsoft Intune ile yönetim için otomatik olarak kaydedilebilir.

   - **Hiçbiri** - MDM otomatik kayıt devre dışı
   - **Bazıları** - Windows 10 cihazlarını otomatik olarak kaydedebilecek **Grupları** seçin
   - **Tümü** - Tüm kullanıcılar Windows 10 cihazlarını otomatik olarak kaydedebilir

      > [!IMPORTANT]
      > Windows KCG cihazlarında, MAM Kullanıcı kapsamı, tüm kullanıcılar (veya aynı kullanıcı grupları) için hem MAM Kullanıcı kapsamı hem de MDM Kullanıcı kapsamı (otomatik MDM kaydı) etkin olursa öncelik kazanır. Cihaz MDM kaydı olmayacaktır ve bunları yapılandırdıysanız Windows Information Protection (WıP) Ilkeleri uygulanır.
      >
      > Amacınız Windows KCG cihazları için MDM 'ye otomatik kaydı etkinleştirmek istiyorsanız: MDM Kullanıcı kapsamını **Tümü** **(veya bir**grup belirtin) olarak yapılandırın ve Mam Kullanıcı kapsamını **hiçbiri** (veya **bazılarına**) olarak yapılandırın ve bir grup belirtin ve kullanıcıların hem MDM hem de mam Kullanıcı kapsamları tarafından hedeflenen bir grubun üyesi olmamasını sağlar.
      >
      >[Kurumsal cihazlarda](../enrollment/enrollment-restrictions-set.md#blocking-personal-windows-devices), MDM ve Mam Kullanıcı KAPSAMLARı etkinse MDM Kullanıcı kapsamı öncelikli olur. Cihaz, yapılandırılan MDM 'ye otomatik olarak kaydedilir.

   > [!NOTE]
   > MDM Kullanıcı kapsamı, Kullanıcı nesneleri içeren bir Azure AD grubuna ayarlanmalıdır.

   ![Azure portalının ekran görüntüsü](../enrollment/media/windows-enroll/auto-enroll-scope.png)

5. Aşağıdaki URL'ler için varsayılan değerleri kullanın:
    - **MDM Kullanım Koşulları URL’si**
    - **MDM Bulma URL’si**
    - **MAM uyumluluk URL’si**

6. **Kaydet**’i seçin.

Varsayılan olarak hizmet için iki öğeli kimlik doğrulama etkin değildir. Yine de bir cihaz kaydedilirken iki öğeli kimlik doğrulama önerilir. İki öğeli kimlik doğrulamasını etkinleştirmek için Azure AD’de bir iki öğeli kimlik doğrulaması sağlayıcısı yapılandırmanız ve çok faktörlü kimlik doğrulaması için kullanıcı hesaplarınızı yapılandırmanız gerekir. Bkz. [Azure Multi-Factor Authentication Sunucusunu kullanmaya başlama](/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).