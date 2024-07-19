---
layout: "../../layouts/BlogPost.astro"

title: "Como fiz meu site usando Astro"
description: "Por que resolvi utilizar um framework que eu não conhecia para criar meu site... E como ele ficou pronto em uma semana."
publishDate: "2024-07-17"
coverImg: "/BlogImage1.svg"
tags: ["Astro", "Frontend"]
---

No começo de Julho comecei o desenvolvimento de meu site pessoal (esse aqui!) para falar de meus projetos e para ter meu próprio blog onde poderia escrever sobre programação e outros assuntos que me interessam. Em quase três anos de desenvolvimento web tive contato com vários frameworks e tecnologias, mas o que estou mais familiarizado é o React, então criei um novo projeto com React, Remix, tailwincss e todas as minhas ferramentas favoritas e comecei a programar.

## Os problemas

Estava feliz desenvolvendo meu site, criei as páginas inicias e inseri alguns exemplos de projetos e artigos para testar os layouts e os componentes, mas enquanto dava os toques finais no visual da aplicação comecei a pensar como faria para publicar o site. Como estava utilizando o Remix me deparei com um problema: ele não suporta _static site generation (SSG)_ por padrão. Ou seja, para hospedar a aplicação seria preciso de um servidor para lidar com as requisições. Isso implica em um custo mais alto e mais complexidade para hospedar. Como meu site seria bem simples e não possui muitas partes que precisam atualizar frequentemente, toda essa complexidade começou a me incomodar.

Além de ser complexo e possívelmente caro de se hospedar a aplicação, outro problema que encontrei é que servir conteúdo estático com Remix é complicado. Por exemplo, os artigos desse blog são escritos em Markdown, que é basicamente um arquivo de texto. Para ler arquivos `.md` e gerar as páginas com Remix seria preciso buscar eles no sistema de arquivos ou em um banco de dados, depois utilizar alguma biblioteca para transformar os conteúdos dos artigos em HTML ou JSX, para que então o servidor consiga responder com a página pronta. Tudo isso adiciona cada vez mais complexidade para gerar um simples blog.

Buscando uma solução, lembrei de uma ferramenta que havia visto algumas vezes no YouTube e outras redes sociais: [Astro](https://astro.build). Logo na página inicial lemos:

> The web framework for content-driven websites

Como esse site é apenas um lugar para reunir conteúdos, Astro parecia ser o framework certo para esse tipo de aplicação.

## Migrando o site

O processo de migração do site foi muito simples. Como o Astro é muito similar com o HTML puro, a estrutura das páginas foi uma questão de copiar e colar o código JSX e mudar alguns detalhes (no react se usa `className` ao invés de `class`), mas no geral o processo foi muito agradável.

A maior diferença foi na hora de escrever o conteúdo, como esse post aqui. Ao invés de criar um objeto para cada post dentro do Javascript, no Astro é possível criar um arquivo Markdowon dentro da pasta de rotas, assim ele será acessível como uma rota normal, e o framework se responsabiliza de transformar o arquivo em HTML puro para que ele seja exibido corretamente no navegador. Muito mais simples e fácil de utilizar.

Além de conter o conteúdo dos posts dentro do arquivo Markdown, o Astro suporta a adição de um cabeçalho (chamado de _frontmatter_) para incluir dados adicionais, como o título, data de publicação e tags. O _frontmatter_ deste post é nesse formato:

```yaml
---
layout: "../../layouts/BlogPost.astro"

title: "Como fiz meu site usando Astro"
description: "Por que resolvi utilizar um framework que eu não conhecia para criar meu site... E como ele ficou pronto em uma semana."
publishDate: "2024-07-17"
coverImg: "/BlogImage1.svg"
tags: ["Astro", "Frontend"]
---
```

Notem que na primeira linha definimos um layout. Esse arquivo vai ser utilizado para gerar a página que você está vendo, nele é definido o cabeçalho, o formato da imagem de capa, e por fim o conteúdo do blog. Assim temos mais flexibilidade para estilizar a página do jeito que queremos, mas ainda tendo a conveniência de ter nosso conteúdo guardado como arquivos Markdown.

## Deploy

Para realizar o deploy do site, o processo não poderia ser mais simples. O Astro possui um comando que reune todos os componentes e rotas definidos e gera um arquivo HTML estático para cada página. Com os arquivos criados, podemos colocar eles em um serviço de armazenamento na nuvem, como o S3 da AWS, e após configurar o domínio da aplicação na AWS, temos um site no ar, com tempos de resposta muito rápidos e com um custo extremamente baixo.

## Conclusão

Nem sempre usar o framework mais legal e capaz é a melhor opção. O ecossistema Javascript está cada vez mais complexo de se trabalhar, com ferramentas novas surgindo todos os dias (veja [dayssincelastjavascriptframework](https://dayssincelastjavascriptframework.com)), mas no final das contas um site estático dá conta do recado na maioria das vezes.
