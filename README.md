<!DOCTYPE html>
<html>
<head>
    <title>Interaktywna mapa</title>
    <style>
        body, html {
            margin: 0;
            padding: 0;
            height: 100%;
            overflow: hidden;
        }

        #container {
            width: 100%;
            height: 100%;
            position: relative;
            overflow: hidden;
        }

        #map {
            position: absolute;
            top: 0;
            left: 0;
            transition: transform 0.25s ease;
        }
    </style>
</head>
<body>
    <div id="container">
        <!-- W tym miejscu wybierasz swój obraz -->
        <img id="map" src="my-map.png" alt="Mapa">
    </div>

    <script>
        (function() {
            var map = document.getElementById('map');
            var container = document.getElementById('container');
            var isDragging = false;
            var startX, startY;
            var initialX = 0, initialY = 0;
            var scale = 1;

            container.addEventListener('mousedown', function(e) {
                isDragging = true;
                startX = e.pageX - initialX;
                startY = e.pageY - initialY;
                e.preventDefault();
            });

            container.addEventListener('mousemove', function(e) {
                if (isDragging) {
                    initialX = e.pageX - startX;
                    initialY = e.pageY - startY;
                    map.style.transform = 'translate(' + initialX + 'px, ' + initialY + 'px) scale(' + scale + ')';
                }
            });

            container.addEventListener('mouseup', function() {
                isDragging = false;
            });

            container.addEventListener('mouseleave', function() {
                isDragging = false;
            });

            container.addEventListener('wheel', function(e) {
                e.preventDefault();
                var delta = e.deltaY > 0 ? -0.1 : 0.1;
                scale += delta;
                scale = Math.min(Math.max(0.5, scale), 3); // Limity zoomowania
                map.style.transform = 'translate(' + initialX + 'px, ' + initialY + 'px) scale(' + scale + ')';
            });
        })();
    </script>
</body>
</html>
