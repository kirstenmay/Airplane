# Airplane
<!DOCTYPE html>
<html>

<head>
    <title>Airplane</title>
</head>

<body>
    <style type="text/css">
        #space {
            background-image: url("space.jpg");
            width: 1024px;
            height: 660px;
        }
        
        .player {
            position: absolute;
            background-image: url("player.png");
            width: 70px;
            height: 75px;
        }
        
        .enemy {
            position: absolute;
            background-image: url("enemy.png");
            width: 70px;
            height: 75px;
        }
        
        .missile {
            position: absolute;
            background-color: greenyellow;
            width: 2px;
            height: 10px;
        }
    </style>
    <div id="space">
        <div id="players"></div>
        <div id="enemies"></div>
        <div id="missiles"></div>
    </div>
    <script type="text/javascript">
        var player = {
            left: 450,
            top: 590
        }

        var missiles = []

        var enemies = [{
            left: 150,
            top: 200
        }, {
            left: 250,
            top: 250
        }, {
            left: 350,
            top: 200
        }, {
            left: 450,
            top: 250
        }, {
            left: 550,
            top: 200
        }, {
            left: 650,
            top: 250
        }]

        function drawPlayer() {
            content = "<div class = 'player' style = 'left:" + player.left + "px; top: " + player.top + "px'></div>";

            document.getElementById("players").innerHTML = content;

        }

        function drawEnemies() {
            content = "";
            for (var idx = 0; idx < enemies.length; idx++) {
                content += "<div class = 'enemy' style = 'left:" + enemies[idx].left + "px; top: " + enemies[idx].top + "px'></div>";
            }
            document.getElementById("enemies").innerHTML = content;
        }

        function drawMissiles() {
            content = "";
            for (var idx = 0; idx < missiles.length; idx++) {
                content += "<div class = 'missile' style = 'left:" + missiles[idx].left + "px; top: " + missiles[idx].top + "px'></div>";
            }
            document.getElementById("missiles").innerHTML = content;
        }

        function moveEnemies() {
            for (var idx = 0; idx < enemies.length; idx++) {
                if (enemies[idx].top < 590) {
                    enemies[idx].top = enemies[idx].top + 2;
                }
            }
        }

        function moveMissiles() {
            for (var idx = 0; idx < missiles.length; idx++) {
                missiles[idx].top = missiles[idx].top - 5;
            }
        }

        document.onkeydown = function(e) {
            if (e.keyCode == 37 && player.left > 260) { //LEFT
                player.left = player.left - 10;
            }
            if (e.keyCode == 39 && player.left < 700) { // RIGHT
                player.left = player.left + 10;
            }
            if (e.keyCode == 40 && player.top < 590) { // DOWN
                player.top = player.top + 10;
            }
            if (e.keyCode == 38 && player.top > 450) { // UP
                player.top = player.top - 10;
            }
            if (e.keyCode == 32) { //Missles
                missiles.push({
                    left: (player.left + 34),
                    top: (player.top - 8)
                })
                drawMissiles();
            }
            drawPlayer();
        }

        function gameLoop() {
            drawPlayer();
            moveEnemies();
            drawEnemies();
            moveMissiles();
            drawMissiles();
            setTimeout(gameLoop, 200)
        }
        gameLoop();
    </script>
</body>

</html>
