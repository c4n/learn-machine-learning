# Generative Adversarial Nets 4 NLP
GAN ได้ผลดีในงานหลากหลายแบบโดยเฉพาะงาน Computer Vision แต่ทำไม GAN ถึงไม่เป็นเทคนิคที่นิยมใน NLP เราจะมาคุยว่าทำไม GAN ถึงยากกว่าใน NLP แล้วปัจจุบันนักวิจัยพยายามแก้ปัญหานี้ด้วยวิธีใดบ้าง.    

ปัญหาหลักในการทำ GAN ในงานคือ NLP คือปกติแล้ว image จะมี output ในลักษณะ continuous แต่ text จะเป็น discrete ทำให้ ดิฟกลับไปทำ backpropagate ไม่ได้ 

ในตอนนี้มีวิธีหลักๆ อยู่สามวิธีที่จะแก้ปัญหาเรื่องการทำให้ดิฟกลับไปได้ 
* ใช้เทคนิคของพวก Reinforcement Learning (RL) มาแก้ปัญหา พวก RL มักจะเจอปัญหานี้เป็นปกติ แนวคิดจาก RL algorithm กับ policy gradients จะสามารถช่วยแก้ปัญหานี้ได้
* [Gumble-softmax approximation](https://arxiv.org/abs/1611.01144) ช่วยประมาณค่า continous จากตัวอย่างใน discrete distribution ได้ 
* พยายามเลี่ยง discrete output โดยพยายามใช้ continuous output แทน (เช่น ใช้ sentence vector แทน discrete tokens หลายๆอัน)

## RL
เราสามารถตีโจทย์ text generation ให้เป็น RL ได้ โดยมองว่า text generation เป็น state-action sequence เช่น state (s) คือ text ที่ถูก generated มาแล้ว ส่วน action คือการเลือกคำถัดไป เมื่อเลือกคำจนจบ (เช่นจบประโยค,เจอ end of sentence token) ก็ให้รางวัลว่า text ที่ generated มามีคุณภาพแค่ไหน ในบริบทของ GAN, discriminator จะมีหน้าที่ให้ reward ส่วนการเลือก action ในแต่ละ state ก็จะเป็นหน้าที่ของ policy function <img src="/notes/GAN4NLP/tex/71eaf018b849f00f26091e219e9ef9f0.svg?invert_in_darkmode&sanitize=true" align=middle width=65.38039694999999pt height=24.65753399999998pt/>  โดย 𝜃 คือ พารามิเตอร์  ส่วน output คือ distribution ของ action ต่างๆ (given state). โมเดลจะ generate text โดย sample จาก policy            
           
ถ้า **J(𝜃)** คือมาตรวัด performance เราก็ต้องการปรับพารามิเตอร์ต่างๆ เพื่อหาพารามิเตอร์ **𝜃*** ที่ให้ performance สูงสุดบน **J(𝜃)** เพื่อที่จะหา พารามิเตอร์ **𝜃*** ที่ maximize performance เราจะทำ gradient ascent: <img src="/notes/GAN4NLP/tex/2b076affa2b854c435b9ef26b9f6ca35.svg?invert_in_darkmode&sanitize=true" align=middle width=155.79307755pt height=36.56024129999999pt/> ในบริบทนี้หมวก (^) หมายความว่า gradient นี้เป็นค่าที่ถูกประมาณมา โดยใช้ concept ของ   [policy gradient theorem](https://lilianweng.github.io/lil-log/2018/04/08/policy-gradient-algorithms.html#policy-gradient-theorem): <img src="/notes/GAN4NLP/tex/c48fce8bebc6bb658babfd5ff2ccecc2.svg?invert_in_darkmode&sanitize=true" align=middle width=284.3723025pt height=24.657735299999988pt/>         
          
* **𝜇(s)** วัดว่า agent มีโอกาสไปที่ state **s** บ่อยแค่ไหน ถ้าหากทำตาม policy **𝜋**
* **q(s, a)** วัดคุณภาพของ action **a** ที่ทำใน state **s** 

ตอนนี้ สมการด้านขวาคือการบวกรวมของทุก  action **a** และทุก state **s** แต่เราต้องการที่จะประมาณค่าจากตัวอย่างอันเดียวได้ เช่น  a กับ s ที่ timestep t  (s_t,a_t) เราจึงต้องใช้ REINFORCE algorithm มาช่วย

เมื่อ  **𝜇(s)** คือความน่าจะเป็นที่ไปได้ที่จะอยู่ที่ state **s** ถ้าหากทำตาม policy **𝜋**  เราจะมองการบวกรวมด้านนอก(outer summation)ได้ว่าเป็น[expected value](https://en.wikipedia.org/wiki/Expected_value)ของการบวกรวมด้านใน(inner summation):                   
<img src="/notes/GAN4NLP/tex/5438c2fb90db561dcf0582b8a64a2bdc.svg?invert_in_darkmode&sanitize=true" align=middle width=211.55697584999996pt height=24.657735299999988pt/>            

Note: นิยามของ expected value ของ X คือ <img src="/notes/GAN4NLP/tex/d80a6cf59402c36f447decf63e8d5c10.svg?invert_in_darkmode&sanitize=true" align=middle width=327.18282465pt height=32.51169900000002pt/> โดยที่ p คือ prob               

ตอนนี้เราสามารถหาค่าจาก state เดียว (s_t) ได้แล้ว แล้วจะทำยังไงต่อให้หาค่าจาก action เดียวได้ action (a_t)                    
อย่าลืมว่า <img src="/notes/GAN4NLP/tex/7dc718cfc361109793ac341baea5a8a5.svg?invert_in_darkmode&sanitize=true" align=middle width=71.67427409999999pt height=24.65753399999998pt/> คือฟังชั่นที่ให้ค่าความแจกแจงของความน่าจะเป็น(probability distribution)ของแต่ละaction ที่state s_t เพราะฉะนั้นเราสามารถลดรูปของมันได้อีก เพราะsummation ของมันก็ดูคล้ายๆ expected value โดยเราจะคูณและหารสมการด้วย<img src="/notes/GAN4NLP/tex/7dc718cfc361109793ac341baea5a8a5.svg?invert_in_darkmode&sanitize=true" align=middle width=71.67427409999999pt height=24.65753399999998pt/> เราก็จะได้:        
<img src="/notes/GAN4NLP/tex/9eb09a612438d8960287f4c92b23be22.svg?invert_in_darkmode&sanitize=true" align=middle width=276.3996113999999pt height=37.80850590000001pt/>                      
<img src="/notes/GAN4NLP/tex/73d7a61c2deba672dbf12f6ca373c70d.svg?invert_in_darkmode&sanitize=true" align=middle width=191.57973779999998pt height=37.80850590000001pt/>

ตอนนี้เราสามารถประมาณค่าของgradientของแต่ละตัวอย่าง(s_t,a_t)ของtimestep tได้แล้ว ถ้าเราเอา<img src="/notes/GAN4NLP/tex/31a441b8de4d0ef22eb966c88a5963af.svg?invert_in_darkmode&sanitize=true" align=middle width=17.890435199999988pt height=22.465723500000017pt/> มาแทน <img src="/notes/GAN4NLP/tex/2de1d121ec1048dd7e95b343d11b5cef.svg?invert_in_darkmode&sanitize=true" align=middle width=73.07526105pt height=24.65753399999998pt/> เราจะสามารถจัดให้อยู่ในรูปของ REINFORCEMENT update ได้: <img src="/notes/GAN4NLP/tex/5902e7fea0765cefe79bdb1c506e27a4.svg?invert_in_darkmode&sanitize=true" align=middle width=204.70508189999998pt height=33.20539859999999pt/>

![ภาพ REINFORCE algorithm ของ Sutton & Barto](https://i.stack.imgur.com/PL8Lk.png "ภาพ REINFORCE algorithm ของ Sutton & Barto")
                
**จะจับใส่GANยังไง?**              
* discriminative model: input คือ ประโยค output บอกว่าประโยคจริงหรือปลอม ซึ่งค่า output เนี่ย generative model จะเอากลับไปอัพเดท policy
* generative model: <img src="/notes/GAN4NLP/tex/f57b64c2994d88ab03f3373049d93cad.svg?invert_in_darkmode&sanitize=true" align=middle width=61.92544544999999pt height=24.65753399999998pt/> โดยที่ <img src="/notes/GAN4NLP/tex/27e556cf3caa0673ac49a8f0de3c73ca.svg?invert_in_darkmode&sanitize=true" align=middle width=8.17352744999999pt height=22.831056599999986pt/> ก็คือพารามิเตอร์ของneural nets ฝั่ง generative model
               

[Monte Carlo](https://en.wikipedia.org/wiki/Monte_Carlo_method)
## Reading List
[GAN - NAACL 2019](https://drive.google.com/drive/folders/1E4uHe4_TD4yDJws3t1kXJQanUFJiqpBB)                  
[Generative Adversarial Networks for Text Generation (blog post)](https://becominghuman.ai/generative-adversarial-networks-for-text-generation-part-1-2b886c8cab10)                 
[SeqGAN: Sequence Generative Adversarial Nets with Policy Gradient](https://www.aaai.org/ocs/index.php/AAAI/AAAI17/paper/download/14344/14489)
