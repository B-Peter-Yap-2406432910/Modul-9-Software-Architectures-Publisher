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