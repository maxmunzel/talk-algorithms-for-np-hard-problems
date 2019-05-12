% Einführung und Definitionen 
% Caspar Nagy 
% 13. Mai 2019 

## Gliederung

* Motivation
* Definitionen


## Motivation – Wo wir bei TGI stehen geblieben sind

### Viele Interessante Probleme $\in NP$

  * Lösungen für \textsc{Bar Fight Prevention} (aka \textsc{Vertex Cover}) schon für $n=1000$ sehr unhandlich
  * Laufzeit kann drastisch reduziert werden, wenn wir den Lösungsraum einschränken 

### Frage: 

  * Welche Parameter vereinfachen unser Problem tatsächlich?
  * Welche Laufzeit kann man mit Parametrisierung erreichen?

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
