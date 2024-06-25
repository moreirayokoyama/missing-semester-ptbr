---
layout: page
title: O Semestre que Faltava na sua Formação de Ciência da Computação
nositetitle: true
---

Disciplinas te ensinam tudo sobre tópicos avançados de Ciência da Computação,
de Sistemas Operacionais a Aprendizado de Máquina, mas existe um assunto crítico
que raramente é coberto, e em vez disto é deixado para os estudantes descobrirem
por conta própria: proficiência com suas ferramentas. Nós te ensinaremos como
dominar a linha-de-comando, usar um editor de texto poderoso, usar funcionalidades
bacanas de Sistemas de Controle de Versão, e muito mais!

Alunos gastam centenas de horas usando suas ferramentas ao longo de sua educação
(e milhares ao longo de sua carreira), então faz sentido tornar a experiência tão
fluida e suave quanto possível. Dominar estas ferramentas não apenas te capacita
a perder menos tempo descobrindo como melhor usá-las para seu benefício, mas também
te permite resolver problemas que antes pareceriam impossivelmente complexos.

Leia sobre a [motivação por trás deste curso](/about/).

# Conteúdo

<ul>
{% assign lectures = site['2020'] | sort: 'date' %}
{% for lecture in lectures %}
    {% if lecture.phony != true %}
        <li>
            <a href="{{ lecture.url }}">{{ lecture.title }}</a>
        </li>
    {% endif %}
{% endfor %}
</ul>

As gravações das aulas estão disponíveis [no Youtube](https://www.youtube.com/playlist?list=PLyzOVJj3bHQuloKGG59rS43e29ro7I57J).

# Sobre o Curso

**Criadores**: Este curso foi co-criado por [Anish Athalye](https://www.anishathalye.com/), [Jon Gjengset](https://thesquareplanet.com/), and [Jose Javier Gonzalez Ortiz](http://josejg.com/).<br>

# Além do MIT

Nós também compartilhamos este curso para além do MIT na esperança de que outros possam
se beneficiar destes recursos. Você pode encontrar posts e discussão (provavelmente em inglês)
nos lugares a seguir:

 - [Hacker News](https://news.ycombinator.com/item?id=22226380)
 - [Lobsters](https://lobste.rs/s/ti1k98/missing_semester_your_cs_education_mit)
 - [/r/learnprogramming](https://www.reddit.com/r/learnprogramming/comments/eyagda/the_missing_semester_of_your_cs_education_mit/)
 - [/r/programming](https://www.reddit.com/r/programming/comments/eyagcd/the_missing_semester_of_your_cs_education_mit/)
 - [Twitter](https://twitter.com/jonhoo/status/1224383452591509507)
 - [YouTube](https://www.youtube.com/playlist?list=PLyzOVJj3bHQuloKGG59rS43e29ro7I57J)

# Página original do Curso (em inglês)

- [https://missing.csail.mit.edu/](https://missing.csail.mit.edu/)

## Reconhecimentos

Nós agradecemos Elaine Mello, Jim Cain, e o [MIT Open
Learning](https://openlearning.mit.edu/) por tornar possível a gravação das aulas; Anthony Zolnik e o [MIT
AeroAstro](https://aeroastro.mit.edu/) pelo equipamento audiovisual; e Brandi Adams e o
[MIT EECS](https://www.eecs.mit.edu/) por dar suporte ao curso.

---

<div class="small center">
<p><a href="https://github.com/missing-semester/missing-semester">Código Fonte</a>.</p>
<p>Sob a licença CC BY-NC-SA.</p>
<p>Veja <a href="/license/">aqui</a> para orientações de contribuição e tradução.</p>
</div>
