---
ipub:
  sphinx:
    toggle_input: true
    toggle_input_all: true
    toggle_output: true
    toggle_output_all: true
jupytext:
  cell_metadata_filter: all
  notebook_metadata_filter: all,-language_info,-toc,-jupytext.text_representation.jupytext_version,-jupytext.text_representation.format_version
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
livereveal:
  auto_select: code
  auto_select_fragment: true
  autolaunch: false
  backimage: media/nologo.png
  height: 100%
  start_slideshow_at: selected
  theme: simple
  transition: fade
  width: 100%
notebookname: asyncio et Python-3.7
version: '3.0'
---

<div class="licence">
<span>Licence CC BY-NC-ND</span>
<span>Thierry Parmentelat &amp; Arnaud Legout</span>
<span><img src="media/both-logos-small-alpha.png" /></span>
</div>

+++

#  Avertissement relatif à `asyncio` et Python-3.7

+++

## Complément - niveau intermédiaire

+++

Puisque cette semaine est consacrée à **`asyncio`**, il faut savoir que cette brique technologique est **relativement récente**, et qu'elle est du coup, plus que d'autres aspects de Python, **sujette à des évolutions**.

+++

## Les vidéos utilisent Python-3.6

+++

Comme on l'a dit en préambule du cours, notre version de **référence** est **Python-3.6**. C'est la version utilisée  dans les vidéos. Par contre les notebooks sur FUN-MOOC utilisent à présent la version 3.7.

+++

## Un résumé des nouveautés

+++

Vous trouverez à la fin de la semaine, dans la séquence consacrée aux bonnes pratiques, un résumé des améliorations  apportées depuis la version 3.6.

+++

## L'essentiel est toujours d'actualité

+++

Cela étant dit, nos buts ici étaient principalement:

* de vous faire découvrir ce nouveau paradigme,
* de vous faire sentir dans quelles applications cela peut avoir un apport très précieux,
* de bien vous faire comprendre ce qui se passe à l'exécution,
* et de vous donner un aperçu de la façon dont tout cela est implémenté.

+++

## Les différences les plus visibles

+++

Les plus grosses différences concernent la prise en main. Comme nous allons bientôt le voir, le "*hello world*" de `asyncio` était en Python-3.6 un peu *awkward*, cela nécessitait pas mal de circonlocutions.

C'est-à-dire que pour faire fonctionner la coroutine :

```{code-cell}
# un exemple de coroutine 
import asyncio

async def hello_world():
    await asyncio.sleep(0.2)
    print("Hello World")
```

### En Python-3.6

+++

Pour exécuter cette coroutine dans un interpréteur Python-3.6, la syntaxe est un peu lourdingue :

```python
# pour exécuter uniquement cette coroutine en Python-3.6
loop = asyncio.get_event_loop()
loop.run_until_complete(hello_world())
```

+++

### En Python-3.7

En 3.7, on arrive au même résultat de manière beaucoup plus simple :

```python
# c'est beaucoup plus simple en 3.7
asyncio.run(hello_world())
```

+++

### Avec IPython 7

Notez qu'avec IPython (et donc aussi dans les notebooks) c'est encore plus simple; en effet IPython s'est débrouillé pour autoriser la syntaxe suivante :

```{code-cell}
# depuis ipython, ou dans un notebook, vous pouvez faire simplement

await hello_world()
```

***Mise en garde*** attention toutefois, je vous mets en garde contre le fait que ceci est une **commodité** pour nous faciliter la vie, mais elle est **spécifique à IPython** et ne va pas fonctionner tel quel dans un programme exécuté directement par l'interpréteur Python standard.

```{code-cell}
:cell_style: split

# un code cassé

!cat data/broken-await.py
```

```{code-cell}
:cell_style: split

# la preuve

!python data/broken-await.py
```

Nous avons choisi de ne pas utiliser ce trait dans les notebooks, car cela pourrait créer de la confusion, mais n'hésitez pas à l'utiliser de votre côté une fois que tout ceci est bien acquis.

+++

### À propos de Python-3.8

Avec Python 3.8 - pas encore disponible à l'heure où j'écris ceci en Avril 2020 - il y a peu de changements concernant `asyncio`, ils sont décrits ici :

<https://docs.python.org/3/whatsnew/3.8.html#asyncio> 

<span style="font-size: smaller">Notez toutefois l'apparition d'une REPL (read-eval-print-loop) qui supporte justement `await` au toplevel</span>

+++

## Conclusion

+++

Pour conclure cet avertissement, ne vous formalisez pas si vous voyez dans le cours des pratiques qui sont dépassées. Les différences par rapport aux pratiques actuelles - même si on elles très visibles dans ce cours introductif - sont en réalité mineures au niveau de ce qu'il est important de comprendre quand on aborde d'un oeil neuf ce nouveau paradigme de programmation.
