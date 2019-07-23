# Generative Adversarial Nets (GAN)
GAN เป็น framework สำหรับสร้าง generative model ที่ได้รับความสนใจสูงมาก        
ใน framework นี้ generative model จะต้องสู้กับ discriminative model โดยที่ discriminative model จะต้องเรียนรู้ที่จะแยกว่าตัวอย่างที่เห็นมาจาก generative model หรือมาจาก data จริงๆ
เราสามารถมองได้ว่า generative model คือช่างทำของเก๊ที่พยายามจะสินค้าเลียนแบบให้เนียนที่สุดไม่ให้ใครจับได้ ส่วน discriminative model จะเป็นผู้ตรวจสินค้าว่าเป็นของแท้หรือไม่ สอง model นี้จะแข่งกันจนกว่าจะไม่มีใครแยกว่าอะไรคือของแท้หรือของปลอม

Note: บางครั้งคนมักจะสับสน Generative Adversarial Nets  กับ "adversarial examples"                   
"adversarial examples" คือ examples ที่คล้ายกับ data จริงแต่ model ทำนายผิด "adversarial examples" ไม่ได้เอาไว้ train โมเดล แต่เอาไว้เป็นเครื่องมือในการวิเคราะห์โมเดล

## Adversarial Nets Framework
ที่จริง GAN แบบเบสิคที่สุดที่สร้างบน multilayer perceptrons ก็ค่อนข้างตรงไปตรงมา generative model (G) <img src="/notes/GAN/tex/d310df9ad2d3171d4bccde0f9c9054aa.svg?invert_in_darkmode&sanitize=true" align=middle width=60.93771089999999pt height=24.65753399999998pt/> มี noise หรือตัวแปรแฝง (latent variables) **z** เป็น input และ<img src="/notes/GAN/tex/6d30287d7e670ef8e7301003a68b62b1.svg?invert_in_darkmode&sanitize=true" align=middle width=14.54286239999999pt height=22.831056599999986pt/> เป็น parameters ส่วน discriminative model (D) <img src="/notes/GAN/tex/c55ebcdd63e4aef1038201b333945f55.svg?invert_in_darkmode&sanitize=true" align=middle width=63.11241419999999pt height=24.65753399999998pt/> มีตัวแปรสังเกตได้ (observed variable) เป็น input และ<img src="/notes/GAN/tex/6d30287d7e670ef8e7301003a68b62b1.svg?invert_in_darkmode&sanitize=true" align=middle width=14.54286239999999pt height=22.831056599999986pt/> เป็น parameters ค่าที่ D พ่นออกมาาแสดงถึงโอกาสที่ **x** น่าจะมาจาก data จริงๆ ไม่ได้ถูก G สร้างขึ้นมา  ทั้งนี้ D และ G ต้องเป็น[differentiable function](https://en.wikipedia.org/wiki/Differentiable_function) คือต้องสามารถดิฟได้          
                      
เราต้องการ maximize โอกาสที่ D ทำนายถูกว่า **x** เป็นของแท้หรือของปลอม ในขณะเดียวกันเราต้องการ  

## Reading list แนะนำ 
[NIPS 2016 Tutorial: Generative Adversarial Networks](https://arxiv.org/abs/1701.00160)
