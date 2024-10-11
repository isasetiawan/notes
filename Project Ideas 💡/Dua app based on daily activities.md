The siri will suggest daily dua for current activities:

**Definisikan Aktivitas Pengguna**: Gunakan `NSUserActivity` untuk mendefinisikan aktivitas yang terkait dengan berbagai jenis doa harian yang pengguna lakukan. Misalnya, aktivitas untuk doa pagi, doa sebelum makan, doa sebelum tidur, dll.

2. **Aktivitas yang Dapat Diprediksi**: Pastikan untuk menandai aktivitas Anda dengan` isEligibleForPrediction` dan `isEligibleForSearch` sehingga Siri dapat mempertimbangkan aktivitas ini untuk disarankan kepada pengguna.

3. **Intent Definition**: Jika Anda ingin pengguna dapat membuat shortcut kustom untuk doa tertentu, Anda bisa mendefinisikan intent di file .intentdefinition Anda. Ini memungkinkan pengguna untuk membuat shortcut langsung dari aplikasi Siri.

4. **Interaksi dengan SiriKit**: Gunakan SiriKit untuk menangani interaksi pengguna dengan aplikasi Anda, termasuk donasi interaksi (interaction.donate) untuk aktivitas yang penting.