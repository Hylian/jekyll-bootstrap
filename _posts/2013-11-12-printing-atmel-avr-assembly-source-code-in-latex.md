---
layout: post
title: "Printing Atmel AVR Assembly source code in LaTeX"
description: ""
category: "LaTeX"
tags: []
---
{% include JB/setup %}

My current class has assignments in AVR Assembly and I've gotten source code printing of Atmel AVR Assembly working in LaTeX with color highlighting.

Here's how it works:

The [listings](https://en.wikibooks.org/wiki/LaTeX/Source_Code_Listings) module in LaTeX allows for printing of source code for a variety of different languages, but AVR Assembly is not one of them. I needed to go ahead and define the language highlighting myself. Assembly is fairly simple, so I just needed to define keywords for all the instructions and registers.

I found a set of keywords defined by Nils Michelsen online, and edited it so that we can highlight instructions, registers, and directives separately:

	%%
	%% AVRASM definition (c) 2005 Nils Michelsen
	%% Modified 2013 by Edward Shin
	%%
	\lst@definelanguage{AVR}{
	morekeywords=[1]{adc,add,adiw,sub,subi,sbc,sbiw,and,andi,or,ori,eor,com,
			neg,sbr,cbr,inc,dec,tst,clr,ser,mul,muls,mulsu,fmul,fmuls,
			fmulsu,rjmp,ijmp,eijmp,jmp,rcall,icall,eicall,call,ret,
			reti,cpse,cp,cpc,cpi,sbrc,sbrs,sbic,sbis,brbs,brbc,breq,
			brne,brcs,brcc,brsh,brlo,brmi,brpl,brge,brlt,brhs,brhc,
			brts,brtc,brvs,brvc,brie,brid,mov,movw,ldi,lds,ld,ldd,st,
			sts,std,lpm,elpm,spm,in,out,push,pop,lsl,lsr,rol,ror,asr,
			swap,bset,bclr,sbi,cbi,bst,bld,sec,sen,cln,sez,clz,sei,cli,
			ses,cls,sev,clv,set,clt,seh,clh,break,nop,sleep,wdr},%
	morekeywords=[2]{X,Y,Z,r0,r1,r2,r3,r4,r5,r6,r7,r8,r9,r10,r11,r12,r13,r14,
			r15,r16,r17,r18,r19,r20,r21,r22,r23,r24,r25,r26,r27,r28,r29,
			r30,r31,tccr3a,tccr3b,tcnt3h,tcnt3l,ocr3ah,ocr3al,ocr3bh,
			ocr3bl,icr3h,icr3l,etimsk,etifr,pcmsk1,pcmsk0,clkpr,sreg,
			sph,spl,ucsr1c,ubrr1h,eimsk,gimsk,gicr,gifr,timsk,tifr,
			spmcr,emcucr,mcucsr,tccr0,tcnt0,ocr0,sfior,tccr1a,tccr1b,
			tcnt1h,tcnt1l,ocr1ah,ocr1al,ocr1bh,ocr1bl,tccr2,assr,icr1h,
			icr1l,tcnt2,ocr2,wdtcr,ubrrhi,ucsroc,ubrroh,eearh,eearl,
			eedr,eecr,porta,ddra,pina,portb,ddrb,pinb,portc,ddrc,pinc,
			portd,ddrd,pind,spdr,spsr,spcr,udr0,udr,ucsr0a,usrucsr0b,ucr,
			ubrr0,ubrr0l,ubrr,acsr,porte,ddre,pine,osccal,udr1,ucsr1a,
			ucsr1b,ubrr1,ubrr1l,com3a1,com3a0,com3b1,com3b0,foc3a,foc3b,
			wgm31,wgm30,icnc3,ices3,wgm33,wgm32,cs32,cs31,cs30,icf3,
			ocf3a,ocf3b,tov3,pcint15,pcint14,pcint13,pcint12,pcint11,
			pcint10,pcint9,pcint8,pcint7,pcint6,pcint5,pcint4,pcint3,
			pcint2,pcint1,pcint0,CLKPCE,CLKPS3,CLKPS2,CLKPS1,CLKPS0,INT1,
			INT0,INT2,PCIE1,PCIE0,IVSEL,IVCE,INTF1,INTF0,INTF2,PCIF1,PCIF0,
			TOIE1,OCIE1A,OCIE1B,OCIE2,TICIE1,TOIE2,TOIE0,OCIE0,TOV1,OCF1A,
			OCF1B,OCF2,ICF1,TOV2,TOV0,OCF0,SPMIE,RWWSB,ASB,RWWSRE,ASRE,
			BLBSET,PGWRT,PGERS,SPMEN,SM0,SRL2,SRL1,SRL0,SRW01,SRW00,SRW11,
			ISC2,SRE,SRW,SRW10,SE,SM,SM1,ISC11,ISC10,ISC01,ISC00,JTD,SM2,
			JTRF,WDRF,BORF,EXTRF,PORF,FOC0,WGM00,PWM0,COM01,COM00,WGM01,
			CTC0,CS02,CS01,CS00,TSM,XMBK,XMM2,XMM1,XMM0,PUD,PSR2,PSR10,PSR1,
			PSR0,COM1A1,COM1A0,COM1B1,COM1B0,FOC1A,FOC1B,PWM11,WGM11,PWM10,
			WGM10,ICNC1,ICES1,CTC11,WGM13,CTC10,WGM12,CTC1,CS12,CS11,CS10,
			FOC2,WGM20,PWM2,COM21,COM20,WGM21,CTC2,CS22,CS21,CS20,AS2,
			TCN2UB,OCR2UB,TCR2UB,WDTOE,WDCE,WDE,WDP2,WDP1,WDP0,EERIE,EEMWE,
			EEWE,EERE,PORTA7,PORTA6,PORTA5,PORTA4,PORTA3,PORTA2,PORTA1,PORTA0,
			DDA7,DDA6,DDA5,DDA4,DDA3,DDA2,DDA1,DDA0,PINA7,PINA6,PINA5,PINA4,
			PINA3,PINA2,PINA1,PINA0,PORTB7,PORTB6,PORTB5,PORTB4,PORTB3,PORTB2,
			PORTB1,PORTB0,DDB7,DDB6,DDB5,DDB4,DDB3,DDB2,DDB1,DDB0,PINB7,PINB6,
			PINB5,PINB4,PINB3,PINB2,PINB1,PINB0,PORTC7,PORTC6,PORTC5,
			PORTC4,PORTC3,PORTC2,PORTC1,PORTC0,DDC7,DDC6,DDC5,DDC4,
			DDC3,DDC2,DDC1,DDC0,PINC7,PINC6,PINC5,PINC4,PINC3,PINC2,
			PINC1,PINC0,PORTD7,PORTD6,PORTD5,PORTD4,PORTD3,PORTD2,
			PORTD1,PORTD0,DDD7,DDD6,DDD5,DDD4,DDD3,DDD2,DDD1,
			DDD0,PIND7,PIND6,PIND5,PIND4,PIND3,PIND2,PIND1,PIND0,
			PORTE2,PORTE1,PORTE0,DDE2,DDE1,DDE0,PINE2,PINE1,PINE0,
			RXC,TXC,UDRE,FE,OR,U2X,RXC0,TXC0,UDRE0,FE0,OR0,DOR0,
			PE0,U2X0,MPCM0,RXC1,TXC1,UDRE1,FE1,OR1,DOR1,PE1,U2X1,
			MPCM1,SPIE,SPE,DORD,MSTR,CPOL,CPHA,SPR1,SPR0,SPIF,WCOL,SPI2X,
			RXCIE,TXCIE,UDRIE,RXEN,TXEN,CHR9,UCSZ2,RXB8,TXB8,RXCIE0,TXCIE0,
			UDRIE0,RXEN0,TXEN0,CHR90,UCSZ02,RXB80,TXB80,RXCIE1,TXCIE1,
			UDRIE1,RXEN1,TXEN1,CHR91,UCSZ12,RXB81,TXB81,URSEL0,UMSEL0,
			UPM01,UPM00,USBS0,UCSZ01,UCSZ00,UCPOL0,URSEL1,UMSEL1,UPM11,
			UPM10,USBS1,UCSZ11,UCSZ10,UCPOL1,ACD,AINBG,ACBG,ACO,ACI,ACIE,
			ACIC,ACIS1,ACIS0,BLB12,BLB11,BLB02,BLB01,XL,XH,YL,YH,ZL,
			ZH,RAMEND,EEPROMEND,FLASHEND,SMALLBOOTSTART,SECONDBOOTSTART,
			THIRDBOOTSTART,LARGEBOOTSTART,BOOTSTART,PAGESIZE,INT0addr,
			INT1addr,INT2addr,PCINT0addr,PCINT1addr,TIMER3CAPTaddr,
			TIMER3COMPAaddr,TIMER3COMPBaddr,TIMER3OVFaddr,TIMER2COMPaddr,
			TIMER2OVFaddr,TIMER1CAPTaddr,TIMER1COMPAaddr,TIMER1COMPBaddr,
			TIMER1OVFaddr,TIMER0COMPaddr,TIMER0OVFaddr,SPISTCaddr,
			USART0RXCaddr,USART1RXCaddr,USART0UDREaddr,USART1UDREaddr,
			USART0TXCaddr,USART1TXCaddr,EE_RDYaddr,ANA_CMPaddr,
			SPM_RDYadd,mcucr,ubrr0h,ucsr0c,ucsr0b},%
	morekeywords=[3]{org,def,equ,db,include,dseg,cseg,eseg},%
	sensitive=f,%
	morecomment=[l];,%
	}[keywords,comments,strings]%

This definition goes into the 'lstlang.sty' file within the listings module.

Now, in my tex file, I configured the listings module to use this definition:

	\definecolor{MyDarkGreen}{rgb}{0.0,0.4,0.0} % This is the color used for comments
	\lstloadlanguages{AVR}%
	\lstset{language=AVR, % AVR 8-bit Assembler
		frame=single, % Single frame around code
		basicstyle=\small\ttfamily, % Use small true type font
		keywordstyle=\color{Blue}\bf, % Instructions in blue, bold
		keywordstyle=[2]\color{Orange}, % Registers and ports in orange
		keywordstyle=[3]\color{Purple}, % Directives in purple
		commentstyle=\usefont{T1}{pcr}{m}{sl}\color{MyDarkGreen}\small,
		tabsize=5, % 5 spaces per tab
		numbers=left, % Line numbers on left
		firstnumber=1, % Line numbers start with line 1
		numberstyle=\tiny\color{Blue}, % Line numbers are blue and small
		stepnumber=5 % Line numbers go in steps of 5
		}
	
	% Creates a new command to include an asm script, 
	% the first parameter is the filename of the program (without .asm),
	% the second parameter is the caption
	\newcommand{\avrasm}[2]{
	\begin{itemize}
	\item[]\lstinputlisting[caption=#2,label=#1]{#1.asm}
	\end{itemize}
	}

Now, I can just place a main.asm file in the same directory, and call it with `\avrasm{main}{comment}`. The output looks like this:

![AVR ASM listings example](assets/avrasm.png)