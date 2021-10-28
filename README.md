# myapp

A new Flutter project.

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://flutter.dev/docs/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://flutter.dev/docs/cookbook)

For help getting started with Flutter, view our
[online documentation](https://flutter.dev/docs), which offers tutorials,
samples, guidance on mobile development, and a full API reference.

# flutter
  
Setiap aplikasi Flutter yang Anda buat juga dikompilasi untuk web. Di IDE Anda di bawah pull-down perangkat , atau di baris perintah menggunakan flutter devices, Anda sekarang akan melihat Chrome dan server Web terdaftar. Perangkat Chrome secara otomatis memulai Chrome. The Web Server dimulai sebuah server yang host aplikasi sehingga Anda dapat memuat dari browser apapun. Gunakan perangkat Chrome selama pengembangan sehingga Anda dapat menggunakan DevTools, dan server web saat Anda ingin menguji di browser lain.

1. Membuat aplikasi flutter pemula

sebagian besar akan mengedit lib/main.dart , tempat kode Dart berada.

Ganti isi lib/main.dart.
Hapus semua kode dari lib/main.dart . Ganti dengan kode berikut, yang menampilkan "Hello World" di tengah layar.

 void main() => runApp(MyApp());

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        title: 'Welcome to Flutter',
        home: Scaffold(
          appBar: AppBar(
            title: const Text('Welcome to Flutter'),
          ),
          body: const Center(
            child: Text('Hello World'),
          ),
        ),
      );
    }
  }
  
lalu kita akan menggunakan external paket Pada langkah ini, Anda akan mulai menggunakan paket sumber terbuka bernama english_words , yang berisi beberapa ribu kata bahasa Inggris yang paling sering digunakan ditambah beberapa fungsi utilitas.Anda dapat menemukan english_wordspaket tersebut, serta banyak paket open source lainnya, di pub.dev .
The pubspec.yamlberkas mengelola aset dan dependensi untuk aplikasi Flutter. Di pubspec.yaml, tambahkan english_words (3.1.5 atau lebih tinggi) ke daftar dependensi:


Pada langkah ini, Anda akan menambahkan widget stateful, RandomWords, yang membuat Statekelasnya, _RandomWordsState. Anda kemudian akan menggunakan RandomWordssebagai anak di dalam MyAppwidget stateless yang ada .

1. Buat kode boilerplate untuk widget stateful.
Di lib/main.dart, posisikan kursor Anda setelah semua kode, masukkan Return beberapa kali untuk memulai pada baris baru. Di IDE Anda, mulailah mengetik stful. Editor menanyakan apakah Anda ingin membuat Statefulwidget. Tekan Kembali untuk menerima. Kode boilerplate untuk dua kelas muncul, dan kursor diposisikan bagi Anda untuk memasukkan nama widget stateful Anda.

2. Masukkan RandomWordssebagai nama widget Anda.
The RandomWordswidget tidak sedikit yang lain di samping menciptakan nya Statekelas.

Setelah Anda memasukkan RandomWordsnama widget stateful, IDE secara otomatis memperbarui Statekelas yang menyertainya , menamainya _RandomWordsState. Secara default, nama Statekelas diawali dengan underbar. Awalan pengenal dengan garis bawah memberlakukan privasi dalam bahasa Dart dan merupakan praktik terbaik yang direkomendasikan untuk Stateobjek.

IDE juga secara otomatis memperbarui kelas status ke extend State<RandomWords>, yang menunjukkan bahwa Anda menggunakan State kelas generik yang dikhususkan untuk digunakan denganRandomWords. Sebagian besar logika aplikasi berada di sini—ini mempertahankan status RandomWordswidget. Kelas ini menyimpan daftar pasangan kata yang dihasilkan, yang tumbuh tanpa batas saat pengguna menggulir dan, di bagian 2 lab ini, pasangan kata favorit saat pengguna menambahkan atau menghapusnya dari daftar dengan mengalihkan ikon hati.

  membuat statefull widget

	class MyApp extends StatelessWidget {
	    @override
	    Widget build(BuildContext context) {
      	      final wordPair = WordPair.random();
	      return MaterialApp(
	        title: 'Welcome to Flutter',
	        home: Scaffold(

	            title: const Text('Welcome to Flutter'),
	          ),
	          body: Center(
            child: Text(wordPair.asPascalCase),
            child: RandomWords(),
	          ),
	        ),
	      );
	    }

Langkah 4: Buat ListView bergulir tak terbatas
Pada langkah ini, Anda akan memperluas _RandomWordsStateuntuk menghasilkan dan menampilkan daftar pasangan kata. Saat pengguna menggulir daftar (ditampilkan dalam ListViewwidget) tumbuh tanpa batas. ListView's builderpabrik konstruktor memungkinkan Anda untuk membangun sebuah tampilan daftar malas, pada permintaan.

  Di MyAppkelas, perbarui build()metode dengan mengubah judul, dan mengubah beranda menjadi RandomWordswidget dan inilah script full nya
  
import 'package:english_words/english_words.dart';
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget { 
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Startup Name Generator',
      home: RandomWords(),
    );
  }
}


class _RandomWordsState extends State<RandomWords> {
  final _suggestions = <WordPair>[];
  final _biggerFont = const TextStyle(fontSize: 18.0);
   
  Widget _buildSuggestions() {
    return ListView.builder(
        padding: const EdgeInsets.all(16.0),
        itemBuilder: /1/ (context, i) {
          if (i.isOdd) return const Divider(); /2/

          final index = i ~/ 2; /3/
          if (index >= _suggestions.length) {
            _suggestions.addAll(generateWordPairs().take(10)); /4/
          }
          return _buildRow(_suggestions[index]);
        });
  }
  
  Widget _buildRow(WordPair pair) {
    return ListTile(
      title: Text(
        pair.asPascalCase,
        style: _biggerFont,
      ),
    );
  }
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Startup Name Generator'),
      ),
      body: _buildSuggestions(),
    );
  }
}

class RandomWords extends StatefulWidget {
  @override
  State<RandomWords> createState() => _RandomWordsState();
}


lalu mulai ulang aplikasi dan jalankan f5 untuk running di visual code
Sejauh ini kita telah menjalankan aplikasi Anda dalam mode debug . Mode debug memperdagangkan kinerja untuk fitur pengembang yang berguna seperti hot reload dan step debugging. Bukan hal yang tidak terduga untuk melihat kinerja yang lambat dan animasi yang tersendat-sendat dalam mode debug. Setelah Anda siap untuk menganalisis kinerja atau merilis aplikasi, Anda dapat menggunakan mode build "profil" atau "rilis" Flutter.
