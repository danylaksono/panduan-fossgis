# Konsumsi Data dengan Standar OGC

## Menggunakan Perangkat FOSS untuk mengakses data OGC
Berbagai perangkat FOSS dapat saling berkomunikasi dengan bantuan dukungan standar OGC. Untuk latihan ini, QGIS akan digunakan sebagai perangkat client untuk memanggil data dari Geoserver.

![](img/2020-12-04-05-23-55.png)


### Memanggil WMS, WFS dan WCS dengan QGIS
QGIS telah menyediakan fungsi yang cukup lengkap untuk memanggil data dari Geoserver. Berikut caranya:

![](img/2020-12-04-08-47-22.png)

Tiap menu digunakan untuk memanggil layanan OGC dari jenis yang berbeda. Parameter yang digunakan antara lain adalah alamat host Geoserver, sedangkan QGIS akan memanggil daftar layer yang tersedia secara otomatis.

### Memanggil data publikasi OGC dengan Javascript Library (LeafletJS)

Pada LeafletJS (dan library web map lain seperti OpenLayers, GMap API, Mapbox dst), layer secara umum terbagi menjadi dua macam, yaitu 1) Tilelayer (‘Slippy Map’) yang dapat diperoleh dalam bentuk layanan (service) dari penyedia tile, dan 2) Feature Layer yang dapat ditambahkan sendiri pada Leaflet. Tilelayer cenderung bersifat statis, tidak interaktif dan disajikan dalam bentuk ‘tile’. Tilelayer sering digunakan sebagai background atau basemap untuk peta yang akan dibuat pada sebuah webmap library seperti Leaflet. Pada Tilelayer ini tidak dapat diterapkan konsep interaktivitas, misalnya memunculkan popup berdasarkan atribut (dengan beberapa pengecualian, misalnya pada Vector Tile).

Adapun Feature Layer merupakan layer yangdapat ditambahkan pada LeafletJS Map bersumber dari data yang kita miliki. Contoh Feature layer yang banyak dijumpai adalah Marker. Pada Marker kita dapat memberikan atribut dan menerapkan interaktivitas, misalnya dengan memunculkan popup, melakukan drag and drop, dan seterusnya. Selain marker, kita juga dapat menambahkan polygon dan polyline dengan cara yang hampir sama. Feature Layer yang lain adalah GeoJSON, yang memungkinkan kita untuk menambahkan layer data spasial lengkap dengan atribut dan fungsi interaktifnya. Pada bagian ini akan dibahas bagaimana menggunakan GeoJSON untuk menampilkan data spasial (shapefile) menjadi peta yang interaktif pada LeafletJS melalui Geoserver.

Untuk memanggil data dari Geoserver menggunakan LeafletJS, dapat digunakan script seperti berikut:

```javascript
    var layerjalan = L.tileLayer.wms('http://localhost:8080/geoserver/wms?', {
        layers: 'latihan:jalan'
    }).addTo(map);
```

Contoh script LeafletJS tersedia pada https://github.com/danylaksono/sample-leafletjs. Sebagai latihan, modifikasi script tersebut untuk memanggil layer KRB dari Server pada alamat http://54.254.9.31:8080/geoserver sebagai WMS. 








