# Generative Adversarial Nets 4 NLP
GAN ได้ผลดีในงานหลากหลายแบบโดยเฉพาะงาน Computer Vision แต่ทำไม GAN ถึงไม่เป็นเทคนิคที่นิยมใน NLP เราจะมาคุยว่าทำไม GAN ถึงยากกว่าใน NLP แล้วปัจจุบันนักวิจัยพยายามแก้ปัญหานี้ด้วยวิธีใดบ้าง.    

ปัญหาหลักในการทำ GAN ในงานคือ NLP คือปกติแล้ว image จะมี output ในลักษณะ continuous แต่ text จะเป็น discrete ทำให้ ดิฟกลับไปทำ backpropagate ไม่ได้ 

ในตอนนี้มีวิธีหลักๆ อยู่สามวิธีที่จะแก้ปัญหาเรื่องการทำให้ดิฟกลับไปได้ 
* ใช้เทคนิคของพวก Reinforcement Learning (RL) มาแก้ปัญหา พวก RL มักจะเจอปัญหานี้เป็นปกติ แนวคิดจาก RL algorithm กับ policy gradients จะสามารถช่วยแก้ปัญหานี้ได้
* [Gumble-softmax approximation](https://arxiv.org/abs/1611.01144) ช่วยประมาณค่า continous จากตัวอย่างใน discrete distribution ได้ 
* พยายามเลี่ยง discrete output โดยพยายามใช้ continuous output แทน


## Reading List
[GAN - NAACL 2019](https://drive.google.com/drive/folders/1E4uHe4_TD4yDJws3t1kXJQanUFJiqpBB)                  
[Generative Adversarial Networks for Text Generation (blog post)](https://becominghuman.ai/generative-adversarial-networks-for-text-generation-part-1-2b886c8cab10)
