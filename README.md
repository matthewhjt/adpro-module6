# Tutorial Module 6

```
Nama    : Matthew Hotmaraja Johan Turnip
NPM     : 2206081231
Kelas   : B
```

1. Commit 1 - handle_connection function

   ```
   fn handle_connection(mut stream: TcpStream) {
       let buf_reader = BufReader::new(&mut stream);
       let http_request: Vec<_> = buf_reader
           .lines()
           .map(|result| result.unwrap())
           .take_while(|line| !line.is_empty())
           .collect();

       println!("Request: {:#?}", http_request);
   }
   ```

   Dari apa yang saya baca dari [dokumentasi Rust](https://doc.rust-lang.org/book/ch20-01-single-threaded.html), `handle_connection` adalah fungsi yang digunakan untuk menangani koneksi ke server. Pada awalnya, fungsi tersebut membuat *instance* baru dari `BufReader` yang membungkus referensi *mutable* ke `stream`. Selanjutnya, *function* menggunakan variabel `http_request` untuk mengumpulkan baris-baris *request* yang dikirimkan oleh browser ke server.

    Selanjutnya, *method* `lines()` yang disediakan oleh `BufReader` mengembalikan iterator dari `Result<String, std::io::Error>`. Setelah itu, kita mengumpulkan baris-baris permintaan dari iterator tersebut. Browser menandai akhir dari permintaan HTTP dengan mengirimkan dua karakter baris baru (*new line*) berturut-turut. Jadi, kita mengambil baris-baris sampai kita mendapatkan baris yang kosong. Dengan demikian, `handle_connection` bertanggung jawab untuk membaca permintaan HTTP dari stream, dan mengelolanya.
