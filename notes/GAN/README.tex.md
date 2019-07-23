# Generative Adversarial Nets (GAN)
GAN เป็น framework สำหรับสร้าง generative model ที่ได้รับความสนใจสูงมาก        
ใน framework นี้ generative model จะต้องสู้กับ discriminative model โดยที่ discriminative model จะต้องเรียนรู้ที่จะแยกว่าตัวอย่างที่เห็นมาจาก generative model หรือมาจาก data จริงๆ
เราสามารถมองได้ว่า generative model คือช่างทำของเก๊ที่พยายามจะสินค้าเลียนแบบให้เนียนที่สุดไม่ให้ใครจับได้ ส่วน discriminative model จะเป็นผู้ตรวจสินค้าว่าเป็นของแท้หรือไม่ สอง model นี้จะแข่งกันจนกว่าจะไม่มีใครแยกว่าอะไรคือของแท้หรือของปลอม

Note: บางครั้งคนมักจะสับสน Generative Adversarial Nets  กับ "adversarial examples"                   
"adversarial examples" คือ examples ที่คล้ายกับ data จริงแต่ model ทำนายผิด "adversarial examples" ไม่ได้เอาไว้ train โมเดล แต่เอาไว้เป็นเครื่องมือในการวิเคราะห์โมเดล

## Adversarial Nets Framework
ที่จริง GAN แบบเบสิคที่สุดที่สร้างบน multilayer perceptrons ก็ค่อนข้างตรงไปตรงมา generative model (G) $G\left(\boldsymbol{z} ; \theta_{g}\right)$ มี noise หรือตัวแปรแฝง (latent variables) **z** เป็น input และ$\theta_{g}$ เป็น parameters ส่วน discriminative model (D) $D\left(\boldsymbol{x} ; \theta_{d}\right)$ มีตัวแปรสังเกตได้ (observed variable) เป็น input และ$\theta_{g}$ เป็น parameters ค่าที่ D พ่นออกมาาแสดงถึงโอกาสที่ **x** น่าจะมาจาก data จริงๆ ไม่ได้ถูก G สร้างขึ้นมา  ทั้งนี้ D และ G ต้องเป็น [differentiable function](https://en.wikipedia.org/wiki/Differentiable_function) คือต้องสามารถดิฟได้          
                      
เราต้องการฝึก D ให้ maximize โอกาสที่ D ทำนายถูกว่า **x** เป็นของแท้ ในขณะเดียวกันเราต้องการฝึก G ให้ minimize โอกาสที่ D ทำนายถูกว่า G(z) เป็นของปลอม คือต้องการ minimize ให้ $\log (1-D(G(\boldsymbol{z})))$ มีค่าน้อยที่สุด  (ถ้า G หลอก D ได้บ่อยๆ $1-D(G(\boldsymbol{z}$ จะมีค่าใกล้เคียง 0) เราสามารถจัดเกมการแข่งของ G และ D ให้อยู่ในรูปของฟังชั่น V(G,D) ได้: $\min _{G} \max _{D} V(D, G)=\mathbb{E}_{\boldsymbol{x} \sim p_{\text { data }}(\boldsymbol{x})}[\log D(\boldsymbol{x})]+\mathbb{E}_{\boldsymbol{z} \sim p_{\boldsymbol{z}}}(\boldsymbol{z})[\log (1-D(G(\boldsymbol{z})))]$ โดยเวลา train จะสลับกันระหว่างฝั่ง D กับ G โดยจะเทรน D จำนวน *k* ครั้งและ G จำนวน 1 ครั้งสลับกันไปเรื่อยๆเพื่อให้มี D ที่แยกแยะเก่งและค่อยๆให้ G พัฒนาไปเรื่อยๆ                  

และนี่คือไอเดียแกนหลักของ GAN แต่สมการข้างบนอาจใช้จริงไม่ดีนัก เพราะทำให้ gradient ของฝั่ง G ไม่พอในตอนแรกๆ ที่ G ปลอมไม่เนียนแต่ D แยกแยะเก่งจะทำให้ $D(G(\boldsymbol{z})))$ พ่นค่าใกล้ 0 (อย่าลืมว่า 1 คือของแท้ 0 คือของปลอม) และทำให้ $\log (1-D(G(\boldsymbol{z})))$ ใกล้ 0 เหมือนกันทำให้ไม่มี  gradient ไปเปลี่ยน weight ใน model  เพราะฉะนั้นถ้าหากต้องการนำไปใช้จริงให้ได้ผลดีต้องมีการเปลี่ยนแปลงเพิ่มเติมไปอีก

## Reading list แนะนำ 
[NIPS 2016 Tutorial: Generative Adversarial Networks](https://arxiv.org/abs/1701.00160)
[Generative Adversarial Nets - NIPS 2014 Proceedings](https://papers.nips.cc/paper/5423-generative-adversarial-nets.pdf)
