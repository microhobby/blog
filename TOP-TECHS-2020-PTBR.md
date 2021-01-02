Aqui está uma lista das minhas tecnologias favoritas de 2020:

> ⚠️ Lembrando que essa lista é baseada apenas e somente na minha humilde opinião 💩 e estão mais relacionadas à minha área de atuação (sistemas embarcados, Linux embarcado)! Foram tecnologias que eu tive a oportunidade de trabalhar e testar durante 2020.

Irei dividir os "prêmios" em classes e para cada uma irei apontar o vencedor, segundo minha opinião, e uma outra que eu achei que é uma "promessa", que vale a pena ficar de olho é um destaque dentro da dita classe. Então vamos lá para os vencedores do "MicroHobby top tech 2020"!

### Linguagem de Programação

![top languages 2020](https://github.com/microhobby/blog/blob/master/img/retro-lang.png?raw=true)

- Favorito: **C#**
- Promessa: **Python**

C# com .NET Core 3.1 ou .NET 5 para sistemas Linux Embarcado tem sido uma mão na roda, tanto para aplicações headless ou com GUI. Interoperabilidade da linguagem é fantástica, super fácil e transparente acessar bibliotecas nativas. A plataforma é bem robusta e otimizada para rodar em armv7 e armv8. Também temos C# rodando para microcontroladores com o `NanoFramework` e com o `Meadow OS`.

Python é a promessa, promessa só pra mim porque já é uma linguagem com um ecossistema bem sólido. Eu pessoalmente não gosto da linguagem (minha opinião pessoal!!!). Mas pelo ecossistema e comunidade a plataforma tem muitas facilidades, bibliotecas que facilitam e agilizam seu trabalho. Tenho trabalhado com python no meu emprego atual em um dos projetos e não tem essa de linguagem favorita, tem a linguagem que é a melhor ferramenta para resolver um certo problema e paga seus boleto 🤣. Então não escapatória, python é muito popular e a tendencia é só crescer. Mesmo não sendo a favorita é bom ficar de olho e manter skills.

### Linux Distro

![top linux distro 2020](https://github.com/microhobby/blog/blob/master/img/retro-distro.png?raw=true)

- Favorito: **Ubuntu**
- Promessa: **Alpine**

Eu costumo mudar bastante de opinião sobre distros Linux. Se eu fosse escolher a minha distro preferida no meio do ano eu escolheria sem nem pensar: DEBIAN! Mas agora no final do ano a minha escolha vai pro Ubuntu, pelo suporte. O suporte da comunidade da Canonical  ao meu ver tem sido melhor, principalmente para o Windows Subsystem for Linux. Na verdade eu não tenho visto nenhum interesse da comunidade Debian com o WSL, talvez estejam com o pé atrás ainda. Eu até me ofereci a ajudar com um suporte da Distro Debian para o WSL 2, mas meio que fui ignorado (novamente deixar claro que essa é minha opinião, talvez eu tenha interpretado de forma errada 🤷‍♂️). Bem, com isso dito, e eu tenho utilizado cada vez mais o WSL  no meu dia a dia, nada mais certo do que ficar no Ubuntu que tem um suporte INCRIVEL para a comunidade do WSL.

Alpine, meu querido Alpine! Escolha promessa porque não é aquela distro que eu usarei como desktop, e acho até que essa não é a premissa dele mesmo. Ele é popular no mundo de containers Docker por ser mínimo, ser baseado no BusyBox, usa o musl ao invés do glibc e etc. E por causa disso mesmo ele tem sido uma ótima escolha como distro pronta para Linux Embarcado. 

### Editor de Código

![top ide 2020](https://github.com/microhobby/blog/blob/master/img/retro-ide.png?raw=true)

- Favorito: **VS Code**
- Promessa: **Codespaces**

Não tem pro VS Code. "Ah mas ele não é IDE, ele é só uma editor de código" 🙄. O VS Code tem trilhões de extensões, você consegue montar sua própria IDE para seja lá o que você quiser fazer! Além disso a API para escrever extensões é a coisa mais fácil e linda que eu já vi. E eu falo com propriedade, desenvolvo extensões tanto para VS Code quanto VS 2019 e a API de extensões do VS 2019 é um filme de terror com o roteiro ruim. CONFIA

E o Codespaces é o VS Code que roda no browser, então sem mais. PRÓXIMO!

### Placa Microcontrolada

![top microcontrolled boards 2020](https://github.com/microhobby/blog/blob/master/img/retro-microcontrolled.png?raw=true)

- Favorito: **Wilderness Labs Meadow F7**
- Promessa: **SparkFun MicroMods**

A Wilderness Labs tem feito um trabalho muito interessante com o Meadow F7. Ele roda um port do Mono Framework que possibilita rodar .NET Standard em microcontroladores, assim eu consigo reutilizar bibliotecas escritas em C# que sigam esse padrão, usar os pacotes NuGet e etc. O Meadow Foundation tem uma API para acesso ao hardware muito boa e fácil no estilo `dotnet` e também já tem implementações para alguns dos dispositivos e módulos mais populares no mundo maker. Mas é bom mencionar que o `Meadow OS` ainda está em fase beta, o stack de rede para conexão WiFi ainda está em desenvolvimento, funciona, mas não é otimizado. Mas de qualquer forma rodar .NET em uma placa com apenas 32MB de RAM à 216MHz é ainda bem impressionante. Ele será uma boa opção para usar as habilidades de .NET e C# para projetos IoT.

A promessa fica por conta do SparkFun MicroMods. Em breve vai ter review dele aqui. A ideia de um MoM (Microcontroller on Module) é muito boa, não é novidade, mas usar um conector M.2 para isso é bem interessante. Outra coisa interessante é que o padrão dos pinos do SparkFun MicroMods é open, então a esperança é que esse padrão fique popular e torne-se um padrão de mercado. Daí teremos vários MoMs por ai pinos compatíveis com múltiplas placas bases.

### Placa Microprocessada

![top microprocessed boards](https://github.com/microhobby/blog/blob/master/img/retro-microprocessed.png?raw=true)

- Favorito: **Apalis iMX8QM**
- Promessa: **Raspberry Pi 4**

Eu não fiz essa lista ano passado, mas com certeza  a placa microprocessada de escolha também seria o Apalis iMX8QM. A placa é uma ignorância só, duas GPUs, processamento heterogêneo, 6 cores ARM sendo 2x A72 e 4x A53, 4 cores ARM  M4F e etc. RODA TUTO!

A promessa não é bem promessa de novo, como todo lançamento da Raspberry Pi Foundation já está bem popular. As placas Raspberry são a melhor escolha pra quem quer começar no mundo do Linux Embarcado, e a nova geração de placas tem um hardware bem potente.

### Framework UI

![top GUI framework 2020](https://github.com/microhobby/blog/blob/master/img/retro-gui.png?raw=true)

- Favorito: **UNO Platform**
- Promessa: **Total Cross**

Nesse ano eu também testei e trabalhei com vários frameworks para GUI, focados para Linux Embarcado. O UNO Platform em si não é uma novidade, mas o suporte para Linux foi anunciado esse ano. E desde que foi anunciado, mesmo como preview, tem um suporte muito bom. Ter a possibilidade de utilizar XAML e C# para trabalhar com GUI em Linux Embarcado é INCRÍVEL. Usar o framework é muito fácil, roda em X11 ou Wayland e não é necessário compilar nada adicional para arquitetura `armv7` ou `armv8`, já vem tudo certo nos pacotes NuGet. Sem falar no suporte da comunidade e documentação. Eu diria que o Uno Platform foi um dos principais achados do meu ano. In love 😍

A promessa fica por conta do Total Cross. Tive oportunidade de testar e trabalhar com o framework esse ano. Primeiro que o framework é desenvolvido por Brasileiros, daí já ganha pontos 😝. Tem sua própria virtual machine para um subset de Java, gera arquivos de deploy bem pequenos (ótimo para sistemas com pouco armazenamento) e também roda bem sem necessidade de GPU. Ainda tem algumas questões de interoperabilidade com bibliotecas nativas, mas esse feedback já foi recebido pelo time da Total Cross e eles estão trabalhando nisso (já tem algo em preview inclusive). Então é ficar de olho no Total Cross porque promete.

### Tecnologia

![top tech 2020](https://github.com/microhobby/blog/blob/master/img/retro-toptech.png?raw=true)

- Favorita: **WSL 2**
- Promessa: **Blazor**

E por fim, mas não menos importante, as tecnologias em uma classificação mais genérica que eu usei esse ano. A minha favorita disparada foi o Windows Subsystem for Linux 2. Ter um Linux rodando em conjunto como Windows é lindo. É uma VM por debaixo dos panos mas como foi estruturado deixa tudo muito transparente e a interoperabilidade é muito boa. Ver a Microsoft dando suporte, e um ótimo suporte, contribuindo com as comunidades de open source e usando isso no Windows não tem preço. As possibilidades e oportunidades são infinitas.

A promessa fica por conta do Blazor. No começo ele rodava um port  `WASM` (Web Assembly) do Mono Framework, e é bem legal ter o .NET rodando direto no seu browser com `WASM`. A experiência de desenvolvimento é realmente interessante, escrever C# como se fosse JavaScript, ainda mais para quem quer se aventurar no mundo da web e vem das tecnologias desktop da Microsoft. Mas para alguns problemas você ainda vai esbarra em código JavaScript de qualquer forma. Ele também tem a opção server side, a experiência é a mesmo do `WASM` só que o código roda no servidor e ele conversa via signalR com browser pra fazer as mudanças no browser. Cheguei a avaliar esse modo para Linux Embarcado e tive bons resultados. É uma tecnologia "hype" que a Microsoft está investindo bastante então tem que ficar de olho.

## Considerações Finais

É isso pessoal! Lembrando que:

> ⚠️ ESSA LISTA É BASEADA NA MINHA HUMILDE OPINIÃO 💩! Não são verdades absolutas e eu posso mudar de opinião sem prévio aviso! 🤣

2020 ficamos em casa e testamos/estudamos/trabalhamos bastante, foi bem louco 🤪

