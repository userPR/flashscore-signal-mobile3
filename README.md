# Flashscore Canlı Sinyaller Mobile v0.3

## v0.3 ANR düzeltmesi

v0.2 gerçek telefonda hâlâ `Uygulama yanıt vermiyor` uyarısı oluşturabildi.
Bunun ana nedeni monitor ve worker WebView'larının MainActivity ile aynı Android
process'inde çalışmasıydı.

v0.3 değişiklikleri:

- `MonitorService` artık ayrı `:monitor` process'inde çalışır.
- Flashscore monitor + stats worker WebView'ları ana uygulama UI thread'ini
  doğrudan bloke edemez.
- Android 9+ için monitor process'e ayrı WebView data directory suffix atanır.
- Dashboard ile monitor process arasındaki state paylaşımı SharedPreferences
  yerine atomik `live_state.json` dosyasıyla yapılır.
- State dosyası yazma işlemi monitor ana thread'inden ayrı tek iş parçacığında yapılır.
- Monitor WebView renderer önceliği `IMPORTANT` yerine `BOUND` seviyesine çekildi.
- Mevcut foreground notification ve 25 saniyelik stats timeout korunur.

Bu sürüm özellikle Samsung/Android cihazlardaki ANR problemini hedefler.
