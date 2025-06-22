<style>
/* Custom styles for architecture page */
.md-sidebar--primary,
.md-sidebar--secondary {
    display: none !important;
}

.md-main__inner {
    margin: 0 !important;
    max-width: none !important;
}

.md-content {
    margin: 0 !important;
    max-width: none !important;
}

.md-content__inner {
    margin: 20px !important;
}

.architecture-nav {
    position: fixed;
    bottom: 20px;
    left: 20px;
    right: 20px;
    z-index: 1000;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.nav-button {
    background: #3f51b5;
    color: white !important;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    text-decoration: none;
    font-weight: bold;
    box-shadow: 0 2px 5px rgba(0,0,0,0.2);
    transition: background 0.3s ease;
    cursor: pointer;
}

.nav-button:hover {
    background: #ff9800;
    color: white !important;
    text-decoration: none;
}

.fullscreen-btn {
    background: #ff9800;
}

.fullscreen-btn:hover {
    background: #f57c00;
}

.architecture-content {
    margin-top: 20px;
    padding: 20px;
    padding-bottom: 80px;
    min-height: calc(100vh - 120px);
}

.mermaid {
    background: white;
    border: 1px solid #e0e0e0;
    border-radius: 8px;
    padding: 20px;
    margin: 0;
    width: 100% !important;
    max-width: none !important;
    height: auto !important;
}

.mermaid svg {
    width: 100% !important;
    max-width: none !important;
    height: auto !important;
}

@media (max-width: 768px) {
    .architecture-nav {
        position: fixed;
        bottom: 10px;
        left: 10px;
        right: 10px;
        flex-direction: column;
        gap: 10px;
    }
    
    .architecture-content {
        margin-top: 10px;
        padding-bottom: 120px;
        min-height: auto;
    }
    
    .nav-button {
        width: 100%;
        text-align: center;
    }
}
</style>

<div class="architecture-nav">
    <a href="../" class="nav-button">← Back to Developers</a>
    <button class="nav-button fullscreen-btn" onclick="toggleFullscreen()">⛶ Fullscreen</button>
</div>

<div class="architecture-content" id="architectureContent">

```mermaid
erDiagram
    %% Client Layer
    WEB-BROWSER ||--|| NGINX : "HTTPS/HTTP"
    ANDROID-APP ||--|| NGINX : "HTTPS/HTTP"
    
    %% Web Infrastructure Layer
    NGINX }|--|{ WEBAPP-SOURCE : "static files"
    NGINX }|--|| SERVER : "REST API"
    NGINX }|--|| MONITOR : SOCKET-IO
    
    %% Client Applications
    WEB-BROWSER {
        access external "https://app.arpi-security.info/"
        access local "https://arpi.local"
        access remote "https://your-dynamic-domain"
    }
    ANDROID-APP {
        type mobile-client
    }

    HOME-AUTOMATION {
        type home-automation

    }

    HOME-AUTOMATION }|--|| MQTT : "MQTT Protocol"
    
    %% Application Services Layer
    SERVER ||--|| MONITOR : IPC-SOCKET
    SERVER {
        type service "systemd: argus_server"
        source path "/home/arpi/server"
        implementation python "flask"
        port value "5000"
    }
    MONITOR {
        type service "systemd: argus_monitor"
        source path "/home/arpi/server"
        implementation python "threading"
        server socket-io
        port value "8081"
    }
    
    %% Data Storage Layer
    MONITOR }|--|| DATABASE : psycopg2
    SERVER }|--|| DATABASE : psycopg2
    DATABASE {
        type postgresql
        port value "5432"
    }
    
    %% Web Presentation Layer
    NGINX {
        type reverse-proxy
        port value "80-443"
    }
    WEBAPP-SOURCE {
        type angular
        source path "/home/arpi/webapplication"
    }
    
    %% Communication Layer
    MONITOR }|--|| MQTT : "paho-mqtt"
    SERVER }|--|| MQTT : "paho-mqtt"
    MQTT {
        type mosquitto
        port value "1883"
        encryption value "TLS/SSL"
    }
    
    %% Hardware Interface Layer
    MONITOR }|--|| GSM-MODULE : serial
    MONITOR }|--|| HW-CLOCK : i2c
    MONITOR }|--|| GPIO : RPi-GPIO
    
    GSM-MODULE {
        type SIM900A
        device path "/dev/ttyAMA0"
        baud value "9600"
    }
    HW-CLOCK {
        type DS1307
        device path "/dev/i2c-1"
    }
    GPIO {
        type raspberry-pi
        sensors wired "NC/NO contacts"
        outputs wired "Relays, siren, keypad"
    }
    
    %% External Services Layer
    SERVER }|--|| SSL-CERT : ssl-certificates
    SERVER }|--|| DYNAMIC-DNS : "ddns-client"
    
    SSL-CERT {
        type cron-job "argus_certbot"
        service external "Let's Encrypt, Certbot"
    }
    DYNAMIC-DNS {
        type cron-job "argus_dyndns"
        service external "noip, duckdns, dyndns"
    }
```

</div>

<script>
function toggleFullscreen() {
    const button = document.querySelector('.fullscreen-btn');
    
    if (!document.fullscreenElement) {
        // Enter fullscreen
        if (document.documentElement.requestFullscreen) {
            document.documentElement.requestFullscreen();
        } else if (document.documentElement.webkitRequestFullscreen) {
            document.documentElement.webkitRequestFullscreen();
        } else if (document.documentElement.msRequestFullscreen) {
            document.documentElement.msRequestFullscreen();
        }
        button.textContent = '✕ Exit Fullscreen';
        document.body.style.overflow = 'auto';
    } else {
        // Exit fullscreen
        if (document.exitFullscreen) {
            document.exitFullscreen();
        } else if (document.webkitExitFullscreen) {
            document.webkitExitFullscreen();
        } else if (document.msExitFullscreen) {
            document.msExitFullscreen();
        }
        button.textContent = '⛶ Fullscreen';
    }
}

// Listen for fullscreen change events
document.addEventListener('fullscreenchange', function() {
    const button = document.querySelector('.fullscreen-btn');
    if (!document.fullscreenElement) {
        button.textContent = '⛶ Fullscreen';
    }
});

// Keyboard shortcuts
document.addEventListener('keydown', function(event) {
    if (event.key === 'F11') {
        event.preventDefault();
        toggleFullscreen();
    }
    if (event.key === 'Escape' && document.fullscreenElement) {
        toggleFullscreen();
    }
});
</script>
