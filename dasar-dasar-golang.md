# Dasar-Dasar Golang
## Daftar Isi
 - [Hello, World!](#hello-world)
 - [Komentar](#komentar)
 - [Variabel](#variabel)
 - [Tipe Data](#tipe-data)
 - [Konstanta](#konstanta)
 - [Operator](#operator)
 - [Seleksi Kondisi](#seleksi-kondisi)
 - [Perulangan](#perulangan)
 - [Array](#array)
 - [Slice](#slice)
 - [Map](#map)
 - [Fungsi](#fungsi)
 - [Fungsi Multiple Return](#fungsi-multiple-return)
 - [Fungsi Variadic](#fungsi-variadic)
 - [Fungsi Closure](#fungsi-closure)
 - [Fungsi sebagai parameter](#fungsi-sebagai-parameter)
 - [Pointer](#pointer)
 - [Struct](#struct)
 - [Latihan](#latihan)

## Hello, World!
Kita akan memulai dengan sebuah program hello world sederhana. Untuk memulai, buatlah folder proyek, dan buatlah sebuah file bernama `main.go`. Pembuatan file dapat dilakukan melalui terminal menggunakan perintah `touch <nama file>`. File berekstensi .go adalah file yang dapat diproses oleh Go. Berikut merupakan contoh kode program hello world.

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello world")
}
```

Untuk menjalankan program, gunakan perintah `go run <nama file>.go`. 

Kita akan membedah program hello world kita,
1. `package main` <br/>
	Setiap program harus memiliki package, dan satu program harus memiliki satu file dengan nama package main. File dengan package main akan dieksekusi pertama kali ketika program dijalankan. Selain dari package main, sebuah file dengan package `<nama package>` harus berada dalam folder bernama `<nama package>`.
2. `import "fmt"` <br/>
    Import digunakan untuk mengimport atau menggunakan package lain pada program kita. Package `fmt` adalah package bawaan Go yang berisi utility I/O.
3. `func main()` <br/>
    `func main()` adalah fungsi main, fungsi main adalah fungsi yang harus ada pada sebuah program dan harus berada pada file dengan package main. Fungsi tersebut adalah fungsi yang pertama kali dipanggil saat eksekusi sebuah program. 
4. `fmt.Println()` <br/>
    `fmt.Println()` adalah fungsi yang berada pada package `fmt` yang sebelumnya di-import. Fungsi `Println` digunakan untuk mencetak teks ke console diikuti dengan karakter newline.

## Komentar
Komentar biasa dimanfaatkan untuk menyisipkan catatan pada kode program, menulis penjelasan/deskripsi mengenai suatu blok kode, atau bisa juga digunakan untuk men-non-aktifkan kode yang tidak digunakan. Komentar akan diabaikan ketika kompilasi maupun eksekusi program.

Sama seperti C atau C++, terdapat 2 jenis komentar di Go,  _inline_  &  _multiline_.

### Komentar Inline
Penulisan komentar jenis ini di awali dengan tanda  **double slash**  (`//`) lalu diikuti pesan komentarnya. Komentar inline hanya berlaku untuk satu baris pesan saja. Jika pesan komentar lebih dari satu baris, maka tanda  `//`  harus ditulis lagi di baris selanjutnya.

```go
package main

import "fmt"

func main() {
    // komentar kode
    // menampilkan pesan hello world
    fmt.Println("hello world")

    // fmt.Println("baris ini tidak akan dieksekusi")
}
```

### Komentar Multiline
Komentar yang cukup panjang akan lebih rapi jika ditulis menggunakan komentar multiline. Ciri dari komentar jenis ini adalah penulisannya diawali dengan tanda  `/*`  dan diakhiri  `*/`.

```go
/*
    komentar kode
    menampilkan pesan hello world
*/
fmt.Println("hello world")

// fmt.Println("baris ini tidak akan dieksekusi")
```

## Variabel
Go mengadopsi dua jenis penulisan variabel, yaitu yang dituliskan tipe data-nya, dan juga yang tidak. Kedua cara tersebut valid dan tujuannya sama, pembedanya hanya cara penulisannya saja.

Pada chapter ini akan dikupas tuntas tentang macam-macam cara deklarasi variabel.

### Deklarasi Variabel Beserta Tipe Data

Go memiliki aturan cukup ketat dalam hal penulisan variabel. Ketika deklarasi, tipe data yg digunakan harus dituliskan juga. Istilah lain dari konsep ini adalah  **manifest typing**.

Berikut adalah contoh cara pembuatan variabel yang tipe datanya harus ditulis. Silakan tulis pada project baru atau pada project yang sudah ada, bebas. Pastikan saja untuk setiap project baru untuk tidak lupa inisialisasi project menggunakan command  `go mod init <nama-project>`. Ok lanjut.

```go
package main

import "fmt"

func main() {
    var firstName string = "john"

    var lastName string
    lastName = "wick"

    fmt.Printf("halo %s %s!\n", firstName, lastName)
}
```

Keyword  `var`  di atas digunakan untuk deklarasi variabel, contohnya bisa dilihat pada  `firstName`  dan  `lastName`.

Nilai variabel  `firstName`  diisi langsung ketika deklarasi, berbeda dibanding  `lastName`  yang nilainya diisi setelah baris kode deklarasi, hal seperti ini diperbolehkan di Go.

### Deklarasi Variabel Menggunakan Keyword  `var`
Pada kode sebelumnya bisa dilihat bagaimana sebuah variabel dideklarasikan dan diisi nilainya. Keyword  `var`  digunakan untuk membuat variabel baru.

Skema penggunaan keyword var:

```go
var <nama-variabel> <tipe-data>
var <nama-variabel> <tipe-data> = <nilai>
```

Contoh:

```go
var lastName string
var firstName string = "john"
```

Nilai variabel bisa di-isi langsung pada saat deklarasi variabel.

#### Penggunaan Fungsi  `fmt.Printf()`

Fungsi ini digunakan untuk menampilkan output dalam bentuk tertentu. Kegunaannya sama seperti fungsi  `fmt.Println()`, hanya saja struktur outputnya didefinisikan di awal.

Perhatikan bagian  `"halo %s %s!\n"`, karakter  `%s`  di situ akan diganti dengan data  `string`  yang berada di parameter ke-2, ke-3, dan seterusnya.

Contoh lain, ketiga baris kode berikut ini akan menghasilkan output yang sama, meskipun cara penulisannya berbeda.

```go
fmt.Printf("halo john wick!\n")
fmt.Printf("halo %s %s!\n", firstName, lastName)
fmt.Println("halo", firstName, lastName + "!")
```

Tanda plus (`+`) jika ditempatkan di antara string, fungsinya adalah untuk penggabungan string atau  _string concatenation_.

Fungsi  `fmt.Printf()`  tidak menghasilkan baris baru di akhir text, oleh karena itu digunakanlah literal  _newline_  yaitu  `\n`, untuk memunculkan baris baru di akhir. Hal ini sangat berbeda jika dibandingkan dengan fungsi  `fmt.Println()`  yang secara otomatis menghasilkan new line (baris baru) di akhir.

### Deklarasi Variabel Tanpa Tipe Data
Selain  _manifest typing_, Go juga mengadopsi konsep  **type inference**, yaitu metode deklarasi variabel yang tipe data-nya ditentukan oleh tipe data nilainya, cara kontradiktif jika dibandingkan dengan cara pertama. Dengan metode jenis ini, keyword  `var`  dan tipe data tidak perlu ditulis.

```go
var firstName string = "john"
lastName := "wick"

fmt.Printf("halo %s %s!\n", firstName, lastName)
```

Variabel  `lastName`  dideklarasikan dengan menggunakan metode type inference. Penandanya tipe data tidak dituliskan pada saat deklarasi. Pada penggunaan metode ini, operand  `=`  harus diganti dengan  `:=`  dan keyword  `var`  dihilangkan.

Tipe data  `lastName`  secara otomatis akan ditentukan menyesuaikan value atau nilai-nya. Jika nilainya adalah berupa  `string`  maka tipe data variabel adalah  `string`. Pada contoh di atas, nilainya adalah string  `"wick"`.

Diperbolehkan untuk tetap menggunakan keyword  `var`  pada saat deklarasi meskipun tanpa menuliskan tipe data, dengan ketentuan tidak menggunakan tanda  `:=`, melainkan tetap menggunakan  `=`.

```go
// menggunakan var, tanpa tipe data, menggunakan perantara "="
var firstName = "john"

// tanpa var, tanpa tipe data, menggunakan perantara ":="
lastName := "wick"
```

Kedua deklarasi di atas maksudnya sama. Silakan pilih yang nyaman di hati.

Tanda  `:=`  hanya digunakan sekali di awal pada saat deklarasi. Untuk assignment nilai selanjutnya harus menggunakan tanda  `=`, contoh:

```go
lastName := "wick"
lastName = "ethan"
lastName = "bourne"
```

> Perlu diketahui, deklarasi menggunakan  `:=`  hanya bisa dilakukan di dalam blok fungsi.

### Deklarasi Multi Variabel

Go mendukung metode deklarasi banyak variabel secara bersamaan, caranya dengan menuliskan variabel-variabel-nya dengan pembatas tanda koma (`,`). Untuk pengisian nilainya-pun diperbolehkan secara bersamaan.

```go
var first, second, third string
first, second, third = "satu", "dua", "tiga"
```

Pengisian nilai juga bisa dilakukan bersamaan pada saat deklarasi. Caranya dengan menuliskan nilai masing-masing variabel berurutan sesuai variabelnya dengan pembatas koma (`,`).

```go
var fourth, fifth, sixth string = "empat", "lima", "enam"
```

Kalau ingin lebih ringkas:

```go
seventh, eight, ninth := "tujuh", "delapan", "sembilan"
```

Dengan menggunakan teknik type inference, deklarasi multi variabel bisa dilakukan untuk variabel-variabel yang tipe data satu sama lainnya berbeda.

```go
one, isFriday, twoPointTwo, say := 1, true, 2.2, "hello"
```

### Variabel Underscore  `_`

Go memiliki aturan unik yang jarang dimiliki bahasa lain, yaitu tidak boleh ada satupun variabel yang menganggur. Artinya, semua variabel yang dideklarasikan harus digunakan. Jika ada variabel yang tidak digunakan tapi dideklarasikan, error akan muncul pada saat kompilasi dan program tidak akan bisa di-run.

_Underscore_  (`_`) adalah  _reserved variable_  yang bisa dimanfaatkan untuk menampung nilai yang tidak dipakai. Bisa dibilang variabel ini merupakan keranjang sampah.

```go
_ = "belajar Golang"
_ = "Golang itu mudah"
name, _ := "john", "wick"
```

Pada contoh di atas, variabel  `name`  akan berisikan text  `john`, sedang nilai  `wick`  ditampung oleh variabel underscore, menandakan bahwa nilai tersebut tidak akan digunakan.

Variabel underscore adalah  _predefined_, jadi tidak perlu menggunakan  `:=`  untuk pengisian nilai, cukup dengan  `=`  saja. Namun khusus untuk pengisian nilai multi variabel yang dilakukan dengan metode type inference, boleh di dalamnya terdapat variabel underscore.

Biasanya variabel underscore sering dimanfaatkan untuk menampung nilai balik fungsi yang tidak digunakan.

Perlu diketahui, bahwa isi variabel underscore tidak dapat ditampilkan. Data yang sudah masuk variabel tersebut akan hilang. Ibaratkan variabel underscore seperti blackhole, objek apapun yang masuk ke dalamnya, akan terjebak selamanya di-dalam singularity dan tidak akan bisa keluar.

### Deklarasi Variabel Menggunakan Keyword  `new`

Keyword  `new`  digunakan untuk membuat variabel  **pointer**  dengan tipe data tertentu. Nilai data default-nya akan menyesuaikan tipe datanya.

```go
name := new(string)

fmt.Println(name)   // 0x20818a220
fmt.Println(*name)  // ""
```

Variabel  `name`  menampung data bertipe  **pointer string**. Jika ditampilkan yang muncul bukanlah nilainya melainkan alamat memori nilai tersebut (dalam bentuk notasi heksadesimal). Untuk menampilkan nilai aslinya, variabel tersebut perlu di-**dereference**  terlebih dahulu, menggunakan tanda asterisk (`*`).

### Deklarasi Variabel Menggunakan Keyword  `make`

Keyword ini hanya bisa digunakan untuk pembuatan beberapa jenis variabel saja, yaitu:

-   channel
-   slice
-   map

Penjelasan lebih lanjut akan muncul pada pembahasan masing masing jenis variabel tersebut.

## Tipe Data
Go mengenal beberapa jenis tipe data, di antaranya adalah tipe data numerik (desimal & non-desimal), string, dan boolean.

Pada pembahasan-pembahasan sebelumnya secara tak sadar kita sudah mengaplikasikan beberapa tipe data, seperti  `string`  dan tipe numerik  `int`.

Pada chapter ini akan dijelaskan beberapa macam tipe data standar yang disediakan oleh Go, beserta cara penggunaannya.

### Tipe Data Numerik Non-Desimal
Tipe data numerik non-desimal atau  **non floating point**  di Go ada beberapa jenis. Secara umum ada 2 tipe data kategori ini yang perlu diketahui.

-   `uint`, tipe data untuk bilangan cacah (bilangan positif).
-   `int`, tipe data untuk bilangan bulat (bilangan negatif dan positif).

Kedua tipe data di atas kemudian dibagi lagi menjadi beberapa jenis, dengan pembagian berdasarkan lebar cakupan nilainya, detailnya bisa dilihat di tabel berikut.
|Tipe data| Cakupan bilangan |
|--|--|
| uint8 | 0 ↔ 255 |
| uint16 | 0 ↔ 65535 |
| uint32 | 0 ↔ 4294967295 |
| uint64 | 0 ↔ 18446744073709551615 |
| uint | sama dengan uint32 atau uint64 (tergantung nilai) |
| byte | sama dengan uint8 |
| int8 | -128 ↔ 127 |
| int16 | -32768 ↔ 32767 |
| int32 | -2147483648 ↔ 2147483647 |
| int64 | -9223372036854775808 ↔ 9223372036854775807 |
| int | sama dengan int32 atau int64 (tergantung nilai) |
| rune | sama dengan int32 |

Dianjurkan untuk tidak sembarangan dalam menentukan tipe data variabel, sebisa mungkin tipe yang dipilih harus disesuaikan dengan nilainya, karena efeknya adalah ke alokasi memori variabel. Pemilihan tipe data yang tepat akan membuat pemakaian memori lebih optimal, tidak berlebihan.

```go
var positiveNumber uint8 = 89
var negativeNumber = -1243423644

fmt.Printf("bilangan positif: %d\n", positiveNumber)
fmt.Printf("bilangan negatif: %d\n", negativeNumber)
```

Variabel  `positiveNumber`  bertipe  `uint8`  dengan nilai awal  `89`. Sedangkan variabel  `negativeNumber`  dideklarasikan dengan nilai awal  `-1243423644`. Compiler secara cerdas akan menentukan tipe data variabel tersebut sebagai  `int32`  (karena angka tersebut masuk ke cakupan tipe data  `int32`).

Template  `%d`  pada  `fmt.Printf()`  digunakan untuk memformat data numerik non-desimal.

### Tipe Data Numerik Desimal
Tipe data numerik desimal yang perlu diketahui ada 2,  `float32`  dan  `float64`. Perbedaan kedua tipe data tersebut berada di lebar cakupan nilai desimal yang bisa ditampung. Untuk lebih jelasnya bisa merujuk ke spesifikasi  [IEEE-754 32-bit floating-point numbers](http://www.h-schmidt.net/FloatConverter/IEEE754.html).

```go
var decimalNumber = 2.62

fmt.Printf("bilangan desimal: %f\n", decimalNumber)
fmt.Printf("bilangan desimal: %.3f\n", decimalNumber)
```

Pada kode di atas, variabel  `decimalNumber`  akan memiliki tipe data  `float32`, karena nilainya berada di cakupan tipe data tersebut.

Template  `%f`  digunakan untuk memformat data numerik desimal menjadi string. Digit desimal yang akan dihasilkan adalah  **6 digit**. Pada contoh di atas, hasil format variabel  `decimalNumber`  adalah  `2.620000`. Jumlah digit yang muncul bisa dikontrol menggunakan  `%.nf`, tinggal ganti  `n`  dengan angka yang diinginkan. Contoh:  `%.3f`  maka akan menghasilkan 3 digit desimal,  `%.10f`  maka akan menghasilkan 10 digit desimal.

### Tipe Data  `bool`  (Boolean)
Tipe data  `bool`  berisikan hanya 2 variansi nilai,  `true`  dan  `false`.

```go
var exist bool = true
fmt.Printf("exist? %t \n", exist)
```

Gunakan  `%t`  untuk memformat data  `bool`  menggunakan fungsi  `fmt.Printf()`.

### Tipe Data  `string`
Ciri khas dari tipe data string adalah nilainya di apit oleh tanda  _quote_  atau petik dua (`"`). Contoh penerapannya:

```go
var message string = "Halo"
fmt.Printf("message: %s \n", message)
```

Selain menggunakan tanda quote, deklarasi string juga bisa dengan tanda  _grave accent/backticks_  (`` ` ``), tanda ini terletak di sebelah kiri tombol 1. Keistimewaan string yang dideklarasikan menggunakan backtics adalah membuat semua karakter di dalamnya  **tidak di escape**, termasuk  `\n`, tanda petik dua dan tanda petik satu, baris baru, dan lainnya. Semua akan terdeteksi sebagai string.

```go
var message = `Nama saya "John Wick".
Salam kenal.
Mari belajar "Golang".`

fmt.Println(message)
```

### Nilai  `nil`  & Zero Value
`nil`  bukan merupakan tipe data, melainkan sebuah nilai. Variabel yang isi nilainya  `nil`  berarti memiliki nilai kosong.

Semua tipe data yang sudah dibahas di atas memiliki zero value (nilai default tipe data). Artinya meskipun variabel dideklarasikan dengan tanpa nilai awal, tetap akan ada nilai default-nya.

-   Zero value dari  `string`  adalah  `""`  (string kosong).
-   Zero value dari  `bool`  adalah  `false`.
-   Zero value dari tipe numerik non-desimal adalah  `0`.
-   Zero value dari tipe numerik desimal adalah  `0.0`.

Zero value berbeda dengan  `nil`.  `Nil`  adalah nilai kosong, benar-benar kosong.  `nil`  tidak bisa digunakan pada tipe data yang sudah dibahas di atas. Ada beberapa tipe data yang bisa di-set nilainya dengan  `nil`, di antaranya:

-   pointer
-   tipe data fungsi
-   slice
-   `map`
-   `channel`
-   interface kosong atau  `any`  (yang merupakan alias dari  `interface{}`)

> Tipe data  `any`  hanya tersedia pada go versi  `1.18`  ke atas

## Konstanta
Konstanta adalah jenis variabel yang nilainya tidak bisa diubah. Inisialisasi nilai hanya dilakukan sekali di awal, setelah itu variabel tidak bisa diubah nilainya.

### Penggunaan Konstanta

Data seperti  **pi**  (22/7), kecepatan cahaya (299.792.458 m/s), adalah contoh data yang tepat jika dideklarasikan sebagai konstanta daripada variabel, karena nilainya sudah pasti dan tidak berubah.

Cara penerapan konstanta sama seperti deklarasi variabel biasa, selebihnya tinggal ganti keyword  `var`  dengan  `const`.

```go
const firstName string = "john"
fmt.Print("halo ", firstName, "!\n")
```

Teknik type inference bisa diterapkan pada konstanta, caranya yaitu cukup dengan menghilangkan tipe data pada saat deklarasi.

```go
const lastName = "wick"
fmt.Print("nice to meet you ", lastName, "!\n")
```

#### Penggunaan Fungsi  `fmt.Print()`
Fungsi ini memiliki peran yang sama seperti fungsi  `fmt.Println()`, pembedanya fungsi  `fmt.Print()`  tidak menghasilkan baris baru di akhir outputnya.

Perbedaan lainnya adalah, nilai pada parameter-parameter yang dimasukkan ke fungsi tersebut digabungkan tanpa pemisah. Tidak seperti pada fungsi  `fmt.Println()`  yang nilai paremeternya digabung menggunakan penghubung spasi.

```go
fmt.Println("john wick")
fmt.Println("john", "wick")

fmt.Print("john wick\n")
fmt.Print("john ", "wick\n")
fmt.Print("john", " ", "wick\n")
```

Kode di atas menunjukkan perbedaan antara  `fmt.Println()`  dan  `fmt.Print()`. Output yang dihasilkan oleh 5 statement di atas adalah sama, meski cara yang digunakan berbeda.

Bila menggunakan  `fmt.Println()`  tidak perlu menambahkan spasi di tiap kata, karena fungsi tersebut akan secara otomatis menambahkannya di sela-sela nilai. Berbeda dengan  `fmt.Print()`, perlu ditambahkan spasi, karena fungsi ini tidak menambahkan spasi di sela-sela nilai parameter yang digabungkan.

### Deklarasi Multi Konstanta
Sama seperti variabel, konstanta juga dapat dideklarasikan secara bersamaan.

Berikut adalah contoh deklarasi konstanta dengan tipe data dan nilai yang berbeda.

```go
const (
    square          = "kotak"
    isToday bool    = true
    numeric uint8   = 1
    floatNum        = 2.2
)
```

-   `isToday`, dideklarasikan dengan metode  _type inference_  dengan tipe data  **bool**  dan nilainya  **true**
-   `square`, dideklarasikan dengan metode  _manifest typing_  dengan tipe data  **string**  dan nilainya  **"kotak"**
-   `numeric`, dideklarasikan dengan metode  _manifest typing_  dengan tipe data  **uint8**  dan nilainya  **1**
-   `floatNum`, dideklarasikan dengan metode  _type inference_  dengan tipe data  **float**  dan nilainya  **2.2**

Contoh deklarasi konstanta dengan tipe data dan nilai yang sama:

```go
const (
    a = "konstanta"
    b
)
```

> Ketika tipe data dan nilai tidak dituliskan dalam deklarasi konstanta, maka tipe data dan nilai yang dipergunakan adalah sama seperti konstanta yang dideklarasikan diatasnya.

-   `a`  dideklarasikan dengan metode  _type inference_  dengan tipe data  **string**  dan nilainya  **"konstanta"**
-   `b`  dideklarasikan dengan metode  _type inference_  dengan tipe data  **string**  dan nilainya  **"konstanta"**

Berikut contoh gabungan dari keduanya:

```go
const (
    today string = "senin"
    sekarang
    isToday2 = true
)
```

-   `today`  dideklarasikan dengan metode  _manifest typing_  dengan tipe data  **string**  dan nilainya  **"senin"**
-   `sekarang`  dideklarasikan dengan metode  _manifest typing_  dengan tipe data  **string**  dan nilainya  **"senin"**
-   `isToday2`  dideklarasikan dengan metode  _type inference_  dengan tipe data  **bool**  dan nilainya  **true**

Berikut contoh deklrasi  _multiple_  konstanta dalam satu baris:

```go
const satu, dua = 1, 2
const three, four string = "tiga", "empat"
```

-   `satu`, dideklarasikan dengan metode  _type inference_  dengan tipe data  **int**  dan nilainya  **1**
-   `dua`, dideklarasikan dengan metode  _type inference_  dengan tipe data  **int**  dan nilainya  **2**
-   `three`, dideklarasikan dengan metode  _manifest typing_  dengan tipe data  **string**  dan nilainya  **"tiga"**
-   `four`, dideklarasikan dengan metode  _manifest typing_  dengan tipe data  **string**  dan nilainya  **"empat"**

## Operator
Chapter ini membahas mengenai macam operator yang bisa digunakan di Go. Secara umum terdapat 3 kategori operator: aritmatika, perbandingan, dan logika.

### Operator Aritmatika
Operator aritmatika adalah operator yang digunakan untuk operasi yang sifatnya perhitungan. Go mendukung beberapa operator aritmatika standar, list-nya bisa dilihat di tabel berikut.

| Tanda | Penjelasan |
|--|--|
| + | penjumlahan |
| - | pengurangan |
| * | perkalian |
| / | pembagian |
| % | modulus / sisa hasil pembagian |

Contoh penggunaan:

```go
var value = (((2 + 6) % 3) * 4 - 2) / 3
```

### Operator Perbandingan

Operator perbandingan digunakan untuk menentukan kebenaran suatu kondisi. Hasilnya berupa nilai boolean,  `true`  atau  `false`.

Tabel di bawah ini berisikan operator perbandingan yang bisa digunakan di Go.

| Tanda | Penjelasan |
|--|--|
| == | apakah nilai kiri sama dengan nilai kanan |
| != | apakah nilai kiri tidak sama dengan nilai kanan |
| < | apakah nilai kiri lebih kecil daripada nilai kanan |
| <= | apakah nilai kiri lebih kecil atau sama dengan nilai kanan |
| > | apakah nilai kiri lebih besar dari nilai kanan |
| >= | apakah nilai kiri lebih besar atau sama dengan nilai kanan |

Contoh penggunaan:

```go
var value = (((2 + 6) % 3) * 4 - 2) / 3
var isEqual = (value == 2)

fmt.Printf("nilai %d (%t) \n", value, isEqual)
```

Pada kode di atas, terdapat statement operasi aritmatika yang hasilnya ditampung oleh variabel  `value`. Selanjutnya, variabel tersebut dibandingkan dengan angka  **2**  untuk dicek apakah nilainya sama. Jika iya, maka hasilnya adalah  `true`, jika tidak maka  `false`. Nilai hasil operasi perbandingan tersebut kemudian disimpan dalam variabel  `isEqual`.

Untuk memunculkan nilai  `bool`  menggunakan  `fmt.Printf()`, bisa gunakan layout format  `%t`.

### Operator Logika

Operator ini digunakan untuk mencari benar tidaknya kombinasi data bertipe  `bool`  (bisa berupa variabel bertipe  `bool`, atau hasil dari operator perbandingan).

Beberapa operator logika standar yang bisa digunakan:

| Tanda | Penjelasan |
|--|--|
| && | kiri dan kanan |
| || | kiri atau kanan |
| ! | negasi / nilai kebalikan |

Contoh penggunaan:

```go
var left = false
var right = true

var leftAndRight = left && right
fmt.Printf("left && right \t(%t) \n", leftAndRight)

var leftOrRight = left || right
fmt.Printf("left || right \t(%t) \n", leftOrRight)

var leftReverse = !left
fmt.Printf("!left \t\t(%t) \n", leftReverse)
```

Hasil dari operator logika sama dengan hasil dari operator perbandingan, yaitu berupa boolean.

Berikut penjelasan statemen operator logika pada kode di atas.

-   `leftAndRight`  bernilai  `false`, karena hasil dari  `false`  **dan**  `true`  adalah  `false`.
-   `leftOrRight`  bernilai  `true`, karena hasil dari  `false`  **atau**  `true`  adalah  `true`.
-   `leftReverse`  bernilai  `true`, karena  **negasi**  (atau lawan dari)  `false`  adalah  `true`.

Template  `\t`  digunakan untuk menambahkan indent tabulasi. Biasa dimanfaatkan untuk merapikan tampilan output pada console.

## Seleksi Kondisi
Seleksi kondisi digunakan untuk mengontrol alur program. Analoginya mirip seperti fungsi rambu lalu lintas di jalan raya. Kapan kendaraan diperbolehkan melaju dan kapan harus berhenti diatur oleh rambu tersebut. Seleksi kondisi pada program juga kurang lebih sama, kapan sebuah blok kode akan dieksekusi dikontrol.

Yang dijadikan acuan oleh seleksi kondisi adalah nilai bertipe  `bool`, bisa berasal dari variabel, ataupun hasil operasi perbandingan. Nilai tersebut menentukan blok kode mana yang akan dieksekusi.

Go memiliki 2 macam keyword untuk seleksi kondisi, yaitu  **if else**  dan  **switch**. Pada chapter ini kita akan mempelajarinya satu-persatu.

> Go tidak mendukung seleksi kondisi menggunakan  **ternary**.  
> Statement seperti:  `var data = (isExist ? "ada" : "tidak ada")`  adalah invalid dan menghasilkan error.

### Seleksi Kondisi Menggunakan Keyword  `if`,  `else if`, &  `else`

Cara penerapan if-else di Go sama seperti pada bahasa pemrograman lain. Yang membedakan hanya tanda kurungnya  _(parentheses)_, di Go tidak perlu ditulis. Kode berikut merupakan contoh penerapan seleksi kondisi if else, dengan jumlah kondisi 4 buah.

```go
var point = 8

if point == 10 {
    fmt.Println("lulus dengan nilai sempurna")
} else if point > 5 {
    fmt.Println("lulus")
} else if point == 4 {
    fmt.Println("hampir lulus")
} else {
    fmt.Printf("tidak lulus. nilai anda %d\n", point)
}
```

Dari ke-empat kondisi di atas, yang terpenuhi adalah  `if point > 5`, karena nilai variabel  `point`  memang lebih besar dari  `5`. Maka blok kode tepat di bawah kondisi tersebut akan dieksekusi (blok kode ditandai kurung kurawal buka dan tutup), hasilnya text  `"lulus"`  muncul sebagai output.

Skema if else Go sama seperti pada pemrograman umumnya. Yaitu di awal seleksi kondisi menggunakan  `if`, dan ketika kondisinya tidak terpenuhi akan menuju ke  `else`  (jika ada). Ketika ada banyak kondisi, gunakan  `else if`.

> Di bahasa pemrograman lain, ketika ada seleksi kondisi yang isi blok-nya hanya 1 baris saja, kurung kurawal boleh tidak dituliskan. Berbeda dengan aturan di Go, kurung kurawal harus tetap dituliskan meski isinya hanya 1 blok satement.

### Variabel Temporary Pada  `if`  -  `else`

Variabel temporary adalah variabel yang hanya bisa digunakan pada blok seleksi kondisi di mana ia ditempatkan saja. Penggunaan variabel ini membawa beberapa manfaat, antara lain:

-   Scope atau cakupan variabel jelas, hanya bisa digunakan pada blok seleksi kondisi itu saja
-   Kode menjadi lebih rapi
-   Ketika nilai variabel tersebut didapat dari sebuah komputasi, perhitungan tidak perlu dilakukan di dalam blok masing-masing kondisi.

```go
var point = 8840.0

if percent := point / 100; percent >= 100 {
    fmt.Printf("%.1f%s perfect!\n", percent, "%")
} else if percent >= 70 {
    fmt.Printf("%.1f%s good\n", percent, "%")
} else {
    fmt.Printf("%.1f%s not bad\n", percent, "%")
}
```

Variabel  `percent`  nilainya didapat dari hasil perhitungan, dan hanya bisa digunakan di deretan blok seleksi kondisi itu saja.

> Deklarasi variabel temporary hanya bisa dilakukan lewat metode type inference yang menggunakan tanda  `:=`. Penggunaan keyword  `var`  di situ tidak diperbolehkan karena akan menyebabkan error.

### Seleksi Kondisi Menggunakan Keyword  `switch`  -  `case`

Switch merupakan seleksi kondisi yang sifatnya fokus pada satu variabel, lalu kemudian di-cek nilainya. Contoh sederhananya seperti penentuan apakah nilai variabel  `x`  adalah:  `1`,  `2`,  `3`, atau lainnya.

```go
var point = 6

switch point {
case 8:
    fmt.Println("perfect")
case 7:
    fmt.Println("awesome")
default:
    fmt.Println("not bad")
}
```

Pada kode di atas, tidak ada kondisi atau  `case`  yang terpenuhi karena nilai variabel  `point`  tetap  `6`. Ketika hal seperti ini terjadi, blok kondisi  `default`  dipanggil. Bisa dibilang bahwa  `default`  merupakan  `else`  dalam sebuah switch.

Perlu diketahui, switch pada pemrograman Go memiliki perbedaan dibanding bahasa lain. Di Go, ketika sebuah case terpenuhi, tidak akan dilanjutkan ke pengecekan case selanjutnya, meskipun tidak ada keyword  `break`  di situ. Konsep ini berkebalikan dengan switch pada umumnya, yang ketika sebuah case terpenuhi, maka akan tetap dilanjut mengecek case selanjutnya kecuali ada keyword  `break`.

### Pemanfaatan  `case`  Untuk Banyak Kondisi

Sebuah  `case`  dapat menampung banyak kondisi. Cara penerapannya yaitu dengan menuliskan nilai pembanding-pembanding variabel yang di-switch setelah keyword  `case`  dipisah tanda koma (`,`).

```go
var point = 6

switch point {
case 8:
    fmt.Println("perfect")
case 7, 6, 5, 4:
    fmt.Println("awesome")
default:
    fmt.Println("not bad")
}
```

Kondisi  `case 7, 6, 5, 4:`  akan terpenuhi ketika nilai variabel  `point`  adalah 7 atau 6 atau 5 atau 4.

### Kurung Kurawal Pada Keyword  `case`  &  `default`
Tanda kurung kurawal (`{ }`) bisa diterapkan pada keyword  `case`  dan  `default`. Tanda ini opsional, boleh dipakai boleh tidak. Bagus jika dipakai pada blok kondisi yang di dalamnya ada banyak statement, kode akan terlihat lebih rapi dan mudah di-maintain.

Perhatikan kode berikut, bisa dilihat pada keyword  `default`  terdapat kurung kurawal yang mengapit 2 statement di dalamnya.

```go
var point = 6

switch point {
case 8:
    fmt.Println("perfect")
case 7, 6, 5, 4:
    fmt.Println("awesome")
default:
    {
        fmt.Println("not bad")
        fmt.Println("you can be better!")
    }
}
```

### Switch Dengan Gaya  `if`  -  `else`

Uniknya di Go, switch bisa digunakan dengan gaya ala if-else. Nilai yang akan dibandingkan tidak dituliskan setelah keyword  `switch`, melainkan akan ditulis langsung dalam bentuk perbandingan dalam keyword  `case`.

Pada kode di bawah ini, kode program switch di atas diubah ke dalam gaya  `if-else`. Variabel  `point`  dihilangkan dari keyword  `switch`, lalu kondisi-kondisinya dituliskan di tiap  `case`.

```go
var point = 6

switch {
case point == 8:
    fmt.Println("perfect")
case (point < 8) && (point > 3):
    fmt.Println("awesome")
default:
    {
        fmt.Println("not bad")
        fmt.Println("you need to learn more")
    }
}
```

### Penggunaan Keyword  `fallthrough`  Dalam  `switch`

Seperti yang sudah dijelaskan sebelumnya, bahwa switch pada Go memiliki perbedaan dengan bahasa lain. Ketika sebuah  `case`  terpenuhi, pengecekan kondisi tidak akan diteruskan ke case-case setelahnya.

Keyword  `fallthrough`  digunakan untuk memaksa proses pengecekan diteruskan ke satu  `case`  selanjutnya dengan  **tanpa menghiraukan nilai kondisinya**, jadi satu case di pengecekan selanjutnya tersebut selalu dianggap benar (meskipun aslinya adalah salah). Dalam sebuah  `switch`  lebih dari satu  `fallthrough`  bisa di tempatkan untuk memaksa melanjutkan proses pengecekan ke satu  `case`  setelahnya.

```go
var point = 6

switch {
case point == 8:
    fmt.Println("perfect")
case (point < 8) && (point > 3):
    fmt.Println("awesome")
    fallthrough
case point < 5:
    fmt.Println("you need to learn more")
default:
    {
        fmt.Println("not bad")
        fmt.Println("you need to learn more")
    }
}
```

Setelah pengecekan  `case (point < 8) && (point > 3)`  selesai, akan dilanjut ke pengecekan  `case point < 5`, karena ada  `fallthrough` di situ.

### Seleksi Kondisi Bersarang
Seleksi kondisi bersarang adalah seleksi kondisi, yang berada dalam seleksi kondisi, yang mungkin juga berada dalam seleksi kondisi, dan seterusnya. Seleksi kondisi bersarang bisa dilakukan pada  `if`  -  `else`,  `switch`, ataupun kombinasi keduanya.

```go
var point = 10

if point > 7 {
    switch point {
    case 10:
        fmt.Println("perfect!")
    default:
        fmt.Println("nice!")
    }
} else {
    if point == 5 {
        fmt.Println("not bad")
    } else if point == 3 {
        fmt.Println("keep trying")
    } else {
        fmt.Println("you can do it")
        if point == 0 {
            fmt.Println("try harder!")
        }
    }
}
```

## Perulangan
Perulangan adalah proses mengulang-ulang eksekusi blok kode tanpa henti, selama kondisi yang dijadikan acuan terpenuhi. Biasanya disiapkan variabel untuk iterasi atau variabel penanda kapan perulangan akan diberhentikan.

Di Go keyword perulangan hanya  **for**  saja, tetapi meski demikian, kemampuannya merupakan gabungan  `for`,  `foreach`, dan  `while`  ibarat bahasa pemrograman lain.

### Perulangan Menggunakan Keyword  `for`
Ada beberapa cara standar menggunakan  `for`. Cara pertama dengan memasukkan variabel counter perulangan beserta kondisinya setelah keyword. Perhatikan dan praktekan kode berikut.

```go
for i := 0; i < 5; i++ {
    fmt.Println("Angka", i)
}
```

Perulangan di atas hanya akan berjalan ketika variabel  `i`  bernilai di bawah  `5`, dengan ketentuan setiap kali perulangan, nilai variabel  `i`  akan di-iterasi atau ditambahkan 1 (`i++`  artinya ditambah satu, sama seperti  `i = i + 1`). Karena  `i`  pada awalnya bernilai 0, maka perulangan akan berlangsung 5 kali, yaitu ketika  `i`  bernilai 0, 1, 2, 3, dan 4.

### Penggunaan Keyword  `for`  Dengan Argumen Hanya Kondisi

Cara ke-2 adalah dengan menuliskan kondisi setelah keyword  `for`  (hanya kondisi). Deklarasi dan iterasi variabel counter tidak dituliskan setelah keyword, hanya kondisi perulangan saja. Konsepnya mirip seperti  `while`  milik bahasa pemrograman lain.

Kode berikut adalah contoh  `for`  dengan argumen hanya kondisi (seperti  `if`), output yang dihasilkan sama seperti penerapan  `for`  cara pertama.

```go
var i = 0

for i < 5 {
    fmt.Println("Angka", i)
    i++
}
```

### Penggunaan Keyword  `for`  Tanpa Argumen
Cara ke-3 adalah  `for`  ditulis tanpa kondisi. Dengan ini akan dihasilkan perulangan tanpa henti (sama dengan  `for true`). Pemberhentian perulangan dilakukan dengan menggunakan keyword  `break`.

```go
var i = 0

for {
    fmt.Println("Angka", i)

    i++
    if i == 5 {
        break
    }
}
```

Dalam perulangan tanpa henti di atas, variabel  `i`  yang nilai awalnya  `0`  di-inkrementasi. Ketika nilai  `i`  sudah mencapai  `5`, keyword  `break`  digunakan, dan perulangan akan berhenti.

### Penggunaan Keyword  `for`  -  `range`
Cara ke-4 adalah perulangan dengan menggunakan kombinasi keyword  `for`  dan  `range`. Cara ini biasa digunakan untuk me-looping data bertipe array. Detailnya akan dibahas dalam bagian selanjutnya.

### Penggunaan Keyword  `break`  &  `continue`
Keyword  `break`  digunakan untuk menghentikan secara paksa sebuah perulangan, sedangkan  `continue`  dipakai untuk memaksa maju ke perulangan berikutnya.

Berikut merupakan contoh penerapan  `continue`  dan  `break`. Kedua keyword tersebut dimanfaatkan untuk menampilkan angka genap berurutan yang lebih besar dari 0 dan kurang dari atau sama dengan 8.

```go
for i := 1; i <= 10; i++ {
    if i % 2 == 1 {
        continue
    }

    if i > 8 {
        break
    }

    fmt.Println("Angka", i)
}
```

Kode di atas akan lebih mudah dicerna jika dijelaskan secara berurutan. Berikut adalah penjelasannya.

1.  Dilakukan perulangan mulai angka 1 hingga 10 dengan  `i`  sebagai variabel iterasi.
2.  Ketika  `i`  adalah ganjil (dapat diketahui dari  `i % 2`, jika hasilnya  `1`, berarti ganjil), maka akan dipaksa lanjut ke perulangan berikutnya.
3.  Ketika  `i`  lebih besar dari 8, maka perulangan akan berhenti.
4.  Nilai  `i`  ditampilkan.

### Perulangan Bersarang
Tak hanya seleksi kondisi yang bisa bersarang, perulangan juga bisa. Cara pengaplikasiannya kurang lebih sama, tinggal tulis blok statement perulangan di dalam perulangan.

```go
for i := 0; i < 5; i++ {
    for j := i; j < 5; j++ {
        fmt.Print(j, " ")
    }

    fmt.Println()
}
```

Pada kode di atas, untuk pertama kalinya fungsi  `fmt.Println()`  dipanggil tanpa disisipkan parameter. Cara seperti ini bisa digunakan untuk menampilkan baris baru. Kegunaannya sama seperti output dari statement  `fmt.Print("\n")`.

### Pemanfaatan Label Dalam Perulangan

Di perulangan bersarang,  `break`  dan  `continue`  akan berlaku pada blok perulangan di mana ia digunakan saja. Ada cara agar kedua keyword ini bisa tertuju pada perulangan terluar atau perulangan tertentu, yaitu dengan memanfaatkan teknik pemberian  **label**.

Program untuk memunculkan matriks berikut merupakan contoh penerapan label perulangan.

```go
outerLoop:
for i := 0; i < 5; i++ {
    for j := 0; j < 5; j++ {
        if i == 3 {
            break outerLoop
        }
        fmt.Print("matriks [", i, "][", j, "]", "\n")
    }
}
```

Tepat sebelum keyword  `for`  terluar, terdapat baris kode  `outerLoop:`. Maksud dari kode tersebut adalah disiapkan sebuah label bernama  `outerLoop`  untuk  `for`  di bawahnya. Nama label bisa diganti dengan nama lain (dan harus diakhiri dengan tanda titik dua atau  _colon_  (`:`) ).

Pada  `for`  bagian dalam, terdapat seleksi kondisi untuk pengecekan nilai  `i`. Ketika nilai tersebut sama dengan  `3`, maka  `break`  dipanggil dengan target adalah perulangan yang dilabeli  `outerLoop`, perulangan tersebut akan dihentikan.

## Array
Array adalah kumpulan data bertipe sama, yang disimpan dalam sebuah variabel. Array memiliki kapasitas yang nilainya ditentukan pada saat pembuatan, menjadikan elemen/data yang disimpan di array tersebut jumlahnya tidak boleh melebihi yang sudah dialokasikan. Default nilai tiap elemen array pada awalnya tergantung dari tipe datanya. Jika  `int`  maka tiap element zero value-nya adalah  `0`, jika  `bool`  maka  `false`, dan seterusnya. Setiap elemen array memiliki indeks berupa angka yang merepresentasikan posisi urutan elemen tersebut. Indeks array dimulai dari 0.

Contoh penerapan array:

```go
var names [4]string
names[0] = "trafalgar"
names[1] = "d"
names[2] = "water"
names[3] = "law"

fmt.Println(names[0], names[1], names[2], names[3])
```

Variabel  `names`  dideklarasikan sebagai  `array string`  dengan alokasi elemen  `4`  slot. Cara mengisi slot elemen array bisa dilihat di kode di atas, yaitu dengan langsung mengakses elemen menggunakan indeks, lalu mengisinya.

### Pengisian Elemen Array yang Melebihi Alokasi Awal

Pengisian elemen array pada indeks yang tidak sesuai dengan alokasi menghasilkan error. Contoh sederhana, jika array memiliki 4 slot, maka pengisian nilai slot 5 seterusnya adalah tidak valid.

```go
var names [4]string
names[0] = "trafalgar"
names[1] = "d"
names[2] = "water"
names[3] = "law"
names[4] = "ez" // baris kode ini menghasilkan error
```

Solusi dari masalah di atas adalah dengan menggunakan keyword  `append`, yang nantinya akan dibahas pada bagian slice.

### Inisialisasi Nilai Awal Array

Pengisian elemen array bisa dilakukan pada saat deklarasi variabel. Caranya dengan menuliskan data elemen dalam kurung kurawal setelah tipe data, dengan pembatas antar elemen adalah tanda koma (`,`).

```go
var fruits = [4]string{"apple", "grape", "banana", "melon"}

fmt.Println("Jumlah element \t\t", len(fruits))
fmt.Println("Isi semua element \t", fruits)
```

Penggunaan fungsi  `fmt.Println()`  pada data array tanpa mengakses indeks tertentu, akan menghasilkan output dalam bentuk string dari semua array yang ada. Teknik ini biasa digunakan untuk  _debugging_  data array.

Fungsi  `len()`  dipakai untuk menghitung jumlah elemen sebuah array.

### Inisialisasi Nilai Array Dengan Gaya Vertikal
Elemen array bisa dituliskan dalam bentuk horizontal (seperti yang sudah dicontohkan di atas) ataupun dalam bentuk vertikal.

```go
var fruits [4]string

// cara horizontal
fruits  = [4]string{"apple", "grape", "banana", "melon"}

// cara vertikal
fruits  = [4]string{
    "apple",
    "grape",
    "banana",
    "melon",
}
```

Khusus untuk deklarasi array dengan cara vertikal, tanda koma wajib dituliskan setelah elemen, termasuk elemen terakhir. Jika tidak, maka akan muncul error.

### Inisialisasi Nilai Awal Array Tanpa Jumlah Elemen

Deklarasi array yang nilainya diset di awal, boleh tidak dituliskan jumlah lebar array-nya, cukup ganti dengan tanda 3 titik (`...`). Jumlah elemen akan di kalkulasi secara otomatis menyesuaikan data elemen yang diisikan.

```go
var numbers = [...]int{2, 3, 2, 4, 3}

fmt.Println("data array \t:", numbers)
fmt.Println("jumlah elemen \t:", len(numbers))
```

Variabel  `numbers`  akan secara otomatis memiliki jumlah elemen  `5`, karena pada saat deklarasi disiapkan 5 buah elemen.

### Array Multidimensi
Array multidimensi adalah array yang tiap elemennya juga berupa array (dan bisa seterusnya, tergantung ke dalaman dimensinya).

Cara deklarasi array multidimensi secara umum sama dengan cara deklarasi array biasa, dengan cara menuliskan data array dimensi selanjutnya sebagai elemen array dimensi sebelumnya.

Khusus untuk array yang merupakan sub dimensi atau elemen, boleh tidak dituliskan jumlah datanya. Contohnya bisa dilihat pada deklarasi variabel  `numbers2`  di kode berikut.

```go
var numbers1 = [2][3]int{[3]int{3, 2, 3}, [3]int{3, 4, 5}}
var numbers2 = [2][3]int{{3, 2, 3}, {3, 4, 5}}

fmt.Println("numbers1", numbers1)
fmt.Println("numbers2", numbers2)
```

Kedua array di atas memiliki elemen yang sama.

### Perulangan Elemen Array Menggunakan Keyword  `for`
Keyword  `for`  dan array memiliki hubungan yang sangat erat. Dengan memanfaatkan perulangan menggunakan keyword ini, elemen-elemen dalam array bisa didapat.

Ada beberapa cara yang bisa digunakan untuk me-looping data array, yg pertama adalah dengan memanfaatkan variabel iterasi perulangan untuk mengakses elemen berdasarkan indeks-nya. Contoh:

```go
var fruits = [4]string{"apple", "grape", "banana", "melon"}

for i := 0; i < len(fruits); i++ {
    fmt.Printf("elemen %d : %s\n", i, fruits[i])
}
```

Perulangan di atas dijalankan sebanyak jumlah elemen array  `fruits`  (bisa diketahui dari kondisi  `i < len(fruits`). Di tiap perulangan, elemen array diakses lewat variabel iterasi  `i`.

### Perulangan Elemen Array Menggunakan Keyword  `for`  -  `range`

Ada cara yang lebih sederhana me-looping data array, dengan menggunakan keyword  `for`  -  `range`. Contoh pengaplikasiannya bisa dilihat di kode berikut.

```go
var fruits = [4]string{"apple", "grape", "banana", "melon"}

for i, fruit := range fruits {
    fmt.Printf("elemen %d : %s\n", i, fruit)
}
```

Array  `fruits`  diambil elemen-nya secara berurutan. Nilai tiap elemen ditampung variabel oleh  `fruit`  (tanpa huruf s), sedangkan indeks nya ditampung variabel  `i`.

Output program di atas, sama dengan output program sebelumnya, hanya cara yang digunakan berbeda.

### Penggunaan Variabel Underscore  `_`  Dalam  `for`  -  `range`

Kadang kala ketika  _looping_  menggunakan  `for`  -  `range`, ada kemungkinan di mana data yang dibutuhkan adalah elemen-nya saja, indeks-nya tidak. Sedangkan kode di atas,  `range`  mengembalikan 2 data, yaitu indeks dan elemen.

Seperti yang sudah diketahui, bahwa di Go tidak memperbolehkan adanya variabel yang menganggur atau tidak dipakai. Jika dipaksakan, error akan muncul, contohnya seperti kode berikut.

```go
var fruits = [4]string{"apple", "grape", "banana", "melon"}

for i, fruit := range fruits {
    fmt.Printf("nama buah : %s\n", fruit)
}
```

Di sinilah salah satu kegunaan variabel pengangguran, atau underscore (`_`). Tampung saja nilai yang tidak ingin digunakan ke underscore.

```go
var fruits = [4]string{"apple", "grape", "banana", "melon"}

for _, fruit := range fruits {
    fmt.Printf("nama buah : %s\n", fruit)
}
```

Pada kode di atas, yang sebelumnya adalah variabel  `i`  diganti dengan  `_`, karena kebetulan variabel  `i`  tidak digunakan.

Jika yang dibutuhkan hanya indeks elemen-nya saja, bisa gunakan 1 buah variabel setelah keyword  `for`.

```go
for i, _ := range fruits { }
// atau
for i := range fruits { }
```

### Alokasi Elemen Array Menggunakan Keyword  `make`

Deklarasi sekaligus alokasi data array juga bisa dilakukan lewat keyword  `make`.

```go
var fruits = make([]string, 2)
fruits[0] = "apple"
fruits[1] = "manggo"

fmt.Println(fruits)  // [apple manggo]
```

Parameter pertama keyword  `make`  diisi dengan tipe data elemen array yang diinginkan, parameter kedua adalah jumlah elemennya. Pada kode di atas, variabel  `fruits`  tercetak sebagai array string dengan alokasi 2 slot.

## Slice
**Slice**  adalah  _reference_  elemen array. Slice bisa dibuat, atau bisa juga dihasilkan dari manipulasi sebuah array ataupun slice lainnya. Karena merupakan data  _reference_, menjadikan perubahan data di tiap elemen slice akan berdampak pada slice lain yang memiliki alamat memori yang sama.

### Inisialisasi Slice

Cara pembuatan slice mirip seperti pembuatan array, bedanya tidak perlu mendefinisikan jumlah elemen ketika awal deklarasi. Pengaksesan nilai elemen-nya juga sama. Contoh pembuatan slice:

```go
var fruits = []string{"apple", "grape", "banana", "melon"}
fmt.Println(fruits[0]) // "apple"
```

Salah satu perbedaan slice dan array bisa diketahui pada saat deklarasi variabel-nya, jika jumlah elemen tidak dituliskan, maka variabel tersebut adalah slice.

```go
var fruitsA = []string{"apple", "grape"}      // slice
var fruitsB = [2]string{"banana", "melon"}    // array
var fruitsC = [...]string{"papaya", "grape"}  // array
```

### Hubungan Slice Dengan Array & Operasi Slice

Kalau perbedannya hanya di penentuan alokasi pada saat inisialisasi, kenapa tidak menggunakan satu istilah saja? atau adakah perbedaan lainnya?

Sebenarnya slice dan array tidak bisa dibedakan karena merupakan sebuah kesatuan. Array adalah kumpulan nilai atau elemen, sedang slice adalah referensi tiap elemen tersebut.

Slice bisa dibentuk dari array yang sudah didefinisikan, caranya dengan memanfaatkan teknik  **2 index**  untuk mengambil elemen-nya. Contoh bisa dilihat pada kode berikut.

```go
var fruits = []string{"apple", "grape", "banana", "melon"}
var newFruits = fruits[0:2]

fmt.Println(newFruits) // ["apple", "grape"]
```

Kode  `fruits[0:2]`  maksudnya adalah pengaksesan elemen dalam slice  `fruits`  yang  **dimulai dari indeks ke-0, hingga elemen sebelum indeks ke-2**. Elemen yang memenuhi kriteria tersebut akan didapat, untuk kemudian disimpan pada variabel lain sebagai slice baru. Pada contoh di atas,  `newFruits`  adalah slice baru yang tercetak dari slice  `fruits`, dengan isi 2 elemen, yaitu  `"apple"`  dan  `"grape"`.

Ketika mengakses elemen array menggunakan satu buah indeks (seperti  `data[2]`), nilai yang didapat merupakan hasil  **copy**  dari referensi aslinya. Berbeda dengan pengaksesan elemen menggunakan 2 indeks (seperti  `data[0:2]`), nilai yang didapat adalah  _reference_  elemen atau slice.

> Tidak apa jikalau pembaca masih bingung, di bawah akan dijelaskan lebih mendetail lagi tentang slice dan  _reference_

Tabel berikut adalah list operasi operasi menggunakan teknik 2 indeks yang bisa dilakukan.

```go
var fruits = []string{"apple", "grape", "banana", "melon"}
```

| Kode | Output | Penjelasan |
|--|--|--|
| fruits[0:2] | [apple, grape] | semua elemen mulai indeks ke-0, hingga sebelum indeks ke-2 |
| fruits[0:4] | [apple, grape, banana, melon] | semua elemen mulai indeks ke-0, hingga sebelum indeks ke-4 |
| fruits[0:0] | [] | menghasilkan slice kosong, karena tidak ada elemen sebelum indeks ke-0 |
| fruits[4:4] | [] | menghasilkan slice kosong, karena tidak ada elemen yang dimulai dari indeks ke-4 |
| fruits[4:0] | [] | error, pada penulisan fruits[a:b] nilai a harus lebih kecil atau sama dengan b |
| fruits[:] | [apple, grape, banana, melon] | semua elemen |
| fruits[2:] | [banana, melon] | semua elemen mulai indeks ke-2 |
| fruits[:2] | [apple, grape] | semua elemen hingga sebelum indeks ke-2 |

### Slice Merupakan Tipe Data Reference

Slice merupakan tipe data  _reference_  atau referensi. Artinya jika ada slice baru yang terbentuk dari slice lama, maka data elemen slice yang baru akan memiliki alamat memori yang sama dengan elemen slice lama. Setiap perubahan yang terjadi di elemen slice baru, akan berdampak juga pada elemen slice lama yang memiliki referensi yang sama.

Program berikut merupakan pembuktian tentang teori yang baru kita bahas. Kita akan mencoba mengubah data elemen slice baru, yang terbentuk dari slice lama.

```go
var fruits = []string{"apple", "grape", "banana", "melon"}

var aFruits = fruits[0:3]
var bFruits = fruits[1:4]

var aaFruits = aFruits[1:2]
var baFruits = bFruits[0:1]

fmt.Println(fruits)   // [apple grape banana melon]
fmt.Println(aFruits)  // [apple grape banana]
fmt.Println(bFruits)  // [grape banana melon]
fmt.Println(aaFruits) // [grape]
fmt.Println(baFruits) // [grape]

// Buah "grape" diubah menjadi "pinnaple"
baFruits[0] = "pinnaple"

fmt.Println(fruits)   // [apple pinnaple banana melon]
fmt.Println(aFruits)  // [apple pinnaple banana]
fmt.Println(bFruits)  // [pinnaple banana melon]
fmt.Println(aaFruits) // [pinnaple]
fmt.Println(baFruits) // [pinnaple]
```

Sekilas bisa kita lihat bahwa setelah slice yang isi datanya adalah  `grape`  di-ubah menjadi  `pinnaple`, semua slice pada 4 variabel lainnya juga ikut berubah.

Variabel  `aFruits`,  `bFruits`  merupakan slice baru yang terbentuk dari variabel  `fruits`. Dengan menggunakan dua slice baru tersebut, diciptakan lagi slice lainnya, yaitu  `aaFruits`, dan  `baFruits`. Kelima slice tersebut ditampilkan nilainya.

Selanjutnya, nilai dari  `baFruits[0]`  diubah, dan 5 slice tadi ditampilkan lagi. Hasilnya akan ada banyak slice yang elemennya ikut berubah. Yaitu elemen-elemen yang referensi-nya sama dengan referensi elemen  `baFruits[0]`.

----------

Pembahasan mengenai dasar slice sepertinya sudah cukup, selanjutnya kita akan membahas tentang beberapa  _built in function_  bawaan Go, yang bisa dimanfaatkan untuk keperluan operasi slice.

### Fungsi  `len()`

Fungsi  `len()`  digunakan untuk menghitung jumlah elemen slice yang ada. Sebagai contoh jika sebuah variabel adalah slice dengan data 4 buah, maka fungsi ini pada variabel tersebut akan mengembalikan angka  **4**.

```go
var fruits = []string{"apple", "grape", "banana", "melon"}
fmt.Println(len(fruits)) // 4
```

### Fungsi  `cap()`

Fungsi  `cap()`  digunakan untuk menghitung lebar atau kapasitas maksimum slice. Nilai kembalian fungsi ini untuk slice yang baru dibuat pasti sama dengan  `len`, tapi bisa berubah seiring operasi slice yang dilakukan. Agar lebih jelas, silakan disimak kode berikut.

```go
var fruits = []string{"apple", "grape", "banana", "melon"}
fmt.Println(len(fruits))  // len: 4
fmt.Println(cap(fruits))  // cap: 4

var aFruits = fruits[0:3]
fmt.Println(len(aFruits)) // len: 3
fmt.Println(cap(aFruits)) // cap: 4

var bFruits = fruits[1:4]
fmt.Println(len(bFruits)) // len: 3
fmt.Println(cap(bFruits)) // cap: 3
```

Variabel  `fruits`  disiapkan di awal dengan jumlah elemen 4, fungsi  `len(fruits)`  dan  `cap(fruits)`  pasti hasinya 4.

Variabel  `aFruits`  dan  `bFruits`  merupakan slice baru berisikan 3 buah elemen milik slice  `fruits`. Variabel  `aFruits`  mengambil elemen index 0, 1, 2; sedangkan  `bFruits`  1, 2, 3.

Fungsi  `len()`  menghasilkan angka 3, karena jumlah elemen kedua slice ini adalah 3. Tetapi  `cap(aFruits)`  menghasilkan angka yang berbeda, yaitu 4 untuk  `aFruits`  dan 3 untuk  `bFruits`. kenapa? jawabannya bisa dilihat pada tabel berikut.

| Kode | Output | len() | cap() |
|--|--|--|--|
| fruits[0:4] | [buah buah buah buah] | 4 | 4 |
| aFruits[0:3] | [buah buah buah ----] | 3 | 4 |
| bFruits[1:4] | ---- [buah buah buah] | 3 | 3 |

Kita analogikan slicing 2 index menggunakan  **x**  dan  **y**.

```go
fruits[x:y]
```

**Slicing**  yang dimulai dari indeks  **0**  hingga  **y**  akan mengembalikan elemen-elemen mulai indeks  **0**  hingga sebelum indeks  **y**, dengan lebar kapasitas adalah sama dengan slice aslinya.

Sedangkan slicing yang dimulai dari indeks  **x**, yang di mana nilai  **x**  adalah lebih dari  **0**, membuat elemen ke-**x**  slice yang diambil menjadi elemen ke-0 slice baru. Hal inilah yang membuat kapasitas slice berubah.

### Fungsi  `append()`

Fungsi  `append()`  digunakan untuk menambahkan elemen pada slice. Elemen baru tersebut diposisikan setelah indeks paling akhir. Nilai balik fungsi ini adalah slice yang sudah ditambahkan nilai barunya. Contoh penggunaannya bisa dilihat di kode berikut.

```go
var fruits = []string{"apple", "grape", "banana"}
var cFruits = append(fruits, "papaya")

fmt.Println(fruits)  // ["apple", "grape", "banana"]
fmt.Println(cFruits) // ["apple", "grape", "banana", "papaya"]
```

Ada 3 hal yang perlu diketahui dalam penggunaan fungsi ini.

-   Ketika jumlah elemen dan lebar kapasitas adalah sama (`len(fruits) == cap(fruits)`), maka elemen baru hasil  `append()`  merupakan referensi baru.
-   Ketika jumlah elemen lebih kecil dibanding kapasitas (`len(fruits) < cap(fruits)`), elemen baru tersebut ditempatkan ke dalam cakupan kapasitas, menjadikan semua elemen slice lain yang referensi-nya sama akan berubah nilainya.

Agar lebih jelas silakan perhatikan contoh berikut.

```go
var fruits = []string{"apple", "grape", "banana"}
var bFruits = fruits[0:2]

fmt.Println(cap(bFruits)) // 3
fmt.Println(len(bFruits)) // 2

fmt.Println(fruits)  // ["apple", "grape", "banana"]
fmt.Println(bFruits) // ["apple", "grape"]

var cFruits = append(bFruits, "papaya")

fmt.Println(fruits)  // ["apple", "grape", "papaya"]
fmt.Println(bFruits) // ["apple", "grape"]
fmt.Println(cFruits) // ["apple", "grape", "papaya"]
```

Pada contoh di atas bisa dilihat, elemen indeks ke-2 slice  `fruits`  nilainya berubah setelah ada penggunaan keyword  `append()`  pada  `bFruits`. Slice  `bFruits`  kapasitasnya adalah  **3**  sedang jumlah datanya hanya  **2**. Karena  `len(bFruits) < cap(bFruits)`, maka elemen baru yang dihasilkan, terdeteksi sebagai perubahan nilai pada referensi yang lama (referensi elemen indeks ke-2 slice  `fruits`), membuat elemen yang referensinya sama, nilainya berubah.

### Fungsi  `copy()`

Fungsi  `copy()`  digunakan untuk men-copy elements slice pada  `src`  (parameter ke-2), ke  `dst`  (parameter pertama).

```go
copy(dst, src)
```

Jumlah element yang di-copy dari  `src`  adalah sejumlah lebar slice  `dst`  (atau  `len(dst)`). Jika jumlah slice pada  `src`  lebih kecil dari  `dst`, maka akan ter-copy semua. Lebih jelasnya silakan perhatikan contoh berikut.

```go
dst := make([]string, 3)
src := []string{"watermelon", "pinnaple", "apple", "orange"}
n := copy(dst, src)

fmt.Println(dst) // watermelon pinnaple apple
fmt.Println(src) // watermelon pinnaple apple orange
fmt.Println(n)   // 3
```

Pada kode di atas variabel slice  `dst`  dipersiapkan dengan lebar adalah 3 elements. Slice  `src`  yang isinya 4 elements, di-copy ke  `dst`. Menjadikan isi slice  `dst`  sekarang adalah 3 buah elements yang sama dengan 3 buah elements  `src`, hasil dari operasi  `copy()`.

Yang ter-copy hanya 3 buah (meski  `src`  memiliki 4 elements) hal ini karena  `copy()`  hanya meng-copy elements sebanyak  `len(dst)`.

> Fungsi  `copy()`  mengembalikan informasi angka, representasi dari jumlah element yang berhasil di-copy.

Pada contoh kedua berikut,  `dst`  merupakan slice yang sudah ada isinya, 3 buah elements. Variabel  `src`  yang juga merupakan slice dengan isi dua elements, di-copy ke  `dst`. Karena operasi  `copy()`  akan meng-copy sejumlah  `len(dst)`, maka semua elements  `src`  akan ter-copy  **karena jumlahnya di bawah atau sama dengan lebar**  `dst`.

```go
dst := []string{"potato", "potato", "potato"}
src := []string{"watermelon", "pinnaple"}
n := copy(dst, src)

fmt.Println(dst) // watermelon pinnaple potato
fmt.Println(src) // watermelon pinnaple
fmt.Println(n)   // 2
```

Jika dilihat pada kode di atas, isi  `dst`  masih tetap 3 elements, tapi dua elements pertama adalah sama dengan  `src`. Element terakhir  `dst`  isinya tidak berubah, tetap  `potato`, hal ini karena proses copy hanya memutasi element ke-1 dan ke-2 milik  `dst`, karena memang pada  `src`  hanya dua itu elements-nya.

### Pengaksesan Elemen Slice Dengan 3 Indeks

**3 index**  adalah teknik slicing elemen yang sekaligus menentukan kapasitasnya. Cara menggunakannnya yaitu dengan menyisipkan angka kapasitas di belakang, seperti  `fruits[0:1:1]`. Angka kapasitas yang diisikan tidak boleh melebihi kapasitas slice yang akan di slicing.

Berikut merupakan contoh penerapannya.

```go
var fruits = []string{"apple", "grape", "banana"}
var aFruits = fruits[0:2]
var bFruits = fruits[0:2:2]

fmt.Println(fruits)      // ["apple", "grape", "banana"]
fmt.Println(len(fruits)) // len: 3
fmt.Println(cap(fruits)) // cap: 3

fmt.Println(aFruits)      // ["apple", "grape"]
fmt.Println(len(aFruits)) // len: 2
fmt.Println(cap(aFruits)) // cap: 3

fmt.Println(bFruits)      // ["apple", "grape"]
fmt.Println(len(bFruits)) // len: 2
fmt.Println(cap(bFruits)) // cap: 2
```

## Map
**Map**  adalah tipe data asosiatif yang ada di Go, berbentuk  _key-value pair_. Untuk setiap data (atau value) yang disimpan, disiapkan juga key-nya. Key harus unik, karena digunakan sebagai penanda (atau identifier) untuk pengaksesan value yang bersangkutan.

Kalau dilihat,  `map`  mirip seperti slice, hanya saja indeks yang digunakan untuk pengaksesan bisa ditentukan sendiri tipe-nya (indeks tersebut adalah key).

### Penggunaan Map

Cara menggunakan map cukup dengan menuliskan keyword  `map`  diikuti tipe data key dan value-nya. Agar lebih mudah dipahami, silakan perhatikan contoh di bawah ini.

```go
var chicken map[string]int
chicken = map[string]int{}

chicken["januari"] = 50
chicken["februari"] = 40

fmt.Println("januari", chicken["januari"]) // januari 50
fmt.Println("mei",     chicken["mei"])     // mei 0
```

Variabel  `chicken`  dideklarasikan sebagai map, dengan tipe data key adalah  `string`  dan value-nya  `int`. Dari kode tersebut bisa dilihat bagaimana cara penggunaan keyword  `map`.

Kode  `map[string]int`  maknanya adalah, tipe data  `map`  dengan key bertipe  `string`  dan value bertipe  `int`.

Default nilai variabel  `map`  adalah  `nil`. Oleh karena itu perlu dilakukan inisialisasi nilai default di awal, caranya cukup dengan tambahkan kurung kurawal pada akhir tipe, contoh seperti pada kode di atas:  `map[string]int{}`.

Cara menge-set nilai pada sebuah map adalah dengan menuliskan variabel-nya, kemudian disisipkan  `key`  pada kurung siku variabel (mirip seperti cara pengaksesan elemen slice), lalu isi nilainya. Contohnya seperti  `chicken["februari"] = 40`. Sedangkan cara pengambilan value adalah cukup dengan menyisipkan  `key`  pada kurung siku variabel.

Pengisian data pada map bersifat  **overwrite**, ketika variabel sudah memiliki item dengan key yang sama, maka value lama akan ditimpa dengan value baru.

Pada pengaksesan item menggunakan key yang belum tersimpan di map, akan dikembalikan nilai default tipe data value-nya. Contohnya seperti pada kode di atas,  `chicken["mei"]`  menghasilkan nilai 0 (nilai default tipe  `int`), karena belum ada item yang tersimpan menggunakan key  `"mei"`.

### Inisialisasi Nilai Map

Zero value dari map adalah  `nil`, maka tiap variabel bertipe map harus di-inisialisasi secara explisit nilai awalnya (agar tidak  `nil`).

```go
var data map[string]int
data["one"] = 1
// akan muncul error!

data = map[string]int{}
data["one"] = 1
// tidak ada error
```

Nilai variabel bertipe map bisa didefinisikan di awal, caranya dengan menambahkan kurung kurawal setelah tipe data, lalu menuliskan key dan value di dalamnya. Cara ini sekilas mirip dengan definisi nilai array/slice namun dalam bentuk key-value.

```go
// cara horizontal
var chicken1 = map[string]int{"januari": 50, "februari": 40}

// cara vertical
var chicken2 = map[string]int{
    "januari":  50,
    "februari": 40,
}
```

Key dan value dituliskan dengan pembatas tanda titik dua (`:`). Sedangkan tiap itemnya dituliskan dengan pembatas tanda koma (`,`). Khusus deklarasi dengan gaya vertikal, tanda koma perlu dituliskan setelah item terakhir.

Variabel  `map`  bisa di-inisialisasi dengan tanpa nilai awal, caranya menggunakan tanda kurung kurawal, contoh:  `map[string]int{}`. Atau bisa juga dengan menggunakan keyword  `make`  dan  `new`. Contohnya bisa dilihat pada kode berikut. Ketiga cara di bawah ini intinya adalah sama.

```go
var chicken3 = map[string]int{}
var chicken4 = make(map[string]int)
var chicken5 = *new(map[string]int)
```

Khusus inisialisasi data menggunakan keyword  `new`, yang dihasilkan adalah data pointer. Untuk mengambil nilai aslinya bisa dengan menggunakan tanda asterisk (`*`). Topik pointer akan dibahas lebih detail pada bagian pointer.

### Iterasi Item Map Menggunakan  `for`  -  `range`

Item variabel  `map`  bisa di iterasi menggunakan  `for`  -  `range`. Cara penerapannya masih sama seperti pada slice, pembedanya data yang dikembalikan di tiap perulangan adalah key dan value, bukan indeks dan elemen. Contohnya bisa dilihat pada kode berikut.

```go
var chicken = map[string]int{
    "januari":  50,
    "februari": 40,
    "maret":    34,
    "april":    67,
}

for key, val := range chicken {
    fmt.Println(key, "  \t:", val)
}
```

### Menghapus Item Map

Fungsi  `delete()`  digunakan untuk menghapus item dengan key tertentu pada variabel map. Cara penggunaannya, dengan memasukan objek map dan key item yang ingin dihapus sebagai parameter.

```go
var chicken = map[string]int{"januari": 50, "februari": 40}

fmt.Println(len(chicken)) // 2
fmt.Println(chicken)

delete(chicken, "januari")

fmt.Println(len(chicken)) // 1
fmt.Println(chicken)
```

Item yang memiliki key  `"januari"`  dalam variabel  `chicken`  akan dihapus.

Fungsi  `len()`  jika digunakan pada map akan mengembalikan jumlah item.

### Deteksi Keberadaan Item Dengan Key Tertentu

Ada cara untuk mengetahui apakah dalam sebuah variabel map terdapat item dengan key tertentu atau tidak, yaitu dengan memanfaatkan 2 variabel sebagai penampung nilai kembalian pengaksesan item. Return value ke-2 ini adalah opsional, isinya nilai  `bool`  yang menunjukkan ada atau tidaknya item yang dicari.

```go
var chicken = map[string]int{"januari": 50, "februari": 40}
var value, isExist = chicken["mei"]

if isExist {
    fmt.Println(value)
} else {
    fmt.Println("item is not exists")
}
```

### Kombinasi Slice & Map

Slice dan  `map`  bisa dikombinasikan, dan sering digunakan pada banyak kasus, contohnya seperti data array yang berisikan informasi siswa, dan banyak lainnya.

Cara menggunakannya cukup mudah, contohnya seperti  `[]map[string]int`, artinya slice yang tipe tiap elemen-nya adalah  `map[string]int`.

Agar lebih jelas, silakan praktekan contoh berikut.

```go
var chickens = []map[string]string{
    map[string]string{"name": "chicken blue",   "gender": "male"},
    map[string]string{"name": "chicken red",    "gender": "male"},
    map[string]string{"name": "chicken yellow", "gender": "female"},
}

for _, chicken := range chickens {
    fmt.Println(chicken["gender"], chicken["name"])
}
```

Variabel  `chickens`  di atas berisikan informasi bertipe  `map[string]string`, yang kebetulan tiap elemen memiliki 2 key yang sama.

Jika anda menggunakan versi go terbaru, cara deklarasi slice-map bisa dipersingkat, tipe tiap elemen tidak wajib untuk dituliskan.

```go
var chickens = []map[string]string{
    {"name": "chicken blue",   "gender": "male"},
    {"name": "chicken red",    "gender": "male"},
    {"name": "chicken yellow", "gender": "female"},
}
```

Dalam  `[]map[string]string`, tiap elemen bisa saja memiliki key yang berbeda-beda, sebagai contoh seperti kode berikut.

```go
var data = []map[string]string{
    {"name": "chicken blue", "gender": "male", "color": "brown"},
    {"address": "mangga street", "id": "k001"},
    {"community": "chicken lovers"},
}
```

## Fungsi
Fungsi merupakan aspek penting dalam pemrograman. Definisi fungsi sendiri adalah sekumpulan blok kode yang dibungkus dengan nama tertentu. Penerapan fungsi yang tepat akan menjadikan kode lebih modular dan juga  _dry_  (kependekan dari  _don't repeat yourself_), tak perlu menuliskan banyak kode yang kegunaannya berkali-kali, cukup sekali saja lalu panggil sesuai kebutuhan.

Pada chapter ini kita akan belajar tentang penggunaan fungsi di Go.

### Penerapan Fungsi

Sebenarnya tanpa sadar, kita sudah menerapkan fungsi pada pembahasan-pembahasan sebelum ini, yaitu pada fungsi  `main`. Fungsi  `main`  merupakan fungsi yang paling utama pada program Go.

Cara membuat fungsi cukup mudah, yaitu dengan menuliskan keyword  `func`, diikuti setelahnya nama fungsi, kurung yang berisikan parameter, dan kurung kurawal untuk membungkus blok kode.

Parameter sendiri adalah variabel yang disisipkan pada saat pemanggilan fungsi.

Silakan lihat dan praktekan kode tentang implementasi fungsi berikut.

```go
package main

import "fmt"
import "strings"

func main() {
    var names = []string{"John", "Wick"}
    printMessage("halo", names)
}

func printMessage(message string, arr []string) {
    var nameString = strings.Join(arr, " ")
    fmt.Println(message, nameString)
}
```

Pada kode di atas, sebuah fungsi baru dibuat dengan nama  `printMessage`  memiliki 2 buah parameter yaitu string  `message`  dan slice string  `arr`.

Fungsi tersebut dipanggil dalam  `main`, dengan disisipkan 2 buah data sebagai parameter, data pertama adalah string  `"hallo"`  yang ditampung parameter  `message`, dan parameter ke 2 adalah slice string  `names`  yang nilainya ditampung oleh parameter  `arr`.

Di dalam  `printMessage`, nilai  `arr`  yang merupakan slice string digabungkan menjadi sebuah string dengan pembatas adalah karakter  **spasi**. Penggabungan slice dapat dilakukan dengan memanfaatkan fungsi  `strings.Join()`  (berada di dalam package  `strings`).

### Fungsi Dengan Return Value / Nilai Balik

Sebuah fungsi bisa dirancang tidak mengembalikan nilai balik (_void_), atau bisa mengembalikan suatu nilai. Fungsi yang memiliki nilai kembalian, harus ditentukan tipe data nilai baliknya pada saat deklarasi.

Program berikut merupakan contoh penerapan fungsi yang memiliki return value.

```go
package main

import (
    "fmt"
    "math/rand"
    "time"
)

func main() {
    rand.Seed(time.Now().Unix())
    var randomValue int

    randomValue = randomWithRange(2, 10)
    fmt.Println("random number:", randomValue)
    randomValue = randomWithRange(2, 10)
    fmt.Println("random number:", randomValue)
    randomValue = randomWithRange(2, 10)
    fmt.Println("random number:", randomValue)
}

func randomWithRange(min, max int) int {
    var value = rand.Int() % (max - min + 1) + min
    return value
}
```

Fungsi  `randomWithRange`  bertugas untuk  _generate_  angka acak sesuai dengan range yang ditentukan, yang kemudian angka tersebut dijadikan nilai kembalian fungsi.

Cara menentukan tipe data nilai balik fungsi adalah dengan menuliskan tipe data yang diinginkan setelah kurung parameter. Bisa dilihat pada kode di atas, bahwa  `int`  merupakan tipe data nilai balik fungsi  `randomWithRange`.

```go
func randomWithRange(min, max int) int
```

Sedangkan cara untuk mengembalikan nilai itu sendiri adalah dengan menggunakan keyword  `return`  diikuti data yang ingin dikembalikan. Pada contoh di atas,  `return value`  artinya nilai variabel  `value`  dijadikan nilai kembalian fungsi.

Eksekusi keyword  `return`  akan menjadikan proses dalam blok fungsi berhenti pada saat itu juga. Semua statement setelah keyword tersebut tidak akan dieksekusi.

----------

Dari kode di atas mungkin ada beberapa hal yang belum pernah kita lakukan pada pembahasan-pembahasan sebelumnya, kita akan bahas satu-persatu.

### Penggunaan Fungsi  `rand.Seed()`

Fungsi ini diperlukan untuk memastikan bahwa angka random yang akan di-generate benar-benar acak. Kita bisa gunakan angka apa saja sebagai nilai parameter fungsi ini (umumnya diisi  `time.Now().Unix()`).

```go
rand.Seed(time.Now().Unix())
```

Fungsi  `rand.Seed()`  berada dalam package  `math/rand`, yang harus di-import terlebih dahulu sebelum bisa dimanfaatkan.

Package  `time`  juga perlu di-import karena kita menggunakan fungsi  `(time.Now().Unix())`  di situ.

### Import Banyak Package

Penulisan keyword  `import`  untuk banyak package bisa dilakukan dengan dua cara, dengan menuliskannya di tiap package, atau cukup sekali saja, bebas.

```go
import "fmt"
import "math/rand"
import "time"

// atau

import (
    "fmt"
    "math/rand"
    "time"
)
```

### Deklarasi Parameter Bertipe Data Sama

Khusus untuk fungsi yang tipe data parameternya sama, bisa ditulis dengan gaya yang unik. Tipe datanya dituliskan cukup sekali saja di akhir. Contohnya bisa dilihat pada kode berikut.

```
func nameOfFunc(paramA type, paramB type, paramC type) returnType
func nameOfFunc(paramA, paramB, paramC type) returnType

func randomWithRange(min int, max int) int
func randomWithRange(min, max int) int
```

### Penggunaan Keyword  `return`  Untuk Menghentikan Proses Dalam Fungsi

Selain sebagai penanda nilai balik, keyword  `return`  juga bisa dimanfaatkan untuk menghentikan proses dalam blok fungsi di mana ia dipakai. Contohnya bisa dilihat pada kode berikut.

```go
package main

import "fmt"

func main() {
    divideNumber(10, 2)
    divideNumber(4, 0)
    divideNumber(8, -4)
}

func divideNumber(m, n int) {
    if n == 0 {
        fmt.Printf("invalid divider. %d cannot divided by %d\n", m, n)
        return
    }

    var res = m / n
    fmt.Printf("%d / %d = %d\n", m, n, res)
}
```

Fungsi  `divideNumber`  dirancang tidak memiliki nilai balik. Fungsi ini dibuat untuk membungkus proses pembagian 2 bilangan, lalu menampilkan hasilnya.

Di dalamnya terdapat proses validasi nilai variabel pembagi, jika nilainya adalah 0, maka akan ditampilkan pesan bahwa pembagian tidak bisa dilakukan, lalu proses dihentikan pada saat itu juga (dengan memanfaatkan keyword  `return`). Jika nilai pembagi valid, maka proses pembagian diteruskan.

## Fungsi Multiple Return
Umumnya fungsi hanya memiliki satu buah nilai balik saja. Jika ada kebutuhan di mana data yang dikembalikan harus banyak, biasanya digunakanlah tipe seperti  `map`, slice, atau  `struct`  sebagai nilai balik.

Go menyediakan kapabilitas bagi programmer untuk membuat fungsi memiliki banyak nilai balik. Pada chapter ini akan dibahas bagaimana penerapannya.

### Penerapan Fungsi Multiple Return

Cara membuat fungsi yang memiliki banyak nilai balik tidaklah sulit. Tinggal tulis saja pada saat deklarasi fungsi semua tipe data nilai yang dikembalikan, dan pada keyword  `return`  tulis semua data yang ingin dikembalikan. Contoh bisa dilihat pada berikut.

```go
package main

import "fmt"
import "math"

func calculate(d float64) (float64, float64) {
    // hitung luas
    var area = math.Pi * math.Pow(d / 2, 2)
    // hitung keliling
    var circumference = math.Pi * d

    // kembalikan 2 nilai
    return area, circumference
}
```

Fungsi  `calculate()`  di atas menerima satu buah parameter (`diameter`) yang digunakan dalam proses perhitungan. Di dalam fungsi tersebut ada 2 hal yang dihitung, yaitu nilai  **keliling**  dan  **lingkaran**. Kedua nilai tersebut kemudian dijadikan sebagai return value fungsi.

Cara pendefinisian banyak nilai balik bisa dilihat pada kode di atas, langsung tulis tipe data semua nilai balik dipisah tanda koma, lalu ditambahkan kurung di antaranya.

```go
func calculate(d float64) (float64, float64)
```

Tak lupa di bagian penulisan keyword  `return`  harus dituliskan juga semua data yang dijadikan nilai balik (dengan pemisah tanda koma).

```go
return area, circumference
```

Implementasi dari fungsi  `calculate()`  di atas, bisa dilihat pada kode berikut.

```go
func main() {
    var diameter float64 = 15
    var area, circumference = calculate(diameter)

    fmt.Printf("luas lingkaran\t\t: %.2f \n", area)
    fmt.Printf("keliling lingkaran\t: %.2f \n", circumference)
}
```

Karena fungsi tersebut memiliki banyak nilai balik, maka pada pemanggilannya harus disiapkan juga banyak variabel untuk menampung nilai kembalian yang ada (sesuai jumlah nilai balik fungsi).

```go
var area, circumference = calculate(diameter)
```

### Fungsi Dengan Predefined Return Value

Keunikan lainnya yang jarang ditemui di bahasa lain adalah, di Go variabel yang digunakan sebagai nilai balik bisa didefinisikan di awal.

```go
func calculate(d float64) (area float64, circumference float64) {
    area = math.Pi * math.Pow(d / 2, 2)
    circumference = math.Pi * d

    return
}
```

Fungsi  `calculate`  kita modifikasi menjadi lebih sederhana. Bisa dilihat di kode di atas, ada cukup banyak perbedaan dibanding fungsi  `calculate`  sebelumnya. Perhatikan kode berikut.

```go
func calculate(d float64) (area float64, circumference float64) {
```

Fungsi dideklarasikan memiliki 2 buah tipe data, dan variabel yang nantinya dijadikan nilai balik juga dideklarasikan. Variabel  `area`  yang bertipe  `float64`, dan  `circumference`  bertipe  `float64`.

Karena variabel nilai balik sudah ditentukan di awal, untuk mengembalikan nilai cukup dengan memanggil  `return`  tanpa perlu diikuti variabel apapun. Nilai terakhir  `area`  dan  `circumference`  sebelum pemanggilan keyword  `return`  adalah hasil dari fungsi di atas.

----------

Ada beberapa hal baru dari kode di atas yang perlu dibahas, seperti  `math.Pow()`  dan  `math.Pi`. Berikut adalah penjelasannya.

#### Penggunaan Fungsi  `math.Pow()`

Fungsi  `math.Pow()`  digunakan untuk memangkat nilai.  `math.Pow(2, 3)`  berarti 2 pangkat 3, hasilnya 8. Fungsi ini berada dalam package  `math`.

#### Penggunaan Konstanta  `math.Pi`

`math.Pi`  adalah konstanta bawaan  `package math`  yang merepresentasikan  **Pi**  atau  **22/7**.

## Fungsi Variadic
Go mengadopsi konsep  **variadic function**  atau pembuatan fungsi dengan parameter sejenis yang tak terbatas. Maksud  **tak terbatas**  di sini adalah jumlah parameter yang disisipkan ketika pemanggilan fungsi bisa berapa saja.

Parameter variadic memiliki sifat yang mirip dengan slice. Nilai dari parameter-parameter yang disisipkan bertipe data sama, dan ditampung oleh sebuah variabel saja. Cara pengaksesan tiap datanya juga sama, dengan menggunakan index.

Pada chapter ini kita akan belajar mengenai cara penerapan fungsi variadic.

### Penerapan Fungsi Variadic

Deklarasi parameter variadic sama dengan cara deklarasi variabel biasa, pembedanya adalah pada parameter jenis ini ditambahkan tanda titik tiga kali (`...`) tepat setelah penulisan variabel (sebelum tipe data). Nantinya semua nilai yang disisipkan sebagai parameter akan ditampung oleh variabel tersebut.

Berikut merupakan contoh penerepannya.

```go
package main

import "fmt"

func main() {
    var avg = calculate(2, 4, 3, 5, 4, 3, 3, 5, 5, 3)
    var msg = fmt.Sprintf("Rata-rata : %.2f", avg)
    fmt.Println(msg)
}

func calculate(numbers ...int) float64 {
    var total int = 0
    for _, number := range numbers {
        total += number
    }

    var avg = float64(total) / float64(len(numbers))
    return avg
}
```

Bisa dilihat pada fungsi  `calculate()`, parameter  `numbers`  dideklarasikan dengan disisipkan tanda 3 titik (`...`), menandakan bahwa  `numbers`  adalah sebuah parameter variadic dengan tipe data  `int`.

```go
func calculate(numbers ...int) float64 {
```

Pemanggilan fungsi dilakukan seperti biasa, hanya saja jumlah parameter yang disisipkan bisa banyak.

```go
var avg = calculate(2, 4, 3, 5, 4, 3, 3, 5, 5, 3)
```

Nilai tiap parameter bisa diakses seperti cara pengaksesan tiap elemen slice. Pada contoh di atas metode yang dipilih adalah  `for`  -  `range`.

```go
for _, number := range numbers {
```

----------

Berikut merupakan penjelasan tambahan dari kode yang telah kita tulis.

#### Penggunaan Fungsi  `fmt.Sprintf()`

Fungsi  `fmt.Sprintf()`  pada dasarnya sama dengan  `fmt.Printf()`, hanya saja fungsi ini tidak menampilkan nilai, melainkan mengembalikan nilainya dalam bentuk string. Pada kasus di atas, nilai kembalian  `fmt.Sprintf()`  ditampung oleh variabel  `msg`.

Selain  `fmt.Sprintf()`, ada juga  `fmt.Sprint()`  dan  `fmt.Sprintln()`.

#### Penggunaan Fungsi  `float64()`

Sebelumnya sudah dibahas bahwa  `float64`  merupakan tipe data. Tipe data jika ditulis sebagai fungsi (penandanya ada tanda kurungnya) berguna untuk  **casting**. Casting sendiri adalah teknik untuk konversi tipe sebuah data ke tipe lain. Sebagian besar tipe data dasar yang telah dipelajari pada bagian variabel bisa di-cast. Dan cara penerapannya juga sama, cukup panggil sebagai fungsi, lalu masukan data yang ingin dikonversi sebagai parameter.

Pada contoh di atas, variabel  `total`  yang tipenya adalah  `int`, dikonversi menjadi  `float64`, begitu juga  `len(numbers)`  yang menghasilkan  `int`  dikonversi ke  `float64`.

Variabel  `avg`  perlu dijadikan  `float64`  karena penghitungan rata-rata lebih sering menghasilkan nilai desimal.

Operasi bilangan (perkalian, pembagian, dan lainnya) di Go hanya bisa dilakukan jika tipe datanya sejenis. Maka dari itulah perlu adanya casting ke tipe  `float64`  pada tiap operand.

----------

### Pengisian Parameter Fungsi Variadic Menggunakan Data Slice

Slice bisa digunakan sebagai parameter variadic. Caranya dengan menambahkan tanda titik tiga kali, tepat setelah nama variabel yang dijadikan parameter. Contohnya bisa dilihat pada kode berikut.

```go
var numbers = []int{2, 4, 3, 5, 4, 3, 3, 5, 5, 3}
var avg = calculate(numbers...)
var msg = fmt.Sprintf("Rata-rata : %.2f", avg)

fmt.Println(msg)
```

Pada kode di atas, variabel  `numbers`  yang merupakan slice int, disisipkan ke fungsi  `calculate()`  sebagai parameter variadic (bisa dilihat tanda 3 titik setelah penulisan variabel). Teknik ini sangat berguna ketika sebuah data slice ingin difungsikan sebagai parameter variadic.

Perhatikan juga kode berikut ini. Intinya adalah sama, hanya caranya yang berbeda.

```go
var numbers = []int{2, 4, 3, 5, 4, 3, 3, 5, 5, 3}
var avg = calculate(numbers...)

// atau

var avg = calculate(2, 4, 3, 5, 4, 3, 3, 5, 5, 3)
```

Pada deklarasi parameter fungsi variadic, tanda 3 titik (`...`) dituliskan sebelum tipe data parameter. Sedangkan pada pemanggilan fungsi dengan menyisipkan parameter array, tanda tersebut dituliskan di belakang variabelnya.

### Fungsi Dengan Parameter Biasa & Variadic

Parameter variadic bisa dikombinasikan dengan parameter biasa, dengan syarat parameter variadic-nya harus diposisikan di akhir. Contohnya bisa dilihat pada kode berikut.

```go
import "fmt"
import "strings"

func yourHobbies(name string, hobbies ...string) {
    var hobbiesAsString = strings.Join(hobbies, ", ")

    fmt.Printf("Hello, my name is: %s\n", name)
    fmt.Printf("My hobbies are: %s\n", hobbiesAsString)
}
```

Nilai parameter pertama fungsi  `yourHobbies()`  akan ditampung oleh  `name`, sedangkan nilai parameter kedua dan seterusnya akan ditampung oleh  `hobbies`  sebagai slice.

Cara pemanggilannya masih sama seperi pada fungsi biasa.

```go
func main() {
    yourHobbies("wick", "sleeping", "eating")
}
```

Jika parameter kedua dan seterusnya ingin diisi dengan data dari slice, maka gunakan tanda titik tiga kali.

```go
func main() {
    var hobbies = []string{"sleeping", "eating"}
    yourHobbies("wick", hobbies...)
}
```

## Fungsi Closure
Definisi  **Closure**  adalah sebuah fungsi yang bisa disimpan dalam variabel. Dengan menerapkan konsep tersebut, kita bisa membuat fungsi di dalam fungsi, atau bahkan membuat fungsi yang mengembalikan fungsi.

Closure merupakan  _anonymous function_  atau fungsi tanpa nama. Biasa dimanfaatkan untuk membungkus suatu proses yang hanya dipakai sekali atau dipakai pada blok tertentu saja.

### Closure Disimpan Sebagai Variabel

Sebuah fungsi tanpa nama bisa disimpan dalam variabel. Variabel yang menyimpan closure memiliki sifat seperti fungsi yang disimpannya. Di bawah ini adalah contoh program sederhana untuk mencari nilai terendah dan tertinggi dari suatu array. Logika pencarian dibungkus dalam closure yang ditampung oleh variabel  `getMinMax`.

```go
package main

import "fmt"

func main() {
    var getMinMax = func(n []int) (int, int) {
        var min, max int
        for i, e := range n {
            switch {
            case i == 0:
                max, min = e, e
            case e > max:
                max = e
            case e < min:
                min = e
            }
        }
        return min, max
    }

    var numbers = []int{2, 3, 4, 3, 4, 2, 3}
    var min, max = getMinMax(numbers)
    fmt.Printf("data : %v\nmin  : %v\nmax  : %v\n", numbers, min, max)
}
```

Bisa dilihat pada kode di atas bagaimana sebuah closure dibuat dan dipanggil. Sedikit berbeda memang dibanding pembuatan fungsi biasa. Fungsi ditulis tanpa nama, lalu ditampung dalam variabel.

```go
var getMinMax = func(n []int) (int, int) {
    // ...
}
```

Cara pemanggilannya, dengan menuliskan nama variabel tersebut sebagai fungsi, seperti pemanggilan fungsi biasa.

```go
var min, max = getMinMax(numbers)
```

----------

Berikut adalah penjelasan tambahan mengenai kode di atas

### Penggunaan Template String  `%v`

Template  `%v`  digunakan untuk menampilkan segala jenis data. Bisa array, int, float, bool, dan lainnya.

```go
fmt.Printf("data : %v\nmin  : %v\nmax  : %v\n", numbers, min, max)
```

Bisa dilihat pada statement di atas, data bertipe array dan numerik ditampilkan menggunakan  `%v`. Template ini biasa dimanfaatkan untuk menampilkan sebuah data yang tipe nya bisa dinamis atau belum diketahui. Sangat tepat jika digunakan pada data bertipe  `interface{}`.

----------

### Immediately-Invoked Function Expression (IIFE)

Closure jenis ini dieksekusi langsung pada saat deklarasinya. Biasa digunakan untuk membungkus proses yang hanya dilakukan sekali, bisa mengembalikan nilai, bisa juga tidak.

Di bawah ini merupakan contoh sederhana penerapan metode IIFE untuk filtering data array.

```go
package main

import "fmt"

func main() {
    var numbers = []int{2, 3, 0, 4, 3, 2, 0, 4, 2, 0, 3}

    var newNumbers = func(min int) []int {
        var r []int
        for _, e := range numbers {
            if e < min {
                continue
            }
            r = append(r, e)
        }
        return r
    }(3)

    fmt.Println("original number :", numbers)
    fmt.Println("filtered number :", newNumbers)
}
```

Ciri khas IIFE adalah adanya kurung parameter tepat setelah deklarasi closure berakhir. Jika ada parameter, bisa juga dituliskan dalam kurung parameternya.

```go
var newNumbers = func(min int) []int {
    // ...
}(3)
```

Pada contoh di atas IIFE menghasilkan nilai balik yang kemudian ditampung  `newNumber`. Perlu diperhatikan bahwa yang ditampung adalah  **nilai kembaliannya**  bukan body fungsi atau  **closure**.

> Closure bisa juga dengan gaya manifest typing, caranya dengan menuliskan skema closure-nya sebagai tipe data. Contoh:  
> ```go
> var closure (func (string, int, []string) int)
>     closure = func (a string, b int, c []string) int {
>     // ..
> }
> ```

### Closure Sebagai Nilai Kembalian

Salah satu keunikan closure lainnya adalah bisa dijadikan sebagai nilai balik fungsi, cukup aneh memang, tapi pada suatu kondisi teknik ini sangat membantu. Di bawah ini disediakan sebuah fungsi bernama  `findMax()`, fungsi ini salah satu nilai kembaliannya berupa closure.

```go
package main

import "fmt"

func findMax(numbers []int, max int) (int, func() []int) {
    var res []int
    for _, e := range numbers {
        if e <= max {
            res = append(res, e)
        }
    }
    return len(res), func() []int {
        return res
    }
}
```

Nilai kembalian ke-2 pada fungsi di atas adalah closure dengan skema  `func() []int`. Bisa dilihat di bagian akhir, ada fungsi tanpa nama yang dikembalikan.

```go
return len(res), func() []int {
    return res
}
```

> Fungsi tanpa nama yang akan dikembalikan boleh disimpan pada variabel terlebih dahulu. Contohnya:  
> ```go
> var getNumbers = func() []int {
>     return res
> }
> return len(res), getNumbers
> ```

Sedikit tentang fungsi  `findMax()`, fungsi ini digunakan untuk mencari banyaknya angka-angka yang nilainya di bawah atau sama dengan angka tertentu. Nilai kembalian pertama adalah jumlah angkanya. Nilai kembalian kedua berupa closure yang mengembalikan angka-angka yang dicari. Berikut merupakan contoh implementasi fungsi tersebut.

```go
func main() {
    var max = 3
    var numbers = []int{2, 3, 0, 4, 3, 2, 0, 4, 2, 0, 3}
    var howMany, getNumbers = findMax(numbers, max)
    var theNumbers = getNumbers()

    fmt.Println("numbers\t:", numbers)
    fmt.Printf("find \t: %d\n\n", max)

    fmt.Println("found \t:", howMany)    // 9
    fmt.Println("value \t:", theNumbers) // [2 3 0 3 2 0 2 0 3]
}
```

## Fungsi sebagai parameter
Setelah pada chapter sebelumnya kita belajar mengenai fungsi yang mengembalikan nilai balik berupa fungsi, kali ini topiknya tidak kalah unik, yaitu fungsi yang digunakan sebagai parameter.

Di Go, fungsi bisa dijadikan sebagai tipe data variabel. Dari situ sangat memungkinkan untuk menjadikannya sebagai parameter juga.

### Penerapan Fungsi Sebagai Parameter

Cara membuat parameter fungsi adalah dengan langsung menuliskan skema fungsi nya sebagai tipe data. Contohnya bisa dilihat pada kode berikut.

```go
package main

import "fmt"
import "strings"

func filter(data []string, callback func(string) bool) []string {
    var result []string
    for _, each := range data {
        if filtered := callback(each); filtered {
            result = append(result, each)
        }
    }
    return result
}
```

Parameter  `callback`  merupakan sebuah closure yang dideklarasikan bertipe  `func(string) bool`. Closure tersebut dipanggil di tiap perulangan dalam fungsi  `filter()`.

Fungsi  `filter()`  sendiri kita buat untuk filtering data array (yang datanya didapat dari parameter pertama), dengan kondisi filter bisa ditentukan sendiri. Di bawah ini adalah contoh pemanfaatan fungsi tersebut.

```go
func main() {
    var data = []string{"wick", "jason", "ethan"}
    var dataContainsO = filter(data, func(each string) bool {
        return strings.Contains(each, "o")
    })
    var dataLenght5 = filter(data, func(each string) bool {
        return len(each) == 5
    })

    fmt.Println("data asli \t\t:", data)
    // data asli : [wick jason ethan]

    fmt.Println("filter ada huruf \"o\"\t:", dataContainsO)
    // filter ada huruf "o" : [jason]

    fmt.Println("filter jumlah huruf \"5\"\t:", dataLenght5)
    // filter jumlah huruf "5" : [jason ethan]
}
```

Ada cukup banyak hal yang terjadi di dalam tiap pemanggilan fungsi  `filter()`  di atas. Berikut merupakan penjelasannya.

1.  Data array (yang didapat dari parameter pertama) akan di-looping.
2.  Di tiap perulangannya, closure  `callback`  dipanggil, dengan disisipkan data tiap elemen perulangan sebagai parameter.
3.  Closure  `callback`  berisikan kondisi filtering, dengan hasil bertipe  `bool`  yang kemudian dijadikan nilai balik dikembalikan.
4.  Di dalam fungsi  `filter()`  sendiri, ada proses seleksi kondisi (yang nilainya didapat dari hasil eksekusi closure  `callback`). Ketika kondisinya bernilai  `true`, maka data elemen yang sedang diulang dinyatakan lolos proses filtering.
5.  Data yang lolos ditampung variabel  `result`. Variabel tersebut dijadikan sebagai nilai balik fungsi  `filter()`.

Pada  `dataContainsO`, parameter kedua fungsi  `filter()`  berisikan statement untuk deteksi apakah terdapat substring  `"o"`  di dalam nilai variabel  `each`  (yang merupakan data tiap elemen), jika iya, maka kondisi filter bernilai  `true`, dan sebaliknya.

pada contoh ke-2 (`dataLength5`), closure  `callback`  berisikan statement untuk deteksi jumlah karakter tiap elemen. Jika ada elemen yang jumlah karakternya adalah 5, berarti elemen tersebut lolos filter.

Memang butuh usaha ekstra untuk memahami pemanfaatan closure sebagai parameter fungsi. Tapi setelah paham, penerapan teknik ini pada kondisi yang tepat akan sangat membantu proses pembuatan aplikasi.

### Alias Skema Closure

Kita sudah mempelajari bahwa closure bisa dimanfaatkan sebagai tipe parameter, contohnya seperti pada fungsi  `filter()`. Pada fungsi tersebut kebetulan skema tipe parameter closure-nya tidak terlalu panjang, hanya ada satu buah parameter dan satu buah nilai balik.

Pada fungsi yang skema-nya cukup panjang, akan lebih baik jika menggunakan alias, apalagi ketika ada parameter fungsi lain yang juga menggunakan skema yang sama. Membuat alias fungsi berarti menjadikan skema fungsi tersebut menjadi tipe data baru. Caranya dengan menggunakan keyword  `type`. Contoh:

```go
type FilterCallback func(string) bool

func filter(data []string, callback FilterCallback) []string {
    // ...
}
```

Skema  `func(string) bool`  diubah menjadi tipe dengan nama  `FilterCallback`. Tipe tersebut kemudian digunakan sebagai tipe data parameter  `callback`.

----------

Di bawah ini merupakan penjelasan tambahan mengenai fungsi  `strings.Contains()`.

### Penggunaan Fungsi  `string.Contains()`

Inti dari fungsi ini adalah untuk deteksi apakah sebuah substring adalah bagian dari string, jika iya maka akan bernilai  `true`, dan sebaliknya. Contoh penggunaannya:

```go
var result = strings.Contains("Golang", "ang")
// true
```

Variabel  `result`  bernilai  `true`  karena string  `"ang"`  merupakan bagian dari string  `"Golang"`.

## Pointer
Pointer adalah  _reference_  atau alamat memori. Variabel pointer berarti variabel yang berisi alamat memori suatu nilai. Sebagai contoh sebuah variabel bertipe integer memiliki nilai  **4**, maka yang dimaksud pointer adalah  **alamat memori di mana nilai 4 disimpan**, bukan nilai 4 itu sendiri.

Variabel-variabel yang memiliki  _reference_  atau alamat pointer yang sama, saling berhubungan satu sama lain dan nilainya pasti sama. Ketika ada perubahan nilai, maka akan memberikan efek kepada variabel lain (yang referensi-nya sama) yaitu nilainya ikut berubah.

### Penerapan Pointer

Variabel bertipe pointer ditandai dengan adanya tanda  **asterisk**  (`*`) tepat sebelum penulisan tipe data ketika deklarasi.

```go
var number *int
var name *string
```

Nilai default variabel pointer adalah  `nil`  (kosong). Variabel pointer tidak bisa menampung nilai yang bukan pointer, dan sebaliknya variabel biasa tidak bisa menampung nilai pointer.

Ada dua hal penting yang perlu diketahui mengenai pointer:

-   Variabel biasa bisa diambil nilai pointernya, caranya dengan menambahkan tanda  **ampersand**  (`&`) tepat sebelum nama variabel. Metode ini disebut dengan  **referencing**.
-   Dan sebaliknya, nilai asli variabel pointer juga bisa diambil, dengan cara menambahkan tanda  **asterisk**  (`*`) tepat sebelum nama variabel. Metode ini disebut dengan  **dereferencing**.

OK, langsung saja kita praktekan.

```go
var numberA int = 4
var numberB *int = &numberA

fmt.Println("numberA (value)   :", numberA)  // 4
fmt.Println("numberA (address) :", &numberA) // 0xc20800a220

fmt.Println("numberB (value)   :", *numberB) // 4
fmt.Println("numberB (address) :", numberB)  // 0xc20800a220
```

Variabel  `numberB`  dideklarasikan bertipe pointer  `int`  dengan nilai awal adalah referensi variabel  `numberA`  (bisa dilihat pada kode  `&numberA`). Dengan ini, variabel  `numberA`  dan  `numberB`  menampung data dengan referensi alamat memori yang sama.

Variabel pointer jika di-print akan menghasilkan string alamat memori (dalam notasi heksadesimal), contohnya seperti  `numberB`  yang diprint menghasilkan  `0xc20800a220`.

Nilai asli sebuah variabel pointer bisa didapatkan dengan cara di-dereference terlebih dahulu (bisa dilihat pada kode  `*numberB`).

### Efek Perubahan Nilai Pointer

Ketika salah satu variabel pointer di ubah nilainya, sedang ada variabel lain yang memiliki referensi memori yang sama, maka nilai variabel lain tersebut juga akan berubah.

```go
var numberA int = 4
var numberB *int = &numberA

fmt.Println("numberA (value)   :", numberA)
fmt.Println("numberA (address) :", &numberA)
fmt.Println("numberB (value)   :", *numberB)
fmt.Println("numberB (address) :", numberB)

fmt.Println("")

numberA = 5

fmt.Println("numberA (value)   :", numberA)
fmt.Println("numberA (address) :", &numberA)
fmt.Println("numberB (value)   :", *numberB)
fmt.Println("numberB (address) :", numberB)
```

Variabel  `numberA`  dan  `numberB`  memiliki referensi memori yang sama. Perubahan pada salah satu nilai variabel tersebut akan memberikan efek pada variabel lainnya. Pada contoh di atas,  `numberA`  nilainya di ubah menjadi  `5`. membuat nilai asli variabel  `numberB`  ikut berubah menjadi  `5`.

### Parameter Pointer

Parameter bisa juga dirancang sebagai pointer. Cara penerapannya kurang lebih sama, dengan cara mendeklarasikan parameter sebagai pointer.

```go
package main

import "fmt"

func main() {
    var number = 4
    fmt.Println("before :", number) // 4

    change(&number, 10)
    fmt.Println("after  :", number) // 10
}

func change(original *int, value int) {
    *original = value
}
```

Fungsi  `change()`  memiliki 2 parameter, yaitu  `original`  yang tipenya adalah pointer  `int`, dan  `value`  yang bertipe  `int`. Di dalam fungsi tersebut nilai asli parameter pointer  `original`  diubah.

Fungsi  `change()`  kemudian diimplementasikan di  `main`. Variabel  `number`  yang nilai awalnya adalah  `4`  diambil referensi-nya lalu digunakan sebagai parameter pada pemanggilan fungsi  `change()`.

Nilai variabel  `number`  berubah menjadi  `10`  karena perubahan yang terjadi di dalam fungsi  `change`  adalah pada variabel pointer.

## Struct
Go tidak memiliki class yang ada di bahasa-bahasa strict OOP lain. Tapi Go memiliki tipe data struktur yang disebut dengan Struct.

Struct adalah kumpulan definisi variabel (atau property) dan atau fungsi (atau method), yang dibungkus sebagai tipe data baru dengan nama tertentu. Property dalam struct, tipe datanya bisa bervariasi. Mirip seperti  `map`, hanya saja key-nya sudah didefinisikan di awal, dan tipe data tiap itemnya bisa berbeda.

Dari sebuah struct, kita bisa buat variabel baru, yang memiliki atribut sesuai skema struct tersebut. Kita sepakati dalam buku ini, variabel tersebut dipanggil dengan istilah  **object**  atau  **object struct**.

> Konsep struct di golang mirip dengan konsep  **class**  pada OOP, meski sebenarnya berbeda. Di sini penulis menggunakan konsep OOP sebagai analogi, dengan tujuan untuk mempermudah dalam mencerna isi chapter ini.

Dengan memanfaatkan struct, grouping data akan lebih mudah, selain itu dan rapi dan gampang untuk di-maintain.

### Deklarasi Struct

Keyword  `type`  digunakan untuk deklarasi struct. Di bawah ini merupakan contoh cara penggunaannya.

```go
type student struct {
    name string
    grade int
}
```

Struct  `student`  dideklarasikan memiliki 2 property, yaitu  `name`  dan  `grade`. Objek yang dibuat dengan struct ini nantinya memiliki skema atau struktur yang sama.

### Penerapan Struct

Struct  `student`  yang sudah disiapkan di atas akan kita manfaatkan untuk membuat variabel objek. Property variabel tersebut di-isi kemudian ditampilkan.

```go
func main() {
    var s1 student
    s1.name = "john wick"
    s1.grade = 2

    fmt.Println("name  :", s1.name)
    fmt.Println("grade :", s1.grade)
}
```

Cara membuat variabel objek sama seperti pembuatan variabel biasa. Tinggal tulis saja nama variabel diikuti nama struct, contoh:  `var s1 student`.

Semua property variabel objek pada awalnya memiliki zero value sesuai tipe datanya.

Property variabel objek bisa diakses nilainya menggunakan notasi titik, contohnya  `s1.name`. Nilai property-nya juga bisa diubah, contohnya  `s1.grade = 2`.

### Inisialisasi Object Struct

Cara inisialisasi variabel objek adalah dengan menambahkan kurung kurawal setelah nama struct. Nilai masing-masing property bisa diisi pada saat inisialisasi.

Pada contoh berikut, terdapat 3 buah variabel objek yang dideklarasikan dengan cara berbeda.

```go
var s1 = student{}
s1.name = "wick"
s1.grade = 2

var s2 = student{"ethan", 2}

var s3 = student{name: "jason"}

fmt.Println("student 1 :", s1.name)
fmt.Println("student 2 :", s2.name)
fmt.Println("student 3 :", s3.name)
```

Pada kode di atas, variabel  `s1`  menampung objek cetakan  `student`. Variabel tersebut kemudian di-set nilai property-nya.

Variabel objek  `s2`  dideklarasikan dengan metode yang sama dengan  `s1`, pembedanya di  `s2`  nilai propertinya di isi langsung ketika deklarasi. Nilai pertama akan menjadi nilai property pertama (yaitu  `name`), dan selanjutnya berurutan.

Pada deklarasi  `s3`, dilakukan juga pengisian property ketika pencetakan objek. Hanya saja, yang diisi hanya  `name`  saja. Cara ini cukup efektif jika digunakan untuk membuat objek baru yang nilai property-nya tidak semua harus disiapkan di awal. Keistimewaan lain menggunakan cara ini adalah penentuan nilai property bisa dilakukan dengan tidak berurutan. Contohnya:

```go
var s4 = student{name: "wayne", grade: 2}
var s5 = student{grade: 2, name: "bruce"}
```

### Variabel Objek Pointer

Objek yang dibuat dari tipe struct bisa diambil nilai pointer-nya, dan bisa disimpan pada variabel objek yang bertipe struct pointer. Contoh penerapannya:

```go
var s1 = student{name: "wick", grade: 2}

var s2 *student = &s1
fmt.Println("student 1, name :", s1.name)
fmt.Println("student 4, name :", s2.name)

s2.name = "ethan"
fmt.Println("student 1, name :", s1.name)
fmt.Println("student 4, name :", s2.name)
```

`s2`  adalah variabel pointer hasil cetakan struct  `student`.  `s2`  menampung nilai referensi  `s1`, menjadikan setiap perubahan pada property variabel tersebut, akan juga berpengaruh pada variabel objek  `s1`.

Meskipun  `s2`  bukan variabel asli, property nya tetap bisa diakses seperti biasa. Inilah keistimewaan property dalam objek pointer, tanpa perlu di-dereferensi nilai asli property tetap bisa diakses. Pengisian nilai pada property tersebut juga bisa langsung menggunakan nilai asli, contohnya seperti  `s2.name = "ethan"`.

### Embedded Struct

**Embedded**  struct adalah mekanisme untuk menempelkan sebuah struct sebagai properti struct lain. Agar lebih mudah dipahami, mari kita bahas kode berikut.

```go
package main

import "fmt"

type person struct {
    name string
    age  int
}

type student struct {
    grade int
    person
}

func main() {
    var s1 = student{}
    s1.name = "wick"
    s1.age = 21
    s1.grade = 2

    fmt.Println("name  :", s1.name)
    fmt.Println("age   :", s1.age)
    fmt.Println("age   :", s1.person.age)
    fmt.Println("grade :", s1.grade)
}
```

Pada kode di atas, disiapkan struct  `person`  dengan properti yang tersedia adalah  `name`  dan  `age`. Disiapkan juga struct  `student`  dengan property  `grade`. Struct  `person`  di-embed ke dalam struct  `student`. Caranya cukup mudah, yaitu dengan menuliskan nama struct yang ingin di-embed ke dalam body  `struct`  target.

Embedded struct adalah  **mutable**, nilai property-nya nya bisa diubah.

Khusus untuk properti yang bukan properti asli (properti turunan dari struct lain), bisa diakses dengan cara mengakses struct  _parent_-nya terlebih dahulu, contohnya  `s1.person.age`. Nilai yang dikembalikan memiliki referensi yang sama dengan  `s1.age`.

### Embedded Struct Dengan Nama Property Yang Sama

Jika salah satu nama properti sebuah struct memiliki kesamaan dengan properti milik struct lain yang di-embed, maka pengaksesan property-nya harus dilakukan secara eksplisit atau jelas. Contoh bisa dilihat di kode berikut.

```go
package main

import "fmt"

type person struct {
    name string
    age  int
}

type student struct {
    person
    age   int
    grade int
}

func main() {
    var s1 = student{}
    s1.name = "wick"
    s1.age = 21        // age of student
    s1.person.age = 22 // age of person

    fmt.Println(s1.name)
    fmt.Println(s1.age)
    fmt.Println(s1.person.age)
}
```

Struct  `person`  di-embed ke dalam struct  `student`, dan kedua struct tersebut kebetulan salah satu nama property-nya ada yang sama, yaitu  `age`. Cara mengakses property  `age`  milik struct  `person`  lewat objek struct  `student`, adalah dengan menuliskan nama struct yang di-embed kemudian nama property-nya, contohnya:  `s1.person.age = 22`.

### Pengisian Nilai Sub-Struct

Pengisian nilai property sub-struct bisa dilakukan dengan langsung memasukkan variabel objek yang tercetak dari struct yang sama.

```go
var p1 = person{name: "wick", age: 21}
var s1 = student{person: p1, grade: 2}

fmt.Println("name  :", s1.name)
fmt.Println("age   :", s1.age)
fmt.Println("grade :", s1.grade)
```

Pada deklarasi  `s1`, property  `person`  diisi variabel objek  `p1`.

### Anonymous Struct

Anonymous struct adalah struct yang tidak dideklarasikan di awal sebagai tipe data baru, melainkan langsung ketika pembuatan objek. Teknik ini cukup efisien untuk pembuatan variabel objek yang struct-nya hanya dipakai sekali.

```go
package main

import "fmt"

type person struct {
    name string
    age  int
}

func main() {
    var s1 = struct {
        person
        grade int
    }{}
    s1.person = person{"wick", 21}
    s1.grade = 2

    fmt.Println("name  :", s1.person.name)
    fmt.Println("age   :", s1.person.age)
    fmt.Println("grade :", s1.grade)
}
```

Pada kode di atas, variabel  `s1`  langsung diisi objek anonymous struct yang memiliki property  `grade`, dan property  `person`  yang merupakan embedded struct.

Salah satu aturan yang perlu diingat dalam pembuatan anonymous struct adalah, deklarasi harus diikuti dengan inisialisasi. Bisa dilihat pada  `s1`  setelah deklarasi struktur struct, terdapat kurung kurawal untuk inisialisasi objek. Meskipun nilai tidak diisikan di awal, kurung kurawal tetap harus ditulis.

```go
// anonymous struct tanpa pengisian property
var s1 = struct {
    person
    grade int
}{}

// anonymous struct dengan pengisian property
var s2 = struct {
    person
    grade int
}{
    person: person{"wick", 21},
    grade:  2,
}
```

### Kombinasi Slice & Struct

Slice dan  `struct`  bisa dikombinasikan seperti pada slice dan  `map`, caranya penggunaannya-pun mirip, cukup tambahkan tanda  `[]`  sebelum tipe data pada saat deklarasi.

```go
type person struct {
    name string
    age  int
}

var allStudents = []person{
    {name: "Wick", age: 23},
    {name: "Ethan", age: 23},
    {name: "Bourne", age: 22},
}

for _, student := range allStudents {
    fmt.Println(student.name, "age is", student.age)
}
```

### Inisialisasi Slice Anonymous Struct

Anonymous struct bisa dijadikan sebagai tipe sebuah slice. Dan nilai awalnya juga bisa diinisialisasi langsung pada saat deklarasi. Berikut adalah contohnya:

```go
var allStudents = []struct {
    person
    grade int
}{
    {person: person{"wick", 21}, grade: 2},
    {person: person{"ethan", 22}, grade: 3},
    {person: person{"bond", 21}, grade: 3},
}

for _, student := range allStudents {
    fmt.Println(student)
}
```

### Deklarasi Anonymous Struct Menggunakan Keyword  **var**

Cara lain untuk deklarasi anonymous struct adalah dengan menggunakan keyword  `var`.

```go
var student struct {
    person
    grade int
}

student.person = person{"wick", 21}
student.grade = 2
```

Statement  `type student struct`  adalah contoh cara deklarasi struct. Maknanya akan berbeda ketika keyword  `type`  diganti  `var`, seperti pada contoh di atas  `var student struct`, yang artinya dicetak sebuah objek dari anonymous struct kemudian disimpan pada variabel bernama  `student`.

Deklarasi anonymous struct menggunakan metode ini juga bisa dilakukan beserta inisialisasi-nya.

```go
// hanya deklarasi
var student struct {
    grade int
}

// deklarasi sekaligus inisialisasi
var student = struct {
    grade int
} {
    12,
}
```

### Nested struct

Nested struct adalah anonymous struct yang di-embed ke sebuah struct. Deklarasinya langsung di dalam struct peng-embed. Contoh:

```go
type student struct {
    person struct {
        name string
        age  int
    }
    grade   int
    hobbies []string
}
```

Teknik ini biasa digunakan ketika decoding data  **json**  yang struktur datanya cukup kompleks dengan proses decode hanya sekali.

### Deklarasi Dan Inisialisasi Struct Secara Horizontal

Deklarasi struct bisa dituliskan secara horizontal, caranya bisa dilihat pada kode berikut:

```go
type person struct { name string; age int; hobbies []string }
```

Tanda semi-colon (`;`) digunakan sebagai pembatas deklarasi poperty yang dituliskan secara horizontal. Inisialisasi nilai juga bisa dituliskan dengan metode ini. Contohnya:

```go
var p1 = struct { name string; age int } { age: 22, name: "wick" }
var p2 = struct { name string; age int } { "ethan", 23 }
```

Bagi pengguna editor Sublime yang terinstal plugin GoSublime di dalamnya, cara ini tidak akan bisa dilakukan, karena setiap kali file di-save, kode program dirapikan. Jadi untuk mengetesnya bisa dengan menggunakan editor lain.

### Tag property dalam struct

Tag merupakan informasi opsional yang bisa ditambahkan pada masing-masing property struct.

```go
type person struct {
    name string `tag1`
    age  int    `tag2`
}
```

Tag biasa dimanfaatkan untuk keperluan encode/decode data json. Informasi tag juga bisa diakses lewat reflect. Nantinya akan ada pembahasan yang lebih detail mengenai pemanfaatan tag dalam struct, terutama ketika sudah masuk chapter JSON.

### Type Alias

Sebuah tipe data, seperti struct, bisa dibuatkan alias baru, caranya dengan  `type NamaAlias = TargetStruct`. Contoh:

```go
type Person struct {
    name string
    age  int
}
type People = Person

var p1 = Person{"wick", 21}
fmt.Println(p1)

var p2 = People{"wick", 21}
fmt.Println(p2)
```

Pada kode di atas, sebuah alias bernama  `People`  dibuat untuk struct  `Person`.

Casting dari objek (yang dicetak lewat struct tertentu) ke tipe yang merupakan alias dari struct pencetak, hasilnya selalu valid. Berlaku juga sebaliknya.

```go
people := People{"wick", 21}
fmt.Println(Person(people))

person := Person{"wick", 21}
fmt.Println(People(person))
```

Pembuatan struct baru juga bisa dilakukan lewat teknik type alias. Silakan perhatikan kode berikut.

```go
type People1 struct {
    name string
    age  int
}
type People2 = struct {
    name string
    age  int
}
```

Struct  `People1`  dideklarasikan. Struct alias  `People2`  juga dideklarasikan, struct ini merupakan alias dari anonymous struct. Penggunaan teknik type alias untuk anonymous struct menghasilkan output yang ekuivalen dengan pendeklarasian struct.

Perlu diketahui juga, dan di atas sudah sempat disinggung, bahwa teknik type alias ini tidak dirancang hanya untuk pembuatan alias pada tipe struct saja, semua jenis tipe data bisa dibuatkan alias. Di contoh berikut, dipersiapkan tipe  `Number`  yang merupakan alias dari tipe data  `int`.

```go
type Number = int
var num Number = 12
```

### Latihan
Buatlah sebuah singly linked list menggunakan Golang dan buat pula fungsi untuk :
1. menambahkan elemen di akhir linked list
2. fungsi untuk menghapus elemen di akhir linked list
3. fungsi untuk mencetak seluruh elemen dalam linked list

Singly linked list adalah sebuah struktur data seperti array yang terdiri atas node yang menunjuk node lainnya dan bersifat satu arah (sebuah node hanya menunjuk pada sebuah node setelahnya). Berikut merupakan ilustrasi singly linked list :


<p align="center">
  <img src="https://socs.binus.ac.id/files/2017/03/rini-1.jpg" width="40%" height="20%">
</p>


