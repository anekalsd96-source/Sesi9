# 📘 Rangkuman Materi: Extension Methods 

## 👤 Identitas
### Nama       : Aneka Lisda 
### NIM        : 25141013P
### Kelas      : SI2KR
### Mata Kuliah: Pemrograman Berbasis Objek  

---

## 🔹 Pengantar Extension Methods
Extension Methods adalah fitur dalam Dart yang memungkinkan kita menambahkan method baru ke tipe data yang sudah ada tanpa mengubah class aslinya.

---

## 🔹 Masalah Tanpa Extension Methods
Masalah Tanpa Extension Methods adalah kondisi ketika kita ingin menambahkan fungsi ke tipe data yang sudah ada, tetapi harus membuat fungsi terpisah (di luar class) sehingga penggunaannya menjadi kurang praktis dan tidak efisien.
Tanpa extension, kita harus membuat fungsi terpisah:

```dart
String capitalize(String text) {
  if (text.isEmpty) return text; // biar aman kalau kosong
  return text[0].toUpperCase() + text.substring(1);
}

void main() {
  String kata = "hello world";
  String hasil = capitalize(kata);

  print(hasil); // Output: Hello world
}
```
[Klik di sini untuk menjalankan kode DartPad](https://dartpad.dev/7b67fd82ab6f9c897292b902e2d0e1ba)
## Kekurangan:
### Tidak praktis
### Tidak bisa dipanggil langsung dari object
---
## 🔹 Solusi dengan Extension Methods
Solusi dengan Extension Methods adalah cara untuk mengatasi keterbatasan tanpa extension dengan menambahkan fungsi langsung ke tipe data yang sudah ada, sehingga fungsi tersebut bisa dipanggil seperti method bawaan.

Dengan menggunakan extension methods, kita tidak perlu lagi membuat fungsi terpisah di luar class. Sebaliknya, kita bisa menambahkan method ke tipe data seperti String, int, atau class lain, sehingga kode menjadi lebih rapi, mudah dibaca, dan lebih praktis digunakan.
```dart
extension StringExtension on String {
  String capitalize() {
    return this[0].toUpperCase() + substring(1);
  }
}
void main() {
  print("hello".capitalize());
}
```
[Klik di sini untuk menjalankan kode DartPad](https://dartpad.dev/a51d99c84303a8b6e7d8fbb3a0c97cb1)

## Kelebihan:
### Lebih rapi
### Lebih mudah digunakan
---
## 🔹 Sintaks Extension Methods
Sintaks Extension Methods di Dart adalah cara untuk menambahkan method (fungsi baru) ke tipe data yang sudah ada (seperti String, int, dll) tanpa mengubah class aslinya.
Secara sederhana, maksud dari sintaks ini adalah:
kita bisa “menyisipkan” kemampuan tambahan ke suatu tipe data agar bisa digunakan seperti method bawaan.
### berikut contohnya :

```dart
extension NamaExtension on String {
  // method
  String capitalize() {
    if (this.isEmpty) return this;
    return this[0].toUpperCase() + this.substring(1);
  }
}

void main() {
  String teks = "hello dart";

  print(teks.capitalize()); // Output: Hello dart
}
```
<img width="959" height="286" alt="image" src="https://github.com/user-attachments/assets/61668597-df86-4b5a-9c85-3a99b189e425" />

---
## 🔹 Tipe yang Bisa Di-extend
### 1. Built-in types: String , int , double , List , Map , etc.
### 2. Custom classes: Kelas buatan sendiri
### 3. Generic types: List<T> , Map<K, V>
### 4. Nullable types: String? , int?
#### Kita bisa menambahkan fungsi baru ke tipe bawaan (int) tanpa mengubah class aslinya.
```dart
extension IntExtension on int {
  int kuadrat() {
    return this * this;
  }
}

void main() {
  print(5.kuadrat()); // Output: 25
}
```

<img width="1910" height="512" alt="image" src="https://github.com/user-attachments/assets/04896901-fa59-4b41-8a32-9ca3999474e7" />

---
## 🔹 Praktik -1 Utilities untuk Dart Types
Utilities untuk Dart types adalah kumpulan fungsi tambahan (biasanya menggunakan extension methods) yang dibuat untuk membantu mempermudah penggunaan tipe data bawaan Dart seperti String, int, List, dll.

Secara sederhana:

Utilities ini berisi “alat bantu” agar kita tidak perlu menulis kode berulang-ulang saat mengolah data.

Contoh menggunakan String Utilities : 
```dart
// String Utilities
extension StringUtils on String {
  String capitalize() {
    if (this.isEmpty) return this;
    return this[0].toUpperCase() + this.substring(1);
  }
}

// List Utilities
extension ListUtils<T> on List<T> {
  T? firstOrNull() {
    return isEmpty ? null : first;
  }
}

// Nullable Utilities
extension NullableString on String? {
  bool isNullOrEmpty() {
    return this?.isEmpty ?? true;
  }
}

void main() {
  // String
  print("hello".capitalize()); // Hello

  // List
  print([1, 2, 3].firstOrNull()); // 1
  print([].firstOrNull()); // null

  // Nullable
  String? text = null;
  print(text.isNullOrEmpty()); // true

  String? text2 = "dart";
  print(text2.isNullOrEmpty()); // false
}
```
<img width="1904" height="859" alt="image" src="https://github.com/user-attachments/assets/ff15030e-fee1-423f-b7b3-333db7573cc9" />
<img width="1906" height="908" alt="image" src="https://github.com/user-attachments/assets/1fb6c78e-b988-42aa-a065-6b1dc45de272" />

## 🔹 Generic Extensions
Generic Extensions pada Dart adalah extension method yang dibuat menggunakan tipe generik (T) sehingga bisa digunakan pada berbagai tipe data, bukan hanya satu tipe tertentu.
```dart
extension ListExtension<T> on List<T> {
  T? firstOrNull() {
    return isEmpty ? null : first;
  }
}

void main() {
  List<int> angka = [1, 2, 3];
  List<int> kosong = [];

  print(angka.firstOrNull());  // Output: 1
  print(kosong.firstOrNull()); // Output: null
}
```
<img width="956" height="282" alt="image" src="https://github.com/user-attachments/assets/5f4a2840-6b3f-49cb-b646-6dfceb3a3d0d" />

---
## 🔹 Unnamed Extensions
Unnamed Extensions dalam Dart adalah extension method yang tidak memiliki nama (tanpa identifier), sehingga hanya bisa digunakan di dalam file tempat extension tersebut dibuat dan tidak bisa diakses atau dipanggil dari luar file.
```dart
extension on String {
  String shout() => toUpperCase();
}

void main() {
  String text = "hello dart";

  print(text.shout()); // Output: HELLO DART
}
```
<img width="959" height="272" alt="image" src="https://github.com/user-attachments/assets/6c3f8035-1e34-4df1-add6-ac02239906a8" />

## ⚠️ Catatan penting
### Unnamed extension:
### ✅ Bisa dipakai di file yang sama
### ❌ Tidak bisa dipanggil dari file lain

---

## 🔹 Konflik Nama Extension
Konflik Nama Extension dalam Dart terjadi ketika dua atau lebih extension memiliki method dengan nama yang sama pada tipe data yang sama, sehingga Dart menjadi bingung menentukan method mana yang harus digunakan.

Secara sederhana, ini seperti ada dua fungsi dengan nama yang sama dalam satu konteks, sehingga terjadi benturan (conflict). Untuk mengatasinya, kita bisa memanggil extension secara spesifik menggunakan nama extension tersebut, sehingga Dart tahu method mana yang dimaksud. Dengan memahami konflik ini, kita bisa menghindari kesalahan dalam penulisan kode dan menjaga agar program tetap jelas serta terstruktur.

```dart
extension A on String {
  String test() => "A";
}

extension B on String {
  String test() => "B";
}

void main() {
  String text = "hello";

  print(A(text).test()); // Output: A
  print(B(text).test()); // Output: B
}
```
<img width="955" height="278" alt="image" src="https://github.com/user-attachments/assets/91a9893c-22ae-4159-8302-10eca23fd90c" />

## 🔍 Penjelasan singkat
### Ada 2 extension dengan method sama: test()
### Dart bingung kalau kita tulis:
### text.test(); ❌ (error)
### Jadi harus jelas:
### A(text).test() → pakai extension A
### B(text).test() → pakai extension B

---

## 🔹 Extension untuk Custom Class
Extension untuk Custom Class adalah penggunaan extension method pada class yang kita buat sendiri (custom class) untuk menambahkan fungsi baru tanpa harus mengubah kode asli dari class tersebut.
```dart
class User {
  String name;
  User(this.name);
}

extension UserExtension on User {
  String sayHello() {
    return "Hello, $name";
  }
}

void main() {
  User user = User("Aneka");

  print(user.sayHello()); // Output: Hello, Aneka
}
```
<img width="959" height="299" alt="image" src="https://github.com/user-attachments/assets/ae37c665-4883-4fba-93b3-7b490f6ae8f1" />

---
## 🔹 Praktik -2 - Validator Extensions
Validator Extensions adalah extension method di Dart yang digunakan untuk memvalidasi data (mengecek apakah suatu nilai valid atau tidak), biasanya pada tipe seperti String, int, atau lainnya.

Tujuannya:

Membuat proses pengecekan data (seperti email, password, dll) jadi lebih mudah, rapi, dan bisa dipanggil seperti method biasa.

<img width="1873" height="775" alt="image" src="https://github.com/user-attachments/assets/82f1c5f7-48bc-4ba7-81ef-f58c70abf1da" />
<img width="1919" height="884" alt="image" src="https://github.com/user-attachments/assets/271633e1-494d-4605-b5b5-0a376d0df348" />



## 🎯 Kesimpulan

Extension Methods membantu membuat kode lebih rapi, reusable, dan mudah digunakan tanpa harus mengubah class asli. Fitur ini sangat berguna dalam pengembangan aplikasi modern menggunakan Dart.
