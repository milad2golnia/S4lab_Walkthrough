First off, we create a file called helloWorld.c:

```
#include <stdio.h>
int main(){
    printf("Hello world.\n");
    return 0;
}
```
We compile the code:
```
gcc helloWorld.c
```

Now we use `radare2` to dump its binary:
```
r2 -q -c 'pi $s' ./a.out > out.txt
```