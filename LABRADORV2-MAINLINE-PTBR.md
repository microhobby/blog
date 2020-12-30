Agora o Labrador V2 da Caninos Loucos, o Single Board Computer Brasileiro, está oficialmente no Kernel Linux 🥳💃 🎉! Nesse post eu apresento as minhas contribuições para incluir o Labrador no repositório git do Linus Torvalds.

Aqui o Caninos Loucos Labrador v2 dando boot rodando Kernel v5.10 e Ubuntu 20.10:

<p style="text-align: center;"><iframe width="350" height="197" src="https://www.youtube.com/embed/_hkDwQZO2iY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="allowfullscreen"><span data-mce-type="bookmark" style="display: inline-block; width: 0px; overflow: hidden; line-height: 0;" class="mce_SELRES_start">﻿</span></iframe></p>

## Caninos Loucos Labrador - Kernel Mainline

O Labrador não tinha suporte para Kernel `mainline`. O pessoal da Caninos mantém um Kernel `downstream` com o suporte ao seu hardware no Github: https://github.com/caninos-loucos/labrador-linux . Daí eu vi uma oportunidade de contribuir para adicionar esse suporte na árvore do Linus Torvalds.

Comecei o trabalho em Fevereiro, foram desde então 7 versões para revisão no `Linux Kernel Mainling List`, com discussões com os mantenedores para melhorias e definições, para enfim agora em Dezembro este suporte entrar no Kernel Linux v5.10:

![Labrador V2 Matheus Castello Kernel Linux Contributions](https://github.com/microhobby/blog/blob/master/img/labrador-contribs.png?raw=true)

>⚠️ Importante lembrar que essas contribuições foram feitas sem nenhum vínculo com a Caninos Loucos ou LSI-Tec. Foram feitas durante meu tempo livre.

### Como Nascem as Placas para o Kernel Linux? 

>😂 Vem a cegonha das placas e taca uma plaquinha bebê na casa do homem Torvalds!

Isso foi algo totalmente novo para mim. É um processo um pouco burocrático, mas vou  defender os processos. Sem essa "burocracia" seria impossível manter tantos sub sistemas, arquiteturas, milhões de linhas de código e garantir a qualidade do Kernel Linux. Tem espaço para melhorias e automações? Tem! Mas não é o escopo desse post.

Como nascem as placas para o Kernel Linux? Primeiramente temos que adicionar o fabricante da placa em uma lista de `vendor prefixes`. Esse foi o [primeiro patch](https://lore.kernel.org/patchwork/patch/1309977/) da série:

>⚠️ Eu não estou adicionando aqui no post o diff completo, apenas alguns trechos para ilustrar. Clique nos links para ver o diff e o patch na integra!

```diff
diff --git Documentation/devicetree/bindings/vendor-prefixes.yaml
   "^calxeda,.*":
     description: Calxeda
+  "^caninos,.*":
+    description: Caninos Loucos Program
``` 

Com podem ver adicionei o prefixo `caninos`. Esse vai ser o prefixo que vamos utilizar para fazer os bindings de hardware compatível com o programa da Caninos Loucos. Então agora podemos documentar o novo hardware que será adicionado. Esse foi o [segundo patch](https://lore.kernel.org/patchwork/patch/1309979/) da série:

```diff
diff --git Documentation/devicetree/bindings/arm/actions.yaml 
+      - items:
+          - enum:
+              - caninos,labrador-base-m # Labrador Base Board M v1
+          - const: caninos,labrador-v2  # Labrador Core v2
+          - const: actions,s500
       - items:
           - enum:
               - lemaker,guitar-bb-rev-b # LeMaker Guitar Base Board rev. B
```

Notem que como o Labrador v2 consiste em um computador em módulo e placa base eu tive que documentar ambos que ficaram respectivamente como: `caninos,labrador-v2` e `caninos,labrador-base-m`.

Pronto, nasceu a placa? Calma! Com o prefixo do fabricante definido e novo hardware documentado podemos então adicionar a descrição do que o Labrador tem suporte e será inicializado pelo Kernel. Adicionar o famoso `Device Tree Source`. Esse foi o [terceiro patch](https://lore.kernel.org/patchwork/patch/1309975/):

```diff
diff --git arch/arm/boot/dts/owl-s500-labrador-base-m.dts 
+/dts-v1/;
+
+#include "owl-s500-labrador-v2.dtsi"
+
+/ {
+	model = "Caninos Labrador Core v2 on Labrador Base-M v1";
+	compatible = "caninos,labrador-base-m",
+		     "caninos,labrador-v2", "actions,s500";
+
```
```diff
diff --git arch/arm/boot/dts/owl-s500-labrador-v2.dtsi 
+#include "owl-s500.dtsi"
+
+/ {
+	model = "Caninos Labrador Core V2.1";
+	compatible = "caninos,labrador-v2", "actions,s500";
+
+	memory@0 {
+		device_type = "memory";
+		reg = <0x0 0x80000000>;
```
Notem como eu uso o `vendor prefix` e os nomes documentados na propriedade `compatible`. No caso do `owl-s500-labrador-base-m.dts` o `compatible` é `caninos,labrador-base-m` pois estou descrevendo o hardware da placa base. No `owl-s500-labrador-v2.dtsi` o `compatible` é `caninos,labrador-v2` pois estou agora descrevendo apenas o hardware do computador em módulo. 

Notem também que há um terceiro nível de descrição do hardware que entra no `#include "owl-s500.dtsi"`. Para uma placa nascer ela precisa também da descrição do processador, SoC (System on Chip). E para isso seria necessário também adicionar o `vendor prefix` da fabricante e etc. No caso do Labrador v2 o SoC é Actions Semiconductors s500 descrito pelo `owl-s500.dtsi`. Ainda bem já existiam duas placas que usavam o s500 assim eu não precisei descrever as funcionalidades, propriedades e fabricante do SoC.

![owl-s500 device tree source hierarchy](https://github.com/microhobby/blog/blob/master/img/cyberpunl-devicetree.png?raw=true)

E com isso, NASCEU! Agora o Kernel Linux tem definido o `vendor prefix` do programa Caninos Loucos e vai saber o que fazer, quais drivers subir, quando der boot em um hardware descrito pelo `Device Tree Source` do Labrador v2 `owl-s500-labrador-base-m.dts` mantido em `mainline`.

## Estado Atual - Em Progresso

Por agora o que o device tree source do Caninos Loucos Labrador descreve é a porta serial UART 3 e um clock para a serial ser usada como console e SÓ!! Há ainda bastante trabalho pela frente, mas como você pode ter notado no vídeo do início do post já estamos dando boot pelo eMMC e micro SD Card. Mas isso é um spoiler, trabalho em progresso e deve entrar no Kernel v5.12. A comunidade ativa que trabalha com a plataforma da Actions Semiconductors no Kernel Linux é bem pequena mas tem tido bastante progresso. Eles também estão adicionando o suporte ao PMIC da Actions que é usado em conjunto com os SoCs, então esperamos que ainda em 2021 teremos uma versão de Kernel mainline pronta  pra uso com tudo que a placa oferece.

### Por que é Importante Manter Mainline?

Talvez você esteja se perguntando:

> 🤔Por que ter esse trabalho para adicionar no Kernel Mainline se o pessoal da Caninos já mantem um repositório no Github com uma versão que funciona bem no hardware do Labrador?

Vamos dizer, hipoteticamente, que uma nova vulnerabilidade foi descoberta no Kernel Linux. Para manter seu sistema seguro você tem que atualizar para a mais recente versão que corrige a dita vulnerabilidade. Quando uma vulnerabilidade é descoberta ocorre um esforço pelos desenvolvedores do Kernel para lançar assim que possível patches de correção. E sabe onde que esses patches são aplicados? Na árvore `mainline` do Kernel Linux. Para aplicar essas correções em um Kernel `downstream` você vai ter mais trabalho e tem que tomar o cuidado de estar usando uma versão `LTS - Long Term Support` e não adicionar modificações que fujam muito do padrão de desenvolvimento do Kernel Linux, mantendo sempre seu `downstream` atualizado para não acontecerem conflitos. Sem dizer nos bug fixes não "críticos" que a comunidade encontra e novas funcionalidades adicionadas, o desenvolvimento do Kernel Linux é muito dinâmico. É bem mais trabalhoso manter um `downstream` ao invés de aplicar um esforço burocrático inicial de manter `mainline`. Como eu defendo sempre, a burocracia e processos de aplicar código no Kernel Linux vão garantir desde o começo a qualidade do suporte do sistema para seu hardware.

>⚠️ Não estou dizendo que é errado manter `downstream`. Em alguns casos, a melhor forma de dar suporte rápido à uma plataforma é manter alguma forma de `downstream`. Mas é importante trabalhar em `downstream` como se você estivesse em `mainline`,  e se esforçar para que as modificações exclusivas do `downstream` sejam aplicadas em `mainline` o quanto antes. Isso vai facilitar muito a sua vida no futuro.

## Conclusão

A priori parece meio bobo ficar tão entusiasmado com um monte de letrinhas aparecendo em uma tela vindo de uma plaquinha eletrônica, mas eu fiquei muito orgulhoso de ver um projeto com trabalho Brasileiro sendo adicionada oficialmente ao maior software de código livre do mundo. E fiquei também muito feliz te ter tido a oportunidade de ter trabalhado nisso. É um suporte ainda inicial mas é um começo. Temos ainda bastante código pela frente mas não podemos desistir dos projetos nacionais e temos que incentivar, dar feedback, testar e contribuir sempre que possível.

### Reconhecimento

Ao pessoal da [RoboCore](https://www.robocore.net/) e LSI-Tec pelo programa de testes do Labrador. Foi pelo programa de testes que eu consegui por as minhas mãos em um Labrador pela primeira vez.
