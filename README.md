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

