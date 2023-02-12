# modul-golang 👨‍💻
## Daftar Isi
- Persiapan
- Pengenalan
- Tujuan
- Golang Dan Bahasa Lainnya
- Backend Engineering Overview
- Perusahaan yang Menggunakan Golang


## Persiapan
Sebelum berlanjut lebih jauh mengenai materi Golang, terdapat beberapa hal yang perlu disiapkan :
1. **Text Editor/Code Editor** <br/>
Contoh : Visual Studio Code **(recommended)**, GoLand, Vim, Vi, Nano, Atom, Sublime Text, Notepad++, atau Notepad.
2. **[Opsional] Terminal atau CLI (Command Line Interface)** <br/>
kalian bisa menggunakan windows terminal apabila menggunakan sistem operasi Windows.
3. **Golang** <br/>
Golang dapat diunduh melalui laman resmi Golang pada <https://go.dev/dl/>. Silakan mengunduh rilis yang tepat sesuai dengan sistem operasi yang kalian gunakan. Untuk petunjuk instalasi, kalian dapat melihat di sini :

    - https://www.youtube.com/watch?v=4zVJBltNwD0&t=132s (Ubuntu Linux 20.04)
    - https://www.youtube.com/watch?v=Rbzul5b5KI8 (Windows)
    - https://www.youtube.com/watch?v=3u6pZkNRCXg (Mac)

Setelah melakukan setup untuk Golang, pastikan bahwa Golang sudah terinstal dengan menjalankan perintah berikut pada terminal kalian :

```
go version
```

Output yang keluar, seharusnya berbentuk seperti berikut :
```
go version go1.19.2 linux/amd64
```

## Pengenalan

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/05/Go_Logo_Blue.svg/1200px-Go_Logo_Blue.svg.png" width="40%" height="20%">
</p>

Apa itu Golang? Golang atau Go adalah sebuah bahasa pemrograman yang open-source dan dibuat oleh Google. Beberapa pembuat bahasa Go yang terkenal adalah Rob Pike (salah satu pengembang Unix), dan Ken Thompson (salah satu pembuat format UTF-8). Go merupakan sebuah bahasa pemrograman yang **statically-typed**, artinya Go mengharuskan penggunaan tipe untuk tiap entitas di dalam bahasanya. Go juga merupakan bahasa yang dikompilasi, artinya kode yang ditulis dengan Go harus diubah ke dalam bytecode atau binary yang kemudian dijalankan. Go biasanya digunakan untuk membuat sistem backend dari sebuah aplikasi web, dan juga untuk membuat aplikasi CLI (Command Line Interface).

Go bukanlah sebuah bahasa pemrograman berorientasi objek seperti Java. Go bersifat prosedural seperti bahasa C/Perl. Oleh karena itu, tidak semua penerapan pemrograman berorientasi objek (OOP) tidak berlaku pada Go. Namun, beberapa penerapan konsep OOP dapat diterapkan dengan cara yang bisa saja berbeda dari biasanya.

## Tujuan
Telah banyak bahasa pemrograman yang penggunaannya serupa, beberapa di antaranya adalah PHP, Java, C, C++, Python. Namun, mengapa kita harus mempelajari Go?
1. Go mudah dipahami dan dipelajari
2. Go ringan memori dan juga cepat
3. Go memudahkan kita dalam menulis program yang berjalan secara konkuren
4. Go memiliki proses kompilasi yang cepat
5. Go memiliki dukungan komunitas yang bagus

## Golang Dan Bahasa Lainnya
Berikut merupakan perbedaan utama dari beberapa bahasa pemrograman yang umum dengan golang :
| PHP                           | NodeJS                                                       | Golang                                               |
|-------------------------------|--------------------------------------------------------------|------------------------------------------------------|
| Bahasa pemrograman OOP        | Bahasa pemrograman fungsional                                | Bahasa pemrograman prosedural                        |
| Biasa digunakan untuk website | Biasa digunakan untuk website dan sedikit pemrograman sistem | Biasa digunakan untuk website dan pemrograman sistem |
| Bahasa yang diinterpretasi    | Bahasa yang diinterpretasi                                   | Bahasa yang dikompilasi                              |
| Diciptakan tahun 1994         | Diciptakan tahun 2009                                        | Diciptakan tahun 2009                                |

## Backend Engineering Overview
Dalam rekayasa perangkat lunak (software engineering), terdapat banyak peran. Peran yang paling umum dan paling banyak diketahui dalam pemrograman perangkat lunak web adalah frontend, dan backend. Namun, untuk pelatihan ini, kita akan lebih banyak membahas mengenai backend engineering. Backend engineering adalah sesorang yang bertanggung jawab untuk mendesain, membangun, dan menjaga perangkat lunak yang berjalan di server (server side). Backend engineer tidak mendesain antarmuka atapun membangun antarmuka perangkat lunak. Perangkat lunak yang dibangun biasanya berkomunikasi dengan perangkat lunak client (frontend) dengan menggunakan API (Application Programming Interface).

## Perusahaan yang Menggunakan Golang
Berikut merupakan beberapa perusahaan yang menggunakan Golang untuk membangun sistem backendnya :

<table class="tg">
<thead>
  <tr>
    <th class="tg-0pky"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2f/Google_2015_logo.svg/1280px-Google_2015_logo.svg.png" width="147" height="50"></th>
    <th class="tg-0lax"><img src="https://upload.wikimedia.org/wikipedia/commons/5/58/Uber_logo_2018.svg" width="143" height="50"></th>
    <th class="tg-0lax"><img src="https://assets-global.website-files.com/6257adef93867e50d84d30e2/636e0a6a49cf127bf92de1e2_icon_clyde_blurple_RGB.png" width="65" height="50"></th>
    <th class="tg-0lax"><img src="https://www.docker.com/wp-content/uploads/2022/03/horizontal-logo-monochromatic-white.png" width="194" height="50"></th>
    <th class="tg-0lax"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4b/Cloudflare_Logo.svg/2560px-Cloudflare_Logo.svg.png" width="148" height="50"></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky"><img src="https://www.freepnglogos.com/uploads/logo-tokopedia-png/tokopedia-apa-itu-startup-pengertian-cara-memulai-dan-1.png" alt="Image" width="148" height="50"><br></td>
    <td class="tg-0lax"><img src="https://www.freepnglogos.com/uploads/shopee-logo/logo-shopee-png-images-download-shopee-1.png" alt="Image" width="148" height="50"></td>
    <td class="tg-0lax"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/99/Gojek_logo_2019.svg/2560px-Gojek_logo_2019.svg.png" width="212" height="50"></td>
    <td class="tg-0lax"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/71/Ruang_Guru_logo.svg/2560px-Ruang_Guru_logo.svg.png" width="89" height="50"></td>
    <td class="tg-0lax"><img src="https://download.logo.wine/logo/Riot_Games/Riot_Games-Logo.wine.png" width="89" height="50"></td>
  </tr>
</tbody>
</table>
