# Trenirovochka

<?PHP session_start(); ?>
<?PHP if(isset($_COOKIE['loggedIn']) && $_COOKIE['loggedIn']) : ?>
    <p>Hello, <?= $_COOKIE['login']; ?></p>
    <a href="<?= $_SERVER['PHP_SELF']; ?>?logout=true">logout</a>
<?PHP else : ?>
    <form action="<?= $_SERVER['PHP_SELF']; ?>" method="post">
        <label>login</label><input type="text" name="login" required><br>
        <label>password</label><input type="password" name="password" required><br>
        <label>email</label><input type="email" name="email" required><br>
        <input type="submit" name="submit" value="login">
    </form>
<?PHP endif; ?>
 
<?PHP
$login = 'login';
$pass = 'pass';
$email = 'email@test.com';
 
if(isset($_POST['submit']) && !empty($_POST['submit'])) {
        $data['login'] = $_POST['login'] == $login ? $_POST['login'] : false;
        $data['pass'] = $_POST['password'] == $pass ? $_POST['password'] : false;
        $data['email'] = $_POST['email'] == $email ? $_POST['email'] : false;
       
        foreach($data as $key => $value) {
                If(!$value) $error[] = $key;
        }
       
        if(empty($error)) {
                setcookie('loggedIn', true);
                setcookie('PHPSESSID', session_id());
                setcookie('login', $data['login']);
                session_start();
                header('Location: ' . $_SERVER['PHP_SELF']);
        }
        else {
                print_r($error);
        }
}
 
if(Isset($_GET['logout']) && $_GET['logout'] == true) {
        setcookie("loggedIn", "false", time() - 3600);
        setcookie("PHPSESSID", "", time() - 3600);
        setcookie("login", "", time() - 3600);
        header('Location: ' . $_SERVER['PHP_SELF']);
        session_destroy();
}
?>
