<!doctype HTML>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no">
<meta http-equiv="X-UA-Compatible" content="ie=edge">
<title>Shop</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@200;500&display=swap');
* {
margin: 0;
padding: 0;
box-sizing: border-box;
}
body {
font-family: 'Montserrat', sans-serif;
font-weight: 200;
color: firebrick;
}
#main {
width: 100%;
padding: 20px;
text-align: center;
}
h1 {
margin-top: 50px;
margin-bottom: 10px;
}
img {
width: 70px;
margin: 30px auto;
}
p {
width: 350px;
margin: 0 auto;
}
button {
border: 0;
border-radius: 5px;
margin-top: 50px;
height: 60px;
width: 200px;
font-size: 20px;
font-weight: 500;
cursor: pointer;
transition: all 500ms ease;
color: burlywood;
background: green;
}
button:hover {
background: blue;
}
#form {
    display: none;
    text-align: center;
}
input {
    width: 90%;
    outline: none;
    margin: 10px 5%;
    padding: 15px 10px;
    font-size: 14px;
    border: 2px solid silver;
    border-radius: 5px;
}
input:focus {
    border-color: #db5d5d;
}
</style>
</head>
<body>
<div id="main">
<h1>Онлайн магазин</h1>
    <img src="https://cdn-icons-png.flaticon.com/512/3595/3595455.png">
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Accusantium ipsum magni, molestias.</p>
<button id="buy">Купить</button>
    </div>
    <form id="form">
        <h1>Оформление покупки</h1>>
        <input type="text" placeholder="Имя" id="user_name">
        <input type="text" placeholder="Email" id="user_email">
        <input type="text" placeholder="Телефон" id="user_phone">
        <div id="error"></div>
        <button id="order">Оформить</button>

    </form>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <script>
        let tg = window.Telegram.WebApp;
        let buy = document.getElementById("buy");
        let order = document.getElementById("order");
        tg.expand();

        buy.addEventListener("click", () => {
            document.getElementById("main").style.display = "none"
            document.getElementById("form").style.display = "block"
            document.getElementById("user_name").value = tg.InitDataUnsafe.user.first_name + " " + tg.InitDataUnsafe.user.last_name

        });


        order.addEventListener("click", () => {
            document.getElementById("error").innerText = '';
            let name = document.getElementById("user_name").value
            let email = document.getElementById("user_email").value
            let phone = document.getElementById("user_phone").value
                document.getElementById("error").innerText = '';
            if(name.length < 1) {
                document.getElementById("error").innerText = 'Ошибка в имени! Введите значение от 2 букв';
                return;
            }
            if(phone.length < 10) {
                document.getElementById("error").innerText = 'Ошибка в номер! Введите значение от 10 букв, в формате: 70000000000';
                return;
            }
            if(email.length < 10) {
                document.getElementById("error").innerText = 'Ошибка в номер! Введите значение от 10 букв!';
                return;
            }
            let data = {
                name: name,
                email: email,
                phone: phone
            }
            tg.sendData(JSON.stringify(data));



            tg.close();
        })
    </script>



</body>
</html>
