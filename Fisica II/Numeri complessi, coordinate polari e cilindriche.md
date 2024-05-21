---
tags: elettromagnetismo
created: 2023-11-17 19:34:29
updated: 2023-11-17 19:34:29
---
#elettromagnetismo 
[[Caratteristiche elettromagnetiche, densità di carica, forza e campo elettrico]]
# Rappresentazione numeri complessi
>[!regola]
Regola fondamentale per i numeri complessi è che $i=\sqrt{-1}$, perciò $i^2=-1$.

Un numero complesso generalmente è composto da una parte reale e da una parte immaginaria: $z=x+iy$ oppure $z=x+jy$, dove x è la parte reale, mentre y la parte immaginaria. 
Esiste poi il coniugato di un numero complesso che è pari a $z^*=x-jy$. In particolare se calcolo $z\cdot z^*$ trovo che $\large z\cdot z^*=(x+jy)(x-jy)=x^2+jxy-jxy-j^2y^2=x^2+y^2$ 
Il modulo è sempre un numero reale positivo in quanto se ne estrae la parte positiva ed è dato da: $\large|z|=\sqrt[+]{x^2+y^2}=\sqrt{z\cdot z^*}$. Esiste anche la forma polare dei numeri complessi: $z=|z|\cdot e^{j\theta}=|z|\cdot(cos\theta+jsen\theta)$

## Coordinate cilindriche o polari
Nel piano cartesiano si ha che $$\begin{gather}x=|z|cos\theta \\y=|z|sen\theta\\ \theta=arctan({y\over x})\end{gather}$$ per passare alle coordinate cilindriche si ha: $$\begin{align}
x=rcos\phi \\
y=rsen\phi \\
z
\end{align}$$
dunque si passa da $P(x,y,z)\equiv P(r,\phi,z)$ dove se fisso $r$ e vario $z$ e $\phi$ ottengo un cilindro. Il differenziale sarà $dV=rdrd\phi dz$

## Coordinate sferiche
Preso un punto identificato dal raggio $R$ che forma l'angolo $\theta$ con l'asse z, se proietto il punto sul piano $xy$ ottengo l'angolo $\phi$. Dunque passo da $P(x,y,z)\equiv P(R,\theta,\phi)$ in particolare $$\begin{align}
x=Rsen\theta cos\phi \\
y=Rsen\theta sen\phi \\
z=Rcos\theta 
\end{align}$$
Il differenziale sarà $dV=R^2sen\theta dRd\phi d\theta$ dove $R^2sen\theta d\phi$ è la variazione lungo $\phi$.

---
