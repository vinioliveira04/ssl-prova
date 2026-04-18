# SSL e Certificados Digitais — Atividade Prática

**Disciplina:** Segurança de Sistemas Computacionais
**Professor:** Clerivaldo

## Dados

- **Nome:** Vinicius Oliveira
- **Ambiente:** WSL2 com Ubuntu 24.04 LTS no Windows
- **IP:** 172.27.63.204 (eth0)

## Estrutura

- [exercicio1/](./exercicio1) — Instalação do OpenSSL
- [exercicio2/](./exercicio2) — Estrutura de diretórios
- [exercicio3/](./exercicio3) — Geração da chave privada RSA 2048
- [exercicio4/](./exercicio4) — Geração do CSR
- [exercicio5/](./exercicio5) — Emissão do certificado autoassinado
- [exercicio6/](./exercicio6) — Transferência segura com SCP
- [exercicio7/](./exercicio7) — Servidor HTTPS e análise do erro
- [exercicio8/](./exercicio8) — Validação do certificado

## Dificuldades

- Entender que `python3 -m http.server` não implementa TLS mesmo rodando na porta 8443. A porta 8443 é só uma convenção para HTTPS; o servidor precisa efetivamente negociar TLS, o que o módulo padrão do Python não faz sozinho. Nos logs foi possível observar os bytes do handshake TLS (`\x16\x03\x01...`) chegando no servidor HTTP e sendo interpretados como "Bad request".
- Como estava em ambiente WSL com uma única máquina, o exercício 6 (SCP) foi adaptado usando `localhost` como destino após iniciar o serviço SSH local, simulando uma transferência entre máquinas.
- Permissões de `/etc/ssl/certificates` exigiram uso de `sudo` na maioria dos comandos, já que os arquivos são de propriedade do `root`.

## Conclusão

A atividade permitiu percorrer na prática toda a cadeia de geração de um certificado digital: desde a criação do par de chaves assimétricas, passando pela requisição formal de assinatura (CSR), emissão do certificado X.509, transferência segura por canal SSH e validação pelo cliente. Ficou evidente por que certificados autoassinados não são aceitos por navegadores (ausência de cadeia de confiança até uma CA raiz) e a diferença fundamental entre simplesmente abrir uma porta 8443 e efetivamente oferecer TLS.
