## PCB์ Context Switching

๐น ๋ค์ ํ๋ฒ ์ง๊ณ  ๋์๊ฐ์!
```
ํ๋์ cpu๋(1 ์ฝ์ด) ํ๋์ task๋ง ์ํํ  ์ ์๋ค.
```

#### Context Swithching ์ด๋ ๋ฌด์์ผ๊น?
![image](https://user-images.githubusercontent.com/58067265/123517290-2319b000-d6db-11eb-9ff3-e2d53c315c8f.png)
```
๋ฉํฐํ๋ก์ธ์ค/๋ฉํฐ์ค๋ ๋ ํ๊ฒฝ์ผ๋, cpu๊ฐ task(ํ๋ก์ธ์ค/์ค๋ ๋)๋ฅผ ์คํํ๊ณ  ์๋ ์ํ์์ ์ธํฐ๋ฝํธ ์์ฒญ์ ์ํด ๋ค์ ์ฐ์ ์์์ Task๊ฐ ์คํ๋์ด์ผ ํ๋ค.
์ด๋ ๊ธฐ์กด์ Task์ํ ๋๋ ๋ ์ง์คํฐ ๊ฐ์ ๊ต์ฒดํ๋ ๊ทธ ์๊ฐ์ ๋งํ๋ค.
```

#### PCB๋ ๋ฌด์์ผ๊น?

์ปจํ์คํธ๋ฅผ ์ค์์นญํ๊ธฐ ์ํด์๋ ๊ฐ ํ๋ก์ธ์ค/์ค๋ ๋์ ์ํ๋ฅผ ์์์ผ ํ๋ค.
๊ทธ๋ฆฌ๊ณ  ์ค์์นญํ๊ธฐ ์ํด์๋ ์ด๋ค ํ๋ก์ธ์ค/์ค๋ ๋๋ฅผ ์ด๋๊น์ง ์งํํ๋์ง ์ฌ๋ถ๋ ์์์ผ ํ๋ค.

```
ํ๋ก์ธ์ค๋ฅผ ์ ์ดํ๊ธฐ ์ํ ์ ๋ณด์ ๋ชจ์์ ๋งํ๋ค. ํ๋ก์ธ์ค๊ฐ ์์ฑ๋  ๋ pcb๊ฐ ๋ง๋ค์ด์ ธ ๊ฐ ํ๋ก์ธ์ค๋ ๊ณ ์ ์ PCB๋ฅผ ๊ฐ๋๋ค. (์ค๋ ๋๋ TCB)
```

#### PCB๊ฐ ์ด๋ค ์ ๋ณด๋ฅผ ์ ์ฅํ๊ณ  ์์๊น?

![image](https://user-images.githubusercontent.com/58067265/123518871-e2be3000-d6e2-11eb-98af-64c6c07c10dc.png)

* ํ๋ก์ธ์ค ๊ณ ์  ๋ฒํธ
* ํ๋ก์ธ์ค ์ํ
  * create 
  * ready
  * waiting
  * running
  * terminated
* ํฌ์ธํฐ = ๋ค์ ์คํ๋  ํ๋ก์ธ์ค์ ํฌ์ธํฐ
* program counter = ๋ค์์ ์คํํ  ๋ช๋ น์ด์ ์ฃผ์
* ๋ ์ง์คํฐ
* cpu ์ค์ผ์ฅด๋ง ์ ๋ณด = ์ฐ์ ์์, ์ต์ข ์คํ ์๊ฐ, cpu ์ ์  ์๊ฐ
* ๋ฉ๋ชจ๋ฆฌ ๊ด๋ฆฌ ์ ๋ณด = ํด๋น ํ๋ก์ธ์ค์ ์ฃผ์ ๊ณต๊ฐ
* ํ๋ก์ธ์ค ๊ณ์  ์ ๋ณด
* ์์ถ๋ ฅ ์ํ ์ ๋ณด = ํ๋ก์ธ์ค์ ํ ๋น๋ ์์ถ๋ ฅ์ฅ์น ๋ชฉ๋ก, ์ด๋ฆฐ ํ์ผ ๋ชฉ๋ก

#### ์ธ์  Context Switching์ด ์ผ์ด๋ ๊น?
![image](https://user-images.githubusercontent.com/58067265/123519245-008c9480-d6e5-11eb-957f-ab820aee7c12.png)

* ํ๋ก์ธ์ค ์ํ
 * ์์ฑ = ํ๋ก์ธ์ค๋ฅผ ์์ฑํ๊ณ  ์๋ ๋จ๊ณ -> ?์ด๋์์ ์ฅ๋๋์ง ๊ฐ์ ์ฐพ์๋ณด์! <์ปค๋์คํ? (์ด๋ ์ปค๋ ๊ณต๊ฐ์ pcb๊ฐ ๋ง๋ค์ด์ง)>
 * ์ค๋น = ํ๋ก์ธ์ค๊ฐ cpu๋ฅผ ๊ธฐ๋ค๋ฆฌ๋ ์ํ (๋ฉ๋ชจ๋ฆฌ์ ์ ์ฌ๋๊ธฐ ์ด์ ์ ์ํ๋ก ํ์ํ ์์์ ๋ชจ๋ ์ป์ ์ํ)
 * blocked = ํ๋ก์ธ์ค๊ฐ cpu๋ฅผ ํ ๋น ๋ฐ์๋ ๋น์ฅ ์คํํ  ์ ์๋ ์ํ (์์ ์ด ์์ฒญํ i/o๊ฐ ๋ง์กฑ๋์ง ์์ ๊ธฐ๋ค๋ฆฌ๋ ์ํ)
 * terminated = ํ๋ก์ธ์ค ์คํ ์ข๋ฃ๋ก cpu ๋ฐ๋ฉ
 * suspended = ํ๋ก์ธ์ค ์ค์ง ์ํ 

```
1) ์ธํฐ๋ฝํธ ๋ฐ์ ์ (Interrupt)
2) ์คํ์ค์ธ cpu ์ฌ์ฉ ํ ๋น์ ๋ชจ๋ ์๋ชจํ์ ๋ (schedular dispatch)
3) ์์ถ๋ ฅ์ ์ํด ๋๊ธฐํ  ๋ (I/O or Event wait)
4) ์์ ํ๋ก์ธ์ค๋ฅผ ๋ง๋ค ๋
```

#### ์ด๋ป๊ฒ ์งํ์ด ๋ ๊น?
![image](https://user-images.githubusercontent.com/58067265/123520003-7bf04500-d6e9-11eb-9925-b03dfb8ee384.png)

1) cpu์์ ๋ค๋ฅธ ํ๋ก์ธ์ค๋ก ์ ํ ์, ๊ธฐ์กด ๋์ ์ค์ธ ํ๋ก์ธ์ค ์ํ๋ฅผ pcb์ ์ ์ฅ
2) ๋๊ธฐ์ด์์ ๋ค์ ํ๋ก์ธ์ค๋ฅผ ์ ํํ๊ณ  ํด๋น pcb๋ฅผ ๋ ์ง์คํฐ์ ์ ์ฌ
3) ํ๋ก๊ทธ๋จ ์นด์ดํฐ๊ฐ ๋ก๋๋์ด ํด๋น ํ๋ก์ธ์ค์ ๋ค์ ๋์ ์งํ

#### ์ค๋ฒํค๋๋?
```
์ปจํ์คํธ ์ค์์นญ์ ๊ฑธ๋ฆฐ ์๊ฐ๊ณผ ๋ฉ๋ชจ๋ฆฌ(ํ๋ก์ธ์ค๋ฅผ ์ฒ๋ฆฌํ๊ธฐ ์ํด ๋ค์ด๊ฐ๋ ๊ฐ์ ์ ์ธ ์ฒ๋ฆฌ ์๊ฐ/๋ฉ๋ชจ๋ฆฌ๋ก ์ด๊ฒ์ ์ค์ฌ์ผ ์ข๋ค!) 
```
ํ๋ก์ธ์ค ์์ ์ค์ ์ค๋ฒํค๋๋ฅผ ๊ฐ์ํด์ผ ํ๋ ์ํฉ์ ๋งํ๋ค.
๋๊ธฐ ์ํ๋ก ์ ํ์์ผฐ์ ๋ cpu๋ฅผ ๋๊ฒ ๋๋๋ ๊ฒ๋ณด๋ค ์ค๋ฒํค๋๊ฐ ์๋๋ผ๋ ๋ค๋ฅธ ํ๋ก์ธ์ค๋ฅผ ์ํ์ํค๋๊ฒ ์ข๋ค.



#### ๋ฉํฐํ๋ก์ธ์ค vs ๋ฉํฐ์ค๋ ๋์ ์ค๋ฒํค๋
os์ ์ค์ผ์ฅด๋ฌ๊ฐ ์ค์ผ์ฅด๋งํด์ฃผ๋ ๊ฒ์ด pcb์ด๊ณ  ํ๋ก์ธ์ค์ ์๋ ์ค๋ ๋ ๋ผ์ด๋ธ๋ฌ๋ฆฌ์ ์ํด ์ค์ผ์ฅด๋ง ๋๋ ๊ฒ์ด tcb์ด๋ค.  
n process ๋ก ํ๋์ ์์ ์ํ vs n thread ๋ก ํ๋์ ์์ ์ํ ์ ๊ด์ ์์ ๋น๊ตํด๋ณด์.

![image](https://user-images.githubusercontent.com/58067265/123532180-05cdfb80-d746-11eb-9fa9-9a699aa53ae9.png)

ํ๋ก์ธ์ค์ ์ค๋ ๋์ด ๋ฉ๋ชจ๋ฆฌ ๊ตฌ์กฐ์ ์ํด pcs๊ฐ ์ผ์ด๋  ๋, ์บ์๊ฐ ํ๋ฌ์๋์ง๋ง tcs๊ฐ ์ผ์ด๋๋ ๊ฒฝ์ฐ ์ ์ง๋๋ค.๊ทธ๋ก์ธํด pcb๋ฅผ ๋ณ๊ฒฝํ๋๋ฐ ๋ ๋ง์ ๋น์ฉ์ด ์๋ชจ๋๋ค.

#### ์ถ๊ฐ๋ก ์๋ฉด ๋์์ด ๋  ํค์๋
* ๋ ์ง์คํฐ

## ์ถ์ฒ
https://thebook.io/006950/ch10/01/03-01/  
https://www.crocus.co.kr/1364  








