# Portal-web-Condominio-pakistan-1
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Simulación de Login</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: Arial, sans-serif;
      background-color: #f0f0f0;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .container {
      background-color: white;
      padding: 40px;
      border-radius: 10px;
      box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.1);
      text-align: center;
      width: 300px;
    }

    h2 {
      font-size: 28px;
      margin-bottom: 20px;
    }

    input[type="email"],
    input[type="password"] {
      width: 100%;
      padding: 12px;
      margin: 10px 0;
      border: 1px solid #ccc;
      border-radius: 5px;
      font-size: 16px;
    }

    button {
      width: 100%;
      padding: 12px;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
      font-size: 16px;
      cursor: pointer;
      margin-bottom: 10px; /* Added margin for Google button */
    }

    button:hover {
      background-color: #45a049;
    }

    .google-btn {
      background-color: #DB4437; /* Google red */
      color: white;
    }

    .google-btn:hover {
      background-color: #c0392b;
    }

    .forgot-password {
      margin-top: 15px;
      font-size: 14px;
    }

    .forgot-password a {
      color: #007bff;
      text-decoration: none;
    }

    .forgot-password a:hover {
      text-decoration: underline;
    }
  </style>
</head>
<body>

  <div class="container">
    <h2>Iniciar sesión</h2>
    <form onsubmit="login(event)">
      <input type="email" id="email" placeholder="Correo electrónico" required><br>
      <input type="password" id="password" placeholder="Contraseña" required><br><br>
      <button type="submit">Ingresar</button>
    </form>
    <button class="google-btn" onclick="loginWithGoogle()">Acceder con Google</button>
    <div class="forgot-password">
      <a href="reset_password.html">¿Olvidaste tu contraseña?</a>
    </div>
  </div>

  <script>
    // User data - This array will be loaded into localStorage
    const usuarios = [
      { email: 'invbordamier@hotmail.com', password: 'Cas@01' },
      { email: 'gladys5185@hotmail.com', password: 'Cas@02' },
      { email: 'nelson.gsosa@hotmail.com', password: 'Cas@02-2' },
      { email: 'dianadu.84@hotmail.com', password: 'Cas@03' },
      { email: 'JESSI-248@HOTMAIL.COM', password: 'Cas@04' },
      { email: 'LALA_BJ@HOTMAIL.COM', password: 'Cas@05' },
      { email: 'MYRIAMCONSUELO@GMAIL.COM', password: 'Cas@05-2' },
      { email: 'INGRID.R.SIERRA@GMAIL.COM', password: 'Cas@06' },
      { email: 'EDGARMOYANO3012@GMAIL.COM', password: 'Cas@07' },
      { email: 'luzgladysroza@hotmail.com', password: 'Cas@08' },
      { email: 'HERNADEZTATIANA2110@GMAIL.COM', password: 'Cas@09' },
      { email: 'ayaeudes@yahoo.com', password: 'Cas@10' },
      { email: 'MARIAE956@YAHOO.COM', password: 'Cas@10-2' },
      { email: 'GEVIBEMU@GMAIL.COM', password: 'Cas@11' },
      { email: 'DORAMBUCI@HOTMAIL.COM', password: 'Cas@12' },
      { email: 'gaby_pili60@hotmail.com', password: 'Cas@13' },
      { email: 'ANDRESMEJIPOLANCO@GMAILCOM', password: 'Cas@14' },
      { email: 'cashtoro@hotmail.com', password: 'Cas@15' },
      { email: 'dianasanchezortegon@gmail.com', password: 'Cas@15-2' },
      { email: 'RAFAELANTONIO.MOYA.DIAZ@GMAIL.COM', password: 'Cas@16' },
      { email: 'ARCHIVALDO1152@GMAIL.COM', password: 'Cas@17' },
      { email: 'OCAICEDO1@HOTMAIL.COM', password: 'Cas@18' },
      { email: 'CAROLDANIELATOROANGULO@GMAIL.COM', password: 'Cas@19' },
      { email: 'JHURANY24@HOTMAIL.COM', password: 'Cas@20' },
      { email: 'andreslpatino@yahoo.com', password: 'Cas@21' },
      { email: 'JURORTIZ@HOTMAIL.COM', password: 'Cas@22' },
      { email: 'FRANJAP24@GMAIL.COM', password: 'Cas@23' },
      { email: 'juade2000@hotmail.com', password: 'Cas@24' },
      { email: 'JMPBASESOR23@GMAIL.COM', password: 'Cas@25' },
      { email: 'bussafo@yahoo.com', password: 'Cas@26' },
      { email: 'dequiro_77@yahoo.es', password: 'Cas@27' },
      { email: 'GLORIASORAYAARIASRAMIREZ@GMAIL.COM', password: 'Cas@28' },
      { email: 'JAVISILVA_VILLANOHOTMAIL.COM', password: 'Cas@29' },
      { email: 'alejo1406@hotmail.com', password: 'Cas@30' },
      { email: 'beltranlugo@hotmail.com', password: 'Cas@31' },
      { email: 'erickbeltran13gmail.com', password: 'Cas@31-2' },
      { email: 'daryeth@hotmail.com', password: 'Cas@32' },
      { email: 'josekasas@hotmail.com', password: 'Cas@33' },
      { email: 'sclaudiapb@hotmail.com', password: 'Cas@34' },
      { email: 'pcpegaso@gmail.com', password: 'Cas@34-2' },
      { email: 'docentevicente@hotmail.com', password: 'Cas@35' },
      { email: 'CLAUDIALILIANAVALENCIAGMAIL.COM', password: 'Cas@36' },
      { email: 'edithmedina448@hotmail.com', password: 'Cas@37' },
      { email: 'emedina@ecoopsoo.com.co', password: 'Cas@37-2' },
      { email: 'gloria13268@yahoo.com', password: 'Cas@38' },
      { email: 'JULIANALR05HOTMAIL.COM', password: 'Cas@39' },
      { email: 'molina.fabio@hotmail.com', password: 'Cas@40' },
      { email: 'anamaria.campos098gmail.com', password: 'Cas@41' },
      { email: 'alfonsoalvarado2007@hotmail.com', password: 'Cas@42' },
      { email: 'estebanfcubides@gmail.com', password: 'Cas@43' },
      { email: 'mariapilic@hotmail.com', password: 'Cas@43-2' },
{ email: 'juanpablo98761234@gmail.com', password: 'Cas@43-3' },
      { email: 'stellarvilla007@yahoo.es', password: 'Cas@44' },
      { email: 'lukas1509@hotmail.com', password: 'Cas@45' },
      { email: 'marthapat929gmail.com', password: 'Cas@46' },
      { email: 'lfdiazc62@hotmail.com', password: 'Cas@46-2' },
      { email: 'bomipabagmail.com', password: 'Cas@47' },
      { email: 'josgue31@gmail.com', password: 'Cas@48' },
      { email: 'bzamorar20@hotmail.com', password: 'Cas@49' },
      { email: 'sandraximenaguerrero123@gmail.com', password: 'Cas@50' },
      { email: 'raulgarvi2009@gmail.com', password: 'Cas@51' },
      { email: 'aleacevedo79@gmail.com', password: 'Cas@52' },
      { email: 'proyectos@jardinesurbanos.com.co', password: 'Cas@53' },
      { email: 'fernandopradilla@yahoo.com', password: 'Cas@53-2' },
      { email: 'alaco20@hotmail.com', password: 'Cas@54' },
      { email: 'joseimw@hotmail.com', password: 'Cas@55' },
      { email: 'm.esperanza330@hotmail.com', password: 'Cas@56' },
      { email: 'myriamgutierrez237@gmail.com', password: 'Cas@57' },
      { email: 'gabrielortizdiazenciso@hotmail.com', password: 'Cas@58' },
      { email: 'henryequinonesb@hotmail.com', password: 'Cas@59' },
      { email: 'ricardolasalagarciataps@gmail.com', password: 'Cas@60' },
      { email: 'monicatatianamahecha@gmail.com', password: 'Cas@61' },
      { email: 'jailander88@gmail.com', password: 'Cas@61-2' },
      { email: 'marlenfi1606@hotmail.com', password: 'Cas@62' },
      { email: 'maxcaicedo@yahoo.com', password: 'Cas@63' },
      { email: 'derly0721@hotmail.com', password: 'Cas@64' },
      { email: 'marthaligia.garciadiaz@gmail.com', password: 'Cas@65' },
      { email: 'claridan69@hotmail.com', password: 'Cas@65-2' },
      { email: 'surkorea-1@hotmail.com', password: 'Cas@66' },
      { email: 'jensonf03@hotmail.com', password: 'Cas@67' },
      { email: 'parratma@yahoo.com', password: 'Cas@68' },
      { email: 'camilojairo@hotmail.com', password: 'Cas@69' },
      { email: 'javelza@yahoo.es', password: 'Cas@70' },
      { email: 'rosalba010559@gmail.com', password: 'Cas@71' },
      { email: 'agustin_luna53@hotmail.com', password: 'Cas@71-2' },
      { email: 'sofiagamboabeta@hotmail.com', password: 'Cas@72' },
      { email: 'docentevicente@hotmail.com', password: 'Cas@73' },
      { email: 'carbolsi3103@gmail.com', password: 'Cas@74' },
      { email: 'diialove17@gmail.com', password: 'Cas@74-2' },
      { email: 'camilo_gomez66@hotmail.com', password: 'Cas@75' },
      { email: 'faguio59@hotmail.com', password: 'Cas@76' },
      { email: 'danitoguio@hotmail.com', password: 'Cas@76-2' },
      { email: 'kittylibia@yahoo.es', password: 'Cas@77' },
      { email: 'fabiangel5@yahoo.es', password: 'Cas@78' },
      { email: 'guapa301@gmail.com', password: 'Cas@79' },
      { email: 'davinchis.eva@gmail.com', password: 'Cas@80' },
      { email: 'ferbusongarcia@hotmail.com', password: 'Cas@81' },
      { email: 'efraincastrofigueroa@hotmail.com', password: 'Cas@82' },
      { email: 'chava1935@hotmail.com', password: 'Cas@83' },
      { email: 'sanyavane@hotmail.com', password: 'Cas@84' },
      { email: 'caritotb1308@hotmail.com', password: 'Cas@85' },
      { email: 'saballestarquino@homtail.com', password: 'Cas@85-2' },
      { email: 'orvimon90@hotmail.com', password: 'Cas@86' },
      { email: 'yuliana.23250207@gmail.com', password: 'Cas@87' },
      { email: 'alsantiago2007@hotmail.com', password: 'Cas@88' }
    ];

    // Store users in localStorage only if they don't already exist
    if (!localStorage.getItem('usuarios')) {
        localStorage.setItem('usuarios', JSON.stringify(usuarios));
    }

    function login(e) {
      e.preventDefault();
      const emailInput = document.getElementById('email').value;
      const passwordInput = document.getElementById('password').value;
      const usuariosGuardados = JSON.parse(localStorage.getItem('usuarios'));

      // Convert email input to lowercase for case-insensitive comparison
      const emailLower = emailInput.toLowerCase();

      const usuarioValido = usuariosGuardados.find(u => u.email.toLowerCase() === emailLower && u.password === passwordInput);

      if (usuarioValido) {
        alert('¡Acceso concedido!');
        window.location.href = 'https://sites.google.com/view/condominiopakistan1etapa/pagina-de-inicio';
      } else {
        alert('Correo o contraseña incorrectos');
      }
    }

    // Basic simulation for "Login with Google"
    function loginWithGoogle() {
        alert('Redirigiendo a Google para iniciar sesión... (Simulación)');
        // In a real application, you would integrate Google Sign-In API here.
        // For this simulation, we'll just redirect to the main page after a short delay.
        setTimeout(() => {
            alert('¡Acceso con Google simulado concedido!');
            window.location.href = 'https://sites.google.com/view/condominiopakistan1etapa/pagina-de-inicio';
        }, 1500); // Simulate a short delay
    }
  </script>

</body>
</html>
