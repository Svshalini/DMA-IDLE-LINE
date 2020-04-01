# DMA-IDLE-LINE
TEST CODE FOR DMA-IDLE-LINE DETECTION USING UART
Steps:

1.create dma_buffer and uart_buffer with the sizes 64 and 256 respectively(the one used in this code) 
2.created temporary buffer(type buffer in live watch it can be visible) 
3.Do not use the irq handlers that are generated by the stm32(comment them )and use the one that i have used in this code.(circular .c file) 
4.set up break point at both irq handlers to understand the flow. 

FLOW CONTROL: 

1.as soon as you give the string in the terminal data will be in the dma_buffer(use live watch if needed) 
2.usart irq handler is executed. the idle line detected and Disabling DMA will force transfer complete interrupt if enabled. 
3.dma irq will be executed next and in this function the data from dma_buffer is copied to the uart_buffer(data is over written if reached the maximun size,since it is a circular buffer) 
4.in this code i have copied data from uart_buffer(check the line number 126 in dma_circular .c file and also have the close look for the 
line 127 in the same file.(127-line:for transmitting the buffer data).to buffer(which is temp buffer). 
Now we can process the data from buffer as per the requirement.

KEY POINTS:

1.uart_buffer size should be greater than the dma_buffer.
2.buffer(temp buffer) should not be less than dma_buffer(assign greater or equal size).
3.you can even assign bigger size buffers based on the requirements.

