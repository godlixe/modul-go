# Web Framework dan ORM Packages

## Daftar Isi

- [Perkenalan Framework](#perkenalan-framework)

- [Framework Web Golang](#framework-web-golang)

- [Kelebihan dan Kekurangan Gin](#kelebihan-dan-kekurangan-gin)

- [Implementasi Gin](#implementasi-gin)

- [Golang ORM Packages](#golang-orm-packages)

- [Kelebihan dan Kekurangan GORM](#kelebihan-dan-kekurangan-gorm)

- [Implementasi GORM](#implementasi-gorm)

- [Membuat Relasi Menggunakan GORM](#membuat-relasi-menggunakan-gorm)

- [Penggabungan Gin dan GORM](#penggabungan-gin-dan-gorm)

- [Penugasan](#penugasan)
  

## Perkenalan Framework

Noorples tau engga, apa itu framework? Mungkin pernah denger tapi gapaham?

![gabisa basa enggres](https://blue.kumparan.com/image/upload/fl_progressive,fl_lossy,c_fill,q_auto:best,w_640/v1611300897/hbismqisdggtfb6h1fer.jpg)

Nah, pada materi minggu ini kita bakal mempelajari apa itu framework, siapa itu framework, berapa itu framework, dan kenapa itu framework?

Jadi berdasarkan namanya sendiri, framework merupakan kerangka kerja. Sekian. 

Tapi mas, kerangka kerja itu apa? Dikutip dari Bing, kerangka kerja merupakan struktur yang ditetapkan di mana tugas dilakukan atau diselesaikan. Oke jawabannya gajelas, aku ulangin. Dikutip dari Google, kerangka kerja pengembangan perangkat lunak adalah alat yang dibuat untuk menyederhanakan kehidupan developer dengan menawarkan struktur dan pengaturan lingkungan untuk merampingkan proses development.

Dengan kehadiran framework, kita sebagai developer dapat dengan mudah membuat sebuah aplikasi tanpa memulai pembangunan dari 0 dikarenakan umumnya framework memiliki fungsionalitas spesifik yang bertujuan untuk memudahkan fitur tertentu atau bahkan memiliki fungsionalitas keseluruhan menjadi fondasi dari sebuah aplikasi. Framework secara general dapat dibagi menjadi beberapa tipe salah tiganya yakni Web Application Frameworks seperti Angular ~~dan Laravel,~~ DataScience Frameworks seperti Apache Spark dan TensorFlow, lalu Mobile Development Frameworks seperti Xamarin dan Flutter.

## Framework Web Golang

Seperti yang disinggung pada penjelasan tadi, terdapat framework web yang kegunaannya tentu saja buat bikin web. Framework web diperuntukkan untuk mempermudah pembuatan, pemeliharaan, dan pembaharuan website. Dengan adanya tools dan library yang mempersingkat pekerjaan webdev yang umum seperti routing URL menuju handler, berinteraksi dengan database, men-support session dan user authorization, formatting output, hingga meningkatkan keamanan website.

Di Golang sendiri terdapat beberapa framework web, 5 yang terbaik antara lain:

### Gin
![jin](https://upload.wikimedia.org/wikipedia/en/0/0c/The_Genie_Aladdin.png)

Dengan Gin kita dapat ~~meminta 3 permintaan~~ melakukan error management secara mudah, membuat sebuah *middleware*, grouping routes, serta melakukan validasi JSON. Mas middleware itu apa? Simpelnya middleware itu sebuah service yang digunakan dalam sebuah pemrosesan tertentu di tengah-tengah suatu alur aplikasi.

### Beego
![bigo](https://static-web.likeevideo.com/as/bigo-static/www.bigo.tv/img/logo_icon.png)

Framework ini bukan untuk live ya ges, melainkan framework ini fokus kepada enterprise application yang memiliki kode yang tebel, fitur yang buanyak, dan struktur yang modular. Selain itu Beego juga dapat membuat dokumentasi API secara otomatis melalui Swagger.

### Iris
![iris](https://thumb.intipseleb.com/media/frontend/thumbs3/2023/01/09/63bb9bcf1ef94-iris-wullur_663_372.jpeg)

Oke fokus ke materi. Untuk framework yang ini, bisa bantu kalian bagi yang baru belajar Golang tapi sebelumnya udah pernah belajar Express.js. Iris memiliki fleksibiltas terhadap library external, memiliki built-in logger untuk print dan logging server request, dan menyediakan support MVC untuk aplikasi yang besar.

### Echo
![logo beneran](https://img.stackshare.io/service/4996/9P0MlumU_400x400.jpg)

Dengan framework Echo, developer bisa membuat middleware sendiri ataupun menggunakan yang sudah ada, mampu mensupport HTTP/2 untuk performa yang lebih cepat, support response HTTP yang beragam, hingga support bermacam-macam templating engines.

### Fiber
![fiber](https://i.postimg.cc/rw0c0Dd4/pengertian-fiber-optik-onpost.jpg)

Dibangun dengan fokus utama minimalistik dan menyediakan teknologi yang simpel dan modular, Fiber mirip seperti Express.js. Framework ini memiliki fitur built-in rate limitter untuk mengurangi traffic menuju endpoint tertentu, dapat menghandle static file dengan mudah, serta men-support koneksi WebSocket bidirectional TCP yang mana akan kalian pelajari di Jarkom semester depan, semangat!

## Kelebihan dan Kekurangan Gin

Nah itu kan banyak ya pilihan framework web Golang yang bisa kita pakai, tapi dalam materi oprec ini, kita bakal menggunakan framework Gin. Kenapa?

| Plus | Minus |
|--|--|
| Performa ciamik | Dokumentasinya di bawah rata-rata |
| Jarang crash | Sintaksnya sedikit kurang jelas |
| Memiliki error management yang bagus | Engga sefleksibel itu dalam development |
| Ez pz validasi JSON |  |

Pada dasarnya Gin yang memiliki performa mantap merupakan highlight dari penggunaannya dibandingkan dengan framework lain. Dengan implementasi multi-goroutine schedule yang dimilki Gin, kita jadi terbantu dengan performa yang cepet tanpa kita perlu setting goroutine manual. Implementasi interface context.Context yang akan dipelajari nanti juga membantu mengontrol alur dan melakukan pass value di dalemnya. Alasan terakhir terkait middleware yang bisa digunakan dengan mudah.

## Implementasi Gin

![mari kita coba](https://assets.pikiran-rakyat.com/crop/0x0:0x0/x/photo/2021/12/19/2186472219.jpg)

Pertama-tama kalian bisa bikin project baru di folder baru dengan file main.go baru dan lakukan pembuatan modules baru seperti yang ada di modul lama (modul kemarin). Next buka terminal baru, dan kita akan men-download Gin dengan command berikut:

```sh
go get -u github.com/gin-gonic/gin
```

Kalau udah, kita bisa langsung pakai Gin di codingan kita dengan import sebagai berikut:

```go
import "github.com/gin-gonic/gin"
```

Oke next kita bakal coba Gin-nya dengan menuliskan fungsi main seperti berikut:

```go
func main() {
	server := gin.Default()
	server.GET("/ping", func(ctx *gin.Context) {
		ctx.JSON(200, gin.H{
			"message": "pong",
		})
	})
	server.Run(":8080")
}
```

Coba jalanin dan buka [http://localhost:8080/ping](http://localhost:8080/ping)

Selain dengan cara seperti itu, kita juga bisa menambahkan route baru dengan cara membuat fungsi terpisah seperti berikut:

```go
func  getRPL(ctx *gin.Context) {
	ctx.JSON(200, gin.H{
		"message": "jaya! jaya! jaya!",
	})
}
```

Lalu untuk penggunaannya pada fungsi main kita hanya perlu mengetik seperti berikut:

```go
server.GET("/rpl", getRPL)
```

##  Golang ORM Packages

Oke istirahat ngoding sejenak, sekarang kita bakal bahas ORM packages. Ini bukan organisasi yang minta merdeka ya temen-temen, melainkan ORM merupakan singkatan dari Object Relation Mapping. ORM digunakan sebagai sebuah metode berubah suatu tabel menjadi sebuah object yang nantinya dapat digunakan dalam codingan kita. Untuk gambaran alurnya dapat melihat ilustrasi berikut:

![gambaran orm](https://miro.medium.com/v2/resize:fit:828/format:webp/0*X4u4FSka7FxSct-_.png)

[Sudah kenal sama ORM?. Ketika kalian hendak mendalami backend… | by Deby Silvia Agnes | wripolinema | Medium](https://medium.com/wripolinema/sudah-kenal-sama-orm-34712e85c6fa)

Di Golang sendiri terdapat berbagai macam framework ORM yang dapat digunakan salah beberapanya yakni:

### GORM
![gorm](https://blog.logrocket.com/wp-content/uploads/2022/09/gorm.png)

GORM memiliki built-in database/sql package, memiliki fungsi auto migration, logging context, association, dan masih banyak lainnya. Menggunakan pendekatan code-first, pembuatan model dapat menggunakan struct untuk berinteraksi dengan database baik MySQL, SQLite, hingga PostgreSQL.

### SQLC
![sqlc](https://civenty.com/uploads/content_image/60c378a947a2a777822625.png)

SQLC merupakan SQL compiler ORM package yang membuat type-safe code dari SQL untuk berinteraksi dengan database SQL menggunakan tipe data Golang. Berlawanan dengan GORM, SQLC menggunakan pendekatan schema-first dimana setelah kita menentukan schema dan query SQL, kita dapat menjalankan command SQLC untuk menghasilkan type-safe code interface ke query.

### GORP
![gorp](https://blog.logrocket.com/wp-content/uploads/2022/09/gorp.jpeg)

Ini bukan typo, GORP dapat membuat mapping antara Go struct dan tabel SQL, transaction, forward engineering database schemas from structs, hooks, database queries, slice binding, testing, logging, and much- eh sorry lupa translate, dan masih banyak lainnya.

### Go-firestorm
![go-firestorm](https://upload.wikimedia.org/wikipedia/en/thumb/8/8e/Jefferson_%27Jax%27_Jackson_-_Firestorm_%28Franz_Drameh%29.jpg/220px-Jefferson_%27Jax%27_Jackson_-_Firestorm_%28Franz_Drameh%29.jpg)

Go-firestorm memiliki karakteristik cepat dan gampang digunakan. Package ini menggunakan pendekatan code-first, mensupport operasi CRUD, search, request yang concurrent, nested transaction, dan masih banyak lainnya.

### SQLBoiler
![sqlboiler](https://blog.logrocket.com/wp-content/uploads/2022/09/sqlboiler.png)

Merupakan ORM schema-first yang mengutamakan pada type safety dan performa. Package ini menyediakan fungsionalitas untuk pembuatan model yang utuh, transactions, model hooks, dan masih banyak lainnya.

## Kelebihan dan Kekurangan GORM

Pada oprec ini kita akan menggunakan GORM. Berikut informasi terkait keunggulan dan ketidakunggulannya.

| Pros | Cons |
|--|--|
| Pendekatan code-first | Penggunaan ORM secara garis besar dapat memperlambat aplikasi |
| Men-support MySQL, SQLite, PostgreSQL, dan masih banyak lainnya |  Penggunaannya pada query yang kompleks tidak mudah |
| Developer friendly |  |
| Banyak pengguna |  |

## Implementasi GORM

Welcome back to VSCode. Pertama kita perlu menginstall GORM dan driver database menggunakan command

```sh
go get -u gorm.io/gorm
go get -u gorm.io/driver/postgres
```

Selanjutnya kita bisa menggunakan GORM dengan mengimport GORM serta driver dari database yang digunakan, dalam kasus ini kita menggunakan postgres

```go
import (
	"gorm.io/gorm"
	"gorm.io/driver/postgres"
)
```

Oke markicob untuk program yang menggunakan GORM sebagai berikut:

```go
type Product struct {
	gorm.Model
	Nama string
	Harga uint
}
  
func main() {
	dsn := "host=localhost user=postgres password=root dbname=oprec port=5432 TimeZone=Asia/Jakarta"
	db, err := gorm.Open(postgres.Open(dsn), &gorm.Config{})
	if err != nil {
		panic("failed to connect database")
	}

	// Migrate the schema
	err = db.AutoMigrate(&Product{})
	if err != nil {
		panic("failed to migrate schema")
	}

	// Create
	db.Create(&Product{Nama: "Lontong", Harga: 1000})

	// Read
	var product Product

	db.First(&product, 1) // find product with integer primary key

	db.First(&product, "nama = ?", "Lontong") // find product with nama D42

	// Update - update product's harga to 200
	db.Model(&product).Update("Harga", 2000)

	// Update - update multiple fields
	db.Model(&product).Updates(Product{Harga: 4000, Nama: "Cilok"}) // non-zero fields
	db.Model(&product).Updates(map[string]interface{}{"Harga": 5000, "Nama": "Cireng"})

	// Delete - delete product
	db.Delete(&product, 1)

	dbSQL, err  := db.DB()
	if err !=  nil {
		panic("failed to get db")
	}
	
	dbSQL.Close()
}
```

## Membuat Relasi Menggunakan GORM
Relasi adalah hubungan antar entitas. Relasi yang dimaksud di sini adalah relasi seperti one to one, one to many, dsb. Oleh karena itu, relasi yang dibuat pada gorm juga memengaruhi relasi pada database (Database level). Referensi lengkap dari relasi terdapat di dokumentasi GORM https://gorm.io/docs/associations.html.

Kita akan mencoba membuat relasi one-to-many oleh sebuah user dan nomor telepon yang dimiliki user tersebut. Berikut merupakan gambaran relasi tersebut :

![Untitled Diagram drawio](https://user-images.githubusercontent.com/79066982/221390773-9acf70f5-21f0-4581-8961-464ae89d91f6.png)

Sebuah user dapat memiliki beberapa nomor telepon.

Untuk itu, kita menggunakan `hasMany` dengan penerapan sebagai berikut :

```go
// definisi entitas User
type User struct {
	ID           uint64        `gorm:"primaryKey" json:"id"`
	Name         string        `json:"name"`
	PhoneNumbers []PhoneNumber `json:"phone_numbers,omitempty"`
}

// definisi entitas PhoneNumber
type PhoneNumber struct {
	ID          uint64 `gorm:"primaryKey" json:"id"`
	CountryCode string `json:"country_code"`
	Number      string `json:"number"`
	UserID      uint64 `gorm:"foreignKey" json:"userID"`
	User        *User  `gorm:"constraint:OnUpdate:CASCADE,OnDelete:SET NULL;" json:"transaksi,omitempty"`
}
```

Perhatikan bahwa kita menggunakan tag gorm `` `gorm:"primaryKey"` ``. Tag digunakan untuk memberitahu gorm mengenai relasi dan properti sebuah entitas. Setelah mendefinisikan entitas tersebut, kita dapat melakukan automigrate pada GORM (`AutoMigrate(entity.User{}, entity.PhoneNumber{})`). Jangan lupa untuk membuat databasenya terlebih dahulu karena GORM tidak membuat database.

Setelah melakukan automigrate, berikut merupakan hasil relasi yang dibuat oleh GORM dilihat dari PostgreSQL :

![Screenshot from 2023-02-26 10-23-49](https://user-images.githubusercontent.com/79066982/221391063-a4542ac5-d5ff-46a4-8664-a6ec9720e585.png)
Perintah `\d dan \d+` digunakan untuk mendeskripsikan tabel ataupun database.

![Screenshot from 2023-02-26 10-24-41](https://user-images.githubusercontent.com/79066982/221391065-83b6e89d-6e7c-4b06-8bed-8f807039c8e4.png)


## Penggabungan Gin dan GORM
Sekarang kita akan mencoba menggabungkan Gin dan Gorm. Kita akan membuat project yang lebih terstruktur. Kita akan membuat folder untuk masing-masing fugnsionalitas. Clone kode berikut menggunakan perintah `git clone https://github.com/godlixe/gin-gorm-simple` di folder pilihanmu. Di dalam folder tersebut, terdapat kode yang akan kita pelajari lebih lanjut di pelatihan nanti.


## Penugasan
