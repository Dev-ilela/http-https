# Relatório — Laboratório de Inspeção HTTP/HTTPS — Fluxo A (Administrador)

> **Como usar este template.** Preencha cada campo `[...]` com sua resposta e arraste as capturas de tela diretamente para os locais indicados. Preserve a formatação Markdown.
>
> **Escopo:** este fluxo inclui HTTP em texto claro, HTTPS sem decriptação e HTTPS com decriptação TLS pelo Fiddler Classic.

---

## Como anexar capturas de tela

1. Faça a captura de tela e salve como PNG.
2. No editor do GitHub ou GitHub.dev, posicione o cursor no local indicado.
3. Arraste o PNG para o editor. O GitHub inserirá uma linha `![image](...)`.

---

## Identificação

| Campo | Valor |
|---|---|
| Nome | Gabriel Vilela e Bianca Mendes|
| RA | 240209 e 240286 |
| Disciplina | Redes de Computadores |
| Turma | S.I. Noturno A |
| Data | 15/05/2026 |
| Fluxo | **A — Aluno com privilégio de administrador** |
| SO utilizado | [Windows 10 / Windows 11] |
| Ferramenta de proxy | Fiddler Classic |
| Navegador(es) | [Chrome / Edge / Firefox / ...] |
| Decriptação HTTPS habilitada? | [sim] |
| Certificado Fiddler instalado durante a atividade? | [sim] |

---

## Atividade 1 — Primeira captura

### Captura

<img width="1204" height="695" alt="Image 01" src="https://github.com/user-attachments/assets/3f3d67c4-a256-489e-b25b-078334afe8cb" />

**Request-line:**

```http
GET http://example.com/ HTTP/1.1
```

**Status-line:**

```http
HTTP/1.1 200 OK
```

**Cabeçalhos do request:**

| Cabeçalho | Função |
|---|---|
| User-Agent | Identifica ao servidor o navegador, sistema operacional e dispositivo (desktop ou mobile) que está fazendo a solicitação |
| Accept-Encoding: | Ele informa ao servidor quais tipos de conteúdo (formatos de dados) o cliente (navegador, aplicativo) consegue entender e processar |
| Accept-Language | Informa ao servidor quais idiomas o cliente (navegador) prefere e consegue entender, permitindo que o servidor envie o conteúdo no idioma correto |

**Resposta:**

| Campo | Valor observado |
|---|---|
| Content-Type | text/html | 
| Content-Length | 528 |

---

## Atividade 2 — Anatomia de um GET

### Captura

<img width="1203" height="984" alt="Image 02" src="https://github.com/user-attachments/assets/2bef2235-e8d0-4cc9-acbb-f96e87248a26" />

**Request-line completa:**

```http
GET https://http.aulasrede.com.br/get?aluno=Bianca&curso=redes HTTP/1.1
```

**Cabeçalhos-chave:**

| Cabeçalho | Valor |
|---|---|
| Host | http.aulasrede.com.br |
| User-Agent | Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36 |
| Accept | text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7 |

**Campos do JSON de resposta:**

```json
{
  "args": {
    "aluno": [
      "Bianca"
    ],
    "curso": [
      "redes"
    ]
  },
, 
  "headers": {
    "Accept": [
      "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7"
    ],
    "Accept-Language": [
      "pt-BR,pt;q=0.9,en-US;q=0.8,en;q=0.7"
    ],
    "Cache-Control": [
      "no-cache"
    ],
    "Host": [
      "func-http-aularedes-meta-w.azurewebsites.net"
    ],
...
},
  "origin": "200.210.165.75:13953",
}
```

**Resposta curta:** o que o campo `origin` representa? O `User-Agent` retornado coincide com o enviado?

O origin é o endereço IP da requisição + a porta. Sim.

---

## Atividade 3 — POST e envio de formulário

### Captura

<img width="1919" height="1043" alt="Image 03" src="https://github.com/user-attachments/assets/1c4927ed-f4bc-4f5e-bd7d-ca994b3b9729" />

**Request-line do POST:**

```http
POST https://http.aulasrede.com.br/post HTTP/1.1
```

| Cabeçalho | Valor |
|---|---|
| `Content-Type` | application/x-www-form-urlencoded |
| `Content-Length` | 103 |

**Corpo do request:**

```text
POST https://http.aulasrede.com.br/post HTTP/1.1
Host: http.aulasrede.com.br
Connection: keep-alive
Content-Length: 103
Cache-Control: max-age=0
sec-ch-ua: "Chromium";v="142", "Google Chrome";v="142", "Not_A Brand";v="99"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Origin: https://http.aulasrede.com.br
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: https://http.aulasrede.com.br/forms/post
Accept-Encoding: gzip, deflate, br, zstd
Accept-Language: pt-BR,pt;q=0.9,en-US;q=0.8,en;q=0.7

nome=Gabriel+Vilela&disciplina=Redes&observacao=Teste+de+formul%C3%A1rio+HTTP.+Uhuuuu&interesse=headers
```

**Campo `form` da resposta:**

```json
  "form": {
    "nome": [
      "Gabriel Vilela"
    ],
    "disciplina": [
      "Redes"
    ],
    "observacao": [
      "Teste de formulário HTTP. Uhuuuu"
    ],
    "interesse": [
      "headers"
    ]
  },
```

**Resposta curta:** qual formato codifica o corpo? Qual aba mostra literalmente os bytes enviados: `WebForms` ou `Raw`?

O 'Content-Type: application/json; charset=utf-8'. O Raw.

---

## Atividade 4 — Status codes

### Captura

<img width="723" height="298" alt="Image 04" src="https://github.com/user-attachments/assets/bb40d766-dd5f-404c-9d37-09ec6aae8a6e" />

| # | Método | URL | Status-line | Tamanho/body |
|---|---|---|---|---|
| 1 | GET | `https://http.aulasrede.com.br/status/200` | HTTP/1.1 200 OK | 38 |
| 2 | GET | `https://http.aulasrede.com.br/redirect-to?status_code=301&url=/get` | HTTP/1.1 200 OK | 3175 |
| 3 | GET | `https://http.aulasrede.com.br/status/404` | HTTP/1.1 404 Not Found | 45 |
| 4 | GET | `https://http.aulasrede.com.br/status/500` | HTTP/1.1 500 Internal Server Error | 57 |

**Resposta curta:** no `301`, qual cabeçalho informa o destino do redirecionamento?
Erro HTTP.

[resposta]

---

## Atividade 5 — Cabeçalhos essenciais

### Captura

<!-- arraste a captura aqui: Inspectors → Headers -->

| Cabeçalho | Req/Resp | Valor capturado | Função |
|---|---|---|---|
| `Host` | [...] | [...] | [...] |
| `User-Agent` | [...] | [...] | [...] |
| `Accept` | [...] | [...] | [...] |
| `Content-Type` | [...] | [...] | [...] |
| `Content-Length` / `Transfer-Encoding` | [...] | [...] | [...] |
| `Content-Encoding` | [...] | [...] | [...] |
| `Set-Cookie` | [...] | [...] | [...] |
| `Cache-Control` | [...] | [...] | [...] |
| `Strict-Transport-Security` | [...] | [...] | [...] |

**Resposta curta:** qual é o papel de `Content-Encoding` e de `Strict-Transport-Security`?

[resposta]

---

## Atividade 6 — HTTP vs HTTPS

### Captura — HTTP puro

<!-- arraste a captura aqui: http://http.aulasrede.com.br/get com redirecionamento 301 para HTTPS -->

### Captura — HTTPS sem decriptação

<!-- arraste a captura aqui: https://http.aulasrede.com.br/get sem decriptação -->

### Captura — HTTPS com decriptação

<!-- arraste a captura aqui: https://http.aulasrede.com.br/get com decriptação -->

| Situação | O que ficou visível? | O que ficou oculto? |
|---|---|---|
| HTTP puro | [...] | [...] |
| HTTPS sem decriptação | [...] | [...] |
| HTTPS com decriptação | [...] | [...] |

**Resposta curta:** por que a decriptação HTTPS pelo Fiddler exige instalar um certificado raiz?

[resposta]

---

## Atividade 7 — Cookies e sessão

### Captura

<!-- arraste a captura aqui: sequência cookies/set e cookies -->

| # | URL | `Set-Cookie` recebido | `Cookie` enviado |
|---|---|---|---|
| 1 | `/cookies/set?...` | [...] | [...] |
| 2 | `/cookies` | [...] | [...] |
| 3 | `/cookies` após recarregar | [...] | [...] |

**Resposta curta:** `Set-Cookie` apareceu em toda requisição ou apenas quando o servidor definiu/atualizou cookies? Quais atributos foram observados?

[resposta]

---

## Atividade 8 — Manipulação simples com breakpoint *(Opcional)*

### Captura

<!-- arraste a captura aqui: breakpoint com User-Agent editado -->

**JSON de resposta:**

```json
{
  "user-agent": ["[valor observado]"]
}
```

**Resposta curta:** o que este teste mostra sobre o papel ativo de um proxy?

[resposta]

- [ ] Breakpoints desabilitados ao final

---

## Reflexão final (opcional)

[até 10 linhas]

---

## Encerramento — Higiene de segurança

### Captura antes da remoção

<!-- arraste aqui a captura do certmgr.msc mostrando DO_NOT_TRUST_FiddlerRoot presente -->

### Captura depois da remoção

<!-- arraste aqui a captura mostrando o certificado ausente -->

- [ ] `Decrypt HTTPS traffic` desabilitado no Fiddler
- [ ] Certificado `DO_NOT_TRUST_FiddlerRoot` removido do Windows
- [ ] Certificado `DO_NOT_TRUST_FiddlerRoot` removido do Firefox, se aplicável
- [ ] Fiddler fechado

**Por que esta etapa é importante?**

[resposta curta]

---

## Checklist de entrega

- [ ] Campos `[...]` substituídos
- [ ] Capturas inseridas
- [ ] Atividades 1 a 7 preenchidas; Atividade 8 preenchida se executada
- [ ] Encerramento com duas capturas concluído
- [ ] PDF gerado como `SOBRENOME_NOME_RA_LAB_HTTP_FLUXOA.pdf`
- [ ] PDF submetido no Microsoft Teams
