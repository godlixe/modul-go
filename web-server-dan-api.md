# Web Server dan API 🌐

## Daftar Isi

- [Preparation](#preparation)
- [Info](#info-ℹ️)
- [Web Server](#web-server)
- [HTTP](#http)
- [FYI](#fyi-😮)
- [Handling Multiple Requests](#handling-multiple-request)
- [Goroutines and Concurrency](#goroutines-and-concurrency)
- [API](#api)
- [Simple Go Web Server](#simple-go-web-server)
- [Try It Out](#try-it=out)
- [Connecting to Database](#connecting-to-database)
- [Inserting Values](#inserting-values)
- [Getting Values](#getting-values)
- [Integrating Both](#integrating-both)
- [Postman](#postman)


## Preparation

Noorples,pada modul sebelumnya kita telah mempelajari dasar-dasar pemrograman dalam bahasa Golang. Pada modul ini dan seterusnya, kita akan lebih berfokus pada pemrograman API. Oleh karena itu, kalian dapat mempersiapkan hal-hal berikut :

1. **Postman**
 Postman adalah tools yang digunakan untuk mempermudah pengembangan API. Kita dapat dengan mudah mengirimkan request HTTP ke API kita dengan postman. Kalian dapat mengunduh Postman dari <https://www.postman.com/downloads/>.
2. **PostgreSQL**
 PostgreSQL adalah salah satu database relasional yang digunakan untuk kepentingan penyimpanan data. Aplikasi backend yang kita buat akan dapat menyimpan data ke dalam PostgreSQL. Silakan unduh PostgreSQL dari <https://www.postgresql.org/download/>.

## Info ℹ️

Terdapat buku-buku terkait Golang yang dapat kalian akses melalui :
<https://drive.google.com/drive/folders/1vlNk40bWBgMEqztgr-jIRePxML2gmgg4?usp=share_link>

## Web Server

Web server (HTTP) adalah perangkat lunak yang memahami URL dan juga HTTP (protokol HTTP). Sebuah web server dapat diakses melalui suatu domain name dan dapat menyajikan konten kepada end user (client). Pada modul ini, akan lebih banyak dibahas mengenai HTTP Server.

## HTTP

HTTP adalah singkatan dari Hypertext Transfer Protocol. HTTP merupakan fondasi dari World Wide Web (WWW). HTTP adalah sebuah protokol (aturan, cara berkomunikasi) yang didesain untuk mentransfer informasi antara perangkat dalam jaringan. Alur tipikal dari protokol HTTP adalah sebuah client yang membuat permintaan pada sebuah server, yang mana server tersebut akan memberikan respons kembali. Terdapat beberapa versi HTTP, tetapi yang paling umum digunakan adalah HTTP 1.1. Aturan mengenai HTTP 1.1 terdapat pada [RFC 2616](https://www.rfc-editor.org/rfc/rfc2616#:~:text=RFC%202616%3A%20Hypertext%20Transfer%20Protocol%20%2D%2D%20HTTP%2F1.1).

**Berikut merupakan struktur permintaan (request) dan respons (response) HTTP 1.1 :**

<p align="center">
  <img src="https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages/httpmsgstructure2.png">
</p>

**Format request HTTP 1.1 :**

<p align="center">
  <img src="https://www.aisangam.com/blog/wp-content/uploads/2019/10/HTTPRequestMessageFormat-1024x700.png"  width="40%" height="20%">
</p>

## FYI 😮

RFC atau Request for Comments adalah dokumen formal yang mengandung spesifikasi dan catatan organisasi mengenai internet dan jaringan komputer. RFC dibuat oleh IETF (Internet Engineering Task Force), IETF adalah organisasi yang bertanggung jawab untuk internet dan standar-standarnya.

## Handling Multiple Requests

Saat mengakses sebuah laman web, atau mengirim request ke sebuah API, pernahkan kalian berpikir mengapa sebuah server dapat menghandle banyak orang dalam waktu bersamaan? Terdapat banyak cara yang telah dikemukakan untuk mengatasi masalah tersebut.

- Awalnya, digunakan metode forking. Forking artinya menduplikasikan program dalam bentuk process menggunakan panggilan sistem fork(). Namun, forking memerlukan banyak overhead (usaha yang diperlukan untuk membuatnya).
- Metode pre-forking kemudian dibuat dengan mempersiapkan duplikasi process tersebut agar mengurangi overhead dalam pembuatannya.
- Metode multi-thread kemudian dikembangkan, yang lebih efisien daripada process karena lebih ringan dan tidak memerlukan overhead sebanyak process dalam pembuatannya.
- Metode event-driven adalah metode yang digunakan sampai sekarang. Metode ini menggunakan thread juga, tetapi menggunakan panggilan secara asynchronous untuk setiap request yang sampai. Asynchronous artinya adalah pemanggilan fungsi pada program yang non-blocking (tidak menunggu hasil), dan dapat berjalan di background.

    Pengibaratannya adalah seperti memesan makanan di restoran cepat saji (McRPL). Pembeli akan datang memesan ke kasir, dan kasir akan menginputnya ke dalam daftar pesanan. Kasir kemudian menyuruh pembeli untuk duduk. Di dapur, para pekerja akan memilih pesanan dari daftar dan mengerjakannya dalam urutan tertentu (biasanya yang memesan lebih dulu akan diutamakan). Setelah selesai, makanan akan diantarkan oleh pelayan.

## Goroutines and Concurrency

Sejauh ini, aplikasi yang kalian buat hanya dapat menjalankan satu fungsionalitas dan keluar. Bagaimana bila kita ingin program kita menjalankan sebuah fungsionalitas lain sekaligus menjalankan fungsionalitas lainnya tanpa saling mengganggu? Bagaimana jika kita ingin mempercepat program kita dengan memproses suatu hal secara bersamaan dan tidak berurutan?

Pada bahasa Go, goroutine adalah jawabannya. Goroutine adalah lightweight thread (bukan thread OS, thread goroutine hanya berada pada level Go). Goroutine sangat ringan, satu buah goroutine memerlukan memori 2KB. Goroutine yang dibuat berjalan secara konkuren. Konkuren artinya adalah eksekusi yang hampir tampak seperti berjalan bersamaan, tetapi sebenarnya berjalan bergantian dengan sangat cepat. Lawan dari konkuren adalah paralel, paralel artinya berjalan bersamaan. Goroutine bersifat non-blocking atau asinkronus, yang berarti setelah menjalankan goroutine, program tetap berlangsung dan berlanjut.

Berikut merupakan program yang menunjukkan cara kerja goroutine. Program di bawah akan mencetak "halo" sebanyak lima kali dan mencetak apa kabar sebanyak lima kali.

```go
package main

import "fmt"
import "runtime"

func print(till int, message string) {
    for i := 0; i < till; i++ {
        fmt.Println((i + 1), message)
    }
}

func main() {
    runtime.GOMAXPROCS(2)

    go print(5, "halo")
    print(5, "apa kabar")

    var input string
    fmt.Scanln(&input)
}
```

## API

API adalah singkatan dari Application Programming Interface. API adalah antarmuka atau cara berkomunikasi dua atau lebih program. Standar yang digunakan untuk membuat API adalah API specification. Dalam konteks pemrograman web, API adalah antarmuka yang digunakan agar client dapat berkomunikasi dengan server. Terdapat banyak jenis API dalam konteks web, sesuai dengan protokol yang digunakan. Jenis yang paling umum digunakan adalah REST API.

REST adalah singkatan dari Representational State Transfer. REST adalah sebuah protokol yang bekerja dengan cara membuat rute/endpoint pada URL. Contohnya, saat kalian mengakses [https://www.its.ac.id/informatika/id/beranda/](https://www.its.ac.id/informatika/id/beranda/), server akan mengetahui bahwa kalian meminta semua yang harus ditampilkan pada halaman utama website Informatika ITS. Komunikasi menggunakna REST API bersifat satu arah, karena hanya client yang dapat mengirim permintaan dan kemudian direspons oleh server.

REST API pada umumnya menggunakan JSON (JavaScript Object Notation) untuk berkomunikas. Penggunaan JSON dipilih karena dapat lebih mudah diproses oleh browser yang umumnya menggunakan JavaScript.

## Simple Go Web Server

Pada modul ini, kita akan belajar menggunakan Go untuk membuat web server. Web server yang dibuat berupa web server sederhana yang akan menyajikan teks saat kita mengakses suatu URL di browser. Pembuatan web servernya akan menggunakan hanya library bawaan (stdlib) Go, yaitu `net/http`.

Pertama, kita akan membuat file bernama `main.go`. Lalu membuat

```go
package main

import (
	"fmt"
	"net/http"
)

func index(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintln(w, "Hello World!")
}

func main() {
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintln(w, "ini /")
	})

	http.HandleFunc("/index", index)

	fmt.Println("starting web server at http://localhost:8080/")
	http.ListenAndServe(":8080", nil)
}
```

Fungsi `http.ListenAndServe()` berfungsi untuk membuka sebuah web server pada port yang ditentukan di parameter pertama, menggunakan handler di parameter kedua. Karena kita memasukkan nil, kita menggunakan handler default golang. Fungsi `http.ListenAndServe()` menggunakan goroutine agar dapat berjalan di background.

Fungsi `http.HandleFunc()` berfungsi untuk menambahkan sebuah fungsi handler ke rute yang ditentukan pada parameter pertama, dan fungsi handler pada parameter kedua. Fungsi handler memiliki parameter `http.ResponseWriter` dan `*http.Request`. ResponseWriter berfungsi untuk menulis respons dan mengembalikannya ke client dan Request berfungsi untuk mendapatkan request dari client.

## Try It Out

Buat sebuah file bernama main.go, masukkan kode berikut dan jalankan programnya. Pergi ke browser, dan akses `http://localhost:8080/`.

```go
package main

import (
	"image"
	"image/color"
	"image/gif"
	"io"
	"math"
	"math/rand"
	"net/http"
)

var palette = []color.Color{color.White, color.Black}

const (
	whiteIndex = 0 // first color in palette
	blackIndex = 1 // next color in palette
)

func lissajousHandler(w http.ResponseWriter, r *http.Request) {
	lissajous(w)
}

func main() {
	http.HandleFunc("/", lissajousHandler)
	http.ListenAndServe(":8080", nil)
}
func lissajous(out io.Writer) {
	const (
		cycles = 5
		// number of complete x oscillator revolutions
		res  = 0.001 // angular resolution
		size = 100
		// image canvas covers [-size..+size]
		nframes = 64
		// number of animation frames
		delay = 8
	// delay between frames in 10ms units
	)
	freq := rand.Float64() * 3.0 // relative frequency of y oscillator
	anim := gif.GIF{LoopCount: nframes}
	phase := 0.0 // phase difference
	for i := 0; i < nframes; i++ {
		rect := image.Rect(0, 0, 2*size+1, 2*size+1)
		img := image.NewPaletted(rect, palette)
		for t := 0.0; t < cycles*2*math.Pi; t += res {
			x := math.Sin(t)
			y := math.Sin(t*freq + phase)
			img.SetColorIndex(size+int(x*size+0.5), size+int(y*size+0.5),
				blackIndex)
		}
		phase += 0.1
		anim.Delay = append(anim.Delay, delay)
		anim.Image = append(anim.Image, img)
	}
	gif.EncodeAll(out, &anim) // NOTE: ignoring encoding errors
}
```

## Connecting to Database

Setelah mengunduh dan menginstall PostgreSQL, pastikan database dapat berjalan, kalian dapat menggunakan DBMS seperti DBeaver/HeidiSQL untuk mencoba koneksi databasenya. Kalian juga bisa melakukan koneksi database melalui terminal dengan perintah "

```bash
psql -U postgres
```

Untuk berkomunikasi dengan database di Golang, kita akan menggunakan sebuah stdlib atau Standard Library bernama `database/sql` yang memiliki utilitas untuk berkomunikasi dengan database SQL. Namun, agar dapat berjalan, library tersebut harus menggunakan sebuah driver database. Terdapat banyak jenis driver yang dapat digunakan, dan yang kita gunakan kali ini adalah `jackc/pgx`. Karena menggunakan library luar, kita harus menggunakan go modules untuk mengatur modul-modul librarynya. Lakukan `go mod init <nama_modul>` untuk membuat project Go mendukung go modules.

Sebelum melanjutkan, kita harus membuat database baru dengan nama bebas, dalam contoh ini kita akan membuatnya dengan nama pgx :

```sql
CREATE DATABASE pgx;
```

Kemudian kalian dapat masuk ke dalam database yang sudah dibuat tersebut dengan perintah :

```bash
\c pgx
```

Untuk menginstall driver tersebut, kita akan menggunakan perintah :

```bash
go get github.com/jackc/pgx
```

Berikut merupakan kode untuk menyambungkan program Go dengan database PostgreSQL menggunakan driver pgx :

```Go
package main

import (
	"database/sql"
	"fmt"

	_ "github.com/jackc/pgx/v5/stdlib"
)

func Connect() (*sql.DB, error) {
	db, err := sql.Open("pgx", "postgres://root:root@localhost:5432/pgx")
	if err != nil {
		return nil, err
	}

	return db, nil
}

func main() {
	db, err := Connect()
	if err != nil {
		fmt.Println(err)
	}

	err = db.Ping()
	if err != nil {
		fmt.Println(err)
	}
}
```

String yang merupakan parameter pertama dari fungsi `sql.Open()` adalah driver yang digunakan. String pada parameter kedua adalah database URL, untuk PostgreSQL, format yang digunakan umumnya sebagai berikut `postgres://username:password@localhost:5432/database_name`. Jangan lupa untuk membuat database terlebih dahulu. Fungsi `db.Ping()` akan membuat koneksi ke database, apabila terjadi error, maka fungsi akan mengembalikan error.

## Inserting Values

Sebelum itu, mari kita buat sebuah tabel sederhana :

```SQL
CREATE TABLE users (
    ID serial PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
);
```

Kita akan mencoba memasukkan data menggunakan Go, berikut kode program untuk memasukkan data :

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/jackc/pgx/v5/stdlib"
)

type User struct {
    ID   uint64
    Name string
}

func Connect() (*sql.DB, error) {
    db, err := sql.Open("pgx", "postgres://postgres:root@localhost:5432/pgx")
    if err != nil {
        return nil, err
    }

    return db, nil
}

func InsertToDB(db *sql.DB, user User) (*User, error) {
    rows, err := db.Query("INSERT INTO users (name) VALUES ($1) RETURNING id, name", user.Name)
    if err != nil {
        return nil, err
    }

    // call rows.Next() to move pointer to first result set
    rows.Next()

    // result container object
    result := User{}

    // insert rows to result
    rows.Scan(&result.ID, &result.Name)
    return &result, nil
}

func main() {
    db, err := Connect()
    if err != nil {
        fmt.Println(err)
    }

    err = db.Ping()
    if err != nil {
        fmt.Println(err)
    }

    alex := User{
        Name: "alex",
    }

    res, err := InsertToDB(db, alex)
    if err != nil {
        fmt.Println(err)
    }

    fmt.Println(res)
}
```

## Getting Values

Sekarang, kita akan mengambil data dari database kita. Berikut merupakan contoh programnya :

```Go
package main

import (
	"database/sql"
	"fmt"

	_ "github.com/jackc/pgx/v5/stdlib"
)

type User struct {
	ID   uint64
	Name string
}

func Connect() (*sql.DB, error) {
	db, err := sql.Open("pgx", "postgres://postgres:root@localhost:5432/pgx")
	if err != nil {
		return nil, err
	}

	return db, nil
}

func InsertToDB(db *sql.DB, user User) (*User, error) {
	rows, err := db.Query("INSERT INTO users (name) VALUES ($1) RETURNING id, name", user.Name)
	if err != nil {
		return nil, err
	}

	// call rows.Next() to move pointer to first result set
	rows.Next()

	// result container object
	result := User{}

	// insert rows to result
	rows.Scan(&result.ID, &result.Name)
	return &result, nil
}

func GetAll(db *sql.DB) ([]User, error) {
	var result []User

	rows, err := db.Query("SELECT * FROM users")
	if err != nil {
		return nil, err
	}

	for rows.Next() {
		var user User
		rows.Scan(&user.ID, &user.Name)
		result = append(result, user)
	}

	return result, nil
}

func main() {
	db, err := Connect()
	if err != nil {
		fmt.Println(err)
	}

	err = db.Ping()
	if err != nil {
		fmt.Println(err)
	}

	res, err := GetAll(db)
	if err != nil {
		fmt.Println(err)
	}
	fmt.Println(res)
}
```

## Integrating Both

Kita akan membuat sebuah API yang dapat mengembalikan hasil JSON dari data yang kita dapat di dalam database. Contoh programnya adalah sebagai berikut :

```Go
package main

import (
	"database/sql"
	"encoding/json"
	"fmt"
	"net/http"

	_ "github.com/jackc/pgx/v5/stdlib"
)

type User struct {
	ID   uint64 `json:"id"`
	Name string `json:"user"`
}

func Connect() (*sql.DB, error) {
	db, err := sql.Open("pgx", "postgres://postgres:root@localhost:5432/pgx")
	if err != nil {
		return nil, err
	}

	return db, nil
}

func InsertToDB(db *sql.DB, user User) (*User, error) {
	rows, err := db.Query("INSERT INTO users (name) VALUES ($1) RETURNING id, name", user.Name)
	if err != nil {
		return nil, err
	}

	// call rows.Next() to move pointer to first result set
	rows.Next()

	// result container object
	result := User{}

	// insert rows to result
	rows.Scan(&result.ID, &result.Name)
	return &result, nil
}

func GetAll(db *sql.DB) ([]User, error) {
	var result []User

	rows, err := db.Query("SELECT * FROM users")
	if err != nil {
		return nil, err
	}

	for rows.Next() {
		var user User
		rows.Scan(&user.ID, &user.Name)
		result = append(result, user)
	}

	return result, nil
}

func main() {
	db, err := Connect()
	if err != nil {
		fmt.Println(err)
	}

	err = db.Ping()
	if err != nil {
		fmt.Println(err)
	}

	res, err := GetAll(db)
	if err != nil {
		fmt.Println(err)
	}

	// turning result into JSON
	jsonMap := map[string]interface{}{
		"data": res,
	}

	b, err := json.Marshal(jsonMap)
	if err != nil {
		fmt.Println(err)
	}

	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		// tell the client that the content type is json
		w.Header().Set("Content-Type", "application/json")
		w.WriteHeader(http.StatusOK)
		fmt.Fprintln(w, string(b))
	})

	fmt.Println("starting web server at http://localhost:8080/")
	http.ListenAndServe(":8080", nil)
}
```

Kita menggunakan library `encoding/json` untuk mengubah object Golang menjadi JSON. Fungsi yang digunakan untuk mengubah object menjadi JSON adalah `json.Marshal()` dan untuk mengubah dari JSON ke object adalah json.UnMarshal(). Berikut merupakan contoh penggunaan library `encoding/json` :

```Go
package main

import (
    "encoding/json"
    "fmt"
    "os"
)

type response1 struct {
    Page   int
    Fruits []string
}

type response2 struct {
    Page   int      `json:"page"`
    Fruits []string `json:"fruits"`
}

func main() {

    bolB, _ := json.Marshal(true)
    fmt.Println(string(bolB))

    intB, _ := json.Marshal(1)
    fmt.Println(string(intB))

    fltB, _ := json.Marshal(2.34)
    fmt.Println(string(fltB))

    strB, _ := json.Marshal("gopher")
    fmt.Println(string(strB))

    slcD := []string{"apple", "peach", "pear"}
    slcB, _ := json.Marshal(slcD)
    fmt.Println(string(slcB))

    mapD := map[string]int{"apple": 5, "lettuce": 7}
    mapB, _ := json.Marshal(mapD)
    fmt.Println(string(mapB))

    res1D := &response1{
        Page:   1,
        Fruits: []string{"apple", "peach", "pear"}}
    res1B, _ := json.Marshal(res1D)
    fmt.Println(string(res1B))

    res2D := &response2{
        Page:   1,
        Fruits: []string{"apple", "peach", "pear"}}
    res2B, _ := json.Marshal(res2D)
    fmt.Println(string(res2B))

    byt := []byte(`{"num":6.13,"strs":["a","b"]}`)

    var dat map[string]interface{}

    if err := json.Unmarshal(byt, &dat); err != nil {
        panic(err)
    }
    fmt.Println(dat)

    num := dat["num"].(float64)
    fmt.Println(num)

    strs := dat["strs"].([]interface{})
    str1 := strs[0].(string)
    fmt.Println(str1)

    str := `{"page": 1, "fruits": ["apple", "peach"]}`
    res := response2{}
    json.Unmarshal([]byte(str), &res)
    fmt.Println(res)
    fmt.Println(res.Fruits[0])

    enc := json.NewEncoder(os.Stdout)
    d := map[string]int{"apple": 5, "lettuce": 7}
    enc.Encode(d)
}
```

## Postman

Postman adalah sebuah tools untuk mengembangkan API. Dengan Postman, kita dapat membuat request, dan melihat respons dengan sebuah UI. Kita juga dapat membuat dokumentasi API menggunakan Postman. Berikut merupakan contoh penggunaannya :

![image](https://user-images.githubusercontent.com/79066982/219708067-6878fb8e-0863-4be0-bd93-863aec37b3c8.png)

## Penugasan
Buat sebuah API Todos sederhana yang mendukung operasi-operasi berikut :

1. Memasukkan data ke dalam database
2. Menghapus data dari database
3. Melihat data dari database

Buat juga dokumentasi postman untuk ketiga endpoint tersebut!
