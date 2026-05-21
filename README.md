# 📘 Rangkuman Materi: Extension Methods (Dart)

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
<img width="959" height="301" alt="image" src="https://github.com/user-attachments/assets/246d45ec-a0b9-4490-aebf-f759f51aa53e" />

## Kekurangan:
### Tidak praktis
### Tidak bisa dipanggil langsung dari object
---
## 🔹 Solusi dengan Extension Methods
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
<img width="959" height="332" alt="image" src="https://github.com/user-attachments/assets/5951e76e-1a74-47d1-9875-0e5ceb58ce97" />

## Kelebihan:
### Lebih rapi
### Lebih mudah digunakan
---
## 🔹 Sintaks Extension
Sintaks Extension di Dart adalah cara untuk menambahkan method (fungsi baru) ke tipe data yang sudah ada (seperti String, int, dll) tanpa mengubah class aslinya.
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
### String
### int
### double
### List
### Custom Class
---
## 🔹 Extension untuk Null Safety
Extension untuk Null Safety dalam Dart adalah penggunaan extension method pada tipe data yang bisa bernilai null (nullable), seperti String?, untuk menangani kondisi null dengan aman tanpa menyebabkan error.
```dart
extension NullableString on String? {
  bool isNullOrEmpty() {
    return this?.isEmpty ?? true;
  }
}

void main() {
  String? text1 = null;
  String? text2 = "";
  String? text3 = "hello";

  print(text1.isNullOrEmpty()); // true
  print(text2.isNullOrEmpty()); // true
  print(text3.isNullOrEmpty()); // false
}
```
<img width="954" height="278" alt="image" src="https://github.com/user-attachments/assets/b423c465-bc59-454d-ba56-e8d016a17081" />

---

## Generic Extensions
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
## 🎯 Kesimpulan

Extension Methods membantu membuat kode lebih rapi, reusable, dan mudah digunakan tanpa harus mengubah class asli. Fitur ini sangat berguna dalam pengembangan aplikasi modern menggunakan Dart.
