# lab8web saya membuat database dengan nama "latihan1" di cmd lalu membuat tabel di sql
# dan memasukkan insert into di cmd
 
![image](https://github.com/user-attachments/assets/6401024d-1da6-4cde-bf0f-522c2e12b5ee)

![image](https://github.com/user-attachments/assets/2fdbc41e-9439-40d4-9b2d-ff545b100211)

### langkah 2 Membuat file koneksi database Buat file baru dengan nama koneksi.php

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

### langkah 3 Membuat file index untuk menampilkan data (Read) Buat file baru dengan nama index.php

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
![image](https://github.com/user-attachments/assets/e4439665-8a42-4c12-820c-70116e982fbe)

### langkah 4 Menambah Data (Create) Buat file baru dengan nama tambah.php

        <?php
        error_reporting(E_ALL);
        include_once 'koneksi.php';
        if (isset($_POST['submit']))
        {
        $nama = $_POST['nama'];
        $kategori = $_POST['kategori'];
        $harga_jual = $_POST['harga_jual'];
        $harga_beli = $_POST['harga_beli'];
        $stok = $_POST['stok'];
        $file_gambar = $_FILES['file_gambar'];
        $gambar = null;
        if ($file_gambar['error'] == 0)
        {
        $filename = str_replace(' ', '_',$file_gambar['name']);
        $destination = dirname(__FILE__) .'/gambar/' . $filename;
        if(move_uploaded_file($file_gambar['tmp_name'], $destination))
        {
        $gambar = 'gambar/' . $filename;;
        }
        }
        $sql = 'INSERT INTO data_barang (nama, kategori,harga_jual, harga_beli,
        stok, gambar) ';
        $sql .= "VALUE ('{$nama}', '{$kategori}','{$harga_jual}',
        '{$harga_beli}', '{$stok}', '{$gambar}')";
        $result = mysqli_query($conn, $sql);
        header('location: index.php');
        }
        
        ?>
        <!DOCTYPE html>
        <html lang="en">
        <head>
        <meta charset="UTF-8">
        <link href="style.css" rel="stylesheet" type="text/css" />
        <title>Tambah Barang</title>
        </head>
        <body>
        <div class="container">
        <h1>Tambah Barang</h1>
        <div class="main">
        <form method="post" action="tambah.php"
        enctype="multipart/form-data">
        <div class="input">
        <label>Nama Barang</label>
        <input type="text" name="nama" />
        </div>
        <div class="input">
        <label>Kategori</label>
        <select name="kategori">
        <option value="Komputer">Komputer</option>
        <option value="Elektronik">Elektronik</option>
        <option value="Hand Phone">Hand Phone</option>
        </select>
        </div>
        <div class="input">
        <label>Harga Jual</label>
        <input type="text" name="harga_jual" />
        </div>
        <div class="input">
        <label>Harga Beli</label>
        <input type="text" name="harga_beli" />
        </div>
        <div class="input">
        <label>Stok</label>
        <input type="text" name="stok" />
        </div>
        <div class="input">
        <label>File Gambar</label>
        <input type="file" name="file_gambar" />
        </div>
        <div class="submit">
        <input type="submit" name="submit" value="Simpan" />
        </div>
        </form>
        </div>
        </div>
        </body>
        </html>
![image](https://github.com/user-attachments/assets/04f88185-af54-4704-85af-ae03fe8b1f11)

### langkah 5 Mengubah Data (Update) Buat file baru dengan nama ubah.php

       <?php
       error_reporting(E_ALL);
       include_once 'koneksi.php';
       if (isset($_POST['submit']))
       {
       $id = $_POST['id'];
       $nama = $_POST['nama'];
       $kategori = $_POST['kategori'];
       $harga_jual = $_POST['harga_jual'];
       $harga_beli = $_POST['harga_beli'];
       $stok = $_POST['stok'];
       $file_gambar = $_FILES['file_gambar'];
       $gambar = null;
       if ($file_gambar['error'] == 0)
       {
       $filename = str_replace(' ', '_', $file_gambar['name']);
       $destination = dirname(__FILE__) . '/gambar/' . $filename;
       if (move_uploaded_file($file_gambar['tmp_name'], $destination))
       {
       $gambar = 'gambar/' . $filename;;
       }
       }
       $sql = 'UPDATE data_barang SET ';
       $sql .= "nama = '{$nama}', kategori = '{$kategori}', ";
       $sql .= "harga_jual = '{$harga_jual}', harga_beli = '{$harga_beli}', stok
       = '{$stok}' ";
       if (!empty($gambar))
       $sql .= ", gambar = '{$gambar}' ";
       $sql .= "WHERE id_barang = '{$id}'";
       $result = mysqli_query($conn, $sql);
       header('location: index.php');
       }
       $id = $_GET['id'];
       $sql = "SELECT * FROM `data_barang` WHERE 1";
       $result = mysqli_query($conn, $sql);
       if (!$result) die('Error: Data tidak tersedia');
       $data = mysqli_fetch_array($result);
       function is_select($var, $val) {
       if ($var == $val) return 'selected="selected"';
       return false;
       }
       ?>
       <!DOCTYPE html>
       <html lang="en">
       <head>
       <meta charset="UTF-8">
       <link href="style.css" rel="stylesheet" type="text/css" />
       <title>Ubah Barang</title>
       </head>
       <body>
       <div class="container">
       <h1>Ubah Barang</h1>
       <div class="main">
       <form method="post" action="ubah.php"
       enctype="multipart/form-data">
       <div class="input">
       <label>Nama Barang</label>
       <input type="text" name="nama" value="<?php echo
       $data['nama'];?>" />
       </div>
       <div class="input">
       <label>Kategori</label>
       <select name="kategori">
       <option <?php echo is_select
       ('Komputer', $data['kategori']);?> value="Komputer">Komputer</option>
       <option <?php echo is_select
       ('Komputer', $data['kategori']);?> value="Elektronik">Elektronik</option>
       <option <?php echo is_select
       ('Komputer', $data['kategori']);?> value="Hand Phone">Hand Phone</option>
       </select>
       </div>
       <div class="input">
       <label>Harga Jual</label>
       <input type="text" name="harga_jual" value="<?php echo
       $data['harga_jual'];?>" />
       </div>
       <div class="input">
       <label>Harga Beli</label>
       <input type="text" name="harga_beli" value="<?php echo
       $data['harga_beli'];?>" />
       </div>
       <div class="input">
       <label>Stok</label>
       <input type="text" name="stok" value="<?php echo
       $data['stok'];?>" />
       </div>
       <div class="input">
       <label>File Gambar</label>
       <input type="file" name="file_gambar" />
       </div>
       <div class="submit">
       <input type="hidden" name="id" value="<?php echo
       $data['id_barang'];?>" />
       <input type="submit" name="submit" value="Simpan" />
       </div>
       </form>
       </div>
       </div>
       </body>
       </html>
![image](https://github.com/user-attachments/assets/1d4a3e35-424a-447c-873e-87df7185d9ff)


### langkah 4 menghapus data(delete)
       <?php
       include_once 'koneksi.php';
       $id = $_GET['id'];
       $sql = "DELETE FROM data_barang WHERE id_barang = '{$id}'";
       $result = mysqli_query($conn, $sql);
       header('location: index.php');
       ?>
   ![image](https://github.com/user-attachments/assets/80de2bf1-b0be-478d-a466-05ccc5d7a524)






      
