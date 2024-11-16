[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/rtPGwteW)
# First_Task
First_Task for C

如下图所示为流水灯控制原理图，请使用C语言编写逻辑代码，实现从左到右的流水灯，间隔时间为500ms。

![water_led](image.png)

示例代码如下：请在 task.c 中编写你的代码。


```
void delay_ms(unsigned int x)  // 延时函数
{
    unsigned int i,j;
    if(x==1000)
    {
        for(i=0;i<19601;i++)//延时1s
        {
            for(j=5;j>0;j--);
        }
    }
    else while(x--)for(j=115;j>0;j--);
}

// tips: 原理图当中led为低电平点亮，比如点亮LED2,代码为： P0 = 0xFE (1111 1110)


  #include "stm32f10x.h"   // Device header
#include "delay.h"

int main(void)
{
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA,ENABLE);
	
	GPIO_InitTypeDef GPIO_Initstrructure;
	GPIO_Initstrructure.GPIO_Mode = GPIO_Mode_Out_PP;
	GPIO_Initstrructure.GPIO_Pin = GPIO_Pin_All;
	GPIO_Initstrructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOA,&GPIO_Initstrructure);
	 
	while (1)
	{
		GPIO_Write(GPIOA,~0x0001);  //0000 0000 0000 0001 
		Delay_ms(500);
		GPIO_Write(GPIOA,~0x0002);  //0000 0000 0000 0010 
		Delay_ms(500);
		GPIO_Write(GPIOA,~0x0004);  //0000 0000 0000 0100 
		Delay_ms(500);
		GPIO_Write(GPIOA,~0x0008);  //0000 0000 0000 1000 
		Delay_ms(500);
		GPIO_Write(GPIOA,~0x0010);  //0000 0000 0001 0000 
		Delay_ms(500);
		GPIO_Write(GPIOA,~0x0020);  //0000 0000 0010 0000 
		Delay_ms(500);
		GPIO_Write(GPIOA,~0x0040);  //0000 0000 0100 0000 
		Delay_ms(500);
		GPIO_Write(GPIOA,~0x0080);  //0000 0000 1000 0000 
		Delay_ms(500);
	}
}

    return 0;
}
```

