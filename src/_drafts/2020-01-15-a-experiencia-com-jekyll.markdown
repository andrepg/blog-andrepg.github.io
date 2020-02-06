---
layout: post
title:  "Reconstruindo meu tema GitHub Pages - Parte 1"
date:   2020-01-15 19:27:47 -0300
---

# Porquê resolvi criar este site?

A primeira pergunta. O que me moveu e incentivou a troca do tema? Bom, eu precisava aprender alguma tecnologia nova. E já tinha um pequeno cartão de visita online no GitHub (este aqui).

Até então o layout era bem simples, em três colunas. Andei visitando outros sites, outros cartões de visita e blogs, e vi que estavam bem mais apresentáveis. Decidi que não estava gostando do meu tema atual. 

Vi uma oportunidade de aprender a nova tecnologia que precisava e resolver o problema de não gostar do meu layout. Resolvi, então, redesenhar meu cartão de visita e ativar o blog que sempre tive intenção de escrever.

Algumas das tecnologias envolvidas na construção são bem simples. E outras eu já tive oportunidade de conhecer profissionalmente em experiências passadas.

Vamos lá.

# Quais tecnologias estou utilizando?

Este site utiliza a combinação simples HMTL/CSS/jQuery e está hospedado no [GitHub Pages][website_github_pages]. Para construir utilizo o [Jekyll][website_jekyll] para HTML e um pouco de [SASS][website_sass] para gerar o CSS. O conteúdo do blog é escrito em [Markdown][website_markdown].

O Jekyll é uma ferramenta construída em Ruby para geração de sites estáticos. Os sites estáticos são aqueles que não mudam. O conteúdo não depende de alguma situação para mudar. São bem simples e geralmente fáceis de construir. A velha web.

O SASS é um programa que a gente chama de pré-processador de CSS. A gente escreve o CSS na linguagem que ele entende. Quando precisamos ver as alterações, o comando `sass update arquivo_origem.scss:arquivo_destino.css` gera o estilo compilado pronto para upload. 

O Markdown é uma linguagem de marcação. Eu escrevo utilizando uma formatação específica dele. Quando quero publicar o site, utilizo o Jekyll para gerar o HTML e fazer upload para o GitHub Pages.

# Já existia um tema antes

O site já possuía um tema antes deste. Coisa simples. Duas colunas e um menu principal no topo de tudo. Mas o layout me parecia muito anos 1990. E já passamos disso há muito tempo. 

Andei visitando outros vários sites que me agradaram e tinham muito mais recursos. Recursos que eu sabia que era capaz de reproduzir ou desenvolver semelhante. Cores mais bem combinadas, animações, transições. Eu já fiz tudo isso. 

Coisas que não precisam de uma super ferramenta ou de interfaces de usuário muito complexas. Coisas possíveis de se fazer com CSS e Javascript. 

# Resolvi que não estava bom

Decidi que deveria, então, reconstruir o tema do blog e do cartão de visita. Isso incluía novas configurações de site, novo portefólio, nova língua... Um completo redesenho, enfim. 

Mas era hora de fazê-lo. Desde que iniciei a versão 1.0 não me dei por satisfeito. E toda vez que faço um release inicial é uma catástrofe para mim. Sempre melhora na versão 2.0 com umas correções de layout.

A construção pensada ia adicionar mais links no perfil, um menu mais simplificado e uma listagem dos posts. No mobile a intenção é adicionar um botão de perfil, exibido em todas as páginas. E essa está sendo uma das minhas maiores dificuldades.

# A construção do tema

Resolvi começar a desenvolver pela barra lateral. Talvez tenha sido meu primeiro erro. Alguma coisa dá errado no alinhamento geral e não consigo sequer manter um layout responsivo até agora. Me vi forçado a resetar todo o CSS e redesenhar o blog por inteiro. 

Por enquanto meu layout mobile está funcionando. Me falta desenvolver o menu do botão Perfil. Aí entra o outro desafio.

![A primeira versão do blog e homepage](/assets/posts/jekyll-primeiras-impressoes/v2.0 mobile - sem cor.png)

## O botão de perfil e a expansão

Essa é a primeira vez que vou construir um botão assim. Pensando: eu preciso de uma seção com todos os  links do menu invisíveis para exibir quando vier o clique. Preciso, então, do botão e do menu na mesma sintonia. 

Sobre o código, o que encontrei, digamos que eu tenha uma estrutura:

```html
<div class="panel-collapsed" id="show-profile-button">
  <img src="/profile-button.jpg" />
  <p id="text-button">Mostrar perfil</p>
</div>

<div id="sidebar" style="display:none">
  <ul>
    <li>Item</li>
    <li>Item</li>
    <li>Item</li>
  </ul>
</div>
```

Aqui, a id `#show-profile-button` é meu botão contendo a frase **Mostrar Perfil**. A classe `.panel-collapsed` serve para determinar se o menu está visível ou não. O Javascript é quem vai cuidar dessa mudança pouco adiante. E, finalmente, a id `#sidebar` contém os menus que estarão visíveis quando alguém clicar. O código JS que vai fazer toda a mudança é o seguinte:

```javascript
$(document).ready(() => {
  $("#show-profile-button").click(() => {
    let button = $("#show-profile-button");

    if (button.hasClass('sidebar-collapsed')) {
      button.find('#text-button').text('Ocultar perfil');
      button.removeClass('sidebar-collapsed');

      // Execute o slideDown para mostrar o menu
      $('#sidebar').slideDown();
    } else {
      button.find('#text-button').text('Mostrar perfil');
      button.addClass('sidebar-collapsed');

      // Execute o slideUp para ocultar o menu
      $('#sidebar').slideUp();
    }
  });
});
```




[website_github_pages]:https://pages.github.com
[website_jekyll]:https://jekyllrb.com
[website_sass]:https://sass-lang.com
[website_markdown]:https://www.markdownguide.org
