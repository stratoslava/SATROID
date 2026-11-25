# SATROID
Super Metroid for Sega Saturn
SUPER METROID PARA SEGA SATURN - PARCHE 1.0
===========================================
Port: Stratoslava

AVISO
  Este parche es solo para quienes tienen el cartucho original de Super
  Metroid para SNES y hicieron su propio volcado (dump) de la ROM.
  El parche NO trae el juego: no incluye la ROM, ni sus graficos, ni su
  musica. Con tu ROM, arma los discos para tu Saturn.
  No compartas los discos que arme el parche: llevan tu ROM adentro.
  Es un proyecto de fans, sin fines de lucro y sin relacion con Nintendo
  ni con SEGA. Super Metroid es una marca de Nintendo.

QUE NECESITAS
  - Una ROM de Super Metroid (Japon/EE.UU.), sin parches ni hacks, en
    formato .smc o .sfc (con o sin encabezado de 512 bytes).
    El parche la comprueba (SHA-1 da957f0d63d14cb441d215462904c4fa8519c613).
    La version europea (PAL) no sirve.
  - Una Sega Saturn con el cartucho de expansion de 4 MB de RAM (o un
    emulador con ese cartucho: Mednafen/Beetle Saturn, SSF, Yaba Sanshiro).
  - Para la musica orquestal (opcional): las pistas MSU-1 de Super Metroid
    (archivos supermetroid_msu1-1.pcm ... supermetroid_msu1-30.pcm) o las
    mismas pistas en .wav. Se consiguen aparte; ver MUSICA mas abajo.

COMO SE USA
  1. Pone la ROM (y, si queres, la carpeta con la musica) en la misma
     carpeta que el parche.
  2. Abri el parche:
       Windows: doble clic en smsaturn_parche.exe
       Linux:   ./smsaturn_parche_linux
       Mac:     smsaturn_parche_mac_apple (M1/M2/M3...) o
                smsaturn_parche_mac_intel. La primera vez, clic derecho >
                Abrir, porque no esta firmado.
  3. Elegi la musica: 1 = la original del juego, 2 = la orquestal.
     Si el parche no encuentra la ROM o la musica, te pide que arrastres
     el archivo o la carpeta a la ventana.
  4. Los discos quedan en la carpeta SuperMetroidSaturn:
       smsaturn.cue / smsaturn.iso                  el juego
       smsaturn_medidor.cue / smsaturn_medidor.iso  el mismo juego con el
                                                    medidor de rendimiento
       pista_02.bin ... pista_31.bin                la musica orquestal
                                                    (solo si la elegiste;
                                                    la usan los dos discos)
     Para grabar o cargar el juego, abri el .cue (no el .iso).
  Tambien se puede usar desde la linea de comandos:
     smsaturn_parche -rom "Super Metroid.sfc" -musica original
     smsaturn_parche -rom sm.smc -musica "carpeta de la musica" -salida discos

MUSICA
  - Original: la del juego, sale de tu ROM. No hace falta nada mas.
  - Orquestal: pistas de CD a partir del pack MSU-1 de Super Metroid
    (hack MSU-1 de DarkShock, arreglos de Blake Robinson). No viene con el
    parche; se consigue aca:
      http://www.mediafire.com/download/euj8ewjv59d2022/SuperMetroidMSU1_Music.7z
    Descomprimi el .7z (con 7-Zip, por ejemplo) dentro de la carpeta del
    parche: el parche busca la musica solo, tambien en subcarpetas.
    El parche acepta los .pcm del pack MSU-1 (traen el punto de loop) o
    .wav (cualquier frecuencia, mono o estereo; se convierten a audio de CD).
    Los archivos tienen que terminar en el numero de pista: "...-12.pcm",
    "12.wav", "Track 12.wav", etc. Si falta alguna pista, ese tema suena con
    la musica original.

EL MEDIDOR (para reportar problemas)
  El disco smsaturn_medidor es el mismo juego con un medidor de rendimiento
  en la esquina de arriba. Arranca mostrando la pagina 1. Para cambiar de
  pagina, mantene L y R y apreta X (o Y o Z):
      pagina 1 -> pagina 2 -> pagina 3 -> apagado -> pagina 1 ...
  Los numeros se actualizan cada 2 segundos.

  Un poco de contexto: la Saturn tiene dos procesadores. El PRINCIPAL corre
  el juego (la logica del SNES); el SEGUNDO dibuja la imagen. El juego
  necesita 60 cuadros por segundo; cada cuadro dura 16,7 ms. Si alguno de
  los dos tarda mas que eso, el juego se pone lento o saltea cuadros.

  PAGINA 1 (la mas util)
      60   60        cuadros del juego por segundo | cuadros dibujados por segundo
      05   04        ms del procesador principal   | ms del segundo procesador
    - Arriba a la izquierda: velocidad del juego. 60 = normal. Menos de 60
      = el juego va en camara lenta.
    - Arriba a la derecha: cuantas imagenes se muestran por segundo. Si es
      menor que el de la izquierda, el juego va a velocidad normal pero se
      saltea cuadros (se ve a los saltos).
    - Abajo: cuanto trabaja cada procesador por cuadro, en milisegundos.
      Hasta 16 esta bien; cerca de 16 o mas es donde aparecen los problemas.

  PAGINA 2 (el segundo procesador, en DECIMAS de ms: 25 = 2,5 ms)
      lista de sprites   | graficos (tiles)
      mapas de fondo     | scroll por linea + registros
      paleta de colores  | mezcla de colores (transparencias)
      Modo 7             | graficos de sprites atrasados
    Sirve para saber QUE parte del dibujo es la lenta.

  PAGINA 3 (el procesador principal, en DECIMAS de ms)
      logica del juego   | captura de la imagen
      copia del cuadro   | sonido
      resto              | total
      cuadros del juego  | cuadros dibujados (por segundo, como en la pag. 1)

  COMO REPORTAR UN PROBLEMA
    1. Usa el disco smsaturn_medidor y anda al lugar del problema.
    2. Saca una foto o un video donde se vea la imagen y el medidor
       (pagina 1; si el problema es de lentitud, tambien las paginas 2 y 3).
    3. Conta donde estabas (zona, sala, que estabas haciendo), si es
       consola real o emulador (cual) y que version del parche usaste.
  El disco normal (smsaturn) no tiene medidor: L + R + X/Y/Z no hace nada.

PROBLEMAS CONOCIDOS
  - En la consola, la intro en Modo 7 (el laboratorio y la pantalla de
    titulo) puede mostrar algunos pixeles de mas. En los emuladores no pasa.
  - Cuando aparece el cartel de un item, el agua o la lava transparente
    dejan de verse hasta que se va el cartel. Asi es tambien en el SNES.

CODIGO FUENTE
  El codigo fuente del port se publica aparte (SuperMetroidSaturn_codigo),
  para que cualquiera pueda seguirlo o mejorarlo. Ver su LEEME_DESARROLLO.

CREDITOS
  - Port a Sega Saturn: Stratoslava, con Claude (Anthropic).
  - Basado en la reimplementacion en C de Super Metroid de snesrev
    (github.com/snesrev/sm).
  - libyaul (biblioteca de desarrollo para Saturn).
  - Musica orquestal: hack MSU-1 de DarkShock, arreglos de Blake Robinson.
