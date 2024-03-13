# Alin Viola Pramudita - 220302028

## Selamat datang di CodeIgniter4
CodeIgniter merupakan sebuah kerangka kerja lunak pengembangan aplikasi web (framework) yang penulisannya menggunakan bahasa pemograman PHP. Tujuannya adalah untuk mengembangkan proyek jauh lebih cepat dan efisien dengan menyediakan sekumpulan library, serta antarmuka sederhana dan struktur yang logis untuk mengaksesnya. CodeIgniter memungkinkan Anda fokus secara kreatif pada proyek Anda dengan meminimalkan jumlah kode yang dibutuhkan untuk tugas tertentu.
## Persyaratan Server
- PHP dan Ekstensions yang Diperlukan
- Extensions PHP Opsional
- Basis Data yang Didukung
### PHP dan Extensions yang diperlukan
- intl
- mbstring
- json
### Extensions PHP Opsional
1. Ekstensi PHP berikut harus diaktifkan di server Anda:
   - mysqlnd ekstensi MySQL Native Driver yang menyediakan koneksi ke server MySQL. Ini adalah bagian dari paket PHP dan biasanya sudah terpasang secara default.
   - curl adalah ekstensi PHP yang memungkinkan Anda melakukan permintaan HTTP dan mengambil konten dari URL. Ini digunakan untuk mengirim permintaan ke server dan menerima respon.
   - imagick ekstensi PHP yang menyediakan antarmuka untuk ImageMagick, perangkat lunak pemrosesan gambar yang kuat. Dengan imagick, Anda dapat melakukan berbagai operasi pemrosesan gambar seperti memanipulasi, mengubah ukuran, dan mengubah format gambar.
   - gd adalah ekstensi PHP yang memungkinkan Anda untuk membuat, memanipulasi, dan menggambar gambar menggunakan fungsi-fungsi GD Library. Dengan gd, Anda dapat membuat grafik, mengubah ukuran gambar, dan melakukan operasi lainnya pada gambar.
   - simplexml adalah ekstensi PHP yang menyediakan antarmuka untuk memanipulasi dan membaca XML. Dengan simplexml, Anda dapat dengan mudah membaca dan menulis data XML menggunakan sintaks yang sederhana.
2. Ekstensi PHP berikut diperlukan saat Anda menggunakan server Cache:
   - memcache adalah ekstensi PHP yang digunakan untuk menghubungkan ke server memcached dan mengelola cache menggunakan objek Memcache. Dengan memcache, Anda dapat menyimpan data dalam memori untuk mengurangi beban pada basis data dan meningkatkan kinerja aplikasi.
   - memcached adalah ekstensi PHP yang menyediakan antarmuka untuk menghubungkan ke server memcached menggunakan objek Memcached. Dengan memcached, Anda dapat mengelola cache dalam aplikasi Anda dan meningkatkan kinerja dengan menyimpan data dalam memori.
   - redis adalah ekstensi PHP yang memungkinkan Anda berinteraksi dengan server Redis, yang merupakan sistem penyimpanan data berkinerja tinggi. Dengan redis, Anda dapat menyimpan dan mengambil data dari cache dalam aplikasi Anda.
### Basis Data yang Didukung
Basis data diperlukan untuk sebagian besar pemrograman aplikasi web. Basis data yang didukung saat ini adalah:
- MySQL melalui MySQLidriver (hanya versi 5.1 ke atas)
- PostgreSQL melalui Postgredriver (hanya versi 7.4 dan lebih tinggi)
- SQLite3 melalui SQLite3driver
- Microsoft SQL Server melalui SQLSRVdriver (hanya versi 2005 dan lebih tinggi)
- Oracle Database melalui OCI8driver (hanya versi 12.1 dan lebih tinggi)
## Installation
### Instalasi Komposer
1. Ketikan perintah berikut pada Terminal. Sebelumnya anda dapat mengatur penempatan file yang akan di install.
   ```shell
   composer create-project codeigniter4/appstarter project-root
   ```
2. Upgrading
   ```shell
   composer update
   ```
3. Update untuk Versi Terbaru
   ```shell
   php builds development
   ```
4. Kembalikan ke Rilis Stabil
   ```shell
   php builds release
   ```
#### Struktur
- aplikasi, publik, tes, dapat ditulis
- vendor/codeigniter4/framework/system
### Instalasi Manual
1. Unduh [versi terbaru] (https://github.com/codeigniter4/framework/archive/v4.0.4.zip)
2. Setelah itu Ekstrak folder zip yang sudah terinstall
#### Struktur
- app, public, tests, writable, system
## Menjalankan Aplikasi 
### Server Pengembangan Lokal
```shell
php spark serve
```
Server pengembangan lokal dapat dikustomisasi dengan tiga opsi baris perintah:
- Anda dapat menggunakan --hostopsi CLI untuk menentukan host berbeda untuk menjalankan aplikasi di:
  ```shell
  php spark serve --host example.dev
  ```
- Secara default, server berjalan pada port 8080 tetapi Anda mungkin menjalankan lebih dari satu situs, atau sudah memiliki aplikasi lain yang menggunakan port tersebut. Anda dapat menggunakan --portopsi CLI untuk menentukan opsi lain:
  ```shell
  php spark serve --port 8081
  ```
- Anda juga dapat menentukan versi PHP tertentu yang akan digunakan, dengan --phpopsi CLI, dengan nilainya disetel ke jalur eksekusi PHP yang ingin Anda gunakan:
  ```shell
  php spark serve --php /usr/bin/php7.6.5.4
  ```
## Membangun Aplikasi Sederhana
### Static Pages
#### Menetapkan Aturan Perutean
Siapkan aturan routing. Buka file rute yang terletak di app/Config/Routes.php .
```shell
<?php

use CodeIgniter\Router\RouteCollection;

/**
 * @var RouteCollection $routes
 */
$routes->get('/', 'Home::index');
```
Arahan ini mengatakan bahwa setiap permintaan masuk tanpa konten apa pun yang ditentukan harus ditangani oleh index() method di dalam Homepengontrol.

Tambahkan baris berikut, setelah arahan rute untuk '/'.
```shell
use App\Controllers\Pages;

$routes->get('pages', [Pages::class, 'index']);
$routes->get('(:segment)', [Pages::class, 'view']);
```
Aturan kedua dalam $routesobjek mencocokkan permintaan GET dengan jalur URI /pages , dan dipetakan ke index()metode kelas Pages.Aturan ketiga dalam $routesobjek mencocokkan permintaan GET ke segmen URI menggunakan placeholder (:segment), dan meneruskan parameter ke view()metode kelas Pages.
#### Buat Pengontrol Halaman 
Buat file di app/Controllers/Pages.php dengan kode berikut.
```shell
<?php

namespace App\Controllers;

class Pages extends BaseController
{
    public function index()
    {
        return view('welcome_message');
    }

    public function view($page = 'home')
    {
        // ...
    }
}
```
#### Buat Tampilan
Buat header di app/Views/templates/header.php dan tambahkan kode berikut:
```shell
<!doctype html>
<html>
<head>
    <title>CodeIgniter Tutorial</title>
</head>
<body>

    <h1><?= esc($title) ?></h1>
```
Header berisi kode HTML dasar yang ingin Anda tampilkan sebelum memuat tampilan utama, bersama dengan judul. Ini juga akan menampilkan $titlevariabel, yang akan kita definisikan nanti di pengontrol. Selanjutnya, buat footer di app/Views/templates/footer.php yang menyertakan kode berikut:
```shell
  <em>&copy; 2022</em>
</body>
</html>
```
#### Menambahkan Logika Ke Controller
##### Buat home.php dan about.php
Sebelumnya Anda menyiapkan pengontrol dengan suatu view() method. Method ini menerima satu parameter, yaitu nama halaman yang akan dimuat. Body halaman statis akan ditempatkan di direktori app/Views/pages .

Di direktori itu, buat dua file bernama home.php dan about.php . Di dalam file tersebut, ketikkan beberapa teks apa pun yang Anda suka dan simpan. Jika Anda ingin tampil tidak orisinal, cobalah “Hello World!”.

Buat file Views/pages/home.php .
```shell
Hello World!
```
#### Halaman Lengkap::view() Method
Kembali ke halaman Controller/Pages.php , lengkapi isi pada bagian method view()
```shell
<?php

namespace App\Controllers;

use CodeIgniter\Exceptions\PageNotFoundException; // Add this line

class Pages extends BaseController
{
    // ...

    public function view($page = 'home')
    {
        if (! is_file(APPPATH . 'Views/pages/' . $page . '.php')) {
            // Whoops, we don't have a page for that!
            throw new PageNotFoundException($page);
        }

        $data['title'] = ucfirst($page); // Capitalize the first letter

        return view('templates/header', $data)
            . view('pages/' . $page)
            . view('templates/footer');
    }
}
```
#### Menjalankan Aplikasi
Dari baris perintah, di root proyek Anda:
```shell
php spark serve
```
Server web dapat diakses pada port 8080. Jika Anda mengatur field lokasi di browser Anda ke localhost:8080 , Anda akan melihat halaman selamat datang CodeIgniter. Selanjutnya kunjungi localhost:8080/home 
### News Section
#### Buat Database untuk Digunakan
Buat database ci4tutorial pada MySQL dengan nama table news.
```shell
CREATE TABLE news (
    id INT UNSIGNED NOT NULL AUTO_INCREMENT,
    title VARCHAR(128) NOT NULL,
    slug VARCHAR(128) NOT NULL,
    body TEXT NOT NULL,
    PRIMARY KEY (id),
    UNIQUE slug (slug)
);
```
Masukkan data berikut pada table news menggunakan INSERT.
```shell
INSERT INTO news VALUES
(1,'Elvis sighted','elvis-sighted','Elvis was sighted at the Podunk internet cafe. It looked like he was writing a CodeIgniter app.'),
(2,'Say it isn\'t so!','say-it-isnt-so','Scientists conclude that some programmers have a sense of humor.'),
(3,'Caffeination, Yes!','caffeination-yes','World\'s largest coffee shop open onsite nested coffee shop for staff only.');
```
#### Hubungkan ke Basis Data 
Buka file konfigurasi lokal .env yang anda buat saat menginstall CodeIgniter. Pastikan Anda telah mengkonfigurasi database dengan benar.
```shell
database.default.hostname = localhost
database.default.database = ci4tutorial
database.default.username = root
database.default.password = root
database.default.DBDriver = MySQLi
```
#### Menyiapkan Model 
##### Buat Model News
Buka direktori app/Models dan buat file baru bernama NewsModel.php dan tambahkan kode berikut.
```shell
<?php

namespace App\Models;

use CodeIgniter\Model;

class NewsModel extends Model
{
    protected $table = 'news';
}
```
##### Tambahkan Metode NewsModel::getNews()
Tambahkan kode berikut ke model Anda.
```shell
  public function getNews($slug = false)
    {
        if ($slug === false) {
            return $this->findAll();
        }

        return $this->where(['slug' => $slug])->first();
    }
```
#### Tampilkan News
##### Menambahkan Aturan Perutean
Ubah file app/Config/Routes.php Anda , sehingga terlihat seperti berikut:
```shell
<?php

// ...

use App\Controllers\News; // Add this line
use App\Controllers\Pages;

$routes->get('news', [News::class, 'index']);           // Add this line
$routes->get('news/(:segment)', [News::class, 'show']); // Add this line

$routes->get('pages', [Pages::class, 'index']);
$routes->get('(:segment)', [Pages::class, 'view']);
```
#### Buat Pengontrol News
Buat pengontrol baru di app/Controllers/News.php .
```shell
<?php

namespace App\Controllers;

use App\Models\NewsModel;

class News extends BaseController
{
    public function index()
    {
        $model = model(NewsModel::class);

        $data['news'] = $model->getNews();
    }

    public function show($slug = null)
    {
        $model = model(NewsModel::class);

        $data['news'] = $model->getNews($slug);
    }
}
```
##### Lengkap News::index() Metode
Ubah index()metodenya menjadi seperti ini:
```shell
<?php

namespace App\Controllers;

use App\Models\NewsModel;

class News extends BaseController
{
    public function index()
    {
        $model = model(NewsModel::class);

        $data = [
            'news'  => $model->getNews(),
            'title' => 'News archive',
        ];

        return view('templates/header', $data)
            . view('news/index')
            . view('templates/footer');
    }

    // ...
}
```
##### Buat news/index pada File Views
Buat app/Views/news/index.php dan tambahkan potongan kode berikutnya.
```shell
<h2><?= esc($title) ?></h2>

<?php if (! empty($news) && is_array($news)): ?>

    <?php foreach ($news as $news_item): ?>

        <h3><?= esc($news_item['title']) ?></h3>

        <div class="main">
            <?= esc($news_item['body']) ?>
        </div>
        <p><a href="/news/<?= esc($news_item['slug'], 'url') ?>">View article</a></p>

    <?php endforeach ?>

<?php else: ?>

    <h3>No News</h3>

    <p>Unable to find any news for you.</p>

<?php endif ?>
```
##### Lengkapi News::show() Method
Kembali ke Newspengontrol dan perbarui show()metode dengan yang berikut:
```shell
<?php

namespace App\Controllers;

use App\Models\NewsModel;
use CodeIgniter\Exceptions\PageNotFoundException;

class News extends BaseController
{
    // ...

    public function show($slug = null)
    {
        $model = model(NewsModel::class);

        $data['news'] = $model->getNews($slug);

        if (empty($data['news'])) {
            throw new PageNotFoundException('Cannot find the news item: ' . $slug);
        }

        $data['title'] = $data['news']['title'];

        return view('templates/header', $data)
            . view('news/view')
            . view('templates/footer');
    }
}
```
##### Buat news/view pada File Views
Membuat tampilan terkait di app/Views/news/view.php . Letakkan kode berikut di file ini.
```shell
<h2><?= esc($news['title']) ?></h2>
<p><?= esc($news['body']) ?></p>
```
Arahkan browser Anda ke halaman “news”, yaitu localhost:8080/news
### Create News Items
#### Aktifkan Filter CSRF
Sebelum membuat formulir, aktifkan perlindungan CSRF.

Buka file app/Config/Filters.php dan perbarui $methodsproperti seperti berikut:
```shell
<?php

namespace Config;

use CodeIgniter\Config\BaseConfig;

class Filters extends BaseConfig
{
    // ...

    public $methods = [
        'post' => ['csrf'],
    ];

    // ...
}
```
#### Menambahkan Routing Rules
Sebelum menambahkan news items ke dalam aplikasi CodeIgniter, Anda harus menambahkan rules tambahan ke file app/Config/Routes.php . Pastikan file berisi sebagai berikut ini:
```shell
<?php

// ...

use App\Controllers\News;
use App\Controllers\Pages;

$routes->get('news', [News::class, 'index']);
$routes->get('news/new', [News::class, 'new']); // Add this line
$routes->post('news', [News::class, 'create']); // Add this line
$routes->get('news/(:segment)', [News::class, 'show']);

$routes->get('pages', [Pages::class, 'index']);
$routes->get('(:segment)', [Pages::class, 'view']);
```
#### Buat Form
##### Buat news/buat File View
Buat tampilan baru di app/Views/news/create.php :
```shell
<h2><?= esc($title) ?></h2>

<?= session()->getFlashdata('error') ?>
<?= validation_list_errors() ?>

<form action="/news" method="post">
    <?= csrf_field() ?>

    <label for="title">Title</label>
    <input type="input" name="title" value="<?= set_value('title') ?>">
    <br>

    <label for="body">Text</label>
    <textarea name="body" cols="45" rows="4"><?= set_value('body') ?></textarea>
    <br>

    <input type="submit" name="submit" value="Create news item">
</form>
```
Fungsi ini session()digunakan untuk mendapatkan objek Sesi, dan session()->getFlashdata('error')digunakan untuk menampilkan kesalahan terkait perlindungan CSRF kepada pengguna. Namun, secara default, jika pemeriksaan validasi CSRF gagal, pengecualian akan dilempar, sehingga belum berfungsi.

Fungsi validation_list_errors()yang disediakan oleh Form Helper digunakan untuk melaporkan kesalahan terkait validasi form.

Fungsi ini csrf_field()membuat masukan tersembunyi dengan token CSRF yang membantu melindungi dari beberapa serangan umum.

Fungsi set_value()yang disediakan oleh Form Helper digunakan untuk menampilkan data masukan lama ketika terjadi kesalahan.
##### Pengendalian News
Kembali ke News Controller Anda.
###### Tambahkan News::new() untuk Menampilkan Form
Buatlah metode untuk menampilkan form HTML yang telah di buat.
```shell
<?php

namespace App\Controllers;

use App\Models\NewsModel;
use CodeIgniter\Exceptions\PageNotFoundException;

class News extends BaseController
{
    // ...

    public function new()
    {
        helper('form');

        return view('templates/header', ['title' => 'Create a news item'])
            . view('news/create')
            . view('templates/footer');
    }
}
```
Mennggunakan fungsi helper() untuk membantu Form
###### Tambahkan News::create() untuk membuat News Item
Selanjutnya, buat metode untuk membuat News Items dari data yang dikirimkan.
Anda akan melakukan tiga hal di sini:
1. Memeriksa apakah data yang dikirimkan lolos aturan validasi.
2. Menyimpan item berita ke database.
3. Mengembalikan halaman sukses.
```shell
<?php

namespace App\Controllers;

use App\Models\NewsModel;
use CodeIgniter\Exceptions\PageNotFoundException;

class News extends BaseController
{
    // ...

    public function create()
    {
        helper('form');

        $data = $this->request->getPost(['title', 'body']);

        // Checks whether the submitted data passed the validation rules.
        if (! $this->validateData($data, [
            'title' => 'required|max_length[255]|min_length[3]',
            'body'  => 'required|max_length[5000]|min_length[10]',
        ])) {
            // The validation fails, so returns the form.
            return $this->new();
        }

        // Gets the validated data.
        $post = $this->validator->getValidated();

        $model = model(NewsModel::class);

        $model->save([
            'title' => $post['title'],
            'slug'  => url_title($post['title'], '-', true),
            'body'  => $post['body'],
        ]);

        return view('templates/header', ['title' => 'Create a news item'])
            . view('news/success')
            . view('templates/footer');
    }
}
```
###### Kembalikan Halaman Sukses
Buat tampilan di app/Views/news/success.php dan tulis pesan sukses.
```shell
<p>News item created successfully.</p>
```
#### Updating NewsModel
Edit NewsModel untuk memberikannya daftar fields yang dapat diperbarui di $allowedFields properti.
```shell
<?php

namespace App\Models;

use CodeIgniter\Model;

class NewsModel extends Model
{
    protected $table = 'news';

    protected $allowedFields = ['title', 'slug', 'body'];
}
```
Arahkan browser lokal tempat anda menginstall CodeIgniter dan tambahkan /news/new ke URL.
## CI4 Overview
### Models, Views, dan Controllers
#### Apa itu MCV?
MVC adalah sebuah konsep atau pola desain dalam pengembangan aplikasi yang memisahkan dan mengelompokkan kode berdasarkan fungsinya.
- Models mengelola data aplikasi dan membantu menegakkan aturan bisnis khusus yang mungkin diperlukan aplikasi. Models biasanya disimpan di app/Models.
- Views adalah file sederhana, dengan sedikit atau tanpa logika, yang menampilkan informasi kepada pengguna. Views biasanya disimpan di app/Views
- Controllers bertindak sebagai kode perekat, menyusun data bolak-balik antara tampilan (atau pengguna yang melihatnya) dan penyimpanan data. Controllers biasanya disimpan di app/Controllers
