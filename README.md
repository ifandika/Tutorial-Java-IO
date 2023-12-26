# Tutorial Java IO(Input/Output)
#
## 1. Pendahuluan
Membahas tentang kelas-kelas pada Java yang digunakan untuk operasi I/O(Input/Output), I/O Stream, 
Akses File, dll. Terdapat pada package java.io untuk kelas-kelas yang diperlukan seperti:

- InputStream
- File
- BufferedReader
- dll.

Dan juga package java.nio

## 2. I/O Stream
I/O Stream adalah representasi sumber & tujuan, representasi dapat berupa File, Perangkat,
Program, Memori, dsb. Aliran Stream mendukung berbagi jenis data seperti Tipe data primitif,
Bytes, Objek.

![Image](resource/img/img-1.gif)  
(Membaca informasi lewat program)

Program membaca informasi menggunakan Input Stream & menulis informasi ke tujuan dengan Output
Stream.

![Image](resource/img/img-2.gif)  
(Menulis informasi ke tujuan)

Sebagai contoh untuk sumber informasi menggunakan file format .txt, untuk nama filenya source.txt

**[source.txt]**
```Txt
Ini adalah file source.txt
Pemilik: Maulana Ifandika

Kali ini kita akan belajar tentang Java I/O dimana
membahas tentang Input & Output pada Java.
```
### 2.1 Byte Stream
Byte Stream digunakan untuk memproses input & output 8-bit(1 Bytes). Kelas untuk Input & Output byte
stream adalah **InputStream** & **OutputStream**, namun ada banyak kelas untuk byte stream. Pada contoh ini
karena sumber menggunakan file, maka I/O menggunakan kelas **FileInputStream** & **FileOutputStream**.  
Buat main
class bernama CopyBytes karena akan membaca isi file source.txt lalu membuat file baru bernama output.txt dan menulis
data yang diambil.
```Java
import java.util.*;
import java.io.*;
import java.nio.*;

public class CopyBytes {
	public static void main(String[] args) throws IOException {
		
		FileInputStream fi = null;
		FileOutputStream fo = null;
		
		try {
			fi = new FileInputStream("source.txt");
			fo = new FileOutputStream("output.txt");
			int c;
			
			while((c = fi.read()) != -1) {
				fo.write(c);
			}
		} finally {
			if(fi != null) {
				fi.close();
			}
			if(fo != null) {
				fo.close();
			}
		}
		
	}
}
```
Untuk cara kerja.
![Image](resource/img/img-3.gif)  
(I/O Byte Stream)

### 2.2 Character Stream
Jika Byte Stream merubah menjadi byte, jika data berisi 




