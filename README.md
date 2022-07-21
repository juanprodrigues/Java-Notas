# Java-Notas
# Temas
### Genéricos y Colecciones
### Threads
### Corrientes de E/S
- Argumentos desde la línea de comando
- Propiedades del sistema
- Fundamentos de las E/S
- Salidas por consola
- Escribiendo en el estándar output
- Leyendo del estándar input
- ¿Qué es una ruta? (Y otros datos del sistema de archivos)
- Creación de un objeto del tipo File
- E/S de Corrientes de Archivos
- Clases básicas previas a la versión 7 para el manejo de corrientes
- Corrientes clásicas
- Corrientes Nodales
- Decoración de corrientes de E/S
- Creando Archivos de Acceso Aleatorio
- Serialización
- Extensión del manejo de excepciones

#### Argumentos desde la línea de comando
Una aplicación puede recibir valores en formato de caracteres desde el sistema operativo. Estos valores se los denomina “argumentos desde la línea de comandos”, puesto que es el intérprete de comandos el encargado de pasarlos a la aplicación.

En el caso de Java, es la máquina virtual la que interacciona con el sistema operativo, sin embargo, a través de ella se pueden recibir dichos argumentos porque el espacio virtual de ejecución que genera emula esta interacción.

Los puede utilizar cualquier aplicación Java siempre y cuando respete el formato definido para pasar los mismos.
Cada argumento de la línea de comando se coloca en el vector args y es pasado a main:

```java
public static void main(String[] args) 
```

Los argumentos, se colocan en la línea de comando cuando se invoca al intérprete luego del
nombre de la clase:

```java
java TestArgs arg1 arg2 "otro arg"
```


El Código 9-1 muestra cómo una vez que se pasan los argumentos por línea de comandos se utiliza el vector args para procesarlos.

##### Código 9-1: Procesamiento de argumentos recibidos por línea de comandos
```java
package consola;

public class VerificarArgumentos {
        public static void main(String[] args) {
                for (int i = 0; i < args.length; i++) {
                        System.out.println("El argumento[" + i + "] es: " + args[i]);
                }
        }
}
```
Se obtiene la salida que se muestra en el Listado 9-1.

##### Listado 9-1: Salida por consola del programa
```java
El argumento[0] es: arg1
El argumento[1] es: arg2
El argumento[2] es: otro arg
```

### Propiedades del sistema
Como la máquina virtual genera su propio espacio de ejecución para las aplicaciones, existen una serie de valores de entorno para dicho ambiente. La forma de sustituir los valores de entorno que se pueden definir para una aplicación en un sistema operativo, Java las maneja como una serie de propiedades que pueden ser consultadas.

A estas propiedades se las denomina propiedades del sistema y es un concepto que se utiliza para remplazar las variables de entorno (las cuales son específicas de la plataforma que las define).

Como todo en Java, los valores se almacenarán en un objeto, el cual es del tipo `Properties`. Este objeto lo define la máquina virtual al arrancar y se puede obtener una referencia al mismo por el método estático `System.getProperties()`, el cual retorna un objeto de este tipo con los valores
antes mencionados.

Una vez obtenida la referencia al objeto que almacena los valores, se puede utilizar un método de servicio, el cual está definido en este, para recuperar el valor asociado al nombre de una propiedad que le sea especificado como argumento. El método `getProperty()` retorna un String el cual representa el valor de la propiedad cuyo nombre se especifica.

Se puede utilizar también la opción -D al ejecutar un programa para incluir una nueva propiedad, como si esta fuese del sistema, y su valor se puede recuperar como el de cualquier otra propiedad. 

El ejemplo del Código 9-2 muestra cómo se realiza la acción antes descripta. Notar como se recupera primero el nombre de la propiedad para luego utilizarlo para saber su valor.

##### Código 9-2: Usando las propiedades del sistema
```java
package propiedades;

import java.util.Properties;
import java.util.Enumeration;

public class PruebaPropiedades {

      public static void main(String[] args) {
            Properties props = System.getProperties();
            Enumeration<?> prop_names = props.propertyNames();
            while (prop_names.hasMoreElements()) {
                String prop_name = (String) prop_names.nextElement();
                String property = props.getProperty(prop_name);
                System.out.println("propiedad '" + prop_name + "' es '" +property + "'");
            }
      }
}
```
Hay que tener en cuenta que dependiendo la configuración de cada sistema, esta salida será diferente. Un posible resultado se muestra en el Listado 9-2.

##### Listado 9-2: Salida por consola de las propiedades leídas
```java

propiedad 'java.runtime.name' es 'Java(TM) SE Runtime Environment'
propiedad 'sun.boot.library.path' es 'C:\Program Files\Java\jre7\bin'
propiedad 'java.vm.version' es '21.0-b17'
propiedad 'user.country.format' es 'AR'
propiedad 'java.vm.vendor' es 'Oracle Corporation'
propiedad 'java.vendor.url' es 'http://java.oracle.com/'
propiedad 'path.separator' es ';'
propiedad 'java.vm.name' es 'Java HotSpot(TM) 64-Bit Server VM'
propiedad 'file.encoding.pkg' es 'sun.io'
propiedad 'user.script' es ''
propiedad 'user.country' es 'US'
propiedad 'sun.java.launcher' es 'SUN_STANDARD'
propiedad 'sun.os.patch.level' es 'Service Pack 1'
propiedad 'java.vm.specification.name' es 'Java Virtual Machine Specification'
propiedad 'user.dir' es 'C:\Educación\Java\Carrera básica - Desarrollador Java\Versión 2\Trabajo\Programación en
Java\Acomodo\Ejemplos\Eclipse\Módulo9\Modulo9\EntradasSalidas'
propiedad 'java.runtime.version' es '1.7.0-b147'
propiedad 'java.awt.graphicsenv' es 'sun.awt.Win32GraphicsEnvironment'
propiedad 'java.endorsed.dirs' es 'C:\Program Files\Java\jre7\lib\endorsed'
propiedad 'os.arch' es 'amd64'
propiedad 'java.io.tmpdir' es 'C:\Users\Marcelo\AppData\Local\Temp\'
propiedad 'line.separator' es '
propiedad 'java.vm.specification.vendor' es 'Oracle Corporation'
propiedad 'user.variant' es ''
propiedad 'os.name' es 'Windows 7'
propiedad 'sun.jnu.encoding' es 'Cp1252'
propiedad 'java.library.path' es 'C:\Program
Files\Java\jre7\bin;C:\Windows\Sun\Java\bin;C:\Windows\system32;C:\Windows;C:\Program Files\Common Files\Microsoft
Shared\Windows Live;C:\Program Files (x86)\Common Files\Microsoft Shared\Windows Live;C:\Program Files (x86)\NVIDIA
Corporation\PhysX\Common;C:\Windows\system32;'
propiedad 'java.specification.name' es 'Java Platform API Specification'
propiedad 'java.class.version' es '51.0'
propiedad 'sun.management.compiler' es 'HotSpot 64-Bit Tiered Compilers'
propiedad 'os.version' es '6.1'
propiedad 'user.home' es 'C:\Users\Marcelo'
propiedad 'user.timezone' es ''
propiedad 'java.awt.printerjob' es 'sun.awt.windows.WPrinterJob'
propiedad 'file.encoding' es 'Cp1252'
propiedad 'java.specification.version' es '1.7'
propiedad 'user.name' es 'Marcelo'
propiedad 'java.class.path' es 'C:\Educación\Java\Carrera básica - Desarrollador Java\Versión 2\Trabajo\Programación en
Java\Acomodo\Ejemplos\Eclipse\Módulo9\Modulo9\EntradasSalidas\bin'
propiedad 'java.vm.specification.version' es '1.7'
propiedad 'sun.arch.data.model' es '64'
propiedad 'java.home' es 'C:\Program Files\Java\jre7'
propiedad 'sun.java.command' es 'propiedades.PruebaPropiedades'
propiedad 'java.specification.vendor' es 'Oracle Corporation'
propiedad 'user.language' es 'en'
propiedad 'user.language.format' es 'es'
propiedad 'awt.toolkit' es 'sun.awt.windows.WToolkit'
propiedad 'java.vm.info' es 'mixed mode'
propiedad 'java.version' es '1.7.0'
propiedad 'java.ext.dirs' es 'C:\Program Files\Java\jre7\lib\ext;C:\Windows\Sun\Java\lib\ext'
propiedad 'sun.boot.class.path' es 'C:\Program Files\Java\jre7\lib\resources.jar;C:\Program
Files\Java\jre7\lib\rt.jar;C:\Program Files\Java\jre7\lib\sunrsasign.jar;C:\Program Files\Java\jre7\lib\jsse.jar;C:\Program
Files\Java\jre7\lib\jce.jar;C:\Program Files\Java\jre7\lib\charsets.jar;C:\Program Files\Java\jre7\classes'
propiedad 'java.vendor' es 'Oracle Corporation'
propiedad 'file.separator' es '\'
propiedad 'java.vendor.url.bug' es 'http://bugreport.sun.com/bugreport/'
propiedad 'sun.cpu.endian' es 'little'
propiedad 'sun.io.unicode.encoding' es 'UnicodeLittle'
propiedad 'sun.desktop' es 'windows'
propiedad 'sun.cpu.isalist' es 'amd64'
```
La clase `Properties` implementa un mapa de nombres respecto de sus valores (un mapa de `String` a `String`) donde se debe interpretar el primer `String` como una clave y el segundo como el valor asociado a dicha clave.

El método `propertyNames()` retorna una referencia a un objeto del tipo `Enumeration` (enumeración) de todos los nombres de propiedades. Esta sirve para recorrer las propiedades y obtener sus valores.

El método `getProperty()` retorna un `String` representando el valor que corresponde al nombre indicado en el argumento del método.

Una colección de propiedades se puede leer y escribir a un archivo utilizando load y store para recuperar de esta manera la información o "persistirla".

#### Fundamentos de las E / S 

Una corriente se puede pensar como un flujo de bytes (datos) desde una fuente a un receptor, donde la fuente y el receptor puede ser cualquier objeto capaz de almacenar, emitir, leer o crear datos.
Las dos posibilidades de una corriente son ser fuente (o emisora) y receptora. Una corriente fuente inicia el flujo de bytes y también es conocida como corriente de ingreso. Una corriente receptora finaliza el flujo de bytes y también es conocida como corriente de salida.

Fuentes y receptores son ambas corrientes nodales (nodos de comunicación), donde un nodo es
cualquier tipo de objeto.

Los tipos de corrientes nodales son, por ejemplo, archivos, memoria y tuberías (pipes) entre subprocesos o procesos

#### Salidas por consola
Los sistemas operativos modernos definen un mínimo de tres corrientes de caracteres estándar
para el acceso a los dispositivos periféricos:
- El ingreso estándar (Standard Input)
- La salida estándar (Standard Output)
- La corriente de errores estándar (Standard Error)

Las corrientes estándar están asociadas siempre a un dispositivo por defecto. Sin embargo. Como son corrientes (en inglés, streams) pueden ser dirigidas hacia a otros dispositivos (como el ejemplo típico de la salida por pantalla que se direcciona a la impresora).

En Java existen objetos que permiten

- ` System.out` permite escribir en la "standard output" (salida estándar).
a. Es un objeto del tipo `PrintStream` (asociado a la salida por consola).
- `System.in` permite leer de la "standard input" (entrada estándar).
a. Es un objeto del tipo `InputStream` (asociado al ingreso por consola).
- `System.err` permite escribir en la "standard error" (error estándar).
a. Es un objeto del tipo `PrintStream` (asociado a la salida por consola).

Cada una de las corrientes pueden manejarse como archivos, es decir, se las puede abrir, escribir, leer y cerrar según sea el caso y la posibilidad de hacerlo (no se puede escribir en el ingreso estándar, pero si se puede leer de él).

### Escribiendo en el estándar output

Java define una serie de clases que permiten un cómodo manejo unificado de todas las corrientes en un sistema operativo (entre las que se encuentran las estándar y las propias de los archivos en disco, canales de comunicación, etc…).

Para llevar a cabo esa unificación, se definen una serie de clases que reciben como parámetros a las corrientes, por ejemplo, y definen métodos en su interfaz que permiten un mejor manejo de las mismas. Esta funcionalidad a nivel de diseño se la denomina “decorador” y es un patrón de
diseño conocido.

Así, a través de los decoradores, se pueden utilizar métodos conocidos para escribir o leer de una corriente (los detalles de esta operatoria se explicarán posteriormente). Se puede definir entonces la funcionalidad de algunos métodos conocidos que permiten interaccionar con las corrientes:
- Los métodos `println` escriben el argumento y una nueva línea.
- Los métodos `print` imprimen el argumento sin la nueva línea

Ambos métodos están sobrecargados para todos los tipos primitivos y además para `char[]`, `Object` y `String`.
Los métodos `print(Object)` y `println(Object)` llaman al método `toString()` del argumento para permitir al programador que coloque de la forma que quiera un mensaje que identifique al objeto tan sólo sobrescribiendo toString. 

### Leyendo del estándar input
Para demostrar la interacción con la corriente estándar, el Código 9-3 lee los ingresos por teclado hasta que se cierra la corriente con un carácter de fin de archivo.

Código 9-3: Lectura de la corriente estándar de ingreso de caracteres del teclado

```java 
package corrientes;

import java.io.*;

public class IngresoPorTeclado {

    public static void main(String args[]) {
            String s;
            // Crea un lector con buffer para cada línea del teclado.
            InputStreamReader ir = new InputStreamReader(System.in);
            BufferedReader in = new BufferedReader(ir);
            System.out.println(
                  "Unix: Tipear ctrl-d o ctrl-c para salir."
                          + "\nWindows: Tipear ctrl-z para salir ");
            try {
                // Lee cada línea de entrada y lo muestra por pantalla.
                s = in.readLine();
                while (s != null) {
                    System.out.println("Leído: " + s);
                    s = in.readLine();
                }
                // Cierra el lector con buffer
                in.close();
            } catch (IOException e) {
              e.printStackTrace();
            }
    }
}

```
### Creación de un objeto del tipo File

Esta clase se utiliza para representar abstractamente un archivo en disco. La representación
abstracta se debe a que cada sistema operativo gestiona el camino hasta un archivo de forma
diferente (un ejemplo de esto es el carácter que divide los directorios y subdirectorios que puede
ser “/” o “\”). En el caso de los nombres UNC (Uniform Naming Convention) para Windows, por
ejemplo, se debe utilizar “\\” para indicar el camino del archivo en el código de un programa Java.
Para evitar problemas con los separadores de nombres, se puede obtener cual es el separador
correcto para la plataforma en la cual se ejecuta el programa obteniendo su valor de la propiedad
del sistema file.separator
Para manejar los nombres y caminos de archivos, esta clase define un camino abstracto o ruta. Un
camino abstracto tiene dos componentes:
- Una cadena de prefijo opcional dependiente del sistema con la letra del dispositivo
seguido de: “/” para Unix o “\\” para Windows
- Una secuencia de nombres con sus respectivos separadores (puede ser nulo)
Todos los nombres se interpretarán como directorios a excepción del __último__.

| Nota: Cuando se construye el objeto nunca se crea un archivo. La máquina virtual no realiza una operación de entrada – salida hasta que un método específico intenta realizarlo, como por ejemplo un `println`. En ese caso, si el archivo no existe, lo crea. Si el archivo existe, lo trunca. Una opción para crear un archivo vacío sin realizar ninguna operación es invocar al método `createNewFile`. |  
| ----| 

El programa del Código 9-4 no crea ningún archivo porque no se especifica ningún método que produzca dicho efecto.
Código 9-4: Código que no crea el archivo al no hacer una operación de E / S

```java
package archivos;

import java.io.File;}

public class ArchivosAnteriores1 {

    public static void main(String[] args) {
        File miArchivo;
        miArchivo = new File("miArchivo.txt");
        File miArchivo2 = new File("MisDocs", "miArchivo.txt");
    }
}
```
Los directorios se tratan igual que archivos en Java. La clase File soporta métodos para recuperar un vector de archivos de un directorio y armar una lista con ellos para tratarlos en programa. El ejemplo del Código 9-5 muestra cómo crear un archivo, pero cuando se intenta crearlo en un directorio llamado `MisDocs`, se produce un error de E/S si el directorio no existe.

###### Código 9-5: Intento de crear un archivo en un directorio inexistente

```java
package archivos;

import java.io.File;
import java.io.IOException;

public class ArchivosAnteriores2 {

      public static void main(String[] args) {
              
              File miArchivo;
              
              miArchivo = new File("miArchivo.txt");
              
              File miArchivo2 = new File("MisDocs", "miArchivo.txt");
              
              try {
                  // A partir del objeto File creamos el archivo físicamente
                  if (miArchivo.createNewFile())
                      System.out.println("El archivo se ha creado " +
                      "correctamente");
                  else
                      System.out.println("No ha podido ser creado el archivo");
                  if (miArchivo2.createNewFile())
                      System.out.println("El archivo se ha creado " +
                      "correctamente");
                  else
                    System.out.println("No ha podido ser creado el " +
                    "archivo");
              } catch (IOException ioe) {
                ioe.printStackTrace();
              }
      }
}
```
Al ejecutar el programa se produce la salida del Listado 9-3 (suponiendo que el directorio no existe). Notar que el primer intento crea al archivo por no especificar el directorio y usar el definido por defecto, que siempre es el CLASSPATH de donde se ejecuta el programa.

Listado 9-3: Salida por consola del programa
```javav
El archivo se ha creado correctamente
java.io.IOException: The system cannot find the path specified
      at java.io.WinNTFileSystem.createFileExclusively(Native Method)
      at java.io.File.createNewFile(Unknown Source)
      at archivos.ArchivosAnteriores2.main(ArchivosAnteriores2.java:22)
```
Como se puede apreciar, el manejo de directorios y archivos puede ser un poco confuso.
### Funciones de utilidad
Como la construcción de un objeto del tipo File implica la creación solamente de un objeto en memoria pero no se realiza ninguna entrada salida hasta el momento en que se indica explícitamente, existen distintas funciones que se pueden utilizar tanto antes como después de hacer una E/S

##### Nombres de archivos
- `String getName()`
  - Retorna el nombre abstracto del archive que define la clase.
- `String getPath()`
  -Convierte el nombre y camino completo abstracto de la clase a un nombre
dependiente de la plataforma.
- `String getAbsolutePath()`
  - Si el nombre de archivo abstracto que posee el objeto es absoluto, lo devuelve. Si
es relativo, lo transforma a absoluto y lo retorna.
- `String getParent()`
  - Si el archivo está en un directorio, retorna el nombre. Si no puede resolver el
nombre del directorio retorna un nulo.
- `boolean renameTo(File newName)`
  - Renombra el archivo al nombre indicado.
  
##### Comprobación de archivos
- `boolean exists()`
  - Verifica si el nombre de directorio o archivo con el que se .construyó el objeto
existe
- `boolean canWrite()`
  - Si el archivo existe, verifica si se puede escribir.
- `boolean canRead()`
  - Si el archivo existe, verifica si se puede leer.
- `boolean isFile()`
  - Verifica si el nombre con el que se construyó el objeto es un archivo.
- `boolean isDirectory()`
  - Verifica si el nombre con el que se construyó el objeto es un directorio.
- `boolean isAbsolute()`
  - Verifica si el nombre con el que se construyó el objeto es absoluto.

##### De información y utilidad en general
- `long lastModified()`
  - Retorna cuando el objeto del sistema que está siendo representado por el que
está en memoria fue modificado por última vez.
- `long length()`
  - Si el objeto representado es un archivo, retorna su tamaño, sino (si es un
directorio) puede retornar cualquier valor.
- `boolean delete()`
  - Si el objeto representado es un archivo, lo borra. Si es un directorio, debe estar
vacío para borrarlo.
##### Utilidades de directorio
- `boolean mkdir()`
  - Crea un directorio con el nombre almacenado por el objeto en memoria
- `String[] list()`
  - Si el objeto representado es un archivo, retorna un nulo. Si es un directorio,
retorna un vector de String que representa los nombres de archivos del
directorio.

### E/S de Corrientes de Archivos
Como se mencionó anteriormente, se utilizan decoradores para simplificar el acceso y escritura de
archivos, ya que estos también conforman corrientes de E/S. Un decorador a su vez, puede ser
argumento de creación para otro decorador. Un ejemplo de estos casos para entradas y salidas
son los siguientes:

Entradas de archivos

- Usar la clase FileReader para leer caracteres en bruto (sin formato)
 - Usar la clase BufferedReader para utilizar el método readLine()

Salidas a archivos
 - Usar la clase FileWriter para escribir caracteres en bruto (sin formato)
 - Usar la clase PrintWriter para usar los métodos print() y println()

#### Ejemplo de Entrada
Para entender mejor el proceso de lectura de un archivo de disco se presenta un ejemplo en el
Código 9-6 de lectura con almacenamiento intermedio (buffer o búfer).
 
 
 

Código 9-6: Lectura con búfer de un archivo en disco
```java
package archivos;

import java.io.BufferedReader;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;

public class LeeArchivo {
        public static void main(String[] args) {
              File file = new File(args[0]);
              try { // Crear un lector
                    // con buffer para leer cada línea del archivo
                    BufferedReader in = new BufferedReader(new FileReader(file));
                    String s;
                    s = in.readLine();
                    // leer cada línea del archivo y mostrarlo en pantalla
                    while (s != null) {
                        System.out.println(" Leyó : " + s);
                        s = in.readLine();
                    }
                    in.close();
                    // Cerrar el lector con buffer, que también
                    // cierra el lector de archivo
              } catch (FileNotFoundException e1) {
                    // Si no existe el archivo
                      System.err.println("Archivo no encontrado : " + file);
              } catch (IOException e2) {
                   e2.printStackTrace();//Para cualquier otra excepción de E/S
              }
        }
}
```
#### Ejemplo de Salida
Análogamente al caso anterior, para comprender el proceso de salida a un archivo en disco, se
presenta el Código 9-7 para comprender el proceso para escribir un archivo en disco con búfer.
 
 Código 9-7: Escritura de un archivo en disco con búfer
```java
package archivos;

import java.io.BufferedReader;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;

public class EscribeArchivo {

      public static void main(String[] args) {

            File file = new File(args[0]); // Crear el archivo
            try {
                // Crear el lector con buffer para leer cada línea del
                // estándar input
                BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
                PrintWriter out = new PrintWriter(new FileWriter(file));
                // Para escribir este archivo
                String s;
                System.out.print("Ingresar el texto del archivo : ");
                System.out.println("[Tipee ctrl-d (or ctrl-z) para " +
                "finalizar.]");
                while ((s = in.readLine()) != null) {
                    // Leer cada línea y mostrarla por pantalla
                    out.println(s);
                }
                in.close(); // Cerrar el lector con buffer y el print
                out.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
      }
}
```
#### Clases básicas previas a la versión 7 para el manejo de corrientes

El paquete java.io contiene dos clases, InputStream y OutputStream, de las que derivan la mayoría de las clases de este paquete.

La clase InputStream es una superclase abstracta que proporciona un interfaz de programación mínima y una implementación parcial de la corriente de entrada. La clase InputStream define métodos para leer bytes o vectores de bytes, marcar posiciones en la corriente, saltar bytes de la entrada, conocer el número de bytes disponibles para ser leídos, y reiniciar la posición actual dentro de la corriente. Una corriente de entrada se abre automáticamente cuando se crea. Se puede cerrar una corriente explícitamente con el método close() o puede dejarse que se cierre implícitamente cuando se recolecta la basura, lo que ocurre cuando el objeto deja de ser referenciado.

La clase OutputStream es una superclase abstracta que proporciona un interfaz de programación mínima y una implementación parcial de las corrientes de salida. Una corriente de salida se abre automáticamente cuando se crea. Se puede cerrar una corriente explícitamente con el método close() o se puede dejar que se cierre implícitamente cuando se recolecta la basura, lo que ocurre cuando el objeto deja de ser referenciado.El paquete java.io contiene muchas subclases de InputStream y OutputStream que implementan funciones específicas de entrada y salida. Por ejemplo, FileInputStream y FileOutputStream son corrientes de entrada y salida que operan con archivos en el sistema operativo nativo en su
formato.

Reader es una clase abstracta para leer corrientes de caracteres. Los únicos métodos que la subclase debe implementar son read(char[], int, int) y close(). Sin embargo, las subclases pueden sobrescribir otros métodos con el fin de lograr mejor rendimiento, mayor funcionalidad o
ambos.

Writer es también una clase abstracta pero para escribir en una corriente de caracteres. Conceptualmente es la contrapartida de Reader y en este caso las subclases deben implementar obligatoriamente los métodos write(char[], int, int), flush(), y close(). Sin embargo, análogamente a Reader, las subclases pueden sobrescribir otros métodos con el fin de lograr mejor rendimiento, mayor funcionalidad o ambos.

### Corrientes clásicas
Todos los sistemas operativos modernos se manejan con corrientes. La principal dificultad en el maneja de las mismas sobrevino con la aparición del Unicode como estándar para remplazar al viejo ASCII. Si bien el Unicode es compatible con su noble antecesor, la dificultad se presentó en el hecho que los caracteres en ASCII ocupan un byte, mientras que en Unicode ocupan dos. Como se debe mantener compatibilidad con los programas que se manejan aún en la actualidad sólo en ASCII, Java soporta dos tipos de corrientes:
 - Orientadas al byte
 - Orientadas al carácter
 
Para el manejo de estas, se proveen una serie de clases que permiten a través de la creación de objetos abstraerse de las dificultades de su gestión, más allá de si el carácter está escrito en Unicode o ASCII, por lo tanto, las entradas y salidas de caracteres son manejadas por “lectores” y “escritores”, que no otra cosa que instancias de las clases provistas por el lenguaje para operaciones de entrada y salida.

Las entradas y salidas de bytes son manejadas por corrientes de ingreso y corrientes de salida. Sin embargo, en la terminología del lenguaje se separa conceptualmente a los bytes de ASCII de los caracteres Unicode. Por lo general, los términos:
 - Corriente: se refiere a una corriente de bytes (ASCII).
 - Lector y Escritor: se refieren a corrientes de caracteres (Unicode).
 
La Tabla 9-1 muestra los tipos de corrientes y su orientación según su contenido.

|  | Corrientes de byte |Corrientes de Caracteres |
| ----| ----|----|
| Corrientes Fuente | InputStream |Reader |
| Corrientes Receptoras | OutputStream |Writer |




