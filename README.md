# **Welcome to Hotel Booking Demand!**
### An Exploratory Data Analysis and Classification Model of Hotel in Portugal

Project ini merupakan project Data Science yang saya buat dengan mengandalkan domain knowledge yang saya miliki, yang meliputi Data Cleaning dan Exploratory Data Analysis, termasuk Univariate/Bivariate/Multivariate Analysis dan Deep Dive Question, serta membuat model Classification menggunakan bahasa pemograman Python.

### **File Description**
Selain README file, terdapat hanya 2 file lain di dalam repository, yaitu:
1. File notebook yang dapat dijalankan dengan menggunakan Google Colab. File tersebut berisikan step-by-step yang dilakukan, coding, model, beserta observation ataupun interpretasi yang didapatkan
2. File power point yang berisikan summary atas project yang dilakukan, sehingga dapat lebih mudah untuk memahami project tanpa melihat secara detail Selain README file, terdapat hanya 2 file lain di dalam repository, yaitu:


### **Business Understanding**
Hotel merupakan bisnis yang menjual "perishable inventory", dimana kamar yang tidak terjual di hari sebelumnya tidak dapat dijual kembali di hari yang akan datang. Dengan demikian, hotel perlu untuk memanage inventory (kamar) sedemikian rupa, sehingga hotel dapat memperoleh profit semaksimal mungkin. Hotel dapat memaksimalkan profit dengan 3 cara, yaitu:
1. Keep existing customer
   Cara yang dapat digunakan untuk retain customer adalah dengan memastikan customer satisfaction. Guest yang puas tentunya akan kembali lagi untuk stay di hotel dan akan mempromosikan hotel kepada customer lain, sehingga dapat membantu untuk menambah new customer ("word of mouth marketing") dan memastikan bertambahnya profit
2. Add  new customer
   Hotel tidak dapat hanya mengandalkan existing customer, melainkan juga harus dapat menambah customer baru. Dengan mengetahui siapa saja guest yang stay di hotel, hotel dapat dengan tepat melakukan marketing untuk menarik new guest untuk stay di hotel dan menambah profit
3. Maximize efficiency
   Hotel memiliki fixed cost yang besar untuk dapat beroperasi. Oleh karena itu, hotel perlu untuk memastikan inventory yang dimiliki terjual semaksimal mungkin. Dengan demikian, sangat perlu bagi hotel untuk dapat mendeteksi siapa saja guest yang akan cancel, sehingga dapat mereplace bookingan tersebut dengan new booking dan dapat memprediksi budget untuk variable cost (jumlah staff yang bekerja, kebutuhan bahan makanan, amenity, etc)


### **Preliminary**
*   Objective Statement:
    *   Mendapatkan business insight untuk mengetahui siapa saja guest yang stay di hotel dan bagaimana detail dari bookingan yang diterima oleh hotel
    *   Mendapatkan business insight dengan menjawab pertanyaan pada deep dive question section
    *   Mengklasifikasikan bookingan apakah akan cancel atau tidak

*   Business Benefit:
    *   Memaksimalkan profit yang diperoleh oleh hotel:
        1. Hotel dapat menargetkan marketing dengan tepat dan menjual kepada customer yang tepat
        2. Hotel dapat meningkatkan efisiensi dengan memprediksi bookingan yang cancel dan mereplace bookingan tersebut

*   Challenges:
    *   Jumlah data yang besar
    *   Adanya missing value, duplikat, kolom yang tidak relevan dan redudancy
   
*   Methodology/Analytic Technique:
    *   Exploratory Data Analysis
    *   Deep-Dive Exploration
    *   Classification

*   Data Understanding:

    Sumber data: Hotel Booking Demand yang berasal dari Kaggle, yang dapat diakses melalui link sebagai berikut:
    https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand

    Selain itu, tertulis di Kaggle bahwa original artikel berasal dari jurnal sebagai berikut:
    https://www.sciencedirect.com/science/article/pii/S2352340918315191#s0010 

    Data merupakan real booking atas city hotel di Lisbon dan resort hotel di Algarve, dimana keduanya terpisahkan sejauh 280 km dengan mobil dan terletak di Portugal, Eropa Selatan, dengan waktu check-in antara 1 July 2015 - 31 August 2017

    Data detail:
    *   hotel: tipe hotel, yaitu resort hotel atau city hotel
    *   is_canceled: apakah bookingan tersebut dicancel atau tidak
    *   lead_time: rentang waktu antara tanggal booking dan tanggal kedatangan (check-in)
    *   arrival_date_year: tahun kedatangan (check-in) 
    *   arrival_date_month: bulan kedatangan (check-in)
    *   arrival_date_week_number: minggu kedatangan (check-in)
    *   arrival_date_day_of_month: tanggal kedatangan (check-in)
    *   stays_in_weekend_nights: jumlah malam hari malam minggu (hari Sabtu atau Minggu) dimana guest stay
    *   stay_in_week_nights: jumlah malam hari biasa (hari Senin - Jumat) dimana guest stay
    *   adults: jumlah dewasa yang stay di hotel
    *   children: jumlah anak yang stay di hotel
    *   babies: jumlah bayi yang stay di hotel
    *   meal: tipe makanan yang termasuk dalam bookingan, terdiri atas undefined/SC (tidak include meal package), BB (hanya include breakfast), HB (include breakfast dan 1 lagi additional meal (biasanya dinner), FB (include breakfast, lunch, dinner)
    *   country: negara asal guest yang stay
    *   market_segment: segmen pasar dari bookingan tersebut, terdiri atas TA (travel agent) dan TO (tour operator)
    *   distribution_channel: jalur distribusi bookingan berasal, terdiri atas TA (travel agent) dan TO (tour operator)
    *   is_repeated_guest: apakah bookingan berasal dari tamu yang sudah pernah stay sebelumnya (diasumsikan bahwa tanggal pembuatan customer profile lebih dulu daripada tanggal pembuatan bookingan ini)
    *   previous_cancellations: jumlah bookingan yang pernah dicancel customer sebelum membuat bookingan ini (diasumsikan bahwa jika customer bukan repeater guest (customer baru), maka = 0)
    *   previous_bookings_not_canceled: jumlah bookingan yang tidak dicancel customer sebelum membuat bookingan ini (diasumsikan bahwa jika customer bukan repeater guest (customer baru), maka = 0)
    *   reserved room type: tipe kamar yang dibooking
    *   assigned_room_type: tipe kamar stay actual
    *   booking_changes: jumlah perubahan/amendemen yang dilakukan sebelum akhirnya guest check-in atau mengcancel bookingan (bisa berupa perubahan nama, tanggal stay, jumlah tamu, etc)
    *   deposit_type: tipe deposit yang dibayarkan, terdiri atas no deposit (tidak ada deposit yang dibayarkan), non refund (deposit dibayarkan sejumlah total biaya stay), refundable (deposit dibayarkan di bawah total biaya stay)
    *   agent: ID agent yang membuat bookingan
    *   company: ID company yang membuat bookingan atau melakukan pembayaran atas bookingan ini
    *   days_in_waiting_list: jumlah hari bookingan berada di waiting list sampai akhirnya diconfirm ke customer (rentang waktu antara tanggal booking diinput ke sistem dan tanggal booking diconfirm ke guest)
    *   customer_type: tipe booking, terdiri atas contract (ketika bookingan memiliki allotment ataupun contract lainnya), group (ketika bookingan berasal dari group), transient (ketika bookingan bukan berasal dari contract atau group dan tidak berhubungan dengan bookingan lainnya), transient party (ketika bookingan berasal dari contract atau group dan tidak berhubungan dengan bookingan lainnya)
    *   adr: average daily rate (penjumlahan atas revenue yang berasal dari guest yang stay dibagi dengan jumlah room night)
    *   required_car_parking_spaces: jumlah tempat parkir mobil yang dibutuhkan
    *   total_of_special_requests: jumlah special request yang disampaikan (seperti kamar di lantai tinggi, kasur twin, kamar tidak merokok, etc)
    *   reservation_status: status terakhir atas bookingan, terdiri atas canceled (bookingan dicancel oleh guest), check out (guest sudah selesai stay), no show (guest tidak check-in dan tidak menginformasikan pada hotel)
    *   reservation_status_date: tanggal terakhir perubahan reservation_status dibuat
