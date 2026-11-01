# Zona Cubo

Shooter de zombis por salas para iPhone y iPad (también funciona en la compu). Es un juego original: personajes con cabeza de caja de cartón, un depósito lleno de zombis y una puerta que se abre cuando limpiás la sala.

Todo está en un solo archivo: `zona-cubo.html`.

## Modos

- **1 jugador:** el pulgar izquierdo mueve y el derecho apunta y dispara. La puntería tiene una pequeña ayuda hacia el zombi más cercano.
- **2 jugadores (mismo aparato):** cada uno mueve a su personaje desde su mitad de la pantalla. Los personajes disparan solos al zombi más cercano que ven. Ideal para iPad.
- **Online:** cada uno juega desde su propio teléfono, con los controles completos del modo 1 jugador.

## Cómo se juega

1. Matá a todos los zombis de la sala.
2. Cuando aparezca el cartel "Sala limpia", la puerta de la pared se abre (brilla en verde). Caminá hasta ella.
3. Cada sala tiene otro diseño. Cada 5 salas aparece un jefe que embiste.
4. Si caés en 2 jugadores u online, tu compañero sigue y volvés a la vida cuando limpian la sala.
5. La partida termina cuando caen todos los jugadores.

### Armas y objetos

| Objeto | Qué hace |
| --- | --- |
| Pistola | Munición infinita. |
| Metralleta (caja **M**) | Dispara muy rápido. |
| Escopeta (caja **E**) | Varios perdigones por disparo, corto alcance. |
| Bazuca (caja **B**) | Explosión en área. |
| Botiquín (cruz roja) | Recupera 35 de vida. |

Tocá el cuadro del arma (arriba, junto a tu barra de vida) para cambiar entre las que tengas.

Los **barriles rojos** explotan si les disparás: dañan a los zombis, pero también a vos. Las bajas seguidas suben el multiplicador de puntos (x2, x3...).

### Enemigos

- **Caminante:** lento y común.
- **Corredor:** frágil y rápido, aparece desde la sala 3.
- **Bruto:** grande y resistente, aparece desde la sala 5.
- **Jefe:** cada 5 salas. Se pone naranja antes de embestir.

## Teclado (opcional, en compu o iPad con teclado)

| Tecla | 1 jugador / online | 2 jugadores |
| --- | --- | --- |
| Mover | W A S D | J1: W A S D, J2: flechas |
| Apuntar y disparar | Flechas | Automático |
| Disparar al más cercano | Espacio o J | Automático |
| Cambiar arma | Q | (tocar el cuadro del arma) |
| Pausa | Esc o P | Esc o P |

## Publicarlo en GitHub Pages e instalarlo en el iPhone

1. Creá un repositorio nuevo en GitHub.
2. Subí `zona-cubo.html` y **renombralo a `index.html`**.
3. En el repositorio: **Settings → Pages → Build and deployment**. Elegí "Deploy from a branch", rama `main`, carpeta `/ (root)`, y guardá.
4. Esperá uno o dos minutos y abrí la dirección que te muestra GitHub, en **Safari**.
5. Tocá **Compartir → Agregar a pantalla de inicio**. Se instala con su ícono y se abre a pantalla completa, sin barra del navegador.

Giralo en horizontal para jugar más cómodo.

## Jugar online

1. El anfitrión toca **Online → Crear sala** y recibe un código de 4 letras o números.
2. El otro jugador toca **Online → Unirme**, escribe el código y toca **Conectar**.
3. Cuando se conectan, la partida empieza sola. Si caen los dos, el anfitrión decide si juegan otra vez.

Cosas a tener en cuenta:

- Solo funciona en la versión publicada (GitHub Pages) y con internet. **Dentro de la vista previa de Claude no conecta.**
- Usa una conexión directa entre los dos teléfonos (WebRTC) a través de la librería PeerJS. Para encontrarse usan el servidor público y gratuito de PeerJS, que a veces anda lento o está caído.
- Algunas redes de datos móviles bloquean las conexiones directas. Si no conecta, probá con la misma red wifi o con otro proveedor.
- La partida corre en el teléfono del anfitrión, así que el invitado puede notar un pequeño retraso al moverse.
- Online no se pausa: el juego sigue corriendo mientras estás en el menú de pausa.
- Se probó con un simulador de conexión entre dos pestañas. Todavía falta probarlo por internet de verdad entre dos teléfonos.

## Detalles técnicos

- Un solo archivo HTML con canvas 2D, sin instalación ni compilación.
- Internet se usa solo para las fuentes de Google (Saira Stencil One y Barlow Condensed) y para cargar PeerJS al entrar al modo online. Sin internet el juego se ve con tipografías de reserva y los modos locales andan igual.
- El sonido se genera en el momento (no hay archivos de audio). Si el iPhone está en modo silencio, no suena.
- El récord (mejor sala y puntaje) se guarda en el navegador de cada dispositivo.
- Las salas se generan al azar y siempre se puede llegar a todos los lugares.

### Para ajustar la dificultad

Dentro del archivo, en la sección `Datos`, están las tablas `WP` (armas: cadencia, daño, munición) y `ZT` (zombis: vida, velocidad, daño, puntos), y la constante `PL_SPEED` (velocidad del jugador). La función `makeQueue` define cuántos zombis y de qué tipo hay en cada sala.
