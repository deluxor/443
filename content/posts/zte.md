---
date: '2025-01-07T11:20:44Z'
draft: true
title: 'Credenciais PPPoE ZTE F8748'
---
**Antes de mais, quero desejar um bom ano de 2025 a todos!**  

Com a mais recente oferta de internet 10Gbps da DIGI, estão a instalar um CPE da marca Chinesa ZTE, cujo modelo é o F8748,
igual ao da imagem abaixo:

![ztef8748](https://i.imgur.com/IAhi5b7.png)

# Credenciais PPPoE

As credenciais PPPoE são utilizadas para realizar a autenticação **PAP/CHAP** e subscrever o **Access Concentrator** do lado do ISP e por conseguinte obter ligação à internet. Como o router em questão não disponibiliza (à data deste post) funcionalidades de **bridge**, esta é a única forma de fazer bypass ao router e utilizar um dispositivo próprio.

---

## Server Override

Este equipamento é um **AIO (All-in-One)**, ou seja, funciona como **ONT** e como router. Em setups anteriores, em que o **ONT** está separado, é possível obter as credenciais PPPoE através de um método de **server override**. 

Neste método:
- O router "pensa" que está a enviar os dados para um servidor legítimo, mas, na realidade, está a enviá-los para uma máquina intermédia que os interceta.

Contudo, como neste caso o equipamento é um bloco único (ONT + Router), não conseguimos aplicar esta estratégia.

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

#### Download

**🔴 PS: EU COMO AUTOR DA FERRAMENTA, NÃO SOU RESPONSÁVEL POR QUALQUER DANO QUE ADVENHA DA SUA MÁ UTILIZAÇÃO! 🔴**

- [Windows x64 (28.62 MB)](/grabber_win64.zip)   
  * ```SHA-256: 37e85cc41fa5cf0a9b3cd6599b4bfafe5bfb8143611983ce0162a75ea4eb0a59```   
  * [https://www.virustotal.com/gui/file/37e85...](https://www.virustotal.com/gui/file/37e85cc41fa5cf0a9b3cd6599b4bfafe5bfb8143611983ce0162a75ea4eb0a59)

- [Linux x64 (45.64 MB)](/grabber_linu.zip)   
  * ```SHA-256: d7390b2fecd8a2fd64076856a7bf67bbd3bcf7b91d15e3ab6c7067b6860582c4```
  * [https://www.virustotal.com/gui/file/d7390...](https://www.virustotal.com/gui/file/d7390b2fecd8a2fd64076856a7bf67bbd3bcf7b91d15e3ab6c7067b6860582c4)

- [MacOS ARM64 (39.07 MB)](/grabber_macos_arm.zip)   
  * ```SHA-256: 3317362a6342df962a74e1f6fc9cd73aec6209cf0d619ec76a9e5251ab953a00```
  * [https://www.virustotal.com/gui/file/33173...](https://www.virustotal.com/gui/file/3317362a6342df962a74e1f6fc9cd73aec6209cf0d619ec76a9e5251ab953a00)

---
Se tiverem alguma dúvida / dificuldade / feedback, queiram por favor enviar um [email](mailto:i@443.pt) 