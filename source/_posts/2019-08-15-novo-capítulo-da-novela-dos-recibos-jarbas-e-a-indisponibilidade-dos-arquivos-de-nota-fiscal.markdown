---
layout: post
title: "Novo capítulo da novela dos Recibos: Jarbas e a indisponibilidade dos arquivos de Nota Fiscal"
description: "Quem acompanha as publicações do Serenata de Amor nos últimos tempos tem tido a oportunidade de acompanhar uma longa jornada em busca de acesso integral às prestações de contas da cota parlamentar, um mecanismo de reembolso concedido aos senadores e deputados federais para exercício da atividade parlamentar."
date: 2019-08-15 00:00:00
comments: true
keywords: "civic tech, dados, democracy"
category: post
image: ../images/serenata.jpg
tags:
- dados
- democracy
---

Oiii sociedade civil mais engajada do Brasil :-)

Me chamo Mário Sérgio, faço parte do time de inovação cívica da Open Knowledge Brasil e esse é o meu primeiro texto para a Operação Serenata de Amor. Espero que esse conteúdo traga informações relevantes para vocês. ❤

Quem acompanha as publicações do Serenata de Amor nos últimos tempos tem tido a oportunidade de acompanhar uma longa jornada em busca de acesso integral às prestações de contas da cota parlamentar, um mecanismo de reembolso concedido aos senadores e deputados federais para exercício da atividade parlamentar.

<h2>Reprise dos últimos capítulos</h2>
Em um dos textos do [Pedro](https://medium.com/@pedrovilanova), [Senado Federal em: passando recibo](https://medium.com/serenata/senado-federal-em-passando-recibo-fc9439122c9c), foi exposta uma análise a respeito de uma manifestação do presidente do Senado Federal, [Davi Alcolumbre](https://twitter.com/davialcolumbre), onde ele posicionou-se oficialmente pela liberação do sigilo arbitrário sobre despesas parlamentares. Ou seja, autorizando seus colegas a omitirem da população notas fiscais e recibos referentes a reembolsos efetuados com a Cota Parlamentar.

Outro capítulo importante foi apresentado pela [Tatiana Balachova](https://medium.com/@tatianasb), no texto [Rosie e o mistério do recibo digitalizado não disponível](https://medium.com/serenata/rosie-e-o-mist%C3%A9rio-do-recibo-digitalizado-n%C3%A3o-dispon%C3%ADvel-feaf874aabc6). Nesse caso, identificamos que alguns recibos digitalizados não estão disponíveis, o que dificulta a verificação de suspeitas irregularidades.

<h2>Jarbas e a indisponibilidade dos arquivos de Nota Fiscal</h2>
O [Jarbas](https://jarbas.serenata.ai/dashboard/chamber_of_deputies/reimbursement/) é um site onde é possível navegar pelos gastos da CEAP (Cota para o Exercício da Atividade Parlamentar) e descobrir mais sobre cada suspeita, de maneira simples e descomplicada. É também onde começa o trabalho de validação de suspeitas levantadas pela [Rosie](https://twitter.com/RosieDaSerenata).

[Nota Fiscal disponível no antigo padrão do portal da câmara](https://drive.google.com/viewerng/viewer?url=https://www.camara.leg.br/cota-parlamentar/documentos/publ/2340/2017/6368649.pdf)

Após uma alteração no sistema de acesso aos arquivos do [portal de acesso a informação](https://www.camara.leg.br/cota-parlamentar/) da câmara dos deputados, os arquivos que antes eram disponibilizados em extensão .pdf, conforme a imagem ao lado, agora não estão mais disponíveis no novo modelo de implementação do portal.

Nós defendemos que todas as instituições devem sim desenvolver melhorias em seus portais e plataformas, para assim se tornarem mais transparentes e consistentes. Entretanto, as mudanças devem ser feitas de uma forma que não danifiquem ou alterem o funcionamento de antigas implementações, que podem estar integradas a outras soluções implementadas pela sociedade civil ou instituições públicas e privadas.

Lembrando que de acordo com a Lei de Acesso à Informação (LAI), os dados devem estar acessíveis. E dado acessível é diferente de dado disponível, pois muitas vezes os dados estão disponibilizados de uma forma que não é possível ter acesso as informações integralmente.

<iframe src="https://giphy.com/embed/2uIo15nEts52m4uYHP" width="480" height="270" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/wetv-we-tv-growing-up-hip-hop-growinguphiphop-2uIo15nEts52m4uYHP">via GIPHY</a></p>

Segundo a equipe técnica da câmara, que nos respondeu muito prontamente, o portal tem duas inconsistências a serem corrigidas:

*1. O que aconteceu foi que as despesas em questão têm como comprovantes notas fiscais eletrônicas e, nesses casos, não há um arquivo PDF, mas sim um HTML, copiado por scrapping dos sites de controle estaduais.*
*2. O segundo problema é que uma parte da URL de acesso ao documento é gerada pelo sistema de Dados Abertos, e a equipe da Câmara dos deputados precisará trabalhar para ajustar essa implementação.*

O resultado é que quando tentamos acessar os arquivos de um recido disponível no Jarbas, o portal de acesso a informação nos apresenta o seguinte erro:

![(A imagem é meramente ilustrativa, mas o texto é esse alterando os número de recibo pra recibo)](https://mariosergio.me/images/not_found.webp)

Vocês terão acesso ao nosso questionamento feito por meio de uma [issue no Github para a equipe técnica da Câmara dos Deputados](https://github.com/CamaraDosDeputados/dados-abertos/issues/268?source=post_page-----bb6b5b43dd65--------------------------------).

Já falamos algumas vezes que existem opções para entrar em contato com o time de suporte da câmara dos deputados. Uma delas é o Fale Conosco no Portal da Câmara, ou até mesmo entrando diretamente em contato com o parlamentar através do e-mail ou telefone. Você pode achar os contatos de cada deputado [aqui](https://www.camara.leg.br/deputados/quem-sao).

<iframe src="https://giphy.com/embed/XbT8b0H8vDk52" width="480" height="270" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/XbT8b0H8vDk52">via GIPHY</a></p>

O método que utilizamos para abrir essa solicitação foi o [repositório do github de dados abertos da Câmara dos Deputados](https://github.com/CamaraDosDeputados/dados-abertos/). Inclusive a resposta foi feita rapidamente e de forma muito clara.

Dessa forma, acreditamos que esse novo capítulo enfrentado, que apresenta mais uma barreira de acesso aos recibos da cota parlamentar, não necessariamente foi um ato de retrocesso em transparência, mas sim um pequeno equívoco na gestão de mudanças nos sistemas, que com o nosso report serão ajustados em breve. São as vantages da abertura de diálogo com a comunidade.

<iframe src="https://giphy.com/embed/RHEqKwRZDwFKE" width="480" height="204" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/satisfying-screen-loading-RHEqKwRZDwFKE">via GIPHY</a></p>

Links importantes da Serenata e Open Knowledge Brasil:
- [SITE Serenata](https://serenata.ai/), [Facebook Serenata](https://www.facebook.com/operacaoSerenataDeAmor/)
- [SITE OKBR](https://ok.org.br/)
- [Jarbas](https://jarbas.serenata.ai/dashboard/chamber_of_deputies/reimbursement/) (nosso banco de dados com os reembolsos da CEAP)
- [GitHub](https://github.com/okfn-brasil) dos nossos projetos
- [DOE para a Serenata!](https://apoia.se/serenata)
