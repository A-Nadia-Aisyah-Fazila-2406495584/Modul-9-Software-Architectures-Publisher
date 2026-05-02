# Tutorial A

## Try to answer the following questions, and write the answer in the new file readme.md in your repository.
**a. How much data your publisher program will send to the message broker in one run?**
- Publisher akan kirim lima message ke message broker dalam sekali jalan. Itu karena di kode publisher ada lima pemanggilan function `publish_event`, masing-masing dengan data `UserCreatedEventMessage` yang berisi `user_id` dan `user_name` yang berbeda-beda. Jadi tiapkali program publishernya dijalankan broker akan menerima lima events sekaligus.

**b. The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?**
- Artinya publisher dan subscriber connect ke message broker yang sama yaitu RabbitMQ yang jalan di localhost port 5672 dengan credentials yang sama. Penting karena untuk komunikasi bisa terjadi, keduanya harus "talking" lewat broker yang sama. Publisher lempar message ke sana dan subscribernya juga dengerin dari sana.

## Running RabbitMQ Image:
![Running RabbitMQ as message broker](/assets/images/RunningRabbitMQ.png)

## Sending and processing event:
- Publisher:
    ![Sending and processing event publisher image](/assets/images/SendingAndProcessingEventPublisher.png)
    - Explanation: Dapat dilihat bahwa publisher dijalankan dua kali dengan `cargo run`. Setiap kali dijalankan, publisher build dan langsung kirim lima event `UserCreatedEventMessage` ke message broker (RabbitMQ) tanpa output tambahan di console karena tugasnya memang only mengirim, bukan memproses.

- Subscriber:
    ![Sending and processing event subscriber image](/assets/images/SendingAndProcessingEventSubscriber.png)
    - Explanation: Di subscriber terlihat ada sepuluh message masuk yaitu lima dari run yang pertama dan lima dari run kedua publisher. Setiap message berisi data user dengan `user_id` 1 - 5 dan `user_name` Amir, Budi, Cica, Dira, dan Emir. Ini membuktikan bahwa subscriber berhasil menerima dan memproses semua event yang dikirim dari publisher lewat RabbitMQ.