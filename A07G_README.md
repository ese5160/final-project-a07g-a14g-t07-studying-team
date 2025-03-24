# a07g-exploring-the-CLI

* Team Number: 07
* Team Name: Studying Team
* Team Members: Guanlin Li & Xinmi Wang
* GitHub Repository URL: https://github.com/ese5160/final-project-a07g-a14g-t07-studying-team
* Description of test hardware: SamW25 Dev Board


## 1 Software Architecture



## 2 Understanding the Starter Code

1. The `InitializeSerialConsole()` provides the initialization function of the Serial Port, which initialize the UART hardware, registers, interrupts, and callback functions for USART events. The `cbufRx` defines the buffer size of the receive buffer, and the `cbufTx` defines the buffer size of the transmit buffer. These two buffers are of type circular buffer structures. 
2. `cbufRX` and `cbufTx` are initialized by the function `circular_buf_init()` which specifies the address to the buffer and the size of the buffer. The library is circular_buffer.c. 
3. The Rx and Tx characters are being stored at `rxCharacterBuffer` and `txCharacterBuffer`, where each one has the size of `RX_BUFFER_SIZE` and `TX_BUFFER_SIZE` which is 512 bytes. 
4. The interrupts are defined inside the ASF folder. 
5. 
    a. The function `usart_read_callback` is called when a character is received. <br>
    b. The function `usart_write_callback` is called when a character has been sent. 
6. The read callback attempts to put the received data that stores in `latestRx` to the buffer `cbufRx` using function `circular_buf_put2`. If `cbufRx` is not full, the insertion success, and it restarts the read job to get the next character. The write callback checks if any data could be retrieved from `cbufTx` using function `circular_buf_get`, and if success, then put the retrieved data into `latestTx` and restart the write job. 
7. 1. User types a character. TODO
   2. The character is transmitted through USART and get into the register `latestRx`. 
   3. An interrupt is called, triggering the callback function `usart_read_callback()`. 
   4. The callback function checks if the buffer `cbufRx` is full or not. 
   5. If `cbufRx` is not full, the data stored in the register `latestRx` are put into `cbufRx`, and restart the read job. 
8. 1. A string is added to the buffer `cbufTx`. TODO
   2. An interrupt is called, triggering the callback function `usart_write_callback()`. 
   3. The callback function checks if any data could be read from `cbufTx`. 
   4. If there are data in `cbufTx`, put the data in the register `latestTx`, and then restart the write job for potential future characters. 
   5. The data in `latestTx` is transmitted through USART. 
9.  It starts the thread named "CLI_TASK", and checks how many heap is free before and after the creation of this thread. Only 1 new thread is started. 

## 3 Debug Logger Module

![image](images/A07G-P3.png)

## 4 Wiretap the convo

1. Should be attached to SERCOM4. 
2. Should attach to PB10 and PB11. 

## 5 Complete the CLI

## 6 Add CLI commands
