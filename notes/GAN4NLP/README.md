# Generative Adversarial Nets 4 NLP
GAN ได้ผลดีในงานหลากหลายแบบโดยเฉพาะงาน Computer Vision แต่ทำไม GAN ถึงไม่เป็นเทคนิคที่นิยมใน NLP เราจะมาคุยว่าทำไม GAN ถึงยากกว่าใน NLP แล้วปัจจุบันนักวิจัยพยายามแก้ปัญหานี้ด้วยวิธีใดบ้าง.    

ปัญหาหลักในการทำ GAN ในงานคือ NLP คือปกติแล้ว image จะมี output ในลักษณะ continuous แต่ text จะเป็น discrete ทำให้ ดิฟกลับไปทำ backpropagate ไม่ได้ 

ในตอนนี้มีวิธีหลักๆ อยู่สามวิธีที่จะแก้ปัญหาเรื่องการทำให้ดิฟกลับไปได้ 
* ใช้เทคนิคของพวก Reinforcement Learning (RL) มาแก้ปัญหา พวก RL มักจะเจอปัญหานี้เป็นปกติ แนวคิดจาก RL algorithm กับ policy gradients จะสามารถช่วยแก้ปัญหานี้ได้
* [Gumble-softmax approximation](https://arxiv.org/abs/1611.01144) ช่วยประมาณค่า continous จากตัวอย่างใน discrete distribution ได้ 
* พยายามเลี่ยง discrete output โดยพยายามใช้ continuous output แทน (เช่น ใช้ sentence vector แทน discrete tokens หลายๆอัน)

## RL
เราสามารถตีโจทย์ text generation ให้เป็น RL ได้ โดยมองว่า text generation เป็น state-action sequence เช่น state (s) คือ text ที่ถูก generated มาแล้ว ส่วน action คือการเลือกคำถัดไป เมื่อเลือกคำจนจบ (เช่นจบประโยค,เจอ end of sentence token) ก็ให้รางวัลว่า text ที่ generated มามีคุณภาพแค่ไหน ในบริบทของ GAN, discriminator จะมีหน้าที่ให้ reward ส่วนการเลือก action ในแต่ละ state ก็จะเป็นหน้าที่ของ policy function <img src="/notes/GAN4NLP/tex/71eaf018b849f00f26091e219e9ef9f0.svg?invert_in_darkmode&sanitize=true" align=middle width=65.38039694999999pt height=24.65753399999998pt/>  โดย 𝜃 คือ พารามิเตอร์  ส่วน output คือ distribution ของ action ต่างๆ (given state). โมเดลจะ generate text โดย sample จาก policy            
           
ถ้า **J(𝜃)** คือมาตรวัด performance เราก็ต้องการปรับพารามิเตอร์ต่างๆ เพื่อหาพารามิเตอร์ **𝜃*** ที่ให้ performance สูงสุดบน **J(𝜃)** เพื่อที่จะหา พารามิเตอร์ **𝜃*** ที่ maximize performance เราจะทำ gradient ascent: <img src="/notes/GAN4NLP/tex/2b076affa2b854c435b9ef26b9f6ca35.svg?invert_in_darkmode&sanitize=true" align=middle width=155.79307755pt height=36.56024129999999pt/> ในบริบทนี้สัญลักษณ์หมวก (^) หมายความว่า gradient นี้เป็นค่าที่ถูกประมาณมา โดยใช้ concept ของ   [policy gradient theorem](https://lilianweng.github.io/lil-log/2018/04/08/policy-gradient-algorithms.html#policy-gradient-theorem): <img src="/notes/GAN4NLP/tex/c48fce8bebc6bb658babfd5ff2ccecc2.svg?invert_in_darkmode&sanitize=true" align=middle width=284.3723025pt height=24.657735299999988pt/>         
          

## Reading List
[GAN - NAACL 2019](https://drive.google.com/drive/folders/1E4uHe4_TD4yDJws3t1kXJQanUFJiqpBB)                  
[Generative Adversarial Networks for Text Generation (blog post)](https://becominghuman.ai/generative-adversarial-networks-for-text-generation-part-1-2b886c8cab10)                 
[SeqGAN: Sequence Generative Adversarial Nets with Policy Gradient](https://www.aaai.org/ocs/index.php/AAAI/AAAI17/paper/download/14344/14489)
