#mov의 사용법 정리

mov 명령의 사용법을 총정리해보겠습니다.

일반적으로 메모리나 레지스터에 값을 읽고 쓰는 경우는 이렇습니다.
Let's summarize the usage of the mov command.

Followings are the common case when reading or writing values to memory or registers.

```
MOV REG, [mem-address]
MOV [mem-address], REG
MOV REG, REG
MOV [mem-address], constant
MOV REG, constant
```


reg는 레지스터를 말하는 것이고 상수는 0b800h같이 직접 숫자를 쓴 것을 말합니다.

mov dx, [bx]를 하면 메모리에서 16비트 값을 읽어서 dx 레지스터에 저장하는 것입니다.

그런데 한가지 주의할 것이 있습니다. mov [bx], 0ffh 라고 쓰면 어떻게 될까요?

[bx]의 메모리에 00ffh의 16비트를 쓰려는 것일까요? 아니면 0ffh의 8비트 값을 쓰려는 것일까요? 알아보려면 역시 실험을 해봐야겠지요.

"Reg" is a register, and the "constant" is a number, such as 0b800h.

``Mov dx, [bx]`` reads the 16-bit value from the memory and stores it in the dx register.

But there is one thing to watch out. Can you guess what ``mov [bx], 0ffh`` will do?

Do you want to write 16 bits value of 00ffh at the memory address of bx? Or do you want to write an 8-bit value of 0ffh? Let's run an example to find out.

```
org 100h
mov ax, 0b800h
mov ds, ax
mov bx, 0
mov cl, 'A'
mov ch, 11011111b
mov ds:[bx], cx
mov [bx+2], cx
mov si, 4
mov [bx+si], cl
mov [bx+si+2], cx
mov [bx], 0ffh
ret
```


이전 글에서 실험한 소스에 마지막으로 mov [bx], 0ffh를 추가한 것입니다. 0ffh를 쓰려는 주소는 0b8000h 이겠지요? 이 소스를 실험하기 위해서 에물레이터를 실행한 후에 에물레이터 화면 아래쪽에 있는 aux 버튼을 눌러봅니다. 또다른 메뉴가 나올겁니다. 메뉴에서 memory를 선택합니다. 그럼 아래 그림처럼 Random Access Memory라는 창이 나타납니다.
Finally, we added ``mov [bx], 0ffh`` to the source we tested in the previous chapter. The address to write 0ffh is 0b8000h. To test this source, run the emulator and then press the aux button at the bottom of the emulator screen. There will be another menu. Select memory from the menu. Then a window called "Random Access Memory" appears as shown below.

![](/assets/2522.png)

update 버튼 왼쪽에 주소 값이 보이지요? 0700:0100으로 표시되어있을 것입니다. 여기를 클릭해서 주소 값을 지우고 b800:0000을 입력하고 update 버튼을 누릅니다. 어떤가요? 우리가 데이터를 쓰려는 메모리 위치에 어떤 값들이 저장되어있는지 나타납니다. 이제 single step으로 명령 하나씩 실행해보세요. 메모리에 값들이 바뀌는걸 확인할 수 있습니다. 그리고 mov [bx], 0ffh 명령을 실행하면 16비트 값이 바뀌나요? 아니면 8비트 값이 바뀌나요?
Do you see the address value on the left side of the update button? It will be marked as 0700:0100. Click here to clear the address value, enter b800:0000 and press the update button. What happends? It shows what values ​​are stored in the memory location where we want to write the data. Now click "single step". You can see that the values ​​change in memory. And when the             ``mov [bx], 0ffh`` command is executed, does the 16 bit value change? Or does the 8-bit value change?

![](/assets/2523.png)

원래 써있던 41이라는 값이 FF로 변했습니다. 한바이트의 값만 변했습니다.

에물레이터 창에서 어셈블리 명령들이 출력된 칸을 보면 mov b.[bx], 0ffh라고 표시되는 것을 보실수 있습니다. 이 말은 mov byte ptr [bx], 0ffh를 줄여서 표시한 것입니다. byte ptr 이라는 말은 이 주소에 한 바이트만을 쓰겠다라는 표시입니다. 16비트를 쓰고 싶다면 word ptr [bx] 라고 쓰면 되지요.

그럼 mov byte ptr [bx], 0ffh 로 바꿔서도 해보고, mov word ptr [bx], 0ffh로 바꿔서도 실험해보세요. 한바이트 값이 바뀌기도 하고 두바이트 값이 바뀌기도 할 것입니다.

The original value of 41 changed to FF. Only one byte of the value has changed.

In the emulator window, you can see ``mov b.[bx], 0ffh`` in the space where assembly instructions are shown. This means that     ``mov byte ptr [bx], 0ffh`` is abbreviated. The "byte ptr" indicates that only one byte will be written to this address. If you want to write 16 bits, you can use ``word ptr [bx]``.

Then try changing it to ``mov byte ptr [bx], 0ffh``, and convert it to ``mov word ptr [bx], 0ffh``. One byte value will change and two byte values ​​will change.