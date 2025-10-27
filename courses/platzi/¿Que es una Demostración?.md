::: center
**¿Como nacen las formulas en las matemáticas?**
:::

En el colegio e incluso en la universidad, nos enseñan a memorizar
ciertas formulas de las matemáticas y algoritmos tales como:

$$\frac{a}{b}+\frac{c}{d}=\frac{a \cdot d + b \cdot c}{b \cdot d}$$

Pero, sabes el ¿por que? ¿por que esto es verdad? Bueno en matemáticas a
las verdades absolutas es decir algo que siempre es verdad pasé lo que
pase lo llamamos teoremas, y concluimos que son verdaderas siempre que
exista una Demostración. Una Demostración es una serie de pasos que nos
permite concluir que cierta proposición es verdadera.\
\
Ahora bien **¿Como hacemos para Demostrar el Teorema aquí expuesto?**
bien en matemática existe algo llamado **Axiomas de campo**, calma por
definición un axioma es una proposición o Enunciado tan evidente que se
considera que no requiere Demostración. Y un cuerpo es simplemente un
sistema algebraico en donde existe la multiplicación y la adicción. Un
ejemplo seria los naturales $\{0,1,2,3,4...\}$ pues sus elementos se
pueden sumar y multiplicar entre si.\
\
Explicado lo anterior vamos a enunciar los axiomas de campo:

1.  Para todo a,b que pertenecen a $\mathbb R$ (los Números Reales de
    toda la vida) se tiene: $a + b = b + a$, y $a \cdot b = b \cdot a$.

2.  para todo a,b,c en $\mathbb R$ se tiene que: $(a+b)+c = c+(a+b)$ y
    $a \cdot (b \cdot c)= (a \cdot b) \cdot c$

3.  Para todo a,b,c en $\mathbb R$ se tiene que:
    $(a + b) \cdot c = a \cdot c + b \cdot c$

4.  Existen elementos 0 y 1 en $\mathbb{R}$ tales que $0 \not = 1$ y
    para cualquier a en $\mathbb R$ se cumple que $x + 0 = 0 + x = x$ y
    $x \cdot 1 = 1 \cdot x = x.$

5.  Para cualquier a en $\mathbb R$ existe un -a, talque $a+(-a)=0$

6.  Para cualquier a en $\mathbb R$ existe un $\frac{1}{a}$ talque
    $a \cdot \frac{1}{a} = 1$ con $a \not = 0$ recordemos que a no puede
    ser igual a 0, porque si a = 0 entonces $\frac{1}{a}$ daría
    indeterminado, es decir su resultado es desconocido.

Ahora enunciemos un **Lema**, un lema es un teorema pero anteriormente
se hizo la demostración.\
\
**Lema** $\frac{a}{b}\cdot b \cdot d = a \cdot d$ y
$\frac{c}{d} \cdot b \cdot d = c \cdot d$ para cualesquiera a,b,c,d en
$\mathbb R$ con $b \not = 0$ y $d \not = 0$. (un consejo para demostrar
este lema sera usando los axiomas 2,1, 6 y 4)\
\
Bueno sin más vueltas al asunto enunciemos formalmente y demostremos el
teorema expuesto al principio de este blog\
\
**Teorema**: si a,b,c,d están en $\mathbb R$, con $b \not = 0$ y
$d \not = 0$ entonces
$\frac{a}{b}+\frac{c}{d}=\frac{a \cdot d + b \cdot c}{b \cdot d}$\
\
**Demostración** es claro que $b \cdot d \not = 0$ puesto que
$b \not = 0$ y $d \not = 0$.\
\
Vamos a comenzar del lado izquierdo de la ecuación y trataremos de
llegar al lado derecho es decir de $\frac{a}{b}+\frac{c}{d}$ llegaremos
a $\frac{a \cdot d + b \cdot c}{b \cdot d}$\
\
Tenemos que $\frac{a}{b}+\frac{c}{d}= \frac{a}{b}+\frac{c}{d} \cdot 1$
esto por el axioma 4.\
\
Y tenemos que $1 = b \cdot d \cdot \frac{1}{b \cdot d}$ esto por axioma
6. Por ende reemplazando el 1 en el paso anterior tenemos
$\frac{a}{b}+\frac{c}{d}= \frac{a}{b}+\frac{c}{d} \cdot (b \cdot d \cdot \frac{1}{b \cdot d})$\
\
Ahora por el axioma 2 podemos hacer
$(\frac{a}{b}+\frac{c}{d} \cdot b \cdot d )\cdot \frac{1}{b \cdot d}$\
\
Por el axioma 3 podemos
$(\frac{a}{b}\cdot b \cdot d + \frac{c}{d} \cdot b \cdot d) \cdot \frac{1}{b \cdot d}$\
\
Por lo tanto tenemos que
$(a \cdot d + c \cdot b) \cdot \frac{1}{b \cdot d}$ y listo simplemente
organizando tenemos que $\frac{(a \cdot d + c \cdot b)}{b \cdot d}$ y
concluimos que
$\frac{a}{b}+\frac{c}{d}=\frac{a \cdot d + b \cdot c}{b \cdot d}$ que es
lo que queríamos demostrar.\
\

::: center
**Conclusiónes**
:::

1.  Todo lo que sea verdad en matemáticas o bien es un axioma o se
    demuestra a partir de axiomas. Podríamos decir que un axioma es como
    una semilla de un árbol, es algo pequeño pero a partir de ella nace
    la teoría que conocemos.

2.  Si piensas que las matemáticas no son para ti o que no te gustan o
    que simplemente no se te dan, tal vez sea la forma como te enseñaron
    las matemáticas. Las matemáticas pueden ser mucho más didácticas y
    divertidas de lo que pueden aparentar a simple vista, solo basta con
    mirarlas diferente

Por último quiero dejarte dos retos el primero es que demuestres el lema
utilizado en la Demostración y el otro es que nunca pares de aprender.
Si tienes dudas escríbeme un comentario en este blog o escríbeme a mí
Twitter \@WilsonJerez estaré feliz de resolver tus dudas.
