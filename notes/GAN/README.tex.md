# Generative Adversarial Nets (GAN)
GAN เป็น framework สำหรับสร้าง generative model ที่ได้รับความสนใจสูงมาก        
ใน framework นี้ generative model จะต้องสู้กับ discriminative model โดยที่ discriminative model จะต้องเรียนรู้ที่จะแยกว่าตัวอย่างที่เห็นมาจาก generative model หรือมาจาก data จริงๆ
เราสามารถมองได้ว่า generative model คือช่างทำของเก๊ที่พยายามจะสินค้าเลียนแบบให้เนียนที่สุดไม่ให้ใครจับได้ ส่วน discriminative model จะเป็นผู้ตรวจสินค้าว่าเป็นของแท้หรือไม่ สอง model นี้จะแข่งกันจนกว่าจะไม่มีใครแยกว่าอะไรคือของแท้หรือของปลอม

Note: บางครั้งคนมักจะสับสน Generative Adversarial Nets  กับ "adversarial examples"                   
"adversarial examples" คือ examples ที่คล้ายกับ data จริงแต่ model จะทำนายผิด "adversarial examples" ไม่ได้เอาไว้ train โมเดล แต่เอาไว้เป็นเครื่องมือในการวิเคราะห์โมเดล
# Reading list 
[NIPS 2016 Tutorial: Generative Adversarial Networks](https://arxiv.org/abs/1701.00160)
