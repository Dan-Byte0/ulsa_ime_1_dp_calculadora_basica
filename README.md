# Práctica 4: Calculadora básica

> **Las secciones 1 a 6 ya están resueltas por el profesor.** Léelas con atención, pero no las modifiques. Tu trabajo empieza en la sección 7.

## 1. Descripción del problema (Fase 1, resuelta)

El programa muestra un menú con cuatro operaciones (suma, resta, multiplicación y división). El usuario elige una, escribe dos números y el programa muestra el resultado de la operación. Es la base de cualquier calculadora y del tipo de menú que se usa, por ejemplo, en el panel de control de una máquina.

## 2. Entradas y salidas (Fase 1, resuelta)

**Entradas:**
1. `opcion` (`int`): la operación elegida, de 1 a 4. Se lee con `leerEntero`.
2. `a` (`double`): el primer número. Se lee con `leerDecimal`.
3. `b` (`double`): el segundo número. Se lee con `leerDecimal`.

**Salidas:**
1. `resultado` (`double`): el resultado de la operación.
2. Se muestra en la forma `a símbolo b = resultado`, por ejemplo `7 / 2 = 3.5`. El símbolo se guarda en `simbolo` (`char`).

**Operaciones:** 1) `a + b`   2) `a - b`   3) `a * b`   4) `a / b`

## 3. Restricciones e invariante (Fases 1 y 2, resuelta)

**Restricciones:**
- La opción debe estar entre 1 y 4. Si no, el programa la vuelve a pedir.
- Si la operación es división, `b` no puede ser 0. Si lo es, el programa vuelve a pedir solo `b`.
- En la resta y en la división el orden importa: siempre se calcula `a` op `b`.

**¿Quién detecta cada error?**
- `leerEntero` y `leerDecimal` detectan el **formato**: texto (`abc`) o, en el caso de `leerEntero`, decimales (`2.5`).
- El programa detecta el **rango**: una opción fuera de 1 a 4 y un divisor igual a 0.

**Invariante:** al llegar al Paso 7 (el cálculo), `opcion` está entre 1 y 4 y, si la opción es 4 (división), `b` es distinto de 0. Por eso el cálculo siempre es válido.

## 4. Casos resueltos a mano (Fase 1, resuelta)

| Caso | Opción | a | b | Resultado |
|---|---|---|---|---|
| 1 | 1 (suma) | 8 | 5 | 8 + 5 = 13 |
| 2 | 2 (resta) | 3 | 5 | 3 - 5 = -2 |
| 3 | 3 (multiplicación) | 2.5 | 4 | 2.5 * 4 = 10 |
| 4 | 4 (división) | 7 | 2 | 7 / 2 = 3.5 |
| 5 | 4 (división) | 5 | 0, luego 2 | vuelve a pedir `b`; 5 / 2 = 2.5 |

## 5. Receta en pseudocódigo (Fase 2, resuelta)

La receta completa está en el archivo `RECETA.md`. No la modifiques: si encuentras algo que no contempla, anótalo en la sección 11.

## 6. Cómo compilar y ejecutar (Fase 3)

```bash
g++ -Wall -Wextra -std=c++17 main.cpp -o calculadora
./calculadora
```

## 7. Ejemplo de ejecución (Fase 3)
<!-- Pega aquí lo que muestra tu programa en pantalla con una división donde primero escribes 0 como segundo número. -->

```
Calculadora basica
1) Suma
2) Resta
3) Multiplicacion
4) Division
Elige una opcion (1-4): 4
Primer numero: 5
Segundo numero: 0
No se puede dividir entre cero
Segundo numero (distinto de 0):2
5 / 2 = 2.5
```

## 8. De la receta al código (Fase 3)
<!-- Para cada paso de la receta, escribe la instrucción (o instrucciones) de C++ que lo implementa. -->

| Paso de la receta | Instrucción de C++ que lo implementa |
|---|---|
| 1 y 2. Título y menú | __std:: cout___ |
| 3. Leer y validar la opción | __leerEntero___ |
| 4 y 5. Leer `a` y `b` | __leerDecimal___ |
| 6. Validar el divisor | __if (opcion == 4 ) while ( b == 0)___ |
| 7. Decisión múltiple (un `case`) | __case 1: y break;___ |
| 8. Mostrar el resultado | __el std:: cout final con a, simbolo, b y resultado___ |

**¿Hubo algún paso de la receta que te costó traducir a C++? ¿Cuál y por qué?**
__Si, el 6 fue el mas complicado para mi porque no lograba entender el como escribirlo.___

## 9. Experimentos (Fase 3)

**Experimento A: sin el `break` del `case 1`, ¿qué mostró el programa con 8 + 5? ¿Qué te dijo el compilador? ¿Por qué pasó?**
__Me mostro una resta, dandome de resultado 3, el compilador no me dijo nada, solo paso al caso 2, como no break paso de largo directamente al mas cercano que fue el caso 2___

**Experimento B: sin la validación del Paso 6, ¿qué mostró el programa con 5 / 0? ¿Tiene sentido?**
__Mostro algo llamado inf, representa infinito, no tiene sentido porque dividir entre 0 no tiene resultado valido y C++ no aviso___

**Experimento C (opcional): con `a` y `b` de tipo `int`, ¿qué resultado dio 7 / 2? ¿Te avisó el compilador?**
___No realizado__

## 10. Tabla de pruebas (Fase 4)

| Caso | Entradas (opción, a, b) | Esperado | Obtenido | ¿Pasó? |
|---|---|---|---|---|
| Suma | 1, 8, 5 | 8 + 5 = 13 | __13___ | __Paso sin problema___ |
| Resta negativa | 2, 3, 5 | 3 - 5 = -2 | __-2___ | __Paso sin problema___ |
| Multiplicación con decimales | 3, 2.5, 4 | 2.5 * 4 = 10 | __10___ | ___Paso sin problema__ |
| Multiplicación con negativo | 3, -3, 4 | -3 * 4 = -12 | ___-12__ | __Paso sin problema___ |
| División | 4, 7, 2 | 7 / 2 = 3.5 | __3.5___ | __Paso sin problema___ |
| Dividendo cero | 4, 0, 5 | 0 / 5 = 0 | ___0__ | _Paso sin problema____ |
| Divisor cero | 4, 5, 0 (luego 2) | vuelve a pedir `b`; 5 / 2 = 2.5 | __2.5___ | __Resultado esperado___ |
| Suma con cero | 1, 5, 0 | 5 + 0 = 5 (**no** vuelve a pedir `b`) | __5___ | __Resultado esperado___ |
| Opción fuera de rango | 5 (luego 1), 8, 5 | vuelve a pedir la opción; 8 + 5 = 13 | ___13__ | ___Resultado esperado__ |
| Opción cero | 0 (luego 1), 8, 5 | vuelve a pedir la opción; 8 + 5 = 13 | ___13__ | __Paso sin problema___ |
| Opción decimal | 2.5 (luego 2), 3, 5 | `leerEntero` vuelve a pedir; 3 - 5 = -2 | ____-2_ | __Resultado esperado___ |
| Opción con texto | `suma` (luego 1), 8, 5 | `leerEntero` vuelve a pedir; 8 + 5 = 13 | __13___ | ___Resultado esperado__ |
| Número con texto | 1, `abc` (luego 8), 5 | `leerDecimal` vuelve a pedir; 8 + 5 = 13 | __13___ | __Resultado esperado___ |
| Caso propio 1 | __3,5,1___ | __5 x 1 = 5___ | ___5__ | __Paso sin problema___ |
| Caso propio 2 | __2,1,1___ | ___1 - 1 = 0__ | __0___ | ___Paso sin problema__ |

## 11. Bitácora de mejoras (Fase 4)

| # | ¿Qué falló o qué quise mejorar? | ¿Qué cambié? | ¿Funcionó? |
|---|---|---|---|
| 1 | __Falle al anotar o no respetar espacios y signos___ | __Los corregi___ | ___Si__ |
| 2 | __No anote el while correctamente___ | __Lo revise y cambie completamente como estaba___ | ___Si__ |

**¿Encontré algo que la receta no contemplaba? ¿Qué?**
__No___

**Reto elegido (opcional):** ___Ninguno__

## 12. Dudas para el profesor (Fase 3)

| Duda | Lo que ya intenté |
|---|---|
| ___Ninguna que no haya podido investigar y resolver__ | __Todo en orden___ |

## 13. Reflexión final

**¿Qué aprendí con esta práctica?**
__Aprendi mas sobre switch, el como tener opciones en mis programas___

**Ahora que terminé, ¿qué cambiaría de mi proceso?**
___Nada__

**¿Qué fue lo más difícil y cómo lo resolví?**
___Fue anotar el paso 6, no sabia donde ponerlo ni como, lo mismo con el switch__

**¿Qué pregunta me quedó sin responder?**
___Ninguna__

**¿Fue más fácil programar a partir de una receta ajena que de la mía? ¿Por qué?**
__Si, porque esta receta nos ayuda, porque por ejemplo en mi caso estoy aprendiendo poco a poco sobre programas y tener un repositorio asi , no en blanco, si me ayuda.___

**Si yo hubiera diseñado la receta, ¿qué le cambiaría?**
___Nada que se me ocurra__

## 14. Lista de verificación antes de entregar (Fase 5)

- [x] Llené las secciones 7 a 13 (no quedan `_____`)
- [x ] No modifiqué las secciones 1 a 6 ni la receta de `RECETA.md`
- [x ] Cada bloque de `main.cpp` tiene su comentario `// Paso N`
- [x ] Mi programa compila sin advertencias
- [x ] Probé todos los casos de la tabla
- [x ] Hice los Experimentos A y B y dejé el código correcto al terminar
- [x ] No modifiqué `utilerias.h`
- [x ] Hice al menos 4 commits con mensajes claros
- [x ] Hice `git push` y verifiqué mi fork en GitHub
- [x ] Entregué el enlace de mi fork en Classroom