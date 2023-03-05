
## Extras
Modul ini berisi materi tambahan mengenai pengembangan backend dengan Golang.

## Daftar Isi
- [Arsitektur/Struktur Aplikasi](#arsitekturstruktur-aplikasi)
- [Autentikasi](#autentikasi)
- [Deployment](#deployment)

## Arsitektur/Struktur Aplikasi
Pada modul sebelumnya, kita telah membuat aplikasi Go yang lebih terstruktur. Struktur tersebut memisahkan beberapa implementasi sehingga kode yang ditulis lebih rapi. Sejatinya, tidak ada struktur proyek yang secara resmi dinyatakan oleh pihak Golang. Struktur yang digunakan oleh orang-orang biasanya mengikuti struktur aplikasi besar yang telah dibuat dengan Golang seperti [Docker Compose](https://github.com/docker/compose), [K8s](https://github.com/kubernetes/kubernetes), dan lain lain.

### Faktor-Faktor yang Memengaruhi Arsitektur Aplikasi
- Budaya organisasi
- Interaksi dengan stakeholder
- Batasan desain

### Pemilihan Arsitektur
Sebelum menentukan arsitektur yang tepat untuk project yang akan dibuat, kita dapat menganalisis kebutuhan pengguna dan pelanggan. Setelah mendapat kesimpulan, kita dapat memilih arsitektur yang tepat. Terdapat banyak arsitektur, di antaranya Clean Architecture, Onion Architecture, Hexagonal Architecture.

### Clean Architecture 
Clean Architecture adalah sebuah arsitektur sistem yang digagas oleh Robert C. Martin (Uncle Bob). Clean Architecture memisahkan elemen-elemen desain ke dalam kelompok sehingga memenuhi prinsip-prinsip perangkat lunak yang baik, seperti :

- Independen terhadap framework
Perangkat lunak yang dibuat tidak terikat terhadap keadaan library ataupun framework, sehingga membuat penggunaan framework lebih sebagai alat dibandingkan menggunakan framework untuk membangun seluruh aplikasi.
- Dapat dilakukan testing
Alur bisnis dapat diuji tanpa UI, database, web server, ataupun elemen external lainnya.
- Independen terhadap UI
UI dapat berubah sewaktu-waktu dan perangkat lunak (utamanya di alur bisnis) tidak perlu ikut diubah.
- Independen terhadap database
Database yang digunakan dapat ditukar (SQL menjadi MongoDB) dan alur bisnis tidak terikat ke database.
- Independen terhadap elemen eksternal apa pun
Alur bisnis seharusnya tidak tahu tentang dunia luar.

<p align="center">
  <img src="https://blog.cleancoder.com/uncle-bob/images/2012-08-13-the-clean-architecture/CleanArchitecture.jpg" width="80%" height="40%">
</p>

### Design Patterns and Design Approaches
Dalam membuat perangkat lunak, terkadang kita menemui permasalahan seperti bagaimana cara membuat suatu objek dapat dimodifikasi untuk kebutuhan tertentu. Masalah tersebut dapat diselesaikan dengan menggunakan design patterns. Design patterns adalah kumpulan solusi untuk permasalahan pada pembuatan perangkat lunak. Penjelasan dan contoh lebih lanjut dapat dilihat di [Sourcemaking](https://sourcemaking.com/design_patterns), [Refactoring Guru](https://refactoring.guru/).

Selain menyelesaikan masalah dengan design pattern, terdapat yang namanya design approaches atau pendekatan desain. Pendekatan desain lebih mengarah kepada cara mendesain perangkat lunak dalam level yang lebih tinggi. Salah satunya adalah Domain-Driven-Design (penyelesaian masalah aplikasi dalam mengelompokkan permasalahan sesuai dengan domain).

### Prinsip Pengembangan Perangkat Lunak
Terdapat beberapa prinsip pengembangan perangkat lunak yang sebaiknya diikuti antara lain :
- [SOLID](https://en.wikipedia.org/wiki/SOLID)
- [KISS](https://en.wikipedia.org/wiki/KISS_principle)

### Implementasi Clean Architecture
Kita akan mencoba mengimplementasikan clean architecture yang umum dipakai. Pada arsitektur ini, aplikasi dibagi menjadi beberapa bagian sesuai dengan struktur folder aplikasi.

<p align="center">
  <img src="https://user-images.githubusercontent.com/79066982/222702222-e51d47c3-de10-4797-845a-93aa1740d50b.png" width="30%" height="15%">
</p>

Penjelasan tiap-tiap folder :
- **config** <br/>
Folder ini digunakan untuk kode terkait konfigurasi, contohnya seperti konfigurasi database.
- **controller** <br/>
Folder ini digunakan untuk kode terkait controller, controller adalah bagian dari program yang berfungsi menerima request dan memberikan respons.
- **dto** <br/>
Folder ini digunakan untuk kode terkait dto, dto atau data transfer object adalah placeholder (wadah) suatu object lain yang digunakan untuk menampung data request dan respons.
- **entity** <br/>
Folder ini digunakan untuk kode terkait entitas/model pada program.
- **middleware** <br/>
Folder ini digunakan untuk kode terkait middleware. Middleware adalah perangkat lunak yang menengahi suatu operasi. 
- **repository** <br/>
Folder ini digunakan untuk kode terkait repository. Repository adalah lapisan yang berhubungan langsung dengan database.
- **routes** <br/>
Folder ini digunakan untuk kode terkait routing.
- **service** <br/>
Folder ini digunakan untuk kode terkait service. Service adalah lapisan yang berhubungan dengan logika/alur bisnis aplikasi.
- **utils** <br/>
Folder ini digunakan untuk kode terkait utilitas lainnya, contohnya seperti kode untuk perhitungan yang akan digunakan di banyak package lainnya.

Alur aplikasi kita akan seperti ini :

<p align="center">
  <img src="https://user-images.githubusercontent.com/79066982/222706937-6cbb15e9-3dd3-413b-b9a1-f8bbdfadf96d.png" width="80%" height="40%">
</p>

Dapat dilihat bahwa tiap lapisan menimbulkan keterkaitan (dependensi) pada lapisan lainnya di bawahnya. Hal ini dapat dilakukan dengan [dependency injection](https://en.wikipedia.org/wiki/Dependency_injection). Contoh dependency injection di golang adalah sebagai berikut :

```go
type userService struct {
	userRepo repository.UserRepository
}

func NewUserService(ur repository.UserRepository) UserService {
	return &userService{
		userRepo: ur,
	}
}
```

Logikanya adalah, karena `userService` memerlukan `userRepository`, maka saat membuat `userService`, kita akan memasukkan `userRepository` sebagai parameternya. `userRepository` juga dibuat sebagai entitas di dalam `userService`.

## Autentikasi
Autentikasi adalah pemastian bahwa sesorang adalah orang tersebut yang dapat dilakukan dengan melakukan login. Autentikasi berbeda dengan autorisasi, autorisasi adalah pemastian bahwa seseorang dapat mengakses/memiliki akses terhadap suatu entitasi. Terdapat banyak jenis autentikasi yang dapat diterapkan pada perangkat lunak antara lain :
- **Basic Authentication** <br/>
Basic authentication adalah metode autentikasi paling sederhana. Client akan mengirimkan username dan password tanpa dienkripsi kepada server dan server akan memastikan kebenaran kredensial tersebut. Username dan password akan disimpan di header dan diperlukan pada tiap request ke server.
- **Digest Authentication** <br/>
Digest authentication serupa dengan basic tetapi dienkripsi agar data lebih aman.
- **Session Based Authentication** <br/>
Session based authentication adalah autentikasi yang menyimpan state user di server, setelah user melakukan login, server akan memeriksa kredensial dan menghasilkan sebuah session. Session tersebut akan disimpan di dalam database dan juga browser (dalam bentuk sessionID di cookie). Metode ini lebih aman karena hanya mengirimkan id dari session akan tetapi setiap user memerlukan autorisasi/autentikasi, server harus memeriksa session yang berkaitan di dalam database.
- **Token Based Authentication** <br/>
Token based authentication menggunakan token. Salah satu jenis token yang umum digunakan adalah JSON Web Token (JWT). JWT menyimpan data header, payload, dan signature di dalamnya untuk memastikan kredensial dari user. Data pada jwt diencode menggunakan base64.
- **One Time Password** <br/>
One time password (OTP) adalah metode yang cukup umum digunakan. OTP merupakan kode yang dibuat secara acak dan biasanya memiliki waktu kedaluwarsa (Time Based OTP). OTP biasanya digunakan pada sistem yang bersifat sensitif. 
- **OAuth dan OpenID** <br/>
OAuth adalah metode yang memperbolehkan user login menggunakan single sign-on (SSO) baik dari media sosial ataupun pihak ketiga lainnya.

### Implementasi Autentikasi
Kita akan menggunakan Token Based Authentication menggunakan token JWT. Kita akan menggunakan library https://github.com/golang-jwt. Kode autentikasi akan dijadikan sebagai middleware yang menengahi antara router dan controller. Karena kita menggunakan framework Gin, maka return value dari fungsi middleware kita akan bertipe `gin.HandlerFunc` yang berupa sebuah fungsi yang menerima `gin.Context`. Token akan dibuat setiap user melakukan login. Token biasanya disimpan di dalam browser dan memiliki string "Bearer " di depannya karena berupa bearer token. Sehingga, saat menerima token, token tersebut berbentuk :

```
Bearer <token>
```

Oleh karena itu, kita harus memastikan bahwa string token sesuai dengan ketentuan.

Berikut merupakan implementasi middleware autentikasi JWT :

```go

func Authenticate(jwtService service.JWTService, role string) gin.HandlerFunc {
	return func(c *gin.Context) {
		authHeader := c.GetHeader("Authorization")
		if authHeader == "" {
			response := utils.BuildErrorResponse("No token found", http.StatusUnauthorized)
			c.AbortWithStatusJSON(http.StatusUnauthorized, response)
			return
		}
		if !strings.Contains(authHeader, "Bearer ") {
			response := utils.BuildErrorResponse("No token found", http.StatusUnauthorized)
			c.AbortWithStatusJSON(http.StatusUnauthorized, response)
			return
		}
		authHeader = strings.Replace(authHeader, "Bearer ", "", -1)
		token, err := jwtService.ValidateToken(authHeader)
		if err != nil {
			response := utils.BuildErrorResponse("Invalid token", http.StatusUnauthorized)
			c.AbortWithStatusJSON(http.StatusUnauthorized, response)
			return
		}

		if !token.Valid {
			response := utils.BuildErrorResponse("Invalid token", http.StatusUnauthorized)
			c.AbortWithStatusJSON(http.StatusForbidden, response)
			return
		}

		teamRole, err := jwtService.GetRoleByToken(string(authHeader))
		fmt.Println("ROLE", teamRole)
		if err != nil || (teamRole != "admin" && teamRole != role) {
			response := utils.BuildErrorResponse("Failed to process request", http.StatusUnauthorized)
			c.AbortWithStatusJSON(http.StatusForbidden, response)
			return
		}

		// get userID from token
		teamID, err := jwtService.GetTeamIDByToken(authHeader)
		if err != nil {
			response := utils.BuildErrorResponse("Failed to process request", http.StatusUnauthorized)
			c.AbortWithStatusJSON(http.StatusUnauthorized, response)
			return
		}
		fmt.Println("ROLE", teamRole)
		c.Set("teamID", teamID)
		c.Next()
	}
}
```

Berikut merupakan implementasi service autentikasi JWT :

```go
type JWTService interface {
	GenerateToken(teamID uint64, role string) string
	ValidateToken(token string) (*jwt.Token, error)
	GetTeamIDByToken(token string) (uint64, error)
	GetRoleByToken(token string) (string, error)
}

type jwtCustomClaim struct {
	TeamID uint64 `json:"team_id"`
	Role   string `json:"role"`
	jwt.RegisteredClaims
}

type jwtService struct {
	secretKey string
	issuer    string
}

func NewJWTService() JWTService {
	return &jwtService{
		secretKey: getSecretKey(),
		issuer:    "admin",
	}
}

func getSecretKey() string {
	secretKey := os.Getenv("JWT_SECRET")
	if secretKey == "" {
		secretKey = "jwt_secret_key"
	}
	return secretKey
}

func (j *jwtService) GenerateToken(teamID uint64, role string) string {
	claims := &jwtCustomClaim{
		teamID,
		role,
		jwt.RegisteredClaims{
			ExpiresAt: jwt.NewNumericDate(time.Now().Add(time.Minute * 120)),
			Issuer:    j.issuer,
			IssuedAt:  jwt.NewNumericDate(time.Now()),
		},
	}
	token := jwt.NewWithClaims(jwt.SigningMethodHS256, claims)
	t, err := token.SignedString([]byte(j.secretKey))
	if err != nil {
		log.Println(err)
	}
	return t
}

func (j *jwtService) ValidateToken(token string) (*jwt.Token, error) {
	return jwt.Parse(token, func(t_ *jwt.Token) (any, error) {
		if _, ok := t_.Method.(*jwt.SigningMethodHMAC); !ok {
			return nil, fmt.Errorf("unexpected signing method %v", t_.Header["alg"])
		}
		return []byte(j.secretKey), nil
	})
}

func (j *jwtService) GetTeamIDByToken(token string) (uint64, error) {
	t_Token, err := j.ValidateToken(token)
	if err != nil {
		return 0, err
	}
	claims := t_Token.Claims.(jwt.MapClaims)
	id := fmt.Sprintf("%v", claims["team_id"])
	teamID, _ := strconv.ParseUint(id, 10, 64)
	return teamID, nil
}

func (j *jwtService) GetRoleByToken(token string) (string, error) {
	t_Token, err := j.ValidateToken(token)
	if err != nil {
		return "", err
	}
	claims := t_Token.Claims.(jwt.MapClaims)
	role := fmt.Sprintf("%v", claims["role"])
	return role, nil
}
```

## Deployment
Terdapat beberapa layanan penyedia deployment gratis, salah satunya [railway.app](https://railway.app/). Sekarang kita akan belajar cara menggunakannya.

### Penggunaan Railway
Sebelum menggunakan Railway, kita harus membuat repo pada GitHub kita untuk 1 API-nya.
1. Buatlah akun Railway dengan menggunakan akun GitHub.
2. Lakukan verifikasi dengan menyetujui Terms and Condition Railway.
3. Pertama kita akan membuat project untuk database kita. Pilihlah Provision PostgreSQL.
4. Perhatikan cara connect DB nya melalui halaman Connect ketika klik Postgres.
5. Selanjutnya kita akan membuat project untuk API kita.
6. Create a New Project dengan memilih Deploy from GitHub repo.
7. Pilih repo API yang ingin di deploy.
8. Install & Authorize.
9. Pada web Railway pilih repo yang sudah tadi kalian beri akses.
10. Add Variables.
11. Masukkan kredensial database pada Variables.
12. Pergi ke Settings, lalu scroll hingga Domains, klik Custom Domain.
13. Apabila sudah mendapatkan domain, kalian bisa cek status pada halaman  deployment.
14. Kalian bisa cek melakukan request ke domain tersebut.
15. Selesai!
