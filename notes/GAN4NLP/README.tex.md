# Generative Adversarial Nets 4 NLP
GAN ได้ผลดีในงานหลากหลายแบบโดยเฉพาะงาน Computer Vision แต่ทำไม GAN ถึงไม่เป็นเทคนิคที่นิยมใน NLP เราจะมาคุยว่าทำไม GAN ถึงยากกว่าใน NLP แล้วปัจจุบันนักวิจัยพยายามแก้ปัญหานี้ด้วยวิธีใดบ้าง.    

ปัญหาหลักในการทำ GAN ในงานคือ NLP คือปกติแล้ว image จะมี output ในลักษณะ continuous แต่ text จะเป็น discrete ทำให้ ดิฟกลับไปทำ backpropagate ไม่ได้ 

ในตอนนี้มีวิธีหลักๆ อยู่สามวิธีที่จะแก้ปัญหาเรื่องการทำให้ดิฟกลับไปได้ 
* ใช้เทคนิคของพวก Reinforcement Learning (RL) มาแก้ปัญหา พวก RL มักจะเจอปัญหานี้เป็นปกติ แนวคิดจาก RL algorithm กับ policy gradients จะสามารถช่วยแก้ปัญหานี้ได้
* [Gumble-softmax approximation](https://arxiv.org/abs/1611.01144) ช่วยประมาณค่า continous จากตัวอย่างใน discrete distribution ได้ 
* พยายามเลี่ยง discrete output โดยพยายามใช้ continuous output แทน (เช่น ใช้ sentence vector แทน discrete tokens หลายๆอัน)

## RL
เราสามารถตีโจทย์ text generation ให้เป็น RL ได้ โดยมองว่า text generation เป็น state-action sequence เช่น state (s) คือ text ที่ถูก generated มาแล้ว ส่วน action คือการเลือกคำถัดไป เมื่อเลือกคำจนจบ (เช่นจบประโยค,เจอ end of sentence token) ก็ให้รางวัลว่า text ที่ generated มามีคุณภาพแค่ไหน ในบริบทของ GAN, discriminator จะมีหน้าที่ให้ reward ส่วนการเลือก action ในแต่ละ state ก็จะเป็นหน้าที่ของ policy function $\boldsymbol{\pi}(\boldsymbol{a} | \boldsymbol{s}, \boldsymbol{\theta})$  โดย 𝜃 คือ พารามิเตอร์  ส่วน output คือ distribution ของ action ต่างๆ (given state). โมเดลจะ generate text โดย sample จาก policy            
           
ถ้า **J(𝜃)** คือมาตรวัด performance เราก็ต้องการปรับพารามิเตอร์ต่างๆ เพื่อหาพารามิเตอร์ **𝜃*** ที่ให้ performance สูงสุดบน **J(𝜃)** เพื่อที่จะหา พารามิเตอร์ **𝜃*** ที่ maximize performance เราจะทำ gradient ascent: $\boldsymbol{\theta}_{t+1}=\boldsymbol{\theta}_{t}+\alpha \widehat{\nabla J\left(\boldsymbol{\theta}_{t}\right)}$ ในบริบทนี้หมวก (^) หมายความว่า gradient นี้เป็นค่าที่ถูกประมาณมา โดยใช้ concept ของ   [policy gradient theorem](https://lilianweng.github.io/lil-log/2018/04/08/policy-gradient-algorithms.html#policy-gradient-theorem): $\nabla J(\boldsymbol{\theta}) \propto \sum_{s} \mu(s) \sum_{a} q_{\pi}(s, a) \nabla \pi(a | s, \boldsymbol{\theta})$         
          
* **𝜇(s)** วัดว่า agent มีโอกาสไปที่ state **s** บ่อยแค่ไหน ถ้าหากทำตาม policy **𝜋**
* **q(s, a)** วัดคุณภาพของ action **a** ที่ทำใน state **s** 

ตอนนี้ สมการด้านขวาคือการบวกรวมของทุก  action **a** และทุก state **s** แต่เราต้องการที่จะประมาณค่าจากตัวอย่างอันเดียวได้ เช่น  a กับ s ที่ timestep t  (s_t,a_t) เราจึงต้องใช้ REINFORCE algorithm มาช่วย

เมื่อ  **𝜇(s)** คือความน่าจะเป็นที่ไปได้ที่จะอยู่ที่ state **s** ถ้าหากทำตาม policy **𝜋**  เราจะมองการบวกรวมด้านนอก(outer summation)ได้ว่าเป็น[expected value](https://en.wikipedia.org/wiki/Expected_value)ของการบวกรวมด้านใน(inner summation):                   
$\mathbb{E}_{\pi}\left[\sum_{a} q_{\pi}\left(S_{t}, a\right) \nabla \pi\left(a | S_{t}, \boldsymbol{\theta}\right)\right]$            

Note: นิยามของ expected value ของ X คือ $\mathrm{E}[X]=\sum_{i=1}^{k} x_{i} p_{i}=x_{1} p_{1}+x_{2} p_{2}+\cdots+x_{k} p_{k}$ โดยที่ p คือ prob               

ตอนนี้เราสามารถหาค่าจาก state เดียว (s_t) ได้แล้ว แล้วจะทำยังไงต่อให้หาค่าจาก action เดียวได้ action (a_t)                    
อย่าลืมว่า $\pi\left(a | S_{t}, \boldsymbol{\theta}\right)$ คือฟังชั่นที่ให้ค่าความแจกแจงของความน่าจะเป็น(probability distribution)ของแต่ละaction ที่state s_t เพราะฉะนั้นเราสามารถลดรูปของมันได้อีก เพราะsummation ของมันก็ดูคล้ายๆ expected value โดยเราจะคูณและหารสมการด้วย$\pi\left(a | S_{t}, \boldsymbol{\theta}\right)$ เราก็จะได้:            
$\mathbb{E}_{\pi}\left[q_{\pi}\left(S_{t}, A_{t}\right) \frac{\nabla \pi\left(A_{t} | S_{t}, \boldsymbol{\theta}\right)}{\pi\left(A_{t} | S_{t}, \boldsymbol{\theta}\right)}\right]$

## Reading List
[GAN - NAACL 2019](https://drive.google.com/drive/folders/1E4uHe4_TD4yDJws3t1kXJQanUFJiqpBB)                  
[Generative Adversarial Networks for Text Generation (blog post)](https://becominghuman.ai/generative-adversarial-networks-for-text-generation-part-1-2b886c8cab10)                 
[SeqGAN: Sequence Generative Adversarial Nets with Policy Gradient](https://www.aaai.org/ocs/index.php/AAAI/AAAI17/paper/download/14344/14489)
