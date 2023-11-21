## Tugas 9
### Apakah bisa kita melakukan pengambilan data JSON tanpa membuat model terlebih dahulu? Jika iya, apakah hal tersebut lebih baik daripada membuat model sebelum melakukan pengambilan data JSON?
Ya, bisa dilakukan pengambilan data JSON tanpa membuat model terlebih dahulu. Pendekatan ini disebut sebagai "parsing" atau "deserialisasi" JSON, di mana data JSON diubah menjadi struktur data yang dapat digunakan dalam bahasa pemrograman tertentu. Hal ini bergantung pada kebutuhan dan kompleksitas data. Jika struktur data JSON sederhana dan langsung dapat digunakan, tanpa perlu pemodelan tambahan, pendekatan ini bisa lebih efisien. Namun, jika data kompleks atau memerlukan transformasi khusus, pembuatan model atau skema dapat membantu dalam pemahaman dan manipulasi data dengan lebih baik. Keputusan antara keduanya tergantung pada kompleksitas tugas dan kebutuhan aplikasi.

### Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.
CookieRequest mungkin merujuk pada sebuah kelas atau objek dalam konteks aplikasi Flutter yang menangani permintaan atau informasi terkait cookie dalam suatu aplikasi. Membagikan instance CookieRequest ke semua komponen dalam aplikasi Flutter dapat memberikan akses yang konsisten dan terkoordinasi terhadap data cookie di seluruh aplikasi. Dengan demikian, setiap komponen dapat berinteraksi dengan cookie secara terpusat dan dapat mengakses atau memodifikasinya sesuai kebutuhan tanpa perlu mengulang proses pengelolaan cookie di setiap bagian aplikasi. Hal ini dapat meningkatkan efisiensi pengelolaan cookie, mengurangi duplikasi kode, dan memastikan konsistensi data di seluruh aplikasi.

### Jelaskan mekanisme pengambilan data dari JSON hingga dapat ditampilkan pada Flutter.
Mekanisme pengambilan data dari JSON hingga ditampilkan pada Flutter melibatkan beberapa langkah. Pertama, data JSON diambil melalui API atau dari penyimpanan lokal. Kemudian, Flutter menggunakan package seperti http untuk mengirim permintaan HTTP dan mendapatkan respons JSON dari server. Data JSON kemudian di-decode menggunakan library seperti dart:convert untuk mengubahnya menjadi objek Dart. Setelah data di-decode, nilai-nilai tersebut dapat digunakan dalam Flutter untuk mengisi widget seperti ListView atau GridView, atau untuk meng-update state dan menampilkan informasi pada antarmuka pengguna menggunakan widget seperti Text atau Image. Proses ini memungkinkan pengembang Flutter untuk mengambil dan menampilkan data dinamis dengan mudah pada aplikasi mereka.

### Jelaskan mekanisme autentikasi dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.

Mekanisme autentikasi dari input data akun pada Flutter ke Django melibatkan beberapa langkah. Pertama, pengguna memasukkan informasi akun seperti username dan password melalui antarmuka pengguna Flutter. Data ini dikirim ke server Django melalui permintaan HTTP, yang kemudian diproses oleh API Django. Django menggunakan sistem autentikasi bawaan atau pustaka pihak ketiga seperti Django Rest Framework untuk memverifikasi kredensial pengguna. Jika autentikasi berhasil, server Django menghasilkan token akses yang dikirim kembali ke aplikasi Flutter. Aplikasi Flutter kemudian menyimpan token ini secara lokal untuk digunakan dalam permintaan berikutnya.

Setelah proses autentikasi selesai, menu pada Flutter dapat ditampilkan berdasarkan status otentikasi pengguna. Aplikasi dapat membuat permintaan ke endpoint tertentu pada Django yang memerlukan otorisasi, dan token akses disertakan dalam setiap permintaan untuk memverifikasi identitas pengguna. Django kemudian memproses permintaan tersebut dan memberikan respons yang sesuai, memungkinkan aplikasi Flutter untuk menampilkan menu atau konten yang sesuai dengan hak akses pengguna yang sudah diautentikasi. Proses ini memastikan bahwa hanya pengguna yang sah yang dapat mengakses bagian tertentu dari aplikasi berbasis Flutter yang terhubung ke backend Django.

### Sebutkan seluruh widget yang kamu pakai pada tugas ini dan jelaskan fungsinya masing-masing.
1. MaterialApp: Widget utama untuk konfigurasi aplikasi Flutter.
2. Scaffold: Widget yang menyediakan struktur dasar untuk antarmuka visual aplikasi, termasuk AppBar dan body.
3. AppBar: Menampilkan bilah aplikasi di bagian atas layar.
4. Container: Digunakan untuk styling dengan memberikan latar belakang gradient.
5. Column: Menyusun widget-widget anak secara vertikal.
6. Stack: Menempatkan widget-widget anak di atas satu sama lain.
7. Text: Menampilkan teks dengan gaya tertentu.
8. TextField: Input teks untuk memasukkan username dan password.
9. ElevatedButton: Tombol dengan latar belakang terisi. Digunakan untuk tombol login.
10. GestureDetector: Mendeteksi gesture. Digunakan untuk membuat teks "Create New Account" dapat diklik.
11. Navigator: Digunakan untuk navigasi antar halaman.
12. Form: Kontainer untuk elemen-elemen formulir. Memungkinkan validasi dan pengiriman formulir.
13. GlobalKey: Kunci global untuk mengakses state Form.
14. TextFormField: Elemen formulir spesifik untuk menangani input teks.
15. Icon: Ikon grafis. Digunakan untuk ikon di samping kolom input.
16. TextButton: Tombol dengan tampilan datar. Digunakan untuk tombol "Submit".
17. Navigator: Digunakan untuk navigasi antar halaman.
18. Drawer: Menu sisi kiri yang dapat diakses dengan menggeser dari kiri.
19. FutureBuilder: Widget untuk membangun antarmuka berdasarkan hasil masa depan (asynchronous).
20. ListView.builder: Menampilkan daftar item dengan builder callback.
21. InkWell: Widget yang mendeteksi ketukan dan memberikan respons visual.

### Implementasi

#### Django
##### Persiapan Awal:

Buat django-app 'authentication'.

Tambahkan 'authentication' ke INSTALLED_APPS.

Install django-cors-headers.

Tambahkan 'corsheaders' ke INSTALLED_APPS.

Tambahkan middleware CorsMiddleware.

Atur variabel CORS_ALLOW_ALL_ORIGINS dan lainnya pada settings.py.

##### Implementasi Login:

Buat metode view untuk login pada authentication/views.py.

Buat file urls.py di folder authentication untuk routing login.

Tambahkan path('auth/', include('authentication.urls')) di main project urls.py.

##### Implementasi Logout:

Buat metode view untuk logout pada authentication/views.py.

Tambahkan path('logout/', logout, name='logout') di authentication/urls.py.

#### Flutter Implementation:
##### Persiapan Awal:

Install package provider dan pbp_django_auth.

Modifikasi root widget di main.dart menggunakan Provider.

##### Halaman Login:

Buat file login.dart di folder screens untuk halaman login.

Integrasi dengan Django pada main.dart.

##### Model Kustom:

Gunakan Quicktype untuk membuat model Dart dari JSON Django.

##### Fetch Data dari Django:

Tambahkan package http untuk melakukan HTTP request.

Fetch data dari Django untuk ditampilkan di aplikasi Flutter.

##### Form dan Fetch Data:

Hubungkan halaman shoplist_form.dart dengan CookieRequest.

Perbarui tombol tambah untuk mengirim data ke Django.

##### Implementasi Logout:

Tambahkan fungsi logout di proyek Django dan implementasikan di aplikasi Flutter.

Hubungkan fungsi logout dengan widget Inkwell di shop_card.dart.

## Tugas 8

### Perbedaan Navigator.push() dan Navigator.pushReplacement()
Navigation pada flutter berfungsi untuk mengarahkan pengguna ke halaman yang mereka inginkan. Salah satu dari method yang terdapat pada class Navigator adalah .push() dan .pushReplacement(). 

* .push() digunakan untuk menambah layar baru pada posisi top dari stack Navigator. Hal ini memungkinkan pengguna untuk kembali ke layar sebelumnya dengan melakukan method .pop(). Contoh:
```
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => newPage()),
);
```

* .pushReplacement() digunakan untuk mengganti layar yang sedang ditampilkan dengan layar lain. Hal ini membuat pengguna tidak dapat kembali ke layar sebelumnya karena layar sebelumnya sudah di-replace dengan layar yang baru

```
Navigator.pushReplacement(
  context,
  MaterialPageRoute(builder: (context) => HalamanBaru()),
);
```


### Layout widget pada flutter
Beberapa contoh layout widget pada flutter adalah :

1. Container

Digunakan sebagai box model yang dapat membungkus widget lain dan membiarkan kita untuk mengkustomisasi penampilan dan dimensi widget-widgetnya.

```
Container(
  padding: EdgeInsets.all(16.0),
  margin: EdgeInsets.all(8.0),
  decoration: BoxDecoration(
    color: Colors.blue,
    borderRadius: BorderRadius.circular(10.0),
  ),
  child: Text('Hello, Flutter!'),
)
```

2. Row and Column

Mengatur posisi children widgetsnya agar menjadi horizontal (row) atau vertical (column)

```
Row(
  children: [
    Icon(Icons.star),
    Text('5.0'),
  ],
)

Column(
  children: [
    Text('First Name'),
    Text('Last Name'),
  ],
)
```

3. ListView

Membuat widget list yang dapat discroll

```
ListView(
  children: <Widget>[
    ListTile(
      leading: Icon(Icons.map),
      title: Text('Map'),
    ),
    ListTile(
      leading: Icon(Icons.photo),
      title: Text('Album'),
    ),
    // ...
  ],
)
```

4. GridView

Membuat widget grid yang dapat discroll
```
GridView.count(
  crossAxisCount: 2,
  children: <Widget>[
    Card(child: Text('Item 1')),
    Card(child: Text('Item 2')),
    // ...
  ],
)
```

### Elemen input pada form
Pada tugas ini, elemen input yang digunakan pada form adalah `TextFormField`. Elemen ini digunakan untuk menerima input teks dari user.

Beberapa manfaat dari TextFormField :

1. Memiliki Built-in Validation

TextFormField memiliki validator yang berguna untuk memvalidasi input dari pengguna. Jadi, form bisa mengecek apakah pengguna melanggar beberapa kriteria tertentu (misal formnya kosong, atau input melebihi panjang).

2. Input Decoration

TextFormField memiliki properti 'decoration', sehingga kita dapat dengan mudah mengubah tampilan input field yang ada di form.

3. Text Input Formatting

TextFormField memiliki properti 'inputFormatters' sehingga pengguna dapat memasukan custom format pada teks mereka. Misal menambahkan koma pada angka.

4. Obscure Text (Password input)

  TextFormField memiliki properti 'obscureText' untuk menutup informasi sensitif seperti password.

### Bagaimana penerapan clean architecture pada flutter?
Clean architecture adalah filosofi design yang bertujuan untuk membuat software yang maintainable dengan menggunakan konsep SoC dan meminimalisir dependancy.

Clean architecture pada flutter membagi codebase kita menjadi lapisan, dengan tanggung jawab dan dependency masing-masing. Umumnya, lapisan yang dimaksud adalah Presentation, Domain, dan Data. Presentation layer digunakan untuk berkomunikasi dengan use case (domain layer), dan domain layer akan  berinteraksi dengan repository (data layer) untuk melakukan read/write data

### Implementasi checklist secara step-by-step

1. Membuat drawer untuk navigasi.

```
import 'package:flutter/material.dart';
import 'package:tugas_invetory/screens/menu.dart';
import 'package:tugas_invetory/screens/shoplist_form.dart';

class LeftDrawer extends StatelessWidget {
  const LeftDrawer({super.key});

  @override
  Widget build(BuildContext context) {
    return Drawer(
      child: ListView(
        children: [
          const DrawerHeader(
            decoration: BoxDecoration(
              color: Colors.indigo,
            ),
            child: Column(
              children: [
                Text(
                  'rhaken invetory',
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                    color: Colors.white,
                  ),
                ),
                Padding(padding: EdgeInsets.all(10)),
                Text(
                  "rhaken invetory",
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 15,
                    fontWeight: FontWeight.normal,
                    color: Colors.white,
                  ),
                ),
              ],
            ),
          ),
          ListTile(
            leading: const Icon(Icons.home_outlined),
            title: const Text('Halaman Utama'),
            // Bagian redirection ke MyHomePage
            onTap: () {
              Navigator.pushReplacement(
                  context,
                  MaterialPageRoute(
                    builder: (context) => MyHomePage(),
                  ));
            },
          ),
          ListTile(
            leading: const Icon(Icons.add_shopping_cart),
            title: const Text('Tambah Produk'),
            // Bagian redirection ke ShopFormPage
            onTap: () {
              Navigator.pushReplacement(
                  context,
                  MaterialPageRoute(
                    builder: (context) => ShopFormPage(),
                  ));
            },
          ),
        ],
      ),
    );
  }
}

```

2. Membuat form page add item untuk memasukan input item yang kita mau. Form ini memanfaatkan TextFormField sehingga bisa langsung memvalidasi input pengguna juga.

```
import 'package:flutter/material.dart';
import 'package:tugas_invetory/widgets/left_drawer.dart';

class ShopFormPage extends StatefulWidget {
  const ShopFormPage({super.key});

  @override
  State<ShopFormPage> createState() => _ShopFormPageState();
}

class _ShopFormPageState extends State<ShopFormPage> {
  final _formKey = GlobalKey<FormState>();
  String _name = "";
  int _amount = 0;
  String _description = "";
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Center(
          child: Text(
            'Form Tambah Produk',
          ),
        ),
        backgroundColor: Colors.indigo,
        foregroundColor: Colors.white,
      ),
      drawer: const LeftDrawer(),
      body: Form(
        key: _formKey,
        child: SingleChildScrollView(
            child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Padding(
              padding: const EdgeInsets.all(8.0),
              child: TextFormField(
                decoration: InputDecoration(
                    hintText: "Nama Produk",
                    labelText: "Nama Produk",
                    border: OutlineInputBorder(
                      borderRadius: BorderRadius.circular(5.0),
                    )),
                onChanged: (String? value) {
                  setState(() {
                    _name = value!;
                  });
                },
                validator: (String? value) {
                  if (value == null || value.isEmpty) {
                    return "Nama tidak boleh kosong!";
                  }
                  return null;
                },
              ),
            ),
            Padding(
              padding: const EdgeInsets.all(8.0),
              child: TextFormField(
                decoration: InputDecoration(
                  hintText: "Harga",
                  labelText: "Harga",
                  border: OutlineInputBorder(
                    borderRadius: BorderRadius.circular(5.0),
                  ),
                ),
                onChanged: (String? value) {
                  setState(() {
                    _amount = int.parse(value!);
                  });
                },
                validator: (String? value) {
                  if (value == null || value.isEmpty) {
                    return "Harga tidak boleh kosong!";
                  }
                  if (int.tryParse(value) == null) {
                    return "Harga harus berupa angka!";
                  }
                  return null;
                },
              ),
            ),
            Padding(
              padding: const EdgeInsets.all(8.0),
              child: TextFormField(
                decoration: InputDecoration(
                  hintText: "Deskripsi",
                  labelText: "Deskripsi",
                  border: OutlineInputBorder(
                    borderRadius: BorderRadius.circular(5.0),
                  ),
                ),
                onChanged: (String? value) {
                  setState(() {
                    _description = value!;
                  });
                },
                validator: (String? value) {
                  if (value == null || value.isEmpty) {
                    return "Deskripsi tidak boleh kosong!";
                  }
                  return null;
                },
              ),
            ),
            Align(
              alignment: Alignment.bottomCenter,
              child: Padding(
                padding: const EdgeInsets.all(8.0),
                child: ElevatedButton(
                  style: ButtonStyle(
                    backgroundColor: MaterialStateProperty.all(Colors.indigo),
                  ),
                  onPressed: () {
                    if (_formKey.currentState!.validate()) {
                      showDialog(
                        context: context,
                        builder: (context) {
                          return AlertDialog(
                            title: const Text('Produk berhasil tersimpan'),
                            content: SingleChildScrollView(
                              child: Column(
                                crossAxisAlignment: CrossAxisAlignment.start,
                                children: [
                                  Text('Nama: $_name'),
                                  Text('Jumlah: $_amount'),
                                  Text('Deskripsi: $_description'),
                                ],
                              ),
                            ),
                            actions: [
                              TextButton(
                                child: const Text('OK'),
                                onPressed: () {
                                  Navigator.pop(context);
                                },
                              ),
                            ],
                          );
                        },
                      );
                    }
                    _formKey.currentState!.reset();
                  },
                  child: const Text(
                    "Save",
                    style: TextStyle(color: Colors.white),
                  ),
                ),
              ),
            ),
          ],
        )),
      ),
    );
  }
}

```

3. Menambahkan drawer yang telah dibuat ke homepage

Pada file `menu.dart`, kita menambahkan drawer dalam widget Scaffold

```
return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.amber,
        title: const Text(
          'invetory',
        ),
      ),
      body: SingleChildScrollView(
        // Widget wrapper yang dapat discroll
        child: Padding(
          padding: const EdgeInsets.all(10.0), // Set padding dari halaman
          child: Column(
            // Widget untuk menampilkan children secara vertikal
            children: <Widget>[
              const Padding(
                padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                // Widget Text untuk menampilkan tulisan dengan alignment center dan style yang sesuai
                child: Text(
                  'PBP Inventory', // Text yang menandakan toko
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
              // Grid layout
              GridView.count(
                // Container pada card kita.
                primary: true,
                padding: const EdgeInsets.all(20),
                crossAxisSpacing: 10,
                mainAxisSpacing: 10,
                crossAxisCount: 3,
                shrinkWrap: true,
                children: items.map((ShopItem item) {
                  // Iterasi untuk setiap item
                  return ShopCard(item);
                }).toList(),
              ),
            ],
          ),
        ),
      ),
      drawer: const LeftDrawer(),
    );
```
4. Memasukan variabel drawer tadi ke form

```
class _ShopFormPageState extends State<ShopFormPage> {
  final _formKey = GlobalKey<FormState>();
  String _name = "";
  int _amount = 0;
  String _description = "";
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Center(
          child: Text(
            'Form Tambah Produk',
          ),
        ),
        backgroundColor: Colors.indigo,
        foregroundColor: Colors.white,
      ),
      drawer: const LeftDrawer(),
      . . .
      . . .
```

5. Memberikan fungsi pada tombol Tambah Item

```
  Widget build(BuildContext context) {
    return Material(
      color: item.color,
      child: InkWell(
        // Area responsive terhadap sentuhan
        onTap: () {
          // Memunculkan SnackBar ketika diklik
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(
                content: Text("Kamu telah menekan tombol ${item.name}!")));
          if (item.name == "Tambah Produk") {
            Navigator.push(
                context,
                MaterialPageRoute(
                  builder: (context) => ShopFormPage(),
                ));
          }
        },
        . . .
        . . .
```

6. Melakukan refactoring sehingga tampilannya seperti berikut :

![image](https://github.com/rhaken/rhaken_invetory/assets/39646450/eeef99ec-c946-43c9-9fbe-ac20e99fcd44)



# Tugas 7
## Perbedaan Stateless dan Stateful Widget
Dalam pengembangan aplikasi Flutter, perbedaan utama antara stateless widget dan stateful widget terletak pada cara mereka mengelola perubahan data dan perilaku komponen UI. Berikut adalah perbedaan utama antara keduanya:

Stateless widget adalah komponen UI yang tidak memiliki keadaan internal (state). Ini berarti bahwa setelah dibuat, widget ini tidak dapat berubah atau diperbarui.
Stateless widget berguna ketika kita memiliki elemen UI yang tidak memerlukan perubahan atau interaksi selama siklus hidup aplikasi.
Contoh penggunaan stateless widget termasuk teks statis, ikon, gambar, atau elemen UI yang tidak perlu berubah sepanjang waktu.

Stateful widget adalah komponen UI yang bisa memiliki keadaan internal (state) yang bisa berubah selama siklus hidup aplikasi. Keadaan ini bisa berisi data atau informasi yang diperlukan untuk mengubah tampilan atau perilaku widget.
Stateful widget berguna ketika kita perlu mengubah tampilan atau perilaku komponen UI berdasarkan perubahan data atau input pengguna.
Untuk mengelola keadaan dalam stateful widget, kita perlu menggunakan objek "State" yang terkait dengan widget tersebut. Objek State ini bisa diubah selama aplikasi berjalan, dan perubahan ini akan memicu pembaruan tampilan widget.

## Widget-Widget di Tugas Ini dan Fungsinya
1. `MaterialApp`: Widget utama yang digunakan untuk menginisialisasi aplikasi. Biasanya merupakan parent utama dari widget kita. Biasanya digunakan untuk mengatur tema dan color palette dari applikasi kita..

2. `Scaffold`: Scaffold adalah template dasar yang digunakan untuk membuat tampilan seperti applikasi pada umumnya. Scaffold memiliki parameter `appbar`, dan `drawer` sebagai navigasi utama pada applikasi kita.

3. `AppBar`: Widget yang digunakan untuk membuat AppBar (Panel yang ada di atas applikasi).

4. `SingleChildScrollView`: Widget yang memungkinkan childnya dapat discroll. Digunakan untuk membungkus konten utama.

5. `Padding`: Digunakan untuk memberikan padding pada childnya.

6. `Column`: Widget yang menampilkan elemen-elemen secara vertikal, child dari widget ini adalah list of widget / kumpulan dari widget yang akan disusun secara vertikal.

7. `Text`: Widget untuk menampilkan teks. Dapat pula diatur font, warna, dan styling text disini.

8. `Center`: Digunakan untuk mengatur childnya pada posisi ke tengah secara horizontal dan vertikal.

9. `GridView.count`: Digunakan untuk membuat grid layout dengan jumlah kolom yang diberikan.

10. `InkWell`: Digunakan untuk memberikan efek sentuhan. Ini memungkinkan untuk menangani interaksi pengguna. Biasanya diterapkan pada button.

11. `Icon`: Digunakan untuk menampilkan ikon.

12. `SnackBar`: Ini adalah widget yang digunakan untuk menampilkan pesan singkat di bagian bawah layar.

## Implementasi
### 1. Membuat Proyek Flutter Baru
```sh
flutter create rhaken_invetory
```

### 2. Membuat File `menu.dart`
Kita perlu memodifikasi `main.dart` agar dapat mereturn widget yang ada di `menu.dart`
```dart
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.indigo),
        useMaterial3: true,
      ),
      home: MyHomePage(),
    );
  }
}
```

### 3. Memodifikasi File `menu.dart`
Kita sekarang tinggal perlu menyusun apa yang mau ditampilkan di `menu.dart`.
```dart
import 'package:flutter/material.dart';

class ShopItem {
  final String name;
  final IconData icon;
  final Color color;

  ShopItem(this.name, this.icon, this.color);
}

class ShopCard extends StatelessWidget {
  final ShopItem item;

  const ShopCard(this.item, {super.key}); // Constructor

  @override
  Widget build(BuildContext context) {
    return Material(
      color: item.color,
      child: InkWell(
        // Area responsive terhadap sentuhan
        onTap: () {
          // Memunculkan SnackBar ketika diklik
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(
                content: Text("Kamu telah menekan tombol ${item.name}!")));
        },
        child: Container(
          // Container untuk menyimpan Icon dan Text
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  item.icon,
                  color: Colors.white,
                  size: 30.0,
                ),
                const Padding(padding: EdgeInsets.all(3)),
                Text(
                  item.name,
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.white),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}

class MyHomePage extends StatelessWidget {
  MyHomePage({Key? key}) : super(key: key);

  // This widget is the home page of your application. It is stateful, meaning
  // that it has a State object (defined below) that contains fields that affect
  // how it looks.

  // This class is the configuration for the state. It holds the values (in this
  // case the title) provided by the parent (in this case the App widget) and
  // used by the build method of the State. Fields in a Widget subclass are
  // always marked "final".
  final List<ShopItem> items = [
    ShopItem("Lihat Produk", Icons.checklist, const Color(0xFF1A46BD)),
    ShopItem("Tambah Produk", Icons.add_shopping_cart, const Color(0xFF0F286B)),
    ShopItem("Logout", Icons.logout, const Color(0xFF091840)),
  ];

  @override
  Widget build(BuildContext context) {
    // This method is rerun every time setState is called, for instance as done
    // by the _incrementCounter method above.
    //
    // The Flutter framework has been optimized to make rerunning build methods
    // fast, so that you can just rebuild anything that needs updating rather
    // than having to individually change instances of widgets.
    return Scaffold(
      appBar: AppBar(
        title: const Text(
          'Shopping List',
        ),
      ),
      body: SingleChildScrollView(
        // Widget wrapper yang dapat discroll
        child: Padding(
          padding: const EdgeInsets.all(10.0), // Set padding dari halaman
          child: Column(
            // Widget untuk menampilkan children secara vertikal
            children: <Widget>[
              const Padding(
                padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                // Widget Text untuk menampilkan tulisan dengan alignment center dan style yang sesuai
                child: Text(
                  'PBP Shop', // Text yang menandakan toko
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
              // Grid layout
              GridView.count(
                // Container pada card kita.
                primary: true,
                padding: const EdgeInsets.all(20),
                crossAxisSpacing: 10,
                mainAxisSpacing: 10,
                crossAxisCount: 3,
                shrinkWrap: true,
                children: items.map((ShopItem item) {
                  // Iterasi untuk setiap item
                  return ShopCard(item);
                }).toList(),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```
