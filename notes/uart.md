# UART
## Basics
- UART stands for Universal Asynchronous Reciver/Transmitter. 
- Hardware peripheral of a microcontroller
- Asynchronous: no clock signal, reciever doesn't know when transmitter transmits data.
- UART basically operates as a shift register with parallel input from Tx (transmitter) and then serial data is provided to Rx (reciever), and then parallel output.
- To ensure synchronisation of clock signal of receiver and transmitter, we use start and stop bits.
- Start bit aligns clock of receving and transmitting UART signals. 
- Optional parity bit to detect errors.
- Stop bit is to indicate receiver to process data before the next transfer.


## Baud Rate
Measure of the number of bits per second that can be transmitted or received by the UART.
