# modul-golang 👨‍💻
## Daftar Isi
- Persiapan
- Pengenalan
- Tujuan


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
Apa itu Golang? Golang atau Go adalah sebuah bahasa pemrograman yang open-source dan dibuat oleh Google. Beberapa pembuat bahasa Go yang terkenal adalah Rob Pike (salah satu pengembang Unix), dan Ken Thompson (salah satu pembuat format UTF-8). Go merupakan sebuah bahasa pemrograman yang **statically-typed**, artinya Go mengharuskan penggunaan tipe untuk tiap entitas di dalam bahasanya. Go juga merupakan bahasa yang dikompilasi, artinya kode yang ditulis dengan Go harus diubah ke dalam bytecode atau binary yang kemudian dijalankan. Go biasanya digunakan untuk membuat sistem backend dari sebuah aplikasi web, dan juga untuk membuat aplikasi CLI (Command Line Interface).

Go bukanlah sebuah bahasa pemrograman berorientasi objek seperti Java. Go bersifat prosedural seperti bahasa C/Perl. Oleh karena itu, tidak semua penerapan pemrograman berorientasi objek (OOP) tidak berlaku pada Go. Namun, beberapa penerapan konsep OOP dapat diterapkan dengan cara yang bisa saja berbeda dari biasanya.

## Tujuan
Telah banyak bahasa pemrograman yang penggunaannya serupa, beberapa di antaranya adalah PHP, Java, C, C++, Python. Namun, mengapa kita harus mempelajari Go?
1. Go mudah dipahami dan dipelajari
2. Go ringan memori dan juga cepat
3. Go memudahkan kita dalam menulis program yang berjalan secara konkuren
4. Go memiliki proses kompilasi yang cepat
5. Go memiliki dukungan komunitas yang bagus
