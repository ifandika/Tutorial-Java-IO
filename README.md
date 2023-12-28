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
Java menyimpan data karakter dengan konvensi Unicode, Character Stream mengkonversi data by karakter.
Character Stream memproses I/O 16-bit Unicode(International Character Encoding). Karena menggunakan
Unicode data yang berbeda seperti data Bahasa Jepang, China memiliki nilai yang berbeda maka jika
menggunakan Byte Stream bisa jadi keluaran data tidak sesuai.

Untuk kelas I/O character stream menggunakan **Reader** & **Writer**. Karena pada contoh sumber menggunakan
file maka menggunakan kelas **FileReader** & **FileWriter**.
```Java
import java.util.*;
import java.io.*;

public class CopyCharacters {
	public static void main(String[] args) throws IOException {
        FileReader inputStream = null;
        FileWriter outputStream = null;
        
        try {
            inputStream = new FileReader("source.txt");
            outputStream = new FileWriter("characteroutput.txt");
            
            int c;
            while ((c = inputStream.read()) != -1) {
                outputStream.write(c);
            }
        } finally {
            if (inputStream != null) {
                inputStream.close();
            }
            if (outputStream != null) {
                outputStream.close();
            }
        }
    }
}
```
### 2.3 Buffered Stream
Byte Stream & Character Stream membaca data per-karakter. Jika Buffered Stream membaca per baris(line-oriented).
Kelas untuk I/O yang digunakan **BufferedReader** & **PrintWriter**.
```Java
import java.util.*;
import java.io.*;

public class CopyBytes {
	public static void main(String[] args) throws IOException {
		BufferedReader br = null;
		PrintWriter pw = null;
		
		try {
			// Karena dari file maka menggunakan FileReader & FileWriter
			br = new BufferedReader(new FileReader("source.txt"));
			pw = new PrintWriter(new FileWriter("bufferedoutput.txt"));
			String line;
			
			while((line = br.readLine()) != null) {
				pw.println(line);
			}
		} finally {
			if(br != null) br.close();
			if(pw != null) pw.close();
		}
	}
}
```
### 2.4 Scanning
Kelas **Scanner** juga bisa digunakan untuk membaca informasi file, dengan cara memecah data masukan menjadi
per-token/per-kalimat yang dipisahkan spasi/whitespace.
```Java
import java.io.*;
import java.util.Scanner;

public class MyScanner {
    public static void main(String[] args) throws IOException {
        Scanner s = null;
        
        try {
            s = new Scanner(new BufferedReader(new FileReader("output.txt")));
            
            while (s.hasNext()) {
                System.out.println(s.next());
            }
        } finally {
            if (s != null) {
                s.close();
            }
        }
    }
}
```
Keluaran
```Bash
Ini
adalah
file
source.txt
Pemilik:
Maulana
Ifandika
Kali
ini
kita
akan
belajar
tentang
Java
I/O
dimana
membahas
tentang
Input
&
Output
pada
Java.
```
Jika data dipisahkan dengan simbol tertentu, menggunakan fungsi **Scanner.useDelimiter()** untuk nilai parameter menggunakan
regular ekspresi. Contoh jika data dipisahkan denga koma ( , ).
```Java
s.useDelimiter(",\\s*");
```
### 2.5 Formatting
Objek Stream mendukung formating, contoh kelas untuk formating **PrintWriter** untuk character stream & **PrintStream** untuk
byte stream. 2 Contoh kelas tersebut sudah ada fungsi standar untuk menulis/write, terbagi menjadi 2:

- print & println untuk format tersendiri.
- format berisi opsi-opsi yang bisa digunakan.
#### Fungsi print & println
Fungsi print & println fungsi standar atau yang umum untuk menampilkan suatu data, jika fungsi print hanya menampilkan data
tanpa membuat baris baru(New line) sedangkan println menampilkan data & membuat baris baru.
```Java
public class Root {
    public static void main(String[] args) {
        int i = 2;
        double r = Math.sqrt(i);
        
        System.out.print("The square root of ");
        System.out.print(i);
        System.out.print(" is ");
        System.out.print(r);
        System.out.println(".");

        i = 5;
        r = Math.sqrt(i);
        System.out.println("The square root of " + i + " is " + r + ".");
    }
}
```
Output
```Bash
The square root of 2 is 1.4142135623730951.
The square root of 5 is 2.23606797749979.
```
#### Fungsi format







