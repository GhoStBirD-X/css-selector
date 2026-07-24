# 5.3 CSS Selectors

Dokumentasi ini menjelaskan secara detail kode yang telah saya buat pada latihan **CSS Selectors**. Latihan ini bertujuan untuk memahami berbagai cara menargetkan (memilih) elemen HTML menggunakan CSS Selector, mulai dari selector paling dasar (element selector) sampai selector yang lebih spesifik (id, class, attribute, dan universal selector).

## Struktur Proyek

```
5.3 CSS Selectors/
├── index.html              # Halaman HTML utama (soal/latihan)
├── style.css                # File CSS tempat saya menulis jawaban
└── solution/
    ├── solution.html        # Halaman HTML kunci jawaban
    └── solution-style.css   # File CSS kunci jawaban (referensi)
```

## Penjelasan `index.html`

File ini berisi struktur HTML yang menjadi "bahan uji" untuk setiap jenis selector. Setiap elemen sengaja diberi `class`, `id`, dan `attribute` yang berbeda-beda supaya saya bisa berlatih menargetkan mereka satu per satu lewat CSS.

```html
<p class="note">1. The element selector targets elements based on their HTML tag name.</p>

<ol>
  <li class="note" value="2">Class selectors target elements based on the value of the class attribute.</li>
  <li class="note" id="id-selector-demo" value="3">ID selectors target elements based on the value of the id attribute.</li>
  <li class="note" value="4">Attribute selectors target elements based on their attributes and values.</li>
  <li class="note" value="5">The universal selector targets all elements.</li>
</ol>
```

Rincian elemen-elemennya:

| Elemen | Class | ID | Attribute | Tujuan |
|---|---|---|---|---|
| `<p>` | `note` | - | - | Target untuk **element selector** (tag `p`) |
| `<li value="2">` | `note` | - | `value="2"` | Target untuk **class selector** (`.note`) |
| `<li value="3">` | `note` | `id-selector-demo` | `value="3"` | Target untuk **id selector** (`#id-selector-demo`) |
| `<li value="4">` | `note` | - | `value="4"` | Target untuk **attribute selector** (`[value="4"]`) |
| `<li value="5">` | `note` | - | `value="5"` | Target untuk **universal selector** (`*`) |

File ini juga memuat 5 komentar `TODO` yang menjadi instruksi/soal latihan, dan setiap TODO dijawab lewat file `style.css`.

## Penjelasan `style.css` (Jawaban Saya)

Berikut isi lengkap kode CSS yang saya tulis, beserta penjelasan baris demi baris.

### 1. Styling dasar untuk elemen `<ol>` (sudah disediakan, bukan bagian dari soal)

```css
ol {
  margin-left: -40px;
  margin-top: -20px;
  list-style-position: inside;
}
```

- `margin-left: -40px;` menggeser daftar `<ol>` ke kiri sebanyak 40px (nilai negatif berarti menarik elemen ke arah kiri, biasanya untuk menghilangkan indentasi default list).
- `margin-top: -20px;` menarik elemen ke atas sebanyak 20px untuk merapikan jarak dengan elemen di atasnya (`<h2>`).
- `list-style-position: inside;` membuat nomor urut list (`1.`, `2.`, dst.) berada **di dalam** kotak konten `<li>`, sehingga teks akan rata dengan angka penomoran, bukan menjorok keluar.

### 2. TODO 1 — Element Selector

```css
p {
  color: red;
}
```

- Selector `p` adalah **element selector** (selector tag), yaitu selector paling dasar yang menargetkan **semua** elemen dengan nama tag tertentu — dalam kasus ini semua tag `<p>` di halaman.
- Efeknya: semua teks di dalam elemen `<p>` akan berwarna merah (`red`).
- Karena hanya ada satu `<p>` di halaman ini, maka hanya paragraf pembuka ("1. The element selector...") yang berubah warna.

### 3. TODO 2 — Class Selector

```css
.note {
  font-size: 20px;
}
```

- Tanda titik (`.`) di depan `note` menandakan ini adalah **class selector**.
- Class selector menargetkan **semua elemen** yang memiliki atribut `class="note"`, tidak peduli jenis tag-nya (bisa `<p>`, `<li>`, `<div>`, dsb).
- Efeknya: ukuran font menjadi `20px` untuk semua elemen ber-class `note` — yaitu `<p>` dan keempat `<li>` di dalam `<ol>`, karena semuanya memiliki `class="note"`.
- Class selector sangat berguna untuk menerapkan style yang sama ke banyak elemen berbeda sekaligus (reusable).

### 4. TODO 3 — ID Selector

```css
#id-selector-demo {
  color: green;
}
```

- Tanda pagar (`#`) di depan `id-selector-demo` menandakan ini adalah **ID selector**.
- ID selector menargetkan **satu elemen spesifik** yang memiliki atribut `id="id-selector-demo"`. Berbeda dengan class, nilai `id` seharusnya unik dan hanya boleh dipakai oleh satu elemen dalam satu halaman.
- Efeknya: hanya `<li>` ketiga (yang membahas tentang ID selector itu sendiri) yang berubah warna menjadi hijau (`green`).
- ID selector memiliki **spesifisitas (specificity)** yang lebih tinggi dibanding class selector, artinya jika terjadi konflik aturan CSS, ID selector akan "menang".

### 5. TODO 4 — Attribute Selector

```css
li[value="4"]{
  color: blue;
}
```

- Ini adalah **attribute selector**, ditulis dengan format `tag[attribute="value"]`.
- `li[value="4"]` berarti: pilih semua elemen `<li>` yang memiliki atribut `value` dengan nilai persis `"4"`.
- Efeknya: hanya `<li>` keempat (yang membahas attribute selector) yang teksnya berubah menjadi biru (`blue`), karena hanya elemen itu yang memiliki `value="4"`.
- Attribute selector sangat berguna ketika kita ingin menargetkan elemen berdasarkan atribut HTML tertentu (misalnya `type`, `href`, `value`, `data-*`) tanpa harus menambahkan class atau id baru.

### 6. TODO 5 — Universal Selector

```css
* {
  text-align: center;
}
```

- Tanda bintang (`*`) adalah **universal selector**, yang menargetkan **seluruh elemen** yang ada di dalam dokumen HTML tanpa terkecuali.
- Efeknya: seluruh teks pada halaman (judul `<h1>`, `<h2>`, paragraf, dan semua item list) menjadi rata tengah (`text-align: center`).
- Universal selector adalah selector dengan cakupan paling luas, sehingga harus digunakan dengan hati-hati karena akan memengaruhi seluruh elemen di halaman, termasuk elemen yang mungkin tidak ingin diubah.

## Ringkasan Urutan Spesifisitas (Specificity)

Dari yang paling lemah ke paling kuat, kelima jenis selector yang dipelajari pada latihan ini memiliki urutan prioritas sebagai berikut apabila terjadi konflik aturan:

1. **Universal selector** (`*`) — prioritas terendah
2. **Element selector** (`p`, `li`, dst.)
3. **Class selector** (`.note`)
4. **Attribute selector** (`[value="4"]`) — setara dengan class selector
5. **ID selector** (`#id-selector-demo`) — prioritas tertinggi

Itulah sebabnya pada latihan ini, meskipun `* { text-align: center; }` diterapkan ke semua elemen, warna teks (`color`) dari `p`, `.note` (khususnya `#id-selector-demo` dan `li[value="4"]`) tetap terlihat karena `text-align` dan `color` adalah properti CSS yang berbeda sehingga tidak saling menimpa (override).

## Perbandingan dengan `solution/solution-style.css`

File `solution-style.css` pada folder `solution/` berisi kunci jawaban resmi dari latihan ini. Setelah dibandingkan, jawaban yang saya tulis di `style.css` sudah **sesuai** dengan kunci jawaban untuk TODO 1 sampai TODO 4 (element, class, id, dan attribute selector menghasilkan CSS yang identik).

Perbedaan kecil hanya ada pada **TODO 5**:
- Instruksi komentar pada `solution-style.css` menyebutkan `font-family: sans-serif;`, namun kode aktual pada kunci jawaban tetap menggunakan `text-align: center;` — sama seperti jawaban saya. Jadi secara hasil akhir, jawaban saya sudah konsisten dengan kunci jawaban yang sebenarnya diterapkan.

## Kesimpulan

Melalui latihan ini saya belajar 5 jenis CSS selector dasar:

1. **Element Selector** (`p`) — menargetkan berdasarkan nama tag.
2. **Class Selector** (`.note`) — menargetkan berdasarkan atribut `class`, bisa dipakai berulang di banyak elemen.
3. **ID Selector** (`#id-selector-demo`) — menargetkan satu elemen unik berdasarkan atribut `id`.
4. **Attribute Selector** (`[value="4"]`) — menargetkan berdasarkan atribut dan nilainya secara spesifik.
5. **Universal Selector** (`*`) — menargetkan seluruh elemen di halaman.

Kelima selector ini adalah dasar penting dalam CSS karena hampir semua styling yang lebih kompleks (combinator, pseudo-class, pseudo-element) dibangun di atas pemahaman kelima selector dasar ini.
