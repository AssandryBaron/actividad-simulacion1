# Actividad de seguimiento - Simulación 1

|Integrante|correo|usuario github|
|---|---|---|
|Assandry Baron Rodriguez|assandry.baron@udea.edu.co|AssandryBaron|
|Huber Steven Arroyave Rojas|huber.arroyave@udea.edu.co|hubersteven|
|John Bayron Quiroz|bayron.quiroz@udea.edu.co|JohnQuiroz|

## Instrucciones

Antes de empezar a realizar esta actividad haga un **fork** de este repositorio y sobre este trabaje en la solución de las preguntas planteadas en la actividad de simulación. Las respuestas deben ser respondidas en español o si lo prefiere en ingles en el lugar señalado para ello (La palabra **answer** muestra donde).

**Importante**:
* Como la actividad es en las parejas del laboratorio, solo uno de los integrantes tiene que hacer el fork; y sobre repositorio bifurcado que se genera, la modificación se realiza en equipo.
* Como la entrega se debe hacer modificando el archivo READNE, se recomienda que consulte mas sobre el lenguaje **Markdown**. En el repo adjuntan dos cheatsheet ([cheat sheet 1](Markdown_Cheat_Sheet.pdf), [cheatsheet 2](markdown-cheatsheet.pdf)) para consulta rapida.
* Entre mas creativo mejor.

## Homework (Simulation)

This program, [`process-run.py`](process-run.py), allows you to see how process states change as programs run and either use the CPU (e.g., perform an add instruction) or do I/O (e.g., send a request to a disk and wait for it to complete). See the [README](https://github.com/remzi-arpacidusseau/ostep-homework/blob/master/cpu-intro/README.md) for details.

### Questions

1. Run `process-run.py` with the following flags: `-l 5:100,5:100`. What should the CPU utilization be (e.g., the percent of time the CPU is in use?) Why do you know this? Use the `-c` and `-p` flags to see if you were right.

   <details>
   <summary>Answer</summary>
    
   ![respuesta_01](https://github.com/user-attachments/assets/05a086a6-ec10-4d80-9c1b-06db07a7dd21)

   Para este caso, esta bandera crea 2 procesos, cada uno con 5 instrucciones, los cuales tienen un 100% de probabilidad de usar la CPU, es decir, que no hay operaciones de I/O.

   La utilización de la CPU es del 100%, ya que como se mencionó anteriormente, los 2 procesos, sólo utilizan la CPU. Cuando un proceso termina con sus 5 instrucciones, el sistema          cambia inmediatamente al otro proceso en espera que en este caso es PID:1. También se puede ver, que la CPU nunca está inactiva, ya que siempre hay un proceso listo para      ejecutarse.

   Al ejecutar con -c y -p, se confirma que el porcentaje de la ocupación de la CPU es del 100% y el tiempo total de la ejecución, sería de 10 unidades de tiempo (5 instrucciones para      cada proceso)

   </details>
   <br>

1. Now run with these flags: `./process-run.py -l 4:100,1:0`. These flags specify one process with 4 instructions (all to use the CPU), and one that simply issues an I/O and waits for it to be done. How long does it take to complete both processes? Use `-c` and `-p` to find out if you were right.

   <details>
   <summary>Answer</summary>
   
   ![respuesta_02](https://github.com/user-attachments/assets/da37a08f-6133-475e-bdae-35870c1531cc)

   En este segundo caso, esta bandera crea un proceso de 4 instrucciones, todas las operaciones de CPU, es decir de una probabilidad de 100% y otro proceso de una instrucción con una       probabilidad de 0% de probabilidad, es decir, es una operación de I/O. 

   El tiempo total de ejecución es de 11 unidades, donde el 54.55% la CPU es ocupada, es decir 6 unidades y las otras 5 unidades, es ocupada por I/O lo que equivale al 45.45%. Ya que el    proceso 0 que es el PID: 0, ejecuta sus 4 instrucciones de CPU del tiempo 1 al 4. Para el tiempo 5 , el proceso 0 finaliza e inicia el proceso 1 con una operación de I/O. Para los       tiempos del 6 al 10, el proceso 1 se encuentra bloqueado, mientras que espera que su operación de I/O se complete. Y por último para el tiempo 11, La operación I/O termina y el          proceso 1 ejecuta su instrucción final
   
   </details>
   <br>

3. Switch the order of the processes: `-l 1:0,4:100`. What happens now? Does switching the order matter? Why? (As always, use `-c` and `-p` to see if you were right)

   <details>
   <summary>Answer</summary>
      
   ![respuesta_03](https://github.com/user-attachments/assets/0328b1f2-15c2-466c-910d-0c50a12cae9d)

   En el tercer caso, que es similar al punto 2 solo que se cambia el orden de los procesos. Se puede ver que es más eficiente, ya que el tiempo total de ejecución, sería de 7 unidades, debido a que se está superponiendo las operaciones de CPU y I/O, para asi mejorar la utilización de los recursos.  
La CPU, se encuentra ocupada durante 6 unidades de tiempo, es decir, 1 instrucción de inicio de I/O del proceso 0, 4 instrucciones del proceso y 1 instrucción de finalización de I/O, representando un 85.71%. Mientras que la I/O está activa durante 5 unidades representando un 71.43%   

   </details>
   <br>

5. We'll now explore some of the other flags. One important flag is `-S`, which determines how the system reacts when a process issues an I/O. With the flag set to SWITCH ON END, the system will NOT switch to another process while one is doing I/O, instead waiting until the process is completely finished. What happens when you run the following two processes (`-l 1:0,4:100 -c -S SWITCH ON END`), one doing I/O and the other doing CPU work?

   <details>
   <summary>Answer</summary>

   ![04_NUEVA](https://github.com/user-attachments/assets/3a3bc3bb-89f5-411f-94bd-5c15670aec83)


   Cuando se utiliza SWITCH_ON_END, el sistema no cambiará de proceso hasta que el que se está ejecutando se complete. Como se puede ver, la CPU permanece inactiva durante los tiempos 2 al 6 mientras que el proceso 0 espera por su operación de I/O, a pesar de que el proceso 1 está listo para ejecutarse, dando como resultado, un uso ineficiente de la CPU, ya que se desperdician 5 unidades de tiempo, los cuales, la CPU podría haber estado trabajando en el proceso 1.

   Analizando el resultado, en el tiempo 1, el proceso 0 ejecuta una operación de I/O. Del 2 al 6, el proceso 0 queda bloqueado mientras que se espera que este, ejecute su I/O, mientras el proceso 1 se mantiene en READY pero no se ejecuta. Para el 7, la operación de I/o del proceso 0 termina y se ejecuta su instrucción final. Para el 8, el proceso 0 finaliza y el proceso 1 comienza a ejecutarse. Por último del tiempo 8 al 11, el proceso 1 ejecuta sus 4 instrucciones de CPU 

   </details>
   <br>

7. Now, run the same processes, but with the switching behavior set to switch to another process whenever one is WAITING for I/O (`-l 1:0,4:100 -c -S SWITCH ON IO`). What happens now? Use `-c` and `-p` to confirm that you are right.

   <details>
   <summary>Answer</summary>
      
   ![respuesta_05](https://github.com/user-attachments/assets/a19276cc-9134-45ef-9b1d-f28ba375e1bc)

   Cuando se utiliza SWITCH_ON_IO el sistema cambia de proceso cuando el proceso actual entra en espera por I/O, evitando que la CPU quede inactiva en operaciones de entrada/salida. Se puede ver que en el tiempo 1, entra el proceso 0 con una operación de I/O y el proceso 1 esta en READY, en el tiempo 2, el proceso 0 pasa a BLOCK e inmediatamente entra el proceso 1 a ejecutarse hasta el tiempo 5, en el tiempo 6 el proceso 1 termina el proceso, por lo cual la CPU queda inactiva una unidad en donde en el tiempo 7 temina la operación de I/O en el proceso 0.
   
   En conclusión, gracias a SWITCH_ON_IO, la CPU mantiene ocupada casi todo el tiempo con un uso de un 85.71% y la I/O estuvo un 71.43% del tiempo, lo cual nos conlleva que el proceso 1 aprovecho bien la CPU, mientras el proceso 0 realizaba una operación I/O.
      
   </details>
   <br>

9. One other important behavior is what to do when an I/O completes. With `-I IO RUN LATER`, when an I/O completes, the process that issued it is not necessarily run right away; rather, whatever was running at the time keeps running. What happens when you run this combination of processes? (`./process-run.py -l 3:0,5:100,5:100,5:100 -S SWITCH ON IO -c -p -I IO RUN LATER`) Are system resources being effectively utilized?

   

   <details>
   <summary>Answer</summary>

   ![06_NUEVA](https://github.com/user-attachments/assets/9764a7d7-5b3d-44b5-b627-0999028ddd74)

   Para el caso 6, el comando IO_RUN_LATER, permite que el proceso actual en CPU continúe ejecutándose cuando una operación de I/O se completa. El proceso que finalizó de I/O no recibe prioridad inmediata, lo que permite reducir los cambios de contexto, pero puede generar ineficiencias.
De acuerdo a la simulación, se puede ver que el comando crea 4 procesos. El proceso 0 de operaciones de I/O y los procesos 1, 2 y 3, cada uno con 5 operaciones de CPU.
En la ejecución, en el tiempo 1, el proceso 0 comienza su primera operación I/O. En los tiempos 2 hasta el 6, mientras que el proceso 0 está bloqueado, el sistema cambia al proceso 1 que ejecuta sus 5 instrucciones de CPU. Para los tiempos 7 al 11, el proceso 2 ejecuta sus 5 instrucciones de CPU. Del 12 al 16, se ejecutan las 5 operaciones del proceso 3. En el 17 la primera I/O del proceso 0 finaliza y ejecuta io_done. En el 18 el proceso 0 inicia su segunda operación de I/O. Del 19 al 23 el proceso permanece bloqueado, pero ya no hay otros procesos para ejecutar en la CPU. En el tiempo 24, la segunda I/O finaliza y ejecuta io_done. Para el 25 el proceso 0 inicia con su tercera operación de I/O. Para los tiempos 26 al 30, el proceso 0 permanece bloqueado mientras que la CPU está inactiva y por último en el tiempo 31, la tercera I/O finaliza, se ejecuta io-done y se terminan todos los procesos.

   Analizando todo lo anterior, se puede evidenciar de que los recursos no se utilizan de una manera eficiente ya que IO_RUN_LATER ocasiona que a pesar de que en los tiempos del 1 al 16 hay un uso eficiente de los recursos, para los otros tiempos, es decir del 17 al 31, la CPU permanece completamente inactiva durante largos periodos mientras el proceso 0, espera que sus operaciones de I/O terminen.
La estadísticas finales son de 31 unidades de tiempo total, donde hay 21 unidades ocupada por la CPU representando el 67.74% y 15 unidades, que representa el 48.39% ocupadas por I/O


   </details>
   <br>

11. Now run the same processes, but with `-I IO RUN IMMEDIATE` set, which immediately runs the process that issued the I/O. How does this behavior differ? Why might running a process that just completed an I/O again be a good idea?

   

   <details>
   <summary>Answer</summary>

   ![07_NUEVA](https://github.com/user-attachments/assets/7ad8dc2d-1add-4119-906b-f093b1839d02)

   
   </details>
   <br>


### Criterios de evaluación
- [x] Despligue de los resultados y analisis claro de los resultados respecto a lo visto en la teoria.
- [x] Creatividad y orden.
