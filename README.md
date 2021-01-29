# Linking

##### 鍵結的研究 for visual studio


在早期C的世界中，沒有修飾這件事，隨著時間演進被開發出的庫越來越多，理所當然會遇到符號衝突的問題，例如C要使用Fortran編出來的庫，因此決定C的global全部加上斜槓 (foo-> _foo_)，fortran的則前後加斜槓(foo -> _foo_)，只是暫時解決不同平台間的問題，多個部門協作時，若命名的規範不嚴格，用同個C compiler編出來的東西最後還是撞來撞去。C++考慮到這點，生出了namespace這個東西，大大解決這個問題。


### decorated name(name mangling)  
compiler在compile過程中為了各個vars,funcs,objects產生出的encoded string  
ex. string裡面記錄著這個func的使用的calling convention,參數,type等等的訊息  

這個東西屬於compile和linker的內部實作細節，它們只對compiler和linker有意義，正常的程序員，是不需要碰這些的  
- 不同的vs版本，decorate的方式也不同  

- 因此假設有一個vs2008生出來的dll，vs2019的專案想使用這dll，是很有可能接不起來的 - LNK2019,LNK2001,LNK1120 無法解析的外部符號


### Func overloading
func signature -> decorated name (p88)

##### 弱符號強符號

```
__attribute__((nocommon)) (p113)
__attribute__((weakref)) (p93)
```

### extern , static
-

#### extern "C"
-

### static link .lib
.lib 有兩種意義
- 編譯dll時，會輸出兩個檔- .lib &.dll，.lib只是用來給linker關於.dll相關的資訊
- 編譯lib時，則只輸出.lib，程式碼的實做全部都在裡面了，此時.lib是.obj檔們用ar壓出來的集合包(ar)，windows下可以用7z打開。

以linux下gcc為例，假設 myLib.lib內含有 A.o B.o C.o  
gcc -c mymain.c (-> mymain.o)  
gcc -o myexec mymain.o A.o B.o C.o  
等同於  
gcc -lmyLib -o myexec mymain.o  




雖然不知道這些知識，也能順利的compile和link出 exe
只是不知道不會怎樣
知道了會很不一樣
@@!!

## Reference:  
[decorated name (MSDN)](https://docs.microsoft.com/zh-tw/cpp/build/reference/decorated-names?view=msvc-160)  
[extern c++(MSDN)](https://docs.microsoft.com/zh-tw/cpp/cpp/extern-cpp?view=msvc-160)  
程序員的自我修養:鍵結,裝載與庫  
[COFF Symbol Table](http://www.delorie.com/djgpp/doc/coff/symtab.html)
