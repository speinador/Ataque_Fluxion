# Auditoría WiFi Ética con Fluxion

> ⚠️ Este material es **exclusivamente para fines educativos**. Las pruebas deben realizarse únicamente en redes propias o autorizadas, dentro de un entorno controlado. El uso indebido de estas herramientas puede ser ilegal.

## 📚 ¿Qué es Fluxion?

Fluxion es una herramienta de auditoría WiFi que permite poner a prueba la seguridad de redes inalámbricas. Usa un ataque tipo "man-in-the-middle" para capturar contraseñas WPA/WPA2 engañando al usuario con un portal cautivo.

## 🧪 Requisitos

- Kali Linux (de preferencia versión actualizada)
- Tarjeta de red WiFi compatible con modo monitor y packet injection (como Alfa AWUS036ACH)
- Acceso a una red de pruebas (creada para prácticas educativas)
- Conexión a Internet (opcional, para descargar dependencias)

## 🔧 Instalación

### 1. Abre una terminal en Kali Linux

### 2. Clona el repositorio de Fluxion:
```bash
git clone https://github.com/FluxionNetwork/fluxion.git
cd fluxion
sudo ./fluxion.sh
```
### 3. Sigue las instrucciones en pantalla para instalar dependencias.

## 🧰 Uso Ético en Laboratorio

### 1. Crear un entorno controlado:
- Usa un router viejo o crea un punto de acceso virtual como red objetivo.
- Asegúrate de tener el consentimiento o ser el propietario de la red.

### 2. Ejecutar Fluxion:
- Corre sudo ./fluxion.sh y selecciona el idioma.
- Detecta redes con la opción de escaneo (Requiere modo monitor).
- Elige una red WPA/WPA2 de pruebas.
- Selecciona el tipo de ataque: Portal cautivo.
- Captura la contraseña cuando el usuario (simulado por vos) la introduzca en el portal falso.

### 3. Verificación:
- Fluxion comparará la contraseña capturada con un handshake previo para confirmar si es válida.

## 📎 Notas Técnicas
- Fluxion no usa ataques de diccionario por fuerza bruta.
- Depende de ingeniería social: simula el portal del router para obtener la clave.
- Requiere un handshake válido previo (capturado automáticamente por la herramienta).

## 🛡️ Buenas Prácticas
- Solo practicar en entornos educativos o de laboratorio.
- Nunca ejecutar ataques sobre redes de terceros sin consentimiento.
- Usar esta herramienta como parte de un curso de Seguridad WiFi o Hacking Ético.

## 📌 Referencias
- Repositorio oficial de Fluxion
- Documentación Kali Linux
- Guía de auditoría WiFi ética - OWASP
