# YMGK Dönem Projesi – CMAK Çift Kirişli Portal Vinç


## Proje konusu

**CMAK (Çakmak Vinç San. ve Tic. A.Ş.) – Çift Kirişli Portal Vinç + HoistSense+ (SAMİB)**

Bu projede SAMİB üyesi Çakmak Vinç'in çift kirişli portal vinci, yeni **Makine Emniyeti Yönetmeliği (2023/1230/AB)** açısından inceleniyor. Yönetmelik 16 Ekim 2026 tarihli Resmî Gazete'de yayımlandı ve 20 Ocak 2027'de yürürlüğe giriyor. İnceleme şu üç parçadan oluşuyor:

- **Emniyet fonksiyonları:** aşırı yük sınırlama, acil durdurma, limitler
- **Siber güvenlik:** HoistSense+ MK-III'ün WiFi / 4G / Ethernet bulut bağlantısı ve 433 MHz kablosuz yük paylaşımı
- **Yeni yönetmelik maddeleri:** EK-3 1.1.9 (bozulmaya karşı koruma) ve 1.2.1 (kontrol sistemlerinin güvenliği)

| Bileşen | Açıklama |
|---|---|
| Makine | Çift kirişli portal vinç (160 tona kadar, 40 m açıklık) |
| Kaldırma grubu | NXS serisi elektrikli halatlı vinç |
| İzleme sistemi | HoistSense+ MK-III: yük tartımı, fren izleme, SWP, bulut bağlantısı |

## Haftalık laboratuvar föyleri

| # | Föy | Çıktı | Dosya |
|---|---|---|---|
| 1 | Safety Architecture | Safety Function Map | [lab1_Gizem_Dusmez.pdf](lab-1-safety-architecture/lab1_Gizem_Dusmez.pdf) |
| 2 | IEC 62443 Mini Workshop | Zone / Conduit Diagram | [lab2_Gizem_Dusmez.pdf](lab-2-iec62443-zone-conduit/lab2_Gizem_Dusmez.pdf) |
| 3 | Threat & Risk + Risk Matrix | Risk Register | [lab3_Gizem_Dusmez.pdf](lab-3-threat-risk-matrix/lab3_Gizem_Dusmez.pdf) |
| 4 | Secure Remote Access | Secure Architecture | [lab4_Gizem_Dusmez.pdf](lab-4-secure-remote-access/lab4_Gizem_Dusmez.pdf) |
| 5 | SBOM / CVE / Patch | Vulnerability Decision | [lab5_Gizem_Dusmez.pdf](lab-5-sbom-cve-patch/lab5_Gizem_Dusmez.pdf) |
| 6 | CRA Incident Simulation | Incident Workflow | [lab6_Gizem_Dusmez.pdf](lab-6-cra-incident-simulation/lab6_Gizem_Dusmez.pdf) |
| 7 | AI Safety Challenge | AI Fail-Safe Decision | [lab7_Gizem_Dusmez.pdf](lab-7-ai-safety-challenge/lab7_Gizem_Dusmez.pdf) |
| – | SWOT Analizi | – | *Hazırlanıyor* |

## Föy özetleri

**Lab 1 – Safety Architecture:** Ana emniyet fonksiyonu aşırı yük sınırlamadır: yük hücresi kapasite aşımını algılar, kaldırma durur ve yalnızca indirmeye izin verilir. Tahmini PLr değeri **d**'dir. Dijital kesişim noktası HoistSense+ bulut bağlantısıdır.

**Lab 2 – IEC 62443:** Vinç ağı beş bölgeye ayrıldı: Z0 Emniyet, Z1 Kontrol, Z2 Bakım/DMZ, Z3 Kurumsal ve Z4 Dış. Bölgeler arasında beş geçiş (C1–C5) tanımlandı. Z0 bölgesine ağ üzerinden yazma erişimi yoktur.

**Lab 3 – Risk Matrix:** Üç saldırı senaryosu L × S × E yöntemiyle puanlandı:
- S1: Bulut üzerinden aşırı yük eşiğinin değiştirilmesi, skor 12 (Yüksek)
- S2: 433 MHz kanalında replay saldırısı, skor 3
- S3: SWP / fren aşınma verisinin sıfırlanması, skor 6

S2 ve S3'ün skoru düşük olsa da şiddet değeri 3 olduğu için öncelik listesinde öne alındı.

**Lab 4 – Secure Remote Access:** Uzak erişim mimarisi beş ilkeyle yeniden tasarlandı: ara nokta (jump server), VPN, MFA ile kişisel hesap, tam kayıt ve varsayılan kapalı. Emniyet fonksiyonlarının HoistSense+ yazılımından bağımsız çalışması bir gereksinim olarak tanımlandı.

**Lab 5 – SBOM / CVE / Patch:** Kritik CVE (CVSS 9.8), HoistSense+ MK-III'ün haberleşme kütüphanesine uyarlandı. Üç şart (bileşen var, sürüm etkileniyor, buluttan ulaşılabilir) sağlandığı için CVE vinci gerçekten etkiliyor. Kararlar:
- Üretim durdurulmaz; bulut bağlantısı kesilir ve vinç yerel modda çalışır.
- Yama sırasıyla test tezgâhında, tek vinçte ve sonra tüm vinçlerde uygulanır.
- Değişen kod emniyetle ilgiliyse aşırı yük fonksiyonu yeniden test edilir.
- Yama uygulanamıyorsa telafi edici önlem: yerel mod, segmentasyon, ağ izleme ve vardiya başı fonksiyon testi.

**Lab 6 – CRA Incident Simulation:** Servis hesabına yetkisiz giriş senaryosu vince uyarlandı. Senaryodaki ışık perdesi parametrelerinin vinçteki karşılığı aşırı yük eşiği ve kalibrasyondur. Müdahale sırası:
1. Önce emniyet: yük indirilir, vinç kilitlenir.
2. Ardından kanıt: kart resetlenmez, loglar korunur.
3. CRA zaman çizgisi: 24 saatte erken uyarı, 72 saatte bildirim, 14 günde son rapor. Bildirim yükümlülüğü imalatçıdadır (CMAK → ENISA/CSIRT).

**Lab 7 – AI Safety Challenge:** Vince YZ'li kamerayla "yük altında personel algılama" eklenmesi planlanan bir senaryo olarak değerlendirildi. Temel ilke: YZ yalnızca destek fonksiyonudur; asıl emniyet YZ'den bağımsız, sertifikalı bir kanalda kalır. Üç başarısızlık için güvenli davranış:
- Model yanlış sınıflandırırsa: fail-safe ve human override.
- Girdi manipüle edilirse: monitoring ve çapraz kontrol.
- Güven skoru düşerse: confidence threshold ve fallback.

Ayrıca yeni Makine Emniyeti Yönetmeliği EK-1 Kısım A ve AB Yapay Zekâ Yasası açısından da değerlendirildi.

## Not

CMAK'ın iç erişim mimarisi ve emniyet devresinin ayrıntıları kamuya açık değildir. Föylerde bu noktalar **"varsayım"** olarak işaretlenmiştir. Teknik veriler cmak.com ürün sayfalarından alınmıştır.

## Kaynaklar

- [Makine Emniyeti Yönetmeliği (2023/1230/AB) – RG 16.10.2026, Sayı 33402](https://www.alomaliye.com/2026/10/16/makine-emniyeti-yonetmeligi-2023-1230-ab/)
- [CMAK – Portal Vinç](https://cmak.com/portal-vinc/)
- [CMAK – HoistSense+](https://cmak.com/hoistsense/)
- [CMAK – CMK Serisi Halatlı Vinç](https://cmak.com/cmk-serisi-elektrikli-halatli-vinc/)
- [SAMİB – Mevcut Üyeler](https://samib.org.tr/mevcut-uyeler/)
