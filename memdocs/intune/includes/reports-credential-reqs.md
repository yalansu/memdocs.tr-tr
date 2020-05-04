<!-- This include is part of the Intune Data Warehouse documentation. -->

## <a name="azure-ad-and-intune-credential-requirements"></a>Azure AD ve Intune kimlik bilgisi gereksinimleri

Kimlik doğrulaması ve yetkilendirme, Azure AD kimlik bilgileri ve Intune rol tabanlı erişim denetimine (RBAC) bağlıdır. Varsayılan olarak kiracınızdaki tüm genel yöneticiler ve Intune hizmet yöneticilerinin Veri ambarına erişimi vardır. Intune **veri ambarı** kaynağına erişim izni vererek daha fazla kullanıcıya erişim sağlamak için Intune rollerini kullanın.

API dahil olmak üzere Intune Veri Ambarı’na erişim önkoşulları şöyledir:

- Kullanıcı şunlardan biri olmalıdır:
  - Azure AD genel yöneticisi
  - Intune hizmet yöneticisi
  - **Intune veri ambarı** kaynağına rol tabanlı erişimi olan kullanıcı
  - [Yalnızca uygulama kimlik doğrulaması](../developer/data-warehouse-app-only-auth.md) kullanılan kullanıcısız kimlik doğrulaması 
