# UART
## Basics
- Universal Asynchronous Reciver/Transmitter. 
- A communication protocol (as well as the similarly named hardware peripheral) that is widely used for serial data communication between hardware devices.
- Asynchronous: no clock signal, reciever doesn't know when transmitter transmits data.
- Simple, uses two lines for transmitting (Tx) and receiving (Rx) data.
- Can operate as simplex (unidirectional), half duplex (data flows in both directions, but only one direction at a time), and full duplex (bidirectional) communication.
- "One or more UART peripherals are commonly integrated in microcontroller chips. Specialised UARTs are used for automobiles, smart cards and SIMs."One of the earliest serial protocols. Seen in serial ports, devices using RS-232 interfaces, external modems, etc.

## Working
- UART operates similarly to a shift register. Parallel data is input at Tx (transmitter) into serial data which is then transmitted to Rx (reciever), and then parallel output.
- To ensure synchronisation of signals at Rx and Tx, we use start and stop bits.

### Components of UART packet
- Start bit aligns clock signal of Rx with the Tx signal. normally the UART data transmission line is kept at high voltage, so for indicating a start bit, it is changed to low voltage for 1 bit. Then it starts reading the data frame following it at the specified baud rate frequency.
- Data frame follows the start bit, and contains the actual data being transmitted. Usually about 5-8 bits with parity bit, or 9 bits without a parity bit.
- Optional parity bit to detect errors. If parity bit is odd (1), the total of logic high (1s) is even, then the error is detected, but if the total of logic high (1s) is odd, then no error is detected. Vice-versa holds true as well.
- Stop bit is to indicate and provide time for the receiver to process data before the next data frame is transferred. To indicate a stop bit, the UART makes data transmission line from low voltage to high voltage for 1-2 bits.

## Baud Rate
- It is the measure of the number of bits per second that can be transmitted or received by the UART, or maximum number of bits per second to be transferred.
- It is predetermined to be same across both ends of UART communication. Synchronization is managed by having the same baud rate on both devices.
- "The allowable difference of baud rate is up to 10% before the timing of bits gets too far off."
- Common baud rates: 9600, 19200, 38400, 57600, 115200, 230400, 460800, 921600, 1000000, 1500000

---

#### References
https://www.rohde-schwarz.com/cz/products/test-and-measurement/essentials-test-equipment/digital-oscilloscopes/understanding-uart_254524.html
https://www.analog.com/en/resources/analog-dialogue/articles/uart-a-hardware-communication-protocol.html
https://www.youtube.com/watch?v=IyGwvGzrqp8
https://www.youtube.com/watch?v=npL5ph9RG84
