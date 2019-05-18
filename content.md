% Einführung und Definitionen 
% Caspar Nagy 
% 27. Mai 2019 

## Gliederung

* Motivation
* Beispiele für parametrisierte Probleme und ihre Komplexität
	* \textsc{Bar Fight Prevention}
		* Brute Force
		* Kernelization
		* Bounded Search Trees
	* \textsc{Vertex Coloring}
	* \textsc{Clique} 
		* mit $k$
		* mit $\Delta$

* Definitionen
* Komplexitätsbeweise für parametrisierte Probleme
	* Theoretische Grundlagen
	* \textsc{Clique} für reguläre Graphen $\in W[1]$ 

## Motivation – Wo wir bei TGI stehen geblieben sind

### Viele Interessante Probleme $\in NP$

  * Lösungen für \textsc{Bar Fight Prevention} (aka \textsc{Vertex Cover}) schon für $n=1000$ sehr unhandlich
  * Laufzeit kann drastisch reduziert werden, wenn wir den Lösungsraum einschränken 

### Frage: 

  * Welche Parameter vereinfachen unser Problem tatsächlich?
  * Welche Laufzeit kann man mit Parametrisierung erreichen?


## Beispiel \textsc{Bar Fight Prevention}

\input{barfightprevention.tex}

## Beispiel \textsc{Bar Fight Prevention}

\input{barfightprevention_colored.tex}

## Beispiel – \textsc{Bar Fight Prevention} – Brute Force

```python
min_size = INFINITY
for candidate in potenzmenge(g.V):
   if solution(candidate) and len(candidate) < min_size:
   	best, min_size = candidate, len(candidate)
return best
```
\vspace{5mm}

* `solution(candidate)` wird $2^n$ mal aufgerufen
* sei $n=1000$: $2^{1000} \approx 10^{301}$
	* terminiert nach Ende des Universums

### Ansatz: Parameter $k$ einführen, der Größe der Lösung beschränkt


## Beispiel – \textsc{Bar Fight Prevention} – Brute Force

```python
for candidate in k_teilmengen(g.V, k):
   if solution(candidate):
   	return candidate	
return None 
```
\vspace{5mm}

* `solution(candidate) wird $\binom{n}{k}$ mal aufgerufen
* sei $n=1000, k=10: \binom{1000}{10} \approx 2,63 * 10^{23}$
	* terminiert nach einigen Jahrzehnten auf einem state-of-the-art Supercomputer


### Noch immer unbefriedigend. Können wir den Suchraum weiter einschränken?

## Beispiel – \textsc{Bar Fight Prevention}  

\begin{center}
\includegraphics[width=7cm]{vertex_random_nocolor.pdf}
\end{center}

## Beispiel – \textsc{Bar Fight Prevention}  

\begin{center}
\includegraphics[width=7cm]{vertex_random.pdf}
\end{center}


## Beispiel – \textsc{Bar Fight Prevention}  

\begin{center}
\includegraphics[width=7cm]{vertex_random_green.pdf}
\end{center}

## Beispiel – \textsc{Bar Fight Prevention} – Kernelization  
\begin{center}
\includegraphics[width=7cm]{vertex_random_kernel_nocolor.pdf}
\end{center}


* Ist effizient berechnenbar 
* Kann viele Instanzen wesentlich verkleinern
	* hilft uns aber nicht im worst-case
	* nutzt noch nicht unseren Parameter $k$




## Beispiel – \textsc{Bar Fight Prevention} – Kernelization  

\begin{center}
\includegraphics[width=7cm]{vertex_random_kernel_nocolor.pdf}
\end{center}

sei $k = 4$

. . .

> * Es ist egal ob wir $419$ oder $533$ herauswerfen.
> * $2$ muss immer herausgeworfen werden. 

## Beispiel – \textsc{Bar Fight Prevention} – Kernelization  

\begin{center}
\includegraphics[width=7cm]{vertex_random_kernel_nocolor.pdf}
\end{center}

Allgemein:

* Knoten mit $degree(n) = 1$ können wir hereinlassen, solange dadurch nicht direkt ein Konflikt entsteht.
* Knoten mit $degree(n) > k$ werden immer heraus geworfen.

## Beispiel – \textsc{Bar Fight Prevention} – Kernelization  



\colA{4cm}


```python
accepted = list()
denied = list()
unknown = list()
for v in G.V:
	if degree(v) == 0:
		accepted += v
	elif degree(v) == 1:
		if confict(v): 
			rejected += v
			k -= 1
		else: accepted += v
	elif degree(v) > k:
		rejected += v
		k -= 1
	else:
		unknown += v
	if k < 0:
		fail()
if len(G.subplot(unknown + accepted).edges) > k*k:
	fail()

```

\colB{8cm}


> * Läuft in Polynomialzeit 
> * Was tun mit `unknown`?
>     * $\forall v \in unknown: degree(v) \leq k$ 
>     * $\Rightarrow$
>          * $\sum_{v\in unknown}^{} degree(v) \leq k^2$
>          * $\leq 2 \cdot k^2$ Konfliktparteien
>          * $\leq \binom{2k^2}{k}$ Checks
>          * $k=10, \binom{200}{10} \approx 2,24*10^{16}$ 
>     * da außerdem: $\forall v \in unknown: degree(v) > 1$ 
>          * im Worst Case (Kreis) 1 Mensch pro Konflikt
>          * also nur noch $\binom{k^2}{k}$ Checks
>          * $k=10, \binom{100}{10} \approx 1,73*10^{13}$ Checks 
>          * $\Rightarrow$ einige Stunden auf einem Laptop

	
\colEnd


## Beispiel – \textsc{Bar Fight Prevention} – Kernelization  

\begin{center}
\includegraphics[width=8cm]{random_kernel.pdf}
\end{center}

## Beispiel – \textsc{Bar Fight Prevention} – Kernelization  

### Fazit

* Kernelization verkleinert bestimmte Instanzen, teilweise drastisch 
* Kernelization mit Paramerter kann viele worst-case-Instanzen abfangen und
  dadurch die Laufzeit begrenzen
* Fortgeschrittene Techniken im nächsten Vortrag

## Beispiel – \textsc{Bar Fight Prevention} – Weitere Ansätze


\begin{center}
\includegraphics[width=6.5cm]{random_kernel_nocolor.pdf}
\end{center}

. . .

> * Jeder Konflikt muss gelöst werden.
> * Normalerweise $2^{|E|}$ Checks
> * Da aber jeder Konflikt gelöst werden muss und die Lösung nur $k$ Knoten enthalten darf:
>     * Abbruch nach $k$ Rekursionen
>     * Also nur $2^k$ Checks

## Beispiel - \textsc{Bar Fight Prevention} – Bounded Search Trees


```python
def bounded_search(G, k, solution=[]):
    if k == 0:
        return []
    v1, v2 = G.random_edge()
    for v in (v1, v2):
        g = G.copy()
        g.remove_node(v)
        if len(g.edges()) == 0:
            return solution + [v]
    g1 = G.copy()
    g2 = G.copy()
    g1.remove_node(v1)
    g2.remove_node(v2)
    return max(
        bounded_search(g1, k-1, solution + [v1]),
        bounded_search(g2, k-1, solution + [v2])
    )
```


## Beispiel - \textsc{Bar Fight Prevention} - Fazit

* exponentieller Worst-case ohne Parametrisierung
* Parametrisierung + Brute Force polynomiell mit Laufzeit  $\binom{n}{k} \in \mathcal{O}(n^k)$
	* jedoch nur praktikabel für kleine k 
* Parametrisierung + Brute Force + Kernelization in $\binom{k^2}{k} * n^{\mathcal{O}(1)}$
* Bounded Search Trees in $2^k * k * n^{\mathcal{O}(1)}$

## Beispiel  

# Definitionen

## Definitionen 1/2

### Parametrisiertes Problem

* $(X,k) \in \Sigma^{*} \times \mathbb{N}$, wobei $X$ die Instanz des Problems und $k$ die unäre Kodierung des Parameters ist. $*$ 

### FPT (*Fixed Parameter Tractable*)

* Menge der parametrisierten Probleme, für die ein Algorithmus $\mathcal{A}$ existiert, der Instanzen in Zeit $f(k) \cdot |(x,k)|^{c}$ entscheidet.

### XP (*slice-wise polynomial*) 

* Menge der parametrisierten Probleme, für die ein Algorithmus $\mathcal{A}$ existiert, der Instanzen in Zeit $f(k) \cdot |(x,k)|^{g(k)}$ entscheidet.

## Definitionen 2/2

### Aus TGI kennen wir die Mengen *P* und *NP*. Für parametrisierte Probleme gibt es analog *FPT/XP* und *W[1]*

* W[1] ist die Menge aller parametrisierten Probleme, die mindestens so komplex sind wie das Finden einer \textsc{Clique} der Größe k. 
* Analog zu NP wird die W[1]-Vollständigkeit über polynomielle Transformationen gezeigt.
* Das alles ist natürlich sinnlos, sollte $P=NP$ oder $\textsc{Clique} \in FPT$ sein.

# Fragen?

