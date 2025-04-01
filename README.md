git remote set-url origin https://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@github.com/JorgeArdila2169/MLOps_2510.git

git remote set-url origin https://ghp_BKljxLNY8ohDcAZaTf(QUITEESTO)6uzhhqOZwa4V1k5D09@github.com/JorgeArdila2169/MLOps_2510.git

# Manual: Actualizar un repositorio local con los cambios de GitHub

Este documento describe los pasos necesarios para sincronizar tu repositorio local con los cambios más recientes del repositorio remoto en GitHub.

## 1. Abrir una Terminal

Abre una terminal en tu sistema operativo Linux o cualquier otro donde tengas Git instalado.

## 2. Navegar al Directorio del Repositorio

Usa el comando `cd` para moverte a la carpeta donde está tu repositorio local. Ejemplo:
```bash
cd /ruta/del/repositorio
```
Si no recuerdas la ruta exacta, puedes verificarla con:
```bash
pwd
```

## 3. Verificar el Estado del Repositorio

Ejecuta:
```bash
git status
```
Esto mostrará si hay cambios no confirmados en tu repositorio local.

### 3.1 Si tienes cambios sin confirmar
Si hay archivos modificados o sin agregar, puedes:
- Guardarlos temporalmente usando **stash**:
  ```bash
  git stash
  ```
  (Recuperar cambios después con `git stash pop`).
- Confirmar los cambios antes de continuar:
  ```bash
  git add .
  git commit -m "Guardando cambios antes de actualizar"
  ```

## 4. Obtener los Últimos Cambios de GitHub

Para actualizar tu repositorio local con los cambios del repositorio remoto, ejecuta:
```bash
git pull origin main
```
(Si tu rama principal es `master`, usa `git pull origin master`).

Esto descargará y fusionará los cambios remotos con tu repositorio local.

## 5. Verificar que Todo se Actualizó Correctamente

Puedes comprobar los últimos commits ejecutando:
```bash
git log --oneline -5
```
Esto muestra los últimos 5 commits en tu repositorio.

## 6. Resolver Conflictos (si los hay)

Si `git pull` muestra conflictos, edita los archivos afectados manualmente y luego ejecuta:
```bash
git add .
git commit -m "Resolviendo conflictos de merge"
```
Después, puedes continuar con tu trabajo normalmente.

## 7. Recuperar Cambios Guardados con Stash (Opcional)
Si en el paso 3.1 usaste `git stash`, recupéralo con:
```bash
git stash pop
```

## 8. Verificar el Estado Final del Repositorio
Ejecuta nuevamente:
```bash
git status
```
Debe indicar que no hay cambios pendientes si todo salió bien.

---

Con estos pasos, tu repositorio local estará actualizado con los últimos cambios de GitHub. 🚀

Aquí tienes el manual organizado y estructurado de manera clara para que puedas actualizar tus cambios de local a GitHub sin problemas:

---

# 📖 Manual: Actualizar cambios de local a GitHub

## 1️⃣ Configurar Git (si es la primera vez)

Antes de hacer cualquier cambio, asegúrate de que Git está configurado correctamente.

📌 Ejecuta en la terminal (solo la primera vez):

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu_correo@example.com"
```

Ejemplo:

```bash
git config --global user.name "Juan Pérez"
git config --global user.email "juanperez@example.com"
```

Para verificar la configuración:

```bash
git config --list
```

---

## 2️⃣ Ir al directorio del proyecto

📌 Navega hasta la carpeta donde está tu repositorio:

```bash
cd /ruta/del/repositorio
```

Ejemplo:

```bash
cd /home/estudiante/MLOps_2510
```

---

## 3️⃣ Ver el estado del repositorio

Antes de subir los cambios, revisa qué archivos han cambiado:

```bash
git status
```

Si ves archivos en rojo, significa que están modificados o no rastreados.

---

## 4️⃣ Agregar los archivos al área de preparación

📌 Para agregar todos los archivos modificados:

```bash
git add .
```

Si quieres agregar archivos específicos:

```bash
git add nombre_del_archivo
```

---

## 5️⃣ Hacer un commit (guardar cambios localmente)

📌 Escribe un mensaje que describa los cambios:

```bash
git commit -m "Descripción de los cambios"
```

Ejemplo:

```bash
git commit -m "Corrigiendo configuración en docker-compose y agregando Dockerfile"
```

---

## 6️⃣ Obtener los cambios más recientes desde GitHub

Antes de subir los cambios, asegúrate de que tu copia local está actualizada:

```bash
git pull origin main --rebase
```

Si hay conflictos, resuélvelos antes de continuar.

---

## 7️⃣ Subir los cambios a GitHub

📌 Para enviar los cambios al repositorio remoto:

```bash
git push origin main
```

Si usas otra rama (branch), reemplaza `main` por el nombre de la rama.

---

## 8️⃣ Verificar en GitHub

📌 Abre tu navegador y entra a GitHub para verificar que los cambios se reflejaron correctamente en tu repositorio.

---

## 💡 Solución a Errores Comunes

### ❌ Git no reconoce tu usuario

Si aparece el error:

```
Author identity unknown
```

📌 Configura Git con tu usuario:

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu_correo@example.com"
```

---

### ❌ Error: ‘Everything up-to-date’ pero los archivos no aparecen en GitHub

Si Git dice que todo está actualizado pero los cambios no aparecen, intenta:

```bash
git push --force origin main
```

---

### ❌ Error de autenticación (Acceso denegado)

Si Git te pide credenciales y no las acepta:

- Si usas HTTPS, genera un Personal Access Token (PAT) en GitHub y úsalo en lugar de la contraseña.
- Si usas SSH, asegúrate de haber agregado tu clave SSH a GitHub.

---

Con este manual, podrás actualizar tus cambios de local a GitHub de manera eficiente y solucionar problemas comunes durante el proceso. ¡Buena suerte!

