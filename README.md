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

   ![respuesta_01](https://github.com/user-attachments/assets/05a086a6-ec10-4d80-9c1b-06db07a7dd21)

   <details>
   <summary>Answer</summary>
   
Para este caso, esta bandera crea 2 procesos, cada uno con 5 instrucciones, los cuales tienen un 100% de probabilidad de usar la CPU, es decir, que no hay operaciones de E/S.

La utilización de la CPU es del 100%, ya que como se mencionó anteriormente, los 2 procesos, sólo utilizan la CPU. Cuando un proceso termina con sus 5 instrucciones, el sistema cambia inmediatamente al otro proceso en espera que en este caso es PID:1, por lo cual, también podemos ver que la CPU nunca está inactiva, ya que siempre hay un proceso listo para ejecutarse.

Al ejecutar con -c y -p, se confirma que el porcentaje de la ocupación de la CPU es del 100% y el tiempo total de la ejecución, sería de 10 unidades de tiempo (5 instrucciones para cada proceso)

   </details>
   <br>

2. Now run with these flags: `./process-run.py -l 4:100,1:0`. These flags specify one process with 4 instructions (all to use the CPU), and one that simply issues an I/O and waits for it to be done. How long does it take to complete both processes? Use `-c` and `-p` to find out if you were right.

   ![respuesta_02](https://github.com/user-attachments/assets/da37a08f-6133-475e-bdae-35870c1531cc)
   
   <details>
   <summary>Answer</summary>
   Coloque aqui su respuerta
   </details>
   <br>

3. Switch the order of the processes: `-l 1:0,4:100`. What happens now? Does switching the order matter? Why? (As always, use `-c` and `-p` to see if you were right)

   ![respuesta_03](https://github.com/user-attachments/assets/0328b1f2-15c2-466c-910d-0c50a12cae9d)

   <details>
   <summary>Answer</summary>
   Coloque aqui su respuerta
   </details>
   <br>

4. We'll now explore some of the other flags. One important flag is `-S`, which determines how the system reacts when a process issues an I/O. With the flag set to SWITCH ON END, the system will NOT switch to another process while one is doing I/O, instead waiting until the process is completely finished. What happens when you run the following two processes (`-l 1:0,4:100 -c -S SWITCH ON END`), one doing I/O and the other doing CPU work?

   ![respuesta_04](https://github.com/user-attachments/assets/5f81e10a-7468-4b98-8624-0e18ec3dacc8)

   <details>
   <summary>Answer</summary>
   Coloque aqui su respuerta
   </details>
   <br>

5. Now, run the same processes, but with the switching behavior set to switch to another process whenever one is WAITING for I/O (`-l 1:0,4:100 -c -S SWITCH ON IO`). What happens now? Use `-c` and `-p` to confirm that you are right.

   ![respuesta_05](https://github.com/user-attachments/assets/a19276cc-9134-45ef-9b1d-f28ba375e1bc)

   <details>
   <summary>Answer</summary>
   Coloque aqui su respuerta
   </details>
   <br>

6. One other important behavior is what to do when an I/O completes. With `-I IO RUN LATER`, when an I/O completes, the process that issued it is not necessarily run right away; rather, whatever was running at the time keeps running. What happens when you run this combination of processes? (`./process-run.py -l 3:0,5:100,5:100,5:100 -S SWITCH ON IO -c -p -I IO RUN LATER`) Are system resources being effectively utilized?

   ![respuesta_06](https://github.com/user-attachments/assets/34b7f128-12fe-46a2-8b98-1cd0c53d4c01)

   <details>
   <summary>Answer</summary>
   Coloque aqui su respuerta
   </details>
   <br>

7. Now run the same processes, but with `-I IO RUN IMMEDIATE` set, which immediately runs the process that issued the I/O. How does this behavior differ? Why might running a process that just completed an I/O again be a good idea?

   ![respuesta_07](https://github.com/user-attachments/assets/a35fabb5-103b-4766-ac91-81f0f76d493d)

   <details>
   <summary>Answer</summary>
   Coloque aqui su respuerta
   </details>
   <br>


### Criterios de evaluación
- [x] Despligue de los resultados y analisis claro de los resultados respecto a lo visto en la teoria.
- [x] Creatividad y orden.
