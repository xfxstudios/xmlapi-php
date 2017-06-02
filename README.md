# xmlapi-php
A PHP Class for Interacting with cPanel's XML-API
#
URL de Comandos:
https://www.codepunker.com/blog/using-php-to-create-new-subdomains-databases-and-email-accounts-on-a-cpanel-driven-server?lang=es

<h3>Creación de un nuevo subdominio</h3>

      $cpanelusr = 'username';
      $cpanelpass = 'password';
      $xmlapi = new xmlapi('127.0.0.1');
      $xmlapi->set_port( 2083 );
      $xmlapi->password_auth($cpanelusr,$cpanelpass);
      $xmlapi->set_debug(0);
      $result = $xmlapi->api1_query($cpanelusr, 'SubDomain', 'addsubdomain', 
      array('subdomainname','domain.com',0,0, '/public_html/subdomainname'));
    
<h3>Creación de una nueva base de datos y un usuario para ella</h3>
    
    $cpanelusr = 'username';
    $cpanelpass = 'password';
    $xmlapi2 = new xmlapi('127.0.0.1');
    $xmlapi2->set_port( 2083 );
    $xmlapi2->password_auth($cpanelusr,$cpanelpass);
    $xmlapi2->set_debug(0);

    //$databasename y $databaseuser contendrán el prefijo de cPanel Ej: prefix_dbname y prefix_dbuser
    $databasename = 'db_name';
    $databaseuser = 'db_usr'; //¡Tener cuidado! Esto puede tener un máximo de 7 caracteres
    $databasepass = 'passwordforthenewuser';

    $createdb = $xmlapi2->api1_query($cpanelusr, "Mysql", "adddb", array($databasename)); //crea la base de datos
    $usr = $xmlapi2->api1_query($cpanelusr, "Mysql", "adduser", array($databaseuser, $databasepass)); //crea el usuario
    $addusr = $xmlapi2->api1_query($cpanelusr, "Mysql", "adduserdb", 
    array("".$cpanelusr."_".$databasename."", "".$cpanelusr."_".$databaseuser."", 'all')); 
    //concede todos los privilegios al usuario que acabamos de crear
     $cpanelusr = 'username';
    $cpanelpass = 'password';
    $xmlapi2 = new xmlapi('127.0.0.1');
    $xmlapi2->set_port( 2083 );
    $xmlapi2->password_auth($cpanelusr,$cpanelpass);
    $xmlapi2->set_debug(0);

    // $databasename y $databaseuser contendrán el prefijo de cPanel Ej: prefix_dbname y prefix_dbuser
    $databasename = 'db_name';
    $databaseuser = 'db_usr'; //¡Tener cuidado! Esto puede tener un máximo de 7 caracteres
    $databasepass = 'passwordforthenewuser';

    $createdb = $xmlapi2->api1_query($cpanelusr, "Mysql", "adddb", array($databasename)); //crea la base de datos
    $usr = $xmlapi2->api1_query($cpanelusr, "Mysql", "adduser", array($databaseuser, $databasepass)); //crea el usuario
    $addusr = $xmlapi2->api1_query($cpanelusr, "Mysql", "adduserdb", 
    array("".$cpanelusr."_".$databasename."", "".$cpanelusr."_".$databaseuser."", 'all')); 
    //concede todos los privilegios al usuario que acabamos de crear
    
     $cpanelusr = 'username';
    $cpanelpass = 'password';
    $xmlapi2 = new xmlapi('127.0.0.1');
    $xmlapi2->set_port( 2083 );
    $xmlapi2->password_auth($cpanelusr,$cpanelpass);
    $xmlapi2->set_debug(0);

    // $databasename y $databaseuser contendrán el prefijo de cPanel Ej: prefix_dbname y prefix_dbuser
    $databasename = 'db_name';
    $databaseuser = 'db_usr'; //¡Tener cuidado! Esto puede tener un máximo de 7 caracteres
    $databasepass = 'passwordforthenewuser';

    $createdb = $xmlapi2->api1_query($cpanelusr, "Mysql", "adddb", array($databasename)); //crea la base de datos
    $usr = $xmlapi2->api1_query($cpanelusr, "Mysql", "adduser", array($databaseuser, $databasepass)); //crea el usuario
    $addusr = $xmlapi2->api1_query($cpanelusr, "Mysql", "adduserdb", 
    array("".$cpanelusr."_".$databasename."", "".$cpanelusr."_".$databaseuser."", 'all')); 
    //concede todos los privilegios al usuario que acabamos de crear
    
<h3>Adición de una nueva cuenta de correo electrónico</h3>

    $email_user = "emailusr";
    $email_password = "emailusrpass";
    $email_domain = "domain.com";
    $email_quota = '10';

    $addemail $xmlapi->api1_query($cpanelusr, "Email", "addpop", array($email_user, $email_password, $email_quota, $email_domain) );
    

Por supuesto que usted puede hacer mucho más si se estudia la API cPanel, pero el código de arriba ha sido 
probado antes por mí mismo y pensé que debía compartirlo con ustedes. No dude en añadir más API llamadas en la sección de comentarios.
