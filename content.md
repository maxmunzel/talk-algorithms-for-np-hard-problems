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
	* terminiert nach einigen Jahren auf einem state-of-the-art Supercomputer

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
\includegraphics[width=7cm]{vertex_random_kernel.pdf}
\end{center}

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

