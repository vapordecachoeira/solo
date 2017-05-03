---
layout: default
---

> _Impermanent are all component things,_ <br>
> _They arise and cease, that is their nature:_ <br>
> _They come into being and pass away,_ <br>
> _Release from them is bliss supreme._ <br>
>     
> _Aniccaa vata sa"nkhaaraa — uppaada vaya dhammino_ <br>
> _Uppajjitvaa nirujjhanti — tesa.m vuupasamo sukho._ <br>
> <br> 
> \- _Mahaa-Parinibbaana Sutta_

<br>
A software, given the right environment, will execute forever - not only unaware of its own existence, but also locked by its loops and functions in its own, ordinary, context.
<br>
<br>
[Transcend.py](https://github.com/vapordecachoeira/transcend.git) gives your software the change to transcend its own existence, making it _age_ over time and eventually cease all its functionatily and die.


## How?

The _**@transcend**_ function decorator (Python) takes into account the given 'date of birth' of the function and, at each call, calculates the chances of the given function executing properly or not. When it's _young_ it pretty much never fails. With time, as it ages, it starts to get old and ill, failing more and more, till the point it simply never executes anymore.


~~~python
from datetime import datetime, timedelta, date
import random
import functools


class transcend(object):
    MAX_DAYS = (27393 / 7)

    def __init__(self, born):
        self.born = born

    def __call__(self, func):

        @functools.wraps(func)
        def decorated():
            now = datetime.now().date()
            delta = (now - self.born).days
            chance = random.uniform(0, 1)
            life = 1.0 - (float(delta) / float(self.MAX_DAYS))
            if life < 0:
                raise FunctionTranscended(func.__name__)
            # print chance, delta, life
            if chance < life:
                func()
            else:
                raise OneStepCloser(func.__name__)

        return decorated


class OneStepCloser(Exception):
    def __init__(self, fname, *args, **kwargs):
        message = 'Function %s is one step closer....' % (fname,)
        super(OneStepCloser, self).__init__(message, *args, **kwargs)


class FunctionTranscended(Exception):
    def __init__(self, fname, *args, **kwargs):
        message = 'Function %s have transcended this plane....' % (fname,)
        super(FunctionTranscended, self).__init__(message, *args, **kwargs)


# Usage / Example

if __name__ == '__main__':
    @transcend(date(2008, 10, 10))
    def func_hello_world():
        print ":(  I'm still around..."


    func_hello_world()

~~~

## Author

Filipe Moura ([GitHub](http://github.com/vapordecachoeira)/[Site](https://fmoura.com)).

![Filipe Moura](https://www.gravatar.com/avatar/5c0d451b945d559dbe1277032f928acb?s=200)

### License

[MIT License](http://chibicode.mit-license.org/)

<a href="https://github.com/vapordecachoeira/transcend" class="github-corner"><svg width="80" height="80" viewBox="0 0 250 250" style="fill:#151513; color:#fff; position: absolute; top: 0; border: 0; right: 0;"><path d="M0,0 L115,115 L130,115 L142,142 L250,250 L250,0 Z"></path><path d="M128.3,109.0 C113.8,99.7 119.0,89.6 119.0,89.6 C122.0,82.7 120.5,78.6 120.5,78.6 C119.2,72.0 123.4,76.3 123.4,76.3 C127.3,80.9 125.5,87.3 125.5,87.3 C122.9,97.6 130.6,101.9 134.4,103.2" fill="currentColor" style="transform-origin: 130px 106px;" class="octo-arm"></path><path d="M115.0,115.0 C114.9,115.1 118.7,116.5 119.8,115.4 L133.7,101.6 C136.9,99.2 139.9,98.4 142.2,98.6 C133.8,88.0 127.5,74.4 143.8,58.0 C148.5,53.4 154.0,51.2 159.7,51.0 C160.3,49.4 163.2,43.6 171.4,40.1 C171.4,40.1 176.1,42.5 178.8,56.2 C183.1,58.6 187.2,61.8 190.9,65.4 C194.5,69.0 197.7,73.2 200.1,77.6 C213.8,80.2 216.3,84.9 216.3,84.9 C212.7,93.1 206.9,96.0 205.4,96.6 C205.1,102.4 203.0,107.8 198.3,112.5 C181.9,128.9 168.3,122.5 157.7,114.1 C157.9,116.9 156.7,120.9 152.7,124.9 L141.0,136.5 C139.8,137.7 141.6,141.9 141.8,141.8 Z" fill="currentColor" class="octo-body"></path></svg></a><style>.github-corner:hover .octo-arm{animation:octocat-wave 560ms ease-in-out}@keyframes octocat-wave{0%,100%{transform:rotate(0)}20%,60%{transform:rotate(-25deg)}40%,80%{transform:rotate(10deg)}}@media (max-width:500px){.github-corner:hover .octo-arm{animation:none}.github-corner .octo-arm{animation:octocat-wave 560ms ease-in-out}}</style>

<iframe src="https://ghbtns.com/github-btn.html?user=vapordecachoeira&amp;repo=transcend&amp;type=watch&amp;count=true&amp;size=large"
  allowtransparency="true" frameborder="0" scrolling="0" width="170" height="30"></iframe><br/>

