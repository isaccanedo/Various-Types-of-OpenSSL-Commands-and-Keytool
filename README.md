# Various-Types-of-OpenSSL-Commands-and-Keytool
:key: # Various Types of OpenSSL Commands and Keytool

### Comandos OpenSSL e lista de keytool SSL
OpenSSL é uma implementação de código aberto de protocolos SSL/TLS e é considerada uma das ferramentas SSL mais versáteis. É uma biblioteca escrita em linguagem de programação C que implementa as funções criptográficas básicas. OpenSSL tem versões diferentes para a maioria dos sistemas operacionais semelhantes ao Unix, que incluem Mac OC X, Linux e Microsoft Windows etc.

O SSL aberto é normalmente usado para gerar uma solicitação de assinatura de certificado (CSR) e uma chave privada para diferentes plataformas. No entanto, ele também possui várias funções diferentes, que podem ser listadas a seguir. É usado para:

- Ver detalhes sobre um CSR ou certificado
- Compare o hash MD5 de um certificado e uma chave privada para garantir que eles correspondam
- Verifique a instalação adequada do certificado em um site
- Converta o formato do certificado

A maioria das funções mencionadas abaixo também pode ser executada sem envolver o OpenSSL usando essas ferramentas SSL convenientes. Aqui, reunimos alguns dos comandos OpenSSL mais comuns.

### Comandos OpenSSL gerais
Estes são o conjunto de comandos que permitem aos usuários gerar CSRs, certificados, chaves privadas e muitas outras tarefas diversas. Aqui, listamos alguns desses comandos:

### (1) Gerar uma solicitação de assinatura de certificado (CSR) e uma nova chave privada

```
openssl req -out CSR.csr -new -newkey rsa:2048 -nodes -keyout privateKey.key
```

### (2) Gerar um certificado autoassinado

```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout privateKey.key -out certificate.crt
```

### (3) Criar CSR com base em uma chave privada existente

```
openssl req -out CSR.csr -key privateKey.key –new
```
