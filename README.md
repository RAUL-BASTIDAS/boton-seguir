# boton-seguir Jhon Molina
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Seguir a Jhon Molina Putumayo</title>
    <style>
        .fb-button {
            background-color: #1877f2;
            border: none;
            border-radius: 6px;
            color: white;
            padding: 12px 24px;
            font-family: Helvetica, Arial, sans-serif;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 10px;
            transform-style: preserve-3d;
            transition: all 0.3s;
            box-shadow: 0 4px 0 #0d5ab9;
            margin: 20px;
        }

        .fb-button.disabled {
            background-color: #666;
            box-shadow: 0 4px 0 #444;
            cursor: not-allowed;
            opacity: 0.7;
        }

        .fb-button:not(.disabled):hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 0 #0d5ab9;
        }

        .fb-icon {
            background-color: white;
            color: #1877f2;
            width: 24px;
            height: 24px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-style: normal;
            font-weight: bold;
        }

        .mensaje {
            background-color: white;
            padding: 15px 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            margin-bottom: 20px;
            font-family: Helvetica, Arial, sans-serif;
            color: #1877f2;
            text-align: center;
        }

        body {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            background-color: #f0f2f5;
        }

        .reset-button {
            margin-top: 20px;
            padding: 8px 16px;
            border: none;
            border-radius: 4px;
            background-color: #f0f2f5;
            color: #666;
            cursor: pointer;
            font-size: 12px;
        }

        .reset-button:hover {
            background-color: #e4e6eb;
        }

        /* Agregamos estilos para la ventana emergente */
        .popup {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0,0,0,0.2);
            z-index: 1001;
            max-width: 90%;
            width: 400px;
        }

        .overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.7);
            z-index: 1000;
        }

        .popup-content {
            text-align: center;
        }

        .popup-buttons {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin-top: 20px;
        }

        .popup-button {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
        }

        .confirm-button {
            background-color: #1877f2;
            color: white;
        }

        .cancel-button {
            background-color: #e4e6eb;
            color: #1c1e21;
        }
    </style>
</head>
<body>
    <div id="mensajeEstado" class="mensaje"></div>
    
    <!-- Ventana emergente -->
    <div class="overlay" id="overlay"></div>
    <div class="popup" id="followPopup">
        <div class="popup-content">
            <h3>Seguir a Jhon Molina Putumayo</h3>
            <p>¿Deseas seguir esta página en Facebook?</p>
            <div class="popup-buttons">
                <button class="popup-button confirm-button" id="confirmFollow">Seguir</button>
                <button class="popup-button cancel-button" id="cancelFollow">Cancelar</button>
            </div>
        </div>
    </div>

    <!-- Botones flotantes -->
    <div class="floating-container">
        <button id="fbFollowBtn" class="fb-button">
            <i class="fb-icon">f</i>
            <span>Seguir a Jhon Molina</span>
        </button>

        <button id="whatsappBtn" class="whatsapp-button">
            <span class="whatsapp-icon">
                <!-- ... ícono de WhatsApp ... -->
            </span>
            <span>Compartir</span>
        </button>
    </div>

    <button id="resetBtn" class="reset-button" style="display: none;">
        Reiniciar estado
    </button>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const fbButton = document.getElementById('fbFollowBtn');
            const whatsappBtn = document.getElementById('whatsappBtn');
            const popup = document.getElementById('followPopup');
            const overlay = document.getElementById('overlay');
            const mensajeEstado = document.getElementById('mensajeEstado');
            const resetBtn = document.getElementById('resetBtn');
            const PAGINA_FB = 'https://www.facebook.com/JhonMolinaPutumayo';

            // Verificar si ya sigue la página
            const yaSiguiendo = localStorage.getItem('siguiendoJhonMolina');

            function actualizarEstado(siguiendo) {
                if (siguiendo) {
                    fbButton.classList.add('disabled');
                    fbButton.innerHTML = '<i class="fb-icon">f</i><span>Ya sigues esta página</span>';
                    mensajeEstado.textContent = '¡Ya estás siguiendo a Jhon Molina Putumayo!';
                    resetBtn.style.display = 'block';
                } else {
                    fbButton.classList.remove('disabled');
                    fbButton.innerHTML = '<i class="fb-icon">f</i><span>Seguir a Jhon Molina</span>';
                    mensajeEstado.textContent = 'Click para seguir a Jhon Molina Putumayo';
                    resetBtn.style.display = 'none';
                }
            }

            // Establecer estado inicial
            actualizarEstado(yaSiguiendo);

            // Manejar click en el botón de seguir
            fbButton.addEventListener('click', function() {
                if (!yaSiguiendo) {
                    popup.style.display = 'block';
                    overlay.style.display = 'block';
                }
            });

            // Botón para reiniciar estado (para pruebas)
            resetBtn.addEventListener('click', function() {
                localStorage.removeItem('siguiendoJhonMolina');
                actualizarEstado(false);
            });

            // Manejar click en el botón de confirmar seguir
            document.getElementById('confirmFollow').addEventListener('click', function() {
                window.open(PAGINA_FB, '_blank');
                localStorage.setItem('siguiendoJhonMolina', 'true');
                actualizarEstado(true);
                popup.style.display = 'none';
                overlay.style.display = 'none';
            });

            // Manejar click en el botón de cancelar seguir
            document.getElementById('cancelFollow').addEventListener('click', function() {
                popup.style.display = 'none';
                overlay.style.display = 'none';
            });
        });
    </script>
</body>
</html> 
