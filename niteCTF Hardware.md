## U Are T Detective
**Flag: `nite{n0n_std_b4ud_r4t3s_ftw}`**

In this challenge, we are given a `signal.sr` file. We can easily find that `.sr` is a Pulseview Sigrok Dump file. So view download Pulseview and open the file. 

On zooming in, we are able to find a signal on the `D1` dataline.

![](/media/uart_1.png)

Using the hint from the challenge title, we find out that this is a `UART` signal. We try to decode it using the UART decoder in Pulseview but it shows an frame error.

![](/media/uart_2.png)

On troubleshooting a bit more, we find out this is because of an incorrect baud rate. 

Baud rate refers to the number of signal changes (symbols) transmitted per second. 
```
Baud rate = number of signal elements/total time (in seconds)
```

To calculate the appropriate baud rate, we find:
```
t = the time taken by the smallest bit of the signal
1/t = new baud rate
``` 

![](/media/uart_3.png)

So in our case the baud rate would be calculated as,
```
t = 187.5 ns
1/t = 1*(10^9)/187.5
	= 5333333
``` 

Now, we set the Receiving line `RX` to `D1`, and the Baud rate is changed to `5333333`. The output data format is set to `ascii` and data bits are changed to `8`, in case not done already.

![](/media/uart_4.png)

We obtain the flag in the output of the complete signal.

**Learnt:** UART protocol, reading signals in Pulseview, baud rate

**Challenges/Wrong Approaches:** First wrong approach was that I was not able to find out what to after obtaining the frame error. Then after I found out about the baud rate, I was choosing the wrong smallest bit, so I was setting the baud rate wrong.

**References:** 
https://www.youtube.com/watch?v=sTHckUyxwp8
https://www.geeksforgeeks.org/baud-rate-and-its-importance/

---
## Mic Mimic
**Flag: `nite{17:0,18:1,19:1,20:0,16}`**

On reading up more about the given device, we try to find it's datasheet. To do this, we find the [report](https://fcc.report/FCC-ID/DD4ULXD8X52/3183678) with FCC ID as `DD4ULXD8X52`.

Then we refer the website `fccid.co` to find out about the parts used in the mic, and other internal documents which could provide us with a hint to which ADC is being used.

On this [report](https://fccid.io/DD4ULXD8X52/Internal-Photos/2407RSU018-UE-Internal-Photograph-r2-7656796) with internal photos of the product, which shows an ADC with the ID `PCM1803A`.

![](/media/micmimic_1.png)

Then we get the component [datasheet](https://www.ti.com/lit/ds/symlink/pcm1803a.pdf?ts=1735330938254&ref_url=https%253A%252F%252Fwww.google.com%252F). 

The following pins are used as mentioned in the challenge description,
![](/media/micmimic_2.png)

Using the provided data, we infer the following:
1. Pin 10 (`LRCK`) and 11 (`BCK`) act as the output, this means that we must be in `master` mode.
2. It is mentioned that when we receive 24 bit from pin 12 (`DOUT`), we get an active low (0) at pin 10 (`LRCK`). This would match with `Format 2` in the PDF. (as 24 on `DOUT`, flips `LRCK`)
![[Pasted image 20241229041838.png]]
 
 3. So now, we look for `right justified, 24 bit` in table 4 to get the data formats. As it is mentioned that the data format is controlled by `FMT1` (1, in our case) and `FMT0` (0, in our case), we find the pin 17 as 0 (`FMT1`) and pin 18 as 1 (`FMT0`).
 4. As the supported sampling rates for the device ranges from 16-96 kHz, only the sampling frequency of `32 kHz` in Table 1 with system clock frequency of `512 fs` is allowable (since master mode does not allow `768 fs`). This means that the interface mode pins `MODE1` (pin 20) and `MODE0` (pin 19) are `0` and `1` respectively (according to Table 3).
 5. Now for the resistor values, the formula under heading `8.2.2.3` is given as `fc = 1/2πRC`. We get know about capacitance as 1μF using heading `8.2 (A)`. So,
 
```
R = 1/2π(fc)(C)
fc = 10 Hz (given)
R = 1/2π(10)(1*10^-6)
R = 15.91 kΩ ~ 16 kΩ
```

Hence we get the flag as `nite{17:0,18:1,19:1,20:0,16}

**Learnt:** Reading datasheets, FCC IDs for products

**Challenges/Wrong Approaches:** Initally, I was able to obtain the FCC ID but then got stuck, as I wasn't able to get the ADC ID. Then, I faced another issue where I was unable to find the values to put into the formula to obtain the resistance.
