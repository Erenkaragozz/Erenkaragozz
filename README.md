# Selam, ben Eren 👋

🎮 Dijital Oyun Tasarımı öğrencisiyim. **Unity ve Unreal Engine** ile oyunlar ve mobil/arka uç uygulamalar geliştiriyorum.  
Yaratıcı fikirleri oynanabilir deneyimlere dönüştürmeyi seviyorum. ⚡

---

## 🧠 Hakkımda
🎓 Doğuş Üniversitesi, Dijital Oyun Tasarımı 3. sınıf öğrencisiyim  
👾 Doğuş Üniversitesi Dijital Oyun Tasarımı kulübü yönetim kadrosundayım ve aynı zamanda sosyal medya yöneticisiyim.
🎮 Oyun geliştirme, uygulama tasarımı ve kullanıcı deneyimi alanlarında aktif çalışıyorum  

## 🧩 Teknolojiler & Araçlar

### 💻 Programlama Dilleri
![C#](https://img.shields.io/badge/C%23-239120?style=for-the-badge&logo=c-sharp&logoColor=white)
![C++](https://img.shields.io/badge/C%2B%2B-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

### 🎮 Oyun Motorları
![Unity](https://img.shields.io/badge/Unity-000000?style=for-the-badge&logo=unity&logoColor=white)
![Unreal Engine](https://img.shields.io/badge/Unreal_Engine-0E1128?style=for-the-badge&logo=unreal-engine&logoColor=white)

### 🎨 Tasarım Araçları
Projelerinde kullandığım tasarım araçları:

- **Figma** – UI/UX prototip ve arayüz tasarımı  
- **Photoshop** – 2D grafik, texture ve konsept tasarım  
- **Blender** – 3D modelleme ve sahne tasarımı  
- **Aseprite** – Pixel art ve sprite çalışmaları  

![Figma](https://img.shields.io/badge/Figma-F24E1E?style=for-the-badge&logo=figma&logoColor=white)
![Photoshop](https://img.shields.io/badge/Photoshop-31A8FF?style=for-the-badge&logo=adobe-photoshop&logoColor=white)
![Blender](https://img.shields.io/badge/Blender-F5792A?style=for-the-badge&logo=blender&logoColor=white)
![Aseprite](https://img.shields.io/badge/Aseprite-FA5C5C?style=for-the-badge&logo=aseprite&logoColor=white)
---


## 📫 İletişim Tıklarsanız Direk Yönlendirir 

- [![Email](https://img.shields.io/badge/Email-000000?style=for-the-badge&logo=gmail&logoColor=white)](mailto:ernysf341@gmail.com)
- [![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/eren-karag%C3%B6z-20a038293/)
- [![itch.io](https://img.shields.io/badge/itch.io-FA5C5C?style=for-the-badge&logo=itch.io&logoColor=white)](https://erenka.itch.io/)


name: generate animation

on:
  # run automatically every 24 hours
  schedule:
    - cron: "0 */24 * * *" 
  
  # allows to manually run the job at any time
  workflow_dispatch:
  
  # run on every push on the master branch
  push:
    branches:
    - master
    
  

jobs:
  generate:
    permissions: 
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 5
    
    steps:
      # generates a snake game from a github user (<github_user_name>) contributions graph, output a svg animation at <svg_out_path>
      - name: generate github-contribution-grid-snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
          
          
      # push the content of <build_dir> to a branch
      # the content will be available at https://raw.githubusercontent.com/<github_user>/<repository>/<target_branch>/<file> , or as github page
      - name: push github-contribution-grid-snake.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

