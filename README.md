# 🛡️ Auditoría WiFi Ética con Fluxion

> ⚠️ **Aviso Legal**: Esta guía es exclusivamente para fines educativos. Las pruebas deben realizarse solo en redes propias o de laboratorio con autorización. El uso indebido de herramientas como Fluxion puede ser ilegal y está penado por la ley.

---

## 🔍 ¿Qué es Fluxion?

**Fluxion** es una herramienta avanzada de auditoría WiFi que permite poner a prueba la seguridad de redes inalámbricas protegidas con WPA/WPA2. Utiliza un enfoque de **ingeniería social**, creando un **portal cautivo falso** que simula la interfaz de configuración del router y solicita la contraseña al usuario.

A diferencia de otras herramientas, **no utiliza ataques por diccionario directo**, sino que:
- Captura un *handshake WPA2*
- Desconecta a los clientes
- Crea una red clonada
- Muestra una interfaz web falsa para engañar al usuario y obtener la contraseña

---

## 🧰 Requisitos

- Kali Linux (o una distro con herramientas de auditoría)
- Tarjeta de red WiFi compatible con modo monitor (ej. Alfa AWUS036ACH)
- Acceso a una red de laboratorio (propia o autorizada)
- Terminal con privilegios root
- Conexión a Internet para dependencias

---

## ⚙️ Instalación de Fluxion

1. Abre una terminal:

```bash
sudo apt update
sudo apt install git -y
git clone https://github.com/FluxionNetwork/fluxion.git
cd fluxion
sudo ./fluxion.sh
```

2. Fluxion instalará automáticamente las dependencias que falten.


## 🛰️ Uso Básico de Fluxion
1. Ejecutá el script:
```bash
sudo ./fluxion.sh
```
2. Seleccioná el idioma y el adaptador WiFi en modo monitor (Fluxion lo activa si es necesario).

3. Se abrirá el escáner de redes. Esperá unos segundos y presioná Ctrl+C para listar las redes encontradas.

4. Seleccioná la red de pruebas (WPA o WPA2, no WEP ni abiertas).

5. Elegí:
- Modo de ataque: Captura de Handshake y Portal Cautivo
- Confirmá el handshake
- Seleccioná una plantilla de portal (simula la página de configuración del router)

6. El sistema desconectará a los clientes de la red y esperará que se reconecten al portal falso, donde se les pedirá la contraseña.

##  📦 ¿Dónde se guarda el Handshake?
Los archivos .cap (capturas) se guardan por defecto en:
```bash
/root/fluxion/handshakes/
```
Podés verificar que el handshake fue capturado exitosamente antes de continuar.

##  🔓 Crackeo del Handshake WPA2 con Aircrack-ng
Una vez capturado el archivo .cap, se puede usar Aircrack-ng para intentar descifrar la clave mediante diccionario.

###  ▶️ Comando Básico
```bash
aircrack-ng -w /ruta/diccionario.txt -b [MAC_ROUTER] /ruta/handshake.cap
```
📌 Ejemplo:

```bash
aircrack-ng -w /usr/share/wordlists/rockyou.txt -b 00:11:22:33:44:55 /root/fluxion/handshakes/red-pruebas.cap
```
- **-w**: ruta del diccionario (como rockyou.txt, descomprimido con gunzip)

- **-b**: BSSID de la red (MAC del router)

- **.cap**: archivo con el handshake capturado

## 💡 Resultado
- Si la contraseña está en el diccionario, se mostrará en pantalla.
- Si no se encuentra, se puede intentar con diccionarios personalizados o herramientas como hashcat (con GPU).

## 🧪 Ejemplo de Laboratorio de Práctica
- Router WiFi viejo configurado como red de pruebas (SSID: LaboratorioWiFi)
- 1 notebook con Kali Linux y Fluxion
- 1 smartphone o dispositivo conectado al WiFi como víctima (puede ser el tuyo)
- Diccionario: rockyou.txt u otro personalizado

## 📌 Buenas Prácticas
- Nunca ejecutar estas prácticas sobre redes públicas o ajenas
- Siempre informar a los alumnos del enfoque ético y legal
- El objetivo es aprender a defender, no a vulnerar

## 📚 Recursos
- [Repositorio oficial de Fluxion](https://github.com/FluxionNetwork/fluxion)
- [Aircrack-ng Docs](https://www.aircrack-ng.org/)
- [Kali Linux Tools](https://www.kali.org/tools/)
- [Wordlists para pruebas](https://github.com/danielmiessler/SecLists)
