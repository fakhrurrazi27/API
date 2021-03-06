# API
Model TimeSeriesForest dataset gladius


# Instalasi Python

Pastikan sudah terinstall python dan pip dalam system anda, jika system anda mengunakan linux bisa mengikuti command di bawah ini

`
sudo apt install python3-pip
`

jika system mengunakan OS windows atau yang lain bisa minjau situs resmi python untuk instalasi python https://www.python.org/downloads/

# Instalasi Dependency 
Agar code dapat berjalan di perlukan beberapa dependecy, dapat langsung menjalankan command di terminal berikut satu demi satu jika python dan pip sudah terinstall

```
pip install fastapi
pip install uvicorn[standard]
pip install pyts # Dependency baru
```

# Menjalankan API
Untuk menjalankan API cukup mejalankan command berikut di terminal
```
uvicorn main:app --reload
```
Secara default dia akan jalan secara lokal di 127.0.0.1 dengan port 8000 

Output jika runnning berhasil

![image](https://user-images.githubusercontent.com/94620431/143467871-e8eec90c-c5d9-4981-8973-cd9e58187a3c.png)

Jika ingin di jalankan di port dan address host yang berbeda bisa mengunakan option --host dan --port
```
uvicorn --host [host address] --port [nilai port]  main:app --reload 
```

# Menggunakan API
kita akan memprediksi status pembayaran user, apakah user tersebut akan bayar tepat waktu sebelum tanggal 20, telat bayar (bayar di atas tanggal 20), atau tidak membayar, untuk mengunakan endpoint bisa dengan menyiapkan body parameternya berupa format JSON dengan format seperti berikut

```
{
    "billing_2_amountTotal" : "341.000,00", // jumlah tagihan 2 bulan yang lalu
    "billing_3_amountTotal" : "341.000,00", // jumlah tagihan 3 bulan yang lalu
    "billing_4_amountTotal" : "341.000,00", // dst
    "billing_5_amountTotal" : "341.000,00",
    "billing_6_amountTotal" : "341.000,00",
    "billing_7_amountTotal" : "341.000,00",
    "billing_8_amountTotal" : "341.000,00",
    "billing_9_amountTotal" : "341.000,00",
    "billing_10_amountTotal" : "341.000,00",
    "billing_11_amountTotal" : "344.000,00",
    "billing_2_channel" : "FINNET BANK - BANK CENTRAL ASIA", // channel pembayaran 2 bulan yang lalu
    "billing_3_channel" : "FINNET BANK - BANK CENTRAL ASIA", // channel pembayaran 3 bulan yang lalu
    "billing_4_channel" : "FINNET BANK - BANK CENTRAL ASIA", // dst
    "billing_5_channel" : "FINNET BANK - BANK CENTRAL ASIA",
    "billing_6_channel" : "FINNET BANK - BANK CENTRAL ASIA",
    "billing_7_channel" : "FINNET BANK - BANK CENTRAL ASIA",
    "billing_8_channel" : "FINNET BANK - BANK CENTRAL ASIA",
    "billing_9_channel" : "FINNET BANK - BANK CENTRAL ASIA",
    "billing_10_channel" : "FINNET BANK - BANK CENTRAL ASIA",
    "billing_11_channel" : "FINNET BANK - BANK CENTRAL ASIA",
    "billing_2_paymentDate" : 20211018.0, // tanggal pembayaran 2 bulan yang lalu
    "billing_3_paymentDate" : 20210819.0, // tanggal pembayaran 3 bulan yang lalu
    "billing_4_paymentDate" : 20210713.0, // dst
    "billing_5_paymentDate" : 20210618.0,
    "billing_6_paymentDate" : 20210517.0,
    "billing_7_paymentDate" : 20210416.0,
    "billing_8_paymentDate" : 20210316.0,
    "billing_9_paymentDate" : 20210216.0,
    "billing_10_paymentDate" : 20210115.0,
    "billing_11_paymentDate" : 20201217.0,
    "gladius_paketradius" : "INETNLOY20", // paket internet
    "usage" : 4.19 // jumlah penggunaan kuota internet bulan terakhir
    }
```
dan untuk URL API mengunakan format sebagai berikut
```
http://[Host]:[Port]/predict
```
dan request method yang digunakan adalah **PUT** 
API akan mengembalikan JSON juga dengan dua jenis model, model pertama mengembalikan tiga persentase probabilitas status pembayaran bulan selanjutnya (bayar tepat waktu, telat bayar, dan tidak bayar), dan model kedua dengan 2 persentase status pembayaran bulan selanjutnya (bayar tepat waktu, dan telat bayar)

## Hasil Retun API
```
{
    "Model 1": {
        "Bayar Tepat Waktu": 97.8,
        "Telat Bayar": 1.7999999999999998,
        "Tidak Bayar": 0.4
    },
    "Model 2": {
        "Bayar Tepat Waktu": 80.0,
        "Telat Bayar": 20.0
    }
}
```
## Contoh mengunakan POSTMAN
![image](https://user-images.githubusercontent.com/94620431/143846469-df531e18-9a33-4793-841e-87ee77534665.png)
