# .gitignore Kuralları ve Pattern Eşleştirme Mantığı

Git, dosyaları izlerken `.gitignore` dosyasındaki kuralları yukarıdan aşağıya doğru okur ve en son eşleşen kuralı uygular.

## 1. Dizin ve Kapsam Kısıtlamaları (`/` Mantığı)
Dizin ayracı (`/`), kuralın etki alanını belirler.
* **`img/` (Global):** Tüm projedeki `img` isimli klasörleri dışlar (örn. `build/img/` veya `src/assets/img/` dahil).
* **`/img/` (Root Sabitleme):** Sadece `.gitignore` dosyasının bulunduğu ana dizindeki (root) `img/` klasörünü dışlar. Alt klasörlere dokunmaz.
* **`build/img/` (Spesifik Yol):** Sadece belirli bir hiyerarşideki hedefi dışlar. Dizin'in ortasında `/` varsa kök dizinden başlatır. Yani `build/img/` = `/build/img/`

## 2. Uzantı ve Karakter Eşleştirme (`*` Wildcard)
Yıldız (`*`) karakteri, herhangi bir uzunluktaki karakter dizisini temsil eder.
* **`*.png`:** Uzantısı `.png` olan tüm dosyaları dışlar.
* **`*serhat.txt`:** Sonu `serhat.txt` ile biten tüm dosyaları dışlar (örn. `eski_serhat.txt`, `log_serhat.txt`).
* **`serhat.*`:** İsmi tam olarak `serhat` olan tüm dosyaları dışlar, uzantı fark etmez (örn. `serhat.csv`, `serhat.json`).
* **`*serhat*.txt`:** Dosya adının herhangi bir yerinde `serhat` geçen tüm `.txt` dosyalarını dışlar.

## 3. Küme Mantığı ve İstisnalar (`!` Negation)
Filtreleme işlemlerinde önce büyük küme dışlanır, ardından istenen spesifik veri `!` işareti ile kümeye geri dahil edilir. Sıralama kritik önem taşır.
```text
*.log       # Kural 1: Tüm .log uzantılı dosyaları engelle.
!hata.log   # Kural 2: Üstteki kuralı ez, sadece hata.log dosyasını repoya dahil et.