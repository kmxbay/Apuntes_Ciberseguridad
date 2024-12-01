Actualiza el sistema
```bash
sudo apt update
sudo apt upgrade -y
```
Instalar Docker
Ejecuta los siguientes comandos para instalar Docker
```bash
sudo apt install -y docker.io
```
Verifica la instalación
```bash
docker --version
```
Habilitar y iniciar el servicio Docker o si Docker está instalado pero no está corriendo
```bash
sudo systemctl start docker
sudo systemctl enable docker
```
Asegúrate de que tu usuario tenga los permisos necesarios para usar Docker
```bash
sudo usermod -aG docker $USER
```
