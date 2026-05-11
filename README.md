# Reflection

### How much data your publisher program will send to the message broker in one run?
- 5 data user

### The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?
- publisher akan join terhubung ke message broker yang sama dengan subscriber (RabbitMQ). mereka akan sama-sama aktif listening di port localhost 5672 dengan mengidentifikasi diri sebagai guest yang memiliki password guest juga.

### Screenshot RabbitMQ
![Screenshot RabbitMQ](static/images/RabbitMQScreen.png)

### Screenshot setelah menjalankan publisher dan subscriber
![Publisher](static/images/Publisher.png)
![Subscriber](static/images/Subscriber.png)

Jadi karena publisher dan subsriber terhubung dengan perantara message broker yang sama (RabbitMQ), maka ketika saya menjalankan publisher data yang dikirim akan tersampaikan ke subscriber. Publisher akan membuat 5 data user setiap dijalankan dan mengirim data tersebut ke rabbitMQ. Subsriber yang melakukan infinite loop akan listening, menangkap, mendeserialisasi, lalu mencetak data yang ia terima setiap ada data yang masuk di rabbitMQ. 

### Screenshot RabbitMQ setelah menjalankan publisher beberapa kali
![RabbitMQPublished](static/images/RabbitMQAfterPublish.png)

Spikenya melambangkan laju publikasi pesan dari publisher ke queue. setiap publisher dijalankan dan 5 data user selesai dikirim ke queue, laju akan kembali ke 0 karena pesan yang ingin diproduksi sudah tidak ada lagi.


### Slow Subscriber
![SlowSubsriber](static/images/RabbitMQSlowSubscriber.png)

Terjadi bottleneck karena subscriber dipaksa menunggu setiap harus memproses event. publisher berjalan lebih cepat dari subscriber dan ketika subscriber tidak bisa memproses secepat itu, maka akan ditampung terlebih dahulu di queue. Pada skenario saya, saya memiliki queue sebanyak 6 karena delay antar run publish yang 1 dengan yang lainnya ada beberapa detik dimana pada delay tersebut queue tersebut dilayani maka peak saya hanya ada di 6 queue saja.