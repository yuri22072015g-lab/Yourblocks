<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Yourblocks — вход и регистрация</title>
    <style>
        body { font-family: Arial, sans-serif; max-width: 400px; margin: 50px auto; padding: 20px; background: #f5f5f5; }
        .container { background: white; padding: 30px; border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); }
        input, button { width: 100%; padding: 12px; margin: 8px 0; border: 1px solid #ddd; border-radius: 4px; box-sizing: border-box; }
        button { background: #4285f4; color: white; border: none; cursor: pointer; font-size: 16px; }
        button:hover { background: #3367d6; }
        .hidden { display: none; }
        .error { color: #d32f2f; margin: 10px 0; }
        .success { color: #388e3c; margin: 10px 0; }
        h2 { margin-top: 0; }
        hr { margin: 20px 0; }
    </style>
    <!-- Firebase SDK (совместимая версия) -->
    <script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-auth-compat.js"></script>
</head>
<body>
    <div class="container" id="app">
        <!-- Формы для неавторизованных -->
        <div id="unauthorized">
            <h2>Добро пожаловать в Yourblocks!</h2>
            <div id="message"></div>
            
            <h3>Вход</h3>
            <input type="email" id="loginEmail" placeholder="Email" required>
            <input type="password" id="loginPassword" placeholder="Пароль" required>
            <button onclick="login()">Войти</button>

            <hr>

            <h3>Регистрация</h3>
            <input type="email" id="regEmail" placeholder="Email" required>
            <input type="password" id="regPassword" placeholder="Пароль (минимум 6 символов)" required>
            <button onclick="register()">Зарегистрироваться</button>
        </div>

        <!-- Профиль авторизованного пользователя -->
        <div id="authorized" class="hidden">
            <h2>Личный кабинет</h2>
            <p>Вы вошли как: <strong><span id="userEmail"></span></strong></p>
            <p><strong>Ваш UID:</strong> <span id="userUid"></span></p>
            <button onclick="logout()" style="background: #dc3545;">Выйти</button>
        </div>
    </div>

    <script>
        // 🔥 ВАШ ОБЪЕКТ firebaseConfig (данные из консоли)
        const firebaseConfig = {
            apiKey: "AIzaSyCMgDxuPbye5rpZcS7JAHD_6PEDbAc3ZdU",
            authDomain: "yourblocks-ccdb7.firebaseapp.com",
            projectId: "yourblocks-ccdb7",
            storageBucket: "yourblocks-ccdb7.firebasestorage.app",
            messagingSenderId: "531017606276",
            appId: "1:531017606276:web:5eab2f87a2f9f5c885ced1",
            measurementId: "G-JSWF0QVSJ9"
        };

        // Инициализация Firebase
        firebase.initializeApp(firebaseConfig);
        const auth = firebase.auth();

        // Отслеживание состояния аутентификации
        auth.onAuthStateChanged((user) => {
            if (user) {
                document.getElementById('unauthorized').classList.add('hidden');
                document.getElementById('authorized').classList.remove('hidden');
                document.getElementById('userEmail').textContent = user.email;
                document.getElementById('userUid').textContent = user.uid;
            } else {
                document.getElementById('unauthorized').classList.remove('hidden');
                document.getElementById('authorized').classList.add('hidden');
                document.getElementById('message').innerHTML = '';
            }
        });

        // Регистрация
        function register() {
            const email = document.getElementById('regEmail').value.trim();
            const password = document.getElementById('regPassword').value.trim();
            const messageDiv = document.getElementById('message');
            
            if (password.length < 6) {
                messageDiv.className = 'error';
                messageDiv.textContent = 'Пароль должен быть не менее 6 символов';
                return;
            }
            
            auth.createUserWithEmailAndPassword(email, password)
                .then(() => {
                    messageDiv.className = 'success';
                    messageDiv.textContent = 'Регистрация успешна! Выполняется вход...';
                    document.getElementById('regEmail').value = '';
                    document.getElementById('regPassword').value = '';
                })
                .catch((error) => {
                    messageDiv.className = 'error';
                    if (error.code === 'auth/email-already-in-use') {
                        messageDiv.textContent = 'Этот email уже зарегистрирован';
                    } else if (error.code === 'auth/invalid-email') {
                        messageDiv.textContent = 'Некорректный email';
                    } else {
                        messageDiv.textContent = 'Ошибка: ' + error.message;
                    }
                });
        }

        // Вход
        function login() {
            const email = document.getElementById('loginEmail').value.trim();
            const password = document.getElementById('loginPassword').value.trim();
            const messageDiv = document.getElementById('message');
            
            auth.signInWithEmailAndPassword(email, password)
                .then(() => {
                    messageDiv.className = 'success';
                    messageDiv.textContent = 'Вход выполнен успешно!';
                    document.getElementById('loginEmail').value = '';
                    document.getElementById('loginPassword').value = '';
                })
                .catch((error) => {
                    messageDiv.className = 'error';
                    if (error.code === 'auth/user-not-found') {
                        messageDiv.textContent = 'Пользователь не найден';
                    } else if (error.code === 'auth/wrong-password') {
                        messageDiv.textContent = 'Неверный пароль';
                    } else {
                        messageDiv.textContent = 'Ошибка: ' + error.message;
                    }
                });
        }

        // Выход
        function logout() {
            auth.signOut().then(() => {
                document.getElementById('message').className = 'success';
                document.getElementById('message').textContent = 'Вы вышли из системы';
            }).catch((error) => {
                document.getElementById('message').className = 'error';
                document.getElementById('message').textContent = 'Ошибка при выходе: ' + error.message;
            });
        }
    </script>
</body>
</html>
