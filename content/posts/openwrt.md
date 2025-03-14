---
date: '2025-03-13T14:00:00Z'
draft: false
title: '[Tutorial] Router OpenWRT com serviço 10 Gbit/s'
ShowToc: true
---
Três meses depois de ter publicado uma forma de obter as credênciais de acesso PPPoE neste [**post**](https://blog.443.pt/posts/zte/), vou apresentar agora uma forma de as podermos utilizar num router próprio a correr um firmware chamado OpenWRT.

![router](https://i.imgur.com/2lIcDSI.jpeg)

### SFP+, XGS-PON, PPPoE, 🤔?
> {{< collapse summary="**Ler**" >}}
Vamos por partes:
- **SFP+**: O Small Form-factor Pluggable (SFP) é um módulo compacto e hot-swappable usado em redes de telecomunicações e transmissão de dados. Essencialmente, uma porta SFP num equipamento de rede funciona como um slot modular onde se pode encaixar um transceiver específico, seja para fibra ótica ou cabo de cobre. No caso do SFP+, é simplesmente pelo facto de suportar velocidades até 10 Gbit/s.
- **XGS-PON**: O XGS-PON é uma tecnologia de rede ótica passiva (PON) que permite ligações de internet de alta velocidade, chegando até 10 Gbit/s tanto para download como para upload. Utiliza fibra ótica para distribuir a ligação a vários utilizadores sem necessidade de equipamentos ativos entre o fornecedor e o cliente. Comparado com o GPON tradicional, oferece maior largura de banda e melhor desempenho.
- **PPPoE**: O PPPoE (Point-to-Point Protocol over Ethernet) é um protocolo usado para estabelecer ligações de internet, combinando as funcionalidades do PPP com o Ethernet. Tipicamente exige autenticação (username e password) para autenticação no ISP.

Estes são alguns dos jargões com que nos deparamos neste mundo das redes, entendendo o papel de cada um, faz com que nos seja mais fácil entender os passos seguintes.
{{</ collapse >}}

### Que transceiver SFP+ XGS-PON aconselhas?
> {{< collapse summary="**Ler**" >}}
Por uma questão de gosto pessoal, tendo sempre a comprar algo que me permita "brincar" ou que seja possível alterar determinadas funcionalidades, firmwares personalizados, etc... Após alguma pesquisa, descobri o: [**WAS-110**](https://pon.wiki/xgs-pon/ont/bfw-solutions/was-110/)

![pon](https://i.imgur.com/eLCh5rK.png)
Este módulo custa aproximadamente 170€ no Aliexpress, mas posso confirmar de viva voz que tem qualidade, e sobretudo bom suporte ao firmware [**8311**](https://pon.wiki/guides/install-the-8311-community-firmware-on-the-was-110/) que também ele é baseado no  OpenWRT. Estão à venda dois flavors, uma versão "SSH" que é um raw firmware, e a versão já com 8311. Aconselho-vos a última, vem pronto a usar.

Assim que o introduzirem no router / switch podem aceder à webui através do seguinte endereço: **https://192.168.11.1** as credênciais podem ser consultadas [**aqui**](https://pon.wiki/xgs-pon/ont/bfw-solutions/was-110/#default-credentials).

![pon2](https://i.imgur.com/BcSA9CY.jpeg)
⚠️ Tipicamente este módulos aquecem muito, facilmente atingem os **80ºC**, é importante manterem algum fluxo de ar, o dissipador que traz não é muito eficaz, devem também ter cuidado quando lhe tocarem após algumas horas de funcionamento, está quente!

**Alguns screenshots do firmware 8311**
![pon3](https://i.imgur.com/6P20aGt.jpeg)
![pon4](https://i.imgur.com/INgWrat.jpeg)
{{</ collapse >}}

### Que router aconselhas?
> {{< collapse summary="**Ler**" >}}
Da mesma forma que introduzi o módulo SFP+ WAS-110, um router é sempre um equipamento no qual gostamos ter liberdade de fazer as nossas modificações, alterar definições, firmwares, etc...
Neste caso, eu já era "cliente" das boards da Sinovoip, desde o tempo do **Banana PI R3**, e quando anunciaram o lançamento do **Banana PI R4**, não tive muitas dúvidas de qual seria o meu futuro router 😉, e sim mais uma vez é um chinaware, no entanto não deixa de ser um excelente equipamento, com uma excelente comunidade a trabalhar continuamente em melhorias e novas funcionalidades.
A foto da capa deste post já o mostra, foi tirada no dia em que o recebi.

{{</ collapse >}}
---
Se tiverem alguma dúvida / dificuldade / feedback, queiram por favor enviar um [email](mailto:i@443.pt) 