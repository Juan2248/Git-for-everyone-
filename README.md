# ■■■ Guía práctica de Git para proyectos de IA con Python y TensorFlow
Bienvenido ■ Este repositorio es una **guía práctica** para aprender y aplicar **Git** en proyectos de
**Inteligencia Artificial (IA) con Python/TensorFlow**.
Aquí encontrarás **instrucciones, ejemplos, trucos y buenas prácticas** que podrás aplicar directamente en tus
propios proyectos.
---
## ■ ¿Qué es Git y por qué usarlo en IA?
Git es un **sistema de control de versiones** que permite:
- Guardar y recuperar versiones de tu proyecto.
- Trabajar en equipo sin perder cambios.
- Probar diferentes experimentos de IA en ramas separadas.
- Colaborar usando GitHub/GitLab.
En proyectos de **IA** esto es clave porque:
- Los modelos y datasets son pesados.
- Necesitamos versionar código, configuraciones y experimentos.
- Queremos evitar subir modelos/datos grandes directamente.
---
## ■■ Configuración inicial de Git
Configura tu usuario y correo antes de empezar:
```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tuemail@example.com"
git config --list
```
---
## ■ Estructura recomendada para proyectos IA
```
mi_proyecto_ia/
■■ data/ # datos (NO versionar)
■■ notebooks/ # Jupyter notebooks
■■ src/
■ ■■ train.py # script de entrenamiento
■ ■■ model.py # definición de la red
■ ■■ utils.py # utilidades
■■ models/ # checkpoints (usar Git LFS o ignorar)
■■ requirements.txt # dependencias
■■ .gitignore
■■ README.md
```
---
## ■ Archivo `.gitignore` recomendado
Ejemplo para Python + TensorFlow:
```
# Entornos virtuales
venv/
.env
# Python
__pycache__/
*.py[cod]
# Jupyter
.ipynb_checkpoints
# Modelos y datasets
models/
*.h5
*.hdf5
*.pb
*.ckpt*
data/
# Logs de entrenamiento
logs/
events.out.tfevents.*
```
---
## ■ Comandos básicos de Git con ejemplos
### 1■■ Inicializar repositorio
```bash
git init
```
### 2■■ Ver estado
```bash
git status
```
### 3■■ Agregar y confirmar cambios
```bash
git add archivo.py
git add .
git commit -m "Primer commit: estructura inicial"
```
### 4■■ Ver historial
```bash
git log --oneline --graph --all
```
### 5■■ Ramas (experimentos)
```bash
git branch experiment/cnn
git switch experiment/cnn
```
### 6■■ Resetear commits
```bash
git reset --soft HEAD~1 # deshacer commit, mantener cambios
git reset --hard HEAD~1 # borrar commit y cambios
```
### 7■■ Conectar con remoto
```bash
git remote add origin https://github.com/usuario/proyecto.git
git push origin main
git pull origin main
```
---
## ■ Ejemplo en TensorFlow
`src/model.py`
```python
import tensorflow as tf
def create_model():
model = tf.keras.Sequential([
tf.keras.layers.Flatten(input_shape=(28, 28)),
tf.keras.layers.Dense(128, activation='relu'),
tf.keras.layers.Dense(10, activation='softmax')
])
model.compile(optimizer='adam',
loss='sparse_categorical_crossentropy',
metrics=['accuracy'])
return model
```
`src/train.py`
```python
import tensorflow as tf
from model import create_model
def main():
(x_train, y_train), (x_test, y_test) = tf.keras.datasets.mnist.load_data()
x_train, x_test = x_train / 255.0, x_test / 255.0
model = create_model()
model.fit(x_train, y_train, epochs=3, validation_data=(x_test, y_test))
model.save("models/mnist_model.h5")
if __name__ == "__main__":
main()
```
---
## ■■ Trucos y Alias útiles
Agrega alias para ahorrar tiempo:
```bash
git config --global alias.st status
git config --global alias.cm "commit -m"
git config --global alias.lg "log --oneline --graph --all"
```
Ahora puedes usar:
```bash
git st
git cm "mensaje"
git lg
```
---
## ■ Manejo de modelos grandes (Git LFS)
TensorFlow produce archivos pesados (`.h5`, `.pb`, `.ckpt`).
No los subas directamente → usa **Git LFS**:
```bash
git lfs install
git lfs track "*.h5"
git lfs track "*.ckpt"
git add .gitattributes
git commit -m "Configurar Git LFS para modelos"
```
---
## ■ Buenas prácticas en proyectos IA con Git
✔■ **Versiona solo código y configs** (no datasets completos ni modelos pesados).
✔■ Usa **ramas** para cada experimento:
```bash
git checkout -b experiment/dropout-0.5
```
✔■ Escribe *commits pequeños y descriptivos*.
✔■ Documenta resultados en `experiments/exp1-notas.md`.
✔■ Usa `requirements.txt` o `environment.yml` para dependencias.
✔■ Automatiza con `Makefile` o scripts (`run_train.sh`).
✔■ Colabora con **Pull Requests** para revisar cambios antes de mezclar.
---
## ■ Recursos recomendados
- [Cheat Sheet de Git (GitHub, en español)](https://training.github.com/downloads/es_ES/github-git-cheat-sheet.pdf)
- [Visualización interactiva de ramas](https://learngitbranching.js.org/?locale=es_ES)
- [Guía oficial de Git LFS](https://git-lfs.com/)
- [TensorFlow Documentation](https://www.tensorflow.org/)
---
✍■ Autor: **[Tu Nombre]**
■ Proyecto educativo – Git + Python + TensorFlow
