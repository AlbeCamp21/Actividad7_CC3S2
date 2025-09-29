# Actividad7_CC3S2

## **Ejercicios guiados**

#### **A) Evitar (o no) `--ff`**

![evidencias/capturas/eg_01.png](evidencias/capturas/eg_01.png)

- **Pregunta:** ¿Cuándo evitarías `--ff` en un equipo y por qué?

    Se evitaría usar `--ff` cuando se trabaja en equipo y se quiere mantener un historial de commits bien detallado, para ver los momentos donde se han fusionado ciertas ramas.

#### **B) Trabajo en equipo con `--no-ff`**

![evidencias/capturas/eg_02.png](evidencias/capturas/eg_02.png)

- **Pregunta:** ¿Qué ventajas de trazabilidad aporta? ¿Qué problemas surgen con exceso de merges?

    Cuanda se trabaja de forma paralela en dos ramas y se quiere fusionar los cambios hechos en dichas ramas a la rama principal, cada `merge` creará un commit de la fusión. La ventaja es que se podría visualizar de manera clara donde comenzó y terminó cada trabajo, sobretodo ver los commits pertenecen a cada rama. Ahora, el exceso de merges podría llenar el historial de commits con varios commits de `merge`, haciendo difícil ver el historial.

#### **C) Squash con muchos commits**

![evidencias/capturas/eg_03.png](evidencias/capturas/eg_03.png)

- **Pregunta:** ¿Cuándo conviene? ¿Qué se pierde respecto a merges estándar?

    La opción `--squash` conviene usar cuando se hacen varios commits en un rama, donde los cambios no son tan grandes o no aportan tanto al historial de commits general, todo esto con el fin de mantener el historial de commits limpio. Sin embargo, aplicar esta opción puede hacer perder información importante para el desarrollo ya que se dificultaría el rastreo de cambios específicos.

---

### **Conflictos reales con no-fast-forward**

![evidencias/capturas/eg_04.png](evidencias/capturas/eg_04.png)

**Preguntas:**

- ¿Qué pasos adicionales hiciste para resolverlo?  
Debido a la aparición del conflicto en la misma linea del archivo, se tuvo que solucionar manualmente el conflicto. En este caso se usó `nano` para editarlo directamente y se optó por mantener los dos cambios hechos: en `main` y en `feature-update`.
- ¿Qué prácticas (convenciones, PRs pequeñas, tests) lo evitarían?  
Para evitar estos conflictos podría ser una buena opción trabajar en diferentes archivos, optar por la comunicación en el equipo o unir los cambios con más frecuencia.

---

### **Comparar historiales tras cada método**

![evidencias/capturas/eg_05.png](evidencias/capturas/eg_05.png)

**Preguntas**

- ¿Cómo se ve el DAG en cada caso?
    - Con `--first-parent`:  
El grafo se ve como una sola línea principal que sigue el historial de la rama `master`, mostrando solo los commits que están de forma directa, sin mostrar los detalles de las ramas fusionadas.
    - Con `--merges`:  
El grafo muestra únicamente los commits de tipo merge. En este caso, aparece solo el commit de la fusión de `feature-update` a `master`.
    - Con `--all`:  
El grafo muestra todo el historial, incluyendo las ramas y sus commits individuales. Se puede ver que `feature-update` tiene un commit propio y luego fue fusionado a `master`.

- ¿Qué método prefieres para: trabajo individual, equipo grande, repos con auditoría
    - Trabajo individual:  
Prefiero `--all` porque permite ver todo el historial y no se pierde detalles de los commits realizados en ramas secundarias.
    - Equipo grande:  
Prefiero `--first-parent` ya que simplifica la visualización del historial principal y reduce la confusión con varias ramas activas.
    - Repos con auditoría estricta:  
Prefiero `--merges` porque resalta las fusiones y facilita la revisión de cuándo y cómo se añadieron cambios de ramas secundarias.

---

### **Revertir una fusión (solo si HEAD es un merge commit)**

![evidencias/capturas/eg_06.png](evidencias/capturas/eg_06.png)

**Preguntas**

- ¿Cuándo usar `git revert` en vez de `git reset`?  
Se usa `git revert` cuando se quiera deshacer de un cambio pero sin borrar información del historial de commits. Este comando crea un nuevo commit que revierte lo anterior. Por otro lado, `git reset` mueve la rama a un punto anterior y puede borrar los commits.

- ¿Impacto en un repo compartido con historial público?  
Si se usa `git reset` en un repo compartido, se puede alterar el historial de los demás trabajos y ocasionar conflictos. Ahora, `git revert` es más seguro porque mantiene el historial de commits visible y solamente agrega un commit que revierte los cambios, sin afectar a los demás miembros del equipo.

---

## **Variantes útiles para DevOps/DevSecOps**

#### **A) Fast-Forward Only (merge seguro)**

![evidencias/capturas/eg_07.png](evidencias/capturas/eg_07.png)

#### **B) Rebase + FF (historial lineal con PRs)**

![evidencias/capturas/eg_08.png](evidencias/capturas/eg_08.png)

#### **C) Merge con validación previa (sin commitear)**

![evidencias/capturas/eg_09.png](evidencias/capturas/eg_09.png)

#### **D) Octopus Merge (varias ramas a la vez)**

![evidencias/capturas/eg_10.png](evidencias/capturas/eg_10.png)

#### **E) Subtree (integrar subproyecto conservando gistorial)**

![evidencias/capturas/eg_11.png](evidencias/capturas/eg_11.png)

#### **F) Sesgos y resolución y normalización (algoritmo ORT)**

![evidencias/capturas/eg_12.png](evidencias/capturas/eg_12.png)

En este caso utilicé la opción `git merge -X ours feature-x`.  
Esta opción consiste que, en caso de conflicto, priorice siempre los cambios de la rama actual e ignore los cambios que vienen de la rama que se está fusionando (`feature-x`).  

Caso contrario con `-X theirs`, que mantiene los cambios de la rama que se está fusionando (`feature-x`).
