# Metro Ağ Simülasyonu 🚇

Bu proje, metro istasyonları arasında en az aktarmalı veya en hızlı rotayı bulmak için geliştirilmiş bir Python uygulamasıdır. Projede metro ağı bir grafik olarak modellenmiş ve üzerinde **BFS** ve **Dijkstra (A* benzeri)** algoritmaları kullanılarak rota bulma işlemleri yapılmıştır.

---

## 📚 Kullanılan Teknolojiler ve Kütüphaneler

- **Python 3.x**: Proje Python dili ile yazılmıştır.
- **collections.deque**: BFS algoritması için hızlı bir kuyruk yapısı sağlamak amacıyla kullanılmıştır.
- **collections.defaultdict**: Metro hatlarını gruplamak için varsayılan değerlerle çalışan sözlük yapısı.
- **heapq**: En hızlı rota bulma algoritması için öncelik kuyruğu (min-heap) yapısında kullanılmıştır.
- **typing**: Tip ipuçları (type hinting) için kullanılmıştır.

---

## ⚙️ Algoritmaların Çalışma Mantığı

### 1️⃣ BFS (Breadth-First Search) - En Az Aktarma Bulma

BFS, bir grafikte minimum adım sayısı ile hedefe ulaşmak için kullanılan en temel algoritmalardan biridir.

- **Amaç:** Metro istasyonları arasındaki en az aktarmalı (en az geçişli) rotayı bulmak.
- **Nasıl Çalışır:**
  - Başlangıç istasyonundan başlanır.
  - Kuyruk (queue) kullanarak seviyeleri genişleterek en kısa yol aranır.
  - İlk ulaşılan hedef istasyon, minimum aktarma ile ulaşılan istasyondur.
- **Avantaj:** Aktarma sayısını minimize eder, süreyi dikkate almaz.

### 2️⃣ Dijkstra (Min-Heap ile A* benzeri) - En Hızlı Rota Bulma

Bu algoritma, metro ağı üzerindeki istasyonlar arasında en kısa süreyi bulur.

- **Amaç:** Metro istasyonları arasındaki toplam seyahat süresini minimize eden rotayı bulmak.
- **Nasıl Çalışır:**
  - Başlangıç istasyonundan başlanır ve `heapq` modülü ile bir öncelik kuyruğu kullanılır.
  - En düşük toplam süreye sahip yol her seferinde kuyruğun başına gelir.
  - Komşular keşfedildikçe toplam süre güncellenir.
  - Hedef istasyona ulaşıldığında en kısa (en hızlı) yol bulunmuş olur.
- **Not:** Projede A* ismi geçse de burada "heuristic" bir tahmin kullanılmamıştır, yani algoritma saf bir Dijkstra mantığıyla çalışır.

### 🎯 Neden Bu Algoritmalar?

- **BFS**: Aktarma sayısını minimize etmek için grafikte "seviyeye dayalı" tarama gereklidir ve BFS bunun için idealdir.
- **Dijkstra**: Metro gibi ağırlıklı (süre bazlı) grafikte en kısa sürede hedefe ulaşmak için Dijkstra algoritması uygundur.

---

## 🧪 Örnek Kullanım ve Test Sonuçları

### Test Senaryosu 1: AŞTİ'den OSB'ye
En az aktarmalı rota: AŞTİ -> Kızılay -> Kızılay -> Ulus -> Demetevler -> OSB
En hızlı rota (17 dakika): AŞTİ -> Kızılay -> Ulus -> Demetevler -> OSB

## 🚀 Projeyi Geliştirme Fikirleri
Gerçek bir A* algoritması implementasyonu yapılabilir. Örneğin, istasyonlar arası coğrafi mesafeye dayalı bir "heuristic" eklenerek rota hesaplama süresi daha da optimize edilebilir.

Metro ağı verisi sabit kodlanmak yerine JSON dosyası veya veritabanı gibi dış kaynaklardan dinamik olarak alınabilir.

Görsel arayüz (GUI) geliştirilebilir. PyQt, Tkinter veya web tabanlı bir arayüzle metro hattı ve rotalar harita üzerinde gösterilebilir.

İstasyonlar için yoğunluk ve trafik simülasyonu eklenebilir. Yoğun saatlerde hatların daha yavaş çalıştığı veya bekleme sürelerinin arttığı durumlar simüle edilebilir.

Hata toleransı veya "kapalı hat/istasyon" senaryoları eklenerek bakım veya arıza durumunda alternatif rotalar sunulabilir.

Ücret hesaplama modülü eklenebilir. Rotaların uzunluğuna veya aktarma sayılarına göre bilet ücreti dinamik olarak hesaplanabilir.

REST API veya web servisi haline getirilerek rota sorgularının dış sistemler tarafından da yapılması sağlanabilir.