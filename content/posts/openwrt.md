---
date: '2025-03-13T14:00:00Z'
draft: false
title: '[Tutorial] Router OpenWRT com serviço 10 Gbit/s'
---
Três meses depois de ter publicado uma forma de obter as credênciais de acesso PPPoE neste BLOG, vou apresentar agora uma forma de as podermos utilizar num router próprio a correr um firmware chamado OpenWRT.

![ztef8748](https://i.imgur.com/2lIcDSI.jpeg)

# SFP+, XGS-PON, PPPoE, 🤔?

Vamos por partes:
- **SFP+**: O Small Form-factor Pluggable (SFP) é um módulo compacto e hot-swappable usado em redes de telecomunicações e transmissão de dados. Essencialmente, uma porta SFP num equipamento de rede funciona como um slot modular onde se pode encaixar um transceiver específico, seja para fibra ótica ou cabo de cobre. No caso do SFP+, é simplesmente pelo facto de suportar velocidades até 10 Gbit/s.
- **XGS-PON**: O XGS-PON é uma tecnologia de rede ótica passiva (PON) que permite ligações de internet de alta velocidade, chegando até 10 Gbit/s tanto para download como para upload. Utiliza fibra ótica para distribuir a ligação a vários utilizadores sem necessidade de equipamentos ativos entre o fornecedor e o cliente. Comparado com o GPON tradicional, oferece maior largura de banda e melhor desempenho.
- **PPPoE**: O PPPoE (Point-to-Point Protocol over Ethernet) é um protocolo usado para estabelecer ligações de internet, combinando as funcionalidades do PPP com o Ethernet. Tipicamente exige autenticação (username e password) para autenticação no ISP.

Estes são alguns dos jargões com que nos deparamos neste mundo das redes, entendendo o papel de cada um, faz com que nos seja mais fácil entender os passos seguintes.

---

## Que transceiver SFP+ XGS-PON aconselhas?

Por uma questão de gosto pessoal, tendo sempre a comprar algo que me permita "brincar" ou que seja possível alterar determinadas funcionalidades, firmwares personalizados, etc... Após alguma pesquisa, descobri o **WAS-110**:
![ztef8748](https://i.imgur.com/eLCh5rK.png)

---

## Como Obter as Credenciais?

Através de algumas vulnerabilidades presentes no firmware original do router, foi possível:
1. Extrair as credenciais PPPoE.
2. Decifrar as mesmas.

Este processo, no entanto, é complexo de realizar manualmente, pois envolve a reconstrução de:
- **IVs (Initialization Vectors)**;
- Senhas de cifra AES;
- Entre outros parâmetros técnicos.

---
## Ferramenta Automática

De forma a simplificar este processo e torná-lo acessível a qualquer utilizador, criei uma ferramenta que automatiza todas estas etapas. Assim, qualquer pessoa consegue obter os dados de acesso de forma simples e rápida.

![Interface da Aplicação](https://i.imgur.com/lFVZoZe.png)

Aproveitei o período natalício para construir esta tool, é escrita em RUST e está disponivel para as principais plataformas, **Windows**, **MacOS** e **Linux**.

**⚠️ ATENÇÃO: Tendo em conta a total e compreensível desconfiança em executar uma ferramenta deste carácter proveniente de uma fonte não confiável, aconselho a sua utilização numa **VM (máquina virtual)** ou através de uma **sandbox**, desde que tenham conectividade com o router do qual pretendem obter as informações. ⚠️**

### Download

##### **🔴 PS: EU COMO AUTOR DA FERRAMENTA, NÃO SOU RESPONSÁVEL POR QUALQUER DANO QUE ADVENHA DA SUA MÁ UTILIZAÇÃO! 🔴**

- [Windows x64 (28.62 MB)](/grabber_win64.zip)   
  * ```SHA-256: 37e85cc41fa5cf0a9b3cd6599b4bfafe5bfb8143611983ce0162a75ea4eb0a59```   
  * [https://www.virustotal.com/gui/file/37e85...](https://www.virustotal.com/gui/file/37e85cc41fa5cf0a9b3cd6599b4bfafe5bfb8143611983ce0162a75ea4eb0a59)

- [Linux x64 (45.64 MB)](/grabber_linux.zip)   
  * ```SHA-256: d7390b2fecd8a2fd64076856a7bf67bbd3bcf7b91d15e3ab6c7067b6860582c4```
  * [https://www.virustotal.com/gui/file/d7390...](https://www.virustotal.com/gui/file/d7390b2fecd8a2fd64076856a7bf67bbd3bcf7b91d15e3ab6c7067b6860582c4)

- [MacOS ARM64 (39.07 MB)](/grabber_macos_arm.zip)   
  * ```SHA-256: 3317362a6342df962a74e1f6fc9cd73aec6209cf0d619ec76a9e5251ab953a00```
  * [https://www.virustotal.com/gui/file/33173...](https://www.virustotal.com/gui/file/3317362a6342df962a74e1f6fc9cd73aec6209cf0d619ec76a9e5251ab953a00)

---
Se tiverem alguma dúvida / dificuldade / feedback, queiram por favor enviar um [email](mailto:i@443.pt) 