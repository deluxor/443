---
date: '2025-03-14T10:00:00Z'
draft: false
title: '[Feedback] Router OpenWRT com serviço 10 Gbit/s'
ShowToc: true
---
Três meses depois de ter publicado uma forma de obter as credênciais de acesso PPPoE neste [**post**](https://blog.443.pt/posts/zte/), vou passar-vos o meu feedback de as utilizar num router próprio a correr um firmware chamado OpenWRT.

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

Este módulo custa aproximadamente [**165€ no Aliexpress**](https://s.click.aliexpress.com/e/_on14BzX) isto no caso de optarem pela versão 8311. Posso confirmar de viva voz que tem qualidade, e sobretudo bom suporte ao firmware [**8311**](https://pon.wiki/guides/install-the-8311-community-firmware-on-the-was-110/) que também ele é baseado no  OpenWRT. Estão à venda dois flavors, uma versão "SSH" que é um raw firmware, e a versão já com 8311. Aconselho-vos a última, vem pronto a usar.

Assim que o introduzirem no router / switch podem aceder à webui através do seguinte endereço: **https://192.168.11.1** as credênciais podem ser consultadas [**aqui**](https://pon.wiki/xgs-pon/ont/bfw-solutions/was-110/#default-credentials).

![pon2](https://i.imgur.com/BcSA9CY.jpeg)
⚠️ Tipicamente este módulos aquecem muito, facilmente atingem os **80ºC**, é importante manterem algum fluxo de ar, o dissipador que traz não é muito eficaz, devem também ter cuidado quando lhe tocarem após algumas horas de funcionamento, está quente!

**Alguns screenshots do firmware 8311**
![pon3](https://i.imgur.com/6P20aGt.jpeg)
![pon4](https://i.imgur.com/INgWrat.jpeg)

{{</ collapse >}}

### Que router aconselhas?
> {{< collapse summary="**Ler**" >}}
Da mesma forma que introduzi o módulo SFP+ WAS-110, um router é sempre um equipamento no qual gostamos ter a liberdade de fazer as nossas modificações, alterar definições, firmwares, etc...
Neste caso, eu já era "cliente" das boards da Sinovoip, desde o tempo do **Banana PI R3**, e quando anunciaram o lançamento do **Banana PI R4**, não tive muitas dúvidas de qual seria o meu futuro router 😉, e sim mais uma vez é um chinaware, no entanto não deixa de ser um excelente equipamento, com uma excelente comunidade a trabalhar continuamente em melhorias e novas funcionalidades.
A foto da capa deste post já o mostra, foi tirada no dia em que o recebi.

Conseguem este conjunto por volta dos [**165€ no Aliexpress**](https://s.click.aliexpress.com/e/_oCgTPev), ou seja, a brincadeira fica num total de **330€** aproximadamente (router + xgs-pon sfp+). Aconselho o bundle 6, pois já traz tudo o que é necessário para montarem o router, desde a alimentação, dissipador, thermal pads e a caixa em aluminio de muito boa qualidade.

![pon6](https://i.imgur.com/UF46Jdm.jpeg)

Uma questão que me colocam, é se efetivamente este router consegue tirar partido dos **10 Gbit/s**, passando a explicar: 

Num serviço **XGS-PON** têm de ter algumas considerações:
- **FEC** (Forward Error Correction) - Isto é o que permite adicionar redundância à informação transmitida de forma a conseguir recuperar eventuais erros.
- **GEM** Encapsulation - Todos os pacotes transmitidos pela fibra vêm encapsulados num pacote GEM, que só por si já adiciona algum overhead.
- **PPPoE** - É mais um encapsulamento adicional, e dependendo do MTU (maximum transmission unit) cria ainda mais overhead por cima do já mencionado.

Em termos práticos:

- **Sem PPPoE**: ~ 8.5–9 Gbit/s (depois do FEC e do PON)
- **Com PPPoE**: ~ 7.5–8.5 Gbit/s (dependendo do MTU e do tamanho do pacote)

O que quer dizer, que por melhor que seja o vosso equipamento, estarão sempre limitados pelo overhead, mas o BPI R4 consegue sem nenhum esforço bater nestes limites, alias, pelo facto de ter hardware offloading, o CPU nem mexe enquanto exaustam a ligação.
![pon5](https://i.imgur.com/Nn3gXIa.png)
Exemplo da WEBUI 
![pon7](https://i.imgur.com/UOJjaKA.png)


Isto combinado com 4GB de RAM, 8GB de armazenamento EMMC, dá-nos muito espaço para instalarmos plugins, adblockers, IDS/IPS, docker, download managers, VPN's wireguard, IPSEC, OpenVPN, e uma infinidade de opções.
{{</ collapse >}}

### Algumas dicas
> {{< collapse summary="**Ler**" >}}
Agora que já sabem que material comprar / usar, vou deixar aqui algumas dicas:
- Instalem a versão **SNAPSHOT** do OpenWRT!!
- Documentação de como instalar o OpenWRT no BPI R4: [**https://openwrt.org/inbox/toh/sinovoip/bananapi_bpi-r4**](https://openwrt.org/inbox/toh/sinovoip/bananapi_bpi-r4)
- Após instalarem o OpenWRT não terão nenhuma interface web disponível, têm de a instalar, mas antes disso precisam de ligação à internet para o poderem fazer, portanto de forma a ganhar ligação à internet, se já tiverem o módulo SFP inserido, acedam por SSH ao router `ssh root@192.168.1.1` by default não precisa de password, de seguida acrescentem esta configuração ao ficheiro (pode ser adicionada no fundo), por exemplo `vi /etc/config/network`:
```
config device
        option type '8021q'
        option ifname 'sfp-wan'
        option vid '20'
        option name 'sfp-wan.20'
        option mtu '1508'
        option macaddr '<MAC_ADDRESS_DO_ROUTER_ORIGINAL>'


config interface 'wan'
        option device 'sfp-wan.20'
        option proto 'pppoe'
        option username 'xxxxxxx@digi'
        option password 'xxxxxxxxx'
        option ipv6 'auto'
        option mtu '1508'
```
De seguida fazemos restart à rede `/etc/init.d/network restart` ao fim de alguns segundos, já deverão ter ligação, testem com um `ping 1.1.1.1`, caso esteja tudo OK, procedam com a instalação da WEBUI, `apk update && apk add luci`, após a execução deste comando já deverão conseguir aceder por http://192.168.1.1 e continuar com o setup.

- Para ativarem o hardware offloading façam: 
```
uci set firewall.@defaults[0].flow_offloading='1'
uci set firewall.@defaults[0].flow_offloading_hw='1'
uci commit
```
- Para manter o CPU com o clock baixo em on-demand e não aquecer tanto, acrescentem isto ao ficheiro `/etc/rc.local` antes do `exit 0`:
```
echo ondemand > /sys/devices/system/cpu/cpufreq/policy0/scaling_governor
```
- Instalar pacotes é fácil, para pesquisar por nome façam `apk search XPTO` para instalarem `apk add XPTO`
- Para adblocker aconselho utilizarem o adblock-fast, podem instalar `apk add adblock-fast luci-app-adblock-fast` e se tiverem curiosidade podem consultar a documentação [**aqui**](https://docs.openwrt.melmac.net/adblock-fast/)
{{</ collapse >}}
---
Se tiverem alguma dúvida / dificuldade / feedback, queiram por favor enviar um [email](mailto:i@443.pt) 