# Control of PiezoSystemJena NV40/3CLE via NI DAQmx

Control of the Jena's piezo accuators via their multi-channel amplifier.
https://www.piezosystem.com/products/amplifiers/multi-channel/40ma-multi-channel-amplifiers/

Uses NIDAQ device to read and write analog voltages between 0 and 10 to
three input and output voltage channels connected to a Jena NV40/3CLE
amplifier. Each input/output channel controls one of three axis (x, y, or z).

When using this software, one must at least provide three analog channels on
the NIDAQ that are connected to the NV40/3CLE amplifier that control (write)
the location of the piezo stage.

This program does not *need* to read voltages from the amplifier. If no read
channels are provided, this program will report the last written values when
reporting the current location.  

This controller does *NOT* lock out usage of analog input and output channels
on the NI-DAQ card. It writes or reads to the analog channels and then releases
the resource. This would allow external programs to access those channels, so
long as the access is not simultaneous.

## Installation

#### Requirements

```
pip install nidaqmx
```

### Local Installation

```
git clone https://github.com/gadamc/nipiezojenapy
cd nipiezojenapy
python -m pip install .
```

## Usage

### Instantiate

```
import nipiezojena
pcon = nipiezojena.PiezoControl('Dev1',['ao0','ao1','ao2'], ['ai0','ai1','ai2'])
```

### Read Position

```
print(pcon.get_current_position())
[39.953595487425225, 40.047631567251806, 39.9510191567554]
```

### Go To Position

```
pcon.go_to_position(x = 20, y = 20, z = 20)
pcon.get_current_position()
[19.935887437291537, 19.94876864898489, 19.872769502734947]
```

Note that each axis can be set independently. Thus one can call

```
pcon.go_to_position(z = 40)
pcon.get_current_position()
[19.913989377848296, 19.988700406441584, 39.91623869419529]
```

# LICENSE

[LICENCE](LICENSE)
