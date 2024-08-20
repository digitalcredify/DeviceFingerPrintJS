# Device Fingerprint para JavaScript

## Introdução

Este repositório contém um exemplo de implementação para capturar a impressão digital do dispositivo (Device Fingerprint) utilizando JavaScript. O código faz uso da biblioteca FingerprintJS e envia os dados coletados para a plataforma da Credify.

## Requisitos

1. **Access Key**: Para usar este serviço, você precisará de uma access key fornecida pela equipe da Credify. Entre em contato com a equipe da Credify para obter sua access key.

## Instruções

### Passo 1: Obtenha sua Access Key

Entre em contato com a equipe da Credify para solicitar sua access key. Esta key é necessária para autenticar suas requisições ao serviço da Credify.

### Passo 2: Adicione o Código à Sua Aplicação

Adicione o código abaixo à sua aplicação para capturar a impressão digital do dispositivo e enviar os dados para a plataforma da Credify.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Device Finger Print para JavaScript</title>
  </head>
  <body></body>
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  <script>
    const getFingerprint = async () => {
      try {
        // Carregar o agente
        const FingerprintJS = await import(
          "https://openfpcdn.io/fingerprintjs/v4"
        );
        const fp = await FingerprintJS.load();

        // Obter o identificador do visitante
        const result = await fp.get();

        // Este é o identificador do visitante:
        const visitorId = result.visitorId;
        const accesskey = "your-access-key"; // Peça seu accesskey para equipe Credify
        const action = "action-to-call-api"; // Descrição do momento da chamada: "login", "cadastro", "consulta", etc.
        const bodyParams = {
          visitorId,
          accesskey,
          action,
          document: "document-to-identify-the-client",
          tipoDocument: "type-of-document", // Opções: "CPF", "CNPJ", "CNH", "RG" ou "OUTROS"
        };

        // Enviar os dados para a Credify
        axios
          .post(`https://back.credify.com.br/device-finger-print`, bodyParams)
          .then((res) => {
            console.log(res.data);
          })
          .catch((err) => {
            console.error(err);
          });
      } catch (error) {
        console.error("Erro ao carregar FingerprintJS:", error);
      }
    };

    getFingerprint();
  </script>
</html>
```

### Parâmetros do Código

- **accesskey**: Substitua `"your-access-key"` pela access key fornecida pela equipe da Credify.
- **action**: Descreva a ação que está sendo realizada quando a chamada à API é feita, como `"login"`, `"cadastro"`, `"consulta"`, etc.
- **document**: Informe o documento do usuário que está acessando a plataforma.
- **tipoDocument**: Informe o tipo de documento utilizando uma das seguintes opções: `"CPF"`, `"CNPJ"`, `"CNH"`, `"RG"`, ou `"OUTROS"`.

### Explicação do Código

1. **Carregamento do FingerprintJS**: O código importa dinamicamente a biblioteca FingerprintJS.
2. **Obtenção do Identificador do Visitante**: O identificador único do visitante é obtido e armazenado na variável `visitorId`.
3. **Criação dos Parâmetros do Corpo da Requisição**: Um objeto `bodyParams` é criado contendo `visitorId`, `accesskey`, `action`, `document`, e `tipoDocument`.
4. **Envio dos Dados para a Credify**: Utilizando Axios, os dados são enviados para o endpoint da Credify.

## Contato

Se você tiver alguma dúvida ou precisar de mais informações, entre em contato com a equipe da Credify.

---

Este README fornece uma visão geral de como implementar e utilizar o serviço de Device Fingerprint da Credify em sua aplicação JavaScript. Certifique-se de substituir os valores de exemplo pelos seus próprios dados antes de utilizar o código em produção.
