 import cv2
import numpy as np

# دالة لتحويل الصورة إلى دقة أعلى
def upscale_image(image_path, scale_factor=2):
    # قراءة الصورة
    img = cv2.imread(image_path)
    if img is None:
        print("خطأ: لم يتم العثور على الصورة. تأكد من المسار.")
        return
    
    # الحصول على الأبعاد الأصلية
    height, width = img.shape[:2]
    
    # حساب الأبعاد الجديدة
    new_width = int(width * scale_factor)
    new_height = int(height * scale_factor)
    
    # تحويل الصورة باستخدام interpolation (bicubic لجودة أفضل)
    upscaled_img = cv2.resize(img, (new_width, new_height), interpolation=cv2.INTER_CUBIC)
    
    # حفظ الصورة المحولة
    output_path = "upscaled_image.jpg"  # يمكنك تغيير الاسم
    cv2.imwrite(output_path, upscaled_img)
    print(f"تم تحويل الصورة وحفظها في: {output_path}")
    
    # عرض الصورة الأصلية والمحولة (اختياري)
    cv2.imshow("Original", img)
    cv2.imshow("Upscaled", upscaled_img)
    cv2.waitKey(0)
    cv2.destroyAllWindows()

# مثال على الاستخدام: استبدل 'path_to_your_image.jpg' بمسار صورة حقيقية
upscale_image('path_to_your_image.jpg', scale_factor=2)  # scale_factor=2 يعني مضاعفة الدقة
