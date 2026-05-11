# 📦 Enterprise Demand Forecasting & Smart Replenishment System
**End-to-End Data Science Project: From Machinelearning to Power BI Actionable Dashboard**

<img width="1519" height="819" alt="image" src="https://github.com/user-attachments/assets/f78592c3-9a06-41b8-8eb0-edd1c7832b71" />


## 📌 1. โปรเจกต์นี้ทำอะไร? (Project Overview)
ระบบพยากรณ์ความต้องการสินค้า (Demand Forecasting) ล่วงหน้าด้วย Machine Learning โดยใช้โมเดล **XGBoost,SARIMA,Prophet** ในการวิเคราะห์ข้อมูลยอดขายย้อนหลัง (Time Series / Lags), ฤดูกาล (Seasonality) และโปรโมชั่น 

จุดเด่นของโปรเจกต์นี้คือ **"การไม่หยุดแค่ตัวเลขพยากรณ์"** แต่ได้นำผลลัพธ์จาก AI ไปผสานเข้ากับ Business Logic ทางด้าน Supply Chain (เช่น สต็อกปัจจุบัน, สินค้าที่อยู่ระหว่างจัดส่ง, และ Lead Time) เพื่อสร้างเป็น **Interactive Dashboard บน Power BI** ที่สามารถคำนวณและแนะนำ "ยอดสั่งซื้อที่เหมาะสม" ให้กับฝ่ายจัดซื้อได้แบบอัตโนมัติ

## 🚨 2. ทำเพื่อแก้ไขปัญหาอะไร? (The Business Problem)
ในการบริหารจัดการคลังสินค้าและกระจายสินค้า ปัญหาคลาสสิกที่ทุกองค์กรต้องเจอคือ:
* **Overstock (ทุนจม):** การสั่งของมาตุนมากเกินความจำเป็นเพราะคาดการณ์ยอดขายผิดพลาด
* **Stockout (เสียโอกาสขาย):** สินค้าหมดคลังเพราะไม่ได้คำนึงถึงระยะเวลารอของ (Lead Time) ที่ต่างกันในแต่ละสินค้า (เช่น ของนำเข้าที่ต้องรอ 30-45 วัน)
* **Manual & Time-Consuming:** ทีมจัดซื้อต้องใช้เวลามหาศาลในการดึงข้อมูลยอดขาย มานั่งหักลบกับสต็อกใน Excel ทีละ SKU เพื่อทำใบสั่งซื้อ (PO)

## 💡 3. ผลลัพธ์เป็นอย่างไร? (Business Impact & Results)
โปรเจกต์นี้ได้เปลี่ยนผ่านการทำงานจาก **Reactive (ตั้งรับ) ไปสู่ Proactive (ทำงานเชิงรุก)** อย่างสมบูรณ์:
1. **Actionable Insights:** แทนที่ AI จะบอกแค่ "เดือนหน้าขายได้ 150 ชิ้น" ระบบใน Power BI จะคำนวณทะลุไปถึง Action ให้ทันทีว่า **"ต้องสั่งซื้อเพิ่ม 80 ชิ้น"**
2. **Automated Alert System:** มีการจัดกลุ่มสถานะการสั่งซื้อ (Action Status) อย่างชาญฉลาด:
   * 🔴 **สั่งซื้อด่วน! (Urgent):** เมื่อของไม่พอ และ Lead Time นานกว่า 30 วัน
   * 🟡 **สั่งซื้อปกติ (Normal Order):** เมื่อของไม่พอ และ Lead Time สั้น
   * 🟢 **รอไปก่อน (Hold):** เมื่อสต็อกปัจจุบันมีเพียงพอต่อความต้องการแล้ว
3. **Dynamic Safety Stock:** ผู้ใช้งานสามารถปรับ "เปอร์เซ็นต์เผื่อเหลือเผื่อขาด (Safety Stock Buffer)" บน Dashboard และเห็นยอดสั่งซื้อปรับเปลี่ยนตามความเสี่ยงได้แบบ Real-time
4. **Time Saving:** ลดเวลาการทำข้อมูล Data Prep และการวิเคราะห์ลงอย่างมหาศาล พร้อมนำตารางไปออกใบ PO ได้ทันที

## 🛠️ เครื่องมือที่ใช้ (Tech Stack)
* **Data Preparation & Engineering:** `Python` (`Pandas`, `NumPy`) - การทำ Data Transformation, สร้างตัวแปร Sliding Window และ Rolling Features
* **Machine Learning:** `SARIMA`,`Prophet`,`XGBoost`, `Scikit-Learn` - สำหรับการเทรนโมเดล Regression และพยากรณ์ยอดขาย
* **Data Visualization:** `Power BI` (พร้อมการเขียนสูตร `DAX`) - สำหรับสร้าง Interactive Dashboard ที่ฝ่าย Business ใช้งานได้จริง

## 📂 โครงสร้างไฟล์ใน Repository นี้
* `DemandForecastingDataset.csv`: ชุดข้อมูลตั้งต้น (Mockup Dataset) ที่จำลองยอดขายและยอดสั่งซื้อย้อนหลัง สำหรับใช้ในการสอนโมเดล
* `DemandForcasting.ipynb`: โค้ด Python ที่รวบรวมกระบวนการ Data Preparation, Feature Engineering (การสร้างตัวแปร Lags และ Seasonality) และการเทรนโมเดล Machine Learning ต่างๆ
* `PowerBI_Forecast_Dashboard_All_Products.xlsx`: ไฟล์ผลลัพธ์ที่ดึงออกมาจากโมเดล XGBoost ซึ่งประกอบไปด้วยยอดขายจริงและยอดพยากรณ์ เพื่อใช้เป็นฐานข้อมูลเชื่อมต่อเข้ากับ Power BI
* `DashboardForcasting.pbix`: ไฟล์โปรแกรม Power BI ที่ผูกสูตร DAX (Business Logic) และสร้าง Interactive Dashboard เสร็จสมบูรณ์
* *(Optional)* `dashboard_preview.png`: รูปภาพ Screenshot ของหน้า Dashboard เพื่อให้ผู้ที่เข้ามาชม Repository สามารถเห็นผลลัพธ์ได้ทันทีโดยไม่ต้องเปิดไฟล์ .pbix

---
*Developed by: Akrit Sirikhan*
