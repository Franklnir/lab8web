# lab8web
 
![image](https://github.com/user-attachments/assets/6401024d-1da6-4cde-bf0f-522c2e12b5ee)

![image](https://github.com/user-attachments/assets/921132b9-4a7c-4d45-8028-60ccb726c448)

### langkah 2
     <?php
      $host = "localhost";
      $user = "root";
      $pass = "";
      $db = "latihan1";
      $conn = mysqli_connect($host, $user, $pass, $db);
      if ($conn == false)
      {
      echo "Koneksi ke server gagal.";
      die();
      } else echo "Koneksi berhasil";
      ?>
![image](https://github.com/user-attachments/assets/09ea1869-3e90-457d-9418-26200317f0e6)

### langkah 3
        <?php
        include("koneksi.php");
        $sql = 'SELECT * FROM data_barang';
        $result = mysqli_query($conn, $sql);
        ?>
        <!DOCTYPE html>
        <html lang="en">
        <head>
        
        <meta charset="UTF-8">
        <link href="style.css" rel="stylesheet" type="text/css" />
        <title>Data Barang</title>
        </head>
        <body>
        <div class="container">
        <h1>Data Barang</h1>
        <div class="main">
        <table>
        <tr>
        <th>Gambar</th>
        <th>Nama Barang</th>
        <th>Katagori</th>
        <th>Harga Jual</th>
        <th>Harga Beli</th>
        <th>Stok</th>
        <th>Aksi</th>
        </tr>
        <?php if($result): ?>
        <?php while($row = mysqli_fetch_array($result)): ?>
        <tr>
        <td><img src="gambar/<?= $row['gambar'];?>" alt="<?=
        $row['nama'];?>"></td>
        <td><?= $row['nama'];?></td>
        <td><?= $row['kategori'];?></td>
        <td><?= $row['harga_beli'];?></td>
        <td><?= $row['harga_jual'];?></td>
        <td><?= $row['stok'];?></td>
        <td><?= $row['id_barang'];?></td>
        </tr>
        <?php endwhile; else: ?>
        <tr>
        <td colspan="7">Belum ada data</td>
        </tr>
        <?php endif; ?>
        </table>
        </div>
        </div>
        </body>
        </html>
![image](https://github.com/user-attachments/assets/b44d7bf3-6b68-4717-b380-1b8dcf49823f)



      
