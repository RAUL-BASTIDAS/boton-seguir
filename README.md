# boton-seguir
<div class="share-buttons">
    <!-- Botón de Facebook -->
    <a href="#" onclick="shareOnFacebook()" class="share-button facebook">
        Compartir en Facebook
    </a>

    <!-- Botón de Twitter -->
    <a href="#" onclick="shareOnTwitter()" class="share-button twitter">
        Compartir en Twitter
    </a>

    <!-- Botón de WhatsApp -->
    <a href="#" onclick="shareOnWhatsApp()" class="share-button whatsapp">
        Compartir en WhatsApp
    </a>
</div>

<style>
.share-buttons {
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin-top: 20px;
}

.share-button {
    padding: 10px 20px;
    border-radius: 6px;
    color: white;
    text-decoration: none;
    font-family: Helvetica, Arial, sans-serif;
    font-weight: bold;
    text-align: center;
    cursor: pointer;
}

.facebook {
    background-color: #1877f2;
}

.twitter {
    background-color: #1da1f2;
}

.whatsapp {
    background-color: #25D366;
}
</style>

<script>
// Función para compartir en Facebook
function shareOnFacebook() {
    const url = encodeURIComponent(window.location.href);
    window.open(`https://www.facebook.com/sharer/sharer.php?u=${url}`, '_blank');
}

// Función para compartir en Twitter
function shareOnTwitter() {
    const url = encodeURIComponent(window.location.href);
    const text = encodeURIComponent('¡Sigue a Jhon Molina Putumayo en Facebook!');
    window.open(`https://twitter.com/intent/tweet?url=${url}&text=${text}`, '_blank');
}

// Función para compartir en WhatsApp
function shareOnWhatsApp() {
    const url = encodeURIComponent(window.location.href);
    const text = encodeURIComponent('¡Hola! Te invito a seguir la página de Jhon Molina Putumayo: ');
    const fullMessage = `${text}${url}`;
    
    if (/Android|iPhone|iPad|iPod/i.test(navigator.userAgent)) {
        window.open(`whatsapp://send?text=${fullMessage}`);
    } else {
        window.open(`https://web.whatsapp.com/send?text=${fullMessage}`);
    }
}
</script>
