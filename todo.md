### CPU


```rust
struct CPU {
    registers: Registers,
    pc: u16,
    bus: MemoryBus
}

```
the cpu holds on to the bus, and can talk through it  to the gpu

cpu also has a program counter, basically a number that points to the next instruction to be executed


- we have a program counter and reading in a byte of data from the bus that is an instruction that we want to execute so we want to interpret that instruction and do something with it

```rust
impl Instruction {
fn from_byte(byte: u8) -> INC<Instruction> {
match byte {
0x02 => Some(Instruction::INC(IncDecTarget::BC)),
0x13 => Some(Instruction::INC(IncDecTarget::DE)),
_ => /* TODO: Add mapping for all instructions */
}
}
}

```

```rust
impl CPU {
fn execute(&mut self, instruction: Instruction) {
match instruction {
Instruction::ADD(AritmeticTarget::C) => {
let result = self.register.a.wrapping_add(value);
self.register.a = result;
}
_ => { /* TODO: Add mapping for all instructions */ }
}
}
}

```

with instructions decoded from the bytes we then need to execute them
this loops infinitely and calls step, this is a high level overview of how a cpu works

#### Instruction Set

```rust
enum Instruction {
    ADD(ArithmeticTarget),
    }
    
    enum ArithmeticTarget {
    A, B, C, D, E, H, L,
    }
   ```
    the add instruction takes an arithmetic target, which is a register, and adds it to the accumulator

basicall it looks at the targets say register d, takes the contents of register d , adds it to the contents of register a and stores the result in register a

example of instructions 

- ADD
- SUB
- AND
- OR
- XOR
- INC
- DEC
- RR
- SRL
- SCF


### MEMORY

basically just one very long array and its full of bytes

 - 0x0000-0x7FFF - 32KB ROM Bank two banks of 16KB
>code run automatically from the gameboy to boot up also includes game cartridge code


- 0x8000-0x9FFF - 8KB Video RAM
>gpu struct 
- 0xA000-0xBFFF - 8KB External RAM

- 0xC000-0xCFFF - 4KB Work RAM Bank 0
>ram the game can use to store data
- 0xD000-0xDFFF - 4KB Work RAM Bank 1

- 0xE000-0xFDFF - Echo RAM

- 0xFE00-0xFE9F - Sprite Attribute Table

- 0xFEA0-0xFEFF - Not Usable

- 0xFF00-0xFF7F - I/O Ports

- 0xFF80-0xFFFE - High RAM

- 0xFFFF - Interrupt Enable Register


```rust
struct MemoryBus {
memory: [u8; 0xFFFF],
gpu: Gpu,
}
```
and address space of 16 bits
that the gameboy could adress

```rust

impl MemoryBus {
    fn read_byte(&self, address: u16) -> u8 {
    if address >= VIDEO_RAM_Begin || address <= VIDEO_RAM_End {
        self.gpu.read_byte(address)
    } else {
        self.memory[address as usize]
    }
}
```

>Next we cover registers
#### Registers
smallest piece of memory in the gameboy is a register
a register is a single byte of memory
registers are used to store data that is used by the cpu
```rust
struct Registers {
    a: u8,
    b: u8,
    c: u8,
    d: u8,
    e: u8,
    f: u8,
    h: u8,
    l: u8,
    pc: u16,
    sp: u16,
}
```



### GRAPHICS
> tileset

constructed from 8x8 pixel tiles

0 - around 300 pixels
> background

map tiles onto place in background

map from a tile in the tileset to a place in the background

background is much larger than the display screen 
so we need to implement a viewport which is a window into the background
and it can scroll around

rust psuedo code
```rust
struct GPU {
    tile_set: [Tileset; 384]
    video_ram: [u8; VIDEO_RAM_SIZE]
    canvas_buffer: [u8; NUM_PIXELS]
}
```
 tileset is 384 tiles and each tile is 8x8 pixels can be thought as an array

video ram includes things like our background map and our tileset

canvas buffer is the actual pixels that we are going to display on the screen and we are going to use this to draw to the screen ourselves using what the program does with the tileset and the video ram composed together

### SOUND

### INPUT



# Make it RUN
use something that gives you a frame buffer (like SDL2) or use a library that does it for you (like ggez, minifb, piston, etc) it is a lot of work to do it yourself, and you will probably get it wrong.

```rust
fn run(mut cpu: CPU, mut window: Window) {
    let mut window_buffer = [0; NumPixels];
    let mut cycles_elapsed_in_frame = 0usize;
    let mut now = Instant::now();
    while window.is_open() && !window.is_key_down(Key::Escape) {
        let time_delta = now.elapsed().subsec_nanos();
        now = Instant::now();
        cycles_elapsed_in_frame += cpu.step(time_delta);
        if cycles_elapsed_in_frame >= One_Frame_In_Cycles {
            for (i, pixel) in cpu.pixel_buffer().enumerate() {
                buffer[i] = pixel;
            }
            window.update_with_buffer(&window_buffer, WIDTH, HEIGHT).unwrap();
            cycles_elapsed_in_frame = 0;
            
        }else{
            sleep(Duration::from_nanos(2))
            }
            }
    }


```
first is some setup code window buffer, cycles elapsed in frame, and some timing stuff "what is right now"

then we have a loop that runs until the window is closed or the escape key is pressed
inside that we do some time tracking how much time has passed since we were last here, and then 
we update the time now with the updated time

then we call cpu.run passing in the time delta so the cpu knows how many times to run step for that ammount of time and the gameboy has a very well defined amount of time its allowed to run. this returns how many cycles have been run, and we add that to our cycles elapsed in frame

then we check if we have run a full frame worth of cycles, if we have we draw the frame to the screen and reset the cycles elapsed in frame (30 times a second)


# Make it FAST