# Tanim

- Her bir proje icin ayri bir virtual environment yaratmak best practice'dir.
 - Her bir virtual ortami ilgili proje icin kucuk kutucuklar olarak dusun.
    - **Avantajlari**: 
        - Projelerin ihtiyac duydugu kutuphaneler birbiriyle karismaz.
        - Iki farkli proje bir kutuphanenin farkli versiyonlarina ihtiyac duyarsa virtual env kullanilmadigi durumda python hangi versiyonu yukleyecegini bilemez.

   
### Virtual Environment Nasil Yaratilir

``` bash


# dilek isimli bir virtual environment yarat
# ve bu environment'a python 3.8 ile calissin.
conda create --name dilek python=3.8


# dilek isimli bir virtual environment yarat
# ve bu environment'a numpy kutuphanesini kur. 
# numpy kismi sart degil. sonradan da kurulabilir 
conda create --name dilek numpy

```

### Var olan virtual environmentlar nasil listelenir

``` bash
conda env list
```

### Ismi dilek olan bir environment nasil active edilir?

``` bash
# Activate etmek icin
conda activate dilek
# Deactivate etmek icin
conda deactivate # Hangi venv icindeyse onu deactivate eder.
```

