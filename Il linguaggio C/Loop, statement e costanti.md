[[Storia e base di C]]
# Loop
For e while sono identici a quelli presenti in Java. Nient'altro da dire.
# Statement
Anche If-else e switch sono identici a quelli di Java. Di seguito è riportata la sintassi dello switch per rinfrescare un minimo la memoria. 
```c 
	int a=1;
	switch (a) {
		case 1: //dosomething break;
		case 2: //dosomething break;
		default:
		//dosomething
		break;
	}
```

# Costanti
Per definire una costante si usa \#define nel modo seguente: 
``` c
	#define N 10
```
Le costanti non vengono "definite", ma in realtà si chiede al prepocessor di sostituire tutte le occorrenze con il valore definito.