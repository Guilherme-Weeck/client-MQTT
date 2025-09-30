# MQTT Test Client — README

Este repositório contém um cliente MQTT leve para testes via WebSocket, pronto para hospedar no **GitHub Pages** ou rodar localmente. O cliente foi desenvolvido com `mqtt.js` (browser) e salva configurações/histórico no `localStorage` do navegador.

---

## Funcionalidades

* Conexão via WebSocket (ws:// / wss://) com ClientID, usuário/senha e keep-alive.
* Gerenciamento de múltiplos tópicos (inscrever/remover) com QoS configurável.
* Publicação com tópico, payload (texto/JSON), QoS e flag `retain`.
* Histórico de mensagens (enviadas/recebidas/infos/erros) com timestamps, filtragem por tópico/QoS.
* Persistência do estado (configurações, inscrições e log) usando `localStorage`.
* Export / Import de configuração completa em JSON.
* Baixar log como `.txt` e exportar configurações como `.json`.
* Atalhos: `Ctrl+Enter` para publicar.

---

## Arquivos

* `mqtt_client_pro.html` — cliente principal (renomear para `index.html` ao publicar no GitHub Pages).
* `README.md` — este arquivo com instruções.

---

## Requisitos e notas

* O cliente usa `mqtt.js` via CDN (`https://unpkg.com/mqtt/dist/mqtt.min.js`).
* Para conectar a brokers públicos, o broker precisa oferecer *WebSocket endpoint* (p.ex. `wss://broker.hivemq.com:8884/mqtt`).
* Se você publicar o site via `https://` (GitHub Pages), o broker deve usar `wss://` (WebSocket seguro) para evitar bloqueio de conteúdo misto.

---

## Testar localmente

1. Abra o arquivo `mqtt_client_pro.html` no navegador (arraste e solte no navegador). Observação: alguns navegadores bloqueiam conexões WebSocket a partir de `file://` — se tiver problemas, use um servidor HTTP local.

2. Com servidor HTTP local (exemplo usando Python 3):

```bash
# no diretório onde está mqtt_client_pro.html
python -m http.server 8000
# abra http://localhost:8000/mqtt_client_pro.html
```

3. Preencha o broker (ex: `wss://broker.hivemq.com:8884/mqtt`) e clique em *Conectar*. Inscreva tópicos, publique mensagens e observe o log.

---

## Publicar no GitHub Pages

1. Crie um repositório no GitHub ou use um existente.
2. Renomeie `mqtt_client_pro.html` para `index.html` (opcional: mantenha uma cópia original como `mqtt_client_pro.html`).
3. Commit e push para o repositório:

```bash
git init
git add index.html README.md
git commit -m "Add MQTT test client"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/NOME-DO-REPO.git
git push -u origin main
```

4. No GitHub: vá em *Settings → Pages* (ou *Site settings → Pages*) e ative GitHub Pages a partir da branch `main` (pasta `/ (root)`). A URL será `https://SEU-USUARIO.github.io/NOME-DO-REPO/`.

> Lembre: se a página estiver servindo via `https://`, o broker deve suportar `wss://`.

---

## Segurança e privacidade

* **Não** coloque credenciais sensíveis em repositórios públicos. Se precisar testar com credenciais, prefira usar o cliente localmente (não commitando senhas).
* O `localStorage` guarda configurações no navegador local — não é seguro para segredos.

---

## Troubleshooting (problemas comuns)

* **Conexão falha / timeout**: verifique se o broker aceita conexões WebSocket e se a URL está correta (porta e caminho). Teste com um broker público conhecido (ex: HiveMQ WebSocket).
* **Conteúdo misto**: página `https://` tentando `ws://` (não seguro) será bloqueada. Use `wss://` no broker.
* **Erro ao abrir arquivo local**: algumas políticas do navegador bloqueiam WebSocket a partir de `file://`. Use um servidor HTTP local (veja seção *Testar localmente*).

---

## Personalizações futuras (sugestões)

* Separar mensagens por abas por tópico.
* Visualizar payloads JSON de forma formatada / collapse-expand.
* Suporte a múltiplos clientes conectados simultaneamente.
* Integração com autenticação via OAuth / tokens (para brokers que suportem).

---

## Licença

MIT — sinta-se à vontade para adaptar para uso pessoal e testes. Se for publicar publicamente, não inclua segredos.

---

## Créditos

* Cliente MQTT: construído com `mqtt.js` ([https://github.com/mqttjs/MQTT.js](https://github.com/mqttjs/MQTT.js)).

Se quiser, posso também gerar o arquivo `index.html` já renomeado e um `.zip` com tudo pronto para upload ao GitHub — quer que eu gere esses arquivos para download?
