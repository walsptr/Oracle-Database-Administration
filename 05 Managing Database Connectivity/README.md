# Managing Connectivity
### Create Listener

masuk ke network configuration melalui perintah dibawah
```
netca
```

Karena kita akan membuat listener, pilih Listener configuration
<br>
![step 1](/05%20Managing%20Database%20Connectivity/img/step1.png)

Pilih options Add
<br>
![step 2](/05%20Managing%20Database%20Connectivity/img/step2.png)

Berikan nama untuk Listener yang akan dibuat
<br>
![step 3](/05%20Managing%20Database%20Connectivity/img/step3.png)

Disini kita akan memilih protocol TCP
<br>
![step 4](/05%20Managing%20Database%20Connectivity/img/step4.png)

Untuk port listener nya kita biarkan default. Bagi kalian yang mau dibikin custom juga bisa, dengan memilih options Use antoher port number.
<br>
![step 5](/05%20Managing%20Database%20Connectivity/img/step5.png)

Karena kita tidak akan melakukan konfigurasi lain untuk listener, pilih aja No
<br>
![step 6](/05%20Managing%20Database%20Connectivity/img/step6.png)

Jika sudah complete klik Next dan finish
<br>
![step 7](/05%20Managing%20Database%20Connectivity/img/step7.png)


### Connect to database using easy connect
```
sqlplus sys/password@SID as sysdba
```

## Database Link

```
```