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
