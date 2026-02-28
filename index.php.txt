<?php
// Запускаем сессию для хранения данных пользователя
session_start();

// Подключаемся к SQLite базе данных (файл users.db создастся автоматически)
try {
    $db = new PDO('sqlite:users.db');
    $db->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    // Создаём таблицу пользователей, если её нет
    $db->exec("CREATE TABLE IF NOT EXISTS users (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        username TEXT UNIQUE NOT NULL,
        password TEXT NOT NULL
    )");
} catch (PDOException $e) {
    die("Ошибка подключения к БД: " . $e->getMessage());
}

// Обработка действий (регистрация, вход, выход)
$message = '';
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    if (isset($_POST['register'])) {
        // Регистрация
        $username = trim($_POST['username']);
        $password = $_POST['password'];
        if ($username && $password) {
            // Хешируем пароль
            $hash = password_hash($password, PASSWORD_DEFAULT);
            try {
                $stmt = $db->prepare("INSERT INTO users (username, password) VALUES (?, ?)");
                $stmt->execute([$username, $hash]);
                $message = "<p style='color:green;'>Регистрация успешна! Теперь войдите.</p>";
            } catch (PDOException $e) {
                $message = "<p style='color:red;'>Ошибка: возможно, имя пользователя уже занято.</p>";
            }
        } else {
            $message = "<p style='color:red;'>Заполните все поля.</p>";
        }
    } elseif (isset($_POST['login'])) {
        // Вход
        $username = trim($_POST['username']);
        $password = $_POST['password'];
        if ($username && $password) {
            $stmt = $db->prepare("SELECT * FROM users WHERE username = ?");
            $stmt->execute([$username]);
            $user = $stmt->fetch(PDO::FETCH_ASSOC);
            if ($user && password_verify($password, $user['password'])) {
                $_SESSION['user_id'] = $user['id'];
                $_SESSION['username'] = $user['username'];
                // Перенаправляем на ту же страницу, чтобы обновить состояние
                header('Location: ' . $_SERVER['PHP_SELF']);
                exit;
            } else {
                $message = "<p style='color:red;'>Неверное имя пользователя или пароль.</p>";
            }
        } else {
            $message = "<p style='color:red;'>Заполните все поля.</p>";
        }
    }
} elseif (isset($_GET['logout'])) {
    // Выход
    session_destroy();
    header('Location: ' . $_SERVER['PHP_SELF']);
    exit;
}
?>
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Простой сайт с входом</title>
    <style>
        body { font-family: Arial, sans-serif; max-width: 400px; margin: 50px auto; padding: 20px; }
        input, button { width: 100%; padding: 10px; margin: 5px 0; box-sizing: border-box; }
        .form-container { border: 1px solid #ccc; padding: 20px; border-radius: 5px; }
        .message { margin: 10px 0; }
        a { color: #007bff; text-decoration: none; }
        a:hover { text-decoration: underline; }
    </style>
</head>
<body>

<?php if (isset($_SESSION['user_id'])): ?>
    <!-- Приветствие для залогиненного пользователя -->
    <h1>Добро пожаловать, <?php echo htmlspecialchars($_SESSION['username']); ?>!</h1>
    <p>Вы успешно вошли в аккаунт.</p>
    <p><a href="?logout=1">Выйти</a></p>
<?php else: ?>
    <!-- Формы регистрации и входа для гостей -->
    <h1>Добро пожаловать</h1>
    <?php if ($message) echo "<div class='message'>$message</div>"; ?>

    <div class="form-container">
        <h2>Вход</h2>
        <form method="post">
            <input type="text" name="username" placeholder="Имя пользователя" required>
            <input type="password" name="password" placeholder="Пароль" required>
            <button type="submit" name="login">Войти</button>
        </form>
    </div>

    <div class="form-container" style="margin-top: 20px;">
        <h2>Регистрация</h2>
        <form method="post">
            <input type="text" name="username" placeholder="Имя пользователя" required>
            <input type="password" name="password" placeholder="Пароль" required>
            <button type="submit" name="register">Зарегистрироваться</button>
        </form>
    </div>
<?php endif; ?>

</body>
</html>