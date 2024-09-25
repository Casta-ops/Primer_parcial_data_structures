# Primer_parcial_data_structures

# Pregunta 1

La clase vector implementa lo que se conoce como un arreglo dinámico. Es decir, en parte
se comporta como un arreglo pero extiende la funcionalidad de los arreglos permitiendo que la
estructura de datos crezca o se contraiga de acuerdo a su uso. Responda las siguientes
preguntas respecto a la estructura de datos vector.

1. Por qué es necesario hacer resize del vector cuando este se llena y es necesario seguir
almacenando elementos?. A caso no sería una mejor opción apartar un espacio en
memoria para seguir almacenando los elementos que se van a insertar en el futuro así se
deba llevar registro dentro de la clase de que los elementos del vector pueden estar
almacenados en diferentes lugares de la memoria?

RE // Esto se debe a que la estructura Vector implementa los elementos de su arreglo de
manera consecutiva en la memoria, hacer resize es fundamental para poder seguir con su
proceso, ya que todo aquel elemento que se aloje por fuera de la capacidad del arreglo se
puede llegar a perder en la memoria, por lo tanto el arreglo no llegaria a conocer su posición,
si deseamos utilizar distintos espacios en la memoria, en ese caso lo mas factible sería 
utilizar listas. Las listas nos permiten utilizar nodos a diferentes lugares de la memoria sin perder
o desconocer la ubicación de cada elemento dentro de la estructura.

2. Si comparamos el vector con una lista enlazada como la implementada en el curso cree
usted que la lista pueda ser más eficiente?. Justifique su respuesta.

RE // Depende de las necesidades que tengamos, realmente esa respuesta se encuentra conforme a los aspectos
y condiciones que tengamos a la hora de programar. Mientras que los Vectores nos facilitan el ordenamiento 
de la estructura, las Listas nos permiten controlar de manera mas factible los elementos en relación 
a su remoción e introducción, ya que no es necesario hacer un resize cada vez que se introducen nuevos elementos,
solo es imperativo incrementar su tamaño.

# Pregunta 2

