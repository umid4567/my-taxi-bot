# my-taxi-bot
<!DOCTYPE html>
<html>
<head>
    <title>Taxi Tracker</title>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://api-maps.yandex.ru/2.1/?lang=uz_UZ&apikey=SIZNING_API_KALITINGIZ" type="text/javascript"></script>
    <style>
        html, body, #map { width: 100%; height: 100%; padding: 0; margin: 0; }
        #info { position: absolute; top: 10px; left: 10px; z-index: 100; background: white; padding: 10px; border-radius: 8px; box-shadow: 0 2px 5px rgba(0,0,0,0.2); }
    </style>
</head>
<body>
    <div id="info">Haydovchi yo'lda...</div>
    <div id="map"></div>

    <script type="text/javascript">
        ymaps.ready(init);
        function init(){
            // Xaritani yaratish (Markaz: Toshkent yoki Kattaqo'rg'on)
            var myMap = new ymaps.Map("map", {
                center: [39.9469, 66.2625], // Kattaqo'rg'on koordinatalari
                zoom: 14
            });

            // Haydovchi belgisi (Mashina)
            var driverMarker = new ymaps.Placemark([39.9469, 66.2625], {
                hintContent: 'Haydovchi shu yerda',
                balloonContent: 'Haydovchi: Umut Home'
            }, {
                preset: 'islands#autoIcon', // Mashina belgisi
                iconColor: '#ff0000'
            });

            myMap.geoObjects.add(driverMarker);

            // Real vaqtda harakatlanishni simulyatsiya qilish (Keyinchalik bazadan olamiz)
            setInterval(function() {
                var currentCoords = driverMarker.geometry.getCoordinates();
                // Mashinani biroz surish (test uchun)
                driverMarker.geometry.setCoordinates([
                    currentCoords[0] + 0.0001,
                    currentCoords[1] + 0.0001
                ]);
            }, 3000);
        }
    </script>
</body>
</html>
