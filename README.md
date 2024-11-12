# Apache Superset Nedir?

Apache Superset, büyük veri kümeleri üzerinde hızlı, sezgisel ve etkileşimli veri keşfi sağlayan açık kaynaklı bir veri görselleştirme ve BI (Business Intelligence) aracıdır. Veri analistleri, veri mühendisleri ve karar vericilere, veriyi etkili bir şekilde anlamalarına yardımcı olacak güçlü araçlar sunar.

## Superset'in Özellikleri

- **Görselleştirme Çeşitliliği:** Çeşitli grafik türleri (çizgi grafiği, pasta grafiği, haritalar vb.) ile verileri görselleştirmenizi sağlar.
- **SQL Editörü:** Veritabanınıza bağlanıp SQL sorguları çalıştırabileceğiniz, sonuçları hızlıca inceleyebileceğiniz bir arayüz sağlar.
- **Dashboard Desteği:** Grafik ve tabloları bir araya getirerek dinamik dashboard'lar oluşturabilirsiniz. Bu dashboard'lar anlık verilerle güncellenebilir ve özelleştirilebilir.
- **Etkileşimli Filtreleme:** Dashboard'lardaki grafiklerdeki filtreleri kullanarak veri kümelerini belirli kriterlere göre ayırabilir ve analiz edebilirsiniz.
- **Güvenlik ve Yetkilendirme:** Kullanıcı yetkilendirme seçenekleri ile erişim kontrolü sağlar, böylece kullanıcıların sadece yetkili oldukları verilere erişmesini sağlarsınız.

## Superset Mimarisi

Superset, bir web uygulaması olarak çalışır ve backend olarak çeşitli veritabanlarını destekler. Docker Compose ile kurulumda Superset, genellikle üç ana bileşenle yapılandırılır:

1. **Web Sunucusu (Frontend):** Kullanıcı arayüzü ve görselleştirme bileşenlerini sağlar.
2. **Veritabanı (Metadata Database):** Superset'in kendi verilerini (kullanıcı bilgileri, dashboard ayarları vb.) sakladığı veritabanıdır.
3. **Cache Sunucusu:** Redis veya benzeri bir cache sistemi ile Superset'in daha hızlı çalışmasını sağlar.

## Superset'in Avantajları

- **Açık Kaynaklı ve Ücretsiz:** Apache lisansı ile sunulması, kullanıcı topluluğunun katkıda bulunmasına olanak tanır.
- **Esnek Veri Kaynağı Desteği:** Birçok farklı veri kaynağı ile kolayca entegre olur.
- **Veri Güvenliği:** Kurumsal seviyede veri güvenliği ve kullanıcı bazlı erişim kontrolü sunar.
- **Yüksek Performanslı Sorgu ve Görselleştirme:** Büyük veri kümelerinde bile hızlı veri işleme ve görselleştirme özelliklerine sahiptir.

## Docker Compose ile Superset Kurulumu

- Superset’i Docker Compose ile kurmak, hızlı ve kolay bir yöntemdir. Docker Compose dosyanızı çalıştırarak tüm gerekli servisleri (Superset, Redis, veritabanı) başlatabilirsiniz. Aşağıda tipik bir Superset Docker Compose dosyasının yapısı bulunmaktadır:

```bash
docker compose up -d
```

# Veritabanı Bağlantıları
- Bazı veri tabanları ön tanımlı olarak imajda yüklü gelmiyor bunları `docker-compose.yml` dosyasında  `command:` bölümüne ekleyebilirsiniz.
- [Connecting to Databases](https://superset.apache.org/docs/configuration/databases/)
```bash
    command:
      - /bin/sh
      - -c
      - |
        pip install pymssql cx_Oracle && # Bu kısma pip komutlarını ekleyebilirsiniz.
        superset db upgrade &&
        superset init &&
        superset fab create-admin --username admin --firstname Superset --lastname Admin --email admin@superset.com --password admin &&
        superset run -h 0.0.0.0 -p 8088
    volumes:
```
