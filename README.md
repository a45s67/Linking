# Linking

鍵結的研究



decorated name(name mangling)
compiler在compile過程中為了各個vars,funcs,objects產生出的encoded string
ex. string裡面記錄著這個func的使用的calling convention,參數,type等等的訊息

這個東西屬於在compile和linker的內部實作細節，正常的程序員，是不需要碰這些的
-> 不同的vs版本，decorate的方式也不同
-> ex. 
  - vs2008 : extern "C" hello(); -> hello
  - vs2019 : extern "C" hello(); -> _hello_ ;加了斜槓
因此假設有一個vs2008生出來的dll，vs2019的專案想使用這dll，是很有可能接不起來的 - LNK2019,LNK2001,LNK1120 無法解析的外部符號



extern , static




雖然不知道這些知識，也能順利的compile和link出 exe
只是不知道不會怎樣
知道了會很不一樣
@@!!

reference:
[decorated name (MSDN)](https://docs.microsoft.com/zh-tw/cpp/build/reference/decorated-names?view=msvc-160)
程序員的自我修養:鍵結,裝載與庫
