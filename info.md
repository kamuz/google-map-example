# Google карты

В самом начале нам нужно получить ключ API на странице, подробности здесь [https://developers.google.com/maps/documentation/javascript/get-api-key](https://developers.google.com/maps/documentation/javascript/get-api-key).

Нам не нужно привязывать ключ к какому либо домену, так как этот тест, нам его не нужно как либо ограничивать, поэтому мы не будем использовать **API Key restrictions**.

Создадим базовую HTML разметку и подключим скрипт Google Map, в параметр которого передадим наш API Key `AIzaSyAP1lvNVYgHVwxMGa0pjlscCxWHJu8er2U`:

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <meta name="viewport" content="initial-scale=1.0">
    </head>
    <body>
        <h1>Google Map</h1>
        <script src="https://maps.googleapis.com/maps/api/js?key=AIzaSyAP1lvNVYgHVwxMGa0pjlscCxWHJu8er2U&callback=initMap"
            async defer></script>
    </body>
</html>
```

Теперь создадим блок, куда мы будем вставлять нашу карту `<div id="map"></div>`. В функции `initMap()` мы описываем инициализацию карты. В начале мы создаём объект `Map` на вход которого первым параметром мы передаём элемент куда нужно вставить карту, а вторым набор параметров для нашей карты.

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <meta name="viewport" content="initial-scale=1.0">
        <style>
            #map {
                height: 400px;
                width: 600px;
                margin: 0 auto;
            }
        </style>
    </head>
    <body>
        <h1>Google Map</h1>
        <div id="map"></div>
        <script>
            function initMap(){
                var myMap = document.getElementById('map');
                var myOptions = {
                    zoom: 10,
                    center: {
                        lat: 50.4501,
                        lng: 30.5234
                    }
                }
                var map = new google.maps.Map(myMap, myOptions);
            }
        </script>
        <script src="https://maps.googleapis.com/maps/api/js?key=AIzaSyAP1lvNVYgHVwxMGa0pjlscCxWHJu8er2U&callback=initMap"
            async defer></script>
    </body>
</html>
```

Чтобы быстро получить от Google необходимые координаты, можно ввести запрос следующего вида - `kiev coordinates`. Название переменной с картой желательно называть `map` иначе могут быть ошибки в консоли и вы не получите желаемого результата.

Чтобы добавить маркет нужно использовать объект `Marker` с переданным набором параметров:

```js
function initMap(){
    // Map element
    var map = document.getElementById('map');
    // Coordinates
    myLatLng = {
        lat: 50.4501,
        lng: 30.5234
    }
    // Map options
    var myOptions = {
        zoom: 10,
        center: myLatLng
    }
    // New map
    var map = new google.maps.Map(map, myOptions);
    // Add marker
    var marker = new google.maps.Marker({
        position:myLatLng,
        map: map,
    });
}
```

Чтобы указать пользовательскую иконку для маркера нужно в свойство `icon` передать путь к изображению:

```js
var marker = new google.maps.Marker({
    position:myLatLng,
    map: map,
    icon: 'https://developers.google.com/maps/documentation/javascript/examples/full/images/beachflag.png'
});
```