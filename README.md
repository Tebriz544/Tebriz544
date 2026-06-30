
<!---# Gerekli kütüphaneler: rembg, torch, diffusers
from rembg import remove
from PIL import Image
import torch
from diffusers import StableDiffusionInpaintPipeline

# 1. Adım: Ürünü Arka Plandan Ayır (Maskeleme)
def urunu_ayikla(input_path, output_path):
    input_image = Image.open(input_path)
    output_image = remove(input_image) # rembg kullanılarak arka plan silinir
    output_image.save(output_path)
    return output_path

# 2. Adım: AI ile Yeni Arka Planlar Ekle
def cekim_olustur(maskelenmis_urun, prompt):
    # Stable Diffusion Inpainting pipeline'ı başlat
    pipe = StableDiffusionInpaintPipeline.from_pretrained("runwayml/stable-diffusion-inpainting")
    
    # 5 farklı prompt için döngü (Örnek: "Stüdyo", "Doğa" vb.)
    generator = pipe(prompt=prompt, image=maskelenmis_urun, mask_image=maskelenmis_urun).images[0]
    return generator

# Örnek Kullanım
urun = urunu_ayikla("urun_fotografi.jpg", "urun_maskeli.png")
sonuc = cekim_olustur(urun, "A professional studio background for a luxury t-shirt")
sonuc.show()
Tebriz544/Tebriz544 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

