<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Conectando al Sistema de Autobuses...</title>
    <style>
        body { font-family: sans-serif; display: flex; justify-content: center; align-items: center; height: 100vh; background: #f0f0f0; }
        .mensaje { text-align: center; padding: 20px; background: white; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
    </style>
</head>
<body>

    <div class="mensaje">
        <h2>Buscando el servidor local... 🚌</h2>
        <p>Por favor, asegúrate de estar conectado al WiFi del autobús.</p>
    </div>

    <script>
        async function conectarAlServidor() {
            // La misma URL de tu Firebase
            const firebaseUrl = "https://TU-PROYECTO-default-rtdb.firebaseio.com/config.json";
            
            try {
                // 1. Preguntamos a la nube cuál es la IP
                const respuesta = await fetch(firebaseUrl);
                const datos = await respuesta.json();
                
                if (datos && datos.ip_servidor) {
                    // 2. Armamos la URL local
                    const urlLocal = `http://${datos.ip_servidor}:${datos.puerto}`;
                    
                    // 3. Redirigimos al usuario a tu aplicación (Vite)
                    window.location.replace(urlLocal);
                } else {
                    alert("El servidor no ha reportado su ubicación todavía.");
                }
            } catch (error) {
                alert("Error de conexión. ¿Tienes internet activo?");
            }
        }

        // Ejecutar apenas cargue la página
        conectarAlServidor();
    </script>

</body>
</html>
